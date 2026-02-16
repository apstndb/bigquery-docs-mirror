# ROUTINE\_OPTIONS view

The `  INFORMATION_SCHEMA.ROUTINE_OPTIONS  ` view contains one row for each option of each routine in a dataset.

## Required permissions

To query the `  INFORMATION_SCHEMA.ROUTINE_OPTIONS  ` view, you need the following Identity and Access Management (IAM) permissions:

  - `  bigquery.routines.get  `
  - `  bigquery.routines.list  `

Each of the following predefined IAM roles includes the permissions that you need in order to get routine metadata:

  - `  roles/bigquery.admin  `
  - `  roles/bigquery.metadataViewer  `
  - `  roles/bigquery.dataViewer  `

For more information about BigQuery permissions, see [Access control with IAM](/bigquery/docs/access-control) .

## Schema

When you query the `  INFORMATION_SCHEMA.ROUTINE_OPTIONS  ` view, the query results contain one row for each option of each routine in a dataset.

The `  INFORMATION_SCHEMA.ROUTINE_OPTIONS  ` view has the following schema:

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
<td>The name of the project that contains the routine where the option is defined</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       specific_schema      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the dataset that contains the routine where the option is defined</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       specific_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the routine</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       option_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>One of the name values in the <a href="#options_table">options table</a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       option_type      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>One of the data type values in the <a href="#options_table">options table</a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       option_value      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>One of the value options in the <a href="#options_table">options table</a></td>
</tr>
</tbody>
</table>

##### Options table

<table>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">       OPTION_NAME      </code></th>
<th><code dir="ltr" translate="no">       OPTION_TYPE      </code></th>
<th><code dir="ltr" translate="no">       OPTION_VALUE      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       description      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The description of the routine, if defined</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       library      </code></td>
<td><code dir="ltr" translate="no">       ARRAY        </code></td>
<td>The names of the libraries referenced in the routine. Only applicable to JavaScript UDFs</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       data_governance_type      </code></td>
<td><code dir="ltr" translate="no">       DataGovernanceType        </code></td>
<td>The name of supported data governance type. For example, <code dir="ltr" translate="no">       DATA_MASKING      </code> .</td>
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
<td><code dir="ltr" translate="no">       [               PROJECT_ID              .]`region-               REGION              `.INFORMATION_SCHEMA.ROUTINE_OPTIONS      </code></td>
<td>Project level</td>
<td><code dir="ltr" translate="no">         REGION       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       [               PROJECT_ID              .]               DATASET_ID              .INFORMATION_SCHEMA.ROUTINE_OPTIONS      </code></td>
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
-- Returns metadata for routines in a single dataset.
SELECT * FROM myDataset.INFORMATION_SCHEMA.ROUTINE_OPTIONS;

-- Returns metadata for routines in a region.
SELECT * FROM region-us.INFORMATION_SCHEMA.ROUTINE_OPTIONS;
```

## Example

##### Example 1:

The following example retrieves the routine options for all routines in `  mydataset  ` in your default project ( `  myproject  ` ) by querying the `  INFORMATION_SCHEMA.ROUTINE_OPTIONS  ` view:

``` text
SELECT
  *
FROM
  mydataset.INFORMATION_SCHEMA.ROUTINE_OPTIONS;
```

**Note:** `  INFORMATION_SCHEMA  ` view names are case-sensitive.

The result is similar to the following:

``` text
+-------------------+------------------+---------------+----------------------+---------------+------------------+
| specific_catalog  | specific_schema  | specific_name |     option_name      | option_type   | option_value     |
+-------------------+------------------+---------------+----------------------+---------------+------------------+
| myproject         | mydataset        | myroutine1    | description          | STRING        | "a description"  |
| myproject         | mydataset        | myroutine2    | library              | ARRAY<STRING> | ["a.js", "b.js"] |
+-------------------+------------------+---------------+----------------------+---------------+------------------+
```
