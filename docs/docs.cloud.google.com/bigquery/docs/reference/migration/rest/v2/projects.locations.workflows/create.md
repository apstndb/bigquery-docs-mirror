  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
  - [Authorization scopes](#body.aspect)
  - [IAM Permissions](#body.aspect_1)
  - [Try it\!](#try-it)

Creates a migration workflow.

### HTTP request

`  POST https://bigquerymigration.googleapis.com/v2/{parent=projects/*/locations/*}/workflows  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  parent  `

`  string  `

Required. The name of the project to which this migration workflow belongs. Example: `  projects/foo/locations/bar  `

### Request body

The request body contains an instance of `  MigrationWorkflow  ` .

### Response body

If successful, the response body contains a newly created instance of `  MigrationWorkflow  ` .

### Authorization scopes

Requires the following OAuth scope:

  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .

### IAM Permissions

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `  parent  ` resource:

  - `  bigquerymigration.workflows.create  `

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .
