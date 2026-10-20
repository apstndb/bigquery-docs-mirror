---
name: documents/docs.cloud.google.com/bigquery/docs/information-schema-jobs-timeline-by-user
uri: https://docs.cloud.google.com/bigquery/docs/information-schema-jobs-timeline-by-user
title: JOBS_TIMELINE_BY_USER view
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# JOBS_TIMELINE_BY_USER view

The `INFORMATION_SCHEMA.JOBS_TIMELINE_BY_USER` view contains near real-time BigQuery metadata by timeslice of the jobs submitted by the current user in the current project. This view contains currently running and completed jobs.

## Required permissions

To query the `INFORMATION_SCHEMA.JOBS_TIMELINE_BY_USER` view, you need the `bigquery.jobs.list` Identity and Access Management (IAM) permission for the project. Each of the following predefined IAM roles includes the required permission:

- Project Viewer
- BigQuery User

For more information about BigQuery permissions, see [Access control with IAM](https://docs.cloud.google.com/bigquery/docs/access-control) .

## Schema

When you query the `INFORMATION_SCHEMA.JOBS_TIMELINE_BY_*` views, the query results contain one row for every second of execution of every BigQuery job. Each period starts on a whole-second interval and lasts exactly one second.

The `INFORMATION_SCHEMA.JOBS_TIMELINE_BY_*` view has the following schema:

> **Note:** The underlying data is partitioned by the `job_creation_time` column and clustered by `project_id` and `user_email` .

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="header">
<th>Column name</th>
<th>Data type</th>
<th>Value</th>
</tr>

<tr class="odd">
<td><code>period_start</code></td>
<td><code>TIMESTAMP</code></td>
<td>Start time of this period.</td>
</tr>
<tr class="even">
<td><code>period_slot_ms</code></td>
<td><code>INTEGER</code></td>
<td>Slot milliseconds consumed in this period.</td>
</tr>
<tr class="odd">
<td><code>project_id</code></td>
<td><code>STRING</code></td>
<td><em>(Clustering column)</em> ID of the project.</td>
</tr>
<tr class="even">
<td><code>project_number</code></td>
<td><code>INTEGER</code></td>
<td>Number of the project.</td>
</tr>
<tr class="odd">
<td><code>user_email</code></td>
<td><code>STRING</code></td>
<td><em>(Clustering column)</em> Email address or service account of the user who ran the job.</td>
</tr>
<tr class="even">
<td><code>principal_subject</code></td>
<td><code>STRING</code></td>
<td>A string representation of the identity of the principal that ran the job.</td>
</tr>
<tr class="odd">
<td><code>job_id</code></td>
<td><code>STRING</code></td>
<td>ID of the job. For example, <code>bquxjob_1234</code> .</td>
</tr>
<tr class="even">
<td><code>job_type</code></td>
<td><code>STRING</code></td>
<td>The type of the job. Can be <code>QUERY</code> , <code>LOAD</code> , <code>EXTRACT</code> , <code>COPY</code> , or <code>NULL</code> . A <code>NULL</code> value indicates a background job.</td>
</tr>
<tr class="odd">
<td><code>labels</code></td>
<td><code>RECORD</code></td>
<td>Array of labels applied to the job as key-value pairs.</td>
</tr>
<tr class="even">
<td><code>statement_type</code></td>
<td><code>STRING</code></td>
<td>The type of query statement, if valid. For example, <code>SELECT</code> , <code>INSERT</code> , <code>UPDATE</code> , or <code>DELETE</code> .</td>
</tr>
<tr class="odd">
<td><code>priority</code></td>
<td><code>STRING</code></td>
<td>The priority of this job. Valid values include <code>INTERACTIVE</code> and <code>BATCH</code> .</td>
</tr>
<tr class="even">
<td><code>parent_job_id</code></td>
<td><code>STRING</code></td>
<td>ID of the parent job, if any.</td>
</tr>
<tr class="odd">
<td><code>job_creation_time</code></td>
<td><code>TIMESTAMP</code></td>
<td><em>(Partitioning column)</em> Creation time of this job. Partitioning is based on the UTC time of this timestamp.</td>
</tr>
<tr class="even">
<td><code>job_start_time</code></td>
<td><code>TIMESTAMP</code></td>
<td>Start time of this job.</td>
</tr>
<tr class="odd">
<td><code>job_end_time</code></td>
<td><code>TIMESTAMP</code></td>
<td>End time of this job.</td>
</tr>
<tr class="even">
<td><code>state</code></td>
<td><code>STRING</code></td>
<td>Running state of the job at the end of this period. Valid states include <code>PENDING</code> , <code>RUNNING</code> , and <code>DONE</code> .</td>
</tr>
<tr class="odd">
<td><code>reservation_id</code></td>
<td><code>STRING</code></td>
<td>Name of the primary reservation assigned to this job at the end of this period, if applicable.</td>
</tr>
<tr class="even">
<td><code>reservation_group_path</code></td>
<td><code>ARRAY&lt;STRING&gt;</code></td>
<td>The reservation group to which the reservation is linked. For example, if the reservation is linked to group <code>my-group</code> , the <code>reservation_group_path</code> field contains a list such as: <code>[my-group]</code> .</td>
</tr>
<tr class="odd">
<td><code>edition</code></td>
<td><code>STRING</code></td>
<td>The edition associated with the reservation assigned to this job. For more information about editions, see <a href="https://docs.cloud.google.com/bigquery/docs/editions-intro">Introduction to BigQuery editions</a> .</td>
</tr>
<tr class="even">
<td><code>total_bytes_billed</code></td>
<td><code>INTEGER</code></td>
<td>If the project is configured to use <a href="https://cloud.google.com/bigquery/pricing#analysis_pricing_models">on-demand pricing</a> , then this field contains the total bytes billed for the job. If the project is configured to use <a href="https://cloud.google.com/bigquery/pricing#analysis_pricing_models">flat-rate pricing</a> , then you are not billed for bytes and this field is informational only. This field is only populated for completed jobs and contains the total number of bytes billed for the entire duration of the job.</td>
</tr>
<tr class="odd">
<td><code>total_bytes_processed</code></td>
<td><code>INTEGER</code></td>
<td>Total bytes processed by the job. This field is only populated for completed jobs and contains the total number of bytes processed over the entire duration of the job.</td>
</tr>
<tr class="even">
<td><code>error_result</code></td>
<td><code>RECORD</code></td>
<td>Details of error (if any) as an <a href="https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/ErrorProto"><code>ErrorProto</code></a><code> .</code></td>
</tr>
<tr class="odd">
<td><code>cache_hit</code></td>
<td><code>BOOLEAN</code></td>
<td>Whether the query results of this job were from a cache.</td>
</tr>
<tr class="even">
<td><code>period_shuffle_ram_usage_ratio</code></td>
<td><code>FLOAT</code></td>
<td>Shuffle usage ratio in the selected time period. The value is <code>0.0</code> if the job ran with a reservation that uses autoscaling and has zero baseline slots.</td>
</tr>
<tr class="odd">
<td><code>period_estimated_runnable_units</code></td>
<td><code>INTEGER</code></td>
<td>Units of work that can be scheduled immediately in this period. Additional slots for these units of work accelerate your query, provided no other query in the reservation needs additional slots.</td>
</tr>
<tr class="even">
<td><code>transaction_id</code></td>
<td><code>STRING</code></td>
<td>ID of the <a href="https://docs.cloud.google.com/bigquery/docs/transactions">transaction</a> in which this job ran, if any.</td>
</tr>
<tr class="odd">
<td><code>global_query_info</code></td>
<td><code>RECORD</code></td>
<td>Information about a <a href="https://docs.cloud.google.com/bigquery/docs/global-queries">global query</a> . Contains the following fields:
<ul>
<li><code>parent_job_id</code> : The ID of the parent global query job in the primary region.</li>
<li><code>parent_job_location</code> : The location of the parent global query job.</li>
<li><code>remote_regions</code> : An array of remote regions referenced by the global query.</li>
</ul></td>
</tr>
</tbody>
</table>

For stability, we recommend that you explicitly list columns in your information schema queries instead of using a wildcard ( `SELECT *` ). Explicitly listing columns prevents queries from breaking if the underlying schema changes.

## Data retention

This view displays running jobs along with job history for the past 180 days. If a project migrates to an organization (either from having no organization or from a different one), job information predating the migration date isn't accessible through the `INFORMATION_SCHEMA.JOBS_TIMELINE_BY_USER` view, as the view only retains data starting from the migration date.

## Scope and syntax

Queries against this view must include a [region qualifier](https://docs.cloud.google.com/bigquery/docs/information-schema-intro#syntax) . If you do not specify a regional qualifier, metadata is retrieved from all regions. The following table explains the region and resource scope for this view:

| View name                                                                                       | Resource scope                                               | Region scope |
|-------------------------------------------------------------------------------------------------|--------------------------------------------------------------|--------------|
| `[ `` PROJECT_ID ```  .]`region-  ``` REGION ```  `.INFORMATION_SCHEMA.JOBS_TIMELINE_BY_USER `` | Jobs submitted by the current user in the specified project. | `REGION`     |

Replace the following:

- Optional: `PROJECT_ID` : the ID of your Google Cloud project. If not specified, the default project is used.

- `REGION` : any [dataset region name](https://docs.cloud.google.com/bigquery/docs/locations) . For example, `` `region-us` `` .

  > **Note:** You must use [a region qualifier](https://docs.cloud.google.com/bigquery/docs/information-schema-intro#region_qualifier) to query `INFORMATION_SCHEMA` views. The location of the query execution must match the region of the `INFORMATION_SCHEMA` view.

## Example

The following query displays the total slot milliseconds consumed per second by jobs submitted by the current user in the designated project:

```
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

> **Note:** `INFORMATION_SCHEMA` view names are case-sensitive.

The result is similar to the following:

```
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
