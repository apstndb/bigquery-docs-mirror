  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
  - [Authorization scopes](#body.aspect)
  - [IAM Permissions](#body.aspect_1)
  - [Try it\!](#try-it)

Gets the details of a data exchange.

### HTTP request

`  GET https://analyticshub.googleapis.com/v1beta1/{name=projects/*/locations/*/dataExchanges/*}  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  name  `

`  string  `

Required. The resource name of the data exchange. e.g. `  projects/myproject/locations/us/dataExchanges/123  ` .

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  DataExchange  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .

### IAM Permissions

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `  name  ` resource:

  - `  analyticshub.dataExchanges.get  `

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .
