  - [Resource: TransferResource](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.transferResources#TransferResource)
      - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.transferResources#TransferResource.SCHEMA_REPRESENTATION)
      - [ResourceType](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.transferResources#TransferResource.ResourceType)
      - [ResourceDestination](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.transferResources#TransferResource.ResourceDestination)
      - [TransferRunBrief](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.transferResources#TransferResource.TransferRunBrief)
          - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.transferResources#TransferResource.TransferRunBrief.SCHEMA_REPRESENTATION)
      - [TransferResourceStatusDetail](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.transferResources#TransferResource.TransferResourceStatusDetail)
          - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.transferResources#TransferResource.TransferResourceStatusDetail.SCHEMA_REPRESENTATION)
      - [ResourceTransferState](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.transferResources#TransferResource.ResourceTransferState)
      - [TransferStatusSummary](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.transferResources#TransferResource.TransferStatusSummary)
          - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.transferResources#TransferResource.TransferStatusSummary.SCHEMA_REPRESENTATION)
      - [TransferStatusMetric](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.transferResources#TransferResource.TransferStatusMetric)
          - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.transferResources#TransferResource.TransferStatusMetric.SCHEMA_REPRESENTATION)
      - [TransferStatusUnit](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.transferResources#TransferResource.TransferStatusUnit)
      - [HierarchyDetail](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.transferResources#TransferResource.HierarchyDetail)
          - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.transferResources#TransferResource.HierarchyDetail.SCHEMA_REPRESENTATION)
      - [TableDetail](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.transferResources#TransferResource.TableDetail)
          - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.transferResources#TransferResource.TableDetail.SCHEMA_REPRESENTATION)
      - [PartitionDetail](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.transferResources#TransferResource.PartitionDetail)
          - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.transferResources#TransferResource.PartitionDetail.SCHEMA_REPRESENTATION)
  - [Methods](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.transferResources#METHODS_SUMMARY)

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

### ResourceType

Type of resource being transferred.

Enums

`  RESOURCE_TYPE_UNSPECIFIED  `

Default value.

`  RESOURCE_TYPE_TABLE  `

Table resource type.

`  RESOURCE_TYPE_PARTITION  `

Partition resource type.

### ResourceDestination

The destination for a transferred resource.

Enums

`  RESOURCE_DESTINATION_UNSPECIFIED  `

Default value.

`  RESOURCE_DESTINATION_BIGQUERY  `

BigQuery.

`  RESOURCE_DESTINATION_DATAPROC_METASTORE  `

Dataproc Metastore.

`  RESOURCE_DESTINATION_BIGLAKE_METASTORE  `

BigLake Metastore.

`  RESOURCE_DESTINATION_BIGLAKE_REST_CATALOG  `

BigLake REST Catalog.

`  RESOURCE_DESTINATION_BIGLAKE_HIVE_CATALOG  `

BigLake Hive Catalog.

### TransferRunBrief

Basic information about a transfer run.

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
  &quot;run&quot;: string,
  &quot;startTime&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  run  `

`  string  `

Optional. Run URI. The format must be: `  projects/{project}/locations/{location}/transferConfigs/{transferConfig}/run/{run}  `

`  startTime  `

`  string ( Timestamp  ` format)

Optional. Start time of the transfer run.

### TransferResourceStatusDetail

Status details of the resource being transferred.

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
  &quot;state&quot;: enum (ResourceTransferState),
  &quot;summary&quot;: {
    object (TransferStatusSummary)
  },
  &quot;error&quot;: {
    object (Status)
  },
  &quot;completedPercentage&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  state  `

`  enum ( ResourceTransferState  ` )

Optional. Transfer state of the resource.

`  summary  `

`  object ( TransferStatusSummary  ` )

Optional. Transfer status summary of the resource.

`  error  `

`  object ( Status  ` )

Optional. Transfer error details for the resource.

`  completedPercentage  `

`  number  `

Output only. Percentage of the transfer completed. Valid values: 0-100.

### ResourceTransferState

The transfer state of an individual resource (e.g., a table or partition). This may differ from the overall transfer run's state. For instance, a resource can be transferred successfully even if the run as a whole fails.

Enums

`  RESOURCE_TRANSFER_STATE_UNSPECIFIED  `

Default value.

`  RESOURCE_TRANSFER_PENDING  `

Resource is waiting to be transferred.

`  RESOURCE_TRANSFER_RUNNING  `

Resource transfer is running.

`  RESOURCE_TRANSFER_SUCCEEDED  `

Resource transfer is a success.

`  RESOURCE_TRANSFER_FAILED  `

Resource transfer failed.

`  RESOURCE_TRANSFER_CANCELLED  `

Resource transfer was cancelled.

### TransferStatusSummary

Status summary of the resource being transferred.

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
  &quot;metrics&quot;: [
    {
      object (TransferStatusMetric)
    }
  ],
  &quot;progressUnit&quot;: enum (TransferStatusUnit)
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  metrics[]  `

`  object ( TransferStatusMetric  ` )

Optional. List of transfer status metrics.

`  progressUnit  `

`  enum ( TransferStatusUnit  ` )

Input only. Unit based on which transfer status progress should be calculated.

### TransferStatusMetric

Metrics for tracking the transfer status.

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
  &quot;completed&quot;: string,
  &quot;pending&quot;: string,
  &quot;failed&quot;: string,
  &quot;total&quot;: string,
  &quot;unit&quot;: enum (TransferStatusUnit)
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  completed  `

`  string ( int64 format)  `

Optional. Number of units transferred successfully.

`  pending  `

`  string ( int64 format)  `

Optional. Number of units pending transfer.

`  failed  `

`  string ( int64 format)  `

Optional. Number of units that failed to transfer.

`  total  `

`  string ( int64 format)  `

Optional. Total number of units for the transfer.

`  unit  `

`  enum ( TransferStatusUnit  ` )

Optional. Unit for measuring progress (e.g., BYTES).

### TransferStatusUnit

Unit of the transfer status.

Enums

`  TRANSFER_STATUS_UNIT_UNSPECIFIED  `

Default value.

`  TRANSFER_STATUS_UNIT_BYTES  `

Bytes.

`  TRANSFER_STATUS_UNIT_OBJECTS  `

Objects.

### HierarchyDetail

Details about the hierarchy.

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

  // Union field detail can be only one of the following:
  &quot;tableDetail&quot;: {
    object (TableDetail)
  },
  &quot;partitionDetail&quot;: {
    object (PartitionDetail)
  }
  // End of list of possible types for union field detail.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `  detail  ` . Details about the hierarchy can be one of table/partition. `  detail  ` can be only one of the following:

`  tableDetail  `

`  object ( TableDetail  ` )

Optional. Table details related to hierarchy.

`  partitionDetail  `

`  object ( PartitionDetail  ` )

Optional. Partition details related to hierarchy.

### TableDetail

Table details related to hierarchy.

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
  &quot;partitionCount&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  partitionCount  `

`  string ( int64 format)  `

Optional. Total number of partitions being tracked within the table.

### PartitionDetail

Partition details related to hierarchy.

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
  &quot;table&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  table  `

`  string  `

Optional. Name of the table which has the partitions.

## Methods

### `             get           `

Returns a transfer resource.

### `             list           `

Returns information about transfer resources.
