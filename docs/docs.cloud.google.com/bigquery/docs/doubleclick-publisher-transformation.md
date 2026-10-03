---
name: documents/docs.cloud.google.com/bigquery/docs/doubleclick-publisher-transformation
uri: https://docs.cloud.google.com/bigquery/docs/doubleclick-publisher-transformation
title: Google Ad Manager report transformation
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# Google Ad Manager report transformation

When your Google Ad Manager (formerly known as DoubleClick for Publishers) data transfer files are transferred to BigQuery, the files are transformed into the BigQuery tables and views described in this document.

When you view the tables and views in BigQuery, the value for ` network_code ` is your Ad Manager network code.

## Data transfer files

The reports in the following sections provide detailed information about your Ad Manager network activity.

### Network requests

Ad Manager files: [NetworkRequests](https://support.google.com/admanager/answer/1733124) and [NetworkBackfillRequests](https://support.google.com/admanager/answer/1733124)

BigQuery tables:  
p_NetworkRequests\_ ` network_code `  
p_NetworkBackfillRequests\_ ` network_code `

BigQuery views:  
NetworkRequests\_ ` network_code `  
NetworkBackfillRequests\_ ` network_code `

### Network code serves

Ad Manager files: [NetworkCodeServes](https://support.google.com/admanager/answer/1733124) and [NetworkBackfillCodeServes](https://support.google.com/admanager/answer/1733124)

BigQuery tables:  
p_NetworkCodeServes  
p_NetworkBackfillCodeServes\_ ` network_code `

BigQuery views:  
NetworkCodeServes  
NetworkBackfillCodeServes\_ ` network_code `

### Network impressions

Ad Manager files: [NetworkImpressions](https://support.google.com/admanager/answer/1733124) and [NetworkBackfillImpressions](https://support.google.com/admanager/answer/1733124)

BigQuery tables:  
p_NetworkImpressions\_ ` network_code `  
p_NetworkBackfillImpressions\_ ` network_code `

BigQuery views:  
NetworkImpressions\_ ` network_code `  
NetworkBackfillImpressions\_ ` network_code `

### Network clicks

Ad Manager files: [NetworkClicks](https://support.google.com/admanager/answer/1733124) and [NetworkBackfillClicks](https://support.google.com/admanager/answer/1733124)

BigQuery tables:  
p_NetworkClicks\_ ` network_code `  
p_NetworkBackfillClicks\_ ` network_code `

BigQuery views:  
NetworkClicks\_ ` network_code `  
NetworkBackfillClicks\_ ` network_code `

### Network active views

Ad Manager files: [NetworkActiveViews](https://support.google.com/admanager/answer/1733124) and [NetworkBackfillActiveViews](https://support.google.com/admanager/answer/1733124)

BigQuery tables:  
p_NetworkActiveViews\_ ` network_code `  
p_NetworkBackfillActiveViews\_ ` network_code `

BigQuery views:  
NetworkActiveViews\_ ` network_code `  
NetworkBackfillActiveViews\_ ` network_code `

### Network backfill bids

Ad Manager file: [NetworkBackfillBids](https://support.google.com/admanager/answer/1733124)

BigQuery table:  
p_NetworkBackfillBids\_ ` network_code `

BigQuery view:  
NetworkBackfillBids\_ ` network_code `

### Network video conversions

Ad Manager files: [NetworkVideoConversions](https://support.google.com/admanager/answer/1733124) and [NetworkBackfillVideoConversions](https://support.google.com/admanager/answer/1733124)

BigQuery tables:  
p_NetworkVideoConversions\_ ` network_code `  
p_NetworkBackfillVideoConversions\_ ` network_code `

BigQuery views:  
NetworkVideoConversions\_ ` network_code `  
NetworkBackfillVideoConversions\_ ` network_code `

### Network rich media conversions

Ad Manager files: [NetworkRichMediaConversions](https://support.google.com/admanager/answer/1733124) and [NetworkBackfillRichMediaConversions](https://support.google.com/admanager/answer/1733124)

BigQuery tables:  
p_NetworkRichMediaConversions\_ ` network_code `  
p_NetworkBackfillRichMediaConversions\_ ` network_code `

BigQuery views:  
NetworkRichMediaConversions\_ ` network_code `  
NetworkBackfillRichMediaConversions\_ ` network_code `

### Network activities

Ad Manager file: [NetworkActivities](https://support.google.com/admanager/answer/1733124)

BigQuery table:  
p_NetworkActivities\_ ` network_code `

BigQuery view:  
NetworkActivities\_ ` network_code `

## Match tables

The tables in the following sections contain attribute fields and metadata for your account.

### Ad category

Ad Manager file: [AdCategory](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

BigQuery table:  
p_MatchTableAdCategory\_ ` network_code `

BigQuery view:  
MatchTableAdCategory\_ ` network_code `

### Ad unit

Ad Manager file: [AdUnit](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

BigQuery table:  
p_MatchTableAdUnit\_ ` network_code `

BigQuery view:  
MatchTableAdUnit\_ ` network_code `

### Audience segment

Ad Manager file: [AudienceSegment](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

BigQuery table:  
p_MatchTableAudienceSegment\_ ` network_code `

BigQuery view:  
MatchTableAudienceSegment\_ ` network_code `

### Audience segment category

Ad Manager file: [AudienceSegmentCategory](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

BigQuery table:  
p_MatchTableAudienceSegmentCategory\_ ` network_code `

BigQuery view:  
MatchTableAudienceSegmentCategory\_ ` network_code `

### Bandwidth group

Ad Manager file: [BandwidthGroup](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

BigQuery table:  
p_MatchTableBandwidthGroup\_ ` network_code `

BigQuery view:  
MatchTableBandwidthGroup\_ ` network_code `

### Browser

Ad Manager file: [Browser](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

BigQuery table:  
p_MatchTableBrowser\_ ` network_code `

BigQuery view:  
MatchTableBrowser\_ ` network_code `

### Browser language

Ad Manager file: [BrowserLanguage](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

BigQuery table:  
p_MatchTableBrowserLanguage\_ ` network_code `

BigQuery view:  
MatchTableBrowserLanguage\_ ` network_code `

### Company

Ad Manager file: [Company](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

BigQuery table:  
p_MatchTableCompany\_ ` network_code `

BigQuery view:  
MatchTableCompany\_ ` network_code `

### Device capability

Ad Manager file: [DeviceCapability](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

BigQuery table:  
p_MatchTableDeviceCapability\_ ` network_code `

BigQuery view:  
MatchTableDeviceCapability\_ ` network_code `

### Device category

Ad Manager file: [DeviceCategory](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

BigQuery table:  
p_MatchTableDeviceCategory\_ ` network_code `

BigQuery view:  
MatchTableDeviceCategory\_ ` network_code `

### Device manufacturer

Ad Manager file: [DeviceManufacturer](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

BigQuery table:  
p_MatchTableDeviceManufacturer\_ ` network_code `

BigQuery view:  
MatchTableDeviceManufacturer\_ ` network_code `

### Exchange rate (deprecated)

Ad Manager file: [ExchangeRate](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

BigQuery table:  
None

BigQuery view:  
None

### Geo target

Ad Manager file: [GeoTarget](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

BigQuery table:  
p_MatchTableGeoTarget\_ ` network_code `

BigQuery view:  
MatchTableGeoTarget\_ ` network_code `

### Line item

Ad Manager file: [LineItem](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

BigQuery table:  
p_MatchTableLineItem\_ ` network_code `

BigQuery view:  
MatchTableLineItem\_ ` network_code `

### Mobile carrier

Ad Manager file: [MobileCarrier](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

BigQuery table:  
p_MatchTableMobileCarrier\_ ` network_code `

BigQuery view:  
MatchTableMobileCarrier\_ ` network_code `

### Mobile device

Ad Manager file: [MobileDevice](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

BigQuery table:  
p_MatchTableMobileDevice\_ ` network_code `

BigQuery view:  
MatchTableMobileDevice\_ ` network_code `

### Mobile device submodel

Ad Manager file: [MobileDeviceSubmodel](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

BigQuery table:  
p_MatchTableMobileDeviceSubmodel\_ ` network_code `

BigQuery view:  
MatchTableMobileDeviceSubmodel\_ ` network_code `

### Operating system

Ad Manager file: [OperatingSystem](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

BigQuery table:  
p_MatchTableOperatingSystem\_ ` network_code `

BigQuery view:  
MatchTableOperatingSystem\_ ` network_code `

### Operating system version

Ad Manager file: [OperatingSystemVersion](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

BigQuery table:  
p_MatchTableOperatingSystemVersion\_ ` network_code `

BigQuery view:  
MatchTableOperatingSystemVersion\_ ` network_code `

### Order

Ad Manager file: [Order](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

BigQuery table:  
p_MatchTableOrder\_ ` network_code `

BigQuery view:  
MatchTableOrder\_ ` network_code `

### Placement

Ad Manager file: [Placement](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

BigQuery table:  
p_MatchTablePlacement\_ ` network_code `

BigQuery view:  
MatchTablePlacement\_ ` network_code `

### Programmatic buyer

Ad Manager file: [ProgrammaticBuyer](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

BigQuery table:  
p_MatchTableProgrammaticBuyer\_ ` network_code `

BigQuery view:  
MatchTableProgrammaticBuyer\_ ` network_code `

### Proposal retraction reason

Ad Manager file: [ProposalRetractionReason](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

BigQuery table:  
p_MatchTableProposalRetractionReason\_ ` network_code `

BigQuery view:  
MatchTableProposalRetractionReason\_ ` network_code `

### Third-party company

Ad Manager file: [ThirdPartyCompany](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

BigQuery table:  
p_MatchTableThirdPartyCompany\_ ` network_code `

BigQuery view:  
MatchTableThirdPartyCompany\_ ` network_code `

### Time zone

Ad Manager file: [TimeZone](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

BigQuery table:  
p_MatchTableTimeZone\_ ` network_code `

BigQuery view:  
MatchTableTimeZone\_ ` network_code `

### User

Ad Manager file: [User](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

BigQuery table:  
p_MatchTableUser\_ ` network_code `

BigQuery view:  
MatchTableUser\_ ` network_code `
