  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Query parameters](#body.QUERY_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
      - [JSON representation](#body.ListDataPoliciesResponse.SCHEMA_REPRESENTATION)
  - [Authorization scopes](#body.aspect)
  - [IAM Permissions](#body.aspect_1)
  - [Try it\!](#try-it)

List all of the data policies in the specified parent project.

### HTTP request

`  GET https://bigquerydatapolicy.googleapis.com/v2beta1/{parent=projects/*/locations/*}/dataPolicies  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  parent  `

`  string  `

Required. Resource name of the project for which to list data policies. Format is `  projects/{projectNumber}/locations/{locationId}  ` .

### Query parameters

Parameters

`  pageSize  `

`  integer  `

Optional. The maximum number of data policies to return. Must be a value between 1 and 1000. If not set, defaults to 50.

`  pageToken  `

`  string  `

Optional. The `  nextPageToken  ` value returned from a previous list request, if any. If not set, defaults to an empty string.

### Request body

The request body must be empty.

### Response body

Response message for the dataPolicies.list method.

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
  &quot;dataPolicies&quot;: [
    {
      object (DataPolicy)
    }
  ],
  &quot;nextPageToken&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  dataPolicies[]  `

`  object ( DataPolicy  ` )

Data policies that belong to the requested project.

`  nextPageToken  `

`  string  `

Token used to retrieve the next page of results, or empty if there are no more results.

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .

### IAM Permissions

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `  parent  ` resource:

  - `  bigquery.dataPolicies.list  `

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .
