# JOBS\_TIMELINE\_BY\_FOLDER view

The `  INFORMATION_SCHEMA.JOBS_TIMELINE_BY_FOLDER  ` view contains near real-time BigQuery metadata by timeslice for all jobs submitted in the parent folder of the current project, including the jobs in subfolders under it. This view contains both running and completed jobs.

## Required permissions

To query the `  INFORMATION_SCHEMA.JOBS_TIMELINE_BY_FOLDER  ` view, you need the `  bigquery.jobs.listAll  ` Identity and Access Management (IAM) permission for the parent folder. Each of the following predefined IAM roles includes the required permission:

  - Folder Admin
  - BigQuery Admin

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
<td>If the project is configured to use <a href="https://cloud.google.com/bigquery/pricing#analysis_pricing_models">on-demand pricing</a> , then this field contains the total bytes billed for the job. If the project is configured to use <a href="https://cloud.google.com/bigquery/pricing#analysis_pricing_models">flat-rate pricing</a> , then you are not billed for bytes and this field is informational only.</td>
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
<tr class="odd">
<td><code dir="ltr" translate="no">       transaction_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>ID of the <a href="/bigquery/docs/transactions">transaction</a> in which this job ran, if any. ( <a href="https://cloud.google.com/products#product-launch-stages">Preview</a> )</td>
</tr>
</tbody>
</table>

For stability, we recommend that you explicitly list columns in your information schema queries instead of using a wildcard ( `  SELECT *  ` ). Explicitly listing columns prevents queries from breaking if the underlying schema changes.

## Data retention

This view displays running jobs along with job history for the past 180 days. If a project migrates to an organization (either from having no organization or from a different one), job information predating the migration date isn't accessible through the `  INFORMATION_SCHEMA.JOBS_TIMELINE_BY_FOLDER  ` view, as the view only retains data starting from the migration date.

## Scope and syntax

Queries against this view must include a [region qualifier](/bigquery/docs/information-schema-intro#syntax) . If you don't specify a regional qualifier, metadata is retrieved from all regions. The following table explains the region scope for this view:

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
<td><code dir="ltr" translate="no">       [               PROJECT_ID              .]`region-               REGION              `.INFORMATION_SCHEMA.JOBS_TIMELINE_BY_FOLDER      </code></td>
<td>Project level</td>
<td>REGION</td>
</tr>
</tbody>
</table>

Replace the following:

  - Optional: `  PROJECT_ID  ` : the ID of your Google Cloud project. If not specified, the default project is used.
  - `  REGION  ` : any [dataset region name](/bigquery/docs/locations) . For example, ``  `region-us`  `` .
    **Note:** You must use [a region qualifier](/bigquery/docs/information-schema-intro#region_qualifier) to query `  INFORMATION_SCHEMA  ` views. The location of the query execution must match the region of the `  INFORMATION_SCHEMA  ` view.

## Examples

The following examples show how to query the `  INFORMATION_SCHEMA.JOBS_TIMELINE_BY_FOLDER  ` view.

### Get the number of unique jobs

The following query displays the number of unique jobs running per minute in the designated project's folder:

``` text
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

**Note:** `  INFORMATION_SCHEMA  ` view names are case-sensitive.

The result is similar to the following:

``` text
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

``` text
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

**Note:** `  INFORMATION_SCHEMA  ` view names are case-sensitive.

**Note:** Projects within a single folder can be assigned to more than one reservation. `  JOBS_TIMELINE_BY_FOLDER  ` can provide data across multiple reservations. When summing `  period_slot_ms  ` , ensure that you are filtering for individual reservations.

The result is similar to the following:

``` text
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
