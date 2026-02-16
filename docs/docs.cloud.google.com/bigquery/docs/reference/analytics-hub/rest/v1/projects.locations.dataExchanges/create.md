  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Query parameters](#body.QUERY_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
  - [Authorization scopes](#body.aspect)
  - [IAM Permissions](#body.aspect_1)
  - [Try it\!](#try-it)

Creates a new data exchange.

### HTTP request

`  POST https://analyticshub.googleapis.com/v1/{parent=projects/*/locations/*}/dataExchanges  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  parent  `

`  string  `

Required. The parent resource path of the data exchange. e.g. `  projects/myproject/locations/us  ` .

### Query parameters

Parameters

`  dataExchangeId  `

`  string  `

Required. The ID of the data exchange. Must contain only Unicode letters, numbers (0-9), underscores (\_). Max length: 100 bytes.

### Request body

The request body contains an instance of `  DataExchange  ` .

### Response body

If successful, the response body contains a newly created instance of `  DataExchange  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .

### IAM Permissions

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `  parent  ` resource:

  - `  analyticshub.dataExchanges.create  `

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .
