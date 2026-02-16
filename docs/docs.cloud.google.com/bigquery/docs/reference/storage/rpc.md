## Service: bigquerystorage.googleapis.com

The Service name `  bigquerystorage.googleapis.com  ` is needed to create RPC client stubs.

## `         google.cloud.bigquery.storage.v1.BigQueryRead       `

Methods

`  CreateReadSession  `

Creates a new read session.

`  ReadRows  `

Reads rows from the stream in the format prescribed by the ReadSession.

`  SplitReadStream  `

Splits a given `  ReadStream  ` into two `  ReadStream  ` objects.

## `         google.cloud.bigquery.storage.v1.BigQueryWrite       `

Methods

`  AppendRows  `

Appends data to the given stream.

`  BatchCommitWriteStreams  `

Atomically commits a group of `  PENDING  ` streams that belong to the same `  parent  ` table.

`  CreateWriteStream  `

Creates a write stream to the given table.

`  FinalizeWriteStream  `

Finalize a write stream so that no new data can be appended to the stream.

`  FlushRows  `

Flushes rows to a BUFFERED stream.

`  GetWriteStream  `

Gets information about a write stream.

## `         google.cloud.bigquery.storage.v1beta1.BigQueryStorage       `

Methods

`  BatchCreateReadSessionStreams  `

Creates additional streams for a ReadSession.

`  CreateReadSession  `

Creates a new read session.

`  FinalizeStream  `

Causes a single stream in a ReadSession to gracefully stop.

`  ReadRows  `

Reads rows from the table in the format prescribed by the read session.

`  SplitReadStream  `

Splits a given read stream into two Streams.

## `         google.cloud.bigquery.storage.v1beta2.BigQueryRead       `

Methods

`  CreateReadSession  `

Creates a new read session.

`  ReadRows  `

Reads rows from the stream in the format prescribed by the ReadSession.

`  SplitReadStream  `

Splits a given `  ReadStream  ` into two `  ReadStream  ` objects.

## `         google.cloud.bigquery.storage.v1beta2.BigQueryWrite       `

This item is deprecated\!

Methods

`  AppendRows  `  
**(deprecated)**

Appends data to the given stream.

`  BatchCommitWriteStreams  `  
**(deprecated)**

Atomically commits a group of `  PENDING  ` streams that belong to the same `  parent  ` table.

`  CreateWriteStream  `  
**(deprecated)**

Creates a write stream to the given table.

`  FinalizeWriteStream  `  
**(deprecated)**

Finalize a write stream so that no new data can be appended to the stream.

`  FlushRows  `  
**(deprecated)**

Flushes rows to a BUFFERED stream.

`  GetWriteStream  `  
**(deprecated)**

Gets a write stream.
