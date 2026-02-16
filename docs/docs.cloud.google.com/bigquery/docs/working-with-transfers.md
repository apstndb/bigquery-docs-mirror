# Manage transfers

This document shows how to manage existing data transfer configurations.

You can also [manually trigger an existing transfer](#manually_trigger_a_transfer) , also known as starting a *backfill run* .

## View your transfers

View your existing transfer configurations by viewing information about each transfer, listing all existing transfers, and viewing transfer run history or log messages.

### Required roles

To get the permissions that you need to view transfer details, ask your administrator to grant you the [BigQuery User](/iam/docs/roles-permissions/bigquery#bigquery.user) ( `  roles/bigquery.user  ` ) IAM role on the project. For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

Additionally, to view log messages through Google Cloud console, you must have permissions to view Cloud Logging data. The Logs Viewer role ( `  roles/logging.viewer  ` ) gives you read-only access to all features of Logging. For more information about the Identity and Access Management (IAM) permissions and roles that apply to cloud logs data, see the Cloud Logging [access control guide](/logging/docs/access-control) .

For more information about IAM roles in BigQuery Data Transfer Service, see [Access control](/bigquery/docs/access-control) .

### Get transfer details

After you create a transfer, you can get information about the transfer's configuration. The configuration includes the values you supplied when you created the transfer, as well as other important information such as resource names.

To get information about a transfer configuration:

### Console

1.  Go to the **Data transfers** page.

2.  Select the transfer for which you want to get the details.

3.  To see the transfer configuration and the data source details, click **Configuration** on the **Transfer details** page. The following example shows the configuration properties for a Google Ads transfer:

### bq

Enter the `  bq show  ` command and provide the transfer configuration's resource name. The `  --format  ` flag can be used to control the output format.

``` text
bq show \
--format=prettyjson \
--transfer_config resource_name
```

Replace `  resource_name  ` with the transfer's resource name (also referred to as the transfer configuration). If you do not know the transfer's resource name, find the resource name with: [`  bq ls --transfer_config --transfer_location= location  `](#list_transfer_configurations) .

For example, enter the following command to display transfer configuration for `  projects/myproject/locations/us/transferConfigs/1234a123-1234-1a23-1be9-12ab3c456de7  ` .

``` text
bq show \
--format=prettyjson \
--transfer_config projects/myproject/locations/us/transferConfigs/1234a123-1234-1a23-1be9-12ab3c456de7
```

### API

Use the [`  projects.locations.transferConfigs.get  `](/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs/get) method and supply the transfer configuration using the `  name  ` parameter.

### Java

Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Java API reference documentation](/java/docs/reference/google-cloud-bigquery/latest/overview) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` java
import com.google.api.gax.rpc.ApiException;
import com.google.cloud.bigquery.datatransfer.v1.DataTransferServiceClient;
import com.google.cloud.bigquery.datatransfer.v1.GetTransferConfigRequest;
import com.google.cloud.bigquery.datatransfer.v1.TransferConfig;
import java.io.IOException;

// Sample to get config info.
public class GetTransferConfigInfo {

  public static void main(String[] args) throws IOException {
    // TODO(developer): Replace these variables before running the sample.
    String configId = "MY_CONFIG_ID";
    // i.e projects/{project_id}/transferConfigs/{config_id}` or
    // `projects/{project_id}/locations/{location_id}/transferConfigs/{config_id}`
    getTransferConfigInfo(configId);
  }

  public static void getTransferConfigInfo(String configId) throws IOException {
    try (DataTransferServiceClient dataTransferServiceClient = DataTransferServiceClient.create()) {
      GetTransferConfigRequest request =
          GetTransferConfigRequest.newBuilder().setName(configId).build();
      TransferConfig info = dataTransferServiceClient.getTransferConfig(request);
      System.out.print("Config info retrieved successfully." + info.getName() + "\n");
    } catch (ApiException ex) {
      System.out.print("config not found." + ex.toString());
    }
  }
}
```

### List transfer configurations

To list all existing transfer configurations in a project:

### Console

1.  In the Google Cloud console, go to the Data transfers page.

2.  If there are any transfer configurations in the project, a list of the transfer configurations appears on the data transfers list.

### bq

To list all transfer configurations for a project by location, enter the `  bq ls  ` command and supply the `  --transfer_location  ` and `  --transfer_config  ` flags. You can also supply the `  --project_id  ` flag to specify a particular project. If `  --project_id  ` isn't specified, the default project is used. The `  --format  ` flag can be used to control the output format.

To list transfer configurations for particular data sources, supply the `  --filter  ` flag.

To view a particular number of transfer configurations in paginated format, supply the `  --max_results  ` flag to specify the number of transfers. The command returns a page token you supply using the `  --page_token  ` flag to see the next n configurations. There is a limit of 1000 configurations that will be returned if `  --max_results  ` is omitted, and `  --max_results  ` will not accept values greater than 1000. If your project has more than 1000 configurations, use `  --max_results  ` and `  --page_token  ` to iterate through them all.

``` text
bq ls \
--transfer_config \
--transfer_location=location \
--project_id=project_id \
--max_results=integer \
--filter=dataSourceIds:data_sources
```

Replace the following:

  - `  location  ` is the location of the transfer configurations. The [location](/bigquery/docs/dts-introduction#supported_regions) is specified when you create a transfer.
  - `  project_id  ` is your project ID.
  - `  integer  ` is the number of results to show per page.
  - `  data_sources  ` is one or more of the following:
      - `  amazon_s3  ` - [Amazon S3 data transfer](/bigquery/docs/s3-transfer#bq)
      - `  azure_blob_storage  ` - [Azure Blob Storage data transfer](/bigquery/docs/blob-storage-transfer#bq)
      - `  dcm_dt  ` - [Campaign Manager data transfer](/bigquery/docs/doubleclick-campaign-transfer#set_up_a_campaign_manager_transfer)
      - `  google_cloud_storage  ` - [Cloud Storage data transfer](/bigquery/docs/cloud-storage-transfer#set_up_a_cloud_storage_transfer)
      - `  cross_region_copy  ` - [Dataset Copy](/bigquery/docs/copying-datasets)
      - `  dfp_dt  ` - [Google Ad Manager data transfer](/bigquery/docs/doubleclick-publisher-transfer#set_up_a_google_ad_manager_transfer)
      - `  displayvideo  ` - [Display & Video 360 data transfer](/bigquery/docs/display-video-transfer)
      - `  google_ads  ` - [Google Ads data transfer](/bigquery/docs/google-ads-transfer)
      - `  merchant_center  ` - [Google Merchant Center data transfer](/bigquery/docs/merchant-center-transfer-schedule-transfers)
      - `  mysql  ` - [MySQL data transfer](/bigquery/docs/mysql-transfer#set-up-a-mysql-data-transfer)
      - `  play  ` - [Google Play data transfer](/bigquery/docs/play-transfer#setup-transfer)
      - `  scheduled_query  ` - [Scheduled queries data transfer](/bigquery/docs/scheduling-queries)
      - `  search_ads  ` - [Search Ads 360 data transfer](/bigquery/docs/search-ads-transfer)
      - `  youtube_channel  ` - [YouTube Channel data transfer](/bigquery/docs/youtube-channel-transfer#set_up_a_youtube_channel_transfer)
      - `  youtube_content_owner  ` - [YouTube Content Owner data transfer](/bigquery/docs/youtube-content-owner-transfer#set_up_a_youtube_content_owner_transfer)
      - `  redshift  ` - [Amazon Redshift migration](/bigquery/docs/migration/redshift#set-up-transfer)
      - `  on_premises  ` - [Teradata migration](/bigquery/docs/migration/teradata)

Examples:

Enter the following command to display all transfer configurations in the US for your default project. The output is controlled using the `  --format  ` flag.

``` text
bq ls \
--format=prettyjson \
--transfer_config \
--transfer_location=us
```

Enter the following command to display all transfer configurations in the US for project ID `  myproject  ` .

``` text
bq ls \
--transfer_config \
--transfer_location=us \
--project_id=myproject
```

Enter the following command to list the 3 most recent transfer configurations.

``` text
bq ls \
--transfer_config \
--transfer_location=us \
--project_id=myproject \
--max_results=3
```

The command returns a next page token. Copy the page token and supply it in the `  bq ls  ` command to see the next 3 results.

``` text
bq ls \
--transfer_config \
--transfer_location=us \
--project_id=myproject \
--max_results=3 \
--page_token=AB1CdEfg_hIJKL
```

Enter the following command to list Ads and Campaign Manager transfer configurations for project ID `  myproject  ` .

``` text
bq ls \
--transfer_config \
--transfer_location=us \
--project_id=myproject \
--filter=dataSourceIds:dcm_dt,google_ads
```

### API

Use the [`  projects.locations.transferConfigs.list  `](/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs/list) method and supply the project ID using the `  parent  ` parameter.

### Java

Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Java API reference documentation](/java/docs/reference/google-cloud-bigquery/latest/overview) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` java
import com.google.api.gax.rpc.ApiException;
import com.google.cloud.bigquery.datatransfer.v1.DataTransferServiceClient;
import com.google.cloud.bigquery.datatransfer.v1.ListTransferConfigsRequest;
import com.google.cloud.bigquery.datatransfer.v1.ProjectName;
import java.io.IOException;

// Sample to get list of transfer config
public class ListTransferConfigs {

  public static void main(String[] args) throws IOException {
    // TODO(developer): Replace these variables before running the sample.
    final String projectId = "MY_PROJECT_ID";
    listTransferConfigs(projectId);
  }

  public static void listTransferConfigs(String projectId) throws IOException {
    try (DataTransferServiceClient dataTransferServiceClient = DataTransferServiceClient.create()) {
      ProjectName parent = ProjectName.of(projectId);
      ListTransferConfigsRequest request =
          ListTransferConfigsRequest.newBuilder().setParent(parent.toString()).build();
      dataTransferServiceClient
          .listTransferConfigs(request)
          .iterateAll()
          .forEach(config -> System.out.print("Success! Config ID :" + config.getName() + "\n"));
    } catch (ApiException ex) {
      System.out.println("Config list not found due to error." + ex.toString());
    }
  }
}
```

### Python

Before trying this sample, follow the Python setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Python API reference documentation](/python/docs/reference/bigquery/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` python
import google.api_core.exceptions
from google.cloud import bigquery_datatransfer_v1

client = bigquery_datatransfer_v1.DataTransferServiceClient()


def list_transfer_configs(project_id: str, location: str) -> None:
    """Lists transfer configurations in a given project.

    This sample demonstrates how to list all transfer configurations in a project.

    Args:
        project_id: The Google Cloud project ID.
        location: The geographic location of the transfer config, for example "us-central1"
    """

    parent = client.common_location_path(project_id, location)

    try:
        for config in client.list_transfer_configs(parent=parent):
            print(f"Name: {config.name}")
            print(f"Display Name: {config.display_name}")
            print(f"Data source: {config.data_source_id}")
            print(f"Destination dataset: {config.destination_dataset_id}")
            if "time_based_schedule" in config.schedule_options_v2:
                print(
                    f"Schedule: {config.schedule_options_v2.time_based_schedule.schedule}"
                )
            else:
                print("Schedule: None")
            print("---")
    except google.api_core.exceptions.NotFound:
        print(
            f"Error: Project '{project_id}' not found or contains no transfer configs."
        )
    except google.api_core.exceptions.PermissionDenied:
        print(
            f"Error: Permission denied for project '{project_id}'. Please ensure you have the correct permissions."
        )
```

### View transfer run history

As your scheduled transfers are run, a run history is kept for each transfer configuration that includes successful transfer runs and transfer runs that fail. Transfer runs more than 90 days old are automatically deleted from the run history.

To view the run history for a transfer configuration:

### Console

1.  In the Google Cloud console, go to the Data transfers page.

2.  Click on the transfer in the data transfers list.

3.  You will be on the **RUN HISTORY** page for the selected transfer.

### bq

To list transfer runs for a particular transfer configuration, enter the `  bq ls  ` command and supply the `  --transfer_run  ` flag. You can also supply the `  --project_id  ` flag to specify a particular project. If resource\_name doesn't contain project information, the `  --project_id  ` value is used. If `  --project_id  ` isn't specified, the default project is used. The `  --format  ` flag can be used to control the output format.

To view a particular number of transfer runs, supply the `  --max_results  ` flag. The command returns a page token you supply using the `  --page_token  ` flag to see the next n configurations.

To list transfer runs based on run state, supply the `  --filter  ` flag.

``` text
bq ls \
--transfer_run \
--max_results=integer \
--transfer_location=location \
--project_id=project_id \
--filter=states:state, ... \
resource_name
```

Replace the following:

  - `  integer  ` is the number of results to return.
  - `  location  ` is the location of the transfer configurations. The [location](/bigquery/docs/dts-introduction#supported_regions) is specified when you create a transfer.
  - `  project_id  ` is your project ID.
  - `  state, ...  ` is one of the following or a comma-separated list:
      - `  SUCCEEDED  `
      - `  FAILED  `
      - `  PENDING  `
      - `  RUNNING  `
      - `  CANCELLED  `
  - `  resource_name  ` is the transfer's resource name (also referred to as the transfer configuration). If you do not know the transfer's resource name, find the resource name with: [`  bq ls --transfer_config --transfer_location= location  `](#list_transfer_configurations) .

Examples:

Enter the following command to display the 3 latest runs for transfer configuration `  projects/myproject/locations/us/transferConfigs/1234a123-1234-1a23-1be9-12ab3c456de7  ` . The output is controlled using the `  --format  ` flag.

``` text
bq ls \
--format=prettyjson \
--transfer_run \
--max_results=3 \
--transfer_location=us \
projects/myproject/locations/us/transferConfigs/1234a123-1234-1a23-1be9-12ab3c456de7
```

The command returns a next page token. Copy the page token and supply it in the `  bq ls  ` command to see the next 3 results.

``` text
bq ls \
--format=prettyjson \
--transfer_run \
--max_results=3 \
--page_token=AB1CdEfg_hIJKL \
--transfer_location=us \
projects/myproject/locations/us/transferConfigs/1234a123-1234-1a23-1be9-12ab3c456de7
```

Enter the following command to display all failed runs for transfer configuration `  projects/myproject/locations/us/transferConfigs/1234a123-1234-1a23-1be9-12ab3c456de7  ` .

``` text
bq ls \
--format=prettyjson \
--transfer_run \
--filter=states:FAILED \
--transfer_location=us \
projects/myproject/locations/us/transferConfigs/1234a123-1234-1a23-1be9-12ab3c456de7
```

### API

Use the [`  projects.locations.transferConfigs.runs.list  `](/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.runs/list) method and specify the project ID using the `  parent  ` parameter.

### Java

Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Java API reference documentation](/java/docs/reference/google-cloud-bigquery/latest/overview) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` java
import com.google.api.gax.rpc.ApiException;
import com.google.cloud.bigquery.datatransfer.v1.DataTransferServiceClient;
import com.google.cloud.bigquery.datatransfer.v1.ListTransferRunsRequest;
import java.io.IOException;

// Sample to get run history from transfer config.
public class RunHistory {

  public static void main(String[] args) throws IOException {
    // TODO(developer): Replace these variables before running the sample.
    String configId = "MY_CONFIG_ID";
    // i.e projects/{project_id}/transferConfigs/{config_id}` or
    // `projects/{project_id}/locations/{location_id}/transferConfigs/{config_id}`
    runHistory(configId);
  }

  public static void runHistory(String configId) throws IOException {
    try (DataTransferServiceClient dataTransferServiceClient = DataTransferServiceClient.create()) {
      ListTransferRunsRequest request =
          ListTransferRunsRequest.newBuilder().setParent(configId).build();
      dataTransferServiceClient
          .listTransferRuns(request)
          .iterateAll()
          .forEach(run -> System.out.print("Success! Run ID :" + run.getName() + "\n"));
    } catch (ApiException ex) {
      System.out.println("Run history not found due to error." + ex.toString());
    }
  }
}
```

### View transfer run details and log messages

When a transfer run appears in the run history, you can view the run details including log messages, warnings and errors, the run name, and the start and end time.

To view transfer run details:

### Console

1.  In the Google Cloud console, go to the Data transfers page.

2.  Click on the transfer in the data transfers list.

3.  You will be on the **RUN HISTORY** page for the selected transfer.

4.  Click on an individual run of the transfer, and the **Run details** panel will open for that run of the transfer.

5.  In the **Run details** , note any error messages. This information is needed if you contact Cloud Customer Care. The run details also include log messages and warnings.

### bq

To view transfer run details, enter the `  bq show  ` command and provide the transfer run's Run Name using the `  --transfer_run  ` flag. The `  --format  ` flag can be used to control the output format.

``` text
bq show \
--format=prettyjson \
--transfer_run run_name
```

Replace `  run_name  ` with the transfer run's Run Name. You can retrieve the Run Name by using the [`  bq ls  `](#view_the_run_history) command.

Example:

Enter the following command to display details for transfer run `  projects/myproject/locations/us/transferConfigs/1234a123-1234-1a23-1be9-12ab3c456de7/runs/1a2b345c-0000-1234-5a67-89de1f12345g  ` .

``` text
bq show \
--format=prettyjson \
--transfer_run \
projects/myproject/locations/us/transferConfigs/1234a123-1234-1a23-1be9-12ab3c456de7/runs/1a2b345c-0000-1234-5a67-89de1f12345g
```

To view transfer log messages for a transfer run, enter the `  bq ls  ` command with the `  --transfer_log  ` flag. You can filter log messages by type using the `  --message_type  ` flag.

To view a particular number of log messages, supply the `  --max_results  ` flag. The command returns a page token you supply using the `  --page_token  ` flag to see the next n messages.

``` text
bq ls \
--transfer_log \
--max_results=integer \
--message_type=messageTypes:message_type \
run_name
```

Replace the following:

  - `  integer  ` is the number of log messages to return.
  - `  message_type  ` is the type of log message to view (a single value or a comma-separated list):
      - `  INFO  `
      - `  WARNING  `
      - `  ERROR  `
  - `  run_name  ` is the transfer run's Run Name. You can retrieve the Run Name using the [`  bq ls  `](#view_the_run_history) command.

Examples:

Enter the following command to view the first 2 log messages for transfer run `  projects/myproject/locations/us/transferConfigs/1234a123-1234-1a23-1be9-12ab3c456de7/runs/1a2b345c-0000-1234-5a67-89de1f12345g  ` .

``` text
bq ls \
--transfer_log \
--max_results=2 \
projects/myproject/locations/us/transferConfigs/1234a123-1234-1a23-1be9-12ab3c456de7/runs/1a2b345c-0000-1234-5a67-89de1f12345g
```

The command returns a next page token. Copy the page token and supply it in the `  bq ls  ` command to see the next 2 results.

``` text
bq ls \
--transfer_log \
--max_results=2 \
--page_token=AB1CdEfg_hIJKL \
projects/myproject/locations/us/transferConfigs/1234a123-1234-1a23-1be9-12ab3c456de7/runs/1a2b345c-0000-1234-5a67-89de1f12345g
```

Enter the following command to view only error messages for transfer run `  projects/myproject/locations/us/transferConfigs/1234a123-1234-1a23-1be9-12ab3c456de7/runs/1a2b345c-0000-1234-5a67-89de1f12345g  ` .

``` text
bq ls \
--transfer_log \
--message_type=messageTypes:ERROR \
projects/myproject/locations/us/transferConfigs/1234a123-1234-1a23-1be9-12ab3c456de7/runs/1a2b345c-0000-1234-5a67-89de1f12345g
```

### API

Use the [`  projects.transferConfigs.runs.transferLogs.list  `](/bigquery/docs/reference/datatransfer/rest/v1/projects.transferConfigs.runs.transferLogs/list) method and supply the transfer run's Run Name using the `  parent  ` parameter.

### Java

Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Java API reference documentation](/java/docs/reference/google-cloud-bigquery/latest/overview) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` java
import com.google.api.gax.rpc.ApiException;
import com.google.cloud.bigquery.datatransfer.v1.DataTransferServiceClient;
import com.google.cloud.bigquery.datatransfer.v1.GetTransferRunRequest;
import com.google.cloud.bigquery.datatransfer.v1.TransferRun;
import java.io.IOException;

// Sample to get run details from transfer config.
public class RunDetails {

  public static void main(String[] args) throws IOException {
    // TODO(developer): Replace these variables before running the sample.
    // runId examples:
    // `projects/{project_id}/transferConfigs/{config_id}/runs/{run_id}` or
    // `projects/{project_id}/locations/{location_id}/transferConfigs/{config_id}/runs/{run_id}`
    String runId = "MY_RUN_ID";
    runDetails(runId);
  }

  public static void runDetails(String runId) throws IOException {
    try (DataTransferServiceClient dataTransferServiceClient = DataTransferServiceClient.create()) {
      GetTransferRunRequest request = GetTransferRunRequest.newBuilder().setName(runId).build();
      TransferRun run = dataTransferServiceClient.getTransferRun(request);
      System.out.print("Run details retrieved successfully :" + run.getName() + "\n");
    } catch (ApiException ex) {
      System.out.print("Run details not found." + ex.toString());
    }
  }
}
```

## Modify your transfers

You can modify existing transfers by editing information on the transfer configuration, updating a user's credentials attached to a transfer configuration, and disabling or deleting a transfer.

### Required roles

To get the permissions that you need to modify transfers, ask your administrator to grant you the [BigQuery Admin](/iam/docs/roles-permissions/bigquery#bigquery.admin) ( `  roles/bigquery.admin  ` ) IAM role on the project. For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

### Update a transfer

After you create a transfer configuration, you can edit the following fields:

  - Destination dataset
  - Display name
  - Any of the parameters specified for the specific transfer type
  - Run notification settings
  - Service account

You cannot edit the source of a transfer once a transfer is created.

To update a transfer:

### Console

1.  In the Google Cloud console, go to the Data transfers page.

2.  Click on the transfer in the data transfers list.

3.  Click **EDIT** to update the transfer configuration.

### bq

Enter the [`  bq update  ` command](/bigquery/docs/reference/bq-cli-reference#bq_update) , provide the transfer configuration's resource name using the `  --transfer_config  ` flag, and supply the `  --display_name  ` , `  --params  ` , `  --refresh_window_days  ` , `  --schedule  ` , or `  --target_dataset  ` flags. You can optionally supply a `  --destination_kms_key  ` flag for [scheduled queries](/bigquery/docs/scheduling-queries) or [Cloud Storage](/bigquery/docs/cloud-storage-transfer-overview) transfers.

``` text
bq update \
--display_name='NAME' \
--params='PARAMETERS' \
--refresh_window_days=INTEGER \
--schedule='SCHEDULE'
--target_dataset=DATASET_ID \
--destination_kms_key="DESTINATION_KEY" \
--transfer_config \
--service_account_name=SERVICE_ACCOUNT \
RESOURCE_NAME
```

Replace the following:

  - `  NAME  ` : the display name for the transfer configuration.
  - `  PARAMETERS  ` : the parameters for the transfer configuration in JSON format. For example: `  --params='{"param1":"param_value1"}'  ` . For information about supported parameters, see the transfer guide for your data source.
  - `  INTEGER  ` : a value from 0 to 30. For information on setting the refresh window, see the documentation for your transfer type.
  - `  SCHEDULE  ` : a recurring schedule, such as `  --schedule="every 3 hours"  ` . For a description of the `  schedule  ` syntax, see [Formatting the `  schedule  `](/appengine/docs/flexible/python/scheduling-jobs-with-cron-yaml#formatting_the_schedule) .
  - DATASET\_ID : the target dataset for the transfer configuration.
  - DESTINATION\_KEY : the [Cloud KMS key resource ID](/bigquery/docs/customer-managed-encryption#key_resource_id) —for example, `  projects/project_name/locations/us/keyRings/key_ring_name/cryptoKeys/key_name  ` . CMEK is only available for [scheduled queries](/bigquery/docs/scheduling-queries) or [Cloud Storage](/bigquery/docs/cloud-storage-transfer-overview) transfers.
  - SERVICE\_ACCOUNT : specify a service account to use with this transfer.
  - RESOURCE\_NAME : the transfer's resource name (also referred to as the transfer configuration). If you don't know the transfer's resource name, find the resource name with: [`  bq ls --transfer_config --transfer_location= location  `](#list_transfer_configurations) .

**Note:** You cannot update notification settings using the bq tool.

Examples:

The following command updates the display name, target dataset, refresh window, and parameters for Google Ads transfer `  projects/myproject/locations/us/transferConfigs/1234a123-1234-1a23-1be9-12ab3c456de7  ` :

``` text
bq update \
--display_name='My changed transfer' \
--params='{"customer_id":"123-123-5678"}' \
--refresh_window_days=3 \
--target_dataset=mydataset2 \
--transfer_config \
 projects/myproject/locations/us/transferConfigs/1234a123-1234-1a23-1be9-12ab3c456de7
```

The following command updates the parameters and schedule for Scheduled Query transfer `  projects/myproject/locations/us/transferConfigs/5678z567-5678-5z67-5yx9-56zy3c866vw9  ` :

``` text
bq update \
--params='{"destination_table_name_template":"test", "write_disposition":"APPEND"}' \
--schedule="every 24 hours" \
--transfer_config \
projects/myproject/locations/us/transferConfigs/5678z567-5678-5z67-5yx9-56zy3c866vw9
```

### API

Use the [`  projects.transferConfigs.patch  `](/bigquery/docs/reference/datatransfer/rest/v1/projects.transferConfigs/patch) method and supply the transfer's resource name using the `  transferConfig.name  ` parameter. If you do not know the transfer's resource name, find the resource name with: [`  bq ls --transfer_config --transfer_location= location  `](#list_transfer_configurations) . You can also call the following method and supply the project ID using the `  parent  ` parameter to list all transfers: [`  projects.locations.transferConfigs.list  `](/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs/list) .

### Java

Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Java API reference documentation](/java/docs/reference/google-cloud-bigquery/latest/overview) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` java
import com.google.api.gax.rpc.ApiException;
import com.google.cloud.bigquery.datatransfer.v1.DataTransferServiceClient;
import com.google.cloud.bigquery.datatransfer.v1.TransferConfig;
import com.google.cloud.bigquery.datatransfer.v1.UpdateTransferConfigRequest;
import com.google.protobuf.FieldMask;
import com.google.protobuf.util.FieldMaskUtil;
import java.io.IOException;

// Sample to update transfer config.
public class UpdateTransferConfig {

  public static void main(String[] args) throws IOException {
    // TODO(developer): Replace these variables before running the sample.
    String configId = "MY_CONFIG_ID";
    TransferConfig transferConfig =
        TransferConfig.newBuilder()
            .setName(configId)
            .setDisplayName("UPDATED_DISPLAY_NAME")
            .build();
    FieldMask updateMask = FieldMaskUtil.fromString("display_name");
    updateTransferConfig(transferConfig, updateMask);
  }

  public static void updateTransferConfig(TransferConfig transferConfig, FieldMask updateMask)
      throws IOException {
    try (DataTransferServiceClient dataTransferServiceClient = DataTransferServiceClient.create()) {
      UpdateTransferConfigRequest request =
          UpdateTransferConfigRequest.newBuilder()
              .setTransferConfig(transferConfig)
              .setUpdateMask(updateMask)
              .build();
      TransferConfig updateConfig = dataTransferServiceClient.updateTransferConfig(request);
      System.out.println("Transfer config updated successfully :" + updateConfig.getDisplayName());
    } catch (ApiException ex) {
      System.out.print("Transfer config was not updated." + ex.toString());
    }
  }
}
```

### Python

Before trying this sample, follow the Python setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Python API reference documentation](/python/docs/reference/bigquery/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` python
import google.api_core.exceptions
from google.cloud import bigquery_datatransfer_v1
from google.protobuf import field_mask_pb2


client = bigquery_datatransfer_v1.DataTransferServiceClient()


def update_transfer_config(
    project_id: str,
    location: str,
    transfer_config_id: str,
) -> None:
    """Updates a data transfer configuration.

    This sample shows how to update the display name for a transfer
    configuration.

    Args:
        project_id: The Google Cloud project ID.
        location: The geographic location of the transfer config, for example "us-central1"
        transfer_config_id: The transfer configuration ID
    """
    transfer_config_name = client.transfer_config_path(
        project=f"{project_id}/locations/{location}",
        transfer_config=transfer_config_id,
    )

    transfer_config = bigquery_datatransfer_v1.types.TransferConfig(
        name=transfer_config_name,
        display_name="My New Transfer Config display name",
    )
    update_mask = field_mask_pb2.FieldMask(paths=["display_name"])

    try:
        response = client.update_transfer_config(
            transfer_config=transfer_config,
            update_mask=update_mask,
        )

        print(f"Updated transfer config: {response.name}")
        print(f"New display name: {response.display_name}")
    except google.api_core.exceptions.NotFound:
        print(f"Error: Transfer config '{transfer_config_name}' not found.")
```

### Update credentials

A transfer uses the credentials of the user that created it. If you need to change the user attached to a transfer configuration, you can update the transfer's credentials. This is useful if the user who created the transfer is no longer with your organization.

To update the credentials for a transfer:

### Console

1.  In the Google Cloud console, sign in as the user you want to transfer ownership to.

2.  Navigate to the Data transfers page.

3.  Click the transfer in the data transfers list.

4.  Click **MORE** menu, and then select **Refresh credentials** .

5.  Click **Allow** to give the BigQuery Data Transfer Service permission to view your reporting data and to access and manage the data in BigQuery.

### bq

Enter the `  bq update  ` command, provide the transfer configuration's resource name using the `  --transfer_config  ` flag, and supply the `  --update_credentials  ` flag.

``` text
bq update \
--update_credentials=boolean \
--transfer_config \
resource_name
```

Replace the following:

  - `  boolean  ` is a boolean value indicating whether the credentials should be updated for the transfer configuration.
  - `  resource_name  ` is the transfer's resource name (also referred to as the transfer configuration). If you do not know the transfer's resource name, find the resource name with: [`  bq ls --transfer_config --transfer_location= location  `](#list_transfer_configurations) .

Examples:

Enter the following command to update the credentials for Google Ads transfer `  projects/myproject/locations/us/transferConfigs/1234a123-1234-1a23-1be9-12ab3c456de7  ` .

``` text
bq update \
--update_credentials=true \
--transfer_config \
projects/myproject/locations/us/transferConfigs/1234a123-1234-1a23-1be9-12ab3c456de7
```

### API

Use the [`  projects.transferConfigs.patch  `](/bigquery/docs/reference/datatransfer/rest/v1/projects.transferConfigs/patch) method and supply the `  authorizationCode  ` and `  updateMask  ` parameters.

### Java

Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Java API reference documentation](/java/docs/reference/google-cloud-bigquery/latest/overview) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` java
import com.google.api.gax.rpc.ApiException;
import com.google.cloud.bigquery.datatransfer.v1.DataTransferServiceClient;
import com.google.cloud.bigquery.datatransfer.v1.TransferConfig;
import com.google.cloud.bigquery.datatransfer.v1.UpdateTransferConfigRequest;
import com.google.protobuf.FieldMask;
import com.google.protobuf.util.FieldMaskUtil;
import java.io.IOException;

// Sample to update credentials in transfer config.
public class UpdateCredentials {

  public static void main(String[] args) throws IOException {
    // TODO(developer): Replace these variables before running the sample.
    String configId = "MY_CONFIG_ID";
    String serviceAccount = "MY_SERVICE_ACCOUNT";
    TransferConfig transferConfig = TransferConfig.newBuilder().setName(configId).build();
    FieldMask updateMask = FieldMaskUtil.fromString("service_account_name");
    updateCredentials(transferConfig, serviceAccount, updateMask);
  }

  public static void updateCredentials(
      TransferConfig transferConfig, String serviceAccount, FieldMask updateMask)
      throws IOException {
    try (DataTransferServiceClient dataTransferServiceClient = DataTransferServiceClient.create()) {
      UpdateTransferConfigRequest request =
          UpdateTransferConfigRequest.newBuilder()
              .setTransferConfig(transferConfig)
              .setUpdateMask(updateMask)
              .setServiceAccountName(serviceAccount)
              .build();
      dataTransferServiceClient.updateTransferConfig(request);
      System.out.println("Credentials updated successfully");
    } catch (ApiException ex) {
      System.out.print("Credentials was not updated." + ex.toString());
    }
  }
}
```

### Python

Before trying this sample, follow the Python setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Python API reference documentation](/python/docs/reference/bigquery/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` python
from google.cloud import bigquery_datatransfer
from google.protobuf import field_mask_pb2

transfer_client = bigquery_datatransfer.DataTransferServiceClient()

service_account_name = "abcdef-test-sa@abcdef-test.iam.gserviceaccount.com"
transfer_config_name = "projects/1234/locations/us/transferConfigs/abcd"

transfer_config = bigquery_datatransfer.TransferConfig(name=transfer_config_name)

transfer_config = transfer_client.update_transfer_config(
    {
        "transfer_config": transfer_config,
        "update_mask": field_mask_pb2.FieldMask(paths=["service_account_name"]),
        "service_account_name": service_account_name,
    }
)

print("Updated config: '{}'".format(transfer_config.name))
```

### Disable a transfer

When you disable a transfer, disabled is added to the transfer name. When the transfer is disabled, no new transfer runs are scheduled, and no new backfills are allowed. Any transfer runs in progress are completed.

Disabling a transfer does **not** remove any data already transferred to BigQuery. Data previously transferred incurs standard BigQuery [storage costs](https://cloud.google.com/bigquery/pricing#storage) until you [delete the dataset](/bigquery/docs/managing-datasets#delete_a_dataset) or [delete the tables](/bigquery/docs/managing-tables#deleting_tables) .

To disable a transfer:

### Console

1.  In the Google Cloud console, go to the BigQuery page.

2.  Click **Transfers** .

3.  On the **Transfers** page, click on the transfer in the list that you want to disable.

4.  Click on **DISABLE** . To re-enable the transfer, click on **ENABLE** .

### bq

Disabling a transfer is not supported by the CLI.

### API

Use the [`  projects.locations.transferConfigs.patch  `](/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs/patch) method and set `  disabled  ` to `  true  ` in the `  projects.locations.transferConfig  ` resource.

### Java

Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Java API reference documentation](/java/docs/reference/google-cloud-bigquery/latest/overview) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` java
import com.google.api.gax.rpc.ApiException;
import com.google.cloud.bigquery.datatransfer.v1.DataTransferServiceClient;
import com.google.cloud.bigquery.datatransfer.v1.TransferConfig;
import com.google.cloud.bigquery.datatransfer.v1.UpdateTransferConfigRequest;
import com.google.protobuf.FieldMask;
import com.google.protobuf.util.FieldMaskUtil;
import java.io.IOException;

// Sample to disable transfer config.
public class DisableTransferConfig {

  public static void main(String[] args) throws IOException {
    // TODO(developer): Replace these variables before running the sample.
    String configId = "MY_CONFIG_ID";
    TransferConfig transferConfig =
        TransferConfig.newBuilder().setName(configId).setDisabled(true).build();
    FieldMask updateMask = FieldMaskUtil.fromString("disabled");
    disableTransferConfig(transferConfig, updateMask);
  }

  public static void disableTransferConfig(TransferConfig transferConfig, FieldMask updateMask)
      throws IOException {
    try (DataTransferServiceClient dataTransferServiceClient = DataTransferServiceClient.create()) {
      UpdateTransferConfigRequest request =
          UpdateTransferConfigRequest.newBuilder()
              .setTransferConfig(transferConfig)
              .setUpdateMask(updateMask)
              .build();
      TransferConfig updateConfig = dataTransferServiceClient.updateTransferConfig(request);
      System.out.println("Transfer config disabled successfully :" + updateConfig.getDisplayName());
    } catch (ApiException ex) {
      System.out.print("Transfer config was not disabled." + ex.toString());
    }
  }
}
```

To re-enable the transfer:

Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Java API reference documentation](/java/docs/reference/google-cloud-bigquery/latest/overview) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` java
/*
 * Copyright 2020 Google LLC
 *
 * Licensed under the Apache License, Version 2.0 (the "License");
 * you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 * http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 */

package com.example.bigquerydatatransfer;

import com.google.api.gax.rpc.ApiException;
import com.google.cloud.bigquery.datatransfer.v1.DataTransferServiceClient;
import com.google.cloud.bigquery.datatransfer.v1.TransferConfig;
import com.google.cloud.bigquery.datatransfer.v1.UpdateTransferConfigRequest;
import com.google.protobuf.FieldMask;
import com.google.protobuf.util.FieldMaskUtil;
import java.io.IOException;

// Sample to disable transfer config.
public class DisableTransferConfig {

  public static void main(String[] args) throws IOException {
    // TODO(developer): Replace these variables before running the sample.
    String configId = "MY_CONFIG_ID";
    TransferConfig transferConfig =
        TransferConfig.newBuilder().setName(configId).setDisabled(true).build();
    FieldMask updateMask = FieldMaskUtil.fromString("disabled");
    disableTransferConfig(transferConfig, updateMask);
  }

  public static void disableTransferConfig(TransferConfig transferConfig, FieldMask updateMask)
      throws IOException {
    try (DataTransferServiceClient dataTransferServiceClient = DataTransferServiceClient.create()) {
      UpdateTransferConfigRequest request =
          UpdateTransferConfigRequest.newBuilder()
              .setTransferConfig(transferConfig)
              .setUpdateMask(updateMask)
              .build();
      TransferConfig updateConfig = dataTransferServiceClient.updateTransferConfig(request);
      System.out.println("Transfer config disabled successfully :" + updateConfig.getDisplayName());
    } catch (ApiException ex) {
      System.out.print("Transfer config was not disabled." + ex.toString());
    }
  }
}
```

### Delete a transfer

When a transfer is deleted, no new transfer runs are scheduled. Any transfer runs in progress are stopped.

Deleting a transfer does **not** remove any data already transferred to BigQuery. Data previously transferred incurs standard BigQuery [storage costs](https://cloud.google.com/bigquery/pricing#storage) until you [delete the dataset](/bigquery/docs/managing-datasets#delete-datasets) or [delete the tables](/bigquery/docs/managing-tables#deleting_tables) .

To delete a transfer:

### Console

1.  In the Google Cloud console, go to the BigQuery page.

2.  Click **Transfers** .

3.  On the **Transfers** page, click on the transfer in the list that you want to delete.

4.  Click on **DELETE** . As a safety measure you will need to type the word "delete" into a box to confirm your intention.
    
    **Caution:** The delete operation cannot be undone.

### bq

Enter the `  bq rm  ` command and provide the transfer configuration's resource name. You can use the `  -f  ` flag to delete a transfer config without confirmation.

``` text
bq rm \
-f \
--transfer_config \
resource_name
```

Where:

  - resource\_name is the transfer's Resource Name which is also referred to as the transfer configuration). If you do not know the transfer's Resource Name, issue the [`  bq ls --transfer_config --transfer_location= location  `](#listing_transfer_configurations) command to list all transfers.

For example, enter the following command to delete transfer configuration `  projects/myproject/locations/us/transferConfigs/1234a123-1234-1a23-1be9-12ab3c456de7  ` .

``` text
bq rm \
--transfer_config \
projects/myproject/locations/us/transferConfigs/1234a123-1234-1a23-1be9-12ab3c456de7
```

### API

Use the [`  projects.locations.transferConfigs.delete  `](/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs/delete) method and supply the resource you're deleting using the `  name  ` parameter.

### Java

Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Java API reference documentation](/java/docs/reference/google-cloud-bigquery/latest/overview) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` java
import com.google.api.gax.rpc.ApiException;
import com.google.cloud.bigquery.datatransfer.v1.DataTransferServiceClient;
import com.google.cloud.bigquery.datatransfer.v1.DeleteTransferConfigRequest;
import java.io.IOException;

// Sample to delete a transfer config
public class DeleteTransferConfig {

  public static void main(String[] args) throws IOException {
    // TODO(developer): Replace these variables before running the sample.
    // i.e projects/{project_id}/transferConfigs/{config_id}` or
    // `projects/{project_id}/locations/{location_id}/transferConfigs/{config_id}`
    String configId = "MY_CONFIG_ID";
    deleteTransferConfig(configId);
  }

  public static void deleteTransferConfig(String configId) throws IOException {
    try (DataTransferServiceClient dataTransferServiceClient = DataTransferServiceClient.create()) {
      DeleteTransferConfigRequest request =
          DeleteTransferConfigRequest.newBuilder().setName(configId).build();
      dataTransferServiceClient.deleteTransferConfig(request);
      System.out.println("Transfer config deleted successfully");
    } catch (ApiException ex) {
      System.out.println("Transfer config was not deleted." + ex.toString());
    }
  }
}
```

### Python

Before trying this sample, follow the Python setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Python API reference documentation](/python/docs/reference/bigquery/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` python
import google.api_core.exceptions
from google.cloud import bigquery_datatransfer_v1

client = bigquery_datatransfer_v1.DataTransferServiceClient()


def delete_transfer_config(
    project_id: str, location: str, transfer_config_id: str
) -> None:
    """Deletes a data transfer configuration, including any associated transfer runs and logs.

    Args:
        project_id: The Google Cloud project ID.
        location: The geographic location of the transfer configuration, for example, "us-central1".
        transfer_config_id: The transfer configuration ID, for example, "1234a-5678-90b1-2c3d-4e5f67890g12".
    """

    name = client.transfer_config_path(
        project=f"{project_id}/locations/{location}",
        transfer_config=transfer_config_id,
    )
    request = bigquery_datatransfer_v1.DeleteTransferConfigRequest(name=name)

    try:
        client.delete_transfer_config(request=request)
        print(f"Deleted transfer config {name}")
    except google.api_core.exceptions.NotFound:
        print(f"Error: Transfer config '{name}' not found.")
```

When you delete a data transfer with network attachments, it can take a few days before you can delete the network attachments associated with that data transfer. For more information, see [General issues](/bigquery/docs/transfer-troubleshooting#general_issues) .

## Manually trigger a transfer

You can manually trigger a transfer, also called a *backfill run* , to load additional data files outside of your automatically scheduled transfers. With data sources that support runtime parameters, you can also manually trigger a transfer by specifying a date or a time range to load past data from.

You can manually initiate data backfills at any time. In addition to source limits, the BigQuery Data Transfer Service supports a maximum of 180 days per backfill request. Simultaneous backfill requests are not supported.

**Caution:** When backfilling large date ranges, break your backfill requests into **180 day** chunks, and wait for the previous backfill request to finish before creating another one.

For information on how much data is available for backfill, see the transfer guide for your data source.

### Required roles

To get the permissions that you need to modify transfers, ask your administrator to grant you the [BigQuery Admin](/iam/docs/roles-permissions/bigquery#bigquery.admin) ( `  roles/bigquery.admin  ` ) IAM role on the project. For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

### Manually trigger a transfer or backfill

You can manually trigger a transfer or backfill run with the following methods:

  - Select your transfer run using the Google Cloud console, then clicking **Run transfer now** or **Schedule backfill** .
  - Use the `  bq mk –transfer run  ` command using the `  bq  ` command-line tool
  - Call the `  projects.locations.transferConfigs.startManualRuns method  ` API method

For detailed instructions about each method, select the corresponding tab:

### Console

1.  In the Google Cloud console, go to the Data transfers page.

2.  Select your transfer from the list.

3.  Click **Run transfer now** or **Schedule backfill** . Only one option is available depending on the type of transfer configuration.
    
      - If you clicked **Run transfer now** , select **Run one time transfer** or **Run for specific date** as applicable. If you selected **Run for specific date** , select a specific date and time:
    
      - If you clicked **Schedule backfill** , select **Run one time transfer** or **Run for a date range** as applicable. If you selected **Run for a date range** , select a start and end date and time:

4.  Click **OK** .

### bq

To manually start a transfer run, enter the `  bq mk  ` command with the `  --transfer_run  ` flag:

``` text
bq mk \
--transfer_run \
--run_time='RUN_TIME' \
RESOURCE_NAME
```

Replace the following:

  - `  RUN_TIME  ` is a timestamp that specifies the date of a past transfer. Use timestamps that end in Z or contain a valid time zone offset—for example, `  2022-08-19T12:11:35.00Z  ` or `  2022-05-25T00:00:00+00:00  ` .
      - If your transfer does not have a runtime parameter, or you just want to trigger a transfer now without specifying a past transfer, input your current time in this field.
  - `  RESOURCE_NAME  ` is the resource name listed on your transfer configuration—for example, `  projects/myproject/locations/us/transferConfigs/1234a123-1234-1a23-1be9-12ab3c456de7  ` .
      - To find the resource name of a transfer configuration, see [Get transfer details](/bigquery/docs/working-with-transfers#get_transfer_details) .
      - The resource name uses the [Relative resource name](/apis/design/resource_names#relative_resource_name) format.

To manually start a transfer run for a range of dates, enter the `  bq mk  ` command with the `  --transfer_run  ` flag along with a date range:

``` text
bq mk \
--transfer_run \
--start_time='START_TIME' \
--end_time='END_TIME' \
RESOURCE_NAME
```

Replace the following:

  - `  START_TIME  ` and `  END_TIME  ` are timestamps that end in Z or contain a valid time zone offset. These values specifies the time range containing the previous transfer runs that you want to backfill from—for example, `  2022-08-19T12:11:35.00Z  ` or `  2022-05-25T00:00:00+00:00  `
  - `  RESOURCE_NAME  ` is the resource name listed on your transfer configuration—for example, `  projects/myproject/locations/us/transferConfigs/1234a123-1234-1a23-1be9-12ab3c456de7  `
      - To find the resource name of a transfer configuration, see [Get transfer details](/bigquery/docs/working-with-transfers#get_transfer_details) .
      - The resource name uses the [Relative resource name](/apis/design/resource_names#relative_resource_name) format.

### API

To manually start a transfer run, use the [`  projects.locations.transferConfigs.startManualRuns  `](/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs/startManualRuns) method and provide the transfer configuration resource name using the parent parameter. To find the resource name of a transfer configuration, see [Get transfer details](/bigquery/docs/working-with-transfers#get_transfer_details)

``` text
  "requestedRunTime": "RUN_TIME"
```

Replace the following:

  - `  RUN_TIME  ` is a timestamp that specifies the date of a past transfer. Use timestamps that end in Z or contain a valid time zone offset—for example, `  2022-08-19T12:11:35.00Z  ` or `  2022-05-25T00:00:00+00:00  ` .
      - If your transfer does not have a runtime parameter, or you just want to trigger a transfer now without specifying a past transfer, input your current time in this field.

To manually start a transfer run for a range of dates, provide a date range:

``` text
"requestedTimeRange": {
  "startTime": "START_TIME",
  "endTime": "END_TIME"
}
```

Replace the following:

  - `  START_TIME  ` and `  END_TIME  ` are timestamps that end in Z or contain a valid time zone offset. These values specifies the time range containing the previous transfer runs that you want to backfill from—for example, `  2022-08-19T12:11:35.00Z  ` or `  2022-05-25T00:00:00+00:00  `

### Java

Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Java API reference documentation](/java/docs/reference/google-cloud-bigquery/latest/overview) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` java
import com.google.api.gax.rpc.ApiException;
import com.google.cloud.bigquery.datatransfer.v1.DataTransferServiceClient;
import com.google.cloud.bigquery.datatransfer.v1.ScheduleTransferRunsRequest;
import com.google.cloud.bigquery.datatransfer.v1.ScheduleTransferRunsResponse;
import com.google.protobuf.Timestamp;
import java.io.IOException;
import org.threeten.bp.Clock;
import org.threeten.bp.Instant;
import org.threeten.bp.temporal.ChronoUnit;

// Sample to run schedule back fill for transfer config
public class ScheduleBackFill {

  public static void main(String[] args) throws IOException {
    // TODO(developer): Replace these variables before running the sample.
    String configId = "MY_CONFIG_ID";
    Clock clock = Clock.systemDefaultZone();
    Instant instant = clock.instant();
    Timestamp startTime =
        Timestamp.newBuilder()
            .setSeconds(instant.minus(5, ChronoUnit.DAYS).getEpochSecond())
            .setNanos(instant.minus(5, ChronoUnit.DAYS).getNano())
            .build();
    Timestamp endTime =
        Timestamp.newBuilder()
            .setSeconds(instant.minus(2, ChronoUnit.DAYS).getEpochSecond())
            .setNanos(instant.minus(2, ChronoUnit.DAYS).getNano())
            .build();
    scheduleBackFill(configId, startTime, endTime);
  }

  public static void scheduleBackFill(String configId, Timestamp startTime, Timestamp endTime)
      throws IOException {
    try (DataTransferServiceClient client = DataTransferServiceClient.create()) {
      ScheduleTransferRunsRequest request =
          ScheduleTransferRunsRequest.newBuilder()
              .setParent(configId)
              .setStartTime(startTime)
              .setEndTime(endTime)
              .build();
      ScheduleTransferRunsResponse response = client.scheduleTransferRuns(request);
      System.out.println("Schedule backfill run successfully :" + response.getRunsCount());
    } catch (ApiException ex) {
      System.out.print("Schedule backfill was not run." + ex.toString());
    }
  }
}
```

### Python

Before trying this sample, follow the Python setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Python API reference documentation](/python/docs/reference/bigquery/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` python
import datetime

from google.cloud.bigquery_datatransfer_v1 import (
    DataTransferServiceClient,
    StartManualTransferRunsRequest,
)

# Create a client object
client = DataTransferServiceClient()

# Replace with your transfer configuration name
transfer_config_name = "projects/1234/locations/us/transferConfigs/abcd"
now = datetime.datetime.now(datetime.timezone.utc)
start_time = now - datetime.timedelta(days=5)
end_time = now - datetime.timedelta(days=2)

# Some data sources, such as scheduled_query only support daily run.
# Truncate start_time and end_time to midnight time (00:00AM UTC).
start_time = datetime.datetime(
    start_time.year, start_time.month, start_time.day, tzinfo=datetime.timezone.utc
)
end_time = datetime.datetime(
    end_time.year, end_time.month, end_time.day, tzinfo=datetime.timezone.utc
)

requested_time_range = StartManualTransferRunsRequest.TimeRange(
    start_time=start_time,
    end_time=end_time,
)

# Initialize request argument(s)
request = StartManualTransferRunsRequest(
    parent=transfer_config_name,
    requested_time_range=requested_time_range,
)

# Make the request
response = client.start_manual_transfer_runs(request=request)

# Handle the response
print("Started manual transfer runs:")
for run in response.runs:
    print(f"backfill: {run.run_time} run: {run.name}")
```

**Caution:** Depending on the data source, and the amount of data you request, backfills may take several hours or days to complete.

## Logging and monitoring

The BigQuery Data Transfer Service exports logs and metrics to Cloud Monitoring and Cloud Logging that provide observability into your transfers. You can [use Monitoring](/bigquery/docs/dts-monitor) to set up dashboards to monitor transfers, evaluate transfer run performance, and view error messages to troubleshoot transfer failures. You can [use Logging](/bigquery/docs/dts-monitor#logs) to view logs related to a transfer run or a transfer configuration.

You can also [view audit logs](/bigquery/docs/audit-logging) that are available to the BigQuery Data Transfer Service for transfer activity and data access logs.
