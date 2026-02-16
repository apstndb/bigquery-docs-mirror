# Listing datasets

This document describes how to list and get information about datasets in BigQuery.

## Before you begin

Grant Identity and Access Management (IAM) roles that give users the necessary permissions to perform each task in this document.

### Required role

To get the permission that you need to list datasets or get information on datasets, ask your administrator to grant you the [BigQuery Metadata Viewer](/iam/docs/roles-permissions/bigquery#bigquery.metadataViewer) ( `  roles/bigquery.metadataViewer  ` ) IAM role on your project. For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

This predefined role contains the `  bigquery.datasets.get  ` permission, which is required to list datasets or get information on datasets.

You might also be able to get this permission with [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

When you apply the `  roles/bigquery.metadataViewer  ` role at the project or organization level, you can list all the datasets in the project. When you apply the `  roles/bigquery.metadataViewer  ` role at the dataset level, you can list all the datasets for which you have been granted that role.

## List datasets

Select one of the following options:

### Console

1.  In the navigation menu, click **Studio** .

2.  In the left pane, click explore **Explorer** :

3.  In the **Explorer** pane, expand a project, click **Datasets** to see the datasets in that project, and then click the name of your dataset. You can also use the search field or filters to find your dataset.

### SQL

Query the [`  INFORMATION_SCHEMA.SCHEMATA  ` view](/bigquery/docs/information-schema-datasets-schemata) :

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
    SELECT
      schema_name
    FROM
      PROJECT_ID.`region-REGION`.INFORMATION_SCHEMA.SCHEMATA;
    ```
    
    Replace the following:
    
      - `  PROJECT_ID  ` : the ID of your Google Cloud project. If not specified, the default project is used.
      - `  REGION  ` : any [dataset region name](/bigquery/docs/locations) . For example, `  us  ` .

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](/bigquery/docs/running-queries#queries) .

### bq

Issue the `  bq ls  ` command to list datasets by dataset ID. The `  --format  ` flag can be used to control the output. If you are listing dataset in a project other than your default project, add the `  --project_id  ` flag to the command.

To list all datasets in a project, including [hidden datasets](/bigquery/docs/datasets#hidden_datasets) , use the `  --all  ` flag or the `  -a  ` shortcut.

To list all datasets in a project, excluding hidden datasets, use the `  --datasets  ` flag or the `  -d  ` shortcut. This flag is optional. By default, hidden datasets are not listed.

Additional flags include:

  - `  --filter  ` : List datasets that match the filter expression. Use a space-separated list of label keys and values in the form `  labels. key:value  ` . For more information on filtering datasets using labels, see [Adding and using labels](/bigquery/docs/filtering-labels#filtering_datasets_using_labels) . Use the `  status: live  ` keyword to filter datasets based on status. Valid values of `  status  ` are `  live  ` (default), `  deleted  ` , and `  any  ` .
  - `  --max_results  ` or `  -n  ` : An integer indicating the maximum number of results. The default value is `  50  ` .

<!-- end list -->

``` text
bq ls --filter labels.key:value \
--max_results integer \
--format=prettyjson \
--project_id project_id
```

Replace the following:

  - key:value : a label key and value
  - integer : an integer representing the number of datasets to list
  - project\_id : the name of your project

Examples:

Enter the following command to list datasets in your default project. `  -- format  ` is set to pretty to return a basic formatted table.

``` text
bq ls --format=pretty
```

Enter the following command to list datasets in `  myotherproject  ` . `  --format  ` is set to `  prettyjson  ` to return detailed results in JSON format.

``` text
bq ls --format=prettyjson --project_id myotherproject
```

Enter the following command to list all datasets including hidden datasets in your default project. In the output, hidden datasets begin with an underscore.

``` text
bq ls -a
```

Enter the following command to return more than the default output of 50 datasets from your default project.

``` text
bq ls --max_results 60
```

Enter the following command to list datasets in your default project with the label `  org:dev  ` .

``` text
bq ls --filter labels.org:dev
```

### API

To list datasets using the API, call the [`  datasets.list  `](/bigquery/docs/reference/rest/v2/datasets/list) API method.

### C\#

Before trying this sample, follow the C\# setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery C\# API reference documentation](/dotnet/docs/reference/Google.Cloud.BigQuery.V2/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` csharp
using Google.Cloud.BigQuery.V2;
using System;
using System.Collections.Generic;
using System.Linq;

public class BigQueryListDatasets
{
    public void ListDatasets(
        string projectId = "your-project-id"
    )
    {
        BigQueryClient client = BigQueryClient.Create(projectId);
        // Retrieve list of datasets in project
        List<BigQueryDataset> datasets = client.ListDatasets().ToList();
        // Display the results
        if (datasets.Count > 0)
        {
            Console.WriteLine($"Datasets in project {projectId}:");
            foreach (var dataset in datasets)
            {
                Console.WriteLine($"\t{dataset.Reference.DatasetId}");
            }
        }
        else
        {
            Console.WriteLine($"{projectId} does not contain any datasets.");
        }
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
 "io"

 "cloud.google.com/go/bigquery"
 "google.golang.org/api/iterator"
)

// listDatasets demonstrates iterating through the collection of datasets in a project.
func listDatasets(projectID string, w io.Writer) error {
 // projectID := "my-project-id"
 ctx := context.Background()
 client, err := bigquery.NewClient(ctx, projectID)
 if err != nil {
     return fmt.Errorf("bigquery.NewClient: %v", err)
 }
 defer client.Close()

 it := client.Datasets(ctx)
 for {
     dataset, err := it.Next()
     if err == iterator.Done {
         break
     }
     if err != nil {
         return err
     }
     fmt.Fprintln(w, dataset.DatasetID)
 }
 return nil
}
```

### Java

Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Java API reference documentation](/java/docs/reference/google-cloud-bigquery/latest/overview) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` java
import com.google.api.gax.paging.Page;
import com.google.cloud.bigquery.BigQuery;
import com.google.cloud.bigquery.BigQuery.DatasetListOption;
import com.google.cloud.bigquery.BigQueryException;
import com.google.cloud.bigquery.BigQueryOptions;
import com.google.cloud.bigquery.Dataset;

public class ListDatasets {

  public static void runListDatasets() {
    // TODO(developer): Replace these variables before running the sample.
    String projectId = "MY_PROJECT_ID";
    listDatasets(projectId);
  }

  public static void listDatasets(String projectId) {
    try {
      // Initialize client that will be used to send requests. This client only needs to be created
      // once, and can be reused for multiple requests.
      BigQuery bigquery = BigQueryOptions.getDefaultInstance().getService();

      Page<Dataset> datasets = bigquery.listDatasets(projectId, DatasetListOption.pageSize(100));
      if (datasets == null) {
        System.out.println("Dataset does not contain any models");
        return;
      }
      datasets
          .iterateAll()
          .forEach(
              dataset -> System.out.printf("Success! Dataset ID: %s ", dataset.getDatasetId()));
    } catch (BigQueryException e) {
      System.out.println("Project does not contain any datasets \n" + e.toString());
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

async function listDatasets() {
  /**
   * TODO(developer): Uncomment the following lines before running the sample.
   */
  // const projectId = "my_project_id";

  // Lists all datasets in the specified project.
  // If projectId is not specified, this method will take
  // the projectId from the authenticated BigQuery Client.
  const [datasets] = await bigquery.getDatasets({projectId});
  console.log('Datasets:');
  datasets.forEach(dataset => console.log(dataset.id));
}
```

### PHP

Before trying this sample, follow the PHP setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery PHP API reference documentation](/php/docs/reference/cloud-bigquery/latest/BigQueryClient) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` php
use Google\Cloud\BigQuery\BigQueryClient;

/** Uncomment and populate these variables in your code */
// $projectId  = 'The Google project ID';

$bigQuery = new BigQueryClient([
    'projectId' => $projectId,
]);
$datasets = $bigQuery->datasets();
foreach ($datasets as $dataset) {
    print($dataset->id() . PHP_EOL);
}
```

### Python

Before trying this sample, follow the Python setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Python API reference documentation](/python/docs/reference/bigquery/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` python
from google.cloud import bigquery

# Construct a BigQuery client object.
client = bigquery.Client()

datasets = list(client.list_datasets())  # Make an API request.
project = client.project

if datasets:
    print("Datasets in project {}:".format(project))
    for dataset in datasets:
        print("\t{}".format(dataset.dataset_id))
else:
    print("{} project does not contain any datasets.".format(project))
```

### Ruby

Before trying this sample, follow the Ruby setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Ruby API reference documentation](https://googleapis.dev/ruby/google-cloud-bigquery/latest/Google/Cloud/Bigquery.html) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` ruby
require "google/cloud/bigquery"

def list_datasets project_id = "your-project-id"
  bigquery = Google::Cloud::Bigquery.new project: project_id

  puts "Datasets in project #{project_id}:"
  bigquery.datasets.each do |dataset|
    puts "\t#{dataset.dataset_id}"
  end
end
```

## Get information about datasets

Select one of the following options:

### Console

1.  In the left pane, click explore **Explorer** :

2.  In the **Explorer** pane, expand a project, click **Datasets** to see the datasets in that project, and then click the name of your dataset. You can also use the search field or filters to find your dataset.
    
    The description and details appear in the **Details** tab.

3.  Optional: You can go to other tabs to see the list of tables, routines, and models in the dataset.

By default, [hidden datasets](/bigquery/docs/datasets#hidden_datasets) are hidden from the Google Cloud console. To show information about hidden datasets, use the bq command-line tool or the API.

### SQL

Query the [`  INFORMATION_SCHEMA.SCHEMATA  ` view](/bigquery/docs/information-schema-datasets-schemata) :

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
    SELECT
      * EXCEPT (schema_owner)
    FROM
      PROJECT_ID.`region-REGION`.INFORMATION_SCHEMA.SCHEMATA;
    ```
    
    Replace the following:
    
      - `  PROJECT_ID  ` : the ID of your Google Cloud project. If not specified, the default project is used.
      - `  REGION  ` : any [dataset region name](/bigquery/docs/locations) . For example, `  us  ` .

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](/bigquery/docs/running-queries#queries) .

You can also query the [`  INFORMATION_SCHEMA.SCHEMATA_OPTIONS  ` view](/bigquery/docs/information-schema-datasets-schemata-options) .

``` text
SELECT
  *
FROM
  PROJECT_ID.`region-REGION`.INFORMATION_SCHEMA.SCHEMATA_OPTIONS;
```

### bq

Issue the `  bq show  ` command. The `  --format  ` flag can be used to control the output. If you are getting information about a dataset in a project other than your default project, add the project ID to the dataset name in the following format: `  project_id : dataset  ` . The output displays the dataset's information such as access control, labels, and location. This command doesn't display a dataset's inherited permissions, but you can see them in the Google Cloud console.

To show information about a [hidden dataset](/bigquery/docs/datasets#hidden_datasets) , use the [`  bq ls --all  `](/bigquery/docs/listing-datasets) command to list all datasets and then use the name of the hidden dataset in the `  bq show  ` command.

``` text
bq show --format=prettyjson project_id:dataset
```

Replace the following:

  - project\_id is the name of your project.
  - dataset is the name of the dataset.

Examples:

Enter the following command to display information about `  mydataset  ` in your default project.

``` text
bq show --format=prettyjson mydataset
```

Enter the following command to display information about `  mydataset  ` in `  myotherproject  ` .

``` text
bq show --format=prettyjson myotherproject:mydataset
```

Enter the following command to display information about the hidden dataset `  _1234abcd56efgh78ijkl1234  ` in your default project.

``` text
bq show --format=prettyjson _1234abcd56efgh78ijkl1234
```

### API

Call the [`  datasets.get  `](/bigquery/docs/reference/rest/v2/datasets/get) API method and provide any relevant parameters.

### Go

Before trying this sample, follow the Go setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Go API reference documentation](https://godoc.org/cloud.google.com/go/bigquery) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` go
import (
 "context"
 "fmt"
 "io"

 "cloud.google.com/go/bigquery"
 "google.golang.org/api/iterator"
)

// printDatasetInfo demonstrates fetching dataset metadata and printing some of it to an io.Writer.
func printDatasetInfo(w io.Writer, projectID, datasetID string) error {
 // projectID := "my-project-id"
 // datasetID := "mydataset"
 ctx := context.Background()
 client, err := bigquery.NewClient(ctx, projectID)
 if err != nil {
     return fmt.Errorf("bigquery.NewClient: %v", err)
 }
 defer client.Close()

 meta, err := client.Dataset(datasetID).Metadata(ctx)
 if err != nil {
     return err
 }

 fmt.Fprintf(w, "Dataset ID: %s\n", datasetID)
 fmt.Fprintf(w, "Description: %s\n", meta.Description)
 fmt.Fprintln(w, "Labels:")
 for k, v := range meta.Labels {
     fmt.Fprintf(w, "\t%s: %s", k, v)
 }
 fmt.Fprintln(w, "Tables:")
 it := client.Dataset(datasetID).Tables(ctx)

 cnt := 0
 for {
     t, err := it.Next()
     if err == iterator.Done {
         break
     }
     cnt++
     fmt.Fprintf(w, "\t%s\n", t.TableID)
 }
 if cnt == 0 {
     fmt.Fprintln(w, "\tThis dataset does not contain any tables.")
 }
 return nil
}
```

### Java

Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Java API reference documentation](/java/docs/reference/google-cloud-bigquery/latest/overview) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` java
import com.google.api.gax.paging.Page;
import com.google.cloud.bigquery.BigQuery;
import com.google.cloud.bigquery.BigQuery.TableListOption;
import com.google.cloud.bigquery.BigQueryException;
import com.google.cloud.bigquery.BigQueryOptions;
import com.google.cloud.bigquery.Dataset;
import com.google.cloud.bigquery.DatasetId;
import com.google.cloud.bigquery.Table;

public class GetDatasetInfo {

  public static void runGetDatasetInfo() {
    // TODO(developer): Replace these variables before running the sample.
    String projectId = "MY_PROJECT_ID";
    String datasetName = "MY_DATASET_NAME";
    getDatasetInfo(projectId, datasetName);
  }

  public static void getDatasetInfo(String projectId, String datasetName) {
    try {
      // Initialize client that will be used to send requests. This client only needs to be created
      // once, and can be reused for multiple requests.
      BigQuery bigquery = BigQueryOptions.getDefaultInstance().getService();
      DatasetId datasetId = DatasetId.of(projectId, datasetName);
      Dataset dataset = bigquery.getDataset(datasetId);

      // View dataset properties
      String description = dataset.getDescription();
      System.out.println(description);

      // View tables in the dataset
      // For more information on listing tables see:
      // https://javadoc.io/static/com.google.cloud/google-cloud-bigquery/0.22.0-beta/com/google/cloud/bigquery/BigQuery.html
      Page<Table> tables = bigquery.listTables(datasetName, TableListOption.pageSize(100));

      tables.iterateAll().forEach(table -> System.out.print(table.getTableId().getTable() + "\n"));

      System.out.println("Dataset info retrieved successfully.");
    } catch (BigQueryException e) {
      System.out.println("Dataset info not retrieved. \n" + e.toString());
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

async function getDataset() {
  // Retrieves dataset named "my_dataset".

  /**
   * TODO(developer): Uncomment the following lines before running the sample
   */
  // const datasetId = "my_dataset";

  // Retrieve dataset reference
  const [dataset] = await bigquery.dataset(datasetId).get();

  console.log('Dataset:');
  console.log(dataset.metadata.datasetReference);
}
getDataset();
```

### Python

Before trying this sample, follow the Python setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Python API reference documentation](/python/docs/reference/bigquery/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` python
from google.cloud import bigquery

# Construct a BigQuery client object.
client = bigquery.Client()

# TODO(developer): Set dataset_id to the ID of the dataset to fetch.
# dataset_id = 'your-project.your_dataset'

dataset = client.get_dataset(dataset_id)  # Make an API request.

full_dataset_id = "{}.{}".format(dataset.project, dataset.dataset_id)
friendly_name = dataset.friendly_name
print(
    "Got dataset '{}' with friendly_name '{}'.".format(
        full_dataset_id, friendly_name
    )
)

# View dataset properties.
print("Description: {}".format(dataset.description))
print("Labels:")
labels = dataset.labels
if labels:
    for label, value in labels.items():
        print("\t{}: {}".format(label, value))
else:
    print("\tDataset has no labels defined.")

# View tables in dataset.
print("Tables:")
tables = list(client.list_tables(dataset))  # Make an API request(s).
if tables:
    for table in tables:
        print("\t{}".format(table.table_id))
else:
    print("\tThis dataset does not contain any tables.")
```

## Verify the dataset name

The following samples show how to check if a dataset exists:

### Java

Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Java API reference documentation](/java/docs/reference/google-cloud-bigquery/latest/overview) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` java
import com.google.cloud.bigquery.BigQuery;
import com.google.cloud.bigquery.BigQueryException;
import com.google.cloud.bigquery.BigQueryOptions;
import com.google.cloud.bigquery.Dataset;
import com.google.cloud.bigquery.DatasetId;

// Sample to check dataset exist
public class DatasetExists {

  public static void main(String[] args) {
    // TODO(developer): Replace these variables before running the sample.
    String datasetName = "MY_DATASET_NAME";
    datasetExists(datasetName);
  }

  public static void datasetExists(String datasetName) {
    try {
      // Initialize client that will be used to send requests. This client only needs to be created
      // once, and can be reused for multiple requests.
      BigQuery bigquery = BigQueryOptions.getDefaultInstance().getService();

      Dataset dataset = bigquery.getDataset(DatasetId.of(datasetName));
      if (dataset != null) {
        System.out.println("Dataset already exists.");
      } else {
        System.out.println("Dataset not found.");
      }
    } catch (BigQueryException e) {
      System.out.println("Something went wrong. \n" + e.toString());
    }
  }
}
```

### Python

Before trying this sample, follow the Python setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Python API reference documentation](/python/docs/reference/bigquery/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` python
from google.cloud import bigquery
from google.cloud.exceptions import NotFound

client = bigquery.Client()

# TODO(developer): Set dataset_id to the ID of the dataset to determine existence.
# dataset_id = "your-project.your_dataset"

try:
    client.get_dataset(dataset_id)  # Make an API request.
    print("Dataset {} already exists".format(dataset_id))
except NotFound:
    print("Dataset {} is not found".format(dataset_id))
```

## What's next

  - For more information on creating datasets, see [Creating datasets](/bigquery/docs/datasets) .
  - For more information on assigning access controls to datasets, see [Controlling access to datasets](/bigquery/docs/dataset-access-controls) .
  - For more information on changing dataset properties, see [Updating dataset properties](/bigquery/docs/updating-datasets) .
  - For more information on creating and managing labels, see [Creating and managing labels](/bigquery/docs/labels) .
  - To see an overview of `  INFORMATION_SCHEMA  ` , go to [Introduction to BigQuery `  INFORMATION_SCHEMA  `](/bigquery/docs/information-schema-intro) .
