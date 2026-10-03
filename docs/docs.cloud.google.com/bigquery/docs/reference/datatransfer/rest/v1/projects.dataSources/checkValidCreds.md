---
name: documents/docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.dataSources/checkValidCreds
uri: https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.dataSources/checkValidCreds
title: 'Method: dataSources.checkValidCreds'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [HTTP request](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.dataSources/checkValidCreds#body.HTTP_TEMPLATE)
- [Path parameters](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.dataSources/checkValidCreds#body.PATH_PARAMETERS)
- [Request body](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.dataSources/checkValidCreds#body.request_body)
- [Response body](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.dataSources/checkValidCreds#body.response_body)
- [Authorization scopes](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.dataSources/checkValidCreds#body.aspect)
- [Try it!](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.dataSources/checkValidCreds#try-it)

**Full name** : projects.dataSources.checkValidCreds

Returns true if valid credentials exist for the given data source and requesting user.

### HTTP request

Choose an endpoint:

global asia-south1 asia-south2 europe-west1 europe-west2 europe-west3 europe-west4 europe-west6 europe-west8 europe-west9 me-central2 northamerica-northeast1 northamerica-northeast2 us-central1 us-central2 us-east1 us-east4 us-east5 us-east7 us-south1 us-west1 us-west2 us-west3 us-west4 us-west8

  
`POST https://bigquerydatatransfer.googleapis.com/v1/{name=projects/*/dataSources/*}:checkValidCreds`

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
<p>Required. The name of the data source. If you are using the regionless method, the location must be <code>US</code> and the name should be in the following form:</p>
<ul>
<li><code>projects/{projectId}/dataSources/{dataSourceId}</code></li>
</ul>
<p>If you are using the regionalized method, the name should be in the following form:</p>
<ul>
<li><code>projects/{projectId}/locations/{locationId}/dataSources/{dataSourceId}</code></li>
</ul>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>bigquery.transfers.get</code></li>
</ul></td>
</tr>
</tbody>
</table>

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of [`CheckValidCredsResponse`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/CheckValidCredsResponse) .

### Authorization scopes

Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
