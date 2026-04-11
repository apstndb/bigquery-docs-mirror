  - [HTTP request](https://docs.cloud.google.com/bigquery/docs/reference/bigquerydatapolicy/rest/v2/projects.locations.dataPolicies/create#body.HTTP_TEMPLATE)
  - [Path parameters](https://docs.cloud.google.com/bigquery/docs/reference/bigquerydatapolicy/rest/v2/projects.locations.dataPolicies/create#body.PATH_PARAMETERS)
  - [Request body](https://docs.cloud.google.com/bigquery/docs/reference/bigquerydatapolicy/rest/v2/projects.locations.dataPolicies/create#body.request_body)
      - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/bigquerydatapolicy/rest/v2/projects.locations.dataPolicies/create#body.request_body.SCHEMA_REPRESENTATION)
  - [Response body](https://docs.cloud.google.com/bigquery/docs/reference/bigquerydatapolicy/rest/v2/projects.locations.dataPolicies/create#body.response_body)
  - [Authorization scopes](https://docs.cloud.google.com/bigquery/docs/reference/bigquerydatapolicy/rest/v2/projects.locations.dataPolicies/create#body.aspect)
  - [IAM Permissions](https://docs.cloud.google.com/bigquery/docs/reference/bigquerydatapolicy/rest/v2/projects.locations.dataPolicies/create#body.aspect_1)
  - [Try it\!](https://docs.cloud.google.com/bigquery/docs/reference/bigquerydatapolicy/rest/v2/projects.locations.dataPolicies/create#try-it)

Creates a new data policy under a project with the given `dataPolicyId` (used as the display name), and data policy type.

### HTTP request

`POST https://bigquerydatapolicy.googleapis.com/v2/{parent=projects/*/locations/*}/dataPolicies`

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`parent`

`string`

Required. Resource name of the project that the data policy will belong to. The format is `projects/{projectNumber}/locations/{locationId}` .

### Request body

The request body contains data with the following structure:

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;dataPolicyId&quot;: string,&quot;dataPolicy&quot;: {object (DataPolicy)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`dataPolicyId`

`string`

Required. User-assigned (human readable) ID of the data policy that needs to be unique within a project. Used as {dataPolicyId} in part of the resource name.

`dataPolicy`

` object ( DataPolicy  ` )

Required. The data policy to create. The `name` field does not need to be provided for the data policy creation.

### Response body

If successful, the response body contains a newly created instance of `  DataPolicy  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `https://www.googleapis.com/auth/bigquery`
  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

### IAM Permissions

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `routine` resource:

  - `bigquery.routines.get`

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `parent` resource:

  - `bigquery.dataPolicies.create`

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .
