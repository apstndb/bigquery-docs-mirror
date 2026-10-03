---
name: documents/docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1beta1/projects.locations.connections/list
uri: https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1beta1/projects.locations.connections/list
title: 'Method: projects.locations.connections.list'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [HTTP request](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1beta1/projects.locations.connections/list#body.HTTP_TEMPLATE)
- [Path parameters](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1beta1/projects.locations.connections/list#body.PATH_PARAMETERS)
- [Query parameters](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1beta1/projects.locations.connections/list#body.QUERY_PARAMETERS)
- [Request body](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1beta1/projects.locations.connections/list#body.request_body)
- [Response body](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1beta1/projects.locations.connections/list#body.response_body)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1beta1/projects.locations.connections/list#body.ListConnectionsResponse.SCHEMA_REPRESENTATION)
- [Authorization scopes](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1beta1/projects.locations.connections/list#body.aspect)
- [Try it!](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1beta1/projects.locations.connections/list#try-it)

Returns a list of connections in the given project.

### HTTP request

`GET https://bigqueryconnection.googleapis.com/v1beta1/{parent=projects/*/locations/*}/connections`

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
<p>Required. Parent resource name. Must be in the form: <code>projects/{projectId}/locations/{locationId}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>bigquery.connections.list</code></li>
</ul></td>
</tr>
</tbody>
</table>

### Query parameters

| Parameters   |                                                         |
|--------------|---------------------------------------------------------|
| `maxResults` | `integer` Required. Maximum number of results per page. |
| `pageToken`  | `string` Page token.                                    |

### Request body

The request body must be empty.

### Response body

The response for [`ConnectionService.ListConnections`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1beta1/projects.locations.connections/list#google.cloud.bigquery.connection.v1beta1.ConnectionService.ListConnections) .

If successful, the response body contains data with the following structure:

**JSON representation**

```
{
  "nextPageToken": string,
  "connections": [
    {
      object (Connection)
    }
  ]
}
```

| Fields          |                                                                                                                                                                                     |
|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `nextPageToken` | `string` Next page token.                                                                                                                                                           |
| `connections[]` | `object ( `[`Connection`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1beta1/projects.locations.connections#Connection)` )` List of connections. |

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
