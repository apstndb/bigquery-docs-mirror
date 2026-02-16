  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Request body](#body.request_body)
      - [JSON representation](#body.request_body.SCHEMA_REPRESENTATION)
  - [Response body](#body.response_body)
  - [Authorization scopes](#body.aspect)
  - [Try it\!](#try-it)

**Full name** : projects.locations.transferConfigs.startManualRuns

Manually initiates transfer runs. You can schedule these runs in two ways:

1.  For a specific point in time using the 'requestedRunTime' parameter.
2.  For a period between 'startTime' (inclusive) and 'endTime' (exclusive).

If scheduling a single run, it is set to execute immediately (scheduleTime equals the current time). When scheduling multiple runs within a time range, the first run starts now, and subsequent runs are delayed by 15 seconds each.

### HTTP request

`  POST https://bigquerydatatransfer.googleapis.com/v1/{parent=projects/*/locations/*/transferConfigs/*}:startManualRuns  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  parent  `

`  string  `

Required. Transfer configuration name. If you are using the regionless method, the location must be `  US  ` and the name should be in the following form:

  - `  projects/{projectId}/transferConfigs/{configId}  `

If you are using the regionalized method, the name should be in the following form:

  - `  projects/{projectId}/locations/{locationId}/transferConfigs/{configId}  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  parent  ` :

  - `  bigquery.transfers.update  `

### Request body

The request body contains data with the following structure:

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
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{

  // Union field time can be only one of the following:
  &quot;requestedTimeRange&quot;: {
    object (TimeRange)
  },
  &quot;requestedRunTime&quot;: string
  // End of list of possible types for union field time.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `  time  ` . The requested time specification - this can be a time range or a specific run\_time. `  time  ` can be only one of the following:

`  requestedTimeRange  `

`  object ( TimeRange  ` )

A time\_range start and end timestamp for historical data files or reports that are scheduled to be transferred by the scheduled transfer run. requestedTimeRange must be a past time and cannot include future time values.

`  requestedRunTime  `

`  string ( Timestamp  ` format)

A runTime timestamp for historical data files or reports that are scheduled to be transferred by the scheduled transfer run. requestedRunTime must be a past time and cannot include future time values.

### Response body

If successful, the response body contains an instance of `  StartManualTransferRunsResponse  ` .

### Authorization scopes

Requires the following OAuth scope:

  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
