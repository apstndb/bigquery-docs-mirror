# Create table clones

This document describes how to copy a table to a [table clone](/bigquery/docs/table-clones-intro) by using a [`  CREATE TABLE CLONE  `](/bigquery/docs/reference/standard-sql/data-definition-language#create_table_clone_statement) SQL statement, a [`  bq cp  `](/bigquery/docs/reference/bq-cli-reference#bq_cp) command, or a [`  jobs.insert  `](/bigquery/docs/reference/rest/v2/jobs/insert) API call. This document is intended for users who are familiar with [table clones](/bigquery/docs/table-clones-intro) .

## Permissions and roles

This section describes the [Identity and Access Management (IAM) permissions](/bigquery/docs/access-control#bq-permissions) that you need to create a table clone, and the [predefined IAM roles](/bigquery/docs/access-control#bigquery) that grant those permissions.

### Permissions

To create a table clone, you need the following permissions:

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
</td>
<td>The table that you want to make a clone of.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigquery.tables.create      </code><br />
<code dir="ltr" translate="no">       bigquery.tables.updateData      </code></td>
<td>The dataset that contains the table clone.</td>
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
<code dir="ltr" translate="no">       bigquery.dataViewer      </code><br />
<code dir="ltr" translate="no">       bigquery.dataEditor      </code><br />
<code dir="ltr" translate="no">       bigquery.dataOwner      </code><br />
<code dir="ltr" translate="no">       bigquery.admin      </code></td>
<td>The table that you want to make a clone of.</td>
</tr>
<tr class="even">
<td>Any of the following:<br />
<br />
<code dir="ltr" translate="no">       bigquery.dataEditor      </code><br />
<code dir="ltr" translate="no">       bigquery.dataOwner      </code><br />
<code dir="ltr" translate="no">       bigquery.admin      </code></td>
<td>The dataset that contains the new table clone.</td>
</tr>
</tbody>
</table>

## Create a table clone

Use GoogleSQL, the bq command-line tool, or the BigQuery API to create a table clone.

### SQL

To clone a table, use the [CREATE TABLE CLONE](/bigquery/docs/reference/standard-sql/data-definition-language#create_table_clone_statement) statement.

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
    CREATE TABLE
    myproject.myDataset_backup.myTableClone
    CLONE myproject.myDataset.myTable;
    ```

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](/bigquery/docs/running-queries#queries) .

Replace the following:

  - `  PROJECT  ` is the project ID of the target project. This project must be in the same organization as the project containing the table you are cloning.
  - `  DATASET  ` is the name of the target dataset. This dataset must be in the same region as the dataset containing the table you are cloning.
  - `  CLONE_NAME  ` is name of the table clone that you are creating.

### bq

Use a [`  bq cp  `](/bigquery/docs/reference/bq-cli-reference#bq_cp) command with the `  --clone  ` flag:

``` text
bq cp --clone --no_clobber project1:myDataset.myTable PROJECT:DATASET.CLONE_NAME
```

Replace the following:

  - `  PROJECT  ` is the project ID of the target project. This project must be in the same organization as the project containing the table you are cloning.
  - `  DATASET  ` is the name of the target dataset. This dataset must be in the same region as the dataset containing the table you are cloning. If the dataset is not in the same region as the dataset containing the table you are cloning then a full table is copied.
  - `  CLONE_NAME  ` is name of the table clone that you are creating.

The `  --no_clobber  ` flag is required.

If you are creating a clone in the same project as the base table, you can skip specifying a project, as shown following:

``` text
bq cp --clone --no_clobber myDataset.myTable DATASET.CLONE_NAME
```

### API

Call the [`  jobs.insert  `](/bigquery/docs/reference/rest/v2/jobs/insert) method with the `  operationType  ` field set to `  CLONE  ` :

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
<td>The project ID of the project that runs the job.</td>
</tr>
<tr class="even">
<td>Request body</td>
<td><pre class="text" dir="ltr" data-is-upgraded="" data-syntax="JSON"><code>{
  &quot;configuration&quot;: {
    &quot;copy&quot;: {
      &quot;sourceTables&quot;: [
        {
          &quot;projectId&quot;: &quot;myProject&quot;,
          &quot;datasetId&quot;: &quot;myDataset&quot;,
          &quot;tableId&quot;: &quot;myTable&quot;
        }
      ],
      &quot;destinationTable&quot;: {
        &quot;projectId&quot;: &quot;PROJECT&quot;,
        &quot;datasetId&quot;: &quot;DATASET&quot;,
        &quot;tableId&quot;: &quot;CLONE_NAME&quot;
      },
      &quot;operationType&quot;: &quot;CLONE&quot;,
      &quot;writeDisposition&quot;: &quot;WRITE_EMPTY&quot;,
    }
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Replace the following:

  - `  PROJECT  ` is the project ID of the target project. This project must be in the same organization as the project containing the table you are cloning.
  - `  DATASET  ` is the name of the target dataset. This dataset must be in the same region as the dataset containing the table you are cloning. If the dataset is not in the same region as the dataset containing the table you are cloning a full table is copied.
  - `  CLONE_NAME  ` is name of the table clone that you are creating.

## Access control

When you create a table clone, access to the table clone is set as follows:

  - [Row-level access policies](/bigquery/docs/row-level-security-intro) are copied from the base table to the table clone.

  - [Column-level access policies](/bigquery/docs/column-level-security-intro) are copied from the base table to the table clone.

  - [Table-level access](/bigquery/docs/table-access-controls-intro) is determined as follows:
    
      - If the table clone overwrites an existing table, then the table-level access for the existing table is maintained. [Tags](/bigquery/docs/tags) aren't copied from the base table.
      - If the table clone is a new resource, then the table-level access for the table clone is determined by the access policies of the dataset in which the table clone is created. Additionally, [tags](/bigquery/docs/tags) are copied from the base table to the table clone.

## What's next

  - After you create a table clone, you can use it like you use standard tables. For more information, see [Manage tables](/bigquery/docs/managing-tables) .
