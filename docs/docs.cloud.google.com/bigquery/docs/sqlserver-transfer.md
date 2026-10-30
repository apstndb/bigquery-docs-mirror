---
name: documents/docs.cloud.google.com/bigquery/docs/sqlserver-transfer
uri: https://docs.cloud.google.com/bigquery/docs/sqlserver-transfer
title: Load Microsoft SQL Server data into BigQuery
description: Learn how to use the BigQuery Data Transfer Service Microsoft SQL Server connector to ingest data from your Microsoft SQL Server instance into BigQuery.
data_source: docs.cloud.google.com
---

# Load Microsoft SQL Server data into BigQuery

> **Preview**
>
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

Note: To get support or provide feedback for this feature, contact <dts-preview-support@google.com> .

To schedule recurring data transfers from Microsoft SQL Server to BigQuery, you can create a transfer configuration to specify what data objects to transfer, and how often to schedule the data transfer. After you set up the transfer configuration, the [BigQuery Data Transfer Service](https://docs.cloud.google.com/bigquery/docs/dts-introduction) transfers the latest data into a BigQuery table on the specified schedule.

To learn about how a Microsoft SQL Server transfer works, see [Introduction to Microsoft SQL Server data transfers](https://docs.cloud.google.com/bigquery/docs/sqlserver-transfer-intro) .

## Limitations

Microsoft SQL Server data transfer jobs are subject to the following limitations:

- There is a limited number of simultaneous connections to a Microsoft SQL Server database. Therefore, the number of simultaneous transfer runs to a single Microsoft SQL Server database is also limited. Ensure that the number of concurrent transfer jobs is less than the maximum number of concurrent connections supported by the Microsoft SQL Server database.
- Some Microsoft SQL Server data types might be mapped to the `STRING` type in BigQuery to avoid data loss. For example, certain numeric types in Microsoft SQL Server that don't have precision and scale defined might be mapped to `STRING` in BigQuery. For more information, see [Data type mapping](https://docs.cloud.google.com/bigquery/docs/sqlserver-transfer-intro#data-type-mapping) .

### Incremental transfer limitations

Incremental Microsoft SQL Server transfers are subject to the following limitations:

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

Before you can schedule a Microsoft SQL Server data transfer, you must meet the following prerequisites.

### Microsoft SQL Server prerequisites

You must have created a user account in the Microsoft SQL Server database. For more information, see [Create a user with a login](https://learn.microsoft.com/en-us/sql/relational-databases/security/authentication-access/create-a-database-user?view=sql-server-ver17#create-a-user-with-a-login) .

### BigQuery prerequisites

- Verify that you have completed all the actions that are required to [enable the BigQuery Data Transfer Service](https://docs.cloud.google.com/bigquery/docs/enable-transfer-service) .
- [Create a BigQuery dataset](https://docs.cloud.google.com/bigquery/docs/datasets) to store your data.

#### Required roles

To get the permissions that you need to create a Microsoft SQL Server data transfer, ask your administrator to grant you the [BigQuery Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin) ( `roles/bigquery.admin` ) IAM role on your project. For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

This predefined role contains the permissions required to create a Microsoft SQL Server data transfer. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

The following permissions are required to create a Microsoft SQL Server data transfer:

- `bigquery.transfers.update`
- `bigquery.datasets.get`

You might also be able to get these permissions with [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

### Network configuration

You must set up specific network configurations when a public IP address isn't available for the Microsoft SQL Server database connection. For more information, see the following sections:

- [Configure a connection to Google Cloud instance](https://docs.cloud.google.com/bigquery/docs/cloud-sql-instance-access)
- [Configure a connection to AWS](https://docs.cloud.google.com/bigquery/docs/aws-vpn-network-attachment)
- [Configure a connection to Azure](https://docs.cloud.google.com/bigquery/docs/azure-vpn-network-attachment)

## Set up a Microsoft SQL Server data transfer

Select one of the following options:

### Console

1.  Go to the **Data transfers** page.

2.  Click add **Create transfer** .

3.  In the **Source type** section, for **Source** , select **Microsoft SQL Server** .

4.  In the **Data source details** section, do the following:

    - For **Network attachment** , select an existing network attachment or click **Create Network Attachment** .
    - For **Host** , enter the hostname or IP address of the Microsoft SQL Server database.
    - For **Port number** , enter the port number for the Microsoft SQL Server database.
    - For **Database name** , enter the name of the Microsoft SQL Server database.
    - For **Username** , enter the username of the Microsoft SQL Server user initiating the Microsoft SQL Server database connection.
    - For **Password** , enter the password of the Microsoft SQL Server user initiating the Microsoft SQL Server database connection.
    - For **TLS Mode** , select an option from the menu. For more information about TLS modes, see [TLS configuration](https://docs.cloud.google.com/bigquery/docs/sqlserver-transfer-intro#tls-configuration) .
    - For **Trusted PEM Certificate** , enter the public certificate of the certificate authority (CA) that issued the TLS certificate of the database server. For more information, see [Trusted Server Certificate (PEM)](https://docs.cloud.google.com/bigquery/docs/sqlserver-transfer-intro#trusted_server_certificate_pem) .
    - For **Enable legacy mapping** , select **true** (default) to use the [legacy data type mapping](https://docs.cloud.google.com/bigquery/docs/sqlserver-transfer-intro#data-type-mapping) . Select **false** to use the updated data type mapping. If you are making an incremental transfer, this value must be **false** . For more information about the data type mapping updates, see [March 16, 2027](https://docs.cloud.google.com/bigquery/docs/transfer-changes#Mar16-sqlserver) . database server.
    - For **Ingestion type** , select **Full** or **Incremental** .
      - If you select **Incremental** ( [Preview](https://cloud.google.com/products#product-launch-stages) ), for **Write mode** , select either **Append** or **Upsert** . For more information about the different write modes, see [Full or incremental transfers](https://docs.cloud.google.com/bigquery/docs/sqlserver-transfer-intro#full-incremental-transfers) .
    - For **Microsoft SQL Server objects to transfer** , browse the Microsoft SQL Server table or manually enter the names of the tables that are required for the transfer.

5.  In the **Destination settings** section, for **Dataset** , select the dataset that you created to store your data, or click **Create new dataset** and create one to use as the destination dataset.

6.  In the **Transfer config name** section, for **Display name** , enter a name for the transfer. The transfer name can be any value that lets you identify the transfer if you need to modify it later.

7.  In the **Schedule options** section, do the following:

    - Select a repeat frequency. If you select the **Hours** , **Days** (default), **Weeks** , or **Months** option, you must also specify a frequency. You can also select the **Custom** option to create a more specific repeat frequency. If you select the **On-demand** option, this data transfer only runs when you [manually trigger the transfer](https://docs.cloud.google.com/bigquery/docs/working-with-transfers#manually_trigger_a_transfer) .
    - If applicable, select either the **Start now** or **Start at a set time** option and provide a start date and run time.

8.  Optional: In the **Notification options** section, do the following:

    - To enable email notifications, click the **Email notifications** toggle to the on position. When you enable this option, the transfer administrator receives an email notification when a transfer run fails.
    - To configure Pub/Sub run [notifications](https://docs.cloud.google.com/bigquery/docs/transfer-run-notifications) for your transfer, click the **Pub/Sub notifications** toggle to the on position. You can select your [topic](https://docs.cloud.google.com/pubsub/docs/admin) name or click **Create a topic** to create one.

9.  Optional: In the **Advanced options** section, select an encryption type for this transfer. You can select either a Google-owned and Google-managed encryption key or a customer-owned Cloud Key Management Service key. For more information about encryption keys, see [Customer-managed encryption keys (CMEK)](https://docs.cloud.google.com/kms/docs/cmek) .

10. Click **Save** .

### bq

Enter the [`bq mk` command](https://docs.cloud.google.com/bigquery/docs/reference/bq-cli-reference#bq_mk) and supply the transfer creation flag `--transfer_config` :

```
bq mk \
    --transfer_config \
    --project_id=PROJECT_ID \
    --data_source=DATA_SOURCE \
    --display_name=DISPLAY_NAME \
    --target_dataset=DATASET \
    --params='PARAMETERS'
```

Replace the following:

- `PROJECT_ID` (optional): your Google Cloud project ID. If the `--project_id` flag isn't supplied to specify a particular project, the default project is used.

- `DATA_SOURCE` : the data source, which is `sqlserver` .

- `DISPLAY_NAME` : the display name for the data transfer configuration. The transfer name can be any value that lets you identify the transfer if you need to modify it later.

- `DATASET` : the target dataset for the data transfer configuration.

- `PARAMETERS` : the parameters for the created transfer configuration in JSON format. For example: `--params='{"param":"param_value"}'` . The following are the parameters for a Microsoft SQL Server transfer:

  - `connector.networkAttachment` (optional): the name of the network attachment to connect to the Microsoft SQL Server database.
  - `connector.database` : the name of the Microsoft SQL Server database.
  - `connector.endpoint.host` : the hostname or IP address of the database.
  - `connector.endpoint.port` : the port number of the database.
  - `connector.authentication.username` : the username of the database user.
  - `connector.authentication.password` : the password of the database user.
  - `connector.legacyMapping` : set to `true` (default) to use the [legacy data type mapping](https://docs.cloud.google.com/bigquery/docs/sqlserver-transfer-intro#data-type-mapping) . Set to `false` to use the updated data type mapping. If you are making an incremental transfer, this value must be `false` . For more information about the data type mapping updates, see [March 16, 2027](https://docs.cloud.google.com/bigquery/docs/transfer-changes#Mar16-sqlserver) .
  - `connector.tls.mode` : specify a [TLS configuration](https://docs.cloud.google.com/bigquery/docs/sqlserver-transfer-intro#tls-configuration) to use with this transfer:
    - `ENCRYPT_VERIFY_CA_AND_HOST` to encrypt data, and verify CA and hostname
    - `ENCRYPT_VERIFY_CA` to encrypt data, and verify CA only
    - `ENCRYPT_VERIFY_NONE` for data encryption only
    - `DISABLE` for no encryption or verification
  - `connector.tls.trustedServerCertificate` : (optional) provide one or more [PEM-encoded certificates](https://docs.cloud.google.com/bigquery/docs/sqlserver-transfer-intro#trusted_server_certificate_pem) . Required only if the value of `connector.tls.mode` is `ENCRYPT_VERIFY_CA_AND_HOST` or `ENCRYPT_VERIFY_CA` .
  - `ingestionType` : specify either `full` or `incremental` . Incremental transfers are supported in [preview](https://cloud.google.com/products#product-launch-stages) . For more information, see [Full or incremental transfers](https://docs.cloud.google.com/bigquery/docs/sqlserver-transfer-intro#full-incremental-transfers) .
  - `writeMode` : specify either `WRITE_MODE_APPEND` or `WRITE_MODE_UPSERT` .
  - `watermarkColumns` : specify columns in your table as watermark columns. This field is required for incremental transfers.
  - `primaryKeys` : specify columns in your table as primary keys. This field is required for incremental transfers.
  - `assets` : a list of the names of the Microsoft SQL Server tables to be transferred from the Microsoft SQL Server database as part of the transfer.

For example, the following command creates a Microsoft SQL Server transfer called `My Transfer` :

```
bq mk \
    --transfer_config
    --target_dataset=mydataset
    --data_source=sqlserver
    --display_name='My Transfer'
    --params='{"assets":["DB1/DEPARTMENT","DB1/EMPLOYEES"],
        "connector.authentication.username": "User1",
        "connector.authentication.password":"ABC12345",
        "connector.database":"DB1",
        "connector.endpoint.host":"192.168.0.1",
        "connector.endpoint.port":"1520",
        "connector.networkAttachment":"projects/dev-project1/regions/us-central1/networkattachments/na1",
        "ingestionType":"incremental",
        "writeMode":"WRITE_MODE_APPEND",
        "watermarkColumns":["createdAt","createdAt"],
        "primaryKeys":[['dep_id'], ['report_by','report_title']],
        "connector.tls.mode": "ENCRYPT_VERIFY_CA_AND_HOST",
        "connector.tls.trustedServerCertificate": "PEM-encoded certificate"}'
```

When specifying multiple assets during an incremental transfer, the values of the `watermarkColumns` and `primaryKeys` fields correspond to the position of values in the `assets` field. In the following example, `dep_id` corresponds to the table `DB1/DEPARTMENT` , while `report_by` and `report_title` corresponds to the table `DB1/EMPLOYEES` .

```
"primaryKeys":[['dep_id'], ['report_by','report_title']],
      "assets":["DB1/DEPARTMENT","DB1/EMPLOYEES"],
```

When you save the transfer configuration, the Microsoft SQL Server connector automatically triggers a transfer run according to your schedule option. With every transfer run, the Microsoft SQL Server connector transfers all available data from Microsoft SQL Server into BigQuery.

To manually run a data transfer outside of your regular schedule, you can start a [backfill run](https://docs.cloud.google.com/bigquery/docs/working-with-transfers#manually_trigger_a_transfer) .

## Troubleshoot

To troubleshoot issues for your data transfer, see [Microsoft SQL Server transfer issues](https://docs.cloud.google.com/bigquery/docs/transfer-troubleshooting#sqlserver-issues) .

## Transfer metadata

You can also use the Microsoft SQL Server connector to [transfer metadata to Knowledge Catalog](https://docs.cloud.google.com/knowledge-catalog/docs/connectors) . For more information, see [Load Microsoft SQL Server metadata into Knowledge Catalog](https://docs.cloud.google.com/knowledge-catalog/docs/sql-server-transfer) .

## What's next

- Read [an overview about the BigQuery Data Transfer Service](https://docs.cloud.google.com/bigquery/docs/dts-introduction) .
- Learn about [managing transfers](https://docs.cloud.google.com/bigquery/docs/working-with-transfers) , including getting information about a transfer configuration, listing transfer configurations, and viewing a transfer's run history.
- Learn how to [load data with BigQuery Omni operations](https://docs.cloud.google.com/bigquery/docs/load-data-using-cross-cloud-transfer) .
