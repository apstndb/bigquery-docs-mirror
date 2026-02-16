# TABLE\_SNAPSHOTS view

The `  INFORMATION_SCHEMA.TABLE_SNAPSHOTS  ` view contains metadata about your table snapshots. For more information, see [Introduction to table snapshots](/bigquery/docs/table-snapshots-intro) .

## Required permissions

To query the `  INFORMATION_SCHEMA.TABLE_SNAPSHOTS  ` view, you need the `  bigquery.tables.list  ` Identity and Access Management (IAM) permission for the dataset. The `  roles/bigquery.metadataViewer  ` predefined role includes the required permission.

For more information about BigQuery permissions, see [Access control with IAM](/bigquery/docs/access-control) .

## Schema

When you query the `  INFORMATION_SCHEMA.TABLE_SNAPSHOTS  ` table, the results contain one row for each table snapshot in the specified dataset or region.

The `  INFORMATION_SCHEMA.TABLE_SNAPSHOTS  ` table has the following schema. The standard table that the table snapshot was taken from is called the *base table* .

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
<td><code dir="ltr" translate="no">       table_catalog      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the project that contains the table snapshot</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       table_schema      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the dataset that contains the table snapshot</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       table_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the table snapshot</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       base_table_catalog      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the project that contains the base table</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       base_table_schema      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the dataset that contains the base table</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       base_table_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the base table</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       snapshot_time      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>The time that the table snapshot was created</td>
</tr>
</tbody>
</table>

For stability, we recommend that you explicitly list columns in your information schema queries instead of using a wildcard ( `  SELECT *  ` ). Explicitly listing columns prevents queries from breaking if the underlying schema changes.

## Scope and syntax

Queries against this view must include a dataset or a region qualifier. For queries with a dataset qualifier, you must have permissions for the dataset. For queries with a region qualifier, you must have permissions for the project. For more information see [Syntax](/bigquery/docs/information-schema-intro#syntax) . The following table explains the region and resource scopes for this view:

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
<td><code dir="ltr" translate="no">       [`               PROJECT_ID              `.]`region-               REGION              `.INFORMATION_SCHEMA.TABLE_SNAPSHOTS      </code></td>
<td>Project level</td>
<td><code dir="ltr" translate="no">         REGION       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       [`               PROJECT_ID              `.]               DATASET_ID              .INFORMATION_SCHEMA.TABLE_SNAPSHOTS      </code></td>
<td>Dataset level</td>
<td>Dataset location</td>
</tr>
</tbody>
</table>

Replace the following:

  - Optional: `  PROJECT_ID  ` : the ID of your Google Cloud project. If not specified, the default project is used.
  - `  REGION  ` : any [dataset region name](/bigquery/docs/locations) . For example, ``  `region-us`  `` .
  - `  DATASET_ID  ` : the ID of your dataset. For more information, see [Dataset qualifier](/bigquery/docs/information-schema-intro#dataset_qualifier) .
    **Note:** You must use [a region qualifier](/bigquery/docs/information-schema-intro#region_qualifier) to query `  INFORMATION_SCHEMA  ` views. The location of the query execution must match the region of the `  INFORMATION_SCHEMA  ` view.

**Example**

``` text
-- Returns metadata for the table snapshots in the specified dataset.
SELECT * FROM myDataset.INFORMATION_SCHEMA.TABLE_SNAPSHOTS;

-- Returns metadata for the table snapshots in the specified region.
SELECT * FROM `region-us`.INFORMATION_SCHEMA.TABLE_SNAPSHOTS;
```

## Example

The following query retrieves metadata for the table snapshots in the `  mydataset  ` dataset. In this example, it displays the table snapshot `  myproject.mydataset.mytablesnapshot  ` , which was taken from the base table `  myproject.mydataset.mytable  ` on May 14, 2021, at 12 PM UTC.

``` text
SELECT *
FROM
  `myproject`.mydataset.INFORMATION_SCHEMA.TABLE_SNAPSHOTS;
```

The result is similar to the following:

``` text
+----------------+---------------+-----------------+--------------------+-------------------+-----------------+-----------------------------+
| table_catalog  | table_schema  | table_name      | base_table_catalog | base_table_schema | base_table_name | snapshot_time               |
+----------------+---------------+-----------------+----------------------------------------------------------------------------------------+
| myproject      | mydataset     | mytablesnapshot | myProject          | mydataset         | mytable         | 2021-05-14 12:00:00.000 UTC |
+----------------+---------------+-----------------+--------------------+-------------------+-----------------+-----------------------------+
```
