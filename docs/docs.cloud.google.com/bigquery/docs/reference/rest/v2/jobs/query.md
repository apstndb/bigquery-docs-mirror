---
name: documents/docs.cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query
uri: https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query
title: 'Method: jobs.query'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [HTTP request](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query#body.HTTP_TEMPLATE)
- [Path parameters](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query#body.PATH_PARAMETERS)
- [Request body](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query#body.request_body)
- [Response body](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query#body.response_body)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query#body.QueryResponse.SCHEMA_REPRESENTATION)
- [Authorization scopes](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query#body.aspect)
- [QueryRequest](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query#QueryRequest)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query#QueryRequest.SCHEMA_REPRESENTATION)
- [JobCreationMode](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query#JobCreationMode)
- [QueryResultsFormat](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query#QueryResultsFormat)
- [ArrowSerializationOptions](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query#ArrowSerializationOptions)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query#ArrowSerializationOptions.SCHEMA_REPRESENTATION)
- [CompressionCodec](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query#CompressionCodec)
- [PicosTimestampPrecision](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query#PicosTimestampPrecision)
- [ArrowSchema](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query#ArrowSchema)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query#ArrowSchema.SCHEMA_REPRESENTATION)
- [ArrowRecordBatch](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query#ArrowRecordBatch)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query#ArrowRecordBatch.SCHEMA_REPRESENTATION)
- [Try it!](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query#try-it)

Runs a BigQuery SQL query synchronously and returns query results if the query completes within a specified timeout.

### IAM Permissions

Requires the `bigquery.jobs.create` permission on the project resource.

Data-level permissions are highly dependent on the SQL statement being executed. While standard queries require data access (such as `bigquery.tables.getData` ), complex operations like DDL or DCL may require permissions to manage reservations, IAM policies, or project settings.

### HTTP request

`POST https://bigquery.googleapis.com/bigquery/v2/projects/{projectId}/queries`

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

| Parameters  |                                                     |
|-------------|-----------------------------------------------------|
| `projectId` | `string` Required. Project ID of the query request. |

### Request body

The request body contains an instance of [`QueryRequest`](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query#QueryRequest) .

### Response body

If successful, the response body contains data with the following structure:

**JSON representation**

```
{
  "kind": string,
  "schema": {
    object (TableSchema)
  },
  "jobReference": {
    object (JobReference)
  },
  "jobCreationReason": {
    object (JobCreationReason)
  },
  "queryId": string,
  "location": string,
  "totalRows": string,
  "pageToken": string,
  "rows": [
    {
      object
    }
  ],
  "totalBytesProcessed": string,
  "jobComplete": boolean,
  "errors": [
    {
      object (ErrorProto)
    }
  ],
  "cacheHit": boolean,
  "numDmlAffectedRows": string,
  "sessionInfo": {
    object (SessionInfo)
  },
  "dmlStats": {
    object (DmlStats)
  },
  "pageRowCount": string,
  "statementType": string,
  "totalBytesBilled": string,
  "totalSlotMs": string,
  "creationTime": string,
  "startTime": string,
  "endTime": string,

  // The following is a list of mutually exclusive fields. At most one of the
  // fields will be set in a response:
  "arrowSchema": {
    object (ArrowSchema)
  }
  // End of mutually exclusive fields.

  // The following is a list of mutually exclusive fields. At most one of the
  // fields will be set in a response:
  "arrowRecordBatch": {
    object (ArrowRecordBatch)
  }
  // End of mutually exclusive fields.
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
<td><code>kind</code></td>
<td><p><code>string</code></p>
<p>The resource type.</p></td>
</tr>
<tr class="even">
<td><code>schema</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/tables#TableSchema"><code>TableSchema</code></a><code> )</code></p>
<p>The schema of the results. Present only when the query completes successfully.</p></td>
</tr>
<tr class="odd">
<td><code>jobReference</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/JobReference"><code>JobReference</code></a><code> )</code></p>
<p>Reference to the Job that was created to run the query. This field will be present even if the original request timed out, in which case jobs.getQueryResults can be used to read the results once the query has completed. Since this API only returns the first page of results, subsequent pages can be fetched via the same mechanism (jobs.getQueryResults).</p>
<p>If jobCreationMode was set to <code>JOB_CREATION_OPTIONAL</code> and the query completes without creating a job, this field will be empty.</p></td>
</tr>
<tr class="even">
<td><code>jobCreationReason</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/JobCreationReason"><code>JobCreationReason</code></a><code> )</code></p>
<p>Optional. The reason why a Job was created.</p>
<p>Only relevant when a jobReference is present in the response. If jobReference is not present it will always be unset.</p></td>
</tr>
<tr class="odd">
<td><code>queryId</code></td>
<td><p><code>string</code></p>
<p>Auto-generated ID for the query.</p></td>
</tr>
<tr class="even">
<td><code>location</code></td>
<td><p><code>string</code></p>
<p>Output only. The geographic location of the query.</p>
<p>For more information about BigQuery locations, see: <a href="https://cloud.google.com/bigquery/docs/locations">https://cloud.google.com/bigquery/docs/locations</a></p></td>
</tr>
<tr class="odd">
<td><code>totalRows</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>UInt64Value</code></a><code> format)</code></p>
<p>The total number of rows in the complete query result set, which can be more than the number of rows in this single page of results.</p></td>
</tr>
<tr class="even">
<td><code>pageToken</code></td>
<td><p><code>string</code></p>
<p>A token used for paging results. A non-empty token indicates that additional results are available. To see additional results, query the <a href="https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/getQueryResults"><code>jobs.getQueryResults</code></a> method. For more information, see <a href="https://cloud.google.com/bigquery/docs/paging-results">Paging through table data</a> .</p></td>
</tr>
<tr class="odd">
<td><code>rows[]</code></td>
<td><p><code>object ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#struct"><code>Struct</code></a><code> format)</code></p>
<p>An object with as many results as can be contained within the maximum permitted reply size. To get any additional rows, you can call jobs.getQueryResults and specify the jobReference returned above.</p></td>
</tr>
<tr class="even">
<td><code>totalBytesProcessed</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>Int64Value</code></a><code> format)</code></p>
<p>The total number of bytes processed for this query. If this query was a dry run, this is the number of bytes that would be processed if the query were run.</p></td>
</tr>
<tr class="odd">
<td><code>jobComplete</code></td>
<td><p><code>boolean</code></p>
<p>Whether the query has completed or not. If rows or totalRows are present, this will always be true. If this is false, totalRows will not be available.</p></td>
</tr>
<tr class="even">
<td><code>errors[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/ErrorProto"><code>ErrorProto</code></a><code> )</code></p>
<p>Output only. The first errors or warnings encountered during the running of the job. The final message includes the number of errors that caused the process to stop. Errors here do not necessarily mean that the job has completed or was unsuccessful. For more information about error messages, see <a href="https://cloud.google.com/bigquery/docs/error-messages">Error messages</a> .</p></td>
</tr>
<tr class="odd">
<td><code>cacheHit</code></td>
<td><p><code>boolean</code></p>
<p>Whether the query result was fetched from the query cache.</p></td>
</tr>
<tr class="even">
<td><code>numDmlAffectedRows</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>Int64Value</code></a><code> format)</code></p>
<p>Output only. The number of rows affected by a DML statement. Present only for DML statements INSERT, UPDATE or DELETE.</p></td>
</tr>
<tr class="odd">
<td><code>sessionInfo</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/SessionInfo"><code>SessionInfo</code></a><code> )</code></p>
<p>Output only. Information of the session if this job is part of one.</p></td>
</tr>
<tr class="even">
<td><code>dmlStats</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/DmlStats"><code>DmlStats</code></a><code> )</code></p>
<p>Output only. Detailed statistics for DML statements INSERT, UPDATE, DELETE, MERGE or TRUNCATE.</p></td>
</tr>
<tr class="odd">
<td><code>pageRowCount</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>int64</code></a><code> format)</code></p>
<p>Output only. The number of rows out of <code>totalRows</code> returned in this response.</p>
<p><a href="https://cloud.google.com/products/#product-launch-stages">Preview</a></p></td>
</tr>
<tr class="even">
<td><code>statementType</code></td>
<td><p><code>string</code></p>
<p>Output only. The type of query statement, if valid. Possible values:</p>
<ul>
<li><code>SELECT</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/query-syntax#select_list"><code>SELECT</code></a> statement.</li>
<li><code>ASSERT</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/debugging-statements#assert"><code>ASSERT</code></a> statement.</li>
<li><code>INSERT</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/dml-syntax#insert_statement"><code>INSERT</code></a> statement.</li>
<li><code>UPDATE</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/dml-syntax#update_statement"><code>UPDATE</code></a> statement.</li>
<li><code>DELETE</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-manipulation-language"><code>DELETE</code></a> statement.</li>
<li><code>MERGE</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-manipulation-language"><code>MERGE</code></a> statement.</li>
<li><code>TRUNCATE_TABLE</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/dml-syntax#truncate_table_statement"><code>TRUNCATE TABLE</code></a> statement.</li>
<li><code>CREATE_TABLE</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_table_statement"><code>CREATE TABLE</code></a> statement, without <code>AS SELECT</code> .</li>
<li><code>CREATE_TABLE_AS_SELECT</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_table_statement"><code>CREATE TABLE AS SELECT</code></a> statement.</li>
<li><code>CREATE_VIEW</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_view_statement"><code>CREATE VIEW</code></a> statement.</li>
<li><code>CREATE_MODEL</code> : <a href="https://cloud.google.com/bigquery-ml/docs/reference/standard-sql/bigqueryml-syntax-create#create_model_statement"><code>CREATE MODEL</code></a> statement.</li>
<li><code>CREATE_MATERIALIZED_VIEW</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_materialized_view_statement"><code>CREATE MATERIALIZED VIEW</code></a> statement.</li>
<li><code>CREATE_FUNCTION</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_function_statement"><code>CREATE FUNCTION</code></a> statement.</li>
<li><code>CREATE_TABLE_FUNCTION</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_table_function_statement"><code>CREATE TABLE FUNCTION</code></a> statement.</li>
<li><code>CREATE_PROCEDURE</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_procedure"><code>CREATE PROCEDURE</code></a> statement.</li>
<li><code>CREATE_ROW_ACCESS_POLICY</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_row_access_policy_statement"><code>CREATE ROW ACCESS POLICY</code></a> statement.</li>
<li><code>CREATE_SCHEMA</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_schema_statement"><code>CREATE SCHEMA</code></a> statement.</li>
<li><code>CREATE_EXTERNAL_SCHEMA</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_external_schema_statement"><code>CREATE EXTERNAL SCHEMA</code></a> statement.</li>
<li><code>CREATE_EXTERNAL_TABLE</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_external_table_statement"><code>CREATE EXTERNAL TABLE</code></a> statement.</li>
<li><code>CREATE_SNAPSHOT_TABLE</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_snapshot_table_statement"><code>CREATE SNAPSHOT TABLE</code></a> statement.</li>
<li><code>CREATE_SEARCH_INDEX</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_search_index_statement"><code>CREATE SEARCH INDEX</code></a> statement.</li>
<li><code>CREATE_VECTOR_INDEX</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_vector_index_statement"><code>CREATE VECTOR INDEX</code></a> statement.</li>
<li><code>CREATE_CONNECTION</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_connection_statement"><code>CREATE CONNECTION</code></a> statement.</li>
<li><code>CREATE_DATA_POLICY</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_data_policy_statement"><code>CREATE DATA_POLICY</code></a> statement.</li>
<li><code>CREATE_PROPERTY_GRAPH</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/graph-schema-statements#gql_create_graph"><code>CREATE PROPERTY GRAPH</code></a> statement.</li>
<li><code>CREATE_CAPACITY</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_capacity_statement"><code>CREATE CAPACITY</code></a> statement.</li>
<li><code>CREATE_RESERVATION</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_reservation_statement"><code>CREATE RESERVATION</code></a> statement.</li>
<li><code>CREATE_ASSIGNMENT</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_assignment_statement"><code>CREATE ASSIGNMENT</code></a> statement.</li>
<li><code>DROP_TABLE</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_table_statement"><code>DROP TABLE</code></a> statement.</li>
<li><code>DROP_EXTERNAL_TABLE</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_external_table_statement"><code>DROP EXTERNAL TABLE</code></a> statement.</li>
<li><code>DROP_VIEW</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_view_statement"><code>DROP VIEW</code></a> statement.</li>
<li><code>DROP_MODEL</code> : <a href="https://cloud.google.com/bigquery-ml/docs/reference/standard-sql/bigqueryml-syntax-drop-model"><code>DROP MODEL</code></a> statement.</li>
<li><code>DROP_MATERIALIZED_VIEW</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_materialized_view_statement"><code>DROP MATERIALIZED VIEW</code></a> statement.</li>
<li><code>DROP_FUNCTION</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_function_statement"><code>DROP FUNCTION</code></a> statement.</li>
<li><code>DROP_TABLE_FUNCTION</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_table_function"><code>DROP TABLE FUNCTION</code></a> statement.</li>
<li><code>DROP_PROCEDURE</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_procedure_statement"><code>DROP PROCEDURE</code></a> statement.</li>
<li><code>DROP_SEARCH_INDEX</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_search_index"><code>DROP SEARCH INDEX</code></a> statement.</li>
<li><code>DROP_VECTOR_INDEX</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_vector_index"><code>DROP VECTOR INDEX</code></a> statement.</li>
<li><code>DROP_SCHEMA</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_schema_statement"><code>DROP SCHEMA</code></a> statement.</li>
<li><code>UNDROP_SCHEMA</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#undrop_schema_statement"><code>UNDROP SCHEMA</code></a> statement.</li>
<li><code>DROP_SNAPSHOT_TABLE</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_snapshot_table_statement"><code>DROP SNAPSHOT TABLE</code></a> statement.</li>
<li><code>DROP_ROW_ACCESS_POLICY</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_row_access_policy_statement"><code>DROP [ALL] ROW ACCESS POLICY|POLICIES</code></a> statement.</li>
<li><code>DROP_CONNECTION</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_connection_statement"><code>DROP CONNECTION</code></a> statement.</li>
<li><code>DROP_DATA_POLICY</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_data_policy"><code>DROP DATA_POLICY</code></a> statement.</li>
<li><code>DROP_PROPERTY_GRAPH</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/graph-schema-statements#gql_drop_graph"><code>DROP PROPERTY GRAPH</code></a> statement.</li>
<li><code>DROP_CAPACITY</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_capacity_statement"><code>DROP CAPACITY</code></a> statement.</li>
<li><code>DROP_RESERVATION</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_reservation_statement"><code>DROP RESERVATION</code></a> statement.</li>
<li><code>DROP_ASSIGNMENT</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_assignment_statement"><code>DROP ASSIGNMENT</code></a> statement.</li>
<li><code>ALTER_TABLE</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#alter_table_set_options_statement"><code>ALTER TABLE</code></a> statement.</li>
<li><code>ALTER_VIEW</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#alter_view_set_options_statement"><code>ALTER VIEW</code></a> statement.</li>
<li><code>ALTER_MATERIALIZED_VIEW</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#alter_materialized_view_set_options_statement"><code>ALTER MATERIALIZED VIEW</code></a> statement.</li>
<li><code>ALTER_SCHEMA</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#alter_schema_set_options_statement"><code>ALTER SCHEMA</code></a> statement.</li>
<li><code>ALTER_MODEL</code> : <a href="https://cloud.google.com/bigquery-ml/docs/reference/standard-sql/bigqueryml-syntax-alter-model"><code>ALTER MODEL</code></a> statement.</li>
<li><code>ALTER_SEARCH_INDEX</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#alter_search_index_statement"><code>ALTER SEARCH INDEX</code></a> statement.</li>
<li><code>ALTER_VECTOR_INDEX</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#alter_vector_index_rebuild_statement"><code>ALTER VECTOR INDEX</code></a> statement.</li>
<li><code>ALTER_CONNECTION</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#alter_connection_set_options_statement"><code>ALTER CONNECTION</code></a> statement.</li>
<li><code>ALTER_DATA_POLICY</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#alter_data_policy_statement"><code>ALTER DATA_POLICY</code></a> statement.</li>
<li><code>ALTER_PROJECT</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#alter_project_set_options_statement"><code>ALTER PROJECT</code></a> statement.</li>
<li><code>ALTER_ORGANIZATION</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#alter_organization_set_options_statement"><code>ALTER ORGANIZATION</code></a> statement.</li>
<li><code>ALTER_BI_CAPACITY</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#alter_bi_capacity_set_options_statement"><code>ALTER BI_CAPACITY</code></a> statement.</li>
<li><code>ALTER_CAPACITY</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#alter_capacity_set_options_statement"><code>ALTER CAPACITY</code></a> statement.</li>
<li><code>ALTER_RESERVATION</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#alter_reservation_set_options_statement"><code>ALTER RESERVATION</code></a> statement.</li>
<li><code>SCRIPT</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/procedural-language"><code>SCRIPT</code></a> statement.</li>
<li><code>CALL</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/procedural-language#call"><code>CALL</code></a> statement.</li>
<li><code>BEGIN_TRANSACTION</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/procedural-language#begin_transaction"><code>BEGIN TRANSACTION</code></a> statement.</li>
<li><code>COMMIT_TRANSACTION</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/procedural-language#commit_transaction"><code>COMMIT TRANSACTION</code></a> statement.</li>
<li><code>ROLLBACK_TRANSACTION</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/procedural-language#rollback_transaction"><code>ROLLBACK TRANSACTION</code></a> statement.</li>
<li><code>EXPORT_DATA</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/export-statements#export_data_statement"><code>EXPORT DATA</code></a> statement.</li>
<li><code>EXPORT_MODEL</code> : <a href="https://cloud.google.com/bigquery-ml/docs/reference/standard-sql/bigqueryml-syntax-export-model"><code>EXPORT MODEL</code></a> statement.</li>
<li><code>EXPORT_METADATA</code> : <a href="https://cloud.google.com/bigquery/docs/biglake-iceberg-tables-in-bigquery"><code>EXPORT TABLE METADATA</code></a> statement, for BigLake Iceberg tables.</li>
<li><code>LOAD_DATA</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/load-statements#load_data_statement"><code>LOAD DATA</code></a> statement.</li>
<li><code>GRANT_ON_SCHEMA</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-control-language#grant_statement"><code>GRANT ... ON SCHEMA</code></a> statement.</li>
<li><code>GRANT_ON_TABLE</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-control-language#grant_statement"><code>GRANT ... ON TABLE</code></a> statement. Also used for <code>GRANT ... ON EXTERNAL TABLE</code> .</li>
<li><code>GRANT_ON_VIEW</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-control-language#grant_statement"><code>GRANT ... ON VIEW</code></a> statement.</li>
<li><code>GRANT_ON_PROJECT</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-control-language#grant_statement"><code>GRANT ... ON PROJECT</code></a> statement.</li>
<li><code>REVOKE_ON_SCHEMA</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-control-language#revoke_statement"><code>REVOKE ... ON SCHEMA</code></a> statement.</li>
<li><code>REVOKE_ON_TABLE</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-control-language#revoke_statement"><code>REVOKE ... ON TABLE</code></a> statement. Also used for <code>REVOKE ... ON EXTERNAL TABLE</code> .</li>
<li><code>REVOKE_ON_VIEW</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-control-language#revoke_statement"><code>REVOKE ... ON VIEW</code></a> statement.</li>
<li><code>REVOKE_ON_PROJECT</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-control-language#revoke_statement"><code>REVOKE ... ON PROJECT</code></a> statement.</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>totalBytesBilled</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>int64</code></a><code> format)</code></p>
<p>Output only. If the project is configured to use on-demand pricing, then this field contains the total bytes billed for the job. If the project is configured to use flat-rate pricing, then you are not billed for bytes and this field is informational only.</p></td>
</tr>
<tr class="even">
<td><code>totalSlotMs</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>int64</code></a><code> format)</code></p>
<p>Output only. Number of slot ms the user is actually billed for.</p></td>
</tr>
<tr class="odd">
<td><code>creationTime</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>int64</code></a><code> format)</code></p>
<p>Output only. Creation time of this query, in milliseconds since the epoch. This field will be present on all queries.</p></td>
</tr>
<tr class="even">
<td><code>startTime</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>int64</code></a><code> format)</code></p>
<p>Output only. Start time of this query, in milliseconds since the epoch. This field will be present when the query job transitions from the PENDING state to either RUNNING or DONE.</p></td>
</tr>
<tr class="odd">
<td><code>endTime</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>int64</code></a><code> format)</code></p>
<p>Output only. End time of this query, in milliseconds since the epoch. This field will be present whenever a query job is in the DONE state.</p></td>
</tr>
<tr class="even">
<td><p>The schema if <code>query_results_format</code> has been specified with value other than default <code>STRUCT_ENCODING</code> .</p>
<p><a href="https://cloud.google.com/products/#product-launch-stages">Preview</a> The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:</p></td>
<td></td>
</tr>
<tr class="odd">
<td><code>arrowSchema</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query#ArrowSchema"><code>ArrowSchema</code></a><code> )</code></p>
<p>Output only. Arrow schema</p></td>
</tr>
<tr class="even">
<td>End of mutually exclusive fields.</td>
<td></td>
</tr>
<tr class="odd">
<td><p>Row data is returned in format when <code>query_results_format</code> has been specified with value other than default <code>STRUCT_ENCODING</code> .</p>
<p><a href="https://cloud.google.com/products/#product-launch-stages">Preview</a> The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>arrowRecordBatch</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query#ArrowRecordBatch"><code>ArrowRecordBatch</code></a><code> )</code></p>
<p>Output only. Serialized row data in Arrow RecordBatch format.</p></td>
</tr>
<tr class="odd">
<td>End of mutually exclusive fields.</td>
<td></td>
</tr>
</tbody>
</table>

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/bigquery.readonly`
- `https://www.googleapis.com/auth/cloud-platform.read-only`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

## QueryRequest

Describes the format of the jobs.query request.

**JSON representation**

```
{
  "kind": string,
  "query": string,
  "maxResults": integer,
  "defaultDataset": {
    object (DatasetReference)
  },
  "timeoutMs": integer,
  "destinationEncryptionConfiguration": {
    object (EncryptionConfiguration)
  },
  "dryRun": boolean,
  "preserveNulls": boolean,
  "useQueryCache": boolean,
  "useLegacySql": boolean,
  "parameterMode": string,
  "queryParameters": [
    {
      object (QueryParameter)
    }
  ],
  "location": string,
  "formatOptions": {
    object (DataFormatOptions)
  },
  "connectionProperties": [
    {
      object (ConnectionProperty)
    }
  ],
  "labels": {
    string: string,
    ...
  },
  "maximumBytesBilled": string,
  "requestId": string,
  "createSession": boolean,
  "jobCreationMode": enum (JobCreationMode),
  "queryResultsFormat": enum (QueryResultsFormat),
  "secureContext": {
    object (SecureContext)
  },
  "jobTimeoutMs": string,
  "reservation": string,

  // The following is a list of mutually exclusive fields. At most one of the
  // fields will be set in a response:
  "arrowSerializationOptions": {
    object (ArrowSerializationOptions)
  }
  // End of mutually exclusive fields.
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
<td><code>kind</code></td>
<td><p><code>string</code></p>
<p>The resource type of the request.</p></td>
</tr>
<tr class="even">
<td><code>query</code></td>
<td><p><code>string</code></p>
<p>Required. A query string to execute, using Google Standard SQL or legacy SQL syntax. Example: "SELECT COUNT(f1) FROM myProjectId.myDatasetId.myTableId".</p></td>
</tr>
<tr class="odd">
<td><code>maxResults</code></td>
<td><p><code>integer</code></p>
<p>Optional. The maximum number of rows of data to return per page of results. Setting this flag to a small value such as 1000 and then paging through results might improve reliability when the query result set is large. In addition to this limit, responses are also limited to 10 MB. By default, there is no maximum row count, and only the byte limit applies.</p></td>
</tr>
<tr class="even">
<td><code>defaultDataset</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/datasets#DatasetReference"><code>DatasetReference</code></a><code> )</code></p>
<p>Optional. Specifies the default datasetId and projectId to assume for any unqualified table names in the query. If not set, all table names in the query string must be qualified in the format 'datasetId.tableId'.</p></td>
</tr>
<tr class="odd">
<td><code>timeoutMs</code></td>
<td><p><code>integer</code></p>
<p>Optional. Optional: Specifies the maximum amount of time, in milliseconds, that the client is willing to wait for the query to complete. By default, this limit is 10 seconds (10,000 milliseconds). If the query is complete, the jobComplete field in the response is true. If the query has not yet completed, jobComplete is false.</p>
<p>You can request a longer timeout period in the timeoutMs field. However, the call is not guaranteed to wait for the specified timeout; it typically returns after around 200 seconds (200,000 milliseconds), even if the query is not complete.</p>
<p>If jobComplete is false, you can continue to wait for the query to complete by calling the getQueryResults method until the jobComplete field in the getQueryResults response is true.</p></td>
</tr>
<tr class="even">
<td><code>destinationEncryptionConfiguration</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/EncryptionConfiguration"><code>EncryptionConfiguration</code></a><code> )</code></p>
<p>Optional. Custom encryption configuration (e.g., Cloud KMS keys)</p></td>
</tr>
<tr class="odd">
<td><code>dryRun</code></td>
<td><p><code>boolean</code></p>
<p>Optional. If set to true, BigQuery doesn't run the job. Instead, if the query is valid, BigQuery returns statistics about the job such as how many bytes would be processed. If the query is invalid, an error returns. The default value is false.</p></td>
</tr>
<tr class="even">
<td><code>preserveNulls </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>boolean</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>This property is deprecated.</p></td>
</tr>
<tr class="odd">
<td><code>useQueryCache</code></td>
<td><p><code>boolean</code></p>
<p>Optional. Whether to look for the result in the query cache. The query cache is a best-effort cache that will be flushed whenever tables in the query are modified. The default value is true.</p></td>
</tr>
<tr class="even">
<td><code>useLegacySql</code></td>
<td><p><code>boolean</code></p>
<p>Specifies whether to use BigQuery's legacy SQL dialect for this query. The default value is true. If set to false, the query uses BigQuery's <a href="https://docs.cloud.google.com/bigquery/docs/introduction-sql">GoogleSQL</a> . When useLegacySql is set to false, the value of flattenResults is ignored; query will be run as if flattenResults is false.</p></td>
</tr>
<tr class="odd">
<td><code>parameterMode</code></td>
<td><p><code>string</code></p>
<p>GoogleSQL only. Set to POSITIONAL to use positional (?) query parameters or to NAMED to use named (@myparam) query parameters in this query.</p></td>
</tr>
<tr class="even">
<td><code>queryParameters[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/QueryParameter"><code>QueryParameter</code></a><code> )</code></p>
<p>jobs.query parameters for GoogleSQL queries.</p></td>
</tr>
<tr class="odd">
<td><code>location</code></td>
<td><p><code>string</code></p>
<p>The geographic location where the job should run. For more information, see how to <a href="https://cloud.google.com/bigquery/docs/locations#specify_locations">specify locations</a> .</p></td>
</tr>
<tr class="even">
<td><code>formatOptions</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/DataFormatOptions"><code>DataFormatOptions</code></a><code> )</code></p>
<p>Optional. Output format adjustments.</p></td>
</tr>
<tr class="odd">
<td><code>connectionProperties[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/ConnectionProperty"><code>ConnectionProperty</code></a><code> )</code></p>
<p>Optional. Connection properties which can modify the query behavior.</p></td>
</tr>
<tr class="even">
<td><code>labels</code></td>
<td><p><code>map (key: string, value: string)</code></p>
<p>Optional. The labels associated with this query. Labels can be used to organize and group query jobs. Label keys and values can be no longer than 63 characters, can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. Label keys must start with a letter and each label in the list must have a different key.</p></td>
</tr>
<tr class="odd">
<td><code>maximumBytesBilled</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>Int64Value</code></a><code> format)</code></p>
<p>Optional. Limits the bytes billed for this query. Queries with bytes billed above this limit will fail (without incurring a charge). If unspecified, the project default is used.</p></td>
</tr>
<tr class="even">
<td><code>requestId</code></td>
<td><p><code>string</code></p>
<p>Optional. A unique user provided identifier to ensure idempotent behavior for queries. Note that this is different from the jobId. It has the following properties:</p>
<ol>
<li><p>It is case-sensitive, limited to up to 36 ASCII characters. A UUID is recommended.</p></li>
<li><p>Read only queries can ignore this token since they are nullipotent by definition.</p></li>
<li><p>For the purposes of idempotency ensured by the requestId, a request is considered duplicate of another only if they have the same requestId and are actually duplicates. When determining whether a request is a duplicate of another request, all parameters in the request that may affect the result are considered. For example, query, connectionProperties, queryParameters, useLegacySql are parameters that affect the result and are considered when determining whether a request is a duplicate, but properties like timeoutMs don't affect the result and are thus not considered. Dry run query requests are never considered duplicate of another request.</p></li>
<li><p>When a duplicate mutating query request is detected, it returns: a. the results of the mutation if it completes successfully within the timeout. b. the running operation if it is still in progress at the end of the timeout.</p></li>
<li><p>Its lifetime is limited to 15 minutes. In other words, if two requests are sent with the same requestId, but more than 15 minutes apart, idempotency is not guaranteed.</p></li>
</ol></td>
</tr>
<tr class="odd">
<td><code>createSession</code></td>
<td><p><code>boolean</code></p>
<p>Optional. If true, creates a new session using a randomly generated sessionId. If false, runs query with an existing sessionId passed in ConnectionProperty, otherwise runs query in non-session mode.</p>
<p>The session location will be set to QueryRequest.location if it is present, otherwise it's set to the default location based on existing routing logic.</p></td>
</tr>
<tr class="even">
<td><code>jobCreationMode</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query#JobCreationMode"><code>JobCreationMode</code></a><code> )</code></p>
<p>Optional. If not set, jobs are always required.</p>
<p>If set, the query request will follow the behavior described JobCreationMode.</p></td>
</tr>
<tr class="odd">
<td><code>queryResultsFormat</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query#QueryResultsFormat"><code>QueryResultsFormat</code></a><code> )</code></p>
<p>Optional. The query results format. If the value is anything other than <code>STRUCT_ENCODING</code> or unspecified:</p>
<ul>
<li>The schema of the results is provided in the <code>QueryResponse.results_schema</code> field.</li>
<li>The results of the first page are provided in the <code>QueryResponse.results</code> field.</li>
<li>The <code>QueryResponse.rows</code> is not populated.</li>
<li>The <code>QueryResponse.schema</code> for <code>QueryResponse.rows</code> is not populated since it is the schema of the <code>QueryResponse.rows</code> .</li>
</ul>
<p><a href="https://cloud.google.com/products/#product-launch-stages">Preview</a></p></td>
</tr>
<tr class="even">
<td><code>secureContext</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/SecureContext"><code>SecureContext</code></a><code> )</code></p>
<p>Optional. A set of key-value pairs representing the secure context. This can be used to pass sensitive or context-specific information. They can be retrieved via the SECURE_CONTEXT() function and used to modify the run-time behavior of a query.</p></td>
</tr>
<tr class="odd">
<td><code>jobTimeoutMs</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>int64</code></a><code> format)</code></p>
<p>Optional. Job timeout in milliseconds. If this time limit is exceeded, BigQuery will attempt to stop a longer job, but may not always succeed in canceling it before the job completes. For example, a job that takes more than 60 seconds to complete has a better chance of being stopped than a job that takes 10 seconds to complete. This timeout applies to the query even if a job does not need to be created.</p></td>
</tr>
<tr class="even">
<td><code>reservation</code></td>
<td><p><code>string</code></p>
<p>Optional. The reservation that jobs.query request would use. User can specify a reservation to execute the job.query. The expected format is <code>projects/{project}/locations/{location}/reservations/{reservation}</code> . Forces the query to use on-demand billing when set to <code>none</code> . This requires the project or organization to have <code>reservation_override_mode</code> set to <code>ALLOW_ANY_OVERRIDE</code> .</p></td>
</tr>
<tr class="odd">
<td><p>Results serialization options for <code>query_results_format</code> other than <code>STRUCT_ENCODING</code> .</p>
<p><a href="https://cloud.google.com/products/#product-launch-stages">Preview</a> The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>arrowSerializationOptions</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query#ArrowSerializationOptions"><code>ArrowSerializationOptions</code></a><code> )</code></p>
<p>Optional. Options specific to the Apache Arrow output format.</p></td>
</tr>
<tr class="odd">
<td>End of mutually exclusive fields.</td>
<td></td>
</tr>
</tbody>
</table>

## JobCreationMode

Job Creation Mode provides different options on job creation.

| Enums                           |                                                                                                                                                                                                                                                                                                                                   |
|---------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `JOB_CREATION_MODE_UNSPECIFIED` | If unspecified JOB_CREATION_REQUIRED is the default.                                                                                                                                                                                                                                                                              |
| `JOB_CREATION_REQUIRED`         | Default. Job creation is always required.                                                                                                                                                                                                                                                                                         |
| `JOB_CREATION_OPTIONAL`         | Job creation is optional. Returning immediate results is prioritized. BigQuery will automatically determine if a Job needs to be created. The conditions under which BigQuery can decide to not create a Job are subject to change. If Job creation is required, JOB_CREATION_REQUIRED mode should be used, which is the default. |

## QueryResultsFormat

The format of the query results.

[Preview](https://cloud.google.com/products/#product-launch-stages)

| Enums                              |                                                                                                                   |
|------------------------------------|-------------------------------------------------------------------------------------------------------------------|
| `QUERY_RESULTS_FORMAT_UNSPECIFIED` | If unspecified it will default to struct `QueryResponse.rows` ( `STRUCT_ENCODING` )                               |
| `STRUCT_ENCODING`                  | Default encoding of results as struct in `QueryResponse.rows`                                                     |
| `ARROW`                            | Arrow is a standard open source column-based message format. See the Apache Arrow documentation for more details. |

## ArrowSerializationOptions

Contains options specific to Arrow Serialization.

[Preview](https://cloud.google.com/products/#product-launch-stages)

**JSON representation**

```
{
  "bufferCompression": enum (CompressionCodec),
  "picosTimestampPrecision": enum (PicosTimestampPrecision)
}
```

| Fields                    |                                                                                                                                                                                                                                         |
|---------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `bufferCompression`       | `enum ( `[`CompressionCodec`](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query#CompressionCodec)` )` The compression codec to use for Arrow buffers in serialized record batches.                               |
| `picosTimestampPrecision` | `enum ( `[`PicosTimestampPrecision`](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query#PicosTimestampPrecision)` )` Optional. Set timestamp precision option. If not set, the default precision is microseconds. |

## CompressionCodec

Compression codec's supported by Arrow.

| Enums                     |                                                                          |
|---------------------------|--------------------------------------------------------------------------|
| `COMPRESSION_UNSPECIFIED` | If unspecified no compression will be used.                              |
| `LZ4_FRAME`               | [LZ4 Frame](https://github.com/lz4/lz4/blob/dev/doc/lz4_Frame_format.md) |
| `ZSTD`                    | Zstandard compression.                                                   |

## PicosTimestampPrecision

The precision of the timestamp value in the Avro message. This precision is only applied to the column(s) with the `TIMESTAMP_PICOS` type.

| Enums                                   |                                                                                                                                                                   |
|-----------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `PICOS_TIMESTAMP_PRECISION_UNSPECIFIED` | Unspecified timestamp precision. The default precision is microseconds.                                                                                           |
| `TIMESTAMP_PRECISION_MICROS`            | Timestamp values returned in the results will be truncated to microsecond level precision. The value will be encoded as Arrow TIMESTAMP type in a 64 bit integer. |
| `TIMESTAMP_PRECISION_NANOS`             | Timestamp values returned in the results will be truncated to nanosecond level precision. The value will be encoded as Arrow TIMESTAMP type in a 64 bit integer.  |
| `TIMESTAMP_PRECISION_PICOS`             | Timestamp values returned in the results will contain full precision picosecond value. The value will be encoded as a string which conforms to ISO 8601 format.   |

## ArrowSchema

Arrow schema as specified in <https://arrow.apache.org/docs/python/api/datatypes.html> and serialized to bytes using IPC: <https://arrow.apache.org/docs/format/Columnar.html#serialization-and-interprocess-communication-ipc>

See code samples on how this message can be deserialized.

[Preview](https://cloud.google.com/products/#product-launch-stages)

**JSON representation**

```
{
  "serializedSchema": string
}
```

| Fields             |                                                                                                                                              |
|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| `serializedSchema` | `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)` IPC serialized Arrow schema. A base64-encoded string. |

## ArrowRecordBatch

Arrow RecordBatch.

[Preview](https://cloud.google.com/products/#product-launch-stages)

**JSON representation**

```
{
  "serializedRecordBatch": string
}
```

| Fields                  |                                                                                                                                                   |
|-------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| `serializedRecordBatch` | `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)` IPC-serialized Arrow RecordBatch. A base64-encoded string. |
