# TABLE\_STORAGE\_BY\_ORGANIZATION view

The `  INFORMATION_SCHEMA.TABLE_STORAGE_BY_ORGANIZATION  ` view contain one row for each table or materialized view for the whole organization associated with the current project.

The data in this table is not kept in real time, and might be delayed by a few seconds to a few minutes. Storage changes that are caused by partition or table expiration alone, or that are caused by modifications to the dataset time travel window, might take up to a day to be reflected in the `  INFORMATION_SCHEMA.TABLE_STORAGE  ` view. In cases of dataset deletion where the dataset contains more than 1,000 tables, this view won't reflect the change until the [time travel window](/bigquery/docs/time-travel#time_travel) for the deleted dataset has passed.

The table storage views give you a convenient way to observe your current storage consumption, and in addition provide details on whether your storage uses logical uncompressed bytes, physical compressed bytes, or time travel bytes. This information can help you with tasks like planning for future growth and understanding the update patterns for tables.

## Data included in the `     *_BYTES    ` columns

The `  *_BYTES  ` columns in the table storage views include information about your use of storage bytes. This information is determined by looking at your storage usage for materialized views and the following types of tables:

  - Permanent tables created through any of the methods described in [Create and use tables](/bigquery/docs/tables) .
  - Temporary tables created in [sessions](/bigquery/docs/sessions-write-queries#use_temporary_tables_in_sessions) . These tables are placed into datasets with generated names like "\_c018003e063d09570001ef33ae401fad6ab92a6a".
  - Temporary tables created in [multi-statement queries](/bigquery/docs/multi-statement-queries#temporary_tables) ("scripts"). These tables are placed into datasets with generated names like "\_script72280c173c88442c3a7200183a50eeeaa4073719".

Data stored in the [query results cache](/bigquery/docs/writing-results#temporary_and_permanent_tables) is not billed to you and so is not included in the `  *_BYTES  ` column values.

Clones and snapshots show `  *_BYTES  ` column values as if they were complete tables, rather than showing the delta from the storage used by the base table, so they are an over-estimation. Your bill does account correctly for this delta in storage usage. For more information on the delta bytes stored and billed by clones and snapshots, see the [`  TABLE_STORAGE_USAGE_TIMELINE  ` view](/bigquery/docs/information-schema-table-storage-usage) .

## Forecast storage billing

In order to forecast the monthly storage billing for a dataset, you can use either the `  logical  ` or `  physical *_BYTES  ` columns in this view, depending on the [dataset storage billing model](/bigquery/docs/datasets-intro#dataset_storage_billing_models) used by the dataset. Please note that this is only a rough forecast, and the precise billing amounts are calculated based on the usage by BigQuery storage billing infrastructure and visible in Cloud Billing.

For datasets that use a logical billing model, you can forecast your monthly storage costs as follows:

(( `  ACTIVE_LOGICAL_BYTES  ` value / `  POW  ` (1024, 3)) \* active logical bytes pricing) + (( `  LONG_TERM_LOGICAL_BYTES  ` value / `  POW  ` (1024, 3)) \* long-term logical bytes pricing)

The `  ACTIVE_LOGICAL_BYTES  ` value for a table reflects the active bytes currently used by that table.

For datasets that use a physical billing model, you can forecast your storage costs as follows:

(( `  ACTIVE_PHYSICAL_BYTES + FAIL_SAFE_PHYSICAL_BYTES  ` value / `  POW  ` (1024, 3)) \* active physical bytes pricing) + (( `  LONG_TERM_PHYSICAL_BYTES  ` value / `  POW  ` (1024, 3)) \* long-term physical bytes pricing)

The `  ACTIVE_PHYSICAL_BYTES  ` value for a table reflects the active bytes currently used by that table plus the bytes used for time travel for that table.

To see the active bytes of the table alone, subtract the `  TIME_TRAVEL_PHYSICAL_BYTES  ` value from the `  ACTIVE_PHYSICAL_BYTES  ` value.

For more information, see [Storage pricing](https://cloud.google.com/bigquery/pricing#storage) .

## Required permissions

To query the `  INFORMATION_SCHEMA.TABLE_STORAGE_BY_ORGANIZATION  ` view, you need the following Identity and Access Management (IAM) permissions for your organization:

  - `  bigquery.tables.get  `
  - `  bigquery.tables.list  `

Each of the following predefined IAM roles includes the preceding permissions:

  - `  roles/bigquery.admin  `
  - `  roles/bigquery.dataViewer  `
  - `  roles/bigquery.dataEditor  `
  - `  roles/bigquery.metadataViewer  `

This schema view is only available to users with defined [Google Cloud organizations](/resource-manager/docs/cloud-platform-resource-hierarchy#organizations) .

For more information about BigQuery permissions, see [Access control with IAM](/bigquery/docs/access-control) .

## Schema

The `  INFORMATION_SCHEMA.TABLE_STORAGE_BY_ORGANIZATION  ` view has the following schema:

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
<td><code dir="ltr" translate="no">       project_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The project ID of the project that contains the dataset.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       project_number      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td>The project number of the project that contains the dataset.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       table_catalog      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The project ID of the project that contains the dataset.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       table_schema      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the dataset that contains the table or materialized view, also referred to as the <code dir="ltr" translate="no">       datasetId      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       table_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the table or materialized view, also referred to as the <code dir="ltr" translate="no">       tableId      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       creation_time      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>The creation time of the table.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       total_rows      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td>The total number of rows in the table or materialized view.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       total_partitions      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td>The number of partitions present in the table or materialized view. Unpartitioned tables return 0.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       total_logical_bytes      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td>Total number of logical (uncompressed) bytes in the table or materialized view.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       active_logical_bytes      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td>Number of logical (uncompressed) bytes that are younger than 90 days.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       long_term_logical_bytes      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td>Number of logical (uncompressed) bytes that are older than 90 days.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       current_physical_bytes      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td>Total number of physical bytes for the current storage of the table across all partitions.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       total_physical_bytes      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td>Total number of physical (compressed) bytes used for storage, including active, long-term, and time travel (deleted or changed data) bytes. Fail-safe (deleted or changed data retained after the time-travel window) bytes aren't included.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       active_physical_bytes      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td>Number of physical (compressed) bytes younger than 90 days, including time travel (deleted or changed data) bytes.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       long_term_physical_bytes      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td>Number of physical (compressed) bytes older than 90 days.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       time_travel_physical_bytes      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td>Number of physical (compressed) bytes used by time travel storage (deleted or changed data).</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       storage_last_modified_time      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>The most recent time that data was written to the table. Returns <code dir="ltr" translate="no">       NULL      </code> if no data exists.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       deleted      </code></td>
<td><code dir="ltr" translate="no">       BOOLEAN      </code></td>
<td>Indicates whether or not the table is deleted.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       table_type      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The type of table. For example, <code dir="ltr" translate="no">       BASE TABLE      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       managed_table_type      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>This column is in Preview. The managed type of the table. For example, <code dir="ltr" translate="no">       NATIVE      </code> or <code dir="ltr" translate="no">       BIGLAKE      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       fail_safe_physical_bytes      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td>Number of physical (compressed) bytes used by the fail-safe storage (deleted or changed data).</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       last_metadata_index_refresh_time      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>The last metadata index refresh time of the table.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       table_deletion_reason      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Table deletion reason if the <code dir="ltr" translate="no">       deleted      </code> field is true. The possible values are as follows:
<ul>
<li><code dir="ltr" translate="no">         TABLE_EXPIRATION:        </code> table deleted after set expiration time</li>
<li><code dir="ltr" translate="no">         DATASET_DELETION:        </code> dataset deleted by user</li>
<li><code dir="ltr" translate="no">         USER_DELETED:        </code> table was deleted by user</li>
</ul></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       table_deletion_time      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>The deletion time of the table.</td>
</tr>
</tbody>
</table>

For stability, we recommend that you explicitly list columns in your information schema queries instead of using a wildcard ( `  SELECT *  ` ). Explicitly listing columns prevents queries from breaking if the underlying schema changes.

## Scope and syntax

Queries against this view must include a [region qualifier](/bigquery/docs/information-schema-intro#syntax) . The following table explains the region scope for this view:

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
<td><code dir="ltr" translate="no">       [`               PROJECT_ID              `.]`region-               REGION              `.INFORMATION_SCHEMA.TABLE_STORAGE_BY_ORGANIZATION      </code></td>
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
SELECT * FROM `myProject`.`region-REGION`.INFORMATION_SCHEMA.TABLE_STORAGE_BY_ORGANIZATION;
```

The following example shows how to return storage information by project for tables in an organization:

``` text
SELECT * FROM `region-REGION`.INFORMATION_SCHEMA.TABLE_STORAGE_BY_ORGANIZATION;
```

## Example

The following example shows you which projects in an organization are currently using the most storage.

``` text
SELECT
  project_id,
  SUM(total_logical_bytes) AS total_logical_bytes
FROM
  `region-REGION`.INFORMATION_SCHEMA.TABLE_STORAGE_BY_ORGANIZATION
GROUP BY
  project_id
ORDER BY
  total_logical_bytes DESC;
```

The result is similar to the following:

``` text
+---------------------+---------------------+
|     project_id      | total_logical_bytes |
+---------------------+---------------------+
| projecta            |     971329178274633 |
+---------------------+---------------------+
| projectb            |     834638211024843 |
+---------------------+---------------------+
| projectc            |     562910385625126 |
+---------------------+---------------------+
```
