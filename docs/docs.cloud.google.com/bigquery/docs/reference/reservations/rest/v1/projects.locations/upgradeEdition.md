---
name: documents/docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations/upgradeEdition
uri: https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations/upgradeEdition
title: 'Method: projects.locations.upgradeEdition'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [HTTP request](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations/upgradeEdition#body.HTTP_TEMPLATE)
- [Path parameters](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations/upgradeEdition#body.PATH_PARAMETERS)
- [Request body](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations/upgradeEdition#body.request_body)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations/upgradeEdition#body.request_body.SCHEMA_REPRESENTATION)
- [Response body](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations/upgradeEdition#body.response_body)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations/upgradeEdition#body.UpgradeEditionResponse.SCHEMA_REPRESENTATION)
- [Authorization scopes](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations/upgradeEdition#body.aspect)
- [Try it!](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations/upgradeEdition#try-it)

Upgrades the [`edition`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/Edition) for a list of reservations and capacity commitments.

You can only upgrade to a higher edition (from `STANDARD` to `ENTERPRISE` or `ENTERPRISE_PLUS` , from `ENTERPRISE` to `ENTERPRISE_PLUS` , or from `EDITION_UNSPECIFIED` to `ENTERPRISE` or `ENTERPRISE_PLUS` ). You can't downgrade an edition.

The upgrade must not cause an overall flexible slot increase across the original and target editions (for example, by upgrading a reservation without upgrading its corresponding capacity commitment). Otherwise, the method fails with a `google.rpc.Code.FAILED_PRECONDITION` error.

Before the upgrade, the service validates that the resources meet the requirements of the target edition (for example, all reservations within a reservation group must be upgraded together).

### HTTP request

`POST https://bigqueryreservation.googleapis.com/v1/{parent=projects/*/locations/*}:upgradeEdition`

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

| Parameters |                                                                                                                                                                                                    |
|------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parent`   | `string` The parent resource name that identifies the admin project and location, in the format `projects/{project}/locations/{location}` . For example, `projects/myproject/locations/us-west1` . |

### Request body

The request body contains data with the following structure:

**JSON representation**

```
{
  "targetEdition": enum (Edition),
  "capacityCommitments": [
    string
  ],
  "reservations": [
    string
  ]
}
```

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>targetEdition</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/Edition"><code>Edition</code></a><code> )</code></p>
<p>The <a href="https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/Edition"><code>edition</code></a> to upgrade the capacity commitments and reservations to. Supported values are <code>ENTERPRISE</code> and <code>ENTERPRISE_PLUS</code> .</p></td>
</tr>
<tr class="even">
<td><code>capacityCommitments[]</code></td>
<td><p><code>string</code></p>
<p>Optional. The resource names of the capacity commitments to upgrade, in the format <code>projects/{project}/locations/{location}/capacityCommitments/{capacityCommitment}</code> . For example, <code>projects/myproject/locations/us-west1/capacityCommitments/123</code> .</p>
<p>These capacity commitments must be in the <code>ACTIVE</code> state and must exist under the specified <code>parent</code> . The <code>commitmentStartTime</code> and <code>commitmentEndTime</code> fields don't change after the upgrade.</p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>capacityCommitments</code> :</p>
<ul>
<li><code>bigquery.capacityCommitments.update</code></li>
</ul></td>
</tr>
<tr class="odd">
<td><code>reservations[]</code></td>
<td><p><code>string</code></p>
<p>Optional. The resource names of the reservations to upgrade, in the format <code>projects/{project}/locations/{location}/reservations/{reservation}</code> . For example, <code>projects/myproject/locations/us-west1/reservations/team1-prod</code> .</p>
<p>These reservations must exist under the specified <code>parent</code> .</p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>reservations</code> :</p>
<ul>
<li><code>bigquery.reservations.update</code></li>
</ul></td>
</tr>
</tbody>
</table>

### Response body

The response for [`ReservationService.UpgradeEdition`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations/upgradeEdition#google.cloud.bigquery.reservation.v1.ReservationService.UpgradeEdition) .

If successful, the response body contains data with the following structure:

**JSON representation**

```
{
  "capacityCommitments": [
    {
      object (CapacityCommitment)
    }
  ],
  "reservations": [
    {
      object (Reservation)
    }
  ]
}
```

| Fields                  |                                                                                                                                                                                                                                 |
|-------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `capacityCommitments[]` | `object ( `[`CapacityCommitment`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments#CapacityCommitment)` )` The updated capacity commitments after the upgrade. |
| `reservations[]`        | `object ( `[`Reservation`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations#Reservation)` )` The updated reservations after the upgrade.                              |

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
