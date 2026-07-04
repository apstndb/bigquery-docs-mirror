---
name: documents/docs.cloud.google.com/bigquery/docs/admin-jobs-explorer
uri: https://docs.cloud.google.com/bigquery/docs/admin-jobs-explorer
title: Monitor jobs
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# Monitor jobs

As a BigQuery administrator, you can monitor jobs across your organization through an administrative jobs explorer in the Google Cloud console. The jobs explorer provides filters and sorting options to identify, compare, and troubleshoot problematic jobs. You don't need to write `INFORMATION_SCHEMA` queries to view job details, such as the owner, project, slot usage, duration, and more.

With the jobs explorer, you can do the following:

  - **Filter and identify jobs.** Search for specific queries across your organization by [applying filters](https://docs.cloud.google.com/bigquery/docs/admin-jobs-explorer#filter-jobs) based on criteria like job status, duration, owner, or slot usage.
  - **Troubleshoot jobs.** Select individual jobs to view their query execution graphs, SQL text, and execution history on the [**Job details**](https://docs.cloud.google.com/bigquery/docs/admin-jobs-explorer#view_job_details) page ( [Preview](https://cloud.google.com/products#product-launch-stages) ).
  - **Compare performance.** [Compare jobs](https://docs.cloud.google.com/bigquery/docs/admin-jobs-explorer#compare-jobs) ( [Preview](https://cloud.google.com/products#product-launch-stages) ) to highlight significant metric differences and address potential performance issues.
  - **Get AI assistance.** [Use Gemini Code Assist directly from the jobs explorer](https://docs.cloud.google.com/bigquery/docs/admin-jobs-explorer#troubleshoot-with-ai) ( [Preview](https://cloud.google.com/products#product-launch-stages) ) to analyze job statistics or explain slow-running queries.

BigQuery provides the job details and insights from the following `INFORMATION_SCHEMA` views:

  - [`INFORMATION_SCHEMA.JOBS_BY_PROJECT`](https://docs.cloud.google.com/bigquery/docs/information-schema-jobs)
  - [`INFORMATION_SCHEMA.JOBS_BY_ORGANIZATION`](https://docs.cloud.google.com/bigquery/docs/information-schema-jobs-by-organization)
  - [`INFORMATION_SCHEMA.JOBS_BY_USER`](https://docs.cloud.google.com/bigquery/docs/information-schema-jobs-by-user)

> **Note:** If you use organization restrictions, see [Enable access to Google-owned resources](https://docs.cloud.google.com/resource-manager/docs/organization-restrictions/additional-considerations#google-owned-resources) .

## Before you begin

To use Gemini Code Assist to [troubleshoot jobs in BigQuery (Preview)](https://docs.cloud.google.com/bigquery/docs/admin-jobs-explorer#troubleshoot-with-ai) , see [Set up Gemini Code Assist](https://docs.cloud.google.com/cloud-assist/set-up-gemini) to enable the API and give the required roles for it.

### Required roles

To get the permissions that you need to use the jobs explorer to monitor jobs, ask your administrator to grant you the following IAM roles:

  - View jobs at the project level: [BigQuery Resource Viewer](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceViewer) ( `roles/bigquery.resourceViewer` ) on the project
  - View jobs at the organization level: [BigQuery Resource Viewer](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceViewer) ( `roles/bigquery.resourceViewer` ) on the organization
  - Filter by reservations in your organization: [BigQuery Resource Viewer](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceViewer) ( `roles/bigquery.resourceViewer` ) on the organization
  - View job details: [BigQuery Resource Viewer](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceViewer) ( `roles/bigquery.resourceViewer` ) on the project where the queries were run
  - View system-level details: [BigQuery Resource Viewer](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceViewer) ( `roles/bigquery.resourceViewer` ) on the administration project

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

These predefined roles contain the permissions required to use the jobs explorer to monitor jobs. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

The following permissions are required to use the jobs explorer to monitor jobs:

  - View jobs at the project level: `bigquery.jobs.listAll` on the project
  - View jobs at the organization level: `bigquery.jobs.listAll` on the organization
  - Filter by reservations in your organization: `bigquery.reservations.list` on the organization

You might also be able to get these permissions with [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

> **Note:** The organization view is only available if you have defined Google Cloud organizations.

To use Gemini Code Assist to troubleshoot jobs, see additional [IAM requirements for using Gemini Code Assist](https://docs.cloud.google.com/cloud-assist/iam-requirements) .

## Filter jobs

To filter jobs for queries that are contained in the `INFORMATION_SCHEMA.JOBS*` views, do the following:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the navigation menu, click **Jobs explorer** .

3.  From the **Location** list, select the location for which you want to view the jobs.

4.  Apply optional **Filters** as needed:
    
      - **Job scope** : filters jobs by their visibility level—for example, the current project, organization, and your jobs. You can choose to view jobs from the current project, across your entire organization, or only jobs that you initiated.
      - **Status** : filters jobs by their current execution state—for example, completed, error, active, and queued. This helps you identify active or failed jobs.
      - **Job category** : filters jobs by the type of operation performed, such as standard SQL queries or continuous queries used for real-time data processing.
      - **Job creation reason** : filters jobs based on why BigQuery created them, such as when a query exceeds a timeout or produces results too large for a single response.
      - **Job priority** : filters jobs by their execution priority, such as interactive or batch jobs.
      - **Job ID** : filters for a specific job by its unique alphanumeric identifier.
      - **Owner** : filters jobs by the email address of the user or service account that started the job.
      - **Project ID** : filters jobs that ran in a specific project. This filter is only available when the **Job scope** is set to **Organization** .
      - **Reservation ID** : filters jobs that used slots from a specific reservation. This helps you monitor how different workloads are consuming reserved capacity.
      - **Slot time more than** : filters for jobs that consumed more than a specified amount of slot-milliseconds. This is a key metric for identifying resource-intensive queries.
      - **Duration more than** : filters for jobs that took longer than a specified amount of time to complete. Use this to find queries that are running slower than expected.
      - **Bytes processed more than** : filters for jobs that scanned more than a specified amount of data. This helps you identify queries that might be contributing to high data processing costs.
      - **Query insights** : filters jobs that BigQuery has identified as having specific performance issues, such as slot contention, memory shuffle capacity exceeded, and data input scale change.
      - **Query hash** : filters for jobs with a specific query hash. A query hash identifies the logic of a query, ignoring differences in comments, parameter values, UDFs, and literals, which helps you find all executions of the same query logic. This field appears for successful [GoogleSQL](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/query-syntax) queries that are not cache hits.
      - **Labels** : filters jobs based on custom metadata labels that you or your organization have attached to them. This lets you categorize and track jobs by department or application.

## Troubleshoot job performance

> **Preview**
> 
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

> **Note:** To request feedback or support for this feature, send an email to <bq-performance-troubleshooting+feedback@google.com> .

To diagnose and troubleshoot queries, you can view execution metrics, SQL text, and historical performance variances on the **Job details** page.

### View job details

To view a job's details and analyze its query execution, do the following:

1.  Go to the **Jobs explorer** page.

2.  Optional: To narrow the displayed jobs, [filter](https://docs.cloud.google.com/bigquery/docs/admin-jobs-explorer#filter-jobs) the jobs.

3.  Click the job ID of the job you want to investigate. For queries that don't create a job, the query ID appears and the link is disabled. Clicking a valid job ID opens the **Job details** page with the **Performance** tab displayed by default.

### Available query information

To help you diagnose query performance, the **Performance** tab in the job details compiles the following information and metrics, when applicable:

  - **Job details** : information about the job, including the job ID, creation time, bytes processed, and slot usage. For more information, see [View job details](https://docs.cloud.google.com/bigquery/docs/managing-jobs#view-job) .

  - **Execution history** : a list of historical executions of the query, grouped by query hash. You can select a job from this list to compare directly against your current job. For more information, see [Compare jobs](https://docs.cloud.google.com/bigquery/docs/admin-jobs-explorer#compare-jobs) .

  - **Execution graph** : a visual representation of the query execution stages. Expand the **Execution graph** section to inspect slot contention, shuffle capacity, and data input scale. For more information, see [Get query performance insights](https://docs.cloud.google.com/bigquery/docs/query-insights) .
    
    The following example shows an execution graph with SQL text mapping enabled:
    
    ![Execution graph for jobs.](https://docs.cloud.google.com/static/bigquery/images/jobs-execution-graph.png)

  - **System load during execution** : a summary of the compute resources and reservation settings allocated during job execution.

## Diagnose performance regressions by comparing jobs and systems

> **Preview**
> 
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

> **Note:** To request feedback or support for this feature, send an email to <bq-performance-troubleshooting+feedback@google.com> .

The performance comparison tool lets you analyze performance differences between two query jobs or across two system intervals. The analysis shows query details, resource utilization shifts, and system environment settings that differ significantly between your baseline and target environments.

### Understand comparison analysis

The comparison tool evaluates performance across query-level metrics and system-level factors. You can turn on the **Show only significant differences** toggle to limit the view to metrics with a variance larger than 20%.

Significant differences are color-coded to help you scan for issues:

  - **Green** : the metric improved (for example, a shorter query duration in the target run).
  - **Yellow** : the metric degraded by less than 20%.
  - **Red** : the metric degraded by more than 20%.

### Compare two jobs

To compare a baseline job against a target job execution, do the following:

1.  Open the **Jobs explorer** page.

2.  Optional: To narrow the displayed jobs, [filter](https://docs.cloud.google.com/bigquery/docs/admin-jobs-explorer#filter-jobs) the jobs.

3.  Click the job ID of your baseline job to open the **Job details** page, and select the **Performance** tab.

4.  In the **Actions** menu, click **Compare Job** .

5.  In the **Job one (baseline job)** field, click **Browse** to open the **Similar comparable jobs** pane.

6.  Select the target job you want to compare against your baseline, and click **Compare** .

7.  Optional: To focus on major performance regressions, turn on **Show only significant differences** . This limits the view to metrics with a variance larger than 20%.

To change the jobs being compared at any time, click **Browse** in the baseline or target job fields and select a new job from the comparable jobs list.

#### Query-level analysis

After comparing two jobs, you can view the **Query level analysis** section, which compares two job executions across three tabs:

  - **Metrics** : compares core query metrics, such as job duration, slot time, bytes processed, and unused accelerators.
  - **SQL text** : displays the SQL statements for both jobs and highlights text differences.
  - **Execution graph** : compares the [execution graphs](https://docs.cloud.google.com/bigquery/docs/query-plan-explanation) of both jobs stage-by-stage to pinpoint where bottlenecks occurred.

### Compare two system intervals

Administrators and analysts can analyze broader environment metrics by executing a system performance comparison. This tool lets you compare historical intervals across specific reservations and projects to understand utilization shifts and isolate whether performance degradation originated internally or externally to your workload.

You can navigate to the system performance comparison view in any of the following ways:

  - On the **Job details** page, after you [compare two jobs](https://docs.cloud.google.com/bigquery/docs/admin-jobs-explorer#compare-two-jobs) , click **View more** in the **System level outputs** section to view system comparison details.
  - If you use Gemini Cloud Assist to perform a system comparison, then Gemini Cloud Assist generates a link that opens the system comparison results.

To perform a system-level comparison over separate time periods, do the following:

1.  From the **System performance comparison** view, click **System** .
2.  Select the system where you want to analyze performance by clicking **Browse** and selecting a reservation or project scope.
3.  Define the comparison time frames:
      - **Target Interval** : select the date and time window for the period experiencing performance issues, and click **Apply** .
      - **Baseline Interval** : select the reference date and time window to act as your performance benchmark, and click **Apply** .

#### System-level analysis

After comparing intervals, the view maps utilization shifts, concurrency variations, and setting differences across the selected environment against its parent group. This helps you determine if slot contention or configuration regressions are impacting your workload. The data is generated under three blocks:

  - **Project** : compares job concurrency, queued concurrency, and total slot usage at the project level.
  - **Reservation** : compares reservation utilization, idle slot sharing, and project concurrency across shared [reservations](https://docs.cloud.google.com/bigquery/docs/reservations-intro) .
  - **Config analysis** : compares workload management settings between the two runs, such as max reservation size caps and idle slot borrowing rules.

## Use agentic performance troubleshooting insights

> **Preview**
> 
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

To provide feedback or request support for this feature, send an email to <bq-performance-troubleshooting+feedback@google.com> .

When you monitor administration tasks or evaluate performance comparisons, BigQuery integrates underlying observability diagnostics with Gemini Cloud Assist to turn the chat pane into an active troubleshooting assistant as you troubleshoot job-level and system-level anomalies.

The insights are access controlled; without sufficient permissions, the insights you receive might be limited. For more information about permissions, see [Control access to resources with IAM](https://docs.cloud.google.com/bigquery/docs/control-access-to-resources-iam) .

### Troubleshoot performance in chat

To initialize context-aware troubleshooting and act on performance insights, do the following:

1.  To open the Gemini Cloud Assist chat pane and automatically load your relevant job or system context, do one of the following:
    
      - In the **Jobs explorer** or **Job history** pages, hover over a job and click spark **Gemini** in that table row.
      - In the **Workload management** page, hover over a reservation and click spark **Gemini** in that table row.
      - In the **Studio** , **Monitoring** or **Jobs explorer** , click spark **Gemini** .

2.  Submit a prompt in natural language. For example, ask Gemini to explain why a job is running slow, analyze specific job statistics, analyze specific reservation performance, troubleshoot system performance issues, or compare performance variances between two similar historical jobs.

3.  If an organization-level or reservation-level threshold is breached, such as severe slot queuing due to an unexpected surge in active project concurrency, review the generated **Performance Insights** report. This report details critical bottlenecks such as the following:
    
      - **Increased Queued Concurrency** : spikes in concurrent query demands that exceed soft concurrency limits or reservation slot allotments.
      - **Increased Project Concurrency** : tracking the exact high-concurrency projects or top user accounts driving the system load across shared reservations or on-demand quotas.

4.  Observe the **Key Metrics Comparison** table to trace precise numeric differences, such as shifts in average project concurrency, queue slots, or maximum reservation slot caps.

5.  Execute inline solutions directly through actionable handoff links generated by Gemini Cloud Assist. These shortcuts redirect you to specific in-product tools with pre-populated context to answer your questions and resolve issues:
    
      - **Edit reservation** : opens the workload management side panel to adjust maximum reservation sizes or activate advanced scale capabilities.
      - **View job performance in Job explorer** : opens the performance details tab for the particular job.
      - **Compare job performance in Job explorer** : compare the performance of two jobs side by side.

## Pricing

Jobs explorer is available at no additional cost. Queries that are used to populate these charts aren't billed and don't use slots in user-owned reservations. Queries that process too much data are timed out.

## What's next

  - Learn about [reservations](https://docs.cloud.google.com/bigquery/docs/reservations-intro) .
  - Learn about [purchasing slots](https://docs.cloud.google.com/bigquery/docs/reservations-commitments) .
  - Learn how to [estimate slot capacity requirements](https://docs.cloud.google.com/bigquery/docs/slot-estimator) .
  - Learn how to [view slot recommendations and insights](https://docs.cloud.google.com/bigquery/docs/slot-recommender) .
