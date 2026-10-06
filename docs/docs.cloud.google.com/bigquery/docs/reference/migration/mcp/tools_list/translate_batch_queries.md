---
name: documents/docs.cloud.google.com/bigquery/docs/reference/migration/mcp/tools_list/translate_batch_queries
uri: https://docs.cloud.google.com/bigquery/docs/reference/migration/mcp/tools_list/translate_batch_queries
title: 'MCP Tools Reference: bigquerymigration.googleapis.com'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

## Tool: `translate_batch_queries`

Translates a batch of SQL queries stored in Google Cloud Storage. The translation runs asynchronously: use the `fetch_batch_translation` tool with the returned translation ID to poll its state until it is `SUCCEEDED` or `FAILED` . Wait at least 10 seconds before rechecking the state.

The following code sample shows how to use `curl` to call the `translate_batch_queries` MCP tool.

**Curl Request**

```
curl --location 'https://bigquerymigration.googleapis.com/mcp' \
--header 'content-type: application/json' \
--header 'accept: application/json, text/event-stream' \
--data '{
  "method": "tools/call",
  "params": {
    "name": "translate_batch_queries",
    "arguments": {
      // Provide these details according to the MCP tool specification.
    }
  },
  "jsonrpc": "2.0",
  "id": 1
}'
```

## Input Schema

Request message for TranslateBatchQueries.

### TranslateBatchQueriesRequest

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
  "targetBaseUri": string,
  "configurationFilePaths": [
    string
  ],
  "metadataFilePaths": [
    string
  ]
}
```

| Fields                     |                                                                                                                                                                                                                                                                                                                                                 |
|----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `projectNumber`            | `string` Required. The Google Cloud project number.                                                                                                                                                                                                                                                                                             |
| `location`                 | `string` Required. The location.                                                                                                                                                                                                                                                                                                                |
| `sourceDialect`            | `string` Required. The dialect of the source queries.                                                                                                                                                                                                                                                                                           |
| `targetDialect`            | `string` Required. The dialect of the target queries.                                                                                                                                                                                                                                                                                           |
| `sourceBaseUri[]`          | `string` Required. The Cloud Storage path containing the inputs. All files with this path will be included in the translation, including input queries, configuration files, and metadata files.                                                                                                                                                |
| `targetBaseUri`            | `string` Required. The base URI for all writes to persistent storage in Cloud Storage.                                                                                                                                                                                                                                                          |
| `configurationFilePaths[]` | `string` Optional. The Cloud Storage path of the configuration files for this batch translation. See [YAML configuration guidelines](https://docs.cloud.google.com/bigquery/docs/config-yaml-translation#yaml_guidelines) . Do not set this field if the configuration files are already located within a path specified in `source_base_uri` . |
| `metadataFilePaths[]`      | `string` Optional. The Cloud Storage path of the metadata files for this batch translation. See [Generate metadata](https://cloud.google.com/bigquery/docs/generate-metadata) . Do not set this field if the metadata files are already located within a path specified in `source_base_uri` .                                                  |

## Output Schema

Response message for TranslateBatchQueries.

### TranslateBatchQueriesResponse

**JSON representation**

```
{
  "translation": string,
  "translationState": string
}
```

| Fields             |                                                                               |
|--------------------|-------------------------------------------------------------------------------|
| `translation`      | `string` The ID of the migration workflow created for this batch translation. |
| `translationState` | `string` The current state of the translation workflow, typically `RUNNING` . |

### Tool Annotations

[Tool annotations](https://modelcontextprotocol.io/specification/latest/schema#toolannotations) are sent to MCP clients to describe the basic risk of a given tool. Most clients treat these hints as untrusted, but they can be used to decide when a confirmation prompt might be sent to a user.

Along with the title string, the following boolean hints are defined as follows:

- `readOnlyHint` : If true, the tool doesn't modify its environment. Default: false.
- `destructiveHint` : If true, then the tool can perform destructive actions. If false, then the tool can only perform additive actions. Default: true.
- `idempotentHint` : If true, then calling the tool repeatedly with the same arguments will have no additional effect on its environment. Default: false.
- `openWorldHint` : If true, then the tool can interact with an 'open world' of external entities. If false, then the tool can only interact with internal entities. For example, a web search tool would be open world, while a memory tool would not be open world.

Destructive Hint: ❌ \| Idempotent Hint: ❌ \| Read Only Hint: ❌ \| Open World Hint: ❌
