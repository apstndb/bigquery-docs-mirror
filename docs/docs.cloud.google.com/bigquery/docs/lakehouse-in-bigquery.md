---
name: documents/docs.cloud.google.com/bigquery/docs/lakehouse-in-bigquery
uri: https://docs.cloud.google.com/bigquery/docs/lakehouse-in-bigquery
title: Interact with Lakehouse data in BigQuery
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# Interact with Lakehouse data in BigQuery

[*Lakehouse for Apache Iceberg*](https://docs.cloud.google.com/lakehouse/docs/introduction) is a storage engine that unites Google Cloud and open source services to create a unified interface for advanced analytics and AI. It provides the foundation to build an open, managed, and high-performance lakehouse with automated data management and built-in governance using Apache Iceberg.

When you [create a table in Lakehouse](https://docs.cloud.google.com/lakehouse/docs/lakehouse-tables) , it is automatically queryable from BigQuery and is visible on the BigQuery page of the Google Cloud console. Your Lakehouse namespaces and schemas are also automatically mapped to BigQuery datasets.

## Differences between Lakehouse resources and other BigQuery resources

The following are key differences between Lakehouse and standard BigQuery resources:

  - Lakehouse datasets appear in the BigQuery page of the Google Cloud console next to the water icon.
  - You can't modify Lakehouse resources from BigQuery.
  - Lakehouse resources have additional metadata in their respective **Details** section.

## Use borderless Lakehouse

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

> **Note:** For support during the preview, email <biglake-help@google.com> .

You can use [borderless Lakehouse](https://docs.cloud.google.com/lakehouse/docs/about-borderless-lakehouse) to query data that's stored in other cloud providers, directly from BigQuery, without migrating files or building complex ETL pipelines. For configuration information, see [Use borderless Lakehouse](https://docs.cloud.google.com/lakehouse/docs/use-borderless-lakehouse) .

## What's next

  - Learn more about [Lakehouse](https://docs.cloud.google.com/lakehouse/docs/lakehouse-basics) .
