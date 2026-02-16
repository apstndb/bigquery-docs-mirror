  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
  - [Authorization scopes](#body.aspect)
  - [ConnectionCredential](#ConnectionCredential)
      - [JSON representation](#ConnectionCredential.SCHEMA_REPRESENTATION)
  - [Try it\!](#try-it)

Sets the credential for the specified connection.

### HTTP request

`  PATCH https://bigqueryconnection.googleapis.com/v1beta1/{name=projects/*/locations/*/connections/*/credential}  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  name  `

`  string  `

Required. Name of the connection, for example: `  projects/{projectId}/locations/{locationId}/connections/{connectionId}/credential  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  name  ` :

  - `  bigquery.connections.update  `

### Request body

The request body contains an instance of `  ConnectionCredential  ` .

### Response body

If successful, the response body is an empty JSON object.

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .

## ConnectionCredential

Credential to use with a connection.

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

  // Union field credential can be only one of the following:
  &quot;cloudSql&quot;: {
    object (CloudSqlCredential)
  }
  // End of list of possible types for union field credential.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `  credential  ` . Credential specific to the underlying data source. `  credential  ` can be only one of the following:

`  cloudSql  `

`  object ( CloudSqlCredential  ` )

Credential for Cloud SQL database.
