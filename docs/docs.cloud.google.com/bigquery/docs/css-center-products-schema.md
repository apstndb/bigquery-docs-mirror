# Comparison Shopping Services Center table schema

When your Comparison Shopping Service (CSS) Center reporting data is transferred to BigQuery, the format of product and product issues data corresponds primarily to the format of the relevant fields of the Content API's [`  ProductView  `](https://developers.google.com/shopping-content/reference/rest/v2.1/reports/search#productview) and [`  Productstatuses  `](https://developers.google.com/shopping-content/v2/reference/v2.1/productstatuses) resources.

## CSS Center Products Schema

The following table lists the schema for the `  Products_  ` table. Some fields are included as subsets of other fields. For example, the `  Price  ` field contain both `  Value  ` and `  Currency  ` fields.

<table>
<thead>
<tr class="header">
<th><p>Field name</p></th>
<th><p>Type</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CSS ID</p></td>
<td><p><code dir="ltr" translate="no">        INTEGER       </code></p></td>
<td><p>CSS ID</p></td>
</tr>
<tr class="even">
<td><p>Merchant ID</p></td>
<td><p><code dir="ltr" translate="no">        INTEGER       </code></p></td>
<td><p>Merchant account ID who owns the offer</p></td>
</tr>
<tr class="odd">
<td><p>Product ID</p></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>A unique identifier of the item</p></td>
</tr>
<tr class="even">
<td><p>Feed label</p></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>The feed label for the item, or "-" if not provided</p></td>
</tr>
<tr class="odd">
<td><p>Language code</p></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>The two-letter ISO 639-1 language code for the item</p></td>
</tr>
<tr class="even">
<td><p>Channel</p></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>The item's channel, either <code dir="ltr" translate="no">        online       </code> or <code dir="ltr" translate="no">        local       </code></p></td>
</tr>
<tr class="odd">
<td><p>Title</p></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>Title of the item</p></td>
</tr>
<tr class="even">
<td><p>Brand</p></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>Brand of the item</p></td>
</tr>
<tr class="odd">
<td>Category l{1-5}</td>
<td><p><code dir="ltr" translate="no">        INTEGER       </code></p></td>
<td><p>Google Product Category of the item</p></td>
</tr>
<tr class="even">
<td>Product type l{1-5}</td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>Product type of the item</p></td>
</tr>
<tr class="odd">
<td><p>Price</p></td>
<td><p><code dir="ltr" translate="no">        RECORD       </code></p></td>
<td><p>Full price of the item, prior to any discounts</p></td>
</tr>
<tr class="even">
<td><p>Value</p></td>
<td><p><code dir="ltr" translate="no">        INTEGER       </code></p></td>
<td><p>Price value of the item</p></td>
</tr>
<tr class="odd">
<td><p>Currency</p></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>The currency of the price</p></td>
</tr>
<tr class="even">
<td><p>Sale Price</p></td>
<td><p><code dir="ltr" translate="no">        RECORD       </code></p></td>
<td><p>Sale price of the item, if applicable</p></td>
</tr>
<tr class="odd">
<td><p>Value</p></td>
<td><p><code dir="ltr" translate="no">        INTEGER       </code></p></td>
<td><p>Sale price value of the item</p></td>
</tr>
<tr class="even">
<td><p>Currency</p></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>The currency of the sale price</p></td>
</tr>
<tr class="odd">
<td><p>Condition</p></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>Condition or state of the item</p></td>
</tr>
<tr class="even">
<td><p>Availability</p></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>Availability status of the item</p></td>
</tr>
<tr class="odd">
<td><p>Shipping label</p></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>The shipping label specified in the feed</p></td>
</tr>
<tr class="even">
<td><p>Gtin</p></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p><a href="https://support.google.com/merchants/answer/188494#gtin">Global Trade Item Number</a> (GTIN) of the item</p></td>
</tr>
<tr class="odd">
<td><p>Item group ID</p></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>Shared identifier for all variants of the same product</p></td>
</tr>
<tr class="even">
<td><p>Creation time</p></td>
<td><p><code dir="ltr" translate="no">        INTEGER       </code></p></td>
<td><p>The time this item was created by the provider as timestamp microseconds</p></td>
</tr>
<tr class="odd">
<td><p>Expiration date</p></td>
<td><p><code dir="ltr" translate="no">        DATE       </code></p></td>
<td><p>Date on which the item should expire, as specified upon insertion</p></td>
</tr>
<tr class="even">
<td><p>Aggregated reporting context status</p></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>The status of the product aggregated for all reporting contexts. The supported values are <code dir="ltr" translate="no">        ELIGIBLE       </code> , <code dir="ltr" translate="no">        ELIGIBLE_LIMITED       </code> , <code dir="ltr" translate="no">        PENDING       </code> , <code dir="ltr" translate="no">        NOT_ELIGIBLE_OR_DISAPPROVED       </code> , <code dir="ltr" translate="no">        AGGREGATED_STATUS_UNSPECIFIED       </code></p></td>
</tr>
<tr class="odd">
<td><p>Reporting context statuses</p></td>
<td><p><code dir="ltr" translate="no">        RECORD       </code> , <code dir="ltr" translate="no">        REPEATED       </code></p></td>
<td><p>The status of the product in each reporting context and region</p></td>
</tr>
<tr class="even">
<td><p>Reporting context</p></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>Reporting context</p></td>
</tr>
<tr class="odd">
<td><p>Region and status</p></td>
<td><p><code dir="ltr" translate="no">        RECORD       </code> , <code dir="ltr" translate="no">        REPEATED       </code></p></td>
<td><p>Status per region</p></td>
</tr>
<tr class="even">
<td><p>Region</p></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>Region code represented in ISO 3166 format</p></td>
</tr>
<tr class="odd">
<td><p>Status</p></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>Status of the product in the region, can be <code dir="ltr" translate="no">        ELIGIBLE       </code> , <code dir="ltr" translate="no">        PENDING       </code> , or <code dir="ltr" translate="no">        DISAPPROVED       </code></p></td>
</tr>
<tr class="even">
<td><p>Item issues</p></td>
<td><p><code dir="ltr" translate="no">        RECORD       </code> , <code dir="ltr" translate="no">        REPEATED       </code></p></td>
<td><p>The list of item level issues associated with the product</p></td>
</tr>
<tr class="odd">
<td><p>Type</p></td>
<td><p><code dir="ltr" translate="no">        RECORD       </code></p></td>
<td><p>Issue type</p></td>
</tr>
<tr class="even">
<td><p>Code</p></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>The error code of the issue, equivalent to the <a href="https://developers.google.com/shopping-content/guides/product-issues"><code dir="ltr" translate="no">         code        </code></a> of Product issues</p></td>
</tr>
<tr class="odd">
<td><p>Canonical attribute</p></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>Canonical attribute name for attribute-specific issues</p></td>
</tr>
<tr class="even">
<td><p>Severity</p></td>
<td><p><code dir="ltr" translate="no">        RECORD       </code></p></td>
<td><p>How this issue affects serving of the offer</p></td>
</tr>
<tr class="odd">
<td><p>Severity per reporting context</p></td>
<td><p><code dir="ltr" translate="no">        RECORD       </code> , <code dir="ltr" translate="no">        REPEATED       </code></p></td>
<td><p>Issue severity per reporting context</p></td>
</tr>
<tr class="even">
<td><p>Reporting context</p></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>Reporting context the issue applies to</p></td>
</tr>
<tr class="odd">
<td><p>Disapproved regions</p></td>
<td><p><code dir="ltr" translate="no">        STRING       </code> , <code dir="ltr" translate="no">        REPEATED       </code></p></td>
<td><p>List of disapproved regions in the reporting context, represented in ISO 3166 format</p></td>
</tr>
<tr class="even">
<td><p>Demoted regions</p></td>
<td><p><code dir="ltr" translate="no">        STRING       </code> , <code dir="ltr" translate="no">        REPEATED       </code></p></td>
<td><p>List of demoted regions in the reporting context, represented in ISO 3166 format</p></td>
</tr>
<tr class="odd">
<td><p>Aggregated severity</p></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>Aggregated severity of the issue for all reporting contexts it affects. Its values can be <code dir="ltr" translate="no">        AGGREGATED_ISSUE_SEVERITY_UNSPECIFIED       </code> , <code dir="ltr" translate="no">        DISAPPROVED       </code> , <code dir="ltr" translate="no">        DEMOTED       </code> , or <code dir="ltr" translate="no">        PENDING       </code></p></td>
</tr>
<tr class="even">
<td><p>Resolution</p></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>Whether the issue can be resolved by the merchant</p></td>
</tr>
</tbody>
</table>
