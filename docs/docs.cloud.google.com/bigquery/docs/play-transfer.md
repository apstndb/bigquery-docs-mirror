# Load Google Play data into BigQuery

You can load data from Google Play to BigQuery using the BigQuery Data Transfer Service for Google Play connector. With the BigQuery Data Transfer Service, you can schedule recurring transfer jobs that add your latest data from Google Play to BigQuery.

## Connector overview

The BigQuery Data Transfer Service for the Google Play connector supports the following options for your data transfer.

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
<td><ul>
<li>Detailed reports:
<ul>
<li><a href="https://support.google.com/googleplay/android-developer/answer/6135870#reviews">Reviews</a></li>
<li><a href="https://support.google.com/googleplay/android-developer/answer/6135870#financial">Financial reports</a></li>
</ul></li>
<li>Aggregated reports:
<ul>
<li><a href="https://support.google.com/googleplay/android-developer/answer/6135870#statistics">Statistics</a></li>
<li><a href="https://support.google.com/googleplay/android-developer/answer/6135870#acquisition">User acquisition</a></li>
</ul></li>
</ul>
<p>For information about how Google Play reports are transformed into BigQuery tables and views, see <a href="/bigquery/docs/play-transformation">Google Play report transformation</a> .</p></td>
</tr>
<tr class="even">
<td>Repeat frequency</td>
<td>The Google Play connector supports daily data transfers.<br />
<br />
By default, data transfers are scheduled at the time when the data transfer is created. You can configure the time of data transfer when you <a href="#setup-transfer">set up your data transfer</a> .</td>
</tr>
<tr class="odd">
<td>Refresh window</td>
<td>The Google Play connector retrieves Google Play data from up to 7 days at the time the data transfer is run.<br />
<br />
For more information, see <a href="#refresh">Refresh windows</a> .</td>
</tr>
<tr class="even">
<td>Backfill data availability</td>
<td><a href="/bigquery/docs/working-with-transfers#manually_trigger_a_transfer">Run a data backfill</a> to retrieve data outside of your scheduled data transfer. You can retrieve data as far back as the data retention policy on your data source allows.</td>
</tr>
</tbody>
</table>

## Data ingestion from Google Play transfers

When you transfer data from Google Play into BigQuery, the data is loaded into BigQuery tables that are partitioned by date. The table partition that the data is loaded into corresponds to the date from the data source. If you schedule multiple transfers for the same date, BigQuery Data Transfer Service overwrites the partition for that specific date with the latest data. Multiple transfers in the same day or running backfills don't result in duplicate data, and partitions for other dates are not affected.

### Refresh windows

A *refresh window* is the number of days that a data transfer retrieves data when a data transfer occurs. For example, if the refresh window is three days and a daily transfer occurs, the BigQuery Data Transfer Service retrieves all data from your source table from the past three days. In this example, when a daily transfer occurs, the BigQuery Data Transfer Service creates a new BigQuery destination table partition with a copy of your source table data from the current day, then automatically triggers backfill runs to update the BigQuery destination table partitions with your source table data from the past two days. The automatically triggered backfill runs will either overwrite or incrementally update your BigQuery destination table, depending on whether or not incremental updates are supported in the BigQuery Data Transfer Service connector.

When you run a data transfer for the first time, the data transfer retrieves all source data available within the refresh window. For example, if the refresh window is three days and you run the data transfer for the first time, the BigQuery Data Transfer Service retrieves all source data within three days.

To retrieve data outside the refresh window, such as historical data, or to recover data from any transfer outages or gaps, you can initiate or schedule a [backfill run](/bigquery/docs/working-with-transfers#manually_trigger_a_transfer) .

## Limitations

  - The minimum frequency that you can schedule a data transfer for is once every 24 hours. By default, a transfer starts at the time that you create the transfer. However, you can configure the transfer start time when you [set up your transfer](/bigquery/docs/play-transfer#setup-transfer) .
  - The BigQuery Data Transfer Service does not support incremental data transfers during a Google Play transfer. When you specify a date for a data transfer, all of the data that is available for that date is transferred.

## Before you begin

Before you create a Google Play data transfer:

  - Verify that you have completed all actions required to [enable the BigQuery Data Transfer Service](/bigquery/docs/enable-transfer-service) .
  - [Create a BigQuery dataset](/bigquery/docs/datasets) to store the Google Play data.
  - Find your Cloud Storage bucket:
    1.  In the [Google Play console](https://play.google.com/apps/publish/) , click file\_download **Download reports** and select **Reviews** , **Statistics** , or **Financial** .
    
    2.  To copy the ID for your Cloud Storage bucket, click content\_copy **Copy Cloud Storage URI** . Your bucket ID begins with `  gs://  ` . For example, for the reviews report, your ID is similar to the following:
        
        ``` text
        gs://pubsite_prod_rev_01234567890987654321/reviews
        ```
    
    3.  For the Google Play data transfer, you need to copy only the unique ID that comes between `  gs://  ` and `  /reviews  ` :
        
        ``` text
        pubsite_prod_rev_01234567890987654321
        ```
  - If you intend to setup transfer run notifications for Pub/Sub, you must have `  pubsub.topics.setIamPolicy  ` permissions. Pub/Sub permissions are not required if you just set up email notifications. For more information, see [BigQuery Data Transfer Service run notifications](/bigquery/docs/transfer-run-notifications) .

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

### Required Google Play roles

Ensure that you have the following permissions in Google Play:

  - You must have reporting access in the [Google Play console](https://play.google.com/apps/publish/) .
    
    The Google Cloud team does **NOT** have the ability to generate or grant access to Google Play files on your behalf. See [Contact Google Play support](https://support.google.com/googleplay/answer/9789798?&ref_topic=3364260&visit_id=636444821343154346-869320595&rd=1) for help accessing Google Play files.

## Set up a Google Play transfer

Setting up a Google Play data transfer requires a:

  - **Cloud Storage bucket** . Steps for locating your Cloud Storage bucket are described in [Before you begin](/bigquery/docs/play-transfer#before_you_begin) . Your Cloud Storage bucket begins with `  pubsite_prod_rev  ` . For example: `  pubsite_prod_rev_01234567890987654321  ` .
  - **Table suffix** : A user-friendly name for all data sources loading into the same dataset. The suffix is used to prevent separate transfers from writing to the same tables. The table suffix must be unique across all transfers that load data into the same dataset, and the suffix should be short to minimize the length of the resulting table name.

To set up a Google Play data transfer:

### Console

1.  Go to the Data transfers page in the Google Cloud console.

2.  Click add **Create transfer** .

3.  On the **Create Transfer** page:
    
      - In the **Source type** section, for **Source** , choose **Google Play** .
    
      - In the **Transfer config name** section, for **Display name** , enter a name for the data transfer such as `  My Transfer  ` . The transfer name can be any value that lets you identify the transfer if you need to modify it later.
    
      - In the **Schedule options** section:
        
          - For **Repeat frequency** , choose an option for how often to run the data transfer. If you select **Days** , provide a valid time in UTC.
          - If applicable, select either **Start now** or **Start at set time** , and provide a start date and run time.
    
      - In the **Destination settings** section, for **Destination dataset** , choose the dataset that you created to store your data.
    
      - In the **Data source details** section:
        
          - For **Cloud Storage bucket** , enter the ID for your Cloud Storage bucket.
          - For **Table suffix** , enter a suffix such as `  MT  ` (for `  My Transfer  ` ).
    
      - In the **Service Account** menu, select a [service account](/iam/docs/service-account-overview) from the service accounts that are associated with your Google Cloud project. You can associate a service account with your data transfer instead of using your user credentials. For more information about using service accounts with data transfers, see [Use service accounts](/bigquery/docs/use-service-accounts) .
        
          - If you signed in with a [federated identity](/iam/docs/workforce-identity-federation) , then a service account is required to create a data transfer. If you signed in with a [Google Account](/iam/docs/principals-overview#google-account) , then a service account for the transfer is optional.
          - The service account must have the [required permissions](/bigquery/docs/play-transfer#required_permissions) .
    
      - (Optional) In the **Notification options** section:
        
          - Click the toggle to enable email notifications. When you enable this option, the transfer administrator receives an email notification when a transfer run fails.
          - For **Select a Pub/Sub topic** , choose your [topic](/pubsub/docs/overview#types) name or click **Create a topic** . This option configures Pub/Sub run [notifications](/bigquery/docs/transfer-run-notifications) for your transfer.

4.  Click **Save** .

### bq

Enter the `  bq mk  ` command and supply the transfer creation flag — `  --transfer_config  ` . The following flags are also required:

  - `  --target_dataset  `
  - `  --display_name  `
  - `  --params  `
  - `  --data_source  `

<!-- end list -->

``` text
bq mk \
--transfer_config \
--project_id=project_id \
--target_dataset=dataset \
--display_name=name \
--params='parameters' \
--data_source=data_source
--service_account_name=service_account_name
```

Where:

  - project\_id is your project ID. If `  --project_id  ` isn't specified, the default project is used.
  - dataset is the target dataset for the transfer configuration.
  - name is the display name for the transfer configuration. The data transfer name can be any value that lets you identify the transfer if you need to modify it later.
  - parameters contains the parameters for the created transfer configuration in JSON format. For example: `  --params='{"param":"param_value"}'  ` . For Google Play, you must supply the `  bucket  ` and `  table_suffix  ` , parameters. `  bucket  ` is the Cloud Storage bucket that contains your Play report files.
  - data\_source is the data source: `  play  ` .
  - service\_account\_name is the service account name used to authenticate your data transfer. The service account should be owned by the same `  project_id  ` used to create the transfer and it should have all of the [required permissions](#required_permissions) .

**Caution:** You cannot configure notifications using the command-line tool.

For example, the following command creates a Google Play data transfer named `  My Transfer  ` using Cloud Storage bucket `  pubsite_prod_rev_01234567890987654321  ` and target dataset `  mydataset  ` . The data transfer is created in the default project:

``` text
bq mk \
--transfer_config \
--target_dataset=mydataset \
--display_name='My Transfer' \
--params='{"bucket":"pubsite_prod_rev_01234567890987654321","table_suffix":"MT"}' \
--data_source=play
```

The first time you run the command, you will receive a message like the following:

`  [URL omitted] Please copy and paste the above URL into your web browser and follow the instructions to retrieve an authentication code.  `

Follow the instructions in the message and paste the authentication code on the command line.

**Caution:** When you create a Google Play data transfer using the command-line tool, the transfer configuration is set up using the default value for **Schedule** (every 24 hours).

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

// Sample to create a play transfer config.
public class CreatePlayTransfer {

  public static void main(String[] args) throws IOException {
    // TODO(developer): Replace these variables before running the sample.
    final String projectId = "MY_PROJECT_ID";
    String datasetId = "MY_DATASET_ID";
    String bucket = "gs://cloud-sample-data";
    String tableSuffix = "_test";
    Map<String, Value> params = new HashMap<>();
    params.put("bucket", Value.newBuilder().setStringValue(bucket).build());
    params.put("table_suffix", Value.newBuilder().setStringValue(tableSuffix).build());
    TransferConfig transferConfig =
        TransferConfig.newBuilder()
            .setDestinationDatasetId(datasetId)
            .setDisplayName("Your Play Config Name")
            .setDataSourceId("play")
            .setParams(Struct.newBuilder().putAllFields(params).build())
            .build();
    createPlayTransfer(projectId, transferConfig);
  }

  public static void createPlayTransfer(String projectId, TransferConfig transferConfig)
      throws IOException {
    try (DataTransferServiceClient client = DataTransferServiceClient.create()) {
      ProjectName parent = ProjectName.of(projectId);
      CreateTransferConfigRequest request =
          CreateTransferConfigRequest.newBuilder()
              .setParent(parent.toString())
              .setTransferConfig(transferConfig)
              .build();
      TransferConfig config = client.createTransferConfig(request);
      System.out.println("play transfer created successfully :" + config.getName());
    } catch (ApiException ex) {
      System.out.print("play transfer was not created." + ex.toString());
    }
  }
}
```

**Warning:** If you change the schema of a report, all files on that day must have the same schema, or the data transfer for the entire day will fail.

## Troubleshoot Google Play transfer set up

If you are having issues setting up your data transfer, see [Troubleshooting BigQuery Data Transfer Service transfer setup](/bigquery/docs/transfer-troubleshooting) .

## Query your data

When your data is transferred to BigQuery, the data is written to ingestion-time partitioned tables. For more information, see [Introduction to partitioned tables](/bigquery/docs/partitioned-tables) .

If you query your tables directly instead of using the auto-generated views, you must use the `  _PARTITIONTIME  ` pseudocolumn in your query. For more information, see [Querying partitioned tables](/bigquery/docs/querying-partitioned-tables) .

## Pricing

For information on Google Play data transfer pricing, see the [Pricing](https://cloud.google.com/bigquery/pricing#data-transfer-service-pricing) page.

Once data is transferred to BigQuery, standard BigQuery [storage](https://cloud.google.com/bigquery/pricing#storage) and [query](https://cloud.google.com/bigquery/pricing#queries) pricing applies.

## What's next

  - To see how your Google Play reports are transferred to BigQuery, see [Google Play report transformations](/bigquery/docs/play-transformation) .
  - For an overview of BigQuery Data Transfer Service, see [Introduction to BigQuery Data Transfer Service](/bigquery/docs/dts-introduction) .
  - For information on using transfers including getting information about a transfer configuration, listing transfer configurations, and viewing a transfer's run history, see [Working with transfers](/bigquery/docs/working-with-transfers) .
