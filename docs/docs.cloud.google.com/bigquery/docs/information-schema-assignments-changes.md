# ASSIGNMENT\_CHANGES view

The `  INFORMATION_SCHEMA.ASSIGNMENT_CHANGES  ` view contains a near real-time list of all changes to assignments within the administration project. Each row represents a single change to a single assignment. For more information about reservation, see [Introduction to Reservations](/bigquery/docs/reservations-intro) .

**Note:** The view names `  INFORMATION_SCHEMA.ASSIGNMENT_CHANGES  ` and `  INFORMATION_SCHEMA.ASSIGNMENT_CHANGES_BY_PROJECT  ` are synonymous and can be used interchangeably.

## Required permission

To query the `  INFORMATION_SCHEMA.ASSIGNMENT_CHANGES  ` view, you need the `  bigquery.reservationAssignments.list  ` Identity and Access Management (IAM) permission for the project. Each of the following predefined IAM roles includes the required permission:

  - `  roles/bigquery.resourceAdmin  `
  - `  roles/bigquery.resourceEditor  `
  - `  roles/bigquery.resourceViewer  `
  - `  roles/bigquery.user  `
  - `  roles/bigquery.admin  `

For more information about BigQuery permissions, see [Access control with IAM](/bigquery/docs/access-control) .

## Schema

The `  INFORMATION_SCHEMA.ASSIGNMENT_CHANGES  ` view has the following schema:

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
<td>The type of job that can use the reservation. Can be <code dir="ltr" translate="no">       PIPELINE      </code> or <code dir="ltr" translate="no">       QUERY      </code> .</td>
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
<tr class="even">
<td><code dir="ltr" translate="no">       action      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Type of event that occurred with the assignment. Can be <code dir="ltr" translate="no">       CREATE      </code> , <code dir="ltr" translate="no">       UPDATE      </code> , or <code dir="ltr" translate="no">       DELETE      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       user_email      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Email address of the user or subject of the <a href="/iam/docs/workforce-identity-federation">workforce identity federation</a> that made the change. <code dir="ltr" translate="no">       google      </code> for changes made by Google. <code dir="ltr" translate="no">       NULL      </code> if the email address is unknown.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       state      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>State of the assignment. Can be <code dir="ltr" translate="no">       PENDING      </code> or <code dir="ltr" translate="no">       ACTIVE      </code> .</td>
</tr>
</tbody>
</table>

For stability, we recommend that you explicitly list columns in your information schema queries instead of using a wildcard ( `  SELECT *  ` ). Explicitly listing columns prevents queries from breaking if the underlying schema changes.

## Data retention

This view contains current assignments and deleted assignments that are kept for a maximum of 41 days after which they are removed from the view.

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
<td><code dir="ltr" translate="no">       [               PROJECT_ID              .]`region-               REGION              `.INFORMATION_SCHEMA.ASSIGNMENT_CHANGES[_BY_PROJECT]      </code></td>
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

### Find the latest changes to an assignment

The following example displays the user who has made the latest assignment update to a particular assignment within a specified date.

``` text
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

``` text
+--------------------------------+-----------------------+--------------------+-----------------+
|           user_email           |    change_timestamp   |  reservation_name  |  assignment_id  |
+--------------------------------+-----------------------+--------------------+-----------------+
|  cloudysanfrancisco@gmail.com  |2021-09-30 09:30:00 UTC|   my_reservation   |  assignment_01  |
+--------------------------------+-----------------------+--------------------+-----------------+
```

### Identify the assignment status of a reservation at a specific point in time

The following example displays all of the active assignments of a reservation at a certain point in time.

``` text
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

  - `  REGION  ` : the region where your reservation is located
  - `  RESERVATION_NAME  ` : the name of the reservation that the assignment uses
  - `  TIMESTAMP  ` : the timestamp representing the specific point in time at which the list of assignments is checked

The result is similar to the following:

``` text
+-------------------------+---------------------------+---------------+----------+
|    reservation_name     |        assignee_id        | assignee_type | job_type |
+-------------------------+---------------------------+---------------+----------+
| test-reservation        | project_1                 | PROJECT       | QUERY    |
| test-reservation        | project_2                 | PROJECT       | QUERY    |
+-------------------------+---------------------------+---------------+----------+
```

### Identify the assignment status of a reservation when a particular job was executed

To display the assignments that were active when a certain job was executed, use the following example.

``` text
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

  - `  REGION  ` : the region where your reservation is located
  - `  RESERVATION_NAME  ` : the name of the reservation that the assignment uses
  - `  PROJECT_ID  ` : the ID of your Google Cloud project where the job was executed
  - `  JOB_ID  ` : the job ID against which the assignment status was checked
