# Quotas and limits

This document lists the quotas and system limits that apply to BigQuery.

  - *Quotas* have default values, but you can typically request adjustments.
  - *System limits* are fixed values that can't be changed.

Google Cloud uses quotas to help ensure fairness and reduce spikes in resource use and availability. A quota restricts how much of a Google Cloud resource your Google Cloud project can use. Quotas apply to a range of resource types, including hardware, software, and network components. For example, quotas can restrict the number of API calls to a service, the number of load balancers used concurrently by your project, or the number of projects that you can create. Quotas protect the community of Google Cloud users by preventing the overloading of services. Quotas also help you to manage your own Google Cloud resources.

The Cloud Quotas system does the following:

  - Monitors your consumption of Google Cloud products and services
  - Restricts your consumption of those resources
  - Provides a way to [request changes to the quota value](/docs/quotas/help/request_increase) and [automate quota adjustments](/docs/quotas/quota-adjuster)

In most cases, when you attempt to consume more of a resource than its quota allows, the system blocks access to the resource, and the task that you're trying to perform fails.

Quotas generally apply at the Google Cloud project level. Your use of a resource in one project doesn't affect your available quota in another project. Within a Google Cloud project, quotas are shared across all applications and IP addresses.

For more information, see the [Cloud Quotas overview](/docs/quotas/overview) .

There are also *system limits* on BigQuery resources. System limits can't be changed.

Some error messages specify quotas or limits that you can increase, while other error messages specify quotas or limits that you can't increase. Reaching a hard limit means that you need to implement temporary or permanent workarounds or best practices for your workload. Doing so is a best practice, even for quotas or limits that can be increased. For details about both types of errors, see [Troubleshoot quota and limit errors](/bigquery/docs/troubleshoot-quotas) .

By default, BigQuery quotas and limits apply on a [per-project](/bigquery/docs/projects) basis. Quotas and limits that apply on a different basis are indicated as such; for example, the maximum number of columns *per table* , or the maximum number of concurrent API requests *per user* . Specific policies vary depending on resource availability, user profile, Service Usage history, and other factors, and are subject to change without notice.

### Quota replenishment

Daily quotas are replenished at regular intervals throughout the day, reflecting their intent to guide rate limiting behaviors. Intermittent refresh is also done to avoid long disruptions when quota is exhausted. More quota is typically made available within minutes rather than globally replenished once daily.

### Request a quota increase

To adjust most quotas, use the Google Cloud console. For more information, see [Request a quota adjustment](/docs/quotas/help/request_increase) .

For step-by-step guidance through the process of requesting a quota increase in Google Cloud console, click **Guide me** :

### Cap quota usage

To learn how you can limit usage of a particular resource by creating a quota override, see [Create quota override](/docs/quotas/view-manage#capping_usage) .

### Required permissions

To view and update your BigQuery quotas in the Google Cloud console, you need the same permissions as for any Google Cloud quota. For more information, see [Google Cloud quota permissions](/docs/quotas/permissions) .

### Troubleshoot

For information about troubleshooting errors related to quotas and limits, see [Troubleshooting BigQuery quota errors](/bigquery/docs/troubleshoot-quotas) .

## Jobs

Quotas and limits apply to jobs that BigQuery runs on your behalf whether they are run by using Google Cloud console, the bq command-line tool, or programmatically using the REST API or client libraries.

### Query jobs

The following quotas apply to query jobs created automatically by running interactive queries, scheduled queries, and jobs submitted by using the [`  jobs.query  `](/bigquery/docs/reference/v2/jobs/query) and query-type [`  jobs.insert  `](/bigquery/docs/reference/v2/jobs/insert) API methods.

For troubleshooting information, see the BigQuery [Troubleshooting page](/bigquery/docs/troubleshoot-quotas) .

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th>Quota</th>
<th>Default</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Query usage per day</td>
<td>200 Tebibytes (TiB)</td>
<td>This quota applies only to <a href="https://cloud.google.com/bigquery/pricing#on_demand_pricing">the on-demand query pricing model.</a><br />
Your project can run up to 200 TiB in queries per day. You can change this limit anytime. See <a href="/bigquery/docs/custom-quotas">Create custom query quotas</a> to learn more about cost controls.<br />
</td>
</tr>
<tr class="even">
<td>Query usage per day per user</td>
<td>Unlimited</td>
<td>This quota applies only to <a href="https://cloud.google.com/bigquery/pricing#on_demand_pricing">the on-demand query pricing model.</a><br />
There is no default limit on how many TiB in queries a user can run per day. You can set the limit anytime. Regardless of the per user limit, the total usage for all users in the project combined can never exceed the query usage per day limit. See <a href="/bigquery/docs/custom-quotas">Create custom query quotas</a> to learn more about cost controls.<br />
</td>
</tr>
<tr class="odd">
<td>GoogleSQL federated query cross-region bytes per day</td>
<td>1 TB</td>
<td>If the <a href="/bigquery/docs/locations">BigQuery query processing location</a> and the Cloud SQL instance location are different, then your query is a cross-region query. Your project can run up to 1 TB in cross-region queries per day. See <a href="/bigquery/docs/cloud-sql-federated-queries">Cloud SQL federated queries</a> .<br />
</td>
</tr>
<tr class="even">
<td>Cross-cloud transferred bytes per day</td>
<td>1 TB</td>
<td>You can transfer up to 1 TB of data per day from <a href="/bigquery/docs/omni-aws-cross-cloud-transfer">an Amazon S3 bucket or from Azure Blob Storage</a> .<br />
</td>
</tr>
</tbody>
</table>

The following limits apply to query jobs created automatically by running interactive queries, scheduled queries, and jobs submitted by using the [`  jobs.query  `](/bigquery/docs/reference/v2/jobs/query) and query-type [`  jobs.insert  `](/bigquery/docs/reference/v2/jobs/insert) API methods:

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Default</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Maximum number of queued interactive queries</td>
<td>1,000 queries</td>
<td>Your project can queue up to 1,000 interactive queries. Additional interactive queries that exceed this limit return a quota error. To troubleshoot these errors, see <a href="/bigquery/docs/troubleshoot-quotas#interactive-query-queue-resolution">Avoid limits for high-volume interactive queries</a> .</td>
</tr>
<tr class="even">
<td>Maximum number of queued batch queries</td>
<td>20,000 queries</td>
<td>Your project can queue up to 20,000 batch queries. Additional batch queries that exceed this limit return a quota error.</td>
</tr>
<tr class="odd">
<td>Maximum number of concurrent interactive queries against Bigtable external data sources</td>
<td>16 queries</td>
<td>Your project can run up to sixteen concurrent queries against a <a href="/bigquery/external-data-bigtable">Bigtable external data source</a> .</td>
</tr>
<tr class="even">
<td>Maximum number of concurrent queries that contain remote functions</td>
<td>10 queries</td>
<td>You can run up to ten concurrent queries with <a href="/bigquery/docs/remote-functions">remote functions</a> per project.</td>
</tr>
<tr class="odd">
<td>Maximum number of concurrent multi-statement queries</td>
<td>1,000 multi-statement queries</td>
<td>Your project can run up to 1,000 concurrent <a href="/bigquery/docs/multi-statement-queries">multi-statement queries</a> . For other quotas and limits related to multi-statement queries, see <a href="/bigquery/quotas#multi_statement_query_limits">Multi-statement queries</a> .</td>
</tr>
<tr class="even">
<td>Maximum number of concurrent legacy SQL queries that contain UDFs</td>
<td>6 queries</td>
<td>Your project can run up to six concurrent legacy SQL queries with user-defined functions (UDFs). This limit includes both <a href="/bigquery/docs/running-queries#queries">interactive</a> and <a href="/bigquery/docs/running-queries#batch">batch</a> queries. Interactive queries that contain UDFs also count toward the concurrent limit for interactive queries. This limit does not apply to GoogleSQL queries.</td>
</tr>
<tr class="odd">
<td>Daily query size limit</td>
<td>Unlimited</td>
<td>By default, there is no daily query size limit. However, you can set limits on the amount of data users can query by creating <a href="/bigquery/cost-controls#controlling_query_costs_using_bigquery_%20custom_quotas">custom quotas</a> to control <a href="/bigquery/quotas#query_usage_per_day">query usage per day</a> or <a href="/bigquery/quotas#query_usage_per_day_per_user">query usage per day per user</a> .</td>
</tr>
<tr class="even">
<td>Daily destination table update limit</td>
<td>See <a href="/bigquery/quotas#load_job_per_table.long">Maximum number of table operations per day</a> .</td>
<td>Updates to destination tables in a query job count toward the limit on the maximum number of table operations per day for the destination tables. Destination table updates include append and overwrite operations that are performed by queries that you run by using the Google Cloud console, using the bq command-line tool, or calling the <a href="/bigquery/docs/reference/v2/jobs/query"><code dir="ltr" translate="no">        jobs.query       </code></a> and query-type <a href="/bigquery/docs/reference/v2/jobs/insert"><code dir="ltr" translate="no">        jobs.insert       </code></a> API methods.</td>
</tr>
<tr class="odd">
<td>Query/multi-statement query execution-time limit</td>
<td>6 hours</td>
<td><p>A query or multi-statement query can execute for up to 6 hours, and then it fails. However, sometimes queries are retried. A query can be tried up to three times, and each attempt can run for up to 6 hours. As a result, it's possible for a query to have a total runtime of more than 6 hours.</p>
<p><code dir="ltr" translate="no">          CREATE MODEL        </code> job timeout defaults to 24 hours, with the exception of time series, AutoML, and hyperparameter tuning jobs which timeout at 48 hours.</p></td>
</tr>
<tr class="even">
<td>Maximum number of resources referenced per query</td>
<td>1,000 resources</td>
<td>A query can reference up to 1,000 total of unique <a href="/bigquery/docs/tables-intro">tables</a> , unique <a href="/bigquery/docs/views-intro">views</a> , unique <a href="/bigquery/docs/user-defined-functions">user-defined functions</a> (UDFs), and unique <a href="/bigquery/docs/table-functions">table functions</a> after full expansion. This limit includes the following:
<ul>
<li>Tables, views, UDFs, and table functions directly referenced by the query.</li>
<li>Tables, views, UDFs, and table functions referenced by other views/UDFs/table functions referenced in the query.</li>
</ul></td>
</tr>
<tr class="odd">
<td>Maximum SQL query character length</td>
<td>1,024k characters</td>
<td>A SQL query can be up to 1,024k characters long. This limit includes comments and whitespace characters. If your query is longer, you receive the following error: <code dir="ltr" translate="no">       The query is too large.      </code> To stay within this limit, consider replacing large arrays or lists with query parameters and breaking a long query into multiple queries in the session.</td>
</tr>
<tr class="even">
<td>Maximum unresolved legacy SQL query length</td>
<td>256 KB</td>
<td>An unresolved legacy SQL query can be up to 256 KB long. If your query is longer, you receive the following error: <code dir="ltr" translate="no">       The query         is too large.      </code> To stay within this limit, consider replacing large arrays or lists with query parameters.</td>
</tr>
<tr class="odd">
<td>Maximum unresolved GoogleSQL query length</td>
<td>1 MB</td>
<td>An unresolved GoogleSQL query can be up to 1 MB long. If your query is longer, you receive the following error: <code dir="ltr" translate="no">       The query is too     large.      </code> To stay within this limit, consider replacing large arrays or lists with query parameters.</td>
</tr>
<tr class="even">
<td>Maximum resolved legacy and GoogleSQL query length</td>
<td>12 MB</td>
<td>The limit on resolved query length includes the length of all views and wildcard tables referenced by the query.</td>
</tr>
<tr class="odd">
<td>Maximum number of GoogleSQL query parameters</td>
<td>10,000 parameters</td>
<td>A GoogleSQL query can have up to 10,000 parameters.</td>
</tr>
<tr class="even">
<td>Maximum request size</td>
<td>10 MB</td>
<td>The request size can be up to 10 MB, including additional properties like query parameters.</td>
</tr>
<tr class="odd">
<td>Maximum response size</td>
<td>10 GB compressed</td>
<td>Sizes vary depending on compression ratios for the data. The actual response size might be significantly larger than 10 GB. The maximum response size is unlimited when <a href="/bigquery/docs/writing-results#large-results">writing large query results to a destination table</a> .</td>
</tr>
<tr class="even">
<td>Maximum row size</td>
<td>100 MB</td>
<td>The maximum row size is approximate, because the limit is based on the internal representation of row data. The maximum row size limit is enforced during certain stages of query job execution.</td>
</tr>
<tr class="odd">
<td>Maximum columns in a table, query result, or view definition</td>
<td>10,000 columns</td>
<td>A table, query result, or view definition can have up to 10,000 columns. This includes nested and repeated columns. Deleted columns can continue to count towards the total number of columns. If you've deleted columns, then you might receive quota errors until the total resets.</td>
</tr>
<tr class="even">
<td>Maximum concurrent slots for on-demand pricing</td>
<td>2,000 slots per project<br />
<br />
20,000 slots per organization</td>
<td>With on-demand pricing, your project can have up to 2,000 concurrent slots. There is also a 20,000 concurrent slots cap at the organization level. BigQuery tries to allocate slots fairly between projects within an organization if their total demand is higher than 20,000 slots. BigQuery slots are shared among all queries in a single project. BigQuery might exceed this limit to accelerate your queries. The capacity is subject to availability. To check how many slots you're using, see <a href="/bigquery/docs/monitoring">Monitoring BigQuery using Cloud Monitoring</a> .</td>
</tr>
<tr class="odd">
<td>Maximum CPU usage per scanned data for on-demand pricing</td>
<td>256 CPU seconds per MiB scanned</td>
<td>With on-demand pricing, your query can use up to approximately 256 CPU seconds per MiB of scanned data. If your query is too CPU-intensive for the amount of data being processed, the query fails with a <code dir="ltr" translate="no">       billingTierLimitExceeded      </code> error. For more information, see <a href="/bigquery/docs/error-messages">Error messages</a> .</td>
</tr>
<tr class="even">
<td>Multi-statement transaction table mutations</td>
<td>100 tables</td>
<td>A <a href="/bigquery/docs/transactions">transaction</a> can mutate data in at most 100 tables.</td>
</tr>
<tr class="odd">
<td>Multi-statement transaction partition modifications</td>
<td>100,000 partition modifications</td>
<td>A <a href="/bigquery/docs/transactions">transaction</a> can perform at most 100,000 partition modifications.</td>
</tr>
<tr class="even">
<td>BigQuery Omni maximum query result size</td>
<td>20 GiB uncompressed</td>
<td>The maximum result size is 20 GiB logical bytes when querying <a href="/bigquery/docs/query-azure-data">Microsoft Azure</a> or <a href="/bigquery/docs/query-aws-data">AWS</a> data. If your query result is larger than 20 GiB, consider exporting the results to <a href="/bigquery/docs/omni-aws-export-results-to-s3">Amazon S3</a> or <a href="/bigquery/docs/omni-azure-export-results-to-azure-storage">Blob Storage</a> . For more information, see <a href="/bigquery/docs/omni-introduction#limitations">BigQuery Omni Limitations</a> .</td>
</tr>
<tr class="odd">
<td>BigQuery Omni total query result size per day</td>
<td>1 TB</td>
<td>The total query result sizes for a project is 1 TB per day. For more information, see <a href="/bigquery/docs/omni-introduction#limitations">BigQuery Omni limitations</a> .<br />
</td>
</tr>
<tr class="even">
<td>BigQuery Omni maximum row size</td>
<td>10 MiB</td>
<td>The maximum row size is 10 MiB when querying <a href="/bigquery/docs/query-azure-data">Microsoft Azure</a> or <a href="/bigquery/docs/query-aws-data">AWS</a> data. For more information, see <a href="/bigquery/docs/omni-introduction#limitations">BigQuery Omni Limitations</a> .</td>
</tr>
</tbody>
</table>

Although scheduled queries use features of the [BigQuery Data Transfer Service](/bigquery/docs/dts-introduction) , scheduled queries are not transfers, and are not subject to [load job limits](/bigquery/quotas#load_jobs) .

### Extract jobs

The following limits apply to jobs that [extract data](/bigquery/docs/exporting-data) from BigQuery by using the bq command-line tool, Google Cloud console, or the extract-type [`  jobs.insert  `](/bigquery/docs/reference/rest/v2/jobs/insert) API method.

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Default</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Maximum number of extracted bytes per day</td>
<td>50 TiB</td>
<td>You can extract up to 50 TiB(Tebibytes) of data per day from a project at no cost using the shared slot pool. You can <a href="/bigquery/docs/exporting-data#view_current_quota_usage">set up a Cloud Monitoring</a> alert policy that provides notification of the number of bytes extracted. To extract more than 50 TiB(Tebibytes) of data per day, do one of the following:
<ul>
<li>Create a <a href="/bigquery/docs/reservations-intro#reservations">slot reservation</a> or use an existing reservation and <a href="/bigquery/docs/reservations-workload-management#assignments">assign</a> your project into the reservation with job type <code dir="ltr" translate="no">         PIPELINE        </code> . You are billed using <a href="https://cloud.google.com/bigquery/pricing#capacity_compute_analysis_pricing">capacity-based pricing</a> . <code dir="ltr" translate="no">         EXPORT DATA        </code> statements aren't supported for <code dir="ltr" translate="no">         PIPELINE        </code> reservations.</li>
<li>Use the <a href="/bigquery/docs/reference/standard-sql/other-statements#export_data_statement"><code dir="ltr" translate="no">          EXPORT DATA         </code></a> SQL statement. We will bill you using either <a href="https://cloud.google.com/bigquery/pricing#on_demand_pricing">on-demand</a> or <a href="https://cloud.google.com/bigquery/pricing#capacity_compute_analysis_pricing">capacity-based pricing</a> , depending on how your project is configured.</li>
<li>Use the <a href="/bigquery/docs/reference/storage">Storage Read API</a> . We will bill you using the price for <a href="https://cloud.google.com/bigquery/pricing#data_extraction_pricing">streaming reads</a> . The expiration time is guaranteed to be at least <a href="/bigquery/docs/reference/storage#create_a_session">6 hours</a> from session creation time.</li>
</ul></td>
</tr>
<tr class="even">
<td>Maximum number of extract jobs per day</td>
<td>100,000 extract jobs</td>
<td>You can run up to 100,000 extract jobs per day in a project. To run more than 100,000 extract jobs per day, do one of the following:
<ul>
<li>Create a <a href="/bigquery/docs/reservations-intro#reservations">slot reservation</a> or use an existing reservation and <a href="/bigquery/docs/reservations-workload-management#assignments">assign</a> your project into the reservation with job type <code dir="ltr" translate="no">         PIPELINE        </code> . We will bill you using <a href="https://cloud.google.com/bigquery/pricing#capacity_compute_analysis_pricing">capacity-based pricing</a> .</li>
<li>Use the <a href="/bigquery/docs/reference/standard-sql/other-statements#export_data_statement"><code dir="ltr" translate="no">          EXPORT DATA         </code></a> SQL statement. We will bill you using either <a href="https://cloud.google.com/bigquery/pricing#on_demand_pricing">on-demand</a> or <a href="https://cloud.google.com/bigquery/pricing#capacity_compute_analysis_pricing">capacity-based pricing</a> , depending on how your project is configured.</li>
<li>Use the <a href="/bigquery/docs/reference/storage">Storage Read API</a> . We will bill you using the price for <a href="https://cloud.google.com/bigquery/pricing#data_extraction_pricing">streaming reads</a> . The expiration time is guaranteed to be at least <a href="/bigquery/docs/reference/storage#create_a_session">6 hours</a> from session creation time.</li>
</ul></td>
</tr>
<tr class="odd">
<td>Maximum table size extracted to a single file</td>
<td>1 GB</td>
<td>You can extract up to 1 GB of table data to a single file. To extract more than 1 GB of data, use a <a href="/bigquery/docs/exporting-data#exporting_data_into_one_or_more_files">wildcard</a> to extract the data into multiple files. When you extract data to multiple files, the size of the files varies. In some cases, the size of the output files is more than 1 GB.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/exporting-data#exporting_data_into_one_or_more_files">Wildcard URIs</a> per extract job</td>
<td>500 URIs</td>
<td>An extract job can have up to 500 wildcard URIs.</td>
</tr>
</tbody>
</table>

For more information about viewing your current extract job usage, see [View current quota usage](/bigquery/docs/exporting-data#view_current_quota_usage) . For troubleshooting information, see [Export troubleshooting](/bigquery/docs/exporting-data#troubleshooting) .

### Load jobs

The following limits apply when you [load data](/bigquery/loading-data-into-bigquery) into BigQuery, using the Google Cloud console, the bq command-line tool, or the load-type [`  jobs.insert  `](/bigquery/docs/reference/rest/v2/jobs/insert) API method.

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Default</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Load jobs per table per day</td>
<td>1,500 jobs</td>
<td>Load jobs, including failed load jobs, count toward the limit on the number of table operations per day for the destination table. For information about limits on the number of table operations per day for standard tables and partitioned tables, see <a href="#table_limits">Tables</a> .</td>
</tr>
<tr class="even">
<td>Load jobs per day</td>
<td>100,000 jobs</td>
<td>Your project is replenished with a maximum of 100,000 load jobs quota every 24 hours. Failed load jobs count toward this limit. In some cases, it is possible to run more than 100,000 load jobs in 24 hours if a prior day's quota is not fully used.</td>
</tr>
<tr class="odd">
<td>Maximum columns per table</td>
<td>10,000 columns</td>
<td>A table can have up to 10,000 columns. This includes nested and repeated columns.</td>
</tr>
<tr class="even">
<td>Maximum size per load job</td>
<td>15 TB</td>
<td>The total size for all of your CSV, JSON, Avro, Parquet, and ORC input files can be up to 15 TB. This limit does not apply for jobs with a reservation.</td>
</tr>
<tr class="odd">
<td>Maximum number of source URIs in job configuration</td>
<td>10,000 URIs</td>
<td>A job configuration can have up to 10,000 source URIs.</td>
</tr>
<tr class="even">
<td>Maximum number of files per load job</td>
<td>10,000,000 files</td>
<td>A load job can have up to 10 million total files, including all files matching all wildcard URIs.</td>
</tr>
<tr class="odd">
<td>Maximum number of files in the source Cloud Storage bucket</td>
<td>Approximately 60,000,000 files</td>
<td>A load job can read from a Cloud Storage bucket containing up to approximately 60,000,000 files.</td>
</tr>
<tr class="even">
<td>Load job execution-time limit</td>
<td>6 hours</td>
<td>A load job fails if it executes for longer than six hours.</td>
</tr>
<tr class="odd">
<td>Avro: Maximum size for file data blocks</td>
<td>16 MB</td>
<td>The size limit for Avro file data blocks is 16 MB.</td>
</tr>
<tr class="even">
<td>CSV: Maximum cell size</td>
<td>100 MB</td>
<td>CSV cells can be up to 100 MB in size.</td>
</tr>
<tr class="odd">
<td>CSV: Maximum row size</td>
<td>100 MB</td>
<td>CSV rows can be up to 100 MB in size.</td>
</tr>
<tr class="even">
<td>CSV: Maximum file size - compressed</td>
<td>4 GB</td>
<td>The size limit for a compressed CSV file is 4 GB.</td>
</tr>
<tr class="odd">
<td>CSV: Maximum file size - uncompressed</td>
<td>5 TB</td>
<td>The size limit for an uncompressed CSV file is 5 TB.</td>
</tr>
<tr class="even">
<td>Newline-delimited JSON (ndJSON): Maximum row size</td>
<td>100 MB</td>
<td>ndJSON rows can be up to 100 MB in size.</td>
</tr>
<tr class="odd">
<td>ndJSON: Maximum file size - compressed</td>
<td>4 GB</td>
<td>The size limit for a compressed ndJSON file is 4 GB.</td>
</tr>
<tr class="even">
<td>ndJSON: Maximum file size - uncompressed</td>
<td>5 TB</td>
<td>The size limit for an uncompressed ndJSON file is 5 TB.</td>
</tr>
</tbody>
</table>

If you regularly exceed the load job limits due to frequent updates, consider [streaming data into BigQuery](/bigquery/docs/streaming-data-into-bigquery) instead.

For information on viewing your current load job usage, see [View current quota usage](/bigquery/docs/batch-loading-data#view_current_quota_usage) .

#### BigQuery Data Transfer Service load job quota considerations

Load jobs created by BigQuery Data Transfer Service transfers are included in BigQuery's quotas on load jobs. It's important to consider how many transfers you enable in each project to prevent transfers and other load jobs from producing `  quotaExceeded  ` errors.

You can use the following equation to estimate how many load jobs are required by your transfers:

`  Number of daily jobs = Number of transfers x Number of tables x Schedule frequency x Refresh window  `

Where:

  - `  Number of transfers  ` is the number of transfer configurations you enable in your project.

  - `  Number of tables  ` is the number of tables created by each specific transfer type. The number of tables varies by transfer type:
    
      - Campaign Manager transfers create approximately 25 tables.
      - Google Ads transfers create approximately 60 tables.
      - Google Ad Manager transfers create approximately 40 tables.
      - Google Play transfers create approximately 25 tables.
      - Search Ads 360 transfers create approximately 50 tables.
      - YouTube transfers create approximately 50 tables.

  - `  Schedule frequency  ` describes how often the transfer runs. Transfer run schedules are provided for each transfer type:
    
      - [Campaign Manager](/bigquery/docs/doubleclick-campaign-transfer#connector_overview)
      - [Google Ads](/bigquery/docs/adwords-transfer#connector_overview)
      - [Google Ad Manager](/bigquery/docs/doubleclick-publisher-transfer)
      - [Google Merchant Center](/bigquery/docs/merchant-center-transfer#supported_reports) (beta)
      - [Google Play](/bigquery/docs/play-transfer)
      - [Search Ads 360](/bigquery/docs/search-ads-transfer#connector_overview) (beta)
      - [YouTube Channel](/bigquery/docs/youtube-channel-transfer)
      - [YouTube Content Owner](/bigquery/docs/youtube-content-owner-transfer)

  - `  Refresh window  ` is the number of days to include in the data transfer. If you enter 1, there is no daily backfill.

### Copy jobs

The following limits apply to BigQuery jobs for [copying tables](/bigquery/docs/managing-tables#copy-table) , including jobs that create a copy, clone, or snapshot of a standard table, table clone, or table snapshot. The limits apply to jobs created by using the Google Cloud console, the bq command-line tool, or the [`  jobs.insert  ` method](/bigquery/docs/reference/rest/v2/jobs/insert) that specifies the [`  copy  ` field](/bigquery/docs/reference/rest/v2/Job#JobConfiguration.FIELDS.copy) in the job configuration. Copy jobs count toward these limits whether they succeed or fail.

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Default</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Copy jobs per destination table per day</td>
<td></td>
<td>See <a href="#load_job_per_table.long">Table operations per day</a> .</td>
</tr>
<tr class="even">
<td>Copy jobs per day</td>
<td>100,000 jobs</td>
<td>Your project can run up to 100,000 copy jobs per day.</td>
</tr>
<tr class="odd">
<td>Cross-region copy jobs per destination table per day</td>
<td>100 jobs</td>
<td>Your project can run up to 100 cross-region copy jobs for a destination table per day.</td>
</tr>
<tr class="even">
<td>Cross-region copy jobs per day</td>
<td>2,000 jobs</td>
<td>Your project can run up to 2,000 cross-region copy jobs per day.</td>
</tr>
<tr class="odd">
<td>Number of source tables to copy</td>
<td>1,200 source tables</td>
<td>You can copy from up to 1,200 source tables per copy job.</td>
</tr>
</tbody>
</table>

For information on viewing your current copy job usage, see [Copy jobs - View current quota usage](/bigquery/docs/managing-tables#view_current_quota_usage) . For information on troubleshooting copy jobs, see [Maximum number of copy jobs per day per project quota errors](/bigquery/docs/troubleshoot-quotas#ts-maximum-number-of-copy-jobs-per-day-per-project-quota) .

The following limits apply to [copying datasets](/bigquery/docs/copying-datasets) :

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Default</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Maximum number of tables in the source dataset</td>
<td>25,000 tables</td>
<td>A source dataset can have up to 25,000 tables.</td>
</tr>
<tr class="even">
<td>Maximum number of tables that can be copied per run to a destination dataset in the same region</td>
<td>20,000 tables</td>
<td>Your project can copy a maximum of 20,000 tables per run to a destination dataset within the same region. If a source dataset contains more than 20,000 tables, the BigQuery Data Transfer Service schedules sequential runs, each copying up to 20,000 tables, until all tables are copied. These runs are separated by a default interval of 24 hours, which users can customize down to a minimum of 12 hours.</td>
</tr>
<tr class="odd">
<td>Maximum number of tables that can be copied per run to a destination dataset in a different region</td>
<td>1,000 tables</td>
<td>Your project can copy a maximum of 1,000 tables per run to a destination dataset in a different region. If a source dataset contains more than 1,000 tables, the BigQuery Data Transfer Service schedules sequential runs, each copying up to 1,000 tables, until all tables are copied. These runs are separated by a default interval of 24 hours, which users can customize down to a minimum of 12 hours.</td>
</tr>
</tbody>
</table>

## Reservations

The following quotas apply to [reservations](/bigquery/docs/reservations-intro) :

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th>Quota</th>
<th>Default</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Total number of slots for the EU region</td>
<td>5,000 slots</td>
<td>The maximum number of BigQuery slots you can purchase in the EU multi-region by using the Google Cloud console.<br />
</td>
</tr>
<tr class="even">
<td>Total number of slots for the US region</td>
<td>10,000 slots</td>
<td>The maximum number of BigQuery slots you can purchase in the US multi-region by using the Google Cloud console.<br />
</td>
</tr>
<tr class="odd">
<td>Total number of slots for the <code dir="ltr" translate="no">       us-east1      </code> region</td>
<td>4,000 slots</td>
<td>The maximum number of BigQuery slots that you can purchase in the listed region by using the Google Cloud console.<br />
</td>
</tr>
<tr class="even">
<td>Total number of slots for the following regions:
<ul>
<li><code dir="ltr" translate="no">         asia-south1        </code></li>
<li><code dir="ltr" translate="no">         asia-southeast1        </code></li>
<li><code dir="ltr" translate="no">         europe-west2        </code></li>
<li><code dir="ltr" translate="no">         us-central1        </code></li>
<li><code dir="ltr" translate="no">         us-west1        </code></li>
</ul></td>
<td>2,000 slots</td>
<td>The maximum number of BigQuery slots that you can purchase in each of the listed regions by using the Google Cloud console.<br />
</td>
</tr>
<tr class="odd">
<td>Total number of slots for the following regions:
<ul>
<li><code dir="ltr" translate="no">         asia-east1        </code></li>
<li><code dir="ltr" translate="no">         asia-northeast1        </code></li>
<li><code dir="ltr" translate="no">         asia-northeast3        </code></li>
<li><code dir="ltr" translate="no">         asia-southeast2        </code></li>
<li><code dir="ltr" translate="no">         australia-southeast1        </code></li>
<li><code dir="ltr" translate="no">         europe-north1        </code></li>
<li><code dir="ltr" translate="no">         europe-west1        </code></li>
<li><code dir="ltr" translate="no">         europe-west3        </code></li>
<li><code dir="ltr" translate="no">         europe-west4        </code></li>
<li><code dir="ltr" translate="no">         northamerica-northeast1        </code></li>
<li><code dir="ltr" translate="no">         us-east4        </code></li>
<li><code dir="ltr" translate="no">         southamerica-east1        </code></li>
</ul></td>
<td>1,000 slots</td>
<td>The maximum number of BigQuery slots you can purchase in each of the listed regions by using the Google Cloud console.<br />
</td>
</tr>
<tr class="even">
<td>Total number of slots for BigQuery Omni regions</td>
<td>100 slots</td>
<td>The maximum number of BigQuery slots you can purchase in the <a href="/bigquery/docs/locations#omni-loc">BigQuery Omni</a> regions by using the Google Cloud console.<br />
</td>
</tr>
<tr class="odd">
<td>Total number of slots for all other regions</td>
<td>500 slots</td>
<td>The maximum number of BigQuery slots you can purchase in each other region by using the Google Cloud console.<br />
</td>
</tr>
</tbody>
</table>

The following limits apply to [reservations](/bigquery/docs/reservations-intro) :

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Value</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Number of <a href="/bigquery/docs/reservations-workload-management#admin-project">administration projects</a> for slot reservations</td>
<td>10 projects per organization</td>
<td>The maximum number of projects within an organization that can contain a reservation or an active commitment for slots for a given location / region.</td>
</tr>
<tr class="even">
<td>Maximum number of <a href="/bigquery/docs/editions-intro">standard</a> edition reservations</td>
<td>10 reservations per project</td>
<td>The maximum number of standard edition reservations per administration project within an organization for a given location / region.</td>
</tr>
<tr class="odd">
<td>Maximum number of <a href="/bigquery/docs/editions-intro">Enterprise or Enterprise Plus</a> edition reservations</td>
<td>200 reservations per project</td>
<td>The maximum number of Enterprise or Enterprise Plus edition reservations per administration project within an organization for a given location / region.</td>
</tr>
<tr class="even">
<td>Maximum number of slots in a reservation that is associated with a reservation assignment with a <code dir="ltr" translate="no">       CONTINUOUS      </code> job type.</td>
<td>500 slots</td>
<td>When you want to create a reservation assignment that has a <code dir="ltr" translate="no">       CONTINUOUS      </code> job type, the associated reservation can't have more than 500 slots.</td>
</tr>
</tbody>
</table>

## Datasets

The following limits apply to BigQuery [datasets](/bigquery/docs/datasets) :

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Default</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Maximum number of datasets</td>
<td>Unlimited</td>
<td>There is no limit on the number of datasets that a project can have.</td>
</tr>
<tr class="even">
<td>Number of tables per dataset</td>
<td>Unlimited</td>
<td>When you use an API call, enumeration performance slows as you approach 50,000 tables in a dataset. The Google Cloud console can display up to 50,000 tables for each dataset.</td>
</tr>
<tr class="odd">
<td>Number of authorized resources in a dataset's access control list</td>
<td>2,500 resources</td>
<td><p>A dataset's access control list can have up to 2,500 total authorized resources, including <a href="/bigquery/docs/authorized-views">authorized views</a> , <a href="/bigquery/docs/authorized-datasets">authorized datasets</a> , and <a href="/bigquery/docs/authorized-functions">authorized functions</a> . If you exceed this limit due to a large number of authorized views, consider grouping the views into authorized datasets. As a best practice, group related views into authorized datasets when you design new BigQuery architectures, especially multi-tenant architectures.</p></td>
</tr>
<tr class="even">
<td>Number of dataset update operations per dataset per 10 seconds</td>
<td>5 operations</td>
<td>Your project can make up to five dataset update operations every 10 seconds. The dataset update limit includes all metadata update operations performed by the following:
<ul>
<li>Google Cloud console</li>
<li>The bq command-line tool</li>
<li>BigQuery client libraries</li>
<li>The following API methods:
<ul>
<li><a href="/bigquery/docs/reference/v2/datasets/insert"><code dir="ltr" translate="no">            datasets.insert           </code></a></li>
<li><a href="/bigquery/docs/reference/v2/datasets/patch"><code dir="ltr" translate="no">            datasets.patch           </code></a></li>
<li><a href="/bigquery/docs/reference/v2/datasets/update"><code dir="ltr" translate="no">            datasets.update           </code></a></li>
<li><a href="/bigquery/docs/reference/v2/datasets/delete"><code dir="ltr" translate="no">            datasets.delete           </code></a></li>
<li><a href="/bigquery/docs/reference/rest/v2/datasets/undelete"><code dir="ltr" translate="no">            datasets.undelete           </code></a></li>
</ul></li>
<li>The following DDL statements:
<ul>
<li><a href="/bigquery/docs/reference/standard-sql/data-definition-language#create_schema_statement"><code dir="ltr" translate="no">            CREATE SCHEMA           </code></a></li>
<li><a href="/bigquery/docs/reference/standard-sql/data-definition-language#alter_schema_set_options_statement"><code dir="ltr" translate="no">            ALTER SCHEMA           </code></a></li>
<li><a href="/bigquery/docs/reference/standard-sql/data-definition-language#drop_schema_statement"><code dir="ltr" translate="no">            DROP SCHEMA           </code></a></li>
<li><a href="/bigquery/docs/reference/standard-sql/data-definition-language#undrop_schema_statement"><code dir="ltr" translate="no">            UNDROP SCHEMA           </code></a></li>
</ul></li>
</ul></td>
</tr>
<tr class="odd">
<td>Maximum length of a dataset description</td>
<td>16,384 characters</td>
<td>When you add a description to a dataset, the text can be at most 16,384 characters.</td>
</tr>
</tbody>
</table>

## Tables

### All tables

The following limits apply to all BigQuery tables.

**Note:** Quotas and limits are associated with table names. Therefore, when you truncate the table, or drop the table and then recreate it, the quota/limit doesn't reset, because the table name hasn't changed.

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Default</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Maximum length of a column name</td>
<td>300 characters</td>
<td>Your column name can be at most 300 characters.</td>
</tr>
<tr class="even">
<td>Maximum length of a column description</td>
<td>1,024 characters</td>
<td>When you add a description to a column, the text can be at most 1,024 characters.</td>
</tr>
<tr class="odd">
<td>Maximum depth of nested records</td>
<td>15 levels</td>
<td>Columns of type <code dir="ltr" translate="no">       RECORD      </code> can contain nested <code dir="ltr" translate="no">       RECORD      </code> types, also called <em>child</em> records. The maximum nested depth limit is 15 levels. This limit is independent of whether the records are scalar or array-based (repeated).</td>
</tr>
<tr class="even">
<td>Maximum length of a table description</td>
<td>16,384 characters</td>
<td>When you add a description to a table, the text can be at most 16,384 characters.</td>
</tr>
</tbody>
</table>

For troubleshooting information related to table quotas or limits, see the [BigQuery Troubleshooting page](/bigquery/docs/troubleshoot-quotas) .

### Standard tables

The following limits apply to BigQuery standard (built-in) [tables](/bigquery/docs/tables) :

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Default</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Table modifications per day</td>
<td>1,500 modifications</td>
<td><p>Your project can make up to 1,500 table modifications per table per day. A <a href="/bigquery/quotas#load_jobs">load job</a> , <a href="/bigquery/quotas#copy_jobs">copy job</a> , or <a href="/bigquery/quotas#query_jobs">query job</a> that appends or overwrites table data counts as one modification to the table. This limit cannot be changed.</p>
<p>DML statements are excluded and <em>don't</em> count toward the number of table modifications per day.</p>
<p>Streaming data is excluded and <em>doesn't</em> count toward the number of table modifications per day.</p></td>
</tr>
<tr class="even">
<td>Maximum rate of table metadata update operations per table</td>
<td>5 operations per 10 seconds</td>
<td>Your project can make up to five table metadata update operations per 10 seconds per table. This limit applies to all table metadata update operations, performed by the following:
<ul>
<li>Google Cloud console</li>
<li>The bq command-line tool</li>
<li>BigQuery client libraries</li>
<li>The following API methods:
<ul>
<li><a href="/bigquery/docs/reference/v2/tables/insert"><code dir="ltr" translate="no">            tables.insert           </code></a></li>
<li><a href="/bigquery/docs/reference/v2/tables/patch"><code dir="ltr" translate="no">            tables.patch           </code></a></li>
<li><a href="/bigquery/docs/reference/v2/tables/update"><code dir="ltr" translate="no">            tables.update           </code></a></li>
</ul></li>
<li><a href="/bigquery/docs/reference/standard-sql/data-definition-language">DDL</a> statements on tables</li>
</ul>
This limit also includes the combined total of all load jobs, copy jobs, and query jobs that append to or overwrite a destination table or that use a <a href="/bigquery/docs/reference/standard-sql/dml-syntax">DML</a> <code dir="ltr" translate="no">       DELETE      </code> , <code dir="ltr" translate="no">       INSERT      </code> , <code dir="ltr" translate="no">       MERGE      </code> , <code dir="ltr" translate="no">       TRUNCATE TABLE      </code> , or <code dir="ltr" translate="no">       UPDATE      </code> statements to write data to a table. Note that while DML statements count toward this limit, they are not subject to it if it is reached. DML operations have <a href="/bigquery/quotas#data-manipulation-language-statements">dedicated rate limits</a> .
<p>If you exceed this limit, you get an error message like <code dir="ltr" translate="no">        Exceeded rate limits: too many table update operations for this             table       </code> . This error is transient; you can retry with an exponential backoff.</p>
<p>To identify the operations that count toward this limit, you can <a href="/bigquery/docs/reference/auditlogs#bigqueryauditmetadata_format">Inspect your logs</a> . Refer to <a href="/bigquery/docs/troubleshoot-quotas#ts-maximum-update-table-metadata-limit">Troubleshoot quota errors</a> for guidance on diagnosing and resolving this error.</p></td>
</tr>
<tr class="odd">
<td>Maximum number of columns per table</td>
<td>10,000 columns</td>
<td>Each table, query result, or view definition can have up to 10,000 columns. This includes nested and repeated columns.</td>
</tr>
</tbody>
</table>

### External tables

The following limits apply to BigQuery tables with data stored on Cloud Storage in Parquet, ORC, Avro, CSV, or JSON format:

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Default</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Maximum number of source URIs per external table</td>
<td>10,000 URIs</td>
<td>Each external table can have up to 10,000 source URIs.</td>
</tr>
<tr class="even">
<td>Maximum number of files per external table</td>
<td>10,000,000 files</td>
<td>An external table can have up to 10 million files, including all files matching all wildcard URIs.</td>
</tr>
<tr class="odd">
<td>Maximum size of stored data on Cloud Storage per external table</td>
<td>600 TB</td>
<td>An external table can have up to 600 terabytes across all input files. This limit applies to the file sizes as stored on Cloud Storage; this size is not the same as the size used in the query <a href="https://cloud.google.com/bigquery/pricing#on_demand_pricing">pricing</a> formula. For <a href="/bigquery/docs/hive-partitioned-queries-gcs">externally partitioned</a> tables, the limit is applied after <a href="/bigquery/docs/hive-partitioned-queries-gcs#partition_pruning">partition pruning</a> .</td>
</tr>
<tr class="even">
<td>Maximum number of files in the source Cloud Storage bucket</td>
<td>Approximately 60,000,000 files</td>
<td>An external table can reference a Cloud Storage bucket containing up to approximately 60,000,000 files. For <a href="/bigquery/docs/hive-partitioned-queries-gcs">externally partitioned</a> tables, this limit is applied before <a href="/bigquery/docs/hive-partitioned-queries-gcs#partition_pruning">partition pruning</a> .</td>
</tr>
</tbody>
</table>

### Partitioned tables

The following limits apply to BigQuery [partitioned tables](/bigquery/docs/partitioned-tables) .

**Note:** These limits don't apply to [Hive-partitioned external tables](/bigquery/docs/hive-partitioned-queries) .

Partition limits apply to the combined total of all [load jobs](/bigquery/quotas#load_jobs) , [copy jobs](/bigquery/quotas#copy_jobs) , and [query jobs](/bigquery/quotas#query_jobs) that append to or overwrite a destination partition.

A single job can affect multiple partitions. For example, query jobs and load jobs can write to multiple partitions.

BigQuery uses the number of partitions affected by a job when determining how much of the limit the job consumes. Streaming inserts do not affect this limit.

For information about strategies to stay within the limits for partitioned tables, see [Troubleshooting quota errors](/bigquery/docs/troubleshoot-quotas#ts-number-column-partition-quota) .

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Default</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Number of partitions per partitioned table</td>
<td>10,000 partitions</td>
<td>Each partitioned table can have up to 10,000 partitions. If you exceed this limit, consider using <a href="/bigquery/docs/clustered-tables">clustering</a> in addition to, or instead of, partitioning.</td>
</tr>
<tr class="even">
<td>Number of partitions modified by a single job</td>
<td>4,000 partitions</td>
<td>Each job operation (query or load) can affect up to 4,000 partitions. BigQuery rejects any query or load job that attempts to modify more than 4,000 partitions.</td>
</tr>
<tr class="odd">
<td>Number of partition modifications during ingestion-time per partitioned table per day</td>
<td>11,000 modifications</td>
<td><p>Your project can make up to 11,000 partition modifications per day.</p>
<p>A partition modification is when you append, update, delete, or truncate data in a partitioned table. A partition modification is counted for each type of data modification that you make. For example, deleting one row would count as one partition modification, just as deleting an entire partition would also count as one modification. If you delete a row from one partition and then insert it into another partition, this would count as two partition modifications.</p>
<p>Modifications using DML statements or the streaming API don't count toward the number of partition modifications per day.</p></td>
</tr>
<tr class="even">
<td>Number of partition modifications per column-partitioned table per day</td>
<td>30,000 modifications</td>
<td><p>Your project can make up to 30,000 partition modifications per day for a column-partitioned table.</p>
<p>DML statements <em>do not</em> count toward the number of partition modifications per day.</p>
<p>Streaming data <em>does not</em> count toward the number of partition modifications per day.</p></td>
</tr>
<tr class="odd">
<td>Maximum rate of table metadata update operations per partitioned table</td>
<td>50 modifications per 10 seconds</td>
<td>Your project can make up to 50 modifications per partitioned table every 10 seconds. This limit applies to all partitioned table metadata update operations, performed by the following:
<ul>
<li>Google Cloud console</li>
<li>The bq command-line tool</li>
<li>BigQuery client libraries</li>
<li>The following API methods:
<ul>
<li><a href="/bigquery/docs/reference/v2/tables/insert"><code dir="ltr" translate="no">            tables.insert           </code></a></li>
<li><a href="/bigquery/docs/reference/v2/tables/patch"><code dir="ltr" translate="no">            tables.patch           </code></a></li>
<li><a href="/bigquery/docs/reference/v2/tables/update"><code dir="ltr" translate="no">            tables.update           </code></a></li>
</ul></li>
<li><a href="/bigquery/docs/reference/standard-sql/data-definition-language">DDL</a> statements on tables</li>
</ul>
This limit also includes the combined total of all load jobs, copy jobs, and query jobs that append to or overwrite a destination table or that use a <a href="/bigquery/docs/reference/standard-sql/dml-syntax">DML</a> <code dir="ltr" translate="no">       DELETE      </code> , <code dir="ltr" translate="no">       INSERT      </code> , <code dir="ltr" translate="no">       MERGE      </code> , <code dir="ltr" translate="no">       TRUNCATE TABLE      </code> , or <code dir="ltr" translate="no">       UPDATE      </code> statements to write data to a table.
<p>If you exceed this limit, you get an error message like <code dir="ltr" translate="no">        Exceeded rate limits: too many partitioned table update           operations for this table       </code> . This error is transient; you can retry with an exponential backoff.</p>
<p>To identify the operations that count toward this limit, you can <a href="/bigquery/docs/reference/auditlogs#bigqueryauditmetadata_format">Inspect your logs</a> .</p></td>
</tr>
<tr class="even">
<td>Number of possible ranges for range partitioning</td>
<td>10,000 ranges</td>
<td>A range-partitioned table can have up to 10,000 possible ranges. This limit applies to the partition specification when you create the table. After you create the table, the limit also applies to the actual number of partitions.</td>
</tr>
</tbody>
</table>

### Table clones

The following limits apply to BigQuery [table clones](/bigquery/docs/table-clones-intro) :

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Default</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Maximum number of clones and snapshots in a chain</td>
<td>3 table clones or snapshots</td>
<td>Clones and snapshots in combination are limited to a depth of 3. When you clone or snapshot a base table, you can clone or snapshot the result only two more times; attempting to clone or snapshot the result a third time results in an error. For example, you can create clone A of the base table, create snapshot B of clone A, and create clone C of snapshot B. To make additional duplicates of the third-level clone or snapshot, use a <a href="/bigquery/docs/managing-tables#copy-table">copy operation</a> instead.</td>
</tr>
<tr class="even">
<td>Maximum number of clones and snapshots for a base table</td>
<td>1,000 table clones or snapshots</td>
<td>You can have no more than 1,000 existing clones and snapshots combined of a given base table. For example, if you have 600 snapshots and 400 clones, you reach the limit.</td>
</tr>
</tbody>
</table>

### Table snapshots

The following limits apply to BigQuery [table snapshots](/bigquery/docs/table-snapshots-intro) :

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Default</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Maximum number of concurrent table snapshot jobs</td>
<td>100 jobs</td>
<td>Your project can run up to 100 concurrent table snapshot jobs.</td>
</tr>
<tr class="even">
<td>Maximum number of table snapshot jobs per day</td>
<td>50,000 jobs</td>
<td>Your project can run up to 50,000 table snapshot jobs per day.</td>
</tr>
<tr class="odd">
<td>Maximum number of table snapshot jobs per table per day</td>
<td>50 jobs</td>
<td>Your project can run up to 50 table snapshot jobs per table per day.</td>
</tr>
<tr class="even">
<td>Maximum number of metadata updates per table snapshot per 10 seconds.</td>
<td>5 updates</td>
<td>Your project can update a table snapshot's metadata up to five times every 10 seconds.</td>
</tr>
<tr class="odd">
<td>Maximum number of clones and snapshots in a chain</td>
<td>3 table clones or snapshots</td>
<td>Clones and snapshots in combination are limited to a depth of 3. When you clone or snapshot a base table, you can clone or snapshot the result only two more times; attempting to clone or snapshot the result a third time results in an error. For example, you can create clone A of the base table, create snapshot B of clone A, and create clone C of snapshot B. To make additional duplicates of the third-level clone or snapshot, use a <a href="/bigquery/docs/managing-tables#copy-table">copy operation</a> instead.</td>
</tr>
<tr class="even">
<td>Maximum number of clones and snapshots for a base table</td>
<td>1,000 table clones or snapshots</td>
<td>You can have no more than 1,000 existing clones and snapshots combined of a given base table. For example, if you have 600 snapshots and 400 clones, you reach the limit.</td>
</tr>
</tbody>
</table>

## Views

The following quotas and limits apply to [views](/bigquery/docs/views-intro) and [materialized views](/bigquery/docs/materialized-views-intro) .

### Logical views

The following limits apply to BigQuery standard [views](/bigquery/docs/views-intro) :

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Default</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Maximum number of nested view levels</td>
<td>16 levels</td>
<td>BigQuery supports up to 16 levels of nested views. Creating views up to this limit is possible, but querying is limited to 15 levels. If the limit is exceeded, BigQuery returns an <code dir="ltr" translate="no">       INVALID_INPUT      </code> error.</td>
</tr>
<tr class="even">
<td>Maximum length of a GoogleSQL query used to define a view</td>
<td>256 K characters</td>
<td>A single GoogleSQL query that defines a view can be up to 256 K characters long. This limit applies to a single query and does not include the length of the views referenced in the query.</td>
</tr>
<tr class="odd">
<td>Maximum number of authorized views per dataset</td>
<td></td>
<td>See <a href="#auth_views_in_dataset_acl">Datasets</a> .</td>
</tr>
<tr class="even">
<td>Maximum length of a view description</td>
<td>16,384 characters</td>
<td>When you add a description to a view, the text can be at most 16,384 characters.</td>
</tr>
</tbody>
</table>

### Materialized views

The following limits apply to BigQuery [materialized views](/bigquery/docs/materialized-views-intro) :

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Default</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Base table references (same project)</td>
<td>100 materialized views</td>
<td>Each base table can be referenced by up to 100 materialized views from the same project.</td>
</tr>
<tr class="even">
<td>Base table references (entire organization)</td>
<td>500 materialized views</td>
<td>Each base table can be referenced by up to 500 materialized views from the entire organization.</td>
</tr>
<tr class="odd">
<td>Maximum number of authorized views per dataset</td>
<td></td>
<td>See <a href="#auth_views_in_dataset_acl">Datasets</a> .</td>
</tr>
<tr class="even">
<td>Maximum length of a materialized view description</td>
<td>16,384 characters</td>
<td>When you add a description to a materialized view, the text can be at most 16,384 characters.</td>
</tr>
<tr class="odd">
<td>Materialized view refresh job execution-time limit</td>
<td>12 hours</td>
<td>A <a href="/bigquery/docs/materialized-views-monitor">materialized view refresh job</a> can run for up to 12 hours before it fails.</td>
</tr>
</tbody>
</table>

## Search indexes

The following limits apply to BigQuery [search indexes](/bigquery/docs/search-intro) :

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Default</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Number of <code dir="ltr" translate="no">       CREATE INDEX      </code> DDL statements per project per region per day</td>
<td>500 operations</td>
<td>Your project can issue up to 500 <code dir="ltr" translate="no">       CREATE INDEX      </code> DDL operations every day within a region.</td>
</tr>
<tr class="even">
<td>Number of search index DDL statements per table per day</td>
<td>20 operations</td>
<td>Your project can issue up to 20 <code dir="ltr" translate="no">       CREATE INDEX      </code> or <code dir="ltr" translate="no">       DROP INDEX      </code> DDL operations per table per day.</td>
</tr>
<tr class="odd">
<td>Maximum total size of table data per organization allowed for search index creation that does not run in a reservation</td>
<td>100 TB in multi-regions; 20 TB in all other regions</td>
<td>You can create a search index for a table if the overall size of tables with indexes in your organization is below your region's limit: 100 TB for the <code dir="ltr" translate="no">       US      </code> and <code dir="ltr" translate="no">       EU      </code> multi-regions, and 20 TB for all other regions. If your index-management jobs run in <a href="/bigquery/docs/search-index#use_your_own_reservation">your own reservation</a> , then this limit doesn't apply.</td>
</tr>
<tr class="even">
<td>Number of columns indexed with column granularity per table</td>
<td>63 columns per table</td>
<td>A table can have up to 63 columns with <code dir="ltr" translate="no">       index_granularity      </code> set to <code dir="ltr" translate="no">       COLUMN      </code> . Columns indexed with <code dir="ltr" translate="no">       COLUMN      </code> granularity from setting the <code dir="ltr" translate="no">       default_index_column_granularity      </code> option count towards this limit. There is no limit on the number of columns that are indexed with <code dir="ltr" translate="no">       GLOBAL      </code> granularity. For more information, see <a href="/bigquery/docs/search-index#column-granularity">index with column granularity</a> .</td>
</tr>
</tbody>
</table>

## Vector indexes

The following limits apply to BigQuery [vector indexes](/bigquery/docs/vector-search-intro) :

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Default</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Base table minimum number of rows</td>
<td>5,000 rows</td>
<td>A table must have at least 5,000 rows to create a vector index.</td>
</tr>
<tr class="even">
<td>Base table maximum number of rows for index type <code dir="ltr" translate="no">       IVF      </code></td>
<td>10,000,000,000 rows</td>
<td>A table can have at most 10,000,000,000 rows to create an <code dir="ltr" translate="no">       IVF      </code> vector index</td>
</tr>
<tr class="odd">
<td>Base table maximum number of rows for index type <code dir="ltr" translate="no">       TREE_AH      </code></td>
<td>200,000,000 rows</td>
<td>A table can have at most 200,000,000 rows to create an <code dir="ltr" translate="no">       TREE_AH      </code> vector index</td>
</tr>
<tr class="even">
<td>Base table maximum number of rows for partitioned index type <code dir="ltr" translate="no">       TREE_AH      </code></td>
<td>10,000,000,000 rows in total<br />
<br />
200,000,000 rows for each partition</td>
<td>A table can have at most 10,000,000,000 rows, and each partition can have at most 200,000,000 rows to create a <code dir="ltr" translate="no">       TREE_AH      </code> partitioned vector index.</td>
</tr>
<tr class="odd">
<td>Maximum size of the array in the indexed column</td>
<td>1,600 elements</td>
<td>The column to index can have at most 1,600 elements in the array.</td>
</tr>
<tr class="even">
<td>Minimum table size for vector index population</td>
<td>10 MB</td>
<td>If you create a vector index on a table that is under 10 MB, then the index is not populated. Similarly, if you delete data from a vector-indexed table such that the table size is under 10 MB, then the vector index is temporarily disabled. This happens regardless of whether you use your own reservation for your index-management jobs. Once a vector-indexed table's size again exceeds 10 MB, its index is populated automatically.</td>
</tr>
<tr class="odd">
<td>Number of <code dir="ltr" translate="no">       CREATE VECTOR INDEX      </code> DDL statements per project per region per day</td>
<td>500 operations</td>
<td>For each project, you can issue up to 500 <code dir="ltr" translate="no">       CREATE VECTOR INDEX      </code> operations per day for each region.</td>
</tr>
<tr class="even">
<td>Number of vector index DDL statements per table per day</td>
<td>10 operations</td>
<td>You can issue up to 10 <code dir="ltr" translate="no">       CREATE VECTOR INDEX      </code> or <code dir="ltr" translate="no">       DROP VECTOR INDEX      </code> operations per table per day.</td>
</tr>
<tr class="odd">
<td>Maximum total size of table data per organization allowed for vector index creation that does not run in a reservation</td>
<td>6 TB</td>
<td>You can create a vector index for a table if the total size of tables with indexes in your organization is under 6 TB. If your index-management jobs run in <a href="/bigquery/docs/vector-index#use_your_own_reservation">your own reservation</a> , then this limit doesn't apply.</td>
</tr>
</tbody>
</table>

## Routines

The following quotas and limits apply to [routines](/bigquery/docs/routines) .

### User-defined functions

The following limits apply to both temporary and persistent [user-defined functions (UDFs)](/bigquery/docs/user-defined-functions) in GoogleSQL queries.

**Note:** UDFs and the tables they reference count toward the limit on the [number of resources referenced in a query](#tables_referenced_per_query) .

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Default</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Maximum output per row</td>
<td>5 MB</td>
<td>The maximum amount of data that your JavaScript UDF can output when processing a single row is approximately 5 MB.</td>
</tr>
<tr class="even">
<td>Maximum concurrent legacy SQL queries with Javascript UDFs</td>
<td>6 queries</td>
<td>Your project can have up to six concurrent legacy SQL queries that contain UDFs in JavaScript. This limit includes both interactive and <a href="/bigquery/docs/running-queries#batch">batch</a> queries. This limit does not apply to GoogleSQL queries.</td>
</tr>
<tr class="odd">
<td>Maximum JavaScript UDF resources per query</td>
<td>50 resources</td>
<td>A query job can have up to 50 JavaScript UDF resources, such as inline code blobs or external files.</td>
</tr>
<tr class="even">
<td>Maximum size of inline code blob</td>
<td>32 KB</td>
<td>An inline code blob in a UDF can be up to 32 KB in size.</td>
</tr>
<tr class="odd">
<td>Maximum size of each external code resource</td>
<td>1 MB</td>
<td>The maximum size of each JavaScript code resource is one MB.</td>
</tr>
</tbody>
</table>

The following limits apply to persistent UDFs:

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Default</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Maximum length of a UDF name</td>
<td>256 characters</td>
<td>A UDF name can be up to 256 characters long.</td>
</tr>
<tr class="even">
<td>Maximum number of arguments</td>
<td>256 arguments</td>
<td>A UDF can have up to 256 arguments.</td>
</tr>
<tr class="odd">
<td>Maximum length of an argument name</td>
<td>128 characters</td>
<td>A UDF argument name can be up to 128 characters long.</td>
</tr>
<tr class="even">
<td>Maximum depth of a UDF reference chain</td>
<td>16 references</td>
<td>A UDF reference chain can be up to 16 references deep.</td>
</tr>
<tr class="odd">
<td>Maximum depth of a <code dir="ltr" translate="no">       STRUCT      </code> type argument or output</td>
<td>15 levels</td>
<td>A <code dir="ltr" translate="no">       STRUCT      </code> type UDF argument or output can be up to 15 levels deep.</td>
</tr>
<tr class="even">
<td>Maximum number of fields in <code dir="ltr" translate="no">       STRUCT      </code> type arguments or output per UDF</td>
<td>1,024 fields</td>
<td>A UDF can have up to 1024 fields in <code dir="ltr" translate="no">       STRUCT      </code> type arguments and output.</td>
</tr>
<tr class="odd">
<td>Maximum number of JavaScript libraries in a <code dir="ltr" translate="no">       CREATE FUNCTION      </code> statement</td>
<td>50 libraries</td>
<td>A <code dir="ltr" translate="no">       CREATE FUNCTION      </code> statement can have up to 50 JavaScript libraries.</td>
</tr>
<tr class="even">
<td>Maximum length of included JavaScript library paths</td>
<td>5,000 characters</td>
<td>The path for a JavaScript library included in a UDF can be up to 5,000 characters long.</td>
</tr>
<tr class="odd">
<td>Maximum update rate per UDF per 10 seconds</td>
<td>5 updates</td>
<td>Your project can update a UDF up to five times every 10 seconds.</td>
</tr>
<tr class="even">
<td>Maximum number of authorized UDFs per dataset</td>
<td></td>
<td>See <a href="#auth_views_in_dataset_acl">Datasets</a> .</td>
</tr>
</tbody>
</table>

### Remote functions

The following limits apply to [remote functions](/bigquery/docs/remote-functions) in BigQuery.

For troubleshooting information, see [Maximum number of concurrent queries that contain remote functions](/bigquery/docs/troubleshoot-quotas#ts-maximum-number-of-concurrent-remote-functions) .

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Default</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Maximum number of concurrent queries that contain remote functions</td>
<td>10 queries</td>
<td>You can run up to ten concurrent queries with <a href="/bigquery/docs/remote-functions">remote functions</a> per project.</td>
</tr>
<tr class="even">
<td>Maximum input size</td>
<td>5 MB</td>
<td>The maximum total size of all input arguments from a single row is 5 MB.</td>
</tr>
<tr class="odd">
<td>HTTP response size limit (Cloud Run functions 1st gen)</td>
<td>10 MB</td>
<td>HTTP response body from your Cloud Run function 1st gen is up to 10 MB. Exceeding this value causes query failures.</td>
</tr>
<tr class="even">
<td>HTTP response size limit (Cloud Run functions 2nd gen or Cloud Run)</td>
<td>15 MB</td>
<td>HTTP response body from your Cloud Run function 2nd gen or Cloud Run is up to 15 MB. Exceeding this value causes query failures.</td>
</tr>
<tr class="odd">
<td>Max HTTP invocation time limit (Cloud Run functions 1st gen)</td>
<td>9 minutes</td>
<td>You can set your own time limit for your Cloud Run function 1st gen for an individual HTTP invocation, but the max time limit is <a href="/functions/quotas#time_limits">9 minutes</a> . Exceeding the time limit set for your Cloud Run function 1st gen can cause HTTP invocation failures and query failure.</td>
</tr>
<tr class="even">
<td>HTTP invocation time limit (Cloud Run functions 2nd gen or Cloud Run)</td>
<td>20 minutes</td>
<td>The time limit for an individual HTTP invocation to your Cloud Run function 2nd gen or Cloud Run. Exceeding this value can cause HTTP invocation failures and query failure.</td>
</tr>
<tr class="odd">
<td>Maximum number of HTTP invocation retry attempts</td>
<td>20</td>
<td>The maximum number of retry attempts for an individual HTTP invocation to your Cloud Run function 1st gen, 2nd gen, or Cloud Run. Exceeding this value can cause HTTP invocation failures and query failure.</td>
</tr>
</tbody>
</table>

### Table functions

The following limits apply to BigQuery [table functions](/bigquery/docs/table-functions) :

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Default</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Maximum length of a table function name</td>
<td>256 characters</td>
<td>The name of a table function can be up to 256 characters in length.</td>
</tr>
<tr class="even">
<td>Maximum length of an argument name</td>
<td>128 characters</td>
<td>The name of a table function argument can be up to 128 characters in length.</td>
</tr>
<tr class="odd">
<td>Maximum number of arguments</td>
<td>256 arguments</td>
<td>A table function can have up to 256 arguments.</td>
</tr>
<tr class="even">
<td>Maximum depth of a table function reference chain</td>
<td>16 references</td>
<td>A table function reference chain can be up to 16 references deep.</td>
</tr>
<tr class="odd">
<td>Maximum depth of argument or output of type <code dir="ltr" translate="no">       STRUCT      </code></td>
<td>15 levels</td>
<td>A <code dir="ltr" translate="no">       STRUCT      </code> argument for a table function can be up to 15 levels deep. Similarly, a <code dir="ltr" translate="no">       STRUCT      </code> record in a table function's output can be up to 15 levels deep.</td>
</tr>
<tr class="even">
<td>Maximum number of fields in argument or return table of type <code dir="ltr" translate="no">       STRUCT      </code> per table function</td>
<td>1,024 fields</td>
<td>A <code dir="ltr" translate="no">       STRUCT      </code> argument for a table function can have up to 1,024 fields. Similarly, a <code dir="ltr" translate="no">       STRUCT      </code> record in a table function's output can have up to 1,024 fields.</td>
</tr>
<tr class="odd">
<td>Maximum number of columns in return table</td>
<td>1,024 columns</td>
<td>A table returned by a table function can have up to 1,024 columns.</td>
</tr>
<tr class="even">
<td>Maximum length of return table column names</td>
<td>128 characters</td>
<td>Column names in returned tables can be up to 128 characters long.</td>
</tr>
<tr class="odd">
<td>Maximum number of updates per table function per 10 seconds</td>
<td>5 updates</td>
<td>Your project can update a table function up to five times every 10 seconds.</td>
</tr>
</tbody>
</table>

### Stored procedures for Apache Spark

The following limits apply for [BigQuery stored procedures for Apache Spark](/bigquery/docs/spark-procedures) :

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Limit</strong></th>
<th><strong>Default</strong></th>
<th><strong>Notes</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Maximum number of concurrent stored procedure queries</td>
<td>50</td>
<td>You can run up to 50 concurrent stored procedure queries for each project.</td>
</tr>
<tr class="even">
<td>Maximum number of in-use CPUs</td>
<td>12,000</td>
<td>You can use up to 12,000 CPUs for each project. Queries that have already been processed don't consume this limit.
<p>You can use up to 2,400 CPUs for each location for each project, except in the following locations:</p>
<ul>
<li><code dir="ltr" translate="no">         asia-south2        </code></li>
<li><code dir="ltr" translate="no">         australia-southeast2        </code></li>
<li><code dir="ltr" translate="no">         europe-central2        </code></li>
<li><code dir="ltr" translate="no">         europe-west8        </code></li>
<li><code dir="ltr" translate="no">         northamerica-northeast2        </code></li>
<li><code dir="ltr" translate="no">         southamerica-west1        </code></li>
</ul>
<p>In these locations, you can use up to 500 CPUs for each location for each project.</p>
<p>If you run concurrent queries in a multi-region location and a single region location that is in the same geographic area, then your queries might consume the same concurrent CPU quota.</p></td>
</tr>
<tr class="odd">
<td>Maximum total size of in-use standard persistent disks</td>
<td>204.8 TB</td>
<td><p>You can use up to 204.8 TB standard persistent disks for each location for each project. Queries that have already been processed don't consume this limit.</p>
<p>If you run concurrent queries in a multi-region location and a single region location that is in the same geographic area, then your queries might consume the same standard persistent disk quota.</p></td>
</tr>
</tbody>
</table>

## Notebooks

All [Dataform quotas and limits](/dataform/docs/quotas) and [Colab Enterprise quotas and limits](/colab/docs/quotas) apply to [notebooks in BigQuery](/bigquery/docs/notebooks-introduction) . The following limits also apply:

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Limit</strong></th>
<th><strong>Default</strong></th>
<th><strong>Notes</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Maximum notebook size</td>
<td>20 MB</td>
<td><p>A notebook's size is the total of its content, metadata, and encoding overhead.</p>
<p>You can view the size of notebook content by expanding the notebook header, clicking <strong>View</strong> , and then clicking <strong>Notebook info</strong> .</p></td>
</tr>
<tr class="even">
<td>Maximum number of requests per second to Dataform</td>
<td>100</td>
<td>Notebooks are created and managed through Dataform. Any action that creates or modifies a notebook counts against this quota. This quota is shared with saved queries. For example, if you make 50 changes to notebooks and 50 changes to saved queries within 1 second, you reach the quota.</td>
</tr>
</tbody>
</table>

## Saved queries

All [Dataform quotas and limits](/dataform/docs/quotas) apply to [saved queries](/bigquery/docs/saved-queries-introduction) . The following limits also apply:

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Limit</strong></th>
<th><strong>Default</strong></th>
<th><strong>Notes</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Maximum saved query size</td>
<td>10 MB</td>
<td></td>
</tr>
<tr class="even">
<td>Maximum number of requests per second to Dataform</td>
<td>100</td>
<td>Saved queries are created and managed through Dataform. Any action that creates or modifies a saved query counts against this quota. This quota is shared with notebooks. For example, if you make 50 changes to notebooks and 50 changes to saved queries within 1 second, you reach the quota.</td>
</tr>
</tbody>
</table>

## Data manipulation language

The following limits apply for BigQuery [data manipulation language (DML)](/bigquery/docs/reference/standard-sql/data-manipulation-language) statements:

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Default</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>DML statements per day</td>
<td>Unlimited</td>
<td>The number of DML statements your project can run per day is unlimited.<br />
<br />
DML statements <em>do not</em> count toward the number of <a href="#load_job_per_table.long">table modifications per day</a> or the number of <a href="#load_job_per_partitioned_table.long">partitioned table modifications per day</a> for partitioned tables.<br />
<br />
DML statements have the following <a href="/bigquery/docs/reference/standard-sql/data-manipulation-language#dml-limitations">limitations</a> to be aware of.</td>
</tr>
<tr class="even">
<td>Concurrent <code dir="ltr" translate="no">       INSERT      </code> DML statements per table per day</td>
<td>1,500 statements</td>
<td>The first 1,500 <code dir="ltr" translate="no">       INSERT      </code> statements run immediately after they are submitted. After this limit is reached, the concurrency of <code dir="ltr" translate="no">       INSERT      </code> statements that write to a table is limited to 10. Additional <code dir="ltr" translate="no">       INSERT      </code> statements are added to a <code dir="ltr" translate="no">       PENDING      </code> queue. Up to 100 <code dir="ltr" translate="no">       INSERT      </code> statements can be queued against a table at any given time. When an <code dir="ltr" translate="no">       INSERT      </code> statement completes, the next <code dir="ltr" translate="no">       INSERT      </code> statement is removed from the queue and run.<br />
<br />
If you must run DML <code dir="ltr" translate="no">       INSERT      </code> statements more frequently, consider streaming data to your table using the <a href="/bigquery/docs/write-api">Storage Write API</a> .</td>
</tr>
<tr class="odd">
<td>Concurrent mutating DML statements per table</td>
<td>2 statements</td>
<td>BigQuery runs up to two concurrent mutating DML statements ( <code dir="ltr" translate="no">       UPDATE      </code> , <code dir="ltr" translate="no">       DELETE      </code> , and <code dir="ltr" translate="no">       MERGE      </code> ) for each table. Additional mutating DML statements for a table are queued.</td>
</tr>
<tr class="even">
<td>Queued mutating DML statements per table</td>
<td>20 statements</td>
<td>A table can have up to 20 mutating DML statements in the queue waiting to run. If you submit additional mutating DML statements for the table, then those statements fail.</td>
</tr>
<tr class="odd">
<td>Maximum time in queue for DML statement</td>
<td>7 hours</td>
<td>An interactive priority DML statement can wait in the queue for up to seven hours. If the statement has not run after seven hours, it fails.</td>
</tr>
<tr class="even">
<td>Maximum rate of DML statements for each table</td>
<td>25 statements every 10 seconds</td>
<td>Your project can run up to 25 DML statements every 10 seconds for each table. Both <code dir="ltr" translate="no">       INSERT      </code> and mutating DML statements contribute to this limit.</td>
</tr>
</tbody>
</table>

For more information about mutating DML statements, see [`  INSERT  ` DML concurrency](/bigquery/docs/reference/standard-sql/data-manipulation-language#insert_dml_concurrency) and [`  UPDATE, DELETE, MERGE  ` DML concurrency](/bigquery/docs/reference/standard-sql/data-manipulation-language#update_delete_merge_dml_concurrency) .

## Multi-statement queries

The following limits apply to [multi-statement queries](/bigquery/docs/multi-statement-queries) in BigQuery.

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Default</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Maximum number of concurrent multi-statement queries</td>
<td>1,000 multi-statement queries</td>
<td>Your project can run up to 1,000 concurrent <a href="/bigquery/docs/multi-statement-queries">multi-statement queries</a> .</td>
</tr>
<tr class="even">
<td>Cumulative time limit</td>
<td>24 hours</td>
<td>The cumulative time limit for a multi-statement query is 24 hours.</td>
</tr>
<tr class="odd">
<td>Statement time limit</td>
<td>6 hours</td>
<td>The time limit for an individual statement within a multi-statement query is 6 hours.</td>
</tr>
</tbody>
</table>

## Recursive CTEs in queries

The following limits apply to [recursive common table expressions (CTEs)](/bigquery/docs/recursive-ctes) in BigQuery.

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Default</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Iteration limit</td>
<td>500 iterations</td>
<td>The recursive CTE can execute this number of iterations. If this limit is exceeded, an error is produced. To work around iteration limits, see <a href="/bigquery/docs/reference/standard-sql/recursive-ctes#troubleshoot">Troubleshoot iteration limit errors</a> .</td>
</tr>
</tbody>
</table>

## Row-level security

The following limits apply for BigQuery [row-level access policies](/bigquery/docs/row-level-security-intro) :

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Limit</strong></th>
<th><strong>Default</strong></th>
<th><strong>Notes</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Maximum number of row-access policies per table</td>
<td>400 policies</td>
<td>A table can have up to 400 row-access policies.</td>
</tr>
<tr class="even">
<td>Maximum number of row-access policies per query</td>
<td>6000 policies</td>
<td>A query can access up to a total of 6000 row-access policies.</td>
</tr>
<tr class="odd">
<td>Maximum number of <code dir="ltr" translate="no">       CREATE      </code> / <code dir="ltr" translate="no">       DROP      </code> DDL statements per policy per 10 seconds</td>
<td>5 statements</td>
<td>Your project can make up to five <code dir="ltr" translate="no">       CREATE      </code> or <code dir="ltr" translate="no">       DROP      </code> statements per row-access policy resource every 10 seconds.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       DROP ALL ROW ACCESS POLICIES      </code> statements per table per 10 seconds</td>
<td>5 statements</td>
<td>Your project can make up to five <code dir="ltr" translate="no">       DROP ALL ROW ACCESS POLICIES      </code> statements per table every 10 seconds.</td>
</tr>
</tbody>
</table>

## Data policies

The following limits apply for [column-level dynamic data masking](/bigquery/docs/column-data-masking-intro) :

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Default</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Maximum number of data policies per policy tag.</td>
<td>8 policies per policy tag</td>
<td>Up to eight data policies per policy tag. One of these policies can be used for <a href="/bigquery/docs/column-level-security#set_up_column-level_access_control">column-level access controls</a> . Duplicate masking expressions are not supported.</td>
</tr>
</tbody>
</table>

## Gemini in BigQuery

For customers using Gemini in BigQuery with on-demand compute or with BigQuery Enterprise or Enterprise Plus editions, the quotas for advanced features such as data insights are provided based upon the daily average use of TiB scanned or the slot hours for the last full calendar month. This quota applies to the organization level and is available to all projects in that organization. Quotas are rounded up to the nearest 100 slot hour usage.

For code assistance features, the quota for Gemini Code Assist and Gemini in BigQuery code requests for features like code completion and code generation is the same. For more information, see [Gemini for Google Cloud quotas and limits](/gemini/docs/quotas) .

<table>
<thead>
<tr class="header">
<th>Quotas per 100 slot hours (Enterprise edition or Enterprise Plus edition daily average usage) or per TiB scanned using on-demand compute model</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Requests per day for chat, visualization, table scans, and other requests that display responses in the <strong>Cloud Assist</strong> panel in the Google Cloud console.</td>
<td>5</td>
</tr>
</tbody>
</table>

**Example** : An organization that has an Enterprise edition reservation with 100 slots as its baseline will use an average of 2,400 slot hours each day (100 slots \* 24 hours = 2,400 slot hours). As a result, in the following month they get the following daily quotas: 120 chat, visualizations, data insights table scans, and automated metadata generations per day

If your organization has not purchased any BigQuery Enterprise slots, Enterprise Plus edition slots, or on-demand compute (TiB) until now, then after your first usage you will receive the default quota of the following for the first full calendar month:

  - 250 chat, visualizations, data insights table scans, and automated metadata generations per day

If you start using on-demand compute, Enterprise edition or Enterprise Plus edition reservations mid-month, then the default quota applies until the end of the following month.

## BigQuery ML

The following limits apply to BigQuery ML.

### Query jobs

All [query job quotas and limits](#query_jobs) apply to GoogleSQL query jobs that use BigQuery ML statements and functions.

### `     CREATE MODEL    ` statements

The following limits apply to [`  CREATE MODEL  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create) jobs:

<table style="width:40%;">
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 0%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Default</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         CREATE MODEL       </code> statement queries per 48 hours for each project</td>
<td>20,000 statement queries</td>
<td>Some models are trained by utilizing <a href="/vertex-ai/docs/start/introduction-unified-platform">Vertex AI services</a> , which have their own <a href="/vertex-ai/docs/quotas">resource and quota management</a> .</td>
</tr>
<tr class="even">
<td>Execution-time limit</td>
<td>24 hours or 48 hours</td>
<td><code dir="ltr" translate="no">         CREATE MODEL       </code> job timeout defaults to 24 hours, with the exception of time series, AutoML, and hyperparameter tuning jobs which timeout at 48 hours.</td>
</tr>
</tbody>
</table>

### Generative AI functions

The following limits apply to functions that use Vertex AI large language models (LLMs). For more information, see [Function quota definitions](#function_quota_definitions) .

#### Requests per minute limits

The following limits apply to Vertex AI models that use a requests per minute limit.

Function

Model

Region

Requests per minute

Rows per job

`  AI.GENERATE_TEXT  `  
  
`  ML.GENERATE_TEXT  `  
  
`  AI.GENERATE_TABLE  `  
  
`  AI.GENERATE  `  
  
`  AI.GENERATE_BOOL  `  
  
`  AI.GENERATE_DOUBLE  `  
  
`  AI.GENERATE_INT  `

`  gemini-2.0-flash-lite-001  `

`  US  ` and `  EU  ` multi-regions  
  
Single regions as documented for `  gemini-2.0-flash-lite-001  ` in [Google model endpoint locations](/vertex-ai/generative-ai/docs/learn/locations#google_model_endpoint_locations)

No set quota. Quota determined by [dynamic shared quota (DSQ) <sup>1</sup>](/vertex-ai/generative-ai/docs/dynamic-shared-quota) and [Provisioned Throughput <sup>2</sup>](/vertex-ai/generative-ai/docs/provisioned-throughput/overview)

N/A for Provisioned Throughput  
  
10,500,000 for DSQ, for a call with an average of 500 input tokens and 50 output tokens

`  gemini-2.0-flash-001  `

`  US  ` and `  EU  ` multi-regions  
  
Single regions as documented for `  gemini-2.0-flash-001  ` in [Google model endpoint locations](/vertex-ai/generative-ai/docs/learn/locations#google_model_endpoint_locations)

N/A for Provisioned Throughput  
  
10,200,000 for DSQ, for a call with an average of 500 input tokens and 50 output tokens

`  gemini-2.5-flash  `

`  US  ` and `  EU  ` multi-regions  
  
Single regions as documented for `  gemini-2.5-flash  ` in [Google model endpoint locations](/vertex-ai/generative-ai/docs/learn/locations#google_model_endpoint_locations)

N/A for Provisioned Throughput  
  
9,300,000 for DSQ, for a call with an average of 500 input tokens and 50 output tokens

`  gemini-2.5-pro  `

`  US  ` and `  EU  ` multi-regions  
  
Single regions as documented for `  gemini-2.5-pro  ` in [Google model endpoint locations](/vertex-ai/generative-ai/docs/learn/locations#google_model_endpoint_locations)

N/A for Provisioned Throughput  
  
7,600,000 for DSQ, for a call with an average of 500 input tokens and 50 output tokens

`  AI.IF  `  
  
`  AI.SCORE  `  
  
`  AI.CLASSIFY  `

Various `  gemini-2.5-*  ` models

`  US  ` and `  EU  ` multi-regions  
  
Any single region supported for one of the `  gemini-2.5-* models  ` in [Google model endpoint locations](/vertex-ai/generative-ai/docs/learn/locations#google_model_endpoint_locations)

No set quota. Quota determined by [dynamic shared quota (DSQ) <sup>1</sup>](/vertex-ai/generative-ai/docs/dynamic-shared-quota)

10,000,000 for a call with an average of 500 tokens in each input row and 50 output tokens.

`  AI.GENERATE_TEXT  `  
  
`  ML.GENERATE_TEXT  `

Anthropic Claude

See [Quotas by model and region](/vertex-ai/generative-ai/docs/partner-models/claude/use-claude#quotas)

See [Quotas by model and region](/vertex-ai/generative-ai/docs/partner-models/claude/use-claude#quotas)

The requests per minute value \* 60 \* 6

Llama

See [Llama model region availability and quotas](/vertex-ai/generative-ai/docs/partner-models/llama/use-llama#regions-quotas)

See [Llama model region availability and quotas](/vertex-ai/generative-ai/docs/partner-models/llama/use-llama#regions-quotas)

Mistral AI

See [Mistral AI model region availability and quotas](/vertex-ai/generative-ai/docs/partner-models/mistral#regions-quotas)

See [Mistral AI model region availability and quotas](/vertex-ai/generative-ai/docs/partner-models/mistral#regions-quotas)

`  AI.GENERATE_EMBEDDING 5  `  
  
`  AI.EMBED  `  
  
`  AI.SIMILARITY  `  
  
`  AI.SEARCH  `  
  
`  VECTOR_SEARCH  `  
  
`  ML.GENERATE_EMBEDDING 5  `

`  text-embedding  `  
  
`  text-multilingual-embedding  `

[All regions that support remote models](/bigquery/docs/locations#locations-for-remote-models)

1,500 <sup>3,4</sup>

80,000,000 for a call with an average of 50 tokens in each input row  
  
14,000,000 for a call with an average of 600 tokens in each input row

`  multimodalembedding  `

[Supported European single regions](/bigquery/docs/locations#regions)

120 <sup>3</sup>

14,000

Regions other than [supported European single regions](/bigquery/docs/locations#regions)

600 <sup>3</sup>

25,000

<sup>1</sup> When you use DSQ, there are no predefined quota limits on your usage. Instead, DSQ provides access to a large shared pool of resources, which are dynamically allocated based on real-time availability of resources and the customer demand for the given model. When more customers are active, each customer gets less throughput. Similarly, when fewer customers are active, each customer might get higher throughput.

<sup>2</sup> Provisioned Throughput is a fixed-cost, fixed-term subscription available in several term-lengths. Provisioned Throughput lets you reserve throughput for supported generative AI models on Vertex AI.

<sup>3</sup> To increase the quota, request a [QPM quota adjustment](/docs/quotas/view-manage#requesting_higher_quota) in Vertex AI. Allow 30 minutes for the increased quota value to propagate.

<sup>4</sup> You can increase the quota for Vertex AI `  text-embedding  ` and `  text-multilingual-embedding  ` models to 10,000 RPM without mannual approval. This results in increased throughput of 500,000,000 rows per job or more, based on a call with an average of 50 tokens in each input row.

<sup>5</sup> This function is limited to a maximum of 5 concurrently running jobs per project.

For more information about quota for Vertex AI LLMs, see [Generative AI on Vertex AI quota limits](/vertex-ai/generative-ai/docs/quotas) .

#### Tokens per minute limits

The following limits apply to Vertex AI models that use a tokens per minute limit:

<table>
<thead>
<tr class="header">
<th><strong>Function</strong></th>
<th><strong>Tokens per minute</strong></th>
<th><strong>Rows per job</strong></th>
<th><strong>Number of concurrently running jobs</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate-embedding"><code dir="ltr" translate="no">        AI.GENERATE_EMBEDDING       </code></a> or <a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-generate-embedding"><code dir="ltr" translate="no">        ML.GENERATE_EMBEDDING       </code></a> when using a remote model over a <code dir="ltr" translate="no">       gemini-embedding-001      </code> model</td>
<td>10,000,000</td>
<td>12,000,000, for a call with an average of 300 tokens per row</td>
<td>5</td>
</tr>
</tbody>
</table>

### Cloud AI service functions

The following limits apply to functions that use Cloud AI services:

<table>
<thead>
<tr class="header">
<th><strong>Function</strong></th>
<th><strong>Requests per minute</strong></th>
<th><strong>Rows per job</strong></th>
<th><strong>Number of concurrently running jobs</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-process-document"><code dir="ltr" translate="no">        ML.PROCESS_DOCUMENT       </code></a> with documents averaging fifty pages</td>
<td>600</td>
<td>100,000 (based on an average of 50 pages in each input document)</td>
<td>5</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-transcribe"><code dir="ltr" translate="no">        ML.TRANSCRIBE       </code></a></td>
<td>200</td>
<td>10,000 (based on an average length of 1 minute for each input audio file)</td>
<td>5</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-annotate-image"><code dir="ltr" translate="no">        ML.ANNOTATE_IMAGE       </code></a></td>
<td>1,800</td>
<td>648,000</td>
<td>5</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-translate"><code dir="ltr" translate="no">        ML.TRANSLATE       </code></a></td>
<td>6,000</td>
<td>2,160,000</td>
<td>5</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-understand-text"><code dir="ltr" translate="no">        ML.UNDERSTAND_TEXT       </code></a></td>
<td>600</td>
<td>21,600</td>
<td>5</td>
</tr>
</tbody>
</table>

For more information about quota for Cloud AI service APIs, see the following documents:

  - [Cloud Translation API quota and limits](/translate/quotas)
  - [Vision API quota and limits](/vision/quotas)
  - [Natural Language API quota and limits](/natural-language/quotas)
  - [Document AI quota and limits](/document-ai/quotas)
  - [Speech-to-Text quota and limits](/speech-to-text/quotas)

### Function quota definitions

The following list describes the quotas that apply to generative AI and Cloud AI service functions:

  - Functions that call a Vertex AI model use one Vertex AI quota, which is queries per minute (QPM). In this context, the queries are request calls from the function to the Vertex AI model's API. The QPM quota applies to a base model and all versions, identifiers, and tuned versions of that model. For more information on the Vertex AI model quotas, see [Generative AI on Vertex AI quota limits](/vertex-ai/generative-ai/docs/quotas) .

  - Functions that call a Cloud AI service use the target service's request quotas. Check the given Cloud AI service's quota reference for details.

  - BigQuery ML uses the following quotas:
    
      - **Requests per minute** . This quota is the limit on the number of request calls per minute that functions can make to the Vertex AI model's or Cloud AI service's API. This limit applies to each project and is shared among all jobs using the same model endpoint.
        
        Calls to Vertex AI Gemini models have no predefined quota limits on your usage, because Gemini models use [dynamic shared quota (DSQ)](/vertex-ai/generative-ai/docs/dynamic-shared-quota) . DSQ provides access to a large shared pool of resources, which are dynamically allocated based on real-time availability of resources and the customer demand for the given model.
    
      - **Tokens per minute** . This quota is the limit on the number of tokens per minute that functions can send to the Vertex AI model's API. This limit applies to each project.
        
        For functions that call a Vertex AI foundation model, the number of tokens per minute varies depending on the Vertex AI model endpoint, version, and region, and also your project's reputation. This quota is conceptually the same as the QPM quota used by Vertex AI.
    
      - **Rows per job** . The `  Rows per job  ` value serves as a performance benchmark, approximating the processing capacity when a single job has exclusive use of the project's model endpoint resources. The actual number of processed rows depends on many factors, including the size of the input request to the model, the size of output responses from the model, and availability of dynamic shared quota. The following examples show some common scenarios:
        
          - For the `  gemini-2.0-flash-lite-001  ` endpoint, the number of rows processable by the `  AI.GENERATE_TEXT  ` or `  ML.GENERATE_TEXT  ` function depends on input and output token counts. The service can process approximately 7.6 million rows for calls that have an average input token count of 2,000 and a maximum output token count of 50. This number decreases to about 1 million rows if the average input token count is 10,000 and the maximum output token count is 3,000.
            
            Similarly, the `  gemini-2.0-flash-001  ` endpoint can process 4.4 million rows for calls that have an average input token count of 2,000 and a maximum output token count of 50, but only about 1 million rows with for calls with 10,000 input and 3,000 output tokens.
        
          - The `  ML.PROCESS_DOCUMENT  ` function can process more rows per job for short documents as opposed to long documents.
        
          - The `  ML.TRANSCRIBE  ` function can process more rows per job for short audio clips as opposed to long audio clips.
    
      - **Number of concurrently running jobs** . This quota is the limit per project on the number of SQL queries that can run at the same time for the given function.

The following examples show how to interpret quota limitations in typical situations:

  - I have a quota of 1,000 QPM in Vertex AI, so a query with 100,000 rows should take around 100 minutes. Why is the job running longer?
    
    Job runtimes can vary even for the same input data. In Vertex AI, remote procedure calls (RPCs) have different priorities in order to avoid quota drainage. When there isn't enough quota, RPCs with lower priorities wait and possibly fail if it takes too long to process them.

  - How should I interpret the rows per job quota?
    
    In BigQuery, a query can execute for up to six hours. The maximum supported rows is a function of this timeline and your Vertex AI QPM quota, in order to make sure that BigQuery can complete query processing in six hours. Since typically a query can't use the whole quota, this is a lower number than your QPM quota multiplied by 360.

  - What happens if I run a batch inference job on a table with more rows than the rows per job quota, for example 10,000,000 rows?
    
    BigQuery only processes the number of rows specified by the rows per job quota. You are only charged for the successful API calls for that number of rows, instead of the full 10,000,000 rows in your table. For the rest of the rows, BigQuery responds to the request with a `  A retryable error occurred: the maximum size quota per query has reached  ` error, which is returned in the `  status  ` column of the result. You can use this set of [SQL scripts](https://github.com/GoogleCloudPlatform/bigquery-ml-utils/tree/master/sql_scripts/remote_inference) or this [Dataform package](https://github.com/dataform-co/dataform-bqml) to iterate through inference calls until all rows are successfully processed.

  - I have many more rows to process than the rows per job quota. Will splitting my rows across multiple queries and running them simultaneously help?
    
    No, because these queries are consuming the same BigQuery ML requests per minute quota and Vertex AI QPM quota. If there are multiple queries that all stay within the rows per job quota and number of concurrently running jobs quota, the cumulative processing exhausts the requests per minute quota.

## BI Engine

The following limits apply to [BigQuery BI Engine](/bigquery/docs/bi-engine-intro) .

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Default</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Maximum reservation size per project per location ( <a href="/bigquery/docs/bi-engine-intro">BigQuery BI Engine</a> )</td>
<td>250 GiB</td>
<td>250 Gib is the default maximum reservation size per project per location. You can <a href="https://docs.google.com/forms/d/1KX2E2ggOy1eUNB0Hjf9l9l0Sm0TbmPuS0XvyZtdnRes/viewform">request an increase</a> of the maximum reservation capacity for your projects. Reservation increases are available in most regions, and might take 3 or more business days depending on the size of the increase requested. Please contact your Google Cloud representative or Cloud Customer Care for urgent requests.</td>
</tr>
<tr class="even">
<td>Maximum number of rows per query</td>
<td>7 billion</td>
<td>Maximum number of rows per query.</td>
</tr>
</tbody>
</table>

## BigQuery sharing (formerly Analytics Hub)

The following limits apply to [BigQuery sharing (formerly Analytics Hub)](/bigquery/docs/analytics-hub-introduction) :

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Default</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Maximum number of data exchanges per project</td>
<td>500 exchanges</td>
<td>You can create up to 500 data exchanges in a project.</td>
</tr>
<tr class="even">
<td>Maximum number of listings per data exchange</td>
<td>1,000 listings</td>
<td>You can create up to 1,000 listings in a data exchange.</td>
</tr>
<tr class="odd">
<td>Maximum number of linked datasets per shared dataset</td>
<td>1,000 linked datasets</td>
<td>All BigQuery sharing subscribers, combined, can have a maximum of 1,000 linked datasets per shared dataset.</td>
</tr>
</tbody>
</table>

## Dataplex Universal Catalog automatic discovery

The following limits apply to [Dataplex Universal Catalog automatic discovery](/bigquery/docs/automatic-discovery) :

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Default</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Maximum BigQuery, BigLake, or external tables per Cloud Storage bucket that a discovery scan supports</td>
<td>1000 BigQuery tables per bucket</td>
<td>You can create up to 1,000 BigQuery tables per Cloud Storage bucket.</td>
</tr>
</tbody>
</table>

## API quotas and limits

These quotas and limits apply to [BigQuery API](/bigquery/docs/reference/libraries-overview) requests.

### BigQuery API

The following quotas apply to [BigQuery API](/bigquery/docs/reference/rest) (core) requests:

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th>Quota</th>
<th>Default</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Requests per day</td>
<td>Unlimited</td>
<td>Your project can make an unlimited number of BigQuery API requests per day.<br />
</td>
</tr>
<tr class="even">
<td>Maximum <a href="/bigquery/docs/reference/rest/v2/tabledata/list"><code dir="ltr" translate="no">        tabledata.list       </code></a> bytes per minute</td>
<td>7.5 GB in multi-regions; 3.7 GB in all other regions</td>
<td>Your project can return a maximum of 7.5 GB of table row data per minute via <code dir="ltr" translate="no">       tabledata.list      </code> in the <code dir="ltr" translate="no">       us      </code> and <code dir="ltr" translate="no">       eu      </code> multi-regions, and 3.7 GB of table row data per minute in all other regions. This quota applies to the project that contains the table being read. Other APIs including <a href="/bigquery/docs/reference/v2/jobs/getQueryResults"><code dir="ltr" translate="no">        jobs.getQueryResults       </code></a> and fetching results from <a href="/bigquery/docs/reference/v2/jobs/query"><code dir="ltr" translate="no">        jobs.query       </code></a> and <a href="/bigquery/docs/reference/v2/jobs/insert"><code dir="ltr" translate="no">        jobs.insert       </code></a> can also consume this quota. For troubleshooting information, see the <a href="/bigquery/docs/troubleshoot-quotas#ts-maximum-tabledata-list-bytes-per-second-per-project-quota">Troubleshooting page</a> .<br />

<p>The <a href="/bigquery/docs/reference/storage">BigQuery Storage Read API</a> can sustain significantly higher throughput than <code dir="ltr" translate="no">        tabledata.list       </code> . If you need more throughput than allowed under this quota, consider using the BigQuery Storage Read API.</p></td>
</tr>
</tbody>
</table>

The following limits apply to [BigQuery API](/bigquery/docs/reference/rest) (core) requests:

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Default</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Maximum number of API requests per second per user per method</td>
<td>100 requests</td>
<td>A user can make up to 100 API requests per second to an API method. If a user makes more than 100 requests per second to a method, then throttling can occur. This limit does not apply to <a href="/bigquery/streaming-data-into-bigquery">streaming inserts</a> .<br />
<br />
For troubleshooting information, see the <a href="/bigquery/docs/troubleshoot-quotas#ts-maximum-api-request-limit">Troubleshooting page</a> .</td>
</tr>
<tr class="even">
<td>Maximum number of concurrent API requests per user</td>
<td>300 requests</td>
<td>If a user makes more than 300 concurrent requests, throttling can occur. This limit does not apply to streaming inserts.</td>
</tr>
<tr class="odd">
<td>Maximum request header size</td>
<td>16 KiB</td>
<td>Your BigQuery API request can be up to 16 KiB, including the request URL and all headers. This limit does not apply to the request body, such as in a <code dir="ltr" translate="no">       POST      </code> request.</td>
</tr>
<tr class="even">
<td>Maximum <a href="/bigquery/docs/reference/rest/v2/jobs/get"><code dir="ltr" translate="no">        jobs.get       </code></a> requests per second</td>
<td>1,000 requests</td>
<td>Your project can make up to 1,000 <code dir="ltr" translate="no">       jobs.get      </code> requests per second.</td>
</tr>
<tr class="odd">
<td>Maximum <a href="/bigquery/docs/reference/rest/v2/jobs/query"><code dir="ltr" translate="no">        jobs.query       </code></a> response size</td>
<td>20 MB</td>
<td>By default, there is no maximum row count for the number of rows of data returned by <code dir="ltr" translate="no">       jobs.query      </code> per page of results. However, you are limited to the 20-MB maximum response size. You can alter the number of rows to return by using the <code dir="ltr" translate="no">       maxResults      </code> parameter.</td>
</tr>
<tr class="even">
<td>Maximum <a href="/bigquery/docs/reference/rest/v2/jobs/getQueryResults"><code dir="ltr" translate="no">        jobs.getQueryResults       </code></a> row size</td>
<td>20 MB</td>
<td>The maximum row size is approximate because the limit is based on the internal representation of row data. The limit is enforced during transcoding.</td>
</tr>
<tr class="odd">
<td>Maximum <a href="/bigquery/docs/reference/rest/v2/projects/list"><code dir="ltr" translate="no">        projects.list       </code></a> requests per second</td>
<td>10 requests</td>
<td>A user can make up to 10 <code dir="ltr" translate="no">       projects.list      </code> requests per second.</td>
</tr>
<tr class="even">
<td>Maximum number of <a href="/bigquery/docs/reference/rest/v2/tabledata/list"><code dir="ltr" translate="no">        tabledata.list       </code></a> requests per second</td>
<td>1,000 requests</td>
<td>Your project can make up to 1,000 <code dir="ltr" translate="no">       tabledata.list      </code> requests per second.</td>
</tr>
<tr class="odd">
<td>Maximum rows per <a href="/bigquery/docs/reference/rest/v2/tabledata/list"><code dir="ltr" translate="no">        tabledata.list       </code></a> response</td>
<td>100,000 rows</td>
<td>A <code dir="ltr" translate="no">       tabledata.list      </code> call can return up to 100,000 table rows. For more information, see <a href="/bigquery/docs/paging-results#paging">Paging through results using the API</a> .</td>
</tr>
<tr class="even">
<td>Maximum <a href="/bigquery/docs/reference/rest/v2/tabledata/list"><code dir="ltr" translate="no">        tabledata.list       </code></a> row size</td>
<td>100 MB</td>
<td>The maximum row size is approximate because the limit is based on the internal representation of row data. The limit is enforced during transcoding.</td>
</tr>
<tr class="odd">
<td>Maximum <a href="/bigquery/docs/reference/rest/v2/tables/insert"><code dir="ltr" translate="no">        tables.insert       </code></a> requests per second</td>
<td>10 requests</td>
<td>A user can make up to 10 <code dir="ltr" translate="no">       tables.insert      </code> requests per second. The <code dir="ltr" translate="no">       tables.insert      </code> method creates a new, empty table in a dataset.</td>
</tr>
</tbody>
</table>

### BigQuery Connection API

The following quotas apply to [BigQuery Connection API](/bigquery/docs/working-with-connections) requests:

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th>Quota</th>
<th>Default</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Read requests per minute</td>
<td>1,000 requests per minute</td>
<td>Your project can make up to 1,000 requests per minute to BigQuery Connection API methods that read connection data.<br />
</td>
</tr>
<tr class="even">
<td>Write requests per minute</td>
<td>100 requests per minute</td>
<td>Your project can make up to 100 requests per minute to BigQuery Connection API methods that create or update connections.<br />
</td>
</tr>
<tr class="odd">
<td>BigQuery Omni connections created per minute</td>
<td>10 connections created per minute</td>
<td>Your project can create up to 10 BigQuery Omni connections total across both AWS and Azure per minute.</td>
</tr>
<tr class="even">
<td>BigQuery Omni connection uses</td>
<td>500 connection uses per minute</td>
<td>Your project can use a BigQuery Omni connection up to 500 times per minute. This applies to operations which use your connection to access your AWS account, such as querying a table.</td>
</tr>
</tbody>
</table>

### BigQuery Migration API

The following limits apply to the [BigQuery Migration API](/bigquery/docs/reference/migration/rpc) :

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Default</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Individual file size for batch SQL translation</td>
<td>10 MB</td>
<td>Each individual source and metadata file can be up to 10 MB. This limit does not apply to the metadata zip file produced by the <code dir="ltr" translate="no">       dwh-migration-dumper      </code> command-line extraction tool.</td>
</tr>
<tr class="even">
<td>Total size of source files for batch SQL translation</td>
<td>1 GB</td>
<td>The total size of all input files uploaded to Cloud Storage can be up to 1 GB. This includes all source files, and all metadata files if you choose to include them.</td>
</tr>
<tr class="odd">
<td>Input string size for interactive SQL translation</td>
<td>1 MB</td>
<td>The string that you enter for interactive SQL translation must not exceed 1 MB. When running interactive translations using the Translation API, this limit applies to the total size of all string inputs.</td>
</tr>
<tr class="even">
<td>Maximum configuration file size for interactive SQL translation</td>
<td>50 MB</td>
<td>Individual metadata files (compressed) and YAML config files in Cloud Storage must not exceed 50 MB. If the file size exceeds 50 MB, the interactive translator skips that configuration file during translation and produces an error message. One method to reduce the metadata file size is to use the <code dir="ltr" translate="no">       —database      </code> or <code dir="ltr" translate="no">       –schema      </code> flags to filter on databases when you <a href="/bigquery/docs/generate-metadata#run-dumper">generate the metadata</a> .</td>
</tr>
<tr class="odd">
<td>Maximum number of Gemini suggestions per hour</td>
<td>1,000 (can accumulate up to 10,000 if not used)</td>
<td>If necessary, you can request a quota increase by contacting <a href="https://cloud.google.com/support-hub">Cloud Customer Care</a> .</td>
</tr>
</tbody>
</table>

The following quotas apply to the [BigQuery Migration API](/bigquery/docs/reference/migration/rpc) . The following default values apply in most cases. The defaults for your project might be different:

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th>Quota</th>
<th>Default</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EDWMigration Service List Requests per minute</p>
<p>EDWMigration Service List Requests per minute per user</p></td>
<td><p>12,000 requests</p>
<p>2,500 requests</p></td>
<td><p>Your project can make up to 12,000 Migration API List requests per minute.</p>
<p>Each user can make up to 2,500 Migration API List requests per minute.</p></td>
</tr>
<tr class="even">
<td><p>EDWMigration Service Get Requests per minute</p>
<p>EDWMigration Service Get Requests per minute per user</p></td>
<td><p>25,000 requests</p>
<p>2,500 requests</p></td>
<td><p>Your project can make up to 25,000 Migration API Get requests per minute.</p>
<p>Each user can make up to 2,500 Migration API Get requests per minute.</p></td>
</tr>
<tr class="odd">
<td><p>EDWMigration Service Other Requests per minute</p>
<p>EDWMigration Service Other Requests per minute per user</p></td>
<td><p>25 requests</p>
<p>5 requests</p></td>
<td><p>Your project can make up to 25 other Migration API requests per minute.</p>
<p>Each user can make up to 5 other Migration API requests per minute.</p></td>
</tr>
<tr class="even">
<td><p>Interactive SQL translation requests per minute</p>
<p>Interactive SQL translation requests per minute per user</p></td>
<td><p>200 requests</p>
<p>50 requests</p></td>
<td><p>Your project can make up to 200 SQL translation service requests per minute.</p>
<p>Each user can make up to 50 other SQL translation service requests per minute.</p></td>
</tr>
</tbody>
</table>

### BigQuery Reservation API

The following quotas apply to [BigQuery Reservation API](/bigquery/docs/reference/reservations/rpc) requests:

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th>Quota</th>
<th>Default</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Requests per minute per region</td>
<td>100 requests</td>
<td>Your project can make a total of up to 100 calls to BigQuery Reservation API methods per minute per region.<br />
</td>
</tr>
<tr class="even">
<td>Number of <code dir="ltr" translate="no">       SearchAllAssignments      </code> calls per minute per region</td>
<td>100 requests</td>
<td>Your project can make up to 100 calls to the <a href="/bigquery/docs/reference/reservations/rest/v1/projects.locations/searchAllAssignments"><code dir="ltr" translate="no">        SearchAllAssignments       </code></a> method per minute per region.<br />
</td>
</tr>
<tr class="odd">
<td>Requests for <code dir="ltr" translate="no">       SearchAllAssignments      </code> per minute per region per user</td>
<td>10 requests</td>
<td>Each user can make up to 10 calls to the <a href="/bigquery/docs/reference/reservations/rest/v1/projects.locations/searchAllAssignments"><code dir="ltr" translate="no">        SearchAllAssignments       </code></a> method per minute per region.<br />
<br />
(In the Google Cloud console search results, search for <strong>per user</strong> .)</td>
</tr>
</tbody>
</table>

### BigQuery Data Policy API

The following limits apply for the [Data Policy API](/bigquery/docs/reference/bigquerydatapolicy/rest) ( [preview](https://cloud.google.com/products/#product-launch-stages) ):

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Default</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Maximum number of <a href="/bigquery/docs/reference/bigquerydatapolicy/rest/v1beta1/projects.locations.dataPolicies/list"><code dir="ltr" translate="no">        dataPolicies.list       </code></a> calls.</td>
<td>400 requests per minute per project<br />
<br />
600 requests per minute per organization</td>
<td></td>
</tr>
<tr class="even">
<td>Maximum number of <a href="/bigquery/docs/reference/bigquerydatapolicy/rest/v1beta1/projects.locations.dataPolicies/testIamPermissions"><code dir="ltr" translate="no">        dataPolicies.testIamPermissions       </code></a> calls.</td>
<td>400 requests per minute per project<br />
<br />
600 requests per minute per organization</td>
<td></td>
</tr>
<tr class="odd">
<td>Maximum number of read requests.</td>
<td>1200 requests per minute per project<br />
<br />
1800 requests per minute per organization</td>
<td>This includes calls to <a href="/bigquery/docs/reference/bigquerydatapolicy/rest/v1beta1/projects.locations.dataPolicies/get"><code dir="ltr" translate="no">        dataPolicies.get       </code></a> and <a href="/bigquery/docs/reference/bigquerydatapolicy/rest/v1beta1/projects.locations.dataPolicies/getIamPolicy"><code dir="ltr" translate="no">        dataPolicies.getIamPolicy       </code></a> .</td>
</tr>
<tr class="even">
<td>Maximum number of write requests.</td>
<td>600 requests per minute per project<br />
<br />
900 requests per minute per organization</td>
<td><p>This includes calls to:</p>
<ul>
<li><a href="/bigquery/docs/reference/bigquerydatapolicy/rest/v1beta1/projects.locations.dataPolicies/create"><code dir="ltr" translate="no">          dataPolicies.create         </code></a></li>
<li><a href="/bigquery/docs/reference/bigquerydatapolicy/rest/v1beta1/projects.locations.dataPolicies/delete"><code dir="ltr" translate="no">          dataPolicies.delete         </code></a></li>
<li><a href="/bigquery/docs/reference/bigquerydatapolicy/rest/v1beta1/projects.locations.dataPolicies/setIamPolicy"><code dir="ltr" translate="no">          dataPolicies.setIamPolicy         </code></a></li>
<li><a href="/bigquery/docs/reference/bigquerydatapolicy/rest/v1beta1/projects.locations.dataPolicies/patch"><code dir="ltr" translate="no">          dataPolicies.patch         </code></a></li>
</ul></td>
</tr>
</tbody>
</table>

### IAM API

The following quotas apply when you use [Identity and Access Management](/iam/docs) features in BigQuery to retrieve and set IAM policies, and to test IAM permissions. [Data control language (DCL) statements](/bigquery/docs/reference/standard-sql/data-control-language) count towards `  SetIAMPolicy  ` quota.

**Note:** If you are encountering IAM request constraints, we recommend that you evaluate whether your project can use [IAM permission inheritance](/iam/docs/resource-hierarchy-access-control) to alleviate the constraint.

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th>Quota</th>
<th>Default</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       IamPolicy      </code> requests per minute per user</td>
<td>1,500 requests per minute per user</td>
<td>Each user can make up to 1,500 requests per minute per project.<br />
</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       IamPolicy      </code> requests per minute per project</td>
<td>3,000 requests per minute per project</td>
<td>Your project can make up to 3,000 requests per minute.<br />
</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/locations#regions">Single-region</a> <code dir="ltr" translate="no">       SetIAMPolicy      </code> requests per minute per project</td>
<td>1,000 requests per minute per project</td>
<td>Your single-region project can make up to 1,000 requests per minute.<br />
</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/locations#multi-regions">Multi-region</a> <code dir="ltr" translate="no">       SetIAMPolicy      </code> requests per minute per project</td>
<td>2,000 requests per minute per project</td>
<td>Your multi-region project can make up to 2,000 requests per minute.<br />
</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/locations#omni-loc">Omni-region</a> <code dir="ltr" translate="no">       SetIAMPolicy      </code> requests per minute per project</td>
<td>200 requests per minute per project</td>
<td>Your Omni-region project can make up to 200 requests per minute.<br />
</td>
</tr>
</tbody>
</table>

### Storage Read API

The following quotas apply to [BigQuery Storage Read API](/bigquery/docs/reference/storage) requests:

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th>Quota</th>
<th>Default</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Read data plane requests per minute per user</td>
<td>25,000 requests</td>
<td>Each user can make up to 25,000 <code dir="ltr" translate="no">       ReadRows      </code> calls per minute per project.<br />
</td>
</tr>
<tr class="even">
<td>Read control plane requests per minute per user</td>
<td>5,000 requests</td>
<td>Each user can make up to 5,000 Storage Read API metadata operation calls per minute per project. The metadata calls include the <code dir="ltr" translate="no">       CreateReadSession      </code> and <code dir="ltr" translate="no">       SplitReadStream      </code> methods.<br />
</td>
</tr>
</tbody>
</table>

The following limits apply to [BigQuery Storage Read API](/bigquery/docs/reference/storage) requests:

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Default</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Maximum row/filter length</td>
<td>1 MB</td>
<td>When you use the Storage Read API <code dir="ltr" translate="no">       CreateReadSession      </code> call, you are limited to a maximum length of 1 MB for each row or filter.</td>
</tr>
<tr class="even">
<td>Maximum serialized data size</td>
<td>128 MB</td>
<td>When you use the Storage Read API <code dir="ltr" translate="no">       ReadRows      </code> call, the serialized representation of the data in an individual <code dir="ltr" translate="no">       ReadRowsResponse      </code> message cannot be larger than 128 MB.</td>
</tr>
<tr class="odd">
<td>Maximum concurrent connections</td>
<td>2,000 in multi-regions; 400 in regions</td>
<td>You can open a maximum of 2,000 concurrent <code dir="ltr" translate="no">       ReadRows      </code> connections per project in the <code dir="ltr" translate="no">       us      </code> and <code dir="ltr" translate="no">       eu      </code> multi-regions, and 400 concurrent <code dir="ltr" translate="no">       ReadRows      </code> connections in other regions. In some cases you may be limited to fewer concurrent connections than this limit.</td>
</tr>
<tr class="even">
<td>Maximum per-stream memory usage</td>
<td>1.5 GB</td>
<td>The maximum per-stream memory is approximate because the limit is based on the internal representation of the row data. Streams utilizing more than 1.5 GB memory for a single row might fail. For more information, see <a href="/bigquery/docs/troubleshoot-queries#ts-resources-exceeded">Troubleshoot resources exceeded issues</a> .</td>
</tr>
</tbody>
</table>

### Storage Write API

The following quotas apply to [Storage Write API](/bigquery/docs/write-api) requests. The following quotas can be applied at the folder level. These quotas are then aggregated and shared across all child projects. To enable this configuration, contact [Cloud Customer Care](https://console.cloud.google.com/support/) .

**Note:** Projects that have opted in folder level quota enforcement can only check folder level quota usage and limit in the folder's Google Cloud console quotas page. Project level quota usage and limit won't be displayed. In this case, the project level [monitoring metrics](/monitoring/api/metrics_gcp_a_b#gcp-bigquerystorage) is still a good source for the project level usage.

**Note:** Due to performance optimization, BigQuery might report greater concurrent connections quota usage than the actual quota usage. The deviation can be up to 1% of the total quota or 100 connections, whichever is smaller, multiplied by a factor of 1-4. That means the reported usage can deviate by at most 400 connections in multi-regions with a 10,000 default quota, and 40 connections in small regions with a 1,000 default quota. The quota enforcement is always based on the actual usage, not the reported value.

If you plan to [request a quota adjustment](/docs/quotas/help/request_increase) , include the quota error message in your request to expedite processing. BigQuery might reduce your provisioned quota if your quota is significantly under-utilized for more than one year.

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th>Quota</th>
<th>Default</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Concurrent connections</td>
<td>1,000 in a region; 10,000 in a multi-region</td>
<td><p>The concurrent connections quota is based on the client project that initiates the Storage Write API request, not the project containing the BigQuery dataset resource. The initiating project is the project associated with the <a href="/docs/authentication/api-keys">API key</a> or the <a href="/iam/docs/understanding-service-accounts">service account</a> .</p>
<p>Your project can operate on 1,000 concurrent connections in a region, or 10,000 concurrent connections in the <code dir="ltr" translate="no">        US       </code> and <code dir="ltr" translate="no">        EU       </code> multi-regions.</p>
<p>When you use the <a href="/bigquery/docs/write-api#default_stream">default stream</a> in Java or Go, we recommend using <a href="/bigquery/docs/write-api-best-practices#connection_pool_management">Storage Write API multiplexing</a> to write to multiple destination tables with shared connections in order to reduce the number of overall connections that are needed. If you are using the <a href="https://beam.apache.org/documentation/io/built-in/google-bigquery/#at-least-once-semantics">Beam connector with at-least-once semantics</a> , you can set <a href="https://beam.apache.org/releases/javadoc/current/org/apache/beam/sdk/io/gcp/bigquery/BigQueryOptions.html#setUseStorageApiConnectionPool-java.lang.Boolean-">UseStorageApiConnectionPool</a> to <code dir="ltr" translate="no">        TRUE       </code> to enable multiplexing.</p>
<br />

<p>You can view usage quota and limits metrics for your projects in <a href="/bigquery/docs/monitoring-dashboard#view_quota_usage_and_limits">Cloud Monitoring</a> . Select the concurrent connections limit name based on your region. The options are <code dir="ltr" translate="no">        ConcurrentWriteConnectionsPerProject       </code> , <code dir="ltr" translate="no">        ConcurrentWriteConnectionsPerProjectEU       </code> , and <code dir="ltr" translate="no">        ConcurrentWriteConnectionsPerProjectRegion       </code> for <code dir="ltr" translate="no">        us       </code> , <code dir="ltr" translate="no">        eu       </code> , and other regions, respectively.<br />
<br />
It is strongly recommended that you set up <a href="/monitoring/alerts/using-quota-metrics">alerts</a> to monitor your quota usage and limits. In addition, if your traffic patterns experience spikes and/or regular organic growth, it might be beneficial to consider over-provisioning your quota by 25 - 50% in order to handle unexpected demand.</p></td>
</tr>
<tr class="even">
<td>Throughput</td>
<td>3 GB per second throughput in multi-regions; 300 MB per second in regions</td>
<td>You can stream up to 3 GBps in the <code dir="ltr" translate="no">       us      </code> and <code dir="ltr" translate="no">       eu      </code> multi-regions, and 300 MBps in other regions per project.<br />
<br />

<p>You can view usage quota and limits metrics for your projects in <a href="/bigquery/docs/monitoring-dashboard#view_quota_usage_and_limits">Cloud Monitoring</a> . Select the throughput limit name based on your region. The options are <code dir="ltr" translate="no">        AppendBytesThroughputPerProject       </code> , <code dir="ltr" translate="no">        AppendBytesThroughputPerProjectEU       </code> , and <code dir="ltr" translate="no">        AppendBytesThroughputPerProjectRegion       </code> for <code dir="ltr" translate="no">        us       </code> , <code dir="ltr" translate="no">        eu       </code> , and other regions, respectively. Write throughput quota is metered based on the project where the target dataset resides, not the client project.<br />
<br />
It is strongly recommended that you set up <a href="/monitoring/alerts/using-quota-metrics">alerts</a> to monitor your quota usage and limits. In addition, if your traffic patterns experience spikes and/or regular organic growth, it might be beneficial to consider over-provisioning your quota by 25 - 50% in order to handle unexpected demand.</p>
<br />
</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       CreateWriteStream      </code> requests</td>
<td>10,000 streams every hour, per project per region</td>
<td>You can call <code dir="ltr" translate="no">       CreateWriteStream      </code> up to 10,000 times per hour per project per region. Consider using the <a href="/bigquery/docs/write-api#default_stream">default stream</a> if you don't need exactly-once semantics. This quota is per hour but the metric shown in the Google Cloud console is per minute.</td>
</tr>
<tr class="even">
<td>Pending stream bytes</td>
<td>10 TB in multi-regions; 1 TB in regions</td>
<td>For every commit that you trigger, you can commit up to 10 TB in the <code dir="ltr" translate="no">       us      </code> and <code dir="ltr" translate="no">       eu      </code> multi-regions, and 1 TB in other regions. There is no quota reporting on this quota.</td>
</tr>
</tbody>
</table>

The following limits apply to [Storage Write API](/bigquery/docs/write-api) requests:

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Default</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Batch commits</td>
<td>10,000 streams per table</td>
<td>You can commit up to 10,000 streams in each <code dir="ltr" translate="no">       BatchCommitWriteStream      </code> call.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       AppendRows      </code> request size</td>
<td>10 MB</td>
<td>The maximum request size is 10 MB.</td>
</tr>
</tbody>
</table>

## Streaming inserts

The following quotas and limits apply when you stream data into BigQuery by using the [legacy streaming API](/bigquery/docs/streaming-data-into-bigquery) . For information about strategies to stay within these limits, see [Troubleshooting quota errors](/bigquery/docs/troubleshoot-quotas#ts-streaming-insert-quota) . If you exceed these quotas, BigQuery returns a `  quotaExceeded  ` error. BigQuery might reduce your provisioned quota if your quota is significantly under-utilized for more than one year.

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Default</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Maximum bytes per second per project in the <code dir="ltr" translate="no">       us      </code> and <code dir="ltr" translate="no">       eu      </code> multi-regions</td>
<td>1 GB per second</td>
<td><p>Your project can stream up to 1 GB per second. This quota is cumulative within a given multi-region. In other words, the sum of bytes per second streamed to all tables for a given project within a multi-region is limited to 1 GB.</p>
<p>Exceeding this limit causes <code dir="ltr" translate="no">        quotaExceeded       </code> errors.</p>
<p>If necessary, you can request a quota increase by contacting <a href="https://cloud.google.com/support-hub">Cloud Customer Care</a> . Request any increase as early as possible, at minimum two weeks before you need it. Quota increase takes time to become available, especially in the case of a significant increase.</p></td>
</tr>
<tr class="even">
<td>Maximum bytes per second per project in all other locations</td>
<td>300 MB per second</td>
<td><p>Your project can stream up to 300 MB per second in all locations except the <code dir="ltr" translate="no">        us       </code> and <code dir="ltr" translate="no">        eu       </code> multi-regions. This quota is cumulative within a given multi-region. In other words, the sum of bytes per second streamed to all tables for a given project within a region is limited to 300 MB.</p>
<p>Exceeding this limit causes <code dir="ltr" translate="no">        quotaExceeded       </code> errors.</p>
<p>If necessary, you can request a quota increase by contacting <a href="https://cloud.google.com/support-hub">Cloud Customer Care</a> . Request any increase as early as possible, at minimum two weeks before you need it. Quota increase takes time to become available, especially in the case of a significant increase.</p></td>
</tr>
<tr class="odd">
<td>Maximum row size</td>
<td>10 MB</td>
<td>Exceeding this value causes <code dir="ltr" translate="no">       invalid      </code> errors.</td>
</tr>
<tr class="even">
<td>HTTP request size limit</td>
<td>10 MB</td>
<td><p>Exceeding this value causes <code dir="ltr" translate="no">        invalid       </code> errors.</p>
<p>Internally the request is translated from HTTP JSON into an internal data structure. The translated data structure has its own enforced size limit. It's hard to predict the size of the resulting internal data structure, but if you keep your HTTP requests to 10 MB or less, the chance of hitting the internal limit is low.</p></td>
</tr>
<tr class="odd">
<td>Maximum rows per request</td>
<td>50,000 rows</td>
<td>A maximum of 500 rows is recommended. Batching can increase performance and throughput to a point, but at the cost of per-request latency. Too few rows per request and the overhead of each request can make ingestion inefficient. Too many rows per request and the throughput can drop. Experiment with representative data (schema and data sizes) to determine the ideal batch size for your data.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       insertId      </code> field length</td>
<td>128 characters</td>
<td>Exceeding this value causes <code dir="ltr" translate="no">       invalid      </code> errors.</td>
</tr>
</tbody>
</table>

For additional streaming quota, see [Request a quota increase](#requesting_a_quota_increase) .

## Bandwidth

The following quotas apply to the replication bandwidth:

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 15%" />
<col style="width: 60%" />
</colgroup>
<thead>
<tr class="header">
<th>Quota</th>
<th>Default</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Maximum initial backfill replication bandwidth for each <a href="/bigquery/docs/locations#regions">region</a> that has cross-region data egress from the primary replica to secondary replicas.</td>
<td>10 physical GiBps per region per organization</td>
<td></td>
</tr>
<tr class="even">
<td>Maximum ongoing replication bandwidth for each <a href="/bigquery/docs/locations#regions">region</a> that has cross-region data egress from the primary replica to secondary replicas.</td>
<td>5 physical GiBps per region per organization</td>
<td></td>
</tr>
<tr class="odd">
<td>Maximum turbo replication bandwidth for each <a href="/bigquery/docs/locations#regions">region</a> that has cross-region data egress from the primary replica to secondary replicas.</td>
<td>5 physical GiBps per region per organization</td>
<td>Turbo replication bandwidth quota doesn't apply to the initial backfill operation.</td>
</tr>
</tbody>
</table>

When a project's replication bandwidth exceeds a certain quota, replication from affected projects might stop with the `  rateLimitExceeded  ` error that includes details of the exceeded quota.
