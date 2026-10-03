---
name: documents/docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservationGroups
uri: https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservationGroups
title: 'REST Resource: projects.locations.reservationGroups'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [Resource: ReservationGroup](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservationGroups#ReservationGroup)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservationGroups#ReservationGroup.SCHEMA_REPRESENTATION)
- [Methods](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservationGroups#METHODS_SUMMARY)

## Resource: ReservationGroup

A reservation group is a container for reservations.

**JSON representation**

```
{
  "name": string,
  "creationTime": string,
  "updateTime": string
}
```

| Fields         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`         | `string` Identifier. The resource name of the reservation group, e.g., `projects/*/locations/*/reservationGroups/team1-prod` . The reservationGroupId must only contain lower case alphanumeric characters or dashes. It must start with a letter and must not end with a dash. Its maximum length is 64 characters.                                                                                                                                                                                                                                                                                                                           |
| `creationTime` | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Creation time of the reservation group. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                                                                                                                                     |
| `updateTime`   | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Last update time of the reservation group via a user operation. This timestamp is updated only when an update operation explicitly targets this reservation group directly. It is not updated when parent or child groups are created, updated, or deleted. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` . |

| Methods                                                                                                                            |                                                                             |
|------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------|
| [`create`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservationGroups/create) | Creates a new reservation group.                                            |
| [`delete`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservationGroups/delete) | Deletes a reservation.                                                      |
| [`get`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservationGroups/get)       | Returns information about the reservation group.                            |
| [`list`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservationGroups/list)     | Lists all the reservation groups for the project in the specified location. |
