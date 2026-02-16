  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Query parameters](#body.QUERY_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
      - [JSON representation](#body.ListSubscriptionsResponse.SCHEMA_REPRESENTATION)
  - [Authorization scopes](#body.aspect)
  - [IAM Permissions](#body.aspect_1)
  - [Try it\!](#try-it)

Lists all subscriptions in a given project and location.

### HTTP request

`  GET https://analyticshub.googleapis.com/v1/{parent=projects/*/locations/*}/subscriptions  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  parent  `

`  string  `

Required. The parent resource path of the subscription. e.g. projects/myproject/locations/us

### Query parameters

Parameters

`  filter  `

`  string  `

An expression for filtering the results of the request. Eligible fields for filtering are:

  - `  listing  `
  - `  dataExchange  `

Alternatively, a literal wrapped in double quotes may be provided. This will be checked for an exact match against both fields above.

In all cases, the full Data Exchange or Listing resource name must be provided. Some example of using filters:

  - dataExchange="projects/myproject/locations/us/dataExchanges/123"
  - listing="projects/123/locations/us/dataExchanges/456/listings/789"
  - "projects/myproject/locations/us/dataExchanges/123"

`  pageSize  `

`  integer  `

The maximum number of results to return in a single response page.

`  pageToken  `

`  string  `

Page token, returned by a previous call.

### Request body

The request body must be empty.

### Response body

Message for response to the listing of subscriptions.

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
  &quot;subscriptions&quot;: [
    {
      object (Subscription)
    }
  ],
  &quot;nextPageToken&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  subscriptions[]  `

`  object ( Subscription  ` )

The list of subscriptions.

`  nextPageToken  `

`  string  `

Next page token.

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .

### IAM Permissions

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `  parent  ` resource:

  - `  analyticshub.subscriptions.list  `

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .
