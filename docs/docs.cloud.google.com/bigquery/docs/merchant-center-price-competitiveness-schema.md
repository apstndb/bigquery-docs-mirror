# Google Merchant Center Price Competitiveness table

## Overview

Price competitiveness data in BigQuery helps merchants understand how other merchants are pricing the same product. When your Google Merchant Center reporting data is transferred to BigQuery, the format of the `  PriceCompetitiveness_  ` table provides a daily price benchmark per country and per product. The price competitiveness table also contains several other attributes of the product to help you to understand the competitiveness of your pricing within a category or brand for example.

The data is written to a table named `  PriceCompetitiveness_ MERCHANT_ID  ` if you are using an individual Merchant ID, or `  PriceCompetitiveness_ AGGREGATOR_ID  ` if you're using an MCA account.

**Note:** To access price competitiveness data, you must meet the [eligibility requirements for market insights](https://support.google.com/merchants/answer/9712881) .

## Schema

The `  PriceCompetitiveness_  ` tables have the following schema:

<table>
<thead>
<tr class="header">
<th>Column</th>
<th>BigQuery data type</th>
<th>Description</th>
<th>Example data</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       aggregator_id      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>ID of the <a href="https://support.google.com/merchants/answer/188487">Multi Client Account (MCA)</a> if the merchant is part of an MCA. Null otherwise.</td>
<td>12345</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         merchant_id       </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>Google Merchant Center account ID. This field is a primary key.</td>
<td>1234</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         id       </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><a href="https://developers.google.com/shopping-content/guides/products/product-id">Content API REST ID</a> of the product in the form: <code dir="ltr" translate="no">       channel:content_language:feed_label:offer_id      </code> , similar to the way it's defined in the <a href="/bigquery/docs/merchant-center-products-schema">products table schema</a> . This field is a primary key.</td>
<td>online:en:AU:666840730</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       title      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Title of the product.</td>
<td>TN2351 black USB</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       brand      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Brand of the product.</td>
<td>Brand Name</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       offer_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Merchant provided <a href="https://support.google.com/merchants/answer/6324405">id of the product</a> .</td>
<td>tddy123uk</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       benchmark_price      </code></td>
<td><code dir="ltr" translate="no">       RECORD      </code></td>
<td>Average click-weighted price for a given product across all merchants who advertise that same product on Shopping ads. Products are matched based on their <a href="https://support.google.com/merchants/answer/6324461">GTIN</a> . For more details, see <a href="https://support.google.com/merchants/answer/9626903">Help Center article about the price competitiveness report</a> .</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       benchmark_price.amount_micros      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>Price of the item, in micros (1 is represented as 1000000).</td>
<td>1000000</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       benchmark_price.currency_code      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Currency of the price of the item.</td>
<td>USD</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       price      </code></td>
<td><code dir="ltr" translate="no">       RECORD      </code></td>
<td>Price of this product.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       price.amount_micros      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Price of the item, in micros (1 is represented as 1000000).</td>
<td>1000000</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       price.currency_code      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>Currency of the price of the item.</td>
<td>USD</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       report_country_code      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Country code where the user performed the query on Google.</td>
<td>CH, US</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       product_type_l1      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><a href="https://support.google.com/merchants/answer/6324406">Product type attribute</a> of the product.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       product_type_l2      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><a href="https://support.google.com/merchants/answer/6324406">Product type attribute</a> of the product.</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       product_type_l3      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><a href="https://support.google.com/merchants/answer/6324406">Product type attribute</a> of the product.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       product_type_l4      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><a href="https://support.google.com/merchants/answer/6324406">Product type attribute</a> of the product.</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       product_type_l5      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><a href="https://support.google.com/merchants/answer/6324406">Product type attribute</a> of the product.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       category_l1      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><a href="https://support.google.com/merchants/answer/6324436">Google product category</a> of the product.</td>
<td>Animals &amp; Pet Supplies</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       category_l2      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><a href="https://support.google.com/merchants/answer/6324436">Google product category</a> of the product.</td>
<td>Pet Supplies</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       category_l3      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><a href="https://support.google.com/merchants/answer/6324436">Google product category</a> of the product.</td>
<td>Dog Supplies</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       category_l4      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><a href="https://support.google.com/merchants/answer/6324436">Google product category</a> of the product.</td>
<td>Dog Beds</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       category_l5      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><a href="https://support.google.com/merchants/answer/6324436">Google product category</a> of the product.</td>
<td></td>
</tr>
</tbody>
</table>
