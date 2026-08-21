---
name: documents/docs.cloud.google.com/bigquery/docs/troubleshoot-intro
uri: https://docs.cloud.google.com/bigquery/docs/troubleshoot-intro
title: Introduction to troubleshooting
description: An overview of the diagnostic tools, telemetry views, and resources available to troubleshoot BigQuery.
data_source: docs.cloud.google.com
---

# Introduction to troubleshooting

This document provides an overview of the diagnostic tools, telemetry interfaces, and documentation resources available to help you troubleshoot issues in BigQuery.

When you encounter query failures, performance bottlenecks, permission errors, quota limits, or data ingestion issues, BigQuery provides built-in tools to help you identify root causes and resolve issues quickly.

## Troubleshooting workflow

To troubleshoot an issue in BigQuery effectively, consider the following diagnostic criteria:

1.  **Identify the symptom and failure mode.** Review your task's results to determine whether the issue is a hard failure (such as an error code or job failure), a performance degradation (such as a slow query or slot starvation), a permission denial, or an unexpected cost discrepancy.
2.  **Inspect job execution details.** Use the Google Cloud console [jobs explorer](https://docs.cloud.google.com/bigquery/docs/admin-jobs-explorer#get-job-details) , the [query execution graph](https://docs.cloud.google.com/bigquery/docs/query-insights) , or [command-line tools](https://docs.cloud.google.com/bigquery/docs/troubleshoot-intro#command-line_and_automated_diagnostic_tools) to examine stage-level timings, slot allocation, and error details. You can also ask [Gemini Cloud Assist](https://docs.cloud.google.com/bigquery/docs/use-cloud-assist) to investigate your issue.
3.  **Analyze telemetry and metadata.** Query [information schema views](https://docs.cloud.google.com/bigquery/docs/information-schema-intro) or inspect Cloud Audit Logs to correlate job behavior with resource contention, reservation limits, or administrative changes.
4.  **Apply targeted mitigations.** Use [category-specific troubleshooting guides](https://docs.cloud.google.com/bigquery/docs/troubleshoot-intro#troubleshoot_by_issue_category) or defensive SQL functions to remediate the underlying cause.

## Distinguish troubleshooting from optimization

When you work with BigQuery, it's important to distinguish between troubleshooting, performance optimization, and best practices:

  - **Troubleshooting.** Focuses on diagnosing and resolving unexpected failures, runtime errors, broken pipelines, quota exhaustion, or unintended behavior that prevents jobs from completing successfully.
  - **Performance optimization.** Focuses on improving the execution speed, latency, or resource efficiency of queries and workloads that are already running successfully. For more information, see [Optimize query performance](https://docs.cloud.google.com/bigquery/docs/best-practices-performance-overview) .
  - **Best practices.** Focuses on architectural and design patterns for data modeling, storage, security, and cost management. For more information, see [Introduction to best practices](https://docs.cloud.google.com/bigquery/docs/best-practices) .

## Diagnostic tools

The following sections describe several BigQuery interfaces and automated tools to help you diagnose issues across your workloads.

### Visual and console tools

The following tools help you troubleshoot BigQuery from Google Cloud console.

  - **Jobs Explorer.** Search, filter, and inspect past and running jobs across projects or organizations without writing SQL queries. You can view error messages, slot usage, execution timelines, and job metadata. For more information, see [Monitor jobs in Jobs Explorer](https://docs.cloud.google.com/bigquery/docs/admin-jobs-explorer) .
  - **Query execution graph.** Inspect the visual stage-by-stage execution plan for a query. The execution graph helps you identify bottlenecks such as shuffle spills to disk, compute-bound stages, data skew, or input/output delays. For more information, see [Troubleshoot query performance with the query execution graph](https://docs.cloud.google.com/bigquery/docs/troubleshoot-queries#query_execution_graph) .
  - **Query Insights and resource charts.** View real-time and historical graphs of slot utilization, job concurrency, and reservation allocations to diagnose capacity constraints. For more information, see [Use administrative resource charts](https://docs.cloud.google.com/bigquery/docs/admin-resource-charts) .
  - **Gemini Cloud Assist in BigQuery.** Get contextual, AI-assisted analysis of failed queries and performance bottlenecks. Gemini Cloud Assist explains error codes, highlights problematic SQL syntax, and suggests remediation steps directly in the Google Cloud console. For more information, see [Troubleshoot queries using Gemini Cloud Assist](https://docs.cloud.google.com/bigquery/docs/troubleshoot-queries#cloud-assist) .

### Command-line and automated diagnostic tools

The following tools can help you diagnose BigQuery issues from a command-line interface.

  - **bq command-line tool.** Inspect detailed error structures, request IDs, and job metadata by using the `bq show -j <var>JOB_ID</var>` command or by adding the `--format=prettyjson` flag to query commands. For more information, see [Troubleshooting CLI commands](https://docs.cloud.google.com/bigquery/docs/reference/bq-cli-reference#troubleshooting-bq) .
  - **`gcpdiag` tool.** Run automated diagnostics from the command line to detect common Google Cloud configuration issues, including IAM permission gaps, network restrictions, and service account errors. For more information, see [Troubleshoot query failure using `gcpdiag`](https://docs.cloud.google.com/bigquery/docs/troubleshoot-queries#failed-query-gcpdiag) .

### Metadata and telemetry views

Information schema views let you query real-time and historical metadata about jobs, capacity, streaming ingestion, and datasets using standard SQL. These views include the following:

  - **Job execution telemetry.** Query [`INFORMATION_SCHEMA.JOBS`](https://docs.cloud.google.com/bigquery/docs/information-schema-jobs) and [`INFORMATION_SCHEMA.JOBS_TIMELINE`](https://docs.cloud.google.com/bigquery/docs/information-schema-jobs-timeline) to analyze slot-millisecond consumption, spilled bytes, queue times, and error codes across jobs.
  - **Reservations and capacity.** Query [`INFORMATION_SCHEMA.RESERVATIONS`](https://docs.cloud.google.com/bigquery/docs/information-schema-reservations) and [`INFORMATION_SCHEMA.CAPACITY_COMMITMENTS`](https://docs.cloud.google.com/bigquery/docs/information-schema-capacity-commitments) to diagnose slot allocation, reservation limits, and autoscaling behaviors.
  - **Streaming and ingestion.** Query [`INFORMATION_SCHEMA.STREAMING_TIMELINE`](https://docs.cloud.google.com/bigquery/docs/information-schema-streaming-timeline) to identify ingestion latency and streaming rate limits.
  - **Storage and partition health.** Query [`INFORMATION_SCHEMA.TABLE_STORAGE`](https://docs.cloud.google.com/bigquery/docs/information-schema-table-storage) to inspect physical table sizes, active versus long-term storage, and partition distribution.

For more information, see [Introduction to BigQuery `INFORMATION_SCHEMA`](https://docs.cloud.google.com/bigquery/docs/information-schema-intro) .

### Cloud Monitoring and Cloud Audit Logs

  - **Cloud Audit Logs.** Review Admin Activity and Data Access audit logs to trace who initiated specific operations, inspect caller identities, and diagnose `PERMISSION_DENIED` errors. For more information, see [BigQuery audit logging reference](https://docs.cloud.google.com/bigquery/docs/reference/auditlogs) .
  - **Cloud Monitoring.** Track metrics such as slot usage, query execution durations, and uploaded bytes, and configure alert policies to notify your team when thresholds or quotas are exceeded. For more information, see [Monitor BigQuery using Cloud Monitoring](https://docs.cloud.google.com/bigquery/docs/monitoring) .

### Defensive SQL functions and debugging statements

To prevent queries from failing unexpectedly due to runtime data errors, use the following:

  - **Safe expressions.** Use `SAFE_CAST()` , `SAFE_DIVIDE()` , `SAFE_OFFSET()` , and `SAFE_ORDINAL()` to return `NULL` instead of generating runtime errors when data types or array bounds don't match. Most scalar functions support the `SAFE.` prefix. For more information, see [Debugging functions](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/debugging_functions) and [`SAFE.` prefix](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/functions-reference#safe_prefix) .
  - **SQL assertions.** Use the `ASSERT` statement in multi-statement transactions or scripts to enforce data validation conditions and fail with custom error messages before downstream operations execute. For more information, see [Debugging statements](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/debugging-statements) .

## Troubleshoot by issue category

Select a category from the following sections to view detailed error codes, root causes, and step-by-step resolution guides.

### Query performance and execution

Diagnose queries that fail to run, time out, encounter resource constraints, or experience unexpected delays.

  - **[Troubleshoot query issues](https://docs.cloud.google.com/bigquery/docs/troubleshoot-queries) .** Resolve `resourcesExceeded` errors, slow query execution, shuffle spill, out-of-memory conditions, and scheduled query failures.
  - **[Troubleshoot long query queue times](https://docs.cloud.google.com/bigquery/docs/query-queues#troubleshooting_long_queue_times) .** Diagnose concurrency bottlenecks and queries queued due to interactive or batch queue limits.
  - **[Error messages reference](https://docs.cloud.google.com/bigquery/docs/error-messages) .** Look up specific HTTP error codes, error reason strings, and recommended actions.

### Identity and Access Management (IAM) and security

Diagnose access control failures, missing role assignments, and data governance policy blocks.

  - **[Troubleshoot IAM permissions in BigQuery](https://docs.cloud.google.com/bigquery/docs/troubleshoot-access-control) .** Diagnose permission denied errors, grant missing IAM roles, and use Policy Troubleshooter.
  - **[Troubleshoot VPC Service Controls](https://docs.cloud.google.com/vpc-service-controls/docs/troubleshooting) .** Identify and resolve perimeter violations and ingress or egress rule blocks.
  - **[Troubleshoot row-level and column-level security](https://docs.cloud.google.com/bigquery/docs/column-level-security#troubleshoot) .** Resolve access issues related to data policies, policy tags, and row-access filters.

### Quotas, rate limits, and reservations

Resolve issues when workloads exceed BigQuery service limits or capacity allocations.

  - **[Troubleshoot quota and limit errors](https://docs.cloud.google.com/bigquery/docs/troubleshoot-quotas) .** Identify adjustable versus non-adjustable quotas, handle concurrent query limits, and resolve API rate-limit errors.
  - **[Troubleshoot issues with reservations](https://docs.cloud.google.com/bigquery/docs/reservations-workload-management#troubleshoot_issues_with_reservations) .** Diagnose slot starvation, reservation assignment mismatches, and baseline capacity shortfalls.

### Data ingestion, streaming, and transfers

Diagnose failures when loading data, streaming records, or syncing external sources.

  - **[Troubleshoot transfer configurations](https://docs.cloud.google.com/bigquery/docs/transfer-troubleshooting) .** Resolve BigQuery Data Transfer Service errors across sources like Amazon S3, Salesforce, Google Ads, and Cloud Storage.
  - **[Troubleshoot streaming inserts](https://docs.cloud.google.com/bigquery/docs/streaming-data-into-bigquery#troubleshooting) .** Debug Storage Write API and legacy streaming ingestion failures, row-level insertion errors, and throughput quotas.
  - **[Troubleshoot data loading](https://docs.cloud.google.com/bigquery/docs/loading-data-cloud-storage-csv#troubleshoot_parsing_errors) .** Resolve CSV, JSON, Parquet, or Avro schema parsing and delimiter errors.

### External data sources and federated queries

Diagnose connectivity, authentication, and execution errors when querying data outside BigQuery.

  - **[Troubleshoot Cloud SQL federated queries](https://docs.cloud.google.com/bigquery/docs/cloud-sql-federated-queries#troubleshooting) .** Resolve connection timeouts, instance configuration issues, and credential failures.
  - **[Troubleshoot BigLake tables](https://docs.cloud.google.com/bigquery/docs/biglake-intro#troubleshooting) .** Diagnose Cloud Storage access permissions, external delegation errors, and metadata sync issues with open table formats.

### Billing and cost discrepancies

Investigate unexpected charges and billing discrepancies across compute and storage.

  - **[Troubleshoot BigQuery cost discrepancies](https://docs.cloud.google.com/bigquery/docs/best-practices-costs#troubleshooting-bigquery-cost-discrepancies-and-unexpected-charges) .** Identify the origin of unexpected charges, analyze on-demand bytes billed, and verify capacity commitment usage.

### Data loss mitigation

To recover historical data that was changed or deleted, or to maintain business continuity during a regional outage, use the following disaster recovery and data retention tools:

  - **Restore data.** Query or restore table data that was changed or deleted within your time travel window. For more information, see [Restore data](https://docs.cloud.google.com/bigquery/docs/access-historical-data) .
  - **Time travel.** Retain updated or deleted data in a dataset for a configured retention period to help protect against accidental modifications. For more information, see [Time travel](https://docs.cloud.google.com/bigquery/docs/time-travel) .
  - **Regional failover.** Promote a secondary replica to the primary role during a regional outage when using BigQuery-managed disaster recovery. For more information, see [Regional failover](https://docs.cloud.google.com/bigquery/docs/managed-disaster-recovery#initiate_a_failover) .

### Using APIs

When you interact with BigQuery programmatically, use the following resources to optimize request latency and manage upload workflows:

  - **API performance tips.** Follow best practices for making API calls, such as managing connection pools, using batch operations, and handling retries. For more information, see [API performance tips](https://docs.cloud.google.com/bigquery/docs/api-performance) .
  - **API uploads.** Troubleshoot and manage data ingestion using REST API resumable and multipart upload requests. For more information, see [API uploads](https://docs.cloud.google.com/bigquery/docs/reference/api-uploads) .

## What's next

  - Learn more about [monitoring BigQuery](https://docs.cloud.google.com/bigquery/docs/monitoring) .
  - Explore the [BigQuery `INFORMATION_SCHEMA` reference](https://docs.cloud.google.com/bigquery/docs/information-schema-intro) .
  - Contact [Cloud Customer Care](https://cloud.google.com/support) for support with persistent or critical production issues.
