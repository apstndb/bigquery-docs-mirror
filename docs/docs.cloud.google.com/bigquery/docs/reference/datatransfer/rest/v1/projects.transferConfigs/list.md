  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Query parameters](#body.QUERY_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
  - [Authorization scopes](#body.aspect)
  - [Try it\!](#try-it)

**Full name** : projects.transferConfigs.list

Returns information about all transfer configs owned by a project in the specified location.

### HTTP request

`  GET https://bigquerydatatransfer.googleapis.com/v1/{parent=projects/*}/transferConfigs  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  parent  `

`  string  `

Required. The BigQuery project id for which transfer configs should be returned. If you are using the regionless method, the location must be `  US  ` and `  parent  ` should be in the following form:

  - \`projects/{projectId}

If you are using the regionalized method, `  parent  ` should be in the following form:

  - `  projects/{projectId}/locations/{locationId}  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  parent  ` :

  - `  bigquery.transfers.get  `

### Query parameters

Parameters

`  dataSourceIds[]  `

`  string  `

When specified, only configurations of requested data sources are returned.

`  pageToken  `

`  string  `

Pagination token, which can be used to request a specific page of `  ListTransfersRequest  ` list results. For multiple-page results, `  ListTransfersResponse  ` outputs a `  next_page  ` token, which can be used as the `  pageToken  ` value to request the next page of list results.

`  pageSize  `

`  integer  `

Page size. The default page size is the maximum value of 1000 results.

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  ListTransferConfigsResponse  ` .

### Authorization scopes

Requires the following OAuth scope:

  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
