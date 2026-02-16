  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Query parameters](#body.QUERY_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
  - [Authorization scopes](#body.aspect)
  - [Try it\!](#try-it)

Updates an existing assignment.

Only the `  priority  ` field can be updated.

### HTTP request

`  PATCH https://bigqueryreservation.googleapis.com/v1/{assignment.name=projects/*/locations/*/reservations/*/assignments/*}  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  assignment.name  `

`  string  `

Output only. Name of the resource. E.g.: `  projects/myproject/locations/US/reservations/team1-prod/assignments/123  ` . The assignmentId must only contain lower case alphanumeric characters or dashes and the max length is 64 characters.

### Query parameters

Parameters

`  updateMask  `

`  string ( FieldMask  ` format)

Standard field mask for the set of fields to be updated.

This is a comma-separated list of fully qualified names of fields. Example: `  "user.displayName,photo"  ` .

### Request body

The request body contains an instance of `  Assignment  ` .

### Response body

If successful, the response body contains an instance of `  Assignment  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
