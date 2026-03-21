# Manage pipelines

This document describes how to manage [BigQuery pipelines](/bigquery/docs/pipelines-introduction) , including how to schedule and delete pipelines.

This document also describes how to view and manage pipeline metadata in [Dataplex Universal Catalog](/dataplex/docs/introduction) .

Pipelines are powered by [Dataform](/dataform/docs/overview) .

## Before you begin

1.  [Create a BigQuery pipeline](/bigquery/docs/create-pipelines) .
2.  To manage pipeline metadata in Dataplex Universal Catalog, ensure that the [Dataplex API](/dataplex/docs/enable-api) is enabled in your Google Cloud project.

### Required roles

To get the permissions that you need to manage pipelines, ask your administrator to grant you the following IAM roles:

  - To delete pipelines: [Dataform Admin](/iam/docs/roles-permissions/dataform#dataform.Admin) ( `  roles/dataform.Admin  ` ) on the pipeline
  - To view and run pipelines: [Dataform Viewer](/iam/docs/roles-permissions/dataform#dataform.Viewer) ( `  roles/dataform.Viewer  ` ) on the project

For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

To manage pipeline metadata in Dataplex Universal Catalog, ensure that you have the required [Dataplex Universal Catalog roles](/dataplex/docs/iam-roles)

For more information about Dataform IAM, see [Control access with IAM](/dataform/docs/access-control) .

**Note:** When you create a pipeline, BigQuery grants you the [Dataform Admin role](/dataform/docs/access-control#dataform.admin) ( `  roles/dataform.admin  ` ) on that pipeline. All users with the Dataform Admin role granted on the Google Cloud project have owner access to all pipelines created in the project.

## View all pipelines

To view a list of all pipelines in your project, do the following:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :
    
    If you don't see the left pane, click last\_page **Expand left pane** to open the pane.

3.  In the **Explorer** pane, expand your project and click **Pipelines** .

## View past manual runs

To view past manual runs of a selected pipeline, follow these steps:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :

3.  In the **Explorer** pane, expand your project, click **Pipelines** , and then select a pipeline.

4.  Click **Executions** .

5.  Optional: To refresh the list of past runs, click **Refresh** .

## Configure alerts for failed pipeline runs

Each pipeline has a corresponding Dataform repository ID. Each BigQuery pipeline run is logged in [Cloud Logging](/logging/docs) using the corresponding Dataform repository ID. You can use Cloud Monitoring to observe trends in Cloud Logging logs for BigQuery pipeline runs and to notify you when conditions you describe occur.

To receive alerts when a BigQuery pipeline run fails, you can create a log-based alerting policy for the corresponding Dataform repository ID. For instructions, see [Configure alerts for failed workflow invocations](/dataform/docs/monitor-runs#configure-alerts-failed-workflow-invocations) .

To find the Dataform repository ID of your pipeline, do the following:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :

3.  In the **Explorer** pane, expand your project, click **Pipelines** , and then select a pipeline.

4.  Click **Settings** .
    
    The Dataform repository ID of your pipeline is displayed at the bottom of the **Settings** tab.

## Delete a pipeline

To permanently delete a pipeline, follow these steps:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :

3.  In the **Explorer** pane, expand your project and click **Pipelines** .

4.  Find the pipeline that you want to delete.

5.  Click more\_vert **View actions** next to the pipeline, and then click **Delete** .

6.  Click **Delete** .

## Manage metadata in Dataplex Universal Catalog

Dataplex Universal Catalog lets you store and manage metadata for pipelines. Pipelines are available in Dataplex Universal Catalog by default, without additional configuration.

You can use Dataplex Universal Catalog to manage pipelines in all [pipeline locations](/bigquery/docs/locations) . Managing pipelines in Dataplex Universal Catalog is subject to [Dataplex Universal Catalog quotas and limits](/dataplex/docs/quotas) and [Dataplex Universal Catalog pricing](https://cloud.google.com/dataplex/pricing) .

Dataplex Universal Catalog automatically retrieves the following metadata from pipelines:

  - Data asset name
  - Data asset parent
  - Data asset location
  - Data asset type
  - Corresponding Google Cloud project

Dataplex Universal Catalog logs pipelines as [entries](/dataplex/docs/ingest-custom-sources#entries) with the following entry values:

  - System entry group  
    The [system entry group](/dataplex/docs/ingest-custom-sources#entry-groups) for pipelines is `  @dataform  ` . To view details of pipeline entries in Dataplex Universal Catalog, you need to view the `  dataform  ` system entry group. For instructions about how to view a list of all entries in an entry group, see [View details of an entry group](/dataplex/docs/ingest-custom-sources#entry-group-details) in the Dataplex Universal Catalog documentation.
  - System entry type  
    The [system entry type](/dataplex/docs/ingest-custom-sources#entry-types) for pipelines is `  dataform-code-asset  ` . To view details of pipelines,you need to view the `  dataform-code-asset  ` system entry type, filter the results with an aspect-based filter, and [set the `  type  ` field inside `  dataform-code-asset  ` aspect to `  WORKFLOW  `](/dataplex/docs/search-syntax#aspect-search) . Then, select an entry of the selected pipeline. For instructions about how to view details of a selected entry type, see [View details of an entry type](/dataplex/docs/ingest-custom-sources#entry-type-details) in the Dataplex Universal Catalog documentation. For instructions about how to view details of a selected entry, see [View details of an entry](/dataplex/docs/search-assets#view-entry-details) in the Dataplex Universal Catalog documentation.
  - System aspect type  
    The [system aspect type](/dataplex/docs/enrich-entries-metadata#aspect-types) for pipelines is `  dataform-code-asset  ` . To provide additional context to pipelines in Dataplex Universal Catalog by annotating data pipeline entries with [aspects](/dataplex/docs/enrich-entries-metadata#aspects) , view the `  dataform-code-asset  ` aspect type, filter the results with an aspect-based filter, and [set the `  type  ` field inside `  dataform-code-asset  ` aspect to `  WORKFLOW  `](/dataplex/docs/search-syntax#aspect-search) . For instructions about how to annotate entries with aspects, see [Manage aspects and enrich metadata](/dataplex/docs/enrich-entries-metadata) in the Dataplex Universal Catalog documentation.
  - Type  
    The type for data canvases is `  WORKFLOW  ` . This type lets you filter pipelines in the `  dataform-code-asset  ` system entry type and the `  dataform-code-asset  ` aspect type by using the `  aspect:dataplex-types.global.dataform-code-asset.type=WORKFLOW  ` query in an [aspect-based filter](/dataplex/docs/search-syntax#aspect-search) .

For instructions about how to search for assets in Dataplex Universal Catalog, see [Search for data assets in Dataplex Universal Catalog](/dataplex/docs/search-assets) in the Dataplex Universal Catalog documentation.

## What's next

  - Learn more about [BigQuery pipelines](/bigquery/docs/pipelines-introduction) .
  - Learn how to [create pipelines](/bigquery/docs/create-pipelines) .
  - Learn how to [schedule pipelines](/bigquery/docs/schedule-pipelines) .
