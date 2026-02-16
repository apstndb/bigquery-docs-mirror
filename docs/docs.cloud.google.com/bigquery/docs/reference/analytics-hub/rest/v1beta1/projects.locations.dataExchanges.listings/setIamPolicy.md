  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Request body](#body.request_body)
      - [JSON representation](#body.request_body.SCHEMA_REPRESENTATION)
  - [Response body](#body.response_body)
  - [Authorization scopes](#body.aspect)
  - [IAM Permissions](#body.aspect_1)
  - [Try it\!](#try-it)

Sets the IAM policy.

### HTTP request

`  POST https://analyticshub.googleapis.com/v1beta1/{resource=projects/*/locations/*/dataExchanges/*/listings/*}:setIamPolicy  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  resource  `

`  string  `

REQUIRED: The resource for which the policy is being specified. See [Resource names](https://cloud.google.com/apis/design/resource_names) for the appropriate value for this field.

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
  &quot;policy&quot;: {
    object (Policy)
  },
  &quot;updateMask&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  policy  `

`  object ( Policy  ` )

REQUIRED: The complete policy to be applied to the `  resource  ` . The size of the policy is limited to a few 10s of KB. An empty policy is a valid policy but certain Google Cloud services (such as Projects) might reject them.

`  updateMask  `

`  string ( FieldMask  ` format)

OPTIONAL: A FieldMask specifying which fields of the policy to modify. Only the fields in the mask will be modified. If no mask is provided, the following default mask is used:

`  paths: "bindings, etag"  `

This is a comma-separated list of fully qualified names of fields. Example: `  "user.displayName,photo"  ` .

### Response body

If successful, the response body contains an instance of `  Policy  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .

### IAM Permissions

Requires **one of** the following [IAM](https://cloud.google.com/iam/docs) permissions on the `  resource  ` resource, depending on the resource type:

  - `  analyticshub.dataExchanges.setIamPolicy  `
  - `  analyticshub.listings.setIamPolicy  `

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .
