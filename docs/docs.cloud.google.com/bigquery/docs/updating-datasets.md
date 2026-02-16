# Update dataset properties

This document describes how to update dataset properties in BigQuery. After you create a dataset, you can update the following dataset properties:

  - [Billing model](#update_storage_billing_models)
  - Default [expiration time](#table-expiration) for new tables
  - Default [partition expiration](#partition-expiration) for new partitioned tables
  - Default [rounding mode](#update_rounding_mode) for new tables
  - [Description](#update-dataset-description)
  - [Labels](/bigquery/docs/adding-using-labels#adding_dataset_labels)
  - [Time travel windows](#update_time_travel_windows)

## Before you begin

Grant Identity and Access Management (IAM) roles that give users the necessary permissions to perform each task in this document.

### Required permissions

To update dataset properties, you need the following IAM permissions:

  - `  bigquery.datasets.update  `
  - `  bigquery.datasets.setIamPolicy  ` (only required when updating dataset access controls in the Google Cloud console)

The `  roles/bigquery.dataOwner  ` predefined IAM role includes the permissions that you need to update dataset properties.

Additionally, if you have the `  bigquery.datasets.create  ` permission, you can update properties of the datasets that you create.

For more information on IAM roles and permissions in BigQuery, see [Predefined roles and permissions](/bigquery/access-control) .

## Update dataset descriptions

You can update a dataset's description in the following ways:

  - Using the Google Cloud console.
  - Using the bq command-line tool's `  bq update  ` command.
  - Calling the [`  datasets.patch  `](/bigquery/docs/reference/rest/v2/datasets/patch) API method.
  - Using the client libraries.

To update a dataset's description:

### Console

1.  In the left pane, click explore **Explorer** :
    
    If you don't see the left pane, click last\_page **Expand left pane** to open the pane.

2.  In the **Explorer** pane, expand your project, click **Datasets** , and then click a dataset.

3.  In the **Details** pane, click mode\_edit **Edit details** to edit the description text.
    
    In the **Edit detail** dialog that appears, do the following:
    
    1.  In the **Description** field, enter a description or edit the existing description.
    2.  To save the new description text, click **Save** .

### SQL

To update a dataset's description, use the [`  ALTER SCHEMA SET OPTIONS  ` statement](/bigquery/docs/reference/standard-sql/data-definition-language#alter_schema_set_options_statement) to set the `  description  ` option.

The following example sets the description on a dataset named `  mydataset  ` :

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
     ALTER SCHEMA mydataset
     SET OPTIONS (
         description = 'Description of mydataset');
     
    ```

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](/bigquery/docs/running-queries#queries) .

### bq

Issue the `  bq update  ` command with the `  --description  ` flag. If you are updating a dataset in a project other than your default project, add the project ID to the dataset name in the following format: `  project_id : dataset  ` .

``` text
bq update \
--description "string" \
project_id:dataset
```

Replace the following:

  - `  string  ` : the text that describes the dataset, in quotes
  - `  project_id  ` : your project ID
  - `  dataset  ` : the name of the dataset that you're updating

Examples:

Enter the following command to change the description of `  mydataset  ` to "Description of mydataset." `  mydataset  ` is in your default project.

``` text
bq update --description "Description of mydataset" mydataset
```

Enter the following command to change the description of `  mydataset  ` to "Description of mydataset." The dataset is in `  myotherproject  ` , not your default project.

``` text
bq update \
--description "Description of mydataset" \
myotherproject:mydataset
```

### API

Call [`  datasets.patch  `](/bigquery/docs/reference/rest/v2/datasets/patch) and update the `  description  ` property in the [dataset resource](/bigquery/docs/reference/rest/v2/datasets) . Because the `  datasets.update  ` method replaces the entire dataset resource, the `  datasets.patch  ` method is preferred.

### Go

Before trying this sample, follow the Go setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Go API reference documentation](https://godoc.org/cloud.google.com/go/bigquery) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` go
import (
 "context"
 "fmt"

 "cloud.google.com/go/bigquery"
)

// updateDatasetDescription demonstrates how the Description metadata of a dataset can
// be read and modified.
func updateDatasetDescription(projectID, datasetID string) error {
 // projectID := "my-project-id"
 // datasetID := "mydataset"
 ctx := context.Background()
 client, err := bigquery.NewClient(ctx, projectID)
 if err != nil {
     return fmt.Errorf("bigquery.NewClient: %v", err)
 }
 defer client.Close()

 ds := client.Dataset(datasetID)
 meta, err := ds.Metadata(ctx)
 if err != nil {
     return err
 }
 update := bigquery.DatasetMetadataToUpdate{
     Description: "Updated Description.",
 }
 if _, err = ds.Update(ctx, update, meta.ETag); err != nil {
     return err
 }
 return nil
}
```

### Java

Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Java API reference documentation](/java/docs/reference/google-cloud-bigquery/latest/overview) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

Create a [Dataset.Builder](/java/docs/reference/google-cloud-bigquery/latest/com.google.cloud.bigquery.Dataset.Builder) instance from an existing [Dataset](/java/docs/reference/google-cloud-bigquery/latest/com.google.cloud.bigquery.Dataset) instance with the [Dataset.toBuilder()](/java/docs/reference/google-cloud-bigquery/latest/com.google.cloud.bigquery.Dataset#com_google_cloud_bigquery_Dataset_toBuilder__) method. Configure the dataset builder object. Build the updated dataset with the [Dataset.Builder.build()](/java/docs/reference/google-cloud-bigquery/latest/com.google.cloud.bigquery.Dataset.Builder#com_google_cloud_bigquery_Dataset_Builder_build__) method, and call the [Dataset.update()](/java/docs/reference/google-cloud-bigquery/latest/com.google.cloud.bigquery.Dataset#com_google_cloud_bigquery_Dataset_update_com_google_cloud_bigquery_BigQuery_DatasetOption____) method to send the update to the API.

``` java
import com.google.cloud.bigquery.BigQuery;
import com.google.cloud.bigquery.BigQueryException;
import com.google.cloud.bigquery.BigQueryOptions;
import com.google.cloud.bigquery.Dataset;

public class UpdateDatasetDescription {

  public static void runUpdateDatasetDescription() {
    // TODO(developer): Replace these variables before running the sample.
    String datasetName = "MY_DATASET_NAME";
    String newDescription = "this is the new dataset description";
    updateDatasetDescription(datasetName, newDescription);
  }

  public static void updateDatasetDescription(String datasetName, String newDescription) {
    try {
      // Initialize client that will be used to send requests. This client only needs to be created
      // once, and can be reused for multiple requests.
      BigQuery bigquery = BigQueryOptions.getDefaultInstance().getService();

      Dataset dataset = bigquery.getDataset(datasetName);
      bigquery.update(dataset.toBuilder().setDescription(newDescription).build());
      System.out.println("Dataset description updated successfully to " + newDescription);
    } catch (BigQueryException e) {
      System.out.println("Dataset description was not updated \n" + e.toString());
    }
  }
}
```

### Node.js

Before trying this sample, follow the Node.js setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Node.js API reference documentation](https://googleapis.dev/nodejs/bigquery/latest/index.html) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` javascript
// Import the Google Cloud client library
const {BigQuery} = require('@google-cloud/bigquery');
const bigquery = new BigQuery();

async function updateDatasetDescription() {
  // Updates a dataset's description.

  // Retreive current dataset metadata
  const dataset = bigquery.dataset(datasetId);
  const [metadata] = await dataset.getMetadata();

  // Set new dataset description
  const description = 'New dataset description.';
  metadata.description = description;

  const [apiResponse] = await dataset.setMetadata(metadata);
  const newDescription = apiResponse.description;

  console.log(`${datasetId} description: ${newDescription}`);
}
```

### Python

Before trying this sample, follow the Python setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Python API reference documentation](/python/docs/reference/bigquery/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

Configure the [Dataset.description](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.Dataset#google_cloud_bigquery_dataset_Dataset_description) property and call [Client.update\_dataset()](/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client#google_cloud_bigquery_client_Client_update_dataset) to send the update to the API.

``` python
from google.cloud import bigquery

# Construct a BigQuery client object.
client = bigquery.Client()

# TODO(developer): Set dataset_id to the ID of the dataset to fetch.
# dataset_id = 'your-project.your_dataset'

dataset = client.get_dataset(dataset_id)  # Make an API request.
dataset.description = "Updated description."
dataset = client.update_dataset(dataset, ["description"])  # Make an API request.

full_dataset_id = "{}.{}".format(dataset.project, dataset.dataset_id)
print(
    "Updated dataset '{}' with description '{}'.".format(
        full_dataset_id, dataset.description
    )
)
```

## Update default table expiration times

You can update a dataset's default table expiration time in the following ways:

  - Using the Google Cloud console.
  - Using the bq command-line tool's `  bq update  ` command.
  - Calling the [`  datasets.patch  `](/bigquery/docs/reference/rest/v2/datasets/patch) API method.
  - Using the client libraries.

You can set a default table expiration time at the dataset level, or you can set a table's expiration time when the table is created. If you set the expiration when the table is created, the dataset's default table expiration is ignored. If you don't set a default table expiration at the dataset level, and you don't set a table expiration when the table is created, the table never expires and you must [delete the table](/bigquery/docs/managing-tables#deleting_tables) manually. When a table expires, it's deleted along with all of the data it contains.

When you update a dataset's default table expiration setting:

  - If you change the value from `  Never  ` to a defined expiration time, any tables that already exist in the dataset won't expire unless the expiration time was set on the table when it was created.
  - If you are changing the value for the default table expiration, any tables that already exist expire according to the original table expiration setting. Any new tables created in the dataset have the new table expiration setting applied unless you specify a different table expiration on the table when it is created.

The value for default table expiration is expressed differently depending on where the value is set. Use the method that gives you the appropriate level of granularity:

  - In the Google Cloud console, expiration is expressed in days.
  - In the bq command-line tool, expiration is expressed in seconds.
  - In the API, expiration is expressed in milliseconds.

To update the default expiration time for a dataset:

### Console

1.  In the left pane, click explore **Explorer** :

2.  In the **Explorer** pane, expand your project, click **Datasets** , and then click a dataset.

3.  In the **Details** tab, click mode\_edit **Edit details** to edit the expiration time.

4.  In the **Edit detail** dialog, in the **Default table expiration** section, select **Enable table expiration** and enter a value for **Default maximum table age** .

5.  Click **Save** .

### SQL

To update the default table expiration time, use the [`  ALTER SCHEMA SET OPTIONS  ` statement](/bigquery/docs/reference/standard-sql/data-definition-language#alter_schema_set_options_statement) to set the `  default_table_expiration_days  ` option.

The following example updates the default table expiration for a dataset named `  mydataset  ` .

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
     ALTER SCHEMA mydataset
     SET OPTIONS(
         default_table_expiration_days = 3.75);
     
    ```

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](/bigquery/docs/running-queries#queries) .

### bq

To update the default expiration time for newly created tables in a dataset, enter the `  bq update  ` command with the `  --default_table_expiration  ` flag. If you are updating a dataset in a project other than your default project, add the project ID to the dataset name in the following format: `  project_id : dataset  ` .

``` text
bq update \
--default_table_expiration integer \
project_id:dataset
```

Replace the following:

  - `  integer  ` : the default lifetime, in seconds, for newly created tables. The minimum value is 3600 seconds (one hour). The expiration time evaluates to the current UTC time plus the integer value. Specify `  0  ` to remove the existing expiration time. Any table created in the dataset is deleted `  integer  ` seconds after its creation time. This value is applied if you do not set a table expiration when the table is [created](/bigquery/docs/tables#create-table) .
  - `  project_id  ` : your project ID.
  - `  dataset  ` : the name of the dataset that you're updating.

Examples:

Enter the following command to set the default table expiration for new tables created in `  mydataset  ` to two hours (7200 seconds) from the current time. The dataset is in your default project.

``` text
bq update --default_table_expiration 7200 mydataset
```

Enter the following command to set the default table expiration for new tables created in `  mydataset  ` to two hours (7200 seconds) from the current time. The dataset is in `  myotherproject  ` , not your default project.

``` text
bq update --default_table_expiration 7200 myotherproject:mydataset
```

### API

Call [`  datasets.patch  `](/bigquery/docs/reference/rest/v2/datasets/patch) and update the `  defaultTableExpirationMs  ` property in the [dataset resource](/bigquery/docs/reference/rest/v2/datasets) . The expiration is expressed in milliseconds in the API. Because the `  datasets.update  ` method replaces the entire dataset resource, the `  datasets.patch  ` method is preferred.

### Go

Before trying this sample, follow the Go setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Go API reference documentation](https://godoc.org/cloud.google.com/go/bigquery) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` go
import (
 "context"
 "fmt"
 "time"

 "cloud.google.com/go/bigquery"
)

// updateDatasetDefaultExpiration demonstrats setting the default expiration of a dataset
// to a specific retention period.
func updateDatasetDefaultExpiration(projectID, datasetID string) error {
 // projectID := "my-project-id"
 // datasetID := "mydataset"
 ctx := context.Background()
 client, err := bigquery.NewClient(ctx, projectID)
 if err != nil {
     return fmt.Errorf("bigquery.NewClient: %v", err)
 }
 defer client.Close()

 ds := client.Dataset(datasetID)
 meta, err := ds.Metadata(ctx)
 if err != nil {
     return err
 }
 update := bigquery.DatasetMetadataToUpdate{
     DefaultTableExpiration: 24 * time.Hour,
 }
 if _, err := client.Dataset(datasetID).Update(ctx, update, meta.ETag); err != nil {
     return err
 }
 return nil
}
```

### Java

Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Java API reference documentation](/java/docs/reference/google-cloud-bigquery/latest/overview) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

Create a [Dataset.Builder](/java/docs/reference/google-cloud-bigquery/latest/com.google.cloud.bigquery.Dataset.Builder) instance from an existing [Dataset](/java/docs/reference/google-cloud-bigquery/latest/com.google.cloud.bigquery.Dataset) instance with the [Dataset.toBuilder()](/java/docs/reference/google-cloud-bigquery/latest/com.google.cloud.bigquery.Dataset#com_google_cloud_bigquery_Dataset_toBuilder__) method. Configure the dataset builder object. Build the updated dataset with the [Dataset.Builder.build()](/java/docs/reference/google-cloud-bigquery/latest/com.google.cloud.bigquery.Dataset.Builder#com_google_cloud_bigquery_Dataset_Builder_build__) method, and call the [Dataset.update()](/java/docs/reference/google-cloud-bigquery/latest/com.google.cloud.bigquery.Dataset#com_google_cloud_bigquery_Dataset_update_com_google_cloud_bigquery_BigQuery_DatasetOption____) method to send the update to the API.

Configure the default expiration time with the [Dataset.Builder.setDefaultTableLifetime()](/java/docs/reference/google-cloud-bigquery/latest/com.google.cloud.bigquery.Dataset.Builder#com_google_cloud_bigquery_Dataset_Builder_setDefaultTableLifetime_java_lang_Long_) method.

``` java
import com.google.cloud.bigquery.BigQuery;
import com.google.cloud.bigquery.BigQueryException;
import com.google.cloud.bigquery.BigQueryOptions;
import com.google.cloud.bigquery.Dataset;
import java.util.concurrent.TimeUnit;

public class UpdateDatasetExpiration {

  public static void runUpdateDatasetExpiration() {
    // TODO(developer): Replace these variables before running the sample.
    String datasetName = "MY_DATASET_NAME";
    updateDatasetExpiration(datasetName);
  }

  public static void updateDatasetExpiration(String datasetName) {
    try {
      // Initialize client that will be used to send requests. This client only needs to be created
      // once, and can be reused for multiple requests.
      BigQuery bigquery = BigQueryOptions.getDefaultInstance().getService();

      // Update dataset expiration to one day
      Long newExpiration = TimeUnit.MILLISECONDS.convert(1, TimeUnit.DAYS);

      Dataset dataset = bigquery.getDataset(datasetName);
      bigquery.update(dataset.toBuilder().setDefaultTableLifetime(newExpiration).build());
      System.out.println("Dataset description updated successfully to " + newExpiration);
    } catch (BigQueryException e) {
      System.out.println("Dataset expiration was not updated \n" + e.toString());
    }
  }
}
```

### Node.js

Before trying this sample, follow the Node.js setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Node.js API reference documentation](https://googleapis.dev/nodejs/bigquery/latest/index.html) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` javascript
// Import the Google Cloud client library
const {BigQuery} = require('@google-cloud/bigquery');
const bigquery = new BigQuery();

async function updateDatasetExpiration() {
  // Updates the lifetime of all tables in the dataset, in milliseconds.

  /**
   * TODO(developer): Uncomment the following lines before running the sample.
   */
  // const datasetId = "my_dataset";

  // Retreive current dataset metadata
  const dataset = bigquery.dataset(datasetId);
  const [metadata] = await dataset.getMetadata();

  // Set new dataset metadata
  const expirationTime = 24 * 60 * 60 * 1000;
  metadata.defaultTableExpirationMs = expirationTime.toString();

  const [apiResponse] = await dataset.setMetadata(metadata);
  const newExpirationTime = apiResponse.defaultTableExpirationMs;

  console.log(`${datasetId} expiration: ${newExpirationTime}`);
}
```

### Python

Before trying this sample, follow the Python setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Python API reference documentation](/python/docs/reference/bigquery/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

Configure the [Dataset.default\_table\_expiration\_ms](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.Dataset#google_cloud_bigquery_dataset_Dataset_default_table_expiration_ms) property and call [Client.update\_dataset()](/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client#google_cloud_bigquery_client_Client_update_dataset) to send the update to the API.

``` python
from google.cloud import bigquery

# Construct a BigQuery client object.
client = bigquery.Client()

# TODO(developer): Set dataset_id to the ID of the dataset to fetch.
# dataset_id = 'your-project.your_dataset'

dataset = client.get_dataset(dataset_id)  # Make an API request.
dataset.default_table_expiration_ms = 24 * 60 * 60 * 1000  # In milliseconds.

dataset = client.update_dataset(
    dataset, ["default_table_expiration_ms"]
)  # Make an API request.

full_dataset_id = "{}.{}".format(dataset.project, dataset.dataset_id)
print(
    "Updated dataset {} with new expiration {}".format(
        full_dataset_id, dataset.default_table_expiration_ms
    )
)
```

## Update default partition expiration times

You can update a dataset's default partition expiration in the following ways:

  - Using the bq command-line tool's `  bq update  ` command.
  - Calling the [`  datasets.patch  `](/bigquery/docs/reference/rest/v2/datasets/patch) API method.
  - Using the client libraries.

Setting or updating a dataset's default partition expiration isn't supported by the Google Cloud console.

You can set a default partition expiration time at the dataset level that affects all newly created partitioned tables, or you can set a [partition expiration](/bigquery/docs/managing-partitioned-tables#partition-expiration) time for individual tables when the partitioned tables are created. If you set the default partition expiration at the dataset level, and you set the default table expiration at the dataset level, new partitioned tables will only have a partition expiration. If both options are set, the default partition expiration overrides the default table expiration.

If you set the partition expiration time when the partitioned table is created, that value overrides the dataset-level default partition expiration if it exists.

If you do not set a default partition expiration at the dataset level, and you do not set a partition expiration when the table is created, the partitions never expire and you must [delete](#deleting_a_table) the partitions manually.

When you set a default partition expiration on a dataset, the expiration applies to all partitions in all partitioned tables created in the dataset. When you set the partition expiration on a table, the expiration applies to all partitions created in the specified table. You cannot apply different expiration times to different partitions in the same table.

When you update a dataset's default partition expiration setting:

  - If you change the value from `  never  ` to a defined expiration time, any partitions that already exist in partitioned tables in the dataset will not expire unless the partition expiration time was set on the table when it was created.
  - If you are changing the value for the default partition expiration, any partitions in existing partitioned tables expire according to the original default partition expiration. Any new partitioned tables created in the dataset have the new default partition expiration setting applied unless you specify a different partition expiration on the table when it is created.

The value for default partition expiration is expressed differently depending on where the value is set. Use the method that gives you the appropriate level of granularity:

  - In the bq command-line tool, expiration is expressed in seconds.
  - In the API, expiration is expressed in milliseconds.

To update the default partition expiration time for a dataset:

### Console

Updating a dataset's default partition expiration is not supported by the Google Cloud console.

### SQL

To update the default partition expiration time, use the [`  ALTER SCHEMA SET OPTIONS  ` statement](/bigquery/docs/reference/standard-sql/data-definition-language#alter_schema_set_options_statement) to set the `  default_partition_expiration_days  ` option.

The following example updates the default partition expiration for a dataset named `  mydataset  ` :

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
     ALTER SCHEMA mydataset
     SET OPTIONS(
         default_partition_expiration_days = 3.75);
     
    ```

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](/bigquery/docs/running-queries#queries) .

### bq

To update the default expiration time for a dataset, enter the `  bq update  ` command with the `  --default_partition_expiration  ` flag. If you are updating a dataset in a project other than your default project, add the project ID to the dataset name in the following format: `  project_id : dataset  ` .

``` text
bq update \
--default_partition_expiration integer \
project_id:dataset
```

Replace the following:

  - `  integer  ` : the default lifetime, in seconds, for partitions in newly created partitioned tables. This flag has no minimum value. Specify `  0  ` to remove the existing expiration time. Any partitions in newly created partitioned tables are deleted `  integer  ` seconds after the partition's UTC date. This value is applied if you do not set a partition expiration on the table when it is created.
  - `  project_id  ` : your project ID.
  - `  dataset  ` : the name of the dataset that you're updating.

Examples:

Enter the following command to set the default partition expiration for new partitioned tables created in `  mydataset  ` to 26 hours (93,600 seconds). The dataset is in your default project.

``` text
bq update --default_partition_expiration 93600 mydataset
```

Enter the following command to set the default partition expiration for new partitioned tables created in `  mydataset  ` to 26 hours (93,600 seconds). The dataset is in `  myotherproject  ` , not your default project.

``` text
bq update --default_partition_expiration 93600 myotherproject:mydataset
```

### API

Call [`  datasets.patch  `](/bigquery/docs/reference/rest/v2/datasets/patch) and update the `  defaultPartitionExpirationMs  ` property in the [dataset resource](/bigquery/docs/reference/rest/v2/datasets) . The expiration is expressed in milliseconds. Because the `  datasets.update  ` method replaces the entire dataset resource, the `  datasets.patch  ` method is preferred.

## Update rounding mode

You can update a dataset's default [rounding mode](/bigquery/docs/schemas#rounding_mode) by using the [`  ALTER SCHEMA SET OPTIONS  ` DDL statement](/bigquery/docs/reference/standard-sql/data-definition-language#alter_schema_set_options_statement) . The following example updates the default rounding mode for `  mydataset  ` to `  ROUND_HALF_EVEN  ` .

``` text
ALTER SCHEMA mydataset
SET OPTIONS (
  default_rounding_mode = "ROUND_HALF_EVEN");
```

This sets the default rounding mode for new tables created in the dataset. It has no impact on new columns added to existing tables. Setting the default rounding mode on a table in the dataset overrides this option.

## Update time travel windows

You can update a dataset's time travel window in the following ways:

  - Using the Google Cloud console.
  - Using the [`  ALTER SCHEMA SET OPTIONS  `](/bigquery/docs/reference/standard-sql/data-definition-language#alter_schema_set_options_statement) statement.
  - Using the bq command-line tool's [`  bq update  `](/bigquery/docs/reference/bq-cli-reference#bq_update) command.
  - Calling the [`  datasets.patch  `](/bigquery/docs/reference/rest/v2/datasets/patch) or [`  datasets.update  `](/bigquery/docs/reference/rest/v2/datasets/update) API method. The `  update  ` method replaces the entire dataset resource, whereas the `  patch  ` method only replaces fields that are provided in the submitted dataset resource.

For more information on the time travel window, see [Configure the time travel window](/bigquery/docs/time-travel#configure_the_time_travel_window) .

To update the time travel window for a dataset:

### Console

1.  In the left pane, click explore **Explorer** :

2.  In the **Explorer** pane, expand your project, click **Datasets** , and then click a dataset.

3.  In the **Details** tab, click mode\_edit **Edit details** .

4.  Expand **Advanced options** , then select the **Time travel window** to use.

5.  Click **Save** .

### SQL

Use the [`  ALTER SCHEMA SET OPTIONS  `](/bigquery/docs/reference/standard-sql/data-definition-language#alter_schema_set_options_statement) statement with the `  max_time_travel_hours  ` option to specify the time travel window when altering a dataset. The `  max_time_travel_hours  ` value must be an integer expressed in multiples of 24 (48, 72, 96, 120, 144, 168) between 48 (2 days) and 168 (7 days).

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
    ALTER SCHEMA DATASET_NAME
    SET OPTIONS(
      max_time_travel_hours = HOURS);
    ```
    
    Replace the following:
    
      - `  DATASET_NAME  ` : the name of the dataset that you're updating
      - `  HOURS  ` with the time travel window's duration in hours.

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](/bigquery/docs/running-queries#queries) .

### bq

Use the [`  bq update  `](/bigquery/docs/reference/bq-cli-reference#bq_update) command with the `  --max_time_travel_hours  ` flag to specify the time travel window when altering a dataset. The `  --max_time_travel_hours  ` value must be an integer expressed in multiples of 24 (48, 72, 96, 120, 144, 168) between 48 (2 days) and 168 (7 days).

``` text
bq update \
--dataset=true --max_time_travel_hours=HOURS \
PROJECT_ID:DATASET_NAME
```

Replace the following:

  - `  PROJECT_ID  ` : your project ID
  - `  DATASET_NAME  ` : the name of the dataset that you're updating
  - `  HOURS  ` with the time travel window's duration in hours

### API

Call the [`  datasets.patch  `](/bigquery/docs/reference/rest/v2/datasets/patch) or [`  datasets.update  `](/bigquery/docs/reference/rest/v2/datasets/update) method with a defined [dataset resource](/bigquery/docs/reference/rest/v2/datasets) in which you have specified a value for the `  maxTimeTravelHours  ` field. The `  maxTimeTravelHours  ` value must be an integer expressed in multiples of 24 (48, 72, 96, 120, 144, 168) between 48 (2 days) and 168 (7 days).

## Update storage billing models

You can alter the [storage billing model](/bigquery/docs/datasets-intro#dataset_storage_billing_models) for a dataset. Set the `  storage_billing_model  ` value to `  PHYSICAL  ` to use physical bytes when calculating storage changes, or to `  LOGICAL  ` to use logical bytes. `  LOGICAL  ` is the default.

When you change a dataset's billing model, it takes 24 hours for the change to take effect.

Once you change a dataset's storage billing model, you must wait 14 days before you can change the storage billing model again.

### Console

1.  In the left pane, click explore **Explorer** :

2.  In the **Explorer** pane, expand your project, click **Datasets** , and then click a dataset.

3.  In the **Details** tab, click mode\_edit **Edit details** .

4.  Expand **Advanced options** .

5.  In the **Storage billing model** menu, select **Physical** to use physical storage billing, or select **Logical** to use logical storage billing. You can also select **Storage\_billing\_model\_unspecified** .

6.  Click **Save** .

### SQL

To update the billing model for a dataset, use the [`  ALTER SCHEMA SET OPTIONS  ` statement](/bigquery/docs/reference/standard-sql/data-definition-language#alter_schema_set_options_statement) and set the `  storage_billing_model  ` option:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
    ALTER SCHEMA DATASET_NAME
    SET OPTIONS(
     storage_billing_model = 'BILLING_MODEL');
    ```
    
    Replace the following:
    
      - `  DATASET_NAME  ` with the name of the dataset that you are changing
      - `  BILLING_MODEL  ` with the type of storage you want to use, either `  LOGICAL  ` or `  PHYSICAL  `

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](/bigquery/docs/running-queries#queries) .

To update the storage billing model for all datasets in a project, use the following SQL query for every region, where datasets are located:

``` text
FOR record IN
 (SELECT CONCAT(catalog_name, '.', schema_name) AS dataset_path
 FROM PROJECT_ID.region-REGION.INFORMATION_SCHEMA.SCHEMATA)
DO
 EXECUTE IMMEDIATE
   "ALTER SCHEMA `" || record.dataset_path || "` SET OPTIONS(storage_billing_model = 'BILLING_MODEL')";
END FOR;
```

Replace the following:

  - `  PROJECT_ID  ` with your project ID
  - `  REGION  ` with a [region qualifier](/bigquery/docs/information-schema-intro#region_qualifier)
  - `  BILLING_MODEL  ` with the type of storage you want to use, either `  LOGICAL  ` or `  PHYSICAL  `

### bq

To update the billing model for a dataset, use the [`  bq update  ` command](/bigquery/docs/reference/bq-cli-reference#bq_update) and set the `  --storage_billing_model  ` flag:

``` text
bq update -d --storage_billing_model=BILLING_MODEL PROJECT_ID:DATASET_NAME
```

Replace the following:

  - `  PROJECT_ID  ` : your project ID
  - `  DATASET_NAME  ` : the name of the dataset that you're updating
  - `  BILLING_MODEL  ` : the type of storage you want to use, either `  LOGICAL  ` or `  PHYSICAL  `

### API

Call the [`  datasets.update  ` method](/bigquery/docs/reference/rest/v2/datasets/update) with a defined [dataset resource](/bigquery/docs/reference/rest/v2/datasets) where the `  storageBillingModel  ` field is set.

The following example shows how to call `  datasets.update  ` using `  curl  ` :

``` text
curl -H "Authorization: Bearer $(gcloud auth print-access-token)" -H "Content-Type: application/json" -L -X PUT https://bigquery.googleapis.com/bigquery/v2/projects/PROJECT_ID/datasets/DATASET_ID -d '{"datasetReference": {"projectId": "PROJECT_ID", "datasetId": "DATASET_NAME"}, "storageBillingModel": "BILLING_MODEL"}'
```

Replace the following:

  - `  PROJECT_ID  ` : your project ID
  - `  DATASET_NAME  ` : the name of the dataset that you're updating
  - `  BILLING_MODEL  ` : the type of storage you want to use, either `  LOGICAL  ` or `  PHYSICAL  `

## Update access controls

To control access to datasets in BigQuery, see [Controlling access to datasets](/bigquery/docs/control-access-to-resources-iam) . For information about data encryption, see [Encryption at rest](/bigquery/docs/encryption-at-rest) .

## What's next

  - For more information about creating datasets, see [Creating datasets](/bigquery/docs/datasets) .
  - For more information about managing datasets, see [Managing datasets](/bigquery/docs/managing-datasets) .
