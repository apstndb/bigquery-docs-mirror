  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Request body](#body.request_body)
      - [JSON representation](#body.request_body.SCHEMA_REPRESENTATION)
  - [Response body](#body.response_body)
  - [Authorization scopes](#body.aspect)
  - [IAM Permissions](#body.aspect_1)
  - [Try it\!](#try-it)

Removes grantees from a data policy. The grantees will be removed from the existing grantees. If the request contains a grantee that does not exist, the grantee will be ignored.

### HTTP request

`  POST https://bigquerydatapolicy.googleapis.com/v2/{dataPolicy=projects/*/locations/*/dataPolicies/*}:removeGrantees  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  dataPolicy  `

`  string  `

Required. Resource name of this data policy, in the format of `  projects/{projectNumber}/locations/{locationId}/dataPolicies/{dataPolicyId}  ` .

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
  &quot;grantees&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  grantees[]  `

`  string  `

Required. IAM principal that should be revoked from Fine Grained Access to the underlying data goverened by the data policy. The target data policy is determined by the `  dataPolicy  ` field.

Uses the [IAM V2 principal syntax](https://cloud.google.com/iam/docs/principal-identifiers#v2) . Supported principal types:

  - User
  - Group
  - Service account

### Response body

If successful, the response body contains an instance of `  DataPolicy  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .

### IAM Permissions

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `  dataPolicy  ` resource:

  - `  bigquery.dataPolicies.update  `

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .
