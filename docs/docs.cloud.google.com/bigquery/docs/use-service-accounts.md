# Use service accounts with BigQuery Data Transfer Service

Some data sources support data transfer authentication by using a [service account](/iam/docs/service-account-overview) through the Google Cloud console, API, or the `  bq  ` command line. A service account is a Google Account associated with your Google Cloud project. A service account can run jobs, such as scheduled queries or batch processing pipelines by authenticating with the service account credentials rather than a user's credentials.

You can update an existing data transfer with the credentials of a service account. For more information, see [Update data transfer credentials](#update_data_transfer_credentials) .

The following situations require updating credentials:

  - Your transfer failed to authorize the user's access to the data source:
    
    `  Error code 401 : Request is missing required authentication credential. UNAUTHENTICATED  `

  - You receive an **INVALID\_USER** error when you attempt to run the transfer:
    
    `  Error code 5 : Authentication failure: User Id not found. Error code: INVALID_USERID  `

To learn more about authenticating with service accounts, see [Introduction to authentication](/bigquery/docs/authentication#sa-impersonation) .

## Data sources with service account support

BigQuery Data Transfer Service can use service account credentials for transfers with the following:

\* [Cloud Storage](/bigquery/docs/cloud-storage-transfer) \* [Amazon Redshift](/bigquery/docs/migration/redshift-overview) \* [Amazon S3](/bigquery/docs/s3-transfer-intro) \* [Campaign Manager](/bigquery/docs/doubleclick-campaign-transfer) \* [Carbon Footprint](/carbon-footprint/docs/export) \* [Dataset Copy](/bigquery/docs/copying-datasets) \* [Display & Video 360](/bigquery/docs/display-video-transfer) \* [Google Ad Manager](/bigquery/docs/doubleclick-publisher-transfer) \* [Google Ads](/bigquery/docs/google-ads-transfer) \* [Google Merchant Center](/bigquery/docs/merchant-center-transfer) \* [Google Play](/bigquery/docs/play-transfer) \* [Scheduled Queries](/bigquery/docs/scheduling-queries#using_a_service_account) \* [Search Ads 360](/bigquery/docs/search-ads-transfer) \* [Teradata](/bigquery/docs/migration/teradata-overview) \* [YouTube Content Owner](/bigquery/docs/youtube-content-owner-transfer)

## Before you begin

  - Verify that you have completed all actions required in [Enabling BigQuery Data Transfer Service](/bigquery/docs/enable-transfer-service) .
  - Grant Identity and Access Management (IAM) roles that give users the necessary permissions to perform each task in this document.

### Required permissions

To update a data transfer to use a service account, you must have the following permissions:

  - The `  bigquery.transfers.update  ` permission to modify the transfer.
    
    The predefined `  roles/bigquery.admin  ` IAM role includes this permission.

  - Access to the service account. For more information about granting users the service account role, see [Service Account User role](/iam/docs/service-account-permissions#user-role) .

Ensure that the service account you choose to run the transfer has the following permissions:

  - The `  bigquery.datasets.get  ` and `  bigquery.datasets.update  ` permissions on the target dataset. If the table uses [column-level access control](/bigquery/docs/column-level-security-intro) , the service account must also have the `  bigquery.tables.setCategory  ` permission.
    
    The `  bigquery.admin  ` predefined IAM role includes all of these permissions. For more information about IAM roles in BigQuery Data Transfer Service, see [Introduction to IAM](/bigquery/docs/access-control) .

  - Access to the configured transfer data source. For more information about the required permissions for different data sources, see [Data sources with service account support](#data_sources_with_service_account_support) .

  - For Google Ads transfers, the service account must be granted domain-wide authority. For more information, see [Google Ads API Service Account guide](https://developers.google.com/google-ads/api/docs/oauth/service-accounts#service_account_access_setup) .

## Update data transfer credentials

### Console

The following procedure updates a data transfer configuration to authenticate as a service account instead of your individual user account.

1.  In the Google Cloud console, go to the Data transfers page.

2.  Click the transfer in the data transfers list.

3.  Click **EDIT** to update the transfer configuration.

4.  In the **Service Account** field, enter the service account name.

5.  Click **Save** .

### bq

To update the credentials of a data transfer, you can use the bq command-line tool to update the transfer configuration.

Use the `  bq update  ` command with the `  --transfer_config  ` , `  --update_credentials  ` , and `  --service_account_name  ` flags.

For example, the following command updates a data transfer configuration to authenticate as a service account instead of your individual user account:

``` text
bq update \
--transfer_config \
--update_credentials \
--service_account_name=abcdef-test-sa@abcdef-test.iam.gserviceaccount.com projects/862514376110/locations/us/transferConfigs/5dd12f26-0000-262f-bc38-089e0820fe38 \
```

**Note:** If you are using the bq command-line tool, use the `  --service_account_name  ` flag instead of authenticating as a service account.

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
