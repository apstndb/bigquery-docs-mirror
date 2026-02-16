# Load Display & Video 360 data into BigQuery

You can load data from Display & Video 360 to BigQuery using the BigQuery Data Transfer Service for Display & Video 360 connector. With the BigQuery Data Transfer Service, you can schedule recurring transfer jobs that add your latest data from your Display & Video 360 to BigQuery.

## Connector overview

The BigQuery Data Transfer Service for the Display & Video 360 connector supports the following options for your data transfer.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Data transfer options</th>
<th>Support</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Supported reports</td>
<td>The Display &amp; Video 360 connector supports the transfer of data from the reports in <a href="https://developers.google.com/bid-manager/dtv2/reference/file-format">Data Transfer v2 (Display &amp; Video DTv2) files</a> .
<p>For information about how Display &amp; Video 360 reports are transformed into BigQuery tables and views, see <a href="/bigquery/docs/display-video-transformation">Display &amp; Video 360 report transformation</a> .</p></td>
</tr>
<tr class="even">
<td>Repeat frequency</td>
<td>The Display &amp; Video 360 connector supports daily data transfers.<br />
<br />
By default, data transfers are scheduled at the time when the data transfer is created. You can configure the time of data transfer when you <a href="#set_up_dv_360_transfer">set up your data transfer</a> .</td>
</tr>
<tr class="odd">
<td>Refresh window</td>
<td>The Display &amp; Video 360 connector retrieves Display &amp; Video 360 data from up to 2 days at the time the data transfer is run. You cannot configure the refresh window for this connector.<br />
<br />
For more information, see <a href="#refresh">Refresh windows</a> .</td>
</tr>
<tr class="even">
<td>Backfill data availability</td>
<td><a href="/bigquery/docs/working-with-transfers#manually_trigger_a_transfer">Run a data backfill</a> to retrieve data outside of your scheduled data transfer. You can retrieve data as far back as the data retention policy on your data source allows.<br />
<br />
For information about the data retention policy for Display &amp; Video 360, see <a href="https://support.google.com/displayvideo/answer/6110224">Report data freshness and availability</a> .</td>
</tr>
</tbody>
</table>

## Supported configuration data

In addition to the reporting data, BigQuery Data Transfer Service also transfers the following configuration data from Display & Video 360. Configuration data is retrieved from [Display & Video 360 API v3](https://developers.google.com/display-video/api/reference/rest/v3) .

  - [Partner](https://developers.google.com/display-video/api/reference/rest/v3/partners#resource:-partner)
  - [Advertiser](https://developers.google.com/display-video/api/reference/rest/v3/advertisers#resource:-advertiser)
  - [LineItem](https://developers.google.com/display-video/api/reference/rest/v3/advertisers.lineItems#LineItem)
  - [LineItemTargeting](https://developers.google.com/display-video/api/reference/rest/v3/advertisers.lineItems/bulkListAssignedTargetingOptions#LineItemAssignedTargetingOption)
  - [Campaign](https://developers.google.com/display-video/api/reference/rest/v3/advertisers.campaigns#Campaign)
  - [CampaignTargeting](https://developers.google.com/display-video/api/reference/rest/v3/advertisers.campaigns.targetingTypes.assignedTargetingOptions#AssignedTargetingOption)
  - [InsertionOrder](https://developers.google.com/display-video/api/reference/rest/v3/advertisers.insertionOrders#InsertionOrder)
  - [InsertionOrderTargeting](https://developers.google.com/display-video/api/reference/rest/v3/advertisers.insertionOrders.targetingTypes.assignedTargetingOptions#AssignedTargetingOption)
  - [AdGroup](https://developers.google.com/display-video/api/reference/rest/v3/advertisers.adGroups#AdGroup)
  - [AdGroupTargeting](https://developers.google.com/display-video/api/reference/rest/v3/advertisers.adGroups/bulkListAdGroupAssignedTargetingOptions#AdGroupAssignedTargetingOption)
  - [AdGroupAd](https://developers.google.com/display-video/api/reference/rest/v3/advertisers.adGroupAds#AdGroupAd)
  - [Creative](https://developers.google.com/display-video/api/reference/rest/v3/advertisers.creatives#resource:-creative)

For more information about each type of configuration data, see the following links:

  - [About Partners](https://support.google.com/displayvideo/answer/7622449)
  - [Create an advertiser](https://support.google.com/displayvideo/answer/3424070)
  - [Create a line item](https://support.google.com/displayvideo/answer/2891312)
  - [Create a campaign](https://support.google.com/displayvideo/answer/7205081)
  - [Create an insertion order](https://support.google.com/displayvideo/answer/2696705)
  - [About YouTube & partners line items](https://support.google.com/displayvideo/answer/6274216)
  - [Manage creatives](https://support.google.com/displayvideo/answer/7530472)

## Data ingestion from Display & Video 360 transfers

When you transfer data from Display & Video 360 into BigQuery, the data is loaded into BigQuery tables that are partitioned by date. The table partition that the data is loaded into corresponds to the date from the data source. If you schedule multiple transfers for the same date, BigQuery Data Transfer Service overwrites the partition for that specific date with the latest data. Multiple transfers in the same day or running backfills don't result in duplicate data, and partitions for other dates are not affected.

### Refresh windows

A *refresh window* is the number of days that a data transfer retrieves data when a data transfer occurs. For example, if the refresh window is three days and a daily transfer occurs, the BigQuery Data Transfer Service retrieves all data from your source table from the past three days. In this example, when a daily transfer occurs, the BigQuery Data Transfer Service creates a new BigQuery destination table partition with a copy of your source table data from the current day, then automatically triggers backfill runs to update the BigQuery destination table partitions with your source table data from the past two days. The automatically triggered backfill runs will either overwrite or incrementally update your BigQuery destination table, depending on whether or not incremental updates are supported in the BigQuery Data Transfer Service connector.

When you run a data transfer for the first time, the data transfer retrieves all source data available within the refresh window. For example, if the refresh window is three days and you run the data transfer for the first time, the BigQuery Data Transfer Service retrieves all source data within three days.

To retrieve data outside the refresh window, such as historical data, or to recover data from any transfer outages or gaps, you can initiate or schedule a [backfill run](/bigquery/docs/working-with-transfers#manually_trigger_a_transfer) .

## Before you begin

Review the following prerequisites and information before you create a Display & Video 360 data transfer.

### Prerequisites

  - Verify that you have completed all actions required to [enable the BigQuery Data Transfer Service](/bigquery/docs/enable-transfer-service) .

  - [Create a BigQuery dataset](/bigquery/docs/datasets) to store Display & Video 360 data.

  - Ensure that you have either your Display & Video 360 [Partner ID](https://support.google.com/displayvideo/answer/7622449) or [Advertiser ID](https://support.google.com/displayvideo/answer/11415707) . The partner ID is the parent in the hierarchy.

  - Ensure that you have [read permissions](https://support.google.com/displayvideo/answer/2723011) to access partner or advertiser data from the Display and Video API.

  - Ensure that your organization has access to Display & Video 360 Data Transfer v2 (Display & Video 360 DTv2) files. These files are delivered by the Display & Video 360 team in a Cloud Storage bucket. Requesting access to the Display & Video 360 DTv2 files depends on whether or not you have a direct contract with Display & Video 360. In both cases, additional charges might apply.
    
      - If you have a contract with Display & Video 360, [contact Display & Video 360 support](https://support.google.com/displayvideo/answer/9026876) to set up Display & Video 360 DTv2 files.
      - If you don't have a contract with Display & Video 360, contact your agency for access to Display & Video 360 DTv2 files.
      - After completing this step, you will receive either of the following Cloud Storage bucket name, depending if your setup is for a partner or an advertiser:
          - `  gs://dcdt_-dbm_partner PARTNER_ID  `
          - `  gs://dcdt_-dbm_advertiser ADVERTISER_ID  `
    
    **Note:** The Google Cloud team does not have the ability to generate or grant access to Display & Video 360 DTv2 files on your behalf. Contact Display & Video 360 [support](https://support.google.com/displayvideo/answer/9026876) or your agency for access to Display & Video 360 DTv2 files.

  - To set up transfer run notifications for Pub/Sub, you must have `  pubsub.topics.setIamPolicy  ` permissions. For more information, see [BigQuery Data Transfer Service run notifications](/bigquery/docs/transfer-run-notifications) .

### Find your Display & Video 360 ID

To retrieve your Display & Video 360 ID, navigate to the Cloud Storage **Buckets** page in the Google Cloud console and examine the files in your Display & Video 360 data transfer Cloud Storage bucket. The Display & Video 360 ID is used to match files in the provided Cloud Storage bucket. The ID is embedded in the filename, not the Cloud Storage bucket name. For example:

  - In a file named `  dbm_partner123_activity_*  ` , the ID is `  123  ` .
  - In a file named `  dbm_advertiser567_activity_*  ` , the ID is `  567  ` .

### Finding your filename prefix

In some cases, the files in your Cloud Storage bucket might have custom, nonstandard file names that were set up for you by the Google Marketing Platform services team. For example:

In a file named `  dbm_partner123456custom_activity_*  ` , the prefix is `  dbm_partner123456custom  ` .

For any assistance regarding filename prefixes, contact [Display & Video 360 support](https://support.google.com/displayvideo/answer/9026876) .

## Set up a Display & Video 360 data transfer

Select one of the following options:

### Console

1.  Go to the Data transfers page in the Google Cloud console.

2.  Click add **Create transfer** .

3.  On the **Create transfer** page, do the following:
    
      - In the **Source type** section, for **Source** , choose **Display & Video 360** .
      - In the **Transfer config name** section, for **Display name** , enter a name for the data transfer. The transfer name can be any value that lets you identify the transfer if you need to modify it later.

4.  In the **Schedule options** section:
    
      - Select either **Start now** or **Start at set time** , then provide a start date and run time.
      - For **Repeats** , choose an option for how often to run the data transfer. If you select **Days** , provide a valid time in UTC.

5.  In the **Destination settings** section, in the **Destination dataset** menu, select the dataset that you created to store your data.

6.  In the **Data source details** section:
    
      - In the **DV360 DTV2 Cloud Storage bucket** field, enter the Cloud Storage bucket that contains the Display & Video 360 DTv2 files. If you need to set up this bucket, contact Display & Video 360 [support](https://support.google.com/displayvideo/answer/9026876) .
      - In the **DV360 Partner/Advertiser ID** field, enter the [Partner ID](https://support.google.com/displayvideo/answer/7622449) or [Advertiser ID](https://support.google.com/displayvideo/answer/11415707) .
      - Optional: In the **Notification options** section:
          - Click the toggle to enable email notifications. When you enable this option, the transfer administrator receives an email notification when a transfer run fails.
          - Click the toggle to enable Pub/Sub notifications. For **Select a Cloud Pub/Sub topic** , choose your [topic](/pubsub/docs/overview#types) name or click **Create a topic** . This option configures Pub/Sub run [notifications](/bigquery/docs/transfer-run-notifications) for your transfer.

7.  Click **Save** .

### bq

Enter the `  bq mk  ` command and supply the transfer creation flag — `  --transfer_config  ` . The following flags are required:

  - `  --data_source  `
  - `  --target_dataset  `
  - `  --display_name  `
  - `  --params  `

<!-- end list -->

``` text
  bq mk --transfer_config \
  --project_id=PROJECT_ID \
  --target_dataset=DATASET \
  --display_name=NAME \
  --params='PARAMETERS' \
  --data_source=DATA_SOURCE
```

Where:

  - PROJECT\_ID : your project ID.
  - DATASET : the target dataset for the data transfer configuration.
  - NAME : the display name for the data transfer configuration. The transfer name can be any value that lets you identify the transfer if you need to modify it later.
  - PARAMETERS : the parameters for the created data transfer configuration in JSON format. For example— `  --params='{"param":"param_value"}'  ` . For Display & Video 360 transfers, the `  bucket  ` and `  displayvideo_id  ` parameters are required. The `  file_name_prefix  ` parameter is optional and used for rare, custom file names only.
  - DATA\_SOURCE : the data source — `  displayvideo  ` .

For example, the following command creates a Display & Video 360 data transfer named `  My Transfer  ` using Display & Video 360 ID `  123456  ` , Cloud Storage bucket `  dcdt_-dbm_partner123456  ` , and target dataset `  mydataset  ` .

The data transfer is created in the default project:

``` text
  bq mk --transfer_config \
  --target_dataset=mydataset \
  --display_name='My Transfer' \
  --params='{"bucket":"dcdt_-dbm_partner123456","displayvideo_id": "123456","file_name_prefix":"YYY"}' \
  --data_source=displayvideo
```

After running the command, you receive a message like the following:

`  [URL omitted] Please copy and paste the above URL into your web browser and follow the instructions to retrieve an authentication code.  `

Follow the instructions in the message and paste the authentication code on the command line.

### API

Use the [`  projects.locations.transferConfigs.create  `](/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs/create) method and supply an instance of the [`  TransferConfig  `](/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs#TransferConfig) resource.

## Query your data

When your data is transferred to BigQuery, the data is written to ingestion-time partitioned tables. For more information, see [Introduction to partitioned tables](/bigquery/docs/partitioned-tables) .

We recommend that you query the auto-generated views instead of querying the tables directly. However, if you want to query your tables directly, you must use the `  _PARTITIONTIME  ` pseudocolumn in your query. For more information, see [Querying partitioned tables](/bigquery/docs/querying-partitioned-tables) .
