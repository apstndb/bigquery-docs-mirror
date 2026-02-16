# Introduction to workload management

BigQuery workload management lets you allocate and manage compute resources available for data analysis and processing, and also lets you specify how you are charged for those resources.

## Workload management models

BigQuery offers two models of workload management. With *on-demand* billing, you pay for the number of bytes processed when you query or process your data. With *capacity-based* billing, you allocate processing capacity for workloads with the option of automatically scaling capacity up and down when needed.

You can switch between on-demand and capacity-based billing models at any time. You can also use a [combination of the two models](/bigquery/docs/reservations-workload-management#combine_reservations_with_on-demand_billing) .

## Choosing a model

Consider the following when choosing a workload management model:

<table>
<thead>
<tr class="header">
<th></th>
<th><strong>On-demand</strong></th>
<th><strong>Capacity-based</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Usage model</strong></td>
<td>Data scanned or processed by your queries</td>
<td>Dedicated slots or autoscaling slots</td>
</tr>
<tr class="even">
<td><strong>Unit of metering</strong></td>
<td>TiB</td>
<td>slot-hours</td>
</tr>
<tr class="odd">
<td><strong>Minimum capacity</strong></td>
<td>Up to 2,000 slots per project</td>
<td>50 slots per reservation</td>
</tr>
<tr class="even">
<td><strong>Maximum capacity</strong></td>
<td>Up to 2,000 slots per project</td>
<td>Configurable per reservation up to regional quota</td>
</tr>
<tr class="odd">
<td><strong>Cost control</strong></td>
<td>Optionally configure project-level or user-level quotas (hard cap)</td>
<td>Configure a budget expressed in slots for each reservation</td>
</tr>
<tr class="even">
<td><strong>Configuration</strong></td>
<td>No configuration required</td>
<td>Create slot reservations and assign to projects</td>
</tr>
<tr class="odd">
<td><strong>Editions support</strong></td>
<td>Fixed feature set</td>
<td>Available in 3 editions</td>
</tr>
<tr class="even">
<td><strong>Capacity discounts</strong></td>
<td>Pay-as-you-go only</td>
<td>Optional slot commitments for steady-state workloads</td>
</tr>
<tr class="odd">
<td><strong>Predictability</strong></td>
<td>Variable usage and billing</td>
<td>Predictable billing through baselines and commitments</td>
</tr>
<tr class="even">
<td><strong>Centralized purchasing</strong></td>
<td>Per project billing</td>
<td>Allocate and bill slots centrally rather than for each project</td>
</tr>
<tr class="odd">
<td><strong>Flexibility</strong></td>
<td>Capacity on-demand (minimum 10 MiB per query)</td>
<td>Baseline or autoscaled slots (1 minute minimum)</td>
</tr>
</tbody>
</table>

## Jobs

Every time you [load](/bigquery/docs/loading-data) , [export](/bigquery/exporting-data-from-bigquery) , [query](/bigquery/docs/running-queries) , or [copy data](/bigquery/docs/managing-tables#copy-table) , BigQuery automatically creates, schedules, and runs a job that tracks the progress of the task.

Because jobs can potentially take a long time to complete, they run asynchronously and can be polled for their status. Shorter actions, such as listing resources or getting metadata, are not managed as jobs.

For more information about jobs, see [Manage jobs](/bigquery/docs/managing-jobs) .

## Slots

A BigQuery slot is a *virtual compute unit* used by BigQuery to execute SQL queries or other [job types](/bigquery/docs/managing-jobs) . During the execution of a query, BigQuery automatically determines how many slots are used by the query. The number of slots used depends on the amount of data being processed, the complexity of the query, and the number of slots available.

To learn more about slots and how they are used, see [understand slots](/bigquery/docs/slots) .

## Reservations

In the capacity-based pricing model, slots are allocated in pools called *reservations* . Reservations let you assign slots in ways that make sense for your organization. For example, you might create a reservation named `  prod  ` for production workloads, and a separate reservation named `  test  ` for testing, so that test jobs don't compete for capacity with production workloads. Or, you might create reservations for different departments in your organization.

For more information about reservations, see [workload management using reservations](/bigquery/docs/reservations-workload-management) .

## BI Engine

BI Engine is a fast, in-memory analysis service that accelerates many SQL queries in BigQuery by intelligently caching the data you use most frequently. BI Engine can accelerate SQL queries from any source, including those written by data visualization tools, and can manage cached tables for ongoing optimization.

[BI Engine reservations](/bigquery/docs/bi-engine-reserve-capacity) are allocated in GiB of memory and managed separately from slot reservations.

For more information about BI Engine, see [Introduction to BI Engine](/bigquery/docs/bi-engine-intro) .

## What's next

  - [Understand slots](/bigquery/docs/slots)
  - [Understand reservations](/bigquery/docs/reservations-workload-management)
  - Learn about [on-demand pricing](https://cloud.google.com/bigquery/pricing#on_demand_pricing)
  - Learn about [capacity-based pricing](https://cloud.google.com/bigquery/pricing#capacity_compute_analysis_pricing)
  - [Estimate and control costs](/bigquery/docs/best-practices-costs)
  - [Create custom cost controls](/bigquery/docs/custom-quotas)
