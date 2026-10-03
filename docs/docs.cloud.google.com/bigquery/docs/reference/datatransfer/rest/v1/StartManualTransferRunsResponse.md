---
name: documents/docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/StartManualTransferRunsResponse
uri: https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/StartManualTransferRunsResponse
title: StartManualTransferRunsResponse
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/StartManualTransferRunsResponse#SCHEMA_REPRESENTATION)

A response to start manual transfer runs.

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

| Fields   |                                                                                                                                                                                                     |
|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `runs[]` | `object ( `[`TransferRun`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.runs#TransferRun)` )` The transfer runs that were created. |
