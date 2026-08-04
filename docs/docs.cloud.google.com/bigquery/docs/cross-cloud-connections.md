---
name: documents/docs.cloud.google.com/bigquery/docs/cross-cloud-connections
uri: https://docs.cloud.google.com/bigquery/docs/cross-cloud-connections
title: Create cross-cloud connections
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# Create cross-cloud connections

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

> **Note:** To request support or provide feedback for this feature, send an email to <biglake-help@google.com> .

Cross-cloud connections are BigQuery connections that bring data from Amazon Web Services (AWS), Microsoft Azure, and Salesforce Data 360 into BigQuery for querying. These connections are an alternative to standard BigQuery connections that use BigQuery Omni, where BigQuery deploys lightweight compute workers to remote regions to make data in other clouds available for querying without any data movement.

Workloads can benefit from cross-cloud connections versus standard connections for the following reasons:

  - **Feature consistency.** By bringing your data from other clouds into BigQuery, you gain direct access to BigQuery AI capabilities, Gemini Enterprise Agent Platform, materialized views, user-defined functions, and other features that aren't available through standard connections.
  - **Cost efficiency.** Workloads that use cross-cloud connections consume standard slot reservations and commitments, eliminating the need to manage separate compute capacities.

If your workload involves Apache Iceberg catalogs or you need query support across engines other than BigQuery, consider using [cross-cloud Lakehouse for Apache Iceberg](https://docs.cloud.google.com/lakehouse/docs/about-cross-cloud-lakehouse) instead.

## Before you begin

Grant Identity and Access Management and third-party roles that give users the necessary permissions to perform each task in this document.

### Required BigQuery roles

To get the permissions that you need to create a cross-cloud connection, ask your administrator to grant you the [BigQuery Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin) ( `roles/bigquery.admin` ) IAM role on the project. For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

### Required third-party roles

To get the permissions that you need to create a cross-cloud connection, ensure that you have the following third-party roles:

  - **For AWS:** a role that lets you create IAM policies and roles in your AWS account.
  - **For Azure:** a role that lets you manage App Registrations in Microsoft Entra ID (Azure AD) and assign roles, such as Storage Blob Data Reader, on the target Azure account.

## Create AWS cross-cloud connections

To create an AWS cross-cloud connection, do the following:

1.  [Create an AWS IAM policy for BigQuery](https://docs.cloud.google.com/bigquery/docs/omni-aws-create-connection#creating-aws-iam-policy) as you would for standard BigQuery connections.

2.  [Create an AWS IAM role for BigQuery](https://docs.cloud.google.com/bigquery/docs/omni-aws-create-connection#creating-aws-iam-role) as you would for standard BigQuery connections.

3.  To create a connection resource, use the [`bq mk --connection` command](https://docs.cloud.google.com/bigquery/docs/reference/bq-cli-reference#mk-connection) :
    
        bq mk --connection \
            --connection_type='AWS' \
            --location=LOCATION \
            --project_id=PROJECT_ID \
            --properties='{"accessRole":{"iamRoleId":"arn:aws:iam::AWS_ACCOUNT_ID:role/ROLE_NAME"}}' \
            CONNECTION_ID
    
    Replace the following:
    
      - `  LOCATION  ` : a standard [BigQuery location](https://docs.cloud.google.com/bigquery/docs/locations) , not a BigQuery Omni location. For guidance on selecting a region, see [Region recommendations](https://docs.cloud.google.com/bigquery/docs/cross-cloud-connections#region_recommendations) .
      - `  PROJECT_ID  ` : the ID of your Google Cloud project.
      - `  AWS_ACCOUNT_ID  ` : the ID of the AWS IAM user from the previous step.
      - `  ROLE_NAME  ` : the AWS role policy name that you chose.
      - `  CONNECTION_ID  ` : an ID to give to this connection resource.

4.  To note the service account information, use the [`bq show` command](https://docs.cloud.google.com/bigquery/docs/reference/bq-cli-reference#bq_show) :
    
        bq show --connection \
            --location=LOCATION \
            PROJECT_ID.LOCATION.CONNECTION_ID

5.  [Add a trust policy to the AWS role](https://docs.cloud.google.com/bigquery/docs/omni-aws-create-connection#add-trust-policy) using the service account information, as you would for standard BigQuery connections.

With your established AWS cross-cloud connection, you can now create tables and datasets to query your remote data.

### AWS examples

The following example creates an external table to query Parquet files directly from an Amazon Simple Storage Service (Amazon S3) bucket with a cross-cloud connection:

    CREATE SCHEMA `my-project.aws_raw_data`
      OPTIONS (
        location = 'us-east4');
    
    CREATE EXTERNAL TABLE `my-project.aws_raw_data.sales_parquet`
    WITH CONNECTION `us-east4.my-aws-connection`
      OPTIONS (
        format = 'PARQUET',
        uris = ['s3://my-data-bucket/sales/year=2025/*']);

The following example federates an entire database into BigQuery using AWS Glue with a cross-cloud connection:

    CREATE EXTERNAL SCHEMA `my-project.aws_glue_data`
    WITH CONNECTION `us-east4.my-aws-connection`
      OPTIONS (
        location = 'us-east4',
        external_source = 'aws-glue://arn:aws:glue:us-east-4:123456789:database/test_database');

For more information on AWS Glue federation, see [Create and manage AWS Glue federated datasets](https://docs.cloud.google.com/bigquery/docs/glue-federated-datasets) .

## Create Azure cross-cloud connections

To create an Azure cross-cloud connection, do the following:

1.  [Create an application in your Azure tenant](https://docs.cloud.google.com/bigquery/docs/omni-azure-create-connection#create-azure-tenant) as you would for standard BigQuery connections, and take note of the Application (client) and Directory (tenant) IDs.

2.  [Assign a role to the Azure application](https://docs.cloud.google.com/bigquery/docs/omni-azure-create-connection#assigning-a-role) as you would for standard BigQuery connections.

3.  To create a connection resource, use the [`bq mk --connection` command](https://docs.cloud.google.com/bigquery/docs/reference/bq-cli-reference#mk-connection) :
    
        bq mk --connection \
            --connection_type='Azure' \
            --tenant_id=TENANT_ID \
            --location=LOCATION \
            --federated_azure=true \
            --federated_app_client_id=APP_ID \
            --project_id=PROJECT_ID \
            CONNECTION_ID
    
    Replace the following:
    
      - `  TENANT_ID  ` : the tenant ID of the Azure directory that contains the Azure account.
      - `  LOCATION  ` : a standard [BigQuery location](https://docs.cloud.google.com/bigquery/docs/locations) , not a BigQuery Omni location. For guidance on selecting a region, see [Region recommendations](https://docs.cloud.google.com/bigquery/docs/cross-cloud-connections#region_recommendations) .
      - `  APP_ID  ` : the Azure Application (client) ID.
      - `  PROJECT_ID  ` : the ID of your Google Cloud project.
      - `  CONNECTION_ID  ` : an ID to give to this connection resource.

4.  To note the service account information, use the [`bq show` command](https://docs.cloud.google.com/bigquery/docs/reference/bq-cli-reference#bq_show) :
    
        bq show --connection \
            --location=LOCATION \
            PROJECT_ID.LOCATION.CONNECTION_ID

5.  [Add a federated credential](https://docs.cloud.google.com/bigquery/docs/omni-azure-create-connection#add-a-federated-credential) using the service account information, as you would for standard BigQuery connections.

With your established Azure cross-cloud connection, you can now create tables and datasets to query your remote data.

### Azure examples

The following example creates an external table to query Parquet files directly from an Azure Blob Storage container with a cross-cloud connection:

    CREATE SCHEMA `my-project.azure_raw_data`
      OPTIONS (
        location = 'us-east4');
    
    CREATE EXTERNAL TABLE `my-project.azure_raw_data.sales_parquet`
    WITH CONNECTION `us-east4.my-azure-connection`
      OPTIONS (
        format = 'PARQUET',
        uris = ['azure://mystorageaccount.blob.core.windows.net/mycontainer/sales/year=2025/*']);

The following example creates an external table to query raw CSV exports from a Blob Storage container with a cross-cloud connection:

    CREATE EXTERNAL TABLE `my-project.azure_raw_data.daily_logs_csv`
    WITH CONNECTION `us-east4.my-azure-connection`
      OPTIONS (
        format = 'CSV',
        skip_leading_rows = 1,
        uris = ['azure://mystorageaccount.blob.core.windows.net/mycontainer/logs/*.csv']);

## Create Data 360 cross-cloud connections

To create a Data 360 cross-cloud connection, follow the steps to [link a Data 360 dataset to BigQuery](https://docs.cloud.google.com/bigquery/docs/salesforce-quickstart#link-dataset) , except instead of creating the linked dataset in a BigQuery Omni location, create it in a standard [BigQuery location](https://docs.cloud.google.com/bigquery/docs/locations) . For guidance on selecting a region, see [Region recommendations](https://docs.cloud.google.com/bigquery/docs/cross-cloud-connections#region_recommendations) .

After you update your queries to use the new datasets, you can delete any legacy linked datasets and BigQuery Omni materialized views.

## Region recommendations

When you select a [standard BigQuery region](https://docs.cloud.google.com/bigquery/docs/locations#regions) for your cross-cloud connection, choose the region that is physically closest to your data for optimal cost and performance efficiency.

The following table lists AWS regions and the best corresponding BigQuery regions:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>AWS region</strong></th>
<th><strong>Closest BigQuery region</strong></th>
<th><strong>Other close BigQuery regions</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">us-east-1</code></td>
<td><code dir="ltr" translate="no">us-east4</code></td>
<td><code dir="ltr" translate="no">us-east1</code><br />
<code dir="ltr" translate="no">us-east5</code><br />
<code dir="ltr" translate="no">us-central1</code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">us-east-2</code></td>
<td><code dir="ltr" translate="no">us-east5</code></td>
<td><code dir="ltr" translate="no">us-east4</code><br />
<code dir="ltr" translate="no">us-east1</code><br />
<code dir="ltr" translate="no">us-central1</code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">us-west-1</code></td>
<td><code dir="ltr" translate="no">us-west2</code></td>
<td><code dir="ltr" translate="no">us-west4</code><br />
<code dir="ltr" translate="no">us-west1</code><br />
<code dir="ltr" translate="no">us-west3</code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">us-west-2</code></td>
<td><code dir="ltr" translate="no">us-west1</code></td>
<td><code dir="ltr" translate="no">us-west3</code><br />
<code dir="ltr" translate="no">us-west4</code><br />
<code dir="ltr" translate="no">us-west2</code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">ca-central-1</code></td>
<td><code dir="ltr" translate="no">northamerica-northeast1</code></td>
<td><code dir="ltr" translate="no">northamerica-northeast2</code><br />
<code dir="ltr" translate="no">us-east4</code><br />
<code dir="ltr" translate="no">us-east5</code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">sa-east-1</code></td>
<td><code dir="ltr" translate="no">southamerica-east1</code></td>
<td><code dir="ltr" translate="no">southamerica-west1</code><br />
<code dir="ltr" translate="no">us-east1</code><br />
<code dir="ltr" translate="no">us-south1</code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">eu-west-1</code></td>
<td><code dir="ltr" translate="no">europe-west1</code></td>
<td><code dir="ltr" translate="no">europe-west2</code><br />
<code dir="ltr" translate="no">europe-west9</code><br />
<code dir="ltr" translate="no">europe-west4</code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">eu-west-2</code></td>
<td><code dir="ltr" translate="no">europe-west2</code></td>
<td><code dir="ltr" translate="no">europe-west1</code><br />
<code dir="ltr" translate="no">europe-west9</code><br />
<code dir="ltr" translate="no">europe-west4</code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">eu-west-3</code></td>
<td><code dir="ltr" translate="no">europe-west9</code></td>
<td><code dir="ltr" translate="no">europe-west1</code><br />
<code dir="ltr" translate="no">europe-west2</code><br />
<code dir="ltr" translate="no">europe-west3</code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">eu-central-1</code></td>
<td><code dir="ltr" translate="no">europe-west3</code></td>
<td><code dir="ltr" translate="no">europe-west4</code><br />
<code dir="ltr" translate="no">europe-west1</code><br />
<code dir="ltr" translate="no">europe-west6</code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">eu-central-2</code></td>
<td><code dir="ltr" translate="no">europe-west6</code></td>
<td><code dir="ltr" translate="no">europe-west8</code><br />
<code dir="ltr" translate="no">europe-west12</code><br />
<code dir="ltr" translate="no">europe-west3</code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">eu-north-1</code></td>
<td><code dir="ltr" translate="no">europe-north1</code></td>
<td><code dir="ltr" translate="no">europe-west4</code><br />
<code dir="ltr" translate="no">europe-central2</code><br />
<code dir="ltr" translate="no">europe-west1</code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">eu-south-1</code></td>
<td><code dir="ltr" translate="no">europe-west8</code></td>
<td><code dir="ltr" translate="no">europe-west12</code><br />
<code dir="ltr" translate="no">europe-west6</code><br />
<code dir="ltr" translate="no">europe-west3</code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">eu-south-2</code></td>
<td><code dir="ltr" translate="no">europe-southwest1</code></td>
<td><code dir="ltr" translate="no">europe-west9</code><br />
<code dir="ltr" translate="no">europe-west1</code><br />
<code dir="ltr" translate="no">europe-west8</code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">me-central-1</code></td>
<td><code dir="ltr" translate="no">me-central1</code></td>
<td><code dir="ltr" translate="no">me-central2</code><br />
<code dir="ltr" translate="no">me-west1</code><br />
<code dir="ltr" translate="no">asia-south1</code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">me-south-1</code></td>
<td><code dir="ltr" translate="no">me-central2</code></td>
<td><code dir="ltr" translate="no">me-central1</code><br />
<code dir="ltr" translate="no">me-west1</code><br />
<code dir="ltr" translate="no">asia-south1</code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">af-south-1</code></td>
<td><code dir="ltr" translate="no">europe-southwest1</code></td>
<td><code dir="ltr" translate="no">me-central2</code><br />
<code dir="ltr" translate="no">me-west1</code><br />
<code dir="ltr" translate="no">europe-west1</code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">ap-east-1</code></td>
<td><code dir="ltr" translate="no">asia-east2</code></td>
<td><code dir="ltr" translate="no">asia-east1</code><br />
<code dir="ltr" translate="no">asia-southeast1</code><br />
<code dir="ltr" translate="no">asia-northeast1</code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">ap-northeast-1</code></td>
<td><code dir="ltr" translate="no">asia-northeast1</code></td>
<td><code dir="ltr" translate="no">asia-northeast2</code><br />
<code dir="ltr" translate="no">asia-northeast3</code><br />
<code dir="ltr" translate="no">asia-east1</code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">ap-northeast-2</code></td>
<td><code dir="ltr" translate="no">asia-northeast3</code></td>
<td><code dir="ltr" translate="no">asia-northeast2</code><br />
<code dir="ltr" translate="no">asia-northeast1</code><br />
<code dir="ltr" translate="no">asia-east1</code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">ap-northeast-3</code></td>
<td><code dir="ltr" translate="no">asia-northeast2</code></td>
<td><code dir="ltr" translate="no">asia-northeast1</code><br />
<code dir="ltr" translate="no">asia-northeast3</code><br />
<code dir="ltr" translate="no">asia-east1</code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">ap-south-1</code></td>
<td><code dir="ltr" translate="no">asia-south1</code></td>
<td><code dir="ltr" translate="no">asia-south2</code><br />
<code dir="ltr" translate="no">me-central1</code><br />
<code dir="ltr" translate="no">asia-southeast1</code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">ap-south-2</code></td>
<td><code dir="ltr" translate="no">asia-south2</code></td>
<td><code dir="ltr" translate="no">asia-south1</code><br />
<code dir="ltr" translate="no">asia-southeast1</code><br />
<code dir="ltr" translate="no">me-central1</code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">ap-southeast-1</code></td>
<td><code dir="ltr" translate="no">asia-southeast1</code></td>
<td><code dir="ltr" translate="no">asia-southeast2</code><br />
<code dir="ltr" translate="no">asia-east1</code><br />
<code dir="ltr" translate="no">asia-south1</code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">ap-southeast-2</code></td>
<td><code dir="ltr" translate="no">australia-southeast1</code></td>
<td><code dir="ltr" translate="no">australia-southeast2</code><br />
<code dir="ltr" translate="no">asia-southeast2</code><br />
<code dir="ltr" translate="no">asia-southeast1</code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">ap-southeast-3</code></td>
<td><code dir="ltr" translate="no">asia-southeast2</code></td>
<td><code dir="ltr" translate="no">asia-southeast1</code><br />
<code dir="ltr" translate="no">australia-southeast1</code><br />
<code dir="ltr" translate="no">asia-east1</code></td>
</tr>
</tbody>
</table>

The following table lists Azure regions and the best corresponding BigQuery regions:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Azure region</strong></th>
<th><strong>Closest BigQuery region</strong></th>
<th><strong>Other close BigQuery regions</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>East US</td>
<td><code dir="ltr" translate="no">us-east4</code></td>
<td><code dir="ltr" translate="no">us-east1</code><br />
<code dir="ltr" translate="no">us-east5</code><br />
<code dir="ltr" translate="no">us-central1</code></td>
</tr>
<tr class="even">
<td>East US 2</td>
<td><code dir="ltr" translate="no">us-east4</code></td>
<td><code dir="ltr" translate="no">us-east1</code><br />
<code dir="ltr" translate="no">us-east5</code><br />
<code dir="ltr" translate="no">us-south1</code></td>
</tr>
<tr class="odd">
<td>West US</td>
<td><code dir="ltr" translate="no">us-west1</code></td>
<td><code dir="ltr" translate="no">us-west2</code><br />
<code dir="ltr" translate="no">us-west3</code><br />
<code dir="ltr" translate="no">us-west4</code></td>
</tr>
<tr class="even">
<td>West US 2</td>
<td><code dir="ltr" translate="no">us-west1</code></td>
<td><code dir="ltr" translate="no">us-west4</code><br />
<code dir="ltr" translate="no">us-west3</code><br />
<code dir="ltr" translate="no">us-west2</code></td>
</tr>
<tr class="odd">
<td>West US 3</td>
<td><code dir="ltr" translate="no">us-west4</code></td>
<td><code dir="ltr" translate="no">us-west2</code><br />
<code dir="ltr" translate="no">us-west3</code><br />
<code dir="ltr" translate="no">us-west1</code></td>
</tr>
<tr class="even">
<td>Central US</td>
<td><code dir="ltr" translate="no">us-central1</code></td>
<td><code dir="ltr" translate="no">us-east5</code><br />
<code dir="ltr" translate="no">us-east4</code><br />
<code dir="ltr" translate="no">us-east1</code></td>
</tr>
<tr class="odd">
<td>North Central US</td>
<td><code dir="ltr" translate="no">us-east5</code></td>
<td><code dir="ltr" translate="no">us-central1</code><br />
<code dir="ltr" translate="no">us-east4</code><br />
<code dir="ltr" translate="no">us-east1</code></td>
</tr>
<tr class="even">
<td>South Central US</td>
<td><code dir="ltr" translate="no">us-south1</code></td>
<td><code dir="ltr" translate="no">us-east5</code><br />
<code dir="ltr" translate="no">us-central1</code><br />
<code dir="ltr" translate="no">us-east1</code></td>
</tr>
<tr class="odd">
<td>West Central US</td>
<td><code dir="ltr" translate="no">us-west3</code></td>
<td><code dir="ltr" translate="no">us-central1</code><br />
<code dir="ltr" translate="no">us-west4</code><br />
<code dir="ltr" translate="no">us-west2</code></td>
</tr>
<tr class="even">
<td>Canada Central</td>
<td><code dir="ltr" translate="no">northamerica-northeast2</code></td>
<td><code dir="ltr" translate="no">northamerica-northeast1</code><br />
<code dir="ltr" translate="no">us-east5</code><br />
<code dir="ltr" translate="no">us-east4</code></td>
</tr>
<tr class="odd">
<td>Canada East</td>
<td><code dir="ltr" translate="no">northamerica-northeast1</code></td>
<td><code dir="ltr" translate="no">northamerica-northeast2</code><br />
<code dir="ltr" translate="no">us-east4</code><br />
<code dir="ltr" translate="no">us-east5</code></td>
</tr>
<tr class="even">
<td>West Europe</td>
<td><code dir="ltr" translate="no">europe-west4</code></td>
<td><code dir="ltr" translate="no">europe-west1</code><br />
<code dir="ltr" translate="no">europe-west3</code><br />
<code dir="ltr" translate="no">europe-west9</code></td>
</tr>
<tr class="odd">
<td>North Europe</td>
<td><code dir="ltr" translate="no">europe-west1</code></td>
<td><code dir="ltr" translate="no">europe-west2</code><br />
<code dir="ltr" translate="no">europe-west9</code><br />
<code dir="ltr" translate="no">europe-west4</code></td>
</tr>
<tr class="even">
<td>France Central</td>
<td><code dir="ltr" translate="no">europe-west9</code></td>
<td><code dir="ltr" translate="no">europe-west1</code><br />
<code dir="ltr" translate="no">europe-west2</code><br />
<code dir="ltr" translate="no">europe-west3</code></td>
</tr>
<tr class="odd">
<td>France South</td>
<td><code dir="ltr" translate="no">europe-west9</code></td>
<td><code dir="ltr" translate="no">europe-southwest1</code><br />
<code dir="ltr" translate="no">europe-west8</code><br />
<code dir="ltr" translate="no">europe-west1</code></td>
</tr>
<tr class="even">
<td>Germany West Central</td>
<td><code dir="ltr" translate="no">europe-west3</code></td>
<td><code dir="ltr" translate="no">europe-west4</code><br />
<code dir="ltr" translate="no">europe-west1</code><br />
<code dir="ltr" translate="no">europe-west6</code></td>
</tr>
<tr class="odd">
<td>Germany North</td>
<td><code dir="ltr" translate="no">europe-west3</code></td>
<td><code dir="ltr" translate="no">europe-west4</code><br />
<code dir="ltr" translate="no">europe-central2</code><br />
<code dir="ltr" translate="no">europe-west2</code></td>
</tr>
<tr class="even">
<td>Switzerland North</td>
<td><code dir="ltr" translate="no">europe-west6</code></td>
<td><code dir="ltr" translate="no">europe-west8</code><br />
<code dir="ltr" translate="no">europe-west12</code><br />
<code dir="ltr" translate="no">europe-west3</code></td>
</tr>
<tr class="odd">
<td>Switzerland West</td>
<td><code dir="ltr" translate="no">europe-west6</code></td>
<td><code dir="ltr" translate="no">europe-west9</code><br />
<code dir="ltr" translate="no">europe-west8</code><br />
<code dir="ltr" translate="no">europe-west3</code></td>
</tr>
<tr class="even">
<td>UK South</td>
<td><code dir="ltr" translate="no">europe-west2</code></td>
<td><code dir="ltr" translate="no">europe-west1</code><br />
<code dir="ltr" translate="no">europe-west9</code><br />
<code dir="ltr" translate="no">europe-west4</code></td>
</tr>
<tr class="odd">
<td>UK West</td>
<td><code dir="ltr" translate="no">europe-west2</code></td>
<td><code dir="ltr" translate="no">europe-west1</code><br />
<code dir="ltr" translate="no">europe-west9</code><br />
<code dir="ltr" translate="no">europe-west4</code></td>
</tr>
<tr class="even">
<td>Norway East</td>
<td><code dir="ltr" translate="no">europe-north1</code></td>
<td><code dir="ltr" translate="no">europe-west4</code><br />
<code dir="ltr" translate="no">europe-central2</code><br />
<code dir="ltr" translate="no">europe-west1</code></td>
</tr>
<tr class="odd">
<td>Norway West</td>
<td><code dir="ltr" translate="no">europe-north1</code></td>
<td><code dir="ltr" translate="no">europe-west4</code><br />
<code dir="ltr" translate="no">europe-central2</code><br />
<code dir="ltr" translate="no">europe-west1</code></td>
</tr>
<tr class="even">
<td>Sweden Central</td>
<td><code dir="ltr" translate="no">europe-north1</code></td>
<td><code dir="ltr" translate="no">europe-west4</code><br />
<code dir="ltr" translate="no">europe-central2</code><br />
<code dir="ltr" translate="no">europe-west1</code></td>
</tr>
<tr class="odd">
<td>East Asia</td>
<td><code dir="ltr" translate="no">asia-east2</code></td>
<td><code dir="ltr" translate="no">asia-east1</code><br />
<code dir="ltr" translate="no">asia-southeast1</code><br />
<code dir="ltr" translate="no">asia-northeast1</code></td>
</tr>
<tr class="even">
<td>Southeast Asia</td>
<td><code dir="ltr" translate="no">asia-southeast1</code></td>
<td><code dir="ltr" translate="no">asia-southeast2</code><br />
<code dir="ltr" translate="no">asia-east1</code><br />
<code dir="ltr" translate="no">asia-south1</code></td>
</tr>
<tr class="odd">
<td>Japan East</td>
<td><code dir="ltr" translate="no">asia-northeast1</code></td>
<td><code dir="ltr" translate="no">asia-northeast2</code><br />
<code dir="ltr" translate="no">asia-northeast3</code><br />
<code dir="ltr" translate="no">asia-east1</code></td>
</tr>
<tr class="even">
<td>Japan West</td>
<td><code dir="ltr" translate="no">asia-northeast2</code></td>
<td><code dir="ltr" translate="no">asia-northeast1</code><br />
<code dir="ltr" translate="no">asia-northeast3</code><br />
<code dir="ltr" translate="no">asia-east1</code></td>
</tr>
<tr class="odd">
<td>Korea Central</td>
<td><code dir="ltr" translate="no">asia-northeast3</code></td>
<td><code dir="ltr" translate="no">asia-northeast2</code><br />
<code dir="ltr" translate="no">asia-northeast1</code><br />
<code dir="ltr" translate="no">asia-east1</code></td>
</tr>
<tr class="even">
<td>Australia East</td>
<td><code dir="ltr" translate="no">australia-southeast1</code></td>
<td><code dir="ltr" translate="no">australia-southeast2</code><br />
<code dir="ltr" translate="no">asia-southeast2</code><br />
<code dir="ltr" translate="no">asia-southeast1</code></td>
</tr>
<tr class="odd">
<td>Australia Southeast</td>
<td><code dir="ltr" translate="no">australia-southeast2</code></td>
<td><code dir="ltr" translate="no">australia-southeast1</code><br />
<code dir="ltr" translate="no">asia-southeast1</code><br />
<code dir="ltr" translate="no">asia-east1</code></td>
</tr>
<tr class="even">
<td>Australia Central</td>
<td><code dir="ltr" translate="no">australia-southeast1</code></td>
<td><code dir="ltr" translate="no">australia-southeast2</code><br />
<code dir="ltr" translate="no">asia-southeast2</code><br />
<code dir="ltr" translate="no">asia-southeast1</code></td>
</tr>
<tr class="odd">
<td>West India</td>
<td><code dir="ltr" translate="no">asia-south1</code></td>
<td><code dir="ltr" translate="no">asia-south2</code><br />
<code dir="ltr" translate="no">me-central1</code><br />
<code dir="ltr" translate="no">asia-southeast1</code></td>
</tr>
<tr class="even">
<td>Central India</td>
<td><code dir="ltr" translate="no">asia-south1</code></td>
<td><code dir="ltr" translate="no">asia-south2</code><br />
<code dir="ltr" translate="no">me-central1</code><br />
<code dir="ltr" translate="no">asia-southeast1</code></td>
</tr>
<tr class="odd">
<td>South India</td>
<td><code dir="ltr" translate="no">asia-south1</code></td>
<td><code dir="ltr" translate="no">asia-south2</code><br />
<code dir="ltr" translate="no">asia-southeast1</code><br />
<code dir="ltr" translate="no">me-central1</code></td>
</tr>
</tbody>
</table>

## What's next

  - Learn about [BigQuery analytics](https://docs.cloud.google.com/bigquery/docs/query-overview) .
