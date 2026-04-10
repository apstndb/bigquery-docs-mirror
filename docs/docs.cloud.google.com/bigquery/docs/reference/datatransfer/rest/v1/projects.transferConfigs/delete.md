  - [HTTP request](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.transferConfigs/delete#body.HTTP_TEMPLATE)
  - [Path parameters](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.transferConfigs/delete#body.PATH_PARAMETERS)
  - [Request body](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.transferConfigs/delete#body.request_body)
  - [Response body](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.transferConfigs/delete#body.response_body)
  - [Authorization scopes](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.transferConfigs/delete#body.aspect)
  - [Try it\!](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.transferConfigs/delete#try-it)

**Full name** : projects.transferConfigs.delete

Deletes a data transfer configuration, including any associated transfer runs and logs.

### HTTP request

`  DELETE https://bigquerydatatransfer.googleapis.com/v1/{name=projects/*/transferConfigs/*}  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  name  `

`  string  `

Required. The name of the resource to delete. If you are using the regionless method, the location must be `  US  ` and the name should be in the following form:

  - `  projects/{projectId}/transferConfigs/{configId}  `

If you are using the regionalized method, the name should be in the following form:

  - `  projects/{projectId}/locations/{locationId}/transferConfigs/{configId}  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  name  ` :

  - `  bigquery.transfers.update  `

### Request body

The request body must be empty.

### Response body

If successful, the response body is an empty JSON object.

### Authorization scopes

Requires the following OAuth scope:

  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
