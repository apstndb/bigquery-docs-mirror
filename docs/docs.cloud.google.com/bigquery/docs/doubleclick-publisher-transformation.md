# Google Ad Manager report transformation

When your Google Ad Manager (formerly known as DoubleClick for Publishers) data transfer files are transferred to BigQuery, the files are transformed into the following BigQuery tables and views.

When you view the tables and views in BigQuery, the value for network\_code is your Google Ad Manager network code.

<table>
<thead>
<tr class="header">
<th><strong>Google Ad Manager file</strong></th>
<th><strong>BigQuery table(s)</strong></th>
<th><strong>BigQuery view(s)</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Data Transfer files</strong></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><a href="https://support.google.com/admanager/answer/1733124">NetworkRequests NetworkBackfillRequests</a></td>
<td>p_NetworkRequests_ network_code p_NetworkBackfillRequests_ network_code</td>
<td>NetworkRequests_ network_code NetworkBackfillRequests_ network_code</td>
</tr>
<tr class="odd">
<td><a href="https://support.google.com/admanager/answer/1733124">NetworkCodeServes NetworkBackfillCodeServes</a></td>
<td>p_NetworkCodeServes p_NetworkBackfillCodeServes_ network_code</td>
<td>NetworkCodeServes NetworkBackfillCodeServes_ network_code</td>
</tr>
<tr class="even">
<td><a href="https://support.google.com/admanager/answer/1733124">NetworkImpressions NetworkBackfillImpressions</a></td>
<td>p_NetworkImpressions_ network_code p_NetworkBackfillImpressions_ network_code</td>
<td>NetworkImpressions_ network_code NetworkBackfillImpressions_ network_code</td>
</tr>
<tr class="odd">
<td><a href="https://support.google.com/admanager/answer/1733124">NetworkClicks NetworkBackfillClicks</a></td>
<td>p_NetworkClicks_ network_code p_NetworkBackfillClicks_ network_code</td>
<td>NetworkClicks_ network_code NetworkBackfillClicks_ network_code</td>
</tr>
<tr class="even">
<td><a href="https://support.google.com/admanager/answer/1733124">NetworkActiveViews NetworkBackfillActiveViews</a></td>
<td>p_NetworkActiveViews_ network_code p_NetworkBackfillActiveViews_ network_code</td>
<td>NetworkActiveViews_ network_code NetworkBackfillActiveViews_ network_code</td>
</tr>
<tr class="odd">
<td><a href="https://support.google.com/admanager/answer/1733124">NetworkBackfillBids</a></td>
<td>p_NetworkBackfillBids_ network_code</td>
<td>NetworkBackfillBids_ network_code</td>
</tr>
<tr class="even">
<td><a href="https://support.google.com/admanager/answer/1733124">NetworkVideoConversions NetworkBackfillVideoConversions</a></td>
<td>p_NetworkVideoConversions_ network_code p_NetworkBackfillVideoConversions_ network_code</td>
<td>NetworkVideoConversions_ network_code NetworkBackfillVideoConversions_ network_code</td>
</tr>
<tr class="odd">
<td><a href="https://support.google.com/admanager/answer/1733124">NetworkRichMediaConversions NetworkBackfillRichMediaConversions</a></td>
<td>p_NetworkRichMediaConversions_ network_code p_NetworkBackfillRichMediaConversions_ network_code</td>
<td>NetworkRichMediaConversions_ network_code NetworkBackfillRichMediaConversions_ network_code</td>
</tr>
<tr class="even">
<td><a href="https://support.google.com/admanager/answer/1733124">NetworkActivities</a></td>
<td>p_NetworkActivities_ network_code</td>
<td>NetworkActivities_ network_code</td>
</tr>
<tr class="odd">
<td><strong>Match Tables</strong></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables">AdCategory</a></td>
<td>p_MatchTableAdCategory_ network_code</td>
<td>MatchTableAdCategory_ network_code</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables">AdUnit</a></td>
<td>p_MatchTableAdUnit_ network_code</td>
<td>MatchTableAdUnit_ network_code</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables">AudienceSegment</a></td>
<td>p_MatchTableAudienceSegment_ network_code</td>
<td>MatchTableAudienceSegment_ network_code</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables">AudienceSegmentCategory</a></td>
<td>p_MatchTableAudienceSegmentCategory_ network_code</td>
<td>MatchTableAudienceSegmentCategory_ network_code</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables">BandwidthGroup</a></td>
<td>p_MatchTableBandwidthGroup_ network_code</td>
<td>MatchTableBandwidthGroup_ network_code</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables">Browser</a></td>
<td>p_MatchTableBrowser_ network_code</td>
<td>MatchTableBrowser_ network_code</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables">BrowserLanguage</a></td>
<td>p_MatchTableBrowserLanguage_ network_code</td>
<td>MatchTableBrowserLanguage_ network_code</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables">Company</a></td>
<td>p_MatchTableCompany_ network_code</td>
<td>MatchTableCompany_ network_code</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables">DeviceCapability</a></td>
<td>p_MatchTableDeviceCapability_ network_code</td>
<td>MatchTableDeviceCapability_ network_code</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables">DeviceCategory</a></td>
<td>p_MatchTableDeviceCategory_ network_code</td>
<td>MatchTableDeviceCategory_ network_code</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables">DeviceManufacturer</a></td>
<td>p_MatchTableDeviceManufacturer_ network_code</td>
<td>MatchTableDeviceManufacturer_ network_code</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables">ExchangeRate</a> (deprecated)</td>
<td>-</td>
<td>-</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables">GeoTarget</a></td>
<td>p_MatchTableGeoTarget_ network_code</td>
<td>MatchTableGeoTarget_ network_code</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables">LineItem</a></td>
<td>p_MatchTableLineItem_ network_code</td>
<td>MatchTableLineItem_ network_code</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables">MobileCarrier</a></td>
<td>p_MatchTableMobileCarrier_ network_code</td>
<td>MatchTableMobileCarrier_ network_code</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables">MobileDevice</a></td>
<td>p_MatchTableMobileDevice_ network_code</td>
<td>MatchTableMobileDevice_ network_code</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables">MobileDeviceSubmodel</a></td>
<td>p_MatchTableMobileDeviceSubmodel_ network_code</td>
<td>MatchTableMobileDeviceSubmodel_ network_code</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables">OperatingSystem</a></td>
<td>p_MatchTableOperatingSystem_ network_code</td>
<td>MatchTableOperatingSystem_ network_code</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables">OperatingSystemVersion</a></td>
<td>p_MatchTableOperatingSystemVersion_ network_code</td>
<td>MatchTableOperatingSystemVersion_ network_code</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables">Order</a></td>
<td>p_MatchTableOrder_ network_code</td>
<td>MatchTableOrder_ network_code</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables">Placement</a></td>
<td>p_MatchTablePlacement_ network_code</td>
<td>MatchTablePlacement_ network_code</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables">ProgrammaticBuyer</a></td>
<td>p_MatchTableProgrammaticBuyer_ network_code</td>
<td>MatchTableProgrammaticBuyer_ network_code</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables">ProposalRetractionReason</a></td>
<td>p_MatchTableProposalRetractionReason_ network_code</td>
<td>MatchTableProposalRetractionReason_ network_code</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables">ThirdPartyCompany</a></td>
<td>p_MatchTableThirdPartyCompany_ network_code</td>
<td>MatchTableThirdPartyCompany_ network_code</td>
</tr>
<tr class="even">
<td><a href="https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables">TimeZone</a></td>
<td>p_MatchTableTimeZone_ network_code</td>
<td>MatchTableTimeZone_ network_code</td>
</tr>
<tr class="odd">
<td><a href="https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables">User</a></td>
<td>p_MatchTableUser_ network_code</td>
<td>MatchTableUser_ network_code</td>
</tr>
</tbody>
</table>
