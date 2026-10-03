---
name: documents/docs.cloud.google.com/bigquery/docs/reference/mcp
uri: https://docs.cloud.google.com/bigquery/docs/reference/mcp
title: 'MCP Reference: bigquery.googleapis.com'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

BigQuery MCP server provides tools to interact with BigQuery

A [Model Context Protocol (MCP) server](https://modelcontextprotocol.io/docs/learn/server-concepts) acts as a proxy between an external service that provides context, data, or capabilities to a Large Language Model (LLM) or AI application. MCP servers connect AI applications to external systems such as databases and web services, translating their responses into a format that the AI application can understand.

### Server Setup

You must [enable MCP servers](https://docs.cloud.google.com/mcp/enable-disable-mcp-servers) and [set up authentication](https://docs.cloud.google.com/mcp/authenticate-mcp) before use. For more information about using Google and Google Cloud remote MCP servers, see [Google Cloud MCP servers overview](https://docs.cloud.google.com/mcp/overview) .

### Server Endpoints

An MCP service endpoint is the network address and communication interface (usually a URL) of the MCP server that an AI application (the Host for the MCP client) uses to establish a secure, standardized connection. It is the point of contact for the LLM to request context, call a tool, or access a resource. Google MCP endpoints can be global or regional.

The BigQuery API MCP server has the following global MCP endpoint:

- https://bigquery.googleapis.com/mcp

## MCP Tools

An [MCP tool](https://modelcontextprotocol.io/legacy/concepts/tools) is a function or executable capability that an MCP server exposes to a LLM or AI application to perform an action in the real world.

### Tools

The bigquery.googleapis.com MCP server has the following tools:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>MCP Tools</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/list_dataset_ids"><code>list_dataset_ids</code></a></td>
<td>List BigQuery dataset IDs and BigLake namespaces in a Google Cloud project. Supports pagination. Use <code>page_size</code> to limit results and <code>page_token</code> to retrieve next page.</td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info"><code>get_dataset_info</code></a></td>
<td>Get metadata information about a BigQuery dataset or BigLake namespace.</td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/list_table_ids"><code>list_table_ids</code></a></td>
<td>List table ids in a BigQuery dataset or BigLake namespace. Supports pagination. Use <code>page_size</code> to limit results and <code>page_token</code> to retrieve next page.</td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info"><code>get_table_info</code></a></td>
<td>Get metadata information about a BigQuery table or BigLake table.</td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/execute_sql_readonly"><code>execute_sql_readonly</code></a></td>
<td><p>Run a read-only SQL query in the project and return the result. Prefer this tool over <code>execute_sql</code> if possible.</p>
<p>This tool is restricted to only <code>SELECT</code> statements. <code>INSERT</code> , <code>UPDATE</code> , and <code>DELETE</code> statements and stored procedures aren't allowed. If the query doesn't include a <code>SELECT</code> statement, an error is returned. For information on creating queries, see the <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/query-syntax">GoogleSQL documentation</a> .</p>
<p>IMPORTANT: For predictive and analytical tasks (forecasting, anomaly detection, key driver / root cause analysis, classification, churn prediction, or text generation), ALWAYS execute computation in-warehouse using BigQuery native AI/ML functions ( <code>AI.FORECAST</code> , <code>AI.DETECT_ANOMALIES</code> , <code>AI.KEY_DRIVERS</code> , <code>AI.CLASSIFY</code> , <code>AI.GENERATE</code> ) rather than exporting raw rows to a local Python sandbox. In-warehouse execution scales to billions of rows, preserves governance, and eliminates data egress latency.</p>
<p>Example Queries:</p>
<pre class="sql"><code>-- Count the number of penguins in each island.
SELECT island, COUNT(*) AS population
FROM bigquery-public-data.ml_datasets.penguins GROUP BY island

-- Forecast data using AI.FORECAST
SELECT *
FROM AI.FORECAST(TABLE `project.dataset.my_table`, data_col =&gt; &#39;num_trips&#39;,
  timestamp_col =&gt; &#39;date&#39;, id_cols =&gt; [&#39;usertype&#39;], horizon =&gt; 30)

-- Detect anomalies in time series data using AI.DETECT_ANOMALIES
SELECT *
FROM AI.DETECT_ANOMALIES(
  TABLE `project.dataset.historical_metrics`,
  TABLE `project.dataset.recent_metrics`,
  data_col =&gt; &#39;num_requests&#39;,
  timestamp_col =&gt; &#39;timestamp&#39;
)

-- Identify key drivers of metric changes using AI.KEY_DRIVERS
SELECT *
FROM AI.KEY_DRIVERS(
  TABLE `project.dataset.sales_summary`,
  metric_col =&gt; &#39;total_revenue&#39;,
  dimension_cols =&gt; [&#39;region&#39;, &#39;product_category&#39;],
  interest_label_col =&gt; &#39;is_current_quarter&#39;
)

-- Classify text into categories using AI.CLASSIFY
SELECT
  ticket_id,
  AI.CLASSIFY(ticket_text, [&#39;Billing&#39;, &#39;Technical Support&#39;, &#39;Feature Request&#39;]) AS category
FROM `project.dataset.support_tickets`

-- Generate text or summaries using AI.GENERATE
SELECT
  review_id,
  AI.GENERATE(CONCAT(&#39;Summarize this customer review: &#39;, review_text)).result AS summary
FROM `project.dataset.reviews`</code></pre>
<p>Queries executed using the <code>execute_sql_readonly</code> tool will always have the job label <code>goog-mcp-server: true</code> automatically set in addition to any custom <code>labels</code> provided in the request. Queries are charged to the project specified in the <code>project_id</code> field.</p>
<p>Query Execution Behavior: * If the query completes within the synchronous timeout (default 20 seconds or custom <code>timeout_ms</code> ), the tool returns <code>job_complete: true</code> and the result rows directly. For fast queries, <code>job_id</code> may be omitted as no persistent background job is created; no further action or polling is needed. * If the query takes longer than <code>timeout_ms</code> , the tool returns <code>job_complete: false</code> and a <code>job_id</code> . In this case, use the <code>get_query_results</code> tool with <code>job_id</code> to poll until <code>job_complete: true</code> , or use <code>cancel_job</code> to abort the running query. * You can optionally specify <code>timeout_ms</code> to configure the maximum synchronous wait time in milliseconds (defaults to 20,000 ms), and <code>job_timeout_ms</code> to enforce a hard server-side timeout after which BigQuery automatically terminates the job.</p></td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/execute_sql"><code>execute_sql</code></a></td>
<td><p>Run a SQL query in the project and return the result. Prefer the <code>execute_sql_readonly</code> tool if possible.</p>
<p>This tool can execute any query that bigquery supports including:</p>
<ul>
<li>SQL Queries ( <code>SELECT</code> , <code>INSERT</code> , <code>UPDATE</code> , <code>DELETE</code> , <code>CREATE</code> , etc.)</li>
<li>AI/ML functions like <code>AI.FORECAST</code> , <code>AI.KEY_DRIVERS</code> , <code>ML.EVALUATE</code> , <code>ML.PREDICT</code></li>
<li>Any other query that bigquery supports.</li>
</ul>
<p>Example Queries:</p>
<pre class="sql"><code>-- Insert data into a table.
INSERT INTO `my_project.my_dataset`.my_table (name, age)
VALUES (&#39;Alice&#39;, 30);

-- Create a table.
CREATE TABLE `my_project.my_dataset`.my_table (
  name STRING,
  age INT64);

-- DELETE data from a table.
DELETE FROM `my_project.my_dataset`.my_table WHERE name = &#39;Alice&#39;;

-- Create Dataset
CREATE SCHEMA `my_project.my_dataset` OPTIONS (location = &#39;US&#39;);

-- Drop table
DROP TABLE `my_project.my_dataset`.my_table;

-- Drop dataset
DROP SCHEMA `my_project.my_dataset`;

-- Create Model
CREATE OR REPLACE MODEL `my_project.my_dataset.my_model`
OPTIONS (
  model_type = &#39;LINEAR_REG&#39;
  LS_INIT_LEARN_RATE=0.15,
  L1_REG=1,
  MAX_ITERATIONS=5,
  DATA_SPLIT_METHOD=&#39;SEQ&#39;,
  DATA_SPLIT_EVAL_FRACTION=0.3,
  DATA_SPLIT_COL=&#39;timestamp&#39;) AS
SELECT col1, col2, timestamp, label FROM `my_project.my_dataset.my_table`;</code></pre>
<p>Queries executed using the <code>execute_sql</code> tool will always have the default job label <code>goog-mcp-server: true</code> automatically set in addition to any custom <code>labels</code> provided in the request. Queries are charged to the project specified in the <code>project_id</code> field.</p>
<p>Query Execution Behavior: * If the query completes within the synchronous timeout (default 20 seconds or custom <code>timeout_ms</code> ), the tool returns <code>job_complete: true</code> and the initial result rows directly. For fast queries, <code>job_id</code> may be omitted as no persistent background job is created; no further action or polling is needed. * If the query takes longer than <code>timeout_ms</code> , the tool returns <code>job_complete: false</code> and a <code>job_id</code> . In this case, use the <code>get_query_results</code> tool with <code>job_id</code> to poll until <code>job_complete: true</code> , or use <code>cancel_job</code> to abort the running query. * You can optionally specify <code>timeout_ms</code> to configure the maximum synchronous wait time in milliseconds (defaults to 20,000 ms), and <code>job_timeout_ms</code> to enforce a hard server-side timeout after which BigQuery automatically terminates the job.</p></td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_query_results"><code>get_query_results</code></a></td>
<td><p>Get the results of a BigQuery SQL query job.</p>
<p>Use this tool ONLY when: 1. A previous <code>execute_sql</code> or <code>execute_sql_readonly</code> call returned <code>job_complete: false</code> with a <code>job_id</code> (poll with this tool until <code>job_complete: true</code> ), OR 2. You need to paginate through additional rows using <code>page_token</code> or <code>start_index</code> for a previously completed job.</p>
<p>Do NOT call this tool if the query already returned <code>job_complete: true</code> with all rows.</p>
<p>Supports pagination. Use <code>max_results</code> to limit results and <code>page_token</code> to retrieve the next page of results.</p></td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job"><code>cancel_job</code></a></td>
<td><p>Cancel a running BigQuery job.</p>
<p>Use this tool to cancel a query job that is currently executing (i.e. returned <code>job_complete: false</code> with a <code>job_id</code> from <code>execute_sql</code> or <code>execute_sql_readonly</code> ). Specify the <code>job_id</code> to abort.</p></td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_job"><code>get_job</code></a></td>
<td><p>Get information and status about a BigQuery job.</p>
<p>Use this tool to check the status, statistics, or configuration of a job using its <code>job_id</code> .</p></td>
</tr>
</tbody>
</table>

### Get MCP tool specifications

To get the MCP tool specifications for all tools in an MCP server, use the `tools/list` method. The following example demonstrates how to use `curl` to list all tools and their specifications currently available within the MCP server.

**Curl Request**

```
curl --location 'https://bigquery.googleapis.com/mcp' \
--header 'content-type: application/json' \
--header 'accept: application/json, text/event-stream' \
--data '{
    "method": "tools/list",
    "jsonrpc": "2.0",
    "id": 1
}'
```
