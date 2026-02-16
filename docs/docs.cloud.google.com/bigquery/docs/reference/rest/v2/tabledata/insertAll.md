  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Request body](#body.request_body)
      - [JSON representation](#body.request_body.SCHEMA_REPRESENTATION)
  - [Response body](#body.response_body)
      - [JSON representation](#body.TableDataInsertAllResponse.SCHEMA_REPRESENTATION)
  - [Authorization scopes](#body.aspect)
  - [Try it\!](#try-it)

Streams data into BigQuery one record at a time without needing to run a load job.

### HTTP request

`  POST https://bigquery.googleapis.com/bigquery/v2/projects/{projectId}/datasets/{datasetId}/tables/{tableId}/insertAll  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  projectId  `

`  string  `

Required. Project ID of the destination.

`  datasetId  `

`  string  `

Required. Dataset ID of the destination.

`  tableId  `

`  string  `

Required. Table ID of the destination.

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
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;kind&quot;: string,
  &quot;skipInvalidRows&quot;: boolean,
  &quot;ignoreUnknownValues&quot;: boolean,
  &quot;templateSuffix&quot;: string,
  &quot;rows&quot;: [
    {
      &quot;insertId&quot;: string,
      &quot;json&quot;: {
        object
      }
    }
  ],
  &quot;traceId&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  kind  `

`  string  `

Optional. The resource type of the response. The value is not checked at the backend. Historically, it has been set to "bigquery\#tableDataInsertAllRequest" but you are not required to set it.

`  skipInvalidRows  `

`  boolean  `

Optional. Insert all valid rows of a request, even if invalid rows exist. The default value is false, which causes the entire request to fail if any invalid rows exist.

`  ignoreUnknownValues  `

`  boolean  `

Optional. Accept rows that contain values that do not match the schema. The unknown values are ignored. Default is false, which treats unknown values as errors.

`  templateSuffix  `

`  string  `

Optional. If specified, treats the destination table as a base template, and inserts the rows into an instance table named "{destination}{templateSuffix}". BigQuery will manage creation of the instance table, using the schema of the base template table.

See <https://cloud.google.com/bigquery/streaming-data-into-bigquery#template-tables> for considerations when working with templates tables.

`  rows[]  `

`  object  `

`  rows[].insertId  `

`  string  `

Insertion ID for best-effort deduplication. This feature is not recommended, and users seeking stronger insertion semantics are encouraged to use other mechanisms such as the BigQuery Write API.

`  rows[].json  `

`  object ( Struct  ` format)

Data for a single row.

`  traceId  `

`  string  `

Optional. Unique request trace id. Used for debugging purposes only. It is case-sensitive, limited to up to 36 ASCII characters. A UUID is recommended.

### Response body

Describes the format of a streaming insert response.

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
  &quot;insertErrors&quot;: [
    {
      &quot;index&quot;: integer,
      &quot;errors&quot;: [
        {
          object (ErrorProto)
        }
      ]
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  kind  `

`  string  `

Returns "bigquery\#tableDataInsertAllResponse".

`  insertErrors[]  `

`  object  `

Describes specific errors encountered while processing the request.

`  insertErrors[].index  `

`  integer ( uint32 format)  `

The index of the row that error applies to.

`  insertErrors[].errors[]  `

`  object ( ErrorProto  ` )

Error information for the row indicated by the index property.

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `
  - `  https://www.googleapis.com/auth/bigquery.insertdata  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
