---
name: documents/docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/SchedulingPolicy
uri: https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/SchedulingPolicy
title: SchedulingPolicy
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/SchedulingPolicy#SCHEMA_REPRESENTATION)

The scheduling policy controls how a reservation's resources are distributed.

**JSON representation**

```
{
  "concurrency": string,
  "maxSlots": string
}
```

| Fields        |                                                                                                                                                                                                                                                                                                           |
|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `concurrency` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Optional. If present and \> 0, the reservation will attempt to limit the concurrency of jobs running for any particular project within it to the given value. This feature is not yet generally available.         |
| `maxSlots`    | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Optional. If present and \> 0, the reservation will attempt to limit the slot consumption of queries running for any particular project within it to the given value. This feature is not yet generally available. |
