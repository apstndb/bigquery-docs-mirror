# Teradata to BigQuery migration: Introduction

This document outlines the reasons you might migrate from Teradata to BigQuery, compares features between Teradata and BigQuery, and provides an outline of steps to begin your BigQuery migration.

## Why migrate from Teradata to BigQuery?

Teradata was an early innovator in managing and analyzing substantial data volumes. However, as your cloud computing needs evolve, you might require a more modern solution for your data analytics.

If you have previously used Teradata, consider migrating to BigQuery for the following reasons:

  - Overcome legacy platform constraints
      - Teradata's conventional architecture often struggles to meet the demands of modern analytics, particularly the need for unlimited concurrency and consistently high performance for diverse workloads. The serverless architecture in BigQuery is designed to handle these demands with minimal effort.
  - Adopt a cloud-native strategy
      - Many organizations are strategically moving from on-premises infrastructure to the cloud. This shift necessitates a departure from conventional, hardware-bound solutions like Teradata towards a fully managed, scalable, and on-demand service like BigQuery to reduce operational overhead.
  - Integrate with modern data sources and analytics
      - Key enterprise data increasingly resides in cloud-based sources. BigQuery is natively integrated with the Google Cloud ecosystem, providing seamless access to these sources and enabling advanced analytics, machine learning, and real-time data processing without the infrastructure limitations of Teradata.
  - Optimize cost and scalability
      - Teradata often involves complex and costly scaling processes. BigQuery offers transparent and automatic scaling of both storage and compute independently, eliminating the need for manual reconfiguration and providing a more predictable and often lower total cost of ownership.

## Feature comparison

The following table compares the features and concepts in Teradata to equivalent features in BigQuery:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Teradata Concept</th>
<th>BigQuery Equivalent</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Teradata (On-premises, Cloud, Hybrid)</td>
<td>BigQuery (Unified, AI Data Platform). BigQuery provides a large set of additional capabilities relative to a conventional data warehouse.</td>
<td>BigQuery is a fully managed, cloud-native data warehouse on Google Cloud. Teradata offers on-premises, cloud, and hybrid options. BigQuery is serverless and available on all clouds as <a href="/bigquery/docs/omni-introduction">BQ Omni.</a></td>
</tr>
<tr class="even">
<td>Teradata Tools (Teradata Studio, BTEQ)</td>
<td>Google Cloud console, BigQuery Studio, the bq command-line tool</td>
<td>Both offer interfaces for managing and interacting with the data warehouse. BigQuery Studio is web-based and integrated with Google Cloud and give ability to write SQL, Python and Apache Spark.</td>
</tr>
<tr class="odd">
<td>Databases/Schemas</td>
<td>Datasets</td>
<td>In Teradata, databases and schemas are used to organize tables and views, similar to BigQuery datasets. However, the way they're managed and used can differ.</td>
</tr>
<tr class="even">
<td>Table</td>
<td>Table</td>
<td>Both platforms use tables to store data in rows and columns.</td>
</tr>
<tr class="odd">
<td>View</td>
<td>View</td>
<td>Views function similarly in both platforms, providing a way to create virtual tables based on queries.</td>
</tr>
<tr class="even">
<td>Primary Key</td>
<td>Primary Key (unenforced in GoogleSQL)</td>
<td>BigQuery supports unenforced <a href="/bigquery/docs/primary-foreign-keys">primary keys</a> in GoogleSQL. These are primarily for helping with query optimization.</td>
</tr>
<tr class="odd">
<td>Foreign Key</td>
<td>Foreign Key (unenforced in GoogleSQL)</td>
<td>BigQuery supports unenforced <a href="/bigquery/docs/primary-foreign-keys">foreign keys</a> in GoogleSQL. These are primarily for helping with query optimization.</td>
</tr>
<tr class="even">
<td>Index</td>
<td>Clustering, Search Indexes, Vector Indexes (automatic or managed)</td>
<td>Teradata allows for explicit index creation.<br />
<br />
We recommend <a href="/bigquery/docs/clustered-tables">clustering in BigQuery</a> . While not equivalent to Database indexes, clustering helps store the data ordered on disk and this helps optimize with data retrieval when clustered columns are used as predicates.<br />
BigQuery supports <a href="/bigquery/docs/search-index">Search Indexes</a> and <a href="/bigquery/docs/vector-index">Vector Indexes</a> .</td>
</tr>
<tr class="odd">
<td>Partitioning</td>
<td>Partitioning</td>
<td>Both platforms support table partitioning for improved query performance on large tables.<br />
<br />
BigQuery only supports partitioning by dates and integers. For strings, use clustering instead.</td>
</tr>
<tr class="even">
<td>Resource allocation (based on hardware and licensing)</td>
<td>Reservations (Capacity Based), On-demand pricing (Analysis Pricing)</td>
<td>BigQuery offers flexible pricing models. Reservations provide predictable costs for consistent as well as ad hoc workloads using autoscaling, while on-demand pricing focused on per query byte-scan charges.</td>
</tr>
<tr class="odd">
<td>BTEQ, SQL Assistant, other client tools</td>
<td>BigQuery Studio, the bq command-line tool, APIs</td>
<td>BigQuery provides various interfaces for running queries, including a web-based editor, a command-line tool, and APIs for programmatic access.</td>
</tr>
<tr class="even">
<td>Query Logging/history</td>
<td>Query history, <code dir="ltr" translate="no">       INFORMATION_SCHEMA.JOBS      </code></td>
<td>BigQuery maintains a history of executed queries, allowing you to review past queries, analyze performance, and troubleshoot issues. <code dir="ltr" translate="no">       INFORMATION_SCHEMA.JOBS      </code> maintains the history of all jobs submitted in the last 6 months.</td>
</tr>
<tr class="odd">
<td>Security features (Access control, Encryption)</td>
<td>Security features (IAM, ACLs, encryption)</td>
<td>Both offer robust security. BigQuery uses Google Cloud IAM for granular access control.</td>
</tr>
<tr class="even">
<td>Network controls (Firewalls, VPNs)</td>
<td>VPC Service Controls, Private Google Access</td>
<td>BigQuery integrates with VPC Service Controls to restrict access to your BigQuery resources from specific networks. Private Google Access lets you access BigQuery without using public IPs.</td>
</tr>
<tr class="odd">
<td>User and Role Management</td>
<td>Identity and Access Management (IAM)</td>
<td>BigQuery uses IAM for fine-grained access control. You can grant specific permissions to users and service accounts at the project, dataset, and table levels.</td>
</tr>
<tr class="even">
<td>Grants and Roles on Objects</td>
<td>Access Control Lists (ACLs) on datasets and tables</td>
<td>BigQuery lets you define ACLs on datasets and tables to control access at a granular level.</td>
</tr>
<tr class="odd">
<td>Encryption at rest and in transit</td>
<td>Encryption at rest and in transit, Customer-Managed Encryption Keys (CMEK), keys can be hosted in external EKM systems.</td>
<td>BigQuery encrypts data by default. You can also manage your own encryption keys for additional control.</td>
</tr>
<tr class="even">
<td>Data governance and compliance features</td>
<td>Data governance policies, DLP (Data Loss Prevention)</td>
<td>BigQuery supports data governance policies and DLP to help you enforce data security and compliance requirements.</td>
</tr>
<tr class="odd">
<td>Teradata Load Utilities (e.g., FastLoad, MultiLoad), bteq</td>
<td>The BigQuery Data Transfer Service, the bq command-line tool, APIs</td>
<td>BigQuery provides various data loading methods. Teradata has specialized load utilities. BigQuery emphasizes scalability and speed for data ingestion.</td>
</tr>
<tr class="even">
<td>Teradata Export Utilities, bteq</td>
<td>The bq command-line tool, APIs, Export to Cloud Storage</td>
<td>BigQuery offers data export to various destinations. Teradata has its own export tools. BigQuery's integration with Cloud Storage is a key advantage.<br />
<br />
The BigQuery Storage read API provides any external compute ability to read data in bulk.</td>
</tr>
<tr class="odd">
<td>External Tables</td>
<td>External Tables</td>
<td>Both support querying data in external storage. BigQuery integrates well with Cloud Storage, Spanner, Bigtable, Cloud SQL, AWS S3, Azure Blob Storage, Google Drive.</td>
</tr>
<tr class="even">
<td>Materialized views</td>
<td>Materialized views</td>
<td>Both offer materialized views for query performance.<br />
<br />
BigQuery provides Smart Tuning materialized views that always return current data and also provide automatic query rewrite to materialized views even when the query refers to base table.</td>
</tr>
<tr class="odd">
<td>User-Defined Functions (UDFs)</td>
<td>User-Defined Functions (UDFs) (SQL, JavaScript)</td>
<td>BigQuery supports UDFs in SQL and JavaScript.</td>
</tr>
<tr class="even">
<td>Teradata Scheduler, other scheduling tools</td>
<td>Scheduled Queries, Cloud Composer, Cloud Functions, BigQuery pipelines</td>
<td>BigQuery integrates with Google Cloud scheduling services and other external scheduling tools.</td>
</tr>
<tr class="odd">
<td>Viewpoint</td>
<td>BigQuery administration for monitoring, health check, explore jobs and manage capacity.</td>
<td>BigQuery offers a UI based comprehensive administration toolbox which contains several panes to monitor operational health and resource utilisation.</td>
</tr>
<tr class="even">
<td>Backup and Recovery</td>
<td>Dataset cloning, time travel and fail safe, table snapshot and cloning, regional and multi-regional storage, cross-regional backup and recovery.</td>
<td>BigQuery offers snapshots and time travel for recovering data. Time travel is a feature that lets you access historical data within a certain timeframe. BigQuery also offers dataset cloning, regional and multi-regional storage, and cross-regional backup and recovery options.</td>
</tr>
<tr class="odd">
<td>Geospatial Functions</td>
<td>Geospatial Functions</td>
<td>Both platforms have support for geospatial data and functions.</td>
</tr>
</tbody>
</table>

## Get started

The following sections summarize the Teradata to BigQuery migration process:

### Run a migration assessment

In your Teradata to BigQuery migration, we recommend that you start by running the [BigQuery migration assessment tool](/bigquery/docs/migration-assessment) to assess the feasibility and potential benefits of moving your data warehouse from Teradata to BigQuery. This tool provides a structured approach to understanding your current Teradata environment and estimating the effort involved in a successful migration.

Running the BigQuery migration assessment tool produces an assessment report that contains the following sections:

  - Existing system report: a snapshot of the existing Teradata system and usage, including the number of databases, schemas, tables, and total size in TB. It also lists the schemas by size and points to potential sub-optimal resource utilization, like tables with no writes or few reads.
  - BigQuery steady state transformation suggestions: shows what the system will look like on BigQuery after migration. It includes suggestions for optimizing workloads on BigQuery and avoiding wastage.
  - Migration plan: provides information about the migration effort itself. For example, getting from the existing system to the BigQuery steady state. This section includes the count of queries that were automatically translated and the expected time to move each table into BigQuery.

For more information about the results of a migration assessment, see [Review the Looker Studio report](/bigquery/docs/migration-assessment#review_the_data_studio_report) .

### Migrate schema and data from Teradata

Once you've reviewed the results of your migration assessment, you can start your Teradata migration by [preparing BigQuery for the migration](/bigquery/docs/migration/teradata#before_you_begin) , then [setting up a data transfer job](/bigquery/docs/migration/teradata#set_up_a_transfer) .

For more information about the Teradata migration process, see [Migrate schema and data from Teradata](/bigquery/docs/migration/teradata) .

### Validate your migration

Once you've migrated your Teradata data to BigQuery, run the Data Validation Tool (DVT) to perform a data validation on your newly migrated BigQuery data The DVT validates various functions, from the table level to the row level, to verify that your migrated data works as intended. For more information about the DVT, see [Introducing the Data Validation Tool for EDW migrations](https://cloud.google.com/blog/products/databases/automate-data-validation-with-dvt) .

You can access the DVT in the [DVT public GitHub repository](https://github.com/GoogleCloudPlatform/professional-services-data-validator) .

## What's next

  - Try a [test migration](/bigquery/docs/migration/teradata-tutorial) of Teradata to BigQuery.
