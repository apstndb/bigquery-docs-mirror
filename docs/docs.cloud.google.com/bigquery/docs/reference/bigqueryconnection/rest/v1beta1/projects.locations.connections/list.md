  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Query parameters](#body.QUERY_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
      - [JSON representation](#body.ListConnectionsResponse.SCHEMA_REPRESENTATION)
  - [Authorization scopes](#body.aspect)
  - [Try it\!](#try-it)

Returns a list of connections in the given project.

### HTTP request

`  GET https://bigqueryconnection.googleapis.com/v1beta1/{parent=projects/*/locations/*}/connections  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  parent  `

`  string  `

Required. Parent resource name. Must be in the form: `  projects/{projectId}/locations/{locationId}  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  parent  ` :

  - `  bigquery.connections.list  `

### Query parameters

Parameters

`  maxResults  `

`  integer  `

Required. Maximum number of results per page.

`  pageToken  `

`  string  `

Page token.

### Request body

The request body must be empty.

### Response body

The response for `  ConnectionService.ListConnections  ` .

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
  &quot;nextPageToken&quot;: string,
  &quot;connections&quot;: [
    {
      object (Connection)
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  nextPageToken  `

`  string  `

Next page token.

`  connections[]  `

`  object ( Connection  ` )

List of connections.

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
