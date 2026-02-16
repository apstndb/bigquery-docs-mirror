  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Query parameters](#body.QUERY_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
  - [Authorization scopes](#body.aspect)
  - [Try it\!](#try-it)

Creates a new listing.

### HTTP request

`  POST https://analyticshub.googleapis.com/v1/{parent=projects/*/locations/*/dataExchanges/*}/listings  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  parent  `

`  string  `

Required. The parent resource path of the listing. e.g. `  projects/myproject/locations/us/dataExchanges/123  ` .

### Query parameters

Parameters

`  listingId  `

`  string  `

Required. The ID of the listing to create. Must contain only Unicode letters, numbers (0-9), underscores (\_). Max length: 100 bytes.

### Request body

The request body contains an instance of `  Listing  ` .

### Response body

If successful, the response body contains a newly created instance of `  Listing  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
