---
name: documents/docs.cloud.google.com/bigquery/docs/analytics-hub-manage-listings
uri: https://docs.cloud.google.com/bigquery/docs/analytics-hub-manage-listings
title: Manage listings
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# Manage listings

As a data publisher in BigQuery sharing (formerly Analytics Hub), you can create and manage listings to securely share datasets with subscribers across organizations without copying data.

When you manage listings, you can perform the following tasks:

  - Create, update, share, and delete listings in any data exchange where you have publishing access.
  - Manage access by assigning BigQuery sharing roles to administrators, subscribers, and viewers.
  - View, monitor, and remove subscribers from your listings.
  - [Monitor subscription usage metrics](https://docs.cloud.google.com/bigquery/docs/analytics-hub-monitor-listings#use-analytics-hub) .

A listing is a reference to a shared dataset that a publisher lists in a [data exchange](https://docs.cloud.google.com/bigquery/docs/analytics-hub-introduction#data_exchanges) . Depending on the Identity and Access Management (IAM) policy that's set for the listing and the type of data exchange that contains the listing, a listing can be one of the following two types:

  - **Public listing.** A public listing can be [discovered](https://docs.cloud.google.com/bigquery/docs/analytics-hub-view-subscribe-listings#discover-listings) and [subscribed to](https://docs.cloud.google.com/bigquery/docs/analytics-hub-view-subscribe-listings#subscribe-listings) by [Google Cloud users ( `allAuthenticatedUsers` )](https://docs.cloud.google.com/iam/docs/principals-overview#all-authenticated-users) . Listings in a public data exchange are public listings. These listings can be references to a *free public dataset* or a *commercial dataset* . If the listing references a commercial dataset, subscribers can request access to the listing directly from the data provider, or they can browse and purchase [Google Cloud Marketplace-integrated commercial listings](https://docs.cloud.google.com/bigquery/docs/analytics-hub-cloud-marketplace) .

  - **Private listing.** A private listing is shared directly with individuals or groups. For example, a private listing can reference a marketing metrics dataset that you share with internal teams in your organization. Even if you [let all Google Cloud users ( `allAuthenticatedUsers` )](https://docs.cloud.google.com/bigquery/docs/analytics-hub-manage-listings#give_users_access_to_a_listing) subscribe to your private listing, the listing remains private. It doesn't [show as a public listing on the BigQuery sharing page](https://docs.cloud.google.com/bigquery/docs/analytics-hub-view-subscribe-listings#discover-listings) . To share a private listing with users, send those users the listing URL. To make a private listing publicly discoverable, [make the data exchange public](https://docs.cloud.google.com/bigquery/docs/analytics-hub-manage-exchanges#make-data-exchange-public) .

> **Note:** Both requesting access and Cloud Marketplace-integrated flows are supported on a single BigQuery sharing listing. As a result, you can create a Cloud Marketplace-integrated listing from an existing (offline) commercial listing, without any disruptions to existing subscriptions.

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

To manage listings and subscriptions, you must have one of the following BigQuery sharing Identity and Access Management (IAM) roles:

  - [Analytics Hub Publisher role](https://docs.cloud.google.com/bigquery/docs/access-control#analyticshub.publisher) ( `roles/analyticshub.publisher` ), which lets you create, update, delete, and set IAM policies on your listings.

  - [Analytics Hub Listing Admin role](https://docs.cloud.google.com/bigquery/docs/access-control#analyticshub.listingAdmin) ( `roles/analyticshub.listingAdmin` ), which lets you update, delete, and set IAM policies on your listings.

  - [Analytics Hub Admin role](https://docs.cloud.google.com/bigquery/docs/access-control#analyticshub.admin) ( `roles/analyticshub.admin` ), which lets you create, update, delete, and set IAM policies on all listings in your data exchange.

For more information, see [BigQuery sharing IAM roles](https://docs.cloud.google.com/bigquery/docs/analytics-hub-grant-roles#user_roles) . To learn how to grant these roles to other users, see [Create a listing administrator](https://docs.cloud.google.com/bigquery/docs/analytics-hub-manage-listings#create-listing-administrator) .

To create listings or update replica regions for a listing, you must have the `bigquery.datasets.get` and `bigquery.datasets.update` permissions on the source datasets. The following [BigQuery predefined roles](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery) include the `bigquery.datasets.update` permission:

  - [BigQuery Data Owner](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataOwner) ( `roles/bigquery.dataOwner` )
  - [BigQuery Admin](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.admin) ( `roles/bigquery.admin` )

To view all data exchanges across projects in an organization that you have access to, you must have the `resourcemanager.organizations.get` permission. There are no BigQuery predefined roles that contain this permission, so you must use an [IAM custom role](https://docs.cloud.google.com/iam/docs/creating-custom-roles) .

## View data exchanges

To view the list of data exchanges in your organization that you can access, see [View data exchanges](https://docs.cloud.google.com/bigquery/docs/analytics-hub-manage-exchanges#view_data_exchanges) . If the data exchange is in another organization, then the BigQuery sharing administrator must [share a data exchange link](https://docs.cloud.google.com/bigquery/docs/analytics-hub-manage-exchanges#share_a_data_exchange) with you.

## Create a listing

A listing is a reference to a [shared dataset](https://docs.cloud.google.com/bigquery/docs/analytics-hub-introduction#shared_datasets) that a BigQuery sharing publisher lists in a data exchange.

> **Caution:** We recommend that you don't create shared datasets in a Google Cloud project that uses a VPC Service Controls service perimeter. If you must use a service perimeter, then you must configure the required [ingress and egress rules](https://docs.cloud.google.com/bigquery/docs/analytics-hub-vpc-sc-rules#create_a_listing) .

To create a listing, follow these steps:

### Console

1.  Go to the **Sharing (Analytics Hub)** page.
    
    A page appears that lists all data exchanges that you can access.

2.  Click the data exchange name where you want to create the listing.

3.  Click add\_box **Create listing** .

4.  In the **Configure data** section, in the **Resource type** menu, select **BigQuery dataset** or **Pub/Sub Topic** .
    
      - If you select **BigQuery dataset** , then do the following:
        
        1.  In the **Shared dataset** menu, select an existing dataset, or click **Create a dataset** to create a dataset. The dataset must be in the same region as the data exchange. You can't change the shared dataset after you create the listing. When subscribers [view the metadata of their linked dataset](https://docs.cloud.google.com/bigquery/docs/analytics-hub-view-subscribe-listings#view-table-metadata) , BigQuery sharing returns the source dataset name and the ID of the project that contains the dataset.
        
        2.  Optional: To let subscribers [share a SQL stored procedure across listings](https://docs.cloud.google.com/bigquery/docs/analytics-hub-manage-listings#share-stored-procedure-in-listing) , select **Allow stored procedure sharing** ( [Preview](https://docs.cloud.google.com/products#product-launch-stages) ).
        
        3.  To make the shared dataset available in additional regions, expand the **Region data availability** menu. The menu displays regions that have existing dataset replicas labeled as **Ready to use** . Before you configure the listing for multiple regions, verify that you enabled [cross-region dataset replication](https://docs.cloud.google.com/bigquery/docs/data-replication#use_dataset_replication) on the shared dataset. You can select only regions where cross-region dataset replication is turned on; all other regions are labeled as **Unavailable** . If you select no additional region, the listing defaults to the primary region of the shared dataset, which is labeled as **Provider primary** .
        
        4.  In **Data Egress controls** , select the appropriate data egress option:
            
              - To restrict data copy and export on your shared dataset while allowing exports of query results, select **Disable copy and export of shared data** .
              - To restrict data copy and export on both your shared dataset and query results, select **Disable copy and export of query results** . This option also selects **Disable copy and export of shared data** .
              - To restrict table copy and export through APIs on your shared dataset, select **Disable copy and export of tables through APIs** . This option also selects **Disable copy and export of shared data** .
            
            For more information about data egress controls, including restrictions, see [Data egress options (BigQuery shared datasets only)](https://docs.cloud.google.com/bigquery/docs/analytics-hub-introduction#data_egress) .
    
      - If you select **Pub/Sub Topic** , then in the **Shared topic** menu, select an existing Pub/Sub topic, or click **Create a topic** to create a topic.

5.  In the **Listing details** section, in **Display name** , enter a name for the listing.

6.  Enter the following optional details:
    
      - **Category** : select up to two categories that best represent your listing. Subscribers can [filter listings](https://docs.cloud.google.com/bigquery/docs/analytics-hub-view-subscribe-listings#discover-listings) using your selected categories.
    
      - **Data affinity** : specify the regions that you use for publishing data. This location setting helps subscribers minimize or avoid Pub/Sub network egress costs by reading data from the same region. For more information about egress costs, see [Data transfer costs](https://cloud.google.com/pubsub/pricing#egress_costs) .
    
      - **Icon** : upload an icon for your listing. PNG and JPEG file formats are supported. Icons must be smaller than 512 KiB with maximum dimensions of 512 x 512 pixels.
    
      - **Description** : enter a brief description of your listing. Subscribers can [search for listings](https://docs.cloud.google.com/bigquery/docs/analytics-hub-view-subscribe-listings#discover-listings) by description text.
    
      - **Public discoverability** : turn this setting on to make your listing publicly discoverable in the BigQuery sharing catalog. If you enable this option, grant the [Analytics Hub Viewer role](https://docs.cloud.google.com/bigquery/docs/access-control#analyticshub.viewer) ( `roles/analyticshub.viewer` ) to `allUsers` or `allAuthenticatedUsers` . For more information, see [Grant the role for a listing](https://docs.cloud.google.com/bigquery/docs/analytics-hub-grant-roles#grant-role-listing) . If the exchange is already [public](https://docs.cloud.google.com/bigquery/docs/analytics-hub-manage-exchanges#make-data-exchange-public) , the listing inherits those permissions and requires no further action.
        
        Publicly discoverable exchanges can't have private listings due to permission inheritance, but private exchanges can have public listings. To create a public listing, the project that contains the listing must have an associated organization and billing account. If you create a [Cloud Marketplace-integrated commercial listing](https://docs.cloud.google.com/bigquery/docs/analytics-hub-cloud-marketplace) , we recommend that you turn on public discoverability.
    
      - **Subscriber Email Logging** : turn this setting on to log the [principal identifiers](https://docs.cloud.google.com/iam/docs/principal-identifiers) of all users running jobs and queries on linked datasets. If you turn on this option, all future subscriptions that are created from this listing enable subscriber email logging. The logged data is available in the `job_principal_subject` column of the [`INFORMATION_SCHEMA.SHARED_DATASET_USAGE` view](https://docs.cloud.google.com/bigquery/docs/information-schema-shared-dataset-usage) .
        
        > **Note:** After you turn on and save subscriber email logging, you can't edit this setting. To turn off email logging, delete the listing, and then recreate the listing without selecting **Subscriber email logging** .
    
      - **Documentation \> Markdown** : enter supporting documentation, links, or instructions in Markdown format to help subscribers use your dataset.

7.  In the **Listing contact information** section, enter the following optional details:
    
      - **Primary contact** : enter the email address or URL for the listing's primary contact.
    
      - **Request access contact** : enter the email address or URL of your intake form so that subscribers can contact you to request access.
    
      - **Provider** : expand the **Provider** section and enter details in the following fields:
        
          - **Provider name** : the name of the data provider.
          - **Provider primary contact** : the email address or URL of the data provider's primary contact.
        
        Subscribers can filter listings by data provider.
    
      - **Publisher** : expand the **Publisher** section and enter details in the following fields:
        
          - **Publisher name** : the name of the publisher creating the listing.
          - **Publisher primary contact** : the email address or URL of the publisher's primary contact.

8.  Review the **Listing preview** section.

9.  To publish the listing, click **Publish** .

### API

Use the [`projects.locations.dataExchanges.listings.create` method](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings/create) :

    POST https://analyticshub.googleapis.com/v1/projects/PROJECT_ID/location/LOCATION/dataExchanges/DATAEXCHANGE_ID/listings?listingId=LISTING_ID

Replace the following:

  - `  PROJECT_ID  ` : the ID of the project that contains the data exchange where you want to create the listing.
  - `  LOCATION  ` : the location of your data exchange. For more information about locations that support BigQuery sharing, see [Supported regions](https://docs.cloud.google.com/bigquery/docs/analytics-hub-introduction#supported-regions) .
  - `  DATAEXCHANGE_ID  ` : the data exchange ID.
  - `  LISTING_ID  ` : the listing ID.

In the request body, provide the [listing details](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#resource:-listing) .

To create a listing across multiple regions, specify those regions in the `bigqueryDataset.replicaLocations` field of the request body. Before you configure the listing for multiple regions, verify that you enabled [cross-region dataset replication](https://docs.cloud.google.com/bigquery/docs/data-replication#use_dataset_replication) on the shared dataset. You can select only regions where cross-region dataset replication is enabled. If you omit this optional field, the listing uses the primary region of the shared dataset.

If the request succeeds, the response body returns the listing details. If you turn on subscriber email logging by setting the `logLinkedDatasetQueryUserEmail` field to `true` , the listing response returns `log_linked_dataset_query_user_email: true` . The logged data is available in the `job_principal_subject` column of the [`INFORMATION_SCHEMA.SHARED_DATASET_USAGE` view](https://docs.cloud.google.com/bigquery/docs/information-schema-shared-dataset-usage) .

For more information about the tasks that you can perform on listings using APIs, see [`projects.locations.dataExchanges.listings` methods](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#methods) .

### Create a listing from a dataset

To create a listing directly from an existing dataset, follow these steps:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  To view the dataset details, click a dataset name.

3.  Click person\_add **Sharing** \> **Publish as listing** .
    
    The **Create listing** dialog opens.

4.  Select a data exchange where you want to publish the listing. The data exchange must be in the same region as the dataset. For more information about creating a data exchange, see [create an exchange and set permissions](https://docs.cloud.google.com/bigquery/docs/analytics-hub-manage-exchanges) .

5.  In the **Shared dataset** menu, select an existing dataset, or click **Create a dataset** to create a dataset. The dataset must be in the same region as the data exchange. You can't change this selection after you create the listing.
    
    When subscribers [view the metadata of their linked dataset](https://docs.cloud.google.com/bigquery/docs/analytics-hub-view-subscribe-listings#view-table-metadata) , BigQuery sharing returns the source dataset name and the ID of the project that contains the dataset.

6.  Optional: To let subscribers [share a SQL stored procedure across listings](https://docs.cloud.google.com/bigquery/docs/analytics-hub-manage-listings#share-stored-procedure-in-listing) , select **Allow stored procedure sharing** ( [Preview](https://docs.cloud.google.com/products#product-launch-stages) ).

7.  To make the shared dataset available in additional regions, expand the **Region data availability** menu. The menu displays regions with dataset replicas labeled as **Ready to use** . Before you configure the listing for multiple regions, verify that you enabled [cross-region dataset replication](https://docs.cloud.google.com/bigquery/docs/data-replication#use_dataset_replication) on the shared dataset. You can select only regions where cross-region dataset replication is enabled; all other regions are labeled as **Unavailable** . If you select no additional region, the listing defaults to the primary region of the shared dataset, which is labeled as **Provider primary** .

8.  In **Data egress controls** , select the appropriate data egress option:
    
      - To restrict copy and export on your shared dataset while permitting exports of query results, select **Disable copy and export of shared data** .
      - To restrict copy and export on both your shared dataset and query results, select **Disable copy and export of query results** . This option also selects **Disable copy and export of shared data** .
      - To restrict table copy and export through APIs on your shared dataset, select **Disable copy and export of tables through APIs** . This option also selects **Disable copy and export of shared data** .
    
    For information about data egress controls and restrictions, see [Data egress options (BigQuery shared datasets only)](https://docs.cloud.google.com/bigquery/docs/analytics-hub-introduction#data_egress) .

9.  In the **Listing details** section, in **Display name** , enter a name for the listing.

10. Enter the following optional details:
    
      - **Category** : select up to two categories that best represent your listing. Subscribers can [filter listings](https://docs.cloud.google.com/bigquery/docs/analytics-hub-view-subscribe-listings#discover-listings) using your selected categories.
    
      - **Data affinity** : specify the regions that you use for publishing data. This location setting helps subscribers minimize or avoid Pub/Sub network egress costs by reading data from the same region. For more information about egress costs, see [Data transfer costs](https://cloud.google.com/pubsub/pricing#egress_costs) .
    
      - **Icon** : upload an icon for your listing. PNG and JPEG file formats are supported. Icons must be smaller than 512 KiB with maximum dimensions of 512 x 512 pixels.
    
      - **Description** : enter a brief description of your listing. Subscribers can [search for listings](https://docs.cloud.google.com/bigquery/docs/analytics-hub-view-subscribe-listings#discover-listings) by description text.
    
      - **Public discoverability** : turn this setting on to make your listing publicly discoverable in the BigQuery sharing catalog. If you enable this option, grant `allUsers` or `allAuthenticatedUsers` the Analytics Hub Viewer role ( `roles/analyticshub.viewer` ). For more information, see [Grant the role for a listing](https://docs.cloud.google.com/bigquery/docs/analytics-hub-grant-roles#grant-role-listing) . If the exchange is already [public](https://docs.cloud.google.com/bigquery/docs/analytics-hub-manage-exchanges#make-data-exchange-public) , the listing inherits those permissions and requires no further action.
        
        Publicly discoverable exchanges can't have private listings due to permission inheritance, but private exchanges can have public listings. To create a public listing, the project that contains the listing must have an associated organization and billing account. If you create a [Cloud Marketplace-integrated commercial listing](https://docs.cloud.google.com/bigquery/docs/analytics-hub-cloud-marketplace) , we recommend turning on public discoverability.
    
      - **Subscriber email logging** : turn on to log the [principal identifiers](https://docs.cloud.google.com/iam/docs/principal-identifiers) of subscribers running jobs and queries on this listing's linked dataset for all future subscriptions. When you turn on this option, only newly created subscriptions log principal identifiers. The logged data is available in the `job_principal_subject` column of the [`INFORMATION_SCHEMA.SHARED_DATASET_USAGE` view](https://docs.cloud.google.com/bigquery/docs/information-schema-shared-dataset-usage) .
        
        > **Note:** After you turn on and save subscriber email logging, you can't edit this setting. To turn off email logging, delete the listing, and then recreate the listing without selecting **Subscriber email logging** .
    
      - **Documentation \> Markdown** : enter supporting documentation, links, or instructions to help subscribers use your dataset.

11. In the **Listing contact information** section, enter the following optional details:
    
      - **Primary contact** : enter the email address or URL for the listing's primary contact.
    
      - **Request access contact** : enter the email address or URL of your intake form so that subscribers can contact you to request access.
    
      - **Provider** : expand the **Provider** section and enter details in the following fields:
        
          - **Provider name** : the name of the data provider.
          - **Provider primary contact** : the email address or a URL of the data provider's primary contact.
        
        Subscribers can filter listings by data provider.
    
      - **Publisher** : expand the **Publisher** section and enter details in the following fields:
        
          - **Publisher name** : the name of the publisher creating the listing.
          - **Publisher primary contact** : the email address or URL of the publisher's primary contact.

12. Review the **Listing preview** section.

13. To publish the listing, click **Publish** .

## Share a SQL stored procedure across listings

> **Preview**
> 
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

> **Note:** To request support or provide feedback for this feature, contact <bq-data-sharing-feedback@google.com> .

You can share [SQL stored procedures](https://docs.cloud.google.com/bigquery/docs/procedures) when creating listings with BigQuery datasets. Because stored procedures can create, drop, and manipulate tables, and invoke other stored procedures, sharing stored procedures requires additional authorization.

### Subscriber authorization

After a subscriber subscribes to a listing, linked stored procedures might not execute right away. To ensure that linked stored procedures can run, the subscriber must send the linked dataset name to the provider so that [the provider authorizes the linked stored procedure on the provider's resources](https://docs.cloud.google.com/bigquery/docs/analytics-hub-manage-listings#provider-authorization) . In addition, the subscriber must [authorize the linked shared stored procedure and attach an IAM role](https://docs.cloud.google.com/bigquery/docs/authorized-routines#bq-attach-role) to the subscriber's resources to allow reading from and writing to those resources.

### Provider authorization

When a provider creates a listing with a stored procedure, the provider must let the subscriber read from and write to the provider's tables through the linked stored procedure. To ensure access, the provider must do the following:

  - For non-read operations, authorize the linked shared stored procedure and [attach an IAM role](https://docs.cloud.google.com/bigquery/docs/authorized-routines#bq-attach-role) to any provider resource accessed by the linked stored procedure.

  - For read operations, authorize either the linked shared stored procedure (in the subscriber's linked dataset) or the original shared stored procedure (in the provider's dataset), and attach an IAM role to any provider resource accessed by the procedure.

## Give users access to a listing

To provide access to a private listing, you must set the IAM policy for that listing to include specific individuals or groups. For a commercial listing, your [data exchange must be public](https://docs.cloud.google.com/bigquery/docs/analytics-hub-manage-exchanges#make-data-exchange-public) . Listings in a public data exchange appear in BigQuery sharing for all [Google Cloud users ( `allAuthenticatedUsers` )](https://docs.cloud.google.com/iam/docs/principals-overview#all-authenticated-users) . To let users browse and request access to commercial listings, grant those users the [Analytics Hub Viewer role](https://docs.cloud.google.com/bigquery/docs/analytics-hub-grant-roles#ah-subscriber-role) ( `roles/analyticshub.viewer` ). To let users subscribe to commercial listings, grant those users the [Analytics Hub Subscriber role](https://docs.cloud.google.com/bigquery/docs/analytics-hub-grant-roles#ah-subscriber-role) ( `roles/analyticshub.subscriber` ). For [Cloud Marketplace-integrated commercial listings](https://docs.cloud.google.com/bigquery/docs/analytics-hub-cloud-marketplace) , BigQuery sharing automatically grants the Analytics Hub Subscriber role based on Cloud Marketplace orders.

To make your listing accessible to everyone—including people without a Google Cloud account—grant `allUsers` the Analytics Hub Viewer role ( `roles/analyticshub.viewer` ).

To give users access to view or subscribe to your listing, follow these steps:

### Console

1.  Go to the **Sharing (Analytics Hub)** page.

2.  Click the data exchange name that contains the listing.

3.  Click the listing that you want to share.

4.  Click person **Set permissions** .

5.  To add principals, click person\_add **Add principal** .

6.  In the **New principals** field, enter principals based on your listing type:
    
      - For a private listing, enter the email addresses of the identities you want to grant access to.
    
      - For a public listing, enter `allAuthenticatedUsers` .
    
      - For a public listing discoverable to everyone, including non-Google Cloud users, enter `allUsers` .

7.  In the **Select a role** menu, point to **Analytics Hub** , and then select a role based on your listing type:
    
      - For a commercial listing (including Cloud Marketplace-integrated listings), select **Analytics Hub Viewer** . This role lets users [view the listing and request access](https://docs.cloud.google.com/bigquery/docs/analytics-hub-view-subscribe-listings#discover-listings) .
    
      - For a private or non-commercial public listing, select **Analytics Hub Subscriber** . This role lets users [subscribe to your listing](https://docs.cloud.google.com/bigquery/docs/analytics-hub-view-subscribe-listings#subscribe-listings) .
    
      - For Cloud Marketplace-integrated listings, you don't need to grant the Analytics Hub Subscriber role ( `roles/analyticshub.subscriber` ). Subscriptions are automatically managed based on the Cloud Marketplace order.
    
    > **Note:** After you grant licenses that let users access non-Cloud Marketplace-integrated commercial listings, you can either [create a private listing](https://docs.cloud.google.com/bigquery/docs/analytics-hub-manage-listings#create_a_listing) for those users or grant those users the [Analytics Hub Subscriber role](https://docs.cloud.google.com/bigquery/docs/analytics-hub-grant-roles#ah-subscriber-role) ( `roles/analyticshub.subscriber` ) on your commercial listing.
    
    For more information, see [Analytics Hub Subscriber and Viewer roles](https://docs.cloud.google.com/bigquery/docs/analytics-hub-grant-roles#ah-subscriber-role) .

8.  To save the permissions, click **Save** .

### API

1.  Read the existing policy by calling the [`projects.locations.dataExchanges.listings.getIamPolicy` method](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings/getIamPolicy) :
    
        POST https://analyticshub.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/dataExchanges/DATAEXCHANGE_ID/listings/LISTING_ID:getIamPolicy
    
    Replace the following:
    
      - `  PROJECT_ID  ` : the project ID—for example, `my-project-1` .
      - `  LOCATION  ` : the location of the data exchange that contains the listing.
      - `  DATAEXCHANGE_ID  ` : the data exchange ID.
      - `  LISTING_ID  ` : the listing ID.
    
    Sharing returns the current policy in the response.

2.  To add or remove members and their associated roles, edit the policy JSON using a text editor. Specify members using the following formats:
    
      - `user:test-user@gmail.com`
      - `group:admins@example.com`
      - `serviceAccount:test123@example.domain.com`
      - `domain:example.domain.com`
    
    For example, to grant the `roles/analyticshub.subscriber` role to `group:subscribers@example.com` , add the following binding to the policy:
    
        {
        "members": [
         "group:subscribers@example.com"
        ],
        "role":"roles/analyticshub.subscriber"
        }

3.  Update the policy by calling the [`projects.locations.dataExchanges.listings.setIamPolicy` method](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings/setIamPolicy) . In the request body, pass the updated IAM policy from the previous step.
    
        POST https://analyticshub.googleapis.com/v1/projects/PROJECT_ID/location/LOCATION/dataExchanges/DATAEXCHANGE_ID/listings/LISTING_ID:setIamPolicy
    
    In the request body, pass the listing details. If the request succeeds, the response body returns the listing details with the updated policy.

For more information about the tasks that you can perform on listings using APIs, see [`projects.locations.dataExchanges.listings` methods](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#methods) .

> **Note:** After you grant licenses to users to access your commercial listing, you can either [create a private listing](https://docs.cloud.google.com/bigquery/docs/analytics-hub-manage-listings#create_a_listing) for those users or grant those users the Analytics Hub Subscriber role ( `roles/analyticshub.subscriber` ) on your commercial listing.

### Create a non-authenticated URL for a public listing

To create an unauthenticated BigQuery sharing listing URL that users without a Google Cloud account can view, follow these steps:

1.  Go to the **Sharing (Analytics Hub)** page.
    
    A page appears that lists all data exchanges that you can access.

2.  Click the data exchange name that contains the listing.

3.  To view the listing details, click the listing display name. The listing must have [public discoverability](https://docs.cloud.google.com/bigquery/docs/analytics-hub-manage-listings#create_a_listing) turned on.

4.  Click **Copy public link** . To ensure that external users can view the listing, verify that the listing grants `allUsers` the Analytics Hub Viewer role ( `roles/analyticshub.viewer` ).

### Create a listing administrator

To let users manage listings, you can create listing administrators by granting those users the [Analytics Hub Publisher or Analytics Hub Listing Admin role](https://docs.cloud.google.com/bigquery/docs/analytics-hub-grant-roles#ah-publisher-role) on the listing. For instructions on granting roles on a listing, see [Grant the role for a listing](https://docs.cloud.google.com/bigquery/docs/analytics-hub-grant-roles#grant-role-listing) .

## View all subscriptions

To view all the current subscriptions to your listing, select one of the following options:

### Console

1.  Go to the **Sharing (Analytics Hub)** page.

2.  Click the data exchange name that contains the listing for which you want to manage the subscriptions.

3.  Click the listing for which you want to list all subscribers.

4.  To view all subscribers of your listing, click **Manage subscriptions** :
    
    ![The highlighted Manage subscriptions option for an Analytics Hub listing.](https://docs.cloud.google.com/static/bigquery/images/analytics-hub-manage-subscription.png)

5.  Optional: You can filter results by subscriber details.

Alternatively, if you have access to the [shared dataset](https://docs.cloud.google.com/bigquery/docs/analytics-hub-introduction#shared_datasets) , you can follow these steps to list subscribers:

1.  Go to the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :
    
    ![Highlighted button for the Explorer pane.](https://docs.cloud.google.com/static/bigquery/images/explorer-tab.png)
    
    If you don't see the left pane, click last\_page **Expand left pane** to open the pane.

3.  In the **Explorer** pane, expand your project name, click **Datasets** , and then click the name of the shared dataset.

4.  In the person\_add **Sharing** list, select **Manage subscriptions** .

### SQL

The following example uses the [`INFORMATION_SCHEMA.SCHEMATA_LINKS` view](https://docs.cloud.google.com/bigquery/docs/information-schema-datasets-schemata-links) to list all the linked datasets linked to a shared dataset in `myproject` that are in the `us` region:

    SELECT * FROM `myproject`.`region-us`.INFORMATION_SCHEMA.SCHEMATA_LINKS;

The output is similar to the following. Some columns are omitted to simplify the output.

    +----------------+-------------+----------------------------+------------------------------+--------------------+--------------------------------+
    |  catalog_name  | schema_name | linked_schema_catalog_name | linked_schema_catalog_number | linked_schema_name | linked_schema_org_display_name |
    +----------------+-------------+----------------------------+------------------------------+--------------------+--------------------------------+
    | myproject      | myschema1   | subscriptionproject1       |                 974999999291 | subscriptionld1    | subscriptionorg                |
    | myproject      | myschema2   | subscriptionproject2       |                 974999999292 | subscriptionld2    | subscriptionorg                |
    | myproject      | myschema3   | subscriptionproject3       |                 974999999293 | subscriptionld3    | subscriptionorg                |
    +----------------+-------------+----------------------------+------------------------------+--------------------+--------------------------------+

For a listing with multiple regions, you can view the subscriptions across different regions by replacing the `us` region with the intended replica location. For example, to view the linked datasets linked to a shared dataset in `myproject` that are in the `eu` region, use the following query:

    SELECT * FROM `myproject`.`region-eu`.INFORMATION_SCHEMA.SCHEMATA_LINKS;

### API

Use the [projects.locations.dataExchanges.listings.listSubscriptions method](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings/listSubscriptions) .

    GET https://analyticshub.googleapis.com/v1/projects/PROJECT_ID/location/LOCATION/dataExchanges/DATAEXCHANGE_ID/listings/LISTING_ID:listSubscriptions

Replace the following:

  - `  PROJECT_ID  ` : the project ID of the listing that you want to subscribe to.
  - `  LOCATION  ` : the location for the listing that you want to subscribe to.
  - `  DATAEXCHANGE_ID  ` : the data exchange ID that contains the listing that you want to subscribe to.
  - `  LISTING_ID  ` : the ID of the listing that you want to subscribe to.

## Remove a subscription

When you remove a subscription created before July 25, 2023, from your listing, the [linked dataset](https://docs.cloud.google.com/bigquery/docs/analytics-hub-introduction#listings) unlinks from the [shared dataset](https://docs.cloud.google.com/bigquery/docs/analytics-hub-introduction#shared_datasets) . Subscribers can still view the dataset in their projects, but the dataset is no longer linked to your shared dataset.

> **Caution:** Revoking [Cloud Marketplace-integrated commercial subscriptions](https://docs.cloud.google.com/bigquery/docs/analytics-hub-cloud-marketplace) can impact your customers and might violate the [Cloud Marketplace Terms of Service](https://cloud.google.com/terms/marketplace/launcher) .

To remove a subscription created before July 25, 2023, from your listing, follow these steps:

1.  To list subscribers of a listing, follow the [View all subscriptions](https://docs.cloud.google.com/bigquery/docs/analytics-hub-manage-listings#view_all_subscriptions) instructions for the Google Cloud console.

2.  To remove a subscriber from a listing, click delete **Delete** . To remove all subscriptions, click **Remove all subscriptions** .

3.  In the **Remove subscription?** dialog, confirm deletion by typing `remove` .

4.  Click **Remove** .

To remove a subscription created after July 25, 2023, follow these steps:

### Console

1.  To list subscribers of a listing, follow the [View all subscriptions](https://docs.cloud.google.com/bigquery/docs/analytics-hub-manage-listings#view_all_subscriptions) instructions for the Google Cloud console.

2.  Click **Subscriptions** .

3.  To select the subscriptions that you want to remove, select the checkboxes next to those subscriptions, and then click delete **Remove Subscriptions** .

4.  In the **Remove subscription?** dialog, confirm removal by typing `remove` .

5.  Click **Remove** .

### API

Call the [`projects.locations.subscriptions.revoke` method](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.subscriptions/revoke) :

    POST https://analyticshub.googleapis.com/v1/projects/PROJECT_ID/location/LOCATION/subscriptions/SUBSCRIPTION_ID:revoke

Replace the following:

  - `  PROJECT_ID  ` : the project ID of the subscription that you want to remove.
  - `  LOCATION  ` : the location of the subscription that you want to remove.
  - `  SUBSCRIPTION  ` : the ID of the [subscription](https://docs.cloud.google.com/bigquery/docs/analytics-hub-manage-subscriptions#list_subscriptions) that you want to remove.

## Update a listing

As your data exchange requirements evolve, you can update a listing's metadata, categories, discoverability settings, and region availability without modifying the underlying shared dataset.

To update a listing, follow these steps:

### Console

1.  Go to the **Sharing (Analytics Hub)** page.

2.  Click the data exchange name that contains the listing.

3.  Click the listing that you want to update.

4.  Click mode\_edit **Edit listing** .

5.  Modify values in the fields. You can modify all values except the listing's shared dataset.

6.  Optional: Update listing settings and availability:
    
      - To enable public discoverability, grant the [Analytics Hub Viewer role](https://docs.cloud.google.com/bigquery/docs/access-control#analyticshub.viewer) ( `roles/analyticshub.viewer` ) to `allUsers` or `allAuthenticatedUsers` . For instructions on granting roles on a listing, see [Grant the role for a listing](https://docs.cloud.google.com/bigquery/docs/analytics-hub-grant-roles#grant-role-listing) .
      - To disable public discoverability for a listing in a private exchange, remove the Analytics Hub Viewer role ( `roles/analyticshub.viewer` ) from `allUsers` and `allAuthenticatedUsers` . If the exchange is already [public](https://docs.cloud.google.com/bigquery/docs/analytics-hub-manage-exchanges#make-data-exchange-public) , listing permissions are already inherited and no further action is required.
      - After you turn on and save subscriber email logging, you can't edit this setting. To turn off email logging, delete the listing, and then recreate the listing without selecting **Subscriber email logging** .
      - To add or remove regions, update your region selection. Before you add multiple regions, verify that you enabled [cross-region dataset replication](https://docs.cloud.google.com/bigquery/docs/data-replication#use_dataset_replication) on the shared dataset. Before you remove a region, delete the shared dataset replica in that region.

7.  Review the listing preview.

8.  To save changes, click **Save** . If you update a Cloud Marketplace-integrated listing, a notification prompts you to update the Cloud Marketplace data product listing as well.
    
    > **Note:** Updating a Cloud Marketplace data product listing requires review and approval by the Marketplace Operations Team.

### API

Call the [`projects.locations.dataExchanges.listings.patch` method](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings/patch) :

    PATCH https://analyticshub.googleapis.com/v1/projects/PROJECT_ID/location/LOCATION/dataExchanges/DATAEXCHANGE_ID/listings/LISTING_ID?updateMask=UPDATEMASK

Replace the following:

  - `  PROJECT_ID  ` : the ID of the project that contains the data exchange in which you want to create the listing.
  - `  LOCATION  ` : the location of the data exchange.
  - `  DATAEXCHANGE_ID  ` : the ID of the data exchange.
  - `  LISTING_ID  ` : the ID of the listing to update.
  - `  UPDATEMASK  ` : the list of fields that you want to update. To update multiple values, use a comma-separated list. For example, to update the display name and primary contact for a data exchange, enter `displayName,primaryContact` .

In the request body, specify updated values for the fields in your update mask:

  - `displayName`
  - `description`
  - `primaryContact`
  - `documentation`
  - `icon`
  - `categories[]`
  - `discoveryType`
  - `logLinkedDatasetQueryUserEmail`
  - `bigqueryDataset.replicaLocations`

For details on these fields, see [Resource: Listing](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#resource:-listing) .

When updating replica regions for your listing, specify all applicable regions. Before you update the listing, verify that you enabled [cross-region dataset replication](https://docs.cloud.google.com/bigquery/docs/data-replication#use_dataset_replication) on the shared dataset. You can only add regions where the shared dataset has a replica. Before you remove a region from the listing, delete the shared dataset replica in that region. You can also convert single-region listings into multi-region listings.

For more information about the tasks that you can perform on listings using APIs, see [`projects.locations.dataExchanges.listings` methods](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#methods) .

## Display a listing in the featured section

To increase visibility of your listing in the BigQuery sharing catalog, you can display your listing in the **Featured** section. Featured listings are governed by the Google Cloud Partner Program Agreement.

To request that your listing display in the **Featured** section, you must meet the following criteria:

  - The shared data must reside in BigQuery.

  - You must be enrolled in the [Google Cloud Partner Network program](https://partners.cloud.google.com/) within the Google Cloud Technology Partner Path.

  - Your listing must be created and have [public discoverability](https://docs.cloud.google.com/bigquery/docs/analytics-hub-manage-listings#create_a_listing) turned on.

To request to add your listing to the **Featured** section, or to request to remove your listing from the section, submit the [Featured listing intake form](https://docs.google.com/forms/d/e/1FAIpQLSe9nLw7kmvU2AEUgaWn5vvPQMFs1Q7XwqKBy7TD5xR1DLX4bQ/viewform?resourcekey=0-zRsM2reDM3QjxegIUluHJA&pli=1) .

## Delete a listing

When you delete a listing, subscribers can no longer [view the listing](https://docs.cloud.google.com/bigquery/docs/analytics-hub-view-subscribe-listings#discover-listings) . Deleting a listing also [deletes all linked datasets](https://docs.cloud.google.com/bigquery/docs/analytics-hub-manage-listings#remove_a_subscription) and removes all subscriptions from subscriber projects. If a dataset remains linked, remove the dataset manually by clicking person\_add **Sharing \> Manage Subscription** . On the **Subscriptions** page, remove specific subscriber datasets or all subscriber datasets at once.

You can't delete [Cloud Marketplace-integrated listings](https://docs.cloud.google.com/bigquery/docs/analytics-hub-cloud-marketplace) that have active commercial subscriptions. You must [revoke all commercial subscriptions](https://docs.cloud.google.com/bigquery/docs/analytics-hub-manage-subscriptions#revoke-subscription) before you delete the listing.

> **Caution:** Revoking [Cloud Marketplace-integrated commercial subscriptions](https://docs.cloud.google.com/bigquery/docs/analytics-hub-cloud-marketplace) can impact your customers and might violate the [Cloud Marketplace Terms of Service](https://cloud.google.com/terms/marketplace/launcher) .

Deleting a multi-region listing doesn't delete the shared dataset replicas. After you delete a multi-region listing, subscribers can no longer view the listing or query the linked datasets. If no other listings reference the shared dataset replicas, you can [delete those replicas](https://docs.cloud.google.com/bigquery/docs/data-replication#remove_a_dataset_replica) .

Before you delete a multi-region listing, verify that the listing has no active subscriptions. If active subscriptions exist, revoke them by calling the [`projects.locations.subscriptions.revoke` method](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.subscriptions/revoke) . After all active subscriptions are removed, delete the multi-region listing.

> **Caution:** Deleting a listing is permanent and can't be undone.

To delete a listing, follow these steps:

### Console

1.  Go to the **Sharing (Analytics Hub)** page.

2.  Click the data exchange name that contains the listing.

3.  Click the listing that you want to delete.

4.  Click delete **Delete** .

5.  In the **Delete listing?** dialog, confirm deletion by typing `delete` .

6.  Click **Delete** .

### API

Call the [`projects.locations.dataExchanges.listings.delete` method](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings/delete) :

    DELETE https://analyticshub.googleapis.com/v1/projects/PROJECT_ID/location/LOCATION/dataExchanges/DATAEXCHANGE_ID/listings/LISTING_ID

Replace the following:

  - `  PROJECT_ID  ` : the ID of the project that contains the data exchange.
  - `  LOCATION  ` : the location of the data exchange.
  - `  DATAEXCHANGE_ID  ` : the ID of the data exchange.
  - `  LISTING_ID  ` : the ID of the listing to delete.

For more information about the tasks that you can perform on listings using APIs, see [`projects.locations.dataExchanges.listings` methods](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings#methods) .

## What's next

  - Learn about [BigQuery sharing architecture](https://docs.cloud.google.com/bigquery/docs/analytics-hub-introduction#architecture) .
  - Learn how to [view and subscribe to listings](https://docs.cloud.google.com/bigquery/docs/analytics-hub-view-subscribe-listings) .
  - Learn about [BigQuery sharing IAM roles](https://docs.cloud.google.com/bigquery/docs/analytics-hub-grant-roles#user_roles) .
  - Learn about [creating datasets](https://docs.cloud.google.com/bigquery/docs/datasets) .
  - Learn about [BigQuery sharing audit logging](https://docs.cloud.google.com/bigquery/docs/analytics-hub-audit-logging) .
  - Learn how to [monitor listings](https://docs.cloud.google.com/bigquery/docs/analytics-hub-monitor-listings) .
