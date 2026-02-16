  - [Resource: DataExchange](#DataExchange)
      - [JSON representation](#DataExchange.SCHEMA_REPRESENTATION)
  - [SharingEnvironmentConfig](#SharingEnvironmentConfig)
      - [JSON representation](#SharingEnvironmentConfig.SCHEMA_REPRESENTATION)
  - [DefaultExchangeConfig](#DefaultExchangeConfig)
  - [DcrExchangeConfig](#DcrExchangeConfig)
      - [JSON representation](#DcrExchangeConfig.SCHEMA_REPRESENTATION)
  - [Methods](#METHODS_SUMMARY)

## Resource: DataExchange

A data exchange is a container that lets you share data. Along with the descriptive information about the data exchange, it contains listings that reference shared datasets.

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
  &quot;listingCount&quot;: integer,
  &quot;icon&quot;: string,
  &quot;sharingEnvironmentConfig&quot;: {
    object (SharingEnvironmentConfig)
  },
  &quot;discoveryType&quot;: enum (DiscoveryType),
  &quot;logLinkedDatasetQueryUserEmail&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  name  `

`  string  `

Output only. The resource name of the data exchange. e.g. `  projects/myproject/locations/us/dataExchanges/123  ` .

`  displayName  `

`  string  `

Required. Human-readable display name of the data exchange. The display name must contain only Unicode letters, numbers (0-9), underscores (\_), dashes (-), spaces ( ), ampersands (&) and must not start or end with spaces. Default value is an empty string. Max length: 63 bytes.

`  description  `

`  string  `

Optional. Description of the data exchange. The description must not contain Unicode non-characters as well as C0 and C1 control codes except tabs (HT), new lines (LF), carriage returns (CR), and page breaks (FF). Default value is an empty string. Max length: 2000 bytes.

`  primaryContact  `

`  string  `

Optional. Email or URL of the primary point of contact of the data exchange. Max Length: 1000 bytes.

`  documentation  `

`  string  `

Optional. Documentation describing the data exchange.

`  listingCount  `

`  integer  `

Output only. Number of listings contained in the data exchange.

`  icon  `

`  string ( bytes format)  `

Optional. Base64 encoded image representing the data exchange. Max Size: 3.0MiB Expected image dimensions are 512x512 pixels, however the API only performs validation on size of the encoded data. Note: For byte fields, the content of the fields are base64-encoded (which increases the size of the data by 33-36%) when using JSON on the wire.

A base64-encoded string.

`  sharingEnvironmentConfig  `

`  object ( SharingEnvironmentConfig  ` )

Optional. Configurable data sharing environment option for a data exchange.

`  discoveryType  `

`  enum ( DiscoveryType  ` )

Optional. Type of discovery on the discovery page for all the listings under this exchange. Updating this field also updates (overwrites) the discoveryType field for all the listings under this exchange.

`  logLinkedDatasetQueryUserEmail  `

`  boolean  `

Optional. By default, false. If true, the DataExchange has an email sharing mandate enabled.

## SharingEnvironmentConfig

Sharing environment is a behavior model for sharing data within a data exchange. This option is configurable for a data exchange.

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

  // Union field environment can be only one of the following:
  &quot;defaultExchangeConfig&quot;: {
    object (DefaultExchangeConfig)
  },
  &quot;dcrExchangeConfig&quot;: {
    object (DcrExchangeConfig)
  }
  // End of list of possible types for union field environment.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `  environment  ` .

`  environment  ` can be only one of the following:

`  defaultExchangeConfig  `

`  object ( DefaultExchangeConfig  ` )

Default Analytics Hub data exchange, used for secured data sharing.

`  dcrExchangeConfig  `

`  object ( DcrExchangeConfig  ` )

Data Clean Room (DCR), used for privacy-safe and secured data sharing.

## DefaultExchangeConfig

This type has no fields.

Default Analytics Hub data exchange, used for secured data sharing.

## DcrExchangeConfig

Data Clean Room (DCR), used for privacy-safe and secured data sharing.

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
  &quot;singleSelectedResourceSharingRestriction&quot;: boolean,
  &quot;singleLinkedDatasetPerCleanroom&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  singleSelectedResourceSharingRestriction  `

`  boolean  `

Output only. If True, this DCR restricts the contributors to sharing only a single resource in a Listing. And no two resources should have the same IDs. So if a contributor adds a view with a conflicting name, the CreateListing API will reject the request. if False, the data contributor can publish an entire dataset (as before). This is not configurable, and by default, all new DCRs will have the restriction set to True.

`  singleLinkedDatasetPerCleanroom  `

`  boolean  `

Output only. If True, when subscribing to this DCR, it will create only one linked dataset containing all resources shared within the cleanroom. If False, when subscribing to this DCR, it will create 1 linked dataset per listing. This is not configurable, and by default, all new DCRs will have the restriction set to True.

## Methods

### `             create           `

Creates a new data exchange.

### `             delete           `

Deletes an existing data exchange.

### `             get           `

Gets the details of a data exchange.

### `             getIamPolicy           `

Gets the IAM policy.

### `             list           `

Lists all data exchanges in a given project and location.

### `             listSubscriptions           `

Lists all subscriptions on a given Data Exchange or Listing.

### `             patch           `

Updates an existing data exchange.

### `             setIamPolicy           `

Sets the IAM policy.

### `             subscribe           `

Creates a Subscription to a Data Clean Room.

### `             testIamPermissions           `

Returns the permissions that a caller has.
