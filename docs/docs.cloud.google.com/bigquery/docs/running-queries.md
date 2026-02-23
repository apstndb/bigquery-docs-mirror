# Run a query

This document shows you how to run a query in BigQuery and understand how much data the query will process before execution by performing a [dry run](#dry-run) .

## Types of queries

You can [query BigQuery data](/bigquery/docs/running-queries) by using one of the following query job types:

  - **[Interactive query jobs](/bigquery/docs/running-queries#queries)** . By default, BigQuery runs queries as interactive query jobs, which are intended to start executing as quickly as possible.

  - **[Batch query jobs](/bigquery/docs/running-queries#batch)** . Batch queries have lower priority than interactive queries. When a project or reservation is using all of its available compute resources, batch queries are more likely to be queued and remain in the queue. After a batch query starts running, the batch query runs the same as an interactive query. For more information, see [query queues](/bigquery/docs/query-queues) .

  - **[Continuous query jobs](/bigquery/docs/continuous-queries-introduction)** . With these jobs, the query runs continuously, letting you analyze incoming data in BigQuery in real time and then write the results to a BigQuery table, or export the results to Bigtable or Pub/Sub. You can use this capability to perform time sensitive tasks, such as creating and immediately acting on insights, applying real time machine learning (ML) inference, and building event-driven data pipelines.

You can run query jobs by using the following methods:

  - Compose and run a query in the [Google Cloud console](/bigquery/bigquery-web-ui#overview) .
  - Run the `  bq query  ` command in the [bq command-line tool](/bigquery/bq-command-line-tool) .
  - Programmatically call the [`  jobs.query  `](/bigquery/docs/reference/v2/jobs/query) or [`  jobs.insert  `](/bigquery/docs/reference/v2/jobs/insert) method in the BigQuery [REST API](/bigquery/docs/reference/rest/v2) .
  - Use the BigQuery [client libraries](/bigquery/docs/reference/libraries) .

BigQuery saves query results to either a [temporary table (default) or permanent table](/bigquery/docs/writing-results#temporary_and_permanent_tables) . When you specify a permanent table as the destination table for the results, you can choose whether to append or overwrite an existing table, or create a new table with a unique name.

**Note:** If you query data from a project to data stored in a different project, the querying project is billed for the query job while the project storing the data is billed for the amount of data stored in BigQuery.

## Required roles

To get the permissions that you need to run a query job, ask your administrator to grant you the following IAM roles :

  - [BigQuery Job User](/iam/docs/roles-permissions/bigquery#bigquery.jobUser) ( `  roles/bigquery.jobUser  ` ) on the project.
  - [BigQuery Data Viewer](/iam/docs/roles-permissions/bigquery#bigquery.dataViewer) ( `  roles/bigquery.dataViewer  ` ) on all tables and views that your query references. To query views, you also need this role on all underlying tables and views. If you're using [authorized views](/bigquery/docs/authorized-views) or [authorized datasets](/bigquery/docs/authorized-datasets) , you don't need access to the underlying source data.

For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

These predefined roles contain the permissions required to run a query job. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

The following permissions are required to run a query job:

  - `  bigquery.jobs.create  ` on the project from which the query is being run, regardless of where the data is stored.
  - `  bigquery.tables.getData  ` on all tables and views that your query references. To query views, you also need this permission on all underlying tables and views. If you're using [authorized views](/bigquery/docs/authorized-views) or [authorized datasets](/bigquery/docs/authorized-datasets) , you don't need access to the underlying source data.

You might also be able to get these permissions with [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

### Troubleshooting

``` text
Access Denied: Project [project_id]: User does not have bigquery.jobs.create
permission in project [project_id].
```

This error occurs when a principal lacks permission to create a query jobs in the project.

**Resolution** : An administrator must grant you the `  bigquery.jobs.create  ` permission on the project you are querying. This permission is required in addition to any permission required to access the queried data.

For more information about BigQuery permissions, see [Access control with IAM](/bigquery/docs/access-control) .

## Run an interactive query

To run an interactive query, select one of the following options:

### Console

1.  Go to the **BigQuery** page.

2.  Click add\_box **SQL query** .

3.  In the query editor, enter a valid GoogleSQL query.
    
    For example, query the [BigQuery public dataset `  usa_names  `](https://console.cloud.google.com/bigquery?p=bigquery-public-data&d=usa_names&page=dataset) to determine the most common names in the United States between the years 1910 and 2013:
    
    ``` text
    SELECT
      name, gender,
      SUM(number) AS total
    FROM
      `bigquery-public-data.usa_names.usa_1910_2013`
    GROUP BY
      name, gender
    ORDER BY
      total DESC
    LIMIT
      10;
    ```
    
    Alternatively, you can use the [**Reference** panel](#use-reference-panel) to construct new queries.

4.  Optional: To automatically display code suggestions when you type a query, click settings **More** , and then select **SQL autocomplete** . If you don't need autocomplete suggestions, deselect **SQL autocomplete** . This also turns off the project name autofill suggestions.

5.  Optional: To select additional [query settings](#query-settings) , click settings **More** , and then click **Query settings** .

6.  Click play\_circle **Run** .
    
    If you don't specify a destination table, the query job writes the output to a temporary (cache) table.
    
    You can now explore the query results in the **Results** tab of the **Query results** pane.

7.  Optional: To sort the query results by column, click arrow\_drop\_down **Open sort menu** next to the column name and select a sort order. If the estimated bytes processed for the sort is more than zero, then the number of bytes is displayed at the top of the menu.

8.  Optional: To see visualization of your query results, go to the **Visualization** tab. You can zoom in or zoom out of the chart, download the chart as a PNG file, or toggle the legend visibility.
    
    In the **Visualization configuration** pane, you can change the visualization type and configure the measures and dimensions of the visualization. Fields in this pane are prefilled with the initial configuration inferred from the destination table schema of the query. The configuration is preserved between following query runs in the same query editor.
    
    For **Line** , **Bar** , or **Scatter** visualizations, the supported dimensions are `  INT64  ` , `  FLOAT64  ` , `  NUMERIC  ` , `  BIGNUMERIC  ` , `  TIMESTAMP  ` , `  DATE  ` , `  DATETIME  ` , `  TIME  ` , and `  STRING  ` data types, while the supported measures are `  INT64  ` , `  FLOAT64  ` , `  NUMERIC  ` , and `  BIGNUMERIC  ` data types.
    
    If your query results include the `  GEOGRAPHY  ` type, then **Map** is the default visualization type, which lets you visualize your results on an [interactive map](/bigquery/docs/geospatial-visualize#bigquery_studio) .

9.  Optional: In the **JSON** tab, you can explore the query results in the JSON format, where the key is the column name and the value is the result for that column.

### bq

1.  In the Google Cloud console, activate Cloud Shell.
    
    At the bottom of the Google Cloud console, a [Cloud Shell](/shell/docs/how-cloud-shell-works) session starts and displays a command-line prompt. Cloud Shell is a shell environment with the Google Cloud CLI already installed and with values already set for your current project. It can take a few seconds for the session to initialize.

2.  Use the [`  bq query  ` command](/bigquery/docs/reference/bq-cli-reference#bq_query) . In the following example, the `  --use_legacy_sql=false  ` flag lets you use GoogleSQL syntax.
    
    ``` text
    bq query \
        --use_legacy_sql=false \
        'QUERY'
    ```
    
    Replace QUERY with a valid GoogleSQL query. For example, query the [BigQuery public dataset `  usa_names  `](https://console.cloud.google.com/bigquery?p=bigquery-public-data&d=usa_names&page=dataset) to determine the most common names in the United States between the years 1910 and 2013:
    
    ``` text
    bq query \
        --use_legacy_sql=false \
        'SELECT
          name, gender,
          SUM(number) AS total
        FROM
          `bigquery-public-data.usa_names.usa_1910_2013`
        GROUP BY
          name, gender
        ORDER BY
          total DESC
        LIMIT
          10;'
    ```
    
    The query job writes the output to a temporary (cache) table.
    
    Optionally, you can specify the destination table and [location](/bigquery/docs/locations) for the query results. To write the results to an existing table, include the appropriate flag to append ( `  --append_table=true  ` ) or overwrite ( `  --replace=true  ` ) the table.
    
    ``` text
    bq query \
        --location=LOCATION \
        --destination_table=TABLE \
        --use_legacy_sql=false \
        'QUERY'
    ```
    
    Replace the following:
    
      - LOCATION : the region or multi-region for the destination table—for example, `  US  `
        
        In this example, the `  usa_names  ` dataset is stored in the US multi-region location. If you specify a destination table for this query, the dataset that contains the destination table must also be in the US multi-region. You cannot query a dataset in one location and write the results to a table in another location.
        
        You can set a default value for the location using the [.bigqueryrc file](/bigquery/docs/bq-command-line-tool#setting_default_values_for_command-line_flags) .
    
      - TABLE : a name for the destination table—for example, `  myDataset.myTable  `
        
        If the destination table is a new table, then BigQuery creates the table when you run your query. However, you must specify an existing dataset.
        
        If the table isn't in your current project, then add the Google Cloud project ID using the format `  PROJECT_ID:DATASET.TABLE  ` —for example, `  myProject:myDataset.myTable  ` . If `  --destination_table  ` is unspecified, a query job is generated that writes the output to a temporary table.

### Terraform

Use the [`  google_bigquery_job  ` resource](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/bigquery_job) .

**Note:** To create BigQuery objects using Terraform, you must enable the [Cloud Resource Manager API](/resource-manager/reference/rest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

The following example runs a query. You can retrieve the query results by [viewing the job details](/bigquery/docs/managing-jobs#view-job) :

``` terraform
# Generate a unique job ID.
resource "random_string" "job_id" {
  lower   = true
  length  = 16
  special = false

  keepers = {
    uuid = uuid()
  }
}

# Create a query using the generated job ID.
resource "google_bigquery_job" "my_query_job" {
  job_id = random_string.job_id.id

  query {
    query = "SELECT name, SUM(number) AS total FROM `bigquery-public-data.usa_names.usa_1910_2013` GROUP BY name ORDER BY total DESC LIMIT 100;"
  }
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

To run a query using the API, [insert a new job](/bigquery/docs/reference/rest/v2/jobs/insert) and populate the `  query  ` job configuration property. Optionally specify your location in the `  location  ` property in the `  jobReference  ` section of the [job resource](/bigquery/docs/reference/rest/v2/jobs) .

Poll for results by calling [`  getQueryResults  `](/bigquery/docs/reference/rest/v2/jobs/getQueryResults) . Poll until `  jobComplete  ` equals `  true  ` . Check for errors and warnings in the `  errors  ` list.

### C\#

Before trying this sample, follow the C\# setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery C\# API reference documentation](/dotnet/docs/reference/Google.Cloud.BigQuery.V2/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` csharp
using Google.Cloud.BigQuery.V2;
using System;

public class BigQueryQuery
{
    public void Query(
        string projectId = "your-project-id"
    )
    {
        BigQueryClient client = BigQueryClient.Create(projectId);
        string query = @"
            SELECT name FROM `bigquery-public-data.usa_names.usa_1910_2013`
            WHERE state = 'TX'
            LIMIT 100";
        BigQueryJob job = client.CreateQueryJob(
            sql: query,
            parameters: null,
            options: new QueryOptions { UseQueryCache = false });
        // Wait for the job to complete.
        job = job.PollUntilCompleted().ThrowOnAnyError();
        // Display the results
        foreach (BigQueryRow row in client.GetQueryResults(job.Reference))
        {
            Console.WriteLine($"{row["name"]}");
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

// queryBasic demonstrates issuing a query and reading results.
func queryBasic(w io.Writer, projectID string) error {
 // projectID := "my-project-id"
 ctx := context.Background()
 client, err := bigquery.NewClient(ctx, projectID)
 if err != nil {
     return fmt.Errorf("bigquery.NewClient: %v", err)
 }
 defer client.Close()

 q := client.Query(
     "SELECT name FROM `bigquery-public-data.usa_names.usa_1910_2013` " +
         "WHERE state = \"TX\" " +
         "LIMIT 100")
 // Location must match that of the dataset(s) referenced in the query.
 q.Location = "US"
 // Run the query and print results when the query job is completed.
 job, err := q.Run(ctx)
 if err != nil {
     return err
 }
 status, err := job.Wait(ctx)
 if err != nil {
     return err
 }
 if err := status.Err(); err != nil {
     return err
 }
 it, err := job.Read(ctx)
 for {
     var row []bigquery.Value
     err := it.Next(&row)
     if err == iterator.Done {
         break
     }
     if err != nil {
         return err
     }
     fmt.Fprintln(w, row)
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
import com.google.cloud.bigquery.QueryJobConfiguration;
import com.google.cloud.bigquery.TableResult;

public class SimpleQuery {

  public static void runSimpleQuery() {
    // TODO(developer): Replace this query before running the sample.
    String query = "SELECT corpus FROM `bigquery-public-data.samples.shakespeare` GROUP BY corpus;";
    simpleQuery(query);
  }

  public static void simpleQuery(String query) {
    try {
      // Initialize client that will be used to send requests. This client only needs to be created
      // once, and can be reused for multiple requests.
      BigQuery bigquery = BigQueryOptions.getDefaultInstance().getService();

      // Create the query job.
      QueryJobConfiguration queryConfig = QueryJobConfiguration.newBuilder(query).build();

      // Execute the query.
      TableResult result = bigquery.query(queryConfig);

      // Print the results.
      result.iterateAll().forEach(rows -> rows.forEach(row -> System.out.println(row.getValue())));

      System.out.println("Query ran successfully");
    } catch (BigQueryException | InterruptedException e) {
      System.out.println("Query did not run \n" + e.toString());
    }
  }
}
```

To run a query with a proxy, see [Configuring a proxy](https://github.com/googleapis/google-cloud-java#configuring-a-proxy) .

### Node.js

Before trying this sample, follow the Node.js setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Node.js API reference documentation](https://googleapis.dev/nodejs/bigquery/latest/index.html) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` javascript
// Import the Google Cloud client library using default credentials
const {BigQuery} = require('@google-cloud/bigquery');
const bigquery = new BigQuery();
async function query() {
  // Queries the U.S. given names dataset for the state of Texas.

  const query = `SELECT name
    FROM \`bigquery-public-data.usa_names.usa_1910_2013\`
    WHERE state = 'TX'
    LIMIT 100`;

  // For all options, see https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query
  const options = {
    query: query,
    // Location must match that of the dataset(s) referenced in the query.
    location: 'US',
  };

  // Run the query as a job
  const [job] = await bigquery.createQueryJob(options);
  console.log(`Job ${job.id} started.`);

  // Wait for the query to finish
  const [rows] = await job.getQueryResults();

  // Print the results
  console.log('Rows:');
  rows.forEach(row => console.log(row));
}
```

### PHP

Before trying this sample, follow the PHP setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery PHP API reference documentation](/php/docs/reference/cloud-bigquery/latest/BigQueryClient) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` php
use Google\Cloud\BigQuery\BigQueryClient;
use Google\Cloud\Core\ExponentialBackoff;

/** Uncomment and populate these variables in your code */
// $projectId = 'The Google project ID';
// $query = 'SELECT id, view_count FROM `bigquery-public-data.stackoverflow.posts_questions`';

$bigQuery = new BigQueryClient([
    'projectId' => $projectId,
]);
$jobConfig = $bigQuery->query($query);
$job = $bigQuery->startQuery($jobConfig);

$backoff = new ExponentialBackoff(10);
$backoff->execute(function () use ($job) {
    print('Waiting for job to complete' . PHP_EOL);
    $job->reload();
    if (!$job->isComplete()) {
        throw new Exception('Job has not yet completed', 500);
    }
});
$queryResults = $job->queryResults();

$i = 0;
foreach ($queryResults as $row) {
    printf('--- Row %s ---' . PHP_EOL, ++$i);
    foreach ($row as $column => $value) {
        printf('%s: %s' . PHP_EOL, $column, json_encode($value));
    }
}
printf('Found %s row(s)' . PHP_EOL, $i);
```

### Python

Before trying this sample, follow the Python setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Python API reference documentation](/python/docs/reference/bigquery/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` python
from google.cloud import bigquery

# Construct a BigQuery client object.
client = bigquery.Client()

query = """
    SELECT name, SUM(number) as total_people
    FROM `bigquery-public-data.usa_names.usa_1910_2013`
    WHERE state = 'TX'
    GROUP BY name, state
    ORDER BY total_people DESC
    LIMIT 20
"""
rows = client.query_and_wait(query)  # Make an API request.

print("The query data:")
for row in rows:
    # Row values can be accessed by field name or index.
    print("name={}, count={}".format(row[0], row["total_people"]))
```

### Ruby

Before trying this sample, follow the Ruby setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Ruby API reference documentation](https://googleapis.dev/ruby/google-cloud-bigquery/latest/Google/Cloud/Bigquery.html) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` ruby
require "google/cloud/bigquery"

def query
  bigquery = Google::Cloud::Bigquery.new
  sql = "SELECT name FROM `bigquery-public-data.usa_names.usa_1910_2013` " \
        "WHERE state = 'TX' " \
        "LIMIT 100"

  # Location must match that of the dataset(s) referenced in the query.
  results = bigquery.query sql do |config|
    config.location = "US"
  end

  results.each do |row|
    puts row.inspect
  end
end
```

## Run a batch query

To run a batch query, select one of the following options:

### Console

1.  Go to the **BigQuery** page.

2.  Click add\_box **SQL query** .

3.  In the query editor, enter a valid GoogleSQL query.
    
    For example, query the [BigQuery public dataset `  usa_names  `](https://console.cloud.google.com/bigquery?p=bigquery-public-data&d=usa_names&page=dataset) to determine the most common names in the United States between the years 1910 and 2013:
    
    ``` text
    SELECT
      name, gender,
      SUM(number) AS total
    FROM
      `bigquery-public-data.usa_names.usa_1910_2013`
    GROUP BY
      name, gender
    ORDER BY
      total DESC
    LIMIT
      10;
    ```

4.  Click settings **More** , and then click **Query settings** .

5.  In the **Resource management** section, select **Batch** .

6.  Optional: Adjust your [query settings](#query-settings) .

7.  Click **Save** .

8.  Click play\_circle **Run** .
    
    If you don't specify a destination table, the query job writes the output to a temporary (cache) table.

### bq

1.  In the Google Cloud console, activate Cloud Shell.
    
    At the bottom of the Google Cloud console, a [Cloud Shell](/shell/docs/how-cloud-shell-works) session starts and displays a command-line prompt. Cloud Shell is a shell environment with the Google Cloud CLI already installed and with values already set for your current project. It can take a few seconds for the session to initialize.

2.  Use the [`  bq query  ` command](/bigquery/docs/reference/bq-cli-reference#bq_query) and specify the `  --batch  ` flag. In the following example, the `  --use_legacy_sql=false  ` flag lets you use GoogleSQL syntax.
    
    ``` text
    bq query \
        --batch \
        --use_legacy_sql=false \
        'QUERY'
    ```
    
    Replace QUERY with a valid GoogleSQL query. For example, query the [BigQuery public dataset `  usa_names  `](https://console.cloud.google.com/bigquery?p=bigquery-public-data&d=usa_names&page=dataset) to determine the most common names in the United States between the years 1910 and 2013:
    
    ``` text
    bq query \
        --batch \
        --use_legacy_sql=false \
        'SELECT
          name, gender,
          SUM(number) AS total
        FROM
          `bigquery-public-data.usa_names.usa_1910_2013`
        GROUP BY
          name, gender
        ORDER BY
          total DESC
        LIMIT
          10;'
    ```
    
    The query job writes the output to a temporary (cache) table.
    
    Optionally, you can specify the destination table and [location](/bigquery/docs/locations) for the query results. To write the results to an existing table, include the appropriate flag to append ( `  --append_table=true  ` ) or overwrite ( `  --replace=true  ` ) the table.
    
    ``` text
    bq query \
        --batch \
        --location=LOCATION \
        --destination_table=TABLE \
        --use_legacy_sql=false \
        'QUERY'
    ```
    
    Replace the following:
    
      - LOCATION : the region or multi-region for the destination table—for example, `  US  `
        
        In this example, the `  usa_names  ` dataset is stored in the US multi-region location. If you specify a destination table for this query, the dataset that contains the destination table must also be in the US multi-region. You cannot query a dataset in one location and write the results to a table in another location.
        
        You can set a default value for the location using the [.bigqueryrc file](/bigquery/docs/bq-command-line-tool#setting_default_values_for_command-line_flags) .
    
      - TABLE : a name for the destination table—for example, `  myDataset.myTable  `
        
        If the destination table is a new table, then BigQuery creates the table when you run your query. However, you must specify an existing dataset.
        
        If the table isn't in your current project, then add the Google Cloud project ID using the format `  PROJECT_ID:DATASET.TABLE  ` —for example, `  myProject:myDataset.myTable  ` . If `  --destination_table  ` is unspecified, a query job is generated that writes the output to a temporary table.

### API

To run a query using the API, [insert a new job](/bigquery/docs/reference/rest/v2/jobs/insert) and populate the `  query  ` job configuration property. Optionally specify your location in the `  location  ` property in the `  jobReference  ` section of the [job resource](/bigquery/docs/reference/rest/v2/jobs) .

When you populate the query job properties, include the `  configuration.query.priority  ` property and set the value to `  BATCH  ` .

Poll for results by calling [`  getQueryResults  `](/bigquery/docs/reference/rest/v2/jobs/getQueryResults) . Poll until `  jobComplete  ` equals `  true  ` . Check for errors and warnings in the `  errors  ` list.

### Go

Before trying this sample, follow the Go setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Go API reference documentation](https://godoc.org/cloud.google.com/go/bigquery) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` go
import (
 "context"
 "fmt"
 "io"
 "time"

 "cloud.google.com/go/bigquery"
)

// queryBatch demonstrates issuing a query job using batch priority.
func queryBatch(w io.Writer, projectID, dstDatasetID, dstTableID string) error {
 // projectID := "my-project-id"
 // dstDatasetID := "mydataset"
 // dstTableID := "mytable"
 ctx := context.Background()
 client, err := bigquery.NewClient(ctx, projectID)
 if err != nil {
     return fmt.Errorf("bigquery.NewClient: %v", err)
 }
 defer client.Close()

 // Build an aggregate table.
 q := client.Query(`
     SELECT
             corpus,
             SUM(word_count) as total_words,
             COUNT(1) as unique_words
     FROM ` + "`bigquery-public-data.samples.shakespeare`" + `
     GROUP BY corpus;`)
 q.Priority = bigquery.BatchPriority
 q.QueryConfig.Dst = client.Dataset(dstDatasetID).Table(dstTableID)

 // Start the job.
 job, err := q.Run(ctx)
 if err != nil {
     return err
 }
 // Job is started and will progress without interaction.
 // To simulate other work being done, sleep a few seconds.
 time.Sleep(5 * time.Second)
 status, err := job.Status(ctx)
 if err != nil {
     return err
 }

 state := "Unknown"
 switch status.State {
 case bigquery.Pending:
     state = "Pending"
 case bigquery.Running:
     state = "Running"
 case bigquery.Done:
     state = "Done"
 }
 // You can continue to monitor job progress until it reaches
 // the Done state by polling periodically.  In this example,
 // we print the latest status.
 fmt.Fprintf(w, "Job %s in Location %s currently in state: %s\n", job.ID(), job.Location(), state)

 return nil

}
```

### Java

To run a batch query, [set the query priority](/java/docs/reference/google-cloud-bigquery/latest/com.google.cloud.bigquery.QueryJobConfiguration.Builder#com_google_cloud_bigquery_QueryJobConfiguration_Builder_setPriority_com_google_cloud_bigquery_QueryJobConfiguration_Priority_) to [QueryJobConfiguration.Priority.BATCH](/java/docs/reference/google-cloud-bigquery/latest/com.google.cloud.bigquery.QueryJobConfiguration.Priority#staticFields) when creating a [QueryJobConfiguration](/java/docs/reference/google-cloud-bigquery/latest/com.google.cloud.bigquery.QueryJobConfiguration) .

Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Java API reference documentation](/java/docs/reference/google-cloud-bigquery/latest/overview) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` java
import com.google.cloud.bigquery.BigQuery;
import com.google.cloud.bigquery.BigQueryException;
import com.google.cloud.bigquery.BigQueryOptions;
import com.google.cloud.bigquery.QueryJobConfiguration;
import com.google.cloud.bigquery.TableResult;

// Sample to query batch in a table
public class QueryBatch {

  public static void runQueryBatch() {
    // TODO(developer): Replace these variables before running the sample.
    String projectId = "MY_PROJECT_ID";
    String datasetName = "MY_DATASET_NAME";
    String tableName = "MY_TABLE_NAME";
    String query =
        "SELECT corpus"
            + " FROM `"
            + projectId
            + "."
            + datasetName
            + "."
            + tableName
            + " GROUP BY corpus;";
    queryBatch(query);
  }

  public static void queryBatch(String query) {
    try {
      // Initialize client that will be used to send requests. This client only needs to be created
      // once, and can be reused for multiple requests.
      BigQuery bigquery = BigQueryOptions.getDefaultInstance().getService();

      QueryJobConfiguration queryConfig =
          QueryJobConfiguration.newBuilder(query)
              // Run at batch priority, which won't count toward concurrent rate limit.
              .setPriority(QueryJobConfiguration.Priority.BATCH)
              .build();

      TableResult results = bigquery.query(queryConfig);

      results
          .iterateAll()
          .forEach(row -> row.forEach(val -> System.out.printf("%s,", val.toString())));

      System.out.println("Query batch performed successfully.");
    } catch (BigQueryException | InterruptedException e) {
      System.out.println("Query batch not performed \n" + e.toString());
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

async function queryBatch() {
  // Runs a query at batch priority.

  // Create query job configuration. For all options, see
  // https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#jobconfigurationquery
  const queryJobConfig = {
    query: `SELECT corpus
            FROM \`bigquery-public-data.samples.shakespeare\` 
            LIMIT 10`,
    useLegacySql: false,
    priority: 'BATCH',
  };

  // Create job configuration. For all options, see
  // https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#jobconfiguration
  const jobConfig = {
    // Specify a job configuration to set optional job resource properties.
    configuration: {
      query: queryJobConfig,
    },
  };

  // Make API request.
  const [job] = await bigquery.createJob(jobConfig);

  const jobId = job.metadata.id;
  const state = job.metadata.status.state;
  console.log(`Job ${jobId} is currently in state ${state}`);
}
```

### Python

Before trying this sample, follow the Python setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Python API reference documentation](/python/docs/reference/bigquery/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` python
from google.cloud import bigquery

# Construct a BigQuery client object.
client = bigquery.Client()

job_config = bigquery.QueryJobConfig(
    # Run at batch priority, which won't count toward concurrent rate limit.
    priority=bigquery.QueryPriority.BATCH
)

sql = """
    SELECT corpus
    FROM `bigquery-public-data.samples.shakespeare`
    GROUP BY corpus;
"""

# Start the query, passing in the extra configuration.
query_job = client.query(sql, job_config=job_config)  # Make an API request.

# Check on the progress by getting the job's updated state. Once the state
# is `DONE`, the results are ready.
query_job = client.get_job(
    query_job.job_id, location=query_job.location
)  # Make an API request.

print("Job {} is currently in state {}".format(query_job.job_id, query_job.state))
```

## Run a continuous query

Running a continuous query job requires additional configuration. For more information, see [Create continuous queries](/bigquery/docs/continuous-queries) .

## Use the **Reference** panel

In the query editor, the **Reference** panel dynamically displays context-aware information about tables, snapshots, views, and materialized views. The panel lets you preview the schema details of these resources, or open them in a new tab. You can also use the **Reference** panel to construct new queries or edit existing queries by inserting query snippets or field names.

To construct a new query using the **Reference** panel, follow these steps:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  Click add\_box **SQL query** .

3.  Click quick\_reference\_all **Reference** .

4.  Click a recent or starred table or view. You can also use the search bar to find tables and views.

5.  Click more\_vert **View actions** , and then click **Insert query snippet** .

6.  Optional: You can preview the schema details of the table or view, or open them in a new tab.

7.  You can now either edit the query manually or insert field names directly into your query. To insert a field name, point to and click a place in the query editor where you want to insert the field name, and then click the field name in the **Reference** panel.

## Query settings

When you run a query, you can specify the following settings:

  - A [destination table](/bigquery/docs/writing-results#permanent-table) for the query results.

  - The priority of the job.

  - Whether to use [cached query results](/bigquery/docs/cached-results) .

  - The job timeout in milliseconds.

  - Whether to use [session mode](/bigquery/docs/sessions-intro) .

  - The type of [encryption](/bigquery/docs/encryption-at-rest) to use.

  - The maximum number of bytes billed for the query.

  - The [dialect of SQL](/bigquery/docs/introduction-sql) to use.

  - The [location](/bigquery/docs/locations) in which to run the query. The query must run in the same location as any tables referenced in the query.

  - The [reservation](/bigquery/docs/reservations-workload-management) to run your query in.

## Optional job creation mode

Optional job creation mode can improve the overall latency of queries that run for a short duration, such as those from dashboards or data exploration workloads. This mode executes the query and returns the results inline for `  SELECT  ` statements without requiring the use of [`  jobs.getQueryResults  `](/bigquery/docs/reference/rest/v2/jobs/getQueryResults) to fetch the results. Queries using optional job creation mode don't create a job when executed unless BigQuery determines that a job creation is necessary to complete the query.

To enable optional job creation mode, set the `  jobCreationMode  ` field of the [QueryRequest](/bigquery/docs/reference/rest/v2/jobs/query#QueryRequest) instance to `  JOB_CREATION_OPTIONAL  ` in the [`  jobs.query  `](/bigquery/docs/reference/rest/v2/jobs/query) request body.

When the value of this field is set to `  JOB_CREATION_OPTIONAL  ` , BigQuery determines if the query can use the optional job creation mode. If so, BigQuery executes the query and returns all results in the `  rows  ` field of the response. Since a job isn't created for this query, BigQuery doesn't return a `  jobReference  ` in the response body. Instead, it returns a `  queryId  ` field, which you can use to get insights about the query using the [`  INFORMATION_SCHEMA.JOBS  ` view](/bigquery/docs/information-schema-jobs#optional-job-creation) . Since no job is created, there is no `  jobReference  ` that can be passed to [`  jobs.get  `](/bigquery/docs/reference/rest/v2/jobs/get) and [`  jobs.getQueryResults  `](/bigquery/docs/reference/rest/v2/jobs/getQueryResults) APIs to lookup these queries.

If BigQuery determines that a job is required to complete the query, a `  jobReference  ` is returned. You can inspect the `  job_creation_reason  ` field in [`  INFORMATION_SCHEMA.JOBS  ` view](/bigquery/docs/information-schema-jobs#optional-job-creation) to determine the reason that a job was created for the query. In this case, you should use [`  jobs.getQueryResults  `](/bigquery/docs/reference/rest/v2/jobs/getQueryResults) to fetch the results when the query is complete.

When you use the `  JOB_CREATION_OPTIONAL  ` value, the `  jobReference  ` field might not be present in the response. Check if the field exists before accessing it.

When `  JOB_CREATION_OPTIONAL  ` is specified for multi-statement queries (scripts), BigQuery might optimize the execution process. As part of this optimization, BigQuery might determine that it can complete the script by creating fewer job resources than the number of individual statements, potentially even executing the entire script without creating any job at all. This optimization depends on BigQuery's assessment of the script, and the optimization might not be applied in every case. The optimization is fully automated by the system. No user controls or actions are required.

To run a query using optional job creation mode, select one of the following options:

### Console

1.  Go to the **BigQuery** page.

2.  Click add\_box **SQL query** .

3.  In the query editor, enter a valid GoogleSQL query.
    
    For example, query the [BigQuery public dataset `  usa_names  `](https://console.cloud.google.com/bigquery?p=bigquery-public-data&d=usa_names&page=dataset) to determine the most common names in the United States between the years 1910 and 2013:
    
    ``` text
    SELECT
      name, gender,
      SUM(number) AS total
    FROM
      `bigquery-public-data.usa_names.usa_1910_2013`
    GROUP BY
      name, gender
    ORDER BY
      total DESC
    LIMIT
      10;
    ```

4.  Click settings **More** , and then choose the **Optional job creation** query mode. To confirm this choice, click **Confirm** .

5.  Click play\_circle **Run** .

### bq

1.  In the Google Cloud console, activate Cloud Shell.
    
    At the bottom of the Google Cloud console, a [Cloud Shell](/shell/docs/how-cloud-shell-works) session starts and displays a command-line prompt. Cloud Shell is a shell environment with the Google Cloud CLI already installed and with values already set for your current project. It can take a few seconds for the session to initialize.

2.  Use the [`  bq query  ` command](/bigquery/docs/reference/bq-cli-reference#bq_query) and specify the `  --job_creation_mode=JOB_CREATION_OPTIONAL  ` flag. In the following example, the `  --use_legacy_sql=false  ` flag lets you use GoogleSQL syntax.
    
    ``` text
    bq query \
        --rpc=true \
        --use_legacy_sql=false \
        --job_creation_mode=JOB_CREATION_OPTIONAL \
        --location=LOCATION \
        'QUERY'
    ```
    
    Replace QUERY with a valid GoogleSQL query, and replace LOCATION with a valid region where the dataset is located. For example, query the [BigQuery public dataset `  usa_names  `](https://console.cloud.google.com/bigquery?p=bigquery-public-data&d=usa_names&page=dataset) to determine the most common names in the United States between the years 1910 and 2013:
    
    ``` text
    bq query \
        --rpc=true \
        --use_legacy_sql=false \
        --job_creation_mode=JOB_CREATION_OPTIONAL \
        --location=us \
        'SELECT
          name, gender,
          SUM(number) AS total
        FROM
          `bigquery-public-data.usa_names.usa_1910_2013`
        GROUP BY
          name, gender
        ORDER BY
          total DESC
        LIMIT
          10;'
    ```
    
    The query job returns the output inline in the response.
    
    **Note:** you may use `  --apilog=stdout  ` to log API requests and responses to extract the `  queryId  ` if needed.

### API

To run a query in optional job creation mode using the API, [run a query synchronously](/bigquery/docs/reference/rest/v2/jobs/query) and populate the [`  QueryRequest  `](/bigquery/docs/reference/rest/v2/jobs/query#QueryRequest) property. Include the `  jobCreationMode  ` property and set its value to `  JOB_CREATION_OPTIONAL  ` .

Check the response. If `  jobComplete  ` equals `  true  ` and `  jobReference  ` is empty, read the results from the `  rows  ` field. You can also get the `  queryId  ` from the response.

If `  jobReference  ` is present, you can check `  jobCreationReason  ` for why a job was created by BigQuery. Poll for results by calling [`  getQueryResults  `](/bigquery/docs/reference/rest/v2/jobs/getQueryResults) . Poll until `  jobComplete  ` equals `  true  ` . Check for errors and warnings in the `  errors  ` list.

### Java

Available version: 2.51.0 and up

Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Java API reference documentation](/java/docs/reference/google-cloud-bigquery/latest/overview) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` java
import com.google.cloud.bigquery.BigQuery;
import com.google.cloud.bigquery.BigQueryException;
import com.google.cloud.bigquery.BigQueryOptions;
import com.google.cloud.bigquery.JobId;
import com.google.cloud.bigquery.QueryJobConfiguration;
import com.google.cloud.bigquery.QueryJobConfiguration.JobCreationMode;
import com.google.cloud.bigquery.TableResult;

// Sample demonstrating short mode query execution.
//
// This feature is controlled by setting the defaultJobCreationMode
// field in the BigQueryOptions used for the client. JOB_CREATION_OPTIONAL
// allows for the execution of queries without creating a job.
public class QueryJobOptional {

  public static void main(String[] args) {
    String query =
        "SELECT name, gender, SUM(number) AS total FROM "
            + "bigquery-public-data.usa_names.usa_1910_2013 GROUP BY "
            + "name, gender ORDER BY total DESC LIMIT 10";
    queryJobOptional(query);
  }

  public static void queryJobOptional(String query) {
    try {
      // Initialize client that will be used to send requests. This client only needs
      // to be created once, and can be reused for multiple requests.
      BigQueryOptions options = BigQueryOptions.getDefaultInstance();
      options.setDefaultJobCreationMode(JobCreationMode.JOB_CREATION_OPTIONAL);
      BigQuery bigquery = options.getService();

      // Execute the query. The returned TableResult provides access information
      // about the query execution as well as query results.
      TableResult results = bigquery.query(QueryJobConfiguration.of(query));

      JobId jobId = results.getJobId();
      if (jobId != null) {
        System.out.println("Query was run with job state.  Job ID: " + jobId.toString());
      } else {
        System.out.println("Query was run in short mode.  Query ID: " + results.getQueryId());
      }

      // Print the results.
      results
          .iterateAll()
          .forEach(
              row -> {
                System.out.print("name:" + row.get("name").getStringValue());
                System.out.print(", gender: " + row.get("gender").getStringValue());
                System.out.print(", total: " + row.get("total").getLongValue());
                System.out.println();
              });

    } catch (BigQueryException | InterruptedException e) {
      System.out.println("Query not performed \n" + e.toString());
    }
  }
}
```

To run a query with a proxy, see [Configuring a proxy](https://github.com/googleapis/google-cloud-java#configuring-a-proxy) .

### Python

Available version: 3.34.0 and up

Before trying this sample, follow the Python setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Python API reference documentation](/python/docs/reference/bigquery/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` python
# This example demonstrates executing a query without requiring an associated
# job.
from google.cloud import bigquery
from google.cloud.bigquery.enums import JobCreationMode

# Construct a BigQuery client object, specifying that the library should
# avoid creating jobs when possible.
client = bigquery.Client(
    default_job_creation_mode=JobCreationMode.JOB_CREATION_OPTIONAL
)

query = """
    SELECT
        name,
        gender,
        SUM(number) AS total
    FROM
        bigquery-public-data.usa_names.usa_1910_2013
    GROUP BY
        name, gender
    ORDER BY
        total DESC
    LIMIT 10
"""
# Run the query.  The returned `rows` iterator can return information about
# how the query was executed as well as the result data.
rows = client.query_and_wait(query)

if rows.job_id is not None:
    print("Query was run with job state.  Job ID: {}".format(rows.job_id))
else:
    print(
        "Query was run without creating a job.  Query ID: {}".format(rows.query_id)
    )

print("The query data:")
for row in rows:
    # Row values can be accessed by field name or index.
    print("name={}, gender={}, total={}".format(row[0], row[1], row["total"]))
```

### Node

Available version: 8.1.0 and up

Before trying this sample, follow the Node.js setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Node.js API reference documentation](https://googleapis.dev/nodejs/bigquery/latest/index.html) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` javascript
// Demonstrates issuing a query that may be run in short query mode.

// Import the Google Cloud client library
const {BigQuery} = require('@google-cloud/bigquery');
const bigquery = new BigQuery({
  // default behavior is to create jobs when using the jobs.query API
  defaultJobCreationMode: 'JOB_CREATION_REQUIRED',
});

async function queryJobOptional() {
  // SQL query to run.

  const sqlQuery = `
    SELECT name, gender, SUM(number) AS total
    FROM bigquery-public-data.usa_names.usa_1910_2013
    GROUP BY name, gender
    ORDER BY total DESC
    LIMIT 10`;

  // Run the query
  const [rows, , res] = await bigquery.query({
    query: sqlQuery,
    // Skip job creation to enable short mode.
    jobCreationMode: 'JOB_CREATION_OPTIONAL',
  });

  if (!res.jobReference) {
    console.log(`Query was run in short mode. Query ID: ${res.queryId}`);
  } else {
    const jobRef = res.jobReference;
    const qualifiedId = `${jobRef.projectId}.${jobRef.location}.${jobRef.jobId}`;
    console.log(
      `Query was run with job state. Job ID: ${qualifiedId}, Query ID: ${res.queryId}`,
    );
  }
  // Print the results
  console.log('Rows:');
  rows.forEach(row => console.log(row));
}
```

### Go

Available version: 1.69.0 and up

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

// queryJobOptional demonstrates issuing a query that doesn't require a
// corresponding job.
func queryJobOptional(w io.Writer, projectID string) error {
 // projectID := "my-project-id"
 ctx := context.Background()
 client, err := bigquery.NewClient(ctx, projectID,
     bigquery.WithDefaultJobCreationMode(bigquery.JobCreationModeOptional),
 )
 if err != nil {
     return fmt.Errorf("bigquery.NewClient: %w", err)
 }
 defer client.Close()

 q := client.Query(`
     SELECT
             name, gender,
             SUM(number) AS total
     FROM
         bigquery-public-data.usa_names.usa_1910_2013
     GROUP BY 
         name, gender
     ORDER BY
         total DESC
     LIMIT 10
     `)
 // Run the query and process the returned row iterator.
 it, err := q.Read(ctx)
 if err != nil {
     return fmt.Errorf("query.Read(): %w", err)
 }

 // The iterator provides information about the query execution.
 // Queries that were run in short query mode will not have the source job
 // populated.
 if it.SourceJob() == nil {
     fmt.Fprintf(w, "Query was run in optional job mode.  Query ID: %q\n", it.QueryID())
 } else {
     j := it.SourceJob()
     qualifiedJobID := fmt.Sprintf("%s:%s.%s", j.ProjectID(), j.Location(), j.ID())
     fmt.Fprintf(w, "Query was run with job state.  Job ID: %q, Query ID: %q\n",
         qualifiedJobID, it.QueryID())
 }

 // Print row data.
 for {
     var row []bigquery.Value
     err := it.Next(&row)
     if err == iterator.Done {
         break
     }
     if err != nil {
         return err
     }
     fmt.Fprintln(w, row)
 }
 return nil
}
```

### JDBC Driver

Available version: JDBC v1.6.1 and up

Requires setting `  JobCreationMode=2  ` in the connection string.

``` text
    jdbc:bigquery://https://www.googleapis.com/bigquery/v2:443;JobCreationMode=2;Location=US;
  
```

**Note:** you may append `  LogLevel=6;LogPath=log.txt  ` to the connection string to enable `  TRACE  ` level logging and extract troubleshooting information, including `  queryId  ` , if needed.

### ODBC Driver

Available version: ODBC v3.0.7.1016 and up

Requires setting `  JobCreationMode=2  ` in the `  .ini  ` file.

``` text
    [ODBC Data Sources]
    Sample DSN=Simba Google BigQuery ODBC Connector 64-bit
    [Sample DSN]
    JobCreationMode=2
  
```

**Note:** you may append `  LogLevel=6  ` and `  LogPath=log.txt  ` to the `  .ini  ` file to enable detailed level logging and extract troubleshooting information, including `  queryId  ` , if needed.

## Global queries

Queries are run in the location of the data that they reference. However, if a query references data stored in more than one location, a global query is executed. When running a global query, BigQuery is able to collect all necessary data from different locations in one place, perform a query, and return the results. Because global queries require transferring data between locations, they require additional permissions and can incur additional costs.

For more information about global queries, see [Global queries](/bigquery/docs/global-queries) .

## Quotas

For information about quotas related to interactive and batch queries, see [Query jobs](/bigquery/quotas#query_jobs) .

To troubleshoot quota errors related to queries, see the [BigQuery Troubleshooting page](/bigquery/docs/troubleshoot-quotas) . The following quota errors and their troubleshooting information are directly related to queries:

  - [Query queue limit errors](/bigquery/docs/troubleshoot-quotas#ts-query-queue-limit)
  - [Table imports or query appends quota errors](/bigquery/docs/troubleshoot-quotas#ts-table-import-quota)

## Monitor queries

You can get information about queries as they are executing by using the [jobs explorer](/bigquery/docs/admin-jobs-explorer) or by querying the [`  INFORMATION_SCHEMA.JOBS_BY_PROJECT  ` view](/bigquery/docs/information-schema-jobs) .

## Dry run

A dry run in BigQuery provides the following information:

  - estimate of charges in [on-demand mode](https://cloud.google.com/bigquery/pricing#on_demand_pricing)
  - validation of your query
  - approximate bytes processed by your query in [capacity mode](https://cloud.google.com/bigquery/pricing#capacity_compute_analysis_pricing)

Dry runs don't use query slots, and you are not charged for performing a dry run. You can use the estimate returned by a dry run to calculate query costs in the [pricing calculator](https://cloud.google.com/products/calculator) .

**Note:** A dry run of a federated query that uses an external data source might report a lower bound of 0 bytes of data, even if rows are returned. This is because the amount of data processed from the external table can't be determined until the actual query completes. Running the federated query still incurs a cost for processing this data.

### Perform a dry run

To perform a dry run, do the following:

### Console

1.  Go to the BigQuery page.

2.  Enter your query in the query editor.
    
    If the query is valid, then a check mark automatically appears along with the amount of data that the query will process. If the query is invalid, then an exclamation point appears along with an error message.

### bq

Enter a query like the following using the `  --dry_run  ` flag.

``` text
bq query \
--use_legacy_sql=false \
--dry_run \
'SELECT
   COUNTRY,
   AIRPORT,
   IATA
 FROM
   `project_id`.dataset.airports
 LIMIT
   1000'
 
```

For a valid query, the command produces the following response:

``` text
Query successfully validated. Assuming the tables are not modified,
running this query will process 10918 bytes of data.
```

**Note:** If your query processes a small amount of data, you might need to convert the bytes that are processed from KB to MB. MB is the smallest measure used by the pricing calculator.

### API

To perform a dry run by using the API, submit a query job with `  dryRun  ` set to `  true  ` in the [JobConfiguration](/bigquery/docs/reference/rest/v2/Job#jobconfiguration) type.

### Go

Before trying this sample, follow the Go setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Go API reference documentation](https://godoc.org/cloud.google.com/go/bigquery) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` go
import (
 "context"
 "fmt"
 "io"

 "cloud.google.com/go/bigquery"
)

// queryDryRun demonstrates issuing a dry run query to validate query structure and
// provide an estimate of the bytes scanned.
func queryDryRun(w io.Writer, projectID string) error {
 // projectID := "my-project-id"
 ctx := context.Background()
 client, err := bigquery.NewClient(ctx, projectID)
 if err != nil {
     return fmt.Errorf("bigquery.NewClient: %v", err)
 }
 defer client.Close()

 q := client.Query(`
 SELECT
     name,
     COUNT(*) as name_count
 FROM ` + "`bigquery-public-data.usa_names.usa_1910_2013`" + `
 WHERE state = 'WA'
 GROUP BY name`)
 q.DryRun = true
 // Location must match that of the dataset(s) referenced in the query.
 q.Location = "US"

 job, err := q.Run(ctx)
 if err != nil {
     return err
 }
 // Dry run is not asynchronous, so get the latest status and statistics.
 status := job.LastStatus()
 if err := status.Err(); err != nil {
     return err
 }
 fmt.Fprintf(w, "This query will process %d bytes\n", status.Statistics.TotalBytesProcessed)
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
import com.google.cloud.bigquery.Job;
import com.google.cloud.bigquery.JobInfo;
import com.google.cloud.bigquery.JobStatistics;
import com.google.cloud.bigquery.QueryJobConfiguration;

// Sample to run dry query on the table
public class QueryDryRun {

  public static void runQueryDryRun() {
    String query =
        "SELECT name, COUNT(*) as name_count "
            + "FROM `bigquery-public-data.usa_names.usa_1910_2013` "
            + "WHERE state = 'WA' "
            + "GROUP BY name";
    queryDryRun(query);
  }

  public static void queryDryRun(String query) {
    try {
      // Initialize client that will be used to send requests. This client only needs to be created
      // once, and can be reused for multiple requests.
      BigQuery bigquery = BigQueryOptions.getDefaultInstance().getService();

      QueryJobConfiguration queryConfig =
          QueryJobConfiguration.newBuilder(query).setDryRun(true).setUseQueryCache(false).build();

      Job job = bigquery.create(JobInfo.of(queryConfig));
      JobStatistics.QueryStatistics statistics = job.getStatistics();

      System.out.println(
          "Query dry run performed successfully." + statistics.getTotalBytesProcessed());
    } catch (BigQueryException e) {
      System.out.println("Query not performed \n" + e.toString());
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

async function queryDryRun() {
  // Runs a dry query of the U.S. given names dataset for the state of Texas.

  const query = `SELECT name
    FROM \`bigquery-public-data.usa_names.usa_1910_2013\`
    WHERE state = 'TX'
    LIMIT 100`;

  // For all options, see https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query
  const options = {
    query: query,
    // Location must match that of the dataset(s) referenced in the query.
    location: 'US',
    dryRun: true,
  };

  // Run the query as a job
  const [job] = await bigquery.createQueryJob(options);

  // Print the status and statistics
  console.log('Status:');
  console.log(job.metadata.status);
  console.log('\nJob Statistics:');
  console.log(job.metadata.statistics);
}
```

### PHP

Before trying this sample, follow the PHP setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery PHP API reference documentation](/php/docs/reference/cloud-bigquery/latest/BigQueryClient) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` php
use Google\Cloud\BigQuery\BigQueryClient;

/** Uncomment and populate these variables in your code */
// $projectId = 'The Google project ID';
// $query = 'SELECT id, view_count FROM `bigquery-public-data.stackoverflow.posts_questions`';

// Construct a BigQuery client object.
$bigQuery = new BigQueryClient([
    'projectId' => $projectId,
]);

// Set job configs
$jobConfig = $bigQuery->query($query);
$jobConfig->useQueryCache(false);
$jobConfig->dryRun(true);

// Extract query results
$queryJob = $bigQuery->startJob($jobConfig);
$info = $queryJob->info();

printf('This query will process %s bytes' . PHP_EOL, $info['statistics']['totalBytesProcessed']);
```

### Python

Set the [QueryJobConfig.dry\_run](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJob#google_cloud_bigquery_job_QueryJob_dry_run) property to `  True  ` . [Client.query()](/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client#google_cloud_bigquery_client_Client_query) always returns a completed [QueryJob](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJob#google_cloud_bigquery_job_QueryJob) when provided a dry run query configuration.

Before trying this sample, follow the Python setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Python API reference documentation](/python/docs/reference/bigquery/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` python
from google.cloud import bigquery

# Construct a BigQuery client object.
client = bigquery.Client()

job_config = bigquery.QueryJobConfig(dry_run=True, use_query_cache=False)

# Start the query, passing in the extra configuration.
query_job = client.query(
    (
        "SELECT name, COUNT(*) as name_count "
        "FROM `bigquery-public-data.usa_names.usa_1910_2013` "
        "WHERE state = 'WA' "
        "GROUP BY name"
    ),
    job_config=job_config,
)  # Make an API request.

# A dry run query completes immediately.
print("This query will process {} bytes.".format(query_job.total_bytes_processed))
```

## What's next

  - Learn how to [manage query jobs](/bigquery/docs/managing-jobs) .
  - Learn how to [view query history](/bigquery/docs/managing-jobs#list_jobs_in_a_project) .
  - Learn how to [save and share queries](/bigquery/docs/saving-sharing-queries) .
  - Learn about [query queues](/bigquery/docs/query-queues) .
  - Learn how to [write query results](/bigquery/docs/writing-results) .
