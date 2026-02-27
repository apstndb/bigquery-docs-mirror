# Troubleshoot query issues

This document is intended to help you troubleshoot common issues related to running queries, such as identifying reasons for slow queries, or providing resolution steps for common errors returned by failed queries.

## Troubleshoot slow queries

When troubleshooting slow query performance, consider the following common causes:

1.  Check the [Google Cloud Service Health](https://status.cloud.google.com/) page for known BigQuery service outages that might impact query performance.

2.  Review the job timeline for your query on the [job details page](/bigquery/docs/managing-jobs#view-job) to see how long each stage of the query took to run.
    
      - If most of the elapsed time was due to long creation times, [contact Cloud Customer Care](/support) for assistance.
    
      - If most of the elapsed time was due to long execution times, then review your [query performance insights](/bigquery/docs/query-insights) . Query performance insights can inform you if your query ran longer than the average execution time, and suggest possible causes. Possible causes might include query slot contention or an insufficient shuffle quota. For more information about each query performance issue and possible resolutions, see [Interpret query performance insights](/bigquery/docs/query-insights#interpret_query_performance_insights) .

3.  Review the `  finalExecutionDurationMs  ` field in the [`  JobStatistics  `](/bigquery/docs/reference/rest/v2/Job#JobStatistics) for your query job. The query might have been retried. The `  finalExecutionDurationMs  ` field contains the duration in milliseconds of the execution of the final attempt of this job.

4.  Review the bytes processed in the [query job details page](/bigquery/docs/managing-jobs#view-job) to see if it is higher than expected. You can do this by comparing the number of bytes processed by the current query with another query job that completed in an acceptable amount of time. If there is a large discrepancy of bytes processed between the two queries, then perhaps the query was slow due to a large data volume. For information on optimizing your queries to handle large data volumes, see [Optimize query computation](/bigquery/docs/best-practices-performance-compute) .
    
    You can also identify queries in your project that process a large amount of data by searching for the most expensive queries using the [`  INFORMATION_SCHEMA.JOBS  ` view](/bigquery/docs/information-schema-jobs#most_expensive_queries_by_project) .

### Compare a slow and fast execution of the same query

If a query that previously ran quickly is now running slowly, examine the [Job API object](/bigquery/docs/reference/rest/v2/Job) output to identify changes in its execution.

#### Cache hits

Confirm whether the fast execution of the job was a cache hit by looking at the [`  cacheHit  `](/bigquery/docs/reference/rest/v2/Job#jobstatistics2) value. If the value is `  true  ` for the fast execution of the query, then the query used [cached results](/bigquery/docs/cached-results) instead of executing the query.

If you expect the slow job to use cached results, investigate why the query is [no longer using cached results](/bigquery/docs/cached-results#cache-exceptions) . If you don't expect the query to retrieve data from the cache, look for a fast query execution example that didn't hit the cache for the investigation.

#### Quota delays

To determine whether the slowdown was caused by any quota deferments, check the [`  quotaDeferments  ` field](/bigquery/docs/reference/rest/v2/Job#jobstatistics) for both jobs. Compare the values to determine whether the slower query's start time was delayed by any quota deferments that didn't affect the faster job.

#### Execution duration

To understand the difference between the execution duration of the last attempt of both jobs, compare their values for the [`  finalExecutionDurationMs  ` field](/bigquery/docs/reference/rest/v2/Job#jobstatistics2) .

If the values for `  finalExecutionDurationMs  ` are quite similar, but the difference in the wall execution time between the two queries, calculated as [`  startTime - endTime  `](/bigquery/docs/reference/rest/v2/Job#jobstatistics) , is much larger, this means that there could have been an internal query execution retry for the slow job due to a possible transient issue. If you see this difference pattern repeatedly, [contact Cloud Customer Care](/support) for assistance

#### Bytes processed

Review the bytes processed in the [query job details page](/bigquery/docs/managing-jobs#view-job) or look at the `  totalBytesProcessed  ` from [JobStatistics](/bigquery/docs/reference/rest/v2/Job#jobstatistics) to see if it is higher than expected. If there is a large discrepancy of bytes processed between the two queries, then the query might be slow due to a change in the volume of data processed. For information on optimizing queries to handle large data volumes, see [Optimize query computation](/bigquery/docs/best-practices-performance-compute) . The following reasons can cause an increase in the number of bytes processed by a query:

  - The size of the tables referenced by the query has increased.
  - The query is now reading a larger partition of the table.
  - The query references a view whose definition has changed.

#### Referenced tables

Check whether the queries read the same tables by analyzing the output of the `  referencedTables  ` field in [`  JobStatistics2  `](/bigquery/docs/reference/rest/v2/Job#jobstatistics2) . Differences in the referenced tables can be explained by the following:

  - The SQL query was modified to read different tables. Compare the query text to confirm this.
  - The view definition has changed between executions of the query. Check the definitions of the views referenced in this query and [update them](/bigquery/docs/managing-views) if necessary.

Differences in referenced tables could explain changes in [`  totalBytesProcessed  `](/bigquery/docs/reference/rest/v2/Job#jobstatistics) .

#### Materialized view usage

If the query references any [materialized views](/bigquery/docs/materialized-views-intro) , differences in performance can be caused by materialized views being chosen or rejected during query execution. Inspect [`  MaterializedViewStatistics  `](/bigquery/docs/reference/rest/v2/Job#materializedviewstatistics) to understand whether any materialized views used in the fast query were rejected in the slow query. Look at the `  chosen  ` and `  rejectedReason  ` fields in the [`  MaterializedView  ` object](/bigquery/docs/reference/rest/v2/Job#materializedview) .

#### Metadata caching statistics

For queries that involve Amazon S3 BigLake tables or Cloud Storage BigLake tables with metadata caching enabled, compare the output of the [`  MetadataCacheStatistics  `](/bigquery/docs/reference/rest/v2/Job#metadatacachestatistics) to check whether there is a difference in metadata cache usage between the slow and fast query and corresponding reasons. For example, the metadata cache might be outside the table's `  maxStaleness  ` window.

#### Comparing BigQuery BI Engine statistics

If the query uses BigQuery BI Engine, analyze the output of [`  BiEngineStatistics  `](/bigquery/docs/reference/rest/v2/Job#bienginestatistics) to determine whether the same acceleration modes were applied to both the slow and fast query. Look at the [`  BiEngineReason  `](/bigquery/docs/reference/rest/v2/Job#bienginereason) field to understand the high-level reason for partial acceleration or no acceleration at all, such as not enough memory, missing a reservation, or input being too large.

#### Reviewing differences in query performance insights

Compare the [query performance insights](/bigquery/docs/query-insights) for each of the queries by looking at the [**Execution Graph**](/bigquery/docs/query-insights#view_query_performance_insights) in the Google Cloud console or the [`  StagePerformanceStandaloneInsight  `](/bigquery/docs/reference/rest/v2/Job#stageperformancestandaloneinsight) object to understand the following possible issues:

  - Slot contention ( [`  slotContention  `](/bigquery/docs/reference/rest/v2/Job#stageperformancestandaloneinsight) )
  - High cardinality joins ( [`  highCardinalityJoins  `](/bigquery/docs/reference/rest/v2/Job#highcardinalityjoin) )
  - Insufficient shuffle quota ( [`  insufficientShuffleQuota  `](/bigquery/docs/reference/rest/v2/Job#stageperformancestandaloneinsight) )
  - Data skew ( [`  partitionSkew  `](/bigquery/docs/reference/rest/v2/Job#PartitionSkew) )

Pay attention to both the insights provided for the slow job as well as differences between insights produced for the fast job to identify stage changes affecting performance.

A more thorough job execution metadata analysis requires going through the single stages of query execution by comparing the [`  ExplainQueryStage  `](/bigquery/docs/reference/rest/v2/Job#explainquerystage) objects for the two jobs.

To get started, look at the `  Wait ms  ` and `  Shuffle output bytes  ` metrics described in the [interpret query stage information](/bigquery/docs/query-insights#interpret_query_stage_information) section.

#### Resource warnings from the `     INFORMATION_SCHEMA.JOBS    ` view

Query the `  query_info.resource_warning  ` field of the [`  INFORMATION_SCHEMA.JOBS  ` view](/bigquery/docs/information-schema-jobs) to see if there is a difference in the warnings analyzed by BigQuery with respect to resources used.

### Workload statistics analysis

Available slot resources and slot contention can affect query execution time. The following sections help you understand the slot usage and availability for a particular run of a query.

#### Average slots per second

To compute the average number of slots used per millisecond by the query, divide the slot-milliseconds value for the job, `  totalSlotMs  ` from [`  JobStatistics2  `](/bigquery/docs/reference/rest/v2/Job#jobstatistics2) , by the duration in milliseconds of the execution of the final attempt of this job, `  finalExecutionDurationMs  ` from [`  JobStatistics  `](/bigquery/docs/reference/rest/v2/Job#jobstatistics) .

You can also compute the [average number of slots per millisecond used by a job](/bigquery/docs/information-schema-jobs#average_number_of_slots_per_millisecond_used_by_a_job) by querying the `  INFORMATION_SCHEMA.JOBS  ` view

A job performing a similar amount of work with a larger amount of average slots per second completes faster. A lower average slot usage per second can be caused by the following:

1.  There were no additional resources available due to a resource contention between different jobs - the reservation was maxed out.
2.  The job didn't request more slots during a large part of the execution. For example, this can happen when there is data skew.

#### Workload management models and reservation size

If you use the on-demand billing model, the number of slots that you can use per project is limited. Your project might also occasionally have fewer slots available if there is a high amount of contention for on-demand capacity in a specific location.

The capacity-based model is more predictable and lets you specify a confirmed number of baseline slots.

Take these differences into account when comparing a query execution run using on-demand to a query execution that uses a reservation.

[Using a reservation](/bigquery/docs/reservations-workload-management) is recommended to have stable predictable query execution performance. For more information about the differences between on-demand and capacity-based workloads, see [Introduction to workload management](/bigquery/docs/reservations-intro) .

#### Job concurrency

Job concurrency represents the competition among jobs for slot resources during query execution. Higher job concurrency generally causes slower job execution because the job has access to fewer slots.

You can query the `  INFORMATION_SCHEMA.JOBS  ` view to [find the average number of concurrent jobs](/bigquery/docs/information-schema-jobs#view_average_concurrent_jobs_running_alongside_a_particular_job_in_the_same_project) that are running at the same time as a particular query within a project.

If there is more than one project assigned to a reservation, modify the query to use `  JOBS_BY_ORGANIZATION  ` instead of `  JOBS_BY_PROJECT  ` to get accurate reservation-level data.

A higher average concurrency during the slow job execution compared to the fast job is a contributing factor to the overall slowness.

Consider reducing the concurrency within the project or reservation by spreading out resource intensive queries, either over time within a reservation or project or over different reservations or projects.

Another solution is to purchase a reservation or increase an existing reservation's size. Consider allowing the reservation to [use idle slots](/bigquery/docs/reservations-tasks#configure_whether_queries_use_idle_slots) .

To understand how many slots to add, read about [estimating slot capacity requirements](/bigquery/docs/slot-estimator) .

Jobs running in reservations with more than one project assigned can experience different slot assignment outcomes with the same average job concurrency depending on which project is running them. Read about [fair scheduling](/bigquery/docs/slots#fair_scheduling_in_bigquery) to learn more.

#### Reservation utilization

[Admin resource charts](/bigquery/docs/admin-resource-charts) and [BigQuery Cloud Monitoring](/bigquery/docs/monitoring-dashboard) can be used to monitor reservation utilization. For more information, see [Monitor BigQuery reservations](/bigquery/docs/reservations-monitoring) .

To understand whether a job requested any additional slots, look at the estimated runnable units metric, which is [`  estimatedRunnableUnits  `](/bigquery/docs/reference/rest/v2/Job#querytimelinesample) from the Job API response, or `  period_estimated_runnable_units  ` in the [`  INFORMATION_SCHEMA.JOBS_TIMELINE  ` view](/bigquery/docs/information-schema-jobs-timeline) . If the value for this metric is more than 0, then the job could have benefited from additional slots at that time. To estimate the percentage of the job execution time where the job would have benefited from additional slots, run the following query against the [`  INFORMATION_SCHEMA.JOBS_TIMELINE  ` view](/bigquery/docs/information-schema-jobs-timeline) :

``` text
SELECT
  ROUND(COUNTIF(period_estimated_runnable_units > 0) / COUNT(*) * 100, 1) AS execution_duration_percentage
FROM `myproject`.`region-us`.INFORMATION_SCHEMA.JOBS_TIMELINE
WHERE job_id = 'my_job_id'
GROUP BY job_id;
```

The result is similar to the following:

``` text
+---------------------------------+
|   execution_duration_percentage |
+---------------------------------+
|                            96.7 |
+---------------------------------+
```

A low percentage means the slot resource availability is not a major contributor to the query slowness in this scenario.

If the percentage is high and the reservation wasn't fully utilized during this time, [contact Cloud Customer Care](/support) to investigate.

If the reservation was fully utilized during the slow job execution and the percentage is high, the job was constrained on resources. Consider reducing concurrency, increasing the reservation size, allowing the reservation to use idle slots, or purchasing a reservation if the job was run on-demand.

### Job metadata and workload analysis findings inconclusive

If you still can't find the reason to explain slower than expected query performance, [contact Cloud Customer Care](/support) for assistance.

## Troubleshoot query failure using Gemini Cloud Assist

To use Gemini Cloud Assist to help you [identify the cause of a query failure](/bigquery/docs/use-cloud-assist#analyze_jobs) , do the following:

1.  In the Google Cloud console, go the **BigQuery** page.

2.  On the Google Cloud toolbar, click spark **Open or close Gemini Cloud Assist chat** .

3.  In the **Cloud Assist** panel, enter a prompt that includes the job ID—for example, `  Why did JOB_ID fail?  `

## Troubleshoot query failure using `     gcpdiag    `

[`  gcpdiag  `](https://gcpdiag.dev) is an open source tool. It is not an officially supported Google Cloud product. You can use the `  gcpdiag  ` tool to help you identify and fix Google Cloud project issues. For more information, see the [gcpdiag project on GitHub](https://github.com/GoogleCloudPlatform/gcpdiag/#gcpdiag---diagnostics-for-google-cloud-platform) .

The [`  gcpdiag  `](https://gcpdiag.dev/) tool helps you analyze failed BigQuery queries to understand if there is a known root cause and mitigation for the specific failure.

### Run the `      gcpdiag     ` command

You can run the `  gcpdiag  ` command from Google Cloud CLI:

## Google Cloud console

1.  Complete and then copy the following command.
2.  Open the Google Cloud console and activate Cloud Shell.
3.  Paste the copied command.
4.  Run the `  gcpdiag  ` command, which downloads the `  gcpdiag  ` docker image, and then performs diagnostic checks. If applicable, follow the output instructions to fix failed checks.

## Docker

You can [run `  gcpdiag  ` using a wrapper](https://github.com/GoogleCloudPlatform/gcpdiag?tab=readme-ov-file#installation) that starts `  gcpdiag  ` in a [Docker](https://www.docker.com/) container. Docker or [Podman](https://podman.io/) must be installed.

1.  Copy and run the following command on your local workstation.
    
    ``` console
    curl https://gcpdiag.dev/gcpdiag.sh >gcpdiag && chmod +x gcpdiag
    ```

2.  Execute the `  gcpdiag  ` command.
    
    ``` text
    ./gcpdiag runbook bigquery/failed_query \
       --parameter project_id=PROJECT_ID \
       --parameter bigquery_job_region=JOB_REGION \
       --parameter bigquery_job_id=JOB_ID \
       --parameter bigquery_skip_permission_check=SKIP_PERMISSION_CHECK
    ```

View [available parameters](https://gcpdiag.dev/runbook/diagnostic-trees/bigquery/failed_query/#parameters) for this runbook.

Replace the following:

  - PROJECT\_ID : The ID of the project containing the resource.
  - JOB\_REGION : The region where the BigQuery job was executed.
  - JOB\_ID : The job identifier of the BigQuery job.
  - SKIP\_PERMISSION\_CHECK : (Optional) set this to `  True  ` if you want to skip the relevant permissions check and speed up the runbook execution (default value is `  False  ` ).

Useful flags:

  - `  --universe-domain  ` : If applicable, the [Trusted Partner Sovereign Cloud](https://cloud.google.com/blog/products/identity-security/new-sovereign-controls-for-gcp-via-assured-workloads) domain hosting the resource
  - `  --parameter  ` or `  -p  ` : Runbook parameters

For a list and description of all `  gcpdiag  ` tool flags, see the [`  gcpdiag  ` usage instructions](https://github.com/GoogleCloudPlatform/gcpdiag?tab=readme-ov-file#usage) .

## Avro schema resolution

Error string: `  Cannot skip stream  `

This error can occur when loading multiple Avro files with different schemas, resulting in a schema resolution issue and causing the import job to fail at a random file.

To address this error, ensure that the last alphabetical file in the load job contains the superset (union) of the differing schemas. This is a requirement based on [how Avro handles schema resolution](https://avro.apache.org/docs/1.8.1/spec.html#Schema+Resolution) .

## Conflicting concurrent queries

Error string: `  Concurrent jobs in the same session are not allowed  `

This error can occur when multiple queries are running concurrently in a session, which is not supported. See session [limitations](/bigquery/docs/sessions-intro#limitations) .

## Conflicting DML statements

Error string: `  Could not serialize access to table due to concurrent update  `

This error can occur when mutating data manipulation language (DML) statements that are running concurrently on the same table conflict with each other, or when the table is truncated during a mutating DML statement. For more information, see [DML statement conflicts](/bigquery/docs/data-manipulation-language#dml_statement_conflicts) .

To address this error, run DML operations that affect a single table such that they don't overlap.

## Correlated subqueries

Error string: `  Correlated subqueries that reference other tables are not supported unless they can be de-correlated  `

This error can occur when your query contains a subquery that references a column from outside that subquery, called a *correlation* column. The correlated subquery is evaluated using an inefficient, nested execution strategy, in which the subquery is evaluated for every row from the outer query that produces the correlation columns. Sometimes, BigQuery can internally rewrite queries with correlated subqueries so that they execute more efficiently. The correlated subqueries error occurs when BigQuery can't sufficiently optimize the query.

To address this error, try the following:

  - Remove any `  ORDER BY  ` , `  LIMIT  ` , `  EXISTS  ` , `  NOT EXISTS  ` , or `  IN  ` clauses from your subquery.
  - Use a [multi-statement query](/bigquery/docs/reference/standard-sql/procedural-language) to create a temporary table to reference in your subquery.
  - Rewrite your query to use a `  CROSS JOIN  ` instead.

## Insufficient column-level access control permissions

Error strings:

  - `  Access denied: Requires fineGrainedGet permission on the read columns to execute the DML statements  `
  - \`Access denied: User does not have permission to access policy tag projects/ PROJECT\_ID /locations/ LOCATION /taxonomies/ TAXONOMY\_ID /policyTags/ POLICY\_TAG\_ID on column PROJECT\_ID . DATASET . TABLE . COLUMN .'

These errors occur when you attempt to run a SQL query or a DML `  DELETE  ` , `  UPDATE  ` , or `  MERGE  ` statement without being granted the [Fine-Grained Reader](/bigquery/docs/column-level-security#fine_grained_reader) role on the columns that use column-level access control. This role is assigned to principals as part of configuring a policy tag. For more information, see [Impact on writes from column-level access control](/bigquery/docs/column-level-security-writes) .

To work around this issue, modify the query to exclude columns with policy tags, or grant the [Fine-Grained Reader](/bigquery/docs/column-level-security#fine_grained_reader) role to the user. This role is assigned to principals as part of configuring a policy tag. For more information, see [Update permissions on policy tags](/bigquery/docs/column-level-security#update_permission_policy_tags) .

## Troubleshoot scheduled queries

The following issues may arise during scheduled query configuration or execution.

### Scheduled query triggers duplicate runs

A scheduled query might be triggered more than once at the scheduled time. This behavior is more likely to occur for queries scheduled exactly on the hour (such as 09:00). This can lead to unexpected outcomes, such as duplicate data if the query performs `  INSERT  ` operations.

To minimize the risk of duplicate runs, schedule your queries at an off-the-hour time, such as a few minutes before or after the hour (for example, 08:58 or 09:03). For more information, see [Scheduling queries](/bigquery/docs/scheduling-queries) .

### Invalid credentials for scheduled queries

Error strings:

  - `  Error code: INVALID_USERID  `
  - `  Error code 5: Authentication failure: User Id not found  `
  - `  PERMISSION_DENIED: BigQuery: Permission denied while getting Drive credentials  `

This error can occur when a scheduled query fails due to having outdated credentials, especially when querying Google Drive data.

To address this error, follow these steps:

  - Ensure that you've enabled the [BigQuery Data Transfer Service](/bigquery/docs/enable-transfer-service#enable-dts) , which is a [prerequisite](/bigquery/docs/scheduling-queries#before_you_begin) for using scheduled queries.
  - Update the [scheduled query credentials](/bigquery/docs/scheduling-queries#update_scheduled_query_credentials) .

### Invalid service account credentials

Error string: `  HttpError 403 when requesting returned: The caller does not have permission  `

This error might appear when you attempt to set up a scheduled query with a service account. To resolve this error, see the troubleshooting steps in [Authorization and permission issues](/bigquery/docs/transfer-troubleshooting#authorization_and_permission_issues) .

## Invalid snapshot time

Error string: `  Invalid snapshot time  `

This error can occur when trying to query historical data that is outside of the [time travel window](/bigquery/docs/time-travel) for the dataset. To address this error, change the query to access historical data within the dataset's time travel window.

This error can also appear if one of the tables used in the query is dropped and re-created after the query starts. Check to see if there is a scheduled query or application that performs this operation that ran at the same time as the failed query. If there is, try moving the process that performs the drop and re-create operation to run at a time that doesn't conflict with queries that read that table.

## Job already exists

Error string: `  Already Exists: Job <job name>  `

This error can occur for query jobs that must evaluate large arrays, such that it takes longer than average to create a query job. For example, a query with a `  WHERE  ` clause like `  WHERE column IN (<2000+ elements array>)  ` .

To address this error, follow these steps:

  - Allow BigQuery to generate a random [`  jobId  ` value](/bigquery/docs/reference/rest/v2/JobReference) instead of specifying one.
  - Use a [parameterized query](/bigquery/docs/parameterized-queries#use_arrays_in_parameterized_queries) to load the array.

This error can also occur when you manually set a job ID but the job doesn't return success within a timeout period. In this case, you can add an exception handler to check if the job exists. If it does, then you can pull the query results from the job.

## Job not found

Error string: `  Job not found  `

This error can occur in response to a [`  getQueryResults  ` call](/bigquery/docs/reference/rest/v2/jobs/getQueryResults) , where no value is specified for the `  location  ` field. If that is the case, try the call again and provide a `  location  ` value.

For more information, see [Avoid multiple evaluations of the same Common Table Expressions (CTEs)](/bigquery/docs/best-practices-performance-compute#avoid_multiple_evaluations_of_the_same_ctes) .

## Location not found

Error string: `  Dataset [project_id]:[dataset_id] was not found in location [region]  `

This error returns when you refer to a dataset resource that doesn't exist, or when the location in the request does not match the location of the dataset.

To address this issue, specify the location of the dataset in the query or confirm that the dataset is available in the same location.

## Query exceeds execution time limit

Error string: `  Query fails due to reaching the execution time limit  `

If your query is hitting the [query execution time limit](/bigquery/quotas#query_jobs) , check the execution time of previous runs of the query by querying the [`  INFORMATION_SCHEMA.JOBS  ` view](/bigquery/docs/information-schema-jobs) with a query similar to the following example:

``` text
SELECT TIMESTAMP_DIFF(end_time, start_time, SECOND) AS runtime_in_seconds
FROM `region-us`.INFORMATION_SCHEMA.JOBS
WHERE statement_type = 'QUERY'
AND query = "my query string";
```

If previous runs of the query have taken significantly less time, use [query performance insights](/bigquery/docs/query-insights) to determine and address the underlying issue.

## Query response is too large

Error string: `  responseTooLarge  `

This error occurs when your query's results are larger than the [maximum response size](/bigquery/quota-policy#query_jobs) .

To address this error, follow the guidance provided for the `  responseTooLarge  ` error message in the [error table](/bigquery/docs/error-messages#errortable) .

## Reservation not found or is missing slots

Error string: `  Cannot run query: project does not have the reservation in the data region or no slots are configured  `

This error occurs when the reservation assigned to the project in the query's region has zero slots assigned. You can either add slots to the reservation, allow the reservation to use idle slots, use a different reservation, or remove the assignment and run the query on-demand.

## Table not found

Error string: `  Not found: Table [project_id]:[dataset].[table_name] was not found in location [region]  `

This error occurs when a table in your query can't be found in the dataset or region that you specified. To address this error, do the following:

  - Check that your query contains the correct project, dataset, and table name.
  - Check that the table exists in the region in which you ran the query.
  - Make sure that the table wasn't dropped and recreated during the execution of the job. Otherwise, incomplete metadata propagation can cause this error.

## Too many DML statements

Error string: `  Too many DML statements outstanding against <table-name>, limit is 20  `

This error occurs when you exceed the [limit of 20 DML statements](/bigquery/quotas#data-manipulation-language-statements) in `  PENDING  ` status in a queue for a single table. This error usually occurs when you submit DML jobs against a single table faster than what BigQuery can process.

One possible solution is to group multiple smaller DML operations into larger but fewer jobs—for example, by batching updates and inserts. When you group smaller jobs into larger ones, the cost to run the larger jobs is amortized and the execution is faster. Consolidating DML statements that affect the same data generally improves the efficiency of DML jobs, and is less likely to exceed the queue size quota limit. For more information about optimizing your DML operations, see [Avoid DML statements that update or insert single rows](/bigquery/docs/best-practices-performance-compute#avoid-dml-update-single-rows) .

Other solutions to improve your DML efficiency could be to partition or cluster your tables. For more information, see [Best practices](/bigquery/docs/data-manipulation-language#best_practices) .

## Transaction aborted due to concurrent update

Error string: `  Transaction is aborted due to concurrent update against table [table_name]  `

This error can occur when two different mutating DML statements attempt to concurrently update the same table. For example, suppose you start a [transaction](/bigquery/docs/transactions) in a session that contains a mutating DML statement followed by an error. If there is no exception handler, then BigQuery automatically rolls back the transaction when the session ends, which takes up to 24 hours. During this time, other attempts to run a mutating DML statement on the table fail.

To address this error, [list your active sessions](/bigquery/docs/sessions#list-sessions) and check whether any of them contains a query job with status `  ERROR  ` that ran a mutating DML statement on the table. Then, terminate that session.

## Error 412: The job references a table that belongs to a failover dataset

Error string: `  Error 412: The job references a table that belongs to a failover dataset in the ... region (PROJECT_ID:DATASET_ID). However, only jobs that run on a reservation with the "ENTERPRISE_PLUS" edition can modify or write to failover datasets. Please also make sure that the job that is writing to the failover dataset is running in the current primary location.  `

This means that either the job wasn't run under a BigQuery Enterprise Plus edition, or the job ran in a region other than the primary location of the failover dataset. See [managed disaster recovery](/bigquery/docs/managed-disaster-recovery) for more details.

## User does not have permission

Error strings:

  - `  Access Denied: Project [project_id]: User does not have bigquery.jobs.create permission in project [project_id].  `
  - `  User does not have permission to query table project-id:dataset.table.  `
  - `  Access Denied: User does not have permission to query table or perhaps it does not exist.  `

These errors can occur when you run a query without the `  bigquery.jobs.create  ` permission on the project from which you are running the query, regardless of your permissions on the project that contains the data.

You may also receive these errors if your service account, user, or group doesn't have the `  bigquery.tables.getData  ` permission on all tables and views that your query references. For more information about the permissions required for running a query, see [Required roles](/bigquery/docs/running-queries#required_permissions) .

These errors can also occur if the table does not exist in the queried region, such as `  asia-south1  ` . You can verify the region by examining the [dataset location](/bigquery/docs/datasets-intro#dataset_location) .

When addressing these errors, consider the following:

  - *Service accounts* : Service accounts must have the `  bigquery.jobs.create  ` permission on the project from which they run, and they must have `  bigquery.tables.getData  ` permission on all tables and views that are referenced by the query.

  - *Custom roles* : Custom IAM roles must have the `  bigquery.jobs.create  ` permission explicitly included in the relevant role, and they must have `  bigquery.tables.getData  ` permission on all tables and views that are referenced by the query.

  - *Shared datasets* : When working with shared datasets in a separate project, you might still need the `  bigquery.jobs.create  ` permission in the project to run queries or jobs in that dataset.

To give permission to access a table or view, see [Grant access to a table or view](/bigquery/docs/control-access-to-resources-iam#grant_access_to_a_table_or_view) .

**Note:** If the user account or service account is impacted by a deny policy, you may receive an `  Access denied  ` error even if the account has the correct permissions. For more information, see [Deny policies](/iam/docs/deny-overview) .

### Permission `     bigquery.reservations.use    ` denied on reservation

Error string:

  - `  Access Denied: Reservation projects/project/locations/region/reservations/reservation_name: Permission bigquery.reservations.use denied on reservation projects/project/locations/region/reservations/reservation_name (or it may not exist)  `

This error occurs when a query is assigned to run in a specific reservation using the `  SET @@reservation  ` statement and the user or service account is missing the `  bigquery.reservations.use  ` permission. You can inspect the failure in Cloud Logging or the BigQuery jobs page to identify which principal tried to perform this operation.

### Other `     Access Denied    ` errors

Error strings:

  - `  Access Denied: Dataset project_id:dataset_id: Permission bigquery.datasets.get denied on dataset project_id:dataset_id (or it may not exist).  `
  - `  Access Denied: Dataset project_id:dataset_id: Permission bigquery.datasets.update denied on dataset project_id:dataset_id (or it may not exist).  `
  - `  Access Denied: BigQuery BigQuery: User does not have permission to access data protected by policy tag  `

To troubleshoot general `  Access Denied  ` errors in BigQuery, use [Policy Analyzer](/policy-intelligence/docs/analyze-iam-policies) to [determine what access a principal has on a resource](/policy-intelligence/docs/analyze-iam-policies#access-query) .

In Policy Analyzer, provide the BigQuery resource that you're trying to access (for example, `  //bigquery.googleapis.com/projects/YOUR_PROJECT/datasets/YOUR_DATASET/tables/YOUR_TABLE  ` ) and the email of the user or service account that's getting the `  Access Denied  ` error as the principal. The analysis shows the principal permissions on the resource, which you can compare with the missing permissions in the error message.

## Destination encryption not supported for scripts

Error string: `  configuration.query.destinationEncryptionConfiguration cannot be set for scripts  `

This error occurs when attempting to set the destination encryption configuration for a BigQuery script job, which is [not supported](/bigquery/docs/customer-managed-encryption#script-limitations) .

## Access denied by organization policy

Error string: `  IAM setPolicy failed for Dataset DATASET : Operation denied by org policy on resource.  `

This error occurs when an organizational policy prevents the principal from querying a BigQuery resource. The [Organization Policy Service](/resource-manager/docs/organization-policy/overview) lets you enforce constraints on [supported resources](/resource-manager/docs/organization-policy/org-policy-constraints) across your organization hierarchy.

If the principal should have access to the resource, you'll need to use the available [VPC troubleshooting tools](/vpc/docs/troubleshooting-policy-and-access-problems#troubleshooting_tools) to diagnose the issue with your organization policy.

## Resources exceeded issues

The following issues result when BigQuery has insufficient resources to complete your query.

### Query exceeds CPU resources

Error string: `  Query exceeded resource limits  `

This error occurs when on-demand queries use too much CPU relative to the amount of data scanned. For information on how to resolve these issues, see [Troubleshoot resources exceeded issues](#ts-resources-exceeded) .

### Query exceeds memory resources

Error string: `  Resources exceeded during query execution: The query could not be executed in the allotted memory  `

For [`  SELECT  ` statements](/bigquery/docs/reference/standard-sql/query-syntax#select_list) , this error occurs when the query uses too many resources. To address this error, see [Troubleshoot resources exceeded issues](#ts-resources-exceeded) .

### Out of stack space

Error string: `  Out of stack space due to deeply nested query expression during query resolution.  `

This error can occur when a query contains too many nested function calls. Sometimes, parts of a query are translated to function calls during parsing. For example, an expression with repeated [concatenation operators](/bigquery/docs/reference/standard-sql/operators#concatenation_operator) , such as `  A || B || C || ...  ` , becomes `  CONCAT(A, CONCAT(B, CONCAT(C, ...)))  ` .

To address this error, rewrite your query to reduce the amount of nesting.

### Resources exceeded during query execution

Error string: `  Resources exceeded during query execution: The query could not be executed in the allotted memory. Peak usage: [percentage]% of limit. Top memory consumer(s): ORDER BY operations.  `

This can happen with `  ORDER BY ... LIMIT ... OFFSET ...  ` queries. Due to implementation details, the sorting might occur on a single compute unit, which can run out of memory if it needs to process too many rows before the `  LIMIT  ` and `  OFFSET  ` are applied, particularly with a large `  OFFSET  ` .

To address this error, avoid large `  OFFSET  ` values in `  ORDER BY  ` ... `  LIMIT  ` queries. Alternatively, use the scalable `  ROW_NUMBER()  ` window function to assign ranks based on the chosen order, and then filter these ranks in a `  WHERE  ` clause. For example:

``` text
SELECT ...
FROM (
  SELECT ROW_NUMBER() OVER (ORDER BY ...) AS rn
  FROM ...
)
WHERE rn > @start_index AND rn <= @page_size + @start_index  -- note that row_number() starts with 1
```

### Query exceeds shuffle resources

Error string: `  Resources exceeded during query execution: Your project or organization exceeded the maximum disk and memory limit available for shuffle operations  `

This error occurs when a query can't access sufficient shuffle resources.

To address this error, provision more slots or reduce the amount of data processed by the query. For more information about ways to do this, see [Insufficient shuffle quota](/bigquery/docs/query-insights#insufficient_shuffle_quota) .

For additional information on how to resolve these issues, see [Troubleshoot resources exceeded issues](#ts-resources-exceeded) .

### Query is too complex

Error string: `  Resources exceeded during query execution: Not enough resources for query planning - too many subqueries or query is too complex  `

This error occurs when a query is too complex. The primary causes of complexity are:

  - `  WITH  ` clauses that are deeply nested or used repeatedly.
  - Views that are deeply nested or used repeatedly.
  - Repeated use of the [`  UNION ALL  ` operator](/bigquery/docs/reference/standard-sql/query-syntax#union_example) .

To address this error, try the following options:

  - Split the query into multiple queries, then use [procedural language](/bigquery/docs/reference/standard-sql/procedural-language) to run those queries in a sequence with shared state.
  - Use temporary tables instead of `  WITH  ` clauses.
  - Rewrite your query to reduce the number of referenced objects and comparisons.

You can proactively monitor queries that are approaching the complexity limit by using the `  query_info.resource_warning  ` field in the [`  INFORMATION_SCHEMA.JOBS  ` view](/bigquery/docs/information-schema-jobs) . The following example returns queries with high resource usage for the last three days:

``` text
SELECT
  ANY_VALUE(query) AS query,
  MAX(query_info.resource_warning) AS resource_warning
FROM
  <your_project_id>.`region-us`.INFORMATION_SCHEMA.JOBS
WHERE
  creation_time > TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 3 DAY)
  AND query_info.resource_warning IS NOT NULL
GROUP BY
  query_info.query_hashes.normalized_literals
LIMIT
  1000
```

For additional information on how to resolve these issues, see [Troubleshoot resources exceeded issues](#ts-resources-exceeded) .

### Troubleshoot resources exceeded issues

**For query jobs** :

To optimize your queries, try the following steps:

  - Try removing an `  ORDER BY  ` clause.
  - If your query uses `  JOIN  ` , ensure that the larger table is on the left side of the clause. Also ensure that your data does not contain duplicate join keys.
  - If your query uses `  FLATTEN  ` , determine if it's necessary for your use case. For more information, see [nested and repeated data](/bigquery/docs/data#nested) .
  - If your query uses `  EXACT_COUNT_DISTINCT  ` , consider using [`  COUNT(DISTINCT)  `](/bigquery/query-reference#countdistinct) instead.
  - If your query uses `  COUNT(DISTINCT <value>, <n>)  ` with a large `  <n>  ` value, consider using `  GROUP BY  ` instead. For more information, see [`  COUNT(DISTINCT)  `](/bigquery/query-reference#countdistinct) .
  - If your query uses `  UNIQUE  ` , consider using `  GROUP BY  ` instead, or a [window function](/bigquery/query-reference#windowfunctions) inside of a subselect.
  - If your query materializes many rows using a `  LIMIT  ` clause, consider filtering on another column, for example `  ROW_NUMBER()  ` , or removing the `  LIMIT  ` clause altogether to allow write parallelization.
  - If your query used deeply nested views and a `  WITH  ` clause, this can cause an exponential growth in complexity, thereby reaching the limits.
  - Use temporary tables instead of `  WITH  ` clauses. A `  WITH  ` clause might have to be recalculated several times, which can make the query complex and therefore slow. Persisting intermediate results in temporary tables instead reduces complexity.
  - Avoid using `  UNION ALL  ` queries.
  - If your query uses `  MATCH_RECOGNIZE  ` , modify the [`  PARTITION BY  ` clause](/bigquery/docs/reference/standard-sql/query-syntax#match_recognize_partition_by) to reduce the size of the partitions, or add a `  PARTITION BY  ` clause if one doesn't exist.

For more information, see the following resources:

  - [Optimize query computation](/bigquery/docs/best-practices-performance-compute) .
  - [Get more details about the resource warning](/bigquery/docs/information-schema-jobs#get_details_about_a_resource_warning)
  - [Monitor health, resource utilization, and jobs](/bigquery/docs/admin-resource-charts)

**For load jobs** :

If you are loading Avro or Parquet files, reduce the row size in the files. Check for specific size restrictions for the file format that you are loading:

  - [Avro input file requirements](/bigquery/docs/loading-data-cloud-storage-avro#input_file_requirements)
  - [Parquet input file requirements](/bigquery/docs/loading-data-cloud-storage-parquet#input_file_requirements)

If you get this error when loading ORC files, [contact Support](/support) .

**For Storage API:**

Error string: `  Stream memory usage exceeded  `

During a Storage Read API `  ReadRows  ` call, some streams with high memory usage might get a `  RESOURCE_EXHAUSTED  ` error with this message. This can happen when reading from wide tables or tables with a complex schema. As a resolution, reduce the result row size by selecting fewer columns to read (using the [`  selected_fields  ` parameter](/bigquery/docs/reference/storage/rpc/google.cloud.bigquery.storage.v1#tablereadoptions) ), or by simplifying the table schema.

## Troubleshoot connectivity problems

The following sections describe how to troubleshoot connectivity issues when trying to interact with BigQuery:

### Allowlist Google DNS

Use the [Google IP Dig tool](https://toolbox.googleapps.com/apps/dig/#A/) to resolve the BigQuery DNS endpoint `  bigquery.googleapis.com  ` to a single 'A' record IP. Make sure this IP is not blocked in your firewall settings.

In general we recommend allowlisting Google DNS names. The IP ranges shared in the <https://www.gstatic.com/ipranges/goog.json> and <https://www.gstatic.com/ipranges/cloud.json> files change often; therefore, we recommended allowlisting Google DNS names instead. Here is a list of common DNS names we recommend to add to the allowlist:

  - `  *.1e100.net  `
  - `  *.google.com  `
  - `  *.gstatic.com  `
  - `  *.googleapis.com  `
  - `  *.googleusercontent.com  `
  - `  *.appspot.com  `
  - `  *.gvt1.com  `

### Identify the proxy or firewall dropping packets

To identify all packet hops between the client and the Google Front End (GFE) run a [`  traceroute  `](https://en.wikipedia.org/wiki/Traceroute) command on your client machine that could highlight the server that is dropping packets directed towards the GFE. Here is a sample `  traceroute  ` command:

``` text
traceroute -T -p 443 bigquery.googleapis.com
```

It is also possible to identify packet hops for specific GFE IP addresses if the problem is related to a particular IP address:

``` text
traceroute -T -p 443 142.250.178.138
```

If there's a Google-side timeout issue, you'll see the request make it all the way to the GFE.

If you see that the packets never reach the GFE, reach out to your network administrator to resolve this problem.

### Generate a PCAP file and analyze your firewall or proxy

Generate a packet capture file (PCAP) and analyze the file to make sure the firewall or proxy is not filtering out packets to Google IPs and is allowing packets to reach the GFE.

Here is a sample command that can be run with the [`  tcpdump  `](https://www.tcpdump.org/) tool:

``` text
tcpdump -s 0 -w debug.pcap -K -n host bigquery.googleapis.com
```

### Set up retries for intermittent connectivity problems

There are situations in which GFE load balancers might drop connections from a client IP - for example, if it detects DDoS traffic patterns, or if the load balancer instance is being scaled down which may result in the endpoint IP being recycled. If the GFE load balancers drop the connection, the client needs to catch the timed-out request and retry the request to the DNS endpoint. Ensure that you don't use the same IP address until the request eventually succeeds, because the IP address may have changed.

If you've identified an issue with consistent Google-side timeouts where retries don't help, [contact Cloud Customer Care](/support) and make sure to include a fresh PCAP file generated by running a packet capturing tool like [tcpdump](https://www.tcpdump.org/) .

## What's next

  - [Get query performance insights](/bigquery/docs/query-insights) .
  - Learn more about [optimizing queries for performance](/bigquery/docs/best-practices-performance-overview) .
  - Review [quotas and limits](/bigquery/quotas#query_jobs) for queries.
  - Learn more about other [BigQuery error messages](/bigquery/docs/error-messages) .
