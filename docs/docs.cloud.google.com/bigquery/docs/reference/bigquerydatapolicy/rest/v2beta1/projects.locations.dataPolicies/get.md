  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
  - [Authorization scopes](#body.aspect)
  - [IAM Permissions](#body.aspect_1)
  - [Try it\!](#try-it)

Gets the data policy specified by its resource name.

### HTTP request

`  GET https://bigquerydatapolicy.googleapis.com/v2beta1/{name=projects/*/locations/*/dataPolicies/*}  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  name  `

`  string  `

Required. Resource name of the requested data policy. Format is `  projects/{projectNumber}/locations/{locationId}/dataPolicies/{id}  ` .

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  DataPolicy  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .

### IAM Permissions

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `  name  ` resource:

  - `  bigquery.dataPolicies.get  `

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .
