# Campaign Manager report transformation

When your Campaign Manager (formerly known as DoubleClick Campaign Manager) data transfer files are transferred to BigQuery, the files are transformed into the following BigQuery tables and views.

When you view the tables and views in BigQuery, the value for campaign\_manager\_id is your Campaign Manager Network, Advertiser, or Floodlight ID.

<table>
<thead>
<tr class="header">
<th><strong>Campaign Manager file</strong></th>
<th><strong>BigQuery table</strong></th>
<th><strong>BigQuery view</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Data Transfer files</strong></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/doubleclick-advertisers/dtv2/reference/file-format">impression</a></td>
<td>p_impression_ campaign_manager_id</td>
<td>impression_ campaign_manager_id</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/doubleclick-advertisers/dtv2/reference/file-format">click</a></td>
<td>p_click_ campaign_manager_id</td>
<td>click_ campaign_manager_id</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/doubleclick-advertisers/dtv2/reference/file-format">activity</a></td>
<td>p_activity_ campaign_manager_id</td>
<td>activity_ campaign_manager_id</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/doubleclick-advertisers/dtv2/reference/file-format">rich_media</a></td>
<td>p_rich_media_ campaign_manager_id</td>
<td>rich_media_ campaign_manager_id</td>
</tr>
<tr class="even">
<td><strong>Match Tables</strong></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/doubleclick-advertisers/dtv2/reference/match-tables#activity_cats">activity_cats</a></td>
<td>p_match_table_activity_cats_ campaign_manager_id</td>
<td>match_table_activity_cats_ campaign_manager_id</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/doubleclick-advertisers/dtv2/reference/match-tables#activity_types">activity_types</a></td>
<td>p_match_table_activity_types_ campaign_manager_id</td>
<td>match_table_activity_types_ campaign_manager_id</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/doubleclick-advertisers/dtv2/reference/match-tables#ads">ads</a></td>
<td>p_match_table_ads_ campaign_manager_id</td>
<td>match_table_ads_ campaign_manager_id</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/doubleclick-advertisers/dtv2/reference/match-tables#ad_placement_assignments">ad_placement_assignments</a></td>
<td>p_match_table_ad_placement_assignments_ campaign_manager_id</td>
<td>match_table_ad_placement_assignments_ campaign_manager_id</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/doubleclick-advertisers/dtv2/reference/match-tables#advertisers">advertisers</a></td>
<td>p_match_table_advertisers_ campaign_manager_id</td>
<td>match_table_advertisers_ campaign_manager_id</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/doubleclick-advertisers/dtv2/reference/match-tables#assets">assets</a></td>
<td>p_match_table_assets_ campaign_manager_id</td>
<td>match_table_assets_ campaign_manager_id</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/doubleclick-advertisers/dtv2/reference/match-tables#browsers">browsers</a></td>
<td>p_match_table_browsers_ campaign_manager_id</td>
<td>match_table_browsers_ campaign_manager_id</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/doubleclick-advertisers/dtv2/reference/match-tables#campaigns">campaigns</a></td>
<td>p_match_table_campaigns_ campaign_manager_id</td>
<td>match_table_campaigns_ campaign_manager_id</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/doubleclick-advertisers/dtv2/reference/match-tables#cities">cities</a></td>
<td>p_match_table_cities_ campaign_manager_id</td>
<td>match_table_cities_ campaign_manager_id</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/doubleclick-advertisers/dtv2/reference/match-tables#creatives">creatives</a></td>
<td>p_match_table_creatives_ campaign_manager_id</td>
<td>match_table_creatives_ campaign_manager_id</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/doubleclick-advertisers/dtv2/reference/match-tables#creative_ad_assignments">creative_ad_assignments</a></td>
<td>p_match_table_creative_ad_assignments_ campaign_manager_id</td>
<td>match_table_creative_ad_assignments_ campaign_manager_id</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/doubleclick-advertisers/dtv2/reference/match-tables#custom_creative_fields">custom_creative_fields</a></td>
<td>p_match_table_custom_creative_fields_ campaign_manager_id</td>
<td>match_table_custom_creative_fields_ campaign_manager_id</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/doubleclick-advertisers/dtv2/reference/match-tables#paid_search">paid_search</a></td>
<td>p_match_table_paid_search_ campaign_manager_id</td>
<td>match_table_paid_search_ campaign_manager_id</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/doubleclick-advertisers/dtv2/reference/match-tables#designated_market_areas">designated_market_areas</a></td>
<td>p_match_table_designated_market_areas_ campaign_manager_id</td>
<td>match_table_designated_market_areas_ campaign_manager_id</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/doubleclick-advertisers/dtv2/reference/match-tables#keyword_value">keyword_value</a></td>
<td>p_match_table_keyword_value_ campaign_manager_id</td>
<td>match_table_keyword_value_ campaign_manager_id</td>
</tr>
<tr class="even">
<td>null user ID reason categories</td>
<td>Unsupported</td>
<td>Unsupported</td>
</tr>
<tr class="odd">
<td>rich media standard event and event type IDs</td>
<td>Unsupported</td>
<td>Unsupported</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/doubleclick-advertisers/dtv2/reference/match-tables#custom_rich_media">custom_rich_media</a></td>
<td>p_match_table_custom_rich_media_ campaign_manager_id</td>
<td>match_table_custom_rich_media_ campaign_manager_id</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/doubleclick-advertisers/dtv2/reference/match-tables#operating_systems">operating_systems</a></td>
<td>p_match_table_operating_systems_ campaign_manager_id</td>
<td>match_table_operating_systems_ campaign_manager_id</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/doubleclick-advertisers/dtv2/reference/match-tables#placements">placements</a></td>
<td>p_match_table_placements_ campaign_manager_id</td>
<td>match_table_placements_ campaign_manager_id</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/doubleclick-advertisers/dtv2/reference/match-tables#placement_cost">placement_cost</a></td>
<td>p_match_table_placement_cost_ campaign_manager_id</td>
<td>match_table_placement_cost_ campaign_manager_id</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/doubleclick-advertisers/dtv2/reference/match-tables#sites">sites</a></td>
<td>p_match_table_sites_ campaign_manager_id</td>
<td>match_table_sites_ campaign_manager_id</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/doubleclick-advertisers/dtv2/reference/match-tables#states">states</a></td>
<td>p_match_table_states_ campaign_manager_id</td>
<td>match_table_states_ campaign_manager_id</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/doubleclick-advertisers/dtv2/reference/match-tables#custom_floodlight_variables">custom_floodlight_variables</a></td>
<td>p_match_table_custom_floodlight_variables_ campaign_manager_id</td>
<td>match_table_custom_floodlight_variables_ campaign_manager_id</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/doubleclick-advertisers/dtv2/reference/match-tables#landing_page_url">landing_page_url</a></td>
<td>p_match_table_landing_page_url_ campaign_manager_id</td>
<td>match_table_landing_page_url_ campaign_manager_id</td>
</tr>
</tbody>
</table>
