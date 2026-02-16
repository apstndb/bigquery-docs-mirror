  - [JSON representation](#SCHEMA_REPRESENTATION)
  - [ErrorDetail](#ErrorDetail)
      - [JSON representation](#ErrorDetail.SCHEMA_REPRESENTATION)
  - [ErrorLocation](#ErrorLocation)
      - [JSON representation](#ErrorLocation.SCHEMA_REPRESENTATION)

Provides details for errors and the corresponding resources.

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
  &quot;resourceInfo&quot;: {
    object (ResourceInfo)
  },
  &quot;errorDetails&quot;: [
    {
      object (ErrorDetail)
    }
  ],
  &quot;errorCount&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  resourceInfo  `

`  object ( ResourceInfo  ` )

Required. Information about the resource where the error is located.

`  errorDetails[]  `

`  object ( ErrorDetail  ` )

Required. The error details for the resource.

`  errorCount  `

`  integer  `

Required. How many errors there are in total for the resource. Truncation can be indicated by having an `  errorCount  ` that is higher than the size of `  errorDetails  ` .

## ErrorDetail

Provides details for errors, e.g. issues that where encountered when processing a subtask.

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
  &quot;location&quot;: {
    object (ErrorLocation)
  },
  &quot;errorInfo&quot;: {
    object (ErrorInfo)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  location  `

`  object ( ErrorLocation  ` )

Optional. The exact location within the resource (if applicable).

`  errorInfo  `

`  object ( ErrorInfo  ` )

Required. Describes the cause of the error with structured detail.

## ErrorLocation

Holds information about where the error is located.

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
  &quot;line&quot;: integer,
  &quot;column&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  line  `

`  integer  `

Optional. If applicable, denotes the line where the error occurred. A zero value means that there is no line information.

`  column  `

`  integer  `

Optional. If applicable, denotes the column where the error occurred. A zero value means that there is no columns information.
