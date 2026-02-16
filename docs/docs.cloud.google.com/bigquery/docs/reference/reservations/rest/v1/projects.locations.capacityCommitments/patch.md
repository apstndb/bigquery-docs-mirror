  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Query parameters](#body.QUERY_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
  - [Authorization scopes](#body.aspect)
  - [Try it\!](#try-it)

Updates an existing capacity commitment.

Only `  plan  ` and `  renewalPlan  ` fields can be updated.

Plan can only be changed to a plan of a longer commitment period. Attempting to change to a plan with shorter commitment period will fail with the error code `  google.rpc.Code.FAILED_PRECONDITION  ` .

### HTTP request

`  PATCH https://bigqueryreservation.googleapis.com/v1/{capacityCommitment.name=projects/*/locations/*/capacityCommitments/*}  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  capacityCommitment.name  `

`  string  `

Output only. The resource name of the capacity commitment, e.g., `  projects/myproject/locations/US/capacityCommitments/123  ` The commitment\_id must only contain lower case alphanumeric characters or dashes. It must start with a letter and must not end with a dash. Its maximum length is 64 characters.

### Query parameters

Parameters

`  updateMask  `

`  string ( FieldMask  ` format)

Standard field mask for the set of fields to be updated.

This is a comma-separated list of fully qualified names of fields. Example: `  "user.displayName,photo"  ` .

### Request body

The request body contains an instance of `  CapacityCommitment  ` .

### Response body

If successful, the response body contains an instance of `  CapacityCommitment  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
