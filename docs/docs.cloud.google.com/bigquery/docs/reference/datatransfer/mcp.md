A [Model Context Protocol (MCP) server](https://modelcontextprotocol.io/docs/learn/server-concepts) acts as a proxy between an external service that provides context, data, or capabilities to a Large Language Model (LLM) or AI application. MCP servers connect AI applications to external systems such as databases and web services, translating their responses into a format that the AI application can understand.

### Server Setup

You must [enable MCP servers](https://docs.cloud.google.com/mcp/enable-disable-mcp-servers) and [set up authentication](https://docs.cloud.google.com/mcp/authenticate-mcp) before use. For more information about using Google and Google Cloud remote MCP servers, see [Google Cloud MCP servers overview](https://docs.cloud.google.com/mcp/overview) .

The BigQuery Data Transfer Service MCP server provides tools to interact with the BigQuery Data Transfer Service.

### Server Endpoints

An MCP service endpoint is the network address and communication interface (usually a URL) of the MCP server that an AI application (the Host for the MCP client) uses to establish a secure, standardized connection. It is the point of contact for the LLM to request context, call a tool, or access a resource. Google MCP endpoints can be global or regional.

The bigquerydatatransfer.googleapis.com MCP server has the following MCP endpoint:

  - https://bigquerydatatransfer.googleapis.com/mcp

## MCP Tools

An [MCP tool](https://modelcontextprotocol.io/legacy/concepts/tools) is a function or executable capability that an MCP server exposes to a LLM or AI application to perform an action in the real world.

The bigquerydatatransfer.googleapis.com MCP server has the following tools:

MCP Tools

[list\_data\_sources](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/mcp/tools_list/list_data_sources)

List all the data sources that the project has access to.

The following example shows a MCP call to list all data sources in the project `  myproject  ` in the location `  myregion  ` .

If the location isn't explicitly specified, and it can't be determined from the resources in the request, then the [default location](https://docs.cloud.google.com/bigquery/docs/locations#default_location) is used. If the default location isn't set, then the job runs in the `  US  ` multi-region.

`  list_data_sources(project_id="myproject", location="myregion")  `

[get\_data\_source](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/mcp/tools_list/get_data_source)

Get details about a data source.

[create\_transfer\_config](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/mcp/tools_list/create_transfer_config)

Create a transfer configuration.

To create a transfer configuration, do the following:

  - Provide the `  required_fields  ` .

  - Specify how often you want your transfer to run by specifying `  schedule_options  `

  - Provide the `  optional_fields  ` .

  - If you want to use a service account to create this transfer, provide a `  service_account_name  ` .

  - Check that you have valid credentials by calling `  check_valid_creds  ` :
    
      - If you do not have valid credentials, do the following:
      - Find your `  client_id  ` and `  data_source_scopes  ` from your data source definition.
      - Authorize your data source by navigating to the following link:
    
    <!-- end list -->
    
        https://bigquery.cloud.google.com/datatransfer/oauthz/auth?redirect_uri=urn:ietf:wg:oauth:2.0:oob&response_type=version_info&client_id=CLIENT_ID&scope=DATA_SOURCE_1%20DATA_SOURCE_2
    
      - Provide the `  version_info  ` .
      - If you have valid credentials, then `  version_info  ` is not required.

[get\_transfer\_config](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/mcp/tools_list/get_transfer_config)

Get details about a transfer config.

The following example shows a MCP call to get details about a transfer configuration named `  transfer_config_id  ` in the project `  myproject  ` in the location `  myregion  ` .

If the location isn't explicitly specified, and it can't be determined from the resources in the request, then the [default location](https://docs.cloud.google.com/bigquery/docs/locations#default_location) is used. If the default location isn't set, then the job runs in the `  US  ` multi-region.

`  get_transfer_config(project_id="myproject", location="myregion", transfer_config_id="mytransferconfig")  `

[list\_transfer\_configs](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/mcp/tools_list/list_transfer_configs)

List all transfer configurations for a project.

If the location isn't explicitly specified, and it can't be determined from the resources in the request, then the [default location](https://docs.cloud.google.com/bigquery/docs/locations#default_location) is used. If the default location isn't set, then the job runs in the `  US  ` multi-region.

`  list_transfer_configs(project_id="myproject", location="myregion")  `

[start\_manual\_transfer\_runs](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/mcp/tools_list/start_manual_transfer_runs)

Start manual transfer runs for a transfer config.

The following example shows a MCP call to start manual transfer runs for a transfer configuration named `  transfer_config_id  ` in the project `  myproject  ` in the location `  myregion  ` .

If the transfer configuration was a manual transfer without a schedule, then request for a single run date. Otherwise ask for either a run date or run date range.

If the location isn't explicitly specified, and it can't be determined from the resources in the request, then the [default location](https://docs.cloud.google.com/bigquery/docs/locations#default_location) is used. If the default location isn't set, then the job runs in the `  US  ` multi-region.

`  start_manual_transfer_runs(project_id="myproject", location="myregion", transfer_config_id="mytransferconfig", run_date="2024-01-01", run_date_range=("2024-01-01", "2024-01-02"))  `

[list\_transfer\_runs](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/mcp/tools_list/list_transfer_runs)

List all the transfer runs for a transfer config.

The following example shows a MCP call to list all transfer runs for a transfer configuration named `  transfer_config_id  ` in the project `  myproject  ` in the location `  myregion  ` .

If the location isn't explicitly specified, and it can't be determined from the resources in the request, then the [default location](https://docs.cloud.google.com/bigquery/docs/locations#default_location) is used. If the default location isn't set, then the job runs in the `  US  ` multi-region.

`  list_transfer_runs(project_id="myproject", location="myregion", transfer_config_id="mytransferconfig")  `

[get\_transfer\_run](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/mcp/tools_list/get_transfer_run)

Get details about a transfer run.

The following example shows a MCP call to get details about a transfer run named `  transfer_run_id  ` in the project `  myproject  ` in the location `  myregion  ` .

If the location isn't explicitly specified, and it can't be determined from the resources in the request, then the [default location](https://docs.cloud.google.com/bigquery/docs/locations#default_location) is used. If the default location isn't set, then the job runs in the `  US  ` multi-region.

`  get_transfer_run(project_id="myproject", location="myregion", transfer_config_id="mytransferconfig", transfer_run_id="mytransferrun")  `

[check\_valid\_creds](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/mcp/tools_list/check_valid_creds)

Check for valid credentials for a data source.

The following example shows a MCP call to check for valid credentials for a data source with the ID `  data_source_id  ` in the project `  myproject  ` in the location `  myregion  ` .

If the location isn't explicitly specified, and it can't be determined from the resources in the request, then the [default location](https://docs.cloud.google.com/bigquery/docs/locations#default_location) is used. If the default location isn't set, then the job runs in the `  US  ` multi-region.

If `  has_valid_creds  ` is true, then the credentials are valid. Otherwise, the credentials are not valid.

`  check_valid_creds(project_id="myproject", location="myregion", data_source_id="mydatasource")  `

### Get MCP tool specifications

To get the MCP tool specifications for all tools in an MCP server, use the `  tools/list  ` method. The following example demonstrates how to use `  curl  ` to list all tools and their specifications currently available within the MCP server.

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
<td><pre dir="ltr" data-is-upgraded="" data-syntax="Bash" translate="no"><code>                      curl --location &#39;https://bigquerydatatransfer.googleapis.com/mcp&#39; \
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
