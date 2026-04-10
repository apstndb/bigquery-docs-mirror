  - [HTTP request](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.subscriptions/revoke#body.HTTP_TEMPLATE)
  - [Path parameters](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.subscriptions/revoke#body.PATH_PARAMETERS)
  - [Request body](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.subscriptions/revoke#body.request_body)
      - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.subscriptions/revoke#body.request_body.SCHEMA_REPRESENTATION)
  - [Response body](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.subscriptions/revoke#body.response_body)
  - [Authorization scopes](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.subscriptions/revoke#body.aspect)
  - [Try it\!](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.subscriptions/revoke#try-it)

Revokes a given subscription.

### HTTP request

`  POST https://analyticshub.googleapis.com/v1/{name=projects/*/locations/*/subscriptions/*}:revoke  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  name  `

`  string  `

Required. Resource name of the subscription to revoke. e.g. projects/123/locations/us/subscriptions/456

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
  &quot;revokeCommercial&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  revokeCommercial  `

`  boolean  `

Optional. If the subscription is commercial then this field must be set to true, otherwise a failure is thrown. This acts as a safety guard to avoid revoking commercial subscriptions accidentally.

### Response body

If successful, the response body is empty.

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
