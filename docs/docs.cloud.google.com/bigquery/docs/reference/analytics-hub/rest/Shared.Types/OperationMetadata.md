  - [JSON representation](#SCHEMA_REPRESENTATION)

Represents the metadata of a long-running operation in Analytics Hub.

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
  &quot;createTime&quot;: string,
  &quot;endTime&quot;: string,
  &quot;target&quot;: string,
  &quot;verb&quot;: string,
  &quot;statusMessage&quot;: string,
  &quot;requestedCancellation&quot;: boolean,
  &quot;apiVersion&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  createTime  `

`  string ( Timestamp  ` format)

Output only. The time the operation was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

`  endTime  `

`  string ( Timestamp  ` format)

Output only. The time the operation finished running.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

`  target  `

`  string  `

Output only. Server-defined resource path for the target of the operation.

`  verb  `

`  string  `

Output only. Name of the verb executed by the operation.

`  statusMessage  `

`  string  `

Output only. Human-readable status of the operation, if any.

`  requestedCancellation  `

`  boolean  `

Output only. Identifies whether the user has requested cancellation of the operation. Operations that have successfully been cancelled have \[Operation.error\]\[\] value with a `  google.rpc.Status.code  ` of 1, corresponding to `  Code.CANCELLED  ` .

`  apiVersion  `

`  string  `

Output only. API version used to start the operation.
