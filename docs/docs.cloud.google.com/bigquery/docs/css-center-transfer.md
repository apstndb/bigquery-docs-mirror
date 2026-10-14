---
name: documents/docs.cloud.google.com/bigquery/docs/css-center-transfer
uri: https://docs.cloud.google.com/bigquery/docs/css-center-transfer
title: Load CSS Center data into BigQuery
description: Learn how the BigQuery Data Transfer Service loads reporting data from Comparison Shopping Service (CSS) Center into BigQuery.
data_source: docs.cloud.google.com
---

# Load CSS Center data into BigQuery

> **Preview**
>
> This product is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

> **Note:** To get support or provide feedback for Comparison Shopping Service (CSS) Center transfers with BigQuery Data Transfer Service, contact <gmc-transfer-preview@google.com> .

You can load data from CSS Center to BigQuery using the [BigQuery Data Transfer Service](https://docs.cloud.google.com/bigquery/docs/dts-introduction) for CSS Center connector. With the BigQuery Data Transfer Service, you can schedule recurring transfer jobs that add your latest data from your CSS Center to BigQuery.

## Supported reports

The BigQuery Data Transfer Service for the CSS Center supports the following data from the [product and product issues reports](https://docs.cloud.google.com/bigquery/docs/merchant-center-transfer#products_and_product_issues) of associated Merchant Center accounts.

### Products and product issues

This report contains data that merchants associated with your CSS Center have uploaded to their Merchant Center accounts. This report also includes item level issues detected by Google for your merchants' products. For information on how this data is loaded into BigQuery, see the [CSS Center product table schema](https://docs.cloud.google.com/bigquery/docs/css-center-products-schema) .

## Data ingestion from CSS Center transfers

When you transfer data from CSS Center into BigQuery, the data is loaded into BigQuery tables that are partitioned by date. The table partition that the data is loaded into corresponds to the date from the data source. If you schedule multiple transfers for the same date, BigQuery Data Transfer Service overwrites the partition for that specific date with the latest data. Multiple transfers in the same day or running backfills don't result in duplicate data, and partitions for other dates are not affected.

## Query your data

When your data is transferred to BigQuery, the data is written to [ingestion-time partitioned tables](https://docs.cloud.google.com/bigquery/docs/partitioned-tables) .

When you query your CSS Center table, you must use the `_PARTITIONTIME` or `_PARTITIONDATE` pseudocolumn in your query. For more information, see [Querying partitioned tables](https://docs.cloud.google.com/bigquery/docs/querying-partitioned-tables) .

The `Products_` table contains nested and repeated fields. For information on handling nested and repeated data, see [Differences in repeated field handling](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/migrating-from-legacy-sql#differences_in_repeated_field_handling) .

## CSS Center sample queries

You can use the following CSS Center sample queries to analyze your transferred data. You can also use the queries in a visualization tool such as [Data Studio](https://www.google.com/analytics/data-studio/) .

In each of the following queries, replace ` dataset ` with your dataset name. Replace ` css_id ` with your CSS domain ID.

### Products and product issues sample queries

The following queries analyze data from the products and product issues report.

#### Products and product issues statistics

The following SQL sample query provides the number of products, products with issues, and issues by day.

```
SELECT
  _PARTITIONDATE AS date,
  COUNT(*) AS num_products,
  COUNTIF(ARRAY_LENGTH(item_issues) > 0) AS num_products_with_issues,
  SUM(ARRAY_LENGTH(item_issues)) AS num_issues
FROM
  dataset.Products_css_id
WHERE
  _PARTITIONDATE >= 'YYYY-MM-DD'
GROUP BY
  date
ORDER BY
  date DESC;
```

#### Disapproved products

The following SQL sample query provides the number of products that are not approved for display, separated by region and reporting context. Disapproval can result from the reporting context being [excluded](https://support.google.com/merchants/answer/6324486) or because of an issue with the product.

```
SELECT
  _PARTITIONDATE AS date,
  statuses.region as disapproved_region,
  reporting_context_status.reporting_context as reporting_context,
  COUNT(*) AS num_products
FROM
  dataset.Products_css_id,
  UNNEST(reporting_context_statuses) AS reporting_context_status,
  UNNEST(reporting_context_status.region_and_status) AS statuses
WHERE
  _PARTITIONDATE >= 'YYYY-MM-DD' AND statuses.status = 'DISAPPROVED'
GROUP BY
  date, disapproved_region, reporting_context
ORDER BY
  date DESC;
```

#### Products with disapproved issues

The following SQL sample query retrieves the number of products with disapproved issues, separated by region.

```
SELECT
  _PARTITIONDATE AS date,
  disapproved_region,
  COUNT(DISTINCT CONCAT(CAST(css_id AS STRING), ':', product_id))
      AS num_distinct_products
FROM
  dataset.Products_css_id,
  UNNEST(item_issues) AS issue,
  UNNEST(issue.severity.severity_per_reporting_context) as severity_per_rc,
  UNNEST(severity_per_rc.disapproved_regions) as disapproved_region
WHERE
  _PARTITIONDATE >= 'YYYY-MM-DD'
GROUP BY
  date, disapproved_region
ORDER BY
  date DESC;
```
