  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
  - [Authorization scopes](#body.aspect)
  - [IAM Permissions](#body.aspect_1)
  - [Try it\!](#try-it)

Deletes a migration workflow by name.

### HTTP request

`  DELETE https://bigquerymigration.googleapis.com/v2alpha/{name=projects/*/locations/*/workflows/*}  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  name  `

`  string  `

Required. The unique identifier for the migration workflow. Example: `  projects/123/locations/us/workflows/1234  `

### Request body

The request body must be empty.

### Response body

If successful, the response body is an empty JSON object.

### Authorization scopes

Requires the following OAuth scope:

  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .

### IAM Permissions

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `  name  ` resource:

  - `  bigquerymigration.workflows.delete  `

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .
