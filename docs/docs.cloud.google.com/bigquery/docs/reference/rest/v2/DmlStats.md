  - [JSON representation](#SCHEMA_REPRESENTATION)

Detailed statistics for DML statements

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
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;insertedRowCount&quot;: string,
  &quot;deletedRowCount&quot;: string,
  &quot;updatedRowCount&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  insertedRowCount  `

`  string ( Int64Value format)  `

Output only. Number of inserted Rows. Populated by DML INSERT and MERGE statements

`  deletedRowCount  `

`  string ( Int64Value format)  `

Output only. Number of deleted Rows. populated by DML DELETE, MERGE and TRUNCATE statements.

`  updatedRowCount  `

`  string ( Int64Value format)  `

Output only. Number of updated Rows. Populated by DML UPDATE and MERGE statements.
