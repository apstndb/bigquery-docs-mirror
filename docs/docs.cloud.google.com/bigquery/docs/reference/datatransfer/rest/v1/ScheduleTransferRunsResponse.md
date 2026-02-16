  - [JSON representation](#SCHEMA_REPRESENTATION)

A response to schedule transfer runs for a time range.

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
  &quot;runs&quot;: [
    {
      object (TransferRun)
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  runs[]  `

`  object ( TransferRun  ` )

The transfer runs that were scheduled.
