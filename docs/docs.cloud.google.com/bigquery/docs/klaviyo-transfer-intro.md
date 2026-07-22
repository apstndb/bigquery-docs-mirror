---
name: documents/docs.cloud.google.com/bigquery/docs/klaviyo-transfer-intro
uri: https://docs.cloud.google.com/bigquery/docs/klaviyo-transfer-intro
title: Introduction to Klaviyo transfers
description: Learn how to use the BigQuery Data Transfer Service Klaviyo connector to ingest data from Klaviyo into BigQuery.
data_source: docs.cloud.google.com
---

# Introduction to Klaviyo transfers

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

> **Note:** To get support or provide feedback for this feature, contact <dts-preview-support@google.com> .

You can load data from Klaviyo to BigQuery using the [BigQuery Data Transfer Service](https://docs.cloud.google.com/bigquery/docs/dts-introduction) for Klaviyo connector. With the BigQuery Data Transfer Service, you can schedule recurring transfer jobs that add your latest data from Klaviyo to BigQuery.

To learn how to schedule a Klaviyo transfer, see [Load Klaviyo data into BigQuery](https://docs.cloud.google.com/bigquery/docs/klaviyo-transfer) .

## Limitations

Incremental Klaviyo transfers are subject to the following limitations:

  - You can only choose `TIMESTAMP` columns as watermark columns.
  - Incremental ingestion is only supported for assets with valid watermark columns.
  - Values in a watermark column must be monotonically increasing.
  - Incremental transfers cannot sync delete operations in the source table.
  - A single transfer configuration can only support either incremental or full ingestion.
  - You cannot update objects in the `asset` list after the first incremental ingestion run.
  - You cannot change the write mode in a transfer configuration after the first incremental ingestion run.
  - You cannot change the watermark column or the primary key after the first incremental ingestion run.
  - The destination BigQuery table is clustered using the provided primary key and is subject to [clustered table limitations](https://docs.cloud.google.com/bigquery/docs/clustered-tables#limitations) .
  - When you update an existing transfer configuration to the incremental ingestion mode for the first time, the first data transfer after that update transfers all available data from your data source. Any subsequent incremental data transfers will transfer only the new and updated rows from your data source.

## Data ingestion options

These sections describe the data ingestion options for setting up a Klaviyo data transfer.

### Full or incremental transfers

You specify how data loads into BigQuery by selecting the **Full** or **Incremental** write preference in the transfer configuration when you [set up a Klaviyo transfer](https://docs.cloud.google.com/bigquery/docs/klaviyo-transfer#klaviyo-transfer-setup) . Incremental transfers are supported in [preview](https://cloud.google.com/products#product-launch-stages) .

> **Note:** To request feedback or support for incremental transfers, send email to <dts-preview-support@google.com> .

You can configure a *full* data transfer to transfer all data from your Klaviyo datasets with each data transfer.

Alternatively, you can configure an *incremental* data transfer ( [Preview](https://cloud.google.com/products#product-launch-stages) ) to only transfer data that was changed since the last data transfer, instead of loading the entire dataset with each data transfer. If you select **Incremental** for your data transfer, you must specify either the **Append** or **Upsert** write modes to define how data is written to BigQuery during an incremental data transfer. The following sections describe the available write modes.

#### Append write mode

The append write mode only inserts new rows to your destination table. This option strictly appends transferred data without checking for existing records, so this mode can potentially cause data duplication in the destination table.

When you select the append mode, you must select a watermark column. A watermark column is required for the Klaviyo connector to track changes in the source table.

For Klaviyo transfers, we recommend selecting a column that is only updated when the record was created, and won't change with subsequent updates—for example, the `CREATED_AT` column.

#### Upsert write mode

The upsert write mode either updates a row or inserts a new row in your destination table by checking for a primary key. You can specify a primary key to let the Klaviyo connector determine what changes are needed to keep your destination table up to date with your source table. If the specified primary key is present in the destination BigQuery table during a data transfer, then the Klaviyo connector updates that row with new data from the source table. If a primary key is not present during a data transfer, then the Klaviyo connector inserts a new row.

When you select the upsert mode, you must select a watermark column and a primary key:

  - A watermark column is required for the Klaviyo connector to track changes in the source table.
      - Select a watermark column that updates every time a row is modified. We recommend columns similar to the `UPDATED_AT` or `LAST_MODIFIED` column.

<!-- end list -->

  - The primary key can be one or more columns on your table that are required for the Klaviyo connector to determine if it needs to insert or update a row.
    
    Select columns that contain non-null values that are unique across all rows of the table. We recommend columns that include system-generated identifiers, unique reference codes (for example, auto-incrementing IDs), or immutable time-based sequence IDs.
    
    To prevent potential data loss or data corruption, the primary key columns that you select must have unique values. If you have doubts about the uniqueness of your chosen primary key column, then we recommend that you use the append write mode instead.

## Data type mapping

The following table maps Klaviyo data types to the corresponding BigQuery data types:

| Klaviyo data type            | BigQuery data type |
| ---------------------------- | ------------------ |
| `String`                     | `STRING`           |
| `Text`                       | `STRING`           |
| `Integer`                    | `INTEGER`          |
| `Boolean`                    | `BOOLEAN`          |
| `Date (YYYY-MM-DD HH:MM:SS)` | `TIMESTAMP`        |
| `List`                       | `ARRAY`            |

## Pricing

There is no cost to transfer Klaviyo data into BigQuery while this feature is in [Preview](https://cloud.google.com/products#product-launch-stages) .

## What's next

  - For an overview of the BigQuery Data Transfer Service, see [What is BigQuery Data Transfer Service](https://docs.cloud.google.com/bigquery/docs/dts-introduction) .
