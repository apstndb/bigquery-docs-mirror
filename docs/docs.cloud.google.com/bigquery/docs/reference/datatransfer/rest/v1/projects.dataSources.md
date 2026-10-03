---
name: documents/docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.dataSources
uri: https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.dataSources
title: 'REST Resource: projects.dataSources'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [Resource: DataSource](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.dataSources#DataSource)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.dataSources#DataSource.SCHEMA_REPRESENTATION)
  - [TransferType](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.dataSources#DataSource.TransferType)
  - [DataSourceParameter](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.dataSources#DataSource.DataSourceParameter)
    - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.dataSources#DataSource.DataSourceParameter.SCHEMA_REPRESENTATION)
  - [Type](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.dataSources#DataSource.Type)
  - [AuthorizationType](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.dataSources#DataSource.AuthorizationType)
  - [DataRefreshType](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.dataSources#DataSource.DataRefreshType)
- [Methods](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.dataSources#METHODS_SUMMARY)

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

### TransferType

> This item is deprecated!

DEPRECATED. Represents data transfer type.

| Enums                       |                                                                                                                 |
|-----------------------------|-----------------------------------------------------------------------------------------------------------------|
| `TRANSFER_TYPE_UNSPECIFIED` | Invalid or Unknown transfer type placeholder.                                                                   |
| `BATCH`                     | Batch data transfer.                                                                                            |
| `STREAMING`                 | Streaming data transfer. Streaming data source currently doesn't support multiple transfer configs per project. |

### DataSourceParameter

A parameter used to define custom fields in a data source definition.

**JSON representation**

```
{
  "paramId": string,
  "displayName": string,
  "description": string,
  "type": enum (Type),
  "required": boolean,
  "repeated": boolean,
  "validationRegex": string,
  "allowedValues": [
    string
  ],
  "minValue": number,
  "maxValue": number,
  "fields": [
    {
      object (DataSourceParameter)
    }
  ],
  "validationDescription": string,
  "validationHelpUrl": string,
  "immutable": boolean,
  "recurse": boolean,
  "deprecated": boolean,
  "secretManagerAllowed": boolean,
  "maxListSize": string
}
```

| Fields                  |                                                                                                                                                                                                              |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `paramId`               | `string` Parameter identifier.                                                                                                                                                                               |
| `displayName`           | `string` Parameter display name in the user interface.                                                                                                                                                       |
| `description`           | `string` Parameter description.                                                                                                                                                                              |
| `type`                  | `enum ( `[`Type`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.dataSources#DataSource.Type)` )` Parameter type.                                                       |
| `required`              | `boolean` Is parameter required.                                                                                                                                                                             |
| `repeated`              | `boolean` Deprecated. This field has no effect.                                                                                                                                                              |
| `validationRegex`       | `string` Regular expression which can be used for parameter validation.                                                                                                                                      |
| `allowedValues[]`       | `string` All possible values for the parameter.                                                                                                                                                              |
| `minValue`              | `number` For integer and double values specifies minimum allowed value.                                                                                                                                      |
| `maxValue`              | `number` For integer and double values specifies maximum allowed value.                                                                                                                                      |
| `fields[]`              | `object ( `[`DataSourceParameter`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.dataSources#DataSource.DataSourceParameter)` )` Deprecated. This field has no effect. |
| `validationDescription` | `string` Description of the requirements for this field, in case the user input does not fulfill the regex pattern or min/max values.                                                                        |
| `validationHelpUrl`     | `string` URL to a help document to further explain the naming requirements.                                                                                                                                  |
| `immutable`             | `boolean` Cannot be changed after initial creation.                                                                                                                                                          |
| `recurse`               | `boolean` Deprecated. This field has no effect.                                                                                                                                                              |
| `deprecated`            | `boolean` If true, it should not be used in new transfers, and it should not be visible to users.                                                                                                            |
| `secretManagerAllowed`  | `boolean` Output only. If true, the parameter value can be provided through Secret Manager.                                                                                                                  |
| `maxListSize`           | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` For list parameters, the max size of the list.                                                                        |

### Type

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

### AuthorizationType

The type of authorization needed for this data source.

| Enums                            |                                                                                                                      |
|----------------------------------|----------------------------------------------------------------------------------------------------------------------|
| `AUTHORIZATION_TYPE_UNSPECIFIED` | Type unspecified.                                                                                                    |
| `AUTHORIZATION_CODE`             | Use OAuth 2 authorization codes that can be exchanged for a refresh token on the backend.                            |
| `GOOGLE_PLUS_AUTHORIZATION_CODE` | Return an authorization code for a given Google+ page that can then be exchanged for a refresh token on the backend. |
| `FIRST_PARTY_OAUTH`              | Use First Party OAuth.                                                                                               |

### DataRefreshType

Represents how the data source supports data auto refresh.

| Enums                           |                                                                                                                                                                |
|---------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `DATA_REFRESH_TYPE_UNSPECIFIED` | The data source won't support data auto refresh, which is default value.                                                                                       |
| `SLIDING_WINDOW`                | The data source supports data auto refresh, and runs will be scheduled for the past few days. Does not allow custom values to be set for each transfer config. |
| `CUSTOM_SLIDING_WINDOW`         | The data source supports data auto refresh, and runs will be scheduled for the past few days. Allows custom values to be set for each transfer config.         |

| Methods                                                                                                                              |                                                                                        |
|--------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------|
| [`checkValidCreds`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.dataSources/checkValidCreds) | Returns true if valid credentials exist for the given data source and requesting user. |
| [`get`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.dataSources/get)                         | Retrieves a supported data source and returns its settings.                            |
| [`list`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.dataSources/list)                       | Lists supported data sources and returns their settings.                               |
