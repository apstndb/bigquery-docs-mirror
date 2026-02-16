  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Request body](#body.request_body)
      - [JSON representation](#body.request_body.SCHEMA_REPRESENTATION)
  - [Response body](#body.response_body)
  - [Authorization scopes](#body.aspect)
  - [IAM Permissions](#body.aspect_1)
  - [Try it\!](#try-it)

Gets the IAM policy.

### HTTP request

`  POST https://analyticshub.googleapis.com/v1beta1/{resource=projects/*/locations/*/dataExchanges/*/listings/*}:getIamPolicy  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  resource  `

`  string  `

REQUIRED: The resource for which the policy is being requested. See [Resource names](https://cloud.google.com/apis/design/resource_names) for the appropriate value for this field.

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
  &quot;options&quot;: {
    object (GetPolicyOptions)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  options  `

`  object ( GetPolicyOptions  ` )

OPTIONAL: A `  GetPolicyOptions  ` object for specifying options to `  listings.getIamPolicy  ` .

### Response body

If successful, the response body contains an instance of `  Policy  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .

### IAM Permissions

Requires **one of** the following [IAM](https://cloud.google.com/iam/docs) permissions on the `  resource  ` resource, depending on the resource type:

  - `  analyticshub.dataExchanges.getIamPolicy  `
  - `  analyticshub.listings.getIamPolicy  `

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .
