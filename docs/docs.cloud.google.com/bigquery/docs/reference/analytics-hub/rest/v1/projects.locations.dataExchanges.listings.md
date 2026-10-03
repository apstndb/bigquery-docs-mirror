---
name: documents/docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings
uri: https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings
title: 'REST Resource: projects.locations.dataExchanges.listings'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [Resource: Listing](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#Listing)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#Listing.SCHEMA_REPRESENTATION)
- [BigQueryDatasetSource](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#BigQueryDatasetSource)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#BigQueryDatasetSource.SCHEMA_REPRESENTATION)
- [SelectedResource](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#SelectedResource)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#SelectedResource.SCHEMA_REPRESENTATION)
- [RestrictedExportPolicy](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#RestrictedExportPolicy)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#RestrictedExportPolicy.SCHEMA_REPRESENTATION)
- [Replica](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#Replica)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#Replica.SCHEMA_REPRESENTATION)
- [ReplicaState](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#ReplicaState)
- [PrimaryState](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#PrimaryState)
- [PubSubTopicSource](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#PubSubTopicSource)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#PubSubTopicSource.SCHEMA_REPRESENTATION)
- [State](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#State)
- [DataProvider](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#DataProvider)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#DataProvider.SCHEMA_REPRESENTATION)
- [Category](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#Category)
- [Publisher](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#Publisher)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#Publisher.SCHEMA_REPRESENTATION)
- [RestrictedExportConfig](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#RestrictedExportConfig)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#RestrictedExportConfig.SCHEMA_REPRESENTATION)
- [StoredProcedureConfig](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#StoredProcedureConfig)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#StoredProcedureConfig.SCHEMA_REPRESENTATION)
- [StoredProcedureType](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#StoredProcedureType)
- [CommercialInfo](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#CommercialInfo)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#CommercialInfo.SCHEMA_REPRESENTATION)
- [GoogleCloudMarketplaceInfo](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#GoogleCloudMarketplaceInfo)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#GoogleCloudMarketplaceInfo.SCHEMA_REPRESENTATION)
- [CommercialState](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#CommercialState)
- [Methods](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#METHODS_SUMMARY)

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
  "storedProcedureConfig": {
    object (StoredProcedureConfig)
  },
  "resourceType": enum (SharedResourceType),

  // The following is a list of mutually exclusive fields. At most one of the
  // fields will be set in a response:
  "bigqueryDataset": {
    object (BigQueryDatasetSource)
  },
  "pubsubTopic": {
    object (PubSubTopicSource)
  }
  // End of mutually exclusive fields.
  "discoveryType": enum (DiscoveryType),
  "commercialInfo": {
    object (CommercialInfo)
  },
  "logLinkedDatasetQueryUserEmail": boolean,
  "allowOnlyMetadataSharing": boolean
}
```

| Fields                                                                                                                     |                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|----------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                                                                                                                     | `string` Output only. The resource name of the listing. e.g. `projects/myproject/locations/us/dataExchanges/123/listings/456`                                                                                                                                                                                                                                                                                                                                   |
| `displayName`                                                                                                              | `string` Required. Human-readable display name of the listing. The display name must contain only Unicode letters, numbers (0-9), underscores (\_), dashes (-), spaces ( ), ampersands (&) and can't start or end with spaces. Default value is an empty string. Max length: 63 bytes.                                                                                                                                                                          |
| `description`                                                                                                              | `string` Optional. Short description of the listing. The description must not contain Unicode non-characters and C0 and C1 control codes except tabs (HT), new lines (LF), carriage returns (CR), and page breaks (FF). Default value is an empty string. Max length: 2000 bytes.                                                                                                                                                                               |
| `primaryContact`                                                                                                           | `string` Optional. Email or URL of the primary point of contact of the listing. Max Length: 1000 bytes.                                                                                                                                                                                                                                                                                                                                                         |
| `documentation`                                                                                                            | `string` Optional. Documentation describing the listing.                                                                                                                                                                                                                                                                                                                                                                                                        |
| `state`                                                                                                                    | `enum ( `[`State`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#State)` )` Output only. Current state of the listing.                                                                                                                                                                                                                                                                  |
| `icon`                                                                                                                     | `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)` Optional. Base64 encoded image representing the listing. Max Size: 3.0MiB Expected image dimensions are 512x512 pixels, however the API only performs validation on size of the encoded data. Note: For byte fields, the contents of the field are base64-encoded (which increases the size of the data by 33-36%) when using JSON on the wire. A base64-encoded string. |
| `dataProvider`                                                                                                             | `object ( `[`DataProvider`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#DataProvider)` )` Optional. Details of the data provider who owns the source data.                                                                                                                                                                                                                            |
| `categories[]`                                                                                                             | `enum ( `[`Category`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#Category)` )` Optional. Categories of the listing. Up to five categories are allowed.                                                                                                                                                                                                                               |
| `publisher`                                                                                                                | `object ( `[`Publisher`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#Publisher)` )` Optional. Details of the publisher who owns the listing and who can share the source data.                                                                                                                                                                                                        |
| `requestAccess`                                                                                                            | `string` Optional. Email or URL of the request access of the listing. Subscribers can use this reference to request access. Max Length: 1000 bytes.                                                                                                                                                                                                                                                                                                             |
| `restrictedExportConfig`                                                                                                   | `object ( `[`RestrictedExportConfig`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#RestrictedExportConfig)` )` Optional. If set, restricted export configuration will be propagated and enforced on the linked dataset.                                                                                                                                                                |
| `storedProcedureConfig`                                                                                                    | `object ( `[`StoredProcedureConfig`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#StoredProcedureConfig)` )` Optional. If set, stored procedure configuration will be propagated and enforced on the linked dataset.                                                                                                                                                                   |
| `resourceType`                                                                                                             | `enum ( `[`SharedResourceType`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/Shared.Types/SharedResourceType)` )` Output only. Listing shared asset type.                                                                                                                                                                                                                                                                           |
| Listing source. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `bigqueryDataset`                                                                                                          | `object ( `[`BigQueryDatasetSource`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#BigQueryDatasetSource)` )` Shared dataset i.e. BigQuery dataset source.                                                                                                                                                                                                                              |
| `pubsubTopic`                                                                                                              | `object ( `[`PubSubTopicSource`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#PubSubTopicSource)` )` Pub/Sub topic source.                                                                                                                                                                                                                                                             |
| End of mutually exclusive fields.                                                                                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `discoveryType`                                                                                                            | `enum ( `[`DiscoveryType`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/DiscoveryType)` )` Optional. Type of discovery of the listing on the discovery page.                                                                                                                                                                                                                                                                     |
| `commercialInfo`                                                                                                           | `object ( `[`CommercialInfo`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#CommercialInfo)` )` Output only. Commercial info contains the information about the commercial data products associated with the listing.                                                                                                                                                                   |
| `logLinkedDatasetQueryUserEmail`                                                                                           | `boolean` Optional. By default, false. If true, the Listing has an email sharing mandate enabled.                                                                                                                                                                                                                                                                                                                                                               |
| `allowOnlyMetadataSharing`                                                                                                 | `boolean` Optional. If true, the listing is only available to get the resource metadata. Listing is non subscribable.                                                                                                                                                                                                                                                                                                                                           |

## BigQueryDatasetSource

A reference to a shared dataset. It is an existing BigQuery dataset with a collection of objects such as tables and views that you want to share with subscribers. When subscriber's subscribe to a listing, Analytics Hub creates a linked dataset in the subscriber's project. A Linked dataset is an opaque, read-only BigQuery dataset that serves as a *symbolic link* to a shared dataset.

**JSON representation**

```
{
  "dataset": string,
  "selectedResources": [
    {
      object (SelectedResource)
    }
  ],
  "restrictedExportPolicy": {
    object (RestrictedExportPolicy)
  },
  "replicaLocations": [
    string
  ],
  "effectiveReplicas": [
    {
      object (Replica)
    }
  ]
}
```

| Fields                   |                                                                                                                                                                                                                                                                                                                                                     |
|--------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `dataset`                | `string` Optional. Resource name of the dataset source for this listing. e.g. `projects/myproject/datasets/123`                                                                                                                                                                                                                                     |
| `selectedResources[]`    | `object ( `[`SelectedResource`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#SelectedResource)` )` Optional. Resource in this dataset that is selectively shared. This field is required for data clean room exchanges.                                                    |
| `restrictedExportPolicy` | `object ( `[`RestrictedExportPolicy`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#RestrictedExportPolicy)` )` Optional. If set, restricted export policy will be propagated and enforced on the linked dataset.                                                           |
| `replicaLocations[]`     | `string` Optional. A list of regions where the publisher has created shared dataset replicas.                                                                                                                                                                                                                                                       |
| `effectiveReplicas[]`    | `object ( `[`Replica`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#Replica)` )` Output only. Server-owned effective state of replicas. Contains both primary and secondary replicas. Each replica includes a system-computed (output-only) state and primary designation. |

## SelectedResource

Resource in this dataset that is selectively shared.

**JSON representation**

```
{

  // The following is a list of mutually exclusive fields. At most one of the
  // fields will be set in a response:
  "table": string,
  "routine": string
  // End of mutually exclusive fields.
}
```

| Fields                                                                                                     |                                                                                                                                                                                      |
|------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| The following is a list of mutually exclusive fields. At most one of the fields will be set in a response: |                                                                                                                                                                                      |
| `table`                                                                                                    | `string` Optional. Format: For table: `projects/{projectId}/datasets/{datasetId}/tables/{tableId}` Example:"projects/test_project/datasets/test_dataset/tables/test_table"           |
| `routine`                                                                                                  | `string` Optional. Format: For routine: `projects/{projectId}/datasets/{datasetId}/routines/{routineId}` Example:"projects/test_project/datasets/test_dataset/routines/test_routine" |
| End of mutually exclusive fields.                                                                          |                                                                                                                                                                                      |

## RestrictedExportPolicy

Restricted export policy used to configure restricted export on linked dataset.

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
| `restrictDirectTableAccess` | `boolean` Optional. If true, restrict direct table access (read api/tabledata.list) on linked table.       |
| `restrictQueryResult`       | `boolean` Optional. If true, restrict export of query result derived from restricted linked dataset table. |

## Replica

Represents the state of a replica of a shared dataset. It includes the geographic location of the replica and system-computed, output-only fields indicating its replication state and whether it is the primary replica.

**JSON representation**

```
{
  "location": string,
  "replicaState": enum (ReplicaState),
  "primaryState": enum (PrimaryState)
}
```

| Fields         |                                                                                                                                                                                                                                                    |
|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `location`     | `string` Output only. The geographic location where the replica resides. See [BigQuery locations](https://cloud.google.com/bigquery/docs/locations) for supported locations. Eg. "us-central1".                                                    |
| `replicaState` | `enum ( `[`ReplicaState`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#ReplicaState)` )` Output only. Assigned by Analytics Hub based on real BigQuery replication state. |
| `primaryState` | `enum ( `[`PrimaryState`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#PrimaryState)` )` Output only. Indicates that this replica is the primary replica.                 |

## ReplicaState

Replica state of the shared dataset.

| Enums                       |                                                                             |
|-----------------------------|-----------------------------------------------------------------------------|
| `REPLICA_STATE_UNSPECIFIED` | Default value. This value is unused.                                        |
| `READY_TO_USE`              | The replica is backfilled and ready to use.                                 |
| `UNAVAILABLE`               | The replica is unavailable, does not exist, or has not been backfilled yet. |

## PrimaryState

Primary state of the replica. Set only for the primary replica.

| Enums                       |                                      |
|-----------------------------|--------------------------------------|
| `PRIMARY_STATE_UNSPECIFIED` | Default value. This value is unused. |
| `PRIMARY_REPLICA`           | The replica is the primary replica.  |

## PubSubTopicSource

Pub/Sub topic source.

**JSON representation**

```
{
  "topic": string,
  "dataAffinityRegions": [
    string
  ]
}
```

| Fields                  |                                                                                                                                                                                                       |
|-------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `topic`                 | `string` Required. Resource name of the Pub/Sub topic source for this listing. e.g. projects/myproject/topics/topicId                                                                                 |
| `dataAffinityRegions[]` | `string` Optional. Region hint on where the data might be published. Data affinity regions are modifiable. See <https://cloud.google.com/about/locations> for full listing of possible Cloud regions. |

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

## StoredProcedureConfig

Stored procedure configuration, used to configure stored procedure sharing on linked dataset.

**JSON representation**

```
{
  "enabled": boolean,
  "allowedStoredProcedureTypes": [
    enum (StoredProcedureType)
  ]
}
```

| Fields                          |                                                                                                                                                                                                                                            |
|---------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `enabled`                       | `boolean` Optional. If true, enable sharing of stored procedure.                                                                                                                                                                           |
| `allowedStoredProcedureTypes[]` | `enum ( `[`StoredProcedureType`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#StoredProcedureType)` )` Output only. Types of stored procedure supported to share. |

## StoredProcedureType

Enum to specify the type of stored procedure to share.

| Enums                               |                                      |
|-------------------------------------|--------------------------------------|
| `STORED_PROCEDURE_TYPE_UNSPECIFIED` | Default value. This value is unused. |
| `SQL_PROCEDURE`                     | SQL stored procedure.                |

## CommercialInfo

Commercial info contains the information about the commercial data products associated with the listing.

**JSON representation**

```
{
  "cloudMarketplace": {
    object (GoogleCloudMarketplaceInfo)
  }
}
```

| Fields             |                                                                                                                                                                                                                                                                                   |
|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `cloudMarketplace` | `object ( `[`GoogleCloudMarketplaceInfo`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#GoogleCloudMarketplaceInfo)` )` Output only. Details of the Marketplace Data Product associated with the Listing. |

## GoogleCloudMarketplaceInfo

Specifies the details of the Marketplace Data Product associated with the Listing.

**JSON representation**

```
{
  "service": string,
  "commercialState": enum (CommercialState)
}
```

| Fields            |                                                                                                                                                                                                                                        |
|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `service`         | `string` Output only. Resource name of the commercial service associated with the Marketplace Data Product. e.g. example.com                                                                                                           |
| `commercialState` | `enum ( `[`CommercialState`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#CommercialState)` )` Output only. Commercial state of the Marketplace Data Product. |

## CommercialState

Indicates whether this commercial access is currently active.

| Enums                          |                                                      |
|--------------------------------|------------------------------------------------------|
| `COMMERCIAL_STATE_UNSPECIFIED` | Commercialization is incomplete and cannot be used.  |
| `ONBOARDING`                   | Commercialization has been initialized.              |
| `ACTIVE`                       | Commercialization is complete and available for use. |

| Methods                                                                                                                                                          |                                                              |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------|
| [`create`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings/create)                         | Creates a new listing.                                       |
| [`delete`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings/delete)                         | Deletes a listing.                                           |
| [`get`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings/get)                               | Gets the details of a listing.                               |
| [`getIamPolicy`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings/getIamPolicy)             | Gets the IAM policy.                                         |
| [`list`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings/list)                             | Lists all listings in a given project and location.          |
| [`listSubscriptions`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings/listSubscriptions)   | Lists all subscriptions on a given Data Exchange or Listing. |
| [`patch`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings/patch)                           | Updates an existing listing.                                 |
| [`setIamPolicy`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings/setIamPolicy)             | Sets the IAM policy.                                         |
| [`subscribe`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings/subscribe)                   | Subscribes to a listing.                                     |
| [`testIamPermissions`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings/testIamPermissions) | Returns the permissions that a caller has.                   |
