# Google Merchant Center regional inventories table

## Overview

Regional inventories table shows merchants their regional availability and pricing overrides of their products. The format of regional inventories data corresponds primarily to the format of the relevant fields of the Content API's [`  regionalinventory  `](https://developers.google.com/shopping-content/reference/rest/v2.1/regionalinventory) resource.

The data is written to a table named `  RegionalInventories_ MERCHANT_ID  ` if you are using an individual Merchant ID, or `  RegionalInventories_ AGGREGATOR_ID  ` if you are using an MCA account.

## Schema

The `  RegionalInventories_  ` table has the following schema:

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
<td>Aggregator account ID for multi-client accounts.</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       region_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Region ID of the inventory.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       price      </code></td>
<td><code dir="ltr" translate="no">       RECORD      </code></td>
<td>Regional price of the item.</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       price.value      </code></td>
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td>Regional price of the item.</td>
<td>99</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       price.currency      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Currency of the regional price of the item.</td>
<td>CHF</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       sale_price      </code></td>
<td><code dir="ltr" translate="no">       RECORD      </code></td>
<td>Regional sale price of the item.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       sale_price.value      </code></td>
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td>Regional sale price of the item.</td>
<td>49</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       sale_price.currency      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Currency of the regional sale price of the item.</td>
<td>CHF</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       sale_price_effective_start_date      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>Start date and time when the item is on sale in the region.</td>
<td>2021-03-30 00:00:00 UTC</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       sale_price_effective_end_date      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>End date and time when the item is on sale in the region.</td>
<td>2021-04-14 00:00:00 UTC</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       availability      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Regional availability status of the item.</td>
<td>out of stock</td>
</tr>
</tbody>
</table>
