# Read data with BigQuery API using pagination

This document describes how to read table data and query results with the BigQuery API using pagination.

## Page through results using the API

All `  *collection*.list  ` methods return paginated results under certain circumstances. The `  maxResults  ` property limits the number of results per page.

<table>
<thead>
<tr class="header">
<th>Method</th>
<th>Pagination criteria</th>
<th>Default <code dir="ltr" translate="no">       maxResults      </code> value</th>
<th>Maximum <code dir="ltr" translate="no">       maxResults      </code> value</th>
<th>Maximum <code dir="ltr" translate="no">       maxFieldValues      </code> value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       tabledata.list      </code></td>
<td>Returns paginated results if the response size is more than 10 MB <sup>1</sup> of data or more than <code dir="ltr" translate="no">       maxResults      </code> rows.</td>
<td>Unlimited</td>
<td>Unlimited</td>
<td>Unlimited</td>
</tr>
<tr class="even">
<td>All other <code dir="ltr" translate="no">       *collection*.list      </code> methods</td>
<td>Returns paginated results if the response is more than <code dir="ltr" translate="no">       maxResults      </code> rows and also less than the maximum limits.</td>
<td>10,000</td>
<td>Unlimited</td>
<td>300,000</td>
</tr>
</tbody>
</table>

If the result is larger than the byte or field limit, the result is trimmed to fit the limit. If one row is greater than the byte or field limit, `  tabledata.list  ` can return up to 100 MB of data <sup>1</sup> , which is consistent with the maximum row size limit for query results. There is no minimum size per page, and some pages might return more rows than others.

<sup>1</sup> The row size is approximate, as the size is based on the internal representation of row data. The maximum row size limit is enforced during certain stages of query job execution.

`  jobs.getQueryResults  ` can return 20 MB of data unless explicitly requested more through support.

A page is a subset of the total number of rows. If your results are more than one page of data, the result data has a `  pageToken  ` property. To retrieve the next page of results, make another `  list  ` call and include the token value as a URL parameter named `  pageToken  ` .

The [`  tabledata.list  `](/bigquery/docs/reference/rest/v2/tabledata/list) method, which is used to page through table data, uses a row offset value or a page token. See [Browsing table data](/bigquery/docs/managing-table-data#browse-table) for information.

## Iterate through client libraries results

The cloud client libraries handle the low-level details of API pagination and provide a more iterator-like experience that simplifies interaction with the individual elements in the page responses.

The following samples demonstrate paging through BigQuery table data.

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

### Node.js

Before trying this sample, follow the Node.js setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Node.js API reference documentation](https://googleapis.dev/nodejs/bigquery/latest/index.html) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

The [Cloud Client Libraries for Node.js](https://googleapis.dev/nodejs/bigquery/latest/index.html) automatically paginates by default, so you do not need to implement pagination yourself, for example:

``` javascript
// Import the Google Cloud client library using default credentials
const {BigQuery} = require('@google-cloud/bigquery');
const bigquery = new BigQuery();

async function browseTable() {
  // Retrieve a table's rows using manual pagination.

  /**
   * TODO(developer): Uncomment the following lines before running the sample.
   */
  // const datasetId = 'my_dataset'; // Existing dataset
  // const tableId = 'my_table'; // Table to create

  const query = `SELECT name, SUM(number) as total_people
    FROM \`bigquery-public-data.usa_names.usa_1910_2013\`
    GROUP BY name 
    ORDER BY total_people 
    DESC LIMIT 100`;

  // Create table reference.
  const dataset = bigquery.dataset(datasetId);
  const destinationTable = dataset.table(tableId);

  // For all options, see https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#jobconfigurationquery
  const queryOptions = {
    query: query,
    destination: destinationTable,
  };

  // Run the query as a job
  const [job] = await bigquery.createQueryJob(queryOptions);

  // For all options, see https://cloud.google.com/bigquery/docs/reference/v2/jobs/getQueryResults
  const queryResultsOptions = {
    // Retrieve zero resulting rows.
    maxResults: 0,
  };

  // Wait for the job to finish.
  await job.getQueryResults(queryResultsOptions);

  function manualPaginationCallback(err, rows, nextQuery) {
    rows.forEach(row => {
      console.log(`name: ${row.name}, ${row.total_people} total people`);
    });

    if (nextQuery) {
      // More results exist.
      destinationTable.getRows(nextQuery, manualPaginationCallback);
    }
  }

  // For all options, see https://cloud.google.com/bigquery/docs/reference/v2/tabledata/list
  const getRowsOptions = {
    autoPaginate: false,
    maxResults: 20,
  };

  // Retrieve all rows.
  destinationTable.getRows(getRowsOptions, manualPaginationCallback);
}
browseTable();
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

The [Cloud Client Libraries for Python](/python/docs/reference/bigquery/latest) automatically paginates by default, so you do not need to implement pagination yourself, for example:

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

## Request arbitrary pages and avoid redundant list calls

When you page backwards or jump to arbitrary pages using cached `  pageToken  ` values, it is possible that the data in your pages might have changed since it was last viewed but there is no clear indication that the data might have changed. To mitigate this, you can use the `  etag  ` property.

Every `  collection.list  ` method (except for Tabledata) returns an `  etag  ` property in the result. This property is a hash of the page results that can be used to verify whether the page has changed since the last request. When you make a request to BigQuery with an ETag value, BigQuery compares the ETag value to the ETag value returned by the API and responds based on whether the ETag values match. You can use ETags to avoid redundant list calls as follows:

  - To return list values if the values have changed.
    
    If you only want to return a page of list values if the values have changed, you can make a list call with a previously-stored ETag using the [HTTP "if-none-match" header](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.26) . If the ETag you provide doesn't match the ETag on the server, BigQuery returns a page of new list values. If the ETags do match, BigQuery returns an `  HTTP 304 Not Modified  ` status code and no values. An example of this might be a web page where users might periodically fill in information that is stored in BigQuery. If there are no changes to your data, you can avoid making redundant list calls to BigQuery by using the if-none-match header with ETags.

  - To return list values if the values have not changed.
    
    If you only want to return a page of list values if the list values have not changed, you can use the [HTTP "if-match" header](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.24) . BigQuery matches the ETag values and returns the page of results if the results have not changed or returns a 412 "Precondition Failed" result if the page has changed.

**Note:** Although ETags are a great way to avoid making redundant list calls, you can apply the same methods to identifying if any objects have changed. For example, you can perform a Get request for a specific table and use ETags to determine if the table has changed before returning the full response.

## Page through query results

Each query writes to a destination table. If no destination table is provided, the BigQuery API automatically populates the destination table property with a reference to a [temporary anonymous table](/bigquery/docs/writing-results#temporary_and_permanent_tables) .

### API

Read the [`  jobs.config.query.destinationTable  `](/bigquery/docs/reference/rest/v2/Job#JobConfigurationQuery.FIELDS.destination_table) field to determine the table that query results have been written to. Call the [`  tabledata.list  `](/bigquery/docs/reference/rest/v2/tabledata/list) to read the query results.

### Java

Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Java API reference documentation](/java/docs/reference/google-cloud-bigquery/latest/overview) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` java
import com.google.cloud.bigquery.BigQuery;
import com.google.cloud.bigquery.BigQueryException;
import com.google.cloud.bigquery.BigQueryOptions;
import com.google.cloud.bigquery.QueryJobConfiguration;
import com.google.cloud.bigquery.TableId;
import com.google.cloud.bigquery.TableResult;

// Sample to run query with pagination.
public class QueryPagination {

  public static void main(String[] args) {
    String datasetName = "MY_DATASET_NAME";
    String tableName = "MY_TABLE_NAME";
    String query =
        "SELECT name, SUM(number) as total_people"
            + " FROM `bigquery-public-data.usa_names.usa_1910_2013`"
            + " GROUP BY name"
            + " ORDER BY total_people DESC"
            + " LIMIT 100";
    queryPagination(datasetName, tableName, query);
  }

  public static void queryPagination(String datasetName, String tableName, String query) {
    try {
      // Initialize client that will be used to send requests. This client only needs to be created
      // once, and can be reused for multiple requests.
      BigQuery bigquery = BigQueryOptions.getDefaultInstance().getService();

      TableId tableId = TableId.of(datasetName, tableName);
      QueryJobConfiguration queryConfig =
          QueryJobConfiguration.newBuilder(query)
              // save results into a table.
              .setDestinationTable(tableId)
              .build();

      bigquery.query(queryConfig);

      TableResult results =
          bigquery.listTableData(tableId, BigQuery.TableDataListOption.pageSize(20));

      // First Page
      results
          .getValues()
          .forEach(row -> row.forEach(val -> System.out.printf("%s,\n", val.toString())));

      while (results.hasNextPage()) {
        // Remaining Pages
        results = results.getNextPage();
        results
            .getValues()
            .forEach(row -> row.forEach(val -> System.out.printf("%s,\n", val.toString())));
      }

      System.out.println("Query pagination performed successfully.");
    } catch (BigQueryException | InterruptedException e) {
      System.out.println("Query not performed \n" + e.toString());
    }
  }
}
```

To set the number of rows returned on each page, use a [`  GetQueryResults  ` job](/java/docs/reference/google-cloud-bigquery/latest/com.google.cloud.bigquery.Job#com_google_cloud_bigquery_Job_getQueryResults_com_google_cloud_bigquery_BigQuery_QueryResultsOption____) and set the [`  pageSize  ` option](/java/docs/reference/google-cloud-bigquery/latest/com.google.cloud.bigquery.BigQuery.QueryResultsOption#com_google_cloud_bigquery_BigQuery_QueryResultsOption_pageSize_long_) of the [`  QueryResultsOption  ` object](/java/docs/reference/google-cloud-bigquery/latest/com.google.cloud.bigquery.BigQuery.QueryResultsOption) that you pass in, as shown in the following example:

``` text
TableResult result = job.getQueryResults();
QueryResultsOption queryResultsOption = QueryResultsOption.pageSize(20);

TableResult result = job.getQueryResults(queryResultsOption);
```

### Node.js

Before trying this sample, follow the Node.js setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Node.js API reference documentation](https://googleapis.dev/nodejs/bigquery/latest/index.html) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` javascript
// Import the Google Cloud client library using default credentials
const {BigQuery} = require('@google-cloud/bigquery');
const bigquery = new BigQuery();

async function queryPagination() {
  // Run a query and get rows using automatic pagination.

  const query = `SELECT name, SUM(number) as total_people
  FROM \`bigquery-public-data.usa_names.usa_1910_2013\`
  GROUP BY name
  ORDER BY total_people DESC
  LIMIT 100`;

  // Run the query as a job.
  const [job] = await bigquery.createQueryJob(query);

  // Wait for job to complete and get rows.
  const [rows] = await job.getQueryResults();

  console.log('Query results:');
  rows.forEach(row => {
    console.log(`name: ${row.name}, ${row.total_people} total people`);
  });
}
queryPagination();
```

### Python

The [`  QueryJob.result  `](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJob#google_cloud_bigquery_job_QueryJob_result) method returns an iterable of the query results. Alternatively,

1.  Read the [`  QueryJob.destination  `](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJob#google_cloud_bigquery_job_QueryJob_destination) property. If this property is not configured, it is set by the API to a reference to a [temporary anonymous table](/bigquery/docs/writing-results#temporary_and_permanent_tables) .
2.  Get the table schema with the [`  Client.get_table  `](/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client#google_cloud_bigquery_client_Client_get_table) method.
3.  Create an iterable over all rows in the destination table with the [`  Client.list_rows  `](/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client#google_cloud_bigquery_client_Client_list_rows) method.

Before trying this sample, follow the Python setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Python API reference documentation](/python/docs/reference/bigquery/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` python
from google.cloud import bigquery

# Construct a BigQuery client object.
client = bigquery.Client()

query = """
    SELECT name, SUM(number) as total_people
    FROM `bigquery-public-data.usa_names.usa_1910_2013`
    GROUP BY name
    ORDER BY total_people DESC
"""
query_job = client.query(query)  # Make an API request.
query_job.result()  # Wait for the query to complete.

# Get the destination table for the query results.
#
# All queries write to a destination table. If a destination table is not
# specified, the BigQuery populates it with a reference to a temporary
# anonymous table after the query completes.
destination = query_job.destination

# Get the schema (and other properties) for the destination table.
#
# A schema is useful for converting from BigQuery types to Python types.
destination = client.get_table(destination)

# Download rows.
#
# The client library automatically handles pagination.
print("The query data:")
rows = client.list_rows(destination, max_results=20)
for row in rows:
    print("name={}, count={}".format(row["name"], row["total_people"]))
```
