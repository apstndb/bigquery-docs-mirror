---
name: documents/docs.cloud.google.com/bigquery/docs/reference/rest/v2/StandardSqlField
uri: https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/StandardSqlField
title: StandardSqlField
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
update_time: "2025-10-17T21:04:42Z"
---

  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/StandardSqlField#SCHEMA_REPRESENTATION)

A field or a column.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;type&quot;: {object (StandardSqlDataType)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

Optional. The name of this field. Can be absent for struct fields.

`type`

` object ( StandardSqlDataType  ` )

Optional. The type of this parameter. Absent if not explicitly specified (e.g., CREATE FUNCTION statement can omit the return type; in this case the output parameter does not have this "type" field).
