---
name: documents/docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations/searchAssignments
uri: https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations/searchAssignments
title: 'Method: projects.locations.searchAssignments'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [HTTP request](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations/searchAssignments#body.HTTP_TEMPLATE)
- [Path parameters](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations/searchAssignments#body.PATH_PARAMETERS)
- [Query parameters](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations/searchAssignments#body.QUERY_PARAMETERS)
- [Request body](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations/searchAssignments#body.request_body)
- [Response body](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations/searchAssignments#body.response_body)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations/searchAssignments#body.SearchAssignmentsResponse.SCHEMA_REPRESENTATION)
- [Authorization scopes](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations/searchAssignments#body.aspect)
- [Try it!](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations/searchAssignments#try-it)

> This item is deprecated!

Deprecated: Looks up assignments for a specified resource for a particular region. If the request is about a project:

1.  Assignments created on the project will be returned if they exist.
2.  Otherwise assignments created on the closest ancestor will be returned.
3.  Assignments for different JobTypes will all be returned.

The same logic applies if the request is about a folder.

If the request is about an organization, then assignments created on the organization will be returned (organization doesn't have ancestors).

Comparing to assignments.list, there are some behavior differences:

1.  permission on the assignee will be verified in this API.
2.  Hierarchy lookup (project-\>folder-\>organization) happens in this API.
3.  Parent here is `projects/*/locations/*` , instead of `projects/*/locations/*reservations/*` .

**Note** "-" cannot be used for projects nor locations.

### HTTP request

`GET https://bigqueryreservation.googleapis.com/v1/{parent=projects/*/locations/*}:searchAssignments`

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
<p>Required. The resource name of the admin project(containing project and location), e.g.: <code>projects/myproject/locations/US</code> .</p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>bigquery.reservationAssignments.search</code></li>
</ul></td>
</tr>
</tbody>
</table>

### Query parameters

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
<td><code>query</code></td>
<td><p><code>string</code></p>
<p>Please specify resource name as assignee in the query.</p>
<p>Examples:</p>
<ul>
<li><code>assignee=projects/myproject</code></li>
<li><code>assignee=folders/123</code></li>
<li><code>assignee=organizations/456</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>pageSize</code></td>
<td><p><code>integer</code></p>
<p>The maximum number of items to return per page.</p></td>
</tr>
<tr class="odd">
<td><code>pageToken</code></td>
<td><p><code>string</code></p>
<p>The nextPageToken value returned from a previous List request, if any.</p></td>
</tr>
</tbody>
</table>

### Request body

The request body must be empty.

### Response body

The response for [`ReservationService.SearchAssignments`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations/searchAssignments#google.cloud.bigquery.reservation.v1.ReservationService.SearchAssignments) .

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
