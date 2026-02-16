# INFORMATION\_SCHEMA.BI\_CAPACITY\_CHANGES view

The `  INFORMATION_SCHEMA.BI_CAPACITY_CHANGES  ` view contains history of changes to the BI Engine capacity. If you want to view the current state of BI Engine reservation, see the [`  INFORMATION_SCHEMA.BI_CAPACITIES  ` view](/bigquery/docs/information-schema-bi-capacities) .

## Required permission

To query the `  INFORMATION_SCHEMA.BI_CAPACITY_CHANGES  ` view, you need the `  bigquery.bireservations.get  ` Identity and Access Management (IAM) permission for BI Engine reservations.

For more information about BigQuery permissions, see [Access control with IAM](/bigquery/docs/access-control) .

## Schema

When you query the `  INFORMATION_SCHEMA.BI_CAPACITY_CHANGES  ` view, the query results contain one row for each update of BI Engine capacity, including the current state.

The `  INFORMATION_SCHEMA.BI_CAPACITY_CHANGES  ` view has the following schema:

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
<td>Timestamp when the current update to BI Engine capacity was made.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       project_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The project ID of the project that contains BI Engine capacity.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       project_number      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>The project number of the project that contains BI Engine capacity.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bi_capacity_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the object. There can only be one capacity per project, hence the name is always <code dir="ltr" translate="no">       default      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       size      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>BI Engine RAM in bytes.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       user_email      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Email address of the user or subject of the <a href="/iam/docs/workforce-identity-federation">workforce identity federation</a> that made the change. <code dir="ltr" translate="no">       google      </code> for changes made by Google. <code dir="ltr" translate="no">       NULL      </code> if the email address is unknown.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       preferred_tables      </code></td>
<td><code dir="ltr" translate="no">       REPEATED STRING      </code></td>
<td>The set of preferred tables this BI Engine capacity must be used for. If set to <code dir="ltr" translate="no">       null      </code> , BI Engine capacity is used for all queries in the current project.</td>
</tr>
</tbody>
</table>

For stability, we recommend that you explicitly list columns in your information schema queries instead of using a wildcard ( `  SELECT *  ` ). Explicitly listing columns prevents queries from breaking if the underlying schema changes.

## Syntax

Queries against this view must include a [region qualifier](/bigquery/docs/information-schema-intro#syntax) . A project ID is optional. If no project ID is specified, the project that the query runs in is used.

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
<td><code dir="ltr" translate="no">       [               PROJECT_ID              .]`region-               REGION              `.INFORMATION_SCHEMA.BI_CAPACITY_CHANGES      </code></td>
<td>Project level</td>
<td><code dir="ltr" translate="no">         REGION       </code></td>
</tr>
</tbody>
</table>

Replace the following:

  - Optional: `  PROJECT_ID  ` : the ID of your Google Cloud project. If not specified, the default project is used.
  - `  REGION  ` : any [dataset region name](/bigquery/docs/locations) . For example, ``  `region-us`  `` .
    **Note:** You must use [a region qualifier](/bigquery/docs/information-schema-intro#region_qualifier) to query `  INFORMATION_SCHEMA  ` views. The location of the query execution must match the region of the `  INFORMATION_SCHEMA  ` view.

<!-- end list -->

``` text
-- Returns the history of BI Engine capacity.
SELECT * FROM myproject.`region-us`.INFORMATION_SCHEMA.BI_CAPACITY_CHANGES;
```

## Examples

The following example retrieves the current BI Engine capacity changes from the `  INFORMATION_SCHEMA.BI_CAPACITY_CHANGES  ` view.

To run the query against a project other than the project that the query is running in, add the project ID to the region in the following format: ``  ` project_id `.` region_id `.INFORMATION_SCHEMA.BI_CAPACITY_CHANGES  `` .

The following example gets all changes made to BI Engine capacity by a user with email `  email@mycompanymail.com  ` :

``` text
SELECT *
FROM `my-project-id.region-us`.INFORMATION_SCHEMA.BI_CAPACITY_CHANGES
WHERE user_email = "email@mycompanymail.com"
```

The result looks similar to the following:

``` text
  +---------------------+---------------+----------------+------------------+--------------+---------------------+----------------------------------------------------------------------------------------+
  |  change_timestamp   |  project_id   | project_number | bi_capacity_name |     size     |     user_email      |                                               preferred_tables                         |
  +---------------------+---------------+----------------+------------------+--------------+---------------------+----------------------------------------------------------------------------------------+
  | 2022-06-14 02:22:18 | my-project-id |   123456789000 | default          | 268435456000 | email@mycompany.com | ["my-project-id.dataset1.table1","bigquery-public-data.chicago_taxi_trips.taxi_trips"] |
  | 2022-06-08 20:25:51 | my-project-id |   123456789000 | default          | 268435456000 | email@mycompany.com | ["bigquery-public-data.chicago_taxi_trips.taxi_trips"]                                 |
  | 2022-04-01 21:06:49 | my-project-id |   123456789000 | default          | 161061273600 | email@mycompany.com | [""]                                                                                   |
  +---------------------+---------------+----------------+------------------+--------------+---------------------+----------------------------------------------------------------------------------------+
  
```

The following example gets BI Engine capacity changes for the last seven days:

``` text
SELECT
  change_timestamp,
  size,
  user_email,
  preferred_tables
FROM `my-project-id.region-us`.INFORMATION_SCHEMA.BI_CAPACITY_CHANGES
WHERE change_timestamp > TIMESTAMP_SUB(CURRENT_DATE(), INTERVAL 7 DAY)
```

The result looks similar to the following:

``` text
  +---------------------+--------------+----------------------+-------------------+
  |  change_timestamp   |     size     |     user_email       |  preferred_tables |                                                                                    |
  +---------------------+--------------+----------------------+-------------------+
  | 2023-07-08 18:25:09 | 268435456000 | sundar@mycompany.com | [""]              |
  | 2023-07-09 17:47:26 | 161061273600 | pichai@mycompany.com | ["pr.dataset.t1"] |
  +---------------------+--------------+----------------------+-------------------+
  
```
