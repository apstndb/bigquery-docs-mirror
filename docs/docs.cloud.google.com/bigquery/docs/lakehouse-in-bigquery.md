---
name: documents/docs.cloud.google.com/bigquery/docs/lakehouse-in-bigquery
uri: https://docs.cloud.google.com/bigquery/docs/lakehouse-in-bigquery
title: Interact with borderless Lakehouse data in BigQuery
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# Interact with borderless Lakehouse data in BigQuery

[Borderless Lakehouse](https://docs.cloud.google.com/lakehouse/docs/introduction) is a storage engine that unites Google Cloud and open source services to create a unified interface for advanced analytics and AI. It provides the foundation to build an open, managed, and high-performance lakehouse with automated data management and built-in governance using Apache Iceberg.

When you [create a table in Lakehouse](https://docs.cloud.google.com/lakehouse/docs/lakehouse-tables) , it is automatically queryable from BigQuery and is visible on the BigQuery page of the Google Cloud console. Your Lakehouse namespaces and schemas are also automatically mapped to BigQuery datasets. Additionally, you can create and update Lakehouse catalogs, namespaces, and tables directly in BigQuery Studio.

## Differences between Lakehouse resources and other BigQuery resources

The following are key differences between Lakehouse and standard BigQuery resources:

  - Lakehouse datasets appear in the BigQuery page of the Google Cloud console next to the water icon.
  - Lakehouse resources have additional metadata in their respective **Details** section.

### Iceberg table capabilities comparison

Use the following table to compare capabilities between Apache Iceberg tables managed by the Lakehouse runtime catalog and Apache Iceberg tables managed by BigQuery.

Capability

Apache Iceberg tables managed by Lakehouse runtime catalog

Apache Iceberg tables managed by BigQuery

**Catalog**

Lakehouse runtime catalog (Iceberg REST catalog compatible)

BigQuery

**Storage**

Cloud Storage

Cloud Storage

**Accessible through the Iceberg REST catalog endpoint**

Yes

Yes, using BigQuery catalog federation

**Read/Write Interoperability**

BigQuery read queries (SELECT, BQML, AI functions)

Supported

Supported

BigQuery DML (INSERT, UPDATE, DELETE, MERGE)

Supported (Preview)

Supported (GA)

OSS engine reads

Supported (GA)

Supported (GA) (using BigQuery catalog federation)

OSS engine writes

Supported (GA)

Not supported

OSS engine streaming writes (Kafka, Spark, Dataflow with Iceberg I/O sink)

Supported (GA)

Not supported

**Managed and Advanced Capabilities**

Table management (compaction, garbage collection)

Supported (Preview)

Supported (GA)

BigQuery streaming writes (storage write API)

Not supported

Supported (GA)

Pub/Sub streaming/subscription, Dataflow streaming with BigQuery I/O sink

Not supported

Supported (GA)

BigQuery Change Data Capture (CDC)

Not supported

Supported

BigQuery multi-statement transactions

Not supported

Supported (Preview)

Managed disaster recovery

Not supported

Not supported

Search index

Not supported

Not supported

Vector index (including auto embedding generation)

Not supported

Not supported

**Time Travel**

Time travel (using OSS engines)

Flexible (configured through table properties)

Not supported

Time travel (using BigQuery)

Limited to 7 days

Limited to 7 days

Snapshot history and rollback to previous snapshot

Supported

Not supported

**Governance, Security and Sharing**

BigQuery Authorized Views

Not supported

Not supported

BigQuery column level security

Not supported

Supported (GA)

BigQuery data masking and policy tags

Not supported

Supported (GA)

BigQuery row level security

Not supported

Not supported

Analytics Hub integration

Not supported

Supported

**Knowledge catalog capabilities**

Metadata cataloging, search and discovery

Supported

Supported

Lineage

Supported

Supported

Data quality/profiling

Supported

Supported

Insights

Supported

Supported

AI-based column and table descriptions generation

Supported

Supported

## Create a Lakehouse table in BigQuery Studio

1.  Go to the **BigQuery** page.

2.  In the **Explorer** pane, click add **Add data** .

3.  Click the **Google Cloud Storage** data source card.

4.  Under **Access external data in place** , click the **GCS data files** card.

5.  For **GCS bucket source or file path** , select your Cloud Storage bucket.

6.  For **File format** , select **Parquet** .

7.  For **Table name** , enter a name for your table.

8.  For **Project** , select your project.

9.  For **Catalog ID** , select your existing Lakehouse catalog for the bucket, or create one if it doesn't exist yet.

10. For **Namespace ID** , select an existing Lakehouse namespace, or create a new one. Namespace IDs can only contain letters, numbers, and underscores.

11. (Optional) For **Schema** , define field names and data types for your new table.

12. Click **Create table** .

Your Lakehouse table is now visible in BigQuery and can be queried and modified like a standard BigQuery table.

Instead of creating a table containing data, you can create an empty Lakehouse table in the same way that you can with [standard BigQuery tables](https://docs.cloud.google.com/bigquery/docs/tables) . The only difference is selecting a Lakehouse namespace as the target dataset.

## Migrate or federate other catalogs to Lakehouse

1.  Go to the **BigQuery** page.

2.  In the **Explorer** pane, click add **Add data** .

3.  Click the **Google Cloud Storage** data source card.

4.  Under **Access external data in place** , click the **External or legacy catalogs** card.

5.  For **Select catalog source** , select the catalog source.
    
      - If you selected **Hive Metastore** , do the following:
        1.  For **Region** , select a region for your new Lakehouse catalog.
        2.  For **Migration display name** , enter a new name for the migration.
        3.  Click **Continue** .
        4.  For **Source system configuration** , enter the URL, service account, and a network attachment.
      - If you selected a different catalog source, do the following:
        1.  For **Catalog name (in Lakehouse)** , enter a name for the catalog.
        2.  For **Data location** , select a region for your new Lakehouse catalog.
        3.  Click **Continue** .
        4.  For **Catalog configuration** , enter the remote catalog details, authentication method, and refresh interval.

6.  Click **Create** .

## Access cross-cloud data

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

> **Note:** For support during the preview, email <biglake-help@google.com> .

The [cross-cloud data access capability of Lakehouse](https://docs.cloud.google.com/lakehouse/docs/about-borderless-lakehouse) lets you query data stored with other cloud providers directly from BigQuery, without migrating files or building complex ETL pipelines. For configuration information, see [Query remote data](https://docs.cloud.google.com/lakehouse/docs/use-borderless-lakehouse) .

## What's next

  - Learn more about [borderless Lakehouse](https://docs.cloud.google.com/lakehouse/docs/lakehouse-basics) .
