---
name: documents/docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/ScheduleTransferRunsResponse
uri: https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/ScheduleTransferRunsResponse
title: ScheduleTransferRunsResponse
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
update_time: "2025-10-17T21:03:01Z"
---

  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/ScheduleTransferRunsResponse#SCHEMA_REPRESENTATION)

A response to schedule transfer runs for a time range.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;runs&quot;: [{object (TransferRun)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`runs[]`

` object ( TransferRun  ` )

The transfer runs that were scheduled.
