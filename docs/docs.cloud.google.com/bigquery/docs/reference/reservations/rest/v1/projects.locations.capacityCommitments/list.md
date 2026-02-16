  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Query parameters](#body.QUERY_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
      - [JSON representation](#body.ListCapacityCommitmentsResponse.SCHEMA_REPRESENTATION)
  - [Authorization scopes](#body.aspect)
  - [Try it\!](#try-it)

Lists all the capacity commitments for the admin project.

### HTTP request

`  GET https://bigqueryreservation.googleapis.com/v1/{parent=projects/*/locations/*}/capacityCommitments  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  parent  `

`  string  `

Required. Resource name of the parent reservation. E.g., `  projects/myproject/locations/US  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  parent  ` :

  - `  bigquery.capacityCommitments.list  `

### Query parameters

Parameters

`  pageSize  `

`  integer  `

The maximum number of items to return.

`  pageToken  `

`  string  `

The nextPageToken value returned from a previous List request, if any.

### Request body

The request body must be empty.

### Response body

The response for `  ReservationService.ListCapacityCommitments  ` .

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
  &quot;capacityCommitments&quot;: [
    {
      object (CapacityCommitment)
    }
  ],
  &quot;nextPageToken&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  capacityCommitments[]  `

`  object ( CapacityCommitment  ` )

List of capacity commitments visible to the user.

`  nextPageToken  `

`  string  `

Token to retrieve the next page of results, or empty if there are no more results in the list.

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
