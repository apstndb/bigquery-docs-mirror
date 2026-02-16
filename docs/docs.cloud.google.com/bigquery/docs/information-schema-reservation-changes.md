# RESERVATION\_CHANGES view

The `  INFORMATION_SCHEMA.RESERVATION_CHANGES  ` view contains a near real-time list of all changes to reservations within the administration project. Each row represents a change to a single reservation. For more information, see [Introduction to reservations](/bigquery/docs/reservations-intro) .

**Note:** The view names `  INFORMATION_SCHEMA.RESERVATION_CHANGES  ` and `  INFORMATION_SCHEMA.RESERVATION_CHANGES_BY_PROJECT  ` are synonymous and can be used interchangeably.

## Required permission

To query the `  INFORMATION_SCHEMA.RESERVATION_CHANGES  ` view, you need the `  bigquery.reservations.list  ` Identity and Access Management (IAM) permission on the project. Each of the following predefined IAM roles includes the required permission:

  - BigQuery Resource Admin ( `  roles/bigquery.resourceAdmin  ` )
  - BigQuery Resource Editor ( `  roles/bigquery.resourceEditor  ` )
  - BigQuery Resource Viewer ( `  roles/bigquery.resourceViewer  ` )
  - BigQuery User ( `  roles/bigquery.user  ` )
  - BigQuery Admin ( `  roles/bigquery.admin  ` )

For more information about BigQuery permissions, see [BigQuery IAM roles and permissions](/bigquery/docs/access-control) .

## Schema

The `  INFORMATION_SCHEMA.RESERVATION_CHANGES  ` view has the following schema:

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
<td><code dir="ltr" translate="no">       change_timestamp      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>Time when the change occurred.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       project_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>ID of the administration project.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       project_number      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>Number of the administration project.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       reservation_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>User provided reservation name.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       ignore_idle_slots      </code></td>
<td><code dir="ltr" translate="no">       BOOL      </code></td>
<td>If false, any query using this reservation can use unused idle slots from other capacity commitments.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       action      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Type of event that occurred with the reservation. Can be <code dir="ltr" translate="no">       CREATE      </code> , <code dir="ltr" translate="no">       UPDATE      </code> , or <code dir="ltr" translate="no">       DELETE      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       slot_capacity      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>Baseline of the reservation.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       user_email      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Email address of the user or subject of the <a href="/iam/docs/workforce-identity-federation">workforce identity federation</a> that made the change. <code dir="ltr" translate="no">       google      </code> for changes made by Google. <code dir="ltr" translate="no">       NULL      </code> if the email address is unknown.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       target_job_concurrency      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>The target number of queries that can execute simultaneously, which is limited by available resources. If zero, then this value is computed automatically based on available resources.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       autoscale      </code></td>
<td><code dir="ltr" translate="no">       STRUCT      </code></td>
<td><p>Information about the autoscale capacity of the reservation. Fields include the following:</p>
<ul>
<li><code dir="ltr" translate="no">         current_slots        </code> : the number of slots added to the reservation by autoscaling.
<strong>Note:</strong> After users reduce <code dir="ltr" translate="no">          max_slots         </code> , it may take a while before it can be propagated, so <code dir="ltr" translate="no">          current_slots         </code> may stay in the original value and could be larger than <code dir="ltr" translate="no">          max_slots         </code> for that brief period (less than one minute).</li>
<li><code dir="ltr" translate="no">         max_slots        </code> : the maximum number of slots that could be added to the reservation by autoscaling.</li>
</ul></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       edition      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The edition associated with this reservation. For more information about editions, see <a href="/bigquery/docs/editions-intro">Introduction to BigQuery editions</a> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       primary_location      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The current location of the reservation's primary replica. This field is only set for reservations using the <a href="/bigquery/docs/managed-disaster-recovery">managed disaster recovery feature</a> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       secondary_location      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The current location of the reservation's secondary replica. This field is only set for reservations using the <a href="/bigquery/docs/managed-disaster-recovery">managed disaster recovery feature</a> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       original_primary_location      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The location where the reservation was originally created.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       labels      </code></td>
<td><code dir="ltr" translate="no">       RECORD      </code></td>
<td>Array of labels associated with the reservation.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       reservation_group_path      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The hierarchical group structure to which the reservation is linked. For example, if the group structure includes a parent group and a child group, the <code dir="ltr" translate="no">       reservation_group_path      </code> field contains a list such as: <code dir="ltr" translate="no">       [parent group, child group]      </code> . This field is in <a href="https://cloud.google.com/products#product-launch-stages">Preview</a> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       max_slots      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>The maximum number of slots that this reservation can use, which includes baseline slots ( <code dir="ltr" translate="no">       slot_capacity      </code> ), idle slots (if <code dir="ltr" translate="no">       ignore_idle_slots      </code> is false), and autoscale slots. This field is specified by users for using the <a href="/bigquery/docs/reservations-workload-management#predictable">reservation predictability feature</a> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       scaling_mode      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The scaling mode for the reservation, which determines how the reservation scales from baseline to <code dir="ltr" translate="no">       max_slots      </code> . This field is specified by users for using the <a href="/bigquery/docs/reservations-workload-management#predictable">reservation predictability feature</a> .</td>
</tr>
</tbody>
</table>

For stability, we recommend that you explicitly list columns in your information schema queries instead of using a wildcard ( `  SELECT *  ` ). Explicitly listing columns prevents queries from breaking if the underlying schema changes.

## Data retention

This view contains current reservations and deleted reservations that are kept for a maximum of 41 days after which they are removed from the view.

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
<td><code dir="ltr" translate="no">       [               PROJECT_ID              ].`region-               REGION              `.INFORMATION_SCHEMA.RESERVATION_CHANGES[_BY_PROJECT]      </code></td>
<td>Project level</td>
<td><code dir="ltr" translate="no">         REGION       </code></td>
</tr>
</tbody>
</table>

Replace the following:

  - Optional: `  PROJECT_ID  ` : the ID of your Google Cloud project. If not specified, the default project is used.
  - `  REGION  ` : any [dataset region name](/bigquery/docs/locations) . For example, ``  `region-us`  `` .
    **Note:** You must use [a region qualifier](/bigquery/docs/information-schema-intro#region_qualifier) to query `  INFORMATION_SCHEMA  ` views. The location of the query execution must match the region of the `  INFORMATION_SCHEMA  ` view.

## Example

The following example gets the history of changes for a given reservation. Use this information to see the list of changes made to a specific reservation, such as creating or deleting the reservation.

``` text
SELECT
  *
FROM
  reservation-admin-project.`region-us`.
  INFORMATION_SCHEMA.RESERVATION_CHANGES
WHERE
  reservation_name = "my-reservation"
ORDER BY
  change_timestamp DESC;
```
