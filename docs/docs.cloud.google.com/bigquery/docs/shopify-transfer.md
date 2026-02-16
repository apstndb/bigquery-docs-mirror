# Load Shopify data into BigQuery

**Preview**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

**Note:** To get support or provide feedback for this feature, contact <dts-preview-support@google.com> .

You can load data from Shopify to BigQuery using the BigQuery Data Transfer Service for Shopify connector. With the BigQuery Data Transfer Service, you can schedule recurring transfer jobs that add your latest data from Shopify to BigQuery.

The Shopify connector supports the data transfer of GraphQL-based resources, such as `  Collections  ` and `  Orders  ` , from the following resources:

  - Subscription-based accounts
  - Partner accounts

## Limitations

Shopify data transfers are subject to following limitations:

  - To include the `  GiftCards  ` object in the data transfer, the account associated with this data transfer must have a ShopifyPlus subscription.
  - To include the following app subscription data objects in the data transfer, the app installed on the Shopify store must be a [sales channel app](https://shopify.dev/docs/apps/build/sales-channels) .
      - `  AppSubscriptionLineItems  `
      - `  AppSubscriptions  `
      - `  ProductResourceFeedbacks  `
  - To include the following Shopify data objects that require a [discount function](https://shopify.dev/docs/apps/build/functions) , you must use the [Shopify CLI](https://shopify.dev/docs/api/shopify-cli) to create a Shopify app.
      - `  DiscountsCodeApp  `
      - `  DiscountsCodeBasic  `

## Before you begin

The following sections describe the prerequisites that you need to do before you create a Shopify data transfer.

### Shopify prerequisites

  - You must have a Shopify account and a Shopify store.
  - You must have a custom Shopify App for your Shopify store. For more information, see [Custom apps](https://help.shopify.com/en/manual/apps/app-types/custom-apps) .
  - You must have access to all the required access scopes. For a list of all required access scopes, see [Authenticated access scopes](https://shopify.dev/docs/api/usage/access-scopes#authenticated-access-scopes) .

### BigQuery prerequisites

  - Verify that you have completed all actions required to [enable the BigQuery Data Transfer Service](/bigquery/docs/enable-transfer-service) .
  - [Create a BigQuery dataset](/bigquery/docs/datasets) to store your data.

### Required BigQuery roles

To get the permissions that you need to create a BigQuery Data Transfer Service data transfer, ask your administrator to grant you the [BigQuery Admin](/iam/docs/roles-permissions/bigquery#bigquery.admin) ( `  roles/bigquery.admin  ` ) IAM role on your project. For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

This predefined role contains the permissions required to create a BigQuery Data Transfer Service data transfer. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

The following permissions are required to create a BigQuery Data Transfer Service data transfer:

  - BigQuery Data Transfer Service permissions:
      - `  bigquery.transfers.update  `
      - `  bigquery.transfers.get  `
  - BigQuery permissions:
      - `  bigquery.datasets.get  `
      - `  bigquery.datasets.getIamPolicy  `
      - `  bigquery.datasets.update  `
      - `  bigquery.datasets.setIamPolicy  `
      - `  bigquery.jobs.create  `

You might also be able to get these permissions with [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

For more information, see [Grant `  bigquery.admin  ` access](/bigquery/docs/enable-transfer-service#grant_bigqueryadmin_access) .

If you intend to set up transfer run notifications for Pub/Sub, ensure that you have the `  pubsub.topics.setIamPolicy  ` Identity and Access Management (IAM) permission. Pub/Sub permissions aren't required if you only set up email notifications. For more information, see [BigQuery Data Transfer Service run notifications](/bigquery/docs/transfer-run-notifications) .

## Set up a Shopify data transfer

Add Shopify data into BigQuery by setting up a transfer configuration using one of the following options:

### Console

1.  Go to the Data transfers page in the Google Cloud console.

2.  Click add **Create transfer** .

3.  In the **Source type** section, for **Source** , choose **Shopify** .

4.  In the **Data source details** section, do the following:
    
      - For **Shop name** , enter the name of your Shopify shop. For example, if your merchant account ID is `  storename.myshopify.com  ` , then your shop name is `  storename  ` .
      - For **Client ID** and **Client Secret** , enter the client ID and secret for your Shopify app. For more information, see [About client secrets](https://shopify.dev/docs/apps/build/authentication-authorization/client-secrets) .
      - For **Shopify objects to transfer** , click **Browse** :
          - Select any objects to be transferred to the BigQuery destination dataset. You can also manually enter any objects to include in the data transfer in this field.

5.  In the **Destination settings** section, for **Dataset** , choose the dataset that you created to store your data.

6.  In the **Transfer config name** section, for **Display name** , enter a name for the data transfer.

7.  In the **Schedule options** section:
    
      - In the **Repeat frequency** list, select an option to specify how often this data transfer runs. To specify a custom repeat frequency, select **Custom** . If you select **On-demand** , then this transfer runs when you [manually trigger the transfer](/bigquery/docs/working-with-transfers#manually_trigger_a_transfer) .
      - If applicable, select either **Start now** or **Start at set time** , and provide a start date and run time.

8.  Optional: In the **Notification options** section, do the following:
    
      - To enable email notifications, click the **Email notification** toggle. When you enable this option, the transfer administrator receives an email notification when a transfer run fails.
      - To enable [Pub/Sub transfer run notifications](/bigquery/docs/transfer-run-notifications) for this transfer, click the **Pub/Sub notifications** toggle. You can select your [topic](/pubsub/docs/overview#types) name, or you can click **Create a topic** to create one.

9.  Click **Save** .

### bq

Enter the [`  bq mk  ` command](/bigquery/docs/reference/bq-cli-reference#bq_mk) and supply the transfer creation flag `  --transfer_config  ` :

``` text
bq mk
    --transfer_config
    --project_id=PROJECT_ID
    --data_source=DATA_SOURCE
    --display_name=NAME
    --target_dataset=DATASET
    --params='PARAMETERS'
```

Where:

  - PROJECT\_ID (optional): your Google Cloud project ID. If `  --project_id  ` isn't supplied to specify a particular project, the default project is used.

  - DATA\_SOURCE : the data source — `  shopify  ` .

  - NAME : the display name for the data transfer configuration. The transfer name can be any value that lets you identify the transfer if you need to modify it later.

  - DATASET : the target dataset for the transfer configuration.

  - PARAMETERS : the parameters for the created transfer configuration in JSON format. For example: `  --params='{"param":"param_value"}'  ` . The following are the parameters for a Shopify data transfer:
    
      - `  assets  ` : the path to the Shopify objects to be transferred to BigQuery.
      - `  connector.shopName  ` : the name of your Shopify shop. For example, if your merchant account ID is `  storename.myshopify.com  ` , then your shop name is `  storename  ` .
      - `  connector.authentication.accessToken  ` : the Shopify Admin API access token.

The following command creates an incremental Shopify data transfer in the default project.

``` text
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

To manually run a data transfer outside of your regular schedule, you can start a [backfill run](/bigquery/docs/working-with-transfers#manually_trigger_a_transfer) .

## Supported tables

The Shopify connector supports the following data objects:

  - `  AppFeedbacks  `
  - `  AppSubscriptionLineItems  ` (Requires a [sales channel app](#limitations) )
  - `  AppSubscriptions  ` (Requires a [sales channel app](#limitations) )
  - `  Catalogs  `
  - `  Collections  `
  - `  Companies  `
  - `  CompanyContactRoleAssignments  `
  - `  CompanyContacts  `
  - `  CompanyLocations  `
  - `  Customers  `
  - `  DeliveryProfiles  `
  - `  DiscountsAutomaticApp  ` (Requires a [discount function](#limitations) )
  - `  DiscountsAutomaticBasic  ` (Requires a [discount function](#limitations) )
  - `  DiscountsAutomaticBxgy  `
  - `  DiscountsCodeApp  `
  - `  DiscountsCodeBasic  `
  - `  DiscountsCodeBxgy  `
  - `  DraftOrders  `
  - `  Files  `
  - `  FulfillmentEvents  `
  - `  FulfillmentOrders  `
  - `  Fulfillments  `
  - `  FulfillmentServices  `
  - `  FulfillmentTrackingInfo  `
  - `  GiftCards  ` (Requires a [ShopifyPlus subscription](#limitations) )
  - `  InventoryItems  `
  - `  Locations  `
  - [`  Metafield  ` objects](https://help.shopify.com/en/manual/custom-data/metafields) , such as `  metafield_product  ` or `  metafield_order  ` .
  - `  OrderRiskAssessments  `
  - `  Orders  `
  - `  OrderTransactions  `
  - `  PriceLists  `
  - `  ProductMediaImages  `
  - `  ProductOptions  `
  - `  ProductOptionValues  `
  - `  ProductResourceFeedbacks  ` (Requires a [sales channel app](#limitations) )
  - `  Products  `
  - `  ProductVariants  `
  - `  Publications  `
  - `  Refunds  `
  - `  Returns  `
  - `  ScriptTags  `
  - `  Segments  `
  - `  SellingPlanGroups  `
  - `  StorefrontAccessTokens  `
  - `  UrlRedirects  `

## Data type mapping

The following table maps Shopify data types to the corresponding BigQuery data types:

<table>
<thead>
<tr class="header">
<th>Shopify data type</th>
<th>BigQuery data type</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       String      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       Int      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       Decimal      </code></td>
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       Double      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       Long      </code></td>
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       Bool      </code></td>
<td><code dir="ltr" translate="no">       BOOL      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       Datetime      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
</tr>
</tbody>
</table>

## Pricing

There is no cost to transfer Shopify data into BigQuery while this feature is in [Preview](https://cloud.google.com/products#product-launch-stages) .

## Troubleshoot transfer setup

If you are having issues setting up your data transfer, see [Shopify transfer issues](/bigquery/docs/transfer-troubleshooting#shopify-issues) .

## What's next

  - For an overview of the BigQuery Data Transfer Service, see [What is BigQuery Data Transfer Service](/bigquery/docs/dts-introduction) .
  - For information on using transfers including getting information about a transfer configuration, listing transfer configurations, and viewing a transfer's run history, see [Manage transfers](/bigquery/docs/working-with-transfers) .
