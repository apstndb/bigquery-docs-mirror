---
name: documents/docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/list_dataset_ids
uri: https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/list_dataset_ids
title: 'MCP Tools Reference: bigquery.googleapis.com'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

## Tool: `list_dataset_ids`

List BigQuery dataset IDs in a Google Cloud project. Supports pagination. Use `page_size` to limit results and `page_token` to retrieve next page.

The following code sample shows how to use `curl` to call the `list_dataset_ids` MCP tool.

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
<td><pre dir="ltr" data-is-upgraded="" data-syntax="Bash" translate="no"><code>curl --location &#39;https://bigquery.googleapis.com/mcp&#39; \
--header &#39;content-type: application/json&#39; \
--header &#39;accept: application/json, text/event-stream&#39; \
--data &#39;{
  &quot;method&quot;: &quot;tools/call&quot;,
  &quot;params&quot;: {
    &quot;name&quot;: &quot;list_dataset_ids&quot;,
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

Request for a list of datasets in a project.

### ListDatasetsRequest

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
  &quot;projectId&quot;: string,
  &quot;pageSize&quot;: integer,
  &quot;pageToken&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`projectId`

`string`

Required. Project ID of the dataset request.

`pageSize`

`integer`

Optional. The maximum number of results to return in a single response page. If unset, the default page size of 5000 is used.

`pageToken`

`string`

Optional. Page token, returned by a previous call, to request the next page of results.

## Output Schema

Response for a list of datasets.

### ListDatasetsResponse

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;datasets&quot;: [{object (ListFormatDataset)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`datasets[]`

` object ( ListFormatDataset  ` )

The datasets that matched the request.

`nextPageToken`

`string`

A token that can be used to request the next results page.

### ListFormatDataset

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
  &quot;id&quot;: string,
  &quot;friendlyName&quot;: string,
  &quot;location&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`id`

`string`

The ID of the dataset.

`friendlyName`

`string`

An alternate name for the dataset. The friendly name is purely decorative in nature. This can be useful to derive additional information about the dataset.

`location`

`string`

The geographic location where the dataset resides.

### StringValue

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
  &quot;value&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`value`

`string`

The string value.

### Tool Annotations

[Tool annotations](https://modelcontextprotocol.io/specification/latest/schema#toolannotations) are sent to MCP clients to describe the basic risk of a given tool. Most clients treat these hints as untrusted, but they can be used to decide when a confirmation prompt might be sent to a user.

Along with the title string, the following boolean hints are defined as follows:

  - `readOnlyHint` : If true, the tool doesn't modify its environment. Default: false.
  - `destructiveHint` : If true, then the tool can perform destructive actions. If false, then the tool can only perform additive actions. Default: true.
  - `idempotentHint` : If true, then calling the tool repeatedly with the same arguments will have no additional effect on its environment. Default: false.
  - `openWorldHint` : If true, then the tool can interact with an 'open world' of external entities. If false, then the tool can only interact with internal entities. For example, a web search tool would be open world, while a memory tool would not be open world.

Destructive Hint: ❌ | Idempotent Hint: ✅ | Read Only Hint: ✅ | Open World Hint: ❌
