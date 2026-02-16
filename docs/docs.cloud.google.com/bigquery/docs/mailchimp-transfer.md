# Load Mailchimp data into BigQuery

**Preview**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

**Note:** To get support or provide feedback for this feature, contact <dts-preview-support@google.com> .

You can load data from Mailchimp to BigQuery using the BigQuery Data Transfer Service for Mailchimp connector. With the BigQuery Data Transfer Service, you can schedule recurring transfer jobs that add your latest data from Mailchimp to BigQuery. The Mailchimp connector has multi-account support, including both Standard and Express Mailchimp accounts.

## Limitations

  - The Mailchimp marketing API only supports a maximum of 10 simultaneous connections per user. Exceeding this limit results in the error `  429: TooManyRequests: You have exceeded the limit of 10 simultaneous connections  `
      - To avoid reaching this rate limit, we recommend only running one data transfer per Mailchimp account.
      - For more information, see [Error glossary](https://mailchimp.com/developer/marketing/docs/errors/#error-glossary) .
  - The `  Integer  ` data type in Mailchimp has a maximum supported value of 2,147,483,647 across all objects.
      - However, some Mailchimp fields support higher values, such as the `  Quantity  ` field in `  EcommerceOrderLines  ` and `  EcommerceCartLines  ` .

### Array field limitations

Mailchimp connector doesn't support `  ARRAY  ` fields in the following Mailchimp objects:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Mailchimp Object</th>
<th>Unsupported <code dir="ltr" translate="no">       ARRAY      </code> fields</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       Campaigns      </code></td>
<td><code dir="ltr" translate="no">       VariateSettings_SubjectLines      </code><br />
<code dir="ltr" translate="no">       VariateSettings_SendTimes      </code><br />
<code dir="ltr" translate="no">       VariateSettings_FromNames      </code><br />
<code dir="ltr" translate="no">       VariateSettings_ReplyToAddresses      </code><br />
<code dir="ltr" translate="no">       VariateSettings_Contents      </code><br />
<code dir="ltr" translate="no">       VariateSettings_Combinations      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       EcommerceCarts      </code></td>
<td><code dir="ltr" translate="no">       Lines      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       EcommerceProducts      </code></td>
<td><code dir="ltr" translate="no">       Variants      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ListMembers      </code></td>
<td><code dir="ltr" translate="no">       TagsAggregate      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       ListMergeFields      </code></td>
<td><code dir="ltr" translate="no">       Options_Choices      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       Lists      </code></td>
<td><code dir="ltr" translate="no">       Modules      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       AuthorizedApps      </code></td>
<td><code dir="ltr" translate="no">       Users      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       AutomationEmails      </code></td>
<td><code dir="ltr" translate="no">       Settings_AutoFbPost      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       CampaignOpenEmailDetails      </code></td>
<td><code dir="ltr" translate="no">       Opens      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       EcommerceProductImages      </code></td>
<td><code dir="ltr" translate="no">       VariantIds      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       ListSignupForms      </code></td>
<td><code dir="ltr" translate="no">       Contents      </code> , <code dir="ltr" translate="no">       Styles      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ReportEmailActivity      </code></td>
<td><code dir="ltr" translate="no">       Activity      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       Reports      </code></td>
<td><code dir="ltr" translate="no">       Timewarp      </code></td>
</tr>
</tbody>
</table>

## Before you begin

The following sections describe the prerequisites that you need to do before you create a Mailchimp data transfer.

### Mailchimp prerequisites

To enable data transfers from Mailchimp to BigQuery, you must have a Mailchimp API key for authorization and access. For information on obtaining an API key, see [Generate an API key](https://mailchimp.com/help/about-api-keys/#Generate_an_API_key) .

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

If you intend to set up transfer run notifications for Pub/Sub, ensure that you have the `  pubsub.topics.setIamPolicy  ` IAM permission. Pub/Sub permissions aren't required if you only set up email notifications. For more information, see [BigQuery Data Transfer Service run notifications](/bigquery/docs/transfer-run-notifications) .

## Set up a Mailchimp data transfer

Add Mailchimp data into BigQuery by setting up a transfer configuration using one of the following options:

### Console

1.  Go to the Data transfers page in the Google Cloud console.

2.  Click add **Create transfer** .

3.  In the **Source type** section, for **Source** , choose **Mailchimp - Preview** .

4.  In the **Data source details** section, do the following:
    
      - For **API Key** , enter your Mailchimp API key. For more information, see [Mailchimp prerequisites](/bigquery/docs/mailchimp-transfer#mailchimp-prerequisites) .
      - Optional: For **Start Date** , specify a start date for new records to be included in the data transfer. Only records created on or after this date are included in the data transfer.
          - Enter a data in the format `  YYYY-MM-DD  ` . The minimum value is `  2001-01-01  ` .
      - For **Mailchimp objects to transfer** , click **Browse** to select any objects to be transferred to the BigQuery destination dataset. You can also manually enter any objects to include in the data transfer in this field.

5.  In the **Destination settings** section, for **Dataset** , choose the dataset that you created to store your data.

6.  In the **Transfer config name** section, for **Display name** , enter a name for the data transfer.

7.  In the **Schedule options** section:
    
      - In the **Repeat frequency** list, select an option to specify how often this data transfer runs. To specify a custom repeat frequency, select **Custom** . If you select **On-demand** , then this transfer runs when you [manually trigger the transfer](/bigquery/docs/working-with-transfers#manually_trigger_a_transfer) .
      - If applicable, select either **Start now** or **Start at set time** , and provide a start date and run time.

8.  Optional: In the **Notification options** section, do the following:
    
      - To enable email notifications, click the **Email notification** toggle. When you enable this option, the transfer administrator receives an email notification when a transfer run fails.
      - To enable [Pub/Sub transfer run notifications](/bigquery/docs/transfer-run-notifications) for this transfer, click the **Pub/Sub notifications** toggle. You can select your [topic](/pubsub/docs/publish-message-overview) name, or you can click **Create a topic** to create one.

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

Replace the following:

  - `  PROJECT_ID  ` (optional): your Google Cloud project ID. If `  --project_id  ` isn't supplied to specify a particular project, the default project is used.

  - `  DATA_SOURCE  ` : the data source — `  mailchimp  ` .

  - `  NAME  ` : the display name for the data transfer configuration. The transfer name can be any value that lets you identify the transfer if you need to modify it later.

  - `  DATASET  ` : the target dataset for the transfer configuration.

  - `  PARAMETERS  ` : the parameters for the created transfer configuration in JSON format. For example: `  --params='{"param":"param_value"}'  ` . The following are the parameters for a Mailchimp data transfer:
    
      - `  assets  ` : the path to the Mailchimp objects to be transferred to BigQuery.
      - `  connector.authentication.apiKey  ` : the Mailchimp API key.
      - `  connector.startDate  ` : (Optional) a start date for new records to be included in the data transfer, in the format `  YYYY-MM-DD  ` . Only records created on or after this date are included in the data transfer.

The following command creates a Mailchimp data transfer in the default project.

``` text
    bq mk
        --transfer_config
        --target_dataset=mydataset
        --data_source=mailchimp
        --display_name='My Transfer'
        --params='{"assets": "Lists",
            "connector.authentication.apiKey":"1234567",
            "connector.startDate":"2025-01-01"}'
```

When you save the transfer configuration, the Mailchimp connector automatically triggers a transfer run according to your schedule option. With every transfer run, the Mailchimp connector transfers all available data from Mailchimp into BigQuery.

To manually run a data transfer outside of your regular schedule, you can start a [backfill run](/bigquery/docs/working-with-transfers#manually_trigger_a_transfer) .

## Data type mapping

The following table maps Mailchimp data types to the corresponding BigQuery data types:

<table>
<thead>
<tr class="header">
<th>Mailchimp data type</th>
<th>BigQuery data type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       String      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       Integer      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       Number      </code></td>
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
<td>Mailchimp <code dir="ltr" translate="no">       Number      </code> data objects are mapped to either the <code dir="ltr" translate="no">       BIGNUMERIC      </code> data type for financial-related fields such as <code dir="ltr" translate="no">       Price      </code> and <code dir="ltr" translate="no">       OrderTotal      </code> , or the <code dir="ltr" translate="no">       FLOAT64      </code> data type, for other fields such as <code dir="ltr" translate="no">       Stats_OpenRate      </code> and <code dir="ltr" translate="no">       Location_Latitude      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       Number      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       Boolean      </code></td>
<td><code dir="ltr" translate="no">       BOOLEAN      </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       String      </code> in date-time format</td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code> data types in date-time format are represented in ISO 8601 format. For example, <code dir="ltr" translate="no">       2019-08-24T14:15:22Z      </code> .</td>
</tr>
</tbody>
</table>

## Pricing

There is no cost to transfer Mailchimp data into BigQuery while this feature is in [Preview](https://cloud.google.com/products#product-launch-stages) .

## Troubleshoot transfer setup

If you are having issues setting up your data transfer, see [Mailchimp transfer issues](/bigquery/docs/transfer-troubleshooting#mailchimp-issues) .

## What's next

  - For an overview of the BigQuery Data Transfer Service, see [What is BigQuery Data Transfer Service](/bigquery/docs/dts-introduction) .
  - For information on using transfers including getting information about a transfer configuration, listing transfer configurations, and viewing a transfer's run history, see [Manage transfers](/bigquery/docs/working-with-transfers) .
