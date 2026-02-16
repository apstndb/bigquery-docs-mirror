  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Query parameters](#body.QUERY_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
  - [Authorization Scopes](#body.aspect)
  - [IAM Permissions](#body.aspect_1)
  - [Try it\!](#try-it)

Updates an existing table specified by the table ID.

### HTTP request

`  PATCH https://biglake.googleapis.com/v1alpha1/{table.name=projects/*/locations/*/catalogs/*/databases/*/tables/*}  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  table.name  `

`  string  `

Output only. The resource name. Format: projects/{project\_id\_or\_number}/locations/{locationId}/catalogs/{catalogId}/databases/{databaseId}/tables/{tableId}

### Query parameters

Parameters

`  updateMask  `

`  string ( FieldMask  ` format)

The list of fields to update.

For the `  FieldMask  ` definition, see <https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#fieldmask> If not set, defaults to all of the fields that are allowed to update.

This is a comma-separated list of fully qualified names of fields. Example: `  "user.displayName,photo"  ` .

### Request body

The request body contains an instance of `  Table  ` .

### Response body

If successful, the response body contains an instance of `  Table  ` .

### Authorization Scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](https://cloud.google.com/docs/authentication/) .

### IAM Permissions

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `  name  ` resource:

  - `  biglake.tables.update  `

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .
