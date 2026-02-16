# Google Merchant Center Performance Table

## Overview

The Performance Table contains columns that you can use to understand the distribution of the following metrics:

  - **Clicks:** The total number of clicks on your products on Google. Only visits to your product detail pages are counted.

  - **Impressions:** The total number of times your products were shown on Google. Only impressions where customers had the option to visit your product detail pages are counted. If your products show zero impressions, you should verify that the products are approved and wait a few days for impressions to appear. Impressions may also not show if they are below a minimum threshold for a category, which can lead to different totals than what is reported in other Google surfaces.

Note that Performance data might get updated up to 3 days in the past to account for corrections. The variations are usually small.

When you select `  Performance  ` as one of the reports that are relevant to your transfer, the following table is created:

  - `  ProductPerformance_ MERCHANT_ID  `

## Schema

The `  ProductPerformance_  ` table has the following schema:

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
<td><code dir="ltr" translate="no">         merchant_id       </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>Google Merchant Center account ID. This field is a primary key</td>
<td>1234</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       aggregator_id      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>ID of the <a href="https://support.google.com/merchants/answer/188487">Multi Client Account (MCA)</a> if the merchant center account ID is managed by an MCA. Null otherwise.</td>
<td>12345</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         offer_id       </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Merchant provided <a href="https://support.google.com/merchants/answer/6324405">id of the product</a> at the time the interaction happened. This field is a primary key.</td>
<td>tddy123uk</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       title      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Title of the product at the time the interaction happened.</td>
<td>TN2351 black USB</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       brand      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Brand of the product at the time the interaction happened.</td>
<td>Brand Name</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       category_l1      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><a href="https://support.google.com/merchants/answer/6324436">Google product category</a> of the product at the time the interaction happened. Set to an empty string when no category exists.</td>
<td>Animals &amp; Pet Supplies</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       category_l2      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><a href="https://support.google.com/merchants/answer/6324436">Google product category</a> of the product at the time the interaction happened. Set to an empty string when no category exists.</td>
<td>Pet Supplies</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       category_l3      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><a href="https://support.google.com/merchants/answer/6324436">Google product category</a> of the product at the time the interaction happened. Set to an empty string when no category exists.</td>
<td>Dog Supplies</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       category_l4      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><a href="https://support.google.com/merchants/answer/6324436">Google product category</a> of the product at the time the interaction happened. Set to an empty string when no category exists.</td>
<td>Dog Beds</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       category_l5      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><a href="https://support.google.com/merchants/answer/6324436">Google product category</a> of the product at the time the interaction happened. Set to an empty string when no category exists.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       product_type_l1      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><a href="https://support.google.com/merchants/answer/6324406">Product type attribute</a> of the product at the time the interaction happened.</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       product_type_l2      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><a href="https://support.google.com/merchants/answer/6324406">Product type attribute</a> of the product at the time the interaction happened.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       product_type_l3      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><a href="https://support.google.com/merchants/answer/6324406">Product type attribute</a> of the product at the time the interaction happened.</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       product_type_l4      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><a href="https://support.google.com/merchants/answer/6324406">Product type attribute</a> of the product at the time the interaction happened.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       product_type_l5      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><a href="https://support.google.com/merchants/answer/6324406">Product type attribute</a> of the product at the time the interaction happened.</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       custom_label0      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><a href="https://support.google.com/merchants/answer/6324473">Custom label attribute</a> of the product at the time the interaction happened.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       custom_label1      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><a href="https://support.google.com/merchants/answer/6324473">Custom label attribute</a> of the product at the time the interaction happened.</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       custom_label2      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><a href="https://support.google.com/merchants/answer/6324473">Custom label attribute</a> of the product at the time the interaction happened.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       custom_label3      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><a href="https://support.google.com/merchants/answer/6324473">Custom label attribute</a> of the product at the time the interaction happened.</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       custom_label4      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><a href="https://support.google.com/merchants/answer/6324473">Custom label attribute</a> of the product at the time the interaction happened.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       customer_country_code      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Country of the customer clicking or seeing the product.</td>
<td>CH</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       clicks      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>Total number of clicks on your products on Google that led to visits to your product detail pages.</td>
<td>17</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       impressions      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>Total number of times your products were shown on Google. Only impressions where customers had the option to visit your product detail pages are counted. If your products show zero impressions, you should verify that the products are approved and wait a few days for impressions to appear. Impressions may also not show if they are below a minimum threshold for a category, which can lead to different totals than what is reported in other Google surfaces.</td>
<td>601</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       destination      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Whether the interaction happened on Shopping Ads or Free Listings.</td>
<td>FREE, ADS</td>
</tr>
</tbody>
</table>
