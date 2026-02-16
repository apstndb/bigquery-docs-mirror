  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Request body](#body.request_body)
      - [JSON representation](#body.request_body.SCHEMA_REPRESENTATION)
  - [Response body](#body.response_body)
      - [JSON representation](#body.SplitCapacityCommitmentResponse.SCHEMA_REPRESENTATION)
  - [Authorization scopes](#body.aspect)
  - [Try it\!](#try-it)

Splits capacity commitment to two commitments of the same plan and `  commitmentEndTime  ` .

A common use case is to enable downgrading commitments.

For example, in order to downgrade from 10000 slots to 8000, you might split a 10000 capacity commitment into commitments of 2000 and 8000. Then, you delete the first one after the commitment end time passes.

### HTTP request

`  POST https://bigqueryreservation.googleapis.com/v1/{name=projects/*/locations/*/capacityCommitments/*}:split  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  name  `

`  string  `

Required. The resource name e.g.,: `  projects/myproject/locations/US/capacityCommitments/123  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  name  ` :

  - `  bigquery.capacityCommitments.update  `

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
  &quot;slotCount&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  slotCount  `

`  string ( int64 format)  `

Number of slots in the capacity commitment after the split.

### Response body

The response for `  ReservationService.SplitCapacityCommitment  ` .

If successful, the response body contains data with the following structure:

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
  &quot;first&quot;: {
    object (CapacityCommitment)
  },
  &quot;second&quot;: {
    object (CapacityCommitment)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  first  `

`  object ( CapacityCommitment  ` )

First capacity commitment, result of a split.

`  second  `

`  object ( CapacityCommitment  ` )

Second capacity commitment, result of a split.

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
