---
name: documents/docs.cloud.google.com/bigquery/docs/reference/migration/mcp/tools_list/explain_translation
uri: https://docs.cloud.google.com/bigquery/docs/reference/migration/mcp/tools_list/explain_translation
title: 'MCP Tools Reference: bigquerymigration.googleapis.com'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

## Tool: `explain_translation`

Explains the SQL translation for a given translation ID.

The following sample demonstrate how to use `curl` to invoke the `explain_translation` MCP tool.

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
<td><pre dir="ltr" data-is-upgraded="" data-syntax="Bash" translate="no"><code>                  
curl --location &#39;https://bigquerymigration.googleapis.com/mcp&#39; \
--header &#39;content-type: application/json&#39; \
--header &#39;accept: application/json, text/event-stream&#39; \
--data &#39;{
  &quot;method&quot;: &quot;tools/call&quot;,
  &quot;params&quot;: {
    &quot;name&quot;: &quot;explain_translation&quot;,
    &quot;arguments&quot;: {
      // provide these details according to the tool&#39;s MCP specification
    }
  },
  &quot;jsonrpc&quot;: &quot;2.0&quot;,
  &quot;id&quot;: 1
}&#39;
                </code></pre></td>
</tr>
</tbody>
</table>

## Input Schema

Request message for `ExplainTranslation` .

### ExplainTranslationRequest

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
  &quot;translation&quot;: string
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

`translation`

`string`

Required. The translation ID.

## Output Schema

Response message for `ExplainTranslation` .

### ExplainTranslationResponse

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
  &quot;explanation&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`explanation`

`string`

The string that explains the translation.

### Tool Annotations

Destructive Hint: ❌ | Idempotent Hint: ✅ | Read Only Hint: ✅ | Open World Hint: ❌
