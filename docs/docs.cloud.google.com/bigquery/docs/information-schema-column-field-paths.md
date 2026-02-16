# COLUMN\_FIELD\_PATHS view

The `  INFORMATION_SCHEMA.COLUMN_FIELD_PATHS  ` view contains one row for each column [nested](/bigquery/docs/nested-repeated) within a `  RECORD  ` (or `  STRUCT  ` ) column.

## Required permissions

To query the `  INFORMATION_SCHEMA.COLUMN_FIELD_PATHS  ` view, you need the following Identity and Access Management (IAM) permissions:

  - `  bigquery.tables.get  `
  - `  bigquery.tables.list  `

Each of the following predefined IAM roles includes the preceding permissions:

  - `  roles/bigquery.admin  `
  - `  roles/bigquery.dataViewer  `
  - `  roles/bigquery.dataEditor  `
  - `  roles/bigquery.metadataViewer  `

For more information about BigQuery permissions, see [Access control with IAM](/bigquery/docs/access-control) .

## Schema

Query results contain one row for each column [nested](/bigquery/docs/nested-repeated) within a `  RECORD  ` (or `  STRUCT  ` ) column.

When you query the `  INFORMATION_SCHEMA.COLUMN_FIELD_PATHS  ` view, the query results contain one row for each column [nested](/bigquery/docs/nested-repeated) within a `  RECORD  ` (or `  STRUCT  ` ) column.

The `  INFORMATION_SCHEMA.COLUMN_FIELD_PATHS  ` view has the following schema:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
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
<td>The project ID of the project that contains the dataset.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       table_schema      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the dataset that contains the table also referred to as the <code dir="ltr" translate="no">       datasetId      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       table_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the table or view also referred to as the <code dir="ltr" translate="no">       tableId      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       column_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the column.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       field_path      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The path to a column <a href="/bigquery/docs/nested-repeated">nested</a> within a `RECORD` or `STRUCT` column.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       data_type      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The column's GoogleSQL <a href="/bigquery/docs/reference/standard-sql/data-types">data type</a> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       description      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The column's description.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       collation_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the <a href="/bigquery/docs/reference/standard-sql/collation-concepts">collation specification</a> if it exists; otherwise, <code dir="ltr" translate="no">       NULL      </code> .<br />
<br />
If a <code dir="ltr" translate="no">       STRING      </code> , <code dir="ltr" translate="no">       ARRAY&lt;STRING&gt;      </code> , or <code dir="ltr" translate="no">       STRING      </code> field in a <code dir="ltr" translate="no">       STRUCT      </code> is passed in, the collation specification is returned if it exists; otherwise, <code dir="ltr" translate="no">       NULL      </code> is returned.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       rounding_mode      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The mode of rounding that's used when applying precision and scale to+ parameterized <code dir="ltr" translate="no">       NUMERIC      </code> or <code dir="ltr" translate="no">       BIGNUMERIC      </code> values; otherwise, the value is <code dir="ltr" translate="no">       NULL      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       data_policies.name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The list of data policies that are attached to the column to control access and masking. This field is in ( <a href="https://cloud.google.com/products#product-launch-stages">Preview</a> ).</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       policy_tags      </code></td>
<td><code dir="ltr" translate="no">       ARRAY&lt;STRING&gt;      </code></td>
<td>The list of policy tags that are attached to the column.</td>
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
<td><code dir="ltr" translate="no">       [               PROJECT_ID              .]`region-               REGION              `.INFORMATION_SCHEMA.COLUMN_FIELD_PATHS      </code></td>
<td>Project level</td>
<td><code dir="ltr" translate="no">         REGION       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       [               PROJECT_ID              .]               DATASET_ID              .INFORMATION_SCHEMA.COLUMN_FIELD_PATHS      </code></td>
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

## Example

The following example retrieves metadata from the `  INFORMATION_SCHEMA.COLUMN_FIELD_PATHS  ` view for the `  commits  ` table in the [`  github_repos  ` dataset](https://console.cloud.google.com/bigquery?p=bigquery-public-data&d=github_repos&page=dataset) . This dataset is part of the BigQuery [public dataset program](https://cloud.google.com/public-datasets/) .

Because the table you're querying is in another project, the `  bigquery-public-data  ` project, you add the project ID to the dataset in the following format: ``  ` project_id `. dataset .INFORMATION_SCHEMA. view  `` ; for example, ``  `bigquery-public-data`.github_repos.INFORMATION_SCHEMA.COLUMN_FIELD_PATHS  `` .

The `  commits  ` table contains the following nested and nested and repeated columns:

  - `  author  ` : nested `  RECORD  ` column
  - `  committer  ` : nested `  RECORD  ` column
  - `  trailer  ` : nested and repeated `  RECORD  ` column
  - `  difference  ` : nested and repeated `  RECORD  ` column

To view metadata about the `  author  ` and `  difference  ` columns, run the following query.

**Note:** `  INFORMATION_SCHEMA  ` view names are case-sensitive.

``` text
SELECT
  *
FROM
  `bigquery-public-data`.github_repos.INFORMATION_SCHEMA.COLUMN_FIELD_PATHS
WHERE
  table_name = 'commits'
  AND (column_name = 'author' OR column_name = 'difference');
```

The result is similar to the following. For readability, some columns are excluded from the result.

``` text
  +------------+-------------+---------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+
  | table_name | column_name |     field_path      |                                                                      data_type                                                                      | description | policy_tags |
  +------------+-------------+---------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+
  | commits    | author      | author              | STRUCT<name STRING, email STRING, time_sec INT64, tz_offset INT64, date TIMESTAMP>                                                                  | NULL        | 0 rows      |
  | commits    | author      | author.name         | STRING                                                                                                                                              | NULL        | 0 rows      |
  | commits    | author      | author.email        | STRING                                                                                                                                              | NULL        | 0 rows      |
  | commits    | author      | author.time_sec     | INT64                                                                                                                                               | NULL        | 0 rows      |
  | commits    | author      | author.tz_offset    | INT64                                                                                                                                               | NULL        | 0 rows      |
  | commits    | author      | author.date         | TIMESTAMP                                                                                                                                           | NULL        | 0 rows      |
  | commits    | difference  | difference          | ARRAY<STRUCT<old_mode INT64, new_mode INT64, old_path STRING, new_path STRING, old_sha1 STRING, new_sha1 STRING, old_repo STRING, new_repo STRING>> | NULL        | 0 rows      |
  | commits    | difference  | difference.old_mode | INT64                                                                                                                                               | NULL        | 0 rows      |
  | commits    | difference  | difference.new_mode | INT64                                                                                                                                               | NULL        | 0 rows      |
  | commits    | difference  | difference.old_path | STRING                                                                                                                                              | NULL        | 0 rows      |
  | commits    | difference  | difference.new_path | STRING                                                                                                                                              | NULL        | 0 rows      |
  | commits    | difference  | difference.old_sha1 | STRING                                                                                                                                              | NULL        | 0 rows      |
  | commits    | difference  | difference.new_sha1 | STRING                                                                                                                                              | NULL        | 0 rows      |
  | commits    | difference  | difference.old_repo | STRING                                                                                                                                              | NULL        | 0 rows      |
  | commits    | difference  | difference.new_repo | STRING                                                                                                                                              | NULL        | 0 rows      |
  +------------+-------------+---------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+
  
```
