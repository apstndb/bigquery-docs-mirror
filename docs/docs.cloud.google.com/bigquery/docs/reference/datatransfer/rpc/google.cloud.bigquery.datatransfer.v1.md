---
name: documents/docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1
uri: https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1
title: Package google.cloud.bigquery.datatransfer.v1
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

## Index

- [`DataTransferService`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.DataTransferService) (interface)
- [`CheckValidCredsRequest`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.CheckValidCredsRequest) (message)
- [`CheckValidCredsResponse`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.CheckValidCredsResponse) (message)
- [`CreateTransferConfigRequest`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.CreateTransferConfigRequest) (message)
- [`DataSource`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.DataSource) (message)
- [`DataSource.AuthorizationType`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.DataSource.AuthorizationType) (enum)
- [`DataSource.DataRefreshType`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.DataSource.DataRefreshType) (enum)
- [`DataSourceParameter`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.DataSourceParameter) (message)
- [`DataSourceParameter.Type`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.DataSourceParameter.Type) (enum)
- [`DataplexConfiguration`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.DataplexConfiguration) (message)
- [`DeleteTransferConfigRequest`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.DeleteTransferConfigRequest) (message)
- [`DeleteTransferRunRequest`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.DeleteTransferRunRequest) (message)
- [`EmailPreferences`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.EmailPreferences) (message)
- [`EncryptionConfiguration`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.EncryptionConfiguration) (message)
- [`EnrollDataSourcesRequest`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.EnrollDataSourcesRequest) (message)
- [`EventDrivenSchedule`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.EventDrivenSchedule) (message)
- [`GetDataSourceRequest`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.GetDataSourceRequest) (message)
- [`GetTransferConfigRequest`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.GetTransferConfigRequest) (message)
- [`GetTransferResourceRequest`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.GetTransferResourceRequest) (message)
- [`GetTransferRunRequest`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.GetTransferRunRequest) (message)
- [`HierarchyDetail`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.HierarchyDetail) (message)
- [`ListDataSourcesRequest`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.ListDataSourcesRequest) (message)
- [`ListDataSourcesResponse`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.ListDataSourcesResponse) (message)
- [`ListTransferConfigsRequest`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.ListTransferConfigsRequest) (message)
- [`ListTransferConfigsResponse`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.ListTransferConfigsResponse) (message)
- [`ListTransferLogsRequest`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.ListTransferLogsRequest) (message)
- [`ListTransferLogsResponse`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.ListTransferLogsResponse) (message)
- [`ListTransferResourcesRequest`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.ListTransferResourcesRequest) (message)
- [`ListTransferResourcesResponse`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.ListTransferResourcesResponse) (message)
- [`ListTransferRunsRequest`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.ListTransferRunsRequest) (message)
- [`ListTransferRunsRequest.RunAttempt`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.ListTransferRunsRequest.RunAttempt) (enum)
- [`ListTransferRunsResponse`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.ListTransferRunsResponse) (message)
- [`ManagedTableType`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.ManagedTableType) (enum)
- [`ManualSchedule`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.ManualSchedule) (message)
- [`MetadataDestination`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.MetadataDestination) (message)
- [`PartitionDetail`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.PartitionDetail) (message)
- [`ResourceDestination`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.ResourceDestination) (enum)
- [`ResourceTransferState`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.ResourceTransferState) (enum)
- [`ResourceType`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.ResourceType) (enum)
- [`ScheduleOptions`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.ScheduleOptions) (message)
- [`ScheduleOptionsV2`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.ScheduleOptionsV2) (message)
- [`ScheduleTransferRunsRequest`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.ScheduleTransferRunsRequest) (message)
- [`ScheduleTransferRunsResponse`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.ScheduleTransferRunsResponse) (message)
- [`StartManualTransferRunsRequest`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.StartManualTransferRunsRequest) (message)
- [`StartManualTransferRunsRequest.TimeRange`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.StartManualTransferRunsRequest.TimeRange) (message)
- [`StartManualTransferRunsResponse`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.StartManualTransferRunsResponse) (message)
- [`TableDetail`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.TableDetail) (message)
- [`TimeBasedSchedule`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.TimeBasedSchedule) (message)
- [`TransferConfig`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.TransferConfig) (message)
- [`TransferConfig.ParameterConfig`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.TransferConfig.ParameterConfig) (message)
- [`TransferMessage`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.TransferMessage) (message)
- [`TransferMessage.MessageSeverity`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.TransferMessage.MessageSeverity) (enum)
- [`TransferResource`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.TransferResource) (message)
- [`TransferResourceStatusDetail`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.TransferResourceStatusDetail) (message)
- [`TransferRun`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.TransferRun) (message)
- [`TransferRunBrief`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.TransferRunBrief) (message)
- [`TransferState`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.TransferState) (enum)
- [`TransferStatusMetric`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.TransferStatusMetric) (message)
- [`TransferStatusSummary`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.TransferStatusSummary) (message)
- [`TransferStatusUnit`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.TransferStatusUnit) (enum)
- [`TransferType`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.TransferType) (enum) **(deprecated)**
- [`UnenrollDataSourcesRequest`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.UnenrollDataSourcesRequest) (message)
- [`UpdateTransferConfigRequest`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.UpdateTransferConfigRequest) (message)
- [`UserInfo`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.UserInfo) (message)

## DataTransferService

This API allows users to manage their data transfers into BigQuery.

**CheckValidCreds**

`rpc CheckValidCreds( `[`CheckValidCredsRequest`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.CheckValidCredsRequest)` ) returns ( `[`CheckValidCredsResponse`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.CheckValidCredsResponse)` )`

Returns true if valid credentials exist for the given data source and requesting user.

Authorization scopes  
Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**CreateTransferConfig**

`rpc CreateTransferConfig( `[`CreateTransferConfigRequest`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.CreateTransferConfigRequest)` ) returns ( `[`TransferConfig`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.TransferConfig)` )`

Creates a new data transfer configuration.

Authorization scopes  
Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**DeleteTransferConfig**

`rpc DeleteTransferConfig( `[`DeleteTransferConfigRequest`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.DeleteTransferConfigRequest)` ) returns ( `[`Empty`](https://protobuf.dev/reference/protobuf/google.protobuf/#empty)` )`

Deletes a data transfer configuration, including any associated transfer runs and logs.

Authorization scopes  
Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**DeleteTransferRun**

`rpc DeleteTransferRun( `[`DeleteTransferRunRequest`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.DeleteTransferRunRequest)` ) returns ( `[`Empty`](https://protobuf.dev/reference/protobuf/google.protobuf/#empty)` )`

Deletes the specified transfer run.

Authorization scopes  
Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**EnrollDataSources**

`rpc EnrollDataSources( `[`EnrollDataSourcesRequest`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.EnrollDataSourcesRequest)` ) returns ( `[`Empty`](https://protobuf.dev/reference/protobuf/google.protobuf/#empty)` )`

Enroll data sources in a user project. This allows users to create transfer configurations for these data sources. They will also appear in the ListDataSources RPC and as such, will appear in the [BigQuery UI](https://console.cloud.google.com/bigquery) , and the documents can be found in the public guide for [BigQuery Web UI](https://cloud.google.com/bigquery/bigquery-web-ui) and [Data Transfer Service](https://cloud.google.com/bigquery/docs/working-with-transfers) .

Authorization scopes  
Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**GetDataSource**

`rpc GetDataSource( `[`GetDataSourceRequest`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.GetDataSourceRequest)` ) returns ( `[`DataSource`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.DataSource)` )`

Retrieves a supported data source and returns its settings.

Authorization scopes  
Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**GetTransferConfig**

`rpc GetTransferConfig( `[`GetTransferConfigRequest`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.GetTransferConfigRequest)` ) returns ( `[`TransferConfig`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.TransferConfig)` )`

Returns information about a data transfer config.

Authorization scopes  
Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**GetTransferResource**

`rpc GetTransferResource( `[`GetTransferResourceRequest`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.GetTransferResourceRequest)` ) returns ( `[`TransferResource`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.TransferResource)` )`

Returns a transfer resource.

Authorization scopes  
Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**GetTransferRun**

`rpc GetTransferRun( `[`GetTransferRunRequest`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.GetTransferRunRequest)` ) returns ( `[`TransferRun`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.TransferRun)` )`

Returns information about the particular transfer run.

Authorization scopes  
Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**ListDataSources**

`rpc ListDataSources( `[`ListDataSourcesRequest`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.ListDataSourcesRequest)` ) returns ( `[`ListDataSourcesResponse`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.ListDataSourcesResponse)` )`

Lists supported data sources and returns their settings.

Authorization scopes  
Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**ListTransferConfigs**

`rpc ListTransferConfigs( `[`ListTransferConfigsRequest`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.ListTransferConfigsRequest)` ) returns ( `[`ListTransferConfigsResponse`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.ListTransferConfigsResponse)` )`

Returns information about all transfer configs owned by a project in the specified location.

Authorization scopes  
Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**ListTransferLogs**

`rpc ListTransferLogs( `[`ListTransferLogsRequest`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.ListTransferLogsRequest)` ) returns ( `[`ListTransferLogsResponse`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.ListTransferLogsResponse)` )`

Returns log messages for the transfer run.

Authorization scopes  
Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**ListTransferResources**

`rpc ListTransferResources( `[`ListTransferResourcesRequest`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.ListTransferResourcesRequest)` ) returns ( `[`ListTransferResourcesResponse`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.ListTransferResourcesResponse)` )`

Returns information about transfer resources.

Authorization scopes  
Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**ListTransferRuns**

`rpc ListTransferRuns( `[`ListTransferRunsRequest`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.ListTransferRunsRequest)` ) returns ( `[`ListTransferRunsResponse`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.ListTransferRunsResponse)` )`

Returns information about running and completed transfer runs.

Authorization scopes  
Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**ScheduleTransferRuns**

> This item is deprecated!

`rpc ScheduleTransferRuns( `[`ScheduleTransferRunsRequest`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.ScheduleTransferRunsRequest)` ) returns ( `[`ScheduleTransferRunsResponse`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.ScheduleTransferRunsResponse)` )`

Creates transfer runs for a time range \[start_time, end_time\]. For each date - or whatever granularity the data source supports - in the range, one transfer run is created. Note that runs are created per UTC time in the time range. DEPRECATED: use StartManualTransferRuns instead.

Authorization scopes  
Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**StartManualTransferRuns**

`rpc StartManualTransferRuns( `[`StartManualTransferRunsRequest`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.StartManualTransferRunsRequest)` ) returns ( `[`StartManualTransferRunsResponse`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.StartManualTransferRunsResponse)` )`

Manually initiates transfer runs. You can schedule these runs in two ways:

1.  For a specific point in time using the 'requested_run_time' parameter.
2.  For a period between 'start_time' (inclusive) and 'end_time' (exclusive).

If scheduling a single run, it is set to execute immediately (schedule_time equals the current time). When scheduling multiple runs within a time range, the first run starts now, and subsequent runs are delayed by 15 seconds each.

Authorization scopes  
Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**UnenrollDataSources**

`rpc UnenrollDataSources( `[`UnenrollDataSourcesRequest`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.UnenrollDataSourcesRequest)` ) returns ( `[`Empty`](https://protobuf.dev/reference/protobuf/google.protobuf/#empty)` )`

Unenroll data sources in a user project. This allows users to remove transfer configurations for these data sources. They will no longer appear in the ListDataSources RPC and will also no longer appear in the [BigQuery UI](https://console.cloud.google.com/bigquery) . Data transfers configurations of unenrolled data sources will not be scheduled.

Authorization scopes  
Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**UpdateTransferConfig**

`rpc UpdateTransferConfig( `[`UpdateTransferConfigRequest`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.UpdateTransferConfigRequest)` ) returns ( `[`TransferConfig`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.TransferConfig)` )`

Updates a data transfer configuration. All fields must be set, even if they are not updated.

Authorization scopes  
Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

## CheckValidCredsRequest

A request to determine whether the user has valid credentials. This method is used to limit the number of OAuth popups in the user interface. The user id is inferred from the API call context. If the data source has the Google+ authorization type, this method returns false, as it cannot be determined whether the credentials are already valid merely based on the user id.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. The name of the data source. If you are using the regionless method, the location must be <code>US</code> and the name should be in the following form:</p>
<ul>
<li><code>projects/{project_id}/dataSources/{data_source_id}</code></li>
</ul>
<p>If you are using the regionalized method, the name should be in the following form:</p>
<ul>
<li><code>projects/{project_id}/locations/{location_id}/dataSources/{data_source_id}</code></li>
</ul>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>bigquery.transfers.get</code></li>
</ul></td>
</tr>
</tbody>
</table>

## CheckValidCredsResponse

A response indicating whether the credentials exist and are valid.

| Fields            |                                                                |
|-------------------|----------------------------------------------------------------|
| `has_valid_creds` | `bool` If set to `true` , the credentials exist and are valid. |

## CreateTransferConfigRequest

A request to create a data transfer configuration. If new credentials are needed for this transfer configuration, authorization info must be provided. If authorization info is provided, the transfer configuration will be associated with the user id corresponding to the authorization info. Otherwise, the transfer configuration will be associated with the calling user.

When using a cross project service account for creating a transfer config, you must enable cross project service account usage. For more information, see [Disable attachment of service accounts to resources in other projects](https://cloud.google.com/resource-manager/docs/organization-policy/restricting-service-accounts#disable_cross_project_service_accounts) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>parent</code></td>
<td><p><code>string</code></p>
<p>Required. The BigQuery project id where the transfer configuration should be created. Must be in the format projects/{project_id}/locations/{location_id} or projects/{project_id}. If specified location and location of the destination bigquery dataset do not match - the request will fail.</p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>bigquery.transfers.update</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>transfer_config</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.TransferConfig"><code>TransferConfig</code></a></p>
<p>Required. Data transfer configuration to create.</p></td>
</tr>
<tr class="odd">
<td><code>authorization_code </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>string</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Deprecated: Authorization code was required when <code>transferConfig.dataSourceId</code> is 'youtube_channel' but it is no longer used in any data sources. Use <code>version_info</code> instead.</p>
<p>Optional OAuth2 authorization code to use with this transfer configuration. This is required only if <code>transferConfig.dataSourceId</code> is 'youtube_channel' and new credentials are needed, as indicated by <code>CheckValidCreds</code> . In order to obtain authorization_code, make a request to the following URL:</p>
<pre data-fenced=""><code>https://bigquery.cloud.google.com/datatransfer/oauthz/auth?redirect_uri=urn:ietf:wg:oauth:2.0:oob&amp;response_type=authorization_code&amp;client_id=client_id&amp;scope=data_source_scopes</code></pre>
<ul>
<li>The <var translate="no"> client_id </var> is the OAuth client_id of the data source as returned by ListDataSources method.</li>
<li><var translate="no"> data_source_scopes </var> are the scopes returned by ListDataSources method.</li>
</ul>
<p>Note that this should not be set when <code>service_account_name</code> is used to create the transfer config.</p></td>
</tr>
<tr class="even">
<td><code>version_info</code></td>
<td><p><code>string</code></p>
<p>Optional version info. This parameter replaces <code>authorization_code</code> which is no longer used in any data sources. This is required only if <code>transferConfig.dataSourceId</code> is 'youtube_channel' <em>or</em> new credentials are needed, as indicated by <code>CheckValidCreds</code> . In order to obtain version info, make a request to the following URL:</p>
<pre data-fenced=""><code>https://bigquery.cloud.google.com/datatransfer/oauthz/auth?redirect_uri=urn:ietf:wg:oauth:2.0:oob&amp;response_type=version_info&amp;client_id=client_id&amp;scope=data_source_scopes</code></pre>
<ul>
<li>The <var translate="no"> client_id </var> is the OAuth client_id of the data source as returned by ListDataSources method.</li>
<li><var translate="no"> data_source_scopes </var> are the scopes returned by ListDataSources method.</li>
</ul>
<p>Note that this should not be set when <code>service_account_name</code> is used to create the transfer config.</p></td>
</tr>
<tr class="odd">
<td><code>service_account_name</code></td>
<td><p><code>string</code></p>
<p>Optional service account email. If this field is set, the transfer config will be created with this service account's credentials. It requires that the requesting user calling this API has permissions to act as this service account.</p>
<p>Note that not all data sources support service account credentials when creating a transfer config. For the latest list of data sources, read about <a href="https://cloud.google.com/bigquery-transfer/docs/use-service-accounts">using service accounts</a> .</p></td>
</tr>
</tbody>
</table>

## DataSource

Defines the properties and custom parameters for a data source.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Output only. Data source resource name.</p></td>
</tr>
<tr class="even">
<td><code>data_source_id</code></td>
<td><p><code>string</code></p>
<p>Data source id.</p></td>
</tr>
<tr class="odd">
<td><code>display_name</code></td>
<td><p><code>string</code></p>
<p>User friendly data source name.</p></td>
</tr>
<tr class="even">
<td><code>description</code></td>
<td><p><code>string</code></p>
<p>User friendly data source description string.</p></td>
</tr>
<tr class="odd">
<td><code>client_id</code></td>
<td><p><code>string</code></p>
<p>Data source client id which should be used to receive refresh token.</p></td>
</tr>
<tr class="even">
<td><code>scopes[]</code></td>
<td><p><code>string</code></p>
<p>Api auth scopes for which refresh token needs to be obtained. These are scopes needed by a data source to prepare data and ingest them into BigQuery, e.g., <a href="https://www.googleapis.com/auth/bigquery">https://www.googleapis.com/auth/bigquery</a></p></td>
</tr>
<tr class="odd">
<td><code>transfer_type </code><strong><code>(deprecated)</code></strong></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.TransferType"><code>TransferType</code></a></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Deprecated. This field has no effect.</p></td>
</tr>
<tr class="even">
<td><code>supports_multiple_transfers </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>bool</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Deprecated. This field has no effect.</p></td>
</tr>
<tr class="odd">
<td><code>update_deadline_seconds</code></td>
<td><p><code>int32</code></p>
<p>The number of seconds to wait for an update from the data source before the Data Transfer Service marks the transfer as FAILED.</p></td>
</tr>
<tr class="even">
<td><code>default_schedule</code></td>
<td><p><code>string</code></p>
<p>Default data transfer schedule. Examples of valid schedules include: <code>1st,3rd monday of month 15:30</code> , <code>every wed,fri of jan,jun 13:15</code> , and <code>first sunday of quarter 00:00</code> .</p></td>
</tr>
<tr class="odd">
<td><code>supports_custom_schedule</code></td>
<td><p><code>bool</code></p>
<p>Specifies whether the data source supports a user defined schedule, or operates on the default schedule. When set to <code>true</code> , user can override default schedule.</p></td>
</tr>
<tr class="even">
<td><code>parameters[]</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.DataSourceParameter"><code>DataSourceParameter</code></a></p>
<p>Data source parameters.</p></td>
</tr>
<tr class="odd">
<td><code>help_url</code></td>
<td><p><code>string</code></p>
<p>Url for the help document for this data source.</p></td>
</tr>
<tr class="even">
<td><code>authorization_type</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.DataSource.AuthorizationType"><code>AuthorizationType</code></a></p>
<p>Indicates the type of authorization.</p></td>
</tr>
<tr class="odd">
<td><code>data_refresh_type</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.DataSource.DataRefreshType"><code>DataRefreshType</code></a></p>
<p>Specifies whether the data source supports automatic data refresh for the past few days, and how it's supported. For some data sources, data might not be complete until a few days later, so it's useful to refresh data automatically.</p></td>
</tr>
<tr class="even">
<td><code>default_data_refresh_window_days</code></td>
<td><p><code>int32</code></p>
<p>Default data refresh window on days. Only meaningful when <code>data_refresh_type</code> = <code>SLIDING_WINDOW</code> .</p></td>
</tr>
<tr class="odd">
<td><code>manual_runs_disabled</code></td>
<td><p><code>bool</code></p>
<p>Disables backfilling and manual run scheduling for the data source.</p></td>
</tr>
<tr class="even">
<td><code>minimum_schedule_interval</code></td>
<td><p><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#duration"><code>Duration</code></a></p>
<p>The minimum interval for scheduler to schedule runs.</p></td>
</tr>
</tbody>
</table>

## AuthorizationType

The type of authorization needed for this data source.

| Enums                            |                                                                                                                      |
|----------------------------------|----------------------------------------------------------------------------------------------------------------------|
| `AUTHORIZATION_TYPE_UNSPECIFIED` | Type unspecified.                                                                                                    |
| `AUTHORIZATION_CODE`             | Use OAuth 2 authorization codes that can be exchanged for a refresh token on the backend.                            |
| `GOOGLE_PLUS_AUTHORIZATION_CODE` | Return an authorization code for a given Google+ page that can then be exchanged for a refresh token on the backend. |
| `FIRST_PARTY_OAUTH`              | Use First Party OAuth.                                                                                               |

## DataRefreshType

Represents how the data source supports data auto refresh.

| Enums                           |                                                                                                                                                                |
|---------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `DATA_REFRESH_TYPE_UNSPECIFIED` | The data source won't support data auto refresh, which is default value.                                                                                       |
| `SLIDING_WINDOW`                | The data source supports data auto refresh, and runs will be scheduled for the past few days. Does not allow custom values to be set for each transfer config. |
| `CUSTOM_SLIDING_WINDOW`         | The data source supports data auto refresh, and runs will be scheduled for the past few days. Allows custom values to be set for each transfer config.         |

## DataSourceParameter

A parameter used to define custom fields in a data source definition.

| Fields                   |                                                                                                                                                                                                                                       |
|--------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `param_id`               | `string` Parameter identifier.                                                                                                                                                                                                        |
| `display_name`           | `string` Parameter display name in the user interface.                                                                                                                                                                                |
| `description`            | `string` Parameter description.                                                                                                                                                                                                       |
| `type`                   | [`Type`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.DataSourceParameter.Type) Parameter type.                                 |
| `required`               | `bool` Is parameter required.                                                                                                                                                                                                         |
| `repeated`               | `bool` Deprecated. This field has no effect.                                                                                                                                                                                          |
| `validation_regex`       | `string` Regular expression which can be used for parameter validation.                                                                                                                                                               |
| `allowed_values[]`       | `string` All possible values for the parameter.                                                                                                                                                                                       |
| `min_value`              | [`DoubleValue`](https://protobuf.dev/reference/protobuf/google.protobuf/#double-value) For integer and double values specifies minimum allowed value.                                                                                 |
| `max_value`              | [`DoubleValue`](https://protobuf.dev/reference/protobuf/google.protobuf/#double-value) For integer and double values specifies maximum allowed value.                                                                                 |
| `fields[]`               | [`DataSourceParameter`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.DataSourceParameter) Deprecated. This field has no effect. |
| `validation_description` | `string` Description of the requirements for this field, in case the user input does not fulfill the regex pattern or min/max values.                                                                                                 |
| `validation_help_url`    | `string` URL to a help document to further explain the naming requirements.                                                                                                                                                           |
| `immutable`              | `bool` Cannot be changed after initial creation.                                                                                                                                                                                      |
| `recurse`                | `bool` Deprecated. This field has no effect.                                                                                                                                                                                          |
| `deprecated`             | `bool` If true, it should not be used in new transfers, and it should not be visible to users.                                                                                                                                        |
| `secret_manager_allowed` | `bool` Output only. If true, the parameter value can be provided through Secret Manager.                                                                                                                                              |
| `max_list_size`          | `int64` For list parameters, the max size of the list.                                                                                                                                                                                |

## Type

Parameter type.

| Enums              |                                                                    |
|--------------------|--------------------------------------------------------------------|
| `TYPE_UNSPECIFIED` | Type unspecified.                                                  |
| `STRING`           | String parameter.                                                  |
| `INTEGER`          | Integer parameter (64-bits). Will be serialized to json as string. |
| `DOUBLE`           | Double precision floating point parameter.                         |
| `BOOLEAN`          | Boolean parameter.                                                 |
| `RECORD`           | Deprecated. This field has no effect.                              |
| `PLUS_PAGE`        | Page ID for a Google+ Page.                                        |
| `LIST`             | List of strings parameter.                                         |

## DataplexConfiguration

Configuration for Dataplex destination.

| Fields        |                                                                                                                                                                                                   |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `entry_group` | `string` Required. The Dataplex Universal Catalog entry group for importing the metadata. entry_group has the format of `projects/{project_id}/locations/{region}/entryGroups/{entry_group_id}` . |

## DeleteTransferConfigRequest

A request to delete data transfer information. All associated transfer runs and log messages will be deleted as well.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. The name of the resource to delete. If you are using the regionless method, the location must be <code>US</code> and the name should be in the following form:</p>
<ul>
<li><code>projects/{project_id}/transferConfigs/{config_id}</code></li>
</ul>
<p>If you are using the regionalized method, the name should be in the following form:</p>
<ul>
<li><code>projects/{project_id}/locations/{location_id}/transferConfigs/{config_id}</code></li>
</ul>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>bigquery.transfers.update</code></li>
</ul></td>
</tr>
</tbody>
</table>

## DeleteTransferRunRequest

A request to delete data transfer run information.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. The name of the resource requested. If you are using the regionless method, the location must be <code>US</code> and the name should be in the following form:</p>
<ul>
<li><code>projects/{project_id}/transferConfigs/{config_id}/runs/{run_id}</code></li>
</ul>
<p>If you are using the regionalized method, the name should be in the following form:</p>
<ul>
<li><code>projects/{project_id}/locations/{location_id}/transferConfigs/{config_id}/runs/{run_id}</code></li>
</ul>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>bigquery.transfers.update</code></li>
</ul></td>
</tr>
</tbody>
</table>

## EmailPreferences

Represents preferences for sending email notifications for transfer run events.

| Fields                 |                                                                            |
|------------------------|----------------------------------------------------------------------------|
| `enable_failure_email` | `bool` If true, email notifications will be sent on transfer run failures. |

## EncryptionConfiguration

Represents the encryption configuration for a transfer.

| Fields         |                                                                                                                                                   |
|----------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| `kms_key_name` | [`StringValue`](https://protobuf.dev/reference/protobuf/google.protobuf/#string-value) The name of the KMS key used for encrypting BigQuery data. |

## EnrollDataSourcesRequest

A request to enroll a set of data sources so they are visible in the BigQuery UI's `Transfer` tab.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. The name of the project resource in the form: <code>projects/{project_id}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>resourcemanager.projects.update</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>data_source_ids[]</code></td>
<td><p><code>string</code></p>
<p>Data sources that are enrolled. It is required to provide at least one data source id.</p></td>
</tr>
</tbody>
</table>

## EventDrivenSchedule

Options customizing EventDriven transfers schedule.

| Fields                                                                                                                                                                                                             |                                                                                                                                                                               |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `eventStream` . The event stream which specifies the Event-driven transfer options. Event-driven transfers listen to an event stream to transfer data. `eventStream` can be only one of the following: |                                                                                                                                                                               |
| `pubsub_subscription`                                                                                                                                                                                              | `string` Pub/Sub subscription name used to receive events. Only Google Cloud Storage data source support this option. Format: projects/{project}/subscriptions/{subscription} |

## GetDataSourceRequest

A request to get data source info.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. The name of the resource requested. If you are using the regionless method, the location must be <code>US</code> and the name should be in the following form:</p>
<ul>
<li><code>projects/{project_id}/dataSources/{data_source_id}</code></li>
</ul>
<p>If you are using the regionalized method, the name should be in the following form:</p>
<ul>
<li><code>projects/{project_id}/locations/{location_id}/dataSources/{data_source_id}</code></li>
</ul>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>bigquery.transfers.get</code></li>
</ul></td>
</tr>
</tbody>
</table>

## GetTransferConfigRequest

A request to get data transfer information.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. The name of the resource requested. If you are using the regionless method, the location must be <code>US</code> and the name should be in the following form:</p>
<ul>
<li><code>projects/{project_id}/transferConfigs/{config_id}</code></li>
</ul>
<p>If you are using the regionalized method, the name should be in the following form:</p>
<ul>
<li><code>projects/{project_id}/locations/{location_id}/transferConfigs/{config_id}</code></li>
</ul>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>bigquery.transfers.get</code></li>
</ul></td>
</tr>
</tbody>
</table>

## GetTransferResourceRequest

Request message for `GetTransferResource` RPC.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. The name of the transfer resource in the form of:</p>
<ul>
<li><code>projects/{project}/transferConfigs/{transfer_config}/transferResources/{transfer_resource}</code></li>
<li><code>projects/{project}/locations/{location}/transferConfigs/{transfer_config}/transferResources/{transfer_resource}</code></li>
</ul>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>bigquery.transfers.get</code></li>
</ul></td>
</tr>
</tbody>
</table>

## GetTransferRunRequest

A request to get data transfer run information.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. The name of the resource requested. If you are using the regionless method, the location must be <code>US</code> and the name should be in the following form:</p>
<ul>
<li><code>projects/{project_id}/transferConfigs/{config_id}/runs/{run_id}</code></li>
</ul>
<p>If you are using the regionalized method, the name should be in the following form:</p>
<ul>
<li><code>projects/{project_id}/locations/{location_id}/transferConfigs/{config_id}/runs/{run_id}</code></li>
</ul>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>bigquery.transfers.get</code></li>
</ul></td>
</tr>
</tbody>
</table>

## HierarchyDetail

Details about the hierarchy.

| Fields                                                                                                                       |                                                                                                                                                                                                                                           |
|------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `detail` . Details about the hierarchy can be one of table/partition. `detail` can be only one of the following: |                                                                                                                                                                                                                                           |
| `table_detail`                                                                                                               | [`TableDetail`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.TableDetail) Optional. Table details related to hierarchy.             |
| `partition_detail`                                                                                                           | [`PartitionDetail`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.PartitionDetail) Optional. Partition details related to hierarchy. |

## ListDataSourcesRequest

Request to list supported data sources and their data transfer settings.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>parent</code></td>
<td><p><code>string</code></p>
<p>Required. The BigQuery project id for which data sources should be returned. Must be in the form: <code>projects/{project_id}</code> or <code>projects/{project_id}/locations/{location_id}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>bigquery.transfers.get</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>page_token</code></td>
<td><p><code>string</code></p>
<p>Pagination token, which can be used to request a specific page of <code>ListDataSourcesRequest</code> list results. For multiple-page results, <code>ListDataSourcesResponse</code> outputs a <code>next_page</code> token, which can be used as the <code>page_token</code> value to request the next page of list results.</p></td>
</tr>
<tr class="odd">
<td><code>page_size</code></td>
<td><p><code>int32</code></p>
<p>Page size. The default page size is the maximum value of 1000 results.</p></td>
</tr>
</tbody>
</table>

## ListDataSourcesResponse

Returns list of supported data sources and their metadata.

| Fields            |                                                                                                                                                                                                                                           |
|-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `data_sources[]`  | [`DataSource`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.DataSource) List of supported data sources and their transfer settings. |
| `next_page_token` | `string` Output only. The next-pagination token. For multiple-page list results, this token can be used as the `ListDataSourcesRequest.page_token` to request the next page of list results.                                              |

## ListTransferConfigsRequest

A request to list data transfers configured for a BigQuery project.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>parent</code></td>
<td><p><code>string</code></p>
<p>Required. The BigQuery project id for which transfer configs should be returned. If you are using the regionless method, the location must be <code>US</code> and <code>parent</code> should be in the following form:</p>
<ul>
<li>`projects/{project_id}</li>
</ul>
<p>If you are using the regionalized method, <code>parent</code> should be in the following form:</p>
<ul>
<li><code>projects/{project_id}/locations/{location_id}</code></li>
</ul>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>bigquery.transfers.get</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>data_source_ids[]</code></td>
<td><p><code>string</code></p>
<p>When specified, only configurations of requested data sources are returned.</p></td>
</tr>
<tr class="odd">
<td><code>page_token</code></td>
<td><p><code>string</code></p>
<p>Pagination token, which can be used to request a specific page of <code>ListTransfersRequest</code> list results. For multiple-page results, <code>ListTransfersResponse</code> outputs a <code>next_page</code> token, which can be used as the <code>page_token</code> value to request the next page of list results.</p></td>
</tr>
<tr class="even">
<td><code>page_size</code></td>
<td><p><code>int32</code></p>
<p>Page size. The default page size is the maximum value of 1000 results.</p></td>
</tr>
</tbody>
</table>

## ListTransferConfigsResponse

The returned list of pipelines in the project.

| Fields               |                                                                                                                                                                                                                                                 |
|----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `transfer_configs[]` | [`TransferConfig`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.TransferConfig) Output only. The stored pipeline transfer configurations. |
| `next_page_token`    | `string` Output only. The next-pagination token. For multiple-page list results, this token can be used as the `ListTransferConfigsRequest.page_token` to request the next page of list results.                                                |

## ListTransferLogsRequest

A request to get user facing log messages associated with data transfer run.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>parent</code></td>
<td><p><code>string</code></p>
<p>Required. Transfer run name. If you are using the regionless method, the location must be <code>US</code> and the name should be in the following form:</p>
<ul>
<li><code>projects/{project_id}/transferConfigs/{config_id}/runs/{run_id}</code></li>
</ul>
<p>If you are using the regionalized method, the name should be in the following form:</p>
<ul>
<li><code>projects/{project_id}/locations/{location_id}/transferConfigs/{config_id}/runs/{run_id}</code></li>
</ul>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>bigquery.transfers.get</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>page_token</code></td>
<td><p><code>string</code></p>
<p>Pagination token, which can be used to request a specific page of <code>ListTransferLogsRequest</code> list results. For multiple-page results, <code>ListTransferLogsResponse</code> outputs a <code>next_page</code> token, which can be used as the <code>page_token</code> value to request the next page of list results.</p></td>
</tr>
<tr class="odd">
<td><code>page_size</code></td>
<td><p><code>int32</code></p>
<p>Page size. The default page size is the maximum value of 1000 results.</p></td>
</tr>
<tr class="even">
<td><code>message_types[]</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.TransferMessage.MessageSeverity"><code>MessageSeverity</code></a></p>
<p>Message types to return. If not populated - INFO, WARNING and ERROR messages are returned.</p></td>
</tr>
</tbody>
</table>

## ListTransferLogsResponse

The returned list transfer run messages.

| Fields                |                                                                                                                                                                                                                                             |
|-----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `transfer_messages[]` | [`TransferMessage`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.TransferMessage) Output only. The stored pipeline transfer messages. |
| `next_page_token`     | `string` Output only. The next-pagination token. For multiple-page list results, this token can be used as the `GetTransferRunLogRequest.page_token` to request the next page of list results.                                              |

## ListTransferResourcesRequest

Request for the `ListTransferResources` RPC.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>parent</code></td>
<td><p><code>string</code></p>
<p>Required. Name of transfer configuration for which transfer resources should be retrieved. The name should be in one of the following forms:</p>
<ul>
<li><code>projects/{project}/transferConfigs/{transfer_config}</code></li>
<li><code>projects/{project}/locations/{location_id}/transferConfigs/{transfer_config}</code></li>
</ul>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>bigquery.transfers.get</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>page_size</code></td>
<td><p><code>int32</code></p>
<p>Optional. The maximum number of transfer resources to return. The maximum value is 1000; values above 1000 will be coerced to 1000. The default page size is the maximum value of 1000 results.</p></td>
</tr>
<tr class="odd">
<td><code>page_token</code></td>
<td><p><code>string</code></p>
<p>Optional. A page token, received from a previous <code>ListTransferResources</code> call. Provide this to retrieve the subsequent page. When paginating, all other parameters provided to <code>ListTransferResources</code> must match the call that provided the page token.</p></td>
</tr>
<tr class="even">
<td><code>filter</code></td>
<td><p><code>string</code></p>
<p>Optional. Filter for the transfer resources. Currently supported filters include:</p>
<ul>
<li>Resource name: <code>name</code> - Wildcard supported</li>
<li>Resource type: <code>type</code></li>
<li>Resource destination: <code>destination</code></li>
<li>Latest resource state: <code>latest_status_detail.state</code></li>
<li>Last update time: <code>update_time</code> - RFC-3339 format</li>
<li>Parent table name: <code>hierarchy_detail.partition_detail.table</code></li>
</ul>
<p>Multiple filters can be applied using the <code>AND/OR</code> operator.</p>
<p>Examples:</p>
<ul>
<li><code>name="*123" AND (type="TABLE" OR latest_status_detail.state="SUCCEEDED")</code></li>
<li><code>update_time &gt;= "2012-04-21T11:30:00-04:00"</code></li>
<li><code>hierarchy_detail.partition_detail.table = "table1"</code></li>
</ul></td>
</tr>
</tbody>
</table>

## ListTransferResourcesResponse

Response for the `ListTransferResources` RPC.

| Fields                 |                                                                                                                                                                                                                                |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `transfer_resources[]` | [`TransferResource`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.TransferResource) Output only. The transfer resources. |
| `next_page_token`      | `string` Output only. A token, which can be sent as `page_token` to retrieve the next page. If this field is omitted, there are no subsequent pages.                                                                           |

## ListTransferRunsRequest

A request to list data transfer runs.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>parent</code></td>
<td><p><code>string</code></p>
<p>Required. Name of transfer configuration for which transfer runs should be retrieved. If you are using the regionless method, the location must be <code>US</code> and the name should be in the following form:</p>
<ul>
<li><code>projects/{project_id}/transferConfigs/{config_id}</code></li>
</ul>
<p>If you are using the regionalized method, the name should be in the following form:</p>
<ul>
<li><code>projects/{project_id}/locations/{location_id}/transferConfigs/{config_id}</code></li>
</ul>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>bigquery.transfers.get</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>states[]</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.TransferState"><code>TransferState</code></a></p>
<p>When specified, only transfer runs with requested states are returned.</p></td>
</tr>
<tr class="odd">
<td><code>page_token</code></td>
<td><p><code>string</code></p>
<p>Pagination token, which can be used to request a specific page of <code>ListTransferRunsRequest</code> list results. For multiple-page results, <code>ListTransferRunsResponse</code> outputs a <code>next_page</code> token, which can be used as the <code>page_token</code> value to request the next page of list results.</p></td>
</tr>
<tr class="even">
<td><code>page_size</code></td>
<td><p><code>int32</code></p>
<p>Page size. The default page size is the maximum value of 1000 results.</p></td>
</tr>
<tr class="odd">
<td><code>run_attempt</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.ListTransferRunsRequest.RunAttempt"><code>RunAttempt</code></a></p>
<p>Indicates how run attempts are to be pulled.</p></td>
</tr>
</tbody>
</table>

## RunAttempt

Represents which runs should be pulled.

| Enums                     |                                             |
|---------------------------|---------------------------------------------|
| `RUN_ATTEMPT_UNSPECIFIED` | All runs should be returned.                |
| `LATEST`                  | Only latest run per day should be returned. |

## ListTransferRunsResponse

The returned list of pipelines in the project.

| Fields            |                                                                                                                                                                                                                                 |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `transfer_runs[]` | [`TransferRun`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.TransferRun) Output only. The stored pipeline transfer runs. |
| `next_page_token` | `string` Output only. The next-pagination token. For multiple-page list results, this token can be used as the `ListTransferRunsRequest.page_token` to request the next page of list results.                                   |

## ManagedTableType

The classifications of managed tables that can be created, native or BigLake.

| Enums                            |                                                                                                                           |
|----------------------------------|---------------------------------------------------------------------------------------------------------------------------|
| `MANAGED_TABLE_TYPE_UNSPECIFIED` | Type unspecified. This defaults to `NATIVE` table.                                                                        |
| `NATIVE`                         | The managed table is a native BigQuery table. This is the default value.                                                  |
| `BIGLAKE`                        | The managed table is a BigQuery table for Apache Iceberg (formerly BigLake managed tables), with a BigLake configuration. |

## ManualSchedule

This type has no fields.

Options customizing manual transfers schedule.

## MetadataDestination

The metadata destination of the transfer config.

| Fields                                                                                                                                                   |                                                                                                                                                                                                                                                   |
|----------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `destination` . The metadata destination of the transfer config can be one of the following: `destination` can be only one of the following: |                                                                                                                                                                                                                                                   |
| `dataplex_configuration`                                                                                                                                 | [`DataplexConfiguration`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.DataplexConfiguration) The Dataplex Universal Catalog configuration. |

## PartitionDetail

Partition details related to hierarchy.

| Fields  |                                                                |
|---------|----------------------------------------------------------------|
| `table` | `string` Optional. Name of the table which has the partitions. |

## ResourceDestination

The destination for a transferred resource.

| Enums                                       |                       |
|---------------------------------------------|-----------------------|
| `RESOURCE_DESTINATION_UNSPECIFIED`          | Default value.        |
| `RESOURCE_DESTINATION_BIGQUERY`             | BigQuery.             |
| `RESOURCE_DESTINATION_DATAPROC_METASTORE`   | Dataproc Metastore.   |
| `RESOURCE_DESTINATION_BIGLAKE_METASTORE`    | BigLake Metastore.    |
| `RESOURCE_DESTINATION_BIGLAKE_REST_CATALOG` | BigLake REST Catalog. |
| `RESOURCE_DESTINATION_BIGLAKE_HIVE_CATALOG` | BigLake Hive Catalog. |

## ResourceTransferState

The transfer state of an individual resource (e.g., a table or partition). This may differ from the overall transfer run's state. For instance, a resource can be transferred successfully even if the run as a whole fails.

| Enums                                 |                                        |
|---------------------------------------|----------------------------------------|
| `RESOURCE_TRANSFER_STATE_UNSPECIFIED` | Default value.                         |
| `RESOURCE_TRANSFER_PENDING`           | Resource is waiting to be transferred. |
| `RESOURCE_TRANSFER_RUNNING`           | Resource transfer is running.          |
| `RESOURCE_TRANSFER_SUCCEEDED`         | Resource transfer is a success.        |
| `RESOURCE_TRANSFER_FAILED`            | Resource transfer failed.              |
| `RESOURCE_TRANSFER_CANCELLED`         | Resource transfer was cancelled.       |

## ResourceType

Type of resource being transferred.

| Enums                       |                          |
|-----------------------------|--------------------------|
| `RESOURCE_TYPE_UNSPECIFIED` | Default value.           |
| `RESOURCE_TYPE_TABLE`       | Table resource type.     |
| `RESOURCE_TYPE_PARTITION`   | Partition resource type. |

## ScheduleOptions

Options customizing the data transfer schedule.

| Fields                    |                                                                                                                                                                                                                                                                                                                                                                                                      |
|---------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `disable_auto_scheduling` | `bool` If true, automatic scheduling of data transfer runs for this configuration will be disabled. The runs can be started on ad-hoc basis using StartManualTransferRuns API. When automatic scheduling is disabled, the TransferConfig.schedule field will be ignored.                                                                                                                             |
| `start_time`              | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Specifies time to start scheduling transfer runs. The first run will be scheduled at or after the start time according to a recurrence pattern defined in the schedule string. The start time can be changed at any moment. The time when a data transfer can be triggered manually is not limited by this option. |
| `end_time`                | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Defines time to stop scheduling transfer runs. A transfer run cannot be scheduled at or after the end time. The end time can be changed at any moment. The time when a data transfer can be triggered manually is not limited by this option.                                                                      |

## ScheduleOptionsV2

V2 options customizing different types of data transfer schedule. This field supports existing time-based and manual transfer schedule. Also supports Event-Driven transfer schedule. ScheduleOptionsV2 cannot be used together with ScheduleOptions/Schedule.

| Fields                                                                                         |                                                                                                                                                                                                                                                                                                                                                                                             |
|------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `schedule` . Data transfer schedules. `schedule` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                             |
| `time_based_schedule`                                                                          | [`TimeBasedSchedule`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.TimeBasedSchedule) Time based transfer schedule options. This is the default schedule option.                                                                                                                      |
| `manual_schedule`                                                                              | [`ManualSchedule`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.ManualSchedule) Manual transfer schedule. If set, the transfer run will not be auto-scheduled by the system, unless the client invokes StartManualTransferRuns. This is equivalent to disable_auto_scheduling = true. |
| `event_driven_schedule`                                                                        | [`EventDrivenSchedule`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.EventDrivenSchedule) Event driven transfer schedule options. If set, the transfer will be scheduled upon events arrial.                                                                                          |

## ScheduleTransferRunsRequest

A request to schedule transfer runs for a time range.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>parent</code></td>
<td><p><code>string</code></p>
<p>Required. Transfer configuration name. If you are using the regionless method, the location must be <code>US</code> and the name should be in the following form:</p>
<ul>
<li><code>projects/{project_id}/transferConfigs/{config_id}</code></li>
</ul>
<p>If you are using the regionalized method, the name should be in the following form:</p>
<ul>
<li><code>projects/{project_id}/locations/{location_id}/transferConfigs/{config_id}</code></li>
</ul>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>bigquery.transfers.update</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>start_time</code></td>
<td><p><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp"><code>Timestamp</code></a></p>
<p>Required. Start time of the range of transfer runs. For example, <code>"2017-05-25T00:00:00+00:00"</code> .</p></td>
</tr>
<tr class="odd">
<td><code>end_time</code></td>
<td><p><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp"><code>Timestamp</code></a></p>
<p>Required. End time of the range of transfer runs. For example, <code>"2017-05-30T00:00:00+00:00"</code> .</p></td>
</tr>
</tbody>
</table>

## ScheduleTransferRunsResponse

A response to schedule transfer runs for a time range.

| Fields   |                                                                                                                                                                                                                        |
|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `runs[]` | [`TransferRun`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.TransferRun) The transfer runs that were scheduled. |

## StartManualTransferRunsRequest

A request to start manual transfer runs.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>parent</code></td>
<td><p><code>string</code></p>
<p>Required. Transfer configuration name. If you are using the regionless method, the location must be <code>US</code> and the name should be in the following form:</p>
<ul>
<li><code>projects/{project_id}/transferConfigs/{config_id}</code></li>
</ul>
<p>If you are using the regionalized method, the name should be in the following form:</p>
<ul>
<li><code>projects/{project_id}/locations/{location_id}/transferConfigs/{config_id}</code></li>
</ul>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>bigquery.transfers.update</code></li>
</ul></td>
</tr>
<tr class="even">
<td>Union field <code>time</code> . The requested time specification - this can be a time range or a specific run_time. <code>time</code> can be only one of the following:</td>
<td></td>
</tr>
<tr class="odd">
<td><code>requested_time_range</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.StartManualTransferRunsRequest.TimeRange"><code>TimeRange</code></a></p>
<p>A time_range start and end timestamp for historical data files or reports that are scheduled to be transferred by the scheduled transfer run. requested_time_range must be a past time and cannot include future time values.</p></td>
</tr>
<tr class="even">
<td><code>requested_run_time</code></td>
<td><p><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp"><code>Timestamp</code></a></p>
<p>A run_time timestamp for historical data files or reports that are scheduled to be transferred by the scheduled transfer run. requested_run_time must be a past time and cannot include future time values.</p></td>
</tr>
</tbody>
</table>

## TimeRange

A specification for a time range, this will request transfer runs with run_time between start_time (inclusive) and end_time (exclusive).

| Fields       |                                                                                                                                                                                                                                                                                                                                                |
|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `start_time` | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Start time of the range of transfer runs. For example, `"2017-05-25T00:00:00+00:00"` . The start_time must be strictly less than the end_time. Creates transfer runs where run_time is in the range between start_time (inclusive) and end_time (exclusive). |
| `end_time`   | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) End time of the range of transfer runs. For example, `"2017-05-30T00:00:00+00:00"` . The end_time must not be in the future. Creates transfer runs where run_time is in the range between start_time (inclusive) and end_time (exclusive).                   |

## StartManualTransferRunsResponse

A response to start manual transfer runs.

| Fields   |                                                                                                                                                                                                                      |
|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `runs[]` | [`TransferRun`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.TransferRun) The transfer runs that were created. |

## TableDetail

Table details related to hierarchy.

| Fields            |                                                                              |
|-------------------|------------------------------------------------------------------------------|
| `partition_count` | `int64` Optional. Total number of partitions being tracked within the table. |

## TimeBasedSchedule

Options customizing the time based transfer schedule. Options are migrated from the original ScheduleOptions message.

| Fields       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `schedule`   | `string` Data transfer schedule. If the data source does not support a custom schedule, this should be empty. If it is empty, the default value for the data source will be used. The specified times are in UTC. Examples of valid format: `1st,3rd monday of month 15:30` , `every wed,fri of jan,jun 13:15` , and `first sunday of quarter 00:00` . See more explanation about the format here: <https://cloud.google.com/appengine/docs/flexible/python/scheduling-jobs-with-cron-yaml#the_schedule_format> NOTE: The minimum interval time between recurring transfers depends on the data source; refer to the documentation for your data source. |
| `start_time` | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Specifies time to start scheduling transfer runs. The first run will be scheduled at or after the start time according to a recurrence pattern defined in the schedule string. The start time can be changed at any moment.                                                                                                                                                                                                                                                                                                                                            |
| `end_time`   | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Defines time to stop scheduling transfer runs. A transfer run cannot be scheduled at or after the end time. The end time can be changed at any moment.                                                                                                                                                                                                                                                                                                                                                                                                                 |

## TransferConfig

Represents a data transfer configuration. A transfer configuration contains all metadata needed to perform a data transfer. For example, `destination_dataset_id` specifies where data should be stored. When a new transfer configuration is created, the specified `destination_dataset_id` is created when needed and shared with the appropriate data source service account.

| Fields                                                                                                              |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|---------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                                                                                                              | `string` Identifier. The resource name of the transfer config. Transfer config names have the form either `projects/{project_id}/locations/{region}/transferConfigs/{config_id}` or `projects/{project_id}/transferConfigs/{config_id}` , where `config_id` is usually a UUID, even though it is not guaranteed or required. The name is ignored when creating a transfer config.                                                                                                                                                                                                                                                                        |
| `display_name`                                                                                                      | `string` User specified display name for the data transfer.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `data_source_id`                                                                                                    | `string` Data source ID. This cannot be changed once data transfer is created. The full list of available data source IDs can be returned through an API call: <https://cloud.google.com/bigquery-transfer/docs/reference/datatransfer/rest/v1/projects.locations.dataSources/list>                                                                                                                                                                                                                                                                                                                                                                      |
| `params`                                                                                                            | [`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct) Parameters specific to each data source. For more information see the bq tab in the 'Setting up a data transfer' section for each data source. For example the parameters for Cloud Storage transfers are listed here: <https://cloud.google.com/bigquery-transfer/docs/cloud-storage-transfer#bq>                                                                                                                                                                                                                                                                           |
| `schedule`                                                                                                          | `string` Data transfer schedule. If the data source does not support a custom schedule, this should be empty. If it is empty, the default value for the data source will be used. The specified times are in UTC. Examples of valid format: `1st,3rd monday of month 15:30` , `every wed,fri of jan,jun 13:15` , and `first sunday of quarter 00:00` . See more explanation about the format here: <https://cloud.google.com/appengine/docs/flexible/python/scheduling-jobs-with-cron-yaml#the_schedule_format> NOTE: The minimum interval time between recurring transfers depends on the data source; refer to the documentation for your data source. |
| `schedule_options`                                                                                                  | [`ScheduleOptions`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.ScheduleOptions) Options customizing the data transfer schedule.                                                                                                                                                                                                                                                                                                                                                                                                                  |
| `schedule_options_v2`                                                                                               | [`ScheduleOptionsV2`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.ScheduleOptionsV2) Options customizing different types of data transfer schedule. This field replaces "schedule" and "schedule_options" fields. ScheduleOptionsV2 cannot be used together with ScheduleOptions/Schedule.                                                                                                                                                                                                                                                        |
| `data_refresh_window_days`                                                                                          | `int32` The number of days to look back to automatically refresh the data. For example, if `data_refresh_window_days = 10` , then every day BigQuery reingests data for \[today-10, today-1\], rather than ingesting data for just \[today-1\]. Only valid if the data source supports the feature. Set the value to 0 to use the default value.                                                                                                                                                                                                                                                                                                         |
| `disabled`                                                                                                          | `bool` Is this config disabled. When set to true, no runs will be scheduled for this transfer config.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `update_time`                                                                                                       | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Output only. Data transfer modification time. Ignored by server on input.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `next_run_time`                                                                                                     | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Output only. Next time when data transfer will run.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `state`                                                                                                             | [`TransferState`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.TransferState) Output only. State of the most recently updated transfer run.                                                                                                                                                                                                                                                                                                                                                                                                        |
| `user_id`                                                                                                           | `int64` Deprecated. Unique ID of the user on whose behalf transfer is done.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `dataset_region`                                                                                                    | `string` Output only. Region in which BigQuery dataset is located.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `notification_pubsub_topic`                                                                                         | `string` Pub/Sub topic where notifications will be sent after transfer runs associated with this transfer config finish. The format for specifying a pubsub topic is: `projects/{project_id}/topics/{topic_id}`                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `email_preferences`                                                                                                 | [`EmailPreferences`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.EmailPreferences) Email notifications will be sent according to these preferences to the email address of the user who owns this transfer config.                                                                                                                                                                                                                                                                                                                                |
| `encryption_configuration`                                                                                          | [`EncryptionConfiguration`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.EncryptionConfiguration) The encryption configuration part. Currently, it is only used for the optional KMS key name. The BigQuery service account of your project must be granted permissions to use the key. Read methods will return the key name applied in effect. Write methods will apply the key if it is present, or otherwise try to apply project default keys if it is absent.                                                                                |
| `error`                                                                                                             | [`Status`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.rpc#google.rpc.Status) Output only. Error code with detailed information about reason of the latest config failure.                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `managed_table_type`                                                                                                | [`ManagedTableType`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.ManagedTableType) The classification of the destination table.                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `metadata_destination`                                                                                              | [`MetadataDestination`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.MetadataDestination) The metadata destination of the transfer config.                                                                                                                                                                                                                                                                                                                                                                                                         |
| `param_config`                                                                                                      | [`ParameterConfig`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.TransferConfig.ParameterConfig) Optional. The config for values in `params` .                                                                                                                                                                                                                                                                                                                                                                                                     |
| Union field `destination` . The destination of the transfer config. `destination` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `destination_dataset_id`                                                                                            | `string` The BigQuery target dataset id.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `owner_info`                                                                                                        | [`UserInfo`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.UserInfo) Output only. Information about the user whose credentials are used to transfer data. Populated only for `transferConfigs.get` requests. In case the user information is not available, this field will not be populated.                                                                                                                                                                                                                                                       |

## ParameterConfig

Configuration for data source parameters.

| Fields                            |                                                                                                                                                                                                                                                                                           |
|-----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `secret_manager_managed_params[]` | `string` Optional. The list of parameters that are stored in Secret Manager. The value of a parameter included in this list will be interpreted as a Secret Manager key version resource name instead of a raw value. The raw value will be retrieved from Secret Manager upon execution. |

## TransferMessage

Represents a user facing message for a particular data transfer run.

| Fields         |                                                                                                                                                                                                                           |
|----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `message_time` | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Time when message was logged.                                                                                                           |
| `severity`     | [`MessageSeverity`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.TransferMessage.MessageSeverity) Message severity. |
| `message_text` | `string` Message text.                                                                                                                                                                                                    |

## MessageSeverity

Represents data transfer user facing message severity.

| Enums                          |                        |
|--------------------------------|------------------------|
| `MESSAGE_SEVERITY_UNSPECIFIED` | No severity specified. |
| `INFO`                         | Informational message. |
| `WARNING`                      | Warning message.       |
| `ERROR`                        | Error message.         |

## TransferResource

Resource (table/partition) that is being transferred.

| Fields                 |                                                                                                                                                                                                                                                                |
|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                 | `string` Identifier. Resource name.                                                                                                                                                                                                                            |
| `type`                 | [`ResourceType`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.ResourceType) Optional. Resource type.                                                     |
| `destination`          | [`ResourceDestination`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.ResourceDestination) Optional. Resource destination.                                |
| `latest_run`           | [`TransferRunBrief`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.TransferRunBrief) Optional. Run details for the latest run.                            |
| `latest_status_detail` | [`TransferResourceStatusDetail`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.TransferResourceStatusDetail) Optional. Status details for the latest run. |
| `last_successful_run`  | [`TransferRunBrief`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.TransferRunBrief) Output only. Run details for the last successful run.                |
| `hierarchy_detail`     | [`HierarchyDetail`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.HierarchyDetail) Optional. Details about the hierarchy.                                 |
| `update_time`          | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Output only. Time when the resource was last updated.                                                                                                                        |

## TransferResourceStatusDetail

Status details of the resource being transferred.

| Fields                 |                                                                                                                                                                                                                                                        |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `state`                | [`ResourceTransferState`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.ResourceTransferState) Optional. Transfer state of the resource.          |
| `summary`              | [`TransferStatusSummary`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.TransferStatusSummary) Optional. Transfer status summary of the resource. |
| `error`                | [`Status`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.rpc#google.rpc.Status) Optional. Transfer error details for the resource.                                                                                     |
| `completed_percentage` | `double` Output only. Percentage of the transfer completed. Valid values: 0-100.                                                                                                                                                                       |

## TransferRun

Represents a data transfer run.

| Fields                                                                                                 |                                                                                                                                                                                                                                                                                                                                                                                             |
|--------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                                                                                                 | `string` Identifier. The resource name of the transfer run. Transfer run names have the form `projects/{project_id}/locations/{location}/transferConfigs/{config_id}/runs/{run_id}` . The name is ignored when creating a transfer run.                                                                                                                                                     |
| `schedule_time`                                                                                        | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Minimum time after which a transfer run can be started.                                                                                                                                                                                                                                                   |
| `run_time`                                                                                             | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) For batch transfer runs, specifies the date and time of the data should be ingested.                                                                                                                                                                                                                      |
| `error_status`                                                                                         | [`Status`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.rpc#google.rpc.Status) Status of the transfer run.                                                                                                                                                                                                                                                 |
| `start_time`                                                                                           | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Output only. Time when transfer run was started. Parameter ignored by server for input requests.                                                                                                                                                                                                          |
| `end_time`                                                                                             | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Output only. Time when transfer run ended. Parameter ignored by server for input requests.                                                                                                                                                                                                                |
| `update_time`                                                                                          | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Output only. Last time the data transfer run state was updated.                                                                                                                                                                                                                                           |
| `params`                                                                                               | [`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct) Output only. Parameters specific to each data source. For more information see the bq tab in the 'Setting up a data transfer' section for each data source. For example the parameters for Cloud Storage transfers are listed here: <https://cloud.google.com/bigquery-transfer/docs/cloud-storage-transfer#bq> |
| `data_source_id`                                                                                       | `string` Output only. Data source id.                                                                                                                                                                                                                                                                                                                                                       |
| `state`                                                                                                | [`TransferState`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.TransferState) Data transfer run state. Ignored for input requests.                                                                                                                                                    |
| `user_id`                                                                                              | `int64` Deprecated. Unique ID of the user on whose behalf transfer is done.                                                                                                                                                                                                                                                                                                                 |
| `schedule`                                                                                             | `string` Output only. Describes the schedule of this transfer run if it was created as part of a regular schedule. For batch transfer runs that are scheduled manually, this is empty. NOTE: the system might choose to delay the schedule depending on the current load, so `schedule_time` doesn't always match this.                                                                     |
| `notification_pubsub_topic`                                                                            | `string` Output only. Pub/Sub topic where a notification will be sent after this transfer run finishes. The format for specifying a pubsub topic is: `projects/{project_id}/topics/{topic_id}`                                                                                                                                                                                              |
| `email_preferences`                                                                                    | [`EmailPreferences`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.EmailPreferences) Output only. Email notifications will be sent according to these preferences to the email address of the user who owns the transfer config this run was derived from.                             |
| `parameter_config`                                                                                     | [`ParameterConfig`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.TransferConfig.ParameterConfig) Output only. The parameter config of the transfer run.                                                                                                                               |
| Union field `destination` . Data transfer destination. `destination` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                             |
| `destination_dataset_id`                                                                               | `string` Output only. The BigQuery target dataset id.                                                                                                                                                                                                                                                                                                                                       |

## TransferRunBrief

Basic information about a transfer run.

| Fields       |                                                                                                                                       |
|--------------|---------------------------------------------------------------------------------------------------------------------------------------|
| `run`        | `string` Optional. Run URI. The format must be: `projects/{project}/locations/{location}/transferConfigs/{transfer_config}/run/{run}` |
| `start_time` | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Optional. Start time of the transfer run.           |

## TransferState

Represents data transfer run state.

| Enums                        |                                                                                         |
|------------------------------|-----------------------------------------------------------------------------------------|
| `TRANSFER_STATE_UNSPECIFIED` | State placeholder (0).                                                                  |
| `PENDING`                    | Data transfer is scheduled and is waiting to be picked up by data transfer backend (2). |
| `RUNNING`                    | Data transfer is in progress (3).                                                       |
| `SUCCEEDED`                  | Data transfer completed successfully (4).                                               |
| `FAILED`                     | Data transfer failed (5).                                                               |
| `CANCELLED`                  | Data transfer is cancelled (6).                                                         |

## TransferStatusMetric

Metrics for tracking the transfer status.

| Fields      |                                                                                                                                                                                                                                                    |
|-------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `completed` | `int64` Optional. Number of units transferred successfully.                                                                                                                                                                                        |
| `pending`   | `int64` Optional. Number of units pending transfer.                                                                                                                                                                                                |
| `failed`    | `int64` Optional. Number of units that failed to transfer.                                                                                                                                                                                         |
| `total`     | `int64` Optional. Total number of units for the transfer.                                                                                                                                                                                          |
| `unit`      | [`TransferStatusUnit`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.TransferStatusUnit) Optional. Unit for measuring progress (e.g., BYTES). |

## TransferStatusSummary

Status summary of the resource being transferred.

| Fields          |                                                                                                                                                                                                                                                                              |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `metrics[]`     | [`TransferStatusMetric`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.TransferStatusMetric) Optional. List of transfer status metrics.                                 |
| `progress_unit` | [`TransferStatusUnit`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.TransferStatusUnit) Input only. Unit based on which transfer status progress should be calculated. |

## TransferStatusUnit

Unit of the transfer status.

| Enums                              |                |
|------------------------------------|----------------|
| `TRANSFER_STATUS_UNIT_UNSPECIFIED` | Default value. |
| `TRANSFER_STATUS_UNIT_BYTES`       | Bytes.         |
| `TRANSFER_STATUS_UNIT_OBJECTS`     | Objects.       |

## TransferType

> This item is deprecated!

DEPRECATED. Represents data transfer type.

| Enums                       |                                                                                                                 |
|-----------------------------|-----------------------------------------------------------------------------------------------------------------|
| `TRANSFER_TYPE_UNSPECIFIED` | Invalid or Unknown transfer type placeholder.                                                                   |
| `BATCH`                     | Batch data transfer.                                                                                            |
| `STREAMING`                 | Streaming data transfer. Streaming data source currently doesn't support multiple transfer configs per project. |

## UnenrollDataSourcesRequest

A request to unenroll a set of data sources so they are no longer visible in the BigQuery UI's `Transfer` tab.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. The name of the project resource in the form: <code>projects/{project_id}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>resourcemanager.projects.update</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>data_source_ids[]</code></td>
<td><p><code>string</code></p>
<p>Data sources that are unenrolled. It is required to provide at least one data source id.</p></td>
</tr>
</tbody>
</table>

## UpdateTransferConfigRequest

A request to update a transfer configuration. To update the user id of the transfer configuration, authorization info needs to be provided.

When using a cross project service account for updating a transfer config, you must enable cross project service account usage. For more information, see [Disable attachment of service accounts to resources in other projects](https://cloud.google.com/resource-manager/docs/organization-policy/restricting-service-accounts#disable_cross_project_service_accounts) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>transfer_config</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rpc/google.cloud.bigquery.datatransfer.v1#google.cloud.bigquery.datatransfer.v1.TransferConfig"><code>TransferConfig</code></a></p>
<p>Required. Data transfer configuration to create.</p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>transferConfig</code> :</p>
<ul>
<li><code>bigquery.transfers.update</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>authorization_code </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>string</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Deprecated: Authorization code was required when <code>transferConfig.dataSourceId</code> is 'youtube_channel' but it is no longer used in any data sources. Use <code>version_info</code> instead.</p>
<p>Optional OAuth2 authorization code to use with this transfer configuration. This is required only if <code>transferConfig.dataSourceId</code> is 'youtube_channel' and new credentials are needed, as indicated by <code>CheckValidCreds</code> . In order to obtain authorization_code, make a request to the following URL:</p>
<pre data-fenced=""><code>https://bigquery.cloud.google.com/datatransfer/oauthz/auth?redirect_uri=urn:ietf:wg:oauth:2.0:oob&amp;response_type=authorization_code&amp;client_id=client_id&amp;scope=data_source_scopes</code></pre>
<ul>
<li>The <var translate="no"> client_id </var> is the OAuth client_id of the data source as returned by ListDataSources method.</li>
<li><var translate="no"> data_source_scopes </var> are the scopes returned by ListDataSources method.</li>
</ul>
<p>Note that this should not be set when <code>service_account_name</code> is used to update the transfer config.</p></td>
</tr>
<tr class="odd">
<td><code>update_mask</code></td>
<td><p><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#field-mask"><code>FieldMask</code></a></p>
<p>Required. Required list of fields to be updated in this request.</p></td>
</tr>
<tr class="even">
<td><code>version_info</code></td>
<td><p><code>string</code></p>
<p>Optional version info. This parameter replaces <code>authorization_code</code> which is no longer used in any data sources. This is required only if <code>transferConfig.dataSourceId</code> is 'youtube_channel' <em>or</em> new credentials are needed, as indicated by <code>CheckValidCreds</code> . In order to obtain version info, make a request to the following URL:</p>
<pre data-fenced=""><code>https://bigquery.cloud.google.com/datatransfer/oauthz/auth?redirect_uri=urn:ietf:wg:oauth:2.0:oob&amp;response_type=version_info&amp;client_id=client_id&amp;scope=data_source_scopes</code></pre>
<ul>
<li>The <var translate="no"> client_id </var> is the OAuth client_id of the data source as returned by ListDataSources method.</li>
<li><var translate="no"> data_source_scopes </var> are the scopes returned by ListDataSources method.</li>
</ul>
<p>Note that this should not be set when <code>service_account_name</code> is used to update the transfer config.</p></td>
</tr>
<tr class="odd">
<td><code>service_account_name</code></td>
<td><p><code>string</code></p>
<p>Optional service account email. If this field is set, the transfer config will be created with this service account's credentials. It requires that the requesting user calling this API has permissions to act as this service account.</p>
<p>Note that not all data sources support service account credentials when creating a transfer config. For the latest list of data sources, read about <a href="https://cloud.google.com/bigquery-transfer/docs/use-service-accounts">using service accounts</a> .</p></td>
</tr>
</tbody>
</table>

## UserInfo

Information about a user.

| Fields  |                                      |
|---------|--------------------------------------|
| `email` | `string` E-mail address of the user. |
