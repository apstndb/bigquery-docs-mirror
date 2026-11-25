---
name: documents/docs.cloud.google.com/bigquery/docs/ai-index-overview
uri: https://docs.cloud.google.com/bigquery/docs/ai-index-overview
title: AI indexes overview
description: Learn about BigQuery AI indexes, a managed indexing abstraction that lets you use natural language search across columns without requiring you to manage models.
data_source: docs.cloud.google.com
---

# AI indexes overview

> **Preview**
>
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

AI indexes let you perform natural language searches across table columns without manually generating embeddings or managing models. To get started, [create an AI index](https://docs.cloud.google.com/bigquery/docs/ai-index#create-ai-index) with a single `CREATE AI INDEX` statement, then query your data with the [`AI.SEARCH`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-search) function while BigQuery automatically handles column selection, index optimization, and ongoing maintenance.

## About AI indexes

An AI index is a managed, self-optimizing indexing abstraction that lets you use natural language search across one or more columns in your BigQuery tables with the `AI.SEARCH` function. Use an AI index when you want natural-language search across one or more text columns without managing embedding models, embedding columns, or vector indexes. If you need a specific embedding model, or custom vector index options, [generate embeddings](https://docs.cloud.google.com/bigquery/docs/autonomous-embedding-generation) and [create a vector index](https://docs.cloud.google.com/bigquery/docs/vector-index) .

BigQuery AI indexes help you perform the following tasks more efficiently:

- **Perform natural language searches without managing models** : you can search across your data using natural language queries without generating embeddings or configuring vector indexes.
- **Automatic column selection** : when you create an AI index with the `AUTO COLUMNS` option, BigQuery automatically identifies and selects candidate columns in the table to index, or lets you specify an explicit list of columns to include.
- **Adaptive indexing** : BigQuery automatically determines and applies the optimal indexing and retrieval strategies for your data and queries.
- **Fully managed lifecycle** : as your table data changes, BigQuery automatically manages index creation, maintenance, updates, and refreshes, without requiring you to manage underlying AI artifacts.

## Workload management

By default, BigQuery uses on-demand slots and the shared slot pool to handle the background processing required to build, refresh, and optimize an AI index. To ensure predictable and consistent indexing performance on larger production workloads, or to create an AI index on a table with more than 1,000,000 rows, do the following:

- Create a reservation in the region where your table is located
- Assign your project to the reservation with the `job_type` set to `BACKGROUND` .

When a `BACKGROUND` reservation is present, BigQuery uses it to run the background jobs that maintain the AI index.

## Pricing

AI index costs fall into the following categories:

- **DDL statements** : there are no additional charges for running the `CREATE AI INDEX` and `DROP AI INDEX` statements.
- **Background index data processing ( `gc_` jobs)** : all data processing runs directly within BigQuery using BigQuery slots. By default, BigQuery uses on-demand slots to handle these jobs, and the table's project is billed following the DML on-demand billing model. If a `BACKGROUND` reservation is assigned to the project, BigQuery uses the `BACKGROUND` reservation to run these background DML jobs, and the reservation is billed for the slot time usage. To learn more, see [Track background job costs](https://docs.cloud.google.com/bigquery/docs/ai-index#track-background-job-costs) .
- **Embedding generation** : embedding generation for AI indexes, including the embeddings generated for `AI.SEARCH` queries on tables with an AI index, is billed at the published rate of the underlying model that the AI index uses. Google might update the default model used by AI indexes over time for model lifecycle or performance improvements, and bill at the published [BigQuery pricing](https://cloud.google.com/bigquery/pricing) for the model.
- **Index training and optimization** : there are no additional charges for the processing required to train and optimize the index structures when you use the default shared slot pool, as long as the total size of the indexed table data is below your organizational limit.
- **Storage** : AI indexes incur storage costs while they exist on the table. You can view the storage size of an AI index in the `total_logical_bytes` column of the `INFORMATION_SCHEMA.AI_INDEXES` view.
- **Queries** : queries that use the `AI.SEARCH` function are billed at standard BigQuery compute pricing. Embedding generation for the query is billed as described previously in this list.

## Limitations on AI indexes

When you use AI indexes, the following limitations apply:

- If the combined text of a row's indexed columns is very long, such as full documents or many long `STRING` columns, only part of the text is used for search. To ensure the most informative fields are used, specify an explicit column list in `CREATE AI INDEX` with the highest-signal columns listed first.

- Queries that require exact matching on identifier values with no natural language meaning, such as IDs, UUIDs, hashes, or system codes, aren't supported. By default, `AUTO COLUMNS` includes all top-level STRING columns without filtering out opaque ID columns. To exclude opaque ID columns from the AI index, specify an explicit column list in `CREATE AI INDEX` .

- Queries that contain strict numeric constraints or require structured filtering on non- `STRING` columns aren't supported by natural-language search text alone. Apply structured or numeric filters using a `WHERE` clause in a pre-filter subquery instead.

- Search quality might degrade if the AI index includes columns with text that doesn't describe the row, such as raw logs, stack traces, URLs, or machine-generated strings. To exclude these columns, list the columns to index instead of using `AUTO COLUMNS` .

- `CREATE OR REPLACE AI INDEX` and `ALTER AI INDEX` statements aren't supported. You also can't drop, rename, or change the data type of a source column included in an AI index. To change indexed columns, drop the AI index and create it again.

- The following table operations aren't supported on tables with AI indexes. To perform these operations, drop the AI index.

  - Create a table from the table's schema ( `CREATE TABLE ... LIKE` ).
  - Copy the table ( `bq cp` or `CREATE TABLE ... COPY` ), including cross-region copies, or copying data into an existing table that has an AI index.
  - Clone the table ( `CREATE TABLE ... CLONE` ).
  - Create a table snapshot ( `CREATE SNAPSHOT TABLE` ).
  - Rename the table ( `ALTER TABLE ... RENAME TO` ).
  - Restore the table ( `RESTORE TABLE` ).

## What's next

- Learn how to [use AI indexes](https://docs.cloud.google.com/bigquery/docs/ai-index) .
- Learn how to search tables using the [`AI.SEARCH` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-search) .
