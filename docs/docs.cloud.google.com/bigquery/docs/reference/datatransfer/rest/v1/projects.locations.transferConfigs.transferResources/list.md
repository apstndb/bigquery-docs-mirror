---
name: documents/docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.transferResources/list
uri: https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.transferResources/list
title: 'Method: transferResources.list'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [HTTP request](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.transferResources/list#body.HTTP_TEMPLATE)
- [Path parameters](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.transferResources/list#body.PATH_PARAMETERS)
- [Query parameters](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.transferResources/list#body.QUERY_PARAMETERS)
- [Request body](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.transferResources/list#body.request_body)
- [Response body](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.transferResources/list#body.response_body)
- [Authorization scopes](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.transferResources/list#body.aspect)
- [Try it!](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.transferResources/list#try-it)

**Full name** : projects.locations.transferConfigs.transferResources.list

Returns information about transfer resources.

### HTTP request

Choose an endpoint:

global asia-south1 asia-south2 europe-west1 europe-west2 europe-west3 europe-west4 europe-west6 europe-west8 europe-west9 me-central2 northamerica-northeast1 northamerica-northeast2 us-central1 us-central2 us-east1 us-east4 us-east5 us-east7 us-south1 us-west1 us-west2 us-west3 us-west4 us-west8

  
`GET https://bigquerydatatransfer.googleapis.com/v1/{parent=projects/*/locations/*/transferConfigs/*}/transferResources`

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
<p>Required. Name of transfer configuration for which transfer resources should be retrieved. The name should be in one of the following forms:</p>
<ul>
<li><code>projects/{project}/transferConfigs/{transferConfig}</code></li>
<li><code>projects/{project}/locations/{locationId}/transferConfigs/{transferConfig}</code></li>
</ul>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>bigquery.transfers.get</code></li>
</ul></td>
</tr>
</tbody>
</table>

### Query parameters

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
<td><code>pageSize</code></td>
<td><p><code>integer</code></p>
<p>Optional. The maximum number of transfer resources to return. The maximum value is 1000; values above 1000 will be coerced to 1000. The default page size is the maximum value of 1000 results.</p></td>
</tr>
<tr class="even">
<td><code>pageToken</code></td>
<td><p><code>string</code></p>
<p>Optional. A page token, received from a previous <code>transferResources.list</code> call. Provide this to retrieve the subsequent page. When paginating, all other parameters provided to <code>transferResources.list</code> must match the call that provided the page token.</p></td>
</tr>
<tr class="odd">
<td><code>filter</code></td>
<td><p><code>string</code></p>
<p>Optional. Filter for the transfer resources. Currently supported filters include:</p>
<ul>
<li>Resource name: <code>name</code> - Wildcard supported</li>
<li>Resource type: <code>type</code></li>
<li>Resource destination: <code>destination</code></li>
<li>Latest resource state: <code>latest_status_detail.state</code></li>
<li>Last update time: <code>update_time</code> - RFC-3339 format</li>
<li>Parent table name: <code>hierarchy_detail.partition_detail.table</code></li>
</ul>
<p>Multiple filters can be applied using the <code>AND/OR</code> operator.</p>
<p>Examples:</p>
<ul>
<li><code>name="*123" AND (type="TABLE" OR latest_status_detail.state="SUCCEEDED")</code></li>
<li><code>update_time &gt;= "2012-04-21T11:30:00-04:00"</code></li>
<li><code>hierarchy_detail.partition_detail.table = "table1"</code></li>
</ul></td>
</tr>
</tbody>
</table>

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of [`ListTransferResourcesResponse`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/ListTransferResourcesResponse) .

### Authorization scopes

Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
