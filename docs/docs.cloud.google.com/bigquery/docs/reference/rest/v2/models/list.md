  - [HTTP request](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/models/list#body.HTTP_TEMPLATE)
  - [Path parameters](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/models/list#body.PATH_PARAMETERS)
  - [Query parameters](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/models/list#body.QUERY_PARAMETERS)
  - [Request body](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/models/list#body.request_body)
  - [Response body](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/models/list#body.response_body)
      - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/models/list#body.ListModelsResponse.SCHEMA_REPRESENTATION)
  - [Authorization scopes](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/models/list#body.aspect)
  - [Try it\!](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/models/list#try-it)

Lists all models in the specified dataset. Requires the READER dataset role. After retrieving the list of models, you can get information about a particular model by calling the models.get method.

### HTTP request

`  GET https://bigquery.googleapis.com/bigquery/v2/projects/{projectId}/datasets/{datasetId}/models  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  projectId  `

`  string  `

Required. Project ID of the models to list.

`  datasetId  `

`  string  `

Required. Dataset ID of the models to list.

### Query parameters

Parameters

`  maxResults  `

`  integer  `

The maximum number of results to return in a single response page. Leverage the page tokens to iterate through the entire collection.

`  pageToken  `

`  string  `

Page token, returned by a previous call to request the next page of results

### Request body

The request body must be empty.

### Response body

Response format for a single page when listing BigQuery ML models.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;models&quot;: [
    {
      object (Model)
    }
  ],
  &quot;nextPageToken&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  models[]  `

`  object ( Model  ` )

Models in the requested dataset. Only the following fields are populated: modelReference, modelType, creationTime, lastModifiedTime and labels.

`  nextPageToken  `

`  string  `

A token to request the next page of results.

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `
  - `  https://www.googleapis.com/auth/bigquery.readonly  `
  - `  https://www.googleapis.com/auth/cloud-platform.read-only  `

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
