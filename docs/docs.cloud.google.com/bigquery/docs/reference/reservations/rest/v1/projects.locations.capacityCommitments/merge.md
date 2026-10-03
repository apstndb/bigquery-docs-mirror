---
name: documents/docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments/merge
uri: https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments/merge
title: 'Method: projects.locations.capacityCommitments.merge'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [HTTP request](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments/merge#body.HTTP_TEMPLATE)
- [Path parameters](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments/merge#body.PATH_PARAMETERS)
- [Request body](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments/merge#body.request_body)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments/merge#body.request_body.SCHEMA_REPRESENTATION)
- [Response body](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments/merge#body.response_body)
- [Authorization scopes](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments/merge#body.aspect)
- [Try it!](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments/merge#try-it)

Merges capacity commitments of the same plan into a single commitment.

The resulting capacity commitment has the greater commitmentEndTime out of the to-be-merged capacity commitments.

Attempting to merge capacity commitments of different plan will fail with the error code `google.rpc.Code.FAILED_PRECONDITION` .

### HTTP request

`POST https://bigqueryreservation.googleapis.com/v1/{parent=projects/*/locations/*}/capacityCommitments:merge`

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
<p>Parent resource that identifies admin project and location e.g., <code>projects/myproject/locations/us</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>bigquery.capacityCommitments.update</code></li>
</ul></td>
</tr>
</tbody>
</table>

### Request body

The request body contains data with the following structure:

**JSON representation**

```
{
  "capacityCommitmentIds": [
    string
  ],
  "capacityCommitmentId": string
}
```

| Fields                    |                                                                                                                                                                                                                                                                                                           |
|---------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `capacityCommitmentIds[]` | `string` Ids of capacity commitments to merge. These capacity commitments must exist under admin project and location specified in the parent. ID is the last portion of capacity commitment name e.g., 'abc' for projects/myproject/locations/US/capacityCommitments/abc                                 |
| `capacityCommitmentId`    | `string` Optional. The optional resulting capacity commitment ID. Capacity commitment name will be generated automatically if this field is empty. This field must only contain lower case alphanumeric characters or dashes. The first and last character cannot be a dash. Max length is 64 characters. |

### Response body

If successful, the response body contains an instance of [`CapacityCommitment`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments#CapacityCommitment) .

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
