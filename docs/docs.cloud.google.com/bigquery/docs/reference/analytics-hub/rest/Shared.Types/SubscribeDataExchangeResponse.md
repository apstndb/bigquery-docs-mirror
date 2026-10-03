---
name: documents/docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/Shared.Types/SubscribeDataExchangeResponse
uri: https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/Shared.Types/SubscribeDataExchangeResponse
title: SubscribeDataExchangeResponse
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/Shared.Types/SubscribeDataExchangeResponse#SCHEMA_REPRESENTATION)

Message for response when you subscribe to a Data Exchange.

**JSON representation**

```
{
  "subscription": {
    object (Subscription)
  }
}
```

| Fields         |                                                                                                                                                                                             |
|----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `subscription` | `object ( `[`Subscription`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/Shared.Types/Subscription)` )` Subscription object created from this subscribe action. |
