---
name: documents/docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1beta1/projects.locations.connections/delete
uri: https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1beta1/projects.locations.connections/delete
title: 'Method: projects.locations.connections.delete'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [HTTP request](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1beta1/projects.locations.connections/delete#body.HTTP_TEMPLATE)
- [Path parameters](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1beta1/projects.locations.connections/delete#body.PATH_PARAMETERS)
- [Request body](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1beta1/projects.locations.connections/delete#body.request_body)
- [Response body](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1beta1/projects.locations.connections/delete#body.response_body)
- [Authorization scopes](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1beta1/projects.locations.connections/delete#body.aspect)
- [Try it!](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1beta1/projects.locations.connections/delete#try-it)

Deletes connection and associated credential.

### HTTP request

`DELETE https://bigqueryconnection.googleapis.com/v1beta1/{name=projects/*/locations/*/connections/*}`

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
<p>Required. Name of the deleted connection, for example: <code>projects/{projectId}/locations/{locationId}/connections/{connectionId}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>bigquery.connections.delete</code></li>
</ul></td>
</tr>
</tbody>
</table>

### Request body

The request body must be empty.

### Response body

If successful, the response body is an empty JSON object.

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
