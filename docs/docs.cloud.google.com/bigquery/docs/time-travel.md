# Data retention with time travel and fail-safe

This document describes *time travel* and *fail-safe* data retention windows for datasets. During the time travel and fail-safe periods, data that you have changed or deleted in any table in the dataset continues to be stored in case you need to recover it.

## Time travel and data retention

You can access changed or deleted data from any point within the time travel window, which covers the past seven days by default. Time travel lets you [query data that was updated or deleted](/bigquery/docs/access-historical-data) , restore a [table](/bigquery/docs/restore-deleted-tables) or [dataset](/bigquery/docs/restore-deleted-datasets) that was deleted, restore a [table that expired](/bigquery/docs/managing-tables#updating_a_tables_expiration_time) , or [restore a table to a point in time](/bigquery/docs/access-historical-data#restore-a-table) .

You can set the duration of the time travel window, from a minimum of two days to a maximum of seven days. A longer time travel window is useful in cases where it is important to be able to recover updated or deleted data. A shorter time travel window lets you save on storage costs when using the [physical storage billing model](/bigquery/docs/datasets-intro#dataset_storage_billing_models) . These savings don't apply when using the logical storage billing model. For more information on how the storage billing model affects cost, see [Billing](#billing) . You can't set the time travel duration for less than 2 days.

## Configure the time travel window

You set the time travel window at the dataset or project level. These settings then apply to all tables associated with the dataset or project.

### Set the project-level time travel window

To specify the project-level default time travel window, you can use data definition language (DDL) statements. To learn how to set the project-level time travel window, see [Manage configuration settings](/bigquery/docs/default-configuration) .

### Set the dataset-level time travel window

To specify or modify the time travel window for a dataset, you can use the Google Cloud console, the bq command-line tool, or the BigQuery API.

  - To specify the default time travel window for new datasets, see [Create datasets](/bigquery/docs/datasets#create-dataset) .
  - To modify or update the time travel window for an existing dataset, see [Update time travel windows](/bigquery/docs/updating-datasets#update_time_travel_windows) .

When modifying a time travel window, if the timestamp specifies a time outside the time travel window, or from before the table was created, then the query fails and returns an error like the following:

``` text
Table ID was created at time which is
before its allowed time travel interval timestamp. Creation
time: timestamp
```

## How time travel works

BigQuery uses a columnar storage format. This means that data is organized and stored by column rather than by row. When you have a table with multiple columns, the values for each column across all rows are stored together in storage blocks.

When you modify a cell in a BigQuery table, you are changing a specific value within a particular row and a specific column. Because BigQuery stores columns together, modifying even a single cell within a column typically requires reading the entire storage block containing that column's data for the affected rows, applying the change, and then writing a new version of that storage block.

The time travel feature works by tracking the versions of storage blocks that make up your table. When you update data, BigQuery doesn't just modify the existing storage block in place. Instead, it creates a new version of the affected storage blocks with the updated data. The previous version is then retained for time travel purposes.

BigQuery uses adaptive file sizes and storage blocks. The size of storage blocks is not fixed but can vary depending on factors like the size of the table and its data distribution. Changing even one cell in a storage block changes the data for that column, potentially affecting many rows. Therefore, the unit of data that is versioned and sent to time travel is often the entire storage block that contains the modified data of that column, not just a single cell.

For this reason, changing one cell can result in more data being sent to time travel than just the size of the change.

### How the time travel window affects table and dataset recovery

A deleted table or dataset uses the time travel window duration that was in effect at the time of deletion.

For example, if you have a time travel window duration of two days and then increase the duration to seven days, tables deleted before that change are still only recoverable for two days. Similarly, if you have a time travel window duration of five days and you reduce that duration to three days, any tables that were deleted before the change are still recoverable for five days.

Because time travel windows are set at the dataset level, you can't change the time travel window of a deleted dataset until it is undeleted.

If you reduce the time travel window duration, delete a table, and then realize that you need a longer period of recoverability for that data, you can create a snapshot of the table from a point in time prior to the table deletion. You must do this while the deleted table is still recoverable. For more information, see [Create a table snapshot using time travel](/bigquery/docs/table-snapshots-create#create_a_table_snapshot_using_time_travel) .

### Time travel and row-level access

If a table has, or has had, [row-level access policies](/bigquery/docs/row-level-security-intro) , then only a table administrator can access historical data for the table.

The following [Identity and Access Management (IAM)](/bigquery/docs/access-control) permission is required:

<table>
<thead>
<tr class="header">
<th><strong>Permission</strong></th>
<th><strong>Resource</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="/bigquery/docs/access-control#bigquery.rowAccessPolicies.overrideTimeTravelRestrictions"><code dir="ltr" translate="no">        bigquery.rowAccessPolicies.overrideTimeTravelRestrictions       </code></a></td>
<td>The table whose historical data is being accessed</td>
</tr>
</tbody>
</table>

The following BigQuery role provides the required permission:

<table>
<colgroup>
<col style="width: 62%" />
<col style="width: 38%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Role</strong></th>
<th><strong>Resource</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="/bigquery/docs/access-control#bigquery.admin"><code dir="ltr" translate="no">        roles/bigquery.admin       </code></a></td>
<td>The table whose historical data is being accessed</td>
</tr>
</tbody>
</table>

The `  bigquery.rowAccessPolicies.overrideTimeTravelRestrictions  ` permission can't be added to a [custom role](/iam/docs/creating-custom-roles) .

**Note:** The **`  roles/owner  `** role does not contain all the permissions present in the **`  roles/bigquery.admin  `** role, so you must grant the **`  roles/bigquery.admin  `** role to any user who restores tables that have or had row-level access policies applied to them.

  - Run the following command to get the equivalent Unix epoch time by passing the UTC timestamp:
    
    ``` text
    date -d '2023-08-04 16:00:34.456789Z' +%s000
    ```

  - Replace the UNIX epoch time `  1691164834000  ` received from the previous command in the bq command-line tool. Run the following command to restore a copy of the deleted table `  deletedTableID  ` in another table `  restoredTable  ` , within the same dataset `  myDatasetID  ` :
    
    ``` text
    bq cp myProjectID:myDatasetID.deletedTableID@1691164834000 myProjectID:myDatasetID.restoredTable
    ```

## Fail-safe

BigQuery provides a fail-safe period. During the fail-safe period, deleted data is automatically retained for an additional seven days after the time travel window, so that the data is available for emergency recovery. Data is recoverable at the table level. Data is recovered for a table from the point in time represented by the timestamp of when that table was deleted. The fail-safe period is not configurable and can't be extended.

When you perform the following operations, the data that is replaced or removed can be recovered through the time travel window. After the time travel window ends, this data then enters the fail-safe period for extended recovery time:

  - **Table deletion or replacement:** When a table is deleted, or when its data is fully replaced (for example, by using the [`  WRITE_TRUNCATE  `](/bigquery/docs/reference/auditlogs/rest/Shared.Types/BigQueryAuditMetadata.WriteDisposition) write disposition in a load job or by using the [`  CREATE OR REPLACE TABLE  `](/bigquery/docs/reference/standard-sql/data-definition-language#create_table_statement) statement), the previous contents of the table are retained.
  - **Partition deletion:** If a specific partition is deleted from a [partitioned table](/bigquery/docs/partitioned-tables) , the data belonging to that specific partition is retained. Other partitions in the table aren't affected.

You can't query or directly recover data in fail-safe storage. To recover data from fail-safe storage, contact [Cloud Customer Care](https://cloud.google.com/support-hub) .

**Warning:** Once the fail-safe period has passed, Cloud Customer Care can't recover any of your deleted data.

## Billing

If you set your [storage billing model](/bigquery/docs/datasets-intro#dataset_storage_billing_models) to use physical bytes, you are billed separately for the bytes used for time travel and fail-safe storage. Time travel and fail-safe storage are charged at the active physical storage rate. You can [configure the time travel window](#configure_the_time_travel_window) to balance storage costs with your data retention needs.

If you set your storage billing model to use logical bytes, the total storage costs for time travel and fail-safe storage are included in the base rate that you are charged.

The following table show a comparison of physical and logical storage costs:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Billing model</strong></th>
<th><strong>What do you pay for?</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Physical (compressed) storage</td>
<td><ul>
<li>You pay for active bytes</li>
<li>You pay for long-term storage</li>
<li>You pay for time travel storage</li>
<li>You pay for fail-safe storage</li>
</ul></td>
</tr>
<tr class="even">
<td>Logical (uncompressed) storage (default setting)</td>
<td><ul>
<li>You pay for active storage</li>
<li>You pay for long-term storage</li>
<li>You don't pay for time travel storage</li>
<li>You don't pay for fail-safe storage</li>
</ul></td>
</tr>
</tbody>
</table>

If you use physical storage, you can see the bytes used by time travel and fail-safe by looking at the `  TIME_TRAVEL_PHYSICAL_BYTES  ` and `  FAIL_SAFE_PHYSICAL_BYTES  ` columns in the [`  TABLE_STORAGE  `](/bigquery/docs/information-schema-table-storage) and [`  TABLE_STORAGE_BY_ORGANIZATION  `](/bigquery/docs/information-schema-table-storage-by-organization) views. For an example of how to use one of these views to estimate your costs, see [Forecast storage billing](/bigquery/docs/information-schema-table-storage#forecast_storage_billing) .

[Storage costs](https://cloud.google.com/bigquery/pricing#storage) apply for time travel and fail-safe data, but you are only billed if data storage fees don't apply elsewhere in BigQuery. The following details apply:

  - When a table is created, there is no time travel or fail-safe storage cost.
  - If data is changed or deleted, then you are charged for the storage of the changed or deleted data saved by time travel during the time travel window and the fail-safe period. This is similar to the storage pricing for table snapshots and clones.
  - Temporary tables aren't billed for fail-safe storage.

## Data retention example

The following table shows how deleted or changed data moves between storage retention windows. This example shows a situation where the total active storage is 200 GiB and 50 GiB is deleted with a time travel window of seven days:

<table>
<thead>
<tr class="header">
<th></th>
<th>Day 0</th>
<th>Day 1</th>
<th>Day 2</th>
<th>Day 3</th>
<th>Day 4</th>
<th>Day 5</th>
<th>Day 6</th>
<th>Day 7</th>
<th>Day 8</th>
<th>Day 9</th>
<th>Day 10</th>
<th>Day 11</th>
<th>Day 12</th>
<th>Day 13</th>
<th>Day 14</th>
<th>Day 15</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Active storage</td>
<td>200</td>
<td>150</td>
<td>150</td>
<td>150</td>
<td>150</td>
<td>150</td>
<td>150</td>
<td>150</td>
<td>150</td>
<td>150</td>
<td>150</td>
<td>150</td>
<td>150</td>
<td>150</td>
<td>150</td>
<td>150</td>
</tr>
<tr class="even">
<td>Time travel storage</td>
<td></td>
<td>50</td>
<td>50</td>
<td>50</td>
<td>50</td>
<td>50</td>
<td>50</td>
<td>50</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Fail-safe storage</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td>50</td>
<td>50</td>
<td>50</td>
<td>50</td>
<td>50</td>
<td>50</td>
<td>50</td>
<td></td>
</tr>
</tbody>
</table>

Deleting data from long-term physical storage works in the same way.

## Limitations

Data retrieval with time travel is subject to the following limitations:

  - Time travel only provides access to historical data for the duration of the time travel window. To preserve table data for non-emergency purposes for longer than the time travel window, use [table snapshots](/bigquery/docs/table-snapshots-intro) .
  - If a table has, or has previously had, row-level access policies, then time travel can only be used by table administrators. For more information, see [Time travel and row-level access](#time_travel_and_row-level_access) .
  - Time travel does not restore table metadata.
  - Time travel is not supported in the following table types:
      - [External tables](/bigquery/docs/external-tables) . However, for Apache Iceberg external tables, you can use the [`  FOR SYSTEM_TIME AS OF  ` clause](/bigquery/docs/access-historical-data#query_data_at_a_point_in_time) to access snapshots that are retained in your Iceberg metadata.
      - [Temporary cached query result tables](/bigquery/docs/cached-results) .
      - [Temporary session tables](/bigquery/docs/sessions-intro) .
      - [Temporary multi-statement tables](/bigquery/docs/multi-statement-queries) .
      - Tables listed under external datasets.

## What's next

  - Learn how to [query and recover time travel data](/bigquery/docs/access-historical-data) .
  - Learn more about [table snapshots](/bigquery/docs/table-snapshots-intro) .
