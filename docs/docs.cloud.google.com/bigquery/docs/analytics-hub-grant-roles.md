---
name: documents/docs.cloud.google.com/bigquery/docs/analytics-hub-grant-roles
uri: https://docs.cloud.google.com/bigquery/docs/analytics-hub-grant-roles
title: Configure BigQuery sharing roles
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# Configure BigQuery sharing roles

To manage access to your BigQuery sharing data exchanges and listings, grant specific Identity and Access Management (IAM) roles for BigQuery sharing (formerly Analytics Hub). By assigning these roles, you control permissions for your data and help ensure that only authorized users can discover, subscribe to, and manage your data sharing resources.

> **Note:** When managing access for users in [external identity providers](https://docs.cloud.google.com/iam/docs/workforce-identity-federation) , replace instances of Google Account principal identifiers—like `user:kiran@example.com` , `group:support@example.com` , and `domain:example.com` —with appropriate [Workforce Identity Federation principal identifiers](https://docs.cloud.google.com/iam/docs/principal-identifiers) .

## BigQuery sharing IAM roles

The following sections describe the predefined BigQuery sharing user roles. Assign these roles to control access to your data exchanges and listings.

### Analytics Hub Admin role

To [manage data exchanges](https://docs.cloud.google.com/bigquery/docs/analytics-hub-manage-exchanges) , BigQuery sharing provides the [Analytics Hub Admin role](https://docs.cloud.google.com/bigquery/docs/access-control#analyticshub.admin) ( `roles/analyticshub.admin` ) that you can grant for a project or a data exchange. This role lets you do the following:

  - Create, update, and delete data exchanges.
  - Create, update, delete, and share listings.
  - Manage BigQuery sharing administrators, listing administrators, publishers, subscribers, and viewers.

With this role, you become a *BigQuery sharing administrator* .

### Analytics Hub Publisher and Listing Admin roles

To [manage listings](https://docs.cloud.google.com/bigquery/docs/analytics-hub-manage-listings) , BigQuery sharing provides the following predefined roles that you can grant for a project, a data exchange, or a listing:

  - [Analytics Hub Publisher role](https://docs.cloud.google.com/bigquery/docs/access-control#analyticshub.publisher) ( `roles/analyticshub.publisher` ), which lets you do the following:
    
      - Create, update, and delete listings.
      - [Set IAM policies on listings](https://docs.cloud.google.com/bigquery/docs/analytics-hub-grant-roles#grant-role-listing) .
    
    With this role, you become a *BigQuery sharing publisher* .

  - [Analytics Hub Listing Admin role](https://docs.cloud.google.com/bigquery/docs/access-control#analyticshub.listingAdmin) ( `roles/analyticshub.listingAdmin` ), which lets you do the following:
    
      - Update and delete listings.
      - [Set IAM policies on listings](https://docs.cloud.google.com/bigquery/docs/analytics-hub-grant-roles#grant-role-listing) .
    
    With this role, you become a *BigQuery sharing listing administrator* .

### Analytics Hub Subscriber and Viewer roles

To [view and subscribe to listings and data exchanges](https://docs.cloud.google.com/bigquery/docs/analytics-hub-view-subscribe-listings) , BigQuery sharing provides the following predefined roles that you can grant for a project, a data exchange, or a listing:

  - [Analytics Hub Subscriber role](https://docs.cloud.google.com/bigquery/docs/access-control#analyticshub.subscriber) ( `roles/analyticshub.subscriber` ), which lets you view and subscribe to listings.
    
    With this role, you become a *BigQuery sharing subscriber* .

  - [Analytics Hub Viewer role](https://docs.cloud.google.com/bigquery/docs/access-control#analyticshub.viewer) ( `roles/analyticshub.viewer` ), which lets you view listings and data exchange permissions.
    
    With this role, you become a *BigQuery sharing viewer* .

### Analytics Hub Subscription Owner role

To [manage subscriptions](https://docs.cloud.google.com/bigquery/docs/analytics-hub-manage-subscriptions) , BigQuery sharing provides the following predefined role that you can grant for a project:

  - [Analytics Hub Subscription Owner role](https://docs.cloud.google.com/bigquery/docs/access-control#analyticshub.subscriptionOwner) ( `roles/analyticshub.subscriptionOwner` ), which lets you manage subscriptions.

With this role, you become a *BigQuery sharing subscription owner* .

## Grant BigQuery sharing IAM roles

You can grant IAM roles at the following levels of the resource hierarchy:

  - **Project.** If you grant a role for a project, it applies to all data exchanges and listings in that project.
  - **Data exchange.** If you grant a role for a data exchange, it applies to all listings in that data exchange.
  - **Listing.** If you grant a role for a listing, it applies only to that specific listing.

### Grant roles for a project

To set IAM policies on a project, you must have the [Project IAM Admin role](https://docs.cloud.google.com/iam/docs/roles-permissions/resourcemanager#resourcemanager.projectIamAdmin) ( `roles/resourcemanager.projectIamAdmin` ) on that project. To grant the predefined BigQuery sharing IAM roles for a project, select one of the following options:

### Console

1.  In the Google Cloud console, go to the **IAM** page.

2.  Click person\_add **Grant access** .

3.  In the **New principals** field, enter the email address of the principal that you want to grant access to. You can specify any of the following principal types:
    
      - Google Account email address: `test-user@gmail.com`
      - Google group: `admins@googlegroups.com`
      - Service account: `server@example.gserviceaccount.com`
      - Google Workspace domain: `example.com`

4.  In the **Select a role** list, hold the pointer over **Analytics Hub** , and then select one of the following roles:
    
      - **Analytics Hub Admin**
      - **Analytics Hub Listing Admin**
      - **Analytics Hub Publisher**
      - **Analytics Hub Subscriber**
      - **Analytics Hub Subscription Owner**
      - **Analytics Hub Viewer**

5.  Optional: To further control access to Google Cloud resources, [add a conditional role binding](https://docs.cloud.google.com/iam/docs/managing-conditional-role-bindings#add) .

6.  Click **Save** .

### gcloud

To grant roles for a project, use the [`gcloud projects add-iam-policy-binding` command](https://docs.cloud.google.com/sdk/gcloud/reference/projects/add-iam-policy-binding) :

    gcloud projects add-iam-policy-binding PROJECT_ID \
        --member='PRINCIPAL' \
        --role='roles/analyticshub.admin'

Replace the following:

  - `  PROJECT_ID  ` : the project ID—for example, `my-project-1` .

  - `  PRINCIPAL  ` : a valid principal that you want to grant the role to. You can specify any of the following principal types:
    
      - Google Account email address: `user:test-user@gmail.com`
      - Google group: `group:admins@googlegroups.com`
      - Service account: `serviceAccount:server@example.gserviceaccount.com`
      - Google Workspace domain: `domain:example.com`

### API

1.  To read the existing policy, use the [`projects.getIamPolicy` method](https://docs.cloud.google.com/resource-manager/reference/rest/v1/projects/getIamPolicy) :
    
        POST https://cloudresourcemanager.googleapis.com/v1/projects/PROJECT_ID:getIamPolicy
    
    Replace `  PROJECT_ID  ` with the project ID—for example, `my-project-1` .

2.  To add principals and their associated roles, edit the policy with a text editor. Use the following format to add members:
    
      - `user:test-user@gmail.com`
      - `group:admins@googlegroups.com`
      - `serviceAccount:server@example.gserviceaccount.com`
      - `domain:example.com`
    
    For example, to grant the `roles/analyticshub.admin` role to `group:admins@googlegroups.com` , add the following binding to the policy:
    
        {
         "members": [
           "group:admins@googlegroups.com"
         ],
         "role":"roles/analyticshub.admin"
        }

3.  To set a policy for a project, use the [`projects.setIamPolicy` method](https://docs.cloud.google.com/resource-manager/reference/rest/v1/projects/setIamPolicy) . In the request body, provide the updated IAM policy from the previous step:
    
        POST https://cloudresourcemanager.googleapis.com/v1/projects/PROJECT_ID:setIamPolicy
    
    Replace `  PROJECT_ID  ` with the project ID—for example, `my-project-1` .

You can update and delete project roles using the same IAM panel.

### Grant roles for a data exchange

When you grant permissions for a data exchange, you must use lowercase letters for the location in the resource name. Using uppercase or mixed-case values can cause permission denied errors.

The following examples show valid and invalid resource name formats:

  - Use: `projects/myproject/locations/us/dataExchanges/123`
  - Avoid: `projects/myproject/locations/US/dataExchanges/123`
  - Avoid: `projects/myproject/locations/Eu/dataExchanges/123`

To grant roles for a data exchange, select one of the following options:

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

You can update and delete data exchange roles using the same IAM panel.

### Grant roles for a listing

When you grant permissions for a listing, you must use lowercase letters for the location in the resource name. Using uppercase or mixed-case values can cause permission denied errors.

The following examples show valid and invalid resource name formats:

  - Use: `projects/myproject/locations/us/dataExchanges/123/listings/456`
  - Avoid: `projects/myproject/locations/US/dataExchanges/123/listings/456`
  - Avoid: `projects/myproject/locations/Eu/dataExchanges/123/listings/456`

To grant roles for a listing, select one of the following options:

### Console

1.  In the Google Cloud console, go to the **Sharing (Analytics Hub)** page.

2.  Click the name of the data exchange that contains the listing.

3.  Click the listing that you want to set permissions for.

4.  Click person **Set permissions** .

5.  To add principals, click person\_add **Add principal** .

6.  In the **New principals** field, enter the email address of the principal that you want to grant access to.

7.  In the **Select a role** list, hold the pointer over **Analytics Hub** , and then select one of the following IAM roles:
    
      - **Analytics Hub Admin**
      - **Analytics Hub Listing Admin**
      - **Analytics Hub Publisher**
      - **Analytics Hub Subscriber**
      - **Analytics Hub Subscription Owner**
      - **Analytics Hub Viewer**

8.  Click **Save** .

### API

1.  To read the existing policy, use the [`projects.locations.dataExchanges.listings.getIamPolicy` method](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings/getIamPolicy) :
    
        POST https://analyticshub.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/dataExchanges/DATAEXCHANGE_ID/listings/LISTING_ID:getIamPolicy
    
    Replace the following:
    
      - `  PROJECT_ID  ` : the project ID—for example, `my-project-1` .
      - `  LOCATION  ` : the location of the data exchange that contains the listing. Use lowercase letters.
      - `  DATAEXCHANGE_ID  ` : the data exchange ID.
      - `  LISTING_ID  ` : the listing ID.
    
    BigQuery sharing returns the current policy.

2.  To add or remove members and their associated IAM roles, edit the policy with a text editor. Use the following format to add members:
    
      - `user:test-user@gmail.com`
      - `group:admins@googlegroups.com`
      - `serviceAccount:server@example.gserviceaccount.com`
      - `domain:example.com`
    
    For example, to grant the `roles/analyticshub.publisher` role to `group:publishers@googlegroups.com` , add the following binding to the policy:
    
        {
         "members": [
           "group:publishers@googlegroups.com"
         ],
         "role":"roles/analyticshub.publisher"
        }

3.  To set the policy for the listing, use the [`projects.locations.dataExchanges.listings.setIamPolicy` method](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings/setIamPolicy) . In the request body, provide the updated IAM policy from the previous step:
    
        POST https://analyticshub.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/dataExchanges/DATAEXCHANGE_ID/listings/LISTING_ID:setIamPolicy

You can update and delete listing roles using the same IAM panel.

## What's next

  - Learn more about [BigQuery sharing roles and permissions](https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub) .
  - Learn about [BigQuery sharing](https://docs.cloud.google.com/bigquery/docs/analytics-hub-introduction) .
  - Learn how to [manage data exchanges](https://docs.cloud.google.com/bigquery/docs/analytics-hub-manage-exchanges) .
  - Learn how to [manage listings](https://docs.cloud.google.com/bigquery/docs/analytics-hub-manage-listings) .
  - Learn how to [view and subscribe to listings and data exchanges](https://docs.cloud.google.com/bigquery/docs/analytics-hub-view-subscribe-listings) .
