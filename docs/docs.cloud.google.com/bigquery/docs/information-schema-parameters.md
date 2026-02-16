# PARAMETERS view

The `  INFORMATION_SCHEMA.PARAMETERS  ` view contains one row for each parameter of each routine in a dataset.

## Required permissions

To query the `  INFORMATION_SCHEMA.PARAMETERS  ` view, you need the following Identity and Access Management (IAM) permissions:

  - `  bigquery.routines.get  `
  - `  bigquery.routines.list  `

Each of the following predefined IAM roles includes the permissions that you need to get routine metadata:

  - `  roles/bigquery.admin  `
  - `  roles/bigquery.metadataViewer  `
  - `  roles/bigquery.dataViewer  `

For more information about BigQuery permissions, see [Access control with IAM](/bigquery/docs/access-control) .

## Schema

When you query the `  INFORMATION_SCHEMA.PARAMETERS  ` view, the query results contain one row for each parameter of each routine in a dataset.

The `  INFORMATION_SCHEMA.PARAMETERS  ` view has the following schema:

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
<td><code dir="ltr" translate="no">       specific_catalog      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the project that contains the dataset in which the routine containing the parameter is defined</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       specific_schema      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the dataset that contains the routine in which the parameter is defined</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       specific_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the routine in which the parameter is defined</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ordinal_position      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The 1-based position of the parameter, or 0 for the return value</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       parameter_mode      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The mode of the parameter, either <code dir="ltr" translate="no">       IN      </code> , <code dir="ltr" translate="no">       OUT      </code> , <code dir="ltr" translate="no">       INOUT      </code> , or <code dir="ltr" translate="no">       NULL      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       is_result      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Whether the parameter is the result of the function, either <code dir="ltr" translate="no">       YES      </code> or <code dir="ltr" translate="no">       NO      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       parameter_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the parameter</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       data_type      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The type of the parameter, will be <code dir="ltr" translate="no">       ANY TYPE      </code> if defined as an any type</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       parameter_default      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The default value of the parameter as a SQL literal value, always <code dir="ltr" translate="no">       NULL      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       is_aggregate      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Whether this is an aggregate parameter, always <code dir="ltr" translate="no">       NULL      </code></td>
</tr>
</tbody>
</table>

For stability, we recommend that you explicitly list columns in your information schema queries instead of using a wildcard ( `  SELECT *  ` ). Explicitly listing columns prevents queries from breaking if the underlying schema changes.

## Scope and syntax

Queries against this view must include a dataset or a region qualifier. For more information see [Syntax](/bigquery/docs/information-schema-intro#syntax) . The following table explains the region and resource scopes for this view:

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
<td><code dir="ltr" translate="no">       [               PROJECT_ID              .]`region-               REGION              `.INFORMATION_SCHEMA.PARAMETERS      </code></td>
<td>Project level</td>
<td><code dir="ltr" translate="no">         REGION       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       [               PROJECT_ID              .]               DATASET_ID              .INFORMATION_SCHEMA.PARAMETERS      </code></td>
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
-- Returns metadata for parameters of a routine in a single dataset.
SELECT * FROM myDataset.INFORMATION_SCHEMA.PARAMETERS;

-- Returns metadata for parameters of a routine in a region.
SELECT * FROM region-us.INFORMATION_SCHEMA.PARAMETERS;
```

## Example

#### Example

To run the query against a dataset in a project other than your default project, add the project ID in the following format:

``` text
`PROJECT_ID`.`DATASET_ID`.INFORMATION_SCHEMA.PARAMETERS
```

Replace the following:

  - `  PROJECT_ID  ` : the ID of the project.
  - `  DATASET_ID  ` : the ID of the dataset.

For example, `  example-project.mydataset.INFORMATION_SCHEMA.JOBS_BY_PROJECT  ` .

The following example retrieves all parameters from the `  INFORMATION_SCHEMA.PARAMETERS  ` view. The metadata returned is for routines in `  mydataset  ` in your default project — `  myproject  ` .

``` text
SELECT
  * EXCEPT(is_typed)
FROM
  mydataset.INFORMATION_SCHEMA.PARAMETERS
WHERE
  table_type = 'BASE TABLE';
```

**Note:** `  INFORMATION_SCHEMA  ` view names are case-sensitive.

The result is similar to the following:

``` text
+-------------------+------------------+---------------+------------------+----------------+-----------+----------------+-----------+-------------------+--------------+
| specific_catalog  | specific_schema  | specific_name | ordinal_position | parameter_mode | is_result | parameter_name | data_type | parameter_default | is_aggregate |
+-------------------+------------------+---------------+------------------+----------------+-----------+----------------+-----------+-------------------+--------------+
| myproject         | mydataset        | myroutine1    | 0                | NULL           | YES       | NULL           | INT64     | NULL              | NULL         |
| myproject         | mydataset        | myroutine1    | 1                | NULL           | NO        | x              | INT64     | NULL              | NULL         |
+-------------------+------------------+---------------+------------------+----------------+-----------+----------------+-----------+-------------------+--------------+
```
