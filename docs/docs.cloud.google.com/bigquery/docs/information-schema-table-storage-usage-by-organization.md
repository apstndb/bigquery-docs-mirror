# TABLE\_STORAGE\_USAGE\_TIMELINE\_BY\_ORGANIZATION view

**Preview**

This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

The `  INFORMATION_SCHEMA.TABLE_STORAGE_USAGE_TIMELINE_BY_ORGANIZATION  ` view provides daily totals of storage usage for the past 90 days for the following types of tables:

  - Standard tables
  - Materialized views
  - Table clones that have a delta in bytes from the base table
  - Table snapshots that have a delta in bytes from the base table

Tables that don't have billable bytes aren't included in the `  INFORMATION_SCHEMA.TABLE_STORAGE_USAGE_TIMELINE_BY_ORGANIZATION  ` view. This includes the following types of tables:

  - External tables
  - Anonymous tables
  - Empty tables
  - Table clones that have no delta in bytes from the base table
  - Table snapshots that have no delta in bytes from the base table

When you query the `  INFORMATION_SCHEMA.TABLE_STORAGE_USAGE_TIMELINE_BY_ORGANIZATION  ` view, the query results contain one row per day for each table or materialized view for the whole organization associated with the current project.

The data in this table is not available in real time. It takes approximately 72 hours for table data to be reflected in this view.

Storage usage is returned in MiB second. For example, if a project uses 1,000,000 physical bytes for 86,400 seconds (24 hours), the total physical usage is 86,400,000,000 byte seconds, which is converted to 82,397 MiB seconds, as shown in the following example:

``` text
86,400,000,000 / 1,024 / 1,024 = 82,397
```

This is the value that would be returned by the `  BILLABLE_TOTAL_PHYSICAL_USAGE  ` column.

For more information, see [Storage pricing details](https://cloud.google.com/bigquery/pricing#storage-pricing-details) .

**Note:** Data for this view has a start date of October 1, 2023. You can query the view for dates prior to that, but the data returned is incomplete.

## Required permissions

To query the `  INFORMATION_SCHEMA.TABLE_STORAGE_USAGE_TIMELINE_BY_ORGANIZATION  ` view, you need the following Identity and Access Management (IAM) permissions for your organization:

  - `  bigquery.tables.get  `
  - `  bigquery.tables.list  `

Each of the following predefined IAM roles includes the preceding permissions:

  - `  roles/bigquery.dataViewer  `
  - `  roles/bigquery.dataEditor  `
  - `  roles/bigquery.metadataViewer  `
  - `  roles/bigquery.admin  `

This schema view is only available to users with defined [Google Cloud organizations](/resource-manager/docs/cloud-platform-resource-hierarchy#organizations) .

For more information about BigQuery permissions, see [Access control with IAM](/bigquery/docs/access-control) .

## Schema

The `  INFORMATION_SCHEMA.TABLE_STORAGE_USAGE_TIMELINE_BY_ORGANIZATION  ` view has the following schema:

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
<td><code dir="ltr" translate="no">       usage_date      </code></td>
<td><code dir="ltr" translate="no">       DATE      </code></td>
<td>The billing date for the bytes shown, using the <code dir="ltr" translate="no">       America/Los_Angeles      </code> time zone</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       project_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The project ID of the project that contains the dataset</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       table_catalog      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The project ID of the project that contains the dataset</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       project_number      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td>The project number of the project that contains the dataset</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       table_schema      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the dataset that contains the table or materialized view, also referred to as the <code dir="ltr" translate="no">       datasetId      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       table_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the table or materialized view, also referred to as the <code dir="ltr" translate="no">       tableId      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       billable_total_logical_usage      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td><p>The total logical usage, in MiB second.</p>
<p>Returns 0 if the dataset uses the physical storage <a href="/bigquery/docs/datasets-intro#dataset_storage_billing_models">billing model</a> .</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       billable_active_logical_usage      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td><p>The logical usage that is less than 90 days old, in MiB second.</p>
<p>Returns 0 if the dataset uses the physical storage <a href="/bigquery/docs/datasets-intro#dataset_storage_billing_models">billing model</a> .</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       billable_long_term_logical_usage      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td><p>The logical usage that is more than 90 days old, in MiB second.</p>
<p>Returns 0 if the dataset uses the physical storage <a href="/bigquery/docs/datasets-intro#dataset_storage_billing_models">billing model</a> .</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       billable_total_physical_usage      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td><p>The total usage in MiB second. This includes physical bytes used for fail-safe and <a href="/bigquery/docs/time-travel">time travel</a> storage.</p>
<p>Returns 0 if the dataset uses the logical storage <a href="/bigquery/docs/datasets-intro#dataset_storage_billing_models">billing model</a> .</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       billable_active_physical_usage      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td><p>The physical usage that is less than 90 days old, in MiB second. This includes physical bytes used for fail-safe and <a href="/bigquery/docs/time-travel">time travel</a> storage.</p>
<p>Returns 0 if the dataset uses the logical storage <a href="/bigquery/docs/datasets-intro#dataset_storage_billing_models">billing model</a> .</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       billable_long_term_physical_usage      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td><p>The physical usage that is more than 90 days old, in MiB second.</p>
<p>Returns 0 if the dataset uses the logical storage <a href="/bigquery/docs/datasets-intro#dataset_storage_billing_models">billing model</a> .</p></td>
</tr>
</tbody>
</table>

For stability, we recommend that you explicitly list columns in your information schema queries instead of using a wildcard ( `  SELECT *  ` ). Explicitly listing columns prevents queries from breaking if the underlying schema changes.

## Scope and syntax

Queries against this view must include a [region qualifier](/bigquery/docs/information-schema-intro#syntax) . If you don't specify a regional qualifier, metadata is retrieved from all regions. The following table explains the region scope for this view:

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
<td><code dir="ltr" translate="no">       [               PROJECT_ID              .]`region-               REGION              `.INFORMATION_SCHEMA.TABLE_STORAGE_USAGE_TIMELINE_BY_ORGANIZATION      </code></td>
<td>Organization that contains the specified project</td>
<td><code dir="ltr" translate="no">         REGION       </code></td>
</tr>
</tbody>
</table>

Replace the following:

  - Optional: `  PROJECT_ID  ` : the ID of your Google Cloud project. If not specified, the default project is used.
  - `  REGION  ` : any [dataset region name](/bigquery/docs/locations) . For example, ``  `region-us`  `` .
    **Note:** You must use [a region qualifier](/bigquery/docs/information-schema-intro#region_qualifier) to query `  INFORMATION_SCHEMA  ` views. The location of the query execution must match the region of the `  INFORMATION_SCHEMA  ` view.

The following example shows how to return storage information for tables in a specified project in an organization:

``` text
SELECT * FROM myProject.`region-REGION`.INFORMATION_SCHEMA.TABLE_STORAGE_USAGE_TIMELINE_BY_ORGANIZATION;
```

The following example shows how to return storage information by project for tables in an organization:

``` text
SELECT * FROM `region-REGION`.INFORMATION_SCHEMA.TABLE_STORAGE_USAGE_TIMELINE_BY_ORGANIZATION;
```

## Example

The following example shows the usage for all tables in the organization for the most recent usage date.

``` text
SELECT
  usage_date,
  project_id,
  table_schema,
  table_name,
  billable_total_logical_usage,
  billable_total_physical_usage
FROM
  (
    SELECT
      *,
      ROW_NUMBER()
        OVER (PARTITION BY project_id, table_schema, table_name ORDER BY usage_date DESC) AS rank
    FROM
      `region-REGION`.INFORMATION_SCHEMA.TABLE_STORAGE_USAGE_TIMELINE_BY_ORGANIZATION
  )
WHERE rank = 1;
```

The result is similar to the following:

``` text
+--------------+------------+--------------+------------+------------------------------+-------------------------------+
| usage_date   | project_id | table_schema | table_name | billable_total_logical_usage | billable_total_physical_usage |
+--------------+------------+--------------+------------+------------------------------+-------------------------------+
|  2023-04-03  | project1   | dataset_A    | table_x    | 734893409201                 |           0                   |
+--------------+------------+--------------+------------+------------------------------+-------------------------------+
|  2023-04-03  | project1   | dataset_A    | table_z    | 110070445455                 |           0                   |
+--------------+------------+--------------+------------+------------------------------+-------------------------------+
|  2023-04-03  | project1   | dataset_B    | table_y    |            0                 | 52500873256                   |
+--------------+------------+--------------+------------+------------------------------+-------------------------------+
|  2023-04-03  | project1   | dataset_B    | table_t    |            0                 | 32513713981                   |
+--------------+------------+--------------+------------+------------------------------+-------------------------------+
|  2023-04-03  | project2   | dataset_C    | table_m    |   8894535352                 |           0                   |
+--------------+------------+--------------+------------+------------------------------+-------------------------------+
|  2023-04-03  | project2   | dataset_C    | table_n    |   4183337201                 |           0                   |
+--------------+------------+--------------+------------+------------------------------+-------------------------------+
```
