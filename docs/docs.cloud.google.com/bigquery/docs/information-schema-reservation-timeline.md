# RESERVATIONS\_TIMELINE view

The `  INFORMATION_SCHEMA.RESERVATIONS_TIMELINE  ` view shows time slices of reservation metadata for each reservation administration project for every minute in real time. Additionally, the `  per_second_details  ` array shows autoscale details for each second.

**Note:** The view names `  INFORMATION_SCHEMA.RESERVATIONS_TIMELINE  ` and `  INFORMATION_SCHEMA.RESERVATIONS_TIMELINE_BY_PROJECT  ` are synonymous and can be used interchangeably.

## Required permission

To query the `  INFORMATION_SCHEMA.RESERVATIONS_TIMELINE  ` view, you need the `  bigquery.reservations.list  ` Identity and Access Management (IAM) permission on the project. Each of the following predefined IAM roles includes the required permission:

  - BigQuery Resource Admin ( `  roles/bigquery.resourceAdmin  ` )
  - BigQuery Resource Editor ( `  roles/bigquery.resourceEditor  ` )
  - BigQuery Resource Viewer ( `  roles/bigquery.resourceViewer  ` )
  - BigQuery User ( `  roles/bigquery.user  ` )
  - BigQuery Admin ( `  roles/bigquery.admin  ` )

For more information about BigQuery permissions, see [BigQuery IAM roles and permissions](/bigquery/docs/access-control) .

## Schema

When you query the `  INFORMATION_SCHEMA.RESERVATIONS_TIMELINE  ` view, the query results contain one row for every minute of every BigQuery reservation in the last 180 days, and one row for every minute with reservation changes for any occurrences older than 180 days. Each period starts on a whole-minute interval and lasts exactly one minute.

The `  INFORMATION_SCHEMA.RESERVATIONS_TIMELINE  ` view has the following schema:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Column name</th>
<th>Data type</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       autoscale      </code></td>
<td><code dir="ltr" translate="no">       STRUCT      </code></td>
<td><p>Contains information about the autoscale capacity of the reservation. Fields include the following:</p>
<ul>
<li><p><code dir="ltr" translate="no">         current_slots        </code> : the number of autoscaling slots available to the reservation.</p>
<p>Because <code dir="ltr" translate="no">          current_slots         </code> could be updated multiple times within a minute, use <code dir="ltr" translate="no">          per_second_details.autoscale_current_slots         </code> instead. It reflects accurate state for each second.</p>
<p>Also, after users reduce <code dir="ltr" translate="no">           max_slots          </code> , it may take a while before it can be propagated, so <code dir="ltr" translate="no">           current_slots          </code> may stay in the original value and could be larger than <code dir="ltr" translate="no">           max_slots          </code> for that brief period (less than one minute).</p></li>
<li><code dir="ltr" translate="no">         max_slots        </code> : the maximum number of slots that could be added to the reservation by autoscaling.</li>
</ul></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       edition      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The edition associated with this reservation. For more information about editions, see <a href="/bigquery/docs/editions-intro">Introduction to BigQuery editions</a> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       ignore_idle_slots      </code></td>
<td><code dir="ltr" translate="no">       BOOL      </code></td>
<td>False if slot sharing is enabled, otherwise true.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       labels      </code></td>
<td><code dir="ltr" translate="no">       RECORD      </code></td>
<td>Array of labels associated with the reservation.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       reservation_group_path      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The hierarchical group structure to which the reservation is linked. For example, if the group structure includes a parent group and a child group, the <code dir="ltr" translate="no">       reservation_group_path      </code> field contains a list such as: <code dir="ltr" translate="no">       [parent group, child group]      </code> . This field is in <a href="https://cloud.google.com/products#product-launch-stages">Preview</a> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       period_start      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>Start time of this one-minute period.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       per_second_details      </code></td>
<td><code dir="ltr" translate="no">       STRUCT      </code></td>
<td><p>Contains information about the reservation capacity and usage at each second. Fields include the following:</p>
<ul>
<li><code dir="ltr" translate="no">         start_time        </code> : the exact timestamp of the second.</li>
<li><code dir="ltr" translate="no">         autoscale_current_slots        </code> : the number of autoscaling slots available to the reservation at this second. This number excludes baseline slots.
<strong>Note:</strong> When you reduce <code dir="ltr" translate="no">          max_slots         </code> , the change might not take effect immediately. During this brief period (under one minute), the <code dir="ltr" translate="no">          current_slots         </code> might remain at its original value that could be higher than the value of <code dir="ltr" translate="no">          max_slots         </code> .</li>
<li><code dir="ltr" translate="no">         autoscale_max_slots        </code> : the maximum number of slots that could be added to the reservation by autoscaling at this second. This number excludes baseline slots.</li>
<li><code dir="ltr" translate="no">         slots_assigned        </code> : the number of slots assigned to this reservation at this second. It equals the baseline slot capacity of a reservation.</li>
<li><code dir="ltr" translate="no">         slots_max_assigned        </code> : the maximum slot capacity for this reservation, including slot sharing at this second. If <code dir="ltr" translate="no">         ignore_idle_slots        </code> is true, this field is same as <code dir="ltr" translate="no">         slots_assigned        </code> . Otherwise, the <code dir="ltr" translate="no">         slots_max_assigned        </code> field is the total number of slots in all capacity commitments in the administration project.</li>
</ul>
<p>If there are any autoscale or reservation changes during this minute, the array is populated with 60 rows. However, for non-autoscale reservations that remain unchanged during this minute, the array is empty because it'll otherwise repeat the same number 60 times.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       project_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>ID of the reservation administration project.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       project_number      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>Number of the project.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       reservation_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>For joining with the jobs_timeline table. This is of the form <em>project_id</em> : <em>location</em> . <em>reservation_name</em> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       reservation_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the reservation.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       slots_assigned      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>The number of slots assigned to this reservation.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       slots_max_assigned      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>The maximum slot capacity for this reservation, including slot sharing. If <code dir="ltr" translate="no">       ignore_idle_slots      </code> is true, this is the same as <code dir="ltr" translate="no">       slots_assigned      </code> , otherwise this is the total number of slots in all capacity commitments in the administration project.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       max_slots      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>The maximum number of slots that this reservation can use, which includes baseline slots ( <code dir="ltr" translate="no">       slot_capacity      </code> ), idle slots (if <code dir="ltr" translate="no">       ignore_idle_slots      </code> is false), and autoscale slots. This field is specified by users for using the <a href="/bigquery/docs/reservations-workload-management#predictable">reservation predictability feature</a> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       scaling_mode      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The scaling mode for the reservation, which determines how the reservation scales from baseline to <code dir="ltr" translate="no">       max_slots      </code> . This field is specified by users for using the <a href="/bigquery/docs/reservations-workload-management#predictable">reservation predictability feature</a> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       period_autoscale_slot_seconds      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>The total slot seconds charged by autoscale for a specific minute (each data row corresponds to one minute).</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       is_creation_region      </code></td>
<td><code dir="ltr" translate="no">       BOOLEAN      </code></td>
<td><p>Specifies if the current region is the location where the reservation was created. This location is used to determine the pricing of the baseline reservation slots. For a failover <a href="/bigquery/docs/managed-disaster-recovery">disaster recovery (DR)</a> reservation, a <code dir="ltr" translate="no">        TRUE       </code> value indicates the original primary location, while for a non-DR reservation, a <code dir="ltr" translate="no">        TRUE       </code> value denotes the reservation's location.</p>
<p>For a non-failover reservation, this value is always <code dir="ltr" translate="no">        TRUE       </code> . For a failover reservation, the value depends on the region: <code dir="ltr" translate="no">        TRUE       </code> for the original primary and <code dir="ltr" translate="no">        FALSE       </code> for the original secondary.</p></td>
</tr>
</tbody>
</table>

For stability, we recommend that you explicitly list columns in your information schema queries instead of using a wildcard ( `  SELECT *  ` ). Explicitly listing columns prevents queries from breaking if the underlying schema changes.

## Scope and syntax

Queries against this view must include a [region qualifier](/bigquery/docs/information-schema-intro#syntax) . If you don't specify a regional qualifier, metadata is retrieved from all regions. The following table explains the region and resource scope for this view:

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
<td><code dir="ltr" translate="no">       [               PROJECT_ID              .]`region-               REGION              `.INFORMATION_SCHEMA.RESERVATIONS_TIMELINE[_BY_PROJECT]      </code></td>
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

#### Example: See autoscaling per second

The following example shows per-second autoscaling of `  YOUR_RESERVATION_ID  ` across all jobs:

``` text
SELECT s.start_time, s.autoscale_current_slots
FROM `region-us.INFORMATION_SCHEMA.RESERVATIONS_TIMELINE` m
JOIN m.per_second_details s
WHERE period_start BETWEEN '2025-09-28' AND '2025-09-29'
  AND reservation_id = 'YOUR_RESERVATION_ID'
ORDER BY period_start, s.start_time
```

The result is similar to the following:

``` text
+---------------------+-------------------------+
|     start_time      | autoscale_current_slots |
+---------------------+-------------------------+
| 2025-09-28 00:00:00 |                    1600 |
| 2025-09-28 00:00:01 |                    1600 |
| 2025-09-28 00:00:02 |                    1600 |
| 2025-09-28 00:00:03 |                    1600 |
| 2025-09-28 00:00:04 |                    1600 |
+---------------------+-------------------------+
```

**Note:** The `  period_start  ` column is a partitioning key, so it's important to filter by `  period_start  ` to make the query efficient.

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
