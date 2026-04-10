  - [Resource: TransferResource](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.transferConfigs.transferResources#TransferResource)
      - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.transferConfigs.transferResources#TransferResource.SCHEMA_REPRESENTATION)
  - [Methods](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.transferConfigs.transferResources#METHODS_SUMMARY)

## Resource: TransferResource

Resource (table/partition) that is being transferred.

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
  &quot;name&quot;: string,
  &quot;type&quot;: enum (ResourceType),
  &quot;destination&quot;: enum (ResourceDestination),
  &quot;latestRun&quot;: {
    object (TransferRunBrief)
  },
  &quot;latestStatusDetail&quot;: {
    object (TransferResourceStatusDetail)
  },
  &quot;lastSuccessfulRun&quot;: {
    object (TransferRunBrief)
  },
  &quot;hierarchyDetail&quot;: {
    object (HierarchyDetail)
  },
  &quot;updateTime&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  name  `

`  string  `

Identifier. Resource name.

`  type  `

`  enum ( ResourceType  ` )

Optional. Resource type.

`  destination  `

`  enum ( ResourceDestination  ` )

Optional. Resource destination.

`  latestRun  `

`  object ( TransferRunBrief  ` )

Optional. Run details for the latest run.

`  latestStatusDetail  `

`  object ( TransferResourceStatusDetail  ` )

Optional. Status details for the latest run.

`  lastSuccessfulRun  `

`  object ( TransferRunBrief  ` )

Output only. Run details for the last successful run.

`  hierarchyDetail  `

`  object ( HierarchyDetail  ` )

Optional. Details about the hierarchy.

`  updateTime  `

`  string ( Timestamp  ` format)

Output only. Time when the resource was last updated.

## Methods

### `             get           `

Returns a transfer resource.

### `             list           `

Returns information about transfer resources.
