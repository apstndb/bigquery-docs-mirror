---
name: documents/docs.cloud.google.com/bigquery/docs/analytics-hub-manage-subscriptions
uri: https://docs.cloud.google.com/bigquery/docs/analytics-hub-manage-subscriptions
title: Manage subscriptions
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# Manage subscriptions

You can manage your subscriptions in BigQuery sharing (formerly Analytics Hub) to control data access and sharing. As a subscriber, you can subscribe to listings, view your subscriptions, and delete them. As a publisher, you can monitor who has access to your listings and revoke subscriptions as needed. A BigQuery sharing subscription is a regionalized resource that resides in the subscriber's project. Subscriptions store information about the subscriber and represent the contract between the publisher and the subscriber.

## Before you begin

To get started with BigQuery sharing (formerly Analytics Hub), you need to enable the Analytics Hub API inside your Google Cloud project.

To enable the Analytics Hub API, you need the following Identity and Access Management (IAM) permissions:

  - `serviceUsage.services.get`
  - `serviceUsage.services.list`
  - `serviceUsage.services.enable`

The following predefined IAM role includes the permissions that you need to enable the Analytics Hub API:

  - [Service Usage Admin](https://docs.cloud.google.com/service-usage/docs/access-control#serviceusage.serviceUsageAdmin) ( `roles/serviceusage.serviceUsageAdmin` )

To enable the Analytics Hub API, select one of the following options:

### Console

Go to the **Analytics Hub API** page and enable the Analytics Hub API for your Google Cloud project.

### gcloud

Run the [gcloud services enable](https://docs.cloud.google.com/sdk/gcloud/reference/services/enable) command:

    gcloud services enable analyticshub.googleapis.com

### Required roles

To get the permissions that you need to manage subscriptions, ask your administrator to grant you the [Analytics Hub Subscription Owner](https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.subscriptionOwner) ( `roles/analyticshub.subscriptionOwner` ) IAM role on the project. For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## Limitations

Subscriptions have the following limitations:

  - You can only use the Analytics Hub API to manage subscriptions that were created after July 25, 2023. Linked datasets created before this date aren't supported because they lack the required subscription resource.

## Manage subscriptions as a subscriber

The following sections describe how BigQuery sharing subscribers manage subscriptions.

### Subscribe to listings

To subscribe to listings, follow the steps in [View and subscribe to listings and data exchanges](https://docs.cloud.google.com/bigquery/docs/analytics-hub-view-subscribe-listings#subscribe-listings) .

### List subscriptions

To list your subscriptions in a project, call the [`projects.locations.subscriptions.list` method](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.subscriptions/list) :

    GET https://analyticshub.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/subscriptions

Replace the following:

  - `  PROJECT_ID  ` : the Google Cloud project ID of the project that contains the subscriptions that you want to list.
  - `  LOCATION  ` : the location of the subscriptions that you want to list. For more information about locations that support sharing, see [Supported regions](https://docs.cloud.google.com/bigquery/docs/analytics-hub-introduction#supported-regions) .

### Delete a subscription

To delete a subscription, call the [`projects.locations.subscriptions.delete` method](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.subscriptions/delete) :

    DELETE https://analyticshub.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/subscriptions/SUBSCRIPTION_ID

Replace the following:

  - `  PROJECT_ID  ` : the Google Cloud project ID of the project that contains the subscription that you want to delete.
  - `  LOCATION  ` : the location of the subscription that you want to delete.
  - `  SUBSCRIPTION_ID  ` : the ID of the subscription that you want to delete.

The request body must be empty. If successful, the response body contains an operation instance.

When you delete a subscription, the linked dataset is also deleted from your project.

When you delete a subscription from a multi-region listing, all primary and secondary linked dataset replicas are also deleted from your project.

For more information about managing subscriptions using the Analytics Hub API, see the [`projects.locations.subscriptions` methods](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.subscriptions#methods) .

## Manage subscriptions as a publisher

The following sections describe how BigQuery sharing publishers manage subscriptions. For more information about managing subscriptions to listings, see [Manage listings](https://docs.cloud.google.com/bigquery/docs/analytics-hub-manage-listings) .

### List subscriptions

To list all subscriptions, select one of the following options:

### Console

1.  In the Google Cloud console, go to the **Sharing (Analytics Hub)** page.
    
    The page lists all the [data exchanges](https://docs.cloud.google.com/bigquery/docs/analytics-hub-introduction#data_exchanges) that you can access.

2.  In the list of data exchanges, click the name of the data exchange that contains the subscriptions that you want to list.

3.  Click the **Subscriptions** tab.

### API

To list subscriptions for listings in a particular data exchange, call the [`projects.locations.dataExchanges.listSubscriptions` method](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges/listSubscriptions) :

    GET https://analyticshub.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/dataExchanges/DATAEXCHANGE_ID:listSubscriptions

Replace the following:

  - `  PROJECT_ID  ` : the Google Cloud project ID of the project that contains the data exchange.
  - `  LOCATION  ` : the location of the data exchange that contains the subscriptions that you want to list.
  - `  DATAEXCHANGE_ID  ` : the ID of the data exchange for which to list subscriptions.

### Revoke a subscription

When you revoke a subscription as a BigQuery sharing publisher, the subscriber can no longer query the linked dataset. Because you initiate this action on a subscriber-owned resource, the linked dataset remains in the subscriber's project. The subscriber can remove the dataset by deleting it.

When you revoke a subscription from a multi-region listing, subscribers can no longer query any primary or secondary linked dataset replicas.

> **Caution:** Revoking [Cloud Marketplace-integrated commercial subscriptions](https://docs.cloud.google.com/bigquery/docs/analytics-hub-cloud-marketplace) might affect your customers and violate the [Cloud Marketplace Terms of Service](https://cloud.google.com/terms/marketplace/launcher) .

To revoke a subscription, select one of the following options:

### Console

1.  In the Google Cloud console, go to the **Sharing (Analytics Hub)** page.
    
    The page lists all the [data exchanges](https://docs.cloud.google.com/bigquery/docs/analytics-hub-introduction#data_exchanges) that you can access.

2.  In the list of data exchanges, click the name of the data exchange that contains the subscription that you want to revoke.

3.  Click the **Subscriptions** tab.

4.  Select the checkbox next to each subscription that you want to revoke.

5.  Click **Revoke subscriptions** .

### API

To revoke a subscription, call the [`projects.locations.subscriptions.revoke` method](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.subscriptions/revoke) :

    POST https://analyticshub.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/subscriptions/SUBSCRIPTION_ID:revoke

Replace the following:

  - `  PROJECT_ID  ` : the Google Cloud project ID of the project that contains the subscription that you want to revoke.
  - `  LOCATION  ` : the location of the subscription that you want to revoke.
  - `  SUBSCRIPTION_ID  ` : the ID of the subscription that you want to revoke.

## What's next

  - Learn about [BigQuery sharing architecture](https://docs.cloud.google.com/bigquery/docs/analytics-hub-introduction#architecture) .
  - Learn how to [view and subscribe to listings and data exchanges](https://docs.cloud.google.com/bigquery/docs/analytics-hub-view-subscribe-listings) .
  - Learn about [BigQuery sharing user roles](https://docs.cloud.google.com/bigquery/docs/analytics-hub-grant-roles#user_roles) .
  - Learn how to [create datasets](https://docs.cloud.google.com/bigquery/docs/datasets) .
  - Learn about [BigQuery sharing audit logging](https://docs.cloud.google.com/bigquery/docs/analytics-hub-audit-logging) .
