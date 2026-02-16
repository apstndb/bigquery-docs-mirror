# INFORMATION\_SCHEMA.BI\_CAPACITIES view

The `  INFORMATION_SCHEMA.BI_CAPACITIES  ` view contains metadata about the current state of BI Engine capacity. If you want to view the history of changes to BI Engine reservation, see the [`  INFORMATION_SCHEMA.BI_CAPACITY_CHANGES  ` view](/bigquery/docs/information-schema-bi-capacity-changes) .

## Required permission

To query the `  INFORMATION_SCHEMA.BI_CAPACITIES  ` view, you need the `  bigquery.bireservations.get  ` Identity and Access Management (IAM) permission for BI Engine reservations.

For more information about BigQuery permissions, see [Access control with IAM](/bigquery/docs/access-control) .

## Schema

When you query the `  INFORMATION_SCHEMA.BI_CAPACITIES  ` view, the query results contain one row with current state of BI Engine capacity.

The `  INFORMATION_SCHEMA.BI_CAPACITIES  ` view has the following schema:

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
<td><code dir="ltr" translate="no">       project_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The project ID of the project that contains BI Engine capacity.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       project_number      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>The project number of the project that contains BI Engine capacity.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       bi_capacity_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the object. There can only be one capacity per project, hence the name is always set to <code dir="ltr" translate="no">       default      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       size      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>BI Engine RAM in bytes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       preferred_tables      </code></td>
<td><code dir="ltr" translate="no">       REPEATED STRING      </code></td>
<td>Set of preferred tables this BI Engine capacity must be used for. If set to <code dir="ltr" translate="no">       null      </code> , BI Engine capacity is used for all queries in the current project</td>
</tr>
</tbody>
</table>

For stability, we recommend that you explicitly list columns in your information schema queries instead of using a wildcard ( `  SELECT *  ` ). Explicitly listing columns prevents queries from breaking if the underlying schema changes.

## Scope and syntax

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
<td><code dir="ltr" translate="no">       [               PROJECT_ID              .]`region-               REGION              `.INFORMATION_SCHEMA.BI_CAPACITIES      </code></td>
<td>Project level</td>
<td><code dir="ltr" translate="no">         REGION       </code></td>
</tr>
</tbody>
</table>

Replace the following:

  - Optional: `  PROJECT_ID  ` : the ID of your Google Cloud project. If not specified, the default project is used.
  - `  REGION  ` : any [dataset region name](/bigquery/docs/locations) . For example, ``  `region-us`  `` .
    **Note:** You must use [a region qualifier](/bigquery/docs/information-schema-intro#region_qualifier) to query `  INFORMATION_SCHEMA  ` views. The location of the query execution must match the region of the `  INFORMATION_SCHEMA  ` view.

**Example**

``` text
-- Returns current state of BI Engine capacity.
SELECT * FROM myproject.`region-us`.INFORMATION_SCHEMA.BI_CAPACITIES;
```

## Examples

The following example retrieves current BI Engine capacity changes from `  INFORMATION_SCHEMA.BI_CAPACITIES  ` view.

To run the query against a project other than the project that the query is running in, add the project ID to the region in the following format: ``  ` project_id `.` region_id `.INFORMATION_SCHEMA.BI_CAPACITIES  `` .

The following example shows the current state of BI Engine in the project with id 'my-project-id':

``` text
SELECT *
FROM `my-project-id.region-us`.INFORMATION_SCHEMA.BI_CAPACITIES
```

The result looks similar to the following:

``` text
  +---------------+----------------+------------------+--------------+-----------------------------------------------------------------------------------------------+
  |  project_id   | project_number | bi_capacity_name |     size     |                                               preferred_tables                                |
  +---------------+----------------+------------------+--------------+-----------------------------------------------------------------------------------------------+
  | my-project-id |   123456789000 | default          | 268435456000 | "my-company-project-id.dataset1.table1","bigquery-public-data.chicago_taxi_trips.taxi_trips"] |
  +---------------+----------------+------------------+--------------+-----------------------------------------------------------------------------------------------+
  
```

The following example returns size of BI Engine capacity in gigabytes for the query project:

``` text
SELECT
  project_id,
  size/1024.0/1024.0/1024.0 AS size_gb
FROM `region-us`.INFORMATION_SCHEMA.BI_CAPACITIES
```

The result looks similar to the following:

``` text
  +---------------+---------+
  |  project_id   | size_gb |
  +---------------+---------+
  | my-project-id |  250.0  |
  +---------------+---------+
  
```
