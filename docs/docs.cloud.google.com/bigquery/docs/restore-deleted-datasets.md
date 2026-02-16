# Restore deleted datasets

**Preview**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

**Note:** To provide feedback or ask questions related to this preview release, contact <bq-dataset-undelete-feedback@google.com> .

This document describes how to restore (or *undelete* ) a deleted dataset in BigQuery.

You can restore a dataset to recover it to the state that it was in when it was deleted. You can only restore datasets that are within your [time travel window](/bigquery/docs/time-travel#time_travel) . This recovery includes all of the objects that were contained in the dataset, the dataset properties, and the security settings. For resources that are not recovered, see [Limitations](#limitations) .

**Caution:** Only the most recent dataset for a given dataset ID can be restored. If you delete a dataset and then create a new dataset with the same ID, you lose the ability to undelete the original dataset. However, you still might be able to [recover specific tables from the deleted dataset](/bigquery/docs/managing-datasets#restore-delete-tables) .

For information about restoring a deleted table or snapshot, see the following resources:

  - [Restore deleted tables](/bigquery/docs/restore-deleted-tables)
  - [Restore table snapshots](/bigquery/docs/table-snapshots-restore)

## Limitations

The following is a list of limitations related to restoring a dataset:

  - Restored datasets might reference security principals that no longer exist.

  - References to a deleted dataset in linked datasets aren't restored when you perform this action. Subscribers must subscribe again to manually restore the links.

  - Business tags aren't restored when you perform this action.

  - You must [manually refresh materialized views](/bigquery/docs/materialized-views-manage#manual-refresh) and reauthorize [authorized views](/bigquery/docs/authorized-views#manage_users_or_groups_for_authorized_views) , [authorized datasets](/bigquery/docs/authorized-datasets#authorize_a_dataset) , and [authorized routines](/bigquery/docs/authorized-routines#authorize_routines) .

  - You can't restore a logical view directly. However, you can undelete the dataset or recreate the view to restore your logical view. For more information on these workarounds, see [Restore a view](/bigquery/docs/managing-views#restore_a_view) .

  - A [BigQuery CDC-enabled table](/bigquery/docs/change-data-capture) doesn't resume background apply jobs when restored as part of an undeleted dataset.

  - It can take up to 24 hours for a restored dataset to appear in BigQuery search results.
    
    When authorized resources (views, datasets, and routines) are deleted, it takes up to 24 hours for the authorization to delete. So, if you restore a dataset with an authorized resource less than 24 hours after deletion, it's possible that reauthorization isn't necessary. As a best practice, always verify authorization after restoring resources.

  - Once a dataset is undeleted it cannot be deleted within the next seven days. The entities of the datasets, such as tables and routines, can be deleted. If you require a shorter period, contact [Google Cloud Support](https://cloud.google.com/support-hub) .

## Before you begin

Ensure that you have the necessary Identity and Access Management (IAM) permissions to restore a deleted dataset.

### Required roles

To get the permissions that you need to restore a deleted dataset, ask your administrator to grant you the [BigQuery User](/iam/docs/roles-permissions/bigquery#bigquery.user) ( `  roles/bigquery.user  ` ) IAM role on the project. For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

This predefined role contains the permissions required to restore a deleted dataset. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

The following permissions are required to restore a deleted dataset:

  - `  bigquery.datasets.create  ` on the project
  - `  bigquery.datasets.get  ` on the dataset

You might also be able to get these permissions with [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

## Restore a dataset

To restore a dataset, select one of the following options:

### SQL

Use the [`  UNDROP SCHEMA  ` data definition language (DDL) statement](/bigquery/docs/reference/standard-sql/data-definition-language#undrop_schema_statement) :

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
    UNDROP SCHEMA DATASET_ID;
    ```
    
    Replace `  DATASET_ID  ` with the dataset that you want to undelete.

3.  [Specify the location](/bigquery/docs/locations#specify_locations) of the dataset that you want to undelete. To specify the location part of the SQL statement use `  location  ` options
    
    ``` text
    UNDROP SCHEMA DATASET_ID OPTIONS (location=location);
    ```

4.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](/bigquery/docs/running-queries#queries) .

### API

Call the [`  datasets.undelete  ` method](/bigquery/docs/reference/rest/v2/datasets/undelete) .

**Note:** If you have two deleted datasets in your project with the same name in two different regions, undeleting a dataset with the BigQuery API undeletes only one, selected at random, unless a location is specified.

When you restore a dataset, the following errors might occur:

  - `  ALREADY_EXISTS  ` : a dataset with the same name already exists in the region in which you tried to restore. You can't use undelete to overwrite or merge datasets.

  - `  NOT_FOUND  ` : the dataset you're trying to recover is past its time travel window, it never existed, or you didn't [specify the correct location](/bigquery/docs/locations#specify_locations) of the dataset.

  - `  ACCESS_DENIED  ` : you don't have the required [permissions](#before-you-begin) to undelete this dataset.
    
    ## What's next

  - For information about querying data at a point in time, see [Access historical data](/bigquery/docs/access-historical-data) .

  - For information about data retention, see [Data retention with time travel and fail-safe](/bigquery/docs/time-travel) .

  - For information about how to delete a dataset, see [Manage datasets](/bigquery/docs/managing-datasets) .
