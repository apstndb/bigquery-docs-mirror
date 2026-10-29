---
name: documents/docs.cloud.google.com/bigquery/docs/reference/rest/v2/SecureContext
uri: https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/SecureContext
title: SecureContext
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/SecureContext#SCHEMA_REPRESENTATION)

A set of key-value pairs representing the secure context.

**JSON representation**

```
{
  "secureParameterEntries": {
    object
  }
}
```

| Fields                   |                                                                                                                                                                                                                                                                                            |
|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `secureParameterEntries` | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Optional. A set of key-value pairs representing the secure parameter values. They can be retrieved via the SECURE_CONTEXT() function and used to modify the run-time behavior of a query. |
