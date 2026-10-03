---
name: documents/docs.cloud.google.com/bigquery/docs/reference/rest/v2/StandardSqlField
uri: https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/StandardSqlField
title: StandardSqlField
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/StandardSqlField#SCHEMA_REPRESENTATION)

A field or a column.

**JSON representation**

```
{
  "name": string,
  "type": {
    object (StandardSqlDataType)
  }
}
```

| Fields |                                                                                                                                                                                                                                                                                                                                   |
|--------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name` | `string` Optional. The name of this field. Can be absent for struct fields.                                                                                                                                                                                                                                                       |
| `type` | `object ( `[`StandardSqlDataType`](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/StandardSqlDataType)` )` Optional. The type of this parameter. Absent if not explicitly specified (e.g., CREATE FUNCTION statement can omit the return type; in this case the output parameter does not have this "type" field). |
