---
name: documents/docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/SchedulingPolicy
uri: https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/SchedulingPolicy
title: SchedulingPolicy
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/SchedulingPolicy#SCHEMA_REPRESENTATION)

The scheduling policy controls how a reservation's resources are distributed.

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
  &quot;concurrency&quot;: string,
  &quot;maxSlots&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`concurrency`

`string ( int64 format)`

Optional. If present and \> 0, the reservation will attempt to limit the concurrency of jobs running for any particular project within it to the given value.

This feature is not yet generally available.

`maxSlots`

`string ( int64 format)`

Optional. If present and \> 0, the reservation will attempt to limit the slot consumption of queries running for any particular project within it to the given value.

This feature is not yet generally available.
