# Create Apache Iceberg external tables

Apache Iceberg external tables let you access [Apache Iceberg](https://iceberg.apache.org/docs/latest/) tables with finer-grained access control in a read-only format.

Iceberg is an open source table format that supports petabyte scale data tables. The Iceberg open specification lets you run multiple query engines on a single copy of data stored in an object store. Apache Iceberg external tables (hereafter called *Iceberg external tables* ) support [Iceberg specification version 2](https://iceberg.apache.org/spec/#version-2-row-level-deletes) , including merge-on-read.

As a BigQuery administrator, you can enforce row- and column-level access control including data masking on tables. For information about how to set up access control at the table level, see [Set up access control policies](#set-access-control) . Table access policies are also enforced when you use the BigQuery Storage API as a data source for the table in Dataproc and Serverless Spark.

You can create Iceberg external tables in the following ways:

  - **[With BigLake metastore (recommended for Google Cloud)](/biglake/docs/about-blms) .** BigLake metastore is a unified, managed, serverless, and scalable metastore that connects lakehouse data stored in Google Cloud to multiple runtimes, including open source engines (like Apache Spark) and BigQuery.

  - **[With AWS Glue Data Catalog (recommended for AWS)](/bigquery/docs/glue-federated-datasets) .** AWS Glue is the recommended method for AWS because it's a centralized metadata repository where you define the structure and location of your data stored in various AWS services and provides capabilities like automatic schema discovery and integration with AWS analytics tools.

  - **[With Iceberg JSON metadata files](#create-using-metadata-file) (recommended for Azure).** If you use an Iceberg JSON metadata file, then you must manually update the latest metadata file whenever there are any table updates. You can use a BigQuery stored procedure for Apache Spark to create Iceberg external tables that reference an Iceberg metadata file.

For a full list of limitations, see [Limitations](#limitations) .

## Before you begin

Enable the BigQuery Connection and BigQuery Reservation APIs.

**Roles required to enable APIs**

To enable APIs, you need the Service Usage Admin IAM role ( `  roles/serviceusage.serviceUsageAdmin  ` ), which contains the `  serviceusage.services.enable  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .

  - If you use a stored procedure for Spark in BigQuery to create Iceberg external tables, you must follow these steps:
    
    1.  [Create a Spark connection](/bigquery/docs/connect-to-spark#create-spark-connection) .
    2.  [Set up access control for that connection](/bigquery/docs/connect-to-spark#grant-access) .

  - To store the Iceberg external table metadata and data files in Cloud Storage, [create a Cloud Storage bucket](/storage/docs/creating-buckets) . You need to connect to your Cloud Storage bucket to access metadata files. To do so, follow these steps:
    
    1.  [Create a Cloud resource connection](/bigquery/docs/create-cloud-resource-connection#create-cloud-resource-connection) .
    2.  [Set up access for that connection](/bigquery/docs/create-cloud-resource-connection#access-storage) .

### Required roles

To get the permissions that you need to create an Iceberg external table, ask your administrator to grant you the following IAM roles on the project:

  - [BigQuery Admin](/iam/docs/roles-permissions/bigquery#bigquery.admin) ( `  roles/bigquery.admin  ` )
  - [Storage Object Admin](/iam/docs/roles-permissions/storage#storage.objectAdmin) ( `  roles/storage.objectAdmin  ` )

For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

These predefined roles contain the permissions required to create an Iceberg external table. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

The following permissions are required to create an Iceberg external table:

  - `  bigquery.tables.create  `
  - `  bigquery.connections.delegate  `
  - `  bigquery.jobs.create  `

You might also be able to get these permissions with [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

## Create tables with BigLake metastore

We recommend creating Iceberg external tables with [BigLake metastore](/biglake/docs/about-blms) .

## Create tables with a metadata file

You can create Iceberg external tables with a [JSON metadata file](https://iceberg.apache.org/spec/#table-metadata) . However, this is not the recommended method because you have to manually [update the URI of the JSON metadata file](#update-table-metadata) to keep the Iceberg external table up to date. If the URI is not kept up to date, queries in BigQuery can either fail or provide different results from other query engines that directly use an Iceberg catalog.

Iceberg table metadata files are created in the Cloud Storage bucket that you specify when you create an [Iceberg table using Spark](/dataproc-metastore/docs/apache-iceberg#iceberg-table-with-spark) .

Select one of the following options:

### SQL

Use the [`  CREATE EXTERNAL TABLE  ` statement](/bigquery/docs/reference/standard-sql/data-definition-language#create_external_table_statement) . The following example creates an Iceberg external table named `  myexternal-table  ` :

``` googlesql
  CREATE EXTERNAL TABLE myexternal-table
  WITH CONNECTION `myproject.us.myconnection`
  OPTIONS (
         format = 'ICEBERG',
         uris = ["gs://mybucket/mydata/mytable/metadata/iceberg.metadata.json"]
   )
```

Replace the `  uris  ` value with the latest [JSON metadata file](https://iceberg.apache.org/spec/#table-metadata) for a specific table snapshot.

You can enable the *require partition filter* by setting the `  require_partition_filter  ` flag.

### bq

In a command-line environment, use the [`  bq mk --table  ` command](/bigquery/docs/reference/bq-cli-reference#mk-table) with the `  @connection  ` decorator to specify the connection to use at the end of the `  --external_table_definition  ` parameter. To enable the require partition filter, use `  --require_partition_filter  ` .

``` text
bq mk 

    --table 

    --external_table_definition=TABLE_FORMAT=URI@projects/CONNECTION_PROJECT_ID/locations/CONNECTION_REGION/connections/CONNECTION_ID 

    PROJECT_ID:DATASET.EXTERNAL_TABLE
```

Replace the following:

  - `  TABLE_FORMAT  ` : the format of the table that you want to create
    
    In this case, `  ICEBERG  ` .

  - `  URI  ` : the latest [JSON metadata file](https://iceberg.apache.org/spec/#table-metadata) for a specific table snapshot.
    
    For example, `  gs://mybucket/mydata/mytable/metadata/iceberg.metadata.json  ` .
    
    The URI can point to an external cloud location as well; such as Amazon S3 or Azure Blob Storage.
    
      - Example for AWS: `  s3://mybucket/iceberg/metadata/1234.metadata.json  ` .
      - Example for Azure: `  azure://mystorageaccount.blob.core.windows.net/mycontainer/iceberg/metadata/1234.metadata.json  ` .

  - `  CONNECTION_PROJECT_ID  ` : the project that contains the [connection](/bigquery/docs/connect-to-spark) to create the Iceberg external table—for example, `  myproject  `

  - `  CONNECTION_REGION  ` : the region that contains the connection to create the Iceberg external table—for example, `  us  `

  - `  CONNECTION_ID  ` : the table connection ID—for example, `  myconnection  `
    
    When you [view the connection details](/bigquery/docs/working-with-connections#view-connections) in the Google Cloud console, the connection ID is the value in the last section of the fully qualified connection ID that is shown in **Connection ID** —for example `  projects/myproject/locations/connection_location/connections/ myconnection  `

  - `  DATASET  ` : the name of the BigQuery dataset that you want to create a table in
    
    For example, `  mydataset  ` .

  - `  EXTERNAL_TABLE  ` : the name of the table that you want to create
    
    For example, `  mytable  ` .

### Update table metadata

If you use a JSON metadata file to create an Iceberg external table, update the table definition to the latest table metadata. To update the schema or the metadata file, select one of the following options:

### bq

1.  Create a table definition file:
    
    ``` bash
    bq mkdef --source_format=ICEBERG \
    "URI" > TABLE_DEFINITION_FILE
    ```

2.  Use the [`  bq update  ` command](/bigquery/docs/reference/bq-cli-reference#bq_update) with the `  --autodetect_schema  ` flag:
    
    ``` bash
    bq update --autodetect_schema --external_table_definition=TABLE_DEFINITION_FILE
    PROJECT_ID:DATASET.TABLE
    ```
    
    Replace the following:
    
      - `  URI  ` : your Cloud Storage URI with the latest [JSON metadata file](https://iceberg.apache.org/spec/#table-metadata)
        
        For example, `  gs://mybucket/us/iceberg/mytable/metadata/1234.metadata.json  ` .
    
      - `  TABLE_DEFINITION_FILE  ` : the name of the file containing the table schema
    
      - `  PROJECT_ID  ` : the project ID containing the table that you want to update
    
      - `  DATASET  ` : the dataset containing the table that you want to update
    
      - `  TABLE  ` : the table that you want to update

### API

Use the [`  tables.patch  ` method](/bigquery/docs/reference/rest/v2/tables/patch) with the `  autodetect_schema  ` property set to `  true  ` :

``` text
PATCH https://bigquery.googleapis.com/bigquery/v2/projects/PROJECT_ID/datasets/DATASET/tables/TABLE?autodetect_schema=true
```

Replace the following:

  - `  PROJECT_ID  ` : the project ID that contains the table that you want to update
  - `  DATASET  ` : the dataset containing the table that you want to update
  - `  TABLE  ` : the table that you want to update

In the body of the request, specify the updated values for the following fields:

``` bash
{
     "externalDataConfiguration": {
      "sourceFormat": "ICEBERG",
      "sourceUris": [
        "URI"
      ]
    },
    "schema": null
  }'
```

Replace `  URI  ` with the latest Iceberg metadata file. For example, `  gs://mybucket/us/iceberg/mytable/metadata/1234.metadata.json  ` .

## Set up access control policies

You can control access to Iceberg external tables through [column-level security](/bigquery/docs/column-level-security) , [row-level security](/bigquery/docs/managing-row-level-security) , and [data masking](/bigquery/docs/column-data-masking) .

## Query Iceberg external tables

For more information, see [Query Iceberg data](/bigquery/docs/query-iceberg-data) .

### Query historical data

You can access snapshots of Iceberg external tables that are retained in your Iceberg metadata by using the [`  FOR SYSTEM_TIME AS OF  ` clause](/bigquery/docs/access-historical-data#query_data_at_a_point_in_time) .

[Time travel and fail-safe data retention windows](/bigquery/docs/time-travel) aren't supported for any external tables.

## Data mapping

BigQuery converts Iceberg data types to BigQuery data types as shown in the following table:

<table>
<thead>
<tr class="header">
<th><strong>Iceberg data type</strong></th>
<th><strong>BigQuery data type</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       boolean      </code></td>
<td><code dir="ltr" translate="no">       BOOL      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       int      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       long      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       float      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       double      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       Decimal(P/S)      </code></td>
<td><code dir="ltr" translate="no">       NUMERIC or BIG_NUMERIC depending on precision      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       date      </code></td>
<td><code dir="ltr" translate="no">       DATE      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       time      </code></td>
<td><code dir="ltr" translate="no">       TIME      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       timestamp      </code></td>
<td><code dir="ltr" translate="no">       DATETIME      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       timestamptz      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       string      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       uuid      </code></td>
<td><code dir="ltr" translate="no">       BYTES      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       fixed(L)      </code></td>
<td><code dir="ltr" translate="no">       BYTES      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       binary      </code></td>
<td><code dir="ltr" translate="no">       BYTES      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       list&lt;Type&gt;      </code></td>
<td><code dir="ltr" translate="no">       ARRAY&lt;Type&gt;      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       struct      </code></td>
<td><code dir="ltr" translate="no">       STRUCT      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       map&lt;KeyType, ValueType&gt;      </code></td>
<td><code dir="ltr" translate="no">       ARRAY&lt;Struct&lt;key KeyType, value ValueType&gt;&gt;      </code></td>
</tr>
</tbody>
</table>

## Limitations

In addition to [external table limitations](/bigquery/docs/biglake-intro#limitations) , Iceberg external tables have the following limitations:

  - Queries that use VPC Service Controls are unsupported and result in an error such as `  NO_MATCHING_ACCESS_LEVEL  ` .

  - Tables using merge-on-read have the following limitations:
    
      - Each data file can be associated with up to 10,000 delete files.
      - No more than 100,000 equality deletes can be applied to a data file.
      - You can work around these limitations by compacting delete files frequently, creating a view on top of the Iceberg table that avoids frequently mutated partitions, or using position deletes rather than equality deletes.

  - BigQuery supports manifest pruning using all [Iceberg partition transformation functions](https://iceberg.apache.org/spec/#partition-transforms) . For information about how to prune partitions, see [Query partitioned tables](/bigquery/docs/querying-partitioned-tables) . Queries referencing Iceberg external tables must contain literals in predicates compared to columns that are partitioned.

  - Only Apache Parquet data files are supported.

## Merge-on-read costs

On-demand billing for merge-on-read data is the sum of scans of the following data:

  - All logical bytes read in the data file (including rows that are marked as deleted by position and equality deletes).
  - Logical bytes read loading the equality delete and position deletes files to find the deleted rows in a data file.

## Require partition filter

You can require the use of predicate filters by enabling the *require partition filter* option for your Iceberg table. If you enable this option, attempts to query the table without specifying a `  WHERE  ` clause that aligns with each manifest file will produce the following error:

``` text
Cannot query over table project_id.dataset.table without a
filter that can be used for partition elimination.
```

Each manifest file requires at least one predicate suitable for partition elimination.

You can enable the `  require_partition_filter  ` in the following ways while creating an Iceberg table :

### SQL

Use the [`  CREATE EXTERNAL TABLE  ` statement](/bigquery/docs/reference/standard-sql/data-definition-language#create_external_table_statement) .The following example creates an Iceberg external table named `  TABLE  ` with require partition filter enabled:

``` googlesql
  CREATE EXTERNAL TABLE TABLE
  WITH CONNECTION `PROJECT_ID.REGION.CONNECTION_ID`
  OPTIONS (
         format = 'ICEBERG',
         uris = [URI],
         require_partition_filter = true
   )
```

Replace the following:

  - `  TABLE  ` : the table name that you want to create.

  - `  PROJECT_ID  ` : the project ID containing the table that you want to create.

  - `  REGION  ` : the [location](/bigquery/docs/locations) where you want to create the Iceberg table.

  - `  CONNECTION_ID  ` : the [connection ID](/bigquery/docs/working-with-connections#view-connections) . For example, `  myconnection  ` .

  - `  URI  ` : the Cloud Storage URI with the latest [JSON metadata file](https://iceberg.apache.org/spec/#table-metadata) .
    
    For example, `  gs://mybucket/us/iceberg/mytable/metadata/1234.metadata.json  ` .
    
    The URI can point to an external cloud location as well; such as Amazon S3 or Azure Blob Storage.
    
      - Example for AWS: `  s3://mybucket/iceberg/metadata/1234.metadata.json  ` .
      - Example for Azure: `  azure://mystorageaccount.blob.core.windows.net/mycontainer/iceberg/metadata/1234.metadata.json  ` .

### bq

Use the [`  bq mk --table  ` command](/bigquery/docs/reference/bq-cli-reference#mk-table) with the `  @connection  ` decorator to specify the connection to use at the end of the `  --external_table_definition  ` parameter. Use `  --require_partition_filter  ` to enable the require partition filter. The following example creates an Iceberg external table named `  TABLE  ` with require partition filter enabled:

``` text
bq mk \
    --table \
    --external_table_definition=ICEBERG=URI@projects/CONNECTION_PROJECT_ID/locations/CONNECTION_REGION/connections/CONNECTION_ID \
    PROJECT_ID:DATASET.EXTERNAL_TABLE \
    --require_partition_filter
```

Replace the following:

  - `  URI  ` : the latest [JSON metadata file](https://iceberg.apache.org/spec/#table-metadata) for a specific table snapshot
    
    For example, `  gs://mybucket/mydata/mytable/metadata/iceberg.metadata.json  ` .
    
    The URI can point to an external cloud location as well; such as Amazon S3 or Azure Blob Storage.
    
      - Example for AWS: `  s3://mybucket/iceberg/metadata/1234.metadata.json  ` .
      - Example for Azure: `  azure://mystorageaccount.blob.core.windows.net/mycontainer/iceberg/metadata/1234.metadata.json  ` .

  - `  CONNECTION_PROJECT_ID  ` : the project that contains the [connection](/bigquery/docs/connect-to-spark) to create the Iceberg external table—for example, `  myproject  `

  - `  CONNECTION_REGION  ` : the [region](/bigquery/docs/locations) that contains the connection to create the Iceberg external table. For example, `  us  ` .

  - `  CONNECTION_ID  ` : : the [connection ID](/bigquery/docs/working-with-connections#view-connections) . For example, `  myconnection  ` .
    
    When you [view the connection details](/bigquery/docs/working-with-connections#view-connections) in the Google Cloud console, the connection ID is the value in the last section of the fully qualified connection ID that is shown in **Connection ID** —for example `  projects/myproject/locations/connection_location/connections/ myconnection  `

  - `  DATASET  ` : the name of the BigQuery
    
    dataset that contains the table that you want to update. For example, `  mydataset  ` .

  - `  EXTERNAL_TABLE  ` : the name of the table that you want to create
    
    For example, `  mytable  ` .

You can also update your Iceberg table to enable the require partition filter.

If you don't enable the *require partition filter* option when you create the partitioned table, you can update the table to add the option.

### bq

Use the `  bq update  ` command and supply the `  --require_partition_filter  ` flag.

For example:

To update `  mypartitionedtable  ` in `  mydataset  ` in your default project, enter:

``` text
bq update --require_partition_filter PROJECT_ID:DATASET.TABLE
```

## What's next

  - Learn about [stored procedure for Spark](/bigquery/docs/spark-procedures) .
  - Learn about [access control policies](/bigquery/docs/access-control) .
  - Learn about [running queries in BigQuery](/bigquery/docs/running-queries) .
  - Learn about the [supported statements and SQL dialects in BigQuery](/bigquery/docs/introduction-sql) .
