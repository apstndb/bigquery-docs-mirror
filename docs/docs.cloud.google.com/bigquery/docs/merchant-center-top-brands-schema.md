# Google Merchant Center top brands table

## Overview

**Caution:** BigQuery will no longer support the report that exports the Top brands table on September 1, 2025. We recommend that you migrate to use the [new best sellers report](/bigquery/docs/merchant-center-best-sellers-schema) instead. For more information about migrating to the new report, see [Migrate the best sellers report](/bigquery/docs/merchant-center-best-sellers-migration) .

Best sellers data helps merchants understand the most popular brands and products in Shopping ads and unpaid listings. For more information about best sellers, see the description in [Supported reports](/bigquery/docs/merchant-center-transfer#supported_reports) .

The data is written to a table named `  BestSellers_TopBrands_ MERCHANT_ID  ` .

## Schema

The `  BestSellers_TopBrands_  ` table has the following schema:

<table>
<thead>
<tr class="header">
<th><strong>Column</strong></th>
<th><strong>BigQuery data type</strong></th>
<th><strong>Description</strong></th>
<th><strong>Example data</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       rank_timestamp      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>Date and time when the rank was published.</td>
<td>2020-05-30 00:00:00 UTC</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       rank_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Unique identifier for the rank.</td>
<td>2020-05-30:FR:264:120:brand</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       rank      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>The popularity rank of the brand on Shopping ads and unpaid listings for the <code dir="ltr" translate="no">       ranking_country      </code> and <code dir="ltr" translate="no">       ranking_category      </code> . Popularity is based on the estimated number of products sold. The rank updates daily. The data included in metrics might be delayed by up 2 days.</td>
<td>120</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       previous_rank      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>The change in rank over the previous 7 days.</td>
<td>86</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       ranking_country      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Country code used for ranking.</td>
<td>FR</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ranking_category      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td><a href="https://support.google.com/merchants/answer/1705911">Google product category ID</a> used for ranking.</td>
<td>264</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       ranking_category_path      </code></td>
<td><code dir="ltr" translate="no">       RECORD, REPEATED      </code></td>
<td>The full path of the <a href="https://support.google.com/merchants/answer/1705911">Google product category</a> used for ranking in each locale.</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ranking_category_path.locale      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The locale of the category path.</td>
<td>en-US</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       ranking_category_path.name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>A human-readable name for the category path.</td>
<td>Electronics &gt; Communications &gt; Telephony &gt; Mobile Phone Accessories</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       relative_demand      </code></td>
<td><code dir="ltr" translate="no">       RECORD      </code></td>
<td>A brand's estimated demand in relation to the brand with the highest popularity rank in the same category and country.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       relative_demand.bucket      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td></td>
<td>Very high</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       relative_demand.min      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td></td>
<td>51</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       relative_demand.max      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td></td>
<td>100</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       previous_relative_demand      </code></td>
<td><code dir="ltr" translate="no">       RECORD      </code></td>
<td>A brand's estimated demand in relation to the brand with the highest popularity rank in the same category and country over the previous 7 days.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       previous_relative_demand.bucket      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td></td>
<td>Very high</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       previous_relative_demand.min      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td></td>
<td>51</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       previous_relative_demand.max      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td></td>
<td>100</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       brand      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Brand of the item.</td>
<td>Example Brand Name</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       google_brand_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Google brand ID of the item.</td>
<td>11887454107284768325</td>
</tr>
</tbody>
</table>

## Query examples

### Top brands for a given category and country

The following SQL query returns top brands for the `  Smartphones  ` category in the US.

``` text
SELECT
  rank,
  previous_rank,
  brand
FROM
  dataset.BestSellers_TopBrands_merchant_id
WHERE
  _PARTITIONDATE = 'YYYY-MM-DD' AND
  ranking_category = 267 /*Smartphones*/ AND
  ranking_country = 'US'
ORDER BY
  rank
```

**Note:** For more information about product categories, including a full list of category codes, see [Definition: `  google_product_category  `](https://support.google.com/merchants/answer/6324436) .

### Products of top brands in your inventory

The following SQL query returns a list of products in your inventory from top brands, listed by category and country.

``` text
  WITH latest_top_brands AS
  (
    SELECT
      *
    FROM
      dataset.BestSellers_TopBrands_merchant_id
    WHERE
      _PARTITIONDATE = 'YYYY-MM-DD'
  ),
  latest_products AS
  (
    SELECT
      product.*,
      product_category_id
    FROM
      dataset.Products_merchant_id AS product,
      UNNEST(product.google_product_category_ids) AS product_category_id,
      UNNEST(destinations) AS destination,
      UNNEST(destination.approved_countries) AS approved_country
    WHERE
      _PARTITIONDATE = 'YYYY-MM-DD'
  )
  SELECT
    top_brands.brand,
    (SELECT name FROM top_brands.ranking_category_path
    WHERE locale = 'en-US') AS ranking_category,
    top_brands.ranking_country,
    top_brands.rank,
    products.product_id,
    products.title
  FROM
    latest_top_brands AS top_brands
  INNER JOIN
    latest_products AS products
  ON top_brands.google_brand_id = products.google_brand_id AND
     top_brands.ranking_category = product_category_id AND
     top_brands.ranking_country = products.approved_country
```

**Note:** For more information about product categories, including a full list of category codes, see [Definition: `  google_product_category  `](https://support.google.com/merchants/answer/6324436) .
