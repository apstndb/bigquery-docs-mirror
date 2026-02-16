# CAPACITY\_COMMITMENTS view

The `  INFORMATION_SCHEMA.CAPACITY_COMMITMENTS  ` view contains a near real-time list of all current capacity commitments within the administration project. Each row represents a single, current capacity commitment. A current capacity commitment is either pending or active and has not been deleted. For more information about reservation, see [Slot commitments](/bigquery/docs/reservations-workload-management#slot_commitments) .

**Note:** The view names `  INFORMATION_SCHEMA.CAPACITY_COMMITMENTS  ` and `  INFORMATION_SCHEMA.CAPACITY_COMMITMENTS_BY_PROJECT  ` are synonymous and can be used interchangeably.

## Required permission

To query the `  INFORMATION_SCHEMA.CAPACITY_COMMITMENTS  ` view, you need the `  bigquery.capacityCommitments.list  ` Identity and Access Management (IAM) permission for the project. Each of the following predefined IAM roles includes the required permission:

  - `  roles/bigquery.resourceAdmin  `
  - `  roles/bigquery.resourceEditor  `
  - `  roles/bigquery.resourceViewer  `
  - `  roles/bigquery.user  `
  - `  roles/bigquery.admin  `

For more information about BigQuery permissions, see [Access control with IAM](/bigquery/docs/access-control)

## Schema

The `  INFORMATION_SCHEMA.CAPACITY_COMMITMENTS  ` view has the following schema:

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
<td><code dir="ltr" translate="no">       ddl      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The DDL statement used to create this capacity commitment.</td>
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
<td><code dir="ltr" translate="no">       edition      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The edition associated with this reservation. For more information about editions, see <a href="/bigquery/docs/editions-intro">Introduction to BigQuery editions</a> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       is_flat_rate      </code></td>
<td><code dir="ltr" translate="no">       BOOL      </code></td>
<td>Whether the commitment is associated with the legacy flat-rate capacity model or an edition. If <code dir="ltr" translate="no">       FALSE      </code> , the current commitment is associated with an edition. If <code dir="ltr" translate="no">       TRUE      </code> , the commitment is the legacy flat-rate capacity model.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       renewal_plan      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>New commitment plan after the end of current commitment plan. You can change the renewal plan for a commitment at any time until it expires.</td>
</tr>
</tbody>
</table>

For stability, we recommend that you explicitly list columns in your information schema queries instead of using a wildcard ( `  SELECT *  ` ). Explicitly listing columns prevents queries from breaking if the underlying schema changes.

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
<td><code dir="ltr" translate="no">       [               PROJECT_ID              .]`region-               REGION              `.INFORMATION_SCHEMA.CAPACITY_COMMITMENTS[_BY_PROJECT]      </code></td>
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

The following example returns a list of active capacity commitments for the current project:

``` text
SELECT
  capacity_commitment_id,
  slot_count
FROM
  `region-us`.INFORMATION_SCHEMA.CAPACITY_COMMITMENTS
WHERE
  state = 'ACTIVE';
```

The result is similar to the following:

``` text
+------------------------+------------+
| capacity_commitment_id | slot_count |
+------------------------+------------+
|    my_commitment_05    |    1000    |
|    my_commitment_06    |    1000    |
|    my_commitment_07    |    1500    |
|    my_commitment_08    |    2000    |
+------------------------+------------+
```
