---
name: documents/docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/Shared.Types/RefreshSubscriptionResponse
uri: https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/Shared.Types/RefreshSubscriptionResponse
title: RefreshSubscriptionResponse
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/Shared.Types/RefreshSubscriptionResponse#SCHEMA_REPRESENTATION)

Message for response when you refresh a subscription.

**JSON representation**

```
{
  "subscription": {
    object (Subscription)
  }
}
```

| Fields         |                                                                                                                                                                          |
|----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `subscription` | `object ( `[`Subscription`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/Shared.Types/Subscription)` )` The refreshed subscription resource. |
