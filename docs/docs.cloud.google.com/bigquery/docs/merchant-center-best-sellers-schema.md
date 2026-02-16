# Google Merchant Center best sellers table

## Overview

You can use the best sellers report to view the best-selling products and brands on Google Shopping and in Shopping Ads. You can use the information from this report to understand which products are performing well on Google, and whether you carry them.

Selecting the best sellers report for your transfer creates five tables. For a given merchant ID, the report creates the following tables:

  - `  BestSellersBrandWeekly_ MERCHANT_ID  `
  - `  BestSellersBrandMonthly_ MERCHANT_ID  `
  - `  BestSellersProductClusterWeekly_ MERCHANT_ID  `
  - `  BestSellersProductClusterMonthly_ MERCHANT_ID  `
  - `  BestSellersEntityProductMapping_ MERCHANT_ID  `

For an MCA account, the report generates the following tables:

  - `  BestSellersBrandWeekly_ AGGREGATOR_ID  `
  - `  BestSellersBrandMonthly_ AGGREGATOR_ID  `
  - `  BestSellersProductClusterWeekly_ AGGREGATOR_ID  `
  - `  BestSellersProductClusterMonthly_ AGGREGATOR_ID  `
  - `  BestSellersEntityProductMapping_ AGGREGATOR_ID  `

The best sellers tables follow the monthly or weekly best seller reports, both product and brand, from [Google Merchant Center](https://support.google.com/merchants/answer/9488679) . The latest monthly or weekly snapshot is updated daily. Since data is updated at the start of each week or month, some data might be repeated several days in a row. You can expect updated popular products data every week or month for the previous period. The new data included in your metrics might not be available for up to two weeks.

The mapping table `  BestSellersEntityProductMapping_  ` contains ranking entity IDs from the `  BestSellersProductCluster<Weekly/Monthly>_  ` tables and their corresponding product IDs from the merchant's inventory. When generated at the MCA level, the table contains mapping data for all of the subaccounts. This table is meant for joining the best sellers data with information in other tables exported by the Merchant Center transfer, which have the same format of product ID (Products, Local Inventories, Regional Inventories, Price Insights, Price Competitiveness, Product Targeting).

While brands are ranked across many different categories, all products in the `  Products_  ` table are in leaf categories. To join brands and products on non-leaf categories, use the `  google_product_category_ids  ` field.

**Note:** To access best sellers data, you must meet the [eligibility requirements for market insights](https://support.google.com/merchants/answer/9712881) .

## `     BestSellersProductCluster<Weekly/Monthly>_    ` tables

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
<td><code dir="ltr" translate="no">       country_code      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Country in which the products are sold. Not all countries will contain ranking data. For more information, see the <a href="https://support.google.com/merchants/answer/13299535#Availability">list of included countries</a> .</td>
<td>CH</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       report_category_id      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td><a href="https://support.google.com/merchants/answer/6324436">Google product category id</a> of the sold products.</td>
<td>1234</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       title      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Title of the best selling product cluster.</td>
<td>TN2351 black USB</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       brand      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Brand of the best selling product cluster. Set to null when no brand exists.</td>
<td>Brand Name</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       category_l1      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Google product category of the best selling product cluster. Set to an empty string when no category exists.</td>
<td>Animals &amp; Pet Supplies</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       category_l2      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Google product category of the best selling product cluster. Set to an empty string when no category exists.</td>
<td>Pet Supplies</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       category_l3      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Google product category of the best selling product cluster. Set to an empty string when no category exists.</td>
<td>Dog Supplies</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       category_l4      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Google product category of the best selling product cluster. Set to an empty string when no category exists.</td>
<td>Dog Beds</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       category_l5      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Google product category of the best selling product cluster.</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       variant_gtins      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><a href="https://support.google.com/merchants/answer/6324461">GTINs</a> of products from your inventory corresponding to this product cluster, each separated by a space.</td>
<td>3234567890126 3234567890131</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       product_inventory_status      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Status of this product in your inventory. In MCA-level tables, the value is always <code dir="ltr" translate="no">       NOT_IN_INVENTORY      </code> or <code dir="ltr" translate="no">       UNKNOWN      </code> . To get the inventory status of subaccounts, join the <code dir="ltr" translate="no">       BestSellersEntityProductMapping_      </code> table with the <code dir="ltr" translate="no">       Products_      </code> table.</td>
<td>IN_STOCK, NOT_IN_INVENTORY, OUT_OF_STOCK</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       brand_inventory_status      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Status of this brand in your inventory, based on the status of products from this brand. Set to <code dir="ltr" translate="no">       UNKNOWN      </code> when no brand exists.</td>
<td>IN_STOCK, NOT_IN_INVENTORY, OUT_OF_STOCK</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       entity_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Identifier of this ranked best sellers entry. This column is used for joining with other tables, using the <code dir="ltr" translate="no">       BestSellersEntityProductMapping      </code> table.</td>
<td>ab12345cdef6789gh</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       rank      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>Rank of the product (the lower, the more sold the product).</td>
<td>5</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       previous_rank      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>Rank of the product in the previous period (week or month).</td>
<td>5</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       relative_demand      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Product's estimated demand in relation to the product with the highest rank in the same category and country.</td>
<td>VERY_HIGH, HIGH, MEDIUM, LOW, VERY_LOW</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       previous_relative_demand      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Relative demand value for this product compared to the previous period (week or month). Set to <code dir="ltr" translate="no">       null      </code> when no previous demand exists.</td>
<td>VERY_HIGH, HIGH, MEDIUM, LOW, VERY_LOW</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       relative_demand_change      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>How the relative demand changed for this product compared to the previous period (week or month). Set to <code dir="ltr" translate="no">       UNKNOWN      </code> when no previous demand exists.</td>
<td>FLAT, SINKER, RISER</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       price_range      </code></td>
<td><code dir="ltr" translate="no">       RECORD      </code></td>
<td>Price range: lower and upper (with no decimals) and currency. The price doesn't include shipping costs.</td>
<td>n/a</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       price_range.min_amount_micros      </code></td>
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td>Price of the item, in micros (1 is represented as 1000000).</td>
<td>115000000</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       price_range.max_amount_micros      </code></td>
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td>Price of the item, in micros (1 is represented as 1000000).</td>
<td>147000000</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       price_range.currency_code      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Currency of the price range of the item.</td>
<td>AUD</td>
</tr>
</tbody>
</table>

**Note:** These tables don't have primary keys.

## `     BestSellersBrand<Weekly/Monthly>_    ` tables

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
<td><code dir="ltr" translate="no">       brand      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Best selling brand.</td>
<td>Brand Name</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       category_id      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td><a href="https://support.google.com/merchants/answer/6324436">Google product category ID</a> of the best selling brand.</td>
<td>1234</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       country_code      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Country in which the best selling brand has been sold. For more information, see the <a href="https://support.google.com/merchants/answer/13299535#Availability">list of included countries</a> .</td>
<td>CH</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       rank      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>Rank of the best selling brand (the lower the more sold).</td>
<td>5</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       previous_rank      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>Rank of the best selling brand in the previous period (week or month). Set to <code dir="ltr" translate="no">       0      </code> when no previous rank exists.</td>
<td>5</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       relative_demand      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Product's estimated demand in relation to the product with the highest rank in the same category and country.</td>
<td>VERY_HIGH, HIGH, MEDIUM, LOW, VERY_LOW</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       previous_relative_demand      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Relative demand in the previous period (week or month). Set to <code dir="ltr" translate="no">       null      </code> when no previous demand exists.</td>
<td>VERY_HIGH, HIGH, MEDIUM, LOW, VERY_LOW</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       relative_demand_change      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Change in demand compared to the previous period (week or month). Set to <code dir="ltr" translate="no">       UNKNOWN      </code> when no previous rank exists.</td>
<td>FLAT, SINKER, RISER</td>
</tr>
</tbody>
</table>

**Note:** These tables don't have primary keys.

## `     BestSellersEntityProductMapping_    ` table

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
<td><code dir="ltr" translate="no">       merchant_id      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>Merchant Center account ID. If you query the table at the MCA level, this field contains the subaccount merchant ID. If you query the table for standalone accounts or subaccounts, this field contains the merchant account ID.</td>
<td>1234</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       product_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>REST ID of the product in the form: <code dir="ltr" translate="no">       channel:content_language:feed_label:offer_id      </code> . This ID will always reflect the latest state of the product at the time the data is exported to BigQuery. This is the join key with all other tables containing the product ID in this format.</td>
<td>online:en:AU:666840730</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       entity_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Identifier of the ranked best sellers entry. This is the join key with the <code dir="ltr" translate="no">       BestSellersProductCluster&amp;ltWeekly/Monthly&gt;_      </code> tables.</td>
<td>ab12345cdef6789gh</td>
</tr>
</tbody>
</table>
