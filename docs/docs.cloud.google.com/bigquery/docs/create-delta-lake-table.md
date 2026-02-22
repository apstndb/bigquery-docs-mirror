# Create BigLake external tables for Delta Lake

**Important:** The term "BigLake" on this page refers to an access delegation functionality for external tables in BigQuery. For information about BigLake, the stand-alone Google Cloud product that includes BigLake metastore, the Apache Iceberg REST catalog, and BigLake tables for Apache Iceberg see [BigLake overview](/biglake/docs/introduction) .

BigLake lets you access Delta Lake tables with more granular access control. [Delta Lake](https://docs.databricks.com/en/delta/index.html) is an open source, tabular data storage format developed by Databricks that supports petabyte scale data tables.

BigQuery supports the following features with Delta Lake tables:

  - **Access delegation** : Query structured data in external data stores with access delegation. Access delegation decouples access to the Delta Lake table from access to the underlying datastore.
  - **Fine-grained access control** : Enforce fine-grained security at the table level, including [row-level](/bigquery/docs/row-level-security-intro) and [column-level](/bigquery/docs/column-level-security-intro) security. For Delta Lake tables based on Cloud Storage, you can also use [dynamic data masking](/bigquery/docs/column-data-masking) .
  - **Schema evolution** : Schema changes in the Delta Lake tables are autodetected. Changes to the schema are reflected in the BigQuery table.

Delta Lake tables also support all BigLake features when you configure them as [BigLake tables](/bigquery/docs/biglake-intro) .

## Before you begin

Enable the BigQuery Connection and BigQuery Reservation APIs.

**Roles required to enable APIs**

To enable APIs, you need the Service Usage Admin IAM role ( `  roles/serviceusage.serviceUsageAdmin  ` ), which contains the `  serviceusage.services.enable  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .

1.  In the Google Cloud console, on the project selector page, select or create a Google Cloud project.
    
    **Roles required to select or create a project**
    
      - **Select a project** : Selecting a project doesn't require a specific IAM role—you can select any project that you've been granted a role on.
      - **Create a project** : To create a project, you need the Project Creator role ( `  roles/resourcemanager.projectCreator  ` ), which contains the `  resourcemanager.projects.create  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .
    
    **Note** : If you don't plan to keep the resources that you create in this procedure, create a project instead of selecting an existing project. After you finish these steps, you can delete the project, removing all resources associated with the project.

2.  [Verify that billing is enabled for your Google Cloud project](/billing/docs/how-to/verify-billing-enabled#confirm_billing_is_enabled_on_a_project) .

3.  Enable the BigQuery Connection and BigQuery Reservation APIs.
    
    **Roles required to enable APIs**
    
    To enable APIs, you need the Service Usage Admin IAM role ( `  roles/serviceusage.serviceUsageAdmin  ` ), which contains the `  serviceusage.services.enable  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .

4.  In the Google Cloud console, activate Cloud Shell.

5.  Ensure that you have a BigQuery [dataset](/bigquery/docs/datasets) .

6.  Ensure that your version of the Google Cloud SDK is 366.0.0 or later:
    
    ``` text
    gcloud version
    ```
    
    If needed, [update the Google Cloud SDK](/sdk/docs/quickstart) .

7.  Create a [Cloud resource connection](/bigquery/docs/create-cloud-resource-connection#create-cloud-resource-connection) based on your external data source, and grant that connection [access to Cloud Storage](/bigquery/docs/create-cloud-resource-connection#access-storage) . If you don't have the appropriate permissions to create a connection, ask your BigQuery administrator to create a connection and share it with you.

### Required roles

The following permissions are required to create a Delta Lake table:

  - `  bigquery.tables.create  `
  - `  bigquery.connections.delegate  `

The BigQuery Admin ( `  roles/bigquery.admin  ` ) predefined Identity and Access Management role includes these permissions.

If you are not a principal in this role, ask your administrator to grant you these permissions or to create the Delta Lake table for you.

Additionally, to allow BigQuery users to query the table, the service account associated with the connection must have the following permission and access:

  - BigQuery Viewer ( `  roles/bigquery.viewer  ` ) role
  - BigQuery Connection User ( `  roles/bigquery.connectionUser  ` ) role
  - Access to the Cloud Storage bucket that contains that data

For more information on Identity and Access Management roles and permissions in BigQuery, see [Predefined roles and permissions](/bigquery/docs/access-control) .

## Create tables with Delta Lake

To create Delta Lake tables, follow these steps.

### SQL

Use the [`  CREATE EXTERNAL TABLE  ` statement](/bigquery/docs/reference/standard-sql/data-definition-language#create_external_table_statement) to create the Delta Lake table:

``` text
CREATE EXTERNAL TABLE `PROJECT_ID.DATASET.DELTALAKE_TABLE_NAME`
WITH CONNECTION `PROJECT_ID.REGION.CONNECTION_ID`
OPTIONS (
  format ="DELTA_LAKE",
  uris=['DELTA_TABLE_GCS_BASE_PATH']);
```

Replace the following values:

  - PROJECT\_ID : the ID of the project that you want to create the Delta Lake table in

  - DATASET : the BigQuery dataset to contain the Delta Lake table

  - DELTALAKE\_TABLE\_NAME : the name of your Delta Lake table

  - REGION : the region that contains the connection to create the Delta Lake table—for example, `  us  `

  - CONNECTION\_ID : the connection ID—for example, `  myconnection  `
    
    When you [view the connection details](/bigquery/docs/working-with-connections#view-connections) in the Google Cloud console, the connection ID is the value in the last section of the fully qualified connection ID that is shown in Connection ID—for example `  projects/myproject/locations/connection_location/connections/myconnection  ` .

  - DELTA\_TABLE\_GCS\_BASE\_PATH : the Delta Lake table prefix

### bq

In a command-line environment, use the [`  bq mk  `](/bigquery/docs/reference/bq-cli-reference#bq_mk) command to create the Delta Lake table:

``` text
bq mk --table --external_table_definition=DEFINITION_FILE PROJECT_ID:DATASET.DELTALAKE_TABLE_NAME
```

Replace the following values:

  - DEFINITION\_FILE : the path to a table definition file
  - PROJECT\_ID : the ID of the project that you want to create the Delta Lake table in
  - DATASET : the BigQuery dataset to contain the Delta Lake table
  - DELTALAKE\_TABLE\_NAME : the name of your Delta Lake table

### REST

Use the [BigQuery API](/bigquery/docs/reference/rest) to create a Delta Lake table by calling the `  tables.insert  ` API method:

``` text
REQUEST='{
  "autodetect": true,
  "externalDataConfiguration": {
  "sourceFormat": "DELTA_LAKE",
  "connectionId": "PROJECT_ID.REGION.CONNECTION_ID",
  "sourceUris": [
    "DELTA_TABLE_GCS_BASE_PATH"
  ],
 },
"tableReference": {
"tableId": "DELTALAKE_TABLE_NAME"
}
}'

echo $REQUEST | curl -X POST -d @- -H "Content-Type: application/json" -H "Authorization: Bearer $(gcloud auth print-access-token)" https://bigquery.googleapis.com/bigquery/v2/projects/PROJECT_ID/datasets/DATASET/tables?autodetect_schema=true
```

Replace the following values:

  - PROJECT\_ID : the ID of the project that you want to create the Delta Lake table in

  - REGION : the region that contains the connection to create the Delta Lake table—for example, `  us  `

  - CONNECTION\_ID : the connection ID—for example, `  myconnection  `
    
    When you [view the connection details](/bigquery/docs/working-with-connections#view-connections) in the Google Cloud console, the connection ID is the value in the last section of the fully qualified connection ID that is shown in Connection ID—for example `  projects/myproject/locations/connection_location/connections/myconnection  ` .

  - DELTA\_TABLE\_GCS\_BASE\_PATH : the Delta Lake table prefix

  - DELTALAKE\_TABLE\_NAME : the name of your Delta Lake table

  - DATASET : the BigQuery dataset to contain the Delta Lake table

When you create Delta Lake tables, the Delta Lake prefix is used as the URI for the table. For example, for a table that has logs in the bucket `  gs://bucket/warehouse/basictable/_delta_log  ` , the table URI is `  gs://bucket/warehouse/basictable  ` . When you run queries on the Delta Lake table, BigQuery reads data under the prefix to identify the current version of the table and then computes the metadata and the files for the table.

Although you can create Delta Lake external tables without a connection, it is not recommended for the following reasons:

  - Users might experience `  ACCESS_DENIED  ` errors when trying to access files on Cloud Storage.
  - Features such as fine-grained access control are only available in Delta Lake BigLake tables.

## Update Delta Lake tables

To update (refresh) the schema of Delta Lake tables, follow these steps.

### bq

In a command-line environment, use the [`  bq update  `](/bigquery/docs/reference/bq-cli-reference#bq_update) command to update (refresh) the schema of the Delta Lake table:

``` text
bq update --autodetect_schema PROJECT_ID:DATASET.DELTALAKE_TABLE_NAME
```

Replace the following values:

  - PROJECT\_ID : the ID of the project that you want to create the Delta Lake table in
  - DATASET : the BigQuery dataset to contain the Delta Lake table
  - DELTALAKE\_TABLE\_NAME : the name of your Delta Lake table

### REST

Use the [BigQuery API](/bigquery/docs/reference/rest) to update a Delta Lake table by calling the `  tables.patch  ` API method:

``` text
REQUEST='{
  "externalDataConfiguration": {
    "sourceFormat": "DELTA_LAKE",
    "sourceUris": [
      "DELTA_TABLE_GCS_BASE_PATH"
    ],
    "connectionId": "PROJECT_ID.REGION.CONNECTION_ID",
    "autodetect": true
  }
}'
echo $REQUEST |curl -X PATCH -d @- -H "Content-Type: application/json" -H "Authorization: Bearer $(gcloud auth print-access-token)" https://bigquery.googleapis.com/bigquery/v2/projects/PROJECT_ID/datasets/DATASET/tables/DELTALAKE_TABLE_NAME?autodetect_schema=true
```

Replace the following values:

  - DELTA\_TABLE\_GCS\_BASE\_PATH : the Delta Lake table prefix

  - PROJECT\_ID : the ID of the project that you want to create the Delta Lake table in

  - REGION : the region that contains the connection to create the Delta Lake table—for example, `  us  `

  - CONNECTION\_ID : the connection ID—for example, `  myconnection  `
    
    When you [view the connection details](/bigquery/docs/working-with-connections#view-connections) in the Google Cloud console, the connection ID is the value in the last section of the fully qualified connection ID that is shown in Connection ID—for example `  projects/myproject/locations/connection_location/connections/myconnection  ` .

  - DELTALAKE\_TABLE\_NAME : the name of your Delta Lake table

  - DATASET : the BigQuery dataset to contain the Delta Lake table

## Query Delta Lake tables

After creating a Delta Lake BigLake table, you can [query it using GoogleSQL syntax](/bigquery/docs/running-queries) , the same as you would a standard BigQuery table. For example:

``` text
SELECT field1, field2 FROM mydataset.my_cloud_storage_table;
```

For more information, see [Query Cloud Storage data in BigLake tables](/bigquery/docs/query-cloud-storage-using-biglake#query-biglake-table-bigquery) .

An [external connection](/bigquery/docs/connections-api-intro) associated with a service account is used to connect to the datastore. Because the service account retrieves data from the datastore, users only need access to the Delta Lake table.

## Data mapping

BigQuery converts Delta Lake data types to BigQuery data types as shown in the following table:

<table>
<thead>
<tr class="header">
<th><strong>Delta Lake Type</strong></th>
<th><strong>BigQuery Type</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       boolean      </code></td>
<td><code dir="ltr" translate="no">       BOOL      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       byte      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       int      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       long      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       float      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       double      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       Decimal(P/S)      </code></td>
<td><code dir="ltr" translate="no">       NUMERIC      </code> or <code dir="ltr" translate="no">       BIG_NUMERIC      </code> depending on precision</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       date      </code></td>
<td><code dir="ltr" translate="no">       DATE      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       time      </code></td>
<td><code dir="ltr" translate="no">       TIME      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       timestamp (not partition column)      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       timestamp (partition column)      </code></td>
<td><code dir="ltr" translate="no">       DATETIME      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       string      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       binary      </code></td>
<td><code dir="ltr" translate="no">       BYTES      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       array&lt;Type&gt;      </code></td>
<td><code dir="ltr" translate="no">       ARRAY&lt;Type&gt;      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       struct      </code></td>
<td><code dir="ltr" translate="no">       STRUCT      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       map&lt;KeyType, ValueType&gt;      </code></td>
<td><code dir="ltr" translate="no">       ARRAY&lt;Struct&lt;key KeyType, value ValueType&gt;&gt;      </code></td>
</tr>
</tbody>
</table>

## Limitations

Delta Lake tables have [BigLake table limitations](/bigquery/docs/biglake-intro#limitations) and also the following limitations:

  - Supports Delta Lake [reader version](https://github.com/delta-io/delta/blob/master/PROTOCOL.md#reader-version-requirements) 3 with relative path deletion vectors and column mapping.
  - Doesn't support Delta Lake V2 checkpoints.
  - You must list the reader version in the last log entry file. For example, new tables must include `  00000..0.json  ` .
  - Change data capture (CDC) operations aren't supported. Any existing CDC operations are ignored.
  - The schema is autodetected. Modifying the schema by using BigQuery isn't supported.
  - Table column names must adhere to BigQuery [column name restrictions](/bigquery/docs/schemas#column_names) .
  - Materialized views aren't supported.
  - The Read API isn't supported for Delta Lake.
  - The `  timestamp_ntz  ` data type isn't supported for Delta Lake BigLake tables.

## Troubleshooting

This section provides help with Delta Lake BigLake tables. For more general help with troubleshooting BigQuery queries, see [Troubleshoot query issues](/bigquery/docs/troubleshoot-queries) .

### Query timeout and resource errors

Check the logs directory ( `  gs://bucket/warehouse/basictable/_delta_log  ` ) of the Delta Lake table and look for JSON files with a version number greater than the previous [checkpoint](https://github.com/delta-io/delta/blob/master/PROTOCOL.md#checkpoints) . You can obtain the version number by listing the directory or inspecting the [\_delta\_log/\_last\_checkpoint file](https://github.com/delta-io/delta/blob/master/PROTOCOL.md#last-checkpoint-file) . JSON files larger than 10 MiB can slow down table expansion which can lead to timeout and resource issues. To resolve this issue, use the following command to create a new checkpoint so that queries skip reading the JSON files:

``` text
  spark.sql("ALTER TABLE delta.`gs://bucket/mydeltatabledir` SET TBLPROPERTIES ('delta.checkpointInterval' = '1')");
```

Users can then use the same command to reset the checkpoint interval to either the default value of 10 or to a value that avoids having more than 50 MB of JSON files between checkpoints.

### Invalid column name

Ensure that column mapping is turned on for the Delta Lake table. Column mapping is supported with [Reader version 2 or greater](https://github.com/delta-io/delta/blob/master/PROTOCOL.md#reader-version-requirements) . For Reader version 1, set 'delta.columnMapping.mode' to 'name' by using the following command:

``` text
spark.sql("ALTER TABLE delta.`gs://bucket/mydeltatabledir` SET TBLPROPERTIES ('delta.columnMapping.mode' = 'name', 'delta.minReaderVersion' = '3', 'delta.minWriterVersion' = '7')");
```

If the invalid column name adheres to [flexible column name restrictions](/bigquery/docs/schemas#flexible-column-names) , contact [Cloud Customer Care](/bigquery/docs/getting-support) or <biglake-help@google.com> .

### Access denied errors

To diagnose issues with Delta Lake BigLake tables, check the following:

  - Ensure that you are using Delta Lake BigLake tables [(with a connection)](#create-tables) .

  - Users have [required permission outlined](#iam-permissions) .

## Performance

To improve query performance, try the following steps:

  - Use [Delta Lake utilities](https://docs.databricks.com/en/delta/best-practices.html) to compact the underlying data files and remove redundant files, such as data and metadata.

  - Ensure that `  delta.checkpoint.writeStatsAsStruct  ` is set to `  true  ` .

  - Ensure that variables that are frequently used in predicate clauses are in partition columns.

Large datasets (greater than 100 TB) might benefit from additional configurations and features. If the preceding steps do not resolve your issues, consider contacting [Customer Care](/bigquery/docs/getting-support) or <biglake-help@google.com> , especially for datasets larger than 100 TB.
