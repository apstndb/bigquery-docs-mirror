---
name: documents/docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1
uri: https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1
title: Package google.cloud.bigquery.storage.v1
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

## Index

- [`BigQueryRead`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.BigQueryRead) (interface)
- [`BigQueryWrite`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.BigQueryWrite) (interface)
- [`AppendRowsRequest`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.AppendRowsRequest) (message)
- [`AppendRowsRequest.MissingValueInterpretation`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.AppendRowsRequest.MissingValueInterpretation) (enum)
- [`AppendRowsRequest.ProtoData`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.AppendRowsRequest.ProtoData) (message)
- [`AppendRowsResponse`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.AppendRowsResponse) (message)
- [`AppendRowsResponse.AppendResult`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.AppendRowsResponse.AppendResult) (message)
- [`ArrowRecordBatch`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.ArrowRecordBatch) (message)
- [`ArrowSchema`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.ArrowSchema) (message)
- [`ArrowSerializationOptions`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.ArrowSerializationOptions) (message)
- [`ArrowSerializationOptions.CompressionCodec`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.ArrowSerializationOptions.CompressionCodec) (enum)
- [`ArrowSerializationOptions.PicosTimestampPrecision`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.ArrowSerializationOptions.PicosTimestampPrecision) (enum)
- [`AvroRows`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.AvroRows) (message)
- [`AvroSchema`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.AvroSchema) (message)
- [`AvroSerializationOptions`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.AvroSerializationOptions) (message)
- [`AvroSerializationOptions.PicosTimestampPrecision`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.AvroSerializationOptions.PicosTimestampPrecision) (enum)
- [`BatchCommitWriteStreamsRequest`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.BatchCommitWriteStreamsRequest) (message)
- [`BatchCommitWriteStreamsResponse`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.BatchCommitWriteStreamsResponse) (message)
- [`ClientStats`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.ClientStats) (message)
- [`ClientStats.RequestStats`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.ClientStats.RequestStats) (message)
- [`ClientStats.WindowStats`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.ClientStats.WindowStats) (message)
- [`CreateReadSessionRequest`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.CreateReadSessionRequest) (message)
- [`CreateWriteStreamRequest`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.CreateWriteStreamRequest) (message)
- [`DataFormat`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.DataFormat) (enum)
- [`FinalizeWriteStreamRequest`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.FinalizeWriteStreamRequest) (message)
- [`FinalizeWriteStreamResponse`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.FinalizeWriteStreamResponse) (message)
- [`FlushRowsRequest`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.FlushRowsRequest) (message)
- [`FlushRowsResponse`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.FlushRowsResponse) (message)
- [`GetWriteStreamRequest`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.GetWriteStreamRequest) (message)
- [`ProtoRows`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.ProtoRows) (message)
- [`ProtoSchema`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.ProtoSchema) (message)
- [`ReadRowsRequest`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.ReadRowsRequest) (message)
- [`ReadRowsResponse`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.ReadRowsResponse) (message)
- [`ReadSession`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.ReadSession) (message)
- [`ReadSession.TableModifiers`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.ReadSession.TableModifiers) (message)
- [`ReadSession.TableReadOptions`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.ReadSession.TableReadOptions) (message)
- [`ReadStream`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.ReadStream) (message)
- [`RowError`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.RowError) (message)
- [`RowError.RowErrorCode`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.RowError.RowErrorCode) (enum)
- [`SplitReadStreamRequest`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.SplitReadStreamRequest) (message)
- [`SplitReadStreamResponse`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.SplitReadStreamResponse) (message)
- [`StorageError`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.StorageError) (message)
- [`StorageError.StorageErrorCode`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.StorageError.StorageErrorCode) (enum)
- [`StreamStats`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.StreamStats) (message)
- [`StreamStats.Progress`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.StreamStats.Progress) (message)
- [`TableFieldSchema`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.TableFieldSchema) (message)
- [`TableFieldSchema.Mode`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.TableFieldSchema.Mode) (enum)
- [`TableFieldSchema.Type`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.TableFieldSchema.Type) (enum)
- [`TableSchema`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.TableSchema) (message)
- [`ThrottleState`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.ThrottleState) (message)
- [`WriteStream`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.WriteStream) (message)
- [`WriteStream.Type`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.WriteStream.Type) (enum)
- [`WriteStreamView`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.WriteStreamView) (enum)

## BigQueryRead

BigQuery Read API.

The Read API can be used to read data from BigQuery.

**CreateReadSession**

`rpc CreateReadSession( `[`CreateReadSessionRequest`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.CreateReadSessionRequest)` ) returns ( `[`ReadSession`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.ReadSession)` )`

Creates a new read session. A read session divides the contents of a BigQuery table into one or more streams, which can then be used to read data from the table. The read session also specifies properties of the data to be read, such as a list of columns or a push-down filter describing the rows to be returned.

A particular row can be read by at most one stream. When the caller has reached the end of each stream in the session, then all the data in the table has been read.

Data is assigned to each stream such that roughly the same number of rows can be read from each stream. Because the server-side unit for assigning data is collections of rows, the API does not guarantee that each stream will return the same number or rows. Additionally, the limits are enforced based on the number of pre-filtered rows, so some filters can lead to lopsided assignments.

Read sessions automatically expire 6 hours after they are created and do not require manual clean-up by the caller.

**ReadRows**

`rpc ReadRows( `[`ReadRowsRequest`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.ReadRowsRequest)` ) returns ( `[`ReadRowsResponse`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.ReadRowsResponse)` )`

Reads rows from the stream in the format prescribed by the ReadSession. Each response contains one or more table rows, up to a maximum of 128 MB per response; read requests which attempt to read individual rows larger than 128 MB will fail.

Each request also returns a set of stream statistics reflecting the current state of the stream.

**SplitReadStream**

`rpc SplitReadStream( `[`SplitReadStreamRequest`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.SplitReadStreamRequest)` ) returns ( `[`SplitReadStreamResponse`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.SplitReadStreamResponse)` )`

Splits a given `ReadStream` into two `ReadStream` objects. These `ReadStream` objects are referred to as the primary and the residual streams of the split. The original `ReadStream` can still be read from in the same manner as before. Both of the returned `ReadStream` objects can also be read from, and the rows returned by both child streams will be the same as the rows read from the original stream.

Moreover, the two child streams will be allocated back-to-back in the original `ReadStream` . Concretely, it is guaranteed that for streams original, primary, and residual, that original\[0-j\] = primary\[0-j\] and original\[j-n\] = residual\[0-m\] once the streams have been read to completion.

## BigQueryWrite

BigQuery Write API.

The Write API can be used to write data to BigQuery.

For supplementary information about the Write API, see: <https://cloud.google.com/bigquery/docs/write-api>

**AppendRows**

`rpc AppendRows( `[`AppendRowsRequest`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.AppendRowsRequest)` ) returns ( `[`AppendRowsResponse`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.AppendRowsResponse)` )`

Appends data to the given stream.

If `offset` is specified, the `offset` is checked against the end of stream. The server returns `OUT_OF_RANGE` in `AppendRowsResponse` if an attempt is made to append to an offset beyond the current end of the stream or `ALREADY_EXISTS` if user provides an `offset` that has already been written to. User can retry with adjusted offset within the same RPC connection. If `offset` is not specified, append happens at the end of the stream.

The response contains an optional offset at which the append happened. No offset information will be returned for appends to a default stream.

Responses are received in the same order in which requests are sent. There will be one response for each successful inserted request. Responses may optionally embed error information if the originating AppendRequest was not successfully processed.

The specifics of when successfully appended data is made visible to the table are governed by the type of stream:

- For COMMITTED streams (which includes the default stream), data is visible immediately upon successful append.

- For BUFFERED streams, data is made visible via a subsequent `FlushRows` rpc which advances a cursor to a newer offset in the stream.

- For PENDING streams, data is not made visible until the stream itself is finalized (via the `FinalizeWriteStream` rpc), and the stream is explicitly committed via the `BatchCommitWriteStreams` rpc.

**BatchCommitWriteStreams**

`rpc BatchCommitWriteStreams( `[`BatchCommitWriteStreamsRequest`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.BatchCommitWriteStreamsRequest)` ) returns ( `[`BatchCommitWriteStreamsResponse`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.BatchCommitWriteStreamsResponse)` )`

Atomically commits a group of `PENDING` streams that belong to the same `parent` table.

Streams must be finalized before commit and cannot be committed multiple times. Once a stream is committed, data in the stream becomes available for read operations.

**CreateWriteStream**

`rpc CreateWriteStream( `[`CreateWriteStreamRequest`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.CreateWriteStreamRequest)` ) returns ( `[`WriteStream`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.WriteStream)` )`

Creates a write stream to the given table. Additionally, every table has a special stream named '\_default' to which data can be written. This stream doesn't need to be created using CreateWriteStream. It is a stream that can be used simultaneously by any number of clients. Data written to this stream is considered committed as soon as an acknowledgement is received.

**FinalizeWriteStream**

`rpc FinalizeWriteStream( `[`FinalizeWriteStreamRequest`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.FinalizeWriteStreamRequest)` ) returns ( `[`FinalizeWriteStreamResponse`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.FinalizeWriteStreamResponse)` )`

Finalize a write stream so that no new data can be appended to the stream. Finalize is not supported on the '\_default' stream.

**FlushRows**

`rpc FlushRows( `[`FlushRowsRequest`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.FlushRowsRequest)` ) returns ( `[`FlushRowsResponse`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.FlushRowsResponse)` )`

Flushes rows to a BUFFERED stream.

If users are appending rows to BUFFERED stream, flush operation is required in order for the rows to become available for reading. A Flush operation flushes up to any previously flushed offset in a BUFFERED stream, to the offset specified in the request.

Flush is not supported on the \_default stream, since it is not BUFFERED.

**GetWriteStream**

`rpc GetWriteStream( `[`GetWriteStreamRequest`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.GetWriteStreamRequest)` ) returns ( `[`WriteStream`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.WriteStream)` )`

Gets information about a write stream.

## AppendRowsRequest

Request message for `AppendRows` .

Because AppendRows is a bidirectional streaming RPC, certain parts of the AppendRowsRequest need only be specified for the first request before switching table destinations. You can also switch table destinations within the same connection for the default stream.

The size of a single AppendRowsRequest must be less than 20 MB in size. Requests larger than this return an error, typically `INVALID_ARGUMENT` .

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
<td><code>write_stream</code></td>
<td><p><code>string</code></p>
<p>Required. The write_stream identifies the append operation. It must be provided in the following scenarios:</p>
<ul>
<li><p>In the first request to an AppendRows connection.</p></li>
<li><p>In all subsequent requests to an AppendRows connection, if you use the same connection to write to multiple tables or change the input schema for default streams.</p></li>
</ul>
<p>For explicitly created write streams, the format is:</p>
<ul>
<li><code>projects/{project}/datasets/{dataset}/tables/{table}/streams/{id}</code></li>
</ul>
<p>For the special default stream, the format is:</p>
<ul>
<li><code>projects/{project}/datasets/{dataset}/tables/{table}/streams/_default</code> .</li>
</ul>
<p>An example of a possible sequence of requests with write_stream fields within a single connection:</p>
<ul>
<li><p>r1: {write_stream: stream_name_1}</p></li>
<li><p>r2: {write_stream: /*omit*/}</p></li>
<li><p>r3: {write_stream: /*omit*/}</p></li>
<li><p>r4: {write_stream: stream_name_2}</p></li>
<li><p>r5: {write_stream: stream_name_2}</p></li>
</ul>
<p>The destination changed in request_4, so the write_stream field must be populated in all subsequent requests in this stream.</p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>writeStream</code> :</p>
<ul>
<li><code>bigquery.tables.updateData</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>offset</code></td>
<td><p><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#int64-value"><code>Int64Value</code></a></p>
<p>If present, the write is only performed if the next append offset is same as the provided value. If not present, the write is performed at the current end of stream. Specifying a value for this field is not allowed when calling AppendRows for the '_default' stream.</p></td>
</tr>
<tr class="odd">
<td><code>trace_id</code></td>
<td><p><code>string</code></p>
<p>Id set by client to annotate its identity. Only initial request setting is respected.</p></td>
</tr>
<tr class="even">
<td><code>missing_value_interpretations</code></td>
<td><p><code>map&lt;string, </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.AppendRowsRequest.MissingValueInterpretation"><code>MissingValueInterpretation</code></a><code> &gt;</code></p>
<p>A map to indicate how to interpret missing value for some fields. Missing values are fields present in user schema but missing in rows. The key is the field name. The value is the interpretation of missing values for the field.</p>
<p>For example, a map {'foo': NULL_VALUE, 'bar': DEFAULT_VALUE} means all missing values in field foo are interpreted as NULL, all missing values in field bar are interpreted as the default value of field bar in table schema.</p>
<p>If a field is not in this map and has missing values, the missing values in this field are interpreted as NULL.</p>
<p>This field only applies to the current request, it won't affect other requests on the connection.</p>
<p>Currently, field name can only be top-level column name, can't be a struct field path like 'foo.bar'.</p></td>
</tr>
<tr class="odd">
<td><code>client_stats</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.ClientStats"><code>ClientStats</code></a></p>
<p>Optional. Stats and telemetry data gathered on the client side.</p></td>
</tr>
<tr class="even">
<td>Union field <code>rows</code> . Input rows. The <code>writer_schema</code> field must be specified at the initial request and currently, it will be ignored if specified in following requests. Following requests must have data in the same format as the initial request. <code>rows</code> can be only one of the following:</td>
<td></td>
</tr>
<tr class="odd">
<td><code>proto_rows</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.AppendRowsRequest.ProtoData"><code>ProtoData</code></a></p>
<p>Rows in proto format.</p></td>
</tr>
</tbody>
</table>

## MissingValueInterpretation

An enum to indicate how to interpret missing values of fields that are present in user schema but missing in rows. A missing value can represent a NULL or a column default value defined in BigQuery table schema.

| Enums                                      |                                                                                                       |
|--------------------------------------------|-------------------------------------------------------------------------------------------------------|
| `MISSING_VALUE_INTERPRETATION_UNSPECIFIED` | Invalid missing value interpretation. Requests with this value will be rejected.                      |
| `NULL_VALUE`                               | Missing value is interpreted as NULL.                                                                 |
| `DEFAULT_VALUE`                            | Missing value is interpreted as column default value if declared in the table schema, NULL otherwise. |

## ProtoData

ProtoData contains the data rows and schema when constructing append requests.

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
<td><code>writer_schema</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.ProtoSchema"><code>ProtoSchema</code></a></p>
<p>Optional. The protocol buffer schema used to serialize the data. Provide this value whenever:</p>
<ul>
<li><p>You send the first request of an RPC connection.</p></li>
<li><p>You change the input schema.</p></li>
<li><p>You specify a new destination table.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><code>rows</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.ProtoRows"><code>ProtoRows</code></a></p>
<p>Required. Serialized row data in protobuf message format. Currently, the backend expects the serialized rows to adhere to proto2 semantics when appending rows, particularly with respect to how default values are encoded.</p></td>
</tr>
</tbody>
</table>

## AppendRowsResponse

Response message for `AppendRows` .

| Fields                                                                |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|-----------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `updated_schema`                                                      | [`TableSchema`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.TableSchema) If backend detects a schema update, pass it to user so that user can use it to input new type of message. It will be empty when no schema updates have occurred.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `row_errors[]`                                                        | [`RowError`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.RowError) If a request failed due to corrupted rows, no rows in the batch will be appended. The API will return row level error info, so that the caller can remove the bad rows and retry the request.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `write_stream`                                                        | `string` The target of the append operation. Matches the write_stream in the corresponding request.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| Union field `response` . `response` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `append_result`                                                       | [`AppendResult`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.AppendRowsResponse.AppendResult) Result if the append is successful.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `error`                                                               | [`Status`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.rpc#google.rpc.Status) Error returned when problems were encountered. If present, it indicates rows were not accepted into the system. Users can retry or continue with other append requests within the same connection. Additional information about error signalling: ALREADY_EXISTS: Happens when an append specified an offset, and the backend already has received data at this offset. Typically encountered in retry scenarios, and can be ignored. OUT_OF_RANGE: Returned when the specified offset in the stream is beyond the current end of the stream. INVALID_ARGUMENT: Indicates a malformed request or data. ABORTED: Request processing is aborted because of prior failures. The request can be retried if previous failure is addressed. INTERNAL: Indicates server side error(s) that can be retried. |

## AppendResult

AppendResult is returned for successful append requests.

| Fields   |                                                                                                                                                                                                       |
|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `offset` | [`Int64Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#int64-value) The row offset at which the last append occurred. The offset will not be set if appending using default streams. |

## ArrowRecordBatch

Arrow RecordBatch.

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
<td><code>serialized_record_batch</code></td>
<td><p><code>bytes</code></p>
<p>IPC-serialized Arrow RecordBatch.</p></td>
</tr>
<tr class="even">
<td><code>row_count </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>int64</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>[Deprecated] The count of rows in <code>serialized_record_batch</code> . Please use the format-independent ReadRowsResponse.row_count instead.</p></td>
</tr>
</tbody>
</table>

## ArrowSchema

Arrow schema as specified in <https://arrow.apache.org/docs/python/api/datatypes.html> and serialized to bytes using IPC: <https://arrow.apache.org/docs/format/Columnar.html#serialization-and-interprocess-communication-ipc>

See code samples on how this message can be deserialized.

| Fields              |                                      |
|---------------------|--------------------------------------|
| `serialized_schema` | `bytes` IPC serialized Arrow schema. |

## ArrowSerializationOptions

Contains options specific to Arrow Serialization.

| Fields                      |                                                                                                                                                                                                                                                                                                                 |
|-----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `buffer_compression`        | [`CompressionCodec`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.ArrowSerializationOptions.CompressionCodec) The compression codec to use for Arrow buffers in serialized record batches.                               |
| `picos_timestamp_precision` | [`PicosTimestampPrecision`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.ArrowSerializationOptions.PicosTimestampPrecision) Optional. Set timestamp precision option. If not set, the default precision is microseconds. |

## CompressionCodec

Compression codec's supported by Arrow.

| Enums                     |                                                                             |
|---------------------------|-----------------------------------------------------------------------------|
| `COMPRESSION_UNSPECIFIED` | If unspecified no compression will be used.                                 |
| `LZ4_FRAME`               | LZ4 Frame ( <https://github.com/lz4/lz4/blob/dev/doc/lz4_Frame_format.md> ) |
| `ZSTD`                    | Zstandard compression.                                                      |

## PicosTimestampPrecision

The precision of the timestamp value in the Avro message. This precision will **only** be applied to the column(s) with the `TIMESTAMP_PICOS` type.

| Enums                                   |                                                                                                                                                                |
|-----------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `PICOS_TIMESTAMP_PRECISION_UNSPECIFIED` | Unspecified timestamp precision. The default precision is microseconds.                                                                                        |
| `TIMESTAMP_PRECISION_MICROS`            | Timestamp values returned by Read API will be truncated to microsecond level precision. The value will be encoded as Arrow TIMESTAMP type in a 64 bit integer. |
| `TIMESTAMP_PRECISION_NANOS`             | Timestamp values returned by Read API will be truncated to nanosecond level precision. The value will be encoded as Arrow TIMESTAMP type in a 64 bit integer.  |
| `TIMESTAMP_PRECISION_PICOS`             | Read API will return full precision picosecond value. The value will be encoded as a string which conforms to ISO 8601 format.                                 |

## AvroRows

Avro rows.

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
<td><code>serialized_binary_rows</code></td>
<td><p><code>bytes</code></p>
<p>Binary serialized rows in a block.</p></td>
</tr>
<tr class="even">
<td><code>row_count </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>int64</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>[Deprecated] The count of rows in the returning block. Please use the format-independent ReadRowsResponse.row_count instead.</p></td>
</tr>
</tbody>
</table>

## AvroSchema

Avro schema.

| Fields   |                                                                                                   |
|----------|---------------------------------------------------------------------------------------------------|
| `schema` | `string` Json serialized schema, as described at <https://avro.apache.org/docs/1.8.1/spec.html> . |

## AvroSerializationOptions

Contains options specific to Avro Serialization.

| Fields                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|---------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `enable_display_name_attribute` | `bool` Enable displayName attribute in Avro schema. The Avro specification requires field names to be alphanumeric. By default, in cases when column names do not conform to these requirements (e.g. non-ascii unicode codepoints) and Avro is requested as an output format, the CreateReadSession call will fail. Setting this field to true, populates avro field names with a placeholder value and populates a "displayName" attribute for every avro field with the original column name. |
| `picos_timestamp_precision`     | [`PicosTimestampPrecision`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.AvroSerializationOptions.PicosTimestampPrecision) Optional. Set timestamp precision option. If not set, the default precision is microseconds.                                                                                                                                                                                   |

## PicosTimestampPrecision

The precision of the timestamp value in the Avro message. This precision will **only** be applied to the column(s) with the `TIMESTAMP_PICOS` type.

| Enums                                   |                                                                                                                                                               |
|-----------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `PICOS_TIMESTAMP_PRECISION_UNSPECIFIED` | Unspecified timestamp precision. The default precision is microseconds.                                                                                       |
| `TIMESTAMP_PRECISION_MICROS`            | Timestamp values returned by Read API will be truncated to microsecond level precision. The value will be encoded as Avro TIMESTAMP type in a 64 bit integer. |
| `TIMESTAMP_PRECISION_NANOS`             | Timestamp values returned by Read API will be truncated to nanosecond level precision. The value will be encoded as Avro TIMESTAMP type in a 64 bit integer.  |
| `TIMESTAMP_PRECISION_PICOS`             | Read API will return full precision picosecond value. The value will be encoded as a string which conforms to ISO 8601 format.                                |

## BatchCommitWriteStreamsRequest

Request message for `BatchCommitWriteStreams` .

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
<td><code>parent</code></td>
<td><p><code>string</code></p>
<p>Required. Parent table that all the streams should belong to, in the form of <code>projects/{project}/datasets/{dataset}/tables/{table}</code> .</p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>bigquery.tables.updateData</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>write_streams[]</code></td>
<td><p><code>string</code></p>
<p>Required. The group of streams that will be committed atomically.</p></td>
</tr>
</tbody>
</table>

## BatchCommitWriteStreamsResponse

Response message for `BatchCommitWriteStreams` .

| Fields            |                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `commit_time`     | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) The time at which streams were committed in microseconds granularity. This field will only exist when there are no stream errors. **Note** if this field is not set, it means the commit was not successful.                                                                                                                                  |
| `stream_errors[]` | [`StorageError`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.StorageError) Stream level error if commit failed. Only streams with error will be in the list. If empty, there is no error and all streams are committed successfully. If non empty, certain streams have errors and ZERO stream is committed due to atomicity guarantee. |

## ClientStats

Stats and telemetry data gathered on the client side about requests being sent to the BigQuery Storage service, for internal use only.

| Fields          |                                                                                                                                                                                                             |
|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `request_stats` | [`RequestStats`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.ClientStats.RequestStats) Optional. Per-request stats. |
| `window_stats`  | [`WindowStats`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.ClientStats.WindowStats) Optional. Windowed stats.      |

## RequestStats

Stats and telemetry data gathered on the client side about a single request.

| Fields                  |                                                                                                                                                           |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| `send_time_millis`      | `int64` Optional. Timestamp indicating when the request was sent over the network, expressed in epoch milliseconds.                                       |
| `queued_requests_count` | `int64` Optional. Number of pending requests at the moment this request was sent. This includes requests waiting to be sent, and those that are inflight. |

## WindowStats

Aggregate connection metrics over a window interval.

| Fields                            |                                                                                                                                                                                                                                         |
|-----------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `max_response_latency_millis`     | `int64` Optional. The maximum response latency observed in the window, expressed in milliseconds.                                                                                                                                       |
| `avg_response_latency_millis`     | `int64` Optional. The average response latency observed in the window, expressed in milliseconds.                                                                                                                                       |
| `longest_wait_no_response_millis` | `int64` Optional. The longest time spent waiting without receiving a response in the window. This could exceed max_response_latency_millis because the latter is evaluated only when a response is received. Expressed in milliseconds. |
| `requests_sent_count`             | `int64` Optional. How many requests were sent in the window.                                                                                                                                                                            |
| `responses_received_count`        | `int64` Optional. How many responses were received in the window.                                                                                                                                                                       |
| `bytes_sent_count`                | `int64` Optional. How many bytes were sent in the window.                                                                                                                                                                               |
| `window_start_time_epoch_millis`  | `int64` Optional. Start time of the window interval for which these stats are aggregated, expressed in epoch milliseconds.                                                                                                              |
| `window_millis`                   | `int64` Optional. Duration of the window interval for which these stats are aggregated, expressed in milliseconds.                                                                                                                      |

## CreateReadSessionRequest

Request message for `CreateReadSession` .

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
<td><code>parent</code></td>
<td><p><code>string</code></p>
<p>Required. The request project that owns the session, in the form of <code>projects/{project_id}</code> .</p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>bigquery.readsessions.create</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>read_session</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.ReadSession"><code>ReadSession</code></a></p>
<p>Required. Session to be created.</p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>readSession</code> :</p>
<ul>
<li><code>bigquery.tables.getData</code></li>
</ul></td>
</tr>
<tr class="odd">
<td><code>max_stream_count</code></td>
<td><p><code>int32</code></p>
<p>Max initial number of streams. If unset or zero, the server will provide a value of streams so as to produce reasonable throughput. Must be non-negative. The number of streams may be lower than the requested number, depending on the amount parallelism that is reasonable for the table. There is a default system max limit of 1,000.</p>
<p>This must be greater than or equal to preferred_min_stream_count. Typically, clients should either leave this unset to let the system to determine an upper bound OR set this a size for the maximum "units of work" it can gracefully handle.</p></td>
</tr>
<tr class="even">
<td><code>preferred_min_stream_count</code></td>
<td><p><code>int32</code></p>
<p>The minimum preferred stream count. This parameter can be used to inform the service that there is a desired lower bound on the number of streams. This is typically a target parallelism of the client (e.g. a Spark cluster with N-workers would set this to a low multiple of N to ensure good cluster utilization).</p>
<p>The system will make a best effort to provide at least this number of streams, but in some cases might provide less.</p></td>
</tr>
</tbody>
</table>

## CreateWriteStreamRequest

Request message for `CreateWriteStream` .

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
<td><code>parent</code></td>
<td><p><code>string</code></p>
<p>Required. Reference to the table to which the stream belongs, in the format of <code>projects/{project}/datasets/{dataset}/tables/{table}</code> .</p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>bigquery.tables.updateData</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>write_stream</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.WriteStream"><code>WriteStream</code></a></p>
<p>Required. Stream to be created.</p></td>
</tr>
</tbody>
</table>

## DataFormat

Data format for input or output data.

| Enums                     |                                                                                                                |
|---------------------------|----------------------------------------------------------------------------------------------------------------|
| `DATA_FORMAT_UNSPECIFIED` | Data format is unspecified.                                                                                    |
| `AVRO`                    | Avro is a standard open source row based file format. See <https://avro.apache.org/> for more details.         |
| `ARROW`                   | Arrow is a standard open source column-based message format. See <https://arrow.apache.org/> for more details. |

## FinalizeWriteStreamRequest

Request message for invoking `FinalizeWriteStream` .

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
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Name of the stream to finalize, in the form of <code>projects/{project}/datasets/{dataset}/tables/{table}/streams/{stream}</code> .</p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>bigquery.tables.updateData</code></li>
</ul></td>
</tr>
</tbody>
</table>

## FinalizeWriteStreamResponse

Response message for `FinalizeWriteStream` .

| Fields      |                                                 |
|-------------|-------------------------------------------------|
| `row_count` | `int64` Number of rows in the finalized stream. |

## FlushRowsRequest

Request message for `FlushRows` .

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
<td><code>write_stream</code></td>
<td><p><code>string</code></p>
<p>Required. The stream that is the target of the flush operation.</p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>writeStream</code> :</p>
<ul>
<li><code>bigquery.tables.updateData</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>offset</code></td>
<td><p><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#int64-value"><code>Int64Value</code></a></p>
<p>Ending offset of the flush operation. Rows before this offset(including this offset) will be flushed.</p></td>
</tr>
</tbody>
</table>

## FlushRowsResponse

Respond message for `FlushRows` .

| Fields   |                                                                          |
|----------|--------------------------------------------------------------------------|
| `offset` | `int64` The rows before this offset (including this offset) are flushed. |

## GetWriteStreamRequest

Request message for `GetWriteStreamRequest` .

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
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Name of the stream to get, in the form of <code>projects/{project}/datasets/{dataset}/tables/{table}/streams/{stream}</code> .</p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>bigquery.tables.get</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>view</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.WriteStreamView"><code>WriteStreamView</code></a></p>
<p>Indicates whether to get full or partial view of the WriteStream. If not set, view returned will be basic.</p></td>
</tr>
</tbody>
</table>

## ProtoRows

| Fields              |                                                                                                                                                                                  |
|---------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `serialized_rows[]` | `bytes` A sequence of rows serialized as a Protocol Buffer. See <https://developers.google.com/protocol-buffers/docs/overview> for more information on deserializing this field. |

## ProtoSchema

ProtoSchema describes the schema of the serialized protocol buffer data rows.

| Fields             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `proto_descriptor` | [`Any`](https://protobuf.dev/reference/protobuf/google.protobuf/#any) Descriptor for input message. The provided descriptor must be self contained, such that data rows sent can be fully decoded using only the single descriptor. For data rows that are compositions of multiple independent messages, this means the descriptor may need to be transformed to only use nested types: <https://developers.google.com/protocol-buffers/docs/proto#nested> For additional information for how proto types and values map onto BigQuery see: <https://cloud.google.com/bigquery/docs/write-api#data_type_conversions> |

## ReadRowsRequest

Request message for `ReadRows` .

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
<td><code>read_stream</code></td>
<td><p><code>string</code></p>
<p>Required. Stream to read rows from.</p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>readStream</code> :</p>
<ul>
<li><code>bigquery.readsessions.getData</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>offset</code></td>
<td><p><code>int64</code></p>
<p>The offset requested must be less than the last row read from Read. Requesting a larger offset is undefined. If not specified, start reading from offset zero.</p></td>
</tr>
</tbody>
</table>

## ReadRowsResponse

Response from calling `ReadRows` may include row data, progress and throttling information.

| Fields                                                                                                                                                                                                                                                                                                                                                            |                                                                                                                                                                                                                                                                     |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `row_count`                                                                                                                                                                                                                                                                                                                                                       | `int64` Number of serialized rows in the rows block.                                                                                                                                                                                                                |
| `stats`                                                                                                                                                                                                                                                                                                                                                           | [`StreamStats`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.StreamStats) Statistics for the stream.                                                                         |
| `throttle_state`                                                                                                                                                                                                                                                                                                                                                  | [`ThrottleState`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.ThrottleState) Throttling state. If unset, the latest response still describes the current throttling status. |
| Union field `rows` . Row data is returned in format specified during session creation. `rows` can be only one of the following:                                                                                                                                                                                                                                   |                                                                                                                                                                                                                                                                     |
| `avro_rows`                                                                                                                                                                                                                                                                                                                                                       | [`AvroRows`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.AvroRows) Serialized row data in AVRO format.                                                                      |
| `arrow_record_batch`                                                                                                                                                                                                                                                                                                                                              | [`ArrowRecordBatch`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.ArrowRecordBatch) Serialized row data in Arrow RecordBatch format.                                         |
| Union field `schema` . The schema for the read. If read_options.selected_fields is set, the schema may be different from the table schema as it will only contain the selected fields. This schema is equivalent to the one returned by CreateSession. This field is only populated in the first ReadRowsResponse RPC. `schema` can be only one of the following: |                                                                                                                                                                                                                                                                     |
| `avro_schema`                                                                                                                                                                                                                                                                                                                                                     | [`AvroSchema`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.AvroSchema) Output only. Avro schema.                                                                            |
| `arrow_schema`                                                                                                                                                                                                                                                                                                                                                    | [`ArrowSchema`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.ArrowSchema) Output only. Arrow schema.                                                                         |

## ReadSession

Information about the ReadSession.

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
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Output only. Unique identifier for the session, in the form <code>projects/{project_id}/locations/{location}/sessions/{session_id}</code> .</p></td>
</tr>
<tr class="even">
<td><code>expire_time</code></td>
<td><p><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp"><code>Timestamp</code></a></p>
<p>Output only. Time at which the session becomes invalid. After this time, subsequent requests to read this Session will return errors. The expire_time is automatically assigned and currently cannot be specified or updated.</p></td>
</tr>
<tr class="odd">
<td><code>data_format</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.DataFormat"><code>DataFormat</code></a></p>
<p>Immutable. Data format of the output data. DATA_FORMAT_UNSPECIFIED not supported.</p></td>
</tr>
<tr class="even">
<td><code>table</code></td>
<td><p><code>string</code></p>
<p>Immutable. Table that this ReadSession is reading from, in the form <code>projects/{project_id}/datasets/{dataset_id}/tables/{table_id}</code></p>
<p>Authorization requires one or more of the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permissions on the specified resource <code>table</code> :</p>
<ul>
<li><code>bigquery.tables.get</code></li>
<li><code>bigquery.tables.getData</code></li>
</ul></td>
</tr>
<tr class="odd">
<td><code>table_modifiers</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.ReadSession.TableModifiers"><code>TableModifiers</code></a></p>
<p>Optional. Any modifiers which are applied when reading from the specified table.</p></td>
</tr>
<tr class="even">
<td><code>read_options</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.ReadSession.TableReadOptions"><code>TableReadOptions</code></a></p>
<p>Optional. Read options for this session (e.g. column selection, filters).</p></td>
</tr>
<tr class="odd">
<td><code>streams[]</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.ReadStream"><code>ReadStream</code></a></p>
<p>Output only. A list of streams created with the session.</p>
<p>At least one stream is created with the session. In the future, larger request_stream_count values <em>may</em> result in this list being unpopulated, in that case, the user will need to use a List method to get the streams instead, which is not yet available.</p></td>
</tr>
<tr class="even">
<td><code>estimated_total_bytes_scanned</code></td>
<td><p><code>int64</code></p>
<p>Output only. An estimate on the number of bytes this session will scan when all streams are completely consumed. This estimate is based on metadata from the table which might be incomplete or stale.</p></td>
</tr>
<tr class="odd">
<td><code>estimated_total_physical_file_size</code></td>
<td><p><code>int64</code></p>
<p>Output only. A pre-projected estimate of the total physical size of files (in bytes) that this session will scan when all streams are consumed. This estimate is independent of the selected columns and can be based on incomplete or stale metadata from the table. This field is only set for BigLake tables.</p></td>
</tr>
<tr class="even">
<td><code>estimated_row_count</code></td>
<td><p><code>int64</code></p>
<p>Output only. An estimate on the number of rows present in this session's streams. This estimate is based on metadata from the table which might be incomplete or stale.</p></td>
</tr>
<tr class="odd">
<td><code>trace_id</code></td>
<td><p><code>string</code></p>
<p>Optional. ID set by client to annotate a session identity. This does not need to be strictly unique, but instead the same ID should be used to group logically connected sessions (e.g. All using the same ID for all sessions needed to complete a Spark SQL query is reasonable).</p>
<p>Maximum length is 256 bytes.</p></td>
</tr>
<tr class="even">
<td>Union field <code>schema</code> . The schema for the read. If read_options.selected_fields is set, the schema may be different from the table schema as it will only contain the selected fields. <code>schema</code> can be only one of the following:</td>
<td></td>
</tr>
<tr class="odd">
<td><code>avro_schema</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.AvroSchema"><code>AvroSchema</code></a></p>
<p>Output only. Avro schema.</p></td>
</tr>
<tr class="even">
<td><code>arrow_schema</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.ArrowSchema"><code>ArrowSchema</code></a></p>
<p>Output only. Arrow schema.</p></td>
</tr>
</tbody>
</table>

## TableModifiers

Additional attributes when reading a table.

| Fields          |                                                                                                                                                   |
|-----------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| `snapshot_time` | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) The snapshot time of the table. If not set, interpreted as now. |

## TableReadOptions

Options dictating how we read a table.

| Fields                                                                                                                      |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|-----------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `selected_fields[]`                                                                                                         | `string` Optional. The names of the fields in the table to be returned. If no field names are specified, then all fields in the table are returned. Nested fields -- the child elements of a STRUCT field -- can be selected individually using their fully-qualified names, and will be returned as record fields containing only the selected nested fields. If a STRUCT field is specified in the selected fields list, all of the child elements will be returned. As an example, consider a table with the following schema: { "name": "struct_field", "type": "RECORD", "mode": "NULLABLE", "fields": \[ { "name": "string_field1", "type": "STRING", . "mode": "NULLABLE" }, { "name": "string_field2", "type": "STRING", "mode": "NULLABLE" } \] } Specifying "struct_field" in the selected fields list will result in a read session schema with the following logical structure: struct_field { string_field1 string_field2 } Specifying "struct_field.string_field1" in the selected fields list will result in a read session schema with the following logical structure: struct_field { string_field1 } The order of the fields in the read session schema is derived from the table schema and does not correspond to the order in which the fields are specified in this list. |
| `row_restriction`                                                                                                           | `string` SQL text filtering statement, similar to a WHERE clause in a query. Aggregates are not supported. Examples: "int_field \> 5" "date_field = CAST('2014-9-27' as DATE)" "nullable_field is not NULL" "st_equals(geo_field, st_geofromtext("POINT(2, 2)"))" "numeric_field BETWEEN 1.0 AND 5.0" Restricted to a maximum length for 1 MB.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| Union field `output_format_serialization_options` . `output_format_serialization_options` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `arrow_serialization_options`                                                                                               | [`ArrowSerializationOptions`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.ArrowSerializationOptions) Optional. Options specific to the Apache Arrow output format.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `avro_serialization_options`                                                                                                | [`AvroSerializationOptions`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.AvroSerializationOptions) Optional. Options specific to the Apache Avro output format                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `sample_percentage`                                                                                                         | `double` Optional. Specifies a table sampling percentage. Specifically, the query planner will use TABLESAMPLE SYSTEM (sample_percentage PERCENT). The sampling percentage is applied at the data block granularity. It will randomly choose for each data block whether to read the rows in that data block. For more details, see <https://cloud.google.com/bigquery/docs/table-sampling> )                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |

## ReadStream

Information about a single stream that gets data out of the storage system. Most of the information about `ReadStream` instances is aggregated, making `ReadStream` lightweight.

| Fields |                                                                                                                                                |
|--------|------------------------------------------------------------------------------------------------------------------------------------------------|
| `name` | `string` Output only. Name of the stream, in the form `projects/{project_id}/locations/{location}/sessions/{session_id}/streams/{stream_id}` . |

## RowError

The message that presents row level error info in a request.

| Fields    |                                                                                                                                                                                                                      |
|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `index`   | `int64` Index of the malformed row in the request.                                                                                                                                                                   |
| `code`    | [`RowErrorCode`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.RowError.RowErrorCode) Structured error reason for a row error. |
| `message` | `string` Description of the issue encountered when processing the row.                                                                                                                                               |

## RowErrorCode

Error code for `RowError` .

| Enums                        |                                           |
|------------------------------|-------------------------------------------|
| `ROW_ERROR_CODE_UNSPECIFIED` | Default error.                            |
| `FIELDS_ERROR`               | One or more fields in the row has errors. |

## SplitReadStreamRequest

Request message for `SplitReadStream` .

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
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Name of the stream to split.</p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>bigquery.readsessions.update</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>fraction</code></td>
<td><p><code>double</code></p>
<p>A value in the range (0.0, 1.0) that specifies the fractional point at which the original stream should be split. The actual split point is evaluated on pre-filtered rows, so if a filter is provided, then there is no guarantee that the division of the rows between the new child streams will be proportional to this fractional value. Additionally, because the server-side unit for assigning data is collections of rows, this fraction will always map to a data storage boundary on the server side.</p></td>
</tr>
</tbody>
</table>

## SplitReadStreamResponse

Response message for `SplitReadStream` .

| Fields             |                                                                                                                                                                                                                                                                                                                       |
|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `primary_stream`   | [`ReadStream`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.ReadStream) Primary stream, which contains the beginning portion of \|original_stream\|. An empty value indicates that the original stream can no longer be split. |
| `remainder_stream` | [`ReadStream`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.ReadStream) Remainder stream, which contains the tail of \|original_stream\|. An empty value indicates that the original stream can no longer be split.            |

## StorageError

Structured custom BigQuery Storage error message. The error can be attached as error details in the returned rpc Status. In particular, the use of error codes allows more structured error handling, and reduces the need to evaluate unstructured error text strings.

| Fields          |                                                                                                                                                                                                                               |
|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `code`          | [`StorageErrorCode`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.StorageError.StorageErrorCode) BigQuery Storage specific error code. |
| `entity`        | `string` Name of the failed entity.                                                                                                                                                                                           |
| `error_message` | `string` Message that describes the error.                                                                                                                                                                                    |

## StorageErrorCode

Error code for `StorageError` .

| Enums                            |                                                                                                     |
|----------------------------------|-----------------------------------------------------------------------------------------------------|
| `STORAGE_ERROR_CODE_UNSPECIFIED` | Default error.                                                                                      |
| `TABLE_NOT_FOUND`                | Table is not found in the system.                                                                   |
| `STREAM_ALREADY_COMMITTED`       | Stream is already committed.                                                                        |
| `STREAM_NOT_FOUND`               | Stream is not found.                                                                                |
| `INVALID_STREAM_TYPE`            | Invalid Stream type. For example, you try to commit a stream that is not pending.                   |
| `INVALID_STREAM_STATE`           | Invalid Stream state. For example, you try to commit a stream that is not finalized or is garbaged. |
| `STREAM_FINALIZED`               | Stream is finalized.                                                                                |
| `SCHEMA_MISMATCH_EXTRA_FIELDS`   | There is a schema mismatch and it is caused by user schema has extra field than bigquery schema.    |
| `OFFSET_ALREADY_EXISTS`          | Offset already exists.                                                                              |
| `OFFSET_OUT_OF_RANGE`            | Offset out of range.                                                                                |
| `CMEK_NOT_PROVIDED`              | Customer-managed encryption key (CMEK) not provided for CMEK-enabled data.                          |
| `INVALID_CMEK_PROVIDED`          | Customer-managed encryption key (CMEK) was incorrectly provided.                                    |
| `CMEK_ENCRYPTION_ERROR`          | There is an encryption error while using customer-managed encryption key.                           |
| `KMS_SERVICE_ERROR`              | Key Management Service (KMS) service returned an error, which can be retried.                       |
| `KMS_PERMISSION_DENIED`          | Permission denied while using customer-managed encryption key.                                      |

## StreamStats

Estimated stream statistics for a given read Stream.

| Fields     |                                                                                                                                                                                                                       |
|------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `progress` | [`Progress`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.StreamStats.Progress) Represents the progress of the current stream. |

## Progress

| Fields              |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|---------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `at_response_start` | `double` The fraction of rows assigned to the stream that have been processed by the server so far, not including the rows in the current response message. This value, along with `at_response_end` , can be used to interpolate the progress made as the rows in the message are being processed using the following formula: `at_response_start + (at_response_end - at_response_start) * rows_processed_from_response / rows_in_response` . Note that if a filter is provided, the `at_response_end` value of the previous response may not necessarily be equal to the `at_response_start` value of the current response. |
| `at_response_end`   | `double` Similar to `at_response_start` , except that this value includes the rows in the current response.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |

## TableFieldSchema

TableFieldSchema defines a single field/column within a table schema.

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
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. The field name. The name must contain only letters (a-z, A-Z), numbers (0-9), or underscores (_), and must start with a letter or underscore. The maximum length is 128 characters.</p></td>
</tr>
<tr class="even">
<td><code>type</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.TableFieldSchema.Type"><code>Type</code></a></p>
<p>Required. The field data type.</p></td>
</tr>
<tr class="odd">
<td><code>mode</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.TableFieldSchema.Mode"><code>Mode</code></a></p>
<p>Optional. The field mode. The default value is NULLABLE.</p></td>
</tr>
<tr class="even">
<td><code>fields[]</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.TableFieldSchema"><code>TableFieldSchema</code></a></p>
<p>Optional. Describes the nested schema fields if the type property is set to STRUCT.</p></td>
</tr>
<tr class="odd">
<td><code>description</code></td>
<td><p><code>string</code></p>
<p>Optional. The field description. The maximum length is 1,024 characters.</p></td>
</tr>
<tr class="even">
<td><code>max_length</code></td>
<td><p><code>int64</code></p>
<p>Optional. Maximum length of values of this field for STRINGS or BYTES.</p>
<p>If max_length is not specified, no maximum length constraint is imposed on this field.</p>
<p>If type = "STRING", then max_length represents the maximum UTF-8 length of strings in this field.</p>
<p>If type = "BYTES", then max_length represents the maximum number of bytes in this field.</p>
<p>It is invalid to set this field if type is not "STRING" or "BYTES".</p></td>
</tr>
<tr class="odd">
<td><code>precision</code></td>
<td><p><code>int64</code></p>
<p>Optional. Precision (maximum number of total digits in base 10) and scale (maximum number of digits in the fractional part in base 10) constraints for values of this field for NUMERIC or BIGNUMERIC.</p>
<p>It is invalid to set precision or scale if type is not "NUMERIC" or "BIGNUMERIC".</p>
<p>If precision and scale are not specified, no value range constraint is imposed on this field insofar as values are permitted by the type.</p>
<p>Values of this NUMERIC or BIGNUMERIC field must be in this range when:</p>
<ul>
<li>Precision (P) and scale (S) are specified: [-10^(P-S) + 10^(-S), 10^(P-S) - 10^(-S)]</li>
<li>Precision (P) is specified but not scale (and thus scale is interpreted to be equal to zero): [-10^P + 1, 10^P - 1].</li>
</ul>
<p>Acceptable values for precision and scale if both are specified:</p>
<ul>
<li>If type = "NUMERIC": 1 &lt;= precision - scale &lt;= 29 and 0 &lt;= scale &lt;= 9.</li>
<li>If type = "BIGNUMERIC": 1 &lt;= precision - scale &lt;= 38 and 0 &lt;= scale &lt;= 38.</li>
</ul>
<p>Acceptable values for precision if only precision is specified but not scale (and thus scale is interpreted to be equal to zero):</p>
<ul>
<li>If type = "NUMERIC": 1 &lt;= precision &lt;= 29.</li>
<li>If type = "BIGNUMERIC": 1 &lt;= precision &lt;= 38.</li>
</ul>
<p>If scale is specified but not precision, then it is invalid.</p></td>
</tr>
<tr class="even">
<td><code>scale</code></td>
<td><p><code>int64</code></p>
<p>Optional. See documentation for precision.</p></td>
</tr>
<tr class="odd">
<td><code>default_value_expression</code></td>
<td><p><code>string</code></p>
<p>Optional. A SQL expression to specify the <a href="https://cloud.google.com/bigquery/docs/default-values">default value</a> for this field.</p></td>
</tr>
<tr class="even">
<td><code>timestamp_precision</code></td>
<td><p><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#int64-value"><code>Int64Value</code></a></p>
<p>Optional. Precision (maximum number of total digits in base 10) for seconds of TIMESTAMP type.</p>
<p>Possible values include:</p>
<ul>
<li>6 (Default, for TIMESTAMP type with microsecond precision)</li>
<li>12 (For TIMESTAMP type with picosecond precision)</li>
</ul></td>
</tr>
</tbody>
</table>

## Mode

| Enums              |               |
|--------------------|---------------|
| `MODE_UNSPECIFIED` | Illegal value |
| `NULLABLE`         |               |
| `REQUIRED`         |               |
| `REPEATED`         |               |

## Type

| Enums              |                                                 |
|--------------------|-------------------------------------------------|
| `TYPE_UNSPECIFIED` | Illegal value                                   |
| `STRING`           | 64K, UTF8                                       |
| `INT64`            | 64-bit signed                                   |
| `DOUBLE`           | 64-bit IEEE floating point                      |
| `STRUCT`           | Aggregate type                                  |
| `BYTES`            | 64K, Binary                                     |
| `BOOL`             | 2-valued                                        |
| `TIMESTAMP`        | 64-bit signed usec since UTC epoch              |
| `DATE`             | Civil date - Year, Month, Day                   |
| `TIME`             | Civil time - Hour, Minute, Second, Microseconds |
| `DATETIME`         | Combination of civil date and civil time        |
| `GEOGRAPHY`        | Geography object                                |
| `NUMERIC`          | Numeric value                                   |
| `BIGNUMERIC`       | BigNumeric value                                |
| `INTERVAL`         | Interval                                        |
| `JSON`             | JSON, String                                    |

## TableSchema

Schema of a table. This schema is a subset of google.cloud.bigquery.v2.TableSchema containing information necessary to generate valid message to write to BigQuery.

| Fields     |                                                                                                                                                                                                             |
|------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `fields[]` | [`TableFieldSchema`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.TableFieldSchema) Describes the fields in a table. |

## ThrottleState

Information on if the current connection is being throttled.

| Fields             |                                                                                                           |
|--------------------|-----------------------------------------------------------------------------------------------------------|
| `throttle_percent` | `int32` How much this connection is being throttled. Zero means no throttling, 100 means fully throttled. |

## WriteStream

Information about a single stream that gets data inside the storage system.

| Fields         |                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`         | `string` Output only. Name of the stream, in the form `projects/{project}/datasets/{dataset}/tables/{table}/streams/{stream}` .                                                                                                                                                                                                                                                                                                                           |
| `type`         | [`Type`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.WriteStream.Type) Immutable. Type of the stream.                                                                                                                                                                                                                                                             |
| `create_time`  | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Output only. Create time of the stream. For the \_default stream, this is the creation_time of the table.                                                                                                                                                                                                                                                               |
| `commit_time`  | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Output only. Commit time of the stream. If a stream is of `COMMITTED` type, then it will have a commit_time same as `create_time` . If the stream is of `PENDING` type, empty commit_time means it is not committed.                                                                                                                                                    |
| `table_schema` | [`TableSchema`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.TableSchema) Output only. The schema of the destination table. It is only returned in `CreateWriteStream` response. Caller should generate data that's compatible with this schema to send in initial `AppendRowsRequest` . The table schema could go out of date during the life time of the stream. |
| `location`     | `string` Output only. The geographic location where the stream's dataset resides. See <https://cloud.google.com/bigquery/docs/locations> for supported locations.                                                                                                                                                                                                                                                                                         |

## Type

Type enum of the stream.

| Enums              |                                                                                 |
|--------------------|---------------------------------------------------------------------------------|
| `TYPE_UNSPECIFIED` | Unknown type.                                                                   |
| `COMMITTED`        | Data will commit automatically and appear as soon as the write is acknowledged. |
| `PENDING`          | Data is invisible until the stream is committed.                                |
| `BUFFERED`         | Data is only visible up to the offset to which it was flushed.                  |

## WriteStreamView

WriteStreamView is a view enum that controls what details about a write stream should be returned.

| Enums                           |                                                                                                                                                                            |
|---------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `WRITE_STREAM_VIEW_UNSPECIFIED` | The default / unset value.                                                                                                                                                 |
| `BASIC`                         | The BASIC projection returns basic metadata about a write stream. The basic view does not include schema information. This is the default view returned by GetWriteStream. |
| `FULL`                          | The FULL projection returns all available write stream metadata, including the schema. CreateWriteStream returns the full projection of write stream metadata.             |
