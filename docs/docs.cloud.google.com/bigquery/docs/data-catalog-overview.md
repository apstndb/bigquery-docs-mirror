# Overview of Data Catalog with BigQuery

**Caution:** Data Catalog is [deprecated](/data-catalog/docs/deprecations) in favor of [Dataplex Universal Catalog](/dataplex/docs/catalog-overview) . Dataplex Universal Catalog is also integrated with BigQuery, offering similar capabilities. See [Manage aspects and enrich metadata](/dataplex/docs/enrich-entries-metadata) for details on enriching your data with aspects, which are the equivalent of Data Catalog tags.

This document provides an overview of how Data Catalog relates to BigQuery.

Data Catalog is a fully managed, scalable metadata management service.

## Data Catalog use cases

BigQuery uses Data Catalog to perform the following use cases:

  - Visualizing data lineage.
  - Searching for resources for which you have access.
  - Tagging resources with metadata.

For a more complete description of Data Catalog, see [What is Data Catalog](/data-catalog/docs/concepts/overview) .

## How Data Catalog works

Data Catalog can catalog metadata from BigQuery data sources. After your metadata is cataloged, you can add your own metadata to these data sources by using tags. For a given BigQuery project, Data Catalog automatically catalogs BigQuery metadata about datasets, tables, views, and models. Data Catalog handles two types of metadata: *technical metadata* and *business metadata* . To learn more about metadata, see [Data Catalog metadata](/data-catalog/docs/concepts/metadata) .

## Search and discovery

Data Catalog offers a powerful predicate-based search experience for technical and business metadata that's associated with a Data Catalog entry that represents a BigQuery data source. You must have the permissions to read the metadata for a resource so that you can apply search and discovery on the metadata. Data Catalog does not index the data within a resource. Data Catalog only indexes the metadata that describes a BigQuery data source.

Data Catalog controls some metadata such as user-generated tags. For all metadata sourced from BigQuery, Data Catalog is a read-only service that reflects the metadata and permissions provided by BigQuery. You can make edits in BigQuery to add, update, or delete the metadata of a data entry.

To learn more about Data Catalog search, see [Search for BigQuery resources](/bigquery/docs/data-catalog#search-for-bq-resources) .

## Access Data Catalog

You can access Data Catalog functionality by using the following interfaces:

  - The **BigQuery** page in the [Google Cloud console](https://console.cloud.google.com/bigquery)

  - The **Dataplex** page in the [Google Cloud console](https://console.cloud.google.com/dataplex)

  - The [Google Cloud CLI](/sdk/gcloud/reference/data-catalog)

  - [Data Catalog APIs](/data-catalog/docs/reference)

  - [Cloud Client Libraries](/data-catalog/docs/reference/libraries)

## What's next

  - To get started with Data Catalog and BigQuery, see [Work with Data Catalog](/bigquery/docs/data-catalog) .
