---
name: documents/docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations.assignments/list
uri: https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations.assignments/list
title: 'Method: projects.locations.reservations.assignments.list'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [HTTP request](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations.assignments/list#body.HTTP_TEMPLATE)
- [Path parameters](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations.assignments/list#body.PATH_PARAMETERS)
- [Query parameters](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations.assignments/list#body.QUERY_PARAMETERS)
- [Request body](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations.assignments/list#body.request_body)
- [Response body](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations.assignments/list#body.response_body)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations.assignments/list#body.ListAssignmentsResponse.SCHEMA_REPRESENTATION)
- [Authorization scopes](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations.assignments/list#body.aspect)
- [Try it!](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations.assignments/list#try-it)

Lists assignments.

Only explicitly created assignments will be returned.

Example:

- Organization `organizationA` contains two projects, `project1` and `project2` .
- Reservation `res1` exists and was created previously.
- assignments.create was used previously to define the following associations between entities and reservations: `<organizationA, res1>` and `<project1, res1>`

In this example, assignments.list will just return the above two assignments for reservation `res1` , and no expansion/merge will happen.

The wildcard "-" can be used for reservations in the request. In that case all assignments belongs to the specified project and location will be listed.

**Note** "-" cannot be used for projects nor locations.

### HTTP request

`GET https://bigqueryreservation.googleapis.com/v1/{parent=projects/*/locations/*/reservations/*}/assignments`

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
<p>Required. The parent resource name e.g.:</p>
<p><code>projects/myproject/locations/US/reservations/team1-prod</code></p>
<p>Or:</p>
<p><code>projects/myproject/locations/US/reservations/-</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>bigquery.reservationAssignments.list</code></li>
</ul></td>
</tr>
</tbody>
</table>

### Query parameters

| Parameters  |                                                                                 |
|-------------|---------------------------------------------------------------------------------|
| `pageSize`  | `integer` The maximum number of items to return per page.                       |
| `pageToken` | `string` The nextPageToken value returned from a previous List request, if any. |

### Request body

The request body must be empty.

### Response body

The response for [`ReservationService.ListAssignments`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations.assignments/list#google.cloud.bigquery.reservation.v1.ReservationService.ListAssignments) .

If successful, the response body contains data with the following structure:

**JSON representation**

```
{
  "assignments": [
    {
      object (Assignment)
    }
  ],
  "nextPageToken": string
}
```

| Fields          |                                                                                                                                                                                                           |
|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `assignments[]` | `object ( `[`Assignment`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations.assignments#Assignment)` )` List of assignments visible to the user. |
| `nextPageToken` | `string` Token to retrieve the next page of results, or empty if there are no more results in the list.                                                                                                   |

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
