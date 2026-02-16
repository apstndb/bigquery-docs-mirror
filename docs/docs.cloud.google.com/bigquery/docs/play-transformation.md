# Google Play report transformation

When your Google Play reports are transferred to BigQuery, the reports are transformed into the following BigQuery tables and views.

When you view the tables and views in BigQuery, the value for suffix is the table suffix you configured when you created the transfer.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Google Play report</th>
<th>BigQuery table</th>
<th>BigQuery view</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Detailed Reports</strong></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><strong><em>Reviews</em></strong></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="https://support.google.com/googleplay/android-developer/answer/6135870#reviews">Reviews</a></td>
<td>p_Reviews_ suffix</td>
<td>Reviews_ suffix</td>
</tr>
<tr class="even">
<td><strong><em>Financial Reports</em></strong></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="https://support.google.com/googleplay/android-developer/answer/6135870#financial">Estimated Sales</a></td>
<td>p_Sales_ suffix</td>
<td>Sales_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://support.google.com/googleplay/android-developer/answer/6135870#financial">Earnings</a></td>
<td>p_Earnings_ suffix</td>
<td>Earnings_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://support.google.com/googleplay/android-developer/answer/6135870#financial">Korean Play balance funded</a></td>
<td>p_Korean_Play_balance_funded_ suffix</td>
<td>Korean_Play_balance_funded_ suffix</td>
</tr>
<tr class="even">
<td><strong>Aggregated Reports</strong></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><strong><em>Statistics</em></strong></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><a href="https://support.google.com/googleplay/android-developer/answer/6135870#statistics">Installs</a></td>
<td>p_Installs_app_version_ suffix<br />
p_Installs_carrier_ suffix<br />
p_Installs_country_ suffix<br />
p_Installs_device_ suffix<br />
p_Installs_language_ suffix<br />
p_Installs_os_version_ suffix</td>
<td>Installs_app_version_ suffix<br />
Installs_carrier_ suffix<br />
Installs_country_ suffix<br />
Installs_device_ suffix<br />
Installs_language_ suffix<br />
Installs_os_version_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://support.google.com/googleplay/android-developer/answer/6135870#statistics">Crashes</a></td>
<td>p_Crashes_app_version_ suffix<br />
p_Crashes_device_ suffix<br />
p_Crashes_os_version_ suffix</td>
<td>Crashes_app_version_ suffix<br />
Crashes_device_ suffix<br />
Crashes_os_version_ suffix</td>
</tr>
<tr class="even">
<td><a href="https://support.google.com/googleplay/android-developer/answer/6135870#statistics">Ratings</a></td>
<td>p_Ratings_app_version_ suffix<br />
p_Ratings_carrier_ suffix<br />
p_Ratings_country_ suffix<br />
p_Ratings_device_ suffix<br />
p_Ratings_language_ suffix<br />
p_Ratings_os_version_ suffix</td>
<td>Ratings_app_version_ suffix<br />
Ratings_carrier_ suffix<br />
Ratings_country_ suffix<br />
Ratings_device_ suffix<br />
Ratings_language_ suffix<br />
Ratings_os_version_ suffix</td>
</tr>
<tr class="odd">
<td><a href="https://support.google.com/googleplay/android-developer/answer/6135870#statistics">Subscribers</a></td>
<td>p_Stats_Subscribers_country_ suffix<br />
p_Stats_Subscribers_device_ suffix</td>
<td>Stats_Subscribers_country_ suffix<br />
Stats_Subscribers_device_ suffix</td>
</tr>
<tr class="even">
<td><strong><em>User Acquisition</em></strong></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="https://support.google.com/googleplay/android-developer/answer/6135870#acquisition">Store Performance</a></td>
<td>p_Store_Performance_country_ suffix<br />
p_Store_Performance_traffic_source_ suffix<br />
</td>
<td>Store_Performance_country_ suffix<br />
Store_Performance_traffic_source_ suffix<br />
</td>
</tr>
</tbody>
</table>
