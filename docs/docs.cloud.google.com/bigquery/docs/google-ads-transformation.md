# Google Ads report transformation

This document describes how you can transform your reports for Google Ads (formerly known as Google AdWords).

## Table mapping for Google Ads reports

When your Google Ads reports are transferred to BigQuery, the reports are transformed into the following BigQuery tables and views.

When you view the tables and views in BigQuery, the value for customer\_id is your Google Ads customer ID.

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>AdWords reports (deprecated)</th>
<th>BigQuery AdWords tables</th>
<th>Google Ads tables</th>
<th>Google Ads API resources (v21.0.0)</th>
<th>BigQuery views</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://developers.google.com/adwords/api/docs/appendix/reports/account-performance-report">Account Performance Report</a></td>
<td>p_Customer_ customer_id<br />
p_HourlyAccountConversionStats_ customer_id<br />
p_AccountConversionStats_ customer_id<br />
p_HourlyAccountStats_ customer_id<br />
p_AccountNonClickStats_ customer_id<br />
p_AccountBasicStats_ customer_id<br />
p_AccountStats_ customer_id</td>
<td>p_ads_Customer_ customer_id<br />
p_ads_HourlyAccountConversionStats_ customer_id<br />
p_ads_AccountConversionStats_ customer_id<br />
p_ads_HourlyAccountStats_ customer_id<br />
p_ads_AccountNonClickStats_ customer_id<br />
p_ads_AccountBasicStats_ customer_id<br />
p_ads_AccountStats_ customer_id</td>
<td><a href="https://developers.google.com/google-ads/api/fields/v21/customer">Customer</a></td>
<td>Customer_ customer_id<br />
HourlyAccountConversionStats_ customer_id<br />
AccountConversionStats_ customer_id<br />
HourlyAccountStats_ customer_id<br />
AccountNonClickStats_ customer_id<br />
AccountBasicStats_ customer_id<br />
AccountStats_ customer_id</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/adwords/api/docs/appendix/reports/ad-performance-report">Ad Performance Report</a></td>
<td>p_AdBasicStats_ customer_id<br />
p_AdCrossDeviceStats_ customer_id<br />
p_AdConversionStats_ customer_id<br />
p_AdStats_ customer_id<br />
p_AdCrossDeviceConversionStats_ customer_id<br />
p_Ad_ customer_id</td>
<td>p_ads_AdBasicStats_ customer_id<br />
p_ads_AdCrossDeviceStats_ customer_id<br />
p_ads_AdConversionStats_ customer_id<br />
p_ads_AdStats_ customer_id<br />
p_ads_AdCrossDeviceConversionStats_ customer_id<br />
p_ads_Ad_ customer_id</td>
<td><a href="https://developers.google.com/google-ads/api/fields/v21/ad_group_ad">Ad Group Ad</a></td>
<td>AdBasicStats_ customer_id<br />
AdCrossDeviceStats_ customer_id<br />
AdConversionStats_ customer_id<br />
AdStats_ customer_id<br />
AdCrossDeviceConversionStats_ customer_id<br />
Ad_ customer_id</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/adwords/api/docs/appendix/reports/adgroup-performance-report">Adgroup Performance Report</a></td>
<td>p_AdGroupStats_ customer_id<br />
p_AdGroupBasicStats_ customer_id<br />
p_AdGroupCrossDeviceStats_ customer_id<br />
p_HourlyAdGroupConversionStats_ customer_id<br />
p_HourlyAdGroupStats_ customer_id<br />
p_AdGroupConversionStats_ customer_id<br />
p_AdGroupCrossDeviceConversionStats_ customer_id<br />
p_AdGroup_ customer_id</td>
<td>p_ads_AdGroupStats_ customer_id<br />
p_ads_AdGroupBasicStats_ customer_id<br />
p_ads_AdGroupCrossDeviceStats_ customer_id<br />
p_ads_HourlyAdGroupConversionStats_ customer_id<br />
p_ads_HourlyAdGroupStats_ customer_id<br />
p_ads_AdGroupConversionStats_ customer_id<br />
p_ads_AdGroupCrossDeviceConversionStats_ customer_id<br />
p_ads_AdGroup_ customer_id</td>
<td><a href="https://developers.google.com/google-ads/api/fields/v21/ad_group">Ad Group</a></td>
<td>AdGroupStats_ customer_id<br />
AdGroupBasicStats_ customer_id<br />
AdGroupCrossDeviceStats_ customer_id<br />
HourlyAdGroupConversionStats_ customer_id<br />
HourlyAdGroupStats_ customer_id<br />
AdGroupConversionStats_ customer_id<br />
AdGroupCrossDeviceConversionStats_ customer_id<br />
AdGroup_ customer_id</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/adwords/api/docs/appendix/reports/age-range-performance-report">Age Range Performance Report</a></td>
<td>p_AgeRange_ customer_id<br />
p_AgeRangeBasicStats_ customer_id<br />
p_AgeRangeStats_ customer_id<br />
p_AgeRangeConversionStats_ customer_id<br />
p_AgeRangeNonClickStats_ customer_id</td>
<td>p_ads_AgeRange_ customer_id<br />
p_ads_AgeRangeBasicStats_ customer_id<br />
p_ads_AgeRangeStats_ customer_id<br />
p_ads_AgeRangeConversionStats_ customer_id<br />
p_ads_AgeRangeNonClickStats_ customer_id</td>
<td><a href="https://developers.google.com/google-ads/api/fields/v21/age_range_view">Age Range View</a></td>
<td>AgeRange_ customer_id<br />
AgeRangeBasicStats_ customer_id<br />
AgeRangeStats_ customer_id<br />
AgeRangeConversionStats_ customer_id<br />
AgeRangeNonClickStats_ customer_id</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/adwords/api/docs/appendix/reports/audience-performance-report">Audience Performance Report</a></td>
<td>p_Audience_ customer_id<br />
p_AudienceConversionStats_ customer_id<br />
p_AudienceNonClickStats_ customer_id<br />
p_AudienceBasicStats_ customer_id<br />
p_AudienceStats_ customer_id</td>
<td><code dir="ltr" translate="no">        NULL       </code><br />
<code dir="ltr" translate="no">        NULL       </code><br />
<code dir="ltr" translate="no">        NULL       </code><br />
<code dir="ltr" translate="no">        NULL       </code><br />
<code dir="ltr" translate="no">        NULL       </code></td>
<td><a href="https://developers.google.com/google-ads/api/fields/v21/ad_group_audience_view">Ad Group Audience View</a><br />
<a href="https://developers.google.com/google-ads/api/fields/v21/campaign_audience_view">Campaign Audience View</a></td>
<td>Audience_ customer_id<br />
AudienceConversionStats_ customer_id<br />
AudienceNonClickStats_ customer_id<br />
AudienceBasicStats_ customer_id<br />
AudienceStats_ customer_id</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/adwords/api/docs/appendix/reports/bid-goal-performance-report">Bid Goal Performance Report</a></td>
<td>p_BidGoal_ customer_id<br />
p_BidGoalStats_ customer_id<br />
p_HourlyBidGoalStats_ customer_id<br />
p_BidGoalConversionStats_ customer_id</td>
<td>p_ads_BidGoal_ customer_id<br />
p_ads_BidGoalStats_ customer_id<br />
p_ads_HourlyBidGoalStats_ customer_id<br />
p_ads_BidGoalConversionStats_ customer_id</td>
<td><a href="https://developers.google.com/google-ads/api/fields/v21/bidding_strategy">Bidding Strategy</a></td>
<td>BidGoal_ customer_id<br />
BidGoalStats_ customer_id<br />
HourlyBidGoalStats_ customer_id<br />
BidGoalConversionStats_ customer_id</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/adwords/api/docs/appendix/reports/budget-performance-report">Budget Performance Report</a></td>
<td>p_Budget_ customer_id<br />
p_BudgetStats_ customer_id</td>
<td>p_ads_Budget_ customer_id<br />
p_ads_BudgetStats_ customer_id</td>
<td><a href="https://developers.google.com/google-ads/api/fields/v21/campaign_budget">Campaign Budget</a></td>
<td>Budget_ customer_id<br />
BudgetStats_ customer_id</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/adwords/api/docs/appendix/reports/campaign-location-target-report">Campaign Location Target Report</a></td>
<td>p_CampaignLocationTargetStats_ customer_id<br />
p_LocationBasedCampaignCriterion_ customer_id</td>
<td>p_ads_CampaignLocationTargetStats_ customer_id<br />
p_ads_LocationBasedCampaignCriterion_ customer_id</td>
<td><a href="https://developers.google.com/google-ads/api/fields/v21/location_view">Location View</a></td>
<td>CampaignLocationTargetStats_ customer_id<br />
LocationBasedCampaignCriterion_ customer_id</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/adwords/api/docs/appendix/reports/campaign-performance-report">Campaign Performance Report</a></td>
<td>p_Campaign_ customer_id<br />
p_CampaignBasicStats_ customer_id<br />
p_CampaignConversionStats_ customer_id<br />
p_CampaignCrossDeviceStats_ customer_id<br />
p_HourlyCampaignConversionStats_ customer_id<br />
p_CampaignStats_ customer_id<br />
p_HourlyCampaignStats_ customer_id<br />
p_CampaignCrossDeviceConversionStats_ customer_id<br />
p_CampaignCookieStats_ customer_id</td>
<td>p_ads_Campaign_ customer_id<br />
p_ads_CampaignBasicStats_ customer_id<br />
p_ads_CampaignConversionStats_ customer_id<br />
p_ads_CampaignCrossDeviceStats_ customer_id<br />
p_ads_HourlyCampaignConversionStats_ customer_id<br />
p_ads_CampaignStats_ customer_id<br />
p_ads_HourlyCampaignStats_ customer_id<br />
p_ads_CampaignCrossDeviceConversionStats_ customer_id<br />
p_ads_CampaignCookieStats_ customer_id</td>
<td><a href="https://developers.google.com/google-ads/api/fields/v21/campaign">Campaign</a></td>
<td>Campaign_ customer_id<br />
CampaignBasicStats_ customer_id<br />
CampaignConversionStats_ customer_id<br />
CampaignCrossDeviceStats_ customer_id<br />
HourlyCampaignConversionStats_ customer_id<br />
CampaignStats_ customer_id<br />
HourlyCampaignStats_ customer_id<br />
CampaignCrossDeviceConversionStats_ customer_id<br />
CampaignCookieStats_ customer_id</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/adwords/api/docs/appendix/reports/click-performance-report">Click Performance Report</a></td>
<td>p_ClickStats_ customer_id</td>
<td>p_ads_ClickStats_ customer_id</td>
<td><a href="https://developers.google.com/google-ads/api/fields/v21/click_view">Click View</a></td>
<td>ClickStats_ customer_id</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/adwords/api/docs/appendix/reports/criteria-performance-report">Criteria Performance Report</a></td>
<td>p_Criteria_ customer_id<br />
p_CriteriaBasicStats_ customer_id<br />
p_CriteriaStats_ customer_id<br />
p_CriteriaConversionStats_ customer_id<br />
p_CriteriaNonClickStats_ customer_id</td>
<td><code dir="ltr" translate="no">        NULL       </code><br />
<code dir="ltr" translate="no">        NULL       </code><br />
<code dir="ltr" translate="no">        NULL       </code><br />
<code dir="ltr" translate="no">        NULL       </code><br />
<code dir="ltr" translate="no">        NULL       </code></td>
<td></td>
<td>Criteria_ customer_id<br />
CriteriaBasicStats_ customer_id<br />
CriteriaStats_ customer_id<br />
CriteriaConversionStats_ customer_id<br />
CriteriaNonClickStats_ customer_id</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/adwords/api/docs/appendix/reports/gender-performance-report">Gender Performance Report</a></td>
<td>p_Gender_ customer_id<br />
p_GenderBasicStats_ customer_id<br />
p_GenderStats_ customer_id<br />
p_GenderConversionStats_ customer_id<br />
p_GenderNonClickStats_ customer_id</td>
<td>p_ads_Gender_ customer_id<br />
p_ads_GenderBasicStats_ customer_id<br />
p_ads_GenderStats_ customer_id<br />
p_ads_GenderConversionStats_ customer_id<br />
p_ads_GenderNonClickStats_ customer_id</td>
<td><a href="https://developers.google.com/google-ads/api/fields/v21/gender_view">Gender View</a></td>
<td>Gender_ customer_id<br />
GenderBasicStats_ customer_id<br />
GenderStats_ customer_id<br />
GenderConversionStats_ customer_id<br />
GenderNonClickStats_ customer_id</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/adwords/api/docs/appendix/reports/geo-performance-report">Geo Performance Report</a></td>
<td>p_GeoConversionStats_ customer_id<br />
p_GeoStats_ customer_id</td>
<td>p_ads_GeoConversionStats_ customer_id<br />
p_ads_GeoStats_ customer_id</td>
<td><a href="https://developers.google.com/google-ads/api/fields/v21/geographic_view">Geographic View</a></td>
<td>GeoConversionStats_ customer_id<br />
GeoStats_ customer_id</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/adwords/api/docs/appendix/reports/keywords-performance-report">Keywords Performance Report</a></td>
<td>p_Keyword_ customer_id<br />
p_KeywordBasicStats_ customer_id<br />
p_KeywordCrossDeviceStats_ customer_id<br />
p_KeywordStats_ customer_id<br />
p_KeywordCrossDeviceConversionStats_ customer_id<br />
p_KeywordConversionStats_ customer_id</td>
<td>p_ads_Keyword_ customer_id<br />
p_ads_KeywordBasicStats_ customer_id<br />
p_ads_KeywordCrossDeviceStats_ customer_id<br />
p_ads_KeywordStats_ customer_id<br />
p_ads_KeywordCrossDeviceConversionStats_ customer_id<br />
p_ads_KeywordConversionStats_ customer_id</td>
<td><a href="https://developers.google.com/google-ads/api/fields/v21/keyword_view">Keyword View</a></td>
<td>Keyword_ customer_id<br />
KeywordBasicStats_ customer_id<br />
KeywordCrossDeviceStats_ customer_id<br />
KeywordStats_ customer_id<br />
KeywordCrossDeviceConversionStats_ customer_id<br />
KeywordConversionStats_ customer_id</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/adwords/api/docs/appendix/reports/paid-organic-query-report">Paid Organic Query Report</a></td>
<td>p_PaidOrganicStats_ customer_id</td>
<td>p_ads_PaidOrganicStats_ customer_id</td>
<td><a href="https://developers.google.com/google-ads/api/fields/v21/paid_organic_search_term_view">Paid Organic Search Term View</a></td>
<td>PaidOrganicStats_ customer_id</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/adwords/api/docs/appendix/reports/parental-status-performance-report">Parental Status Performance Report</a></td>
<td>p_ParentalStatus_ customer_id<br />
p_ParentalStatusBasicStats_ customer_id<br />
p_ParentalStatusStats_ customer_id<br />
p_ParentalStatusConversionStats_ customer_id<br />
p_ParentalStatusNonClickStats_ customer_id</td>
<td>p_ads_ParentalStatus_ customer_id<br />
p_ads_ParentalStatusBasicStats_ customer_id<br />
p_ads_ParentalStatusStats_ customer_id<br />
p_ads_ParentalStatusConversionStats_ customer_id<br />
p_ads_ParentalStatusNonClickStats_ customer_id</td>
<td><a href="https://developers.google.com/google-ads/api/fields/v21/parental_status_view">Parental Status View</a></td>
<td>ParentalStatus_ customer_id<br />
ParentalStatusBasicStats_ customer_id<br />
ParentalStatusStats_ customer_id<br />
ParentalStatusConversionStats_ customer_id<br />
ParentalStatusNonClickStats_ customer_id</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/adwords/api/docs/appendix/reports/placement-performance-report">Placement Performance Report</a></td>
<td>p_PlacementBasicStats_ customer_id<br />
p_PlacementNonClickStats_ customer_id<br />
p_PlacementStats_ customer_id<br />
p_Placement_ customer_id<br />
p_PlacementConversionStats_ customer_id</td>
<td>p_ads_PlacementBasicStats_ customer_id<br />
p_ads_PlacementNonClickStats_ customer_id<br />
p_ads_PlacementStats_ customer_id<br />
p_ads_Placement_ customer_id<br />
p_ads_PlacementConversionStats_ customer_id</td>
<td><a href="https://developers.google.com/google-ads/api/fields/v21/managed_placement_view">Managed Placement View</a></td>
<td>PlacementBasicStats_ customer_id<br />
PlacementNonClickStats_ customer_id<br />
PlacementStats_ customer_id<br />
Placement_ customer_id<br />
PlacementConversionStats_ customer_id</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/adwords/api/docs/appendix/reports/search-query-performance-report">Search Query Performance Report</a></td>
<td>p_SearchQueryStats_ customer_id<br />
p_SearchQueryConversionStats_ customer_id</td>
<td>p_ads_SearchQueryStats_ customer_id<br />
p_ads_SearchQueryConversionStats_ customer_id</td>
<td><a href="https://developers.google.com/google-ads/api/fields/v21/search_term_view">Search Term View</a></td>
<td>SearchQueryStats_ customer_id<br />
SearchQueryConversionStats_ customer_id</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/adwords/api/docs/appendix/reports/shopping-performance-report">Shopping Performance Report</a></td>
<td>p_ShoppingProductConversionStats_ customer_id<br />
p_ShoppingProductStats_ customer_id</td>
<td>p_ads_ShoppingProductConversionStats_ customer_id<br />
p_ads_ShoppingProductStats_ customer_id</td>
<td><a href="https://developers.google.com/google-ads/api/fields/v21/shopping_performance_view">Shopping Performance View</a></td>
<td>ShoppingProductConversionStats_ customer_id<br />
ShoppingProductStats_ customer_id</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/adwords/api/docs/appendix/reports/video-performance-report">Video Performance Report</a></td>
<td>p_VideoBasicStats_ customer_id<br />
p_VideoConversionStats_ customer_id<br />
p_VideoStats_ customer_id<br />
p_Video_ customer_id<br />
p_VideoNonClickStats_ customer_id</td>
<td>p_ads_VideoBasicStats_ customer_id<br />
p_ads_VideoConversionStats_ customer_id<br />
p_ads_VideoStats_ customer_id<br />
p_ads_Video_ customer_id<br />
p_ads_VideoNonClickStats_ customer_id</td>
<td><a href="https://developers.google.com/google-ads/api/fields/v21/video">Video</a></td>
<td>VideoBasicStats_ customer_id<br />
VideoConversionStats_ customer_id<br />
VideoStats_ customer_id<br />
Video_ customer_id<br />
VideoNonClickStats_ customer_id</td>
</tr>
<tr class="odd">
<td></td>
<td></td>
<td>AdGroupBidModifier</td>
<td><a href="https://developers.google.com/google-ads/api/fields/v21/ad_group_bid_modifier">Ad Group Bid Modifier</a></td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td></td>
<td>AdGroupAdLabel</td>
<td><a href="https://developers.google.com/google-ads/api/fields/v21/ad_group_ad_label">Ad Group Ad Label</a></td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td></td>
<td>CampaignLabel</td>
<td><a href="https://developers.google.com/google-ads/api/fields/v21/campaign_label">Campaign Label</a></td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td></td>
<td>CampaignCriterion</td>
<td><a href="https://developers.google.com/google-ads/api/fields/v21/campaign_criterion">Campaign Criterion</a></td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td></td>
<td>AdGroupLabel</td>
<td><a href="https://developers.google.com/google-ads/api/fields/v21/ad_group_label">Ad Group Label</a></td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td></td>
<td>AdGroupAudience<br />
AdGroupAudienceStats<br />
AdGroupAudienceConversionStats<br />
AdGroupAudienceNonClickStats<br />
AdGroupAudienceBasicStats</td>
<td><a href="https://developers.google.com/google-ads/api/fields/v21/ad_group_audience_view">Ad Group Audience View</a></td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td></td>
<td>Assets (available if <a href="https://developers.google.com/google-ads/api/docs/performance-max/overview">Pmax</a> data is enabled)</td>
<td><a href="https://developers.google.com/google-ads/api/fields/v21/asset">Assets</a></td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td></td>
<td>AssetGroup (available if <a href="https://developers.google.com/google-ads/api/docs/performance-max/overview">Pmax</a> data is enabled)</td>
<td><a href="https://developers.google.com/google-ads/api/fields/v21/asset_group">Asset Groups</a></td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td></td>
<td>AssetGroupAsset (available if <a href="https://developers.google.com/google-ads/api/docs/performance-max/overview">Pmax</a> data is enabled)</td>
<td><a href="https://developers.google.com/google-ads/api/fields/v21/asset_group_asset">Asset Group Assets</a></td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td></td>
<td>AssetGroupSignal (available if <a href="https://developers.google.com/google-ads/api/docs/performance-max/overview">Pmax</a> data is enabled)</td>
<td><a href="https://developers.google.com/google-ads/api/fields/v21/asset_group_signal">Asset Group Signal</a></td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td></td>
<td>AssetGroupProductGroupStats (available if <a href="https://developers.google.com/google-ads/api/docs/performance-max/overview">Pmax</a> data is enabled)</td>
<td><a href="https://developers.google.com/google-ads/api/fields/v21/asset_group_product_group_view">AssetGroupProductGroupStats</a></td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td></td>
<td>CampaignAssetStats (available if <a href="https://developers.google.com/google-ads/api/docs/performance-max/overview">Pmax</a> data is enabled)</td>
<td><a href="https://developers.google.com/google-ads/api/fields/v21/campaign_asset">CampaignAssetStats</a></td>
<td></td>
</tr>
</tbody>
</table>

## Column mapping for Google Ads reports

The BigQuery tables created by a Google Ads transfer consist of the following columns (fields):

Google Ads Table Name: AccountBasicStats

Google Ads API Resource: [customer](https://developers.google.com/google-ads/api/fields/v21/customer)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="even">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
<td>Clicks</td>
</tr>
<tr class="odd">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>Conversions</td>
</tr>
<tr class="even">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="odd">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
<td>Cost</td>
</tr>
<tr class="even">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
<td>Impressions</td>
</tr>
<tr class="odd">
<td>metrics_interaction_event_types</td>
<td>The types of payable and free interactions.</td>
<td>InteractionTypes</td>
</tr>
<tr class="even">
<td>metrics_interactions</td>
<td>The number of interactions. An interaction is the main user action associated with an ad format, such as clicks for text and shopping ads or views for video ads.</td>
<td>Interactions</td>
</tr>
<tr class="odd">
<td>metrics_view_through_conversions</td>
<td>The total number of view-through conversions. These happen when a customer sees an image or rich media ad, then later completes a conversion on your site without interacting with (for example, clicking on) another ad.</td>
<td>ViewThroughConversions</td>
</tr>
<tr class="even">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="even">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
<tr class="odd">
<td>segments_slot</td>
<td>Position of the ad.</td>
<td>Slot</td>
</tr>
</tbody>
</table>

Google Ads Table Name: AccountConversionStats

Google Ads API Resource: [customer](https://developers.google.com/google-ads/api/fields/v21/customer)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="even">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>Conversions</td>
</tr>
<tr class="odd">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="even">
<td>metrics_value_per_conversion</td>
<td>The value of conversions divided by the number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ValuePerConversion</td>
</tr>
<tr class="odd">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="even">
<td>segments_click_type</td>
<td>Click type.</td>
<td>ClickType</td>
</tr>
<tr class="odd">
<td>segments_conversion_action</td>
<td>Resource name of the conversion action.</td>
<td>ConversionTrackerId</td>
</tr>
<tr class="even">
<td>segments_conversion_action_category</td>
<td>Conversion action category.</td>
<td>ConversionCategoryName</td>
</tr>
<tr class="odd">
<td>segments_conversion_action_name</td>
<td>Conversion action name.</td>
<td>ConversionTypeName</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="odd">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="even">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
<tr class="odd">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="even">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="odd">
<td>segments_slot</td>
<td>Position of the ad.</td>
<td>Slot</td>
</tr>
<tr class="even">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="odd">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: AccountNonClickStats

Google Ads API Resource: [customer](https://developers.google.com/google-ads/api/fields/v21/customer)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="even">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>AllConversions</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions_from_interactions_rate</td>
<td>All conversions from interactions (as oppose to view through conversions) divided by the number of ad interactions.</td>
<td>AllConversionRate</td>
</tr>
<tr class="even">
<td>metrics_all_conversions_value</td>
<td>The total value of all conversions.</td>
<td>AllConversionValue</td>
</tr>
<tr class="odd">
<td>metrics_average_cpe</td>
<td>The average amount that you've been charged for an ad engagement. This amount is the total cost of all ad engagements divided by the total number of ad engagements.</td>
<td>AverageCpe</td>
</tr>
<tr class="even">
<td>metrics_average_cpv</td>
<td>The average amount you pay each time someone views your ad. The average CPV is defined by the total cost of all ad views divided by the number of views.</td>
<td>AverageCpv</td>
</tr>
<tr class="odd">
<td>metrics_content_budget_lost_impression_share</td>
<td>The estimated percent of times that your ad was eligible to show on the Display Network but didn't because your budget was too low. Note: Content budget lost impression share is reported in the range of 0 to 0.9. Any value above 0.9 is reported as 0.9001.</td>
<td>ContentBudgetLostImpressionShare</td>
</tr>
<tr class="even">
<td>metrics_content_impression_share</td>
<td>The impressions you've received on the Display Network divided by the estimated number of impressions you were eligible to receive. Note: Content impression share is reported in the range of 0.1 to 1. Any value below 0.1 is reported as 0.0999.</td>
<td>ContentImpressionShare</td>
</tr>
<tr class="odd">
<td>metrics_content_rank_lost_impression_share</td>
<td>The estimated percentage of impressions on the Display Network that your ads didn't receive due to poor Ad Rank. Note: Content rank lost impression share is reported in the range of 0 to 0.9. Any value above 0.9 is reported as 0.9001.</td>
<td>ContentRankLostImpressionShare</td>
</tr>
<tr class="even">
<td>metrics_cost_per_all_conversions</td>
<td>The cost of ad interactions divided by all conversions.</td>
<td>CostPerAllConversion</td>
</tr>
<tr class="odd">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on a Google Ads ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
<td>CrossDeviceConversions</td>
</tr>
<tr class="even">
<td>metrics_engagement_rate</td>
<td>How often people engage with your ad after it's shown to them. This is the number of ad expansions divided by the number of times your ad is shown.</td>
<td>EngagementRate</td>
</tr>
<tr class="odd">
<td>metrics_engagements</td>
<td>The number of engagements. An engagement occurs when a viewer expands your Lightbox ad. Also, in the future, other ad types may support engagement metrics.</td>
<td>Engagements</td>
</tr>
<tr class="even">
<td>metrics_invalid_click_rate</td>
<td>The percentage of clicks filtered out of your total number of clicks (filtered + non-filtered clicks) during the reporting period.</td>
<td>InvalidClickRate</td>
</tr>
<tr class="odd">
<td>metrics_invalid_clicks</td>
<td>Number of clicks Google considers illegitimate and doesn't charge you for.</td>
<td>InvalidClicks</td>
</tr>
<tr class="even">
<td>metrics_search_budget_lost_impression_share</td>
<td>The estimated percent of times that your ad was eligible to show on the Search Network but didn't because your budget was too low. Note: Search budget lost impression share is reported in the range of 0 to 0.9. Any value above 0.9 is reported as 0.9001.</td>
<td>SearchBudgetLostImpressionShare</td>
</tr>
<tr class="odd">
<td>metrics_search_exact_match_impression_share</td>
<td>The impressions you've received divided by the estimated number of impressions you were eligible to receive on the Search Network for search terms that matched your keywords exactly (or were close variants of your keyword), regardless of your keyword match types. Note: Search exact match impression share is reported in the range of 0.1 to 1. Any value below 0.1 is reported as 0.0999.</td>
<td>SearchExactMatchImpressionShare</td>
</tr>
<tr class="even">
<td>metrics_search_impression_share</td>
<td>The impressions you've received on the Search Network divided by the estimated number of impressions you were eligible to receive. Note: Search impression share is reported in the range of 0.1 to 1. Any value below 0.1 is reported as 0.0999.</td>
<td>SearchImpressionShare</td>
</tr>
<tr class="odd">
<td>metrics_search_rank_lost_impression_share</td>
<td>The estimated percentage of impressions on the Search Network that your ads didn't receive due to poor Ad Rank. Note: Search rank lost impression share is reported in the range of 0 to 0.9. Any value above 0.9 is reported as 0.9001.</td>
<td>SearchRankLostImpressionShare</td>
</tr>
<tr class="even">
<td>metrics_value_per_all_conversions</td>
<td>The value of all conversions divided by the number of all conversions.</td>
<td>ValuePerAllConversion</td>
</tr>
<tr class="odd">
<td>metrics_video_view_rate</td>
<td>The number of views your TrueView video ad receives divided by its number of impressions, including thumbnail impressions for TrueView in-display ads.</td>
<td>VideoViewRate</td>
</tr>
<tr class="even">
<td>metrics_video_views</td>
<td>The number of times your video ads were viewed.</td>
<td>VideoViews</td>
</tr>
<tr class="odd">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="odd">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="even">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="odd">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="even">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="odd">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: AccountStats

Google Ads API Resource: [customer](https://developers.google.com/google-ads/api/fields/v21/customer)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="even">
<td>metrics_active_view_cpm</td>
<td>Average cost of viewable impressions (`active_view_impressions`).</td>
<td>ActiveViewCpm</td>
</tr>
<tr class="odd">
<td>metrics_active_view_ctr</td>
<td>Active view measurable clicks divided by active view viewable impressions. This metric is reported only for display network.</td>
<td>ActiveViewCtr</td>
</tr>
<tr class="even">
<td>metrics_active_view_impressions</td>
<td>A measurement of how often your ad has become viewable on a Display Network site.</td>
<td>ActiveViewImpressions</td>
</tr>
<tr class="odd">
<td>metrics_active_view_measurability</td>
<td>The ratio of impressions that could be measured by Active View over the number of served impressions.</td>
<td>ActiveViewMeasurability</td>
</tr>
<tr class="even">
<td>metrics_active_view_measurable_cost_micros</td>
<td>The cost of the impressions you received that were measurable by Active View.</td>
<td>ActiveViewMeasurableCost</td>
</tr>
<tr class="odd">
<td>metrics_active_view_measurable_impressions</td>
<td>The number of times your ads are appearing on placements in positions where they can be seen.</td>
<td>ActiveViewMeasurableImpressions</td>
</tr>
<tr class="even">
<td>metrics_active_view_viewability</td>
<td>The percentage of time when your ad appeared on an Active View enabled site (measurable impressions) and was viewable (viewable impressions).</td>
<td>ActiveViewViewability</td>
</tr>
<tr class="odd">
<td>metrics_average_cost</td>
<td>The average amount you pay per interaction. This amount is the total cost of your ads divided by the total number of interactions.</td>
<td>AverageCost</td>
</tr>
<tr class="even">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
<td>AverageCpc</td>
</tr>
<tr class="odd">
<td>metrics_average_cpm</td>
<td>Average cost-per-thousand impressions (CPM).</td>
<td>AverageCpm</td>
</tr>
<tr class="even">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
<td>Clicks</td>
</tr>
<tr class="odd">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>Conversions</td>
</tr>
<tr class="even">
<td>metrics_conversions_from_interactions_rate</td>
<td>Conversions from interactions divided by the number of ad interactions (such as clicks for text ads or views for video ads). This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionRate</td>
</tr>
<tr class="odd">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="even">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
<td>Cost</td>
</tr>
<tr class="odd">
<td>metrics_cost_per_conversion</td>
<td>The cost of ad interactions divided by conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>CostPerConversion</td>
</tr>
<tr class="even">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
<td>Ctr</td>
</tr>
<tr class="odd">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
<td>Impressions</td>
</tr>
<tr class="even">
<td>metrics_interaction_event_types</td>
<td>The types of payable and free interactions.</td>
<td>InteractionTypes</td>
</tr>
<tr class="odd">
<td>metrics_interaction_rate</td>
<td>How often people interact with your ad after it is shown to them. This is the number of interactions divided by the number of times your ad is shown.</td>
<td>InteractionRate</td>
</tr>
<tr class="even">
<td>metrics_interactions</td>
<td>The number of interactions. An interaction is the main user action associated with an ad format, such as clicks for text and shopping ads or views for video ads.</td>
<td>Interactions</td>
</tr>
<tr class="odd">
<td>metrics_value_per_conversion</td>
<td>The value of conversions divided by the number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ValuePerConversion</td>
</tr>
<tr class="even">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="odd">
<td>segments_click_type</td>
<td>Click type.</td>
<td>ClickType</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="odd">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="even">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
<tr class="odd">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="even">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="odd">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="even">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: Ad

Google Ads API Resource: [ad\_group\_ad](https://developers.google.com/google-ads/api/fields/v21/ad_group_ad)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_ad_ad_added_by_google_ads</td>
<td>Indicates if this ad was automatically added by Google Ads and not by a user. For example, this could happen when ads are automatically created as suggestions for new ads based on knowledge of how existing ads are performing.</td>
<td>Automated</td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_app_ad_descriptions</td>
<td>List of text assets for descriptions. When the ad serves the descriptions, they are selected from this list.</td>
<td>UniversalAppAdDescriptions</td>
</tr>
<tr class="odd">
<td>ad_group_ad_ad_app_ad_headlines</td>
<td>List of text assets for headlines. When the ad serves the headlines is selected from this list.</td>
<td>UniversalAppAdHeadlines</td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_app_ad_html5_media_bundles</td>
<td>List of media bundle assets that may be used with the ad.</td>
<td>UniversalAppAdHtml5MediaBundles</td>
</tr>
<tr class="odd">
<td>ad_group_ad_ad_app_ad_images</td>
<td>List of image assets that may be displayed with the ad.</td>
<td>UniversalAppAdImages</td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_app_ad_mandatory_ad_text</td>
<td>An optional text asset that, if specified, must always be displayed when the ad is served.</td>
<td>UniversalAppAdMandatoryAdText</td>
</tr>
<tr class="odd">
<td>ad_group_ad_ad_app_ad_youtube_videos</td>
<td>List of YouTube video assets that may be displayed with the ad.</td>
<td>UniversalAppAdYouTubeVideos</td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_call_ad_phone_number</td>
<td>The phone number in the ad.</td>
<td>CallOnlyPhoneNumber</td>
</tr>
<tr class="odd">
<td>ad_group_ad_ad_device_preference</td>
<td>The device preference for the ad. You can only specify a preference for mobile devices. When this preference is set, the ad is preferred over other ads when being displayed on a mobile device. The ad can still be displayed on other device types. For example, if no other ads are available. If unspecified (no device preference), all devices are targeted. This is only supported by some ad types.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_display_url</td>
<td>The URL that appears in the ad description for some ad formats.</td>
<td>DisplayUrl</td>
</tr>
<tr class="odd">
<td>ad_group_ad_ad_expanded_dynamic_search_ad_description</td>
<td>The description of the ad.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_expanded_dynamic_search_ad_description2</td>
<td>The second description of the ad.</td>
<td>ExpandedDynamicSearchCreativeDescription2</td>
</tr>
<tr class="odd">
<td>ad_group_ad_ad_expanded_text_ad_description</td>
<td>The description of the ad.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_expanded_text_ad_description2</td>
<td>The second description of the ad.</td>
<td>ExpandedTextAdDescription2</td>
</tr>
<tr class="odd">
<td>ad_group_ad_ad_expanded_text_ad_headline_part1</td>
<td>The first part of the ad's headline.</td>
<td>HeadlinePart1</td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_expanded_text_ad_headline_part2</td>
<td>The second part of the ad's headline.</td>
<td>HeadlinePart2</td>
</tr>
<tr class="odd">
<td>ad_group_ad_ad_expanded_text_ad_headline_part3</td>
<td>The third part of the ad's headline.</td>
<td>ExpandedTextAdHeadlinePart3</td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_expanded_text_ad_path1</td>
<td>The text that can appear alongside the ad's displayed URL.</td>
<td>Path1</td>
</tr>
<tr class="odd">
<td>ad_group_ad_ad_expanded_text_ad_path2</td>
<td>Additional text that can appear alongside the ad's displayed URL.</td>
<td>Path2</td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_final_app_urls</td>
<td>A list of final app URLs that are used on mobile if the user has the specific app installed.</td>
<td>CreativeFinalAppUrls</td>
</tr>
<tr class="odd">
<td>ad_group_ad_ad_final_mobile_urls</td>
<td>The list of possible final mobile URLs after all cross-domain redirects for the ad.</td>
<td>CreativeFinalMobileUrls</td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_final_urls</td>
<td>The list of possible final URLs after all cross-domain redirects for the ad.</td>
<td>CreativeFinalUrls</td>
</tr>
<tr class="odd">
<td>ad_group_ad_ad_group</td>
<td>The ad group to which the ad belongs.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_id</td>
<td>The ID of the ad.</td>
<td>CreativeId</td>
</tr>
<tr class="odd">
<td>ad_group_ad_ad_image_ad_image_url</td>
<td>URL of the full size image.</td>
<td>ImageAdUrl</td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_image_ad_mime_type</td>
<td>The mime type of the image.</td>
<td>ImageCreativeMimeType</td>
</tr>
<tr class="odd">
<td>ad_group_ad_ad_image_ad_name</td>
<td>The name of the image. If the image was created from a MediaFile, this is the MediaFile's name. If the image was created from bytes, this is empty.</td>
<td>ImageCreativeName</td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_image_ad_pixel_height</td>
<td>Height in pixels of the full size image.</td>
<td>ImageCreativeImageHeight</td>
</tr>
<tr class="odd">
<td>ad_group_ad_ad_image_ad_pixel_width</td>
<td>Width in pixels of the full size image.</td>
<td>ImageCreativeImageWidth</td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_legacy_responsive_display_ad_accent_color</td>
<td>The accent color of the ad in hexadecimal. For example, #ffffff for white. If one of main_color and accent_color is set, the other is required as well.</td>
<td>AccentColor</td>
</tr>
<tr class="odd">
<td>ad_group_ad_ad_legacy_responsive_display_ad_allow_flexible_color</td>
<td>Advertiser's consent to allow flexible color. When true, the ad may be served with different colors if necessary. When false, the ad is served with the specified colors or a neutral color. The default value is true. Must be true if main_color and accent_color are not set.</td>
<td>AllowFlexibleColor</td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_legacy_responsive_display_ad_business_name</td>
<td>The business name in the ad.</td>
<td>BusinessName</td>
</tr>
<tr class="odd">
<td>ad_group_ad_ad_legacy_responsive_display_ad_call_to_action_text</td>
<td>The call-to-action text for the ad.</td>
<td>CallToActionText</td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_legacy_responsive_display_ad_description</td>
<td>The description of the ad.</td>
<td>Description</td>
</tr>
<tr class="odd">
<td>ad_group_ad_ad_legacy_responsive_display_ad_format_setting</td>
<td>Specifies which format the ad is served in. Default is ALL_FORMATS.</td>
<td>FormatSetting</td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_legacy_responsive_display_ad_logo_image</td>
<td>The MediaFile resource name of the logo image used in the ad.</td>
<td>EnhancedDisplayCreativeLandscapeLogoImageMediaId</td>
</tr>
<tr class="odd">
<td>ad_group_ad_ad_legacy_responsive_display_ad_long_headline</td>
<td>The long version of the ad's headline.</td>
<td>LongHeadline</td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_legacy_responsive_display_ad_main_color</td>
<td>The main color of the ad in hexadecimal. For example, #ffffff for white. If one of main_color and accent_color is set, the other is required as well.</td>
<td>MainColor</td>
</tr>
<tr class="odd">
<td>ad_group_ad_ad_legacy_responsive_display_ad_marketing_image</td>
<td>The MediaFile resource name of the marketing image used in the ad.</td>
<td>EnhancedDisplayCreativeMarketingImageMediaId</td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_legacy_responsive_display_ad_price_prefix</td>
<td>Prefix before price. For example, 'as low as'.</td>
<td>PricePrefix</td>
</tr>
<tr class="odd">
<td>ad_group_ad_ad_legacy_responsive_display_ad_promo_text</td>
<td>Promotion text used for dynamic formats of responsive ads. For example 'Free two-day shipping'.</td>
<td>PromoText</td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_legacy_responsive_display_ad_short_headline</td>
<td>The short version of the ad's headline.</td>
<td>ShortHeadline</td>
</tr>
<tr class="odd">
<td>ad_group_ad_ad_legacy_responsive_display_ad_square_logo_image</td>
<td>The MediaFile resource name of the square logo image used in the ad.</td>
<td>EnhancedDisplayCreativeLogoImageMediaId</td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_legacy_responsive_display_ad_square_marketing_image</td>
<td>The MediaFile resource name of the square marketing image used in the ad.</td>
<td>EnhancedDisplayCreativeMarketingImageSquareMediaId</td>
</tr>
<tr class="odd">
<td>ad_group_ad_ad_responsive_display_ad_accent_color</td>
<td>The accent color of the ad in hexadecimal. For example, #ffffff for white. If one of main_color and accent_color is set, the other is required as well.</td>
<td>MultiAssetResponsiveDisplayAdAccentColor</td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_responsive_display_ad_business_name</td>
<td>The advertiser or brand name. Maximum display width is 25.</td>
<td>MultiAssetResponsiveDisplayAdBusinessName</td>
</tr>
<tr class="odd">
<td>ad_group_ad_ad_responsive_display_ad_call_to_action_text</td>
<td>The call-to-action text for the ad. Maximum display width is 30.</td>
<td>MultiAssetResponsiveDisplayAdCallToActionText</td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_responsive_display_ad_descriptions</td>
<td>Descriptive texts for the ad. The maximum length is 90 characters. At least 1 and max 5 headlines can be specified.</td>
<td>MultiAssetResponsiveDisplayAdDescriptions</td>
</tr>
<tr class="odd">
<td>ad_group_ad_ad_responsive_display_ad_format_setting</td>
<td>Specifies which format the ad is served in. Default is ALL_FORMATS.</td>
<td>MultiAssetResponsiveDisplayAdFormatSetting</td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_responsive_display_ad_headlines</td>
<td>Short format headlines for the ad. The maximum length is 30 characters. At least 1 and max 5 headlines can be specified.</td>
<td>MultiAssetResponsiveDisplayAdHeadlines</td>
</tr>
<tr class="odd">
<td>ad_group_ad_ad_responsive_display_ad_logo_images</td>
<td>Logo images to be used in the ad. Valid image types are GIF, JPEG, and PNG. The minimum size is 512x128 and the aspect ratio must be 4:1 (+-1%). Combined with square_logo_images the maximum is 5.</td>
<td>MultiAssetResponsiveDisplayAdLandscapeLogoImages</td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_responsive_display_ad_long_headline</td>
<td>A required long format headline. The maximum length is 90 characters.</td>
<td>MultiAssetResponsiveDisplayAdLongHeadline</td>
</tr>
<tr class="odd">
<td>ad_group_ad_ad_responsive_display_ad_main_color</td>
<td>The main color of the ad in hexadecimal. For example, #ffffff for white. If one of main_color and accent_color is set, the other is required as well.</td>
<td>MultiAssetResponsiveDisplayAdMainColor</td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_responsive_display_ad_marketing_images</td>
<td>Marketing images to be used in the ad. Valid image types are GIF, JPEG, and PNG. The minimum size is 600x314 and the aspect ratio must be 1.91:1 (+-1%). At least one marketing_image is required. Combined with square_marketing_images the maximum is 15.</td>
<td>MultiAssetResponsiveDisplayAdMarketingImages</td>
</tr>
<tr class="odd">
<td>ad_group_ad_ad_responsive_display_ad_price_prefix</td>
<td>Prefix before price. For example, 'as low as'.</td>
<td>MultiAssetResponsiveDisplayAdDynamicSettingsPricePrefix</td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_responsive_display_ad_promo_text</td>
<td>Promotion text used for dynamic formats of responsive ads. For example 'Free two-day shipping'.</td>
<td>MultiAssetResponsiveDisplayAdDynamicSettingsPromoText</td>
</tr>
<tr class="odd">
<td>ad_group_ad_ad_responsive_display_ad_square_logo_images</td>
<td>Square logo images to be used in the ad. Valid image types are GIF, JPEG, and PNG. The minimum size is 128x128 and the aspect ratio must be 1:1 (+-1%). Combined with square_logo_images the maximum is 5.</td>
<td>MultiAssetResponsiveDisplayAdLogoImages</td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_responsive_display_ad_square_marketing_images</td>
<td>Square marketing images to be used in the ad. Valid image types are GIF, JPEG, and PNG. The minimum size is 300x300 and the aspect ratio must be 1:1 (+-1%). At least one square marketing_image is required. Combined with marketing_images the maximum is 15.</td>
<td>MultiAssetResponsiveDisplayAdSquareMarketingImages</td>
</tr>
<tr class="odd">
<td>ad_group_ad_ad_responsive_display_ad_youtube_videos</td>
<td>Optional YouTube videos for the ad. A maximum of 5 videos can be specified.</td>
<td>MultiAssetResponsiveDisplayAdYouTubeVideos</td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_responsive_search_ad_descriptions</td>
<td>List of text assets for descriptions. When the ad serves the descriptions, they are selected from this list.</td>
<td>ResponsiveSearchAdDescriptions</td>
</tr>
<tr class="odd">
<td>ad_group_ad_ad_responsive_search_ad_headlines</td>
<td>List of text assets for headlines. When the ad serves the headlines, they are selected from this list.</td>
<td>ResponsiveSearchAdHeadlines</td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_responsive_search_ad_path1</td>
<td>First part of text that may appear appended to the url displayed in the ad.</td>
<td>ResponsiveSearchAdPath1</td>
</tr>
<tr class="odd">
<td>ad_group_ad_ad_responsive_search_ad_path2</td>
<td>Second part of text that may appear appended to the url displayed in the ad. This field can only be set when path1 is also set.</td>
<td>ResponsiveSearchAdPath2</td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_strength</td>
<td>Overall ad strength for this ad group ad.</td>
<td>AdStrengthInfo</td>
</tr>
<tr class="odd">
<td>ad_group_ad_ad_system_managed_resource_source</td>
<td>If this ad is system managed, then this field indicates the source. This field is read-only.</td>
<td>SystemManagedEntitySource</td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_text_ad_description1</td>
<td>The first line of the ad's description.</td>
<td>Description1</td>
</tr>
<tr class="odd">
<td>ad_group_ad_ad_text_ad_description2</td>
<td>The second line of the ad's description.</td>
<td>Description2</td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_text_ad_headline</td>
<td>The headline of the ad.</td>
<td>Headline</td>
</tr>
<tr class="odd">
<td>ad_group_ad_ad_tracking_url_template</td>
<td>The URL template for constructing a tracking URL.</td>
<td>CreativeTrackingUrlTemplate</td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_type</td>
<td>The type of ad.</td>
<td>AdType</td>
</tr>
<tr class="odd">
<td>ad_group_ad_ad_url_custom_parameters</td>
<td>The list of mappings that can be used to substitute custom parameter tags in a `tracking_url_template`, `final_urls`, or `mobile_final_urls`. For mutates, please use url custom parameter operations.</td>
<td>CreativeUrlCustomParameters</td>
</tr>
<tr class="even">
<td>ad_group_ad_status</td>
<td>The status of the ad.</td>
<td>Status</td>
</tr>
<tr class="odd">
<td>ad_group_id</td>
<td>Output only. The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
</tbody>
</table>

Google Ads Table Name: AdBasicStats

Google Ads API Resource: [ad\_group\_ad](https://developers.google.com/google-ads/api/fields/v21/ad_group_ad)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_ad_ad_group</td>
<td>The ad group to which the ad belongs.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_id</td>
<td>The ID of the ad.</td>
<td>CreativeId</td>
</tr>
<tr class="odd">
<td>ad_group_base_ad_group</td>
<td>For draft or experiment ad groups, this field is the resource name of the base ad group from which this ad group was created. If a draft or experiment ad group does not have a base ad group, then this field is null. For base ad groups, this field equals the ad group resource name. This field is read-only.</td>
<td>BaseAdGroupId</td>
</tr>
<tr class="even">
<td>ad_group_id</td>
<td>Output only. The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="odd">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td>BaseCampaignId</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="even">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
<td>Clicks</td>
</tr>
<tr class="odd">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>Conversions</td>
</tr>
<tr class="even">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="odd">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
<td>Cost</td>
</tr>
<tr class="even">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
<td>Impressions</td>
</tr>
<tr class="odd">
<td>metrics_interaction_event_types</td>
<td>The types of payable and free interactions.</td>
<td>InteractionTypes</td>
</tr>
<tr class="even">
<td>metrics_interactions</td>
<td>The number of interactions. An interaction is the main user action associated with an ad format, such as clicks for text and shopping ads or views for video ads.</td>
<td>Interactions</td>
</tr>
<tr class="odd">
<td>metrics_view_through_conversions</td>
<td>The total number of view-through conversions. These happen when a customer sees an image or rich media ad, then later completes a conversion on your site without interacting with (for example, clicking on) another ad.</td>
<td>ViewThroughConversions</td>
</tr>
<tr class="even">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="even">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
<tr class="odd">
<td>segments_slot</td>
<td>Position of the ad.</td>
<td>Slot</td>
</tr>
</tbody>
</table>

Google Ads Table Name: AdConversionStats

Google Ads API Resource: [ad\_group\_ad](https://developers.google.com/google-ads/api/fields/v21/ad_group_ad)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_ad_ad_group</td>
<td>The ad group to which the ad belongs.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_id</td>
<td>The ID of the ad.</td>
<td>CreativeId</td>
</tr>
<tr class="odd">
<td>ad_group_base_ad_group</td>
<td>For draft or experiment ad groups, this field is the resource name of the base ad group from which this ad group was created. If a draft or experiment ad group doesn't have a base ad group, then this field is null. For base ad groups, this field equals the ad group resource name. This field is read-only.</td>
<td>BaseAdGroupId</td>
</tr>
<tr class="even">
<td>ad_group_id</td>
<td>Output only. The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="odd">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td>BaseCampaignId</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="even">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>Conversions</td>
</tr>
<tr class="odd">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="even">
<td>metrics_value_per_conversion</td>
<td>The value of conversions divided by the number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ValuePerConversion</td>
</tr>
<tr class="odd">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="even">
<td>segments_click_type</td>
<td>Click type.</td>
<td>ClickType</td>
</tr>
<tr class="odd">
<td>segments_conversion_action</td>
<td>Resource name of the conversion action.</td>
<td>ConversionTrackerId</td>
</tr>
<tr class="even">
<td>segments_conversion_action_category</td>
<td>Conversion action category.</td>
<td>ConversionCategoryName</td>
</tr>
<tr class="odd">
<td>segments_conversion_action_name</td>
<td>Conversion action name.</td>
<td>ConversionTypeName</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="odd">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="even">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
<tr class="odd">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="even">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="odd">
<td>segments_slot</td>
<td>Position of the ad.</td>
<td>Slot</td>
</tr>
<tr class="even">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="odd">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: AdCrossDeviceConversionStats

Google Ads API Resource: [ad\_group\_ad](https://developers.google.com/google-ads/api/fields/v21/ad_group_ad)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_ad_ad_group</td>
<td>The ad group to which the ad belongs.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_id</td>
<td>The ID of the ad.</td>
<td>CreativeId</td>
</tr>
<tr class="odd">
<td>ad_group_base_ad_group</td>
<td>For draft or experiment ad groups, this field is the resource name of the base ad group from which this ad group was created. If a draft or experiment ad group does not have a base ad group, then this field is null. For base ad groups, this field equals the ad group resource name. This field is read-only.</td>
<td>BaseAdGroupId</td>
</tr>
<tr class="even">
<td>ad_group_id</td>
<td>Output only. The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="odd">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td>BaseCampaignId</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="even">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>AllConversions</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions_value</td>
<td>The total value of all conversions.</td>
<td>AllConversionValue</td>
</tr>
<tr class="even">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on a Google Ads ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
<td>CrossDeviceConversions</td>
</tr>
<tr class="odd">
<td>metrics_value_per_all_conversions</td>
<td>The value of all conversions divided by the number of all conversions.</td>
<td>ValuePerAllConversion</td>
</tr>
<tr class="even">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="odd">
<td>segments_conversion_action</td>
<td>Resource name of the conversion action.</td>
<td>ConversionTrackerId</td>
</tr>
<tr class="even">
<td>segments_conversion_action_category</td>
<td>Conversion action category.</td>
<td>ConversionCategoryName</td>
</tr>
<tr class="odd">
<td>segments_conversion_action_name</td>
<td>Conversion action name.</td>
<td>ConversionTypeName</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="odd">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="even">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="odd">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="even">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="odd">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: AdCrossDeviceStats

Google Ads API Resource: [ad\_group\_ad](https://developers.google.com/google-ads/api/fields/v21/ad_group_ad)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_ad_ad_group</td>
<td>The ad group to which the ad belongs.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_id</td>
<td>The ID of the ad.</td>
<td>CreativeId</td>
</tr>
<tr class="odd">
<td>ad_group_base_ad_group</td>
<td>For draft or experiment ad groups, this field is the resource name of the base ad group from which this ad group was created. If a draft or experiment ad group does not have a base ad group, then this field is null. For base ad groups, this field equals the ad group resource name. This field is read-only.</td>
<td>BaseAdGroupId</td>
</tr>
<tr class="even">
<td>ad_group_id</td>
<td>Output only. The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="odd">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td>BaseCampaignId</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="even">
<td>metrics_absolute_top_impression_percentage</td>
<td>The percent of your ad impressions that are shown as the very first ad above the organic search results.</td>
<td>AbsoluteTopImpressionPercentage</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>AllConversions</td>
</tr>
<tr class="even">
<td>metrics_all_conversions_from_interactions_rate</td>
<td>All conversions from interactions (as oppose to view through conversions) divided by the number of ad interactions.</td>
<td>AllConversionRate</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions_value</td>
<td>The total value of all conversions.</td>
<td>AllConversionValue</td>
</tr>
<tr class="even">
<td>metrics_average_cpe</td>
<td>The average amount that you've been charged for an ad engagement. This amount is the total cost of all ad engagements divided by the total number of ad engagements.</td>
<td>AverageCpe</td>
</tr>
<tr class="odd">
<td>metrics_average_cpv</td>
<td>The average amount you pay each time someone views your ad. The average CPV is defined by the total cost of all ad views divided by the number of views.</td>
<td>AverageCpv</td>
</tr>
<tr class="even">
<td>metrics_average_page_views</td>
<td>Average number of pages viewed per session.</td>
<td>AveragePageviews</td>
</tr>
<tr class="odd">
<td>metrics_average_time_on_site</td>
<td>Total duration of all sessions (in seconds) / number of sessions. Imported from Google Analytics.</td>
<td>AverageTimeOnSite</td>
</tr>
<tr class="even">
<td>metrics_bounce_rate</td>
<td>Percentage of clicks where the user only visited a single page on your site. Imported from Google Analytics.</td>
<td>BounceRate</td>
</tr>
<tr class="odd">
<td>metrics_cost_per_all_conversions</td>
<td>The cost of ad interactions divided by all conversions.</td>
<td>CostPerAllConversion</td>
</tr>
<tr class="even">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on a Google Ads ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
<td>CrossDeviceConversions</td>
</tr>
<tr class="odd">
<td>metrics_engagement_rate</td>
<td>How often people engage with your ad after it's shown to them. This is the number of ad expansions divided by the number of times your ad is shown.</td>
<td>EngagementRate</td>
</tr>
<tr class="even">
<td>metrics_engagements</td>
<td>The number of engagements. An engagement occurs when a viewer expands your Lightbox ad. Also, in the future, other ad types may support engagement metrics.</td>
<td>Engagements</td>
</tr>
<tr class="odd">
<td>metrics_percent_new_visitors</td>
<td>Percentage of first-time sessions (from people who had never visited your site before). Imported from Google Analytics.</td>
<td>PercentNewVisitors</td>
</tr>
<tr class="even">
<td>metrics_top_impression_percentage</td>
<td>The percent of your ad impressions that are shown anywhere above the organic search results.</td>
<td>TopImpressionPercentage</td>
</tr>
<tr class="odd">
<td>metrics_value_per_all_conversions</td>
<td>The value of all conversions divided by the number of all conversions.</td>
<td>ValuePerAllConversion</td>
</tr>
<tr class="even">
<td>metrics_video_quartile_p100_rate</td>
<td>Percentage of impressions where the viewer watched all of your video.</td>
<td>VideoQuartile100Rate</td>
</tr>
<tr class="odd">
<td>metrics_video_quartile_p25_rate</td>
<td>Percentage of impressions where the viewer watched 25% of your video.</td>
<td>VideoQuartile25Rate</td>
</tr>
<tr class="even">
<td>metrics_video_quartile_p50_rate</td>
<td>Percentage of impressions where the viewer watched 50% of your video.</td>
<td>VideoQuartile50Rate</td>
</tr>
<tr class="odd">
<td>metrics_video_quartile_p75_rate</td>
<td>Percentage of impressions where the viewer watched 75% of your video.</td>
<td>VideoQuartile75Rate</td>
</tr>
<tr class="even">
<td>metrics_video_view_rate</td>
<td>The number of views your TrueView video ad receives divided by its number of impressions, including thumbnail impressions for TrueView in-display ads.</td>
<td>VideoViewRate</td>
</tr>
<tr class="odd">
<td>metrics_video_views</td>
<td>The number of times your video ads were viewed.</td>
<td>VideoViews</td>
</tr>
<tr class="even">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="even">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="odd">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="even">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="odd">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="even">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: AdGroup

Google Ads API Resource: [ad\_group](https://developers.google.com/google-ads/api/fields/v21/ad_group)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_ad_rotation_mode</td>
<td>The ad rotation mode of the ad group.</td>
<td>AdRotationMode</td>
</tr>
<tr class="even">
<td>ad_group_cpc_bid_micros</td>
<td>The maximum CPC (cost-per-click) bid.</td>
<td>CpcBid</td>
</tr>
<tr class="odd">
<td>ad_group_cpm_bid_micros</td>
<td>The maximum CPM (cost-per-thousand viewable impressions) bid.</td>
<td>CpmBidStr</td>
</tr>
<tr class="even">
<td>ad_group_cpv_bid_micros</td>
<td>The CPV (cost-per-view) bid.</td>
<td>CpvBid</td>
</tr>
<tr class="odd">
<td>ad_group_display_custom_bid_dimension</td>
<td>Allows advertisers to specify a targeting dimension on which to place absolute bids. This is only applicable for campaigns that target only the display network and not search.</td>
<td>ContentBidCriterionTypeGroup</td>
</tr>
<tr class="even">
<td>ad_group_effective_target_cpa_micros</td>
<td>The effective target CPA (cost-per-acquisition). This field is read-only.</td>
<td>TargetCpa</td>
</tr>
<tr class="odd">
<td>ad_group_effective_target_cpa_source</td>
<td>Source of the effective target CPA. This field is read-only.</td>
<td>TargetCpaBidSource</td>
</tr>
<tr class="even">
<td>ad_group_effective_target_roas</td>
<td>The effective target ROAS (return-on-ad-spend). This field is read-only.</td>
<td>EffectiveTargetRoas</td>
</tr>
<tr class="odd">
<td>ad_group_effective_target_roas_source</td>
<td>Source of the effective target ROAS. This field is read-only.</td>
<td>EffectiveTargetRoasSource</td>
</tr>
<tr class="even">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="odd">
<td>ad_group_name</td>
<td>The name of the ad group. This field is required and shouldn't be empty when creating new ad groups. It must contain fewer than 255 UTF-8 full-width characters. It must not contain any null (code point 0x0), NL line feed (code point 0xA) or carriage return (code point 0xD) characters.</td>
<td>AdGroupName</td>
</tr>
<tr class="even">
<td>ad_group_status</td>
<td>The status of the ad group.</td>
<td>AdGroupStatus</td>
</tr>
<tr class="odd">
<td>ad_group_tracking_url_template</td>
<td>The URL template for constructing a tracking URL.</td>
<td>TrackingUrlTemplate</td>
</tr>
<tr class="even">
<td>ad_group_type</td>
<td>The type of the ad group.</td>
<td>AdGroupType</td>
</tr>
<tr class="odd">
<td>ad_group_url_custom_parameters</td>
<td>The list of mappings used to substitute custom parameter tags in a `tracking_url_template`, `final_urls`, or `mobile_final_urls`.</td>
<td>UrlCustomParameters</td>
</tr>
<tr class="even">
<td>campaign_bidding_strategy</td>
<td>Portfolio bidding strategy used by campaign.</td>
<td>BiddingStrategyId</td>
</tr>
<tr class="odd">
<td>campaign_bidding_strategy_type</td>
<td>The type of bidding strategy. A bidding strategy can be created by setting either the bidding scheme to create a standard bidding strategy or the `bidding_strategy` field to create a portfolio bidding strategy. This field is read-only.</td>
<td>BiddingStrategyType</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="odd">
<td>campaign_manual_cpc_enhanced_cpc_enabled</td>
<td>Whether bids are to be enhanced based on conversion optimizer data.</td>
<td>EnhancedCpcEnabled</td>
</tr>
<tr class="even">
<td>campaign_percent_cpc_enhanced_cpc_enabled</td>
<td>Adjusts the bid for each auction upward or downward, depending on the likelihood of a conversion. Individual bids may exceed cpc_bid_ceiling_micros, but the average bid amount for a campaign shouldn't.</td>
<td></td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
</tbody>
</table>

Google Ads Table Name: AdGroupAdLabel

Google Ads API Resource: [ad\_group\_ad\_label](https://developers.google.com/google-ads/api/fields/v21/ad_group_ad_label)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_ad_label_ad_group_ad</td>
<td>The ad group ad to which the label is attached.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_ad_label_label</td>
<td>The label assigned to the ad group ad.</td>
<td></td>
</tr>
<tr class="odd">
<td>ad_group_ad_label_resource_name</td>
<td>The resource name of the ad group ad label. Ad group ad label resource names have the form: `customers/{customer_id}/adGroupAdLabels/{ad_group_id}~{ad_id}~{label_id}`</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td></td>
</tr>
<tr class="odd">
<td>ad_group_name</td>
<td>The name of the ad group. This field is required and shouldn't be empty when creating new ad groups. It must contain fewer than 255 UTF-8 full-width characters. It must not contain any null (code point 0x0), NL line feed (code point 0xA) or carriage return (code point 0xD) characters.</td>
<td></td>
</tr>
<tr class="even">
<td>label_id</td>
<td>Id of the label. Read only.</td>
<td></td>
</tr>
<tr class="odd">
<td>label_name</td>
<td>The name of the label. This field is required and shouldn't be empty when creating a new label. The length of this string should be between 1 and 80, inclusive.</td>
<td></td>
</tr>
<tr class="even">
<td>label_resource_name</td>
<td>Name of the resource. Label resource names have the form: `customers/{customer_id}/labels/{label_id}`</td>
<td></td>
</tr>
</tbody>
</table>

Google Ads Table Name: AdGroupAudience

Google Ads API Resource: [ad\_group\_audience\_view](https://developers.google.com/google-ads/api/fields/v21/ad_group_audience_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_base_ad_group</td>
<td>For draft or experiment ad groups, this field is the resource name of the base ad group from which this ad group was created. If a draft or experiment ad group does not have a base ad group, then this field is null. For base ad groups, this field equals the ad group resource name. This field is read-only.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_campaign</td>
<td>The campaign to which the ad group belongs.</td>
<td></td>
</tr>
<tr class="odd">
<td>ad_group_criterion_bid_modifier</td>
<td>The modifier for the bid when the criterion matches. The modifier must be in the range: 0.1 - 10.0. Most targetable criteria types support modifiers.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion. This field is ignored for mutates.</td>
<td></td>
</tr>
<tr class="odd">
<td>ad_group_criterion_effective_cpc_bid_micros</td>
<td>The effective CPC (cost-per-click) bid.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_criterion_effective_cpc_bid_source</td>
<td>Source of the effective CPC bid.</td>
<td></td>
</tr>
<tr class="odd">
<td>ad_group_criterion_effective_cpm_bid_micros</td>
<td>The effective CPM (cost-per-thousand viewable impressions) bid.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_criterion_effective_cpm_bid_source</td>
<td>Source of the effective CPM bid.</td>
<td></td>
</tr>
<tr class="odd">
<td>ad_group_criterion_final_mobile_urls</td>
<td>The list of possible final mobile URLs after all cross-domain redirects.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_criterion_final_urls</td>
<td>The list of possible final URLs after all cross-domain redirects for the ad.</td>
<td></td>
</tr>
<tr class="odd">
<td>ad_group_criterion_keyword_text</td>
<td>The text of the keyword (at most 80 characters and 10 words).</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_criterion_status</td>
<td>The status of the criterion.</td>
<td></td>
</tr>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_targeting_setting_target_restrictions</td>
<td>The per-targeting-dimension setting to restrict the reach of your campaign or ad group.</td>
<td></td>
</tr>
<tr class="odd">
<td>ad_group_tracking_url_template</td>
<td>The URL template for constructing a tracking URL.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_url_custom_parameters</td>
<td>The list of mappings used to substitute custom parameter tags in a `tracking_url_template`, `final_urls`, or `mobile_final_urls`.</td>
<td></td>
</tr>
<tr class="odd">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td></td>
</tr>
<tr class="even">
<td>campaign_bidding_strategy</td>
<td>Portfolio bidding strategy used by campaign.</td>
<td></td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td></td>
</tr>
</tbody>
</table>

Google Ads Table Name: AdGroupAudienceBasicStats

Google Ads API Resource: [ad\_group\_audience\_view](https://developers.google.com/google-ads/api/fields/v21/ad_group_audience_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_base_ad_group</td>
<td>For draft or experiment ad groups, this field is the resource name of the base ad group from which this ad group was created. If a draft or experiment ad group does not have a base ad group, then this field is null. For base ad groups, this field equals the ad group resource name. This field is read-only.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_campaign</td>
<td>The campaign to which the ad group belongs.</td>
<td></td>
</tr>
<tr class="odd">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion. This field is ignored for mutates.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td></td>
</tr>
<tr class="odd">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td></td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_interaction_event_types</td>
<td>The types of payable and free interactions.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_interactions</td>
<td>The number of interactions. An interaction is the main user action associated with an ad format, such as clicks for text and shopping ads or views for video ads.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_view_through_conversions</td>
<td>The total number of view-through conversions. These happen when a customer sees an image or rich media ad, then later completes a conversion on your site without interacting with (for example, clicking on) another ad.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_slot</td>
<td>Position of the ad.</td>
<td></td>
</tr>
</tbody>
</table>

Google Ads Table Name: AdGroupAudienceConversionStats

Google Ads API Resource: [ad\_group\_audience\_view](https://developers.google.com/google-ads/api/fields/v21/ad_group_audience_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_base_ad_group</td>
<td>For draft or experiment ad groups, this field is the resource name of the base ad group from which this ad group was created. If a draft or experiment ad group does not have a base ad group, then this field is null. For base ad groups, this field equals the ad group resource name. This field is read-only.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_campaign</td>
<td>The campaign to which the ad group belongs.</td>
<td></td>
</tr>
<tr class="odd">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion. This field is ignored for mutates.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td></td>
</tr>
<tr class="odd">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td></td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_all_conversions_value</td>
<td>The total value of all conversions.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on a Google Ads ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_value_per_all_conversions</td>
<td>The value of all conversions divided by the number of all conversions.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_value_per_conversion</td>
<td>The value of conversions divided by the number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_view_through_conversions</td>
<td>The total number of view-through conversions. These happen when a customer sees an image or rich media ad, then later completes a conversion on your site without interacting with (for example, clicking on) another ad.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_conversion_action</td>
<td>Resource name of the conversion action.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_conversion_action_category</td>
<td>Conversion action category.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_conversion_action_name</td>
<td>Conversion action name.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td></td>
</tr>
</tbody>
</table>

Google Ads Table Name: AdGroupAudienceNonClickStats

Google Ads API Resource: [ad\_group\_audience\_view](https://developers.google.com/google-ads/api/fields/v21/ad_group_audience_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_base_ad_group</td>
<td>For draft or experiment ad groups, this field is the resource name of the base ad group from which this ad group was created. If a draft or experiment ad group does not have a base ad group, then this field is null. For base ad groups, this field equals the ad group resource name. This field is read-only.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_campaign</td>
<td>The campaign to which the ad group belongs.</td>
<td></td>
</tr>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td></td>
</tr>
<tr class="even">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td></td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_average_cpe</td>
<td>The average amount that you've been charged for an ad engagement. This amount is the total cost of all ad engagements divided by the total number of ad engagements.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_average_cpv</td>
<td>The average amount you pay each time someone views your ad. The average CPV is defined by the total cost of all ad views divided by the number of views.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_engagement_rate</td>
<td>How often people engage with your ad after it's shown to them. This is the number of ad expansions divided by the number of times your ad is shown.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_engagements</td>
<td>The number of engagements. An engagement occurs when a viewer expands your Lightbox ad. Also, in the future, other ad types may support engagement metrics.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_video_view_rate</td>
<td>The number of views your TrueView video ad receives divided by its number of impressions, including thumbnail impressions for TrueView in-display ads.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_video_views</td>
<td>The number of times your video ads were viewed.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td></td>
</tr>
</tbody>
</table>

Google Ads Table Name: AdGroupAudienceStats

Google Ads API Resource: [ad\_group\_audience\_view](https://developers.google.com/google-ads/api/fields/v21/ad_group_audience_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_base_ad_group</td>
<td>For draft or experiment ad groups, this field is the resource name of the base ad group from which this ad group was created. If a draft or experiment ad group does not have a base ad group, then this field is null. For base ad groups, this field equals the ad group resource name. This field is read-only.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_campaign</td>
<td>The campaign to which the ad group belongs.</td>
<td></td>
</tr>
<tr class="odd">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion. This field is ignored for mutates.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td></td>
</tr>
<tr class="odd">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td></td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_active_view_cpm</td>
<td>Average cost of viewable impressions (`active_view_impressions`).</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_active_view_ctr</td>
<td>Active view measurable clicks divided by active view viewable impressions. This metric is reported only for display network.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_active_view_impressions</td>
<td>A measurement of how often your ad has become viewable on a Display Network site.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_active_view_measurability</td>
<td>The ratio of impressions that could be measured by Active View over the number of served impressions.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_active_view_measurable_cost_micros</td>
<td>The cost of the impressions you received that were measurable by Active View.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_active_view_measurable_impressions</td>
<td>The number of times your ads are appearing on placements in positions where they can be seen.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_active_view_viewability</td>
<td>The percentage of time when your ad appeared on an Active View enabled site (measurable impressions) and was viewable (viewable impressions).</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_all_conversions_from_interactions_rate</td>
<td>All conversions from interactions (as oppose to view through conversions) divided by the number of ad interactions.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_average_cost</td>
<td>The average amount you pay per interaction. This amount is the total cost of your ads divided by the total number of interactions.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_average_cpm</td>
<td>Average cost-per-thousand impressions (CPM).</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_conversions_from_interactions_rate</td>
<td>Conversions from interactions divided by the number of ad interactions (such as clicks for text ads or views for video ads). This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_cost_per_all_conversions</td>
<td>The cost of ad interactions divided by all conversions.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_cost_per_conversion</td>
<td>The cost of ad interactions divided by conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_gmail_forwards</td>
<td>The number of times the ad was forwarded to someone else as a message.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_gmail_saves</td>
<td>The number of times someone has saved your Gmail ad to their inbox as a message.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_gmail_secondary_clicks</td>
<td>The number of clicks to the landing page on the expanded state of Gmail ads.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_interaction_event_types</td>
<td>The types of payable and free interactions.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_interaction_rate</td>
<td>How often people interact with your ad after it is shown to them. This is the number of interactions divided by the number of times your ad is shown.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_interactions</td>
<td>The number of interactions. An interaction is the main user action associated with an ad format, such as clicks for text and shopping ads or views for video ads.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_value_per_conversion</td>
<td>The value of conversions divided by the number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_click_type</td>
<td>Click type.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td></td>
</tr>
</tbody>
</table>

Google Ads Table Name: AdGroupBasicStats

Google Ads API Resource: [ad\_group](https://developers.google.com/google-ads/api/fields/v21/ad_group)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_base_ad_group</td>
<td>For draft or experiment ad groups, this field is the resource name of the base ad group from which this ad group was created. If a draft or experiment ad group does not have a base ad group, then this field is null. For base ad groups, this field equals the ad group resource name. This field is read-only.</td>
<td>BaseAdGroupId</td>
</tr>
<tr class="even">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="odd">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td>BaseCampaignId</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="even">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
<td>Clicks</td>
</tr>
<tr class="odd">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>Conversions</td>
</tr>
<tr class="even">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="odd">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
<td>Cost</td>
</tr>
<tr class="even">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
<td>Impressions</td>
</tr>
<tr class="odd">
<td>metrics_interaction_event_types</td>
<td>The types of payable and free interactions.</td>
<td>InteractionTypes</td>
</tr>
<tr class="even">
<td>metrics_interactions</td>
<td>The number of interactions. An interaction is the main user action associated with an ad format, such as clicks for text and shopping ads or views for video ads.</td>
<td>Interactions</td>
</tr>
<tr class="odd">
<td>metrics_view_through_conversions</td>
<td>The total number of view-through conversions. These happen when a customer sees an image or rich media ad, then later completes a conversion on your site without interacting with (for example, clicking on) another ad.</td>
<td>ViewThroughConversions</td>
</tr>
<tr class="even">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="even">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
<tr class="odd">
<td>segments_slot</td>
<td>Position of the ad.</td>
<td>Slot</td>
</tr>
</tbody>
</table>

Google Ads Table Name: AdGroupBidModifier

Google Ads API Resource: [ad\_group\_bid\_modifier](https://developers.google.com/google-ads/api/fields/v21/ad_group_bid_modifier)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_bid_modifier_ad_group</td>
<td>The ad group to which this criterion belongs.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_bid_modifier_base_ad_group</td>
<td>The base ad group from which this draft or trial adgroup bid modifier was created. If ad_group is a base ad group then this field is equal to ad_group. If the ad group was created in the draft or trial and has no corresponding base ad group, then this field is null. This field is read-only.</td>
<td></td>
</tr>
<tr class="odd">
<td>ad_group_bid_modifier_bid_modifier</td>
<td>The modifier for the bid when the criterion matches. The modifier must be in the range: 0.1 - 10.0. The range is 1.0 - 6.0 for PreferredContent. Use 0 to opt out of a Device type.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_bid_modifier_bid_modifier_source</td>
<td>Bid modifier source.</td>
<td></td>
</tr>
<tr class="odd">
<td>ad_group_bid_modifier_criterion_id</td>
<td>The ID of the criterion to bid modify. This field is ignored for mutates.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_bid_modifier_device_type</td>
<td>Type of the device.</td>
<td></td>
</tr>
<tr class="odd">
<td>ad_group_bid_modifier_resource_name</td>
<td>The resource name of the ad group bid modifier. Ad group bid modifier resource names have the form: `customers/{customer_id}/adGroupBidModifiers/{ad_group_id}~{criterion_id}`</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td></td>
</tr>
<tr class="odd">
<td>ad_group_name</td>
<td>The name of the ad group. This field is required and shouldn't be empty when creating new ad groups. It must contain fewer than 255 UTF-8 full-width characters. It must not contain any null (code point 0x0), NL line feed (code point 0xA) or carriage return (code point 0xD) characters.</td>
<td></td>
</tr>
</tbody>
</table>

Google Ads Table Name: AdGroupConversionStats

Google Ads API Resource: [ad\_group](https://developers.google.com/google-ads/api/fields/v21/ad_group)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_base_ad_group</td>
<td>For draft or experiment ad groups, this field is the resource name of the base ad group from which this ad group was created. If a draft or experiment ad group does not have a base ad group, then this field is null. For base ad groups, this field equals the ad group resource name. This field is read-only.</td>
<td>BaseAdGroupId</td>
</tr>
<tr class="even">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="odd">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td>BaseCampaignId</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="even">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>Conversions</td>
</tr>
<tr class="odd">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="even">
<td>metrics_value_per_conversion</td>
<td>The value of conversions divided by the number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ValuePerConversion</td>
</tr>
<tr class="odd">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="even">
<td>segments_click_type</td>
<td>Click type.</td>
<td>ClickType</td>
</tr>
<tr class="odd">
<td>segments_conversion_action</td>
<td>Resource name of the conversion action.</td>
<td>ConversionTrackerId</td>
</tr>
<tr class="even">
<td>segments_conversion_action_category</td>
<td>Conversion action category.</td>
<td>ConversionCategoryName</td>
</tr>
<tr class="odd">
<td>segments_conversion_action_name</td>
<td>Conversion action name.</td>
<td>ConversionTypeName</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="odd">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="even">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
<tr class="odd">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="even">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="odd">
<td>segments_slot</td>
<td>Position of the ad.</td>
<td>Slot</td>
</tr>
<tr class="even">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="odd">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: AdGroupCriterion

Google Ads API Resource: [ad\_group\_criterion](https://developers.google.com/google-ads/api/fields/v21/ad_group_criterion)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_criterion_ad_group</td>
<td>The ad group to which the criterion belongs.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_criterion_bid_modifier</td>
<td>The modifier for the bid when the criterion matches. The modifier must be in the range: 0.1 - 10.0. Most targetable criteria types support modifiers.</td>
<td></td>
</tr>
<tr class="odd">
<td>ad_group_criterion_cpc_bid_micros</td>
<td>The CPC (cost-per-click) bid.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_criterion_cpm_bid_micros</td>
<td>The CPM (cost-per-thousand viewable impressions) bid.</td>
<td></td>
</tr>
<tr class="odd">
<td>ad_group_criterion_cpv_bid_micros</td>
<td>The CPC (cost-per-view) bid.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion. This field is ignored for mutates.</td>
<td></td>
</tr>
<tr class="odd">
<td>ad_group_criterion_display_name</td>
<td>The display name of the criterion. This field is ignored for mutates.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_criterion_negative</td>
<td>Whether to target (`false`) or exclude (`true`) the criterion.</td>
<td></td>
</tr>
<tr class="odd">
<td>ad_group_criterion_status</td>
<td>The status of the criterion.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_criterion_type</td>
<td>The type of the criterion.</td>
<td></td>
</tr>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_name</td>
<td>The name of the ad group. This field is required and shouldn't be empty when creating new ad groups. It must contain fewer than 255 UTF-8 full-width characters. It must not contain any null (code point 0x0), NL line feed (code point 0xA) or carriage return (code point 0xD) characters.</td>
<td></td>
</tr>
</tbody>
</table>

Google Ads Table Name: AdGroupCriterionLabel

Google Ads API Resource: [ad\_group\_criterion\_label](https://developers.google.com/google-ads/api/fields/v21/ad_group_criterion_label)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion. This field is ignored for mutates.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_criterion_label_ad_group_criterion</td>
<td>The ad group criterion to which the label is attached.</td>
<td></td>
</tr>
<tr class="odd">
<td>ad_group_criterion_label_label</td>
<td>The label assigned to the ad group criterion.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_criterion_label_resource_name</td>
<td>The resource name of the ad group criterion label. Ad group criterion label resource names have the form: `customers/{customer_id}/adGroupCriterionLabels/{ad_group_id}~{criterion_id}~{label_id}`</td>
<td></td>
</tr>
<tr class="odd">
<td>label_id</td>
<td>Id of the label. Read only.</td>
<td></td>
</tr>
<tr class="even">
<td>label_name</td>
<td>The name of the label. This field is required and shouldn't be empty when creating a new label. The length of this string should be between 1 and 80, inclusive.</td>
<td></td>
</tr>
<tr class="odd">
<td>label_resource_name</td>
<td>Name of the resource. Label resource names have the form: `customers/{customer_id}/labels/{label_id}`</td>
<td></td>
</tr>
</tbody>
</table>

Google Ads Table Name: AdGroupCrossDeviceConversionStats

Google Ads API Resource: [ad\_group](https://developers.google.com/google-ads/api/fields/v21/ad_group)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_base_ad_group</td>
<td>For draft or experiment ad groups, this field is the resource name of the base ad group from which this ad group was created. If a draft or experiment ad group does not have a base ad group, then this field is null. For base ad groups, this field equals the ad group resource name. This field is read-only.</td>
<td>BaseAdGroupId</td>
</tr>
<tr class="even">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="odd">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td>BaseCampaignId</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="even">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>AllConversions</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions_value</td>
<td>The total value of all conversions.</td>
<td>AllConversionValue</td>
</tr>
<tr class="even">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on a Google Ads ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
<td>CrossDeviceConversions</td>
</tr>
<tr class="odd">
<td>metrics_value_per_all_conversions</td>
<td>The value of all conversions divided by the number of all conversions.</td>
<td>ValuePerAllConversion</td>
</tr>
<tr class="even">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="odd">
<td>segments_conversion_action</td>
<td>Resource name of the conversion action.</td>
<td>ConversionTrackerId</td>
</tr>
<tr class="even">
<td>segments_conversion_action_category</td>
<td>Conversion action category.</td>
<td>ConversionCategoryName</td>
</tr>
<tr class="odd">
<td>segments_conversion_action_name</td>
<td>Conversion action name.</td>
<td>ConversionTypeName</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="odd">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="even">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="odd">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="even">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="odd">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: AdGroupCrossDeviceStats

Google Ads API Resource: [ad\_group](https://developers.google.com/google-ads/api/fields/v21/ad_group)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_base_ad_group</td>
<td>For draft or experiment ad groups, this field is the resource name of the base ad group from which this ad group was created. If a draft or experiment ad group does not have a base ad group, then this field is null. For base ad groups, this field equals the ad group resource name. This field is read-only.</td>
<td>BaseAdGroupId</td>
</tr>
<tr class="even">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="odd">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td>BaseCampaignId</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="even">
<td>metrics_absolute_top_impression_percentage</td>
<td>The percent of your ad impressions that are shown as the very first ad above the organic search results.</td>
<td>AbsoluteTopImpressionPercentage</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>AllConversions</td>
</tr>
<tr class="even">
<td>metrics_all_conversions_from_interactions_rate</td>
<td>All conversions from interactions (as oppose to view through conversions) divided by the number of ad interactions.</td>
<td>AllConversionRate</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions_value</td>
<td>The total value of all conversions.</td>
<td>AllConversionValue</td>
</tr>
<tr class="even">
<td>metrics_average_cpe</td>
<td>The average amount that you've been charged for an ad engagement. This amount is the total cost of all ad engagements divided by the total number of ad engagements.</td>
<td>AverageCpe</td>
</tr>
<tr class="odd">
<td>metrics_average_cpv</td>
<td>The average amount you pay each time someone views your ad. The average CPV is defined by the total cost of all ad views divided by the number of views.</td>
<td>AverageCpv</td>
</tr>
<tr class="even">
<td>metrics_average_page_views</td>
<td>Average number of pages viewed per session.</td>
<td>AveragePageviews</td>
</tr>
<tr class="odd">
<td>metrics_average_time_on_site</td>
<td>Total duration of all sessions (in seconds) / number of sessions. Imported from Google Analytics.</td>
<td>AverageTimeOnSite</td>
</tr>
<tr class="even">
<td>metrics_bounce_rate</td>
<td>Percentage of clicks where the user only visited a single page on your site. Imported from Google Analytics.</td>
<td>BounceRate</td>
</tr>
<tr class="odd">
<td>metrics_content_impression_share</td>
<td>The impressions you've received on the Display Network divided by the estimated number of impressions you were eligible to receive. Note: Content impression share is reported in the range of 0.1 to 1. Any value below 0.1 is reported as 0.0999.</td>
<td>ContentImpressionShare</td>
</tr>
<tr class="even">
<td>metrics_content_rank_lost_impression_share</td>
<td>The estimated percentage of impressions on the Display Network that your ads didn't receive due to poor Ad Rank. Note: Content rank lost impression share is reported in the range of 0 to 0.9. Any value above 0.9 is reported as 0.9001.</td>
<td>ContentRankLostImpressionShare</td>
</tr>
<tr class="odd">
<td>metrics_cost_per_all_conversions</td>
<td>The cost of ad interactions divided by all conversions.</td>
<td>CostPerAllConversion</td>
</tr>
<tr class="even">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on a Google Ads ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
<td>CrossDeviceConversions</td>
</tr>
<tr class="odd">
<td>metrics_engagement_rate</td>
<td>How often people engage with your ad after it's shown to them. This is the number of ad expansions divided by the number of times your ad is shown.</td>
<td>EngagementRate</td>
</tr>
<tr class="even">
<td>metrics_engagements</td>
<td>The number of engagements. An engagement occurs when a viewer expands your Lightbox ad. Also, in the future, other ad types may support engagement metrics.</td>
<td>Engagements</td>
</tr>
<tr class="odd">
<td>metrics_percent_new_visitors</td>
<td>Percentage of first-time sessions (from people who had never visited your site before). Imported from Google Analytics.</td>
<td>PercentNewVisitors</td>
</tr>
<tr class="even">
<td>metrics_phone_calls</td>
<td>Number of offline phone calls.</td>
<td>NumOfflineInteractions</td>
</tr>
<tr class="odd">
<td>metrics_phone_impressions</td>
<td>Number of offline phone impressions.</td>
<td>NumOfflineImpressions</td>
</tr>
<tr class="even">
<td>metrics_phone_through_rate</td>
<td>Number of phone calls received (phone_calls) divided by the number of times your phone number is shown (phone_impressions).</td>
<td>OfflineInteractionRate</td>
</tr>
<tr class="odd">
<td>metrics_relative_ctr</td>
<td>Your clickthrough rate (Ctr) divided by the average clickthrough rate of all advertisers on the websites that show your ads. Measures how your ads perform on Display Network sites compared to other ads on the same sites.</td>
<td>RelativeCtr</td>
</tr>
<tr class="even">
<td>metrics_search_absolute_top_impression_share</td>
<td>The percentage of the customer's Shopping or Search ad impressions that are shown in the most prominent Shopping position. See https://support.google.com/google-ads/answer/7501826 for details. Any value below 0.1 is reported as 0.0999.</td>
<td>SearchAbsoluteTopImpressionShare</td>
</tr>
<tr class="odd">
<td>metrics_search_budget_lost_absolute_top_impression_share</td>
<td>The number estimating how often your ad wasn't the very first ad above the organic search results due to a low budget. Note: Search budget lost absolute top impression share is reported in the range of 0 to 0.9. Any value above 0.9 is reported as 0.9001.</td>
<td>SearchBudgetLostAbsoluteTopImpressionShare</td>
</tr>
<tr class="even">
<td>metrics_search_budget_lost_top_impression_share</td>
<td>The number estimating how often your ad didn't show anywhere above the organic search results due to a low budget. Note: Search budget lost top impression share is reported in the range of 0 to 0.9. Any value above 0.9 is reported as 0.9001.</td>
<td>SearchBudgetLostTopImpressionShare</td>
</tr>
<tr class="odd">
<td>metrics_search_exact_match_impression_share</td>
<td>The impressions you've received divided by the estimated number of impressions you were eligible to receive on the Search Network for search terms that matched your keywords exactly (or were close variants of your keyword), regardless of your keyword match types. Note: Search exact match impression share is reported in the range of 0.1 to 1. Any value below 0.1 is reported as 0.0999.</td>
<td>SearchExactMatchImpressionShare</td>
</tr>
<tr class="even">
<td>metrics_search_impression_share</td>
<td>The impressions you've received on the Search Network divided by the estimated number of impressions you were eligible to receive. Note: Search impression share is reported in the range of 0.1 to 1. Any value below 0.1 is reported as 0.0999.</td>
<td>SearchImpressionShare</td>
</tr>
<tr class="odd">
<td>metrics_search_rank_lost_absolute_top_impression_share</td>
<td>The number estimating how often your ad wasn't the very first ad above the organic search results due to poor Ad Rank. Note: Search rank lost absolute top impression share is reported in the range of 0 to 0.9. Any value above 0.9 is reported as 0.9001.</td>
<td>SearchRankLostAbsoluteTopImpressionShare</td>
</tr>
<tr class="even">
<td>metrics_search_rank_lost_impression_share</td>
<td>The estimated percentage of impressions on the Search Network that your ads didn't receive due to poor Ad Rank. Note: Search rank lost impression share is reported in the range of 0 to 0.9. Any value above 0.9 is reported as 0.9001.</td>
<td>SearchRankLostImpressionShare</td>
</tr>
<tr class="odd">
<td>metrics_search_rank_lost_top_impression_share</td>
<td>The number estimating how often your ad didn't show anywhere above the organic search results due to poor Ad Rank. Note: Search rank lost top impression share is reported in the range of 0 to 0.9. Any value above 0.9 is reported as 0.9001.</td>
<td>SearchRankLostTopImpressionShare</td>
</tr>
<tr class="even">
<td>metrics_search_top_impression_share</td>
<td>The impressions you've received in the top location (anywhere above the organic search results) compared to the estimated number of impressions you were eligible to receive in the top location. Note: Search top impression share is reported in the range of 0.1 to 1. Any value below 0.1 is reported as 0.0999.</td>
<td>SearchTopImpressionShare</td>
</tr>
<tr class="odd">
<td>metrics_top_impression_percentage</td>
<td>The percent of your ad impressions that are shown anywhere above the organic search results.</td>
<td>TopImpressionPercentage</td>
</tr>
<tr class="even">
<td>metrics_value_per_all_conversions</td>
<td>The value of all conversions divided by the number of all conversions.</td>
<td>ValuePerAllConversion</td>
</tr>
<tr class="odd">
<td>metrics_video_quartile_p100_rate</td>
<td>Percentage of impressions where the viewer watched all of your video.</td>
<td>VideoQuartile100Rate</td>
</tr>
<tr class="even">
<td>metrics_video_quartile_p25_rate</td>
<td>Percentage of impressions where the viewer watched 25% of your video.</td>
<td>VideoQuartile25Rate</td>
</tr>
<tr class="odd">
<td>metrics_video_quartile_p50_rate</td>
<td>Percentage of impressions where the viewer watched 50% of your video.</td>
<td>VideoQuartile50Rate</td>
</tr>
<tr class="even">
<td>metrics_video_quartile_p75_rate</td>
<td>Percentage of impressions where the viewer watched 75% of your video.</td>
<td>VideoQuartile75Rate</td>
</tr>
<tr class="odd">
<td>metrics_video_view_rate</td>
<td>The number of views your TrueView video ad receives divided by its number of impressions, including thumbnail impressions for TrueView in-display ads.</td>
<td>VideoViewRate</td>
</tr>
<tr class="even">
<td>metrics_video_views</td>
<td>The number of times your video ads were viewed.</td>
<td>VideoViews</td>
</tr>
<tr class="odd">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="odd">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="even">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="odd">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="even">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="odd">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: AdGroupLabel

Google Ads API Resource: [ad\_group\_label](https://developers.google.com/google-ads/api/fields/v21/ad_group_label)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_label_ad_group</td>
<td>The ad group to which the label is attached.</td>
<td></td>
</tr>
<tr class="odd">
<td>ad_group_label_label</td>
<td>The label assigned to the ad group.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_label_resource_name</td>
<td>The resource name of the ad group label. Ad group label resource names have the form: `customers/{customer_id}/adGroupLabels/{ad_group_id}~{label_id}`</td>
<td></td>
</tr>
<tr class="odd">
<td>ad_group_name</td>
<td>The name of the ad group. This field is required and shouldn't be empty when creating new ad groups. It must contain fewer than 255 UTF-8 full-width characters. It must not contain any null (code point 0x0), NL line feed (code point 0xA) or carriage return (code point 0xD) characters.</td>
<td></td>
</tr>
<tr class="even">
<td>label_id</td>
<td>Id of the label. Read only.</td>
<td></td>
</tr>
<tr class="odd">
<td>label_name</td>
<td>The name of the label. This field is required and shouldn't be empty when creating a new label. The length of this string should be between 1 and 80, inclusive.</td>
<td></td>
</tr>
<tr class="even">
<td>label_resource_name</td>
<td>Name of the resource. Label resource names have the form: `customers/{customer_id}/labels/{label_id}`</td>
<td></td>
</tr>
</tbody>
</table>

Google Ads Table Name: AdGroupStats

Google Ads API Resource: [ad\_group](https://developers.google.com/google-ads/api/fields/v21/ad_group)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_base_ad_group</td>
<td>For draft or experiment ad groups, this field is the resource name of the base ad group from which this ad group was created. If a draft or experiment ad group does not have a base ad group, then this field is null. For base ad groups, this field equals the ad group resource name. This field is read-only.</td>
<td>BaseAdGroupId</td>
</tr>
<tr class="even">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="odd">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td>BaseCampaignId</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="even">
<td>metrics_active_view_cpm</td>
<td>Average cost of viewable impressions (`active_view_impressions`).</td>
<td>ActiveViewCpm</td>
</tr>
<tr class="odd">
<td>metrics_active_view_ctr</td>
<td>Active view measurable clicks divided by active view viewable impressions. This metric is reported only for display network.</td>
<td>ActiveViewCtr</td>
</tr>
<tr class="even">
<td>metrics_active_view_impressions</td>
<td>A measurement of how often your ad has become viewable on a Display Network site.</td>
<td>ActiveViewImpressions</td>
</tr>
<tr class="odd">
<td>metrics_active_view_measurability</td>
<td>The ratio of impressions that could be measured by Active View over the number of served impressions.</td>
<td>ActiveViewMeasurability</td>
</tr>
<tr class="even">
<td>metrics_active_view_measurable_cost_micros</td>
<td>The cost of the impressions you received that were measurable by Active View.</td>
<td>ActiveViewMeasurableCost</td>
</tr>
<tr class="odd">
<td>metrics_active_view_measurable_impressions</td>
<td>The number of times your ads are appearing on placements in positions where they can be seen.</td>
<td>ActiveViewMeasurableImpressions</td>
</tr>
<tr class="even">
<td>metrics_active_view_viewability</td>
<td>The percentage of time when your ad appeared on an Active View enabled site (measurable impressions) and was viewable (viewable impressions).</td>
<td>ActiveViewViewability</td>
</tr>
<tr class="odd">
<td>metrics_average_cost</td>
<td>The average amount you pay per interaction. This amount is the total cost of your ads divided by the total number of interactions.</td>
<td>AverageCost</td>
</tr>
<tr class="even">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
<td>AverageCpc</td>
</tr>
<tr class="odd">
<td>metrics_average_cpm</td>
<td>Average cost-per-thousand impressions (CPM).</td>
<td>AverageCpm</td>
</tr>
<tr class="even">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
<td>Clicks</td>
</tr>
<tr class="odd">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>Conversions</td>
</tr>
<tr class="even">
<td>metrics_conversions_from_interactions_rate</td>
<td>Conversions from interactions divided by the number of ad interactions (such as clicks for text ads or views for video ads). This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionRate</td>
</tr>
<tr class="odd">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="even">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
<td>Cost</td>
</tr>
<tr class="odd">
<td>metrics_cost_per_conversion</td>
<td>The cost of ad interactions divided by conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>CostPerConversion</td>
</tr>
<tr class="even">
<td>metrics_cost_per_current_model_attributed_conversion</td>
<td>The cost of ad interactions divided by current model attributed conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>CostPerCurrentModelAttributedConversion</td>
</tr>
<tr class="odd">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
<td>Ctr</td>
</tr>
<tr class="even">
<td>metrics_current_model_attributed_conversions</td>
<td>Shows how your historic conversions data would look under the attribution model you've selected. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>CurrentModelAttributedConversions</td>
</tr>
<tr class="odd">
<td>metrics_current_model_attributed_conversions_value</td>
<td>The total value of current model attributed conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>CurrentModelAttributedConversionValue</td>
</tr>
<tr class="even">
<td>metrics_gmail_forwards</td>
<td>The number of times the ad was forwarded to someone else as a message.</td>
<td>GmailForwards</td>
</tr>
<tr class="odd">
<td>metrics_gmail_saves</td>
<td>The number of times someone has saved your Gmail ad to their inbox as a message.</td>
<td>GmailSaves</td>
</tr>
<tr class="even">
<td>metrics_gmail_secondary_clicks</td>
<td>The number of clicks to the landing page on the expanded state of Gmail ads.</td>
<td>GmailSecondaryClicks</td>
</tr>
<tr class="odd">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
<td>Impressions</td>
</tr>
<tr class="even">
<td>metrics_interaction_event_types</td>
<td>The types of payable and free interactions.</td>
<td>InteractionTypes</td>
</tr>
<tr class="odd">
<td>metrics_interaction_rate</td>
<td>How often people interact with your ad after it is shown to them. This is the number of interactions divided by the number of times your ad is shown.</td>
<td>InteractionRate</td>
</tr>
<tr class="even">
<td>metrics_interactions</td>
<td>The number of interactions. An interaction is the main user action associated with an ad format, such as clicks for text and shopping ads or views for video ads.</td>
<td>Interactions</td>
</tr>
<tr class="odd">
<td>metrics_value_per_conversion</td>
<td>The value of conversions divided by the number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ValuePerConversion</td>
</tr>
<tr class="even">
<td>metrics_value_per_current_model_attributed_conversion</td>
<td>The value of current model attributed conversions divided by the number of the conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ValuePerCurrentModelAttributedConversion</td>
</tr>
<tr class="odd">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="even">
<td>segments_click_type</td>
<td>Click type.</td>
<td>ClickType</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="even">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="odd">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
<tr class="even">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="odd">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="even">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="odd">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: AdStats

Google Ads API Resource: [ad\_group\_ad](https://developers.google.com/google-ads/api/fields/v21/ad_group_ad)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_ad_ad_group</td>
<td>The ad group to which the ad belongs.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_id</td>
<td>The ID of the ad.</td>
<td>CreativeId</td>
</tr>
<tr class="odd">
<td>ad_group_base_ad_group</td>
<td>For draft or experiment ad groups, this field is the resource name of the base ad group from which this ad group was created. If a draft or experiment ad group does not have a base ad group, then this field is null. For base ad groups, this field equals the ad group resource name. This field is read-only.</td>
<td>BaseAdGroupId</td>
</tr>
<tr class="even">
<td>ad_group_id</td>
<td>Output only. The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="odd">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td>BaseCampaignId</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="even">
<td>metrics_active_view_cpm</td>
<td>Average cost of viewable impressions (`active_view_impressions`).</td>
<td>ActiveViewCpm</td>
</tr>
<tr class="odd">
<td>metrics_active_view_ctr</td>
<td>Active view measurable clicks divided by active view viewable impressions. This metric is reported only for display network.</td>
<td>ActiveViewCtr</td>
</tr>
<tr class="even">
<td>metrics_active_view_impressions</td>
<td>A measurement of how often your ad has become viewable on a Display Network site.</td>
<td>ActiveViewImpressions</td>
</tr>
<tr class="odd">
<td>metrics_active_view_measurability</td>
<td>The ratio of impressions that could be measured by Active View over the number of served impressions.</td>
<td>ActiveViewMeasurability</td>
</tr>
<tr class="even">
<td>metrics_active_view_measurable_cost_micros</td>
<td>The cost of the impressions you received that were measurable by Active View.</td>
<td>ActiveViewMeasurableCost</td>
</tr>
<tr class="odd">
<td>metrics_active_view_measurable_impressions</td>
<td>The number of times your ads are appearing on placements in positions where they can be seen.</td>
<td>ActiveViewMeasurableImpressions</td>
</tr>
<tr class="even">
<td>metrics_active_view_viewability</td>
<td>The percentage of time when your ad appeared on an Active View enabled site (measurable impressions) and was viewable (viewable impressions).</td>
<td>ActiveViewViewability</td>
</tr>
<tr class="odd">
<td>metrics_average_cost</td>
<td>The average amount you pay per interaction. This amount is the total cost of your ads divided by the total number of interactions.</td>
<td>AverageCost</td>
</tr>
<tr class="even">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
<td>AverageCpc</td>
</tr>
<tr class="odd">
<td>metrics_average_cpm</td>
<td>Average cost-per-thousand impressions (CPM).</td>
<td>AverageCpm</td>
</tr>
<tr class="even">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
<td>Clicks</td>
</tr>
<tr class="odd">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>Conversions</td>
</tr>
<tr class="even">
<td>metrics_conversions_from_interactions_rate</td>
<td>Conversions from interactions divided by the number of ad interactions (such as clicks for text ads or views for video ads). This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionRate</td>
</tr>
<tr class="odd">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="even">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
<td>Cost</td>
</tr>
<tr class="odd">
<td>metrics_cost_per_conversion</td>
<td>The cost of ad interactions divided by conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>CostPerConversion</td>
</tr>
<tr class="even">
<td>metrics_cost_per_current_model_attributed_conversion</td>
<td>The cost of ad interactions divided by current model attributed conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>CostPerCurrentModelAttributedConversion</td>
</tr>
<tr class="odd">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
<td>Ctr</td>
</tr>
<tr class="even">
<td>metrics_current_model_attributed_conversions</td>
<td>Shows how your historic conversions data would look under the attribution model you've selected. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>CurrentModelAttributedConversions</td>
</tr>
<tr class="odd">
<td>metrics_gmail_forwards</td>
<td>The number of times the ad was forwarded to someone else as a message.</td>
<td>GmailForwards</td>
</tr>
<tr class="even">
<td>metrics_gmail_saves</td>
<td>The number of times someone has saved your Gmail ad to their inbox as a message.</td>
<td>GmailSaves</td>
</tr>
<tr class="odd">
<td>metrics_gmail_secondary_clicks</td>
<td>The number of clicks to the landing page on the expanded state of Gmail ads.</td>
<td>GmailSecondaryClicks</td>
</tr>
<tr class="even">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
<td>Impressions</td>
</tr>
<tr class="odd">
<td>metrics_interaction_event_types</td>
<td>The types of payable and free interactions.</td>
<td>InteractionTypes</td>
</tr>
<tr class="even">
<td>metrics_interaction_rate</td>
<td>How often people interact with your ad after it is shown to them. This is the number of interactions divided by the number of times your ad is shown.</td>
<td>InteractionRate</td>
</tr>
<tr class="odd">
<td>metrics_interactions</td>
<td>The number of interactions. An interaction is the main user action associated with an ad format, such as clicks for text and shopping ads or views for video ads.</td>
<td>Interactions</td>
</tr>
<tr class="even">
<td>metrics_value_per_conversion</td>
<td>The value of conversions divided by the number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ValuePerConversion</td>
</tr>
<tr class="odd">
<td>metrics_value_per_current_model_attributed_conversion</td>
<td>The value of current model attributed conversions divided by the number of the conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ValuePerCurrentModelAttributedConversion</td>
</tr>
<tr class="even">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="odd">
<td>segments_click_type</td>
<td>Click type.</td>
<td>ClickType</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="odd">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="even">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
<tr class="odd">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="even">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="odd">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="even">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: AgeRange

Google Ads API Resource: [age\_range\_view](https://developers.google.com/google-ads/api/fields/v21/age_range_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_base_ad_group</td>
<td>For draft or experiment ad groups, this field is the resource name of the base ad group from which this ad group was created. If a draft or experiment ad group does not have a base ad group, then this field is null. For base ad groups, this field equals the ad group resource name. This field is read-only.</td>
<td>BaseAdGroupId</td>
</tr>
<tr class="even">
<td>ad_group_criterion_age_range_type</td>
<td>Type of the age range.</td>
<td>Criteria</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_bid_modifier</td>
<td>The modifier for the bid when the criterion matches. The modifier must be in the range: 0.1 - 10.0. Most targetable criteria types support modifiers.</td>
<td>BidModifier</td>
</tr>
<tr class="even">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion. This field is ignored for mutates.</td>
<td>CriterionId</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_effective_cpc_bid_micros</td>
<td>The effective CPC (cost-per-click) bid.</td>
<td>CpcBid</td>
</tr>
<tr class="even">
<td>ad_group_criterion_effective_cpc_bid_source</td>
<td>Source of the effective CPC bid.</td>
<td>CpcBidSource</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_effective_cpm_bid_micros</td>
<td>The effective CPM (cost-per-thousand viewable impressions) bid.</td>
<td>CpmBidStr</td>
</tr>
<tr class="even">
<td>ad_group_criterion_effective_cpm_bid_source</td>
<td>Source of the effective CPM bid.</td>
<td>CpmBidSource</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_final_mobile_urls</td>
<td>The list of possible final mobile URLs after all cross-domain redirects.</td>
<td>FinalMobileUrls</td>
</tr>
<tr class="even">
<td>ad_group_criterion_final_urls</td>
<td>The list of possible final URLs after all cross-domain redirects for the ad.</td>
<td>FinalUrls</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_negative</td>
<td>Whether to target (`false`) or exclude (`true`) the criterion. This field is immutable. To switch a criterion from positive to negative, remove then re-add it.</td>
<td>IsNegative</td>
</tr>
<tr class="even">
<td>ad_group_criterion_status</td>
<td>The status of the criterion.</td>
<td>Status</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_tracking_url_template</td>
<td>The URL template for constructing a tracking URL.</td>
<td>TrackingUrlTemplate</td>
</tr>
<tr class="even">
<td>ad_group_criterion_url_custom_parameters</td>
<td>The list of mappings used to substitute custom parameter tags in a `tracking_url_template`, `final_urls`, or `mobile_final_urls`.</td>
<td>UrlCustomParameters</td>
</tr>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="even">
<td>ad_group_targeting_setting_target_restrictions</td>
<td>The per-targeting-dimension setting to restrict the reach of your campaign or ad group.</td>
<td></td>
</tr>
<tr class="odd">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td>BaseCampaignId</td>
</tr>
<tr class="even">
<td>campaign_bidding_strategy</td>
<td>Portfolio bidding strategy used by campaign.</td>
<td>BiddingStrategyId</td>
</tr>
<tr class="odd">
<td>campaign_bidding_strategy_type</td>
<td>The type of bidding strategy. A bidding strategy can be created by setting either the bidding scheme to create a standard bidding strategy or the `bidding_strategy` field to create a portfolio bidding strategy. This field is read-only.</td>
<td>BiddingStrategyType</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
</tbody>
</table>

Google Ads Table Name: AgeRangeBasicStats

Google Ads API Resource: [age\_range\_view](https://developers.google.com/google-ads/api/fields/v21/age_range_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_base_ad_group</td>
<td>For draft or experiment ad groups, this field is the resource name of the base ad group from which this ad group was created. If a draft or experiment ad group does not have a base ad group, then this field is null. For base ad groups, this field equals the ad group resource name. This field is read-only.</td>
<td>BaseAdGroupId</td>
</tr>
<tr class="even">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion. This field is ignored for mutates.</td>
<td>CriterionId</td>
</tr>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="even">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td>BaseCampaignId</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="odd">
<td>metrics_active_view_impressions</td>
<td>A measurement of how often your ad has become viewable on a Display Network site.</td>
<td>ActiveViewImpressions</td>
</tr>
<tr class="even">
<td>metrics_active_view_measurability</td>
<td>The ratio of impressions that could be measured by Active View over the number of served impressions.</td>
<td>ActiveViewMeasurability</td>
</tr>
<tr class="odd">
<td>metrics_active_view_measurable_cost_micros</td>
<td>The cost of the impressions you received that were measurable by Active View.</td>
<td>ActiveViewMeasurableCost</td>
</tr>
<tr class="even">
<td>metrics_active_view_measurable_impressions</td>
<td>The number of times your ads are appearing on placements in positions where they can be seen.</td>
<td>ActiveViewMeasurableImpressions</td>
</tr>
<tr class="odd">
<td>metrics_active_view_viewability</td>
<td>The percentage of time when your ad appeared on an Active View enabled site (measurable impressions) and was viewable (viewable impressions).</td>
<td>ActiveViewViewability</td>
</tr>
<tr class="even">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>AllConversions</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions_value</td>
<td>The total value of all conversions.</td>
<td>AllConversionValue</td>
</tr>
<tr class="even">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
<td>Clicks</td>
</tr>
<tr class="odd">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>Conversions</td>
</tr>
<tr class="even">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="odd">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
<td>Cost</td>
</tr>
<tr class="even">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on a Google Ads ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
<td>CrossDeviceConversions</td>
</tr>
<tr class="odd">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
<td>Impressions</td>
</tr>
<tr class="even">
<td>metrics_interaction_event_types</td>
<td>The types of payable and free interactions.</td>
<td>InteractionTypes</td>
</tr>
<tr class="odd">
<td>metrics_interactions</td>
<td>The number of interactions. An interaction is the main user action associated with an ad format, such as clicks for text and shopping ads or views for video ads.</td>
<td>Interactions</td>
</tr>
<tr class="even">
<td>metrics_view_through_conversions</td>
<td>The total number of view-through conversions. These happen when a customer sees an image or rich media ad, then later completes a conversion on your site without interacting with (for example, clicking on) another ad.</td>
<td>ViewThroughConversions</td>
</tr>
<tr class="odd">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="odd">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
</tbody>
</table>

Google Ads Table Name: AgeRangeConversionStats

Google Ads API Resource: [age\_range\_view](https://developers.google.com/google-ads/api/fields/v21/age_range_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_base_ad_group</td>
<td>For draft or experiment ad groups, this field is the resource name of the base ad group from which this ad group was created. If a draft or experiment ad group does not have a base ad group, then this field is null. For base ad groups, this field equals the ad group resource name. This field is read-only.</td>
<td>BaseAdGroupId</td>
</tr>
<tr class="even">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion. This field is ignored for mutates.</td>
<td>CriterionId</td>
</tr>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="even">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td>BaseCampaignId</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>AllConversions</td>
</tr>
<tr class="even">
<td>metrics_all_conversions_value</td>
<td>The total value of all conversions.</td>
<td>AllConversionValue</td>
</tr>
<tr class="odd">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>Conversions</td>
</tr>
<tr class="even">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="odd">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on a Google Ads ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
<td>CrossDeviceConversions</td>
</tr>
<tr class="even">
<td>metrics_value_per_all_conversions</td>
<td>The value of all conversions divided by the number of all conversions.</td>
<td>ValuePerAllConversion</td>
</tr>
<tr class="odd">
<td>metrics_value_per_conversion</td>
<td>The value of conversions divided by the number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ValuePerConversion</td>
</tr>
<tr class="even">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="odd">
<td>segments_click_type</td>
<td>Click type.</td>
<td>ClickType</td>
</tr>
<tr class="even">
<td>segments_conversion_action</td>
<td>Resource name of the conversion action.</td>
<td>ConversionTrackerId</td>
</tr>
<tr class="odd">
<td>segments_conversion_action_category</td>
<td>Conversion action category.</td>
<td>ConversionCategoryName</td>
</tr>
<tr class="even">
<td>segments_conversion_action_name</td>
<td>Conversion action name.</td>
<td>ConversionTypeName</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="even">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="odd">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
<tr class="even">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="odd">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="even">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="odd">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: AgeRangeNonClickStats

Google Ads API Resource: [age\_range\_view](https://developers.google.com/google-ads/api/fields/v21/age_range_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_base_ad_group</td>
<td>For draft or experiment ad groups, this field is the resource name of the base ad group from which this ad group was created. If a draft or experiment ad group does not have a base ad group, then this field is null. For base ad groups, this field equals the ad group resource name. This field is read-only.</td>
<td>BaseAdGroupId</td>
</tr>
<tr class="even">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion. This field is ignored for mutates.</td>
<td>CriterionId</td>
</tr>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="even">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td>BaseCampaignId</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="odd">
<td>metrics_average_cpe</td>
<td>The average amount that you've been charged for an ad engagement. This amount is the total cost of all ad engagements divided by the total number of ad engagements.</td>
<td>AverageCpe</td>
</tr>
<tr class="even">
<td>metrics_average_cpv</td>
<td>The average amount you pay each time someone views your ad. The average CPV is defined by the total cost of all ad views divided by the number of views.</td>
<td>AverageCpv</td>
</tr>
<tr class="odd">
<td>metrics_engagement_rate</td>
<td>How often people engage with your ad after it's shown to them. This is the number of ad expansions divided by the number of times your ad is shown.</td>
<td>EngagementRate</td>
</tr>
<tr class="even">
<td>metrics_engagements</td>
<td>The number of engagements. An engagement occurs when a viewer expands your Lightbox ad. Also, in the future, other ad types may support engagement metrics.</td>
<td>Engagements</td>
</tr>
<tr class="odd">
<td>metrics_video_quartile_p100_rate</td>
<td>Percentage of impressions where the viewer watched all of your video.</td>
<td>VideoQuartile100Rate</td>
</tr>
<tr class="even">
<td>metrics_video_quartile_p25_rate</td>
<td>Percentage of impressions where the viewer watched 25% of your video.</td>
<td>VideoQuartile25Rate</td>
</tr>
<tr class="odd">
<td>metrics_video_quartile_p50_rate</td>
<td>Percentage of impressions where the viewer watched 50% of your video.</td>
<td>VideoQuartile50Rate</td>
</tr>
<tr class="even">
<td>metrics_video_quartile_p75_rate</td>
<td>Percentage of impressions where the viewer watched 75% of your video.</td>
<td>VideoQuartile75Rate</td>
</tr>
<tr class="odd">
<td>metrics_video_view_rate</td>
<td>The number of views your TrueView video ad receives divided by its number of impressions, including thumbnail impressions for TrueView in-display ads.</td>
<td>VideoViewRate</td>
</tr>
<tr class="even">
<td>metrics_video_views</td>
<td>The number of times your video ads were viewed.</td>
<td>VideoViews</td>
</tr>
<tr class="odd">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="odd">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="even">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
<tr class="odd">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="even">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="odd">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="even">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: AgeRangeStats

Google Ads API Resource: [age\_range\_view](https://developers.google.com/google-ads/api/fields/v21/age_range_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_base_ad_group</td>
<td>For draft or experiment ad groups, this field is the resource name of the base ad group from which this ad group was created. If a draft or experiment ad group does not have a base ad group, then this field is null. For base ad groups, this field equals the ad group resource name. This field is read-only.</td>
<td>BaseAdGroupId</td>
</tr>
<tr class="even">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion. This field is ignored for mutates.</td>
<td>CriterionId</td>
</tr>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="even">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td>BaseCampaignId</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="odd">
<td>metrics_active_view_cpm</td>
<td>Average cost of viewable impressions (`active_view_impressions`).</td>
<td>ActiveViewCpm</td>
</tr>
<tr class="even">
<td>metrics_active_view_ctr</td>
<td>Active view measurable clicks divided by active view viewable impressions. This metric is reported only for display network.</td>
<td>ActiveViewCtr</td>
</tr>
<tr class="odd">
<td>metrics_active_view_impressions</td>
<td>A measurement of how often your ad has become viewable on a Display Network site.</td>
<td>ActiveViewImpressions</td>
</tr>
<tr class="even">
<td>metrics_active_view_measurability</td>
<td>The ratio of impressions that could be measured by Active View over the number of served impressions.</td>
<td>ActiveViewMeasurability</td>
</tr>
<tr class="odd">
<td>metrics_active_view_measurable_cost_micros</td>
<td>The cost of the impressions you received that were measurable by Active View.</td>
<td>ActiveViewMeasurableCost</td>
</tr>
<tr class="even">
<td>metrics_active_view_measurable_impressions</td>
<td>The number of times your ads are appearing on placements in positions where they can be seen.</td>
<td>ActiveViewMeasurableImpressions</td>
</tr>
<tr class="odd">
<td>metrics_active_view_viewability</td>
<td>The percentage of time when your ad appeared on an Active View enabled site (measurable impressions) and was viewable (viewable impressions).</td>
<td>ActiveViewViewability</td>
</tr>
<tr class="even">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>AllConversions</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions_from_interactions_rate</td>
<td>All conversions from interactions (as oppose to view through conversions) divided by the number of ad interactions.</td>
<td>AllConversionRate</td>
</tr>
<tr class="even">
<td>metrics_all_conversions_value</td>
<td>The total value of all conversions.</td>
<td>AllConversionValue</td>
</tr>
<tr class="odd">
<td>metrics_average_cost</td>
<td>The average amount you pay per interaction. This amount is the total cost of your ads divided by the total number of interactions.</td>
<td>AverageCost</td>
</tr>
<tr class="even">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
<td>AverageCpc</td>
</tr>
<tr class="odd">
<td>metrics_average_cpm</td>
<td>Average cost-per-thousand impressions (CPM).</td>
<td>AverageCpm</td>
</tr>
<tr class="even">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
<td>Clicks</td>
</tr>
<tr class="odd">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>Conversions</td>
</tr>
<tr class="even">
<td>metrics_conversions_from_interactions_rate</td>
<td>Conversions from interactions divided by the number of ad interactions (such as clicks for text ads or views for video ads). This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionRate</td>
</tr>
<tr class="odd">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="even">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
<td>Cost</td>
</tr>
<tr class="odd">
<td>metrics_cost_per_all_conversions</td>
<td>The cost of ad interactions divided by all conversions.</td>
<td>CostPerAllConversion</td>
</tr>
<tr class="even">
<td>metrics_cost_per_conversion</td>
<td>The cost of ad interactions divided by conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>CostPerConversion</td>
</tr>
<tr class="odd">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on a Google Ads ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
<td>CrossDeviceConversions</td>
</tr>
<tr class="even">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
<td>Ctr</td>
</tr>
<tr class="odd">
<td>metrics_gmail_forwards</td>
<td>The number of times the ad was forwarded to someone else as a message.</td>
<td>GmailForwards</td>
</tr>
<tr class="even">
<td>metrics_gmail_saves</td>
<td>The number of times someone has saved your Gmail ad to their inbox as a message.</td>
<td>GmailSaves</td>
</tr>
<tr class="odd">
<td>metrics_gmail_secondary_clicks</td>
<td>The number of clicks to the landing page on the expanded state of Gmail ads.</td>
<td>GmailSecondaryClicks</td>
</tr>
<tr class="even">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
<td>Impressions</td>
</tr>
<tr class="odd">
<td>metrics_interaction_event_types</td>
<td>The types of payable and free interactions.</td>
<td>InteractionTypes</td>
</tr>
<tr class="even">
<td>metrics_interaction_rate</td>
<td>How often people interact with your ad after it is shown to them. This is the number of interactions divided by the number of times your ad is shown.</td>
<td>InteractionRate</td>
</tr>
<tr class="odd">
<td>metrics_interactions</td>
<td>The number of interactions. An interaction is the main user action associated with an ad format, such as clicks for text and shopping ads, or views for video ads.</td>
<td>Interactions</td>
</tr>
<tr class="even">
<td>metrics_value_per_all_conversions</td>
<td>The value of all conversions divided by the number of all conversions.</td>
<td>ValuePerAllConversion</td>
</tr>
<tr class="odd">
<td>metrics_value_per_conversion</td>
<td>The value of conversions divided by the number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ValuePerConversion</td>
</tr>
<tr class="even">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="odd">
<td>segments_click_type</td>
<td>Click type.</td>
<td>ClickType</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="odd">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="even">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
<tr class="odd">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="even">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="odd">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="even">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: Asset

Google Ads API Resource: [asset](https://developers.google.com/google-ads/api/fields/v21/asset)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>asset_final_urls</td>
<td>Output only. Type of the asset.</td>
<td></td>
</tr>
<tr class="even">
<td>asset_name</td>
<td>Optional name of the asset.</td>
<td></td>
</tr>
<tr class="odd">
<td>asset_source</td>
<td>Output only. Source of the asset.</td>
<td></td>
</tr>
<tr class="even">
<td>asset_type</td>
<td>A list of possible final URLs after all cross domain redirects.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_conversion_action</td>
<td>Resource name of the conversion action.</td>
<td></td>
</tr>
</tbody>
</table>

Google Ads Table Name: AssetGroup

Google Ads API Resource: [asset\_group](https://developers.google.com/google-ads/api/fields/v21/asset_group)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>asset_group_campaign</td>
<td>Immutable. The campaign with which this asset group is associated. The asset which is linked to the asset group.</td>
<td></td>
</tr>
<tr class="even">
<td>asset_group_final_mobile_urls</td>
<td>A list of final mobile URLs after all cross domain redirects. In performance max, by default, the urls are eligible for expansion unless opted out.</td>
<td></td>
</tr>
<tr class="odd">
<td>asset_group_final_urls</td>
<td>A list of final URLs after all cross domain redirects. In performance max, by default, the urls are eligible for expansion unless opted out.</td>
<td></td>
</tr>
<tr class="even">
<td>asset_group_id</td>
<td>Output only. The ID of the asset group.</td>
<td></td>
</tr>
<tr class="odd">
<td>asset_group_name</td>
<td>Required. Name of the asset group. Required. It must have a minimum length of 1 and maximum length of 128. It must be unique under a campaign.</td>
<td></td>
</tr>
<tr class="even">
<td>asset_group_status</td>
<td>The status of the asset group.</td>
<td></td>
</tr>
</tbody>
</table>

Google Ads Table Name: AssetGroupAsset

Google Ads API Resource: [asset\_group\_asset](https://developers.google.com/google-ads/api/fields/v21/asset_group_asset)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>asset_group_asset_asset</td>
<td>The asset which this asset group asset is linking.</td>
<td></td>
</tr>
<tr class="even">
<td>asset_group_asset_asset_group</td>
<td>The asset group which this asset group asset is linking.</td>
<td></td>
</tr>
<tr class="odd">
<td>asset_group_asset_field_type</td>
<td>The description of the placement of the asset within the asset group. For example: HEADLINE, YOUTUBE_VIDEO.</td>
<td></td>
</tr>
<tr class="even">
<td>asset_group_asset_performance_label</td>
<td>The performance of this asset group asset.</td>
<td></td>
</tr>
<tr class="odd">
<td>asset_group_asset_policy_summary_approval_status</td>
<td>The overall approval status, which is calculated based on the status of its individual policy topic entries.</td>
<td></td>
</tr>
<tr class="even">
<td>asset_group_asset_policy_summary_policy_topic_entries</td>
<td>The list of policy findings.</td>
<td></td>
</tr>
<tr class="odd">
<td>asset_group_asset_policy_summary_review_status</td>
<td>Where in the review process the resource is.</td>
<td></td>
</tr>
</tbody>
</table>

Google Ads Table Name: AssetGroupListingGroupFilter

Google Ads API Resource: [asset\_group\_listing\_group\_filter](https://developers.google.com/google-ads/api/fields/v21/asset_group_listing_group_filter)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>asset_group_listing_group_filter_asset_group</td>
<td>The asset group which this asset group listing group filter is part of.</td>
<td></td>
</tr>
<tr class="even">
<td>asset_group_listing_group_filter_case_value_product_bidding_category_id (obsolete - use asset_group_listing_group_filter_case_value_product_category_category_id instead)</td>
<td>ID of the product bidding category. This ID is equivalent to the google_product_category ID as described in this document: https://support.google.com/merchants/answer/6324436</td>
<td></td>
</tr>
<tr class="odd">
<td>asset_group_listing_group_filter_case_value_product_bidding_category_level (obsolete - use asset_group_listing_group_filter_case_value_product_category_level instead)</td>
<td>Indicates the level of the category in the taxonomy.</td>
<td></td>
</tr>
<tr class="even">
<td>asset_group_listing_group_filter_case_value_product_brand_value</td>
<td>String value of the product brand.</td>
<td></td>
</tr>
<tr class="odd">
<td>asset_group_listing_group_filter_case_value_product_channel_channel</td>
<td>Value of the locality.</td>
<td></td>
</tr>
<tr class="even">
<td>asset_group_listing_group_filter_case_value_product_condition_condition</td>
<td>Value of the condition.</td>
<td></td>
</tr>
<tr class="odd">
<td>asset_group_listing_group_filter_case_value_product_custom_attribute_index</td>
<td>Indicates the index of the custom attribute.</td>
<td></td>
</tr>
<tr class="even">
<td>asset_group_listing_group_filter_case_value_product_custom_attribute_value</td>
<td>String value of the product custom attribute.</td>
<td></td>
</tr>
<tr class="odd">
<td>asset_group_listing_group_filter_case_value_product_item_id_value</td>
<td>Value of the id.</td>
<td></td>
</tr>
<tr class="even">
<td>asset_group_listing_group_filter_case_value_product_type_level</td>
<td>Level of the type.</td>
<td></td>
</tr>
<tr class="odd">
<td>asset_group_listing_group_filter_case_value_product_type_value</td>
<td>Value of the type.</td>
<td></td>
</tr>
<tr class="even">
<td>asset_group_listing_group_filter_id</td>
<td>The ID of the ListingGroupFilter.</td>
<td></td>
</tr>
<tr class="odd">
<td>asset_group_listing_group_filter_parent_listing_group_filter</td>
<td>Resource name of the parent listing group subdivision. Null for the root listing group filter node.</td>
<td></td>
</tr>
<tr class="even">
<td>asset_group_listing_group_filter_type</td>
<td>Type of a listing group filter node.</td>
<td></td>
</tr>
<tr class="odd">
<td>asset_group_listing_group_filter_vertical (obsolete - use asset_group_listing_group_filter_listing_source instead)</td>
<td>The vertical the current node tree represents. All nodes in the same tree must belong to the same vertical.</td>
<td></td>
</tr>
</tbody>
</table>

Google Ads Table Name: AssetGroupProductGroupStats

Google Ads API Resource: [asset\_group\_product\_group\_view](https://developers.google.com/google-ads/api/fields/v21/asset_group_product_group_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>asset_group_product_group_view_asset_group</td>
<td>The asset group associated with the listing group filter.</td>
<td></td>
</tr>
<tr class="even">
<td>asset_group_product_group_view_asset_group_listing_group_filter</td>
<td>The resource name of the asset group listing group filter.</td>
<td></td>
</tr>
<tr class="odd">
<td>asset_group_product_group_view_resource_name</td>
<td>The resource name of the asset group product group view. Asset group product group view resource names have the form: customers/{customer_id}/assetGroupProductGroupViews/{asset_group_id}~{listing_group_filter_id}</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_average_cpm</td>
<td>Average cost-per-thousand impressions (CPM).</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies optimize for these conversions.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_conversions_from_interactions_rate</td>
<td>Conversions from interactions divided by the number of ad interactions (such as clicks for text ads or views for video ads). This only includes conversion actions which include_in_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies optimize for these conversions.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_conversions_value</td>
<td>The value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies optimize for these conversions.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_cost_per_conversion</td>
<td>The cost of ad interactions divided by conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies optimize for these conversions.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td></td>
</tr>
</tbody>
</table>

Google Ads Table Name: AssetGroupSignal

Google Ads API Resource: [asset\_group\_signal](https://developers.google.com/google-ads/api/fields/v21/asset_group_signal)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>asset_group_signal_asset_group</td>
<td>The asset group which this asset group signal belongs to.</td>
<td></td>
</tr>
<tr class="even">
<td>asset_group_signal_audience_audience</td>
<td>The Audience resource name.</td>
<td></td>
</tr>
<tr class="odd">
<td>asset_group_signal_resource_name</td>
<td>The resource name of the asset group signal. Asset group signal resource name have the form: customers/{customer_id}/assetGroupSignals/{asset_group_id}~{signal_id}</td>
<td></td>
</tr>
</tbody>
</table>

Google Ads Table Name: Audience

Google Ads API Resource: [audience](https://developers.google.com/google-ads/api/fields/v21/audience)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>audience_description</td>
<td>Description of this audience.</td>
<td></td>
</tr>
<tr class="even">
<td>audience_dimensions</td>
<td>Positive dimensions specifying the audience composition.</td>
<td></td>
</tr>
<tr class="odd">
<td>audience_exclusion_dimension</td>
<td>Negative dimension specifying the audience composition.</td>
<td></td>
</tr>
<tr class="even">
<td>audience_id</td>
<td>ID of the audience.</td>
<td></td>
</tr>
<tr class="odd">
<td>audience_name</td>
<td>Name of the audience. It should be unique across all audiences. It must have a minimum length of 1 and maximum length of 255.</td>
<td></td>
</tr>
<tr class="even">
<td>audience_status</td>
<td>Status of this audience. Indicates whether the audience is enabled or removed.</td>
<td></td>
</tr>
</tbody>
</table>

Google Ads Table Name: BidGoal

Google Ads API Resource: [bidding\_strategy](https://developers.google.com/google-ads/api/fields/v21/bidding_strategy)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>bidding_strategy_id</td>
<td>The ID of the bidding strategy.</td>
<td>BidStrategyID</td>
</tr>
<tr class="even">
<td>bidding_strategy_name</td>
<td>The name of the bidding strategy. All bidding strategies within an account must be named distinctly. The length of this string should be between 1 and 255, inclusive, in UTF-8 bytes, (trimmed).</td>
<td>Name</td>
</tr>
<tr class="odd">
<td>bidding_strategy_status</td>
<td>The status of the bidding strategy. This field is read-only.</td>
<td>Status</td>
</tr>
<tr class="even">
<td>bidding_strategy_target_cpa_cpc_bid_ceiling_micros</td>
<td>Maximum bid limit that can be set by the bid strategy. The limit applies to all keywords managed by the strategy.</td>
<td>TargetCpaMaxCpcBidCeiling</td>
</tr>
<tr class="odd">
<td>bidding_strategy_target_cpa_cpc_bid_floor_micros</td>
<td>Minimum bid limit that can be set by the bid strategy. The limit applies to all keywords managed by the strategy.</td>
<td>TargetCpaMaxCpcBidFloor</td>
</tr>
<tr class="even">
<td>bidding_strategy_target_cpa_target_cpa_micros</td>
<td>Average CPA target. This target should be greater than or equal to minimum billable unit based on the currency for the account.</td>
<td>TargetCpa</td>
</tr>
<tr class="odd">
<td>bidding_strategy_target_roas_cpc_bid_ceiling_micros</td>
<td>Maximum bid limit that can be set by the bid strategy. The limit applies to all keywords managed by the strategy.</td>
<td>TargetRoasBidCeiling</td>
</tr>
<tr class="even">
<td>bidding_strategy_target_roas_cpc_bid_floor_micros</td>
<td>Minimum bid limit that can be set by the bid strategy. The limit applies to all keywords managed by the strategy.</td>
<td>TargetRoasBidFloor</td>
</tr>
<tr class="odd">
<td>bidding_strategy_target_roas_target_roas</td>
<td>Required. The wanted revenue (based on conversion data) per unit of spend. Value must be between 0.01 and 1000.0, inclusive.</td>
<td>TargetRoas</td>
</tr>
<tr class="even">
<td>bidding_strategy_target_spend_cpc_bid_ceiling_micros</td>
<td>Maximum bid limit that can be set by the bid strategy. The limit applies to all keywords managed by the strategy.</td>
<td>TargetSpendBidCeiling</td>
</tr>
<tr class="odd">
<td>bidding_strategy_target_spend_target_spend_micros</td>
<td>The spend target under which to maximize clicks. A TargetSpend bidder attempts to spend the smaller of this value or the natural throttling spend amount. If not specified, the budget is used as the spend target.</td>
<td>TargetSpendSpendTarget</td>
</tr>
<tr class="even">
<td>bidding_strategy_type</td>
<td>The type of the bidding strategy. Create a bidding strategy by setting the bidding scheme. This field is read-only.</td>
<td>Type</td>
</tr>
<tr class="odd">
<td>customer_descriptive_name</td>
<td>Optional, non-unique descriptive name of the customer.</td>
<td>AccountDescriptiveName</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
</tbody>
</table>

Google Ads Table Name: BidGoalConversionStats

Google Ads API Resource: [bidding\_strategy](https://developers.google.com/google-ads/api/fields/v21/bidding_strategy)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>bidding_strategy_campaign_count</td>
<td>The number of campaigns attached to this bidding strategy. This field is read-only.</td>
<td>CampaignCount</td>
</tr>
<tr class="even">
<td>bidding_strategy_id</td>
<td>The ID of the bidding strategy.</td>
<td>BidStrategyID</td>
</tr>
<tr class="odd">
<td>bidding_strategy_non_removed_campaign_count</td>
<td>The number of non-removed campaigns attached to this bidding strategy. This field is read-only.</td>
<td>NonRemovedCampaignCount</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>AllConversions</td>
</tr>
<tr class="even">
<td>metrics_all_conversions_value</td>
<td>The total value of all conversions.</td>
<td>AllConversionValue</td>
</tr>
<tr class="odd">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>Conversions</td>
</tr>
<tr class="even">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="odd">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on a Google Ads ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
<td>CrossDeviceConversions</td>
</tr>
<tr class="even">
<td>metrics_value_per_all_conversions</td>
<td>The value of all conversions divided by the number of all conversions.</td>
<td>ValuePerAllConversion</td>
</tr>
<tr class="odd">
<td>metrics_view_through_conversions</td>
<td>The total number of view-through conversions. These happen when a customer sees an image or rich media ad, then later completes a conversion on your site without interacting with (for example, clicking on) another ad.</td>
<td>ViewThroughConversions</td>
</tr>
<tr class="even">
<td>segments_conversion_action</td>
<td>Resource name of the conversion action.</td>
<td>ConversionTrackerId</td>
</tr>
<tr class="odd">
<td>segments_conversion_action_category</td>
<td>Conversion action category.</td>
<td>ConversionCategoryName</td>
</tr>
<tr class="even">
<td>segments_conversion_action_name</td>
<td>Conversion action name.</td>
<td>ConversionTypeName</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="even">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="odd">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
<tr class="even">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="odd">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="even">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="odd">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: BidGoalStats

Google Ads API Resource: [bidding\_strategy](https://developers.google.com/google-ads/api/fields/v21/bidding_strategy)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>bidding_strategy_campaign_count</td>
<td>The number of campaigns attached to this bidding strategy. This field is read-only.</td>
<td>CampaignCount</td>
</tr>
<tr class="even">
<td>bidding_strategy_id</td>
<td>The ID of the bidding strategy.</td>
<td>BidStrategyID</td>
</tr>
<tr class="odd">
<td>bidding_strategy_non_removed_campaign_count</td>
<td>The number of non-removed campaigns attached to this bidding strategy. This field is read-only.</td>
<td>NonRemovedCampaignCount</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions_from_interactions_rate</td>
<td>All conversions from interactions (as oppose to view through conversions) divided by the number of ad interactions.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
<td>AverageCpc</td>
</tr>
<tr class="odd">
<td>metrics_average_cpm</td>
<td>Average cost-per-thousand impressions (CPM).</td>
<td>AverageCpm</td>
</tr>
<tr class="even">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
<td>Clicks</td>
</tr>
<tr class="odd">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>Conversions</td>
</tr>
<tr class="even">
<td>metrics_conversions_from_interactions_rate</td>
<td>Conversions from interactions divided by the number of ad interactions (such as clicks for text ads or views for video ads). This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionRate</td>
</tr>
<tr class="odd">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="even">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
<td>Cost</td>
</tr>
<tr class="odd">
<td>metrics_cost_per_all_conversions</td>
<td>The cost of ad interactions divided by all conversions.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_cost_per_conversion</td>
<td>The cost of ad interactions divided by conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>CostPerConversion</td>
</tr>
<tr class="odd">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
<td>Ctr</td>
</tr>
<tr class="even">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
<td>Impressions</td>
</tr>
<tr class="odd">
<td>metrics_value_per_conversion</td>
<td>The value of conversions divided by the number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ValuePerConversion</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="odd">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="even">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
<tr class="odd">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="even">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="odd">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="even">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: Budget

Google Ads API Resource: [campaign\_budget](https://developers.google.com/google-ads/api/fields/v21/campaign_budget)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>campaign_budget_amount_micros</td>
<td>The amount of the budget, in the local currency for the account. Amount is specified in micros, where one million is equivalent to one currency unit. Monthly spend is capped at 30.4 times this amount.</td>
<td>Amount</td>
</tr>
<tr class="even">
<td>campaign_budget_delivery_method</td>
<td>The delivery method that determines the rate at which the campaign budget is spent. Defaults to STANDARD if unspecified in a create operation.</td>
<td>DeliveryMethod</td>
</tr>
<tr class="odd">
<td>campaign_budget_explicitly_shared</td>
<td>Specifies whether the budget is explicitly shared. Defaults to true if unspecified in a create operation. If true, the budget was created with the purpose of sharing across one or more campaigns. If false, the budget was created with the intention of only being used with a single campaign. The budget's name and status stays in sync with the campaign's name and status. Attempting to share the budget with a second campaign results in an error. A non-shared budget can become an explicitly shared. The same operation must also assign the budget a name. A shared campaign budget can never become non-shared.</td>
<td>IsBudgetExplicitlyShared</td>
</tr>
<tr class="even">
<td>campaign_budget_has_recommended_budget</td>
<td>Indicates whether there is a recommended budget for this campaign budget. This field is read-only.</td>
<td>HasRecommendedBudget</td>
</tr>
<tr class="odd">
<td>campaign_budget_id</td>
<td>The ID of the campaign budget. A campaign budget is created using the CampaignBudgetService create operation and is assigned a budget ID. A budget ID can be shared across different campaigns; the system allocates the campaign budget among different campaigns to get optimum results.</td>
<td>BudgetId</td>
</tr>
<tr class="even">
<td>campaign_budget_name</td>
<td>The name of the campaign budget. When creating a campaign budget through CampaignBudgetService, every explicitly shared campaign budget must have a non-null, non-empty name. Campaign budgets that are not explicitly shared derive their name from the attached campaign's name. The length of this string must be between 1 and 255, inclusive, in UTF-8 bytes, (trimmed).</td>
<td>BudgetName</td>
</tr>
<tr class="odd">
<td>campaign_budget_period</td>
<td>Period over which to spend the budget. Defaults to DAILY if not specified.</td>
<td>Period</td>
</tr>
<tr class="even">
<td>campaign_budget_recommended_budget_amount_micros</td>
<td>The recommended budget amount. If no recommendation is available, this is set to the budget amount. Amount is specified in micros, where one million is equivalent to one currency unit. This field is read-only.</td>
<td>RecommendedBudgetAmount</td>
</tr>
<tr class="odd">
<td>campaign_budget_reference_count</td>
<td>The number of campaigns actively using the budget. This field is read-only.</td>
<td>BudgetReferenceCount</td>
</tr>
<tr class="even">
<td>campaign_budget_status</td>
<td>The status of this campaign budget. This field is read-only.</td>
<td>BudgetStatus</td>
</tr>
<tr class="odd">
<td>campaign_budget_total_amount_micros</td>
<td>The lifetime amount of the budget, in the local currency for the account. Amount is specified in micros, where one million is equivalent to one currency unit.</td>
<td>TotalAmount</td>
</tr>
<tr class="even">
<td>customer_descriptive_name</td>
<td>Optional, non-unique descriptive name of the customer.</td>
<td>AccountDescriptiveName</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
</tbody>
</table>

Google Ads Table Name: BudgetStats

Google Ads API Resource: [campaign\_budget](https://developers.google.com/google-ads/api/fields/v21/campaign_budget)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>campaign_budget_id</td>
<td>The ID of the campaign budget. A campaign budget is created using the CampaignBudgetService create operation and is assigned a budget ID. A budget ID can be shared across different campaigns; the system then allocates the campaign budget among different campaigns to get optimum results.</td>
<td>BudgetId</td>
</tr>
<tr class="even">
<td>campaign_budget_recommended_budget_estimated_change_weekly_clicks</td>
<td>The estimated change in weekly clicks if the recommended budget is applied. This field is read-only.</td>
<td>RecommendedBudgetEstimatedChangeInWeeklyClicks</td>
</tr>
<tr class="odd">
<td>campaign_budget_recommended_budget_estimated_change_weekly_cost_micros</td>
<td>The estimated change in weekly cost in micros if the recommended budget is applied. One million is equivalent to one currency unit. This field is read-only.</td>
<td>RecommendedBudgetEstimatedChangeInWeeklyCost</td>
</tr>
<tr class="even">
<td>campaign_budget_recommended_budget_estimated_change_weekly_interactions</td>
<td>The estimated change in weekly interactions if the recommended budget is applied. This field is read-only.</td>
<td>RecommendedBudgetEstimatedChangeInWeeklyInteractions</td>
</tr>
<tr class="odd">
<td>campaign_budget_recommended_budget_estimated_change_weekly_views</td>
<td>The estimated change in weekly views if the recommended budget is applied. This field is read-only.</td>
<td>RecommendedBudgetEstimatedChangeInWeeklyViews</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>AssociatedCampaignId</td>
</tr>
<tr class="odd">
<td>campaign_name</td>
<td>The name of the campaign. This field is required and shouldn't be empty when creating new campaigns. It must not contain any null (code point 0x0), NL line feed (code point 0xA) or carriage return (code point 0xD) characters.</td>
<td>AssociatedCampaignName</td>
</tr>
<tr class="even">
<td>campaign_status</td>
<td>The status of the campaign. When a new campaign is added, the status defaults to ENABLED.</td>
<td>AssociatedCampaignStatus</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="even">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>AllConversions</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions_from_interactions_rate</td>
<td>All conversions from interactions (as oppose to view through conversions) divided by the number of ad interactions.</td>
<td>AllConversionRate</td>
</tr>
<tr class="even">
<td>metrics_all_conversions_value</td>
<td>The total value of all conversions.</td>
<td>AllConversionValue</td>
</tr>
<tr class="odd">
<td>metrics_average_cost</td>
<td>The average amount you pay per interaction. This amount is the total cost of your ads divided by the total number of interactions.</td>
<td>AverageCost</td>
</tr>
<tr class="even">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
<td>AverageCpc</td>
</tr>
<tr class="odd">
<td>metrics_average_cpe</td>
<td>The average amount that you've been charged for an ad engagement. This amount is the total cost of all ad engagements divided by the total number of ad engagements.</td>
<td>AverageCpe</td>
</tr>
<tr class="even">
<td>metrics_average_cpm</td>
<td>Average cost-per-thousand impressions (CPM).</td>
<td>AverageCpm</td>
</tr>
<tr class="odd">
<td>metrics_average_cpv</td>
<td>The average amount you pay each time someone views your ad. The average CPV is defined by the total cost of all ad views divided by the number of views.</td>
<td>AverageCpv</td>
</tr>
<tr class="even">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
<td>Clicks</td>
</tr>
<tr class="odd">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>Conversions</td>
</tr>
<tr class="even">
<td>metrics_conversions_from_interactions_rate</td>
<td>Conversions from interactions divided by the number of ad interactions (such as clicks for text ads or views for video ads). This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionRate</td>
</tr>
<tr class="odd">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="even">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
<td>Cost</td>
</tr>
<tr class="odd">
<td>metrics_cost_per_all_conversions</td>
<td>The cost of ad interactions divided by all conversions.</td>
<td>CostPerAllConversion</td>
</tr>
<tr class="even">
<td>metrics_cost_per_conversion</td>
<td>The cost of ad interactions divided by conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>CostPerConversion</td>
</tr>
<tr class="odd">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on a Google Ads ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
<td>CrossDeviceConversions</td>
</tr>
<tr class="even">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
<td>Ctr</td>
</tr>
<tr class="odd">
<td>metrics_engagement_rate</td>
<td>How often people engage with your ad after it's shown to them. This is the number of ad expansions divided by the number of times your ad is shown.</td>
<td>EngagementRate</td>
</tr>
<tr class="even">
<td>metrics_engagements</td>
<td>The number of engagements. An engagement occurs when a viewer expands your Lightbox ad. Also, in the future, other ad types may support engagement metrics.</td>
<td>Engagements</td>
</tr>
<tr class="odd">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
<td>Impressions</td>
</tr>
<tr class="even">
<td>metrics_interaction_event_types</td>
<td>The types of payable and free interactions.</td>
<td>InteractionTypes</td>
</tr>
<tr class="odd">
<td>metrics_interaction_rate</td>
<td>How often people interact with your ad after it is shown to them. This is the number of interactions divided by the number of times your ad is shown.</td>
<td>InteractionRate</td>
</tr>
<tr class="even">
<td>metrics_interactions</td>
<td>The number of interactions. An interaction is the main user action associated with an ad format, such as clicks for text and shopping ads or views for video ads.</td>
<td>Interactions</td>
</tr>
<tr class="odd">
<td>metrics_value_per_all_conversions</td>
<td>The value of all conversions divided by the number of all conversions.</td>
<td>ValuePerAllConversion</td>
</tr>
<tr class="even">
<td>metrics_value_per_conversion</td>
<td>The value of conversions divided by the number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ValuePerConversion</td>
</tr>
<tr class="odd">
<td>metrics_video_view_rate</td>
<td>The number of views your TrueView video ad receives divided by its number of impressions, including thumbnail impressions for TrueView in-display ads.</td>
<td>VideoViewRate</td>
</tr>
<tr class="even">
<td>metrics_video_views</td>
<td>The number of times your video ads were viewed.</td>
<td>VideoViews</td>
</tr>
<tr class="odd">
<td>metrics_view_through_conversions</td>
<td>The total number of view-through conversions. These happen when a customer sees an image or rich media ad, then later completes a conversion on your site without interacting with (for example, clicking on) another ad.</td>
<td>ViewThroughConversions</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td></td>
</tr>
</tbody>
</table>

Google Ads Table Name: Campaign

Google Ads API Resource: [campaign](https://developers.google.com/google-ads/api/fields/v21/campaign)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>bidding_strategy_name</td>
<td>The name of the bidding strategy. All bidding strategies within an account must be named distinctly. The length of this string should be between 1 and 255, inclusive, in UTF-8 bytes, (trimmed).</td>
<td>BiddingStrategyName</td>
</tr>
<tr class="even">
<td>campaign_advertising_channel_sub_type</td>
<td>Optional refinement to `advertising_channel_type`. Must be a valid sub-type of the parent channel type. Can be set only when creating campaigns. After campaign is created, the field cannot be changed.</td>
<td>AdvertisingChannelSubType</td>
</tr>
<tr class="odd">
<td>campaign_advertising_channel_type</td>
<td>The primary serving target for ads within the campaign. The targeting options can be refined in `network_settings`. This field is required and shouldn't be empty when creating new campaigns. Can be set only when creating campaigns. After the campaign is created, the field cannot be changed.</td>
<td>AdvertisingChannelType</td>
</tr>
<tr class="even">
<td>campaign_bidding_strategy</td>
<td>Portfolio bidding strategy used by campaign.</td>
<td>BiddingStrategyId</td>
</tr>
<tr class="odd">
<td>campaign_bidding_strategy_type</td>
<td>The type of bidding strategy. A bidding strategy can be created by setting either the bidding scheme to create a standard bidding strategy or the `bidding_strategy` field to create a portfolio bidding strategy. This field is read-only.</td>
<td>BiddingStrategyType</td>
</tr>
<tr class="even">
<td>campaign_budget_amount_micros</td>
<td>The amount of the budget, in the local currency for the account. Amount is specified in micros, where one million is equivalent to one currency unit. Monthly spend is capped at 30.4 times this amount.</td>
<td>Amount</td>
</tr>
<tr class="odd">
<td>campaign_budget_explicitly_shared</td>
<td>Specifies whether the budget is explicitly shared. Defaults to true if unspecified in a create operation. If true, the budget was created with the purpose of sharing across one or more campaigns. If false, the budget was created with the intention of only being used with a single campaign. The budget's name and status stays in sync with the campaign's name and status. Attempting to share the budget with a second campaign results in an error. A non-shared budget can become an explicitly shared. The same operation must also assign the budget a name. A shared campaign budget can never become non-shared.</td>
<td>IsBudgetExplicitlyShared</td>
</tr>
<tr class="even">
<td>campaign_budget_has_recommended_budget</td>
<td>Indicates whether there is a recommended budget for this campaign budget. This field is read-only.</td>
<td>HasRecommendedBudget</td>
</tr>
<tr class="odd">
<td>campaign_budget_period</td>
<td>Period over which to spend the budget. Defaults to DAILY if not specified.</td>
<td>Period</td>
</tr>
<tr class="even">
<td>campaign_budget_recommended_budget_amount_micros</td>
<td>The recommended budget amount. If no recommendation is available, this is set to the budget amount. Amount is specified in micros, where one million is equivalent to one currency unit. This field is read-only.</td>
<td>RecommendedBudgetAmount</td>
</tr>
<tr class="odd">
<td>campaign_budget_total_amount_micros</td>
<td>The lifetime amount of the budget, in the local currency for the account. Amount is specified in micros, where one million is equivalent to one currency unit.</td>
<td>TotalAmount</td>
</tr>
<tr class="even">
<td>campaign_campaign_budget</td>
<td>The budget of the campaign.</td>
<td>BudgetId</td>
</tr>
<tr class="odd">
<td>campaign_end_date</td>
<td>The date when campaign ended. This field must not be used in WHERE clauses.</td>
<td>EndDate</td>
</tr>
<tr class="even">
<td>campaign_experiment_type</td>
<td>The type of campaign: normal, draft, or experiment.</td>
<td>CampaignTrialType</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="even">
<td>campaign_manual_cpc_enhanced_cpc_enabled</td>
<td>Whether bids are to be enhanced based on conversion optimizer data.</td>
<td>EnhancedCpcEnabled</td>
</tr>
<tr class="odd">
<td>campaign_maximize_conversion_value_target_roas</td>
<td>The target return on ad spend (ROAS) option. If set, the bid strategy maximizes revenue while averaging the target return on ad spend. If the target ROAS is high, the bid strategy may not be able to spend the full budget. If the target ROAS is not set, the bid strategy aims to achieve the highest possible ROAS for the budget.</td>
<td>MaximizeConversionValueTargetRoas</td>
</tr>
<tr class="even">
<td>campaign_name</td>
<td>The name of the campaign. This field is required and shouldn't be empty when creating new campaigns. It must not contain any null (code point 0x0), NL line feed (code point 0xA) or carriage return (code point 0xD) characters.</td>
<td>CampaignName</td>
</tr>
<tr class="odd">
<td>campaign_percent_cpc_enhanced_cpc_enabled</td>
<td>Adjusts the bid for each auction upward or downward, depending on the likelihood of a conversion. Individual bids may exceed cpc_bid_ceiling_micros, but the average bid amount for a campaign shouldn't.</td>
<td></td>
</tr>
<tr class="even">
<td>campaign_serving_status</td>
<td>The ad serving status of the campaign.</td>
<td>ServingStatus</td>
</tr>
<tr class="odd">
<td>campaign_start_date</td>
<td>The date when campaign started. This field must not be used in WHERE clauses.</td>
<td>StartDate</td>
</tr>
<tr class="even">
<td>campaign_status</td>
<td>The status of the campaign. When a new campaign is added, the status defaults to ENABLED.</td>
<td>CampaignStatus</td>
</tr>
<tr class="odd">
<td>campaign_tracking_url_template</td>
<td>The URL template for constructing a tracking URL.</td>
<td>TrackingUrlTemplate</td>
</tr>
<tr class="even">
<td>campaign_url_custom_parameters</td>
<td>The list of mappings used to substitute custom parameter tags in a `tracking_url_template`, `final_urls`, or `mobile_final_urls`.</td>
<td>UrlCustomParameters</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
</tbody>
</table>

Google Ads Table Name: CampaignAssetStats

Google Ads API Resource: [campaign\_asset](https://developers.google.com/google-ads/api/fields/v21/campaign_asset)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>campaign_asset_asset</td>
<td>The asset which is linked to the campaign.</td>
<td></td>
</tr>
<tr class="even">
<td>campaign_asset_campaign</td>
<td>The campaign to which the asset is linked.</td>
<td></td>
</tr>
<tr class="odd">
<td>campaign_asset_field_type</td>
<td>Role that the asset takes under the linked campaign.</td>
<td></td>
</tr>
<tr class="even">
<td>campaign_asset_resource_name</td>
<td>The resource name of the campaign asset. CampaignAsset resource names have the form: customers/{customer_id}/campaignAssets/{campaign_id}~{asset_id}~{field_type}</td>
<td></td>
</tr>
<tr class="odd">
<td>campaign_asset_source</td>
<td>Source of the campaign asset link.</td>
<td></td>
</tr>
<tr class="even">
<td>campaign_asset_status</td>
<td>Status of the campaign asset.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_average_cpe</td>
<td>The average amount that you've been charged for an ad engagement. This amount is the total cost of all ad engagements divided by the total number of ad engagements.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_average_cpm</td>
<td>Average cost-per-thousand impressions (CPM).</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_average_cpv</td>
<td>The average amount you pay each time someone views your ad. The average CPV is defined by the total cost of all ad views divided by the number of views.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies optimize for these conversions.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_conversions_from_interactions_rate</td>
<td>Conversions from interactions divided by the number of ad interactions (such as clicks for text ads or views for video ads). This only includes conversion actions which include_in_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies optimize for these conversions.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_conversions_value</td>
<td>The value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies optimize for these conversions.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_cost_per_conversion</td>
<td>The cost of ad interactions divided by conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true. If you use conversion-based bidding, your bid strategies optimize for these conversions.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_interactions</td>
<td>The number of interactions. An interaction is the main user action associated with an ad format, such as clicks for text and shopping ads or views for video ads.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_top_impression_percentage</td>
<td>The percent of your ad impressions that are shown as the very first ad above the organic search results.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td></td>
</tr>
</tbody>
</table>

Google Ads Table Name: CampaignAudience

Google Ads API Resource: [campaign\_audience\_view](https://developers.google.com/google-ads/api/fields/v21/campaign_audience_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td></td>
</tr>
<tr class="even">
<td>campaign_criterion_bid_modifier</td>
<td>Portfolio bidding strategy used by campaign.</td>
<td></td>
</tr>
<tr class="odd">
<td>campaign_criterion_criterion_id</td>
<td>Output only. The ID of the criterion. This field is ignored during mutate.</td>
<td></td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td></td>
</tr>
</tbody>
</table>

Google Ads Table Name: CampaignAudienceBasicStats

Google Ads API Resource: [campaign\_audience\_view](https://developers.google.com/google-ads/api/fields/v21/campaign_audience_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td></td>
</tr>
<tr class="even">
<td>campaign_criterion_criterion_id</td>
<td>Output only. The ID of the criterion. This field is ignored during mutate.</td>
<td></td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_interaction_event_types</td>
<td>The types of payable and free interactions.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_interactions</td>
<td>The number of interactions. An interaction is the main user action associated with an ad format, such as clicks for text and shopping ads or views for video ads.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_view_through_conversions</td>
<td>The total number of view-through conversions. These happen when a customer sees an image or rich media ad, then later completes a conversion on your site without interacting with (for example, clicking on) another ad.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_slot</td>
<td>Position of the ad.</td>
<td></td>
</tr>
</tbody>
</table>

Google Ads Table Name: CampaignAudienceConversionStats

Google Ads API Resource: [campaign\_audience\_view](https://developers.google.com/google-ads/api/fields/v21/campaign_audience_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td></td>
</tr>
<tr class="even">
<td>campaign_criterion_criterion_id</td>
<td>Output only. The ID of the criterion. This field is ignored during mutate.</td>
<td></td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_all_conversions_value</td>
<td>The total value of all conversions.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on a Google Ads ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_value_per_all_conversions</td>
<td>The value of all conversions divided by the number of all conversions.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_value_per_conversion</td>
<td>The value of conversions divided by the number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_view_through_conversions</td>
<td>The total number of view-through conversions. These happen when a customer sees an image or rich media ad, then later completes a conversion on your site without interacting with (for example, clicking on) another ad.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_conversion_action</td>
<td>Resource name of the conversion action.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_conversion_action_category</td>
<td>Conversion action category.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_conversion_action_name</td>
<td>Conversion action name.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td></td>
</tr>
</tbody>
</table>

Google Ads Table Name: CampaignAudienceNonClickStats

Google Ads API Resource: [campaign\_audience\_view](https://developers.google.com/google-ads/api/fields/v21/campaign_audience_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td></td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_average_cpe</td>
<td>The average amount that you've been charged for an ad engagement. This amount is the total cost of all ad engagements divided by the total number of ad engagements.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_average_cpv</td>
<td>The average amount you pay each time someone views your ad. The average CPV is defined by the total cost of all ad views divided by the number of views.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_engagement_rate</td>
<td>How often people engage with your ad after it's shown to them. This is the number of ad expansions divided by the number of times your ad is shown.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_engagements</td>
<td>The number of engagements. An engagement occurs when a viewer expands your Lightbox ad. Also, in the future, other ad types may support engagement metrics.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_video_view_rate</td>
<td>The number of views your TrueView video ad receives divided by its number of impressions, including thumbnail impressions for TrueView in-display ads.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_video_views</td>
<td>The number of times your video ads were viewed.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td></td>
</tr>
</tbody>
</table>

Google Ads Table Name: CampaignAudienceStats

Google Ads API Resource: [campaign\_audience\_view](https://developers.google.com/google-ads/api/fields/v21/campaign_audience_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td></td>
</tr>
<tr class="even">
<td>campaign_criterion_criterion_id</td>
<td>Output only. The ID of the criterion. This field is ignored during mutate.</td>
<td></td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_active_view_cpm</td>
<td>Average cost of viewable impressions (`active_view_impressions`).</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_active_view_ctr</td>
<td>Active view measurable clicks divided by active view viewable impressions. This metric is reported only for display network.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_active_view_impressions</td>
<td>A measurement of how often your ad has become viewable on a Display Network site.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_active_view_measurability</td>
<td>The ratio of impressions that could be measured by Active View over the number of served impressions.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_active_view_measurable_cost_micros</td>
<td>The cost of the impressions you received that were measurable by Active View.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_active_view_measurable_impressions</td>
<td>The number of times your ads are appearing on placements in positions where they can be seen.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_active_view_viewability</td>
<td>The percentage of time when your ad appeared on an Active View enabled site (measurable impressions) and was viewable (viewable impressions).</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_all_conversions_from_interactions_rate</td>
<td>All conversions from interactions (as oppose to view through conversions) divided by the number of ad interactions.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_average_cost</td>
<td>The average amount you pay per interaction. This amount is the total cost of your ads divided by the total number of interactions.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_average_cpm</td>
<td>Average cost-per-thousand impressions (CPM).</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_conversions_from_interactions_rate</td>
<td>Conversions from interactions divided by the number of ad interactions (such as clicks for text ads or views for video ads). This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_cost_per_all_conversions</td>
<td>The cost of ad interactions divided by all conversions.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_cost_per_conversion</td>
<td>The cost of ad interactions divided by conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_gmail_forwards</td>
<td>The number of times the ad was forwarded to someone else as a message.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_gmail_saves</td>
<td>The number of times someone has saved your Gmail ad to their inbox as a message.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_gmail_secondary_clicks</td>
<td>The number of clicks to the landing page on the expanded state of Gmail ads.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_interaction_event_types</td>
<td>The types of payable and free interactions.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_interaction_rate</td>
<td>How often people interact with your ad after it is shown to them. This is the number of interactions divided by the number of times your ad is shown.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_interactions</td>
<td>The number of interactions. An interaction is the main user action associated with an ad format, such as clicks for text and shopping ads or views for video ads.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_value_per_conversion</td>
<td>The value of conversions divided by the number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_click_type</td>
<td>Click type.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td></td>
</tr>
</tbody>
</table>

Google Ads Table Name: CampaignBasicStats

Google Ads API Resource: [campaign](https://developers.google.com/google-ads/api/fields/v21/campaign)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td>BaseCampaignId</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="even">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
<td>Clicks</td>
</tr>
<tr class="odd">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>Conversions</td>
</tr>
<tr class="even">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="odd">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
<td>Cost</td>
</tr>
<tr class="even">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
<td>Impressions</td>
</tr>
<tr class="odd">
<td>metrics_interaction_event_types</td>
<td>The types of payable and free interactions.</td>
<td>InteractionTypes</td>
</tr>
<tr class="even">
<td>metrics_interactions</td>
<td>The number of interactions. An interaction is the main user action associated with an ad format, such as clicks for text and shopping ads or views for video ads.</td>
<td>Interactions</td>
</tr>
<tr class="odd">
<td>metrics_view_through_conversions</td>
<td>The total number of view-through conversions. These happen when a customer sees an image or rich media ad, then later completes a conversion on your site without interacting with (for example, clicking on) another ad.</td>
<td>ViewThroughConversions</td>
</tr>
<tr class="even">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="even">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
<tr class="odd">
<td>segments_slot</td>
<td>Position of the ad.</td>
<td>Slot</td>
</tr>
</tbody>
</table>

Google Ads Table Name: CampaignConversionStats

Google Ads API Resource: [campaign](https://developers.google.com/google-ads/api/fields/v21/campaign)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td>BaseCampaignId</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="even">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>Conversions</td>
</tr>
<tr class="odd">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="even">
<td>metrics_value_per_conversion</td>
<td>The value of conversions divided by the number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ValuePerConversion</td>
</tr>
<tr class="odd">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="even">
<td>segments_conversion_action</td>
<td>Resource name of the conversion action.</td>
<td>ConversionTrackerId</td>
</tr>
<tr class="odd">
<td>segments_conversion_action_category</td>
<td>Conversion action category.</td>
<td>ConversionCategoryName</td>
</tr>
<tr class="even">
<td>segments_conversion_action_name</td>
<td>Conversion action name.</td>
<td>ConversionTypeName</td>
</tr>
<tr class="odd">
<td>segments_conversion_attribution_event_type</td>
<td>Conversion attribution event type.</td>
<td>ConversionAttributionEventType</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="odd">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="even">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="odd">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="even">
<td>segments_slot</td>
<td>Position of the ad.</td>
<td>Slot</td>
</tr>
<tr class="odd">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="even">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: CampaignCookieStats

Google Ads API Resource: [campaign](https://developers.google.com/google-ads/api/fields/v21/campaign)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td>BaseCampaignId</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="even">
<td>metrics_absolute_top_impression_percentage</td>
<td>The percent of your ad impressions that are shown as the very first ad above the organic search results.</td>
<td>AbsoluteTopImpressionPercentage</td>
</tr>
<tr class="odd">
<td>metrics_search_budget_lost_absolute_top_impression_share</td>
<td>The number estimating how often your ad wasn't the very first ad above the organic search results due to a low budget. Note: Search budget lost absolute top impression share is reported in the range of 0 to 0.9. Any value above 0.9 is reported as 0.9001.</td>
<td>SearchBudgetLostAbsoluteTopImpressionShare</td>
</tr>
<tr class="even">
<td>metrics_search_budget_lost_top_impression_share</td>
<td>The number estimating how often your ad didn't show anywhere above the organic search results due to a low budget. Note: Search budget lost top impression share is reported in the range of 0 to 0.9. Any value above 0.9 is reported as 0.9001.</td>
<td>SearchBudgetLostTopImpressionShare</td>
</tr>
<tr class="odd">
<td>metrics_search_rank_lost_absolute_top_impression_share</td>
<td>The number estimating how often your ad wasn't the very first ad above the organic search results due to poor Ad Rank. Note: Search rank lost absolute top impression share is reported in the range of 0 to 0.9. Any value above 0.9 is reported as 0.9001.</td>
<td>SearchRankLostAbsoluteTopImpressionShare</td>
</tr>
<tr class="even">
<td>metrics_search_rank_lost_top_impression_share</td>
<td>The number estimating how often your ad didn't show anywhere above the organic search results due to poor Ad Rank. Note: Search rank lost top impression share is reported in the range of 0 to 0.9. Any value above 0.9 is reported as 0.9001.</td>
<td>SearchRankLostTopImpressionShare</td>
</tr>
<tr class="odd">
<td>metrics_search_top_impression_share</td>
<td>The impressions you've received in the top location (anywhere above the organic search results) compared to the estimated number of impressions you were eligible to receive in the top location. Note: Search top impression share is reported in the range of 0.1 to 1. Any value below 0.1 is reported as 0.0999.</td>
<td>SearchTopImpressionShare</td>
</tr>
<tr class="even">
<td>metrics_top_impression_percentage</td>
<td>The percent of your ad impressions that are shown anywhere above the organic search results.</td>
<td>TopImpressionPercentage</td>
</tr>
<tr class="odd">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="odd">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="even">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
</tbody>
</table>

Google Ads Table Name: CampaignCriterion

Google Ads API Resource: [campaign\_criterion](https://developers.google.com/google-ads/api/fields/v21/campaign_criterion)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>campaign_criterion_bid_modifier</td>
<td>The modifier for the bids when the criterion matches. The modifier must be in the range: 0.1 - 10.0. Most targetable criteria types support modifiers. Use 0 to opt out of a Device type.</td>
<td></td>
</tr>
<tr class="even">
<td>campaign_criterion_campaign</td>
<td>The campaign to which the criterion belongs.</td>
<td></td>
</tr>
<tr class="odd">
<td>campaign_criterion_criterion_id</td>
<td>The ID of the criterion. This field is ignored during mutate.</td>
<td></td>
</tr>
<tr class="even">
<td>campaign_criterion_device_type</td>
<td>Type of the device.</td>
<td></td>
</tr>
<tr class="odd">
<td>campaign_criterion_display_name</td>
<td>The display name of the criterion. This field is ignored for mutates.</td>
<td></td>
</tr>
<tr class="even">
<td>campaign_criterion_negative</td>
<td>Whether to target (`false`) or exclude (`true`) the criterion.</td>
<td></td>
</tr>
<tr class="odd">
<td>campaign_criterion_status</td>
<td>The status of the criterion.</td>
<td></td>
</tr>
<tr class="even">
<td>campaign_criterion_type</td>
<td>The type of the criterion.</td>
<td></td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td></td>
</tr>
<tr class="even">
<td>campaign_name</td>
<td>The name of the campaign. This field is required and shouldn't be empty when creating new campaigns. It must not contain any null (code point 0x0), NL line feed (code point 0xA) or carriage return (code point 0xD) characters.</td>
<td></td>
</tr>
</tbody>
</table>

Google Ads Table Name: CampaignCrossDeviceConversionStats

Google Ads API Resource: [campaign](https://developers.google.com/google-ads/api/fields/v21/campaign)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td>BaseCampaignId</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="even">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>AllConversions</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions_value</td>
<td>The total value of all conversions.</td>
<td>AllConversionValue</td>
</tr>
<tr class="even">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on a Google Ads ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
<td>CrossDeviceConversions</td>
</tr>
<tr class="odd">
<td>metrics_value_per_all_conversions</td>
<td>The value of all conversions divided by the number of all conversions.</td>
<td>ValuePerAllConversion</td>
</tr>
<tr class="even">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="odd">
<td>segments_conversion_action</td>
<td>Resource name of the conversion action.</td>
<td>ConversionTrackerId</td>
</tr>
<tr class="even">
<td>segments_conversion_action_category</td>
<td>Conversion action category.</td>
<td>ConversionCategoryName</td>
</tr>
<tr class="odd">
<td>segments_conversion_action_name</td>
<td>Conversion action name.</td>
<td>ConversionTypeName</td>
</tr>
<tr class="even">
<td>segments_conversion_attribution_event_type</td>
<td>Conversion attribution event type.</td>
<td>ConversionAttributionEventType</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="even">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="odd">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="even">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="odd">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="even">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: CampaignCrossDeviceStats

Google Ads API Resource: [campaign](https://developers.google.com/google-ads/api/fields/v21/campaign)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td>BaseCampaignId</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="even">
<td>metrics_absolute_top_impression_percentage</td>
<td>The percent of your ad impressions that are shown as the very first ad above the organic search results.</td>
<td>AbsoluteTopImpressionPercentage</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>AllConversions</td>
</tr>
<tr class="even">
<td>metrics_all_conversions_from_interactions_rate</td>
<td>All conversions from interactions (as oppose to view through conversions) divided by the number of ad interactions.</td>
<td>AllConversionRate</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions_value</td>
<td>The total value of all conversions.</td>
<td>AllConversionValue</td>
</tr>
<tr class="even">
<td>metrics_average_cpe</td>
<td>The average amount that you've been charged for an ad engagement. This amount is the total cost of all ad engagements divided by the total number of ad engagements.</td>
<td>AverageCpe</td>
</tr>
<tr class="odd">
<td>metrics_average_cpv</td>
<td>The average amount you pay each time someone views your ad. The average CPV is defined by the total cost of all ad views divided by the number of views.</td>
<td>AverageCpv</td>
</tr>
<tr class="even">
<td>metrics_average_page_views</td>
<td>Average number of pages viewed per session.</td>
<td>AveragePageviews</td>
</tr>
<tr class="odd">
<td>metrics_average_time_on_site</td>
<td>Total duration of all sessions (in seconds) / number of sessions. Imported from Google Analytics.</td>
<td>AverageTimeOnSite</td>
</tr>
<tr class="even">
<td>metrics_bounce_rate</td>
<td>Percentage of clicks where the user only visited a single page on your site. Imported from Google Analytics.</td>
<td>BounceRate</td>
</tr>
<tr class="odd">
<td>metrics_content_budget_lost_impression_share</td>
<td>The estimated percent of times that your ad was eligible to show on the Display Network but didn't because your budget was too low. Note: Content budget lost impression share is reported in the range of 0 to 0.9. Any value above 0.9 is reported as 0.9001.</td>
<td>ContentBudgetLostImpressionShare</td>
</tr>
<tr class="even">
<td>metrics_content_impression_share</td>
<td>The impressions you've received on the Display Network divided by the estimated number of impressions you were eligible to receive. Note: Content impression share is reported in the range of 0.1 to 1. Any value below 0.1 is reported as 0.0999.</td>
<td>ContentImpressionShare</td>
</tr>
<tr class="odd">
<td>metrics_content_rank_lost_impression_share</td>
<td>The estimated percentage of impressions on the Display Network that your ads didn't receive due to poor Ad Rank. Note: Content rank lost impression share is reported in the range of 0 to 0.9. Any value above 0.9 is reported as 0.9001.</td>
<td>ContentRankLostImpressionShare</td>
</tr>
<tr class="even">
<td>metrics_cost_per_all_conversions</td>
<td>The cost of ad interactions divided by all conversions.</td>
<td>CostPerAllConversion</td>
</tr>
<tr class="odd">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on a Google Ads ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
<td>CrossDeviceConversions</td>
</tr>
<tr class="even">
<td>metrics_engagement_rate</td>
<td>How often people engage with your ad after it's shown to them. This is the number of ad expansions divided by the number of times your ad is shown.</td>
<td>EngagementRate</td>
</tr>
<tr class="odd">
<td>metrics_engagements</td>
<td>The number of engagements. An engagement occurs when a viewer expands your Lightbox ad. Also, in the future, other ad types may support engagement metrics.</td>
<td>Engagements</td>
</tr>
<tr class="even">
<td>metrics_invalid_click_rate</td>
<td>The percentage of clicks filtered out of your total number of clicks (filtered + non-filtered clicks) during the reporting period.</td>
<td>InvalidClickRate</td>
</tr>
<tr class="odd">
<td>metrics_invalid_clicks</td>
<td>Number of clicks Google considers illegitimate and doesn't charge you for.</td>
<td>InvalidClicks</td>
</tr>
<tr class="even">
<td>metrics_percent_new_visitors</td>
<td>Percentage of first-time sessions (from people who had never visited your site before). Imported from Google Analytics.</td>
<td>PercentNewVisitors</td>
</tr>
<tr class="odd">
<td>metrics_phone_calls</td>
<td>Number of offline phone calls.</td>
<td>NumOfflineInteractions</td>
</tr>
<tr class="even">
<td>metrics_phone_impressions</td>
<td>Number of offline phone impressions.</td>
<td>NumOfflineImpressions</td>
</tr>
<tr class="odd">
<td>metrics_phone_through_rate</td>
<td>Number of phone calls received (phone_calls) divided by the number of times your phone number is shown (phone_impressions).</td>
<td>OfflineInteractionRate</td>
</tr>
<tr class="even">
<td>metrics_relative_ctr</td>
<td>Your clickthrough rate (Ctr) divided by the average clickthrough rate of all advertisers on the websites that show your ads. Measures how your ads perform on Display Network sites compared to other ads on the same sites.</td>
<td>RelativeCtr</td>
</tr>
<tr class="odd">
<td>metrics_search_absolute_top_impression_share</td>
<td>The percentage of the customer's Shopping or Search ad impressions that are shown in the most prominent Shopping position. See https://support.google.com/google-ads/answer/7501826 for details. Any value below 0.1 is reported as 0.0999.</td>
<td>SearchAbsoluteTopImpressionShare</td>
</tr>
<tr class="even">
<td>metrics_search_budget_lost_absolute_top_impression_share</td>
<td>The number estimating how often your ad wasn't the very first ad above the organic search results due to a low budget. Note: Search budget lost absolute top impression share is reported in the range of 0 to 0.9. Any value above 0.9 is reported as 0.9001.</td>
<td>SearchBudgetLostAbsoluteTopImpressionShare</td>
</tr>
<tr class="odd">
<td>metrics_search_budget_lost_impression_share</td>
<td>The estimated percent of times that your ad was eligible to show on the Search Network but didn't because your budget was too low. Note: Search budget lost impression share is reported in the range of 0 to 0.9. Any value above 0.9 is reported as 0.9001.</td>
<td>SearchBudgetLostImpressionShare</td>
</tr>
<tr class="even">
<td>metrics_search_budget_lost_top_impression_share</td>
<td>The number estimating how often your ad didn't show anywhere above the organic search results due to a low budget. Note: Search budget lost top impression share is reported in the range of 0 to 0.9. Any value above 0.9 is reported as 0.9001.</td>
<td>SearchBudgetLostTopImpressionShare</td>
</tr>
<tr class="odd">
<td>metrics_search_click_share</td>
<td>The number of clicks you've received on the Search Network divided by the estimated number of clicks you were eligible to receive. Note: Search click share is reported in the range of 0.1 to 1. Any value below 0.1 is reported as 0.0999.</td>
<td>SearchClickShare</td>
</tr>
<tr class="even">
<td>metrics_search_exact_match_impression_share</td>
<td>The impressions you've received divided by the estimated number of impressions you were eligible to receive on the Search Network for search terms that matched your keywords exactly (or were close variants of your keyword), regardless of your keyword match types. Note: Search exact match impression share is reported in the range of 0.1 to 1. Any value below 0.1 is reported as 0.0999.</td>
<td>SearchExactMatchImpressionShare</td>
</tr>
<tr class="odd">
<td>metrics_search_impression_share</td>
<td>The impressions you've received on the Search Network divided by the estimated number of impressions you were eligible to receive. Note: Search impression share is reported in the range of 0.1 to 1. Any value below 0.1 is reported as 0.0999.</td>
<td>SearchImpressionShare</td>
</tr>
<tr class="even">
<td>metrics_search_rank_lost_absolute_top_impression_share</td>
<td>The number estimating how often your ad wasn't the very first ad above the organic search results due to poor Ad Rank. Note: Search rank lost absolute top impression share is reported in the range of 0 to 0.9. Any value above 0.9 is reported as 0.9001.</td>
<td>SearchRankLostAbsoluteTopImpressionShare</td>
</tr>
<tr class="odd">
<td>metrics_search_rank_lost_impression_share</td>
<td>The estimated percentage of impressions on the Search Network that your ads didn't receive due to poor Ad Rank. Note: Search rank lost impression share is reported in the range of 0 to 0.9. Any value above 0.9 is reported as 0.9001.</td>
<td>SearchRankLostImpressionShare</td>
</tr>
<tr class="even">
<td>metrics_search_rank_lost_top_impression_share</td>
<td>The number estimating how often your ad didn't show anywhere above the organic search results due to poor Ad Rank. Note: Search rank lost top impression share is reported in the range of 0 to 0.9. Any value above 0.9 is reported as 0.9001.</td>
<td>SearchRankLostTopImpressionShare</td>
</tr>
<tr class="odd">
<td>metrics_search_top_impression_share</td>
<td>The impressions you've received in the top location (anywhere above the organic search results) compared to the estimated number of impressions you were eligible to receive in the top location. Note: Search top impression share is reported in the range of 0.1 to 1. Any value below 0.1 is reported as 0.0999.</td>
<td>SearchTopImpressionShare</td>
</tr>
<tr class="even">
<td>metrics_top_impression_percentage</td>
<td>The percent of your ad impressions that are shown anywhere above the organic search results.</td>
<td>TopImpressionPercentage</td>
</tr>
<tr class="odd">
<td>metrics_value_per_all_conversions</td>
<td>The value of all conversions divided by the number of all conversions.</td>
<td>ValuePerAllConversion</td>
</tr>
<tr class="even">
<td>metrics_video_quartile_p100_rate</td>
<td>Percentage of impressions where the viewer watched all of your video.</td>
<td>VideoQuartile100Rate</td>
</tr>
<tr class="odd">
<td>metrics_video_quartile_p25_rate</td>
<td>Percentage of impressions where the viewer watched 25% of your video.</td>
<td>VideoQuartile25Rate</td>
</tr>
<tr class="even">
<td>metrics_video_quartile_p50_rate</td>
<td>Percentage of impressions where the viewer watched 50% of your video.</td>
<td>VideoQuartile50Rate</td>
</tr>
<tr class="odd">
<td>metrics_video_quartile_p75_rate</td>
<td>Percentage of impressions where the viewer watched 75% of your video.</td>
<td>VideoQuartile75Rate</td>
</tr>
<tr class="even">
<td>metrics_video_view_rate</td>
<td>The number of views your TrueView video ad receives divided by its number of impressions, including thumbnail impressions for TrueView in-display ads.</td>
<td>VideoViewRate</td>
</tr>
<tr class="odd">
<td>metrics_video_views</td>
<td>The number of times your video ads were viewed.</td>
<td>VideoViews</td>
</tr>
<tr class="even">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="even">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="odd">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="even">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="odd">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="even">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: CampaignLabel

Google Ads API Resource: [campaign\_label](https://developers.google.com/google-ads/api/fields/v21/campaign_label)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td></td>
</tr>
<tr class="even">
<td>campaign_label_campaign</td>
<td>The campaign to which the label is attached.</td>
<td></td>
</tr>
<tr class="odd">
<td>campaign_label_label</td>
<td>The label assigned to the campaign.</td>
<td></td>
</tr>
<tr class="even">
<td>campaign_label_resource_name</td>
<td>Name of the resource. Campaign label resource names have the form: `customers/{customer_id}/campaignLabels/{campaign_id}~{label_id}`</td>
<td></td>
</tr>
<tr class="odd">
<td>campaign_name</td>
<td>The name of the campaign. This field is required and shouldn't be empty when creating new campaigns. It must not contain any null (code point 0x0), NL line feed (code point 0xA) or carriage return (code point 0xD) characters.</td>
<td></td>
</tr>
<tr class="even">
<td>label_id</td>
<td>Id of the label. Read only.</td>
<td></td>
</tr>
<tr class="odd">
<td>label_name</td>
<td>The name of the label. This field is required and shouldn't be empty when creating a new label. The length of this string should be between 1 and 80, inclusive.</td>
<td></td>
</tr>
<tr class="even">
<td>label_resource_name</td>
<td>Name of the resource. Label resource names have the form: `customers/{customer_id}/labels/{label_id}`</td>
<td></td>
</tr>
</tbody>
</table>

Google Ads Table Name: CampaignLocationTargetStats

Google Ads API Resource: [location\_view](https://developers.google.com/google-ads/api/fields/v21/location_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>campaign_criterion_criterion_id</td>
<td>The ID of the criterion. This field is ignored during mutate.</td>
<td>CriterionId</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="even">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>AllConversions</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions_from_interactions_rate</td>
<td>All conversions from interactions (as oppose to view through conversions) divided by the number of ad interactions.</td>
<td>AllConversionRate</td>
</tr>
<tr class="even">
<td>metrics_all_conversions_value</td>
<td>The total value of all conversions.</td>
<td>AllConversionValue</td>
</tr>
<tr class="odd">
<td>metrics_average_cost</td>
<td>The average amount you pay per interaction. This amount is the total cost of your ads divided by the total number of interactions.</td>
<td>AverageCost</td>
</tr>
<tr class="even">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
<td>AverageCpc</td>
</tr>
<tr class="odd">
<td>metrics_average_cpe</td>
<td>The average amount that you've been charged for an ad engagement. This amount is the total cost of all ad engagements divided by the total number of ad engagements.</td>
<td>AverageCpe</td>
</tr>
<tr class="even">
<td>metrics_average_cpm</td>
<td>Average cost-per-thousand impressions (CPM).</td>
<td>AverageCpm</td>
</tr>
<tr class="odd">
<td>metrics_average_cpv</td>
<td>The average amount you pay each time someone views your ad. The average CPV is defined by the total cost of all ad views divided by the number of views.</td>
<td>AverageCpv</td>
</tr>
<tr class="even">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
<td>Clicks</td>
</tr>
<tr class="odd">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>Conversions</td>
</tr>
<tr class="even">
<td>metrics_conversions_from_interactions_rate</td>
<td>Conversions from interactions divided by the number of ad interactions (such as clicks for text ads or views for video ads). This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionRate</td>
</tr>
<tr class="odd">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="even">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
<td>Cost</td>
</tr>
<tr class="odd">
<td>metrics_cost_per_all_conversions</td>
<td>The cost of ad interactions divided by all conversions.</td>
<td>CostPerAllConversion</td>
</tr>
<tr class="even">
<td>metrics_cost_per_conversion</td>
<td>The cost of ad interactions divided by conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>CostPerConversion</td>
</tr>
<tr class="odd">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on a Google Ads ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
<td>CrossDeviceConversions</td>
</tr>
<tr class="even">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
<td>Ctr</td>
</tr>
<tr class="odd">
<td>metrics_engagement_rate</td>
<td>How often people engage with your ad after it's shown to them. This is the number of ad expansions divided by the number of times your ad is shown.</td>
<td>EngagementRate</td>
</tr>
<tr class="even">
<td>metrics_engagements</td>
<td>The number of engagements. An engagement occurs when a viewer expands your Lightbox ad. Also, in the future, other ad types may support engagement metrics.</td>
<td>Engagements</td>
</tr>
<tr class="odd">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
<td>Impressions</td>
</tr>
<tr class="even">
<td>metrics_interaction_event_types</td>
<td>The types of payable and free interactions.</td>
<td>InteractionTypes</td>
</tr>
<tr class="odd">
<td>metrics_interaction_rate</td>
<td>How often people interact with your ad after it is shown to them. This is the number of interactions divided by the number of times your ad is shown.</td>
<td>InteractionRate</td>
</tr>
<tr class="even">
<td>metrics_interactions</td>
<td>The number of interactions. An interaction is the main user action associated with an ad format, such as clicks for text and shopping ads or views for video ads.</td>
<td>Interactions</td>
</tr>
<tr class="odd">
<td>metrics_value_per_all_conversions</td>
<td>The value of all conversions divided by the number of all conversions.</td>
<td>ValuePerAllConversion</td>
</tr>
<tr class="even">
<td>metrics_value_per_conversion</td>
<td>The value of conversions divided by the number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ValuePerConversion</td>
</tr>
<tr class="odd">
<td>metrics_video_view_rate</td>
<td>The number of views your TrueView video ad receives divided by its number of impressions, including thumbnail impressions for TrueView in-display ads.</td>
<td>VideoViewRate</td>
</tr>
<tr class="even">
<td>metrics_video_views</td>
<td>The number of times your video ads were viewed.</td>
<td>VideoViews</td>
</tr>
<tr class="odd">
<td>metrics_view_through_conversions</td>
<td>The total number of view-through conversions. These happen when a customer sees an image or rich media ad, then later completes a conversion on your site without interacting with (for example, clicking on) another ad.</td>
<td>ViewThroughConversions</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="odd">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="even">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="odd">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="even">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: CampaignStats

Google Ads API Resource: [campaign](https://developers.google.com/google-ads/api/fields/v21/campaign)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td>BaseCampaignId</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="even">
<td>metrics_active_view_cpm</td>
<td>Average cost of viewable impressions (`active_view_impressions`).</td>
<td>ActiveViewCpm</td>
</tr>
<tr class="odd">
<td>metrics_active_view_ctr</td>
<td>Active view measurable clicks divided by active view viewable impressions. This metric is reported only for display network.</td>
<td>ActiveViewCtr</td>
</tr>
<tr class="even">
<td>metrics_active_view_impressions</td>
<td>A measurement of how often your ad has become viewable on a Display Network site.</td>
<td>ActiveViewImpressions</td>
</tr>
<tr class="odd">
<td>metrics_active_view_measurability</td>
<td>The ratio of impressions that could be measured by Active View over the number of served impressions.</td>
<td>ActiveViewMeasurability</td>
</tr>
<tr class="even">
<td>metrics_active_view_measurable_cost_micros</td>
<td>The cost of the impressions you received that were measurable by Active View.</td>
<td>ActiveViewMeasurableCost</td>
</tr>
<tr class="odd">
<td>metrics_active_view_measurable_impressions</td>
<td>The number of times your ads are appearing on placements in positions where they can be seen.</td>
<td>ActiveViewMeasurableImpressions</td>
</tr>
<tr class="even">
<td>metrics_active_view_viewability</td>
<td>The percentage of time when your ad appeared on an Active View enabled site (measurable impressions) and was viewable (viewable impressions).</td>
<td>ActiveViewViewability</td>
</tr>
<tr class="odd">
<td>metrics_average_cost</td>
<td>The average amount you pay per interaction. This amount is the total cost of your ads divided by the total number of interactions.</td>
<td>AverageCost</td>
</tr>
<tr class="even">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
<td>AverageCpc</td>
</tr>
<tr class="odd">
<td>metrics_average_cpm</td>
<td>Average cost-per-thousand impressions (CPM).</td>
<td>AverageCpm</td>
</tr>
<tr class="even">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
<td>Clicks</td>
</tr>
<tr class="odd">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>Conversions</td>
</tr>
<tr class="even">
<td>metrics_conversions_from_interactions_rate</td>
<td>Conversions from interactions divided by the number of ad interactions (such as clicks for text ads or views for video ads). This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionRate</td>
</tr>
<tr class="odd">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="even">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
<td>Cost</td>
</tr>
<tr class="odd">
<td>metrics_cost_per_conversion</td>
<td>The cost of ad interactions divided by conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>CostPerConversion</td>
</tr>
<tr class="even">
<td>metrics_cost_per_current_model_attributed_conversion</td>
<td>The cost of ad interactions divided by current model attributed conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>CostPerCurrentModelAttributedConversion</td>
</tr>
<tr class="odd">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
<td>Ctr</td>
</tr>
<tr class="even">
<td>metrics_current_model_attributed_conversions</td>
<td>Shows how your historic conversions data would look under the attribution model you've selected. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>CurrentModelAttributedConversions</td>
</tr>
<tr class="odd">
<td>metrics_current_model_attributed_conversions_value</td>
<td>The total value of current model attributed conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>CurrentModelAttributedConversionValue</td>
</tr>
<tr class="even">
<td>metrics_gmail_forwards</td>
<td>The number of times the ad was forwarded to someone else as a message.</td>
<td>GmailForwards</td>
</tr>
<tr class="odd">
<td>metrics_gmail_saves</td>
<td>The number of times someone has saved your Gmail ad to their inbox as a message.</td>
<td>GmailSaves</td>
</tr>
<tr class="even">
<td>metrics_gmail_secondary_clicks</td>
<td>The number of clicks to the landing page on the expanded state of Gmail ads.</td>
<td>GmailSecondaryClicks</td>
</tr>
<tr class="odd">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
<td>Impressions</td>
</tr>
<tr class="even">
<td>metrics_interaction_event_types</td>
<td>The types of payable and free interactions.</td>
<td>InteractionTypes</td>
</tr>
<tr class="odd">
<td>metrics_interaction_rate</td>
<td>How often people interact with your ad after it is shown to them. This is the number of interactions divided by the number of times your ad is shown.</td>
<td>InteractionRate</td>
</tr>
<tr class="even">
<td>metrics_interactions</td>
<td>The number of interactions. An interaction is the main user action associated with an ad format, such as clicks for text and shopping ads or views for video ads.</td>
<td>Interactions</td>
</tr>
<tr class="odd">
<td>metrics_value_per_conversion</td>
<td>The value of conversions divided by the number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ValuePerConversion</td>
</tr>
<tr class="even">
<td>metrics_value_per_current_model_attributed_conversion</td>
<td>The value of current model attributed conversions divided by the number of the conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ValuePerCurrentModelAttributedConversion</td>
</tr>
<tr class="odd">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="even">
<td>segments_click_type</td>
<td>Click type.</td>
<td>ClickType</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="even">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="odd">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
<tr class="even">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="odd">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="even">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="odd">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: ClickStats

Google Ads API Resource: [click\_view](https://developers.google.com/google-ads/api/fields/v21/click_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="even">
<td>ad_group_status</td>
<td>The status of the ad group.</td>
<td></td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="even">
<td>click_view_ad_group_ad</td>
<td>The associated ad.</td>
<td>CreativeId</td>
</tr>
<tr class="odd">
<td>click_view_area_of_interest_city</td>
<td>The city location criterion associated with the impression.</td>
<td>AoiCityCriteriaId</td>
</tr>
<tr class="even">
<td>click_view_area_of_interest_country</td>
<td>The country location criterion associated with the impression.</td>
<td>AoiCountryCriteriaId</td>
</tr>
<tr class="odd">
<td>click_view_area_of_interest_metro</td>
<td>The metro location criterion associated with the impression.</td>
<td>AoiMetroCriteriaId</td>
</tr>
<tr class="even">
<td>click_view_area_of_interest_most_specific</td>
<td>The most specific location criterion associated with the impression.</td>
<td>AoiMostSpecificTargetId</td>
</tr>
<tr class="odd">
<td>click_view_area_of_interest_region</td>
<td>The region location criterion associated with the impression.</td>
<td>AoiRegionCriteriaId</td>
</tr>
<tr class="even">
<td>click_view_gclid</td>
<td>The Google Click ID.</td>
<td>GclId</td>
</tr>
<tr class="odd">
<td>click_view_keyword</td>
<td>The associated keyword, if one exists and the click corresponds to the SEARCH channel.</td>
<td>CriteriaId</td>
</tr>
<tr class="even">
<td>click_view_keyword_info_match_type</td>
<td>The match type of the keyword.</td>
<td>KeywordMatchType</td>
</tr>
<tr class="odd">
<td>click_view_keyword_info_text</td>
<td>The text of the keyword (at most 80 characters and 10 words).</td>
<td>CriteriaParameters</td>
</tr>
<tr class="even">
<td>click_view_location_of_presence_city</td>
<td>The city location criterion associated with the impression.</td>
<td>LopCityCriteriaId</td>
</tr>
<tr class="odd">
<td>click_view_location_of_presence_country</td>
<td>The country location criterion associated with the impression.</td>
<td>LopCountryCriteriaId</td>
</tr>
<tr class="even">
<td>click_view_location_of_presence_metro</td>
<td>The metro location criterion associated with the impression.</td>
<td>LopMetroCriteriaId</td>
</tr>
<tr class="odd">
<td>click_view_location_of_presence_most_specific</td>
<td>The most specific location criterion associated with the impression.</td>
<td>LopMostSpecificTargetId</td>
</tr>
<tr class="even">
<td>click_view_location_of_presence_region</td>
<td>The region location criterion associated with the impression.</td>
<td>LopRegionCriteriaId</td>
</tr>
<tr class="odd">
<td>click_view_page_number</td>
<td>Page number in search results where the ad was shown.</td>
<td>Page</td>
</tr>
<tr class="even">
<td>customer_descriptive_name</td>
<td>Optional, non-unique descriptive name of the customer.</td>
<td>AccountDescriptiveName</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="even">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
<td>Clicks</td>
</tr>
<tr class="odd">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="even">
<td>segments_click_type</td>
<td>Click type.</td>
<td>ClickType</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="even">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
<tr class="odd">
<td>segments_slot</td>
<td>Position of the ad.</td>
<td>Slot</td>
</tr>
</tbody>
</table>

Google Ads Table Name: Customer

Google Ads API Resource: [customer](https://developers.google.com/google-ads/api/fields/v21/customer)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>customer_auto_tagging_enabled</td>
<td>Whether autotagging is enabled for the customer.</td>
<td>IsAutoTaggingEnabled</td>
</tr>
<tr class="even">
<td>customer_currency_code</td>
<td>The currency in which the account operates. A subset of the currency codes from the ISO 4217 standard is supported.</td>
<td>AccountCurrencyCode</td>
</tr>
<tr class="odd">
<td>customer_descriptive_name</td>
<td>Optional, non-unique descriptive name of the customer.</td>
<td>AccountDescriptiveName,CustomerDescriptiveName</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="odd">
<td>customer_manager</td>
<td>Whether the customer is a manager.</td>
<td>CanManageClients</td>
</tr>
<tr class="even">
<td>customer_test_account</td>
<td>Whether the customer is a test account.</td>
<td>IsTestAccount</td>
</tr>
<tr class="odd">
<td>customer_time_zone</td>
<td>The local timezone ID of the customer.</td>
<td>AccountTimeZone</td>
</tr>
</tbody>
</table>

Google Ads Table Name: DisplayVideoAutomaticPlacementsStats

Google Ads API Resource: [group\_placement\_view](https://developers.google.com/google-ads/api/fields/v21/group_placement_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_name</td>
<td>The name of the ad group. This field is required and shouldn't be empty when creating new ad groups. It must contain fewer than 255 UTF-8 full-width characters. It must not contain any null (code point 0x0), NL line feed (code point 0xA) or carriage return (code point 0xD) characters.</td>
<td></td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td></td>
</tr>
<tr class="even">
<td>campaign_name</td>
<td>The name of the campaign. This field is required and shouldn't be empty when creating new campaigns. It must not contain any null (code point 0x0), NL line feed (code point 0xA) or carriage return (code point 0xD) characters.</td>
<td></td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td></td>
</tr>
<tr class="even">
<td>group_placement_view_placement</td>
<td>The automatic placement string at group level, e. g. web domain, mobile app ID, or a YouTube channel ID.</td>
<td></td>
</tr>
<tr class="odd">
<td>group_placement_view_placement_type</td>
<td>Type of the placement. For example, Website, YouTube Channel, Mobile Application.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_average_cpm</td>
<td>Average cost-per-thousand impressions (CPM).</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_average_cpv</td>
<td>The average amount you pay each time someone views your ad. The average CPV is defined by the total cost of all ad views divided by the number of views.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_video_view_rate</td>
<td>The number of views your TrueView video ad receives divided by its number of impressions, including thumbnail impressions for TrueView in-display ads.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_video_views</td>
<td>The number of times your video ads were viewed.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td></td>
</tr>
</tbody>
</table>

Google Ads Table Name: DisplayVideoKeywordStats

Google Ads API Resource: [display\_keyword\_view](https://developers.google.com/google-ads/api/fields/v21/display_keyword_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_criterion_keyword_text</td>
<td>The text of the keyword (at most 80 characters and 10 words).</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td></td>
</tr>
<tr class="odd">
<td>ad_group_name</td>
<td>The name of the ad group. This field is required and shouldn't be empty when creating new ad groups. It must contain fewer than 255 UTF-8 full-width characters. It must not contain any null (code point 0x0), NL line feed (code point 0xA) or carriage return (code point 0xD) characters.</td>
<td></td>
</tr>
<tr class="even">
<td>campaign_advertising_channel_sub_type</td>
<td>Optional refinement to `advertising_channel_type`. Must be a valid sub-type of the parent channel type. Can be set only when creating campaigns. After campaign is created, the field cannot be changed.</td>
<td></td>
</tr>
<tr class="odd">
<td>campaign_bidding_strategy_type</td>
<td>The type of bidding strategy. A bidding strategy can be created by setting either the bidding scheme to create a standard bidding strategy or the `bidding_strategy` field to create a portfolio bidding strategy. This field is read-only.</td>
<td></td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td></td>
</tr>
<tr class="odd">
<td>campaign_name</td>
<td>The name of the campaign. This field is required and shouldn't be empty when creating new campaigns. It must not contain any null (code point 0x0), NL line feed (code point 0xA) or carriage return (code point 0xD) characters.</td>
<td></td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_average_cpm</td>
<td>Average cost-per-thousand impressions (CPM).</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_average_cpv</td>
<td>The average amount you pay each time someone views your ad. The average CPV is defined by the total cost of all ad views divided by the number of views.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_conversions_from_interactions_rate</td>
<td>Conversions from interactions divided by the number of ad interactions (such as clicks for text ads or views for video ads). This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_cost_per_conversion</td>
<td>The cost of ad interactions divided by conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_interaction_rate</td>
<td>How often people interact with your ad after it is shown to them. This is the number of interactions divided by the number of times your ad is shown.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_interactions</td>
<td>The number of interactions. An interaction is the main user action associated with an ad format, such as clicks for text and shopping ads or views for video ads.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_view_through_conversions</td>
<td>The total number of view-through conversions. These happen when a customer sees an image or rich media ad, then later completes a conversion on your site without interacting with (for example, clicking on) another ad.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td></td>
</tr>
</tbody>
</table>

Google Ads Table Name: DisplayVideoTopicStats

Google Ads API Resource: [topic\_view](https://developers.google.com/google-ads/api/fields/v21/topic_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_criterion_status</td>
<td>The status of the criterion.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_criterion_topic_path</td>
<td>The category to target or exclude. Each subsequent element in the array describes a more specific sub-category. For example, \"Pets &amp; Animals\", \"Pets\", \"Dogs\" represents the \"Pets &amp; Animals/Pets/Dogs\" category.</td>
<td></td>
</tr>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_name</td>
<td>The name of the ad group. This field is required and shouldn't be empty when creating new ad groups. It must contain fewer than 255 UTF-8 full-width characters. It must not contain any null (code point 0x0), NL line feed (code point 0xA) or carriage return (code point 0xD) characters.</td>
<td></td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td></td>
</tr>
<tr class="even">
<td>campaign_name</td>
<td>The name of the campaign. This field is required and shouldn't be empty when creating new campaigns. It must not contain any null (code point 0x0), NL line feed (code point 0xA) or carriage return (code point 0xD) characters.</td>
<td></td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_average_cpm</td>
<td>Average cost-per-thousand impressions (CPM).</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td></td>
</tr>
</tbody>
</table>

Google Ads Table Name: Gender

Google Ads API Resource: [gender\_view](https://developers.google.com/google-ads/api/fields/v21/gender_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_base_ad_group</td>
<td>For draft or experiment ad groups, this field is the resource name of the base ad group from which this ad group was created. If a draft or experiment ad group does not have a base ad group, then this field is null. For base ad groups, this field equals the ad group resource name. This field is read-only.</td>
<td>BaseAdGroupId</td>
</tr>
<tr class="even">
<td>ad_group_criterion_bid_modifier</td>
<td>The modifier for the bid when the criterion matches. The modifier must be in the range: 0.1 - 10.0. Most targetable criteria types support modifiers.</td>
<td>BidModifier</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion. This field is ignored for mutates.</td>
<td>CriterionId</td>
</tr>
<tr class="even">
<td>ad_group_criterion_effective_cpc_bid_micros</td>
<td>The effective CPC (cost-per-click) bid.</td>
<td>CpcBid</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_effective_cpc_bid_source</td>
<td>Source of the effective CPC bid.</td>
<td>CpcBidSource</td>
</tr>
<tr class="even">
<td>ad_group_criterion_effective_cpm_bid_micros</td>
<td>The effective CPM (cost-per-thousand viewable impressions) bid.</td>
<td>CpmBidStr</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_effective_cpm_bid_source</td>
<td>Source of the effective CPM bid.</td>
<td>CpmBidSource</td>
</tr>
<tr class="even">
<td>ad_group_criterion_final_mobile_urls</td>
<td>The list of possible final mobile URLs after all cross-domain redirects.</td>
<td>FinalMobileUrls</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_final_urls</td>
<td>The list of possible final URLs after all cross-domain redirects for the ad.</td>
<td>FinalUrls</td>
</tr>
<tr class="even">
<td>ad_group_criterion_gender_type</td>
<td>Type of the gender.</td>
<td>Criteria</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_negative</td>
<td>Whether to target (`false`) or exclude (`true`) the criterion. This field is immutable. To switch a criterion from positive to negative, remove then re-add it.</td>
<td>IsNegative</td>
</tr>
<tr class="even">
<td>ad_group_criterion_status</td>
<td>The status of the criterion.</td>
<td>Status</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_tracking_url_template</td>
<td>The URL template for constructing a tracking URL.</td>
<td>TrackingUrlTemplate</td>
</tr>
<tr class="even">
<td>ad_group_criterion_url_custom_parameters</td>
<td>The list of mappings used to substitute custom parameter tags in a `tracking_url_template`, `final_urls`, or `mobile_final_urls`.</td>
<td>UrlCustomParameters</td>
</tr>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="even">
<td>ad_group_targeting_setting_target_restrictions</td>
<td>The per-targeting-dimension setting to restrict the reach of your campaign or ad group.</td>
<td></td>
</tr>
<tr class="odd">
<td>bidding_strategy_name</td>
<td>The name of the bidding strategy. All bidding strategies within an account must be named distinctly. The length of this string should be between 1 and 255, inclusive, in UTF-8 bytes, (trimmed).</td>
<td>BiddingStrategyName</td>
</tr>
<tr class="even">
<td>bidding_strategy_type</td>
<td>The type of the bidding strategy. Create a bidding strategy by setting the bidding scheme. This field is read-only.</td>
<td>BiddingStrategyType</td>
</tr>
<tr class="odd">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td>BaseCampaignId</td>
</tr>
<tr class="even">
<td>campaign_bidding_strategy</td>
<td>Portfolio bidding strategy used by campaign.</td>
<td>BiddingStrategyId</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
</tbody>
</table>

Google Ads Table Name: GenderBasicStats

Google Ads API Resource: [gender\_view](https://developers.google.com/google-ads/api/fields/v21/gender_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_base_ad_group</td>
<td>For draft or experiment ad groups, this field is the resource name of the base ad group from which this ad group was created. If a draft or experiment ad group does not have a base ad group, then this field is null. For base ad groups, this field equals the ad group resource name. This field is read-only.</td>
<td>BaseAdGroupId</td>
</tr>
<tr class="even">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion. This field is ignored for mutates.</td>
<td>CriterionId</td>
</tr>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="even">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td>BaseCampaignId</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="odd">
<td>metrics_active_view_impressions</td>
<td>A measurement of how often your ad has become viewable on a Display Network site.</td>
<td>ActiveViewImpressions</td>
</tr>
<tr class="even">
<td>metrics_active_view_measurability</td>
<td>The ratio of impressions that could be measured by Active View over the number of served impressions.</td>
<td>ActiveViewMeasurability</td>
</tr>
<tr class="odd">
<td>metrics_active_view_measurable_cost_micros</td>
<td>The cost of the impressions you received that were measurable by Active View.</td>
<td>ActiveViewMeasurableCost</td>
</tr>
<tr class="even">
<td>metrics_active_view_measurable_impressions</td>
<td>The number of times your ads are appearing on placements in positions where they can be seen.</td>
<td>ActiveViewMeasurableImpressions</td>
</tr>
<tr class="odd">
<td>metrics_active_view_viewability</td>
<td>The percentage of time when your ad appeared on an Active View enabled site (measurable impressions) and was viewable (viewable impressions).</td>
<td>ActiveViewViewability</td>
</tr>
<tr class="even">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>AllConversions</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions_value</td>
<td>The total value of all conversions.</td>
<td>AllConversionValue</td>
</tr>
<tr class="even">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
<td>Clicks</td>
</tr>
<tr class="odd">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>Conversions</td>
</tr>
<tr class="even">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="odd">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
<td>Cost</td>
</tr>
<tr class="even">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on a Google Ads ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
<td>CrossDeviceConversions</td>
</tr>
<tr class="odd">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
<td>Impressions</td>
</tr>
<tr class="even">
<td>metrics_interaction_event_types</td>
<td>The types of payable and free interactions.</td>
<td>InteractionTypes</td>
</tr>
<tr class="odd">
<td>metrics_interactions</td>
<td>The number of interactions. An interaction is the main user action associated with an ad format, such as clicks for text and shopping ads or views for video ads.</td>
<td>Interactions</td>
</tr>
<tr class="even">
<td>metrics_view_through_conversions</td>
<td>The total number of view-through conversions. These happen when a customer sees an image or rich media ad, then later completes a conversion on your site without interacting with (for example, clicking on) another ad.</td>
<td>ViewThroughConversions</td>
</tr>
<tr class="odd">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="odd">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
</tbody>
</table>

Google Ads Table Name: GenderConversionStats

Google Ads API Resource: [gender\_view](https://developers.google.com/google-ads/api/fields/v21/gender_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_base_ad_group</td>
<td>For draft or experiment ad groups, this field is the resource name of the base ad group from which this ad group was created. If a draft or experiment ad group does not have a base ad group, then this field is null. For base ad groups, this field equals the ad group resource name. This field is read-only.</td>
<td>BaseAdGroupId</td>
</tr>
<tr class="even">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion. This field is ignored for mutates.</td>
<td>CriterionId</td>
</tr>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="even">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td>BaseCampaignId</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>AllConversions</td>
</tr>
<tr class="even">
<td>metrics_all_conversions_value</td>
<td>The total value of all conversions.</td>
<td>AllConversionValue</td>
</tr>
<tr class="odd">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>Conversions</td>
</tr>
<tr class="even">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="odd">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on a Google Ads ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
<td>CrossDeviceConversions</td>
</tr>
<tr class="even">
<td>metrics_value_per_all_conversions</td>
<td>The value of all conversions divided by the number of all conversions.</td>
<td>ValuePerAllConversion</td>
</tr>
<tr class="odd">
<td>metrics_value_per_conversion</td>
<td>The value of conversions divided by the number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ValuePerConversion</td>
</tr>
<tr class="even">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="odd">
<td>segments_click_type</td>
<td>Click type.</td>
<td>ClickType</td>
</tr>
<tr class="even">
<td>segments_conversion_action</td>
<td>Resource name of the conversion action.</td>
<td>ConversionTrackerId</td>
</tr>
<tr class="odd">
<td>segments_conversion_action_category</td>
<td>Conversion action category.</td>
<td>ConversionCategoryName</td>
</tr>
<tr class="even">
<td>segments_conversion_action_name</td>
<td>Conversion action name.</td>
<td>ConversionTypeName</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="even">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="odd">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
<tr class="even">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="odd">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="even">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="odd">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: GenderNonClickStats

Google Ads API Resource: [gender\_view](https://developers.google.com/google-ads/api/fields/v21/gender_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_base_ad_group</td>
<td>For draft or experiment ad groups, this field is the resource name of the base ad group from which this ad group was created. If a draft or experiment ad group does not have a base ad group, then this field is null. For base ad groups, this field equals the ad group resource name. This field is read-only.</td>
<td>BaseAdGroupId</td>
</tr>
<tr class="even">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion. This field is ignored for mutates.</td>
<td>CriterionId</td>
</tr>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="even">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td>BaseCampaignId</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="odd">
<td>metrics_average_cpe</td>
<td>The average amount that you've been charged for an ad engagement. This amount is the total cost of all ad engagements divided by the total number of ad engagements.</td>
<td>AverageCpe</td>
</tr>
<tr class="even">
<td>metrics_average_cpv</td>
<td>The average amount you pay each time someone views your ad. The average CPV is defined by the total cost of all ad views divided by the number of views.</td>
<td>AverageCpv</td>
</tr>
<tr class="odd">
<td>metrics_engagement_rate</td>
<td>How often people engage with your ad after it's shown to them. This is the number of ad expansions divided by the number of times your ad is shown.</td>
<td>EngagementRate</td>
</tr>
<tr class="even">
<td>metrics_engagements</td>
<td>The number of engagements. An engagement occurs when a viewer expands your Lightbox ad. Also, in the future, other ad types may support engagement metrics.</td>
<td>Engagements</td>
</tr>
<tr class="odd">
<td>metrics_video_quartile_p100_rate</td>
<td>Percentage of impressions where the viewer watched all of your video.</td>
<td>VideoQuartile100Rate</td>
</tr>
<tr class="even">
<td>metrics_video_quartile_p25_rate</td>
<td>Percentage of impressions where the viewer watched 25% of your video.</td>
<td>VideoQuartile25Rate</td>
</tr>
<tr class="odd">
<td>metrics_video_quartile_p50_rate</td>
<td>Percentage of impressions where the viewer watched 50% of your video.</td>
<td>VideoQuartile50Rate</td>
</tr>
<tr class="even">
<td>metrics_video_quartile_p75_rate</td>
<td>Percentage of impressions where the viewer watched 75% of your video.</td>
<td>VideoQuartile75Rate</td>
</tr>
<tr class="odd">
<td>metrics_video_view_rate</td>
<td>The number of views your TrueView video ad receives divided by its number of impressions, including thumbnail impressions for TrueView in-display ads.</td>
<td>VideoViewRate</td>
</tr>
<tr class="even">
<td>metrics_video_views</td>
<td>The number of times your video ads were viewed.</td>
<td>VideoViews</td>
</tr>
<tr class="odd">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="odd">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="even">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
<tr class="odd">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="even">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="odd">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="even">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: GenderStats

Google Ads API Resource: [gender\_view](https://developers.google.com/google-ads/api/fields/v21/gender_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_base_ad_group</td>
<td>For draft or experiment ad groups, this field is the resource name of the base ad group from which this ad group was created. If a draft or experiment ad group does not have a base ad group, then this field is null. For base ad groups, this field equals the ad group resource name. This field is read-only.</td>
<td>BaseAdGroupId</td>
</tr>
<tr class="even">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion. This field is ignored for mutates.</td>
<td>CriterionId</td>
</tr>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="even">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td>BaseCampaignId</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="odd">
<td>metrics_active_view_cpm</td>
<td>Average cost of viewable impressions (`active_view_impressions`).</td>
<td>ActiveViewCpm</td>
</tr>
<tr class="even">
<td>metrics_active_view_ctr</td>
<td>Active view measurable clicks divided by active view viewable impressions. This metric is reported only for display network.</td>
<td>ActiveViewCtr</td>
</tr>
<tr class="odd">
<td>metrics_active_view_impressions</td>
<td>A measurement of how often your ad has become viewable on a Display Network site.</td>
<td>ActiveViewImpressions</td>
</tr>
<tr class="even">
<td>metrics_active_view_measurability</td>
<td>The ratio of impressions that could be measured by Active View over the number of served impressions.</td>
<td>ActiveViewMeasurability</td>
</tr>
<tr class="odd">
<td>metrics_active_view_measurable_cost_micros</td>
<td>The cost of the impressions you received that were measurable by Active View.</td>
<td>ActiveViewMeasurableCost</td>
</tr>
<tr class="even">
<td>metrics_active_view_measurable_impressions</td>
<td>The number of times your ads are appearing on placements in positions where they can be seen.</td>
<td>ActiveViewMeasurableImpressions</td>
</tr>
<tr class="odd">
<td>metrics_active_view_viewability</td>
<td>The percentage of time when your ad appeared on an Active View enabled site (measurable impressions) and was viewable (viewable impressions).</td>
<td>ActiveViewViewability</td>
</tr>
<tr class="even">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>AllConversions</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions_from_interactions_rate</td>
<td>All conversions from interactions (as oppose to view through conversions) divided by the number of ad interactions.</td>
<td>AllConversionRate</td>
</tr>
<tr class="even">
<td>metrics_all_conversions_value</td>
<td>The total value of all conversions.</td>
<td>AllConversionValue</td>
</tr>
<tr class="odd">
<td>metrics_average_cost</td>
<td>The average amount you pay per interaction. This amount is the total cost of your ads divided by the total number of interactions.</td>
<td>AverageCost</td>
</tr>
<tr class="even">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
<td>AverageCpc</td>
</tr>
<tr class="odd">
<td>metrics_average_cpm</td>
<td>Average cost-per-thousand impressions (CPM).</td>
<td>AverageCpm</td>
</tr>
<tr class="even">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
<td>Clicks</td>
</tr>
<tr class="odd">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>Conversions</td>
</tr>
<tr class="even">
<td>metrics_conversions_from_interactions_rate</td>
<td>Conversions from interactions divided by the number of ad interactions (such as clicks for text ads or views for video ads). This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionRate</td>
</tr>
<tr class="odd">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="even">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
<td>Cost</td>
</tr>
<tr class="odd">
<td>metrics_cost_per_all_conversions</td>
<td>The cost of ad interactions divided by all conversions.</td>
<td>CostPerAllConversion</td>
</tr>
<tr class="even">
<td>metrics_cost_per_conversion</td>
<td>The cost of ad interactions divided by conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>CostPerConversion</td>
</tr>
<tr class="odd">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on a Google Ads ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
<td>CrossDeviceConversions</td>
</tr>
<tr class="even">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
<td>Ctr</td>
</tr>
<tr class="odd">
<td>metrics_gmail_forwards</td>
<td>The number of times the ad was forwarded to someone else as a message.</td>
<td>GmailForwards</td>
</tr>
<tr class="even">
<td>metrics_gmail_saves</td>
<td>The number of times someone has saved your Gmail ad to their inbox as a message.</td>
<td>GmailSaves</td>
</tr>
<tr class="odd">
<td>metrics_gmail_secondary_clicks</td>
<td>The number of clicks to the landing page on the expanded state of Gmail ads.</td>
<td>GmailSecondaryClicks</td>
</tr>
<tr class="even">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
<td>Impressions</td>
</tr>
<tr class="odd">
<td>metrics_interaction_event_types</td>
<td>The types of payable and free interactions.</td>
<td>InteractionTypes</td>
</tr>
<tr class="even">
<td>metrics_interaction_rate</td>
<td>How often people interact with your ad after it is shown to them. This is the number of interactions divided by the number of times your ad is shown.</td>
<td>InteractionRate</td>
</tr>
<tr class="odd">
<td>metrics_interactions</td>
<td>The number of interactions. An interaction is the main user action associated with an ad format, such as clicks for text and shopping ads or views for video ads.</td>
<td>Interactions</td>
</tr>
<tr class="even">
<td>metrics_value_per_all_conversions</td>
<td>The value of all conversions divided by the number of all conversions.</td>
<td>ValuePerAllConversion</td>
</tr>
<tr class="odd">
<td>metrics_value_per_conversion</td>
<td>The value of conversions divided by the number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ValuePerConversion</td>
</tr>
<tr class="even">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="odd">
<td>segments_click_type</td>
<td>Click type.</td>
<td>ClickType</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="odd">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="even">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
<tr class="odd">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="even">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="odd">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="even">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: GeoConversionStats

Google Ads API Resource: [geographic\_view](https://developers.google.com/google-ads/api/fields/v21/geographic_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="even">
<td>ad_group_name</td>
<td>The name of the ad group. This field is required and shouldn't be empty when creating new ad groups. It must contain fewer than 255 UTF-8 full-width characters. It must not contain any null (code point 0x0), NL line feed (code point 0xA) or carriage return (code point 0xD) characters.</td>
<td>AdGroupName</td>
</tr>
<tr class="odd">
<td>ad_group_status</td>
<td>The status of the ad group.</td>
<td>AdGroupStatus</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="odd">
<td>campaign_status</td>
<td>The status of the campaign. When a new campaign is added, the status defaults to ENABLED.</td>
<td></td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="odd">
<td>geographic_view_country_criterion_id</td>
<td>Criterion Id for the country.</td>
<td>CountryCriteriaId</td>
</tr>
<tr class="even">
<td>geographic_view_location_type</td>
<td>Type of the geo targeting of the campaign.</td>
<td>LocationType</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>AllConversions</td>
</tr>
<tr class="even">
<td>metrics_all_conversions_value</td>
<td>The total value of all conversions.</td>
<td>AllConversionValue</td>
</tr>
<tr class="odd">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>Conversions</td>
</tr>
<tr class="even">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="odd">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on a Google Ads ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
<td>CrossDeviceConversions</td>
</tr>
<tr class="even">
<td>metrics_value_per_all_conversions</td>
<td>The value of all conversions divided by the number of all conversions.</td>
<td>ValuePerAllConversion</td>
</tr>
<tr class="odd">
<td>metrics_value_per_conversion</td>
<td>The value of conversions divided by the number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ValuePerConversion</td>
</tr>
<tr class="even">
<td>metrics_view_through_conversions</td>
<td>The total number of view-through conversions. These happen when a customer sees an image or rich media ad, then later completes a conversion on your site without interacting with (for example, clicking on) another ad.</td>
<td>ViewThroughConversions</td>
</tr>
<tr class="odd">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="even">
<td>segments_conversion_action</td>
<td>Resource name of the conversion action.</td>
<td>ConversionTrackerId</td>
</tr>
<tr class="odd">
<td>segments_conversion_action_category</td>
<td>Conversion action category.</td>
<td>ConversionCategoryName</td>
</tr>
<tr class="even">
<td>segments_conversion_action_name</td>
<td>Conversion action name.</td>
<td>ConversionTypeName</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="even">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="odd">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
<tr class="even">
<td>segments_geo_target_most_specific_location</td>
<td>Resource name of the geo target constant that represents the most specific location.</td>
<td>MostSpecificCriteriaId</td>
</tr>
<tr class="odd">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="even">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="odd">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="even">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: GeoStats

Google Ads API Resource: [geographic\_view](https://developers.google.com/google-ads/api/fields/v21/geographic_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="even">
<td>ad_group_name</td>
<td>The name of the ad group. This field is required and shouldn't be empty when creating new ad groups. It must contain fewer than 255 UTF-8 full-width characters. It must not contain any null (code point 0x0), NL line feed (code point 0xA) or carriage return (code point 0xD) characters.</td>
<td>AdGroupName</td>
</tr>
<tr class="odd">
<td>ad_group_status</td>
<td>The status of the ad group.</td>
<td>AdGroupStatus</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="odd">
<td>campaign_status</td>
<td>The status of the campaign. When a new campaign is added, the status defaults to ENABLED.</td>
<td></td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="odd">
<td>geographic_view_country_criterion_id</td>
<td>Criterion Id for the country.</td>
<td>CountryCriteriaId</td>
</tr>
<tr class="even">
<td>geographic_view_location_type</td>
<td>Type of the geo targeting of the campaign.</td>
<td>LocationType</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>AllConversions</td>
</tr>
<tr class="even">
<td>metrics_all_conversions_from_interactions_rate</td>
<td>All conversions from interactions (as oppose to view through conversions) divided by the number of ad interactions.</td>
<td>AllConversionRate</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions_value</td>
<td>The total value of all conversions.</td>
<td>AllConversionValue</td>
</tr>
<tr class="even">
<td>metrics_average_cost</td>
<td>The average amount you pay per interaction. This amount is the total cost of your ads divided by the total number of interactions.</td>
<td>AverageCost</td>
</tr>
<tr class="odd">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
<td>AverageCpc</td>
</tr>
<tr class="even">
<td>metrics_average_cpm</td>
<td>Average cost-per-thousand impressions (CPM).</td>
<td>AverageCpm</td>
</tr>
<tr class="odd">
<td>metrics_average_cpv</td>
<td>The average amount you pay each time someone views your ad. The average CPV is defined by the total cost of all ad views divided by the number of views.</td>
<td>AverageCpv</td>
</tr>
<tr class="even">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
<td>Clicks</td>
</tr>
<tr class="odd">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>Conversions</td>
</tr>
<tr class="even">
<td>metrics_conversions_from_interactions_rate</td>
<td>Conversions from interactions divided by the number of ad interactions (such as clicks for text ads or views for video ads). This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionRate</td>
</tr>
<tr class="odd">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="even">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
<td>Cost</td>
</tr>
<tr class="odd">
<td>metrics_cost_per_all_conversions</td>
<td>The cost of ad interactions divided by all conversions.</td>
<td>CostPerAllConversion</td>
</tr>
<tr class="even">
<td>metrics_cost_per_conversion</td>
<td>The cost of ad interactions divided by conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>CostPerConversion</td>
</tr>
<tr class="odd">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on a Google Ads ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
<td>CrossDeviceConversions</td>
</tr>
<tr class="even">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
<td>Ctr</td>
</tr>
<tr class="odd">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
<td>Impressions</td>
</tr>
<tr class="even">
<td>metrics_interaction_event_types</td>
<td>The types of payable and free interactions.</td>
<td>InteractionTypes</td>
</tr>
<tr class="odd">
<td>metrics_interaction_rate</td>
<td>How often people interact with your ad after it is shown to them. This is the number of interactions divided by the number of times your ad is shown.</td>
<td>InteractionRate</td>
</tr>
<tr class="even">
<td>metrics_interactions</td>
<td>The number of interactions. An interaction is the main user action associated with an ad format, such as clicks for text and shopping ads or views for video ads.</td>
<td>Interactions</td>
</tr>
<tr class="odd">
<td>metrics_value_per_all_conversions</td>
<td>The value of all conversions divided by the number of all conversions.</td>
<td>ValuePerAllConversion</td>
</tr>
<tr class="even">
<td>metrics_value_per_conversion</td>
<td>The value of conversions divided by the number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ValuePerConversion</td>
</tr>
<tr class="odd">
<td>metrics_video_view_rate</td>
<td>The number of views your TrueView video ad receives divided by its number of impressions, including thumbnail impressions for TrueView in-display ads.</td>
<td>VideoViewRate</td>
</tr>
<tr class="even">
<td>metrics_video_views</td>
<td>The number of times your video ads were viewed.</td>
<td>VideoViews</td>
</tr>
<tr class="odd">
<td>metrics_view_through_conversions</td>
<td>The total number of view-through conversions. These happen when a customer sees an image or rich media ad, then later completes a conversion on your site without interacting with (for example, clicking on) another ad.</td>
<td>ViewThroughConversions</td>
</tr>
<tr class="even">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="even">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="odd">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
<tr class="even">
<td>segments_geo_target_most_specific_location</td>
<td>Resource name of the geo target constant that represents the most specific location.</td>
<td>MostSpecificCriteriaId</td>
</tr>
<tr class="odd">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="even">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="odd">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="even">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: HourlyAccountConversionStats

Google Ads API Resource: [customer](https://developers.google.com/google-ads/api/fields/v21/customer)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="even">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>Conversions</td>
</tr>
<tr class="odd">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="even">
<td>metrics_value_per_conversion</td>
<td>The value of conversions divided by the number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ValuePerConversion</td>
</tr>
<tr class="odd">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="even">
<td>segments_click_type</td>
<td>Click type.</td>
<td>ClickType</td>
</tr>
<tr class="odd">
<td>segments_conversion_action</td>
<td>Resource name of the conversion action.</td>
<td>ConversionTrackerId</td>
</tr>
<tr class="even">
<td>segments_conversion_action_category</td>
<td>Conversion action category.</td>
<td>ConversionCategoryName</td>
</tr>
<tr class="odd">
<td>segments_conversion_action_name</td>
<td>Conversion action name.</td>
<td>ConversionTypeName</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="odd">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="even">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
<tr class="odd">
<td>segments_hour</td>
<td>Hour of day as a number between 0 and 23, inclusive.</td>
<td>HourOfDay</td>
</tr>
<tr class="even">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="odd">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="even">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="odd">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: HourlyAccountStats

Google Ads API Resource: [customer](https://developers.google.com/google-ads/api/fields/v21/customer)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="even">
<td>metrics_active_view_cpm</td>
<td>Average cost of viewable impressions (`active_view_impressions`).</td>
<td>ActiveViewCpm</td>
</tr>
<tr class="odd">
<td>metrics_active_view_ctr</td>
<td>Active view measurable clicks divided by active view viewable impressions. This metric is reported only for display network.</td>
<td>ActiveViewCtr</td>
</tr>
<tr class="even">
<td>metrics_active_view_impressions</td>
<td>A measurement of how often your ad has become viewable on a Display Network site.</td>
<td>ActiveViewImpressions</td>
</tr>
<tr class="odd">
<td>metrics_active_view_measurability</td>
<td>The ratio of impressions that could be measured by Active View over the number of served impressions.</td>
<td>ActiveViewMeasurability</td>
</tr>
<tr class="even">
<td>metrics_active_view_measurable_cost_micros</td>
<td>The cost of the impressions you received that were measurable by Active View.</td>
<td>ActiveViewMeasurableCost</td>
</tr>
<tr class="odd">
<td>metrics_active_view_measurable_impressions</td>
<td>The number of times your ads are appearing on placements in positions where they can be seen.</td>
<td>ActiveViewMeasurableImpressions</td>
</tr>
<tr class="even">
<td>metrics_active_view_viewability</td>
<td>The percentage of time when your ad appeared on an Active View enabled site (measurable impressions) and was viewable (viewable impressions).</td>
<td>ActiveViewViewability</td>
</tr>
<tr class="odd">
<td>metrics_average_cost</td>
<td>The average amount you pay per interaction. This amount is the total cost of your ads divided by the total number of interactions.</td>
<td>AverageCost</td>
</tr>
<tr class="even">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
<td>AverageCpc</td>
</tr>
<tr class="odd">
<td>metrics_average_cpm</td>
<td>Average cost-per-thousand impressions (CPM).</td>
<td>AverageCpm</td>
</tr>
<tr class="even">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
<td>Clicks</td>
</tr>
<tr class="odd">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>Conversions</td>
</tr>
<tr class="even">
<td>metrics_conversions_from_interactions_rate</td>
<td>Conversions from interactions divided by the number of ad interactions (such as clicks for text ads or views for video ads). This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionRate</td>
</tr>
<tr class="odd">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="even">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
<td>Cost</td>
</tr>
<tr class="odd">
<td>metrics_cost_per_conversion</td>
<td>The cost of ad interactions divided by conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>CostPerConversion</td>
</tr>
<tr class="even">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
<td>Ctr</td>
</tr>
<tr class="odd">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
<td>Impressions</td>
</tr>
<tr class="even">
<td>metrics_interaction_event_types</td>
<td>The types of payable and free interactions.</td>
<td>InteractionTypes</td>
</tr>
<tr class="odd">
<td>metrics_interaction_rate</td>
<td>How often people interact with your ad after it is shown to them. This is the number of interactions divided by the number of times your ad is shown.</td>
<td>InteractionRate</td>
</tr>
<tr class="even">
<td>metrics_interactions</td>
<td>The number of interactions. An interaction is the main user action associated with an ad format, such as clicks for text and shopping ads or views for video ads.</td>
<td>Interactions</td>
</tr>
<tr class="odd">
<td>metrics_value_per_conversion</td>
<td>The value of conversions divided by the number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ValuePerConversion</td>
</tr>
<tr class="even">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="odd">
<td>segments_click_type</td>
<td>Click type.</td>
<td>ClickType</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="odd">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="even">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
<tr class="odd">
<td>segments_hour</td>
<td>Hour of day as a number between 0 and 23, inclusive.</td>
<td>HourOfDay</td>
</tr>
<tr class="even">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="odd">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="even">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="odd">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: HourlyAdGroupConversionStats

Google Ads API Resource: [ad\_group](https://developers.google.com/google-ads/api/fields/v21/ad_group)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_base_ad_group</td>
<td>For draft or experiment ad groups, this field is the resource name of the base ad group from which this ad group was created. If a draft or experiment ad group does not have a base ad group, then this field is null. For base ad groups, this field equals the ad group resource name. This field is read-only.</td>
<td>BaseAdGroupId</td>
</tr>
<tr class="even">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="odd">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td>BaseCampaignId</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="even">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>Conversions</td>
</tr>
<tr class="odd">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="even">
<td>metrics_value_per_conversion</td>
<td>The value of conversions divided by the number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ValuePerConversion</td>
</tr>
<tr class="odd">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="even">
<td>segments_click_type</td>
<td>Click type.</td>
<td>ClickType</td>
</tr>
<tr class="odd">
<td>segments_conversion_action</td>
<td>Resource name of the conversion action.</td>
<td>ConversionTrackerId</td>
</tr>
<tr class="even">
<td>segments_conversion_action_category</td>
<td>Conversion action category.</td>
<td>ConversionCategoryName</td>
</tr>
<tr class="odd">
<td>segments_conversion_action_name</td>
<td>Conversion action name.</td>
<td>ConversionTypeName</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="odd">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="even">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
<tr class="odd">
<td>segments_hour</td>
<td>Hour of day as a number between 0 and 23, inclusive.</td>
<td>HourOfDay</td>
</tr>
<tr class="even">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="odd">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="even">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="odd">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: HourlyAdGroupStats

Google Ads API Resource: [ad\_group](https://developers.google.com/google-ads/api/fields/v21/ad_group)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_base_ad_group</td>
<td>For draft or experiment ad groups, this field is the resource name of the base ad group from which this ad group was created. If a draft or experiment ad group does not have a base ad group, then this field is null. For base ad groups, this field equals the ad group resource name. This field is read-only.</td>
<td>BaseAdGroupId</td>
</tr>
<tr class="even">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="odd">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td>BaseCampaignId</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="even">
<td>metrics_active_view_cpm</td>
<td>Average cost of viewable impressions (`active_view_impressions`).</td>
<td>ActiveViewCpm</td>
</tr>
<tr class="odd">
<td>metrics_active_view_ctr</td>
<td>Active view measurable clicks divided by active view viewable impressions. This metric is reported only for display network.</td>
<td>ActiveViewCtr</td>
</tr>
<tr class="even">
<td>metrics_active_view_impressions</td>
<td>A measurement of how often your ad has become viewable on a Display Network site.</td>
<td>ActiveViewImpressions</td>
</tr>
<tr class="odd">
<td>metrics_active_view_measurability</td>
<td>The ratio of impressions that could be measured by Active View over the number of served impressions.</td>
<td>ActiveViewMeasurability</td>
</tr>
<tr class="even">
<td>metrics_active_view_measurable_cost_micros</td>
<td>The cost of the impressions you received that were measurable by Active View.</td>
<td>ActiveViewMeasurableCost</td>
</tr>
<tr class="odd">
<td>metrics_active_view_measurable_impressions</td>
<td>The number of times your ads are appearing on placements in positions where they can be seen.</td>
<td>ActiveViewMeasurableImpressions</td>
</tr>
<tr class="even">
<td>metrics_active_view_viewability</td>
<td>The percentage of time when your ad appeared on an Active View enabled site (measurable impressions) and was viewable (viewable impressions).</td>
<td>ActiveViewViewability</td>
</tr>
<tr class="odd">
<td>metrics_average_cost</td>
<td>The average amount you pay per interaction. This amount is the total cost of your ads divided by the total number of interactions.</td>
<td>AverageCost</td>
</tr>
<tr class="even">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
<td>AverageCpc</td>
</tr>
<tr class="odd">
<td>metrics_average_cpm</td>
<td>Average cost-per-thousand impressions (CPM).</td>
<td>AverageCpm</td>
</tr>
<tr class="even">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
<td>Clicks</td>
</tr>
<tr class="odd">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>Conversions</td>
</tr>
<tr class="even">
<td>metrics_conversions_from_interactions_rate</td>
<td>Conversions from interactions divided by the number of ad interactions (such as clicks for text ads or views for video ads). This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionRate</td>
</tr>
<tr class="odd">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="even">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
<td>Cost</td>
</tr>
<tr class="odd">
<td>metrics_cost_per_conversion</td>
<td>The cost of ad interactions divided by conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>CostPerConversion</td>
</tr>
<tr class="even">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
<td>Ctr</td>
</tr>
<tr class="odd">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
<td>Impressions</td>
</tr>
<tr class="even">
<td>metrics_interaction_event_types</td>
<td>The types of payable and free interactions.</td>
<td>InteractionTypes</td>
</tr>
<tr class="odd">
<td>metrics_interaction_rate</td>
<td>How often people interact with your ad after it is shown to them. This is the number of interactions divided by the number of times your ad is shown.</td>
<td>InteractionRate</td>
</tr>
<tr class="even">
<td>metrics_interactions</td>
<td>The number of interactions. An interaction is the main user action associated with an ad format, such as clicks for text and shopping ads or views for video ads.</td>
<td>Interactions</td>
</tr>
<tr class="odd">
<td>metrics_value_per_conversion</td>
<td>The value of conversions divided by the number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ValuePerConversion</td>
</tr>
<tr class="even">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="odd">
<td>segments_click_type</td>
<td>Click type.</td>
<td>ClickType</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="odd">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="even">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
<tr class="odd">
<td>segments_hour</td>
<td>Hour of day as a number between 0 and 23, inclusive.</td>
<td>HourOfDay</td>
</tr>
<tr class="even">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="odd">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="even">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="odd">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: HourlyBidGoalStats

Google Ads API Resource: [bidding\_strategy](https://developers.google.com/google-ads/api/fields/v21/bidding_strategy)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>bidding_strategy_campaign_count</td>
<td>The number of campaigns attached to this bidding strategy. This field is read-only.</td>
<td>CampaignCount</td>
</tr>
<tr class="even">
<td>bidding_strategy_id</td>
<td>The ID of the bidding strategy.</td>
<td>BidStrategyID</td>
</tr>
<tr class="odd">
<td>bidding_strategy_non_removed_campaign_count</td>
<td>The number of non-removed campaigns attached to this bidding strategy. This field is read-only.</td>
<td>NonRemovedCampaignCount</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="odd">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
<td>AverageCpc</td>
</tr>
<tr class="even">
<td>metrics_average_cpm</td>
<td>Average cost-per-thousand impressions (CPM).</td>
<td>AverageCpm</td>
</tr>
<tr class="odd">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
<td>Clicks</td>
</tr>
<tr class="even">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>Conversions</td>
</tr>
<tr class="odd">
<td>metrics_conversions_from_interactions_rate</td>
<td>Conversions from interactions divided by the number of ad interactions (such as clicks for text ads or views for video ads). This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionRate</td>
</tr>
<tr class="even">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="odd">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
<td>Cost</td>
</tr>
<tr class="even">
<td>metrics_cost_per_conversion</td>
<td>The cost of ad interactions divided by conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>CostPerConversion</td>
</tr>
<tr class="odd">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
<td>Ctr</td>
</tr>
<tr class="even">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
<td>Impressions</td>
</tr>
<tr class="odd">
<td>metrics_value_per_conversion</td>
<td>The value of conversions divided by the number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ValuePerConversion</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="odd">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="even">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
<tr class="odd">
<td>segments_hour</td>
<td>Hour of day as a number between 0 and 23, inclusive.</td>
<td>HourOfDay</td>
</tr>
<tr class="even">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="odd">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="even">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="odd">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: HourlyCampaignConversionStats

Google Ads API Resource: [campaign](https://developers.google.com/google-ads/api/fields/v21/campaign)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td>BaseCampaignId</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="even">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>Conversions</td>
</tr>
<tr class="odd">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="even">
<td>metrics_value_per_conversion</td>
<td>The value of conversions divided by the number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ValuePerConversion</td>
</tr>
<tr class="odd">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="even">
<td>segments_click_type</td>
<td>Click type.</td>
<td>ClickType</td>
</tr>
<tr class="odd">
<td>segments_conversion_action</td>
<td>Resource name of the conversion action.</td>
<td>ConversionTrackerId</td>
</tr>
<tr class="even">
<td>segments_conversion_action_category</td>
<td>Conversion action category.</td>
<td>ConversionCategoryName</td>
</tr>
<tr class="odd">
<td>segments_conversion_action_name</td>
<td>Conversion action name.</td>
<td>ConversionTypeName</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="odd">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="even">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
<tr class="odd">
<td>segments_hour</td>
<td>Hour of day as a number between 0 and 23, inclusive.</td>
<td>HourOfDay</td>
</tr>
<tr class="even">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="odd">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="even">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="odd">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: HourlyCampaignStats

Google Ads API Resource: [campaign](https://developers.google.com/google-ads/api/fields/v21/campaign)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td>BaseCampaignId</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="even">
<td>metrics_active_view_cpm</td>
<td>Average cost of viewable impressions (`active_view_impressions`).</td>
<td>ActiveViewCpm</td>
</tr>
<tr class="odd">
<td>metrics_active_view_ctr</td>
<td>Active view measurable clicks divided by active view viewable impressions. This metric is reported only for display network.</td>
<td>ActiveViewCtr</td>
</tr>
<tr class="even">
<td>metrics_active_view_impressions</td>
<td>A measurement of how often your ad has become viewable on a Display Network site.</td>
<td>ActiveViewImpressions</td>
</tr>
<tr class="odd">
<td>metrics_active_view_measurability</td>
<td>The ratio of impressions that could be measured by Active View over the number of served impressions.</td>
<td>ActiveViewMeasurability</td>
</tr>
<tr class="even">
<td>metrics_active_view_measurable_cost_micros</td>
<td>The cost of the impressions you received that were measurable by Active View.</td>
<td>ActiveViewMeasurableCost</td>
</tr>
<tr class="odd">
<td>metrics_active_view_measurable_impressions</td>
<td>The number of times your ads are appearing on placements in positions where they can be seen.</td>
<td>ActiveViewMeasurableImpressions</td>
</tr>
<tr class="even">
<td>metrics_active_view_viewability</td>
<td>The percentage of time when your ad appeared on an Active View enabled site (measurable impressions) and was viewable (viewable impressions).</td>
<td>ActiveViewViewability</td>
</tr>
<tr class="odd">
<td>metrics_average_cost</td>
<td>The average amount you pay per interaction. This amount is the total cost of your ads divided by the total number of interactions.</td>
<td>AverageCost</td>
</tr>
<tr class="even">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
<td>AverageCpc</td>
</tr>
<tr class="odd">
<td>metrics_average_cpm</td>
<td>Average cost-per-thousand impressions (CPM).</td>
<td>AverageCpm</td>
</tr>
<tr class="even">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
<td>Clicks</td>
</tr>
<tr class="odd">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>Conversions</td>
</tr>
<tr class="even">
<td>metrics_conversions_from_interactions_rate</td>
<td>Conversions from interactions divided by the number of ad interactions (such as clicks for text ads or views for video ads). This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionRate</td>
</tr>
<tr class="odd">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="even">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
<td>Cost</td>
</tr>
<tr class="odd">
<td>metrics_cost_per_conversion</td>
<td>The cost of ad interactions divided by conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>CostPerConversion</td>
</tr>
<tr class="even">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
<td>Ctr</td>
</tr>
<tr class="odd">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
<td>Impressions</td>
</tr>
<tr class="even">
<td>metrics_interaction_event_types</td>
<td>The types of payable and free interactions.</td>
<td>InteractionTypes</td>
</tr>
<tr class="odd">
<td>metrics_interaction_rate</td>
<td>How often people interact with your ad after it is shown to them. This is the number of interactions divided by the number of times your ad is shown.</td>
<td>InteractionRate</td>
</tr>
<tr class="even">
<td>metrics_interactions</td>
<td>The number of interactions. An interaction is the main user action associated with an ad format, such as clicks for text and shopping ads or views for video ads.</td>
<td>Interactions</td>
</tr>
<tr class="odd">
<td>metrics_value_per_conversion</td>
<td>The value of conversions divided by the number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ValuePerConversion</td>
</tr>
<tr class="even">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="odd">
<td>segments_click_type</td>
<td>Click type.</td>
<td>ClickType</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="odd">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="even">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
<tr class="odd">
<td>segments_hour</td>
<td>Hour of day as a number between 0 and 23, inclusive.</td>
<td>HourOfDay</td>
</tr>
<tr class="even">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="odd">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="even">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="odd">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: Keyword

Google Ads API Resource: [keyword\_view](https://developers.google.com/google-ads/api/fields/v21/keyword_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_criterion_approval_status</td>
<td>Approval status of the criterion.</td>
<td>ApprovalStatus</td>
</tr>
<tr class="even">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion. This field is ignored for mutates.</td>
<td>CriterionId</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_effective_cpc_bid_micros</td>
<td>The effective CPC (cost-per-click) bid.</td>
<td>CpcBid</td>
</tr>
<tr class="even">
<td>ad_group_criterion_effective_cpc_bid_source</td>
<td>Source of the effective CPC bid.</td>
<td>CpcBidSource</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_effective_cpm_bid_micros</td>
<td>The effective CPM (cost-per-thousand viewable impressions) bid.</td>
<td>CpmBidStr</td>
</tr>
<tr class="even">
<td>ad_group_criterion_final_mobile_urls</td>
<td>The list of possible final mobile URLs after all cross-domain redirects.</td>
<td>FinalMobileUrls</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_final_url_suffix</td>
<td>URL template for appending params to final URL.</td>
<td>FinalUrlSuffix</td>
</tr>
<tr class="even">
<td>ad_group_criterion_final_urls</td>
<td>The list of possible final URLs after all cross-domain redirects for the ad.</td>
<td>FinalUrls</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_keyword_match_type</td>
<td>The match type of the keyword.</td>
<td>KeywordMatchType</td>
</tr>
<tr class="even">
<td>ad_group_criterion_keyword_text</td>
<td>The text of the keyword (at most 80 characters and 10 words).</td>
<td>Criteria</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_negative</td>
<td>Whether to target (`false`) or exclude (`true`) the criterion. This field is immutable. To switch a criterion from positive to negative, remove then re-add it.</td>
<td>IsNegative</td>
</tr>
<tr class="even">
<td>ad_group_criterion_position_estimates_estimated_add_clicks_at_first_position_cpc</td>
<td>Estimate of how many clicks per week you might get by changing your keyword bid to the value in first_position_cpc_micros.</td>
<td>EstimatedAddClicksAtFirstPositionCpc</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_position_estimates_estimated_add_cost_at_first_position_cpc</td>
<td>Estimate of how your cost per week might change when changing your keyword bid to the value in first_position_cpc_micros.</td>
<td>EstimatedAddCostAtFirstPositionCpc</td>
</tr>
<tr class="even">
<td>ad_group_criterion_position_estimates_first_page_cpc_micros</td>
<td>The estimate of the CPC bid required for ad to be shown on first page of search results.</td>
<td>FirstPageCpc</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_position_estimates_first_position_cpc_micros</td>
<td>The estimate of the CPC bid required for ad to be displayed in first position, at the top of the first page of search results.</td>
<td>FirstPositionCpc</td>
</tr>
<tr class="even">
<td>ad_group_criterion_position_estimates_top_of_page_cpc_micros</td>
<td>The estimate of the CPC bid required for ad to be displayed at the top of the first page of search results.</td>
<td>TopOfPageCpc</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_quality_info_creative_quality_score</td>
<td>The performance of the ad compared to other advertisers.</td>
<td>CreativeQualityScore</td>
</tr>
<tr class="even">
<td>ad_group_criterion_quality_info_post_click_quality_score</td>
<td>The quality score of the landing page.</td>
<td>PostClickQualityScore</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_quality_info_quality_score</td>
<td>The quality score. This field may not be populated if Google does not have enough information to determine a value.</td>
<td>QualityScore</td>
</tr>
<tr class="even">
<td>ad_group_criterion_quality_info_search_predicted_ctr</td>
<td>The click-through rate compared to that of other advertisers.</td>
<td>SearchPredictedCtr</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_status</td>
<td>The status of the criterion.</td>
<td>Status</td>
</tr>
<tr class="even">
<td>ad_group_criterion_system_serving_status</td>
<td>Serving status of the criterion.</td>
<td>SystemServingStatus</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_topic_topic_constant</td>
<td>The Topic Constant resource name.</td>
<td>VerticalId</td>
</tr>
<tr class="even">
<td>ad_group_criterion_tracking_url_template</td>
<td>The URL template for constructing a tracking URL.</td>
<td>TrackingUrlTemplate</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_url_custom_parameters</td>
<td>The list of mappings used to substitute custom parameter tags in a `tracking_url_template`, `final_urls`, or `mobile_final_urls`.</td>
<td>UrlCustomParameters</td>
</tr>
<tr class="even">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="odd">
<td>campaign_bidding_strategy</td>
<td>Portfolio bidding strategy used by campaign.</td>
<td>BiddingStrategyId</td>
</tr>
<tr class="even">
<td>campaign_bidding_strategy_type</td>
<td>The type of bidding strategy. A bidding strategy can be created by setting either the bidding scheme to create a standard bidding strategy or the `bidding_strategy` field to create a portfolio bidding strategy. This field is read-only.</td>
<td>BiddingStrategyType</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="even">
<td>campaign_manual_cpc_enhanced_cpc_enabled</td>
<td>Whether bids are to be enhanced based on conversion optimizer data.</td>
<td>EnhancedCpcEnabled</td>
</tr>
<tr class="odd">
<td>campaign_percent_cpc_enhanced_cpc_enabled</td>
<td>Adjusts the bid for each auction upward or downward, depending on the likelihood of a conversion. Individual bids may exceed cpc_bid_ceiling_micros, but the average bid amount for a campaign shouldn't.</td>
<td></td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
</tbody>
</table>

Google Ads Table Name: KeywordBasicStats

Google Ads API Resource: [keyword\_view](https://developers.google.com/google-ads/api/fields/v21/keyword_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_base_ad_group</td>
<td>For draft or experiment ad groups, this field is the resource name of the base ad group from which this ad group was created. If a draft or experiment ad group does not have a base ad group, then this field is null. For base ad groups, this field equals the ad group resource name. This field is read-only.</td>
<td>BaseAdGroupId</td>
</tr>
<tr class="even">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion. This field is ignored for mutates.</td>
<td>CriterionId</td>
</tr>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="even">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td>BaseCampaignId</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="odd">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
<td>Clicks</td>
</tr>
<tr class="even">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>Conversions</td>
</tr>
<tr class="odd">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="even">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
<td>Cost</td>
</tr>
<tr class="odd">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
<td>Impressions</td>
</tr>
<tr class="even">
<td>metrics_interaction_event_types</td>
<td>The types of payable and free interactions.</td>
<td>InteractionTypes</td>
</tr>
<tr class="odd">
<td>metrics_interactions</td>
<td>The number of interactions. An interaction is the main user action associated with an ad format, such as clicks for text and shopping ads or views for video ads.</td>
<td>Interactions</td>
</tr>
<tr class="even">
<td>metrics_view_through_conversions</td>
<td>The total number of view-through conversions. These happen when a customer sees an image or rich media ad, then later completes a conversion on your site without interacting with (for example, clicking on) another ad.</td>
<td>ViewThroughConversions</td>
</tr>
<tr class="odd">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="odd">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
<tr class="even">
<td>segments_slot</td>
<td>Position of the ad.</td>
<td>Slot</td>
</tr>
</tbody>
</table>

Google Ads Table Name: KeywordConversionStats

Google Ads API Resource: [keyword\_view](https://developers.google.com/google-ads/api/fields/v21/keyword_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_base_ad_group</td>
<td>For draft or experiment ad groups, this field is the resource name of the base ad group from which this ad group was created. If a draft or experiment ad group does not have a base ad group, then this field is null. For base ad groups, this field equals the ad group resource name. This field is read-only.</td>
<td>BaseAdGroupId</td>
</tr>
<tr class="even">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion. This field is ignored for mutates.</td>
<td>CriterionId</td>
</tr>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="even">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td>BaseCampaignId</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="odd">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>Conversions</td>
</tr>
<tr class="even">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="odd">
<td>metrics_value_per_conversion</td>
<td>The value of conversions divided by the number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ValuePerConversion</td>
</tr>
<tr class="even">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="odd">
<td>segments_click_type</td>
<td>Click type.</td>
<td>ClickType</td>
</tr>
<tr class="even">
<td>segments_conversion_action</td>
<td>Resource name of the conversion action.</td>
<td>ConversionTrackerId</td>
</tr>
<tr class="odd">
<td>segments_conversion_action_category</td>
<td>Conversion action category.</td>
<td>ConversionCategoryName</td>
</tr>
<tr class="even">
<td>segments_conversion_action_name</td>
<td>Conversion action name.</td>
<td>ConversionTypeName</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="even">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="odd">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
<tr class="even">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="odd">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="even">
<td>segments_slot</td>
<td>Position of the ad.</td>
<td>Slot</td>
</tr>
<tr class="odd">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="even">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: KeywordCrossDeviceConversionStats

Google Ads API Resource: [keyword\_view](https://developers.google.com/google-ads/api/fields/v21/keyword_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_base_ad_group</td>
<td>For draft or experiment ad groups, this field is the resource name of the base ad group from which this ad group was created. If a draft or experiment ad group does not have a base ad group, then this field is null. For base ad groups, this field equals the ad group resource name. This field is read-only.</td>
<td>BaseAdGroupId</td>
</tr>
<tr class="even">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion. This field is ignored for mutates.</td>
<td>CriterionId</td>
</tr>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="even">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td>BaseCampaignId</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>AllConversions</td>
</tr>
<tr class="even">
<td>metrics_all_conversions_value</td>
<td>The total value of all conversions.</td>
<td>AllConversionValue</td>
</tr>
<tr class="odd">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on a Google Ads ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
<td>CrossDeviceConversions</td>
</tr>
<tr class="even">
<td>metrics_value_per_all_conversions</td>
<td>The value of all conversions divided by the number of all conversions.</td>
<td>ValuePerAllConversion</td>
</tr>
<tr class="odd">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="even">
<td>segments_conversion_action</td>
<td>Resource name of the conversion action.</td>
<td>ConversionTrackerId</td>
</tr>
<tr class="odd">
<td>segments_conversion_action_category</td>
<td>Conversion action category.</td>
<td>ConversionCategoryName</td>
</tr>
<tr class="even">
<td>segments_conversion_action_name</td>
<td>Conversion action name.</td>
<td>ConversionTypeName</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="even">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="odd">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="even">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="odd">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="even">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: KeywordCrossDeviceStats

Google Ads API Resource: [keyword\_view](https://developers.google.com/google-ads/api/fields/v21/keyword_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_base_ad_group</td>
<td>For draft or experiment ad groups, this field is the resource name of the base ad group from which this ad group was created. If a draft or experiment ad group does not have a base ad group, then this field is null. For base ad groups, this field equals the ad group resource name. This field is read-only.</td>
<td>BaseAdGroupId</td>
</tr>
<tr class="even">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion. This field is ignored for mutates.</td>
<td>CriterionId</td>
</tr>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="even">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td>BaseCampaignId</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="odd">
<td>metrics_absolute_top_impression_percentage</td>
<td>The percent of your ad impressions that are shown as the very first ad above the organic search results.</td>
<td>AbsoluteTopImpressionPercentage</td>
</tr>
<tr class="even">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>AllConversions</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions_from_interactions_rate</td>
<td>All conversions from interactions (as oppose to view through conversions) divided by the number of ad interactions.</td>
<td>AllConversionRate</td>
</tr>
<tr class="even">
<td>metrics_all_conversions_value</td>
<td>The total value of all conversions.</td>
<td>AllConversionValue</td>
</tr>
<tr class="odd">
<td>metrics_average_cpe</td>
<td>The average amount that you've been charged for an ad engagement. This amount is the total cost of all ad engagements divided by the total number of ad engagements.</td>
<td>AverageCpe</td>
</tr>
<tr class="even">
<td>metrics_average_cpv</td>
<td>The average amount you pay each time someone views your ad. The average CPV is defined by the total cost of all ad views divided by the number of views.</td>
<td>AverageCpv</td>
</tr>
<tr class="odd">
<td>metrics_average_page_views</td>
<td>Average number of pages viewed per session.</td>
<td>AveragePageviews</td>
</tr>
<tr class="even">
<td>metrics_average_time_on_site</td>
<td>Total duration of all sessions (in seconds) / number of sessions. Imported from Google Analytics.</td>
<td>AverageTimeOnSite</td>
</tr>
<tr class="odd">
<td>metrics_bounce_rate</td>
<td>Percentage of clicks where the user only visited a single page on your site. Imported from Google Analytics.</td>
<td>BounceRate</td>
</tr>
<tr class="even">
<td>metrics_cost_per_all_conversions</td>
<td>The cost of ad interactions divided by all conversions.</td>
<td>CostPerAllConversion</td>
</tr>
<tr class="odd">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on a Google Ads ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
<td>CrossDeviceConversions</td>
</tr>
<tr class="even">
<td>metrics_engagement_rate</td>
<td>How often people engage with your ad after it's shown to them. This is the number of ad expansions divided by the number of times your ad is shown.</td>
<td>EngagementRate</td>
</tr>
<tr class="odd">
<td>metrics_engagements</td>
<td>The number of engagements. An engagement occurs when a viewer expands your Lightbox ad. Also, in the future, other ad types may support engagement metrics.</td>
<td>Engagements</td>
</tr>
<tr class="even">
<td>metrics_percent_new_visitors</td>
<td>Percentage of first-time sessions (from people who had never visited your site before). Imported from Google Analytics.</td>
<td>PercentNewVisitors</td>
</tr>
<tr class="odd">
<td>metrics_search_absolute_top_impression_share</td>
<td>The percentage of the customer's Shopping or Search ad impressions that are shown in the most prominent Shopping position. See https://support.google.com/google-ads/answer/7501826 for details. Any value below 0.1 is reported as 0.0999.</td>
<td>SearchAbsoluteTopImpressionShare</td>
</tr>
<tr class="even">
<td>metrics_search_budget_lost_absolute_top_impression_share</td>
<td>The number estimating how often your ad wasn't the very first ad above the organic search results due to a low budget. Note: Search budget lost absolute top impression share is reported in the range of 0 to 0.9. Any value above 0.9 is reported as 0.9001.</td>
<td>SearchBudgetLostAbsoluteTopImpressionShare</td>
</tr>
<tr class="odd">
<td>metrics_search_budget_lost_top_impression_share</td>
<td>The number estimating how often your ad didn't show anywhere above the organic search results due to a low budget. Note: Search budget lost top impression share is reported in the range of 0 to 0.9. Any value above 0.9 is reported as 0.9001.</td>
<td>SearchBudgetLostTopImpressionShare</td>
</tr>
<tr class="even">
<td>metrics_search_exact_match_impression_share</td>
<td>The impressions you've received divided by the estimated number of impressions you were eligible to receive on the Search Network for search terms that matched your keywords exactly (or were close variants of your keyword), regardless of your keyword match types. Note: Search exact match impression share is reported in the range of 0.1 to 1. Any value below 0.1 is reported as 0.0999.</td>
<td>SearchExactMatchImpressionShare</td>
</tr>
<tr class="odd">
<td>metrics_search_impression_share</td>
<td>The impressions you've received on the Search Network divided by the estimated number of impressions you were eligible to receive. Note: Search impression share is reported in the range of 0.1 to 1. Any value below 0.1 is reported as 0.0999.</td>
<td>SearchImpressionShare</td>
</tr>
<tr class="even">
<td>metrics_search_rank_lost_absolute_top_impression_share</td>
<td>The number estimating how often your ad wasn't the very first ad above the organic search results due to poor Ad Rank. Note: Search rank lost absolute top impression share is reported in the range of 0 to 0.9. Any value above 0.9 is reported as 0.9001.</td>
<td>SearchRankLostAbsoluteTopImpressionShare</td>
</tr>
<tr class="odd">
<td>metrics_search_rank_lost_impression_share</td>
<td>The estimated percentage of impressions on the Search Network that your ads didn't receive due to poor Ad Rank. Note: Search rank lost impression share is reported in the range of 0 to 0.9. Any value above 0.9 is reported as 0.9001.</td>
<td>SearchRankLostImpressionShare</td>
</tr>
<tr class="even">
<td>metrics_search_rank_lost_top_impression_share</td>
<td>The number estimating how often your ad didn't show anywhere above the organic search results due to poor Ad Rank. Note: Search rank lost top impression share is reported in the range of 0 to 0.9. Any value above 0.9 is reported as 0.9001.</td>
<td>SearchRankLostTopImpressionShare</td>
</tr>
<tr class="odd">
<td>metrics_search_top_impression_share</td>
<td>The impressions you've received in the top location (anywhere above the organic search results) compared to the estimated number of impressions you were eligible to receive in the top location. Note: Search top impression share is reported in the range of 0.1 to 1. Any value below 0.1 is reported as 0.0999.</td>
<td>SearchTopImpressionShare</td>
</tr>
<tr class="even">
<td>metrics_top_impression_percentage</td>
<td>The percent of your ad impressions that are shown anywhere above the organic search results.</td>
<td>TopImpressionPercentage</td>
</tr>
<tr class="odd">
<td>metrics_value_per_all_conversions</td>
<td>The value of all conversions divided by the number of all conversions.</td>
<td>ValuePerAllConversion</td>
</tr>
<tr class="even">
<td>metrics_video_quartile_p100_rate</td>
<td>Percentage of impressions where the viewer watched all of your video.</td>
<td>VideoQuartile100Rate</td>
</tr>
<tr class="odd">
<td>metrics_video_quartile_p25_rate</td>
<td>Percentage of impressions where the viewer watched 25% of your video.</td>
<td>VideoQuartile25Rate</td>
</tr>
<tr class="even">
<td>metrics_video_quartile_p50_rate</td>
<td>Percentage of impressions where the viewer watched 50% of your video.</td>
<td>VideoQuartile50Rate</td>
</tr>
<tr class="odd">
<td>metrics_video_quartile_p75_rate</td>
<td>Percentage of impressions where the viewer watched 75% of your video.</td>
<td>VideoQuartile75Rate</td>
</tr>
<tr class="even">
<td>metrics_video_view_rate</td>
<td>The number of views your TrueView video ad receives divided by its number of impressions, including thumbnail impressions for TrueView in-display ads.</td>
<td>VideoViewRate</td>
</tr>
<tr class="odd">
<td>metrics_video_views</td>
<td>The number of times your video ads were viewed.</td>
<td>VideoViews</td>
</tr>
<tr class="even">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="even">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="odd">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="even">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="odd">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="even">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: KeywordStats

Google Ads API Resource: [keyword\_view](https://developers.google.com/google-ads/api/fields/v21/keyword_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_base_ad_group</td>
<td>For draft or experiment ad groups, this field is the resource name of the base ad group from which this ad group was created. If a draft or experiment ad group does not have a base ad group, then this field is null. For base ad groups, this field equals the ad group resource name. This field is read-only.</td>
<td>BaseAdGroupId</td>
</tr>
<tr class="even">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion. This field is ignored for mutates.</td>
<td>CriterionId</td>
</tr>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="even">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td>BaseCampaignId</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="odd">
<td>metrics_active_view_cpm</td>
<td>Average cost of viewable impressions (`active_view_impressions`).</td>
<td>ActiveViewCpm</td>
</tr>
<tr class="even">
<td>metrics_active_view_ctr</td>
<td>Active view measurable clicks divided by active view viewable impressions. This metric is reported only for display network.</td>
<td>ActiveViewCtr</td>
</tr>
<tr class="odd">
<td>metrics_active_view_impressions</td>
<td>A measurement of how often your ad has become viewable on a Display Network site.</td>
<td>ActiveViewImpressions</td>
</tr>
<tr class="even">
<td>metrics_active_view_measurability</td>
<td>The ratio of impressions that could be measured by Active View over the number of served impressions.</td>
<td>ActiveViewMeasurability</td>
</tr>
<tr class="odd">
<td>metrics_active_view_measurable_cost_micros</td>
<td>The cost of the impressions you received that were measurable by Active View.</td>
<td>ActiveViewMeasurableCost</td>
</tr>
<tr class="even">
<td>metrics_active_view_measurable_impressions</td>
<td>The number of times your ads are appearing on placements in positions where they can be seen.</td>
<td>ActiveViewMeasurableImpressions</td>
</tr>
<tr class="odd">
<td>metrics_active_view_viewability</td>
<td>The percentage of time when your ad appeared on an Active View enabled site (measurable impressions) and was viewable (viewable impressions).</td>
<td>ActiveViewViewability</td>
</tr>
<tr class="even">
<td>metrics_average_cost</td>
<td>The average amount you pay per interaction. This amount is the total cost of your ads divided by the total number of interactions.</td>
<td>AverageCost</td>
</tr>
<tr class="odd">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
<td>AverageCpc</td>
</tr>
<tr class="even">
<td>metrics_average_cpm</td>
<td>Average cost-per-thousand impressions (CPM).</td>
<td>AverageCpm</td>
</tr>
<tr class="odd">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
<td>Clicks</td>
</tr>
<tr class="even">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>Conversions</td>
</tr>
<tr class="odd">
<td>metrics_conversions_from_interactions_rate</td>
<td>Conversions from interactions divided by the number of ad interactions (such as clicks for text ads or views for video ads). This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionRate</td>
</tr>
<tr class="even">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="odd">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
<td>Cost</td>
</tr>
<tr class="even">
<td>metrics_cost_per_conversion</td>
<td>The cost of ad interactions divided by conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>CostPerConversion</td>
</tr>
<tr class="odd">
<td>metrics_cost_per_current_model_attributed_conversion</td>
<td>The cost of ad interactions divided by current model attributed conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>CostPerCurrentModelAttributedConversion</td>
</tr>
<tr class="even">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
<td>Ctr</td>
</tr>
<tr class="odd">
<td>metrics_current_model_attributed_conversions</td>
<td>Shows how your historic conversions data would look under the attribution model you've selected. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>CurrentModelAttributedConversions</td>
</tr>
<tr class="even">
<td>metrics_current_model_attributed_conversions_value</td>
<td>The total value of current model attributed conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>CurrentModelAttributedConversionValue</td>
</tr>
<tr class="odd">
<td>metrics_gmail_forwards</td>
<td>The number of times the ad was forwarded to someone else as a message.</td>
<td>GmailForwards</td>
</tr>
<tr class="even">
<td>metrics_gmail_saves</td>
<td>The number of times someone has saved your Gmail ad to their inbox as a message.</td>
<td>GmailSaves</td>
</tr>
<tr class="odd">
<td>metrics_gmail_secondary_clicks</td>
<td>The number of clicks to the landing page on the expanded state of Gmail ads.</td>
<td>GmailSecondaryClicks</td>
</tr>
<tr class="even">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
<td>Impressions</td>
</tr>
<tr class="odd">
<td>metrics_interaction_event_types</td>
<td>The types of payable and free interactions.</td>
<td>InteractionTypes</td>
</tr>
<tr class="even">
<td>metrics_interaction_rate</td>
<td>How often people interact with your ad after it is shown to them. This is the number of interactions divided by the number of times your ad is shown.</td>
<td>InteractionRate</td>
</tr>
<tr class="odd">
<td>metrics_interactions</td>
<td>The number of interactions. An interaction is the main user action associated with an ad format, such as clicks for text and shopping ads or views for video ads.</td>
<td>Interactions</td>
</tr>
<tr class="even">
<td>metrics_value_per_conversion</td>
<td>The value of conversions divided by the number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ValuePerConversion</td>
</tr>
<tr class="odd">
<td>metrics_value_per_current_model_attributed_conversion</td>
<td>The value of current model attributed conversions divided by the number of the conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ValuePerCurrentModelAttributedConversion</td>
</tr>
<tr class="even">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="odd">
<td>segments_click_type</td>
<td>Click type.</td>
<td>ClickType</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="odd">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="even">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
<tr class="odd">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="even">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="odd">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="even">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: LandingPageStats

Google Ads API Resource: [landing\_page\_view](https://developers.google.com/google-ads/api/fields/v21/landing_page_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_name</td>
<td>The name of the ad group. This field is required and shouldn't be empty when creating new ad groups. It must contain fewer than 255 UTF-8 full-width characters. It must not contain any null (code point 0x0), NL line feed (code point 0xA) or carriage return (code point 0xD) characters.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_status</td>
<td>The status of the ad group.</td>
<td></td>
</tr>
<tr class="odd">
<td>campaign_name</td>
<td>The name of the campaign. This field is required and shouldn't be empty when creating new campaigns. It must not contain any null (code point 0x0), NL line feed (code point 0xA) or carriage return (code point 0xD) characters.</td>
<td></td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td></td>
</tr>
<tr class="odd">
<td>landing_page_view_unexpanded_final_url</td>
<td>The advertiser-specified final URL.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_mobile_friendly_clicks_percentage</td>
<td>The percentage of mobile clicks that go to a mobile-friendly page.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_speed_score</td>
<td>A measure of how quickly your page loads after clicks on your mobile ads. The score is a range from 1 to 10, 10 being the fastest.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_valid_accelerated_mobile_pages_clicks_percentage</td>
<td>The percentage of ad clicks to Accelerated Mobile Pages (AMP) landing pages that reach a valid AMP page.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td></td>
</tr>
</tbody>
</table>

Google Ads Table Name: LocationBasedCampaignCriterion

Google Ads API Resource: [location\_view](https://developers.google.com/google-ads/api/fields/v21/location_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>campaign_criterion_bid_modifier</td>
<td>The modifier for the bids when the criterion matches. The modifier must be in the range: 0.1 - 10.0. Most targetable criteria types support modifiers. Use 0 to opt out of a Device type.</td>
<td>BidModifier</td>
</tr>
<tr class="even">
<td>campaign_criterion_criterion_id</td>
<td>The ID of the criterion. This field is ignored during mutate.</td>
<td>CriterionId</td>
</tr>
<tr class="odd">
<td>campaign_criterion_negative</td>
<td>Whether to target (`false`) or exclude (`true`) the criterion.</td>
<td>IsNegative</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
</tbody>
</table>

Google Ads Table Name: LocationsDistanceStats

Google Ads API Resource: [distance\_view](https://developers.google.com/google-ads/api/fields/v21/distance_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td></td>
</tr>
<tr class="even">
<td>distance_view_distance_bucket</td>
<td>Grouping of user distance from location extensions.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_conversions_from_interactions_rate</td>
<td>Conversions from interactions divided by the number of ad interactions (such as clicks for text ads or views for video ads). This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_cost_per_conversion</td>
<td>The cost of ad interactions divided by conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_view_through_conversions</td>
<td>The total number of view-through conversions. These happen when a customer sees an image or rich media ad, then later completes a conversion on your site without interacting with (for example, clicking on) another ad.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td></td>
</tr>
</tbody>
</table>

Google Ads Table Name: LocationsUserLocationsStats

Google Ads API Resource: [user\_location\_view](https://developers.google.com/google-ads/api/fields/v21/user_location_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_conversions_from_interactions_rate</td>
<td>Conversions from interactions divided by the number of ad interactions (such as clicks for text ads or views for video ads). This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_cost_per_conversion</td>
<td>The cost of ad interactions divided by conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_view_through_conversions</td>
<td>The total number of view-through conversions. These happen when a customer sees an image or rich media ad, then later completes a conversion on your site without interacting with (for example, clicking on) another ad.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_geo_target_city</td>
<td>Resource name of the geo target constant that represents a city.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_geo_target_most_specific_location</td>
<td>Resource name of the geo target constant that represents the most specific location.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_geo_target_region</td>
<td>Resource name of the geo target constant that represents a region.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td></td>
</tr>
<tr class="even">
<td>user_location_view_country_criterion_id</td>
<td>Criterion Id for the country.</td>
<td></td>
</tr>
<tr class="odd">
<td>user_location_view_targeting_location</td>
<td>Target location.</td>
<td></td>
</tr>
</tbody>
</table>

Google Ads Table Name: PaidOrganicStats

Google Ads API Resource: [paid\_organic\_search\_term\_view](https://developers.google.com/google-ads/api/fields/v21/paid_organic_search_term_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="even">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
<td>AverageCpc</td>
</tr>
<tr class="odd">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
<td>Clicks</td>
</tr>
<tr class="even">
<td>metrics_combined_clicks</td>
<td>The number of times your ad or your site's listing in the unpaid results was clicked. See the help page at https://support.google.com/google-ads/answer/3097241 for details.</td>
<td>CombinedAdsOrganicClicks</td>
</tr>
<tr class="odd">
<td>metrics_combined_clicks_per_query</td>
<td>The number of times your ad or your site's listing in the unpaid results was clicked (combined_clicks) divided by combined_queries. See the help page at https://support.google.com/google-ads/answer/3097241 for details.</td>
<td>CombinedAdsOrganicClicksPerQuery</td>
</tr>
<tr class="even">
<td>metrics_combined_queries</td>
<td>The number of searches that returned pages from your site in the unpaid results or showed one of your text ads. See the help page at https://support.google.com/google-ads/answer/3097241 for details.</td>
<td>CombinedAdsOrganicQueries</td>
</tr>
<tr class="odd">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
<td>Ctr</td>
</tr>
<tr class="even">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
<td>Impressions</td>
</tr>
<tr class="odd">
<td>metrics_organic_clicks</td>
<td>The number of times someone clicked your site's listing in the unpaid results for a particular query. See the help page at https://support.google.com/google-ads/answer/3097241 for details.</td>
<td>OrganicClicks</td>
</tr>
<tr class="even">
<td>metrics_organic_clicks_per_query</td>
<td>The number of times someone clicked your site's listing in the unpaid results (organic_clicks) divided by the total number of searches that returned pages from your site (organic_queries). See the help page at https://support.google.com/google-ads/answer/3097241 for details.</td>
<td>OrganicClicksPerQuery</td>
</tr>
<tr class="odd">
<td>metrics_organic_impressions</td>
<td>The number of listings for your site in the unpaid search results. See the help page at https://support.google.com/google-ads/answer/3097241 for details.</td>
<td>OrganicImpressions</td>
</tr>
<tr class="even">
<td>metrics_organic_impressions_per_query</td>
<td>The number of times a page from your site was listed in the unpaid search results (organic_impressions) divided by the number of searches returning your site's listing in the unpaid results (organic_queries). See the help page at https://support.google.com/google-ads/answer/3097241 for details.</td>
<td>OrganicImpressionsPerQuery</td>
</tr>
<tr class="odd">
<td>metrics_organic_queries</td>
<td>The total number of searches that returned your site's listing in the unpaid results. See the help page at https://support.google.com/google-ads/answer/3097241 for details.</td>
<td>OrganicQueries</td>
</tr>
<tr class="even">
<td>paid_organic_search_term_view_search_term</td>
<td>The search term.</td>
<td>SearchQuery</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="even">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="odd">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="even">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="odd">
<td>segments_search_engine_results_page_type</td>
<td>Type of the search engine results page.</td>
<td>SerpType</td>
</tr>
<tr class="even">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="odd">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: ParentalStatus

Google Ads API Resource: [parental\_status\_view](https://developers.google.com/google-ads/api/fields/v21/parental_status_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_base_ad_group</td>
<td>For draft or experiment ad groups, this field is the resource name of the base ad group from which this ad group was created. If a draft or experiment ad group does not have a base ad group, then this field is null. For base ad groups, this field equals the ad group resource name. This field is read-only.</td>
<td>BaseAdGroupId</td>
</tr>
<tr class="even">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion. This field is ignored for mutates.</td>
<td>CriterionId</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_effective_cpc_bid_micros</td>
<td>The effective CPC (cost-per-click) bid.</td>
<td>CpcBid</td>
</tr>
<tr class="even">
<td>ad_group_criterion_effective_cpc_bid_source</td>
<td>Source of the effective CPC bid.</td>
<td>CpcBidSource</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_effective_cpm_bid_micros</td>
<td>The effective CPM (cost-per-thousand viewable impressions) bid.</td>
<td>CpmBidStr</td>
</tr>
<tr class="even">
<td>ad_group_criterion_effective_cpm_bid_source</td>
<td>Source of the effective CPM bid.</td>
<td>CpmBidSource</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_final_mobile_urls</td>
<td>The list of possible final mobile URLs after all cross-domain redirects.</td>
<td>FinalMobileUrls</td>
</tr>
<tr class="even">
<td>ad_group_criterion_final_urls</td>
<td>The list of possible final URLs after all cross-domain redirects for the ad.</td>
<td>FinalUrls</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_negative</td>
<td>Whether to target (`false`) or exclude (`true`) the criterion. This field is immutable. To switch a criterion from positive to negative, remove then re-add it.</td>
<td>IsNegative</td>
</tr>
<tr class="even">
<td>ad_group_criterion_parental_status_type</td>
<td>Type of the parental status.</td>
<td>Criteria</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_status</td>
<td>The status of the criterion.</td>
<td>Status</td>
</tr>
<tr class="even">
<td>ad_group_criterion_tracking_url_template</td>
<td>The URL template for constructing a tracking URL.</td>
<td>TrackingUrlTemplate</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_url_custom_parameters</td>
<td>The list of mappings used to substitute custom parameter tags in a `tracking_url_template`, `final_urls`, or `mobile_final_urls`.</td>
<td>UrlCustomParameters</td>
</tr>
<tr class="even">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="odd">
<td>ad_group_targeting_setting_target_restrictions</td>
<td>The per-targeting-dimension setting to restrict the reach of your campaign or ad group.</td>
<td></td>
</tr>
<tr class="even">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td>BaseCampaignId</td>
</tr>
<tr class="odd">
<td>campaign_bidding_strategy</td>
<td>Portfolio bidding strategy used by campaign.</td>
<td>BiddingStrategyId</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
</tbody>
</table>

Google Ads Table Name: ParentalStatusBasicStats

Google Ads API Resource: [parental\_status\_view](https://developers.google.com/google-ads/api/fields/v21/parental_status_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_base_ad_group</td>
<td>For draft or experiment ad groups, this field is the resource name of the base ad group from which this ad group was created. If a draft or experiment ad group does not have a base ad group, then this field is null. For base ad groups, this field equals the ad group resource name. This field is read-only.</td>
<td>BaseAdGroupId</td>
</tr>
<tr class="even">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion. This field is ignored for mutates.</td>
<td>CriterionId</td>
</tr>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="even">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td>BaseCampaignId</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="odd">
<td>metrics_active_view_impressions</td>
<td>A measurement of how often your ad has become viewable on a Display Network site.</td>
<td>ActiveViewImpressions</td>
</tr>
<tr class="even">
<td>metrics_active_view_measurability</td>
<td>The ratio of impressions that could be measured by Active View over the number of served impressions.</td>
<td>ActiveViewMeasurability</td>
</tr>
<tr class="odd">
<td>metrics_active_view_measurable_cost_micros</td>
<td>The cost of the impressions you received that were measurable by Active View.</td>
<td>ActiveViewMeasurableCost</td>
</tr>
<tr class="even">
<td>metrics_active_view_measurable_impressions</td>
<td>The number of times your ads are appearing on placements in positions where they can be seen.</td>
<td>ActiveViewMeasurableImpressions</td>
</tr>
<tr class="odd">
<td>metrics_active_view_viewability</td>
<td>The percentage of time when your ad appeared on an Active View enabled site (measurable impressions) and was viewable (viewable impressions).</td>
<td>ActiveViewViewability</td>
</tr>
<tr class="even">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>AllConversions</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions_value</td>
<td>The total value of all conversions.</td>
<td>AllConversionValue</td>
</tr>
<tr class="even">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
<td>Clicks</td>
</tr>
<tr class="odd">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>Conversions</td>
</tr>
<tr class="even">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="odd">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
<td>Cost</td>
</tr>
<tr class="even">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on a Google Ads ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
<td>CrossDeviceConversions</td>
</tr>
<tr class="odd">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
<td>Impressions</td>
</tr>
<tr class="even">
<td>metrics_interaction_event_types</td>
<td>The types of payable and free interactions.</td>
<td>InteractionTypes</td>
</tr>
<tr class="odd">
<td>metrics_interactions</td>
<td>The number of interactions. An interaction is the main user action associated with an ad format, such as clicks for text and shopping ads or views for video ads.</td>
<td>Interactions</td>
</tr>
<tr class="even">
<td>metrics_view_through_conversions</td>
<td>The total number of view-through conversions. These happen when a customer sees an image or rich media ad, then later completes a conversion on your site without interacting with (for example, clicking on) another ad.</td>
<td>ViewThroughConversions</td>
</tr>
<tr class="odd">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="odd">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
</tbody>
</table>

Google Ads Table Name: ParentalStatusConversionStats

Google Ads API Resource: [parental\_status\_view](https://developers.google.com/google-ads/api/fields/v21/parental_status_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_base_ad_group</td>
<td>For draft or experiment ad groups, this field is the resource name of the base ad group from which this ad group was created. If a draft or experiment ad group does not have a base ad group, then this field is null. For base ad groups, this field equals the ad group resource name. This field is read-only.</td>
<td>BaseAdGroupId</td>
</tr>
<tr class="even">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion. This field is ignored for mutates.</td>
<td>CriterionId</td>
</tr>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="even">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td>BaseCampaignId</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>AllConversions</td>
</tr>
<tr class="even">
<td>metrics_all_conversions_value</td>
<td>The total value of all conversions.</td>
<td>AllConversionValue</td>
</tr>
<tr class="odd">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>Conversions</td>
</tr>
<tr class="even">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="odd">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on a Google Ads ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
<td>CrossDeviceConversions</td>
</tr>
<tr class="even">
<td>metrics_value_per_all_conversions</td>
<td>The value of all conversions divided by the number of all conversions.</td>
<td>ValuePerAllConversion</td>
</tr>
<tr class="odd">
<td>metrics_value_per_conversion</td>
<td>The value of conversions divided by the number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ValuePerConversion</td>
</tr>
<tr class="even">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="odd">
<td>segments_click_type</td>
<td>Click type.</td>
<td>ClickType</td>
</tr>
<tr class="even">
<td>segments_conversion_action</td>
<td>Resource name of the conversion action.</td>
<td>ConversionTrackerId</td>
</tr>
<tr class="odd">
<td>segments_conversion_action_category</td>
<td>Conversion action category.</td>
<td>ConversionCategoryName</td>
</tr>
<tr class="even">
<td>segments_conversion_action_name</td>
<td>Conversion action name.</td>
<td>ConversionTypeName</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="even">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="odd">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
<tr class="even">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="odd">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="even">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="odd">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: ParentalStatusNonClickStats

Google Ads API Resource: [parental\_status\_view](https://developers.google.com/google-ads/api/fields/v21/parental_status_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_base_ad_group</td>
<td>For draft or experiment ad groups, this field is the resource name of the base ad group from which this ad group was created. If a draft or experiment ad group does not have a base ad group, then this field is null. For base ad groups, this field equals the ad group resource name. This field is read-only.</td>
<td>BaseAdGroupId</td>
</tr>
<tr class="even">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion. This field is ignored for mutates.</td>
<td>CriterionId</td>
</tr>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="even">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td>BaseCampaignId</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="odd">
<td>metrics_average_cpe</td>
<td>The average amount that you've been charged for an ad engagement. This amount is the total cost of all ad engagements divided by the total number of ad engagements.</td>
<td>AverageCpe</td>
</tr>
<tr class="even">
<td>metrics_average_cpv</td>
<td>The average amount you pay each time someone views your ad. The average CPV is defined by the total cost of all ad views divided by the number of views.</td>
<td>AverageCpv</td>
</tr>
<tr class="odd">
<td>metrics_engagement_rate</td>
<td>How often people engage with your ad after it's shown to them. This is the number of ad expansions divided by the number of times your ad is shown.</td>
<td>EngagementRate</td>
</tr>
<tr class="even">
<td>metrics_engagements</td>
<td>The number of engagements. An engagement occurs when a viewer expands your Lightbox ad. Also, in the future, other ad types may support engagement metrics.</td>
<td>Engagements</td>
</tr>
<tr class="odd">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_video_quartile_p100_rate</td>
<td>Percentage of impressions where the viewer watched all of your video.</td>
<td>VideoQuartile100Rate</td>
</tr>
<tr class="odd">
<td>metrics_video_quartile_p25_rate</td>
<td>Percentage of impressions where the viewer watched 25% of your video.</td>
<td>VideoQuartile25Rate</td>
</tr>
<tr class="even">
<td>metrics_video_quartile_p50_rate</td>
<td>Percentage of impressions where the viewer watched 50% of your video.</td>
<td>VideoQuartile50Rate</td>
</tr>
<tr class="odd">
<td>metrics_video_quartile_p75_rate</td>
<td>Percentage of impressions where the viewer watched 75% of your video.</td>
<td>VideoQuartile75Rate</td>
</tr>
<tr class="even">
<td>metrics_video_view_rate</td>
<td>The number of views your TrueView video ad receives divided by its number of impressions, including thumbnail impressions for TrueView in-display ads.</td>
<td>VideoViewRate</td>
</tr>
<tr class="odd">
<td>metrics_video_views</td>
<td>The number of times your video ads were viewed.</td>
<td>VideoViews</td>
</tr>
<tr class="even">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="even">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="odd">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
<tr class="even">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="odd">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="even">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="odd">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: ParentalStatusStats

Google Ads API Resource: [parental\_status\_view](https://developers.google.com/google-ads/api/fields/v21/parental_status_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_base_ad_group</td>
<td>For draft or experiment ad groups, this field is the resource name of the base ad group from which this ad group was created. If a draft or experiment ad group does not have a base ad group, then this field is null. For base ad groups, this field equals the ad group resource name. This field is read-only.</td>
<td>BaseAdGroupId</td>
</tr>
<tr class="even">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion. This field is ignored for mutates.</td>
<td>CriterionId</td>
</tr>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="even">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td>BaseCampaignId</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="odd">
<td>metrics_active_view_cpm</td>
<td>Average cost of viewable impressions (`active_view_impressions`).</td>
<td>ActiveViewCpm</td>
</tr>
<tr class="even">
<td>metrics_active_view_ctr</td>
<td>Active view measurable clicks divided by active view viewable impressions. This metric is reported only for display network.</td>
<td>ActiveViewCtr</td>
</tr>
<tr class="odd">
<td>metrics_active_view_impressions</td>
<td>A measurement of how often your ad has become viewable on a Display Network site.</td>
<td>ActiveViewImpressions</td>
</tr>
<tr class="even">
<td>metrics_active_view_measurability</td>
<td>The ratio of impressions that could be measured by Active View over the number of served impressions.</td>
<td>ActiveViewMeasurability</td>
</tr>
<tr class="odd">
<td>metrics_active_view_measurable_cost_micros</td>
<td>The cost of the impressions you received that were measurable by Active View.</td>
<td>ActiveViewMeasurableCost</td>
</tr>
<tr class="even">
<td>metrics_active_view_measurable_impressions</td>
<td>The number of times your ads are appearing on placements in positions where they can be seen.</td>
<td>ActiveViewMeasurableImpressions</td>
</tr>
<tr class="odd">
<td>metrics_active_view_viewability</td>
<td>The percentage of time when your ad appeared on an Active View enabled site (measurable impressions) and was viewable (viewable impressions).</td>
<td>ActiveViewViewability</td>
</tr>
<tr class="even">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>AllConversions</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions_from_interactions_rate</td>
<td>All conversions from interactions (as oppose to view through conversions) divided by the number of ad interactions.</td>
<td>AllConversionRate</td>
</tr>
<tr class="even">
<td>metrics_all_conversions_value</td>
<td>The total value of all conversions.</td>
<td>AllConversionValue</td>
</tr>
<tr class="odd">
<td>metrics_average_cost</td>
<td>The average amount you pay per interaction. This amount is the total cost of your ads divided by the total number of interactions.</td>
<td>AverageCost</td>
</tr>
<tr class="even">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
<td>AverageCpc</td>
</tr>
<tr class="odd">
<td>metrics_average_cpm</td>
<td>Average cost-per-thousand impressions (CPM).</td>
<td>AverageCpm</td>
</tr>
<tr class="even">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
<td>Clicks</td>
</tr>
<tr class="odd">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>Conversions</td>
</tr>
<tr class="even">
<td>metrics_conversions_from_interactions_rate</td>
<td>Conversions from interactions divided by the number of ad interactions (such as clicks for text ads or views for video ads). This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionRate</td>
</tr>
<tr class="odd">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="even">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
<td>Cost</td>
</tr>
<tr class="odd">
<td>metrics_cost_per_all_conversions</td>
<td>The cost of ad interactions divided by all conversions.</td>
<td>CostPerAllConversion</td>
</tr>
<tr class="even">
<td>metrics_cost_per_conversion</td>
<td>The cost of ad interactions divided by conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>CostPerConversion</td>
</tr>
<tr class="odd">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on a Google Ads ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
<td>CrossDeviceConversions</td>
</tr>
<tr class="even">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
<td>Ctr</td>
</tr>
<tr class="odd">
<td>metrics_gmail_forwards</td>
<td>The number of times the ad was forwarded to someone else as a message.</td>
<td>GmailForwards</td>
</tr>
<tr class="even">
<td>metrics_gmail_saves</td>
<td>The number of times someone has saved your Gmail ad to their inbox as a message.</td>
<td>GmailSaves</td>
</tr>
<tr class="odd">
<td>metrics_gmail_secondary_clicks</td>
<td>The number of clicks to the landing page on the expanded state of Gmail ads.</td>
<td>GmailSecondaryClicks</td>
</tr>
<tr class="even">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
<td>Impressions</td>
</tr>
<tr class="odd">
<td>metrics_interaction_event_types</td>
<td>The types of payable and free interactions.</td>
<td>InteractionTypes</td>
</tr>
<tr class="even">
<td>metrics_interaction_rate</td>
<td>How often people interact with your ad after it is shown to them. This is the number of interactions divided by the number of times your ad is shown.</td>
<td>InteractionRate</td>
</tr>
<tr class="odd">
<td>metrics_interactions</td>
<td>The number of interactions. An interaction is the main user action associated with an ad format, such as clicks for text and shopping ads or views for video ads.</td>
<td>Interactions</td>
</tr>
<tr class="even">
<td>metrics_value_per_all_conversions</td>
<td>The value of all conversions divided by the number of all conversions.</td>
<td>ValuePerAllConversion</td>
</tr>
<tr class="odd">
<td>metrics_value_per_conversion</td>
<td>The value of conversions divided by the number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ValuePerConversion</td>
</tr>
<tr class="even">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="odd">
<td>segments_click_type</td>
<td>Click type.</td>
<td>ClickType</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="odd">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="even">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
<tr class="odd">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="even">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="odd">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="even">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: Placement

Google Ads API Resource: [managed\_placement\_view](https://developers.google.com/google-ads/api/fields/v21/managed_placement_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_base_ad_group</td>
<td>For draft or experiment ad groups, this field is the resource name of the base ad group from which this ad group was created. If a draft or experiment ad group does not have a base ad group, then this field is null. For base ad groups, this field equals the ad group resource name. This field is read-only.</td>
<td>BaseAdGroupId</td>
</tr>
<tr class="even">
<td>ad_group_criterion_bid_modifier</td>
<td>The modifier for the bid when the criterion matches. The modifier must be in the range: 0.1 - 10.0. Most targetable criteria types support modifiers.</td>
<td>BidModifier</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion. This field is ignored for mutates.</td>
<td>CriterionId</td>
</tr>
<tr class="even">
<td>ad_group_criterion_effective_cpc_bid_micros</td>
<td>The effective CPC (cost-per-click) bid.</td>
<td>CpcBid</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_effective_cpc_bid_source</td>
<td>Source of the effective CPC bid.</td>
<td>CpcBidSource</td>
</tr>
<tr class="even">
<td>ad_group_criterion_effective_cpm_bid_micros</td>
<td>The effective CPM (cost-per-thousand viewable impressions) bid.</td>
<td>CpmBidStr</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_effective_cpm_bid_source</td>
<td>Source of the effective CPM bid.</td>
<td>CpmBidSource</td>
</tr>
<tr class="even">
<td>ad_group_criterion_final_mobile_urls</td>
<td>The list of possible final mobile URLs after all cross-domain redirects.</td>
<td>FinalMobileUrls</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_final_urls</td>
<td>The list of possible final URLs after all cross-domain redirects for the ad.</td>
<td>FinalUrls</td>
</tr>
<tr class="even">
<td>ad_group_criterion_negative</td>
<td>Whether to target (`false`) or exclude (`true`) the criterion. This field is immutable. To switch a criterion from positive to negative, remove then re-add it.</td>
<td>IsNegative</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_placement_url</td>
<td>URL of the placement. For example, \"http://www.domain.com\".</td>
<td>Criteria</td>
</tr>
<tr class="even">
<td>ad_group_criterion_status</td>
<td>The status of the criterion.</td>
<td>Status</td>
</tr>
<tr class="odd">
<td>ad_group_criterion_tracking_url_template</td>
<td>The URL template for constructing a tracking URL.</td>
<td>TrackingUrlTemplate</td>
</tr>
<tr class="even">
<td>ad_group_criterion_url_custom_parameters</td>
<td>The list of mappings used to substitute custom parameter tags in a `tracking_url_template`, `final_urls`, or `mobile_final_urls`.</td>
<td>UrlCustomParameters</td>
</tr>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="even">
<td>ad_group_targeting_setting_target_restrictions</td>
<td>The per-targeting-dimension setting to restrict the reach of your campaign or ad group.</td>
<td></td>
</tr>
<tr class="odd">
<td>bidding_strategy_name</td>
<td>The name of the bidding strategy. All bidding strategies within an account must be named distinctly. The length of this string should be between 1 and 255, inclusive, in UTF-8 bytes, (trimmed).</td>
<td>BiddingStrategyName</td>
</tr>
<tr class="even">
<td>bidding_strategy_type</td>
<td>The type of the bidding strategy. Create a bidding strategy by setting the bidding scheme. This field is read-only.</td>
<td>BiddingStrategyType</td>
</tr>
<tr class="odd">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td>BaseCampaignId</td>
</tr>
<tr class="even">
<td>campaign_bidding_strategy</td>
<td>Portfolio bidding strategy used by campaign.</td>
<td>BiddingStrategyId</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
</tbody>
</table>

Google Ads Table Name: PlacementBasicStats

Google Ads API Resource: [managed\_placement\_view](https://developers.google.com/google-ads/api/fields/v21/managed_placement_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_base_ad_group</td>
<td>For draft or experiment ad groups, this field is the resource name of the base ad group from which this ad group was created. If a draft or experiment ad group does not have a base ad group, then this field is null. For base ad groups, this field equals the ad group resource name. This field is read-only.</td>
<td>BaseAdGroupId</td>
</tr>
<tr class="even">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion. This field is ignored for mutates.</td>
<td>CriterionId</td>
</tr>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="even">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td>BaseCampaignId</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="odd">
<td>metrics_active_view_impressions</td>
<td>A measurement of how often your ad has become viewable on a Display Network site.</td>
<td>ActiveViewImpressions</td>
</tr>
<tr class="even">
<td>metrics_active_view_measurability</td>
<td>The ratio of impressions that could be measured by Active View over the number of served impressions.</td>
<td>ActiveViewMeasurability</td>
</tr>
<tr class="odd">
<td>metrics_active_view_measurable_cost_micros</td>
<td>The cost of the impressions you received that were measurable by Active View.</td>
<td>ActiveViewMeasurableCost</td>
</tr>
<tr class="even">
<td>metrics_active_view_measurable_impressions</td>
<td>The number of times your ads are appearing on placements in positions where they can be seen.</td>
<td>ActiveViewMeasurableImpressions</td>
</tr>
<tr class="odd">
<td>metrics_active_view_viewability</td>
<td>The percentage of time when your ad appeared on an Active View enabled site (measurable impressions) and was viewable (viewable impressions).</td>
<td>ActiveViewViewability</td>
</tr>
<tr class="even">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>AllConversions</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions_value</td>
<td>The total value of all conversions.</td>
<td>AllConversionValue</td>
</tr>
<tr class="even">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
<td>Clicks</td>
</tr>
<tr class="odd">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>Conversions</td>
</tr>
<tr class="even">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="odd">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
<td>Cost</td>
</tr>
<tr class="even">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on a Google Ads ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
<td>CrossDeviceConversions</td>
</tr>
<tr class="odd">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
<td>Impressions</td>
</tr>
<tr class="even">
<td>metrics_interaction_event_types</td>
<td>The types of payable and free interactions.</td>
<td>InteractionTypes</td>
</tr>
<tr class="odd">
<td>metrics_interactions</td>
<td>The number of interactions. An interaction is the main user action associated with an ad format, such as clicks for text and shopping ads or views for video ads.</td>
<td>Interactions</td>
</tr>
<tr class="even">
<td>metrics_view_through_conversions</td>
<td>The total number of view-through conversions. These happen when a customer sees an image or rich media ad, then later completes a conversion on your site without interacting with (for example, clicking on) another ad.</td>
<td>ViewThroughConversions</td>
</tr>
<tr class="odd">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="odd">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
</tbody>
</table>

Google Ads Table Name: PlacementConversionStats

Google Ads API Resource: [managed\_placement\_view](https://developers.google.com/google-ads/api/fields/v21/managed_placement_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_base_ad_group</td>
<td>For draft or experiment ad groups, this field is the resource name of the base ad group from which this ad group was created. If a draft or experiment ad group does not have a base ad group, then this field is null. For base ad groups, this field equals the ad group resource name. This field is read-only.</td>
<td>BaseAdGroupId</td>
</tr>
<tr class="even">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion. This field is ignored for mutates.</td>
<td>CriterionId</td>
</tr>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="even">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td>BaseCampaignId</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>AllConversions</td>
</tr>
<tr class="even">
<td>metrics_all_conversions_value</td>
<td>The total value of all conversions.</td>
<td>AllConversionValue</td>
</tr>
<tr class="odd">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>Conversions</td>
</tr>
<tr class="even">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="odd">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on a Google Ads ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
<td>CrossDeviceConversions</td>
</tr>
<tr class="even">
<td>metrics_value_per_all_conversions</td>
<td>The value of all conversions divided by the number of all conversions.</td>
<td>ValuePerAllConversion</td>
</tr>
<tr class="odd">
<td>metrics_value_per_conversion</td>
<td>The value of conversions divided by the number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ValuePerConversion</td>
</tr>
<tr class="even">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="odd">
<td>segments_click_type</td>
<td>Click type.</td>
<td>ClickType</td>
</tr>
<tr class="even">
<td>segments_conversion_action</td>
<td>Resource name of the conversion action.</td>
<td>ConversionTrackerId</td>
</tr>
<tr class="odd">
<td>segments_conversion_action_category</td>
<td>Conversion action category.</td>
<td>ConversionCategoryName</td>
</tr>
<tr class="even">
<td>segments_conversion_action_name</td>
<td>Conversion action name.</td>
<td>ConversionTypeName</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="even">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="odd">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
<tr class="even">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="odd">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="even">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="odd">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: PlacementNonClickStats

Google Ads API Resource: [managed\_placement\_view](https://developers.google.com/google-ads/api/fields/v21/managed_placement_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_base_ad_group</td>
<td>For draft or experiment ad groups, this field is the resource name of the base ad group from which this ad group was created. If a draft or experiment ad group does not have a base ad group, then this field is null. For base ad groups, this field equals the ad group resource name. This field is read-only.</td>
<td>BaseAdGroupId</td>
</tr>
<tr class="even">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion. This field is ignored for mutates.</td>
<td>CriterionId</td>
</tr>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="even">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td>BaseCampaignId</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="odd">
<td>metrics_average_cpe</td>
<td>The average amount that you've been charged for an ad engagement. This amount is the total cost of all ad engagements divided by the total number of ad engagements.</td>
<td>AverageCpe</td>
</tr>
<tr class="even">
<td>metrics_average_cpv</td>
<td>The average amount you pay each time someone views your ad. The average CPV is defined by the total cost of all ad views divided by the number of views.</td>
<td>AverageCpv</td>
</tr>
<tr class="odd">
<td>metrics_engagement_rate</td>
<td>How often people engage with your ad after it's shown to them. This is the number of ad expansions divided by the number of times your ad is shown.</td>
<td>EngagementRate</td>
</tr>
<tr class="even">
<td>metrics_engagements</td>
<td>The number of engagements. An engagement occurs when a viewer expands your Lightbox ad. Also, in the future, other ad types may support engagement metrics.</td>
<td>Engagements</td>
</tr>
<tr class="odd">
<td>metrics_video_quartile_p100_rate</td>
<td>Percentage of impressions where the viewer watched all of your video.</td>
<td>VideoQuartile100Rate</td>
</tr>
<tr class="even">
<td>metrics_video_quartile_p25_rate</td>
<td>Percentage of impressions where the viewer watched 25% of your video.</td>
<td>VideoQuartile25Rate</td>
</tr>
<tr class="odd">
<td>metrics_video_quartile_p50_rate</td>
<td>Percentage of impressions where the viewer watched 50% of your video.</td>
<td>VideoQuartile50Rate</td>
</tr>
<tr class="even">
<td>metrics_video_quartile_p75_rate</td>
<td>Percentage of impressions where the viewer watched 75% of your video.</td>
<td>VideoQuartile75Rate</td>
</tr>
<tr class="odd">
<td>metrics_video_view_rate</td>
<td>The number of views your TrueView video ad receives divided by its number of impressions, including thumbnail impressions for TrueView in-display ads.</td>
<td>VideoViewRate</td>
</tr>
<tr class="even">
<td>metrics_video_views</td>
<td>The number of times your video ads were viewed.</td>
<td>VideoViews</td>
</tr>
<tr class="odd">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="odd">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="even">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
<tr class="odd">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="even">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="odd">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="even">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: PlacementStats

Google Ads API Resource: [managed\_placement\_view](https://developers.google.com/google-ads/api/fields/v21/managed_placement_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_base_ad_group</td>
<td>For draft or experiment ad groups, this field is the resource name of the base ad group from which this ad group was created. If a draft or experiment ad group does not have a base ad group, then this field is null. For base ad groups, this field equals the ad group resource name. This field is read-only.</td>
<td>BaseAdGroupId</td>
</tr>
<tr class="even">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion. This field is ignored for mutates.</td>
<td>CriterionId</td>
</tr>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="even">
<td>campaign_base_campaign</td>
<td>The resource name of the base campaign of a draft or experiment campaign. For base campaigns, this is equal to `resource_name`. This field is read-only.</td>
<td>BaseCampaignId</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="odd">
<td>metrics_active_view_cpm</td>
<td>Average cost of viewable impressions (`active_view_impressions`).</td>
<td>ActiveViewCpm</td>
</tr>
<tr class="even">
<td>metrics_active_view_ctr</td>
<td>Active view measurable clicks divided by active view viewable impressions. This metric is reported only for display network.</td>
<td>ActiveViewCtr</td>
</tr>
<tr class="odd">
<td>metrics_active_view_impressions</td>
<td>A measurement of how often your ad has become viewable on a Display Network site.</td>
<td>ActiveViewImpressions</td>
</tr>
<tr class="even">
<td>metrics_active_view_measurability</td>
<td>The ratio of impressions that could be measured by Active View over the number of served impressions.</td>
<td>ActiveViewMeasurability</td>
</tr>
<tr class="odd">
<td>metrics_active_view_measurable_cost_micros</td>
<td>The cost of the impressions you received that were measurable by Active View.</td>
<td>ActiveViewMeasurableCost</td>
</tr>
<tr class="even">
<td>metrics_active_view_measurable_impressions</td>
<td>The number of times your ads are appearing on placements in positions where they can be seen.</td>
<td>ActiveViewMeasurableImpressions</td>
</tr>
<tr class="odd">
<td>metrics_active_view_viewability</td>
<td>The percentage of time when your ad appeared on an Active View enabled site (measurable impressions) and was viewable (viewable impressions).</td>
<td>ActiveViewViewability</td>
</tr>
<tr class="even">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>AllConversions</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions_from_interactions_rate</td>
<td>All conversions from interactions (as oppose to view through conversions) divided by the number of ad interactions.</td>
<td>AllConversionRate, ConversionRate</td>
</tr>
<tr class="even">
<td>metrics_all_conversions_value</td>
<td>The total value of all conversions.</td>
<td>AllConversionValue</td>
</tr>
<tr class="odd">
<td>metrics_average_cost</td>
<td>The average amount you pay per interaction. This amount is the total cost of your ads divided by the total number of interactions.</td>
<td>AverageCost</td>
</tr>
<tr class="even">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
<td>AverageCpc</td>
</tr>
<tr class="odd">
<td>metrics_average_cpm</td>
<td>Average cost-per-thousand impressions (CPM).</td>
<td>AverageCpm</td>
</tr>
<tr class="even">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
<td>Clicks</td>
</tr>
<tr class="odd">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>Conversions</td>
</tr>
<tr class="even">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="odd">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
<td>Cost</td>
</tr>
<tr class="even">
<td>metrics_cost_per_all_conversions</td>
<td>The cost of ad interactions divided by all conversions.</td>
<td>CostPerAllConversion</td>
</tr>
<tr class="odd">
<td>metrics_cost_per_conversion</td>
<td>The cost of ad interactions divided by conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>CostPerConversion</td>
</tr>
<tr class="even">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on a Google Ads ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
<td>CrossDeviceConversions</td>
</tr>
<tr class="odd">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
<td>Ctr</td>
</tr>
<tr class="even">
<td>metrics_gmail_forwards</td>
<td>The number of times the ad was forwarded to someone else as a message.</td>
<td>GmailForwards</td>
</tr>
<tr class="odd">
<td>metrics_gmail_saves</td>
<td>The number of times someone has saved your Gmail ad to their inbox as a message.</td>
<td>GmailSaves</td>
</tr>
<tr class="even">
<td>metrics_gmail_secondary_clicks</td>
<td>The number of clicks to the landing page on the expanded state of Gmail ads.</td>
<td>GmailSecondaryClicks</td>
</tr>
<tr class="odd">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
<td>Impressions</td>
</tr>
<tr class="even">
<td>metrics_interaction_event_types</td>
<td>The types of payable and free interactions.</td>
<td>InteractionTypes</td>
</tr>
<tr class="odd">
<td>metrics_interaction_rate</td>
<td>How often people interact with your ad after it is shown to them. This is the number of interactions divided by the number of times your ad is shown.</td>
<td>InteractionRate</td>
</tr>
<tr class="even">
<td>metrics_interactions</td>
<td>The number of interactions. An interaction is the main user action associated with an ad format, such as clicks for text and shopping ads or views for video ads.</td>
<td>Interactions</td>
</tr>
<tr class="odd">
<td>metrics_value_per_all_conversions</td>
<td>The value of all conversions divided by the number of all conversions.</td>
<td>ValuePerAllConversion</td>
</tr>
<tr class="even">
<td>metrics_value_per_conversion</td>
<td>The value of conversions divided by the number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ValuePerConversion</td>
</tr>
<tr class="odd">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="even">
<td>segments_click_type</td>
<td>Click type.</td>
<td>ClickType</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="even">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="odd">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
<tr class="even">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="odd">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="even">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="odd">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: ProductGroupStats

Google Ads API Resource: [product\_group\_view](https://developers.google.com/google-ads/api/fields/v21/product_group_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_criterion_cpc_bid_micros</td>
<td>The CPC (cost-per-click) bid.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_criterion_criterion_id</td>
<td>The ID of the criterion. This field is ignored for mutates.</td>
<td></td>
</tr>
<tr class="odd">
<td>ad_group_criterion_display_name</td>
<td>The display name of the criterion. This field is ignored for mutates.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_criterion_listing_group_case_value_product_bidding_category_id (obsolete - use ad_group_criterion_listing_group_case_value_product_category_category_id instead)</td>
<td>ID of the product bidding category. This ID is equivalent to the google_product_category ID as described in this document: https://support.google.com/merchants/answer/6324436</td>
<td></td>
</tr>
<tr class="odd">
<td>ad_group_criterion_listing_group_case_value_product_bidding_category_level (obsolete - use ad_group_criterion_listing_group_case_value_product_category_level instead)</td>
<td>Level of the product bidding category.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_criterion_listing_group_case_value_product_brand_value</td>
<td>String value of the product brand.</td>
<td></td>
</tr>
<tr class="odd">
<td>ad_group_criterion_listing_group_case_value_product_channel_channel</td>
<td>Value of the locality.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_criterion_listing_group_case_value_product_channel_exclusivity_channel_exclusivity</td>
<td>Value of the availability.</td>
<td></td>
</tr>
<tr class="odd">
<td>ad_group_criterion_listing_group_case_value_product_condition_condition</td>
<td>Value of the condition.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_criterion_listing_group_case_value_product_custom_attribute_index</td>
<td>Indicates the index of the custom attribute.</td>
<td></td>
</tr>
<tr class="odd">
<td>ad_group_criterion_listing_group_case_value_product_custom_attribute_value</td>
<td>String value of the product custom attribute.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_criterion_listing_group_case_value_product_item_id_value</td>
<td>Value of the id.</td>
<td></td>
</tr>
<tr class="odd">
<td>ad_group_criterion_listing_group_case_value_product_type_level</td>
<td>Level of the type.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_criterion_listing_group_case_value_product_type_value</td>
<td>Value of the type.</td>
<td></td>
</tr>
<tr class="odd">
<td>ad_group_criterion_status</td>
<td>The status of the criterion.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td></td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_average_cpm</td>
<td>Average cost-per-thousand impressions (CPM).</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
<td></td>
</tr>
<tr class="even">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
<td></td>
</tr>
<tr class="odd">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
<td></td>
</tr>
<tr class="even">
<td>product_group_view_resource_name</td>
<td>The resource name of the product group view. Product group view resource names have the form: customers/{customer_id}/productGroupViews/{ad_group_id}~{criterion_id}</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td></td>
</tr>
<tr class="odd">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td></td>
</tr>
<tr class="even">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td></td>
</tr>
</tbody>
</table>

Google Ads Table Name: SearchQueryConversionStats

Google Ads API Resource: [search\_term\_view](https://developers.google.com/google-ads/api/fields/v21/search_term_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_ad_ad_id</td>
<td>The ID of the ad.</td>
<td>CreativeId</td>
</tr>
<tr class="even">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>AllConversions</td>
</tr>
<tr class="even">
<td>metrics_all_conversions_value</td>
<td>The total value of all conversions.</td>
<td>AllConversionValue</td>
</tr>
<tr class="odd">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>Conversions</td>
</tr>
<tr class="even">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="odd">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on a Google Ads ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
<td>CrossDeviceConversions</td>
</tr>
<tr class="even">
<td>metrics_value_per_all_conversions</td>
<td>The value of all conversions divided by the number of all conversions.</td>
<td>ValuePerAllConversion</td>
</tr>
<tr class="odd">
<td>metrics_value_per_conversion</td>
<td>The value of conversions divided by the number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ValuePerConversion</td>
</tr>
<tr class="even">
<td>metrics_view_through_conversions</td>
<td>The total number of view-through conversions. These happen when a customer sees an image or rich media ad, then later completes a conversion on your site without interacting with (for example, clicking on) another ad.</td>
<td>ViewThroughConversions</td>
</tr>
<tr class="odd">
<td>search_term_view_search_term</td>
<td>The search term.</td>
<td>Query</td>
</tr>
<tr class="even">
<td>search_term_view_status</td>
<td>Indicates whether the search term is one of your targeted or excluded keywords.</td>
<td>QueryTargetingStatus</td>
</tr>
<tr class="odd">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="even">
<td>segments_conversion_action</td>
<td>Resource name of the conversion action.</td>
<td>ConversionTrackerId</td>
</tr>
<tr class="odd">
<td>segments_conversion_action_category</td>
<td>Conversion action category.</td>
<td>ConversionCategoryName</td>
</tr>
<tr class="even">
<td>segments_conversion_action_name</td>
<td>Conversion action name.</td>
<td>ConversionTypeName</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="even">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="odd">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
<tr class="even">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="odd">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="even">
<td>segments_search_term_match_type</td>
<td>Match type of the keyword that triggered the ad, including variants.</td>
<td>QueryMatchTypeWithVariant</td>
</tr>
<tr class="odd">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="even">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: SearchQueryStats

Google Ads API Resource: [search\_term\_view](https://developers.google.com/google-ads/api/fields/v21/search_term_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_ad_ad_id</td>
<td>The ID of the ad.</td>
<td>CreativeId</td>
</tr>
<tr class="even">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="odd">
<td>metrics_absolute_top_impression_percentage</td>
<td>The percent of your ad impressions that are shown as the very first ad above the organic search results.</td>
<td>AbsoluteTopImpressionPercentage</td>
</tr>
<tr class="even">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>AllConversions</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions_from_interactions_rate</td>
<td>All conversions from interactions (as oppose to view through conversions) divided by the number of ad interactions.</td>
<td>AllConversionRate</td>
</tr>
<tr class="even">
<td>metrics_all_conversions_value</td>
<td>The total value of all conversions.</td>
<td>AllConversionValue</td>
</tr>
<tr class="odd">
<td>metrics_average_cost</td>
<td>The average amount you pay per interaction. This amount is the total cost of your ads divided by the total number of interactions.</td>
<td>AverageCost</td>
</tr>
<tr class="even">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
<td>AverageCpc</td>
</tr>
<tr class="odd">
<td>metrics_average_cpe</td>
<td>The average amount that you've been charged for an ad engagement. This amount is the total cost of all ad engagements divided by the total number of ad engagements.</td>
<td>AverageCpe</td>
</tr>
<tr class="even">
<td>metrics_average_cpm</td>
<td>Average cost-per-thousand impressions (CPM).</td>
<td>AverageCpm</td>
</tr>
<tr class="odd">
<td>metrics_average_cpv</td>
<td>The average amount you pay each time someone views your ad. The average CPV is defined by the total cost of all ad views divided by the number of views.</td>
<td>AverageCpv</td>
</tr>
<tr class="even">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
<td>Clicks</td>
</tr>
<tr class="odd">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>Conversions</td>
</tr>
<tr class="even">
<td>metrics_conversions_from_interactions_rate</td>
<td>Conversions from interactions divided by the number of ad interactions (such as clicks for text ads or views for video ads). This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionRate</td>
</tr>
<tr class="odd">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="even">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
<td>Cost</td>
</tr>
<tr class="odd">
<td>metrics_cost_per_all_conversions</td>
<td>The cost of ad interactions divided by all conversions.</td>
<td>CostPerAllConversion</td>
</tr>
<tr class="even">
<td>metrics_cost_per_conversion</td>
<td>The cost of ad interactions divided by conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>CostPerConversion</td>
</tr>
<tr class="odd">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on a Google Ads ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
<td>CrossDeviceConversions</td>
</tr>
<tr class="even">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
<td>Ctr</td>
</tr>
<tr class="odd">
<td>metrics_engagement_rate</td>
<td>How often people engage with your ad after it's shown to them. This is the number of ad expansions divided by the number of times your ad is shown.</td>
<td>EngagementRate</td>
</tr>
<tr class="even">
<td>metrics_engagements</td>
<td>The number of engagements. An engagement occurs when a viewer expands your Lightbox ad. Also, in the future, other ad types may support engagement metrics.</td>
<td>Engagements</td>
</tr>
<tr class="odd">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
<td>Impressions</td>
</tr>
<tr class="even">
<td>metrics_interaction_event_types</td>
<td>The types of payable and free interactions.</td>
<td>InteractionTypes</td>
</tr>
<tr class="odd">
<td>metrics_interaction_rate</td>
<td>How often people interact with your ad after it is shown to them. This is the number of interactions divided by the number of times your ad is shown.</td>
<td>InteractionRate</td>
</tr>
<tr class="even">
<td>metrics_interactions</td>
<td>The number of interactions. An interaction is the main user action associated with an ad format, such as clicks for text and shopping ads or views for video ads.</td>
<td>Interactions</td>
</tr>
<tr class="odd">
<td>metrics_top_impression_percentage</td>
<td>The percent of your ad impressions that are shown anywhere above the organic search results.</td>
<td>TopImpressionPercentage</td>
</tr>
<tr class="even">
<td>metrics_value_per_all_conversions</td>
<td>The value of all conversions divided by the number of all conversions.</td>
<td>ValuePerAllConversion</td>
</tr>
<tr class="odd">
<td>metrics_value_per_conversion</td>
<td>The value of conversions divided by the number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ValuePerConversion</td>
</tr>
<tr class="even">
<td>metrics_video_quartile_p100_rate</td>
<td>Percentage of impressions where the viewer watched all of your video.</td>
<td>VideoQuartile100Rate</td>
</tr>
<tr class="odd">
<td>metrics_video_quartile_p25_rate</td>
<td>Percentage of impressions where the viewer watched 25% of your video.</td>
<td>VideoQuartile25Rate</td>
</tr>
<tr class="even">
<td>metrics_video_quartile_p50_rate</td>
<td>Percentage of impressions where the viewer watched 50% of your video.</td>
<td>VideoQuartile50Rate</td>
</tr>
<tr class="odd">
<td>metrics_video_quartile_p75_rate</td>
<td>Percentage of impressions where the viewer watched 75% of your video.</td>
<td>VideoQuartile75Rate</td>
</tr>
<tr class="even">
<td>metrics_video_view_rate</td>
<td>The number of views your TrueView video ad receives divided by its number of impressions, including thumbnail impressions for TrueView in-display ads.</td>
<td>VideoViewRate</td>
</tr>
<tr class="odd">
<td>metrics_video_views</td>
<td>The number of times your video ads were viewed.</td>
<td>VideoViews</td>
</tr>
<tr class="even">
<td>metrics_view_through_conversions</td>
<td>The total number of view-through conversions. These happen when a customer sees an image or rich media ad, then later completes a conversion on your site without interacting with (for example, clicking on) another ad.</td>
<td>ViewThroughConversions</td>
</tr>
<tr class="odd">
<td>search_term_view_search_term</td>
<td>The search term.</td>
<td>Query</td>
</tr>
<tr class="even">
<td>search_term_view_status</td>
<td>Indicates whether the search term is one of your targeted or excluded keywords.</td>
<td>QueryTargetingStatus</td>
</tr>
<tr class="odd">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="odd">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="even">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
<tr class="odd">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="even">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="odd">
<td>segments_search_term_match_type</td>
<td>Match type of the keyword that triggered the ad, including variants.</td>
<td>QueryMatchTypeWithVariant</td>
</tr>
<tr class="even">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="odd">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: ShoppingProductConversionStats

Google Ads API Resource: [shopping\_performance\_view](https://developers.google.com/google-ads/api/fields/v21/shopping_performance_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="odd">
<td>campaign_status</td>
<td>The status of the campaign. When a new campaign is added, the status defaults to ENABLED.</td>
<td></td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>AllConversions</td>
</tr>
<tr class="even">
<td>metrics_all_conversions_value</td>
<td>The total value of all conversions.</td>
<td>AllConversionValue</td>
</tr>
<tr class="odd">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="even">
<td>metrics_value_per_all_conversions</td>
<td>The value of all conversions divided by the number of all conversions.</td>
<td>ValuePerAllConversion</td>
</tr>
<tr class="odd">
<td>metrics_value_per_conversion</td>
<td>The value of conversions divided by the number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ValuePerConversion</td>
</tr>
<tr class="even">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="odd">
<td>segments_click_type</td>
<td>Click type.</td>
<td>ClickType</td>
</tr>
<tr class="even">
<td>segments_conversion_action</td>
<td>Resource name of the conversion action.</td>
<td>ConversionTrackerId</td>
</tr>
<tr class="odd">
<td>segments_conversion_action_category</td>
<td>Conversion action category.</td>
<td>ConversionCategoryName</td>
</tr>
<tr class="even">
<td>segments_conversion_action_name</td>
<td>Conversion action name.</td>
<td>ConversionTypeName</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="even">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="odd">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
<tr class="even">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="odd">
<td>segments_product_aggregator_id</td>
<td>Aggregator ID of the product.</td>
<td>AggregatorId</td>
</tr>
<tr class="even">
<td>segments_product_bidding_category_level1 <strong>(obsolete - use segments_product_category_level1 instead)</strong></td>
<td>Bidding category (level 1) of the product.</td>
<td>CategoryL1</td>
</tr>
<tr class="odd">
<td>segments_product_bidding_category_level2 <strong>(obsolete - use segments_product_category_level2 instead)</strong></td>
<td>Bidding category (level 2) of the product.</td>
<td>CategoryL2</td>
</tr>
<tr class="even">
<td>segments_product_bidding_category_level3 <strong>(obsolete - use segments_product_category_level3 instead)</strong></td>
<td>Bidding category (level 3) of the product.</td>
<td>CategoryL3</td>
</tr>
<tr class="odd">
<td>segments_product_bidding_category_level4 <strong>(obsolete - use segments_product_category_level4 instead)</strong></td>
<td>Bidding category (level 4) of the product.</td>
<td>CategoryL4</td>
</tr>
<tr class="even">
<td>segments_product_bidding_category_level5 <strong>(obsolete - use segments_product_category_level5 instead)</strong></td>
<td>Bidding category (level 5) of the product.</td>
<td>CategoryL5</td>
</tr>
<tr class="odd">
<td>segments_product_category_level1</td>
<td>Category (level 1) of the product.</td>
<td>CategoryL1</td>
</tr>
<tr class="even">
<td>segments_product_category_level2</td>
<td>Category (level 2) of the product.</td>
<td>CategoryL2</td>
</tr>
<tr class="odd">
<td>segments_product_category_level3</td>
<td>Category (level 3) of the product.</td>
<td>CategoryL3</td>
</tr>
<tr class="even">
<td>segments_product_category_level4</td>
<td>Category (level 4) of the product.</td>
<td>CategoryL4</td>
</tr>
<tr class="odd">
<td>segments_product_category_level5</td>
<td>Category (level 5) of the product.</td>
<td>CategoryL5</td>
</tr>
<tr class="even">
<td>segments_product_brand</td>
<td>Brand of the product.</td>
<td>Brand</td>
</tr>
<tr class="odd">
<td>segments_product_channel</td>
<td>Channel of the product.</td>
<td>Channel</td>
</tr>
<tr class="even">
<td>segments_product_channel_exclusivity</td>
<td>Channel exclusivity of the product.</td>
<td>ChannelExclusivity</td>
</tr>
<tr class="odd">
<td>segments_product_condition</td>
<td>Condition of the product.</td>
<td>ProductCondition</td>
</tr>
<tr class="even">
<td>segments_product_country</td>
<td>Resource name of the geo target constant for the country of sale of the product.</td>
<td>CountryCriteriaId</td>
</tr>
<tr class="odd">
<td>segments_product_custom_attribute0</td>
<td>Custom attribute 0 of the product.</td>
<td>CustomAttribute0</td>
</tr>
<tr class="even">
<td>segments_product_custom_attribute1</td>
<td>Custom attribute 1 of the product.</td>
<td>CustomAttribute1</td>
</tr>
<tr class="odd">
<td>segments_product_custom_attribute2</td>
<td>Custom attribute 2 of the product.</td>
<td>CustomAttribute2</td>
</tr>
<tr class="even">
<td>segments_product_custom_attribute3</td>
<td>Custom attribute 3 of the product.</td>
<td>CustomAttribute3</td>
</tr>
<tr class="odd">
<td>segments_product_custom_attribute4</td>
<td>Custom attribute 4 of the product.</td>
<td>CustomAttribute4</td>
</tr>
<tr class="even">
<td>segments_product_item_id</td>
<td>Item ID of the product.</td>
<td>OfferId</td>
</tr>
<tr class="odd">
<td>segments_product_language</td>
<td>Resource name of the language constant for the language of the product.</td>
<td>LanguageCriteriaId</td>
</tr>
<tr class="even">
<td>segments_product_merchant_id</td>
<td>Merchant ID of the product.</td>
<td>MerchantId</td>
</tr>
<tr class="odd">
<td>segments_product_store_id</td>
<td>Store ID of the product.</td>
<td>StoreId</td>
</tr>
<tr class="even">
<td>segments_product_type_l1</td>
<td>Type (level 1) of the product.</td>
<td>ProductTypeL1</td>
</tr>
<tr class="odd">
<td>segments_product_type_l2</td>
<td>Type (level 2) of the product.</td>
<td>ProductTypeL2</td>
</tr>
<tr class="even">
<td>segments_product_type_l3</td>
<td>Type (level 3) of the product.</td>
<td>ProductTypeL3</td>
</tr>
<tr class="odd">
<td>segments_product_type_l4</td>
<td>Type (level 4) of the product.</td>
<td>ProductTypeL4</td>
</tr>
<tr class="even">
<td>segments_product_type_l5</td>
<td>Type (level 5) of the product.</td>
<td>ProductTypeL5</td>
</tr>
<tr class="odd">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="even">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="odd">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: ShoppingProductStats

Google Ads API Resource: [shopping\_performance\_view](https://developers.google.com/google-ads/api/fields/v21/shopping_performance_view)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="odd">
<td>campaign_status</td>
<td>The status of the campaign. When a new campaign is added, the status defaults to ENABLED.</td>
<td></td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>AllConversions</td>
</tr>
<tr class="even">
<td>metrics_all_conversions_from_interactions_rate</td>
<td>All conversions from interactions (as oppose to view through conversions) divided by the number of ad interactions.</td>
<td>AllConversionRate</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions_value</td>
<td>The total value of all conversions.</td>
<td>AllConversionValue</td>
</tr>
<tr class="even">
<td>metrics_average_cpc</td>
<td>The total cost of all clicks divided by the total number of clicks received.</td>
<td>AverageCpc</td>
</tr>
<tr class="odd">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
<td>Clicks</td>
</tr>
<tr class="even">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>Conversions</td>
</tr>
<tr class="odd">
<td>metrics_conversions_from_interactions_rate</td>
<td>Conversions from interactions divided by the number of ad interactions (such as clicks for text ads or views for video ads). This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionRate</td>
</tr>
<tr class="even">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="odd">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
<td>Cost</td>
</tr>
<tr class="even">
<td>metrics_cost_per_all_conversions</td>
<td>The cost of ad interactions divided by all conversions.</td>
<td>CostPerAllConversion</td>
</tr>
<tr class="odd">
<td>metrics_cost_per_conversion</td>
<td>The cost of ad interactions divided by conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>CostPerConversion</td>
</tr>
<tr class="even">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on a Google Ads ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
<td>CrossDeviceConversions</td>
</tr>
<tr class="odd">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
<td>Ctr</td>
</tr>
<tr class="even">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
<td>Impressions</td>
</tr>
<tr class="odd">
<td>metrics_search_absolute_top_impression_share</td>
<td>The percentage of the customer's Shopping or Search ad impressions that are shown in the most prominent Shopping position. See https://support.google.com/google-ads/answer/7501826 for details. Any value below 0.1 is reported as 0.0999.</td>
<td>SearchAbsoluteTopImpressionShare</td>
</tr>
<tr class="even">
<td>metrics_search_click_share</td>
<td>The number of clicks you've received on the Search Network divided by the estimated number of clicks you were eligible to receive. Note: Search click share is reported in the range of 0.1 to 1. Any value below 0.1 is reported as 0.0999.</td>
<td>SearchClickShare</td>
</tr>
<tr class="odd">
<td>metrics_search_impression_share</td>
<td>The impressions you've received on the Search Network divided by the estimated number of impressions you were eligible to receive. Note: Search impression share is reported in the range of 0.1 to 1. Any value below 0.1 is reported as 0.0999.</td>
<td>SearchImpressionShare</td>
</tr>
<tr class="even">
<td>metrics_value_per_all_conversions</td>
<td>The value of all conversions divided by the number of all conversions.</td>
<td>ValuePerAllConversion</td>
</tr>
<tr class="odd">
<td>metrics_value_per_conversion</td>
<td>The value of conversions divided by the number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ValuePerConversion</td>
</tr>
<tr class="even">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="even">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="odd">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
<tr class="even">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="odd">
<td>segments_product_aggregator_id</td>
<td>Aggregator ID of the product.</td>
<td>AggregatorId</td>
</tr>
<tr class="even">
<td>segments_product_bidding_category_level1 <strong>(obsolete - use segments_product_category_level1 instead)</strong></td>
<td>Bidding category (level 1) of the product.</td>
<td>CategoryL1</td>
</tr>
<tr class="odd">
<td>segments_product_bidding_category_level2 <strong>(obsolete - use segments_product_category_level2 instead)</strong></td>
<td>Bidding category (level 2) of the product.</td>
<td>CategoryL2</td>
</tr>
<tr class="even">
<td>segments_product_bidding_category_level3 <strong>(obsolete - use segments_product_category_level3 instead)</strong></td>
<td>Bidding category (level 3) of the product.</td>
<td>CategoryL3</td>
</tr>
<tr class="odd">
<td>segments_product_bidding_category_level4 <strong>(obsolete - use segments_product_category_level4 instead)</strong></td>
<td>Bidding category (level 4) of the product.</td>
<td>CategoryL4</td>
</tr>
<tr class="even">
<td>segments_product_bidding_category_level5 <strong>(obsolete - use segments_product_category_level5 instead)</strong></td>
<td>Bidding category (level 5) of the product.</td>
<td>CategoryL5</td>
</tr>
<tr class="odd">
<td>segments_product_category_level1</td>
<td>Category (level 1) of the product.</td>
<td>CategoryL1</td>
</tr>
<tr class="even">
<td>segments_product_category_level2</td>
<td>Category (level 2) of the product.</td>
<td>CategoryL2</td>
</tr>
<tr class="odd">
<td>segments_product_category_level3</td>
<td>Category (level 3) of the product.</td>
<td>CategoryL3</td>
</tr>
<tr class="even">
<td>segments_product_category_level4</td>
<td>Category (level 4) of the product.</td>
<td>CategoryL4</td>
</tr>
<tr class="odd">
<td>segments_product_category_level5</td>
<td>Category (level 5) of the product.</td>
<td>CategoryL5</td>
</tr>
<tr class="even">
<td>segments_product_brand</td>
<td>Brand of the product.</td>
<td>Brand</td>
</tr>
<tr class="odd">
<td>segments_product_channel</td>
<td>Channel of the product.</td>
<td>Channel</td>
</tr>
<tr class="even">
<td>segments_product_channel_exclusivity</td>
<td>Channel exclusivity of the product.</td>
<td>ChannelExclusivity</td>
</tr>
<tr class="odd">
<td>segments_product_condition</td>
<td>Condition of the product.</td>
<td>ProductCondition</td>
</tr>
<tr class="even">
<td>segments_product_country</td>
<td>Resource name of the geo target constant for the country of sale of the product.</td>
<td>CountryCriteriaId</td>
</tr>
<tr class="odd">
<td>segments_product_custom_attribute0</td>
<td>Custom attribute 0 of the product.</td>
<td>CustomAttribute0</td>
</tr>
<tr class="even">
<td>segments_product_custom_attribute1</td>
<td>Custom attribute 1 of the product.</td>
<td>CustomAttribute1</td>
</tr>
<tr class="odd">
<td>segments_product_custom_attribute2</td>
<td>Custom attribute 2 of the product.</td>
<td>CustomAttribute2</td>
</tr>
<tr class="even">
<td>segments_product_custom_attribute3</td>
<td>Custom attribute 3 of the product.</td>
<td>CustomAttribute3</td>
</tr>
<tr class="odd">
<td>segments_product_custom_attribute4</td>
<td>Custom attribute 4 of the product.</td>
<td>CustomAttribute4</td>
</tr>
<tr class="even">
<td>segments_product_item_id</td>
<td>Item ID of the product.</td>
<td>OfferId</td>
</tr>
<tr class="odd">
<td>segments_product_language</td>
<td>Resource name of the language constant for the language of the product.</td>
<td>LanguageCriteriaId</td>
</tr>
<tr class="even">
<td>segments_product_merchant_id</td>
<td>Merchant ID of the product.</td>
<td>MerchantId</td>
</tr>
<tr class="odd">
<td>segments_product_type_l1</td>
<td>Type (level 1) of the product.</td>
<td>ProductTypeL1</td>
</tr>
<tr class="even">
<td>segments_product_type_l2</td>
<td>Type (level 2) of the product.</td>
<td>ProductTypeL2</td>
</tr>
<tr class="odd">
<td>segments_product_type_l3</td>
<td>Type (level 3) of the product.</td>
<td>ProductTypeL3</td>
</tr>
<tr class="even">
<td>segments_product_type_l4</td>
<td>Type (level 4) of the product.</td>
<td>ProductTypeL4</td>
</tr>
<tr class="odd">
<td>segments_product_type_l5</td>
<td>Type (level 5) of the product.</td>
<td>ProductTypeL5</td>
</tr>
<tr class="even">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="odd">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="even">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
</tbody>
</table>

Google Ads Table Name: Video

Google Ads API Resource: [video](https://developers.google.com/google-ads/api/fields/v21/video)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_ad_status</td>
<td>The status of the ad.</td>
<td></td>
</tr>
<tr class="even">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="odd">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="even">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="odd">
<td>video_duration_millis</td>
<td>The duration of the video in milliseconds.</td>
<td>VideoDuration</td>
</tr>
<tr class="even">
<td>video_id</td>
<td>The ID of the video.</td>
<td>VideoId</td>
</tr>
<tr class="odd">
<td>video_title</td>
<td>The title of the video.</td>
<td>VideoTitle</td>
</tr>
</tbody>
</table>

Google Ads Table Name: VideoBasicStats

Google Ads API Resource: [video](https://developers.google.com/google-ads/api/fields/v21/video)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_ad_ad_id</td>
<td>The ID of the ad.</td>
<td>CreativeId</td>
</tr>
<tr class="even">
<td>ad_group_ad_status</td>
<td>The status of the ad.</td>
<td>CreativeStatus</td>
</tr>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="even">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
<td>Clicks</td>
</tr>
<tr class="odd">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>Conversions</td>
</tr>
<tr class="even">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="odd">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
<td>Cost</td>
</tr>
<tr class="even">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
<td>Impressions</td>
</tr>
<tr class="odd">
<td>metrics_view_through_conversions</td>
<td>The total number of view-through conversions. These happen when a customer sees an image or rich media ad, then later completes a conversion on your site without interacting with (for example, clicking on) another ad.</td>
<td>ViewThroughConversions</td>
</tr>
<tr class="even">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="even">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
<tr class="odd">
<td>video_channel_id</td>
<td>The owner channel id of the video.</td>
<td>VideoChannelId</td>
</tr>
<tr class="even">
<td>video_id</td>
<td>The ID of the video.</td>
<td>VideoId</td>
</tr>
</tbody>
</table>

Google Ads Table Name: VideoConversionStats

Google Ads API Resource: [video](https://developers.google.com/google-ads/api/fields/v21/video)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_ad_ad_id</td>
<td>The ID of the ad.</td>
<td>CreativeId</td>
</tr>
<tr class="even">
<td>ad_group_ad_status</td>
<td>The status of the ad.</td>
<td>CreativeStatus</td>
</tr>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="even">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>Conversions</td>
</tr>
<tr class="odd">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="even">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="odd">
<td>segments_click_type</td>
<td>Click type.</td>
<td>ClickType</td>
</tr>
<tr class="even">
<td>segments_conversion_action</td>
<td>Resource name of the conversion action.</td>
<td>ConversionTrackerId</td>
</tr>
<tr class="odd">
<td>segments_conversion_action_category</td>
<td>Conversion action category.</td>
<td>ConversionCategoryName</td>
</tr>
<tr class="even">
<td>segments_conversion_action_name</td>
<td>Conversion action name.</td>
<td>ConversionTypeName</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="even">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="odd">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
<tr class="even">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="odd">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="even">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="odd">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
<tr class="even">
<td>video_channel_id</td>
<td>The owner channel id of the video.</td>
<td>VideoChannelId</td>
</tr>
<tr class="odd">
<td>video_id</td>
<td>The ID of the video.</td>
<td>VideoId</td>
</tr>
</tbody>
</table>

Google Ads Table Name: VideoNonClickStats

Google Ads API Resource: [video](https://developers.google.com/google-ads/api/fields/v21/video)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_ad_ad_id</td>
<td>The ID of the ad.</td>
<td>CreativeId</td>
</tr>
<tr class="even">
<td>ad_group_ad_status</td>
<td>The status of the ad.</td>
<td></td>
</tr>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="even">
<td>metrics_all_conversions</td>
<td>The total number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>AllConversions</td>
</tr>
<tr class="odd">
<td>metrics_all_conversions_from_interactions_rate</td>
<td>All conversions from interactions (as oppose to view through conversions) divided by the number of ad interactions.</td>
<td>AllConversionRate</td>
</tr>
<tr class="even">
<td>metrics_all_conversions_value</td>
<td>The total value of all conversions.</td>
<td>AllConversionValue</td>
</tr>
<tr class="odd">
<td>metrics_average_cpv</td>
<td>The average amount you pay each time someone views your ad. The average CPV is defined by the total cost of all ad views divided by the number of views.</td>
<td>AverageCpv</td>
</tr>
<tr class="even">
<td>metrics_cost_per_all_conversions</td>
<td>The cost of ad interactions divided by all conversions.</td>
<td>CostPerAllConversion</td>
</tr>
<tr class="odd">
<td>metrics_cross_device_conversions</td>
<td>Conversions from when a customer clicks on a Google Ads ad on one device, then converts on a different device or browser. Cross-device conversions are already included in all_conversions.</td>
<td>CrossDeviceConversions</td>
</tr>
<tr class="even">
<td>metrics_engagement_rate</td>
<td>How often people engage with your ad after it's shown to them. This is the number of ad expansions divided by the number of times your ad is shown.</td>
<td>EngagementRate</td>
</tr>
<tr class="odd">
<td>metrics_engagements</td>
<td>The number of engagements. An engagement occurs when a viewer expands your Lightbox ad. Also, in the future, other ad types may support engagement metrics.</td>
<td>Engagements</td>
</tr>
<tr class="even">
<td>metrics_value_per_all_conversions</td>
<td>The value of all conversions divided by the number of all conversions.</td>
<td>ValuePerAllConversion</td>
</tr>
<tr class="odd">
<td>metrics_video_quartile_p100_rate</td>
<td>Percentage of impressions where the viewer watched all of your video.</td>
<td>VideoQuartile100Rate</td>
</tr>
<tr class="even">
<td>metrics_video_quartile_p25_rate</td>
<td>Percentage of impressions where the viewer watched 25% of your video.</td>
<td>VideoQuartile25Rate</td>
</tr>
<tr class="odd">
<td>metrics_video_quartile_p50_rate</td>
<td>Percentage of impressions where the viewer watched 50% of your video.</td>
<td>VideoQuartile50Rate</td>
</tr>
<tr class="even">
<td>metrics_video_quartile_p75_rate</td>
<td>Percentage of impressions where the viewer watched 75% of your video.</td>
<td>VideoQuartile75Rate</td>
</tr>
<tr class="odd">
<td>metrics_video_view_rate</td>
<td>The number of views your TrueView video ad receives divided by its number of impressions, including thumbnail impressions for TrueView in-display ads.</td>
<td>VideoViewRate</td>
</tr>
<tr class="even">
<td>metrics_video_views</td>
<td>The number of times your video ads were viewed.</td>
<td>VideoViews</td>
</tr>
<tr class="odd">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="even">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="odd">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="even">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
<tr class="odd">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="even">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="odd">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="even">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
<tr class="odd">
<td>video_channel_id</td>
<td>The owner channel id of the video.</td>
<td>VideoChannelId</td>
</tr>
<tr class="even">
<td>video_id</td>
<td>The ID of the video.</td>
<td>VideoId</td>
</tr>
</tbody>
</table>

Google Ads Table Name: VideoStats

Google Ads API Resource: [video](https://developers.google.com/google-ads/api/fields/v21/video)

<table>
<thead>
<tr class="header">
<th>Google Ads Field Name</th>
<th>Description</th>
<th>Adwords Mapped Field Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_ad_ad_id</td>
<td>The ID of the ad.</td>
<td>CreativeId</td>
</tr>
<tr class="even">
<td>ad_group_ad_status</td>
<td>The status of the ad.</td>
<td>CreativeStatus</td>
</tr>
<tr class="odd">
<td>ad_group_id</td>
<td>The ID of the ad group.</td>
<td>AdGroupId</td>
</tr>
<tr class="even">
<td>campaign_id</td>
<td>The ID of the campaign.</td>
<td>CampaignId</td>
</tr>
<tr class="odd">
<td>customer_id</td>
<td>The ID of the customer.</td>
<td>ExternalCustomerId</td>
</tr>
<tr class="even">
<td>metrics_all_conversions_from_interactions_rate</td>
<td>All conversions from interactions (as oppose to view through conversions) divided by the number of ad interactions.</td>
<td>ConversionRate</td>
</tr>
<tr class="odd">
<td>metrics_average_cpm</td>
<td>Average cost-per-thousand impressions (CPM).</td>
<td>AverageCpm</td>
</tr>
<tr class="even">
<td>metrics_clicks</td>
<td>The number of clicks.</td>
<td>Clicks</td>
</tr>
<tr class="odd">
<td>metrics_conversions</td>
<td>The number of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>Conversions</td>
</tr>
<tr class="even">
<td>metrics_conversions_value</td>
<td>The total value of conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>ConversionValue</td>
</tr>
<tr class="odd">
<td>metrics_cost_micros</td>
<td>The sum of your cost-per-click (CPC) and cost-per-thousand impressions (CPM) costs during this period.</td>
<td>Cost</td>
</tr>
<tr class="even">
<td>metrics_cost_per_conversion</td>
<td>The cost of ad interactions divided by conversions. This only includes conversion actions which include_in_conversions_metric attribute is set to true.</td>
<td>CostPerConversion</td>
</tr>
<tr class="odd">
<td>metrics_ctr</td>
<td>The number of clicks your ad receives (Clicks) divided by the number of times your ad is shown (Impressions).</td>
<td>Ctr</td>
</tr>
<tr class="even">
<td>metrics_impressions</td>
<td>Count of how often your ad has appeared on a search results page or website on the Google Network.</td>
<td>Impressions</td>
</tr>
<tr class="odd">
<td>segments_ad_network_type</td>
<td>Ad network type.</td>
<td>AdNetworkType2</td>
</tr>
<tr class="even">
<td>segments_click_type</td>
<td>Click type.</td>
<td>ClickType</td>
</tr>
<tr class="odd">
<td>segments_date</td>
<td>Date to which metrics apply. yyyy-MM-dd format. For example, 2018-04-17.</td>
<td>Date</td>
</tr>
<tr class="even">
<td>segments_day_of_week</td>
<td>Day of the week. For example, MONDAY.</td>
<td>DayOfWeek</td>
</tr>
<tr class="odd">
<td>segments_device</td>
<td>Device to which metrics apply.</td>
<td>Device</td>
</tr>
<tr class="even">
<td>segments_month</td>
<td>Month as represented by the date of the first day of a month. Formatted as yyyy-MM-dd.</td>
<td>Month</td>
</tr>
<tr class="odd">
<td>segments_quarter</td>
<td>Quarter as represented by the date of the first day of a quarter. Uses the calendar year for quarters. For example, the second quarter of 2018 starts on 2018-04-01. Formatted as yyyy-MM-dd.</td>
<td>Quarter</td>
</tr>
<tr class="even">
<td>segments_week</td>
<td>Week as defined as Monday through Sunday, and represented by the date of Monday. Formatted as yyyy-MM-dd.</td>
<td>Week</td>
</tr>
<tr class="odd">
<td>segments_year</td>
<td>Year, formatted as yyyy.</td>
<td>Year</td>
</tr>
<tr class="even">
<td>video_channel_id</td>
<td>The owner channel id of the video.</td>
<td>VideoChannelId</td>
</tr>
<tr class="odd">
<td>video_id</td>
<td>The ID of the video.</td>
<td>VideoId</td>
</tr>
</tbody>
</table>

## Google Ads Match Tables

Google Ads Match Tables are tables that contain only **Attribute** fields (fields containing settings or other fixed data), and they are defined for users to query account structure information. If you use the refresh window or schedule a backfill, Match Table snapshots are not updated.

Below is a list of Match Tables in Google Ads transfer:

  - Ad
  - AdGroup
  - AdGroupAudience
  - AdGroupBidModifier
  - AdGroupAdLabel
  - AdGroupCriterion
  - AdGroupCriterionLabel
  - AdGroupLabel
  - AgeRange
  - Asset
  - AssetGroup
  - AssetGroupAsset
  - AssetGroupListingGroupFilter
  - AssetGroupSignal
  - Audience
  - BidGoal
  - Budget
  - Campaign
  - CampaignAudience
  - CampaignCriterion
  - CampaignLabel
  - Customer
  - Gender
  - Keyword
  - LocationBasedCampaignCriterion
  - ParentalStatus
  - Placement
  - Video
