# JOBS\_TIMELINE\_BY\_USER view

The `  INFORMATION_SCHEMA.JOBS_TIMELINE_BY_USER  ` view contains near real-time BigQuery metadata by timeslice of the jobs submitted by the current user in the current project. This view contains currently running and completed jobs.

## Required permissions

To query the `  INFORMATION_SCHEMA.JOBS_TIMELINE_BY_USER  ` view, you need the `  bigquery.jobs.list  ` Identity and Access Management (IAM) permission for the project. Each of the following predefined IAM roles includes the required permission:

  - Project Viewer
  - BigQuery User

For more information about BigQuery permissions, see [Access control with IAM](/bigquery/docs/access-control) .

## Schema

When you query the `  INFORMATION_SCHEMA.JOBS_TIMELINE_BY_*  ` views, the query results contain one row for every second of execution of every BigQuery job. Each period starts on a whole-second interval and lasts exactly one second.

The `  INFORMATION_SCHEMA.JOBS_TIMELINE_BY_*  ` view has the following schema:

**Note:** The underlying data is partitioned by the `  job_creation_time  ` column and clustered by `  project_id  ` and `  user_email  ` .

<table>
<thead>
<tr class="header">
<th>Column name</th>
<th>Data type</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       period_start      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>Start time of this period.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       period_slot_ms      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>Slot milliseconds consumed in this period.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       project_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><em>(Clustering column)</em> ID of the project.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       project_number      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>Number of the project.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       user_email      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><em>(Clustering column)</em> Email address or service account of the user who ran the job.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       principal_subject      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>A string representation of the identity of the principal that ran the job.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       job_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>ID of the job. For example, <code dir="ltr" translate="no">       bquxjob_1234      </code> .</td>
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
<td><code dir="ltr" translate="no">       statement_type      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The type of query statement, if valid. For example, <code dir="ltr" translate="no">       SELECT      </code> , <code dir="ltr" translate="no">       INSERT      </code> , <code dir="ltr" translate="no">       UPDATE      </code> , or <code dir="ltr" translate="no">       DELETE      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       priority      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The priority of this job. Valid values include <code dir="ltr" translate="no">       INTERACTIVE      </code> and <code dir="ltr" translate="no">       BATCH      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       parent_job_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>ID of the parent job, if any.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       job_creation_time      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td><em>(Partitioning column)</em> Creation time of this job. Partitioning is based on the UTC time of this timestamp.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       job_start_time      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>Start time of this job.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       job_end_time      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>End time of this job.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       state      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Running state of the job at the end of this period. Valid states include <code dir="ltr" translate="no">       PENDING      </code> , <code dir="ltr" translate="no">       RUNNING      </code> , and <code dir="ltr" translate="no">       DONE      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       reservation_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Name of the primary reservation assigned to this job at the end of this period, if applicable.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       edition      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The edition associated with the reservation assigned to this job. For more information about editions, see <a href="/bigquery/docs/editions-intro">Introduction to BigQuery editions</a> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       total_bytes_billed      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>If the project is configured to use <a href="https://cloud.google.com/bigquery/pricing#analysis_pricing_models">on-demand pricing</a> , then this field contains the total bytes billed for the job. If the project is configured to use <a href="https://cloud.google.com/bigquery/pricing#analysis_pricing_models">flat-rate pricing</a> , then you are not billed for bytes and this field is informational only. This field is only populated for completed jobs and contains the total number of bytes billed for the entire duration of the job.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       total_bytes_processed      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>Total bytes processed by the job. This field is only populated for completed jobs and contains the total number of bytes processed over the entire duration of the job.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       error_result      </code></td>
<td><code dir="ltr" translate="no">       RECORD      </code></td>
<td>Details of error (if any) as an <code dir="ltr" translate="no">         ErrorProto              .      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       cache_hit      </code></td>
<td><code dir="ltr" translate="no">       BOOLEAN      </code></td>
<td>Whether the query results of this job were from a cache.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       period_shuffle_ram_usage_ratio      </code></td>
<td><code dir="ltr" translate="no">       FLOAT      </code></td>
<td>Shuffle usage ratio in the selected time period. The value is <code dir="ltr" translate="no">       0.0      </code> if the job ran with a reservation that uses autoscaling and has zero baseline slots.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       period_estimated_runnable_units      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>Units of work that can be scheduled immediately in this period. Additional slots for these units of work accelerate your query, provided no other query in the reservation needs additional slots.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       transaction_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>ID of the <a href="/bigquery/docs/transactions">transaction</a> in which this job ran, if any.</td>
</tr>
</tbody>
</table>

For stability, we recommend that you explicitly list columns in your information schema queries instead of using a wildcard ( `  SELECT *  ` ). Explicitly listing columns prevents queries from breaking if the underlying schema changes.

## Data retention

This view displays running jobs along with job history for the past 180 days. If a project migrates to an organization (either from having no organization or from a different one), job information predating the migration date isn't accessible through the `  INFORMATION_SCHEMA.JOBS_TIMELINE_BY_USER  ` view, as the view only retains data starting from the migration date.

## Scope and syntax

Queries against this view must include a [region qualifier](/bigquery/docs/information-schema-intro#syntax) . If you do not specify a regional qualifier, metadata is retrieved from all regions. The following table explains the region and resource scope for this view:

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
<td><code dir="ltr" translate="no">       [               PROJECT_ID              .]`region-               REGION              `.INFORMATION_SCHEMA.JOBS_TIMELINE_BY_USER      </code></td>
<td>Jobs submitted by the current user in the specified project.</td>
<td><code dir="ltr" translate="no">         REGION       </code></td>
</tr>
</tbody>
</table>

Replace the following:

  - Optional: `  PROJECT_ID  ` : the ID of your Google Cloud project. If not specified, the default project is used.
  - `  REGION  ` : any [dataset region name](/bigquery/docs/locations) . For example, ``  `region-us`  `` .
    **Note:** You must use [a region qualifier](/bigquery/docs/information-schema-intro#region_qualifier) to query `  INFORMATION_SCHEMA  ` views. The location of the query execution must match the region of the `  INFORMATION_SCHEMA  ` view.

## Example

The following query displays the total slot milliseconds consumed per second by jobs submitted by the current user in the designated project:

``` text
SELECT
  period_start,
  SUM(period_slot_ms) AS total_period_slot_ms
FROM
  `region-us`.INFORMATION_SCHEMA.JOBS_TIMELINE_BY_USER
GROUP BY
  period_start
ORDER BY
  period_start DESC;
```

**Note:** `  INFORMATION_SCHEMA  ` view names are case-sensitive.

The result is similar to the following:

``` text
+---------------------------+---------------------------------+
|  period_start             |  total_period_slot_ms           |
+---------------------------+---------------------------------+
|  2019-10-10 00:00:04 UTC  |  118639                         |
|  2019-10-10 00:00:03 UTC  |  251353                         |
|  2019-10-10 00:00:02 UTC  |  1074064                        |
|  2019-10-10 00:00:01 UTC  |  1124868                        |
|  2019-10-10 00:00:00 UTC  |  1113961                        |
+---------------------------+---------------------------------+
```
