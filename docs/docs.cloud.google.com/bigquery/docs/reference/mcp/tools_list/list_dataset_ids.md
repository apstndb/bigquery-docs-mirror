---
name: documents/docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/list_dataset_ids
uri: https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/list_dataset_ids
title: 'MCP Tools Reference: bigquery.googleapis.com'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

## Tool: `list_dataset_ids`

List BigQuery dataset IDs and BigLake namespaces in a Google Cloud project. Supports pagination. Use `page_size` to limit results and `page_token` to retrieve next page.

The following code sample shows how to use `curl` to call the `list_dataset_ids` MCP tool.

**Curl Request**

```
curl --location 'https://bigquery.googleapis.com/mcp' \
--header 'content-type: application/json' \
--header 'accept: application/json, text/event-stream' \
--data '{
  "method": "tools/call",
  "params": {
    "name": "list_dataset_ids",
    "arguments": {
      // Provide these details according to the MCP tool specification.
    }
  },
  "jsonrpc": "2.0",
  "id": 1
}'
```

## Input Schema

Request for a list of datasets in a project.

### ListDatasetsRequest

**JSON representation**

```
{
  "projectId": string,
  "pageSize": integer,
  "pageToken": string
}
```

| Fields      |                                                                                                                                         |
|-------------|-----------------------------------------------------------------------------------------------------------------------------------------|
| `projectId` | `string` Required. Project ID of the dataset request.                                                                                   |
| `pageSize`  | `integer` Optional. The maximum number of results to return in a single response page. If unset, the default page size of 5000 is used. |
| `pageToken` | `string` Optional. Page token, returned by a previous call, to request the next page of results.                                        |

## Output Schema

Response for a list of datasets.

### ListDatasetsResponse

**JSON representation**

```
{
  "datasets": [
    {
      object (ListFormatDataset)
    }
  ],
  "nextPageToken": string
}
```

| Fields          |                                                                                                                                                                                                    |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `datasets[]`    | `object ( `[`ListFormatDataset`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/list_dataset_ids#Output.Schema.ListFormatDataset)` )` The datasets that matched the request. |
| `nextPageToken` | `string` A token that can be used to request the next results page.                                                                                                                                |

### ListFormatDataset

**JSON representation**

```
{
  "id": string,
  "friendlyName": string,
  "location": string,
  "type": string
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
<td><code>id</code></td>
<td><p><code>string</code></p>
<p>The ID of the dataset.</p></td>
</tr>
<tr class="even">
<td><code>friendlyName</code></td>
<td><p><code>string</code></p>
<p>An alternate name for the dataset. The friendly name is purely decorative in nature. This can be useful to derive additional information about the dataset.</p></td>
</tr>
<tr class="odd">
<td><code>location</code></td>
<td><p><code>string</code></p>
<p>The geographic location where the dataset resides.</p></td>
</tr>
<tr class="even">
<td><code>type</code></td>
<td><p><code>string</code></p>
<p>Output only. Same as <code>type</code> . The type of the dataset, one of:</p>
<ul>
<li><code>DEFAULT</code> - only accessible by owner and authorized accounts,</li>
<li><code>PUBLIC</code> - accessible by everyone,</li>
<li><code>LINKED</code> - linked dataset,</li>
<li><code>EXTERNAL</code> - dataset with definition in external metadata catalog,</li>
<li><code>BIGLAKE_ICEBERG</code> - a Biglake dataset accessible through the Iceberg API,</li>
<li><code>BIGLAKE_HIVE</code> - a Biglake dataset accessible through the Hive API.</li>
</ul></td>
</tr>
</tbody>
</table>

### StringValue

**JSON representation**

```
{
  "value": string
}
```

| Fields  |                            |
|---------|----------------------------|
| `value` | `string` The string value. |

### Tool Annotations

[Tool annotations](https://modelcontextprotocol.io/specification/latest/schema#toolannotations) are sent to MCP clients to describe the basic risk of a given tool. Most clients treat these hints as untrusted, but they can be used to decide when a confirmation prompt might be sent to a user.

Along with the title string, the following boolean hints are defined as follows:

- `readOnlyHint` : If true, the tool doesn't modify its environment. Default: false.
- `destructiveHint` : If true, then the tool can perform destructive actions. If false, then the tool can only perform additive actions. Default: true.
- `idempotentHint` : If true, then calling the tool repeatedly with the same arguments will have no additional effect on its environment. Default: false.
- `openWorldHint` : If true, then the tool can interact with an 'open world' of external entities. If false, then the tool can only interact with internal entities. For example, a web search tool would be open world, while a memory tool would not be open world.

Destructive Hint: ❌ \| Idempotent Hint: ✅ \| Read Only Hint: ✅ \| Open World Hint: ❌
