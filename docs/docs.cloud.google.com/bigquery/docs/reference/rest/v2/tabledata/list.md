  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Query parameters](#body.QUERY_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
      - [JSON representation](#body.TableDataList.SCHEMA_REPRESENTATION)
  - [Authorization scopes](#body.aspect)
  - [Try it\!](#try-it)

tabledata.list the content of a table in rows.

### HTTP request

`  GET https://bigquery.googleapis.com/bigquery/v2/projects/{projectId}/datasets/{datasetId}/tables/{tableId}/data  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  projectId  `

`  string  `

Required. Project id of the table to list.

`  datasetId  `

`  string  `

Required. Dataset id of the table to list.

`  tableId  `

`  string  `

Required. Table id of the table to list.

### Query parameters

Parameters

`  startIndex  `

`  string  `

Start row index of the table.

`  maxResults  `

`  integer ( uint32 format)  `

Row limit of the table.

`  pageToken  `

`  string  `

To retrieve the next page of table data, set this field to the string provided in the pageToken field of the response body from your previous call to tabledata.list.

`  selectedFields  `

`  string  `

Subset of fields to return, supports select into sub fields. Example: selectedFields = "a,e.d.f";

`  formatOptions  `

`  object ( DataFormatOptions  ` )

Output timestamp field value in usec int64 instead of double. Output format adjustments.

### Request body

The request body must be empty.

### Response body

The response of a tabledata.list request.

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
  &quot;etag&quot;: string,
  &quot;totalRows&quot;: string,
  &quot;pageToken&quot;: string,
  &quot;rows&quot;: [
    {
      object
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  kind  `

`  string  `

Will be set to "bigquery\#tableDataList".

`  etag  `

`  string  `

Etag to the response.

`  totalRows  `

`  string  `

Total rows of the entire table. In order to show default value "0", we have to present it as string.

`  pageToken  `

`  string  `

When this field is non-empty, it indicates that additional results are available. To request the next page of data, set the pageToken field of your next tabledata.list call to the string returned in this field.

`  rows[]  `

`  object ( Struct  ` format)

Repeated rows as result. The REST-based representation of this data leverages a series of JSON f,v objects for indicating fields and values.

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/bigquery  `
  - `  https://www.googleapis.com/auth/cloud-platform  `
  - `  https://www.googleapis.com/auth/bigquery.readonly  `
  - `  https://www.googleapis.com/auth/cloud-platform.read-only  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
