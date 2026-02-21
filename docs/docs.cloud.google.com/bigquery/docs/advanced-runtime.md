# Use the BigQuery advanced runtime

BigQuery advanced runtime is a set of performance enhancements designed to automatically accelerate analytical workloads without requiring user action or code changes. This document describes these performance enhancements, including enhanced vectorization and short query optimizations.

## Roles and permissions

To get the permissions that you need to specify a configuration setting, ask your administrator to grant you the [BigQuery Admin](/iam/docs/roles-permissions/bigquery#bigquery.admin) ( `  roles/bigquery.admin  ` ) IAM role on your project or organization. For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

## Enhanced vectorization

Vectorized execution is a query processing model that operates on columns of data in blocks that align with CPU cache size and uses single instruction, multiple data (SIMD) instructions. Enhanced vectorization extends the vectorized query execution in BigQuery to the following aspects of query processing:

  - By leveraging specialized data encodings within the Capacitor storage format, filter evaluation operations can be executed on the encoded data.
  - Specialized encodings are propagated through the query plan, which allows more data to be processed while it's still encoded.
  - By implementing expression folding to evaluate deterministic functions and constant expressions, BigQuery can simplify complex predicates into constant values.

## Short query optimizations

BigQuery typically executes queries in a distributed environment using a shuffle intermediate layer. Short query optimizations dynamically identify queries that can be run as a single stage, reducing latency and slot consumption. Specialized encodings can be used more effectively when a query is run in a single stage. These optimizations are most effective when used with [optional job creation mode](/bigquery/docs/running-queries#optional-job-creation) , which minimizes job startup, maintenance, and result retrieval latency.

Eligibility for short query optimizations is dynamic and influenced by the following factors:

  - The predicted size of the data scan.
  - The amount of data movement required.
  - The selectivity of query filters.
  - The type and physical layout of the data in storage.
  - The overall query structure.
  - The [historical statistics](/bigquery/docs/history-based-optimizations) of past query executions.

## Enable the advanced runtime

Between September 15, 2025 and early 2026, BigQuery will start using the advanced runtime as the default runtime for all projects. To enable the advanced runtime in an existing project or organization now, use the [`  ALTER PROJECT  `](/bigquery/docs/reference/standard-sql/data-definition-language#alter_project_set_options_statement) or [`  ALTER ORGANIZATION  `](/bigquery/docs/reference/standard-sql/data-definition-language#alter_organization_set_options_statement) statement to change the [default configuration](/bigquery/docs/default-configuration) . In the statement, set the `  query_runtime  ` argument to `  'advanced'  ` . For example:

``` text
ALTER PROJECT PROJECT_NAME
SET OPTIONS (
  `region-LOCATION.query_runtime` = 'advanced'
);
```

Replace the following:

  - `  PROJECT_NAME  ` : the name of the project
  - `  LOCATION  ` : the location in which jobs should attempt to use the advanced runtime

It can take several minutes for the change to take effect.

Once you've enabled the advanced runtime, qualifying queries in the project or organization use the advanced runtime regardless of which user created the query job.

## Estimate the impact of the advanced runtime

To estimate the impact of the advanced runtime, you can use the following SQL query to identify project queries with the greatest estimated improvement to execution time:

``` text
WITH
  jobs AS (
    SELECT
      *,
      query_info.query_hashes.normalized_literals AS query_hash,
      TIMESTAMP_DIFF(end_time, start_time, MILLISECOND) AS elapsed_ms,
      EXISTS(
        SELECT 1
        FROM UNNEST(JSON_QUERY_ARRAY(query_info.optimization_details.optimizations)) AS o
        WHERE JSON_VALUE(o, '$.enhanced_vectorization') = 'applied'
      ) AS has_advanced_runtime
    FROM region-LOCATION.INFORMATION_SCHEMA.JOBS_BY_PROJECT
    WHERE EXTRACT(DATE FROM creation_time) > DATE_SUB(CURRENT_DATE(), INTERVAL 30 DAY)
  ),
  most_recent_jobs_without_advanced_runtime AS (
    SELECT *
    FROM jobs
    WHERE NOT has_advanced_runtime
    QUALIFY ROW_NUMBER() OVER (PARTITION BY query_hash ORDER BY end_time DESC) = 1
  )
SELECT
  job.job_id,
  100 * SAFE_DIVIDE(
    original_job.elapsed_ms - job.elapsed_ms,
    original_job.elapsed_ms) AS percent_execution_time_saved,
  job.elapsed_ms AS new_elapsed_ms,
  original_job.elapsed_ms AS original_elapsed_ms,
FROM jobs AS job
INNER JOIN most_recent_jobs_without_advanced_runtime AS original_job
  USING (query_hash)
WHERE
  job.has_advanced_runtime
  AND original_job.end_time < job.start_time
ORDER BY percent_execution_time_saved DESC
LIMIT 10;
```

Replace the following:

  - `  LOCATION  ` : the location in which job performance should be measured

If the advanced runtime was enabled and applied, the results of this query may be similar to the following:

``` text
/*--------------+----------------------------+----------------+---------------------*
 |    job_id    | percent_elapsed_time_saved | new_elapsed_ms | original_elapsed_ms |
 +--------------+----------------------------+----------------+---------------------+
 | sample_job1  |         45.38834951456311  |            225 |                 412 |
 | sample_job2  |         45.19480519480519  |            211 |                 385 |
 | sample_job3  |         33.246753246753244 |            257 |                 385 |
 | sample_job4  |         29.28802588996764  |           1311 |                1854 |
 | sample_job5  |         28.18181818181818  |           1027 |                1430 |
 | sample_job6  |         25.804195804195807 |           1061 |                1430 |
 | sample_job7  |         25.734265734265733 |           1062 |                1430 |
 | sample_job8  |         25.454545454545453 |           1066 |                1430 |
 | sample_job9  |         25.384615384615383 |           1067 |                1430 |
 | sample_job10 |         25.034965034965033 |           1072 |                1430 |
 *--------------+----------------------------+----------------+---------------------*/
```

The results of this query are only an estimate of the advanced runtime's impact. Many factors can influence query performance, including but not limited to slot availability, change in data over time, view or UDF definitions, and differences in query parameter values.

If the results of this query are empty, then either no jobs have used advanced runtime, or all jobs were optimized more than 30 days ago.

This query can be applied to other query performance metrics such as `  total_slot_ms  ` and `  total_bytes_billed  ` . For more information, see the schema for [`  INFORMATION_SCHEMA.JOBS_BY_PROJECT  `](/bigquery/docs/information-schema-jobs#schema) .
