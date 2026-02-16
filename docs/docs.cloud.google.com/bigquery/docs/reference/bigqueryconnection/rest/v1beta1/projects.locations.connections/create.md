  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Query parameters](#body.QUERY_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
  - [Authorization scopes](#body.aspect)
  - [Try it\!](#try-it)

Creates a new connection.

### HTTP request

`  POST https://bigqueryconnection.googleapis.com/v1beta1/{parent=projects/*/locations/*}/connections  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  parent  `

`  string  `

Required. Parent resource name. Must be in the format `  projects/{projectId}/locations/{locationId}  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  parent  ` :

  - `  bigquery.connections.create  `

### Query parameters

Parameters

`  connectionId  `

`  string  `

Optional. Connection id that should be assigned to the created connection.

### Request body

The request body contains an instance of `  Connection  ` .

### Response body

If successful, the response body contains a newly created instance of `  Connection  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
