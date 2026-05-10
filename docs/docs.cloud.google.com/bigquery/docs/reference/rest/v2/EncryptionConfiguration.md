---
name: documents/docs.cloud.google.com/bigquery/docs/reference/rest/v2/EncryptionConfiguration
uri: https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/EncryptionConfiguration
title: EncryptionConfiguration
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
update_time: "2025-10-17T21:04:20Z"
---

  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/EncryptionConfiguration#SCHEMA_REPRESENTATION)

Configuration for Cloud KMS encryption settings.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;kmsKeyName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`kmsKeyName`

`string`

Optional. Describes the Cloud KMS encryption key that will be used to protect destination BigQuery table. The BigQuery Service Account associated with your project requires access to this encryption key.
