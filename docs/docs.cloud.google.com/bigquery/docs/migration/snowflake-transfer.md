# Schedule a Snowflake transfer

**Preview**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

**Note:** To get support, provide feedback, or inquire about the limitations of this feature, contact <dts-migration-preview-support@google.com> .

The Snowflake connector provided by the BigQuery Data Transfer Service lets you schedule and manage automated transfer jobs to migrate data from Snowflake into BigQuery using public IP allow lists.

## Overview

The Snowflake connector engages migration agents in the Google Kubernetes Engine and triggers a load operation from Snowflake to a staging area within the same cloud provider where Snowflake is hosted.

  - For AWS-hosted Snowflake accounts, the data is first staged in your Amazon S3 bucket, which is then transferred to BigQuery with the BigQuery Data Transfer Service.
  - For Google Cloud-hosted Snowflake accounts, the data is first staged in your Cloud Storage bucket, which is then transferred to BigQuery with the BigQuery Data Transfer Service.
  - For Azure-hosted Snowflake accounts, the data is first staged in your Azure Blob Storage container, which is then transferred to BigQuery with the BigQuery Data Transfer Service.

## Limitations

Data transfers made using the Snowflake connector are subject to the following limitations:

  - The Snowflake connector only supports transfers from tables within a single Snowflake database and schema. To transfer from tables with multiple Snowflake databases or schemas, you can set up each transfer job separately.
  - The speed of loading data from Snowflake to your Amazon S3 bucket or Azure Blob Storage container or Cloud Storage bucket is limited by the Snowflake warehouse you have chosen for this transfer.

### Incremental transfer limitations

Incremental Snowflake transfers are subject to the following limitations:

  - You must provide primary key columns to use the upsert write mode. For more information, see [Defining primary keys for incremental transfers](#defining_primary_keys_for_incremental_transfers) .
  - Primary keys must be unique in the source table. If duplicates exist, the results of the merge operation in BigQuery might be inconsistent and not match the source data.
  - The automatic handling of schema changes with incremental transfers is not supported. If the schema of a source table changes, you must manually update the BigQuery table schema.
  - Incremental transfers work best when changes in your source data are concentrated within a small number of partitions. Incremental transfer performance can degrade significantly if updates are scattered across the source table, as this requires scanning many partitions. If you have many rows that are changed between data transfers, then we recommend that you use a full transfer instead.
  - Some operations in Snowflake, such as `  CREATE OR REPLACE TABLE  ` or `  CLONE  ` , can overwrite the original table object and its associated change tracking history. This makes existing data transfers stale and requires a new full sync to resume incremental transfers.
  - Incremental transfers must be run frequently enough to stay within [Snowflake's data retention period](https://docs.snowflake.com/en/user-guide/data-time-travel#data-retention-period) for change tracking. If the last successful transfer is run outside of this window, then the next transfer will be a full transfer.

## Data ingestion behavior

You can specify how data is loaded into BigQuery by selecting either the **Full** or **Incremental** write preference in the transfer configuration when you [set up a Snowflake transfer](#set-up-transfer) . Incremental transfers are supported in [Preview](https://cloud.google.com/products#product-launch-stages) .

**Note:** To request feedback or support for incremental transfers, send email to <dts-preview-support@google.com> .

You can select **Full** to transfer all data from your Snowflake datasets with each data transfer.

Alternatively, you can select **Incremental** ( [Preview](https://cloud.google.com/products#product-launch-stages) ) to only transfer data that was changed since the last data transfer, instead of loading the entire dataset with each data transfer. If you select **Incremental** for your data transfer, you must specify either the **Append** or **Upsert** write modes to define how data is written to BigQuery during an incremental data transfer. The following sections describe the available write modes.

#### **Append** write mode

The **Append** write mode only inserts new rows to your destination table. This option strictly appends transferred data without checking for existing records, so this mode can potentially cause data duplication in the destination table.

When you select the **Append** mode, you must select a watermark column. A watermark column is required for the Snowflake connector to track changes in the source table.

#### **Upsert** write mode

The **Upsert** write mode either updates a row or inserts a new row in your destination table by checking for a primary key. You can specify a primary key to let the Snowflake connector determine what changes are needed to keep your destination table up-to-date with your source table. If the specified primary key is present in the destination BigQuery table during a data transfer, then the Snowflake connector updates that row with new data from the source table. If a primary key is not present during a data transfer, then the Snowflake connector inserts a new row.

When you select the **Upsert** mode, you must select a watermark column and a primary key:

  - The primary key can be one or more columns on your table that are required for the Snowflake connector to determine if it needs to insert or update a row.
      - Select columns that contain non-null values that are unique across all rows of the table. We recommend columns that include system-generated identifiers, unique reference codes (for example, auto-incrementing IDs), or immutable time-based sequence IDs.
      - To prevent potential data loss or data corruption, the primary key columns that you select must have unique values. If you have doubts about the uniqueness of your chosen primary key column, then we recommend that you use the **Append** write mode instead.

To use the upsert write mode with your incremental data transfer, you must [define primary keys in your custom schema file](/bigquery/docs/migration/snowflake-transfer#defining_primary_keys_for_incremental_transfers) .

## Before you begin

Before you set up a Snowflake transfer, you must perform all the steps listed in this section. The following is a list of all required steps.

1.  [Prepare your Google Cloud project](#preparing-gcp-project)
2.  [Required BigQuery roles](#required-roles)
3.  [Prepare your staging bucket](#preparing-staging-bucket)
4.  [Create a Snowflake user with the required permissions](#create-snowflake-user)
5.  [Add network policies](#add_network_policies)
6.  Optional: [Schema detection and mapping](#schema_detection_and_mapping)
7.  [Assess your Snowflake for any unsupported data types](#assess-snowflake-data)
8.  Optional: [Enable incremental transfers](#enable_incremental_transfers)
9.  [Gather transfer information](#gather_transfer_information)
10. If you plan on specifying a customer-managed encryption key (CMEK), ensure that your [service account has permissions to encrypt and decrypt](/bigquery/docs/customer-managed-encryption#grant_permission) , and that you have the [Cloud KMS key resource ID](/bigquery/docs/customer-managed-encryption#key_resource_id) required to use CMEK. For information about how CMEK works with the transfers, see [Specify encryption key with transfers](#CMEK) .

### Prepare your Google Cloud project

Create and configure your Google Cloud project for a Snowflake transfer with the following steps:

1.  [Create a Google Cloud project](/resource-manager/docs/creating-managing-projects) or select an existing project.
    
    **Note:** If you don't plan on keeping the resources created during this Snowflake transfer, create a new Google Cloud project instead of selecting an existing one. You can then delete the project once you are done with your Snowflake transfer.

2.  Verify that you have completed all actions required to [enable the BigQuery Data Transfer Service](/bigquery/docs/enable-transfer-service) .

3.  [Create a BigQuery dataset](/bigquery/docs/datasets) to store your data. You don't need to create any tables.

### Required BigQuery roles

To get the permissions that you need to create a BigQuery Data Transfer Service data transfer, ask your administrator to grant you the [BigQuery Admin](/iam/docs/roles-permissions/bigquery#bigquery.admin) ( `  roles/bigquery.admin  ` ) IAM role on your project. For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

This predefined role contains the permissions required to create a BigQuery Data Transfer Service data transfer. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

The following permissions are required to create a BigQuery Data Transfer Service data transfer:

  - BigQuery Data Transfer Service permissions:
      - `  bigquery.transfers.update  `
      - `  bigquery.transfers.get  `
  - BigQuery permissions:
      - `  bigquery.datasets.get  `
      - `  bigquery.datasets.getIamPolicy  `
      - `  bigquery.datasets.update  `
      - `  bigquery.datasets.setIamPolicy  `
      - `  bigquery.jobs.create  `

You might also be able to get these permissions with [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

For more information, see [Grant `  bigquery.admin  ` access](/bigquery/docs/enable-transfer-service#grant_bigqueryadmin_access) .

**Note:** For ease of selection of your service account and the Cloud Storage bucket URI during transfer creation, we recommend that you grant the `  iam.serviceAccounts.list  ` and `  storage.buckets.list  ` permissions on the user creating the transfer configuration.

### Prepare staging bucket

To complete a Snowflake data transfer, you must create a staging bucket and then configure it to allow write access from Snowflake.

#### Staging bucket for AWS-hosted Snowflake account

For AWS-hosted Snowflake account, create an Amazon S3 bucket to stage the Snowflake data before it is loaded into BigQuery.

1.  [Create an Amazon S3 bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/create-bucket-overview.html) .

2.  [Create and configure a Snowflake storage integration object](https://docs.snowflake.com/en/user-guide/data-load-s3-config-storage-integration) to allow Snowflake to write data into the Amazon S3 bucket as an external stage.

To allow read access on your Amazon S3 bucket, you must also do the following:

1.  Create a dedicated [Amazon IAM user](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users.html) and grant it the [AmazonS3ReadOnlyAccess](https://docs.aws.amazon.com/aws-managed-policy/latest/reference/AmazonS3ReadOnlyAccess.html) policy.

2.  [Create an Amazon access key pair](https://docs.aws.amazon.com/keyspaces/latest/devguide/create.keypair.html) for the IAM user.

#### Staging Azure Blob Storage container for Azure-hosted Snowflake account

For Azure-hosted Snowflake accounts, create a Azure Blob Storage container to stage the Snowflake data before it is loaded into BigQuery.

1.  [Create an Azure storage account](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-create) and a [storage container](https://learn.microsoft.com/en-us/azure/storage/blobs/blob-containers-portal#create-a-container) within it.
2.  <span id="storage-azure-integration-container">[Create and configure a Snowflake storage integration object](https://docs.snowflake.com/en/user-guide/data-load-azure-config#option-1-configuring-a-snowflake-storage-integration) to allow Snowflake to write data into the Azure storage container as an external stage. Note that 'Step 3: Creating an external stage' can be skipped as we don't use it.</span>

To allow read access on your Azure container, [generate a SAS Token](https://learn.microsoft.com/en-us/azure/ai-services/translator/document-translation/how-to-guides/create-sas-tokens?tabs=Containers#create-sas-tokens-in-the-azure-portal) for it.

#### Staging bucket for Google Cloud-hosted Snowflake account

For Google Cloud-hosted Snowflake accounts, create a Cloud Storage bucket to stage the Snowflake data before it is loaded into BigQuery.

1.  [Create a Cloud Storage bucket](/storage/docs/creating-buckets) .

2.  <span id="storage-gcs-integration-bucket">[Create and configure a Snowflake storage integration object](https://docs.snowflake.com/en/user-guide/data-load-gcs-config) to allow Snowflake to write data into the Cloud Storage bucket as an external stage.</span>

3.  To allow access to staging bucket, Grant [DTS service agent](/bigquery/docs/enable-transfer-service#service_agent) the `  roles/storage.objectViewer  ` role with the following command:
    
    ``` text
    gcloud storage buckets add-iam-policy-binding gs://STAGING_BUCKET_NAME \
      --member=serviceAccount:service-PROJECT_NUMBER@gcp-sa-bigquerydatatransfer.iam.gserviceaccount.com \
      --role=roles/storage.objectViewer
    ```

### Create a Snowflake user with the required permissions

During a Snowflake transfer, the Snowflake connector connects to your Snowflake account using a JDBC connection. You must create a new Snowflake user with a custom role that only has the necessary privileges to perform the data transfer:

``` text
  // Create and configure new role, MIGRATION_ROLE
  GRANT USAGE
    ON WAREHOUSE WAREHOUSE_NAME
    TO ROLE MIGRATION_ROLE;

  GRANT USAGE
    ON DATABASE DATABASE_NAME
    TO ROLE MIGRATION_ROLE;

  GRANT USAGE
    ON SCHEMA DATABASE_NAME.SCHEMA_NAME
    TO ROLE MIGRATION_ROLE;

  // You can modify this to give select permissions for all tables in a schema
  GRANT SELECT
    ON TABLE DATABASE_NAME.SCHEMA_NAME.TABLE_NAME
    TO ROLE MIGRATION_ROLE;

  GRANT USAGE
    ON STORAGE_INTEGRATION_OBJECT_NAME
    TO ROLE MIGRATION_ROLE;
```

Replace the following:

  - `  MIGRATION_ROLE  ` : the name of the custom role you are creating
  - `  WAREHOUSE_NAME  ` : the name of your data warehouse
  - `  DATABASE_NAME  ` : the name of your Snowflake database
  - `  SCHEMA_NAME  ` : the name of your Snowflake schema
  - `  TABLE_NAME  ` : the name of the Snowflake included in this data transfer
  - `  STORAGE_INTEGRATION_OBJECT_NAME  ` : the name of your Snowflake storage integration object.

#### Generate key pair for authentication

Due to the [deprecation of single factor password sign-ins by Snowflake](https://docs.snowflake.com/en/user-guide/security-mfa-rollout) , we recommend that you use key pair for authentication.

You can configure a key pair by generating an encrypted or unencrypted RSA key pair, then assigning the public key to a Snowflake user. For more information, see [Configuring key-pair authentication](https://docs.snowflake.com/en/user-guide/key-pair-auth#configuring-key-pair-authentication) .

### Add network policies

For public connectivity, the Snowflake account allows public connection with database credentials by default. However, you might have configured network rules or policies that could prevent the Snowflake connector from connecting to your account. In this case, you must add the necessary IP addresses to your allowlist.

The following table is a list of IP addresses for the regional and multi-regional locations used for public transfers. You can either add the IP addresses that only correspond to your dataset's location, or you can add all the IP addresses listed in the table. These are IP addresses reserved by Google for BigQuery Data Transfer Service data transfers.

To add an IP address to an allowlist, do the following:

1.  [Create a network rule](https://docs.snowflake.com/en/sql-reference/sql/create-network-rule) with `  type  ` = `  IPV4  ` . The BigQuery Data Transfer Service uses a JDBC connection to connect to the Snowflake account.
2.  [Create a network policy](https://docs.snowflake.com/en/sql-reference/sql/create-network-policy) with the network rule that you created earlier and the IP address from the following table.

**Caution:** The communication between BigQuery and Snowflake happens through the following Google-owned IP addresses. However, the data movement from Amazon S3 to BigQuery happens over the public internet.

#### Regional locations

Region description

Region name

IP addresses

**Americas**

Columbus, Ohio

`  us-east5  `

34.162.72.184  
34.162.173.185  
34.162.205.205  
34.162.81.45  
34.162.182.149  
34.162.59.92  
34.162.157.190  
34.162.191.145

Dallas

`  us-south1  `

34.174.172.89  
34.174.40.67  
34.174.5.11  
34.174.96.109  
34.174.148.99  
34.174.176.19  
34.174.253.135  
34.174.129.163

Iowa

`  us-central1  `

34.121.70.114  
34.71.81.17  
34.122.223.84  
34.121.145.212  
35.232.1.105  
35.202.145.227  
35.226.82.216  
35.225.241.102

Las Vegas

`  us-west4  `

34.125.53.201  
34.125.69.174  
34.125.159.85  
34.125.152.1  
34.125.195.166  
34.125.50.249  
34.125.68.55  
34.125.91.116

Los Angeles

`  us-west2  `

35.236.59.167  
34.94.132.139  
34.94.207.21  
34.94.81.187  
34.94.88.122  
35.235.101.187  
34.94.238.66  
34.94.195.77

Mexico

`  northamerica-south1  `

34.51.6.35  
34.51.7.113  
34.51.12.83  
34.51.10.94  
34.51.11.219  
34.51.11.52  
34.51.2.114  
34.51.15.251

Montréal

`  northamerica-northeast1  `

34.95.20.253  
35.203.31.219  
34.95.22.233  
34.95.27.99  
35.203.12.23  
35.203.39.46  
35.203.116.49  
35.203.104.223

Northern Virginia

`  us-east4  `

35.245.95.250  
35.245.126.228  
35.236.225.172  
35.245.86.140  
35.199.31.35  
35.199.19.115  
35.230.167.48  
35.245.128.132  
35.245.111.126  
35.236.209.21

Oregon

`  us-west1  `

35.197.117.207  
35.199.178.12  
35.197.86.233  
34.82.155.140  
35.247.28.48  
35.247.31.246  
35.247.106.13  
34.105.85.54

Salt Lake City

`  us-west3  `

34.106.37.58  
34.106.85.113  
34.106.28.153  
34.106.64.121  
34.106.246.131  
34.106.56.150  
34.106.41.31  
34.106.182.92

São Paolo

`  southamerica-east1  `

35.199.88.228  
34.95.169.140  
35.198.53.30  
34.95.144.215  
35.247.250.120  
35.247.255.158  
34.95.231.121  
35.198.8.157

Santiago

`  southamerica-west1  `

34.176.188.48  
34.176.38.192  
34.176.205.134  
34.176.102.161  
34.176.197.198  
34.176.223.236  
34.176.47.188  
34.176.14.80

South Carolina

`  us-east1  `

35.196.207.183  
35.237.231.98  
104.196.102.222  
35.231.13.201  
34.75.129.215  
34.75.127.9  
35.229.36.137  
35.237.91.139

Toronto

`  northamerica-northeast2  `

34.124.116.108  
34.124.116.107  
34.124.116.102  
34.124.116.80  
34.124.116.72  
34.124.116.85  
34.124.116.20  
34.124.116.68

**Europe**

Belgium

`  europe-west1  `

35.240.36.149  
35.205.171.56  
34.76.234.4  
35.205.38.234  
34.77.237.73  
35.195.107.238  
35.195.52.87  
34.76.102.189

Berlin

`  europe-west10  `

34.32.28.80  
34.32.31.206  
34.32.19.49  
34.32.33.71  
34.32.15.174  
34.32.23.7  
34.32.1.208  
34.32.8.3

Finland

`  europe-north1  `

35.228.35.94  
35.228.183.156  
35.228.211.18  
35.228.146.84  
35.228.103.114  
35.228.53.184  
35.228.203.85  
35.228.183.138

Frankfurt

`  europe-west3  `

35.246.153.144  
35.198.80.78  
35.246.181.106  
35.246.211.135  
34.89.165.108  
35.198.68.187  
35.242.223.6  
34.89.137.180

London

`  europe-west2  `

35.189.119.113  
35.189.101.107  
35.189.69.131  
35.197.205.93  
35.189.121.178  
35.189.121.41  
35.189.85.30  
35.197.195.192

Madrid

`  europe-southwest1  `

34.175.99.115  
34.175.186.237  
34.175.39.130  
34.175.135.49  
34.175.1.49  
34.175.95.94  
34.175.102.118  
34.175.166.114

Milan

`  europe-west8  `

34.154.183.149  
34.154.40.104  
34.154.59.51  
34.154.86.2  
34.154.182.20  
34.154.127.144  
34.154.201.251  
34.154.0.104

Netherlands

`  europe-west4  `

35.204.237.173  
35.204.18.163  
34.91.86.224  
34.90.184.136  
34.91.115.67  
34.90.218.6  
34.91.147.143  
34.91.253.1

Paris

`  europe-west9  `

34.163.76.229  
34.163.153.68  
34.155.181.30  
34.155.85.234  
34.155.230.192  
34.155.175.220  
34.163.68.177  
34.163.157.151

Stockholm

`  europe-north2  `

34.51.133.48  
34.51.136.177  
34.51.128.140  
34.51.141.252  
34.51.139.127  
34.51.142.55  
34.51.134.218  
34.51.138.9

Turin

`  europe-west12  `

34.17.15.186  
34.17.44.123  
34.17.41.160  
34.17.47.82  
34.17.43.109  
34.17.38.236  
34.17.34.223  
34.17.16.47

Warsaw

`  europe-central2  `

34.118.72.8  
34.118.45.245  
34.118.69.169  
34.116.244.189  
34.116.170.150  
34.118.97.148  
34.116.148.164  
34.116.168.127

Zürich

`  europe-west6  `

34.65.205.160  
34.65.121.140  
34.65.196.143  
34.65.9.133  
34.65.156.193  
34.65.216.124  
34.65.233.83  
34.65.168.250

**Asia Pacific**

Bangkok

`  asia-southeast3  `

34.15.142.80  
34.15.131.78  
34.15.141.141  
34.15.143.6  
34.15.142.166  
34.15.138.0  
34.15.135.129  
34.15.139.45

Delhi

`  asia-south2  `

34.126.212.96  
34.126.212.85  
34.126.208.224  
34.126.212.94  
34.126.208.226  
34.126.212.232  
34.126.212.93  
34.126.212.206

Hong Kong

`  asia-east2  `

34.92.245.180  
35.241.116.105  
35.220.240.216  
35.220.188.244  
34.92.196.78  
34.92.165.209  
35.220.193.228  
34.96.153.178

Jakarta

`  asia-southeast2  `

34.101.79.105  
34.101.129.32  
34.101.244.197  
34.101.100.180  
34.101.109.205  
34.101.185.189  
34.101.179.27  
34.101.197.251

Melbourne

`  australia-southeast2  `

34.126.196.95  
34.126.196.106  
34.126.196.126  
34.126.196.96  
34.126.196.112  
34.126.196.99  
34.126.196.76  
34.126.196.68

Mumbai

`  asia-south1  `

34.93.67.112  
35.244.0.1  
35.200.245.13  
35.200.203.161  
34.93.209.130  
34.93.120.224  
35.244.10.12  
35.200.186.100

Osaka

`  asia-northeast2  `

34.97.94.51  
34.97.118.176  
34.97.63.76  
34.97.159.156  
34.97.113.218  
34.97.4.108  
34.97.119.140  
34.97.30.191

Seoul

`  asia-northeast3  `

34.64.152.215  
34.64.140.241  
34.64.133.199  
34.64.174.192  
34.64.145.219  
34.64.136.56  
34.64.247.158  
34.64.135.220

Singapore

`  asia-southeast1  `

34.87.12.235  
34.87.63.5  
34.87.91.51  
35.198.197.191  
35.240.253.175  
35.247.165.193  
35.247.181.82  
35.247.189.103

Sydney

`  australia-southeast1  `

35.189.33.150  
35.189.38.5  
35.189.29.88  
35.189.22.179  
35.189.20.163  
35.189.29.83  
35.189.31.141  
35.189.14.219

Taiwan

`  asia-east1  `

35.221.201.20  
35.194.177.253  
34.80.17.79  
34.80.178.20  
34.80.174.198  
35.201.132.11  
35.201.223.177  
35.229.251.28  
35.185.155.147  
35.194.232.172

Tokyo

`  asia-northeast1  `

34.85.11.246  
34.85.30.58  
34.85.8.125  
34.85.38.59  
34.85.31.67  
34.85.36.143  
34.85.32.222  
34.85.18.128  
34.85.23.202  
34.85.35.192

**Middle East**

Dammam

`  me-central2  `

34.166.20.177  
34.166.10.104  
34.166.21.128  
34.166.19.184  
34.166.20.83  
34.166.18.138  
34.166.18.48  
34.166.23.171  

Doha

`  me-central1  `

34.18.48.121  
34.18.25.208  
34.18.38.183  
34.18.33.25  
34.18.21.203  
34.18.21.80  
34.18.36.126  
34.18.23.252

Tel Aviv

`  me-west1  `

34.165.184.115  
34.165.110.74  
34.165.174.16  
34.165.28.235  
34.165.170.172  
34.165.187.98  
34.165.85.64  
34.165.245.97

**Africa**

Johannesburg

`  africa-south1  `

34.35.11.24  
34.35.10.66  
34.35.8.32  
34.35.3.248  
34.35.2.113  
34.35.5.61  
34.35.7.53  
34.35.3.17

#### Multi-regional locations

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Multi-region description</th>
<th>Multi-region name</th>
<th>IP addresses</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Data centers within <a href="https://europa.eu/european-union/about-eu/countries_en" class="external">member states</a> of the European Union <sup>1</sup></td>
<td><code dir="ltr" translate="no">       EU      </code></td>
<td>34.76.156.158<br />
34.76.156.172<br />
34.76.136.146<br />
34.76.1.29<br />
34.76.156.232<br />
34.76.156.81<br />
34.76.156.246<br />
34.76.102.206<br />
34.76.129.246<br />
34.76.121.168</td>
</tr>
<tr class="even">
<td>Data centers in the United States</td>
<td><code dir="ltr" translate="no">       US      </code></td>
<td>35.185.196.212<br />
35.197.102.120<br />
35.185.224.10<br />
35.185.228.170<br />
35.197.5.235<br />
35.185.206.139<br />
35.197.67.234<br />
35.197.38.65<br />
35.185.202.229<br />
35.185.200.120</td>
</tr>
</tbody>
</table>

<sup>1</sup> Data located in the `  EU  ` multi-region is not stored in the `  europe-west2  ` (London) or `  europe-west6  ` (Zürich) data centers.

### Schema detection and mapping

To define your schema, you can use the BigQuery Data Transfer Service to automatically detect schema and data-type mapping when transferring data from Snowflake to BigQuery. Alternatively, you can use the translation engine to define your schema and data types manually.

#### Custom schema file

You can use a custom schema file to define primary keys for incremental transfers and to customize schema mapping. A custom schema file is a JSON file that describes the source and target schema.

##### Defining primary keys for incremental transfers

For incremental transfers in **Upsert** mode, you must identify one or more columns as primary keys. To do this, annotate the columns with the `  PRIMARY_KEY  ` usage type in the custom schema file.

The following example shows a custom schema file that defines `  O_ORDERKEY  ` and `  O_ORDERDATE  ` as primary keys for the `  orders  ` table:

``` text
{
  "databases": [
    {
      "name": "my_db",
      "originalName": "my_db",
      "tables": [
        {
          "name": "orders",
          "originalName": "orders",
          "columns": [
            {
              "name": "O_ORDERKEY",
              "originalName": "O_ORDERKEY",
              "usageType": [
                "PRIMARY_KEY"
              ]
            },
            {
              "name": "O_ORDERDATE",
              "originalName": "O_ORDERDATE",
              "usageType": [
                "PRIMARY_KEY"
              ]
            }
          ]
        }
      ]
    }
  ]
}
```

#### Default Schema Detection

The Snowflake connector can automatically detect your Snowflake table schema. To use automatic schema detection, you can leave the **Translation output GCS path** field blank when you [set up a Snowflake transfer](#set-up-transfer) .

The following list shows how the Snowflake connector maps your Snowflake data types into BigQuery:

  - The following data types are mapped as `  STRING  ` in BigQuery:
      - `  TIMESTAMP_TZ  `
      - `  TIMESTAMP_LTZ  `
      - `  OBJECT  `
      - `  VARIANT  `
      - `  ARRAY  `
  - The following data types are mapped as `  TIMESTAMP  ` in BigQuery:
      - `  TIMESTAMP_NTZ  `

All other Snowflake data types are mapped directly to their equivalent types in BigQuery.

#### Using translation engine output for schema

To define your schema manually (for example, to override certain schema attributes), you can generate your metadata and run the translation engine with the following steps:

##### Limitations

  - Data is extracted from Snowflake in the Parquet data format before it is loaded into BigQuery:
    
      - The following Parquet data types are unsupported:
        
          - `  TIMESTAMP_TZ  ` , `  TIMESTAMP_LTZ  `
          - For more information, see [Assess Snowflake data](#assess-snowflake-data) .
    
      - The following Parquet data types are unsupported, but can be converted:
        
          - `  TIMESTAMP_NTZ  `
          - `  OBJECT  ` , `  VARIANT  ` , `  ARRAY  `
        
        Use the [global type conversion configuration YAML](/bigquery/docs/config-yaml-translation#global_type_conversion) to override the default behavior of these data types when you run translation engine.
        
        The configuration YAML might look similar to the following example:
        
        ``` text
        type: experimental_object_rewriter
        global:
          typeConvert:
            datetime: TIMESTAMP
            json: VARCHAR
        ```

The BigQuery Data Transfer Service for Snowflake connector uses the BigQuery migration service translation engine for schema mapping when migrating Snowflake tables into BigQuery. To complete a Snowflake data transfer, you must first generate metadata for translation, then run the translation engine:

1.  Run the `  dwh-migration-tool  ` for Snowflake. For more information, see [Generate metadata for translation and assessment](/bigquery/docs/generate-metadata#snowflake) .

2.  Upload the generated `  metadata.zip  ` file to a Cloud Storage bucket. The `  metadata.zip  ` file is used as input for the translation engine.

3.  Run the batch translation service, specifying the `  target_types  ` field as `  metadata  ` . For more information, see [Translate SQL queries with the translation API](/bigquery/docs/api-sql-translator) .
    
      - The following is an example of a command to run a batch translation for Snowflake:
    
    <!-- end list -->
    
    ``` text
      curl -d "{
      \"name\": \"sf_2_bq_translation\",
      \"displayName\": \"Snowflake to BigQuery Translation\",
      \"tasks\": {
          string: {
            \"type\": \"Snowflake2BigQuery_Translation\",
            \"translation_details\": {
                \"target_base_uri\": \"gs://sf_test_translation/output\",
                \"source_target_mapping\": {
                  \"source_spec\": {
                      \"base_uri\": \"gs://sf_test_translation/input\"
                  }
                },
                \"target_types\": \"metadata\",
            }
          }
      },
      }" \
      -H "Content-Type:application/json" \
      -H "Authorization: Bearer TOKEN" -X POST https://bigquerymigration.googleapis.com/v2alpha/projects/project_id/locations/location/workflows
    ```
    
      - You can check the status of this command in the [SQL Translation page](https://console.cloud.google.com/bigquery/migrations/batch-translation) in BigQuery. The output of the batch translation job is stored in `  gs://translation_target_base_uri/metadata/config/  ` .

#### Required service account permissions

In a Snowflake transfer, a service account is used to read data from the translation engine output in the specified Cloud Storage path. You must grant the service account the `  storage.objects.get  ` and the `  storage.objects.list  ` permissions.

We recommend that the service account belongs to the same Google Cloud project where the transfer configuration and destination dataset is created. If the service account is in a Google Cloud project that is different from the project that created the BigQuery data transfer, then you must [enable cross-project service account authorization](/bigquery/docs/enable-transfer-service#cross-project_service_account_authorization) .

For more information, see [BigQuery IAM roles and permissions](/bigquery/docs/access-control) .

### Assess Snowflake data

BigQuery writes data from Snowflake to Cloud Storage as Parquet files. Parquet files don't support the [`  TIMESTAMP_TZ  ` and `  TIMESTAMP_LTZ  `](https://community.snowflake.com/s/article/How-To-Unload-Timestamp-data-in-a-Parquet-file) data types. If your data contains these types, you can export it to Amazon S3 as CSV files and then import the CSV files into BigQuery. For more information, see [Overview of Amazon S3 transfers](/bigquery/docs/s3-transfer-intro) .

### Enable incremental transfers

Before you can set up an incremental Snowflake transfer, you must enable change tracking on each source table with the following command:

``` text
ALTER TABLE DATABASE_NAME.SCHEMA_NAME.TABLE_NAME SET CHANGE_TRACKING = TRUE;
```

If change tracking is not enabled for a table, then the Snowflake connector defaults to a full data transfer for that table.

### Gather transfer information

Gather the information that you need to set up the migration with the BigQuery Data Transfer Service:

  - Your Snowflake account identifier, which is the prefix in your Snowflake account URL. For example, `  ACCOUNT_IDENTIFIER .snowflakecomputing.com  ` .
  - The username and the associated private key with appropriate permissions to your Snowflake database. It can just have the [required permissions to execute the data transfer](#create-snowflake-user) .
  - The URI of the staging bucket that you want to use for the transfer:
      - For an AWS-hosted Snowflake account, an [Amazon S3 bucket URI](#preparing-s3-bucket) is required along with access credentials.
      - For an Azure-hosted Snowflake, an [Azure Blob Storage account and container](#preparing-azure-container) is required.
      - <span id="staging_bucket_uri">For a Google Cloud-hosted Snowflake account, a [Cloud Storage bucket URI](#preparing-gcs-bucket) is required. We recommend that you set up a lifecycle policy for this bucket to avoid unnecessary charges.</span>
  - The URI of the Cloud Storage bucket where you have stored the [schema mapping files obtained from the translation engine](#schema_detection_and_mapping) .

## Set up a Snowflake transfer

Select one of the following options:

### Console

1.  Go to the Data transfers page in the Google Cloud console.

2.  Click add **Create transfer** .

3.  In the **Source type** section, select **Snowflake Migration** from the **Source** list.

4.  In the **Transfer config name** section, enter a name for the transfer, such as `  My migration  ` , in the **Display name** field. The display name can be any value that lets you identify the transfer if you need to modify it later.

5.  In the **Destination settings** section, choose [the dataset you created](#preparing-gcp-project) from the **Dataset** list.

6.  In the **Data source details** section, do the following:
    
    1.  For **Account identifier** , enter a unique identifier for your Snowflake account, which is a combination of your organization name and account name. The identifier is the prefix of Snowflake account URL and not the complete URL. For example, `  ACCOUNT_IDENTIFIER .snowflakecomputing.com  ` .
    
    2.  For **Username** , enter the username of the Snowflake user whose credentials and authorization is used to access your database to transfer the Snowflake tables. We recommend using [the user that you created for this transfer](#create-snowflake-user) .
    
    3.  For **Auth mechanism** , select a Snowflake user authentication method. For more information, see [Generate key pair for authentication](#generate_key_pair_for_authentication)
    
    4.  For **Password** , enter the password of the Snowflake user. This field is required if you have selected **PASSWORD** in the **Auth mechanism** field.
    
    5.  For **Private key** , enter the private key linked with the [public key associated with the Snowflake user](#create-snowflake-user) . This field is required if you have selected **KEY\_PAIR** in the **Auth mechanism** field.
    
    6.  For **Is Private key encrypted** , select this field if the private key is encrypted with a passphrase.
    
    7.  For **Private key passphrase** , enter the passphrase for the encrypted private key. This field is required if you have selected **KEY\_PAIR** in the **Auth mechanism** and **Is Private Key Encrypted** fields.
    
    8.  For **Warehouse** , enter a [warehouse](https://docs.snowflake.com/en/user-guide/warehouses-tasks) that is used for the execution of this data transfer.
    
    9.  For **Service account** , enter a service account to use with this data transfer. The service account should belong to the same Google Cloud project where the transfer configuration and destination dataset is created. The service account must have the `  storage.objects.list  ` and `  storage.objects.get  ` [required permissions](#required_service_account_permissions) .
    
    10. For **Database** , enter the name of the Snowflake database that contains the tables included in this data transfer.
    
    11. For **Schema** , enter the name of the Snowflake schema that contains the tables included in this data transfer.
    
    12. For **Table name patterns** , specify a table to transfer by entering a name or a pattern that matches the table name in the schema. You can use regular expressions to specify the pattern, for example `  table1_regex ; table2_regex  ` . The pattern should follow Java regular expression syntax. For example,
        
          - `  lineitem;ordertb  ` matches tables that are named `  lineitem  ` and `  ordertb  ` .
          - `  .*  ` matches all tables.
    
    13. For **Ingestion mode** , select **FULL** or **INCREMENTAL** . For more information, see [Data ingestion behavior](#data-ingestion) .
    
    14. Optional: For **Translation output GCS path** , specify a path to the Cloud Storage folder that contains the [schema mapping files from the translation engine](#schema_detection_and_mapping) . You can leave this empty to have the Snowflake connector automatically detect your schema.
        
          - The path should follow the format `  translation_target_base_uri /metadata/config/db/schema/  ` and must end with `  /  ` .
    
    15. For **Storage integration object name** , enter the name of the Snowflake storage integration object.
    
    16. For **Cloud provider** , select `  AWS  ` or `  AZURE  ` or `  GCP  ` depending on which cloud provider is hosting your Snowflake account.
    
    17. For **Amazon S3 URI** , enter the [URI of the Amazon S3 bucket](#preparing-s3-bucket) to use as a staging area. Only required when your **Cloud Provider** is `  AWS  ` .
    
    18. For **Access key ID** and **Secret access key** , enter the [access key pair](#snowflake_key_pair) . Only required when your **Cloud Provider** is `  AWS  ` .
    
    19. For **Azure Storage Account** and **Azure Storage Container** , enter the [storage account and container name of the Azure Blob Storage](#preparing-azure-container) to use as a staging area. Only required when your **Cloud Provider** is `  AZURE  ` .
    
    20. For **SAS Token** , enter the [SAS token generated for the container](#azure_sas_token) . Only required when your **Cloud Provider** is `  AZURE  ` .
    
    21. For **GCS URI** , enter the [URI of the Cloud Storage](#preparing-gcs-bucket) to use as a staging area. Only required when your **Cloud Provider** is `  GCP  ` .

7.  Optional: In the **Notification options** section, do the following:
    
    1.  Click the toggle to enable email notifications. When you enable this option, the transfer administrator receives an email notification when a transfer run fails.
    2.  For **Select a Pub/Sub topic** , choose your [topic](/pubsub/docs/overview#types) name or click **Create a topic** . This option configures Pub/Sub run [notifications](/bigquery/docs/transfer-run-notifications) for your transfer.

8.  If you use [CMEKs](/bigquery/docs/customer-managed-encryption) , in the **Advanced options** section, select **Customer-managed key** . A list of your available CMEKs appears for you to choose from. For information about how CMEKs work with the BigQuery Data Transfer Service, see [Specify encryption key with transfers](#CMEK) .

9.  Click **Save** .

10. The Google Cloud console displays all the transfer setup details, including a **Resource name** for this transfer.

### bq

Enter the `  bq mk  ` command and supply the transfer creation flag `  --transfer_config  ` . The following flags are also required:

  - `  --project_id  `
  - `  --data_source  `
  - `  --target_dataset  `
  - `  --display_name  `
  - `  --params  `

<!-- end list -->

``` text
bq mk \
    --transfer_config \
    --project_id=project_id \
    --data_source=data_source \
    --target_dataset=dataset \
    --display_name=name \
    --service_account_name=service_account \
    --params='parameters'
```

Replace the following:

  - project\_id : your Google Cloud project ID. If `  --project_id  ` isn't specified, the default project is used.
  - data\_source : the data source, `  snowflake_migration  ` .
  - dataset : the BigQuery target dataset for the transfer configuration.
  - name : the display name for the transfer configuration. The transfer name can be any value that lets you identify the transfer if you need to modify it later.
  - service\_account : (Optional) the service account name used to authenticate your transfer. The service account should be owned by the same `  project_id  ` used to create the transfer and it should have all of the [required roles](#required-roles) .
  - parameters : the parameters for the created transfer configuration in JSON format. For example: `  --params='{"param":"param_value"}'  ` .

Parameters required for an Snowflake transfer configuration are:

  - `  account_identifier  ` : specify a unique identifier for your Snowflake account, which is a combination of your organization name and account name. The identifier is the prefix of Snowflake account URL and not the complete URL. For example, `  account_identifier .snowflakecomputing.com  ` .

  - `  username  ` : specify the username of the Snowflake user whose credentials and authorization is used to access your database to transfer the Snowflake tables.

  - `  auth_mechanism  ` : specify the Snowflake user authentication method. Supported values are `  PASSWORD  ` and `  KEY_PAIR  ` . For more information, see [Generate key pair for authentication](#generate_key_pair_for_authentication) .

  - `  password  ` : specify the password of the Snowflake user. This field is required if you have specified `  PASSWORD  ` in the `  auth_mechanism  ` field.

  - `  private_key  ` : specify the private key linked with the [public key associated with the Snowflake user](#create-snowflake-user) . This field is required if you have specified `  KEY_PAIR  ` in the `  auth_mechanism  ` field.

  - `  is_private_key_encrypted  ` : specify `  true  ` if the private key is encrypted with a passphrase.

  - `  private_key_passphrase  ` : specify the passphrase for the encrypted private key. This field is required if you have specified `  KEY_PAIR  ` in the `  auth_mechanism  ` field and specified `  true  ` in the `  is_private_key_encrypted  ` field.

  - `  warehouse  ` : specify a [warehouse](https://docs.snowflake.com/en/user-guide/warehouses-tasks) that is used for the execution of this data transfer.

  - `  service_account  ` : specify a service account to use with this data transfer. The service account should belong to the same Google Cloud project where the transfer configuration and destination dataset is created. The service account must have the `  storage.objects.list  ` and `  storage.objects.get  ` [required permissions](#required_service_account_permissions) .

  - `  database  ` : specify the name of the Snowflake database that contains the tables included in this data transfer.

  - `  schema  ` : specify the name of the Snowflake schema that contains the tables included in this data transfer.

  - `  table_name_patterns  ` : specify a table to transfer by entering a name or a pattern that matches the table name in the schema. You can use regular expressions to specify the pattern, for example `  table1_regex ; table2_regex  ` . The pattern should follow Java regular expression syntax. For example,
    
      - `  lineitem;ordertb  ` matches tables that are named `  lineitem  ` and `  ordertb  ` .
    
      - `  .*  ` matches all tables.
        
        You can also leave this field blank to migrate all tables from the specified schema.

  - `  ingestion_mode  ` : specify the ingestion mode for the transfer. Supported values are `  FULL  ` and `  INCREMENTAL  ` . For more information, see [Data ingestion behavior](#data-ingestion) .

  - `  translation_output_gcs_path  ` : (Optional) specify a path to the Cloud Storage folder that contains the [schema mapping files from the translation engine](#schema_detection_and_mapping) . You can leave this empty to have the Snowflake connector automatically detect your schema.
    
      - The path should follow the format `  gs:// translation_target_base_uri /metadata/config/db/schema/  ` and must end with `  /  ` .

  - `  storage_integration_object_name  ` : specify the name of the Snowflake storage integration object.

  - `  cloud_provider  ` : enter `  AWS  ` or `  AZURE  ` or `  GCP  ` depending on which cloud provider is hosting your Snowflake account.

  - `  staging_s3_uri  ` : enter the [URI of the S3 bucket](#preparing-s3-bucket) to use as a staging area. Only required when your `  cloud_provider  ` is `  AWS  ` .

  - `  aws_access_key_id  ` : enter the [access key pair](#snowflake_key_pair) . Only required when your `  cloud_provider  ` is `  AWS  ` .

  - `  aws_secret_access_key  ` : enter the [access key pair](#snowflake_key_pair) . Only required when your `  cloud_provider  ` is `  AWS  ` .

  - `  azure_storage_account  ` : enter the [storage account name](#preparing-azure-container) to use as a staging area. Only required when your `  cloud_provider  ` is `  AZURE  ` .

  - `  staging_azure_container  ` : enter the [container within Azure Blob Storage](#preparing-azure-container) to use as a staging area. Only required when your `  cloud_provider  ` is `  AZURE  ` .

  - `  azure_sas_token  ` : enter the [SAS token](#azure_sas_token) . Only required when your `  cloud_provider  ` is `  AZURE  ` .

  - `  staging_gcs_uri  ` : enter the [URI of the Cloud Storage](#preparing-gcs-bucket) to use as a staging area. Only required when your `  cloud_provider  ` is `  GCP  ` .

For example, for an AWS-hosted Snowflake account, the following command creates a Snowflake transfer named `  Snowflake transfer config  ` with a target dataset named `  your_bq_dataset  ` and a project with the ID of `  your_project_id  ` .

``` text
  PARAMS='{
  "account_identifier": "your_account_identifier",
  "auth_mechanism": "KEY_PAIR",
  "aws_access_key_id": "your_access_key_id",
  "aws_secret_access_key": "your_aws_secret_access_key",
  "cloud_provider": "AWS",
  "database": "your_sf_database",
  "ingestion_mode": "INCREMENTAL",
  "private_key": "-----BEGIN PRIVATE KEY----- privatekey\nseparatedwith\nnewlinecharacters=-----END PRIVATE KEY-----",
  "schema": "your_snowflake_schema",
  "service_account": "your_service_account",
  "storage_integration_object_name": "your_storage_integration_object",
  "staging_s3_uri": "s3://your/s3/bucket/uri",
  "table_name_patterns": ".*",
  "translation_output_gcs_path": "gs://sf_test_translation/output/metadata/config/database_name/schema_name/",
  "username": "your_sf_username",
  "warehouse": "your_warehouse"
}'

bq mk --transfer_config \
    --project_id=your_project_id \
    --target_dataset=your_bq_dataset \
    --display_name='snowflake transfer config' \
    --params="$PARAMS" \
    --data_source=snowflake_migration
```

**Note:** You can't configure notifications using the command-line tool.

### API

Use the [`  projects.locations.transferConfigs.create  `](/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs/create) method and supply an instance of the [`  TransferConfig  `](/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs#TransferConfig) resource.

If multiple transfers are created for the same Snowflake tables or if the same transfer configuration is run multiple times, the data in the existing BigQuery destination tables is overwritten.

## Specify encryption key with transfers

You can specify [customer-managed encryption keys (CMEKs)](/kms/docs/cmek) to encrypt data for a transfer run. You can use a CMEK to support transfers from [Snowflake](/bigquery/docs/migration/snowflake-migration-intro) .

When you specify a CMEK with a transfer, the BigQuery Data Transfer Service applies the CMEK to any intermediate on-disk cache of ingested data so that the entire data transfer workflow is CMEK compliant.

You cannot update an existing transfer to add a CMEK if the transfer was not originally created with a CMEK. For example, you cannot change a destination table that was originally default encrypted to now be encrypted with CMEK. Conversely, you also cannot change a CMEK-encrypted destination table to have a different type of encryption.

You can update a CMEK for a transfer if the transfer configuration was originally created with a CMEK encryption. When you update a CMEK for a transfer configuration, the BigQuery Data Transfer Service propagates the CMEK to the destination tables at the next run of the transfer, where the BigQuery Data Transfer Service replaces any outdated CMEKs with the new CMEK during the transfer run. For more information, see [Update a transfer](/bigquery/docs/working-with-transfers#update_a_transfer) .

You can also use [project default keys](/bigquery/docs/customer-managed-encryption#project_default_key) . When you specify a project default key with a transfer, the BigQuery Data Transfer Service uses the project default key as the default key for any new transfer configurations.

**Note:** For Snowflake transfers, CMEK encryption handles encryption of the data in the BigQuery destination tables as well as encryption of data in the intermediate Cloud Storage tenant bucket used during the transfer process for Snowflake on Amazon S3 or Azure Blob Storage.

## Quotas and limits

BigQuery has a load quota of 15 TB for each load job for each table. Internally, Snowflake compresses the table data, so the exported table size is larger than the table size reported by Snowflake. If you plan to migrate a table larger than 15 TB, please contact contact <dts-migration-preview-support@google.com> .

Because of [Amazon S3's consistency model](/bigquery/docs/s3-transfer-intro#consistency_considerations) , it's possible that some files won't be included in the transfer to BigQuery.

## Pricing

For information on BigQuery Data Transfer Service pricing, see the [Pricing](https://cloud.google.com/bigquery/pricing#data-transfer-service-pricing) page.

  - If the Snowflake warehouse and the Amazon S3 bucket are in different regions, then Snowflake applies egress charges when you run a Snowflake data transfer. There are no egress charges for Snowflake data transfers if both the Snowflake warehouse and the Amazon S3 bucket are in the same region.
  - When data is transferred from AWS to Google Cloud, inter-cloud egress charges are applied.

## What's next

  - Learn more about the [BigQuery Data Transfer Service](/bigquery/docs/transfer-service-overview) .
  - Migrate SQL code with the [Batch SQL translation](/bigquery/docs/batch-sql-translator) .
