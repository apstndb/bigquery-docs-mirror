  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Query parameters](#body.QUERY_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
      - [JSON representation](#body.ListRoutinesResponse.SCHEMA_REPRESENTATION)
  - [Authorization scopes](#body.aspect)
  - [Try it\!](#try-it)

Lists all routines in the specified dataset. Requires the READER dataset role.

### HTTP request

`  GET https://bigquery.googleapis.com/bigquery/v2/projects/{projectId}/datasets/{datasetId}/routines  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  projectId  `

`  string  `

Required. Project ID of the routines to list

`  datasetId  `

`  string  `

Required. Dataset ID of the routines to list

### Query parameters

Parameters

`  maxResults  `

`  integer  `

The maximum number of results to return in a single response page. Leverage the page tokens to iterate through the entire collection.

`  pageToken  `

`  string  `

Page token, returned by a previous call, to request the next page of results

`  readMask  `

`  string ( FieldMask  ` format)

If set, then only the Routine fields in the field mask, as well as projectId, datasetId and routineId, are returned in the response. If unset, then the following Routine fields are returned: etag, projectId, datasetId, routineId, routineType, creationTime, lastModifiedTime, and language.

This is a comma-separated list of fully qualified names of fields. Example: `  "user.displayName,photo"  ` .

`  filter  `

`  string  `

If set, then only the Routines matching this filter are returned. The supported format is `  routineType:{RoutineType}  ` , where `  {RoutineType}  ` is a RoutineType enum. For example: `  routineType:SCALAR_FUNCTION  ` .

### Request body

The request body must be empty.

### Response body

Describes the format of a single result page when listing routines.

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
  &quot;routines&quot;: [
    {
      object (Routine)
    }
  ],
  &quot;nextPageToken&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  routines[]  `

`  object ( Routine  ` )

Routines in the requested dataset. Unless readMask is set in the request, only the following fields are populated: etag, projectId, datasetId, routineId, routineType, creationTime, lastModifiedTime, language, and remoteFunctionOptions.

`  nextPageToken  `

`  string  `

A token to request the next page of results.

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `
  - `  https://www.googleapis.com/auth/bigquery.readonly  `
  - `  https://www.googleapis.com/auth/cloud-platform.read-only  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
