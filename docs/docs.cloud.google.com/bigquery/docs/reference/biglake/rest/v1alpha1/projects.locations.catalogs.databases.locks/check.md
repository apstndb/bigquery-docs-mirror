  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
  - [Authorization Scopes](#body.aspect)
  - [IAM Permissions](#body.aspect_1)
  - [Try it\!](#try-it)

Checks the state of a lock specified by the lock ID.

### HTTP request

`  POST https://biglake.googleapis.com/v1alpha1/{name=projects/*/locations/*/catalogs/*/databases/*/locks/*}:check  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  name  `

`  string  `

Required. The name of the lock to check. Format: projects/{project\_id\_or\_number}/locations/{locationId}/catalogs/{catalogId}/databases/{databaseId}/locks/{lock\_id}

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  Lock  ` .

### Authorization Scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](https://cloud.google.com/docs/authentication/) .

### IAM Permissions

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `  name  ` resource:

  - `  biglake.locks.check  `

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .
