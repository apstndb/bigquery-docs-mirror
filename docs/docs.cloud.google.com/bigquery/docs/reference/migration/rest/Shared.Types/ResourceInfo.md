  - [JSON representation](#SCHEMA_REPRESENTATION)

Describes the resource that is being accessed.

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
  &quot;resourceType&quot;: string,
  &quot;resourceName&quot;: string,
  &quot;owner&quot;: string,
  &quot;description&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  resourceType  `

`  string  `

A name for the type of resource being accessed, e.g. "sql table", "cloud storage bucket", "file", "Google calendar"; or the type URL of the resource: e.g. "type.googleapis.com/google.pubsub.v1.Topic".

`  resourceName  `

`  string  `

The name of the resource being accessed. For example, a shared calendar name: "example.com [\_4fghdhgsrgh@group.calendar.google.com"](mailto:_4fghdhgsrgh@group.calendar.google.com%22) , if the current error is `  google.rpc.Code.PERMISSION_DENIED  ` .

`  owner  `

`  string  `

The owner of the resource (optional). For example, "user: " or "project: ".

`  description  `

`  string  `

Describes what error is encountered when accessing this resource. For example, updating a cloud project may require the `  writer  ` permission on the developer console project.
