---
name: documents/docs.cloud.google.com/bigquery/docs/entity-resolution-intro
uri: https://docs.cloud.google.com/bigquery/docs/entity-resolution-intro
title: Introduction to the BigQuery entity resolution framework
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# Introduction to the BigQuery entity resolution framework

BigQuery entity resolution lets you match records across shared datasets that lack a common identifier. You can also use an identity provider from a Google Cloud partner to augment your shared data with additional attributes. For example, you can link customer records across datasets to build unified customer profiles, detect financial fraud, or analyze supply chains.

Before you contribute data to a [data clean room](https://docs.cloud.google.com/bigquery/docs/data-clean-rooms) , you can use entity resolution to prepare and match your records. Entity resolution is available in on-demand and capacity pricing models across all BigQuery editions. For more information about implementation, see [Configure and use entity resolution in BigQuery](https://docs.cloud.google.com/bigquery/docs/entity-resolution-setup) .

## Benefits of entity resolution

Entity resolution provides operational and data-sharing advantages for both end users and identity providers.

### End-user benefits

When you resolve entities in BigQuery, you gain the following end-user benefits:

  - **In-place resolution** : you resolve entities in place without data transfer fees. An identity provider matches your data to their identity graph and writes the entity resolution results to a dataset in your Google Cloud project.
  - **Simplified operations** : you avoid managing extract, transform, and load (ETL) pipelines or custom data replication workflows.

### Identity provider benefits

When you offer identity services in BigQuery, you gain the following identity provider benefits:

  - **Marketplace integration** : you can offer entity resolution as a managed software as a service (SaaS) product on [Google Cloud Marketplace](https://docs.cloud.google.com/marketplace/docs/partners/integrated-saas) .
  - **Intellectual property protection** : you use your proprietary identity graphs and matching logic without revealing them to end users. This architecture helps protect your intellectual property.

## Entity resolution architecture

BigQuery implements entity resolution by calling remote functions that run matching processes in an identity provider's environment. BigQuery doesn't copy or move your data during this process.

The following diagram illustrates the entity resolution workflow between an end-user Google Cloud project and an identity provider Google Cloud project:

![A diagram showing the BigQuery entity resolution workflow between an end-user Google Cloud project and an identity provider Google Cloud project.](https://docs.cloud.google.com/static/bigquery/images/entity-resolution-arch-diagram.svg)

The entity resolution workflow involves the following steps:

1.  You grant the identity provider's service account read access to your input dataset and write access to your output dataset.
2.  You call the remote function to match your input data with the identity provider's identity graph data. The remote function passes your matching parameters to the identity provider.
3.  The identity provider's service account reads and processes your input dataset.
4.  The identity provider's service account writes the entity resolution results to your output dataset.

To run this workflow, entity resolution relies on components across both your environment and the identity provider's environment.

### End-user components

Your Google Cloud project contains the following end-user components:

  - **Remote function call** : a call that runs a procedure that the identity provider defines and implements. This call starts the entity resolution process.
  - **Input dataset** : the source dataset that contains the data that you want to match. Optionally, the input dataset can contain a metadata table with additional parameters. Identity providers specify the schema requirements for input datasets.
  - **Output dataset** : the destination dataset where the identity provider writes the matched results as an output table. Optionally, the identity provider can write a job status table with job details to this dataset. The output dataset can be the same dataset as the input dataset.

### Identity provider components

The identity provider's environment contains the following components:

  - **Control plane** : contains a [BigQuery remote function](https://docs.cloud.google.com/bigquery/docs/remote-functions) that orchestrates the matching process. The identity provider can implement this function as a [Cloud Run](https://docs.cloud.google.com/run/docs/overview/what-is-cloud-run) job or a [Cloud Run function](https://docs.cloud.google.com/functions/docs/concepts/overview) . The control plane can also contain authentication and authorization services.
  - **Data plane** : contains the identity graph dataset and the stored procedure that runs the matching logic. An identity graph is a reference database of known entity identifiers and attributes. The identity provider can implement the stored procedure as a [SQL stored procedure](https://docs.cloud.google.com/bigquery/docs/procedures) or an [Apache Spark stored procedure](https://docs.cloud.google.com/bigquery/docs/spark-procedures) . The identity graph dataset contains the tables that the identity provider matches against your data.

## Considerations

When you plan your entity resolution deployment, consider the following factors:

  - **Identity provider coordination** : before you run matching jobs, you must coordinate with a supported identity provider to obtain their service account credentials and remote function signature.
  - **External databases** : identity providers typically host identity graphs in BigQuery, but they can also store identity graphs in external databases.

## What's next

  - Learn how to [configure and use entity resolution](https://docs.cloud.google.com/bigquery/docs/entity-resolution-setup) .
  - Learn how to [work with remote functions](https://docs.cloud.google.com/bigquery/docs/remote-functions) .
  - Learn how to [work with SQL stored procedures](https://docs.cloud.google.com/bigquery/docs/procedures) .
  - Learn how to [share sensitive data with data clean rooms](https://docs.cloud.google.com/bigquery/docs/data-clean-rooms) .
