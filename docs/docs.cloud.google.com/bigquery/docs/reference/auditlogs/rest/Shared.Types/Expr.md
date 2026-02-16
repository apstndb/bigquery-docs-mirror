  - [JSON representation](#SCHEMA_REPRESENTATION)

Represents a textual expression in the Common Expression Language (CEL) syntax. CEL is a C-like expression language. The syntax and semantics of CEL are documented at <https://github.com/google/cel-spec> .

Example (Comparison):

``` text
title: "Summary size limit"
description: "Determines if a summary is less than 100 chars"
expression: "document.summary.size() < 100"
```

Example (Equality):

``` text
title: "Requestor is owner"
description: "Determines if requestor is the document owner"
expression: "document.owner == request.auth.claims.email"
```

Example (Logic):

``` text
title: "Public documents"
description: "Determine whether the document should be publicly visible"
expression: "document.type != 'private' && document.type != 'internal'"
```

Example (Data Manipulation):

``` text
title: "Notification string"
description: "Create a notification string with a timestamp."
expression: "'New message received at ' + string(document.create_time)"
```

The exact variables and functions that may be referenced within an expression are determined by the service that evaluates it. See the service documentation for additional information.

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
  &quot;expression&quot;: string,
  &quot;title&quot;: string,
  &quot;description&quot;: string,
  &quot;location&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  expression  `

`  string  `

Textual representation of an expression in Common Expression Language syntax.

`  title  `

`  string  `

Optional. Title for the expression, i.e. a short string describing its purpose. This can be used e.g. in UIs which allow to enter the expression.

`  description  `

`  string  `

Optional. Description of the expression. This is a longer text which describes the expression, e.g. when hovered over it in a UI.

`  location  `

`  string  `

Optional. String indicating the location of the expression for error reporting, e.g. a file name and a position in the file.
