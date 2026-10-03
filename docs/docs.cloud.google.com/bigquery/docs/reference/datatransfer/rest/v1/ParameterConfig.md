---
name: documents/docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/ParameterConfig
uri: https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/ParameterConfig
title: ParameterConfig
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/ParameterConfig#SCHEMA_REPRESENTATION)

Configuration for data source parameters.

**JSON representation**

```
{
  "secretManagerManagedParams": [
    string
  ]
}
```

| Fields                         |                                                                                                                                                                                                                                                                                           |
|--------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `secretManagerManagedParams[]` | `string` Optional. The list of parameters that are stored in Secret Manager. The value of a parameter included in this list will be interpreted as a Secret Manager key version resource name instead of a raw value. The raw value will be retrieved from Secret Manager upon execution. |
