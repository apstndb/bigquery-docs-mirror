  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Query parameters](#body.QUERY_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
  - [Authorization scopes](#body.aspect)
  - [IAM Permissions](#body.aspect_1)
  - [Try it\!](#try-it)

Updates the metadata for an existing data policy. The target data policy can be specified by the resource name.

### HTTP request

`  PATCH https://bigquerydatapolicy.googleapis.com/v1beta1/{dataPolicy.name=projects/*/locations/*/dataPolicies/*}  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  dataPolicy.name  `

`  string  `

Output only. Resource name of this data policy, in the format of `  projects/{projectNumber}/locations/{locationId}/dataPolicies/{dataPolicyId}  ` .

### Query parameters

Parameters

`  updateMask  `

`  string ( FieldMask  ` format)

The update mask applies to the resource. For the `  FieldMask  ` definition, see <https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#fieldmask> If not set, defaults to all of the fields that are allowed to update.

Updates to the `  name  ` and `  dataPolicyId  ` fields are not allowed.

This is a comma-separated list of fully qualified names of fields. Example: `  "user.displayName,photo"  ` .

### Request body

The request body contains an instance of `  DataPolicy  ` .

### Response body

If successful, the response body contains an instance of `  DataPolicy  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .

### IAM Permissions

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `  name  ` resource:

  - `  bigquery.dataPolicies.update  `

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `  taxonomy  ` resource:

  - `  datacatalog.taxonomies.get  `

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .
