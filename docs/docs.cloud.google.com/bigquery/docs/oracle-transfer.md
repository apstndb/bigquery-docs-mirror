---
name: documents/docs.cloud.google.com/bigquery/docs/oracle-transfer
uri: https://docs.cloud.google.com/bigquery/docs/oracle-transfer
title: Load Oracle data into BigQuery
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# Load Oracle data into BigQuery

To schedule recurring data transfers from your Oracle database to BigQuery, you create a transfer configuration to specify what data objects to transfer, and how often to schedule the data transfer. After you set up the transfer configuration, the [BigQuery Data Transfer Service](https://docs.cloud.google.com/bigquery/docs/dts-introduction) transfers the latest data into a BigQuery table on the specified schedule.

For general information about Oracle transfers, including configuration options, see [Introduction to Oracle data transfers](https://docs.cloud.google.com/bigquery/docs/oracle-transfer-intro) .

## Limitations

Oracle transfers are subject to the following limitations:

  - The maximum number of simultaneous connections to an Oracle database is limited, and as a result, the number of simultaneous transfer runs to a single Oracle database is limited to that maximum amount.
  - You must [set up a network attachment](https://docs.cloud.google.com/vpc/docs/create-manage-network-attachments) in cases where a public IP is not available for an Oracle database connection, with the following requirements:
      - The data source must be accessible from the subnet where the network attachment resides.
      - The network attachment must not be in the subnet within the range `240.0.0.0/24` .
      - Network attachments cannot be deleted if there are active connections to the attachment. To delete a network attachment, [contact Cloud Customer Care](https://docs.cloud.google.com/bigquery/docs/getting-support) .
      - For the `us` multi-region, the network attachment must be in the `us-central1` region. For the `eu` multi-region, the network attachment must be in the `europe-west4` region.
  - The minimum interval time between recurring Oracle transfers is 15 minutes. The default interval for a recurring transfer is 24 hours.
  - A single transfer configuration can only support one data transfer run at a given time. In the case where a second data transfer is scheduled to run before the first transfer is completed, then only the first data transfer completes while any other data transfers that overlap with the first transfer is skipped.
      - To avoid skipped transfers within a single transfer configuration, we recommend that you increase the duration of time between large data transfers by configuring the **Repeat frequency** .
  - During a data transfer, the Oracle connector identifies indexed and partitioned key columns to transfer your data in parallel batches. For this reason, we recommend that you specify primary key columns or use indexed columns in your table to improve the performance and reduce the error rate in your data transfers.
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
      - Oracle data transfers that don't use primary key or indexed columns can't support more than 2,000,000 records per table.
  - If your configured network attachment and virtual machine (VM) instance are located in different regions, there might be cross-region data movement when you transfer data from Oracle.

### Incremental transfer limitations

Incremental Oracle transfers are subject to the following limitations:

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

To learn about how incremental transfers work, see [Full or incremental transfers](https://docs.cloud.google.com/bigquery/docs/oracle-transfer-intro#full-incremental-transfers) .

## Before you begin

The following sections describe the steps that you need to take before you create an Oracle transfer.

### Oracle prerequisites

  - [Create a User credential](https://docs.oracle.com/cd/B13789_01/server.101/b10759/statements_8003.htm) in the Oracle database.
  - [Grant `Create Session` system privileges to the user](https://docs.oracle.com/cd/B13789_01/server.101/b10759/statements_9013.htm) to allow session creation.
  - [Assign a tablespace](https://docs.oracle.com/cd/B19306_01/network.102/b14266/admusers.htm#i1006219) to the user account.

You must also have the following Oracle database information when creating an Oracle transfer.

| Parameter Name | Description                             |
| -------------- | --------------------------------------- |
| `database`     | Name of the database.                   |
| `host`         | Hostname or IP address of the database. |
| `port`         | Port number of the database.            |
| `username`     | Username to access the database.        |
| `password`     | Password to access the database.        |

### BigQuery prerequisites

  - Verify that you have completed all actions required to [enable the BigQuery Data Transfer Service](https://docs.cloud.google.com/bigquery/docs/enable-transfer-service) .
  - [Create a BigQuery dataset](https://docs.cloud.google.com/bigquery/docs/datasets) to store your data.
  - If you intend to set up transfer run notifications for Pub/Sub, verify that you have the `pubsub.topics.setIamPolicy` Identity and Access Management (IAM) permission. Pub/Sub permissions are not required if you only set up email notifications. For more information, see [BigQuery Data Transfer Service run notifications](https://docs.cloud.google.com/bigquery/docs/transfer-run-notifications) .

### Required BigQuery roles

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

## Load Oracle data into BigQuery

Add Oracle data into BigQuery by setting up a transfer configuration using one of the following options:

### Console

1.  Go to the Data transfers page in the Google Cloud console.

2.  Click add **Create transfer** .

3.  In the **Source type** section, for **Source** , select **Oracle** .

4.  In the **Data source details** section, do the following:
    
      - For **Network attachment** , select an existing network attachment or click **Create Network Attachment** .
      - For **Host** , enter the hostname or IP of the database.
      - For **Port** , enter the port number that the Oracle database is using for incoming connections, such as `1521` .
      - For **Database name** , enter the name of the Oracle database.
      - For **Connection type** , enter the connection URL type, either `SERVICE` , `SID` , or `TNS` .
      - For **Username** , enter the username of the user initiating the Oracle database connection.
      - For **Password** , enter the password of the user initiating the Oracle database connection.
      - For **TLS Mode** , select an option from the drop-down menu. For more information about TLS modes, see [TLS configuration](https://docs.cloud.google.com/bigquery/docs/oracle-transfer-intro#tls-configuration) .
      - For **Trusted PEM Certificate** , enter the public certificate of the certificate authority (CA) that issued the TLS certificate of the database server. For more information, see [Trusted Server Certificate (PEM)](https://docs.cloud.google.com/bigquery/docs/oracle-transfer-intro#trusted_server_certificate_pem) .
      - For **Ingestion type** , select **Full** or **Incremental** .
          - If you select **Incremental** ( [Preview](https://cloud.google.com/products#product-launch-stages) ), for **Write mode** , select either **Append** or **Upsert** . For more information about the different write modes, see [Full or incremental transfers](https://docs.cloud.google.com/bigquery/docs/oracle-transfer-intro#full-incremental-transfers) .
      - For **Oracle objects to transfer** , click **Browse** :
          - Select any objects to be transferred to the BigQuery destination dataset. You can also manually enter any objects to include in the data transfer in this field.
          - If you have selected **Append** as your incremental write mode, you must select a column as the watermark column.
          - If you have selected **Upsert** as your incremental write mode, you must select a column as the watermark column, and then select one or more columns as the primary key.

5.  In the **Destination settings** section, for **Dataset** , select the dataset that you created to store your data.

6.  In the **Transfer config name** section, for **Display name** , enter a name for the data transfer.

7.  In the **Schedule options** section:
    
      - In the **Repeat frequency** list, select an option to specify how often this data transfer runs. To specify a custom repeat frequency, select **Custom** . If you select **On-demand** , then this transfer runs when you [manually trigger the transfer](https://docs.cloud.google.com/bigquery/docs/working-with-transfers#manually_trigger_a_transfer) .
      - If applicable, select either **Start now** or **Start at set time** , and provide a start date and run time.

8.  Optional: In the **Notification options** section, do the following:
    
      - To enable email notifications, click the **Email notification** toggle. When you enable this option, the transfer administrator receives an email notification when a transfer run fails.
      - To enable [Pub/Sub transfer run notifications](https://docs.cloud.google.com/bigquery/docs/transfer-run-notifications) for this transfer, click the **Pub/Sub notifications** toggle. You can select your [topic](https://docs.cloud.google.com/pubsub/docs/overview#types) name, or you can click **Create a topic** to create one.

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

Where:

  - PROJECT\_ID (optional): your Google Cloud project ID. If `--project_id` isn't supplied to specify a particular project, the default project is used.

  - DATA\_SOURCE : the data source — `oracle` .

  - DISPLAY\_NAME : the display name for the transfer configuration. The data transfer name can be any value that lets you identify the transfer if you need to modify it later.

  - DATASET : the target dataset for the transfer configuration.

  - PARAMETERS : the parameters for the created transfer configuration in JSON format. For example: `--params='{"param":"param_value"}'` . The following are the parameters for an Oracle data transfer:
    
      - `connector.networkAttachment` (optional): name of the network attachment to connect to the Oracle database.
      - `connector.authentication.Username` : username of the Oracle account.
      - `connector.authentication.Password` : password of the Oracle account.
      - `connector.database` : name of the Oracle database.
      - `connector.endpoint.host` : the hostname or IP of the database.
      - `connector.endpoint.port` : the port number that the Oracle database is using for incoming connections, such as `1520` .
      - `connector.connectionType` : the connection URL type, either `SERVICE` , `SID` , or `TNS` .
      - `connector.tls.mode` : specify a [TLS configuration](https://docs.cloud.google.com/bigquery/docs/oracle-transfer-intro#tls-configuration) to use with this transfer:
          - `ENCRYPT_VERIFY_CA_AND_HOST` to encrypt data, and verify CA and hostname
          - `ENCRYPT_VERIFY_CA` to encrypt data, and verify CA only
          - `ENCRYPT_VERIFY_NONE` for data encryption only
          - `DISABLE` for no encryption or verification
      - `connector.tls.trustedServerCertificate` : (optional) provide one or more [PEM-encoded certificates](https://docs.cloud.google.com/bigquery/docs/oracle-transfer-intro#trusted_server_certificate_pem) . Required only if `connector.tls.mode` is `ENCRYPT_VERIFY_CA_AND_HOST` or `ENCRYPT_VERIFY_CA` .
      - `ingestionType` : specify either `full` or `incremental` . Incremental transfers are supported in [preview](https://cloud.google.com/products#product-launch-stages) . For more information, see [Full or incremental transfers](https://docs.cloud.google.com/bigquery/docs/oracle-transfer-intro#full-incremental-transfers) .
      - `writeMode` : specify either `WRITE_MODE_APPEND` or `WRITE_MODE_UPSERT` .
      - `watermarkColumns` : specify columns in your table as watermark columns. This field is required for incremental transfers.
      - `primaryKeys` : specify columns in your table as primary keys. This field is required for incremental transfers.
      - `assets` : the path to the Oracle objects to be transferred to BigQuery, using the format: `  DATABASE_NAME / SCHEMA_NAME / TABLE_NAME  `

When specifying multiple assets during an incremental transfer, the values of the `watermarkColumns` and `primaryKeys` fields correspond to the position of values in the `assets` field. In the following example, `dep_id` corresponds to the table `DB1/USER1/DEPARTMENT` , while `report_by` and `report_title` corresponds to the table `DB1/USER1/EMPLOYEES` .

``` 
      "primaryKeys":[['dep_id'], ['report_by','report_title']],
      "assets":["DB1/USER1/DEPARTMENT","DB1/USER1/EMPLOYEES"],
  
```

For example, the following command creates an Oracle data transfer in the default project with all the required parameters:

    bq mk
        --transfer_config
        --target_dataset=mydataset
        --data_source=oracle
        --display_name='My Transfer'
        --params='{"assets":["DB1/USER1/DEPARTMENT","DB1/USER1/EMPLOYEES"],
            "connector.authentication.username": "User1",
            "connector.authentication.password":"ABC12345",
            "connector.database":"DB1",
            "connector.endpoint.host":"192.168.0.1",
            "connector.endpoint.port":1520,
            "connector.connectionType":"SERVICE",
            "connector.tls.mode": "ENCRYPT_VERIFY_CA_AND_HOST",
            "connector.tls.trustedServerCertificate": "PEM-encoded certificate",
            "connector.networkAttachment":
            "projects/dev-project1/regions/us-central1/networkattachments/na1"
            "ingestionType":"incremental",
            "writeMode":"WRITE_MODE_APPEND",
            "watermarkColumns":["createdAt","createdAt"],
            "primaryKeys":[['dep_id'], ['report_by','report_title']]}'

### API

Use the [`projects.locations.transferConfigs.create`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs/create) method and supply an instance of the [`TransferConfig`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs#TransferConfig) resource.

When you save the transfer configuration, the Oracle connector automatically triggers a transfer run according to your schedule option. With every transfer run, the Oracle connector transfers all available data from Oracle into BigQuery.

To manually run a data transfer outside of your regular schedule, you can start a [backfill run](https://docs.cloud.google.com/bigquery/docs/working-with-transfers#manually_trigger_a_transfer) .

## Troubleshoot transfer setup

If you are having issues setting up your data transfer, see [Oracle transfer issues](https://docs.cloud.google.com/bigquery/docs/transfer-troubleshooting#oracle-issues) .

## What's next

  - To learn more about BigQuery Data Transfer Service, see [What is BigQuery Data Transfer Service](https://docs.cloud.google.com/bigquery/docs/dts-introduction) .
  - To learn about using transfers, including getting information about a transfer configuration, listing transfer configurations, and viewing a transfer's run history, see [Manage transfers](https://docs.cloud.google.com/bigquery/docs/working-with-transfers) .
  - To learn how to load data with BigQuery Omni operations, see [Load data with BigQuery Omni operations](https://docs.cloud.google.com/bigquery/docs/load-data-using-cross-cloud-transfer) .
