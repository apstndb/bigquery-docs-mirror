# Set up incremental transfers for Snowflake

This guide shows you how to configure incremental data transfers from Snowflake to BigQuery. Incremental transfers let you transfer only the data that has changed since the last transfer run, which can reduce transfer time and costs.

## Limitations

Incremental Snowflake transfers are subject to the following limitations:

  - You must provide primary key columns to use the upsert write mode. For more information, see [Defining primary keys for incremental transfers](https://docs.cloud.google.com/bigquery/docs/migration/snowflake-incremental#custom_schema_file) .
  - Primary keys must be unique in the source table. If duplicates exist, the results of the merge operation in BigQuery might be inconsistent and not match the source data.
  - The automatic handling of schema changes with incremental transfers is not supported. If the schema of a source table changes, you must manually update the BigQuery table schema.
  - Incremental transfers work best when changes in your source data are concentrated within a small number of partitions. Incremental transfer performance can degrade significantly if updates are scattered across the source table, as this requires scanning many partitions. If you have many rows that are changed between data transfers, then we recommend that you use a full transfer instead.
  - Some operations in Snowflake, such as `CREATE OR REPLACE TABLE` or `CLONE` , can overwrite the original table object and its associated change tracking history. This makes existing data transfers stale and requires a new full sync to resume incremental transfers.
  - Incremental transfers must be run frequently enough to stay within [Snowflake's data retention period](https://docs.snowflake.com/en/user-guide/data-time-travel#data-retention-period) for change tracking. If the last successful transfer is run outside of this window, then the next transfer will be a full transfer.

## Data ingestion behavior

You can specify how data is loaded into BigQuery by selecting either the **Full** or **Incremental** write preference in the transfer configuration when you [set up a Snowflake transfer](https://docs.cloud.google.com/bigquery/docs/migration/snowflake-transfer#set-up-transfer) .

You can configure a *full* data transfer to transfer all data from your Snowflake datasets with each data transfer.

Alternatively, you can configure an *incremental* data transfer ( [Preview](https://cloud.google.com/products#product-launch-stages) ) to only transfer data that was changed since the last data transfer, instead of loading the entire dataset with each data transfer. If you select **Incremental** for your data transfer, you must specify either the **Append** or **Upsert** write modes to define how data is written to BigQuery during an incremental data transfer. The following sections describe the available write modes.

#### Append write mode

The append write mode only inserts new rows to your destination table. This option strictly appends transferred data without checking for existing records, so this mode can potentially cause data duplication in the destination table.

When you select the append mode, you must select a watermark column. A watermark column is required for the Snowflake connector to track changes in the source table.

For Snowflake transfers, we recommend selecting a column that is only updated when the record was created, and won't change with subsequent updates. For example, the `CREATED_AT` column.

#### Upsert write mode

The upsert write mode either updates a row or inserts a new row in your destination table by checking for a primary key. You can specify a primary key to let the Snowflake connector determine what changes are needed to keep your destination table up to date with your source table. If the specified primary key is present in the destination BigQuery table during a data transfer, then the Snowflake connector updates that row with new data from the source table. If a primary key is not present during a data transfer, then the Snowflake connector inserts a new row.

When you select the upsert mode, you must select a watermark column and a primary key:

  - A watermark column is required for the Snowflake connector to track changes in the source table.
      - Select a watermark column that updates every time a row is modified. We recommend columns similar to the `UPDATED_AT` or `LAST_MODIFIED` column.

<!-- end list -->

  - The primary key can be one or more columns on your table that are required for the Snowflake connector to determine if it needs to insert or update a row.
    
    Select columns that contain non-null values that are unique across all rows of the table. We recommend columns that include system-generated identifiers, unique reference codes (for example, auto-incrementing IDs), or immutable time-based sequence IDs.
    
    To prevent potential data loss or data corruption, the primary key columns that you select must have unique values. If you have doubts about the uniqueness of your chosen primary key column, then we recommend that you use the append write mode instead.

To use the upsert write mode with your incremental data transfer, you must [define primary keys in your custom schema file](https://docs.cloud.google.com/bigquery/docs/migration/snowflake-incremental#defining_primary_keys_for_incremental_transfers) .

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
<td>The connector only supports <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#details_21">data type conversions that are supported by the <code dir="ltr" translate="no">ALTER COLUMN</code> DDL statement</a> . Any other data type conversions causes the data transfer to fail.
<p>If you encounter any issues, we recommend creating a new transfer configuration.</p></td>
</tr>
<tr class="even">
<td>Renaming a column</td>
<td>The original column remains in the destination BigQuery table as is, while a new column is added to the destination table with the updated name.</td>
</tr>
</tbody>
</table>

## Custom schema file for incremental transfers

You can use a custom schema file to define primary keys for incremental transfers and to customize schema mapping. A custom schema file is a JSON file that describes the source and target schema.

For incremental transfers in **Upsert** mode, you must identify one or more columns as primary keys. To do this, annotate the columns with the `PRIMARY_KEY` usage type in the custom schema file.

The following example shows a custom schema file that defines `O_ORDERKEY` and `O_ORDERDATE` as primary keys for the `orders` table:

    {
      "databases": [
        {
          "name": "my_db",
          "originalName": "my_db",
          "tables": [
            {
              "name": "orders",
              "originalName": "orders",
              "columns": [
                {
                  "name": "O_ORDERKEY",
                  "originalName": "O_ORDERKEY",
                  "usageType": [
                    "PRIMARY_KEY"
                  ]
                },
                {
                  "name": "O_ORDERDATE",
                  "originalName": "O_ORDERDATE",
                  "usageType": [
                    "PRIMARY_KEY"
                  ]
                }
              ]
            }
          ]
        }
      ]
    }

## Enable change tracking

Before you can set up an incremental Snowflake transfer, you must enable change tracking on each source table with the following command:

    ALTER TABLE DATABASE_NAME.SCHEMA_NAME.TABLE_NAME SET CHANGE_TRACKING = TRUE;

If change tracking is not enabled for a table, then the Snowflake connector defaults to a full data transfer for that table.

## What's next

Once you have configured all the steps required for an incremental Snowflake transfer, you can enable incremental transfers for your Snowflake transfer configuration. For more information, see [Set up a Snowflake transfer](https://docs.cloud.google.com/bigquery/docs/migration/snowflake-transfer#set-up-transfer) .
