---
name: documents/docs.cloud.google.com/bigquery/docs/info-schema-troubleshoot
uri: https://docs.cloud.google.com/bigquery/docs/info-schema-troubleshoot
title: Troubleshoot with information schema
description: Learn the principles of troubleshooting BigQuery using INFORMATION_SCHEMA views, explore how to use metadata views, and navigate relevant documentation in the BigQuery library.
data_source: docs.cloud.google.com
---

# Troubleshoot with information schema

As a BigQuery administrator or data analyst, managing enterprise workloads requires a reliable, scalable way to diagnose performance bottlenecks, query failures, capacity limits, and storage growth. BigQuery information schema views serve as an observability foundation, providing near real-time and historical metadata accessible through standard GoogleSQL queries.

This document outlines the core principles of troubleshooting BigQuery using information schema, provides a structured overview of the administrative troubleshooting toolbox, and directs you to specific views in the BigQuery library.

## Information schema troubleshooting by task

The following table summarizes useful information schema views categorized by task and diagnostic use case:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Task</th>
<th>Use cases</th>
<th>Information schema views</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Query performance and errors</strong></td>
<td><ul>
<li>Identify top slot-consuming and expensive queries.</li>
<li>Aggregate job error reasons and failure patterns.</li>
<li>Analyze per-stage execution times and spilled bytes.</li>
</ul></td>
<td><ul>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-jobs"><code dir="ltr" translate="no">JOBS_BY_PROJECT</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-jobs-by-organization"><code dir="ltr" translate="no">JOBS_BY_ORGANIZATION</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-jobs-by-folder"><code dir="ltr" translate="no">JOBS_BY_FOLDER</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-jobs-by-user"><code dir="ltr" translate="no">JOBS_BY_USER</code></a></li>
</ul></td>
</tr>
<tr class="even">
<td><strong>Workload capacity and contention</strong></td>
<td><ul>
<li>Detect slot contention, throttling, and queue times.</li>
<li>Monitor in-memory shuffle memory saturation.</li>
<li>Audit reservation baseline and autoscaling slot usage.</li>
<li>Verify project and folder reservation assignments.</li>
</ul></td>
<td><ul>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-jobs-timeline"><code dir="ltr" translate="no">JOBS_TIMELINE_BY_*</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-reservation-timeline"><code dir="ltr" translate="no">RESERVATIONS_TIMELINE_BY_*</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-reservations"><code dir="ltr" translate="no">RESERVATIONS_BY_*</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-assignments"><code dir="ltr" translate="no">ASSIGNMENTS_BY_*</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-capacity-commitments"><code dir="ltr" translate="no">CAPACITY_COMMITMENTS_BY_*</code></a></li>
</ul></td>
</tr>
<tr class="odd">
<td><strong>Storage costs and data architecture</strong></td>
<td><ul>
<li>Identify tables with runaway physical or logical storage.</li>
<li>Detect time-travel and fail-safe storage bloat.</li>
<li>Diagnose partition skew and tables nearing partition limits.</li>
<li>Discover expired or deleted tables in time-travel windows.</li>
</ul></td>
<td><ul>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-table-storage"><code dir="ltr" translate="no">TABLE_STORAGE_BY_*</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-partitions"><code dir="ltr" translate="no">PARTITIONS</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-tables"><code dir="ltr" translate="no">TABLES</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-table-options"><code dir="ltr" translate="no">TABLE_OPTIONS</code></a></li>
</ul></td>
</tr>
<tr class="even">
<td><strong>Access control and governance</strong></td>
<td><ul>
<li>Audit explicit Identity and Access Management (IAM) role grants on tables and datasets.</li>
<li>Troubleshoot access denied errors for users and service accounts.</li>
<li>Track cross-project dataset sharing and analytical usage.</li>
</ul></td>
<td><ul>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-object-privileges"><code dir="ltr" translate="no">OBJECT_PRIVILEGES</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-shared-dataset-usage"><code dir="ltr" translate="no">SHARED_DATASET_USAGE</code></a></li>
</ul></td>
</tr>
<tr class="odd">
<td><strong>Data ingestion pipelines</strong></td>
<td><ul>
<li>Monitor Storage Write API ingestion throughput and errors.</li>
<li>Diagnose streaming insert latency and rate limits.</li>
<li>Identify failing streams by stream type and error code.</li>
</ul></td>
<td><ul>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-write-api"><code dir="ltr" translate="no">WRITE_API_TIMELINE_BY_*</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-streaming"><code dir="ltr" translate="no">STREAMING_TIMELINE_BY_*</code></a></li>
</ul></td>
</tr>
<tr class="even">
<td><strong>Machine learning and vector search</strong></td>
<td><ul>
<li>Track model training duration and resource consumption.</li>
<li>Audit vector index build status and coverage percentage.</li>
<li>Troubleshoot stored procedure and Python UDF builds.</li>
</ul></td>
<td><ul>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-vector-indexes"><code dir="ltr" translate="no">VECTOR_INDEXES</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-routines"><code dir="ltr" translate="no">ROUTINES</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-jobs"><code dir="ltr" translate="no">JOBS_BY_*</code></a> (filter on ML statement types)</li>
</ul></td>
</tr>
<tr class="odd">
<td><strong>Workload optimization insights</strong></td>
<td><ul>
<li>Review automated partitioning and clustering recommendations.</li>
<li>Identify materialized view candidate tables.</li>
</ul></td>
<td><ul>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-recommendations"><code dir="ltr" translate="no">RECOMMENDATIONS_BY_*</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-insights"><code dir="ltr" translate="no">INSIGHTS_BY_*</code></a></li>
</ul></td>
</tr>
</tbody>
</table>

## Principles of troubleshooting with information schema

When you diagnose workload or environment issues in BigQuery, apply the following core principles:

  - **Scope by region, dataset, and project.** BigQuery workload management and compute resources execute within regional boundaries. Consider the following:
    
      - Always specify the correct regional qualifier (for example, `region- REGION .INFORMATION_SCHEMA.JOBS_BY_PROJECT` ) or dataset qualifier.
    
      - Choose the appropriate hierarchy level ( [`BY_PROJECT`](https://docs.cloud.google.com/bigquery/docs/information-schema-jobs) , [`BY_USER`](https://docs.cloud.google.com/bigquery/docs/information-schema-jobs-by-user) , [`BY_FOLDER`](https://docs.cloud.google.com/bigquery/docs/information-schema-jobs-by-folder) , or [`BY_ORGANIZATION`](https://docs.cloud.google.com/bigquery/docs/information-schema-jobs-by-organization) ) based on whether you are investigating a single user issue, a project-specific workload, or a tenant-wide issue.

  - **Correlate compute demand with capacity.** Slow query performance is often the result of slot contention rather than inefficient SQL alone. Compare job resource requests ( `period_estimated_runnable_units` ) against allocated reservation slots ( `period_slot_ms` ) over identical time windows to distinguish between query tuning opportunities and issues caused by insufficient capacity.

  - **Account for telemetry granularity and retention boundaries.** Different information schema views operate on distinct refresh intervals and data retention windows. Job metadata in the `JOBS` view is available for 180 days, whereas high-resolution timeline metrics in the [`JOBS_TIMELINE`](https://docs.cloud.google.com/bigquery/docs/information-schema-jobs-timeline) and [`RESERVATIONS_TIMELINE`](https://docs.cloud.google.com/bigquery/docs/information-schema-reservation-timeline) views are retained for shorter periods (typically 14 to 30 days). For long-term audit and trend analysis, you should export telemetry to partitioned tables.

  - **Avoid metric distortion in multi-statement queries.** Multi-statement scripts (procedural SQL containing `DECLARE` , `IF` , or `WHILE` ) generate a parent job with `statement_type = 'SCRIPT'` and individual child jobs for each statement. When aggregating metrics such as `total_slot_ms` or `total_bytes_billed` , filter out `statement_type = 'SCRIPT'` to prevent double-counting.

  - **Filter on partition columns.** To minimize query execution time and avoid unnecessary scan costs on on-demand analysis, always include restrictive time filters on partition columns such as `creation_time` , `job_start_time` , or `period_start` .

## What's next

  - For more information about information schema syntax and a list of available views, see [Introduction to INFORMATION\_SCHEMA](https://docs.cloud.google.com/bigquery/docs/information-schema-intro) .
  - To learn how to view job details, list active jobs, and cancel running jobs, see [Manage jobs](https://docs.cloud.google.com/bigquery/docs/managing-jobs) .
