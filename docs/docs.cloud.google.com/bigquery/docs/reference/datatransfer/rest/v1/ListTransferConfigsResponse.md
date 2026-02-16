  - [JSON representation](#SCHEMA_REPRESENTATION)

The returned list of pipelines in the project.

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
  &quot;transferConfigs&quot;: [
    {
      object (TransferConfig)
    }
  ],
  &quot;nextPageToken&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  transferConfigs[]  `

`  object ( TransferConfig  ` )

Output only. The stored pipeline transfer configurations.

`  nextPageToken  `

`  string  `

Output only. The next-pagination token. For multiple-page list results, this token can be used as the `  ListTransferConfigsRequest.page_token  ` to request the next page of list results.
