# SEARCH\_INDEX\_COLUMN\_OPTIONS view

**Preview**

This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

The `  INFORMATION_SCHEMA.SEARCH_INDEX_COLUMN_OPTIONS  ` view contains one row for each option set on a search-indexed column in the tables in a dataset.

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

When you query the `  INFORMATION_SCHEMA.SEARCH_INDEX_COLUMN_OPTIONS  ` view, the query results contain one row for each option set on a search-indexed column in the tables in a dataset.

The `  INFORMATION_SCHEMA.SEARCH_INDEX_COLUMN_OPTIONS  ` view has the following schema:

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
<td>The name of the indexed column that the option is set on.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       option_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the option specified on the column.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       option_type      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The type of the option.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       option_value      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The value of the option.</td>
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
<td><code dir="ltr" translate="no">       [               PROJECT_ID              .]               DATASET_ID              .INFORMATION_SCHEMA.SEARCH_INDEX_COLUMN_OPTIONS      </code></td>
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
-- Returns metadata for search index column options in a single dataset.
SELECT * FROM myDataset.INFORMATION_SCHEMA.SEARCH_INDEX_COLUMN_OPTIONS;
```

## Example

The following example sets the default index column granularity to `  COLUMN  ` , and individually sets the granularity for `  col2  ` and `  col3  ` to `  GLOBAL  ` and `  COLUMN  ` respectively. In this example, columns `  col2  ` and `  col3  ` appear in the results because their granularity is set explicitly. The granularity for column `  col1  ` is not shown because it uses the default granularity.

``` text
CREATE SEARCH INDEX index1 ON `mydataset.table1` (
  ALL COLUMNS WITH COLUMN OPTIONS (
    col2 OPTIONS(index_granularity = 'GLOBAL'),
    col3 OPTIONS(index_granularity = 'COLUMN')
  )
)
OPTIONS(
  default_index_column_granularity = 'COLUMN'
);

SELECT
  index_column_name, option_name, option_type, option_value
FROM
  mydataset.INFORMATION_SCHEMA.SEARCH_INDEX_COLUMN_OPTIONS
WHERE
  index_schema = 'mydataset' AND index_name = 'index1' AND table_name = 'table1';
```

The result is similar to the following:

``` text
+-------------------+-------------------+---------------+--------------+
| index_column_name |  option_name      | option_type   | option_value |
+-------------------+-------------------+---------------+--------------+
| col2              | index_granularity | STRING        | GLOBAL       |
| col3              | index_granularity | STRING        | COLUMN       |
+-------------------+-------------------+---------------+--------------+
```

The following equivalent example, which doesn't use `  ALL COLUMNS  ` , sets the default index column granularity to `  COLUMN  ` and individually sets the granularity for two columns to `  GLOBAL  ` and `  COLUMN  ` respectively:

``` text
CREATE SEARCH INDEX index1 ON `mydataset.table1` (
  col1,
  col2 OPTIONS(index_granularity = 'GLOBAL'),
  col3 OPTIONS(index_granularity = 'COLUMN')
)
OPTIONS(
  default_index_column_granularity = 'COLUMN'
);

SELECT
  index_column_name, option_name, option_type, option_value
FROM
  mydataset.INFORMATION_SCHEMA.SEARCH_INDEX_COLUMN_OPTIONS
WHERE
  index_schema = 'mydataset' AND index_name = 'index1' AND table_name = 'table1';
```

The result is similar to the following:

``` text
+-------------------+-------------------+---------------+--------------+
| index_column_name |  option_name      | option_type   | option_value |
+-------------------+-------------------+---------------+--------------+
| col2              | index_granularity | STRING        | GLOBAL       |
| col3              | index_granularity | STRING        | COLUMN       |
+-------------------+-------------------+---------------+--------------+
```
