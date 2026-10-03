---
name: documents/docs.cloud.google.com/bigquery/docs/youtube-channel-transformation
uri: https://docs.cloud.google.com/bigquery/docs/youtube-channel-transformation
title: YouTube Channel report transformation
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# YouTube Channel report transformation

When your YouTube Channel reports are transferred to BigQuery, the reports are transformed into the following BigQuery tables and views.

When you view the tables and views in BigQuery, the value for ` suffix ` is the table suffix you configured when you created the transfer.

| **YouTube Channel report**                                                                                                                               | **BigQuery table**                           | **BigQuery view**                          |
|----------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------|--------------------------------------------|
| **Video reports**                                                                                                                                        |                                              |                                            |
| [User activity](https://developers.google.com/youtube/reporting/v1/reports/channel_reports#video-user-activity)                                          | p_channel_basic_a3\_ ` suffix `              | channel_basic_a3\_ ` suffix `              |
| [User activity by province](https://developers.google.com/youtube/reporting/v1/reports/channel_reports#video-province)                                   | p_channel_province_a3\_ ` suffix `           | channel_province_a3\_ ` suffix `           |
| [Playback locations](https://developers.google.com/youtube/reporting/v1/reports/channel_reports#video-playback-locations)                                | p_channel_playback_location_a3\_ ` suffix `  | channel_playback_location_a3\_ ` suffix `  |
| [Traffic sources](https://developers.google.com/youtube/reporting/v1/reports/channel_reports#video-traffic-sources)                                      | p_channel_traffic_source_a3\_ ` suffix `     | channel_traffic_source_a3\_ ` suffix `     |
| [Device type and operating system](https://developers.google.com/youtube/reporting/v1/reports/channel_reports#video-device-type-and-operating-system)    | p_channel_device_os_a3\_ ` suffix `          | channel_device_os_a3\_ ` suffix `          |
| [Viewer demographics](https://developers.google.com/youtube/reporting/v1/reports/channel_reports#video-viewer-demographics)                              | p_channel_demographics_a1\_ ` suffix `       | channel_demographics_a1\_ ` suffix `       |
| [Content sharing by platform](https://developers.google.com/youtube/reporting/v1/reports/channel_reports#video-content-sharing)                          | p_channel_sharing_service_a1\_ ` suffix `    | channel_sharing_service_a1\_ ` suffix `    |
| [Annotations](https://developers.google.com/youtube/reporting/v1/reports/channel_reports#video-annotations)                                              | p_channel_annotations_a1\_ ` suffix `        | channel_annotations_a1\_ ` suffix `        |
| [Cards](https://developers.google.com/youtube/reporting/v1/reports/channel_reports#video-cards)                                                          | p_channel_cards_a1\_ ` suffix `              | channel_cards_a1\_ ` suffix `              |
| [End screens](https://developers.google.com/youtube/reporting/v1/reports/channel_reports#video-end-screens)                                              | p_channel_end_screens_a1\_ ` suffix `        | channel_end_screens_a1\_ ` suffix `        |
| [Subtitles](https://developers.google.com/youtube/reporting/v1/reports/channel_reports#video-subtitles)                                                  | p_channel_subtitles_a3\_ ` suffix `          | channel_subtitles_a3\_ ` suffix `          |
| [Combined](https://developers.google.com/youtube/reporting/v1/reports/channel_reports#video-combined)                                                    | p_channel_combined_a3\_ ` suffix `           | channel_combined_a3\_ ` suffix `           |
| **Playlist reports**                                                                                                                                     |                                              |                                            |
| [User activity](https://developers.google.com/youtube/reporting/v1/reports/channel_reports#playlist-user-activity)                                       | p_playlist_basic_a2\_ ` suffix `             | playlist_basic_a2\_ ` suffix `             |
| [User activity by province](https://developers.google.com/youtube/reporting/v1/reports/channel_reports#playlist-province)                                | p_playlist_province_a2\_ ` suffix `          | playlist_province_a2\_ ` suffix `          |
| [Playback locations](https://developers.google.com/youtube/reporting/v1/reports/channel_reports#playlist-playback-locations)                             | p_playlist_playback_location_a2\_ ` suffix ` | playlist_playback_location_a2\_ ` suffix ` |
| [Traffic sources](https://developers.google.com/youtube/reporting/v1/reports/channel_reports#playlist-traffic-sources)                                   | p_playlist_traffic_source_a2\_ ` suffix `    | playlist_traffic_source_a2\_ ` suffix `    |
| [Device type and operating system](https://developers.google.com/youtube/reporting/v1/reports/channel_reports#playlist-device-type-and-operating-system) | p_playlist_device_os_a2\_ ` suffix `         | playlist_device_os_a2\_ ` suffix `         |
| [Combined](https://developers.google.com/youtube/reporting/v1/reports/channel_reports#playlist-combined)                                                 | p_playlist_combined_a2\_ ` suffix `          | playlist_combined_a2\_ ` suffix `          |
| **Reach reports**                                                                                                                                        |                                              |                                            |
| [Reach basic](https://developers.google.com/youtube/reporting/v1/reports/channel_reports#reach-reports)                                                  | p_channel_reach_basic_a1\_ ` suffix `        | channel_reach_basic_a1\_ ` suffix `        |
| [Reach combined](https://developers.google.com/youtube/reporting/v1/reports/channel_reports#reach-reports)                                               | p_channel_reach_combined_a1\_ ` suffix `     | channel_reach_combined_a1\_ ` suffix `     |
