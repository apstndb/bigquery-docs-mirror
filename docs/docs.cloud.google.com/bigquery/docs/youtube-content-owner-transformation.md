---
name: documents/docs.cloud.google.com/bigquery/docs/youtube-content-owner-transformation
uri: https://docs.cloud.google.com/bigquery/docs/youtube-content-owner-transformation
title: YouTube Content Owner report transformation
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# YouTube Content Owner report transformation

When your YouTube Content Owner or system-managed reports are transferred to BigQuery, the reports are transformed into the following BigQuery tables and views.

When you view the tables and views in BigQuery, the value for suffix is the table suffix you configured when you created the transfer.

## YouTube Content Owner reports

The following sections describe transformations for YouTube Content Owner reports.

### Video reports

The following reports focus on video-level user activity, playback locations, traffic sources, and demographics.

#### User activity

YouTube report: [User activity](https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#video-user-activity)

  - BigQuery table:  
    p\_content\_owner\_basic\_a4\_ suffix
  - BigQuery view:  
    content\_owner\_basic\_a4\_ suffix

#### User activity by province

YouTube report: [User activity by province](https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#video-province)

  - BigQuery table:  
    p\_content\_owner\_province\_a3\_ suffix
  - BigQuery view:  
    content\_owner\_province\_3\_ suffix

#### Playback locations

YouTube report: [Playback locations](https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#video-playback-locations)

  - BigQuery table:  
    p\_content\_owner\_playback\_location\_a3\_ suffix
  - BigQuery view:  
    content\_owner\_playback\_location\_a3\_ suffix

#### Traffic sources

YouTube report: [Traffic sources](https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#video-traffic-sources)

  - BigQuery table:  
    p\_content\_owner\_traffic\_source\_a3\_ suffix
  - BigQuery view:  
    content\_owner\_traffic\_source\_a3\_ suffix

#### Device type and operating system

YouTube report: [Device type and operating system](https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#video-device-type-and-operating-system)

  - BigQuery table:  
    p\_content\_owner\_device\_os\_a3\_ suffix
  - BigQuery view:  
    content\_owner\_device\_os\_a3\_ suffix

#### Viewer demographics

YouTube report: [Viewer demographics](https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#video-viewer-demographics)

  - BigQuery table:  
    p\_content\_owner\_demographics\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_demographics\_a1\_ suffix

#### Content sharing by platform

YouTube report: [Content sharing by platform](https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#video-content-sharing)

  - BigQuery table:  
    p\_content\_owner\_sharing\_service\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_sharing\_service\_a1\_ suffix

#### Annotations

YouTube report: [Annotations](https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#video-annotations)

  - BigQuery table:  
    p\_content\_owner\_annotations\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_annotations\_a1\_ suffix

#### Cards

YouTube report: [Cards](https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#video-cards)

  - BigQuery table:  
    p\_content\_owner\_cards\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_cards\_a1\_ suffix

#### End screens

YouTube report: [End screens](https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#video-end-screens)

  - BigQuery table:  
    p\_content\_owner\_end\_screens\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_end\_screens\_a1\_ suffix

#### Subtitles

YouTube report: [Subtitles](https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#video-subtitles)

  - BigQuery table:  
    p\_content\_owner\_subtitles\_a3\_ suffix
  - BigQuery view:  
    content\_owner\_subtitles\_a3\_ suffix

#### Combined

YouTube report: [Combined](https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#video-combined)

  - BigQuery table:  
    p\_content\_owner\_combined\_a3\_ suffix
  - BigQuery view:  
    content\_owner\_combined\_a3\_ suffix

### Playlist reports

The following reports contain performance metrics and user activity for playlists.

#### User activity

YouTube report: [User activity](https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#playlist-user-activity)

  - BigQuery table:  
    p\_content\_owner\_playlist\_basic\_a2\_ suffix
  - BigQuery view:  
    content\_owner\_playlist\_basic\_a2\_ suffix

#### User activity by province

YouTube report: [User activity by province](https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#playlist-province)

  - BigQuery table:  
    p\_content\_owner\_playlist\_province\_a2\_ suffix
  - BigQuery view:  
    content\_owner\_playlist\_province\_a2\_ suffix

#### Playback locations

YouTube report: [Playback locations](https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#playlist-playback-locations)

  - BigQuery table:  
    p\_content\_owner\_playlist\_playback\_location\_a2\_ suffix
  - BigQuery view:  
    content\_owner\_playlist\_playback\_location\_a2

#### Traffic sources

YouTube report: [Traffic sources](https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#playlist-traffic-sources)

  - BigQuery table:  
    p\_content\_owner\_playlist\_traffic\_source\_a2
  - BigQuery view:  
    content\_owner\_playlist\_traffic\_source\_a2\_ suffix

#### Device type and operating system

YouTube report: [Device type and operating system](https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#playlist-device-type-and-operating-system)

  - BigQuery table:  
    p\_content\_owner\_playlist\_device\_os\_a2\_ suffix
  - BigQuery view:  
    content\_owner\_playlist\_device\_os\_a2\_ suffix

#### Combined

YouTube report: [Combined](https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#playlist-combined)

  - BigQuery table:  
    p\_content\_owner\_playlist\_combined\_a2\_ suffix
  - BigQuery view:  
    content\_owner\_playlist\_combined\_a2\_ suffix

### Ad rate reports

The following reports display key ad metrics and transaction rates.

#### Ad rate reports

YouTube report: [Ad rate reports](https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#ad-rate-reports)

  - BigQuery table:  
    p\_content\_owner\_ad\_rates\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_ad\_rates\_a1\_ suffix

### Estimated revenue reports

The following reports estimate revenue generated at the video and asset levels.

#### Estimated video revenue

YouTube report: [Estimated video revenue](https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#estimated-revenue-videos)

  - BigQuery table:  
    p\_content\_owner\_estimated\_revenue\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_estimated\_revenue\_a1\_ suffix

#### Estimated asset revenue

YouTube report: [Estimated asset revenue](https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#estimated-revenue-assets)

  - BigQuery table:  
    p\_content\_owner\_asset\_estimated\_revenue\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_asset\_estimated\_revenue\_a1\_ suffix

### Asset reports

The following reports focus on asset performance, user engagement, and metadata.

#### User activity

YouTube report: [User activity](https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#asset-user-activity)

  - BigQuery table:  
    p\_content\_owner\_asset\_basic\_a3\_ suffix
  - BigQuery view:  
    content\_owner\_asset\_basic\_a3\_ suffix

#### User activity by province

YouTube report: [User activity by province](https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#asset-province)

  - BigQuery table:  
    p\_content\_owner\_asset\_province\_a3\_ suffix
  - BigQuery view:  
    content\_owner\_asset\_province\_a3\_ suffix

#### Video playback locations

YouTube report: [Video playback locations](https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#asset-playback-locations)

  - BigQuery table:  
    p\_content\_owner\_asset\_playback\_location\_a3\_ suffix
  - BigQuery view:  
    content\_owner\_asset\_playback\_location\_a3\_ suffix

#### Traffic sources

YouTube report: [Traffic sources](https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#asset-traffic-sources)

  - BigQuery table:  
    p\_content\_owner\_asset\_traffic\_source\_a3\_ suffix
  - BigQuery view:  
    content\_owner\_asset\_traffic\_source\_a3\_ suffix

#### Device type and operating system

YouTube report: [Device type and operating system](https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#asset-device-type-and-operating-system)

  - BigQuery table:  
    p\_content\_owner\_asset\_device\_os\_a3\_ suffix
  - BigQuery view:  
    content\_owner\_asset\_device\_os\_a3\_ suffix

#### Viewer demographics

YouTube report: [Viewer demographics](https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#asset-viewer-demographics)

  - BigQuery table:  
    p\_content\_owner\_asset\_demographics\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_asset\_demographics\_a1\_ suffix

#### Content sharing by platform

YouTube report: [Content sharing by platform](https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#asset-content-sharing)

  - BigQuery table:  
    p\_content\_owner\_asset\_sharing\_service\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_asset\_sharing\_service\_a1\_ suffix

#### Annotations

YouTube report: [Annotations](https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#asset-annotations)

  - BigQuery table:  
    p\_content\_owner\_asset\_annotations\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_asset\_annotations\_a1\_ suffix

#### Cards

YouTube report: [Cards](https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#asset-cards)

  - BigQuery table:  
    p\_content\_owner\_asset\_cards\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_asset\_cards\_a1\_ suffix

#### End screens

YouTube report: [End screens](https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#asset-end-screens)

  - BigQuery table:  
    p\_content\_owner\_asset\_end\_screens\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_asset\_end\_screens\_a1\_ suffix

#### Combined

YouTube report: [Combined](https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#asset-combined)

  - BigQuery table:  
    p\_content\_owner\_asset\_combined\_a3\_ suffix
  - BigQuery view:  
    content\_owner\_asset\_combined\_a3\_ suffix

### Reach reports

The following reports cover audience reach metrics for your channel content.

#### Reach basic

YouTube report: [Reach basic](https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#reach-reports)

  - BigQuery table:  
    p\_content\_owner\_reach\_basic\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_reach\_basic\_a1\_ suffix

#### Reach combined

YouTube report: [Reach combined](https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#reach-reports)

  - BigQuery table:  
    p\_content\_owner\_reach\_combined\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_reach\_combined\_a1\_ suffix

## YouTube system-managed reports

The following sections describe transformations for reports managed by the YouTube system.

### Financial summary reports

The following reports summarize payments and billing data for your network.

#### Monthly payments summary

YouTube report: [Monthly payments summary](https://developers.google.com/youtube/reporting/v1/reports/system_managed/financial-summaries#monthly-payments-summary)

  - BigQuery table:  
    p\_content\_owner\_payments\_summary\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_payments\_summary\_a1\_ suffix

### Ad revenue reports

The following reports provide summaries of advertising revenue across different dimensions like country, video, and asset.

#### Monthly global ad revenue summary

YouTube report: [Monthly global ad revenue summary](https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#monthly-global-ad-revenue-summary)

  - BigQuery table:  
    p\_content\_owner\_global\_ad\_revenue\_summary\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_global\_ad\_revenue\_summary\_a1\_ suffix

#### Monthly country ad revenue summary

YouTube report: [Monthly country ad revenue summary](https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#monthly-country-ad-revenue-summary)

  - BigQuery table:  
    p\_content\_owner\_country\_ad\_revenue\_summary\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_country\_ad\_revenue\_summary\_a1\_ suffix

#### Monthly day ad revenue summary

YouTube report: [Monthly day ad revenue summary](https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#monthly-day-ad-revenue-summary)

  - BigQuery table:  
    p\_content\_owner\_day\_ad\_revenue\_summary\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_day\_ad\_revenue\_summary\_a1\_ suffix

#### Weekly global ad revenue summary

YouTube report: [Weekly global ad revenue summary](https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#weekly-global-ad-revenue-summary)

  - BigQuery table:  
    p\_content\_owner\_global\_ad\_revenue\_summary\_weekly\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_global\_ad\_revenue\_summary\_weekly\_a1\_ suffix

#### Weekly country ad revenue summary

YouTube report: [Weekly country ad revenue summary](https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#weekly-country-ad-revenue-summary)

  - BigQuery table:  
    p\_content\_owner\_country\_ad\_revenue\_summary\_weekly\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_country\_ad\_revenue\_summary\_weekly\_a1\_ suffix

#### Weekly day ad revenue summary

YouTube report: [Weekly day ad revenue summary](https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#weekly-day-ad-revenue-summary)

  - BigQuery table:  
    p\_content\_owner\_day\_ad\_revenue\_summary\_weekly\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_day\_ad\_revenue\_summary\_weekly\_a1\_ suffix

#### Aggregate ad revenue per video

YouTube report: [Aggregate ad revenue per video](https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#aggregate-ad-revenue-per-video)

  - BigQuery table:  
    p\_content\_owner\_ad\_revenue\_summary\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_ad\_revenue\_summary\_a1\_ suffix

#### Weekly video ad revenue summary

YouTube report: [Weekly video ad revenue summary](https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#weekly-video-ad-revenue-summary)

  - BigQuery table:  
    p\_content\_owner\_ad\_revenue\_summary\_weekly\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_ad\_revenue\_summary\_weekly\_a1\_ suffix

#### Weekly video ad revenue

YouTube report: [Weekly video ad revenue](https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#weekly-video-ad-revenue)

  - BigQuery table:  
    p\_content\_owner\_ad\_revenue\_raw\_weekly\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_ad\_revenue\_raw\_weekly\_a1\_ suffix

#### Daily ad revenue per video

YouTube report: [Daily ad revenue per video](https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#daily-ad-revenue-per-video)

  - BigQuery table:  
    p\_content\_owner\_ad\_revenue\_raw\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_ad\_revenue\_raw\_a1\_ suffix

#### Aggregate ad revenue per asset

YouTube report: [Aggregate ad revenue per asset](https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#aggregate-ad-revenue-per-asset)

  - BigQuery table:  
    p\_content\_owner\_asset\_ad\_revenue\_summary\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_asset\_ad\_revenue\_summary\_a1\_ suffix

#### Daily ad revenue per asset

YouTube report: [Daily ad revenue per asset](https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#daily-ad-revenue-per-asset)

  - BigQuery table:  
    p\_content\_owner\_asset\_ad\_revenue\_raw\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_asset\_ad\_revenue\_raw\_a1\_ suffix

#### Monthly claim ad revenue summary

YouTube report: [Monthly claim ad revenue summary](https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#monthly-claim-ad-revenue-summary)

  - BigQuery table:  
    p\_content\_owner\_claim\_ad\_revenue\_summary\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_claim\_ad\_revenue\_summary\_a1\_ suffix

#### Weekly claim ad revenue summary

YouTube report: [Weekly claim ad revenue summary](https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#weekly-claim-ad-revenue-summary)

  - BigQuery table:  
    p\_content\_owner\_claim\_ad\_revenue\_summary\_weekly\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_claim\_ad\_revenue\_summary\_weekly\_a1\_ suffix

#### Monthly claim ad revenue

YouTube report: [Monthly claim ad revenue](https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#monthly-claim-ad-revenue)

  - BigQuery table:  
    p\_content\_owner\_claim\_ad\_revenue\_raw\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_claim\_ad\_revenue\_raw\_a1\_ suffix

#### Weekly claim ad revenue

YouTube report: [Weekly claim ad revenue](https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#weekly-claim-ad-revenue)

  - BigQuery table:  
    p\_content\_owner\_claim\_ad\_revenue\_raw\_weekly\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_claim\_ad\_revenue\_raw\_weekly\_a1\_ suffix

#### Monthly global ad adjustment revenue summary

YouTube report: [Monthly global ad adjustment revenue summary](https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#monthly-global-ad-adjustment-revenue-summary)

  - BigQuery table:  
    p\_content\_owner\_global\_ad\_adjustment\_revenue\_summary\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_global\_ad\_adjustment\_revenue\_summary\_a1\_ suffix

#### Monthly asset ad adjustment revenue summary

YouTube report: [Monthly asset ad adjustment revenue summary](https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#monthly-asset-ad-adjustment-revenue-summary)

  - BigQuery table:  
    p\_content\_owner\_asset\_ad\_adjustment\_revenue\_summary\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_asset\_ad\_adjustment\_revenue\_summary\_a1\_ suffix

#### Monthly asset ad adjustment revenue

YouTube report: [Monthly asset ad adjustment revenue](https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#monthly-asset-ad-adjustment-revenue)

  - BigQuery table:  
    p\_content\_owner\_asset\_ad\_adjustment\_revenue\_raw\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_asset\_ad\_adjustment\_revenue\_raw\_a1\_ suffix

#### Monthly video ad adjustment revenue summary

YouTube report: [Monthly video ad adjustment revenue summary](https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#monthly-video-ad-adjustment-revenue-summary)

  - BigQuery table:  
    p\_content\_owner\_ad\_adjustment\_revenue\_summary\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_ad\_adjustment\_revenue\_summary\_a1\_ suffix

#### Monthly video ad adjustment revenue raw

YouTube report: [Monthly video ad adjustment revenue raw](https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#monthly-video-ad-adjustment-revenue-raw)

  - BigQuery table:  
    p\_content\_owner\_ad\_adjustment\_revenue\_raw\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_ad\_adjustment\_revenue\_raw\_a1\_ suffix

#### Monthly claim ad adjustment revenue summary

YouTube report: [Monthly claim ad adjustment revenue summary](https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#monthly-claim-ad-adjustment-revenue-summary)

  - BigQuery table:  
    p\_content\_owner\_claim\_ad\_adjustment\_revenue\_summary\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_claim\_ad\_adjustment\_revenue\_summary\_a1\_ suffix

#### Monthly claim ad adjustment revenue

YouTube report: [Monthly claim ad adjustment revenue](https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#monthly-claim-ad-adjustment-revenue)

  - BigQuery table:  
    p\_content\_owner\_claim\_ad\_adjustment\_revenue\_raw\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_claim\_ad\_adjustment\_revenue\_raw\_a1\_ suffix

#### Monthly country ad adjustment revenue summary

YouTube report: [Monthly country ad adjustment revenue summary](https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#monthly-country-ad-adjustment-revenue-summary)

  - BigQuery table:  
    p\_content\_owner\_country\_ad\_adjustment\_revenue\_summary\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_country\_ad\_adjustment\_revenue\_summary\_a1\_ suffix

#### Monthly day ad adjustment revenue summary

YouTube report: [Monthly day ad adjustment revenue summary](https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#monthly-day-ad-adjustment-revenue-summary)

  - BigQuery table:  
    p\_content\_owner\_day\_ad\_adjustment\_revenue\_summary\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_day\_ad\_adjustment\_revenue\_summary\_a1\_ suffix

### Subscription revenue reports

The following reports summarize music and non-music subscription revenue across videos and assets.

#### Monthly music revenue summary

YouTube report: [Monthly music revenue summary](https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-music-revenue-summary)

  - BigQuery table:  
    p\_content\_owner\_country\_music\_red\_revenue\_summary\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_country\_music\_red\_revenue\_summary\_a1\_ suffix

#### Monthly music label video revenue

YouTube report: [Monthly music label video revenue](https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-music-label-video-revenue)

  - BigQuery table:  
    p\_music\_content\_owner\_red\_revenue\_raw\_a1\_ suffix
  - BigQuery view:  
    music\_content\_owner\_red\_revenue\_raw\_a1\_ suffix

#### Monthly music label assets revenue

YouTube report: [Monthly music label assets revenue](https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-music-label-assets-revenue)

  - BigQuery table:  
    p\_music\_content\_owner\_asset\_red\_revenue\_raw\_a1\_ suffix
  - BigQuery view:  
    music\_content\_owner\_asset\_red\_revenue\_raw\_a1\_ suffix

#### Monthly music label subscriber revenue summary

YouTube report: [Monthly music label subscriber revenue summary](https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-music-label-subscriber-revenue-summary)

  - BigQuery table:  
    p\_music\_content\_owner\_subscriber\_red\_revenue\_summary\_a1\_ suffix
  - BigQuery view:  
    music\_content\_owner\_subscriber\_red\_revenue\_summary\_a1\_ suffix

#### Monthly music publisher revenue summary

YouTube report: [Monthly music publisher revenue summary](https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-music-publisher-revenue-summary)

  - BigQuery table:  
    p\_publisher\_content\_owner\_music\_red\_revenue\_summary\_a1\_ suffix
  - BigQuery view:  
    publisher\_content\_owner\_music\_red\_revenue\_summary\_a1\_ suffix

#### Monthly music publisher subscription revenue summary

YouTube report: [Monthly music publisher subscription revenue summary](https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-music-publisher-subscription-revenue-summary)

  - BigQuery table:  
    p\_publisher\_content\_owner\_subscriber\_red\_revenue\_summary\_a1\_ suffix
  - BigQuery view:  
    publisher\_content\_owner\_subscriber\_red\_revenue\_summary\_a1\_ suffix

#### Monthly music publisher non-music subscription revenue summary

YouTube report: [Monthly music publisher non-music subscription revenue summary](https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-music-publisher-non-music-subscription-revenue-summary)

  - BigQuery table:  
    p\_publisher\_content\_owner\_non\_music\_red\_revenue\_summary\_a1\_ suffix
  - BigQuery view:  
    publisher\_content\_owner\_non\_music\_red\_revenue\_summary\_a1\_ suffix

#### Monthly music label music revenue summary

YouTube report: [Monthly music label music revenue summary](https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-music-label-music-revenue-summary)

  - BigQuery table:  
    p\_music\_content\_owner\_country\_music\_red\_revenue\_summary\_a1\_ suffix
  - BigQuery view:  
    music\_content\_owner\_country\_music\_red\_revenue\_summary\_a1\_ suffix

#### Monthly subscriptions music video revenue

YouTube report: [Monthly subscriptions music video revenue](https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-subscriptions-music-video-revenue)

  - BigQuery table:  
    p\_content\_owner\_music\_red\_revenue\_raw\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_music\_red\_revenue\_raw\_a1\_ suffix

#### Monthly subscriptions music assets revenue

YouTube report: [Monthly subscriptions music assets revenue](https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-subscriptions-music-assets-revenue)

  - BigQuery table:  
    p\_content\_owner\_music\_asset\_red\_revenue\_raw\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_music\_asset\_red\_revenue\_raw\_a1\_ suffix

#### Weekly music revenue summary

YouTube report: [Weekly music revenue summary](https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#weekly-music-revenue-summary)

  - BigQuery table:  
    p\_music\_content\_owner\_country\_music\_red\_revenue\_summary\_weekly\_a1\_ suffix
  - BigQuery view:  
    music\_content\_owner\_country\_music\_red\_revenue\_summary\_weekly\_a1\_ suffix

#### Weekly music label videos revenue

YouTube report: [Weekly music label videos revenue](https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#weekly-music-label-videos-revenue)

  - BigQuery table:  
    p\_music\_content\_owner\_red\_revenue\_raw\_weekly\_a1\_ suffix
  - BigQuery view:  
    music\_content\_owner\_red\_revenue\_raw\_weekly\_a1\_ suffix

#### Weekly music label assets revenue

YouTube report: [Weekly music label assets revenue](https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#weekly-music-label-assets-revenue)

  - BigQuery table:  
    p\_music\_content\_owner\_asset\_red\_revenue\_raw\_weekly\_a1\_ suffix
  - BigQuery view:  
    music\_content\_owner\_asset\_red\_revenue\_raw\_weekly\_a1\_ suffix

#### Monthly non-music summary

YouTube report: [Monthly non-music summary](https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-non-music-summary)

  - BigQuery table:  
    p\_content\_owner\_country\_non\_music\_red\_revenue\_summary\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_country\_non\_music\_red\_revenue\_summary\_a1\_ suffix

#### Monthly music label non-music revenue summary

YouTube report: [Monthly music label non-music revenue summary](https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-music-label-non-music-revenue-summary)

  - BigQuery table:  
    p\_music\_content\_owner\_country\_non\_music\_red\_revenue\_summary\_a1\_ suffix
  - BigQuery view:  
    music\_content\_owner\_country\_non\_music\_red\_revenue\_summary\_a1\_ suffix

#### Monthly subscriptions non-music videos revenue

YouTube report: [Monthly subscriptions non-music videos revenue](https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-subscriptions-non-music-videos-revenue)

  - BigQuery table:  
    p\_content\_owner\_non\_music\_red\_revenue\_raw\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_non\_music\_red\_revenue\_raw\_a1\_ suffix

#### Monthly subscriptions non-music assets revenue

YouTube report: [Monthly subscriptions non-music assets revenue](https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-subscriptions-non-music-assets-revenue)

  - BigQuery table:  
    p\_content\_owner\_non\_music\_asset\_red\_revenue\_raw\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_non\_music\_asset\_red\_revenue\_raw\_a1\_ suffix

#### Weekly non-music revenue summary

YouTube report: [Weekly non-music revenue summary](https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#weekly-non-music-revenue-summary)

  - BigQuery table:  
    p\_music\_content\_owner\_country\_non\_music\_red\_revenue\_summary\_weekly\_a1\_ suffix
  - BigQuery view:  
    music\_content\_owner\_country\_non\_music\_red\_revenue\_summary\_weekly\_a1\_ suffix

#### Monthly music label asset subscription adjustment revenue raw

YouTube report: [Monthly music label asset subscription adjustment revenue raw](https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-music-label-asset-subscription-adjustment-revenue-raw)

  - BigQuery table:  
    p\_music\_content\_owner\_asset\_red\_adjustment\_revenue\_raw\_a1\_ suffix
  - BigQuery view:  
    music\_content\_owner\_asset\_red\_adjustment\_revenue\_raw\_a1\_ suffix

#### Monthly subscriptions adjustment music video raw

YouTube report: [Monthly subscriptions adjustment music video raw](https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-subscriptions-adjustment-music-video-raw)

  - BigQuery table:  
    p\_music\_content\_owner\_red\_adjustment\_revenue\_raw\_a1\_ suffix
  - BigQuery view:  
    music\_content\_owner\_red\_adjustment\_revenue\_raw\_a1\_ suffix

#### Monthly music label country music subscription adjustment revenue summary

YouTube report: [Monthly music label country music subscription adjustment revenue summary](https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-music-label-country-music-subscription-adjustment-revenue-summary)

  - BigQuery table:  
    p\_music\_content\_owner\_country\_music\_red\_adjustment\_revenue\_summary\_a1\_ suffix
  - BigQuery view:  
    music\_content\_owner\_country\_music\_red\_adjustment\_revenue\_summary\_a1\_ suffix

#### Monthly music label country non-music subscription adjustment revenue summary

YouTube report: [Monthly music label country non-music subscription adjustment revenue summary](https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-music-label-country-non-music-subscription-adjustment-revenue-summary)

  - BigQuery table:  
    p\_music\_content\_owner\_country\_non\_music\_red\_adjustment\_revenue\_summary\_a1\_ suffix
  - BigQuery view:  
    music\_content\_owner\_country\_non\_music\_red\_adjustment\_revenue\_summary\_a1\_ suffix

#### Monthly non-music asset subscription adjustment revenue raw

YouTube report: [Monthly non-music asset subscription adjustment revenue raw](https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-non-music-asset-subscription-adjustment-revenue-raw)

  - BigQuery table:  
    p\_content\_owner\_non\_music\_asset\_red\_adjustment\_revenue\_raw\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_non\_music\_asset\_red\_adjustment\_revenue\_raw\_a1\_ suffix

#### Monthly non-music subscription adjustment revenue raw

YouTube report: [Monthly non-music subscription adjustment revenue raw](https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-non-music-subscription-adjustment-revenue-raw)

  - BigQuery table:  
    p\_content\_owner\_non\_music\_red\_adjustment\_revenue\_raw\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_non\_music\_red\_adjustment\_revenue\_raw\_a1\_ suffix

#### Monthly music video subscription adjustment revenue raw

YouTube report: [Monthly music video subscription adjustment revenue raw](https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-music-video-subscription-adjustment-revenue-raw)

  - BigQuery table:  
    p\_content\_owner\_music\_video\_red\_adjustment\_revenue\_raw\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_music\_video\_red\_adjustment\_revenue\_raw\_a1\_ suffix

#### Monthly music asset subscription adjustment revenue raw

YouTube report: [Monthly music asset subscription adjustment revenue raw](https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-music-asset-subscription-adjustment-revenue-raw)

  - BigQuery table:  
    p\_content\_owner\_music\_asset\_red\_adjustment\_revenue\_raw\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_music\_asset\_red\_adjustment\_revenue\_raw\_a1\_ suffix

#### Monthly music publisher asset subscription adjustment revenue raw

YouTube report: [Monthly music publisher asset subscription adjustment revenue raw](https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-music-publisher-asset-subscription-adjustment-revenue-raw)

  - BigQuery table:  
    p\_publisher\_content\_owner\_asset\_red\_adjustment\_revenue\_raw\_a1\_ suffix
  - BigQuery view:  
    publisher\_content\_owner\_asset\_red\_adjustment\_revenue\_raw\_a1\_ suffix

#### Monthly music publisher country non-music subscription adjustment revenue summary

YouTube report: [Monthly music publisher country non-music subscription adjustment revenue summary](https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-music-publisher-country-non-music-subscription-adjustment-revenue-summary)

  - BigQuery table:  
    p\_publisher\_content\_owner\_country\_non\_music\_red\_adjustment\_revenue\_summary\_a1\_ suffix
  - BigQuery view:  
    publisher\_content\_owner\_country\_non\_music\_red\_adjustment\_revenue\_summary\_a1\_ suffix

#### Monthly music publisher country music subscription adjustment revenue summary

YouTube report: [Monthly music publisher country music subscription adjustment revenue summary](https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-music-publisher-country-music-subscription-adjustment-revenue-summary)

  - BigQuery table:  
    p\_publisher\_content\_owner\_country\_music\_red\_adjustment\_revenue\_summary\_a1\_ suffix
  - BigQuery view:  
    publisher\_content\_owner\_country\_music\_red\_adjustment\_revenue\_summary\_a1\_ suffix

### YouTube Shorts revenue reports

The following reports summarize revenue and engagement metrics for YouTube Shorts.

#### Monthly YouTube Shorts music label content owner revenue summary

YouTube report: [Monthly YouTube Shorts music label content owner revenue summary](https://developers.google.com/youtube/reporting/v1/reports/system_managed/shorts#monthly-youtube-shorts-music-label-content-owner-revenue-summary)

  - BigQuery table:  
    p\_music\_content\_owner\_shorts\_revenue\_summary\_a1\_ suffix
  - BigQuery view:  
    music\_content\_owner\_shorts\_revenue\_summary\_a1\_ suffix

#### Monthly YouTube Shorts music publisher content owner revenue summary

YouTube report: [Monthly YouTube Shorts music publisher content owner revenue summary](https://developers.google.com/youtube/reporting/v1/reports/system_managed/shorts#monthly-youtube-shorts-music-publisher-content-owner-revenue-summary)

  - BigQuery table:  
    p\_publisher\_content\_owner\_shorts\_revenue\_summary\_a1\_ suffix
  - BigQuery view:  
    publisher\_content\_owner\_shorts\_revenue\_summary\_a1\_ suffix

#### Monthly YouTube Shorts global ad revenue summary

YouTube report: [Monthly YouTube Shorts global ad revenue summary](https://developers.google.com/youtube/reporting/v1/reports/system_managed/shorts#monthly-youtube-shorts-global-ad-revenue-summary)

  - BigQuery table:  
    p\_content\_owner\_shorts\_global\_ad\_revenue\_summary\_a2\_ suffix
  - BigQuery view:  
    content\_owner\_shorts\_global\_ad\_revenue\_summary\_a2\_ suffix

#### Daily YouTube Shorts ad revenue summary

YouTube report: [Daily YouTube Shorts ad revenue summary](https://developers.google.com/youtube/reporting/v1/reports/system_managed/shorts#daily-youtube-shorts-ad-revenue-summary)

  - BigQuery table:  
    p\_content\_owner\_shorts\_day\_ad\_revenue\_summary\_a2\_ suffix
  - BigQuery view:  
    content\_owner\_shorts\_day\_ad\_revenue\_summary\_a2\_ suffix

#### Monthly YouTube Shorts country ad revenue summary

YouTube report: [Monthly YouTube Shorts country ad revenue summary](https://developers.google.com/youtube/reporting/v1/reports/system_managed/shorts#monthly-youtube-shorts-country-ad-revenue-summary)

  - BigQuery table:  
    p\_content\_owner\_shorts\_country\_ad\_revenue\_summary\_a2\_ suffix
  - BigQuery view:  
    content\_owner\_shorts\_country\_ad\_revenue\_summary\_a2\_ suffix

#### Monthly YouTube Shorts ad revenue summary

YouTube report: [Monthly YouTube Shorts ad revenue summary](https://developers.google.com/youtube/reporting/v1/reports/system_managed/shorts#monthly-youtube-shorts-ad-revenue-summary)

  - BigQuery table:  
    p\_content\_owner\_shorts\_ad\_revenue\_summary\_a2\_ suffix
  - BigQuery view:  
    content\_owner\_shorts\_ad\_revenue\_summary\_a2\_ suffix

#### Monthly YouTube Shorts subscriptions revenue summary

YouTube report: [Monthly YouTube Shorts subscriptions revenue summary](https://developers.google.com/youtube/reporting/v1/reports/system_managed/shorts#monthly-youtube-shorts-subscriptions-revenue-summary)

  - BigQuery table:  
    p\_content\_owner\_shorts\_red\_revenue\_summary\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_shorts\_red\_revenue\_summary\_a1\_ suffix

#### Monthly YouTube Shorts subscriptions revenue video summary

YouTube report: [Monthly YouTube Shorts subscriptions revenue video summary](https://developers.google.com/youtube/reporting/v1/reports/system_managed/shorts#monthly-youtube-shorts-subscriptions-revenue-video-summary)

  - BigQuery table:  
    p\_content\_owner\_shorts\_red\_revenue\_video\_summary\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_shorts\_red\_revenue\_video\_summary\_a1\_ suffix

### Tax withholding reports

The following reports show tax withholding calculations and summaries.

#### Tax withholding

YouTube report: [Tax withholding](https://developers.google.com/youtube/reporting/v1/reports/system_managed/taxes#tax-withholding)

  - BigQuery table:  
    p\_content\_owner\_tax\_withholding\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_tax\_withholding\_a1\_ suffix

### Video reports

The following reports contain daily metadata and summaries for videos.

#### Daily video metadata (version 1.4)

YouTube report: [Daily video metadata (version 1.4)](https://developers.google.com/youtube/reporting/v1/reports/system_managed/videos#daily-video-metadata-version-1.4)

  - BigQuery table:  
    p\_content\_owner\_video\_metadata\_a4\_ suffix
  - BigQuery view:  
    content\_owner\_video\_metadata\_a4\_ suffix

### Asset reports

The following reports detail daily network assets and asset conflicts.

#### Daily asset report

YouTube report: [Daily asset report](https://developers.google.com/youtube/reporting/v1/reports/system_managed/assets#daily-asset-report-version-1.3)

  - BigQuery table:  
    p\_content\_owner\_asset\_a3\_ suffix
  - BigQuery view:  
    content\_owner\_asset\_a3\_ suffix

#### Daily asset conflicts

YouTube report: [Daily asset conflicts](https://developers.google.com/youtube/reporting/v1/reports/system_managed/assets#daily-asset-conflicts-version-1.3)

  - BigQuery table:  
    p\_content\_owner\_asset\_conflict\_a3\_ suffix
  - BigQuery view:  
    content\_owner\_asset\_conflict\_a3\_ suffix

### Reference reports

The following reports track active reference files and metadata.

#### Weekly references

YouTube report: [Weekly references](https://developers.google.com/youtube/reporting/v1/reports/system_managed/references#weekly-references)

  - BigQuery table:  
    p\_content\_owner\_active\_references\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_active\_references\_a1\_ suffix

### Claims reports

The following reports provide daily summaries of active claims.

#### Daily claims (Version 1.2)

YouTube report: [Daily claims (Version 1.2)](https://developers.google.com/youtube/reporting/v1/reports/system_managed/claims#daily-claims-version-1.2)

  - BigQuery table:  
    p\_content\_owner\_active\_claims\_a3\_ suffix
  - BigQuery view:  
    content\_owner\_active\_claims\_a3\_ suffix

#### Monthly ad revenue audio claims

YouTube report: [Monthly ad revenue audio claims](https://developers.google.com/youtube/reporting/v1/reports/system_managed/claims#monthly-ad-revenue-audio-claims)

  - BigQuery table:  
    p\_content\_owner\_claim\_audio\_tier\_revenue\_raw\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_claim\_audio\_tier\_revenue\_raw\_a1\_ suffix

#### Monthly ad revenue audio claims summary

YouTube report: [Monthly ad revenue audio claims summary](https://developers.google.com/youtube/reporting/v1/reports/system_managed/claims#monthly-ad-revenue-audio-claims-summary)

  - BigQuery table:  
    p\_content\_owner\_claim\_audio\_tier\_revenue\_summary\_a1\_ suffix
  - BigQuery view:  
    content\_owner\_claim\_audio\_tier\_revenue\_summary\_a1\_ suffix
