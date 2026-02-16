# Restore table snapshots

This document describes how to create a writeable table from a table snapshot by using the Google Cloud console, a `  CREATE TABLE CLONE  ` query, a `  bq cp  ` command, or the `  jobs.insert  ` API. It is intended for users who are familiar with [table snapshots](/bigquery/docs/table-snapshots-intro) .

## Permissions and roles

This section describes the [Identity and Access Management (IAM) permissions](/bigquery/docs/access-control#bq-permissions) that you need to create a writeable table from a table snapshot, and the [predefined IAM roles](/bigquery/docs/access-control#bigquery) that grant those permissions.

### Permissions

To create a writeable table from a table snapshot, you need the following permissions:

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
<td>All of the following:<br />
<br />
<code dir="ltr" translate="no">       bigquery.tables.get      </code><br />
<code dir="ltr" translate="no">       bigquery.tables.getData      </code><br />
<code dir="ltr" translate="no">       bigquery.tables.restoreSnapshot      </code><br />
</td>
<td>The table snapshot that you want to copy into a writeable table.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigquery.tables.create      </code></td>
<td>The dataset that contains the destination table.</td>
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
<code dir="ltr" translate="no">       bigquery.dataEditor      </code><br />
<code dir="ltr" translate="no">       bigquery.dataOwner      </code><br />
<code dir="ltr" translate="no">       bigquery.admin      </code></td>
<td>The table snapshot that you want to copy into a writeable table.</td>
</tr>
<tr class="even">
<td>Any of the following:<br />
<br />
<code dir="ltr" translate="no">       bigquery.dataEditor      </code><br />
<code dir="ltr" translate="no">       bigquery.dataOwner      </code><br />
<code dir="ltr" translate="no">       bigquery.admin      </code></td>
<td>The dataset that contains the destination table.</td>
</tr>
</tbody>
</table>

## Restore a table snapshot

To create a writeable table from a snapshot, specify the table snapshot that you want to copy and the destination table. The destination table can be a new table, or you can overwrite an existing table with the table snapshot.

### Restore to a new table

You can restore a table snapshot into a new table by using one of the following options:

### Console

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :
    
    If you don't see the left pane, click last\_page **Expand left pane** to open the pane.

3.  In the **Explorer** pane, expand the project, click **Datasets** , and then click the dataset that contains the table snapshot that you want to restore from.

4.  Click **Overview \> Tables** , and then click the name of the table snapshot.

5.  In the table snapshot pane that appears, click update **Restore** .

6.  In the **Restore snapshot** pane that appears, enter the **Project** , **Dataset** , and **Table** information for the new table.

7.  Click **Save** .

### SQL

Use the [`  CREATE TABLE CLONE  ` DDL statement](/bigquery/docs/reference/standard-sql/data-definition-language#create_table_clone_statement) :

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
    CREATE TABLE TABLE_PROJECT_ID.TABLE_DATASET_NAME.NEW_TABLE_NAME
    CLONE SNAPSHOT_PROJECT_ID.SNAPSHOT_DATASET_NAME.SNAPSHOT_NAME;
    ```
    
    Replace the following:
    
      - `  TABLE_PROJECT_ID  ` : the project ID of the project in which to create the new table.
      - `  TABLE_DATASET_NAME  ` : the name of the dataset in which to create the new table.
      - `  NEW_TABLE_NAME  ` : the name of the new table.
      - `  SNAPSHOT_PROJECT_ID  ` : the project ID of the project that contains the snapshot you are restoring from.
      - `  SNAPSHOT_DATASET_NAME  ` : the name of the dataset that contains the snapshot you are restoring from.
      - `  SNAPSHOT_NAME  ` : the name of the snapshot you are restoring from.

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](/bigquery/docs/running-queries#queries) .

### bq

Enter the following command in the Cloud Shell:

``` text
bq cp \
--restore \
--no_clobber \
SNAPSHOT_PROJECT_ID:SNAPSHOT_DATASET_NAME.SNAPSHOT_NAME \
TABLE_PROJECT_ID:TABLE_DATASET_NAME.NEW_TABLE_NAME
```

Replace the following:

  - `  SNAPSHOT_PROJECT_ID  ` : the project ID of the project that contains the snapshot you are restoring from.
  - `  SNAPSHOT_DATASET_NAME  ` : the name of the dataset that contains the snapshot you are restoring from.
  - `  SNAPSHOT_NAME  ` : the name of the snapshot you are restoring from.
  - `  TABLE_PROJECT_ID  ` : the project ID of the project in which to create the new table.
  - `  TABLE_DATASET_NAME  ` : the name of the dataset in which to create the new table.
  - `  NEW_TABLE_NAME  ` : the name of the new table.

The `  --no_clobber  ` flag instructs the command to fail if the destination table already exists.

### API

Call the [`  jobs.insert  `](/bigquery/docs/reference/rest/v2/jobs/insert) method with the following parameters:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Parameter</strong></th>
<th><strong>Value</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         projectId        </code></td>
<td>The project ID of the project to bill for this operation.</td>
</tr>
<tr class="even">
<td>Request body</td>
<td><pre class="text" dir="ltr" data-is-upgraded="" data-syntax="JSON"><code>{
  &quot;configuration&quot;: {
    &quot;copy&quot;: {
      &quot;sourceTables&quot;: [
        {
          &quot;projectId&quot;: &quot;SNAPSHOT_PROJECT_ID&quot;,
          &quot;datasetId&quot;: &quot;SNAPSHOT_DATASET_NAME&quot;,
          &quot;tableId&quot;: &quot;SNAPSHOT_NAME&quot;
        }
      ],
      &quot;destinationTable&quot;: {
        &quot;projectId&quot;: &quot;TABLE_PROJECT_ID&quot;,
        &quot;datasetId&quot;: &quot;TABLE_DATASET_NAME&quot;,
        &quot;tableId&quot;: &quot;NEW_TABLE_NAME&quot;
      },
      &quot;operationType&quot;: &quot;RESTORE&quot;,
      &quot;writeDisposition&quot;: &quot;WRITE_EMPTY&quot;
    }
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Replace the following:

  - `  SNAPSHOT_PROJECT_ID  ` : the project ID of the project that contains the snapshot you are restoring from.
  - `  SNAPSHOT_DATASET_NAME  ` : the name of the dataset that contains the snapshot you are restoring from.
  - `  SNAPSHOT_NAME  ` : the name of the snapshot you are restoring from.
  - `  TABLE_PROJECT_ID  ` : the project ID of the project in which to create the new table.
  - `  TABLE_DATASET_NAME  ` : the name of the dataset in which to create the new table.
  - `  NEW_TABLE_NAME  ` : the name of the new table.

If an expiration is not specified, then the destination table expires after the default table expiration time for the dataset that contains the destination table.

### Overwrite an existing table

You can overwrite an existing table with a table snapshot by using one of the following options:

### Console

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :

3.  In the **Explorer** pane, expand the project, click **Datasets** , and then click the dataset that contains the table snapshot that you want to restore from.

4.  Click **Overview \> Tables** , and then click the name of the table snapshot.

5.  In the table snapshot pane that appears, click **Restore** .

6.  In the **Restore snapshot** pane that appears, enter the **Project** , **Dataset** , and **Table** information for the existing table.

7.  Select **Overwrite table if it exists** .

8.  Click **Save** .

### SQL

Use the [`  CREATE TABLE CLONE  ` DDL statement](/bigquery/docs/reference/standard-sql/data-definition-language#create_table_clone_statement) :

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
    CREATE OR REPLACE TABLE TABLE_PROJECT_ID.TABLE_DATASET_NAME.TABLE_NAME
    CLONE SNAPSHOT_PROJECT_ID.SNAPSHOT_DATASET_NAME.SNAPSHOT_NAME;
    ```
    
    Replace the following:
    
      - `  TABLE_PROJECT_ID  ` : the project ID of the project in which to create the new table.
      - `  TABLE_DATASET_NAME  ` : the name of the dataset that contains the table you are overwriting.
      - `  TABLE_NAME  ` : the name of the table you are overwriting.
      - `  SNAPSHOT_PROJECT_ID  ` : the project ID of the project that contains the snapshot you are restoring from.
      - `  SNAPSHOT_DATASET_NAME  ` : the name of the dataset that contains the snapshot you are restoring from.
      - `  SNAPSHOT_NAME  ` : the name of the snapshot you are restoring from.

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](/bigquery/docs/running-queries#queries) .

### bq

Enter the following command in the Cloud Shell:

``` text
bq cp \
--restore \
--force \
SNAPSHOT_PROJECT_ID:SNAPSHOT_DATASET_NAME.SNAPSHOT_NAME \
TABLE_PROJECT_ID:TABLE_DATASET_NAME.TABLE_NAME
```

Replace the following:

  - `  SNAPSHOT_PROJECT_ID  ` : the project ID of the project that contains the snapshot you are restoring from.
  - `  SNAPSHOT_DATASET_NAME  ` : the name of the dataset that contains the snapshot you are restoring from.
  - `  SNAPSHOT_NAME  ` : the name of the snapshot you are restoring from.
  - `  TABLE_PROJECT_ID  ` : the project ID of the project in which to create the new table.
  - `  TABLE_DATASET_NAME  ` : the name of the dataset that contains the table you are overwriting.
  - `  TABLE_NAME  ` : the name of the table you are overwriting.

### API

Call the [`  jobs.insert  `](/bigquery/docs/reference/rest/v2/jobs/insert) method with the following parameters:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Parameter</strong></th>
<th><strong>Value</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         projectId        </code></td>
<td>The project ID of the project to bill for this operation.</td>
</tr>
<tr class="even">
<td>Request body</td>
<td><pre class="text" dir="ltr" data-is-upgraded="" data-syntax="JSON"><code>{
  &quot;configuration&quot;: {
    &quot;copy&quot;: {
      &quot;sourceTables&quot;: [
        {
          &quot;projectId&quot;: &quot;SNAPSHOT_PROJECT_ID&quot;,
          &quot;datasetId&quot;: &quot;SNAPSHOT_DATASET_NAME&quot;,
          &quot;tableId&quot;: &quot;SNAPSHOT_NAME&quot;
        }
      ],
      &quot;destinationTable&quot;: {
        &quot;projectId&quot;: &quot;TABLE_PROJECT_ID&quot;,
        &quot;datasetId&quot;: &quot;TABLE_DATASET_NAME&quot;,
        &quot;tableId&quot;: &quot;TABLE_NAME&quot;
      },
      &quot;operationType&quot;: &quot;RESTORE&quot;,
      &quot;writeDisposition&quot;: &quot;WRITE_TRUNCATE&quot;
    }
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Replace the following:

  - `  SNAPSHOT_PROJECT_ID  ` : the project ID of the project that contains the snapshot you are restoring from.
  - `  SNAPSHOT_DATASET_NAME  ` : the name of the dataset that contains the snapshot you are restoring from.
  - `  SNAPSHOT_NAME  ` : the name of the snapshot you are restoring from.
  - `  TABLE_PROJECT_ID  ` : the project ID of the project in which to create the new table.
  - `  TABLE_DATASET_NAME  ` : the name of the dataset that contains the table you are overwriting.
  - `  TABLE_NAME  ` : the name of the table you are overwriting.

If an expiration is not specified, then the destination table expires after the default table expiration time for the dataset that contains the destination table.

## What's next

  - [List the table snapshots of a specified base table](/bigquery/docs/table-snapshots-list#list_the_table_snapshots_of_a_specified_base_table) .
