---
name: documents/docs.cloud.google.com/bigquery/docs/troubleshoot-workload-management
uri: https://docs.cloud.google.com/bigquery/docs/troubleshoot-workload-management
title: Troubleshoot BigQuery workload management
description: Troubleshoot common issues with BigQuery workload management, including reservations, capacity commitments, slot contention, and monitoring.
data_source: docs.cloud.google.com
---

# Troubleshoot BigQuery workload management

This document shows you how to troubleshoot common issues with BigQuery workload management, including reservation allocation and assignments, reservation configuration errors, capacity commitments, slot contention, and reservation monitoring.

To view and manage reservations, commitments, and administrative resource charts, ensure that you have the required Identity and Access Management (IAM) roles, such as the BigQuery Resource Viewer ( `roles/bigquery.resourceViewer` ) or BigQuery Resource Admin ( `roles/bigquery.resourceAdmin` ) role on the administration project. For more information, see [Access control with IAM](https://docs.cloud.google.com/bigquery/docs/access-control) .

## Troubleshoot issues with reservations

Use the following information to troubleshoot common issues with reservations, such as errors when adding slots, why a reservation isn't used for a BigQuery job, or unrecognized reservations.

### Unable to add more slots to the reservation size

If you encounter errors like `Failed to allocate slots for reservation in the current system state` or `Failed to update reservation: Failed to allocate slots for reservation` while trying to add more slots to your reservation, this is usually a transient issue. To mitigate the issue, do the following:

  - Retry with a smaller number of slots.
  - If trying with a smaller number of slots fails, wait 15 minutes and retry the operation.

If after retrying multiple times and waiting for 30 minutes you still receive the same error, [contact Cloud Customer Care](https://docs.cloud.google.com/bigquery/docs/getting-support) .

### There is insufficient quota to complete this request

If the error message states `There is insufficient quota to complete this request` , the request exceeds the quota limit that is set for the project.

To resolve this error, do one of the following:

  - Add a smaller number of slots to the reservation so that the request doesn't exceed the quota limit.
  - Request a quota increase in the corresponding region. For more information, see [Request a quota increase](https://docs.cloud.google.com/bigquery/quotas#requesting_a_quota_increase) .

### Reservation not used by BigQuery to run a job

There are multiple scenarios where a job might run using [on-demand pricing](https://cloud.google.com/bigquery/pricing#on_demand_pricing) or a free shared slot pool instead of using the reservation that you created.

#### Query and reservation are in different regions

Reservations are regional resources. A query runs in the same location as any tables referenced in the query.

If the location of a table doesn't match the location of the reservation, the query doesn't use the reservation and instead runs using on-demand pricing (or the free shared slot pool for eligible batch load and export jobs).

#### Querying BigQuery Omni tables

When querying a BigQuery Omni table, make sure that you create the reservation in the same region as the table, not in a colocated region. If you create the reservation in the colocated BigQuery region, the query runs using on-demand pricing.

#### The reservation was created, but the project wasn't assigned to it

To use the slots in a reservation, you must create an assignment that assigns the project, folder, or organization to the specific reservation. Make sure that the project has a corresponding [assignment for the reservation](https://docs.cloud.google.com/bigquery/docs/reservations-assignments) .

#### Job type mismatch

Make sure to select the correct [job type](https://docs.cloud.google.com/bigquery/docs/reservations-workload-management#assignments) when creating an assignment; otherwise, the jobs don't use the reservation.

For example, if you select `PIPELINE` as the job type, all query jobs run using on-demand pricing. Change the assignment type to `QUERY` to make the query jobs run using the reservation.

#### Multi-statement queries

If you're running multi-statement queries, the parent job object doesn't have a reservation associated with it, even if the child jobs run under a reservation.

To confirm whether the job actually used a reservation, check the child job metadata.

#### Retrieving cached results

When a query job retrieves cached results, the reservation field is empty because BigQuery performs no computation and fetches the results directly from the temporary table.

#### Change data capture row modification operations

If you have [change data capture (CDC) tables](https://docs.cloud.google.com/bigquery/docs/change-data-capture) , BigQuery applies pending row modifications within the `max_staleness` interval as background jobs that use the `BACKGROUND` assignment type. If there are no `BACKGROUND` assignments, these jobs use on-demand pricing. Consider creating a `BACKGROUND` assignment for the project to avoid unexpected on-demand costs. You can identify these jobs by the `queueworker_cdc_background_merge_coalesce` substring in the job identifier.

#### BigQuery ML model types that use external services

If no reservation assignment with an `ML_EXTERNAL` job type is found in the project, external model creation jobs run using on-demand pricing. The `QUERY` job type assignment applies to standard BigQuery ML models and matrix factorization models (which require an Enterprise or Enterprise Plus edition reservation), whereas external models require an `ML_EXTERNAL` assignment. For more information, see [Assign slots to BigQuery workloads](https://docs.cloud.google.com/bigquery/docs/reservations-assignments#assign-ml-workload) .

### Unrecognized reservations identified in the project

BigQuery owns reservations that represent a free shared slot pool for certain operations in BigQuery.

#### `default-pipeline`

By default, batch loading or batch exporting of data in BigQuery uses a free shared slot pool. When you inspect these load or extract jobs, the reservation field shows `default-pipeline` .

There are no charges for using the shared slot pool. If you want consistent, predictable performance, consider purchasing a `PIPELINE` reservation.

## Troubleshoot reservation management tasks

You might encounter the following errors when creating or updating a reservation.

### Reservation size or baseline slots must be a multiple of 50

**Error message**

  - `Max reservation size can only be configured in multiples of 50, except when covered by excess commitments.`
  - `Baseline slots can only be configured in multiples of 50, except when covered by excess commitments.`

**Cause**

Slots always autoscale to a multiple of 50. BigQuery scales up slots based on actual usage and rounds up to the nearest 50-slot increment. When there's no commitment or if the commitment can't cover the increases, you can only increase the baseline and autoscaling slots in multiples of 50.

If `baseline slots` or `max reservation size - baseline slots` isn't a multiple of 50 (and isn't covered by excess capacity commitments), then the reservation can't scale up to the maximum reservation size, resulting in this error.

**Resolution**

Do one of the following:

  - Purchase more capacity commitments to cover the slot increases.
  - Choose baseline and maximum slots that are increments of 50.

## Troubleshoot capacity commitments

This section describes troubleshooting steps that you might find helpful if you run into issues with BigQuery capacity commitments.

### Purchased slots are pending

Slots are subject to available capacity. When you purchase slot commitments and BigQuery allocates them, the **Status** column shows a check mark. If BigQuery can't allocate the requested slots immediately, the **Status** column remains pending. You might have to wait several hours for the slots to become available. If you need access to slots sooner, try the following:

1.  Delete the pending commitment.
2.  Purchase a new commitment for a smaller number of slots. Depending on capacity, the smaller commitment might become active immediately.
3.  Purchase the remaining slots as a separate commitment. These slots might show as pending in the **Status** column, but they generally become active within a few hours.
4.  Optional: When both commitments become active, [merge](https://docs.cloud.google.com/bigquery/docs/reservations-commitments#merging-commitments) them into a single commitment, provided that both commitments are in the same region and edition and have the same commitment plan.

If a slot commitment fails or takes a long time to complete, consider using [on-demand pricing](https://cloud.google.com/bigquery/pricing#on_demand_pricing) temporarily. With this solution, you can run critical queries in a different project that isn't assigned to any reservations, [assign the project to `None`](https://docs.cloud.google.com/bigquery/docs/reservations-assignments#assign-project-to-none) , or remove the project assignment altogether.

## Troubleshoot slot contention

Slot contention can happen when there aren't enough slots to run all of your jobs, causing performance issues. To analyze whether performance degradation stems from workload increases or environment configuration changes, you can [compare two system intervals](https://docs.cloud.google.com/bigquery/docs/admin-jobs-explorer#compare-two-system-intervals) across reservations and projects.

To troubleshoot slot contention issues, use the following steps and best practices.

If you've tried these best practices but are still experiencing job performance issues, you can [request support](https://docs.cloud.google.com/bigquery/docs/getting-support) .

### Job concurrency spikes

Use the [detailed view](https://docs.cloud.google.com/bigquery/docs/admin-resource-charts#detailed-view) in the administrative resource charts to check for a sudden surge in job runs with simultaneous slot usage spikes. These spikes can indicate that too many jobs are contending for the slots available in your reservation.

**Best practice:** Consider optimizing resource-intensive queries or increasing your reservation's slot capacity. For more information about optimizing query performance, see [Optimize query computation](https://docs.cloud.google.com/bigquery/docs/best-practices-performance-compute) .

### High slot usage

Use the [detailed view](https://docs.cloud.google.com/bigquery/docs/admin-resource-charts#detailed-view) to check for increased job durations, especially if there are jobs that exceed your reservation's maximum capacity. Consistently high slot usage can indicate ongoing slot contention.

**Best practice:** Check queries using the [jobs explorer](https://docs.cloud.google.com/bigquery/docs/admin-jobs-explorer) slot contention filter to identify the queries that consume the most slots and optimize them.

### Lengthy job durations

If jobs are taking significantly longer to complete, check the [detailed view](https://docs.cloud.google.com/bigquery/docs/admin-resource-charts#detailed-view) . High job concurrency and slot usage spikes can indicate slot contention.

**Best practice:** Isolate critical jobs by temporarily pausing less important jobs or reducing your overall job submission rate.

### Slot contention messages

The [insights table](https://docs.cloud.google.com/bigquery/docs/admin-resource-charts#insights-table) can display messages such as `There were NUMBER jobs detected with slot_contention in the reservation.` that indicate slot contention issues. Check the [jobs explorer](https://docs.cloud.google.com/bigquery/docs/admin-jobs-explorer) to review details about the specific jobs flagged in these messages.

**Best practice:** Optimize the identified queries or adjust your reservation's slot allocation.

## Troubleshoot reservation monitoring

The following sections describe how to resolve common issues when monitoring BigQuery reservations and slot usage.

### Slot usage metrics don't match `INFORMATION_SCHEMA`

If you encounter discrepancies between slot usage metrics in resource charts and `INFORMATION_SCHEMA` data, try the following:

  - **Reduce granularity.** Change the chart granularity to 1-second intervals instead of 1-hour intervals.
  - **Align aggregation.** Make sure that you're using aggregation methods that align between resource charts and `INFORMATION_SCHEMA` data. For example, to better reflect peak usage in resource charts, change the metric aggregation to p99 or p90 consistently.

### Borrowed slots appear when idle slots are disabled

Your monitoring charts might show a non-zero value for `borrowed_slots` even if `ignore_idle_slots=true` is set for one or more reservations. This setting prevents a reservation from *borrowing* idle slots, but doesn't prevent it from *lending* its unused slots to other reservations.

These borrowed slots appear in the following cases:

  - **Lending to other reservations.** A reservation with `ignore_idle_slots=true` can lend its unused baseline slots to other reservations in the same administration project, region, and edition that *do* allow idle slot borrowing ( `ignore_idle_slots=false` ). If all reservations in an administration project, region, and edition have `ignore_idle_slots=true` , then idle slots aren't shared between them.
    
    For example, assume Reservation A has 100 slots, 0 usage, and is configured with `ignore_idle_slots=true` . Reservation B is in the same administration project, region, and edition, has 100 slots, needs 150 slots for its workload, and is configured with `ignore_idle_slots=false` . Reservation B can borrow 50 idle slots from Reservation A to meet its needs. When this occurs, monitoring charts report 50 `lent_slots` for Reservation A and 50 `borrowed_slots` for Reservation B.

  - **Usage exceeding capacity.** If a reservation's slot usage temporarily exceeds its capacity (baseline + autoscaled slots), monitoring charts show this difference as `borrowed_slots` . This behavior can occur even for reservations with `ignore_idle_slots=true` .

Slot usage can occasionally exceed the sum of your baseline plus scaled slots. You aren't billed for slot usage that's greater than your baseline plus scaled slots.

### Borrowed slots appear before a reservation is fully used

Monitoring dashboards use sampled data, which might not accurately reflect the precise timing of slot usage within a sampling interval.

For a more accurate analysis of slot usage, query columns related to idle slots, such as the `borrowed_slots` and `lent_slots` columns in the [`INFORMATION_SCHEMA.RESERVATIONS_TIMELINE` view](https://docs.cloud.google.com/bigquery/docs/information-schema-reservation-timeline#schema) .

## What's next

  - Learn more about [workload management using reservations](https://docs.cloud.google.com/bigquery/docs/reservations-workload-management) .
  - Learn how to [manage workload reservations](https://docs.cloud.google.com/bigquery/docs/reservations-tasks) .
  - Learn about [purchasing and managing slot commitments](https://docs.cloud.google.com/bigquery/docs/reservations-commitments) .
  - Learn how to [monitor reservations](https://docs.cloud.google.com/bigquery/docs/reservations-monitoring) and [use administrative resource charts](https://docs.cloud.google.com/bigquery/docs/admin-resource-charts) .
  - Explore other [BigQuery troubleshooting resources](https://docs.cloud.google.com/bigquery/docs/troubleshoot-intro) .
