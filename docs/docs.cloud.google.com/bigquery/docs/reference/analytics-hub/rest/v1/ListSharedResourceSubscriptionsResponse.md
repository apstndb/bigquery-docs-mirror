---
name: documents/docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/ListSharedResourceSubscriptionsResponse
uri: https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/ListSharedResourceSubscriptionsResponse
title: ListSharedResourceSubscriptionsResponse
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/ListSharedResourceSubscriptionsResponse#SCHEMA_REPRESENTATION)

Message for response to the listing of shared resource subscriptions.

**JSON representation**

```
{
  "sharedResourceSubscriptions": [
    {
      object (Subscription)
    }
  ],
  "nextPageToken": string
}
```

| Fields                          |                                                                                                                                                                |
|---------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `sharedResourceSubscriptions[]` | `object ( `[`Subscription`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/Shared.Types/Subscription)` )` The list of subscriptions. |
| `nextPageToken`                 | `string` Next page token.                                                                                                                                      |
