# YouTube Content Owner report transformation

When your YouTube Content Owner or system-managed reports are transferred to BigQuery, the reports are transformed into the following BigQuery tables and views.

When you view the tables and views in BigQuery, the value for suffix is the table suffix you configured when you created the transfer.

<table>
<thead>
<tr class="header">
<th><strong>YouTube Content Owner report</strong></th>
<th><strong>BigQuery table</strong></th>
<th><strong>BigQuery view</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Video reports</strong></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#video-user-activity">User activity</a></td>
<td>p_content_owner_basic_a4_ suffix</td>
<td>content_owner_basic_a4_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#video-province">User activity by province</a></td>
<td>p_content_owner_province_a3_ suffix</td>
<td>content_owner_province_3_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#video-playback-locations">Playback locations</a></td>
<td>p_content_owner_playback_location_a3_ suffix</td>
<td>content_owner_playback_location_a3_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#video-traffic-sources">Traffic sources</a></td>
<td>p_content_owner_traffic_source_a3_ suffix</td>
<td>content_owner_traffic_source_a3_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#video-device-type-and-operating-system">Device type and operating system</a></td>
<td>p_content_owner_device_os_a3_ suffix</td>
<td>content_owner_device_os_a3_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#video-viewer-demographics">Viewer demographics</a></td>
<td>p_content_owner_demographics_a1_ suffix</td>
<td>content_owner_demographics_a1_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#video-content-sharing">Content sharing by platform</a></td>
<td>p_content_owner_sharing_service_a1_ suffix</td>
<td>content_owner_sharing_service_a1_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#video-annotations">Annotations</a></td>
<td>p_content_owner_annotations_a1_ suffix</td>
<td>content_owner_annotations_a1_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#video-cards">Cards</a></td>
<td>p_content_owner_cards_a1_ suffix</td>
<td>content_owner_cards_a1_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#video-end-screens">End screens</a></td>
<td>p_content_owner_end_screens_a1_ suffix</td>
<td>content_owner_end_screens_a1_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#video-subtitles">Subtitles</a></td>
<td>p_content_owner_subtitles_a3_ suffix</td>
<td>content_owner_subtitles_a3_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#video-combined">Combined</a></td>
<td>p_content_owner_combined_a3_ suffix</td>
<td>content_owner_combined_a3_ suffix</td>
</tr>
<tr class="even">
<td><strong>Playlist reports</strong></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#playlist-user-activity">User activity</a></td>
<td>p_content_owner_playlist_basic_a2_ suffix</td>
<td>content_owner_playlist_basic_a2_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#playlist-province">User activity by province</a></td>
<td>p_content_owner_playlist_province_a2_ suffix</td>
<td>content_owner_playlist_province_a2_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#playlist-playback-locations">Playback locations</a></td>
<td>p_content_owner_playlist_playback_location_a2_ suffix</td>
<td>content_owner_playlist_playback_location_a2</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#playlist-traffic-sources">Traffic sources</a></td>
<td>p_content_owner_playlist_traffic_source_a2</td>
<td>content_owner_playlist_traffic_source_a2_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#playlist-device-type-and-operating-system">Device type and operating system</a></td>
<td>p_content_owner_playlist_device_os_a2_ suffix</td>
<td>content_owner_playlist_device_os_a2_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#playlist-combined">Combined</a></td>
<td>p_content_owner_playlist_combined_a2_ suffix</td>
<td>content_owner_playlist_combined_a2_ suffix</td>
</tr>
<tr class="odd">
<td><strong>Ad rate reports</strong></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#ad-rate-reports">Ad rate reports</a></td>
<td>p_content_owner_ad_rates_a1_ suffix</td>
<td>content_owner_ad_rates_a1_ suffix</td>
</tr>
<tr class="odd">
<td><strong>Estimated revenue reports</strong></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#estimated-revenue-videos">Estimated video revenue</a></td>
<td>p_content_owner_estimated_revenue_a1_ suffix</td>
<td>content_owner_estimated_revenue_a1_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#estimated-revenue-assets">Estimated asset revenue</a></td>
<td>p_content_owner_asset_estimated_revenue_a1_ suffix</td>
<td>content_owner_asset_estimated_revenue_a1_ suffix</td>
</tr>
<tr class="even">
<td><strong>Asset reports</strong></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#asset-user-activity">User activity</a></td>
<td>p_content_owner_asset_basic_a3_ suffix</td>
<td>content_owner_asset_basic_a3_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#asset-province">User activity by province</a></td>
<td>p_content_owner_asset_province_a3_ suffix</td>
<td>content_owner_asset_province_a3_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#asset-playback-locations">Video playback locations</a></td>
<td>p_content_owner_asset_playback_location_a3_ suffix</td>
<td>content_owner_asset_playback_location_a3_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#asset-traffic-sources">Traffic sources</a></td>
<td>p_content_owner_asset_traffic_source_a3_ suffix</td>
<td>content_owner_asset_traffic_source_a3_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#asset-device-type-and-operating-system">Device type and operating system</a></td>
<td>p_content_owner_asset_device_os_a3_ suffix</td>
<td>content_owner_asset_device_os_a3_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#asset-viewer-demographics">Viewer demographics</a></td>
<td>p_content_owner_asset_demographics_a1_ suffix</td>
<td>content_owner_asset_demographics_a1_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#asset-content-sharing">Content sharing by platform</a></td>
<td>p_content_owner_asset_sharing_service_a1_ suffix</td>
<td>content_owner_asset_sharing_service_a1_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#asset-annotations">Annotations</a></td>
<td>p_content_owner_asset_annotations_a1_ suffix</td>
<td>content_owner_asset_annotations_a1_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#asset-cards">Cards</a></td>
<td>p_content_owner_asset_cards_a1_ suffix</td>
<td>content_owner_asset_cards_a1_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#asset-end-screens">End screens</a></td>
<td>p_content_owner_asset_end_screens_a1_ suffix</td>
<td>content_owner_asset_end_screens_a1_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#asset-combined">Combined</a></td>
<td>p_content_owner_asset_combined_a3_ suffix</td>
<td>content_owner_asset_combined_a3_ suffix</td>
</tr>
<tr class="even">
<td><strong>Reach reports</strong></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#reach-reports">Reach basic</a></td>
<td>p_content_owner_reach_basic_a1_ suffix</td>
<td>content_owner_reach_basic_a1_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/content_owner_reports#reach-reports">Reach combined</a></td>
<td>p_content_owner_reach_combined_a1_ suffix</td>
<td>content_owner_reach_combined_a1_ suffix</td>
</tr>
</tbody>
</table>

<table>
<thead>
<tr class="header">
<th><strong>Youtube System-managed reports</strong></th>
<th><strong>BigQuery table</strong></th>
<th><strong>BigQuery view</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Ads revenue reports</strong></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#monthly-global-ad-revenue-summary">Monthly global ad revenue summary</a></td>
<td>p_content_owner_global_ad_revenue_summary_a1_ suffix</td>
<td>content_owner_global_ad_revenue_summary_a1_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#monthly-country-ad-revenue-summary">Monthly country ad revenue summary</a></td>
<td>p_content_owner_country_ad_revenue_summary_a1_ suffix</td>
<td>content_owner_country_ad_revenue_summary_a1_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#monthly-day-ad-revenue-summary">Monthly day ad revenue summary</a></td>
<td>p_content_owner_day_ad_revenue_summary_a1_ suffix</td>
<td>content_owner_day_ad_revenue_summary_a1_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#weekly-global-ad-revenue-summary">Weekly global ad revenue summary</a></td>
<td>p_content_owner_global_ad_revenue_summary_weekly_a1_ suffix</td>
<td>content_owner_global_ad_revenue_summary_weekly_a1_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#weekly-country-ad-revenue-summary">Weekly country ad revenue summary</a></td>
<td>p_content_owner_country_ad_revenue_summary_weekly_a1_ suffix</td>
<td>content_owner_country_ad_revenue_summary_weekly_a1_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#weekly-day-ad-revenue-summary">Weekly day ad revenue summary</a></td>
<td>p_content_owner_day_ad_revenue_summary_weekly_a1_ suffix</td>
<td>content_owner_day_ad_revenue_summary_weekly_a1_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#aggregate-ad-revenue-per-video">Aggregate ad revenue per video</a></td>
<td>p_content_owner_ad_revenue_summary_a1_ suffix</td>
<td>content_owner_ad_revenue_summary_a1_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#weekly-video-ad-revenue-summary">Weekly video ad revenue summary</a></td>
<td>p_content_owner_ad_revenue_summary_weekly_a1_ suffix</td>
<td>content_owner_ad_revenue_summary_weekly_a1_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#weekly-video-ad-revenue">Weekly video ad revenue</a></td>
<td>p_content_owner_ad_revenue_raw_weekly_a1_ suffix</td>
<td>content_owner_ad_revenue_raw_weekly_a1_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#daily-ad-revenue-per-video">Daily ad revenue per video</a></td>
<td>p_content_owner_ad_revenue_raw_a1_ suffix</td>
<td>content_owner_ad_revenue_raw_a1_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#aggregate-ad-revenue-per-asset">Aggregate ad revenue per asset</a></td>
<td>p_content_owner_asset_ad_revenue_summary_a1_ suffix</td>
<td>content_owner_asset_ad_revenue_summary_a1_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#daily-ad-revenue-per-asset">Daily ad revenue per asset</a></td>
<td>p_content_owner_asset_ad_revenue_raw_a1_ suffix</td>
<td>content_owner_asset_ad_revenue_raw_a1_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#monthly-claim-ad-revenue-summary">Monthly claim ad revenue summary</a></td>
<td>p_content_owner_claim_ad_revenue_summary_a1_ suffix</td>
<td>content_owner_claim_ad_revenue_summary_a1_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#weekly-claim-ad-revenue-summary">Weekly claim ad revenue summary</a></td>
<td>p_content_owner_claim_ad_revenue_summary_weekly_a1_ suffix</td>
<td>content_owner_claim_ad_revenue_summary_weekly_a1_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#monthly-claim-ad-revenue">Monthly claim ad revenue</a></td>
<td>p_content_owner_claim_ad_revenue_raw_a1_ suffix</td>
<td>content_owner_claim_ad_revenue_raw_a1_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#weekly-claim-ad-revenue">Weekly claim ad revenue</a></td>
<td>p_content_owner_claim_ad_revenue_raw_weekly_a1_ suffix</td>
<td>content_owner_claim_ad_revenue_raw_weekly_a1_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#monthly-global-ad-adjustment-revenue-summary">Monthly global ad adjustment revenue summary</a></td>
<td>p_content_owner_global_ad_adjustment_revenue_summary_a1_ suffix</td>
<td>content_owner_global_ad_adjustment_revenue_summary_a1_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#monthly-asset-ad-adjustment-revenue-summary">Monthly asset ad adjustment revenue summary</a></td>
<td>p_content_owner_asset_ad_adjustment_revenue_summary_a1_ suffix</td>
<td>content_owner_asset_ad_adjustment_revenue_summary_a1_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#monthly-asset-ad-adjustment-revenue">Monthly asset ad adjustment revenue</a></td>
<td>p_content_owner_asset_ad_adjustment_revenue_raw_a1_ suffix</td>
<td>content_owner_asset_ad_adjustment_revenue_raw_a1_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#monthly-video-ad-adjustment-revenue-summary">Monthly video ad adjustment revenue summary</a></td>
<td>p_content_owner_ad_adjustment_revenue_summary_a1_ suffix</td>
<td>content_owner_ad_adjustment_revenue_summary_a1_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#monthly-video-ad-adjustment-revenue-raw">Monthly video ad adjustment revenue raw</a></td>
<td>p_content_owner_ad_adjustment_revenue_raw_a1_ suffix</td>
<td>content_owner_ad_adjustment_revenue_raw_a1_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#monthly-claim-ad-adjustment-revenue-summary">Monthly claim ad adjustment revenue summary</a></td>
<td>p_content_owner_claim_ad_adjustment_revenue_summary_a1_ suffix</td>
<td>content_owner_claim_ad_adjustment_revenue_summary_a1_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#monthly-claim-ad-adjustment-revenue">Monthly claim ad adjustment revenue</a></td>
<td>p_content_owner_claim_ad_adjustment_revenue_raw_a1_ suffix</td>
<td>content_owner_claim_ad_adjustment_revenue_raw_a1_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#monthly-country-ad-adjustment-revenue-summary">Monthly country ad adjustment revenue summary</a></td>
<td>p_content_owner_country_ad_adjustment_revenue_summary_a1_ suffix</td>
<td>content_owner_country_ad_adjustment_revenue_summary_a1_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/ads#monthly-day-ad-adjustment-revenue-summary">Monthly day ad adjustment revenue summary</a></td>
<td>p_content_owner_day_ad_adjustment_revenue_summary_a1_ suffix</td>
<td>content_owner_day_ad_adjustment_revenue_summary_a1_ suffix</td>
</tr>
<tr class="odd">
<td><strong>Subscription revenue reports</strong></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-music-revenue-summary">Monthly music revenue summary</a></td>
<td>p_content_owner_country_music_red_revenue_summary_a1_ suffix</td>
<td>content_owner_country_music_red_revenue_summary_a1_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-music-label-video-revenue">Monthly music label video revenue</a></td>
<td>p_music_content_owner_red_revenue_raw_a1_ suffix</td>
<td>music_content_owner_red_revenue_raw_a1_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-music-label-assets-revenue">Monthly music label assets revenue</a></td>
<td>p_music_content_owner_asset_red_revenue_raw_a1_ suffix</td>
<td>music_content_owner_asset_red_revenue_raw_a1_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-music-label-subscriber-revenue-summary">Monthly music label subscriber revenue summary</a></td>
<td>p_music_content_owner_subscriber_red_revenue_summary_a1_ suffix</td>
<td>music_content_owner_subscriber_red_revenue_summary_a1_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-music-publisher-revenue-summary">Monthly music publisher revenue summary</a></td>
<td>p_publisher_content_owner_music_red_revenue_summary_a1_ suffix</td>
<td>publisher_content_owner_music_red_revenue_summary_a1_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-music-publisher-subscription-revenue-summary">Monthly music publisher subscription revenue summary</a></td>
<td>p_publisher_content_owner_subscriber_red_revenue_summary_a1_ suffix</td>
<td>publisher_content_owner_subscriber_red_revenue_summary_a1_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-music-publisher-non-music-subscription-revenue-summary">Monthly music publisher non-music subscription revenue summary</a></td>
<td>p_publisher_content_owner_non_music_red_revenue_summary_a1_ suffix</td>
<td>publisher_content_owner_non_music_red_revenue_summary_a1_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-music-label-music-revenue-summary">Monthly music label music revenue summary</a></td>
<td>p_music_content_owner_country_music_red_revenue_summary_a1_ suffix</td>
<td>music_content_owner_country_music_red_revenue_summary_a1_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-subscriptions-music-video-revenue">Monthly subscriptions music video revenue</a></td>
<td>p_content_owner_music_red_revenue_raw_a1_ suffix</td>
<td>content_owner_music_red_revenue_raw_a1_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-subscriptions-music-assets-revenue">Monthly subscriptions music assets revenue</a></td>
<td>p_content_owner_music_asset_red_revenue_raw_a1_ suffix</td>
<td>content_owner_music_asset_red_revenue_raw_a1_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#weekly-music-revenue-summary">Weekly music revenue summary</a></td>
<td>p_music_content_owner_country_music_red_revenue_summary_weekly_a1_ suffix</td>
<td>music_content_owner_country_music_red_revenue_summary_weekly_a1_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#weekly-music-label-videos-revenue">Weekly music label videos revenue</a></td>
<td>p_music_content_owner_red_revenue_raw_weekly_a1_ suffix</td>
<td>music_content_owner_red_revenue_raw_weekly_a1_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#weekly-music-label-assets-revenue">Weekly music label assets revenue</a></td>
<td>p_music_content_owner_asset_red_revenue_raw_weekly_a1_ suffix</td>
<td>music_content_owner_asset_red_revenue_raw_weekly_a1_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-non-music-summary">Monthly non-music summary</a></td>
<td>p_content_owner_country_non_music_red_revenue_summary_a1_ suffix</td>
<td>content_owner_country_non_music_red_revenue_summary_a1_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-music-label-non-music-revenue-summary">Monthly music label non-music revenue summary</a></td>
<td>p_music_content_owner_country_non_music_red_revenue_summary_a1_ suffix</td>
<td>music_content_owner_country_non_music_red_revenue_summary_a1_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-subscriptions-non-music-videos-revenue">Monthly subscriptions non-music videos revenue</a></td>
<td>p_content_owner_non_music_red_revenue_raw_a1_ suffix</td>
<td>content_owner_non_music_red_revenue_raw_a1_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-subscriptions-non-music-assets-revenuee">Monthly subscriptions non-music assets revenue</a></td>
<td>p_content_owner_non_music_asset_red_revenue_raw_a1_ suffix</td>
<td>content_owner_non_music_asset_red_revenue_raw_a1_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#weekly-non-music-revenue-summary">Weekly non-music revenue summary</a></td>
<td>p_music_content_owner_country_non_music_red_revenue_summary_weekly_a1_ suffix</td>
<td>music_content_owner_country_non_music_red_revenue_summary_weekly_a1_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-music-label-asset-subscription-adjustment-revenue-raw">Monthly music label asset subscription adjustment revenue raw</a></td>
<td>p_music_content_owner_asset_red_adjustment_revenue_raw_a1_ suffix</td>
<td>music_content_owner_asset_red_adjustment_revenue_raw_a1_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-subscriptions-adjustment-music-video-raw">Monthly subscriptions adjustment music video raw</a></td>
<td>p_music_content_owner_red_adjustment_revenue_raw_a1_ suffix</td>
<td>music_content_owner_red_adjustment_revenue_raw_a1_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-music-label-country-music-subscription-adjustment-revenue-summary">Monthly music label country music subscription adjustment revenue summary</a></td>
<td>p_music_content_owner_country_music_red_adjustment_revenue_summary_a1_ suffix</td>
<td>music_content_owner_country_music_red_adjustment_revenue_summary_a1_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-music-label-country-non-music-subscription-adjustment-revenue-summary">Monthly music label country non-music subscription adjustment revenue summary</a></td>
<td>p_music_content_owner_country_non_music_red_adjustment_revenue_summary_a1_ suffix</td>
<td>music_content_owner_country_non_music_red_adjustment_revenue_summary_a1_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-non-music-asset-subscription-adjustment-revenue-raw">Monthly non-music asset subscription adjustment revenue raw</a></td>
<td>p_content_owner_non_music_asset_red_adjustment_revenue_raw_a1_ suffix</td>
<td>content_owner_non_music_asset_red_adjustment_revenue_raw_a1_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-non-music-subscription-adjustment-revenue-raw">Monthly non-music subscription adjustment revenue raw</a></td>
<td>p_content_owner_non_music_red_adjustment_revenue_raw_a1_ suffix</td>
<td>content_owner_non_music_red_adjustment_revenue_raw_a1_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-music-video-subscription-adjustment-revenue-raw">Monthly music video subscription adjustment revenue raw</a></td>
<td>p_content_owner_music_video_red_adjustment_revenue_raw_a1_ suffix</td>
<td>content_owner_music_video_red_adjustment_revenue_raw_a1_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-music-asset-subscription-adjustment-revenue-raw">Monthly music asset subscription adjustment revenue raw</a></td>
<td>p_content_owner_music_asset_red_adjustment_revenue_raw_a1_ suffix</td>
<td>content_owner_music_asset_red_adjustment_revenue_raw_a1_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-music-publisher-asset-subscription-adjustment-revenue-raw">Monthly music publisher asset subscription adjustment revenue raw</a></td>
<td>p_publisher_content_owner_asset_red_adjustment_revenue_raw_a1_ suffix</td>
<td>publisher_content_owner_asset_red_adjustment_revenue_raw_a1_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-music-publisher-country-non-music-subscription-adjustment-revenue-summary">Monthly music publisher country non-music subscription adjustment revenue summary</a></td>
<td>p_publisher_content_owner_country_non_music_red_adjustment_revenue_summary_a1_ suffix</td>
<td>publisher_content_owner_country_non_music_red_adjustment_revenue_summary_a1_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/subscriptions#monthly-music-publisher-country-music-subscription-adjustment-revenue-summary">Monthly music publisher country music subscription adjustment revenue summary</a></td>
<td>p_publisher_content_owner_country_music_red_adjustment_revenue_summary_a1_ suffix</td>
<td>publisher_content_owner_country_music_red_adjustment_revenue_summary_a1_ suffix</td>
</tr>
<tr class="odd">
<td><strong>Shorts revenue reports</strong></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/shorts#monthly-youtube-shorts-music-label-content-owner-revenue-summary">Monthly YouTube Shorts music label content owner revenue summary</a></td>
<td>p_music_content_owner_shorts_revenue_summary_a1_ suffix</td>
<td>music_content_owner_shorts_revenue_summary_a1_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/shorts#monthly-youtube-shorts-music-publisher-content-owner-revenue-summary">Monthly YouTube Shorts music publisher content owner revenue summary</a></td>
<td>p_publisher_content_owner_shorts_revenue_summary_a1_ suffix</td>
<td>publisher_content_owner_shorts_revenue_summary_a1_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/shorts#monthly-youtube-shorts-global-ad-revenue-summary">Monthly YouTube Shorts global ad revenue summary</a></td>
<td>p_content_owner_shorts_global_ad_revenue_summary_a2_ suffix</td>
<td>content_owner_shorts_global_ad_revenue_summary_a2_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/shorts#daily-youtube-shorts-ad-revenue-summary">Daily YouTube Shorts ad revenue summary</a></td>
<td>p_content_owner_shorts_day_ad_revenue_summary_a2_ suffix</td>
<td>content_owner_shorts_day_ad_revenue_summary_a2_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/shorts#monthly-youtube-shorts-country-ad-revenue-summary">Monthly YouTube Shorts country ad revenue summary</a></td>
<td>p_content_owner_shorts_country_ad_revenue_summary_a2_ suffix</td>
<td>content_owner_shorts_country_ad_revenue_summary_a2_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/shorts#monthly-youtube-shorts-ad-revenue-summary">Monthly YouTube Shorts ad revenue summary</a></td>
<td>p_content_owner_shorts_ad_revenue_summary_a2_ suffix</td>
<td>content_owner_shorts_ad_revenue_summary_a2_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/shorts#monthly-youtube-shorts-subscriptions-revenue-summary">Monthly YouTube Shorts subscriptions revenue summary</a></td>
<td>p_content_owner_shorts_red_revenue_summary_a1_ suffix</td>
<td>content_owner_shorts_red_revenue_summary_a1_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/shorts#monthly-youtube-shorts-subscriptions-revenue-video-summary">Monthly YouTube Shorts subscriptions revenue video summary</a></td>
<td>p_content_owner_shorts_red_revenue_video_summary_a1_ suffix</td>
<td>content_owner_shorts_red_revenue_video_summary_a1_ suffix</td>
</tr>
<tr class="even">
<td><strong>Taxes withholding reports</strong></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/taxes#tax-withholding">Tax withholding</a></td>
<td>p_content_owner_tax_withholding_a1_ suffix</td>
<td>content_owner_tax_withholding_a1_ suffix</td>
</tr>
<tr class="even">
<td><strong>Videos reports</strong></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/videos#daily-video-metadata-version-1.4">Daily video metadata (version 1.4)</a></td>
<td>p_content_owner_video_metadata_a4_ suffix</td>
<td>content_owner_video_metadata_a4_ suffix</td>
</tr>
<tr class="even">
<td><strong>Assets reports</strong></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/assets#daily-asset-report-version-1.3">Daily asset report</a></td>
<td>p_content_owner_asset_a3_ suffix</td>
<td>content_owner_asset_a3_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/assets#daily-asset-conflicts-version-1.3">Daily asset conflicts</a></td>
<td>p_content_owner_asset_conflict_a3_ suffix</td>
<td>content_owner_asset_conflict_a3_ suffix</td>
</tr>
<tr class="odd">
<td><strong>References reports</strong></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/references#weekly-references">Weekly references</a></td>
<td>p_content_owner_active_references_a1_ suffix</td>
<td>content_owner_active_references_a1_ suffix</td>
</tr>
<tr class="odd">
<td><strong>Claims reports</strong></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/system_managed/claims#daily-claims-version-1.2">Daily claims (Version 1.2)</a></td>
<td>p_content_owner_active_claims_a3_ suffix</td>
<td>content_owner_active_claims_a3_ suffix</td>
</tr>
</tbody>
</table>
