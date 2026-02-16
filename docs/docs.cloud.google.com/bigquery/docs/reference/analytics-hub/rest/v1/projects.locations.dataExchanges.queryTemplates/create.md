  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Query parameters](#body.QUERY_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
  - [Authorization scopes](#body.aspect)
  - [IAM Permissions](#body.aspect_1)
  - [Try it\!](#try-it)

Creates a new QueryTemplate

### HTTP request

`  POST https://analyticshub.googleapis.com/v1/{parent=projects/*/locations/*/dataExchanges/*}/queryTemplates  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  parent  `

`  string  `

Required. The parent resource path of the QueryTemplate. e.g. `  projects/myproject/locations/us/dataExchanges/123/queryTemplates/myQueryTemplate  ` .

### Query parameters

Parameters

`  queryTemplateId  `

`  string  `

Required. The ID of the QueryTemplate to create. Must contain only Unicode letters, numbers (0-9), underscores (\_). Max length: 100 bytes.

### Request body

The request body contains an instance of `  QueryTemplate  ` .

### Response body

If successful, the response body contains a newly created instance of `  QueryTemplate  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .

### IAM Permissions

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `  parent  ` resource:

  - `  analyticshub.queryTemplates.create  `

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .
