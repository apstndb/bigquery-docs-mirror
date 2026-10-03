---
name: documents/docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.transferConfigs.transferResources
uri: https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.transferConfigs.transferResources
title: 'REST Resource: projects.transferConfigs.transferResources'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [Resource: TransferResource](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.transferConfigs.transferResources#TransferResource)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.transferConfigs.transferResources#TransferResource.SCHEMA_REPRESENTATION)
- [Methods](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.transferConfigs.transferResources#METHODS_SUMMARY)

## Resource: TransferResource

Resource (table/partition) that is being transferred.

**JSON representation**

```
{
  "name": string,
  "type": enum (ResourceType),
  "destination": enum (ResourceDestination),
  "latestRun": {
    object (TransferRunBrief)
  },
  "latestStatusDetail": {
    object (TransferResourceStatusDetail)
  },
  "lastSuccessfulRun": {
    object (TransferRunBrief)
  },
  "hierarchyDetail": {
    object (HierarchyDetail)
  },
  "updateTime": string
}
```

| Fields               |                                                                                                                                                                                                                                                                             |
|----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`               | `string` Identifier. Resource name.                                                                                                                                                                                                                                         |
| `type`               | `enum ( `[`ResourceType`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.transferResources#TransferResource.ResourceType)` )` Optional. Resource type.                                                       |
| `destination`        | `enum ( `[`ResourceDestination`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.transferResources#TransferResource.ResourceDestination)` )` Optional. Resource destination.                                  |
| `latestRun`          | `object ( `[`TransferRunBrief`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.transferResources#TransferResource.TransferRunBrief)` )` Optional. Run details for the latest run.                            |
| `latestStatusDetail` | `object ( `[`TransferResourceStatusDetail`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.transferResources#TransferResource.TransferResourceStatusDetail)` )` Optional. Status details for the latest run. |
| `lastSuccessfulRun`  | `object ( `[`TransferRunBrief`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.transferResources#TransferResource.TransferRunBrief)` )` Output only. Run details for the last successful run.                |
| `hierarchyDetail`    | `object ( `[`HierarchyDetail`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.transferResources#TransferResource.HierarchyDetail)` )` Optional. Details about the hierarchy.                                 |
| `updateTime`         | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Time when the resource was last updated.                                                                                                                |

| Methods                                                                                                                              |                                               |
|--------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------|
| [`get`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.transferConfigs.transferResources/get)   | Returns a transfer resource.                  |
| [`list`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.transferConfigs.transferResources/list) | Returns information about transfer resources. |
