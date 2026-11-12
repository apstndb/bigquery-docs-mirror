---
name: documents/docs.cloud.google.com/bigquery/docs/information-schema-assignments-changes
uri: https://docs.cloud.google.com/bigquery/docs/information-schema-assignments-changes
title: ASSIGNMENT_CHANGES view
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# ASSIGNMENT_CHANGES view

The `INFORMATION_SCHEMA.ASSIGNMENT_CHANGES` view contains a near real-time list of all changes to assignments within the administration project. Each row represents a single change to a single assignment. For more information about reservation, see [Introduction to Reservations](https://docs.cloud.google.com/bigquery/docs/reservations-intro) .

> **Note:** The view names `INFORMATION_SCHEMA.ASSIGNMENT_CHANGES` and `INFORMATION_SCHEMA.ASSIGNMENT_CHANGES_BY_PROJECT` are synonymous and can be used interchangeably.

## Required permission

To query the `INFORMATION_SCHEMA.ASSIGNMENT_CHANGES` view, you need the `bigquery.reservationAssignments.list` Identity and Access Management (IAM) permission for the project. Each of the following predefined IAM roles includes the required permission:

- `roles/bigquery.resourceAdmin`
- `roles/bigquery.resourceEditor`
- `roles/bigquery.resourceViewer`
- `roles/bigquery.user`
- `roles/bigquery.admin`

For more information about BigQuery permissions, see [Access control with IAM](https://docs.cloud.google.com/bigquery/docs/access-control) .

## Schema

The `INFORMATION_SCHEMA.ASSIGNMENT_CHANGES` view has the following schema:

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
<td><code>change_timestamp</code></td>
<td><code>TIMESTAMP</code></td>
<td>Time when the change occurred.</td>
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
<td><code>action</code></td>
<td><code>STRING</code></td>
<td>Type of event that occurred with the assignment. Can be <code>CREATE</code> , <code>UPDATE</code> , or <code>DELETE</code> .</td>
</tr>
<tr class="odd">
<td><code>user_email</code></td>
<td><code>STRING</code></td>
<td>Email address of the user or subject of the <a href="https://docs.cloud.google.com/iam/docs/workforce-identity-federation">workforce identity federation</a> that made the change. <code>google</code> for changes made by Google. <code>NULL</code> if the email address is unknown.</td>
</tr>
<tr class="even">
<td><code>state</code></td>
<td><code>STRING</code></td>
<td>State of the assignment. Can be <code>PENDING</code> or <code>ACTIVE</code> .</td>
</tr>
<tr class="odd">
<td><code>assignment_type</code></td>
<td><code>STRING</code></td>
<td>Type of the assignment. Can be <code>RESERVATION_SELECTION</code> for assignments that route jobs to a reservation, or <code>SCHEDULING_POLICY</code> for <a href="https://docs.cloud.google.com/bigquery/docs/reservations-assignments#scheduling-policy-assignments">project caps and scheduling policy overrides</a> . If a change to a reservation-selection assignment occurred before <code>assignment_type</code> tracking was supported, this value is <code>NULL</code> .</td>
</tr>
<tr class="even">
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

## Data retention

This view contains current assignments and deleted assignments that are kept for a maximum of 41 days after which they are removed from the view.

## Scope and syntax

Queries against this view must include a [region qualifier](https://docs.cloud.google.com/bigquery/docs/information-schema-intro#syntax) . If you don't specify a regional qualifier, metadata is retrieved from all regions. The following table explains the region scope for this view:

| View name                                                                                                 | Resource scope | Region scope |
|-----------------------------------------------------------------------------------------------------------|----------------|--------------|
| `[ `` PROJECT_ID ```  .]`region-  ``` REGION ```  `.INFORMATION_SCHEMA.ASSIGNMENT_CHANGES[_BY_PROJECT] `` | Project level  | `REGION`     |

Replace the following:

- Optional: `PROJECT_ID` : the ID of your Google Cloud project. If not specified, the default project is used.

- `REGION` : any [dataset region name](https://docs.cloud.google.com/bigquery/docs/locations) . For example, `` `region-us` `` .

  > **Note:** You must use [a region qualifier](https://docs.cloud.google.com/bigquery/docs/information-schema-intro#region_qualifier) to query `INFORMATION_SCHEMA` views. The location of the query execution must match the region of the `INFORMATION_SCHEMA` view.

## Examples

### Find the latest changes to an assignment

The following example displays the user who has made the latest assignment update to a particular assignment within a specified date.

```
SELECT
  user_email,
  change_timestamp,
  reservation_name,
  assignment_id
FROM
  `region-us`.INFORMATION_SCHEMA.ASSIGNMENT_CHANGES
WHERE
  change_timestamp BETWEEN '2021-09-30' AND '2021-10-01'
  AND assignment_id = 'assignment_01'
ORDER BY
  change_timestamp DESC
LIMIT 1;
```

The result is similar to the following:

```
+--------------------------------+-----------------------+--------------------+-----------------+
|           user_email           |    change_timestamp   |  reservation_name  |  assignment_id  |
+--------------------------------+-----------------------+--------------------+-----------------+
|  cloudysanfrancisco@gmail.com  |2021-09-30 09:30:00 UTC|   my_reservation   |  assignment_01  |
+--------------------------------+-----------------------+--------------------+-----------------+
```

### Identify the assignment status of a reservation at a specific point in time

The following example displays all of the active assignments of a reservation at a certain point in time.

```
SELECT
    reservation_name,
    assignee_id,
    assignee_type,
    job_type
FROM
    `region-REGION`.INFORMATION_SCHEMA.ASSIGNMENT_CHANGES
WHERE
    reservation_name = RESERVATION_NAME
    AND change_timestamp < TIMESTAMP
QUALIFY ROW_NUMBER() OVER(PARTITION BY assignee_id, job_type ORDER BY change_timestamp DESC) = 1
AND action != 'DELETE';
```

Replace the following:

- ` ``REGION`` ` : the region where your reservation is located
- ` ``RESERVATION_NAME`` ` : the name of the reservation that the assignment uses
- ` ``TIMESTAMP`` ` : the timestamp representing the specific point in time at which the list of assignments is checked

The result is similar to the following:

```
+-------------------------+---------------------------+---------------+----------+
|    reservation_name     |        assignee_id        | assignee_type | job_type |
+-------------------------+---------------------------+---------------+----------+
| test-reservation        | project_1                 | PROJECT       | QUERY    |
| test-reservation        | project_2                 | PROJECT       | QUERY    |
+-------------------------+---------------------------+---------------+----------+
```

### Identify the assignment status of a reservation when a particular job was executed

To display the assignments that were active when a certain job was executed, use the following example.

```
SELECT
    reservation_name,
    assignee_id,
    assignee_type,
    job_type
FROM
    `region-REGION`.INFORMATION_SCHEMA.ASSIGNMENT_CHANGES
WHERE
    reservation_name = RESERVATION_NAME
    AND change_timestamp < (SELECT creation_time FROM PROJECT_ID.`region-REGION`.INFORMATION_SCHEMA.JOBS WHERE job_id = JOB_ID)
QUALIFY ROW_NUMBER() OVER(PARTITION BY assignee_id, job_type ORDER BY change_timestamp DESC) = 1
AND action != 'DELETE';
```

Replace the following:

- ` ``REGION`` ` : the region where your reservation is located
- ` ``RESERVATION_NAME`` ` : the name of the reservation that the assignment uses
- ` ``PROJECT_ID`` ` : the ID of your Google Cloud project where the job was executed
- ` ``JOB_ID`` ` : the job ID against which the assignment status was checked
