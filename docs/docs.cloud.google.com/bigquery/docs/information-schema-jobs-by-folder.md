# JOBS\_BY\_FOLDER view

The `  INFORMATION_SCHEMA.JOBS_BY_FOLDER  ` view contains near real-time metadata about all jobs submitted in the parent folder of the current project, including the jobs in subfolders under it.

## Required role

To get the permission that you need to query the `  INFORMATION_SCHEMA.JOBS_BY_FOLDER  ` view, ask your administrator to grant you the [BigQuery Resource Viewer](/iam/docs/roles-permissions/bigquery#bigquery.resourceViewer) ( `  roles/bigquery.resourceViewer  ` ) IAM role on your parent folder. For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

This predefined role contains the `  bigquery.jobs.listAll  ` permission, which is required to query the `  INFORMATION_SCHEMA.JOBS_BY_FOLDER  ` view.

You might also be able to get this permission with [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

For more information about BigQuery permissions, see [Access control with IAM](/bigquery/docs/access-control) .

## Schema

The underlying data is partitioned by the `  creation_time  ` column and clustered by `  project_id  ` and `  user_email  ` . The `  query_info  ` column contains additional information about your query jobs.

The `  INFORMATION_SCHEMA.JOBS_BY_FOLDER  ` view has the following schema:

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
<td><code dir="ltr" translate="no">       folder_numbers      </code></td>
<td><code dir="ltr" translate="no">       REPEATED INTEGER      </code></td>
<td>Number IDs of folders that contain the project, starting with the folder that immediately contains the project, followed by the folder that contains the child folder, and so forth. For example, if <code dir="ltr" translate="no">       folder_numbers      </code> is <code dir="ltr" translate="no">       [1, 2, 3]      </code> , then folder <code dir="ltr" translate="no">       1      </code> immediately contains the project, folder <code dir="ltr" translate="no">       2      </code> contains <code dir="ltr" translate="no">       1      </code> , and folder <code dir="ltr" translate="no">       3      </code> contains <code dir="ltr" translate="no">       2      </code> . This column is only populated in <code dir="ltr" translate="no">       JOBS_BY_FOLDER      </code> .</td>
</tr>
<tr class="odd">
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
<tr class="even">
<td><code dir="ltr" translate="no">       job_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The ID of the job if a job was created. Otherwise, the query ID of a query using optional job creation mode. For example, <code dir="ltr" translate="no">       bquxjob_1234      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       job_stages      </code></td>
<td><code dir="ltr" translate="no">       RECORD      </code></td>
<td><a href="https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#ExplainQueryStage">Query stages</a> of the job.
<p><strong>Note</strong> : This column's values are empty for queries that read from tables with row-level access policies. For more information, see <a href="/bigquery/docs/best-practices-row-level-security">best practices for row-level security in BigQuery.</a></p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       job_type      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The type of the job. Can be <code dir="ltr" translate="no">       QUERY      </code> , <code dir="ltr" translate="no">       LOAD      </code> , <code dir="ltr" translate="no">       EXTRACT      </code> , <code dir="ltr" translate="no">       COPY      </code> , or <code dir="ltr" translate="no">       NULL      </code> . A <code dir="ltr" translate="no">       NULL      </code> value indicates a background job.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       labels      </code></td>
<td><code dir="ltr" translate="no">       RECORD      </code></td>
<td>Array of labels applied to the job as key-value pairs.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       parent_job_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>ID of the parent job, if any.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       priority      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The priority of this job. Valid values include <code dir="ltr" translate="no">       INTERACTIVE      </code> and <code dir="ltr" translate="no">       BATCH      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       project_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>( <em>Clustering column</em> ) The ID of the project.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       project_number      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>The number of the project.</td>
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

For stability, we recommend that you explicitly list columns in your information schema queries instead of using a wildcard ( `  SELECT *  ` ). Explicitly listing columns prevents queries from breaking if the underlying schema changes.

## Data retention

This view displays running jobs along with job history for the past 180 days. If a project migrates to an organization (either from having no organization or from a different one), job information predating the migration date isn't accessible through the `  INFORMATION_SCHEMA.JOBS_BY_FOLDER  ` view, as the view only retains data starting from the migration date.

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
<td><code dir="ltr" translate="no">       [               PROJECT_ID              .]`region-               REGION              `.INFORMATION_SCHEMA.JOBS_BY_FOLDER      </code></td>
<td>Folder that contains the specified project</td>
<td><code dir="ltr" translate="no">         REGION       </code></td>
</tr>
</tbody>
</table>

Replace the following:

  - Optional: `  PROJECT_ID  ` : the ID of your Google Cloud project. If not specified, the default project is used.
  - `  REGION  ` : any [dataset region name](/bigquery/docs/locations) . For example, ``  `region-us`  `` .
    **Note:** You must use [a region qualifier](/bigquery/docs/information-schema-intro#region_qualifier) to query `  INFORMATION_SCHEMA  ` views. The location of the query execution must match the region of the `  INFORMATION_SCHEMA  ` view.

**Note:** When you query `  INFORMATION_SCHEMA.JOBS_BY_FOLDER  ` to find a summary cost of query jobs, you should exclude the `  SCRIPT  ` statement type, otherwise some values might be counted twice. The `  SCRIPT  ` row includes summary values for all child jobs that were executed as part of this job.

## Examples

To run the query against a project other than your default project, add the project ID in the following format:

``` text
`PROJECT_ID`.`region-REGION_NAME`.INFORMATION_SCHEMA.JOBS_BY_FOLDER
```

Replace the following:

  - `  PROJECT_ID  ` : the ID of the project
  - `  REGION_NAME  ` : the region for your project

For example, ``  `myproject`.`region-us`.INFORMATION_SCHEMA.JOBS_BY_FOLDER  `` .

### View interactive jobs

The following query displays the job ID, creation time, and state ( `  PENDING  ` , `  RUNNING  ` , or `  DONE  ` ) of all interactive jobs in the designated project's folder:

``` text
SELECT
  job_id,
  creation_time,
  state
FROM
  `region-REGION_NAME`.INFORMATION_SCHEMA.JOBS_BY_FOLDER
WHERE
  priority = 'INTERACTIVE';
```

**Note:** `  INFORMATION_SCHEMA  ` view names are case-sensitive.

The result is similar to the following:

``` text
+--------------+---------------------------+---------------------------------+
| job_id       |  creation_time            |  state                          |
+--------------+---------------------------+---------------------------------+
| bquxjob_1    |  2019-10-10 00:00:00 UTC  |  DONE                           |
| bquxjob_4    |  2019-10-10 00:00:03 UTC  |  RUNNING                        |
| bquxjob_5    |  2019-10-10 00:00:04 UTC  |  PENDING                        |
+--------------+---------------------------+---------------------------------+
```
