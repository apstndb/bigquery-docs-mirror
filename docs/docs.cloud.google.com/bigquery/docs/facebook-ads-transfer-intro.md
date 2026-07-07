---
name: documents/docs.cloud.google.com/bigquery/docs/facebook-ads-transfer-intro
uri: https://docs.cloud.google.com/bigquery/docs/facebook-ads-transfer-intro
title: Introduction to Facebook Ads transfers
description: Learn how to use the BigQuery Data Transfer Service Facebook Ads connector to ingest data from Facebook Ads into BigQuery.
data_source: docs.cloud.google.com
---

# Introduction to Facebook Ads transfers

You can load data from Facebook Ads to BigQuery using the [BigQuery Data Transfer Service](https://docs.cloud.google.com/bigquery/docs/dts-introduction) for Facebook Ads connector. With BigQuery Data Transfer Service, you can schedule recurring transfer jobs that add your latest data from your Facebook Ads to BigQuery.

The BigQuery Data Transfer Service for the Facebook Ads connector supports the following options for your data transfer.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Data transfer options</th>
<th>Support</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Supported reports</td>
<td>The BigQuery Data Transfer Service for Facebook Ads supports the transfer of the following Facebook Ads reports:
<ul>
<li><code dir="ltr" translate="no">AdAccounts</code></li>
<li><code dir="ltr" translate="no">AdInsights</code></li>
<li><code dir="ltr" translate="no">AdInsightsActions</code></li>
<li><p><code dir="ltr" translate="no">AdInsightsMMM</code><br />
</p>
<blockquote>
<strong>Note:</strong> Support for this report is temporarily disabled. For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/transfer-changes#Jul06-fb-ads">July 06, 2026</a>
</blockquote></li>
<li><code dir="ltr" translate="no">Ads</code></li>
<li><code dir="ltr" translate="no">AdCreatives</code></li>
<li><code dir="ltr" translate="no">AdSets</code></li>
<li><code dir="ltr" translate="no">Campaigns</code></li>
<li><code dir="ltr" translate="no">AdImages</code></li>
<li><code dir="ltr" translate="no">AdLabels</code></li>
<li><code dir="ltr" translate="no">Businesses</code></li>
<li><code dir="ltr" translate="no">CustomAudiences</code></li>
</ul>
<p>For information about how Facebook Ads reports are transformed into BigQuery tables and views, see <a href="https://docs.cloud.google.com/bigquery/docs/facebook-ads-transformation">Facebook Ads report transformation</a> .</p></td>
</tr>
<tr class="even">
<td>Repeat frequency</td>
<td>The Facebook Ads connector supports daily data transfers.<br />
<br />
By default, data transfers are scheduled at the time when the data transfer is created. You can configure the time of data transfer when you <a href="https://docs.cloud.google.com/bigquery/docs/facebook-ads-transfer#fb_ads_transfer_setup">set up your data transfer</a> .</td>
</tr>
<tr class="odd">
<td>Refresh window</td>
<td>The Facebook Ads connector retrieves Facebook Ads data from up to 30 days at the time the data transfer is run. You cannot configure the refresh window for this connector.<br />
<br />
For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/facebook-ads-transfer-intro#refresh">Refresh windows</a> .</td>
</tr>
<tr class="even">
<td>Backfill data availability</td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/working-with-transfers#manually_trigger_a_transfer">Run a data backfill</a> to retrieve data outside of your scheduled data transfer. You can retrieve data as far back as the data retention policy on your data source allows.</td>
</tr>
</tbody>
</table>

To learn how to schedule a Facebook Ads transfer, see [Load Facebook Ads data into BigQuery](https://docs.cloud.google.com/bigquery/docs/facebook-ads-transfer) .

## Data ingestion from Facebook Ads transfers

When you transfer data from Facebook Ads into BigQuery, the data is loaded into BigQuery tables that are partitioned by date. The table partition that the data is loaded into corresponds to the date from the data source. If you schedule multiple transfers for the same date, BigQuery Data Transfer Service overwrites the partition for that specific date with the latest data. Multiple transfers in the same day or running backfills don't result in duplicate data, and partitions for other dates are not affected.

Some ingestion behaviors differ between different Facebook Ads reports:

  - For `AdAccounts` , `AdCreatives` , `AdImages` , `AdLabels` , `Businesses` , and `CustomAudiences` tables, snapshots are taken once a day and stored in the partition of the last transfer run date.

  - Data transfers for the `AdInsights` , `AdInsightActions` , `Ads` , `AdSets` and `Campaigns` tables will transfer Facebook Ads data that corresponds to the run date of the transfer. For these tables, if you specify a `insightsTimeIncrement` value that is more than 1, then the data transfer includes data from a number of days before the run date according to the `insightsTimeIncrement` value, including the run date. For example, if the `insightsTimeIncrement` value is 3, then the data transfer only includes data from the run date and data from 2 days before the run date, for a total of 3 days of data.

  - For `AdInsights` and `AdInsightsActions` tables, the table partition that the data is loaded into corresponds to the date from the data source.

  - The [refresh window](https://docs.cloud.google.com/bigquery/docs/facebook-ads-transfer-intro#refresh) only applies to the `AdInsights` and `AdInsightsActions` tables.

### Refresh windows

A *refresh window* is the number of days that a data transfer retrieves data when a data transfer occurs. For example, if the refresh window is three days and a daily transfer occurs, the BigQuery Data Transfer Service retrieves all data from your source table from the past three days. In this example, when a daily transfer occurs, the BigQuery Data Transfer Service creates a new BigQuery destination table partition with a copy of your source table data from the current day, then automatically triggers backfill runs to update the BigQuery destination table partitions with your source table data from the past two days. The automatically triggered backfill runs will either overwrite or incrementally update your BigQuery destination table, depending on whether or not incremental updates are supported in the BigQuery Data Transfer Service connector.

When you run a data transfer for the first time, the data transfer retrieves all source data available within the refresh window. For example, if the refresh window is three days and you run the data transfer for the first time, the BigQuery Data Transfer Service retrieves all source data within three days.

To retrieve data outside the refresh window, such as historical data, or to recover data from any transfer outages or gaps, you can initiate or schedule a [backfill run](https://docs.cloud.google.com/bigquery/docs/working-with-transfers#manually_trigger_a_transfer) .

## Pricing

For pricing information about Facebook Ads transfers, see [Data Transfer Service pricing](https://docs.cloud.google.com/bigquery/pricing#data-transfer-service-pricing) .

## What's next

  - Learn about [scheduling a Facebook Ads transfer](https://docs.cloud.google.com/bigquery/docs/facebook-ads-transfer) .
  - Learn more about the [BigQuery Data Transfer Service](https://docs.cloud.google.com/bigquery/docs/dts-introduction) .
