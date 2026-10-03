---
name: documents/docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.subscriptions/list
uri: https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.subscriptions/list
title: 'Method: projects.locations.subscriptions.list'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [HTTP request](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.subscriptions/list#body.HTTP_TEMPLATE)
- [Path parameters](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.subscriptions/list#body.PATH_PARAMETERS)
- [Query parameters](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.subscriptions/list#body.QUERY_PARAMETERS)
- [Request body](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.subscriptions/list#body.request_body)
- [Response body](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.subscriptions/list#body.response_body)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.subscriptions/list#body.ListSubscriptionsResponse.SCHEMA_REPRESENTATION)
- [Authorization scopes](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.subscriptions/list#body.aspect)
- [IAM Permissions](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.subscriptions/list#body.aspect_1)
- [Try it!](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.subscriptions/list#try-it)

Lists all subscriptions in a given project and location.

### HTTP request

`GET https://analyticshub.googleapis.com/v1/{parent=projects/*/locations/*}/subscriptions`

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

| Parameters |                                                                                                       |
|------------|-------------------------------------------------------------------------------------------------------|
| `parent`   | `string` Required. The parent resource path of the subscription. e.g. projects/myproject/locations/us |

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
<td><code>filter</code></td>
<td><p><code>string</code></p>
<p>An expression for filtering the results of the request. Eligible fields for filtering are:</p>
<ul>
<li><code>listing</code></li>
<li><code>dataExchange</code></li>
</ul>
<p>Alternatively, a literal wrapped in double quotes may be provided. This will be checked for an exact match against both fields above.</p>
<p>In all cases, the full Data Exchange or Listing resource name must be provided. Some example of using filters:</p>
<ul>
<li>dataExchange="projects/myproject/locations/us/dataExchanges/123"</li>
<li>listing="projects/123/locations/us/dataExchanges/456/listings/789"</li>
<li>"projects/myproject/locations/us/dataExchanges/123"</li>
</ul></td>
</tr>
<tr class="even">
<td><code>pageSize</code></td>
<td><p><code>integer</code></p>
<p>The maximum number of results to return in a single response page.</p></td>
</tr>
<tr class="odd">
<td><code>pageToken</code></td>
<td><p><code>string</code></p>
<p>Page token, returned by a previous call.</p></td>
</tr>
</tbody>
</table>

### Request body

The request body must be empty.

### Response body

Message for response to the listing of subscriptions.

If successful, the response body contains data with the following structure:

**JSON representation**

```
{
  "subscriptions": [
    {
      object (Subscription)
    }
  ],
  "nextPageToken": string
}
```

| Fields            |                                                                                                                                                                |
|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `subscriptions[]` | `object ( `[`Subscription`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/Shared.Types/Subscription)` )` The list of subscriptions. |
| `nextPageToken`   | `string` Next page token.                                                                                                                                      |

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

### IAM Permissions

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `parent` resource:

- `analyticshub.subscriptions.list`

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .
