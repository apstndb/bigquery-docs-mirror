---
name: documents/docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1beta1/projects.locations.connections/patch
uri: https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1beta1/projects.locations.connections/patch
title: 'Method: projects.locations.connections.patch'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [HTTP request](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1beta1/projects.locations.connections/patch#body.HTTP_TEMPLATE)
- [Path parameters](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1beta1/projects.locations.connections/patch#body.PATH_PARAMETERS)
- [Query parameters](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1beta1/projects.locations.connections/patch#body.QUERY_PARAMETERS)
- [Request body](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1beta1/projects.locations.connections/patch#body.request_body)
- [Response body](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1beta1/projects.locations.connections/patch#body.response_body)
- [Authorization scopes](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1beta1/projects.locations.connections/patch#body.aspect)
- [Try it!](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1beta1/projects.locations.connections/patch#try-it)

Updates the specified connection. For security reasons, also resets credential if connection properties are in the update field mask.

### HTTP request

`PATCH https://bigqueryconnection.googleapis.com/v1beta1/{name=projects/*/locations/*/connections/*}`

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
<p>Required. Name of the connection to update, for example: <code>projects/{projectId}/locations/{locationId}/connections/{connectionId}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>bigquery.connections.update</code></li>
</ul></td>
</tr>
</tbody>
</table>

### Query parameters

| Parameters   |                                                                                                                                                                        |
|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `updateMask` | `string ( `[`FieldMask`](https://protobuf.dev/reference/protobuf/google.protobuf/#field-mask)` format)` Required. Update mask for the connection fields to be updated. |

### Request body

The request body contains an instance of [`Connection`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1beta1/projects.locations.connections#Connection) .

### Response body

If successful, the response body contains an instance of [`Connection`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1beta1/projects.locations.connections#Connection) .

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
