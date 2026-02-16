  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
  - [Authorization scopes](#body.aspect)
  - [Try it\!](#try-it)

Creates a new routine in the dataset.

### HTTP request

`  POST https://bigquery.googleapis.com/bigquery/v2/projects/{projectId}/datasets/{datasetId}/routines  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  projectId  `

`  string  `

Required. Project ID of the new routine

`  datasetId  `

`  string  `

Required. Dataset ID of the new routine

### Request body

The request body contains an instance of `  Routine  ` .

### Response body

If successful, the response body contains a newly created instance of `  Routine  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
