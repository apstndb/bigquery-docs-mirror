---
name: documents/docs.cloud.google.com/bigquery/docs/reference/bigquerydatapolicy/rest/v2beta1/projects.locations.dataPolicies/addGrantees
uri: https://docs.cloud.google.com/bigquery/docs/reference/bigquerydatapolicy/rest/v2beta1/projects.locations.dataPolicies/addGrantees
title: 'Method: projects.locations.dataPolicies.addGrantees'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [HTTP request](https://docs.cloud.google.com/bigquery/docs/reference/bigquerydatapolicy/rest/v2beta1/projects.locations.dataPolicies/addGrantees#body.HTTP_TEMPLATE)
- [Path parameters](https://docs.cloud.google.com/bigquery/docs/reference/bigquerydatapolicy/rest/v2beta1/projects.locations.dataPolicies/addGrantees#body.PATH_PARAMETERS)
- [Request body](https://docs.cloud.google.com/bigquery/docs/reference/bigquerydatapolicy/rest/v2beta1/projects.locations.dataPolicies/addGrantees#body.request_body)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/bigquerydatapolicy/rest/v2beta1/projects.locations.dataPolicies/addGrantees#body.request_body.SCHEMA_REPRESENTATION)
- [Response body](https://docs.cloud.google.com/bigquery/docs/reference/bigquerydatapolicy/rest/v2beta1/projects.locations.dataPolicies/addGrantees#body.response_body)
- [Authorization scopes](https://docs.cloud.google.com/bigquery/docs/reference/bigquerydatapolicy/rest/v2beta1/projects.locations.dataPolicies/addGrantees#body.aspect)
- [IAM Permissions](https://docs.cloud.google.com/bigquery/docs/reference/bigquerydatapolicy/rest/v2beta1/projects.locations.dataPolicies/addGrantees#body.aspect_1)
- [Try it!](https://docs.cloud.google.com/bigquery/docs/reference/bigquerydatapolicy/rest/v2beta1/projects.locations.dataPolicies/addGrantees#try-it)

Adds new grantees to a data policy. The new grantees will be added to the existing grantees. If the request contains a duplicate grantee, the grantee will be ignored. If the request contains a grantee that already exists, the grantee will be ignored.

### HTTP request

`POST https://bigquerydatapolicy.googleapis.com/v2beta1/{dataPolicy=projects/*/locations/*/dataPolicies/*}:addGrantees`

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

| Parameters   |                                                                                                                                                        |
|--------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| `dataPolicy` | `string` Required. Resource name of this data policy, in the format of `projects/{projectNumber}/locations/{locationId}/dataPolicies/{dataPolicyId}` . |

### Request body

The request body contains data with the following structure:

**JSON representation**

```
{
  "grantees": [
    string
  ]
}
```

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>grantees[]</code></td>
<td><p><code>string</code></p>
<p>Required. IAM principal that should be granted Fine Grained Access to the underlying data goverened by the data policy. The target data policy is determined by the <code>dataPolicy</code> field.</p>
<p>Uses the <a href="https://cloud.google.com/iam/docs/principal-identifiers#v2">IAM V2 principal syntax</a> . Supported principal types:</p>
<ul>
<li>User</li>
<li>Group</li>
<li>Service account</li>
</ul></td>
</tr>
</tbody>
</table>

### Response body

If successful, the response body contains an instance of [`DataPolicy`](https://docs.cloud.google.com/bigquery/docs/reference/bigquerydatapolicy/rest/v2beta1/projects.locations.dataPolicies#DataPolicy) .

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

### IAM Permissions

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `dataPolicy` resource:

- `bigquery.dataPolicies.update`

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .
