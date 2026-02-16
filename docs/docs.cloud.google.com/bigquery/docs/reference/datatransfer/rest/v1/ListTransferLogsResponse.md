  - [JSON representation](#SCHEMA_REPRESENTATION)

The returned list transfer run messages.

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
  &quot;transferMessages&quot;: [
    {
      object (TransferMessage)
    }
  ],
  &quot;nextPageToken&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  transferMessages[]  `

`  object ( TransferMessage  ` )

Output only. The stored pipeline transfer messages.

`  nextPageToken  `

`  string  `

Output only. The next-pagination token. For multiple-page list results, this token can be used as the `  GetTransferRunLogRequest.page_token  ` to request the next page of list results.
