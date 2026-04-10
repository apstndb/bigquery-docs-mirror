  - [HTTP request](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.runs.transferLogs/list#body.HTTP_TEMPLATE)
  - [Path parameters](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.runs.transferLogs/list#body.PATH_PARAMETERS)
  - [Query parameters](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.runs.transferLogs/list#body.QUERY_PARAMETERS)
  - [Request body](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.runs.transferLogs/list#body.request_body)
  - [Response body](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.runs.transferLogs/list#body.response_body)
  - [Authorization scopes](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.runs.transferLogs/list#body.aspect)
  - [Try it\!](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.runs.transferLogs/list#try-it)

**Full name** : projects.locations.transferConfigs.runs.transferLogs.list

Returns log messages for the transfer run.

### HTTP request

`  GET https://bigquerydatatransfer.googleapis.com/v1/{parent=projects/*/locations/*/transferConfigs/*/runs/*}/transferLogs  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  parent  `

`  string  `

Required. Transfer run name. If you are using the regionless method, the location must be `  US  ` and the name should be in the following form:

  - `  projects/{projectId}/transferConfigs/{configId}/runs/{run_id}  `

If you are using the regionalized method, the name should be in the following form:

  - `  projects/{projectId}/locations/{locationId}/transferConfigs/{configId}/runs/{run_id}  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  parent  ` :

  - `  bigquery.transfers.get  `

### Query parameters

Parameters

`  pageToken  `

`  string  `

Pagination token, which can be used to request a specific page of `  ListTransferLogsRequest  ` list results. For multiple-page results, `  ListTransferLogsResponse  ` outputs a `  next_page  ` token, which can be used as the `  pageToken  ` value to request the next page of list results.

`  pageSize  `

`  integer  `

Page size. The default page size is the maximum value of 1000 results.

`  messageTypes[]  `

`  enum ( MessageSeverity  ` )

Message types to return. If not populated - INFO, WARNING and ERROR messages are returned.

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  ListTransferLogsResponse  ` .

### Authorization scopes

Requires the following OAuth scope:

  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
