  - [Resource: Listing](#Listing)
      - [JSON representation](#Listing.SCHEMA_REPRESENTATION)
  - [BigQueryDatasetSource](#BigQueryDatasetSource)
      - [JSON representation](#BigQueryDatasetSource.SCHEMA_REPRESENTATION)
  - [SelectedResource](#SelectedResource)
      - [JSON representation](#SelectedResource.SCHEMA_REPRESENTATION)
  - [RestrictedExportPolicy](#RestrictedExportPolicy)
      - [JSON representation](#RestrictedExportPolicy.SCHEMA_REPRESENTATION)
  - [Replica](#Replica)
      - [JSON representation](#Replica.SCHEMA_REPRESENTATION)
  - [ReplicaState](#ReplicaState)
  - [PrimaryState](#PrimaryState)
  - [PubSubTopicSource](#PubSubTopicSource)
      - [JSON representation](#PubSubTopicSource.SCHEMA_REPRESENTATION)
  - [State](#State)
  - [DataProvider](#DataProvider)
      - [JSON representation](#DataProvider.SCHEMA_REPRESENTATION)
  - [Category](#Category)
  - [Publisher](#Publisher)
      - [JSON representation](#Publisher.SCHEMA_REPRESENTATION)
  - [RestrictedExportConfig](#RestrictedExportConfig)
      - [JSON representation](#RestrictedExportConfig.SCHEMA_REPRESENTATION)
  - [StoredProcedureConfig](#StoredProcedureConfig)
      - [JSON representation](#StoredProcedureConfig.SCHEMA_REPRESENTATION)
  - [StoredProcedureType](#StoredProcedureType)
  - [CommercialInfo](#CommercialInfo)
      - [JSON representation](#CommercialInfo.SCHEMA_REPRESENTATION)
  - [GoogleCloudMarketplaceInfo](#GoogleCloudMarketplaceInfo)
      - [JSON representation](#GoogleCloudMarketplaceInfo.SCHEMA_REPRESENTATION)
  - [CommercialState](#CommercialState)
  - [Methods](#METHODS_SUMMARY)

## Resource: Listing

A listing is what gets published into a data exchange that a subscriber can subscribe to. It contains a reference to the data source along with descriptive information that will help subscribers find and subscribe the data.

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
  &quot;name&quot;: string,
  &quot;displayName&quot;: string,
  &quot;description&quot;: string,
  &quot;primaryContact&quot;: string,
  &quot;documentation&quot;: string,
  &quot;state&quot;: enum (State),
  &quot;icon&quot;: string,
  &quot;dataProvider&quot;: {
    object (DataProvider)
  },
  &quot;categories&quot;: [
    enum (Category)
  ],
  &quot;publisher&quot;: {
    object (Publisher)
  },
  &quot;requestAccess&quot;: string,
  &quot;restrictedExportConfig&quot;: {
    object (RestrictedExportConfig)
  },
  &quot;storedProcedureConfig&quot;: {
    object (StoredProcedureConfig)
  },
  &quot;resourceType&quot;: enum (SharedResourceType),

  // Union field source can be only one of the following:
  &quot;bigqueryDataset&quot;: {
    object (BigQueryDatasetSource)
  },
  &quot;pubsubTopic&quot;: {
    object (PubSubTopicSource)
  }
  // End of list of possible types for union field source.
  &quot;discoveryType&quot;: enum (DiscoveryType),
  &quot;commercialInfo&quot;: {
    object (CommercialInfo)
  },
  &quot;logLinkedDatasetQueryUserEmail&quot;: boolean,
  &quot;allowOnlyMetadataSharing&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  name  `

`  string  `

Output only. The resource name of the listing. e.g. `  projects/myproject/locations/us/dataExchanges/123/listings/456  `

`  displayName  `

`  string  `

Required. Human-readable display name of the listing. The display name must contain only Unicode letters, numbers (0-9), underscores (\_), dashes (-), spaces ( ), ampersands (&) and can't start or end with spaces. Default value is an empty string. Max length: 63 bytes.

`  description  `

`  string  `

Optional. Short description of the listing. The description must not contain Unicode non-characters and C0 and C1 control codes except tabs (HT), new lines (LF), carriage returns (CR), and page breaks (FF). Default value is an empty string. Max length: 2000 bytes.

`  primaryContact  `

`  string  `

Optional. Email or URL of the primary point of contact of the listing. Max Length: 1000 bytes.

`  documentation  `

`  string  `

Optional. Documentation describing the listing.

`  state  `

`  enum ( State  ` )

Output only. Current state of the listing.

`  icon  `

`  string ( bytes format)  `

Optional. Base64 encoded image representing the listing. Max Size: 3.0MiB Expected image dimensions are 512x512 pixels, however the API only performs validation on size of the encoded data. Note: For byte fields, the contents of the field are base64-encoded (which increases the size of the data by 33-36%) when using JSON on the wire.

A base64-encoded string.

`  dataProvider  `

`  object ( DataProvider  ` )

Optional. Details of the data provider who owns the source data.

`  categories[]  `

`  enum ( Category  ` )

Optional. Categories of the listing. Up to five categories are allowed.

`  publisher  `

`  object ( Publisher  ` )

Optional. Details of the publisher who owns the listing and who can share the source data.

`  requestAccess  `

`  string  `

Optional. Email or URL of the request access of the listing. Subscribers can use this reference to request access. Max Length: 1000 bytes.

`  restrictedExportConfig  `

`  object ( RestrictedExportConfig  ` )

Optional. If set, restricted export configuration will be propagated and enforced on the linked dataset.

`  storedProcedureConfig  `

`  object ( StoredProcedureConfig  ` )

Optional. If set, stored procedure configuration will be propagated and enforced on the linked dataset.

`  resourceType  `

`  enum ( SharedResourceType  ` )

Output only. Listing shared asset type.

Union field `  source  ` . Listing source. `  source  ` can be only one of the following:

`  bigqueryDataset  `

`  object ( BigQueryDatasetSource  ` )

Shared dataset i.e. BigQuery dataset source.

`  pubsubTopic  `

`  object ( PubSubTopicSource  ` )

Pub/Sub topic source.

`  discoveryType  `

`  enum ( DiscoveryType  ` )

Optional. Type of discovery of the listing on the discovery page.

`  commercialInfo  `

`  object ( CommercialInfo  ` )

Output only. Commercial info contains the information about the commercial data products associated with the listing.

`  logLinkedDatasetQueryUserEmail  `

`  boolean  `

Optional. By default, false. If true, the Listing has an email sharing mandate enabled.

`  allowOnlyMetadataSharing  `

`  boolean  `

Optional. If true, the listing is only available to get the resource metadata. Listing is non subscribable.

## BigQueryDatasetSource

A reference to a shared dataset. It is an existing BigQuery dataset with a collection of objects such as tables and views that you want to share with subscribers. When subscriber's subscribe to a listing, Analytics Hub creates a linked dataset in the subscriber's project. A Linked dataset is an opaque, read-only BigQuery dataset that serves as a *symbolic link* to a shared dataset.

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
  &quot;dataset&quot;: string,
  &quot;selectedResources&quot;: [
    {
      object (SelectedResource)
    }
  ],
  &quot;restrictedExportPolicy&quot;: {
    object (RestrictedExportPolicy)
  },
  &quot;replicaLocations&quot;: [
    string
  ],
  &quot;effectiveReplicas&quot;: [
    {
      object (Replica)
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  dataset  `

`  string  `

Optional. Resource name of the dataset source for this listing. e.g. `  projects/myproject/datasets/123  `

`  selectedResources[]  `

`  object ( SelectedResource  ` )

Optional. Resource in this dataset that is selectively shared. This field is required for data clean room exchanges.

`  restrictedExportPolicy  `

`  object ( RestrictedExportPolicy  ` )

Optional. If set, restricted export policy will be propagated and enforced on the linked dataset.

`  replicaLocations[]  `

`  string  `

Optional. A list of regions where the publisher has created shared dataset replicas.

`  effectiveReplicas[]  `

`  object ( Replica  ` )

Output only. Server-owned effective state of replicas. Contains both primary and secondary replicas. Each replica includes a system-computed (output-only) state and primary designation.

## SelectedResource

Resource in this dataset that is selectively shared.

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

  // Union field resource can be only one of the following:
  &quot;table&quot;: string,
  &quot;routine&quot;: string
  // End of list of possible types for union field resource.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `  resource  ` .

`  resource  ` can be only one of the following:

`  table  `

`  string  `

Optional. Format: For table: `  projects/{projectId}/datasets/{datasetId}/tables/{tableId}  ` Example:"projects/test\_project/datasets/test\_dataset/tables/test\_table"

`  routine  `

`  string  `

Optional. Format: For routine: `  projects/{projectId}/datasets/{datasetId}/routines/{routineId}  ` Example:"projects/test\_project/datasets/test\_dataset/routines/test\_routine"

## RestrictedExportPolicy

Restricted export policy used to configure restricted export on linked dataset.

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
  &quot;enabled&quot;: boolean,
  &quot;restrictDirectTableAccess&quot;: boolean,
  &quot;restrictQueryResult&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  enabled  `

`  boolean  `

Optional. If true, enable restricted export.

`  restrictDirectTableAccess  `

`  boolean  `

Optional. If true, restrict direct table access (read api/tabledata.list) on linked table.

`  restrictQueryResult  `

`  boolean  `

Optional. If true, restrict export of query result derived from restricted linked dataset table.

## Replica

Represents the state of a replica of a shared dataset. It includes the geographic location of the replica and system-computed, output-only fields indicating its replication state and whether it is the primary replica.

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
  &quot;location&quot;: string,
  &quot;replicaState&quot;: enum (ReplicaState),
  &quot;primaryState&quot;: enum (PrimaryState)
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  location  `

`  string  `

Output only. The geographic location where the replica resides. See [BigQuery locations](https://cloud.google.com/bigquery/docs/locations) for supported locations. Eg. "us-central1".

`  replicaState  `

`  enum ( ReplicaState  ` )

Output only. Assigned by Analytics Hub based on real BigQuery replication state.

`  primaryState  `

`  enum ( PrimaryState  ` )

Output only. Indicates that this replica is the primary replica.

## ReplicaState

Replica state of the shared dataset.

Enums

`  REPLICA_STATE_UNSPECIFIED  `

Default value. This value is unused.

`  READY_TO_USE  `

The replica is backfilled and ready to use.

`  UNAVAILABLE  `

The replica is unavailable, does not exist, or has not been backfilled yet.

## PrimaryState

Primary state of the replica. Set only for the primary replica.

Enums

`  PRIMARY_STATE_UNSPECIFIED  `

Default value. This value is unused.

`  PRIMARY_REPLICA  `

The replica is the primary replica.

## PubSubTopicSource

Pub/Sub topic source.

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
  &quot;topic&quot;: string,
  &quot;dataAffinityRegions&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  topic  `

`  string  `

Required. Resource name of the Pub/Sub topic source for this listing. e.g. projects/myproject/topics/topicId

`  dataAffinityRegions[]  `

`  string  `

Optional. Region hint on where the data might be published. Data affinity regions are modifiable. See <https://cloud.google.com/about/locations> for full listing of possible Cloud regions.

## State

State of the listing.

Enums

`  STATE_UNSPECIFIED  `

Default value. This value is unused.

`  ACTIVE  `

Subscribable state. Users with dataexchange.listings.subscribe permission can subscribe to this listing.

## DataProvider

Contains details of the data provider.

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
  &quot;name&quot;: string,
  &quot;primaryContact&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  name  `

`  string  `

Optional. Name of the data provider.

`  primaryContact  `

`  string  `

Optional. Email or URL of the data provider. Max Length: 1000 bytes.

## Category

Listing categories.

Enums

`  CATEGORY_UNSPECIFIED  `

`  CATEGORY_OTHERS  `

`  CATEGORY_ADVERTISING_AND_MARKETING  `

`  CATEGORY_COMMERCE  `

`  CATEGORY_CLIMATE_AND_ENVIRONMENT  `

`  CATEGORY_DEMOGRAPHICS  `

`  CATEGORY_ECONOMICS  `

`  CATEGORY_EDUCATION  `

`  CATEGORY_ENERGY  `

`  CATEGORY_FINANCIAL  `

`  CATEGORY_GAMING  `

`  CATEGORY_GEOSPATIAL  `

`  CATEGORY_HEALTHCARE_AND_LIFE_SCIENCE  `

`  CATEGORY_MEDIA  `

`  CATEGORY_PUBLIC_SECTOR  `

`  CATEGORY_RETAIL  `

`  CATEGORY_SPORTS  `

`  CATEGORY_SCIENCE_AND_RESEARCH  `

`  CATEGORY_TRANSPORTATION_AND_LOGISTICS  `

`  CATEGORY_TRAVEL_AND_TOURISM  `

`  CATEGORY_GOOGLE_EARTH_ENGINE  `

## Publisher

Contains details of the listing publisher.

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
  &quot;name&quot;: string,
  &quot;primaryContact&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  name  `

`  string  `

Optional. Name of the listing publisher.

`  primaryContact  `

`  string  `

Optional. Email or URL of the listing publisher. Max Length: 1000 bytes.

## RestrictedExportConfig

Restricted export config, used to configure restricted export on linked dataset.

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
  &quot;enabled&quot;: boolean,
  &quot;restrictDirectTableAccess&quot;: boolean,
  &quot;restrictQueryResult&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  enabled  `

`  boolean  `

Optional. If true, enable restricted export.

`  restrictDirectTableAccess  `

`  boolean  `

Output only. If true, restrict direct table access(read api/tabledata.list) on linked table.

`  restrictQueryResult  `

`  boolean  `

Optional. If true, restrict export of query result derived from restricted linked dataset table.

## StoredProcedureConfig

Stored procedure configuration, used to configure stored procedure sharing on linked dataset.

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
  &quot;enabled&quot;: boolean,
  &quot;allowedStoredProcedureTypes&quot;: [
    enum (StoredProcedureType)
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  enabled  `

`  boolean  `

Optional. If true, enable sharing of stored procedure.

`  allowedStoredProcedureTypes[]  `

`  enum ( StoredProcedureType  ` )

Output only. Types of stored procedure supported to share.

## StoredProcedureType

Enum to specify the type of stored procedure to share.

Enums

`  STORED_PROCEDURE_TYPE_UNSPECIFIED  `

Default value. This value is unused.

`  SQL_PROCEDURE  `

SQL stored procedure.

## CommercialInfo

Commercial info contains the information about the commercial data products associated with the listing.

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
  &quot;cloudMarketplace&quot;: {
    object (GoogleCloudMarketplaceInfo)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  cloudMarketplace  `

`  object ( GoogleCloudMarketplaceInfo  ` )

Output only. Details of the Marketplace Data Product associated with the Listing.

## GoogleCloudMarketplaceInfo

Specifies the details of the Marketplace Data Product associated with the Listing.

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
  &quot;service&quot;: string,
  &quot;commercialState&quot;: enum (CommercialState)
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  service  `

`  string  `

Output only. Resource name of the commercial service associated with the Marketplace Data Product. e.g. example.com

`  commercialState  `

`  enum ( CommercialState  ` )

Output only. Commercial state of the Marketplace Data Product.

## CommercialState

Indicates whether this commercial access is currently active.

Enums

`  COMMERCIAL_STATE_UNSPECIFIED  `

Commercialization is incomplete and cannot be used.

`  ONBOARDING  `

Commercialization has been initialized.

`  ACTIVE  `

Commercialization is complete and available for use.

## Methods

### `             create           `

Creates a new listing.

### `             delete           `

Deletes a listing.

### `             get           `

Gets the details of a listing.

### `             getIamPolicy           `

Gets the IAM policy.

### `             list           `

Lists all listings in a given project and location.

### `             listSubscriptions           `

Lists all subscriptions on a given Data Exchange or Listing.

### `             patch           `

Updates an existing listing.

### `             setIamPolicy           `

Sets the IAM policy.

### `             subscribe           `

Subscribes to a listing.

### `             testIamPermissions           `

Returns the permissions that a caller has.
