---
name: documents/docs.cloud.google.com/bigquery/docs/analyze-conversation-logs
uri: https://docs.cloud.google.com/bigquery/docs/analyze-conversation-logs
title: Analyze conversation logs
description: Query, evaluate, and troubleshoot conversational analytics conversation logs in BigQuery using SQL recipes, interactive notebooks, and the Python SDK.
data_source: docs.cloud.google.com
---

# Analyze conversation logs

This document shows how to query, evaluate, and troubleshoot conversational analytics conversation logs in BigQuery using GoogleSQL recipes, an interactive Colab notebook, and the [BigQuery agent analytics](https://docs.cloud.google.com/bigquery/docs/bigquery-agent-analytics) Python SDK. For more information about the destination table columns and JSON structure, see [Conversation log schema](https://docs.cloud.google.com/bigquery/docs/conversation-log-schema) .

## Use the Colab notebook and Python SDK

You can run the SQL recipes in this document alongside the [`bigquery-agent-analytics`](https://github.com/GoogleCloudPlatform/BigQuery-Agent-Analytics-SDK) Python SDK (v0.5.4 or later) by using the Customer Analytics, FinOps & Evaluation Starter Notebook ( [open in Colaboratory](https://colab.research.google.com/github/GoogleCloudPlatform/BigQuery-Agent-Analytics-SDK/blob/main/examples/bqca_prompt_response_logging_customer_notebook.ipynb) \| [view on GitHub](https://github.com/GoogleCloudPlatform/BigQuery-Agent-Analytics-SDK/blob/main/examples/bqca_prompt_response_logging_customer_notebook.ipynb) ).

To use the Python SDK with your conversation log table, first create the `v_bqca_sdk_events` compatibility view. On `AGENT_RESPONSE` rows, conversational analytics stores a JSON object in `content.response` , whereas the SDK's `LLMAsJudge` evaluators expect `JSON_VALUE(content, '$.response')` to return a scalar string. This view sets `$.text_summary` and `$.response` to the plain-text answer while keeping the original object in `$.raw_response` .

In the following SQL and Python snippets, replace these placeholders:

- `PROJECT_ID` : the ID of the project that contains your data agent and log dataset.

- `LOG_DATASET` : the ID of the BigQuery dataset that stores your raw conversation log table.

- `LOG_TABLE` : the ID of the conversation log table, such as `agent_events` .

- `ANALYTICS_DATASET` : the ID of the BigQuery dataset in the same location where you create analytics views and table functions.

- `LOCATION` : the BigQuery location of the analytics dataset, such as `US` .

Creating views and table functions in `ANALYTICS_DATASET` requires write access on `ANALYTICS_DATASET` , such as the [BigQuery Data Editor](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataEditor) ( `roles/bigquery.dataEditor` ) role, and the [BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer) ( `roles/bigquery.dataViewer` ) role on `LOG_DATASET` . Analysts who only query the views need the BigQuery Data Viewer role on `ANALYTICS_DATASET` and the [BigQuery Job User](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.jobUser) ( `roles/bigquery.jobUser` ) role on the project where they run queries.

The following query creates the `v_bqca_sdk_events` view, which is used in the next step to validate your table schema and event coverage:

```
CREATE OR REPLACE VIEW `PROJECT_ID.ANALYTICS_DATASET.v_bqca_sdk_events` AS
WITH allowlisted AS (
  SELECT
    *,
    IF(
      event_type = 'AGENT_RESPONSE' AND content IS NOT NULL,
      COALESCE(
        NULLIF(JSON_VALUE(content, '$.text_summary'), ''),
        NULLIF(ARRAY_TO_STRING(ARRAY(
          SELECT JSON_VALUE(part, '$.markdown')
          FROM UNNEST(JSON_QUERY_ARRAY(content, '$.response.parts')) AS part WITH OFFSET AS part_offset
          WHERE JSON_VALUE(part, '$.markdown') IS NOT NULL
          ORDER BY part_offset
        ), '\n\n'), ''),
        NULLIF(JSON_VALUE(content, '$.response.clarifying_question'), ''),
        JSON_VALUE(content, '$.response')
      ),
      NULL
    ) AS answer_text
  FROM `PROJECT_ID.LOG_DATASET.LOG_TABLE`
  WHERE event_type IN (
    'INVOCATION_STARTING', 'USER_MESSAGE_RECEIVED', 'AGENT_RESPONSE',
    'INVOCATION_COMPLETED', 'LLM_RESPONSE', 'EMBEDDING_SUGGESTION',
    'INVOCATION_ERROR', 'AGENT_ERROR', 'LLM_ERROR'
  )
)
SELECT
  * EXCEPT(answer_text)
  REPLACE (
    CASE
      WHEN event_type = 'AGENT_RESPONSE' AND content IS NOT NULL THEN
        JSON_SET(
          content,
          '$.raw_response', JSON_QUERY(content, '$.response'),
          '$.text_summary', answer_text,
          '$.response', answer_text
        )
      ELSE content
    END AS content,
    JSON_SET(
      COALESCE(attributes, JSON '{}'),
      '$.root_agent_name',
      JSON_VALUE(attributes, '$.adk.app_name')
    ) AS attributes
  )
FROM allowlisted;
```

After creating the compatibility view, initialize the SDK `Client` . You can optionally run `client.doctor()` to validate your table schema and event coverage:

```
from datetime import datetime, timedelta, timezone
from bigquery_agent_analytics import Client, TraceFilter

client = Client(
    project_id="PROJECT_ID",
    dataset_id="ANALYTICS_DATASET",
    table_id="v_bqca_sdk_events",
    location="LOCATION",
)

# Optionally run diagnostic checks over recent partitions:
report = client.doctor(
    filters=TraceFilter(start_time=datetime.now(timezone.utc) - timedelta(days=7))
)
print(report)
```

The `client.doctor()` function returns a dictionary that validates the table schema and compares event coverage against standard Agent Development Kit (ADK) event types. Because the `v_bqca_sdk_events` compatibility view exposes only allowlisted conversational analytics event types, warnings about missing `AGENT_COMPLETED` , `AGENT_STARTING` , `LLM_REQUEST` , `TOOL_COMPLETED` , or `TOOL_STARTING` events are expected. An error or a missing column warning means that the `Client` parameters don't match where the view was created or you lack read access to the dataset, while an empty `event_coverage` result means that the view has no conversations from the last 7 days.

For more information about using the SDK to evaluate agent quality, reconstruct traces, and monitor drift, see [Use the BigQuery agent analytics SDK](https://docs.cloud.google.com/bigquery/docs/bigquery-agent-analytics#use-the-sdk) and the interactive Colab notebook linked in this section.

## SQL recipes

In the following GoogleSQL queries, use the same `PROJECT_ID` , `LOG_DATASET` , `LOG_TABLE` , and `ANALYTICS_DATASET` placeholders described in [Use the Colab notebook and Python SDK](https://docs.cloud.google.com/bigquery/docs/analyze-conversation-logs#conversation-logging-colab-sdk) .

Start with [Create the cross-agent events view ( `v_ca_events` )](https://docs.cloud.google.com/bigquery/docs/analyze-conversation-logs#recipe-cross-agent-events-view) and [Create the turns table function ( `ca_turns` )](https://docs.cloud.google.com/bigquery/docs/analyze-conversation-logs#recipe-turns-table-function) . Most of the following queries use the `ca_turns` table function or the `v_ca_events` view; the `AI.GENERATE` error-summary query and the deduplication query read the log table directly.

### Create the cross-agent events view ( `v_ca_events` )

This view returns one row per event, with agent ID, conversation ID, question, answer text, insights, tokens, and latency as plain columns. Filters on `timestamp` pass through to the log table, so partition pruning still works. The view doesn't remove duplicate events; write retries are rare, but if you want to inspect or filter duplicate events by `event_id` , see [Remove duplicate rows](https://docs.cloud.google.com/bigquery/docs/analyze-conversation-logs#recipe-deduplicate-events) :

```
CREATE OR REPLACE VIEW `PROJECT_ID.ANALYTICS_DATASET.v_ca_events` AS
SELECT
  timestamp,
  DATE(timestamp) AS event_date,
  event_id,
  event_type,
  status,
  error_message,
  user_id,
  COALESCE(NULLIF(user_id, ''), JSON_VALUE(attributes, '$.session_metadata.user_id')) AS internal_user_key,
  JSON_VALUE(attributes, '$.session_metadata.state."data-agent-id"') AS data_agent_id,
  JSON_VALUE(attributes, '$.adk.app_name') AS data_agent_resource_name,
  JSON_VALUE(attributes, '$.session_metadata.state."conversation-id"') AS conversation_id,
  session_id AS turn_id,
  invocation_id,
  IF(event_type = 'USER_MESSAGE_RECEIVED', JSON_VALUE(content, '$.text_summary'), NULL) AS user_question,
  IF(event_type = 'AGENT_RESPONSE',
    COALESCE(
      NULLIF(JSON_VALUE(content, '$.text_summary'), ''),
      NULLIF(ARRAY_TO_STRING(ARRAY(
        SELECT JSON_VALUE(p, '$.markdown')
        FROM UNNEST(JSON_QUERY_ARRAY(content, '$.response.parts')) AS p WITH OFFSET AS o
        WHERE JSON_VALUE(p, '$.markdown') IS NOT NULL
        ORDER BY o), '\n\n'), ''),
      NULLIF(JSON_VALUE(content, '$.response.clarifying_question'), ''),
      JSON_VALUE(content, '$.response')),
    NULL) AS agent_response,
  IF(event_type = 'AGENT_RESPONSE',
    NULLIF(ARRAY_TO_STRING(ARRAY(
      SELECT JSON_VALUE(p, '$.insight')
      FROM UNNEST(JSON_QUERY_ARRAY(content, '$.response.parts')) AS p WITH OFFSET AS o
      WHERE JSON_VALUE(p, '$.insight') IS NOT NULL
      ORDER BY o), '\n'), ''),
    NULL) AS agent_insights,
  IF(event_type = 'AGENT_RESPONSE',
    NULLIF(ARRAY_TO_STRING(ARRAY(
      SELECT JSON_VALUE(p, '$.assumption')
      FROM UNNEST(JSON_QUERY_ARRAY(content, '$.response.parts')) AS p WITH OFFSET AS o
      WHERE JSON_VALUE(p, '$.assumption') IS NOT NULL
      ORDER BY o), '\n'), ''),
    NULL) AS agent_assumptions,
  IF(event_type = 'AGENT_RESPONSE',
    NULLIF(ARRAY_TO_STRING(ARRAY(
      SELECT JSON_VALUE(q)
      FROM UNNEST(JSON_QUERY_ARRAY(content, '$.response.followup_questions')) AS q WITH OFFSET AS o
      WHERE JSON_VALUE(q) IS NOT NULL
      ORDER BY o), '\n'), ''),
    NULL) AS followup_questions,
  IF(event_type = 'AGENT_RESPONSE',
    NULLIF(ARRAY_TO_STRING(ARRAY(
      SELECT artifact_name
      FROM UNNEST(JSON_QUERY_ARRAY(content, '$.response.parts')) AS p WITH OFFSET AS o,
        UNNEST([JSON_VALUE(p, '$.data_result_artifact_name'), JSON_VALUE(p, '$.chart_artifact_name')]) AS artifact_name WITH OFFSET AS a_o
      WHERE artifact_name IS NOT NULL
      ORDER BY o, a_o), ', '), ''),
    NULL) AS result_artifact_names,
  IF(event_type = 'LLM_RESPONSE', JSON_VALUE(attributes, '$.model_version'), NULL) AS model_version,
  IF(event_type = 'LLM_RESPONSE', SAFE_CAST(JSON_VALUE(content, '$.usage.prompt') AS INT64), NULL) AS prompt_tokens,
  IF(event_type = 'LLM_RESPONSE', SAFE_CAST(JSON_VALUE(content, '$.usage.completion') AS INT64), NULL) AS completion_tokens,
  IF(event_type = 'LLM_RESPONSE', SAFE_CAST(JSON_VALUE(content, '$.usage.total') AS INT64), NULL) AS total_tokens,
  IF(event_type = 'LLM_RESPONSE', SAFE_CAST(JSON_VALUE(attributes, '$.usage_metadata.thoughts_token_count') AS INT64), NULL) AS thoughts_tokens,
  IF(event_type = 'INVOCATION_COMPLETED', SAFE_CAST(JSON_VALUE(latency_ms, '$.total_ms') AS INT64), NULL) AS turn_latency_ms,
  is_truncated,
  trace_id,
  span_id,
  parent_span_id
FROM `PROJECT_ID.LOG_DATASET.LOG_TABLE`;
```

### Create the turns table function ( `ca_turns` ): one row per question and answer

This table function takes a time window and returns one row per turn. Because it applies the time filter to the log table, you pay only for the days that you ask for:

```
CREATE OR REPLACE TABLE FUNCTION `PROJECT_ID.ANALYTICS_DATASET.ca_turns`(start_ts TIMESTAMP, end_ts TIMESTAMP) AS
SELECT
  turn_id,
  MIN(timestamp) AS turn_start,
  MAX(timestamp) AS turn_end,
  DATE(MIN(timestamp)) AS turn_date,
  NULLIF(MAX(user_id), '') AS user_id,
  MAX(internal_user_key) AS internal_user_key,
  MAX(data_agent_id) AS data_agent_id,
  MAX(conversation_id) AS conversation_id,
  ARRAY_AGG(user_question IGNORE NULLS ORDER BY timestamp, event_id LIMIT 1)[SAFE_OFFSET(0)] AS user_question,
  ARRAY_AGG(agent_response IGNORE NULLS ORDER BY timestamp DESC, event_id DESC LIMIT 1)[SAFE_OFFSET(0)] AS agent_response,
  ARRAY_AGG(agent_insights IGNORE NULLS ORDER BY timestamp DESC, event_id DESC LIMIT 1)[SAFE_OFFSET(0)] AS agent_insights,
  ARRAY_AGG(agent_assumptions IGNORE NULLS ORDER BY timestamp DESC, event_id DESC LIMIT 1)[SAFE_OFFSET(0)] AS agent_assumptions,
  ARRAY_AGG(followup_questions IGNORE NULLS ORDER BY timestamp DESC, event_id DESC LIMIT 1)[SAFE_OFFSET(0)] AS followup_questions,
  ARRAY_AGG(result_artifact_names IGNORE NULLS ORDER BY timestamp DESC, event_id DESC LIMIT 1)[SAFE_OFFSET(0)] AS result_artifact_names,
  MAX(turn_latency_ms) AS turn_latency_ms,
  SUM(total_tokens) AS total_tokens,
  COUNTIF(status = 'ERROR') AS error_events,
  LOGICAL_OR(IFNULL(is_truncated, FALSE)) AS any_truncated
FROM `PROJECT_ID.ANALYTICS_DATASET.v_ca_events`
WHERE timestamp >= start_ts
  AND timestamp < end_ts
  AND turn_id IS NOT NULL
GROUP BY turn_id;
```

### Every question and answer for one user (last 30 days)

Set `target_user` to the user's email address, or to the internal key for callers without an email address:

```
DECLARE target_user STRING DEFAULT 'analyst@example.com';

SELECT turn_start, data_agent_id, conversation_id, user_question, agent_response, agent_insights
FROM `PROJECT_ID.ANALYTICS_DATASET.ca_turns`(
  TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 30 DAY), CURRENT_TIMESTAMP())
WHERE user_id = target_user
   OR internal_user_key = target_user
ORDER BY turn_start;
```

### Sample questions and answers across all agents for review

This query returns about 10% of the turns from the last 24 hours. Change `0.10` to set your review rate:

```
SELECT data_agent_id, turn_start, user_question, agent_response, agent_assumptions
FROM `PROJECT_ID.ANALYTICS_DATASET.ca_turns`(
  TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 1 DAY), CURRENT_TIMESTAMP())
WHERE user_question IS NOT NULL
  AND RAND() < 0.10
ORDER BY data_agent_id, turn_start;
```

### Adoption by day

The `internal_user_key` field falls back to `attributes.session_metadata.user_id` when `user_id` is `NULL` (for example, for some federated identities), so daily user counts stay consistent per person:

```
SELECT
  turn_date,
  COUNT(DISTINCT internal_user_key) AS active_users,
  COUNT(DISTINCT data_agent_id) AS active_agents,
  COUNT(DISTINCT conversation_id) AS conversations,
  COUNT(*) AS questions
FROM `PROJECT_ID.ANALYTICS_DATASET.ca_turns`(
  TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 30 DAY), CURRENT_TIMESTAMP())
GROUP BY turn_date
ORDER BY turn_date DESC;
```

### Adoption by user: agents, conversations, and questions per person

To count distinct agents, conversations, and questions per user over the last 30 days, run the following query:

```
SELECT
  t.internal_user_key,
  COUNT(DISTINCT t.data_agent_id) AS agents_used,
  COUNT(DISTINCT t.conversation_id) AS conversations,
  COUNT(*) AS questions,
  MIN(t.turn_start) AS first_seen,
  MAX(t.turn_start) AS last_seen
FROM `PROJECT_ID.ANALYTICS_DATASET.ca_turns`(
  TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 30 DAY), CURRENT_TIMESTAMP()) AS t
GROUP BY internal_user_key
ORDER BY questions DESC;
```

### Adoption and health by agent

To compare users, conversations, question volume, average latency, error rate, and total tokens across all data agents in your project, run the following query:

```
SELECT
  data_agent_id,
  COUNT(DISTINCT internal_user_key) AS users,
  COUNT(DISTINCT conversation_id) AS conversations,
  COUNT(*) AS questions,
  ROUND(AVG(turn_latency_ms)) AS avg_turn_latency_ms,
  ROUND(100 * SAFE_DIVIDE(COUNTIF(error_events > 0), COUNT(*)), 2) AS pct_turns_with_errors,
  SUM(total_tokens) AS total_tokens
FROM `PROJECT_ID.ANALYTICS_DATASET.ca_turns`(
  TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 30 DAY), CURRENT_TIMESTAMP())
GROUP BY data_agent_id
ORDER BY questions DESC;
```

### Conversation summaries

To roll up multi-turn conversations over the last 7 days, run the following query:

```
SELECT
  conversation_id,
  MAX(data_agent_id) AS data_agent_id,
  MAX(internal_user_key) AS internal_user_key,
  COUNT(*) AS turns,
  MIN(turn_start) AS started_at,
  TIMESTAMP_DIFF(MAX(turn_end), MIN(turn_start), SECOND) AS duration_seconds,
  ARRAY_AGG(user_question IGNORE NULLS ORDER BY turn_start LIMIT 1)[SAFE_OFFSET(0)] AS first_question
FROM `PROJECT_ID.ANALYTICS_DATASET.ca_turns`(
  TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 7 DAY), CURRENT_TIMESTAMP())
WHERE conversation_id IS NOT NULL
GROUP BY conversation_id
ORDER BY started_at DESC
LIMIT 100;
```

### Token use by model and by agent (last 7 days)

To break down model call counts and token usage (including thinking tokens) by date, `data_agent_id` , and `model_version` over the last 7 days, query `v_ca_events` for `LLM_RESPONSE` rows:

```
SELECT
  event_date,
  data_agent_id,
  model_version,
  COUNT(*) AS model_calls,
  SUM(prompt_tokens) AS prompt_tokens,
  SUM(completion_tokens) AS completion_tokens,
  SUM(thoughts_tokens) AS thoughts_tokens,  -- thinking tokens, already included in total_tokens
  SUM(total_tokens) AS total_tokens
FROM `PROJECT_ID.ANALYTICS_DATASET.v_ca_events`
WHERE event_type = 'LLM_RESPONSE'
  AND timestamp >= TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 7 DAY)
GROUP BY event_date, data_agent_id, model_version
ORDER BY event_date DESC, total_tokens DESC;
```

### Errors by agent, with AI-assisted root-cause summaries

To check error counts by agent and day over the last 7 days, run the following query:

```
SELECT
  event_date,
  data_agent_id,
  COUNT(*) AS error_events,
  COUNT(DISTINCT turn_id) AS turns_with_errors,
  ANY_VALUE(error_message) AS sample_error
FROM `PROJECT_ID.ANALYTICS_DATASET.v_ca_events`
WHERE status = 'ERROR'
  AND timestamp >= TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 7 DAY)
GROUP BY event_date, data_agent_id
ORDER BY event_date DESC, error_events DESC;
```

To summarize the root cause of recent errors, use the [`AI.GENERATE`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate) function.

> **Caution:** This query sends error messages from your logs to a Gemini model on Gemini Enterprise Agent Platform in your project. Check your data-governance policy first. The person running the query needs the Agent Platform User ( `roles/aiplatform.user` ) role, or you can use a BigQuery connection that has it.

The CTE caps the rows before the model is called, so cost stays predictable:

```
WITH recent_errors AS (
  SELECT
    timestamp,
    JSON_VALUE(attributes, '$.session_metadata.state."data-agent-id"') AS data_agent_id,
    session_id AS turn_id,
    error_message
  FROM `PROJECT_ID.LOG_DATASET.LOG_TABLE`
  WHERE status = 'ERROR'
    AND timestamp >= TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 1 DAY)
  ORDER BY timestamp DESC
  LIMIT 10
)
SELECT
  timestamp,
  data_agent_id,
  turn_id,
  error_message,
  AI.GENERATE(
    CONCAT(
      'Analyze this BigQuery Conversational Analytics error log and summarize the likely root cause in two sentences. Error: ',
      IFNULL(error_message, '(none)'))
  ).result AS ai_root_cause_summary
FROM recent_errors;
```

### Remove duplicate rows

This step is optional. A retried write can occasionally produce the same event twice. The following query demonstrates how to select unique rows per `event_id` for the last 24 hours:

```
SELECT * EXCEPT (row_num)
FROM (
  SELECT
    *,
    ROW_NUMBER() OVER (
      PARTITION BY event_id
      ORDER BY timestamp) AS row_num
  FROM `PROJECT_ID.LOG_DATASET.LOG_TABLE`
  WHERE timestamp >= TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 1 DAY)
)
WHERE row_num = 1 OR event_id IS NULL;
```

## Troubleshoot conversation logging

If your conversation log table is missing, empty, or missing turns from specific users, or if you encounter destination validation errors, see [Troubleshoot conversation logging](https://docs.cloud.google.com/bigquery/docs/troubleshoot-workload-management#troubleshoot-conversation-logging) .

## What's next

- [Review the conversation log schema](https://docs.cloud.google.com/bigquery/docs/conversation-log-schema) .

- [Read the conversation logging overview](https://docs.cloud.google.com/bigquery/docs/conversation-logging-overview) .

- [Create and configure data agents](https://docs.cloud.google.com/bigquery/docs/create-data-agents#configure_settings) .
