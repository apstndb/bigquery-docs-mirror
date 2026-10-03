---
name: documents/docs.cloud.google.com/bigquery/docs/reference/datatransfer/mcp/tools_list/list_transfer_logs
uri: https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/mcp/tools_list/list_transfer_logs
title: 'MCP Tools Reference: bigquerydatatransfer.googleapis.com'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

## Tool: `list_transfer_logs`

List transfer logs for a transfer run by its resource name.

The following example shows a MCP call to list transfer logs for a transfer run.

`list_transfer_logs(parent="projects/myproject/locations/myregion/transferConfigs/mytransferconfig/runs/mytransferrun")`

The following code sample shows how to use `curl` to call the `list_transfer_logs` MCP tool.

**Curl Request**

```
curl --location 'https://bigquerydatatransfer.googleapis.com/mcp' \
--header 'content-type: application/json' \
--header 'accept: application/json, text/event-stream' \
--data '{
  "method": "tools/call",
  "params": {
    "name": "list_transfer_logs",
    "arguments": {
      // Provide these details according to the MCP tool specification.
    }
  },
  "jsonrpc": "2.0",
  "id": 1
}'
```

## Input Schema

A request to get user facing log messages associated with data transfer run.

### ListTransferLogsRequest

**JSON representation**

```
{
  "parent": string,
  "pageToken": string,
  "pageSize": integer,
  "messageTypes": [
    enum (MessageSeverity)
  ]
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
<td><code>parent</code></td>
<td><p><code>string</code></p>
<p>Required. Transfer run name. If you are using the regionless method, the location must be <code>US</code> and the name should be in the following form:</p>
<ul>
<li><code>projects/{project_id}/transferConfigs/{config_id}/runs/{run_id}</code></li>
</ul>
<p>If you are using the regionalized method, the name should be in the following form:</p>
<ul>
<li><code>projects/{project_id}/locations/{location_id}/transferConfigs/{config_id}/runs/{run_id}</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>pageToken</code></td>
<td><p><code>string</code></p>
<p>Pagination token, which can be used to request a specific page of <code>ListTransferLogsRequest</code> list results. For multiple-page results, <code>ListTransferLogsResponse</code> outputs a <code>next_page</code> token, which can be used as the <code>page_token</code> value to request the next page of list results.</p></td>
</tr>
<tr class="odd">
<td><code>pageSize</code></td>
<td><p><code>integer</code></p>
<p>Page size. The default page size is the maximum value of 1000 results.</p></td>
</tr>
<tr class="even">
<td><code>messageTypes[]</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/mcp/tools_list/list_transfer_logs#Input.Schema.MessageSeverity"><code>MessageSeverity</code></a><code> )</code></p>
<p>Message types to return. If not populated - INFO, WARNING and ERROR messages are returned.</p></td>
</tr>
</tbody>
</table>

### MessageSeverity

Represents data transfer user facing message severity.

| Enums                          |                        |
|--------------------------------|------------------------|
| `MESSAGE_SEVERITY_UNSPECIFIED` | No severity specified. |
| `INFO`                         | Informational message. |
| `WARNING`                      | Warning message.       |
| `ERROR`                        | Error message.         |

## Output Schema

The returned list transfer run messages.

### ListTransferLogsResponse

**JSON representation**

```
{
  "transferMessages": [
    {
      object (TransferMessage)
    }
  ],
  "nextPageToken": string
}
```

| Fields               |                                                                                                                                                                                                                            |
|----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `transferMessages[]` | `object ( `[`TransferMessage`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/mcp/tools_list/list_transfer_logs#Output.Schema.TransferMessage)` )` Output only. The stored pipeline transfer messages. |
| `nextPageToken`      | `string` Output only. The next-pagination token. For multiple-page list results, this token can be used as the `GetTransferRunLogRequest.page_token` to request the next page of list results.                             |

### TransferMessage

**JSON representation**

```
{
  "messageTime": string,
  "severity": enum (MessageSeverity),
  "messageText": string
}
```

| Fields        |                                                                                                                                                                                                                                                                                                                                                                                                     |
|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `messageTime` | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Time when message was logged. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` . |
| `severity`    | `enum ( `[`MessageSeverity`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/mcp/tools_list/list_transfer_logs#Input.Schema.MessageSeverity)` )` Message severity.                                                                                                                                                                                                               |
| `messageText` | `string` Message text.                                                                                                                                                                                                                                                                                                                                                                              |

### Timestamp

**JSON representation**

```
{
  "seconds": string,
  "nanos": integer
}
```

| Fields    |                                                                                                                                                                                                                                                                                                                      |
|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `seconds` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Represents seconds of UTC time since Unix epoch 1970-01-01T00:00:00Z. Must be between -62135596800 and 253402300799 inclusive (which corresponds to 0001-01-01T00:00:00Z to 9999-12-31T23:59:59Z).                            |
| `nanos`   | `integer` Non-negative fractions of a second at nanosecond resolution. This field is the nanosecond portion of the duration, not an alternative to seconds. Negative second values with fractions must still have non-negative nanos values that count forward in time. Must be between 0 and 999,999,999 inclusive. |

### MessageSeverity

Represents data transfer user facing message severity.

| Enums                          |                        |
|--------------------------------|------------------------|
| `MESSAGE_SEVERITY_UNSPECIFIED` | No severity specified. |
| `INFO`                         | Informational message. |
| `WARNING`                      | Warning message.       |
| `ERROR`                        | Error message.         |

### Tool Annotations

[Tool annotations](https://modelcontextprotocol.io/specification/latest/schema#toolannotations) are sent to MCP clients to describe the basic risk of a given tool. Most clients treat these hints as untrusted, but they can be used to decide when a confirmation prompt might be sent to a user.

Along with the title string, the following boolean hints are defined as follows:

- `readOnlyHint` : If true, the tool doesn't modify its environment. Default: false.
- `destructiveHint` : If true, then the tool can perform destructive actions. If false, then the tool can only perform additive actions. Default: true.
- `idempotentHint` : If true, then calling the tool repeatedly with the same arguments will have no additional effect on its environment. Default: false.
- `openWorldHint` : If true, then the tool can interact with an 'open world' of external entities. If false, then the tool can only interact with internal entities. For example, a web search tool would be open world, while a memory tool would not be open world.

Destructive Hint: ❌ \| Idempotent Hint: ✅ \| Read Only Hint: ✅ \| Open World Hint: ❌
