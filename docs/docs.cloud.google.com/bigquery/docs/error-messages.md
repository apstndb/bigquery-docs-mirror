# Error messages

This document describes error messages that you might encounter when working with BigQuery, including HTTP error codes and suggested troubleshooting steps.

For more information about query errors, see [Troubleshoot query errors](/bigquery/docs/troubleshoot-queries) .

For more information about streaming insert errors, see [Troubleshoot streaming inserts](/bigquery/docs/streaming-data-into-bigquery#troubleshooting) .

## Error table

Responses from the BigQuery API include an HTTP error code and an error object in the response body. An error object is typically one of the following:

  - An [`  errors  ` object](/bigquery/docs/reference/rest/v2/Job#jobstatus) , which contains an array of [`  ErrorProto  ` objects](/bigquery/docs/reference/rest/v2/tables#errorproto) .
  - An [`  errorResults  ` object](/bigquery/docs/reference/rest/v2/Job#jobstatus) , which contains a single [`  ErrorProto  ` object](/bigquery/docs/reference/rest/v2/tables#errorproto) .

The **Error message** column in the following table maps to the `  reason  ` property in an `  ErrorProto  ` object.

The table does not include all possible HTTP errors or other networking errors. Therefore, don't assume that an error object is present in every error response from BigQuery. In addition, you might receive different errors or error objects if you use the Cloud Client Libraries for the BigQuery API. For more information, see [BigQuery API Client Libraries](/bigquery/docs/reference/libraries) .

If you receive an HTTP response code that doesn't appear in the following table, the response code indicates an issue or an expected result with the HTTP request. Response codes in the `  5xx  ` range indicate a server-side error. If you receive a `  5xx  ` response code, then retry the request later. In some cases, a `  5xx  ` response code might be returned by an intermediate server such as a proxy. Examine the response body and response headers for details about the error. For a full list of HTTP response codes, see [HTTP response codes](https://en.wikipedia.org/wiki/HTTP_response_codes) .

If you use the [bq command-line tool](/bigquery/bq-command-line-tool) to check job status, the error object is not returned by default. To view the error object and the corresponding `  reason  ` property that maps to the following table, use the `  --format=prettyjson  ` flag. For example, `  bq --format=prettyjson show -j *<job id>*  ` . To view verbose logging for the bq tool, use `  --apilog=stdout  ` . To learn more about troubleshooting the bq tool, see [Debugging](/bigquery/docs/bq-command-line-tool#debugging) .

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Error message</th>
<th>HTTP code</th>
<th>Description</th>
<th>Troubleshooting</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>accessDenied</td>
<td>403</td>
<td><p>This error returns when you try to access a resource such as a <a href="/bigquery/docs/datasets">dataset</a> , <a href="/bigquery/docs/tables">table</a> , <a href="/bigquery/docs/views-intro">view</a> , or <a href="/bigquery/docs/managing-jobs">job</a> that you don't have access to. This error also returns when you try to modify a read-only object.</p></td>
<td><p>Contact the resource owner and <a href="/bigquery/access-control">request access to the resource</a> for the user identified by the <code dir="ltr" translate="no">        principalEmail       </code> value in the error's audit log.</p></td>
</tr>
<tr class="even">
<td>attributeError</td>
<td>400</td>
<td><p>This error returns when there is an issue with the user code where a certain object attribute is called but does not exist.</p></td>
<td><p>Ensure that the object you are working with has the attribute you are trying to access. For more information on this error, see <a href="https://docs.python.org/3/library/exceptions.html#AttributeError">AttributeError</a> .</p></td>
</tr>
<tr class="odd">
<td>backendError</td>
<td>500, 503 or 504</td>
<td><p>This error indicates that the service is currently unavailable. This can happen due to a number of transient issues, including:<br />
</p>
<ul>
<li><strong>Service demand surge</strong> : Sudden spikes in demand, such as peak usage times, can result in load shedding to protect the quality of service for all BigQuery users. To prevent the system from getting overwhelmed BigQuery can return 500 or 503 errors for a small portion of requests.</li>
<li><strong>Network issues</strong> : The distributed nature of BigQuery means data is often transferred between different components or machines in the system. Various intermittent network connectivity issues can cause BigQuery to return a 5xx error, including SSL handshake failures, or other network infrastructure issues between the user and Google Cloud.</li>
<li><strong>Resource exhaustion</strong> : BigQuery has various internal resource limits in place to protect the overall service performance from a single user or a single job from consuming too many resources. BigQuery implements load shedding to tackle resource exhaustion.</li>
<li><strong>Backend errors</strong> : In rare cases, an internal problem within one of the BigQuery components can result in a 500 or 503 error returned to the client.</li>
</ul></td>
<td><p>5xx errors are service-side issues and the client has no way to fix or control them. From the client side, in order to mitigate the impact of 5xx errors, you need to retry your requests using <a href="https://cloud.google.com/monitoring/api/troubleshooting#exponential-retry">truncated exponential backoffs</a> . For more information about exponential backoffs, see <a href="https://en.wikipedia.org/wiki/Exponential_backoff">Exponential backoff</a> . However, there are two special cases for troubleshooting this error: <code dir="ltr" translate="no">        jobs.get       </code> calls and <code dir="ltr" translate="no">        jobs.insert       </code> calls.<br />
</p>
<p><strong><code dir="ltr" translate="no">         jobs.get        </code> calls</strong><br />
</p>
<ul>
<li>If you received a 503 error when polling <code dir="ltr" translate="no">         jobs.get        </code> , wait a few seconds and poll again.</li>
<li>If the job completes but includes an error object that contains <code dir="ltr" translate="no">         backendError        </code> , the job failed. You can safely retry the job without concerns about data consistency.</li>
</ul>
<p><strong><code dir="ltr" translate="no">         jobs.insert        </code> calls</strong><br />
If you receive this error when making a <code dir="ltr" translate="no">        jobs.insert       </code> call, it's unclear if the job succeeded. In this situation, you'll need to retry the job.<br />
</p>
<p>If the retries are not effective and the issues persist, you can <a href="#calculate-rate-of-failing-requests">calculate the rate of failing requests</a> and <a href="https://cloud.google.com/support">contact support</a> .<br />
Also, if you observe a specific request to BigQuery persistently fail with a 5xx error, even when retried using exponential backoff on multiple workflow restart attempts, you should escalate this to <a href="https://cloud.google.com/support">support</a> to troubleshoot the issue from the BigQuery side, regardless of the overall calculated error rate. Make sure to clearly communicate the <a href="https://cloud.google.com/support/docs/customer-care-procedures#support_case_priority">business impact</a> so that the issue can be triaged correctly.</p></td>
</tr>
<tr class="even">
<td>badRequest</td>
<td>400</td>
<td><p>The error <code dir="ltr" translate="no">        'UPDATE or DELETE statement over table                 project                .                 dataset                .                 table                would affect rows in the streaming buffer, which is not supported'       </code> can occur when some recently streamed rows in a table might not be available for DML operations ( <code dir="ltr" translate="no">        DELETE       </code> , <code dir="ltr" translate="no">        UPDATE       </code> , <code dir="ltr" translate="no">        MERGE       </code> ), typically for a few minutes, but in rare cases, up to 90 minutes. For more information, see <a href="/bigquery/docs/streaming-data-into-bigquery#dataavailability">Streaming data availability</a> and <a href="/bigquery/docs/data-manipulation-language#dml-limitations">DML Limitations.</a></p></td>
<td><p>Wait a few minutes and try again, or filter your statement to only operate on older data that is outside of the streaming buffer. To see if data is available for table DML operations, check the <a href="/bigquery/docs/reference/rest/v2/tables/get"><code dir="ltr" translate="no">         tables.get        </code> response</a> for the <a href="/bigquery/docs/reference/rest/v2/tables#streamingbuffer">streamingBuffer section</a> . If the streamingBuffer section is absent, then table data is available for DML operations. You can also use the <code dir="ltr" translate="no">        streamingBuffer.oldestEntryTime       </code> field to identify the age of records in the streaming buffer.</p>
<p>Alternatively, consider streaming data with the <a href="/bigquery/docs/write-api#use_data_manipulation_language_dml_with_recently_streamed_data">BigQuery Storage Write API</a> , which doesn't have this limitation.</p></td>
</tr>
<tr class="odd">
<td>billingNotEnabled</td>
<td>403</td>
<td><p>This error returns when billing isn't enabled for the project.</p></td>
<td><p>Enable billing for the project in the <a href="https://console.cloud.google.com/">Google Cloud console</a> .</p></td>
</tr>
<tr class="even">
<td>billingTierLimitExceeded</td>
<td>400</td>
<td><p>This error returns when the value of <code dir="ltr" translate="no">        statistics.query.billingTier       </code> for an on-demand Job exceeds 100. This occurs when on-demand queries use too much CPU relative to the amount of data scanned. For instructions on how to inspect job details, see <a href="/bigquery/docs/managing-jobs#view-job">Managing jobs</a> .</p></td>
<td><p>This error most often results from executing inefficient cross-joins, either explicitly or implicitly, for example due to an inexact join condition. These types of queries are not suitable for on-demand pricing due to high resource consumption, and in general they may not scale well. You can either optimize the query or switch to use the <a href="/bigquery/docs/reservations-intro">capacity-based (slots)</a> pricing model to resolve this error. For information about optimizing queries, see <a href="/bigquery/docs/best-practices-performance-patterns">Avoiding SQL anti-patterns</a> .</p></td>
</tr>
<tr class="odd">
<td>blocked</td>
<td>403</td>
<td><p>This error returns when BigQuery has temporarily denylisted the operation you attempted to perform, usually to prevent a service outage.</p></td>
<td><p><a href="https://cloud.google.com/support">Contact support</a> for more information.</p></td>
</tr>
<tr class="even">
<td>duplicate</td>
<td>409</td>
<td><p>This error returns when trying to create a job, dataset, or table that already exists. The error also returns when a job's <code dir="ltr" translate="no">        writeDisposition       </code> property is set to <code dir="ltr" translate="no">        WRITE_EMPTY       </code> and the destination table accessed by the job already exists.</p></td>
<td><p>Rename the resource you're trying to create, or change the <code dir="ltr" translate="no">        writeDisposition       </code> value in the job. For more information, see how to troubleshoot the <a href="/bigquery/docs/troubleshoot-queries#job_already_exists">Job already exists</a> error.</p></td>
</tr>
<tr class="odd">
<td>internalError</td>
<td>500</td>
<td><p>This error returns when an internal error occurs within BigQuery.</p></td>
<td><p>Wait according to the back-off requirements described in the <a href="https://cloud.google.com/bigquery/sla">BigQuery Service Level Agreement</a> , then try the operation again. If the error continues to occur, <a href="https://cloud.google.com/support">contact support</a> or <a href="https://issuetracker.google.com/issues/new?component=187149&amp;template=0">file a bug</a> using the BigQuery issue tracker. You can also reduce the frequency of this error by using <a href="/bigquery/docs/reservations-intro">Reservations</a> .</p></td>
</tr>
<tr class="even">
<td>invalid</td>
<td>400</td>
<td><p>This error returns when there is any type of invalid input other than an invalid query, such as missing required fields or an invalid table schema. Invalid queries return an <code dir="ltr" translate="no">        invalidQuery       </code> error.</p></td>
<td></td>
</tr>
<tr class="odd">
<td>invalidQuery</td>
<td>400</td>
<td><p>This error returns when you attempt to run an invalid query.</p></td>
<td><p>Check your query for syntax errors. The <a href="/bigquery/query-reference">query reference</a> contains descriptions and examples of how to construct valid queries.</p></td>
</tr>
<tr class="even">
<td>invalidUser</td>
<td>400</td>
<td><p>This error returns when you attempt to schedule a query with invalid user credentials.</p></td>
<td><p>Refresh the user credentials, as explained in <a href="/bigquery/docs/scheduling-queries#update_scheduled_query_credentials">Scheduling queries</a> .</p></td>
</tr>
<tr class="odd">
<td>jobBackendError</td>
<td>400</td>
<td><p>This error returns when the job was created successfully, but failed with an internal error. You might see this error in <code dir="ltr" translate="no">        jobs.query       </code> or <code dir="ltr" translate="no">        jobs.getQueryResults       </code> .</p></td>
<td><p>Retry the job with a new <code dir="ltr" translate="no">        jobId       </code> . If the error continues to occur, contact support.</p></td>
</tr>
<tr class="even">
<td>jobInternalError</td>
<td>400</td>
<td><p>This error returns when the job was created successfully, but failed with an internal error. You might see this error in <code dir="ltr" translate="no">        jobs.query       </code> or <code dir="ltr" translate="no">        jobs.getQueryResults       </code> .</p></td>
<td><p>Retry the job with a new <code dir="ltr" translate="no">        jobId       </code> . If the error continues to occur, contact support.</p></td>
</tr>
<tr class="odd">
<td>jobRateLimitExceeded</td>
<td>400</td>
<td><p>This error returns when the job was created successfully, but failed with a <a href="#rateLimitExceeded">rateLimitExceeded</a> error. You might see this error in <code dir="ltr" translate="no">        jobs.query       </code> or <code dir="ltr" translate="no">        jobs.getQueryResults       </code> .</p></td>
<td><p>Use <a href="https://cloud.google.com/monitoring/api/troubleshooting#exponential-retry">exponential backoff</a> to reduce the request rate, and then retry the job with a new <code dir="ltr" translate="no">        jobId       </code> .</p></td>
</tr>
<tr class="even">
<td>notFound</td>
<td>404</td>
<td><p>This error returns when you refer to a resource (a dataset, a table, or a job) that doesn't exist, or when the location in the request does not match the location of the resource (for example, the location in which a job is running). This can also occur when using <a href="/bigquery/docs/table-decorators">table decorators</a> to refer to deleted tables that have recently been <a href="/bigquery/docs/streaming-data-into-bigquery">streamed to</a> .</p></td>
<td><p>Fix the resource names, correctly specify the location, or wait at least 6 hours after streaming before querying a deleted table.</p></td>
</tr>
<tr class="odd">
<td>notImplemented</td>
<td>501</td>
<td><p>This job error returns when you try to access a feature that isn't implemented.</p></td>
<td><p><a href="https://cloud.google.com/support">Contact support</a> for more information.</p></td>
</tr>
<tr class="even">
<td>proxyAuthenticationRequired</td>
<td>407</td>
<td><p>This error returns between the client environment and the proxy server when the request lacks valid authentication credentials for the proxy server. For more information, see <a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/407">407 Proxy Authentication Required</a> .</p></td>
<td><p>Troubleshooting is specific to your environment. If you receive this error while working in Java, ensure you have set both the <code dir="ltr" translate="no">        jdk.http.auth.tunneling.disabledSchemes=       </code> and <code dir="ltr" translate="no">        jdk.http.auth.proxying.disabledSchemes=       </code> properties with no value following the equal sign.</p></td>
</tr>
<tr class="odd">
<td>quotaExceeded</td>
<td>403</td>
<td><p>This error returns when your project exceeds a <a href="/bigquery/quota-policy">BigQuery quota</a> , a <a href="/bigquery/docs/custom-quotas">custom quota</a> , or when you haven't set up billing and you have exceeded the <a href="https://cloud.google.com/bigquery/pricing#free-tier">free tier for queries</a> .</p></td>
<td><p>View the <code dir="ltr" translate="no">        message       </code> property of the error object for more information about which quota was exceeded. To reset or raise a BigQuery quota, <a href="https://cloud.google.com/support">contact support</a> . To modify a custom quota, submit a request from the <a href="https://console.cloud.google.com/iam-admin/quotas">Quotas</a> page. If you receive this error using the BigQuery sandbox, you can <a href="/bigquery/docs/sandbox#upgrade">upgrade from the sandbox</a> .<br />
For more information, see <a href="/bigquery/docs/troubleshoot-quotas">Troubleshooting BigQuery quota errors</a> .</p></td>
</tr>
<tr class="even">
<td>rateLimitExceeded</td>
<td>403</td>
<td><p>This error returns if your project exceeds a short-term rate limit by sending too many requests too quickly. For example, see the <a href="/bigquery/quota-policy#query_jobs">rate limits for query jobs</a> and <a href="/bigquery/quota-policy#api_requests">rate limits for API requests</a> .</p></td>
<td><p>Slow down the request rate.<br />
If you believe that your project did not exceed one of these limits, <a href="https://cloud.google.com/support">contact support</a> .<br />
For more information, see <a href="/bigquery/docs/troubleshoot-quotas">Troubleshooting BigQuery quota errors</a> .</p></td>
</tr>
<tr class="odd">
<td>resourceInUse</td>
<td>400</td>
<td><p>This error returns when you try to delete a dataset that contains tables or when you try to delete a job that is currently running.</p></td>
<td><p>Empty the dataset before attempting to delete it, or wait for a job to complete before deleting it.</p></td>
</tr>
<tr class="even">
<td>resourcesExceeded</td>
<td>400</td>
<td><p>This error returns when your job uses too many resources.</p></td>
<td><p>This error returns when your job uses too many resources. For troubleshooting information, see <a href="/bigquery/docs/troubleshoot-queries#ts-resources-exceeded">Troubleshoot resources exceeded errors</a> .</p></td>
</tr>
<tr class="odd">
<td>responseTooLarge</td>
<td>403</td>
<td><p>This error returns when your query's results are larger than the <a href="/bigquery/quota-policy#query_jobs">maximum response size</a> . Some queries execute in multiple stages, and this error returns when any stage returns a response size that is too large, even if the final result is smaller than the maximum. This error commonly returns when queries use an <code dir="ltr" translate="no">        ORDER BY       </code> clause.</p></td>
<td><p>Adding a <code dir="ltr" translate="no">        LIMIT       </code> clause can sometimes help, or removing the <code dir="ltr" translate="no">        ORDER BY       </code> clause. If you want to ensure that large results can return, you can set the <code dir="ltr" translate="no">        allowLargeResults       </code> property to <code dir="ltr" translate="no">        true       </code> and specify a destination table. For more information, see <a href="/bigquery/docs/writing-results#large-results">Writing large query results</a> .</p></td>
</tr>
<tr class="even">
<td>stopped</td>
<td>200</td>
<td><p>This status code returns when a job is canceled.</p></td>
<td></td>
</tr>
<tr class="odd">
<td>tableUnavailable</td>
<td>400</td>
<td><p>Certain BigQuery tables are backed by data managed by other Google product teams. This error indicates that one of these tables is unavailable.</p></td>
<td><p>When you encounter this error message, you can retry your request (see <a href="#internalError">internalError</a> troubleshooting suggestions) or contact the Google product team that granted you access to their data.</p></td>
</tr>
<tr class="even">
<td>timeout</td>
<td>400</td>
<td><p>The job timed out.</p></td>
<td><p>Consider reducing the amount of work performed by your operation so that it can complete within the set limit. For more information, see <a href="/bigquery/docs/troubleshoot-quotas">Troubleshoot quota and limit errors</a> .</p></td>
</tr>
</tbody>
</table>

### Sample error response

``` text
GET https://bigquery.googleapis.com/bigquery/v2/projects/12345/datasets/foo
Response:
[404]
{
  "error": {
  "errors": [
  {
    "domain": "global",
    "reason": "notFound",
    "message": "Not Found: Dataset myproject:foo"
  }],
  "code": 404,
  "message": "Not Found: Dataset myproject:foo"
  }
}
```

### Calculate rate of failing requests and uptime

The majority of 500 and 503 errors can be resolved by performing a retry with exponential backoff. In the case where 500 and 503 errors still persist, you can calculate the overall rate of failing requests and corresponding uptime to compare it to the [BigQuery Service Level Agreement (SLA)](https://cloud.google.com/bigquery/sla) to determine if the service is working as expected.

To calculate the overall rate of failing requests during the last 30 days, take the number of failed requests for a specific API call or method from the last 30 days and divide by the total number of requests for that API call or method from the last 30 days. Multiply this value by 100 to get the average percentage of failed requests over 30 days.

For example, you can query [Cloud Logging data](/logging/docs/view/logging-query-language) to get the number of total `  jobs.insert  ` requests and the number of failed `  jobs.insert  ` requests and perform the calculation. You can also obtain the error rate values from the [API dashboard](/apis/docs/monitoring#using_the_api_dashboard) or using the Metrics Explorer in [Cloud Monitoring](/apis/docs/monitoring#using) . These options won't include data about networking or routing problems encountered between the client and BigQuery, so we also recommend using a client-side logging and reporting system for more precise failure rate calculations.

First, take 100% minus the overall rate of failing requests. If this value is more than or equal to the value described in the BigQuery SLA, then the uptime also meets the BigQuery SLA. However, if this value is less than the value described in the SLA, calculate the uptime manually.

In order to calculate the uptime, you need to know the number of minutes that are considered service downtime. Service downtime means a period of one minute with more than 10% error rate calculated according to SLA definitions. To calculate the uptime, take the total minutes from the last 30 days and subtract the total minutes that the service was down. Divide the remaining time by the total minutes from the last 30 days and multiply this value by 100 to get the percentage of uptime over 30 days. For more information about the definitions and calculations related to SLA , see [BigQuery Service Level Agreement (SLA)](https://cloud.google.com/bigquery/sla)

If your monthly uptime percentage is greater than or equal to the value described in the BigQuery SLA, then the error was most likely caused by a transient issue, so you can continue to retry using [exponential backoff](/monitoring/api/troubleshooting#exponential-retry) .

If the uptime is below the value presented in the SLA, [contact support](/support) for help and share the observed overall error rate and uptime calculations.

## Authentication errors

Errors thrown by the OAuth token generation system return the following JSON object, as defined by the [OAuth2 specification](https://tools.ietf.org/html/rfc6749#section-5.2) .

`  {"error" : "_description_string_"}  `

The error is accompanied by either an HTTP `  400  ` Bad Request error or an HTTP `  401  ` Unauthorized error. `  _description_string_  ` is one of the error codes defined by the OAuth2 specification. For example:

`  {"error":"invalid_client"}  `

### Review errors

You can use the [logs explorer](/logging/docs/view/logs-explorer-interface) to view authentication errors for specific jobs, users, or other scopes. The following are examples of logs explorer filters that you can use to review authentication errors:

  - Search for failed jobs with permission issues in the Policy Denied audit logs:
    
    ``` text
    resource.type="bigquery_resource"
    protoPayload.status.message=~"Access Denied"
    logName="projects/PROJECT_ID/logs/cloudaudit.googleapis.com%2Fdata_access"
    ```
    
    Replace `  PROJECT_ID  ` with the ID of the project containing the resource.

  - Search for a specific user or service account used for authentication:
    
    ``` text
    resource.type="bigquery_resource"
    protoPayload.authenticationInfo.principalEmail="EMAIL"
    ```
    
    Replace `  EMAIL  ` with the email address of the user or service account.

  - Search for Identity and Access Management policy changes in the Admin Activity audit logs:
    
    ``` text
    protoPayload.methodName=~"SetIamPolicy"
    logName="projects/PROJECT_ID/logs/cloudaudit.googleapis.com%2Factivity"
    ```

  - Search for changes to a specific BigQuery dataset in the Data Access audit logs:
    
    ``` text
    resource.type="bigquery_resource"
    protoPayload.resourceName="projects/PROJECT_ID/datasets/DATASET_ID"
    logName=projects/PROJECT_ID/logs/cloudaudit.googleapis.com%2Fdata_access
    ```
    
    Replace `  DATASET_ID  ` with the ID of the dataset containing the resource.

## Connectivity error messages

The following table lists error messages that you might see because of intermittent connectivity issues when using the client libraries or calling the BigQuery API from your code:

<table>
<thead>
<tr class="header">
<th>Error message</th>
<th>Client library or API</th>
<th>Troubleshooting</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>com.google.cloud.bigquery.BigQueryException: Read timed out</td>
<td>Java</td>
<td>Set a larger timeout value.</td>
</tr>
<tr class="even">
<td>Connection has been shutdown: javax.net.ssl.SSLException: java.net.SocketException: Connection reset at com.google.cloud.bigquery.spi.v2.HttpBigQueryRpc.translate(HttpBigQueryRpc.java:115)</td>
<td>Java</td>
<td>Implement a retry mechanism and set a larger timeout value.</td>
</tr>
<tr class="odd">
<td>javax.net.ssl.SSLHandshakeException: Remote host terminated the handshake</td>
<td>Java</td>
<td>Implement a retry mechanism and set a larger timeout value.</td>
</tr>
<tr class="even">
<td>BrokenPipeError: [Errno 32] Broken pipe</td>
<td>Python</td>
<td>Implement a retry mechanism. For more information on this error, see <a href="https://docs.python.org/3/library/exceptions.html#BrokenPipeError">BrokenPipeError</a> .</td>
</tr>
<tr class="odd">
<td>Connection aborted. RemoteDisconnected('Remote end closed connection without response'</td>
<td>Python</td>
<td>Set a larger timeout value.</td>
</tr>
<tr class="even">
<td>SSLEOFError (EOF occurred in violation of protocol)</td>
<td>Python</td>
<td>This error returns instead of a 413 ( <code dir="ltr" translate="no">       ENTITY_TOO_LARGE      </code> ) HTTP error. Reduce the size of the request.</td>
</tr>
<tr class="odd">
<td>TaskCanceledException: A task was canceled</td>
<td>.NET library</td>
<td>Increase the timeout value on the client side.</td>
</tr>
<tr class="even">
<td>google.api_core.exceptions.PreconditionFailed: 412 PATCH</td>
<td>Python</td>
<td>This error returns while trying to update a table resource using a <a href="/bigquery/docs/reference/rest/v2/tables/update">HTTP request</a> . Make sure the ETag in the HTTP header isn't outdated. For table or dataset level operations, make sure that the resource hasn't changed since the last time it was instantiated and recreate the object if necessary.</td>
</tr>
<tr class="odd">
<td>Failed to establish a new connection: [Errno 110] Connection timed out</td>
<td>Client Libraries</td>
<td>This error returns when this request has reached the end-of-file (EOF) when streaming or reading data from BigQuery. Implement a <a href="https://cloud.google.com/monitoring/api/troubleshooting#exponential-retry">retry mechanism</a> and set a larger timeout value.</td>
</tr>
<tr class="even">
<td>socks.ProxyConnectionError: Error connecting to HTTP proxy :8080: [Errno 110] Connection timed out</td>
<td>Client Libraries</td>
<td>Troubleshoot proxy status and settings. Implement a <a href="https://cloud.google.com/monitoring/api/troubleshooting#exponential-retry">retry mechanism</a> and set a larger timeout value.</td>
</tr>
<tr class="odd">
<td>Received an unexpected EOF or 0 bytes from the transport stream</td>
<td>Client Libraries</td>
<td>Implement a <a href="https://cloud.google.com/monitoring/api/troubleshooting#exponential-retry">retry mechanism</a> and set a larger timeout value.</td>
</tr>
</tbody>
</table>

## Google Cloud console error messages

The following table lists error messages that you might see while you work in the Google Cloud console.

<table>
<thead>
<tr class="header">
<th>Error message</th>
<th>Description</th>
<th>Troubleshooting</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Unknown error response from the server.</td>
<td>This error displays when the Google Cloud console receives an unknown error from the server; for example, when you click a dataset or other type of link, and the page cannot be displayed.</td>
<td>Switch to your browser's incognito, or private, mode and repeating the action that resulted in the error. If no error results in incognito mode, then the error might be due to a browser extension, such as an ad blocker. Disable your browser extensions while not in incognito mode, and see if that resolves the issue.</td>
</tr>
</tbody>
</table>
