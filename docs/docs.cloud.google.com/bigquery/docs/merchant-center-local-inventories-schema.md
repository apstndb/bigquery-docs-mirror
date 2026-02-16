# Google Merchant Center local inventories table

## Overview

Local inventories data allows merchants to export their local offers of their products to BigQuery. This data includes pricing, availability, and quantity of the product along with the information about pick-up and product in-store location.

The format of local inventories data corresponds primarily to the format of the relevant fields of the Content API's [`  localinventory  `](https://developers.google.com/shopping-content/reference/rest/v2.1/localinventory) resource.

Depending on the type of Merchant account that you use, the data is written to one of the following tables:

  - If you are using an individual Merchant ID, then the data is written to the `  LocalInventories_ MERCHANT_ID  ` table.
  - If you are using an MCA account, then the data is written to the `  LocalInventories_ AGGREGATOR_ID  ` table.

## Schema

The `  LocalInventories_  ` tables have the following schema:

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
<td><code dir="ltr" translate="no">         product_id       </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Content API's REST ID of the product in the form: <code dir="ltr" translate="no">       channel:content_language:feed_label:offer_id      </code> . This field is a primary key.</td>
<td>online:en:AU:666840730</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         merchant_id       </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>Merchant account ID. This field is a primary key.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       aggregator_id      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>ID of the <a href="https://support.google.com/merchants/answer/188487">Multi Client Account (MCA)</a> .</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       store_code      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Store code of this local inventory resource.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       price      </code></td>
<td><code dir="ltr" translate="no">       RECORD      </code></td>
<td>Local price of the item.</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       price.value      </code></td>
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td>Local price of the item.</td>
<td>99</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       price.currency      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Currency of the local price of the item.</td>
<td>CHF</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       sale_price      </code></td>
<td><code dir="ltr" translate="no">       RECORD      </code></td>
<td>Local sale price of the item.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       sale_price.value      </code></td>
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td>Local sale price of the item.</td>
<td>49</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       sale_price.currency      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Currency of the local sale price of the item.</td>
<td>CHF</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       sale_price_effective_start_date      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>Start date and time when the item is on sale.</td>
<td>2021-03-30 00:00:00 UTC</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       sale_price_effective_end_date      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>End date and time when the item is on sale.</td>
<td>2021-04-14 00:00:00 UTC</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       availability      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Local availability status of the item.</td>
<td>out of stock</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       quantity      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>Quantity of the item.</td>
<td>500</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       pickup_method      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Supported pick-up method of the item.</td>
<td>ship to store</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       pickup_sla      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Expected elapsed time between the order date and the date that the item is ready for pickup.</td>
<td>three days</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       instore_product_location      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>In-store location of the item.</td>
<td></td>
</tr>
</tbody>
</table>
