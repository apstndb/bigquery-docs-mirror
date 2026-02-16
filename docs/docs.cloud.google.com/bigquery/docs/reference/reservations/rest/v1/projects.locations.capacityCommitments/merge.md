  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Request body](#body.request_body)
      - [JSON representation](#body.request_body.SCHEMA_REPRESENTATION)
  - [Response body](#body.response_body)
  - [Authorization scopes](#body.aspect)
  - [Try it\!](#try-it)

Merges capacity commitments of the same plan into a single commitment.

The resulting capacity commitment has the greater commitmentEndTime out of the to-be-merged capacity commitments.

Attempting to merge capacity commitments of different plan will fail with the error code `  google.rpc.Code.FAILED_PRECONDITION  ` .

### HTTP request

`  POST https://bigqueryreservation.googleapis.com/v1/{parent=projects/*/locations/*}/capacityCommitments:merge  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  parent  `

`  string  `

Parent resource that identifies admin project and location e.g., `  projects/myproject/locations/us  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  parent  ` :

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
  &quot;capacityCommitmentIds&quot;: [
    string
  ],
  &quot;capacityCommitmentId&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  capacityCommitmentIds[]  `

`  string  `

Ids of capacity commitments to merge. These capacity commitments must exist under admin project and location specified in the parent. ID is the last portion of capacity commitment name e.g., 'abc' for projects/myproject/locations/US/capacityCommitments/abc

`  capacityCommitmentId  `

`  string  `

Optional. The optional resulting capacity commitment ID. Capacity commitment name will be generated automatically if this field is empty. This field must only contain lower case alphanumeric characters or dashes. The first and last character cannot be a dash. Max length is 64 characters.

### Response body

If successful, the response body contains an instance of `  CapacityCommitment  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
