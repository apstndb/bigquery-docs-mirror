# JOBS view

The `  INFORMATION_SCHEMA.JOBS  ` view contains near real-time metadata about all BigQuery jobs in the current project.

**Note:** The view names `  INFORMATION_SCHEMA.JOBS  ` and `  INFORMATION_SCHEMA.JOBS_BY_PROJECT  ` are synonymous and can be used interchangeably.

## Required role

To get the permission that you need to query the `  INFORMATION_SCHEMA.JOBS  ` view, ask your administrator to grant you the [BigQuery Resource Viewer](/iam/docs/roles-permissions/bigquery#bigquery.resourceViewer) ( `  roles/bigquery.resourceViewer  ` ) IAM role on your project. For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

This predefined role contains the `  bigquery.jobs.listAll  ` permission, which is required to query the `  INFORMATION_SCHEMA.JOBS  ` view.

You might also be able to get this permission with [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

For more information about BigQuery permissions, see [Access control with IAM](/bigquery/docs/access-control) .

## Schema

The underlying data is partitioned by the `  creation_time  ` column and clustered by `  project_id  ` and `  user_email  ` . The `  query_info  ` column contains additional information about your query jobs.

The `  INFORMATION_SCHEMA.JOBS  ` view has the following schema:

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
<td><code dir="ltr" translate="no">       bi_engine_statistics      </code></td>
<td><code dir="ltr" translate="no">       RECORD      </code></td>
<td>If the project is configured to use the <a href="https://cloud.google.com/bigquery/docs/bi-engine-intro">BI Engine</a> , then this field contains <a href="https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#bienginestatistics">BiEngineStatistics</a> . Otherwise <code dir="ltr" translate="no">       NULL      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       cache_hit      </code></td>
<td><code dir="ltr" translate="no">       BOOLEAN      </code></td>
<td>Whether the query results of this job were from a cache. If you have a <a href="/bigquery/docs/multi-statement-queries">multi-query statement job</a> , <code dir="ltr" translate="no">       cache_hit      </code> for your parent query is <code dir="ltr" translate="no">       NULL      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       creation_time      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>( <em>Partitioning column</em> ) Creation time of this job. Partitioning is based on the UTC time of this timestamp.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       destination_table      </code></td>
<td><code dir="ltr" translate="no">       RECORD      </code></td>
<td>Destination <a href="https://cloud.google.com/bigquery/docs/reference/rest/v2/TableReference">table</a> for results, if any.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       dml_statistics      </code></td>
<td><code dir="ltr" translate="no">       RECORD      </code></td>
<td>If the job is a query with a DML statement, the value is a record with the following fields:<br />

<ul>
<li><code dir="ltr" translate="no">         inserted_row_count        </code> : The number of rows that were inserted.</li>
<li><code dir="ltr" translate="no">         deleted_row_count        </code> : The number of rows that were deleted.</li>
<li><code dir="ltr" translate="no">         updated_row_count        </code> : The number of rows that were updated.</li>
</ul>
For all other jobs, the value is <code dir="ltr" translate="no">       NULL      </code> .<br />
This column is present in the <code dir="ltr" translate="no">       INFORMATION_SCHEMA.JOBS_BY_USER      </code> and <code dir="ltr" translate="no">       INFORMATION_SCHEMA.JOBS_BY_PROJECT      </code> views.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       end_time      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>The end time of this job, in milliseconds since the epoch. This field represents the time when the job enters the <code dir="ltr" translate="no">       DONE      </code> state.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       error_result      </code></td>
<td><code dir="ltr" translate="no">       RECORD      </code></td>
<td>Details of any errors as <a href="https://cloud.google.com/bigquery/docs/reference/rest/v2/ErrorProto">ErrorProto</a> objects.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       job_creation_reason.code      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Specifies the high level reason why a job was created.<br />
Possible values are:
<ul>
<li><code dir="ltr" translate="no">         REQUESTED        </code> : job creation was requested.</li>
<li><code dir="ltr" translate="no">         LONG_RUNNING        </code> : the query request ran beyond a system defined timeout specified by the <a href="/bigquery/docs/reference/rest/v2/jobs/query#queryrequest">timeoutMs field in the <code dir="ltr" translate="no">          QueryRequest         </code></a> . As a result it was considered a long running operation for which a job was created.</li>
<li><code dir="ltr" translate="no">         LARGE_RESULTS        </code> : the results from the query cannot fit in the in-line response.</li>
<li><code dir="ltr" translate="no">         OTHER        </code> : the system has determined that the query needs to be executed as a job.</li>
</ul></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       job_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The ID of the job if a job was created. Otherwise, the query ID of a query using optional job creation mode. For example, <code dir="ltr" translate="no">       bquxjob_1234      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       job_stages      </code></td>
<td><code dir="ltr" translate="no">       RECORD      </code></td>
<td><a href="https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#ExplainQueryStage">Query stages</a> of the job.
<p><strong>Note</strong> : This column's values are empty for queries that read from tables with row-level access policies. For more information, see <a href="/bigquery/docs/best-practices-row-level-security">best practices for row-level security in BigQuery.</a></p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       job_type      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The type of the job. Can be <code dir="ltr" translate="no">       QUERY      </code> , <code dir="ltr" translate="no">       LOAD      </code> , <code dir="ltr" translate="no">       EXTRACT      </code> , <code dir="ltr" translate="no">       COPY      </code> , or <code dir="ltr" translate="no">       NULL      </code> . A <code dir="ltr" translate="no">       NULL      </code> value indicates a background job.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       labels      </code></td>
<td><code dir="ltr" translate="no">       RECORD      </code></td>
<td>Array of labels applied to the job as key-value pairs.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       parent_job_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>ID of the parent job, if any.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       priority      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The priority of this job. Valid values include <code dir="ltr" translate="no">       INTERACTIVE      </code> and <code dir="ltr" translate="no">       BATCH      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       project_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>( <em>Clustering column</em> ) The ID of the project.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       project_number      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>The number of the project.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       query      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>SQL query text.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       referenced_tables      </code></td>
<td><code dir="ltr" translate="no">       RECORD      </code></td>
<td>Array of <code dir="ltr" translate="no">       STRUCT      </code> values that contain the following <code dir="ltr" translate="no">       STRING      </code> fields for each table referenced by the query: <code dir="ltr" translate="no">       project_id      </code> , <code dir="ltr" translate="no">       dataset_id      </code> , and <code dir="ltr" translate="no">       table_id      </code> . Only populated for query jobs that are not cache hits.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       reservation_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Name of the primary reservation assigned to this job, in the format <code dir="ltr" translate="no">       RESERVATION_ADMIN_PROJECT:RESERVATION_LOCATION.RESERVATION_NAME      </code> .<br />
In this output:
<ul>
<li><code dir="ltr" translate="no">         RESERVATION_ADMIN_PROJECT        </code> : the name of the Google Cloud project that administers the reservation</li>
<li><code dir="ltr" translate="no">         RESERVATION_LOCATION        </code> : the location of the reservation</li>
<li><code dir="ltr" translate="no">         RESERVATION_NAME        </code> : the name of the reservation</li>
</ul></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       edition      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The edition associated with the reservation assigned to this job. For more information about editions, see <a href="/bigquery/docs/editions-intro">Introduction to BigQuery editions</a> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       session_info      </code></td>
<td><code dir="ltr" translate="no">       RECORD      </code></td>
<td>Details about the <a href="https://cloud.google.com/bigquery/docs/sessions-intro">session</a> in which this job ran, if any.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       start_time      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>The start time of this job, in milliseconds since the epoch. This field represents the time when the job transitions from the <code dir="ltr" translate="no">       PENDING      </code> state to either <code dir="ltr" translate="no">       RUNNING      </code> or <code dir="ltr" translate="no">       DONE      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       state      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Running state of the job. Valid states include <code dir="ltr" translate="no">       PENDING      </code> , <code dir="ltr" translate="no">       RUNNING      </code> , and <code dir="ltr" translate="no">       DONE      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       statement_type      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The type of query statement. For example, <code dir="ltr" translate="no">       DELETE      </code> , <code dir="ltr" translate="no">       INSERT      </code> , <code dir="ltr" translate="no">       SCRIPT      </code> , <code dir="ltr" translate="no">       SELECT      </code> , or <code dir="ltr" translate="no">       UPDATE      </code> . See <a href="https://cloud.google.com/bigquery/docs/reference/auditlogs/rest/Shared.Types/BigQueryAuditMetadata.QueryStatementType">QueryStatementType</a> for list of valid values.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       timeline      </code></td>
<td><code dir="ltr" translate="no">       RECORD      </code></td>
<td><a href="https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#QueryTimelineSample">Query timeline</a> of the job. Contains snapshots of query execution.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       total_bytes_billed      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>If the project is configured to use <a href="https://cloud.google.com/bigquery/pricing#analysis_pricing_models">on-demand pricing</a> , then this field contains the total bytes billed for the job. If the project is configured to use <a href="https://cloud.google.com/bigquery/pricing#analysis_pricing_models">flat-rate pricing</a> , then you are not billed for bytes and this field is informational only.
<p><strong>Note</strong> : This column's values are empty for queries that read from tables with row-level access policies. For more information, see <a href="/bigquery/docs/best-practices-row-level-security">best practices for row-level security in BigQuery.</a></p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       total_bytes_processed      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td><p>Total bytes processed by the job.</p>
<p><strong>Note</strong> : This column's values are empty for queries that read from tables with row-level access policies. For more information, see <a href="/bigquery/docs/best-practices-row-level-security">best practices for row-level security in BigQuery.</a></p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       total_modified_partitions      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>The total number of partitions the job modified. This field is populated for <code dir="ltr" translate="no">       LOAD      </code> and <code dir="ltr" translate="no">       QUERY      </code> jobs.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       total_slot_ms      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>Slot milliseconds for the job over its entire duration in the <code dir="ltr" translate="no">       RUNNING      </code> state, including retries.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       total_services_sku_slot_ms      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>Total slot milliseconds for the job that runs on external services and is billed on the services SKU. This field is only populated for jobs that have external service costs, and is the total of the usage for costs whose billing method is <code dir="ltr" translate="no">       "SERVICES_SKU"      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       transaction_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>ID of the <a href="https://cloud.google.com/bigquery/docs/transactions">transaction</a> in which this job ran, if any.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       user_email      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>( <em>Clustering column</em> ) Email address or service account of the user who ran the job.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       principal_subject      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>A string representation of the identity of the principal that ran the job.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       query_info.resource_warning      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The warning message that appears if the resource usage during query processing is above the internal threshold of the system.<br />
A successful query job can have the <code dir="ltr" translate="no">       resource_warning      </code> field populated. With <code dir="ltr" translate="no">       resource_warning      </code> , you get additional data points to optimize your queries and to set up monitoring for performance trends of an equivalent set of queries by using <code dir="ltr" translate="no">       query_hashes      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       query_info.query_hashes.normalized_literals      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Contains the hash value of the query. <code dir="ltr" translate="no">       normalized_literals      </code> is a hexadecimal <code dir="ltr" translate="no">       STRING      </code> hash that ignores comments, parameter values, UDFs, and literals. The hash value will differ when underlying views change, or if the query implicitly references columns, such as <code dir="ltr" translate="no">       SELECT *      </code> , and the table schema changes.<br />
This field appears for successful <a href="/bigquery/docs/reference/standard-sql/query-syntax">GoogleSQL</a> queries that are not cache hits.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       query_info.performance_insights      </code></td>
<td><code dir="ltr" translate="no">       RECORD      </code></td>
<td><a href="https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#PerformanceInsights">Performance insights</a> for the job.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       query_info.optimization_details      </code></td>
<td><code dir="ltr" translate="no">       STRUCT      </code></td>
<td>The <a href="/bigquery/docs/history-based-optimizations">history-based optimizations</a> for the job. Only the <code dir="ltr" translate="no">       JOBS_BY_PROJECT      </code> view has this column.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       transferred_bytes      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>Total bytes transferred for cross-cloud queries, such as BigQuery Omni cross-cloud transfer jobs.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       materialized_view_statistics      </code></td>
<td><code dir="ltr" translate="no">       RECORD      </code></td>
<td><a href="/bigquery/docs/reference/rest/v2/Job#MaterializedViewStatistics">Statistics of materialized views</a> considered in a query job. ( <a href="https://cloud.google.com/products#product-launch-stages">Preview</a> )</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       metadata_cache_statistics      </code></td>
<td><code dir="ltr" translate="no">       RECORD      </code></td>
<td><a href="/bigquery/docs/reference/rest/v2/Job#metadatacachestatistics">Statistics for metadata column index usage for tables</a> referenced in a query job.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       search_statistics      </code></td>
<td><code dir="ltr" translate="no">       RECORD      </code></td>
<td><a href="/bigquery/docs/reference/rest/v2/Job#SearchStatistics">Statistics for a search query.</a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       query_dialect      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>This field will be available sometime in May, 2025. The query dialect used for the job. Valid values include:<br />

<ul>
<li><code dir="ltr" translate="no">         GOOGLE_SQL        </code> : Job was requested to use GoogleSQL.</li>
<li><code dir="ltr" translate="no">         LEGACY_SQL        </code> : Job was requested to use LegacySQL.</li>
<li><code dir="ltr" translate="no">         DEFAULT_LEGACY_SQL        </code> : No query dialect was specified in the job request. BigQuery used the default value of LegacySQL.</li>
<li><code dir="ltr" translate="no">         DEFAULT_GOOGLE_SQL        </code> : No query dialect was specified in the job request. BigQuery used the default value of GoogleSQL.</li>
</ul>
<br />
This field is only populated for query jobs. The default selection of query dialect can be controlled by the <a href="/bigquery/docs/default-configuration#configuration-settings">configuration settings</a> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       continuous      </code></td>
<td><code dir="ltr" translate="no">       BOOLEAN      </code></td>
<td>Whether the job is a <a href="https://cloud.google.com/bigquery/docs/continuous-queries-introduction">continuous query</a> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       continuous_query_info.output_watermark      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>Represents the point up to which the continuous query has successfully processed data.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       vector_search_statistics      </code></td>
<td><code dir="ltr" translate="no">       RECORD      </code></td>
<td><a href="/bigquery/docs/reference/rest/v2/Job#VectorSearchStatistics">Statistics for a vector search query.</a></td>
</tr>
</tbody>
</table>

When you query `  INFORMATION_SCHEMA.JOBS  ` to find a summary cost of query jobs, exclude the `  SCRIPT  ` statement type, otherwise some values might be counted twice. The `  SCRIPT  ` row includes summary values for all child jobs that were executed as part of this job.

For stability, we recommend that you explicitly list columns in your information schema queries instead of using a wildcard ( `  SELECT *  ` ). Explicitly listing columns prevents queries from breaking if the underlying schema changes.

## Multi-statement query jobs

A multi-statement query job is a query job that uses the [procedural language](/bigquery/docs/reference/standard-sql/procedural-language) . Multi-statement query jobs often define variables with `  DECLARE  ` or have control flow statements such as `  IF  ` or `  WHILE  ` . When you query `  INFORMATION_SCHEMA.JOBS  ` , you might need to recognize the difference between a multi-statement query job and other jobs. A multi-statement query job has the following traits:

  - `  statement_type  ` = `  SCRIPT  `
  - `  reservation_id  ` = `  NULL  `

### Child jobs

Each of a multi-statement query job's child jobs has a `  parent_job_id  ` pointing to the multi-statement query job itself. This includes summary values for all child jobs that were executed as part of this job.

If you query `  INFORMATION_SCHEMA.JOBS  ` to find a summary cost of query jobs, then you should exclude the `  SCRIPT  ` statement type. Otherwise, some values such as `  total_slot_ms  ` might be counted twice.

## Data retention

This view displays running jobs along with job history for the past 180 days. If a project migrates to an organization (either from having no organization or from a different one), job information predating the migration date isn't accessible through the `  INFORMATION_SCHEMA.JOBS  ` view, as the view only retains data starting from the migration date.

## Scope and syntax

Queries against this view must include a [region qualifier](/bigquery/docs/information-schema-intro#syntax) . The following table explains the region scope for this view:

<table>
<thead>
<tr class="header">
<th>View name</th>
<th>Resource scope</th>
<th>Region scope</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       [               PROJECT_ID              .]`region-               REGION              `.INFORMATION_SCHEMA.JOBS[_BY_PROJECT]      </code></td>
<td>Project level</td>
<td><code dir="ltr" translate="no">         REGION       </code></td>
</tr>
</tbody>
</table>

Replace the following:

  - Optional: `  PROJECT_ID  ` : the ID of your Google Cloud project. If not specified, the default project is used.
  - `  REGION  ` : any [dataset region name](/bigquery/docs/locations) . For example, ``  `region-us`  `` .
    **Note:** You must use [a region qualifier](/bigquery/docs/information-schema-intro#region_qualifier) to query `  INFORMATION_SCHEMA  ` views. The location of the query execution must match the region of the `  INFORMATION_SCHEMA  ` view.

## Examples

To run the query against a project other than your default project, add the project ID in the following format:

``` text
`PROJECT_ID`.`region-REGION_NAME`.INFORMATION_SCHEMA.JOBS
```

Replace the following:

  - `  PROJECT_ID  ` : the ID of the project.
  - `  REGION_NAME  ` : the region for your project.

For example, ``  `myproject`.`region-us-central1`.INFORMATION_SCHEMA.JOBS  `` .

### Compare on-demand job usage to billing data

For projects using [on-demand pricing](https://cloud.google.com/bigquery/pricing#on_demand_pricing) , you can use the `  INFORMATION_SCHEMA.JOBS  ` view to review compute charges over a given period.

For projects using [capacity-based (slots) pricing](https://cloud.google.com/bigquery/pricing#capacity_compute_analysis_pricing) , you can use the [`  INFORMATION_SCHEMA.RESERVATIONS_TIMELINE  `](/bigquery/docs/information-schema-reservation-timeline) to review compute charges over a given period.

The following query produces daily estimated aggregates of your billed TiB and the resulting charges. The [limitations](#limitations) section explains when these estimates may not match your bill.

For this example only, the following additional variables must be set. They can be edited here for ease of use.

  - `  START_DATE  ` : the earliest date to aggregate over (inclusive).
  - `  END_DATE  ` : the latest date to aggregate over (inclusive).
  - `  PRICE_PER_TIB  ` : the [on-demand price per TiB](https://cloud.google.com/bigquery/pricing#on_demand_pricing) used for bill estimates.

<!-- end list -->

``` text
CREATE TEMP FUNCTION isBillable(error_result ANY TYPE)
AS (
  -- You aren't charged for queries that return an error.
  error_result IS NULL
  -- However, canceling a running query might incur charges.
  OR error_result.reason = 'stopped'
);

-- BigQuery hides the number of bytes billed on all queries against tables with
-- row-level security.
CREATE TEMP FUNCTION isMaybeUsingRowLevelSecurity(
  job_type STRING, tib_billed FLOAT64, error_result ANY TYPE)
AS (
  job_type = 'QUERY'
  AND tib_billed IS NULL
  AND isBillable(error_result)
);

WITH
  query_params AS (
    SELECT
      date 'START_DATE' AS start_date,  -- inclusive
      date 'END_DATE' AS end_date,  -- inclusive
  ),
  usage_with_multiplier AS (
    SELECT
      job_type,
      error_result,
      creation_time,
      -- Jobs are billed by end_time in PST8PDT timezone, regardless of where
      -- the job ran.
      EXTRACT(date FROM end_time AT TIME ZONE 'PST8PDT') billing_date,
      total_bytes_billed / 1024 / 1024 / 1024 / 1024 total_tib_billed,
      CASE statement_type
        WHEN 'SCRIPT' THEN 0
        WHEN 'CREATE_MODEL' THEN 50 * PRICE_PER_TIB
        ELSE PRICE_PER_TIB
        END AS multiplier,
    FROM `region-REGION_NAME`.INFORMATION_SCHEMA.JOBS
    WHERE statement_type <> 'SCRIPT'
  )
SELECT
  billing_date,
  sum(total_tib_billed * multiplier) estimated_charge,
  sum(total_tib_billed) estimated_usage_in_tib,
  countif(isMaybeUsingRowLevelSecurity(job_type, total_tib_billed, error_result))
    AS jobs_using_row_level_security,
FROM usage_with_multiplier, query_params
WHERE
  1 = 1
  -- Filter by creation_time for partition pruning.
  AND date(creation_time) BETWEEN date_sub(start_date, INTERVAL 2 day) AND date_add(end_date, INTERVAL 1 day)
  AND billing_date BETWEEN start_date AND end_date
  AND isBillable(error_result)
GROUP BY billing_date
ORDER BY billing_date;
```

#### Limitations

  - BigQuery [hides some statistics](/bigquery/docs/best-practices-row-level-security#limit-side-channel-attacks) for queries over tables with row-level security. The provided query counts the number of jobs impacted as `  jobs_using_row_level_security  ` , but does not have access to the billable usage.

  - BigQuery ML [pricing for on-demand queries](https://cloud.google.com/bigquery/pricing#ml_on_demand_pricing) depends on the type of model being created. `  INFORMATION_SCHEMA.JOBS  ` does not track which type of model was created, so the provided query assumes all CREATE\_MODEL statements were creating the higher billed model types.

  - Apache Spark procedures use a [similar pricing model](/bigquery/docs/spark-procedures#pricing) , but charges are reported as [BigQuery Enterprise edition pay-as-you-go SKU](https://cloud.google.com/bigquery/pricing#capacity_compute_analysis_pricing) . `  INFORMATION_SCHEMA.JOBS  ` tracks this usage as `  total_bytes_billed  ` , but cannot determine which SKU the usage represents.

### Calculate average slot utilization

The following example calculates average slot utilization for all queries over the past 7 days for a given project. Note that this calculation is most accurate for projects that have consistent slot usage throughout the week. If your project does not have consistent slot usage, this number might be lower than expected.

To run the query:

``` text
SELECT
  SUM(total_slot_ms) / (1000 * 60 * 60 * 24 * 7) AS avg_slots
FROM
  `region-REGION_NAME`.INFORMATION_SCHEMA.JOBS
WHERE
  -- Filter by the partition column first to limit the amount of data scanned.
  -- Eight days allows for jobs created before the 7 day end_time filter.
  creation_time BETWEEN TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 8 DAY) AND CURRENT_TIMESTAMP()
  AND job_type = 'QUERY'
  AND statement_type != 'SCRIPT'
  AND end_time BETWEEN TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 7 DAY) AND CURRENT_TIMESTAMP();
```

**Note:** `  INFORMATION_SCHEMA  ` view names are case-sensitive.

The result is similar to the following:

``` text
+------------+
| avg_slots  |
+------------+
| 3879.1534  |
+------------+
```

You can check usage for a particular reservation with `  WHERE reservation_id = "…"  ` . This can be helpful to determine percentage use of a reservation over a period of time. For script jobs, the parent job also reports the total slot usage from its children jobs. To avoid double counting, use `  WHERE statement_type != "SCRIPT"  ` to exclude the parent job.

If instead you would like to check the average slot utilization for individual jobs, use `  total_slot_ms / TIMESTAMP_DIFF(end_time, start_time, MILLISECOND)  ` .

### Count recent active queries by query priority

The following example displays the number of queries, grouped by priority (interactive or batch) that were started within the last 7 hours:

``` text
SELECT
  priority,
  COUNT(*) active_jobs
FROM
  `region-REGION_NAME`.INFORMATION_SCHEMA.JOBS
WHERE
  creation_time > TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 7 hour)
  AND job_type = 'QUERY'
GROUP BY priority;
```

The result is similar to the following:

``` text
+-------------+-------------+
| priority    | active_jobs |
+-------------+-------------+
| INTERACTIVE |           2 |
| BATCH       |           3 |
+-------------+-------------+
```

The `  priority  ` field indicates whether a query is `  INTERACTIVE  ` or `  BATCH  ` .

### View load job history

The following example lists all users or service accounts that submitted a batch load job for a given project. Because no time boundary is specified, this query scans all available history.

``` text
SELECT
  user_email AS user,
  COUNT(*) num_jobs
FROM
  `region-REGION_NAME`.INFORMATION_SCHEMA.JOBS
WHERE
  job_type = 'LOAD'
GROUP BY
  user_email;
```

**Note:** `  INFORMATION_SCHEMA  ` view names are case-sensitive.

The result is similar to the following:

``` text
+--------------+
| user         |
+--------------+
| abc@xyz.com  |
| xyz@xyz.com  |
| bob@xyz.com  |
+--------------+
```

### Get the number of load jobs to determine the daily job quota used

The following example returns the number of jobs by day, dataset, and table so that you can determine how much of the daily job quota is used.

``` text
SELECT
    DATE(creation_time) as day,
    destination_table.project_id as project_id,
    destination_table.dataset_id as dataset_id,
    destination_table.table_id as table_id,
    COUNT(job_id) AS load_job_count
 FROM
   `region-REGION_NAME`.INFORMATION_SCHEMA.JOBS
 WHERE
    creation_time BETWEEN TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 8 DAY) AND CURRENT_TIMESTAMP()
    AND job_type = "LOAD"
GROUP BY
    day,
    project_id,
    dataset_id,
    table_id
ORDER BY
    day DESC;
```

**Note:** `  INFORMATION_SCHEMA  ` view names are case-sensitive.

The result is similar to the following:

``` text
+-------------+------------+-------------+----------+-----------------+
|day          | project_id | dataset_id  | table_id | load_job_count  |
+-------------+------------+-------------+----------+-----------------+
| 2020-10-10  | my_project | dataset1    | orders   | 58              |
| 2020-10-10  | my_project | dataset1    | product  | 20              |
| 2020-10-10  | my_project | dataset1    | sales    | 11              |
+-------------+------------+-------------+----------+-----------------+
```

### Get the last few failed jobs

The following example shows the last three failed jobs:

``` text
SELECT
   job_id,
  creation_time,
  user_email,
   error_result
 FROM `region-REGION_NAME`.INFORMATION_SCHEMA.JOBS_BY_PROJECT
WHERE
  error_result.reason != "Null"
ORDER BY
  creation_time DESC
LIMIT 3;
```

The results should look similar to the following:

``` text
+------------+--------------------------+------------------+-------------------------------------+
| job_id     | creation_time            | user_email       | error_result                        |
+------------+--------------------------+------------------+-------------------------------------+
| bquxjob_1  | 2020-10-10 00:00:00 UTC  | abc@example.com  | Column 'col1' has mismatched type...|
| bquxjob_2  | 2020-10-11 00:00:00 UTC  | xyz@example.com  | Column 'col1' has mismatched type...|
| bquxjob_3  | 2020-10-11 00:00:00 UTC  | bob@example.com  | Column 'col1' has mismatched type...|
+------------+--------------------------+------------------+-------------------------------------+
```

### Query the list of long running jobs

The following example shows the list of long running jobs that are in the `  RUNNING  ` or `  PENDING  ` state for more than 30 minutes:

``` text
SELECT
  job_id,
  job_type,
  state,
  creation_time,
  start_time,
  user_email
 FROM `region-REGION_NAME`.INFORMATION_SCHEMA.JOBS
 WHERE
  state!="DONE" AND
  creation_time <= TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 30 MINUTE)
ORDER BY
  creation_time ASC;
```

The result is similar to the following:

``` text
+-----------+----------+---------+--------------------------------+--------------------------------+------------------+
| job_id    | job_type | state   | creation_time                  | start_time                     | user_email       |
+-----------+----------+---------+--------------------------------+--------------------------------+------------------+
| bquxjob_1 | QUERY    | RUNNING | 2023-05-03 05:07:22.818000 UTC | 2023-05-03 05:07:22.905000 UTC | abc@example.com  |
| bquxjob_2 | QUERY    | PENDING | 2023-05-01 02:05:47.925000 UTC | 2023-05-01 02:05:47.998000 UTC | xyz@example.com  |
| bquxjob_3 | QUERY    | PENDING | 2023-05-01 02:05:47.925000 UTC | 2023-05-01 02:05:47.998000 UTC | abc@example.com  |
+-----------+----------+---------+--------------------------------+--------------------------------+------------------+
```

### Queries using optional job creation mode

The following example shows a list of queries that were executed in optional job creation mode for which BigQuery did not create jobs.

``` text
SELECT
 job_id,
FROM
 `region-REGION_NAME`.INFORMATION_SCHEMA.JOBS
WHERE
 TIMESTAMP_TRUNC(creation_time, DAY) = '2024-06-12'
 AND job_creation_reason.code IS NULL
LIMIT 3;
```

The results should look like the following:

``` text
+-----------+
| job_id    |                                          |
+-----------+
| bquxjob_1 |
| bquxjob_2 |
| bquxjob_3 |
+-----------+
```

The following example shows information about a query that was executed in optional job creation mode for which BigQuery did not create a job.

``` text
SELECT
 job_id,
 statement_type,
 priority,
 cache_hit,
 job_creation_reason.code AS job_creation_reason_code,
 total_bytes_billed,
 total_bytes_processed,
 total_slot_ms,
 state,
 error_result.message AS error_result_message,
FROM
 `region-REGION_NAME`.INFORMATION_SCHEMA.JOBS
WHERE
 TIMESTAMP_TRUNC(creation_time, DAY) = '2024-06-12'
 AND job_id = '2Lm09bHxDEsoVK8zwzWJomLHU_Ud%1910479b151' -- queryId
```

**Note** : The `  job_id  ` field contains the `  queryId  ` of the query when a job was not created for this query.

The results should look like the following:

``` text
+-----------+----------------+-------------+-----------+--------------------------+--------------------+---------------------+---------------+-------+----------------------+
| job_id    | statement_type | priority    | cache_hit | job_creation_reason_code | total_bytes_billed | total_bytes_processed | total_slot_ms | state | error_result_message |
+-----------+----------------+-------------+-----------+--------------------------+--------------------+---------------------+---------------+-------+----------------------+
| bquxjob_1 | SELECT         | INTERACTIVE | false     | null                     | 161480704          | 161164718             | 3106          | DONE  | null                 |
+-----------+----------------+-------------+-----------+--------------------------+--------------------+---------------------+---------------+-------+----------------------+
```

The following example shows a list of queries that were executed in optional job creation mode for which BigQuery did create jobs.

``` text
SELECT
 job_id,
 job_creation_reason.code AS job_creation_reason_code
FROM
 `region-REGION_NAME`.INFORMATION_SCHEMA.JOBS
WHERE
 TIMESTAMP_TRUNC(creation_time, DAY) = '2024-06-12'
 AND job_creation_reason.code IS NOT NULL
 AND job_creation_reason.code != 'REQUESTED'
LIMIT 3
```

The results should look like the following:

``` text
+-----------+--------------------------+
| job_id    | job_creation_reason_code |
+-----------+--------------------------+
| bquxjob_1 | LARGE_RESULTS            |
| bquxjob_2 | LARGE_RESULTS            |
| bquxjob_3 | LARGE_RESULTS            |
+-----------+--------------------------+
```

### Bytes processed per user identity

The following example shows the total bytes billed for query jobs per user:

``` text
SELECT
  user_email,
  SUM(total_bytes_billed) AS bytes_billed
FROM
  `region-REGION_NAME`.INFORMATION_SCHEMA.JOBS
WHERE
  job_type = 'QUERY'
  AND statement_type != 'SCRIPT'
GROUP BY
  user_email;
```

**Note** : See the caveat for the `  total_bytes_billed  ` column in the schema documentation for the `  JOBS  ` views.

The results should look like the following:

``` text
+---------------------+--------------+
| user_email          | bytes_billed |
+---------------------+--------------+
| bob@example.com     | 2847932416   |
| alice@example.com   | 1184890880   |
| charles@example.com | 10485760     |
+---------------------+--------------+
```

### Aggregate Connected Sheets usage by user at the project level

If you don't have organization-level permissions or only need to monitor a specific project, run the following query to identify the top Connected Sheets users within a project over the last 30 days. The query aggregates the total number of queries, total bytes billed, and total slot milliseconds for each user. This information is useful for understanding adoption and for identifying top consumers of resources.

``` text
SELECT
  user_email,
  COUNT(*) AS total_queries,
  SUM(total_bytes_billed) AS total_bytes_billed,
  SUM(total_slot_ms) AS total_slot_ms
FROM
  -- This view queries the project you are currently running the query in.
  `region-REGION_NAME`.INFORMATION_SCHEMA.JOBS_BY_PROJECT
WHERE
  -- Filter for jobs created in the last 30 days
  creation_time >= TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 30 DAY)
  -- Filter for jobs originating from Connected Sheets
  AND job_id LIKE 'sheets_dataconnector%'
  -- Filter for completed jobs
  AND state = 'DONE'
  AND (statement_type IS NULL OR statement_type <> 'SCRIPT')
GROUP BY
  user_email
ORDER BY
  total_bytes_billed DESC
LIMIT
  10;
```

Replace `  REGION_NAME  ` with the region for your project. For example, `  region-us  ` .

**Note:** You must use a region qualifier to query `  INFORMATION_SCHEMA  ` views. The location of the query execution must match the region of the `  INFORMATION_SCHEMA  ` view.

The result looks similar to the following:

``` text
+---------------------+---------------+--------------------+-----------------+
| user_email          | total_queries | total_bytes_billed | total_slot_ms   |
+---------------------+---------------+--------------------+-----------------+
| alice@example.com   | 152           | 12000000000        | 3500000         |
| bob@example.com     | 45            | 8500000000         | 2100000         |
| charles@example.com | 210           | 1100000000         | 1800000         |
+---------------------+---------------+--------------------+-----------------+
```

### Find job logs of Connected Sheets queries at the project-level

If you don't have organization-level permissions or only need to monitor a specific project, run the following query to see a detailed log of all Connected Sheets queries for the current project:

``` text
SELECT
  job_id,
  creation_time,
  user_email,
  total_bytes_billed,
  total_slot_ms,
  query
FROM
  -- This view queries the project you are currently running the query in.
  `region-REGION_NAME.INFORMATION_SCHEMA.JOBS_BY_PROJECT`
WHERE
  creation_time >= TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 30 DAY)
  AND job_id LIKE 'sheets_dataconnector%'
  AND state = 'DONE'
  AND (statement_type IS NULL OR statement_type <> 'SCRIPT')
ORDER BY
  creation_time DESC;
```

Replace `  REGION_NAME  ` with the region for your project. For example, `  region-us  ` .

**Note:** You must use a region qualifier to query `  INFORMATION_SCHEMA  ` views. The location of the query execution must match the region of the `  INFORMATION_SCHEMA  ` view.

The result looks similar to the following:

``` text
+---------------------------------+---------------------------------+------------------+--------------------+-----------------+---------------------------------+
| job_id                          | creation_time                   | user_email       | total_bytes_billed | total_slot_ms   |  query                          |
+---------------------------------+---------------------------------+------------------+--------------------+-----------------+---------------------------------+
| sheets_dataconnector_bquxjob_1  | 2025-11-06 00:26:53.077000 UTC  | abc@example.com  | 12000000000        | 3500000         |  SELECT ... FROM dataset.table1 |
| sheets_dataconnector_bquxjob_2  | 2025-11-06 00:24:04.294000 UTC  | xyz@example.com  | 8500000000         | 2100000         |  SELECT ... FROM dataset.table2 |
| sheets_dataconnector_bquxjob_3  | 2025-11-03 23:17:25.975000 UTC  | bob@example.com  | 1100000000         | 1800000         |  SELECT ... FROM dataset.table3 |
+---------------------------------+---------------------------------+------------------+--------------------+-----------------+---------------------------------+
```

### Hourly breakdown of bytes processed

The following example shows total bytes billed for query jobs, in hourly intervals:

``` text
SELECT
  TIMESTAMP_TRUNC(end_time, HOUR) AS time_window,
  SUM(total_bytes_billed) AS bytes_billed
FROM
  `region-REGION_NAME`.INFORMATION_SCHEMA.JOBS
WHERE
  job_type = 'QUERY'
  AND statement_type != 'SCRIPT'
GROUP BY
  time_window
ORDER BY
  time_window DESC;
```

The result is similar to the following:

``` text
+-------------------------+--------------+
| time_window             | bytes_billed |
+-------------------------+--------------+
| 2022-05-17 20:00:00 UTC | 1967128576   |
| 2022-05-10 21:00:00 UTC | 0            |
| 2022-04-15 17:00:00 UTC | 41943040     |
+-------------------------+--------------+
```

### Query jobs per table

The following example shows how many times each table queried in `  my_project  ` was referenced by a query job:

``` text
SELECT
  t.project_id,
  t.dataset_id,
  t.table_id,
  COUNT(*) AS num_references
FROM
  `region-REGION_NAME`.INFORMATION_SCHEMA.JOBS, UNNEST(referenced_tables) AS t
GROUP BY
  t.project_id,
  t.dataset_id,
  t.table_id
ORDER BY
  num_references DESC;
```

The result is similar to the following:

``` text
+------------+------------+----------+----------------+
| project_id | dataset_id | table_id | num_references |
+------------+------------+----------+----------------+
| my_project | dataset1   | orders   | 58             |
| my_project | dataset1   | products | 40             |
| other_proj | dataset1   | accounts | 12             |
+------------+------------+----------+----------------+
```

### Legacy sql query jobs count per project

The 'query\_dialect' field in the INFORMATION\_SCHEMA has been available since May 2025. The following example shows how many legacy sql query jobs are executed by projects.

``` text
SELECT
  project_id,
  -- Implicitly defaulted to LegacySQL since the query dialect was not specified
  -- in the request.
  COUNTIF(query_dialect = 'DEFAULT_LEGACY_SQL') AS default_legacysql_query_jobs,
  -- Explicitly requested LegacySQL.
  COUNTIF(query_dialect = 'LEGACY_SQL') AS legacysql_query_jobs,
FROM
  `region-REGION_NAME`.INFORMATION_SCHEMA.JOBS
WHERE
  query_dialect = 'DEFAULT_LEGACY_SQL'
  OR query_dialect = 'LEGACY_SQL'
GROUP BY
  project_id
ORDER BY
  default_legacysql_query_jobs DESC,
  legacysql_query_jobs DESC;
```

### Number of partitions modified by query and load jobs per table

The following example shows the number of partitions modified by queries with DML statements and load jobs, per table. Note that this query doesn't show the `  total_modified_partitions  ` for copy jobs.

``` text
SELECT
  destination_table.table_id,
  SUM(total_modified_partitions) AS total_modified_partitions
FROM
  `region-REGION_NAME`.INFORMATION_SCHEMA.JOBS
WHERE
  DATE(creation_time, "America/Los_Angeles") = CURRENT_DATE()
GROUP BY
  table_id
ORDER BY
  total_modified_partitions DESC
```

### Average number of slots per millisecond used by a job

The following example shows how to calculate the average number of slots used by a job throughout the execution. This can be helpful when troubleshooting slow queries and comparing a slow execution of a query to a faster execution of the same query. Comparing this value with the total reservation size and the average number of concurrent jobs executed within the project or reservation can help you to understand whether multiple queries were competing for slots at the same time during the execution.

A higher average number of slots means more resources allocated to the job, which generally results in a faster execution.

``` text
SELECT ROUND(SAFE_DIVIDE(total_slot_ms,TIMESTAMP_DIFF(end_time, start_time, MILLISECOND)), 1) as avg_slots_per_ms
FROM `region-REGION_NAME`.INFORMATION_SCHEMA.JOBS_BY_PROJECT
WHERE job_id = 'JOB_ID'
```

Replace `  JOB_ID  ` with the `  job_id  ` you are investigating.

**Note:** `  INFORMATION_SCHEMA  ` view names are case-sensitive.

The result will be similar to the following:

``` text
+------------------+
| avg_slots_per_ms |
+------------------+
|             17.0 |
+------------------+
```

### Most expensive queries by project

The following example lists the most expensive queries in `  my_project  ` by slot usage time:

``` text
SELECT
 job_id,
 query,
 user_email,
 total_slot_ms
FROM `my_project`.`region-REGION_NAME`.INFORMATION_SCHEMA.JOBS
WHERE EXTRACT(DATE FROM  creation_time) = current_date()
ORDER BY total_slot_ms DESC
LIMIT 3
```

You can also list the most expensive queries by data processed with the following example:

``` text
SELECT
 job_id,
 query,
 user_email,
 total_bytes_processed
FROM `my_project`.`region-REGION_NAME`.INFORMATION_SCHEMA.JOBS
WHERE EXTRACT(DATE FROM  creation_time) = current_date()
ORDER BY total_bytes_processed DESC
LIMIT 3
```

The result for either example is similar to the following:

``` text
+-----------+---------------------------------+-----------------------+---------------+
| job_id    | query                           | user_email            | total_slot_ms |
+-----------+---------------------------------+-----------------------+---------------+
| bquxjob_1 | SELECT ... FROM dataset.table1  | bob@example.com       | 80,000        |
| bquxjob_2 | SELECT ... FROM dataset.table2  | alice@example.com     | 78,000        |
| bquxjob_3 | SELECT ... FROM dataset.table3  | charles@example.com   | 75,000        |
+-----------+---------------------------------+-----------------------+---------------+
```

### Get details about a resource warning

If you get a **Resources exceeded** error message, you can inquire about the queries in a time window:

``` text
SELECT
  query,
  query_info.resource_warning
FROM
  `region-REGION_NAME`.INFORMATION_SCHEMA.JOBS
WHERE
 creation_time BETWEEN TIMESTAMP("2022-12-01")
 AND TIMESTAMP("2022-12-08")
 AND query_info.resource_warning IS NOT NULL
LIMIT 3;
```

### Monitor resource warnings grouped by date

If you get a **Resources exceeded** error message, you can monitor the total number of resource warnings grouped by date to know if there are any changes to workload:

``` text
WITH resource_warnings AS (
  SELECT
    EXTRACT(DATE FROM creation_time) AS creation_date
  FROM
    `region-REGION_NAME`.INFORMATION_SCHEMA.JOBS
  WHERE
    creation_time >= TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 14 DAY)
    AND query_info.resource_warning IS NOT NULL
)
SELECT
  creation_date,
  COUNT(1) AS warning_counts
FROM
  resource_warnings
GROUP BY creation_date
ORDER BY creation_date DESC;
```

### Estimate slot usage and cost for queries

The following example computes the average slots and max slots for each job by using `  estimated_runnable_units  ` .

The `  reservation_id  ` is `  NULL  ` if you don't have any reservations.

``` text
SELECT
  project_id,
  job_id,
  reservation_id,
  EXTRACT(DATE FROM creation_time) AS creation_date,
  TIMESTAMP_DIFF(end_time, start_time, SECOND) AS job_duration_seconds,
  job_type,
  user_email,
  total_bytes_billed,

  -- Average slot utilization per job is calculated by dividing total_slot_ms by the millisecond duration of the job

  SAFE_DIVIDE(job.total_slot_ms,(TIMESTAMP_DIFF(job.end_time, job.start_time, MILLISECOND))) AS job_avg_slots,
  query,

  -- Determine the max number of slots used at ANY stage in the query.
  -- The average slots might be 55. But a single stage might spike to 2000 slots.
  -- This is important to know when estimating number of slots to purchase.

  MAX(SAFE_DIVIDE(unnest_job_stages.slot_ms,unnest_job_stages.end_ms - unnest_job_stages.start_ms)) AS jobstage_max_slots,

  -- Check if there's a job that requests more units of works (slots). If so you need more slots.
  -- estimated_runnable_units = Units of work that can be scheduled immediately.
  -- Providing additional slots for these units of work accelerates the query,
  -- if no other query in the reservation needs additional slots.

  MAX(unnest_timeline.estimated_runnable_units) AS estimated_runnable_units
FROM `region-REGION_NAME`.INFORMATION_SCHEMA.JOBS AS job
  CROSS JOIN UNNEST(job_stages) as unnest_job_stages
  CROSS JOIN UNNEST(timeline) AS unnest_timeline
WHERE
  DATE(creation_time) BETWEEN DATE_SUB(CURRENT_DATE(), INTERVAL 7 DAY) AND CURRENT_DATE()
  AND project_id = 'my_project'
  AND (statement_type != 'SCRIPT' OR statement_type IS NULL)
GROUP BY 1,2,3,4,5,6,7,8,9,10
ORDER BY job_id;
```

The result for example is similar to the following:

``` text
+-----------+-----------+----------------+---------------+----------------------+----------+-----------------+--------------------+--------------+--------------------------------+--------------------+--------------------------+
|project_id | job_id    | reservation_id | creation_date | job_duration_seconds | job_type | user_email      | total_bytes_billed | job_avg_slots| query                          | jobstage_max_slots | estimated_runnable_units |
+-----------+-----------+----------------+---------------+----------------------+----------+-----------------+--------------------+--------------+--------------------------------+--------------------+--------------------------+
| project1  | bquxjob1  | reservation1   | 2020-10-10    | 160                  | LOAD     | abc@example.com | 161480704          | 2890         | SELECT ... FROM dataset.table1 | 2779.1534          | 1000                     |
| project1  | bquxjob2  | reservation2   | 2020-12-10    | 120                  | LOAD     | abc@example.com | 161480704          | 2890         | SELECT ... FROM dataset.table1 | 2779.1534          | 1000                     |
| project1  | bquxjob3  | reservation1   | 2020-12-10    | 120                  | LOAD     | abc@example.com | 161480704          | 2890         | SELECT ... FROM dataset.table1 | 1279.1534          | 998                     |
+-----------+-----------+----------------+---------------+----------------------+----------+-----------------+--------------------+--------------+--------------------------------+--------------------+--------------------------+
```

### View performance insights for queries

The following example returns all query jobs that have performance insights from your project in the last 30 days, along with a URL that links to the query execution graph in the Google Cloud console.

``` text
SELECT
  `bigquery-public-data`.persistent_udfs.job_url(
    project_id || ':us.' || job_id) AS job_url,
  query_info.performance_insights
FROM
  `region-REGION_NAME`.INFORMATION_SCHEMA.JOBS_BY_PROJECT
WHERE
  DATE(creation_time) >= CURRENT_DATE - 30 -- scan 30 days of query history
  AND job_type = 'QUERY'
  AND state = 'DONE'
  AND error_result IS NULL
  AND statement_type != 'SCRIPT'
  AND EXISTS ( -- Only include queries which had performance insights
    SELECT 1
    FROM UNNEST(
      query_info.performance_insights.stage_performance_standalone_insights
    )
    WHERE
      slot_contention
      OR insufficient_shuffle_quota
      OR bi_engine_reasons IS NOT NULL
      OR high_cardinality_joins IS NOT NULL
      OR partition_skew IS NOT NULL
    UNION ALL
    SELECT 1
    FROM UNNEST(
      query_info.performance_insights.stage_performance_change_insights
    )
    WHERE input_data_change.records_read_diff_percentage IS NOT NULL
  );
```

### View metadata refresh jobs

The following example lists the metadata refresh jobs in last six hours:

``` text
SELECT
 *
FROM
 `region-REGION_NAME`.INFORMATION_SCHEMA.JOBS_BY_PROJECT
WHERE
 job_id LIKE '%metadata_cache_refresh%'
 AND creation_time > TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 6 HOUR)
ORDER BY start_time desc
LIMIT 10;
```

Replace REGION\_NAME with your region.

### Analyze performance over time for identical queries

The following example returns the top 10 slowest jobs over the past 7 days that have run the same query:

``` text
DECLARE querytext STRING DEFAULT(
  SELECT query
  FROM `region-REGION_NAME`.INFORMATION_SCHEMA.JOBS
  WHERE job_id = 'JOB_ID'
  LIMIT 1
);

SELECT
  start_time,
  end_time,
  project_id,
  job_id,
  TIMESTAMP_DIFF(end_time, start_time, SECOND) AS run_secs,
  total_bytes_processed / POW(1024, 3) AS total_gigabytes_processed,
  query
FROM
  `region-REGION_NAME`.INFORMATION_SCHEMA.JOBS
WHERE
  query = querytext
  AND total_bytes_processed > 0
  AND creation_time >= TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 7 DAY)
ORDER BY 5 DESC
LIMIT 3;
```

Replace `  JOB_ID  ` with any `  job_id  ` that ran the query you are analyzing.

### View jobs with slot contention insights

To view jobs with their slot contention insights, run the following query:

``` text
SELECT
  job_id,
  creation_time,
  query_info.performance_insights,
FROM
  `region-REGION_NAME`.INFORMATION_SCHEMA.JOBS j,
  UNNEST(query_info.performance_insights.stage_performance_standalone_insights) i
WHERE
  (j.statement_type != "SCRIPT" OR j.statement_type IS NULL)
  AND i IS NOT NULL
  AND i.slot_contention
```

The output shows different performance insights about jobs, including slot contention:

``` text
+------------+-------------------------+-------------------------------------------------+----------------------------------------------------------------------------+
| job_id     | creation_time           | performance_insights.avg_previous_execution_ms  | performance_insightsstage_performance_standalone_insights.slot_contention  |
+------------+-------------------------+-------------------------------------------------+----------------------------------------------------------------------------+
| bquxjob_1  | 2025-08-08 00:00:00 UTC | null                                            | true                                                                       |
| bquxjob_2  | 2025-08-08 00:00:00 UTC | 42689                                           | true                                                                       |
| bquxjob_3  | 2025-08-08 00:00:00 UTC | 42896                                           | true                                                                       |
+------------+-------------------------+-------------------------------------------------+----------------------------------------------------------------------------+
```

### Get jobs with the same query hash

The following query returns the job IDs with the same query hash as a specific job:

``` text
SELECT
  j.job_id,
  j.creation_time,
  j.query
FROM
  `region-REGION_NAME`.INFORMATION_SCHEMA.JOBS j
WHERE
  j.job_id != "JOB_IDENTIFIER"
  AND j.query_info.query_hashes.normalized_literals = (
    SELECT
      sub.query_info.query_hashes.normalized_literals
    FROM
      `region-REGION_NAME`.INFORMATION_SCHEMA.JOBS sub
    WHERE
      sub.job_id = "JOB_IDENTIFIER"
    LIMIT 1
  )
ORDER BY
  j.creation_time DESC;
```

**Note:** `  INFORMATION_SCHEMA  ` view names are case-sensitive.

The result is similar to the following:

``` text
+--------------+---------------------------+------------------------------------------------+
| job_id       |  creation_time            |  query                                         |
+--------------+---------------------------+------------------------------------------------+
| bquxjob_1    |  2019-10-10 00:00:00 UTC  |  SELECT ... FROM dataset.table1 WHERE x = "a"  |
| bquxjob_2    |  2019-10-10 00:00:01 UTC  |  SELECT ... FROM dataset.table1 WHERE x = "b"  |
| bquxjob_3    |  2019-10-10 00:00:02 UTC  |  SELECT ... FROM dataset.table1 WHERE x = "c"  |
+--------------+---------------------------+------------------------------------------------+
```

### View average concurrent jobs running alongside a particular job in the same project

The following example demonstrates how to calculate the average number of jobs running at the same time as a specific query job in the same project.

This calculation helps determine if an increased number of concurrent jobs within the same project caused [slot contention](/bigquery/docs/query-insights#slot_contention) problems. Gather this data when troubleshooting slow queries or comparing slow and fast query runs.

If there are far more concurrent queries running than expected, check if more jobs were started, queried data changed, or both.

``` text
WITH job_metadata AS (
 SELECT creation_time, end_time, job_type
 FROM `region-REGION_NAME`.INFORMATION_SCHEMA.JOBS_BY_PROJECT
 WHERE job_id = 'JOB_ID'
-- If you know the date the job was created, add the following line to speed up the query by providing the date in UTC:
-- AND DATE(creation_time) = 'YYYY-MM-DD'
),
intervals AS (
 SELECT TIMESTAMP_ADD(creation_time, INTERVAL (seconds_offset) SECOND) AS ts,
 job_type
 FROM job_metadata,
 UNNEST (GENERATE_ARRAY(0, IF(TIMESTAMP_DIFF(end_time, creation_time, SECOND) > 0, TIMESTAMP_DIFF(end_time, creation_time, SECOND), 1))) as seconds_offset
),
concurrent_jobs AS (
 SELECT int.ts, COUNT(*) as concurrent_jobs_count
 FROM intervals int JOIN
 `region-REGION_NAME`.INFORMATION_SCHEMA.JOBS_BY_PROJECT j
 ON int.ts BETWEEN j.creation_time and j.end_time
 WHERE job_id != 'JOB_ID'
 AND j.job_type = int.job_type
 GROUP BY int.ts)

SELECT ROUND(AVG(concurrent_jobs_count),1) as average_concurrent_jobs FROM concurrent_jobs
```

**Note:** The granularity for metadata aggregation is set to seconds. If you require a more precise granularity for shorter running jobs, replace `  SECOND  ` with `  MILLISECOND  ` in the query body for milliseconds sampling.

Replace the following:

  - `  JOB_ID  ` : the job ID of the query that you are analyzing

  - `  REGION_NAME  ` : the region for your project

The result is similar to the following:

``` text
+-------------------------+
| average_concurrent_jobs |
+-------------------------+
|                     2.8 |
+-------------------------+
```

### Get bytes processed by extract jobs

The following example computes the `  total_bytes_processed  ` value for `  EXTRACT  ` job types. For information about quotas for extract jobs, see [Quota policy for extract jobs](/bigquery/docs/exporting-data#quota_policy) . The total bytes processed can be used to monitor the aggregate usage and verify that extract jobs stays below the 50 TB per-day limit:

``` text
SELECT
    DATE(creation_time) as day,
    project_id as source_project_id,
    SUM(total_bytes_processed) AS total_bytes_processed
 FROM
   `region-REGION_NAME`.INFORMATION_SCHEMA.JOBS
 WHERE
    creation_time BETWEEN TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 8 DAY) AND CURRENT_TIMESTAMP()
    AND job_type = "EXTRACT"
GROUP BY
    day,
    source_project_id
ORDER BY
    day DESC;
```

### Get usage of copy jobs

For information about copy jobs, see [Copy a table](/bigquery/docs/managing-tables#copy-table) . The following example provides the usage of copy jobs:

``` text
SELECT
    DATE(creation_time) as day,
    project_id as source_project_id,
CONCAT(destination_table.project_id,":",destination_table.dataset_id,".",destination_table.table_id) as destination_table,
    COUNT(job_id) AS copy_job_count
 FROM
   `region-REGION_NAME`.INFORMATION_SCHEMA.JOBS
 WHERE
    creation_time BETWEEN TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 8 DAY) AND CURRENT_TIMESTAMP()
    AND job_type = "COPY"
GROUP BY
    day,
    source_project_id,
    destination_table
ORDER BY
    day DESC;
```

### Get usage of BigLake tables for Apache Iceberg in BigQuery storage optimization

The following example provides the usage of BigLake Iceberg table in BigQuery storage optimization.

``` text
SELECT
    job_id, reservation_id, edition,
    total_slot_ms, total_bytes_processed, state
FROM `region-REGION_NAME`.INFORMATION_SCHEMA.JOBS
WHERE creation_time > TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 6 HOUR)
    AND user_email = "bigquery-adminbot@system.gserviceaccount.com"
    AND query LIKE "CALL BQ.OPTIMIZE_STORAGE(%)";
```

### Get usage of BigLake Iceberg table in BigQuery export table metadata

The following example provides the usage of Iceberg `  EXPORT TABLE METADATA FROM  ` .

``` text
SELECT
   job_id,
   user_email,
   start_time,
   end_time,
   TIMESTAMP_DIFF(end_time, start_time, SECOND) AS duration_seconds,
   total_bytes_processed,
   reservation_id,
   CASE
     WHEN reservation_id IS NULL THEN 'PAYG (On-demand)'
     WHEN reservation_id != '' THEN 'Reservation'
     ELSE 'Unknown'
   END AS compute_type,
   query
 FROM
   `region-REGION_NAME`.INFORMATION_SCHEMA.JOBS
 WHERE
   job_type = 'QUERY'
   AND end_time IS NOT NULL
   -- Filter for queries containing the specified pattern (case-insensitive)
   AND REGEXP_CONTAINS(LOWER(query), r"export table metadata from")
 ORDER BY
   start_time DESC
 LIMIT 3;
```

### Match slot usage behavior from administrative resource charts

To explore slot usage behavior similar to the information in administrative resource charts, query the [`  INFORMATION_SCHEMA.JOBS_TIMELINE  ` view](/bigquery/docs/information-schema-jobs-timeline#charts_example) .
