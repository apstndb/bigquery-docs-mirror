---
name: documents/docs.cloud.google.com/bigquery/docs/analytics-hub-manage-exchanges
uri: https://docs.cloud.google.com/bigquery/docs/analytics-hub-manage-exchanges
title: Manage data exchanges
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# Manage data exchanges

You can use data exchanges in BigQuery sharing to share datasets securely across projects, organizations, or with the public. As a BigQuery sharing administrator, you can perform the following tasks:

  - Create, update, view, share, and delete [data exchanges](https://docs.cloud.google.com/bigquery/docs/analytics-hub-introduction#data_exchanges) .
  - Manage access permissions and roles for data exchanges.
  - Make data exchanges publicly discoverable.

To manage listings within a data exchange, see [Manage listings](https://docs.cloud.google.com/bigquery/docs/analytics-hub-manage-listings) .

By default, a data exchange is private. Only users or groups that have access to an exchange can view or subscribe to its listings. You can [make your data exchange public](https://docs.cloud.google.com/bigquery/docs/analytics-hub-manage-exchanges#make-data-exchange-public) . Making your data exchange public lets [Google Cloud users ( `allAuthenticatedUsers` )](https://docs.cloud.google.com/iam/docs/principals-overview#all-authenticated-users) [discover](https://docs.cloud.google.com/bigquery/docs/analytics-hub-view-subscribe-listings#discover-listings) and [subscribe to](https://docs.cloud.google.com/bigquery/docs/analytics-hub-view-subscribe-listings#subscribe-listings) listings.

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

To get the permissions that you need to manage data exchanges, ask your administrator to grant you the [Analytics Hub Admin role](https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.admin) ( `roles/analyticshub.admin` ) IAM role on your project. For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## Create a data exchange

You can create a data exchange to share datasets with specific individuals, groups, or the public. When you create a data exchange, you specify its project, region, display name, and optional settings such as subscriber email logging and public discoverability.

> **Caution:** Avoid creating a data exchange in a Google Cloud project that is protected by a VPC Service Controls perimeter. If you create a data exchange in a perimeter, you must add the appropriate [ingress and egress rules](https://docs.cloud.google.com/bigquery/docs/analytics-hub-vpc-sc-rules#create_a_data_exchange) .

To create a data exchange, follow these steps:

### Console

1.  In the Google Cloud console, go to the **Sharing (Analytics Hub)** page.

2.  Click add\_box **Create exchange** .

3.  In the **Create exchange** dialog, select a **Project** and a **Region** for your data exchange. You can't change the project and region after you create the data exchange.

4.  In the **Display name** field, enter a name for your data exchange.

5.  Optional: Enter values in the following fields:
    
      - **Primary contact** : enter the URL or email address of the primary contact for the data exchange.
      - **Description** : enter a description for the data exchange.

6.  To log the [principal identifiers](https://docs.cloud.google.com/iam/docs/principal-identifiers) of all users who run jobs and queries on linked datasets, click the **Subscriber Email Logging** toggle to the on position. When you turn on this setting, all future listings under the data exchange have subscriber email logging turned on. The logged data is available in the `job_principal_subject` field of the [`INFORMATION_SCHEMA.SHARED_DATASET_USAGE` view](https://docs.cloud.google.com/bigquery/docs/information-schema-shared-dataset-usage) .
    
    > **Note:** After you enable and save email logging, you can't edit this setting. To disable email logging, delete the data exchange and create a new data exchange without clicking the **Subscriber Email Logging** to the on position.

7.  To make the exchange publicly discoverable, click the **Public Discoverability** toggle to the on position. When an exchange is publicly discoverable, all listings in the exchange appear and are searchable in the catalog. Consider the following factors when you enable public discoverability:
    
      - **Listing inheritance** : all listings inherit the public discoverability setting of the data exchange by default. Public exchanges can't have private listings, but private exchanges can have public listings. You can configure the public discoverability type at the individual listing level.
      - **Permissions** : if you enable public discoverability, configure the exchange permissions to grant the [Analytics Hub Viewer role](https://docs.cloud.google.com/bigquery/docs/analytics-hub-grant-roles#ah-subscriber-role) ( `roles/analyticshub.viewer` ) to `allUsers` or `allAuthenticatedUsers` .
      - **Project requirements** : the project where you create the data exchange must have an associated organization and billing account.

8.  To create the data exchange, click **Create exchange** .

9.  Optional: In the **Exchange Permissions** section, complete the following steps:
    
    1.  In the following fields, enter email addresses to grant Identity and Access Management (IAM) roles:
        
          - **Administrators** : assign the [Analytics Hub Admin role](https://docs.cloud.google.com/bigquery/docs/analytics-hub-grant-roles#ah-admin-role) ( `roles/analyticshub.admin` ) to these users.
          - **Publishers** : assign the [Analytics Hub Publisher role](https://docs.cloud.google.com/bigquery/docs/analytics-hub-grant-roles#ah-publisher-role) ( `roles/analyticshub.publisher` ) to these users. For more information about the tasks that BigQuery sharing publishers can perform, see [Manage listings](https://docs.cloud.google.com/bigquery/docs/analytics-hub-manage-listings) .
          - **Subscribers** : assign the [Analytics Hub Subscriber role](https://docs.cloud.google.com/bigquery/docs/analytics-hub-grant-roles#ah-subscriber-role) ( `roles/analyticshub.subscriber` ) to these users. For more information about the tasks that BigQuery sharing subscribers can perform, see [View and subscribe to listings and data exchanges](https://docs.cloud.google.com/bigquery/docs/analytics-hub-view-subscribe-listings) .
          - **Viewers** : assign the Analytics Hub Viewer role ( `roles/analyticshub.viewer` ) to these users. BigQuery sharing viewers can [view listings](https://docs.cloud.google.com/bigquery/docs/analytics-hub-view-subscribe-listings#discover-listings) . If public discoverability is enabled, grant the Analytics Hub Viewer role to `allUsers` or `allAuthenticatedUsers` .
    
    2.  To save permissions, click **Set permissions** .

10. If you didn't set permissions for your data exchange, click **Skip** .

### API

To create a data exchange, use the [`projects.locations.dataExchanges.create` method](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges/create) :

    POST https://analyticshub.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/dataExchanges?dataExchangeId=DATAEXCHANGE_ID

Replace the following:

  - `  PROJECT_ID  ` : the ID of the project where you want to create the data exchange.
  - `  LOCATION  ` : the location for your data exchange. For more information about regions that support BigQuery sharing, see [Supported regions](https://docs.cloud.google.com/bigquery/docs/analytics-hub-introduction#supported-regions) .
  - `  DATAEXCHANGE_ID  ` : the ID of your data exchange.

In the body of the request, provide the [data exchange details](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges#resource:-dataexchange) .

If the request is successful, the response body contains the details of the data exchange.

If you enable subscriber email logging with the `logLinkedDatasetQueryUserEmail` field, the data exchange response contains `log_linked_dataset_query_user_email: true` . The logged data is available in the `job_principal_subject` field of the [`INFORMATION_SCHEMA.SHARED_DATASET_USAGE` view](https://docs.cloud.google.com/bigquery/docs/information-schema-shared-dataset-usage) .

For more information about the tasks that you can perform on data exchanges using APIs, see [`projects.locations.dataExchanges` methods](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges#methods) .

## Update a data exchange

You can update the configuration of an existing data exchange, such as its display name, description, primary contact, and public discoverability settings. You can't change the project or region of an existing data exchange.

To update a data exchange, follow these steps:

### Console

1.  In the Google Cloud console, go to the **Sharing (Analytics Hub)** page.

2.  In the list of data exchanges, select the data exchange that you want to update.

3.  Click the **Details** tab.

4.  Click mode\_edit **Edit exchange** .

5.  In the **Edit exchange** dialog, update the following fields:
    
      - **Display name** : enter a new display name.
    
      - **Primary contact** : enter an updated URL or email address.
    
      - **Description** : enter an updated description.
    
      - **Public discoverability** : turn public discoverability on or off.
        
          - If you turn public discoverability on, grant the [Analytics Hub Viewer role](https://docs.cloud.google.com/bigquery/docs/analytics-hub-grant-roles#ah-subscriber-role) ( `roles/analyticshub.viewer` ) to `allUsers` or `allAuthenticatedUsers` .
          - If you turn public discoverability off, remove the Analytics Hub Viewer role ( `roles/analyticshub.viewer` ) from `allUsers` or `allAuthenticatedUsers` . Public exchanges can't have private listings, but private exchanges can have public listings.
    
      - **Subscriber Email Logging** : turn subscriber email logging on or off.
        
        > **Note:** After you enable and save email logging, you can't edit this setting. To disable email logging, delete the data exchange and create a new data exchange without clicking the **Subscriber Email Logging** to the on position.

6.  To apply your changes, click **Save** .

### API

To update a data exchange, use the [`projects.locations.dataExchanges.patch` method](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges/patch) :

    PATCH https://analyticshub.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/dataExchanges/DATAEXCHANGE_ID?updateMask=UPDATEMASK

Replace the following:

  - `  PROJECT_ID  ` : the ID of the project that contains the data exchange.
  - `  LOCATION  ` : the location of your data exchange.
  - `  DATAEXCHANGE_ID  ` : the ID of your data exchange.
  - `  UPDATEMASK  ` : a comma-separated list of fields that you want to update (for example, `displayName,primaryContact` ).

In the body of the request, specify updated values for any of the following fields:

  - `displayName`
  - `description`
  - `primaryContact`
  - `documentation`
  - `icon`
  - `discoveryType`
  - `logLinkedDatasetQueryUserEmail`

For more information about these fields, see [Resource: DataExchange](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges#resource:-dataexchange) .

For more information about the tasks that you can perform on data exchanges using APIs, see [`projects.locations.dataExchanges` methods](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges#methods) .

## View data exchanges

You can view the list of data exchanges in your Google Cloud project or organization that you have permission to access.

To view data exchanges, follow these steps:

### Console

1.  In the Google Cloud console, go to the **Sharing (Analytics Hub)** page.

2.  In the list of data exchanges, view the data exchanges displayed for your Google Cloud project. If you have the `resourcemanager.organizations.get` permission, you can also view data exchanges across your Google Cloud organization.

### API

To view data exchanges in your project, use the [`projects.locations.dataExchanges.list` method](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges/list) :

    GET https://analyticshub.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/dataExchanges

Replace the following:

  - `  PROJECT_ID  ` : the ID of the project where you want to list data exchanges.
  - `  LOCATION  ` : the location where you want to list existing data exchanges.

To view data exchanges in your organization, use the [`organizations.locations.dataExchanges.list` method](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/organizations.locations.dataExchanges/list) :

    GET https://analyticshub.googleapis.com/v1/organizations/ORGANIZATION_ID/locations/LOCATION/dataExchanges

Replace the following:

  - `  ORGANIZATION_ID  ` : the organization ID. For more information, see [Get your organization ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-organization#retrieving_your_organization_id) .
  - `  LOCATION  ` : the location where you want to list existing data exchanges.

## Share a data exchange

If a BigQuery sharing publisher belongs to a different organization from the organization that contains the data exchange, they can't browse or [view your data exchange](https://docs.cloud.google.com/bigquery/docs/analytics-hub-manage-exchanges#view_data_exchanges) in BigQuery sharing. To let the publisher access the data exchange, you can copy and share a direct link.

To share a link to a data exchange, follow these steps:

1.  In the Google Cloud console, go to the **Sharing (Analytics Hub)** page.

2.  In the list of data exchanges, find the data exchange that you want to share, and then click more\_vert **More options** .

3.  To copy the link to your clipboard, click content\_copy **Copy share link** .

## Give users access to a data exchange

To give users access to a data exchange, set the IAM policy for that data exchange. For more information about predefined IAM user roles, see [BigQuery sharing IAM roles](https://docs.cloud.google.com/bigquery/docs/analytics-hub-grant-roles#user_roles) .

> **Note:** When managing access for users in [external identity providers](https://docs.cloud.google.com/iam/docs/workforce-identity-federation) , replace instances of Google Account principal identifiers—like `user:kiran@example.com` , `group:support@example.com` , and `domain:example.com` —with appropriate [Workforce Identity Federation principal identifiers](https://docs.cloud.google.com/iam/docs/principal-identifiers) .

### Console

1.  In the Google Cloud console, go to the **Sharing (Analytics Hub)** page.

2.  Click the name of the data exchange that you want to set permissions for.

3.  Click the **Details** tab.

4.  Click person **Set permissions** .

5.  To add principals, click person\_add **Add principal** .

6.  In the **New principals** field, enter the email address of the principal that you want to grant access to. You can also use `allUsers` to make a resource public and accessible to everyone on the internet, or `allAuthenticatedUsers` to make it accessible only to signed-in Google users.

7.  In the **Select a role** list, hold the pointer over **Analytics Hub** , and then select one of the following IAM roles:
    
      - **Analytics Hub Admin**
      - **Analytics Hub Listing Admin**
      - **Analytics Hub Publisher**
      - **Analytics Hub Subscriber**
      - **Analytics Hub Subscription Owner**
      - **Analytics Hub Viewer**

8.  Click **Save** .

### API

1.  To read the existing policy, use the [`projects.locations.dataExchanges.getIamPolicy` method](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges/getIamPolicy) :
    
        POST https://analyticshub.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/dataExchanges/DATAEXCHANGE_ID:getIamPolicy
    
    Replace the following:
    
      - `  PROJECT_ID  ` : the project ID—for example, `my-project-1` .
      - `  LOCATION  ` : the location for your data exchange. Use lowercase letters.
      - `  DATAEXCHANGE_ID  ` : the data exchange ID.
    
    BigQuery sharing returns the current policy.

2.  To add or remove members and their associated IAM roles, edit the policy with a text editor. Use the following format to add members:
    
      - `user:test-user@gmail.com`
      - `group:admins@googlegroups.com`
      - `serviceAccount:server@example.gserviceaccount.com`
      - `domain:example.com`
    
    For example, to grant the `roles/analyticshub.subscriber` role to `group:subscribers@googlegroups.com` , add the following binding to the policy:
    
        {
         "members": [
           "group:subscribers@googlegroups.com"
         ],
         "role":"roles/analyticshub.subscriber"
        }

3.  To set the policy for the data exchange, use the [`projects.locations.dataExchanges.setIamPolicy` method](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges/setIamPolicy) . In the request body, provide the updated IAM policy from the previous step:
    
        POST https://analyticshub.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/dataExchanges/DATAEXCHANGE_ID:setIamPolicy

### Create BigQuery sharing administrators

To delegate data exchange management, you can create data exchange administrators by granting users the [Analytics Hub Admin role](https://docs.cloud.google.com/bigquery/docs/analytics-hub-grant-roles#ah-admin-role) ( `roles/analyticshub.admin` ) at the project or data exchange level.

  - To let administrators manage all data exchanges in a project, [grant them the Analytics Hub Admin role for that project](https://docs.cloud.google.com/bigquery/docs/analytics-hub-grant-roles#grant-role-project) .
  - To let administrators manage a specific data exchange only, [grant them the Analytics Hub Admin role for that data exchange](https://docs.cloud.google.com/bigquery/docs/analytics-hub-grant-roles#grant-role-data-exchange) .

## Make a data exchange public

By default, a data exchange is private. Only users or groups that have access to an exchange can view or subscribe to its listings. You can make a data exchange public, which lets [Google Cloud users ( `allAuthenticatedUsers` )](https://docs.cloud.google.com/iam/docs/principals-overview#all-authenticated-users) discover and subscribe to its listings.

To make a data exchange public, follow these steps:

1.  To let `allAuthenticatedUsers` [view listings](https://docs.cloud.google.com/bigquery/docs/analytics-hub-view-subscribe-listings#discover-listings) , grant them the [Analytics Hub Viewer role](https://docs.cloud.google.com/bigquery/docs/analytics-hub-grant-roles#ah-subscriber-role) ( `roles/analyticshub.viewer` ) at the data exchange level.

2.  To let `allAuthenticatedUsers` [subscribe to listings](https://docs.cloud.google.com/bigquery/docs/analytics-hub-view-subscribe-listings#subscribe-listings) , grant them the [Analytics Hub Subscriber role](https://docs.cloud.google.com/bigquery/docs/analytics-hub-grant-roles#ah-subscriber-role) ( `roles/analyticshub.subscriber` ) at the data exchange level.

3.  When you [create](https://docs.cloud.google.com/bigquery/docs/analytics-hub-manage-exchanges#create-exchange) or [update](https://docs.cloud.google.com/bigquery/docs/analytics-hub-manage-exchanges#update-exchange) a data exchange, click the **Public Discoverability** toggle to the on position.

> **Note:** You can also convert a public data exchange to private. To do so, remove `allAuthenticatedUsers` and the associated BigQuery sharing roles from the permissions list for your data exchange, and disable public discoverability in the exchange settings.

## Delete a data exchange

When you delete a data exchange, all listings within the exchange are also deleted. Shared and linked datasets aren't deleted. Deleting a project doesn't automatically delete its data exchanges, so you must delete all data exchanges before [shutting down the project](https://docs.cloud.google.com/resource-manager/docs/delete-restore-projects#shutting_down_projects) . You can't undo a data exchange deletion.

Before you delete a data exchange, complete the following prerequisites based on the data exchange configuration:

  - For data exchanges with Google Cloud Marketplace-integrated commercial listings, [offboard the Cloud Marketplace-integrated listings](https://docs.cloud.google.com/bigquery/docs/analytics-hub-cloud-marketplace#offboard-listing) .
  - For data exchanges with listings for multiple regions, [revoke all active subscriptions](https://docs.cloud.google.com/bigquery/docs/analytics-hub-manage-subscriptions#revoke-subscription) .

To delete a data exchange, follow these steps:

### Console

1.  In the Google Cloud console, go to the **Sharing (Analytics Hub)** page.

2.  In the list of data exchanges, select the data exchange that you want to delete.

3.  Click the **Details** tab.

4.  Click delete **Delete exchange** .

5.  In the **Delete exchange?** dialog, confirm deletion by entering `delete` .

6.  To permanently delete the data exchange, click **Delete** .

### API

To delete a data exchange, use the [`projects.locations.dataExchanges.delete` method](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges/delete) :

    DELETE https://analyticshub.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/dataExchanges/DATAEXCHANGE_ID

Replace the following:

  - `  PROJECT_ID  ` : the ID of the project that contains the data exchange.
  - `  LOCATION  ` : the location for your data exchange. For more information about regions that support BigQuery sharing, see [Supported regions](https://docs.cloud.google.com/bigquery/docs/analytics-hub-introduction#supported-regions) .
  - `  DATAEXCHANGE_ID  ` : the ID of your data exchange.

For more information about the tasks that you can perform on data exchanges using APIs, see [`projects.locations.dataExchanges` methods](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges#methods) .

## What's next

  - Learn how to [manage listings](https://docs.cloud.google.com/bigquery/docs/analytics-hub-manage-listings) .
  - Learn how to [grant BigQuery sharing user roles](https://docs.cloud.google.com/bigquery/docs/analytics-hub-grant-roles) .
  - Learn how to [view and subscribe to listings and data exchanges](https://docs.cloud.google.com/bigquery/docs/analytics-hub-view-subscribe-listings) .
  - Learn how to [view BigQuery sharing audit logs](https://docs.cloud.google.com/bigquery/docs/analytics-hub-audit-logging) .
