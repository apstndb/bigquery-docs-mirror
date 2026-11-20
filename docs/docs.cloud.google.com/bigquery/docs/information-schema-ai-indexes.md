---
name: documents/docs.cloud.google.com/bigquery/docs/information-schema-ai-indexes
uri: https://docs.cloud.google.com/bigquery/docs/information-schema-ai-indexes
title: AI_INDEXES view
description: Learn about the INFORMATION_SCHEMA.AI_INDEXES view.
data_source: docs.cloud.google.com
---

# AI_INDEXES view

> **Preview**
>
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

The `INFORMATION_SCHEMA.AI_INDEXES` view contains one row for each AI index in a dataset.

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

When you query the INFORMATION_SCHEMA.AI_INDEXES view, the query results contain one row for each AI index in a dataset.

The `INFORMATION_SCHEMA.AI_INDEXES` view has the following schema:

| Column name              | Data type   | Value                                                                                         |
|--------------------------|-------------|-----------------------------------------------------------------------------------------------|
| `index_catalog`          | `STRING`    | The name of the project that contains the dataset.                                            |
| `index_schema`           | `STRING`    | The name of the dataset that contains the AI index.                                           |
| `table_name`             | `STRING`    | The name of the table that the AI index is created on.                                        |
| `index_name`             | `STRING`    | The name of the AI index.                                                                     |
| `index_status`           | `RECORD`    | The status of the AI index, containing `index_state` ( `STRING` ) and `message` ( `STRING` ). |
| `creation_time`          | `TIMESTAMP` | The time when the AI index was created.                                                       |
| `last_modification_time` | `TIMESTAMP` | The last time the AI index configuration was modified.                                        |
| `disable_time`           | `TIMESTAMP` | The time when the AI index was disabled, or NULL if the index isn't disabled.                 |
| `ddl`                    | `STRING`    | The DDL statement used to create the AI index.                                                |
| `coverage_percentage`    | `INTEGER`   | The approximate percentage of table rows that are indexed by the AI index.                    |
| `unindexed_row_count`    | `INTEGER`   | The number of rows in the table that aren't indexed by the AI index yet.                      |
| `total_logical_bytes`    | `INTEGER`   | The total billable logical bytes used by the AI index.                                        |

## Scope and syntax

Queries against this view must have a [dataset qualifier](https://docs.cloud.google.com/bigquery/docs/information-schema-intro#syntax) . The following table explains the region scope for this view:

| View Name                                                               | Resource scope | Region scope     |
|-------------------------------------------------------------------------|----------------|------------------|
| `[ `` PROJECT_ID `` .] `` DATASET_ID `` .INFORMATION_SCHEMA.AI_INDEXES` | Dataset level  | Dataset location |

Replace the following:

- `PROJECT_ID` : the ID of your Google Cloud project.
- `DATASET_ID` : the ID of your dataset.

## Example

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
