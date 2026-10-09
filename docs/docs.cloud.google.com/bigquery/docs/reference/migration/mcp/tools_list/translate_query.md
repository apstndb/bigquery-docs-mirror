---
name: documents/docs.cloud.google.com/bigquery/docs/reference/migration/mcp/tools_list/translate_query
uri: https://docs.cloud.google.com/bigquery/docs/reference/migration/mcp/tools_list/translate_query
title: 'MCP Tools Reference: bigquerymigration.googleapis.com'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

## Tool: `translate_query`

Translates a single SQL query or script into BigQuery SQL. The translation runs asynchronously. Use the `get_translation` tool with the returned translation ID to poll its state until it is `SUCCEEDED` or `FAILED` . Wait at least two seconds before rechecking the state. To translate multiple queries, use the `translate_batch_queries` tool instead. A `SUCCEEDED` state means the translator finished, not that the output is correct. Check `translation_logs` before using the output. Entries with severity `ERROR` mark parts of the output that are best effort. `RelationNotFound` , `AttributeNotFound` and `MissingMetadataError` mean the translator didn't know the schema of a referenced table or column. Unresolved types can appear in the output as `ERROR_TYPE(...)` or `Error<error-type>` , which is not valid BigQuery SQL. To fix the error, provide the schema by using a metadata .ZIP file generated using the BigQuery Migration Service metadata extractor. Upload the file to Cloud Storage and pass the path to the file in `metadata_file_path` . If the user did not supply a metadata file, ask for it before guessing. Only when no metadata can be provided, use `generate_ddl_suggestion` to infer approximate DDL from the query. `NoSuchFunction` means a function the translator couldn't map was copied into the output verbatim, wrapped in backticks. This query should be rewritten manually. The output isn't validated against BigQuery so it must be validated by using a BigQuery dry run, before it is used.

The following code sample shows how to use `curl` to call the `translate_query` MCP tool.

**Curl Request**

```
curl --location 'https://bigquerymigration.googleapis.com/mcp' \
--header 'content-type: application/json' \
--header 'accept: application/json, text/event-stream' \
--data '{
  "method": "tools/call",
  "params": {
    "name": "translate_query",
    "arguments": {
      // Provide these details according to the MCP tool specification.
    }
  },
  "jsonrpc": "2.0",
  "id": 1
}'
```

## Input Schema

Request message for `TranslateQuery` .

### TranslateQueryRequest

**JSON representation**

```
{
  "projectNumber": string,
  "location": string,
  "inputQuery": string,
  "sourceDialect": string,
  "metadataFilePath": string,
  "translationConfigs": [
    {
      object (TranslationConfig)
    }
  ],
  "targetDialect": string
}
```

| Fields                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `projectNumber`        | `string` Required. The Google Cloud project number.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `location`             | `string` Required. The location. For more information, see [Locations](https://cloud.google.com/bigquery/docs/interactive-sql-translator#locations) .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `inputQuery`           | `string` Required. The SQL query or script to translate. If it references tables or columns, also provide their schema in `metadata_file_path` ; without it, name and type resolution is best effort.                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `sourceDialect`        | `string` Required. The dialect of the source query. The following source to target dialect pairs are supported: source: Teradata, Bteq, Redshift, Oracle, HiveQL, Impala, SparkSQL, Snowflake, Netezza, AzureSynapse, Vertica, SQLServer, Presto, MySQL, Postgresql, Db2, SQLite, Greenplum, BigQuery; target: BigQuery.                                                                                                                                                                                                                                                                                                                                            |
| `metadataFilePath`     | `string` Optional. The path to the metadata file in Cloud Storage. Format: `gs://BUCKET_NAME/PATH_TO_FILE.zip` . The metadata file contains the schema of the source database, which the translator needs to resolve the names and types of the tables and columns the query references. Without it, queries that reference tables are translated best effort and the logs report `RelationNotFound` , `AttributeNotFound` or `MissingMetadataError` . For more information on generating a metadata file, see [Generate metadata](https://cloud.google.com/bigquery/docs/generate-metadata) . Translation may fail if the metadata file isn't generated correctly. |
| `translationConfigs[]` | `object ( `[`TranslationConfig`](https://docs.cloud.google.com/bigquery/docs/reference/migration/mcp/tools_list/translate_query#Input.Schema.TranslationConfig)` )` Optional. Specifies the translation YAML configurations for this translation. For more information, see [YAML configuration guidelines](https://docs.cloud.google.com/bigquery/docs/config-yaml-translation#yaml_guidelines) .                                                                                                                                                                                                                                                                  |
| `targetDialect`        | `string` Required. The dialect of the target query. See list of supported pairs in source_dialect.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |

### TranslationConfig

**JSON representation**

```
{
  "displayName": string,
  "content": string
}
```

| Fields        |                                                                                                                     |
|---------------|---------------------------------------------------------------------------------------------------------------------|
| `displayName` | `string` Required. The display name of the configuration. Important: Name has to end with `.config.yaml` extension. |
| `content`     | `string` Required. The content of the configuration.                                                                |

## Output Schema

Response message for `TranslateQuery` .

### TranslateQueryResponse

**JSON representation**

```
{
  "translatedQuery": string,
  "translation": string,
  "translationState": string,
  "translationLogs": [
    {
      object (Log)
    }
  ],
  "errorInfo": {
    object (ErrorInfo)
  }
}
```

| Fields              |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `translatedQuery`   | `string` The translated query. It is not validated against BigQuery; check `translation_logs` for entries with severity `ERROR` before using it.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `translation`       | `string` The ID of the migration workflow created for this translation. Use this ID with `get_translation` and `explain_translation` tools.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `translationState`  | `string` The current state of the translation, for example, `SUCCEEDED` or `FAILED` .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `translationLogs[]` | `object ( `[`Log`](https://docs.cloud.google.com/bigquery/docs/reference/migration/mcp/tools_list/translate_query#Output.Schema.Log)` )` A list of logs generated during the translation process. Entries with severity `ERROR` mean the translated query contains unresolved, best-effort parts; `effect` says why: `COMPLETENESS` means the schema of a referenced object was missing (see `metadata_file_path` ), `CORRECTNESS` means the translator could not process part of the input, and `COMPATIBILITY` means a feature was approximated for BigQuery. Tip: If you're using an AI client, these logs can be used to troubleshoot issues and to improve translation quality. You should persist these logs so users can see them in the UI and use them for troubleshooting or improving translation quality. |
| `errorInfo`         | `object ( `[`ErrorInfo`](https://docs.cloud.google.com/bigquery/docs/reference/migration/mcp/tools_list/translate_query#Output.Schema.ErrorInfo)` )` The error information.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |

### Log

**JSON representation**

```
{
  "severity": string,
  "category": string,
  "message": string,
  "action": string,
  "effect": string,
  "impactedObject": string
}
```

| Fields           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `severity`       | `string` Severity of the translation record, for example, `INFO` , `WARNING` , or `ERROR` .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `category`       | `string` Category of the error or warning, for example, `SyntaxError` .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `message`        | `string` Detailed message of the record.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `action`         | `string` Recommended action to address the log.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `effect`         | `string` The effect or impact of the issue noted in the log. Effect can be one of the following values: `CORRECTNESS` : Errors with this effect indicate that the translation service couldn't meaningfully process the translation. This is caused by issues in the user's input such as incorrect language or formatting, or using an unsupported file type. `COMPLETENESS` : Errors with this effect indicate that the translation service doesn't have sufficient information to complete the translation. This can be caused by missing information in the user's input such as missing metadata for name resolution. `COMPATIBILITY` : Errors with this effect indicate that the translation service encountered compatibility issues when it processed the translation. This can happen when the target platform doesn't support a feature used in the input script, and the translation service tries to make a semantic approximation for the target platform. `NONE` : Errors with this effect are purely informational messages that have no effect on the output. Effects are ordered by their stage in the translation process. For example, `CORRECTNESS` issues are identified before `COMPLETENESS` issues. |
| `impactedObject` | `string` Name of the object that is impacted by the log message.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |

### ErrorInfo

**JSON representation**

```
{
  "reason": string,
  "domain": string,
  "metadata": {
    string: string,
    ...
  }
}
```

| Fields     |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `reason`   | `string` The reason for the error. This is a constant value that identifies the proximate cause of the error. Error reasons are unique within a particular domain of errors. This should be at most 63 characters and match a regular expression of `[A-Z][A-Z0-9_]+[A-Z0-9]` , which represents UPPER_SNAKE_CASE.                                                                                                                                                                                                                                                                                                                                                                                               |
| `domain`   | `string` The logical grouping to which the "reason" belongs. The error domain is typically the registered service name of the tool or product that generates the error. Example: "pubsub.googleapis.com". If the error is generated by some common infrastructure, the error domain must be a globally unique value that identifies the infrastructure. For Google API infrastructure, the error domain is "googleapis.com".                                                                                                                                                                                                                                                                                     |
| `metadata` | `map (key: string, value: string)` Additional structured details about this error. Keys must match a regular expression of `[a-z][a-zA-Z0-9-_]+` but should ideally be lowerCamelCase. Also, they must be limited to 64 characters in length. When identifying the current value of an exceeded limit, the units should be contained in the key, not the value. For example, rather than `{"instanceLimit": "100/request"}` , should be returned as, `{"instanceLimitPerRequest": "100"}` , if the client exceeds the number of instances that can be created in a single (batch) request. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |

### MetadataEntry

**JSON representation**

```
{
  "key": string,
  "value": string
}
```

| Fields  |          |
|---------|----------|
| `key`   | `string` |
| `value` | `string` |

### Tool Annotations

[Tool annotations](https://modelcontextprotocol.io/specification/latest/schema#toolannotations) are sent to MCP clients to describe the basic risk of a given tool. Most clients treat these hints as untrusted, but they can be used to decide when a confirmation prompt might be sent to a user.

Along with the title string, the following boolean hints are defined as follows:

- `readOnlyHint` : If true, the tool doesn't modify its environment. Default: false.
- `destructiveHint` : If true, then the tool can perform destructive actions. If false, then the tool can only perform additive actions. Default: true.
- `idempotentHint` : If true, then calling the tool repeatedly with the same arguments will have no additional effect on its environment. Default: false.
- `openWorldHint` : If true, then the tool can interact with an 'open world' of external entities. If false, then the tool can only interact with internal entities. For example, a web search tool would be open world, while a memory tool would not be open world.

Destructive Hint: ❌ \| Idempotent Hint: ❌ \| Read Only Hint: ❌ \| Open World Hint: ❌
