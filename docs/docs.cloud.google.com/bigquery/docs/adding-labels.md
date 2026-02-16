# Adding labels to resources

This page explains how to label your BigQuery resources.

## Before you begin

Grant Identity and Access Management (IAM) roles that give users the necessary permissions to perform each task in this document. Any permissions required to perform a task are listed in the "Required IAM roles" section of the task.

## Add labels to datasets

A label can be added to a BigQuery dataset when it is created by using the bq command-line tool's `  bq mk  ` command or by calling the [`  datasets.insert  `](/bigquery/docs/reference/rest/v2/datasets/insert) API method. You cannot add a label to a dataset when it's created using the Google Cloud console.

This page discusses how to add a label to a dataset after it is created. For more information on adding a label when you create a dataset, see [Creating a dataset](/bigquery/docs/datasets) .

When you add a label to a dataset, it does not propagate to resources within the dataset. Dataset labels are not inherited by tables or views. Also, when you add a label to a dataset, it is included in your storage billing data, but not in your job-related billing data.

For more details on the format of a label, see [Requirements for labels](/bigquery/docs/labels-intro#requirements) .

### Required IAM roles

To get the permission that you need to add a label to an existing dataset, ask your administrator to grant you the [BigQuery Data Owner](/iam/docs/roles-permissions/bigquery#bigquery.dataOwner) ( `  roles/bigquery.dataOwner  ` ) IAM role. For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

This predefined role contains the `  bigquery.datasets.update  ` permission, which is required to add a label to an existing dataset.

You might also be able to get this permission with [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

For more information on IAM roles and permissions in BigQuery, see [Predefined roles and permissions](/bigquery/docs/access-control) .

### Add a label to a dataset

To add a label to a dataset after it is created:

### Console

1.  In the Google Cloud console, select the dataset.

2.  On the dataset details page, click the pencil icon to the right of **Labels** .

3.  In the **Edit labels** dialog:
    
      - Click **Add label**
      - Enter the key and value. To apply additional labels, click **Add label** . Each key can be used only once per dataset, but you can use the same key in different datasets in the same project.
      - To update a label, modify the existing keys or values.
      - To save your changes, click **Update** .

### SQL

Use the [`  ALTER SCHEMA SET OPTIONS  ` DDL statement](/bigquery/docs/reference/standard-sql/data-definition-language#alter_schema_set_options_statement) to set the labels on an existing dataset. Setting labels overwrites any existing labels on the dataset. The following example sets a label on the dataset `  mydataset  ` :

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
    ALTER SCHEMA mydataset
    SET OPTIONS (
      labels = [('sensitivity', 'high')]);
    ```

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](/bigquery/docs/running-queries#queries) .

### bq

To add a label to an existing dataset, issue the `  bq update  ` command with the `  set_label  ` flag. Repeat the flag to add multiple labels.

If the dataset is in a project other than your default project, add the project ID to the dataset in the following format: `  PROJECT_ID:DATASET  ` .

``` text
bq update --set_label KEY:VALUE PROJECT_ID:DATASET
```

Replace the following:

  - `  KEY:VALUE  ` : a key-value pair for a label that you want to add. The key must be unique. Keys and values can contain only lowercase letters, numeric characters, underscores, and dashes. All characters must use UTF-8 encoding, and international characters are allowed.
  - `  PROJECT_ID  ` : your project ID.
  - `  DATASET  ` : the dataset you're labeling.

Examples:

To add a label to track departments, enter the `  bq update  ` command and specify `  department  ` as the label key. For example, to add a `  department:shipping  ` label to `  mydataset  ` in your default project, enter:

``` text
    bq update --set_label department:shipping mydataset
```

To add multiple labels to a dataset, repeat the `  set_label  ` flag and specify a unique key for each label. For example, to add a `  department:shipping  ` label and `  cost_center:logistics  ` label to `  mydataset  ` in your default project, enter:

``` text
    bq update \
    --set_label department:shipping \
    --set_label cost_center:logistics \
    mydataset
```

### API

To add a label to an existing dataset, call the [`  datasets.patch  `](/bigquery/docs/reference/rest/v2/datasets/patch) method and populate the `  labels  ` property for the [dataset resource](/bigquery/docs/reference/rest/v2/datasets) .

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

  public static void main(String[] args) {
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

## Add labels to tables and views

This page discusses how to add a label to an existing table or view. For more information on adding a label when you create a table or view, see [Creating a table](/bigquery/docs/tables) or [Creating a view](/bigquery/docs/views) .

Because views are treated like table resources, you use the `  tables.patch  ` method to modify both views and tables.

**Note:** Table and view labels are not included in billing data.

### Required IAM roles

To get the permissions that you need to add a label to an existing table or view, ask your administrator to grant you the [BigQuery Data Editor](/iam/docs/roles-permissions/bigquery#bigquery.dataEditor) ( `  roles/bigquery.dataEditor  ` ) IAM role. For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

This predefined role contains the permissions required to add a label to an existing table or view. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

The following permissions are required to add a label to an existing table or view:

  - `  bigquery.tables.update  `
  - `  bigquery.tables.get  `

You might also be able to get these permissions with [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

For more information on IAM roles and permissions in BigQuery, see [Predefined roles and permissions](/bigquery/docs/access-control) .

### Add a label to a table or view

To add a label to an existing table or view:

### Console

1.  In the Google Cloud console, select the table, or view.

2.  Click the **Details** tab.

3.  Click the pencil icon to the right of **Labels** .

4.  In the **Edit labels** dialog:
    
      - Click **Add label**
      - Enter your key and value to add a label. To apply additional labels, click **Add label** . Each key can be used only once per dataset, but you can use the same key in different datasets in the same project.
      - Modify existing keys or values to update a label.
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

To add a label to an existing table or view, issue the `  bq update  ` command with the `  set_label  ` flag. To add multiple labels, repeat the flag.

If the table or view is in a project other than your default project, add the project ID to the dataset in the following format: `  project_id:dataset  ` .

``` text
bq update \
--set_label KEY:VALUE \
PROJECT_ID:DATASET.TABLE_OR_VIEW
```

Replace the following:

  - `  KEY:VALUE  ` : a key-value pair for a label that you want to add. The key must be unique. Keys and values can contain only lowercase letters, numeric characters, underscores, and dashes. All characters must use UTF-8 encoding, and international characters are allowed.
  - `  PROJECT_ID  ` : your project ID.
  - `  DATASET  ` : the dataset that contains the table or view you're labeling.
  - `  TABLE_OR_VIEW  ` : the name of the table or view you're labeling.

Examples:

To add a table label that tracks departments, enter the `  bq update  ` command and specify `  department  ` as the label key. For example, to add a `  department:shipping  ` label to `  mytable  ` in your default project, enter:

``` text
    bq update --set_label department:shipping mydataset.mytable
```

To add a view label that tracks departments, enter the `  bq update  ` command and specify `  department  ` as the label key. For example, to add a `  department:shipping  ` label to `  myview  ` in your default project, enter:

``` text
    bq update --set_label department:shipping mydataset.myview
```

To add multiple labels to a table or view, repeat the `  set_label  ` flag and specify a unique key for each label. For example, to add a `  department:shipping  ` label and `  cost_center:logistics  ` label to `  mytable  ` in your default project, enter:

``` text
    bq update \
    --set_label department:shipping \
    --set_label cost_center:logistics \
    mydataset.mytable
```

### API

To add a label to an existing table or view, call the [`  tables.patch  `](/bigquery/docs/reference/rest/v2/tables/patch) method and populate the `  labels  ` property for the [table resource](/bigquery/docs/reference/rest/v2/tables) .

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

  public static void main(String[] args) {
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
from google.cloud import bigquery

client = bigquery.Client()

# TODO(dev): Change table_id to the full name of the table you want to create.
table_id = "your-project.your_dataset.your_table_name"

table = client.get_table(table_id)  # API request

labels = {"color": "green"}
table.labels = labels

table = client.update_table(table, ["labels"])  # API request

print(f"Added {table.labels} to {table_id}.")
```

## Add labels to jobs

Labels can be added to query jobs through the command line by using the bq command-line tool's `  --label  ` flag. The bq tool supports adding labels only to query jobs.

You can also add a label to a job when it's submitted through the API by specifying the `  labels  ` property in the job configuration when you call the [`  jobs.insert  `](/bigquery/docs/reference/rest/v2/jobs/insert) method. The API can be used to add labels to any job type.

You cannot add labels to or update labels on pending, running, or completed jobs.

When you add a label to a job, the label is included in your billing data.

### Required IAM roles

To get the permission that you need to add a label to a job, ask your administrator to grant you the [BigQuery User](/iam/docs/roles-permissions/bigquery#bigquery.user) ( `  roles/bigquery.user  ` ) IAM role. For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

This predefined role contains the `  bigquery.jobs.create  ` permission, which is required to add a label to a job.

You might also be able to get this permission with [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

For more information on IAM roles and permissions in BigQuery, see [Predefined roles and permissions](/bigquery/docs/access-control) .

### Add a label to a job

To add a label to a job:

### bq

To add a label to a query job, issue the `  bq query  ` command with the `  --label  ` flag. To add multiple labels, repeat the flag. The flag indicates that your query is in GoogleSQL syntax.

``` text
bq query --label KEY:VALUE  'QUERY'
```

Replace the following:

  - `  KEY:VALUE  ` : a key-value pair for a label that you want to add to the query job. The key must be unique. Keys and values can contain only lowercase letters, numeric characters, underscores, and dashes. All characters must use UTF-8 encoding, and international characters are allowed. To add multiple labels to a query job, repeat the `  --label  ` flag and specify a unique key for each label.
  - `  QUERY  ` : a valid GoogleSQL query.

Examples:

To add a label to a query job, enter:

``` text
    bq query \
    --label department:shipping \
     \
    'SELECT
       column1, column2
     FROM
       `mydataset.mytable`'
```

To add multiple labels to a query job, repeat the `  --label  ` flag and specify a unique key for each label. For example, to add a `  department:shipping  ` label and `  cost_center:logistics  ` label to a query job, enter:

``` text
    bq query \
    --label department:shipping \
    --label cost_center:logistics \
     \
    'SELECT
       column1, column2
     FROM
       `mydataset.mytable`'
```

### API

To add a label to a job, call the [`  jobs.insert  `](/bigquery/docs/reference/rest/v2/jobs/insert) method and populate the `  labels  ` property for the [job configuration](/bigquery/docs/reference/rest/v2/Job#jobconfiguration) . You can use the API to add labels to any job type.

### Python

Before trying this sample, follow the Python setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Python API reference documentation](/python/docs/reference/bigquery/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` python
from google.cloud import bigquery

client = bigquery.Client()

sql = """
    SELECT corpus
    FROM `bigquery-public-data.samples.shakespeare`
    GROUP BY corpus;
"""
labels = {"color": "green"}

config = bigquery.QueryJobConfig()
config.labels = labels
location = "us"
job = client.query(sql, location=location, job_config=config)
job_id = job.job_id

print(f"Added {job.labels} to {job_id}.")
```

### Associate jobs in a session with a label

If you are running queries in a [session](/bigquery/docs/sessions-intro) , you can assign a label to all future query jobs in the session using BigQuery multi-statement queries.

### SQL

Set the [`  @@query_label  `](/bigquery/docs/reference/system-variables) system variable in the session by running this query:

``` text
  SET @@query_label = "KEY:VALUE";
  
```

  - KEY:VALUE : a key-value pair for the label to assign to all future queries in the session. You can also add multiple key-value pairs, separated by a comma (for example, `  SET @@query_label = "key1:value1,key2:value2"  ` ). The key must be unique. Keys and values can contain only lowercase letters, numeric characters, underscores, and dashes. All characters must use UTF-8 encoding, and international characters are allowed.

Example:

``` text
  SET @@query_label = "cost_center:logistics";
  
```

### API

To add a label to a query job in a session when you [run a query using an API call](/bigquery/docs/sessions#run-queries) , call the [`  jobs.insert  `](/bigquery/docs/reference/rest/v2/jobs/insert) method and populate the `  query_label  ` property for the [`  connectionProperties  `](/bigquery/docs/reference/rest/v2/ConnectionProperty) [job configuration](/bigquery/docs/reference/rest/v2/Job#jobconfiguration) .

After you have associated a query label with a session and run queries inside the session, you can collect audit logs for queries with that query label. For more information, see the [Audit log reference for BigQuery](/bigquery/docs/reference/auditlogs) .

## Add a label to a reservation

When you add a label to a reservation, the label is included in your billing data. You can use the labels to filter the Analysis Slots Attribution SKU in your Cloud Billing data.

The Analysis Slots Attribution SKU only records slot usage. It doesn't record costs for BigQuery Reservation API SKUs. Reservation labels aren't supported as filters for BigQuery Reservation API SKUs.

For more information about using labels in your billing data, see [Use **Filters** to refine data](/billing/docs/how-to/reports#filter-by-labels) .

### Required IAM roles

To get the permission that you need to add a label to a reservation, ask your administrator to grant you the [BigQuery Resource Editor](/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor) ( `  roles/bigquery.resourceEditor  ` ) IAM role on the administration project. For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

This predefined role contains the `  bigquery.reservations.update  ` permission, which is required to add a label to a reservation.

You might also be able to get this permission with [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

### Add a label to a reservation

To add a label to a reservation:

### Console

1.  In the Google Cloud console, go to the BigQuery page.

2.  In the navigation menu, click **Capacity management** .

3.  Click the **Slot reservations** tab.

4.  Find the reservation you want to update.

5.  Expand the more\_vert **Actions** option.

6.  Click **Edit** .

7.  To expand the **Advanced settings** section, click the expand\_more expander arrow.

8.  Click **Add Label** .

9.  Enter the key-value pair. To apply additional labels, click **Add label** .

10. Click **Save** .

### SQL

To add a label to a reservation, use the [`  ALTER RESERVATION SET OPTIONS  ` DDL statement](/bigquery/docs/reference/standard-sql/data-definition-language#alter_reservation_set_options_statement) . Setting labels overwrites any existing labels on the reservation. The following example sets a label on the reservation `  myreservation  ` :

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
    ALTER RESERVATION myreservation
    SET OPTIONS (
      labels = [('sensitivity', 'high')]);
    ```

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](/bigquery/docs/running-queries#queries) .

### bq

To add a label to a reservation, issue the `  bq update  ` command with the `  set_label  ` flag and the `  --reservation  ` flag. To add multiple labels, repeat the `  set_label  ` flag.

``` text
bq update --set_label KEY:VALUE --location LOCATION --reservation RESERVATION_NAME
```

Replace the following:

  - `  KEY:VALUE  ` : a key-value pair for a label that you want to add to the reservation. The key must be unique. Keys and values can contain only lowercase letters, numeric characters, underscores, and dashes. All characters must use UTF-8 encoding, and international characters are allowed. To add multiple labels to a reservation, repeat the `  --set_label  ` flag and specify a unique key for each label.
  - `  LOCATION  ` : the location of the reservation. The `  location  ` flag can't be last in the command, otherwise the `  FATAL Flags positioning  ` error is returned.
  - `  RESERVATION_NAME  ` : the name of the reservation.

## Add a label without a value

A label that has a key with an empty value is sometimes called a tag. This shouldn't be confused with a [tag resource](/bigquery/docs/tags) . For more information, see [labels and tags](/resource-manager/docs/tags/tags-overview) . You can create a new label with no value, or you can remove a value from an existing label key.

Labels without values can be useful in situations where you are labeling a resource, but you don't need the key-value format. For example, if a table contains test data that is used by multiple groups, such as support or development, you can add a `  test_data  ` label to the table to identify it.

To add a label without a value:

### Console

1.  In the Google Cloud console, select the appropriate resource (a dataset, table, or view).

2.  For datasets, the dataset details page is automatically opened. For tables and views, click **Details** to open the details page.

3.  On the details page, click the pencil icon to the right of **Labels** .

4.  In the **Edit labels** dialog:
    
      - Click **Add label** .
      - Enter a new key and leave the value blank. To apply additional labels, click **Add label** and repeat.
      - To save your changes, click **Update** .

### SQL

To add a label without a value, use the [`  ALTER TABLE SET OPTIONS  ` DDL statement](/bigquery/docs/reference/standard-sql/data-definition-language#alter_table_set_options_statement) :

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
    ALTER TABLE mydataset.mytable
    SET OPTIONS (
      labels=[("key1", ""), ("key2", "")]);
    ```

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](/bigquery/docs/running-queries#queries) .

### bq

To add a label without a value to an existing resource, use the `  bq update  ` command with the `  set_label  ` flag. Specify the key, followed by a colon, but leave the value unspecified.

``` text
bq update --set_label KEY: RESOURCE_ID
```

Replace the following:

  - `  KEY:  ` : the label key that you want to use.
  - `  RESOURCE_ID  ` : a valid dataset, table, or view name. If the resource is in a project other than your default project, add the project ID in the following format: `  PROJECT_ID:DATASET  ` .

Examples:

Enter the following command to create a `  test_data  ` label for `  mydataset.mytable  ` . `  mydataset  ` is in your default project.

``` text
bq update --set_label test_data: mydataset
```

### API

Call the [`  datasets.patch  `](/bigquery/docs/reference/rest/v2/datasets/patch) method or the [`  tables.patch  `](/bigquery/docs/reference/rest/v2/tables/patch) method and add labels with the value set to the empty string ( `  ""  ` ) in the [dataset resource](/bigquery/docs/reference/rest/v2/datasets) or the [table resource](/bigquery/docs/reference/rest/v2/tables) . You can remove values from existing labels by replacing their values with the empty string.

Because views are treated like table resources, you use the `  tables.patch  ` method to modify both views and tables. Also, because the `  tables.update  ` method replaces the entire dataset resource, the `  tables.patch  ` method is preferred.

## What's next

  - Learn how to [view labels](/bigquery/docs/viewing-labels) on BigQuery resources.
  - Learn how to [update labels](/bigquery/docs/updating-labels) on BigQuery resources.
  - Learn how to [filter resources using labels](/bigquery/docs/filtering-labels) .
  - Learn how to [delete labels](/bigquery/docs/deleting-labels) on BigQuery resources.
  - Read about [Using labels](/resource-manager/docs/using-labels) in the Resource Manager documentation.
