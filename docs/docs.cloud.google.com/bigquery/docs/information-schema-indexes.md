# SEARCH\_INDEXES view

The `  INFORMATION_SCHEMA.SEARCH_INDEXES  ` view contains one row for each search index in a dataset.

## Required permissions

To see [search index](/bigquery/docs/search-index) metadata, you need the `  bigquery.tables.get  ` or `  bigquery.tables.list  ` Identity and Access Management (IAM) permission on the table with the index. Each of the following predefined IAM roles includes at least one of these permissions:

  - `  roles/bigquery.admin  `
  - `  roles/bigquery.dataEditor  `
  - `  roles/bigquery.dataOwner  `
  - `  roles/bigquery.dataViewer  `
  - `  roles/bigquery.metadataViewer  `
  - `  roles/bigquery.user  `

For more information about BigQuery permissions, see [Access control with IAM](/bigquery/docs/access-control) .

## Schema

When you query the `  INFORMATION_SCHEMA.SEARCH_INDEXES  ` view, the query results contain one row for each search index in a dataset.

The `  INFORMATION_SCHEMA.SEARCH_INDEXES  ` view has the following schema:

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
<td>The name of the index.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       index_status      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The status of the index: <code dir="ltr" translate="no">       ACTIVE      </code> , <code dir="ltr" translate="no">       PENDING           DISABLEMENT      </code> , <code dir="ltr" translate="no">       TEMPORARILY DISABLED      </code> , or <code dir="ltr" translate="no">       PERMANENTLY DISABLED      </code> .
<ul>
<li><code dir="ltr" translate="no">         ACTIVE        </code> means that the index is usable or being created. Refer to the <code dir="ltr" translate="no">         coverage_percentage        </code> to see the progress of index creation.</li>
<li><code dir="ltr" translate="no">         PENDING DISABLEMENT        </code> means that the total size of indexed base tables exceeds your organization's <a href="/bigquery/quotas#index_limits">limit</a> ; the index is queued for deletion. While in this state, the index is usable in search queries and you are charged for the search index storage.</li>
<li><code dir="ltr" translate="no">         TEMPORARILY DISABLED        </code> means that either the total size of indexed base tables exceeds your organization's <a href="/bigquery/quotas#index_limits">limit</a> , or the base indexed table is smaller than 10GB. While in this state, the index is not used in search queries and you are not charged for the search index storage.</li>
<li><code dir="ltr" translate="no">         PERMANENTLY DISABLED        </code> means that there is an incompatible schema change on the base table, such as changing the type of an indexed column from <code dir="ltr" translate="no">         STRING        </code> to <code dir="ltr" translate="no">         INT64        </code> .</li>
</ul></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       creation_time      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>The time the index was created.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       last_modification_time      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>The last time the index configuration was modified. For example, deleting an indexed column.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       last_refresh_time      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>The last time the table data was indexed. A <code dir="ltr" translate="no">       NULL      </code> value means the index is not yet available.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       disable_time      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>The time the status of the index was set to <code dir="ltr" translate="no">       DISABLED      </code> . The value is <code dir="ltr" translate="no">       NULL      </code> if the index status is not <code dir="ltr" translate="no">       DISABLED      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       disable_reason      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The reason the index was disabled. <code dir="ltr" translate="no">       NULL      </code> if the index status is not <code dir="ltr" translate="no">       DISABLED      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       DDL      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The DDL statement used to create the index.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       coverage_percentage      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>The approximate percentage of table data that has been indexed. 0% means the index is not usable in a <code dir="ltr" translate="no">       SEARCH      </code> query, even if some data has already been indexed.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       unindexed_row_count      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>The number of rows in the base table that have not been indexed.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       total_logical_bytes      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>The number of billable logical bytes for the index.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       total_storage_bytes      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>The number of billable storage bytes for the index.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       analyzer      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The <a href="/bigquery/docs/reference/standard-sql/text-analysis">text analyzer</a> to use to generate tokens for the search index.</td>
</tr>
</tbody>
</table>

For stability, we recommend that you explicitly list columns in your information schema queries instead of using a wildcard ( `  SELECT *  ` ). Explicitly listing columns prevents queries from breaking if the underlying schema changes.

## Scope and syntax

Queries against this view must have a [dataset qualifier](/bigquery/docs/information-schema-intro#syntax) . The following table explains the region scope for this view:

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
<td><code dir="ltr" translate="no">       [               PROJECT_ID              .]               DATASET_ID              .INFORMATION_SCHEMA.SEARCH_INDEXES      </code></td>
<td>Dataset level</td>
<td>Dataset location</td>
</tr>
</tbody>
</table>

Replace the following:

  - Optional: `  PROJECT_ID  ` : the ID of your Google Cloud project. If not specified, the default project is used.
  - `  DATASET_ID  ` : the ID of your dataset. For more information, see [Dataset qualifier](/bigquery/docs/information-schema-intro#dataset_qualifier) .

**Example**

``` text
-- Returns metadata for search indexes in a single dataset.
SELECT * FROM myDataset.INFORMATION_SCHEMA.SEARCH_INDEXES;
```

## Example

The following example shows all active search indexes on tables in the dataset `  my_dataset  ` , located in the project `  my_project  ` . It includes their names, the DDL statements used to create them, their coverage percentage, and their text analyzer. If an indexed base table is less than 10GB, then its index is not populated, in which case `  coverage_percentage  ` is 0.

``` text
SELECT table_name, index_name, ddl, coverage_percentage, analyzer
FROM my_project.my_dataset.INFORMATION_SCHEMA.SEARCH_INDEXES
WHERE index_status = 'ACTIVE';
```

The results should look like the following:

``` text
+-------------+-------------+--------------------------------------------------------------------------------------+---------------------+----------------+
| table_name  | index_name  | ddl                                                                                  | coverage_percentage | analyzer       |
+-------------+-------------+--------------------------------------------------------------------------------------+---------------------+----------------+
| small_table | names_index | CREATE SEARCH INDEX `names_index` ON `my_project.my_dataset.small_table`(names)      | 0                   | NO_OP_ANALYZER |
| large_table | logs_index  | CREATE SEARCH INDEX `logs_index` ON `my_project.my_dataset.large_table`(ALL COLUMNS) | 100                 | LOG_ANALYZER   |
+-------------+-------------+--------------------------------------------------------------------------------------+---------------------+----------------+
```
