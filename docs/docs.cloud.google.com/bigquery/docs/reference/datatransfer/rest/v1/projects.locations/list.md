  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Query parameters](#body.QUERY_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
      - [JSON representation](#body.ListLocationsResponse.SCHEMA_REPRESENTATION)
  - [Authorization scopes](#body.aspect)
  - [Try it\!](#try-it)

**Full name** : projects.locations.list

Lists information about the supported locations for this service. This method can be called in two ways:

  - **List all public locations:** Use the path `  GET /v1/locations  ` .
  - **List project-visible locations:** Use the path `  GET /v1/projects/{projectId}/locations  ` . This may include public locations as well as private or other locations specifically visible to the project.

### HTTP request

`  GET https://bigquerydatatransfer.googleapis.com/v1/{name=projects/*}/locations  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  name  `

`  string  `

The resource that owns the locations collection, if applicable.

### Query parameters

Parameters

`  filter  `

`  string  `

A filter to narrow down results to a preferred subset. The filtering language accepts strings like `  "displayName=tokyo"  ` , and is documented in more detail in [AIP-160](https://google.aip.dev/160) .

`  pageSize  `

`  integer  `

The maximum number of results to return. If not set, the service selects a default.

`  pageToken  `

`  string  `

A page token received from the `  nextPageToken  ` field in the response. Send that page token to receive the subsequent page.

`  extraLocationTypes[]  `

`  string  `

Optional. Do not use this field. It is unsupported and is ignored unless explicitly documented otherwise. This is primarily for internal usage.

### Request body

The request body must be empty.

### Response body

The response message for `  Locations.ListLocations  ` .

If successful, the response body contains data with the following structure:

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
  &quot;locations&quot;: [
    {
      object (Location)
    }
  ],
  &quot;nextPageToken&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  locations[]  `

`  object ( Location  ` )

A list of locations that matches the specified filter in the request.

`  nextPageToken  `

`  string  `

The standard List next-page token.

### Authorization scopes

Requires the following OAuth scope:

  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
