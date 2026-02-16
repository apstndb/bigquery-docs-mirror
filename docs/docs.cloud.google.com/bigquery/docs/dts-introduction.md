# What is BigQuery Data Transfer Service?

The BigQuery Data Transfer Service automates data movement into [BigQuery](/bigquery/docs/introduction) on a scheduled, managed basis. Your analytics team can lay the foundation for a BigQuery data warehouse without writing a single line of code.

You can access the BigQuery Data Transfer Service using the:

  - [Google Cloud console](/bigquery/docs/bigquery-web-ui)
  - [bq command-line tool](/bigquery/docs/reference/bq-cli-reference)
  - [BigQuery Data Transfer Service API](/bigquery/docs/reference/datatransfer/rest)

After you configure a data transfer, the BigQuery Data Transfer Service automatically loads data into BigQuery on a regular basis. You can also initiate data backfills to recover from any outages or gaps. You cannot use the BigQuery Data Transfer Service to transfer data out of BigQuery.

In addition to loading data into BigQuery, BigQuery Data Transfer Service is used for two BigQuery operations: [dataset copies](/bigquery/docs/copying-datasets) and [scheduled queries](/bigquery/docs/scheduling-queries) .

**Note:** Subscribe to the [BigQuery DTS announcements group](https://groups.google.com/g/bigquery-dts-announcements) to receive announcements related to the BigQuery Data Transfer Service.

## Supported data sources

The BigQuery Data Transfer Service supports loading data from the following data sources:

  - [Amazon S3](/bigquery/docs/s3-transfer)
  - [Amazon Redshift](/bigquery/docs/migration/redshift)
  - [Apache Hive](/bigquery/docs/hdfs-data-lake-transfer) ( [Preview](https://cloud.google.com/products/#product-launch-stages) )
  - [Azure Blob Storage](/bigquery/docs/blob-storage-transfer)
  - [Campaign Manager](/bigquery/docs/doubleclick-campaign-transfer)
  - [Cloud Storage](/bigquery/docs/cloud-storage-transfer)
  - [Comparison Shopping Service (CSS) Center](/bigquery/docs/css-center-transfer-schedule-transfers) ( [Preview](https://cloud.google.com/products/#product-launch-stages) )
  - [Display & Video 360](/bigquery/docs/display-video-transfer)
  - [Facebook Ads](/bigquery/docs/facebook-ads-transfer)
  - [Google Ad Manager](/bigquery/docs/doubleclick-publisher-transfer)
  - [Google Ads](/bigquery/docs/google-ads-transfer)
  - [Google Analytics 4](/bigquery/docs/google-analytics-4-transfer)
  - [Google Merchant Center](/bigquery/docs/merchant-center-transfer) ( [Preview](https://cloud.google.com/products/#product-launch-stages) )
  - [Google Play](/bigquery/docs/play-transfer)
  - [HubSpot](/bigquery/docs/hubspot-transfer) ( [Preview](https://cloud.google.com/products/#product-launch-stages) )
  - [Klaviyo](/bigquery/docs/klaviyo-transfer) ( [Preview](https://cloud.google.com/products/#product-launch-stages) )
  - [Mailchimp](/bigquery/docs/mailchimp-transfer) ( [Preview](https://cloud.google.com/products/#product-launch-stages) )
  - [Microsoft SQL Server](/bigquery/docs/sqlserver-transfer) ( [Preview](https://cloud.google.com/products/#product-launch-stages) )
  - [MySQL](/bigquery/docs/mysql-transfer)
  - [PayPal](/bigquery/docs/paypal-transfer) ( [Preview](https://cloud.google.com/products/#product-launch-stages) )
  - [Oracle](/bigquery/docs/oracle-transfer)
  - [PostgreSQL](/bigquery/docs/postgresql-transfer)
  - [Salesforce](/bigquery/docs/salesforce-transfer)
  - [Salesforce Marketing Cloud](/bigquery/docs/sfmc-transfer)
  - [Search Ads 360](/bigquery/docs/search-ads-transfer)
  - [ServiceNow](/bigquery/docs/servicenow-transfer)
  - [Shopify](/bigquery/docs/shopify-transfer) ( [Preview](https://cloud.google.com/products/#product-launch-stages) )
  - [Snowflake](/bigquery/docs/migration/snowflake-transfer) ( [Preview](https://cloud.google.com/products/#product-launch-stages) )
  - [Stripe](/bigquery/docs/stripe-transfer) ( [Preview](https://cloud.google.com/products/#product-launch-stages) )
  - [Teradata](/bigquery/docs/migration/teradata)
  - [YouTube Channel](/bigquery/docs/youtube-channel-transfer)
  - [YouTube Content Owner](/bigquery/docs/youtube-content-owner-transfer)

### Data delivery SLO considerations

The [Data Delivery SLO](https://cloud.google.com/bigquery/sla?e=48754805) applies to automatically scheduled data transfers using the BigQuery Data Transfer Service from sources within Google Cloud.

For data transfers involving third-party or non-Google Cloud sources, service outages with these sources can impact performance with the BigQuery Data Transfer Service. As such, the Data Delivery SLO does not apply to BigQuery Data Transfer Service data transfers from non-Google Cloud sources.

## Supported regions

Like BigQuery, the BigQuery Data Transfer Service is a [multi-regional resource](/docs/geography-and-regions#regional_resources) , with many additional single regions available.

A BigQuery dataset's locality is specified when you [create a destination dataset](/bigquery/docs/datasets) to store the data transferred by the BigQuery Data Transfer Service. When you set up a transfer, the transfer configuration itself is set to the same location as the destination dataset. The BigQuery Data Transfer Service processes and stages data in the same location as the destination dataset.

The BigQuery Data Transfer Service supports data transfers from any region where your data is stored to any location where your destination dataset is located.

For detailed information about transfers and region compatibility for BigQuery Data Transfer Service, see [Dataset locations and transfers](/bigquery/docs/dts-locations) . For supported regions for BigQuery, see [Dataset locations](/bigquery/docs/locations#supported_locations) .

## Using reservation slots with data transfers

Jobs triggered by the BigQuery Data Transfer Service only use reservation slots if the project, folder, or organization is assigned to a reservation with any of the following [job types](/bigquery/docs/reservations-workload-management#assignments) :

  - Query jobs using `  QUERY  `
  - Load jobs using `  PIPELINE  `

Jobs that [copy datasets](/bigquery/docs/managing-datasets#copy-datasets) don't use reservation slots.

## Pricing

For information on BigQuery Data Transfer Service pricing, see the [Pricing](https://cloud.google.com/bigquery/pricing) page.

Once data is transferred to BigQuery, standard BigQuery [storage](https://cloud.google.com/bigquery/pricing#storage) and [query](https://cloud.google.com/bigquery/pricing#queries) pricing applies.

## Quotas

For information on BigQuery Data Transfer Service quotas, see the [Quotas and limits](/bigquery/quotas) page.

## What's next

To learn how to create a transfer, see the documentation for your [data source](#supported_data_sources) .
