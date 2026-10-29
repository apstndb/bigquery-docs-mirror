---
name: documents/docs.cloud.google.com/bigquery/docs/reliability-intro
uri: https://docs.cloud.google.com/bigquery/docs/reliability-intro
title: Understand reliability
description: Learn about BigQuery reliability features, including availability, durability, consistency, disaster recovery, and error-handling best practices.
data_source: docs.cloud.google.com
---

# Understand reliability

BigQuery lets you run analytics workloads with minimal disruption by automatically handling machine and zonal failures within a region. For broader resiliency, you can configure cross-region disaster recovery, restore deleted or corrupted data, and implement client-side error retries to meet your reliability requirements.

These capabilities support workloads that ingest and analyze large volumes of data with consistent performance, including anomaly detection, real-time analytics with [streaming ingestion](https://docs.cloud.google.com/bigquery/docs/streaming-data-into-bigquery) , and predictive analytics with [BigQuery ML](https://docs.cloud.google.com/bigquery/docs/bqml-introduction) . For detailed examples of these solutions, see [BigQuery reference patterns](https://docs.cloud.google.com/bigquery/docs/reference-patterns) .

## Dimensions of reliability in BigQuery

To determine whether BigQuery meets your workload's requirements, you can evaluate its reliability across five key dimensions: availability, durability, data consistency, performance consistency, and data recovery.

### Availability

Availability defines your ability to read data from BigQuery or write data to it. BigQuery is built to make both read and write operations highly available with a [99.99% uptime SLA](https://cloud.google.com/bigquery/sla) . There are two components involved in both operations:

- The BigQuery service
- Compute resources required to execute the specific query

Reliability of the service is a function of the specific BigQuery API that you use to retrieve the data. The availability of compute resources depends on the capacity available to you when you run the query. For more information about the fundamental unit of compute for BigQuery and the [slot resource economy](https://docs.cloud.google.com/bigquery/docs/slots#slot_resource_economy) , see [Understand slots](https://docs.cloud.google.com/bigquery/docs/slots) .

### Durability

Durability measures the proportion of data that you can successfully read, as defined in the [Implementing SLOs](https://sre.google/workbook/implementing-slos/) chapter of the *Site Reliability Workbook* . To provide high durability, BigQuery automatically stores redundant copies of your data across two zones within your selected location.

### Data consistency

Data consistency defines how and when you can query data after it's written or modified. One aspect of data consistency is ensuring "exactly-once" semantics for data ingestion. For more information, see [Retry failed job insertions](https://docs.cloud.google.com/bigquery/docs/reliability-intro#retry_failed_job_insertions) .

### Performance consistency

In general, performance can be expressed in two dimensions. *Latency* is a measure of the execution time of long data retrieval operations such as queries. *Throughput* is a measure of how much data BigQuery can process during a specific period of time. Due to BigQuery's multi-tenant, horizontally scalable design, its throughput can scale up to arbitrary data sizes. Your specific use case determines the relative importance of latency and throughput.

### Data recovery

You can measure the ability to recover data after an outage by using the following metrics:

- *Recovery Time Objective* (RTO): the maximum length of time that data can be unavailable after an incident.
- *Recovery Point Objective* (RPO): the maximum amount of data collected before the incident that your organization can tolerate losing.

These considerations are specifically relevant in the unlikely case that a zone or region experiences a multi-day or destructive outage.

## Disaster planning

In this section, *disaster planning* covers failures ranging from the loss of a single machine to the catastrophic loss of an entire region. BigQuery handles single-machine and zonal failures automatically, whereas regional failures require you to design your architecture for recovery if your workload requires it. Understanding where automatic recovery ends and your responsibility begins is essential for disaster planning.

BigQuery offers a [99.99% uptime SLA](https://cloud.google.com/bigquery/sla) . This availability is supported by BigQuery's regional architecture, which writes data to two different zones and provisions redundant compute capacity. The BigQuery SLA is the same for regions (such as `us-central1` ) and multi-regions (such as `US` ).

### Automatic failure handling

Because BigQuery is a regional service, it automatically handles the loss of an individual machine or an entire zone. BigQuery abstracts underlying zonal infrastructure from you.

#### Loss of a machine

Machine failures are an everyday occurrence at the scale at which Google operates. BigQuery is designed to handle machine failures automatically without affecting the containing zone.

BigQuery breaks each query into small tasks and dispatches them in parallel across many machines. If a machine fails or degrades, then BigQuery automatically redispatches the affected tasks to another machine. This approach is crucial to reducing tail latency.

BigQuery uses [Reed-Solomon](https://en.wikipedia.org/wiki/Binary_Reed%E2%80%93Solomon_encoding) encoding to durably store a zonal copy of your data, and it stores at least one additional zonal copy in another zone. If multiple machine failures cause the loss of a zonal copy, then BigQuery detects the loss and creates a new zonal copy to restore redundancy.

#### Loss of a zone

To meet its 99.99% uptime SLA, BigQuery provides automatic zonal redundancy for both data and compute slots. Because single-zone compute availability can't meet this SLA alone, BigQuery automatically routes new queries to another zone within one minute of a severe zonal disruption. In-flight queries might take longer to finish, whereas newly issued queries complete normally in another zone.

Even if a zone remains unavailable for an extended period, no data loss occurs because BigQuery synchronously writes data to two zones. As a result, a zonal outage doesn't disrupt your service.

### Types of failures

There are two types of failures: soft failures and hard failures.

A *soft failure* is an operational deficiency where hardware isn't destroyed. Examples include a power failure, network partition, or machine crash. BigQuery is designed to prevent data loss during a soft failure.

A *hard failure* is an operational failure in which hardware is destroyed, such as damage from floods, earthquakes, or hurricanes. Whether BigQuery can prevent data loss during a hard failure depends on whether the failure affects a single zone or an entire region.

### Location redundancy and failure behavior

When you create a BigQuery dataset, you select a location in which to store your data. This location is one of the following:

- A region: a specific geographical location, such as Iowa ( `us-central1` ) or Montréal ( `northamerica-northeast1` ).
- A multi-region: a large geographic area that contains two or more geographic places, such as the United States ( `US` ) or Europe ( `EU` ).

In either case, BigQuery automatically stores copies of your data in two different Google Cloud [zones](https://docs.cloud.google.com/docs/geography-and-regions#regions_and_zones) within a single region in the selected location.

In addition to storage redundancy, BigQuery also maintains redundant compute capacity across multiple zones. By combining redundant storage and compute across multiple availability zones, BigQuery provides both high availability and durability.

> **Note:** Selecting a multi-region location doesn't provide cross-region replication or regional redundancy. BigQuery stores your data in a single region within the multi-region location.

In the event of a machine-level failure, BigQuery continues to run with no more than a few milliseconds of delay, and all currently running queries continue processing. During a soft or hard zonal failure, no data loss occurs, although you might need to resubmit currently running queries. BigQuery automatically mitigates soft zonal failures—such as power outages, transformer failures, or network partitions—within a few minutes.

A soft regional failure, such as a region-wide loss of network connectivity, results in a loss of availability until the region comes back online, but it doesn't result in lost data. A hard regional failure, such as a disaster that destroys an entire region, can result in the loss of data stored in that region. BigQuery doesn't automatically provide a backup or replica of your data in another geographic region. You can use [cross-region dataset replication](https://docs.cloud.google.com/bigquery/docs/data-replication) or [managed disaster recovery](https://docs.cloud.google.com/bigquery/docs/managed-disaster-recovery) to enhance your resiliency to hard regional failures.

For more information about BigQuery dataset locations, see [Location considerations](https://docs.cloud.google.com/bigquery/docs/locations#data-locations) .

### Scenario: Loss of region

BigQuery doesn't provide durability or availability if a physical region is destroyed. This limitation applies to both regions and multi-regions, so maintaining durability and availability during a regional outage requires you to plan ahead. If BigQuery's 99.99% SLA doesn't meet your availability requirements during a temporary regional outage, then consider configuring redundant availability across regions.

To prevent data loss if a region is destroyed, back up your data to another geographic location. For example, you can use [cross-region dataset replication](https://docs.cloud.google.com/bigquery/docs/data-replication) to continuously replicate your data to a geographically distinct region.

If you use a BigQuery multi-region, then don't back up data to a single region within that multi-region's geographic scope. For example, if you back up data from the `US` multi-region, then avoid choosing an overlapping region such as `us-central1` because of the risk of correlated failure during a disaster. For more information about the geographic scope of multi-regions, see [Multi-regions](https://docs.cloud.google.com/bigquery/docs/locations#multi-regions) .

To avoid extended unavailability, replicate your data and provision slots in two geographically separate BigQuery locations. You can use [managed disaster recovery](https://docs.cloud.google.com/bigquery/docs/managed-disaster-recovery) to automatically provision slots in a secondary region and control failover of your workloads from one region to another.

### Scenario: Accidental deletion or data corruption

By virtue of BigQuery's [multiversion concurrency control](https://en.wikipedia.org/wiki/Multiversion_concurrency_control) architecture, BigQuery supports [time travel](https://docs.cloud.google.com/bigquery/docs/time-travel) . With time travel, you can query data from any point in time within the past 7 days. This capability lets you restore data that was mistakenly deleted, modified, or corrupted within the 7-day window. Time travel also works on tables that have been deleted.

BigQuery also lets you create [table snapshots](https://docs.cloud.google.com/bigquery/docs/table-snapshots-intro) to back up data within the same region for longer than the 7-day time travel window. Creating a snapshot is a metadata-only operation that doesn't incur additional storage charges. Although table snapshots help protect against accidental deletion, they don't increase data durability.

### Disaster recovery for real-time analytics

For a [real-time analytics pipeline](https://docs.cloud.google.com/bigquery/docs/reliability-intro#real-time_analytics) that continuously ingests streaming endpoint logs into BigQuery, protecting against extended regional unavailability requires continuously replicating data and provisioning slots in a secondary region. However, because the ingestion architecture is already resilient to temporary BigQuery unavailability when it uses Pub/Sub and Dataflow as one of its [data loading methods](https://docs.cloud.google.com/bigquery/docs/loading-data#methods) , this high level of redundancy might not be worth the cost.

For example, suppose that you configure nightly extract jobs to export BigQuery data from `us-east4` to Cloud Storage Archive storage in `us-central1` . This export provides a durable backup if catastrophic data loss occurs in `us-east4` . In this configuration, the Recovery Point Objective (RPO) is 24 hours because the most recent backup can be up to 24 hours old. The Recovery Time Objective (RTO) can be several days because you must restore the data from the Cloud Storage backup to BigQuery in `us-central1` . If you provision BigQuery in a different region from your backups, then you must transfer the data to that region first. Unless you purchase redundant slots in the recovery region in advance, provisioning the required BigQuery capacity might take additional time depending on the quantity that you request.

### Disaster recovery for batch data processing

For a [batch data processing workload](https://docs.cloud.google.com/bigquery/docs/reliability-intro#batch_data_processing) where you must deliver a business-critical daily report to a regulator by a fixed deadline, implementing redundancy by running two separate instances of the entire processing pipeline is often worth the cost. Using two separate regions, such as `us-west1` and `us-east4` , provides geographic separation and two independent failure domains in case of extended regional unavailability or permanent region loss.

If you must deliver the report exactly once, then you need to reconcile the output when both pipelines finish successfully. One approach is to select the result from the pipeline that finishes first—for example, by publishing a notification to a Pub/Sub topic upon completion. Alternatively, you can let the second pipeline overwrite the result and use object versioning in Cloud Storage. If the pipeline that finishes later writes corrupt data, then you can restore the version written by the first pipeline from Cloud Storage.

## Error handling

The following sections describe best practices for handling errors that affect reliability.

### Retry failed API requests

When your client applications, client libraries, or partner tools issue API requests to BigQuery, use [truncated exponential backoff](https://en.wikipedia.org/wiki/Exponential_backoff) . With this retry strategy, if a client receives a system error or a quota error, then it retries the request up to a maximum number of times using a randomized, increasing wait interval.

Using truncated exponential backoff makes your application more resilient to transient errors. Even under normal operating conditions, you can expect approximately one in 10,000 requests to fail, as described in BigQuery's [99.99% availability SLA](https://cloud.google.com/bigquery/sla) . Under abnormal conditions, this error rate might increase, but if errors are randomly distributed, then exponential backoff can mitigate most failures.

If a request persistently fails with a `5xx` error, then contact Cloud Customer Care and clearly communicate the business impact when setting the [support case priority](https://docs.cloud.google.com/support/docs/customer-care-procedures#support_case_priority) so that support can triage the issue accurately. Conversely, if a request persistently fails with a `4xx` error, then you can resolve the issue by modifying your application. Check the error message for details.

### Exponential backoff logic example

Exponential backoff logic retries a query or request by increasing the wait time between retries up to a maximum backoff time. The following steps illustrate how a client implements truncated exponential backoff:

1.  Make a request to BigQuery.

2.  If the request fails, then wait `1 + random_number_milliseconds` seconds and retry the request.

3.  If the request fails, then wait `2 + random_number_milliseconds` seconds and retry the request.

4.  If the request fails, then wait `4 + random_number_milliseconds` seconds and retry the request.

5.  Repeat this pattern, doubling the base wait time on each retry up to the `maximum_backoff` time.

6.  Continue to wait and retry up to a maximum number of retries, without increasing the wait period beyond `maximum_backoff` .

Consider the following details for this backoff calculation:

- The wait time is `min(((2^n)+random_number_milliseconds), maximum_backoff)` , with `n` incremented by 1 for each iteration (request).

- `random_number_milliseconds` is a random number of milliseconds less than or equal to 1,000. This randomization helps avoid situations where many clients synchronize by chance and retry simultaneously, sending requests in synchronized waves. Recalculate `random_number_milliseconds` after each retry request.

- The maximum backoff interval ( `maximum_backoff` ) is typically 32 or 64 seconds. The appropriate value for `maximum_backoff` depends on your use case.

The client can continue retrying after it reaches the maximum backoff time. Retries after this point don't need to continue increasing the backoff time. For example, if the client uses a maximum backoff time of 64 seconds, then after the client reaches this value, it can continue to retry every 64 seconds. To avoid infinite retry loops, configure a maximum number of retries so that the client stops retrying after a set limit.

The wait time between retries and the number of retries depend on your use case and network conditions.

### Retry failed job insertions

If your application requires exactly-once insertion semantics, then consider how your job's [`WriteDisposition`](https://docs.cloud.google.com/bigquery/docs/reference/auditlogs/rest/Shared.Types/BigQueryAuditMetadata.WriteDisposition) handles existing data in a table (fail, overwrite, or append).

With a `WRITE_EMPTY` or `WRITE_TRUNCATE` disposition, you can achieve at-most-once semantics by retrying any failed job insertion or execution, because BigQuery atomically writes all rows that a job ingests to the table.

With a `WRITE_APPEND` disposition, specify a custom job ID so that a retry doesn't append duplicate data. Because BigQuery rejects any job creation request that reuses a previous job ID, specifying a job ID provides at-most-once semantics for that ID. You can then achieve exactly-once semantics by confirming that all previous attempts failed before retrying with a new predictable job ID.

If a transient network issue prevents your client from receiving confirmation of a job insertion, then a retry with the same job ID fails with `status=ALREADY_EXISTS` ( `code=409` and `reason="duplicate"` ). Call `jobs.get` to retrieve the status of the existing job and determine whether to create a new job with a new job ID.

## Use cases and reliability requirements

BigQuery can serve as a critical component in a variety of architectures. Depending on the use case and architecture that you deploy, you might need to meet different availability, performance, and reliability requirements. The following sections examine two common architectures and their reliability requirements.

### Real-time analytics

The first example is an event data processing pipeline. In this architecture, Pub/Sub ingests log events from endpoints, and a streaming Dataflow pipeline processes and writes the data to BigQuery by using the [BigQuery Storage Write API](https://docs.cloud.google.com/bigquery/docs/write-api) . Analysts then run ad hoc queries on the data to recreate event sequences, and near-real-time dashboards visualize the data to detect trends and patterns.

Because this workload requires high end-to-end data freshness, low ingestion *latency* is critical. After data is written to BigQuery, *reliability* depends on two factors: whether users can run ad hoc queries with *consistent* , predictable latency, and whether dashboards that use the data reflect the most recent information.

### Batch data processing

The second example is a batch processing architecture for regulatory compliance in the financial services industry. A key requirement is to deliver daily reports to regulators by a fixed nightly deadline. As long as the nightly batch process that generates the reports completes by this deadline, it meets the performance requirement.

The pipeline loads data into BigQuery and joins it with other data sources for dashboarding, analysis, and PDF report generation. Delivering these reports on time and without errors is a critical business requirement. Therefore, you must ensure *reliability* during data ingestion and generate accurate reports within a *consistent* timeframe to meet regulatory deadlines.
