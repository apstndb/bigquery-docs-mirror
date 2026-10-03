---
name: documents/docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/ScheduleTransferRunsResponse
uri: https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/ScheduleTransferRunsResponse
title: ScheduleTransferRunsResponse
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/ScheduleTransferRunsResponse#SCHEMA_REPRESENTATION)

A response to schedule transfer runs for a time range.

**JSON representation**

```
{
  "runs": [
    {
      object (TransferRun)
    }
  ]
}
```

| Fields   |                                                                                                                                                                                                       |
|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `runs[]` | `object ( `[`TransferRun`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.runs#TransferRun)` )` The transfer runs that were scheduled. |
