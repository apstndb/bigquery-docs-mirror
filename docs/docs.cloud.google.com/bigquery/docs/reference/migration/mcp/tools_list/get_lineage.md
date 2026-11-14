---
name: documents/docs.cloud.google.com/bigquery/docs/reference/migration/mcp/tools_list/get_lineage
uri: https://docs.cloud.google.com/bigquery/docs/reference/migration/mcp/tools_list/get_lineage
title: 'MCP Tools Reference: bigquerymigration.googleapis.com'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

## Tool: `get_lineage`

Retrieves the job state and the results of a lineage tracing job that is created by the `trace_lineage` tool. If the state is not yet `SUCCEEDED` or `FAILED` , wait at least 30 seconds before rechecking the state. When the state is `SUCCEEDED` , give the user the `lineage.webapp_uri` value. The URL in `lineage.webapp_uri` opens the interactive lineage graph. The user needs the `bigquerymigration.lineageDbs.query` IAM permission to open it. Check `lineage.recognized_inputs` to confirm that the expected metadata, query logs, or SQL scripts were found. If an input type is missing, verify that the files were uploaded in the correct format in `source_base_uri` . SQL scripts are traced only if their Cloud Storage path includes a folder named after their SQL dialect, such as `teradata` in `gs://my_bucket/input/teradata/script.sql` . `lineage.progress_reports` break down the work by processing stage. Work in state `SKIPPED` or `FAILED` means the lineage graph is incomplete. This tool doesn't return the lineage graph itself.

The following code sample shows how to use `curl` to call the `get_lineage` MCP tool.

**Curl Request**

```
curl --location 'https://bigquerymigration.googleapis.com/mcp' \
--header 'content-type: application/json' \
--header 'accept: application/json, text/event-stream' \
--data '{
  "method": "tools/call",
  "params": {
    "name": "get_lineage",
    "arguments": {
      // Provide these details according to the MCP tool specification.
    }
  },
  "jsonrpc": "2.0",
  "id": 1
}'
```

## Input Schema

Request message for `FetchLineage` .

### FetchLineageRequest

**JSON representation**

```
{
  "projectNumber": string,
  "location": string,
  "lineage": string
}
```

| Fields          |                                                                           |
|-----------------|---------------------------------------------------------------------------|
| `projectNumber` | `string` Required. The Google Cloud project number.                       |
| `location`      | `string` Required. The location.                                          |
| `lineage`       | `string` Required. The lineage ID returned in `name` by `trace_lineage` . |

## Output Schema

Response message for `FetchLineage` .

### FetchLineageResponse

**JSON representation**

```
{
  "lineage": {
    object (Lineage)
  },
  "errorInfo": {
    object (ErrorInfo)
  }
}
```

| Fields      |                                                                                                                                                                                                       |
|-------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `lineage`   | `object ( `[`Lineage`](https://docs.cloud.google.com/bigquery/docs/reference/migration/mcp/tools_list/get_lineage#Output.Schema.Lineage)` )` The lineage resource.                                    |
| `errorInfo` | `object ( `[`ErrorInfo`](https://docs.cloud.google.com/bigquery/docs/reference/migration/mcp/tools_list/translate_query#Output.Schema.ErrorInfo)` )` The error information if the lineage job failed. |

### Lineage

**JSON representation**

```
{
  "lineage": string,
  "state": enum (State),
  "webappUri": string,
  "consoleUri": string,
  "recognizedInputs": [
    {
      object (LineageInput)
    }
  ],
  "progressReports": [
    {
      object (LineageProgressReport)
    }
  ]
}
```

| Fields               |                                                                                                                                                                                                                                                                                                                                     |
|----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `lineage`            | `string` The ID of the lineage job.                                                                                                                                                                                                                                                                                                 |
| `state`              | `enum ( `[`State`](https://docs.cloud.google.com/bigquery/docs/reference/migration/mcp/tools_list/get_lineage#Output.Schema.State)` )` Output only. The current state of the lineage job.                                                                                                                                           |
| `webappUri`          | `string` The URI of the web app that visualizes the traced lineage. It is set as soon as the lineage service starts producing output, but the graph is complete only when `state` is `SUCCEEDED` . Give this URI to the user. The user needs the `bigquerymigration.lineageDbs.query` IAM permission to open it.                    |
| `consoleUri`         | `string` The Google Cloud console URI of the lineage job.                                                                                                                                                                                                                                                                           |
| `recognizedInputs[]` | `object ( `[`LineageInput`](https://docs.cloud.google.com/bigquery/docs/reference/migration/mcp/tools_list/get_lineage#Output.Schema.LineageInput)` )` The inputs that the lineage service recognized, by type. If an expected type is missing, verify that the files were uploaded in the correct format under `source_base_uri` . |
| `progressReports[]`  | `object ( `[`LineageProgressReport`](https://docs.cloud.google.com/bigquery/docs/reference/migration/mcp/tools_list/get_lineage#Output.Schema.LineageProgressReport)` )` Work processing progress reports broken up by processing stage. Work in state `SKIPPED` or `FAILED` means the lineage graph is incomplete.                 |

### LineageInput

**JSON representation**

```
{
  "type": enum (Type),
  "uncompressedSizeBytes": string
}
```

| Fields                  |                                                                                                                                                                   |
|-------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `type`                  | `enum ( `[`Type`](https://docs.cloud.google.com/bigquery/docs/reference/migration/mcp/tools_list/get_lineage#Output.Schema.Type)` )` The type of the input.       |
| `uncompressedSizeBytes` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` The uncompressed size of the recognized input of the given type, in bytes. |

### LineageProgressReport

**JSON representation**

```
{
  "processingStage": enum (ProcessingStage),
  "workSummaries": [
    {
      object (LineageWorkSummary)
    }
  ]
}
```

| Fields            |                                                                                                                                                                                                                                                                                                                         |
|-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `processingStage` | `enum ( `[`ProcessingStage`](https://docs.cloud.google.com/bigquery/docs/reference/migration/mcp/tools_list/get_lineage#Output.Schema.ProcessingStage)` )` The processing stage.                                                                                                                                        |
| `workSummaries[]` | `object ( `[`LineageWorkSummary`](https://docs.cloud.google.com/bigquery/docs/reference/migration/mcp/tools_list/get_lineage#Output.Schema.LineageWorkSummary)` )` Summaries of work broken up by the state of the work. Aggregate `work_unit_count` across all summaries to get the total amount of work in the stage. |

### LineageWorkSummary

**JSON representation**

```
{
  "state": enum (State),
  "workUnitCount": string,
  "comment": string
}
```

| Fields          |                                                                                                                                                                              |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `state`         | `enum ( `[`State`](https://docs.cloud.google.com/bigquery/docs/reference/migration/mcp/tools_list/get_lineage#Output.Schema.State_1)` )` Output only. The state of the work. |
| `workUnitCount` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` The number of units of work in this state.                                            |
| `comment`       | `string` Human-readable comment.                                                                                                                                             |

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

### State

The state of the lineage job.

| Enums               |                                              |
|---------------------|----------------------------------------------|
| `STATE_UNSPECIFIED` | The state of the lineage job is unspecified. |
| `PENDING`           | The lineage job is pending execution.        |
| `RUNNING`           | The lineage job is currently running.        |
| `PAUSED`            | The lineage job is paused.                   |
| `SUCCEEDED`         | The lineage job completed successfully.      |
| `FAILED`            | The lineage job failed.                      |

### Type

The type of the lineage input.

| Enums              |                                                                |
|--------------------|----------------------------------------------------------------|
| `TYPE_UNSPECIFIED` | The input type is unspecified.                                 |
| `METADATA`         | Schema metadata extracted from the source data warehouse.      |
| `QUERY_LOG`        | Query execution logs extracted from the source data warehouse. |
| `SCRIPT`           | SQL script files.                                              |

### ProcessingStage

The processing stage of the lineage job.

| Enums                          |                                                           |
|--------------------------------|-----------------------------------------------------------|
| `PROCESSING_STAGE_UNSPECIFIED` | The processing stage is unspecified.                      |
| `INPUT_INGESTION`              | Ingestion of input metadata, query logs, and scripts.     |
| `POSTPROCESSING`               | Postprocessing of ingested inputs into the lineage graph. |

### State

The state of the lineage work.

| Enums               |                                                                             |
|---------------------|-----------------------------------------------------------------------------|
| `STATE_UNSPECIFIED` | The work state is unspecified.                                              |
| `SUCCEEDED`         | The work completed successfully.                                            |
| `FAILED`            | The work failed.                                                            |
| `IN_PROGRESS`       | The work is currently in progress.                                          |
| `SKIPPED`           | The work was recognized as necessary but skipped due to system limitations. |

### Tool Annotations

[Tool annotations](https://modelcontextprotocol.io/specification/latest/schema#toolannotations) are sent to MCP clients to describe the basic risk of a given tool. Most clients treat these hints as untrusted, but they can be used to decide when a confirmation prompt might be sent to a user.

Along with the title string, the following boolean hints are defined as follows:

- `readOnlyHint` : If true, the tool doesn't modify its environment. Default: false.
- `destructiveHint` : If true, then the tool can perform destructive actions. If false, then the tool can only perform additive actions. Default: true.
- `idempotentHint` : If true, then calling the tool repeatedly with the same arguments will have no additional effect on its environment. Default: false.
- `openWorldHint` : If true, then the tool can interact with an 'open world' of external entities. If false, then the tool can only interact with internal entities. For example, a web search tool would be open world, while a memory tool would not be open world.

Destructive Hint: ❌ \| Idempotent Hint: ✅ \| Read Only Hint: ✅ \| Open World Hint: ❌
