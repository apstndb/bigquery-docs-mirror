---
name: documents/docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.runs
uri: https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.runs
title: 'REST Resource: projects.locations.transferConfigs.runs'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [Resource: TransferRun](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.runs#TransferRun)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.runs#TransferRun.SCHEMA_REPRESENTATION)
- [Methods](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.runs#METHODS_SUMMARY)

## Resource: TransferRun

Represents a data transfer run.

**JSON representation**

```
{
  "name": string,
  "scheduleTime": string,
  "runTime": string,
  "errorStatus": {
    object (Status)
  },
  "startTime": string,
  "endTime": string,
  "updateTime": string,
  "params": {
    object
  },
  "dataSourceId": string,
  "state": enum (TransferState),
  "userId": string,
  "schedule": string,
  "notificationPubsubTopic": string,
  "emailPreferences": {
    object (EmailPreferences)
  },
  "parameterConfig": {
    object (ParameterConfig)
  },

  // The following is a list of mutually exclusive fields. At most one of the
  // fields will be set in a response:
  "destinationDatasetId": string
  // End of mutually exclusive fields.
}
```

| Fields                                                                                                                                |                                                                                                                                                                                                                                                                                                                                                                                                                  |
|---------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                                                                                                                                | `string` Identifier. The resource name of the transfer run. Transfer run names have the form `projects/{projectId}/locations/{location}/transferConfigs/{configId}/runs/{run_id}` . The name is ignored when creating a transfer run.                                                                                                                                                                            |
| `scheduleTime`                                                                                                                        | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Minimum time after which a transfer run can be started.                                                                                                                                                                                                                                                   |
| `runTime`                                                                                                                             | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` For batch transfer runs, specifies the date and time of the data should be ingested.                                                                                                                                                                                                                      |
| `errorStatus`                                                                                                                         | `object ( `[`Status`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/Status)` )` Status of the transfer run.                                                                                                                                                                                                                                                                         |
| `startTime`                                                                                                                           | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Time when transfer run was started. Parameter ignored by server for input requests.                                                                                                                                                                                                          |
| `endTime`                                                                                                                             | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Time when transfer run ended. Parameter ignored by server for input requests.                                                                                                                                                                                                                |
| `updateTime`                                                                                                                          | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Last time the data transfer run state was updated.                                                                                                                                                                                                                                           |
| `params`                                                                                                                              | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Output only. Parameters specific to each data source. For more information see the bq tab in the 'Setting up a data transfer' section for each data source. For example the parameters for Cloud Storage transfers are listed here: <https://cloud.google.com/bigquery-transfer/docs/cloud-storage-transfer#bq> |
| `dataSourceId`                                                                                                                        | `string` Output only. Data source id.                                                                                                                                                                                                                                                                                                                                                                            |
| `state`                                                                                                                               | `enum ( `[`TransferState`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/TransferState)` )` Data transfer run state. Ignored for input requests.                                                                                                                                                                                                                                    |
| `userId`                                                                                                                              | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Deprecated. Unique ID of the user on whose behalf transfer is done.                                                                                                                                                                                                                                                       |
| `schedule`                                                                                                                            | `string` Output only. Describes the schedule of this transfer run if it was created as part of a regular schedule. For batch transfer runs that are scheduled manually, this is empty. NOTE: the system might choose to delay the schedule depending on the current load, so `scheduleTime` doesn't always match this.                                                                                           |
| `notificationPubsubTopic`                                                                                                             | `string` Output only. Pub/Sub topic where a notification will be sent after this transfer run finishes. The format for specifying a pubsub topic is: `projects/{projectId}/topics/{topic_id}`                                                                                                                                                                                                                    |
| `emailPreferences`                                                                                                                    | `object ( `[`EmailPreferences`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/EmailPreferences)` )` Output only. Email notifications will be sent according to these preferences to the email address of the user who owns the transfer config this run was derived from.                                                                                                           |
| `parameterConfig`                                                                                                                     | `object ( `[`ParameterConfig`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/ParameterConfig)` )` Output only. The parameter config of the transfer run.                                                                                                                                                                                                                            |
| Data transfer destination. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response: |                                                                                                                                                                                                                                                                                                                                                                                                                  |
| `destinationDatasetId`                                                                                                                | `string` Output only. The BigQuery target dataset id.                                                                                                                                                                                                                                                                                                                                                            |
| End of mutually exclusive fields.                                                                                                     |                                                                                                                                                                                                                                                                                                                                                                                                                  |

| Methods                                                                                                                               |                                                                |
|---------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------|
| [`delete`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.runs/delete) | Deletes the specified transfer run.                            |
| [`get`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.runs/get)       | Returns information about the particular transfer run.         |
| [`list`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.runs/list)     | Returns information about running and completed transfer runs. |
