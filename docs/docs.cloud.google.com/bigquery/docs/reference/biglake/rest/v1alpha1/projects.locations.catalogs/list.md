  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Query parameters](#body.QUERY_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
      - [JSON representation](#body.ListCatalogsResponse.SCHEMA_REPRESENTATION)
  - [Authorization Scopes](#body.aspect)
  - [IAM Permissions](#body.aspect_1)
  - [Try it\!](#try-it)

List all catalogs in a specified project.

### HTTP request

`  GET https://biglake.googleapis.com/v1alpha1/{parent=projects/*/locations/*}/catalogs  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  parent  `

`  string  `

Required. The parent, which owns this collection of catalogs. Format: projects/{project\_id\_or\_number}/locations/{locationId}

### Query parameters

Parameters

`  pageSize  `

`  integer  `

The maximum number of catalogs to return. The service may return fewer than this value. If unspecified, at most 50 catalogs will be returned. The maximum value is 1000; values above 1000 will be coerced to 1000.

`  pageToken  `

`  string  `

A page token, received from a previous `  catalogs.list  ` call. Provide this to retrieve the subsequent page.

When paginating, all other parameters provided to `  catalogs.list  ` must match the call that provided the page token.

### Request body

The request body must be empty.

### Response body

If successful, the response body contains data with the following structure:

Response message for the catalogs.list method.

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
  &quot;catalogs&quot;: [
    {
      object (Catalog)
    }
  ],
  &quot;nextPageToken&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  catalogs[]  `

`  object ( Catalog  ` )

The catalogs from the specified project.

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

  - `  biglake.catalogs.list  `

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .
