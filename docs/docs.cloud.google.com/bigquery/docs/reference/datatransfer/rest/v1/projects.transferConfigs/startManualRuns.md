---
name: documents/docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.transferConfigs/startManualRuns
uri: https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.transferConfigs/startManualRuns
title: 'Method: transferConfigs.startManualRuns'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [HTTP request](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.transferConfigs/startManualRuns#body.HTTP_TEMPLATE)
- [Path parameters](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.transferConfigs/startManualRuns#body.PATH_PARAMETERS)
- [Request body](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.transferConfigs/startManualRuns#body.request_body)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.transferConfigs/startManualRuns#body.request_body.SCHEMA_REPRESENTATION)
- [Response body](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.transferConfigs/startManualRuns#body.response_body)
- [Authorization scopes](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.transferConfigs/startManualRuns#body.aspect)
- [Try it!](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.transferConfigs/startManualRuns#try-it)

**Full name** : projects.transferConfigs.startManualRuns

Manually initiates transfer runs. You can schedule these runs in two ways:

1.  For a specific point in time using the 'requestedRunTime' parameter.
2.  For a period between 'startTime' (inclusive) and 'endTime' (exclusive).

If scheduling a single run, it is set to execute immediately (scheduleTime equals the current time). When scheduling multiple runs within a time range, the first run starts now, and subsequent runs are delayed by 15 seconds each.

### HTTP request

Choose an endpoint:

global asia-south1 asia-south2 europe-west1 europe-west2 europe-west3 europe-west4 europe-west6 europe-west8 europe-west9 me-central2 northamerica-northeast1 northamerica-northeast2 us-central1 us-central2 us-east1 us-east4 us-east5 us-east7 us-south1 us-west1 us-west2 us-west3 us-west4 us-west8

  
`POST https://bigquerydatatransfer.googleapis.com/v1/{parent=projects/*/transferConfigs/*}:startManualRuns`

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

  // The following is a list of mutually exclusive fields. At most one of the
  // fields will be set in a response:
  "requestedTimeRange": {
    object (TimeRange)
  },
  "requestedRunTime": string
  // End of mutually exclusive fields.
}
```

| Fields                                                                                                                                                                                         |                                                                                                                                                                                                                                                                                                                                                |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| The requested time specification - this can be a time range or a specific run_time. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response: |                                                                                                                                                                                                                                                                                                                                                |
| `requestedTimeRange`                                                                                                                                                                           | `object ( `[`TimeRange`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/TimeRange)` )` A time_range start and end timestamp for historical data files or reports that are scheduled to be transferred by the scheduled transfer run. requestedTimeRange must be a past time and cannot include future time values. |
| `requestedRunTime`                                                                                                                                                                             | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` A runTime timestamp for historical data files or reports that are scheduled to be transferred by the scheduled transfer run. requestedRunTime must be a past time and cannot include future time values.                                |
| End of mutually exclusive fields.                                                                                                                                                              |                                                                                                                                                                                                                                                                                                                                                |

### Response body

If successful, the response body contains an instance of [`StartManualTransferRunsResponse`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/StartManualTransferRunsResponse) .

### Authorization scopes

Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
