# BigQuery Data Transfer Service data source change log

This page provides details about changes to BigQuery Data Transfer Service data source schemas and schema mappings. For information about upcoming changes to the BigQuery Data Transfer Service connectors, you can search this page for data sources, such as `  Google Ads API  ` or `  Display & Video 360 API  ` , or for specific table names or values.

## Campaign Manager 360

The BigQuery Data Transfer Service for Campaign Manager 360 connector periodically updates to support new, deprecated, or migrated columns. The BigQuery Data Transfer Service for Campaign Manager 360 connector retrieves data from Campaign Manager 360 [Data Transfer files](https://developers.google.com/doubleclick-advertisers/dtv2/reference/release-notes) .

The following sections outline the changes. Changes are organized by release date, and each entry provides information on the changes you need to make to continue receiving data from Campaign Manager 360.

### July 07, 2025

Campaign Manager 360 made an [announcement](https://support.google.com/campaignmanager/answer/16320235?hl=#111) to update its criterion IDs for browser, operating system, mobile make and model, and ISP data to align with the cross-platform data standards. After the migration, Campaign Manager 360 will stop populating values for deprecated columns and will start populating the new columns. The impacted columns are as follows:

<table>
<thead>
<tr class="header">
<th>Deprecated columns</th>
<th>New columns</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       DBM_Browser_Platform_ID      </code></td>
<td><code dir="ltr" translate="no">       DV360_Browser_Platform_Reportable_ID      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       DBM_ISP_ID      </code></td>
<td><code dir="ltr" translate="no">       DV360_ISP_Reportable_ID      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       DBM_Operating_System_ID      </code></td>
<td><code dir="ltr" translate="no">       DV360_Operating_System_Reportable_ID      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       DBM_Mobile_Make_ID      </code></td>
<td><code dir="ltr" translate="no">       DV360_Mobile_Make_Reportable_ID      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       DBM_Mobile_Model_ID      </code></td>
<td><code dir="ltr" translate="no">       DV360_Mobile_Model_Reportable_ID      </code></td>
</tr>
</tbody>
</table>

## Display & Video 360 API

The BigQuery Data Transfer Service for Display & Video 360 connector periodically updates to support new columns and adapt to changes introduced by new [Display & Video 360 API](https://developers.google.com/display-video/api/release-notes) versions. The BigQuery Data Transfer Service for Display & Video 360 connector uses the supported API version to retrieve [configuration data](/bigquery/docs/display-video-transfer#supported_configuration_data) .

The following sections outline the changes when updating to a new Display & Video 360 API version. Changes are organized by release date, and each entry provides information on the changes you need to make for you to continue receiving data from Display & Video 360.

### August 26, 2025

[The Display & Video 360 connector](/bigquery/docs/display-video-transfer) plans to update the [Display & Video 360 API version](https://developers.google.com/display-video/api/release-notes) used to retrieve configuration data from [v3](https://developers.google.com/display-video/api/reference/rest/v3) to [v4](https://developers.google.com/display-video/api/reference/rest/v4) . Changes from the API upgrade are listed in the following section. For more information, see [Display & Video 360 API v3 to v4 migration guide](https://developers.google.com/display-video/api/v4-migration-guide) .

This update for the Display & Video 360 connector is planned to start on August 26, 2025.

#### Deprecated Tables

The following tables will stop receiving new data. Existing data will remain, but no further updates will be populated.

  - `  CampaignTargeting  `
  - `  InsertionOrderTargeting  `

#### Tables with renamed columns

Tables affected

Deprecated columns

New columns

  - `  AdGroupTargeting  `
  - `  LineItemTargeting  `

`  audienceGroupDetails.includedFirstAndThirdPartyAudienceGroups  `

`  audienceGroupDetails.includedFirstPartyAndPartnerAudienceGroups  `

`  audienceGroupDetails.includedFirstAndThirdPartyAudienceGroups.settings  `

`  audienceGroupDetails.includedFirstPartyAndPartnerAudienceGroups.settings  `

`  audienceGroupDetails.includedFirstAndThirdPartyAudienceGroups.settings.firstAndThirdPartyAudienceId  `

`  audienceGroupDetails.includedFirstPartyAndPartnerAudienceGroups.settings.firstPartyAndPartnerAudienceId  `

`  audienceGroupDetails.includedFirstAndThirdPartyAudienceGroups.settings.recency  `

`  audienceGroupDetails.includedFirstPartyAndPartnerAudienceGroups.settings.recency  `

`  audienceGroupDetails.excludedFirstAndThirdPartyAudienceGroup  `

`  audienceGroupDetails.excludedFirstPartyAndPartnerAudienceGroup  `

`  audienceGroupDetails.excludedFirstAndThirdPartyAudienceGroup.settings  `

`  audienceGroupDetails.excludedFirstPartyAndPartnerAudienceGroup.settings  `

`  audienceGroupDetails.excludedFirstAndThirdPartyAudienceGroup.settings.firstAndThirdPartyAudienceId  `

`  audienceGroupDetails.excludedFirstPartyAndPartnerAudienceGroup.settings.firstPartyAndPartnerAudienceId  `

`  audienceGroupDetails.excludedFirstAndThirdPartyAudienceGroup.settings.recency  `

`  audienceGroupDetails.excludedFirstPartyAndPartnerAudienceGroup.settings.recency  `

#### Tables with deprecated columns

<table>
<thead>
<tr class="header">
<th>Tables affected</th>
<th>Deprecated columns</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       Creative      </code></td>
<td><code dir="ltr" translate="no">       reviewStatus.publisherReviewStatuses      </code></td>
</tr>
</tbody>
</table>

## Google Ads API

The BigQuery Data Transfer Service for Google Ads periodically updates to support new columns and adapt to changes introduced by new [Google Ads API](https://developers.google.com/google-ads/api/docs/release-notes) versions. The BigQuery Data Transfer Service for Google Ads connector uses the [supported API version](/bigquery/docs/google-ads-transfer#connector_overview) in the Google Ads connector.

The following sections outline the changes when updating to a new Google Ads API version. Changes are organized by release date, and each entry provides information on the changes you need to make for you to continue receiving data from Google Ads.

For more information about the Google Ads API release schedule, see [Timetable](https://developers.google.com/google-ads/api/docs/sunset-dates#timetable) .

### March 2, 2026

The [Google Ads connector](/bigquery/docs/google-ads-transfer) plans to update the [Google Ads API version](https://developers.google.com/google-ads/api/docs/release-notes) from [v21](https://developers.google.com/google-ads/api/fields/v21/overview) to [v22](https://developers.google.com/google-ads/api/fields/v22/overview) . After the API upgrade, the column values for newly transferred data in the affected tables will change. For more information, see [Google Ads API upgrade](https://developers.google.com/google-ads/api/docs/upgrade#v21-v22) .

Deprecated columns

New columns

Tables affected

`  metrics_average_cpv  `

`  metrics_trueview_average_cpv  `

  - `  AccountNonClickStats  `
  - `  AdCrossDeviceStats  `
  - `  AdGroupAudienceNonClickStats  `
  - `  AdGroupCrossDeviceStats  `
  - `  AgeRangeNonClickStats  `
  - `  BudgetStats  `
  - `  CampaignAssetStats  `
  - `  CampaignAudienceNonClickStats  `
  - `  CampaignCrossDeviceStats  `
  - `  CampaignLocationTargetStats  `
  - `  DisplayVideoAutomaticPlacementsStats  `
  - `  DisplayVideoKeywordStats  `
  - `  GenderNonClickStats  `
  - `  GeoStats  `
  - `  KeywordCrossDeviceStats  `
  - `  ParentalStatusNonClickStats  `
  - `  PlacementNonClickStats  `
  - `  SearchQueryStats  `
  - `  VideoNonClickStats  `

`  metrics_video_view_rate  `

`  metrics_video_trueview_view_rate  `

  - `  AccountNonClickStats  `
  - `  AdCrossDeviceStats  `
  - `  AdGroupAudienceNonClickStats  `
  - `  AdGroupCrossDeviceStats  `
  - `  AgeRangeNonClickStats  `
  - `  BudgetStats  `
  - `  CampaignAudienceNonClickStats  `
  - `  CampaignCrossDeviceStats  `
  - `  CampaignLocationTargetStats  `
  - `  DisplayVideoAutomaticPlacementsStats  `
  - `  GenderNonClickStats  `
  - `  GeoStats  `
  - `  KeywordCrossDeviceStats  `
  - `  ParentalStatusNonClickStats  `
  - `  PlacementNonClickStats  `
  - `  SearchQueryStats  `
  - `  VideoNonClickStats  `

`  metrics_video_views  `

`  metrics_video_trueview_views  `

  - `  AccountNonClickStats  `
  - `  AdCrossDeviceStats  `
  - `  AdGroupAudienceNonClickStats  `
  - `  AdGroupCrossDeviceStats  `
  - `  AgeRangeNonClickStats  `
  - `  BudgetStats  `
  - `  CampaignAudienceNonClickStats  `
  - `  CampaignCrossDeviceStats  `
  - `  CampaignLocationTargetStats  `
  - `  DisplayVideoAutomaticPlacementsStats  `
  - `  GenderNonClickStats  `
  - `  GeoStats  `
  - `  KeywordCrossDeviceStats  `
  - `  ParentalStatusNonClickStats  `
  - `  PlacementNonClickStats  `
  - `  SearchQueryStats  `
  - `  VideoNonClickStats  `

By Jan 16, 2026, the Google Ads connector will add the columns `  metrics_trueview_average_cpv  ` , `  metrics_video_trueview_view_rate  ` and `  metrics_video_trueview_views  ` to the table schema and populate them with `  null  ` . After the update to Google Ads API v22 on March 2, 2026, these new columns will be populated with new values. Some columns are now deprecated, such as `  metrics_average_cpv  ` , `  metrics_video_view_rate  ` and `  metrics_video_views  ` . Deprecated columns are now populated with `  null  ` , but will still remain in the table schema.

For each pair of columns, only one column is populated with values from the Google Ads API while the other is populated with `  null  ` . In response to the Google Ads API v22 update, update your queries to specify one of the two columns. For example, if your SQL query selects the column `  metrics_average_cpv  ` , update the query so that it specifies the correct column:

``` text
IFNULL(metrics_average_cpv, metrics_trueview_average_cpv)
```

If you use [custom reports](/bigquery/docs/google-ads-transfer#custom_reports) , see the [Google Ads API v22 reference page](https://developers.google.com/google-ads/api/fields/v22/overview) and the [Google Ads API release notes](https://developers.google.com/google-ads/api/docs/release-notes) to update impacted GAQL queries after the [Google Ads connector](/bigquery/docs/google-ads-transfer) is upgraded to Google Ads v22 API. If you use [custom reports](/bigquery/docs/google-ads-transfer#custom_reports) , see the [Google Ads API v22 reference page](https://developers.google.com/google-ads/api/fields/v22/overview) and the [Google Ads API release notes](https://developers.google.com/google-ads/api/docs/release-notes) to update impacted GAQL queries after the [Google Ads connector](/bigquery/docs/google-ads-transfer) is upgraded to Google Ads v22 API.

### August 1, 2025

[Google Ads transfers](/bigquery/docs/google-ads-transfer) plans to update the [Google Ads API version](https://developers.google.com/google-ads/api/docs/release-notes) from [v18](https://developers.google.com/google-ads/api/reference/rpc/v18/overview) to [v20](https://developers.google.com/google-ads/api/reference/rpc/v20/overview) . After the API upgrade, the column values for newly transferred data in the affected tables will change. For more information, see [Google Ads API upgrade](https://developers.google.com/google-ads/api/docs/upgrade#v18-v19) .

#### Table: `     p_ads_Ad_customer_id    `

<table>
<thead>
<tr class="header">
<th>Columns impacted</th>
<th>Deprecated data type</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_group_type</td>
<td>VIDEO_OUTSTREAM</td>
</tr>
<tr class="even">
<td>ad_group_ad_ad_type</td>
<td>VIDEO_OUTSTREAM</td>
</tr>
</tbody>
</table>

#### Table: `     p_ads_Campaign_customer_id    `

<table>
<thead>
<tr class="header">
<th>Columns impacted</th>
<th>Deprecated data type</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>campaign_advertising_channel_sub_type</td>
<td>VIDEO_OUTSTREAM</td>
</tr>
</tbody>
</table>

#### Table: `     p_ads_DisplayVideoKeywordStats_customer_id    `

<table>
<thead>
<tr class="header">
<th>Columns impacted</th>
<th>Deprecated data type</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>campaign_advertising_channel_sub_type</td>
<td>VIDEO_OUTSTREAM</td>
</tr>
</tbody>
</table>

### January 20, 2025

[Google Ads transfers](/bigquery/docs/google-ads-transfer) plans to update the [Google Ads API version](https://developers.google.com/google-ads/api/docs/release-notes) from [v16](https://developers.google.com/google-ads/api/reference/rpc/v16/overview) to [v18](https://developers.google.com/google-ads/api/reference/rpc/v18/overview) . After the API upgrade, the column values for newly transferred data in the affected tables will change. For more information, see [Google Ads API upgrade](https://developers.google.com/google-ads/api/docs/upgrade#v17-v18) .

This update for the Google Ads connector started on January 20, 2025, and was completed on February 4, 2025.

#### Table: `     p_ads_Campaign_customer_id    `

<table>
<thead>
<tr class="header">
<th>Columns impacted</th>
<th>Old value (v16)</th>
<th>New value (v18)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>campaign_advertising_channel_type</td>
<td>DISCOVERY</td>
<td>DEMAND_GEN</td>
</tr>
</tbody>
</table>

#### Table: `     p_ads_Ad_customer_id    `

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Columns impacted</th>
<th>Old value (v16)</th>
<th>New value (v18)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ad_type</td>
<td><p>DISCOVERY_MULTI_ASSET_AD</p>
<p>DISCOVERY_CAROUSEL_AD</p>
<p>DISCOVERY_VIDEO_RESPONSIVE_AD</p></td>
<td><p>DEMAND_GEN_MULTI_ASSET_AD</p>
<p>DEMAND_GEN_CAROUSEL_AD</p>
<p>DEMAND_GEN_VIDEO_RESPONSIVE_AD</p></td>
</tr>
</tbody>
</table>

#### Table: `     Asset    `

<table>
<thead>
<tr class="header">
<th>Columns impacted</th>
<th>Old value (v16)</th>
<th>New value (v18)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>asset_type</td>
<td>DISCOVERY_CAROUSEL_CARD</td>
<td>DEMAND_GEN_CAROUSEL_CARD</td>
</tr>
</tbody>
</table>

To ensure your queries work after the update, change your queries to select both old and new values. For example, if you have the following `  WHERE  ` condition in your SQL query:

``` text
WHERE asset_type='DISCOVERY_CAROUSEL_CARD'
```

Replace with the following statement:

``` text
WHERE
  asset_type='DISCOVERY_CAROUSEL_CARD'
  OR asset_type='DEMAND_GEN_CAROUSEL_CARD'
```

### June 24, 2024

[Google Ads transfers](/bigquery/docs/google-ads-transfer) plans to update the [Google Ads API version](https://developers.google.com/google-ads/api/docs/release-notes) from v14 to [v16](https://developers.google.com/google-ads/api/reference/rpc/v16/overview) . In this API upgrade, the column names for newly transferred data in the affected tables are changed. Also, some columns are deprecated. For more information, see [Google Ads API upgrade](https://developers.google.com/google-ads/api/docs/upgrade#v17-v18) .

This update for the Google Ads connector started on June 17, 2024, and was completed on June 23, 2024.

Tables affected

Deprecated columns

New columns

  - `  ShoppingProductStats  `
  - `  ShoppingProductConversionStats  `

`  segments_product_bidding_category_level1  `

`  segments_product_category_level1  `

`  segments_product_bidding_category_level2  `

`  segments_product_category_level2  `

`  segments_product_bidding_category_level3  `

`  segments_product_category_level3  `

`  segments_product_bidding_category_level4  `

`  segments_product_category_level4  `

`  segments_product_bidding_category_level5  `

`  segments_product_category_level5  `

  - `  ProductGroupStats  `

`  ad_group_criterion_listing_group_case_value_product_bidding_category_id  `

`  ad_group_criterion_listing_group_case_value_product_category_category_id  `

`  ad_group_criterion_listing_group_case_value_product_bidding_category_level  `

`  ad_group_criterion_listing_group_case_value_product_category_level  `

  - `  AssetGroupListingFilter  `

`  asset_group_listing_group_filter_case_value_product_bidding_category_id  `

`  asset_group_listing_group_filter_case_value_product_category_category_id  `

`  asset_group_listing_group_filter_case_value_product_bidding_category_level  `

`  asset_group_listing_group_filter_case_value_product_category_level  `

`  asset_group_listing_group_filter_vertical  `

`  asset_group_listing_group_filter_listing_source  `

With Google Ads API v14, new columns, such as `  segments_product_category_level1  ` and `  segments_product_category_level2  ` , were added to the BigQuery table schema but were populated with `  null  ` . With the update to Google Ads API v16, these new columns will be populated with new values. Deprecated columns, such as `  segments_product_bidding_category_level1  ` and `  segments_product_bidding_category_level2  ` , will be populated with `  null  ` , but will still remain in the table schema.

For each pair of columns, only one column is populated with values from the Google Ads API while the other will be populated with `  null  ` . To ensure your existing queries keep working after the update, update your queries to choose one of the two columns. For example, if you have the following statement in your SQL query:

``` text
segments_product_bidding_category_level1
```

Replace with the following statement that specifies the correct column:

``` text
IFNULL(segments_product_category_level1, segments_product_bidding_category_level1)
```

Transfer configurations that are created after June 24th 2024 will always use the new columns. Deprecated columns will still remain in the table schema but populated with `  null  ` .

## Google Analytics API

The BigQuery Data Transfer Service for Google Analytics connector periodically updates to support new columns and adapt to changes introduced by new [Google Analytics Data API](https://developers.google.com/analytics/devguides/reporting/data/v1/changelog) versions. The BigQuery Data Transfer Service for Google Analytics connector uses the latest supported API version to retrieve reporting data.

The following sections outline the changes when updating to a new Google Analytics Data API version. Changes are organized by release date, and each entry provides information on the changes you need to make to continue receiving data from Google Analytics.

### September 22, 2025

**Note:** These changes only affect users who used the Google Analytics connector before April 25, 2025.

[The Google Analytics connector](/bigquery/docs/google-analytics-4-transfer) plans to deprecate tables and update schemas to reflect changes in [Google Analytics Data API v1](https://developers.google.com/analytics/devguides/reporting/data/v1/changelog) . These changes are listed in the following sections.

This update for the Google Analytics connector is planned to start on September 22, 2025.

#### Deprecated tables

The following table shows the tables that will be deprecated and replaced with new tables with updated schemas. Note that the `  p_ga4_conversions  ` and `  p_ga4_inAppPurchases  ` tables will be discontinued after this update. Both deprecated and new tables will be populated until September 22, 2025 to allow time for migration. You can filter out deprecated tables using the [Table Filter](/bigquery/docs/google-analytics-4-transfer#set-up-ga4-transfer) option in the transfer configuration.

<table>
<thead>
<tr class="header">
<th>Deprecated Table</th>
<th>New Table</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       p_ga4_audiences      </code></td>
<td><code dir="ltr" translate="no">       p_ga4_Audiences      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       p_ga4_conversions      </code></td>
<td><code dir="ltr" translate="no">       Deprecated      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       p_ga4_demographicDetails      </code></td>
<td><code dir="ltr" translate="no">       p_ga4_DemographicDetails      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       p_ga4_ecommercePurchase      </code></td>
<td><code dir="ltr" translate="no">       p_ga4_EcommercePurchase      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       p_ga4_events      </code></td>
<td><code dir="ltr" translate="no">       p_ga4_Events      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       p_ga4_inAppPurchases      </code></td>
<td><code dir="ltr" translate="no">       Deprecated      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       p_ga4_landingPage      </code></td>
<td><code dir="ltr" translate="no">       p_ga4_LandingPage      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       p_ga4_pagesAndScreens      </code></td>
<td><code dir="ltr" translate="no">       p_ga4_PagesAndScreens      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       p_ga4_promotions      </code></td>
<td><code dir="ltr" translate="no">       p_ga4_Promotions      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       p_ga4_techDetails      </code></td>
<td><code dir="ltr" translate="no">       p_ga4_TechDetails      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       p_ga4_trafficAcquisition      </code></td>
<td><code dir="ltr" translate="no">       p_ga4_TrafficAcquisition      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       p_ga4_userAcquisition      </code></td>
<td><code dir="ltr" translate="no">       p_ga4_UserAcquisition      </code></td>
</tr>
</tbody>
</table>

#### Updated table schemas

New table schemas can be found on the [Google Analytics report transformation](/bigquery/docs/google-analytics-4-transformation) page.

Summary of schema changes:

  - **Corrected schemas:** The schemas for traffic acquisition, user acquisition, and landing page reports are corrected. For example, traffic acquisition and user acquisition report schemas were previously swapped, and the landing page report was missing the `  landingPage  ` dimension.
  - **Field renaming and discontinuation:** The conversions field is renamed to `  keyEvents  ` across all reports to align with current Google Analytics terminology. Consequently, the "conversions" report itself is discontinued.
  - **Data type changes:** Revenue fields change from `  INTEGER  ` to `  FLOAT  ` in BigQuery to accurately represent floating-point micro values as returned by the API.
  - **New table and field naming convention:** Field names in new tables use `  camelCase  ` (for example, `  eventCount  ` ) for consistency with the Google Analytics API, replacing the previous `  snake_case  ` (for example, `  event_count  ` ).

## Google Play Console

The BigQuery Data Transfer Service for Google Play connector periodically updates to support new reports and changes of current reports introduced by Google Play.

The following sections outline the changes organized by release date.

### December 1, 2025

Google Play plans to make the following changes to the [Earnings report](https://support.google.com/googleplay/android-developer/answer/6135870#financial&zippy=%2Cearnings) . The changes will be reflected in the BigQuery table `  p_Earnings_ suffix  ` . These changes are listed in the following sections.

#### Renamed columns

The following Google Play columns will be renamed.

<table>
<thead>
<tr class="header">
<th>Deprecated columns</th>
<th>New columns</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       Base_Plan_ID      </code></td>
<td><code dir="ltr" translate="no">       Base_Plan_or_Purchase_Option_ID      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       Product_id      </code></td>
<td><code dir="ltr" translate="no">       Package_ID      </code></td>
</tr>
</tbody>
</table>

#### Column value change

The column `  Product_Type  ` will change from a numeric representation to a human-readable string.

#### New column

A new column `  Sales_Channel  ` will be added to the Earnings report. This field provides information on where the sale originates from.

## Salesforce Bulk API

The BigQuery Data Transfer Service for Salesforce connector periodically updates to support changes introduced by the Salesforce Bulk API.

The following sections outline the changes when the Salesforce connector updates to a new Bulk API version. Changes are organized by release date, and each entry provides information on the changes you need to make for you to continue receiving data from Salesforce.

### October 14, 2025

As part of the Salesforce connector GA release, the Salesforce connector now uses Salesforce Bulk API V1 version 64.0. Several fields that were supported in the Salesforce Bulk API V1 version 53.0 are no longer supported.

#### Deprecated fields

The following table shows the fields deprecated with the Salesforce connector GA release, along with the `  sObject  ` name associated with each field.

<table>
<thead>
<tr class="header">
<th>Deprecated Field</th>
<th><code dir="ltr" translate="no">       sObject      </code> name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       EffectiveDate      </code></td>
<td><code dir="ltr" translate="no">       MobSecurityCertPinConfig      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       PermissionsAllowObjectDetectionTraining      </code></td>
<td><code dir="ltr" translate="no">       Profile      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       PermissionsAllowObjectDetection      </code></td>
<td><code dir="ltr" translate="no">       Profile      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       PermissionsAllowObjectDetectionTraining      </code></td>
<td><code dir="ltr" translate="no">       PermissionSet      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       PermissionsAllowObjectDetection      </code></td>
<td><code dir="ltr" translate="no">       PermissionSet      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       MaximumPermissionsAllowObjectDetectionTraining      </code></td>
<td><code dir="ltr" translate="no">       PermissionSetLicense      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       MaximumPermissionsAllowObjectDetection      </code></td>
<td><code dir="ltr" translate="no">       PermissionSetLicense      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       PermissionsAllowObjectDetectionTraining      </code></td>
<td><code dir="ltr" translate="no">       UserPermissionAccess      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       PermissionsAllowObjectDetection      </code></td>
<td><code dir="ltr" translate="no">       UserPermissionAccess      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       PermissionsAllowObjectDetectionTraining      </code></td>
<td><code dir="ltr" translate="no">       MutingPermissionSet      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       PermissionsAllowObjectDetection      </code></td>
<td><code dir="ltr" translate="no">       MutingPermissionSet      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       OptionsHstsHeaders      </code></td>
<td><code dir="ltr" translate="no">       Domain      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       UserPreferencesHideInvoicesRedirectConfirmation      </code></td>
<td><code dir="ltr" translate="no">       User      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       UserPreferencesHideStatementsRedirectConfirmation      </code></td>
<td><code dir="ltr" translate="no">       User      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       UserPreferencesHideInvoicesRedirectConfirmation      </code></td>
<td><code dir="ltr" translate="no">       UserChangeEvent      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       UserPreferencesHideStatementsRedirectConfirmation      </code></td>
<td><code dir="ltr" translate="no">       UserChangeEvent      </code></td>
</tr>
</tbody>
</table>

## YouTube Reporting API

The BigQuery Data Transfer Service for YouTube Content Owner connector and YouTube Channel connector periodically updates to support new reports introduced by [YouTube Reporting API](https://developers.google.com/youtube/reporting) and deprecate old reports.

The following sections outline the changes when new reports are introduced by YouTube Reporting API. Changes are organized by release date, and each entry provides information on the changes you need to make to continue receiving data from YouTube.

### September 22, 2025

[The YouTube Content Owner connector](/bigquery/docs/youtube-content-owner-transfer) and [The YouTube Channel connector](/bigquery/docs/youtube-channel-transfer) plan to introduce new reports and deprecate old reports to reflect the YouTube [shorts view count change](https://support.google.com/youtube/thread/333869549/a-change-to-how-we-count-views-on-shorts) . These changes are listed in the following sections.

New reports are planned to start on July 7, 2025. No action is required from you to get the new reports. The deprecation of old reports is planned to start on September 22, 2025.

#### YouTube Content Owner connector - deprecated tables

For the YouTube Content Owner connector, the following table shows the BigQuery tables that will be deprecated and replaced with new tables with updated schemas. Both deprecated and new tables will be populated until September 22, 2025 to allow time for migration. After September 22, 2025, only the new tables will be populated. The value for suffix is the table suffix you configured when you created the transfer.

<table>
<thead>
<tr class="header">
<th>Deprecated Table</th>
<th>New Table</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       p_content_owner_asset_basic_a2_               suffix       </code></td>
<td><code dir="ltr" translate="no">       p_content_owner_asset_basic_a3_               suffix       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       p_content_owner_asset_combined_a2_               suffix       </code></td>
<td><code dir="ltr" translate="no">       p_content_owner_asset_combined_a3_               suffix       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       p_content_owner_asset_device_os_a2_               suffix       </code></td>
<td><code dir="ltr" translate="no">       p_content_owner_asset_device_os_a3_               suffix       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       p_content_owner_asset_playback_location_a2_               suffix       </code></td>
<td><code dir="ltr" translate="no">       p_content_owner_asset_playback_location_a3_               suffix       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       p_content_owner_asset_province_a2_               suffix       </code></td>
<td><code dir="ltr" translate="no">       p_content_owner_asset_province_a3_               suffix       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       p_content_owner_asset_traffic_source_a2_               suffix       </code></td>
<td><code dir="ltr" translate="no">       p_content_owner_asset_traffic_source_a3_               suffix       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       p_content_owner_basic_a3_               suffix       </code></td>
<td><code dir="ltr" translate="no">       p_content_owner_basic_a4_               suffix       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       p_content_owner_combined_a2_               suffix       </code></td>
<td><code dir="ltr" translate="no">       p_content_owner_combined_a3_               suffix       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       p_content_owner_device_os_a2_               suffix       </code></td>
<td><code dir="ltr" translate="no">       p_content_owner_device_os_a3_               suffix       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       p_content_owner_playback_location_a2_               suffix       </code></td>
<td><code dir="ltr" translate="no">       p_content_owner_playback_location_a3_               suffix       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       p_content_owner_playlist_basic_a1_               suffix       </code></td>
<td><code dir="ltr" translate="no">       p_content_owner_playlist_basic_a2_               suffix       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       p_content_owner_playlist_combined_a1_               suffix       </code></td>
<td><code dir="ltr" translate="no">       p_content_owner_playlist_combined_a2_               suffix       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       p_content_owner_playlist_device_os_a1_               suffix       </code></td>
<td><code dir="ltr" translate="no">       p_content_owner_playlist_device_os_a2_               suffix       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       p_content_owner_playlist_playback_location_a1_               suffix       </code></td>
<td><code dir="ltr" translate="no">       p_content_owner_playlist_playback_location_a2_               suffix       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       p_content_owner_playlist_province_a1_               suffix       </code></td>
<td><code dir="ltr" translate="no">       p_content_owner_playlist_province_a2_               suffix       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       p_content_owner_playlist_traffic_source_a1_               suffix       </code></td>
<td><code dir="ltr" translate="no">       p_content_owner_playlist_traffic_source_a2_               suffix       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       p_content_owner_province_a2_               suffix       </code></td>
<td><code dir="ltr" translate="no">       p_content_owner_province_a3_               suffix       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       p_content_owner_subtitles_a2_               suffix       </code></td>
<td><code dir="ltr" translate="no">       p_content_owner_subtitles_a3_               suffix       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       p_content_owner_traffic_source_a2_               suffix       </code></td>
<td><code dir="ltr" translate="no">       p_content_owner_traffic_source_a3_               suffix       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       p_content_owner_shorts_ad_revenue_summary_a1_               suffix       </code></td>
<td><code dir="ltr" translate="no">       p_content_owner_shorts_ad_revenue_summary_a2_               suffix       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       p_content_owner_shorts_country_ad_revenue_summary_a1_               suffix       </code></td>
<td><code dir="ltr" translate="no">       p_content_owner_shorts_country_ad_revenue_summary_a2_               suffix       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       p_content_owner_shorts_day_ad_revenue_summary_a1_               suffix       </code></td>
<td><code dir="ltr" translate="no">       p_content_owner_shorts_day_ad_revenue_summary_a2_               suffix       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       p_content_owner_shorts_global_ad_revenue_summary_a1_               suffix       </code></td>
<td><code dir="ltr" translate="no">       p_content_owner_shorts_global_ad_revenue_summary_a2_               suffix       </code></td>
</tr>
</tbody>
</table>

#### YouTube Channel connector - deprecated tables

For the YouTube Channel connector, the following table shows the BigQuery tables that will be deprecated and replaced with new tables with updated schemas. Both deprecated and new tables will be populated until September 22, 2025 to allow time for migration. After September 22, 2025, only the new tables will be populated. The value for suffix is the table suffix you configured when you created the transfer.

<table>
<thead>
<tr class="header">
<th>Deprecated Table</th>
<th>New Table</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       p_channel_basic_a2_               suffix       </code></td>
<td><code dir="ltr" translate="no">       p_channel_basic_a3_               suffix       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       p_channel_combined_a2_               suffix       </code></td>
<td><code dir="ltr" translate="no">       p_channel_combined_a3_               suffix       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       p_channel_device_os_a2_               suffix       </code></td>
<td><code dir="ltr" translate="no">       p_channel_device_os_a3_               suffix       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       p_channel_playback_location_a2_               suffix       </code></td>
<td><code dir="ltr" translate="no">       p_channel_playback_location_a3_               suffix       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       p_channel_province_a2_               suffix       </code></td>
<td><code dir="ltr" translate="no">       p_channel_province_a3_               suffix       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       p_channel_subtitles_a2_               suffix       </code></td>
<td><code dir="ltr" translate="no">       p_channel_subtitles_a3_               suffix       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       p_channel_traffic_source_a2_               suffix       </code></td>
<td><code dir="ltr" translate="no">       p_channel_traffic_source_a3_               suffix       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       p_playlist_basic_a1_               suffix       </code></td>
<td><code dir="ltr" translate="no">       p_playlist_basic_a2_               suffix       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       p_playlist_combined_a1_               suffix       </code></td>
<td><code dir="ltr" translate="no">       p_playlist_combined_a2_               suffix       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       p_playlist_device_os_a1_               suffix       </code></td>
<td><code dir="ltr" translate="no">       p_playlist_device_os_a2_               suffix       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       p_playlist_playback_location_a1_               suffix       </code></td>
<td><code dir="ltr" translate="no">       p_playlist_playback_location_a2_               suffix       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       p_playlist_province_a1_               suffix       </code></td>
<td><code dir="ltr" translate="no">       p_playlist_province_a2_               suffix       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       p_playlist_traffic_source_a1_               suffix       </code></td>
<td><code dir="ltr" translate="no">       p_playlist_traffic_source_a2_               suffix       </code></td>
</tr>
</tbody>
</table>

#### Updated table schemas

The new tables will have a new column named `  engaged_views  ` . For more information about this metric, see [Shorts Viewcounting Changes](https://support.google.com/youtubekb/answer/10950071) .
