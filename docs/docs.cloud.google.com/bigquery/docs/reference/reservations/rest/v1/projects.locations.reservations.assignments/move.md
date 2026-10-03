---
name: documents/docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations.assignments/move
uri: https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations.assignments/move
title: 'Method: projects.locations.reservations.assignments.move'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [HTTP request](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations.assignments/move#body.HTTP_TEMPLATE)
- [Path parameters](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations.assignments/move#body.PATH_PARAMETERS)
- [Request body](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations.assignments/move#body.request_body)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations.assignments/move#body.request_body.SCHEMA_REPRESENTATION)
- [Response body](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations.assignments/move#body.response_body)
- [Authorization scopes](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations.assignments/move#body.aspect)
- [Try it!](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations.assignments/move#try-it)

Moves an assignment under a new reservation.

This differs from removing an existing assignment and recreating a new one by providing a transactional change that ensures an assignee always has an associated reservation.

### HTTP request

`POST https://bigqueryreservation.googleapis.com/v1/{name=projects/*/locations/*/reservations/*/assignments/*}:move`

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
<p>Required. The resource name of the assignment, e.g. <code>projects/myproject/locations/US/reservations/team1-prod/assignments/123</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>bigquery.reservationAssignments.delete</code></li>
</ul></td>
</tr>
</tbody>
</table>

### Request body

The request body contains data with the following structure:

**JSON representation**

```
{
  "destinationId": string,
  "assignmentId": string
}
```

| Fields          |                                                                                                                                                                                                       |
|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `destinationId` | `string` The new reservation ID, e.g.: `projects/myotherproject/locations/US/reservations/team2-prod`                                                                                                 |
| `assignmentId`  | `string` The optional assignment ID. A new assignment name is generated if this field is empty. This field can contain only lowercase alphanumeric characters or dashes. Max length is 64 characters. |

### Response body

If successful, the response body contains an instance of [`Assignment`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations.assignments#Assignment) .

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
