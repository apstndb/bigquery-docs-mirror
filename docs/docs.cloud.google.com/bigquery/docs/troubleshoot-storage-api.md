---
name: documents/docs.cloud.google.com/bigquery/docs/troubleshoot-storage-api
uri: https://docs.cloud.google.com/bigquery/docs/troubleshoot-storage-api
title: Troubleshoot the BigQuery Storage API errors
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# Troubleshoot the BigQuery Storage API errors

This document explains how to troubleshoot issues when you read or stream data in BigQuery using the BigQuery Storage Read API, the BigQuery Storage Write API (gRPC), or streaming inserts with the BigQuery Storage Write API (REST) ( `tabledata.insertAll` method).

## Analyze streaming telemetry with INFORMATION\_SCHEMA views

You can query `INFORMATION_SCHEMA` views to monitor streaming ingestion health, identify throughput bottlenecks, and inspect error codes over one-minute intervals:

  - **Storage Write API (gRPC):** query the [`INFORMATION_SCHEMA.WRITE_API_TIMELINE` views](https://docs.cloud.google.com/bigquery/docs/information-schema-write-api) to inspect gRPC streaming ingestion requests, total bytes and rows appended, and error counts by `error_code` .
  - **Storage Write API (REST):** query the [`INFORMATION_SCHEMA.STREAMING_TIMELINE` views](https://docs.cloud.google.com/bigquery/docs/information-schema-streaming) to inspect legacy REST `tabledata.insertAll` streaming requests and quota or rate limit errors.

The following example queries `INFORMATION_SCHEMA.WRITE_API_TIMELINE_BY_PROJECT` to retrieve error counts and ingested bytes for the Storage Write API (gRPC) over the past 24 hours:

    SELECT
      start_timestamp,
      error_code,
      SUM(total_requests) AS request_count,
      SUM(total_input_bytes) AS input_bytes
    FROM
      `region-REGION`.INFORMATION_SCHEMA.WRITE_API_TIMELINE_BY_PROJECT
    WHERE
      start_timestamp > TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 1 DAY)
      AND error_code IS NOT NULL
    GROUP BY
      start_timestamp,
      error_code
    ORDER BY
      start_timestamp DESC;

Replace `  REGION  ` with the dataset region name, such as `us` or `europe-west1` .

<span id="troubleshoot"></span>

## Troubleshoot Storage Read API errors

The following are common errors encountered when you use the Storage Read API:

  - Error: `Stream removed`  
    **Resolution:** Retry the Storage Read API request. This is likely a transient error that you can resolve by retrying the request. If the problem persists, [contact Cloud Customer Care](https://docs.cloud.google.com/bigquery/docs/getting-support) .

  - Error: `Stream expired`  
    **Cause:** This error occurs when the Storage Read API session reaches the [6-hour timeout](https://docs.cloud.google.com/bigquery/docs/reference/storage#create_a_session) .
    
    **Resolution:**

<!-- end list -->

1.  Increase the parallelism of the job.
2.  If the CPU utilization of the worker nodes is relatively consistent and doesn't exceed 85%, consider running the job on a larger machine type.
3.  Split the job into multiple jobs or smaller queries.

For more information about session management and reading data, see the [Storage Read API overview](https://docs.cloud.google.com/bigquery/docs/reference/storage) .

## Troubleshoot streaming inserts

The following sections discuss how to troubleshoot errors that occur when you [stream data into BigQuery using the Storage Write API (REST)](https://docs.cloud.google.com/bigquery/docs/write-api-rest) . For more information about how to resolve quota errors for streaming inserts, see [Streaming insert quota errors](https://docs.cloud.google.com/bigquery/docs/troubleshoot-quotas#ts-streaming-insert-quota) .

### Failure HTTP response codes

If you receive a failure HTTP response code, such as a network error, there's no way to tell whether the streaming insert succeeded. If you try to resend the request, you might get duplicated rows in your table. To help protect your table against duplication, set the `insertId` property when you send your request. BigQuery uses the `insertId` property for deduplication.

If you receive a permission error, an invalid table name error, or an exceeded quota error, no rows are inserted and the entire request fails.

### Success HTTP response codes

Even if you receive a [success HTTP response code](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/tabledata/insertAll#response-body) , you must check the `insertErrors` property of the response to determine whether the row insertions were successful, because BigQuery might be only partially successful at inserting the rows. You might encounter one of the following scenarios:

  - **All rows inserted successfully:** If the `insertErrors` property is an empty list, all of the rows were inserted successfully.
  - **Some rows inserted successfully:** Except in cases where there's a schema mismatch in any of the rows, rows indicated in the `insertErrors` property aren't inserted, and all other rows are inserted successfully. The `errors` property contains detailed information about why each unsuccessful row failed. The `index` property indicates the 0-based row index of the request that the error applies to.
  - **No rows inserted successfully:** If BigQuery encounters a schema mismatch on individual rows in the request, none of the rows are inserted and an `insertErrors` entry is returned for each row, even for rows that didn't have a schema mismatch. Rows that didn't have a schema mismatch have an error with the `reason` property set to `stopped` , and you can resend them as-is. Rows that failed include detailed information about the schema mismatch. To learn about the supported protocol buffer types for each BigQuery data type, see [Supported protocol buffer and Arrow data types](https://docs.cloud.google.com/bigquery/docs/supported-data-types) .

### Metadata errors for streaming inserts

Because the BigQuery streaming API is designed for high insertion rates, modifications to the underlying table metadata are eventually consistent when interacting with the streaming system. Most of the time, metadata changes propagate within minutes, but during this period API responses might reflect the inconsistent state of the table.

Some scenarios include the following:

  - **Schema changes:** Modifying the schema of a table that recently received streaming inserts can cause responses with schema mismatch errors because the streaming system might not immediately detect the schema change.
  - **Table creation or deletion:** Streaming to a nonexistent table returns a variation of a `notFound` response. A table created in response might not immediately be recognized by subsequent streaming inserts. Similarly, deleting or recreating a table can create a period of time where streaming inserts are delivered to the old table. The streaming inserts might not be present in the new table.
  - **Table truncation:** Truncating a table's data (by using a query job that uses a `writeDisposition` value of `WRITE_TRUNCATE` ) can similarly cause subsequent inserts during the consistency period to be dropped.

### Missing or unavailable data

Streaming inserts reside temporarily in write-optimized storage, which has different availability characteristics than managed storage. Certain operations in BigQuery don't interact with write-optimized storage, such as table copy jobs and API methods like `tabledata.list` . Recent streaming data isn't present in the destination table or output.

<span id="ts-streaming-insert-quota"></span>

### Streaming insert quota errors

This section provides tips for troubleshooting quota errors related to streaming data into BigQuery.

In certain regions, streaming inserts have a higher quota if you don't populate the `insertId` field for each row. For more information about quotas for streaming inserts, see [Streaming inserts](https://docs.cloud.google.com/bigquery/quotas#streaming_inserts) . The quota-related errors for BigQuery streaming depend on the presence or absence of `insertId` .

**Error message**

If the `insertId` field is empty, the following quota error is possible:

| Quota limit                  | Error message                                                                                                            |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| Bytes per second per project | Your entity with gaia\_id: GAIA\_ID , project: PROJECT\_ID in region: REGION exceeded quota for insert bytes per second. |

If the `insertId` field is populated, the following quota errors are possible:

| Quota limit                 | Error message                                                                            |
| --------------------------- | ---------------------------------------------------------------------------------------- |
| Rows per second per project | Your project: PROJECT\_ID in REGION exceeded quota for streaming insert rows per second. |
| Rows per second per table   | Your table: TABLE\_ID exceeded quota for streaming insert rows per second.               |
| Bytes per second per table  | Your table: TABLE\_ID exceeded quota for streaming insert bytes per second.              |

The purpose of the `insertId` field is to deduplicate inserted rows. If multiple inserts with the same `insertId` arrive within a few minutes' window, BigQuery writes a single version of the record. However, this automatic deduplication is not guaranteed. For maximum streaming throughput, we recommend that you don't include `insertId` and instead use [manual deduplication](https://docs.cloud.google.com/bigquery/docs/streaming-data-into-bigquery#manually_removing_duplicates) . For more information, see [Ensuring data consistency](https://docs.cloud.google.com/bigquery/docs/streaming-data-into-bigquery#dataconsistency) .

When you encounter this error, [diagnose the issue](https://docs.cloud.google.com/bigquery/docs/troubleshoot-storage-api#ts-streaming-insert-quota-diagnose) , and then [follow the recommended steps](https://docs.cloud.google.com/bigquery/docs/troubleshoot-storage-api#ts-streaming-insert-quota-resolution) to resolve it.

#### Diagnosis

Use the [`STREAMING_TIMELINE_BY_*`](https://docs.cloud.google.com/bigquery/docs/information-schema-streaming) views to analyze the streaming traffic. These views aggregate streaming statistics over one-minute intervals, grouped by `error_code` . Quota errors appear in the results with `error_code` equal to `RATE_LIMIT_EXCEEDED` or `QUOTA_EXCEEDED` .

Depending on the specific quota limit that was reached, look at `total_rows` or `total_input_bytes` . If the error is a table-level quota, filter by `table_id` .

For example, the following query shows total bytes ingested per minute, and the total number of quota errors:

    SELECT
     start_timestamp,
     error_code,
     SUM(total_input_bytes) as sum_input_bytes,
     SUM(IF(error_code IN ('QUOTA_EXCEEDED', 'RATE_LIMIT_EXCEEDED'),
         total_requests, 0)) AS quota_error
    FROM
     `region-REGION_NAME`.INFORMATION_SCHEMA.STREAMING_TIMELINE_BY_PROJECT
    WHERE
      start_timestamp > TIMESTAMP_SUB(CURRENT_TIMESTAMP, INTERVAL 1 DAY)
    GROUP BY
     start_timestamp,
     error_code
    ORDER BY 1 DESC

#### Resolution

To resolve this quota error, do the following:

  - If you are using the `insertId` field for deduplication, and your project is in a region that supports the higher streaming quota, we recommend removing the `insertId` field. This solution might require some additional steps to manually deduplicate the data. For more information, see [Manually removing duplicates](https://docs.cloud.google.com/bigquery/docs/streaming-data-into-bigquery#manually_removing_duplicates) .

  - If you are not using `insertId` , or if it's not feasible to remove it, monitor your streaming traffic over a 24-hour period and analyze the quota errors:
    
      - If you see mostly `RATE_LIMIT_EXCEEDED` errors rather than `QUOTA_EXCEEDED` errors, and your overall traffic is less than 80% of quota, the errors probably indicate temporary spikes. You can address these errors by retrying the operation using exponential backoff between retries.
    
      - If you are using a Dataflow job to insert data, consider using load jobs instead of streaming inserts. For more information, see [Setting the insertion method](https://beam.apache.org/documentation/io/built-in/google-bigquery/#setting-the-insertion-method) . If you are using Dataflow with a custom I/O connector, consider using a built-in I/O connector instead. For more information, see [Custom I/O patterns](https://beam.apache.org/documentation/patterns/custom-io/) .
    
      - If you see `QUOTA_EXCEEDED` errors or the overall traffic consistently exceeds 80% of the quota, submit a request for a quota increase. For more information, see [Request a quota adjustment](https://docs.cloud.google.com/docs/quotas/help/request_increase) .
    
      - You might also want to consider replacing streaming inserts with the newer [Storage Write API](https://docs.cloud.google.com/bigquery/docs/write-api) , which has higher throughput, lower price, and many useful features.
