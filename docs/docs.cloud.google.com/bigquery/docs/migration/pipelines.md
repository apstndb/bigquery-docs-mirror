# Migrate data pipelines

This document describes how you can migrate your upstream data pipelines, which load data into your data warehouse. You can use this document to better understand what a data pipeline is, what procedures and patterns a pipeline can employ, and which migration options and technologies are available for a data warehouse migration.

### What is a data pipeline?

In computing, a [data pipeline](https://wikipedia.org/wiki/Pipeline_\(computing\)) is a type of application that processes data through a sequence of connected processing steps. As a general concept, data pipelines can be applied, for example, to data transfer between information systems, [extract, transform, and load](https://wikipedia.org/wiki/Extract,_transform,_load) (ETL), data enrichment, and real-time data analysis. Typically, data pipelines are operated as a *batch* process that executes and processes data when run, or as a *streaming* process that executes continuously and processes data as it becomes available to the pipeline.

In the context of data warehousing, data pipelines are commonly used to read data from transactional systems, apply transformations, and then write data to the data warehouse. Each of the transformations is described by a function, and the input for any given function is the output of the previous function or functions. These connected functions are described as a graph, and this graph is often referred to as a [Directed Acyclic Graph](https://wikipedia.org/wiki/Directed_acyclic_graph) (DAG)—that is, the graph follows a direction (from source to destination), and is acyclic—the input for any function cannot be dependent on the output of another function downstream in the DAG. In other words, loops are not permitted. Each node of the graph is a function, and each edge represents the data flowing from one function to the next. The initial functions are *sources* , or connections to source data systems. The final functions are *sinks* , or connections to destination data systems.

In the context of data pipelines, sources are usually transactional systems—for example, an RDBMS—and the sink connects to a data warehouse. This type of graph is referred to as a *data flow DAG* . You can also use DAGs to orchestrate data movement between data pipelines and other systems. This usage is referred to as an *orchestration* or *control flow DAG* .

### When to migrate the data pipelines

When you migrate a [*use case*](/bigquery/docs/migration/migration-overview#use-case) to BigQuery, you can choose to [*offload*](/bigquery/docs/migration/migration-overview#offload) or [*fully migrate*](/bigquery/docs/migration/migration-overview#full-migration) .

On the one hand, when you offload a use case, you don't need to migrate its upstream data pipelines up front. You first migrate the use case schema and data from your existing data warehouse into BigQuery. You then establish an incremental copy from the old to the new data warehouse to keep the data synchronized. Finally, you migrate and validate downstream processes such as scripts, queries, dashboards, and business applications.

At this point, your upstream data pipelines are unchanged and are still writing data to your existing data warehouse. You can include the offloaded use cases in the migration backlog again to be fully migrated in a subsequent [iteration](/bigquery/docs/migration/migration-overview#migrating-using-an-iterative-approach) .

On the other hand, when you fully migrate a use case, the upstream data pipelines required for the use case are migrated to Google Cloud. Full migration requires you to offload the use case first. After the full migration, you can deprecate the corresponding legacy tables from the on-premises data warehouse because data is ingested directly into BigQuery.

During an iteration, you can choose one of the following options:

  - Offload only your use case.
  - Fully migrate a use case that was previously offloaded.
  - Fully migrate a use case from scratch by offloading it first in the same iteration.

When all of your use cases are fully migrated, you can elect to switch off the old warehouse, which is an important step for reducing overhead and costs.

### How to migrate the data pipelines

The rest of this document addresses how to migrate your data pipelines, including which approach and procedures to use and which technologies to employ. Options range from repurposing existing data pipelines (redirecting them to load to BigQuery) to rewriting the data pipelines in order to take advantage of Google Cloud-managed services.

## Procedures and patterns for data pipelines

You can use data pipelines to execute a number of procedures and patterns. These pipelines are the most commonly used in data warehousing. You might have *batch data* pipelines or *streaming* data pipelines. Batch data pipelines run on data collected over a period of time (for example, once a day). Streaming data pipelines handle real-time events being generated by your operational systems—for example, in [CDC](#cdc) row changes being generated by your Online Transaction Processing (OLTP) databases.

### Extract, transform, and load (ETL)

In the context of data warehousing, data pipelines often execute an extract, transform, and load (ETL) procedure. ETL technologies run outside of the data warehouse, which means the resources of the data warehouse can be used primarily for concurrent querying, instead of for preparing and transforming data. One downside of the transformation being executed outside of the data warehouse is that it requires you to learn additional tooling and languages (other than SQL) to express the transformations.

The following diagram shows a typical ETL procedure.

**Figure 1** . A typical ETL procedure.

**Note:** The arrows denote the direction of data flow; the sources within the DAG typically pull their data from the source systems.

A typical ETL data pipeline pulls data from one or more source systems (preferably, as few as possible to avoid failures caused by issues like unavailable systems). The pipeline then performs a series of transformations, including cleaning data, applying business rules to it, checking for data integrity, and create aggregates or disaggregates. For more information, see [Real-life ETL cycle](https://wikipedia.org/wiki/Extract,_transform,_load#Real-life_ETL_cycle) .

It's common to have multiple data pipelines. The first pipeline focuses on copying data from the source system to the data warehouse. Subsequent pipelines apply business logic and transform the data for use in various [data marts](https://wikipedia.org/wiki/Data_mart) , which are subsets of the data warehouse focused on a specific business unit or business focus.

When you have multiple data pipelines, you need to [orchestrate](#orchestration_and_scheduling) them. The following diagram shows what this orchestration process might look like.

**Figure 2** . Orchestration process for multiple data pipelines.

In the diagram, each data pipeline is considered a sub-DAG of the orchestration DAG. Each orchestration DAG encompasses several data pipelines to align with the larger objective, for example, preparing data for a business unit so that business analysts can run their dashboards or reports.

### Extract, load, and transform (ELT)

ELT is an alternative to ETL. With ELT, the data pipeline is split into two parts. First, an ELT technology extracts the data from the source system and loads it into the data warehouse. Second, SQL scripts on top of the data warehouse perform the transformations. The upside of this approach is that you can use SQL to express the transformations; the downside is that this might consume data warehouse resources that are needed for concurrent querying. For this reason, ELT batches often run during the night (or off-peak) when the data warehouse's system resources are in lesser demand.

The following diagram shows a typical ELT procedure.

**Figure 3** . A typical ELT procedure.

When you adopt an ELT approach, it's common to separate the extract and load into one DAG and the transformations into their own DAGs. Data is loaded into the data warehouse once and then transformed multiple times to create the different tables that are used downstream in reporting and so on. These DAGs in turn become sub-DAGs in a larger orchestration DAG (as shown in the [ETL section](#etl) ).

When you migrate data pipelines from a congested on-premises data warehouse to the cloud, it's important to remember that cloud data warehouse systems such as BigQuery are massively parallel data processing technologies. In fact, in the case of BigQuery, you can buy more resources to support both increasing demands for ELT and concurrent querying. For more information, see the [Introduction to optimizing query performance](/bigquery/docs/best-practices-performance-overview) .

### Extract and load (EL)

You can use the extract and load (EL) procedure on its own or followed by transformations, in which case it becomes ELT. EL is mentioned separately because several automated services are available that perform this task, mitigating the need for you to create your own ingestion data pipeline. For more details, see [What is BigQuery Data Transfer Service?](/bigquery/docs/dts-introduction) .

### Change data capture (CDC)

Change data capture ( [CDC](https://wikipedia.org/wiki/Change_data_capture) ) is one of several software design patterns used to track data changes. It's often used in data warehousing because the data warehouse is used to collate and track data and its changes from various source systems over time.

The following diagram shows an example of how CDC works with ELT.

**Figure 4** . How CDC works with ELT.

CDC works well with ELT because you want to store the original record before making any changes downstream.

To make the EL part happen, you can process database logs by using CDC software such as [Datastream](/datastream) or open source tools like [Debezium](https://debezium.io/) and writing the records to BigQuery using [Dataflow](/dataflow) . Then you can use a SQL query to determine the latest version before you apply further transformations. Here's an example:

``` text
WITH ranked AS (
  SELECT
    *,
    ROW_NUMBER() OVER (
      PARTITION BY RECORD KEY
      ORDER BY EVENT TIMESTAMP DESC
    ) AS rank
  FROM TABLE NAME
)
SELECT *
FROM ranked
WHERE rank = 1
```

When you are refactoring or creating new data pipelines, consider using the CDC pattern applied as an ELT procedure. This approach ensures that you have a complete history of data changes upstream and provides a good segregation of responsibilities—for example:

  - Source system teams ensure availability of their logs and publication of their data events.
  - The data platform team ensures that ingestion collation of the original records includes timestamps in the data warehouse.
  - Data engineering and analyst teams schedule a series of transformations to populate their data marts.

### Feedback loops with operational data pipelines

*Operational data pipelines* are data processing pipelines that take data from the data warehouse, transform it if needed, and write the result into *operational systems* .

[Operational systems](https://wikipedia.org/wiki/Operational_system) refer to systems that process the organization's day-to-day transactions, such as OLTP databases, Customer Relationship Management (CRM) systems, Product Catalog Management (PCM) systems, and so on. Because these systems often act as a source of data, the operational data pipelines implement a *feedback loop pattern* .

The operational data pipeline pattern is shown in the following diagram.

**Figure 5** . Pattern for an operational data pipeline.

The following example describes an operational data pipeline that writes product prices into a PCM system. A PCM system is the authoritative system for sales-related product information such as colors, sales channels, price, and seasonality. Here's the end-to-end flow of data:

  - Price-related data is available from multiple sources. This data can include the current price by region from the PCM, competitor pricing from a third-party service, demand forecasting and supplier reliability from internal systems, and so on.
  - An ETL pipeline pulls the data from the sources, transforms it, and writes the result into the data warehouse. The transformation in this case is a complex calculation involving all the sources with the goal of producing an optimal base price for each product in the PCM.
  - Finally, the operational pipeline takes the base prices from the data warehouse, performs light transformations to adjust the prices for seasonal events and writes the final prices back into the PCM.

**Figure 6** . An operational data pipeline that writes product prices into a PCM system.

An operational data pipeline is a type of downstream process, whereas data pipelines implementing [ETL](#etl) , [ELT](#elt) , or [CDC](#cdc) are upstream processes. Nevertheless, the tools used to implement both can overlap. For instance, you can use [Dataflow](/dataflow) to define and run all the data processing DAGs, [GoogleSQL](/bigquery/docs/reference/standard-sql) to define transformations that execute within BigQuery, and [Cloud Composer](/composer) to orchestrate the end-to-end flow of data.

## Choosing a migration approach

This section describes different approaches you can adopt to migrate your data pipelines.

### Redirect data pipelines to write to BigQuery

In the following conditions, you might consider whether a technology that you use offers a built-in BigQuery sink (write connector):

  - The legacy data warehouse is fed by data pipelines executing an [ETL](#etl) procedure.
  - The transformation logic is executed before the data is stored in the data warehouse.

Independent software vendors (ISV) offer data processing technologies with BigQuery connectors, including the following:

  - Informatica: [BigQuery connector guide](https://docs.informatica.com/integration-cloud/data-integration-connectors/current-version/google-bigquery-connectors/preface.html)
  - Talend: [Writing data in BigQuery](https://help.qlik.com/talend/en-US/components/8.0/google-bigquery/tbigqueryoutput-trowgenerator-tmysqlinput-tmap-writing-data-in-google-bigquery-standard-component-this)

**Note:** It's important to check that the data processing software takes advantage of the BigQuery large-scale [ingestion mechanisms](/bigquery/docs/loading-data) , such as streaming inserts or batch loads from Cloud Storage. An approach that employs the [Magnitude Simba](https://www.simba.com) [JDBC](https://wikipedia.org/wiki/Java_Database_Connectivity) or [ODBC](https://wikipedia.org/wiki/Open_Database_Connectivity) BigQuery drivers isn't suitable for large-scale ingestion operations, because these drivers implement the query interface. While the drivers can perform inserts, this interface is intended for querying and data manipulation language (DML) statements on BigQuery, not for large-scale inserts or updates.

If the data pipeline technology doesn't support data ingestion to BigQuery, consider using a [variation on this approach](#intermediate-vehicle) that writes the data temporarily to files that are subsequently ingested by BigQuery.

**Figure 7** . Rewriting, or reconfiguring, the last function of a data pipeline to write data to BigQuery.

At a high level, the work involved concerns rewriting, or reconfiguring, the last function of the data pipeline to write data to BigQuery. However, you face a number of options that might require additional changes or new work, for example:

**Functional**

  - Data mappings: Given that the target database table schema might change, you might need to reconfigure these mappings.
  - Metric validation: You must validate both historic and new reports, because both the schema and the queries might change.

**Nonfunctional**

  - Firewalls might need to be configured to allow outbound data transfer from on-premises to BigQuery.
  - Network changes might be required to create additional bandwidth, to accommodate outbound data transfer.

### Redirect data pipelines by using files as an intermediate vehicle

When the existing on-premises data pipeline technology doesn't support Google APIs, or if you are restricted from using Google APIs, you can use files as an intermediate vehicle for your data to reach BigQuery.

This approach is similar to the redirect approach, but instead of using a native sink that can write to BigQuery, you use a sink that can write to an on-premises file system. When your data is in your file system, you copy the files to Cloud Storage. For more details, see the [overview of the ingest options for Cloud Storage](/solutions/transferring-big-data-sets-to-gcp) and the criteria that are involved in choosing an ingest option.

The final step is to load the data from Cloud Storage into BigQuery following the guidelines in [Batch loading data](/bigquery/docs/loading-data-cloud-storage) .

The following diagram shows the approach outlined in this section.

**Figure 8** . Redirecting data pipelines by using files as an intermediate vehicle.

With respect to the orchestration of the ETL pipeline, you need to perform two separate steps:

1.  Reuse your existing on-premises pipeline orchestration to write the transformed data into the file system. Extend this orchestration to copy the files from your on-premises file system into Cloud Storage, or create an additional script that runs regularly to perform the copy step.
2.  When the data is in Cloud Storage, use a [Cloud Storage transfer](/bigquery/docs/cloud-storage-transfer) to schedule recurring loads from Cloud Storage to BigQuery. Alternatives to Cloud Storage transfers are [Cloud Storage triggers](/functions/docs/calling/storage) and [Cloud Composer](/composer) .

In Figure 8, note how it's also possible for the orchestration on Google Cloud to use a pull model by retrieving the files using a protocol such as [SFTP](https://wikipedia.org/wiki/SSH_File_Transfer_Protocol) .

### Migrate existing ELT pipelines to BigQuery

ELT pipelines consist of two parts: the part that loads the data into your data warehouse, and the part that transforms the data by using SQL so it can be consumed downstream. When you migrate ELT pipelines, each of these parts has its own approach for migration.

For the part that loads data into your data warehouse (the EL part), you can follow the guidelines in the [redirect data pipelines](#redirect_data_pipelines_to_write_to_bigquery) section, minus the advice on transformations, which are not part of an EL pipeline.

If your data sources are supported by the [BigQuery Data Transfer Service](/bigquery/docs/dts-introduction) (DTS) either [directly](/bigquery/docs/dts-introduction#supported_data_sources) or through [third-party integrations](/bigquery/docs/third-party-transfer) , you can use DTS to replace your EL pipeline.

### Migrating existing OSS data pipelines to Dataproc

When you migrate your data pipeline to Google Cloud, you might want to migrate some legacy jobs that are written with an open source software framework like [Apache Hadoop](https://hadoop.apache.org/) , [Apache Spark](https://spark.apache.org/) , or [Apache Flink](https://flink.apache.org/) .

[Dataproc](/dataproc) lets you deploy fast, easy-to-use, fully managed Hadoop and Spark clusters in a simple, cost-efficient way. Dataproc integrates with the [BigQuery connector](/dataproc/docs/concepts/connectors/bigquery) , a Java library that enables Hadoop and Spark to directly write data to BigQuery by using abstracted versions of the Apache Hadoop [InputFormat](http://hadoop.apache.org/docs/current/api/org/apache/hadoop/mapreduce/InputFormat.html) and [OutputFormat](http://hadoop.apache.org/docs/current/api/org/apache/hadoop/mapreduce/OutputFormat.html) classes.

Dataproc makes it easy to create and delete clusters so that instead of using one monolithic cluster, you can use many ephemeral clusters. This approach has several advantages:

  - You can use different cluster configurations for individual jobs, eliminating the administrative burden of managing tools across jobs.
  - You can scale clusters to suit individual jobs or groups of jobs.
  - You pay only for resources when your jobs are using them.
  - You don't need to maintain clusters over time, because they are freshly configured every time you use them.
  - You don't need to maintain separate infrastructure for development, testing, and production. You can use the same definitions to create as many different versions of a cluster as you need when you need them.

When you migrate your jobs, we recommend that you take an incremental approach. By migrating incrementally, you can do the following:

  - Isolate individual jobs in your existing Hadoop infrastructure from the complexity that's inherent in a mature environment.
  - Examine each job in isolation to evaluate its needs and to determine the best path for migration.
  - Handle unexpected problems as they arise without delaying dependent tasks.
  - Create a proof of concept for each complex process without affecting your production environment.
  - Move your jobs to the recommended ephemeral model thoughtfully and deliberately.

When you migrate your existing Hadoop and Spark jobs to Dataproc, you can check that your jobs' dependencies are covered by the supported [Dataproc versions](/dataproc/docs/concepts/versioning/dataproc-versions) . If you need to install custom software, you might consider [creating your own Dataproc image](/dataproc/docs/guides/dataproc-images) , using some of the available [initialization actions](/dataproc/docs/concepts/configuring-clusters/init-actions) (for example, for [Apache Flink](https://github.com/GoogleCloudDataproc/initialization-actions/tree/master/flink) ), writing your own initialization action, or [specifying custom Python package requirements](/dataproc/docs/tutorials/python-configuration) .

To get started, see the Dataproc [quickstart guides](/dataproc/docs/quickstarts) and the [BigQuery connector code samples](/dataproc/docs/examples/bigquery-example) .

### Rehost third-party data pipelines to run on Google Cloud

A common scenario when building data pipelines on-premises is to use third-party software to manage execution of the pipeline and allocation of computing resources.

To move these pipelines to the cloud, you have several alternatives, depending on the capabilities of the software that you are using, and also depending on your licensing, support, and maintenance terms.

The following sections present some of these alternatives.

At a high level, you have the following alternatives for executing your third-party software in Google Cloud, from least to most complex:

  - Your software vendor has partnered with Google Cloud to offer their software in [Google Cloud Marketplace](/marketplace) .
  - Your third-party software vendor can run on [Kubernetes](https://kubernetes.io/) .
  - Your third-party software runs on one or more virtual machines (VMs).

If your third-party software provides a Cloud Marketplace solution, the work involved is as follows:

  - Deploy your third-party software from the [Cloud Marketplace console](https://console.cloud.google.com/marketplace/browse?filter=category:big-data) .
  - Select and migrate your use cases following the iterative approach explained in [Migrating using an iterative approach](/bigquery/docs/migration/migration-overview#migrating-using-an-iterative-approach) .

This alternative is the simplest because you onboard your data pipelines to the cloud using the familiar platform provided by your vendor. You might also be able to use proprietary tools from your vendor to facilitate migration between your original environment and your new environment on Google Cloud.

If your vendor doesn't provide a Cloud Marketplace solution, but their product is able to run on top of Kubernetes, you can use [Google Kubernetes Engine](/kubernetes-engine) (GKE) to host your pipelines. The following work is involved:

  - [Create a GKE cluster](/kubernetes-engine/docs/how-to/creating-a-cluster) by following the recommendations from your vendor to make sure that the third-party product can take advantage of the task parallelization that Kubernetes offers.
  - Install your third-party software on your GKE cluster by following the vendor recommendations.
  - Select and migrate your use cases by following the iterative approach explained in [Migrating data warehouses to BigQuery: Overview](/bigquery/docs/migration/migration-overview) .

This alternative provides a middle ground in terms of complexity. It takes advantage of your vendor-native support for Kubernetes in order to scale and parallelize the execution of your pipelines. However, it requires you to create and manage a GKE cluster.

If your vendor doesn't support Kubernetes, you must install their software on a pool of VMs to enable scaling out and parallelizing the work. If your vendor software natively supports the distribution of work to several VMs, use those provided facilities, possibly grouping the VM instances in a [managed instance group](/compute/docs/instance-groups) (MIG) for scaling in and out as required.

Handling the parallelization of the work is nontrivial. If your vendor doesn't provide capabilities for distributing tasks to different VMs, we recommend using a task-farming pattern to distribute work to VMs in a MIG. The following diagram illustrates this approach.

**Figure 9** . A managed instance group (MIG) with three VMs.

In this diagram, each VM in the MIG executes the third-party pipeline software. You can trigger a pipeline execution in several ways:

  - Automatically, by using [Cloud Scheduler](/scheduler) , [Cloud Composer](/composer) , or a [Cloud Storage trigger](/functions/docs/calling/storage) when new data arrives into a Cloud Storage bucket.
  - Programmatically, by calling a [Cloud Endpoint](/endpoints) or [Cloud Function](/functions) , or by using the [Pub/Sub API](/pubsub/docs/apis) .
  - Manually, by placing a new message in a Pub/Sub topic with the Google Cloud CLI.

In essence, all of these methods send a message to a predefined [Pub/Sub topic](/pubsub/architecture#the_basics_of_a_publishsubscribe_service) . You create a simple agent to be installed in each VM. The agent listens to the one or more Pub/Sub topics. Whenever a message arrives in the topic, the agent pulls the message from the topic, starts a pipeline in your third-party software, and listens for its completion. When the pipeline is completed, the agent retrieves the next message from the topics it's listening to.

In all scenarios, we recommend that you work with your vendor to comply with the appropriate licensing terms for your pipelines to work on Google Cloud.

### Rewrite data pipelines to use Google Cloud-managed services

In some cases, you might elect to rewrite some of your existing data pipelines to use new frameworks and services that are fully managed on Google Cloud. This option works well if your existing pipelines were originally implemented with technologies that are now deprecated, or if you anticipate that porting and continuing to maintain those pipelines unmodified in the cloud would be too impractical or cost prohibitive.

The following sections present fully managed Google Cloud services that let you perform advanced data transformations at scale: Cloud Data Fusion and Dataflow.

#### Cloud Data Fusion

[Cloud Data Fusion](/data-fusion) , which is built on the open source [CDAP](https://cdap.io/) project, is a fully managed data integration service for building and managing data pipelines through a graphical interface.

You develop the data pipelines in the Cloud Data Fusion UI by connecting sources to transformations, sinks, and other nodes to form a DAG. When you deploy your data pipeline, the Cloud Data Fusion planner transforms this DAG into a series of parallel computations which will be executed as an Apache Spark job on [Dataproc](/dataproc) .

When using Cloud Data Fusion, you can connect to a source system's database by using the Java Database Connectivity (JDBC) drivers to read data, transform it, and load it into a destination of your choice (for example, BigQuery), without having to write any code. To do this, you need to upload a JDBC driver to your Cloud Data Fusion instance and configure it so that you can use it in your data pipelines. For more details, see the guide on [using JDBC drivers with Cloud Data Fusion](/data-fusion/docs/how-to/using-jdbc-drivers) .

Cloud Data Fusion exposes plugins for sources, transforms, aggregates, sinks, error collectors, alert publishers, actions, and post-run actions as customizable components. Prebuilt plugins offer access to a wide range of data sources. If a plugin doesn't exist, you can build your own plugin by using the Cloud Data Fusion plugin APIs. For more information, see the [Plugin overview](/data-fusion/docs/concepts/overview#plugin) .

With Cloud Data Fusion pipelines, you can create both batch and streaming data pipelines. By providing access to logs and metrics, data pipelines also offer ways for administrators to operationalize their data processing workflows without needing custom tooling.

To get started, see the [Cloud Data Fusion conceptual overview](/data-fusion/docs/concepts/overview) . For practical examples, see the [quickstart guide](/data-fusion/docs/create-data-pipeline) and the tutorial on creating a [targeting campaign pipeline](/data-fusion/docs/tutorials/targeting-campaign-pipeline) .

#### Dataflow

[Dataflow](/dataflow) is a fully managed service for running [Apache Beam](https://beam.apache.org/) jobs at scale. Apache Beam is an open source framework that provides a rich set of windowing and session-analysis primitives as well as an ecosystem of source and sink connectors, including a [connector for BigQuery](https://beam.apache.org/documentation/io/built-in/google-bigquery/) . Apache Beam lets you transform and enrich data both in stream (real time) and batch (historical) modes with equal reliability and expressiveness.

The serverless approach of Dataflow removes operational overhead with performance, scaling, availability, security, and compliance handled automatically. This lets you focus on programming instead of managing server clusters.

You can submit Dataflow jobs in different ways, either through the [command-line interface](/dataflow/docs/guides/using-command-line-intf) , the [Java SDK](https://beam.apache.org/documentation/sdks/java/) , or the [Python SDK](https://beam.apache.org/documentation/sdks/python/) . Also, we are developing a [portability framework](https://beam.apache.org/roadmap/portability/) to bring full interoperability between all SDKs and [runners](https://beam.apache.org/documentation/runners/capability-matrix/) .

If you want to migrate your data queries and pipelines from other frameworks to Apache Beam and Dataflow, read about the [Apache Beam programming model](/dataflow/docs/concepts/beam-programming-model) and browse the official [Dataflow documentation](/dataflow/docs) .

For practical examples, see the Dataflow [quickstarts](/dataflow/docs/quickstarts) and [tutorials](/dataflow/docs/samples) .

## Orchestration and scheduling

At a high level, *orchestration* is the automated coordination of several systems, whereas *scheduling* refers to the automated triggering of orchestration work.

  - Zooming in: A data pipeline is in itself an orchestration of data transformations described by a DAG, which is a *data processing DAG* .
  - Zooming out: When a data pipeline depends on the output of other data pipelines, you need orchestration of multiple pipelines. Each pipeline constitutes a sub-DAG in a larger DAG, which is an *orchestration DAG* .

This setup is typical in data warehousing. Figure 1 in the [ETL section](#etl) shows an example setup. The following sections focus on the orchestration of several data pipelines.

### Dependencies

Dependencies can be *fan-in* , where multiple data pipelines merge into a vertex of an orchestration DAG; *fan-out* , where a single data pipeline triggers multiple others; or often both, as shown in the following diagram.

**Figure 10** . Fan-in and fan-out dependencies used in combination.

In suboptimal environments, some dependencies are a result of limitations in the amount of available resources. For example, a data pipeline runs and produces some common data as a byproduct. Other data pipelines depend on this common data simply to avoid recalculating it, but are unrelated to the data pipeline that created the data. If this first pipeline encounters any functional or nonfunctional issues, failures cascade down to its dependent data pipelines—at best, forcing them to wait, or at worst, preventing them from running at all, as shown in the following diagram.

**Figure 11** . Failures cascading down a data pipeline prevent dependent pipelines from running.

In Google Cloud, a wealth of compute resources and specialized tools are available to allow you to optimize the execution of your pipelines and their orchestration. The remaining sections discuss these resources and tools.

### Migration work involved

It's a best practice to simplify your orchestration needs. Your orchestration increases in complexity with the number of dependencies between your data pipelines. Migrating to Google Cloud presents an opportunity to examine your orchestration DAGs, identify your dependencies, and determine how to optimize those dependencies.

We recommend optimizing your dependencies incrementally, as follows:

1.  In a first iteration, move your orchestration as is to Google Cloud.
2.  In later iterations, analyze your dependencies and parallelize them if feasible.
3.  Finally, reorganize your orchestration by extracting common tasks into their own DAGs.

The next section explains this method with a practical example.

### A practical example

Suppose that an organization has two related pipelines:

  - The first pipeline calculates the profits and losses (P\&L) for the whole organization. It's a complex pipeline involving many transformations. Part of the pipeline consists of calculating the monthly sales, which are used in subsequent transformation steps and eventually written to a table.
  - The second pipeline calculates the year-over-year and month-over-month sales growth for different products so that the marketing department can tune its ad campaign efforts. This pipeline needs the monthly sales data previously calculated by the P\&L data pipeline.

The organization considers the P\&L data pipeline to have higher priority than the marketing pipeline. Unfortunately, because P\&L is a complex data pipeline, it consumes a large amount of resources, preventing other pipelines from running concurrently. In addition, if the P\&L pipeline fails, the marketing pipeline and other dependent pipelines don't have the required data to be able to run, and must wait for a retry of P\&L. The following diagram illustrates this situation.

**Figure 12** . Complex data pipelines can prevent lower-priority pipelines from running.

The organization is migrating to BigQuery. It has identified the two use cases—P\&L and marketing sales growth—and included them in the migration backlog. When planning the next iteration, the organization [prioritizes](/bigquery/docs/migration/migration-overview#prioritizing-use-cases) the P\&L use case and [includes it in the iteration backlog](/bigquery/docs/migration/migration-overview#execute) because it's severely limited by the current on-premises resources and regularly causes delays. Some of its dependent use cases are also included, among them the marketing use case.

The migration team runs the first iteration. They choose to move both the P\&L and marketing use cases to Google Cloud by using a [redirect approach](#redirect_data_pipelines_to_write_to_bigquery) . They make no changes to the pipeline steps or orchestration. An important difference is that now the P\&L pipeline can dispose almost unlimited compute power, and therefore executes much faster than on-premises. The pipeline writes the sales monthly data to a BigQuery table that the marketing growth pipeline uses. The following diagram illustrates these changes.

**Figure 13** . Speeding up a complex data pipeline by using a redirect approach.

Although Google Cloud has helped with the nonfunctional P\&L issues, functional issues still remain. Some unrelated tasks that precede the calculation of the monthly sales often cause errors that prevent that calculation from happening, and result in the dependent pipelines being unable to start.

In a second iteration, the team hopes to improve performance by including both use cases in the iteration backlog. The team identifies the pipeline steps to calculate the monthly sales in the P\&L pipeline. The steps constitute a sub-DAG, as shown in the next diagram. The migration team copies the sub-DAG into the marketing pipeline so that that pipeline can run independently of P\&L. Having sufficient computing power in Google Cloud enables both pipelines to run concurrently.

**Figure 14** . Pipelines running concurrently by using a sub-DAG.

The downside is that duplicating the sub-DAG logic creates code management overhead, because now the team needs to keep both copies of the sub-DAG logic in sync.

In a third iteration, the team revisits the use cases and extracts the monthly sales sub-DAG into an independent pipeline. When the new monthly sales pipeline is done, it triggers or fans out into the P\&L, marketing growth, and other dependent pipelines. This configuration creates a new overall orchestration DAG, with each of the pipelines being one of its sub-DAGs.

**Figure 15** . Overall orchestration DAG with each pipeline in its own sub-DAG.

In subsequent iterations, the migration team can solve any remaining functional issues and migrate the pipelines to use the following [Google Cloud-managed services](#rewrite_data_pipelines_to_use_gcp-managed_services) , among others:

  - [Dataflow](/dataflow) : Enables you to define each data pipeline as a self-contained DAG using the [Beam model](https://beam.apache.org/documentation/execution-model/) .
  - [Cloud Composer](/composer) : Enables you to define the broader orchestration as one or more [Airflow DAGs](https://airflow.apache.org/concepts.html#dags) .

Even though Airflow supports sub-DAGs natively, this functionality might limit its performance and is therefore [discouraged](/composer/docs/faq#using_operators) . In their place, use independent DAGs with the [`  TriggerDagRunOperator  `](https://github.com/apache/airflow/blob/main/providers/src/airflow/providers/standard/operators/trigger_dagrun.py) operator.

## What's next

Learn more about the following steps in data warehouse migration:

  - [Migration overview](/bigquery/docs/migration/migration-overview)
  - [Migration assessment](/bigquery/docs/migration-assessment)
  - [Schema and data transfer overview](/bigquery/docs/migration/schema-data-overview)
  - [Batch SQL translation](/bigquery/docs/batch-sql-translator)
  - [Interactive SQL translation](/bigquery/docs/interactive-sql-translator)
  - [Data security and governance](/bigquery/docs/data-governance)
  - [Data validation tool](https://github.com/GoogleCloudPlatform/professional-services-data-validator#data-validation-tool)

You can also learn about moving from specific data warehouse technologies to BigQuery:

  - [Migrating from Netezza](/architecture/dw2bq/netezza/netezza-bq-migration-guide)
  - [Migrating from Oracle](/bigquery/docs/migration/oracle-migration)
  - [Migrating from Amazon Redshift](/bigquery/docs/migration/redshift-overview)
  - [Migrating from Teradata](/bigquery/docs/migration/teradata-overview)
  - [Migrating from Snowflake](/architecture/dw2bq/snowflake/snowflake-bq-migration-guide)
