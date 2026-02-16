  - [JSON representation](#SCHEMA_REPRESENTATION)

Request message for `  SetIamPolicy  ` method.

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
  &quot;policy&quot;: {
    object (Policy)
  },
  &quot;updateMask&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  resource  `

`  string  `

REQUIRED: The resource for which the policy is being specified. See [Resource names](https://cloud.google.com/apis/design/resource_names) for the appropriate value for this field.

`  policy  `

`  object ( Policy  ` )

REQUIRED: The complete policy to be applied to the `  resource  ` . The size of the policy is limited to a few 10s of KB. An empty policy is a valid policy but certain Google Cloud services (such as Projects) might reject them.

`  updateMask  `

`  string ( FieldMask  ` format)

OPTIONAL: A FieldMask specifying which fields of the policy to modify. Only the fields in the mask will be modified. If no mask is provided, the following default mask is used:

`  paths: "bindings, etag"  `
