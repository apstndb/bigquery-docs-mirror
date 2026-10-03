---
name: documents/docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservationGroups/create
uri: https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservationGroups/create
title: 'Method: projects.locations.reservationGroups.create'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [HTTP request](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservationGroups/create#body.HTTP_TEMPLATE)
- [Path parameters](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservationGroups/create#body.PATH_PARAMETERS)
- [Query parameters](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservationGroups/create#body.QUERY_PARAMETERS)
- [Request body](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservationGroups/create#body.request_body)
- [Response body](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservationGroups/create#body.response_body)
- [Authorization scopes](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservationGroups/create#body.aspect)
- [Try it!](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservationGroups/create#try-it)

Creates a new reservation group.

### HTTP request

`POST https://bigqueryreservation.googleapis.com/v1/{parent=projects/*/locations/*}/reservationGroups`

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
<p>Required. Project, location. E.g., <code>projects/myproject/locations/US</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>bigquery.reservationGroups.create</code></li>
</ul></td>
</tr>
</tbody>
</table>

### Query parameters

| Parameters           |                                                                                                                                                                                                                |
|----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `reservationGroupId` | `string` Required. The reservation group ID. It must only contain lower case alphanumeric characters or dashes. It must start with a letter and must not end with a dash. Its maximum length is 64 characters. |

### Request body

The request body contains an instance of [`ReservationGroup`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservationGroups#ReservationGroup) .

### Response body

If successful, the response body contains a newly created instance of [`ReservationGroup`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservationGroups#ReservationGroup) .

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
