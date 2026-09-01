---
name: documents/docs.cloud.google.com/bigquery/docs/manage-pipelines
uri: https://docs.cloud.google.com/bigquery/docs/manage-pipelines
title: Manage pipelines
description: Learn how to manage BigQuery pipelines, including scheduling, deletion, and monitoring.
data_source: docs.cloud.google.com
---

# Manage pipelines

This document describes how to manage [BigQuery pipelines](https://docs.cloud.google.com/bigquery/docs/pipelines-introduction) , including how to view, schedule, deploy, and delete pipelines.

This document also describes how to view and manage pipeline metadata in [Knowledge Catalog](https://docs.cloud.google.com/dataplex/docs/introduction) .

Pipelines are powered by [Dataform](https://docs.cloud.google.com/dataform/docs/overview) . You can organize and manage pipelines stored in **Files and Folders** (user folders and team folders) or in **BigQuery Studio Git repositories (Git Folders)** ( [Preview](https://cloud.google.com/products#product-launch-stages) ).

## Before you begin

1.  [Create a BigQuery pipeline](https://docs.cloud.google.com/bigquery/docs/create-pipelines) .
2.  To manage pipeline metadata in Knowledge Catalog, ensure that the [Dataplex API](https://docs.cloud.google.com/dataplex/docs/enable-api) is enabled in your Google Cloud project.

### Required roles

To get the permissions that you need to manage pipelines, ask your administrator to grant you the following IAM roles:

  - To view and run pipelines:
      - [Dataform Viewer](https://docs.cloud.google.com/iam/docs/roles-permissions/dataform#dataform.Viewer) ( `roles/dataform.Viewer` ) on the project
      - [BigQuery Job User](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.jobUser) ( `roles/bigquery.jobUser` ) on the project
  - To run pipelines with user credentials for a Google Account: [BigQuery Data Editor](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor) ( `roles/bigquery.dataEditor` ) on the project or specific BigQuery datasets
  - To delete pipelines: [Dataform Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/dataform#dataform.Admin) ( `roles/dataform.Admin` ) on the pipeline
  - To manage pipelines in user folders:
      - [Code Owner](https://docs.cloud.google.com/iam/docs/roles-permissions/dataform#dataform.codeOwner) ( `roles/dataform.codeOwner` ) on the folder
      - [Code Editor](https://docs.cloud.google.com/iam/docs/roles-permissions/dataform#dataform.codeEditor) ( `roles/dataform.codeEditor` ) on the folder
      - [Code Viewer](https://docs.cloud.google.com/iam/docs/roles-permissions/dataform#dataform.codeViewer) ( `roles/dataform.codeViewer` ) on the folder
  - To manage pipelines in team folders:
      - [Team Folder Owner](https://docs.cloud.google.com/iam/docs/roles-permissions/dataform#dataform.teamFolderOwner) ( `roles/dataform.teamFolderOwner` ) on the team folder
      - [Team Folder Contributor](https://docs.cloud.google.com/iam/docs/roles-permissions/dataform#dataform.teamFolderContributor) ( `roles/dataform.teamFolderContributor` ) on the team folder
      - [Team Folder Viewer](https://docs.cloud.google.com/iam/docs/roles-permissions/dataform#dataform.teamFolderViewer) ( `roles/dataform.teamFolderViewer` ) on the team folder
  - To manage pipelines in Git repositories: [Developer Connect OAuth User](https://docs.cloud.google.com/iam/docs/roles-permissions/developerconnect#developerconnect.oauthUser) ( `roles/developerconnect.oauthUser` ) on the project
  - To view and manage metadata in Knowledge Catalog: [Dataplex Catalog Editor](https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.catalogEditor) ( `roles/dataplex.catalogEditor` ) on the project or `@bigquery` entry group

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

For more information about Dataform IAM, see [Control access with IAM](https://docs.cloud.google.com/dataform/docs/access-control) . For more information about roles for folders, see [Create and manage folders](https://docs.cloud.google.com/bigquery/docs/create-manage-folders#required_roles) . For more information about roles for Git repositories, see [Manage code with BigQuery Studio Git repositories](https://docs.cloud.google.com/bigquery/docs/git-repositories#required_roles) .

> **Note:** When you create a pipeline, BigQuery grants you the [Dataform Admin role](https://docs.cloud.google.com/dataform/docs/access-control#dataform.admin) ( `roles/dataform.admin` ) on that pipeline. All users with the Dataform Admin role granted on the Google Cloud project have owner access to all pipelines created in the project.

If you use a custom service account to run pipelines, you must grant the following roles to that service account:

  - [BigQuery Job User](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.jobUser) ( `roles/bigquery.jobUser` ) on the project
  - [BigQuery Data Editor](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor) ( `roles/bigquery.dataEditor` ) on the project or specific BigQuery datasets
  - [Dataplex Catalog Editor](https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.catalogEditor) ( `roles/dataplex.catalogEditor` ) on the project or `@bigquery` entry group

## View pipelines

You can view and inspect pipelines stored in folders or Git folders in the **Files** pane. You can view standalone pipelines and pipelines stored in folders in the **Explorer** pane. Pipelines stored in Git folders are not displayed in the **Explorer** pane.

### View pipelines in the Files pane

Pipelines stored in folders or in Git folders appear directly in the **Files** pane.

To view a pipeline stored in a folder or Git folder, follow these steps:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click folder **Files** to open the file browser.
    
    If you don't see the left pane, click last\_page **Expand left pane** to open the pane.

3.  Expand your **User** folder, a **Team folder** , or a connected Git repository folder.
    
    Pipelines are displayed with a **Pipeline** icon instead of a standard folder icon.

4.  Click a pipeline folder to open the **Pipeline Viewer** .
    
    The **Pipeline Viewer** displays the compiled Directed Acyclic Graph (DAG) of your pipeline tasks, execution status, and configuration tabs.

5.  Expand the pipeline directory in the file browser to browse nested directories (such as `definitions/` ) and individual task files.

> **Note:** If a connected Git repository contains `workflow_settings.yaml` in its root directory, BigQuery Studio recognizes it as a root-level pipeline. The Git repository folder itself displays the **Pipeline** icon. When you click the Git repository folder, the **Pipeline Viewer** opens, displaying the compiled DAG for the entire repository.

### View pipelines in the Explorer pane

To view a list of standalone pipelines and pipelines stored in folders, do the following:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :
    
    ![Highlighted button for the Explorer pane.](https://docs.cloud.google.com/static/bigquery/images/explorer-tab.png)
    
    If you don't see the left pane, click last\_page **Expand left pane** to open the pane.

3.  In the **Explorer** pane, expand your project and click **Pipelines** .

4.  Select a pipeline to open it in the **Pipeline Viewer** .

## View past manual runs

To view past manual runs of a selected pipeline, follow these steps:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :
    
    ![Highlighted button for the Explorer pane.](https://docs.cloud.google.com/static/bigquery/images/explorer-tab.png)

3.  In the **Explorer** pane, expand your project, click **Pipelines** , and then select a pipeline.

4.  Click **Executions** .

5.  Optional: To refresh the list of past runs, click **Refresh** .

## Configure alerts for failed pipeline runs

Each pipeline has a corresponding Dataform repository ID. Each BigQuery pipeline run is logged in [Cloud Logging](https://docs.cloud.google.com/logging/docs) using the corresponding Dataform repository ID. You can use Cloud Monitoring to observe trends in Cloud Logging logs for BigQuery pipeline runs and to notify you when conditions you describe occur.

To receive alerts when a BigQuery pipeline run fails, you can create a log-based alerting policy for the corresponding Dataform repository ID. For instructions, see [Configure alerts for failed workflow invocations](https://docs.cloud.google.com/dataform/docs/monitor-runs#configure-alerts-failed-workflow-invocations) .

To find the Dataform repository ID of your pipeline, do the following:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :
    
    ![Highlighted button for the Explorer pane.](https://docs.cloud.google.com/static/bigquery/images/explorer-tab.png)

3.  In the **Explorer** pane, expand your project, click **Pipelines** , and then select a pipeline.

4.  Click **Settings** .
    
    The Dataform repository ID of your pipeline is displayed at the bottom of the **Settings** tab.

## Delete a pipeline

To permanently delete a pipeline, follow these steps:

1.  In the Google Cloud console, go to the **BigQuery** page.

<!-- end list -->

  - To delete a pipeline stored in a folder or Git folder, do the following:
    
    1.  In the left pane, click folder **Files** .
    
    2.  In the file tree, find the pipeline folder that you want to delete.
    
    3.  Click more\_vert **View actions** next to the pipeline folder, and then click **Delete** .
    
    4.  In the confirmation dialog, click **Delete** .
        
        The pipeline folder and all tasks and files contained within it are deleted from your workspace.

  - To delete a pipeline listed in the **Explorer** pane, do the following:
    
    1.  In the left pane, click explore **Explorer** :
        
        ![Highlighted button for the Explorer pane.](https://docs.cloud.google.com/static/bigquery/images/explorer-tab.png)
    
    2.  In the **Explorer** pane, expand your project and click **Pipelines** .
    
    3.  Find the pipeline that you want to delete.
    
    4.  Click more\_vert **View actions** next to the pipeline, and then click **Delete** .
    
    5.  Click **Delete** .

## Manage metadata in Knowledge Catalog

Knowledge Catalog lets you store and manage metadata for pipelines. Pipelines are available in Knowledge Catalog by default, without additional configuration.

You can use Knowledge Catalog to manage pipelines in all [pipeline locations](https://docs.cloud.google.com/bigquery/docs/locations) . Managing pipelines in Knowledge Catalog is subject to [Knowledge Catalog quotas and limits](https://docs.cloud.google.com/dataplex/docs/quotas) and [Knowledge Catalog pricing](https://cloud.google.com/dataplex/pricing) .

Knowledge Catalog automatically retrieves the following metadata from pipelines:

  - Data asset name
  - Data asset parent
  - Data asset location
  - Data asset type
  - Corresponding Google Cloud project

Knowledge Catalog logs pipelines as [entries](https://docs.cloud.google.com/dataplex/docs/ingest-custom-sources#entries) with the following entry values:

  - System entry group  
    The [system entry group](https://docs.cloud.google.com/dataplex/docs/ingest-custom-sources#entry-groups) for pipelines is `@dataform` . To view details of pipeline entries in Knowledge Catalog, you need to view the `dataform` system entry group. For instructions about how to view a list of all entries in an entry group, see [View details of an entry group](https://docs.cloud.google.com/dataplex/docs/ingest-custom-sources#entry-group-details) in the Knowledge Catalog documentation.
  - System entry type  
    The [system entry type](https://docs.cloud.google.com/dataplex/docs/ingest-custom-sources#entry-types) for pipelines is `dataform-code-asset` . To view details of pipelines,you need to view the `dataform-code-asset` system entry type, filter the results with an aspect-based filter, and [set the `type` field inside `dataform-code-asset` aspect to `WORKFLOW`](https://docs.cloud.google.com/dataplex/docs/search-syntax#aspect-search) . Then, select an entry of the selected pipeline. For instructions about how to view details of a selected entry type, see [View details of an entry type](https://docs.cloud.google.com/dataplex/docs/ingest-custom-sources#entry-type-details) in the Knowledge Catalog documentation. For instructions about how to view details of a selected entry, see [View details of an entry](https://docs.cloud.google.com/dataplex/docs/search-assets#view-entry-details) in the Knowledge Catalog documentation.
  - System aspect type  
    The [system aspect type](https://docs.cloud.google.com/dataplex/docs/enrich-entries-metadata#aspect-types) for pipelines is `dataform-code-asset` . To provide additional context to pipelines in Knowledge Catalog by annotating data pipeline entries with [aspects](https://docs.cloud.google.com/dataplex/docs/enrich-entries-metadata#aspects) , view the `dataform-code-asset` aspect type, filter the results with an aspect-based filter, and [set the `type` field inside `dataform-code-asset` aspect to `WORKFLOW`](https://docs.cloud.google.com/dataplex/docs/search-syntax#aspect-search) . For instructions about how to annotate entries with aspects, see [Manage aspects and enrich metadata](https://docs.cloud.google.com/dataplex/docs/enrich-entries-metadata) in the Knowledge Catalog documentation.
  - Type  
    The type for data canvases is `WORKFLOW` . This type lets you filter pipelines in the `dataform-code-asset` system entry type and the `dataform-code-asset` aspect type by using the `aspect:dataplex-types.global.dataform-code-asset.type=WORKFLOW` query in an [aspect-based filter](https://docs.cloud.google.com/dataplex/docs/search-syntax#aspect-search) .

For instructions about how to search for assets in Knowledge Catalog, see [Search for data assets in Knowledge Catalog](https://docs.cloud.google.com/dataplex/docs/search-assets) in the Knowledge Catalog documentation.

### Metadata enrichment and data quality scorecard integration

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

> **Note:** To provide feedback or request support for this feature, send an email to <bq-pipelines-preview-support@google.com> .

Dataform can publish the following metadata to Knowledge Catalog:

  - Overview aspect type
  - Generic aspect type
  - Data quality scorecard aspect type

Dataform assertions are automatically integrated with the [Knowledge Catalog data quality scorecard](https://docs.cloud.google.com/dataplex/docs/enrich-entries-metadata#data-quality-scorecard) . During pipeline execution, the results of any Dataform assertions are automatically published to Knowledge Catalog. These results populate the Knowledge Catalog data quality scorecard with a pass or fail status.

> **Note:** Each execution overwrites existing data quality scorecards published by prior Dataform runs, but doesn't affect scorecards created by Knowledge Catalog data scans.

To check the status of a metadata update, follow the instructions in [View past manual runs](https://docs.cloud.google.com/bigquery/docs/manage-pipelines#view-manual-runs) .

After the metadata has been synchronized, you can search for and view the entry in Knowledge Catalog. For more information, see [Search for resources](https://docs.cloud.google.com/dataplex/docs/search-assets#search-data-assets) .

## What's next

  - Learn more about [BigQuery pipelines](https://docs.cloud.google.com/bigquery/docs/pipelines-introduction) .
  - Learn how to [create pipelines](https://docs.cloud.google.com/bigquery/docs/create-pipelines) .
  - Learn how to [schedule pipelines](https://docs.cloud.google.com/bigquery/docs/schedule-pipelines) .
  - Learn how to [manage code with BigQuery Studio Git repositories](https://docs.cloud.google.com/bigquery/docs/git-repositories) .
  - Learn how to [organize code assets with folders](https://docs.cloud.google.com/bigquery/docs/code-asset-folders) .
  - Learn more about [Dataform Deployments](https://docs.cloud.google.com/dataform/docs/deployments) .
