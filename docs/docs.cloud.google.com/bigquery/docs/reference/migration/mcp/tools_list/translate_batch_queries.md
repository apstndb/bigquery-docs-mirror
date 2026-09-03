---
name: documents/docs.cloud.google.com/bigquery/docs/reference/migration/mcp/tools_list/translate_batch_queries
uri: https://docs.cloud.google.com/bigquery/docs/reference/migration/mcp/tools_list/translate_batch_queries
title: 'MCP Tools Reference: bigquerymigration.googleapis.com'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

## Tool: `translate_batch_queries`

Translates a batch of SQL queries stored in Google Cloud Storage. **NOTE: This feature is experimental and in active development. It may not work correctly and should be used with caution.**

The following code sample shows how to use `curl` to call the `translate_batch_queries` MCP tool.

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
    &quot;name&quot;: &quot;translate_batch_queries&quot;,
    &quot;arguments&quot;: {
      // Provide these details according to the MCP tool specification.
    }
  },
  &quot;jsonrpc&quot;: &quot;2.0&quot;,
  &quot;id&quot;: 1
}&#39;</code></pre></td>
</tr>
</tbody>
</table>

## Input Schema

Request message for TranslateBatchQueries.

### TranslateBatchQueriesRequest

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
  &quot;sourceDialect&quot;: string,
  &quot;targetDialect&quot;: string,
  &quot;sourceBaseUri&quot;: [
    string
  ],
  &quot;targetBaseUri&quot;: string,
  &quot;configurationFilePaths&quot;: [
    string
  ],
  &quot;metadataFilePaths&quot;: [
    string
  ]
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

`sourceDialect`

`string`

Required. The dialect of the source queries.

`targetDialect`

`string`

Required. The dialect of the target queries.

`sourceBaseUri[]`

`string`

Required. The Cloud Storage path containing the inputs. All files with this path will be included in the translation, including input queries, configuration files, and metadata files.

`targetBaseUri`

`string`

Required. The base URI for all writes to persistent storage in Cloud Storage.

`configurationFilePaths[]`

`string`

Optional. The Cloud Storage path of the configuration files for this batch translation. See [YAML configuration guidelines](https://docs.cloud.google.com/bigquery/docs/config-yaml-translation#yaml_guidelines) .

Do not set this field if the configuration files are already located within a path specified in `source_base_uri` .

`metadataFilePaths[]`

`string`

Optional. The Cloud Storage path of the metadata files for this batch translation. See [Generate metadata](https://cloud.google.com/bigquery/docs/generate-metadata) .

Do not set this field if the metadata files are already located within a path specified in `source_base_uri` .

## Output Schema

Response message for TranslateBatchQueries.

### TranslateBatchQueriesResponse

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
  &quot;translation&quot;: string,
  &quot;translationState&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`translation`

`string`

The ID of the migration workflow created for this batch translation.

`translationState`

`string`

The current state of the translation workflow, typically `RUNNING` .

### Tool Annotations

[Tool annotations](https://modelcontextprotocol.io/specification/latest/schema#toolannotations) are sent to MCP clients to describe the basic risk of a given tool. Most clients treat these hints as untrusted, but they can be used to decide when a confirmation prompt might be sent to a user.

Along with the title string, the following boolean hints are defined as follows:

  - `readOnlyHint` : If true, the tool doesn't modify its environment. Default: false.
  - `destructiveHint` : If true, then the tool can perform destructive actions. If false, then the tool can only perform additive actions. Default: true.
  - `idempotentHint` : If true, then calling the tool repeatedly with the same arguments will have no additional effect on its environment. Default: false.
  - `openWorldHint` : If true, then the tool can interact with an 'open world' of external entities. If false, then the tool can only interact with internal entities. For example, a web search tool would be open world, while a memory tool would not be open world.

Destructive Hint: ❌ | Idempotent Hint: ❌ | Read Only Hint: ❌ | Open World Hint: ❌
