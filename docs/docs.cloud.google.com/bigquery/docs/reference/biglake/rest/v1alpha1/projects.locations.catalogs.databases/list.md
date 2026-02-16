  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Query parameters](#body.QUERY_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
      - [JSON representation](#body.ListDatabasesResponse.SCHEMA_REPRESENTATION)
  - [Authorization Scopes](#body.aspect)
  - [IAM Permissions](#body.aspect_1)
  - [Try it\!](#try-it)

List all databases in a specified catalog.

### HTTP request

`  GET https://biglake.googleapis.com/v1alpha1/{parent=projects/*/locations/*/catalogs/*}/databases  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  parent  `

`  string  `

Required. The parent, which owns this collection of databases. Format: projects/{project\_id\_or\_number}/locations/{locationId}/catalogs/{catalogId}

### Query parameters

Parameters

`  pageSize  `

`  integer  `

The maximum number of databases to return. The service may return fewer than this value. If unspecified, at most 50 databases will be returned. The maximum value is 1000; values above 1000 will be coerced to 1000.

`  pageToken  `

`  string  `

A page token, received from a previous `  databases.list  ` call. Provide this to retrieve the subsequent page.

When paginating, all other parameters provided to `  databases.list  ` must match the call that provided the page token.

### Request body

The request body must be empty.

### Response body

If successful, the response body contains data with the following structure:

Response message for the databases.list method.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;databases&quot;: [
    {
      object (Database)
    }
  ],
  &quot;nextPageToken&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  databases[]  `

`  object ( Database  ` )

The databases from the specified catalog.

`  nextPageToken  `

`  string  `

A token, which can be sent as `  pageToken  ` to retrieve the next page. If this field is omitted, there are no subsequent pages.

### Authorization Scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](https://cloud.google.com/docs/authentication/) .

### IAM Permissions

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `  parent  ` resource:

  - `  biglake.databases.list  `

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .
