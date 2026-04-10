  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/ListDataSourcesResponse#SCHEMA_REPRESENTATION)

Returns list of supported data sources and their metadata.

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
  &quot;dataSources&quot;: [
    {
      object (DataSource)
    }
  ],
  &quot;nextPageToken&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  dataSources[]  `

`  object ( DataSource  ` )

List of supported data sources and their transfer settings.

`  nextPageToken  `

`  string  `

Output only. The next-pagination token. For multiple-page list results, this token can be used as the `  ListDataSourcesRequest.page_token  ` to request the next page of list results.
