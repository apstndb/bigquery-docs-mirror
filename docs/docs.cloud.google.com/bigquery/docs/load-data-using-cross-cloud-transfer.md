# Load data with cross-cloud operations

As a BigQuery administrator or analyst, you can load data from an Amazon Simple Storage Service (Amazon S3) bucket or Azure Blob Storage into [BigQuery tables](/bigquery/docs/tables-intro#standard-tables) . You can either join the transferred data with the data present in Google Cloud regions or take advantage of BigQuery features like [BigQuery ML](/bigquery/docs/bqml-introduction) . You can also create materialized view replicas of certain external sources to make that data available in BigQuery.

You can transfer data into BigQuery in the following ways:

  - Transfer data from files in Amazon S3 and Azure Blob Storage into BigQuery tables, by using the [`  LOAD DATA  ` statement](#load-data) .

  - Filter data from files in Amazon S3 or Blob Storage before transferring results into BigQuery tables, by using the [`  CREATE TABLE AS SELECT  ` statement](#filter-data) . To append data to the destination table, use the [`  INSERT INTO SELECT  ` statement](#filter-data) . Data manipulation is applied on the external tables that reference data from [Amazon S3](/bigquery/docs/omni-aws-create-external-table) or [Blob Storage](/bigquery/docs/omni-azure-create-external-table) .

  - Create [materialized view replicas](#materialized_view_replicas) of external Amazon S3, Apache Iceberg, or Salesforce Data Cloud data in a BigQuery dataset so that the data is available locally in BigQuery.

**Note:** If you want to transfer large files from Amazon Simple Storage Service (Amazon S3) bucket or Azure Blob Storage into BigQuery tables on a scheduled basis, use [BigQuery Data Transfer Service](/bigquery/docs/dts-introduction) . If you want to read and process data before transferring data into BigQuery tables, use the [`  CREATE TABLE AS SELECT  ` statement](#filter-data) .

## Quotas and limits

For information about quotas and limits, see [query jobs quotas and limits](/bigquery/quotas#query_jobs) .

## Before you begin

To provide Google Cloud with read access required to load or filter data in other clouds, ask your administrator to create a [connection](/bigquery/docs/connections-api-intro) and share it with you. For information about how to create connections, see [Connect to Amazon S3](/bigquery/docs/omni-aws-create-connection) or [Blob Storage](/bigquery/docs/omni-azure-create-connection) .

### Required role

To get the permissions that you need to load data using cross-cloud transfers, ask your administrator to grant you the [BigQuery Data Editor](/iam/docs/roles-permissions/bigquery#bigquery.dataEditor) ( `  roles/bigquery.dataEditor  ` ) IAM role on the dataset. For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

This predefined role contains the permissions required to load data using cross-cloud transfers. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

The following permissions are required to load data using cross-cloud transfers:

  - `  bigquery.tables.create  `
  - `  bigquery.tables.get  `
  - `  bigquery.tables.updateData  `
  - `  bigquery.tables.update  `
  - `  bigquery.jobs.create  `
  - `  bigquery.connections.use  `

You might also be able to get these permissions with [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

For more information about IAM roles in BigQuery, see [BigQuery IAM roles and permissions](/bigquery/docs/access-control) .

## Pricing

You are billed for the bytes that are transferred across clouds by using the [`  LOAD  ` statement](#load-data) . For pricing information, see the Omni Cross Cloud Data Transfer section in [BigQuery Omni pricing](https://cloud.google.com/bigquery/pricing#bqomni) .

You are billed for the bytes that are transferred across clouds by using the [`  CREATE TABLE AS SELECT  ` statement](#filter-data) or [`  INSERT INTO SELECT  ` statement](#filter-data) and for the [compute capacity](https://cloud.google.com/bigquery/pricing#capacity_compute_analysis_pricing) .

Both `  LOAD  ` and `  CREATE TABLE AS SELECT  ` statements require slots in the BigQuery Omni regions to scan Amazon S3 and Blob Storage files to load them. For more information, see [BigQuery Omni pricing](https://cloud.google.com/bigquery/pricing#bqomni) .

For materialized view replicas of external data sources, costs can also include [materialized views pricing](/bigquery/docs/materialized-views-intro#materialized_views_pricing) .

## Best practices for load and filter options

  - Avoid loading multiple files that are less than 5 MB. Instead, create an external table for your file and export query result to [Amazon S3](/bigquery/docs/omni-aws-create-external-table) or [Blob Storage](/bigquery/docs/omni-azure-create-external-table) to create a larger file. This method helps to improve the transfer time of your data.
  - If your source data is in a gzip-compressed file, then while creating external tables, set the [`  external_table_options.compression  `](/bigquery/docs/reference/standard-sql/data-definition-language#external_table_option_list) option to `  GZIP  ` .

## Load data

You can load data into BigQuery with the [`  LOAD DATA [INTO|OVERWRITE]  ` statement](/bigquery/docs/reference/standard-sql/load-statements) .

### Limitations

  - The connection and the destination dataset must belong to the same project. Loading data across projects is not supported.
  - `  LOAD DATA  ` is only supported when you transfer data from an Amazon Simple Storage Service (Amazon S3) or Azure Blob Storage to a colocated BigQuery region. For more information, see [Locations](/bigquery/docs/omni-introduction#locations) .
      - You can transfer data from any `  US  ` region to a `  US  ` multi-region. You can also transfer from any `  EU  ` region to a `  EU  ` multi-region.

### Example

#### Example 1

The following example loads a parquet file named `  sample.parquet  ` from an Amazon S3 bucket into the `  test_parquet  ` table with an auto-detect schema:

``` text
LOAD DATA INTO mydataset.testparquet
  FROM FILES (
    uris = ['s3://test-bucket/sample.parquet'],
    format = 'PARQUET'
  )
  WITH CONNECTION `aws-us-east-1.test-connection`
```

#### Example 2

The following example loads a CSV file with the prefix `  sampled*  ` from your Blob Storage into the `  test_csv  ` table with predefined column partitioning by time:

``` text
LOAD DATA INTO mydataset.test_csv (Number INT64, Name STRING, Time DATE)
  PARTITION BY Time
  FROM FILES (
    format = 'CSV', uris = ['azure://test.blob.core.windows.net/container/sampled*'],
    skip_leading_rows=1
  )
  WITH CONNECTION `azure-eastus2.test-connection`
```

#### Example 3

The following example overwrites the existing table `  test_parquet  ` with data from a file named `  sample.parquet  ` with an auto-detect schema:

``` text
LOAD DATA OVERWRITE mydataset.testparquet
  FROM FILES (
    uris = ['s3://test-bucket/sample.parquet'],
    format = 'PARQUET'
  )
  WITH CONNECTION `aws-us-east-1.test-connection`
```

## Filter data

You can filter data before transferring them into BigQuery by using the [`  CREATE TABLE AS SELECT  ` statement](/bigquery/docs/reference/standard-sql/data-definition-language?#create_table_statement) and the [`  INSERT INTO SELECT  ` statement](/bigquery/docs/reference/standard-sql/dml-syntax#insert_statement) .

### Limitations

  - If the result of the `  SELECT  ` query exceeds 60 GiB in logical bytes, the query fails. The table is not created and data is not transferred. To learn how to reduce the size of data that is scanned, see [Reduce data processed in queries](/bigquery/docs/best-practices-performance-communication) .

  - Temporary tables are not supported.

  - Transferring the [Well-known binary (WKB)](/bigquery/docs/geospatial-data) geospatial data format is not supported.

  - `  INSERT INTO SELECT  ` statement does not support transferring data into clustered table.

  - In the `  INSERT INTO SELECT  ` statement, if the destination table is the same as the source table in the `  SELECT  ` query, then the `  INSERT INTO SELECT  ` statement doesn't modify any rows in the destination table. The destination table isn't modified as BigQuery can't read data across regions.

  - `  CREATE TABLE AS SELECT  ` and `  INSERT INTO SELECT  ` are only supported when you transfer data from an Amazon S3 or Blob Storage to a colocated BigQuery region. For more information, see [Locations](/bigquery/docs/omni-introduction#locations) .
    
      - You can transfer data from any `  US  ` region to a `  US  ` multi-region. You can also transfer from any `  EU  ` region to a `  EU  ` multi-region.

### Example

#### Example 1

Suppose you have a BigLake table named `  myawsdataset.orders  ` that references data from [Amazon S3](/bigquery/docs/omni-aws-create-external-table) . You want to transfer data from that table to a BigQuery table `  myotherdataset.shipments  ` in the US multi-region.

First, display information about the `  myawsdataset.orders  ` table:

``` text
    bq show myawsdataset.orders;
```

The output is similar to the following:

``` text
  Last modified             Schema              Type     Total URIs   Expiration
----------------- -------------------------- ---------- ------------ -----------
  31 Oct 17:40:28   |- l_orderkey: integer     EXTERNAL   1
                    |- l_partkey: integer
                    |- l_suppkey: integer
                    |- l_linenumber: integer
                    |- l_returnflag: string
                    |- l_linestatus: string
                    |- l_commitdate: date
```

Next, display information about the `  myotherdataset.shipments  ` table:

``` text
  bq show myotherdataset.shipments
```

The output is similar to the following. Some columns are omitted to simplify the output.

``` text
  Last modified             Schema             Total Rows   Total Bytes   Expiration   Time Partitioning   Clustered Fields   Total Logical
 ----------------- --------------------------- ------------ ------------- ------------ ------------------- ------------------ ---------------
  31 Oct 17:34:31   |- l_orderkey: integer      3086653      210767042                                                         210767042
                    |- l_partkey: integer
                    |- l_suppkey: integer
                    |- l_commitdate: date
                    |- l_shipdate: date
                    |- l_receiptdate: date
                    |- l_shipinstruct: string
                    |- l_shipmode: string
```

Now, using the `  CREATE TABLE AS SELECT  ` statement you can selectively load data to the `  myotherdataset.orders  ` table in the US multi-region:

``` text
CREATE OR REPLACE TABLE
  myotherdataset.orders
  PARTITION BY DATE_TRUNC(l_commitdate, YEAR) AS
SELECT
  *
FROM
  myawsdataset.orders
WHERE
  EXTRACT(YEAR FROM l_commitdate) = 1992;
```

**Note:** If you get a `  ResourceExhausted  ` error, retry after sometime. If the issue persists, you can [contact support](/bigquery/docs/getting-support) .

You can then perform a join operation with the newly created table:

``` text
SELECT
  orders.l_orderkey,
  orders.l_orderkey,
  orders.l_suppkey,
  orders.l_commitdate,
  orders.l_returnflag,
  shipments.l_shipmode,
  shipments.l_shipinstruct
FROM
  myotherdataset.shipments
JOIN
  `myotherdataset.orders` as orders
ON
  orders.l_orderkey = shipments.l_orderkey
AND orders.l_partkey = shipments.l_partkey
AND orders.l_suppkey = shipments.l_suppkey
WHERE orders.l_returnflag = 'R'; -- 'R' means refunded.
```

When new data is available, append the data of the 1993 year to the destination table using the `  INSERT INTO SELECT  ` statement:

``` text
INSERT INTO
   myotherdataset.orders
 SELECT
   *
 FROM
   myawsdataset.orders
 WHERE
   EXTRACT(YEAR FROM l_commitdate) = 1993;
```

#### Example 2

The following example inserts data into an ingestion-time partitioned table:

``` text
CREATE TABLE
 mydataset.orders(id String, numeric_id INT64)
PARTITION BY _PARTITIONDATE;
```

After creating a partitioned table, you can insert data into the ingestion-time partitioned table:

``` text
INSERT INTO
 mydataset.orders(
   _PARTITIONTIME,
   id,
   numeric_id)
SELECT
 TIMESTAMP("2023-01-01"),
 id,
 numeric_id,
FROM
 mydataset.ordersof23
WHERE
 numeric_id > 4000000;
```

## Materialized view replicas

A materialized view replica is a replication of external Amazon Simple Storage Service (Amazon S3), Apache Iceberg, or Salesforce Data Cloud data in a BigQuery dataset so that the data is available locally in BigQuery. This can help you avoid data egress costs and improve query performance. BigQuery lets you [create materialized views on BigLake metadata cache-enabled tables](/bigquery/docs/omni-introduction#cache-enabled_tables_with_materialized_views) over Amazon Simple Storage Service (Amazon S3), Apache Iceberg, or Salesforce Data Cloud data.

A materialized view replica lets you use the Amazon S3, Iceberg, or Data Cloud materialized view data in queries while avoiding data egress costs and improving query performance. A materialized view replica does this by replicating the Amazon S3, Iceberg, or Data Cloud data to a dataset in a [supported BigQuery region](#supported_regions) , so that the data is available locally in BigQuery.

### Before you begin

1.  Ensure that you have the [required Identity and Access Management (IAM) permissions](#required_permissions) to perform the tasks in this section.

#### Required roles

To get the permissions that you need to perform the tasks in this section, ask your administrator to grant you the [BigQuery Admin](/iam/docs/roles-permissions/bigquery#bigquery.admin) ( `  roles/bigquery.admin  ` ) IAM role . For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

This predefined role contains the permissions required to perform the tasks in this section. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

The following permissions are required to perform the tasks in this section:

  - `  bigquery.tables.create  `
  - `  bigquery.tables.get  `
  - `  bigquery.tables.getData  `
  - `  bigquery.tables.replicateData  `
  - `  bigquery.jobs.create  `

You might also be able to get these permissions with [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

For more information about BigQuery IAM, see [BigQuery IAM roles and permissions](/bigquery/docs/access-control) .

### Prepare a dataset for materialized view replicas

Before creating a materialized view replica, you must complete the following tasks:

1.  [Create a dataset](/bigquery/docs/datasets) in a [region that supports Amazon S3](/bigquery/docs/omni-introduction#locations)
2.  Create a source table in the dataset you created in the preceding step. The source table can be any of the following table types:
      - An [Amazon S3 BigLake table](/bigquery/docs/omni-aws-create-external-table) that has [metadata caching](/bigquery/docs/metadata-caching) enabled and doesn't use an Iceberg file format.
      - An [Apache Iceberg external table](/bigquery/docs/iceberg-external-tables) .
      - A [Data Cloud table](/bigquery/docs/salesforce-quickstart) .

### Create materialized view replicas

Select one of the following options:

### Console

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :
    
    If you don't see the left pane, click last\_page **Expand left pane** to open the pane.

3.  In the **Explorer** pane, navigate to the project and dataset where you want to create the materialized view replica, and then click more\_vert **Actions \> Create table** .

4.  In the **Source** section of the **Create table** dialog, do the following:
    
    1.  For **Create table from** , select **Existing table/view** .
    2.  For **Project** , enter the project where the source table or view is located.
    3.  For **Dataset** , enter the dataset where the source table or view is located.
    4.  For **View** , enter the source table or view that you are replicating. If you choose a view, it must be an [authorized view](/bigquery/docs/authorized-views) , or if not, all tables that are used to generate that view must be located in the view's dataset.

5.  Optional: For **Local materialized view max staleness** , enter a [`  max_staleness  ` value](/bigquery/docs/materialized-views-create#max_staleness) for your local materialized view.

6.  In the **Destination** section of the **Create table** dialog, do the following:
    
    1.  For **Project** , enter the project in which you want to create the materialized view replica.
    2.  For **Dataset** , enter the dataset in which you want to create the materialized view replica.
    3.  For **Replica materialized view name** , enter a name for your replica.

7.  Optional: Specify **tags** and **advanced options** for your materialized view replica. If you don't specify a dataset for **Local Materialized View Dataset** , then one is automatically created in the same project and region as the source data and named `  bq_auto_generated_local_mv_dataset  ` . If you don't specify a name for **Local Materialized View Name** , then one is automatically created in the same project and region as the source data and given the prefix `  bq_auto_generated_local_mv_  ` .

8.  Click **Create table** .

A new local materialized view is created (if it wasn't specified) and authorized in the source dataset. Then the materialized view replica is created in the destination dataset.

### SQL

1.  [Create a materialized view](/bigquery/docs/materialized-views-create) over the base table in the dataset that you created. You can also create the materialized view in a different dataset that is in an Amazon S3 region.

2.  [Authorize the materialized view](/bigquery/docs/authorized-views) on the datasets that contain the source tables used in the query that created the materialized view.

3.  If you configured manual metadata cache refreshing for the source table, run the [`  BQ.REFRESH_EXTERNAL_METADATA_CACHE  ` system procedure](/bigquery/docs/reference/system-procedures#bqrefresh_external_metadata_cache) to refresh the metadata cache.

4.  Run the [`  BQ.REFRESH_MATERIALIZED_VIEW  ` system procedure](/bigquery/docs/reference/system-procedures#bqrefresh_materialized_view) to refresh the materialized view.

5.  Create materialized view replicas by using the [`  CREATE MATERIALIZED VIEW AS REPLICA OF  ` statement](/bigquery/docs/reference/standard-sql/data-definition-language#create_materialized_view_as_replica_of_statement) :
    
    ``` text
    CREATE MATERIALIZED VIEW PROJECT_ID.BQ_DATASET.REPLICA_NAME
    OPTIONS(replication_interval_seconds=REPLICATION_INTERVAL)
    AS REPLICA OF PROJECT_ID.S3_DATASET.MATERIALIZED_VIEW_NAME;
    ```
    
    Replace the following:
    
      - `  PROJECT_ID  ` : the name of your project in which you want to create the materialized view replica—for example, `  myproject  ` .
      - `  BQ_DATASET  ` : the name of the BigQuery dataset that you want to create the materialized view replica in—for example, `  bq_dataset  ` . The dataset must be in the BigQuery [region](/bigquery/docs/omni-introduction#locations) that maps to the region of the source materialized view.
      - `  REPLICA_NAME  ` : the name of the materialized view replica that you want to create—for example, `  my_mv_replica  ` .
      - `  REPLICATION_INTERVAL  ` : specifies how often to replicate the data from the source materialized view to the replica, in seconds. Must be a value between 60 and 3,600, inclusive. Defaults to 300 (5 minutes).
      - `  S3_DATASET  ` : the name of the dataset that contains the source materialized view—for example, `  s3_dataset  ` .
      - `  MATERIALIZED_VIEW_NAME  ` : the name of the materialized view to replicate—for example, `  my_mv  ` .
    
    The following example creates a materialized view replica named `  mv_replica  ` in `  bq_dataset  ` :
    
    ``` text
    CREATE MATERIALIZED VIEW `myproject.bq_dataset.mv_replica`
    OPTIONS(
    replication_interval_seconds=600
    )
    AS REPLICA OF `myproject.s3_dataset.my_s3_mv`
    ```

After you create the materialized view replica, the replication process polls the source materialized view for changes and replicates data to the materialized view replica, refreshing the data at the interval you specified in the `  replication_interval_seconds  ` or `  max_staleness  ` option. If you query the replica before the first backfill completes, you get a `  backfill in progress  ` error. You can query the data in the materialized view replica after the first replication completes.

### Data freshness

After you create the materialized view replica, the replication process polls the source materialized view for changes and replicates data to the materialized view replica. The data is replicated at the interval you specified in the `  replication_interval_seconds  ` option of the [`  CREATE MATERIALIZED VIEW AS REPLICA OF  ` statement](/bigquery/docs/reference/standard-sql/data-definition-language#create_materialized_view_as_replica_of_statement) .

In addition to the replication interval, the freshness of the materialized view replica data is also affected by how often the source materialized view refreshes, and how often the metadata cache of the Amazon S3, Iceberg, or Data Cloud table used by the materialized view refreshes.

You can check the data freshness for the materialized view replica and the resources it is based on by using the Google Cloud console:

  - For materialized view replica freshness, look at the **Last modified** field in the materialized view replica's **Details** pane.
  - For source materialized view freshness, look at the **Last modified** field in the materialized view's **Details** pane.
  - For source Amazon S3, Iceberg, or Data Cloud table metadata cache freshness, look at the **Max staleness** field in the materialized view's **Details** pane.

### Supported materialized view replica regions

Use the location mappings in the following table when creating materialized view replicas:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Location of the source materialized view</strong></th>
<th><strong>Location of the materialized view replica</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       aws-us-east-1      </code></td>
<td>The <code dir="ltr" translate="no">       US      </code> <a href="/bigquery/docs/locations#multi-regions">multi-region</a> , or any of the following <a href="/bigquery/docs/locations#regions">regions</a> :
<ul>
<li><code dir="ltr" translate="no">         northamerica-northeast1        </code></li>
<li><code dir="ltr" translate="no">         northamerica-northeast2        </code></li>
<li><code dir="ltr" translate="no">         us-central1        </code></li>
<li><code dir="ltr" translate="no">         us-east1        </code></li>
<li><code dir="ltr" translate="no">         us-east4        </code></li>
<li><code dir="ltr" translate="no">         us-east5        </code></li>
<li><code dir="ltr" translate="no">         us-south1        </code></li>
<li><code dir="ltr" translate="no">         us-west1        </code></li>
<li><code dir="ltr" translate="no">         us-west2        </code></li>
<li><code dir="ltr" translate="no">         us-west3        </code></li>
<li><code dir="ltr" translate="no">         us-west4        </code></li>
</ul></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       aws-us-west-2      </code></td>
<td>The <code dir="ltr" translate="no">       US      </code> <a href="/bigquery/docs/locations#multi-regions">multi-region</a> , or any of the following <a href="/bigquery/docs/locations#regions">regions</a> :
<ul>
<li><code dir="ltr" translate="no">         northamerica-northeast1        </code></li>
<li><code dir="ltr" translate="no">         northamerica-northeast2        </code></li>
<li><code dir="ltr" translate="no">         us-central1        </code></li>
<li><code dir="ltr" translate="no">         us-east1        </code></li>
<li><code dir="ltr" translate="no">         us-east4        </code></li>
<li><code dir="ltr" translate="no">         us-east5        </code></li>
<li><code dir="ltr" translate="no">         us-south1        </code></li>
<li><code dir="ltr" translate="no">         us-west1        </code></li>
<li><code dir="ltr" translate="no">         us-west2        </code></li>
<li><code dir="ltr" translate="no">         us-west3        </code></li>
<li><code dir="ltr" translate="no">         us-west4        </code></li>
</ul></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       aws-eu-west-1      </code></td>
<td>The <code dir="ltr" translate="no">       EU      </code> <a href="/bigquery/docs/locations#multi-regions">multi-region</a> , or any of the following <a href="/bigquery/docs/locations#regions">regions</a> :
<ul>
<li><code dir="ltr" translate="no">         europe-central2        </code></li>
<li><code dir="ltr" translate="no">         europe-north1        </code></li>
<li><code dir="ltr" translate="no">         europe-southwest1        </code></li>
<li><code dir="ltr" translate="no">         europe-west1        </code></li>
<li><code dir="ltr" translate="no">         europe-west2        </code></li>
<li><code dir="ltr" translate="no">         europe-west3        </code></li>
<li><code dir="ltr" translate="no">         europe-west4        </code></li>
<li><code dir="ltr" translate="no">         europe-west6        </code></li>
<li><code dir="ltr" translate="no">         europe-west8        </code></li>
<li><code dir="ltr" translate="no">         europe-west9        </code></li>
<li><code dir="ltr" translate="no">         europe-west10        </code></li>
</ul></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       aws-ap-northeast-2      </code></td>
<td>Any of the following <a href="/bigquery/docs/locations#regions">regions</a> :
<ul>
<li><code dir="ltr" translate="no">         asia-east1        </code></li>
<li><code dir="ltr" translate="no">         asia-east2        </code></li>
<li><code dir="ltr" translate="no">         asia-northeast1        </code></li>
<li><code dir="ltr" translate="no">         asia-northeast2        </code></li>
<li><code dir="ltr" translate="no">         asia-northeast3        </code></li>
<li><code dir="ltr" translate="no">         asia-south1        </code></li>
<li><code dir="ltr" translate="no">         asia-south2        </code></li>
<li><code dir="ltr" translate="no">         asia-southeast1        </code></li>
</ul></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       aws-ap-southeast-2      </code></td>
<td>Any of the following <a href="/bigquery/docs/locations#regions">regions</a> :
<ul>
<li><code dir="ltr" translate="no">         australia-southeast1        </code></li>
<li><code dir="ltr" translate="no">         australia-southeast2        </code></li>
</ul></td>
</tr>
</tbody>
</table>

### Limitations of materialized view replicas

  - You can't create materialized view replicas for materialized views that are based on any tables that use [row-level security](/bigquery/docs/row-level-security-intro) or [column-level security](/bigquery/docs/column-level-security-intro) .
  - You can't use [customer-managed encryption keys (CMEKs)](/bigquery/docs/customer-managed-encryption) with either the source materialized view or the materialized view replica.
  - You can only create materialized view replicas for materialized views that are based on any tables that use [metadata caching](/bigquery/docs/metadata-caching) .
  - You can create only one materialized view replica for a given source materialized view.
  - You can only create materialized view replicas for [authorized materialized views](/bigquery/docs/authorized-views) .

### Materialized view replica pricing

Use of materialized view replicas incurs compute, outbound data transfer, and storage costs.

## What's next

  - Learn about [BigQuery ML](/bigquery/docs/bqml-introduction) .
  - Learn about [BigQuery Omni](/bigquery/docs/omni-introduction) .
  - Learn how to [run queries](/bigquery/docs/running-queries) .
  - Learn how to [set up VPC Service Controls for BigQuery Omni](/bigquery/docs/omni-vpc-sc) .
  - Learn how to schedule and manage recurring load jobs from [Amazon S3 into BigQuery](/bigquery/docs/s3-transfer-intro) and [Blob Storage into BigQuery](/bigquery/docs/blob-storage-transfer-intro) .
