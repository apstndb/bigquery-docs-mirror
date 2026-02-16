# Analyze data with conversations

**Preview**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

**Note:** To provide feedback or request support for this feature, send an email to <bqca-feedback-external@google.com> .

This document describes how to create, edit, and delete conversations in BigQuery. Conversations are persisted chats with a [data agent](/bigquery/docs/create-data-agents) or data sources, such as tables or views, that you select.

You can ask data agents multi-part questions that use common terms—for example, "sales" or "most popular"—without specifying table field names, or defining conditions to filter the data. The chat response provides the answer to your question as text and code, and it generates images and charts when appropriate. The response includes the reasoning behind the results.

You can create a conversation with a data agent, or a direct conversation with one or more tables. When you create a direct conversation, the [Conversational Analytics API](/gemini/docs/conversational-analytics-api/overview) interprets your question without the context and processing instructions offered by a data agent.

## Before you begin

1.  [Verify that billing is enabled for your Google Cloud project](/billing/docs/how-to/verify-billing-enabled#confirm_billing_is_enabled_on_a_project) .

2.  Enable the BigQuery, Gemini Data Analytics, and Gemini for Google Cloud APIs.
    
    **Roles required to enable APIs**
    
    To enable APIs, you need the Service Usage Admin IAM role ( `  roles/serviceusage.serviceUsageAdmin  ` ), which contains the `  serviceusage.services.enable  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .

### Required roles

To create conversations, you must have one of the following [Conversational Analytics API IAM roles](/gemini/docs/conversational-analytics-api/access-control) :

  - To view and create conversations with any data agent that has been shared with you, you must have the Gemini Data Analytics Data Agent User ( `  roles/geminidataanalytics.dataAgentUser  ` ) role and the Gemini for Google Cloud User ( `  roles/cloudaicompanion.user  ` ) role at the project level.
  - To create a direct conversation, you must have the Gemini Data Analytics Stateless Chat User ( `  roles/geminidataanalytics.dataAgentStatelessUser  ` ) role.

Additionally, in the following situations, you must have the following roles:

  - If a data agent uses a data table as a knowledge source, you must have the BigQuery Data Viewer ( `  roles/bigquery.dataViewer  ` ) role on that table.
  - If a data table uses [column-level access control](/bigquery/docs/column-level-security-intro) , you need the Fine-Grained Reader ( `  roles/datacatalog.categoryFineGrainedReader  ` ) role on the appropriate policy tag. For more information, see [Roles used with column-level access control](/bigquery/docs/column-level-security-intro#roles) .
  - If a data table uses [row-level access control](/bigquery/docs/row-level-security-intro) , you must have the role-level access policy on that table. For more information, see [Create or update row-level access policies](/bigquery/docs/managing-row-level-security#create-policy) .
  - If a data table uses [data masking](/bigquery/docs/column-data-masking-intro) , you need the Masked Reader ( `  roles/bigquerydatapolicy.maskedReader  ` ) role on the appropriate data policy. For more information, see [Roles for querying masked data](/bigquery/docs/column-data-masking-intro#roles_for_querying_masked_data) .

If you don't have appropriate roles on the source data tables used by the data agent, the system returns the following error when you chat with the data agent:

``` text
Schema_Resolution: Access Denied
```

## Best practices

When using conversational analytics, queries are automatically run to answer your questions. You might incur unforeseen charges in the following cases:

  - If your tables are large
  - If the queries use data joins
  - If the queries make a lot of calls to AI functions

To prevent this issue, consider size when selecting knowledge sources, and when having conversations, consider using joins.

## Create conversations

You can create persistent conversations with an agent or with a data source in the Google Cloud console for BigQuery in the following ways:

  - From the **Agent Catalog** tab on the **Agents** page.
  - When you view a table or query results.
  - When the system automatically uses the data source that you select for the conversation. This practice is useful for quick, one-off questions about a specific table.

### Create a conversation with a data agent

To create a conversation with a data agent, you first [create a data agent](/bigquery/docs/create-data-agents) and publish it. You can also initiate a conversation with agents that others share with you.

To create a conversation with a data agent in the Google Cloud console, select one of the following options:

### Agents page

1.  Go to the BigQuery **Agents** page.

2.  Select the **Agent Catalog** tab.

3.  From either the **My agents** or **Shared by others in your organization** section, click the agent card of the agent that you want to chat with.

4.  Click **Start a Conversation** . A new chat panel opens.

5.  In the **Ask a question** field, enter a question for the data agent. For example, "What were our total sales last quarter?" or "Show me the top 5 users by session time." You can also click one of the Gemini-suggested questions to get started.
    
    The data agent responds by stating the action it is taking to address your question, and then returns the results.
    
    To see each step the data agent took to provide the answer to your question, click **Show reasoning** to view each message in the agent's reasoning process.
    
    To see information about how the results were calculated, click keyboard\_arrow\_down **How was this calculated?**
    
    The **Summary** section now includes a generated query followed by the query result. You can optionally open the code in the query editor.
    
    When appropriate for the data, the data agent provides images, charts, tables, and other visualizations.
    
    To view your chat history, see the **Conversation Management** list.
    
    To view agent information, see the **Agent Details** panel. This panel includes a description of the agent and its knowledge sources.

### BigQuery Editor

1.  When you [work with a table](/bigquery/docs/tables) , or [run a query](/bigquery/docs/running-queries#query-settings) , click the **Create conversation** button in the menu bar to create a new conversation.

2.  In the **Ask a question** field, enter a question for the data agent. For example, "What were our total sales last quarter?" or "Show me the top 5 users by session time." You can also click one of the Gemini-suggested questions to get started.
    
    The data agent responds by stating the action it is taking to address your question, and then returns the results.
    
    To see each step the data agent took to provide the answer to your question, click **Show reasoning** to view each message in the agent's reasoning process.
    
    To see information about how the results were calculated, click keyboard\_arrow\_down **How was this calculated?**
    
    The **Summary** section now includes a generated query followed by the query result. You can optionally open the code in the query editor.
    
    When appropriate for the data, the data agent provides images, charts, tables, and other visualizations.
    
    To view your chat history, see the **Conversation Management** list.
    
    To view agent information, see the **Agent Details** panel. This panel includes a description of the agent and its knowledge sources.

### Create a direct conversation with a data source

To create a conversation with a data source in the Google Cloud console, select one of the following options:

### Agents page

To create a direct conversation with a data source from the **Agents** page, follow these steps:

1.  Go to the BigQuery **Agents** page.

2.  On the **Conversations** tab, on the **Chat with your data** pane, click **Data sources** .

3.  Select one or more tables and click **Create conversation** .

4.  In the **Ask a question** field, enter a question for the data agent. You can also click one of the Gemini-suggested questions to get started.
    
    The Conversational Analytics API processes your question and returns the results.
    
    To see the steps the Conversational Analytics API took, click **Show reasoning** to view each message in the API's reasoning process.
    
    To see information about how the results were calculated, click keyboard\_arrow\_down **How was this calculated?**
    
    The **Summary** section now includes a generated query followed by the query result. You can optionally open the query in the query editor.
    
    When appropriate for the data, the response provides images, charts, tables, and other visualizations.

### BigQuery Editor

1.  When you [work with a table](/bigquery/docs/tables) , or [run a query](/bigquery/docs/running-queries#query-settings) , click the **Create conversation** button in the menu bar to create a new conversation.

2.  In the **Ask a question** field, enter a question for the data agent. You can also click one of the Gemini-suggested questions to get started.
    
    The Conversational Analytics API processes your question and returns the results.
    
    To see the steps the Conversational Analytics API took, click **Show reasoning** .
    
    To see each step the data agent took to provide the answer to your question, click **Show reasoning** . From the list, and view each message in the agent's reasoning process.
    
    To see information about how the results were calculated, click keyboard\_arrow\_down **How was this calculated?**
    
    The **Summary** section now includes the generated query followed by the query result. You can optionally open the query in the query editor.
    
    When appropriate for the data, the response provides images, charts, tables, and other visualizations.

### Create a data agent from a conversation

1.  From within a conversation's **Data** pane, in the **Quick Actions** section, click **Create Agent** .
2.  Follow the steps to [create an agent](/bigquery/docs/create-data-agents#create-a-data-agent) .

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

1.  In the Google Cloud console, go to the BigQuery **Agents** page.

2.  On the **Conversations** tab, in the conversations list, click the conversation you want to delete.

3.  Click more\_vert **View actions** \> **Delete** .

4.  In the **Delete conversation?** dialog, click **Delete** .

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

## Locations

Conversational analytics operates globally; you can't choose which region to use.

## What's next

  - Learn about [Conversational analytics in BigQuery](/bigquery/docs/conversational-analytics) .
  - Learn about the [Conversational Analytics API](/gemini/docs/conversational-analytics-api/overview) .
  - [Create data agents](/bigquery/docs/create-data-agents) .
