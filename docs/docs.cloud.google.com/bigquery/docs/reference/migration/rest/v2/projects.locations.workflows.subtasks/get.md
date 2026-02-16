  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Query parameters](#body.QUERY_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
  - [Authorization scopes](#body.aspect)
  - [IAM Permissions](#body.aspect_1)
  - [Try it\!](#try-it)

Gets a previously created migration subtask.

### HTTP request

`  GET https://bigquerymigration.googleapis.com/v2/{name=projects/*/locations/*/workflows/*/subtasks/*}  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  name  `

`  string  `

Required. The unique identifier for the migration subtask. Example: `  projects/123/locations/us/workflows/1234/subtasks/543  `

### Query parameters

Parameters

`  readMask  `

`  string ( FieldMask  ` format)

Optional. The list of fields to be retrieved.

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  MigrationSubtask  ` .

### Authorization scopes

Requires the following OAuth scope:

  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .

### IAM Permissions

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `  name  ` resource:

  - `  bigquerymigration.subtasks.get  `

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .
