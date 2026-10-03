---
name: documents/docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1beta1/projects.locations.dataExchanges.listings
uri: https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1beta1/projects.locations.dataExchanges.listings
title: 'REST Resource: projects.locations.dataExchanges.listings'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [Resource: Listing](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1beta1/projects.locations.dataExchanges.listings#Listing)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1beta1/projects.locations.dataExchanges.listings#Listing.SCHEMA_REPRESENTATION)
- [BigQueryDatasetSource](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1beta1/projects.locations.dataExchanges.listings#BigQueryDatasetSource)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1beta1/projects.locations.dataExchanges.listings#BigQueryDatasetSource.SCHEMA_REPRESENTATION)
- [State](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1beta1/projects.locations.dataExchanges.listings#State)
- [DataProvider](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1beta1/projects.locations.dataExchanges.listings#DataProvider)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1beta1/projects.locations.dataExchanges.listings#DataProvider.SCHEMA_REPRESENTATION)
- [Category](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1beta1/projects.locations.dataExchanges.listings#Category)
- [Publisher](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1beta1/projects.locations.dataExchanges.listings#Publisher)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1beta1/projects.locations.dataExchanges.listings#Publisher.SCHEMA_REPRESENTATION)
- [RestrictedExportConfig](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1beta1/projects.locations.dataExchanges.listings#RestrictedExportConfig)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1beta1/projects.locations.dataExchanges.listings#RestrictedExportConfig.SCHEMA_REPRESENTATION)
- [Methods](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1beta1/projects.locations.dataExchanges.listings#METHODS_SUMMARY)

## Resource: Listing

A listing is what gets published into a data exchange that a subscriber can subscribe to. It contains a reference to the data source along with descriptive information that will help subscribers find and subscribe the data.

**JSON representation**

```
{
  "name": string,
  "displayName": string,
  "description": string,
  "primaryContact": string,
  "documentation": string,
  "state": enum (State),
  "icon": string,
  "dataProvider": {
    object (DataProvider)
  },
  "categories": [
    enum (Category)
  ],
  "publisher": {
    object (Publisher)
  },
  "requestAccess": string,
  "restrictedExportConfig": {
    object (RestrictedExportConfig)
  },
  "allowOnlyMetadataSharing": boolean,

  // The following is a list of mutually exclusive fields. At most one of the
  // fields will be set in a response:
  "bigqueryDataset": {
    object (BigQueryDatasetSource)
  }
  // End of mutually exclusive fields.
}
```

| Fields                                                                                                                     |                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|----------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                                                                                                                     | `string` Output only. The resource name of the listing. e.g. `projects/myproject/locations/us/dataExchanges/123/listings/456`                                                                                                                                                                                                                                                                                                                                   |
| `displayName`                                                                                                              | `string` Required. Human-readable display name of the listing. The display name must contain only Unicode letters, numbers (0-9), underscores (\_), dashes (-), spaces ( ), ampersands (&) and can't start or end with spaces. Default value is an empty string. Max length: 63 bytes.                                                                                                                                                                          |
| `description`                                                                                                              | `string` Optional. Short description of the listing. The description must not contain Unicode non-characters and C0 and C1 control codes except tabs (HT), new lines (LF), carriage returns (CR), and page breaks (FF). Default value is an empty string. Max length: 2000 bytes.                                                                                                                                                                               |
| `primaryContact`                                                                                                           | `string` Optional. Email or URL of the primary point of contact of the listing. Max Length: 1000 bytes.                                                                                                                                                                                                                                                                                                                                                         |
| `documentation`                                                                                                            | `string` Optional. Documentation describing the listing.                                                                                                                                                                                                                                                                                                                                                                                                        |
| `state`                                                                                                                    | `enum ( `[`State`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1beta1/projects.locations.dataExchanges.listings#State)` )` Output only. Current state of the listing.                                                                                                                                                                                                                                                             |
| `icon`                                                                                                                     | `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)` Optional. Base64 encoded image representing the listing. Max Size: 3.0MiB Expected image dimensions are 512x512 pixels, however the API only performs validation on size of the encoded data. Note: For byte fields, the contents of the field are base64-encoded (which increases the size of the data by 33-36%) when using JSON on the wire. A base64-encoded string. |
| `dataProvider`                                                                                                             | `object ( `[`DataProvider`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1beta1/projects.locations.dataExchanges.listings#DataProvider)` )` Optional. Details of the data provider who owns the source data.                                                                                                                                                                                                                       |
| `categories[]`                                                                                                             | `enum ( `[`Category`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1beta1/projects.locations.dataExchanges.listings#Category)` )` Optional. Categories of the listing. Up to five categories are allowed.                                                                                                                                                                                                                          |
| `publisher`                                                                                                                | `object ( `[`Publisher`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1beta1/projects.locations.dataExchanges.listings#Publisher)` )` Optional. Details of the publisher who owns the listing and who can share the source data.                                                                                                                                                                                                   |
| `requestAccess`                                                                                                            | `string` Optional. Email or URL of the request access of the listing. Subscribers can use this reference to request access. Max Length: 1000 bytes.                                                                                                                                                                                                                                                                                                             |
| `restrictedExportConfig`                                                                                                   | `object ( `[`RestrictedExportConfig`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1beta1/projects.locations.dataExchanges.listings#RestrictedExportConfig)` )` Optional. If set, restricted export configuration will be propagated and enforced on the linked dataset. This is a required field for data clean room exchanges.                                                                                                   |
| `allowOnlyMetadataSharing`                                                                                                 | `boolean` Optional. If true, the listing is only available to get the resource metadata. Listing is non subscribable.                                                                                                                                                                                                                                                                                                                                           |
| Listing source. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `bigqueryDataset`                                                                                                          | `object ( `[`BigQueryDatasetSource`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1beta1/projects.locations.dataExchanges.listings#BigQueryDatasetSource)` )` Required. Shared dataset i.e. BigQuery dataset source.                                                                                                                                                                                                               |
| End of mutually exclusive fields.                                                                                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |

## BigQueryDatasetSource

A reference to a shared dataset. It is an existing BigQuery dataset with a collection of objects such as tables and views that you want to share with subscribers. When subscriber's subscribe to a listing, Analytics Hub creates a linked dataset in the subscriber's project. A Linked dataset is an opaque, read-only BigQuery dataset that serves as a *symbolic link* to a shared dataset.

**JSON representation**

```
{
  "dataset": string
}
```

| Fields    |                                                                                                       |
|-----------|-------------------------------------------------------------------------------------------------------|
| `dataset` | `string` Resource name of the dataset source for this listing. e.g. `projects/myproject/datasets/123` |

## State

State of the listing.

| Enums               |                                                                                                          |
|---------------------|----------------------------------------------------------------------------------------------------------|
| `STATE_UNSPECIFIED` | Default value. This value is unused.                                                                     |
| `ACTIVE`            | Subscribable state. Users with dataexchange.listings.subscribe permission can subscribe to this listing. |

## DataProvider

Contains details of the data provider.

**JSON representation**

```
{
  "name": string,
  "primaryContact": string
}
```

| Fields           |                                                                               |
|------------------|-------------------------------------------------------------------------------|
| `name`           | `string` Optional. Name of the data provider.                                 |
| `primaryContact` | `string` Optional. Email or URL of the data provider. Max Length: 1000 bytes. |

## Category

Listing categories.

| Enums                                   |     |
|-----------------------------------------|-----|
| `CATEGORY_UNSPECIFIED`                  |     |
| `CATEGORY_OTHERS`                       |     |
| `CATEGORY_ADVERTISING_AND_MARKETING`    |     |
| `CATEGORY_COMMERCE`                     |     |
| `CATEGORY_CLIMATE_AND_ENVIRONMENT`      |     |
| `CATEGORY_DEMOGRAPHICS`                 |     |
| `CATEGORY_ECONOMICS`                    |     |
| `CATEGORY_EDUCATION`                    |     |
| `CATEGORY_ENERGY`                       |     |
| `CATEGORY_FINANCIAL`                    |     |
| `CATEGORY_GAMING`                       |     |
| `CATEGORY_GEOSPATIAL`                   |     |
| `CATEGORY_HEALTHCARE_AND_LIFE_SCIENCE`  |     |
| `CATEGORY_MEDIA`                        |     |
| `CATEGORY_PUBLIC_SECTOR`                |     |
| `CATEGORY_RETAIL`                       |     |
| `CATEGORY_SPORTS`                       |     |
| `CATEGORY_SCIENCE_AND_RESEARCH`         |     |
| `CATEGORY_TRANSPORTATION_AND_LOGISTICS` |     |
| `CATEGORY_TRAVEL_AND_TOURISM`           |     |
| `CATEGORY_GOOGLE_EARTH_ENGINE`          |     |

## Publisher

Contains details of the listing publisher.

**JSON representation**

```
{
  "name": string,
  "primaryContact": string
}
```

| Fields           |                                                                                   |
|------------------|-----------------------------------------------------------------------------------|
| `name`           | `string` Optional. Name of the listing publisher.                                 |
| `primaryContact` | `string` Optional. Email or URL of the listing publisher. Max Length: 1000 bytes. |

## RestrictedExportConfig

Restricted export config, used to configure restricted export on linked dataset.

**JSON representation**

```
{
  "enabled": boolean,
  "restrictDirectTableAccess": boolean,
  "restrictQueryResult": boolean
}
```

| Fields                      |                                                                                                            |
|-----------------------------|------------------------------------------------------------------------------------------------------------|
| `enabled`                   | `boolean` Optional. If true, enable restricted export.                                                     |
| `restrictDirectTableAccess` | `boolean` Output only. If true, restrict direct table access(read api/tabledata.list) on linked table.     |
| `restrictQueryResult`       | `boolean` Optional. If true, restrict export of query result derived from restricted linked dataset table. |

| Methods                                                                                                                                                               |                                                     |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------|
| [`create`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1beta1/projects.locations.dataExchanges.listings/create)                         | Creates a new listing.                              |
| [`delete`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1beta1/projects.locations.dataExchanges.listings/delete)                         | Deletes a listing.                                  |
| [`get`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1beta1/projects.locations.dataExchanges.listings/get)                               | Gets the details of a listing.                      |
| [`getIamPolicy`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1beta1/projects.locations.dataExchanges.listings/getIamPolicy)             | Gets the IAM policy.                                |
| [`list`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1beta1/projects.locations.dataExchanges.listings/list)                             | Lists all listings in a given project and location. |
| [`patch`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1beta1/projects.locations.dataExchanges.listings/patch)                           | Updates an existing listing.                        |
| [`setIamPolicy`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1beta1/projects.locations.dataExchanges.listings/setIamPolicy)             | Sets the IAM policy.                                |
| [`subscribe`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1beta1/projects.locations.dataExchanges.listings/subscribe)                   | Subscribes to a listing.                            |
| [`testIamPermissions`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1beta1/projects.locations.dataExchanges.listings/testIamPermissions) | Returns the permissions that a caller has.          |
