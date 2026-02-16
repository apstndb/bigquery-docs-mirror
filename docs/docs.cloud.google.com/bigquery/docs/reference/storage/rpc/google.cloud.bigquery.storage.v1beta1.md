## Index

  - `  BigQueryStorage  ` (interface)
  - `  ArrowRecordBatch  ` (message)
  - `  ArrowSchema  ` (message)
  - `  AvroRows  ` (message)
  - `  AvroSchema  ` (message)
  - `  BatchCreateReadSessionStreamsRequest  ` (message)
  - `  BatchCreateReadSessionStreamsResponse  ` (message)
  - `  CreateReadSessionRequest  ` (message)
  - `  DataFormat  ` (enum)
  - `  FinalizeStreamRequest  ` (message)
  - `  Progress  ` (message)
  - `  ReadRowsRequest  ` (message)
  - `  ReadRowsResponse  ` (message)
  - `  ReadSession  ` (message)
  - `  ShardingStrategy  ` (enum)
  - `  SplitReadStreamRequest  ` (message)
  - `  SplitReadStreamResponse  ` (message)
  - `  Stream  ` (message)
  - `  StreamPosition  ` (message)
  - `  StreamStatus  ` (message)
  - `  TableModifiers  ` (message)
  - `  TableReadOptions  ` (message)
  - `  TableReference  ` (message)
  - `  ThrottleStatus  ` (message)

## BigQueryStorage

BigQuery storage API.

The BigQuery storage API can be used to read data stored in BigQuery.

The v1beta1 API is not yet officially deprecated, and will go through a full deprecation cycle ( <https://cloud.google.com/products#product-launch-stages> ) before the service is turned down. However, new code should use the v1 API going forward.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>BatchCreateReadSessionStreams</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc BatchCreateReadSessionStreams(                         BatchCreateReadSessionStreamsRequest            </code> ) returns ( <code dir="ltr" translate="no">              BatchCreateReadSessionStreamsResponse            </code> )</p>
<p>Creates additional streams for a ReadSession. This API can be used to dynamically adjust the parallelism of a batch processing task upwards by adding additional workers.</p></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>CreateReadSession</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc CreateReadSession(                         CreateReadSessionRequest            </code> ) returns ( <code dir="ltr" translate="no">              ReadSession            </code> )</p>
<p>Creates a new read session. A read session divides the contents of a BigQuery table into one or more streams, which can then be used to read data from the table. The read session also specifies properties of the data to be read, such as a list of columns or a push-down filter describing the rows to be returned.</p>
<p>A particular row can be read by at most one stream. When the caller has reached the end of each stream in the session, then all the data in the table has been read.</p>
<p>Read sessions automatically expire 6 hours after they are created and do not require manual clean-up by the caller.</p></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>FinalizeStream</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc FinalizeStream(                         FinalizeStreamRequest            </code> ) returns ( <code dir="ltr" translate="no">              Empty            </code> )</p>
<p>Causes a single stream in a ReadSession to gracefully stop. This API can be used to dynamically adjust the parallelism of a batch processing task downwards without losing data.</p>
<p>This API does not delete the stream -- it remains visible in the ReadSession, and any data processed by the stream is not released to other streams. However, no additional data will be assigned to the stream once this call completes. Callers must continue reading data on the stream until the end of the stream is reached so that data which has already been assigned to the stream will be processed.</p>
<p>This method will return an error if there are no other live streams in the Session, or if SplitReadStream() has been called on the given Stream.</p></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>ReadRows</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc ReadRows(                         ReadRowsRequest            </code> ) returns ( <code dir="ltr" translate="no">              ReadRowsResponse            </code> )</p>
<p>Reads rows from the table in the format prescribed by the read session. Each response contains one or more table rows, up to a maximum of 10 MiB per response; read requests which attempt to read individual rows larger than this will fail.</p>
<p>Each request also returns a set of stream statistics reflecting the estimated total number of rows in the read stream. This number is computed based on the total table size and the number of active streams in the read session, and may change as other streams continue to read data.</p></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>SplitReadStream</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc SplitReadStream(                         SplitReadStreamRequest            </code> ) returns ( <code dir="ltr" translate="no">              SplitReadStreamResponse            </code> )</p>
<p>Splits a given read stream into two Streams. These streams are referred to as the primary and the residual of the split. The original stream can still be read from in the same manner as before. Both of the returned streams can also be read from, and the total rows return by both child streams will be the same as the rows read from the original stream.</p>
<p>Moreover, the two child streams will be allocated back to back in the original Stream. Concretely, it is guaranteed that for streams Original, Primary, and Residual, that Original[0-j] = Primary[0-j] and Original[j-n] = Residual[0-m] once the streams have been read to completion.</p>
<p>This method is guaranteed to be idempotent.</p></td>
</tr>
</tbody>
</table>

## ArrowRecordBatch

Arrow RecordBatch.

Fields

`  serialized_record_batch  `

`  bytes  `

IPC serialized Arrow RecordBatch.

`  row_count  `

`  int64  `

The count of rows in the returning block.

## ArrowSchema

Arrow schema.

Fields

`  serialized_schema  `

`  bytes  `

IPC serialized Arrow schema.

## AvroRows

Avro rows.

Fields

`  serialized_binary_rows  `

`  bytes  `

Binary serialized rows in a block.

`  row_count  `

`  int64  `

The count of rows in the returning block.

## AvroSchema

Avro schema.

Fields

`  schema  `

`  string  `

Json serialized schema, as described at <https://avro.apache.org/docs/1.8.1/spec.html>

## BatchCreateReadSessionStreamsRequest

Information needed to request additional streams for an established read session.

Fields

`  session  `

`  ReadSession  `

Required. Must be a non-expired session obtained from a call to CreateReadSession. Only the name field needs to be set.

`  requested_streams  `

`  int32  `

Required. Number of new streams requested. Must be positive. Number of added streams may be less than this, see CreateReadSessionRequest for more information.

## BatchCreateReadSessionStreamsResponse

The response from `  BatchCreateReadSessionStreams  ` returns the stream identifiers for the newly created streams.

Fields

`  streams[]  `

`  Stream  `

Newly added streams.

## CreateReadSessionRequest

Creates a new read session, which may include additional options such as requested parallelism, projection filters and constraints.

Fields

`  table_reference  `

`  TableReference  `

Required. Reference to the table to read.

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  tableReference  ` :

  - `  bigquery.tables.getData  `

`  parent  `

`  string  `

Required. String of the form `  projects/{project_id}  ` indicating the project this ReadSession is associated with. This is the project that will be billed for usage.

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  parent  ` :

  - `  bigquery.readsessions.create  `

`  table_modifiers  `

`  TableModifiers  `

Any modifiers to the Table (e.g. snapshot timestamp).

`  requested_streams  `

`  int32  `

Initial number of streams. If unset or 0, we will provide a value of streams so as to produce reasonable throughput. Must be non-negative. The number of streams may be lower than the requested number, depending on the amount parallelism that is reasonable for the table and the maximum amount of parallelism allowed by the system.

Streams must be read starting from offset 0.

`  read_options  `

`  TableReadOptions  `

Read options for this session (e.g. column selection, filters).

`  format  `

`  DataFormat  `

Data output format. Currently default to Avro. DATA\_FORMAT\_UNSPECIFIED not supported.

`  sharding_strategy  `

`  ShardingStrategy  `

The strategy to use for distributing data among multiple streams. Currently defaults to liquid sharding.

## DataFormat

Data format for input or output data.

Enums

`  DATA_FORMAT_UNSPECIFIED  `

Data format is unspecified.

`  AVRO  `

Avro is a standard open source row based file format. See <https://avro.apache.org/> for more details.

`  ARROW  `

Arrow is a standard open source column-based message format. See <https://arrow.apache.org/> for more details.

## FinalizeStreamRequest

Request information for invoking `  FinalizeStream  ` .

Fields

`  stream  `

`  Stream  `

Required. Stream to finalize.

## Progress

Fields

`  at_response_start  `

`  float  `

The fraction of rows assigned to the stream that have been processed by the server so far, not including the rows in the current response message.

This value, along with `  at_response_end  ` , can be used to interpolate the progress made as the rows in the message are being processed using the following formula: `  at_response_start + (at_response_end - at_response_start) * rows_processed_from_response / rows_in_response  ` .

Note that if a filter is provided, the `  at_response_end  ` value of the previous response may not necessarily be equal to the `  at_response_start  ` value of the current response.

`  at_response_end  `

`  float  `

Similar to `  at_response_start  ` , except that this value includes the rows in the current response.

## ReadRowsRequest

Requesting row data via `  ReadRows  ` must provide Stream position information.

Fields

`  read_position  `

`  StreamPosition  `

Required. Identifier of the position in the stream to start reading from. The offset requested must be less than the last row read from ReadRows. Requesting a larger offset is undefined.

## ReadRowsResponse

Response from calling `  ReadRows  ` may include row data, progress and throttling information.

Fields

`  row_count  `

`  int64  `

Number of serialized rows in the rows block. This value is recorded here, in addition to the row\_count values in the output-specific messages in `  rows  ` , so that code which needs to record progress through the stream can do so in an output format-independent way.

`  status  `

`  StreamStatus  `

Estimated stream statistics.

`  throttle_status  `

`  ThrottleStatus  `

Throttling status. If unset, the latest response still describes the current throttling status.

Union field `  rows  ` . Row data is returned in format specified during session creation. `  rows  ` can be only one of the following:

`  avro_rows  `

`  AvroRows  `

Serialized row data in AVRO format.

`  arrow_record_batch  `

`  ArrowRecordBatch  `

Serialized row data in Arrow RecordBatch format.

Union field `  schema  ` . The schema for the read. If read\_options.selected\_fields is set, the schema may be different from the table schema as it will only contain the selected fields. This schema is equivalent to the one returned by CreateSession. This field is only populated in the first ReadRowsResponse RPC. `  schema  ` can be only one of the following:

`  avro_schema  `

`  AvroSchema  `

Output only. Avro schema.

`  arrow_schema  `

`  ArrowSchema  `

Output only. Arrow schema.

## ReadSession

Information returned from a `  CreateReadSession  ` request.

Fields

`  name  `

`  string  `

Unique identifier for the session, in the form `  projects/{project_id}/locations/{location}/sessions/{session_id}  ` .

`  expire_time  `

`  Timestamp  `

Time at which the session becomes invalid. After this time, subsequent requests to read this Session will return errors.

`  streams[]  `

`  Stream  `

Streams associated with this session.

`  table_reference  `

`  TableReference  `

Table that this ReadSession is reading from.

`  table_modifiers  `

`  TableModifiers  `

Any modifiers which are applied when reading from the specified table.

`  sharding_strategy  `

`  ShardingStrategy  `

The strategy to use for distributing data among the streams.

Union field `  schema  ` . The schema for the read. If read\_options.selected\_fields is set, the schema may be different from the table schema as it will only contain the selected fields. `  schema  ` can be only one of the following:

`  avro_schema  `

`  AvroSchema  `

Avro schema.

`  arrow_schema  `

`  ArrowSchema  `

Arrow schema.

## ShardingStrategy

Strategy for distributing data among multiple streams in a read session.

Enums

`  SHARDING_STRATEGY_UNSPECIFIED  `

Same as LIQUID.

`  LIQUID  `

Assigns data to each stream based on the client's read rate. The faster the client reads from a stream, the more data is assigned to the stream. In this strategy, it's possible to read all data from a single stream even if there are other streams present.

`  BALANCED  `

Assigns data to each stream such that roughly the same number of rows can be read from each stream. Because the server-side unit for assigning data is collections of rows, the API does not guarantee that each stream will return the same number or rows. Additionally, the limits are enforced based on the number of pre-filtering rows, so some filters can lead to lopsided assignments.

## SplitReadStreamRequest

Request information for `  SplitReadStream  ` .

Fields

`  original_stream  `

`  Stream  `

Required. Stream to split.

`  fraction  `

`  float  `

A value in the range (0.0, 1.0) that specifies the fractional point at which the original stream should be split. The actual split point is evaluated on pre-filtered rows, so if a filter is provided, then there is no guarantee that the division of the rows between the new child streams will be proportional to this fractional value. Additionally, because the server-side unit for assigning data is collections of rows, this fraction will always map to to a data storage boundary on the server side.

## SplitReadStreamResponse

Response from `  SplitReadStream  ` .

Fields

`  primary_stream  `

`  Stream  `

Primary stream, which contains the beginning portion of |original\_stream|. An empty value indicates that the original stream can no longer be split.

`  remainder_stream  `

`  Stream  `

Remainder stream, which contains the tail of |original\_stream|. An empty value indicates that the original stream can no longer be split.

## Stream

Information about a single data stream within a read session.

Fields

`  name  `

`  string  `

Name of the stream, in the form `  projects/{project_id}/locations/{location}/streams/{stream_id}  ` .

## StreamPosition

Expresses a point within a given stream using an offset position.

Fields

`  stream  `

`  Stream  `

Identifier for a given Stream.

`  offset  `

`  int64  `

Position in the stream.

## StreamStatus

Progress information for a given Stream.

Fields

`  estimated_row_count  `

`  int64  `

Number of estimated rows in the current stream. May change over time as different readers in the stream progress at rates which are relatively fast or slow.

`  fraction_consumed  `

`  float  `

A value in the range \[0.0, 1.0\] that represents the fraction of rows assigned to this stream that have been processed by the server. In the presence of read filters, the server may process more rows than it returns, so this value reflects progress through the pre-filtering rows.

This value is only populated for sessions created through the BALANCED sharding strategy.

`  progress  `

`  Progress  `

Represents the progress of the current stream.

`  is_splittable  `

`  bool  `

Whether this stream can be split. For sessions that use the LIQUID sharding strategy, this value is always false. For BALANCED sessions, this value is false when enough data have been read such that no more splits are possible at that point or beyond. For small tables or streams that are the result of a chain of splits, this value may never be true.

## TableModifiers

All fields in this message optional.

Fields

`  snapshot_time  `

`  Timestamp  `

The snapshot time of the table. If not set, interpreted as now.

## TableReadOptions

Options dictating how we read a table.

Fields

`  selected_fields[]  `

`  string  `

Optional. The names of the fields in the table to be returned. If no field names are specified, then all fields in the table are returned.

Nested fields -- the child elements of a STRUCT field -- can be selected individually using their fully-qualified names, and will be returned as record fields containing only the selected nested fields. If a STRUCT field is specified in the selected fields list, all of the child elements will be returned.

As an example, consider a table with the following schema:

{ "name": "struct\_field", "type": "RECORD", "mode": "NULLABLE", "fields": \[ { "name": "string\_field1", "type": "STRING", . "mode": "NULLABLE" }, { "name": "string\_field2", "type": "STRING", "mode": "NULLABLE" } \] }

Specifying "struct\_field" in the selected fields list will result in a read session schema with the following logical structure:

struct\_field { string\_field1 string\_field2 }

Specifying "struct\_field.string\_field1" in the selected fields list will result in a read session schema with the following logical structure:

struct\_field { string\_field1 }

The order of the fields in the read session schema is derived from the table schema and does not correspond to the order in which the fields are specified in this list.

`  row_restriction  `

`  string  `

Optional. SQL text filtering statement, similar to a WHERE clause in a SQL query. Aggregates are not supported.

Examples: "int\_field \> 5" "date\_field = CAST('2014-9-27' as DATE)" "nullable\_field is not NULL" "st\_equals(geo\_field, st\_geofromtext("POINT(2, 2)"))" "numeric\_field BETWEEN 1.0 AND 5.0"

Restricted to a maximum length for 1 MB.

## TableReference

Table reference that includes just the 3 strings needed to identify a table.

Fields

`  project_id  `

`  string  `

The assigned project ID of the project.

`  dataset_id  `

`  string  `

The ID of the dataset in the above project.

`  table_id  `

`  string  `

The ID of the table in the above dataset.

## ThrottleStatus

Information on if the current connection is being throttled.

Fields

`  throttle_percent  `

`  int32  `

How much this connection is being throttled. 0 is no throttling, 100 is completely throttled.
