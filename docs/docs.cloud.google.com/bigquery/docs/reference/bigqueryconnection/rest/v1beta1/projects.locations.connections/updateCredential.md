---
name: documents/docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1beta1/projects.locations.connections/updateCredential
uri: https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1beta1/projects.locations.connections/updateCredential
title: 'Method: projects.locations.connections.updateCredential'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [HTTP request](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1beta1/projects.locations.connections/updateCredential#body.HTTP_TEMPLATE)
- [Path parameters](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1beta1/projects.locations.connections/updateCredential#body.PATH_PARAMETERS)
- [Request body](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1beta1/projects.locations.connections/updateCredential#body.request_body)
- [Response body](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1beta1/projects.locations.connections/updateCredential#body.response_body)
- [Authorization scopes](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1beta1/projects.locations.connections/updateCredential#body.aspect)
- [ConnectionCredential](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1beta1/projects.locations.connections/updateCredential#ConnectionCredential)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1beta1/projects.locations.connections/updateCredential#ConnectionCredential.SCHEMA_REPRESENTATION)
- [Try it!](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1beta1/projects.locations.connections/updateCredential#try-it)

Sets the credential for the specified connection.

### HTTP request

`PATCH https://bigqueryconnection.googleapis.com/v1beta1/{name=projects/*/locations/*/connections/*/credential}`

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Parameters</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Name of the connection, for example: <code>projects/{projectId}/locations/{locationId}/connections/{connectionId}/credential</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>bigquery.connections.update</code></li>
</ul></td>
</tr>
</tbody>
</table>

### Request body

The request body contains an instance of [`ConnectionCredential`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1beta1/projects.locations.connections/updateCredential#ConnectionCredential) .

### Response body

If successful, the response body is an empty JSON object.

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

## ConnectionCredential

Credential to use with a connection.

**JSON representation**

```
{

  // The following is a list of mutually exclusive fields. At most one of the
  // fields will be set in a response:
  "cloudSql": {
    object (CloudSqlCredential)
  }
  // End of mutually exclusive fields.
}
```

| Fields                                                                                                                                                        |                                                                                                                                                                                                                   |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Credential specific to the underlying data source. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response: |                                                                                                                                                                                                                   |
| `cloudSql`                                                                                                                                                    | `object ( `[`CloudSqlCredential`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1beta1/projects.locations.connections#CloudSqlCredential)` )` Credential for Cloud SQL database. |
| End of mutually exclusive fields.                                                                                                                             |                                                                                                                                                                                                                   |
