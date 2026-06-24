---
name: documents/docs.cloud.google.com/bigquery/docs/create-conversations
uri: https://docs.cloud.google.com/bigquery/docs/create-conversations
title: Analyze data with conversations
description: Learn how to create, edit, and delete conversations in BigQuery. You can use conversations to explore your BigQuery data using natural language.
data_source: docs.cloud.google.com
---

# Analyze data with conversations

This document describes how to create, edit, and delete conversations in BigQuery. Conversations are persisted chats with a [data agent](https://docs.cloud.google.com/bigquery/docs/create-data-agents) or data sources, such as tables, views or graphs, that you select.

Conversations are persisted chats with a data agent or data source. You can ask data agents multi-part questions that use common terms like "sales" or "most popular," without having to specify table field names or define conditions to filter the data. You can also ask questions about data located in objects such as PDFs. An agent can determine which data sources to query and take advantage of optimizations, such as table partitions or search indexes, when it constructs a response.

The chat response returned to you provides the following features:

  - The answer to your question as text, code, or images (multimodal). The answer can include supported BigQuery AI and ML functions.
  - Generated charts where appropriate.
  - The agent's reasoning behind the results.
  - Metadata about the conversation, such as the agent and data sources used.

When you create a direct conversation with a data source, the [Conversational Analytics API](https://docs.cloud.google.com/gemini/docs/conversational-analytics-api/overview) interprets your question without the context and processing instructions that a data agent offers. Because of this, direct conversation results can be less accurate. Use data agents for cases that require greater accuracy.

You can create and manage conversations in BigQuery using the Google Cloud console. For more information, see [Analyze data with conversations](https://docs.cloud.google.com/bigquery/docs/create-conversations) .

## Before you begin

1.  [Verify that billing is enabled for your Google Cloud project](https://docs.cloud.google.com/billing/docs/how-to/verify-billing-enabled#confirm_billing_is_enabled_on_a_project) .

2.  Enable the BigQuery, Gemini Data Analytics, and Gemini for Google Cloud APIs.
    
    **Roles required to enable APIs**
    
    To enable APIs, you need the Service Usage Admin IAM role ( `roles/serviceusage.serviceUsageAdmin` ), which contains the `serviceusage.services.enable` permission. [Learn how to grant roles](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

### Required roles

To create conversations, you must have one of the following [Conversational Analytics API IAM roles](https://docs.cloud.google.com/gemini/docs/conversational-analytics-api/access-control) :

  - To view and create conversations with any data agent that has been shared with you, you must have the Gemini Data Analytics Data Agent User ( `roles/geminidataanalytics.dataAgentUser` ) role and the Gemini for Google Cloud User ( `roles/cloudaicompanion.user` ) role at the project level.
  - To create a direct conversation, you must have the Gemini Data Analytics Stateless Chat User ( `roles/geminidataanalytics.dataAgentStatelessUser` ) role.

Additionally, in the following situations, you must have the following roles:

  - If a data agent uses a dataset as a knowledge source, you need the [BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer) ( `roles/bigquery.dataViewer` ) role on the dataset.
  - If a data agent runs a SQL query for you, you need the [BigQuery Job User](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.jobUser) ( `roles/bigquery.jobUser` ) role on the project.
  - If a data agent uses a table or view as a knowledge source, you need the [BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer) ( `roles/bigquery.dataViewer` ) role on the table or view.
  - If a table uses [column-level access control](https://docs.cloud.google.com/bigquery/docs/column-level-security-intro) , you need the [Fine-Grained Reader](https://docs.cloud.google.com/iam/docs/roles-permissions/datacatalog#datacatalog.categoryFineGrainedReader) ( `roles/datacatalog.categoryFineGrainedReader` ) role. This role is assigned to principals as part of configuring a policy tag. For more information, see [Roles used with column-level access control](https://docs.cloud.google.com/bigquery/docs/column-level-security-intro#roles) .
  - If a data table uses [row-level access control](https://docs.cloud.google.com/bigquery/docs/row-level-security-intro) , you must be granted access through the role-level access policy on that table. For more information, see [Create or update row-level access policies](https://docs.cloud.google.com/bigquery/docs/managing-row-level-security#create-policy) .
  - If a data table uses [data masking](https://docs.cloud.google.com/bigquery/docs/column-data-masking-intro) , you must be granted the [Masked Reader](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.maskedReader) ( `roles/bigquerydatapolicy.maskedReader` ) role through the appropriate data policy. For more information, see [Roles for querying masked data](https://docs.cloud.google.com/bigquery/docs/column-data-masking-intro#roles_for_querying_masked_data) .
  - To converse with a dataset, you need the [Data Catalog Viewer](https://docs.cloud.google.com/iam/docs/roles-permissions/datacatalog#datacatalog.viewer) ( `roles/datacatalog.viewer` ) on the project.

If you don't have appropriate roles on the source data tables used by the data agent, the system returns the following error when you chat with the data agent:

    Schema_Resolution: Access Denied

## Best practices

Conversational analytics automatically runs queries on your behalf to answer your questions. Consider the following factors that might increase query cost:

  - Large table sizes
  - Use of data joins in queries
  - Frequent calls to AI functions within queries

## Create a conversation with a data agent

To create a conversation with a data agent, you first [create a data agent](https://docs.cloud.google.com/bigquery/docs/create-data-agents) and publish it. You can also initiate a conversation with agents that others share with you.

To create a conversation with an existing data agent in the Google Cloud console, follow these steps:

1.  Go to the BigQuery **Agents** page.

2.  Select the **Agent Catalog** tab.

3.  From either the **My agents** or **Shared by others in your organization** section, click the agent card of the agent that you want to chat with.
    
    A new chat panel opens.

4.  In the **Ask a question** field, enter your question and choose a mode:
    
      - **Fast** (default): best for most questions.
      - **Thinking** : detailed reasoning.
    
    You can also click one of the Gemini-suggested questions to get started.

5.  Click send\_spark **Send** .
    
    The Conversational Analytics API processes your question and returns the results.

## Create a direct conversation with a data source

You can create a direct conversation with these BigQuery data sources (also referred to as knowledge sources). When you create a direct conversation, the [Conversational Analytics API](https://docs.cloud.google.com/gemini/docs/conversational-analytics-api/overview) interprets your question without the context and processing instructions offered by a data agent.

You can create a conversation with the following data sources:

  - Table
  - View
  - Dataset ( [Preview](https://docs.cloud.google.com/products#product-launch-stages) )
  - Graph ( [Preview](https://docs.cloud.google.com/products#product-launch-stages) )

### Converse with a data source using the Agents page

To create a conversation with a data source using the **Agents** page in the Google Cloud console, follow these steps:

To create a direct conversation with a data source from the **Agents** page, follow these steps:

1.  Go to the BigQuery **Agents** page.

2.  On the **Conversations** tab, click **New conversation** .

3.  In the **Chat with your data** pane, click the **Knowledge sources** tab. If your data source doesn't appear in the list, you can search for it.

4.  Select one or more data sources and click **Chat** .

### Converse with a data source using BigQuery Studio

To create a direct conversation with a data source using BigQuery Studio, choose one of the following options.

#### Converse with a dataset, table, view, or graph

To create a direct conversation with a dataset, table, view, or graph, follow these steps:

1.  In the Google Cloud console, go to the **BigQuery Studio** page.

2.  In the left pane, click explore **Explorer** .

3.  In the **Explorer** pane, expand your project, click **Datasets** , and then select a dataset. The **Datasets** page opens.

4.  Click a dataset to open it.

5.  To chat with the dataset, click chat\_spark **Chat** .

6.  To chat with a table or view in the dataset, follow these steps:
    
    1.  On the **Overview** tab, click **Tables** .
    
    2.  In the **Table ID** column, click the link to the table or view.
    
    3.  Click chat\_spark **Chat** .

7.  To chat with a graph, follow these steps:
    
    1.  On the **Overview** tab, click **Graphs** .
    
    2.  In the **Graph ID** column, click the link to the graph.
    
    3.  Click chat\_spark **Chat** .

##### Datasets

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

> **Note:** To provide feedback or request support, send an email to <bqca-feedback-external@google.com> .

Creating a conversation with a dataset lets you ask questions about your data without having to list data sources explicitly. When you create a conversation with a dataset, the data agent has access to all the tables in that dataset. When you ask a question, the data agent looks for relevant tables and joins them if necessary to produce an answer.

#### Converse with a query result

You can create a new conversation with the results after you [run a query](https://docs.cloud.google.com/bigquery/docs/running-queries#query-settings) . The data source is the temporary table of [cached results](https://docs.cloud.google.com/bigquery/docs/cached-results) that typically persists for 24 hours. After the cached results expire, you can't ask questions about the data.

To create a conversation from a query result, follow these steps:

1.  In the Google Cloud console, go to the **BigQuery Studio** page.

2.  Switch to the search\_insights query editor tab or click arrow\_drop\_down \> **Sql query** .

3.  Enter your SQL query, and then click play\_circle **Run** .

4.  On the **Results** tab, click chat\_spark **Chat** .

### How to have a conversation with a data source

After you click the **Chat** option for your data source, you can start your conversation. To have a conversation, do the following:

1.  In the **Ask a question** field, enter your question and choose a mode:
    
      - **Fast** (default): best for most questions.
      - **Thinking** : detailed reasoning.

2.  Click send\_spark **Send** .
    
    The Conversational Analytics API processes your question and returns the results. When appropriate for the data, the response provides images, charts, tables, and other visualizations.

3.  To see each step the data agent took to provide the answer to your question, expand the **Show thinking** option in the response.
    
    ![How to open the \*\*Show reasoning\*\* results](https://docs.cloud.google.com/static/bigquery/images/ca-show-reasoning.png)

4.  To see information about how the results were calculated, click keyboard\_arrow\_down **How was this calculated?**
    
    ![The API's calculation details, including the generated query and the query result.](https://docs.cloud.google.com/static/bigquery/images/ca-how-calculated.png)
    
    The **Summary** section includes the generated query followed by the query result. You can optionally open the query in the query editor.

## Create a data agent from a conversation

You can create a data agent from a conversation with a table or view. You can't create a custom agent from a conversation with a dataset.

To create a data agent from a conversation, follow these steps:

1.  From within a conversation's **Details** pane, click **Create Agent** .

2.  In the **Editor** section, in the **Agent name** field, type a descriptive name for the data agent—for example, `Q4 sales data` or `User activity logs` .

3.  In the **Agent description** field, type a description of the data agent. A good description explains what the agent does, what data it uses, and helps you know when this is the right data agent to chat with—for example, `Ask questions about customer orders and revenue` .

4.  In the **Knowledge sources** section, verify the entry in **Knowledge sources** . You can customize the existing data source, or you can click **Add source** to add additional data sources. If your data source doesn't appear in the list, you can search for it.

5.  After you've made changes, click **Save draft** .

6.  Click **Publish** .

## Manage conversations

You can open, rename, or delete a conversation on the **Agents** page, and manage conversations in BigQuery Studio Explorer.

### Open an existing conversation

1.  In the Google Cloud console, go to the BigQuery **Agents** page.

2.  On the **Conversations** tab, in the conversations list, click the conversation you want to open.

### Rename a conversation

1.  In the Google Cloud console, go to the BigQuery **Agents** page.

2.  On the **Conversations** tab, in the conversations list, click the conversation you want to rename.

3.  Click more\_vert **View actions** \> **Rename** .

4.  In the **Rename conversation** dialog, enter a new name for the conversation in the **Conversation name** field.

5.  Click **Rename** .

### Delete a conversation

Results from questions in a conversation persist even if the underlying data sources are deleted. To delete a conversation and all the results that it contains, follow these steps:

1.  In the Google Cloud console, go to the BigQuery **Agents** page.

2.  On the **Conversations** tab, in the conversations list, click the conversation you want to delete.

3.  Click more\_vert **View actions** \> **Delete** .

4.  In the **Delete conversation?** dialog, click **Delete** .

If you don't update a conversation for 180 days, then BigQuery deletes it automatically.

### Manage conversations using BigQuery Studio Explorer

Manage conversations using BigQuery Studio Explorer. This conversation list provides a central place to search for, open, or create conversations. You can also copy the conversation ID or refresh the conversations list.

To manage your conversations, follow these steps:

1.  Go to the BigQuery Studio Explorer page.

2.  In the **Explorer** pane, expand a project name.

3.  Click **Conversations** .
    
    1.  To filter the conversation list, enter a property name or value in the filter field.
    2.  To open a conversation, click more\_vert **View actions** \> **Open** .
    3.  To copy a conversation ID, click more\_vert **View actions** \> **Copy ID** .
    4.  To create a conversation, in the menu bar, click **Create conversation** .
    5.  To refresh the list, in the menu bar, click **Refresh** .

## What's next

  - Learn about [Conversational analytics in BigQuery](https://docs.cloud.google.com/bigquery/docs/conversational-analytics) .
  - Learn about the [Conversational Analytics API](https://docs.cloud.google.com/gemini/docs/conversational-analytics-api/overview) .
  - [Create data agents](https://docs.cloud.google.com/bigquery/docs/create-data-agents) .
