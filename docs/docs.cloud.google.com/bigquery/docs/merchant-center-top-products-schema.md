# Google Merchant Center top products

## Overview

**Caution:** BigQuery will no longer support this version of the Top products table on September 1, 2025. We recommend that you migrate to use the [new best sellers report](/bigquery/docs/merchant-center-best-sellers-schema) instead. For more information about migrating to the new report, see [Migrate the best sellers report](/bigquery/docs/merchant-center-best-sellers-migration) .

Best sellers data helps merchants understand the most popular brands and products in Shopping ads. For more information about best sellers, see the description in [Supported Reports](/bigquery/docs/merchant-center-transfer#supported_reports) .

The data is written to a table named `  BestSellers_TopProducts_ MERCHANT_ID  ` .

## Schema

The `  BestSellers_TopProducts_  ` table has the following schema:

<table>
<thead>
<tr class="header">
<th><strong>Column</strong></th>
<th><strong>BigQuery data type</strong></th>
<th><strong>Description</strong></th>
<th><strong>Sample field</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       rank_timestamp      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>Date and time when the rank was published.</td>
<td>2020-03-14 00:00:00 UTC</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       rank_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Rank identifier to join against the <a href="/bigquery/docs/merchant-center-product-inventory-schema">Product Inventory</a> table.</td>
<td>2020-03-14:AU:100:2:product</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       rank      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>The popularity rank of the product on Shopping ads for the `ranking_country` and `ranking_category`. Popularity is based on the estimated number of products sold. The rank updates daily. The data included in metrics might be delayed by up 2 days.</td>
<td>2</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       previous_rank      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>The change in rank over the previous 7 days.</td>
<td>4</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       ranking_country      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Country code used for ranking.</td>
<td>AU</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ranking_category      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td><a href="https://support.google.com/merchants/answer/1705911">Google product category</a> ID used for ranking.</td>
<td>5181</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       ranking_category_path      </code></td>
<td><code dir="ltr" translate="no">       RECORD,              REPEATED      </code></td>
<td><a href="https://support.google.com/merchants/answer/1705911">Google product category</a> full path for each locale used for ranking.</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ranking_category_path.locale      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td></td>
<td>en-AU</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       ranking_category_path.name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td></td>
<td>Luggage &amp; Bags</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       relative_demand      </code></td>
<td><code dir="ltr" translate="no">       RECORD      </code></td>
<td>A product's estimated demand in relation to the product with the highest popularity rank in the same category and country.</td>
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
<td>A product's estimated demand in relation to the product with the highest popularity rank in the same category and country over the previous 7 days.</td>
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
<td><code dir="ltr" translate="no">       product_title      </code></td>
<td><code dir="ltr" translate="no">       RECORD,              REPEATED      </code></td>
<td>Product title.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       product_title.locale      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td></td>
<td>en-AU</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       product_title.name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td></td>
<td>ExampleBrand Backpack</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       gtins      </code></td>
<td><code dir="ltr" translate="no">       STRING,              REPEATED      </code></td>
<td><a href="https://support.google.com/merchants/answer/188494#gtin">Global Trade Item Number</a> (GTIN).</td>
<td>07392158680955</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       brand      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Brand of the item.</td>
<td>ExampleBrand</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       google_brand_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Google brand ID of the item.</td>
<td>11887454107284768328</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       google_product_category      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td><a href="https://support.google.com/merchants/answer/1705911">Google product category</a> ID of the item.</td>
<td>100</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       google_product_category_path      </code></td>
<td><code dir="ltr" translate="no">       RECORD,              REPEATED      </code></td>
<td><a href="https://support.google.com/merchants/answer/1705911">Google product category</a> full path of the item.</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       google_product_category_path.locale      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td></td>
<td>en-US</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       google_product_category_path.name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td></td>
<td>Luggage &amp; Bags &gt; Backpacks</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       price_range      </code></td>
<td><code dir="ltr" translate="no">       RECORD      </code></td>
<td>Price range: lower and upper (with no decimals) and currency. The price does not include shipping costs.</td>
<td>n/a</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       price_range.min      </code></td>
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td></td>
<td>115</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       price_range.max      </code></td>
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td></td>
<td>147</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       price_range.currency      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td></td>
<td>AUD</td>
</tr>
</tbody>
</table>

## Understanding the data

  - Ranking categories are subject to change over time.
  - The [Google product category](https://support.google.com/merchants/answer/6324436) in the `  BestSellers_TopProducts_Inventory_  ` table might be different from the Google Product Category in the [`  Products_  `](/bigquery/docs/merchant-center-products-schema) table. The `  Products_  ` table surfaces a retailer provided value of Google product category.
  - For products in your inventory, the price range in `  BestSellers_TopProducts_  ` might differ from the `  Products_PriceBenchmarks_  ` table. Price benchmarks metrics are calculated over a different time period. The price ranges in `  BestSellers_TopProducts_  ` reflect prices of different variants of the product, whereas the price ranges in `  Products_PriceBenchmarks_  ` only refer to a single variant.
  - Some products in your inventory might not have a rank for each category in the path. We limit the number of products per category to 10,000, and in some sub-categories we don't publish any ranking.

## Example

Products might have a rank for each category within the product category path. For example, a Google Pixel 4 phone is classified as `  Electronics > Communications > Telephony > Mobile Phones  ` . The Pixel 4 will have a separate ranking for Electronics, Communications, Telephony, and Mobile Phones. Use `  ranking_category_path  ` in addition to `  ranking_country  ` to determine the depth of category that you want to see a ranking for.

In the example below, an ExampleBrand Backpack contains a separate ranking for both the Luggage & Bags and Backpacks categories. Select "Backpacks" and "AU" to see what its ranking is in Australia in the Backpacks category.

### Ranking for Luggage & Bags

<table>
<thead>
<tr class="header">
<th><strong>product_title</strong></th>
<th><strong>ExampleBrand Backpack</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>ranking_country</strong></td>
<td>AU</td>
</tr>
<tr class="even">
<td><strong>ranking_category</strong></td>
<td>5181</td>
</tr>
<tr class="odd">
<td><strong>ranking_category_path</strong></td>
<td>Luggage &amp; Bags</td>
</tr>
<tr class="even">
<td><strong>Rank</strong></td>
<td>40</td>
</tr>
<tr class="odd">
<td><strong>google_product_category</strong></td>
<td>100</td>
</tr>
<tr class="even">
<td><strong>google_product_category_path</strong></td>
<td>Luggage &amp; Bags &gt; Backpacks</td>
</tr>
</tbody>
</table>

### Ranking for Luggage & Bags \> Backpacks

<table>
<thead>
<tr class="header">
<th><strong>product_title</strong></th>
<th><strong>ExampleBrand Backpack</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>ranking_country</strong></td>
<td>AU</td>
</tr>
<tr class="even">
<td><strong>ranking_category</strong></td>
<td>100</td>
</tr>
<tr class="odd">
<td><strong>ranking_category_path</strong></td>
<td>Luggage &amp; Bags &gt; Backpacks</td>
</tr>
<tr class="even">
<td><strong>rank</strong></td>
<td>4</td>
</tr>
<tr class="odd">
<td><strong>google_product_category</strong></td>
<td>100</td>
</tr>
<tr class="even">
<td><strong>google_product_category_path</strong></td>
<td>Luggage &amp; Bags &gt; Backpacks</td>
</tr>
</tbody>
</table>

## Query examples

### Top products for a given category and country

The following SQL query returns top products for the `  Smartphones  ` category in the US.

``` text
SELECT
  rank,
  previous_rank,
  relative_demand.bucket,
  (SELECT name FROM top_products.product_title WHERE locale = 'en-US') AS product_title,
  brand,
  price_range
FROM
  dataset.BestSellers_TopProducts_merchant_id AS top_products
WHERE
  _PARTITIONDATE = 'YYYY-MM-DD' AND
  ranking_category = 267 /*Smartphones*/ AND
  ranking_country = 'US'
ORDER BY
  rank
```

**Note:** For more information about product categories, including a full list of category codes, see [Definition: `  google_product_category  `](https://support.google.com/merchants/answer/6324436) .

### Top products in your inventory

The following SQL query joins `  BestSellers_TopProducts_Inventory_  ` and `  BestSellers_TopProducts_  ` data to return a list of top products you have in your inventory.

``` text
WITH latest_top_products AS
(
  SELECT
    *
  FROM
    dataset.BestSellers_TopProducts_merchant_id
  WHERE
    _PARTITIONDATE = 'YYYY-MM-DD'
),
latest_top_products_inventory AS
(
  SELECT
    *
  FROM
    dataset.BestSellers_TopProducts_Inventory_merchant_id
  WHERE
    _PARTITIONDATE = 'YYYY-MM-DD'
)
SELECT
  top_products.rank,
  inventory.product_id,
  (SELECT ANY_VALUE(name) FROM top_products.product_title) AS product_title,
  top_products.brand,
  top_products.gtins
FROM
  latest_top_products AS top_products
INNER JOIN
  latest_top_products_inventory AS inventory
USING (rank_id)
```

**Note:** For more information about product categories, including a full list of category codes, see [Definition: `  google_product_category  `](https://support.google.com/merchants/answer/6324436) .
