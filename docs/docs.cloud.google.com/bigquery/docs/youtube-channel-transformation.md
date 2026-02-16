# YouTube Channel report transformation

When your YouTube Channel reports are transferred to BigQuery, the reports are transformed into the following BigQuery tables and views.

When you view the tables and views in BigQuery, the value for suffix is the table suffix you configured when you created the transfer.

<table>
<thead>
<tr class="header">
<th><strong>YouTube Channel report</strong></th>
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
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/channel_reports#video-user-activity">User activity</a></td>
<td>p_channel_basic_a3_ suffix</td>
<td>channel_basic_a3_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/channel_reports#video-province">User activity by province</a></td>
<td>p_channel_province_a3_ suffix</td>
<td>channel_province_a3_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/channel_reports#video-playback-locations">Playback locations</a></td>
<td>p_channel_playback_location_a3_ suffix</td>
<td>channel_playback_location_a3_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/channel_reports#video-traffic-sources">Traffic sources</a></td>
<td>p_channel_traffic_source_a3_ suffix</td>
<td>channel_traffic_source_a3_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/channel_reports#video-device-type-and-operating-system">Device type and operating system</a></td>
<td>p_channel_device_os_a3_ suffix</td>
<td>channel_device_os_a3_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/channel_reports#video-viewer-demographics">Viewer demographics</a></td>
<td>p_channel_demographics_a1_ suffix</td>
<td>channel_demographics_a1_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/channel_reports#video-content-sharing">Content sharing by platform</a></td>
<td>p_channel_sharing_service_a1_ suffix</td>
<td>channel_sharing_service_a1_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/channel_reports#video-annotations">Annotations</a></td>
<td>p_channel_annotations_a1_ suffix</td>
<td>channel_annotations_a1_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/channel_reports#video-cards">Cards</a></td>
<td>p_channel_cards_a1_ suffix</td>
<td>channel_cards_a1_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/channel_reports#video-end-screens">End screens</a></td>
<td>p_channel_end_screens_a1_ suffix</td>
<td>channel_end_screens_a1_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/channel_reports#video-subtitles">Subtitles</a></td>
<td>p_channel_subtitles_a3_ suffix</td>
<td>channel_subtitles_a3_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/channel_reports#video-combined">Combined</a></td>
<td>p_channel_combined_a3_ suffix</td>
<td>channel_combined_a3_ suffix</td>
</tr>
<tr class="even">
<td><strong>Playlist reports</strong></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/channel_reports#playlist-user-activity">User activity</a></td>
<td>p_playlist_basic_a2_ suffix</td>
<td>playlist_basic_a2_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/channel_reports#playlist-province">User activity by province</a></td>
<td>p_playlist_province_a2_ suffix</td>
<td>playlist_province_a2_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/channel_reports#playlist-playback-locations">Playback locations</a></td>
<td>p_playlist_playback_location_a2_ suffix</td>
<td>playlist_playback_location_a2_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/channel_reports#playlist-traffic-sources">Traffic sources</a></td>
<td>p_playlist_traffic_source_a2_ suffix</td>
<td>playlist_traffic_source_a2_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/channel_reports#playlist-device-type-and-operating-system">Device type and operating system</a></td>
<td>p_playlist_device_os_a2_ suffix</td>
<td>playlist_device_os_a2_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/channel_reports#playlist-combined">Combined</a></td>
<td>p_playlist_combined_a2_ suffix</td>
<td>playlist_combined_a2_ suffix</td>
</tr>
<tr class="odd">
<td><strong>Reach reports</strong></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/channel_reports#reach-reports">Reach basic</a></td>
<td>p_channel_reach_basic_a1_ suffix</td>
<td>channel_reach_basic_a1_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/youtube/reporting/v1/reports/channel_reports#reach-reports">Reach combined</a></td>
<td>p_channel_reach_combined_a1_ suffix</td>
<td>channel_reach_combined_a1_ suffix</td>
</tr>
</tbody>
</table>
