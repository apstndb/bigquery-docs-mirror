  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Query parameters](#body.QUERY_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
  - [Authorization scopes](#body.aspect)
  - [Try it\!](#try-it)

Updates a BI reservation.

Only fields specified in the `  field_mask  ` are updated.

A singleton BI reservation always exists with default size 0. In order to reserve BI capacity it needs to be updated to an amount greater than 0. In order to release BI capacity reservation size must be set to 0.

### HTTP request

`  PATCH https://bigqueryreservation.googleapis.com/v1/{biReservation.name=projects/*/locations/*/biReservation}  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  biReservation.name  `

`  string  `

Identifier. The resource name of the singleton BI reservation. Reservation names have the form `  projects/{projectId}/locations/{locationId}/biReservation  ` .

### Query parameters

Parameters

`  updateMask  `

`  string ( FieldMask  ` format)

A list of fields to be updated in this request.

This is a comma-separated list of fully qualified names of fields. Example: `  "user.displayName,photo"  ` .

### Request body

The request body contains an instance of `  BiReservation  ` .

### Response body

If successful, the response body contains an instance of `  BiReservation  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
