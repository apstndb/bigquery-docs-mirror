---
name: documents/docs.cloud.google.com/bigquery/docs/reference/datatransfer/mcp
uri: https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/mcp
title: 'MCP Reference: bigquerydatatransfer.googleapis.com'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

BigQuery DTS MCP server provides tools to interact with BigQuery DTS

A [Model Context Protocol (MCP) server](https://modelcontextprotocol.io/docs/learn/server-concepts) acts as a proxy between an external service that provides context, data, or capabilities to a Large Language Model (LLM) or AI application. MCP servers connect AI applications to external systems such as databases and web services, translating their responses into a format that the AI application can understand.

### Server Setup

You must [enable MCP servers](https://docs.cloud.google.com/mcp/enable-disable-mcp-servers) and [set up authentication](https://docs.cloud.google.com/mcp/authenticate-mcp) before use. For more information about using Google and Google Cloud remote MCP servers, see [Google Cloud MCP servers overview](https://docs.cloud.google.com/mcp/overview) .

### Server Endpoints

An MCP service endpoint is the network address and communication interface (usually a URL) of the MCP server that an AI application (the Host for the MCP client) uses to establish a secure, standardized connection. It is the point of contact for the LLM to request context, call a tool, or access a resource. Google MCP endpoints can be global or regional.

The BigQuery Data Transfer API MCP server has the following global MCP endpoint:

- https://bigquerydatatransfer.googleapis.com/mcp

## MCP Tools

An [MCP tool](https://modelcontextprotocol.io/legacy/concepts/tools) is a function or executable capability that an MCP server exposes to a LLM or AI application to perform an action in the real world.

### Tools

The bigquerydatatransfer.googleapis.com MCP server has the following tools:

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
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/mcp/tools_list/list_data_sources"><code>list_data_sources</code></a></td>
<td><p>List all the data sources that the project has access to.</p>
<p>The following example shows a MCP call to list all data sources in the project <code>myproject</code> in the location <code>myregion</code> .</p>
<p>If the location isn't explicitly specified, and it can't be determined from the resources in the request, then the <a href="https://docs.cloud.google.com/bigquery/docs/locations#default_location">default location</a> is used. If the default location isn't set, then the job runs in the <code>US</code> multi-region.</p>
<p><code>list_data_sources(project_id="myproject", location="myregion")</code></p></td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/mcp/tools_list/get_data_source"><code>get_data_source</code></a></td>
<td>Get details about a data source.</td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/mcp/tools_list/create_transfer_config"><code>create_transfer_config</code></a></td>
<td><p>Create a transfer configuration.</p>
<p>To create a transfer configuration, do the following:</p>
<ul>
<li>Provide the <code>required_fields</code> . Parameters allowed for Secret Manager must be set with Secret Manager. Plaintext is strictly disallowed in requests.</li>
<li>Specify how often you want your transfer to run by specifying <code>schedule_options</code></li>
<li>Provide the <code>optional_fields</code> .</li>
<li>If you want to use a service account to create this transfer, provide a <code>service_account_name</code> .</li>
</ul>
<p>If the request fails due to missing valid credentials, do the following: * Find your <code>client_id</code> and <code>data_source_scopes</code> from your data source definition. * Authorize your data source by navigating to the following link:</p>
<pre data-fenced=""><code>https://bigquery.cloud.google.com/datatransfer/oauthz/auth?redirect_uri=urn:ietf:wg:oauth:2.0:oob&amp;response_type=version_info&amp;client_id=CLIENT_ID&amp;scope=DATA_SOURCE_1%20DATA_SOURCE_2</code></pre>
<ul>
<li>Provide the <code>version_info</code> .</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/mcp/tools_list/update_transfer_config"><code>update_transfer_config</code></a></td>
<td><p>Update a transfer configuration.</p>
<ul>
<li>When updating params, parameters allowed for Secret Manager must be set with Secret Manager. Plaintext is strictly disallowed in requests.</li>
</ul>
<p>The following example shows a MCP call to update a transfer configuration named <code>transfer_config_id</code> in the project <code>myproject</code> in the location <code>myregion</code> .</p>
<p><code>update_transfer_config(data_source=GOOGLE_ADS, project_id="myproject", location="myregion", transfer_config_id="mytransferconfig", display_name="Updated Name")</code></p></td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/mcp/tools_list/delete_transfer_config"><code>delete_transfer_config</code></a></td>
<td><p>Delete a transfer configuration.</p>
<p>The following example shows a MCP call to delete a transfer configuration by its resource name.</p>
<p><code>delete_transfer_config(name="projects/myproject/locations/myregion/transferConfigs/mytransferconfig")</code></p></td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/mcp/tools_list/get_transfer_config"><code>get_transfer_config</code></a></td>
<td><p>Get details about a transfer config.</p>
<p>The following example shows a MCP call to get details about a transfer configuration named <code>transfer_config_id</code> in the project <code>myproject</code> in the location <code>myregion</code> .</p>
<p>If the location isn't explicitly specified, and it can't be determined from the resources in the request, then the <a href="https://docs.cloud.google.com/bigquery/docs/locations#default_location">default location</a> is used. If the default location isn't set, then the job runs in the <code>US</code> multi-region.</p>
<p><code>get_transfer_config(project_id="myproject", location="myregion", transfer_config_id="mytransferconfig")</code></p></td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/mcp/tools_list/list_transfer_configs"><code>list_transfer_configs</code></a></td>
<td><p>List all transfer configurations for a project.</p>
<p>If the location isn't explicitly specified, and it can't be determined from the resources in the request, then the <a href="https://docs.cloud.google.com/bigquery/docs/locations#default_location">default location</a> is used. If the default location isn't set, then the job runs in the <code>US</code> multi-region.</p>
<p><code>list_transfer_configs(project_id="myproject", location="myregion")</code></p></td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/mcp/tools_list/start_manual_transfer_runs"><code>start_manual_transfer_runs</code></a></td>
<td><p>Start manual transfer runs for a transfer config.</p>
<p>The following example shows a MCP call to start manual transfer runs for a transfer configuration named <code>transfer_config_id</code> in the project <code>myproject</code> in the location <code>myregion</code> .</p>
<p>If the transfer configuration was a manual transfer without a schedule, then request for a single run date. Otherwise ask for either a run date or run date range.</p>
<p>If the location isn't explicitly specified, and it can't be determined from the resources in the request, then the <a href="https://docs.cloud.google.com/bigquery/docs/locations#default_location">default location</a> is used. If the default location isn't set, then the job runs in the <code>US</code> multi-region.</p>
<p><code>start_manual_transfer_runs(project_id="myproject", location="myregion", transfer_config_id="mytransferconfig", run_date="2024-01-01", run_date_range=("2024-01-01", "2024-01-02"))</code></p></td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/mcp/tools_list/list_transfer_runs"><code>list_transfer_runs</code></a></td>
<td><p>List all the transfer runs for a transfer config.</p>
<p>The following example shows a MCP call to list all transfer runs for a transfer configuration named <code>transfer_config_id</code> in the project <code>myproject</code> in the location <code>myregion</code> .</p>
<p>If the location isn't explicitly specified, and it can't be determined from the resources in the request, then the <a href="https://docs.cloud.google.com/bigquery/docs/locations#default_location">default location</a> is used. If the default location isn't set, then the job runs in the <code>US</code> multi-region.</p>
<p><code>list_transfer_runs(project_id="myproject", location="myregion", transfer_config_id="mytransferconfig")</code></p></td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/mcp/tools_list/get_transfer_run"><code>get_transfer_run</code></a></td>
<td><p>Get details about a transfer run.</p>
<p>The following example shows a MCP call to get details about a transfer run named <code>transfer_run_id</code> in the project <code>myproject</code> in the location <code>myregion</code> .</p>
<p>If the location isn't explicitly specified, and it can't be determined from the resources in the request, then the <a href="https://docs.cloud.google.com/bigquery/docs/locations#default_location">default location</a> is used. If the default location isn't set, then the job runs in the <code>US</code> multi-region.</p>
<p><code>get_transfer_run(project_id="myproject", location="myregion", transfer_config_id="mytransferconfig", transfer_run_id="mytransferrun")</code></p></td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/mcp/tools_list/delete_transfer_run"><code>delete_transfer_run</code></a></td>
<td><p>Delete a transfer run.</p>
<p>The following example shows an MCP call to delete a transfer run by its resource name.</p>
<p><code>delete_transfer_run(name="projects/myproject/locations/myregion/transferConfigs/mytransferconfig/runs/mytransferrun")</code></p></td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/mcp/tools_list/list_transfer_logs"><code>list_transfer_logs</code></a></td>
<td><p>List transfer logs for a transfer run by its resource name.</p>
<p>The following example shows a MCP call to list transfer logs for a transfer run.</p>
<p><code>list_transfer_logs(parent="projects/myproject/locations/myregion/transferConfigs/mytransferconfig/runs/mytransferrun")</code></p></td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/mcp/tools_list/check_valid_creds"><code>check_valid_creds</code></a></td>
<td><p>Check for valid credentials for a data source.</p>
<p>The following example shows a MCP call to check for valid credentials for a data source with the ID <code>data_source_id</code> in the project <code>myproject</code> in the location <code>myregion</code> .</p>
<p>If the location isn't explicitly specified, and it can't be determined from the resources in the request, then the <a href="https://docs.cloud.google.com/bigquery/docs/locations#default_location">default location</a> is used. If the default location isn't set, then the job runs in the <code>US</code> multi-region.</p>
<p>If <code>has_valid_creds</code> is true, then the credentials are valid. Otherwise, the credentials are not valid.</p>
<p><code>check_valid_creds(project_id="myproject", location="myregion", data_source_id="mydatasource")</code></p></td>
</tr>
</tbody>
</table>

### Get MCP tool specifications

To get the MCP tool specifications for all tools in an MCP server, use the `tools/list` method. The following example demonstrates how to use `curl` to list all tools and their specifications currently available within the MCP server.

**Curl Request**

```
curl --location 'https://bigquerydatatransfer.googleapis.com/mcp' \
--header 'content-type: application/json' \
--header 'accept: application/json, text/event-stream' \
--data '{
    "method": "tools/list",
    "jsonrpc": "2.0",
    "id": 1
}'
```
