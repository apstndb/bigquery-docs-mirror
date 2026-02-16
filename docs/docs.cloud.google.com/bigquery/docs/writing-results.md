# Writing query results

This document describes how to write query results to temporary or permanent tables.

## Temporary and permanent tables

BigQuery saves all query results to a table, which can be either permanent or temporary.

  - BigQuery uses temporary tables to [cache query results](/bigquery/docs/cached-results) that aren't written to a permanent table. The tables are created in a special dataset and named randomly. You can also create temporary tables for your own use within [multi-statement queries](/bigquery/docs/multi-statement-queries#temporary_tables) and [sessions](/bigquery/docs/sessions-write-queries#use_temporary_tables_in_sessions) . You aren't charged for [temporary cached query result tables](/bigquery/docs/cached-results) . You are charged for temporary tables that aren't cached query results.

  - After a query finishes, the temporary table exists for up to 24 hours. To view table structure and data, do the following:
    
    1.  Go to the **BigQuery** page.
    
    2.  In the left pane, click explore **Explorer** :
        
        If you don't see the left pane, click last\_page **Expand left pane** to open the pane.
    
    3.  In the **Explorer** pane, click **Job history** .
    
    4.  Click **Personal history** .
    
    5.  Choose the query that created the temporary table. Then, in the **Destination table** row, click **Temporary table** .

  - Access to the temporary table data is restricted to the user or service account that created the query job.

  - You cannot share temporary tables, and they are not visible using any of the standard list or other table manipulation methods. If you need to share your query results, write the results to a permanent table, download them, or share them though Google Sheets or Google Drive.

  - Temporary tables are created in the same region as the table or tables being queried.

  - A permanent table can be a new or existing table in any dataset to which you have access. If you write query results to a new table, you are charged for [storing](https://cloud.google.com/bigquery/pricing#storage) the data. When you write query results to a permanent table, the tables you're querying must be in the same location as the dataset that contains the destination table.

  - You can't save query results in a temporary table when the [domain-restricted organization policy](/resource-manager/docs/organization-policy/restricting-domains) is enabled. As a workaround, temporarily disable the domain-restricted organization policy, run the query, and then again enable the policy. Alternatively, you can save query results in a destination table.

**Note:** If you query data from a project to data stored in a different project, the querying project is billed for the query job while the project storing the data is billed for the amount of data stored in BigQuery.

## Required permissions

At a minimum, to write query results to a table, you must be granted the following permissions:

  - `  bigquery.tables.create  ` permissions to create a new table
  - `  bigquery.tables.updateData  ` to write data to a new table, overwrite a table, or append data to a table
  - `  bigquery.jobs.create  ` to run a query job

Additional permissions such as `  bigquery.tables.getData  ` may be required to access the data you're querying.

The following predefined IAM roles include both `  bigquery.tables.create  ` and `  bigquery.tables.updateData  ` permissions:

  - `  bigquery.dataEditor  `
  - `  bigquery.dataOwner  `
  - `  bigquery.admin  `

The following predefined IAM roles include `  bigquery.jobs.create  ` permissions:

  - `  bigquery.user  `
  - `  bigquery.jobUser  `
  - `  bigquery.admin  `

In addition, if a user has `  bigquery.datasets.create  ` permissions, when that user creates a dataset, they are granted `  bigquery.dataOwner  ` access to it. `  bigquery.dataOwner  ` access gives the user the ability to create and update tables in the dataset.

For more information on IAM roles and permissions in BigQuery, see [Predefined roles and permissions](/bigquery/docs/access-control) .

## Write query results to a permanent table

When you write query results to a permanent table, you can create a new table, append the results to an existing table, or overwrite an existing table.

### Writing query results

Use the following procedure to write your query results to a permanent table. To help control costs, you can [preview data](/bigquery/docs/best-practices-costs#preview-data) before running the query.

### Console

1.  Open the BigQuery page in the Google Cloud console.

2.  In the left pane, click explore **Explorer** :
    
    If you don't see the left pane, click last\_page **Expand left pane** to open the pane.

3.  In the **Explorer** pane, expand your project, click **Datasets** , and then select a dataset.

4.  In the query editor, enter a valid SQL query.

5.  Click **More** and then select **Query settings** .

6.  Select the **Set a destination table for query results** option.

7.  In the **Destination** section, select the **Dataset** in which you want to create the table, and then choose a **Table Id** .

8.  In the **Destination table write preference** section, choose one of the following:
    
      - **Write if empty** — Writes the query results to the table only if the table is empty.
      - **Append to table** — Appends the query results to an existing table.
      - **Overwrite table** — Overwrites an existing table with the same name using the query results.

9.  Optional: For **Data location** , choose your [location](/bigquery/docs/locations) .

10. To update the query settings, click **Save** .

11. Click **Run** . This creates a query job that writes the query results to the table you specified.

Alternatively, if you forget to specify a destination table before running your query, you can copy the cached results table to a permanent table by clicking the [**Save Results**](#save-query-results) button above the editor.

### SQL

The following example uses the [`  CREATE TABLE  ` statement](/bigquery/docs/reference/standard-sql/data-definition-language#create_table_statement) to create the `  trips  ` table from data in the public `  bikeshare_trips  ` table:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
    CREATE TABLE mydataset.trips AS (
      SELECT
        bike_id,
        start_time,
        duration_minutes
      FROM
        bigquery-public-data.austin_bikeshare.bikeshare_trips
    );
    ```

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](/bigquery/docs/running-queries#queries) .

For more information, see [Creating a new table from an existing table](/bigquery/docs/reference/standard-sql/data-definition-language#creating_a_new_table_from_an_existing_table) .

### bq

1.  In the Google Cloud console, activate Cloud Shell.
    
    At the bottom of the Google Cloud console, a [Cloud Shell](/shell/docs/how-cloud-shell-works) session starts and displays a command-line prompt. Cloud Shell is a shell environment with the Google Cloud CLI already installed and with values already set for your current project. It can take a few seconds for the session to initialize.

2.  Enter the [`  bq query  `](/bigquery/docs/reference/bq-cli-reference#bq_query) command and specify the `  --destination_table  ` flag to create a permanent table based on the query results. Specify the `  use_legacy_sql=false  ` flag to use GoogleSQL syntax. To write the query results to a table that is not in your default project, add the project ID to the dataset name in the following format: `  project_id : dataset  ` .
    
    Optional: Supply the `  --location  ` flag and set the value to your [location](/bigquery/docs/dataset-locations) .
    
    To control the write disposition for an existing destination table, specify one of the following optional flags:
    
      - `  --append_table  ` : If the destination table exists, the query results are appended to it.
    
      - `  --replace  ` : If the destination table exists, it is overwritten with the query results.
        
        ``` text
        bq --location=location query \
        --destination_table project_id:dataset.table \
        --use_legacy_sql=false 'query'
        ```
        
        Replace the following:
    
      - `  location  ` is the name of the location used to process the query. The `  --location  ` flag is optional. For example, if you are using BigQuery in the Tokyo region, you can set the flag's value to `  asia-northeast1  ` . You can set a default value for the location by using the [`  .bigqueryrc  ` file](/bigquery/docs/bq-command-line-tool#setting_default_values_for_command-line_flags) .
    
      - `  project_id  ` is your project ID.
    
      - `  dataset  ` is the name of the dataset that contains the table to which you are writing the query results.
    
      - `  table  ` is the name of the table to which you're writing the query results.
    
      - `  query  ` is a query in GoogleSQL syntax.
        
        If no write disposition flag is specified, the default behavior is to write the results to the table only if it is empty. If the table exists and it is not empty, the following error is returned: `  BigQuery error in query operation: Error processing job project_id :bqjob_123abc456789_00000e1234f_1: Already Exists: Table project_id:dataset.table  ` .
        
        Examples:
        
        **Note:** These examples query a US-based public dataset. Because the public dataset is stored in the US multi-region location, the dataset that contains your destination table must also be in the US. You cannot query a dataset in one location and write the results to a destination table in another location.
        
        Enter the following command to write query results to a destination table named `  mytable  ` in `  mydataset  ` . The dataset is in your default project. Since no write disposition flag is specified in the command, the table must be new or empty. Otherwise, an `  Already exists  ` error is returned. The query retrieves data from the [USA Name Data public dataset](https://console.cloud.google.com/marketplace/product/social-security-administration/us-names) .
        
        ``` text
        bq query \
        --destination_table mydataset.mytable \
        --use_legacy_sql=false \
        'SELECT
        name,
        number
        FROM
        `bigquery-public-data`.usa_names.usa_1910_current
        WHERE
        gender = "M"
        ORDER BY
        number DESC'
        ```
        
        Enter the following command to use query results to overwrite a destination table named `  mytable  ` in `  mydataset  ` . The dataset is in your default project. The command uses the `  --replace  ` flag to overwrite the destination table.
        
        ``` text
        bq query \
        --destination_table mydataset.mytable \
        --replace \
        --use_legacy_sql=false \
        'SELECT
        name,
        number
        FROM
        `bigquery-public-data`.usa_names.usa_1910_current
        WHERE
        gender = "M"
        ORDER BY
        number DESC'
        ```
        
        Enter the following command to append query results to a destination table named `  mytable  ` in `  mydataset  ` . The dataset is in `  my-other-project  ` , not your default project. The command uses the `  --append_table  ` flag to append the query results to the destination table.
        
        ``` text
        bq query \
        --append_table \
        --use_legacy_sql=false \
        --destination_table my-other-project:mydataset.mytable \
        'SELECT
        name,
        number
        FROM
        `bigquery-public-data`.usa_names.usa_1910_current
        WHERE
        gender = "M"
        ORDER BY
        number DESC'
        ```
        
        The output for each of these examples looks like the following. For readability, some output is truncated.
        
        ``` text
        Waiting on bqjob_r123abc456_000001234567_1 ... (2s) Current status: DONE
        +---------+--------+
        |  name   | number |
        +---------+--------+
        | Robert  |  10021 |
        | John    |   9636 |
        | Robert  |   9297 |
        | ...              |
        +---------+--------+
        ```

### API

To save query results to a permanent table, call the [`  jobs.insert  `](/bigquery/docs/reference/rest/v2/jobs/insert) method, configure a `  query  ` job, and include a value for the `  destinationTable  ` property. To control the write disposition for an existing destination table, configure the `  writeDisposition  ` property.

To control the processing location for the query job, specify the `  location  ` property in the `  jobReference  ` section of the [job resource](/bigquery/docs/reference/rest/v2/jobs) .

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

// queryWithDestination demonstrates saving the results of a query to a specific table by setting the destination
// via the API properties.
func queryWithDestination(w io.Writer, projectID, destDatasetID, destTableID string) error {
 // projectID := "my-project-id"
 // datasetID := "mydataset"
 // tableID := "mytable"
 ctx := context.Background()
 client, err := bigquery.NewClient(ctx, projectID)
 if err != nil {
     return fmt.Errorf("bigquery.NewClient: %v", err)
 }
 defer client.Close()

 q := client.Query("SELECT 17 as my_col")
 q.Location = "US" // Location must match the dataset(s) referenced in query.
 q.QueryConfig.Dst = client.Dataset(destDatasetID).Table(destTableID)
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

To save query results to a permanent table, set the [destination table](https://cloud.google.com/java/docs/reference/google-cloud-bigquery/latest/com.google.cloud.bigquery.QueryJobConfiguration.Builder#com_google_cloud_bigquery_QueryJobConfiguration_Builder_setDestinationTable_com_google_cloud_bigquery_TableId_) to the desired [TableId](https://cloud.google.com/java/docs/reference/google-cloud-bigquery/latest/com.google.cloud.bigquery.TableId) in a [QueryJobConfiguration](https://cloud.google.com/java/docs/reference/google-cloud-bigquery/latest/com.google.cloud.bigquery.QueryJobConfiguration) .

``` java
import com.google.cloud.bigquery.BigQuery;
import com.google.cloud.bigquery.BigQueryException;
import com.google.cloud.bigquery.BigQueryOptions;
import com.google.cloud.bigquery.QueryJobConfiguration;
import com.google.cloud.bigquery.TableId;

public class SaveQueryToTable {

  public static void runSaveQueryToTable() {
    // TODO(developer): Replace these variables before running the sample.
    String query = "SELECT corpus FROM `bigquery-public-data.samples.shakespeare` GROUP BY corpus;";
    String destinationTable = "MY_TABLE";
    String destinationDataset = "MY_DATASET";

    saveQueryToTable(destinationDataset, destinationTable, query);
  }

  public static void saveQueryToTable(
      String destinationDataset, String destinationTableId, String query) {
    try {
      // Initialize client that will be used to send requests. This client only needs to be created
      // once, and can be reused for multiple requests.
      BigQuery bigquery = BigQueryOptions.getDefaultInstance().getService();

      // Identify the destination table
      TableId destinationTable = TableId.of(destinationDataset, destinationTableId);

      // Build the query job
      QueryJobConfiguration queryConfig =
          QueryJobConfiguration.newBuilder(query).setDestinationTable(destinationTable).build();

      // Execute the query.
      bigquery.query(queryConfig);

      // The results are now saved in the destination table.

      System.out.println("Saved query ran successfully");
    } catch (BigQueryException | InterruptedException e) {
      System.out.println("Saved query did not run \n" + e.toString());
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

async function queryDestinationTable() {
  // Queries the U.S. given names dataset for the state of Texas
  // and saves results to permanent table.

  /**
   * TODO(developer): Uncomment the following lines before running the sample.
   */
  // const datasetId = 'my_dataset';
  // const tableId = 'my_table';

  // Create destination table reference
  const dataset = bigquery.dataset(datasetId);
  const destinationTable = dataset.table(tableId);

  const query = `SELECT name
    FROM \`bigquery-public-data.usa_names.usa_1910_2013\`
    WHERE state = 'TX'
    LIMIT 100`;

  // For all options, see https://cloud.google.com/bigquery/docs/reference/v2/tables#resource
  const options = {
    query: query,
    // Location must match that of the dataset(s) referenced in the query.
    location: 'US',
    destination: destinationTable,
  };

  // Run the query as a job
  const [job] = await bigquery.createQueryJob(options);

  console.log(`Job ${job.id} started.`);
  console.log(`Query results loaded to table ${destinationTable.id}`);
}
```

### Python

Before trying this sample, follow the Python setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Python API reference documentation](/python/docs/reference/bigquery/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

To save query results to a permanent table, create a [QueryJobConfig](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJob#google_cloud_bigquery_job_QueryJob) and set the [destination](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJob#google_cloud_bigquery_job_QueryJob_destination) to the desired [TableReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableReference) . Pass the job configuration to the [query method](/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client#google_cloud_bigquery_client_Client_query) .

``` python
from google.cloud import bigquery

# Construct a BigQuery client object.
client = bigquery.Client()

# TODO(developer): Set table_id to the ID of the destination table.
# table_id = "your-project.your_dataset.your_table_name"

job_config = bigquery.QueryJobConfig(destination=table_id)

sql = """
    SELECT corpus
    FROM `bigquery-public-data.samples.shakespeare`
    GROUP BY corpus;
"""

# Start the query, passing in the extra configuration.
query_job = client.query(sql, job_config=job_config)  # Make an API request.
query_job.result()  # Wait for the job to complete.

print("Query results loaded to the table {}".format(table_id))
```

## Write large query results

Normally, queries have a [maximum response size](/bigquery/quotas#query_jobs) . If you plan to run a query that might return larger results, you can do one of the following:

  - In GoogleSQL, specify a destination table for the query results.
  - In legacy SQL, specify a destination table and set the `  allowLargeResults  ` option.

When you specify a destination table for large query results, you are charged for [storing](https://cloud.google.com/bigquery/pricing#storage) the data.

### Limitations

In legacy SQL, writing large results is subject to these limitations:

  - You must specify a destination table.
  - You cannot specify a top-level `  ORDER BY  ` , `  TOP  ` or `  LIMIT  ` clause. Doing so negates the benefit of using `  allowLargeResults  ` , because the query output can no longer be computed in parallel.
  - [Window functions](/bigquery/query-reference#windowfunctions) can return large query results only if used in conjunction with a `  PARTITION BY  ` clause.

### Writing large results using legacy SQL

To write large result sets using legacy SQL:

### Console

1.  In the Google Cloud console, open the BigQuery page.

2.  Click **Compose new query** .

3.  Enter a valid SQL query in the **Query editor** text area. Use the `  #legacySQL  ` prefix or be sure you have **Use Legacy SQL** checked in the query settings.

4.  Click **More** then select **Query settings** .

5.  For **Destination** , check **Set a destination table for query results** .

6.  For **Dataset** , choose the dataset that will store the table.

7.  In the **Table Id** field, enter a table name.

8.  If you are writing a large results set to an existing table, you can use the **Destination table write preference** options to control the write disposition of the destination table:
    
      - **Write if empty:** Writes the query results to the table only if the table is empty.
      - **Append to table:** Appends the query results to an existing table.
      - **Overwrite table:** Overwrites an existing table with the same name using the query results.

9.  For **Results Size** , check **Allow large results (no size limit)** .

10. Optional: For **Data location** , choose the [location](/bigquery/docs/locations) of your data.

11. Click **Save** to update the query settings.

12. Click **Run** . This creates a query job that writes the large results set to the table you specified.

### bq

Use the `  --allow_large_results  ` flag with the `  --destination_table  ` flag to create a destination table to hold the large results set. Because the `  --allow_large_results  ` option only applies to legacy SQL, you must also specify the `  --use_legacy_sql=true  ` flag. To write the query results to a table that is not in your default project, add the project ID to the dataset name in the following format: `  PROJECT_ID : DATASET  ` . Supply the `  --location  ` flag and set the value to your [location](/bigquery/docs/locations) .

To control the write disposition for an existing destination table, specify one of the following optional flags:

  - `  --append_table  ` : If the destination table exists, the query results are appended to it.
  - `  --replace  ` : If the destination table exists, it is overwritten with the query results.

<!-- end list -->

``` text
bq --location=location query \
--destination_table PROJECT_ID:DATASET.TABLE \
--use_legacy_sql=true \
--allow_large_results "QUERY"
```

Replace the following:

  - `  LOCATION  ` is the name of the location used to process the query. The `  --location  ` flag is optional. For example, if you are using BigQuery in the Tokyo region, you can set the flag's value to `  asia-northeast1  ` . You can set a default value for the location using the [`  .bigqueryrc  ` file](/bigquery/docs/bq-command-line-tool#setting_default_values_for_command-line_flags) .
  - `  PROJECT_ID  ` is your project ID.
  - `  DATASET  ` is the name of the dataset that contains the table to which you are writing the query results.
  - `  TABLE  ` is the name of the table to which you're writing the query results.
  - `  QUERY  ` is a query in legacy SQL syntax.

Examples:

**Note:** These examples query a public dataset. Because the dataset is stored in the `  US  ` multi-region location, your destination dataset must also be in the US. You cannot write public data query results to a table in another region.

Enter the following command to write large query results to a destination table named `  mytable  ` in `  mydataset  ` . The dataset is in your default project. Since no write disposition flag is specified in the command, the table must be new or empty. Otherwise, an `  Already exists  ` error is returned. The query retrieves data from the [USA Name Data public dataset](https://console.cloud.google.com/bigquery?p=bigquery-public-data&d=usa_names&page=dataset) . This query is used for example purposes only. The results set returned does not exceed the maximum response size.

``` text
bq query \
--destination_table mydataset.mytable \
--use_legacy_sql=true \
--allow_large_results \
"SELECT
  name,
  number
FROM
  [bigquery-public-data:usa_names.usa_1910_current]
WHERE
  gender = 'M'
ORDER BY
  number DESC"
```

Enter the following command to use large query results to overwrite a destination table named `  mytable  ` in `  mydataset  ` . The dataset is in `  myotherproject  ` , not your default project. The command uses the `  --replace  ` flag to overwrite the destination table.

``` text
bq query \
--destination_table mydataset.mytable \
--replace \
--use_legacy_sql=true \
--allow_large_results \
"SELECT
  name,
  number
FROM
  [bigquery-public-data:usa_names.usa_1910_current]
WHERE
  gender = 'M'
ORDER BY
  number DESC"
```

Enter the following command to append large query results to a destination table named `  mytable  ` in `  mydataset  ` . The dataset is in `  myotherproject  ` , not your default project. The command uses the `  --append_table  ` flag to append the query results to the destination table.

``` text
bq query \
--destination_table myotherproject:mydataset.mytable \
--append_table \
--use_legacy_sql=true \
--allow_large_results \
"SELECT
  name,
  number
FROM
  [bigquery-public-data:usa_names.usa_1910_current]
WHERE
  gender = 'M'
ORDER BY
  number DESC"
```

### API

To write large results to a destination table, call the [`  jobs.insert  `](/bigquery/docs/reference/rest/v2/jobs/insert) method, configure a `  query  ` job, and set the `  allowLargeResults  ` property to `  true  ` . Specify the destination table using the `  destinationTable  ` property. To control the write disposition for an existing destination table, configure the `  writeDisposition  ` property.

Specify your location in the `  location  ` property in the `  jobReference  ` section of the [job resource](/bigquery/docs/reference/rest/v2/jobs) .

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

// queryLegacyLargeResults demonstrates issuing a legacy SQL query and writing a large result set
// into a destination table.
func queryLegacyLargeResults(w io.Writer, projectID, datasetID, tableID string) error {
 // projectID := "my-project-id"
 // datasetID := "destinationdataset"
 // tableID := "destinationtable"
 ctx := context.Background()
 client, err := bigquery.NewClient(ctx, projectID)
 if err != nil {
     return fmt.Errorf("bigquery.NewClient: %v", err)
 }
 defer client.Close()

 q := client.Query(
     "SELECT corpus FROM [bigquery-public-data:samples.shakespeare] GROUP BY corpus;")
 q.UseLegacySQL = true
 q.AllowLargeResults = true
 q.QueryConfig.Dst = client.Dataset(datasetID).Table(tableID)
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

To enable large results, set [allow large results](/java/docs/reference/google-cloud-bigquery/latest/com.google.cloud.bigquery.QueryJobConfiguration.Builder#com_google_cloud_bigquery_QueryJobConfiguration_Builder_setAllowLargeResults_java_lang_Boolean_) to `  true  ` and set the [destination table](/java/docs/reference/google-cloud-bigquery/latest/com.google.cloud.bigquery.TableId) to the desired [TableId](/java/docs/reference/google-cloud-bigquery/latest/com.google.cloud.bigquery.TableId) in a [QueryJobConfiguration](/java/docs/reference/google-cloud-bigquery/latest/com.google.cloud.bigquery.QueryJobConfiguration) .

Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Java API reference documentation](/java/docs/reference/google-cloud-bigquery/latest/overview) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` java
import com.google.cloud.bigquery.BigQuery;
import com.google.cloud.bigquery.BigQueryException;
import com.google.cloud.bigquery.BigQueryOptions;
import com.google.cloud.bigquery.QueryJobConfiguration;
import com.google.cloud.bigquery.TableId;
import com.google.cloud.bigquery.TableResult;

// Sample to run query with large results and save the results to a table.
public class QueryLargeResults {

  public static void runQueryLargeResults() {
    // TODO(developer): Replace these variables before running the sample.
    String destinationDataset = "MY_DESTINATION_DATASET_NAME";
    String destinationTable = "MY_DESTINATION_TABLE_NAME";
    String query = "SELECT corpus FROM [bigquery-public-data:samples.shakespeare] GROUP BY corpus;";
    queryLargeResults(destinationDataset, destinationTable, query);
  }

  public static void queryLargeResults(
      String destinationDataset, String destinationTable, String query) {
    try {
      // Initialize client that will be used to send requests. This client only needs to be created
      // once, and can be reused for multiple requests.
      BigQuery bigquery = BigQueryOptions.getDefaultInstance().getService();

      QueryJobConfiguration queryConfig =
          // To use legacy SQL syntax, set useLegacySql to true.
          QueryJobConfiguration.newBuilder(query)
              .setUseLegacySql(true)
              // Save the results of the query to a permanent table.
              .setDestinationTable(TableId.of(destinationDataset, destinationTable))
              // Allow results larger than the maximum response size.
              // If true, a destination table must be set.
              .setAllowLargeResults(true)
              .build();

      TableResult results = bigquery.query(queryConfig);

      results
          .iterateAll()
          .forEach(row -> row.forEach(val -> System.out.printf("%s,", val.toString())));

      System.out.println("Query large results performed successfully.");
    } catch (BigQueryException | InterruptedException e) {
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

async function queryLegacyLargeResults() {
  // Query enables large result sets.

  /**
   * TODO(developer): Uncomment the following lines before running the sample
   */
  // const projectId = "my_project"
  // const datasetId = "my_dataset";
  // const tableId = "my_table";

  const query = `SELECT word FROM [bigquery-public-data:samples.shakespeare] LIMIT 10;`;

  // For all options, see https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query
  const options = {
    query: query,
    // Location must match that of the dataset(s) referenced
    // in the query and of the destination table.
    useLegacySql: true,
    allowLargeResult: true,
    destinationTable: {
      projectId: projectId,
      datasetId: datasetId,
      tableId: tableId,
    },
  };

  const [job] = await bigquery.createQueryJob(options);
  console.log(`Job ${job.id} started.`);

  // Wait for the query to finish
  const [rows] = await job.getQueryResults();

  // Print the results
  console.log('Rows:');
  rows.forEach(row => console.log(row));
}
```

### Python

Before trying this sample, follow the Python setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Python API reference documentation](/python/docs/reference/bigquery/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` python
from google.cloud import bigquery

# Construct a BigQuery client object.
client = bigquery.Client()

# TODO(developer): Set table_id to the ID of the destination table.
# table_id = "your-project.your_dataset.your_table_name"

# Set the destination table and use_legacy_sql to True to use
# legacy SQL syntax.
job_config = bigquery.QueryJobConfig(
    allow_large_results=True, destination=table_id, use_legacy_sql=True
)

sql = """
    SELECT corpus
    FROM [bigquery-public-data:samples.shakespeare]
    GROUP BY corpus;
"""

# Start the query, passing in the extra configuration.
query_job = client.query(sql, job_config=job_config)  # Make an API request.
query_job.result()  # Wait for the job to complete.

print("Query results loaded to the table {}".format(table_id))
```

## Downloading and saving query results from the Google Cloud console

After you run a SQL query by using the Google Cloud console, you can save the results to another location. You can use the Google Cloud console to download query results to a local file, Google Sheets, or Google Drive. If you first sort the query results by column, then the order is preserved in the downloaded data. Saving results to a local file, Google Sheets, or Google Drive is not supported by the bq command-line tool or the API.

### Limitations

Downloading and saving query results are subject to the following limitations:

  - You can download query results locally only in CSV or newline-delimited JSON format.
  - You cannot save query results containing nested and repeated data to Google Sheets.
  - To save query results to Google Drive using the Google Cloud console, the results set must be 1 GB or less. If your results are larger, you can save them to a table instead.
  - When saving query results to a local CSV file, the maximum download size is 10 MB. The maximum download size is based on the size of each row returned in the [`  tabledata.list  `](/bigquery/docs/reference/rest/v2/tabledata/list) method response, and can vary based on the schema of the query results. As a result, the size of the downloaded CSV file can vary, and might be less than the maximum download size limit.
  - You can save query results to Google Drive only in CSV or newline-delimited JSON format.

## What's next

  - Learn how to programmatically [export a table to a JSON file](/bigquery/docs/samples/bigquery-extract-table-json) .
  - Learn about [quotas for query jobs](/bigquery/quotas#query_jobs) .
  - Learn about [BigQuery storage pricing](https://cloud.google.com/bigquery/pricing#storage) .
