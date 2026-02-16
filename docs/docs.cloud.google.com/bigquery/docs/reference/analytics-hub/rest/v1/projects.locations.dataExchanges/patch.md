  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Query parameters](#body.QUERY_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
  - [Authorization scopes](#body.aspect)
  - [IAM Permissions](#body.aspect_1)
  - [Try it\!](#try-it)

Updates an existing data exchange.

### HTTP request

`  PATCH https://analyticshub.googleapis.com/v1/{dataExchange.name=projects/*/locations/*/dataExchanges/*}  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  dataExchange.name  `

`  string  `

Output only. The resource name of the data exchange. e.g. `  projects/myproject/locations/us/dataExchanges/123  ` .

### Query parameters

Parameters

`  updateMask  `

`  string ( FieldMask  ` format)

Required. Field mask specifies the fields to update in the data exchange resource. The fields specified in the `  updateMask  ` are relative to the resource and are not a full request.

This is a comma-separated list of fully qualified names of fields. Example: `  "user.displayName,photo"  ` .

### Request body

The request body contains an instance of `  DataExchange  ` .

### Response body

If successful, the response body contains an instance of `  DataExchange  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .

### IAM Permissions

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `  name  ` resource:

  - `  analyticshub.dataExchanges.update  `

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .
