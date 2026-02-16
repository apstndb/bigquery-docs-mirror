  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Query parameters](#body.QUERY_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
      - [JSON representation](#body.ListOrgDataExchangesResponse.SCHEMA_REPRESENTATION)
  - [Authorization scopes](#body.aspect)
  - [Try it\!](#try-it)

Lists all data exchanges from projects in a given organization and location.

### HTTP request

`  GET https://analyticshub.googleapis.com/v1/{organization=organizations/*/locations/*}/dataExchanges  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  organization  `

`  string  `

Required. The organization resource path of the projects containing DataExchanges. e.g. `  organizations/myorg/locations/us  ` .

### Query parameters

Parameters

`  pageSize  `

`  integer  `

The maximum number of results to return in a single response page. Leverage the page tokens to iterate through the entire collection.

`  pageToken  `

`  string  `

Page token, returned by a previous call, to request the next page of results.

### Request body

The request body must be empty.

### Response body

Message for response to listing data exchanges in an organization and location.

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
  &quot;dataExchanges&quot;: [
    {
      object (DataExchange)
    }
  ],
  &quot;nextPageToken&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  dataExchanges[]  `

`  object ( DataExchange  ` )

The list of data exchanges.

`  nextPageToken  `

`  string  `

A token to request the next page of results.

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
