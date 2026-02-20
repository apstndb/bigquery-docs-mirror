# Create data agents

**Preview**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

**Note:** To provide feedback or request support for this feature, send an email to <bqca-feedback-external@google.com> .

This document describes how to create, edit, manage, and delete data agents in BigQuery.

In BigQuery, you can have [conversations](/bigquery/docs/ca/create-conversations) with data agents to ask questions about BigQuery data using natural language. Data agents contain table metadata and use-case-specific query processing instructions that define the best way to answer user questions about a set of knowledge sources, such as tables, views, or user-defined functions (UDFs) that you select.

## Before you begin

1.  [Verify that billing is enabled for your Google Cloud project](/billing/docs/how-to/verify-billing-enabled#confirm_billing_is_enabled_on_a_project) .

2.  Enable the BigQuery, Gemini Data Analytics, and Gemini for Google Cloud APIs.
    
    **Roles required to enable APIs**
    
    To enable APIs, you need the Service Usage Admin IAM role ( `  roles/serviceusage.serviceUsageAdmin  ` ), which contains the `  serviceusage.services.enable  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .

### Required roles

To work with data agents, you must have one of the following [Conversational Analytics API Identity and Access Management roles](/gemini/docs/conversational-analytics-api/access-control) :

  - Create, edit, share, and delete all data agents in the project: Gemini Data Analytics Data Agent Owner ( `  roles/geminidataanalytics.dataAgentOwner  ` ) on the project.
  - Create, edit, share, and delete your own data agents in the project: Gemini Data Analytics Data Agent Creator ( `  roles/geminidataanalytics.dataAgentCreator  ` ) on the project. This role automatically grants you the Gemini Data Analytics Data Agent Owner role on the data agents that you create.
  - View and edit all data agents in the project: Gemini Data Analytics Data Agent Editor ( `  roles/geminidataanalytics.dataAgentEditor  ` ) at the project level.
  - View all data agents in the project: Gemini Data Analytics Data Agent Viewer ( `  roles/geminidataanalytics.dataAgentViewer  ` ).

Additionally, you must have the following roles to create or edit a data agent:

  - Gemini Data Analytics Stateless Chat User ( `  roles/geminidataanalytics.dataAgentStatelessUser  ` ).
  - BigQuery Data Viewer ( `  roles/bigquery.dataViewer  ` ) on any table that the data agent uses as a knowledge source.
  - Dataplex Catalog Viewer ( `  roles/datacatalog.catalogViewer  ` ) on the project
  - If a data table uses [column-level access control](/bigquery/docs/column-level-security-intro) , Fine-Grained Reader ( `  roles/datacatalog.categoryFineGrainedReader  ` ) on the appropriate policy tag. For more information, see [Roles used with column-level access control](/bigquery/docs/column-level-security-intro#roles) .
  - If a data table uses [row-level access control](/bigquery/docs/row-level-security-intro) , you must have the row-level access policy on that table. For more information, see [Create or update row-level access policies](/bigquery/docs/managing-row-level-security#create-policy) .
  - If a data table uses [data masking](/bigquery/docs/column-data-masking-intro) , Masked Reader ( `  roles/bigquerydatapolicy.maskedReader  ` ) on the appropriate data policy. For more information, see [Roles for querying masked data](/bigquery/docs/column-data-masking-intro#roles_for_querying_masked_data) .

To work with BigQuery resources, such as viewing tables or running queries, see [BigQuery roles](/bigquery/docs/access-control#bigquery-roles) .

## Best practices

When using conversational analytics, queries are automatically run to answer your questions. You might incur unforeseen charges in the following cases:

  - If your tables are large
  - If the queries use data joins
  - If the queries make a lot of calls to AI functions

To prevent this issue, consider size when selecting knowledge sources, and when having conversations, consider using joins.

### Generate insights

You can optionally [generate data insights](/dataplex/docs/data-insights) in Dataplex Universal Catalog for any table that you want to use as a knowledge source.

Generated insights provide table metadata that the data agent can use to help generate responses to your questions.

If you don't generate insights beforehand, the system automatically generates them when you select a table as a knowledge source while creating a data agent.

## Work with the sample data agent

If you're unfamiliar with configuring agents for conversational analytics, you can optionally view the predefined sample agent generated for every Google Cloud project. You can chat with it and view its parameters to see how it was created, but you can't modify it.

To view the sample agent, do the following:

1.  In the Google Cloud console, go to the BigQuery **Agents** page.

2.  Select the **Agent catalog** tab.

3.  Under the section **Sample agents by Google** , click the sample agent card.

## Create a data agent

The following sections describe how to create a data agent.

After you create an agent, you can [edit its settings](#edit-agent) .

**Note:** If you're in a conversation with a data source, you can also [create an agent](/bigquery/docs/create-conversations#create-agent-from-conversation) from that conversation.

### Configure basics

1.  In the Google Cloud console, go to the BigQuery **Agents** page.

2.  Select the **Agent catalog** tab.

3.  Click **New agent** . The **New agent** page opens.

4.  In the **Editor** section, in the **Agent name** field, type a descriptive name for the data agent—for example, `  Q4 sales data  ` or `  User activity logs  ` .

5.  In the **Agent description** field, type a description of the data agent. A good description explains what the agent does, what data it uses, and helps you know when this is the right data agent to chat with—for example, `  Ask questions about customer orders and revenue  ` .

6.  In the **Knowledge sources** section, click **Add source** . The **Add knowledge source** page opens.

7.  In the **Recents** section, select any tables, views, or UDFs that you want to use as knowledge sources. UDFs are prefixed with an 'fx' indicator in the Google Cloud console.

8.  To view additional knowledge sources, select keyboard\_arrow\_down **Show more** .

9.  Optional: Add a knowledge source that isn't listed in the **Recents** section:
    
    1.  In the **Search** section, type the source name into the **Search for tables** field, and then press **Enter** . The source name doesn't need to be exact.
    
    2.  In the **Search results** section, select one or more sources.

10. Click **Add** . The new agent page reopens.

#### Customize table and field descriptions

To improve data agent accuracy, you can optionally provide additional table metadata. Only the data agent uses this metadata, and it doesn't affect the source table.

Follow these best practices when you create a table and field descriptions:

  - Use these descriptions as a guide to understand how the data agent understands the schema. If the descriptions suggested by the agent are correct, you can accept them.

  - If the data agent doesn't show an understanding of the schema after you configure these descriptions, then manually adjust the descriptions to provide the correct information.

Follow these steps to configure table and field descriptions:

1.  In the **Knowledge sources** section, click the **Customize** link for a table.

2.  Create a table description. You can type a description in the **Table Description** field or accept the suggestion from Gemini.

3.  In the **Fields** section, review the Gemini-suggested field descriptions.

4.  Select any field descriptions that you want to accept and click **Accept suggestions** . Select any descriptions that you want to reject and click **Reject suggestions** .

5.  Manually edit any field description by clicking edit **Edit** next to the field. The **Edit field** pane opens.
    
    1.  In the **Description** field, type a field description.
    2.  To save the field description, click **Update** .

6.  To save the description and field updates, click **Update** . The new agent page reopens.

7.  Repeat these steps for each table that needs customization.

### Configure advanced features

Configure optional advanced features such as agent instructions, verified queries (previously known as *golden queries* ), and settings.

#### Create agent instructions

The agent should understand context for user questions without needing any custom instructions. Create custom instructions for the agent only if you need to change the agent's behavior or improve the context in ways that aren't already supported by other context features—for example, custom table and field metadata, or verified queries.

In the **Instructions** section, type instructions for the data agent in the **Agent instructions** field. Because the data agent uses these instructions to understand the context for user questions and to provide answers, make the instructions as clear as possible.

If you don't get a satisfactory answer from the agent, then add structured context such as descriptions or examples. If you still don't get a satisfactory answer, then add custom instructions like the examples in the following table. For even more examples of instructions, click **Show examples** .

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Information type</th>
<th>Description</th>
<th>Examples</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Key fields</td>
<td>The most important fields for analysis.</td>
<td>"The most important fields in this table are: Customer ID, Product ID, Order Date."</td>
</tr>
<tr class="even">
<td>Filtering and grouping</td>
<td>Fields that the agent should use to filter and group data.</td>
<td>"When a question is about a timeline or 'over time,' always use the order_created_date column." "When someone says 'by product,' group by the product_category column."</td>
</tr>
<tr class="odd">
<td>Default filtering</td>
<td>Fields to filter on by default.</td>
<td>"Unless stated otherwise, always filter the data on order_status = 'Complete'."</td>
</tr>
<tr class="even">
<td>Synonyms and business terms</td>
<td>Alternative terms for key fields.</td>
<td>"If someone asks about 'Revenue' or 'Sales', use the total_sale_amount column." "We consider 'loyal' customers to be those with purchase_count &gt; 5."</td>
</tr>
<tr class="odd">
<td>Excluded fields</td>
<td>Fields that the data agent should avoid using.</td>
<td>"Never use these fields: Transaction Date Derived, City Derived."</td>
</tr>
<tr class="even">
<td>Join relationships</td>
<td>How two or more tables are related to each other, and which columns are used to join them. The agent must use standard SQL JOINs on column pairs to combine data. See the example column.</td>
<td><strong>Customer Activity</strong>
<ul>
<li><code dir="ltr" translate="no">         order_items.user_id        </code> = <code dir="ltr" translate="no">         users.id        </code><br />
(to link sales to customers)</li>
<li><code dir="ltr" translate="no">         events.user_id        </code> = <code dir="ltr" translate="no">         users.id        </code><br />
(to link website activity to logged-in customers)</li>
</ul></td>
</tr>
</tbody>
</table>

#### Create verified queries

An agent uses verified queries in two ways:

  - If an agent can use a verified query to answer a question that you ask it, to ensure a trustworthy answer, the agent invokes the query exactly as written.
  - If the agent can't use the verified query to answer a question, it still uses the query as a reference to understand the data and the best practices for querying it.

You can select verified queries from a list generated by the system, or create your own.

To create a verified query for the data agent, formerly known as a *golden query* , do the following:

1.  Select one or more Gemini-suggested verified queries:
    
    1.  In the **Verified Queries** section, click **Review suggestions** . The **Review suggested verified queries** page opens.
    2.  Review the suggested verified queries. Select any that apply to your use case.
    3.  Click **Add** . The new agent page reopens.

2.  To create your own verified query, click **Add query** . The **Add verified query** page opens.
    
    1.  In the **Question** field, type the user question that the verified query answers.
    2.  Click **Generate SQL** to have Gemini generate a verified query that corresponds to the user question that you specified.
    3.  Modify the verified query if you choose.
    4.  Click **Run** and verify that the query returns the results that you expect.
    5.  Click **Add** . The new agent page reopens.

3.  Repeat these steps as needed to create additional verified queries.

#### Configure settings

In the **Settings** section, you can configure the following optional settings:

1.  Create [labels](/bigquery/docs/labels-intro) to help you organize your Google Cloud resources. Labels are key-value pairs that let you group related objects together or with other Google Cloud resources.
    
    1.  In the **Settings** section, click **Manage labels** .
    2.  Click **Add label** .
    3.  In the **key** and **value** fields, enter your key-value pair for the label.
    4.  If you want to add more labels, click **Add label** again.
    5.  To delete a label, click **Delete** .
    6.  When you're finished, click **Add** . The new agent page reopens.

2.  Optional: Set a size limit for the queries processed by the data agent. In the **Settings** section, type a value in the **Maximum bytes billed** field. You must set this limit to `  10485760  ` or higher, otherwise you receive the following error message:

<!-- end list -->

``` text
Value error. In BigQuery on-demand pricing charges are
rounded up to the nearest MB, with a minimum of 10 MB of data processed
per query. So, max bytes billed must be set to greater or equal to
10485760.
```

If you don't specify a value, `  maximum bytes billed  ` defaults to the project's [query usage per day quota](/bigquery/quotas#query_jobs) . The usage per day quota is unlimited unless you have specified a [custom quota](/bigquery/docs/custom-quotas) .

Continue to the next section to place the agent in draft mode or publish the agent.

### Preview and publish the agent

1.  In the **Preview** section, type an example user question in the **Ask a question** field, and then press **Enter** . To verify that the data agent returns the data that you expect, review the agent's response. If the response is not what you expect, change the settings in the **Editor** section to refine the data agent configuration until you get satisfactory responses. You can continue to test and modify your agent to refine the agent's results.

2.  Click **Save** .

3.  To place the data agent in draft mode, which you can re-edit later, click arrow\_back **Go back** to return to the **Agent Catalog** page. Because your agent is now in draft mode, it appears in the **My Draft Agents** section on the **Agent Catalog** tab.
    
    To publish your agent, remain on the agent creation page and proceed to the next step.

4.  Click **Publish** to publish the data agent and make it available for use in the project. You can create conversations with the data agent by using BigQuery Studio, and [by using Looker Studio Pro](/looker/docs/studio/conversational-data-agents#start-a-conversation-with-an-agent) if you have a [Looker Studio subscription](/looker/docs/studio/about-looker-studio-pro#how-to-get-looker-studio-pro) . You can also build your own interface to chat with the data agent by using the Conversational Analytics API.

5.  Optional: In the **Your agent has been published** dialog, click **Share** to share the data agent with other users.
    
    1.  In the **Share permissions** pane, click **Add principal** .
    
    2.  In the **New principals** field, enter one or more principals.
    
    3.  Click the **Select a role** list.
    
    4.  In the **Role** list, select one of the following roles:
        
          - Gemini Data Analytics Data Agent User ( `  roles/geminidataanalytics.dataAgentUser  ` ): grants permission to chat with the data agent.
          - Gemini Data Analytics Data Agent Editor ( `  roles/geminidataanalytics.dataAgentEditor  ` ): grants permission to edit the data agent.
          - Gemini Data Analytics Data Agent Viewer ( `  roles/geminidataanalytics.dataAgentViewer  ` ): grants permission to view the data agent.

6.  Click **Save** .

7.  To return to the new agent page, click **Close** . Immediately after saving or publishing your agent, you can see it in the **Agent Catalog** .

## Manage data agents

You can find existing agents in the **Agent Catalog** tab, which consists of three sections:

  - **My Agents** : a list of all agents that you create and publish. You can modify and share published agents with others.
  - **My Draft Agents** : agents that you haven't published yet. You can't share draft agents.
  - **Shared by others in your organization** : Agents that others create and share with you. If others grant you permissions, you can edit these shared agents.

### Edit a data agent

Follow these steps to edit a data agent:

1.  Go to the BigQuery **Agents** page.

2.  Select the **Agent Catalog** tab.

3.  Locate the agent card of the data agent that you want to modify.

4.  To open the data agent in the agent editor, click more\_vert **Open actions** \> click **Edit** on the agent card.

5.  Edit the data agent's configuration as needed.

6.  To save your changes without publishing, click **Save** .

7.  To publish your changes, click **Publish** . In the **Share** dialog, you can either [share](#share-a-data-agent) the agent with others, or click **Cancel** .

8.  To return to the **Agents** pane, click arrow\_back **Go back** .

### Share a data agent

Follow these steps to share a published data agent. You can't share draft agents.

1.  Go to the BigQuery **Agents** page.

2.  Select the **Agent Catalog** tab.

3.  Locate the agent card of the data agent that you want to modify.

4.  To open the data agent in the agent editor, click more\_vert **Open actions** \> click **Edit** on the agent card.

5.  To share the data agent with other users, click **Share** .

6.  In the **Share permissions** pane, click **Add principal** .

7.  In the **New principals** field, enter one or more principals.

8.  Click the **Select a role** list.

9.  In the **Role** list, select one of the following roles:
    
      - Gemini Data Analytics Data Agent User ( `  roles/geminidataanalytics.dataAgentUser  ` ): gives permission to chat with the data agent.
      - Gemini Data Analytics Data Agent Editor ( `  roles/geminidataanalytics.dataAgentEditor  ` ): gives permission to edit the data agent.
      - Gemini Data Analytics Data Agent Viewer ( `  roles/geminidataanalytics.dataAgentViewer  ` ): gives permission to view the data agent.

10. Click **Save** .

11. To return to the agent editing page, click **Close** .

12. To return to the **Agents** pane, click arrow\_back **Go back** .

### Delete a data agent

1.  Go to the BigQuery **Agents** page.

2.  Select the **Agent Catalog** tab.

3.  In either the **My Agents** or **Draft Agents** section of the **Agent Catalog** tab, locate the agent card of the data agent that you want to delete.

4.  Click more\_vert **Open actions** \> **Delete** .

5.  In the **Delete agent?** dialog, click **Delete** .

## Locations

Conversational analytics operates globally; you can't choose which region to use.

## What's next

  - Learn more about [conversational analytics in BigQuery](/bigquery/docs/ca/conversational-analytics) .
  - Learn more about the [Conversational Analytics API](/gemini/docs/conversational-analytics-api/overview) .
  - [Analyze data with conversations](/bigquery/docs/ca/create-conversations) .
  - Learn more about how the [Gemini Data Analytics Data Agent Viewer ( `  roles/geminidataanalytics.dataAgentViewer  ` )](/gemini/docs/conversational-analytics-api/access-control#predefined-roles) role gives permission to view the data agent.
