---
name: documents/docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations/unenrollDataSources
uri: https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations/unenrollDataSources
title: 'Method: locations.unenrollDataSources'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [HTTP request](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations/unenrollDataSources#body.HTTP_TEMPLATE)
- [Path parameters](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations/unenrollDataSources#body.PATH_PARAMETERS)
- [Request body](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations/unenrollDataSources#body.request_body)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations/unenrollDataSources#body.request_body.SCHEMA_REPRESENTATION)
- [Response body](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations/unenrollDataSources#body.response_body)
- [Authorization scopes](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations/unenrollDataSources#body.aspect)
- [Try it!](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations/unenrollDataSources#try-it)

**Full name** : projects.locations.unenrollDataSources

Unenroll data sources in a user project. This allows users to remove transfer configurations for these data sources. They will no longer appear in the ListDataSources RPC and will also no longer appear in the [BigQuery UI](https://console.cloud.google.com/bigquery) . Data transfers configurations of unenrolled data sources will not be scheduled.

### HTTP request

Choose an endpoint:

global asia-south1 asia-south2 europe-west1 europe-west2 europe-west3 europe-west4 europe-west6 europe-west8 europe-west9 me-central2 northamerica-northeast1 northamerica-northeast2 us-central1 us-central2 us-east1 us-east4 us-east5 us-east7 us-south1 us-west1 us-west2 us-west3 us-west4 us-west8

  
`POST https://bigquerydatatransfer.googleapis.com/v1/{name=projects/*/locations/*}:unenrollDataSources`

The URLs use [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Parameters</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. The name of the project resource in the form: <code>projects/{projectId}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>resourcemanager.projects.update</code></li>
</ul></td>
</tr>
</tbody>
</table>

### Request body

The request body contains data with the following structure:

**JSON representation**

```
{
  "dataSourceIds": [
    string
  ]
}
```

| Fields            |                                                                                                   |
|-------------------|---------------------------------------------------------------------------------------------------|
| `dataSourceIds[]` | `string` Data sources that are unenrolled. It is required to provide at least one data source id. |

### Response body

If successful, the response body is an empty JSON object.

### Authorization scopes

Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
