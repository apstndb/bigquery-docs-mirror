---
name: documents/docs.cloud.google.com/bigquery/docs/conversation-logging-overview
uri: https://docs.cloud.google.com/bigquery/docs/conversation-logging-overview
title: Conversation logging overview
description: Learn how conversational analytics conversation logging works in BigQuery, including privacy, limitations, and pricing.
data_source: docs.cloud.google.com
---

# Conversation logging overview

Conversational analytics conversation logging lets you record a data agent's conversations in a BigQuery table in your project so that you can review answer quality, track adoption, and monitor cost across your conversational analytics agents. For each turn, the log captures the user's question, the agent's answer, latency, model token usage, and the identifiers that you need to group turns by agent, conversation, and user. Rows are written using the [BigQuery agent analytics](https://docs.cloud.google.com/bigquery/docs/bigquery-agent-analytics) schema through the [BigQuery Storage Write API (gRPC)](https://docs.cloud.google.com/bigquery/docs/write-api) .

## What gets logged

Each logged turn writes multiple event rows ( *events* ) to the destination table that record the following information:

- The user's question.

- The agent's answer: the text, insights, assumptions, suggested follow-up questions, citation sources, and the names of any data results or charts.

- Per-turn latency.

- Model token usage, model version, and the finish reason (why the model stopped generating tokens) for each model call.

- The data agent ID and conversation ID, so that you can analyze multiple agents in one table.

- A user identifier. For more information about user identifiers, see [User identity](https://docs.cloud.google.com/bigquery/docs/conversation-log-schema#conversation-logging-user-identity) .

- Status and error details.

## What doesn't get logged

Conversation logging doesn't record the following:

- **The SQL queries that the agent runs** : the log contains the final answer and the names of the referenced data results and charts, but not the queries that produced them. The exception is when a user explicitly asks the agent to show or explain SQL; in that case, the SQL can appear in the answer text.

- **The agent's tool calls** : each model call writes one `LLM_RESPONSE` row, including calls in which the model decides to run a tool. Before the row is written, the model's output is removed, including the name and arguments of any tool that it called. Only token usage, model version, and the finish reason are kept.

- **User feedback** : thumbs-up or thumbs-down feedback isn't logged.

Some conversations aren't logged at all, such as conversations in the BigQuery Studio preview pane. For more information about unsupported conversation surfaces, see [Limitations](https://docs.cloud.google.com/bigquery/docs/conversation-logging-overview#conversation-logging-limitations) .

## How conversation logging works

When a user chats with a data agent that has conversation logging enabled, conversational analytics processes each turn through the following stages:

1.  **Configure** : an agent owner enables conversation logging and selects an existing destination dataset and table name in the agent's project in BigQuery Studio.

2.  **Ask** : a user sends a question to the agent. In BigQuery Studio, users see a notice that their conversations are logged.

3.  **Privacy check** : before the agent starts working on the turn, a privacy check reads the metadata of the agent's knowledge-source tables using the chatting user's credentials. This check confirms that none of the tables use [row-level security](https://docs.cloud.google.com/bigquery/docs/row-level-security-intro) (row access policies), [column-level security](https://docs.cloud.google.com/bigquery/docs/column-level-security-intro) (policy tags), or [dynamic data masking](https://docs.cloud.google.com/bigquery/docs/column-data-masking-intro) . If the check finds a policy or can't confirm that there are none, the turn isn't logged, and the agent still answers the user's question.

4.  **Answer** : the agent answers the user as usual.

5.  **Write** : the project's Conversational Analytics API service agent ( `service- `` PROJECT_NUMBER `` @gcp-sa-geminidataanalytics.iam.gserviceaccount.com` ) writes the log rows to the destination table through the Storage Write API (gRPC). On the first logged turn, the service agent creates the table if it doesn't already exist.

6.  **Query** : rows typically appear within a few seconds after the answer completes. Delivery time isn't guaranteed.

Logging errors never fail a turn, and the privacy check and log write can add latency. A missing permission on the log dataset, a dataset that doesn't exist, or exhausted quota doesn't fail the chat request. Conversational analytics doesn't report logging failures in the chat interface or in Cloud Logging.

> **Note:** An empty or missing table is the only signal that logging failed. If your table stays empty, see [Troubleshoot conversation logging](https://docs.cloud.google.com/bigquery/docs/troubleshoot-workload-management#troubleshoot-conversation-logging) .

## Privacy, data governance, and security

When you enable conversation logging for an agent, review how end-user notices, data access, encryption, and network controls apply to your logs.

### End-user notices and logged content

The following notices and rules govern what conversation logging records and who can view the logged data:

- **End-user notice in BigQuery Studio** : when conversation logging is turned on for an agent, users who chat with the agent in BigQuery Studio see the following notice whenever conversation logging is enabled, including on the new-conversation screen before the user sends a first prompt:

  > All prompts and responses are logged to BigQuery and are accessible to users with dataset permissions.

- **Your responsibilities when you use the API** : if you enable conversation logging (trace logging) on a data agent and make that agent available to end users through your own application or integration, Google can't display a notice to those users. You're responsible for any notices, disclosures, or consents that apply to the logged conversations under applicable law and your agreements with your end users. For more information, see [Security, privacy, risk, and compliance for the Conversational Analytics API](https://docs.cloud.google.com/gemini/data-agents/conversational-analytics-api/security-privacy-compliance) .

- **What the log contains, and who can see it** : the destination table stores question-and-answer content under these privacy rules:

  - **Full questions and answers** : answers can include values returned from your knowledge sources. Anyone who can read the log table can see data that the agent returned to a user, including data that they can't read in the source tables. Grant read access to the log dataset only to people who should see this content.

  - **User identifiers and write location** : the `user_id` column identifies the caller who asked the question (see [User identity](https://docs.cloud.google.com/bigquery/docs/conversation-log-schema#conversation-logging-user-identity) ), and rows are written only to the destination that you configure in the agent's project.

  - **Tables with row-level security, column-level security, or data masking** : if an agent's knowledge sources use [row-level security](https://docs.cloud.google.com/bigquery/docs/row-level-security-intro) (row access policies), [column-level security](https://docs.cloud.google.com/bigquery/docs/column-level-security-intro) (policy tags), or [dynamic data masking](https://docs.cloud.google.com/bigquery/docs/column-data-masking-intro) , then its turns aren't logged. The privacy check skips tables in `bigquery-public-data` and looks only at the tables and views that you select as knowledge sources, not at the tables behind a view:

    - A view over a table that uses these policies can pass the check, so its turns can be logged. Before you turn on logging, make sure that the tables behind views don't use row access policies, policy tags, or data masking.

    - If you add one of these policies to a source table later, rows that were already logged stay in the log table. If your retention or governance policy prohibits keeping those rows, then delete them.

### Access control, encryption, and network security

You can manage retention, access, encryption, and perimeter security for your conversation logs using the following settings:

- **Retention and access control on the log dataset** : configure retention, dataset roles, table policies, and audit logs for your destination table:

  - **Retention** : Google doesn't delete log rows. Set a [partition expiration](https://docs.cloud.google.com/bigquery/docs/managing-partitioned-tables#partition-expiration) on the log dataset or table that matches your policy (for example, 90 days).

  - **Least privilege** : keep the log dataset separate from your other datasets so that the shared Conversational Analytics API service agent's write access stays away from your other tables. Grant analysts `roles/bigquery.dataViewer` on the log dataset, or give them access only to [authorized views](https://docs.cloud.google.com/bigquery/docs/authorized-views) or [authorized datasets](https://docs.cloud.google.com/bigquery/docs/authorized-datasets) .

  - **Column-level and row-level controls on the log table** : you can apply [policy tags](https://docs.cloud.google.com/bigquery/docs/column-level-security-intro) , [data masking](https://docs.cloud.google.com/bigquery/docs/column-data-masking-intro) , or [row access policies](https://docs.cloud.google.com/bigquery/docs/row-level-security-intro) to the log table itself, such as on `content` or `user_id` . These log-table controls don't affect the knowledge-source privacy check.

  - **Audit logging** : changes to a data agent are recorded in [Admin Activity audit logs](https://docs.cloud.google.com/gemini/data-agents/conversational-analytics-api/audit-logging) . In BigQuery audit logs, table creation and metadata updates by the service agent are logged under `bigquery.googleapis.com` , and row appends through the Storage Write API (gRPC) are logged under `bigquerystorage.googleapis.com` .

- **CMEK, VPC Service Controls, and data residency** : the following encryption, perimeter, and location controls apply to conversation logging:

  - **CMEK** : if the log dataset uses [customer-managed Cloud KMS keys](https://docs.cloud.google.com/bigquery/docs/customer-managed-encryption) (CMEK), grant the BigQuery encryption service account ( `bq- `` PROJECT_NUMBER `` @bigquery-encryption.iam.gserviceaccount.com` ) the `roles/cloudkms.cryptoKeyEncrypterDecrypter` role on the key. CMEK on a data agent encrypts the agent resource, not the log table (see [Customer-managed encryption keys](https://docs.cloud.google.com/gemini/data-agents/conversational-analytics-api/cmek) ).

  - **VPC Service Controls** : if you use a service perimeter, include both `geminidataanalytics.googleapis.com` and `bigquery.googleapis.com` in the perimeter that contains the agent's project. The service agent writes to the log table from Google-managed infrastructure, so if the perimeter restricts `bigquery.googleapis.com` , add an ingress rule like the following. Replace `PROJECT_NUMBER` with the agent's project number:

    ```
    - ingressFrom:
        identities:
        - serviceAccount:service-PROJECT_NUMBER@gcp-sa-geminidataanalytics.iam.gserviceaccount.com
        sources:
        - accessLevel: "*"
      ingressTo:
        operations:
        - serviceName: bigquery.googleapis.com
          methodSelectors:
          - permission: bigquery.tables.get
          - permission: bigquery.tables.create
          - permission: bigquery.tables.update
          - permission: bigquery.tables.updateData
        resources:
        - projects/PROJECT_NUMBER
    ```

    For more information, see [Configure perimeter security with VPC Service Controls](https://docs.cloud.google.com/gemini/data-agents/conversational-analytics-api/vpc-sc) .

  - **Data residency** : log rows and the auto-created table are stored in the log dataset's location, where resource-location organization policies ( `gcp.resourceLocations` ) apply.

## Limitations

Conversation logging has the following limitations:

- The **Preview** pane in the BigQuery Studio agent editor isn't logged.

- Direct conversations without a data agent aren't logged.

- Agents that use a search scope instead of specific tables, or that don't declare any BigQuery tables, aren't logged. Agents that configure BigQuery property graphs as knowledge sources aren't logged.

- Generated SQL, tool calls, and Agent Development Kit (ADK) tool or request events ( `TOOL_STARTING` , `TOOL_COMPLETED` , `TOOL_ERROR` , and `LLM_REQUEST` ) aren't logged; only the answer and the names of its data results and charts are logged. Turns answered directly from a verified query don't write `LLM_RESPONSE` rows, and failed verified-query turns aren't logged.

- Thumbs-up or thumbs-down user feedback isn't logged.

- Turns aren't logged if knowledge sources use row access policies, column-level security (policy tags), or data masking, or if the privacy check can't complete. The check doesn't look through views to the tables behind them.

- Only BigQuery table agents are supported; Looker, Data Studio, AlloyDB, Spanner, and Cloud SQL data sources aren't supported.

- The destination dataset must already exist in the same project as the agent.

- Schema changes to existing tables are additive only; a conflicting column type or mode stops writes to that table.

- Every eligible turn is logged without a sampling setting; sample at query time instead (see [Sample questions and answers across all agents for review](https://docs.cloud.google.com/bigquery/docs/analyze-conversation-logs#recipe-sample-turns) ).

- The `agent` column holds the agent type rather than the agent display name; use the data agent ID in `attributes` .

- API callers that use one service account for many end users see that service account's email in every row.

- Text values longer than 512,000 characters ( `500 * 1,024` ) are cut with the suffix `...[TRUNCATED]` , and the removed part can't be recovered.

- Writes are best-effort with limited retries; turns that fail to write aren't logged, and retries can occasionally produce duplicate rows (use `event_id` to deduplicate).

- An agent doesn't inherit the project-level observability setting.

## Pricing

Conversational analytics doesn't charge separately for conversation logging. Your project pays standard BigQuery prices for [BigQuery Storage Write API (gRPC) data ingestion](https://docs.cloud.google.com/bigquery/pricing#data_ingestion_pricing) , [storage](https://docs.cloud.google.com/bigquery/pricing#storage) , and [analysis queries](https://docs.cloud.google.com/bigquery/pricing#analysis_pricing_models) . BigQuery Storage Write API (gRPC) ingestion includes 2 TiB of free usage per month for each billing account, shared across Storage Write API (gRPC) usage. Filter queries on `timestamp` to reduce scanned bytes. The pre-turn privacy check reads table metadata and runs dry-run queries at no charge.

## What's next

- [Enable conversation logging for a data agent](https://docs.cloud.google.com/bigquery/docs/create-data-agents#configure_settings) .

- [Explore the conversation log schema](https://docs.cloud.google.com/bigquery/docs/conversation-log-schema) .

- [Analyze conversation logs](https://docs.cloud.google.com/bigquery/docs/analyze-conversation-logs) .
