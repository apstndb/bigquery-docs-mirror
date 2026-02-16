# SEARCH\_INDEX\_COLUMNS view

The `  INFORMATION_SCHEMA.SEARCH_INDEX_COLUMNS  ` view contains one row for each search-indexed column on each table in a dataset.

## Required permissions

To see [search index](/bigquery/docs/search-index) metadata, you need the `  bigquery.tables.get  ` or `  bigquery.tables.list  ` Identity and Access Management (IAM) permission on the table with the index. Each of the following predefined IAM roles includes at least one of these permissions:

  - `  roles/bigquery.admin  `
  - `  roles/bigquery.dataEditor  `
  - `  roles/bigquery.dataOwner  `
  - `  roles/bigquery.dataViewer  `
  - `  roles/bigquery.metadataViewer  `
  - `  roles/bigquery.user  `

For more information about BigQuery permissions, see [Access control with IAM](/bigquery/docs/access-control) .

## Schema

When you query the `  INFORMATION_SCHEMA.SEARCH_INDEX_COLUMNS  ` view, the query results contain one row for each indexed column on each table in a dataset.

The `  INFORMATION_SCHEMA.SEARCH_INDEX_COLUMNS  ` view has the following schema:

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
<td><code dir="ltr" translate="no">       index_catalog      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the project that contains the dataset.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       index_schema      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the dataset that contains the index.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       table_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the base table that the index is created on.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       index_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the index.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       index_column_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the top-level indexed column.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       index_field_path      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The full path of the expanded indexed field, starting with the column name. Fields are separated by a period.</td>
</tr>
</tbody>
</table>

For stability, we recommend that you explicitly list columns in your information schema queries instead of using a wildcard ( `  SELECT *  ` ). Explicitly listing columns prevents queries from breaking if the underlying schema changes.

## Scope and syntax

Queries against this view must have a [dataset qualifier](/bigquery/docs/information-schema-intro#syntax) . The following table explains the region scope for this view:

<table>
<thead>
<tr class="header">
<th>View Name</th>
<th>Resource scope</th>
<th>Region scope</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       [               PROJECT_ID              .]               DATASET_ID              .INFORMATION_SCHEMA.SEARCH_INDEX_COLUMNS      </code></td>
<td>Dataset level</td>
<td>Dataset location</td>
</tr>
</tbody>
</table>

Replace the following:

  - Optional: `  PROJECT_ID  ` : the ID of your Google Cloud project. If not specified, the default project is used.
  - `  DATASET_ID  ` : the ID of your dataset. For more information, see [Dataset qualifier](/bigquery/docs/information-schema-intro#dataset_qualifier) .

**Example**

``` text
-- Returns metadata for search indexes in a single dataset.
SELECT * FROM myDataset.INFORMATION_SCHEMA.SEARCH_INDEX_COLUMNS;
```

## Examples

The following example creates a search index on all columns of `  my_table  ` .

``` text
CREATE TABLE dataset.my_table(
  a STRING,
  b INT64,
  c STRUCT <d INT64,
            e ARRAY<STRING>,
            f STRUCT<g STRING, h INT64>>) AS
SELECT 'hello' AS a, 10 AS b, (20, ['x', 'y'], ('z', 30)) AS c;

CREATE SEARCH INDEX my_index
ON dataset.my_table(ALL COLUMNS);
```

The following query extracts information on which fields are indexed. The `  index_field_path  ` indicates which field of a column is indexed. This differs from the `  index_column_name  ` only in the case of a `  STRUCT  ` , where the full path to the indexed field is given. In this example, column `  c  ` contains an `  ARRAY<STRING>  ` field `  e  ` and another `  STRUCT  ` called `  f  ` which contains a `  STRING  ` field `  g  ` , each of which is indexed.

``` text
SELECT table_name, index_name, index_column_name, index_field_path
FROM my_project.dataset.INFORMATION_SCHEMA.SEARCH_INDEX_COLUMNS
```

The result is similar to the following:

``` text
+------------+------------+-------------------+------------------+
| table_name | index_name | index_column_name | index_field_path |
+------------+------------+-------------------+------------------+
| my_table   | my_index   | a                 | a                |
| my_table   | my_index   | c                 | c.e              |
| my_table   | my_index   | c                 | c.f.g            |
+------------+------------+-------------------+------------------+
```

The following query joins the `  INFORMATION_SCHEMA.SEARCH_INDEX_COUMNS  ` view with the `  INFORMATION_SCHEMA.SEARCH_INDEXES  ` and `  INFORMATION_SCHEMA.COLUMNS  ` views to include the search index status and the data type of each column:

``` text
SELECT
  index_columns_view.index_catalog AS project_name,
  index_columns_view.index_SCHEMA AS dataset_name,
  indexes_view.TABLE_NAME AS table_name,
  indexes_view.INDEX_NAME AS index_name,
  indexes_view.INDEX_STATUS AS status,
  index_columns_view.INDEX_COLUMN_NAME AS column_name,
  index_columns_view.INDEX_FIELD_PATH AS field_path,
  columns_view.DATA_TYPE AS data_type
FROM
  mydataset.INFORMATION_SCHEMA.SEARCH_INDEXES indexes_view
INNER JOIN
  mydataset.INFORMATION_SCHEMA.SEARCH_INDEX_COLUMNS index_columns_view
  ON
    indexes_view.TABLE_NAME = index_columns_view.TABLE_NAME
    AND indexes_view.INDEX_NAME = index_columns_view.INDEX_NAME
LEFT OUTER JOIN
  mydataset.INFORMATION_SCHEMA.COLUMNS columns_view
  ON
    indexes_view.INDEX_CATALOG = columns_view.TABLE_CATALOG
    AND indexes_view.INDEX_SCHEMA = columns_view.TABLE_SCHEMA
    AND index_columns_view.TABLE_NAME = columns_view.TABLE_NAME
    AND index_columns_view.INDEX_COLUMN_NAME = columns_view.COLUMN_NAME
ORDER BY
  project_name,
  dataset_name,
  table_name,
  column_name;
```

The result is similar to the following:

``` text
+------------+------------+----------+------------+--------+-------------+------------+---------------------------------------------------------------+
| project    | dataset    | table    | index_name | status | column_name | field_path | data_type                                                     |
+------------+------------+----------+------------+--------+-------------+------------+---------------------------------------------------------------+
| my_project | my_dataset | my_table | my_index   | ACTIVE | a           | a          | STRING                                                        |
| my_project | my_dataset | my_table | my_index   | ACTIVE | c           | c.e        | STRUCT<d INT64, e ARRAY<STRING>, f STRUCT<g STRING, h INT64>> |
| my_project | my_dataset | my_table | my_index   | ACTIVE | c           | c.f.g      | STRUCT<d INT64, e ARRAY<STRING>, f STRUCT<g STRING, h INT64>> |
+------------+------------+----------+------------+--------+-------------+------------+---------------------------------------------------------------+
```
