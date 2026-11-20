---
name: documents/docs.cloud.google.com/bigquery/docs/errors
uri: https://docs.cloud.google.com/bigquery/docs/errors
title: HTTP status and error codes for BigQuery API
description: Interactively analyze large datasets.
data_source: docs.cloud.google.com
---

This page describes the HTTP status codes and error messages returned by the BigQuery API. You can use these codes to troubleshoot and resolve request failures, and verify API behavior.

For more information about non-API errors, client library connectivity errors, and Google Cloud console errors, see [Error messages](https://docs.cloud.google.com/bigquery/docs/error-messages) .

For more information about query errors, see [Troubleshoot query errors](https://docs.cloud.google.com/bigquery/docs/troubleshoot-queries) .

For more information about streaming insert errors, see [Troubleshoot streaming inserts](https://docs.cloud.google.com/bigquery/docs/write-api-rest#troubleshooting) .

> **Note:** This list contains common error messages related to the API, but isn't an exhaustive list of all error messages.

## Error response format

BigQuery uses the standard HTTP error reporting format for its API. Successful requests return HTTP status codes in the `2xx` range. Failed requests return status codes in the `4xx` and `5xx` ranges. Requests that require a redirect return status codes in the `3xx` range. Error responses usually include a JSON document in the response body, which contains an error object with information about the error.

In BigQuery API responses, an error object is typically one of the following:

- An [`errors` object](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatus.FIELDS.errors) , which contains an array of [`ErrorProto` objects](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/ErrorProto) .
- An [`errorResults` object](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatus.FIELDS.error_result) , which contains a single [`ErrorProto` object](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/ErrorProto) .

The **Reason** column in the status code tables on this page maps to the `reason` property in an `ErrorProto` object. If you use the [bq command-line tool](https://docs.cloud.google.com/bigquery/docs/reference/bq-cli-reference) to check job status, use the `--format=prettyjson` flag (for example, `bq --format=prettyjson show -j <var>JOB_ID</var>` ) or `--apilog=stdout` to view the error object and its `reason` property.

The following table describes the elements that can appear in the response body of an error. Fields should be used together to help determine the problem. Also, the example values in the following table are meant for illustration and aren't an exhaustive list of all possible values.

| Element                | Description                                                                                                                                                                                                                                |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `code`                 | An [HTTP status code](https://datatracker.ietf.org/doc/html/rfc7231#section-6) value, without the textual description. Example values include: `400` (Bad Request), `403` (Forbidden), and `404` (Not Found).                              |
| `error`                | A container for the error information.                                                                                                                                                                                                     |
| `errors`               | A container for the error details.                                                                                                                                                                                                         |
| errors. `domain`       | The scope of the error. Example values include: `global` and `usageLimits` .                                                                                                                                                               |
| errors. `location`     | The specific item within the `locationType` that caused the error. For example, if you specify an invalid value for a parameter, the `location` will be the name of the parameter. Example values include: `Authorization` and `project` . |
| errors. `locationType` | The location or part of the request that caused the error. Use with `location` to pinpoint the error. Example values include `header` and `parameter` .                                                                                    |
| errors. `message`      | Description of the error. Example values include `Invalid argument` , `Access Denied` , and `Not Found: Dataset myproject:foo` .                                                                                                           |
| errors. `reason`       | A unique identifier for the error cause. Example values include `invalid` , `accessDenied` , and `notFound` .                                                                                                                              |
| `message`              | Description of the error. Same as errors. `message` .                                                                                                                                                                                      |

## HTTP status and error codes

This section contains a non-exhaustive list of HTTP status and error codes from the BigQuery API. The `1xx` Informational and `2xx` Success codes are omitted. For more information, see Response Status Codes in [RFC 7231 §6](https://datatracker.ietf.org/doc/html/rfc7231#section-6) , [RFC 7232 §4](https://datatracker.ietf.org/doc/html/rfc7232#section-4) , [RFC 7233 §4](https://datatracker.ietf.org/doc/html/rfc7233#section-4) , [RFC 7235 §3](https://datatracker.ietf.org/doc/html/rfc7235#section-3) , and [RFC 6585](https://datatracker.ietf.org/doc/html/rfc6585) .

### 400 — [Bad Request](https://datatracker.ietf.org/doc/html/rfc7231#section-6.5.1)

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Reason</th>
<th>HTTP Status Code</th>
<th>Description</th>
<th>Troubleshooting</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>badRequest</code></td>
<td>400</td>
<td><p>A DML statement attempts to modify rows that were recently streamed with the legacy <code>tabledata.insertAll</code> API and remain in the table's streaming buffer. The error returns: <code>UPDATE or DELETE statement over table </code><var translate="no"> project </var><code> . </code><var translate="no"> dataset </var><code> . </code><var translate="no"> table </var><code> would affect rows in the streaming buffer, which is not supported</code> .</p></td>
<td><p>Migrate to the <a href="https://docs.cloud.google.com/bigquery/docs/write-api-grpc#use_data_manipulation_language_dml_with_recently_streamed_data">BigQuery Storage Write API (gRPC)</a> , wait a few minutes for the streaming buffer to flush, or filter your statement to exclude recently streamed rows. For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/troubleshoot-queries#streaming-dml">DML statements on tables with a streaming buffer</a> .</p></td>
</tr>
<tr class="even">
<td><code>invalid</code></td>
<td>400</td>
<td><p>The request contains invalid input other than an invalid query, including the following cases:</p>
<ul>
<li>A schema mismatch ( <code>Provided Schema does not match Table </code><var translate="no"> table</var> ).</li>
<li>A <code>RECORD</code> column, file, or routine that exceeds the 15-level nesting limit ( <code>Schema nested too deeply</code> ).</li>
<li>A destination table that is deleted or expires during a job ( <code>Destination deleted/expired during operation</code> ).</li>
</ul></td>
<td><p>Ensure provided schemas match existing columns and modes, flatten structures exceeding 15 levels of nesting (or store them as <code>JSON</code> ), and set destination table expiration times to outlive running jobs. For per-subtype steps, see <a href="https://docs.cloud.google.com/bigquery/docs/troubleshoot-queries#troubleshoot-invalid-errors">Troubleshoot invalid input and schema errors</a> .</p></td>
</tr>
<tr class="odd">
<td><code>invalidQuery</code></td>
<td>400</td>
<td><p>A SQL query fails validation or execution checks for one of the following reasons:</p>
<ul>
<li>Invalid SQL syntax, identifiers, or data types.</li>
<li>Unsatisfied feature options or required partition filters.</li>
<li>Exceeded view nesting or partition output limits.</li>
<li>A concurrent DML transaction conflict (such as <code>Concurrent conflicting update to </code><var translate="no"> details</var> ).</li>
</ul></td>
<td><p>Check the <code>[ </code><var translate="no"> line </var><code> : </code><var translate="no"> column </var><code> ]</code> location for GoogleSQL syntax or type mismatches, satisfy required <code>OPTIONS</code> or partition filters, or roll back stalled sessions and retry conflicting DML jobs. For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/troubleshoot-queries#ts-invalid-query">Invalid query errors</a> and <a href="https://docs.cloud.google.com/bigquery/docs/troubleshoot-queries#transaction_aborted_due_to_concurrent_update">Transaction aborted due to concurrent update</a> .</p></td>
</tr>
<tr class="even">
<td><code>jobBackendError</code></td>
<td>400</td>
<td><p>In <code>jobs.query</code> or <code>jobs.getQueryResults</code> , a job was created and then failed during execution with a <code>backendError</code> . The error returns: <code>The job encountered an error during execution. Retrying the job may solve the problem.</code></p></td>
<td><p>Retry the job with a new <code>jobId</code> using <a href="https://docs.cloud.google.com/monitoring/api/troubleshooting#retry">truncated exponential backoff</a> , ensuring client retry logic handles HTTP <code>400</code> responses in addition to <code>5xx</code> codes. For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/troubleshoot-queries#ts-job-backend-error">Troubleshoot jobBackendError and jobInternalError errors</a> .</p></td>
</tr>
<tr class="odd">
<td><code>jobInternalError</code></td>
<td>400</td>
<td><p>In <code>jobs.query</code> or <code>jobs.getQueryResults</code> , a job was created and then failed during execution with an internal error. The error returns: <code>The job encountered an internal error during execution and was unable to complete.</code></p></td>
<td><p>Retry the job with a new <code>jobId</code> using <a href="https://docs.cloud.google.com/monitoring/api/troubleshooting#retry">truncated exponential backoff</a> . For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/troubleshoot-queries#ts-job-internal-error">Troubleshoot jobBackendError and jobInternalError errors</a> .</p></td>
</tr>
<tr class="even">
<td><code>preconditionFailed</code></td>
<td>400</td>
<td><p>A request precondition isn't met, including the following cases:</p>
<ul>
<li>An <code>If-Match</code> ETag mismatch during a metadata update.</li>
<li>A missing CMEK encryption key required by organization policy.</li>
<li>A feature that isn't supported in the Standard edition.</li>
<li>A write to a failover dataset outside an Enterprise Plus primary reservation.</li>
<li>A materialized view query over a CDC base table with pending upserts.</li>
</ul></td>
<td><p>Fetch the current resource <code>etag</code> before retrying, specify the required Cloud Key Management Service key, run the workload in an Enterprise or Enterprise Plus reservation, or wait a few minutes for pending CDC upserts to apply. For per-subtype steps, see <a href="https://docs.cloud.google.com/bigquery/docs/troubleshoot-queries#ts-precondition-failed">Request precondition failed</a> .</p></td>
</tr>
<tr class="odd">
<td><code>resourceInUse</code></td>
<td>400</td>
<td><p>A delete request targets a resource that is still active or populated:</p>
<ul>
<li>A dataset that still contains tables, views, or routines.</li>
<li>A job that is still pending or running.</li>
</ul>
<p>The error returns: <var translate="no">resource_type </var><code> </code><var translate="no"> resource_id </var><code> is still in use</code> .</p></td>
<td><p>Empty the dataset before deleting it (or set <code>deleteContents=true</code> , run <code>bq rm -r -f -d</code> , or execute <code>DROP SCHEMA IF EXISTS </code><var translate="no"> dataset_name </var><code> CASCADE</code> ), or wait for an active job to finish or cancel it before deleting job metadata. For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/troubleshoot-queries#ts-resource-in-use">Resource is still in use</a> .</p></td>
</tr>
<tr class="even">
<td><code>resourcesExceeded</code></td>
<td>400</td>
<td><p>A job exceeds execution resource limits in one of the following areas:</p>
<ul>
<li>Per-table DML concurrency queues or session concurrency limits.</li>
<li>Worker, UDF, shuffle, or ML model memory budgets.</li>
<li>Table partition (10,000 partitions) or output column limits.</li>
<li>Cloud Key Management Service CMEK request rates, streaming reads, or cross-region data transfers.</li>
<li>Query planning complexity limits.</li>
</ul>
<p>The error returns: <code>Resources exceeded during query execution: </code><var translate="no"> details</var> .</p></td>
<td><p>Simplify queries, batch DML operations, reduce scanned columns or partitions, avoid concurrent jobs in the same session, or provision dedicated slot capacity for shuffle-heavy workloads. For per-subtype steps, see <a href="https://docs.cloud.google.com/bigquery/docs/troubleshoot-queries#ts-resources-exceeded">Troubleshoot resources exceeded issues</a> and <a href="https://docs.cloud.google.com/bigquery/docs/troubleshoot-queries#query_not_executed">Query exceeds memory resources</a> .</p></td>
</tr>
<tr class="odd">
<td><code>storageUnusable</code></td>
<td>400</td>
<td><p>Internal BigQuery storage holding the table's data is temporarily unavailable due to a service-side storage issue. The error returns: <code>Storage of </code><var translate="no"> resource_id </var><code> is unusable because </code><var translate="no"> reason </var><code> .</code></p></td>
<td><p>Retry the job using <a href="https://docs.cloud.google.com/monitoring/api/troubleshooting#retry">truncated exponential backoff</a> . For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/troubleshoot-queries#ts-storage-unusable">Table storage is unusable</a> .</p></td>
</tr>
<tr class="even">
<td><code>streamingDataUnavailable</code></td>
<td>400</td>
<td><p>Recently streamed data in write-optimized storage is temporarily unavailable to a reading job. The error returns: <code>Job failed because streaming data from </code><var translate="no"> table_source </var><code> is temporarily unavailable. Retrying the job may solve the problem.</code></p></td>
<td><p>Retry the job with a new <code>jobId</code> using <a href="https://docs.cloud.google.com/monitoring/api/troubleshooting#retry">truncated exponential backoff</a> , ensuring client retry logic handles HTTP <code>400</code> responses. For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/troubleshoot-queries#ts-streaming-data-unavailable">Streaming data is temporarily unavailable</a> .</p></td>
</tr>
<tr class="odd">
<td><code>tableUnavailable</code></td>
<td>400</td>
<td><p>BigQuery can't read a table whose data it doesn't manage, including the following cases:</p>
<ul>
<li>Fetching an Apache Iceberg or Delta Lake table schema times out.</li>
<li>A Hive-partitioned external table has no partition keys.</li>
<li>A Google-managed backing table is temporarily unavailable.</li>
</ul></td>
<td><p>Retry schema fetch or backing-table timeouts using <a href="https://docs.cloud.google.com/monitoring/api/troubleshooting#retry">truncated exponential backoff</a> , or verify <code>key=value</code> Cloud Storage URI paths and recreate Hive-partitioned external tables with at least one partition key. For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/troubleshoot-queries#ts-table-unavailable">External or backing table is unavailable</a> .</p></td>
</tr>
<tr class="even">
<td><code>userOwnedResourceError</code></td>
<td>400</td>
<td><p>An external resource that you own returns an error when accessed by BigQuery. The error returns: <code>Error when accessing a user-owned external </code><var translate="no"> resource_type </var><code> resource </code><var translate="no"> resource_name </var><code> . The resource provided error: </code><var translate="no"> external_error</var> .</p></td>
<td><p>Inspect <var translate="no"> resource_type </var> and <var translate="no"> resource_name </var> in the error message to identify the external resource, and resolve the underlying error reported in <var translate="no"> external_error </var> . For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/troubleshoot-queries#ts-user-owned-resource-error">User-owned external resource error</a> .</p></td>
</tr>
<tr class="odd">
<td><code>vortexDataUnavailable</code></td>
<td>400</td>
<td><p>Data recently streamed using the BigQuery Storage Write API (gRPC) into write-optimized storage is temporarily unavailable to a query. The error returns: <code>Job failed because vortex streaming data from </code><var translate="no"> table_source </var><code> is temporarily unavailable. Retrying the job may solve the problem.</code></p></td>
<td><p>Retry the query job with a new <code>jobId</code> using <a href="https://docs.cloud.google.com/monitoring/api/troubleshooting#retry">truncated exponential backoff</a> , ensuring client retry logic handles HTTP <code>400</code> responses. For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/troubleshoot-queries#ts-vortex-data-unavailable">Streaming data is temporarily unavailable</a> .</p></td>
</tr>
<tr class="even">
<td><code>billingTierLimitExceeded</code></td>
<td>400</td>
<td><p>An on-demand query exceeds the <a href="https://docs.cloud.google.com/bigquery/quotas#max_cpu_usage_on-demand">maximum CPU usage per scanned data limit</a> . The error returns: <code>Query exceeded resource limits. This query used </code><var translate="no"> cpu_seconds_used </var><code> CPU seconds but would charge only </code><var translate="no"> analysis_megabytes_billed </var><code> M Analysis bytes... </code><var translate="no"> cpu_seconds_used </var><code> CPU seconds were used, and this query must use less than </code><var translate="no"> cpu_seconds_limit </var><code> CPU seconds.</code></p></td>
<td><p>Refactor your SQL to remove unintended Cartesian products, inexact joins, unpartitioned window functions, or heavy JavaScript UDFs, or switch to <a href="https://docs.cloud.google.com/bigquery/docs/reservations-intro">capacity-based (slots) pricing</a> . For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/troubleshoot-queries#exceeded_resource_limits">Query exceeds CPU resources</a> and <a href="https://docs.cloud.google.com/bigquery/docs/best-practices-performance-compute#avoid-anti-sql-patterns">Avoid anti-SQL patterns</a> .</p></td>
</tr>
<tr class="odd">
<td><code>bytesBilledLimitExceeded</code></td>
<td>400</td>
<td><p>The pre-execution upper-bound byte estimate for a query exceeds <a href="https://docs.cloud.google.com/bigquery/docs/best-practices-costs#restrict-bytes-billed"><code>maximumBytesBilled</code></a> before execution starts. The error returns: <code>Query exceeded limit for bytes billed: </code><var translate="no"> limit_bytes </var><code> . </code><var translate="no"> required_bytes </var><code> or higher required.</code></p></td>
<td><p>Preview estimated bytes with a <a href="https://docs.cloud.google.com/bigquery/docs/running-queries#dry-run">dry run</a> , select only needed columns and filter on partitioned columns to <a href="https://docs.cloud.google.com/bigquery/docs/best-practices-performance-compute#reduce-data-processed">reduce data processed</a> , or raise <code>maximumBytesBilled</code> to at least <var translate="no">required_bytes</var> . For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/troubleshoot-queries#ts-bytes-billed-limit-exceeded">Query exceeds maximum bytes billed limit</a> .</p></td>
</tr>
<tr class="even">
<td><code>jobRateLimitExceeded</code></td>
<td>400</td>
<td><p>In <code>jobs.query</code> or <code>jobs.getQueryResults</code> , a job fails for one of the following reasons:</p>
<ul>
<li>The job exceeds a rate limit during execution ( <code>Job exceeded rate limits: Your </code><var translate="no"> scope </var><code> exceeded quota for </code><var translate="no"> quota_metric </var><code> ...</code> ).</li>
<li>The query isn't admitted because the query queue concurrency or continuous-query slot limit is reached (for example, <code>Query was not admitted as the maximum concurrency has been reached...</code> ).</li>
</ul></td>
<td><p>Reduce concurrent submissions (or use batch priority or slot autoscaling for continuous queries), and retry the job with a new <code>jobId</code> using <a href="https://docs.cloud.google.com/monitoring/api/troubleshooting#retry">truncated exponential backoff</a> . For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/troubleshoot-quotas#ts-job-rate-limit-exceeded">Job exceeded rate limits</a> and <a href="https://docs.cloud.google.com/bigquery/docs/troubleshoot-quotas#ts-query-admission-denied">Query admission denied</a> .</p></td>
</tr>
<tr class="odd">
<td><code>timeout</code></td>
<td>400</td>
<td><p>An operation exceeds its execution time limit, including the following cases:</p>
<ul>
<li>A query or dry run exceeds the 6-hour execution limit.</li>
<li>A child job inside a multi-statement query times out.</li>
<li>External table schema auto-detection times out.</li>
</ul></td>
<td><p>Filter on partitioned or clustered columns and split complex or multi-statement queries into smaller stages, or specify an explicit schema and narrower source URIs when creating external tables. For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/troubleshoot-queries#reach_execution_limit">Query exceeds execution time limit</a> and <a href="https://docs.cloud.google.com/bigquery/docs/troubleshoot-quotas">Troubleshoot quota and limit errors</a> .</p></td>
</tr>
<tr class="even">
<td><code>invalidUser</code></td>
<td>400</td>
<td><p>A scheduled query was configured with invalid user credentials.</p></td>
<td><p>Refresh the user credentials for the scheduled query. For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/scheduling-queries#update_scheduled_query_credentials">Scheduling queries</a> .</p></td>
</tr>
<tr class="odd">
<td><code>required</code></td>
<td>400</td>
<td><p>A required input is missing before execution:</p>
<ul>
<li>A required field in an API request payload or URL wasn't provided.</li>
<li>A required configuration object in a client library is empty or unassigned.</li>
</ul>
<p>The error returns: <code>Required parameter is missing: </code><var translate="no"> parameter_name</var> .</p></td>
<td><p>Verify required request body and query parameters in the <a href="https://docs.cloud.google.com/bigquery/docs/reference/rest">BigQuery API reference</a> or client library documentation, and inspect the configuration object before calling the API. For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/troubleshoot-queries#ts-required-parameter-missing">Required parameter is missing</a> .</p></td>
</tr>
</tbody>
</table>

### 401 — [Unauthorized](https://datatracker.ietf.org/doc/html/rfc7235#section-3.1)

The following is an example of an error response that you receive if your request lacks valid authentication credentials.

```
401 Unauthorized

{
  "error": {
    "errors": [
      {
        "domain": "global",
        "reason": "unauthenticated",
        "message": "Request had invalid authentication credentials. Expected OAuth 2 access token, login cookie or other valid authentication credential."
      }
    ],
    "code": 401,
    "message": "Request had invalid authentication credentials. Expected OAuth 2 access token, login cookie or other valid authentication credential.",
    "status": "UNAUTHENTICATED"
  }
}
```

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Reason</th>
<th>HTTP Status Code</th>
<th>Description</th>
<th>Troubleshooting</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>unauthenticated</code></td>
<td>401</td>
<td><p>Authentication for the request fails for one of the following reasons:</p>
<ul>
<li>The request lacks valid authentication credentials or uses an expired OAuth 2.0 access token.</li>
<li>End-user credentials or service account impersonation permissions are missing.</li>
<li>The caller's user account is restricted or deleted.</li>
</ul></td>
<td><p>Refresh your OAuth or Application Default Credentials, grant <code>roles/iam.serviceAccountUser</code> or <code>roles/iam.serviceAccountTokenCreator</code> when running with or impersonating a service account, or contact your administrator to restore a restricted account. For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/troubleshoot-access-control#ts-unauthenticated">Troubleshoot unauthenticated errors</a> .</p></td>
</tr>
</tbody>
</table>

### 403 — [Forbidden](https://datatracker.ietf.org/doc/html/rfc7231#section-6.5.3)

This is an example of an error response that you receive if you don't have permission to access the requested resource.

```
403 Forbidden

{
  "error": {
    "errors": [
      {
        "domain": "global",
        "reason": "accessDenied",
        "message": "Access Denied: Dataset myproject:mydataset: User does not have bigquery.datasets.get permission in project myproject."
      }
    ],
    "code": 403,
    "message": "Access Denied: Dataset myproject:mydataset: User does not have bigquery.datasets.get permission in project myproject."
  }
}
```

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Reason</th>
<th>HTTP Status Code</th>
<th>Description</th>
<th>Troubleshooting</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>responseTooLarge</code></td>
<td>403</td>
<td><p>A query or table read response exceeds size limits in one of the following ways:</p>
<ul>
<li>A query result or intermediate query stage exceeds the <a href="https://docs.cloud.google.com/bigquery/quotas#query_jobs">maximum response size</a> .</li>
<li>A single row exceeds the <a href="https://docs.cloud.google.com/bigquery/quotas#jobs.getQueryResults_max_row_size">20 MB <code>jobs.getQueryResults</code></a> or <a href="https://docs.cloud.google.com/bigquery/quotas#tabledata.list_max_row_size">100 MB <code>tabledata.list</code></a> REST row-size limit.</li>
</ul>
<p>The error returns: <code>Response too large to return. </code><var translate="no"> details</var> .</p></td>
<td><p>Specify a destination table (and set <code>configuration.query.allowLargeResults</code> to <code>true</code> for legacy SQL), remove <code>ORDER BY</code> or add <code>LIMIT</code> , or read large rows using the <a href="https://docs.cloud.google.com/bigquery/docs/reference/storage">BigQuery Storage Read API</a> or <code>EXPORT DATA</code> . For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/troubleshoot-queries#response_too_large">Query response is too large</a> and <a href="https://docs.cloud.google.com/bigquery/docs/troubleshoot-queries#ts-single-row-response-limit">Single-row response size limit exceeded</a> .</p></td>
</tr>
<tr class="even">
<td><code>apiLimitExceeded</code></td>
<td>403</td>
<td><p>A request exceeds one of the following API or metadata limits:</p>
<ul>
<li>Per-minute API request rate limits.</li>
<li>Table or policy metadata evaluation quotas.</li>
<li>Cross-region dataset replica creation limits ( <code>Cannot add more than </code><var translate="no"> limit </var><code> replicas for a region within </code><var translate="no"> window </var><code> day(s)</code> ).</li>
</ul>
<p>The error returns: <code>API limit exceeded: </code><var translate="no"> details</var> .</p></td>
<td><p>Retry failed requests with truncated exponential backoff, batch loads and reads, simplify granular per-table IAM or row-level security policies, and wait for the rolling window before adding dataset replicas. For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/troubleshoot-quotas#ts-api-limit-rate-and-metadata">API rate and metadata evaluation limit errors</a> and <a href="https://docs.cloud.google.com/bigquery/docs/troubleshoot-quotas#ts-dataset-replica-limit">Cross-region dataset replica creation limit errors</a> .</p></td>
</tr>
<tr class="odd">
<td><code>quotaExceeded</code></td>
<td>403</td>
<td><p>Your project exceeds one of the following usage quotas:</p>
<ul>
<li>A project or table <a href="https://docs.cloud.google.com/bigquery/quotas">BigQuery quota</a> .</li>
<li>A <a href="https://docs.cloud.google.com/bigquery/docs/custom-quotas">custom daily query quota</a> .</li>
<li>The <a href="https://cloud.google.com/bigquery/pricing#free-usage-tier">free tier for queries</a> when billing isn't enabled.</li>
</ul>
<p>The error returns: <code>Quota exceeded: Your </code><var translate="no"> scope </var><code> exceeded quota for </code><var translate="no"> quota_metric </var><code> . For more information, see https://cloud.google.com/bigquery/docs/troubleshoot-quotas</code> .</p></td>
<td><p>Inspect the error <code>message</code> to identify the exceeded quota, optimize high-scanning queries or <a href="https://docs.cloud.google.com/bigquery/docs/sandbox#upgrade">upgrade from the sandbox</a> , or adjust custom quotas on the <a href="https://console.cloud.google.com/iam-admin/quotas">Quotas</a> page. For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/troubleshoot-quotas#ts-custom-daily-query-quota">Custom daily query quota errors</a> .</p></td>
</tr>
<tr class="even">
<td><code>rateLimitExceeded</code></td>
<td>403</td>
<td><p>A request is rejected for one of the following rate or concurrency limits:</p>
<ul>
<li>Short-term API or query job rate limits ( <code>Exceeded rate limits: too many </code><var translate="no"> quota_metric </var><code> for this </code><var translate="no"> scope </var><code> ...</code> ).</li>
<li>Query queue concurrency or continuous-query reservation slot limits (for example, <code>Query was not admitted as the maximum concurrency has been reached...</code> ).</li>
</ul></td>
<td><p>Slow down the request rate and retry using <a href="https://docs.cloud.google.com/monitoring/api/troubleshooting#retry">truncated exponential backoff</a> , or run non-urgent queries with batch priority and adjust reservation concurrency or slot autoscaling. For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/troubleshoot-quotas">Troubleshoot quota and limit errors</a> and <a href="https://docs.cloud.google.com/bigquery/docs/troubleshoot-quotas#ts-query-admission-denied">Query admission denied</a> .</p></td>
</tr>
<tr class="odd">
<td><code>accessDenied</code></td>
<td>403</td>
<td><p>Access to a BigQuery resource is denied for one of the following reasons:</p>
<ul>
<li>The principal lacks required IAM permissions on the target project, dataset, or table.</li>
<li>An authorized view, row-level access policy, or column-level policy tag restricts access.</li>
<li>Cloud Key Management Service CMEK permissions or external data source permissions are missing.</li>
</ul>
<p>The error returns: <code>Access Denied: </code><var translate="no"> resource_type </var><code> </code><var translate="no"> resource_id </var><code> : </code><var translate="no"> details</var> .</p></td>
<td><p>Inspect <a href="https://docs.cloud.google.com/bigquery/docs/troubleshoot-access-control#get-audit-logs">Cloud Audit Logs</a> ( <code>protoPayload.authorizationInfo</code> ) and <a href="https://docs.cloud.google.com/bigquery/docs/troubleshoot-access-control#use-policy-analyzer">Policy Analyzer</a> to identify the missing permission, and grant the <a href="https://docs.cloud.google.com/bigquery/docs/troubleshoot-access-control#find-role">least-privilege predefined BigQuery role</a> . For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/troubleshoot-access-control#ts-access-denied-scenarios">Troubleshoot common Access Denied scenarios</a> .</p></td>
</tr>
<tr class="even">
<td><code>policyViolation</code></td>
<td>403</td>
<td><p>A security perimeter or organization policy blocks the request:</p>
<ul>
<li>A VPC Service Controls perimeter restricts access (including Google Drive exports or external tables in VPC-SC projects).</li>
<li>An organization policy constraint such as <code>constraints/gcp.resourceLocations</code> disallows the operation.</li>
</ul></td>
<td><p>Filter Logs Explorer by <code>vpcServiceControlsUniqueIdentifier</code> and check the <a href="https://docs.cloud.google.com/vpc-service-controls/docs/violation-analyzer">Violation Analyzer</a> , export or load data using a Cloud Storage bucket inside the perimeter, or select a region allowed by your <a href="https://docs.cloud.google.com/organization-policy/reference/org-policy-constraints">organization policy constraints</a> . For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/troubleshoot-access-control#ts-policy-violation">Troubleshoot policy violation errors</a> .</p></td>
</tr>
<tr class="odd">
<td><code>billingNotEnabled</code></td>
<td>403</td>
<td><p>The project lacks active billing for the requested operation:</p>
<ul>
<li>Billing isn't enabled for the project.</li>
<li>The project runs in the <a href="https://docs.cloud.google.com/bigquery/docs/sandbox#limitations">BigQuery sandbox</a> , where tables, views, and partitions expire after 60 days ( <code>expiration time must be less than 60 days</code> ).</li>
</ul>
<p>The error returns: <code>Billing has not been enabled for this project. Enable billing at https://console.cloud.google.com/billing. </code><var translate="no"> details</var> .</p></td>
<td><p><a href="https://docs.cloud.google.com/billing/docs/how-to/modify-project#enable_billing_for_a_project">Enable billing for the project</a> in the <a href="https://console.cloud.google.com/billing">Google Cloud console</a> to <a href="https://docs.cloud.google.com/bigquery/docs/sandbox#upgrade">upgrade from the BigQuery sandbox</a> , and then update the default expiration times for your tables, views, and partitions. For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/troubleshoot-access-control#ts-billing-not-enabled">Billing isn't enabled for the project</a> .</p></td>
</tr>
<tr class="even">
<td><code>blocked</code></td>
<td>403</td>
<td><p>BigQuery temporarily added the attempted operation to a denylist to prevent a service outage. The error returns: <code>Request was blocked to protect the system's operation. Please contact support at https://cloud.google.com/support.</code></p></td>
<td><p><a href="https://cloud.google.com/support">Contact Cloud Customer Care</a> with the exact timestamp, project ID, and BigQuery job ID to investigate the administrative mitigation rule. For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/troubleshoot-access-control#ts-request-blocked">Request was blocked to protect system operation</a> .</p></td>
</tr>
<tr class="odd">
<td><code>termsOfServiceNotAccepted</code></td>
<td>403</td>
<td><p>The project hasn't accepted the BigQuery Terms of Service. The error returns: <code>BigQuery Terms of Service have not been accepted</code> .</p></td>
<td><p>Sign in to the <a href="https://console.cloud.google.com/bigquery">Google Cloud console</a> , select your country and the Terms of Service checkbox on the welcome page if prompted, and click <strong>Agree and continue</strong> . For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/troubleshoot-access-control#ts-terms-of-service-not-accepted">BigQuery Terms of Service not accepted</a> .</p></td>
</tr>
</tbody>
</table>

### 404 — [Not Found](https://datatracker.ietf.org/doc/html/rfc7231#section-6.5.4)

The following is an example of an error response that you receive if you try to retrieve a dataset or resource that doesn't exist.

```
404 Not Found

{
  "error": {
    "errors": [
      {
        "domain": "global",
        "reason": "notFound",
        "message": "Not Found: Dataset myproject:foo"
      }
    ],
    "code": 404,
    "message": "Not Found: Dataset myproject:foo"
  }
}
```

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Reason</th>
<th>HTTP Status Code</th>
<th>Description</th>
<th>Troubleshooting</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>notFound</code></td>
<td>404</td>
<td><p>A requested resource can't be found for one of the following reasons:</p>
<ul>
<li>The target dataset, table, or job doesn't exist or has expired.</li>
<li>An external Cloud Storage or Google Drive file URI doesn't exist.</li>
<li>The request location doesn't match the dataset or job location.</li>
</ul>
<p>The error returns: <code>Not found: </code><var translate="no"> resource_type </var><code> </code><var translate="no"> resource_id</var> .</p></td>
<td><p>Verify the exact case-sensitive project, dataset, and table identifier and location, <a href="https://docs.cloud.google.com/bigquery/docs/restore-deleted-tables">restore deleted tables</a> within the time travel window, rerun queries whose cached result tables expired, or confirm external Cloud Storage or Google Drive files exist. For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/troubleshoot-queries#table_not_found">Table not found</a> , <a href="https://docs.cloud.google.com/bigquery/docs/troubleshoot-queries#location_not_found">Location not found</a> , and <a href="https://docs.cloud.google.com/bigquery/docs/troubleshoot-queries#job_not_found">Job not found</a> .</p></td>
</tr>
</tbody>
</table>

### 409 — [Conflict](https://datatracker.ietf.org/doc/html/rfc7231#section-6.5.8)

The following is an example of an error response that you receive if you try to create a resource that already exists.

```
409 Conflict

{
  "error": {
    "errors": [
      {
        "domain": "global",
        "reason": "duplicate",
        "message": "Already Exists: Dataset myproject:mydataset"
      }
    ],
    "code": 409,
    "message": "Already Exists: Dataset myproject:mydataset"
  }
}
```

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Reason</th>
<th>HTTP Status Code</th>
<th>Description</th>
<th>Troubleshooting</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>abortd</code></td>
<td>409</td>
<td><p>An operation stops because of a concurrent modification or conflict (returned with reason spelled <code>abortd</code> ).</p></td>
<td><p>Retry the operation after the conflicting operation finishes using <a href="https://docs.cloud.google.com/monitoring/api/troubleshooting#retry">truncated exponential backoff</a> , or roll back stopped multi-statement transactions before retrying. For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/troubleshoot-queries#ts-aborted">Operation was aborted</a> .</p></td>
</tr>
<tr class="even">
<td><code>duplicate</code></td>
<td>409</td>
<td><p>A request conflicts with an existing resource in one of the following ways:</p>
<ul>
<li>Creating a dataset, table, or job resource that already exists.</li>
<li>Running a job with <code>writeDisposition</code> set to <code>WRITE_EMPTY</code> when the destination table already exists.</li>
</ul>
<p>The error returns: <code>Already Exists: </code><var translate="no"> resource_type </var><code> </code><var translate="no"> resource_id</var> .</p></td>
<td><p>Use a different resource name, use <code>IF NOT EXISTS</code> or <code>CREATE OR REPLACE</code> in DDL statements, change <code>writeDisposition</code> to <code>WRITE_APPEND</code> or <code>WRITE_TRUNCATE</code> , or let BigQuery generate a random <code>jobId</code> . For per-subtype steps, see <a href="https://docs.cloud.google.com/bigquery/docs/troubleshoot-queries#ts-duplicate-resource">Resource already exists</a> .</p></td>
</tr>
</tbody>
</table>

### 499 — Client closed request

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Reason</th>
<th>HTTP Status Code</th>
<th>Description</th>
<th>Troubleshooting</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>stopped</code></td>
<td>499</td>
<td><p>A job stops before completion for one of the following reasons (polling <code>jobs.get</code> returns HTTP <code>200</code> with <code>reason: stopped</code> ):</p>
<ul>
<li>A caller explicitly cancels the job ( <code>User requested cancellation</code> ).</li>
<li>The job exceeds a configured execution or queue timeout ( <code>Job timed out after </code><var translate="no"> duration</var> or <code>Job timed out in the queue after </code><var translate="no"> duration</var> ).</li>
</ul>
<p>The error returns: <code>Job execution was cancelled: </code><var translate="no"> details</var> .</p></td>
<td><p>Increase <code>configuration.jobTimeoutMs</code> or project queue timeout options (or optimize query runtime and concurrency), or check <a href="https://docs.cloud.google.com/bigquery/docs/reference/auditlogs">Cloud Audit Logs</a> for <code>jobservice.cancel</code> calls. For per-subtype steps, see <a href="https://docs.cloud.google.com/bigquery/docs/troubleshoot-queries#ts-stopped-job">Job execution was canceled</a> .</p></td>
</tr>
</tbody>
</table>

### 500 — [Internal server error](https://datatracker.ietf.org/doc/html/rfc7231#section-6.6.1)

| Reason          | HTTP Status Code | Description                                                                                                                         | Troubleshooting                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|-----------------|------------------|-------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `internalError` | 500              | An internal error occurred within BigQuery. The error returns: `An internal error occurred and the request could not be completed.` | Wait according to the backoff requirements in the [BigQuery Service Level Agreement](https://cloud.google.com/bigquery/sla) and retry using [truncated exponential backoff](https://docs.cloud.google.com/monitoring/api/troubleshooting#retry) , or use [Reservations](https://docs.cloud.google.com/bigquery/docs/reservations-intro) to reduce transient error frequency. For more information, see [Troubleshoot internalError errors](https://docs.cloud.google.com/bigquery/docs/troubleshoot-queries#troubleshoot-internal-error) . |

### 501 — [Not implemented](https://datatracker.ietf.org/doc/html/rfc7231#section-6.6.2)

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Reason</th>
<th>HTTP Status Code</th>
<th>Description</th>
<th>Troubleshooting</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>notImplemented</code></td>
<td>501</td>
<td><p>A request attempts to use an unimplemented feature or operation for the target resource, such as the following:</p>
<ul>
<li>Copying a table with a non-managed storage type.</li>
<li>Running an unsupported <code>ALTER SEARCH INDEX</code> option.</li>
</ul>
<p>The error returns: <code>Not Implemented: </code><var translate="no"> details</var> .</p></td>
<td><p>Materialize unsupported table copy sources using <code>CREATE TABLE </code><var translate="no"> destination_table </var><code> AS SELECT * FROM </code><var translate="no"> source_table</var> , or drop and recreate search indexes with <code>DROP SEARCH INDEX</code> and <code>CREATE SEARCH INDEX</code> . For per-subtype steps, see <a href="https://docs.cloud.google.com/bigquery/docs/troubleshoot-queries#ts-not-implemented">Feature or operation isn't implemented</a> .</p></td>
</tr>
</tbody>
</table>

### 503 — [Service unavailable](https://datatracker.ietf.org/doc/html/rfc7231#section-6.6.4)

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Reason</th>
<th>HTTP Status Code</th>
<th>Description</th>
<th>Troubleshooting</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>backendError</code></td>
<td>503</td>
<td><p>The service is temporarily unavailable for one of the following reasons:</p>
<ul>
<li>A service demand surge (load shedding) or internal resource exhaustion.</li>
<li>Intermittent network connectivity issues.</li>
<li>A transient backend component issue.</li>
</ul>
<p>The error returns: <code>Error encountered during execution. Retrying may solve the problem.</code></p></td>
<td><p>Retry requests using <a href="https://docs.cloud.google.com/monitoring/api/troubleshooting#retry">truncated exponential backoff</a> , and retry failed jobs with a new <code>jobId</code> . If errors persist across retries, compare your 30-day failure rate against the <a href="https://cloud.google.com/bigquery/sla">BigQuery SLA</a> and <a href="https://cloud.google.com/support">contact Cloud Customer Care</a> ; see <a href="https://docs.cloud.google.com/bigquery/docs/troubleshoot-queries#troubleshoot-backend-error">Troubleshoot backendError errors</a> .</p></td>
</tr>
</tbody>
</table>
