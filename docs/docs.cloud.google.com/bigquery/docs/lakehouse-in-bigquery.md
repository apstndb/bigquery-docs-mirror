---
name: documents/docs.cloud.google.com/bigquery/docs/lakehouse-in-bigquery
uri: https://docs.cloud.google.com/bigquery/docs/lakehouse-in-bigquery
title: Interact with borderless Lakehouse data in BigQuery
description: Introduction to Lakehouse tables and how they work in BigQuery.
data_source: docs.cloud.google.com
---

# Interact with borderless Lakehouse data in BigQuery

[Borderless Lakehouse](https://docs.cloud.google.com/lakehouse/docs/introduction) is a storage engine that unites Google Cloud and open source services to create a unified interface for advanced analytics and AI. It provides the foundation to build an open, managed, and high-performance lakehouse with automated data management and built-in governance using Apache Iceberg.

When you [create a table in Lakehouse](https://docs.cloud.google.com/lakehouse/docs/lakehouse-tables) , it is automatically queryable from BigQuery and is visible on the BigQuery page of the Google Cloud console. Your Lakehouse namespaces and schemas are also automatically mapped to BigQuery datasets. Additionally, you can create and update Lakehouse catalogs, namespaces, and tables directly in BigQuery Studio.

## Differences between Lakehouse resources and other BigQuery resources

The following are key differences between Lakehouse and standard BigQuery resources:

- Lakehouse datasets appear in the BigQuery page of the Google Cloud console next to the water icon.
- Lakehouse resources have additional metadata in their respective **Details** section.

## Create a Lakehouse table in BigQuery Studio

1.  Go to the **BigQuery** page.

2.  In the **Data** pane, click **Add data** .

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

2.  In the **Data** pane, click **Add data** .

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

The [cross-cloud data access capability of Lakehouse](https://docs.cloud.google.com/lakehouse/docs/about-cross-cloud-data-access) lets you query external Iceberg tables across Amazon Web Services (AWS) and Microsoft Azure directly from BigQuery without migrating files or building ETL pipelines. You can route query reads, background metadata refresh, or both privately over Cross-Cloud Interconnect, while optional local caching in Google Cloud helps reduce recurring egress costs. For query syntax and configuration details, see [Query remote data](https://docs.cloud.google.com/lakehouse/docs/query-remote-data) .

## Row-level and column-level security

Apache Iceberg tables managed by the Lakehouse runtime catalog natively support BigQuery [row-level security](https://docs.cloud.google.com/bigquery/docs/managing-row-level-security) (row-level access policies) and [column-level security with dynamic data masking](https://docs.cloud.google.com/bigquery/docs/column-data-masking#data-policies-on-column) (data policies applied directly to columns):

- **SQL DDL binding with four-part identifiers** : You create and drop row-level access policies, and you attach, update, and detach column data policies, by using GoogleSQL DDL statements. These statements reference the four-part **P.C.N.T** ( `PROJECT_ID `` . `` CATALOG_ID `` . `` NAMESPACE `` . `` TABLE_NAME` ) table identifier. Supported DDL statements include `CREATE TABLE` , `ALTER TABLE ... ADD COLUMN` , `ALTER TABLE ... ALTER COLUMN ... SET OPTIONS` , `CREATE ROW ACCESS POLICY` , `CREATE OR REPLACE ROW ACCESS POLICY` , `DROP ROW ACCESS POLICY` , and `DROP ALL ROW ACCESS POLICIES` . To bind policies to a table, you need `biglake.*` Identity and Access Management (IAM) permissions ( `biglake.tables.setColumnDataPolicy` and `biglake.rowAccessPolicies.*` ), which are included in the BigLake Admin role ( `roles/biglake.admin` ). You also need BigQuery data policy permissions ( `bigquery.dataPolicies.*` ).
- **Important limitations** :
  - **SQL DDL only** : You can attach and manage policies on Apache Iceberg tables in the Lakehouse runtime catalog only through GoogleSQL DDL. The Google Cloud console, the BigQuery API `tables.patch` method, the bq command-line tool, and Terraform aren't supported.
  - **Credential vending guardrail** : On catalogs that use [credential vending mode](https://docs.cloud.google.com/lakehouse/docs/credential-vending) , the Apache Iceberg REST catalog endpoint returns a `403 Forbidden` HTTP status code for Cloud Storage credential requests on tables protected by fine-grained access control (FGAC). To obtain vended credentials, the calling principal must have unmasked ( `RAW_DATA_ACCESS_POLICY` ) access to every protected column and, if the table has row-level access policies, unfiltered row access ( `FILTER USING (TRUE)` ).
  - **Policy tags and data governance tags aren't supported** : Data Catalog policy tags (and taxonomies) and Resource Manager data governance tags aren't supported on Apache Iceberg tables in the Lakehouse runtime catalog. Apply data policies directly to columns instead.
  - **Subqueries in row-level access policies aren't supported** : Row-level access policies on Apache Iceberg tables in the Lakehouse runtime catalog don't support subqueries in the `FILTER USING` expression.
  - **Federated catalogs aren't supported** : FGAC (row-level security and column-level data policies) isn't supported on external or federated catalog tables accessed through [cross-cloud connections](https://docs.cloud.google.com/lakehouse/docs/about-cross-cloud-data-access) .

For step-by-step instructions and SQL examples, see [Row-level and column-level security](https://docs.cloud.google.com/lakehouse/docs/fine-grained-access-control) .

## Iceberg table capabilities comparison

Use the following table to compare capabilities between Apache Iceberg tables managed by the Lakehouse runtime catalog and Apache Iceberg tables managed by BigQuery.

| Capability                                                                                                                              | Apache Iceberg tables managed by Lakehouse runtime catalog                                               | Apache Iceberg tables managed by BigQuery |
|-----------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|-------------------------------------------|
| **Catalog**                                                                                                                             | Lakehouse runtime catalog (Iceberg REST catalog compatible)                                              | BigQuery                                  |
| **Storage**                                                                                                                             | Cloud Storage                                                                                            | Cloud Storage                             |
| **Accessible through the Apache Iceberg REST catalog endpoint**                                                                         | Yes                                                                                                      | Yes (read-only)                           |
| **Read/write interoperability**                                                                                                         |                                                                                                          |                                           |
| BigQuery read queries ( `SELECT` , BigQuery ML, AI functions)                                                                           | Supported                                                                                                | Supported                                 |
| BigQuery DML (INSERT, UPDATE, DELETE, MERGE)                                                                                            | Supported (Preview)                                                                                      | Supported (GA)                            |
| OSS engine reads                                                                                                                        | Supported (GA)                                                                                           | Supported (GA)                            |
| OSS engine writes                                                                                                                       | Supported (GA)                                                                                           | Not supported                             |
| OSS engine streaming writes (Apache Kafka, Apache Spark, Dataflow with Iceberg I/O sink)                                                | Supported (GA)                                                                                           | Not supported                             |
| **Managed and advanced capabilities**                                                                                                   |                                                                                                          |                                           |
| Table management (compaction, garbage collection)                                                                                       | Supported (Preview)                                                                                      | Supported (GA)                            |
| BigQuery streaming writes (Storage Write API)                                                                                           | Not supported                                                                                            | Supported (GA)                            |
| Pub/Sub streaming and subscriptions, Dataflow streaming with BigQuery I/O sink                                                          | Not supported                                                                                            | Supported (GA)                            |
| BigQuery Change Data Capture (CDC)                                                                                                      | Supported (Preview)                                                                                      | Supported                                 |
| BigQuery change history (APPENDS)                                                                                                       | Not supported                                                                                            | Supported                                 |
| BigQuery change history (CHANGES)                                                                                                       | Not supported                                                                                            | Not supported                             |
| BigQuery continuous queries                                                                                                             | Not supported                                                                                            | Supported                                 |
| BigQuery multi-statement transactions                                                                                                   | Not supported                                                                                            | Supported (GA)                            |
| Managed disaster recovery                                                                                                               | Supported (Preview)                                                                                      | Not supported                             |
| Search index                                                                                                                            | Not supported                                                                                            | Not supported                             |
| Vector index (including auto embedding generation)                                                                                      | Not supported                                                                                            | Not supported                             |
| **Time travel**                                                                                                                         |                                                                                                          |                                           |
| Time travel (using OSS engines)                                                                                                         | Flexible (configured through table properties)                                                           | Not supported                             |
| Time travel (using BigQuery)                                                                                                            | Limited to 7 days                                                                                        | Limited to 7 days                         |
| Snapshot history and rollback to previous snapshot                                                                                      | Supported                                                                                                | Not supported                             |
| **Governance, security, and sharing**                                                                                                   |                                                                                                          |                                           |
| BigQuery Authorized Views                                                                                                               | Not supported                                                                                            | Not supported                             |
| [BigQuery column-level security](https://docs.cloud.google.com/lakehouse/docs/fine-grained-access-control#column-level-security)        | Supported (GA) for data policies on columns only                                                         | Supported (GA)                            |
| [BigQuery data masking and policy tags](https://docs.cloud.google.com/lakehouse/docs/fine-grained-access-control#column-level-security) | Supported (GA) for data policies on columns only. Policy tags and data governance tags aren't supported. | Supported (GA)                            |
| [BigQuery row-level security](https://docs.cloud.google.com/lakehouse/docs/fine-grained-access-control#row-level-security)              | Supported (GA)                                                                                           | Supported (GA)                            |
| BigQuery sharing integration                                                                                                            | Not supported                                                                                            | Supported                                 |
| **Knowledge Catalog capabilities**                                                                                                      |                                                                                                          |                                           |
| Metadata cataloging, search and discovery                                                                                               | Supported                                                                                                | Supported                                 |
| [Lineage](https://docs.cloud.google.com/knowledge-catalog/docs/about-data-lineage)                                                      | Supported                                                                                                | Supported                                 |
| Data quality/profiling                                                                                                                  | Supported                                                                                                | Supported                                 |
| Insights                                                                                                                                | Supported                                                                                                | Supported                                 |
| AI-based column and table description generation                                                                                        | Supported                                                                                                | Supported                                 |

## What's next

- Learn more about [borderless Lakehouse](https://docs.cloud.google.com/lakehouse/docs/lakehouse-basics) .
- Learn how to configure [row-level and column-level security on Lakehouse tables](https://docs.cloud.google.com/lakehouse/docs/fine-grained-access-control) .
