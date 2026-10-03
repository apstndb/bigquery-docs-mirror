---
name: documents/docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/ListTransferLogsResponse
uri: https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/ListTransferLogsResponse
title: ListTransferLogsResponse
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/ListTransferLogsResponse#SCHEMA_REPRESENTATION)

The returned list transfer run messages.

**JSON representation**

```
{
  "transferMessages": [
    {
      object (TransferMessage)
    }
  ],
  "nextPageToken": string
}
```

| Fields               |                                                                                                                                                                                                                                         |
|----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `transferMessages[]` | `object ( `[`TransferMessage`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.runs.transferLogs#TransferMessage)` )` Output only. The stored pipeline transfer messages. |
| `nextPageToken`      | `string` Output only. The next-pagination token. For multiple-page list results, this token can be used as the `GetTransferRunLogRequest.page_token` to request the next page of list results.                                          |
