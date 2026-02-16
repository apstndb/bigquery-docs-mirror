  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Query parameters](#body.QUERY_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
      - [JSON representation](#body.ListAssignmentsResponse.SCHEMA_REPRESENTATION)
  - [Authorization scopes](#body.aspect)
  - [Try it\!](#try-it)

Lists assignments.

Only explicitly created assignments will be returned.

Example:

  - Organization `  organizationA  ` contains two projects, `  project1  ` and `  project2  ` .
  - Reservation `  res1  ` exists and was created previously.
  - assignments.create was used previously to define the following associations between entities and reservations: `  <organizationA, res1>  ` and `  <project1, res1>  `

In this example, assignments.list will just return the above two assignments for reservation `  res1  ` , and no expansion/merge will happen.

The wildcard "-" can be used for reservations in the request. In that case all assignments belongs to the specified project and location will be listed.

**Note** "-" cannot be used for projects nor locations.

### HTTP request

`  GET https://bigqueryreservation.googleapis.com/v1/{parent=projects/*/locations/*/reservations/*}/assignments  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  parent  `

`  string  `

Required. The parent resource name e.g.:

`  projects/myproject/locations/US/reservations/team1-prod  `

Or:

`  projects/myproject/locations/US/reservations/-  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  parent  ` :

  - `  bigquery.reservationAssignments.list  `

### Query parameters

Parameters

`  pageSize  `

`  integer  `

The maximum number of items to return per page.

`  pageToken  `

`  string  `

The nextPageToken value returned from a previous List request, if any.

### Request body

The request body must be empty.

### Response body

The response for `  ReservationService.ListAssignments  ` .

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
  &quot;assignments&quot;: [
    {
      object (Assignment)
    }
  ],
  &quot;nextPageToken&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  assignments[]  `

`  object ( Assignment  ` )

List of assignments visible to the user.

`  nextPageToken  `

`  string  `

Token to retrieve the next page of results, or empty if there are no more results in the list.

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
