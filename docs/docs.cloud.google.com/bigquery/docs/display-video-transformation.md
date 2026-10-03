---
name: documents/docs.cloud.google.com/bigquery/docs/display-video-transformation
uri: https://docs.cloud.google.com/bigquery/docs/display-video-transformation
title: Display & Video 360 data transformation
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# Display & Video 360 data transformation

When your Display & Video 360 data are transferred to BigQuery, they are transformed into the following BigQuery tables and views.

When you view the tables and views in BigQuery, the value for ` displayvideo_id ` is your Display & Video 360 partner or advertiser ID.

| **Display & Video 360 resource**                                                                                                                                                         | **BigQuery table**                              | **BigQuery view**                             |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------|-----------------------------------------------|
| **Data Transfer files**                                                                                                                                                                  |                                                 |                                               |
| [Impression](https://developers.google.com/bid-manager/dtv2/reference/file-format)                                                                                                       | p_Impression\_ ` displayvideo_id `              | Impression\_ ` displayvideo_id `              |
| [Click](https://developers.google.com/bid-manager/dtv2/reference/file-format)                                                                                                            | p_Click\_ ` displayvideo_id `                   | Click\_ ` displayvideo_id `                   |
| [Activity](https://developers.google.com/bid-manager/dtv2/reference/file-format)                                                                                                         | p_Activity\_ ` displayvideo_id `                | Activity\_ ` displayvideo_id `                |
| **DV360 API Resource (v3)**                                                                                                                                                              |                                                 |                                               |
| [Partner](https://developers.google.com/display-video/api/reference/rest/v3/partners#resource:-partner)                                                                                  | p_Partner\_ ` displayvideo_id `                 | Partner\_ ` displayvideo_id `                 |
| [Advertiser](https://developers.google.com/display-video/api/reference/rest/v3/advertisers#resource:-advertiser)                                                                         | p_Advertiser\_ ` displayvideo_id `              | Advertiser\_ ` displayvideo_id `              |
| [LineItem](https://developers.google.com/display-video/api/reference/rest/v3/advertisers.lineItems#LineItem)                                                                             | p_LineItem\_ ` displayvideo_id `                | LineItem\_ ` displayvideo_id `                |
| [LineItemTargeting](https://developers.google.com/display-video/api/reference/rest/v3/advertisers.lineItems/bulkListAssignedTargetingOptions#LineItemAssignedTargetingOption)            | p_LineItemTargeting\_ ` displayvideo_id `       | LineItemTargeting\_ ` displayvideo_id `       |
| [Campaign](https://developers.google.com/display-video/api/reference/rest/v3/advertisers.campaigns#Campaign)                                                                             | p_Campaign\_ ` displayvideo_id `                | Campaign\_ ` displayvideo_id `                |
| [CampaignTargeting](https://developers.google.com/display-video/api/reference/rest/v3/advertisers.campaigns.targetingTypes.assignedTargetingOptions#AssignedTargetingOption)             | p_CampaignTargeting\_ ` displayvideo_id `       | CampaignTargeting\_ ` displayvideo_id `       |
| [InsertionOrder](https://developers.google.com/display-video/api/reference/rest/v3/advertisers.insertionOrders#InsertionOrder)                                                           | p_InsertionOrder\_ ` displayvideo_id `          | InsertionOrder\_ ` displayvideo_id `          |
| [InsertionOrderTargeting](https://developers.google.com/display-video/api/reference/rest/v3/advertisers.insertionOrders.targetingTypes.assignedTargetingOptions#AssignedTargetingOption) | p_InsertionOrderTargeting\_ ` displayvideo_id ` | InsertionOrderTargeting\_ ` displayvideo_id ` |
| [AdGroup](https://developers.google.com/display-video/api/reference/rest/v3/advertisers.adGroups#AdGroup)                                                                                | p_AdGroup\_ ` displayvideo_id `                 | AdGroup\_ ` displayvideo_id `                 |
| [AdGroupTargeting](https://developers.google.com/display-video/api/reference/rest/v3/advertisers.adGroups/bulkListAdGroupAssignedTargetingOptions#AdGroupAssignedTargetingOption)        | p_AdGroupTargeting\_ ` displayvideo_id `        | AdGroupTargeting\_ ` displayvideo_id `        |
| [AdGroupAd](https://developers.google.com/display-video/api/reference/rest/v3/advertisers.adGroupAds#AdGroupAd)                                                                          | p_AdGroupAd\_ ` displayvideo_id `               | AdGroupAd\_ ` displayvideo_id `               |
| [Creative](https://developers.google.com/display-video/api/reference/rest/v3/advertisers.creatives#resource:-creative)                                                                   | p_Creative\_ ` displayvideo_id `                | Creative\_ ` displayvideo_id `                |
