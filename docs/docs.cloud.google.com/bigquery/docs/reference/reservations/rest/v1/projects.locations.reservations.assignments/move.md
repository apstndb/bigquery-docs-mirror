  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Request body](#body.request_body)
      - [JSON representation](#body.request_body.SCHEMA_REPRESENTATION)
  - [Response body](#body.response_body)
  - [Authorization scopes](#body.aspect)
  - [Try it\!](#try-it)

Moves an assignment under a new reservation.

This differs from removing an existing assignment and recreating a new one by providing a transactional change that ensures an assignee always has an associated reservation.

### HTTP request

`  POST https://bigqueryreservation.googleapis.com/v1/{name=projects/*/locations/*/reservations/*/assignments/*}:move  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  name  `

`  string  `

Required. The resource name of the assignment, e.g. `  projects/myproject/locations/US/reservations/team1-prod/assignments/123  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  name  ` :

  - `  bigquery.reservationAssignments.delete  `

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
  &quot;destinationId&quot;: string,
  &quot;assignmentId&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  destinationId  `

`  string  `

The new reservation ID, e.g.: `  projects/myotherproject/locations/US/reservations/team2-prod  `

`  assignmentId  `

`  string  `

The optional assignment ID. A new assignment name is generated if this field is empty.

This field can contain only lowercase alphanumeric characters or dashes. Max length is 64 characters.

### Response body

If successful, the response body contains an instance of `  Assignment  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
