  - [HTTP request](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.transferConfigs.runs/get#body.HTTP_TEMPLATE)
  - [Path parameters](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.transferConfigs.runs/get#body.PATH_PARAMETERS)
  - [Request body](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.transferConfigs.runs/get#body.request_body)
  - [Response body](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.transferConfigs.runs/get#body.response_body)
  - [Authorization scopes](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.transferConfigs.runs/get#body.aspect)
  - [Try it\!](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.transferConfigs.runs/get#try-it)

**Full name** : projects.transferConfigs.runs.get

Returns information about the particular transfer run.

### HTTP request

`GET https://bigquerydatatransfer.googleapis.com/v1/{name=projects/*/transferConfigs/*/runs/*}`

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`name`

`string`

Required. The name of the resource requested. If you are using the regionless method, the location must be `US` and the name should be in the following form:

  - `projects/{projectId}/transferConfigs/{configId}/runs/{run_id}`

If you are using the regionalized method, the name should be in the following form:

  - `projects/{projectId}/locations/{locationId}/transferConfigs/{configId}/runs/{run_id}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `name` :

  - `bigquery.transfers.get`

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  TransferRun  ` .

### Authorization scopes

Requires the following OAuth scope:

  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
