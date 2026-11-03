---
name: documents/docs.cloud.google.com/bigquery/docs/conversation-log-schema
uri: https://docs.cloud.google.com/bigquery/docs/conversation-log-schema
title: Conversation log schema
description: Reference for the conversational analytics conversation logging destination table schema, event types, and JSON fields in BigQuery.
data_source: docs.cloud.google.com
---

# Conversation log schema

This document describes the table layout, columns, event types, user identity fields, and JSON payload structure for conversational analytics conversation logging in BigQuery. For an overview of how conversation logging works, see [Conversation logging overview](https://docs.cloud.google.com/bigquery/docs/conversation-logging-overview) .

## Table layout and auto-creation

Create the destination dataset in the same project as the data agent before enabling logging; the Conversational Analytics API service agent creates the table in the dataset's location on the first logged turn (or adds any missing schema columns to an existing compatible table). The auto-created table is partitioned by day on `timestamp` (inheriting any default partition expiration on the dataset) and clustered on `event_type` , `agent` , and `user_id` . Always filter on `timestamp` when you query the table.

## Columns

The following table describes the columns in the conversation logging destination table.

| Column           | Type        | Mode       | Contents                                                                                                                                                                                                                                                                          |
|------------------|-------------|------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `timestamp`      | `TIMESTAMP` | `REQUIRED` | UTC time of the event. Partitioning column.                                                                                                                                                                                                                                       |
| `event_id`       | `STRING`    | `NULLABLE` | Unique ID for the event. It stays the same if a write is retried, so you can use it to remove duplicates.                                                                                                                                                                         |
| `event_type`     | `STRING`    | `NULLABLE` | Kind of event. See [Event types](https://docs.cloud.google.com/bigquery/docs/conversation-log-schema#conversation-logging-event-types) .                                                                                                                                          |
| `agent`          | `STRING`    | `NULLABLE` | The agent type, not your agent's name or ID (for example, `ConversationalAnalyticsAgent` ). To tell agents apart, use the data agent ID (see [Fields inside `attributes`](https://docs.cloud.google.com/bigquery/docs/conversation-log-schema#conversation-logging-attributes) ). |
| `session_id`     | `STRING`    | `NULLABLE` | One turn, not a whole conversation. All events for one question and its answer share a `session_id` . To group turns into conversations, use the conversation ID in `attributes` .                                                                                                |
| `invocation_id`  | `STRING`    | `NULLABLE` | One execution within a turn.                                                                                                                                                                                                                                                      |
| `user_id`        | `STRING`    | `NULLABLE` | The caller who asked the question. See [User identity](https://docs.cloud.google.com/bigquery/docs/conversation-log-schema#conversation-logging-user-identity) .                                                                                                                  |
| `trace_id`       | `STRING`    | `NULLABLE` | OpenTelemetry trace ID (32 hexadecimal characters).                                                                                                                                                                                                                               |
| `span_id`        | `STRING`    | `NULLABLE` | ID of this operation in the turn's execution tree.                                                                                                                                                                                                                                |
| `parent_span_id` | `STRING`    | `NULLABLE` | ID of the parent operation.                                                                                                                                                                                                                                                       |
| `content`        | `JSON`      | `NULLABLE` | Event payload. Its shape depends on `event_type` .                                                                                                                                                                                                                                |
| `content_parts`  | `RECORD`    | `REPEATED` | Multi-part content, with one element per part (for example, `mime_type` , `uri` , `object_ref` , `text` , `part_index` , `part_attributes` , and `storage_mode` ).                                                                                                                |
| `attributes`     | `JSON`      | `NULLABLE` | Metadata: data agent ID, conversation ID, internal user key, model version, and detailed token usage.                                                                                                                                                                             |
| `latency_ms`     | `JSON`      | `NULLABLE` | Latency measurements, such as `total_ms` and `time_to_first_token_ms` .                                                                                                                                                                                                           |
| `status`         | `STRING`    | `NULLABLE` | `OK` or `ERROR` .                                                                                                                                                                                                                                                                 |
| `error_message`  | `STRING`    | `NULLABLE` | Error details. It can also be set on `OK` `LLM_RESPONSE` rows when the model stops for a reason other than a normal stop (for example, when it reaches the maximum token limit).                                                                                                  |
| `is_truncated`   | `BOOLEAN`   | `NULLABLE` | `true` if any text value in the event exceeded 512,000 characters ( `500 * 1,024` ) and was cut. Cut values end with `...[TRUNCATED]` . The removed part can't be recovered.                                                                                                      |

## Event types

The following table describes the values that can appear in the `event_type` column and the columns or JSON fields that store the data for each event.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><code>event_type</code> value</th>
<th>Description</th>
<th>Populated columns and JSON fields</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<th><code>INVOCATION_STARTING</code></th>
<td>Start of a turn.</td>
<td>None</td>
</tr>
<tr class="even">
<th><code>USER_MESSAGE_RECEIVED</code></th>
<td>The user's question.</td>
<td><code>content.text_summary</code></td>
</tr>
<tr class="odd">
<th><code>AGENT_RESPONSE</code></th>
<td>The agent's answer, as a structured object.</td>
<td><code>content.text_summary</code> (plain text) and <code>content.response</code> (see <a href="https://docs.cloud.google.com/bigquery/docs/conversation-log-schema#conversation-logging-agent-response">Structure of <code>AGENT_RESPONSE</code></a> )</td>
</tr>
<tr class="even">
<th><code>LLM_RESPONSE</code></th>
<td>One row for each model call, including calls that requested a tool (not written when a turn is answered directly from a verified query, where <code>attributes.fast_path</code> is <code>true</code> ). The model's output isn't stored.</td>
<td><ul>
<li>Tokens: <code>content.usage.prompt</code> , <code>content.usage.completion</code> , and <code>content.usage.total</code> .</li>
<li>Detailed token usage: <code>attributes.usage_metadata</code> , including <code>tool_use_prompt_token_count</code> , <code>thoughts_token_count</code> , and <code>cached_content_token_count</code> .</li>
<li>Total tokens: the <code>content.usage.total</code> value equals the <code>content.usage.prompt</code> + <code>tool_use_prompt_token_count</code> + <code>content.usage.completion</code> + <code>thoughts_token_count</code> values, with the <code>cached_content_token_count</code> value included in the <code>content.usage.prompt</code> value. For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/conversation-log-schema#conversation-logging-attributes">Fields inside <code>attributes</code></a> .</li>
<li>Model: <code>attributes.model_version</code> .</li>
<li>Finish reason: <code>attributes.finish_reason</code> .</li>
</ul></td>
</tr>
<tr class="odd">
<th><code>INVOCATION_COMPLETED</code></th>
<td>End of a turn, with per-turn latency. <code>content</code> is empty.</td>
<td><code>latency_ms.total_ms</code></td>
</tr>
<tr class="even">
<th><code>EMBEDDING_SUGGESTION</code></th>
<td>Suggestions for the agent owner about columns that could benefit from embeddings. It appears only for some agents.</td>
<td><code>content.reason</code> , <code>content.suggested_columns</code></td>
</tr>
<tr class="odd">
<th><code>INVOCATION_ERROR</code> , <code>AGENT_ERROR</code> , <code>LLM_ERROR</code></th>
<td>Failed turn. <code>status</code> is <code>ERROR</code> and <code>content</code> is <code>NULL</code> .</td>
<td><code>error_message</code> (one-line summary with SQL statements and table names redacted)</td>
</tr>
</tbody>
</table>

## User identity

The `user_id` column contains the caller's email address: the user's email address, a service account's email address when an API caller authenticates with a service account, or `NULL` if the caller has no email address (such as some Workforce Identity Federation identities). An internal user key is also recorded in `attributes.session_metadata.user_id` on every row, so you can count distinct users with `internal_user_key` (see [Create the cross-agent events view](https://docs.cloud.google.com/bigquery/docs/analyze-conversation-logs#recipe-cross-agent-events-view) ).

To attribute turns to your own end users when you call the API through a service account, record the user mapping in your application. The API doesn't accept an end-user identifier for logging.

## Fields inside `attributes`

The following table shows the GoogleSQL expressions used to extract metadata fields from the `attributes` JSON column.

| What you need                                   | GoogleSQL expression                                                                         |
|-------------------------------------------------|----------------------------------------------------------------------------------------------|
| Data agent ID                                   | `JSON_VALUE(attributes, '$.session_metadata.state."data-agent-id"')`                         |
| Data agent full resource name                   | `JSON_VALUE(attributes, '$.adk.app_name')`                                                   |
| Conversation ID                                 | `JSON_VALUE(attributes, '$.session_metadata.state."conversation-id"')`                       |
| Internal user key                               | `JSON_VALUE(attributes, '$.session_metadata.user_id')`                                       |
| Model version (on `LLM_RESPONSE` rows)          | `JSON_VALUE(attributes, '$.model_version')`                                                  |
| Tool-use prompt tokens (on `LLM_RESPONSE` rows) | `SAFE_CAST(JSON_VALUE(attributes, '$.usage_metadata.tool_use_prompt_token_count') AS INT64)` |
| Thinking tokens (on `LLM_RESPONSE` rows)        | `SAFE_CAST(JSON_VALUE(attributes, '$.usage_metadata.thoughts_token_count') AS INT64)`        |
| Cached prompt tokens (on `LLM_RESPONSE` rows)   | `SAFE_CAST(JSON_VALUE(attributes, '$.usage_metadata.cached_content_token_count') AS INT64)`  |

On `LLM_RESPONSE` rows, token counts split into the input tokens and the output tokens that add up to the `content.usage.total` value:

- **Input tokens** : the `content.usage.prompt` value plus the `attributes.usage_metadata.tool_use_prompt_token_count` value, which counts tokens from tool execution results that are sent back to the model as input. If you use context caching, the `attributes.usage_metadata.cached_content_token_count` value is already included in the `content.usage.prompt` value.

- **Output tokens** : the `content.usage.completion` value plus the `attributes.usage_metadata.thoughts_token_count` value, which counts reasoning tokens generated by thinking models.

- **Total tokens** : the `content.usage.total` value equals the `content.usage.prompt` + `tool_use_prompt_token_count` + `content.usage.completion` + `thoughts_token_count` values. Optional `usage_metadata` fields are omitted or `null` when a model call doesn't use them. Wrap extracted counts in `COALESCE(..., 0)` before adding row values together (such as `prompt` + `completion` ) or to prevent aggregate functions like `SUM(...)` from producing `null` . For an example query, see [Token use by model and by agent](https://docs.cloud.google.com/bigquery/docs/analyze-conversation-logs#recipe-token-use-by-model) .

## Structure of `AGENT_RESPONSE`

To read the agent's answer as plain text, use `JSON_VALUE(content, '$.text_summary')` . It combines the answer's Markdown, assumption, and insight parts, and any clarifying questions. In `AGENT_RESPONSE` rows, `content.response` is a JSON object, not a string, so `JSON_VALUE(content, '$.response')` returns `NULL` .

The following table describes the paths under `content.response` .

| Path under `content.response`       | Type            | Contents                                                                      |
|-------------------------------------|-----------------|-------------------------------------------------------------------------------|
| `parts`                             | `ARRAY<JSON>`   | The answer, in parts.                                                         |
| `parts[].markdown`                  | `STRING`        | Answer text (Markdown).                                                       |
| `parts[].insight`                   | `STRING`        | An insight drawn from the data.                                               |
| `parts[].assumption`                | `STRING`        | An assumption that the agent made.                                            |
| `parts[].data_result_artifact_name` | `STRING`        | Name of a data result.                                                        |
| `parts[].chart_artifact_name`       | `STRING`        | Name of a chart.                                                              |
| `followup_questions`                | `ARRAY<STRING>` | Suggested follow-up questions.                                                |
| `clarifying_question`               | `STRING`        | Set when the agent asked the user a clarifying question instead of answering. |
| `citation_sources`                  | `JSON`          | Sources cited in the answer.                                                  |

## What's next

- [Analyze conversation logs](https://docs.cloud.google.com/bigquery/docs/analyze-conversation-logs) .

- [Read the conversation logging overview](https://docs.cloud.google.com/bigquery/docs/conversation-logging-overview) .

- [Create and configure data agents](https://docs.cloud.google.com/bigquery/docs/create-data-agents#configure_settings) .
