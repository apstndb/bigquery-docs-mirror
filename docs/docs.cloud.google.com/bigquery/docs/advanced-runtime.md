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
  - `  LOCATION  ` : the location of the project

It can take several minutes for the change to take effect.

Once you've enabled the advanced runtime, qualifying queries in the project or organization use the advanced runtime regardless of which user created the query job.
