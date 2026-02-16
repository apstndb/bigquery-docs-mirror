# ASSIGNMENTS view

The `  INFORMATION_SCHEMA.ASSIGNMENTS  ` view contains a near real-time list of all current assignments within the administration project. Each row represents a single, current assignment. A current assignment is either pending or active and has not been deleted. For more information about reservation, see [Introduction to Reservations](/bigquery/docs/reservations-intro) .

**Note:** The view names `  INFORMATION_SCHEMA.ASSIGNMENTS  ` and `  INFORMATION_SCHEMA.ASSIGNMENTS_BY_PROJECT  ` are synonymous and can be used interchangeably.

## Required permission

To query the `  INFORMATION_SCHEMA.ASSIGNMENTS  ` view, you need the `  bigquery.reservationAssignments.list  ` Identity and Access Management (IAM) permission for the project. Each of the following predefined IAM roles includes the required permission:

  - `  roles/bigquery.resourceAdmin  `
  - `  roles/bigquery.resourceEditor  `
  - `  roles/bigquery.resourceViewer  `
  - `  roles/bigquery.user  `
  - `  roles/bigquery.admin  `

For more information about BigQuery permissions, see [Access control with IAM](/bigquery/docs/access-control) .

## Schema

The `  INFORMATION_SCHEMA.ASSIGNMENTS  ` view has the following schema:

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
<td>The DDL statement used to create this assignment.</td>
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
<td><code dir="ltr" translate="no">       assignment_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>ID that uniquely identifies the assignment.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       reservation_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Name of the reservation that the assignment uses.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       job_type      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The type of job that can use the reservation. Can be <code dir="ltr" translate="no">       PIPELINE      </code> , <code dir="ltr" translate="no">       QUERY      </code> , <code dir="ltr" translate="no">       CONTINUOUS      </code> , <code dir="ltr" translate="no">       ML_EXTERNAL      </code> , or <code dir="ltr" translate="no">       BACKGROUND      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       assignee_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>ID that uniquely identifies the assignee resource.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       assignee_number      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>Number that uniquely identifies the assignee resource.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       assignee_type      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Type of assignee resource. Can be <code dir="ltr" translate="no">       organization      </code> , <code dir="ltr" translate="no">       folder      </code> or <code dir="ltr" translate="no">       project      </code> .</td>
</tr>
</tbody>
</table>

For stability, we recommend that you explicitly list columns in your information schema queries instead of using a wildcard ( `  SELECT *  ` ). Explicitly listing columns prevents queries from breaking if the underlying schema changes.

## Scope and syntax

Queries against this view must include a [region qualifier](/bigquery/docs/information-schema-intro#syntax) . If you don't specify a regional qualifier, metadata is retrieved from all regions. The following table explains the region scope for this view:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>View name</th>
<th>Resource scope</th>
<th>Region scope</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       [               PROJECT_ID              .]`region-               REGION              `.INFORMATION_SCHEMA.ASSIGNMENTS[_BY_PROJECT]      </code><br />
</td>
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

To run the query against a project other than your default project, add the project ID in the following format:

``` text
`PROJECT_ID`.`region-REGION_NAME`.INFORMATION_SCHEMA.ASSIGNMENTS
```

.

Replace the following:

  - PROJECT\_ID : the ID of the project to which you have assigned reservations.
  - REGION\_NAME : the name of the region.

For example, ``  `myproject`.`region-us`.INFORMATION_SCHEMA.ASSIGNMENTS  `` .

The following example gets a project's currently assigned reservation and its slot capacity. This information is useful for debugging job performance by comparing the project's slot usage with the slot capacity of the reservation assigned to that project.

``` text
SELECT
  reservation.reservation_name,
  reservation.slot_capacity
FROM
  `RESERVATION_ADMIN_PROJECT.region-REGION_NAME`.
  INFORMATION_SCHEMA.ASSIGNMENTS_BY_PROJECT assignment
INNER JOIN
  `RESERVATION_ADMIN_PROJECT.region-REGION_NAME`.
  INFORMATION_SCHEMA.RESERVATIONS_BY_PROJECT AS reservation
ON
  (assignment.reservation_name = reservation.reservation_name)
WHERE
   assignment.assignee_id = "PROJECT_ID"
  AND job_type = "QUERY";
```
