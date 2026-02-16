  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Query parameters](#body.QUERY_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
  - [Authorization scopes](#body.aspect)
  - [Try it\!](#try-it)

Requests the deletion of the metadata of a job. This call returns when the job's metadata is deleted.

### HTTP request

`  DELETE https://bigquery.googleapis.com/bigquery/v2/projects/{projectId}/jobs/{jobId}/delete  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  projectId  `

`  string  `

Required. Project ID of the job for which metadata is to be deleted.

`  jobId  `

`  string  `

Required. Job ID of the job for which metadata is to be deleted. If this is a parent job which has child jobs, the metadata from all child jobs will be deleted as well. Direct deletion of the metadata of child jobs is not allowed.

### Query parameters

Parameters

`  location  `

`  string  `

The geographic location of the job. Required.

For more information, see how to [specify locations](https://cloud.google.com/bigquery/docs/locations#specify_locations) .

### Request body

The request body must be empty.

### Response body

If successful, the response body is an empty JSON object.

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
