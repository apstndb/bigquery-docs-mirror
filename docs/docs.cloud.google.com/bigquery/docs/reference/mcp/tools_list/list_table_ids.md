---
name: documents/docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/list_table_ids
uri: https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/list_table_ids
title: 'MCP Tools Reference: bigquery.googleapis.com'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

## Tool: `list_table_ids`

List table ids in a BigQuery dataset or BigLake namespace. Supports pagination. Use `page_size` to limit results and `page_token` to retrieve next page.

The following code sample shows how to use `curl` to call the `list_table_ids` MCP tool.

**Curl Request**

```
curl --location 'https://bigquery.googleapis.com/mcp' \
--header 'content-type: application/json' \
--header 'accept: application/json, text/event-stream' \
--data '{
  "method": "tools/call",
  "params": {
    "name": "list_table_ids",
    "arguments": {
      // Provide these details according to the MCP tool specification.
    }
  },
  "jsonrpc": "2.0",
  "id": 1
}'
```

## Input Schema

Request for a list of tables in a dataset.

### ListTablesRequest

**JSON representation**

```
{
  "projectId": string,
  "datasetId": string,
  "pageSize": integer,
  "pageToken": string
}
```

| Fields      |                                                                                                                                         |
|-------------|-----------------------------------------------------------------------------------------------------------------------------------------|
| `projectId` | `string` Required. Project ID of the table request.                                                                                     |
| `datasetId` | `string` Required. Dataset ID of the table request.                                                                                     |
| `pageSize`  | `integer` Optional. The maximum number of results to return in a single response page. If unset, the default page size of 5000 is used. |
| `pageToken` | `string` Optional. Page token, returned by a previous call, to request the next page of results.                                        |

## Output Schema

Response for a list of tables.

### ListTablesResponse

**JSON representation**

```
{
  "tables": [
    {
      object (ListFormatTable)
    }
  ],
  "nextPageToken": string
}
```

| Fields          |                                                                                                                                                                                            |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `tables[]`      | `object ( `[`ListFormatTable`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/list_table_ids#Output.Schema.ListFormatTable)` )` The tables that matched the request. |
| `nextPageToken` | `string` A token that can be used to request the next results page.                                                                                                                        |

### ListFormatTable

**JSON representation**

```
{
  "id": string,
  "type": string
}
```

| Fields |                                                                                                    |
|--------|----------------------------------------------------------------------------------------------------|
| `id`   | `string` The ID of the table.                                                                      |
| `type` | `string` Output only. The type of table (e.g. TABLE, VIEW, EXTERNAL, MATERIALIZED_VIEW, SNAPSHOT). |

### Tool Annotations

[Tool annotations](https://modelcontextprotocol.io/specification/latest/schema#toolannotations) are sent to MCP clients to describe the basic risk of a given tool. Most clients treat these hints as untrusted, but they can be used to decide when a confirmation prompt might be sent to a user.

Along with the title string, the following boolean hints are defined as follows:

- `readOnlyHint` : If true, the tool doesn't modify its environment. Default: false.
- `destructiveHint` : If true, then the tool can perform destructive actions. If false, then the tool can only perform additive actions. Default: true.
- `idempotentHint` : If true, then calling the tool repeatedly with the same arguments will have no additional effect on its environment. Default: false.
- `openWorldHint` : If true, then the tool can interact with an 'open world' of external entities. If false, then the tool can only interact with internal entities. For example, a web search tool would be open world, while a memory tool would not be open world.

Destructive Hint: ❌ \| Idempotent Hint: ✅ \| Read Only Hint: ✅ \| Open World Hint: ❌
