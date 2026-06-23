---
name: documents/docs.cloud.google.com/bigquery/docs/reference/datatransfer/mcp/tools_list/delete_transfer_run
uri: https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/mcp/tools_list/delete_transfer_run
title: 'MCP Tools Reference: bigquerydatatransfer.googleapis.com'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

## Tool: `delete_transfer_run`

Delete a transfer run.

The following example shows an MCP call to delete a transfer run by its resource name.

`delete_transfer_run(name="projects/myproject/locations/myregion/transferConfigs/mytransferconfig/runs/mytransferrun")`

The following sample demonstrate how to use `curl` to invoke the `delete_transfer_run` MCP tool.

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
curl --location &#39;https://bigquerydatatransfer.googleapis.com/mcp&#39; \
--header &#39;content-type: application/json&#39; \
--header &#39;accept: application/json, text/event-stream&#39; \
--data &#39;{
  &quot;method&quot;: &quot;tools/call&quot;,
  &quot;params&quot;: {
    &quot;name&quot;: &quot;delete_transfer_run&quot;,
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

A request to delete data transfer run information.

### DeleteTransferRunRequest

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
  &quot;name&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

Required. The name of the resource requested. If you are using the regionless method, the location must be `US` and the name should be in the following form:

  - `projects/{project_id}/transferConfigs/{config_id}/runs/{run_id}`

If you are using the regionalized method, the name should be in the following form:

  - `projects/{project_id}/locations/{location_id}/transferConfigs/{config_id}/runs/{run_id}`

## Output Schema

A generic empty message that you can re-use to avoid defining duplicated empty messages in your APIs. A typical example is to use it as the request or the response type of an API method. For instance:

    service Foo {
      rpc Bar(google.protobuf.Empty) returns (google.protobuf.Empty);
    }

### Tool Annotations

Destructive Hint: ✅ | Idempotent Hint: ❌ | Read Only Hint: ❌ | Open World Hint: ❌
