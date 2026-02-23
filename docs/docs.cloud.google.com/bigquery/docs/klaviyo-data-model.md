# Klaviyo data model reference

This page lists the data that's transferred to BigQuery when you [run a Klaviyo data transfer](/bigquery/docs/klaviyo-transfer) . The data is organized into tables that list each field name, its associated destination data type, and the JSON path from the source data.

## Accounts

Klaviyo account information and metadata.

  - Table name: Accounts
  - Endpoint: `  /accounts  `
  - Klaviyo API reference: [Get Accounts](https://developers.klaviyo.com/en/reference/get_accounts)

<table>
<thead>
<tr class="header">
<th>Field Name</th>
<th>Type</th>
<th>JSON Path</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       type      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.type      </code></td>
<td>Resource type (always <code dir="ltr" translate="no">       account      </code> ).</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       id      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.id      </code></td>
<td>Unique identifier for the account.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       test_account      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.test_account      </code></td>
<td>Indicates if this is a test account.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       default_sender_name      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.contact_information.default_sender_name      </code></td>
<td>Default name used as the sender for emails.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       default_sender_email      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.contact_information.default_sender_email      </code></td>
<td>Default email address used as the sender.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       website_url      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.contact_information.website_url      </code></td>
<td>URL of the organization's website.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       organization_name      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.contact_information.organization_name      </code></td>
<td>Name of the organization.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       address1      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.contact_information.street_address.address1      </code></td>
<td>Street address line 1.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       address2      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.contact_information.street_address.address2      </code></td>
<td>Street address line 2.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       city      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.contact_information.street_address.city      </code></td>
<td>City of the organization.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       region      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.contact_information.street_address.region      </code></td>
<td>State, province, or region.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       country      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.contact_information.street_address.country      </code></td>
<td>Country.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       zip      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.contact_information.street_address.zip      </code></td>
<td>Postal or Zip code.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       industry      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.industry      </code></td>
<td>Industry vertical of the account.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       timezone      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.timezone      </code></td>
<td>Timezone setting for the account.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       preferred_currency      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.preferred_currency      </code></td>
<td>Primary currency used by the account.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       public_api_key      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.public_api_key      </code></td>
<td>Public API key (Site ID) for client-side integrations.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       locale      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.locale      </code></td>
<td>Locale setting (e.g., en-US).</td>
</tr>
</tbody>
</table>

## Coupons

Coupons for discounts and promotions.

  - Table name: Coupons
  - Endpoint: `  /coupons  `
  - Klaviyo API reference: [Get Coupons](https://developers.klaviyo.com/en/reference/get_coupons)

<table>
<thead>
<tr class="header">
<th>Field Name</th>
<th>Type</th>
<th>JSON Path</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       type      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.type      </code></td>
<td>Resource type (always <code dir="ltr" translate="no">       coupon      </code> ).</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       id      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.id      </code></td>
<td>Unique internal identifier for the coupon.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       external_id      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.external_id      </code></td>
<td>External identifier (often the same as name/id).</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       description      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.description      </code></td>
<td>Description of the coupon offer.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       low_balance_threshold      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.monitor_configuration.low_balance_threshold      </code></td>
<td>Threshold to trigger low balance alerts.</td>
</tr>
</tbody>
</table>

## CouponCode

Individual unique codes generated for specific coupons.

  - Table name: CouponCode
  - Endpoint: `  /coupon-codes  `
  - Klaviyo API reference: [Get Coupon Codes](https://developers.klaviyo.com/en/reference/get_coupon_codes)

<table>
<thead>
<tr class="header">
<th>Field Name</th>
<th>Type</th>
<th>JSON Path</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       type      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.type      </code></td>
<td>Resource type (always <code dir="ltr" translate="no">       coupon-code      </code> ).</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       id      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.id      </code></td>
<td>Unique identifier for this specific code instance.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       unique_code      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.unique_code      </code></td>
<td>The actual alphanumeric code string.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       expires_at      </code></td>
<td>TIMESTAMP</td>
<td><code dir="ltr" translate="no">       $.attributes.expires_at      </code></td>
<td>Timestamp when this code expires.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       status      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.status      </code></td>
<td>Status of the code (e.g., ASSIGNED, UNASSIGNED).</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       coupon_id      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.relationships.coupon.data.id      </code></td>
<td>ID of the parent Coupon definition.</td>
</tr>
</tbody>
</table>

## Events

Activity events tracked for profiles (e.g., Placed Order, Viewed Product).

  - Table name: Events
  - Endpoint: `  /events  `
  - Klaviyo API reference: [Get Events](https://developers.klaviyo.com/en/reference/get_events)

<table>
<thead>
<tr class="header">
<th>Field Name</th>
<th>Type</th>
<th>JSON Path</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       type      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.type      </code></td>
<td>Resource type (always <code dir="ltr" translate="no">       event      </code> ).</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       id      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.id      </code></td>
<td>Unique identifier for the event.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       timestamp      </code></td>
<td>FLOAT</td>
<td><code dir="ltr" translate="no">       $.attributes.timestamp      </code></td>
<td>Unix timestamp of when the event occurred.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       event_properties      </code></td>
<td>JSON</td>
<td><code dir="ltr" translate="no">       $.attributes.event_properties      </code></td>
<td>Custom JSON properties specific to the event type (e.g., items in order).</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       datetime      </code></td>
<td>TIMESTAMP</td>
<td><code dir="ltr" translate="no">       $.attributes.datetime      </code></td>
<td>ISO 8601 timestamp of the event.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       uuid      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.uuid      </code></td>
<td>Universally Unique Identifier for the event.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       profile_id      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.relationships.profile.data.id      </code></td>
<td>ID of the profile (customer) associated with the event.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       metric_id      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.relationships.metric.data.id      </code></td>
<td>ID of the metric (event type) definition.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       attribution_ids      </code></td>
<td>REPEATED STRING</td>
<td><code dir="ltr" translate="no">       $.relationships.attributions.data[*].id      </code></td>
<td>IDs of campaigns/flows attributed to this event.</td>
</tr>
</tbody>
</table>

## Flows

Automated marketing flows triggered by specific events or conditions.

  - Table name: Flows
  - Endpoint: `  /flows  `
  - Klaviyo API reference: [Get Flows](https://developers.klaviyo.com/en/reference/get_flows)

<table>
<thead>
<tr class="header">
<th>Field Name</th>
<th>Type</th>
<th>JSON Path</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       type      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.type      </code></td>
<td>Resource type (always <code dir="ltr" translate="no">       flow      </code> ).</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       id      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.id      </code></td>
<td>Unique identifier for the flow.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       name      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.name      </code></td>
<td>Name of the flow.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       status      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.status      </code></td>
<td>Operational status (e.g., live, draft).</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       archived      </code></td>
<td>BOOLEAN</td>
<td><code dir="ltr" translate="no">       $.attributes.archived      </code></td>
<td>Whether the flow is archived.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       created      </code></td>
<td>TIMESTAMP</td>
<td><code dir="ltr" translate="no">       $.attributes.created      </code></td>
<td>Creation timestamp.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       updated      </code></td>
<td>TIMESTAMP</td>
<td><code dir="ltr" translate="no">       $.attributes.updated      </code></td>
<td>Last modification timestamp.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       trigger_type      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.trigger_type      </code></td>
<td>Mechanism triggering the flow (e.g., "Added to List", "Metric").</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       flow_actions_ids      </code></td>
<td>REPEATED STRING</td>
<td><code dir="ltr" translate="no">       $.relationships.flow-actions.data[*].id      </code></td>
<td>IDs of the actions (steps) within this flow.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       tag_ids      </code></td>
<td>REPEATED STRING</td>
<td><code dir="ltr" translate="no">       $.relationships.tags.data[*].id      </code></td>
<td>IDs of tags assigned to this flow.</td>
</tr>
</tbody>
</table>

## Forms

Signup forms for collecting subscriber information.

  - Table name: Forms
  - Endpoint: `  /forms  `
  - Klaviyo API reference: [Get Forms](https://developers.klaviyo.com/en/reference/get_forms)

<table>
<thead>
<tr class="header">
<th>Field Name</th>
<th>Type</th>
<th>JSON Path</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       type      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.type      </code></td>
<td>Resource type (always <code dir="ltr" translate="no">       form      </code> ).</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       id      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.id      </code></td>
<td>Unique identifier for the form.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       name      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.name      </code></td>
<td>Name of the form.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       status      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.status      </code></td>
<td>Status of the form (e.g., live, draft).</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       ab_test      </code></td>
<td>BOOLEAN</td>
<td><code dir="ltr" translate="no">       $.attributes.ab_test      </code></td>
<td>Whether the form is running an A/B test.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       created_at      </code></td>
<td>TIMESTAMP</td>
<td><code dir="ltr" translate="no">       $.attributes.created_at      </code></td>
<td>Creation timestamp.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       updated_at      </code></td>
<td>TIMESTAMP</td>
<td><code dir="ltr" translate="no">       $.attributes.updated_at      </code></td>
<td>Last modification timestamp.</td>
</tr>
</tbody>
</table>

## Images

Images uploaded to Klaviyo for use in campaigns and templates.

  - Table name: Images
  - Endpoint: `  /images  `
  - Klaviyo API reference: [Get Images](https://developers.klaviyo.com/en/reference/get_images)

<table>
<thead>
<tr class="header">
<th>Field Name</th>
<th>Type</th>
<th>JSON Path</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       type      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.type      </code></td>
<td>Resource type (always <code dir="ltr" translate="no">       image      </code> ).</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       id      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.id      </code></td>
<td>Unique identifier.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       name      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.name      </code></td>
<td>Filename or name of the image.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       image_url      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.image_url      </code></td>
<td>Public URL to access the image.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       format      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.format      </code></td>
<td>Image file format (e.g., jpeg, png).</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       size      </code></td>
<td>FLOAT</td>
<td><code dir="ltr" translate="no">       $.attributes.size      </code></td>
<td>File size in bytes.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       hidden      </code></td>
<td>BOOLEAN</td>
<td><code dir="ltr" translate="no">       $.attributes.hidden      </code></td>
<td>Whether the image is hidden in the UI.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       updated_at      </code></td>
<td>TIMESTAMP</td>
<td><code dir="ltr" translate="no">       $.attributes.updated_at      </code></td>
<td>Last modification timestamp.</td>
</tr>
</tbody>
</table>

## Lists

Static lists of contacts/profiles.

  - Table name: Lists
  - Endpoint: `  /lists  `
  - Klaviyo API reference: [Get Lists](https://developers.klaviyo.com/en/reference/get_lists)

<table>
<thead>
<tr class="header">
<th>Field Name</th>
<th>Type</th>
<th>JSON Path</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       type      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.type      </code></td>
<td>Resource type (always <code dir="ltr" translate="no">       list      </code> ).</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       id      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.id      </code></td>
<td>Unique identifier for the list.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       name      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.name      </code></td>
<td>Name of the contact list.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       created      </code></td>
<td>TIMESTAMP</td>
<td><code dir="ltr" translate="no">       $.attributes.created      </code></td>
<td>Creation timestamp.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       updated      </code></td>
<td>TIMESTAMP</td>
<td><code dir="ltr" translate="no">       $.attributes.updated      </code></td>
<td>Last modification timestamp.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       opt_in_process      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.opt_in_process      </code></td>
<td>Opt-in setting (e.g., 'single_opt_in' or 'double_opt_in').</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       tag_ids      </code></td>
<td>REPEATED STRING</td>
<td><code dir="ltr" translate="no">       $.relationships.tags.data[*].id      </code></td>
<td>IDs of tags assigned to this list.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       flow_triggers_ids      </code></td>
<td>REPEATED STRING</td>
<td><code dir="ltr" translate="no">       $.relationships.flow-triggers.data[*].id      </code></td>
<td>IDs of flows triggered by adding profiles to this list.</td>
</tr>
</tbody>
</table>

## Metrics

Types of events that can be tracked (e.g., "Received Email").

  - Table name: Metrics
  - Endpoint: `  /metrics  `
  - Klaviyo API reference: [Get Metrics](https://developers.klaviyo.com/en/reference/get_metrics)

<table>
<thead>
<tr class="header">
<th>Field Name</th>
<th>Type</th>
<th>JSON Path</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       type      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.type      </code></td>
<td>Resource type (always <code dir="ltr" translate="no">       metric      </code> ).</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       id      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.id      </code></td>
<td>Unique identifier (e.g., 6-char code for generic, long UUID for custom).</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       name      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.name      </code></td>
<td>Human-readable name (e.g., "Placed Order").</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       created      </code></td>
<td>TIMESTAMP</td>
<td><code dir="ltr" translate="no">       $.attributes.created      </code></td>
<td>Creation timestamp.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       updated      </code></td>
<td>TIMESTAMP</td>
<td><code dir="ltr" translate="no">       $.attributes.updated      </code></td>
<td>Last modification timestamp.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       integration      </code></td>
<td>JSON</td>
<td><code dir="ltr" translate="no">       $.attributes.integration      </code></td>
<td>Info about the integration providing this metric (e.g., name, category, image).</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       flow_triggers_ids      </code></td>
<td>REPEATED STRING</td>
<td><code dir="ltr" translate="no">       $.relationships.flow-triggers.data[*].id      </code></td>
<td>IDs of flows triggered by this metric.</td>
</tr>
</tbody>
</table>

## Profiles

Comprehensive customer profiles containing attributes and activity history.

  - Table name: Profiles
  - Endpoint: `  /profiles  `
  - Klaviyo API reference: [Get Profiles](https://developers.klaviyo.com/en/reference/get_profiles)

<table>
<thead>
<tr class="header">
<th>Field Name</th>
<th>Type</th>
<th>JSON Path</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       type      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.type      </code></td>
<td>Resource type (always <code dir="ltr" translate="no">       profile      </code> ).</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       id      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.id      </code></td>
<td>Unique Klaviyo ID for the profile.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       email      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.email      </code></td>
<td>Primary email address.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       phone_number      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.phone_number      </code></td>
<td>Phone number in E.164 format.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       external_id      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.external_id      </code></td>
<td>ID from an external system.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       first_name      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.first_name      </code></td>
<td>First name.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       last_name      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.last_name      </code></td>
<td>Last name.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       organization      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.organization      </code></td>
<td>Company or organization name.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       locale      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.locale      </code></td>
<td>Locale/Language setting.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       title      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.title      </code></td>
<td>Job title.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       image      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.image      </code></td>
<td>Profile image URL.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       created      </code></td>
<td>TIMESTAMP</td>
<td><code dir="ltr" translate="no">       $.attributes.created      </code></td>
<td>Profile creation timestamp.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       updated      </code></td>
<td>TIMESTAMP</td>
<td><code dir="ltr" translate="no">       $.attributes.updated      </code></td>
<td>Last update timestamp.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       last_event_date      </code></td>
<td>TIMESTAMP</td>
<td><code dir="ltr" translate="no">       $.attributes.last_event_date      </code></td>
<td>Timestamp of the most recent event.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       address1      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.location.address1      </code></td>
<td>Address line 1.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       address2      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.location.address2      </code></td>
<td>Address line 2.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       city      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.location.city      </code></td>
<td>City.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       country      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.location.country      </code></td>
<td>Country.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       latitude      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.location.latitude      </code></td>
<td>Latitude coordinates.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       longitude      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.location.longitude      </code></td>
<td>Longitude coordinates.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       region      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.location.region      </code></td>
<td>State or region.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       zip      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.location.zip      </code></td>
<td>Postal or Zip code.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       timezone      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.location.timezone      </code></td>
<td>Timezone.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ip      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.location.ip      </code></td>
<td>IP address.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       properties      </code></td>
<td>JSON</td>
<td><code dir="ltr" translate="no">       $.attributes.properties      </code></td>
<td>Custom properties key-value pairs.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       email_marketing_can_receive_email_marketing      </code></td>
<td>BOOLEAN</td>
<td><code dir="ltr" translate="no">       $.attributes.subscriptions.email.marketing.can_receive_email_marketing      </code></td>
<td>Whether profile can receive email marketing.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       email_marketing_consent      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.subscriptions.email.marketing.consent      </code></td>
<td>Consent status (e.g., SUBSCRIBED, UNSUBSCRIBED).</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       email_marketing_consent_timestamp      </code></td>
<td>TIMESTAMP</td>
<td><code dir="ltr" translate="no">       $.attributes.subscriptions.email.marketing.consent_timestamp      </code></td>
<td>When consent was given.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       email_marketing_last_updated      </code></td>
<td>TIMESTAMP</td>
<td><code dir="ltr" translate="no">       $.attributes.subscriptions.email.marketing.last_updated      </code></td>
<td>When email consent was last updated.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       email_marketing_method      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.subscriptions.email.marketing.method      </code></td>
<td>Method of consent (e.g., FORM).</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       email_marketing_method_detail      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.subscriptions.email.marketing.method_detail      </code></td>
<td>Specific source of method.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       email_marketing_custom_method_detail      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.subscriptions.email.marketing.custom_method_detail      </code></td>
<td>Custom details for consent method.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       email_marketing_double_optin      </code></td>
<td>BOOLEAN</td>
<td><code dir="ltr" translate="no">       $.attributes.subscriptions.email.marketing.double_optin      </code></td>
<td>Whether double opt-in was completed.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       sms_marketing_can_receive_sms_marketing      </code></td>
<td>BOOLEAN</td>
<td><code dir="ltr" translate="no">       $.attributes.subscriptions.sms.marketing.can_receive_sms_marketing      </code></td>
<td>Whether profile can receive SMS marketing.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       sms_marketing_consent      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.subscriptions.sms.marketing.consent      </code></td>
<td>SMS consent status.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       sms_marketing_consent_timestamp      </code></td>
<td>TIMESTAMP</td>
<td><code dir="ltr" translate="no">       $.attributes.subscriptions.sms.marketing.consent_timestamp      </code></td>
<td>When SMS consent was given.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       sms_marketing_last_updated      </code></td>
<td>TIMESTAMP</td>
<td><code dir="ltr" translate="no">       $.attributes.subscriptions.sms.marketing.last_updated      </code></td>
<td>When SMS consent was last updated.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       sms_marketing_method      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.subscriptions.sms.marketing.method      </code></td>
<td>SMS consent method.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       sms_marketing_method_detail      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.subscriptions.sms.marketing.method_detail      </code></td>
<td>Details of SMS consent method.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       sms_transactional_can_receive_sms_transactional      </code></td>
<td>BOOLEAN</td>
<td><code dir="ltr" translate="no">       $.attributes.subscriptions.sms.transactional.can_receive_sms_transactional      </code></td>
<td>Whether profile can receive transactional SMS.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       sms_transactional_consent      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.subscriptions.sms.transactional.consent      </code></td>
<td>Transactional SMS consent status.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       sms_transactional_consent_timestamp      </code></td>
<td>TIMESTAMP</td>
<td><code dir="ltr" translate="no">       $.attributes.subscriptions.sms.transactional.consent_timestamp      </code></td>
<td>When transactional consent was given.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       sms_transactional_last_updated      </code></td>
<td>TIMESTAMP</td>
<td><code dir="ltr" translate="no">       $.attributes.subscriptions.sms.transactional.last_updated      </code></td>
<td>When transactional status was last updated.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       sms_transactional_method      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.subscriptions.sms.transactional.method      </code></td>
<td>Transactional SMS method.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       sms_transactional_method_detail      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.subscriptions.sms.transactional.method_detail      </code></td>
<td>Transactional SMS method detail.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       mobile_push_can_receive_push_marketing      </code></td>
<td>BOOLEAN</td>
<td><code dir="ltr" translate="no">       $.attributes.subscriptions.mobile_push.marketing.can_receive_push_marketing      </code></td>
<td>Whether profile can receive push marketing.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       mobile_push_consent      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.subscriptions.mobile_push.marketing.consent      </code></td>
<td>Push consent status.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       mobile_push_consent_timestamp      </code></td>
<td>TIMESTAMP</td>
<td><code dir="ltr" translate="no">       $.attributes.subscriptions.mobile_push.marketing.consent_timestamp      </code></td>
<td>When push consent was given.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       predictive_analytics_historic_number_of_orders      </code></td>
<td>FLOAT</td>
<td><code dir="ltr" translate="no">       $.attributes.predictive_analytics.historic_number_of_orders      </code></td>
<td>Total historical orders.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       predictive_analytics_predicted_number_of_orders      </code></td>
<td>FLOAT</td>
<td><code dir="ltr" translate="no">       $.attributes.predictive_analytics.predicted_number_of_orders      </code></td>
<td>Predicted future orders.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       predictive_analytics_average_days_between_orders      </code></td>
<td>FLOAT</td>
<td><code dir="ltr" translate="no">       $.attributes.predictive_analytics.average_days_between_orders      </code></td>
<td>Avg days between orders.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       predictive_analytics_average_order_value      </code></td>
<td>FLOAT</td>
<td><code dir="ltr" translate="no">       $.attributes.predictive_analytics.average_order_value      </code></td>
<td>Historic average order value.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       predictive_analytics_historic_clv      </code></td>
<td>FLOAT</td>
<td><code dir="ltr" translate="no">       $.attributes.predictive_analytics.historic_clv      </code></td>
<td>Historic Customer Lifetime Value.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       predictive_analytics_predicted_clv      </code></td>
<td>FLOAT</td>
<td><code dir="ltr" translate="no">       $.attributes.predictive_analytics.predicted_clv      </code></td>
<td>Predicted Customer Lifetime Value.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       predictive_analytics_total_clv      </code></td>
<td>FLOAT</td>
<td><code dir="ltr" translate="no">       $.attributes.predictive_analytics.total_clv      </code></td>
<td>Historic + Predicted CLV.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       predictive_analytics_churn_probability      </code></td>
<td>FLOAT</td>
<td><code dir="ltr" translate="no">       $.attributes.predictive_analytics.churn_probability      </code></td>
<td>Probability of churn (0-1).</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       predictive_analytics_expected_date_of_next_order      </code></td>
<td>TIMESTAMP</td>
<td><code dir="ltr" translate="no">       $.attributes.predictive_analytics.expected_date_of_next_order      </code></td>
<td>Predicted date of next order.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       email_marketing_suppression_reason      </code></td>
<td>REPEATED JSON</td>
<td><code dir="ltr" translate="no">       $.attributes.subscriptions.email.marketing.suppression[*      </code> ]</td>
<td>Reasons for email suppression (e.g., bounced).</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       email_marketing_list_suppressions_reason      </code></td>
<td>REPEATED JSON</td>
<td><code dir="ltr" translate="no">       $.attributes.subscriptions.email.marketing.list_suppressions[*      </code> ]</td>
<td>List-specific suppression reasons.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       push_tokens_ids      </code></td>
<td>REPEATED STRING</td>
<td><code dir="ltr" translate="no">       $.relationships.push-tokens.data[*].id      </code></td>
<td>Associated push token IDs.</td>
</tr>
</tbody>
</table>

## Reviews

Product reviews submitted by customers.

  - Table name: Reviews
  - Endpoint: `  /reviews  `
  - Klaviyo API reference: [Get Reviews](https://developers.klaviyo.com/en/reference/get_reviews)

<table>
<thead>
<tr class="header">
<th>Field Name</th>
<th>Type</th>
<th>JSON Path</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       type      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.type      </code></td>
<td>Resource type (always <code dir="ltr" translate="no">       review      </code> ).</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       id      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.id      </code></td>
<td>Unique identifier for the review.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       email      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.email      </code></td>
<td>Email of the reviewer.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       value      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.status.value      </code></td>
<td>Status value (e.g., published, rejected).</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       reason      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.status.rejection_reason.reason      </code></td>
<td>Reason for rejection if applicable.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       status_explanation      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.status.rejection_reason.status_explanation      </code></td>
<td>Detailed explanation of status.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       verified      </code></td>
<td>BOOLEAN</td>
<td><code dir="ltr" translate="no">       $.attributes.verified      </code></td>
<td>Whether the purchase was verified.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       review_type      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.review_type      </code></td>
<td>Type of review (e.g., product review).</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       created      </code></td>
<td>TIMESTAMP</td>
<td><code dir="ltr" translate="no">       $.attributes.created      </code></td>
<td>Creation timestamp.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       updated      </code></td>
<td>TIMESTAMP</td>
<td><code dir="ltr" translate="no">       $.attributes.updated      </code></td>
<td>Last modification timestamp.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       images      </code></td>
<td>REPEATED STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.images[*      </code> ]</td>
<td>URLs of images attached to the review.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       product_url      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.product.url      </code></td>
<td>URL of the reviewed product.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       product_name      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.product.name      </code></td>
<td>Name of the product.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       product_image_url      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.product.image_url      </code></td>
<td>Image URL of the product.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       product_external_id      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.product.external_id      </code></td>
<td>External ID of the product.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       rating      </code></td>
<td>INTEGER</td>
<td><code dir="ltr" translate="no">       $.attributes.rating      </code></td>
<td>Rating score.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       author      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.author      </code></td>
<td>Name of the reviewer.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       content      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.content      </code></td>
<td>Text content of the review.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       title      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.title      </code></td>
<td>Title of the review.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       smart_quote      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.smart_quote      </code></td>
<td>Highlighted quote from the review.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       public_reply_content      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.public_reply.content      </code></td>
<td>Content of the merchant's public reply.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       public_reply_author      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.public_reply.author      </code></td>
<td>Author of the reply.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       public_reply_updated      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.public_reply.updated      </code></td>
<td>Timestamp of reply update.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       event_ids      </code></td>
<td>REPEATED STRING</td>
<td><code dir="ltr" translate="no">       $.relationships.events.data[*].id      </code></td>
<td>Associated event IDs.</td>
</tr>
</tbody>
</table>

## Segments

Dynamic groups of profiles based on specific criteria.

  - Table name: Segments
  - Endpoint: `  /segments  `
  - Klaviyo API reference: [Get Segments](https://developers.klaviyo.com/en/reference/get_segments)

<table>
<thead>
<tr class="header">
<th>Field Name</th>
<th>Type</th>
<th>JSON Path</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       type      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.type      </code></td>
<td>Resource type (always <code dir="ltr" translate="no">       segment      </code> ).</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       id      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.id      </code></td>
<td>Unique identifier for the segment.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       name      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.name      </code></td>
<td>Segment name.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       created      </code></td>
<td>TIMESTAMP</td>
<td><code dir="ltr" translate="no">       $.attributes.created      </code></td>
<td>Creation timestamp.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       updated      </code></td>
<td>TIMESTAMP</td>
<td><code dir="ltr" translate="no">       $.attributes.updated      </code></td>
<td>Last modification timestamp.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       is_active      </code></td>
<td>BOOLEAN</td>
<td><code dir="ltr" translate="no">       $.attributes.is_active      </code></td>
<td>Whether the segment is active.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       is_processing      </code></td>
<td>BOOLEAN</td>
<td><code dir="ltr" translate="no">       $.attributes.is_processing      </code></td>
<td>Whether the segment is being processed.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       is_starred      </code></td>
<td>BOOLEAN</td>
<td><code dir="ltr" translate="no">       $.attributes.is_starred      </code></td>
<td>Whether the segment is starred/favorited.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       tag_ids      </code></td>
<td>REPEATED STRING</td>
<td><code dir="ltr" translate="no">       $.relationships.tags.data[*].id      </code></td>
<td>IDs of associated tags.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       flow_triggers_ids      </code></td>
<td>REPEATED STRING</td>
<td><code dir="ltr" translate="no">       $.relationships.flow-triggers.data[*].id      </code></td>
<td>IDs of flows triggered by this segment.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       condition_groups      </code></td>
<td>REPEATED RECORD</td>
<td><code dir="ltr" translate="no">       $.attributes.definition.condition_groups[*      </code> ]</td>
<td>Groups of logic conditions defining the segment.</td>
</tr>
</tbody>
</table>

### ConditionGroup

<table>
<thead>
<tr class="header">
<th>Field Name</th>
<th>Type</th>
<th>JSON Path</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       conditions      </code></td>
<td>REPEATED Condition</td>
<td><code dir="ltr" translate="no">       conditions[*      </code> ]</td>
<td>List of individual conditions within the group.</td>
</tr>
</tbody>
</table>

#### Condition

<table>
<thead>
<tr class="header">
<th>Field Name</th>
<th>Type</th>
<th>JSON Path</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       type      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       type      </code></td>
<td>Type of condition (e.g., profile-property).</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       value      </code></td>
<td>JSON</td>
<td><code dir="ltr" translate="no">       N/A      </code></td>
<td>Condition value/configuration.</td>
</tr>
</tbody>
</table>

## Tags

Tags used to organize campaigns, flows, and lists.

  - Table name: Tags
  - Endpoint: `  /tags  `
  - Klaviyo API reference: [Get Tags](https://developers.klaviyo.com/en/reference/get_tags)

<table>
<thead>
<tr class="header">
<th>Field Name</th>
<th>Type</th>
<th>JSON Path</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       type      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.type      </code></td>
<td>Resource type (always <code dir="ltr" translate="no">       tag      </code> ).</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       id      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.id      </code></td>
<td>Unique tag identifier.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       name      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.name      </code></td>
<td>Name of the tag.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       tag_group_id      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.relationships.tag-group.data.id      </code></td>
<td>ID of the tag group this tag belongs to.</td>
</tr>
</tbody>
</table>

## Templates

Email and message templates.

  - Table name: Templates
  - Endpoint: `  /templates  `
  - Klaviyo API reference: [Get Templates](https://developers.klaviyo.com/en/reference/get_templates)

<table>
<thead>
<tr class="header">
<th>Field Name</th>
<th>Type</th>
<th>JSON Path</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       type      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.type      </code></td>
<td>Resource type (always <code dir="ltr" translate="no">       template      </code> ).</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       id      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.id      </code></td>
<td>Unique identifier.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       name      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.name      </code></td>
<td>Template name.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       editor_type      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.editor_type      </code></td>
<td>Editor used (e.g., drag-and-drop).</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       html      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.html      </code></td>
<td>HTML content</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       text      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.text      </code></td>
<td>Text version of the template.</td>
</tr>
<tr class="odd">
<td>amp</td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.amp      </code></td>
<td>AMP version of the template.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       created      </code></td>
<td>TIMESTAMP</td>
<td><code dir="ltr" translate="no">       $.attributes.created      </code></td>
<td>Creation timestamp.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       updated      </code></td>
<td>TIMESTAMP</td>
<td><code dir="ltr" translate="no">       $.attributes.updated      </code></td>
<td>Last update timestamp.</td>
</tr>
</tbody>
</table>

## WebFeeds

Web feeds used to populate content in messages.

  - Table name: WebFeeds
  - Endpoint: `  /web-feeds  `
  - Klaviyo API reference: [Get Web Feeds](https://developers.klaviyo.com/en/reference/get_web_feeds)

<table>
<thead>
<tr class="header">
<th>Field Name</th>
<th>Type</th>
<th>JSON Path</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       type      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.type      </code></td>
<td>Resource type (always <code dir="ltr" translate="no">       web-feed      </code> ).</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       id      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.id      </code></td>
<td>Unique identifier.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       name      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.name      </code></td>
<td>Feed name.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       url      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.url      </code></td>
<td>Feed Source URL.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       request_method      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.request_method      </code></td>
<td>HTTP method (GET/POST).</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       content_type      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.content_type      </code></td>
<td>Content type (e.g., JSON).</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       status      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.status      </code></td>
<td>Status of the feed.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       created      </code></td>
<td>TIMESTAMP</td>
<td><code dir="ltr" translate="no">       $.attributes.created      </code></td>
<td>Creation timestamp.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       updated      </code></td>
<td>TIMESTAMP</td>
<td><code dir="ltr" translate="no">       $.attributes.updated      </code></td>
<td>Last update timestamp.</td>
</tr>
</tbody>
</table>

## DataSources

Sources of data integrated into Klaviyo.

  - Table name: DataSources
  - Endpoint: `  /data-sources  `
  - Klaviyo API reference: [Get Data Sources](https://developers.klaviyo.com/en/reference/get_data_sources)

<table>
<thead>
<tr class="header">
<th>Field Name</th>
<th>Type</th>
<th>JSON Path</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       type      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.type      </code></td>
<td>Resource type (always <code dir="ltr" translate="no">       data-source      </code> ).</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       id      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.id      </code></td>
<td>Unique identifier.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       title      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.title      </code></td>
<td>Title of the data source.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       visibility      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.visibility      </code></td>
<td>Visibility level.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       description      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.description      </code></td>
<td>Description text.</td>
</tr>
</tbody>
</table>

## Campaigns

Marketing campaigns sent to lists or segments.

  - Table name: Campaigns
  - Endpoint: `  /campaigns  `
  - Klaviyo API reference: [Get Campaigns](https://developers.klaviyo.com/en/reference/get_campaigns)

<table>
<thead>
<tr class="header">
<th>Field Name</th>
<th>Type</th>
<th>JSON Path</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       type      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.type      </code></td>
<td>Resource type (always <code dir="ltr" translate="no">       campaign      </code> ).</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       id      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.id      </code></td>
<td>Unique identifier.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       name      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.name      </code></td>
<td>Campaign name.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       status      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.status      </code></td>
<td>Campaign status (e.g., Sent, Scheduling).</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       archived      </code></td>
<td>BOOLEAN</td>
<td><code dir="ltr" translate="no">       $.attributes.archived      </code></td>
<td>Whether campaign is archived.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       included      </code></td>
<td>REPEATED STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.audiences.included      </code></td>
<td>IDs of included lists/segments.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       excluded      </code></td>
<td>REPEATED STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.audiences.excluded      </code></td>
<td>IDs of excluded lists/segments.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       send_options      </code></td>
<td>JSON</td>
<td><code dir="ltr" translate="no">       $.attributes.send_options      </code></td>
<td>Configuration for sending (e.g., smart sending).</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       tracking_options      </code></td>
<td>JSON</td>
<td><code dir="ltr" translate="no">       $.attributes.tracking_options      </code></td>
<td>Configuration for tracking (e.g., utm params).</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       send_strategy      </code></td>
<td>JSON</td>
<td><code dir="ltr" translate="no">       $.attributes.send_strategy      </code></td>
<td>Strategy for delivery time.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       created_at      </code></td>
<td>TIMESTAMP</td>
<td><code dir="ltr" translate="no">       $.attributes.created_at      </code></td>
<td>Creation timestamp.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       scheduled_at      </code></td>
<td>TIMESTAMP</td>
<td><code dir="ltr" translate="no">       $.attributes.scheduled_at      </code></td>
<td>When the campaign is scheduled to send.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       updated_at      </code></td>
<td>TIMESTAMP</td>
<td><code dir="ltr" translate="no">       $.attributes.updated_at      </code></td>
<td>Last update timestamp.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       send_time      </code></td>
<td>TIMESTAMP</td>
<td><code dir="ltr" translate="no">       $.attributes.send_time      </code></td>
<td>Actual time sent.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       tag_ids      </code></td>
<td>REPEATED STRING</td>
<td><code dir="ltr" translate="no">       $.relationships.tags.data[*].id      </code></td>
<td>IDs of associated tags.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       campaign_message_ids      </code></td>
<td>REPEATED STRING</td>
<td><code dir="ltr" translate="no">       $.relationships.campaign-messages.data[*].id      </code></td>
<td>IDs of messages contained in this campaign.</td>
</tr>
</tbody>
</table>

## CampaignMessages

Individual messages (email/SMS) within a campaign.

  - Table name: CampaignMessages
  - Endpoint: `  /campaign-messages  `
  - Klaviyo API reference: [Get Campaign Message](https://developers.klaviyo.com/en/reference/get_campaign_message)

<table>
<thead>
<tr class="header">
<th>Field Name</th>
<th>Type</th>
<th>JSON Path</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       type      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.type      </code></td>
<td>Resource type (always <code dir="ltr" translate="no">       campaign-message      </code> ).</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       id      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.id      </code></td>
<td>Unique identifier.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       definition      </code></td>
<td>JSON</td>
<td><code dir="ltr" translate="no">       $.attributes.definition      </code></td>
<td>Message content and configuration.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       send_times      </code></td>
<td>REPEATED JSON</td>
<td><code dir="ltr" translate="no">       $.attributes.send_times[*      </code> ]</td>
<td>Scheduled send times.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       created_at      </code></td>
<td>TIMESTAMP</td>
<td><code dir="ltr" translate="no">       $.attributes.created_at      </code></td>
<td>Creation timestamp.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       updated_at      </code></td>
<td>TIMESTAMP</td>
<td><code dir="ltr" translate="no">       $.attributes.updated_at      </code></td>
<td>Last update timestamp.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       campaign_id      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.relationships.campaign.data.id      </code></td>
<td>ID of parent campaign.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       template_id      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.relationships.template.data.id      </code></td>
<td>ID of used template.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       image_id      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.relationships.image.data.id      </code></td>
<td>ID of attached image.</td>
</tr>
</tbody>
</table>

## Categories

Product categories from your catalog.

  - Table name: Categories
  - Endpoint: `  /catalog-categories  `
  - Klaviyo API reference: [Get Catalog Categories](https://developers.klaviyo.com/en/reference/get_catalog_categories)

<table>
<thead>
<tr class="header">
<th>Field Name</th>
<th>Type</th>
<th>JSON Path</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       type      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.type      </code></td>
<td>Resource type.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       id      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.id      </code></td>
<td>Unique identifier.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       name      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.name      </code></td>
<td>Category name.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       external_id      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.external_id      </code></td>
<td>External system ID.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       updated      </code></td>
<td>TIMESTAMP</td>
<td><code dir="ltr" translate="no">       $.attributes.updated      </code></td>
<td>Last update timestamp.</td>
</tr>
</tbody>
</table>

## Items

Individual products or items in your catalog.

  - Table name: Items
  - Endpoint: `  /catalog-items  `
  - Klaviyo API reference: [Get Catalog Items](https://developers.klaviyo.com/en/reference/get_catalog_items)

<table>
<thead>
<tr class="header">
<th>Field Name</th>
<th>Type</th>
<th>JSON Path</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       type      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.type      </code></td>
<td>Resource type.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       id      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.id      </code></td>
<td>Unique identifier.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       external_id      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.external_id      </code></td>
<td>External system ID.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       title      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.title      </code></td>
<td>Item title/name.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       description      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.description      </code></td>
<td>Description available.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       price      </code></td>
<td>FLOAT</td>
<td><code dir="ltr" translate="no">       $.attributes.price      </code></td>
<td>Price of the item.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       url      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.url      </code></td>
<td>URL to the item.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       image_full_url      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.image_full_url      </code></td>
<td>URL of full-size image.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       image_thumbnail_url      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.image_thumbnail_url      </code></td>
<td>URL of thumbnail image.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       images      </code></td>
<td>REPEATED STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.images[*      </code> ]</td>
<td>List of additional image URLs.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       custom_metadata      </code></td>
<td>JSON</td>
<td><code dir="ltr" translate="no">       $.attributes.custom_metadata      </code></td>
<td>Custom metadata key-values.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       published      </code></td>
<td>BOOLEAN</td>
<td><code dir="ltr" translate="no">       $.attributes.published      </code></td>
<td>Publication status.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       created      </code></td>
<td>TIMESTAMP</td>
<td><code dir="ltr" translate="no">       $.attributes.created      </code></td>
<td>Creation timestamp.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       updated      </code></td>
<td>TIMESTAMP</td>
<td><code dir="ltr" translate="no">       $.attributes.updated      </code></td>
<td>Last update timestamp.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       variants_ids      </code></td>
<td>REPEATED STRING</td>
<td><code dir="ltr" translate="no">       $.relationships.variants.data[*].id      </code></td>
<td>IDs of variants for this item.</td>
</tr>
</tbody>
</table>

## Variants

Specific variants of catalog items (e.g., sizes, colors).

  - Table name: Variants
  - Endpoint: `  /catalog-variants  `
  - Klaviyo API reference: [Get Catalog Variants](https://developers.klaviyo.com/en/reference/get_catalog_variants)

<table>
<thead>
<tr class="header">
<th>Field Name</th>
<th>Type</th>
<th>JSON Path</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       type      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.type      </code></td>
<td>Resource type.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       id      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.id      </code></td>
<td>Unique identifier.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       external_id      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.external_id      </code></td>
<td>External system ID.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       title      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.title      </code></td>
<td>Variant title.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       description      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.description      </code></td>
<td>Description available.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       sku      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.sku      </code></td>
<td>Stock Keeping Unit.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       inventory_policy      </code></td>
<td>FLOAT</td>
<td><code dir="ltr" translate="no">       $.attributes.inventory_policy      </code></td>
<td>Policy for inventory management.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       inventory_quantity      </code></td>
<td>FLOAT</td>
<td><code dir="ltr" translate="no">       $.attributes.inventory_quantity      </code></td>
<td>Current stock quantity.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       price      </code></td>
<td>FLOAT</td>
<td><code dir="ltr" translate="no">       $.attributes.price      </code></td>
<td>Price.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       url      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.url      </code></td>
<td>URL to variant.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       image_full_url      </code></td>
<td>BOOLEAN</td>
<td><code dir="ltr" translate="no">       $.attributes.image_full_url      </code></td>
<td>Full image URL available (Boolean).</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       image_thumbnail_url      </code></td>
<td>STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.image_thumbnail_url      </code></td>
<td>Thumbnail image URL.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       images      </code></td>
<td>REPEATED STRING</td>
<td><code dir="ltr" translate="no">       $.attributes.images[*      </code> ]</td>
<td>List of images.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       published      </code></td>
<td>BOOLEAN</td>
<td><code dir="ltr" translate="no">       $.attributes.published      </code></td>
<td>Publication status.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       created      </code></td>
<td>TIMESTAMP</td>
<td><code dir="ltr" translate="no">       $.attributes.created      </code></td>
<td>Creation timestamp.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       updated      </code></td>
<td>TIMESTAMP</td>
<td><code dir="ltr" translate="no">       $.attributes.updated      </code></td>
<td>Last update timestamp.</td>
</tr>
</tbody>
</table>
