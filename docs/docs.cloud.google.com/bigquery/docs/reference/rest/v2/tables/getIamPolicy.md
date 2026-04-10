  - [HTTP request](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/tables/getIamPolicy#body.HTTP_TEMPLATE)
  - [Path parameters](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/tables/getIamPolicy#body.PATH_PARAMETERS)
  - [Request body](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/tables/getIamPolicy#body.request_body)
      - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/tables/getIamPolicy#body.request_body.SCHEMA_REPRESENTATION)
  - [Response body](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/tables/getIamPolicy#body.response_body)
  - [Authorization scopes](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/tables/getIamPolicy#body.aspect)
  - [Try it\!](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/tables/getIamPolicy#try-it)

Gets the access control policy for a resource. Returns an empty policy if the resource exists and does not have a policy set.

### HTTP request

`  POST https://bigquery.googleapis.com/bigquery/v2/{resource=projects/*/datasets/*/tables/*}:getIamPolicy  `

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
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

OPTIONAL: A `  GetPolicyOptions  ` object for specifying options to `  tables.getIamPolicy  ` .

### Response body

If successful, the response body contains an instance of `  Policy  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `
  - `  https://www.googleapis.com/auth/bigquery.readonly  `
  - `  https://www.googleapis.com/auth/cloud-platform.read-only  `

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
