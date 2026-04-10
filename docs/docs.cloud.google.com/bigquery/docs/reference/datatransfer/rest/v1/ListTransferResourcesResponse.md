  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/ListTransferResourcesResponse#SCHEMA_REPRESENTATION)

Response for the `  transferResources.list  ` RPC.

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
  &quot;transferResources&quot;: [
    {
      object (TransferResource)
    }
  ],
  &quot;nextPageToken&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  transferResources[]  `

`  object ( TransferResource  ` )

Output only. The transfer resources.

`  nextPageToken  `

`  string  `

Output only. A token, which can be sent as `  pageToken  ` to retrieve the next page. If this field is omitted, there are no subsequent pages.
