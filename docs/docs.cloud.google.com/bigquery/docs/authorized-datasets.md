# Authorized datasets

This document describes how to use *authorized datasets* in BigQuery. An authorized dataset lets you authorize all of the views in a specified dataset to access the data in a second dataset. With an authorized dataset, you don't need to configure individual [authorized views](/bigquery/docs/authorized-views) .

## Overview

A [view](/bigquery/docs/views-intro) in BigQuery is a virtual table defined by a SQL query. For example, a view's query might return only a subset of the columns of a table, excluding columns that contain personal identifiable information (PII). To query a view, a user needs to have access to the resources that are accessed by the view's query.

### Authorized views

If you want to let users query a view, without giving them direct access to the resources referenced by the view, you can use an [*authorized view*](/bigquery/docs/authorized-views) . When you create an authorized view, you can share either a logical view or a materialized view. When you authorize a materialized view, it's referred to as an *authorized materialized view* .

An authorized view lets you, for example, share more limited data in a view with specified groups or users (principals), without giving the principals access to all of the underlying data. Principals can view the data you share and run queries on it, but they can't access the source dataset directly. Instead, the authorized view has access to the source data.

### Authorized datasets

If you want to give a *collection of views* access to a dataset, without having to authorize each individual view, you can group the views together into a dataset, and then give the dataset that contains the views access to the dataset that contains the data. You can then give principals access to the dataset with the group of views, or to individual views in the dataset, as needed.

A dataset that has access to another dataset is called an *authorized dataset* . The dataset that authorizes another dataset to access its data is called the *shared dataset.*

**Note:** Because all current and future views in an authorized dataset have access to the tables in the shared dataset, BigQuery requires additional permissions to create or update the views in an authorized dataset, beyond the permissions that are required to create or update views in a standard dataset. For more information, see [Create or update a view in an authorized dataset](#create_or_update_view) .

## Required permissions and roles

To authorize a dataset, or to revoke a dataset's authorization, you must have the following [Identity and Access Management (IAM) permissions](/bigquery/docs/access-control#bq-permissions) , which let you update the access control list of the dataset you are sharing.

<table>
<thead>
<tr class="header">
<th><strong>Permission</strong></th>
<th><strong>Resource</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.datasets.get      </code></td>
<td>The dataset you are sharing.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigquery.datasets.update      </code></td>
<td>The dataset you are sharing.</td>
</tr>
</tbody>
</table>

The following predefined [IAM roles](/bigquery/docs/access-control#bigquery) provide the required permissions.

<table>
<thead>
<tr class="header">
<th><strong>Role</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.dataOwner      </code></td>
<td>BigQuery Data Owner</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigquery.admin      </code></td>
<td>BigQuery Admin</td>
</tr>
</tbody>
</table>

After a dataset is authorized, you can create or update views in the authorized dataset. For more information and required permissions, see [Create or update a view in an authorized dataset](#create_or_update_view) .

## Quotas and limits

Authorized datasets are subject to dataset limits. For more information, see [Dataset limits](/bigquery/quotas#dataset_limits) .

A dataset's access control list can have up to 2,500 total authorized resources, including [authorized views](/bigquery/docs/authorized-views) , [authorized datasets](/bigquery/docs/authorized-datasets) , and [authorized functions](/bigquery/docs/authorized-functions) . If you exceed this limit due to a large number of authorized views, consider grouping the views into authorized datasets. As a best practice, group related views into authorized datasets when you design new BigQuery architectures, especially multi-tenant architectures.

## Authorize a dataset

You can authorize a dataset's current and future views to access another dataset by adding the dataset you want to authorize to the access list of the dataset you want to share, as follows:

### Console

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :
    
    If you don't see the left pane, click last\_page **Expand left pane** to open the pane.

3.  In the **Explorer** pane, expand your project, click **Datasets** , and then click a dataset.

4.  In the details pane that appears, click **Sharing** and select the **Authorize Datasets** option.

5.  In the **Authorized dataset** pane that appears, enter the **Dataset ID** of the dataset that you want to authorize, in the following format:
    
    `  PROJECT . AUTHORIZED_DATASET  `
    
    For example:
    
    `  myProject.myDataset  `

6.  Click **Add Authorization** and then click **Close** .

### bq

1.  Open the Cloud Shell:

2.  Write the existing metadata (including the access control list) for the dataset you want to share into a JSON file by using the [`  bq show  `](/bigquery/docs/reference/bq-cli-reference#bq_show) command.
    
    ``` text
    bq show --format=prettyjson PROJECT:SHARED_DATASET > FILE_PATH
    ```

3.  Use a text editor to add the dataset that you want to authorize into the existing `  access  ` section of the JSON file that was created at FILE\_PATH .
    
    For example:
    
    ``` text
    "access": [
     ...
     {
       "dataset": {
         "dataset": {
           "project_id": "PROJECT",
           "dataset_id": "AUTHORIZED_DATASET"
         },
         "target_types": "VIEWS"
       }
     }
    ]
    ```

4.  Update the shared dataset by using the [`  bq update  `](/bigquery/docs/reference/bq-cli-reference#bq_update) command. For example:
    
    ``` text
    bq update --source FILE_PATH PROJECT:SHARED_DATASET
    ```

5.  To verify that the authorized dataset has been added, enter the `  bq show  ` command again. For example:
    
    ``` text
    bq show --format=prettyjson PROJECT:SHARED_DATASET
    ```

### API

1.  Get the current metadata for the dataset you want to share by calling the [`  datasets.get  `](/bigquery/docs/reference/rest/v2/datasets/get) method, as follows:
    
    ``` text
    GET https://bigquery.googleapis.com/bigquery/v2/projects/PROJECT/datasets/SHARED_DATASET
    ```
    
    The response body returns a [`  Dataset  `](/bigquery/docs/reference/rest/v2/datasets#Dataset) resource that contains JSON metadata for the dataset.

2.  Add the dataset that you want authorize into the `  access  ` section of the JSON metadata that was returned in the `  Dataset  ` resource as follows:
    
    ``` text
    "access": [
     ...
     {
       "dataset": {
         "dataset": {
           "project_id": "PROJECT",
           "dataset_id": "AUTHORIZED_DATASET"
         },
         "target_types": "VIEWS"
       }
     }
    ]
    ```

3.  Use the [`  datasets.update  `](/bigquery/docs/reference/v2/datasets/update) method to update the dataset with the added authorization:
    
    ``` text
    PUT https://bigquery.googleapis.com/bigquery/v2/projects/PROJECT/datasets/SHARED_DATASET
    ```
    
    Include the updated `  Dataset  ` resource in the request body.

4.  You can verify that the authorized dataset has been added by calling the [`  datasets.get  `](/bigquery/docs/reference/rest/v2/datasets/get) method again.

## Revoke a dataset's authorization

When you delete a dataset authorized to access another source dataset, it can take up to 24 hours for the change to fully reflect in the source dataset's [access control lists (ACLs)](/storage/docs/access-control/lists) . During this time:

  - You won't be able to access the source data through the deleted dataset.
  - The deleted dataset might still appear in the source dataset's ACL and count towards any authorized dataset limits. This could prevent you from creating new authorized datasets until the ACL is updated.

To revoke the access granted to the views in an authorized dataset, remove the authorized dataset from the shared dataset's access list, as follows:

### Console

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :

3.  In the **Explorer** pane, expand your project, click **Datasets** , and then click a dataset.

4.  In the details pane that appears, click **Sharing** and select the **Authorize Datasets** option.

5.  In the **Authorized dataset** pane that appears, find the entry for the authorized dataset in the **Currently authorized datasets** section.

6.  Click the delete icon next to the authorized dataset you want to remove, and then click **Close** .

### bq

1.  Open the Cloud Shell:

2.  Write the existing metadata (including the access control list) for the shared dataset into a JSON file by using the [`  bq show  `](/bigquery/docs/reference/bq-cli-reference#bq_show) command.
    
    ``` text
    bq show --format=prettyjson PROJECT:SHARED_DATASET > FILE_PATH
    ```

3.  Use a text editor to remove the authorized dataset from the `  access  ` section of the JSON file that was created at FILE\_PATH , as follows:
    
    ``` text
      {
        "dataset": {
          "dataset": {
            "project_id": "PROJECT",
            "dataset_id": "AUTHORIZED_DATASET"
          },
          "target_types": "VIEWS"
        }
      }
    ```

4.  Update the shared dataset by using the [`  bq update  `](/bigquery/docs/reference/bq-cli-reference#bq_update) command. For example:
    
    ``` text
    bq update --source FILE_PATH PROJECT:SHARED_DATASET
    ```

5.  To verify that the authorized dataset has been removed, enter the `  bq show  ` command again. For example:
    
    ``` text
    bq show --format=prettyjson PROJECT:SHARED_DATASET
    ```

### API

1.  Get the current metadata for the shared dataset by calling the [`  datasets.get  `](/bigquery/docs/reference/rest/v2/datasets/get) method, as follows:
    
    ``` text
    GET https://bigquery.googleapis.com/bigquery/v2/projects/PROJECT/datasets/SHARED_DATASET
    ```
    
    The response body returns a [`  Dataset  `](/bigquery/docs/reference/rest/v2/datasets#Dataset) resource that contains JSON metadata for the dataset.

2.  Remove the authorized dataset from the `  access  ` section of the JSON that was returned in the `  Dataset  ` resource, for example:
    
    ``` text
     {
       "dataset": {
         "dataset": {
           "project_id": "PROJECT",
           "dataset_id": "AUTHORIZED_DATASET"
         },
         "target_types": "VIEWS"
       }
     }
    ```

3.  Use the [`  datasets.update  `](/bigquery/docs/reference/v2/datasets/update) method to update the dataset with the removed authorization:
    
    ``` text
    PUT https://bigquery.googleapis.com/bigquery/v2/projects/PROJECT/datasets/SHARED_DATASET
    ```
    
    Include the updated `  Dataset  ` resource in the request body.

4.  You can verify that the authorized dataset has been removed by calling the [`  datasets.get  `](/bigquery/docs/reference/rest/v2/datasets/get) method again.

## Create or update a view in an authorized dataset

To create or update a view that is in an authorized dataset, you must have the permissions for the shared dataset that are listed in [Required permissions and roles](#permissions_datasets) , in addition to the permissions that are required to [create](/bigquery/docs/views#required_permissions) or [update](/bigquery/docs/managing-views#update_a_view) a view in a standard dataset.

The following table summarizes the necessary [Identity and Access Management (IAM) permissions](/bigquery/docs/access-control#bq-permissions) to create or update a view that is in an authorized dataset:

<table>
<thead>
<tr class="header">
<th><strong>Permission</strong></th>
<th><strong>Resource</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.datasets.get      </code></td>
<td>The dataset you are sharing.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigquery.tables.getData      </code></td>
<td>Any tables or views from the shared dataset that are referenced in the new view you are creating or updating.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.tables.create      </code></td>
<td>The authorized dataset in which you are creating a view.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigquery.tables.update      </code></td>
<td>The authorized dataset in which you are updating a view.</td>
</tr>
</tbody>
</table>

You don't need any additional permissions to [delete a view](/bigquery/docs/managing-views#delete_views) from an authorized dataset.

**Note:** The `  bigquery.datasets.update  ` permission is not required for creating or updating a view in an authorized dataset. However, `  bigquery.datasets.update  ` is required for managing authorized views. For more information, see [Required roles](/bigquery/docs/authorized-views#required_permissions) .

**Note:** Statements that manage views, such as `  ALTER VIEW  ` , can apply to both regular views and authorized views. Verify that you are managing the correct view when running these statements.

## Query a view in an authorized dataset

To query a view in an authorized dataset, a user needs to have access to the view, but access to the shared dataset is not required.

For more information, see [Authorized views](/bigquery/docs/authorized-views) .

## Authorized dataset example

The following example describes how to create and use an authorized dataset.

Assume you have two datasets, named `  private_dataset  ` and `  public_dataset  ` . The `  private_dataset  ` dataset contains a table named `  private_table  ` . The `  public_dataset  ` dataset contains a view named `  private_table_filtered  ` . The `  private_table_filtered  ` view is based on a query that returns some, but not all, of the fields in the `  private_table  ` table.

You can give a user access to the data returned by the `  private_table_filtered  ` view, but not all of the data in the `  private_table  ` table, as follows:

1.  Grant the `  bigquery.dataViewer  ` role to the user for the `  public_dataset  ` dataset. This role includes the `  bigquery.tables.getData  ` permission, which lets the user query the views in the `  public_dataset  ` dataset. For information about how to grant a role to a user for a dataset, see [Controlling access to datasets](/bigquery/docs/dataset-access-controls) .
    
    The user now has permission to query views in the `  public_dataset  ` , but they still cannot access the `  private_table  ` table in `  private_dataset  ` . If the user tries to query the `  private_table  ` table directly, or if they try to access the `  private_table  ` table indirectly by querying the `  private_table_filtered  ` view, they get an error message similar to the following:
    
    `  Access Denied: Table PROJECT :private_dataset.private_table: User does not have permission to query table PROJECT :private_dataset.private_table.  `

2.  In the **BigQuery** page of the Google Cloud console, open the `  private_dataset  ` dataset, click **Sharing** , and then select **Authorize Datasets** .

3.  In the **Authorized dataset** pane that appears, enter `  PROJECT .public_dataset  ` in the **Dataset ID** field, and then click **Add Authorization** .
    
    The `  public_dataset  ` dataset is added to the access control list of the `  private_dataset  ` dataset, authorizing the views in the `  public_dataset  ` dataset to query the data in the `  private_dataset  ` dataset.
    
    The user can now query the `  private_table_filtered  ` view in the `  public_dataset  ` dataset, which indirectly accesses the `  private_dataset  ` dataset, without having any permissions to directly access data in the `  private_dataset  ` dataset.

## Limitations

  - You can create authorized datasets in different regions, but BigQuery doesn't support cross-region queries. Therefore, we recommend that you create datasets in the same region.

## What's next

  - For information about authorizing an individual view to access data in a dataset, see [Authorized views](/bigquery/docs/authorized-views) .

  - For information about authorizing a table function or a user-defined function to access data in a dataset, see [Authorized functions](/bigquery/docs/authorized-functions) .
