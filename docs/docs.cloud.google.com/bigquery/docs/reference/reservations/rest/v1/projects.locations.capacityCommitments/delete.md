---
name: documents/docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments/delete
uri: https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments/delete
title: 'Method: projects.locations.capacityCommitments.delete'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [HTTP request](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments/delete#body.HTTP_TEMPLATE)
- [Path parameters](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments/delete#body.PATH_PARAMETERS)
- [Query parameters](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments/delete#body.QUERY_PARAMETERS)
- [Request body](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments/delete#body.request_body)
- [Response body](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments/delete#body.response_body)
- [Authorization scopes](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments/delete#body.aspect)
- [Try it!](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments/delete#try-it)

Deletes a capacity commitment. Attempting to delete capacity commitment before its commitmentEndTime will fail with the error code `google.rpc.Code.FAILED_PRECONDITION` .

### HTTP request

`DELETE https://bigqueryreservation.googleapis.com/v1/{name=projects/*/locations/*/capacityCommitments/*}`

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
<p>Required. Resource name of the capacity commitment to delete. E.g., <code>projects/myproject/locations/US/capacityCommitments/123</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>bigquery.capacityCommitments.delete</code></li>
</ul></td>
</tr>
</tbody>
</table>

### Query parameters

| Parameters |                                                                                                                                                                                      |
|------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `force`    | `boolean` Can be used to force delete commitments even if assignments exist. Deleting commitments with assignments may cause queries to fail if they no longer have access to slots. |

### Request body

The request body must be empty.

### Response body

If successful, the response body is an empty JSON object.

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
