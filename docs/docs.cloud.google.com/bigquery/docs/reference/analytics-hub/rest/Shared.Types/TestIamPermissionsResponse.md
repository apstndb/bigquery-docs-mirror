---
name: documents/docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/Shared.Types/TestIamPermissionsResponse
uri: https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/Shared.Types/TestIamPermissionsResponse
title: TestIamPermissionsResponse
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/Shared.Types/TestIamPermissionsResponse#SCHEMA_REPRESENTATION)

Response message for `TestIamPermissions` method.

**JSON representation**

```
{
  "permissions": [
    string
  ]
}
```

| Fields          |                                                                                       |
|-----------------|---------------------------------------------------------------------------------------|
| `permissions[]` | `string` A subset of `TestPermissionsRequest.permissions` that the caller is allowed. |
