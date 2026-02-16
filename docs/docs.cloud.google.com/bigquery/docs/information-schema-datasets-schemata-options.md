# SCHEMATA\_OPTIONS view

The `  INFORMATION_SCHEMA.SCHEMATA_OPTIONS  ` view contains one row for each option that is set in each dataset in a project.

## Before you begin

To query the `  SCHEMATA_OPTIONS  ` view for dataset metadata, you need the `  bigquery.datasets.get  ` Identity and Access Management (IAM) permission at the project level.

Each of the following predefined IAM roles includes the permissions that you need in order to get the `  SCHEMATA_OPTIONS  ` view:

  - `  roles/bigquery.admin  `
  - `  roles/bigquery.dataEditor  `
  - `  roles/bigquery.dataOwner  `
  - `  roles/bigquery.dataViewer  `

For more information about BigQuery permissions, see [Access control with IAM](/bigquery/docs/access-control) .

## Schema

When you query the `  INFORMATION_SCHEMA.SCHEMATA_OPTIONS  ` view, the query results contain one row for each option that is set in each dataset in a project.

The `  INFORMATION_SCHEMA.SCHEMATA_OPTIONS  ` view has the following schema:

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
<td><code dir="ltr" translate="no">       catalog_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the project that contains the dataset</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       schema_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the dataset, also referred to as the <code dir="ltr" translate="no">       datasetId      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       option_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the option. For a list of supported options, see the <a href="/bigquery/docs/reference/standard-sql/data-definition-language#schema_option_list">schema options list</a> .
<p>The <code dir="ltr" translate="no">        storage_billing_model       </code> option is only displayed for datasets that have been updated after December 1, 2022. For datasets that were last updated before that date, the storage billing model is <code dir="ltr" translate="no">        LOGICAL       </code> .</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       option_type      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The data type of the option</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       option_value      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The value of the option</td>
</tr>
</tbody>
</table>

For stability, we recommend that you explicitly list columns in your information schema queries instead of using a wildcard ( `  SELECT *  ` ). Explicitly listing columns prevents queries from breaking if the underlying schema changes.

## Scope and syntax

Queries against this view must include a [region qualifier](/bigquery/docs/information-schema-intro#syntax) . If you do not specify a regional qualifier, metadata is retrieved from the US region. The following table explains the region scope for this view:

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
<td><code dir="ltr" translate="no">       [               PROJECT_ID              .]INFORMATION_SCHEMA.SCHEMATA_OPTIONS      </code></td>
<td>Project level</td>
<td>US region</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       [               PROJECT_ID              .]`region-               REGION              `.INFORMATION_SCHEMA.SCHEMATA_OPTIONS      </code></td>
<td>Project level</td>
<td><code dir="ltr" translate="no">         REGION       </code></td>
</tr>
</tbody>
</table>

Replace the following:

  - Optional: `  PROJECT_ID  ` : the ID of your Google Cloud project. If not specified, the default project is used.
  - `  REGION  ` : any [dataset region name](/bigquery/docs/locations) . For example, ``  `region-us`  `` .
    **Note:** You must use [a region qualifier](/bigquery/docs/information-schema-intro#region_qualifier) to query `  INFORMATION_SCHEMA  ` views. The location of the query execution must match the region of the `  INFORMATION_SCHEMA  ` view.

**Example**

``` text
-- Returns metadata for datasets in a region.
SELECT * FROM region-us.INFORMATION_SCHEMA.SCHEMATA_OPTIONS;
```

## Examples

#### Retrieve the default table expiration time for all datasets in your project

To run the query against a project other than your default project, add the project ID to the dataset in the following format:

``` text
`PROJECT_ID`.INFORMATION_SCHEMA.SCHEMATA_OPTIONS
```

for example, ``  `myproject`.INFORMATION_SCHEMA.SCHEMATA_OPTIONS  `` .

``` text
SELECT
  *
FROM
  INFORMATION_SCHEMA.SCHEMATA_OPTIONS
WHERE
  option_name = 'default_table_expiration_days';
```

**Note:** `  INFORMATION_SCHEMA  ` view names are case-sensitive.

The result is similar to the following:

``` text
  +----------------+---------------+-------------------------------+-------------+---------------------+
  |  catalog_name  |  schema_name  |          option_name          | option_type |    option_value     |
  +----------------+---------------+-------------------------------+-------------+---------------------+
  | myproject      | mydataset3    | default_table_expiration_days | FLOAT64     | 0.08333333333333333 |
  | myproject      | mydataset2    | default_table_expiration_days | FLOAT64     | 90.0                |
  | myproject      | mydataset1    | default_table_expiration_days | FLOAT64     | 30.0                |
  +----------------+---------------+-------------------------------+-------------+---------------------+
  
```

**Note:** `  0.08333333333333333  ` is the floating point representation of 2 hours.

#### Retrieve labels for all datasets in your project

To run the query against a project other than your default project, add the project ID to the dataset in the following format:

``` text
`PROJECT_ID`.INFORMATION_SCHEMA.SCHEMATA_OPTIONS
```

; for example, ``  `myproject`.INFORMATION_SCHEMA.SCHEMATA_OPTIONS  `` .

``` text
SELECT
  *
FROM
  INFORMATION_SCHEMA.SCHEMATA_OPTIONS
WHERE
  option_name = 'labels';
```

**Note:** `  INFORMATION_SCHEMA  ` view names are case-sensitive.

The result is similar to the following:

``` text
  +----------------+---------------+-------------+---------------------------------+------------------------+
  |  catalog_name  |  schema_name  | option_name |          option_type            |      option_value      |
  +----------------+---------------+-------------+---------------------------------+------------------------+
  | myproject      | mydataset1    | labels      | ARRAY<STRUCT<STRING, STRING>>   | [STRUCT("org", "dev")] |
  | myproject      | mydataset2    | labels      | ARRAY<STRUCT<STRING, STRING>>   | [STRUCT("org", "dev")] |
  +----------------+---------------+-------------+---------------------------------+------------------------+
  
```

**Note:** Datasets without labels are excluded from the query results.
