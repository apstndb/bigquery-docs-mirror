---
name: documents/docs.cloud.google.com/bigquery/docs/information-schema-jobs-timeline
uri: https://docs.cloud.google.com/bigquery/docs/information-schema-jobs-timeline
title: JOBS_TIMELINE view
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# JOBS_TIMELINE view

The `INFORMATION_SCHEMA.JOBS_TIMELINE` view contains near real-time BigQuery metadata by timeslice for all jobs submitted in the current project. This view contains currently running and completed jobs.

> **Note:** The view names `INFORMATION_SCHEMA.JOBS_TIMELINE` and `INFORMATION_SCHEMA.JOBS_TIMELINE_BY_PROJECT` are synonymous and can be used interchangeably.

## Required permissions

To query the `INFORMATION_SCHEMA.JOBS_TIMELINE` view, you need the `bigquery.jobs.listAll` Identity and Access Management (IAM) permission for the project. Each of the following predefined IAM roles includes the required permission:

- Project Owner
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
<tr class="even">
<td><code>copy_job_statistics</code></td>
<td><code>RECORD</code></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/Job#CopyJobStatistics">Statistics for a copy job.</a></td>
</tr>
</tbody>
</table>

For stability, we recommend that you explicitly list columns in your information schema queries instead of using a wildcard ( `SELECT *` ). Explicitly listing columns prevents queries from breaking if the underlying schema changes.

## Data retention

This view displays running jobs along with job history for the past 180 days. If a project migrates to an organization (either from having no organization or from a different one), job information predating the migration date isn't accessible through the `INFORMATION_SCHEMA.JOBS_TIMELINE` view, as the view only retains data starting from the migration date.

## Scope and syntax

Queries against this view must include a [region qualifier](https://docs.cloud.google.com/bigquery/docs/information-schema-intro#syntax) . If you don't specify a regional qualifier, metadata is retrieved from all regions. The following table explains the region scope for this view:

| View name                                                                                            | Resource scope | Region scope |
|------------------------------------------------------------------------------------------------------|----------------|--------------|
| `[ `` PROJECT_ID ```  .]`region-  ``` REGION ```  `.INFORMATION_SCHEMA.JOBS_TIMELINE[_BY_PROJECT] `` | Project level  | `REGION`     |

Replace the following:

- Optional: `PROJECT_ID` : the ID of your Google Cloud project. If not specified, the default project is used.

- `REGION` : any [dataset region name](https://docs.cloud.google.com/bigquery/docs/locations) . For example, `` `region-us` `` .

  > **Note:** You must use [a region qualifier](https://docs.cloud.google.com/bigquery/docs/information-schema-intro#region_qualifier) to query `INFORMATION_SCHEMA` views. The location of the query execution must match the region of the `INFORMATION_SCHEMA` view.

## Examples

To run the query against a project other than your default project, add the project ID in the following format:

```
`PROJECT_ID`.`region-REGION_NAME`.INFORMATION_SCHEMA.VIEW
```

For example, `` `myproject`.`region-us`.INFORMATION_SCHEMA.JOBS_TIMELINE `` .

The following example calculates the slot utilization for every second in the last day:

```
SELECT
  period_start,
  SUM(period_slot_ms) AS total_slot_ms,
FROM
  `reservation-admin-project.region-us`.INFORMATION_SCHEMA.JOBS_TIMELINE
WHERE
  period_start BETWEEN TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 1 DAY) AND CURRENT_TIMESTAMP()
GROUP BY
  period_start
ORDER BY
  period_start DESC;
```

> **Note:** `INFORMATION_SCHEMA` view names are case-sensitive.

The result is similar to the following:

```
+---------------------+---------------+
|    period_start     | total_slot_ms |
+---------------------+---------------+
| 2020-07-29 03:52:14 |     122415176 |
| 2020-07-29 03:52:15 |     141107048 |
| 2020-07-29 03:52:16 |     173335142 |
| 2020-07-28 03:52:17 |     131107048 |
+---------------------+---------------+
```

You can check usage for a particular reservation with `WHERE reservation_id = "…"` . For script jobs, the parent job also reports the total slot usage from its children jobs. To avoid double counting, use `WHERE statement_type != "SCRIPT"` to exclude the parent job.

### Number of `RUNNING` and `PENDING` jobs over time

To run the query against a project other than your default project, add the project ID in the following format:

```
`PROJECT_ID`.`region-REGION_NAME`.INFORMATION_SCHEMA.VIEW
```

For example, `` `myproject`.`region-us`.INFORMATION_SCHEMA.JOBS_TIMELINE `` .

The following example computes the number of `RUNNING` and `PENDING` jobs at every second in the last day:

```
SELECT
  period_start,
  SUM(IF(state = "PENDING", 1, 0)) as PENDING,
  SUM(IF(state = "RUNNING", 1, 0)) as RUNNING
FROM
  `reservation-admin-project.region-us`.INFORMATION_SCHEMA.JOBS_TIMELINE
WHERE
  period_start BETWEEN TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 1 DAY) AND CURRENT_TIMESTAMP()
GROUP BY
  period_start;
```

> **Note:** `INFORMATION_SCHEMA` view names are case-sensitive.

The result is similar to the following:

```
+---------------------+---------+---------+
|    period_start     | PENDING | RUNNING |
+---------------------+---------+---------+
| 2020-07-29 03:52:14 |       7 |      27 |
| 2020-07-29 03:52:15 |       1 |      21 |
| 2020-07-29 03:52:16 |       5 |      21 |
| 2020-07-29 03:52:17 |       4 |      22 |
+---------------------+---------+---------+
```

### Resource usage by jobs at a specific point in time

To run the query against a project other than your default project, add the project ID in the following format:

```
`PROJECT_ID`.`region-REGION_NAME`.INFORMATION_SCHEMA.VIEW
```

For example, `` `myproject`.`region-us`.INFORMATION_SCHEMA.JOBS `` .

The following example returns the `job_id` of all jobs running at a specific point in time together with their resource usage during that one-second period:

```
SELECT
  job_id,
  period_slot_ms
FROM
  `reservation-admin-project.region-us`.INFORMATION_SCHEMA.JOBS_TIMELINE_BY_PROJECT
WHERE
  period_start = '2020-07-29 03:52:14'
  AND (statement_type != 'SCRIPT' OR statement_type IS NULL);
```

> **Note:** `INFORMATION_SCHEMA` view names are case-sensitive.

The result is similar to the following:

```
+------------------+
| job_id | slot_ms |
+------------------+
| job_1  | 2415176 |
| job_2  | 4417245 |
| job_3  |  427416 |
| job_4  | 1458122 |
+------------------+
```

### Match slot usage behavior from administrative resource charts

You can use [administrative resource charts](https://docs.cloud.google.com/bigquery/docs/admin-resource-charts) to monitor your organization's health, slot usage, and BigQuery jobs performance over time. The following example queries the `INFORMATION_SCHEMA.JOBS_TIMELINE` view for a slot usage timeline at one-hour intervals, similar to the information that is available in administrative resource charts.

```
DECLARE
  start_time timestamp DEFAULT TIMESTAMP(START_TIME);
DECLARE
  end_time timestamp DEFAULT TIMESTAMP(END_TIME);

WITH
  snapshot_data AS (
  SELECT
    UNIX_MILLIS(period_start) AS period_start,
    IFNULL(SUM(period_slot_ms), 0) AS period_slot_ms,
    DIV(UNIX_MILLIS(period_start), 3600000 * 1) * 3600000 * 1 AS time_ms
  FROM (
    SELECT
      *
    FROM
      `PROJECT_ID.region-US`.INFORMATION_SCHEMA.JOBS_TIMELINE_BY_PROJECT
    WHERE
      ((job_creation_time >= TIMESTAMP_SUB(start_time, INTERVAL 1200 MINUTE)
          AND job_creation_time < TIMESTAMP(end_time))
        AND period_start >= TIMESTAMP(start_time)
        AND period_start < TIMESTAMP(end_time))
      AND (statement_type != "SCRIPT"
        OR statement_type IS NULL)
      AND REGEXP_CONTAINS(reservation_id, "^PROJECT_ID:") )
  GROUP BY
    period_start,
    time_ms ),
  converted_percentiles_data AS (
  SELECT
    time_ms,
    100 - CAST(SAFE_DIVIDE(3600000 * 1 * 1 / 1000, COUNT(*)) AS INT64) AS converted_percentiles,
  FROM
    snapshot_data
  GROUP BY
    time_ms ),
  data_by_time AS (
  SELECT
    time_ms,
  IF
    (converted_percentiles <= 0, 0, APPROX_QUANTILES(period_slot_ms, 100)[SAFE_OFFSET(converted_percentiles)] / 1000) AS p99_slots,
    SUM(period_slot_ms) / (3600000 * 1) AS avg_slots
  FROM
    snapshot_data
  JOIN
    converted_percentiles_data AS c
  USING
    (time_ms)
  GROUP BY
    time_ms,
    converted_percentiles )
SELECT
  time_ms,
  TIMESTAMP_MILLIS(time_ms) AS time_stamp,
  IFNULL(avg_slots, 0) AS avg_slots,
  IFNULL(p99_slots, 0) AS p99_slots,
FROM (
  SELECT
    time_ms * 3600000 * 1 AS time_ms
  FROM
    UNNEST(GENERATE_ARRAY(DIV(UNIX_MILLIS(start_time), 3600000 * 1), DIV(UNIX_MILLIS(end_time), 3600000 * 1) - 1, 1)) AS time_ms )
LEFT JOIN
  data_by_time
USING
  (time_ms)
ORDER BY
  time_ms DESC;
```

### Calculate the percentage of execution time that had pending work

To run the query against a project other than your default project, add the project ID in the following format:

```
`PROJECT_ID`.`region-REGION_NAME`.INFORMATION_SCHEMA.VIEW
```

For example, `` `myproject`.`region-us`.INFORMATION_SCHEMA.JOBS `` .

The following example returns a float value that represents the percentage of the total job execution duration where the value of [`period_estimated_runnable_units`](https://docs.cloud.google.com/bigquery/docs/information-schema-jobs-timeline#schema) was non-zero, which means that the job was requesting more slots. A large value indicates that the job suffered from slot contention, whereas a small value indicates that the job wasn't requesting slots for the majority of the execution time, which means that there was little to no slot contention.

If the resulting value is large, you can try adding more slots to see the impact and understand whether slot contention is the only bottleneck.

```
SELECT ROUND(COUNTIF(period_estimated_runnable_units > 0) / COUNT(*) * 100, 1) as execution_duration_percentage
FROM `myproject`.`region-us`.INFORMATION_SCHEMA.JOBS_TIMELINE
WHERE job_id = 'my_job_id'
GROUP BY job_id
```

If you know the date of the query execution, add a `DATE(period_start) = 'YYYY-MM-DD'` clause to the query to reduce the amount of bytes processed and speed up the execution. For example, `DATE(period_start) = '2025-08-22'` .

> **Note:** `INFORMATION_SCHEMA` view names are case-sensitive.

The result is similar to the following:

```
+-------------------------------+
| execution_duration_percentage |
+-------------------------------+
|                          96.7 |
+-------------------------------+
```
