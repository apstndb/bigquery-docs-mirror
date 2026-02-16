  - [JSON representation](#SCHEMA_REPRESENTATION)
  - [TableReference](#TableReference)
      - [JSON representation](#TableReference.SCHEMA_REPRESENTATION)

Represents a BI Reservation.

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
  &quot;name&quot;: string,
  &quot;updateTime&quot;: string,
  &quot;size&quot;: string,
  &quot;preferredTables&quot;: [
    {
      object (TableReference)
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  name  `

`  string  `

Identifier. The resource name of the singleton BI reservation. Reservation names have the form `  projects/{projectId}/locations/{locationId}/biReservation  ` .

`  updateTime  `

`  string ( Timestamp  ` format)

Output only. The last update timestamp of a reservation.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

`  size  `

`  string ( int64 format)  `

Optional. Size of a reservation, in bytes.

`  preferredTables[]  `

`  object ( TableReference  ` )

Optional. Preferred tables to use BI capacity for.

## TableReference

Fully qualified reference to BigQuery table. Internally stored as google.cloud.bi.v1.BqTableReference.

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
  &quot;projectId&quot;: string,
  &quot;datasetId&quot;: string,
  &quot;tableId&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  projectId  `

`  string  `

Optional. The assigned project ID of the project.

`  datasetId  `

`  string  `

Optional. The ID of the dataset in the above project.

`  tableId  `

`  string  `

Optional. The ID of the table in the above dataset.
