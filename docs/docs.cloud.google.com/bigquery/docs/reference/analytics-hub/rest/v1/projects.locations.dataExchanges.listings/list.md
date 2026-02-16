  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Query parameters](#body.QUERY_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
      - [JSON representation](#body.ListListingsResponse.SCHEMA_REPRESENTATION)
  - [Authorization scopes](#body.aspect)
  - [IAM Permissions](#body.aspect_1)
  - [Try it\!](#try-it)

Lists all listings in a given project and location.

### HTTP request

`  GET https://analyticshub.googleapis.com/v1/{parent=projects/*/locations/*/dataExchanges/*}/listings  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  parent  `

`  string  `

Required. The parent resource path of the listing. e.g. `  projects/myproject/locations/us/dataExchanges/123  ` .

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

Message for response to the list of Listings.

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
  &quot;listings&quot;: [
    {
      object (Listing)
    }
  ],
  &quot;nextPageToken&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  listings[]  `

`  object ( Listing  ` )

The list of Listing.

`  nextPageToken  `

`  string  `

A token to request the next page of results.

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .

### IAM Permissions

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `  parent  ` resource:

  - `  analyticshub.listings.list  `

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .
