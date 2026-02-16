# Google Merchant Center products table schema

## Overview

When your Google Merchant Center reporting data is transferred to BigQuery, the format of product and product issues data corresponds primarily to the format of the relevant fields of the Content API's [Products](https://developers.google.com/shopping-content/v2/reference/v2.1/products) and [Productstatuses](https://developers.google.com/shopping-content/v2/reference/v2.1/productstatuses) resources.

The data is written to a table named `  Products_ MERCHANT_ID  ` if you are using an individual Merchant ID, or `  Products_ AGGREGATOR_ID  ` if you're using an MCA account.

**Note:** The `  Products and product issues  ` data is not available immediately when the report is first requested. When you first request a transfer for a merchant or aggregator ID, there might be a delay of up to 1 day before the `  Products_  ` table is available for exporting.

## Schema

The `  Products_  ` table has the following schema:

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
<td><code dir="ltr" translate="no">       product_data_timestamp      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>Timestamp of the product data.</td>
<td>2023-09-14 11:49:50 UTC</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         product_id       </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Content API's REST ID of the product in the form: <code dir="ltr" translate="no">       channel:content_language:feed_label:offer_id      </code> . This is the primary key.</td>
<td>online:en:AU:666840730</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       merchant_id      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>Merchant account ID.</td>
<td>1234</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       aggregator_id      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>Aggregator account ID for multi-client accounts.</td>
<td>12345</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       offer_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Merchant provided <a href="https://support.google.com/merchants/answer/6324405">id of the product</a> .</td>
<td>tddy123uk</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       title      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Title of the item.</td>
<td>TN2351 black USB</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       description      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><a href="https://support.google.com/merchants/answer/6324468">Description</a> of the item.</td>
<td>The TN2351 black USB has redefined how XJS can impact LLCD experiences.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       link      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Merchant provided <a href="https://support.google.com/merchants/answer/6324416">URL of the landing page</a> of the product.</td>
<td>https://www.example.com/tn2351-black-usb/6538811?skuId=1234</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       mobile_link      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Merchant provided <a href="https://support.google.com/merchants/answer/6324459">URL of a mobile-optimized version</a> of the landing page.</td>
<td>https://www.example.com/tn2351-black-usb/6538811?skuId=1234</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       image_link      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Merchant provided <a href="https://support.google.com/merchants/answer/6324350">URL of the main product image</a> .</td>
<td>https://www.example.com/tn2351-black-usb/6538811?skuId=1234</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       additional_image_links      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code> , <code dir="ltr" translate="no">       REPEATED      </code></td>
<td>Merchant provided <a href="https://support.google.com/merchants/answer/6324370">additional URLs</a> of images of the item.</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       content_language      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The two-letter ISO 639-1 language code for the item.</td>
<td>en</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       target_country      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Deprecated (always set to NULL) as part of a change to allow products to <a href="https://support.google.com/merchants/answer/7448571">target multiple countries</a> . Instead, use the following fields to read the status of each targeted country: <a href="#destinations.approved_countries">destinations.approved_countries</a> , <a href="#destinations.pending_countries">destinations.pending_countries</a> , <a href="#destinations.disapproved_countries">destinations.disapproved_countries</a> . Issues can now apply to certain target countries and not others, as indicated in the field <a href="#issues.applicable_countries">issues.applicable_countries</a> .</td>
<td>null</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       feed_label      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The merchant provided <a href="https://support.google.com/merchants/answer/12453549">feed label</a> for the item, or <code dir="ltr" translate="no">       -      </code> if not provided.</td>
<td>US</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       channel      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The item's channel, either <code dir="ltr" translate="no">       online      </code> or <code dir="ltr" translate="no">       local      </code> .</td>
<td>local, online</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       expiration_date      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>Merchant provided date and time on which the <a href="https://support.google.com/merchants/answer/6324499">item should expire</a> , as specified upon insertion. Set to null if not provided.</td>
<td>2023-10-14 00:00:00 UTC</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       google_expiration_date      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>Date and time on which the item expires in Google Shopping. Never set to null.</td>
<td>2023-10-14 00:00:00 UTC</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       adult      </code></td>
<td><code dir="ltr" translate="no">       BOOLEAN      </code></td>
<td>Set to true if the item is <a href="https://support.google.com/merchants/answer/6324508">targeted towards adults.</a></td>
<td>true, false</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       age_group      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Merchant provided <a href="https://support.google.com/merchants/answer/6324463">target age group</a> of the item. NULL if not provided.</td>
<td>newborn, infant, toddler, kids, adult</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       availability      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Merchant provided <a href="https://support.google.com/merchants/answer/6324448">availability</a> status of the item.</td>
<td>in stock, out of stock</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       availability_date      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>Merchant provided date and time <a href="https://support.google.com/merchants/answer/6324470">when a pre-ordered product becomes available</a> for delivery. NULL if not provided.</td>
<td>2023-10-14 00:00:00 UTC</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       brand      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Merchant provided <a href="https://support.google.com/merchants/answer/6324351">brand</a> of the item. NULL if not provided.</td>
<td>Brand Name</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       google_brand_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Google brand ID of the item.</td>
<td>12759524623914508053</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       color      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Merchant provided <a href="https://support.google.com/merchants/answer/6324487">color</a> of the item. NULL if not provided.</td>
<td>Silver, Gray, Multi</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       condition      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Merchant provided <a href="https://support.google.com/merchants/answer/6324469">Condition</a> or state of the item.</td>
<td>new, used, refurbished</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       custom_labels      </code></td>
<td><code dir="ltr" translate="no">       RECORD      </code></td>
<td>Merchant provided <a href="https://support.google.com/merchants/answer/6324473">custom labels</a> for custom grouping of items in Shopping Ads. NULL if not provided.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       custom_labels.label_0      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Custom label 0.</td>
<td>my custom label</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       custom_labels.label_1      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Custom label 1.</td>
<td>my custom label</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       custom_labels.label_2      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Custom label 2.</td>
<td>my custom label</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       custom_labels.label_3      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Custom label 3.</td>
<td>my custom label</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       custom_labels.label_4      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Custom label 4.</td>
<td>my custom label</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       gender      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Merchant provided target <a href="https://support.google.com/merchants/answer/6324479">gender</a> of the item. NULL if not provided.</td>
<td>unisex, male, female</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       gtin      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Merchant provided <a href="https://support.google.com/merchants/answer/6324461">Global Trade Item Number (GTIN)</a> of the item. NULL if not provided.</td>
<td>3234567890126</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       item_group_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Merchant provided <a href="https://support.google.com/merchants/answer/6324507">Shared identifier</a> for all variants of the same product. NULL if not provided.</td>
<td>AB12345</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       material      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Merchant provided <a href="https://support.google.com/merchants/answer/6324410">material</a> of which the item is made. NULL if not provided.</td>
<td>Leather</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       mpn      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Merchant provided <a href="https://support.google.com/merchants/answer/6324482">Manufacturer Part Number</a> (MPN) of the item. Set to NULL if not provided.</td>
<td>GO12345OOGLE</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       pattern      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Merchant provided <a href="https://support.google.com/merchants/answer/6324483">pattern</a> . NULL if not provided.</td>
<td>Striped</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       price      </code></td>
<td><code dir="ltr" translate="no">       RECORD      </code></td>
<td>Merchant provided <a href="https://support.google.com/merchants/answer/6324371">price</a> of the item.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       price.value      </code></td>
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td>The price of the item.</td>
<td>19.99</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       price.currency      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The currency of the price.</td>
<td>USD</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       sale_price      </code></td>
<td><code dir="ltr" translate="no">       RECORD      </code></td>
<td>Merchant provided <a href="https://support.google.com/merchants/answer/6324471">sale price</a> of the item.</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       sale_price.value      </code></td>
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td>The sale price of the item. NULL if not provided.</td>
<td>19.99</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       sale_price.currency      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The currency of the sale price. NULL if not provided.</td>
<td>USD</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       sale_price_effective_start_date      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>Start date and time when the item is on sale.</td>
<td>2023-10-14 00:00:00 UTC</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       sale_price_effective_end_date      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>End date and time when the item is on sale.</td>
<td>2023-10-14 00:00:00 UTC</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       google_product_category      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>The item's <a href="https://support.google.com/merchants/answer/1705911">Google product category</a> ID. NULL if not provided.</td>
<td>2271</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       google_product_category_ids      </code></td>
<td><code dir="ltr" translate="no">       INTEGER, REPEATED      </code></td>
<td>The full path of <a href="https://support.google.com/merchants/answer/1705911">Google product categories</a> to the item, stored as a set of IDs. NULL if not provided.</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       google_product_category_path      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>A human-readable version of the full path. Empty if not provided.</td>
<td>Apparel &amp; Accessories &gt; Clothing &gt; Dresses</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       product_type      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Merchant-provided <a href="https://support.google.com/merchants/answer/6324406">category</a> of the item.</td>
<td>Home &gt; Women &gt; Dresses &gt; Maxi Dresses</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       additional_product_types      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code> , <code dir="ltr" translate="no">       REPEATED      </code></td>
<td>Additional categories of the item.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       promotion_ids      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code> , <code dir="ltr" translate="no">       REPEATED      </code></td>
<td>The list of <a href="https://support.google.com/merchants/answer/7050148">promotion IDs</a> associated with the product.</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       destinations      </code></td>
<td><code dir="ltr" translate="no">       RECORD      </code> , <code dir="ltr" translate="no">       REPEATED      </code></td>
<td>The intended destinations for the product.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       destinations.name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the destination; only <code dir="ltr" translate="no">       Shopping      </code> is supported. This corresponds to the <a href="https://support.google.com/merchants/answer/15130232">Marketing Methods</a> "Shopping Ads" and "Local Inventory Ads" in Merchant Center.</td>
<td>Shopping</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       destinations.status               *       </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Deprecated (always set to NULL) as part of a change to allow products to <a href="https://support.google.com/merchants/answer/7448571">target multiple countries</a> . Instead, use the following fields to read the status of each targeted country: <a href="#destinations.approved_countries">destinations.approved_countries</a> , <a href="#destinations.pending_countries">destinations.pending_countries</a> , <a href="#destinations.disapproved_countries">destinations.disapproved_countries</a> . Issues can now apply to certain target countries and not others, as indicated in the field <a href="#issues.applicable_countries">issues.applicable_countries</a> .</td>
<td>NULL</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       destinations.approved_countries      </code></td>
<td><code dir="ltr" translate="no">       STRING, REPEATED      </code></td>
<td>List of <a href="http://www.unicode.org/repos/cldr/tags/latest/common/main/en.xml">CLDR territory codes</a> where the offer is approved.</td>
<td>US, CH</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       destinations.pending_countries      </code></td>
<td><code dir="ltr" translate="no">       STRING, REPEATED      </code></td>
<td>List of <a href="http://www.unicode.org/repos/cldr/tags/latest/common/main/en.xml">CLDR territory codes</a> where the offer is pending.</td>
<td>US, CH</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       destinations.disapproved_countries      </code></td>
<td><code dir="ltr" translate="no">       STRING, REPEATED      </code></td>
<td>List of <a href="http://www.unicode.org/repos/cldr/tags/latest/common/main/en.xml">CLDR territory codes</a> where the offer is disapproved.</td>
<td>US, CH</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       issues      </code></td>
<td><code dir="ltr" translate="no">       RECORD      </code> , <code dir="ltr" translate="no">       REPEATED      </code></td>
<td>The list of item level issues associated with the product.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       issues.code      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The error code of the issue.</td>
<td>image_too_generic</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       issues.servability      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>How this issue affects serving of the offer.</td>
<td>disapproved, unaffected</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       issues.resolution      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Whether the issue can be resolved by the merchant.</td>
<td>merchant_action, pending_processing</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       issues.attribute_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The attribute's name, if the issue is caused by a single attribute. NULL otherwise.</td>
<td>image link</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       issues.destination      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The destination the issue applies to. Always set to <code dir="ltr" translate="no">       Shopping      </code> .</td>
<td>Shopping</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       issues.short_description      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Short issue description in English.</td>
<td>Generic image</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       issues.detailed_description      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Detailed issue description in English.</td>
<td>Use an image that shows the product</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       issues.documentation      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>URL of a web page to help with resolving this issue.</td>
<td>https://support.google.com/merchants/answer/6098288</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       issues.applicable_countries      </code></td>
<td><code dir="ltr" translate="no">       STRING, REPEATED      </code></td>
<td>List of <a href="http://www.unicode.org/repos/cldr/tags/latest/common/main/en.xml">CLDR territory codes</a> where the issue applies.</td>
<td>CH</td>
</tr>
</tbody>
</table>

## Query examples

### Products and product issues statistics

The following SQL sample query provides the number of products, products with issues, and issues by day.

``` text
SELECT
  _PARTITIONDATE AS date,
  COUNT(*) AS num_products,
  COUNTIF(ARRAY_LENGTH(issues) > 0) AS num_products_with_issues,
  SUM(ARRAY_LENGTH(issues)) AS num_issues
FROM
  dataset.Products_merchant_id
WHERE
  _PARTITIONDATE >= 'YYYY-MM-DD'
GROUP BY
  date
ORDER BY
  date DESC
```

### Products disapproved for Shopping Ads

The following SQL sample query provides the number of products that are not approved for display in Shopping Ads, separated by country. Disapproval can result from the destination being [excluded](https://support.google.com/merchants/answer/6324486) or because of an issue with the product.

``` text
SELECT
  _PARTITIONDATE AS date,
  disapproved_country,
  COUNT(*) AS num_products
FROM
  dataset.Products_merchant_id,
  UNNEST(destinations) AS destination,
  UNNEST(disapproved_countries) AS disapproved_country
WHERE
  _PARTITIONDATE >= 'YYYY-MM-DD'
GROUP BY
  date, disapproved_country
ORDER BY
  date DESC
```

### Products with disapproved issues

The following SQL sample query retrieves the number of products with disapproved issues, separated by country.

``` text
SELECT
  _PARTITIONDATE AS date,
  applicable_country,
  COUNT(DISTINCT CONCAT(CAST(merchant_id AS STRING), ':', product_id))
      AS num_distinct_products
FROM
  dataset.Products_merchant_id,
  UNNEST(issues) AS issue,
  UNNEST(issue.applicable_countries) as applicable_country
WHERE
  _PARTITIONDATE >= 'YYYY-MM-DD' AND
  issue.servability = 'disapproved'
GROUP BY
  date, applicable_country
ORDER BY
  date DESC
```

**Note:** This query constructs a unique key by using `  merchant_id  ` and `  product_id  ` . This is only required if you have an MCA account. When you use an MCA account, there is the potential for `  product_id  ` collisions across multiple sub-accounts.
