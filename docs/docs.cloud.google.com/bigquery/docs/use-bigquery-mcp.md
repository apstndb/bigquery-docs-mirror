# Use the BigQuery MCP server

**Preview**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) , and the [Additional Terms for Generative AI Preview Products](https://cloud.google.com/trustedtester/aitos) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

This document describes how to use the BigQuery Model Context Protocol (MCP) server to connect to BigQuery from AI applications such as Gemini CLI, agent mode in Gemini Code Assist, Claude Code, or in AI applications you're developing.

[Model Context Protocol](https://modelcontextprotocol.io/docs/getting-started/intro) (MCP) standardizes how large language models (LLMs) and AI applications or agents connect to outside data sources. MCP servers let you use their tools, resources, and prompts to take actions and get updated data from their backend service.

Local MCP servers typically run on your local machine and use the standard input and output streams ( `  stdio  ` ) for communication between services on the same device. MCP servers run on the service's infrastructure and offer an HTTPS endpoint to AI applications for communication between the AI MCP client and the MCP server. For more information on MCP architecture, see [MCP architecture](https://modelcontextprotocol.io/docs/learn/architecture) .

Google and Google Cloud MCP servers have the following features and benefits:

  - Simplified, centralized discovery
  - Managed global or regional HTTPS endpoints
  - Fine-grained authorization
  - Optional prompt and response security with Model Armor protection
  - Centralized audit logging

For information about other MCP servers and information about security and governance controls available for Google Cloud MCP servers, see [Google Cloud MCP servers overview](https://docs.cloud.google.com/mcp/overview) .

You might use the BigQuery [local MCP server](/bigquery/docs/pre-built-tools-with-mcp-toolbox) for the following reasons:

  - You need to build a custom tool over a parameterized SQL query.
  - You don't have permissions to enable or use the MCP server in your project.

For more information about how to use our local MCP server, see [Connect LLMs to BigQuery with MCP](https://docs.cloud.google.com/bigquery/docs/pre-built-tools-with-mcp-toolbox) . The following sections apply only to the BigQuery MCP server.

## Before you begin

1.  Enable the BigQuery API.
    
    **Roles required to enable APIs**
    
    To enable APIs, you need the Service Usage Admin IAM role ( `  roles/serviceusage.serviceUsageAdmin  ` ), which contains the `  serviceusage.services.enable  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .
    
    For new projects, the BigQuery API is automatically enabled.

2.  Optional: [Enable billing](/billing/docs/how-to/modify-project) for the project. If you don't want to enable billing or provide a credit card, the steps in this document still work. BigQuery provides you a sandbox to perform the steps. For more information, see [Enable the BigQuery sandbox](/bigquery/docs/sandbox#setup) .
    
    **Note:** If your project has a billing account and you want to use the BigQuery sandbox, then [disable billing for your project](/billing/docs/how-to/modify-project#disable_billing_for_a_project) .

### Required roles

To get the permissions that you need to enable the BigQuery MCP server, ask your administrator to grant you the following IAM roles on the project where you want to enable the BigQuery MCP server:

  - Enable APIs and MCP servers in the project: [Service Usage Admin](/iam/docs/roles-permissions/serviceusage#serviceusage.serviceUsageAdmin) ( `  roles/serviceusage.serviceUsageAdmin  ` )
  - Make MCP tool calls: [MCP Tool User](/iam/docs/roles-permissions/mcp#mcp.toolUser) ( `  roles/mcp.toolUser  ` )
  - Run BigQuery jobs: [BigQuery Job User](/iam/docs/roles-permissions/bigquery#bigquery.jobUser) ( `  roles/bigquery.jobUser  ` )
  - Query BigQuery data: [BigQuery Data Viewer](/iam/docs/roles-permissions/bigquery#bigquery.dataViewer) ( `  roles/bigquery.dataViewer  ` )

For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

These predefined roles contain the permissions required to enable the BigQuery MCP server. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

The following permissions are required to enable the BigQuery MCP server:

  - Enable MCP servers in a project:
      - `  serviceusage.mcppolicy.get  `
      - `  serviceusage.mcppolicy.update  `
  - Make MCP tool calls: `  mcp.tools.call  `
  - Run BigQuery jobs: `  bigquery.jobs.create  `
  - Query BigQuery data: `  bigquery.tables.getData  `

You might also be able to get these permissions with [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

**Note:** Additional BigQuery permissions might be required depending on the task. For information about BigQuery permissions, see [BigQuery IAM roles and permissions](/bigquery/docs/access-control) .

## Enable or disable the BigQuery MCP server

You can enable or disable the BigQuery MCP server in a project with the `  gcloud beta services mcp enable  ` command. For more information, see the following sections.

### Enable the BigQuery MCP server in a project

**Note:** After March 17, 2026, the BigQuery remote MCP server is automatically enabled when you enable BigQuery.

If you're using different projects for your client credentials, such as service account keys, OAuth client ID or API keys, and for hosting your resources, then you must enable the BigQuery service and the BigQuery MCP server on both projects.

To enable the BigQuery MCP server in your Google Cloud project, run the following command:

``` text
gcloud beta services mcp enable SERVICE \
    --project=PROJECT_ID
```

Replace the following:

  - `  PROJECT_ID  ` : the Google Cloud project ID
  - `  SERVICE  ` : `  bigquery.googleapis.com  ` (the global service name for BigQuery)

The BigQuery MCP server is enabled for use in your Google Cloud project. If the BigQuery service isn't enabled for your Google Cloud project, you're prompted to enable the service before enabling the BigQuery MCP server.

As a security best practice, we recommend that you enable MCP servers only for the services required for your AI application to function.

### Disable the BigQuery MCP server in a project

To disable the BigQuery MCP server in your Google Cloud project, run the following command:

``` text
gcloud beta services mcp disable SERVICE \
    --project=PROJECT_ID
```

The BigQuery MCP server is disabled for use in your Google Cloud project.

## Authentication and authorization

BigQuery MCP servers use the [OAuth 2.0](https://developers.google.com/identity/protocols/oauth2) protocol with [Identity and Access Management (IAM)](/iam/docs/overview) for authentication and authorization. All [Google Cloud identities](/docs/authentication/identity-products) are supported for authentication to MCP servers.

The BigQuery MCP server doesn't accept API keys.

## BigQuery MCP OAuth scopes

OAuth 2.0 uses scopes and credentials to determine if an authenticated principal is authorized to take a specific action on a resource. For more information about OAuth 2.0 scopes at Google, read [Using OAuth 2.0 to access Google APIs](https://developers.google.com/identity/protocols/oauth2) .

BigQuery has the following MCP tool OAuth scopes:

<table>
<thead>
<tr class="header">
<th>Scope URI for gcloud CLI</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       https://www.googleapis.com/auth/bigquery      </code></td>
<td>View and manage your data in BigQuery and see the email address for your Google Account.</td>
</tr>
</tbody>
</table>

Additional scopes might be required on the resources accessed during a tool call. To view a list of scopes required for BigQuery, see [OAuth 2.0 scopes for BigQuery API v2](https://developers.google.com/identity/protocols/oauth2/scopes#bigquery) .

## Configure an MCP client to use the BigQuery MCP server

Host programs, such as Claude or Gemini CLI, can instantiate MCP clients that connect to a single MCP server. A host program can have multiple clients that connect to different MCP servers. To connect to an MCP server, the MCP client must know at a minimum the URL of the MCP server.

In your host, look for a way to connect to a MCP server. You're prompted to enter details about the server, such as its name and URL.

For the BigQuery MCP server, enter the following as required:

  - **Server name** : BigQuery MCP server

  - **Server URL** or **Endpoint** : https://bigquery.googleapis.com/mcp

  - **Transport** : HTTP

  - **Authentication details** : your Google Cloud credentials, your OAuth Client ID and secret, or an agent identity and credentials
    
    Which authentication details you choose depend on how you want to authenticate. For more information, see [Authenticate to MCP servers](https://docs.cloud.google.com/mcp/authenticate-mcp) .

For host-specific guidance, see the following:

  - [Gemini CLI MCP server setup](https://docs.cloud.google.com/mcp/configure-mcp-ai-application#gemini-cli)
  - [Claude support: Getting started with custom connectors using remote MCP](https://support.claude.com/en/articles/11175166-getting-started-with-custom-connectors-using-remote-mcp)

For more general guidance, see [Connect to remote MCP servers](https://modelcontextprotocol.io/docs/develop/connect-remote-servers) .

## Available tools

To view details of available MCP tools and their descriptions for the BigQuery MCP server, see the [BigQuery MCP reference](/bigquery/docs/reference/mcp) .

### Limitations

The BigQuery MCP tools are subject to the following limitations:

  - The [`  execute_sql  `](/bigquery/docs/reference/mcp/execute_sql) tool doesn't support querying Google Drive external tables.
  - By default, the `  execute_sql  ` tool limits query processing time to three minutes. Queries that run longer than three minutes are automatically canceled.

### List tools

Use the [MCP inspector](https://modelcontextprotocol.io/docs/tools/inspector) to list tools, or send a `  tools/list  ` HTTP request directly to the BigQuery MCP server. The `  tools/list  ` method doesn't require authentication.

``` text
POST /mcp HTTP/1.1
Host: bigquery.googleapis.com
Content-Type: application/json

{
  "jsonrpc": "2.0",
  "method": "tools/list",
}
```

## Sample use cases

The following are sample use cases for the BigQuery MCP server:

  - Build workflows that use insights from BigQuery data to trigger certain actions such as creating issues and composing emails.

  - Use BigQuery's advanced capabilities like forecasting for higher-order insights.

  - Build a conversational experience for your users with custom agent instructions.

### Sample prompts

You can use the following sample prompts to get information about BigQuery resources, gain insights, and analyze BigQuery data:

  - List the datasets in project `  PROJECT_ID  ` .
  - Find all the queries that I ran in project `  PROJECT_ID  ` using the MCP server in the `  REGION  ` region. Use the tag `  goog-mcp-server:true  ` to identify the query jobs that ran through the MCP server.
  - Find the top orders by volume from `  DATASET_ID  ` in project `  PROJECT_ID  ` . Identify the appropriate tables, find the correct schema, and show the results.
  - Create a forecast on the table `  PROJECT_ID  ` . `  DATASET_ID  ` . `  TABLE_ID  ` for future years. Use `  COLUMN_NAME  ` as the data column and `  COLUMN_NAME  ` as the timestamp column. Show the top 10 forecasts.

In the prompts, replace the following:

  - `  PROJECT_ID  ` : the Google Cloud project ID
  - `  REGION  ` : the name of the region
  - `  DATASET_ID  ` : the name of the dataset
  - `  TABLE_ID  ` : the name of the table
  - `  COLUMN_NAME  ` : the name of the column

## Optional security and safety configurations

MCP introduces new security risks and considerations due to the wide variety of actions that you can take with MCP tools. To minimize and manage these risks, Google Cloud offers defaults and customizable policies to control the use of MCP tools in your Google Cloud organization or project.

For more information about MCP security and governance, see [AI security and safety](https://docs.cloud.google.com/mcp/ai-security-safety) .

### Model Armor

Model Armor is a Google Cloud service designed to enhance the security and safety of your AI applications. It works by proactively screening LLM prompts and responses, protecting against various risks and supporting responsible AI practices. Whether you deploy AI in your cloud environment, or on external cloud providers, Model Armor can help you prevent malicious input, verify content safety, protect sensitive data, maintain compliance, and enforce your AI safety and security policies consistently across your diverse AI landscape.

Model Armor is only available in specific regional locations. If Model Armor is enabled for a project, and a call to that project comes from an unsupported region, Model Armor makes a cross-regional call. For more information, see [Model Armor locations](https://docs.cloud.google.com/security-command-center/docs/regional-endpoints#locations-model-armor) .

#### Enable Model Armor

To enable Model Armor, complete the following steps:

1.  Enable Model Armor on your Google Cloud project.
    
    ``` text
    gcloud services enable modelarmor.googleapis.com \
        --project=PROJECT_ID
    ```
    
    Replace `  PROJECT_ID  ` with your Google Cloud project ID.

2.  Configure the recommended [floor settings for Model Armor](https://docs.cloud.google.com/security-command-center/docs/configure-model-armor-floor-settings) .
    
    ``` text
    gcloud model-armor floorsettings update \
        --full-uri='projects/PROJECT_ID/locations/global/floorSetting' \
        --mcp-sanitization=ENABLED \
        --malicious-uri-filter-settings-enforcement=ENABLED \
        --pi-and-jailbreak-filter-settings-enforcement=ENABLED \
        --pi-and-jailbreak-filter-settings-confidence-level=MEDIUM_AND_ABOVE
    ```
    
    Replace `  PROJECT_ID  ` with your Google Cloud project ID.
    
    Model Armor is configured to scan for [malicious URLs](https://docs.cloud.google.com/security-command-center/docs/model-armor-overview#ma-malicious-url-detection) and [prompt injection and jailbreak](https://docs.cloud.google.com/security-command-center/docs/model-armor-overview#ma-prompt-injection) attempts.
    
    For more information about configurable Model Armor filters, see [Model Armor filters](https://docs.cloud.google.com/security-command-center/docs/model-armor-overview#ma-filters) .

3.  Add Model Armor as a content security provider for MCP services.
    
    ``` text
    gcloud beta services mcp content-security add modelarmor.googleapis.com \
        --project=PROJECT_ID
    ```
    
    Replace `  PROJECT_ID  ` with the Google Cloud project ID.

4.  Confirm that MCP traffic is sent to Model Armor.
    
    ``` text
    gcloud beta services mcp content-security get \
        --project=PROJECT_ID
    ```
    
    Replace `  PROJECT_ID  ` with the Google Cloud project ID.

#### Model Armor logging

For information about Model Armor audit and platform logs, see [Model Armor audit logging](/security-command-center/docs/audit-logging-model-armor) .

**Caution:** If a request fails, Model Armor logs the entire payload. This might expose sensitive information in the logs.

#### Disable Model Armor in a project

To disable Model Armor in a Google Cloud project, run the following command:

``` text
gcloud beta services mcp content-security remove modelarmor.googleapis.com \
    --project=PROJECT_ID
```

Replace `  PROJECT_ID  ` with the Google Cloud project ID.

MCP traffic on Google Cloud isn't be scanned by Model Armor for the specified project.

#### Disable scanning MCP traffic with Model Armor

If you still want to use Model Armor in a project, but you want to stop scanning MCP traffic with Model Armor, then run the following command:

``` text
gcloud model-armor floorsettings update \
    --full-uri='projects/PROJECT_ID/locations/global/floorSetting' \
    --mcp-sanitization=DISABLED
```

Replace `  PROJECT_ID  ` with the Google Cloud project ID.

Model Armor won't scan MCP traffic on Google Cloud.

### Control MCP use with IAM deny policies

[Identity and Access Management (IAM) deny policies](/iam/docs/deny-overview) help you secure Google Cloud remote MCP servers. Configure these policies to block unwanted MCP tool access.

For example, you can deny or allow access based on:

  - The principal.
  - Tool properties like read-only.
  - The application's OAuth client ID.

For more information, see [Control MCP use with Identity and Access Management](/mcp/control-mcp-use-iam) .

## Quotas and limits

The BigQuery MCP server doesn't have its own quotas. There is no limit on the number of call that can be made to the MCP server.

You are still subject to the quotas enforced by the APIs called by the MCP server tools. The following API methods are called by the MCP server tools:

<table>
<thead>
<tr class="header">
<th>Tool</th>
<th>API method</th>
<th>Quotas</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       list_dataset_ids      </code></td>
<td><a href="/bigquery/docs/reference/rest/v2/datasets/list"><code dir="ltr" translate="no">        datasets.list       </code></a></td>
<td><a href="/bigquery/quotas#dataset_limits">Dataset quotas and limits</a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       list_table_ids      </code></td>
<td><a href="/bigquery/docs/reference/rest/v2/tables/list"><code dir="ltr" translate="no">        tables.list       </code></a></td>
<td><a href="/bigquery/quotas#table_limits">Table quotas and limits</a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       get_dataset_info      </code></td>
<td><a href="/bigquery/docs/reference/rest/v2/datasets/get"><code dir="ltr" translate="no">        datasets.get       </code></a></td>
<td><a href="/bigquery/quotas#dataset_limits">Dataset quotas and limits</a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       get_table_info      </code></td>
<td><a href="/bigquery/docs/reference/rest/v2/tables/get"><code dir="ltr" translate="no">        tables.get       </code></a></td>
<td><a href="/bigquery/quotas#table_limits">Table quotas and limits</a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       execute_sql      </code></td>
<td><a href="/bigquery/docs/reference/rest/v2/jobs/query"><code dir="ltr" translate="no">        jobs.Query       </code></a></td>
<td><a href="/bigquery/quotas#query_jobs">Query job quotas and limits</a></td>
</tr>
</tbody>
</table>

For more information on BigQuery quotas, see [Quotas and limits](/bigquery/quotas) .

## What's next

  - Read the [BigQuery MCP reference documentation](/bigquery/docs/reference/mcp) .
  - Learn more about [Google Cloud MCP servers](https://docs.cloud.google.com/mcp/overview) .
  - See the MCP [supported products](/mcp/supported-products) .
