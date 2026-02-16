  - [JSON representation](#SCHEMA_REPRESENTATION)

Message for response to the listing of shared resource subscriptions.

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
  &quot;sharedResourceSubscriptions&quot;: [
    {
      object (Subscription)
    }
  ],
  &quot;nextPageToken&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  sharedResourceSubscriptions[]  `

`  object ( Subscription  ` )

The list of subscriptions.

`  nextPageToken  `

`  string  `

Next page token.
