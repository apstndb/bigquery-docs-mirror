  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
  - [Authorization scopes](#body.aspect)
  - [IAM Permissions](#body.aspect_1)
  - [Try it\!](#try-it)

Creates a new data policy under a project with the given `  dataPolicyId  ` (used as the display name), policy tag, and data policy type.

### HTTP request

`  POST https://bigquerydatapolicy.googleapis.com/v1/{parent=projects/*/locations/*}/dataPolicies  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  parent  `

`  string  `

Required. Resource name of the project that the data policy will belong to. The format is `  projects/{projectNumber}/locations/{locationId}  ` .

### Request body

The request body contains an instance of `  DataPolicy  ` .

### Response body

If successful, the response body contains a newly created instance of `  DataPolicy  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .

### IAM Permissions

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `  routine  ` resource:

  - `  bigquery.routines.get  `

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `  taxonomy  ` resource:

  - `  datacatalog.taxonomies.get  `

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `  parent  ` resource:

  - `  bigquery.dataPolicies.create  `

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .
