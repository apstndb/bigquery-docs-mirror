  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Request body](#body.request_body)
      - [JSON representation](#body.request_body.SCHEMA_REPRESENTATION)
  - [Response body](#body.response_body)
  - [Authorization scopes](#body.aspect)
  - [IAM Permissions](#body.aspect_1)
  - [Try it\!](#try-it)

Creates a Subscription to a Data Clean Room. This is a long-running operation as it will create one or more linked datasets. Throws a Bad Request error if the Data Exchange does not contain any listings.

### HTTP request

`  POST https://analyticshub.googleapis.com/v1/{name=projects/*/locations/*/dataExchanges/*}:subscribe  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  name  `

`  string  `

Required. Resource name of the Data Exchange. e.g. `  projects/publisherproject/locations/us/dataExchanges/123  `

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
  &quot;destination&quot;: string,
  &quot;destinationDataset&quot;: {
    object (DestinationDataset)
  },
  &quot;subscription&quot;: string,
  &quot;subscriberContact&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  destination  `

`  string  `

Required. The parent resource path of the Subscription. e.g. `  projects/subscriberproject/locations/us  `

`  destinationDataset  `

`  object ( DestinationDataset  ` )

Optional. BigQuery destination dataset to create for the subscriber.

`  subscription  `

`  string  `

Required. Name of the subscription to create. e.g. `  subscription1  `

`  subscriberContact  `

`  string  `

Email of the subscriber.

### Response body

If successful, the response body contains an instance of `  Operation  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .

### IAM Permissions

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `  destination  ` resource:

  - `  analyticshub.subscriptions.create  `

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `  name  ` resource:

  - `  analyticshub.dataExchanges.subscribe  `

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .
