# Load Google Ad Manager data into BigQuery

You can load data from Google Ad Manager to BigQuery using the BigQuery Data Transfer Service for Google Ad Manager connector. With the BigQuery Data Transfer Service, you can schedule recurring transfer jobs that add your latest data from Google Ad Manager to BigQuery.

## Connector overview

The BigQuery Data Transfer Service for the Google Ad Manager connector supports the following options for your data transfer.

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
<td>The Google Ad Manager connector supports the transfer of data from the following reports:<br />

<ul>
<li><a href="https://support.google.com/admanager/answer/1733124">Data Transfer (Google Ad Manager DT) files</a></li>
<li><a href="https://support.google.com/admanager/table/7401123">Data Transfer fields</a></li>
<li><a href="/bigquery/docs/doubleclick-publisher-transformation">Match tables provided by the BigQuery Data Transfer Service</a> . These are automatically created and updated.</li>
<li><a href="https://developers.google.com/doubleclick-publishers/docs/pqlreference#matchtables">Match tables fetched with PQL</a></li>
<li><a href="https://developers.google.com/doubleclick-publishers/docs/reference/v201908/CompanyService">Match tables from CompanyService (v201908)</a></li>
<li><a href="https://developers.google.com/doubleclick-publishers/docs/reference/v201908/OrderService">Match tables from OrderService (v201908)</a></li>
<li><a href="https://developers.google.com/doubleclick-publishers/docs/reference/v201908/PlacementService">Match tables from PlacementService (v201908)</a></li>
</ul>
<p>For information about how Google Ad Manager reports are transformed into BigQuery tables and views, see <a href="/bigquery/docs/doubleclick-publisher-transformation">Google Ad Manager report transformation</a> .</p></td>
</tr>
<tr class="even">
<td>Repeat frequency</td>
<td>The Google Ad Manager connector supports data transfers every 4 hours. By default, Google Ad Manager data transfers repeat every 8 hours.<br />
<br />
You can configure the time of data transfer when you <a href="#set_up_a_google_ad_manager_transfer">set up your data transfer</a> .</td>
</tr>
<tr class="odd">
<td>Refresh window</td>
<td>The Google Ad Manager connector retrieves Google Ad Manager data from up to 2 days at the time the data transfer is run. You cannot configure the refresh window for this connector.<br />
<br />
For more information, see <a href="#refresh">Refresh windows</a> .</td>
</tr>
<tr class="even">
<td>Backfill data availability</td>
<td><a href="/bigquery/docs/working-with-transfers#manually_trigger_a_transfer">Run a data backfill</a> to retrieve data outside of your scheduled data transfer. You can retrieve data as far back as the data retention policy on your data source allows.<br />
<br />
For information about the data retention policy for Google Ad Manager, see <a href="https://support.google.com/admanager/answer/1733124">Google Ad Manager Data Transfer reports</a> .</td>
</tr>
</tbody>
</table>

**Note:** The BigQuery Data Transfer Service supports the following delimiters for Google Ad Manager DT files: Tab ( \\t ), Pipe ( | ), Caret ( ^ ), and Comma ( , ).

## Data ingestion from Google Ad Manager transfers

When you transfer data from Google Ad Manager into BigQuery, the data is loaded into BigQuery tables that are partitioned by date. The table partition that the data is loaded into corresponds to the date from the data source. If you schedule multiple transfers for the same date, BigQuery Data Transfer Service overwrites the partition for that specific date with the latest data. Multiple transfers in the same day or running backfills don't result in duplicate data, and partitions for other dates are not affected.

### Refresh windows

A *refresh window* is the number of days that a data transfer retrieves data when a data transfer occurs. For example, if the refresh window is three days and a daily transfer occurs, the BigQuery Data Transfer Service retrieves all data from your source table from the past three days. In this example, when a daily transfer occurs, the BigQuery Data Transfer Service creates a new BigQuery destination table partition with a copy of your source table data from the current day, then automatically triggers backfill runs to update the BigQuery destination table partitions with your source table data from the past two days. The automatically triggered backfill runs will either overwrite or incrementally update your BigQuery destination table, depending on whether or not incremental updates are supported in the BigQuery Data Transfer Service connector.

When you run a data transfer for the first time, the data transfer retrieves all source data available within the refresh window. For example, if the refresh window is three days and you run the data transfer for the first time, the BigQuery Data Transfer Service retrieves all source data within three days.

To retrieve data outside the refresh window, such as historical data, or to recover data from any transfer outages or gaps, you can initiate or schedule a [backfill run](/bigquery/docs/working-with-transfers#manually_trigger_a_transfer) .

### Updates to data transfer (DT) files

Tables that are created from Google Ad Manager data transfer (Google Ad Manager DT) files can be updated incrementally. Google Ad Manager adds the Google Ad Manager DT files into the Cloud Storage bucket. A transfer run then incrementally loads the new Google Ad Manager DT files from the Cloud Storage bucket into the BigQuery table without reloading files that have already been transferred to the BigQuery table.

For example, Google Ad Manager adds `  file1  ` into the bucket at 1:00 AM and `  file2  ` at 2:00 AM. A transfer run begins at 3:30 AM and loads `  file1  ` and `  file2  ` to BigQuery. Google Ad Manager then adds `  file3  ` at 5:00 AM and `  file4  ` at 6:00 AM. A second transfer run begins at 7:30AM and appends `  file3  ` and `  file4  ` into BigQuery, instead of overwriting the table by loading all four files.

### Updates to match tables

Match tables provide a lookup mechanism for the raw values contained within data transfer files. For a list of match tables, see [Google Ad Manager report transformation](/bigquery/docs/doubleclick-publisher-transformation) . Different match tables are updated with different ingestion methods. The match tables and their ingestion methods are listed in the following table:

<table>
<thead>
<tr class="header">
<th>Ingestion method</th>
<th>Description</th>
<th>Match table</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Incremental update</td>
<td>Incremental updates are appended in every run. For example, a first transfer run of the day loads all data modified before the transfer run, the second transfer run in the same day loads data modified after the previous run and before the current run.</td>
<td><code dir="ltr" translate="no">       Company      </code> , <code dir="ltr" translate="no">       Order      </code> , <code dir="ltr" translate="no">       Placement      </code> , <code dir="ltr" translate="no">       LineItem      </code> , <code dir="ltr" translate="no">       AdUnit      </code></td>
</tr>
<tr class="even">
<td>Whole table update</td>
<td>Whole table updates loads the whole table once a day. For example, a first transfer run of the day loads all available data for a table. A second transfer run on the same day skips loading these tables.</td>
<td><code dir="ltr" translate="no">       AdCategory      </code> , <code dir="ltr" translate="no">       AudienceSegmentCategory      </code> , <code dir="ltr" translate="no">       BandwidthGroup      </code> , <code dir="ltr" translate="no">       Browser      </code> , <code dir="ltr" translate="no">       BrowserLanguage      </code> , <code dir="ltr" translate="no">       DeviceCapability      </code> , <code dir="ltr" translate="no">       DeviceCategory      </code> , <code dir="ltr" translate="no">       DeviceManufacturer      </code> , <code dir="ltr" translate="no">       GeoTarget      </code> , <code dir="ltr" translate="no">       MobileCarrier      </code> , <code dir="ltr" translate="no">       MobileDevice      </code> , <code dir="ltr" translate="no">       MobileDeviceSubmodel      </code> , <code dir="ltr" translate="no">       OperatingSystem      </code> , <code dir="ltr" translate="no">       OperatingSystemVersion      </code> , <code dir="ltr" translate="no">       ThirdPartyCompany      </code> , <code dir="ltr" translate="no">       TimeZone      </code> , <code dir="ltr" translate="no">       User      </code> , <code dir="ltr" translate="no">       ProgrammaticBuyer      </code></td>
</tr>
<tr class="odd">
<td>Whole table overwrite</td>
<td>The whole table is overwritten with every transfer run.</td>
<td><code dir="ltr" translate="no">       AudienceSegment      </code></td>
</tr>
</tbody>
</table>

## Before you begin

Before you create a Google Ad Manager data transfer:

  - Verify that you have completed all actions required to [enable the BigQuery Data Transfer Service](/bigquery/docs/enable-transfer-service) .

  - [Create a BigQuery dataset](/bigquery/docs/datasets) to store the Google Ad Manager data.

  - **Ensure that your organization has access to Google Ad Manager Data Transfer (Google Ad Manager DT) files.** These files are delivered by the Google Ad Manager team to a Cloud Storage bucket. To gain access to Google Ad Manager DT files, review [Ad Manager Data Transfer reports](https://support.google.com/admanager/answer/1733124) . Additional charges from the Google Ad Manager team might apply.
    
    After completing this step, you will receive a Cloud Storage bucket similar to the following:
    
    ``` text
        gdfp-12345678
      
    ```
    
    The Google Cloud team does **NOT** have the ability to generate or grant access to Google Ad Manager DT files on your behalf. Contact, Google Ad Manager [support](https://support.google.com/admanager/answer/3059042?&ref_topic=7519191) , for access to Google Ad Manager DT files.

  - [Enable API access](https://support.google.com/admanager/answer/3088588) to your Google Ad Manager network.

  - If you intend to set up data transfer notifications, you must have `  pubsub.topics.setIamPolicy  ` permissions for Pub/Sub. Pub/Sub permissions are not required if you just set up email notifications. For more information, see [BigQuery Data Transfer Service run notifications](/bigquery/docs/transfer-run-notifications) .

## Required permissions

Ensure that you have granted the following permissions.

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

### Required Google Ad Manager roles

Grant read access to the Google Ad Manager DT files stored in Cloud Storage. Permissions for Google Ad Manager DT files are managed by the Google Ad Manager team. In addition to the Google Ad Manager DT files, the person creating the data transfer must be added to the Google Ad Manager network, with read access to all the entities needed to create the various [match tables](/bigquery/docs/doubleclick-publisher-transformation) (line item, order, ad unit, etc.). This can be accomplished by adding the Ad Manager user who authenticated the data transfer to the [All Entities team](https://support.google.com/admanager/answer/2445815?#:%7E:text=All%20entities%C2%A0team,with%20their%20account) in Ad Manager.

## Set up a Google Ad Manager transfer

Setting up a BigQuery data transfer for Google Ad Manager requires a:

  - **Cloud Storage bucket** : The Cloud Storage bucket URI for your Google Ad Manager DT files as described in [Before you begin](/bigquery/docs/doubleclick-publisher-transfer#before_you_begin) . The bucket name should look like the following:
    
    ``` text
    gdfp-12345678
    ```

  - **Network Code** : You'll find the Google Ad Manager network code in the URL when you are logged into your network. For example, in the URL `  https://admanager.google.com/2032576#delivery  ` , `  2032576  ` is your network code. For more information, see [Get started with Google Ad Manager](https://developers.google.com/doubleclick-publishers/docs/start) .

To create a BigQuery Data Transfer Service data transfer for Google Ad Manager:

### Console

1.  Go to the Data transfers page in the Google Cloud console.

2.  Click add **Create a transfer** .

3.  On the **Create Transfer** page:
    
      - In the **Source type** section, for **Source** , choose **Google Ad Manager (formerly DFP)** .
    
    <!-- end list -->
    
      - In the **Transfer config name** section, for **Display name** , enter a name for the data transfer such as `  My Transfer  ` . The transfer name can be any value that lets you identify the transfer if you need to modify it later.
    
    <!-- end list -->
    
      - In the **Destination settings** section, for **Dataset** , choose the dataset that you created to store your data.
    
    <!-- end list -->
    
      - In the **Data source details** section:
          - For **Cloud Storage bucket** , enter the name of the Cloud Storage bucket that stores your data transfer files. When you enter the bucket name, don't include `  gs://  ` .
          - For **Network code** , enter your network code.
    
    <!-- end list -->
    
      - In the **Service account** menu, select a [service account](/iam/docs/service-account-overview) from the service accounts associated with your Google Cloud project. You can associate a service account with your transfer instead of using your user credentials. For more information about using service accounts with data transfers, see [Use service accounts](/bigquery/docs/use-service-accounts) .  
          
        If you signed in with a [federated identity](/iam/docs/workforce-identity-federation) , then a service account is required to create a transfer. If you signed in with a Google Account, then a service account for the transfer is optional. The service account must have the [required permissions](/bigquery/docs/doubleclick-publisher-transfer#required_permissions) .
    
      - (Optional) In the **Notification options** section:
        
          - Click the toggle to enable email notifications. When you enable this option, the transfer administrator receives an email notification when a transfer run fails.
          - Click the toggle to enable Pub/Sub run notifications. For **Select a Cloud Pub/Sub topic** , choose your topic name or click **Create a topic** . This option configures Pub/Sub run [notifications](/bigquery/docs/transfer-run-notifications) for your transfer.

4.  Click **Save** .

### bq

Enter the `  bq mk  ` command and supply the transfer creation flag — `  --transfer_config  ` . The following flags are also required:

  - `  --data_source  `
  - `  --target_dataset  `
  - `  --display_name  `
  - `  --params  `

Optional flags:

  - `  --service_account_name  ` - Specifies a service account to use for Google Ad Manager transfer authentication instead of your user account.

<!-- end list -->

``` text
bq mk --transfer_config \
--project_id=project_id \
--target_dataset=dataset \
--display_name=name \
--params='parameters' \
--data_source=data_source \
--service_account_name=service_account_name
```

Where:

  - project\_id is your project ID.
  - dataset is the target dataset for the transfer configuration.
  - name is the display name for the data transfer configuration. The transfer name can be any value that lets you identify the data transfer if you need to modify it later.
  - parameters contains the parameters for the created transfer configuration in JSON format. For example: `  --params='{"param":"param_value"}'  ` . For Google Ad Manager, you must supply the `  bucket  ` and `  network_code  ` , parameters.
      - `  bucket  ` : The Cloud Storage bucket that contains your Google Ad Manager DT files.
      - `  network_code  ` : Network code
      - `  load_match_tables  ` : Whether to load match tables. By default set to `  True  `
  - data\_source is the data source — `  dfp_dt  ` (Google Ad Manager).
  - service\_account\_name is the service account name used to authenticate your data transfer. The service account should be owned by the same `  project_id  ` used to create the transfer and it should have all of the [required permissions](#required_permissions) .

**Caution:** You cannot configure notifications using the command-line tool.

You can also supply the `  --project_id  ` flag to specify a particular project. If `  --project_id  ` isn't specified, the default project is used.

For example, the following command creates a Google Ad Manager data transfer named `  My Transfer  ` using network code `  12345678  ` , Cloud Storage bucket `  gdfp-12345678  ` , and target dataset `  mydataset  ` . The data transfer is created in the default project:

``` text
bq mk --transfer_config \
--target_dataset=mydataset \
--display_name='My Transfer' \
--params='{"bucket": "gdfp-12345678","network_code": "12345678"}' \
--data_source=dfp_dt
```

After running the command, you receive a message like the following:

`  [URL omitted] Please copy and paste the above URL into your web browser and follow the instructions to retrieve an authentication code.  `

Follow the instructions and paste the authentication code on the command line.

### API

Use the [`  projects.locations.transferConfigs.create  `](/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs/create) method and supply an instance of the [`  TransferConfig  `](/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs#TransferConfig) resource.

### Java

Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Java API reference documentation](/java/docs/reference/google-cloud-bigquery/latest/overview) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` java
import com.google.api.gax.rpc.ApiException;
import com.google.cloud.bigquery.datatransfer.v1.CreateTransferConfigRequest;
import com.google.cloud.bigquery.datatransfer.v1.DataTransferServiceClient;
import com.google.cloud.bigquery.datatransfer.v1.ProjectName;
import com.google.cloud.bigquery.datatransfer.v1.TransferConfig;
import com.google.protobuf.Struct;
import com.google.protobuf.Value;
import java.io.IOException;
import java.util.HashMap;
import java.util.Map;

// Sample to create a ad manager(formerly DFP) transfer config
public class CreateAdManagerTransfer {

  public static void main(String[] args) throws IOException {
    // TODO(developer): Replace these variables before running the sample.
    final String projectId = "MY_PROJECT_ID";
    String datasetId = "MY_DATASET_ID";
    String bucket = "gs://cloud-sample-data";
    // the network_code can only be digits with length 1 to 15
    String networkCode = "12345678";
    Map<String, Value> params = new HashMap<>();
    params.put("bucket", Value.newBuilder().setStringValue(bucket).build());
    params.put("network_code", Value.newBuilder().setStringValue(networkCode).build());
    TransferConfig transferConfig =
        TransferConfig.newBuilder()
            .setDestinationDatasetId(datasetId)
            .setDisplayName("Your Ad Manager Config Name")
            .setDataSourceId("dfp_dt")
            .setParams(Struct.newBuilder().putAllFields(params).build())
            .build();
    createAdManagerTransfer(projectId, transferConfig);
  }

  public static void createAdManagerTransfer(String projectId, TransferConfig transferConfig)
      throws IOException {
    try (DataTransferServiceClient client = DataTransferServiceClient.create()) {
      ProjectName parent = ProjectName.of(projectId);
      CreateTransferConfigRequest request =
          CreateTransferConfigRequest.newBuilder()
              .setParent(parent.toString())
              .setTransferConfig(transferConfig)
              .build();
      TransferConfig config = client.createTransferConfig(request);
      System.out.println("Ad manager transfer created successfully :" + config.getName());
    } catch (ApiException ex) {
      System.out.print("Ad manager transfer was not created." + ex.toString());
    }
  }
}
```

**Warning:** If you change the schema of a report, all files on that day must have the same schema, or the data transfer for the entire day will fail.

## Troubleshoot Google Ad Manager transfer setup

If you are having issues setting up your data transfer, see [Google Ad Manager transfer issues](/bigquery/docs/transfer-troubleshooting#google_ad_manager_transfer_issues) in [Troubleshooting transfer configurations](/bigquery/docs/transfer-troubleshooting) .

## Query your data

When your data is transferred to BigQuery, the data is written to ingestion-time partitioned tables. For more information, see [Introduction to partitioned tables](/bigquery/docs/partitioned-tables) .

If you query your tables directly instead of using the auto-generated views, you must use the `  _PARTITIONTIME  ` pseudocolumn in your query. For more information, see [Querying partitioned tables](/bigquery/docs/querying-partitioned-tables) .

## Sample queries

You can use the following Google Ad Manager sample queries to analyze your transferred data. You can also use the queries in a visualization tool such as [Looker Studio](https://www.google.com/analytics/data-studio/) . These queries are provided to help you get started on querying your Google Ad Manager data with BigQuery. For additional questions on what you can do with these reports, contact your Google Ad Manager technical representative.

**Note:** If you query your tables directly instead of using the auto-generated views, you must use the `  _PARTITIONTIME  ` pseudocolumn in your query. For more information, see [Querying partitioned tables](/bigquery/docs/querying-partitioned-tables) .

In each of the following queries, replace variables like dataset with your values. For example, replace network\_code with your Google Ad Manager network code.

### Impressions and unique users by city

The following SQL sample query analyzes the number of impressions and unique users by city over the past 30 days.

``` text
# START_DATE = DATE_ADD(CURRENT_DATE(), INTERVAL -31 DAY)
# END_DATE = DATE_ADD(CURRENT_DATE(), INTERVAL -1 DAY)
SELECT
  City,
  _DATA_DATE AS Date,
  count(*) AS imps,
  count(distinct UserId) AS uniq_users
FROM `dataset.NetworkImpressions_network_code`
WHERE
  _DATA_DATE BETWEEN start_date AND end_date
GROUP BY City, Date
```

### Impressions and unique users by line item type

The following SQL sample query analyzes the number of impressions and unique users by line item type over the past 30 days.

``` text
# START_DATE = DATE_ADD(CURRENT_DATE(), INTERVAL -31 DAY)
# END_DATE = DATE_ADD(CURRENT_DATE(), INTERVAL -1 DAY)
SELECT
  MT.LineItemType AS LineItemType,
  DT._DATA_DATE AS Date,
  count(*) AS imps,
  count(distinct UserId) AS uniq_users
FROM `dataset.NetworkImpressions_network_code` AS DT
LEFT JOIN `dataset.MatchTableLineItem_network_code` AS MT
ON
  DT.LineItemId = MT.Id
WHERE
  DT._DATA_DATE BETWEEN start_date AND end_date
GROUP BY LineItemType, Date
ORDER BY Date desc, imps desc
```

### Impressions by ad unit

The following SQL sample query analyzes the number of impressions by ad unit over the past 30 days.

``` text
# START_DATE = DATE_ADD(CURRENT_DATE(), INTERVAL -31 DAY)
# END_DATE = DATE_ADD(CURRENT_DATE(), INTERVAL -1 DAY)
SELECT
  MT.AdUnitCode AS AdUnitCode,
  DT.DATA_DATE AS Date,
  count(*) AS imps
FROM `dataset.NetworkImpressions_network_code` AS DT
LEFT JOIN `dataset.MatchTableAdUnit_network_code` AS MT
ON
  DT.AdUnitId = MT.Id
WHERE
  DT._DATA_DATE BETWEEN start_date AND end_date
GROUP BY AdUnitCode, Date
ORDER BY Date desc, imps desc
```

### Impressions by line item

The following SQL sample query analyzes the number of impressions by line item over the past 30 days.

``` text
# START_DATE = DATE_ADD(CURRENT_DATE(), INTERVAL -31 DAY)
# END_DATE = DATE_ADD(CURRENT_DATE(), INTERVAL -1 DAY)
SELECT
  MT.Name AS LineItemName,
  DT._DATA_DATE AS Date,
  count(*) AS imps
FROM `dataset.NetworkImpressions_network_code` AS DT
LEFT JOIN `dataset.MatchTableLineItem_network_code` AS MT
ON
  DT.LineItemId = MT.Id
WHERE
  DT._DATA_DATE BETWEEN start_date AND end_date
GROUP BY LineItemName, Date
ORDER BY Date desc, imps desc
```
