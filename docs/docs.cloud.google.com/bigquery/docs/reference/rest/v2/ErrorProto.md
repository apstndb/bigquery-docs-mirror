---
name: documents/docs.cloud.google.com/bigquery/docs/reference/rest/v2/ErrorProto
uri: https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/ErrorProto
title: ErrorProto
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/ErrorProto#SCHEMA_REPRESENTATION)

Error details.

**JSON representation**

```
{
  "reason": string,
  "location": string,
  "debugInfo": string,
  "message": string
}
```

| Fields      |                                                                                             |
|-------------|---------------------------------------------------------------------------------------------|
| `reason`    | `string` A short error code that summarizes the error.                                      |
| `location`  | `string` Specifies where the error occurred, if present.                                    |
| `debugInfo` | `string` Debugging information. This property is internal to Google and should not be used. |
| `message`   | `string` A human-readable description of the error.                                         |
