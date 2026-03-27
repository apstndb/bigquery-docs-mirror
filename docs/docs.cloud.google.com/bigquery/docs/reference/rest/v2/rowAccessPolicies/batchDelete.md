  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Request body](#body.request_body)
      - [JSON representation](#body.request_body.SCHEMA_REPRESENTATION)
  - [Response body](#body.response_body)
  - [Authorization scopes](#body.aspect)
  - [Try it\!](#try-it)

Deletes provided row access policies.

### HTTP request

`  POST https://bigquery.googleapis.com/bigquery/v2/projects/{projectId}/datasets/{datasetId}/tables/{tableId}/rowAccessPolicies:batchDelete  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  projectId  `

`  string  `

Required. Project ID of the table to delete the row access policies.

`  datasetId  `

`  string  `

Required. Dataset ID of the table to delete the row access policies.

`  tableId  `

`  string  `

Required. Table ID of the table to delete the row access policies.

### Request body

The request body contains data with the following structure:

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
  &quot;policyIds&quot;: [
    string
  ],
  &quot;force&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  policyIds[]  `

`  string  `

Required. Policy IDs of the row access policies.

`  force  `

`  boolean  `

If set to true, it deletes the row access policy even if it's the last row access policy on the table and the deletion will widen the access rather narrowing it.

### Response body

If successful, the response body is an empty JSON object.

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
