---
name: documents/docs.cloud.google.com/bigquery/docs/reference/auditlogs/rest/Shared.Types/RoutineReference
uri: https://docs.cloud.google.com/bigquery/docs/reference/auditlogs/rest/Shared.Types/RoutineReference
title: RoutineReference
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/auditlogs/rest/Shared.Types/RoutineReference#SCHEMA_REPRESENTATION)

Id path of a routine.

**JSON representation**

```
{
  "projectId": string,
  "datasetId": string,
  "routineId": string
}
```

| Fields      |                                                                                                                                                                  |
|-------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `projectId` | `string` Required. The ID of the project containing this routine.                                                                                                |
| `datasetId` | `string` Required. The ID of the dataset containing this routine.                                                                                                |
| `routineId` | `string` Required. The ID of the routine. The ID must contain only letters (a-z, A-Z), numbers (0-9), or underscores (\_). The maximum length is 256 characters. |
