---
name: documents/docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges
uri: https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges
title: 'REST Resource: projects.locations.dataExchanges'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [Resource: DataExchange](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges#DataExchange)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges#DataExchange.SCHEMA_REPRESENTATION)
- [SharingEnvironmentConfig](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges#SharingEnvironmentConfig)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges#SharingEnvironmentConfig.SCHEMA_REPRESENTATION)
- [DefaultExchangeConfig](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges#DefaultExchangeConfig)
- [DcrExchangeConfig](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges#DcrExchangeConfig)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges#DcrExchangeConfig.SCHEMA_REPRESENTATION)
- [Methods](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges#METHODS_SUMMARY)

## Resource: DataExchange

A data exchange is a container that lets you share data. Along with the descriptive information about the data exchange, it contains listings that reference shared datasets.

**JSON representation**

```
{
  "name": string,
  "displayName": string,
  "description": string,
  "primaryContact": string,
  "documentation": string,
  "listingCount": integer,
  "icon": string,
  "sharingEnvironmentConfig": {
    object (SharingEnvironmentConfig)
  },
  "discoveryType": enum (DiscoveryType),
  "logLinkedDatasetQueryUserEmail": boolean
}
```

| Fields                           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|----------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                           | `string` Output only. The resource name of the data exchange. e.g. `projects/myproject/locations/us/dataExchanges/123` .                                                                                                                                                                                                                                                                                                                                              |
| `displayName`                    | `string` Required. Human-readable display name of the data exchange. The display name must contain only Unicode letters, numbers (0-9), underscores (\_), dashes (-), spaces ( ), ampersands (&) and must not start or end with spaces. Default value is an empty string. Max length: 63 bytes.                                                                                                                                                                       |
| `description`                    | `string` Optional. Description of the data exchange. The description must not contain Unicode non-characters as well as C0 and C1 control codes except tabs (HT), new lines (LF), carriage returns (CR), and page breaks (FF). Default value is an empty string. Max length: 2000 bytes.                                                                                                                                                                              |
| `primaryContact`                 | `string` Optional. Email or URL of the primary point of contact of the data exchange. Max Length: 1000 bytes.                                                                                                                                                                                                                                                                                                                                                         |
| `documentation`                  | `string` Optional. Documentation describing the data exchange.                                                                                                                                                                                                                                                                                                                                                                                                        |
| `listingCount`                   | `integer` Output only. Number of listings contained in the data exchange.                                                                                                                                                                                                                                                                                                                                                                                             |
| `icon`                           | `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)` Optional. Base64 encoded image representing the data exchange. Max Size: 3.0MiB Expected image dimensions are 512x512 pixels, however the API only performs validation on size of the encoded data. Note: For byte fields, the content of the fields are base64-encoded (which increases the size of the data by 33-36%) when using JSON on the wire. A base64-encoded string. |
| `sharingEnvironmentConfig`       | `object ( `[`SharingEnvironmentConfig`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges#SharingEnvironmentConfig)` )` Optional. Configurable data sharing environment option for a data exchange.                                                                                                                                                                                                        |
| `discoveryType`                  | `enum ( `[`DiscoveryType`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/DiscoveryType)` )` Optional. Type of discovery on the discovery page for all the listings under this exchange. Updating this field also updates (overwrites) the discoveryType field for all the listings under this exchange.                                                                                                                                 |
| `logLinkedDatasetQueryUserEmail` | `boolean` Optional. By default, false. If true, the DataExchange has an email sharing mandate enabled.                                                                                                                                                                                                                                                                                                                                                                |

## SharingEnvironmentConfig

Sharing environment is a behavior model for sharing data within a data exchange. This option is configurable for a data exchange.

**JSON representation**

```
{

  // The following is a list of mutually exclusive fields. At most one of the
  // fields will be set in a response:
  "defaultExchangeConfig": {
    object (DefaultExchangeConfig)
  },
  "dcrExchangeConfig": {
    object (DcrExchangeConfig)
  }
  // End of mutually exclusive fields.
}
```

| Fields                                                                                                     |                                                                                                                                                                                                                                                  |
|------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| The following is a list of mutually exclusive fields. At most one of the fields will be set in a response: |                                                                                                                                                                                                                                                  |
| `defaultExchangeConfig`                                                                                    | `object ( `[`DefaultExchangeConfig`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges#DefaultExchangeConfig)` )` Default Analytics Hub data exchange, used for secured data sharing. |
| `dcrExchangeConfig`                                                                                        | `object ( `[`DcrExchangeConfig`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges#DcrExchangeConfig)` )` Data Clean Room (DCR), used for privacy-safe and secured data sharing.      |
| End of mutually exclusive fields.                                                                          |                                                                                                                                                                                                                                                  |

## DefaultExchangeConfig

This type has no fields.

Default Analytics Hub data exchange, used for secured data sharing.

## DcrExchangeConfig

Data Clean Room (DCR), used for privacy-safe and secured data sharing.

**JSON representation**

```
{
  "singleSelectedResourceSharingRestriction": boolean,
  "singleLinkedDatasetPerCleanroom": boolean
}
```

| Fields                                     |                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|--------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `singleSelectedResourceSharingRestriction` | `boolean` Output only. If True, this DCR restricts the contributors to sharing only a single resource in a Listing. And no two resources should have the same IDs. So if a contributor adds a view with a conflicting name, the CreateListing API will reject the request. if False, the data contributor can publish an entire dataset (as before). This is not configurable, and by default, all new DCRs will have the restriction set to True. |
| `singleLinkedDatasetPerCleanroom`          | `boolean` Output only. If True, when subscribing to this DCR, it will create only one linked dataset containing all resources shared within the cleanroom. If False, when subscribing to this DCR, it will create 1 linked dataset per listing. This is not configurable, and by default, all new DCRs will have the restriction set to True.                                                                                                      |

| Methods                                                                                                                                                 |                                                              |
|---------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------|
| [`create`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges/create)                         | Creates a new data exchange.                                 |
| [`delete`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges/delete)                         | Deletes an existing data exchange.                           |
| [`get`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges/get)                               | Gets the details of a data exchange.                         |
| [`getIamPolicy`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges/getIamPolicy)             | Gets the IAM policy.                                         |
| [`list`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges/list)                             | Lists all data exchanges in a given project and location.    |
| [`listSubscriptions`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges/listSubscriptions)   | Lists all subscriptions on a given Data Exchange or Listing. |
| [`patch`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges/patch)                           | Updates an existing data exchange.                           |
| [`setIamPolicy`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges/setIamPolicy)             | Sets the IAM policy.                                         |
| [`subscribe`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges/subscribe)                   | Creates a Subscription to a Data Clean Room.                 |
| [`testIamPermissions`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges/testIamPermissions) | Returns the permissions that a caller has.                   |
