  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Query parameters](#body.QUERY_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
      - [JSON representation](#body.JobCancelResponse.SCHEMA_REPRESENTATION)
  - [Authorization scopes](#body.aspect)
  - [Try it\!](#try-it)

Requests that a job be cancelled. This call will return immediately, and the client will need to poll for the job status to see if the cancel completed successfully. Cancelled jobs may still incur costs.

### HTTP request

`  POST https://bigquery.googleapis.com/bigquery/v2/projects/{projectId}/jobs/{jobId}/cancel  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  projectId  `

`  string  `

Required. Project ID of the job to cancel

`  jobId  `

`  string  `

Required. Job ID of the job to cancel

### Query parameters

Parameters

`  location  `

`  string  `

The geographic location of the job. You must [specify the location](https://cloud.google.com/bigquery/docs/locations#specify_locations) to run the job for the following scenarios:

  - If the location to run a job is not in the `  us  ` or the `  eu  ` multi-regional location
  - If the job's location is in a single region (for example, `  us-central1  ` )

### Request body

The request body must be empty.

### Response body

Describes format of a jobs cancellation response.

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
  &quot;kind&quot;: string,
  &quot;job&quot;: {
    object (Job)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  kind  `

`  string  `

The resource type of the response.

`  job  `

`  object ( Job  ` )

The final state of the job.

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
