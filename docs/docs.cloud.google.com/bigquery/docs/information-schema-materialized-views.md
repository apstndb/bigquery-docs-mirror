# MATERIALIZED\_VIEWS view

The `  INFORMATION_SCHEMA.MATERIALIZED_VIEWS  ` view contains status about materialized views.

## Required permissions

To get the permissions that you need to query the `  INFORMATION_SCHEMA.MATERIALIZED_VIEWS  ` view, ask your administrator to grant you the [BigQuery Metadata Viewer](/iam/docs/roles-permissions/bigquery#bigquery.metadataViewer) ( `  roles/bigquery.metadataViewer  ` ) IAM role on your project or dataset. For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

This predefined role contains the permissions required to query the `  INFORMATION_SCHEMA.MATERIALIZED_VIEWS  ` view. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

The following permissions are required to query the `  INFORMATION_SCHEMA.MATERIALIZED_VIEWS  ` view:

  - `  bigquery.tables.get  `
  - `  bigquery.tables.list  `

You might also be able to get these permissions with [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

For more information about BigQuery permissions, see [Access control with IAM](/bigquery/docs/access-control) .

## Schema

When you query the `  INFORMATION_SCHEMA.MATERIALIZED_VIEWS  ` view, the query results contain one row for each materialized view in a dataset.

The `  INFORMATION_SCHEMA.MATERIALIZED_VIEWS  ` view has the following schema:

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
<td>The name of the project that contains the dataset. Also referred to as the <code dir="ltr" translate="no">       projectId      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       table_schema      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the dataset that contains the materialized view. Also referred to as the <code dir="ltr" translate="no">       datasetId      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       table_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the materialized view. Also referred to as the <code dir="ltr" translate="no">       tableId      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       last_refresh_time      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>The time when this materialized view was last refreshed.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       refresh_watermark      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>The refresh watermark of the materialized view. The data contained in materialized view base tables up to this time are included in the materialized view cache.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       last_refresh_status      </code></td>
<td><code dir="ltr" translate="no">       RECORD      </code></td>
<td>Error result of the last automatic refresh job as an <a href="/bigquery/docs/reference/rest/v2/ErrorProto">ErrorProto</a> object. If present, indicates that the last automatic refresh was unsuccessful.</td>
</tr>
</tbody>
</table>

For stability, we recommend that you explicitly list columns in your information schema queries instead of using a wildcard ( `  SELECT *  ` ). Explicitly listing columns prevents queries from breaking if the underlying schema changes.

## Scope and syntax

Queries against this view must include a dataset or a region qualifier. For queries with a dataset qualifier, you must have permissions for the dataset. For queries with a region qualifier, you must have permissions for the project. For more information, see [Syntax](/bigquery/docs/information-schema-intro#syntax) . The following table explains the region and resource scopes for this view:

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
<td><code dir="ltr" translate="no">       [               PROJECT_ID              .]`region-               REGION              `.INFORMATION_SCHEMA.MATERIALIZED_VIEWS      </code></td>
<td>Project level</td>
<td><code dir="ltr" translate="no">         REGION       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       [               PROJECT_ID              .]               DATASET_ID              .INFORMATION_SCHEMA.MATERIALIZED_VIEWS      </code></td>
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
SELECT * FROM myDataset.INFORMATION_SCHEMA.MATERIALIZED_VIEWS;

-- Returns metadata for all views in a region.
SELECT * FROM region-us.INFORMATION_SCHEMA.MATERIALIZED_VIEWS;
```

## Examples

##### Example 1:

The following example retrieves all the unhealthy materialized views from the `  INFORMATION_SCHEMA.MATERIALIZED_VIEWS  ` view. It returns the materialized views with non `  NULL  ` `  last_refresh_status  ` values in `  mydataset  ` in your default project — `  myproject  ` .

To run the query against a project other than your default project, add the project ID to the dataset in the following format: ``  ` project_id `. dataset .INFORMATION_SCHEMA.MATERIALIZED_VIEWS  `` ; for example, ``  `myproject`.mydataset.INFORMATION_SCHEMA.MATERIALIZED_VIEWS  `` .

``` text
SELECT
  table_name, last_refresh_status
FROM
  mydataset.INFORMATION_SCHEMA.MATERIALIZED_VIEWS
WHERE
  last_refresh_status IS NOT NULL;
```

**Note:** `  INFORMATION_SCHEMA  ` view names are case-sensitive.

The result is similar to the following:

``` text
  +---------------+---------------------------------------------------------------------+
  |  table_name   |                        last_refresh_status                          |
  +---------------------------------------------------------------------+---------------+
  |  myview       |   {"reason":"invalidQuery","location":"query","message":"..."}      |
  +---------------------------------------------------------------------+---------------+
  
```

##### Example 2:

The following example retrieves the `  last_refresh_time  ` and `  refresh_watermark  ` of materialized view `  myview  ` in `  mydataset  ` in your default project — `  myproject  ` . The result shows when the materialized was last refreshed and up to when data of base tables are collected into the materialized view cache.

To run the query against a project other than your default project, add the project ID to the dataset in the following format: ``  ` project_id `. dataset .INFORMATION_SCHEMA.MATERIALIZED_VIEWS  `` ; for example, ``  `myproject`.mydataset.INFORMATION_SCHEMA.MATERIALIZED_VIEWS  `` .

``` text
SELECT
  table_name, last_refresh_time, refresh_watermark
FROM
  mydataset.INFORMATION_SCHEMA.MATERIALIZED_VIEWS
WHERE
  table_name = 'myview';
```

**Note:** `  INFORMATION_SCHEMA  ` view names are case-sensitive.

The result is similar to the following:

``` text
  +---------------+------------------------------------------------+
  |  table_name   |  last_refresh_time     | refresh_watermark     |
  +---------------+------------------------------------------------+
  |  myview       | 2023-02-22 19:37:17    | 2023-03-08 16:52:57   |
  +---------------+------------------------------------------------+
  
```

**Note:** If there have been no recent changes to the base tables, BigQuery periodically increases the `  refresh_watermark  ` to indicate that the materialized view is up-to-date without actually refreshing it. As a result, the `  last_refresh_time  ` can be earlier than the `  refresh_watermark  ` .
