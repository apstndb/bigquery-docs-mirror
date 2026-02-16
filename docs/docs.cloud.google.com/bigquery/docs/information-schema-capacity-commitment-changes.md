# CAPACITY\_COMMITMENT\_CHANGES view

The `  INFORMATION_SCHEMA.CAPACITY_COMMITMENT_CHANGES  ` view contains a near real-time list of all changes to capacity commitments within the administration project. Each row represents a single change to a single capacity commitment. For more information, see [Slot commitments](/bigquery/docs/reservations-workload-management#slot_commitments) .

**Note:** The view names `  INFORMATION_SCHEMA.CAPACITY_COMMITMENT_CHANGES  ` and `  INFORMATION_SCHEMA.CAPACITY_COMMITMENT_CHANGES_BY_PROJECT  ` are synonymous and can be used interchangeably.

## Required permission

To query the `  INFORMATION_SCHEMA.CAPACITY_COMMITMENT_CHANGES  ` view, you need the `  bigquery.capacityCommitments.list  ` Identity and Access Management (IAM) permission for the project. Each of the following predefined IAM roles includes the required permission:

  - `  roles/bigquery.resourceAdmin  `
  - `  roles/bigquery.resourceEditor  `
  - `  roles/bigquery.resourceViewer  `
  - `  roles/bigquery.user  `
  - `  roles/bigquery.admin  `

For more information about BigQuery permissions, see [Access control with IAM](/bigquery/docs/access-control) .

## Schema

The `  INFORMATION_SCHEMA.CAPACITY_COMMITMENT_CHANGES  ` view has the following schema:

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
<td><code dir="ltr" translate="no">       capacity_commitment_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>ID that uniquely identifies the capacity commitment.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       commitment_plan      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Commitment plan of the capacity commitment.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       state      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>State the capacity commitment is in. Can be <code dir="ltr" translate="no">       PENDING      </code> or <code dir="ltr" translate="no">       ACTIVE      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       slot_count      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>Slot count associated with the capacity commitment.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       action      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Type of event that occurred with the capacity commitment. Can be <code dir="ltr" translate="no">       CREATE      </code> , <code dir="ltr" translate="no">       UPDATE      </code> , or <code dir="ltr" translate="no">       DELETE      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       user_email      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Email address of the user or subject of the <a href="/iam/docs/workforce-identity-federation">workforce identity federation</a> that made the change. <code dir="ltr" translate="no">       google      </code> for changes made by Google. <code dir="ltr" translate="no">       NULL      </code> if the email address is unknown.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       commitment_start_time      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>The start of the current commitment period. Only applicable for <code dir="ltr" translate="no">       ACTIVE      </code> capacity commitments, otherwise this is <code dir="ltr" translate="no">       NULL      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       commitment_end_time      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>The end of the current commitment period. Only applicable for <code dir="ltr" translate="no">       ACTIVE      </code> capacity commitments, otherwise this is <code dir="ltr" translate="no">       NULL      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       failure_status      </code></td>
<td><code dir="ltr" translate="no">       RECORD      </code></td>
<td>For a <code dir="ltr" translate="no">       FAILED      </code> commitment plan, provides the failure reason, otherwise this is <code dir="ltr" translate="no">       NULL      </code> . <code dir="ltr" translate="no">       RECORD      </code> consists of <code dir="ltr" translate="no">       code      </code> and <code dir="ltr" translate="no">       message      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       renewal_plan      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The plan this capacity commitment is converted to after <code dir="ltr" translate="no">       commitment_end_time      </code> passes. After the plan is changed, the committed period is extended according to the commitment plan. Only applicable for <code dir="ltr" translate="no">       ANNUAL      </code> and <code dir="ltr" translate="no">       TRIAL      </code> commitments, otherwise this is <code dir="ltr" translate="no">       NULL      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       edition      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The edition associated with this reservation. For more information about editions, see <a href="/bigquery/docs/editions-intro">Introduction to BigQuery editions</a> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       is_flat_rate      </code></td>
<td><code dir="ltr" translate="no">       BOOL      </code></td>
<td>Whether the commitment is associated with the legacy flat-rate capacity model or an edition. If <code dir="ltr" translate="no">       FALSE      </code> , the current commitment is associated with an edition. If <code dir="ltr" translate="no">       TRUE      </code> , the commitment is the legacy flat-rate capacity model.</td>
</tr>
</tbody>
</table>

For stability, we recommend that you explicitly list columns in your information schema queries instead of using a wildcard ( `  SELECT *  ` ). Explicitly listing columns prevents queries from breaking if the underlying schema changes.

## Data retention

This view contains current capacity commitments and the deleted capacity commitments that are kept for a maximum of 41 days after which they are removed from the view.

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
<td><code dir="ltr" translate="no">       [               PROJECT_ID              .]`region-               REGION              `.INFORMATION_SCHEMA.CAPACITY_COMMITMENT_CHANGES[_BY_PROJECT]      </code></td>
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

The following query displays the user who has made the latest capacity commitment update to the current project within the specified date.

``` text
SELECT
  user_email,
  change_timestamp
FROM
  `region-us`.INFORMATION_SCHEMA.CAPACITY_COMMITMENT_CHANGES
WHERE
  change_timestamp BETWEEN '2021-09-30' AND '2021-10-01'
ORDER BY
  change_timestamp DESC
LIMIT 1;
```

The result is similar to the following:

``` text
+--------------------------------+-------------------------+
|           user_email           |     change_timestamp    |
+--------------------------------+-------------------------+
|     222larabrown@gmail.com     | 2021-09-30 09:30:00 UTC |
+--------------------------------+-------------------------+
```
