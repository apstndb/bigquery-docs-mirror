---
name: documents/docs.cloud.google.com/bigquery/docs/information-schema-jobs-timeline-by-folder
uri: https://docs.cloud.google.com/bigquery/docs/information-schema-jobs-timeline-by-folder
title: JOBS_TIMELINE_BY_FOLDER view
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# JOBS_TIMELINE_BY_FOLDER view

The `INFORMATION_SCHEMA.JOBS_TIMELINE_BY_FOLDER` view contains near real-time BigQuery metadata by timeslice for all jobs submitted in the parent folder of the current project, including the jobs in subfolders under it. This view contains both running and completed jobs.

## Required permissions

To query the `INFORMATION_SCHEMA.JOBS_TIMELINE_BY_FOLDER` view, you need the `bigquery.jobs.listAll` Identity and Access Management (IAM) permission for the parent folder. Each of the following predefined IAM roles includes the required permission:

- Folder Admin
- BigQuery Admin

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
<td><code>folder_numbers</code></td>
<td><code>REPEATED INTEGER</code></td>
<td>Number IDs of the folders that contain the project, starting with the folder that immediately contains the project, followed by the folder that contains the child folder, and so forth. For example, if `folder_numbers` is `[1, 2, 3]`, then folder `1` immediately contains the project, folder `2` contains `1`, and folder `3` contains `2`.</td>
</tr>
<tr class="even">
<td><code>user_email</code></td>
<td><code>STRING</code></td>
<td><em>(Clustering column)</em> Email address or service account of the user who ran the job.</td>
</tr>
<tr class="odd">
<td><code>principal_subject</code></td>
<td><code>STRING</code></td>
<td>A string representation of the identity of the principal that ran the job.</td>
</tr>
<tr class="even">
<td><code>job_id</code></td>
<td><code>STRING</code></td>
<td>ID of the job. For example, <code>bquxjob_1234</code> .</td>
</tr>
<tr class="odd">
<td><code>job_type</code></td>
<td><code>STRING</code></td>
<td>The type of the job. Can be <code>QUERY</code> , <code>LOAD</code> , <code>EXTRACT</code> , <code>COPY</code> , or <code>null</code> . Job type <code>null</code> indicates an internal job, such as script job statement evaluation or materialized view refresh.</td>
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
<td>If the project is configured to use <a href="https://cloud.google.com/bigquery/pricing#analysis_pricing_models">on-demand pricing</a> , then this field contains the total bytes billed for the job. If the project is configured to use <a href="https://cloud.google.com/bigquery/pricing#analysis_pricing_models">flat-rate pricing</a> , then you are not billed for bytes and this field is informational only.</td>
</tr>
<tr class="odd">
<td><code>total_bytes_processed</code></td>
<td><code>INTEGER</code></td>
<td>Total bytes processed by the job.</td>
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
<td>ID of the <a href="https://docs.cloud.google.com/bigquery/docs/transactions">transaction</a> in which this job ran, if any. ( <a href="https://cloud.google.com/products#product-launch-stages">Preview</a> )</td>
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
<tr class="even">
<td><code>copy_job_statistics</code></td>
<td><code>RECORD</code></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/Job#CopyJobStatistics">Statistics for a copy job.</a></td>
</tr>
</tbody>
</table>

For stability, we recommend that you explicitly list columns in your information schema queries instead of using a wildcard ( `SELECT *` ). Explicitly listing columns prevents queries from breaking if the underlying schema changes.

## Data retention

This view displays running jobs along with job history for the past 180 days. If a project migrates to an organization (either from having no organization or from a different one), job information predating the migration date isn't accessible through the `INFORMATION_SCHEMA.JOBS_TIMELINE_BY_FOLDER` view, as the view only retains data starting from the migration date.

## Scope and syntax

Queries against this view must include a [region qualifier](https://docs.cloud.google.com/bigquery/docs/information-schema-intro#syntax) . If you don't specify a regional qualifier, metadata is retrieved from all regions. The following table explains the region scope for this view:

| View name                                                                                         | Resource scope | Region scope |
|---------------------------------------------------------------------------------------------------|----------------|--------------|
| `[ `` PROJECT_ID ```  .]`region-  ``` REGION ```  `.INFORMATION_SCHEMA.JOBS_TIMELINE_BY_FOLDER `` | Project level  | ` REGION `   |

Replace the following:

- Optional: `PROJECT_ID` : the ID of your Google Cloud project. If not specified, the default project is used.

- `REGION` : any [dataset region name](https://docs.cloud.google.com/bigquery/docs/locations) . For example, `` `region-us` `` .

  > **Note:** You must use [a region qualifier](https://docs.cloud.google.com/bigquery/docs/information-schema-intro#region_qualifier) to query `INFORMATION_SCHEMA` views. The location of the query execution must match the region of the `INFORMATION_SCHEMA` view.

## Examples

The following examples show how to query the `INFORMATION_SCHEMA.JOBS_TIMELINE_BY_FOLDER` view.

### Get the number of unique jobs

The following query displays the number of unique jobs running per minute in the designated project's folder:

```
SELECT
  TIMESTAMP_TRUNC(period_start, MINUTE) AS per_start,
  COUNT(DISTINCT job_id) AS unique_jobs
FROM
  `region-us`.INFORMATION_SCHEMA.JOBS_TIMELINE_BY_FOLDER,
  UNNEST(folder_numbers) f
WHERE
  my_folder_number = f
GROUP BY
  per_start
ORDER BY
  per_start DESC;
```

> **Note:** `INFORMATION_SCHEMA` view names are case-sensitive.

The result is similar to the following:

```
+---------------------------+---------------------------------+
|  per_start                |  unique_jobs                    |
+---------------------------+---------------------------------+
|  2019-10-10 00:04:00 UTC  |  5                              |
|  2019-10-10 00:03:00 UTC  |  2                              |
|  2019-10-10 00:02:00 UTC  |  3                              |
|  2019-10-10 00:01:00 UTC  |  4                              |
|  2019-10-10 00:00:00 UTC  |  4                              |
+---------------------------+---------------------------------+
```

### Calculate the slot-time used

The following query displays the slot-time used per minute in the designated project's folder:

```
SELECT
  TIMESTAMP_TRUNC(period_start, MINUTE) AS per_start,
  SUM(period_slot_ms) AS slot_ms
FROM
  `region-us`.INFORMATION_SCHEMA.JOBS_TIMELINE_BY_FOLDER,
  UNNEST(folder_numbers) f
WHERE
  my_folder_number = f
  AND reservation_id = "my reservation id"
  AND statement_type != "SCRIPT"
GROUP BY
  per_start
ORDER BY
  per_start DESC;
```

> **Note:** `INFORMATION_SCHEMA` view names are case-sensitive.

> **Note:** Projects within a single folder can be assigned to more than one reservation. `JOBS_TIMELINE_BY_FOLDER` can provide data across multiple reservations. When summing `period_slot_ms` , ensure that you are filtering for individual reservations.

The result is similar to the following:

```
+---------------------------+---------------------------------+
|  per_start                |  slot_ms                        |
+---------------------------+---------------------------------+
|  2019-10-10 00:04:00 UTC  |  500                            |
|  2019-10-10 00:03:00 UTC  |  1000                           |
|  2019-10-10 00:02:00 UTC  |  3000                           |
|  2019-10-10 00:01:00 UTC  |  4000                           |
|  2019-10-10 00:00:00 UTC  |  4000                           |
+---------------------------+---------------------------------+
```
