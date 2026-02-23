# Manage data preparations

This document describes how to manage your BigQuery data preparations, including managing access, versioning, performance, and metadata. It also describes how to perform basic tasks, such as viewing and downloading your data preparations.

Data preparations are [BigQuery](/bigquery/docs/query-overview#bigquery-studio) resources powered by [Dataform](/dataform/docs/overview) . For more information, see [Introduction to BigQuery data preparation](/bigquery/docs/data-prep-introduction) .

## Before you begin

1.  Ensure that you have enabled the [Gemini for Google Cloud API](/bigquery/docs/gemini-set-up#enable-api) .
2.  To manage data preparation metadata in Dataplex Universal Catalog, ensure that the [Dataplex API](/dataplex/docs/enable-api) is enabled in your Google Cloud project.

### Required roles

Users who are preparing the data and the Dataform service accounts that are running the jobs require the permissions granted by the following Identity and Access Management (IAM) roles.

#### Get user access for data preparation

To get the permissions that you need to prepare data in BigQuery, ask your administrator to grant you the following IAM roles :

  - [BigQuery Studio User](/iam/docs/roles-permissions/bigquery#bigquery.studioUser) ( `  roles/bigquery.studioUser  ` ) on the project
  - [Gemini for Google Cloud User](/iam/docs/roles-permissions/cloudaicompanion#cloudaicompanion.user) ( `  roles/cloudaicompanion.user  ` ) on the project
  - Access the source tables: [BigQuery Data Viewer](/iam/docs/roles-permissions/bigquery#bigquery.dataViewer) ( `  roles/bigquery.dataViewer  ` ) on the table, dataset, or project

For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

For more information about IAM for datasets in BigQuery, see [Grant access to a dataset](/bigquery/docs/control-access-to-resources-iam#grant_access_to_a_dataset) .

You might also be able to get these permissions with [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

#### Get access to manage metadata

To get the permissions you need to manage data preparation metadata in Dataplex Universal Catalog, ensure that you have the required [Dataplex Universal Catalog roles](/dataplex/docs/iam-roles) and the [`  dataform.repositories.get  `](/dataform/docs/access-control#predefined-roles) permission.

#### Give access to the Dataform service account

To ensure that the Dataform service account has the necessary permissions to execute data preparations in BigQuery, ask your administrator to grant the following IAM roles to the Dataform service account:

**Important:** You must grant these roles to the Dataform service account, *not* to your user account. Failure to grant the roles to the correct principal might result in permission errors.

  - Access the source tables: [BigQuery Data Viewer](/iam/docs/roles-permissions/bigquery#bigquery.dataViewer) ( `  roles/bigquery.dataViewer  ` ) on the table, dataset, or project
  - Access the destination tables: [BigQuery Data Editor](/iam/docs/roles-permissions/bigquery#bigquery.dataEditor) ( `  roles/bigquery.dataEditor  ` ) on the table, dataset, or project

The Dataform service account might require additional permissions, depending on your data preparation pipeline. For more information, see [Grant Dataform required access](/dataform/docs/access-control#grant-dataform-required-access) .

## View existing data preparations

To view a list of existing data preparations, follow these steps:

1.  Go to the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :
    
    If you don't see the left pane, click last\_page **Expand left pane** to open the pane.

3.  In the **Explorer** pane, expand your project.

4.  Click **Data preparations** .

## Optimize data preparation by incrementally processing data

To configure the way your prepared data is written into a destination table, follow these steps.

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :

3.  In the **Explorer** pane, click **Data preparations** , and then select your data preparation.

4.  In the toolbar of your data preparation, select **More \> Write mode** .

5.  Select one of the options. For more information, see [Write mode](/bigquery/docs/data-prep-introduction#write-mode) .

6.  Click **Save** .

## Help improve suggestions

You can help improve Gemini suggestions by sharing with Google the prompt data that you submit to features in [Preview](https://cloud.google.com/products?#product-launch-stages) . To share your prompt data, follow these steps:

1.  [Open the data preparation editor in BigQuery](/bigquery/docs/data-prep-get-suggestions#open-data-prep-editor) .
2.  In the data preparation toolbar, click settings **More** .
3.  Select **Share data to improve Gemini in BigQuery** .

Data sharing settings apply to the entire project and can only be set by a project administrator with the `  serviceusage.services.enable  ` and `  serviceusage.services.list  ` IAM permissions. For more information about data use in the Trusted Tester Program, see [Gemini for Google Cloud Trusted Tester Program](https://cloud.google.com/gemini-for-cloud/ttp/welcome) .

## Data preparation versions

You can choose to create a data preparation either inside of or outside of a [repository](/bigquery/docs/repository-intro) . Data preparation versioning is handled differently based on where the data preparation is located.

### Data preparation versioning in repositories

Repositories are Git repositories that reside either in BigQuery or with a third-party provider. You can use [workspaces](/bigquery/docs/workspaces-intro) in repositories to perform version control on data preparations. For more information, see [Use version control with a file](/bigquery/docs/workspaces#use_version_control_with_a_file) .

### Data preparation versioning outside of repositories

BigQuery data preparations that aren't in repositories don't support viewing, comparing, or restoring data preparation versions.

For a list of data preparation versions in chronological order, follow these steps:

1.  Go to the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :

3.  In the **Explorer** pane, click **Data preparations** , and then select your data preparation.

4.  Click schedule **Version history** .

## Download a data preparation

To download a data preparation in a SQLX file, follow these steps:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :

3.  In the **Explorer** pane, expand your project and click **Data preparations** .

4.  Click the name of the data preparation that you want to download.

5.  Click **Download** . The data preparation is saved in the [SQLX file format](/dataform/docs/overview#dataform-core) —for example, `  NAME data preparation.dp.sqlx  ` .

**Note:** Data preparation files created before July 2025 are automatically migrated to the SQLX format, which changes how they are stored and run. This one-time migration is triggered in the following scenarios:

  - An existing data preparation migrates when you open it.
  - A data preparation in a pipeline migrates when you save or update the data preparation.

## Upload a data preparation

To upload a data preparation from a SQLX file, follow these steps:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :

3.  In the **Explorer** pane, expand your project.

4.  Click **Data preparations** and click more\_vert **View actions \> Upload to Data preparation** .

5.  In the **Upload data preparation** dialog, select a file to upload, or enter the URL of the data preparation.

6.  Enter a name for the data preparation.

7.  Select a data preparation location where resources are managed and stored.

8.  Click **Upload** .

## Manage metadata in Dataplex Universal Catalog

Dataplex Universal Catalog lets you store and manage metadata for data preparations. Data preparations are available in Dataplex Universal Catalog by default, without additional configuration.

You can use Dataplex Universal Catalog to manage data preparations in all [BigQuery locations](/bigquery/docs/locations) . Managing data preparations in Dataplex Universal Catalog is subject to [Dataplex Universal Catalog quotas and limits](/dataplex/docs/quotas) and [Dataplex Universal Catalog pricing](https://cloud.google.com/dataplex/pricing) .

Dataplex Universal Catalog automatically retrieves the following metadata from data preparations:

  - Data asset name
  - Data asset parent
  - Data asset location
  - Data asset type
  - Corresponding Google Cloud project

Dataplex Universal Catalog logs data preparations as [entries](/dataplex/docs/ingest-custom-sources#entries) with the following entry values:

  - System entry group  
    The [system entry group](/dataplex/docs/ingest-custom-sources#entry-groups) for data preparations is `  @dataform  ` . To view details of data preparation entries in Dataplex Universal Catalog, you need to view the `  dataform  ` system entry group. For instructions about how to view a list of all entries in an entry group, see [View details of an entry group](/dataplex/docs/ingest-custom-sources#entry-group-details) in the Dataplex Universal Catalog documentation.
  - System entry type  
    The [system entry type](/dataplex/docs/ingest-custom-sources#entry-types) for data preparations is `  dataform-code-asset  ` . To view details of data preparations,you need to view the `  dataform-code-asset  ` system entry type, filter the results with an aspect-based filter, and [set the `  type  ` field inside `  dataform-code-asset  ` aspect to `  DATA_PREPARATION  `](/dataplex/docs/search-syntax#aspect-search) . Then, select an entry of the selected data preparation. For instructions about how to view details of a selected entry type, see [View details of an entry type](/dataplex/docs/ingest-custom-sources#entry-type-details) in the Dataplex Universal Catalog documentation. For instructions about how to view details of a selected entry, see [View details of an entry](/dataplex/docs/search-assets#view-entry-details) in the Dataplex Universal Catalog documentation.
  - System aspect type  
    The [system aspect type](/dataplex/docs/enrich-entries-metadata#aspect-types) for data preparations is `  dataform-code-asset  ` . To provide additional context to data preparations in Dataplex Universal Catalog by annotating data preparation entries with [aspects](/dataplex/docs/enrich-entries-metadata#aspects) , view the `  dataform-code-asset  ` aspect type, filter the results with an aspect-based filter, and [set the `  type  ` field inside `  dataform-code-asset  ` aspect to `  DATA_PREPARATION  `](/dataplex/docs/search-syntax#aspect-search) . For instructions about how to annotate entries with aspects, see [Manage aspects and enrich metadata](/dataplex/docs/enrich-entries-metadata) in the Dataplex Universal Catalog documentation.
  - Type  
    The type for data canvases is `  DATA_PREPARATION  ` . This type lets you filter data preparations in the `  dataform-code-asset  ` system entry type and the `  dataform-code-asset  ` aspect type by using the `  aspect:dataplex-types.global.dataform-code-asset.type=DATA_PREPARATION  ` query in an [aspect-based filter](/dataplex/docs/search-syntax#aspect-search) .

For instructions about how to search for assets, see [Search for data assets in Dataplex Universal Catalog](/dataplex/docs/search-assets) in the Dataplex Universal Catalog documentation.

## What's next

  - Learn more about [preparing data in BigQuery](/bigquery/docs/data-prep-introduction) .
  - Learn how to [run data preparations manually or with a schedule](/bigquery/docs/orchestrate-data-preparations) .
  - Learn how to [create data preparations](/bigquery/docs/data-prep-get-suggestions) .
