---
name: documents/docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.dataSources
uri: https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.dataSources
title: 'REST Resource: projects.locations.dataSources'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [Resource: DataSource](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.dataSources#DataSource)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.dataSources#DataSource.SCHEMA_REPRESENTATION)
- [Methods](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.dataSources#METHODS_SUMMARY)

## Resource: DataSource

Defines the properties and custom parameters for a data source.

**JSON representation**

```
{
  "name": string,
  "dataSourceId": string,
  "displayName": string,
  "description": string,
  "clientId": string,
  "scopes": [
    string
  ],
  "transferType": enum (TransferType),
  "supportsMultipleTransfers": boolean,
  "updateDeadlineSeconds": integer,
  "defaultSchedule": string,
  "supportsCustomSchedule": boolean,
  "parameters": [
    {
      object (DataSourceParameter)
    }
  ],
  "helpUrl": string,
  "authorizationType": enum (AuthorizationType),
  "dataRefreshType": enum (DataRefreshType),
  "defaultDataRefreshWindowDays": integer,
  "manualRunsDisabled": boolean,
  "minimumScheduleInterval": string
}
```

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
<td><code>dataSourceId</code></td>
<td><p><code>string</code></p>
<p>Data source id.</p></td>
</tr>
<tr class="odd">
<td><code>displayName</code></td>
<td><p><code>string</code></p>
<p>User friendly data source name.</p></td>
</tr>
<tr class="even">
<td><code>description</code></td>
<td><p><code>string</code></p>
<p>User friendly data source description string.</p></td>
</tr>
<tr class="odd">
<td><code>clientId</code></td>
<td><p><code>string</code></p>
<p>Data source client id which should be used to receive refresh token.</p></td>
</tr>
<tr class="even">
<td><code>scopes[]</code></td>
<td><p><code>string</code></p>
<p>Api auth scopes for which refresh token needs to be obtained. These are scopes needed by a data source to prepare data and ingest them into BigQuery, e.g., <a href="https://www.googleapis.com/auth/bigquery">https://www.googleapis.com/auth/bigquery</a></p></td>
</tr>
<tr class="odd">
<td><code>transferType </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.dataSources#DataSource.TransferType"><code>TransferType</code></a><code> )</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Deprecated. This field has no effect.</p></td>
</tr>
<tr class="even">
<td><code>supportsMultipleTransfers </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>boolean</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Deprecated. This field has no effect.</p></td>
</tr>
<tr class="odd">
<td><code>updateDeadlineSeconds</code></td>
<td><p><code>integer</code></p>
<p>The number of seconds to wait for an update from the data source before the Data Transfer Service marks the transfer as FAILED.</p></td>
</tr>
<tr class="even">
<td><code>defaultSchedule</code></td>
<td><p><code>string</code></p>
<p>Default data transfer schedule. Examples of valid schedules include: <code>1st,3rd monday of month 15:30</code> , <code>every wed,fri of jan,jun 13:15</code> , and <code>first sunday of quarter 00:00</code> .</p></td>
</tr>
<tr class="odd">
<td><code>supportsCustomSchedule</code></td>
<td><p><code>boolean</code></p>
<p>Specifies whether the data source supports a user defined schedule, or operates on the default schedule. When set to <code>true</code> , user can override default schedule.</p></td>
</tr>
<tr class="even">
<td><code>parameters[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.dataSources#DataSource.DataSourceParameter"><code>DataSourceParameter</code></a><code> )</code></p>
<p>Data source parameters.</p></td>
</tr>
<tr class="odd">
<td><code>helpUrl</code></td>
<td><p><code>string</code></p>
<p>Url for the help document for this data source.</p></td>
</tr>
<tr class="even">
<td><code>authorizationType</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.dataSources#DataSource.AuthorizationType"><code>AuthorizationType</code></a><code> )</code></p>
<p>Indicates the type of authorization.</p></td>
</tr>
<tr class="odd">
<td><code>dataRefreshType</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.dataSources#DataSource.DataRefreshType"><code>DataRefreshType</code></a><code> )</code></p>
<p>Specifies whether the data source supports automatic data refresh for the past few days, and how it's supported. For some data sources, data might not be complete until a few days later, so it's useful to refresh data automatically.</p></td>
</tr>
<tr class="even">
<td><code>defaultDataRefreshWindowDays</code></td>
<td><p><code>integer</code></p>
<p>Default data refresh window on days. Only meaningful when <code>dataRefreshType</code> = <code>SLIDING_WINDOW</code> .</p></td>
</tr>
<tr class="odd">
<td><code>manualRunsDisabled</code></td>
<td><p><code>boolean</code></p>
<p>Disables backfilling and manual run scheduling for the data source.</p></td>
</tr>
<tr class="even">
<td><code>minimumScheduleInterval</code></td>
<td><p><code>string ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#duration"><code>Duration</code></a><code> format)</code></p>
<p>The minimum interval for scheduler to schedule runs.</p>
<p>A duration in seconds with up to nine fractional digits, ending with ' <code>s</code> '. Example: <code>"3.5s"</code> .</p></td>
</tr>
</tbody>
</table>

| Methods                                                                                                                                        |                                                                                        |
|------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------|
| [`checkValidCreds`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.dataSources/checkValidCreds) | Returns true if valid credentials exist for the given data source and requesting user. |
| [`get`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.dataSources/get)                         | Retrieves a supported data source and returns its settings.                            |
| [`list`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.dataSources/list)                       | Lists supported data sources and returns their settings.                               |
