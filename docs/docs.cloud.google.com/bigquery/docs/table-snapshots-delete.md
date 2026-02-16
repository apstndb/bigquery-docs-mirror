# Delete table snapshots

This document describes how to delete a table snapshot by using the Google Cloud console, a [`  DROP SNAPSHOT TABLE  `](/bigquery/docs/reference/standard-sql/data-definition-language#drop_snapshot_table_statement) GoogleSQL statement, a [`  bq rm  `](/bigquery/docs/reference/bq-cli-reference#bq_rm) command, or a BigQuery API [`  tables.delete  `](/bigquery/docs/reference/rest/v2/tables/delete) call. It also provides information about how to recover a table snapshot that was deleted or that expired in the past seven days. It is intended for users who are familiar with [table snapshots](/bigquery/docs/table-snapshots-intro) .

## Permissions and roles

This section describes the [Identity and Access Management (IAM) permission](/bigquery/docs/access-control#bq-permissions) that you need to delete a table snapshot, and the [predefined IAM roles](/bigquery/docs/access-control#bigquery) that grant those permissions.

### Permissions

To delete a table snapshot, you need the following permission:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Permission</strong></th>
<th><strong>Resource</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.tables.deleteSnapshot      </code></td>
<td>The table snapshot that you want to delete</td>
</tr>
</tbody>
</table>

### Roles

The predefined BigQuery roles that provide the required permissions are as follows:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Role</strong></th>
<th><strong>Resource</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Any of the following:<br />
<br />
<code dir="ltr" translate="no">       bigquery.dataOwner      </code><br />
<code dir="ltr" translate="no">       bigquery.admin      </code></td>
<td>The table snapshot that you want to delete.</td>
</tr>
</tbody>
</table>

## Delete a table snapshot

Delete a table snapshot as you would delete a standard table. You don't need to delete a table snapshot that has expired.

You can delete a table snapshot by using one of the following options:

### Console

1.  In the Google Cloud console, go to the **BigQuery** page.

<!-- end list -->

1.  In the left pane, click explore **Explorer** :
    
    If you don't see the left pane, click last\_page **Expand left pane** to open the pane.

2.  In the **Explorer** pane, expand your project, click **Datasets** , and then click the dataset that has the table snapshot.

3.  Click **Overview \> Tables** , and then click the name of the table snapshot.

4.  In the details pane that appears, click **Delete** .

5.  In the dialog that appears, type `  delete  ` , and then click **Delete** again.

### SQL

Use the [`  DROP SNAPSHOT TABLE  ` DDL statement](/bigquery/docs/reference/standard-sql/data-definition-language#drop_snapshot_table_statement) :

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
    DROP SNAPSHOT TABLE PROJECT_ID.DATASET_NAME.SNAPSHOT_NAME;
    ```
    
    Replace the following:
    
      - `  PROJECT_ID  ` : the project ID of the project that contains the snapshot.
      - `  DATASET_NAME  ` : the name of the dataset that contains the snapshot.
      - `  SNAPSHOT_NAME  ` : the name of the snapshot.

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](/bigquery/docs/running-queries#queries) .

### bq

Enter the following command in the Cloud Shell:

``` text
bq rm \
PROJECT_ID:DATASET_NAME.SNAPSHOT_NAME
```

Replace the following:

  - `  PROJECT_ID  ` : the project ID of the project that contains the snapshot.
  - `  DATASET_NAME  ` : the name of the dataset that contains the snapshot.
  - `  SNAPSHOT_NAME  ` : the name of the snapshot.

### API

Call the [`  tables.delete  `](/bigquery/docs/reference/rest/v2/tables/delete) method with the following parameters:

<table>
<thead>
<tr class="header">
<th><strong>Parameter</strong></th>
<th><strong>Value</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         projectId        </code></td>
<td>The project ID of the project that contains the snapshot.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         datasetId        </code></td>
<td>The name of the dataset that contains the snapshot.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         tableId        </code></td>
<td>The name of the snapshot.</td>
</tr>
</tbody>
</table>

## Restore a deleted or expired table snapshot

You can recover a table snapshot that was deleted or that expired in the past seven days in the same way that you recover a standard table. For more information, see [Restore table snapshots](/bigquery/docs/table-snapshots-restore) .

## What's next

  - [Create monthly snapshots of a table by using a service account that runs a scheduled query](/bigquery/docs/table-snapshots-scheduled) .
