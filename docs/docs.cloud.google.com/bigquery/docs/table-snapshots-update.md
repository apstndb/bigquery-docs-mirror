# Update table snapshot metadata

This document describes how to update the description, expiration date, or access policy for a table snapshot by using the Google Cloud console, the [`  bq update  `](/bigquery/docs/reference/bq-cli-reference#bq_update) command, or the [`  tables.patch  `](/bigquery/docs/reference/rest/v2/tables/patch) API. It is intended for users who are familiar with [tables](/bigquery/docs/tables-intro) and [table snapshots](/bigquery/docs/table-snapshots-intro) in BigQuery.

## Permissions and roles

This section describes the [Identity and Access Management (IAM) permissions](/bigquery/docs/access-control#bq-permissions) that you need to update the metadata for a table snapshot, and the [predefined IAM roles](/bigquery/docs/access-control#bigquery) that grant those permissions.

### Permissions

To update a table snapshot's metadata, you need the following permission:

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
<td><code dir="ltr" translate="no">       bigquery.tables.update      </code></td>
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
<code dir="ltr" translate="no">       bigquery.dataEditor      </code><br />
<code dir="ltr" translate="no">       bigquery.dataOwner      </code><br />
<code dir="ltr" translate="no">       biguqery.admin      </code></td>
<td>The table snapshot</td>
</tr>
</tbody>
</table>

## Limitations

You can update a table snapshot's metadata, but you can't update its data because table snapshot data is read only. To update a table snapshot's data, you must first restore the table snapshot to a standard table, and then update the standard table's data. For more information, see [Restoring table snapshots](/bigquery/docs/table-snapshots-restore) .

## Update a table snapshot's metadata

You can change a table snapshot's description, expiration, and access policies in the same way as you change a standard table's metadata. Some examples are provided in the following sections.

### Update the description

You can change the description for a table snapshot by using one of the following options:

### Console

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :
    
    If you don't see the left pane, click last\_page **Expand left pane** to open the pane.

3.  In the **Explorer** pane, expand your project, click **Datasets** , and then click the dataset that has the table snapshot.

4.  Click **Overview \> Tables** , and then click the name of the table snapshot that you want to update.

5.  Go to the **Details** tab, and then click **Edit Details** .

6.  In the **Description** field, add or update the description for the table snapshot.

7.  Click **Save** .

### bq

Enter the following command in the Cloud Shell:

``` text
bq update \
--description="DESCRIPTION" \
PROJECT_ID:DATASET_NAME.SNAPSHOT_NAME
```

Replace the following:

  - `  DESCRIPTION  ` : text describing the snapshot. For example, `  Snapshot after table schema change X.  ` .
  - `  PROJECT_ID  ` : the project ID of the project that contains the snapshot.
  - `  DATASET_NAME  ` : the name of the dataset that contains the snapshot.
  - `  SNAPSHOT_NAME  ` : the name of the snapshot.

### API

Call the [`  tables.patch  `](/bigquery/docs/reference/rest/v2/tables/patch) method with the following parameters:

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
<tr class="even">
<td>Request body <code dir="ltr" translate="no">         description        </code> field</td>
<td>Text describing the snapshot. For example, <code dir="ltr" translate="no">         Snapshot after table schema change X        </code> .</td>
</tr>
</tbody>
</table>

Prefer the `  tables.patch  ` method over the `  tables.update  ` method because the `  tables.update  ` method replaces the entire `  Table  ` resource.

### Update the expiration

You can change the expiration of a table snapshot by using one of the following options:

### Console

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :

3.  In the **Explorer** pane, expand your project, click **Datasets** , and then click the dataset that has the table snapshot.

4.  Click **Overview \> Tables** , and then click the name of the table snapshot that you want to update.

5.  Go to the **Details** tab and then click **Edit Details** .

6.  In the **Expiration time** field, enter the new expiration time for the table snapshot.

7.  Click **Save** .

### bq

Enter the following command in the Cloud Shell:

``` text
bq update \
--expiration=EXPIRATION_TIME \
PROJECT_ID:DATASET_NAME.SNAPSHOT_NAME
```

Replace the following:

  - `  EXPIRATION_TIME  ` : the number of seconds from the current time to the expiration time.
  - `  PROJECT_ID  ` : the project ID of the project that contains the snapshot.
  - `  DATASET_NAME  ` : the name of the dataset that contains the snapshot.
  - `  SNAPSHOT_NAME  ` : the name of the snapshot.

### API

Call the [`  tables.patch  `](/bigquery/docs/reference/rest/v2/tables/patch) method with the following parameters:

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
<tr class="even">
<td>Request body <code dir="ltr" translate="no">         expirationTime        </code> field</td>
<td>The time when the snapshot expires, in milliseconds since the epoch.</td>
</tr>
</tbody>
</table>

Prefer the `  tables.patch  ` method over the `  tables.update  ` method because the `  tables.update  ` method replaces the entire `  Table  ` resource.

### Update access

You can give a user access to view the data in a table snapshot by using one of the following options:

### Console

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :

3.  In the **Explorer** pane, expand your project, click **Datasets** , and then click the dataset that has the table snapshot.

4.  Click **Overview \> Tables** , and then click the name of the table snapshot that you want to share.

5.  In the snapshot pane that appears, click **Share** , then click **Add principal** .

6.  In the **Add principals** pane that appears, enter the identifier of the [principal](/iam/docs/principals-overview) you want to give access to the table snapshot.

7.  In the **Select a role** dropdown, choose **BigQuery** , then **BigQuery Data Viewer** .

8.  Click **Save** .

### bq

Enter the following command in the Cloud Shell:

``` text
bq add-iam-policy-binding \
    --member="user:PRINCIPAL" \
    --role="roles/bigquery.dataViewer" \
    PROJECT_ID:DATASET_NAME.SNAPSHOT_NAME
```

Replace the following:

  - `  PRINCIPAL  ` : the [principal](/iam/docs/principals-overview) you want to give access to the table snapshot.
  - `  PROJECT_ID  ` : the project ID of the project that contains the snapshot.
  - `  DATASET_NAME  ` : the name of the dataset that contains the snapshot.
  - `  SNAPSHOT_NAME  ` : the name of the snapshot.

### API

Call the [`  tables.setIamPolicy  `](/bigquery/docs/reference/rest/v2/tables/setIamPolicy) method with the following parameters:

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
<td><code dir="ltr" translate="no">         Resource        </code></td>
<td><pre class="text" dir="ltr" data-is-upgraded="" data-syntax="JSON"><code>projects/PROJECT_ID/datasets/DATASET_NAME/tables/SNAPSHOT_NAME</code></pre></td>
</tr>
<tr class="even">
<td>Request body</td>
<td><pre class="text" dir="ltr" data-is-upgraded="" data-syntax="JSON"><code>{
      &quot;policy&quot;: {
        &quot;bindings&quot;: [
          {
            &quot;members&quot;: [
              &quot;user:PRINCIPAL&quot;
            ],
            &quot;role&quot;: &quot;roles/bigquery.dataViewer&quot;
          }
        ]
      }
    }</code></pre></td>
</tr>
</tbody>
</table>

Replace the following:

  - `  PROJECT_ID  ` : the project ID of the project that contains the snapshot.
  - `  DATASET_NAME  ` : the name of the dataset that contains the snapshot.
  - `  SNAPSHOT_NAME  ` : the name of the snapshot.
  - `  PRINCIPAL  ` : the [principal](/iam/docs/overview#concepts_related_identity) you want to give access to the table snapshot.

## What's next

  - [List the table snapshots in a dataset](/bigquery/docs/table-snapshots-list) .
  - [View the metadata for a table snapshot](/bigquery/docs/table-snapshots-metadata) .
  - [Delete a table snapshot](/bigquery/docs/table-snapshots-delete) .
