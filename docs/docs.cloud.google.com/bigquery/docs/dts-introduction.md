---
name: documents/docs.cloud.google.com/bigquery/docs/dts-introduction
uri: https://docs.cloud.google.com/bigquery/docs/dts-introduction
title: Introduction to the BigQuery Data Transfer Service
description: Gives an overview of the BigQuery Data Transfer Service, a service that automates data movement into BigQuery.
data_source: docs.cloud.google.com
---

# Introduction to the BigQuery Data Transfer Service

The BigQuery Data Transfer Service lets you automate scheduled, managed data transfers into [BigQuery](https://docs.cloud.google.com/bigquery/docs/introduction) . After you configure a data transfer, the BigQuery Data Transfer Service automatically loads data into BigQuery on a regular basis. You can also initiate data backfills to recover from outages or gaps, perform [dataset copies](https://docs.cloud.google.com/bigquery/docs/copying-datasets) , and run [scheduled queries](https://docs.cloud.google.com/bigquery/docs/scheduling-queries) . You can't use BigQuery Data Transfer Service to transfer data out of BigQuery.

To configure and manage transfers, you can use the [Google Cloud console](https://docs.cloud.google.com/bigquery/docs/bigquery-web-ui) , the [bq command-line tool](https://docs.cloud.google.com/bigquery/docs/reference/bq-cli-reference) , or the [BigQuery Data Transfer Service API](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest) . The **Pipelines & Connections** page also provides a [streamlined workflow](https://docs.cloud.google.com/bigquery/docs/pipeline-connection-page) ( [preview](https://cloud.google.com/products/#product-launch-stages) ) for creating transfers. To receive service updates, subscribe to the [BigQuery DTS announcements group](https://groups.google.com/g/bigquery-dts-announcements) .

## Supported data sources

The BigQuery Data Transfer Service supports loading data from the following data sources:

| Category                      | Data source                                                                                                                                                                        |
|-------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Cloud storage                 | [Amazon Simple Storage Service (Amazon S3)](https://docs.cloud.google.com/bigquery/docs/s3-transfer-intro)                                                                         |
| Cloud storage                 | [Azure Blob Storage](https://docs.cloud.google.com/bigquery/docs/blob-storage-transfer-intro)                                                                                      |
| Cloud storage                 | [Cloud Storage](https://docs.cloud.google.com/bigquery/docs/cloud-storage-transfer-overview)                                                                                       |
| Databases and data warehouses | [Amazon Redshift](https://docs.cloud.google.com/bigquery/docs/migration/redshift)                                                                                                  |
| Databases and data warehouses | [Apache Hive Metastore](https://docs.cloud.google.com/bigquery/docs/hdfs-data-lake-transfer)                                                                                       |
| Databases and data warehouses | [Microsoft SQL Server](https://docs.cloud.google.com/bigquery/docs/sqlserver-transfer-intro) ( [Preview](https://cloud.google.com/products#product-launch-stages) )                |
| Databases and data warehouses | [MySQL](https://docs.cloud.google.com/bigquery/docs/mysql-transfer-intro)                                                                                                          |
| Databases and data warehouses | [Oracle](https://docs.cloud.google.com/bigquery/docs/oracle-transfer-intro)                                                                                                        |
| Databases and data warehouses | [PostgreSQL](https://docs.cloud.google.com/bigquery/docs/postgresql-transfer-intro)                                                                                                |
| Databases and data warehouses | [Snowflake](https://docs.cloud.google.com/bigquery/docs/migration/snowflake-transfer)                                                                                              |
| Databases and data warehouses | [Teradata](https://docs.cloud.google.com/bigquery/docs/migration/teradata)                                                                                                         |
| Google services               | [Campaign Manager](https://docs.cloud.google.com/bigquery/docs/doubleclick-campaign-transfer)                                                                                      |
| Google services               | [Comparison Shopping Service (CSS) Center](https://docs.cloud.google.com/bigquery/docs/css-center-transfer) ( [Preview](https://cloud.google.com/products#product-launch-stages) ) |
| Google services               | [Display & Video 360](https://docs.cloud.google.com/bigquery/docs/display-video-transfer)                                                                                          |
| Google services               | [Google Ad Manager](https://docs.cloud.google.com/bigquery/docs/doubleclick-publisher-transfer)                                                                                    |
| Google services               | [Google Ads](https://docs.cloud.google.com/bigquery/docs/google-ads-transfer)                                                                                                      |
| Google services               | [Google Analytics 4](https://docs.cloud.google.com/bigquery/docs/google-analytics-4-transfer)                                                                                      |
| Google services               | [Google Merchant Center](https://docs.cloud.google.com/bigquery/docs/merchant-center-transfer) ( [Preview](https://cloud.google.com/products#product-launch-stages) )              |
| Google services               | [Google Play](https://docs.cloud.google.com/bigquery/docs/play-transfer)                                                                                                           |
| Google services               | [Search Ads 360](https://docs.cloud.google.com/bigquery/docs/search-ads-transfer)                                                                                                  |
| Google services               | [YouTube Channel](https://docs.cloud.google.com/bigquery/docs/youtube-channel-transfer)                                                                                            |
| Google services               | [YouTube Content Owner](https://docs.cloud.google.com/bigquery/docs/youtube-content-owner-transfer)                                                                                |
| Marketing platforms           | [Facebook Ads](https://docs.cloud.google.com/bigquery/docs/facebook-ads-transfer-intro)                                                                                            |
| Marketing platforms           | [HubSpot](https://docs.cloud.google.com/bigquery/docs/hubspot-transfer) ( [Preview](https://cloud.google.com/products#product-launch-stages) )                                     |
| Marketing platforms           | [Klaviyo](https://docs.cloud.google.com/bigquery/docs/klaviyo-transfer-intro) ( [Preview](https://cloud.google.com/products#product-launch-stages) )                               |
| Marketing platforms           | [Mailchimp](https://docs.cloud.google.com/bigquery/docs/mailchimp-transfer) ( [Preview](https://cloud.google.com/products#product-launch-stages) )                                 |
| Payment platforms             | [PayPal](https://docs.cloud.google.com/bigquery/docs/paypal-transfer) ( [Preview](https://cloud.google.com/products#product-launch-stages) )                                       |
| Payment platforms             | [Shopify](https://docs.cloud.google.com/bigquery/docs/shopify-transfer) ( [Preview](https://cloud.google.com/products#product-launch-stages) )                                     |
| Payment platforms             | [Stripe](https://docs.cloud.google.com/bigquery/docs/stripe-transfer) ( [Preview](https://cloud.google.com/products#product-launch-stages) )                                       |
| SaaS platforms                | [Salesforce](https://docs.cloud.google.com/bigquery/docs/salesforce-transfer-intro)                                                                                                |
| SaaS platforms                | [Salesforce Marketing Cloud](https://docs.cloud.google.com/bigquery/docs/sfmc-transfer)                                                                                            |
| SaaS platforms                | [ServiceNow](https://docs.cloud.google.com/bigquery/docs/servicenow-transfer)                                                                                                      |

### Data delivery SLO considerations

The [Data Delivery SLO](https://cloud.google.com/bigquery/sla?e=48754805) applies to automatically scheduled data transfers using the BigQuery Data Transfer Service from sources within Google Cloud.

For data transfers involving third-party or non-Google Cloud sources, service outages with these sources can impact performance with the BigQuery Data Transfer Service. As such, the Data Delivery SLO does not apply to BigQuery Data Transfer Service data transfers from non-Google Cloud sources.

## Supported regions

Like BigQuery, the BigQuery Data Transfer Service is a [multi-regional resource](https://docs.cloud.google.com/docs/geography-and-regions#regional_resources) , with many additional single regions available.

A BigQuery dataset's locality is specified when you [create a destination dataset](https://docs.cloud.google.com/bigquery/docs/datasets) to store the data transferred by the BigQuery Data Transfer Service. When you set up a transfer, the transfer configuration itself is set to the same location as the destination dataset. The BigQuery Data Transfer Service processes and stages data in the same location as the destination dataset.

The BigQuery Data Transfer Service supports data transfers from any region where your data is stored to any location where your destination dataset is located.

For detailed information about transfers and region compatibility for BigQuery Data Transfer Service, see [Dataset locations and transfers](https://docs.cloud.google.com/bigquery/docs/dts-locations) . For supported regions for BigQuery, see [Dataset locations](https://docs.cloud.google.com/bigquery/docs/locations#supported_locations) .

## Using reservation slots with data transfers

Jobs triggered by the BigQuery Data Transfer Service only use reservation slots if the project, folder, or organization is assigned to a reservation with any of the following [job types](https://docs.cloud.google.com/bigquery/docs/reservations-workload-management#assignments) :

- Query jobs using `QUERY`
- Load jobs using `PIPELINE`

Jobs that [copy datasets](https://docs.cloud.google.com/bigquery/docs/managing-datasets#copy-datasets) don't use reservation slots.

## Pricing

For information on BigQuery Data Transfer Service pricing, see the [Pricing](https://cloud.google.com/bigquery/pricing) page.

Once data is transferred to BigQuery, standard BigQuery [storage](https://cloud.google.com/bigquery/pricing#storage) and [query](https://cloud.google.com/bigquery/pricing#queries) pricing applies.

## Quotas

For information on BigQuery Data Transfer Service quotas, see the [Quotas and limits](https://docs.cloud.google.com/bigquery/quotas) page.

## Troubleshoot transfer configurations

For information about resolving issues with BigQuery Data Transfer Service, see [Troubleshoot transfer configurations](https://docs.cloud.google.com/bigquery/docs/transfer-troubleshooting) .

## What's next

- To learn how to create a transfer, see the documentation for your [data source](https://docs.cloud.google.com/bigquery/docs/dts-introduction#supported_data_sources) .
