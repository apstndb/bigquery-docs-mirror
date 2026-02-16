  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Query parameters](#body.QUERY_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
  - [Authorization scopes](#body.aspect)
  - [Try it\!](#try-it)

Updates the specified connection. For security reasons, also resets credential if connection properties are in the update field mask.

### HTTP request

`  PATCH https://bigqueryconnection.googleapis.com/v1/{name=projects/*/locations/*/connections/*}  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  name  `

`  string  `

Required. Name of the connection to update, for example: `  projects/{projectId}/locations/{locationId}/connections/{connectionId}  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  name  ` :

  - `  bigquery.connections.update  `

### Query parameters

Parameters

`  updateMask  `

`  string ( FieldMask  ` format)

Required. Update mask for the connection fields to be updated.

### Request body

The request body contains an instance of `  Connection  ` .

### Response body

If successful, the response body contains an instance of `  Connection  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
