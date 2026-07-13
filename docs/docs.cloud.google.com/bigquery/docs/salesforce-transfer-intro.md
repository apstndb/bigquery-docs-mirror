---
name: documents/docs.cloud.google.com/bigquery/docs/salesforce-transfer-intro
uri: https://docs.cloud.google.com/bigquery/docs/salesforce-transfer-intro
title: Introduction to Salesforce transfers
description: Learn how to use the BigQuery Data Transfer Service Salesforce connector to ingest data from Salesforce into BigQuery.
data_source: docs.cloud.google.com
---

# Introduction to Salesforce transfers

You can load data from your Salesforce Sales Cloud to BigQuery using the [BigQuery Data Transfer Service](https://docs.cloud.google.com/bigquery/docs/dts-introduction) for Salesforce connector. With BigQuery Data Transfer Service, you can schedule recurring transfer jobs that add your latest data from your Salesforce Sales Cloud to BigQuery.

To learn how to schedule a Salesforce transfer, see [Load Salesforce data into BigQuery](https://docs.cloud.google.com/bigquery/docs/salesforce-transfer) .

## Data ingestion options

The following sections provide more information on the data ingestion options when you set up a Salesforce data transfer.

### Full or incremental transfers

You can specify how data is loaded into BigQuery by selecting either the **Full** or **Incremental** write preference in the transfer configuration when you [set up a Salesforce transfer](https://docs.cloud.google.com/bigquery/docs/salesforce-transfer#sf-transfer-setup) .

You can configure a *full* data transfer to transfer all data from your Salesforce datasets with each data transfer.

Alternatively, you can configure an *incremental* data transfer to only transfer data that was changed since the last data transfer, instead of loading the entire dataset with each data transfer. If you select **Incremental** for your data transfer, you must specify either the **Append** or **Upsert** write modes to define how data is written to BigQuery during an incremental data transfer. The following sections describe the available write modes.

#### Append write mode

The append write mode only inserts new rows to your destination table. This option strictly appends transferred data without checking for existing records, so this mode can potentially cause data duplication in the destination table.

When you select the append mode, you must select a watermark column. A watermark column is required for the Salesforce connector to track changes in the source table.

Select a watermark column that is only updated when the record was created, and won't change with subsequent updates. For example, the `CreatedDate` column.

#### Upsert write mode

The upsert write mode either updates a row or inserts a new row in your destination table by checking for a primary key. You can specify a primary key to let the Salesforce connector determine what changes are needed to keep your destination table up to date with your source table. If the specified primary key is present in the destination BigQuery table during a data transfer, then the Salesforce connector updates that row with new data from the source table. If a primary key is not present during a data transfer, then the Salesforce connector inserts a new row.

When you select the upsert mode, you must select a watermark column and a primary key:

  - A watermark column is required for the Salesforce connector to track changes in the source table.
    
    Select a watermark column that updates every time a row is modified. We recommend using the `SystemModstamp` or `LastModifiedDate` column.

<!-- end list -->

  - The primary key can be one or more columns on your table that are required for the Salesforce connector to determine if it needs to insert or update a row.
    
    Select columns that contain non-null values that are unique across all rows of the table. We recommend columns that include system-generated identifiers, unique reference codes (for example, auto-incrementing IDs), or immutable time-based sequence IDs.
    
    To prevent potential data loss or data corruption, the primary key columns that you select must have unique values. If you have doubts about the uniqueness of your chosen primary key column, then we recommend that you use the append write mode instead.

### Incremental ingestion behavior

When you make changes to the table schema in your data source, incremental data transfers from those tables are reflected in BigQuery in the following ways:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Changes to data source</th>
<th>Incremental ingestion behavior</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Adding a new column</td>
<td>A new column is added to the destination BigQuery table. Any previous records for this column will have null values.</td>
</tr>
<tr class="even">
<td>Deleting a column</td>
<td>The deleted column remains in the destination BigQuery table. New entries to this deleted column are populated with null values.</td>
</tr>
<tr class="odd">
<td>Changing the data type in a column</td>
<td>The connector only supports <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#alter_column_set_data_type_statement">data type conversions that are supported by the <code dir="ltr" translate="no">ALTER COLUMN</code> DDL statement</a> . Any other data type conversion causes the data transfer to fail.
<p>If you encounter any issues, we recommend creating a new transfer configuration.</p></td>
</tr>
<tr class="even">
<td>Renaming a column</td>
<td>The original column remains in the destination BigQuery table as is, while a new column is added to the destination table with the updated name.</td>
</tr>
</tbody>
</table>

## Data type mapping

The following table maps Salesforce data types to the corresponding BigQuery data types:

| Salesforce data type         | BigQuery data type |
| ---------------------------- | ------------------ |
| `_bool`                      | `BOOLEAN`          |
| `_int`                       | `INTEGER`          |
| `_long`                      | `INTEGER`          |
| `_double`                    | `FLOAT`            |
| `currency`                   | `FLOAT`            |
| `percent`                    | `FLOAT`            |
| `geolocation (latitude)`     | `FLOAT`            |
| `geolocation (longitude)`    | `FLOAT`            |
| `date`                       | `DATE`             |
| `datetime`                   | `TIMESTAMP`        |
| `time`                       | `TIME`             |
| `picklist`                   | `STRING`           |
| `multipicklist`              | `STRING`           |
| `combobox`                   | `STRING`           |
| `reference`                  | `STRING`           |
| `base64`                     | `STRING`           |
| `textarea`                   | `STRING`           |
| `phone`                      | `STRING`           |
| `id`                         | `STRING`           |
| `url`                        | `STRING`           |
| `email`                      | `STRING`           |
| `encryptedstring`            | `STRING`           |
| `datacategorygroupreference` | `STRING`           |
| `location`                   | `STRING`           |
| `address`                    | `STRING`           |
| `anyType`                    | `STRING`           |

## Pricing

For pricing information about Salesforce transfers, see [Data Transfer Service pricing](https://docs.cloud.google.com/bigquery/pricing#data-transfer-service-pricing) .

## What's next

  - Learn about [scheduling a Salesforce transfer](https://docs.cloud.google.com/bigquery/docs/salesforce-transfer) .
  - Learn more about the [BigQuery Data Transfer Service](https://docs.cloud.google.com/bigquery/docs/dts-introduction) .
