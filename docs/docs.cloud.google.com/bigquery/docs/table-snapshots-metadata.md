# View table snapshot metadata

This document describes how to view the metadata for a BigQuery table snapshot in the Google Cloud console, by querying the [`  TABLE_SNAPSHOTS  `](/bigquery/docs/information-schema-snapshots) view of the `  INFORMATION_SCHEMA  ` table, by using the [`  bq show  `](/bigquery/docs/reference/bq-cli-reference#bq_show) command, or by calling the [`  tables.get  `](/bigquery/docs/reference/rest/v2/tables/get) API. It is intended for users who are familiar with BigQuery [tables](/bigquery/docs/tables-intro) and [table snapshots](/bigquery/docs/table-snapshots-intro) .

## Permissions and roles

This section describes the [Identity and Access Management (IAM) permission](/bigquery/docs/access-control#bq-permissions) that you need to view the metadata for a table snapshot, and the [predefined IAM roles](/bigquery/docs/access-control#bigquery) that grant those permissions.

### Permissions

To view a table snapshot's metadata, you need the following permission:

<table>
<thead>
<tr class="header">
<th><strong>Permission</strong></th>
<th><strong>Resource</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.tables.get      </code></td>
<td>The table snapshot</td>
</tr>
</tbody>
</table>

### Roles

The predefined BigQuery roles that provide the required permission are as follows:

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
<code dir="ltr" translate="no">       bigquery.metadataViewer      </code><br />
<code dir="ltr" translate="no">       bigquery.dataViewer      </code><br />
<code dir="ltr" translate="no">       bigquery.dataEditor      </code><br />
<code dir="ltr" translate="no">       bigquery.dataOwner      </code><br />
<code dir="ltr" translate="no">       bigquery.admin      </code></td>
<td>The table snapshot</td>
</tr>
</tbody>
</table>

## Get a table snapshot's metadata

The metadata for a table snapshot is similar to the metadata for a standard table, with the following differences:

  - An additional `  baseTableReference  ` field identifies the base table that the snapshot was taken from.
  - The `  type  ` field has the value `  SNAPSHOT  ` .

You can view the metadata for a table snapshot by using one of the following options:

### Console

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :
    
    If you don't see the left pane, click last\_page **Expand left pane** to open the pane.

3.  In the **Explorer** pane, expand your project, click **Datasets** , and then click the dataset that has the table snapshot.

4.  Click **Overview \> Tables** , and then click the name of the table snapshot.

5.  In the snapshot pane that appears, you can do the following:
    
      - Click the **Schema** tab to view the table snapshot's schema and policy tags.
    
      - Click the **Details** table to view the table snapshot's size, expiration, base table, snapshot time, and other information.

### SQL

To see metadata for a table snapshot, query the [`  INFORMATION_SCHEMA.TABLE_SNAPSHOTS  ` view](/bigquery/docs/information-schema-snapshots) :

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
    SELECT
      *
    FROM
      PROJECT_ID.DATASET_NAME.INFORMATION_SCHEMA.TABLE_SNAPSHOTS
    WHERE
      table_name = 'SNAPSHOT_NAME';
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
bq show \
--format=prettyjson \
PROJECT_ID:DATASET_NAME.SNAPSHOT_NAME
```

Replace the following:

  - `  PROJECT_ID  ` : the project ID of the project that contains the snapshot.
  - `  DATASET_NAME  ` : the name of the dataset that contains the snapshot.
  - `  SNAPSHOT_NAME  ` : the name of the snapshot.

The output is similar to the following:

``` text
{
  "creationTime": "1593194331936",
   ...
  "snapshotDefinition": {
    "baseTableReference": {
      "datasetId": "myDataset",
      "projectId": "myProject",
      "tableId": "mytable"
    },
    "snapshotTime": "2020-06-26T17:58:50.815Z"
  },
  "tableReference": {
    "datasetId": "otherDataset",
    "projectId": "myProject",
    "tableId": "mySnapshot"
  },
  "type": "SNAPSHOT"
}
```

### API

Call the [`  tables.get  `](/bigquery/docs/reference/rest/v2/tables/get) method with the following parameters:

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

The response body is similar to the following:

``` json
{
  "kind": "bigquery#table",
  "etag": "...",
  "id": "myProject:myDataset.mySnapshot",
  "selfLink": "https://content-bigquery.googleapis.com/bigquery/v2/projects/myProject/datasets/myDataset/tables/mySnapshot",
  "tableReference": {
    "projectId": "myProject",
    "datasetId": "myDataset",
    "tableId": "mySnapshot"
  },
  "description": "...",
  "schema": {
    "fields": [
      ...
    ]
  },
  "numBytes": "637931",
  "numLongTermBytes": "0",
  "numRows": "33266",
  "creationTime": "1593194331936",
  "lastModifiedTime": "1593194331936",
  "type": "SNAPSHOT",
  "location": "US",
  "snapshotDefinition": {
    "baseTableReference": {
      "projectId": "myProject",
      "datasetId": "otherDataset",
      "tableId": "myTable"
    },
    "snapshotTime": "2020-06-26T17:58:50.815Z"
  }
}
```

## What's next

  - [Update a table snapshot's description, expiration date, or access policy](/bigquery/docs/table-snapshots-update) .
  - [Delete a table snapshot](/bigquery/docs/table-snapshots-delete) .
