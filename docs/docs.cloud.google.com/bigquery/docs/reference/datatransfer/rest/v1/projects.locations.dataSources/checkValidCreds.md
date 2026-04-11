  - [HTTP request](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.dataSources/checkValidCreds#body.HTTP_TEMPLATE)
  - [Path parameters](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.dataSources/checkValidCreds#body.PATH_PARAMETERS)
  - [Request body](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.dataSources/checkValidCreds#body.request_body)
  - [Response body](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.dataSources/checkValidCreds#body.response_body)
  - [Authorization scopes](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.dataSources/checkValidCreds#body.aspect)
  - [Try it\!](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.dataSources/checkValidCreds#try-it)

**Full name** : projects.locations.dataSources.checkValidCreds

Returns true if valid credentials exist for the given data source and requesting user.

### HTTP request

`POST https://bigquerydatatransfer.googleapis.com/v1/{name=projects/*/locations/*/dataSources/*}:checkValidCreds`

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`name`

`string`

Required. The name of the data source. If you are using the regionless method, the location must be `US` and the name should be in the following form:

  - `projects/{projectId}/dataSources/{dataSourceId}`

If you are using the regionalized method, the name should be in the following form:

  - `projects/{projectId}/locations/{locationId}/dataSources/{dataSourceId}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `name` :

  - `bigquery.transfers.get`

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  CheckValidCredsResponse  ` .

### Authorization scopes

Requires the following OAuth scope:

  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
