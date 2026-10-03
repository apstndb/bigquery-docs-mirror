---
name: documents/docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.subscriptions
uri: https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.subscriptions
title: 'REST Resource: projects.locations.subscriptions'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [Resource: Subscription](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.subscriptions#Subscription)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.subscriptions#Subscription.SCHEMA_REPRESENTATION)
- [Methods](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.subscriptions#METHODS_SUMMARY)

## Resource: Subscription

A subscription represents a subscribers' access to a particular set of published data. It contains references to associated listings, data exchanges, and linked datasets.

**JSON representation**

```
{
  "name": string,
  "creationTime": string,
  "lastModifyTime": string,
  "organizationId": string,
  "organizationDisplayName": string,
  "state": enum (State),
  "linkedDatasetMap": {
    string: {
      object (LinkedResource)
    },
    ...
  },
  "subscriberContact": string,
  "linkedResources": [
    {
      object (LinkedResource)
    }
  ],
  "resourceType": enum (SharedResourceType),
  "commercialInfo": {
    object (CommercialInfo)
  },
  "destinationDataset": {
    object (DestinationDataset)
  },

  // The following is a list of mutually exclusive fields. At most one of the
  // fields will be set in a response:
  "listing": string,
  "dataExchange": string
  // End of mutually exclusive fields.
  "logLinkedDatasetQueryUserEmail": boolean
}
```

| Fields                                                                                                     |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                                                                                                     | `string` Output only. The resource name of the subscription. e.g. `projects/myproject/locations/us/subscriptions/123` .                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `creationTime`                                                                                             | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Timestamp when the subscription was created. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                                                                            |
| `lastModifyTime`                                                                                           | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Timestamp when the subscription was last modified. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                                                                      |
| `organizationId`                                                                                           | `string` Output only. Organization of the project this subscription belongs to.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `organizationDisplayName`                                                                                  | `string` Output only. Display name of the project of this subscription.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `state`                                                                                                    | `enum ( `[`State`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/Shared.Types/State)` )` Output only. Current state of the subscription.                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `linkedDatasetMap`                                                                                         | `map (key: string, value: object ( `[`LinkedResource`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/Shared.Types/Subscription#LinkedResource)` ))` Output only. Map of listing resource names to associated linked resource, e.g. projects/123/locations/us/dataExchanges/456/listings/789 -\> projects/123/datasets/my_dataset For listing-level subscriptions, this is a map of size 1. Only contains values if state == STATE_ACTIVE. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |
| `subscriberContact`                                                                                        | `string` Output only. Email of the subscriber.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `linkedResources[]`                                                                                        | `object ( `[`LinkedResource`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/Shared.Types/Subscription#LinkedResource)` )` Output only. Linked resources created in the subscription. Only contains values if state = STATE_ACTIVE.                                                                                                                                                                                                                                                                                                                              |
| `resourceType`                                                                                             | `enum ( `[`SharedResourceType`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/Shared.Types/SharedResourceType)` )` Output only. Listing shared asset type.                                                                                                                                                                                                                                                                                                                                                                                                      |
| `commercialInfo`                                                                                           | `object ( `[`CommercialInfo`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/Shared.Types/Subscription#CommercialInfo)` )` Output only. This is set if this is a commercial subscription i.e. if this subscription was created from subscribing to a commercial listing.                                                                                                                                                                                                                                                                                         |
| `destinationDataset`                                                                                       | `object ( `[`DestinationDataset`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/Shared.Types/DestinationDataset)` )` Optional. BigQuery destination dataset to create for the subscriber.                                                                                                                                                                                                                                                                                                                                                                       |
| The following is a list of mutually exclusive fields. At most one of the fields will be set in a response: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `listing`                                                                                                  | `string` Output only. Resource name of the source Listing. e.g. projects/123/locations/us/dataExchanges/456/listings/789                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `dataExchange`                                                                                             | `string` Output only. Resource name of the source Data Exchange. e.g. projects/123/locations/us/dataExchanges/456                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| End of mutually exclusive fields.                                                                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `logLinkedDatasetQueryUserEmail`                                                                           | `boolean` Output only. By default, false. If true, the Subscriber agreed to the email sharing mandate that is enabled for DataExchange/Listing.                                                                                                                                                                                                                                                                                                                                                                                                                                            |

| Methods                                                                                                                                     |                                                          |
|---------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------|
| [`delete`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.subscriptions/delete)             | Deletes a subscription.                                  |
| [`get`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.subscriptions/get)                   | Gets the details of a Subscription.                      |
| [`getIamPolicy`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.subscriptions/getIamPolicy) | Gets the IAM policy.                                     |
| [`list`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.subscriptions/list)                 | Lists all subscriptions in a given project and location. |
| [`refresh`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.subscriptions/refresh)           | Refreshes a Subscription to a Data Exchange.             |
| [`revoke`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.subscriptions/revoke)             | Revokes a given subscription.                            |
| [`setIamPolicy`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.subscriptions/setIamPolicy) | Sets the IAM policy.                                     |
