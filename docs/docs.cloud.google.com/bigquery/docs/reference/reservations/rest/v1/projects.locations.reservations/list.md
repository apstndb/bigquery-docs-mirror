---
name: documents/docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations/list
uri: https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations/list
title: 'Method: projects.locations.reservations.list'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [HTTP request](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations/list#body.HTTP_TEMPLATE)
- [Path parameters](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations/list#body.PATH_PARAMETERS)
- [Query parameters](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations/list#body.QUERY_PARAMETERS)
- [Request body](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations/list#body.request_body)
- [Response body](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations/list#body.response_body)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations/list#body.ListReservationsResponse.SCHEMA_REPRESENTATION)
- [Authorization scopes](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations/list#body.aspect)
- [Try it!](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations/list#try-it)

Lists all the reservations for the project in the specified location.

### HTTP request

`GET https://bigqueryreservation.googleapis.com/v1/{parent=projects/*/locations/*}/reservations`

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
<p>Required. The parent resource name containing project and location, e.g.: <code>projects/myproject/locations/US</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>bigquery.reservations.list</code></li>
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

The response for [`ReservationService.ListReservations`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations/list#google.cloud.bigquery.reservation.v1.ReservationService.ListReservations) .

If successful, the response body contains data with the following structure:

**JSON representation**

```
{
  "reservations": [
    {
      object (Reservation)
    }
  ],
  "nextPageToken": string
}
```

| Fields           |                                                                                                                                                                                                  |
|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `reservations[]` | `object ( `[`Reservation`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations#Reservation)` )` List of reservations visible to the user. |
| `nextPageToken`  | `string` Token to retrieve the next page of results, or empty if there are no more results in the list.                                                                                          |

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
