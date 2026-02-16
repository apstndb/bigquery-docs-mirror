# Updating labels

This page explains how to update labels on BigQuery resources.

## Before you begin

Grant Identity and Access Management (IAM) roles that give users the necessary permissions to perform each task in this document. The permissions required to perform a task (if any) are listed in the "Required permissions" section of the task.

## Update dataset labels

A dataset label can be updated by:

  - Using the Google Cloud console
  - Using SQL [DDL statements](/bigquery/docs/reference/standard-sql/data-definition-language)
  - Using the bq command-line tool's `  bq update  ` command
  - Calling the [`  datasets.patch  `](/bigquery/docs/reference/rest/v2/datasets/patch) API method
  - Using the client libraries

### Required permissions

To update a dataset label, you need the `  bigquery.datasets.update  ` IAM permission.

Each of the following predefined IAM roles includes the permissions that you need in order to update a dataset label:

  - `  roles/bigquery.dataOwner  `
  - `  roles/bigquery.admin  `

Additionally, if you have the `  bigquery.datasets.create  ` permission, you can update labels of the datasets that you create.

For more information on IAM roles and permissions in BigQuery, see [Predefined roles and permissions](/bigquery/docs/access-control) .

### Update a dataset label

To update labels on a dataset, select one of the following options:

### Console

1.  In the Google Cloud console, select the dataset.

2.  On the dataset details page, click the pencil icon to the right of **Labels** .

3.  In the **Edit labels** dialog:
    
      - To apply additional labels, click **Add label** . Each key can be used only once per dataset, but you can use the same key in different datasets in the same project.
      - Modify the existing keys or values to update a label.
      - Click **Update** to save your changes.

### SQL

Use the [`  ALTER SCHEMA SET OPTIONS  ` DDL statement](/bigquery/docs/reference/standard-sql/data-definition-language#alter_schema_set_options_statement) to set the labels on an existing dataset. Setting labels overwrites any existing labels on the dataset. The following example sets a single label on the dataset `  mydataset  ` :

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
    ALTER SCHEMA mydataset
    SET OPTIONS (labels = [('sensitivity', 'high')]);
    ```

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](/bigquery/docs/running-queries#queries) .

### bq

To add additional labels or to update a dataset label, issue the `  bq update  ` command with the `  set_label  ` flag. Repeat the flag to add or update multiple labels.

If the dataset is in a project other than your default project, add the project ID to the dataset in the following format: `  [PROJECT_ID]:[DATASET]  ` .

``` text
bq update \
--set_label key:value \
project_id:dataset
```

Where:

  - key:value corresponds to a key:value pair for a label that you want to add or update. If you specify the same key as an existing label, the value for the existing label is updated. The key must be unique.
  - project\_id is your project ID.
  - dataset is the dataset you're updating.

Example:

To update the `  department  ` label on `  mydataset  ` , enter the `  bq update  ` command and specify `  department  ` as the label key. For example, to update the `  department:shipping  ` label to `  department:logistics  ` , enter the following command. `  mydataset  ` is in `  myotherproject  ` , not your default project.

``` text
    bq update \
    --set_label department:logistics \
    myotherproject:mydataset
```

The output looks like the following.

``` text
Dataset 'myotherproject:mydataset' successfully updated.
```

### API

To add additional labels or to update a label for an existing dataset, call the [`  datasets.patch  `](/bigquery/docs/reference/rest/v2/datasets/patch) method and add to or update the `  labels  ` property for the [dataset resource](/bigquery/docs/reference/rest/v2/datasets) .

Because the `  datasets.update  ` method replaces the entire dataset resource, the `  datasets.patch  ` method is preferred.

### Go

Before trying this sample, follow the Go setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Go API reference documentation](https://godoc.org/cloud.google.com/go/bigquery) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` go
import (
 "context"
 "fmt"

 "cloud.google.com/go/bigquery"
)

// addDatasetLabel demonstrates adding label metadata to an existing dataset.
func addDatasetLabel(projectID, datasetID string) error {
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

 update := bigquery.DatasetMetadataToUpdate{}
 update.SetLabel("color", "green")
 if _, err := ds.Update(ctx, update, meta.ETag); err != nil {
     return err
 }
 return nil
}
```

### Java

This sample uses the [Google HTTP Client Library for Java](https://developers.google.com/api-client-library/java/google-http-java-client/) to send a request to the BigQuery API.

Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Java API reference documentation](/java/docs/reference/google-cloud-bigquery/latest/overview) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` java
import com.google.cloud.bigquery.BigQuery;
import com.google.cloud.bigquery.BigQueryException;
import com.google.cloud.bigquery.BigQueryOptions;
import com.google.cloud.bigquery.Dataset;
import java.util.HashMap;
import java.util.Map;

// Sample to updates a label on dataset
public class LabelDataset {

  public static void runLabelDataset() {
    // TODO(developer): Replace these variables before running the sample.
    String datasetName = "MY_DATASET_NAME";
    labelDataset(datasetName);
  }

  public static void labelDataset(String datasetName) {
    try {
      // Initialize client that will be used to send requests. This client only needs to be created
      // once, and can be reused for multiple requests.
      BigQuery bigquery = BigQueryOptions.getDefaultInstance().getService();

      // This example dataset starts with existing label { color: 'green' }
      Dataset dataset = bigquery.getDataset(datasetName);
      // Add label to dataset
      Map<String, String> labels = new HashMap<>();
      labels.put("color", "green");

      dataset.toBuilder().setLabels(labels).build().update();
      System.out.println("Label added successfully");
    } catch (BigQueryException e) {
      System.out.println("Label was not added. \n" + e.toString());
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

async function labelDataset() {
  // Updates a label on a dataset.

  /**
   * TODO(developer): Uncomment the following lines before running the sample
   */
  // const datasetId = "my_dataset";

  // Retrieve current dataset metadata.
  const dataset = bigquery.dataset(datasetId);
  const [metadata] = await dataset.getMetadata();

  // Add label to dataset metadata
  metadata.labels = {color: 'green'};
  const [apiResponse] = await dataset.setMetadata(metadata);

  console.log(`${datasetId} labels:`);
  console.log(apiResponse.labels);
}
```

### Python

Before trying this sample, follow the Python setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Python API reference documentation](/python/docs/reference/bigquery/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` python
from google.cloud import bigquery

# Construct a BigQuery client object.
client = bigquery.Client()

# TODO(developer): Set dataset_id to the ID of the dataset to fetch.
# dataset_id = "your-project.your_dataset"

dataset = client.get_dataset(dataset_id)  # Make an API request.
dataset.labels = {"color": "green"}
dataset = client.update_dataset(dataset, ["labels"])  # Make an API request.

print("Labels added to {}".format(dataset_id))
```

## Update table and view labels

A label can be updated after a table or view is created by:

  - Using the Google Cloud console
  - Using the bq command-line tool's `  bq update  ` command
  - Calling the [`  tables.patch  `](/bigquery/docs/reference/rest/v2/tables/patch) API method
      - Because views are treated like table resources, you use the `  tables.patch  ` method to modify both views and tables.
  - Using the client libraries

### Required permissions

To update a table or view label, you need the `  bigquery.tables.update  ` IAM permission.

Each of the following predefined IAM roles includes the permissions that you need in order to update a table or view label:

  - `  roles/bigquery.dataEditor  `
  - `  roles/bigquery.dataOwner  `
  - `  roles/bigquery.admin  `

Additionally, if you have the `  bigquery.datasets.create  ` permission, you can update labels of the tables and views in the datasets that you create.

For more information on IAM roles and permissions in BigQuery, see [Predefined roles and permissions](/bigquery/docs/access-control) .

### Update a table or view label

To update a table or view label:

### Console

1.  In the Google Cloud console, select the table or view.

2.  Click the **Details** tab, and then click the pencil icon to the right of **Labels** .

3.  In the **Edit labels** dialog:
    
      - To apply additional labels, click **Add label** . Each key can be used only once per table or view, but you can use the same key in tables or views in different datasets.
      - Modify the existing keys or values to update a label.
      - Click **Update** to save your changes.

### SQL

Use the [`  ALTER TABLE SET OPTIONS  ` DDL statement](/bigquery/docs/reference/standard-sql/data-definition-language#alter_table_set_options_statement) to set the labels on an existing table, or the [`  ALTER VIEW SET OPTIONS  ` DDL statement](/bigquery/docs/reference/standard-sql/data-definition-language#alter_view_set_options_statement) to set the labels on an existing view. Setting labels overwrites any existing labels on the table or view. The following example sets two labels on the table `  mytable  ` :

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
    ALTER TABLE mydataset.mytable
    SET OPTIONS (
      labels = [('department', 'shipping'), ('cost_center', 'logistics')]);
    ```

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](/bigquery/docs/running-queries#queries) .

### bq

To add additional labels or to update a table or view label, issue the `  bq update  ` command with the `  set_label  ` flag. Repeat the flag to add or update multiple labels.

If the table or view is in a project other than your default project, add the project ID to the dataset in the following format: `  project_id:dataset  ` .

``` text
bq update \
--set_label key:value \
project_id:dataset.table_or_view
```

Where:

  - key:value corresponds to a key:value pair for a label that you want to add or update. If you specify the same key as an existing label, the value for the existing label is updated. The key must be unique.
  - project\_id is your project ID.
  - dataset is the dataset that contains the table or view you're updating.
  - table\_or\_view is the name of the table or view you're updating.

Example:

To update the `  department  ` label for `  mytable  ` , enter the `  bq update  ` command and specify `  department  ` as the label key. For example, to update the `  department:shipping  ` label to `  department:logistics  ` for `  mytable  ` , enter the following command. `  mytable  ` is in `  myotherproject  ` , not your default project.

``` text
    bq update \
    --set_label department:logistics \
    myotherproject:mydataset.mytable
```

The output looks like the following:

``` text
Table 'myotherproject:mydataset.mytable' successfully updated.
```

### API

To add labels or to update a label for an existing table or view, call the [`  tables.patch  `](/bigquery/docs/reference/rest/v2/tables/patch) method and add to or update the `  labels  ` property for the [table resource](/bigquery/docs/reference/rest/v2/tables) .

Because views are treated like table resources, you use the `  tables.patch  ` method to modify both views and tables.

Because the `  tables.update  ` method replaces the entire dataset resource, the `  tables.patch  ` method is preferred.

### Go

Before trying this sample, follow the Go setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Go API reference documentation](https://godoc.org/cloud.google.com/go/bigquery) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` go
import (
 "context"
 "fmt"

 "cloud.google.com/go/bigquery"
)

// addTableLabel demonstrates adding Label metadata to a BigQuery table.
func addTableLabel(projectID, datasetID, tableID string) error {
 // projectID := "my-project-id"
 // datasetID := "mydataset"
 // tableID := "mytable"
 ctx := context.Background()
 client, err := bigquery.NewClient(ctx, projectID)
 if err != nil {
     return fmt.Errorf("bigquery.NewClient: %v", err)
 }
 defer client.Close()

 tbl := client.Dataset(datasetID).Table(tableID)
 meta, err := tbl.Metadata(ctx)
 if err != nil {
     return err
 }

 update := bigquery.TableMetadataToUpdate{}
 update.SetLabel("color", "green")
 if _, err := tbl.Update(ctx, update, meta.ETag); err != nil {
     return err
 }
 return nil
}
```

### Java

This sample uses the [Google HTTP Client Library for Java](https://developers.google.com/api-client-library/java/google-http-java-client/) to send a request to the BigQuery API.

Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Java API reference documentation](/java/docs/reference/google-cloud-bigquery/latest/overview) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` java
import com.google.cloud.bigquery.BigQuery;
import com.google.cloud.bigquery.BigQueryException;
import com.google.cloud.bigquery.BigQueryOptions;
import com.google.cloud.bigquery.Table;
import com.google.cloud.bigquery.TableId;
import java.util.HashMap;
import java.util.Map;

// Sample to adds a label to an existing table
public class LabelTable {

  public static void runLabelTable() {
    // TODO(developer): Replace these variables before running the sample.
    String datasetName = "MY_DATASET_NAME";
    String tableName = "MY_TABLE_NAME";
    labelTable(datasetName, tableName);
  }

  public static void labelTable(String datasetName, String tableName) {
    try {
      // Initialize client that will be used to send requests. This client only needs to be created
      // once, and can be reused for multiple requests.
      BigQuery bigquery = BigQueryOptions.getDefaultInstance().getService();

      // This example table starts with existing label { color: 'green' }
      Table table = bigquery.getTable(TableId.of(datasetName, tableName));
      // Add label to table
      Map<String, String> labels = new HashMap<>();
      labels.put("color", "green");

      table.toBuilder().setLabels(labels).build().update();
      System.out.println("Label added successfully");
    } catch (BigQueryException e) {
      System.out.println("Label was not added. \n" + e.toString());
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

async function labelTable() {
  // Adds a label to an existing table.

  /**
   * TODO(developer): Uncomment the following lines before running the sample.
   */
  // const datasetId = 'my_dataset';
  // const tableId = 'my_table';

  const dataset = bigquery.dataset(datasetId);
  const [table] = await dataset.table(tableId).get();

  // Retrieve current table metadata
  const [metadata] = await table.getMetadata();

  // Add label to table metadata
  metadata.labels = {color: 'green'};
  const [apiResponse] = await table.setMetadata(metadata);

  console.log(`${tableId} labels:`);
  console.log(apiResponse.labels);
}
```

### Python

Before trying this sample, follow the Python setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Python API reference documentation](/python/docs/reference/bigquery/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` python
# from google.cloud import bigquery
# client = bigquery.Client()
# project = client.project
# dataset_ref = bigquery.DatasetReference(project, dataset_id)
# table_ref = dataset_ref.table('my_table')
# table = client.get_table(table_ref)  # API request

assert table.labels == {}
labels = {"color": "green"}
table.labels = labels

table = client.update_table(table, ["labels"])  # API request

assert table.labels == labels
```

## Update job labels

Updating a job label is not supported. To update the label on a job, resubmit the job with a new label specified.

## Update reservation labels

You can update a label on a reservation. Updating a label using SQL overwrites any existing labels on the reservation.

### Required IAM roles

To get the permission that you need to update a label to a reservation, ask your administrator to grant you the [BigQuery Resource Editor](/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor) ( `  roles/bigquery.resourceEditor  ` ) IAM role on the administration project. For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

This predefined role contains the `  bigquery.reservations.update  ` permission, which is required to update a label to a reservation.

You might also be able to get this permission with [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

### Update a label on a reservation

To update a label to a reservation:

### Console

1.  In the Google Cloud console, go to the BigQuery page.

2.  In the navigation menu, click **Capacity management** .

3.  Click the **Slot reservations** tab.

4.  Find the reservation you want to update.

5.  Expand the more\_vert **Actions** option.

6.  Click **Edit** .

7.  To expand the **Advanced settings** section, click the expand\_more expander arrow.

8.  Update the names of the key-value pair.

9.  Click **Save** .

### bq

To update a label to a reservation, issue the `  bq update  ` command with the `  set_label  ` flag and `  --reservation  ` flag. To update multiple labels, repeat the flag.

``` text
bq update --set_label KEY:VALUE  --reservation RESERVATION_NAME
```

Replace the following:

  - `  KEY:VALUE  ` : a key-value pair for a label that you want to update on the reservation. The key must be unique. Keys and values can contain only lowercase letters, numeric characters, underscores, and dashes. All characters must use UTF-8 encoding, and international characters are allowed. To update multiple labels on a reservation, repeat the `  --label  ` flag and specify a unique key for each label.
  - `  RESERVATION_NAME  ` : the name of the reservation.

### SQL

To update a label to a reservation, use the [`  ALTER RESERVATION SET OPTIONS  ` DDL statement](/bigquery/docs/reference/standard-sql/data-definition-language#alter_reservation_set_options_statement) to set the labels on an existing reservation. Setting labels overwrites any existing labels on the reservation. The following example sets a label on the reservation `  myreservation  ` :

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
    ALTER RESERVATION myreservation
    SET OPTIONS (
      labels = [('sensitivity', 'high')]);
    ```

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](/bigquery/docs/running-queries#queries) .

## Convert labels to tags

A label that has a key with an empty value is used as a tag. You can create a new label with no value, or you can turn an existing label into a tag on a dataset, table, or view. You cannot convert a job label to a tag.

Tags can be useful in situations where you are labeling a resource, but you don't need the `  key:value  ` format. For example, if you have a table that contains test data that is used by multiple groups (support, development, and so on), you can add a `  test_data  ` tag to the table to identify it.

### Required permissions

To convert a label to a tag, you need the following IAM permissions:

  - `  bigquery.datasets.update  ` (lets you convert a dataset label)
  - `  bigquery.tables.update  ` (lets you convert a table or view label)

Each of the following predefined IAM roles includes the permissions that you need in order to convert a dataset label:

  - `  roles/bigquery.dataOwner  `
  - `  roles/bigquery.admin  `

Each of the following predefined IAM roles includes the permissions that you need in order to convert a table or view label:

  - `  roles/bigquery.dataEditor  `
  - `  roles/bigquery.dataOwner  `
  - `  roles/bigquery.admin  `

Additionally, if you have the `  bigquery.datasets.create  ` permission, you can update labels of the datasets that you create and the tables and views in those datasets.

For more information on IAM roles and permissions in BigQuery, see [Predefined roles and permissions](/bigquery/docs/access-control) .

### Convert a label to a tag

To convert a label to a tag:

### Console

1.  In the Google Cloud console, select the dataset, table, or view.

2.  For datasets, the dataset details page is automatically opened. For tables and views, click **Details** to open the details page.

3.  On the details page, click the pencil icon to the right of **Labels** .

4.  In the **Edit labels** dialog:
    
      - Delete the value for an existing label.
      - Click **Update** .

### bq

To convert a label to a tag, use the `  bq update  ` command with the `  set_label  ` flag. Specify the key, followed by a colon, but leave the value unspecified. This updates an existing label to a tag.

``` text
bq update \
--set_label key: \
resource_id
```

Where:

  - key: is the label key that you want update to a tag.
  - resource\_id is a valid dataset, table, or view name. If the resource is in a project other than your default project, add the project ID in the following format: `  project_id:dataset  ` .

Examples:

Enter the following command to change the existing `  test_data:development  ` label on `  mydataset  ` to a tag. `  mydataset  ` is in `  myotherproject  ` , not your default project.

``` text
bq update --set_label test_data: myotherproject:mydataset
```

The output looks like the following:

``` text
Dataset 'myotherproject:mydataset' successfully updated.
```

### API

To turn an existing label into a tag, call the [`  datasets.patch  `](/bigquery/docs/reference/rest/v2/datasets/patch) method or the [`  tables.patch  `](/bigquery/docs/reference/rest/v2/tables/patch) method and replace the label values with the empty string ( `  ""  ` ) in the [dataset resource](/bigquery/docs/reference/rest/v2/datasets) or the [table resource](/bigquery/docs/reference/rest/v2/tables) .

Because views are treated like table resources, you use the `  tables.patch  ` method to modify both views and tables. Also, because the `  tables.update  ` method replaces the entire dataset resource, the `  tables.patch  ` method is preferred.

## What's next

  - Learn how to [add labels](/bigquery/docs/adding-labels) to BigQuery resources.
  - Learn how to [view labels](/bigquery/docs/viewing-labels) on BigQuery resources.
  - Learn how to [filter resources using labels](/bigquery/docs/filtering-labels) .
  - Learn how to [delete labels](/bigquery/docs/deleting-labels) on BigQuery resources.
  - Read about [using labels](/resource-manager/docs/using-labels) in the Resource Manager documentation.
