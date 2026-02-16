  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Query parameters](#body.QUERY_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
  - [Authorization scopes](#body.aspect)
  - [Try it\!](#try-it)

Lists all subscriptions on a given Data Exchange or Listing.

### HTTP request

`  GET https://analyticshub.googleapis.com/v1/{resource=projects/*/locations/*/dataExchanges/*/listings/*}:listSubscriptions  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  resource  `

`  string  `

Required. Resource name of the requested target. This resource may be either a Listing or a DataExchange. e.g. projects/123/locations/us/dataExchanges/456 OR e.g. projects/123/locations/us/dataExchanges/456/listings/789

### Query parameters

Parameters

`  includeDeletedSubscriptions  `

`  boolean  `

If selected, includes deleted subscriptions in the response (up to 63 days after deletion).

`  pageSize  `

`  integer  `

The maximum number of results to return in a single response page.

`  pageToken  `

`  string  `

Page token, returned by a previous call.

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  ListSharedResourceSubscriptionsResponse  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
