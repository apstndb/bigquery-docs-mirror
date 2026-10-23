---
name: documents/docs.cloud.google.com/bigquery/docs/use-knowledge-catalog
uri: https://docs.cloud.google.com/bigquery/docs/use-knowledge-catalog
title: Use Knowledge Catalog with BigQuery
description: Learn how Knowledge Catalog interacts with BigQuery as a central automation and governance layer for metadata.
data_source: docs.cloud.google.com
---

# Use Knowledge Catalog with BigQuery

Knowledge Catalog (formerly known as Dataplex Universal Catalog) lets you centrally govern and provide agentic access to BigQuery metadata. For more information, see [Knowledge Catalog overview](https://docs.cloud.google.com/knowledge-catalog/docs/introduction) .

## How do I use Knowledge Catalog with BigQuery?

Knowledge Catalog interacts with BigQuery in the following ways.

### Automated metadata ingestion

Knowledge Catalog automatically discovers and indexes technical metadata from BigQuery assets. This includes the following:

- **Asset types** : [datasets, tables, views, models, routines, connections, linked datasets](https://docs.cloud.google.com/bigquery/docs/resource-hierarchy) , and [graphs](https://docs.cloud.google.com/bigquery/docs/graph-overview) ( [Preview](https://cloud.google.com/products#product-launch-stages) ).
- **BigQuery sharing** : [exchanges and listings](https://docs.cloud.google.com/bigquery/docs/analytics-hub-introduction) from BigQuery sharing (formerly Analytics Hub).
- **Real-time updates** : the system supports near real-time ingestion and provides [*metadata change feeds*](https://docs.cloud.google.com/knowledge-catalog/docs/metadata-change-feeds-overview) using Pub/Sub to notify downstream systems of schema changes or deletions in BigQuery.
- **Dark data discovery** : Knowledge Catalog can [scan unstructured files](https://docs.cloud.google.com/knowledge-catalog/docs/data-insights-unstructured-data) (like PDFs in Cloud Storage), extract entities, and convert them into queryable assets in BigQuery. This capability makes previously inaccessible "dark data" available for BigQuery-based analytics and AI grounding.

### Metadata representation and enrichment

- **Entries** : each BigQuery table or asset is represented as [an *entry*](https://docs.cloud.google.com/knowledge-catalog/docs/ingest-custom-sources) in the catalog, rather than the entire table; for example, `project.dataset.table` .

- **Data quality scorecard integration** : Knowledge Catalog provides a [data quality scorecard](https://docs.cloud.google.com/knowledge-catalog/docs/enrich-entries-metadata#data-quality-scorecard) for each entry in the catalog. In addition to built-in Knowledge Catalog data scans, assertion results from Dataform are a source for this scorecard.

- **Automated metadata enrichment** : for tables and views created with Dataform, you can define semantic metadata directly in your code. This metadata is automatically synchronized to Knowledge Catalog upon successful completion of a pipeline action. The following aspect types are supported:

  - Overview: documentation and summary text for the entry.
  - Generic aspects: semantic metadata tags for technical details, such as table system and type information.

  To check the status of a metadata update, follow the instructions in [View past manual runs](https://docs.cloud.google.com/bigquery/docs/manage-pipelines#view-manual-runs) .

  After the metadata has been synchronized, you can search for and view the entry in Knowledge Catalog. For more information, see [Search for resources](https://docs.cloud.google.com/knowledge-catalog/docs/search-assets#search-data-assets) .

- **Column-level metadata** : individual columns or fields are represented as *[paths](https://docs.cloud.google.com/knowledge-catalog/docs/enrich-entries-metadata)* , allowing you to attach specific metadata, like PII markers or data quality scores, to individual fields within a BigQuery table rather than just the table itself.

- **Aspects** : technical metadata is enriched with [*aspects*](https://docs.cloud.google.com/knowledge-catalog/docs/enrich-entries-metadata#aspects) , which add business context to data, such as ownership, data quality, and documentation.

- **Data products** : you can package related BigQuery assets into [data products](https://docs.cloud.google.com/knowledge-catalog/docs/data-products-overview) —for example, ecommerce business data—which have shared access and governance constraints.

### Data discovery and search

- **Semantic search** : users can use natural language to [search](https://docs.cloud.google.com/knowledge-catalog/docs/semantic-search) for BigQuery data, which is especially useful for data scientists and AI agents to find trusted data products using long or complex queries.
- **Name translation** : for easier programmatic lookup, the system allows for [translating](https://docs.cloud.google.com/knowledge-catalog/docs/samples/dataplex-lookup-entry#code-sample) BigQuery SQL names, or fully qualified names, into Knowledge Catalog entry names.

### Agentic access and grounding

- **Agentic access** : AI agents can discover and adaptively use Knowledge Catalog tools through [a local or remote MCP server](https://docs.cloud.google.com/knowledge-catalog/docs/mcp-overview) .
- **Context for AI Agents** : Knowledge Catalog curates [a context graph](https://docs.cloud.google.com/knowledge-catalog/docs/introduction#sample-workflows) that links BigQuery datasets with business semantics, helping reduce AI hallucinations by ensuring models use enterprise-approved data.

### Governance and compliance

- **Data Lineage** : Knowledge Catalog automatically [tracks](https://docs.cloud.google.com/knowledge-catalog/docs/about-data-lineage) how data flows and transforms into and out of BigQuery tables. This capability is critical for auditing sensitive information, like PII, across the data estate.
- **Access Control:** metadata management is integrated with [Identity and Access Management (IAM)](https://docs.cloud.google.com/bigquery/docs/access-control) and [VPC Service Controls](https://docs.cloud.google.com/bigquery/docs/vpc-sc) to ensure that discovery and access to BigQuery metadata follow organizational security policies.

## What's next

Learn more about Knowledge Catalog:

- [Knowledge Catalog use cases](https://docs.cloud.google.com/knowledge-catalog/docs/use-cases)
- [Knowledge Catalog FAQ](https://docs.cloud.google.com/knowledge-catalog/docs/faq)
- [About metadata management in Knowledge Catalog](https://docs.cloud.google.com/knowledge-catalog/docs/metadata-overview)
