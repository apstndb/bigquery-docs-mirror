---
name: documents/docs.cloud.google.com/bigquery/docs/facebook-ads-transformation
uri: https://docs.cloud.google.com/bigquery/docs/facebook-ads-transformation
title: Facebook Ads report transformation
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# Facebook Ads report transformation

This document describes how your Facebook Ads reports are transformed when you [run a Facebook Ads transfer to BigQuery](https://docs.cloud.google.com/bigquery/docs/facebook-ads-transfer) .

## Table mapping for Facebook Ads reports

When your Facebook Ads reports are transferred to BigQuery, the reports are transformed into the following BigQuery tables and views.

### `AdAccounts` report

| **Meta API field name**        | **Mapped BigQuery field name** | **Type**   | **Description**                                                                                                                                                |
| ------------------------------ | ------------------------------ | ---------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`                           | ID \[KEY\]                     | *String*   | The Id of Ad Account.                                                                                                                                          |
| `  `                           | Target                         | *String*   | The target used to get ad accounts from. This value is \`null\` - to get all ad accounts.                                                                      |
| `account_id`                   | AccountId                      | *String*   | The Id of the Ad Account when viewed directly in Facebook.                                                                                                     |
| `account_status`               | AccountStatus                  | *Integer*  | Status of the account. 1 = Active, 2 = Disabled, 3 = Unsettled, 7 = Pending Review, 9 = in Grace Period, 101 = temporarily unavailable, 100 = pending closure. |
| `age`                          | Age                            | *Double*   | Amount of time the ad account has been open, in days.                                                                                                          |
| `amount_spent`                 | AmountSpent                    | *Integer*  | Current total amount spent by the account. This can be reset.                                                                                                  |
| `balance`                      | Balance                        | *Integer*  | Bill amount due.                                                                                                                                               |
| `business_city`                | BusinessCity                   | *String*   | City for business address.                                                                                                                                     |
| `business_country_code`        | BusinessCountryCode            | *String*   | Country code for the business address.                                                                                                                         |
| `business_name`                | BusinessName                   | *String*   | The business name for the account.                                                                                                                             |
| `business_state`               | BusinessState                  | *String*   | State abbreviation for business address.                                                                                                                       |
| `business_street`              | BusinessStreet                 | *String*   | First line of the business street address for the account.                                                                                                     |
| `business_street2`             | BusinessStreet2                | *String*   | Second line of the business street address for the account.                                                                                                    |
| `business_zip`                 | BusinessZip                    | *String*   | Zip code for business address.                                                                                                                                 |
| `capabilities`                 | Capabilities                   | *String*   | Capabilities allowed for this ad account.                                                                                                                      |
| `created_time`                 | CreatedTime                    | *Datetime* | The time the account was created.                                                                                                                              |
| `currency`                     | Currency                       | *String*   | The currency used for the account, based on the corresponding value in the account settings.                                                                   |
| `min_campaign_group_spend_cap` | MinCampaignGroupSpendCap       | *String*   | The minimum campaign group spend limit.                                                                                                                        |
| `name`                         | Name                           | *String*   | Name of the account; note that many accounts are unnamed, so this field may be empty.                                                                          |
| `offsite_pixels_tos_accepted`  | OffsitePixelsTosAccepted       | *String*   | Indicates whether the offsite pixel Terms Of Service contract was signed.                                                                                      |
| `owner`                        | OwnerId                        | *String*   | Facebook ID of the owner for the Ad Account.                                                                                                                   |
| `spend_cap`                    | SpendCap                       | *Integer*  | The maximum that can be spent by this account after which campaigns will be paused. A value of 0 signifies no spending-cap.                                    |
| `timezone_id`                  | TimezoneId                     | *String*   | ID for the timezone.                                                                                                                                           |
| `timezone_name`                | TimezoneName                   | *String*   | Name for the timezone.                                                                                                                                         |
| `timezone_offset_hours_utc`    | TimezoneOffsetHoursUTC         | *Double*   | Time Zone difference from UTC.                                                                                                                                 |

### `AdInsights` report

**Meta API field name**

**Mapped BigQuery field name**

**Type**

**Description**

`  `

Target

*String*

The Id of the Account to get insights for.

`date_start`

DateStart

*Date*

The starting date to retrieve insights. In the Facebook UI, this is the Report Start field.

`date_stop`

DateEnd

*Date*

The ending date to retrieve insights. In the Facebook UI, this is the Report End field.

`  `

TimeIncrement

*String*

The number of days of data aggregation. This value is set to 1.

`  `

Level

*String*

The level to represent the results at. This value is set to \`ad\`.

`account_currency`

AccountCurrency

*String*

The currency that is being used by the ad account.

`action_attribution_windows`

ActionAttributionWindows

*String*

A comma separated list that determines what is the attribution window for the actions. For example, 28d\_click means the API returns all actions that happened 28 days after someone clicked on the ad. This option is set at \[1d\_view,28d\_click\].

`account_id`

AdAccountId

*String*

The Id of the Ad Account that is associated with the report row.

`account_name`

AdAccountName

*String*

The name of the Ad Account that is associated with the report row.

`campaign_id`

CampaignId

*String*

The Id of the Campaign that is associated with the report row.

`campaign_name`

CampaignName

*String*

The name of the Campaign that is associated with the report row.

`adset_id`

AdSetId

*String*

The Id of the Ad Set that is associated with the report row.

`adset_name`

AdSetName

*String*

The name of the Ad Set that is associated with the report row.

`ad_id`

AdId

*String*

The Id of the Ad that is associated with the report row.

`ad_name`

AdName

*String*

The name of the Ad that is associated with the report row.

`buying_type`

BuyingType

*String*

The method by which target ads are paid for in your campaigns.

`clicks`

Clicks

*Long*

The total number of clicks on your ad. Depending on what you're promoting, this can include Page likes, event responses or app installs. In the Facebook UI, this is the Clicks (All) field.

`conversion_rate_ranking`

ConversionRateRanking

*String*

The conversion rate ranking.

`cost_per_estimated_ad_recallers`

CostPerEstimatedAdRecallers

*Decimal*

The average cost per additional person that we estimate will recall seeing your ad if asked within 2 days.

`cost_per_inline_link_click`

CostPerInlineLinkClick

*Decimal*

The average cost per click on links in the ad.

`cost_per_inline_post_engagement`

CostPerInlinePostEngagement

*Decimal*

The average cost per engagement on the post.

`cost_per_unique_click`

CostPerUniqueClick

*Decimal*

The average cost per unique click for these ads, calculated as the amount spent divided by the number of unique clicks received.

`cost_per_unique_inline_link_click`

CostPerUniqueInlineLinkClick

*Decimal*

The average you paid for each unique inline link click.

`cpc`

CPC

*Decimal*

The average cost per click for these ads, calculated as the amount spent divided by the number of clicks received.

`cpm`

CPM

*Decimal*

The average cost that you've paid to have 1,000 impressions on your ad.

`cpp`

CPP

*Decimal*

The average cost that you've paid to have your ad served to 1,000 unique people.

`ctr`

CTR

*Double*

The number of clicks you received divided by the number of impressions. In the Facebook UI, this is the CTR (All) % field.

`estimated_ad_recall_rate`

EstimatedAdRecallRate

*Double*

The estimated number of people who recall your ad divided by the number of people your ad reached.

`estimated_ad_recallers`

EstimatedAdRecallers

*Double*

The additional number of people that we estimate will remember seeing your ads if asked within 2 days.

`frequency`

Frequency

*Double*

The average number of times that your ad was served to each person.

`impressions`

Impressions

*Long*

The number of times that your ad was served. On mobile apps an ad is counted as served the first time it's viewed. On all other Facebook interfaces, an ad is served the first time it's placed in a person's News Feed or each time it's placed in the right column.

`inline_link_clicks`

InlineLinkClicks

*Long*

Total number of clicks on links in the ad.

`inline_link_click_ctr`

InlineLinkClicksCounter

*Double*

The click-through rate for inline clicks to link.

`inline_post_engagement`

InlinePostEngagement

*Long*

The total number of engagements on the post.

`instant_experience_clicks_to_open`

InstantExperienceClicksToOpen

*Long*

Corresponds to the instant\_experience\_clicks\_to\_open field from the META API.

`instant_experience_clicks_to_start`

InstantExperienceClicksToStart

*Long*

Corresponds to the instant\_experience\_clicks\_to\_start field from the META API.

`instant_experience_outbound_clicks`

InstantExperienceOutboundClicks

*Long*

Corresponds to the instant\_experience\_outbound\_clicks field from the META API.

`objective`

Objective

*String*

The objective you selected for your campaign. Your objective reflects the goal you want to achieve with your advertising.

`quality_ranking`

QualityRanking

*String*

The quality ranking.

`reach`

Reach

*Long*

The number of people your ad was served to.

`spend`

Spend

*Decimal*

The total amount you've spent so far.

`  `

UniqueClicks

*Long*

The total number of unique people who have clicked on your ad. For example, if 3 people click the same ad 5 times, it counts as 3 unique clicks.

`  `

UniqueCTR

*Double*

The number of people who clicked on your ad divided by the number of people you reached. For example, if you received 20 unique clicks and your ad was served to 1,000 unique people, your unique click-through rate would be 2%.

`inline_link_clicks`

UniqueInlineLinkClicks

*Long*

The number of unique inline link clicks that your ad got. In the Facebook UI, this is the Unique Clicks to Link field.

`  `

UniqueInlineLinkClickCounter

*Double*

The click-through rate for unique inline clicks to link.

`  `

UniqueLinkClicksCounter

*Double*

The unique click-through rate for clicks to link. The number of people who clicked on the link in your ad that directs people off Facebook divided by the number of people you reached. For example, if you received 20 unique clicks to link and your ad was shown to 1,000 unique people, your unique click-through rate would be 2%.

`  `

Checkins

*Int*

The number of checkins attributed to the Ad.

`  `

EventResponses

*Int*

The number of event responses attributed to the Ad.

`inline_link_clicks`

LinkClicks

*Int*

The number of link clicks attributed to the Ad.

`  `

OfferSaves

*Int*

The number of receive offers attributed to the Ad.

`outbound_clicks`

OutboundClicks

*Int*

The number of outbound clicks attributed to the Ad.

`  `

PageEngagements

*Int*

The number of page engagements attributed to the Ad.

`  `

PageLikes

*Int*

The number of page likes attributed to the Ad.

`  `

PageMentions

*Int*

The number of page mentions attributed to the Ad.

`  `

PagePhotoViews

*Int*

The number of photo views attributed to the Ad.

`  `

PostComments

*Int*

The number of post comments attributed to the Ad.

`  `

PostEngagements

*Int*

The number of post engagements attributed to the Ad.

`  `

PostShares

*Int*

The number of post shares attributed to the Ad.

`  `

PostReactions

*Int*

The number of post reactions attributed to the Ad.

`  `

PageTabViews

*Int*

The number of tab views attributed to the Ad.

`  `

Region

*String*

The region someone viewed the Ad from. This is a breakdown field.

`  `

Video3SecondViews

*Int*

The number of video views attributed to the Ad. Views count if at least 3 seconds or the entire video (if the video is less than 3 seconds) were played.

**Generic Breakdowns**

`  `

Age

*String*

The age range for the metrics in this row.

`  `

Gender

*String*

The gender for the metrics in this row.

`  `

Country

*String*

The country for the metrics in this row.

`  `

Region

*String*

The region someone viewed the ad from.

`  `

FrequencyValue

*String*

The number of times an ad in your Reach and Frequency campaign was served to each person.

`  `

HStatsByAdvertiserTZ

*String*

Time period over which the stats were taken for the advertiser.

`  `

HStatsByAudienceTZ

*String*

Time period over which the stats were taken for the audience.

`  `

ImpressionDevice

*String*

The devices used to view the Ad.

`  `

PlatformPosition

*String*

The position on the platform.

`  `

PublisherPlatform

*String*

The platforms the ads were published on.

`  `

ProductId

*String*

The product Id advertised in the Ad.

### `AdInsightsActions` report

`  ACTION_COLLECTION  ` refers to the types of actions people have taken in response to your ad. For a full list of action collections, see [Action collections](https://docs.cloud.google.com/bigquery/docs/facebook-ads-transfer#action_collections) .

**Meta API field name**

**Mapped BigQuery field name**

**Type**

**Description**

`  `

Target

*String*

The Id of the Account to get insights for.

`date_start`

DateStart

*Date*

The starting date to retrieve insights for. In the Facebook UI, this is the Report Start field.

`date_stop`

DateEnd

*Date*

The ending date to retrieve insights for. In the Facebook UI, this is the Report End field.

`  `

TimeIncrement

*String*

The number of days of data aggregation. This value is set at 1.

`  `

Level

*String*

The level to represent the results at. The value is set at `ad` .

`action_attribution_windows`

ActionAttributionWindows

*String*

A comma separated list which determines what is the attribution window for the actions. For example, 28d\_click means the API returns all actions that happened 28 days after someone clicked on the ad. The default option means \[1d\_view,7d\_click\]. Possible values include 1d\_view, 7d\_view, 28d\_view, 1d\_click, 7d\_click, 28d\_click, default.

`  `

ActionCollection

*String*

This comes from your choice of Action Collections in the transfer.

`account_id`

AdAccountId

*String*

The Id of the Ad Account associated with the report row.

`account_name`

AdAccountName

*String*

The name of the Ad Account associated with the report row.

`campaign_id`

CampaignId

*String*

The Id of the Campaign associated with the report row.

`campaign_name`

CampaignName

*String*

The name of the Campaign associated with the report row.

`adset_id`

AdSetId

*String*

The Id of the Ad Set associated with the report row.

`adset_name`

AdSetName

*String*

The name of the Ad Set associated with the report row.

`ad_id`

AdId

*String*

The Id of the Ad associated with the report row.

`ad_name`

AdName

*String*

The name of the Ad associated with the report row.

`  ACTION_COLLECTION .value `

ActionValue

*Integer*

Metric value of default attribution window.  
  
The Facebook Ads plans to update this data type mapping. For more information, see [July 25, 2026](https://docs.cloud.google.com/bigquery/docs/transfer-changes#Jul25-fb-ads) .

`  ACTION_COLLECTION .1d_click `

Action1dClick

*String*

Metric value of attribution window 1 day after clicking the ad.

`  ACTION_COLLECTION .1d_view `

Action1dView

*String*

Metric value of attribution window 1 day after viewing the ad.

`  ACTION_COLLECTION .7d_click `

Action7dClick

*String*

Metric value of attribution window 7 days after clicking the ad.

`  ACTION_COLLECTION .7d_view `

Action7dView

*String*

Metric value of attribution window 7 days after viewing the ad.

`  ACTION_COLLECTION .28d_click `

Action28dClick

*String*

Metric value of attribution window 28 days after clicking the ad.

`  ACTION_COLLECTION .28d_view `

Action28dView

*String*

Metric value of attribution window 28 days after viewing the ad.

`  ACTION_COLLECTION .dda `

ActionDDA

*String*

Metric value of attribution window which is powered by data driven model.

**Generic Breakdowns**

`  `

Age

*String*

The age range for the metrics in this row.

`  `

Gender

*String*

The gender for the metrics in this row.

`  `

Country

*String*

The country for the metrics in this row.

`  `

Region

*String*

The region someone viewed the ad from.

`  `

FrequencyValue

*String*

The number of times an ad in your Reach and Frequency campaign was served to each person.

`  `

HStatsByAdvertiserTZ

*String*

Time period over which the stats were taken for the advertiser.

`  `

HStatsByAudienceTZ

*String*

Time period over which the stats were taken for the audience.

`  `

ImpressionDevice

*String*

The devices used to view the Ad.

`  `

PlatformPosition

*String*

The position on the platform.

`  `

PublisherPlatform

*String*

The platforms the ads were published on.

`  `

ProductId

*String*

The product Id advertised in the Ad.

**Action Breakdowns**

ActionType

*String*

The kind of actions taken on your ad after your ad was served to someone, even if they didn't click it.

ActionCanvasComponentName

*String*

Name of a component within a Canvas ad.

ActionCarouselCardId

*String*

The ID of the specific carousel card that people engaged with when they saw your ad.

ActionCarouselCardName

*String*

The specific carousel card that people engaged with when they saw your ad. The cards are identified by their headlines.

ActionDestination

*String*

The destination where people go after clicking on your ad.

ActionDevice

*String*

The device on which the conversion event you are tracking occurred.

ActionReaction

*String*

The number of reactions on your ads or boosted posts.

ActionTargetId

*String*

The id of destination where people go after clicking on your ad.

ActionVideoSound

*String*

The sound status (on/off) when user watches your video ad.

ActionVideoType

*String*

Video metrics breakdown.

ActionConvertedProductId

*String*

Converted product ids - for Collaborative Ads.

### `AdInsightsMMM` report

| **Meta API field name** | **Mapped BigQuery field name** | **Type**  | **Description**                                   |
| ----------------------- | ------------------------------ | --------- | ------------------------------------------------- |
| `  `                    | Target                         | *String*  | The ID of the Account to get insights for.        |
| `  `                    | TimeIncrement                  | *String*  | The number of days of data aggregation.           |
| `account_id`            | AccountId                      | *String*  | The ID of the Ad Account associated with the row. |
| `campaign_id`           | CampaignId                     | *String*  | The ID of the Campaign associated with the row.   |
| `adset_id`              | AdSetId                        | *String*  | The ID of the Ad Set associated with the row.     |
| `date_start`            | DateStart                      | *Date*    | The starting date for insights retrieval.         |
| `date_stop`             | DateEnd                        | *Date*    | The ending date for insights retrieval.           |
| `impressions`           | Impressions                    | *Long*    | The number of times the ad was served.            |
| `spend`                 | Spend                          | *Decimal* | The total amount spent.                           |
| `country`               | Country                        | *String*  | The country for the metrics.                      |
| `region`                | Region                         | *String*  | The region from which the ad was viewed.          |
| `dma`                   | DMA                            | *String*  | The Designated Market Area for the metrics.       |
| `device_platform`       | DevicePlatform                 | *String*  | The platform of the device used.                  |
| `platform_position`     | PlatformPosition               | *String*  | The position on the platform.                     |
| `publisher_platform`    | PublisherPlatform              | *String*  | The publisher platform.                           |
| `creative_media_type`   | CreativeMediaType              | *String*  | The type of media used in the creative.           |

### `Ads` report

| **Meta API field name**  | **Mapped BigQuery field name** | **Type**   | **Description**                               |
| ------------------------ | ------------------------------ | ---------- | --------------------------------------------- |
| `id`                     | ID                             | *String*   | The ID of the Ad.                             |
| `  `                     | Target                         | *String*   | The target field used to retrieve the ad.     |
| `name`                   | Name                           | *String*   | The name of the Ad.                           |
| `status`                 | AdStatus                       | *String*   | The status of the Ad.                         |
| `bid_info`               | BidInfo                        | *String*   | Bid information associated with the Ad.       |
| `bid_type`               | BidType                        | *String*   | Bid type associated with the Ad.              |
| `campaign_id`            | CampaignId                     | *String*   | The ID of the campaign.                       |
| `adset_id`               | AdSetId                        | *String*   | The ID of the ad set.                         |
| `creative`               | AdCreativeId                   | *String*   | The ID of the ad creative.                    |
| `configured_status`      | ConfiguredStatus               | *String*   | The configured status of the Ad.              |
| `created_time`           | CreatedTime                    | *Datetime* | The creation time of the Ad.                  |
| `updated_time`           | UpdatedTime                    | *Datetime* | The last update time of the Ad.               |
| `conversion_specs`       | ConversionSpecs                | *String*   | Conversion specifications.                    |
| `failed_delivery_checks` | FailedDeliveryChecks           | *String*   | Information regarding failed delivery checks. |
| `recommendations`        | Recommendations                | *String*   | Recommendations for the Ad.                   |
| `tracking_specs`         | TrackingSpecs                  | *JSON*     | Tracking specifications.                      |
| `ad_active_time`         | AdActiveTime                   | *String*   | Active time parameters.                       |
| `ad_schedule_end_time`   | AdScheduleEndTime              | *Datetime* | Scheduled end time.                           |
| `ad_schedule_start_time` | AdScheduleStartTime            | *Datetime* | Scheduled start time.                         |
| `bid_amount`             | BidAmount                      | *Integer*  | The bid amount.                               |
| `last_updated_by_app_id` | LastUpdatedByAppId             | *String*   | App ID that last updated the ad.              |
| `preview_shareable_link` | PreviewShareableLink           | *String*   | Shareable preview link.                       |
| `source_ad_id`           | SourceAdId                     | *String*   | The source Ad ID.                             |

### `AdCreatives` report

| **Meta API field name**           | **Mapped BigQuery field name** | **Type** | **Description**                          |
| --------------------------------- | ------------------------------ | -------- | ---------------------------------------- |
| `id`                              | ID                             | *String* | The ID of the ad creative.               |
| `  `                              | Target                         | *String* | The target field.                        |
| `name`                            | Name                           | *String* | The name of the creative.                |
| `applink_treatment`               | ApplinkTreatment               | *String* | Deep link treatment for the ad creative. |
| `body`                            | Body                           | *String* | The body text of the ad block.           |
| `call_to_action_type`             | CallToActionType               | *String* | Type of call to action.                  |
| `effective_instagram_media_id`    | EffectiveInstagramMediaId      | *String* | Effective ID of the Instagram media.     |
| `image_hash`                      | ImageHash                      | *String* | The hash of the associated image.        |
| `image_url`                       | ImageUrl                       | *String* | The URL to the creative image.           |
| `instagram_permalink_url`         | InstagramPermalinkUrl          | *String* | Permalink URL for Instagram.             |
| `instagram_user_id`               | InstagramUserId                | *String* | Instagram user ID.                       |
| `link_og_id`                      | LinkOgId                       | *String* | Open Graph ID of the link.               |
| `link_url`                        | LinkUrl                        | *String* | The landing page URL.                    |
| `object_id`                       | ObjectId                       | *String* | The associated object ID.                |
| `object_story_id`                 | ObjectStoryId                  | *String* | Object story ID.                         |
| `object_type`                     | ObjectType                     | *String* | The type of the object.                  |
| `object_url`                      | ObjectUrl                      | *String* | URL of the object.                       |
| `page_id`                         | PageId                         | *String* | The associated Facebook Page ID.         |
| `product_set_id`                  | ProductSetId                   | *String* | Product set ID.                          |
| `run_status`                      | RunStatus                      | *String* | The run status of the creative.          |
| `source_instagram_media_id`       | SourceInstagramMediaId         | *String* | Source Instagram media ID.               |
| `template_url`                    | TemplateUrl                    | *String* | Template URL.                            |
| `thumbnail_url`                   | ThumbnailUrl                   | *String* | Thumbnail URL.                           |
| `title`                           | Title                          | *String* | The title text of the ad creative.       |
| `url_tags`                        | UrlTags                        | *String* | URL tags parameters.                     |
| `adlabels`                        | AdLabels                       | *String* | Labels associated with the creative.     |
| `object_story_spec.link_data`     | ObjectStorySpecLinkData        | *JSON*   | Link data specification.                 |
| `object_story_spec.photo_data`    | ObjectStorySpecPhotoData       | *JSON*   | Photo data specification.                |
| `object_story_spec.video_data`    | ObjectStorySpecVideoData       | *JSON*   | Video data specification.                |
| `object_story_spec.text_data`     | ObjectStorySpecTextData        | *JSON*   | Text data specification.                 |
| `object_story_spec.template_data` | ObjectStorySpecTemplateData    | *JSON*   | Template data specification.             |

### `AdSets` report

| **Meta API field name**                   | **Mapped BigQuery field name**      | **Type**   | **Description**                               |
| ----------------------------------------- | ----------------------------------- | ---------- | --------------------------------------------- |
| `id`                                      | ID                                  | *String*   | The ID of the Ad Set.                         |
| `  `                                      | Target                              | *String*   | The target field.                             |
| `name`                                    | Name                                | *String*   | The name of the Ad Set.                       |
| `budget_remaining`                        | BudgetRemaining                     | *Integer*  | The remaining budget.                         |
| `campaign_id`                             | CampaignId                          | *String*   | The associated Campaign ID.                   |
| `status`                                  | AdSetStatus                         | *String*   | The Ad Set status.                            |
| `billing_event`                           | BillingEvent                        | *String*   | Billing event criteria.                       |
| `created_time`                            | CreatedTime                         | *Datetime* | Ad Set creation time.                         |
| `daily_budget`                            | DailyBudget                         | *Integer*  | The daily budget limit.                       |
| `lifetime_budget`                         | LifetimeBudget                      | *Integer*  | The lifetime budget limit.                    |
| `end_time`                                | EndTime                             | *Datetime* | Scheduled end time.                           |
| `start_time`                              | StartTime                           | *Datetime* | Scheduled start time.                         |
| `updated_time`                            | UpdatedTime                         | *Datetime* | Time when the Ad Set was last updated.        |
| `recommendations`                         | Recommendations                     | *String*   | Recommendations for the Ad Set.               |
| `targeting.genders`                       | TargetingGenders                    | *String*   | Targeted genders.                             |
| `targeting.age_max`                       | TargetingAgeMax                     | *Integer*  | Targeted maximum age.                         |
| `targeting.age_min`                       | TargetingAgeMin                     | *Integer*  | Targeted minimum age.                         |
| `targeting.countries`                     | TargetingCountries                  | *String*   | Targeted countries.                           |
| `targeting.location_types`                | TargetingLocationTypes              | *String*   | Targeted location types.                      |
| `targeting.regions`                       | TargetingRegions                    | *String*   | Targeted regions or states.                   |
| `targeting.cities`                        | TargetingCities                     | *String*   | Targeted cities.                              |
| `targeting.zips`                          | TargetingZips                       | *String*   | Targeted zip codes.                           |
| `targeting.custom_locations`              | TargetingCustomLocations            | *String*   | Targeted custom locations.                    |
| `targeting.geo_markets`                   | TargetingGeoMarkets                 | *String*   | Targeted geographic markets.                  |
| `targeting.interests`                     | TargetingInterests                  | *String*   | Targeted personal interests.                  |
| `targeting.behaviors`                     | TargetingBehaviors                  | *String*   | Targeted user behaviors.                      |
| `targeting.device_platforms`              | TargetingDevicePlatforms            | *String*   | Targeted platforms.                           |
| `targeting.publisher_platforms`           | TargetingPublisherPlatforms         | *String*   | Targeted publisher platforms.                 |
| `targeting.instagram_positions`           | TargetingInstagramPositions         | *String*   | Targeted Instagram placement positions.       |
| `targeting.page_types`                    | TargetingPageTypes                  | *String*   | Targeted page types.                          |
| `learning_stage_info.status`              | LearningStageInfoStatus             | *String*   | Status of the learning stage.                 |
| `learning_stage_info.conversions`         | LearningStageInfoConversions        | *Integer*  | Conversions during the learning stage.        |
| `learning_stage_info.attribution_windows` | LearningStageInfoAttributionWindows | *String*   | Attribution windows for learning stage.       |
| `learning_stage_info.last_sig_edit_time`  | LearningStageInfoLastSigEditTime    | *Datetime* | Last significant edit time in learning phase. |

### `Campaigns` report

| **Meta API field name** | **Mapped BigQuery field name** | **Type**   | **Description**                        |
| ----------------------- | ------------------------------ | ---------- | -------------------------------------- |
| `id`                    | ID                             | *String*   | The ID of the Campaign.                |
| `  `                    | Target                         | *String*   | The target field.                      |
| `name`                  | Name                           | *String*   | The name of the Campaign.              |
| `buying_type`           | BuyingType                     | *String*   | The buying type.                       |
| `configured_status`     | ConfiguredStatus               | *String*   | The configured status.                 |
| `effective_status`      | EffectiveStatus                | *String*   | The effective status.                  |
| `status`                | Status                         | *String*   | The current status of the Campaign.    |
| `created_time`          | CreatedTime                    | *Datetime* | Creation time.                         |
| `objective`             | Objective                      | *String*   | The selected campaign objective.       |
| `spend_cap`             | SpendCap                       | *Integer*  | The maximum lifetime spending cap.     |
| `daily_budget`          | DailyBudget                    | *Integer*  | The daily budget.                      |
| `budget_remaining`      | BudgetRemaining                | *Integer*  | The remaining budget for the campaign. |
| `lifetime_budget`       | LifetimeBudget                 | *Integer*  | The total lifetime budget.             |
| `bid_strategy`          | BidStrategy                    | *String*   | The strategy used for bidding.         |
| `start_time`            | StartTime                      | *Datetime* | Scheduled start time.                  |
| `stop_time`             | StopTime                       | *Datetime* | Scheduled stop/end time.               |
| `updated_time`          | UpdatedTime                    | *Datetime* | Last updated time.                     |
| `boosted_object_id`     | BoostedObjectId                | *String*   | The ID of any boosted object.          |

### `AdImages` report

| **Meta API field name** | **Mapped BigQuery field name** | **Type**   | **Description**                      |
| ----------------------- | ------------------------------ | ---------- | ------------------------------------ |
| `id`                    | ID                             | *String*   | The ID of the image.                 |
| `  `                    | Target                         | *String*   | Target field.                        |
| `account_id`            | AccountId                      | *String*   | Ad account ID owning the image.      |
| `created_time`          | CreatedTime                    | *Datetime* | Creation time of the image.          |
| `hash`                  | hash                           | *String*   | Unique hash of the image content.    |
| `height`                | height                         | *Integer*  | Height of the image in pixels.       |
| `width`                 | width                          | *Integer*  | Width of the image in pixels.        |
| `creatives`             | AssociatedWithCreatives        | *String*   | Associated creatives info.           |
| `name`                  | name                           | *String*   | Name identifier for the image.       |
| `original_height`       | OriginalHeight                 | *Integer*  | Original uploaded height.            |
| `original_width`        | OriginalWidth                  | *Integer*  | Original uploaded width.             |
| `status`                | Status                         | *String*   | Validation status of the image.      |
| `permalink_url`         | PermalinkUrl                   | *String*   | URL pointing to the image permalink. |

### `AdLabels` report

| **Meta API field name** | **Mapped BigQuery field name** | **Type**   | **Description**                  |
| ----------------------- | ------------------------------ | ---------- | -------------------------------- |
| `id`                    | ID                             | *String*   | The ID of the ad label.          |
| `  `                    | Target                         | *String*   | Target field.                    |
| `name`                  | Name                           | *String*   | The display name of the label.   |
| `created_time`          | CreatedTime                    | *Datetime* | Time the label was created.      |
| `updated_time`          | UpdatedTime                    | *Datetime* | Time the label was last updated. |

### `Businesses` report

| **Meta API field name** | **Mapped BigQuery field name** | **Type**   | **Description**                            |
| ----------------------- | ------------------------------ | ---------- | ------------------------------------------ |
| `id`                    | ID                             | *String*   | The ID of the business.                    |
| `name`                  | Name                           | *String*   | The name of the business.                  |
| `primary_page`          | PrimaryPage                    | *String*   | Primary page associated with the business. |
| `timezone_id`           | TimezoneId                     | *String*   | Timezone identifier for the business.      |
| `link`                  | Link                           | *String*   | Link to the business profile.              |
| `created_time`          | CreatedTime                    | *Datetime* | Business creation time.                    |
| `updated_time`          | UpdatedTime                    | *Datetime* | Last updated time.                         |

### `CustomAudiences` report

| **Meta API field name**         | **Mapped BigQuery field name** | **Type**   | **Description**                               |
| ------------------------------- | ------------------------------ | ---------- | --------------------------------------------- |
| `id`                            | ID                             | *String*   | The ID of the custom audience.                |
| `  `                            | Target                         | *String*   | The target field.                             |
| `account_id`                    | AccountID                      | *String*   | The ad account ID mapped from Account\_ID.    |
| `name`                          | Name                           | *String*   | The name of the custom audience.              |
| `description`                   | Description                    | *String*   | Description of the audience.                  |
| `subtype`                       | Subtype                        | *String*   | Subtype category of the audience.             |
| `time_created`                  | TimeCreated                    | *Datetime* | Audience creation time.                       |
| `time_updated`                  | TimeUpdated                    | *Datetime* | Audience last updated time.                   |
| `time_content_updated`          | TimeContentUpdated             | *Datetime* | Time when audience content was last modified. |
| `rule`                          | Rule                           | *String*   | Rules used to govern audience membership.     |
| `rule_aggregation`              | RuleAggregation                | *String*   | Aggregation setting for audience rules.       |
| `approximate_count_lower_bound` | ApproximateCountLowerBound     | *Integer*  | Lower bound approximation for audience size.  |
| `approximate_count_upper_bound` | ApproximateCountUpperBound     | *Integer*  | Upper bound approximation for audience size.  |
| `pixel_id`                      | PixelID                        | *String*   | Associated pixel ID.                          |
| `retention_days`                | RetentionDays                  | *Integer*  | Number of days members are retained.          |
| `customer_file_source`          | CustomerFileSource             | *String*   | The original source of the customer file.     |
| `data_source`                   | DataSource                     | *JSON*     | Primary data source.                          |
| `delivery_status`               | DeliveryStatus                 | *JSON*     | Current delivery status.                      |
| `operation_status`              | OperationStatus                | *JSON*     | Status of recent operations.                  |
| `permission_for_actions`        | PermissionForActions           | *JSON*     | Permissions for actions.                      |
| `is_value_based`                | IsValueBased                   | *Boolean*  | Flag indicating if audience is value based.   |
| `opt_out_link`                  | OptOutLink                     | *String*   | Opt out link.                                 |
