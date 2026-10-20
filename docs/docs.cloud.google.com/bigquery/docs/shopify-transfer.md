---
name: documents/docs.cloud.google.com/bigquery/docs/shopify-transfer
uri: https://docs.cloud.google.com/bigquery/docs/shopify-transfer
title: Load Shopify data into BigQuery
description: Learn how to use the BigQuery Data Transfer Service Shopify connector to ingest data from Shopify into BigQuery.
data_source: docs.cloud.google.com
---

# Load Shopify data into BigQuery

> **Preview**
>
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

> **Note:** To get support or provide feedback for this feature, contact <dts-preview-support@google.com> .

You can load data from Shopify to BigQuery using the [BigQuery Data Transfer Service](https://docs.cloud.google.com/bigquery/docs/dts-introduction) for Shopify connector. With the BigQuery Data Transfer Service, you can schedule recurring transfer jobs that add your latest data from Shopify to BigQuery.

The Shopify connector supports the data transfer of GraphQL-based resources, such as `Collections` and `Orders` , from the following resources:

- Subscription-based accounts
- Partner accounts

## Limitations

Shopify data transfers are subject to following limitations:

- To include the `GiftCards` object in the data transfer, the account associated with this data transfer must have a ShopifyPlus subscription.
- To include the following app subscription data objects in the data transfer, the app installed on the Shopify store must be a [sales channel app](https://shopify.dev/docs/apps/build/sales-channels) .
  - `AppSubscriptionLineItems`
  - `AppSubscriptions`
  - `ProductResourceFeedbacks`
- To include the following Shopify data objects that require a [discount function](https://shopify.dev/docs/apps/build/functions) , you must use the [Shopify CLI](https://shopify.dev/docs/api/shopify-cli) to create a Shopify app.
  - `DiscountsCodeApp`
  - `DiscountsCodeBasic`

## Before you begin

The following sections describe the prerequisites that you need to do before you create a Shopify data transfer.

### Shopify prerequisites

- You must have a Shopify account and a Shopify store.
- You must have a custom Shopify App for your Shopify store. For more information, see [Custom apps](https://help.shopify.com/en/manual/apps/app-types/custom-apps) .
- You must have access to the required scope for the Shopify data object that you want to transfer to BigQuery. For a list of required scopes for each object, see [Supported objects and required scopes](https://docs.cloud.google.com/bigquery/docs/shopify-transfer#supported-objects-and-scopes) .

### BigQuery prerequisites

- Verify that you have completed all actions required to [enable the BigQuery Data Transfer Service](https://docs.cloud.google.com/bigquery/docs/enable-transfer-service) .
- [Create a BigQuery dataset](https://docs.cloud.google.com/bigquery/docs/datasets) to store your data.

### Required BigQuery roles

To get the permissions that you need to create a BigQuery Data Transfer Service data transfer, ask your administrator to grant you the [BigQuery Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin) ( `roles/bigquery.admin` ) IAM role on your project. For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

This predefined role contains the permissions required to create a BigQuery Data Transfer Service data transfer. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

The following permissions are required to create a BigQuery Data Transfer Service data transfer:

- BigQuery Data Transfer Service permissions:
  - `bigquery.transfers.update`
  - `bigquery.transfers.get`
- BigQuery permissions:
  - `bigquery.datasets.get`
  - `bigquery.datasets.getIamPolicy`
  - `bigquery.datasets.update`
  - `bigquery.datasets.setIamPolicy`
  - `bigquery.jobs.create`

You might also be able to get these permissions with [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

For more information, see [Grant `bigquery.admin` access](https://docs.cloud.google.com/bigquery/docs/enable-transfer-service#grant_bigqueryadmin_access) .

If you intend to set up transfer run notifications for Pub/Sub, ensure that you have the `pubsub.topics.setIamPolicy` Identity and Access Management (IAM) permission. Pub/Sub permissions aren't required if you only set up email notifications. For more information, see [BigQuery Data Transfer Service run notifications](https://docs.cloud.google.com/bigquery/docs/transfer-run-notifications) .

## Set up a Shopify data transfer

Add Shopify data into BigQuery by setting up a transfer configuration using one of the following options:

### Console

1.  Go to the Data transfers page in the Google Cloud console.

2.  Click add **Create transfer** .

3.  In the **Source type** section, for **Source** , choose **Shopify** .

4.  In the **Data source details** section, do the following:

    - For **Shop name** , enter the name of your Shopify shop. For example, if your merchant account ID is `storename.myshopify.com` , then your shop name is `storename` .
    - For **Client ID** and **Client Secret** , enter the client ID and secret for your Shopify app. For more information, see [About client secrets](https://shopify.dev/docs/apps/build/authentication-authorization/client-secrets) .
    - For **Shopify objects to transfer** , click **Browse** :
      - Select any objects to be transferred to the BigQuery destination dataset. You can also manually enter any objects to include in the data transfer in this field.

5.  In the **Destination settings** section, for **Dataset** , choose the dataset that you created to store your data.

6.  In the **Transfer config name** section, for **Display name** , enter a name for the data transfer.

7.  In the **Schedule options** section:

    - In the **Repeat frequency** list, select an option to specify how often this data transfer runs. To specify a custom repeat frequency, select **Custom** . If you select **On-demand** , then this transfer runs when you [manually trigger the transfer](https://docs.cloud.google.com/bigquery/docs/working-with-transfers#manually_trigger_a_transfer) .
    - If applicable, select either **Start now** or **Start at set time** , and provide a start date and run time.

8.  Optional: In the **Notification options** section, do the following:

    - To enable email notifications, click the **Email notification** toggle. When you enable this option, the transfer administrator receives an email notification when a transfer run fails.
    - To enable [Pub/Sub transfer run notifications](https://docs.cloud.google.com/bigquery/docs/transfer-run-notifications) for this transfer, click the **Pub/Sub notifications** toggle. You can select your [topic](https://docs.cloud.google.com/pubsub/docs/overview#types) name, or you can click **Create a topic** to create one.

9.  Click **Save** .

### bq

Enter the [`bq mk` command](https://docs.cloud.google.com/bigquery/docs/reference/bq-cli-reference#bq_mk) and supply the transfer creation flag `--transfer_config` :

```
bq mk
    --transfer_config
    --project_id=PROJECT_ID
    --data_source=DATA_SOURCE
    --display_name=NAME
    --target_dataset=DATASET
    --params='PARAMETERS'
```

Where:

- ` PROJECT_ID ` (optional): your Google Cloud project ID. If `--project_id` isn't supplied to specify a particular project, the default project is used.

- ` DATA_SOURCE ` : the data source — `shopify` .

- ` NAME ` : the display name for the data transfer configuration. The transfer name can be any value that lets you identify the transfer if you need to modify it later.

- ` DATASET ` : the target dataset for the transfer configuration.

- ` PARAMETERS ` : the parameters for the created transfer configuration in JSON format. For example: `--params='{"param":"param_value"}'` . The following are the parameters for a Shopify data transfer:

  - `assets` : the path to the Shopify objects to be transferred to BigQuery.
  - `connector.shopName` : the name of your Shopify shop. For example, if your merchant account ID is `storename.myshopify.com` , then your shop name is `storename` .
  - `connector.authentication.accessToken` : the Shopify Admin API access token.

The following command creates an incremental Shopify data transfer in the default project.

```
bq mk
    --transfer_config
    --target_dataset=mydataset
    --data_source=shopify
    --display_name='My Transfer'
    --params='{"assets": ["Orders"]
        "connector.shopName": "storename",
        "connector.authentication.accessToken":"sk_test_123456789"}'
```

When you save the transfer configuration, the Shopify connector automatically triggers a transfer run according to your schedule option. With every transfer run, the Shopify connector transfers all available data from Shopify into BigQuery.

To manually run a data transfer outside of your regular schedule, you can start a [backfill run](https://docs.cloud.google.com/bigquery/docs/working-with-transfers#manually_trigger_a_transfer) .

## Supported objects and required scopes

The following table lists the Shopify data objects that can be transferred to BigQuery and the required scopes for each object.

| Data object                                                                                                               | Required scope                             |     |
|---------------------------------------------------------------------------------------------------------------------------|--------------------------------------------|-----|
| [AppFeedbacks](https://shopify.dev/docs/api/admin-graphql/latest/objects/AppFeedback)                                     | No scope required                          |     |
| [AppSubscriptionLineItems](https://shopify.dev/docs/api/admin-graphql/latest/objects/AppSubscriptionLineItem)             | No scope required                          |     |
| [AppSubscriptions](https://shopify.dev/docs/api/admin-graphql/latest/objects/AppSubscription)                             | No scope required                          |     |
| [Catalogs](https://shopify.dev/docs/api/admin-graphql/latest/interfaces/Catalog)                                          | `read_products` or `read_product_listings` |     |
| `read_publications`                                                                                                       |                                            |     |
| [Collections](https://shopify.dev/docs/api/admin-graphql/latest/objects/Collection)                                       | `read_products`                            |     |
| `read_publications`                                                                                                       |                                            |     |
| [Companies](https://shopify.dev/docs/api/admin-graphql/latest/objects/Company)                                            | `read_customers` or `read_companies`       |     |
| [CompanyContactRoleAssignments](https://shopify.dev/docs/api/admin-graphql/latest/objects/CompanyContactRoleAssignment)   | `read_customers` or `read_companies`       |     |
| [CompanyContacts](https://shopify.dev/docs/api/admin-graphql/latest/objects/CompanyContact)                               | `read_customers` or `read_companies`       |     |
| [CompanyLocations](https://shopify.dev/docs/api/admin-graphql/latest/objects/CompanyLocation)                             | `read_customers` or `read_companies`       |     |
| [Customers](https://shopify.dev/docs/api/admin-graphql/latest/objects/Customer)                                           | `read_customers`                           |     |
| `write_customers`                                                                                                         |                                            |     |
| `read_customer_merge`                                                                                                     |                                            |     |
| `read_locations` or `read_inventory`                                                                                      |                                            |     |
| `read_markets`                                                                                                            |                                            |     |
| `read_orders`                                                                                                             |                                            |     |
| [DeliveryProfiles](https://shopify.dev/docs/api/admin-graphql/latest/objects/DeliveryProfile)                             | `read_products`                            |     |
| `read_shipping`                                                                                                           |                                            |     |
| [DiscountsAutomaticApp](https://shopify.dev/docs/api/admin-graphql/latest/objects/DiscountAutomaticApp)                   | `read_discounts`                           |     |
| [DiscountsAutomaticBasic](https://shopify.dev/docs/api/admin-graphql/latest/objects/DiscountAutomaticBasic)               | `read_discounts`                           |     |
| [DiscountsAutomaticBxgy](https://shopify.dev/docs/api/admin-graphql/latest/objects/DiscountAutomaticBxgy)                 | `read_discounts`                           |     |
| [DiscountsCodeApp](https://shopify.dev/docs/api/admin-graphql/latest/objects/DiscountCodeApp)                             | `read_discounts`                           |     |
| [DiscountsCodeBasic](https://shopify.dev/docs/api/admin-graphql/latest/objects/DiscountCodeBasic)                         | `read_discounts`                           |     |
| [DiscountsCodeBxgy](https://shopify.dev/docs/api/admin-graphql/latest/objects/DiscountCodeBxgy)                           | `read_discounts`                           |     |
| [DraftOrders](https://shopify.dev/docs/api/admin-graphql/latest/objects/DraftOrder)                                       | `read_customers`                           |     |
| `read_draft_orders`                                                                                                       |                                            |     |
| `read_orders`                                                                                                             |                                            |     |
| `read_payment_terms`                                                                                                      |                                            |     |
| [Files](https://shopify.dev/docs/api/admin-graphql/latest/interfaces/File)                                                | `read_files`                               |     |
| [FulfillmentEvents](https://shopify.dev/docs/api/admin-graphql/latest/objects/FulfillmentEvent)                           | `read_orders`                              |     |
| [FulfillmentOrders](https://shopify.dev/docs/api/admin-graphql/latest/objects/FulfillmentOrder)                           | `read_locations`                           |     |
| `read_orders`                                                                                                             |                                            |     |
| `read_assigned_fulfillment_orders` or `read_merchant_managed_fulfillment_orders` or `read_third_party_fulfillment_orders` |                                            |     |
| [Fulfillments](https://shopify.dev/docs/api/admin-graphql/latest/objects/Fulfillment)                                     | `read_fulfillments` or `read_products`     |     |
| `read_locations`                                                                                                          |                                            |     |
| `read_orders`                                                                                                             |                                            |     |
| [FulfillmentServices](https://shopify.dev/docs/api/admin-graphql/latest/objects/FulfillmentService)                       | `read_locations` or `read_inventory`       |     |
| `read_fulfillments` or `read_products` or `read_custom_fulfillment_services` or `assigned_fulfillment_orders`             |                                            |     |
| [FulfillmentTrackingInfo](https://shopify.dev/docs/api/admin-graphql/latest/objects/FulfillmentTrackingInfo)              | `read_fulfillments` or `read_products`     |     |
| `read_locations`                                                                                                          |                                            |     |
| `read_orders`                                                                                                             |                                            |     |
| [GiftCards](https://shopify.dev/docs/api/admin-graphql/latest/objects/GiftCard)                                           | `read_gift_cards`                          |     |
| `read_orders`                                                                                                             |                                            |     |
| `read_customers`                                                                                                          |                                            |     |
| [InventoryItems](https://shopify.dev/docs/api/admin-graphql/latest/objects/InventoryItem)                                 | `read_inventory`                           |     |
| `read_products`                                                                                                           |                                            |     |
| [Locations](https://shopify.dev/docs/api/admin-graphql/latest/objects/Location)                                           | `read_locations`                           |     |
| `read_fulfillments`                                                                                                       |                                            |     |
| Metafields_Article                                                                                                        | `read_content`                             |     |
| Metafields_Blog                                                                                                           | `read_content`                             |     |
| Metafields_Collection                                                                                                     | `read_products`                            |     |
| `read_publications`                                                                                                       |                                            |     |
| Metafields_Customer                                                                                                       | `read_customers`                           |     |
| `write_customers`                                                                                                         |                                            |     |
| `read_customer_merge`                                                                                                     |                                            |     |
| `read_locations` or `read_inventory`                                                                                      |                                            |     |
| `read_markets`                                                                                                            |                                            |     |
| `read_orders`                                                                                                             |                                            |     |
| Metafields_Draft_Order                                                                                                    | `read_customers`                           |     |
| `read_draft_orders`                                                                                                       |                                            |     |
| `read_orders`                                                                                                             |                                            |     |
| `read_payment_terms`                                                                                                      |                                            |     |
| Metafields_Order                                                                                                          | `read_customers`                           |     |
| `read_inventory`                                                                                                          |                                            |     |
| `read_locations`                                                                                                          |                                            |     |
| `read_orders`                                                                                                             |                                            |     |
| `read_payment_terms`                                                                                                      |                                            |     |
| Metafields_Page                                                                                                           | `read_content`                             |     |
| Metafields_Product                                                                                                        | `read_products`                            |     |
| `read_product_listings`                                                                                                   |                                            |     |
| `read_publications`                                                                                                       |                                            |     |
| Metafields_Selling_Plan                                                                                                   | `read_products`                            |     |
| Metafields_Shop                                                                                                           | No scope required                          |     |
| Metafields_Variant                                                                                                        | `read_products`                            |     |
| `read_shipping`                                                                                                           |                                            |     |
| [OrderLineItems](https://shopify.dev/docs/api/admin-graphql/latest/objects/LineItem)                                      | `read_orders`                              |     |
| `read_products`                                                                                                           |                                            |     |
| [OrderRiskAssessments](https://shopify.dev/docs/api/admin-graphql/latest/objects/OrderRiskAssessment)                     | `read_orders`                              |     |
| [Orders](https://shopify.dev/docs/api/admin-graphql/latest/objects/Order)                                                 | `read_customers`                           |     |
| `read_inventory`                                                                                                          |                                            |     |
| `read_locations`                                                                                                          |                                            |     |
| `read_orders`                                                                                                             |                                            |     |
| `read_payment_terms`                                                                                                      |                                            |     |
| `read_draft_orders`                                                                                                       |                                            |     |
| `read_products` or `read_fulfillments`                                                                                    |                                            |     |
| [OrderTransactions](https://shopify.dev/docs/api/admin-graphql/latest/objects/OrderTransaction)                           | `read_orders`                              |     |
| `read_products`                                                                                                           |                                            |     |
| [PriceLists](https://shopify.dev/docs/api/admin-graphql/latest/objects/PriceList)                                         | `read_products`                            |     |
| [ProductMediaImages](https://shopify.dev/docs/api/admin-graphql/latest/objects/MediaImage)                                | `read_products`                            |     |
| [ProductOptions](https://shopify.dev/docs/api/admin-graphql/latest/objects/ProductOption)                                 | `read_products`                            |     |
| [ProductOptionValues](https://shopify.dev/docs/api/admin-graphql/latest/objects/ProductOptionValue)                       | `read_products`                            |     |
| [ProductResourceFeedbacks](https://shopify.dev/docs/api/admin-graphql/latest/objects/ProductResourceFeedback)             | `read_resource_feedbacks`                  |     |
| `read_products`                                                                                                           |                                            |     |
| [Products](https://shopify.dev/docs/api/admin-graphql/latest/objects/Product)                                             | `read_products`                            |     |
| `read_product_listings`                                                                                                   |                                            |     |
| `read_publications`                                                                                                       |                                            |     |
| [ProductVariants](https://shopify.dev/docs/api/admin-graphql/latest/objects/ProductVariant)                               | `read_products`                            |     |
| `read_shipping`                                                                                                           |                                            |     |
| [Publications](https://shopify.dev/docs/api/admin-graphql/latest/objects/Publication)                                     | `read_products`                            |     |
| `read_publications`                                                                                                       |                                            |     |
| [Refunds](https://shopify.dev/docs/api/admin-graphql/latest/objects/Refund)                                               | `read_products`                            |     |
| `read_orders`                                                                                                             |                                            |     |
| `read_returns`                                                                                                            |                                            |     |
| [Returns](https://shopify.dev/docs/api/admin-graphql/latest/objects/Return)                                               | `read_orders`                              |     |
| `read_returns`                                                                                                            |                                            |     |
| [ScriptTags](https://shopify.dev/docs/api/admin-graphql/latest/objects/ScriptTag)                                         | `read_script_tags`                         |     |
| [Segments](https://shopify.dev/docs/api/admin-graphql/latest/objects/Segment)                                             | `read_customers`                           |     |
| [SellingPlanGroups](https://shopify.dev/docs/api/admin-graphql/latest/objects/SellingPlanGroup)                           | `read_products`                            |     |
| [StorefrontAccessTokens](https://shopify.dev/docs/api/admin-graphql/latest/objects/StorefrontAccessToken)                 | No scope required                          |     |
| [UrlRedirects](https://shopify.dev/docs/api/admin-graphql/latest/objects/UrlRedirect)                                     | `read_online_store_navigation`             |     |

## Data type mapping

The following table maps Shopify data types to the corresponding BigQuery data types:

| Shopify data type | BigQuery data type |
|-------------------|--------------------|
| `String`          | `STRING`           |
| `Int`             | `INT64`            |
| `Decimal`         | `NUMERIC`          |
| `Double`          | `FLOAT64`          |
| `Long`            | `BIGNUMERIC`       |
| `Bool`            | `BOOL`             |
| `Datetime`        | `TIMESTAMP`        |

## Pricing

There is no cost to transfer Shopify data into BigQuery while this feature is in [Preview](https://cloud.google.com/products#product-launch-stages) .

## Troubleshoot transfer setup

If you are having issues setting up your data transfer, see [Shopify transfer issues](https://docs.cloud.google.com/bigquery/docs/transfer-troubleshooting#shopify-issues) .

## What's next

- For an overview of the BigQuery Data Transfer Service, see [What is BigQuery Data Transfer Service](https://docs.cloud.google.com/bigquery/docs/dts-introduction) .
- For information on using transfers including getting information about a transfer configuration, listing transfer configurations, and viewing a transfer's run history, see [Manage transfers](https://docs.cloud.google.com/bigquery/docs/working-with-transfers) .
