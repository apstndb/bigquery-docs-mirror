# JOBS\_TIMELINE\_BY\_ORGANIZATION view

The `  INFORMATION_SCHEMA.JOBS_TIMELINE_BY_ORGANIZATION  ` view contains near real-time BigQuery metadata by timeslice for all jobs submitted in the organization associated with the current project. This view contains currently running and completed jobs.

## Required permissions

To query the `  INFORMATION_SCHEMA.JOBS_TIMELINE_BY_ORGANIZATION  ` view, you need the `  bigquery.jobs.listAll  ` Identity and Access Management (IAM) permission for the organization. Each of the following predefined IAM roles includes the required permission:

  - BigQuery Resource Admin at the organization level
  - Organization Owner
  - Organization Admin

The `  JOBS_BY_ORGANIZATION  ` schema table is only available to users with defined Google Cloud organizations.

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
<td><code dir="ltr" translate="no">       folder_numbers      </code></td>
<td><code dir="ltr" translate="no">       REPEATED INTEGER      </code></td>
<td>Number IDs of the folders that contain the project, starting with the folder that immediately contains the project, followed by the folder that contains the child folder, and so forth. For example, if `folder_numbers` is `[1, 2, 3]`, then folder `1` immediately contains the project, folder `2` contains `1`, and folder `3` contains `2`.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       user_email      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><em>(Clustering column)</em> Email address or service account of the user who ran the job.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       principal_subject      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>A string representation of the identity of the principal that ran the job.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       job_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>ID of the job. For example, <code dir="ltr" translate="no">       bquxjob_1234      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       job_type      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The type of the job. Can be <code dir="ltr" translate="no">       QUERY      </code> , <code dir="ltr" translate="no">       LOAD      </code> , <code dir="ltr" translate="no">       EXTRACT      </code> , <code dir="ltr" translate="no">       COPY      </code> , or <code dir="ltr" translate="no">       null      </code> . Job type <code dir="ltr" translate="no">       null      </code> indicates an internal job, such as script job statement evaluation or materialized view refresh.</td>
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
<td>If the project is configured to use <a href="https://cloud.google.com/bigquery/pricing#analysis_pricing_models">on-demand pricing</a> , then this field contains the total bytes billed for the job. If the project is configured to use <a href="https://cloud.google.com/bigquery/pricing#analysis_pricing_models">flat-rate pricing</a> , then you are not billed for bytes. This field is not configurable.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       total_bytes_processed      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>Total bytes processed by the job.</td>
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
</tbody>
</table>

For stability, we recommend that you explicitly list columns in your information schema queries instead of using a wildcard ( `  SELECT *  ` ). Explicitly listing columns prevents queries from breaking if the underlying schema changes.

## Data retention

This view displays running jobs along with job history for the past 180 days. If a project migrates to an organization (either from having no organization or from a different one), job information predating the migration date isn't accessible through the `  INFORMATION_SCHEMA.JOBS_TIMELINE_BY_ORGANIZATION  ` view, as the view only retains data starting from the migration date.

## Scope and syntax

Queries against this view must include a [region qualifier](/bigquery/docs/information-schema-intro#syntax) . If you do not specify a regional qualifier, metadata is retrieved from all regions. The following table explains the region scope for this view:

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
<td><code dir="ltr" translate="no">       [               PROJECT_ID              .]`region-               REGION              `.INFORMATION_SCHEMA.JOBS_TIMELINE_BY_ORGANIZATION      </code></td>
<td>Organization that contains the specified project</td>
<td>REGION</td>
</tr>
</tbody>
</table>

Replace the following:

  - Optional: `  PROJECT_ID  ` : the ID of your Google Cloud project. If not specified, the default project is used.
  - `  REGION  ` : any [dataset region name](/bigquery/docs/locations) . For example, ``  `region-us`  `` .
    **Note:** You must use [a region qualifier](/bigquery/docs/information-schema-intro#region_qualifier) to query `  INFORMATION_SCHEMA  ` views. The location of the query execution must match the region of the `  INFORMATION_SCHEMA  ` view.

## Examples

#### Example: See total slot usage per second

To run the query against a project other than your default project, add the project ID in the following format:

``` text
`PROJECT_ID`.`region-REGION_NAME`.INFORMATION_SCHEMA.JOBS_TIMELINE_BY_ORGANIZATION
```

For example, ``  `myproject`.`region-us`.INFORMATION_SCHEMA.JOBS_TIMELINE_BY_ORGANIZATION  `` .

The following example shows per-second slot usage from projects assigned to `  YOUR_RESERVATION_ID  ` across all jobs:

``` text
SELECT
  jobs.period_start,
  SUM(jobs.period_slot_ms) / 1000 AS period_slot_seconds,
  ANY_VALUE(COALESCE(s.slots_assigned, res.slots_assigned)) AS estimated_slots_assigned,
  ANY_VALUE(COALESCE(s.slots_max_assigned, res.slots_max_assigned)) AS estimated_slots_max_assigned
FROM `region-us`.INFORMATION_SCHEMA.JOBS_TIMELINE_BY_ORGANIZATION jobs
JOIN `region-us`.INFORMATION_SCHEMA.RESERVATIONS_TIMELINE res
  ON jobs.reservation_id = res.reservation_id
  AND TIMESTAMP_TRUNC(jobs.period_start, MINUTE) = res.period_start
LEFT JOIN UNNEST(res.per_second_details) s
  ON jobs.period_start = s.start_time
WHERE
  jobs.job_creation_time
    BETWEEN TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 1 DAY)
        AND CURRENT_TIMESTAMP()
  AND res.period_start
    BETWEEN TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 1 DAY)
        AND CURRENT_TIMESTAMP()
  AND res.reservation_id = 'YOUR_RESERVATION_ID'
  AND (jobs.statement_type != "SCRIPT" OR jobs.statement_type IS NULL)  -- Avoid duplicate byte counting in parent and children jobs.
GROUP BY
  period_start
ORDER BY
  period_start DESC;
```

The result is similar to the following:

``` text
+-----------------------+---------------------+--------------------------+------------------------------+
|     period_start      | period_slot_seconds | estimated_slots_assigned | estimated_slots_max_assigned |
+-----------------------+---------------------+--------------------------+------------------------------+
|2021-06-08 21:33:59 UTC|       100.000       |         100              |           100                |
|2021-06-08 21:33:58 UTC|        96.753       |         100              |           100                |
|2021-06-08 21:33:57 UTC|        41.668       |         100              |           100                |
+-----------------------+---------------------+--------------------------+------------------------------+
```

#### Example: Slot usage by reservation

The following example shows per-second slot usage for each reservation in the last day:

``` text
SELECT
  jobs.period_start,
  res.reservation_id,
  SUM(jobs.period_slot_ms) / 1000 AS period_slot_seconds,
  ANY_VALUE(COALESCE(s.slots_assigned, res.slots_assigned)) AS estimated_slots_assigned,
  ANY_VALUE(COALESCE(s.slots_max_assigned, res.slots_max_assigned)) AS estimated_slots_max_assigned
FROM `region-us`.INFORMATION_SCHEMA.JOBS_TIMELINE_BY_ORGANIZATION jobs
JOIN `region-us`.INFORMATION_SCHEMA.RESERVATIONS_TIMELINE res
  ON jobs.reservation_id = res.reservation_id
  AND TIMESTAMP_TRUNC(jobs.period_start, MINUTE) = res.period_start
LEFT JOIN UNNEST(res.per_second_details) s
  ON jobs.period_start = s.start_time
WHERE
  jobs.job_creation_time
      BETWEEN TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 1 DAY)
          AND CURRENT_TIMESTAMP()
  AND res.period_start
      BETWEEN TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 1 DAY)
          AND CURRENT_TIMESTAMP()
  AND (jobs.statement_type != "SCRIPT" OR jobs.statement_type IS NULL)  -- Avoid duplicate byte counting in parent and children jobs.
GROUP BY
  period_start,
  reservation_id
ORDER BY
  period_start DESC,
  reservation_id;
```

The result is similar to the following:

``` text
+-----------------------+----------------+---------------------+--------------------------+------------------------------+
|     period_start      | reservation_id | period_slot_seconds | estimated_slots_assigned | estimated_slots_max_assigned |
+-----------------------+----------------+---------------------+--------------------------+------------------------------+
|2021-06-08 21:33:59 UTC|     prod01     |       100.000       |             100          |              100             |
|2021-06-08 21:33:58 UTC|     prod02     |       177.201       |             200          |              500             |
|2021-06-08 21:32:57 UTC|     prod01     |        96.753       |             100          |              100             |
|2021-06-08 21:32:56 UTC|     prod02     |       182.329       |             200          |              500             |
+-----------------------+----------------+---------------------+--------------------------+------------------------------+
```
