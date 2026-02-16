  - [JSON representation](#SCHEMA_REPRESENTATION)
  - [DestinationDatasetReference](#DestinationDatasetReference)
      - [JSON representation](#DestinationDatasetReference.SCHEMA_REPRESENTATION)

Defines the destination bigquery dataset.

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
  &quot;datasetReference&quot;: {
    object (DestinationDatasetReference)
  },
  &quot;friendlyName&quot;: string,
  &quot;description&quot;: string,
  &quot;labels&quot;: {
    string: string,
    ...
  },
  &quot;location&quot;: string,
  &quot;replicaLocations&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  datasetReference  `

`  object ( DestinationDatasetReference  ` )

Required. A reference that identifies the destination dataset.

`  friendlyName  `

`  string  `

Optional. A descriptive name for the dataset.

`  description  `

`  string  `

Optional. A user-friendly description of the dataset.

`  labels  `

`  map (key: string, value: string)  `

Optional. The labels associated with this dataset. You can use these to organize and group your datasets. You can set this property when inserting or updating a dataset. See <https://cloud.google.com/resource-manager/docs/creating-managing-labels> for more information.

An object containing a list of `  "key": value  ` pairs. Example: `  { "name": "wrench", "mass": "1.3kg", "count": "3" }  ` .

`  location  `

`  string  `

Required. The geographic location where the dataset should reside. See <https://cloud.google.com/bigquery/docs/locations> for supported locations.

`  replicaLocations[]  `

`  string  `

Optional. The geographic locations where the dataset should be replicated. See [BigQuery locations](https://cloud.google.com/bigquery/docs/locations) for supported locations.

## DestinationDatasetReference

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

Required. The ID of the project containing this dataset.
