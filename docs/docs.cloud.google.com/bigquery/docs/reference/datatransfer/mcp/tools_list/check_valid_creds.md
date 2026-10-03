---
name: documents/docs.cloud.google.com/bigquery/docs/reference/datatransfer/mcp/tools_list/check_valid_creds
uri: https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/mcp/tools_list/check_valid_creds
title: 'MCP Tools Reference: bigquerydatatransfer.googleapis.com'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

## Tool: `check_valid_creds`

Check for valid credentials for a data source.

The following example shows a MCP call to check for valid credentials for a data source with the ID `data_source_id` in the project `myproject` in the location `myregion` .

If the location isn't explicitly specified, and it can't be determined from the resources in the request, then the [default location](https://docs.cloud.google.com/bigquery/docs/locations#default_location) is used. If the default location isn't set, then the job runs in the `US` multi-region.

If `has_valid_creds` is true, then the credentials are valid. Otherwise, the credentials are not valid.

`check_valid_creds(project_id="myproject", location="myregion", data_source_id="mydatasource")`

The following code sample shows how to use `curl` to call the `check_valid_creds` MCP tool.

**Curl Request**

```
curl --location 'https://bigquerydatatransfer.googleapis.com/mcp' \
--header 'content-type: application/json' \
--header 'accept: application/json, text/event-stream' \
--data '{
  "method": "tools/call",
  "params": {
    "name": "check_valid_creds",
    "arguments": {
      // Provide these details according to the MCP tool specification.
    }
  },
  "jsonrpc": "2.0",
  "id": 1
}'
```

## Input Schema

A request to determine whether the user has valid credentials. This method is used to limit the number of OAuth popups in the user interface. The user id is inferred from the API call context. If the data source has the Google+ authorization type, this method returns false, as it cannot be determined whether the credentials are already valid merely based on the user id.

### CheckValidCredsRequest

**JSON representation**

```
{
  "name": string
}
```

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. The name of the data source. If you are using the regionless method, the location must be <code>US</code> and the name should be in the following form:</p>
<ul>
<li><code>projects/{project_id}/dataSources/{data_source_id}</code></li>
</ul>
<p>If you are using the regionalized method, the name should be in the following form:</p>
<ul>
<li><code>projects/{project_id}/locations/{location_id}/dataSources/{data_source_id}</code></li>
</ul></td>
</tr>
</tbody>
</table>

## Output Schema

A response indicating whether the credentials exist and are valid.

### CheckValidCredsResponse

**JSON representation**

```
{
  "hasValidCreds": boolean
}
```

| Fields          |                                                                   |
|-----------------|-------------------------------------------------------------------|
| `hasValidCreds` | `boolean` If set to `true` , the credentials exist and are valid. |

### Tool Annotations

[Tool annotations](https://modelcontextprotocol.io/specification/latest/schema#toolannotations) are sent to MCP clients to describe the basic risk of a given tool. Most clients treat these hints as untrusted, but they can be used to decide when a confirmation prompt might be sent to a user.

Along with the title string, the following boolean hints are defined as follows:

- `readOnlyHint` : If true, the tool doesn't modify its environment. Default: false.
- `destructiveHint` : If true, then the tool can perform destructive actions. If false, then the tool can only perform additive actions. Default: true.
- `idempotentHint` : If true, then calling the tool repeatedly with the same arguments will have no additional effect on its environment. Default: false.
- `openWorldHint` : If true, then the tool can interact with an 'open world' of external entities. If false, then the tool can only interact with internal entities. For example, a web search tool would be open world, while a memory tool would not be open world.

Destructive Hint: ❌ \| Idempotent Hint: ✅ \| Read Only Hint: ✅ \| Open World Hint: ❌
