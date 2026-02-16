# SEARCH\_INDEXES\_BY\_ORGANIZATION view

[BigQuery search indexes](/bigquery/docs/search-intro) provide free index management until your organization reaches the [limit](/bigquery/quotas#index_limits) in a given region. You can use the `  INFORMATION_SCHEMA.SEARCH_INDEXES_BY_ORGANIZATION  ` view to understand your current consumption towards that limit, broken down by projects and tables. The `  INFORMATION_SCHEMA.SEARCH_INDEXES_BY_ORGANIZATION  ` view contains one row for each search index for the whole organization associated with the current project.

**Note:** The data in the `  INFORMATION_SCHEMA.SEARCH_INDEXES_BY_ORGANIZATION  ` view isn't kept in real time, and might be delayed by a few seconds to a few minutes.

## Required permissions

To query the `  INFORMATION_SCHEMA.SEARCH_INDEXES_BY_ORGANIZATION  ` view, you need the following Identity and Access Management (IAM) permissions for your organization:

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

The `  INFORMATION_SCHEMA.SEARCH_INDEXES_BY_ORGANIZATION  ` view has the following schema:

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
<td>The name of the project that contains the dataset.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       project_number      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The project number that contains the dataset.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       index_catalog      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the project that contains the dataset.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       index_schema      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the dataset that contains the index.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       table_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the base table that the index is created on.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       index_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the search index.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       index_status      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The status of the index can be one of the following:<br />

<ul>
<li><code dir="ltr" translate="no">         ACTIVE        </code> : the index is usable or being created.</li>
<li><code dir="ltr" translate="no">         PENDING DISABLEMENT        </code> : the total size of indexed base tables exceeds your organization's <a href="https://cloud.google.com/bigquery/quotas#index_limits">limit</a> ; the index is queued for deletion. While in this state, the index is usable in search queries and you are charged for the search index storage.</li>
<li><code dir="ltr" translate="no">         TEMPORARILY DISABLED        </code> : either the total size of indexed base tables exceeds your organization's <a href="https://cloud.google.com/bigquery/quotas#index_limits">limit</a> , or the base indexed table is smaller than 10 GB. While in this state, the index is not used in search queries and you are not charged for the search index storage.</li>
<li><code dir="ltr" translate="no">         PERMANENTLY DISABLED        </code> : there is an incompatible schema change on the base table, such as changing the type of an indexed column from <code dir="ltr" translate="no">         STRING        </code> to <code dir="ltr" translate="no">         INT64        </code> .</li>
</ul></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       index_status_details      </code></td>
<td><code dir="ltr" translate="no">       RECORD      </code></td>
<td>The record contains following fields:<br />

<ul>
<li><code dir="ltr" translate="no">         throttle_status        </code> : indicates the throttle status of the search index, possible values are as follows:
<ul>
<li><code dir="ltr" translate="no">           UNTHROTTLED          </code> : the index is usable.</li>
<li><code dir="ltr" translate="no">           BASE_TABLE_TOO_SMALL          </code> : the base table size is smaller than 10 GB. This limit applies whether or not you use your own reservation for your index-management jobs. In this case, the index is temporarily disabled and search queries don't use the index.</li>
<li><code dir="ltr" translate="no">           BASE_TABLE_TOO_LARGE          </code> : the base table size exceeds your organization's <a href="https://cloud.google.com/bigquery/quotas#index_limits">limit</a> .</li>
<li><code dir="ltr" translate="no">           ORGANIZATION_LIMIT_EXCEEDED          </code> : the total size of indexed base tables in your organization exceeds your organization's <a href="https://cloud.google.com/bigquery/quotas#index_limits">limit</a> .</li>
</ul></li>
<li><code dir="ltr" translate="no">         message        </code> : detailed message that describes the index status.</li>
</ul></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       use_background_reservation      </code></td>
<td><code dir="ltr" translate="no">       BOOL      </code></td>
<td>Indicates whether the index maintenance uses the <code dir="ltr" translate="no">         BACKGROUND       </code> reservation. This is set to <code dir="ltr" translate="no">       FALSE      </code> when the index maintenance uses the limit.</td>
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
<td><code dir="ltr" translate="no">       [`               PROJECT_ID              `.]`region-               REGION              `.INFORMATION_SCHEMA.SEARCH_INDEXES_BY_ORGANIZATION      </code></td>
<td>Organization that contains the specified project</td>
<td><code dir="ltr" translate="no">         REGION       </code></td>
</tr>
</tbody>
</table>

Replace the following:

  - Optional: `  PROJECT_ID  ` : the ID of your Google Cloud project. If not specified, the default project is used.

  - `  REGION  ` : the [region](/bigquery/docs/locations) for your project. For example, ``  `myproject`.`region-us`.INFORMATION_SCHEMA.SEARCH_INDEXES_BY_ORGANIZATION  `` .
    
    **Note:** You must use [a region qualifier](/bigquery/docs/information-schema-intro#region_qualifier) to query `  INFORMATION_SCHEMA  ` views. The location of the query execution must match the region of the `  INFORMATION_SCHEMA  ` view.

## Index throttling

If an index is throttled, its table size is not counted towards your organization's limit. This throttling occurs when the base table size falls under 10 GB or exceeds your organization's [limit](/bigquery/quotas#index_limits) . When an index is throttled, its management jobs are paused, causing the index to become stale and eventually temporarily disabled. Consequently, search queries are unable to use the index.

You can set up alerts to get notified when a certain threshold is exceeded, similar to [setting up alerts for scheduled queries](/bigquery/docs/create-alert-scheduled-query) . For example, set up an alert when the table size exceeds 70% of the quota limit, so that you have time to act.

## Examples

This section includes example queries of the `  INFORMATION_SCHEMA.SEARCH_INDEXES_BY_ORGANIZATION  ` view.

#### Find if the consumption exceeds the limit in a given region

The following example illustrates if the total indexed base table size across an organization, utilizing shared slots within the US multi-region, exceeds 100 TB:

``` text
WITH
 indexed_base_table_size AS (
 SELECT
   SUM(base_table.total_logical_bytes) AS total_logical_bytes
 FROM
   `region-us`.INFORMATION_SCHEMA.SEARCH_INDEXES_BY_ORGANIZATION AS search_index
 JOIN
   `region-us`.INFORMATION_SCHEMA.TABLE_STORAGE_BY_ORGANIZATION AS base_table
 ON
   (search_index.table_name = base_table.table_name
     AND search_index.project_id = base_table.project_id
     AND search_index.index_schema = base_table.table_schema)
 WHERE
   TRUE
   -- Excludes search indexes that are permanently disabled.
   AND search_index.index_status != 'PERMANENTLY DISABLED'
   -- Excludes BASE_TABLE_TOO_SMALL search indexes whose base table size is
   -- less than 10 GB. These tables don't count toward the limit.
   AND search_index.index_status_details.throttle_status != 'BASE_TABLE_TOO_SMALL'
   -- Excludes search indexes whose project has BACKGROUND reservation purchased
   -- for search indexes.
   AND search_index.use_background_reservation = false
 -- Outputs the total indexed base table size if it exceeds 100 TB,
 -- otherwise, doesn't return any output.
)
SELECT * FROM indexed_base_table_size
WHERE total_logical_bytes >= 109951162777600 -- 100 TB
```

The result is similar to the following:

``` text
+---------------------+
| total_logical_bytes |
+---------------------+
|     109951162777601 |
+---------------------+
```

#### Find total indexed base table size by projects in a region

The following example gives the breakdown on each project in a US multi-region with the total size of indexed base tables:

``` text
SELECT
 search_index.project_id,
 search_index.use_background_reservation,
 SUM(base_table.total_logical_bytes) AS total_logical_bytes
FROM
 `region-us`.INFORMATION_SCHEMA.SEARCH_INDEXES_BY_ORGANIZATION AS search_index
JOIN
 `region-us`.INFORMATION_SCHEMA.TABLE_STORAGE_BY_ORGANIZATION AS base_table
ON
 (search_index.table_name = base_table.table_name
   AND search_index.project_id = base_table.project_id
   AND search_index.index_schema = base_table.table_schema)
WHERE
 TRUE
  -- Excludes search indexes that are permanently disabled.
  AND search_index.index_status != 'PERMANENTLY DISABLED'
  -- Excludes BASE_TABLE_TOO_SMALL search indexes whose base table size is
  -- less than 10 GB. These tables don't count toward limit.
 AND search_index.index_status_details.throttle_status != 'BASE_TABLE_TOO_SMALL'
GROUP BY search_index.project_id, search_index.use_background_reservation
```

The result is similar to the following:

``` text
+---------------------+----------------------------+---------------------+
|     project_id      | use_background_reservation | total_logical_bytes |
+---------------------+----------------------------+---------------------+
| projecta            |     true                   |     971329178274633 |
+---------------------+----------------------------+---------------------+
| projectb            |     false                  |     834638211024843 |
+---------------------+----------------------------+---------------------+
| projectc            |     false                  |     562910385625126 |
+---------------------+----------------------------+---------------------+
```

#### Find throttled search indexes

This following example returns all search indexes that are throttled within the organization and region:

``` text
SELECT project_id, index_schema, table_name, index_name
FROM
 `region-us`.INFORMATION_SCHEMA.SEARCH_INDEXES_BY_ORGANIZATION
WHERE
 -- Excludes search indexes that are permanently disabled.
 index_status != 'PERMANENTLY DISABLED'
 AND index_status_details.throttle_status IN ('ORGANIZATION_LIMIT_EXCEEDED', 'BASE_TABLE_TOO_LARGE')
```

The result is similar to the following:

``` text
+--------------------+--------------------+---------------+----------------+
|     project_id     |    index_schema    |  table_name   |   index_name   |
+--------------------+--------------------+---------------+----------------+
|     projecta       |     dataset_us     |   table1      |    index1      |
|     projectb       |     dataset_us     |   table1      |    index1      |
+--------------------+--------------------+---------------+----------------+
```
