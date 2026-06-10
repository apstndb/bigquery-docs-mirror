---
name: documents/docs.cloud.google.com/bigquery/docs/use-cloud-assist
uri: https://docs.cloud.google.com/bigquery/docs/use-cloud-assist
title: Use Gemini Cloud Assist
description: Describes how to use assistive AI with Gemini Cloud Assist in BigQuery.
data_source: docs.cloud.google.com
---

# Use Gemini Cloud Assist

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

This document describes how to use [Gemini Cloud Assist](https://docs.cloud.google.com/cloud-assist/overview) , a product of the [Gemini for Google Cloud](https://cloud.google.com/products/gemini) portfolio, to help you understand and work with your metadata, jobs, and queries in BigQuery. It provides supported use cases and sample prompts that you can use in Gemini Cloud Assist.

## Before you begin

Before you can use Gemini Cloud Assist, your administrator must perform the steps to [Set up Gemini Cloud Assist](https://docs.cloud.google.com/cloud-assist/set-up-gemini) for the project or folder that you're working in.

In order to support questions and requests about your Google Cloud resources, Gemini Cloud Assist needs the appropriate Identity and Access Management (IAM) permissions for those resources. Gemini Cloud Assist inherits your permissions when you prompt it to query your BigQuery data, so in many cases, the necessary IAM permissions are already granted. For more information, see [IAM requirements for using Gemini Cloud Assist](https://docs.cloud.google.com/cloud-assist/iam-requirements) .

## Use Gemini Cloud Assist

1.  Go to the **BigQuery** page.

2.  In the Google Cloud toolbar, click spark **Open or close Gemini AI chat** to open Gemini Cloud Assist chat.
    
    ![Gemini Cloud Assist button in the BigQuery toolbar.](https://docs.cloud.google.com/static/bigquery/images/gemini-spark.png)

3.  In the **Enter a prompt** field, enter your prompt.

4.  Click send **Send** .

The following sections provide examples of tasks that you can perform with Gemini Cloud Assist, along with sample prompts.

## Analyze jobs

Learn more about jobs executed in your project, including your personal job history and project job history, to support the following use cases:

  - **Debug long-running queries** . Learn about the current status of a job and reasons it might be taking longer than expected, such as slot contention, a large number of rows scanned, high data volume, and others. In the **Cloud Assist** panel, enter a prompt similar to the following:
    
    ` Why is this job taking so long? JOB_ID  `

  - **Analyze the cause of a failed job** . Learn about why a specific query failed. In the **Cloud Assist** panel, enter a prompt similar to the following:
    
    `Why did JOB_ID fail?`

  - **Find resource-intensive queries** . Learn about your most expensive queries based on the estimated number of bytes processed. In the **Cloud Assist** panel, enter a prompt similar to the following:
    
    `What are the 3 most expensive queries that I ran in the last 2 days?`

## Discover resources

Search for and learn about datasets and table resources in a single project or across multiple projects. Gemini Cloud Assist uses Knowledge Catalog to search your BigQuery resources. Searches are performed using your permissions. For example, if you don't have permission to view the metadata of a resource, then it won't show up in the results. Supported use cases include the following:

  - **Search for a resource by name** . In the **Cloud Assist** panel, enter a prompt similar to the following:
    
    `Do I have any datasets named ecommerce?`

  - **Ask about a table's metadata** . You can ask about a table by name, or let Gemini Cloud Assist infer which table you mean based on your chat history or which table is referenced in your active query tab. If you specify a table by name, then you must use the fully qualified name. You can ask about a table's schema or other metadata, such as partitioning and clustering. In the **Cloud Assist** panel, enter a prompt similar to the following:
    
    `What's the schema for PROJECT_NAME . DATASET_NAME . TABLE_NAME ?`

  - **Ask where to find specific information** . In the **Cloud Assist** panel, enter a prompt similar to the following:
    
    `Where can I find demographics, such as age and location, for new users from the last year?`

## Analyze data lineage with Gemini Cloud Assist

You can use Gemini Cloud Assist to explore and analyze data lineage. It can help you understand data dependencies, evaluate the impact of structural changes, and summarize complex data flows. To analyze lineage, you can ask Gemini Cloud Assist questions across the following functional areas:

  - **Get lineage statistics** . Ask Gemini Cloud Assist for quantitative data about a lineage graph, such as the total number of assets, datasets, or projects involved. In the **Cloud Assist** panel, enter a prompt similar to the following:
    
      - `How many upstream assets does Customer_Master have?`
      - `How many BigQuery datasets are involved in the upstream lineage of Customer_Interaction_Summary?`
      - `Provide a count of all unique assets in the upstream graph of Marketing_Interaction.`

  - **Analyze immediate dependencies** . Identify the direct parents (sources) or direct children (consumers) of a specific asset by analyzing one-hop relationships. In the **Cloud Assist** panel, enter a prompt similar to the following:
    
      - `What are the immediate sources of Customer_Master?`
      - `What are the direct consumers of the Card_Master table?`
      - `What are the direct sources of Web_Session_Validated?`

  - **Evaluate downstream impact** . Understand the downstream consequences of modifying or dropping an asset. You can scope these prompts by depth (number of hops) or specific project boundaries. In the **Cloud Assist** panel, enter a prompt similar to the following:
    
      - `Which assets are impacted if I drop Customer_Master?`
      - `Show me the assets downstream from Customer_Master within 2 hops.`
      - `Will changing Customer_Master affect any assets in the 'data-lineage-manual-tests' project?`

  - **Identify root sources and final destinations** . Find the ultimate origins or terminal destinations of your data, bypassing intermediate transformation steps. In the **Cloud Assist** panel, enter a prompt similar to the following:
    
      - `What are all of the ultimate sources of data for Customer_Master?`
      - `What are the original data sources for Transaction_Data_Enriched, excluding intermediate tables?`
      - `What are the ultimate destinations of data from Card_Data_Validated?`

  - **Trace data flow between assets** . Ask Gemini Cloud Assist to explain the specific connection, path, or data flow between two known assets. In the **Cloud Assist** panel, enter a prompt similar to the following:
    
      - `How does Customer_Master depend on Customer_Data_Raw?`
      - `How does the data flow from Customer_Data_Raw to Customer_Profile_Snapshot?`
      - `How many hops are there between Customer_Data_Raw and Alert_Fact?`

  - **Filter lineage by asset type or name** . Search for specific types of connected assets (such as BigQuery views or Looker dashboards) or assets that match a specific naming pattern. In the **Cloud Assist** panel, enter a prompt similar to the following:
    
      - `Is Customer_Master used in any BigQuery views?`
      - `Are there any Looker dashboards downstream of Customer_Master?`
      - `What upstream tables of Customer_Master have 'Country' in their name?`

  - **Summarize lineage graphs** . Request a natural language overview of an asset's lineage rather than a specific list or count. In the **Cloud Assist** panel, enter a prompt similar to the following:
    
      - `Give me a summary of assets that depend on Web_Session_Validated.`
      - `Summarize the downstream lineage of this table.`
      - `What is the lineage of bigquery:PROJECT_NAME.DATASET_NAME`

## Generate SQL

Generate a SQL query by describing what you want the query to do. For best results, include the name of the table that you want to query. For example, in the **Cloud Assist** panel, enter a prompt similar to the following:

`Generate a SQL query to show me the duration and subscriber type for the ten longest trips. Use the bigquery-public-data.san_francisco_bikeshare.bikeshare_trips` table.

## Generate Python code

Generate Python code by describing what you want it to do. For example, in the **Cloud Assist** panel, you can enter the following prompt to ask Gemini to query the `penguins` table from a public dataset using the BigQuery magics syntax:

`Generate python code to query the bigquery-public-data.ml_datasets.penguins` table using BigQuery magics.

## Schedule a query

Schedule a query by providing the following details in your prompt:

  - Schedule, such as every Monday at 5 PM or every other Tuesday at 2 AM
  - Display name
  - Destination table ID and destination dataset ID
  - Start time
  - End time
  - Write disposition, such as `WRITE_EMPTY` , `WRITE_APPEND` or `WRITE_TRUNCATE`

For example, in the **Cloud Assist** panel, you can enter a prompt similar to the following:

    Schedule the query open in the editor to run daily. The display name
    should be "test query". Write the results to a new table in mydataset
    called scheduled_results. Use WRITE_APPEND. Start it now.

## What's next

  - Learn more about [Gemini Cloud Assist](https://docs.cloud.google.com/cloud-assist/overview) .
  - Learn how [Gemini for Google Cloud uses your data](https://docs.cloud.google.com/gemini/docs/discover/data-governance) .
