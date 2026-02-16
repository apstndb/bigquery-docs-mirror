# VECTOR\_INDEX\_COLUMNS view

The `  INFORMATION_SCHEMA.VECTOR_INDEX_COLUMNS  ` view contains one row for each vector-indexed column on each table in a dataset.

## Required permissions

To see [vector index](/bigquery/docs/vector-index) metadata, you need the `  bigquery.tables.get  ` or `  bigquery.tables.list  ` Identity and Access Management (IAM) permission on the table with the index. Each of the following predefined IAM roles includes at least one of these permissions:

  - `  roles/bigquery.admin  `
  - `  roles/bigquery.dataEditor  `
  - `  roles/bigquery.dataOwner  `
  - `  roles/bigquery.dataViewer  `
  - `  roles/bigquery.metadataViewer  `
  - `  roles/bigquery.user  `

For more information about BigQuery permissions, see [Access control with IAM](/bigquery/docs/access-control) .

## Schema

When you query the `  INFORMATION_SCHEMA.VECTOR_INDEX_COLUMNS  ` view, the query results contain one row for each indexed column on each table in a dataset.

The `  INFORMATION_SCHEMA.VECTOR_INDEX_COLUMNS  ` view has the following schema:

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
<td>The name of the dataset that contains the vector index.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       table_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the table that the vector index is created on.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       index_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the vector index.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       index_column_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the indexed column.</td>
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
<td><code dir="ltr" translate="no">       [               PROJECT_ID              .]               DATASET_ID              .INFORMATION_SCHEMA.VECTOR_INDEX_COLUMNS      </code></td>
<td>Dataset level</td>
<td>Dataset location</td>
</tr>
</tbody>
</table>

Replace the following:

  - Optional: `  PROJECT_ID  ` : the ID of your Google Cloud project. If not specified, the default project is used.
  - `  DATASET_ID  ` : the ID of your dataset. For more information, see [Dataset qualifier](/bigquery/docs/information-schema-intro#dataset_qualifier) .
    **Note:** You must use [a region qualifier](/bigquery/docs/information-schema-intro#region_qualifier) to query `  INFORMATION_SCHEMA  ` views. The location of the query execution must match the region of the `  INFORMATION_SCHEMA  ` view.

**Example**

``` text
-- Returns metadata for vector indexes in a single dataset.
SELECT * FROM myDataset.INFORMATION_SCHEMA.VECTOR_INDEX_COLUMNS;
```

## Examples

The following query extracts information on columns that have vector indexes:

``` text
SELECT table_name, index_name, index_column_name, index_field_path
FROM my_project.dataset.INFORMATION_SCHEMA.VECTOR_INDEX_COLUMNS;
```

The result is similar to the following:

``` console
+------------+------------+-------------------+------------------+
| table_name | index_name | index_column_name | index_field_path |
+------------+------------+-------------------+------------------+
| table1     | indexa     | embeddings        | embeddings       |
| table2     | indexb     | vectors           | vectors          |
| table3     | indexc     | vectors           | vectors          |
+------------+------------+-------------------+------------------+
```
