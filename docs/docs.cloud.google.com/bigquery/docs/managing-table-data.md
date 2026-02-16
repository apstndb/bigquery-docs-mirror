# Managing table data

This document describes how to manage table data in BigQuery. You can work with BigQuery table data in the following ways:

  - Load data into a table
  - Append to or overwrite table data
  - Browse (or preview) table data
  - Query table data
  - Modify table data using data manipulation language (DML)
  - Copy table data
  - Export table data

For information on managing table schemas, see [Modifying table schemas](/bigquery/docs/managing-table-schemas) .

## Before you begin

Grant roles that give the necessary permissions to users who need to perform each task in this document. Permissions required (if any) to perform a task are listed in the "Required permissions" section of the task.

## Loading data into a table

You can [load data](/bigquery/docs/loading-data) when you create a table, or you can create an empty table and load the data later. When you load data, you can use [schema auto-detect](/bigquery/docs/schema-detect) for supported data formats, or you can [specify the schema](/bigquery/docs/schemas) .

For more information on loading data, see the documentation for your source data's format and location:

  - For more information on loading data from Cloud Storage, see:
    
      - [Loading Avro data](/bigquery/docs/loading-data-cloud-storage-avro)
      - [Loading CSV data](/bigquery/docs/loading-data-cloud-storage-csv)
      - [Loading JSON data](/bigquery/docs/loading-data-cloud-storage-json)
      - [Loading Parquet data](/bigquery/docs/loading-data-cloud-storage-parquet)
      - [Loading ORC data](/bigquery/docs/loading-data-cloud-storage-orc)
      - [Loading data from Datastore exports](/bigquery/docs/loading-data-cloud-datastore)
      - [Loading data from Firestore exports](/bigquery/docs/loading-data-cloud-firestore)

  - For more information on loading data from a local source, see [Loading data from local files](/bigquery/docs/batch-loading-data) .

## Appending to and overwriting table data

You can overwrite table data using a load or query operation. You can append additional data to an existing table by performing a load-append operation or by appending query results to the table.

For more information on appending to or overwriting a table when loading data, see the documentation for your source data format:

  - [Appending to or overwriting a table with Avro data](/bigquery/docs/loading-data-cloud-storage-avro#appending_to_or_overwriting_a_table_with_avro_data)
  - [Appending to or overwriting a table with CSV data](/bigquery/docs/loading-data-cloud-storage-csv#appending_to_or_overwriting_a_table_with_csv_data)
  - [Appending to or overwriting a table with JSON data](/bigquery/docs/loading-data-cloud-storage-json#appending_to_or_overwriting_a_table_with_json_data)
  - [Appending to or overwriting a table with Parquet data](/bigquery/docs/loading-data-cloud-storage-parquet#appending_to_or_overwriting_a_table_with_parquet_data)
  - [Appending to or overwriting a table with ORC data](/bigquery/docs/loading-data-cloud-storage-orc#append_to_or_overwrite_a_table_with_orc_data)
  - [Appending to or overwriting a table with Datastore data](/bigquery/docs/loading-data-cloud-datastore#appending_to_or_overwriting_a_table_with_cloud_datastore_data)

To append to or overwrite a table using query results, specify a destination table and set the write disposition to either:

  - **Append to table** — Appends the query results to an existing table.
  - **Overwrite table** — Overwrites an existing table with the same name using the query results.

You can use the following query to append records from one table to another:

``` text
  INSERT INTO <projectID>.<datasetID>.<table1> (
    <column2>,
    <column3>) (SELECT * FROM <projectID>.<datasetID>.<table2>)
```

For more information on using query results to append to or overwrite data, see [Writing query results](/bigquery/docs/writing-results#writing_query_results) .

## Browsing table data

You can browse or read table data by:

  - Using the Google Cloud console
  - Using the bq command-line tool's `  bq head  ` command
  - Calling the [`  tabledata.list  `](/bigquery/docs/reference/rest/v2/tabledata/list) API method
  - Using the client libraries

### Required permissions

To read table and partition data, you need the `  bigquery.tables.getData  ` Identity and Access Management (IAM) permission.

**Note:** Consider [special cases](/bigquery/docs/control-access-to-resources-iam#special_cases) when creating an [IAM deny policy](/iam/docs/deny-overview) on the `  bigquery.tables.getData  ` permission.

Each of the following predefined IAM roles includes the permissions that you need in order to browse table and partition data:

  - `  roles/bigquery.dataViewer  `
  - `  roles/bigquery.dataEditor  `
  - `  roles/bigquery.dataOwner  `
  - `  roles/bigquery.admin  `

If you have the `  bigquery.datasets.create  ` permission, you can browse data in the tables and partitions of the datasets you create.

For more information on IAM roles and permissions in BigQuery, see [Predefined roles and permissions](/bigquery/docs/access-control) .

### Browsing table data

To browse table data:

### Console

1.  In the Google Cloud console, open the BigQuery page.

2.  In the left pane, click explore **Explorer** :
    
    If you don't see the left pane, click last\_page **Expand left pane** to open the pane.

3.  In the **Explorer** pane, expand your project, click **Datasets** , and then select a dataset.

4.  Click **Overview \> Tables** , and then select the table.

5.  Click **Details** and note the value in **Number of rows** . You may need this value to control the starting point for your results using the bq command-line tool or API.

6.  Click **Preview** . A sample set of data is displayed.

### Command-line

Issue the `  bq head  ` command with the `  --max_rows  ` flag to list all columns in a particular number of table rows. If `  --max_rows  ` is not specified, the default is 100.

To browse a subset of columns in the table (including nested and repeated columns), use the `  --selected_fields  ` flag and enter the columns as a comma- separated list.

To specify the number of rows to skip before displaying table data, use the `  --start_row= integer  ` flag (or the `  -s  ` shortcut). The default value is `  0  ` . You can retrieve the number of rows in a table by using the `  bq show  ` command to [retrieve table information](/bigquery/docs/tables#get_information_about_tables) .

If the table you're browsing is in a project other than your default project, add the project ID to the command in the following format: `  project_id:dataset.table  ` .

``` text
bq head \
--max_rows integer1 \
--start_row integer2 \
--selected_fields "columns" \
project_id:dataset.table
```

Where:

  - integer1 is the number of rows to display.
  - integer2 is the number of rows to skip before displaying data.
  - columns is a comma-separated list of columns.
  - project\_id is your project ID.
  - dataset is the name of the dataset containing the table.
  - table is the name of the table to browse.

Examples:

Enter the following command to list all columns in the first 10 rows in `  mydataset.mytable  ` . `  mydataset  ` is in your default project.

``` text
bq head --max_rows=10 mydataset.mytable
```

Enter the following command to list all columns in the first 100 rows in `  mydataset.mytable  ` . `  mydataset  ` is in `  myotherproject  ` , not your default project.

``` text
bq head myotherproject:mydataset.mytable
```

Enter the following command to display only `  field1  ` and `  field2  ` in `  mydataset.mytable  ` . The command uses the `  --start_row  ` flag to skip to row 100. `  mydataset.mytable  ` is in your default project.

``` text
bq head --start_row 100 --selected_fields "field1,field2" mydataset.mytable
```

Because the `  bq head  ` command does not create a query job, `  bq head  ` commands do not appear in your query history, and you are not charged for them.

### API

Browse through a table's data by calling [`  tabledata.list  `](/bigquery/docs/reference/rest/v2/tabledata/list) . Specify the name of the table in the `  tableId  ` parameter.

Configure these optional parameters to control the output:

  - `  maxResults  ` — Maximum number of results to return
  - `  selectedFields  ` — Comma-separated list of columns to return; If unspecified, all columns are returned
  - `  startIndex  ` — Zero-based index of the starting row to read

**Note:** If you request a `  startIndex  ` beyond the last row, the method will return successfully but without a `  rows  ` property. You can find out how many rows are in your table by calling the [`  tables.get  `](/bigquery/docs/reference/rest/v2/tables/get) method and examining the `  numRows  ` property.

Values are returned wrapped in a JSON object that you must parse, as described in the [`  tabledata.list  `](/bigquery/docs/reference/rest/v2/tabledata/list) reference documentation.

### C\#

Before trying this sample, follow the C\# setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery C\# API reference documentation](/dotnet/docs/reference/Google.Cloud.BigQuery.V2/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` csharp
using Google.Api.Gax;
using Google.Apis.Bigquery.v2.Data;
using Google.Cloud.BigQuery.V2;
using System;
using System.Linq;

public class BigQueryBrowseTable
{
    public void BrowseTable(
        string projectId = "your-project-id"
    )
    {
        BigQueryClient client = BigQueryClient.Create(projectId);
        TableReference tableReference = new TableReference()
        {
            TableId = "shakespeare",
            DatasetId = "samples",
            ProjectId = "bigquery-public-data"
        };
        // Load all rows from a table
        PagedEnumerable<TableDataList, BigQueryRow> result = client.ListRows(
            tableReference: tableReference,
            schema: null
        );
        // Print the first 10 rows
        foreach (BigQueryRow row in result.Take(10))
        {
            Console.WriteLine($"{row["corpus"]}: {row["word_count"]}");
        }
    }
}
```

### Go

Before trying this sample, follow the Go setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Go API reference documentation](https://godoc.org/cloud.google.com/go/bigquery) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

The [Cloud Client Libraries for Go](/bigquery/docs/reference/libraries) automatically paginates by default, so you do not need to implement pagination yourself, for example:

``` go
import (
 "context"
 "fmt"
 "io"

 "cloud.google.com/go/bigquery"
 "google.golang.org/api/iterator"
)

// browseTable demonstrates reading data from a BigQuery table directly without the use of a query.
// For large tables, we also recommend the BigQuery Storage API.
func browseTable(w io.Writer, projectID, datasetID, tableID string) error {
 // projectID := "my-project-id"
 // datasetID := "mydataset"
 // tableID := "mytable"
 ctx := context.Background()
 client, err := bigquery.NewClient(ctx, projectID)
 if err != nil {
     return fmt.Errorf("bigquery.NewClient: %v", err)
 }
 defer client.Close()

 table := client.Dataset(datasetID).Table(tableID)
 it := table.Read(ctx)
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
import com.google.cloud.bigquery.BigQuery.TableDataListOption;
import com.google.cloud.bigquery.BigQueryException;
import com.google.cloud.bigquery.BigQueryOptions;
import com.google.cloud.bigquery.TableId;
import com.google.cloud.bigquery.TableResult;

// Sample to directly browse a table with optional paging
public class BrowseTable {

  public static void runBrowseTable() {
    // TODO(developer): Replace these variables before running the sample.
    String table = "MY_TABLE_NAME";
    String dataset = "MY_DATASET_NAME";
    browseTable(dataset, table);
  }

  public static void browseTable(String dataset, String table) {
    try {
      // Initialize client that will be used to send requests. This client only needs to be created
      // once, and can be reused for multiple requests.
      BigQuery bigquery = BigQueryOptions.getDefaultInstance().getService();

      // Identify the table itself
      TableId tableId = TableId.of(dataset, table);

      // Page over 100 records. If you don't need pagination, remove the pageSize parameter.
      TableResult result = bigquery.listTableData(tableId, TableDataListOption.pageSize(100));

      // Print the records
      result
          .iterateAll()
          .forEach(
              row -> {
                row.forEach(fieldValue -> System.out.print(fieldValue.toString() + ", "));
                System.out.println();
              });

      System.out.println("Query ran successfully");
    } catch (BigQueryException e) {
      System.out.println("Query failed to run \n" + e.toString());
    }
  }
}
```

### Node.js

Before trying this sample, follow the Node.js setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Node.js API reference documentation](https://googleapis.dev/nodejs/bigquery/latest/index.html) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

The [Cloud Client Libraries for Node.js](/bigquery/docs/reference/libraries) automatically paginates by default, so you do not need to implement pagination yourself, for example:

``` javascript
// Import the Google Cloud client library and create a client
const {BigQuery} = require('@google-cloud/bigquery');
const bigquery = new BigQuery();

async function browseRows() {
  // Displays rows from "my_table" in "my_dataset".

  /**
   * TODO(developer): Uncomment the following lines before running the sample.
   */
  // const datasetId = "my_dataset";
  // const tableId = "my_table";

  // List rows in the table
  const [rows] = await bigquery
    .dataset(datasetId)
    .table(tableId)
    .getRows();

  console.log('Rows:');
  rows.forEach(row => console.log(row));
}
```

### PHP

Before trying this sample, follow the PHP setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery PHP API reference documentation](/php/docs/reference/cloud-bigquery/latest/BigQueryClient) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

Pagination happens automatically in the [Cloud Client Libraries for PHP](/bigquery/docs/reference/libraries) using the generator function `  rows  ` , which fetches the next page of results during iteration.

``` php
use Google\Cloud\BigQuery\BigQueryClient;

/** Uncomment and populate these variables in your code */
// $projectId = 'The Google project ID';
// $datasetId = 'The BigQuery dataset ID';
// $tableId   = 'The BigQuery table ID';
// $maxResults = 10;

$maxResults = 10;
$startIndex = 0;

$options = [
    'maxResults' => $maxResults,
    'startIndex' => $startIndex
];
$bigQuery = new BigQueryClient([
    'projectId' => $projectId,
]);
$dataset = $bigQuery->dataset($datasetId);
$table = $dataset->table($tableId);
$numRows = 0;
foreach ($table->rows($options) as $row) {
    print('---');
    foreach ($row as $column => $value) {
        printf('%s: %s' . PHP_EOL, $column, $value);
    }
    $numRows++;
}
```

### Python

Before trying this sample, follow the Python setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Python API reference documentation](/python/docs/reference/bigquery/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` python
from google.cloud import bigquery

# Construct a BigQuery client object.
client = bigquery.Client()

# TODO(developer): Set table_id to the ID of the table to browse data rows.
# table_id = "your-project.your_dataset.your_table_name"

# Download all rows from a table.
rows_iter = client.list_rows(table_id)  # Make an API request.

# Iterate over rows to make the API requests to fetch row data.
rows = list(rows_iter)
print("Downloaded {} rows from table {}".format(len(rows), table_id))

# Download at most 10 rows.
rows_iter = client.list_rows(table_id, max_results=10)
rows = list(rows_iter)
print("Downloaded {} rows from table {}".format(len(rows), table_id))

# Specify selected fields to limit the results to certain columns.
table = client.get_table(table_id)  # Make an API request.
fields = table.schema[:2]  # First two columns.
rows_iter = client.list_rows(table_id, selected_fields=fields, max_results=10)
rows = list(rows_iter)
print("Selected {} columns from table {}.".format(len(rows_iter.schema), table_id))
print("Downloaded {} rows from table {}".format(len(rows), table_id))

# Print row data in tabular format.
rows = client.list_rows(table, max_results=10)
format_string = "{!s:<16} " * len(rows.schema)
field_names = [field.name for field in rows.schema]
print(format_string.format(*field_names))  # Prints column headers.
for row in rows:
    print(format_string.format(*row))  # Prints row data.
```

### Ruby

Before trying this sample, follow the Ruby setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Ruby API reference documentation](https://googleapis.dev/ruby/google-cloud-bigquery/latest/Google/Cloud/Bigquery.html) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

Pagination happens automatically in the [Cloud Client Libraries for Ruby](/bigquery/docs/reference/libraries) using `  Table#data  ` and `  Data#next  ` .

``` ruby
require "google/cloud/bigquery"

def browse_table
  bigquery = Google::Cloud::Bigquery.new project_id: "bigquery-public-data"
  dataset  = bigquery.dataset "samples"
  table    = dataset.table "shakespeare"

  # Load all rows from a table
  rows = table.data

  # Load the first 10 rows
  rows = table.data max: 10

  # Print row data
  rows.each { |row| puts row }
end
```

## Querying table data

You can [query BigQuery data](/bigquery/docs/running-queries) by using one of the following query job types:

  - **[Interactive query jobs](/bigquery/docs/running-queries#queries)** . By default, BigQuery runs queries as interactive query jobs, which are intended to start executing as quickly as possible.

  - **[Batch query jobs](/bigquery/docs/running-queries#batch)** . Batch queries have lower priority than interactive queries. When a project or reservation is using all of its available compute resources, batch queries are more likely to be queued and remain in the queue. After a batch query starts running, the batch query runs the same as an interactive query. For more information, see [query queues](/bigquery/docs/query-queues) .

  - **[Continuous query jobs](/bigquery/docs/continuous-queries-introduction)** . With these jobs, the query runs continuously, letting you analyze incoming data in BigQuery in real time and then write the results to a BigQuery table, or export the results to Bigtable or Pub/Sub. You can use this capability to perform time sensitive tasks, such as creating and immediately acting on insights, applying real time machine learning (ML) inference, and building event-driven data pipelines.

You can run query jobs by using the following methods:

  - Compose and run a query in the [Google Cloud console](/bigquery/bigquery-web-ui#overview) .
  - Run the `  bq query  ` command in the [bq command-line tool](/bigquery/bq-command-line-tool) .
  - Programmatically call the [`  jobs.query  `](/bigquery/docs/reference/v2/jobs/query) or [`  jobs.insert  `](/bigquery/docs/reference/v2/jobs/insert) method in the BigQuery [REST API](/bigquery/docs/reference/rest/v2) .
  - Use the BigQuery [client libraries](/bigquery/docs/reference/libraries) .

For more information on querying BigQuery tables, see [Introduction to querying BigQuery data](/bigquery/docs/query-overview) .

In addition to querying data stored in BigQuery tables, you can query data stored externally. For more information, see [Introduction to external data sources](/bigquery/external-data-sources) .

## Modifying table data

You can modify data in a table using data manipulation language (DML) statements in SQL. DML statements let you [update](/bigquery/docs/reference/standard-sql/dml-syntax#update_statement) , [merge](/bigquery/docs/reference/standard-sql/dml-syntax#merge_statement) , [insert](/bigquery/docs/reference/standard-sql/dml-syntax#insert_statement) , and [delete](/bigquery/docs/reference/standard-sql/dml-syntax#delete_statement) rows in tables. For syntax reference and examples of each type of DML statement, see [Data manipulation language statements in GoogleSQL](/bigquery/docs/reference/standard-sql/dml-syntax) .

The legacy SQL dialect does not support DML statements. To update or delete data using legacy SQL, you must delete the table and then recreate it with new data. Alternatively, you can write a query that modifies the data and write the query results to a new, destination table.

## Copying table data

You can copy a table by:

  - Using the Google Cloud console
  - Using the bq command-line tool's `  bq cp  ` command
  - Calling the [`  jobs.insert  ` API method](/bigquery/docs/reference/rest/v2/jobs/insert) and configuring a [copy job](/bigquery/docs/reference/rest/v2/Job#JobConfigurationTableCopy)
  - Using the client libraries

For more information on copying tables, see [Copying a table](/bigquery/docs/managing-tables#copy-table) .

## Exporting table data

You can export table data to a Cloud Storage bucket in CSV, JSON, Avro, or Parquet ( [Preview](https://cloud.google.com/products/#product-launch-stages) ) format. Exporting to your local machine is not supported; however, you can [download and save query results](/bigquery/docs/writing-results#downloading-saving-results-console) using the Google Cloud console.

For more information, see [Exporting table data](/bigquery/docs/exporting-data) .

## Table security

To control access to tables in BigQuery, see [Control access to resources with IAM](/bigquery/docs/control-access-to-resources-iam) .

## What's next

  - For more information on loading data, see [Introduction to loading data](/bigquery/docs/loading-data) .
  - For more information on querying data, see [Introduction to querying BigQuery data](/bigquery/docs/query-overview) .
  - For more information on modifying table schemas, see [Modifying table schemas](/bigquery/docs/managing-table-schemas) .
  - For more information on creating and using tables, see [Creating and using tables](/bigquery/docs/tables) .
  - For more information on managing tables, see [Managing tables](/bigquery/docs/managing-tables) .
