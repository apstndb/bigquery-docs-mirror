  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Request body](#body.request_body)
      - [JSON representation](#body.request_body.SCHEMA_REPRESENTATION)
  - [Response body](#body.response_body)
  - [Authorization scopes](#body.aspect)
  - [IAM Permissions](#body.aspect_1)
  - [DestinationDataset](#DestinationDataset)
      - [JSON representation](#DestinationDataset.SCHEMA_REPRESENTATION)
  - [DestinationDatasetReference](#DestinationDatasetReference)
      - [JSON representation](#DestinationDatasetReference.SCHEMA_REPRESENTATION)
  - [Try it\!](#try-it)

Subscribes to a listing.

Currently, with Analytics Hub, you can create listings that reference only BigQuery datasets. Upon subscription to a listing for a BigQuery dataset, Analytics Hub creates a linked dataset in the subscriber's project.

### HTTP request

`  POST https://analyticshub.googleapis.com/v1beta1/{name=projects/*/locations/*/dataExchanges/*/listings/*}:subscribe  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  name  `

`  string  `

Required. Resource name of the listing that you want to subscribe to. e.g. `  projects/myproject/locations/us/dataExchanges/123/listings/456  ` .

### Request body

The request body contains data with the following structure:

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

  // Union field destination can be only one of the following:
  &quot;destinationDataset&quot;: {
    object (DestinationDataset)
  }
  // End of list of possible types for union field destination.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `  destination  ` . Resulting destination of the listing that you subscribed to. `  destination  ` can be only one of the following:

`  destinationDataset  `

`  object ( DestinationDataset  ` )

BigQuery destination dataset to create for the subscriber.

### Response body

If successful, the response body is empty.

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .

### IAM Permissions

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `  name  ` resource:

  - `  analyticshub.listings.subscribe  `

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .

## DestinationDataset

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
  &quot;location&quot;: string
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
