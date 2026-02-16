# Google Merchant Center Product Targeting table

## Overview

Product targeting data helps merchants understand which products are targeted by the Shopping and Performance Max campaigns in each linked advertiser account that they can access.

  - All campaign targeting parameters are considered, such as [listing groups](https://support.google.com/google-ads/answer/11596074) , [product groups](https://support.google.com/google-ads/answer/6275317) , and [feed labels](https://support.google.com/merchants/answer/14994087) .
  - Only active campaigns with active ad groups or asset groups are considered.
  - To compute the `  targeting_status  ` , we only consider advertiser accounts that are accessible to the user who owns the BigQuery export. For more information, see [Manage access to your Google Ads account](https://support.google.com/google-ads/answer/6372672) .

## Table name

If you choose the **Product Targeting** report option when you [set up a Google Merchant Center transfer](/bigquery/docs/merchant-center-transfer-schedule-transfers#set_up_a_google_merchant_center_transfer) , BigQuery creates a table for the data during the transfer. The table name starts with the `  ProductTargeting_  ` prefix:

  - If you configured the transfer with an individual merchant ID, the table name is `  ProductTargeting_ MERCHANT_ID  ` .
  - If you configured the transfer with an MCA account, the table name is `  ProductTargeting_ AGGREGATOR_ID  ` .

## Schema

The Product Targeting table has the following schema:

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Name</th>
<th>Type</th>
<th>Description</th>
<th>Example data</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       product_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The Content API REST ID for the product is in the format: <code dir="ltr" translate="no">       channel:content_language:feed_label:offer_id      </code> . This field is a primary key.</td>
<td>online:en:AU:666840730</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         advertiser_id       </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>Advertiser ID of the campaign. This field is a primary key.</td>
<td>4321</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       targeting_status      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Whether the product is targeted by Ads campaigns.<br />

<strong>Note:</strong> Products targeted by Ads campaigns might not be eligible to serve. To check if your products are eligible, use the <code dir="ltr" translate="no">        destinations.status       </code> field of the <a href="/bigquery/docs/merchant-center-products-schema">Products report</a> .</td>
<td>TARGETED, NOT_TARGETED</td>
</tr>
</tbody>
</table>
