  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Query parameters](#body.QUERY_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
      - [JSON representation](#body.ListRowAccessPoliciesResponse.SCHEMA_REPRESENTATION)
  - [Authorization scopes](#body.aspect)
  - [Try it\!](#try-it)

Lists all row access policies on the specified table.

### HTTP request

`  GET https://bigquery.googleapis.com/bigquery/v2/projects/{projectId}/datasets/{datasetId}/tables/{tableId}/rowAccessPolicies  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  projectId  `

`  string  `

Required. Project ID of the row access policies to list.

`  datasetId  `

`  string  `

Required. Dataset ID of row access policies to list.

`  tableId  `

`  string  `

Required. Table ID of the table to list row access policies.

### Query parameters

Parameters

`  pageToken  `

`  string  `

Page token, returned by a previous call, to request the next page of results.

`  pageSize  `

`  integer  `

The maximum number of results to return in a single response page. Leverage the page tokens to iterate through the entire collection.

### Request body

The request body must be empty.

### Response body

Response message for the rowAccessPolicies.list method.

If successful, the response body contains data with the following structure:

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
  &quot;rowAccessPolicies&quot;: [
    {
      object (RowAccessPolicy)
    }
  ],
  &quot;nextPageToken&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  rowAccessPolicies[]  `

`  object ( RowAccessPolicy  ` )

Row access policies on the requested table.

`  nextPageToken  `

`  string  `

A token to request the next page of results.

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `
  - `  https://www.googleapis.com/auth/bigquery.readonly  `
  - `  https://www.googleapis.com/auth/cloud-platform.read-only  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
