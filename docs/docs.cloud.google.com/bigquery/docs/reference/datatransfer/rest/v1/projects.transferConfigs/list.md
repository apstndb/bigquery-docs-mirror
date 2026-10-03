---
name: documents/docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.transferConfigs/list
uri: https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.transferConfigs/list
title: 'Method: transferConfigs.list'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [HTTP request](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.transferConfigs/list#body.HTTP_TEMPLATE)
- [Path parameters](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.transferConfigs/list#body.PATH_PARAMETERS)
- [Query parameters](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.transferConfigs/list#body.QUERY_PARAMETERS)
- [Request body](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.transferConfigs/list#body.request_body)
- [Response body](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.transferConfigs/list#body.response_body)
- [Authorization scopes](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.transferConfigs/list#body.aspect)
- [Try it!](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.transferConfigs/list#try-it)

**Full name** : projects.transferConfigs.list

Returns information about all transfer configs owned by a project in the specified location.

### HTTP request

Choose an endpoint:

global asia-south1 asia-south2 europe-west1 europe-west2 europe-west3 europe-west4 europe-west6 europe-west8 europe-west9 me-central2 northamerica-northeast1 northamerica-northeast2 us-central1 us-central2 us-east1 us-east4 us-east5 us-east7 us-south1 us-west1 us-west2 us-west3 us-west4 us-west8

  
`GET https://bigquerydatatransfer.googleapis.com/v1/{parent=projects/*}/transferConfigs`

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
<td><code>parent</code></td>
<td><p><code>string</code></p>
<p>Required. The BigQuery project id for which transfer configs should be returned. If you are using the regionless method, the location must be <code>US</code> and <code>parent</code> should be in the following form:</p>
<ul>
<li>`projects/{projectId}</li>
</ul>
<p>If you are using the regionalized method, <code>parent</code> should be in the following form:</p>
<ul>
<li><code>projects/{projectId}/locations/{locationId}</code></li>
</ul>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>bigquery.transfers.get</code></li>
</ul></td>
</tr>
</tbody>
</table>

### Query parameters

| Parameters        |                                                                                                                                                                                                                                                                                      |
|-------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `dataSourceIds[]` | `string` When specified, only configurations of requested data sources are returned.                                                                                                                                                                                                 |
| `pageToken`       | `string` Pagination token, which can be used to request a specific page of `ListTransfersRequest` list results. For multiple-page results, `ListTransfersResponse` outputs a `next_page` token, which can be used as the `pageToken` value to request the next page of list results. |
| `pageSize`        | `integer` Page size. The default page size is the maximum value of 1000 results.                                                                                                                                                                                                     |

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of [`ListTransferConfigsResponse`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/ListTransferConfigsResponse) .

### Authorization scopes

Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
