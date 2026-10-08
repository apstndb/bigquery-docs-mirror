---
name: documents/docs.cloud.google.com/bigquery/docs/information-schema-jobs-by-user
uri: https://docs.cloud.google.com/bigquery/docs/information-schema-jobs-by-user
title: JOBS_BY_USER view
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# JOBS_BY_USER view

The `INFORMATION_SCHEMA.JOBS_BY_USER` view contains near real-time metadata about the BigQuery jobs submitted by the current user in the current project.

## Required role

To get the permission that you need to query the `INFORMATION_SCHEMA.JOBS_BY_USER` view, ask your administrator to grant you the [BigQuery User](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.user) ( `roles/bigquery.user` ) IAM role on your project. For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

This predefined role contains the `bigquery.jobs.list` permission, which is required to query the `INFORMATION_SCHEMA.JOBS_BY_USER` view.

You might also be able to get this permission with [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

For more information about BigQuery permissions, see [Access control with IAM](https://docs.cloud.google.com/bigquery/docs/access-control) .

## Schema

The underlying data is partitioned by the `creation_time` column and clustered by `project_id` and `user_email` .

The `INFORMATION_SCHEMA.JOBS_BY_USER` view has the following schema:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Column name</strong></th>
<th><strong>Data type</strong></th>
<th><strong>Value</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>bi_engine_statistics</code></td>
<td><code>RECORD</code></td>
<td>If the project is configured to use the <a href="https://cloud.google.com/bigquery/docs/bi-engine-intro">BI Engine</a> , then this field contains <a href="https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#bienginestatistics">BiEngineStatistics</a> . Otherwise <code>NULL</code> .</td>
</tr>
<tr class="even">
<td><code>cache_hit</code></td>
<td><code>BOOLEAN</code></td>
<td>Whether the query results of this job were from a cache. If you have a <a href="https://docs.cloud.google.com/bigquery/docs/multi-statement-queries">multi-query statement job</a> , <code>cache_hit</code> for your parent query is <code>NULL</code> .</td>
</tr>
<tr class="odd">
<td><code>creation_time</code></td>
<td><code>TIMESTAMP</code></td>
<td>( <em>Partitioning column</em> ) Creation time of this job. Partitioning is based on the UTC time of this timestamp.</td>
</tr>
<tr class="even">
<td><code>destination_table</code></td>
<td><code>RECORD</code></td>
<td>Destination <a href="https://cloud.google.com/bigquery/docs/reference/rest/v2/TableReference">table</a> for results, if any.</td>
</tr>
<tr class="odd">
<td><code>dml_statistics</code></td>
<td><code>RECORD</code></td>
<td>If the job is a query with a DML statement, the value is a record with the following fields:<br />

<ul>
<li><code>inserted_row_count</code> : The number of rows that were inserted.</li>
<li><code>deleted_row_count</code> : The number of rows that were deleted.</li>
<li><code>updated_row_count</code> : The number of rows that were updated.</li>
</ul>
For all other jobs, the value is <code>NULL</code> .<br />
This column is present in the <code>INFORMATION_SCHEMA.JOBS_BY_USER</code> and <code>INFORMATION_SCHEMA.JOBS_BY_PROJECT</code> views.</td>
</tr>
<tr class="even">
<td><code>end_time</code></td>
<td><code>TIMESTAMP</code></td>
<td>The end time of this job, in milliseconds since the epoch. This field represents the time when the job enters the <code>DONE</code> state.</td>
</tr>
<tr class="odd">
<td><code>error_result</code></td>
<td><code>RECORD</code></td>
<td>Details of any errors as <a href="https://cloud.google.com/bigquery/docs/reference/rest/v2/ErrorProto">ErrorProto</a> objects.</td>
</tr>
<tr class="even">
<td><code>job_creation_reason.code</code></td>
<td><code>STRING</code></td>
<td>Specifies the high level reason why a job was created.<br />
Possible values are:
<ul>
<li><code>REQUESTED</code> : job creation was requested.</li>
<li><code>LONG_RUNNING</code> : the query request ran beyond a system defined timeout specified by the <a href="https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query#queryrequest">timeoutMs field in the <code>QueryRequest</code></a> . As a result it was considered a long running operation for which a job was created.</li>
<li><code>LARGE_RESULTS</code> : the results from the query cannot fit in the in-line response.</li>
<li><code>OTHER</code> : the system has determined that the query needs to be executed as a job.</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>job_id</code></td>
<td><code>STRING</code></td>
<td>The ID of the job if a job was created. Otherwise, the query ID of a query using optional job creation mode. For example, <code>bquxjob_1234</code> .</td>
</tr>
<tr class="even">
<td><code>job_stages</code></td>
<td><code>RECORD REPEATED</code></td>
<td><a href="https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#ExplainQueryStage">Query stages</a> of the job.
<p><strong>Note</strong> : This column's values are empty for queries that read from tables with row-level access policies. For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/best-practices-row-level-security">best practices for row-level security in BigQuery.</a></p></td>
</tr>
<tr class="odd">
<td><code>job_type</code></td>
<td><code>STRING</code></td>
<td>The type of the job. Can be <code>QUERY</code> , <code>LOAD</code> , <code>EXTRACT</code> , <code>COPY</code> , or <code>NULL</code> . A <code>NULL</code> value indicates a background job.</td>
</tr>
<tr class="even">
<td><code>labels</code></td>
<td><code>RECORD</code></td>
<td>Array of labels applied to the job as key-value pairs.</td>
</tr>
<tr class="odd">
<td><code>object_storage_stats</code></td>
<td><code>RECORD REPEATED</code></td>
<td>Statistics for object storage and caching usage for a query job. The value is a repeated record with the following fields:<br />

<ul>
<li><code>cloud_provider</code> : The cloud provider where the object storage is hosted (for example, <code>AWS</code> ).</li>
<li><code>object_storage_bytes_read</code> : Total number of bytes read directly from object storage.</li>
<li><code>cache_bytes_read</code> : Total number of bytes read from cache.</li>
</ul></td>
</tr>
<tr class="even">
<td><code>parent_job_id</code></td>
<td><code>STRING</code></td>
<td>ID of the parent job, if any.</td>
</tr>
<tr class="odd">
<td><code>priority</code></td>
<td><code>STRING</code></td>
<td>The priority of this job. Valid values include <code>INTERACTIVE</code> and <code>BATCH</code> .</td>
</tr>
<tr class="even">
<td><code>project_id</code></td>
<td><code>STRING</code></td>
<td>( <em>Clustering column</em> ) The ID of the project.</td>
</tr>
<tr class="odd">
<td><code>project_number</code></td>
<td><code>INTEGER</code></td>
<td>The number of the project.</td>
</tr>
<tr class="even">
<td><code>query</code></td>
<td><code>STRING</code></td>
<td>SQL query text.</td>
</tr>
<tr class="odd">
<td><code>referenced_tables</code></td>
<td><code>RECORD</code></td>
<td>Array of <code>STRUCT</code> values that contain the following <code>STRING</code> fields for each table referenced by the query: <code>project_id</code> , <code>dataset_id</code> , and <code>table_id</code> . Only populated for query jobs that are not cache hits.</td>
</tr>
<tr class="even">
<td><code>reservation_id</code></td>
<td><code>STRING</code></td>
<td>Name of the primary reservation assigned to this job, in the format <code>RESERVATION_ADMIN_PROJECT:RESERVATION_LOCATION.RESERVATION_NAME</code> .<br />
In this output:
<ul>
<li><code>RESERVATION_ADMIN_PROJECT</code> : the name of the Google Cloud project that administers the reservation</li>
<li><code>RESERVATION_LOCATION</code> : the location of the reservation</li>
<li><code>RESERVATION_NAME</code> : the name of the reservation</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>reservation_group_path</code></td>
<td><code>ARRAY&lt;STRING&gt;</code></td>
<td>The reservation group to which the reservation is linked. For example, if the reservation is linked to group <code>my-group</code> , the <code>reservation_group_path</code> field contains a list such as: <code>[my-group]</code> .</td>
</tr>
<tr class="even">
<td><code>edition</code></td>
<td><code>STRING</code></td>
<td>The edition associated with the reservation assigned to this job. For more information about editions, see <a href="https://docs.cloud.google.com/bigquery/docs/editions-intro">Introduction to BigQuery editions</a> .</td>
</tr>
<tr class="odd">
<td><code>session_info</code></td>
<td><code>RECORD</code></td>
<td>Details about the <a href="https://cloud.google.com/bigquery/docs/sessions-intro">session</a> in which this job ran, if any.</td>
</tr>
<tr class="even">
<td><code>start_time</code></td>
<td><code>TIMESTAMP</code></td>
<td>The start time of this job, in milliseconds since the epoch. This field represents the time when the job transitions from the <code>PENDING</code> state to either <code>RUNNING</code> or <code>DONE</code> .</td>
</tr>
<tr class="odd">
<td><code>state</code></td>
<td><code>STRING</code></td>
<td>Running state of the job. Valid states include <code>PENDING</code> , <code>RUNNING</code> , and <code>DONE</code> .</td>
</tr>
<tr class="even">
<td><code>statement_type</code></td>
<td><code>STRING</code></td>
<td>The type of query statement. For example, <code>DELETE</code> , <code>INSERT</code> , <code>SCRIPT</code> , <code>SELECT</code> , or <code>UPDATE</code> . See <a href="https://cloud.google.com/bigquery/docs/reference/auditlogs/rest/Shared.Types/BigQueryAuditMetadata.QueryStatementType">QueryStatementType</a> for list of valid values.</td>
</tr>
<tr class="odd">
<td><code>timeline</code></td>
<td><code>RECORD</code></td>
<td><a href="https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#QueryTimelineSample">Query timeline</a> of the job. Contains snapshots of query execution.</td>
</tr>
<tr class="even">
<td><code>total_bytes_billed</code></td>
<td><code>INTEGER</code></td>
<td>If the project is configured to use <a href="https://cloud.google.com/bigquery/pricing#analysis_pricing_models">on-demand pricing</a> , then this field contains the total bytes billed for the job. If the project is configured to use <a href="https://cloud.google.com/bigquery/pricing#analysis_pricing_models">flat-rate pricing</a> , then you are not billed for bytes and this field is informational only.
<p><strong>Note</strong> : This column's values are empty for queries that read from tables with row-level access policies. For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/best-practices-row-level-security">best practices for row-level security in BigQuery.</a></p></td>
</tr>
<tr class="odd">
<td><code>total_bytes_processed</code></td>
<td><code>INTEGER</code></td>
<td><p>Total bytes processed by the job.</p>
<p><strong>Note</strong> : This column's values are empty for queries that read from tables with row-level access policies. For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/best-practices-row-level-security">best practices for row-level security in BigQuery.</a></p></td>
</tr>
<tr class="even">
<td><code>total_modified_partitions</code></td>
<td><code>INTEGER</code></td>
<td>The total number of partitions the job modified. This field is populated for <code>LOAD</code> and <code>QUERY</code> jobs.</td>
</tr>
<tr class="odd">
<td><code>total_slot_ms</code></td>
<td><code>INTEGER</code></td>
<td>Slot milliseconds for the job over its entire duration in the <code>RUNNING</code> state, including retries.</td>
</tr>
<tr class="even">
<td><code>total_services_sku_slot_ms</code></td>
<td><code>INTEGER</code></td>
<td>Total slot milliseconds for the job that runs on external services and is billed on the services SKU. This field is only populated for jobs that have external service costs, and is the total of the usage for costs whose billing method is <code>"SERVICES_SKU"</code> .</td>
</tr>
<tr class="odd">
<td><code>transaction_id</code></td>
<td><code>STRING</code></td>
<td>ID of the <a href="https://cloud.google.com/bigquery/docs/transactions">transaction</a> in which this job ran, if any.</td>
</tr>
<tr class="even">
<td><code>user_email</code></td>
<td><code>STRING</code></td>
<td>( <em>Clustering column</em> ) Email address or service account of the user who ran the job.</td>
</tr>
<tr class="odd">
<td><code>principal_subject</code></td>
<td><code>STRING</code></td>
<td>A string representation of the identity of the principal that ran the job.</td>
</tr>
<tr class="even">
<td><code>query_info.resource_warning</code></td>
<td><code>STRING</code></td>
<td>The warning message that appears if the resource usage during query processing is above the internal threshold of the system.<br />
A successful query job can have the <code>resource_warning</code> field populated. With <code>resource_warning</code> , you get additional data points to optimize your queries and to set up monitoring for performance trends of an equivalent set of queries by using <code>query_hashes</code> .</td>
</tr>
<tr class="odd">
<td><code>query_info.query_hashes.normalized_literals</code></td>
<td><code>STRING</code></td>
<td>Contains the hash value of the query. <code>normalized_literals</code> is a hexadecimal <code>STRING</code> hash that ignores comments, parameter values, UDFs, and literals. The hash value will differ when underlying views change, or if the query implicitly references columns, such as <code>SELECT *</code> , and the table schema changes.<br />
This field appears for successful <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/query-syntax">GoogleSQL</a> queries that are not cache hits.</td>
</tr>
<tr class="even">
<td><code>query_info.performance_insights</code></td>
<td><code>RECORD</code></td>
<td><a href="https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#PerformanceInsights">Performance insights</a> for the job.</td>
</tr>
<tr class="odd">
<td><code>transferred_bytes</code></td>
<td><code>INTEGER</code></td>
<td>Total bytes transferred for BigQuery Omni queries, such as BigQuery Omni transfer jobs.</td>
</tr>
<tr class="even">
<td><code>materialized_view_statistics</code></td>
<td><code>RECORD</code></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/Job#MaterializedViewStatistics">Statistics of materialized views</a> considered in a query job. ( <a href="https://cloud.google.com/products#product-launch-stages">Preview</a> )</td>
</tr>
<tr class="odd">
<td><code>metadata_cache_statistics</code></td>
<td><code>RECORD</code></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/Job#metadatacachestatistics">Statistics for metadata column index usage for tables</a> referenced in a query job.</td>
</tr>
<tr class="even">
<td><code>search_statistics</code></td>
<td><code>RECORD</code></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/Job#SearchStatistics">Statistics for a search query.</a></td>
</tr>
<tr class="odd">
<td><code>query_dialect</code></td>
<td><code>STRING</code></td>
<td>This field will be available sometime in May, 2025. The query dialect used for the job. Valid values include:<br />

<ul>
<li><code>GOOGLE_SQL</code> : Job was requested to use GoogleSQL.</li>
<li><code>LEGACY_SQL</code> : Job was requested to use LegacySQL.</li>
<li><code>DEFAULT_LEGACY_SQL</code> : No query dialect was specified in the job request. BigQuery used the default value of LegacySQL.</li>
<li><code>DEFAULT_GOOGLE_SQL</code> : No query dialect was specified in the job request. BigQuery used the default value of GoogleSQL.</li>
</ul>
<p>For jobs submitted by users, this field is only populated for query jobs. The default selection of query dialect can be controlled by the <a href="https://docs.cloud.google.com/bigquery/docs/default-configuration#configuration-settings">configuration settings</a> .</p>
<p>For background jobs, the value of this field isn't controlled by the default query dialect configuration settings, and doesn't impact jobs submitted by users. For some background jobs, the value is omitted.</p></td>
</tr>
<tr class="even">
<td><code>continuous</code></td>
<td><code>BOOLEAN</code></td>
<td>Whether the job is a <a href="https://cloud.google.com/bigquery/docs/continuous-queries-introduction">continuous query</a> .</td>
</tr>
<tr class="odd">
<td><code>continuous_query_info.output_watermark</code></td>
<td><code>TIMESTAMP</code></td>
<td>Represents the point up to which the continuous query has successfully processed data.</td>
</tr>
<tr class="even">
<td><code>vector_search_statistics</code></td>
<td><code>RECORD</code></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/Job#VectorSearchStatistics">Statistics for a vector search query.</a></td>
</tr>
<tr class="odd">
<td><code>external_service_costs</code></td>
<td><code>RECORD</code></td>
<td>An array of information about the external service costs for a query job.</td>
</tr>
<tr class="even">
<td><code>ml_statistics.model_type</code></td>
<td><code>STRING</code></td>
<td>If the job is a BigQuery ML model creation query, then this field specifies the <a href="https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/models#ModelType">type of model</a> being created. For all other jobs, the value is <code>NULL</code> .</td>
</tr>
</tbody>
</table>

For stability, we recommend that you explicitly list columns in your information schema queries instead of using a wildcard ( `SELECT *` ). Explicitly listing columns prevents queries from breaking if the underlying schema changes.

## Data retention

This view displays running jobs along with job history for the past 180 days. If a project migrates to an organization (either from having no organization or from a different one), job information predating the migration date isn't accessible through the `INFORMATION_SCHEMA.JOBS_BY_USER` view, as the view only retains data starting from the migration date.

## Scope and syntax

Queries against this view must include a [region qualifier](https://docs.cloud.google.com/bigquery/docs/information-schema-intro#syntax) . The following table explains the region scope for this view:

| View name                                                                              | Resource scope                                               | Region scope |
|----------------------------------------------------------------------------------------|--------------------------------------------------------------|--------------|
| `[ `` PROJECT_ID ```  .]`region-  ``` REGION ```  `.INFORMATION_SCHEMA.JOBS_BY_USER `` | Jobs submitted by the current user in the specified project. | `REGION`     |

Replace the following:

- Optional: `PROJECT_ID` : the ID of your Google Cloud project. If not specified, the default project is used.

- `REGION` : any [dataset region name](https://docs.cloud.google.com/bigquery/docs/locations) . For example, `` `region-us` `` .

  > **Note:** You must use [a region qualifier](https://docs.cloud.google.com/bigquery/docs/information-schema-intro#region_qualifier) to query `INFORMATION_SCHEMA` views. The location of the query execution must match the region of the `INFORMATION_SCHEMA` view.

> **Note:** When you query `INFORMATION_SCHEMA.JOBS_BY_USER` to find a summary cost of query jobs, exclude the `SCRIPT` statement type, otherwise some values might be counted twice. The `SCRIPT` row includes summary values for all child jobs that were executed as part of this job.

## Examples

To run the query against a project other than your default project, add the project ID in the following format:

```
`PROJECT_ID`.`region-REGION_NAME`.INFORMATION_SCHEMA.JOBS_BY_USER
```

Replace the following:

- `PROJECT_ID` : the ID of the project
- `REGION_NAME` : the region for your project

For example, `` `myproject`.`region-us`.INFORMATION_SCHEMA.JOBS_BY_USER `` .

### View pending or running jobs

The following query displays the job ID, creation time, and query of all pending or running jobs submitted by the current user in the designated project:

```
SELECT
  job_id,
  creation_time,
  query
FROM
  `region-REGION_NAME`.INFORMATION_SCHEMA.JOBS_BY_USER
WHERE
  state != 'DONE';
```

> **Note:** `INFORMATION_SCHEMA` view names are case-sensitive.

The result is similar to the following:

```
+--------------+---------------------------+---------------------------------+
| job_id       |  creation_time            |  query                          |
+--------------+---------------------------+---------------------------------+
| bquxjob_1    |  2019-10-10 00:00:00 UTC  |  SELECT ... FROM dataset.table1 |
| bquxjob_2    |  2019-10-10 00:00:01 UTC  |  SELECT ... FROM dataset.table2 |
| bquxjob_3    |  2019-10-10 00:00:02 UTC  |  SELECT ... FROM dataset.table3 |
+--------------+---------------------------+---------------------------------+
```
