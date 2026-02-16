# SCHEMATA\_LINKS view

The `  INFORMATION_SCHEMA.SCHEMATA_LINKS  ` view contains one row for each [linked dataset](/bigquery/docs/analytics-hub-introduction#linked_datasets) that is shared using BigQuery sharing. This view also contains individual resources, such as tables or views, in a project that is shared using [data clean rooms](/bigquery/docs/data-clean-rooms) . This view displays one row for each individual resource in the linked dataset.

## Required permission

To query the `  INFORMATION_SCHEMA.SCHEMATA_LINKS  ` view, you need the `  bigquery.datasets.get  ` Identity and Access Management (IAM) permission at the project level.

Each of the following predefined IAM roles includes the permissions that you need in order to query the `  INFORMATION_SCHEMA.SCHEMATA_LINKS  ` view:

  - `  roles/bigquery.admin  `
  - `  roles/bigquery.dataEditor  `
  - `  roles/bigquery.dataOwner  `
  - `  roles/bigquery.dataViewer  `

For more information about BigQuery permissions, see [Access control with IAM](/bigquery/docs/access-control) .

## Schema

The `  INFORMATION_SCHEMA.SCHEMATA_LINKS  ` view has the following schema:

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
<td><code dir="ltr" translate="no">       catalog_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the project that contains the source dataset.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       schema_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the source dataset. The dataset name is also referred to as the <code dir="ltr" translate="no">       datasetId      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       linked_schema_catalog_number      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The project number of the project that contains the linked dataset.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       linked_schema_catalog_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The project name of the project that contains the linked dataset.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       linked_schema_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the linked dataset. The dataset name is also referred to as the <code dir="ltr" translate="no">       datasetId      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       linked_schema_creation_time      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>The time when the linked dataset was created.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       linked_schema_org_display_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The display name of the organization in which the linked dataset is created.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       shared_asset_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The ID of the asset that is shared using data clean rooms. This value is <code dir="ltr" translate="no">       null      </code> if <code dir="ltr" translate="no">       link_type      </code> is <code dir="ltr" translate="no">       REGULAR      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       link_type      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The type of linked dataset. Possible values are <code dir="ltr" translate="no">       REGULAR      </code> or <code dir="ltr" translate="no">       DCR      </code> (Data clean rooms).</td>
</tr>
</tbody>
</table>

For stability, we recommend that you explicitly list columns in your information schema queries instead of using a wildcard ( `  SELECT *  ` ). Explicitly listing columns prevents queries from breaking if the underlying schema changes.

## Scope and syntax

Queries against this view must include a [region qualifier](/bigquery/docs/information-schema-intro#syntax) . If you don't specify a regional qualifier, metadata is retrieved from the US region. The following table explains the region scope for this view:

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
<td><code dir="ltr" translate="no">       [               PROJECT_ID              .]INFORMATION_SCHEMA.SCHEMATA_LINKS      </code></td>
<td>Project level</td>
<td>US region</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       [               PROJECT_ID              .]`region-               REGION              `.INFORMATION_SCHEMA.SCHEMATA_LINKS      </code></td>
<td>Project level</td>
<td><code dir="ltr" translate="no">         REGION       </code></td>
</tr>
</tbody>
</table>

Replace the following:

  - Optional: `  PROJECT_ID  ` : the ID of your Google Cloud project. If not specified, the default project is used.
  - `  REGION  ` : any [dataset region name](/bigquery/docs/locations) . For example, ``  `region-us`  `` .
    **Note:** You must use [a region qualifier](/bigquery/docs/information-schema-intro#region_qualifier) to query `  INFORMATION_SCHEMA  ` views. The location of the query execution must match the region of the `  INFORMATION_SCHEMA  ` view.

## Examples

This section lists examples to query the `  INFORMATION_SCHEMA.SCHEMATA_LINKS  ` view.

**Example: List all linked datasets against another project**

The following example lists all the linked datasets against another project named `  otherproject  ` within the `  EU  ` multi-region:

``` text
SELECT * FROM `otherproject`.`region-eu`.INFORMATION_SCHEMA.SCHEMATA_LINKS;
```

The output is similar to the following. Some columns are omitted to simplify the output.

``` text
+---------------------+----------------+----------------------------+------------------------------+--------------------+--------------------------------+-----------------------------+-----------------+-----------+
|    catalog_name    |  schema_name    | linked_schema_catalog_name | linked_schema_catalog_number | linked_schema_name | linked_schema_org_display_name | linked_schema_creation_time | shared_asset_id | link_type |
+---------------------+----------------+----------------------------+------------------------------+--------------------+--------------------------------+-----------------------------+-----------------+-----------+
|  otherproject      | source_dataset  | subscriptioproject1        |                974999999291  | linked_dataset     |  subscriptionorg1              |         2025-08-07 05:02:27 | NULL            | REGULAR   |
|  otherproject      | source_dataset1 | subscriptionproject2       |                974999999292  | test_dcr           |  subscriptionorg2              |         2025-08-07 10:08:50 | test_table      | DCR       |
+---------------------+----------------+----------------------------+------------------------------+--------------------+--------------------------------+-----------------------------+-----------------+-----------+
```

**Example: List all linked datasets by a shared dataset**

The following example lists all the linked datasets by a shared dataset named `  sharedataset  ` in the `  US  ` multi-region:

``` text
SELECT * FROM INFORMATION_SCHEMA.SCHEMATA_LINKS WHERE schema_name = 'sharedataset';
```

The output is similar to the following. Some columns are omitted to simplify the output.

``` text
+---------------------+----------------+----------------------------+------------------------------+--------------------+--------------------------------+-----------------------------+-----------------+-----------+
|    catalog_name     |  schema_name   | linked_schema_catalog_name | linked_schema_catalog_number | linked_schema_name | linked_schema_org_display_name | linked_schema_creation_time | shared_asset_id | link_type |
+---------------------+----------------+----------------------------+------------------------------+--------------------+--------------------------------+-----------------------------+-----------------+-----------+
|  myproject          | sharedataset   | subscriptionproject1       |                974999999291  | linked_dataset     |  subscriptionorg1              |         2025-08-07 05:02:27 | NULL            | REGULAR   |
|  myproject          | sharedataset   | subscriptionproject2       |                974999999292  | test_dcr           |  subscriptionorg2              |         2025-08-07 10:08:50 | test_table      | DCR       |
+---------------------+----------------+----------------------------+------------------------------+--------------------+--------------------------------+-----------------------------+-----------------+-----------+
```

**Example: List all resources shared using a data clean room**

The following example lists all the individual resources, such as tables or views, that are shared using a data clean room from another project named `  otherproject  ` within the `  EU  ` multi-region:

``` text
SELECT * FROM `otherproject`.`region-eu`.INFORMATION_SCHEMA.SCHEMATA_LINKS where link_type='DCR';
```

The output is similar to the following. Some columns are omitted to simplify the output.

``` text
+---------------------+----------------+----------------------------+------------------------------+--------------------+--------------------------------+-----------------------------+-----------------+-----------+
|    catalog_name     |  schema_name   | linked_schema_catalog_name | linked_schema_catalog_number | linked_schema_name | linked_schema_org_display_name | linked_schema_creation_time | shared_asset_id | link_type |
+---------------------+----------------+----------------------------+------------------------------+--------------------+--------------------------------+-----------------------------+-----------------+-----------+
|  otherproject       | sharedataset1  | subscriptionproject1       |                 974999999291 | test_dcr1          |  subscriptionorg1              |         2025-08-07 05:02:27 | test_view       | DCR       |
|  otherproject       | sharedataset2  | subscriptionproject2       |                 974999999292 | test_dcr2          |  subscriptionorg2              |         2025-08-07 10:08:50 | test_table      | DCR       |
+---------------------+----------------+----------------------------+------------------------------+--------------------+--------------------------------+-----------------------------+-----------------+-----------+
```
