# Introduction to repositories

**Preview**

This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

**Note:** To provide feedback or ask questions that are related to this Preview feature, contact [bigquery-repositories-feedback@google.com](mailto:%20bigquery-repositories-feedback@google.com) .

This document helps you understand the concept of repositories in BigQuery. You can use repositories to perform version control on files you use in BigQuery. BigQuery uses Git to record changes and manage file versions.

Each BigQuery repository represents a Git repository. You can use BigQuery's built-in Git capabilities, or you can connect to a third-party Git repository. Within each repository, you can create one or more [workspaces](/bigquery/docs/workspaces-intro) to edit the code stored in the repository.

To view repositories, on the BigQuery page, in the left pane, click explore **Explorer** , and then click **Repositories** . Your repositories are displayed in alphabetical order in a new tab in the details pane.

**Important:** If you create an asset in a BigQuery repository—for example, a query, notebook (including a notebook with an Apache Spark job), BigQuery pipeline, or Dataform workflow—you cannot schedule it for execution in BigQuery repository. For scheduling and executing Dataform workflows, you need to use Dataform repositories. For scheduling queries and notebooks, use BigQuery Studio. For more information, see [Scheduling queries](/bigquery/docs/scheduling-queries) , [Schedule notebooks](/bigquery/docs/orchestrate-notebooks) , and [Schedule pipelines](/bigquery/docs/schedule-pipelines) .

## Third-party repositories

You can connect a BigQuery repository to a third-party Git repository if you choose. In this case, the third-party repository stores the repository code instead of BigQuery. BigQuery interacts with the third-party repository to allow you to edit and execute its contents in a BigQuery workspace. Depending on the type of repository you choose, you can connect to a third-party repository by using SSH or HTTPS.

The following table lists supported Git providers and the connection methods that are available for their repositories:

<table>
<thead>
<tr class="header">
<th>Git provider</th>
<th>Connection method</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Microsoft Azure DevOps Services</td>
<td>SSH</td>
</tr>
<tr class="even">
<td>Bitbucket</td>
<td>SSH</td>
</tr>
<tr class="odd">
<td>GitHub</td>
<td>SSH or HTTPS</td>
</tr>
<tr class="even">
<td>GitLab</td>
<td>SSH or HTTPS</td>
</tr>
</tbody>
</table>

For more information, see [Connect to a third-party repository](/bigquery/docs/repositories#connect-third-party) .

## Service account

All BigQuery repositories are connected to the default Dataform service agent. This service account is derived from your project number in the following format:

``` text
service-YOUR_PROJECT_NUMBER@gcp-sa-dataform.iam.gserviceaccount.com
```

## Locations

You can create repositories in all [BigQuery Studio locations](/bigquery/docs/locations#bqstudio-loc) .

## Quotas

[Dataform quotas](/dataform/docs/quotas#quotas) apply to use of BigQuery repositories.

## Pricing

You are not charged for creating, updating, or deleting a repository.

For more information on BigQuery pricing, see [Pricing](https://cloud.google.com/bigquery/pricing) .

## What's next

  - Learn how to [create repositories](/bigquery/docs/repositories) .
  - Learn how to [create workspaces](/bigquery/docs/workspaces) .
