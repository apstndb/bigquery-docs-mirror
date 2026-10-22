---
name: documents/docs.cloud.google.com/bigquery/docs/information-schema-column-field-paths
uri: https://docs.cloud.google.com/bigquery/docs/information-schema-column-field-paths
title: COLUMN_FIELD_PATHS view
description: Describes INFORMATION_SCHEMA.COLUMN_FIELD_PATHS views to get metadata about tables, columns, and partitions.
data_source: docs.cloud.google.com
---

# COLUMN_FIELD_PATHS view

The `INFORMATION_SCHEMA.COLUMN_FIELD_PATHS` view contains one row for each top-level column or column [nested](https://docs.cloud.google.com/bigquery/docs/nested-repeated) within a `RECORD` (or `STRUCT` ) column.

## Required permissions

To query the `INFORMATION_SCHEMA.COLUMN_FIELD_PATHS` view, you need the following Identity and Access Management (IAM) permissions:

- `bigquery.tables.get`
- `bigquery.tables.list`

Each of the following predefined IAM roles includes the preceding permissions:

- `roles/bigquery.admin`
- `roles/bigquery.dataViewer`
- `roles/bigquery.dataEditor`
- `roles/bigquery.metadataViewer`

For more information about BigQuery permissions, see [Access control with IAM](https://docs.cloud.google.com/bigquery/docs/access-control) .

## Schema

Query results contain one row for each top-level column or column [nested](https://docs.cloud.google.com/bigquery/docs/nested-repeated) within a `RECORD` (or `STRUCT` ) column.

When you query the `INFORMATION_SCHEMA.COLUMN_FIELD_PATHS` view, the query results contain one row for each column [nested](https://docs.cloud.google.com/bigquery/docs/nested-repeated) within a `RECORD` (or `STRUCT` ) column.

The `INFORMATION_SCHEMA.COLUMN_FIELD_PATHS` view has the following schema:

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
<td><code>table_catalog</code></td>
<td><code>STRING</code></td>
<td>The project ID of the project that contains the dataset.</td>
</tr>
<tr class="even">
<td><code>table_schema</code></td>
<td><code>STRING</code></td>
<td>The name of the dataset that contains the table also referred to as the <code>datasetId</code> .</td>
</tr>
<tr class="odd">
<td><code>table_name</code></td>
<td><code>STRING</code></td>
<td>The name of the table or view also referred to as the <code>tableId</code> .</td>
</tr>
<tr class="even">
<td><code>column_name</code></td>
<td><code>STRING</code></td>
<td>The name of the top-level column.</td>
</tr>
<tr class="odd">
<td><code>field_path</code></td>
<td><code>STRING</code></td>
<td>The name of the top-level column or the path to the column <a href="https://docs.cloud.google.com/bigquery/docs/nested-repeated">nested</a> within a <code>RECORD</code> or <code>STRUCT</code> column.</td>
</tr>
<tr class="even">
<td><code>data_type</code></td>
<td><code>STRING</code></td>
<td>The column's GoogleSQL <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-types">data type</a> .</td>
</tr>
<tr class="odd">
<td><code>description</code></td>
<td><code>STRING</code></td>
<td>The column's description.</td>
</tr>
<tr class="even">
<td><code>collation_name</code></td>
<td><code>STRING</code></td>
<td>The name of the <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/collation-concepts">collation specification</a> if it exists; otherwise, <code>NULL</code> .<br />
<br />
If a <code>STRING</code> , <code>ARRAY&lt;STRING&gt;</code> , or <code>STRING</code> field in a <code>STRUCT</code> is passed in, the collation specification is returned if it exists; otherwise, <code>NULL</code> is returned.</td>
</tr>
<tr class="odd">
<td><code>rounding_mode</code></td>
<td><code>STRING</code></td>
<td>The mode of rounding that's used when applying precision and scale to parameterized <code>NUMERIC</code> or <code>BIGNUMERIC</code> values; otherwise, the value is <code>NULL</code> .</td>
</tr>
<tr class="even">
<td><code>data_policies.name</code></td>
<td><code>STRING</code></td>
<td>The list of data policies that are attached to the column to control access and masking. This field is in ( <a href="https://cloud.google.com/products#product-launch-stages">Preview</a> ).</td>
</tr>
<tr class="odd">
<td><code>data_governance_tags</code></td>
<td><code>ARRAY&lt;STRUCT&gt;</code></td>
<td>The list of <a href="https://docs.cloud.google.com/bigquery/docs/tags#data-governance-tags">data governance tags</a> that are attached to the column or nested field to control access and masking. Each <code>STRUCT</code> contains the following <code>STRING</code> fields:
<ul>
<li><code>key</code> : the namespaced tag key, in the format <var translate="no">PROJECT_ID </var><code> / </code><var translate="no"> TAG_KEY</var> or <var translate="no">ORGANIZATION_ID </var><code> / </code><var translate="no"> TAG_KEY</var> .</li>
<li><code>value</code> : the short name of the tag value.</li>
</ul></td>
</tr>
<tr class="even">
<td><code>policy_tags</code></td>
<td><code>ARRAY&lt;STRING&gt;</code></td>
<td>The list of policy tags that are attached to the column.</td>
</tr>
</tbody>
</table>

For stability, we recommend that you explicitly list columns in your information schema queries instead of using a wildcard ( `SELECT *` ). Explicitly listing columns prevents queries from breaking if the underlying schema changes.

## Scope and syntax

Queries against this view must include a dataset or a region qualifier. For queries with a dataset qualifier, you must have permissions for the dataset. For queries with a region qualifier, you must have permissions for the project. For more information see [Syntax](https://docs.cloud.google.com/bigquery/docs/information-schema-intro#syntax) . The following table explains the region and resource scopes for this view:

| View name                                                                                    | Resource scope | Region scope     |
|----------------------------------------------------------------------------------------------|----------------|------------------|
| `[ `` PROJECT_ID ```  .]`region-  ``` REGION ```  `.INFORMATION_SCHEMA.COLUMN_FIELD_PATHS `` | Project level  | `REGION`         |
| `[ `` PROJECT_ID `` .] `` DATASET_ID `` .INFORMATION_SCHEMA.COLUMN_FIELD_PATHS`              | Dataset level  | Dataset location |

Replace the following:

- Optional: `PROJECT_ID` : the ID of your Google Cloud project. If not specified, the default project is used.

- `REGION` : any [dataset region name](https://docs.cloud.google.com/bigquery/docs/locations) . For example, `` `region-us` `` .

- `DATASET_ID` : the ID of your dataset. For more information, see [Dataset qualifier](https://docs.cloud.google.com/bigquery/docs/information-schema-intro#dataset_qualifier) .

  > **Note:** You must use [a region qualifier](https://docs.cloud.google.com/bigquery/docs/information-schema-intro#region_qualifier) to query `INFORMATION_SCHEMA` views. The location of the query execution must match the region of the `INFORMATION_SCHEMA` view.

## Example

The following example retrieves metadata from the `INFORMATION_SCHEMA.COLUMN_FIELD_PATHS` view for the `commits` table in the [`github_repos` dataset](https://console.cloud.google.com/bigquery?p=bigquery-public-data&d=github_repos&page=dataset) . This dataset is part of the BigQuery [public dataset program](https://cloud.google.com/public-datasets/) .

Because the table you're querying is in another project, the `bigquery-public-data` project, you add the project ID to the dataset in the following format: `` `  ``` project_id ```  `.  ``` dataset `` .INFORMATION_SCHEMA. `` view` ; for example, `` `bigquery-public-data`.github_repos.INFORMATION_SCHEMA.COLUMN_FIELD_PATHS `` .

The `commits` table contains the following nested and repeated columns:

- `author` : nested `RECORD` column
- `committer` : nested `RECORD` column
- `trailer` : nested and repeated `RECORD` column
- `difference` : nested and repeated `RECORD` column

To view metadata about the `author` and `difference` columns, run the following query.

> **Note:** `INFORMATION_SCHEMA` view names are case-sensitive.

```
SELECT
  *
FROM
  `bigquery-public-data`.github_repos.INFORMATION_SCHEMA.COLUMN_FIELD_PATHS
WHERE
  table_name = 'commits'
  AND (column_name = 'author' OR column_name = 'difference');
```

The result is similar to the following. For readability, some columns are excluded from the result.

```
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
