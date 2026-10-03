---
name: documents/docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs/patch
uri: https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs/patch
title: 'Method: transferConfigs.patch'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [HTTP request](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs/patch#body.HTTP_TEMPLATE)
- [Path parameters](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs/patch#body.PATH_PARAMETERS)
- [Query parameters](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs/patch#body.QUERY_PARAMETERS)
- [Request body](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs/patch#body.request_body)
- [Response body](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs/patch#body.response_body)
- [Authorization scopes](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs/patch#body.aspect)
- [Try it!](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs/patch#try-it)

**Full name** : projects.locations.transferConfigs.patch

Updates a data transfer configuration. All fields must be set, even if they are not updated.

### HTTP request

Choose an endpoint:

global asia-south1 asia-south2 europe-west1 europe-west2 europe-west3 europe-west4 europe-west6 europe-west8 europe-west9 me-central2 northamerica-northeast1 northamerica-northeast2 us-central1 us-central2 us-east1 us-east4 us-east5 us-east7 us-south1 us-west1 us-west2 us-west3 us-west4 us-west8

  
`PATCH https://bigquerydatatransfer.googleapis.com/v1/{transferConfig.name=projects/*/locations/*/transferConfigs/*}`

The URLs use [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

| Parameters            |                                                                                                                                                                                                                                                                                                                                                                              |
|-----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `transferConfig.name` | `string` Identifier. The resource name of the transfer config. Transfer config names have the form either `projects/{projectId}/locations/{region}/transferConfigs/{configId}` or `projects/{projectId}/transferConfigs/{configId}` , where `configId` is usually a UUID, even though it is not guaranteed or required. The name is ignored when creating a transfer config. |

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
<td><code>authorizationCode </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>string</code></p>
<p>Deprecated: Authorization code was required when <code>transferConfig.dataSourceId</code> is 'youtube_channel' but it is no longer used in any data sources. Use <code>versionInfo</code> instead.</p>
<p>Optional OAuth2 authorization code to use with this transfer configuration. This is required only if <code>transferConfig.dataSourceId</code> is 'youtube_channel' and new credentials are needed, as indicated by <code>dataSources.checkValidCreds</code> . In order to obtain authorizationCode, make a request to the following URL:</p>
<pre data-fenced=""><code>https://bigquery.cloud.google.com/datatransfer/oauthz/auth?redirect_uri=urn:ietf:wg:oauth:2.0:oob&amp;response_type=authorization_code&amp;client_id=clientId&amp;scope=data_source_scopes</code></pre>
<ul>
<li>The <var translate="no"> clientId </var> is the OAuth clientId of the data source as returned by ListDataSources method.</li>
<li><var translate="no"> data_source_scopes </var> are the scopes returned by ListDataSources method.</li>
</ul>
<p>Note that this should not be set when <code>serviceAccountName</code> is used to update the transfer config.</p></td>
</tr>
<tr class="even">
<td><code>updateMask</code></td>
<td><p><code>string ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#field-mask"><code>FieldMask</code></a><code> format)</code></p>
<p>Required. Required list of fields to be updated in this request.</p>
<p>This is a comma-separated list of fully qualified names of fields. Example: <code>"user.displayName,photo"</code> .</p></td>
</tr>
<tr class="odd">
<td><code>versionInfo</code></td>
<td><p><code>string</code></p>
<p>Optional version info. This parameter replaces <code>authorizationCode</code> which is no longer used in any data sources. This is required only if <code>transferConfig.dataSourceId</code> is 'youtube_channel' <em>or</em> new credentials are needed, as indicated by <code>dataSources.checkValidCreds</code> . In order to obtain version info, make a request to the following URL:</p>
<pre data-fenced=""><code>https://bigquery.cloud.google.com/datatransfer/oauthz/auth?redirect_uri=urn:ietf:wg:oauth:2.0:oob&amp;response_type=version_info&amp;client_id=clientId&amp;scope=data_source_scopes</code></pre>
<ul>
<li>The <var translate="no"> clientId </var> is the OAuth clientId of the data source as returned by ListDataSources method.</li>
<li><var translate="no"> data_source_scopes </var> are the scopes returned by ListDataSources method.</li>
</ul>
<p>Note that this should not be set when <code>serviceAccountName</code> is used to update the transfer config.</p></td>
</tr>
<tr class="even">
<td><code>serviceAccountName</code></td>
<td><p><code>string</code></p>
<p>Optional service account email. If this field is set, the transfer config will be created with this service account's credentials. It requires that the requesting user calling this API has permissions to act as this service account.</p>
<p>Note that not all data sources support service account credentials when creating a transfer config. For the latest list of data sources, read about <a href="https://cloud.google.com/bigquery-transfer/docs/use-service-accounts">using service accounts</a> .</p></td>
</tr>
</tbody>
</table>

### Request body

The request body contains an instance of [`TransferConfig`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs#TransferConfig) .

### Response body

If successful, the response body contains an instance of [`TransferConfig`](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs#TransferConfig) .

### Authorization scopes

Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
