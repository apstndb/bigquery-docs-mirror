# Create datasets

This document describes how to create datasets in BigQuery.

You can create datasets in the following ways:

  - Using the Google Cloud console.
  - Using a SQL query.
  - Using the `  bq mk  ` command in the bq command-line tool.
  - Calling the [`  datasets.insert  `](/bigquery/docs/reference/rest/v2/datasets/insert) API method.
  - Using the client libraries.
  - Copying an existing dataset.

To see steps for copying a dataset, including across regions, see [Copying datasets](/bigquery/docs/copying-datasets) .

Copying datasets is currently in [beta](https://cloud.google.com/products/#product-launch-stages) .

This document describes how to work with regular datasets that store data in BigQuery. To learn how to work with Spanner external datasets see [Create Spanner external datasets](/bigquery/docs/spanner-external-datasets) . To learn how to work with AWS Glue federated datasets see [Create AWS Glue federated datasets](/bigquery/docs/glue-federated-datasets) .

To learn to query tables in a public dataset, see [Query a public dataset with the Google Cloud console](/bigquery/docs/quickstarts/query-public-dataset-console) .

## Dataset limitations

BigQuery datasets are subject to the following limitations:

  - The [dataset location](/bigquery/docs/locations) can only be set at creation time. After a dataset is created, its location cannot be changed.

  - All tables that are referenced in a query must be stored in datasets in the same location.

  - External datasets don't support table expiration, replicas, time travel, default collation, default rounding mode, or the option to enable or disable case-insensitive table names.

  - When [you copy a table](/bigquery/docs/managing-tables#copy-table) , the datasets that contain the source table and destination table must reside in the same location.

  - Dataset names must be unique for each project.

  - If you change a dataset's [storage billing model](#dataset_storage_billing_models) , you must wait 14 days before you can change the storage billing model again.

  - You can't enroll a dataset in physical storage billing if you have any existing legacy [flat-rate slot commitments](/bigquery/docs/reservations-commitments-legacy) located in the same region as the dataset.

## Before you begin

Grant Identity and Access Management (IAM) roles that give users the necessary permissions to perform each task in this document.

### Required permissions

To create a dataset, you need the `  bigquery.datasets.create  ` IAM permission.

Each of the following predefined IAM roles includes the permissions that you need in order to create a dataset:

  - `  roles/bigquery.dataEditor  `
  - `  roles/bigquery.dataOwner  `
  - `  roles/bigquery.user  `
  - `  roles/bigquery.admin  `

For more information about IAM roles in BigQuery, see [Predefined roles and permissions](/bigquery/docs/access-control) .

**Note:** The creator of a dataset is automatically assigned the [BigQuery Data Owner ( `  roles/bigquery.dataOwner  ` ) role](/bigquery/docs/access-control#bigquery.dataOwner) on that dataset. So, a user or service account that has the ability to create a dataset also has the ability to delete it, even though that permission wasn't explicitly granted.

## Create datasets

To create a dataset:

### Console

Open the BigQuery page in the Google Cloud console.

In the left pane, click explore **Explorer** .

Select the project where you want to create the dataset.

Click more\_vert **View actions** , and then click **Create dataset** .

On the **Create dataset** page:

1.  For **Dataset ID** , enter a unique dataset [name](#dataset-naming) .
2.  For **Location type** , choose a geographic [location](/bigquery/docs/locations) for the dataset. After a dataset is created, the location can't be changed.
3.  Optional: Select **Link to an external dataset** if you're creating an [external dataset](/bigquery/docs/spanner-external-datasets) .
4.  If you don't need to configure additional options such as tags and table expirations, click **Create dataset** . Otherwise, expand the following section to configure the additional dataset options.

#### Additional options for datasets

Optional: Expand the **Tags** section to add [tags](/bigquery/docs/tags#attach_tags_when_you_create_a_new_dataset) to your dataset.

To apply an existing tag, do the following:

1.  Click the drop-down arrow beside **Select scope** and choose **Current scope** — **Select current organization** or **Select current project** .
2.  For **Key 1** and **Value 1** , choose the appropriate values from the lists.

To manually enter a new tag, do the following:

1.  Click the drop-down arrow beside **Select a scope** and choose **Manually enter IDs** \> **Organization** , **Project** , or **Tags** .
2.  If you're creating a tag for your project or organization, in the dialog, enter the `  PROJECT_ID  ` or the `  ORGANIZATION_ID  ` , and then click **Save** .
3.  For **Key 1** and **Value 1** , choose the appropriate values from the lists.
4.  To add additional tags to the table, click **Add tag** and follow the previous steps.

Optional: Expand the **Advanced options** section to configure one or more of the following options.

1.  To change the **Encryption** option to use your own cryptographic key with the [Cloud Key Management Service](/kms/docs/key-management-service) , select **Cloud KMS key** .
2.  To use case-insensitive table names, select **Enable case insensitive table names** .
3.  To change the **Default collation** [specification](/bigquery/docs/reference/standard-sql/collation-concepts#collate_spec_details) , choose the collation type from the list.
4.  To set an expiration for tables in the dataset, select **Enable table expiration** , then specify the **Default maximum table age** in days.
5.  To set a [**Default rounding mode**](/bigquery/docs/reference/rest/v2/RoundingMode) , choose the rounding mode from the list.
6.  To enable the physical [**Storage billing model**](/bigquery/docs/datasets-intro#dataset_storage_billing_models) , choose the billing model from the list.
7.  To set the dataset's [time travel window](/bigquery/docs/time-travel#time_travel) , choose the window size from the list.

Click **Create dataset** .

### SQL

Use the [`  CREATE SCHEMA  ` statement](/bigquery/docs/reference/standard-sql/data-definition-language#create_schema_statement) .

To create a dataset in a project other than your default project, add the project ID to the dataset ID in the following format: `  PROJECT_ID . DATASET_ID  ` .

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
    CREATE SCHEMA PROJECT_ID.DATASET_ID
      OPTIONS (
        default_kms_key_name = 'KMS_KEY_NAME',
        default_partition_expiration_days = PARTITION_EXPIRATION,
        default_table_expiration_days = TABLE_EXPIRATION,
        description = 'DESCRIPTION',
        labels = [('KEY_1','VALUE_1'),('KEY_2','VALUE_2')],
        location = 'LOCATION',
        max_time_travel_hours = HOURS,
        storage_billing_model = BILLING_MODEL);
    ```
    
    Replace the following:
    
      - `  PROJECT_ID  ` : your project ID
    
      - `  DATASET_ID  ` : the ID of the dataset that you're creating
    
      - `  KMS_KEY_NAME  ` : the name of the default Cloud Key Management Service key used to protect newly created tables in this dataset unless a different key is supplied at the time of creation. You cannot create a Google-encrypted table in a dataset with this parameter set.
    
      - `  PARTITION_EXPIRATION  ` : the default lifetime (in days) for partitions in newly created partitioned tables. The default partition expiration has no minimum value. The expiration time evaluates to the partition's date plus the integer value. Any partition created in a partitioned table in the dataset is deleted `  PARTITION_EXPIRATION  ` days after the partition's date. If you supply the `  time_partitioning_expiration  ` option when you create or update a partitioned table, the table-level partition expiration takes precedence over the dataset-level default partition expiration.
    
      - `  TABLE_EXPIRATION  ` : the default lifetime (in days) for newly created tables. The minimum value is 0.042 days (one hour). The expiration time evaluates to the current time plus the integer value. Any table created in the dataset is deleted `  TABLE_EXPIRATION  ` days after its creation time. This value is applied if you do not set a table expiration when you [create the table](/bigquery/docs/tables#create-table) .
    
      - `  DESCRIPTION  ` : a description of the dataset
    
      - `  KEY_1 : VALUE_1  ` : the key-value pair that you want to set as the first label on this dataset
    
      - `  KEY_2 : VALUE_2  ` : the key-value pair that you want to set as the second label
    
      - `  LOCATION  ` : the dataset's [location](/bigquery/docs/locations) . After a dataset is created, the location can't be changed.
        
        **Note:** If you choose `  EU  ` or an EU-based region for the dataset location, your Core BigQuery Customer Data resides in the EU. Core BigQuery Customer Data is defined in the [Service Specific Terms](https://cloud.google.com/terms/service-terms#13-google-bigquery-service) .
    
      - `  HOURS  ` : the duration in hours of the time travel window for the new dataset. The `  HOURS  ` value must be an integer expressed in multiples of 24 (48, 72, 96, 120, 144, 168) between 48 (2 days) and 168 (7 days). 168 hours is the default if this option isn't specified.
    
      - `  BILLING_MODEL  ` : sets the [storage billing model](/bigquery/docs/datasets-intro#dataset_storage_billing_models) for the dataset. Set the `  BILLING_MODEL  ` value to `  PHYSICAL  ` to use physical bytes when calculating storage charges, or to `  LOGICAL  ` to use logical bytes. `  LOGICAL  ` is the default.
        
        When you change a dataset's billing model, it takes 24 hours for the change to take effect.
        
        Once you change a dataset's storage billing model, you must wait 14 days before you can change the storage billing model again.

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](/bigquery/docs/running-queries#queries) .

### bq

To create a new dataset, use the [`  bq mk  `](/bigquery/docs/reference/bq-cli-reference#mk-dataset) command with the `  --location  ` flag. For a full list of possible parameters, see the [`  bq mk --dataset  ` command](/bigquery/docs/reference/bq-cli-reference#mk-dataset) reference.

To create a dataset in a project other than your default project, add the project ID to the dataset name in the following format: `  PROJECT_ID : DATASET_ID  ` .

``` text
bq --location=LOCATION mk \
    --dataset \
    --default_kms_key=KMS_KEY_NAME \
    --default_partition_expiration=PARTITION_EXPIRATION \
    --default_table_expiration=TABLE_EXPIRATION \
    --description="DESCRIPTION" \
    --label=KEY_1:VALUE_1 \
    --label=KEY_2:VALUE_2 \
    --add_tags=KEY_3:VALUE_3[,...] \
    --max_time_travel_hours=HOURS \
    --storage_billing_model=BILLING_MODEL \
    PROJECT_ID:DATASET_ID
```

Replace the following:

  - `  LOCATION  ` : the dataset's [location](/bigquery/docs/locations) . After a dataset is created, the location can't be changed. You can set a default value for the location by using the [`  .bigqueryrc  ` file](/bigquery/docs/bq-command-line-tool#setting_default_values_for_command-line_flags) .
    
    **Note:** If you choose **EU** for the dataset location, your Core BigQuery Customer Data resides in the EU. Core BigQuery Customer Data is defined in the [Service Specific Terms](https://cloud.google.com/terms/service-terms#13-google-bigquery-service) .

  - `  KMS_KEY_NAME  ` : the name of the default Cloud Key Management Service key used to protect newly created tables in this dataset unless a different key is supplied at the time of creation. You cannot create a Google-encrypted table in a dataset with this parameter set.

  - `  PARTITION_EXPIRATION  ` : the default lifetime (in seconds) for partitions in newly created partitioned tables. The default partition expiration has no minimum value. The expiration time evaluates to the partition's date plus the integer value. Any partition created in a partitioned table in the dataset is deleted `  PARTITION_EXPIRATION  ` seconds after the partition's date. If you supply the `  --time_partitioning_expiration  ` flag when you create or update a partitioned table, the table-level partition expiration takes precedence over the dataset-level default partition expiration.

  - `  TABLE_EXPIRATION  ` : the default lifetime (in seconds) for newly created tables. The minimum value is 3600 seconds (one hour). The expiration time evaluates to the current time plus the integer value. Any table created in the dataset is deleted `  TABLE_EXPIRATION  ` seconds after its creation time. This value is applied if you don't set a table expiration when you [create the table](/bigquery/docs/tables#create-table) .

  - `  DESCRIPTION  ` : a description of the dataset

  - `  KEY_1 : VALUE_1  ` : the key-value pair that you want to set as the first label on this dataset, and `  KEY_2 : VALUE_2  ` is the key-value pair that you want to set as the second label.

  - `  KEY_3 : VALUE_3  ` : the key-value pair that you want to set as a tag on the dataset. Add multiple tags under the same flag with commas between key:value pairs.

  - `  HOURS  ` : the duration in hours of the time travel window for the new dataset. The `  HOURS  ` value must be an integer expressed in multiples of 24 (48, 72, 96, 120, 144, 168) between 48 (2 days) and 168 (7 days). 168 hours is the default if this option isn't specified.

  - `  BILLING_MODEL  ` : sets the [storage billing model](/bigquery/docs/datasets-intro#dataset_storage_billing_models) for the dataset. Set the `  BILLING_MODEL  ` value to `  PHYSICAL  ` to use physical bytes when calculating storage charges, or to `  LOGICAL  ` to use logical bytes. `  LOGICAL  ` is the default.
    
    When you change a dataset's billing model, it takes 24 hours for the change to take effect.
    
    Once you change a dataset's storage billing model, you must wait 14 days before you can change the storage billing model again.

  - `  PROJECT_ID  ` : your project ID.

  - `  DATASET_ID  ` is the ID of the dataset that you're creating.

For example, the following command creates a dataset named `  mydataset  ` with data location set to `  US  ` , a default table expiration of 3600 seconds (1 hour), and a description of `  This is my dataset  ` . Instead of using the `  --dataset  ` flag, the command uses the `  -d  ` shortcut. If you omit `  -d  ` and `  --dataset  ` , the command defaults to creating a dataset.

``` text
bq --location=US mk -d \
    --default_table_expiration 3600 \
    --description "This is my dataset." \
    mydataset
```

To confirm that the dataset was created, enter the `  bq ls  ` command. Also, you can create a table when you create a new dataset using the following format: `  bq mk -t dataset . table  ` . For more information about creating tables, see [Creating a table](/bigquery/docs/tables#create-table) .

### Terraform

Use the [`  google_bigquery_dataset  `](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/bigquery_dataset) resource.

**Note:** You must enable the Cloud Resource Manager API in order to use Terraform to create BigQuery objects.

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

**Create a dataset**

The following example creates a dataset named `  mydataset  ` :

``` terraform
resource "google_bigquery_dataset" "default" {
  dataset_id                      = "mydataset"
  default_partition_expiration_ms = 2592000000  # 30 days
  default_table_expiration_ms     = 31536000000 # 365 days
  description                     = "dataset description"
  location                        = "US"
  max_time_travel_hours           = 96 # 4 days

  labels = {
    billing_group = "accounting",
    pii           = "sensitive"
  }
}
```

When you create a dataset using the `  google_bigquery_dataset  ` resource, it automatically grants access to the dataset to all accounts that are members of project-level [basic roles](/iam/docs/roles-overview#basic) . If you run the [`  terraform show  ` command](https://developer.hashicorp.com/terraform/cli/commands/show) after creating the dataset, the [`  access  ` block](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/bigquery_dataset#nested_access) for the dataset looks similar to the following:

To grant access to the dataset, we recommend that you use one of the [`  google_bigquery_iam  ` resources](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/bigquery_dataset_iam) , as shown in the following example, unless you plan to create authorized objects, such as [authorized views](/bigquery/docs/authorized-views) , within the dataset. In that case, use the [`  google_bigquery_dataset_access  ` resource](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/bigquery_dataset_access) . Refer to that documentation for examples.

**Create a dataset and grant access to it**

The following example creates a dataset named `  mydataset  ` , then uses the [`  google_bigquery_dataset_iam_policy  `](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/bigquery_dataset_iam#google_bigquery_dataset_iam_policy) resource to grant access to it.

**Note:** Don't use this approach if you want to use authorized objects, such as [authorized views](/bigquery/docs/authorized-views) , with this dataset. In that case, use the `  google_bigquery_dataset_access  ` resource. For examples, see [`  google_bigquery_dataset_access  `](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/bigquery_dataset_access) .

``` terraform
resource "google_bigquery_dataset" "default" {
  dataset_id                      = "mydataset"
  default_partition_expiration_ms = 2592000000  # 30 days
  default_table_expiration_ms     = 31536000000 # 365 days
  description                     = "dataset description"
  location                        = "US"
  max_time_travel_hours           = 96 # 4 days

  labels = {
    billing_group = "accounting",
    pii           = "sensitive"
  }
}

# Update the user, group, or service account
# provided by the members argument with the
# appropriate principals for your organization.
data "google_iam_policy" "default" {
  binding {
    role = "roles/bigquery.dataOwner"
    members = [
      "user:raha@altostrat.com",
    ]
  }
  binding {
    role = "roles/bigquery.admin"
    members = [
      "user:raha@altostrat.com",
    ]
  }
  binding {
    role = "roles/bigquery.user"
    members = [
      "group:analysts@altostrat.com",
    ]
  }
  binding {
    role = "roles/bigquery.dataViewer"
    members = [
      "serviceAccount:bqcx-1234567891011-abcd@gcp-sa-bigquery-condel.iam.gserviceaccount.com",
    ]
  }
}

resource "google_bigquery_dataset_iam_policy" "default" {
  dataset_id  = google_bigquery_dataset.default.dataset_id
  policy_data = data.google_iam_policy.default.policy_data
}
```

**Create a dataset with a customer-managed encryption key**

The following example creates a dataset named `  mydataset  ` , and also uses the [`  google_kms_crypto_key  `](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/kms_crypto_key) and [`  google_kms_key_ring  `](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/kms_key_ring) resources to specify a Cloud Key Management Service key for the dataset. You must [enable the Cloud Key Management Service API](https://console.cloud.google.com/flows/enableapi?apiid=cloudkms.googleapis.com&redirect=https://console.cloud.google.com) before running this example.

``` terraform
resource "google_bigquery_dataset" "default" {
  dataset_id                      = "mydataset"
  default_partition_expiration_ms = 2592000000  # 30 days
  default_table_expiration_ms     = 31536000000 # 365 days
  description                     = "dataset description"
  location                        = "US"
  max_time_travel_hours           = 96 # 4 days

  default_encryption_configuration {
    kms_key_name = google_kms_crypto_key.crypto_key.id
  }

  labels = {
    billing_group = "accounting",
    pii           = "sensitive"
  }
  depends_on = [google_project_iam_member.service_account_access]
}

resource "google_kms_crypto_key" "crypto_key" {
  name     = "example-key"
  key_ring = google_kms_key_ring.key_ring.id
}

resource "random_id" "default" {
  byte_length = 8
}

resource "google_kms_key_ring" "key_ring" {
  name     = "${random_id.default.hex}-example-keyring"
  location = "us"
}

# Enable the BigQuery service account to encrypt/decrypt Cloud KMS keys
data "google_project" "project" {
}

resource "google_project_iam_member" "service_account_access" {
  project = data.google_project.project.project_id
  role    = "roles/cloudkms.cryptoKeyEncrypterDecrypter"
  member  = "serviceAccount:bq-${data.google_project.project.number}@bigquery-encryption.iam.gserviceaccount.com"
}
```

To apply your Terraform configuration in a Google Cloud project, complete the steps in the following sections.

## Prepare Cloud Shell

1.  Launch [Cloud Shell](https://shell.cloud.google.com/) .

2.  Set the default Google Cloud project where you want to apply your Terraform configurations.
    
    You only need to run this command once per project, and you can run it in any directory.
    
    ``` text
    export GOOGLE_CLOUD_PROJECT=PROJECT_ID
    ```
    
    Environment variables are overridden if you set explicit values in the Terraform configuration file.

## Prepare the directory

Each Terraform configuration file must have its own directory (also called a *root module* ).

1.  In [Cloud Shell](https://shell.cloud.google.com/) , create a directory and a new file within that directory. The filename must have the `  .tf  ` extension—for example `  main.tf  ` . In this tutorial, the file is referred to as `  main.tf  ` .
    
    ``` text
    mkdir DIRECTORY && cd DIRECTORY && touch main.tf
    ```

2.  If you are following a tutorial, you can copy the sample code in each section or step.
    
    Copy the sample code into the newly created `  main.tf  ` .
    
    Optionally, copy the code from GitHub. This is recommended when the Terraform snippet is part of an end-to-end solution.

3.  Review and modify the sample parameters to apply to your environment.

4.  Save your changes.

5.  Initialize Terraform. You only need to do this once per directory.
    
    ``` text
    terraform init
    ```
    
    Optionally, to use the latest Google provider version, include the `  -upgrade  ` option:
    
    ``` text
    terraform init -upgrade
    ```

## Apply the changes

1.  Review the configuration and verify that the resources that Terraform is going to create or update match your expectations:
    
    ``` text
    terraform plan
    ```
    
    Make corrections to the configuration as necessary.

2.  Apply the Terraform configuration by running the following command and entering `  yes  ` at the prompt:
    
    ``` text
    terraform apply
    ```
    
    Wait until Terraform displays the "Apply complete\!" message.

3.  [Open your Google Cloud project](https://console.cloud.google.com/) to view the results. In the Google Cloud console, navigate to your resources in the UI to make sure that Terraform has created or updated them.

**Note:** Terraform samples typically assume that the required APIs are enabled in your Google Cloud project.

### API

Call the [`  datasets.insert  `](/bigquery/docs/reference/rest/v2/datasets/insert) method with a defined [dataset resource](/bigquery/docs/reference/rest/v2/datasets) .

### C\#

Before trying this sample, follow the C\# setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery C\# API reference documentation](/dotnet/docs/reference/Google.Cloud.BigQuery.V2/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` csharp
using Google.Apis.Bigquery.v2.Data;
using Google.Cloud.BigQuery.V2;

public class BigQueryCreateDataset
{
    public BigQueryDataset CreateDataset(
        string projectId = "your-project-id",
        string location = "US"
    )
    {
        BigQueryClient client = BigQueryClient.Create(projectId);
        var dataset = new Dataset
        {
            // Specify the geographic location where the dataset should reside.
            Location = location
        };
        // Create the dataset
        return client.CreateDataset(
            datasetId: "your_new_dataset_id", dataset);
    }
}
```

### Go

Before trying this sample, follow the Go setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Go API reference documentation](https://godoc.org/cloud.google.com/go/bigquery) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` go
import (
 "context"
 "fmt"

 "cloud.google.com/go/bigquery"
)

// createDataset demonstrates creation of a new dataset using an explicit destination location.
func createDataset(projectID, datasetID string) error {
 // projectID := "my-project-id"
 // datasetID := "mydataset"
 ctx := context.Background()

 client, err := bigquery.NewClient(ctx, projectID)
 if err != nil {
     return fmt.Errorf("bigquery.NewClient: %v", err)
 }
 defer client.Close()

 meta := &bigquery.DatasetMetadata{
     Location: "US", // See https://cloud.google.com/bigquery/docs/locations
 }
 if err := client.Dataset(datasetID).Create(ctx, meta); err != nil {
     return err
 }
 return nil
}
```

### Java

Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Java API reference documentation](/java/docs/reference/google-cloud-bigquery/latest/overview) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` java
import com.google.cloud.bigquery.BigQuery;
import com.google.cloud.bigquery.BigQueryException;
import com.google.cloud.bigquery.BigQueryOptions;
import com.google.cloud.bigquery.Dataset;
import com.google.cloud.bigquery.DatasetInfo;

public class CreateDataset {

  public static void runCreateDataset() {
    // TODO(developer): Replace these variables before running the sample.
    String datasetName = "MY_DATASET_NAME";
    createDataset(datasetName);
  }

  public static void createDataset(String datasetName) {
    try {
      // Initialize client that will be used to send requests. This client only needs to be created
      // once, and can be reused for multiple requests.
      BigQuery bigquery = BigQueryOptions.getDefaultInstance().getService();

      DatasetInfo datasetInfo = DatasetInfo.newBuilder(datasetName).build();

      Dataset newDataset = bigquery.create(datasetInfo);
      String newDatasetName = newDataset.getDatasetId().getDataset();
      System.out.println(newDatasetName + " created successfully");
    } catch (BigQueryException e) {
      System.out.println("Dataset was not created. \n" + e.toString());
    }
  }
}
```

### Node.js

Before trying this sample, follow the Node.js setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Node.js API reference documentation](https://googleapis.dev/nodejs/bigquery/latest/index.html) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` javascript
// Import the Google Cloud client library and create a client
const {BigQuery} = require('@google-cloud/bigquery');
const bigquery = new BigQuery();

async function createDataset() {
  // Creates a new dataset named "my_dataset".

  /**
   * TODO(developer): Uncomment the following lines before running the sample.
   */
  // const datasetId = "my_new_dataset";

  // Specify the geographic location where the dataset should reside
  const options = {
    location: 'US',
  };

  // Create a new dataset
  const [dataset] = await bigquery.createDataset(datasetId, options);
  console.log(`Dataset ${dataset.id} created.`);
}
createDataset();
```

### PHP

Before trying this sample, follow the PHP setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery PHP API reference documentation](/php/docs/reference/cloud-bigquery/latest/BigQueryClient) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` php
use Google\Cloud\BigQuery\BigQueryClient;

/** Uncomment and populate these variables in your code */
// $projectId = 'The Google project ID';
// $datasetId = 'The BigQuery dataset ID';

$bigQuery = new BigQueryClient([
    'projectId' => $projectId,
]);
$dataset = $bigQuery->createDataset($datasetId);
printf('Created dataset %s' . PHP_EOL, $datasetId);
```

### Python

Before trying this sample, follow the Python setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Python API reference documentation](/python/docs/reference/bigquery/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` python
from google.cloud import bigquery

# Construct a BigQuery client object.
client = bigquery.Client()

# TODO(developer): Set dataset_id to the ID of the dataset to create.
# dataset_id = "{}.your_dataset".format(client.project)

# Construct a full Dataset object to send to the API.
dataset = bigquery.Dataset(dataset_id)

# TODO(developer): Specify the geographic location where the dataset should reside.
dataset.location = "US"

# Send the dataset to the API for creation, with an explicit timeout.
# Raises google.api_core.exceptions.Conflict if the Dataset already
# exists within the project.
dataset = client.create_dataset(dataset, timeout=30)  # Make an API request.
print("Created dataset {}.{}".format(client.project, dataset.dataset_id))
```

### Ruby

Before trying this sample, follow the Ruby setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Ruby API reference documentation](https://googleapis.dev/ruby/google-cloud-bigquery/latest/Google/Cloud/Bigquery.html) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` ruby
require "google/cloud/bigquery"

def create_dataset dataset_id = "my_dataset", location = "US"
  bigquery = Google::Cloud::Bigquery.new

  # Create the dataset in a specified geographic location
  bigquery.create_dataset dataset_id, location: location

  puts "Created dataset: #{dataset_id}"
end
```

## Name datasets

When you create a dataset in BigQuery, the dataset name must be unique for each project. The dataset name can contain the following:

  - Up to 1,024 characters.
  - Letters (uppercase or lowercase), numbers, and underscores.

Dataset names are case-sensitive by default. `  mydataset  ` and `  MyDataset  ` can coexist in the same project, unless one of them has case-sensitivity turned off. For examples, see [Creating a case-insensitive dataset](/bigquery/docs/reference/standard-sql/data-definition-language#creating_a_case-insensitive_dataset) and [Resource: Dataset](/bigquery/docs/reference/rest/v2/datasets#resource:-dataset) .

Dataset names cannot contain spaces or special characters such as `  -  ` , `  &  ` , `  @  ` , or `  %  ` .

### Hidden datasets

A hidden dataset is a dataset whose name begins with an underscore. You can query tables and views in hidden datasets the same way you would in any other dataset. Hidden datasets have the following restrictions:

  - They are hidden from the **Explorer** panel in the Google Cloud console.
  - They don't appear in any `  INFORMATION_SCHEMA  ` views.
  - They can't be used with [linked datasets](/bigquery/docs/analytics-hub-introduction#linked_datasets) .
  - They can't be used as a source dataset with the following authorized resources:
      - [Authorized datasets](/bigquery/docs/authorized-datasets)
      - [Authorized routines](/bigquery/docs/authorized-routines)
      - [Authorized views](/bigquery/docs/authorized-views)
  - They don't appear in Data Catalog (deprecated) or Dataplex Universal Catalog.
  - They can't be used as a source dataset for creating a [dataset replica](/bigquery/docs/data-replication#dataset_replication)

## Dataset security

To control access to datasets in BigQuery, see [Controlling access to datasets](/bigquery/docs/control-access-to-resources-iam) . For information about data encryption, see [Encryption at rest](/bigquery/docs/encryption-at-rest) .

## What's next

  - For more information about listing datasets in a project, see [Listing datasets](/bigquery/docs/listing-datasets) .
  - For more information about dataset metadata, see [Getting information about datasets](/bigquery/docs/dataset-metadata) .
  - For more information about changing dataset properties, see [Updating datasets](/bigquery/docs/updating-datasets) .
  - For more information about creating and managing labels, see [Creating and managing labels](/bigquery/docs/labels) .
