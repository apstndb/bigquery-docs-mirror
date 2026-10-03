---
name: documents/docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs/scheduleRuns
uri: https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs/scheduleRuns
title: 'Method: transferConfigs.scheduleRuns'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [HTTP request](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs/scheduleRuns#body.HTTP_TEMPLATE)
- [Path parameters](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs/scheduleRuns#body.PATH_PARAMETERS)
- [Request body](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs/scheduleRuns#body.request_body)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs/scheduleRuns#body.request_body.SCHEMA_REPRESENTATION)
- [Response body](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs/scheduleRuns#body.response_body)
- [Authorization scopes](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs/scheduleRuns#body.aspect)
- [Try it!](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs/scheduleRuns#try-it)

> This item is deprecated!

**Full name** : projects.locations.transferConfigs.scheduleRuns

Creates transfer runs for a time range \[startTime, endTime\]. For each date - or whatever granularity the data source supports - in the range, one transfer run is created. Note that runs are created per UTC time in the time range. DEPRECATED: use transferConfigs.startManualRuns instead.

### HTTP request

Choose an endpoint:

global asia-south1 asia-south2 europe-west1 europe-west2 europe-west3 europe-west4 europe-west6 europe-west8 europe-west9 me-central2 northamerica-northeast1 northamerica-northeast2 us-central1 us-central2 us-east1 us-east4 us-east5 us-east7 us-south1 us-west1 us-west2 us-west3 us-west4 us-west8

  
`POST https://bigquerydatatransfer.googleapis.com/v1/{parent=projects/*/locations/*/transferConfigs/*}:scheduleRuns`

The URLs use [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Parameters</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>parent</code></td>
<td><p><code>string</code></p>
<p>Required. Transfer configuration name. If you are using the regionless method, the location must be <code>US</code> and the name should be in the following form:</p>
<ul>
<li><code>projects/{projectId}/transferConfigs/{configId}</code></li>
</ul>
<p>If you are using the regionalized method, the name should be in the following form:</p>
<ul>
<li><code>projects/{projectId}/locations/{locationId}/transferConfigs/{configId}</code></li>
</ul>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>bigquery.transfers.update</code></li>
</ul></td>
</tr>
</tbody>
</table>

### Request body

The request body contains data with the following structure:

**JSON representation**

```
{
  "startTime": string,
  "endTime": string
}
```

| Fields      |                                                                                                                                                                                                         |
|-------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `startTime` | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Required. Start time of the range of transfer runs. For example, `"2017-05-25T00:00:00+00:00"` . |
| `endTime`   | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Required. End time of the range of transfer runs. For example, `"2017-05-30T00:00:00+00:00"` .   |

### Response body

If successful, the response body contains an instance of [`ScheduleTransferRunsResponse`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/ScheduleTransferRunsResponse) .

### Authorization scopes

Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
