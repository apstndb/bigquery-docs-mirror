  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
  - [Authorization scopes](#body.aspect)
  - [Try it\!](#try-it)

Returns information about the capacity commitment.

### HTTP request

`  GET https://bigqueryreservation.googleapis.com/v1/{name=projects/*/locations/*/capacityCommitments/*}  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  name  `

`  string  `

Required. Resource name of the capacity commitment to retrieve. E.g., `  projects/myproject/locations/US/capacityCommitments/123  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  name  ` :

  - `  bigquery.capacityCommitments.get  `

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  CapacityCommitment  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
