  - [JSON representation](#SCHEMA_REPRESENTATION)

A specification for a time range, this will request transfer runs with runTime between startTime (inclusive) and endTime (exclusive).

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
  &quot;startTime&quot;: string,
  &quot;endTime&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  startTime  `

`  string ( Timestamp  ` format)

Start time of the range of transfer runs. For example, `  "2017-05-25T00:00:00+00:00"  ` . The startTime must be strictly less than the endTime. Creates transfer runs where runTime is in the range between startTime (inclusive) and endTime (exclusive).

`  endTime  `

`  string ( Timestamp  ` format)

End time of the range of transfer runs. For example, `  "2017-05-30T00:00:00+00:00"  ` . The endTime must not be in the future. Creates transfer runs where runTime is in the range between startTime (inclusive) and endTime (exclusive).
