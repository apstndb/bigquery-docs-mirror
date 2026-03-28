  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Query parameters](#body.QUERY_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
  - [Authorization scopes](#body.aspect)
  - [Try it\!](#try-it)

**Full name** : projects.transferConfigs.transferResources.list

Returns information about transfer resources.

### HTTP request

`  GET https://bigquerydatatransfer.googleapis.com/v1/{parent=projects/*/transferConfigs/*}/transferResources  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  parent  `

`  string  `

Required. Name of transfer configuration for which transfer resources should be retrieved. The name should be in one of the following forms:

  - `  projects/{project}/transferConfigs/{transferConfig}  `
  - `  projects/{project}/locations/{locationId}/transferConfigs/{transferConfig}  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  parent  ` :

  - `  bigquery.transfers.get  `

### Query parameters

Parameters

`  pageSize  `

`  integer  `

Optional. The maximum number of transfer resources to return. The maximum value is 1000; values above 1000 will be coerced to 1000. The default page size is the maximum value of 1000 results.

`  pageToken  `

`  string  `

Optional. A page token, received from a previous `  transferResources.list  ` call. Provide this to retrieve the subsequent page. When paginating, all other parameters provided to `  transferResources.list  ` must match the call that provided the page token.

`  filter  `

`  string  `

Optional. Filter for the transfer resources. Currently supported filters include:

  - Resource name: `  name  ` - Wildcard supported
  - Resource type: `  type  `
  - Resource destination: `  destination  `
  - Latest resource state: `  latest_status_detail.state  `
  - Last update time: `  update_time  ` - RFC-3339 format
  - Parent table name: `  hierarchy_detail.partition_detail.table  `

Multiple filters can be applied using the `  AND/OR  ` operator.

Examples:

  - `  name="*123" AND (type="TABLE" OR latest_status_detail.state="SUCCEEDED")  `
  - `  update_time >= "2012-04-21T11:30:00-04:00"  `
  - `  hierarchy_detail.partition_detail.table = "table1"  `

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  ListTransferResourcesResponse  ` .

### Authorization scopes

Requires the following OAuth scope:

  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
