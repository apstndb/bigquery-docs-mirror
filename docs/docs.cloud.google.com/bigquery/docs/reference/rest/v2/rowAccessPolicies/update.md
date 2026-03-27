  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
  - [Authorization scopes](#body.aspect)
  - [Try it\!](#try-it)

Updates a row access policy.

### HTTP request

`  PUT https://bigquery.googleapis.com/bigquery/v2/projects/{projectId}/datasets/{datasetId}/tables/{tableId}/rowAccessPolicies/{policyId}  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  projectId  `

`  string  `

Required. Project ID of the table to get the row access policy.

`  datasetId  `

`  string  `

Required. Dataset ID of the table to get the row access policy.

`  tableId  `

`  string  `

Required. Table ID of the table to get the row access policy.

`  policyId  `

`  string  `

Required. Policy ID of the row access policy.

### Request body

The request body contains an instance of `  RowAccessPolicy  ` .

### Response body

If successful, the response body contains an instance of `  RowAccessPolicy  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
