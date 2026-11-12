---
name: documents/docs.cloud.google.com/bigquery/docs/information-schema-assignments
uri: https://docs.cloud.google.com/bigquery/docs/information-schema-assignments
title: ASSIGNMENTS view
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# ASSIGNMENTS view

The `INFORMATION_SCHEMA.ASSIGNMENTS` view contains a near real-time list of all current assignments within the administration project. Each row represents a single, current assignment. A current assignment is either pending or active and has not been deleted. For more information about reservations, see [Introduction to Reservations](https://docs.cloud.google.com/bigquery/docs/reservations-intro) .

> **Note:** The view names `INFORMATION_SCHEMA.ASSIGNMENTS` and `INFORMATION_SCHEMA.ASSIGNMENTS_BY_PROJECT` are synonymous and can be used interchangeably.

## Required permission

To query the `INFORMATION_SCHEMA.ASSIGNMENTS` view, you need the `bigquery.reservationAssignments.list` Identity and Access Management (IAM) permission for the project. Each of the following predefined IAM roles includes the required permission:

- `roles/bigquery.resourceAdmin`
- `roles/bigquery.resourceEditor`
- `roles/bigquery.resourceViewer`
- `roles/bigquery.user`
- `roles/bigquery.admin`

For more information about BigQuery permissions, see [Access control with IAM](https://docs.cloud.google.com/bigquery/docs/access-control) .

## Schema

The `INFORMATION_SCHEMA.ASSIGNMENTS` view has the following schema:

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
<td><code>ddl</code></td>
<td><code>STRING</code></td>
<td>The DDL statement used to create this assignment.</td>
</tr>
<tr class="even">
<td><code>project_id</code></td>
<td><code>STRING</code></td>
<td>ID of the administration project.</td>
</tr>
<tr class="odd">
<td><code>project_number</code></td>
<td><code>INTEGER</code></td>
<td>Number of the administration project.</td>
</tr>
<tr class="even">
<td><code>assignment_id</code></td>
<td><code>STRING</code></td>
<td>ID that uniquely identifies the assignment.</td>
</tr>
<tr class="odd">
<td><code>reservation_name</code></td>
<td><code>STRING</code></td>
<td>Name of the reservation that the assignment uses.</td>
</tr>
<tr class="even">
<td><code>job_type</code></td>
<td><code>STRING</code></td>
<td>The type of job that can use the reservation. Can be <code>PIPELINE</code> , <code>QUERY</code> , <code>CONTINUOUS</code> , <code>ML_EXTERNAL</code> , or <code>BACKGROUND</code> . When <code>assignment_type</code> is <code>SCHEDULING_POLICY</code> , this value is <code>JOB_TYPE_UNSPECIFIED</code> .</td>
</tr>
<tr class="odd">
<td><code>assignee_id</code></td>
<td><code>STRING</code></td>
<td>ID that uniquely identifies the assignee resource.</td>
</tr>
<tr class="even">
<td><code>assignee_number</code></td>
<td><code>INTEGER</code></td>
<td>Number that uniquely identifies the assignee resource.</td>
</tr>
<tr class="odd">
<td><code>assignee_type</code></td>
<td><code>STRING</code></td>
<td>Type of assignee resource. Can be <code>organization</code> , <code>folder</code> or <code>project</code> .</td>
</tr>
<tr class="even">
<td><code>assignment_type</code></td>
<td><code>STRING</code></td>
<td>Type of the assignment. Can be <code>RESERVATION_SELECTION</code> for assignments that route jobs to a reservation, or <code>SCHEDULING_POLICY</code> for <a href="https://docs.cloud.google.com/bigquery/docs/reservations-assignments#scheduling-policy-assignments">project caps and scheduling policy overrides</a> . If a reservation-selection assignment was created before <code>assignment_type</code> tracking was supported and hasn't been updated since, this value is <code>NULL</code> .</td>
</tr>
<tr class="odd">
<td><code>scheduling_policy</code></td>
<td><code>STRUCT</code></td>
<td><p>Project-specific <a href="https://docs.cloud.google.com/bigquery/docs/reservations-assignments#scheduling-policy-assignments">project caps and scheduling policy overrides</a> for <code>assignee_id</code> within the reservation, or <code>NULL</code> if <code>assignment_type</code> isn't <code>SCHEDULING_POLICY</code> . Fields include the following:</p>
<ul>
<li><code>max_slots</code> : the limit on the slot consumption of queries running for <code>assignee_id</code> in the reservation, or <code>NULL</code> if unset.</li>
<li><code>concurrency</code> : the limit on the number of simultaneous queries admitted for <code>assignee_id</code> in the reservation, or <code>NULL</code> if unset.</li>
</ul></td>
</tr>
</tbody>
</table>

For stability, we recommend that you explicitly list columns in your information schema queries instead of using a wildcard ( `SELECT *` ). Explicitly listing columns prevents queries from breaking if the underlying schema changes.

## Scope and syntax

Queries against this view must include a [region qualifier](https://docs.cloud.google.com/bigquery/docs/information-schema-intro#syntax) . If you don't specify a regional qualifier, metadata is retrieved from all regions. The following table explains the region scope for this view:

| View name                                                                                          | Resource scope | Region scope |
|----------------------------------------------------------------------------------------------------|----------------|--------------|
| `[ `` PROJECT_ID ```  .]`region-  ``` REGION ```  `.INFORMATION_SCHEMA.ASSIGNMENTS[_BY_PROJECT] `` | Project level  | `REGION`     |

Replace the following:

- Optional: `PROJECT_ID` : the ID of your Google Cloud project. If not specified, the default project is used.

- `REGION` : any [dataset region name](https://docs.cloud.google.com/bigquery/docs/locations) . For example, `` `region-us` `` .

  > **Note:** You must use [a region qualifier](https://docs.cloud.google.com/bigquery/docs/information-schema-intro#region_qualifier) to query `INFORMATION_SCHEMA` views. The location of the query execution must match the region of the `INFORMATION_SCHEMA` view.

## Example

To run the query against a project other than your default project, add the project ID in the following format:

```
`PROJECT_ID`.`region-REGION_NAME`.INFORMATION_SCHEMA.ASSIGNMENTS
```

.

Replace the following:

- ` PROJECT_ID ` : the ID of the project to which you have assigned reservations.
- ` REGION_NAME ` : the name of the region.

For example, `` `myproject`.`region-us`.INFORMATION_SCHEMA.ASSIGNMENTS `` .

The following example gets a project's currently assigned reservation and its slot capacity. This information is useful for debugging job performance by comparing the project's slot usage with the slot capacity of the reservation assigned to that project.

```
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
