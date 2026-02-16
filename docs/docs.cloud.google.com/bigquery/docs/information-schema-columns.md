# COLUMNS view

The `  INFORMATION_SCHEMA.COLUMNS  ` view contains one row for each column (field) in a table.

## Required permissions

To query the `  INFORMATION_SCHEMA.COLUMNS  ` view, you need the following Identity and Access Management (IAM) permissions:

  - `  bigquery.tables.get  `
  - `  bigquery.tables.list  `

Each of the following predefined IAM roles includes the preceding permissions:

  - `  roles/bigquery.admin  `
  - `  roles/bigquery.dataViewer  `
  - `  roles/bigquery.dataEditor  `
  - `  roles/bigquery.metadataViewer  `

For more information about BigQuery permissions, see [Access control with IAM](/bigquery/docs/access-control) .

## Schema

When you query the `  INFORMATION_SCHEMA.COLUMNS  ` view, the query results contain one row for each column (field) in a table.

The `  INFORMATION_SCHEMA.COLUMNS  ` view has the following schema:

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
<td><code dir="ltr" translate="no">       ordinal_position      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td>The 1-indexed offset of the column within the table; if it's a pseudo column such as _PARTITIONTIME or _PARTITIONDATE, the value is <code dir="ltr" translate="no">       NULL      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       is_nullable      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><code dir="ltr" translate="no">       YES      </code> or <code dir="ltr" translate="no">       NO      </code> depending on whether the column's mode allows <code dir="ltr" translate="no">       NULL      </code> values.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       data_type      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The column's GoogleSQL <a href="/bigquery/docs/reference/standard-sql/data-types">data type</a> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       is_generated      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The value is <code dir="ltr" translate="no">       ALWAYS      </code> if the column is an <a href="/bigquery/docs/autonomous-embedding-generation">automatically generated embedding column</a> ; otherwise, the value is <code dir="ltr" translate="no">       NEVER      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       generation_expression      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The value is the generation expression used to define the column if the column is an automatically generated embedding column; otherwise the value is <code dir="ltr" translate="no">       NULL      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       is_stored      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The value is <code dir="ltr" translate="no">       YES      </code> if the column is an automatically generated embedding column; otherwise, the value is <code dir="ltr" translate="no">       NULL      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       is_hidden      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><code dir="ltr" translate="no">       YES      </code> or <code dir="ltr" translate="no">       NO      </code> depending on whether the column is a pseudo column such as _PARTITIONTIME or _PARTITIONDATE.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       is_updatable      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The value is always <code dir="ltr" translate="no">       NULL      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       is_system_defined      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><code dir="ltr" translate="no">       YES      </code> or <code dir="ltr" translate="no">       NO      </code> depending on whether the column is a pseudo column such as _PARTITIONTIME or _PARTITIONDATE.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       is_partitioning_column      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><code dir="ltr" translate="no">       YES      </code> or <code dir="ltr" translate="no">       NO      </code> depending on whether the column is a <a href="/bigquery/docs/partitioned-tables">partitioning column</a> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       clustering_ordinal_position      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td>The 1-indexed offset of the column within the table's clustering columns; the value is <code dir="ltr" translate="no">       NULL      </code> if the table is not a clustered table.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       collation_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the <a href="/bigquery/docs/reference/standard-sql/collation-concepts">collation specification</a> if it exists; otherwise, <code dir="ltr" translate="no">       NULL      </code> .<br />
<br />
If a <code dir="ltr" translate="no">       STRING      </code> or <code dir="ltr" translate="no">       ARRAY&lt;STRING&gt;      </code> is passed in, the collation specification is returned if it exists; otherwise <code dir="ltr" translate="no">       NULL      </code> is returned.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       column_default      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The <a href="/bigquery/docs/default-values">default value</a> of the column if it exists; otherwise, the value is <code dir="ltr" translate="no">       NULL      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       rounding_mode      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The mode of rounding that's used for values written to the field if its type is a parameterized <code dir="ltr" translate="no">       NUMERIC      </code> or <code dir="ltr" translate="no">       BIGNUMERIC      </code> ; otherwise, the value is <code dir="ltr" translate="no">       NULL      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       data_policies.name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The list of data policies that are attached to the column to control access and masking. This field is in ( <a href="https://cloud.google.com/products#product-launch-stages">Preview</a> ).</td>
</tr>
<tr class="even">
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
<td><code dir="ltr" translate="no">       [               PROJECT_ID              .]`region-               REGION              `.INFORMATION_SCHEMA.COLUMNS      </code></td>
<td>Project level</td>
<td><code dir="ltr" translate="no">         REGION       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       [               PROJECT_ID              .]               DATASET_ID              .INFORMATION_SCHEMA.COLUMNS      </code></td>
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

The following example retrieves metadata from the `  INFORMATION_SCHEMA.COLUMNS  ` view for the `  population_by_zip_2010  ` table in the [`  census_bureau_usa  `](https://console.cloud.google.com/bigquery?p=bigquery-public-data&d=census_bureau_usa&page=dataset) dataset. This dataset is part of the BigQuery [public dataset program](https://cloud.google.com/public-datasets/) .

Because the table you're querying is in another project, the `  bigquery-public-data  ` project, you add the project ID to the dataset in the following format: ``  ` project_id `. dataset .INFORMATION_SCHEMA. view  `` ; for example, ``  `bigquery-public-data`.census_bureau_usa.INFORMATION_SCHEMA.TABLES  `` .

The following column is excluded from the query results:

  - `  IS_UPDATABLE  `

**Note:** `  INFORMATION_SCHEMA  ` view names are case-sensitive.

``` text
  SELECT
    * EXCEPT(is_updatable)
  FROM
    `bigquery-public-data`.census_bureau_usa.INFORMATION_SCHEMA.COLUMNS
  WHERE
    table_name = 'population_by_zip_2010';
```

The result is similar to the following. For readability, some columns are excluded from the result.

``` text
+------------------------+-------------+------------------+-------------+-----------+-----------+-------------------+------------------------+-----------------------------+-------------+
|       table_name       | column_name | ordinal_position | is_nullable | data_type | is_hidden | is_system_defined | is_partitioning_column | clustering_ordinal_position | policy_tags |
+------------------------+-------------+------------------+-------------+-----------+-----------+-------------------+------------------------+-----------------------------+-------------+
| population_by_zip_2010 | zipcode     |                1 | NO          | STRING    | NO        | NO                | NO                     |                        NULL | 0 rows      |
| population_by_zip_2010 | geo_id      |                2 | YES         | STRING    | NO        | NO                | NO                     |                        NULL | 0 rows      |
| population_by_zip_2010 | minimum_age |                3 | YES         | INT64     | NO        | NO                | NO                     |                        NULL | 0 rows      |
| population_by_zip_2010 | maximum_age |                4 | YES         | INT64     | NO        | NO                | NO                     |                        NULL | 0 rows      |
| population_by_zip_2010 | gender      |                5 | YES         | STRING    | NO        | NO                | NO                     |                        NULL | 0 rows      |
| population_by_zip_2010 | population  |                6 | YES         | INT64     | NO        | NO                | NO                     |                        NULL | 0 rows      |
+------------------------+-------------+------------------+-------------+-----------+-----------+-------------------+------------------------+-----------------------------+-------------+
  
```
