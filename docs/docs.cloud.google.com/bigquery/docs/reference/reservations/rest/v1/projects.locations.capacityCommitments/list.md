---
name: documents/docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments/list
uri: https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments/list
title: 'Method: projects.locations.capacityCommitments.list'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [HTTP request](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments/list#body.HTTP_TEMPLATE)
- [Path parameters](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments/list#body.PATH_PARAMETERS)
- [Query parameters](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments/list#body.QUERY_PARAMETERS)
- [Request body](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments/list#body.request_body)
- [Response body](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments/list#body.response_body)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments/list#body.ListCapacityCommitmentsResponse.SCHEMA_REPRESENTATION)
- [Authorization scopes](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments/list#body.aspect)
- [Try it!](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments/list#try-it)

Lists all the capacity commitments for the admin project.

### HTTP request

`GET https://bigqueryreservation.googleapis.com/v1/{parent=projects/*/locations/*}/capacityCommitments`

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
<p>Required. Resource name of the parent reservation. E.g., <code>projects/myproject/locations/US</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>bigquery.capacityCommitments.list</code></li>
</ul></td>
</tr>
</tbody>
</table>

### Query parameters

| Parameters  |                                                                                 |
|-------------|---------------------------------------------------------------------------------|
| `pageSize`  | `integer` The maximum number of items to return.                                |
| `pageToken` | `string` The nextPageToken value returned from a previous List request, if any. |

### Request body

The request body must be empty.

### Response body

The response for [`ReservationService.ListCapacityCommitments`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments/list#google.cloud.bigquery.reservation.v1.ReservationService.ListCapacityCommitments) .

If successful, the response body contains data with the following structure:

**JSON representation**

```
{
  "capacityCommitments": [
    {
      object (CapacityCommitment)
    }
  ],
  "nextPageToken": string
}
```

| Fields                  |                                                                                                                                                                                                                               |
|-------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `capacityCommitments[]` | `object ( `[`CapacityCommitment`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments#CapacityCommitment)` )` List of capacity commitments visible to the user. |
| `nextPageToken`         | `string` Token to retrieve the next page of results, or empty if there are no more results in the list.                                                                                                                       |

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
