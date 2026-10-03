---
name: documents/docs.cloud.google.com/bigquery/docs/reference/datatransfer/mcp/tools_list/delete_transfer_run
uri: https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/mcp/tools_list/delete_transfer_run
title: 'MCP Tools Reference: bigquerydatatransfer.googleapis.com'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

## Tool: `delete_transfer_run`

Delete a transfer run.

The following example shows an MCP call to delete a transfer run by its resource name.

`delete_transfer_run(name="projects/myproject/locations/myregion/transferConfigs/mytransferconfig/runs/mytransferrun")`

The following code sample shows how to use `curl` to call the `delete_transfer_run` MCP tool.

**Curl Request**

```
curl --location 'https://bigquerydatatransfer.googleapis.com/mcp' \
--header 'content-type: application/json' \
--header 'accept: application/json, text/event-stream' \
--data '{
  "method": "tools/call",
  "params": {
    "name": "delete_transfer_run",
    "arguments": {
      // Provide these details according to the MCP tool specification.
    }
  },
  "jsonrpc": "2.0",
  "id": 1
}'
```

## Input Schema

A request to delete data transfer run information.

### DeleteTransferRunRequest

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
<p>Required. The name of the resource requested. If you are using the regionless method, the location must be <code>US</code> and the name should be in the following form:</p>
<ul>
<li><code>projects/{project_id}/transferConfigs/{config_id}/runs/{run_id}</code></li>
</ul>
<p>If you are using the regionalized method, the name should be in the following form:</p>
<ul>
<li><code>projects/{project_id}/locations/{location_id}/transferConfigs/{config_id}/runs/{run_id}</code></li>
</ul></td>
</tr>
</tbody>
</table>

## Output Schema

A generic empty message that you can re-use to avoid defining duplicated empty messages in your APIs. A typical example is to use it as the request or the response type of an API method. For instance:

```
service Foo {
  rpc Bar(google.protobuf.Empty) returns (google.protobuf.Empty);
}
```

### Tool Annotations

[Tool annotations](https://modelcontextprotocol.io/specification/latest/schema#toolannotations) are sent to MCP clients to describe the basic risk of a given tool. Most clients treat these hints as untrusted, but they can be used to decide when a confirmation prompt might be sent to a user.

Along with the title string, the following boolean hints are defined as follows:

- `readOnlyHint` : If true, the tool doesn't modify its environment. Default: false.
- `destructiveHint` : If true, then the tool can perform destructive actions. If false, then the tool can only perform additive actions. Default: true.
- `idempotentHint` : If true, then calling the tool repeatedly with the same arguments will have no additional effect on its environment. Default: false.
- `openWorldHint` : If true, then the tool can interact with an 'open world' of external entities. If false, then the tool can only interact with internal entities. For example, a web search tool would be open world, while a memory tool would not be open world.

Destructive Hint: ✅ \| Idempotent Hint: ❌ \| Read Only Hint: ❌ \| Open World Hint: ❌
