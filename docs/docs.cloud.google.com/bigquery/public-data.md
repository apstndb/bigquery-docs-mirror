# BigQuery public datasets

A public dataset is any dataset that is stored in BigQuery and made available to the general public through the [Google Cloud Public Dataset Program](https://cloud.google.com/datasets) . The public datasets are datasets that BigQuery hosts for you to access and integrate into your applications. Google pays for the storage of these datasets and provides public access to the data using a [project](/docs/overview#projects) . You pay only for the queries that you perform on the data. The first 1 TB per month is free, subject to [query pricing details](https://cloud.google.com/bigquery/pricing#analysis_pricing_models) .

Public datasets are available for you to analyze using either legacy SQL or [GoogleSQL](/bigquery/docs/reference/standard-sql/query-syntax) queries. Use a fully qualified table name when querying public datasets, for example `  bigquery-public-data.bbc_news.fulltext  ` . If your organization restricts data access, for example with security perimeters, then you might need to contact your administrator for permission to access public datasets.

You can access BigQuery public datasets by using the [Google Cloud console](https://console.cloud.google.com/marketplace/partners/bigquery-public-data) , by using the [bq command-line tool](/bigquery/docs/cli_tool) , or by making calls to the [BigQuery REST API](/bigquery/docs/reference/v2) using a variety of [client libraries](/bigquery/docs/reference/libraries) such as [Java](https://developers.google.com/api-client-library/java/apis/bigquery/v2) , [.NET](https://developers.google.com/api-client-library/dotnet/get_started) , or [Python](https://developers.google.com/api-client-library/python/) . You can also [view and query public datasets through BigQuery sharing (formerly Analytics Hub)](/bigquery/docs/analytics-hub-view-subscribe-listings#view-linked-datasets) , a data exchange platform that helps you discover and access data libraries.

Public datasets are not accessible by default from within a [VPC Service Controls](/vpc-service-controls/docs/overview) perimeter. There is no service-level agreement (SLA) for the Public Dataset Program.

You can find more details about each individual dataset by clicking the dataset's name in the Datasets section of Cloud Marketplace.

**Note:** The **Last Updated** date on a Cloud Marketplace dataset page indicates when the dataset page was last updated. To find out when the data itself was last updated, see [Accessing public datasets in the Google Cloud console](#public-ui) .

## Before you begin

To get started using a BigQuery public dataset, you must create or select a project. The first terabyte of data processed per month is free, so you can start querying public datasets without enabling billing. If you intend to go beyond the [free tier](https://cloud.google.com/bigquery/pricing#free-tier) , you must also enable billing.

Sign in to your Google Cloud account. If you're new to Google Cloud, [create an account](https://console.cloud.google.com/freetrial) to evaluate how our products perform in real-world scenarios. New customers also get $300 in free credits to run, test, and deploy workloads.

In the Google Cloud console, on the project selector page, select or create a Google Cloud project.

**Roles required to select or create a project**

  - **Select a project** : Selecting a project doesn't require a specific IAM role—you can select any project that you've been granted a role on.
  - **Create a project** : To create a project, you need the Project Creator role ( `  roles/resourcemanager.projectCreator  ` ), which contains the `  resourcemanager.projects.create  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .

**Note** : If you don't plan to keep the resources that you create in this procedure, create a project instead of selecting an existing project. After you finish these steps, you can delete the project, removing all resources associated with the project.

[Verify that billing is enabled for your Google Cloud project](/billing/docs/how-to/verify-billing-enabled#confirm_billing_is_enabled_on_a_project) .

Enable the BigQuery API.

**Roles required to enable APIs**

To enable APIs, you need the Service Usage Admin IAM role ( `  roles/serviceusage.serviceUsageAdmin  ` ), which contains the `  serviceusage.services.enable  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .

In the Google Cloud console, on the project selector page, select or create a Google Cloud project.

**Roles required to select or create a project**

  - **Select a project** : Selecting a project doesn't require a specific IAM role—you can select any project that you've been granted a role on.
  - **Create a project** : To create a project, you need the Project Creator role ( `  roles/resourcemanager.projectCreator  ` ), which contains the `  resourcemanager.projects.create  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .

**Note** : If you don't plan to keep the resources that you create in this procedure, create a project instead of selecting an existing project. After you finish these steps, you can delete the project, removing all resources associated with the project.

[Verify that billing is enabled for your Google Cloud project](/billing/docs/how-to/verify-billing-enabled#confirm_billing_is_enabled_on_a_project) .

Enable the BigQuery API.

**Roles required to enable APIs**

To enable APIs, you need the Service Usage Admin IAM role ( `  roles/serviceusage.serviceUsageAdmin  ` ), which contains the `  serviceusage.services.enable  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .

BigQuery is automatically enabled in new projects. To activate BigQuery in a preexisting project,

Enable the BigQuery API.

**Roles required to enable APIs**

To enable APIs, you need the Service Usage Admin IAM role ( `  roles/serviceusage.serviceUsageAdmin  ` ), which contains the `  serviceusage.services.enable  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .

## Public dataset locations

Each public dataset is stored in a specific location like `  US  ` or `  EU  ` . Currently, the BigQuery sample tables are stored in the `  US  ` multi-region [location](/bigquery/docs/locations) . When you query a sample table, supply the `  --location=US  ` flag on the command line, choose `  US  ` as the processing location in the Google Cloud console, or specify the `  location  ` property in the `  jobReference  ` section of the [job resource](/bigquery/docs/reference/rest/v2/jobs) when you use the API. Because the sample tables are stored in the US, you cannot write sample table query results to a table in another region, and you cannot join sample tables with tables in another region.

## Access public datasets in the Google Cloud console

You can access public datasets in the [Google Cloud console](https://console.cloud.google.com/bigquery) through the following methods:

  - In the [**Explorer**](/bigquery/docs/bigquery-web-ui#open-ui) pane, view the `  bigquery-public-data  ` project. For more information, see [Open a public dataset](/bigquery/docs/quickstarts/query-public-dataset-console#open_a_public_dataset) .

  - Use Sharing to [view and subscribe to public datasets](/bigquery/docs/analytics-hub-view-subscribe-listings) .

To find out when a data table was last updated, go to the table's **Details** section as described in [Get information about tables](/bigquery/docs/tables#get_information_about_tables) , and view the **Last modified** field.

## Other public datasets

There are many other public datasets available for you to query, some of which are also hosted by Google, but many more that are hosted by third parties. Other datasets include:

  - [NIH chest x-ray dataset](/healthcare-api/docs/resources/public-datasets/nih-chest)
  - [The Cancer Imaging Archive (TCIA) dataset](/healthcare-api/docs/resources/public-datasets/tcia)
  - [Dataset of release notes for the majority of generally available Google Cloud products.](https://console.cloud.google.com/bigquery?p=bigquery-public-data&d=google_cloud_release_notes&t=release_notes&page=table)

## Share a dataset with the public

You can share any of your datasets with the public by changing the dataset's access controls to allow access by "All Authenticated Users". For more information about setting dataset access controls, see [Controlling access to datasets](/bigquery/docs/dataset-access-controls) .

When you share a dataset with the public:

  - Storage charges are incurred by the billing account attached to the project that contains the publicly-shared dataset.
  - Query charges are incurred by the billing account attached to the project where the query jobs are run.

For more information, see [Overview of BigQuery pricing](https://cloud.google.com/bigquery/pricing#overview_of_pricing) .

## Sample tables

In addition to the [public datasets](https://console.cloud.google.com/marketplace/browse?filter=solution-type:dataset&q=public%20data) , BigQuery provides a limited number of sample tables that you can query. These tables are contained in the [`  bigquery-public-data:samples  ` dataset](https://console.cloud.google.com/bigquery?p=bigquery-public-data&d=samples&page=dataset) .

The requirements for querying the BigQuery sample tables are the same as the requirements for querying the public datasets.

The `  bigquery-public-data:samples  ` dataset includes the following tables:

<table>
<thead>
<tr class="header">
<th>Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://console.cloud.google.com/bigquery?p=bigquery-public-data&amp;d=samples&amp;t=gsod&amp;page=table"><code dir="ltr" translate="no">        gsod       </code></a></td>
<td>Contains weather information collected by NOAA, such as precipitation amounts and wind speeds from late 1929 to early 2010.</td>
</tr>
<tr class="even">
<td><a href="https://console.cloud.google.com/bigquery?p=bigquery-public-data&amp;d=samples&amp;t=github_nested&amp;page=table"><code dir="ltr" translate="no">        github_nested       </code></a></td>
<td>Contains a timeline of actions such as pull requests and comments on GitHub repositories with a nested schema. Created in September 2012.</td>
</tr>
<tr class="odd">
<td><a href="https://console.cloud.google.com/bigquery?p=bigquery-public-data&amp;d=samples&amp;t=github_timeline&amp;page=table"><code dir="ltr" translate="no">        github_timeline       </code></a></td>
<td>Contains a timeline of actions such as pull requests and comments on GitHub repositories with a flat schema. Created in May 2012.</td>
</tr>
<tr class="even">
<td><a href="https://console.cloud.google.com/bigquery?p=bigquery-public-data&amp;d=samples&amp;t=natality&amp;page=table"><code dir="ltr" translate="no">        natality       </code></a></td>
<td>Describes all United States births registered in the 50 States, the District of Columbia, and New York City from 1969 to 2008.</td>
</tr>
<tr class="odd">
<td><a href="https://console.cloud.google.com/bigquery?p=bigquery-public-data&amp;d=samples&amp;t=shakespeare&amp;page=table"><code dir="ltr" translate="no">        shakespeare       </code></a></td>
<td>Contains a word index of the works of Shakespeare, giving the number of times each word appears in each corpus.</td>
</tr>
<tr class="even">
<td><a href="https://console.cloud.google.com/bigquery?p=bigquery-public-data&amp;d=samples&amp;t=trigrams&amp;page=table"><code dir="ltr" translate="no">        trigrams       </code></a></td>
<td>Contains English language trigrams from a sample of works published between 1520 and 2008.</td>
</tr>
<tr class="odd">
<td><a href="https://console.cloud.google.com/bigquery?p=bigquery-public-data&amp;d=samples&amp;t=wikipedia&amp;page=table"><code dir="ltr" translate="no">        wikipedia       </code></a></td>
<td>Contains the complete revision history for all Wikipedia articles up to April 2010.</td>
</tr>
</tbody>
</table>

## Contact us

If you have any questions about the BigQuery public dataset program, contact us at `  bq-public-data@google.com  ` .

## What's next

Learn how to query a table in a public dataset at [Quickstart using the Google Cloud console](/bigquery/docs/quickstarts/quickstart-web-ui) .
