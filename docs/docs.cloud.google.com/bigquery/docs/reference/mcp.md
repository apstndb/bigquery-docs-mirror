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

MCP Tools

`  list_dataset_ids  `

List BigQuery dataset IDs and BigLake namespaces in a Google Cloud project. Supports pagination. Use `page_size` to limit results and `page_token` to retrieve next page.

`  get_dataset_info  `

Get metadata information about a BigQuery dataset or BigLake namespace.

`  list_table_ids  `

List table ids in a BigQuery dataset or BigLake namespace. Supports pagination. Use `page_size` to limit results and `page_token` to retrieve next page.

`  get_table_info  `

Get metadata information about a BigQuery table or BigLake table.

`  execute_sql_readonly  `

Run a read-only SQL query in the project and return the result. Prefer this tool over `execute_sql` if possible.

This tool is restricted to only `SELECT` statements. `INSERT` , `UPDATE` , and `DELETE` statements and stored procedures aren't allowed. If the query doesn't include a `SELECT` statement, an error is returned. For information on creating queries, see the [GoogleSQL documentation](https://cloud.google.com/bigquery/docs/reference/standard-sql/query-syntax) .

Example Queries:

```sql
-- Count the number of penguins in each island.
SELECT island, COUNT(*) AS population
FROM bigquery-public-data.ml_datasets.penguins GROUP BY island

-- Evaluate a bigquery ML Model.
SELECT * FROM ML.EVALUATE(MODEL `my_dataset.my_model`)

-- Evaluate BigQuery ML model on custom data
SELECT *
FROM ML.EVALUATE(MODEL `my_dataset.my_model`, (SELECT * FROM `my_dataset.my_table`))

-- Predict using BigQuery ML model:
SELECT *
FROM ML.PREDICT(MODEL `my_dataset.my_model`, (SELECT * FROM `my_dataset.my_table`))

-- Forecast data using AI.FORECAST
SELECT *
FROM AI.FORECAST(TABLE `project.dataset.my_table`, data_col => 'num_trips',
  timestamp_col => 'date', id_cols => ['usertype'], horizon => 30)
```

Queries executed using the `execute_sql_readonly` tool will always have the job label `goog-mcp-server: true` automatically set in addition to any custom `labels` provided in the request. Queries are charged to the project specified in the `project_id` field.

`  execute_sql  `

Run a SQL query in the project and return the result. Prefer the `execute_sql_readonly` tool if possible.

This tool can execute any query that bigquery supports including:

  - SQL Queries ( `SELECT` , `INSERT` , `UPDATE` , `DELETE` , `CREATE` , etc.)
  - AI/ML functions like `AI.FORECAST` , `ML.EVALUATE` , `ML.PREDICT`
  - Any other query that bigquery supports.

Example Queries:

```sql
-- Insert data into a table.
INSERT INTO `my_project.my_dataset`.my_table (name, age)
VALUES ('Alice', 30);

-- Create a table.
CREATE TABLE `my_project.my_dataset`.my_table (
  name STRING,
  age INT64);

-- DELETE data from a table.
DELETE FROM `my_project.my_dataset`.my_table WHERE name = 'Alice';

-- Create Dataset
CREATE SCHEMA `my_project.my_dataset` OPTIONS (location = 'US');

-- Drop table
DROP TABLE `my_project.my_dataset`.my_table;

-- Drop dataset
DROP SCHEMA `my_project.my_dataset`;

-- Create Model
CREATE OR REPLACE MODEL `my_project.my_dataset.my_model`
OPTIONS (
  model_type = 'LINEAR_REG'
  LS_INIT_LEARN_RATE=0.15,
  L1_REG=1,
  MAX_ITERATIONS=5,
  DATA_SPLIT_METHOD='SEQ',
  DATA_SPLIT_EVAL_FRACTION=0.3,
  DATA_SPLIT_COL='timestamp') AS
SELECT col1, col2, timestamp, label FROM `my_project.my_dataset.my_table`;
```

Queries executed using the `execute_sql` tool will always have the default job label `goog-mcp-server: true` automatically set in addition to any custom `labels` provided in the request. Queries are charged to the project specified in the `project_id` field.

### Get MCP tool specifications

To get the MCP tool specifications for all tools in an MCP server, use the `tools/list` method. The following example demonstrates how to use `curl` to list all tools and their specifications currently available within the MCP server.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Curl Request</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" data-syntax="Bash" translate="no"><code>curl --location &#39;https://bigquery.googleapis.com/mcp&#39; \
--header &#39;content-type: application/json&#39; \
--header &#39;accept: application/json, text/event-stream&#39; \
--data &#39;{
    &quot;method&quot;: &quot;tools/list&quot;,
    &quot;jsonrpc&quot;: &quot;2.0&quot;,
    &quot;id&quot;: 1
}&#39;</code></pre></td>
</tr>
</tbody>
</table>
