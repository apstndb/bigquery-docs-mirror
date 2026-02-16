# VIEWS view

The `  INFORMATION_SCHEMA.VIEWS  ` view contains metadata about views.

## Required permissions

To get view metadata, you need the following Identity and Access Management (IAM) permissions:

  - `  bigquery.tables.get  `
  - `  bigquery.tables.list  `

Each of the following predefined IAM roles includes the permissions that you need in order to get view metadata:

  - `  roles/bigquery.admin  `
  - `  roles/bigquery.dataEditor  `
  - `  roles/bigquery.metadataViewer  `
  - `  roles/bigquery.dataViewer  `

For more information about BigQuery permissions, see [Access control with IAM](/bigquery/docs/access-control) .

## Schema

When you query the `  INFORMATION_SCHEMA.VIEWS  ` view, the query results contain one row for each view in a dataset.

The `  INFORMATION_SCHEMA.VIEWS  ` view has the following schema:

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
<td>The name of the project that contains the dataset</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       table_schema      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the dataset that contains the view also referred to as the dataset <code dir="ltr" translate="no">       id      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       table_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the view also referred to as the table <code dir="ltr" translate="no">       id      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       view_definition      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The SQL query that defines the view</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       check_option      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The value returned is always <code dir="ltr" translate="no">       NULL      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       use_standard_sql      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><code dir="ltr" translate="no">       YES      </code> if the view was created by using a GoogleSQL query; <code dir="ltr" translate="no">       NO      </code> if <code dir="ltr" translate="no">       useLegacySql      </code> is set to <code dir="ltr" translate="no">       true      </code></td>
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
<td><code dir="ltr" translate="no">       [               PROJECT_ID              .]`region-               REGION              `.INFORMATION_SCHEMA.VIEWS      </code></td>
<td>Project level</td>
<td><code dir="ltr" translate="no">         REGION       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       [               PROJECT_ID              .]               DATASET_ID              .INFORMATION_SCHEMA.VIEWS      </code></td>
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

For example:

``` text
-- Returns metadata for views in a single dataset.
SELECT * FROM myDataset.INFORMATION_SCHEMA.VIEWS;

-- Returns metadata for all views in a region.
SELECT * FROM region-us.INFORMATION_SCHEMA.VIEWS;
```

## Examples

##### Example 1:

The following example retrieves all columns from the `  INFORMATION_SCHEMA.VIEWS  ` view except for `  check_option  ` which is reserved for future use. The metadata returned is for all views in `  mydataset  ` in your default project — `  myproject  ` .

To run the query against a project other than your default project, add the project ID to the dataset in the following format: ``  ` project_id `. dataset .INFORMATION_SCHEMA. view  `` ; for example, ``  `myproject`.mydataset.INFORMATION_SCHEMA.VIEWS  `` .

``` text
SELECT
  * EXCEPT (check_option)
FROM
  mydataset.INFORMATION_SCHEMA.VIEWS;
```

**Note:** `  INFORMATION_SCHEMA  ` view names are case-sensitive.

The result is similar to the following:

``` text
  +----------------+---------------+---------------+---------------------------------------------------------------------+------------------+
  | table_catalog  | table_schema  |  table_name   |                        view_definition                              | use_standard_sql |
  +----------------+---------------+---------------+---------------------------------------------------------------------+------------------+
  | myproject      | mydataset     | myview        | SELECT column1, column2 FROM [myproject:mydataset.mytable] LIMIT 10 | NO               |
  +----------------+---------------+---------------+---------------------------------------------------------------------+------------------+
  
```

Note that the results show that this view was created by using a legacy SQL query.

##### Example 2:

The following example retrieves the SQL query and query syntax used to define `  myview  ` in `  mydataset  ` in your default project — `  myproject  ` .

To run the query against a project other than your default project, add the project ID to the dataset in the following format: ``  ` project_id `. dataset .INFORMATION_SCHEMA. view  `` ; for example, ``  `myproject`.mydataset.INFORMATION_SCHEMA.VIEWS  `` .

``` text
SELECT
  table_name, view_definition, use_standard_sql
FROM
  mydataset.INFORMATION_SCHEMA.VIEWS
WHERE
  table_name = 'myview';
```

**Note:** `  INFORMATION_SCHEMA  ` view names are case-sensitive.

The result is similar to the following:

``` text
  +---------------+---------------------------------------------------------------+------------------+
  |  table_name   |                        view_definition                        | use_standard_sql |
  +---------------+---------------------------------------------------------------+------------------+
  | myview        | SELECT column1, column2, column3 FROM mydataset.mytable       | YES              |
  +---------------+---------------------------------------------------------------+------------------+
  
```

Note that the results show that this view was created by using a GoogleSQL query.
