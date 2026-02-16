  - [Resource: Subscription](#Subscription)
      - [JSON representation](#Subscription.SCHEMA_REPRESENTATION)
  - [Methods](#METHODS_SUMMARY)

## Resource: Subscription

A subscription represents a subscribers' access to a particular set of published data. It contains references to associated listings, data exchanges, and linked datasets.

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
  &quot;creationTime&quot;: string,
  &quot;lastModifyTime&quot;: string,
  &quot;organizationId&quot;: string,
  &quot;organizationDisplayName&quot;: string,
  &quot;state&quot;: enum (State),
  &quot;linkedDatasetMap&quot;: {
    string: {
      object (LinkedResource)
    },
    ...
  },
  &quot;subscriberContact&quot;: string,
  &quot;linkedResources&quot;: [
    {
      object (LinkedResource)
    }
  ],
  &quot;resourceType&quot;: enum (SharedResourceType),
  &quot;commercialInfo&quot;: {
    object (CommercialInfo)
  },
  &quot;destinationDataset&quot;: {
    object (DestinationDataset)
  },

  // Union field resource_name can be only one of the following:
  &quot;listing&quot;: string,
  &quot;dataExchange&quot;: string
  // End of list of possible types for union field resource_name.
  &quot;logLinkedDatasetQueryUserEmail&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  name  `

`  string  `

Output only. The resource name of the subscription. e.g. `  projects/myproject/locations/us/subscriptions/123  ` .

`  creationTime  `

`  string ( Timestamp  ` format)

Output only. Timestamp when the subscription was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

`  lastModifyTime  `

`  string ( Timestamp  ` format)

Output only. Timestamp when the subscription was last modified.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

`  organizationId  `

`  string  `

Output only. Organization of the project this subscription belongs to.

`  organizationDisplayName  `

`  string  `

Output only. Display name of the project of this subscription.

`  state  `

`  enum ( State  ` )

Output only. Current state of the subscription.

`  linkedDatasetMap  `

`  map (key: string, value: object ( LinkedResource  ` ))

Output only. Map of listing resource names to associated linked resource, e.g. projects/123/locations/us/dataExchanges/456/listings/789 -\> projects/123/datasets/my\_dataset

For listing-level subscriptions, this is a map of size 1. Only contains values if state == STATE\_ACTIVE.

An object containing a list of `  "key": value  ` pairs. Example: `  { "name": "wrench", "mass": "1.3kg", "count": "3" }  ` .

`  subscriberContact  `

`  string  `

Output only. Email of the subscriber.

`  linkedResources[]  `

`  object ( LinkedResource  ` )

Output only. Linked resources created in the subscription. Only contains values if state = STATE\_ACTIVE.

`  resourceType  `

`  enum ( SharedResourceType  ` )

Output only. Listing shared asset type.

`  commercialInfo  `

`  object ( CommercialInfo  ` )

Output only. This is set if this is a commercial subscription i.e. if this subscription was created from subscribing to a commercial listing.

`  destinationDataset  `

`  object ( DestinationDataset  ` )

Optional. BigQuery destination dataset to create for the subscriber.

Union field `  resource_name  ` .

`  resource_name  ` can be only one of the following:

`  listing  `

`  string  `

Output only. Resource name of the source Listing. e.g. projects/123/locations/us/dataExchanges/456/listings/789

`  dataExchange  `

`  string  `

Output only. Resource name of the source Data Exchange. e.g. projects/123/locations/us/dataExchanges/456

`  logLinkedDatasetQueryUserEmail  `

`  boolean  `

Output only. By default, false. If true, the Subscriber agreed to the email sharing mandate that is enabled for DataExchange/Listing.

## Methods

### `             delete           `

Deletes a subscription.

### `             get           `

Gets the details of a Subscription.

### `             getIamPolicy           `

Gets the IAM policy.

### `             list           `

Lists all subscriptions in a given project and location.

### `             refresh           `

Refreshes a Subscription to a Data Exchange.

### `             revoke           `

Revokes a given subscription.

### `             setIamPolicy           `

Sets the IAM policy.
