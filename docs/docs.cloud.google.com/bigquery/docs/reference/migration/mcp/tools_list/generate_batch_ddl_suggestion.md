---
name: documents/docs.cloud.google.com/bigquery/docs/reference/migration/mcp/tools_list/generate_batch_ddl_suggestion
uri: https://docs.cloud.google.com/bigquery/docs/reference/migration/mcp/tools_list/generate_batch_ddl_suggestion
title: 'MCP Tools Reference: bigquerymigration.googleapis.com'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

## Tool: `generate_batch_ddl_suggestion`

Generates Data Definition Language (DDL) suggestions for a batch translation. **NOTE: This feature is experimental and in active development. It may not work correctly and should be used with caution.**

The following code sample shows how to use `curl` to call the `generate_batch_ddl_suggestion` MCP tool.

**Curl Request**

```
curl --location 'https://bigquerymigration.googleapis.com/mcp' \
--header 'content-type: application/json' \
--header 'accept: application/json, text/event-stream' \
--data '{
  "method": "tools/call",
  "params": {
    "name": "generate_batch_ddl_suggestion",
    "arguments": {
      // Provide these details according to the MCP tool specification.
    }
  },
  "jsonrpc": "2.0",
  "id": 1
}'
```

## Input Schema

Request message for `GenerateBatchDdlSuggestion` .

### GenerateBatchDdlSuggestionRequest

**JSON representation**

```
{
  "projectNumber": string,
  "location": string,
  "sourceDialect": string,
  "targetDialect": string,
  "sourceBaseUri": [
    string
  ],
  "targetBaseUri": string
}
```

| Fields            |                                                                                        |
|-------------------|----------------------------------------------------------------------------------------|
| `projectNumber`   | `string` Required. The Google Cloud project number.                                    |
| `location`        | `string` Required. The location.                                                       |
| `sourceDialect`   | `string` Required. The dialect of the source queries.                                  |
| `targetDialect`   | `string` Required. The dialect of the target queries.                                  |
| `sourceBaseUri[]` | `string` Required. The Cloud Storage path containing the inputs.                       |
| `targetBaseUri`   | `string` Required. The base URI for all writes to persistent storage in Cloud Storage. |

## Output Schema

Response message for `GenerateBatchDdlSuggestion` .

### GenerateBatchDdlSuggestionResponse

**JSON representation**

```
{
  "suggestion": string,
  "suggestionState": string
}
```

| Fields            |                                                                                |
|-------------------|--------------------------------------------------------------------------------|
| `suggestion`      | `string` The ID of the suggestion workflow created for this batch translation. |
| `suggestionState` | `string` The current state of the suggestion workflow, typically `RUNNING` .   |

### Tool Annotations

[Tool annotations](https://modelcontextprotocol.io/specification/latest/schema#toolannotations) are sent to MCP clients to describe the basic risk of a given tool. Most clients treat these hints as untrusted, but they can be used to decide when a confirmation prompt might be sent to a user.

Along with the title string, the following boolean hints are defined as follows:

- `readOnlyHint` : If true, the tool doesn't modify its environment. Default: false.
- `destructiveHint` : If true, then the tool can perform destructive actions. If false, then the tool can only perform additive actions. Default: true.
- `idempotentHint` : If true, then calling the tool repeatedly with the same arguments will have no additional effect on its environment. Default: false.
- `openWorldHint` : If true, then the tool can interact with an 'open world' of external entities. If false, then the tool can only interact with internal entities. For example, a web search tool would be open world, while a memory tool would not be open world.

Destructive Hint: ❌ \| Idempotent Hint: ❌ \| Read Only Hint: ❌ \| Open World Hint: ❌
