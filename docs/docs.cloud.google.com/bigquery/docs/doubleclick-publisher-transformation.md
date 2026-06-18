---
name: documents/docs.cloud.google.com/bigquery/docs/doubleclick-publisher-transformation
uri: https://docs.cloud.google.com/bigquery/docs/doubleclick-publisher-transformation
title: Google Ad Manager report transformation
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# Google Ad Manager report transformation

When your Google Ad Manager (formerly known as DoubleClick for Publishers) data transfer files are transferred to BigQuery, the files are transformed into the BigQuery tables and views described in this document.

When you view the tables and views in BigQuery, the value for network\_code is your Ad Manager network code.

## Data transfer files

The reports in the following sections provide detailed information about your Ad Manager network activity.

### Network requests

Ad Manager files: [NetworkRequests](https://support.google.com/admanager/answer/1733124) and [NetworkBackfillRequests](https://support.google.com/admanager/answer/1733124)

  - BigQuery tables:  
    p\_NetworkRequests\_ network\_code  
    p\_NetworkBackfillRequests\_ network\_code
  - BigQuery views:  
    NetworkRequests\_ network\_code  
    NetworkBackfillRequests\_ network\_code

### Network code serves

Ad Manager files: [NetworkCodeServes](https://support.google.com/admanager/answer/1733124) and [NetworkBackfillCodeServes](https://support.google.com/admanager/answer/1733124)

  - BigQuery tables:  
    p\_NetworkCodeServes  
    p\_NetworkBackfillCodeServes\_ network\_code
  - BigQuery views:  
    NetworkCodeServes  
    NetworkBackfillCodeServes\_ network\_code

### Network impressions

Ad Manager files: [NetworkImpressions](https://support.google.com/admanager/answer/1733124) and [NetworkBackfillImpressions](https://support.google.com/admanager/answer/1733124)

  - BigQuery tables:  
    p\_NetworkImpressions\_ network\_code  
    p\_NetworkBackfillImpressions\_ network\_code
  - BigQuery views:  
    NetworkImpressions\_ network\_code  
    NetworkBackfillImpressions\_ network\_code

### Network clicks

Ad Manager files: [NetworkClicks](https://support.google.com/admanager/answer/1733124) and [NetworkBackfillClicks](https://support.google.com/admanager/answer/1733124)

  - BigQuery tables:  
    p\_NetworkClicks\_ network\_code  
    p\_NetworkBackfillClicks\_ network\_code
  - BigQuery views:  
    NetworkClicks\_ network\_code  
    NetworkBackfillClicks\_ network\_code

### Network active views

Ad Manager files: [NetworkActiveViews](https://support.google.com/admanager/answer/1733124) and [NetworkBackfillActiveViews](https://support.google.com/admanager/answer/1733124)

  - BigQuery tables:  
    p\_NetworkActiveViews\_ network\_code  
    p\_NetworkBackfillActiveViews\_ network\_code
  - BigQuery views:  
    NetworkActiveViews\_ network\_code  
    NetworkBackfillActiveViews\_ network\_code

### Network backfill bids

Ad Manager file: [NetworkBackfillBids](https://support.google.com/admanager/answer/1733124)

  - BigQuery table:  
    p\_NetworkBackfillBids\_ network\_code
  - BigQuery view:  
    NetworkBackfillBids\_ network\_code

### Network video conversions

Ad Manager files: [NetworkVideoConversions](https://support.google.com/admanager/answer/1733124) and [NetworkBackfillVideoConversions](https://support.google.com/admanager/answer/1733124)

  - BigQuery tables:  
    p\_NetworkVideoConversions\_ network\_code  
    p\_NetworkBackfillVideoConversions\_ network\_code
  - BigQuery views:  
    NetworkVideoConversions\_ network\_code  
    NetworkBackfillVideoConversions\_ network\_code

### Network rich media conversions

Ad Manager files: [NetworkRichMediaConversions](https://support.google.com/admanager/answer/1733124) and [NetworkBackfillRichMediaConversions](https://support.google.com/admanager/answer/1733124)

  - BigQuery tables:  
    p\_NetworkRichMediaConversions\_ network\_code  
    p\_NetworkBackfillRichMediaConversions\_ network\_code
  - BigQuery views:  
    NetworkRichMediaConversions\_ network\_code  
    NetworkBackfillRichMediaConversions\_ network\_code

### Network activities

Ad Manager file: [NetworkActivities](https://support.google.com/admanager/answer/1733124)

  - BigQuery table:  
    p\_NetworkActivities\_ network\_code
  - BigQuery view:  
    NetworkActivities\_ network\_code

## Match tables

The tables in the following sections contain attribute fields and metadata for your account.

### Ad category

Ad Manager file: [AdCategory](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

  - BigQuery table:  
    p\_MatchTableAdCategory\_ network\_code
  - BigQuery view:  
    MatchTableAdCategory\_ network\_code

### Ad unit

Ad Manager file: [AdUnit](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

  - BigQuery table:  
    p\_MatchTableAdUnit\_ network\_code
  - BigQuery view:  
    MatchTableAdUnit\_ network\_code

### Audience segment

Ad Manager file: [AudienceSegment](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

  - BigQuery table:  
    p\_MatchTableAudienceSegment\_ network\_code
  - BigQuery view:  
    MatchTableAudienceSegment\_ network\_code

### Audience segment category

Ad Manager file: [AudienceSegmentCategory](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

  - BigQuery table:  
    p\_MatchTableAudienceSegmentCategory\_ network\_code
  - BigQuery view:  
    MatchTableAudienceSegmentCategory\_ network\_code

### Bandwidth group

Ad Manager file: [BandwidthGroup](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

  - BigQuery table:  
    p\_MatchTableBandwidthGroup\_ network\_code
  - BigQuery view:  
    MatchTableBandwidthGroup\_ network\_code

### Browser

Ad Manager file: [Browser](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

  - BigQuery table:  
    p\_MatchTableBrowser\_ network\_code
  - BigQuery view:  
    MatchTableBrowser\_ network\_code

### Browser language

Ad Manager file: [BrowserLanguage](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

  - BigQuery table:  
    p\_MatchTableBrowserLanguage\_ network\_code
  - BigQuery view:  
    MatchTableBrowserLanguage\_ network\_code

### Company

Ad Manager file: [Company](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

  - BigQuery table:  
    p\_MatchTableCompany\_ network\_code
  - BigQuery view:  
    MatchTableCompany\_ network\_code

### Device capability

Ad Manager file: [DeviceCapability](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

  - BigQuery table:  
    p\_MatchTableDeviceCapability\_ network\_code
  - BigQuery view:  
    MatchTableDeviceCapability\_ network\_code

### Device category

Ad Manager file: [DeviceCategory](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

  - BigQuery table:  
    p\_MatchTableDeviceCategory\_ network\_code
  - BigQuery view:  
    MatchTableDeviceCategory\_ network\_code

### Device manufacturer

Ad Manager file: [DeviceManufacturer](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

  - BigQuery table:  
    p\_MatchTableDeviceManufacturer\_ network\_code
  - BigQuery view:  
    MatchTableDeviceManufacturer\_ network\_code

### Exchange rate (deprecated)

Ad Manager file: [ExchangeRate](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

  - BigQuery table:  
    None
  - BigQuery view:  
    None

### Geo target

Ad Manager file: [GeoTarget](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

  - BigQuery table:  
    p\_MatchTableGeoTarget\_ network\_code
  - BigQuery view:  
    MatchTableGeoTarget\_ network\_code

### Line item

Ad Manager file: [LineItem](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

  - BigQuery table:  
    p\_MatchTableLineItem\_ network\_code
  - BigQuery view:  
    MatchTableLineItem\_ network\_code

### Mobile carrier

Ad Manager file: [MobileCarrier](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

  - BigQuery table:  
    p\_MatchTableMobileCarrier\_ network\_code
  - BigQuery view:  
    MatchTableMobileCarrier\_ network\_code

### Mobile device

Ad Manager file: [MobileDevice](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

  - BigQuery table:  
    p\_MatchTableMobileDevice\_ network\_code
  - BigQuery view:  
    MatchTableMobileDevice\_ network\_code

### Mobile device submodel

Ad Manager file: [MobileDeviceSubmodel](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

  - BigQuery table:  
    p\_MatchTableMobileDeviceSubmodel\_ network\_code
  - BigQuery view:  
    MatchTableMobileDeviceSubmodel\_ network\_code

### Operating system

Ad Manager file: [OperatingSystem](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

  - BigQuery table:  
    p\_MatchTableOperatingSystem\_ network\_code
  - BigQuery view:  
    MatchTableOperatingSystem\_ network\_code

### Operating system version

Ad Manager file: [OperatingSystemVersion](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

  - BigQuery table:  
    p\_MatchTableOperatingSystemVersion\_ network\_code
  - BigQuery view:  
    MatchTableOperatingSystemVersion\_ network\_code

### Order

Ad Manager file: [Order](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

  - BigQuery table:  
    p\_MatchTableOrder\_ network\_code
  - BigQuery view:  
    MatchTableOrder\_ network\_code

### Placement

Ad Manager file: [Placement](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

  - BigQuery table:  
    p\_MatchTablePlacement\_ network\_code
  - BigQuery view:  
    MatchTablePlacement\_ network\_code

### Programmatic buyer

Ad Manager file: [ProgrammaticBuyer](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

  - BigQuery table:  
    p\_MatchTableProgrammaticBuyer\_ network\_code
  - BigQuery view:  
    MatchTableProgrammaticBuyer\_ network\_code

### Proposal retraction reason

Ad Manager file: [ProposalRetractionReason](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

  - BigQuery table:  
    p\_MatchTableProposalRetractionReason\_ network\_code
  - BigQuery view:  
    MatchTableProposalRetractionReason\_ network\_code

### Third-party company

Ad Manager file: [ThirdPartyCompany](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

  - BigQuery table:  
    p\_MatchTableThirdPartyCompany\_ network\_code
  - BigQuery view:  
    MatchTableThirdPartyCompany\_ network\_code

### Time zone

Ad Manager file: [TimeZone](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

  - BigQuery table:  
    p\_MatchTableTimeZone\_ network\_code
  - BigQuery view:  
    MatchTableTimeZone\_ network\_code

### User

Ad Manager file: [User](https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables)

  - BigQuery table:  
    p\_MatchTableUser\_ network\_code
  - BigQuery view:  
    MatchTableUser\_ network\_code
