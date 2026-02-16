  - [JSON representation](#SCHEMA_REPRESENTATION)
  - [DatasetReference](#DatasetReference)
      - [JSON representation](#DatasetReference.SCHEMA_REPRESENTATION)

Grants all resources of particular types in a particular dataset read access to the current dataset.

Similar to how individually authorized views work, updates to any resource granted through its dataset (including creation of new resources) requires read permission to referenced resources, plus write permission to the authorizing dataset.

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
  &quot;dataset&quot;: {
    object (DatasetReference)
  },
  &quot;targetTypes&quot;: [
    enum (DatasetAccessEntry.TargetType)
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  dataset  `

`  object ( DatasetReference  ` )

The dataset this entry applies to

`  targetTypes[]  `

`  enum ( DatasetAccessEntry.TargetType  ` )

Which resources in the dataset this entry applies to. Currently, only views are supported, but additional target types may be added in the future.

## DatasetReference

Identifier for a dataset.

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
  &quot;datasetId&quot;: string,
  &quot;projectId&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  datasetId  `

`  string  `

Required. A unique ID for this dataset, without the project name. The ID must contain only letters (a-z, A-Z), numbers (0-9), or underscores (\_). The maximum length is 1,024 characters.

`  projectId  `

`  string  `

Optional. The ID of the project containing this dataset.
