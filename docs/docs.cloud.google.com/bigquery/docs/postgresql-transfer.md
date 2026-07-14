---
name: documents/docs.cloud.google.com/bigquery/docs/postgresql-transfer
uri: https://docs.cloud.google.com/bigquery/docs/postgresql-transfer
title: Load PostgreSQL data into BigQuery
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# Load PostgreSQL data into BigQuery

To schedule recurring data transfers from PostgreSQL to BigQuery, you can create a transfer configuration to specify what data objects to transfer, and how often to schedule the data transfer. After you set up the transfer configuration, the [BigQuery Data Transfer Service](https://docs.cloud.google.com/bigquery/docs/dts-introduction) transfers the latest data into a BigQuery table on the specified schedule.

For general information about PostgreSQL transfers, including configuration options, see [Introduction to PostgreSQL data transfers](https://docs.cloud.google.com/bigquery/docs/postgresql-transfer-intro) .

## Limitations

PostgreSQL data transfers are subject to following limitations:

  - The maximum number of simultaneous transfer runs to a single PostgreSQL database is determined by [the maximum number of concurrent connections supported by the PostgreSQL database](https://www.postgresql.org/docs/current/runtime-config-connection.html#GUC-MAX-CONNECTIONS) . The number of concurrent transfer jobs should be limited to a value less than the maximum number of concurrent connections supported by the PostgreSQL database.

  - A single transfer configuration can only support one data transfer run at a given time. When a second data transfer is scheduled to run before the first transfer is completed, then only the first data transfer completes while any other data transfers that overlap with the first transfer are skipped.
    
    To avoid skipped transfers within a single transfer configuration, we recommend that you increase the duration of time between large data transfers by configuring the repeat frequency.

  - During a data transfer, the PostgreSQL connector identifies indexed and partitioned key columns to transfer your data in parallel batches. For this reason, we recommend that you specify primary key columns or use indexed columns in your table to improve the performance and reduce the error rate in your data transfers. Consider the following:
    
      - If you have indexed or primary key constraints, only the following column types are supported for creating parallel batches:
          - `INTEGER`
          - `TINYINT`
          - `SMALLINT`
          - `FLOAT`
          - `REAL`
          - `DOUBLE`
          - `NUMERIC`
          - `BIGINT`
          - `DECIMAL`
          - `DATE`
      - PostgreSQL data transfers that don't use primary key or indexed columns can't support more than 2,000,000 records per table.

### Incremental transfer limitations

Incremental PostgreSQL transfers are subject to the following limitations:

  - You can only choose `TIMESTAMP` columns as watermark columns.

  - Incremental ingestion is only supported for assets with valid watermark columns.

  - Values in a watermark column must be monotonically increasing.

  - Incremental transfers cannot sync delete operations in the source table.

  - A single transfer configuration can only support either incremental or full ingestion.

  - You cannot update objects in the `asset` list after the first incremental ingestion run.

  - You cannot change the write mode in a transfer configuration after the first incremental ingestion run.

  - You cannot change the watermark column or the primary key after the first incremental ingestion run.

  - The destination BigQuery table is clustered using the provided primary key and is subject to [clustered table limitations](https://docs.cloud.google.com/bigquery/docs/clustered-tables#limitations) .

  - When you update an existing transfer configuration to the incremental ingestion mode for the first time, the first data transfer after that update transfers all available data from your data source. Any subsequent incremental data transfers will transfer only the new and updated rows from your data source.

  - We recommend that you create indexes on the watermark column. This connector uses watermark columns for filters in incremental transfers, so indexing these columns can improve performance.

  - When making an incremental transfer, you must use the updated data type mapping.

## Before you begin

  - [Create a user](https://www.postgresql.org/docs/16/app-createuser.html) in the PostgreSQL database.
  - Verify that you have completed all the actions that are required to [enable the BigQuery Data Transfer Service](https://docs.cloud.google.com/bigquery/docs/enable-transfer-service) .
  - [Create a BigQuery dataset](https://docs.cloud.google.com/bigquery/docs/datasets) to store your data.
  - Ensure you have the [required roles](https://docs.cloud.google.com/bigquery/docs/postgresql-transfer#required-roles) to complete the tasks in this document.

### Required roles

If you intend to set up transfer run notifications for Pub/Sub, ensure that you have the `pubsub.topics.setIamPolicy` Identity and Access Management (IAM) permission. Pub/Sub permissions are not required if you only set up email notifications. For more information, see [BigQuery Data Transfer Service run notifications](https://docs.cloud.google.com/bigquery/docs/transfer-run-notifications) .

To get the permissions that you need to create a BigQuery Data Transfer Service data transfer, ask your administrator to grant you the [BigQuery Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin) ( `roles/bigquery.admin` ) IAM role on your project. For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

This predefined role contains the permissions required to create a BigQuery Data Transfer Service data transfer. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

The following permissions are required to create a BigQuery Data Transfer Service data transfer:

  - BigQuery Data Transfer Service permissions:
      - `bigquery.transfers.update`
      - `bigquery.transfers.get`
  - BigQuery permissions:
      - `bigquery.datasets.get`
      - `bigquery.datasets.getIamPolicy`
      - `bigquery.datasets.update`
      - `bigquery.datasets.setIamPolicy`
      - `bigquery.jobs.create`

You might also be able to get these permissions with [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

For more information, see [Grant `bigquery.admin` access](https://docs.cloud.google.com/bigquery/docs/enable-transfer-service#grant_bigqueryadmin_access) .

### Network connections

If a public IP address is not available for the PostgreSQL database connection, you must [set up a network attachment](https://docs.cloud.google.com/vpc/docs/create-manage-network-attachments) .

For detailed instructions on the required network setup, refer to the following documents:

  - If you're transferring from Cloud SQL, see [Configure Cloud SQL instance access](https://docs.cloud.google.com/bigquery/docs/cloud-sql-instance-access) .
  - If you're transferring from AWS, see [Set up the AWS-Google Cloud VPN and network attachment](https://docs.cloud.google.com/bigquery/docs/aws-vpn-network-attachment) .
  - If you're transferring from Azure, see [Set up the Azure-Google Cloud VPN and network attachment](https://docs.cloud.google.com/bigquery/docs/azure-vpn-network-attachment) .

## Set up a PostgreSQL data transfer

Add PostgreSQL data into BigQuery by setting up a transfer configuration using one of the following options:

### Console

1.  Go to the **Data transfers** page.

2.  Click add **Create transfer** .

3.  In the **Source type** section, for **Source** , select **PostgreSQL** .

4.  In the **Data source details** section, do the following:
    
      - For **Network attachment** , select an existing network attachment or click **Create Network Attachment** . For more information, see the [Network connections](https://docs.cloud.google.com/bigquery/docs/postgresql-transfer#network-connections) section of this document.
    
      - For **Host** , enter the hostname or IP address of the PostgreSQL database server.
    
      - For **Port number** , enter the port number for the PostgreSQL database server.
    
      - For **Database name** , enter the name of the PostgreSQL database.
    
      - For **Username** , enter the username of the PostgreSQL user initiating the PostgreSQL database connection.
    
      - For **Password** , enter the password of the PostgreSQL user initiating the PostgreSQL database connection.
    
      - For **TLS Mode** , select an option from the menu. For more information about TLS modes, see [TLS configuration](https://docs.cloud.google.com/bigquery/docs/postgresql-transfer-intro#tls-configuration) .
    
      - For **Trusted PEM Certificate** , enter the public certificate of the certificate authority (CA) that issued the TLS certificate of the database server. For more information, see [Trusted Server Certificate (PEM)](https://docs.cloud.google.com/bigquery/docs/postgresql-transfer-intro#trusted_server_certificate_pem) .
    
      - For **Enable legacy mapping** , select **true** (default) to use the [legacy data type mapping](https://docs.cloud.google.com/bigquery/docs/postgresql-transfer-intro#data-type-mapping) . Select **false** to use the updated data type mapping. If you are making an incremental transfer, this value must be **false** . For more information about the data type mapping updates, see [March 16, 2027](https://docs.cloud.google.com/bigquery/docs/transfer-changes#Mar16-postgresql) . database server.
    
      - For **Ingestion type** , select **Full** or **Incremental** .
        
          - If you select **Incremental** ( [Preview](https://cloud.google.com/products#product-launch-stages) ), for **Write mode** , select either **Append** or **Upsert** . For more information about the different write modes, see [Full or incremental transfers](https://docs.cloud.google.com/bigquery/docs/postgresql-transfer-intro#full-incremental-transfers) .
    
      - For **PostgreSQL objects to transfer** , click **Browse** .
        
        Select any objects to be transferred to the BigQuery destination dataset. You can also manually enter any objects to include in the data transfer in this field.
        
          - If you have selected **Append** as your incremental write mode, you must select a column as the watermark column.
          - If you have selected **Upsert** as your incremental write mode, you must select a column as the watermark column, and then select one or more columns as the primary key.

5.  In the **Transfer config name** section, for **Display name** , enter a name for the transfer. The transfer name can be any value that lets you identify the transfer if you need to modify it later.

6.  In the **Schedule options** section, do the following:
    
      - Select a repeat frequency. If you select the **Hours** , **Days** (default), **Weeks** , or **Months** option, you must also specify a frequency. You can also select the **Custom** option to create a more specific repeat frequency. If you select the **On-demand** option, this data transfer only runs when you [manually trigger the transfer](https://docs.cloud.google.com/bigquery/docs/working-with-transfers#manually_trigger_a_transfer) .
      - If applicable, select either the **Start now** or **Start at a set time** option and provide a start date and run time.

7.  In the **Destination settings** section, for **Dataset** , select the dataset that you created to store your data, or click **Create new dataset** and create one to use as the destination dataset.

8.  Optional: In the **Notification options** section, do the following:
    
      - To enable email notifications, click the **Email notifications** toggle to the on position. When you enable this option, the transfer administrator receives an email notification when a transfer run fails.
      - To configure Pub/Sub run [notifications](https://docs.cloud.google.com/bigquery/docs/transfer-run-notifications) for your transfer, click the **Pub/Sub notifications** toggle to the on position. You can select your [topic](https://docs.cloud.google.com/pubsub/docs/admin) name or click **Create a topic** to create one.

9.  Click **Save** .

### bq

Enter the [`bq mk` command](https://docs.cloud.google.com/bigquery/docs/reference/bq-cli-reference#bq_mk) and supply the transfer creation flag `--transfer_config` :

    bq mk
        --transfer_config
        --project_id=PROJECT_ID
        --data_source=DATA_SOURCE
        --display_name=DISPLAY_NAME
        --target_dataset=DATASET
        --params='PARAMETERS'

Replace the following:

  - PROJECT\_ID (optional): your Google Cloud project ID. If the `--project_id` flag isn't supplied to specify a particular project, the default project is used.

  - DATA\_SOURCE : the data source, which is `postgresql` .

  - DISPLAY\_NAME : the display name for the data transfer configuration. The transfer name can be any value that lets you identify the transfer if you need to modify it later.

  - DATASET : the target dataset for the data transfer configuration.

  - PARAMETERS : the parameters for the created transfer configuration in JSON format. For example: `--params='{"param":"param_value"}'` . The following are the parameters for a PostgreSQL transfer:
    
      - `connector.networkAttachment` (optional): the name of the network attachment to connect to the PostgreSQL database.
      - `connector.database` : the name of the PostgreSQL database.
      - `connector.endpoint.host` : the hostname or IP address of the database.
      - `connector.endpoint.port` : the port number of the database.
      - `connector.authentication.username` : the username of the database user.
      - `connector.authentication.password` : the password of the database user.
      - `connector.tls.mode` : specify a [TLS configuration](https://docs.cloud.google.com/bigquery/docs/postgresql-transfer-intro#tls-configuration) to use with this transfer:
          - `ENCRYPT_VERIFY_CA_AND_HOST` to encrypt data, and verify CA and hostname
          - `ENCRYPT_VERIFY_CA` to encrypt data, and verify CA only
          - `ENCRYPT_VERIFY_NONE` for data encryption only
          - `DISABLE` for no encryption or verification
      - `connector.tls.trustedServerCertificate` : (optional) provide one or more [PEM-encoded certificates](https://docs.cloud.google.com/bigquery/docs/postgresql-transfer-intro#trusted_server_certificate_pem) . Required only if `connector.tls.mode` is `ENCRYPT_VERIFY_CA_AND_HOST` or `ENCRYPT_VERIFY_CA` .
      - `ingestionType` : specify either `full` or `incremental` . Incremental transfers are supported in [Preview](https://cloud.google.com/products#product-launch-stages) . For more information, see [Full or incremental transfers](https://docs.cloud.google.com/bigquery/docs/postgresql-transfer-intro#full-incremental-transfers) .
      - `writeMode` : specify either `WRITE_MODE_APPEND` or `WRITE_MODE_UPSERT` .
      - `watermarkColumns` : specify columns in your table as watermark columns. This field is required for incremental transfers.
      - `primaryKeys` : specify columns in your table as primary keys. This field is required for incremental transfers.
      - `connector.legacyMapping` : set to `true` (default) to use the [legacy data type mapping](https://docs.cloud.google.com/bigquery/docs/postgresql-transfer-intro#data-type-mapping) . Set to `false` to use the updated data type mapping. If you are making an incremental transfer, this value must be `false` . For more information about the data type mapping updates, see [March 16, 2027](https://docs.cloud.google.com/bigquery/docs/transfer-changes#Mar16-postgresql) .
      - `assets` : a list of the names of the PostgreSQL tables to be transferred from the PostgreSQL database as part of the transfer.

For example, the following command creates a PostgreSQL transfer called `My Transfer` :

    bq mk
        --transfer_config
        --target_dataset=mydataset
        --data_source=postgresql
        --display_name='My Transfer'
        --params='{"assets":["DB1/PUBLIC/DEPARTMENT","DB1/PUBLIC/EMPLOYEES"],
            "connector.authentication.username": "User1",
            "connector.authentication.password":"ABC12345",
            "connector.database":"DB1",
            "connector.endpoint.host":"192.168.0.1",
            "connector.endpoint.port":5432,
            "ingestionType":"incremental",
            "writeMode":"WRITE_MODE_APPEND",
            "watermarkColumns":["createdAt","createdAt"],
            "primaryKeys":[['dep_id'], ['report_by','report_title']],
            "connector.tls.mode": "ENCRYPT_VERIFY_CA_AND_HOST",
            "connector.tls.trustedServerCertificate": "PEM-encoded certificate"}'

When you specify multiple assets during an incremental transfer, the values of the `watermarkColumns` and `primaryKeys` fields correspond to the position of values in the `assets` field. In the following example, `dep_id` corresponds to the table `DB1/USER1/DEPARTMENT` , while `report_by` and `report_title` corresponds to the table `DB1/USER1/EMPLOYEES` .

``` 
      "primaryKeys":[['dep_id'], ['report_by','report_title']],
      "assets":["DB1/USER1/DEPARTMENT","DB1/USER1/EMPLOYEES"],
  
```

### API

Use the [`projects.locations.transferConfigs.create` method](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs/create) and supply an instance of the [`TransferConfig` resource](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs#TransferConfig) .

When you save the transfer configuration, the PostgreSQL connector automatically triggers a transfer run according to your schedule option. With every transfer run, the PostgreSQL connector transfers all available data from PostgreSQL into BigQuery.

To manually run a data transfer outside of your regular schedule, you can start a [backfill run](https://docs.cloud.google.com/bigquery/docs/working-with-transfers#manually_trigger_a_transfer) .

## Troubleshoot

If you are having issues setting up your data transfer, see [PostgreSQL transfer issues](https://docs.cloud.google.com/bigquery/docs/transfer-troubleshooting#postgresql-issues) .

## Transfer metadata

> **Preview**
> 
> This product is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

You can also use the PostgreSQL connector to [transfer metadata to Knowledge Catalog](https://docs.cloud.google.com/dataplex/docs/connectors) . For more information, see [Load PostgreSQL metadata into Knowledge Catalog](https://docs.cloud.google.com/dataplex/docs/postgresql-transfer) .

## What's next

  - Read [an overview about the BigQuery Data Transfer Service](https://docs.cloud.google.com/bigquery/docs/dts-introduction) .
  - Learn about [managing transfers](https://docs.cloud.google.com/bigquery/docs/working-with-transfers) , including getting information about a transfer configuration, listing transfer configurations, and viewing a transfer's run history.
  - Learn how to [load data with BigQuery Omni operations](https://docs.cloud.google.com/bigquery/docs/load-data-using-cross-cloud-transfer) .
