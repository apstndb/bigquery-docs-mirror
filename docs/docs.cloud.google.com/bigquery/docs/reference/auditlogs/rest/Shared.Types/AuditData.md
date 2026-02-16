  - [JSON representation](#SCHEMA_REPRESENTATION)
  - [TableInsertRequest](#TableInsertRequest)
      - [JSON representation](#TableInsertRequest.SCHEMA_REPRESENTATION)
  - [Table](#Table)
      - [JSON representation](#Table.SCHEMA_REPRESENTATION)
  - [TableName](#TableName)
      - [JSON representation](#TableName.SCHEMA_REPRESENTATION)
  - [TableInfo](#TableInfo)
      - [JSON representation](#TableInfo.SCHEMA_REPRESENTATION)
  - [TableViewDefinition](#TableViewDefinition)
      - [JSON representation](#TableViewDefinition.SCHEMA_REPRESENTATION)
  - [EncryptionInfo](#EncryptionInfo)
      - [JSON representation](#EncryptionInfo.SCHEMA_REPRESENTATION)
  - [TableUpdateRequest](#TableUpdateRequest)
      - [JSON representation](#TableUpdateRequest.SCHEMA_REPRESENTATION)
  - [DatasetListRequest](#DatasetListRequest)
      - [JSON representation](#DatasetListRequest.SCHEMA_REPRESENTATION)
  - [DatasetInsertRequest](#DatasetInsertRequest)
      - [JSON representation](#DatasetInsertRequest.SCHEMA_REPRESENTATION)
  - [Dataset](#Dataset)
      - [JSON representation](#Dataset.SCHEMA_REPRESENTATION)
  - [DatasetName](#DatasetName)
      - [JSON representation](#DatasetName.SCHEMA_REPRESENTATION)
  - [DatasetInfo](#DatasetInfo)
      - [JSON representation](#DatasetInfo.SCHEMA_REPRESENTATION)
  - [BigQueryAcl](#BigQueryAcl)
      - [JSON representation](#BigQueryAcl.SCHEMA_REPRESENTATION)
  - [BigQueryAcl.Entry](#BigQueryAcl.Entry)
      - [JSON representation](#BigQueryAcl.Entry.SCHEMA_REPRESENTATION)
  - [DatasetUpdateRequest](#DatasetUpdateRequest)
      - [JSON representation](#DatasetUpdateRequest.SCHEMA_REPRESENTATION)
  - [JobInsertRequest](#JobInsertRequest)
      - [JSON representation](#JobInsertRequest.SCHEMA_REPRESENTATION)
  - [Job](#Job)
      - [JSON representation](#Job.SCHEMA_REPRESENTATION)
  - [JobName](#JobName)
      - [JSON representation](#JobName.SCHEMA_REPRESENTATION)
  - [JobConfiguration](#JobConfiguration)
      - [JSON representation](#JobConfiguration.SCHEMA_REPRESENTATION)
  - [JobConfiguration.Query](#JobConfiguration.Query)
      - [JSON representation](#JobConfiguration.Query.SCHEMA_REPRESENTATION)
  - [TableDefinition](#TableDefinition)
      - [JSON representation](#TableDefinition.SCHEMA_REPRESENTATION)
  - [JobConfiguration.Load](#JobConfiguration.Load)
      - [JSON representation](#JobConfiguration.Load.SCHEMA_REPRESENTATION)
  - [JobConfiguration.Extract](#JobConfiguration.Extract)
      - [JSON representation](#JobConfiguration.Extract.SCHEMA_REPRESENTATION)
  - [JobConfiguration.TableCopy](#JobConfiguration.TableCopy)
      - [JSON representation](#JobConfiguration.TableCopy.SCHEMA_REPRESENTATION)
  - [JobStatus](#JobStatus)
      - [JSON representation](#JobStatus.SCHEMA_REPRESENTATION)
  - [JobStatistics](#JobStatistics)
      - [JSON representation](#JobStatistics.SCHEMA_REPRESENTATION)
  - [JobStatistics.ReservationResourceUsage](#JobStatistics.ReservationResourceUsage)
      - [JSON representation](#JobStatistics.ReservationResourceUsage.SCHEMA_REPRESENTATION)
  - [JobQueryRequest](#JobQueryRequest)
      - [JSON representation](#JobQueryRequest.SCHEMA_REPRESENTATION)
  - [JobGetQueryResultsRequest](#JobGetQueryResultsRequest)
      - [JSON representation](#JobGetQueryResultsRequest.SCHEMA_REPRESENTATION)
  - [TableDataListRequest](#TableDataListRequest)
      - [JSON representation](#TableDataListRequest.SCHEMA_REPRESENTATION)
  - [SetIamPolicyRequest](#SetIamPolicyRequest)
      - [JSON representation](#SetIamPolicyRequest.SCHEMA_REPRESENTATION)
  - [TableInsertResponse](#TableInsertResponse)
      - [JSON representation](#TableInsertResponse.SCHEMA_REPRESENTATION)
  - [TableUpdateResponse](#TableUpdateResponse)
      - [JSON representation](#TableUpdateResponse.SCHEMA_REPRESENTATION)
  - [DatasetInsertResponse](#DatasetInsertResponse)
      - [JSON representation](#DatasetInsertResponse.SCHEMA_REPRESENTATION)
  - [DatasetUpdateResponse](#DatasetUpdateResponse)
      - [JSON representation](#DatasetUpdateResponse.SCHEMA_REPRESENTATION)
  - [JobInsertResponse](#JobInsertResponse)
      - [JSON representation](#JobInsertResponse.SCHEMA_REPRESENTATION)
  - [JobQueryResponse](#JobQueryResponse)
      - [JSON representation](#JobQueryResponse.SCHEMA_REPRESENTATION)
  - [JobGetQueryResultsResponse](#JobGetQueryResultsResponse)
      - [JSON representation](#JobGetQueryResultsResponse.SCHEMA_REPRESENTATION)
  - [JobQueryDoneResponse](#JobQueryDoneResponse)
      - [JSON representation](#JobQueryDoneResponse.SCHEMA_REPRESENTATION)
  - [JobCompletedEvent](#JobCompletedEvent)
      - [JSON representation](#JobCompletedEvent.SCHEMA_REPRESENTATION)
  - [TableDataReadEvent](#TableDataReadEvent)
      - [JSON representation](#TableDataReadEvent.SCHEMA_REPRESENTATION)

BigQuery AuditData represents the older AuditData.serviceData log messages.

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
  &quot;jobCompletedEvent&quot;: {
    object (JobCompletedEvent)
  },
  &quot;tableDataReadEvents&quot;: [
    {
      object (TableDataReadEvent)
    }
  ],

  // Union field request can be only one of the following:
  &quot;tableInsertRequest&quot;: {
    object (TableInsertRequest)
  },
  &quot;tableUpdateRequest&quot;: {
    object (TableUpdateRequest)
  },
  &quot;datasetListRequest&quot;: {
    object (DatasetListRequest)
  },
  &quot;datasetInsertRequest&quot;: {
    object (DatasetInsertRequest)
  },
  &quot;datasetUpdateRequest&quot;: {
    object (DatasetUpdateRequest)
  },
  &quot;jobInsertRequest&quot;: {
    object (JobInsertRequest)
  },
  &quot;jobQueryRequest&quot;: {
    object (JobQueryRequest)
  },
  &quot;jobGetQueryResultsRequest&quot;: {
    object (JobGetQueryResultsRequest)
  },
  &quot;tableDataListRequest&quot;: {
    object (TableDataListRequest)
  },
  &quot;setIamPolicyRequest&quot;: {
    object (SetIamPolicyRequest)
  }
  // End of list of possible types for union field request.

  // Union field response can be only one of the following:
  &quot;tableInsertResponse&quot;: {
    object (TableInsertResponse)
  },
  &quot;tableUpdateResponse&quot;: {
    object (TableUpdateResponse)
  },
  &quot;datasetInsertResponse&quot;: {
    object (DatasetInsertResponse)
  },
  &quot;datasetUpdateResponse&quot;: {
    object (DatasetUpdateResponse)
  },
  &quot;jobInsertResponse&quot;: {
    object (JobInsertResponse)
  },
  &quot;jobQueryResponse&quot;: {
    object (JobQueryResponse)
  },
  &quot;jobGetQueryResultsResponse&quot;: {
    object (JobGetQueryResultsResponse)
  },
  &quot;jobQueryDoneResponse&quot;: {
    object (JobQueryDoneResponse)
  },
  &quot;policyResponse&quot;: {
    object (Policy)
  }
  // End of list of possible types for union field response.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  jobCompletedEvent  `

`  object ( JobCompletedEvent  ` )

A job completion event.

`  tableDataReadEvents[]  `

`  object ( TableDataReadEvent  ` )

Information about the table access events.

Union field `  request  ` . Request data for each BigQuery method. `  request  ` can be only one of the following:

`  tableInsertRequest  `

`  object ( TableInsertRequest  ` )

Table insert request.

`  tableUpdateRequest  `

`  object ( TableUpdateRequest  ` )

Table update request.

`  datasetListRequest  `

`  object ( DatasetListRequest  ` )

Dataset list request.

`  datasetInsertRequest  `

`  object ( DatasetInsertRequest  ` )

Dataset insert request.

`  datasetUpdateRequest  `

`  object ( DatasetUpdateRequest  ` )

Dataset update request.

`  jobInsertRequest  `

`  object ( JobInsertRequest  ` )

Job insert request.

`  jobQueryRequest  `

`  object ( JobQueryRequest  ` )

Job query request.

`  jobGetQueryResultsRequest  `

`  object ( JobGetQueryResultsRequest  ` )

Job get query results request.

`  tableDataListRequest  `

`  object ( TableDataListRequest  ` )

Table data-list request.

`  setIamPolicyRequest  `

`  object ( SetIamPolicyRequest  ` )

Iam policy request.

Union field `  response  ` . Response data for each BigQuery method. `  response  ` can be only one of the following:

`  tableInsertResponse  `

`  object ( TableInsertResponse  ` )

Table insert response.

`  tableUpdateResponse  `

`  object ( TableUpdateResponse  ` )

Table update response.

`  datasetInsertResponse  `

`  object ( DatasetInsertResponse  ` )

Dataset insert response.

`  datasetUpdateResponse  `

`  object ( DatasetUpdateResponse  ` )

Dataset update response.

`  jobInsertResponse  `

`  object ( JobInsertResponse  ` )

Job insert response.

`  jobQueryResponse  `

`  object ( JobQueryResponse  ` )

Job query response.

`  jobGetQueryResultsResponse  `

`  object ( JobGetQueryResultsResponse  ` )

Job get query results response.

`  jobQueryDoneResponse  `

`  object ( JobQueryDoneResponse  ` )

Deprecated: Job query-done response. Use this information for usage analysis.

`  policyResponse  `

`  object ( Policy  ` )

Iam Policy.

## TableInsertRequest

Table insert request.

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
  &quot;resource&quot;: {
    object (Table)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  resource  `

`  object ( Table  ` )

The new table.

## Table

Describes a BigQuery table. See the [Table](/bigquery/docs/reference/v2/tables) API resource for more details on individual fields. Note: `  Table.schema  ` has been deprecated in favor of `  Table.schemaJson  ` . `  Table.schema  ` may continue to be present in your logs during this transition.

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
  &quot;tableName&quot;: {
    object (TableName)
  },
  &quot;info&quot;: {
    object (TableInfo)
  },
  &quot;schemaJson&quot;: string,
  &quot;view&quot;: {
    object (TableViewDefinition)
  },
  &quot;expireTime&quot;: string,
  &quot;createTime&quot;: string,
  &quot;truncateTime&quot;: string,
  &quot;updateTime&quot;: string,
  &quot;encryption&quot;: {
    object (EncryptionInfo)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  tableName  `

`  object ( TableName  ` )

The name of the table.

`  info  `

`  object ( TableInfo  ` )

User-provided metadata for the table.

`  schemaJson  `

`  string  `

A JSON representation of the table's schema.

`  view  `

`  object ( TableViewDefinition  ` )

If present, this is a virtual table defined by a SQL query.

`  expireTime  `

`  string ( Timestamp  ` format)

The expiration date for the table, after which the table is deleted and the storage reclaimed. If not present, the table persists indefinitely.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

`  createTime  `

`  string ( Timestamp  ` format)

The time the table was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

`  truncateTime  `

`  string ( Timestamp  ` format)

The time the table was last truncated by an operation with a `  writeDisposition  ` of `  WRITE_TRUNCATE  ` .

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

`  updateTime  `

`  string ( Timestamp  ` format)

The time the table was last modified.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

`  encryption  `

`  object ( EncryptionInfo  ` )

The table encryption information. Set when non-default encryption is used.

## TableName

The fully-qualified name for a table.

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
  &quot;projectId&quot;: string,
  &quot;datasetId&quot;: string,
  &quot;tableId&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  projectId  `

`  string  `

The project ID.

`  datasetId  `

`  string  `

The dataset ID within the project.

`  tableId  `

`  string  `

The table ID of the table within the dataset.

## TableInfo

User-provided metadata for a table.

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
  &quot;friendlyName&quot;: string,
  &quot;description&quot;: string,
  &quot;labels&quot;: {
    string: string,
    ...
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  friendlyName  `

`  string  `

A short name for the table, such as `  "Analytics Data - Jan 2011"  ` .

`  description  `

`  string  `

A long description, perhaps several paragraphs, describing the table contents in detail.

`  labels  `

`  map (key: string, value: string)  `

Labels provided for the table.

An object containing a list of `  "key": value  ` pairs. Example: `  { "name": "wrench", "mass": "1.3kg", "count": "3" }  ` .

## TableViewDefinition

Describes a virtual table defined by a SQL query.

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
  &quot;query&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  query  `

`  string  `

SQL query defining the view.

## EncryptionInfo

Describes encryption properties for a table or a job

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
  &quot;kmsKeyName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  kmsKeyName  `

`  string  `

unique identifier for cloud kms key

## TableUpdateRequest

Table update request.

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
  &quot;resource&quot;: {
    object (Table)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  resource  `

`  object ( Table  ` )

The table to be updated.

## DatasetListRequest

Dataset list request.

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
  &quot;listAll&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  listAll  `

`  boolean  `

Whether to list all datasets, including hidden ones.

## DatasetInsertRequest

Dataset insert request.

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
  &quot;resource&quot;: {
    object (Dataset)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  resource  `

`  object ( Dataset  ` )

The dataset to be inserted.

## Dataset

BigQuery dataset information. See the [Dataset](/bigquery/docs/reference/v2/datasets) API resource for more details on individual fields.

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
  &quot;datasetName&quot;: {
    object (DatasetName)
  },
  &quot;info&quot;: {
    object (DatasetInfo)
  },
  &quot;createTime&quot;: string,
  &quot;updateTime&quot;: string,
  &quot;acl&quot;: {
    object (BigQueryAcl)
  },
  &quot;defaultTableExpireDuration&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  datasetName  `

`  object ( DatasetName  ` )

The name of the dataset.

`  info  `

`  object ( DatasetInfo  ` )

User-provided metadata for the dataset.

`  createTime  `

`  string ( Timestamp  ` format)

The time the dataset was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

`  updateTime  `

`  string ( Timestamp  ` format)

The time the dataset was last modified.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

`  acl  `

`  object ( BigQueryAcl  ` )

The access control list for the dataset.

`  defaultTableExpireDuration  `

`  string ( Duration  ` format)

If this field is present, each table that does not specify an expiration time is assigned an expiration time by adding this duration to the table's `  createTime  ` . If this field is empty, there is no default table expiration time.

A duration in seconds with up to nine fractional digits, ending with ' `  s  ` '. Example: `  "3.5s"  ` .

## DatasetName

The fully-qualified name for a dataset.

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
  &quot;projectId&quot;: string,
  &quot;datasetId&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  projectId  `

`  string  `

The project ID.

`  datasetId  `

`  string  `

The dataset ID within the project.

## DatasetInfo

User-provided metadata for a dataset.

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
  &quot;friendlyName&quot;: string,
  &quot;description&quot;: string,
  &quot;labels&quot;: {
    string: string,
    ...
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  friendlyName  `

`  string  `

A short name for the dataset, such as `  "Analytics Data 2011"  ` .

`  description  `

`  string  `

A long description, perhaps several paragraphs, describing the dataset contents in detail.

`  labels  `

`  map (key: string, value: string)  `

Labels provided for the dataset.

An object containing a list of `  "key": value  ` pairs. Example: `  { "name": "wrench", "mass": "1.3kg", "count": "3" }  ` .

## BigQueryAcl

An access control list.

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
  &quot;entries&quot;: [
    {
      object (BigQueryAcl.Entry)
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  entries[]  `

`  object ( BigQueryAcl.Entry  ` )

Access control entry list.

## BigQueryAcl.Entry

Access control entry.

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
  &quot;role&quot;: string,
  &quot;groupEmail&quot;: string,
  &quot;userEmail&quot;: string,
  &quot;domain&quot;: string,
  &quot;specialGroup&quot;: string,
  &quot;viewName&quot;: {
    object (TableName)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  role  `

`  string  `

The granted role, which can be `  READER  ` , `  WRITER  ` , or `  OWNER  ` .

`  groupEmail  `

`  string  `

Grants access to a group identified by an email address.

`  userEmail  `

`  string  `

Grants access to a user identified by an email address.

`  domain  `

`  string  `

Grants access to all members of a domain.

`  specialGroup  `

`  string  `

Grants access to special groups. Valid groups are `  PROJECT_OWNERS  ` , `  PROJECT_READERS  ` , `  PROJECT_WRITERS  ` and `  ALL_AUTHENTICATED_USERS  ` .

`  viewName  `

`  object ( TableName  ` )

Grants access to a BigQuery View.

## DatasetUpdateRequest

Dataset update request.

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
  &quot;resource&quot;: {
    object (Dataset)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  resource  `

`  object ( Dataset  ` )

The dataset to be updated.

## JobInsertRequest

Job insert request.

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
  &quot;resource&quot;: {
    object (Job)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  resource  `

`  object ( Job  ` )

Job insert request.

## Job

Describes a job.

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
  &quot;jobName&quot;: {
    object (JobName)
  },
  &quot;jobConfiguration&quot;: {
    object (JobConfiguration)
  },
  &quot;jobStatus&quot;: {
    object (JobStatus)
  },
  &quot;jobStatistics&quot;: {
    object (JobStatistics)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  jobName  `

`  object ( JobName  ` )

Job name.

`  jobConfiguration  `

`  object ( JobConfiguration  ` )

Job configuration.

`  jobStatus  `

`  object ( JobStatus  ` )

Job status.

`  jobStatistics  `

`  object ( JobStatistics  ` )

Job statistics.

## JobName

The fully-qualified name for a job.

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
  &quot;projectId&quot;: string,
  &quot;jobId&quot;: string,
  &quot;location&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  projectId  `

`  string  `

The project ID.

`  jobId  `

`  string  `

The job ID within the project.

`  location  `

`  string  `

The job location.

## JobConfiguration

Job configuration information. See the [Jobs](/bigquery/docs/reference/v2/jobs) API resource for more details on individual fields.

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
  &quot;dryRun&quot;: boolean,
  &quot;labels&quot;: {
    string: string,
    ...
  },

  // Union field configuration can be only one of the following:
  &quot;query&quot;: {
    object (JobConfiguration.Query)
  },
  &quot;load&quot;: {
    object (JobConfiguration.Load)
  },
  &quot;extract&quot;: {
    object (JobConfiguration.Extract)
  },
  &quot;tableCopy&quot;: {
    object (JobConfiguration.TableCopy)
  }
  // End of list of possible types for union field configuration.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  dryRun  `

`  boolean  `

If true, don't actually run the job. Just check that it would run.

`  labels  `

`  map (key: string, value: string)  `

Labels provided for the job.

An object containing a list of `  "key": value  ` pairs. Example: `  { "name": "wrench", "mass": "1.3kg", "count": "3" }  ` .

Union field `  configuration  ` . Job configuration information. `  configuration  ` can be only one of the following:

`  query  `

`  object ( JobConfiguration.Query  ` )

Query job information.

`  load  `

`  object ( JobConfiguration.Load  ` )

Load job information.

`  extract  `

`  object ( JobConfiguration.Extract  ` )

Extract job information.

`  tableCopy  `

`  object ( JobConfiguration.TableCopy  ` )

TableCopy job information.

## JobConfiguration.Query

Describes a query job, which executes a SQL-like query.

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
  &quot;query&quot;: string,
  &quot;destinationTable&quot;: {
    object (TableName)
  },
  &quot;createDisposition&quot;: string,
  &quot;writeDisposition&quot;: string,
  &quot;defaultDataset&quot;: {
    object (DatasetName)
  },
  &quot;tableDefinitions&quot;: [
    {
      object (TableDefinition)
    }
  ],
  &quot;queryPriority&quot;: string,
  &quot;destinationTableEncryption&quot;: {
    object (EncryptionInfo)
  },
  &quot;statementType&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  query  `

`  string  `

The SQL query to run.

`  destinationTable  `

`  object ( TableName  ` )

The table where results are written.

`  createDisposition  `

`  string  `

Describes when a job is allowed to create a table: `  CREATE_IF_NEEDED  ` , `  CREATE_NEVER  ` .

`  writeDisposition  `

`  string  `

Describes how writes affect existing tables: `  WRITE_TRUNCATE  ` , `  WRITE_APPEND  ` , `  WRITE_EMPTY  ` .

`  defaultDataset  `

`  object ( DatasetName  ` )

If a table name is specified without a dataset in a query, this dataset will be added to table name.

`  tableDefinitions[]  `

`  object ( TableDefinition  ` )

Describes data sources outside BigQuery, if needed.

`  queryPriority  `

`  string  `

Describes the priority given to the query: `  QUERY_INTERACTIVE  ` or `  QUERY_BATCH  ` .

`  destinationTableEncryption  `

`  object ( EncryptionInfo  ` )

Result table encryption information. Set when non-default encryption is used.

`  statementType  `

`  string  `

Type of the statement (e.g. SELECT, INSERT, CREATE\_TABLE, CREATE\_MODEL..)

## TableDefinition

Describes an external data source used in a query.

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
  &quot;name&quot;: string,
  &quot;sourceUris&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  name  `

`  string  `

Name of the table, used in queries.

`  sourceUris[]  `

`  string  `

Google Cloud Storage URIs for the data to be imported.

## JobConfiguration.Load

Describes a load job, which loads data from an external source via the import pipeline.

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
  &quot;sourceUris&quot;: [
    string
  ],
  &quot;schemaJson&quot;: string,
  &quot;destinationTable&quot;: {
    object (TableName)
  },
  &quot;createDisposition&quot;: string,
  &quot;writeDisposition&quot;: string,
  &quot;destinationTableEncryption&quot;: {
    object (EncryptionInfo)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  sourceUris[]  `

`  string  `

URIs for the data to be imported. Only Google Cloud Storage URIs are supported.

`  schemaJson  `

`  string  `

The table schema in JSON format representation of a TableSchema.

`  destinationTable  `

`  object ( TableName  ` )

The table where the imported data is written.

`  createDisposition  `

`  string  `

Describes when a job is allowed to create a table: `  CREATE_IF_NEEDED  ` , `  CREATE_NEVER  ` .

`  writeDisposition  `

`  string  `

Describes how writes affect existing tables: `  WRITE_TRUNCATE  ` , `  WRITE_APPEND  ` , `  WRITE_EMPTY  ` .

`  destinationTableEncryption  `

`  object ( EncryptionInfo  ` )

Result table encryption information. Set when non-default encryption is used.

## JobConfiguration.Extract

Describes an extract job, which exports data to an external source via the export pipeline.

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
  &quot;destinationUris&quot;: [
    string
  ],
  &quot;sourceTable&quot;: {
    object (TableName)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  destinationUris[]  `

`  string  `

Google Cloud Storage URIs where extracted data should be written.

`  sourceTable  `

`  object ( TableName  ` )

The source table.

## JobConfiguration.TableCopy

Describes a copy job, which copies an existing table to another table.

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
  &quot;sourceTables&quot;: [
    {
      object (TableName)
    }
  ],
  &quot;destinationTable&quot;: {
    object (TableName)
  },
  &quot;createDisposition&quot;: string,
  &quot;writeDisposition&quot;: string,
  &quot;destinationTableEncryption&quot;: {
    object (EncryptionInfo)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  sourceTables[]  `

`  object ( TableName  ` )

Source tables.

`  destinationTable  `

`  object ( TableName  ` )

Destination table.

`  createDisposition  `

`  string  `

Describes when a job is allowed to create a table: `  CREATE_IF_NEEDED  ` , `  CREATE_NEVER  ` .

`  writeDisposition  `

`  string  `

Describes how writes affect existing tables: `  WRITE_TRUNCATE  ` , `  WRITE_APPEND  ` , `  WRITE_EMPTY  ` .

`  destinationTableEncryption  `

`  object ( EncryptionInfo  ` )

Result table encryption information. Set when non-default encryption is used.

## JobStatus

Running state of a job.

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
  &quot;state&quot;: string,
  &quot;error&quot;: {
    object (Status)
  },
  &quot;additionalErrors&quot;: [
    {
      object (Status)
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  state  `

`  string  `

State of a job: `  PENDING  ` , `  RUNNING  ` , or `  DONE  ` .

`  error  `

`  object ( Status  ` )

If the job did not complete successfully, this field describes why.

`  additionalErrors[]  `

`  object ( Status  ` )

Errors encountered during the running of the job. Do not necessarily mean that the job has completed or was unsuccessful.

## JobStatistics

Job statistics that may change after a job starts.

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
  &quot;createTime&quot;: string,
  &quot;startTime&quot;: string,
  &quot;endTime&quot;: string,
  &quot;totalProcessedBytes&quot;: string,
  &quot;totalBilledBytes&quot;: string,
  &quot;billingTier&quot;: integer,
  &quot;totalSlotMs&quot;: string,
  &quot;reservationUsage&quot;: [
    {
      object (JobStatistics.ReservationResourceUsage)
    }
  ],
  &quot;reservation&quot;: string,
  &quot;referencedTables&quot;: [
    {
      object (TableName)
    }
  ],
  &quot;totalTablesProcessed&quot;: integer,
  &quot;referencedViews&quot;: [
    {
      object (TableName)
    }
  ],
  &quot;totalViewsProcessed&quot;: integer,
  &quot;queryOutputRowCount&quot;: string,
  &quot;totalLoadOutputBytes&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  createTime  `

`  string ( Timestamp  ` format)

Time when the job was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

`  startTime  `

`  string ( Timestamp  ` format)

Time when the job started.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

`  endTime  `

`  string ( Timestamp  ` format)

Time when the job ended.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

`  totalProcessedBytes  `

`  string ( int64 format)  `

Total bytes processed for a job.

`  totalBilledBytes  `

`  string ( int64 format)  `

Processed bytes, adjusted by the job's CPU usage.

`  billingTier  `

`  integer  `

The tier assigned by CPU-based billing.

`  totalSlotMs  `

`  string ( int64 format)  `

The total number of slot-ms consumed by the query job.

`  reservationUsage[] (deprecated)  `

`  object ( JobStatistics.ReservationResourceUsage  ` )

This item is deprecated\!

Deprecated as of 12/15/2022.

`  reservation  `

`  string  `

Reservation name or "unreserved" for on-demand resource usage.

`  referencedTables[]  `

`  object ( TableName  ` )

The first N tables accessed by the query job. Older queries that reference a large number of tables may not have all of their tables in this list. You can use the totalTablesProcessed count to know how many total tables were read in the query. For new queries, there is currently no limit.

`  totalTablesProcessed  `

`  integer  `

Total number of unique tables referenced in the query.

`  referencedViews[]  `

`  object ( TableName  ` )

The first N views accessed by the query job. Older queries that reference a large number of views may not have all of their views in this list. You can use the totalTablesProcessed count to know how many total tables were read in the query. For new queries, there is currently no limit.

`  totalViewsProcessed  `

`  integer  `

Total number of unique views referenced in the query.

`  queryOutputRowCount  `

`  string ( int64 format)  `

Number of output rows produced by the query job.

`  totalLoadOutputBytes  `

`  string ( int64 format)  `

Total bytes loaded for an import job.

## JobStatistics.ReservationResourceUsage

This field is deprecated. Job resource usage breakdown by reservation.

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
  &quot;name&quot;: string,
  &quot;slotMs&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  name  `

`  string  `

Reservation name or "unreserved" for on-demand resources usage.

`  slotMs  `

`  string ( int64 format)  `

Total slot milliseconds used by the reservation for a particular job.

## JobQueryRequest

Job query request.

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
  &quot;query&quot;: string,
  &quot;maxResults&quot;: integer,
  &quot;defaultDataset&quot;: {
    object (DatasetName)
  },
  &quot;projectId&quot;: string,
  &quot;dryRun&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  query  `

`  string  `

The query.

`  maxResults  `

`  integer ( uint32 format)  `

The maximum number of results.

`  defaultDataset  `

`  object ( DatasetName  ` )

The default dataset for tables that do not have a dataset specified.

`  projectId  `

`  string  `

Project that the query should be charged to.

`  dryRun  `

`  boolean  `

If true, don't actually run the job. Just check that it would run.

## JobGetQueryResultsRequest

Job getQueryResults request.

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
  &quot;maxResults&quot;: integer,
  &quot;startRow&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  maxResults  `

`  integer ( uint32 format)  `

Maximum number of results to return.

`  startRow  `

`  string  `

Zero-based row number at which to start.

## TableDataListRequest

Table data-list request.

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
  &quot;startRow&quot;: string,
  &quot;maxResults&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  startRow  `

`  string  `

Starting row offset.

`  maxResults  `

`  integer ( uint32 format)  `

Maximum number of results to return.

## SetIamPolicyRequest

Request message for `  SetIamPolicy  ` method.

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
  &quot;resource&quot;: string,
  &quot;policy&quot;: {
    object (Policy)
  },
  &quot;updateMask&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  resource  `

`  string  `

REQUIRED: The resource for which the policy is being specified. See [Resource names](https://cloud.google.com/apis/design/resource_names) for the appropriate value for this field.

`  policy  `

`  object ( Policy  ` )

REQUIRED: The complete policy to be applied to the `  resource  ` . The size of the policy is limited to a few 10s of KB. An empty policy is a valid policy but certain Google Cloud services (such as Projects) might reject them.

`  updateMask  `

`  string ( FieldMask  ` format)

OPTIONAL: A FieldMask specifying which fields of the policy to modify. Only the fields in the mask will be modified. If no mask is provided, the following default mask is used:

`  paths: "bindings, etag"  `

This is a comma-separated list of fully qualified names of fields. Example: `  "user.displayName,photo"  ` .

## TableInsertResponse

Table insert response.

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
  &quot;resource&quot;: {
    object (Table)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  resource  `

`  object ( Table  ` )

Final state of the inserted table.

## TableUpdateResponse

Table update response.

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
  &quot;resource&quot;: {
    object (Table)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  resource  `

`  object ( Table  ` )

Final state of the updated table.

## DatasetInsertResponse

Dataset insert response.

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
  &quot;resource&quot;: {
    object (Dataset)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  resource  `

`  object ( Dataset  ` )

Final state of the inserted dataset.

## DatasetUpdateResponse

Dataset update response.

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
  &quot;resource&quot;: {
    object (Dataset)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  resource  `

`  object ( Dataset  ` )

Final state of the updated dataset.

## JobInsertResponse

Job insert response.

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
  &quot;resource&quot;: {
    object (Job)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  resource  `

`  object ( Job  ` )

Job insert response.

## JobQueryResponse

Job query response.

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
  &quot;totalResults&quot;: string,
  &quot;job&quot;: {
    object (Job)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  totalResults  `

`  string  `

The total number of rows in the full query result set.

`  job  `

`  object ( Job  ` )

Information about the queried job.

## JobGetQueryResultsResponse

Job getQueryResults response.

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
  &quot;totalResults&quot;: string,
  &quot;job&quot;: {
    object (Job)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  totalResults  `

`  string  `

Total number of results in query results.

`  job  `

`  object ( Job  ` )

The job that was created to run the query. It completed if `  job.status.state  ` is `  DONE  ` . It failed if `  job.status.errorResult  ` is also present.

## JobQueryDoneResponse

Job getQueryDone response.

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
  &quot;job&quot;: {
    object (Job)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  job  `

`  object ( Job  ` )

The job and status information. The job completed if `  job.status.state  ` is `  DONE  ` .

## JobCompletedEvent

Query job completed event.

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
  &quot;eventName&quot;: string,
  &quot;job&quot;: {
    object (Job)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  eventName  `

`  string  `

Name of the event.

`  job  `

`  object ( Job  ` )

Job information.

## TableDataReadEvent

Table data read event. Only present for tables, not views, and is only included in the log record for the project that owns the table.

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
  &quot;tableName&quot;: {
    object (TableName)
  },
  &quot;referencedFields&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  tableName  `

`  object ( TableName  ` )

Name of the accessed table.

`  referencedFields[]  `

`  string  `

A list of referenced fields. This information is not included by default. To enable this in the logs, please contact BigQuery support or open a bug in the BigQuery issue tracker.
