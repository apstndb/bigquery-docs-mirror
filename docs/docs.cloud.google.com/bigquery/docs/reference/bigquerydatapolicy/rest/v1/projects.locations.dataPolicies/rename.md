  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Request body](#body.request_body)
      - [JSON representation](#body.request_body.SCHEMA_REPRESENTATION)
  - [Response body](#body.response_body)
  - [Authorization scopes](#body.aspect)
  - [IAM Permissions](#body.aspect_1)
  - [Try it\!](#try-it)

Renames the id (display name) of the specified data policy.

### HTTP request

`  POST https://bigquerydatapolicy.googleapis.com/v1/{name=projects/*/locations/*/dataPolicies/*}:rename  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  name  `

`  string  `

Required. Resource name of the data policy to rename. The format is `  projects/{projectNumber}/locations/{locationId}/dataPolicies/{dataPolicyId}  `

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
  &quot;newDataPolicyId&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  newDataPolicyId  `

`  string  `

Required. The new data policy id.

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

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .
