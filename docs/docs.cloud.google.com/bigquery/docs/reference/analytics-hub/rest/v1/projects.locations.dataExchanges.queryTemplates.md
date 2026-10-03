---
name: documents/docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.queryTemplates
uri: https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.queryTemplates
title: 'REST Resource: projects.locations.dataExchanges.queryTemplates'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [Resource: QueryTemplate](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.queryTemplates#QueryTemplate)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.queryTemplates#QueryTemplate.SCHEMA_REPRESENTATION)
- [State](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.queryTemplates#State)
- [Routine](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.queryTemplates#Routine)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.queryTemplates#Routine.SCHEMA_REPRESENTATION)
- [RoutineType](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.queryTemplates#RoutineType)
- [EncryptionConfig](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.queryTemplates#EncryptionConfig)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.queryTemplates#EncryptionConfig.SCHEMA_REPRESENTATION)
- [Methods](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.queryTemplates#METHODS_SUMMARY)

## Resource: QueryTemplate

A query template is a container for sharing table-valued functions defined by contributors in a data clean room.

**JSON representation**

```
{
  "name": string,
  "displayName": string,
  "description": string,
  "proposer": string,
  "primaryContact": string,
  "documentation": string,
  "state": enum (State),
  "routine": {
    object (Routine)
  },
  "createTime": string,
  "updateTime": string,
  "encryptionConfiguration": {
    object (EncryptionConfig)
  }
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
<p>Output only. The resource name of the QueryTemplate. e.g. <code>projects/myproject/locations/us/dataExchanges/123/queryTemplates/456</code></p></td>
</tr>
<tr class="even">
<td><code>displayName</code></td>
<td><p><code>string</code></p>
<p>Required. Human-readable display name of the QueryTemplate. The display name must contain only Unicode letters, numbers (0-9), underscores (_), dashes (-), spaces ( ), ampersands (&amp;) and can't start or end with spaces. Default value is an empty string. Max length: 63 bytes.</p></td>
</tr>
<tr class="odd">
<td><code>description</code></td>
<td><p><code>string</code></p>
<p>Optional. Short description of the QueryTemplate. The description must not contain Unicode non-characters and C0 and C1 control codes except tabs (HT), new lines (LF), carriage returns (CR), and page breaks (FF). Default value is an empty string. Max length: 2000 bytes.</p></td>
</tr>
<tr class="even">
<td><code>proposer </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>string</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Optional. Deprecated: Use <code>primaryContact</code> instead. Email or URL of the primary point of contact of the QueryTemplate. Max Length: 1000 bytes.</p></td>
</tr>
<tr class="odd">
<td><code>primaryContact</code></td>
<td><p><code>string</code></p>
<p>Optional. Email or URL of the primary point of contact of the QueryTemplate. Max Length: 1000 bytes.</p></td>
</tr>
<tr class="even">
<td><code>documentation</code></td>
<td><p><code>string</code></p>
<p>Optional. Documentation describing the QueryTemplate.</p></td>
</tr>
<tr class="odd">
<td><code>state</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.queryTemplates#State"><code>State</code></a><code> )</code></p>
<p>Output only. The QueryTemplate lifecycle state.</p></td>
</tr>
<tr class="even">
<td><code>routine</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.queryTemplates#Routine"><code>Routine</code></a><code> )</code></p>
<p>Optional. The routine associated with the QueryTemplate.</p></td>
</tr>
<tr class="odd">
<td><code>createTime</code></td>
<td><p><code>string ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp"><code>Timestamp</code></a><code> format)</code></p>
<p>Output only. Timestamp when the QueryTemplate was created.</p>
<p>Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: <code>"2014-10-02T15:01:23Z"</code> , <code>"2014-10-02T15:01:23.045123456Z"</code> or <code>"2014-10-02T15:01:23+05:30"</code> .</p></td>
</tr>
<tr class="even">
<td><code>updateTime</code></td>
<td><p><code>string ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp"><code>Timestamp</code></a><code> format)</code></p>
<p>Output only. Timestamp when the QueryTemplate was last modified.</p>
<p>Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: <code>"2014-10-02T15:01:23Z"</code> , <code>"2014-10-02T15:01:23.045123456Z"</code> or <code>"2014-10-02T15:01:23+05:30"</code> .</p></td>
</tr>
<tr class="odd">
<td><code>encryptionConfiguration</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.queryTemplates#EncryptionConfig"><code>EncryptionConfig</code></a><code> )</code></p>
<p>Optional. Encryption configuration for the query template. If set, the customer-managed KMS key is used to encrypt the query template definition body.</p></td>
</tr>
</tbody>
</table>

## State

The QueryTemplate lifecycle state.

| Enums               |                                         |
|---------------------|-----------------------------------------|
| `STATE_UNSPECIFIED` | Default value. This value is unused.    |
| `DRAFTED`           | The QueryTemplate is in draft state.    |
| `PENDING`           | The QueryTemplate is in pending state.  |
| `DELETED`           | The QueryTemplate is in deleted state.  |
| `APPROVED`          | The QueryTemplate is in approved state. |

## Routine

Represents a bigquery routine.

**JSON representation**

```
{
  "routineType": enum (RoutineType),
  "definitionBody": string
}
```

| Fields           |                                                                                                                                                                                                      |
|------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `routineType`    | `enum ( `[`RoutineType`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.queryTemplates#RoutineType)` )` Required. The type of routine. |
| `definitionBody` | `string` Optional. The definition body of the routine.                                                                                                                                               |

## RoutineType

Represents the type of a given routine.

| Enums                      |                              |
|----------------------------|------------------------------|
| `ROUTINE_TYPE_UNSPECIFIED` | Default value.               |
| `TABLE_VALUED_FUNCTION`    | Non-built-in persistent TVF. |

## EncryptionConfig

Encryption configuration for the query template.

**JSON representation**

```
{
  "kmsKeyName": string
}
```

| Fields       |                                                                                                                                                          |
|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| `kmsKeyName` | `string` Optional. The KMS key used to encrypt the query template. Format: `projects/{project}/locations/{location}/keyRings/{keyring}/cryptoKeys/{key}` |

| Methods                                                                                                                                          |                                                           |
|--------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------|
| [`approve`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.queryTemplates/approve) | Approves a query template.                                |
| [`create`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.queryTemplates/create)   | Creates a new QueryTemplate                               |
| [`delete`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.queryTemplates/delete)   | Deletes a query template.                                 |
| [`get`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.queryTemplates/get)         | Gets a QueryTemplate                                      |
| [`list`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.queryTemplates/list)       | Lists all QueryTemplates in a given project and location. |
| [`patch`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.queryTemplates/patch)     | Updates an existing QueryTemplate                         |
| [`submit`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.queryTemplates/submit)   | Submits a query template for approval.                    |
