---
name: documents/docs.cloud.google.com/bigquery/docs/reference/migration/mcp
uri: https://docs.cloud.google.com/bigquery/docs/reference/migration/mcp
title: 'MCP Reference: bigquerymigration.googleapis.com'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

BigQuery Migration MCP server provides tools to work with BigQuery Migration Services, such as [SQL translation](https://docs.cloud.google.com/bigquery/docs/api-sql-translator) .

A [Model Context Protocol (MCP) server](https://modelcontextprotocol.io/docs/learn/server-concepts) acts as a proxy between an external service that provides context, data, or capabilities to a Large Language Model (LLM) or AI application. MCP servers connect AI applications to external systems such as databases and web services, translating their responses into a format that the AI application can understand.

### Server Setup

You must [enable MCP servers](https://docs.cloud.google.com/mcp/enable-disable-mcp-servers) and [set up authentication](https://docs.cloud.google.com/mcp/authenticate-mcp) before use. For more information about using Google and Google Cloud remote MCP servers, see [Google Cloud MCP servers overview](https://docs.cloud.google.com/mcp/overview) .

### Server Endpoints

An MCP service endpoint is the network address and communication interface (usually a URL) of the MCP server that an AI application (the Host for the MCP client) uses to establish a secure, standardized connection. It is the point of contact for the LLM to request context, call a tool, or access a resource. Google MCP endpoints can be global or regional.

The BigQuery Migration API MCP server has the following global MCP endpoint:

  - https://bigquerymigration.googleapis.com/mcp

## MCP Tools

An [MCP tool](https://modelcontextprotocol.io/legacy/concepts/tools) is a function or executable capability that an MCP server exposes to a LLM or AI application to perform an action in the real world.

### Tools

The bigquerymigration.googleapis.com MCP server has the following tools:

MCP Tools

`  translate_query  `

Translates a single query into BigQuery SQL syntax.

`  get_translation  `

Gets the SQL translation for a given translation ID.

`  explain_translation  `

Explains the SQL translation for a given translation ID.

`  generate_ddl_suggestion  `

Suggests Data Definition Language (DDL) statements for an input query. For example, `CREATE TABLE` or `CREATE VIEW` . The generated DDL provides schema definitions for tables and views that are used in the query. To get DDL suggestions, call this tool, and then use the `fetch_ddl_suggestion` tool with the returned suggestion ID to retrieve the DDL. You can then prepend the retrieved DDL to the original input query and translate it again to improve translation quality.

`  fetch_ddl_suggestion  `

Fetches DDL suggestion for a given suggestion ID.

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
<td><pre dir="ltr" data-is-upgraded="" data-syntax="Bash" translate="no"><code>                      
curl --location &#39;https://bigquerymigration.googleapis.com/mcp&#39; \
--header &#39;content-type: application/json&#39; \
--header &#39;accept: application/json, text/event-stream&#39; \
--data &#39;{
    &quot;method&quot;: &quot;tools/list&quot;,
    &quot;jsonrpc&quot;: &quot;2.0&quot;,
    &quot;id&quot;: 1
}&#39;
                    </code></pre></td>
</tr>
</tbody>
</table>
