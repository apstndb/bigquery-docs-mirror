# Introduction to SQL in BigQuery

This document provides an overview of supported statements and SQL dialects in BigQuery.

GoogleSQL is an ANSI-compliant [Structured Query Language (SQL)](https://en.wikipedia.org/wiki/SQL) that includes the following types of supported statements:

  - [Query statements](/bigquery/docs/reference/standard-sql/query-syntax) , also known as Data Query Language (DQL) statements, are the primary method to analyze data in BigQuery. They scan one or more tables or expressions and return the computed result rows. Query statements can include [pipe syntax](/bigquery/docs/pipe-syntax) .

  - [Procedural language statements](/bigquery/docs/reference/standard-sql/procedural-language) are procedural extensions to GoogleSQL that allow you to execute multiple SQL statements in one request. Procedural statements can use variables and control-flow statements, and can have side effects.

  - [Data Definition Language (DDL) statements](/bigquery/docs/reference/standard-sql/data-definition-language) let you create and modify objects such as the following:
    
      - Datasets
      - Tables, including their schema and column types
      - Table clones and snapshots
      - Views
      - Functions
      - Indexes
      - Capacity commitments, reservations, and assignments
      - Row-level access policies

  - [Data Manipulation Language (DML) statements](/bigquery/docs/reference/standard-sql/dml-syntax) enable you to update, insert, and delete data from your BigQuery tables.

  - [Data Control Language (DCL) statements](/bigquery/docs/reference/standard-sql/data-control-language) let you control BigQuery system resources such as access and capacity.

  - [Transaction Control Language (TCL) statements](/bigquery/docs/reference/standard-sql/procedural-language#transactions) allow you to manage transactions for data modifications.

  - [Load statements](/bigquery/docs/reference/standard-sql/load-statements) and [export statements](/bigquery/docs/reference/standard-sql/export-statements) to manage data coming in and out of BigQuery.

## BigQuery SQL dialects

BigQuery supports the GoogleSQL dialect, but a legacy SQL dialect is also available. If you are new to BigQuery, you should use GoogleSQL as it supports the broadest range of functionality. For example, features such as DDL and DML statements are only supported using GoogleSQL. Legacy SQL is maintained for backward compatibility and we recommend that customers [migrate](/bigquery/docs/reference/standard-sql/migrating-from-legacy-sql) if they are using legacy SQL.

### Changing from the default dialect

The interface you use to query your data determines which query dialect is the default. To switch to a different dialect:

### Console

The default dialect for the Google Cloud console is GoogleSQL. To change the dialect to legacy SQL:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, click the **More \> Query settings** button.

3.  In the **Advanced options** section, for **SQL dialect** , click **Legacy** , then click **Save** . This sets the legacy SQL option for this query. When you click add\_box **SQL Query** to create a new query, you must select the legacy SQL option again.

### SQL

The default SQL dialect is GoogleSQL. You can set the SQL dialect by including the prefix `  #standardSQL  ` or `  #legacySQL  ` as part of your query. These query prefixes are not case-sensitive, must precede the query, and must be separated from the query by a newline character. The following example sets the dialect to legacy SQL and queries the natality dataset:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
    #legacySQL
    SELECT
      weight_pounds, state, year, gestation_weeks
    FROM
      [bigquery-public-data:samples.natality]
    ORDER BY
      weight_pounds DESC
    LIMIT
      10;
    ```

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](/bigquery/docs/running-queries#queries) .

### bq

The default query dialect in the `  bq  ` command-line tool is legacy SQL. To switch to the GoogleSQL dialect, add the `  --use_legacy_sql=false  ` or `  --nouse_legacy_sql  ` flag to your command-line statement.

**Switch to the GoogleSQL dialect**

To use GoogleSQL syntax in a query job, set the `  use_legacy_sql  ` parameter to `  false  ` .

``` text
  bq query \
  --use_legacy_sql=false \
  'SELECT
    word
  FROM
    `bigquery-public-data.samples.shakespeare`'
```

**Set GoogleSQL as the default dialect**

You can set GoogleSQL as the default dialect for the command-line tool and the interactive shell by editing the command-line tool's configuration file: `  .bigqueryrc  ` .

For more information on `  .bigqueryrc  ` , see [Setting default values for command-specific flags](/bigquery/docs/bq-command-line-tool#setting_default_values_for_command-line_flags) .

To set `  --use_legacy_sql=false  ` in `  .bigqueryrc  ` :

1.  Open `  .bigqueryrc  ` in a text editor. By default, `  .bigqueryrc  ` should be in your user directory, for example, `  $HOME/.bigqueryrc  ` .

2.  Add the following text to the file. This example sets GoogleSQL as the default syntax for queries and for the `  mk  ` command (used when you create a view). If you have already configured default values for `  query  ` or `  mk  ` command flags, you do not need to add `  [query]  ` or `  [mk]  ` again.
    
    ``` text
    [query]
    --use_legacy_sql=false
    [mk]
    --use_legacy_sql=false
    ```

3.  Save and close the file.

4.  If you are using the interactive shell, you must exit and restart for the changes to be applied.

For information on available command-line flags, see [bq command-line tool reference](/bigquery/docs/reference/bq-cli-reference) .

### C\#

Before trying this sample, follow the C\# setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery C\# API reference documentation](/dotnet/docs/reference/Google.Cloud.BigQuery.V2/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

By default, the C\# library uses GoogleSQL.

**Switch to the legacy SQL dialect**

To use legacy SQL syntax in a query job, set the `  UseLegacySql  ` parameter to `  true  ` .

``` csharp
using Google.Cloud.BigQuery.V2;
using System;

public class BigQueryQueryLegacy
{
    public void QueryLegacy(
        string projectId = "your-project-id"
    )
    {
        BigQueryClient client = BigQueryClient.Create(projectId);
        string query = @"
            SELECT name FROM [bigquery-public-data:usa_names.usa_1910_2013]
            WHERE state = 'TX'
            LIMIT 100";
        BigQueryJob job = client.CreateQueryJob(
            sql: query,
            parameters: null,
            options: new QueryOptions { UseLegacySql = true });
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

By default, the Go client library uses GoogleSQL.

**Switch to the legacy SQL dialect**

To use legacy SQL syntax in a query job, set the `  UseLegacySQL  ` property within the query configuration to `  true  ` .

``` go
import (
 "context"
 "fmt"
 "io"

 "cloud.google.com/go/bigquery"
 "google.golang.org/api/iterator"
)

// queryLegacy demonstrates running a query using Legacy SQL.
func queryLegacy(w io.Writer, projectID, sqlString string) error {
 // projectID := "my-project-id"
 // sqlString = "SELECT 3 as somenum"
 ctx := context.Background()
 client, err := bigquery.NewClient(ctx, projectID)
 if err != nil {
     return fmt.Errorf("bigquery.NewClient: %w", err)
 }
 defer client.Close()

 q := client.Query(sqlString)
 q.UseLegacySQL = true

 // Run the query and process the returned row iterator.
 it, err := q.Read(ctx)
 if err != nil {
     return fmt.Errorf("query.Read(): %w", err)
 }
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

By default, the Java client library uses GoogleSQL.

**Switch to the legacy SQL dialect**

To use legacy SQL syntax in a query job, set the `  useLegacySql  ` parameter to `  true  ` .

``` java
import com.google.cloud.bigquery.BigQuery;
import com.google.cloud.bigquery.BigQueryException;
import com.google.cloud.bigquery.BigQueryOptions;
import com.google.cloud.bigquery.QueryJobConfiguration;
import com.google.cloud.bigquery.TableResult;

public class RunLegacyQuery {

  public static void main(String[] args) {
    runLegacyQuery();
  }

  public static void runLegacyQuery() {
    try {
      // Initialize client that will be used to send requests. This client only needs to be created
      // once, and can be reused for multiple requests.
      BigQuery bigquery = BigQueryOptions.getDefaultInstance().getService();

      // To use legacy SQL syntax, set useLegacySql to true.
      String query =
          "SELECT corpus FROM [bigquery-public-data:samples.shakespeare] GROUP BY corpus;";
      QueryJobConfiguration queryConfig =
          QueryJobConfiguration.newBuilder(query).setUseLegacySql(true).build();

      // Execute the query.
      TableResult result = bigquery.query(queryConfig);

      // Print the results.
      result.iterateAll().forEach(rows -> rows.forEach(row -> System.out.println(row.getValue())));

      System.out.println("Legacy query ran successfully");
    } catch (BigQueryException | InterruptedException e) {
      System.out.println("Legacy query did not run \n" + e.toString());
    }
  }
}
```

### Node.js

Before trying this sample, follow the Node.js setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Node.js API reference documentation](https://googleapis.dev/nodejs/bigquery/latest/index.html) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

By default, the Node.js client library uses GoogleSQL.

**Switch to the legacy SQL dialect**

To use legacy SQL syntax in a query job, set the `  useLegacySql  ` parameter to `  true  ` .

``` javascript
// Import the Google Cloud client library
const {BigQuery} = require('@google-cloud/bigquery');
const bigquery = new BigQuery();

async function queryLegacy() {
  // Queries the U.S. given names dataset for the state of Texas using legacy SQL.

  const query =
    'SELECT word FROM [bigquery-public-data:samples.shakespeare] LIMIT 10;';

  // For all options, see https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query
  const options = {
    query: query,
    // Location must match that of the dataset(s) referenced in the query.
    location: 'US',
    useLegacySql: true,
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

By default, the PHP client library uses GoogleSQL.

**Switch to the legacy SQL dialect**

To use legacy SQL syntax in a query job, set the `  useLegacySql  ` parameter to `  true  ` .

``` php
use Google\Cloud\BigQuery\BigQueryClient;

/**
 * Query using legacy sql
 *
 * @param string $projectId The project Id of your Google Cloud Project.
 */
function query_legacy(string $projectId): void
{
    $query = 'SELECT corpus FROM [bigquery-public-data:samples.shakespeare] GROUP BY corpus';

    $bigQuery = new BigQueryClient([
      'projectId' => $projectId,
    ]);
    $jobConfig = $bigQuery->query($query)->useLegacySql(true);

    $queryResults = $bigQuery->runQuery($jobConfig);

    $i = 0;
    foreach ($queryResults as $row) {
        printf('--- Row %s ---' . PHP_EOL, ++$i);
        foreach ($row as $column => $value) {
            printf('%s: %s' . PHP_EOL, $column, json_encode($value));
        }
    }
    printf('Found %s row(s)' . PHP_EOL, $i);
}
```

### Python

Before trying this sample, follow the Python setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Python API reference documentation](/python/docs/reference/bigquery/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

By default, the Python client library uses GoogleSQL.

**Switch to the legacy SQL dialect**

To use legacy SQL syntax in a query job, set the `  use_legacy_sql  ` parameter to `  True  ` .

``` python
from google.cloud import bigquery

# Construct a BigQuery client object.
client = bigquery.Client()

query = (
    "SELECT name FROM [bigquery-public-data:usa_names.usa_1910_2013] "
    'WHERE state = "TX" '
    "LIMIT 100"
)

# Set use_legacy_sql to True to use legacy SQL syntax.
job_config = bigquery.QueryJobConfig(use_legacy_sql=True)

# Start the query and waits for query job to complete, passing in the extra configuration.
results = client.query_and_wait(
    query, job_config=job_config
)  # Make an API request.

print("The query data:")
for row in results:
    print(row)
```

### Ruby

Before trying this sample, follow the Ruby setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Ruby API reference documentation](https://googleapis.dev/ruby/google-cloud-bigquery/latest/Google/Cloud/Bigquery.html) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

By default, the Ruby client library uses GoogleSQL.

**Switch to the legacy SQL dialect**

To use legacy SQL syntax in a query job, pass the option `  legacy_sql: true  ` with your query.

``` ruby
require "google/cloud/bigquery"

def query_legacy
  bigquery = Google::Cloud::Bigquery.new
  sql = "SELECT name FROM [bigquery-public-data:usa_names.usa_1910_2013] " \
        "WHERE state = 'TX' " \
        "LIMIT 100"

  results = bigquery.query sql, legacy_sql: true do |config|
    # Location must match that of the dataset(s) referenced in the query.
    config.location = "US"
  end

  results.each do |row|
    puts row.inspect
  end
end
```

## What's next

  - For information about how to run a SQL query in BigQuery, see [Running interactive and batch query jobs](/bigquery/docs/running-queries) .
  - For more information about query optimization in general, see [Introduction to optimizing query performance](/bigquery/docs/best-practices-performance-overview) .
  - To learn about the GoogleSQL syntax used for querying data in BigQuery, see [Query syntax](/bigquery/docs/reference/standard-sql/query-syntax) .
  - To learn more about how to use pipe syntax in your queries, see [pipe syntax](/bigquery/docs/pipe-syntax) .
