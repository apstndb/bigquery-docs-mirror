---
name: documents/docs.cloud.google.com/bigquery/docs/ai-index
uri: https://docs.cloud.google.com/bigquery/docs/ai-index
title: Use AI indexes
description: Learn how to create, monitor, and delete AI indexes in BigQuery, and how to use the AI.SEARCH function to perform natural language searches across indexed columns.
data_source: docs.cloud.google.com
---

# Use AI indexes

> **Preview**
>
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

You can use the [`AI.SEARCH`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-search) function to query your data while BigQuery automatically handles column selection, index optimization, and ongoing maintenance.

This document explains how to create, monitor, and delete AI indexes, and how to query your indexed data.

## Roles and permissions

To get the permissions that you need to Use AI indexes, ask your administrator to grant you the following IAM roles on the project:

- Create or drop an AI index: [BigQuery Data Owner](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner) ( `roles/bigquery.dataOwner` )
- Query a table:
  - [BigQuery Data Viewer](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataViewer) ( `roles/bigquery.dataViewer` )
  - [BigQuery Job User](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.jobUser) ( `roles/bigquery.jobUser` )
- View AI index metadata: [BigQuery Data Viewer](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataViewer) ( `roles/bigquery.dataViewer` )

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## Create an AI index

You can create an AI index on a standard BigQuery table by using the [`CREATE AI INDEX`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_ai_index) data definition language (DDL) statement. You can specify the columns to index, or you can have BigQuery automatically select candidate columns by using the `AUTO COLUMNS` option.

### Limitations on creating AI indexes

When you create an AI index, the following limitations apply:

- Only top-level, non-repeated STRING columns are supported. `ARRAY<STRING>` , `STRUCT` , `JSON` , `ObjectRef` , nested fields, non- `STRING` columns, and pseudocolumns aren't supported.
- You can index up to 50 columns in a single AI index.
- You can create an AI index only on a standard BigQuery table. Views, materialized views, external tables, BigLake tables, Apache Iceberg tables, and table snapshots aren't supported.
- You can't create AI indexes in datasets that have cross-region replicas.
- When you run [`CREATE AI INDEX`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_ai_index) , the base table can have at most 1,000,000 rows for on-demand projects, or up to 100,000,000 rows if the project that contains the table has a `BACKGROUND` reservation assignment.
- `AUTO COLUMNS` selects columns when the `CREATE AI INDEX` statement runs. If you add columns to the table later, they aren't automatically indexed. To include new columns, drop the AI index and create it again.
- Each table supports at most one AI index. A table with an AI index can't also have a vector index or an automatically generated embedding column.

For a full list of limitations, see [Limitations on AI indexes](https://docs.cloud.google.com/bigquery/docs/ai-index-overview#limitations) .

### Create an AI index with `AUTO COLUMNS`

When you create an AI index with `AUTO COLUMNS` , BigQuery automatically scans the table schema and selects up to 50 eligible columns. To create an AI index with `AUTO COLUMNS` , use the `CREATE AI INDEX` DDL statement:

1.  Go to **BigQuery Studio** in the Google Cloud console.

2.  In the query editor, run the following SQL statement:

    ```
    CREATE AI INDEX INDEX_NAME
    ON DATASET_NAME.TABLE_NAME(AUTO COLUMNS);
    ```

    Replace the following:

    - `INDEX_NAME` : the name of the AI index that you're creating. Because the index is always created in the same project and dataset as the base table, you don't need to specify the project or dataset in the index name. The index name must be unique among all indexes on the table.
    - `DATASET_NAME` : the name of the dataset that contains the table.
    - `TABLE_NAME` : the name of the standard table to index.

In the following example, an AI index is created with `AUTO COLUMNS` on `mydataset.products` :

```
CREATE AI INDEX products_ai_index
ON mydataset.products(AUTO COLUMNS);
```

### Create an AI index on specific columns

You can create an AI index on a single column or a specific subset of columns. For example, when your table has more than 50 eligible columns, or when you want to exclude sensitive or high-noise columns, such as opaque IDs, UUIDs, hashes, or raw logs. If you specify multiple columns, place the most informative columns, such as a title or name column, first in the column list.

In the following example, an AI index is created only on the `name` and `description` columns of `mydataset.products` :

```
CREATE AI INDEX products_ai_index
ON mydataset.products(name, description);
```

In the following example, an AI index is created only on the `description` column of `mydataset.products` :

```
CREATE AI INDEX products_ai_index
ON mydataset.products(description);
```

## Search a table with an AI index

You can query a table that has an AI index by using the [`AI.SEARCH`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-search) function. When a table has an AI index, only two arguments are required: `base_table` or `base_table_query` , and `query_value` .

> **Warning:** The `AI.SEARCH` function only searches rows that the AI index has already processed. When you create an AI index or add a large amount of data, results are incomplete until indexing completes. To view progress, query the `coverage_percentage` column of the `INFORMATION_SCHEMA.AI_INDEXES` view.

### Search across all indexed columns

To search across all columns covered by the AI index, omit the `column_to_search` argument and pass the base table and query string.

The following example searches all columns in `mydataset.products` that are covered by the AI index:

```
SELECT
  base.id,
  base.name,
  base.description,
  distance
FROM
  AI.SEARCH(
    TABLE mydataset.products,
    'shoes that keep your feet dry in the rain',
    top_k => 5)
ORDER BY distance;
```

## Monitor the status of AI indexes

You can monitor the status, coverage, and indexed columns of your AI indexes by querying the following `INFORMATION_SCHEMA` views:

- [`INFORMATION_SCHEMA.AI_INDEXES`](https://docs.cloud.google.com/bigquery/docs/information-schema-ai-indexes) : contains metadata about each AI index in a dataset.
- [`INFORMATION_SCHEMA.AI_INDEX_COLUMNS`](https://docs.cloud.google.com/bigquery/docs/information-schema-ai-index-columns) : lists the columns covered by each AI index in a dataset, allowing you to verify which columns were selected when using `AUTO COLUMNS` .
- [`INFORMATION_SCHEMA.JOBS`](https://docs.cloud.google.com/bigquery/docs/information-schema-jobs) : contains information about background jobs, including the background jobs used to create and maintain AI indexes.

### AI index example

The following query shows the coverage and storage size of all AI indexes in `my_project.my_dataset` :

```
SELECT
  table_name,
  index_name,
  creation_time,
  coverage_percentage,
  unindexed_row_count,
  total_logical_bytes
FROM
  my_project.my_dataset.INFORMATION_SCHEMA.AI_INDEXES;
```

The result is similar to the following:

```
+------------+-------------------+---------------------+---------------------+---------------------------+-----------------------+
| table_name | index_name        | creation_time       | coverage_percentage | unindexed_row_count       | total_logical_bytes   |
+------------+-------------------+---------------------+---------------------+---------------------------+-----------------------+
| products   | products_ai_index | 2026-10-01 18:02:11 | 100                 | 0                         | 25344                 |
+------------+-------------------+---------------------+---------------------+---------------------------+-----------------------+
```

### AI index columns example

The following query lists the indexed columns for AI indexes in `my_project.my_dataset` :

```
SELECT
  table_name,
  index_name,
  index_column_name
FROM
  my_project.my_dataset.INFORMATION_SCHEMA.AI_INDEX_COLUMNS;
```

The result is similar to the following:

```
+------------+-------------------+-------------------+
| table_name | index_name        | index_column_name |
+------------+-------------------+-------------------+
| products   | products_ai_index | name              |
| products   | products_ai_index | description       |
| products   | products_ai_index | category          |
| products   | products_ai_index | review            |
+------------+-------------------+-------------------+
```

### Track background job costs example

To track the `total_slot_ms` and `total_bytes_billed` values for background AI index data processing jobs on a table, query the `INFORMATION_SCHEMA.JOBS` view for jobs with a `job_id` prefix of `gc_` :

```
SELECT
  job_id,
  creation_time,
  reservation_id,
  total_slot_ms,
  total_bytes_processed,
  total_bytes_billed
FROM
  `region-REGION`.INFORMATION_SCHEMA.JOBS j
WHERE
  EXISTS (
    SELECT 1
    FROM UNNEST(j.referenced_tables) t
    WHERE
      j.project_id = 'PROJECT_ID'
      AND t.dataset_id = 'DATASET_ID'
      AND t.table_id = 'TABLE'
  )
  AND STARTS_WITH(job_id, 'gc_')
ORDER BY
  j.creation_time DESC;
```

Replace the following:

- `REGION` : the dataset region that contains your table, for example, us.
- `PROJECT_ID` : the ID of the project that contains your table.
- `DATASET_ID` : the name of the dataset that contains your table.
- `TABLE` : the name of the table that contains the AI index.

## Delete an AI index

When you delete an indexed table, its AI index is also deleted. To delete an AI index without deleting the table, use the [`DROP AI INDEX`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_ai_index) DDL statement:

```
DROP AI INDEX IF EXISTS INDEX_NAME ON DATASET_NAME.TABLE_NAME;
```

Replace the following:

- `INDEX_NAME` : the name of the AI index that you're deleting.
- `DATASET_NAME` : the name of the dataset that contains the table.
- `TABLE_NAME` : the name of the table that contains the AI index.

## What's next

- Learn more about the [`AI.SEARCH` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-search) .
- Learn about [embeddings in BigQuery](https://docs.cloud.google.com/bigquery/docs/vector-search-intro) .
