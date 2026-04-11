  - [HTTP request](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.dataSources/list#body.HTTP_TEMPLATE)
  - [Path parameters](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.dataSources/list#body.PATH_PARAMETERS)
  - [Query parameters](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.dataSources/list#body.QUERY_PARAMETERS)
  - [Request body](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.dataSources/list#body.request_body)
  - [Response body](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.dataSources/list#body.response_body)
  - [Authorization scopes](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.dataSources/list#body.aspect)
  - [Try it\!](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.dataSources/list#try-it)

**Full name** : projects.locations.dataSources.list

Lists supported data sources and returns their settings.

### HTTP request

`GET https://bigquerydatatransfer.googleapis.com/v1/{parent=projects/*/locations/*}/dataSources`

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`parent`

`string`

Required. The BigQuery project id for which data sources should be returned. Must be in the form: `projects/{projectId}` or `projects/{projectId}/locations/{locationId}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `parent` :

  - `bigquery.transfers.get`

### Query parameters

Parameters

`pageToken`

`string`

Pagination token, which can be used to request a specific page of `ListDataSourcesRequest` list results. For multiple-page results, `ListDataSourcesResponse` outputs a `next_page` token, which can be used as the `pageToken` value to request the next page of list results.

`pageSize`

`integer`

Page size. The default page size is the maximum value of 1000 results.

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  ListDataSourcesResponse  ` .

### Authorization scopes

Requires the following OAuth scope:

  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
