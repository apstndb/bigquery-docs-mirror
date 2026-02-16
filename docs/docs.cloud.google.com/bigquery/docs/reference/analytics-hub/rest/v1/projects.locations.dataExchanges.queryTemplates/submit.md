  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
  - [Authorization scopes](#body.aspect)
  - [IAM Permissions](#body.aspect_1)
  - [Try it\!](#try-it)

Submits a query template for approval.

### HTTP request

`  POST https://analyticshub.googleapis.com/v1/{name=projects/*/locations/*/dataExchanges/*/queryTemplates/*}:submit  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  name  `

`  string  `

Required. The resource path of the QueryTemplate. e.g. `  projects/myproject/locations/us/dataExchanges/123/queryTemplates/myqueryTemplate  ` .

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  QueryTemplate  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .

### IAM Permissions

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `  name  ` resource:

  - `  analyticshub.queryTemplates.update  `

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .
