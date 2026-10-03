---
name: documents/docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/ListTransferRunsResponse
uri: https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/ListTransferRunsResponse
title: ListTransferRunsResponse
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/ListTransferRunsResponse#SCHEMA_REPRESENTATION)

The returned list of pipelines in the project.

**JSON representation**

```
{
  "transferRuns": [
    {
      object (TransferRun)
    }
  ],
  "nextPageToken": string
}
```

| Fields           |                                                                                                                                                                                                                |
|------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `transferRuns[]` | `object ( `[`TransferRun`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.runs#TransferRun)` )` Output only. The stored pipeline transfer runs. |
| `nextPageToken`  | `string` Output only. The next-pagination token. For multiple-page list results, this token can be used as the `ListTransferRunsRequest.page_token` to request the next page of list results.                  |
