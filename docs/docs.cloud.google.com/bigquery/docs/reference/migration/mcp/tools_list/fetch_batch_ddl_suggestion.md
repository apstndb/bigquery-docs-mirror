---
name: documents/docs.cloud.google.com/bigquery/docs/reference/migration/mcp/tools_list/fetch_batch_ddl_suggestion
uri: https://docs.cloud.google.com/bigquery/docs/reference/migration/mcp/tools_list/fetch_batch_ddl_suggestion
title: 'MCP Tools Reference: bigquerymigration.googleapis.com'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

## Tool: `fetch_batch_ddl_suggestion`

Retrieves the status and logs of a batch DDL suggestion workflow. **NOTE: This feature is experimental and in active development. It may not work correctly and should be used with caution.**

The following code sample shows how to use `curl` to call the `fetch_batch_ddl_suggestion` MCP tool.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Curl Request</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" data-syntax="Bash" translate="no"><code>curl --location &#39;https://bigquerymigration.googleapis.com/mcp&#39; \
--header &#39;content-type: application/json&#39; \
--header &#39;accept: application/json, text/event-stream&#39; \
--data &#39;{
  &quot;method&quot;: &quot;tools/call&quot;,
  &quot;params&quot;: {
    &quot;name&quot;: &quot;fetch_batch_ddl_suggestion&quot;,
    &quot;arguments&quot;: {
      // provide these details according to the tool&#39;s MCP specification
    }
  },
  &quot;jsonrpc&quot;: &quot;2.0&quot;,
  &quot;id&quot;: 1
}&#39;</code></pre></td>
</tr>
</tbody>
</table>

## Input Schema

Request message for `FetchBatchDdlSuggestion` .

### FetchBatchDdlSuggestionRequest

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;projectNumber&quot;: string,
  &quot;location&quot;: string,
  &quot;suggestion&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`projectNumber`

`string`

Required. The Google Cloud project number.

`location`

`string`

Required. The location.

`suggestion`

`string`

Required. The suggestion ID of the batch workflow.

## Output Schema

Response message for `FetchBatchDdlSuggestion` .

### FetchBatchDdlSuggestionResponse

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;suggestion&quot;: {object (BatchSuggestion)},&quot;logs&quot;: [{object (Log)}],&quot;errorInfo&quot;: {object (ErrorInfo)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`suggestion`

` object ( BatchSuggestion  ` )

The batch suggestion resource.

`logs[]`

` object ( Log  ` )

A summary list of logs generated during the batch suggestion process.

`errorInfo`

` object ( ErrorInfo  ` )

The error information if the workflow itself failed to orchestrate.

### BatchSuggestion

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;suggestion&quot;: string,
  &quot;state&quot;: string,
  &quot;cloudStorageUri&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`suggestion`

`string`

The ID of the batch suggestion.

`state`

`string`

The current state of the batch suggestion workflow, for example, `RUNNING` , `SUCCEEDED` , or `FAILED` .

`cloudStorageUri`

`string`

The Cloud Storage URI of the folder containing the generated suggestion outputs. AI INSTRUCTION: Download the outputs from this URI to get the suggestion content and logs. Ask the user to review the generated DDL suggestions. If the user is satisfied, upload the DDL suggestions into one of the directory under the source\_base\_uri then trigger a new batch translation with the generated DDL suggestions.

### Log

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;severity&quot;: string,
  &quot;category&quot;: string,
  &quot;message&quot;: string,
  &quot;action&quot;: string,
  &quot;effect&quot;: string,
  &quot;impactedObject&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`severity`

`string`

Severity of the translation record, for example, `INFO` , `WARNING` , or `ERROR` .

`category`

`string`

Category of the error or warning, for example, `SyntaxError` .

`message`

`string`

Detailed message of the record.

`action`

`string`

Recommended action to address the log.

`effect`

`string`

The effect or impact of the issue noted in the log. Effect can be one of the following values: `CORRECTNESS` : Errors with this effect indicate that the translation service couldn't meaningfully process the translation. This is caused by issues in the user's input such as incorrect language or formatting, or using an unsupported file type. `COMPLETENESS` : Errors with this effect indicate that the translation service doesn't have sufficient information to complete the translation. This can be caused by missing information in the user's input such as missing metadata for name resolution. `COMPATIBILITY` : Errors with this effect indicate that the translation service encountered compatibility issues when it processed the translation. This can happen when the target platform doesn't support a feature used in the input script, and the translation service tries to make a semantic approximation for the target platform. `NONE` : Errors with this effect are purely informational messages that have no effect on the output. Effects are ordered by their stage in the translation process. For example, `CORRECTNESS` issues are identified before `COMPLETENESS` issues.

`impactedObject`

`string`

Name of the object that is impacted by the log message.

### ErrorInfo

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;reason&quot;: string,
  &quot;domain&quot;: string,
  &quot;metadata&quot;: {
    string: string,
    ...
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`reason`

`string`

The reason for the error. This is a constant value that identifies the proximate cause of the error. Error reasons are unique within a particular domain of errors. This should be at most 63 characters and match a regular expression of `[A-Z][A-Z0-9_]+[A-Z0-9]` , which represents UPPER\_SNAKE\_CASE.

`domain`

`string`

The logical grouping to which the "reason" belongs. The error domain is typically the registered service name of the tool or product that generates the error. Example: "pubsub.googleapis.com". If the error is generated by some common infrastructure, the error domain must be a globally unique value that identifies the infrastructure. For Google API infrastructure, the error domain is "googleapis.com".

`metadata`

`map (key: string, value: string)`

Additional structured details about this error.

Keys must match a regular expression of `[a-z][a-zA-Z0-9-_]+` but should ideally be lowerCamelCase. Also, they must be limited to 64 characters in length. When identifying the current value of an exceeded limit, the units should be contained in the key, not the value. For example, rather than `{"instanceLimit": "100/request"}` , should be returned as, `{"instanceLimitPerRequest": "100"}` , if the client exceeds the number of instances that can be created in a single (batch) request.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

### MetadataEntry

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;key&quot;: string,
  &quot;value&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

`string`

### Tool Annotations

[Tool annotations](https://modelcontextprotocol.io/specification/latest/schema#toolannotations) are sent to MCP clients to describe the basic risk of a given tool. Most clients treat these hints as untrusted, but they can be used to decide when a confirmation prompt might be sent to a user.

Along with the title string, the following boolean hints are defined as follows:

  - `readOnlyHint` : If true, the tool doesn't modify its environment. Default: false.
  - `destructiveHint` : If true, then the tool can perform destructive actions. If false, then the tool can only perform additive actions. Default: true.
  - `idempotentHint` : If true, then calling the tool repeatedly with the same arguments will have no additional effect on its environment. Default: false.
  - `openWorldHint` : If true, then the tool can interact with an 'open world' of external entities. If false, then the tool can only interact with internal entities. For example, a web search tool would be open world, while a memory tool would not be open world.

Destructive Hint: ❌ | Idempotent Hint: ✅ | Read Only Hint: ✅ | Open World Hint: ❌
