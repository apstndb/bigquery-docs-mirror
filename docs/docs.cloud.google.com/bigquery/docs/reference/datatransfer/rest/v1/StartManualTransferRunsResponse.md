  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/StartManualTransferRunsResponse#SCHEMA_REPRESENTATION)

A response to start manual transfer runs.

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

The transfer runs that were created.
