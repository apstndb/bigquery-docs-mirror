  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
      - [JSON representation](#body.GetServiceAccountResponse.SCHEMA_REPRESENTATION)
  - [Authorization scopes](#body.aspect)
  - [Try it\!](#try-it)

RPC to get the service account for a project used for interactions with Google Cloud KMS

### HTTP request

`  GET https://bigquery.googleapis.com/bigquery/v2/projects/{projectId}/serviceAccount  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  projectId  `

`  string  `

Required. ID of the project.

### Request body

The request body must be empty.

### Response body

Response object of projects.getServiceAccount

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
  &quot;kind&quot;: string,
  &quot;email&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  kind  `

`  string  `

The resource type of the response.

`  email  `

`  string  `

The service account email address.

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `
  - `  https://www.googleapis.com/auth/bigquery.readonly  `
  - `  https://www.googleapis.com/auth/cloud-platform.read-only  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
