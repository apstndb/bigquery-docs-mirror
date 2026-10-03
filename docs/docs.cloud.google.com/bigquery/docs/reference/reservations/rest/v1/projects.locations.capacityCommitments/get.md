---
name: documents/docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments/get
uri: https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments/get
title: 'Method: projects.locations.capacityCommitments.get'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [HTTP request](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments/get#body.HTTP_TEMPLATE)
- [Path parameters](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments/get#body.PATH_PARAMETERS)
- [Request body](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments/get#body.request_body)
- [Response body](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments/get#body.response_body)
- [Authorization scopes](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments/get#body.aspect)
- [Try it!](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments/get#try-it)

Returns information about the capacity commitment.

### HTTP request

`GET https://bigqueryreservation.googleapis.com/v1/{name=projects/*/locations/*/capacityCommitments/*}`

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
<p>Required. Resource name of the capacity commitment to retrieve. E.g., <code>projects/myproject/locations/US/capacityCommitments/123</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>bigquery.capacityCommitments.get</code></li>
</ul></td>
</tr>
</tbody>
</table>

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of [`CapacityCommitment`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments#CapacityCommitment) .

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
