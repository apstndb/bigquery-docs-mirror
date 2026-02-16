# Search Ads 360 report transformation

This document describes how you can transform your reports for Search Ads 360.

To see the Search Ads 360 report transformation that uses the old Search Ads 360 reporting API, see [Search Ads 360 report transformation (Deprecated)](/bigquery/docs/sa360-transformation) .

## Table mapping for Search Ads 360 reports

When your Search Ads 360 reports are transferred to BigQuery, the reports are transformed into the following BigQuery tables and views. When you view the tables and views in BigQuery, the value for customer\_id is your Search Ads 360 customer ID.

### ad\_group

[ad\_group](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/ad_group)

  - Tables:  
    p\_sa\_AdGroup\_ customer\_id  
    p\_sa\_AdGroupConversionActionAndDeviceStats\_ customer\_id  
    p\_sa\_AdGroupDeviceStats\_ customer\_id  
    p\_sa\_AdGroupStats\_ customer\_id
  - Views:  
    sa\_AdGroup\_ customer\_id  
    sa\_AdGroupConversionActionAndDeviceStats\_ customer\_id  
    sa\_AdGroupDeviceStats\_ customer\_id  
    sa\_AdGroupStats\_ customer\_id

### ad\_group\_ad

[ad\_group\_ad](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/ad_group_ad)

  - Tables:  
    p\_sa\_Ad\_ customer\_id  
    p\_sa\_AdConversionActionAndDeviceStats\_ customer\_id  
    p\_sa\_AdDeviceStats\_ customer\_id
  - Views:  
    a\_Ad\_ customer\_id  
    sa\_AdConversionActionAndDeviceStats\_ customer\_id  
    sa\_AdDeviceStats\_ customer\_id

### ad\_group\_asset

[ad\_group\_asset](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/ad_group_asset)

  - Tables:  
    p\_sa\_AdGroupAssetStats\_ customer\_id  
    p\_sa\_AdGroupConversionActionAndAssetStats\_ customer\_id
  - Views:  
    sa\_AdGroupAssetStats\_ customer\_id  
    sa\_AdGroupConversionActionAndAssetStats\_ customer\_id

### ad\_group\_audience\_view

[ad\_group\_audience\_view](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/ad_group_audience_view)

  - Tables:  
    p\_sa\_AdGroupAudienceConversionActionAndDeviceStats\_ customer\_id  
    p\_sa\_AdGroupAudienceDeviceStats\_ customer\_id
  - Views:  
    sa\_AdGroupAudienceConversionActionAndDeviceStats\_ customer\_id  
    sa\_AdGroupAudienceDeviceStats\_ customer\_id

### ad\_group\_criterion

[ad\_group\_criterion](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/ad_group_criterion)

  - Tables:  
    p\_sa\_AdGroupCriterion\_ customer\_id  
    p\_sa\_NegativeAdGroupCriterion\_ customer\_id  
    p\_sa\_NegativeAdGroupKeyword\_ customer\_id
  - Views:  
    sa\_AdGroupCriterion\_ customer\_id  
    sa\_NegativeAdGroupCriterion\_ customer\_id  
    sa\_NegativeAdGroupKeyword\_ customer\_id

### ad\_group\_label

[ad\_group\_label](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/ad_group_label)

  - Tables:  
    p\_sa\_AdGroupLabel\_ customer\_id  
  - Views:  
    sa\_AdGroupLabel\_ customer\_id  

### age\_range\_view

[age\_range\_view](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/age_range_view)

  - Tables:  
    p\_sa\_AgeRangeConversionActionAndDeviceStats\_ customer\_id  
    p\_sa\_AgeRangeDeviceStats\_ customer\_id
  - Views:  
    sa\_AgeRangeConversionActionAndDeviceStats\_ customer\_id  
    sa\_AgeRangeDeviceStats\_ customer\_id

### asset

[asset](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/asset)

  - Tables:  
    p\_sa\_Asset\_ customer\_id
  - Views:  
    sa\_Asset\_ customer\_id

### asset\_set\_asset

[asset\_set\_asset](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/asset_set_asset)

  - Tables:  
    p\_sa\_AccountConversionActionAndAssetStats\_ customer\_id  
    p\_sa\_AssetSetStats\_ customer\_id
  - Views:  
    sa\_AccountConversionActionAndAssetStats\_ customer\_id  
    sa\_AssetSetStats\_ customer\_id

### bidding\_strategy

[bidding\_strategy](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/bidding_strategy)

  - Tables:  
    p\_sa\_BidStrategy\_ customer\_id  
    p\_sa\_BidStrategyStats\_ customer\_id
  - Views:  
    sa\_BidStrategy\_ customer\_id  
    sa\_BidStrategyStats\_ customer\_id

### campaign

[campaign](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/campaign)

  - Tables:  
    p\_sa\_Campaign\_ customer\_id  
    p\_sa\_CampaignConversionActionAndDeviceStats\_ customer\_id  
    p\_sa\_CampaignDeviceStats\_ customer\_id  
    p\_sa\_CampaignStats\_ customer\_id
  - Views:  
    sa\_Campaign\_ customer\_id  
    sa\_CampaignConversionActionAndDeviceStats\_ customer\_id  
    sa\_CampaignDeviceStats\_ customer\_id  
    sa\_CampaignStats\_ customer\_id

### campaign\_asset

[campaign\_asset](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/campaign_asset)

  - Tables:  
    p\_sa\_CampaignAssetStats\_ customer\_id  
    p\_sa\_CampaignConversionActionAndAssetStats\_ customer\_id
  - Views:  
    sa\_CampaignAssetStats\_ customer\_id  
    sa\_CampaignConversionActionAndAssetStats\_ customer\_id

### campaign\_audience\_view

[campaign\_audience\_view](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/campaign_audience_view)

  - Tables:  
    p\_sa\_CampaignAudienceConversionActionAndDeviceStats\_ customer\_id  
    p\_sa\_CampaignAudienceDeviceStats\_ customer\_id
  - Views:  
    sa\_CampaignAudienceConversionActionAndDeviceStats\_ customer\_id  
    sa\_CampaignAudienceDeviceStats\_ customer\_id

### campaign\_criterion

[campaign\_criterion](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/campaign_criterion)

  - Tables:  
    p\_sa\_CampaignCriterion\_ customer\_id  
    p\_sa\_NegativeCampaignCriterion\_ customer\_id  
    p\_sa\_NegativeCampaignKeyword\_ customer\_id
  - Views:  
    sa\_CampaignCriterion\_ customer\_id  
    sa\_NegativeCampaignCriterion\_ customer\_id  
    sa\_NegativeCampaignKeyword\_ customer\_id

### campaign\_label

[campaign\_label](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/campaign_label)

  - Tables:  
    p\_sa\_CampaignLabel\_ customer\_id  
  - Views:  
    sa\_CampaignLabel\_ customer\_id  

### cart\_data\_sales\_view

[cart\_data\_sales\_view](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/cart_data_sales_view)

  - Tables:  
    p\_sa\_CartDataSalesStats\_ customer\_id
  - Views:  
    sa\_CartDataSalesStats\_ customer\_id

### conversion

[conversion](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/conversion)

  - Tables:  
    p\_sa\_Conversion\_ customer\_id
  - Views:  
    sa\_Conversion\_ customer\_id

### conversion\_action

[conversion\_action](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/conversion_action)

  - Tables:  
    p\_sa\_ConversionAction\_ customer\_id
  - Views:  
    sa\_ConversionAction\_ customer\_id

### customer

[customer](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/customer)

  - Tables:  
    p\_sa\_Account\_ customer\_id  
    p\_sa\_AccountConversionActionAndDeviceStats\_ customer\_id  
    p\_sa\_AccountDeviceStats\_ customer\_id  
    p\_sa\_AccountStats\_ customer\_id
  - Views:  
    sa\_Account\_ customer\_id  
    sa\_AccountConversionActionAndDeviceStats\_ customer\_id  
    sa\_AccountDeviceStats\_ customer\_id  
    sa\_AccountStats\_ customer\_id

### customer\_asset

[customer\_asset](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/customer_asset)

  - Tables:  
    p\_sa\_AccountAssetStats\_ customer\_id
  - Views:  
    sa\_AccountAssetStats\_ customer\_id

### gender\_view

[gender\_view](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/gender_view)

  - Tables:  
    p\_sa\_GenderConversionActionAndDeviceStats\_ customer\_id  
    p\_sa\_GenderDeviceStats\_ customer\_id
  - Views:  
    sa\_GenderConversionActionAndDeviceStats\_ customer\_id  
    sa\_GenderDeviceStats\_ customer\_id

### keyword\_view

[keyword\_view](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/keyword_view)

  - Tables:  
    p\_sa\_Keyword\_ customer\_id  
    p\_sa\_KeywordConversionActionAndDeviceStats\_ customer\_id  
    p\_sa\_KeywordDeviceStats\_ customer\_id  
    p\_sa\_KeywordStats\_ customer\_id
  - Views:  
    sa\_Keyword\_ customer\_id  
    sa\_KeywordConversionActionAndDeviceStats\_ customer\_id  
    sa\_KeywordDeviceStats\_ customer\_id  
    sa\_KeywordStats\_ customer\_id

### location\_view

[location\_view](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/location_view)

  - Tables:  
    p\_sa\_LocationConversionActionAndDeviceStats\_ customer\_id  
    p\_sa\_LocationDeviceStats\_ customer\_id
  - Views:  
    sa\_LocationConversionActionAndDeviceStats\_ customer\_id  
    sa\_LocationDeviceStats\_ customer\_id

### product\_group\_view

[product\_group\_view](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/product_group_view)

  - Tables:  
    p\_sa\_ProductGroup\_ customer\_id  
    p\_sa\_ProductGroupStats\_ customer\_id
  - Views:  
    sa\_ProductGroup\_ customer\_id  
    sa\_ProductGroupStats\_ customer\_id

### shopping\_performance\_view

[shopping\_performance\_view](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/shopping_performance_view)

  - Tables:  
    p\_sa\_ProductAdvertised\_ customer\_id  
    p\_sa\_ProductAdvertisedConversionActionAndDeviceStats\_ customer\_id  
    p\_sa\_ProductAdvertisedDeviceStats\_ customer\_id
  - Views:  
    sa\_ProductAdvertised\_ customer\_id  
    sa\_ProductAdvertisedConversionActionAndDeviceStats\_ customer\_id  
    sa\_ProductAdvertisedDeviceStats\_ customer\_id

### visit

[visit](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/visit)

  - Tables:  
    p\_sa\_Visit\_ customer\_id
  - Views:  
    sa\_Visit\_ customer\_id

### webpage\_view

[webpage\_view](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/webpage_view)

  - Tables:  
    p\_sa\_WebpageConversionActionAndDeviceStats\_ customer\_id  
    p\_sa\_WebpageDeviceStats\_ customer\_id
  - Views:  
    sa\_WebpageConversionActionAndDeviceStats\_ customer\_id  
    sa\_WebpageDeviceStats\_ customer\_id

## Column details for Search Ads 360 reports

The BigQuery tables created by a Search Ads 360 transfer consist of the following columns (fields):

Search Ads 360 Table Name: Account

Search Ads 360 API Resource: [customer](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/customer)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>customer_account_level</td>
<td>The account level of the customer: Manager, Sub-manager, Associate manager or Service account.</td>
</tr>
<tr class="even">
<td>customer_account_type</td>
<td>Engine account type. For example: Google Ads, Microsoft Advertising, Yahoo Japan, Baidu, Facebook, Engine Track.</td>
</tr>
<tr class="odd">
<td>customer_creation_time</td>
<td>The timestamp when this customer was created. The timestamp is in the customer's time zone and in "yyyy-MM-dd HH:mm:ss" format.</td>
</tr>
<tr class="even">
<td>customer_currency_code</td>
<td>The currency in which the account operates. A subset of the currency codes from the ISO 4217 standard is supported.</td>
</tr>
<tr class="odd">
<td>customer_descriptive_name</td>
<td>Optional, non-unique descriptive name of the customer.</td>
</tr>
<tr class="even">
<td>customer_manager_descriptive_name</td>
<td>The descriptive name of the manager.</td>
</tr>
<tr class="odd">
<td>customer_sub_manager_descriptive_name</td>
<td>The descriptive name of the sub manager.</td>
</tr>
<tr class="even">
<td>customer_associate_manager_descriptive_name</td>
<td>The descriptive name of the associate manager.</td>
</tr>
<tr class="odd">
<td>customer_engine_id</td>
<td>ID of the account in the external engine account.</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
<tr class="odd">
<td>customer_manager_id</td>
<td>The customer ID of the manager.</td>
</tr>
<tr class="even">
<td>customer_sub_manager_id</td>
<td>The customer ID of the sub manager.</td>
</tr>
<tr class="odd">
<td>customer_associate_manager_id</td>
<td>The customer ID of the associate manager.</td>
</tr>
<tr class="even">
<td>customer_last_modified_time</td>
<td>The datetime when this customer was last modified. The datetime is in the customer's time zone and in "yyyy-MM-dd HH:mm:ss.ssssss" format.</td>
</tr>
<tr class="odd">
<td>customer_status</td>
<td>The status of the customer.</td>
</tr>
<tr class="even">
<td>customer_time_zone</td>
<td>The local timezone ID of the customer.</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: AccountAssetStats

Search Ads 360 API Resource: [customer\_asset](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/customer_asset)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>customer_asset_asset</td>
<td>Required. Immutable. The asset which is linked to the customer.</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
<tr class="odd">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
</tr>
<tr class="even">
<td>metrics_average_cpm</td>
<td>Average cost-per-thousand impressions (CPM).</td>
</tr>
<tr class="odd">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
</tr>
<tr class="even">
<td>metrics_client_account_conversions</td>
<td>The number of client account conversions. This only includes conversion actions which include_in_client_account_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies will optimize for these conversions.</td>
</tr>
<tr class="odd">
<td>metrics_client_account_conversions_value</td>
<td>The value of client account conversions. This only includes conversion actions which include_in_client_account_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies will optimize for these conversions.</td>
</tr>
<tr class="even">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
</tr>
<tr class="odd">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
</tr>
<tr class="even">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply, in yyyy-MM-dd format. For example: 2024-04-17</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: AccountConversionActionAndAssetStats

Search Ads 360 API Resource: [asset\_set\_asset](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/asset_set_asset)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>asset_set_asset_asset</td>
<td>Immutable. The asset which this asset set asset is linking to.</td>
</tr>
<tr class="even">
<td>asset_set_asset_asset_set</td>
<td>Immutable. The asset set which this asset set asset is linking to.</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
<tr class="even">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This includes all conversions regardless of the value of include_in_conversions_metric.</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions_value</td>
<td>The value of all conversions.</td>
</tr>
<tr class="even">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on an ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
</tr>
<tr class="odd">
<td>metrics_cross_device_conversions_value</td>
<td>The sum of the value of cross-device conversions.</td>
</tr>
<tr class="even">
<td>segments.conversion_action_name</td>
<td>Conversion action name.</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply, in yyyy-MM-dd format. For example: 2024-04-17</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: AccountConversionActionAndDeviceStats

Search Ads 360 API Resource: [customer](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/customer)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>customer_engine_id</td>
<td>ID of the account in the external engine account.</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This includes all conversions regardless of the value of include_in_conversions_metric.</td>
</tr>
<tr class="even">
<td>metrics_all_conversions_value</td>
<td>The value of all conversions.</td>
</tr>
<tr class="odd">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on an ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
</tr>
<tr class="even">
<td>metrics_cross_device_conversions_value</td>
<td>The sum of the value of cross-device conversions.</td>
</tr>
<tr class="odd">
<td>segments.conversion_action_name</td>
<td>Conversion action name.</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply, in yyyy-MM-dd format. For example: 2024-04-17</td>
</tr>
<tr class="odd">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: AccountDeviceStats

Search Ads 360 API Resource: [customer](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/customer)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>customer_engine_id</td>
<td>ID of the account in the external engine account.</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
<tr class="odd">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
</tr>
<tr class="even">
<td>metrics_average_cpm</td>
<td>Average cost-per-thousand impressions (CPM).</td>
</tr>
<tr class="odd">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
</tr>
<tr class="even">
<td>metrics_client_account_conversions</td>
<td>The number of client account conversions. This only includes conversion actions which include_in_client_account_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies will optimize for these conversions.</td>
</tr>
<tr class="odd">
<td>metrics_client_account_conversions_value</td>
<td>The value of client account conversions. This only includes conversion actions which include_in_client_account_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies will optimize for these conversions.</td>
</tr>
<tr class="even">
<td>metrics_client_account_view_through_conversions</td>
<td>The total number of view-through conversions. These happen when a customer sees an image or rich media ad, then later completes a conversion on your site without interacting with (for example, clicking on) another ad.</td>
</tr>
<tr class="odd">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
</tr>
<tr class="even">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
</tr>
<tr class="odd">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
</tr>
<tr class="even">
<td>metrics_visits</td>
<td>Clicks that Search Ads 360 has successfully recorded and forwarded to an advertiser's landing page.</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply, in yyyy-MM-dd format. For example: 2024-04-17</td>
</tr>
<tr class="even">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: AccountStats

Search Ads 360 API Resource: [customer](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/customer)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>customer_engine_id</td>
<td>ID of the account in the external engine account.</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
<tr class="odd">
<td>metrics_content_budget_lost_impression_share</td>
<td>The estimated percent of times that your ad was eligible to show on the Search Network but didn't because your budget was too low. Note: Search budget lost impression share is reported in the range of 0 to 0.9. Any value above 0.9 is reported as 0.9001.</td>
</tr>
<tr class="even">
<td>metrics_content_impression_share</td>
<td>The impressions you've received on the Display Network divided by the estimated number of impressions you were eligible to receive. Note: Content impression share is reported in the range of 0.1 to 1. Any value below 0.1 is reported as 0.0999.</td>
</tr>
<tr class="odd">
<td>metrics_content_rank_lost_impression_share</td>
<td>The estimated percentage of impressions on the Display Network that your ads didn't receive due to poor Ad Rank. Note: Content rank lost impression share is reported in the range of 0 to 0.9. Any value above 0.9 is reported as 0.9001.</td>
</tr>
<tr class="even">
<td>metrics_historical_quality_score</td>
<td>The historical quality score.</td>
</tr>
<tr class="odd">
<td>metrics_search_budget_lost_impression_share</td>
<td>The estimated percent of times that your ad was eligible to show on the Search Network but didn't because your budget was too low. Note: Search budget lost impression share is reported in the range of 0 to 0.9. Any value above 0.9 is reported as 0.9001.</td>
</tr>
<tr class="even">
<td>metrics_search_impression_share</td>
<td>The impressions you've received on the Search Network divided by the estimated number of impressions you were eligible to receive. Note: Search impression share is reported in the range of 0.1 to 1. Any value below 0.1 is reported as 0.0999.</td>
</tr>
<tr class="odd">
<td>metrics_search_rank_lost_impression_share</td>
<td>The estimated percentage of impressions on the Search Network that your ads didn't receive due to poor Ad Rank. Note: Search rank lost impression share is reported in the range of 0 to 0.9. Any value above 0.9 is reported as 0.9001.</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply, in yyyy-MM-dd format. For example: 2024-04-17</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: Ad

Search Ads 360 API Resource: [ad\_group\_ad](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/ad_group_ad)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_ad_ad_display_url</td>
<td>The URL that appears in the ad description for some ad formats.</td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_expanded_dynamic_search_ad_description1</td>
<td>The first line of the ad's description.</td>
</tr>
<tr class="odd">
<td>ad_group_ad_ad_expanded_dynamic_search_ad_description2</td>
<td>The second line of the ad's description.</td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_expanded_text_ad_description1</td>
<td>The first line of the ad's description.</td>
</tr>
<tr class="odd">
<td>ad_group_ad_ad_expanded_text_ad_description2</td>
<td>The second line of the ad's description.</td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_expanded_text_ad_headline</td>
<td>The headline of the ad.</td>
</tr>
<tr class="odd">
<td>ad_group_ad_ad_expanded_text_ad_headline2</td>
<td>The second headline of the ad.</td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_expanded_text_ad_headline3</td>
<td>The third headline of the ad.</td>
</tr>
<tr class="odd">
<td>ad_group_ad_ad_final_urls</td>
<td>The list of possible final URLs after all cross-domain redirects for the ad.</td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_id</td>
<td>The ID of the ad.</td>
</tr>
<tr class="odd">
<td>ad_group_ad_ad_name</td>
<td>The name of the ad. This is only used to be able to identify the ad. It does not need to be unique and does not affect the served ad. The name field is only supported for DisplayUploadAd, ImageAd, ShoppingComparisonListingAd and VideoAd.</td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_text_ad_description1</td>
<td>The first line of the ad's description.</td>
</tr>
<tr class="odd">
<td>ad_group_ad_ad_text_ad_description2</td>
<td>The second line of the ad's description.</td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_text_ad_headline</td>
<td>The headline of the ad.</td>
</tr>
<tr class="odd">
<td>ad_group_ad_ad_type</td>
<td>The type of ad.</td>
</tr>
<tr class="even">
<td>ad_group_ad_creation_time</td>
<td>The timestamp when this ad group ad was created. The datetime is in the customer's time zone and in "yyyy-MM-dd HH:mm:ss.ssssss" format.</td>
</tr>
<tr class="odd">
<td>ad_group_ad_engine_id</td>
<td>ID of the ad in the external engine account. This field is for SearchAds 360 account only. For example: Yahoo Japan, Microsoft, Baidu. For non-SearchAds 360 entity, use "ad_group_ad.ad.id" instead.</td>
</tr>
<tr class="even">
<td>ad_group_ad_engine_status</td>
<td>Additional status of the ad in the external engine account. Possible statuses (depending on the type of external account) include active, eligible, pending review.</td>
</tr>
<tr class="odd">
<td>ad_group_ad_labels</td>
<td>The resource names of labels attached to this ad group ad.</td>
</tr>
<tr class="even">
<td>ad_group_ad_last_modified_time</td>
<td>The datetime when this ad group ad was last modified. The datetime is in the customer's time zone and in "yyyy-MM-dd HH:mm:ss.ssssss" format.</td>
</tr>
<tr class="odd">
<td>ad_group_ad_status</td>
<td>The status of the ad.</td>
</tr>
<tr class="even">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: AdConversionActionAndDeviceStats

Search Ads 360 API Resource: [ad\_group\_ad](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/ad_group_ad)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_ad_ad_id</td>
<td>The ID of the ad.</td>
</tr>
<tr class="even">
<td>ad_group_ad_engine_id</td>
<td>ID of the ad in the external engine account. This field is for SearchAds 360 account only. For example: Yahoo Japan, Microsoft, Baidu. For non-SearchAds 360 entity, use "ad_group_ad.ad.id" instead.</td>
</tr>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
<tr class="even">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This includes all conversions regardless of the value of include_in_conversions_metric.</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions_by_conversion_date</td>
<td>The total number of conversions. This includes all conversions regardless of the value of include_in_conversions_metric. When this column is selected with date, the values in date column means the conversion date. For more information about <code dir="ltr" translate="no">       by_conversion_date      </code> columns, see <a href="https://support.google.com/sa360/answer/9250611">About the "All conversions" column</a> .</td>
</tr>
<tr class="even">
<td>metrics_all_conversions_value</td>
<td>The value of all conversions.</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions_value_by_conversion_date</td>
<td>The value of all conversions. When this column is selected with date, the values in date column means the conversion date. For more information about <code dir="ltr" translate="no">       by_conversion_date      </code> columns, see <a href="https://support.google.com/sa360/answer/9250611">About the "All conversions" column</a> .</td>
</tr>
<tr class="even">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on an ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
</tr>
<tr class="odd">
<td>metrics_cross_device_conversions_by_conversion_date</td>
<td>The number of cross-device conversions by conversion date. For more information about <code dir="ltr" translate="no">       by_conversion_date      </code> columns, see <a href="https://support.google.com/sa360/answer/9250611">About the "All conversions" column</a> .</td>
</tr>
<tr class="even">
<td>metrics_cross_device_conversions_value</td>
<td>The sum of the value of cross-device conversions.</td>
</tr>
<tr class="odd">
<td>metrics_cross_device_conversions_value_by_conversion_date</td>
<td>The sum of cross-device conversions value by conversion date. For more information about <code dir="ltr" translate="no">       by_conversion_date      </code> columns, see <a href="https://support.google.com/sa360/answer/9250611">About the "All conversions" column</a> .</td>
</tr>
<tr class="even">
<td>segments.conversion_action_name</td>
<td>Conversion action name.</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply, in yyyy-MM-dd format. For example: 2024-04-17</td>
</tr>
<tr class="even">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: AdDeviceStats

Search Ads 360 API Resource: [ad\_group\_ad](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/ad_group_ad)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_ad_ad_id</td>
<td>The ID of the ad.</td>
</tr>
<tr class="even">
<td>ad_group_ad_engine_id</td>
<td>ID of the ad in the external engine account. This field is for SearchAds 360 account only. For example: Yahoo Japan, Microsoft, Baidu. For non-SearchAds 360 entity, use "ad_group_ad.ad.id" instead.</td>
</tr>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
<tr class="even">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
</tr>
<tr class="odd">
<td>metrics_average_cpm</td>
<td>Average cost-per-thousand impressions (CPM).</td>
</tr>
<tr class="even">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
</tr>
<tr class="odd">
<td>metrics_client_account_conversions</td>
<td>The number of client account conversions. This only includes conversion actions which include_in_client_account_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies will optimize for these conversions.</td>
</tr>
<tr class="even">
<td>metrics_client_account_conversions_value</td>
<td>The value of client account conversions. This only includes conversion actions which include_in_client_account_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies will optimize for these conversions.</td>
</tr>
<tr class="odd">
<td>metrics_client_account_view_through_conversions</td>
<td>The total number of view-through conversions. These happen when a customer sees an image or rich media ad, then later completes a conversion on your site without interacting with (for example, clicking on) another ad.</td>
</tr>
<tr class="even">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
</tr>
<tr class="odd">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
</tr>
<tr class="even">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
</tr>
<tr class="odd">
<td>metrics_visits</td>
<td>Clicks that Search Ads 360 has successfully recorded and forwarded to an advertiser's landing page.</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply, in yyyy-MM-dd format. For example: 2024-04-17</td>
</tr>
<tr class="odd">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: AdGroup

Search Ads 360 API Resource: [ad\_group](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/ad_group)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_bid_modifier_bid_modifier</td>
<td>The modifier for the bid when the criterion matches. The modifier must be in the range: 0.1 - 10.0. The range is 1.0 - 6.0 for PreferredContent. Use 0 to opt out of a Device type.</td>
</tr>
<tr class="even">
<td>ad_group_bid_modifier_device_type</td>
<td>Type of the device.</td>
</tr>
<tr class="odd">
<td>ad_group_cpc_bid_micros</td>
<td>The maximum CPC (cost-per-click) bid.</td>
</tr>
<tr class="even">
<td>ad_group_creation_time</td>
<td>The timestamp when this ad group was created. The timestamp is in the customer's time zone and in "yyyy-MM-dd HH:mm:ss" format.</td>
</tr>
<tr class="odd">
<td>ad_group_end_date</td>
<td>Date when the ad group ends serving ads. By default, the ad group ends on the ad group's end date. If this field is set, then the ad group ends at the end of the specified date in the customer's time zone. This field is only available for Microsoft Advertising and Facebook gateway accounts. Format: YYYY-MM-DD Example: 2019-03-14</td>
</tr>
<tr class="even">
<td>ad_group_engine_id</td>
<td>ID of the ad group in the external engine account. This field is for non-Google Ads account only. For example: Yahoo Japan, Microsoft, Baidu. For Google Ads entity, use "ad_group.id" instead.</td>
</tr>
<tr class="odd">
<td>ad_group_engine_status</td>
<td>The Engine Status for ad group.</td>
</tr>
<tr class="even">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
</tr>
<tr class="odd">
<td>ad_group_labels</td>
<td>The resource names of labels attached to this ad group.</td>
</tr>
<tr class="even">
<td>ad_group_language_code</td>
<td>The language of the ads and keywords in an ad group. This field is only available for Microsoft Advertising accounts.</td>
</tr>
<tr class="odd">
<td>ad_group_last_modified_time</td>
<td>The datetime when this ad group was last modified. The datetime is in the customer's time zone and in "yyyy-MM-dd HH:mm:ss.ssssss" format.</td>
</tr>
<tr class="even">
<td>ad_group_name</td>
<td>The name of the ad group. This field is required and should not be empty when creating new ad groups. It must contain fewer than 255 UTF-8 full-width characters. It must not contain any null (code point 0x0), NL line feed (code point 0xA) or carriage return (code point 0xD) characters.</td>
</tr>
<tr class="odd">
<td>ad_group_start_date</td>
<td>Date when this ad group starts serving ads. By default, the ad group starts now or the ad group's start date, whichever is later. If this field is set, then the ad group starts at the beginning of the specified date in the customer's time zone. This field is only available for Microsoft Advertising and Facebook gateway accounts. Format: YYYY-MM-DD Example: 2019-03-14</td>
</tr>
<tr class="even">
<td>ad_group_status</td>
<td>The status of the ad group.</td>
</tr>
<tr class="odd">
<td>ad_group_targeting_setting_target_restrictions</td>
<td>The per-targeting-dimension setting to restrict the reach of your campaign or ad group.</td>
</tr>
<tr class="even">
<td>bidding_strategy_id</td>
<td>The ID of the bidding strategy.</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: AdGroupAssetStats

Search Ads 360 API Resource: [ad\_group\_asset](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/ad_group_asset)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_asset_ad_group</td>
<td>Required. Immutable. The ad group to which the asset is linked.</td>
</tr>
<tr class="even">
<td>ad_group_asset_asset</td>
<td>Required. Immutable. The asset which is linked to the ad group.</td>
</tr>
<tr class="odd">
<td>ad_group_engine_id</td>
<td>ID of the ad group in the external engine account. This field is for non-Google Ads account only. For example: Yahoo Japan, Microsoft, Baidu. For Google Ads entity, use "ad_group.id" instead.</td>
</tr>
<tr class="even">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
<tr class="odd">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
</tr>
<tr class="even">
<td>metrics_average_cpm</td>
<td>Average cost-per-thousand impressions (CPM).</td>
</tr>
<tr class="odd">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
</tr>
<tr class="even">
<td>metrics_client_account_conversions</td>
<td>The number of client account conversions. This only includes conversion actions which include_in_client_account_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies will optimize for these conversions.</td>
</tr>
<tr class="odd">
<td>metrics_client_account_conversions_value</td>
<td>The value of client account conversions. This only includes conversion actions which include_in_client_account_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies will optimize for these conversions.</td>
</tr>
<tr class="even">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
</tr>
<tr class="odd">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
</tr>
<tr class="even">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply, in yyyy-MM-dd format. For example: 2024-04-17</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: AdGroupAudienceConversionActionAndDeviceStats

Search Ads 360 API Resource: [ad\_group\_audience\_view](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/ad_group_audience_view)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_criterion_age_range_type</td>
<td>Type of the age range.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_bid_modifier</td>
<td>The modifier for the bid when the criterion matches. The modifier must be in the range: 0.1 - 10.0. Most targetable criteria types support modifiers.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_cpc_bid_micros</td>
<td>The CPC (cost-per-click) bid.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_gender_type</td>
<td>Type of the gender.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_location_geo_target_constant</td>
<td>The geo target constant resource name.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_user_list_user_list</td>
<td>The User List resource name.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_webpage_conditions</td>
<td>Conditions, or logical expressions, for webpage targeting. The list of webpage targeting conditions are and-ed together when evaluated for targeting. An empty list of conditions indicates all pages of the campaign's website are targeted. This field is required for CREATE operations and is prohibited on UPDATE operations.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_webpage_coverage_percentage</td>
<td>Website criteria coverage percentage. This is the computed percentage of website coverage based on the website target, negative website target and negative keywords in the ad group and campaign. For instance, when coverage returns as 1, it indicates it has 100% coverage.</td>
</tr>
<tr class="even">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
<tr class="odd">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on an ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
</tr>
<tr class="even">
<td>metrics_cross_device_conversions_value</td>
<td>The sum of the value of cross-device conversions.</td>
</tr>
<tr class="odd">
<td>segments.conversion_action_name</td>
<td>Conversion action name.</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply, in yyyy-MM-dd format. For example: 2024-04-17.</td>
</tr>
<tr class="odd">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: AdGroupAudienceDeviceStats

Search Ads 360 API Resource: [ad\_group\_audience\_view](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/ad_group_audience_view)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_criterion_age_range_type</td>
<td>Type of the age range.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_bid_modifier</td>
<td>The modifier for the bid when the criterion matches. The modifier must be in the range: 0.1 - 10.0. Most targetable criteria types support modifiers.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_cpc_bid_micros</td>
<td>The CPC (cost-per-click) bid.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_gender_type</td>
<td>Type of the gender.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_location_geo_target_constant</td>
<td>The geo target constant resource name.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_user_list_user_list</td>
<td>The User List resource name.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_webpage_conditions</td>
<td>Conditions, or logical expressions, for webpage targeting. The list of webpage targeting conditions are and-ed together when evaluated for targeting. An empty list of conditions indicates all pages of the campaign's website are targeted. This field is required for CREATE operations and is prohibited on UPDATE operations.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_webpage_coverage_percentage</td>
<td>Website criteria coverage percentage. This is the computed percentage of website coverage based on the website target, negative website target and negative keywords in the ad group and campaign. For instance, when coverage returns as 1, it indicates it has 100% coverage.</td>
</tr>
<tr class="even">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
<tr class="odd">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
</tr>
<tr class="even">
<td>metrics_average_cpm</td>
<td>Average cost-per-thousand impressions (CPM).</td>
</tr>
<tr class="odd">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
</tr>
<tr class="even">
<td>metrics_client_account_conversions</td>
<td>The number of client account conversions. This only includes conversion actions which include_in_client_account_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies will optimize for these conversions.</td>
</tr>
<tr class="odd">
<td>metrics_client_account_conversions_value</td>
<td>The value of client account conversions. This only includes conversion actions which include_in_client_account_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies will optimize for these conversions.</td>
</tr>
<tr class="even">
<td>metrics_client_account_view_through_conversions</td>
<td>The total number of view-through conversions. These happen when a customer sees an image or rich media ad, then later completes a conversion on your site without interacting with (for example, clicking on) another ad.</td>
</tr>
<tr class="odd">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
</tr>
<tr class="even">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
</tr>
<tr class="odd">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply, in yyyy-MM-dd format. For example: 2024-04-17</td>
</tr>
<tr class="odd">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: AdGroupConversionActionAndAssetStats

Search Ads 360 API Resource: [ad\_group\_asset](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/ad_group_asset)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_asset_ad_group</td>
<td>Required. Immutable. The ad group to which the asset is linked.</td>
</tr>
<tr class="even">
<td>ad_group_asset_asset</td>
<td>Required. Immutable. The asset which is linked to the ad group.</td>
</tr>
<tr class="odd">
<td>ad_group_engine_id</td>
<td>ID of the ad group in the external engine account. This field is for non-Google Ads account only. For example: Yahoo Japan, Microsoft, Baidu. For Google Ads entity, use "ad_group.id" instead.</td>
</tr>
<tr class="even">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This includes all conversions regardless of the value of include_in_conversions_metric.</td>
</tr>
<tr class="even">
<td>metrics_all_conversions_value</td>
<td>The value of all conversions.</td>
</tr>
<tr class="odd">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on an ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
</tr>
<tr class="even">
<td>metrics_cross_device_conversions_value</td>
<td>The sum of the value of cross-device conversions.</td>
</tr>
<tr class="odd">
<td>segments.conversion_action_name</td>
<td>Conversion action name.</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply, in yyyy-MM-dd format. For example: 2018-04-17</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: AdGroupConversionActionAndDeviceStats

Search Ads 360 API Resource: [ad\_group](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/ad_group)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_engine_id</td>
<td>Output only. ID of the ad group in the external engine account. This field is for non-Google Ads account only. For example: Yahoo Japan, Microsoft, Baidu. For Google Ads entity, use "ad_group.id" instead.</td>
</tr>
<tr class="even">
<td>ad_group_id</td>
<td>Output only. The ID of the ad group.</td>
</tr>
<tr class="odd">
<td>bidding_strategy_id</td>
<td>Output only. The ID of the bidding strategy.</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>Output only. The ID of the campaign.</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>Output only. The ID of the customer.</td>
</tr>
<tr class="even">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This includes all conversions regardless of the value of include_in_conversions_metric.</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions_value</td>
<td>The value of all conversions.</td>
</tr>
<tr class="even">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on an ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
</tr>
<tr class="odd">
<td>metrics_cross_device_conversions_value</td>
<td>The sum of the value of cross-device conversions.</td>
</tr>
<tr class="even">
<td>segments.conversion_action_name</td>
<td>Conversion action name.</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply, in yyyy-MM-dd format. For example: 2024-04-17</td>
</tr>
<tr class="even">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: AdGroupCriterion

Search Ads 360 API Resource: [ad\_group\_criterion](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/ad_group_criterion)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_criterion_age_range_type</td>
<td>Type of the age range.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_bid_modifier</td>
<td>The modifier for the bid when the criterion matches. The modifier must be in the range: 0.1 - 10.0. Most targetable criteria types support modifiers.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_cpc_bid_micros</td>
<td>The CPC (cost-per-click) bid.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_creation_time</td>
<td>The timestamp when this ad group criterion was created. The timestamp is in the customer's time zone and in "yyyy-MM-dd HH:mm:ss" format.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_gender_type</td>
<td>Type of the gender.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_last_modified_time</td>
<td>The datetime when this ad group criterion was last modified. The datetime is in the customer's time zone and in "yyyy-MM-dd HH:mm:ss.ssssss" format.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_location_geo_target_constant</td>
<td>The geo target constant resource name.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_status</td>
<td>The status of the criterion. This is the status of the ad group criterion entity, set by the client. Note: UI reports may incorporate additional information that affects whether a criterion is eligible to run. In some cases a criterion that's REMOVED in the API can still show as enabled in the UI. For example, campaigns by default show to users of all age ranges unless excluded. The UI will show each age range as "enabled", since they're eligible to see the ads; but AdGroupCriterion.status will show "removed", since no positive criterion was added.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_type</td>
<td>The type of the criterion.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_user_list_user_list</td>
<td>The User List resource name.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_webpage_conditions</td>
<td>Conditions, or logical expressions, for webpage targeting. The list of webpage targeting conditions are and-ed together when evaluated for targeting. An empty list of conditions indicates all pages of the campaign's website are targeted. This field is required for CREATE operations and is prohibited on UPDATE operations.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_webpage_coverage_percentage</td>
<td>Website criteria coverage percentage. This is the computed percentage of website coverage based on the website target, negative website target and negative keywords in the ad group and campaign. For instance, when coverage returns as 1, it indicates it has 100% coverage.</td>
</tr>
<tr class="even">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
</tr>
<tr class="odd">
<td>ad_group_name</td>
<td>The name of the ad group. This field is required and should not be empty when creating new ad groups. It must contain fewer than 255 UTF-8 full-width characters. It must not contain any null (code point 0x0), NL line feed (code point 0xA) or carriage return (code point 0xD) characters.</td>
</tr>
<tr class="even">
<td>ad_group_status</td>
<td>The status of the ad group.</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
</tr>
<tr class="even">
<td>campaign_name</td>
<td>The name of the campaign. This field is required and should not be empty when creating new campaigns. It must not contain any null (code point 0x0), NL line feed (code point 0xA) or carriage return (code point 0xD) characters.</td>
</tr>
<tr class="odd">
<td>campaign_status</td>
<td>The status of the campaign.</td>
</tr>
<tr class="even">
<td>customer_account_type</td>
<td>Engine account type. For example: Google Ads, Microsoft Advertising, Yahoo Japan, Baidu, Facebook, Engine Track.</td>
</tr>
<tr class="odd">
<td>customer_descriptive_name</td>
<td>Optional, non-unique descriptive name of the customer.</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: AdGroupDeviceStats

Search Ads 360 API Resource: [ad\_group](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/ad_group)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_engine_id</td>
<td>ID of the ad group in the external engine account. This field is for non-Google Ads account only. For example: Yahoo Japan, Microsoft, Baidu. For Google Ads entity, use "ad_group.id" instead.</td>
</tr>
<tr class="even">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
</tr>
<tr class="odd">
<td>bidding_strategy_id</td>
<td>The ID of the bidding strategy.</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
<tr class="even">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
</tr>
<tr class="odd">
<td>metrics_average_cpm</td>
<td>Average cost-per-thousand impressions (CPM).</td>
</tr>
<tr class="even">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
</tr>
<tr class="odd">
<td>metrics_client_account_conversions</td>
<td>The number of client account conversions. This only includes conversion actions which include_in_client_account_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies will optimize for these conversions.</td>
</tr>
<tr class="even">
<td>metrics_client_account_conversions_value</td>
<td>The value of client account conversions. This only includes conversion actions which include_in_client_account_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies will optimize for these conversions.</td>
</tr>
<tr class="odd">
<td>metrics_client_account_view_through_conversions</td>
<td>The total number of view-through conversions. These happen when a customer sees an image or rich media ad, then later completes a conversion on your site without interacting with (for example, clicking on) another ad.</td>
</tr>
<tr class="even">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
</tr>
<tr class="odd">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
</tr>
<tr class="even">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
</tr>
<tr class="odd">
<td>metrics_visits</td>
<td>Clicks that Search Ads 360 has successfully recorded and forwarded to an advertiser's landing page.</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply, in yyyy-MM-dd format. For example: 2024-04-17</td>
</tr>
<tr class="odd">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: AdGroupLabel

Search Ads 360 API Resource: [ad\_group\_label](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/ad_group_label)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_label_ad_group</td>
<td>The ad group to which the label is attached.</td>
</tr>
<tr class="even">
<td>ad_group_label_label</td>
<td>The label assigned to the ad group.</td>
</tr>
<tr class="odd">
<td>ad_group_label_owner_customer_id</td>
<td>The ID of the Customer which owns the label.</td>
</tr>
<tr class="even">
<td>ad_group_label_resource_name</td>
<td>The resource name of the ad group label. Ad group label resource names have the form: customers/{customer_id}/adGroupLabels/{ad_group_id}~{label_id}</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: AdGroupStats

Search Ads 360 API Resource: [ad\_group](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/ad_group)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_engine_id</td>
<td>ID of the ad group in the external engine account. This field is for non-Google Ads account only. For example: Yahoo Japan, Microsoft, Baidu. For Google Ads entity, use "ad_group.id" instead.</td>
</tr>
<tr class="even">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
</tr>
<tr class="odd">
<td>bidding_strategy_id</td>
<td>The ID of the bidding strategy.</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
<tr class="even">
<td>metrics_content_impression_share</td>
<td>The impressions you've received on the Display Network divided by the estimated number of impressions you were eligible to receive. Note: Content impression share is reported in the range of 0.1 to 1. Any value below 0.1 is reported as 0.0999.</td>
</tr>
<tr class="odd">
<td>metrics_content_rank_lost_impression_share</td>
<td>The estimated percentage of impressions on the Display Network that your ads didn't receive due to poor Ad Rank. Note: Content rank lost impression share is reported in the range of 0 to 0.9. Any value above 0.9 is reported as 0.9001.</td>
</tr>
<tr class="even">
<td>metrics_historical_quality_score</td>
<td>The historical quality score.</td>
</tr>
<tr class="odd">
<td>metrics_search_impression_share</td>
<td>The impressions you've received on the Search Network divided by the estimated number of impressions you were eligible to receive. Note: Search impression share is reported in the range of 0.1 to 1. Any value below 0.1 is reported as 0.0999.</td>
</tr>
<tr class="even">
<td>metrics_search_rank_lost_impression_share</td>
<td>The estimated percentage of impressions on the Search Network that your ads didn't receive due to poor Ad Rank. Note: Search rank lost impression share is reported in the range of 0 to 0.9. Any value above 0.9 is reported as 0.9001.</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply, in yyyy-MM-dd format. For example: 2024-04-17.</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: AgeRangeConversionActionAndDeviceStats

Search Ads 360 API Resource: [age\_range\_view](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/age_range_view)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_criterion_age_range_type</td>
<td>Type of the age range.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_bid_modifier</td>
<td>The modifier for the bid when the criterion matches. The modifier must be in the range: 0.1 - 10.0. Most targetable criteria types support modifiers.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_cpc_bid_micros</td>
<td>The CPC (cost-per-click) bid.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_gender_type</td>
<td>Type of the gender.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_location_geo_target_constant</td>
<td>The geo target constant resource name.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_user_list_user_list</td>
<td>The User List resource name.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_webpage_conditions</td>
<td>Conditions, or logical expressions, for webpage targeting. The list of webpage targeting conditions are and-ed together when evaluated for targeting. An empty list of conditions indicates all pages of the campaign's website are targeted. This field is required for CREATE operations and is prohibited on UPDATE operations.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_webpage_coverage_percentage</td>
<td>Website criteria coverage percentage. This is the computed percentage of website coverage based on the website target, negative website target and negative keywords in the ad group and campaign. For instance, when coverage returns as 1, it indicates it has 100% coverage.</td>
</tr>
<tr class="even">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
<tr class="odd">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on an ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
</tr>
<tr class="even">
<td>metrics_cross_device_conversions_value</td>
<td>The sum of the value of cross-device conversions.</td>
</tr>
<tr class="odd">
<td>segments.conversion_action_name</td>
<td>Conversion action name.</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply, in yyyy-MM-dd format. For example: 2024-04-17</td>
</tr>
<tr class="odd">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: AgeRangeDeviceStats

Search Ads 360 API Resource: [age\_range\_view](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/age_range_view)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_criterion_age_range_type</td>
<td>Type of the age range.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_bid_modifier</td>
<td>The modifier for the bid when the criterion matches. The modifier must be in the range: 0.1 - 10.0. Most targetable criteria types support modifiers.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_cpc_bid_micros</td>
<td>The CPC (cost-per-click) bid.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_gender_type</td>
<td>Type of the gender.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_location_geo_target_constant</td>
<td>The geo target constant resource name.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_user_list_user_list</td>
<td>The User List resource name.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_webpage_conditions</td>
<td>Conditions, or logical expressions, for webpage targeting. The list of webpage targeting conditions are and-ed together when evaluated for targeting. An empty list of conditions indicates all pages of the campaign's website are targeted. This field is required for CREATE operations and is prohibited on UPDATE operations.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_webpage_coverage_percentage</td>
<td>Website criteria coverage percentage. This is the computed percentage of website coverage based on the website target, negative website target and negative keywords in the ad group and campaign. For instance, when coverage returns as 1, it indicates it has 100% coverage.</td>
</tr>
<tr class="even">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
<tr class="odd">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
</tr>
<tr class="even">
<td>metrics_average_cpm</td>
<td>Average cost-per-thousand impressions (CPM).</td>
</tr>
<tr class="odd">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
</tr>
<tr class="even">
<td>metrics_client_account_conversions</td>
<td>The number of client account conversions. This only includes conversion actions which include_in_client_account_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies will optimize for these conversions.</td>
</tr>
<tr class="odd">
<td>metrics_client_account_conversions_value</td>
<td>The value of client account conversions. This only includes conversion actions which include_in_client_account_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies will optimize for these conversions.</td>
</tr>
<tr class="even">
<td>metrics_client_account_view_through_conversions</td>
<td>The total number of view-through conversions. These happen when a customer sees an image or rich media ad, then later completes a conversion on your site without interacting with (for example, clicking on) another ad.</td>
</tr>
<tr class="odd">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
</tr>
<tr class="even">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
</tr>
<tr class="odd">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply, in yyyy-MM-dd format. For example: 2024-04-17</td>
</tr>
<tr class="odd">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: Asset

Search Ads 360 API Resource: [asset](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/asset)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>asset_creation_time</td>
<td>The timestamp when this asset was created. The timestamp is in the customer's time zone and in "yyyy-MM-dd HH:mm:ss" format.</td>
</tr>
<tr class="even">
<td>asset_engine_status</td>
<td>The Engine Status of the asset.</td>
</tr>
<tr class="odd">
<td>asset_final_urls</td>
<td>A list of possible final URLs after all cross domain redirects.</td>
</tr>
<tr class="even">
<td>asset_id</td>
<td>The ID of the asset.</td>
</tr>
<tr class="odd">
<td>asset_last_modified_time</td>
<td>The datetime when this asset was last modified. The datetime is in the customer's time zone and in "yyyy-MM-dd HH:mm:ss.ssssss" format.</td>
</tr>
<tr class="even">
<td>asset_sitelink_asset.description1</td>
<td>First line of the description for the sitelink. If set, the length should be between 1 and 35, inclusive, and description2 must also be set.</td>
</tr>
<tr class="odd">
<td>asset_sitelink_asset.description2</td>
<td>Second line of the description for the sitelink. If set, the length should be between 1 and 35, inclusive, and description1 must also be set.</td>
</tr>
<tr class="even">
<td>asset_sitelink_asset_link_text</td>
<td>URL display text for the sitelink. The length of this string should be between 1 and 25, inclusive.</td>
</tr>
<tr class="odd">
<td>asset_status</td>
<td>The status of the asset.</td>
</tr>
<tr class="even">
<td>asset_tracking_url_template</td>
<td>URL template for constructing a tracking URL.</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: AssetSetStats

Search Ads 360 API Resource: [asset\_set\_asset](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/asset_set_asset)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>asset_set_asset_asset</td>
<td>Immutable. The asset which this asset set asset is linking to.</td>
</tr>
<tr class="even">
<td>asset_set_asset_asset_set</td>
<td>Immutable. The asset set which this asset set asset is linking to.</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
<tr class="even">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
</tr>
<tr class="odd">
<td>metrics_average_cpm</td>
<td>Average cost-per-thousand impressions (CPM).</td>
</tr>
<tr class="even">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
</tr>
<tr class="odd">
<td>metrics_client_account_conversions</td>
<td>The number of client account conversions. This only includes conversion actions which include_in_client_account_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies will optimize for these conversions.</td>
</tr>
<tr class="even">
<td>metrics_client_account_conversions_value</td>
<td>The value of client account conversions. This only includes conversion actions which include_in_client_account_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies will optimize for these conversions.</td>
</tr>
<tr class="odd">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
</tr>
<tr class="even">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
</tr>
<tr class="odd">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply, in yyyy-MM-dd format. For example: 2024-04-17</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: BidStrategy

Search Ads 360 API Resource: [bidding\_strategy](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/bidding_strategy)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>bidding_strategy_id</td>
<td>The ID of the bidding strategy.</td>
</tr>
<tr class="even">
<td>bidding_strategy_name</td>
<td>The name of the bidding strategy. All bidding strategies within an account must be named distinctly. The length of this string should be between 1 and 255, inclusive, in UTF-8 bytes, (trimmed).</td>
</tr>
<tr class="odd">
<td>bidding_strategy_status</td>
<td>The status of the bidding strategy.</td>
</tr>
<tr class="even">
<td>bidding_strategy_target_cpa_cpc_bid_ceiling_micros</td>
<td>Maximum bid limit that can be set by the bid strategy. The limit applies to all keywords managed by the strategy. This should only be set for portfolio bid strategies.</td>
</tr>
<tr class="odd">
<td>bidding_strategy_target_cpa_cpc_bid_floor_micros</td>
<td>Minimum bid limit that can be set by the bid strategy. The limit applies to all keywords managed by the strategy. This should only be set for portfolio bid strategies.</td>
</tr>
<tr class="even">
<td>bidding_strategy_target_cpa_target_cpa_micros</td>
<td>Average CPA target. This target should be greater than or equal to minimum billable unit based on the currency for the account.</td>
</tr>
<tr class="odd">
<td>bidding_strategy_target_impression_share_cpc_bid_ceiling_micros</td>
<td>The highest CPC bid the automated bidding system is permitted to specify. This is a required field entered by the advertiser that sets the ceiling and specified in local micros.</td>
</tr>
<tr class="even">
<td>bidding_strategy_target_outrank_share_cpc_bid_ceiling_micros</td>
<td>Maximum bid limit that can be set by the bid strategy. The limit applies to all keywords managed by the strategy.</td>
</tr>
<tr class="odd">
<td>bidding_strategy_target_roas_cpc_bid_ceiling_micros</td>
<td>Maximum bid limit that can be set by the bid strategy. The limit applies to all keywords managed by the strategy. This should only be set for portfolio bid strategies.</td>
</tr>
<tr class="even">
<td>bidding_strategy_target_roas_cpc_bid_floor_micros</td>
<td>Minimum bid limit that can be set by the bid strategy. The limit applies to all keywords managed by the strategy. This should only be set for portfolio bid strategies.</td>
</tr>
<tr class="odd">
<td>bidding_strategy_target_roas_target_roas</td>
<td>The chosen revenue (based on conversion data) per unit of spend. Value must be between 0.01 and 1000.0, inclusive.</td>
</tr>
<tr class="even">
<td>bidding_strategy_target_spend_cpc_bid_ceiling_micros</td>
<td>Maximum bid limit that can be set by the bid strategy. The limit applies to all keywords managed by the strategy.</td>
</tr>
<tr class="odd">
<td>bidding_strategy_target_spend_target_spend_micros</td>
<td>The spend target under which to maximize clicks. A TargetSpend bidder will attempt to spend the smaller of this value or the natural throttling spend amount. If not specified, the budget is used as the spend target. This field is deprecated and should no longer be used.</td>
</tr>
<tr class="even">
<td>segments_conversion_action</td>
<td>Resource name of the conversion action.</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: BidStrategyStats

Search Ads 360 API Resource: [bidding\_strategy](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/bidding_strategy)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>bidding_strategy_id</td>
<td>The ID of the bidding strategy.</td>
</tr>
<tr class="even">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This includes all conversions regardless of the value of include_in_conversions_metric.</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions_by_conversion_date</td>
<td>The total number of conversions. This includes all conversions regardless of the value of include_in_conversions_metric. When this column is selected with date, the values in date column means the conversion date. For more information about <code dir="ltr" translate="no">       by_conversion_date      </code> columns, see <a href="https://support.google.com/sa360/answer/9250611">About the "All conversions" column</a> .</td>
</tr>
<tr class="even">
<td>metrics_all_conversions_value</td>
<td>The value of all conversions.</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions_value_by_conversion_date</td>
<td>The value of all conversions. When this column is selected with date, the values in date column means the conversion date. For more information about <code dir="ltr" translate="no">       by_conversion_date      </code> columns, see <a href="https://support.google.com/sa360/answer/9250611">About the "All conversions" column</a> .</td>
</tr>
<tr class="even">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
</tr>
<tr class="odd">
<td>metrics_average_cpm</td>
<td>Average cost-per-thousand impressions (CPM).</td>
</tr>
<tr class="even">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
</tr>
<tr class="odd">
<td>metrics_client_account_conversions</td>
<td>The number of client account conversions. This only includes conversion actions which include_in_client_account_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies will optimize for these conversions.</td>
</tr>
<tr class="even">
<td>metrics_client_account_conversions_value</td>
<td>The value of client account conversions. This only includes conversion actions which include_in_client_account_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies will optimize for these conversions.</td>
</tr>
<tr class="odd">
<td>metrics_client_account_view_through_conversions</td>
<td>The total number of view-through conversions. These happen when a customer sees an image or rich media ad, then later completes a conversion on your site without interacting with (for example, clicking on) another ad.</td>
</tr>
<tr class="even">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
</tr>
<tr class="odd">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on an ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
</tr>
<tr class="even">
<td>metrics_cross_device_conversions_by_conversion_date</td>
<td>The number of cross-device conversions by conversion date. For more information about <code dir="ltr" translate="no">       by_conversion_date      </code> columns, see <a href="https://support.google.com/sa360/answer/9250611">About the "All conversions" column</a> .</td>
</tr>
<tr class="odd">
<td>metrics_cross_device_conversions_value</td>
<td>The sum of the value of cross-device conversions.</td>
</tr>
<tr class="even">
<td>metrics_cross_device_conversions_value_by_conversion_date</td>
<td>The sum of cross-device conversions value by conversion date. For more information about <code dir="ltr" translate="no">       by_conversion_date      </code> columns, see <a href="https://support.google.com/sa360/answer/9250611">About the "All conversions" column</a> .</td>
</tr>
<tr class="odd">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
</tr>
<tr class="even">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply, in yyyy-MM-dd format. For example: 2024-04-17</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: Campaign

Search Ads 360 API Resource: [campaign](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/campaign)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>accessible_bidding_strategy_id</td>
<td>The ID of the bidding strategy.</td>
</tr>
<tr class="even">
<td>accessible_bidding_strategy_name</td>
<td>The name of the bidding strategy.</td>
</tr>
<tr class="odd">
<td>bidding_strategy_id</td>
<td>The ID of the bidding strategy.</td>
</tr>
<tr class="even">
<td>bidding_strategy_name</td>
<td>The name of the bidding strategy. All bidding strategies within an account must be named distinctly. The length of this string should be between 1 and 255, inclusive, in UTF-8 bytes, (trimmed).</td>
</tr>
<tr class="odd">
<td>campaign_advertising_channel_sub_type</td>
<td>Optional refinement to advertising_channel_type. Must be a valid sub-type of the parent channel type. Can be set only when creating campaigns. After campaign is created, the field can not be changed.</td>
</tr>
<tr class="even">
<td>campaign_advertising_channel_type</td>
<td>The primary serving target for ads within the campaign. The targeting options can be refined in network_settings. This field is required and should not be empty when creating new campaigns. Can be set only when creating campaigns. After the campaign is created, the field can not be changed.</td>
</tr>
<tr class="odd">
<td>campaign_bidding_strategy_type</td>
<td>The type of bidding strategy. A bidding strategy can be created by setting either the bidding scheme to create a standard bidding strategy or the bidding_strategy field to create a portfolio bidding strategy. This field is read-only.</td>
</tr>
<tr class="even">
<td>campaign_budget_amount_micros</td>
<td>The amount of the budget, in the local currency for the account. Amount is specified in micros, where one million is equivalent to one currency unit. Monthly spend is capped at 30.4 times this amount.</td>
</tr>
<tr class="odd">
<td>campaign_budget_delivery_method</td>
<td>The delivery method that determines the rate at which the campaign budget is spent. Defaults to STANDARD if unspecified in a create operation.</td>
</tr>
<tr class="even">
<td>campaign_budget_period</td>
<td>Period over which to spend the budget. Defaults to DAILY if not specified.</td>
</tr>
<tr class="odd">
<td>campaign_creation_time</td>
<td>The timestamp when this campaign was created. The timestamp is in the customer's time zone and in "yyyy-MM-dd HH:mm:ss" format.</td>
</tr>
<tr class="even">
<td>campaign_end_date</td>
<td>The last day of the campaign in serving customer's timezone in YYYY-MM-DD format. On create, defaults to 2037-12-30, which means the campaign will run indefinitely. To set an existing campaign to run indefinitely, set this field to 2037-12-30.</td>
</tr>
<tr class="odd">
<td>campaign_engine_id</td>
<td>ID of the campaign in the external engine account. This field is for non-Google Ads account only. For example: Yahoo Japan, Microsoft, Baidu. For Google Ads entity, use "campaign.id" instead.</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
</tr>
<tr class="odd">
<td>campaign_labels</td>
<td>The resource names of labels attached to this campaign.</td>
</tr>
<tr class="even">
<td>campaign_last_modified_time</td>
<td>The datetime when this campaign was last modified. The datetime is in the customer's time zone and in "yyyy-MM-dd HH:mm:ss.ssssss" format.</td>
</tr>
<tr class="odd">
<td>campaign_name</td>
<td>The name of the campaign. This field is required and should not be empty when creating new campaigns. It must not contain any null (code point 0x0), NL line feed (code point 0xA) or carriage return (code point 0xD) characters.</td>
</tr>
<tr class="even">
<td>campaign_network_settings_target_content_network</td>
<td>Whether ads will be served on specified placements in the Google Display Network. Placements are specified using the Placement criterion.</td>
</tr>
<tr class="odd">
<td>campaign_network_settings_target_google_search</td>
<td>Whether ads will be served with google.com search results.</td>
</tr>
<tr class="even">
<td>campaign_network_settings_target_partner_search_network</td>
<td>Whether ads will be served on the Google Partner Network. This is available only to some select Google partner accounts.</td>
</tr>
<tr class="odd">
<td>campaign_network_settings_target_search_network</td>
<td>Whether ads will be served on partner sites in the Google Search Network (requires target_google_search to also be true).</td>
</tr>
<tr class="even">
<td>campaign_start_date</td>
<td>The date when campaign started in serving customer's timezone in YYYY-MM-DD format.</td>
</tr>
<tr class="odd">
<td>campaign_status</td>
<td>The status of the campaign.</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: CampaignAssetStats

Search Ads 360 API Resource: [campaign\_asset](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/campaign_asset)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>campaign_asset_asset</td>
<td>Immutable. The asset which is linked to the campaign.</td>
</tr>
<tr class="even">
<td>campaign_asset_campaign</td>
<td>Immutable. The campaign to which the asset is linked.</td>
</tr>
<tr class="odd">
<td>campaign_engine_id</td>
<td>ID of the campaign in the external engine account. This field is for non-Google Ads account only. For example: Yahoo Japan, Microsoft, Baidu. For Google Ads entity, use "campaign.id" instead.</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
<tr class="even">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
</tr>
<tr class="odd">
<td>metrics_average_cpm</td>
<td>Average cost-per-thousand impressions (CPM).</td>
</tr>
<tr class="even">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
</tr>
<tr class="odd">
<td>metrics_client_account_conversions</td>
<td>The number of client account conversions. This only includes conversion actions which include_in_client_account_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies will optimize for these conversions.</td>
</tr>
<tr class="even">
<td>metrics_client_account_conversions_value</td>
<td>The value of client account conversions. This only includes conversion actions which include_in_client_account_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies will optimize for these conversions.</td>
</tr>
<tr class="odd">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
</tr>
<tr class="even">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
</tr>
<tr class="odd">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply, in yyyy-MM-dd format. For example: 2024-04-17</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: CampaignAudienceConversionActionAndDeviceStats

Search Ads 360 API Resource: [campaign\_audience\_view](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/campaign_audience_view)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>campaign_criterion_criterion_id</td>
<td>The ID of the criterion.</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
<tr class="even">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This includes all conversions regardless of the value of include_in_conversions_metric.</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions_value</td>
<td>The value of all conversions.</td>
</tr>
<tr class="even">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on an ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
</tr>
<tr class="odd">
<td>metrics_cross_device_conversions_value</td>
<td>The sum of the value of cross-device conversions.</td>
</tr>
<tr class="even">
<td>segments.conversion_action_name</td>
<td>Conversion action name.</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply, in yyyy-MM-dd format. For example: 2024-04-17</td>
</tr>
<tr class="even">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: CampaignAudienceDeviceStats

Search Ads 360 API Resource: [campaign\_audience\_view](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/campaign_audience_view)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>campaign_criterion_criterion_id</td>
<td>The ID of the criterion.</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
<tr class="even">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
</tr>
<tr class="odd">
<td>metrics_average_cpm</td>
<td>Average cost-per-thousand impressions (CPM).</td>
</tr>
<tr class="even">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
</tr>
<tr class="odd">
<td>metrics_client_account_conversions</td>
<td>The number of client account conversions. This only includes conversion actions which include_in_client_account_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies will optimize for these conversions.</td>
</tr>
<tr class="even">
<td>metrics_client_account_conversions_value</td>
<td>The value of client account conversions. This only includes conversion actions which include_in_client_account_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies will optimize for these conversions.</td>
</tr>
<tr class="odd">
<td>metrics_client_account_view_through_conversions</td>
<td>The total number of view-through conversions. These happen when a customer sees an image or rich media ad, then later completes a conversion on your site without interacting with (for example, clicking on) another ad.</td>
</tr>
<tr class="even">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
</tr>
<tr class="odd">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
</tr>
<tr class="even">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply, in yyyy-MM-dd format. For example: 2024-04-17</td>
</tr>
<tr class="even">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: CampaignConversionActionAndAssetStats

Search Ads 360 API Resource: [campaign\_asset](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/campaign_asset)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
</tr>
<tr class="even">
<td>campaign_asset_campaign</td>
<td>Immutable. The campaign to which the asset is linked.</td>
</tr>
<tr class="odd">
<td>campaign_engine_id</td>
<td>ID of the campaign in the external engine account. This field is for non-Google Ads account only. For example: Yahoo Japan, Microsoft, Baidu. For Google Ads entity, use "campaign.id" instead.</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
</tr>
<tr class="odd">
<td>campain_asset_asset</td>
<td>Immutable. The asset which is linked to the campaign.</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This includes all conversions regardless of the value of include_in_conversions_metric.</td>
</tr>
<tr class="even">
<td>metrics_all_conversions_value</td>
<td>The value of all conversions.</td>
</tr>
<tr class="odd">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on an ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
</tr>
<tr class="even">
<td>metrics_cross_device_conversions_value</td>
<td>The sum of the value of cross-device conversions.</td>
</tr>
<tr class="odd">
<td>segments.conversion_action_name</td>
<td>Conversion action name.</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply, in yyyy-MM-dd format. For example: 2024-04-17</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: CampaignConversionActionAndDeviceStats

Search Ads 360 API Resource: [campaign](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/campaign)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>bidding_strategy_id</td>
<td>The ID of the bidding strategy.</td>
</tr>
<tr class="even">
<td>campaign_engine_id</td>
<td>ID of the campaign in the external engine account. This field is for non-Google Ads account only. For example: Yahoo Japan, Microsoft, Baidu. For Google Ads entity, use "campaign.id" instead.</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This includes all conversions regardless of the value of include_in_conversions_metric.</td>
</tr>
<tr class="even">
<td>metrics_all_conversions_by_conversion_date</td>
<td>The total number of conversions. This includes all conversions regardless of the value of include_in_conversions_metric. When this column is selected with date, the values in date column means the conversion date. For more information about <code dir="ltr" translate="no">       by_conversion_date      </code> columns, see <a href="https://support.google.com/sa360/answer/9250611">About the "All conversions" column</a> .</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions_value</td>
<td>The value of all conversions.</td>
</tr>
<tr class="even">
<td>metrics_all_conversions_value_by_conversion_date</td>
<td>The value of all conversions. When this column is selected with date, the values in date column means the conversion date. For more information about <code dir="ltr" translate="no">       by_conversion_date      </code> columns, see <a href="https://support.google.com/sa360/answer/9250611">About the "All conversions" column</a> .</td>
</tr>
<tr class="odd">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on an ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
</tr>
<tr class="even">
<td>metrics_cross_device_conversions_by_conversion_date</td>
<td>The number of cross-device conversions by conversion date. For more information about <code dir="ltr" translate="no">       by_conversion_date      </code> columns, see <a href="https://support.google.com/sa360/answer/9250611">About the "All conversions" column</a> .</td>
</tr>
<tr class="odd">
<td>metrics_cross_device_conversions_value</td>
<td>The sum of the value of cross-device conversions.</td>
</tr>
<tr class="even">
<td>metrics_cross_device_conversions_value_by_conversion_date</td>
<td>The sum of cross-device conversions value by conversion date. For more information about <code dir="ltr" translate="no">       by_conversion_date      </code> columns, see <a href="https://support.google.com/sa360/answer/9250611">About the "All conversions" column</a> .</td>
</tr>
<tr class="odd">
<td>segments.conversion_action_name</td>
<td>Conversion action name.</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply, in yyyy-MM-dd format. For example: 2024-04-17</td>
</tr>
<tr class="odd">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: CampaignCriterion

Search Ads 360 API Resource: [campaign\_criterion](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/campaign_criterion)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>campaign_criterion_bid_modifier</td>
<td>The modifier for the bid when the criterion matches. The modifier must be in the range: 0.1 - 10.0. Most targetable criteria types support modifiers.</td>
</tr>
<tr class="even">
<td>campaign_criterion_criterion_id</td>
<td>The ID of the criterion.</td>
</tr>
<tr class="odd">
<td>campaign_criterion_last_modified_time</td>
<td>The datetime when this campaign criterion was last modified. The datetime is in the customer's time zone and in "yyyy-MM-dd HH:mm:ss.ssssss" format.</td>
</tr>
<tr class="even">
<td>campaign_criterion_location_geo_target_constant</td>
<td>The geo target constant resource name.</td>
</tr>
<tr class="odd">
<td>campaign_criterion_status</td>
<td>The status of the criterion.</td>
</tr>
<tr class="even">
<td>campaign_criterion_type</td>
<td>The type of the criterion.</td>
</tr>
<tr class="odd">
<td>campaign_criterion_user_list_user_list</td>
<td>The User List resource name.</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: CampaignDeviceStats

Search Ads 360 API Resource: [campaign](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/campaign)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>bidding_strategy_id</td>
<td>The ID of the bidding strategy.</td>
</tr>
<tr class="even">
<td>campaign_engine_id</td>
<td>ID of the campaign in the external engine account. This field is for non-Google Ads account only. For example: Yahoo Japan, Microsoft, Baidu. For Google Ads entity, use "campaign.id" instead.</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
<tr class="odd">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
</tr>
<tr class="even">
<td>metrics_average_cpm</td>
<td>Average cost-per-thousand impressions (CPM).</td>
</tr>
<tr class="odd">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
</tr>
<tr class="even">
<td>metrics_client_account_conversions</td>
<td>The number of client account conversions. This only includes conversion actions which include_in_client_account_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies will optimize for these conversions.</td>
</tr>
<tr class="odd">
<td>metrics_client_account_conversions_value</td>
<td>The value of client account conversions. This only includes conversion actions which include_in_client_account_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies will optimize for these conversions.</td>
</tr>
<tr class="even">
<td>metrics_client_account_view_through_conversions</td>
<td>The total number of view-through conversions. These happen when a customer sees an image or rich media ad, then later completes a conversion on your site without interacting with (for example, clicking on) another ad.</td>
</tr>
<tr class="odd">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
</tr>
<tr class="even">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
</tr>
<tr class="odd">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
</tr>
<tr class="even">
<td>metrics_visits</td>
<td>Clicks that Search Ads 360 has successfully recorded and forwarded to an advertiser's landing page.</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply, in yyyy-MM-dd format. For example: 2024-04-17</td>
</tr>
<tr class="even">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: CampaignLabel

Search Ads 360 API Resource: [campaign\_label](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/campaign_label)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
</tr>
<tr class="even">
<td>campaign_label_campaign</td>
<td>The campaign to which the label is attached.</td>
</tr>
<tr class="odd">
<td>campaign_label_label</td>
<td>The label assigned to the campaign.</td>
</tr>
<tr class="even">
<td>campaign_label_owner_customer_id</td>
<td>The ID of the Customer which owns the label.</td>
</tr>
<tr class="odd">
<td>campaign_label_resource_name</td>
<td>Name of the resource. Campaign label resource names have the form: customers/{customer_id}/campaignLabels/{campaign_id}~{label_id}</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: CampaignStats

Search Ads 360 API Resource: [campaign](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/campaign)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>bidding_strategy_id</td>
<td>The ID of the bidding strategy.</td>
</tr>
<tr class="even">
<td>campaign_engine_id</td>
<td>ID of the campaign in the external engine account. This field is for non-Google Ads account only. For example: Yahoo Japan, Microsoft, Baidu. For Google Ads entity, use "campaign.id" instead.</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This includes all conversions regardless of the value of include_in_conversions_metric.</td>
</tr>
<tr class="even">
<td>metrics_all_conversions_value</td>
<td>The value of all conversions.</td>
</tr>
<tr class="odd">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
</tr>
<tr class="even">
<td>metrics_average_cpm</td>
<td>Average cost-per-thousand impressions (CPM).</td>
</tr>
<tr class="odd">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
</tr>
<tr class="even">
<td>metrics_client_account_conversions</td>
<td>The number of client account conversions. This only includes conversion actions which include_in_client_account_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies will optimize for these conversions.</td>
</tr>
<tr class="odd">
<td>metrics_client_account_conversions_value</td>
<td>The value of client account conversions. This only includes conversion actions which include_in_client_account_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies will optimize for these conversions.</td>
</tr>
<tr class="even">
<td>metrics_client_account_view_through_conversions</td>
<td>The total number of view-through conversions. These happen when a customer sees an image or rich media ad, then later completes a conversion on your site without interacting with (for example, clicking on) another ad.</td>
</tr>
<tr class="odd">
<td>metrics_content_budget_lost_impression_share</td>
<td>The estimated percent of times that your ad was eligible to show on the Search Network but didn't because your budget was too low. Note: Search budget lost impression share is reported in the range of 0 to 0.9. Any value greater than 0.9 is reported as 0.9001.</td>
</tr>
<tr class="even">
<td>metrics_content_impression_share</td>
<td>The impressions you've received on the Display Network divided by the estimated number of impressions you were eligible to receive. Note: Content impression share is reported in the range of 0.1 to 1. Any value lower than 0.1 is reported as 0.0999.</td>
</tr>
<tr class="odd">
<td>metrics_content_rank_lost_impression_share</td>
<td>The estimated percentage of impressions on the Display Network that your ads didn't receive due to poor Ad Rank. Note: Content rank lost impression share is reported in the range of 0 to 0.9. Any value greater than 0.9 is reported as 0.9001.</td>
</tr>
<tr class="even">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies will optimize for these conversions.</td>
</tr>
<tr class="odd">
<td>metrics_conversions_value</td>
<td>The sum of conversion values for the conversions included in the "conversions" field. This metric is useful only if you entered a value for your conversion actions.</td>
</tr>
<tr class="even">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
</tr>
<tr class="odd">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
</tr>
<tr class="even">
<td>metrics_historical_quality_score</td>
<td>The historical quality score.</td>
</tr>
<tr class="odd">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
</tr>
<tr class="even">
<td>metrics_search_budget_lost_impression_share</td>
<td>The estimated percent of times that your ad was eligible to show on the Search Network but didn't because your budget was too low. Note: Search budget lost impression share is reported in the range of 0 to 0.9. Any value above 0.9 is reported as 0.9001.</td>
</tr>
<tr class="odd">
<td>metrics_search_impression_share</td>
<td>The impressions you've received on the Search Network divided by the estimated number of impressions you were eligible to receive. Note: Search impression share is reported in the range of 0.1 to 1. Any value below 0.1 is reported as 0.0999.</td>
</tr>
<tr class="even">
<td>metrics_search_rank_lost_impression_share</td>
<td>The estimated percentage of impressions on the Search Network that your ads didn't receive due to poor Ad Rank. Note: Search rank lost impression share is reported in the range of 0 to 0.9. Any value above 0.9 is reported as 0.9001.</td>
</tr>
<tr class="odd">
<td>metrics_visits</td>
<td>Clicks that Search Ads 360 has successfully recorded and forwarded to an advertiser's landing page.</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply, in yyyy-MM-dd format. For example: 2024-04-17</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: CartDataSalesStats

Search Ads 360 API Resource: [cart\_data\_sales\_view](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/cart_data_sales_view)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
<tr class="even">
<td>metrics_client_account_cross_sell_gross_profit_micros</td>
<td>https://developers.google.com/search-ads/reporting/api/reference/fields/v0/cart_data_sales_view#metrics.client_account_cross_sell_gross_profit_micros</td>
</tr>
<tr class="odd">
<td>metrics_client_account_cross_sell_revenue_micros</td>
<td>https://developers.google.com/search-ads/reporting/api/reference/fields/v0/cart_data_sales_view#metrics.client_account_cross_sell_revenue_micros</td>
</tr>
<tr class="even">
<td>metrics_client_account_cross_sell_units_sold</td>
<td>https://developers.google.com/search-ads/reporting/api/reference/fields/v0/cart_data_sales_view#metrics.client_account_cross_sell_units_sold</td>
</tr>
<tr class="odd">
<td>metrics_client_account_lead_gross_profit_micros</td>
<td>https://developers.google.com/search-ads/reporting/api/reference/fields/v0/cart_data_sales_view#metrics.client_account_lead_gross_profit_micros</td>
</tr>
<tr class="even">
<td>metrics_client_account_lead_revenue_micros</td>
<td>https://developers.google.com/search-ads/reporting/api/reference/fields/v0/cart_data_sales_view#metrics.client_account_lead_revenue_micros</td>
</tr>
<tr class="odd">
<td>metrics_client_account_lead_units_sold</td>
<td>https://developers.google.com/search-ads/reporting/api/reference/fields/v0/cart_data_sales_view#metrics.client_account_lead_units_sold</td>
</tr>
<tr class="even">
<td>metrics_cross_sell_gross_profit_micros</td>
<td>https://developers.google.com/search-ads/reporting/api/reference/fields/v0/cart_data_sales_view#metrics.cross_sell_gross_profit_micros</td>
</tr>
<tr class="odd">
<td>metrics_cross_sell_revenue_micros</td>
<td>https://developers.google.com/search-ads/reporting/api/reference/fields/v0/cart_data_sales_view#metrics.cross_sell_revenue_micros</td>
</tr>
<tr class="even">
<td>metrics_cross_sell_units_sold</td>
<td>https://developers.google.com/search-ads/reporting/api/reference/fields/v0/cart_data_sales_view#metrics.cross_sell_units_sold</td>
</tr>
<tr class="odd">
<td>metrics_lead_gross_profit_micros</td>
<td>https://developers.google.com/search-ads/reporting/api/reference/fields/v0/cart_data_sales_view#metrics.lead_gross_profit_micros</td>
</tr>
<tr class="even">
<td>metrics_lead_revenue_micros</td>
<td>https://developers.google.com/search-ads/reporting/api/reference/fields/v0/cart_data_sales_view#metrics.lead_revenue_micros</td>
</tr>
<tr class="odd">
<td>metrics_lead_units_sold</td>
<td>https://developers.google.com/search-ads/reporting/api/reference/fields/v0/cart_data_sales_view#metrics.lead_units_sold</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply, in yyyy-MM-dd format. For example: 2024-04-17</td>
</tr>
<tr class="odd">
<td>segments_product_brand</td>
<td>Brand of the product.</td>
</tr>
<tr class="even">
<td>segments_product_item_id</td>
<td>Item ID of the product.</td>
</tr>
<tr class="odd">
<td>segments_product_sold_brand</td>
<td>Brand of the product sold.</td>
</tr>
<tr class="even">
<td>segments_product_sold_item_id</td>
<td>Item ID of the product sold.</td>
</tr>
<tr class="odd">
<td>segments_product_sold_title</td>
<td>Title of the product sold.</td>
</tr>
<tr class="even">
<td>segments_product_sold_type_l1</td>
<td>Type (level 1) of the product sold.</td>
</tr>
<tr class="odd">
<td>segments_product_sold_type_l2</td>
<td>Type (level 2) of the product sold.</td>
</tr>
<tr class="even">
<td>segments_product_sold_type_l3</td>
<td>Type (level 3) of the product sold.</td>
</tr>
<tr class="odd">
<td>segments_product_sold_type_l4</td>
<td>Type (level 4) of the product sold.</td>
</tr>
<tr class="even">
<td>segments_product_sold_type_l5</td>
<td>Type (level 5) of the product sold.</td>
</tr>
<tr class="odd">
<td>segments_product_title</td>
<td>Title of the product.</td>
</tr>
<tr class="even">
<td>segments_product_type_l1</td>
<td>Type (level 1) of the product.</td>
</tr>
<tr class="odd">
<td>segments_product_type_l2</td>
<td>Type (level 2) of the product.</td>
</tr>
<tr class="even">
<td>segments_product_type_l3</td>
<td>Type (level 3) of the product.</td>
</tr>
<tr class="odd">
<td>segments_product_type_l4</td>
<td>Type (level 4) of the product.</td>
</tr>
<tr class="even">
<td>segments_product_type_l5</td>
<td>Type (level 5) of the product.</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: Conversion

Search Ads 360 API Resource: [conversion](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/conversion)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion.</td>
</tr>
<tr class="even">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
</tr>
<tr class="even">
<td>conversion_ad_id</td>
<td>Ad ID. A value of 0 indicates that the ad is unattributed.</td>
</tr>
<tr class="odd">
<td>conversion_advertiser_conversion_id</td>
<td>For offline conversions, this is an ID provided by advertisers. If an advertiser doesn't specify such an ID, Search Ads 360 generates one. For online conversions, this is equal to the id column or the floodlight_order_id column depending on the advertiser's Floodlight instructions.</td>
</tr>
<tr class="even">
<td>conversion_attribution_type</td>
<td>What the conversion is attributed to: Visit or Keyword+Ad.</td>
</tr>
<tr class="odd">
<td>conversion_click_id</td>
<td>A unique string, for the visit that the conversion is attributed to, that is passed to the landing page as the click id URL parameter.</td>
</tr>
<tr class="even">
<td>conversion_conversion_date_time</td>
<td>The timestamp of the conversion event.</td>
</tr>
<tr class="odd">
<td>conversion_conversion_last_modified_date_time</td>
<td>The timestamp of the last time the conversion was modified.</td>
</tr>
<tr class="even">
<td>conversion_conversion_quantity</td>
<td>The quantity of items recorded by the conversion, as determined by the qty url parameter. The advertiser is responsible for dynamically populating the parameter (such as number of items sold in the conversion), otherwise it defaults to 1.</td>
</tr>
<tr class="odd">
<td>conversion_conversion_revenue_micros</td>
<td>The adjusted revenue in micros for the conversion event. This will always be in the currency of the serving account.</td>
</tr>
<tr class="even">
<td>conversion_conversion_visit_date_time</td>
<td>The timestamp of the visit that the conversion is attributed to.</td>
</tr>
<tr class="odd">
<td>conversion_criterion_id</td>
<td>Search Ads 360 criterion ID. A value of 0 indicates that the criterion is unattributed.</td>
</tr>
<tr class="even">
<td>conversion_floodlight_order_id</td>
<td>The Floodlight order ID provided by the advertiser for the conversion.</td>
</tr>
<tr class="odd">
<td>conversion_floodlight_original_revenue</td>
<td>The original, unchanged revenue associated with the Floodlight event (in the currency of the current report), before Floodlight currency instruction modifications.</td>
</tr>
<tr class="even">
<td>conversion_id</td>
<td>The ID of the conversion</td>
</tr>
<tr class="odd">
<td>conversion_merchant_id</td>
<td>The SearchAds360 inventory account ID containing the product that was clicked on. SearchAds360 generates this ID when you link an inventory account in SearchAds360.</td>
</tr>
<tr class="even">
<td>conversion_product_channel</td>
<td>The sales channel of the product that was clicked on: Online or Local.</td>
</tr>
<tr class="odd">
<td>conversion_product_country_code</td>
<td>The country (ISO-3166-format) registered for the inventory feed that contains the product clicked on.</td>
</tr>
<tr class="even">
<td>conversion_product_id</td>
<td>The ID of the product clicked on.</td>
</tr>
<tr class="odd">
<td>conversion_product_language_code</td>
<td>The language (ISO-639-1) that has been set for the Merchant Center feed containing data about the product.</td>
</tr>
<tr class="even">
<td>conversion_product_store_id</td>
<td>The store in the Local Inventory Ad that was clicked on. This should match the store IDs used in your local products feed.</td>
</tr>
<tr class="odd">
<td>conversion_status</td>
<td>The status of the conversion, either ENABLED or REMOVED.</td>
</tr>
<tr class="even">
<td>conversion_visit_id</td>
<td>The SearchAds360 visit ID that the conversion is attributed to.</td>
</tr>
<tr class="odd">
<td>customer_account_type</td>
<td>Engine account type. For example: Google Ads, Microsoft Advertising, Yahoo Japan, Baidu, Facebook, Engine Track.</td>
</tr>
<tr class="even">
<td>customer_descriptive_name</td>
<td>Optional, non-unique descriptive name of the customer.</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
<tr class="even">
<td>segments.conversion_action_name</td>
<td>Conversion action name.</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply, in yyyy-MM-dd format. For example: 2024-04-17</td>
</tr>
<tr class="even">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: ConversionAction

Search Ads 360 API Resource: [conversion\_action](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/conversion_action)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>conversion_action_creation_time</td>
<td>Timestamp of the Floodlight activity's creation, formatted in ISO 8601.</td>
</tr>
<tr class="even">
<td>conversion_action_floodlight_settings_activity_group_tag</td>
<td>String used to identify a Floodlight activity group when reporting conversions.</td>
</tr>
<tr class="odd">
<td>conversion_action_floodlight_settings_activity_id</td>
<td>ID of the Floodlight activity in DoubleClick Campaign Manager (DCM).</td>
</tr>
<tr class="even">
<td>conversion_action_floodlight_settings_activity_tag</td>
<td>String used to identify a Floodlight activity when reporting conversions.</td>
</tr>
<tr class="odd">
<td>conversion_action_name</td>
<td>The name of the conversion action. This field is required and should not be empty when creating new conversion actions.</td>
</tr>
<tr class="even">
<td>conversion_action_status</td>
<td>The status of this conversion action for conversion event accrual.</td>
</tr>
<tr class="odd">
<td>conversion_action_type</td>
<td>The type of this conversion action.</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: GenderConversionActionAndDeviceStats

Search Ads 360 API Resource: [gender\_view](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/gender_view)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_criterion_age_range_type</td>
<td>Type of the age range.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_bid_modifier</td>
<td>The modifier for the bid when the criterion matches. The modifier must be in the range: 0.1 - 10.0. Most targetable criteria types support modifiers.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_cpc_bid_micros</td>
<td>The CPC (cost-per-click) bid.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_gender_type</td>
<td>Type of the gender.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_location_geo_target_constant</td>
<td>The geo target constant resource name.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_user_list_user_list</td>
<td>The User List resource name.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_webpage_conditions</td>
<td>Conditions, or logical expressions, for webpage targeting. The list of webpage targeting conditions are and-ed together when evaluated for targeting. An empty list of conditions indicates all pages of the campaign's website are targeted. This field is required for CREATE operations and is prohibited on UPDATE operations.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_webpage_coverage_percentage</td>
<td>Website criteria coverage percentage. This is the computed percentage of website coverage based on the website target, negative website target and negative keywords in the ad group and campaign. For instance, when coverage returns as 1, it indicates it has 100% coverage.</td>
</tr>
<tr class="even">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
<tr class="odd">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on an ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
</tr>
<tr class="even">
<td>metrics_cross_device_conversions_value</td>
<td>The sum of the value of cross-device conversions.</td>
</tr>
<tr class="odd">
<td>segments.conversion_action_name</td>
<td>Conversion action name.</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply, in yyyy-MM-dd format. For example: 2024-04-17</td>
</tr>
<tr class="odd">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: GenderDeviceStats

Search Ads 360 API Resource: [gender\_view](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/gender_view)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_criterion_age_range_type</td>
<td>Type of the age range.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_bid_modifier</td>
<td>The modifier for the bid when the criterion matches. The modifier must be in the range: 0.1 - 10.0. Most targetable criteria types support modifiers.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_cpc_bid_micros</td>
<td>The CPC (cost-per-click) bid.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_gender_type</td>
<td>Type of the gender.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_location_geo_target_constant</td>
<td>The geo target constant resource name.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_user_list_user_list</td>
<td>The User List resource name.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_webpage_conditions</td>
<td>Conditions, or logical expressions, for webpage targeting. The list of webpage targeting conditions are and-ed together when evaluated for targeting. An empty list of conditions indicates all pages of the campaign's website are targeted. This field is required for CREATE operations and is prohibited on UPDATE operations.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_webpage_coverage_percentage</td>
<td>Website criteria coverage percentage. This is the computed percentage of website coverage based on the website target, negative website target and negative keywords in the ad group and campaign. For instance, when coverage returns as 1, it indicates it has 100% coverage.</td>
</tr>
<tr class="even">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
<tr class="odd">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
</tr>
<tr class="even">
<td>metrics_average_cpm</td>
<td>Average cost-per-thousand impressions (CPM).</td>
</tr>
<tr class="odd">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
</tr>
<tr class="even">
<td>metrics_client_account_conversions</td>
<td>The number of client account conversions. This only includes conversion actions which include_in_client_account_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies will optimize for these conversions.</td>
</tr>
<tr class="odd">
<td>metrics_client_account_conversions_value</td>
<td>The value of client account conversions. This only includes conversion actions which include_in_client_account_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies will optimize for these conversions.</td>
</tr>
<tr class="even">
<td>metrics_client_account_view_through_conversions</td>
<td>The total number of view-through conversions. These happen when a customer sees an image or rich media ad, then later completes a conversion on your site without interacting with (for example, clicking on) another ad.</td>
</tr>
<tr class="odd">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
</tr>
<tr class="even">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
</tr>
<tr class="odd">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply, in yyyy-MM-dd format. For example: 2024-04-17</td>
</tr>
<tr class="odd">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: Keyword

Search Ads 360 API Resource: [keyword\_view](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/keyword_view)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_criterion_cpc_bid_micros</td>
<td>The CPC (cost-per-click) bid.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_creation_time</td>
<td>The timestamp when this ad group criterion was created. The timestamp is in the customer's time zone and in "yyyy-MM-dd HH:mm:ss" format.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_effective_cpc_bid_micros</td>
<td>The effective CPC (cost-per-click) bid.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_engine_id</td>
<td>ID of the ad group criterion in the external engine account. This field is for SearchAds 360 account only,. For example: Yahoo Japan, Microsoft, Baidu. For non-SearchAds 360 entity, use "ad_group_criterion.criterion_id" instead.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_engine_status</td>
<td>The Engine Status for ad group criterion.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_final_url_suffix</td>
<td>URL template for appending params to final URL.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_final_urls</td>
<td>The list of possible final URLs after all cross-domain redirects for the ad.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_keyword_match_type</td>
<td>The match type of the keyword.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_keyword_text</td>
<td>The text of the keyword (at most 80 characters and 10 words).</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_labels</td>
<td>The resource names of labels attached to this ad group criterion.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_last_modified_time</td>
<td>The datetime when this ad group criterion was last modified. The datetime is in the customer's time zone and in "yyyy-MM-dd HH:mm:ss.ssssss" format.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_quality_info_quality_score</td>
<td>The quality score. This field may not be populated if Google does not have enough information to determine a value.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_status</td>
<td>The status of the criterion. This is the status of the ad group criterion entity, set by the client. Note: UI reports may incorporate additional information that affects whether a criterion is eligible to run. In some cases a criterion that's REMOVED in the API can still show as enabled in the UI. For example, campaigns by default show to users of all age ranges unless excluded. The UI will show each age range as "enabled", since they're eligible to see the ads; but AdGroupCriterion.status will show "removed", since no positive criterion was added.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_tracking_url_template</td>
<td>The URL template for constructing a tracking URL.</td>
</tr>
<tr class="even">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
</tr>
<tr class="odd">
<td>bidding_strategy_id</td>
<td>The ID of the bidding strategy.</td>
</tr>
<tr class="even">
<td>bidding_strategy_target_cpa_cpc_bid_ceiling_micros</td>
<td>Maximum bid limit that can be set by the bid strategy. The limit applies to all keywords managed by the strategy. This should only be set for portfolio bid strategies.</td>
</tr>
<tr class="odd">
<td>bidding_strategy_target_cpa_cpc_bid_floor_micros</td>
<td>Minimum bid limit that can be set by the bid strategy. The limit applies to all keywords managed by the strategy. This should only be set for portfolio bid strategies.</td>
</tr>
<tr class="even">
<td>bidding_strategy_target_impression_share_cpc_bid_ceiling_micros</td>
<td>The highest CPC bid the automated bidding system is permitted to specify. This is a required field entered by the advertiser that sets the ceiling and specified in local micros.</td>
</tr>
<tr class="odd">
<td>bidding_strategy_target_outrank_share_cpc_bid_ceiling_micros</td>
<td>Maximum bid limit that can be set by the bid strategy. The limit applies to all keywords managed by the strategy.</td>
</tr>
<tr class="even">
<td>bidding_strategy_target_roas_cpc_bid_ceiling_micros</td>
<td>Maximum bid limit that can be set by the bid strategy. The limit applies to all keywords managed by the strategy. This should only be set for portfolio bid strategies.</td>
</tr>
<tr class="odd">
<td>bidding_strategy_target_roas_cpc_bid_floor_micros</td>
<td>Minimum bid limit that can be set by the bid strategy. The limit applies to all keywords managed by the strategy. This should only be set for portfolio bid strategies.</td>
</tr>
<tr class="even">
<td>bidding_strategy_target_spend_cpc_bid_ceiling_micros</td>
<td>Maximum bid limit that can be set by the bid strategy. The limit applies to all keywords managed by the strategy.</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: KeywordConversionActionAndDeviceStats

Search Ads 360 API Resource: [keyword\_view](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/keyword_view)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_engine_id</td>
<td>ID of the ad group criterion in the external engine account. This field is for SearchAds 360 account only. For example: Yahoo Japan, Microsoft, Baidu. For non-SearchAds 360 entity, use "ad_group_criterion.criterion_id" instead.</td>
</tr>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
</tr>
<tr class="even">
<td>bidding_strategy_id</td>
<td>The ID of the bidding strategy.</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This includes all conversions regardless of the value of include_in_conversions_metric.</td>
</tr>
<tr class="even">
<td>metrics_all_conversions_by_conversion_date</td>
<td>The total number of conversions. This includes all conversions regardless of the value of include_in_conversions_metric. When this column is selected with date, the values in date column means the conversion date. For more information about <code dir="ltr" translate="no">       by_conversion_date      </code> columns, see <a href="https://support.google.com/sa360/answer/9250611">About the "All conversions" column</a> .</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions_value</td>
<td>The value of all conversions.</td>
</tr>
<tr class="even">
<td>metrics_all_conversions_value_by_conversion_date</td>
<td>The value of all conversions. When this column is selected with date, the values in date column means the conversion date. For more information about <code dir="ltr" translate="no">       by_conversion_date      </code> columns, see <a href="https://support.google.com/sa360/answer/9250611">About the "All conversions" column</a> .</td>
</tr>
<tr class="odd">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on an ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
</tr>
<tr class="even">
<td>metrics_cross_device_conversions_by_conversion_date</td>
<td>The number of cross-device conversions by conversion date. For more information about <code dir="ltr" translate="no">       by_conversion_date      </code> columns, see <a href="https://support.google.com/sa360/answer/9250611">About the "All conversions" column</a> .</td>
</tr>
<tr class="odd">
<td>metrics_cross_device_conversions_value</td>
<td>The sum of the value of cross-device conversions.</td>
</tr>
<tr class="even">
<td>metrics_cross_device_conversions_value_by_conversion_date</td>
<td>The sum of cross-device conversions value by conversion date. For more information about <code dir="ltr" translate="no">       by_conversion_date      </code> columns, see <a href="https://support.google.com/sa360/answer/9250611">About the "All conversions" column</a> .</td>
</tr>
<tr class="odd">
<td>segments.conversion_action_name</td>
<td>Conversion action name.</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply, in yyyy-MM-dd format. For example: 2024-04-17</td>
</tr>
<tr class="odd">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: KeywordDeviceStats

Search Ads 360 API Resource: [keyword\_view](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/keyword_view)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_engine_id</td>
<td>ID of the ad group criterion in the external engine account. This field is for SearchAds 360 account only. For example: Yahoo Japan, Microsoft, Baidu. For non-SearchAds 360 entity, use "ad_group_criterion.criterion_id" instead.</td>
</tr>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
</tr>
<tr class="even">
<td>bidding_strategy_id</td>
<td>The ID of the bidding strategy.</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
<tr class="odd">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
</tr>
<tr class="even">
<td>metrics_average_cpm</td>
<td>Average cost-per-thousand impressions (CPM).</td>
</tr>
<tr class="odd">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
</tr>
<tr class="even">
<td>metrics_client_account_conversions</td>
<td>The number of client account conversions. This only includes conversion actions which include_in_client_account_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies will optimize for these conversions.</td>
</tr>
<tr class="odd">
<td>metrics_client_account_conversions_value</td>
<td>The value of client account conversions. This only includes conversion actions which include_in_client_account_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies will optimize for these conversions.</td>
</tr>
<tr class="even">
<td>metrics_client_account_view_through_conversions</td>
<td>The total number of view-through conversions. These happen when a customer sees an image or rich media ad, then later completes a conversion on your site without interacting with (for example, clicking on) another ad.</td>
</tr>
<tr class="odd">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
</tr>
<tr class="even">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
</tr>
<tr class="odd">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
</tr>
<tr class="even">
<td>metrics_visits</td>
<td>Clicks that Search Ads 360 has successfully recorded and forwarded to an advertiser's landing page.</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply, in yyyy-MM-dd format. For example: 2024-04-17</td>
</tr>
<tr class="even">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: KeywordStats

Search Ads 360 API Resource: [keyword\_view](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/keyword_view)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion.</td>
</tr>
<tr class="even">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
</tr>
<tr class="odd">
<td>bidding_strategy_id</td>
<td>The ID of the bidding strategy.</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
<tr class="even">
<td>metrics_historical_quality_score</td>
<td>The historical quality score.</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply, in yyyy-MM-dd format. For example: 2024-04-17</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: LocationConversionActionAndDeviceStats

Search Ads 360 API Resource: [location\_view](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/location_view)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>campaign_criterion_criterion_id</td>
<td>The ID of the criterion.</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
<tr class="even">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This includes all conversions regardless of the value of include_in_conversions_metric.</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions_value</td>
<td>The value of all conversions.</td>
</tr>
<tr class="even">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on an ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
</tr>
<tr class="odd">
<td>metrics_cross_device_conversions_value</td>
<td>The sum of the value of cross-device conversions.</td>
</tr>
<tr class="even">
<td>segments.conversion_action_name</td>
<td>Conversion action name.</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply, in yyyy-MM-dd format. For example: 2024-04-17</td>
</tr>
<tr class="even">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: LocationDeviceStats

Search Ads 360 API Resource: [location\_view](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/location_view)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>campaign_criterion_criterion_id</td>
<td>The ID of the criterion.</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
<tr class="even">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
</tr>
<tr class="odd">
<td>metrics_average_cpm</td>
<td>Average cost-per-thousand impressions (CPM).</td>
</tr>
<tr class="even">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
</tr>
<tr class="odd">
<td>metrics_client_account_conversions</td>
<td>The number of client account conversions. This only includes conversion actions which include_in_client_account_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies will optimize for these conversions.</td>
</tr>
<tr class="even">
<td>metrics_client_account_conversions_value</td>
<td>The value of client account conversions. This only includes conversion actions which include_in_client_account_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies will optimize for these conversions.</td>
</tr>
<tr class="odd">
<td>metrics_client_account_view_through_conversions</td>
<td>The total number of view-through conversions. These happen when a customer sees an image or rich media ad, then later completes a conversion on your site without interacting with (for example, clicking on) another ad.</td>
</tr>
<tr class="even">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
</tr>
<tr class="odd">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
</tr>
<tr class="even">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply, in yyyy-MM-dd format. For example: 2024-04-17</td>
</tr>
<tr class="even">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: NegativeAdGroupCriterion

Search Ads 360 API Resource: [ad\_group\_criterion](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/ad_group_criterion)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_criterion_age_range_type</td>
<td>Type of the age range.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_creation_time</td>
<td>The timestamp when this ad group criterion was created. The timestamp is in the customer's time zone and in "yyyy-MM-dd HH:mm:ss" format.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_gender_type</td>
<td>Type of the gender.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_last_modified_time</td>
<td>The datetime when this ad group criterion was last modified. The datetime is in the customer's time zone and in "yyyy-MM-dd HH:mm:ss.ssssss" format.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_location_geo_target_constant</td>
<td>The geo target constant resource name.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_status</td>
<td>The status of the criterion. This is the status of the ad group criterion entity, set by the client. Note: UI reports may incorporate additional information that affects whether a criterion is eligible to run. In some cases a criterion that's REMOVED in the API can still show as enabled in the UI. For example, campaigns by default show to users of all age ranges unless excluded. The UI will show each age range as "enabled", since they're eligible to see the ads; but AdGroupCriterion.status will show "removed", since no positive criterion was added.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_type</td>
<td>The type of the criterion.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_user_list_user_list</td>
<td>The User List resource name.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_webpage_conditions</td>
<td>Conditions, or logical expressions, for web page targeting. The list of web page targeting conditions are and-ed together when evaluated for targeting. An empty list of conditions indicates all pages of the campaign's website are targeted. This field is required for CREATE operations and is prohibited on UPDATE operations.</td>
</tr>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: NegativeAdGroupKeyword

Search Ads 360 API Resource: [ad\_group\_criterion](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/ad_group_criterion)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_criterion_creation_time</td>
<td>The timestamp when this ad group criterion was created. The timestamp is in the customer's time zone and in "yyyy-MM-dd HH:mm:ss" format.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_keyword_match_type</td>
<td>The match type of the keyword.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_keyword_text</td>
<td>The text of the keyword (at most 80 characters and 10 words).</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_last_modified_time</td>
<td>The datetime when this ad group criterion was last modified. The datetime is in the customer's time zone and in "yyyy-MM-dd HH:mm:ss.ssssss" format.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_status</td>
<td>The status of the criterion. This is the status of the ad group criterion entity, set by the client. Note: UI reports may incorporate additional information that affects whether a criterion is eligible to run. In some cases a criterion that's REMOVED in the API can still show as enabled in the UI. For example, campaigns by default show to users of all age ranges unless excluded. The UI will show each age range as "enabled", since they're eligible to see the ads; but AdGroupCriterion.status will show "removed", since no positive criterion was added.</td>
</tr>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: NegativeCampaignCriterion

Search Ads 360 API Resource: [campaign\_criterion](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/campaign_criterion)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>campaign_criterion_age_range_type</td>
<td>Type of the age range.</td>
</tr>
<tr class="even">
<td>campaign_criterion_criterion_id</td>
<td>The ID of the criterion.</td>
</tr>
<tr class="odd">
<td>campaign_criterion_gender_type</td>
<td>Type of the gender.</td>
</tr>
<tr class="even">
<td>campaign_criterion_last_modified_time</td>
<td>The datetime when this campaign criterion was last modified. The datetime is in the customer's time zone and in "yyyy-MM-dd HH:mm:ss.ssssss" format.</td>
</tr>
<tr class="odd">
<td>campaign_criterion_location_geo_target_constant</td>
<td>The geo target constant resource name.</td>
</tr>
<tr class="even">
<td>campaign_criterion_status</td>
<td>The status of the criterion.</td>
</tr>
<tr class="odd">
<td>campaign_criterion_type</td>
<td>The type of the criterion.</td>
</tr>
<tr class="even">
<td>campaign_criterion_user_list_user_list</td>
<td>The User List resource name.</td>
</tr>
<tr class="odd">
<td>campaign_criterion_webpage_conditions</td>
<td>Conditions, or logical expressions, for webpage targeting. The list of webpage targeting conditions are and-ed together when evaluated for targeting. An empty list of conditions indicates all pages of the campaign's website are targeted. This field is required for CREATE operations and is prohibited on UPDATE operations.</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: NegativeCampaignKeyword

Search Ads 360 API Resource: [campaign\_criterion](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/campaign_criterion)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>campaign_criterion_criterion_id</td>
<td>The ID of the criterion.</td>
</tr>
<tr class="even">
<td>campaign_criterion_keyword_match_type</td>
<td>The match type of the keyword.</td>
</tr>
<tr class="odd">
<td>campaign_criterion_keyword_text</td>
<td>The text of the keyword (at most 80 characters and 10 words).</td>
</tr>
<tr class="even">
<td>campaign_criterion_last_modified_time</td>
<td>The datetime when this ad group criterion was last modified. The datetime is in the customer's time zone and in "yyyy-MM-dd HH:mm:ss.ssssss" format.</td>
</tr>
<tr class="odd">
<td>campaign_criterion_status</td>
<td>The status of the criterion.</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: ProductAdvertised

Search Ads 360 API Resource: [shopping\_performance\_view](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/shopping_performance_view)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
<tr class="even">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
</tr>
<tr class="odd">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
</tr>
<tr class="even">
<td>metrics_client_account_conversions</td>
<td>The number of client account conversions. This only includes conversion actions which include_in_client_account_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies will optimize for these conversions.</td>
</tr>
<tr class="odd">
<td>metrics_client_account_conversions_value</td>
<td>The value of client account conversions. This only includes conversion actions which include_in_client_account_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies will optimize for these conversions.</td>
</tr>
<tr class="even">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
</tr>
<tr class="odd">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
</tr>
<tr class="even">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply, in yyyy-MM-dd format. For example: 2024-04-17</td>
</tr>
<tr class="even">
<td>segments_product_bidding_category_level1</td>
<td>Bidding category (level 1) of the product.</td>
</tr>
<tr class="odd">
<td>segments_product_bidding_category_level2</td>
<td>Bidding category (level 2) of the product.</td>
</tr>
<tr class="even">
<td>segments_product_bidding_category_level3</td>
<td>Bidding category (level 3) of the product.</td>
</tr>
<tr class="odd">
<td>segments_product_bidding_category_level4</td>
<td>Bidding category (level 4) of the product.</td>
</tr>
<tr class="even">
<td>segments_product_bidding_category_level5</td>
<td>Bidding category (level 5) of the product.</td>
</tr>
<tr class="odd">
<td>segments_product_brand</td>
<td>Brand of the product.</td>
</tr>
<tr class="even">
<td>segments_product_channel</td>
<td>Channel of the product.</td>
</tr>
<tr class="odd">
<td>segments_product_channel_exclusivity</td>
<td>Channel exclusivity of the product.</td>
</tr>
<tr class="even">
<td>segments_product_condition</td>
<td>Condition of the product.</td>
</tr>
<tr class="odd">
<td>segments_product_country</td>
<td>Resource name of the geo target constant for the country of sale of the product.</td>
</tr>
<tr class="even">
<td>segments_product_custom_attribute0</td>
<td>Custom attribute 0 of the product.</td>
</tr>
<tr class="odd">
<td>segments_product_custom_attribute1</td>
<td>Custom attribute 1 of the product.</td>
</tr>
<tr class="even">
<td>segments_product_custom_attribute2</td>
<td>Custom attribute 2 of the product.</td>
</tr>
<tr class="odd">
<td>segments_product_custom_attribute3</td>
<td>Custom attribute 3 of the product.</td>
</tr>
<tr class="even">
<td>segments_product_custom_attribute4</td>
<td>Custom attribute 4 of the product.</td>
</tr>
<tr class="odd">
<td>segments_product_item_id</td>
<td>Item ID of the product.</td>
</tr>
<tr class="even">
<td>segments_product_language</td>
<td>Resource name of the language constant for the language of the product.</td>
</tr>
<tr class="odd">
<td>segments_product_store_id</td>
<td>Store ID of the product.</td>
</tr>
<tr class="even">
<td>segments_product_title</td>
<td>Title of the product.</td>
</tr>
<tr class="odd">
<td>segments_product_type_l1</td>
<td>Type (level 1) of the product.</td>
</tr>
<tr class="even">
<td>segments_product_type_l2</td>
<td>Type (level 2) of the product.</td>
</tr>
<tr class="odd">
<td>segments_product_type_l3</td>
<td>Type (level 3) of the product.</td>
</tr>
<tr class="even">
<td>segments_product_type_l4</td>
<td>Type (level 4) of the product.</td>
</tr>
<tr class="odd">
<td>segments_product_type_l5</td>
<td>Type (level 5) of the product.</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: ProductAdvertisedConversionActionAndDeviceStats

Search Ads 360 API Resource: [shopping\_performance\_view](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/shopping_performance_view)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
<tr class="even">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This includes all conversions regardless of the value of include_in_conversions_metric.</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions_value</td>
<td>The value of all conversions.</td>
</tr>
<tr class="even">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on an ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
</tr>
<tr class="odd">
<td>metrics_cross_device_conversions_value</td>
<td>The sum of the value of cross-device conversions.</td>
</tr>
<tr class="even">
<td>segments.conversion_action_name</td>
<td>Conversion action name.</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply, in yyyy-MM-dd format. For example: 2024-04-17</td>
</tr>
<tr class="even">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
</tr>
<tr class="odd">
<td>segments_product_item_id</td>
<td>Item ID of the product.</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: ProductAdvertisedDeviceStats

Search Ads 360 API Resource: [shopping\_performance\_view](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/shopping_performance_view)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
<tr class="even">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
</tr>
<tr class="odd">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
</tr>
<tr class="even">
<td>metrics_client_account_conversions</td>
<td>The number of client account conversions. This only includes conversion actions which include_in_client_account_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies will optimize for these conversions.</td>
</tr>
<tr class="odd">
<td>metrics_client_account_conversions_value</td>
<td>The value of client account conversions. This only includes conversion actions which include_in_client_account_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies will optimize for these conversions.</td>
</tr>
<tr class="even">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
</tr>
<tr class="odd">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
</tr>
<tr class="even">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply, in yyyy-MM-dd format. For example: 2024-04-17</td>
</tr>
<tr class="even">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
</tr>
<tr class="odd">
<td>segments_product_item_id</td>
<td>Item ID of the product.</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: ProductGroup

Search Ads 360 API Resource: [product\_group\_view](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/product_group_view)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_criterion_cpc_bid_micros</td>
<td>The CPC (cost-per-click) bid.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_creation_time</td>
<td>Output only. The timestamp when this ad group criterion was created. The timestamp is in the customer's time zone and in "yyyy-MM-dd HH:mm:ss" format.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_criterion_id</td>
<td>Output only. The ID of the criterion.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_effective_cpc_bid_micros</td>
<td>Output only. The effective CPC (cost-per-click) bid.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_engine_status</td>
<td>Output only. The Engine Status for ad group criterion.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_final_urls</td>
<td>The list of possible final URLs after all cross-domain redirects for the ad.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_last_modified_time</td>
<td>Output only. The datetime when this ad group criterion was last modified. The datetime is in the customer's time zone and in "yyyy-MM-dd HH:mm:ss.ssssss" format.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_listing_group_type</td>
<td>Type of the listing group.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_status</td>
<td>The status of the criterion. This is the status of the ad group criterion entity, set by the client. Note: UI reports may incorporate additional information that affects whether a criterion is eligible to run. In some cases a criterion that's REMOVED in the API can still show as enabled in the UI. For example, campaigns by default show to users of all age ranges unless excluded. The UI will show each age range as "enabled", since they're eligible to see the ads; but AdGroupCriterion.status will show "removed", since no positive criterion was added.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_tracking_url_template</td>
<td>The URL template for constructing a tracking URL.</td>
</tr>
<tr class="odd">
<td>ad_group_id</td>
<td>Output only. The ID of the ad group.</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>Output only. The ID of the campaign.</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
<tr class="even">
<td>product_group_view_resource_name</td>
<td>Output only. The resource name of the product group view. Product group view resource names have the form: customers/{customer_id}/productGroupViews/{ad_group_id}~{criterion_id}</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: ProductGroupStats

Search Ads 360 API Resource: [product\_group\_view](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/product_group_view)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_criterion_criterion_id</td>
<td>Output only. The ID of the criterion.</td>
</tr>
<tr class="even">
<td>ad_group_id</td>
<td>Output only. The ID of the ad group.</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>Output only. The ID of the campaign.</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This includes all conversions regardless of the value of include_in_conversions_metric.</td>
</tr>
<tr class="even">
<td>metrics_all_conversions_value</td>
<td>The value of all conversions.</td>
</tr>
<tr class="odd">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
</tr>
<tr class="even">
<td>metrics_average_cpm</td>
<td>Average cost-per-thousand impressions (CPM).</td>
</tr>
<tr class="odd">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
</tr>
<tr class="even">
<td>metrics_client_account_conversions</td>
<td>The number of client account conversions. This only includes conversion actions which include_in_client_account_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies will optimize for these conversions.</td>
</tr>
<tr class="odd">
<td>metrics_client_account_conversions_value</td>
<td>The value of client account conversions. This only includes conversion actions which include_in_client_account_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies will optimize for these conversions.</td>
</tr>
<tr class="even">
<td>metrics_client_account_view_through_conversions</td>
<td>The total number of view-through conversions. These happen when a customer sees an image or rich media ad, then later completes a conversion on your site without interacting with (for example, clicking on) another ad.</td>
</tr>
<tr class="odd">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
</tr>
<tr class="even">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on an ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
</tr>
<tr class="odd">
<td>metrics_cross_device_conversions_value</td>
<td>The sum of the value of cross-device conversions.</td>
</tr>
<tr class="even">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
</tr>
<tr class="odd">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply, in yyyy-MM-dd format. For example: 2024-04-17</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: Visit

Search Ads 360 API Resource: [visit](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/visit)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion.</td>
</tr>
<tr class="even">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
</tr>
<tr class="even">
<td>customer_account_type</td>
<td>Engine account type. For example: Google Ads, Microsoft Advertising, Yahoo Japan, Baidu, Facebook, Engine Track.</td>
</tr>
<tr class="odd">
<td>customer_descriptive_name</td>
<td>Optional, non-unique descriptive name of the customer.</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
<tr class="odd">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply, in yyyy-MM-dd format. For example: 2024-04-17</td>
</tr>
<tr class="odd">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
</tr>
<tr class="even">
<td>visit_ad_id</td>
<td>Ad ID. A value of 0 indicates that the ad is unattributed.</td>
</tr>
<tr class="odd">
<td>visit_click_id</td>
<td>A unique string for each visit that is passed to the landing page as the click id URL parameter.</td>
</tr>
<tr class="even">
<td>visit_criterion_id</td>
<td>Search Ads 360 keyword ID. A value of 0 indicates that the keyword is unattributed..</td>
</tr>
<tr class="odd">
<td>visit_id</td>
<td>The ID of the visit.</td>
</tr>
<tr class="even">
<td>visit_merchant_id</td>
<td>The Search Ads 360 inventory account ID containing the product that was clicked on. Search Ads 360 generates this ID when you link an inventory account in Search Ads 360.</td>
</tr>
<tr class="odd">
<td>visit_product_channel</td>
<td>The sales channel of the product that was clicked on: Online or Local.</td>
</tr>
<tr class="even">
<td>visit_product_country_code</td>
<td>The country (ISO-3166 format) registered for the inventory feed that contains the product clicked on.</td>
</tr>
<tr class="odd">
<td>visit_product_id</td>
<td>The ID of the product clicked on.</td>
</tr>
<tr class="even">
<td>visit_product_language_code</td>
<td>The language (ISO-639-1) that has been set for the Merchant Center feed containing data about the product.</td>
</tr>
<tr class="odd">
<td>visit_product_store_id</td>
<td>The store in the Local Inventory Ad that was clicked on. This should match the store IDs used in your local products feed.</td>
</tr>
<tr class="even">
<td>visit_visit_date_time</td>
<td>The timestamp of the visit event. The timestamp is in the customer's time zone and in "yyyy-MM-dd HH:mm:ss" format.</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: WebpageConversionActionAndDeviceStats

Search Ads 360 API Resource: [webpage\_view](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/webpage_view)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_criterion_age_range_type</td>
<td>Type of the age range.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_bid_modifier</td>
<td>The modifier for the bid when the criterion matches. The modifier must be in the range: 0.1 - 10.0. Most targetable criteria types support modifiers.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_cpc_bid_micros</td>
<td>The CPC (cost-per-click) bid.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_gender_type</td>
<td>Type of the gender.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_location_geo_target_constant</td>
<td>The geo target constant resource name.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_user_list_user_list</td>
<td>The User List resource name.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_webpage_conditions</td>
<td>Conditions, or logical expressions, for webpage targeting. The list of webpage targeting conditions are and-ed together when evaluated for targeting. An empty list of conditions indicates all pages of the campaign's website are targeted. This field is required for CREATE operations and is prohibited on UPDATE operations.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_webpage_coverage_percentage</td>
<td>Website criteria coverage percentage. This is the computed percentage of website coverage based on the website target, negative website target and negative keywords in the ad group and campaign. For instance, when coverage returns as 1, it indicates it has 100% coverage.</td>
</tr>
<tr class="even">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
<tr class="odd">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on an ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
</tr>
<tr class="even">
<td>metrics_cross_device_conversions_value</td>
<td>The sum of the value of cross-device conversions.</td>
</tr>
<tr class="odd">
<td>segments_conversion_action_name</td>
<td>Conversion action name.</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply, in yyyy-MM-dd format. For example: 2024-04-17</td>
</tr>
<tr class="odd">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
</tr>
</tbody>
</table>

Search Ads 360 Table Name: WebpageDeviceStats

Search Ads 360 API Resource: [webpage\_view](https://developers.google.com/search-ads/reporting/api/reference/fields/v0/webpage_view)

<table>
<thead>
<tr class="header">
<th>Search Ads 360 Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_criterion_age_range_type</td>
<td>Type of the age range.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_bid_modifier</td>
<td>The modifier for the bid when the criterion matches. The modifier must be in the range: 0.1 - 10.0. Most targetable criteria types support modifiers.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_cpc_bid_micros</td>
<td>The CPC (cost-per-click) bid.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_gender_type</td>
<td>Type of the gender.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_location_geo_target_constant</td>
<td>The geo target constant resource name.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_user_list_user_list</td>
<td>The User List resource name.</td>
</tr>
<tr class="even">
<td>ad_group_criterion_webpage_conditions</td>
<td>Conditions, or logical expressions, for webpage targeting. The list of webpage targeting conditions are and-ed together when evaluated for targeting. An empty list of conditions indicates all pages of the campaign's website are targeted. This field is required for CREATE operations and is prohibited on UPDATE operations.</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_webpage_coverage_percentage</td>
<td>Website criteria coverage percentage. This is the computed percentage of website coverage based on the website target, negative website target and negative keywords in the ad group and campaign. For instance, when coverage returns as 1, it indicates it has 100% coverage.</td>
</tr>
<tr class="even">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
</tr>
<tr class="odd">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
</tr>
<tr class="even">
<td>metrics_average_cpm</td>
<td>Average cost-per-thousand impressions (CPM).</td>
</tr>
<tr class="odd">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
</tr>
<tr class="even">
<td>metrics_client_account_conversions</td>
<td>The number of client account conversions. This only includes conversion actions which include_in_client_account_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies will optimize for these conversions.</td>
</tr>
<tr class="odd">
<td>metrics_client_account_conversions_value</td>
<td>The value of client account conversions. This only includes conversion actions which include_in_client_account_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies will optimize for these conversions.</td>
</tr>
<tr class="even">
<td>metrics_client_account_view_through_conversions</td>
<td>The total number of view-through conversions. These happen when a customer sees an image or rich media ad, then later completes a conversion on your site without interacting with (for example, clicking on) another ad.</td>
</tr>
<tr class="odd">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
</tr>
<tr class="even">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
</tr>
<tr class="odd">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply, in yyyy-MM-dd format. For example: 2024-04-17</td>
</tr>
<tr class="odd">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
</tr>
</tbody>
</table>

## Search Ads 360 Match Tables

Search Ads 360 Match Tables are tables that contain only **Attribute** fields (fields containing settings or other fixed data), and they are defined for users to query account structure information. If you use the refresh window or schedule a backfill, Match Table snapshots are not updated.

Below is a list of Match Tables in Search Ads 360 transfer:

  - Account
  - Ad
  - AdGroup
  - AdGroupCriterion
  - Any [ID mapping table](/bigquery/docs/search-ads-transfer#id-mapping)
  - Asset
  - BidStrategy
  - Campaign
  - CampaignCriterion
  - ConversionAction
  - Keyword
  - NegativeAdGroupKeyword
  - NegativeAdGroupCriterion
  - NegativeCampaignKeyword
  - NegativeCampaignCriterion
  - ProductGroup
