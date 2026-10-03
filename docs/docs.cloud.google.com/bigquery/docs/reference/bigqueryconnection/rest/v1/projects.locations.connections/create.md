---
name: documents/docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1/projects.locations.connections/create
uri: https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1/projects.locations.connections/create
title: 'Method: projects.locations.connections.create'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [HTTP request](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1/projects.locations.connections/create#body.HTTP_TEMPLATE)
- [Path parameters](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1/projects.locations.connections/create#body.PATH_PARAMETERS)
- [Query parameters](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1/projects.locations.connections/create#body.QUERY_PARAMETERS)
- [Request body](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1/projects.locations.connections/create#body.request_body)
- [Response body](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1/projects.locations.connections/create#body.response_body)
- [Authorization scopes](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1/projects.locations.connections/create#body.aspect)
- [Try it!](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1/projects.locations.connections/create#try-it)

Creates a new connection.

### HTTP request

`POST https://bigqueryconnection.googleapis.com/v1/{parent=projects/*/locations/*}/connections`

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
<td><code>parent</code></td>
<td><p><code>string</code></p>
<p>Required. Parent resource name. Must be in the format <code>projects/{projectId}/locations/{locationId}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>bigquery.connections.create</code></li>
</ul></td>
</tr>
</tbody>
</table>

### Query parameters

| Parameters     |                                                                                     |
|----------------|-------------------------------------------------------------------------------------|
| `connectionId` | `string` Optional. Connection id that should be assigned to the created connection. |

### Request body

The request body contains an instance of [`Connection`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1/projects.locations.connections#Connection) .

### Response body

If successful, the response body contains a newly created instance of [`Connection`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1/projects.locations.connections#Connection) .

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
