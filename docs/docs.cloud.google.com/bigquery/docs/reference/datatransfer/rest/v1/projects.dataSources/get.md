  - [HTTP request](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.dataSources/get#body.HTTP_TEMPLATE)
  - [Path parameters](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.dataSources/get#body.PATH_PARAMETERS)
  - [Request body](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.dataSources/get#body.request_body)
  - [Response body](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.dataSources/get#body.response_body)
  - [Authorization scopes](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.dataSources/get#body.aspect)
  - [Try it\!](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.dataSources/get#try-it)

**Full name** : projects.dataSources.get

Retrieves a supported data source and returns its settings.

### HTTP request

`  GET https://bigquerydatatransfer.googleapis.com/v1/{name=projects/*/dataSources/*}  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  name  `

`  string  `

Required. The name of the resource requested. If you are using the regionless method, the location must be `  US  ` and the name should be in the following form:

  - `  projects/{projectId}/dataSources/{dataSourceId}  `

If you are using the regionalized method, the name should be in the following form:

  - `  projects/{projectId}/locations/{locationId}/dataSources/{dataSourceId}  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  name  ` :

  - `  bigquery.transfers.get  `

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  DataSource  ` .

### Authorization scopes

Requires the following OAuth scope:

  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
