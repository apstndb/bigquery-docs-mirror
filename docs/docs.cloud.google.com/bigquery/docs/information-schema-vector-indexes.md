# VECTOR\_INDEXES view

The `  INFORMATION_SCHEMA.VECTOR_INDEXES  ` view contains one row for each vector index in a dataset.

## Required permissions

To see [vector index](/bigquery/docs/vector-index) metadata, you need the `  bigquery.tables.get  ` or `  bigquery.tables.list  ` Identity and Access Management (IAM) permission on the table with the index. Each of the following predefined IAM roles includes at least one of these permissions:

  - `  roles/bigquery.admin  `
  - `  roles/bigquery.dataEditor  `
  - `  roles/bigquery.dataOwner  `
  - `  roles/bigquery.dataViewer  `
  - `  roles/bigquery.metadataViewer  `
  - `  roles/bigquery.user  `

For more information about BigQuery permissions, see [Access control with IAM](/bigquery/docs/access-control) .

## Schema

When you query the `  INFORMATION_SCHEMA.VECTOR_INDEXES  ` view, the query results contain one row for each vector index in a dataset.

The `  INFORMATION_SCHEMA.VECTOR_INDEXES  ` view has the following schema:

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
<td>The name of the table that the index is created on.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       index_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the vector index.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       index_status      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The status of the index: <code dir="ltr" translate="no">       ACTIVE      </code> , <code dir="ltr" translate="no">       PENDING           DISABLEMENT      </code> , <code dir="ltr" translate="no">       TEMPORARILY DISABLED      </code> , or <code dir="ltr" translate="no">       PERMANENTLY DISABLED      </code> .
<ul>
<li><code dir="ltr" translate="no">         ACTIVE        </code> means that the index is usable or being created. Refer to the <code dir="ltr" translate="no">         coverage_percentage        </code> to see the progress of index creation.</li>
<li><code dir="ltr" translate="no">         PENDING DISABLEMENT        </code> means that the total size of indexed tables exceeds your organization's <a href="/bigquery/quotas#index_limits">limit</a> ; the index is queued for deletion. While in this state, the index is usable in vector search queries and you are charged for the vector index storage.</li>
<li><code dir="ltr" translate="no">         TEMPORARILY DISABLED        </code> means that either the total size of indexed tables exceeds your organization's <a href="/bigquery/quotas#index_limits">limit</a> , or the indexed table is smaller than 10 MB. While in this state, the index isn't used in vector search queries and you aren't charged for the vector index storage.</li>
<li><code dir="ltr" translate="no">         PERMANENTLY DISABLED        </code> means that there is an incompatible schema change on the indexed table.</li>
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
<td>The data definition language (DDL) statement used to create the index.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       coverage_percentage      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>The approximate percentage of table data that has been indexed. 0% means the index is not usable in a <code dir="ltr" translate="no">       VECTOR_SEARCH      </code> query, even if some data has already been indexed.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       unindexed_row_count      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>The number of rows in the table that have not been indexed.</td>
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
<td><code dir="ltr" translate="no">       last_index_alteration_info      </code></td>
<td><code dir="ltr" translate="no">       RECORD      </code></td>
<td>The details of the latest user-triggered index alteration, containing following fields:
<ul>
<li><code dir="ltr" translate="no">         status        </code> : a <code dir="ltr" translate="no">         STRING        </code> value that indicates the alteration status. Possible values are <code dir="ltr" translate="no">         NULL        </code> (complete), <code dir="ltr" translate="no">         IN_PROGRESS        </code> , and <code dir="ltr" translate="no">         FAILED        </code> .</li>
<li><code dir="ltr" translate="no">         message        </code> : a <code dir="ltr" translate="no">         STRUCT        </code> field that contains the details of the <code dir="ltr" translate="no">         FAILED        </code> status as an <a href="/bigquery/docs/reference/rest/v2/ErrorProto">ErrorProto</a> . The value is <code dir="ltr" translate="no">         NULL        </code> for other statuses.</li>
<li><code dir="ltr" translate="no">         new_coverage_percentage        </code> : an <code dir="ltr" translate="no">         INT64        </code> value that contains the approximate percentage of table data that has been indexed for the alteration.</li>
<li><code dir="ltr" translate="no">         start_time        </code> : the timestamp when the alteration was initiated.</li>
<li><code dir="ltr" translate="no">         end_time        </code> : the timestamp when the alteration enters the <code dir="ltr" translate="no">         FAILED        </code> status.</li>
<li><code dir="ltr" translate="no">         ddl        </code> : the data definition language (DDL) statement used to alter the index.</li>
</ul></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       last_model_build_time      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>The start time of the last index model build.</td>
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
<td><code dir="ltr" translate="no">       [               PROJECT_ID              .]               DATASET_ID              .INFORMATION_SCHEMA.VECTOR_INDEXES      </code></td>
<td>Dataset level</td>
<td>Dataset location</td>
</tr>
</tbody>
</table>

Replace the following:

  - Optional: `  PROJECT_ID  ` : the ID of your Google Cloud project. If not specified, the default project is used.
  - `  DATASET_ID  ` : the ID of your dataset. For more information, see [Dataset qualifier](/bigquery/docs/information-schema-intro#dataset_qualifier) .
    **Note:** You must use [a region qualifier](/bigquery/docs/information-schema-intro#region_qualifier) to query `  INFORMATION_SCHEMA  ` views. The location of the query execution must match the region of the `  INFORMATION_SCHEMA  ` view.

**Example**

``` text
-- Returns metadata for vector indexes in a single dataset.
SELECT * FROM myDataset.INFORMATION_SCHEMA.VECTOR_INDEXES;
```

## Example

The following example shows all active vector indexes on tables in the dataset `  my_dataset  ` , located in the project `  my_project  ` . It includes their names, the DDL statements used to create them, and their coverage percentage. If an indexed base table is less than 10 MB, then its index is not populated, in which case the `  coverage_percentage  ` value is 0.

``` text
SELECT table_name, index_name, ddl, coverage_percentage
FROM my_project.my_dataset.INFORMATION_SCHEMA.VECTOR_INDEXES
WHERE index_status = 'ACTIVE';
```

The result is similar to the following:

``` text
+------------+------------+-------------------------------------------------------------------------------------------------+---------------------+
| table_name | index_name | ddl                                                                                             | coverage_percentage |
+------------+------------+-------------------------------------------------------------------------------------------------+---------------------+
| table1     | indexa     | CREATE VECTOR INDEX `indexa` ON `my_project.my_dataset.table1`(embeddings)                      | 100                 |
|            |            | OPTIONS (distance_type = 'EUCLIDEAN', index_type = 'IVF', ivf_options = '{"num_lists": 100}')   |                     |
+------------+------------+-------------------------------------------------------------------------------------------------+---------------------+
| table2     | indexb     | CREATE VECTOR INDEX `indexb` ON `my_project.my_dataset.table2`(vectors)                         | 42                  |
|            |            | OPTIONS (distance_type = 'COSINE', index_type = 'IVF', ivf_options = '{"num_lists": 500}')      |                     |
+------------+------------+-------------------------------------------------------------------------------------------------+---------------------+
| table3     | indexc     | CREATE VECTOR INDEX `indexc` ON `my_project.my_dataset.table3`(vectors)                         | 98                  |
|            |            | OPTIONS (distance_type = 'DOT_PRODUCT', index_type = 'TREE_AH',                                 |                     |
|            |            |          tree_ah_options = '{"leaf_node_embedding_count": 1000, "normalization_type": "NONE"}') |                     |
+------------+------------+-------------------------------------------------------------------------------------------------+---------------------+
```
