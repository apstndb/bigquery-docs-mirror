# Export data to Spanner (reverse ETL)

This document describes how you can set up a reverse extract, transform, and load (reverse ETL) workflow from BigQuery to Spanner. You can do this by using the [`  EXPORT DATA  ` statement](/bigquery/docs/reference/standard-sql/export-statements) to export data from BigQuery data sources, including [Iceberg tables](/bigquery/docs/iceberg-tables) , to a [Spanner](/spanner/docs/overview) table.

This reverse ETL workflow combines analytic capabilities in BigQuery with low latency and high throughput in Spanner. This workflow lets you serve data to application users without exhausting quotas and limits on BigQuery.

## Before you begin

  - Create a [Spanner database](/spanner/docs/create-manage-databases) including a table to receive the exported data.

  - Grant [Identity and Access Management (IAM) roles](#required_roles) that give users the necessary permissions to perform each task in this document.

  - Create an [Enterprise or a higher tier reservation](/bigquery/docs/reservations-tasks#create_reservations) . You might reduce BigQuery compute costs when you run one-time exports to Spanner by setting a baseline slot capacity of zero and enabling [autoscaling](/bigquery/docs/slots-autoscaling-intro) .

### Required roles

To get the permissions that you need to export BigQuery data to Spanner, ask your administrator to grant you the following IAM roles on your project:

  - Export data from a BigQuery table: [BigQuery Data Viewer](/iam/docs/roles-permissions/bigquery#bigquery.dataViewer) ( `  roles/bigquery.dataViewer  ` )
  - Run an extract job: [BigQuery User](/iam/docs/roles-permissions/bigquery#bigquery.user) ( `  roles/bigquery.user  ` )
  - Check parameters of the Spanner instance: [Cloud Spanner Viewer](/iam/docs/roles-permissions/spanner#spanner.viewer) ( `  roles/spanner.viewer  ` )
  - Write data to a Spanner table: [Cloud Spanner Database User](/iam/docs/roles-permissions/spanner#spanner.databaseUser) ( `  roles/spanner.databaseUser  ` )

For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

## Limitations

  - This feature is not supported in Assured Workloads.

  - The following BigQuery data types don't have equivalents in Spanner and are not supported:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Spanner database dialect</th>
<th>Unsupported BigQuery types</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>All dialects</td>
<td><ul>
<li><code dir="ltr" translate="no">         STRUCT        </code></li>
<li><code dir="ltr" translate="no">         GEOGRAPHY        </code></li>
<li><code dir="ltr" translate="no">         DATETIME        </code></li>
<li><code dir="ltr" translate="no">         RANGE        </code></li>
<li><code dir="ltr" translate="no">         TIME        </code></li>
</ul></td>
</tr>
<tr class="even">
<td>GoogleSQL</td>
<td><ul>
<li><code dir="ltr" translate="no">         BIGNUMERIC        </code> : The supported <code dir="ltr" translate="no">         NUMERIC        </code> type is not wide enough. Consider adding explicit casts to the <code dir="ltr" translate="no">         NUMERIC        </code> type in the query.</li>
</ul></td>
</tr>
</tbody>
</table>

  - The maximum size of an exported row cannot exceed 1 MiB.

  - Spanner enforces referential integrity during the export. If the target table is a child of another table (INTERLEAVE IN PARENT), or if the target table has foreign key constraints, the foreign keys and parent key will be validated during the export. If an exported row is is written to a table with INTERLEAVE IN PARENT and the parent row doesn't exist, the export will fail with "Parent row is missing. Row cannot be written" error. If the exported row is written to a table with foreign key constraints and is referencing a key that doesn't exist, the export will fail with "Foreign key constraint is violated" error. When exporting to multiple tables, we recommend sequencing the export to ensure that referential integrity will be maintained through the export. This usually means exporting parent tables and tables that are referenced by foreign keys before tables that reference them.
    
    If the table that is the target of the export has foreign key constraints, or is a child of another table (INTERLEAVE IN PARENT), the parent table must be populated before a child table export, and should contain all the corresponding keys. An attempt to export a child table while a parent table does not have the complete set of relevant keys will fail.

  - A BigQuery job, such as an extract job to Spanner, has a maximum duration of 6 hours. For information about optimizing large extract jobs, see [Export optimization](#export_optimization) . Alternatively, consider splitting the input into individual blocks of data, which may be exported as individual extract jobs.

  - Exports to Spanner are only supported for the BigQuery Enterprise or Enterprise Plus editions. The BigQuery Standard edition and on-demand compute are not supported.

  - You cannot use continuous queries to export to Spanner tables with [auto-generated primary keys](/spanner/docs/primary-key-default-value) .

  - You cannot use continuous queries to export to Spanner tables in a PostgreSQL-dialect database.

  - When using continuous queries to export to a Spanner table, ensure that you choose a primary key that doesn't correspond to a monotonically increasing integer in your BigQuery table. Doing so might cause performance issues in your export. For information about primary keys in Spanner, and ways to mitigate these performance issues, see [Choose a primary key](/spanner/docs/schema-and-data-model#choose_a_primary_key) .

## Configure exports with `     spanner_options    ` option

You can use the `  spanner_options  ` option to specify a destination Spanner database and table. The configuration is expressed in the form of a JSON string, as the following example shows:

``` text
EXPORT DATA OPTIONS(
   uri="https://spanner.googleapis.com/projects/PROJECT_ID/instances/INSTANCE_ID/databases/DATABASE_ID",
  format='CLOUD_SPANNER',
   spanner_options = """{
      "table": "TABLE_NAME",
      "change_timestamp_column": "CHANGE_TIMESTAMP",
      "priority": "PRIORITY",
      "tag": "TAG",
   }"""
)
```

Replace the following:

  - `  PROJECT_ID  ` : the name of your Google Cloud project.
  - `  INSTANCE_ID  ` : the name of your database instance.
  - `  DATABASE_ID  ` : the name of your database.
  - `  TABLE_NAME  ` : the name of an existing destination table.
  - `  CHANGE_TIMESTAMP  ` : the name of the `  TIMESTAMP  ` type column in the destination Spanner table. This option is used during export to track the timestamp of the most recent row update. When this option is specified, the export first performs a read of the row in the Spanner table, to ensure that only the latest row update is written. We recommend specifying a `  TIMESTAMP  ` type column when you run a [continuous export](#export_continuously) , where the ordering of changes to rows with the same primary key is important.
  - `  PRIORITY  ` (optional): [priority](/spanner/docs/reference/rest/v1/RequestOptions#priority) of the write requests. Allowed values: `  LOW  ` , `  MEDIUM  ` , `  HIGH  ` . Default value: `  MEDIUM  ` .
  - `  TAG  ` (optional): [request tag](/spanner/docs/introspection/troubleshooting-with-tags) to help identify exporter traffic in Spanner monitoring. Default value: `  bq_export  ` .

## Export query requirements

To export query results to Spanner, the results must meet the following requirements:

  - All columns in the result set must exist in the destination table, and their types must match or be [convertible](#type_conversions) .
  - The result set must contain all `  NOT NULL  ` columns for the destination table.
  - Column values must not exceed Spanner [data size limits within tables](/spanner/quotas#tables) .
  - Any unsupported column types must be converted to one of the supported types before exporting to Spanner.

### Type conversions

For ease of use, Spanner exporter automatically applies the following type conversions:

<table>
<thead>
<tr class="header">
<th>BigQuery type</th>
<th>Spanner type</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>BIGNUMERIC</td>
<td>NUMERIC (PostgreSQL dialect only)</td>
</tr>
<tr class="even">
<td>FLOAT64</td>
<td>FLOAT32</td>
</tr>
<tr class="odd">
<td>BYTES</td>
<td>PROTO</td>
</tr>
<tr class="even">
<td>INT64</td>
<td>ENUM</td>
</tr>
</tbody>
</table>

## Export data

You can use the [`  EXPORT DATA  ` statement](/bigquery/docs/reference/standard-sql/export-statements) to export data from a BigQuery table into a Spanner table.

The following example exports selected fields from a table that's named `  mydataset.table1  ` :

``` text
EXPORT DATA OPTIONS (
  uri="https://spanner.googleapis.com/projects/PROJECT_ID/instances/INSTANCE_ID/databases/DATABASE_ID",
  format='CLOUD_SPANNER',
  spanner_options="""{ "table": "TABLE_NAME" }"""
)
AS SELECT * FROM mydataset.table1;
```

Replace the following:

  - `  PROJECT_ID  ` : the name of your Google Cloud project
  - `  INSTANCE_ID  ` : the name of your database instance
  - `  DATABASE_ID  ` : the name of your database
  - `  TABLE_NAME  ` : the name of an existing destination table

## Export multiple results with the same `     rowkey    ` value

When you export a result containing multiple rows with the same `  rowkey  ` value, values written to Spanner end up in the same Spanner row. Only single matching BigQuery row (there is no guarantee which one) will be present in the Spanner row set produced by export.

## Export continuously

**Preview**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

To continuously process an export query, see [Create continuous queries](/bigquery/docs/continuous-queries) for instructions and [example code](/bigquery/docs/continuous-queries#spanner-example) .

## Export optimization

To optimize the export of records from BigQuery to Spanner, you can try the following:

  - [Increase the number of nodes in the Spanner destination instance](/spanner/docs/compute-capacity) . During the early stages of the export, increasing the number of nodes in the instance might not immediately increase export throughput. A slight delay can occur while Spanner performs [load-based splitting](/spanner/docs/schema-and-data-model#load-based_splitting) . With load-based splitting, the export throughput grows and stabilizes. Using the `  EXPORT DATA  ` statement batches data to optimize writes to Spanner. For more information, see [Performance overview](/spanner/docs/performance) .

  - Specify `  HIGH  ` priority within [`  spanner_options  `](#spanner_options) . If your Spanner instance has [autoscaling](/spanner/docs/autoscaling-overview) enabled, setting `  HIGH  ` priority helps ensure that CPU utilization reaches the necessary threshold to trigger scaling. This allows the autoscaler to add compute resources in response to the export load, which can improve overall export throughput.
    
    **Caution:** using `  HIGH  ` priority can cause significant performance degradation for other workloads served by the same Spanner instance. Consider using `  HIGH  ` priority only if the Spanner instance is dedicated to this export, or if other workloads are not sensitive to performance impacts.
    
    The following example shows a Spanner export command set to `  HIGH  ` priority:
    
    ``` text
    EXPORT DATA OPTIONS (
      uri="https://spanner.googleapis.com/projects/PROJECT_ID/instances/INSTANCE_ID/databases/DATABASE_ID",
      format='CLOUD_SPANNER',
      spanner_options="""{ "table": "TABLE_NAME", "priority": "HIGH" }"""
    )
    ```

  - Avoid ordering the query results. If the result set contains all primary key columns, the exporter automatically sorts the primary keys of the destination table to streamline writes and minimize contention.
    
    If the destination table's primary key includes generated columns, add the generated columns' expressions to the query to ensure that the exported data is sorted and batched properly.
    
    For example, in the following Spanner schema, `  SaleYear  ` and `  SaleMonth  ` are generated columns that make up the beginning of the Spanner primary key:
    
    ``` text
    CREATE TABLE Sales (
      SaleId STRING(36) NOT NULL,
      ProductId INT64 NOT NULL,
      SaleTimestamp TIMESTAMP NOT NULL,
      Amount FLOAT64,
      -- Generated columns
      SaleYear INT64 AS (EXTRACT(YEAR FROM SaleTimestamp)) STORED,
      SaleMonth INT64 AS (EXTRACT(MONTH FROM SaleTimestamp)) STORED,
    ) PRIMARY KEY (SaleYear, SaleMonth, SaleId);
    ```
    
    When you export data from BigQuery to a Spanner table with generated columns used in the primary key, it is recommended, but not required, to include the expressions for these generated columns in your `  EXPORT DATA  ` query. This lets BigQuery pre-sort the data correctly, which is critical for efficient batching and writing to Spanner. The values for the generated columns in the `  EXPORT DATA  ` statement aren't committed in Spanner, because they are auto-generated by Spanner, but they are used to optimize the export.
    
    The following example exports data to a Spanner `  Sales  ` table whose primary key uses generated columns. To optimize write performance, the query includes `  EXTRACT  ` expressions that match the generated `  SaleYear  ` and `  SaleMonth  ` columns, letting BigQuery pre-sort the data before export:
    
    ``` text
    EXPORT DATA OPTIONS (
      uri="https://spanner.googleapis.com/projects/PROJECT_ID/instances/INSTANCE_ID/databases/DATABASE_ID",
      format='CLOUD_SPANNER',
      spanner_options="""{ "table": "Sales" }"""
    )
    AS SELECT
      s.SaleId,
      s.ProductId,
      s.SaleTimestamp,
      s.Amount,
      -- Add expressions that match the generated columns in the Spanner PK
      EXTRACT(YEAR FROM s.SaleTimestamp) AS SaleYear,
      EXTRACT(MONTH FROM s.SaleTimestamp) AS SaleMonth
    FROM my_dataset.sales_export AS s;
    ```

  - To prevent long running jobs, export data by partition. Shard your BigQuery data using a partition key, such as a timestamp in your query:
    
    ``` text
    EXPORT DATA OPTIONS (
      uri="https://spanner.googleapis.com/projects/PROJECT_ID/instances/INSTANCE_ID/databases/DATABASE_ID",
      format='CLOUD_SPANNER',
      spanner_options="""{ "table": "TABLE_NAME", "priority": "MEDIUM" }"""
    )
    AS SELECT *
    FROM 'mydataset.table1' d
    WHERE
    d.timestamp >= TIMESTAMP '2025-08-28T00:00:00Z' AND
    d.timestamp < TIMESTAMP '2025-08-29T00:00:00Z';
    ```
    
    This lets the query complete within the 6-hour job runtime. For more information about these limits, see the [query job limits](/bigquery/quotas#query_jobs) .

  - To improve data loading performance, drop the index in the Spanner table where data is imported. Then, recreate it after the import completes.

  - We recommend starting with one Spanner node (1000 processor units) and a minimal BigQuery slot reservation. For example, 100 slots, or 0 baseline slots with autoscaling. For exports under 100 GB, this configuration typically completes within the 6-hour job limit. For exports larger than 100 GB, increase throughput by scaling up Spanner nodes and BigQuery slot reservations, as needed. Throughput scales at approximately 5 MiB/s per node.

## Pricing

When you export data to Spanner using the `  EXPORT DATA  ` statement, you are billed using [BigQuery capacity compute pricing](https://cloud.google.com/bigquery/pricing#capacity_compute_analysis_pricing) .

To export continuously to Spanner using a continuous query, you must have a [BigQuery Enterprise or Enterprise Plus edition](/bigquery/docs/editions-intro) slot reservation and a [reservation assignment](/bigquery/docs/reservations-workload-management#assignments) that uses the `  CONTINUOUS  ` job type.

BigQuery exports to Spanner that cross regional boundaries are charged using data extraction rates. For more information, see [BigQuery pricing](https://cloud.google.com/bigquery/pricing#data_extraction_pricing) . To avoid data transfer charges, make sure that your BigQuery export runs in the same region as the Spanner [default leader](/spanner/docs/instance-configurations#configure-leader-region) . Continuous query exports don't support exports that cross regional boundaries.

After the data is exported, you're charged for storing the data in Spanner. For more information, see [Spanner pricing](https://cloud.google.com/spanner/pricing#storage) .
