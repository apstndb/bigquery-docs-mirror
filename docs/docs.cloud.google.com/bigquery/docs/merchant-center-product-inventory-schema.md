# Google Merchant Center product inventory table

## Overview

**Caution:** BigQuery will no longer support the report that exports the Product Inventory table on September 1, 2025. We recommend that you migrate to use the [new best sellers report](/bigquery/docs/merchant-center-best-sellers-schema) instead. For more information about migrating to the new report, see [Migrate the best sellers report](/bigquery/docs/merchant-center-best-sellers-migration) .

Best sellers data helps merchants understand the most popular brands and products in Shopping ads and unpaid listings. For more information about best sellers, see the description in [Supported reports](/bigquery/docs/merchant-center-transfer#supported_reports) .

The data is written to a table named `  BestSellers_TopProducts_Inventory_ MERCHANT_ID  ` .

## Schema

The `  BestSellers_TopProducts_Inventory_  ` table has the following schema:

<table>
<thead>
<tr class="header">
<th><strong>Column</strong></th>
<th><strong>BigQuery data type</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       rank_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Rank identifier to join against the <a href="/bigquery/docs/merchant-center-top-products-schema">Top Products</a> table</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       product_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Content API's REST ID of the product in the form <code dir="ltr" translate="no">       channel:content_language:feed_label:offer_id      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       merchant_Id      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>Merchant account ID.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       aggregator_id      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>Aggregator account ID for multi-client accounts.</td>
</tr>
</tbody>
</table>

## Example

The example below demonstrates how the `  BestSellers_TopProducts_Inventory_  ` table provides a mapping to your products for all target countries in the `  Products_  ` table.

**Top Products**

<table>
<thead>
<tr class="header">
<th><strong>product_title</strong></th>
<th><strong>rank_id:</strong></th>
<th><strong>ranking_country</strong></th>
<th><strong>ranking_category</strong></th>
<th><strong>rank</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Example Backpack</td>
<td>2020-03-14:AU:5181:40:product</td>
<td>AU</td>
<td>5181</td>
<td>40</td>
</tr>
</tbody>
</table>

**Product inventory table**

<table>
<thead>
<tr class="header">
<th><strong>rank_id</strong></th>
<th><strong>product_id</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>2020-03-14:AU:5181:40:product</td>
<td>online:en:AU:666840730</td>
</tr>
<tr class="even">
<td>2020-03-14:AU:5181:40:product</td>
<td>online:en:AU:666840730</td>
</tr>
</tbody>
</table>
