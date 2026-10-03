---
name: documents/docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments
uri: https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments
title: 'REST Resource: projects.locations.capacityCommitments'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [Resource: CapacityCommitment](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments#CapacityCommitment)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments#CapacityCommitment.SCHEMA_REPRESENTATION)
- [CommitmentPlan](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments#CommitmentPlan)
- [State](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments#State)
- [Methods](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments#METHODS_SUMMARY)

## Resource: CapacityCommitment

Capacity commitment is a way to purchase compute capacity for BigQuery jobs (in the form of slots) with some committed period of usage. Annual commitments renew by default. Commitments can be removed after their commitment end time passes.

In order to remove annual commitment, its plan needs to be changed to monthly or flex first.

A capacity commitment resource exists as a child resource of the admin project.

**JSON representation**

```
{
  "name": string,
  "slotCount": string,
  "plan": enum (CommitmentPlan),
  "state": enum (State),
  "commitmentStartTime": string,
  "commitmentEndTime": string,
  "failureStatus": {
    object (Status)
  },
  "renewalPlan": enum (CommitmentPlan),
  "edition": enum (Edition),
  "isFlatRate": boolean
}
```

| Fields                |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|-----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                | `string` Output only. The resource name of the capacity commitment, e.g., `projects/myproject/locations/US/capacityCommitments/123` The commitment_id must only contain lower case alphanumeric characters or dashes. It must start with a letter and must not end with a dash. Its maximum length is 64 characters.                                                                                                                                                                                                                                                                                                                                                                      |
| `slotCount`           | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Optional. Number of slots in this commitment.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `plan`                | `enum ( `[`CommitmentPlan`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments#CommitmentPlan)` )` Optional. Capacity commitment commitment plan.                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `state`               | `enum ( `[`State`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments#State)` )` Output only. State of the commitment.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `commitmentStartTime` | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. The start of the current commitment period. It is applicable only for ACTIVE capacity commitments. Note after the commitment is renewed, commitmentStartTime won't be changed. It refers to the start time of the original commitment. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                 |
| `commitmentEndTime`   | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. The end of the current commitment period. It is applicable only for ACTIVE capacity commitments. Note after renewal, commitmentEndTime is the time the renewed commitment expires. So itwould be at a time after commitmentStartTime + committed period, because we don't change commitmentStartTime , Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` . |
| `failureStatus`       | `object ( `[`Status`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/Status)` )` Output only. For FAILED commitment plan, provides the reason of failure.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `renewalPlan`         | `enum ( `[`CommitmentPlan`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments#CommitmentPlan)` )` Optional. The plan this capacity commitment is converted to after commitmentEndTime passes. Once the plan is changed, committed period is extended according to commitment plan. Only applicable for ANNUAL and TRIAL commitments.                                                                                                                                                                                                                                                                                      |
| `edition`             | `enum ( `[`Edition`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/Edition)` )` Optional. Edition of the capacity commitment.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `isFlatRate`          | `boolean` Output only. If true, the commitment is a flat-rate commitment, otherwise, it's an edition commitment.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |

## CommitmentPlan

Commitment plan defines the current committed period. Capacity commitment cannot be deleted during it's committed period.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Enums</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>COMMITMENT_PLAN_UNSPECIFIED</code></td>
<td>Invalid plan value. Requests with this value will be rejected with error code <code>google.rpc.Code.INVALID_ARGUMENT</code> .</td>
</tr>
<tr class="even">
<td><code>FLEX</code></td>
<td><p>Deprecated: Flex commitments are deprecated. Please use Edition-based capacity commitments. Flex commitments have committed period of 1 minute after becoming ACTIVE. After that, they are not in a committed period anymore and can be removed any time.</p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote></td>
</tr>
<tr class="odd">
<td><code>FLEX_FLAT_RATE</code></td>
<td><p>Same as FLEX, should only be used if flat-rate commitments are still available.</p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote></td>
</tr>
<tr class="even">
<td><code>TRIAL</code></td>
<td><p>Trial commitments have a committed period of 182 days after becoming ACTIVE. After that, they are converted to a new commitment based on the <code>renewalPlan</code> . Default <code>renewalPlan</code> for Trial commitment is Flex so that it can be deleted right after committed period ends.</p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote></td>
</tr>
<tr class="odd">
<td><code>MONTHLY</code></td>
<td>Monthly commitments have a committed period of 30 days after becoming ACTIVE. After that, they are not in a committed period anymore and can be removed any time.</td>
</tr>
<tr class="even">
<td><code>MONTHLY_FLAT_RATE</code></td>
<td><p>Same as MONTHLY, should only be used if flat-rate commitments are still available.</p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote></td>
</tr>
<tr class="odd">
<td><code>ANNUAL</code></td>
<td>Annual commitments have a committed period of 365 days after becoming ACTIVE. After that they are converted to a new commitment based on the renewalPlan.</td>
</tr>
<tr class="even">
<td><code>ANNUAL_FLAT_RATE</code></td>
<td><p>Same as ANNUAL, should only be used if flat-rate commitments are still available.</p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote></td>
</tr>
<tr class="odd">
<td><code>THREE_YEAR</code></td>
<td>3-year commitments have a committed period of 1095(3 * 365) days after becoming ACTIVE. After that they are converted to a new commitment based on the renewalPlan.</td>
</tr>
<tr class="even">
<td><code>NONE</code></td>
<td>Should only be used for <code>renewalPlan</code> and is only meaningful if edition is specified to values other than EDITION_UNSPECIFIED. Otherwise CreateCapacityCommitmentRequest or UpdateCapacityCommitmentRequest will be rejected with error code <code>google.rpc.Code.INVALID_ARGUMENT</code> . If the renewalPlan is NONE, capacity commitment will be removed at the end of its commitment period.</td>
</tr>
</tbody>
</table>

## State

Capacity commitment can either become ACTIVE right away or transition from PENDING to ACTIVE or FAILED.

| Enums               |                                                                                                                             |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------|
| `STATE_UNSPECIFIED` | Invalid state value.                                                                                                        |
| `PENDING`           | Capacity commitment is pending provisioning. Pending capacity commitment does not contribute to the project's slotCapacity. |
| `ACTIVE`            | Once slots are provisioned, capacity commitment becomes active. slotCount is added to the project's slotCapacity.           |
| `FAILED`            | Capacity commitment is failed to be activated by the backend.                                                               |

| Methods                                                                                                                              |                                                                                            |
|--------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------|
| [`create`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments/create) | Creates a new capacity commitment resource.                                                |
| [`delete`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments/delete) | Deletes a capacity commitment.                                                             |
| [`get`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments/get)       | Returns information about the capacity commitment.                                         |
| [`list`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments/list)     | Lists all the capacity commitments for the admin project.                                  |
| [`merge`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments/merge)   | Merges capacity commitments of the same plan into a single commitment.                     |
| [`patch`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments/patch)   | Updates an existing capacity commitment.                                                   |
| [`split`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.capacityCommitments/split)   | Splits capacity commitment to two commitments of the same plan and `commitment_end_time` . |
