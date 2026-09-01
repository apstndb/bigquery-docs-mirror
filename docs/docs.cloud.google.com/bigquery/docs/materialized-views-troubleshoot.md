---
name: documents/docs.cloud.google.com/bigquery/docs/materialized-views-troubleshoot
uri: https://docs.cloud.google.com/bigquery/docs/materialized-views-troubleshoot
title: Troubleshoot materialized views
description: Troubleshoot common issues with BigQuery materialized views, including creation errors, refresh failures, and query performance.
data_source: docs.cloud.google.com
---

# Troubleshoot materialized views

This document helps you troubleshoot common issues related to materialized views in BigQuery, including errors when creating materialized views, refresh failures, and unexpected query performance.

## Diagnostic workflow

When you investigate an issue with a materialized view, follow these diagnostic steps to identify the root cause:

1.  **Verify the table type and metadata** . Confirm that the target table is a materialized view and check its configuration options:
    
        SELECT
         table_name,
         table_type
        FROM
         `PROJECT_ID.DATASET`.INFORMATION_SCHEMA.TABLES
        WHERE
         table_name = 'MATERIALIZED_VIEW';
    
    Replace the following:
    
      - `  PROJECT_ID  ` : the project that contains the materialized view.
      - `  DATASET  ` : the dataset that contains the materialized view.
      - `  MATERIALIZED_VIEW  ` : the name of the materialized view.
    
    To inspect configuration options such as `enable_refresh` , `refresh_interval_minutes` , and `max_staleness` , query the [`INFORMATION_SCHEMA.TABLE_OPTIONS` view](https://docs.cloud.google.com/bigquery/docs/information-schema-table-options) :
    
        SELECT
         table_name,
         option_name,
         option_value
        FROM
         `PROJECT_ID.DATASET`.INFORMATION_SCHEMA.TABLE_OPTIONS
        WHERE
         table_name = 'MATERIALIZED_VIEW';

2.  **Check the last refresh status** . Query the [`INFORMATION_SCHEMA.MATERIALIZED_VIEWS` view](https://docs.cloud.google.com/bigquery/docs/information-schema-materialized-views) to check when the view was last refreshed and whether the last automatic refresh encountered errors:
    
        SELECT
         table_name,
         last_refresh_time,
         refresh_watermark,
         last_refresh_status
        FROM
         `PROJECT_ID.DATASET`.INFORMATION_SCHEMA.MATERIALIZED_VIEWS
        WHERE
         table_name = 'MATERIALIZED_VIEW';
    
    If `last_refresh_status` is not `NULL` , the last automatic refresh job failed. If `last_refresh_time` is `NULL` or old, the materialized view has never successfully completed a refresh or has been failing to refresh.

3.  **Inspect refresh job history and errors** . Query the [`INFORMATION_SCHEMA.JOBS_BY_PROJECT` view](https://docs.cloud.google.com/bigquery/docs/information-schema-jobs) to inspect recent automatic refresh jobs:
    
        SELECT
         job_id,
         creation_time,
         end_time,
         state,
         error_result.reason AS error_reason,
         error_result.message AS error_message,
         total_slot_ms,
         total_bytes_processed
        FROM
         `region-REGION`.INFORMATION_SCHEMA.JOBS_BY_PROJECT
        WHERE
         job_id LIKE '%materialized_view_refresh_%'
         AND creation_time >= TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 7 DAY)
        ORDER BY
         creation_time DESC
        LIMIT 50;
    
    Replace `  REGION  ` with your dataset's region—for example, `us` or `europe-west3` .

4.  **Examine query execution and smart tuning statistics** . If a query is running slower than expected, examine the `materialized_view_statistics` field in the job statistics to verify whether the query optimizer used the materialized view:
    
        SELECT
         job_id,
         total_slot_ms,
         total_bytes_billed,
         materialized_view_statistics
        FROM
         `region-REGION`.INFORMATION_SCHEMA.JOBS_BY_PROJECT
        WHERE
         job_id = 'JOB_ID';
    
    Replace `  JOB_ID  ` with the query job ID.

## Troubleshoot materialized view creation errors

This section describes errors that you might encounter when creating materialized views, along with their causes and resolution steps.

### Unsupported SQL operator or syntax

**Error message:**

    Unsupported operator in materialized view: KEYWORD

or

    Materialized view queries do not support FEATURE

**Cause:**

Incremental materialized views support a restricted subset of SQL syntax to enable incremental maintenance and smart tuning. You might encounter this error if the query defining your materialized view includes unsupported features, such as the following:

  - Non-deterministic functions (for example, `CURRENT_TIMESTAMP()` , `RAND()` , or `SESSION_USER()` )
  - Analytical window functions with `OVER()`
  - `ORDER BY` or `LIMIT` clauses
  - `DISTINCT` without aggregation
  - Subqueries in the `WHERE` or `SELECT` clauses
  - User-defined functions (UDFs)

**Resolution:**

  - Review the list of [unsupported SQL features](https://docs.cloud.google.com/bigquery/docs/materialized-views-create#unsupported_sql_features) .

  - If your query requires broader SQL capabilities, consider creating a [non-incremental materialized view](https://docs.cloud.google.com/bigquery/docs/materialized-views-create#non-incremental) by setting `allow_non_incremental_definition = true` and defining a `max_staleness` interval:
    
        CREATE MATERIALIZED VIEW `PROJECT_ID.DATASET.MATERIALIZED_VIEW`
        OPTIONS (
        enable_refresh = true,
        refresh_interval_minutes = 60,
        max_staleness = INTERVAL "4" HOUR,
        allow_non_incremental_definition = true
        ) AS
        SELECT
        ...
    
    Replace the following:
    
      - `  PROJECT_ID  ` : the project that contains the materialized view.
      - `  DATASET  ` : the dataset that contains the materialized view.
      - `  MATERIALIZED_VIEW  ` : the name of the materialized view.
    
    Non-incremental materialized views support a broader set of SQL queries, but they always perform full refreshes and don't support smart tuning.

  - If the required SQL syntax isn't supported in non-incremental materialized views, use a [logical view](https://docs.cloud.google.com/bigquery/docs/views) or a [scheduled query](https://docs.cloud.google.com/bigquery/docs/scheduling-queries) to write results to a destination table.

### Invalid max\_staleness with CDC base table

**Error message:**

    Materialized view PROJECT_ID:DATASET.MATERIALIZED_VIEW has a CDC table as base table PROJECT_ID:DATASET.TABLE but does not have valid max_staleness. Materialized views over CDC tables must have max_staleness set at least 2 times the base table's max_staleness: 0-0 0 0:0:0

**Cause:**

When you create a materialized view over a change data capture (CDC) base table, the materialized view's `max_staleness` option must be configured to at least twice the value of the base table's `max_staleness` value.

**Resolution:**

1.  Check the `max_staleness` value of the base CDC table by querying the [`INFORMATION_SCHEMA.TABLE_OPTIONS` view](https://docs.cloud.google.com/bigquery/docs/information-schema-table-options) .
2.  Set the `max_staleness` option of the materialized view to a value that is at least two times the base table's `max_staleness` value. For example, if the base CDC table has a `max_staleness` value of 15 minutes, set the materialized view's `max_staleness` value to at least 30 minutes. For more information, see " `ALTER MATERIALIZED VIEW SET OPTIONS` statement" in [Data definition language (DDL) statements in GoogleSQL](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#alter_materialized_view_set_options_statement) .

### Partitioned materialized view over non-partitioned base table

**Error message:**

    Partitioned incremental materialized view must be created on top of partitioned managed storage base table.

**Cause:**

To create a partitioned incremental materialized view, the underlying base table must also be partitioned, and the materialized view's partitioning column must align with the base table's partitioning column.

**Resolution:**

  - If you want the materialized view to be partitioned, ensure the base table is partitioned and configure the materialized view to use the same partitioning column. For more information, see [Partition alignment](https://docs.cloud.google.com/bigquery/docs/materialized-views-use#partition_alignment) .
  - If the base table is not partitioned, create the materialized view without a `PARTITION BY` clause.
  - If you need a partitioned view over a non-partitioned table, create a [non-incremental materialized view](https://docs.cloud.google.com/bigquery/docs/materialized-views-create#non-incremental) with `allow_non_incremental_definition = true` and `max_staleness` . Non-incremental materialized views don't require partition alignment with base tables.

### Cross-region dataset replica is read-only

**Error message:**

    The dataset replica of the cross region dataset 'PROJECT_ID:DATASET' in region 'REGION' is read-only because it's not the primary replica.

**Cause:**

When you use [cross-region dataset replication](https://docs.cloud.google.com/bigquery/docs/data-replication) , secondary replicas are read-only. You cannot create a materialized view in a secondary replica region.

**Resolution:**

Create the materialized view in the primary region of the replicated dataset. If you need the materialized view in the replica region, create a materialized view replica in that region. For more information, see [Manage materialized view replicas](https://docs.cloud.google.com/bigquery/docs/materialized-view-replicas-manage) .

### Exceeding the base table limit

**Error message:**

    Materialized views support at most 10 source tables, query has NUMBER_OF_SOURCE_TABLES

**Cause:**

BigQuery materialized views support joins across at most 10 base tables.

**Resolution:**

Refactor the query defining the materialized view to reference 10 or fewer base tables. If your architecture requires joining more than 10 tables, consider pre-joining static or dimension tables into intermediate tables, or use a [scheduled query](https://docs.cloud.google.com/bigquery/docs/scheduling-queries) or a [Dataform pipeline](https://docs.cloud.google.com/dataform/docs/overview) .

### Resources exceeded during materialized view creation

**Error message:**

    Resources exceeded during query execution: The data accessed in this query is too large; consider accessing fewer tables, or for partitioned tables, fewer partitions.

**Cause:**

When you create a materialized view, BigQuery performs an initial full refresh to populate the view. If the underlying base table contains massive amounts of unpartitioned data, or if the view produces high cardinality intermediate aggregations, the initial refresh can exceed slot memory or query limits.

**Resolution:**

  - Add filter conditions in the `WHERE` clause of the materialized view to limit the scope of scanned data to the required subset.
  - Align the materialized view partitioning with the base table partitioning to prune partitions during refreshes.
  - If using on-demand compute, consider using [BigQuery editions](https://docs.cloud.google.com/bigquery/docs/editions-intro) with dedicated slot reservations to provide sufficient compute capacity for large refreshes.

### Issues with BigLake tables and metadata caching

**Symptoms:**

Materialized views over [BigLake external tables](https://docs.cloud.google.com/bigquery/docs/biglake-intro) fail during creation or fail to refresh.

**Cause:**

Materialized views over external tables have specific architectural requirements:

  - Materialized views are only supported over BigLake tables with [metadata caching enabled](https://docs.cloud.google.com/bigquery/docs/metadata-caching) .
  - The `max_staleness` value of the materialized view must be greater than the `max_staleness` value of the underlying BigLake base table.
  - A materialized view can reference BigLake external tables or BigQuery managed storage tables, but can't mix types in a single materialized view.

**Resolution:**

1.  Ensure metadata caching is enabled on all underlying BigLake base tables.
2.  Configure `max_staleness` on the materialized view to a value higher than the metadata cache interval of the base tables. For example, if the base table cache interval is 30 minutes, set the materialized view's `max_staleness` to at least 45 minutes to allow a buffer for refresh execution.
3.  Don't mix external tables and managed tables in a materialized view definition.

## Troubleshoot refresh issues

This section describes common causes of refresh failures and performance delays for materialized views.

### Base table schema changes ( `invalidQuery` )

**Symptoms:**

The `last_refresh_status` column in `INFORMATION_SCHEMA.MATERIALIZED_VIEWS` displays an `invalidQuery` error, and automatic refreshes stop running.

**Cause:**

If a base table's schema changes—such as dropping a column referenced by the materialized view, renaming a column, or altering a column's data type—the underlying query defining the materialized view becomes invalid.

**Resolution:**

BigQuery does not support altering the column schema of an existing materialized view. To resolve schema invalidation, do the following:

1.  Recreate the materialized view using the [`CREATE OR REPLACE MATERIALIZED VIEW` statement](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_materialized_view_statement) :
    
        CREATE OR REPLACE MATERIALIZED VIEW `PROJECT_ID.DATASET.MATERIALIZED_VIEW`
        OPTIONS (
         enable_refresh = true,
         refresh_interval_minutes = 30
        ) AS
        SELECT
         ...
    
    Replace the following:
    
      - `  PROJECT_ID  ` : the project that contains the materialized view.
      - `  DATASET  ` : the dataset that contains the materialized view.
      - `  MATERIALIZED_VIEW  ` : the name of the materialized view.

2.  Verify that the new definition matches the updated base table schema.

### Base table partition expiration, truncation, or DML changes

**Symptoms:**

Materialized view refreshes fail, or queries against the materialized view fall back to the base table and run slowly.

**Cause:**

The following base table operations invalidate existing materialized view data:

  - Truncating a base table or base table partition ( `TRUNCATE TABLE` )
  - Partition expiration on a base table
  - `DELETE` or `MERGE` data manipulation language (DML) statements on unpartitioned tables or secondary joined base tables

When these operations occur, the affected partitions (or the entire materialized view for unpartitioned tables) are marked as invalid.

**Resolution:**

1.  Manually trigger a refresh to restore the materialized view to a valid state:
    
        CALL BQ.REFRESH_MATERIALIZED_VIEW('PROJECT_ID.DATASET.MATERIALIZED_VIEW');

2.  If you run batch ETL pipelines that execute DML statements or truncate data regularly, disable automatic refresh and call `BQ.REFRESH_MATERIALIZED_VIEW` at the end of your ETL pipeline. For more information, see [Automatic refresh](https://docs.cloud.google.com/bigquery/docs/materialized-views-manage#automatic-refresh) .

### Refresh jobs timing out

**Symptoms:**

Refresh jobs fail with a timeout error after running for several hours (up to 12 hours).

**Cause:**

As base tables grow, the volume of data processed during a refresh increases. If the materialized view query does not filter rows, or if the view cannot perform incremental updates due to full invalidation, each refresh requires a full scan of the base tables, which can exhaust slot time.

**Resolution:**

  - Add filter criteria in the `WHERE` clause of the materialized view to restrict unnecessary historic data.
  - Ensure the materialized view is partition-aligned with the base table so only modified partitions are refreshed incrementally.
  - Allocate a slot reservation with sufficient capacity to accommodate the refresh workload.

### Duplicate refresh message

**Message:**

    Materialized view is already being refreshed.

**Cause:**

If base tables in a `JOIN` materialized view are updated simultaneously, or if a manual refresh is triggered while an automatic refresh is already in progress, BigQuery detects the concurrent refresh and cancels the duplicate job.

**Resolution:**

This behavior is normal and transient. The duplicate job is stopped to prevent redundant processing, and you aren't billed for the duplicate refresh attempt. No action is required.

### Streaming data (write-optimized storage) refresh delays

**Symptoms:**

Queries against base tables with high-velocity streaming data don't appear in the materialized view immediately, or queries fall back to the base table.

**Cause:**

Data streamed into BigQuery using the Storage Write API is initially stored in the write-optimized storage (streaming buffer). The refresh jobs of the materialized view process data after it is committed and converted from the streaming buffer into optimized columnar storage.

To maintain real-time consistency, queries reading from the materialized view read committed data from the materialized view and simultaneously read the delta directly from the base table streaming buffer.

**Resolution:**

  - If real-time read consistency on streaming data is required, the query planner automatically combines materialized view data with base table deltas.
  - If real-time consistency is not required and you want to avoid scanning the streaming buffer on every query, set `max_staleness` on the materialized view (for example, `max_staleness = INTERVAL "15" MINUTE` ). Queries can then read directly from the precomputed materialized view without delta processing.

## Troubleshoot query performance and smart tuning

This section describes how to troubleshoot queries that run slower than expected or don't take advantage of smart tuning.

### Verify smart tuning usage

When you query a base table, BigQuery uses smart tuning to automatically rewrite the query to use an available materialized view if it improves performance and reduces cost.

To check whether a query used a materialized view, inspect the `materialized_view_statistics` field in the query job details or query the [`INFORMATION_SCHEMA.JOBS_BY_PROJECT` view](https://docs.cloud.google.com/bigquery/docs/information-schema-jobs) :

    SELECT
      job_id,
      total_slot_ms,
      total_bytes_billed,
      mv.table_reference.dataset_id,
      mv.table_reference.table_id,
      mv.chosen,
      mv.rejected_reason
    FROM
      `region-REGION`.INFORMATION_SCHEMA.JOBS_BY_PROJECT,
      UNNEST(materialized_view_statistics.materialized_view) AS mv
    WHERE
      job_id = 'JOB_ID';

Replace the following:

  - `  REGION  ` : your dataset's region (for example, `us` or `europe-west3` ).
  - `  JOB_ID  ` : the query job ID.

In the `materialized_view_statistics` object, each entry in the `materialized_view` array contains the following fields:

  - `table_reference` : identifies the materialized view candidate.
  - `chosen` : a boolean indicating whether the query optimizer selected the materialized view for execution ( `true` ) or rejected it ( `false` ).
  - `estimated_bytes_saved` : the estimated bytes that the query avoided scanning by using the materialized view.
  - `rejected_reason` : if `chosen` is `false` , specifies the reason why the optimizer rejected the materialized view.

For more information about rejected reasons and the `rejected_reason` enum, see [Understand why materialized views were rejected](https://docs.cloud.google.com/bigquery/docs/materialized-views-use#understand-rejected) .

### Common reasons a materialized view is rejected

When `chosen` is `false` , examine the value of `rejected_reason` to diagnose the cause:

| `rejected_reason` value                   | Description                                                                                                                                  | Resolution                                                                                                                                                                                                |
| :---------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `NO_DATA`                                 | The materialized view has no cached data because it hasn't refreshed yet, or the initial refresh failed.                                     | Trigger a manual refresh using `CALL BQ.REFRESH_MATERIALIZED_VIEW(...)` .                                                                                                                                 |
| `COST`                                    | The query optimizer estimated that querying the base table (or reading from the query cache) is cheaper than querying the materialized view. | Review query filters and partitions. If the base table query scans only a tiny partition while the materialized view spans multiple partitions, querying the base table directly might be more efficient. |
| `BASE_TABLE_DATA_CHANGE`                  | Data changes in one or more base tables invalidated the cached data outside the configured staleness window.                                 | Perform a manual refresh or configure `max_staleness` to allow queries to read stale data without falling back to base tables.                                                                            |
| `BASE_TABLE_TRUNCATED`                    | A base table was truncated, invalidating all materialized view data.                                                                         | Refresh the materialized view after data is repopulated.                                                                                                                                                  |
| `BASE_TABLE_EXPIRED_PARTITION`            | A partition in the base table expired.                                                                                                       | Ensure partition expiration settings match between the base table and the materialized view, and refresh the view.                                                                                        |
| `BASE_TABLE_PARTITION_EXPIRATION_CHANGE`  | The partition expiration duration of a base table was modified.                                                                              | Refresh the materialized view to realign partition expiration metadata.                                                                                                                                   |
| `BASE_TABLE_INCOMPATIBLE_METADATA_CHANGE` | A metadata change occurred on a base table (such as a schema modification).                                                                  | Recreate the materialized view using `CREATE OR REPLACE MATERIALIZED VIEW` .                                                                                                                              |
| `BASE_TABLE_TOO_STALE`                    | A base table's cached metadata (for example, on a BigLake external table) is older than the allowed threshold.                               | Refresh the external table's metadata cache.                                                                                                                                                              |
| `BASE_TABLE_FINE_GRAINED_SECURITY_POLICY` | The query user lacks access under a row-level or column-level access control policy on a base table.                                         | Verify IAM permissions and data policy grants.                                                                                                                                                            |
| `TIME_ZONE`                               | The view was refreshed using a time zone different from the time zone of the current query.                                                  | Align time zone settings between your environment and refresh jobs.                                                                                                                                       |

### Materialized view not considered (query structure mismatch)

If a materialized view is not listed in `materialized_view_statistics` , the query optimizer determined during syntax parsing that the query pattern did not match the materialized view definition.

Common causes include the following:

1.  **Aggregation or filter mismatch** . The query uses aggregation functions, grouping columns, or filter predicates that cannot be computed from the precomputed aggregations in the materialized view.
      - *Resolution* : Align aggregate functions and groupings between your queries and the materialized view definition.
2.  **Non-incremental materialized views** . Views created with `allow_non_incremental_definition = true` don't support smart tuning.
      - *Resolution* : Query non-incremental materialized views directly by specifying the view name in the `FROM` clause.
3.  **Direct query over stale view** . If you query a materialized view directly that has `max_staleness` set, the query returns stale precomputed results up to `max_staleness` without delta processing from base tables.

### Incompatible HyperLogLog sketch error

**Error message:**

    Invalid or incompatible sketch in HLL_COUNT.MERGE_PARTIAL

**Cause:**

When you use approximate aggregation functions like `HLL_COUNT.INIT` and `HLL_COUNT.MERGE_PARTIAL` , BigQuery uses HyperLogLog sketches. If the precision parameter specified in the query does not match the precision parameter defined in the materialized view, the sketch merge operation fails.

**Resolution:**

Ensure the precision parameter (for example, `HLL_COUNT.INIT(x, 12)` ) is identical in both the materialized view definition and the queries referencing or rewriting to the view.

## Troubleshoot view alteration and schema modifications

This section describes issues that you might encounter when modifying the schema or options of a materialized view.

### Editing materialized view schema

**Issue:**

Attempting to add or modify columns in a materialized view using `ALTER TABLE` or the Google Cloud console results in an error, or the **Edit Schema** option is unavailable.

**Cause:**

BigQuery does not support modifying the column schema of a materialized view directly.

**Resolution:**

  - You can modify materialized view options (such as `enable_refresh` , `refresh_interval_minutes` , and `max_staleness` ) using the `ALTER MATERIALIZED VIEW SET OPTIONS` statement:
    
        ALTER MATERIALIZED VIEW `PROJECT_ID.DATASET.MATERIALIZED_VIEW`
        SET OPTIONS (
        enable_refresh = true,
        refresh_interval_minutes = 20
        );
    
    Replace the following:
    
      - `  PROJECT_ID  ` : the project that contains the materialized view.
      - `  DATASET  ` : the dataset that contains the materialized view.
      - `  MATERIALIZED_VIEW  ` : the name of the materialized view.

  - To change the SQL query definition, add columns, or change column data types, recreate the view using `CREATE OR REPLACE MATERIALIZED VIEW` :
    
        CREATE OR REPLACE MATERIALIZED VIEW `PROJECT_ID.DATASET.MATERIALIZED_VIEW`
        AS SELECT
        ...

## What's next

  - Learn how to [create materialized views](https://docs.cloud.google.com/bigquery/docs/materialized-views-create) .
  - Learn how to [use materialized views and smart tuning](https://docs.cloud.google.com/bigquery/docs/materialized-views-use) .
  - Learn how to [manage and refresh materialized views](https://docs.cloud.google.com/bigquery/docs/materialized-views-manage) .
  - Learn how to [monitor materialized view refreshes and usage](https://docs.cloud.google.com/bigquery/docs/materialized-views-monitor) .
  - Learn how to [troubleshoot general query performance issues](https://docs.cloud.google.com/bigquery/docs/troubleshoot-queries) .
