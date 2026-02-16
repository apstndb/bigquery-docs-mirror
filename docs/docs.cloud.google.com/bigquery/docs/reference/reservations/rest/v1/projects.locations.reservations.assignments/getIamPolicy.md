  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Query parameters](#body.QUERY_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
  - [Authorization scopes](#body.aspect)
  - [Try it\!](#try-it)

Gets the access control policy for a resource. May return:

  - A `  NOT_FOUND  ` error if the resource doesn't exist or you don't have the permission to view it.
  - An empty policy if the resource exists but doesn't have a set policy.

Supported resources are: - Reservations - ReservationAssignments

To call this method, you must have the following Google IAM permissions:

  - `  bigqueryreservation.reservations.getIamPolicy  ` to get policies on reservations.

### HTTP request

`  GET https://bigqueryreservation.googleapis.com/v1/{resource=projects/*/locations/*/reservations/*/assignments/*}:getIamPolicy  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  resource  `

`  string  `

REQUIRED: The resource for which the policy is being requested. See [Resource names](https://cloud.google.com/apis/design/resource_names) for the appropriate value for this field.

### Query parameters

Parameters

`  options  `

`  object ( GetPolicyOptions  ` )

OPTIONAL: A `  GetPolicyOptions  ` object for specifying options to `  assignments.getIamPolicy  ` .

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  Policy  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
