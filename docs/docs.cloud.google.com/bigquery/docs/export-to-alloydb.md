---
name: documents/docs.cloud.google.com/bigquery/docs/export-to-alloydb
uri: https://docs.cloud.google.com/bigquery/docs/export-to-alloydb
title: Export data to AlloyDB (reverse ETL)
description: Prepare and configure a data export from BigQuery to AlloyDB for PostgreSQL.
data_source: docs.cloud.google.com
---

# Export data to AlloyDB (reverse ETL)

A reverse extract, transform, and load (reverse ETL) workflow from BigQuery to AlloyDB for PostgreSQL lets you move data from BigQuery into an AlloyDB database. You can use the [`EXPORT DATA` statement](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/export-statements) to process or filter the data with a query before you export it, or you can [sync your BigQuery table to AlloyDB](https://docs.cloud.google.com/bigquery/docs/export-to-alloydb#sync_a_table_for_export) to copy or mirror the full table.

## Before you begin

- Create an [AlloyDB cluster and instance](https://docs.cloud.google.com/alloydb/docs/cluster-create) , which includes a database, schema, and table, to receive the exported data. You must have the target schema and table before you run the export job. For `UPSERT` mode, the destination table must have a `PRIMARY KEY` or at least one `UNIQUE` constraint.

- The target AlloyDB instance must be a `PRIMARY` instance in `READY` state.

- [Create a BigQuery connection](https://docs.cloud.google.com/bigquery/docs/connect-to-alloydb) to connect to your AlloyDB instance. The connection must use username and password authentication. The database user requires the following privileges:

  | Table type                                         | Destination table privileges   | Destination schema privileges | Database privileges     | Notes                                                                              |
  |----------------------------------------------------|--------------------------------|-------------------------------|-------------------------|------------------------------------------------------------------------------------|
  | Tables with a `PRIMARY KEY` or `UNIQUE` constraint | `INSERT` , `UPDATE` , `SELECT` | `USAGE`                       | `CONNECT` , `TEMPORARY` | Required for both `UPSERT` and `APPEND` modes to support automatic retry fallback. |
  | Tables without constraints                         | `INSERT`                       | `USAGE`                       | `CONNECT`               |                                                                                    |

- To use this feature, you must create a [BigQuery Enterprise or Enterprise Plus tier reservation](https://docs.cloud.google.com/bigquery/docs/reservations-tasks#create_reservations) . Exports to AlloyDB are only supported for reservations with a [`QUERY` assignment](https://docs.cloud.google.com/bigquery/docs/reservations-assignments) .

- Grant [Identity and Access Management (IAM) roles](https://docs.cloud.google.com/bigquery/docs/export-to-alloydb#required_roles) that give users the necessary permissions to perform each task in this document.

### Required roles

To get the permissions that you need to export BigQuery data to AlloyDB, ask your administrator to grant you the following IAM roles on your project:

- Export data from a BigQuery table: [BigQuery Data Viewer](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataViewer) ( `roles/bigquery.dataViewer` )
- Run an extract job: [BigQuery User](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.user) ( `roles/bigquery.user` )
- Use a BigQuery connection: [BigQuery Connection User](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.connectionUser) ( `roles/bigquery.connectionUser` )
- Connect to an AlloyDB instance: AlloyDB Client ( `roles/alloydb.client` ) - the connection service account

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## Limitations

- AlloyDB exports only support batch exports. You can't use continuous queries to export to AlloyDB.

- To use `UPSERT` mode, the destination AlloyDB table must have a `PRIMARY KEY` or at least one `UNIQUE` constraint, and your `SELECT` query must project all columns that belong to that constraint. You can only export tables without a primary key or unique constraint using `APPEND` mode.

- Exporting data in `UPSERT` mode has lower write throughput and higher CPU and I/O overhead on the AlloyDB instance than `APPEND` mode. While `APPEND` mode streams rows directly using PostgreSQL's bulk `COPY` command, `UPSERT` mode performs an insert-or-update ( `INSERT ... ON CONFLICT DO UPDATE` ) operation, which requires AlloyDB to check unique indexes for existing keys and update matching rows. When you export only new records, use `APPEND` mode for optimal performance.

- If the destination table has no constraints defined, running multiple `APPEND` exports with the same data results in duplicate rows.

- We don't recommend running multiple concurrent `EXPORT DATA` jobs to the same AlloyDB table. Doing so can result in unpredictable behavior, like data loss or job failures. We recommend verifying that only one export job writes to a specific table at a time.

- Only username and password authentication through a BigQuery connection is supported.

- `ARRAY` , `BYTES` , `GEOGRAPHY` , `INTERVAL` , and `STRUCT` BigQuery data types are not supported.

- If the BigQuery `SELECT` statement omits columns that exist in the target AlloyDB table, those columns must either allow `NULL` values or have default values defined in AlloyDB. If they have a `NOT NULL` constraint and no default value, the export will fail.

- Exports to AlloyDB are only supported for the BigQuery Enterprise or Enterprise Plus editions. The BigQuery Standard edition and on-demand compute are not supported. For more information, see [Administration features](https://docs.cloud.google.com/bigquery/docs/editions-intro#administration_features) .

- A BigQuery job, such as an extract job to AlloyDB, has a maximum duration of 6 hours. For very large exports, we recommend breaking down the export into multiple smaller jobs.

## Location considerations

Exporting data to AlloyDB has specific requirements regarding the location of your BigQuery dataset and your AlloyDB instance:

- **Same-region exports:** The target AlloyDB instance must reside in the exact same Google Cloud region as the BigQuery dataset. For example, a dataset in `us-east1` can only be exported to an AlloyDB instance in `us-east1` .

- **Multi-region exports:**

  - Datasets in the `US` multi-region can only be exported to an AlloyDB instance located in the `us-central1` region.
  - Datasets in the `EU` multi-region can only be exported to an AlloyDB instance located in the `europe-west4` region.

Cross-region exports other than the previously mentioned combinations aren't supported.

## Configure exports with `alloydb_options`

You can use the `alloydb_options` option in the [`EXPORT DATA` statement](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/export-statements) to specify the destination AlloyDB schema, table, write mode, and maximum connections. The configuration is expressed as a JSON string. Only the `table` parameter is required. All other parameters are optional.

When configuring the export, the columns in the `SELECT` statement must have aliases that match the names of the columns in the target AlloyDB table.

```
EXPORT DATA
  WITH CONNECTION `PROJECT_ID.LOCATION.CONNECTION_ID`
  OPTIONS(
    format='ALLOYDB',
    uri="https://alloydb.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/clusters/CLUSTER_ID/instances/INSTANCE_ID",
    alloydb_options="""{
      "schema": "SCHEMA_NAME",
      "table": "TABLE_NAME",
      "write_mode": "WRITE_MODE",
      "max_parallel_connections": MAX_CONNECTIONS
    }"""
  )
AS SELECT * FROM `mydataset.table1`;
```

Replace the following:

- `PROJECT_ID` : the name of your Google Cloud project.
- `LOCATION` : the location of your connection and target instance.
- `CONNECTION_ID` : the name of your BigQuery connection.
- `CLUSTER_ID` : the name of your AlloyDB cluster.
- `INSTANCE_ID` : the name of your target AlloyDB instance.
- `SCHEMA_NAME` (Optional): the name of the destination schema in AlloyDB. If not provided, the default schema configured for the database user is used (typically `public` ).
- `TABLE_NAME` : the name of an existing destination table in AlloyDB, without the schema prefix.
- `WRITE_MODE` (Optional): the write mode to use when exporting data. Supported values:
  - `APPEND` : by default, this value directly inserts exported rows for faster throughput when you export new records. If the destination table has a `PRIMARY KEY` or `UNIQUE` constraint and a duplicate key conflict occurs, for example, because matching keys already exist in the table or a failed job attempt is retried after writing partial data, BigQuery automatically retries the export in `UPSERT` mode. If you expect your export to update existing rows, specify `UPSERT` directly to avoid the overhead of a retry.
  - `UPSERT` : updates existing records if a matching key exists, or inserts new records if no matching key is found. Requires a `PRIMARY KEY` or `UNIQUE` constraint on the destination table, with all key columns selected in the query. BigQuery matches rows using the table's `PRIMARY KEY` , or a `UNIQUE` constraint if the table has no primary key. If the table has additional `UNIQUE` constraints and an exported row contains a duplicate value in one of those columns, the export fails.
- `MAX_CONNECTIONS` (Optional): the maximum number of concurrent parallel connections from BigQuery workers to the AlloyDB instance. If specified, the value must be `1` or greater. Limiting connections can prevent overloading the target instance during large exports.

## Export statement examples

This section provides examples of `EXPORT DATA` statements for different use cases.

### Export in `APPEND` mode

The following example appends selected fields from the `mydataset.table1` table into an AlloyDB table named `my_target_table` :

```
EXPORT DATA
  WITH CONNECTION `myproject.us-central1.my-alloydb-conn`
  OPTIONS (
    format='ALLOYDB',
    uri="https://alloydb.googleapis.com/v1/projects/myproject/locations/us-central1/clusters/my-cluster/instances/my-instance",
    alloydb_options="""{
      "schema": "public",
      "table": "my_target_table",
      "write_mode": "APPEND"
    }"""
  )
AS SELECT
  col1 AS id,
  col2 AS name,
  col3 AS value
FROM
  `mydataset.table1`;
```

### Export in `UPSERT` mode

The following example upserts records from `mydataset.customers` into the AlloyDB `customer_profiles` table, which includes updating existing records matching the `customer_id` primary key and inserting new records:

```
EXPORT DATA
  WITH CONNECTION `myproject.us-central1.my-alloydb-conn`
  OPTIONS (
    format='ALLOYDB',
    uri="https://alloydb.googleapis.com/v1/projects/myproject/locations/us-central1/clusters/my-cluster/instances/my-instance",
    alloydb_options="""{
      "schema": "public",
      "table": "customer_profiles",
      "write_mode": "UPSERT",
      "max_parallel_connections": 8
    }"""
  )
AS SELECT
  customer_id,
  email,
  status,
  updated_at
FROM
  `mydataset.customers`;
```

## Sync a table for export

For full-table copies or automated mirroring without the need for SQL-based transformations, you can sync your BigQuery table directly to AlloyDB. While the `EXPORT DATA` statement lets you use a `SELECT` query to process, alias, or filter data before it is moved, you can use table syncs for a one-for-one migration of a BigQuery table.

Table syncs are available in the following modes:

- One-time import: Creates a writable, independent copy of a BigQuery table within AlloyDB.
- Periodic sync (mirroring): Creates a read-only local table in AlloyDB that automatically refreshes from BigQuery on a defined schedule.

For more information, see [Sync BigQuery data to AlloyDB](https://docs.cloud.google.com/alloydb/docs/sync-bigquery-data-to-alloydb) .

## Pricing

When you export data to AlloyDB using the `EXPORT DATA` statement, you are billed using [BigQuery capacity compute pricing](https://cloud.google.com/bigquery/pricing#capacity_compute_analysis_pricing) .

After the data is exported, you're charged for storing the data in AlloyDB. For more information, see [AlloyDB for PostgreSQL pricing](https://cloud.google.com/alloydb/pricing) .
