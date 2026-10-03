---
name: documents/docs.cloud.google.com/bigquery/docs/reference/auditlogs/rest/Shared.Types/DatasetAccessEntry
uri: https://docs.cloud.google.com/bigquery/docs/reference/auditlogs/rest/Shared.Types/DatasetAccessEntry
title: DatasetAccessEntry
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/auditlogs/rest/Shared.Types/DatasetAccessEntry#SCHEMA_REPRESENTATION)
- [DatasetReference](https://docs.cloud.google.com/bigquery/docs/reference/auditlogs/rest/Shared.Types/DatasetAccessEntry#DatasetReference)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/auditlogs/rest/Shared.Types/DatasetAccessEntry#DatasetReference.SCHEMA_REPRESENTATION)

Grants all resources of particular types in a particular dataset read access to the current dataset.

Similar to how individually authorized views work, updates to any resource granted through its dataset (including creation of new resources) requires read permission to referenced resources, plus write permission to the authorizing dataset.

**JSON representation**

```
{
  "dataset": {
    object (DatasetReference)
  },
  "targetTypes": [
    enum (DatasetAccessEntry.TargetType)
  ]
}
```

| Fields          |                                                                                                                                                                                                                                                                                                                    |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `dataset`       | `object ( `[`DatasetReference`](https://docs.cloud.google.com/bigquery/docs/reference/auditlogs/rest/Shared.Types/DatasetAccessEntry#DatasetReference)` )` The dataset this entry applies to                                                                                                                       |
| `targetTypes[]` | `enum ( `[`DatasetAccessEntry.TargetType`](https://docs.cloud.google.com/bigquery/docs/reference/auditlogs/rest/Shared.Types/DatasetAccessEntry.TargetType)` )` Which resources in the dataset this entry applies to. Currently, only views are supported, but additional target types may be added in the future. |

## DatasetReference

Identifier for a dataset.

**JSON representation**

```
{
  "datasetId": string,
  "projectId": string
}
```

| Fields      |                                                                                                                                                                                                     |
|-------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `datasetId` | `string` Required. A unique ID for this dataset, without the project name. The ID must contain only letters (a-z, A-Z), numbers (0-9), or underscores (\_). The maximum length is 1,024 characters. |
| `projectId` | `string` Optional. The ID of the project containing this dataset.                                                                                                                                   |
