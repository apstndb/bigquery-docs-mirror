---
name: documents/docs.cloud.google.com/bigquery/docs/reference/datatransfer/mcp/tools_list/list_transfer_logs
uri: https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/mcp/tools_list/list_transfer_logs
title: 'MCP Tools Reference: bigquerydatatransfer.googleapis.com'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

## Tool: `list_transfer_logs`

List transfer logs for a transfer run by its resource name.

The following example shows a MCP call to list transfer logs for a transfer run.

`list_transfer_logs(parent="projects/myproject/locations/myregion/transferConfigs/mytransferconfig/runs/mytransferrun")`

The following sample demonstrate how to use `curl` to invoke the `list_transfer_logs` MCP tool.

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
    &quot;name&quot;: &quot;list_transfer_logs&quot;,
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

A request to get user facing log messages associated with data transfer run.

### ListTransferLogsRequest

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;parent&quot;: string,&quot;pageToken&quot;: string,&quot;pageSize&quot;: integer,&quot;messageTypes&quot;: [enum (MessageSeverity)]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`parent`

`string`

Required. Transfer run name. If you are using the regionless method, the location must be `US` and the name should be in the following form:

  - `projects/{project_id}/transferConfigs/{config_id}/runs/{run_id}`

If you are using the regionalized method, the name should be in the following form:

  - `projects/{project_id}/locations/{location_id}/transferConfigs/{config_id}/runs/{run_id}`

`pageToken`

`string`

Pagination token, which can be used to request a specific page of `ListTransferLogsRequest` list results. For multiple-page results, `ListTransferLogsResponse` outputs a `next_page` token, which can be used as the `page_token` value to request the next page of list results.

`pageSize`

`integer`

Page size. The default page size is the maximum value of 1000 results.

`messageTypes[]`

` enum ( MessageSeverity  ` )

Message types to return. If not populated - INFO, WARNING and ERROR messages are returned.

### MessageSeverity

Represents data transfer user facing message severity.

Enums

`MESSAGE_SEVERITY_UNSPECIFIED`

No severity specified.

`INFO`

Informational message.

`WARNING`

Warning message.

`ERROR`

Error message.

## Output Schema

The returned list transfer run messages.

### ListTransferLogsResponse

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;transferMessages&quot;: [{object (TransferMessage)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`transferMessages[]`

` object ( TransferMessage  ` )

Output only. The stored pipeline transfer messages.

`nextPageToken`

`string`

Output only. The next-pagination token. For multiple-page list results, this token can be used as the `GetTransferRunLogRequest.page_token` to request the next page of list results.

### TransferMessage

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;messageTime&quot;: string,&quot;severity&quot;: enum (MessageSeverity),&quot;messageText&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`messageTime`

` string ( Timestamp  ` format)

Time when message was logged.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`severity`

` enum ( MessageSeverity  ` )

Message severity.

`messageText`

`string`

Message text.

### Timestamp

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
  &quot;seconds&quot;: string,
  &quot;nanos&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`seconds`

`string ( int64 format)`

Represents seconds of UTC time since Unix epoch 1970-01-01T00:00:00Z. Must be between -62135596800 and 253402300799 inclusive (which corresponds to 0001-01-01T00:00:00Z to 9999-12-31T23:59:59Z).

`nanos`

`integer`

Non-negative fractions of a second at nanosecond resolution. This field is the nanosecond portion of the duration, not an alternative to seconds. Negative second values with fractions must still have non-negative nanos values that count forward in time. Must be between 0 and 999,999,999 inclusive.

### MessageSeverity

Represents data transfer user facing message severity.

Enums

`MESSAGE_SEVERITY_UNSPECIFIED`

No severity specified.

`INFO`

Informational message.

`WARNING`

Warning message.

`ERROR`

Error message.

### Tool Annotations

Destructive Hint: ❌ | Idempotent Hint: ✅ | Read Only Hint: ✅ | Open World Hint: ❌
