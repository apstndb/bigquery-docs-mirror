---
name: documents/docs.cloud.google.com/bigquery/docs/reference/storage/rpc
uri: https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc
title: BigQuery Storage API
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

## Service: bigquerystorage.googleapis.com

The Service name `bigquerystorage.googleapis.com` is needed to create RPC client stubs.

## [`google.cloud.bigquery.storage.v1.BigQueryRead`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.BigQueryRead)

| Methods                                                                                                                                                                                   |                                                                         |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
| [`CreateReadSession`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.BigQueryRead.CreateReadSession) | Creates a new read session.                                             |
| [`ReadRows`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.BigQueryRead.ReadRows)                   | Reads rows from the stream in the format prescribed by the ReadSession. |
| [`SplitReadStream`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.BigQueryRead.SplitReadStream)     | Splits a given `ReadStream` into two `ReadStream` objects.              |

## [`google.cloud.bigquery.storage.v1.BigQueryWrite`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.BigQueryWrite)

| Methods                                                                                                                                                                                                |                                                                                         |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------|
| [`AppendRows`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.BigQueryWrite.AppendRows)                           | Appends data to the given stream.                                                       |
| [`BatchCommitWriteStreams`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.BigQueryWrite.BatchCommitWriteStreams) | Atomically commits a group of `PENDING` streams that belong to the same `parent` table. |
| [`CreateWriteStream`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.BigQueryWrite.CreateWriteStream)             | Creates a write stream to the given table.                                              |
| [`FinalizeWriteStream`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.BigQueryWrite.FinalizeWriteStream)         | Finalize a write stream so that no new data can be appended to the stream.              |
| [`FlushRows`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.BigQueryWrite.FlushRows)                             | Flushes rows to a BUFFERED stream.                                                      |
| [`GetWriteStream`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#google.cloud.bigquery.storage.v1.BigQueryWrite.GetWriteStream)                   | Gets information about a write stream.                                                  |

## [`google.cloud.bigquery.storage.v1beta1.BigQueryStorage`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1beta1#google.cloud.bigquery.storage.v1beta1.BigQueryStorage)

| Methods                                                                                                                                                                                                                        |                                                                         |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
| [`BatchCreateReadSessionStreams`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1beta1#google.cloud.bigquery.storage.v1beta1.BigQueryStorage.BatchCreateReadSessionStreams) | Creates additional streams for a ReadSession.                           |
| [`CreateReadSession`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1beta1#google.cloud.bigquery.storage.v1beta1.BigQueryStorage.CreateReadSession)                         | Creates a new read session.                                             |
| [`FinalizeStream`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1beta1#google.cloud.bigquery.storage.v1beta1.BigQueryStorage.FinalizeStream)                               | Causes a single stream in a ReadSession to gracefully stop.             |
| [`ReadRows`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1beta1#google.cloud.bigquery.storage.v1beta1.BigQueryStorage.ReadRows)                                           | Reads rows from the table in the format prescribed by the read session. |
| [`SplitReadStream`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1beta1#google.cloud.bigquery.storage.v1beta1.BigQueryStorage.SplitReadStream)                             | Splits a given read stream into two Streams.                            |

## [`google.cloud.bigquery.storage.v1beta2.BigQueryRead`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1beta2#google.cloud.bigquery.storage.v1beta2.BigQueryRead)

| Methods                                                                                                                                                                                             |                                                                         |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
| [`CreateReadSession`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1beta2#google.cloud.bigquery.storage.v1beta2.BigQueryRead.CreateReadSession) | Creates a new read session.                                             |
| [`ReadRows`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1beta2#google.cloud.bigquery.storage.v1beta2.BigQueryRead.ReadRows)                   | Reads rows from the stream in the format prescribed by the ReadSession. |
| [`SplitReadStream`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1beta2#google.cloud.bigquery.storage.v1beta2.BigQueryRead.SplitReadStream)     | Splits a given `ReadStream` into two `ReadStream` objects.              |

## [`google.cloud.bigquery.storage.v1beta2.BigQueryWrite`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1beta2#google.cloud.bigquery.storage.v1beta2.BigQueryWrite)

> This item is deprecated!

| Methods                                                                                                                                                                                                                               |                                                                                         |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------|
| [`AppendRows`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1beta2#google.cloud.bigquery.storage.v1beta2.BigQueryWrite.AppendRows)` `**`(deprecated)`**                           | Appends data to the given stream.                                                       |
| [`BatchCommitWriteStreams`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1beta2#google.cloud.bigquery.storage.v1beta2.BigQueryWrite.BatchCommitWriteStreams)` `**`(deprecated)`** | Atomically commits a group of `PENDING` streams that belong to the same `parent` table. |
| [`CreateWriteStream`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1beta2#google.cloud.bigquery.storage.v1beta2.BigQueryWrite.CreateWriteStream)` `**`(deprecated)`**             | Creates a write stream to the given table.                                              |
| [`FinalizeWriteStream`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1beta2#google.cloud.bigquery.storage.v1beta2.BigQueryWrite.FinalizeWriteStream)` `**`(deprecated)`**         | Finalize a write stream so that no new data can be appended to the stream.              |
| [`FlushRows`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1beta2#google.cloud.bigquery.storage.v1beta2.BigQueryWrite.FlushRows)` `**`(deprecated)`**                             | Flushes rows to a BUFFERED stream.                                                      |
| [`GetWriteStream`](https://docs.cloud.google.com/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1beta2#google.cloud.bigquery.storage.v1beta2.BigQueryWrite.GetWriteStream)` `**`(deprecated)`**                   | Gets a write stream.                                                                    |
