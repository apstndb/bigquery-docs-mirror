---
name: documents/docs.cloud.google.com/bigquery/docs/information-schema-ai-index-columns
uri: https://docs.cloud.google.com/bigquery/docs/information-schema-ai-index-columns
title: AI_INDEX_COLUMNS view
description: Learn about the INFORMATION_SCHEMA.AI_INDEX_COLUMNS view.
data_source: docs.cloud.google.com
---

# AI_INDEX_COLUMNS view

> **Preview**
>
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

The `INFORMATION_SCHEMA.AI_INDEX_COLUMNS` view contains one row for each AI-indexed column on each table in a dataset.

## Required permissions

To view AI index metadata, you need the `bigquery.tables.get` or `bigquery.tables.list` Identity and Access Management (IAM) permission on the table with the index. Each of the following predefined IAM roles includes at least one of these permissions:

- `roles/bigquery.admin`
- `roles/bigquery.dataEditor`
- `roles/bigquery.dataOwner`
- `roles/bigquery.dataViewer`
- `roles/bigquery.metadataViewer`
- `roles/bigquery.user`

For more information about BigQuery permissions, see [Access control with IAM](https://docs.cloud.google.com/bigquery/docs/access-control) .

## Schema

When you query the `INFORMATION_SCHEMA.AI_INDEX_COLUMNS` view, the query results contain one row for each indexed column on each table in a dataset.

The `INFORMATION_SCHEMA.AI_INDEX_COLUMNS` view has the following schema:

| Column name         | Data type | Value                                                                                                                          |
|---------------------|-----------|--------------------------------------------------------------------------------------------------------------------------------|
| `index_catalog`     | `STRING`  | The name of the project that contains the dataset.                                                                             |
| `index_schema`      | `STRING`  | The name of the dataset that contains the AI index.                                                                            |
| `table_name`        | `STRING`  | The name of the table that the AI index is created on.                                                                         |
| `index_name`        | `STRING`  | The name of the AI index.                                                                                                      |
| `index_column_name` | `STRING`  | The name of an AI-indexed column. For AI indexes created with `AUTO COLUMNS` , this view lists every column that was selected. |

## Scope and syntax

Queries against this view must have a [dataset qualifier](https://docs.cloud.google.com/bigquery/docs/information-schema-intro#syntax) . The following table explains the region scope for this view:

| View Name                                                                     | Resource scope | Region scope     |
|-------------------------------------------------------------------------------|----------------|------------------|
| `[ `` PROJECT_ID `` .] `` DATASET_ID `` .INFORMATION_SCHEMA.AI_INDEX_COLUMNS` | Dataset level  | Dataset location |

Replace the following:

- `PROJECT_ID` : the ID of your Google Cloud project.
- `DATASET_ID` : the ID of your dataset.

## Example

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
