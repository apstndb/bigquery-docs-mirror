  - [JSON representation](#SCHEMA_REPRESENTATION)

Request message for `  TestIamPermissions  ` method.

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
  &quot;resource&quot;: string,
  &quot;permissions&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  resource  `

`  string  `

REQUIRED: The resource for which the policy detail is being requested. See [Resource names](https://cloud.google.com/apis/design/resource_names) for the appropriate value for this field.

`  permissions[]  `

`  string  `

The set of permissions to check for the `  resource  ` . Permissions with wildcards (such as `  *  ` or `  storage.*  ` ) are not allowed. For more information see [IAM Overview](https://cloud.google.com/iam/docs/overview#permissions) .
