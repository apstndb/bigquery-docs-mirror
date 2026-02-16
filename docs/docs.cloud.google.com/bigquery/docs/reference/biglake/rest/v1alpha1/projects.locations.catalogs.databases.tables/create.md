  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Query parameters](#body.QUERY_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
  - [Authorization Scopes](#body.aspect)
  - [IAM Permissions](#body.aspect_1)
  - [Try it\!](#try-it)

Creates a new table.

### HTTP request

`  POST https://biglake.googleapis.com/v1alpha1/{parent=projects/*/locations/*/catalogs/*/databases/*}/tables  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  parent  `

`  string  `

Required. The parent resource where this table will be created. Format: projects/{project\_id\_or\_number}/locations/{locationId}/catalogs/{catalogId}/databases/{databaseId}

### Query parameters

Parameters

`  tableId  `

`  string  `

Required. The ID to use for the table, which will become the final component of the table's resource name.

### Request body

The request body contains an instance of `  Table  ` .

### Response body

If successful, the response body contains a newly created instance of `  Table  ` .

### Authorization Scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](https://cloud.google.com/docs/authentication/) .

### IAM Permissions

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `  parent  ` resource:

  - `  biglake.tables.create  `

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .
