# Manage materialized views

This document describes how to manage materialized views in BigQuery.

BigQuery management of materialized views includes the following operations:

  - [Alter materialized views](#alter)
  - [List materialized views](#list)
  - [Get information about materialized views](#get-info)
  - [Delete materialized views](#delete)
  - [Refresh materialized views](#refresh)

For more information about materialized views, see the following:

  - [Introduction to materialized views](/bigquery/docs/materialized-views-intro)
  - [Create materialized views](/bigquery/docs/materialized-views-create)
  - [Use materialized views](/bigquery/docs/materialized-views-use)
  - [Monitor materialized views](/bigquery/docs/materialized-views-monitor)

## Before you begin

Grant Identity and Access Management (IAM) roles that give users the necessary permissions to perform each task in this document. The permissions required to perform a task (if any) are listed in the "Required permissions" section of the task.

## Alter materialized views

You can alter a materialized view through the Google Cloud console or the bq command-line tool, by using data definition language (DDL) with `  ALTER MATERIALIZED VIEW  ` and `  SET OPTIONS  ` . For a list of materialized view options, see [`  materialized_view_set_options_list  `](/bigquery/docs/reference/standard-sql/data-definition-language#materialized_view_set_options_list) .

The following shows an example that sets `  enable_refresh  ` to `  true  ` . Adjust as needed for your use case.

### Required permissions

To alter materialized views, you need the `  bigquery.tables.get  ` and `  bigquery.tables.update  ` IAM permissions.

Each of the following predefined IAM roles includes the permissions that you need in order to alter a materialized view:

  - `  bigquery.dataEditor  `
  - `  bigquery.dataOwner  `
  - `  bigquery.admin  `

For more information about BigQuery Identity and Access Management (IAM), see [Predefined roles and permissions](/bigquery/docs/access-control) .

### SQL

To alter a materialized view, use the [`  ALTER MATERIALIZED VIEW SET OPTIONS  ` DDL statement](/bigquery/docs/reference/standard-sql/data-definition-language#alter_materialized_view_set_options_statement) :

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
    ALTER MATERIALIZED VIEW PROJECT.DATASET.MATERIALIZED_VIEW
    SET OPTIONS (enable_refresh = true);
    ```
    
    Replace the following:
    
      - `  PROJECT  ` : the name of the project that contains the materialized view
      - `  DATASET  ` : the name of the dataset that contains the materialized view
      - `  MATERIALIZED_VIEW  ` : the name of the materialized view you want to alter

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](/bigquery/docs/running-queries#queries) .

### bq

Run the `  bq update  ` command:

``` text
bq update \
--enable_refresh=true \
--refresh_interval_ms= \
PROJECT.DATASET.MATERIALIZED_VIEW
```

### Java

Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Java API reference documentation](/java/docs/reference/google-cloud-bigquery/latest/overview) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` java
import com.google.cloud.bigquery.BigQuery;
import com.google.cloud.bigquery.BigQueryException;
import com.google.cloud.bigquery.BigQueryOptions;
import com.google.cloud.bigquery.MaterializedViewDefinition;
import com.google.cloud.bigquery.Table;
import com.google.cloud.bigquery.TableId;

// Sample to update materialized view
public class UpdateMaterializedView {

  public static void main(String[] args) {
    // TODO(developer): Replace these variables before running the sample.
    String datasetName = "MY_DATASET_NAME";
    String materializedViewName = "MY_MATERIALIZED_VIEW_NAME";
    updateMaterializedView(datasetName, materializedViewName);
  }

  public static void updateMaterializedView(String datasetName, String materializedViewName) {
    try {
      // Initialize client that will be used to send requests. This client only needs to be created
      // once, and can be reused for multiple requests.
      BigQuery bigquery = BigQueryOptions.getDefaultInstance().getService();

      TableId tableId = TableId.of(datasetName, materializedViewName);

      // Get existing materialized view
      Table table = bigquery.getTable(tableId);
      MaterializedViewDefinition materializedViewDefinition = table.getDefinition();
      // Update materialized view
      materializedViewDefinition
          .toBuilder()
          .setEnableRefresh(true)
          .setRefreshIntervalMs(1000L)
          .build();
      table.toBuilder().setDefinition(materializedViewDefinition).build().update();
      System.out.println("Materialized view updated successfully");
    } catch (BigQueryException e) {
      System.out.println("Materialized view was not updated. \n" + e.toString());
    }
  }
}
```

## List materialized views

You can list materialized views through the Google Cloud console, the bq command-line tool, or the BigQuery API.

### Required permissions

To list materialized views in a dataset, you need the `  bigquery.tables.list  ` IAM permission.

Each of the following predefined IAM roles includes the permissions that you need in order to list materialized views in a dataset:

  - `  roles/bigquery.user  `
  - `  roles/bigquery.metadataViewer  `
  - `  roles/bigquery.dataViewer  `
  - `  roles/bigquery.dataOwner  `
  - `  roles/bigquery.dataEditor  `
  - `  roles/bigquery.admin  `

For more information on IAM roles and permissions in IAM, see [Predefined roles and permissions](/bigquery/docs/access-control) .

The process to list materialized views is identical to the process for listing tables. To list the materialized views in a dataset:

### Console

1.  In the left pane, click explore **Explorer** :
    
    If you don't see the left pane, click last\_page **Expand left pane** to open the pane.

2.  In the **Explorer** pane, expand your project, click **Datasets** , and then click the dataset.

3.  Click **Overview \> Tables** . Scroll through the list to see the tables in the dataset. Tables, views, and materialized views are identified by different values in the **Type** column. Materialized view replicas have the same value as materialized views.

### bq

Issue the `  bq ls  ` command. The `  --format  ` flag can be used to control the output. If you are listing materialized views in a project other than your default project, add the project ID to the dataset in the following format: `  project_id:dataset  ` .

``` text
bq ls --format=pretty project_id:dataset
```

Where:

  - project\_id is your project ID.
  - dataset is the name of the dataset.

When you run the command, the `  Type  ` field displays the table type. For example:

``` text
+-------------------------+--------------------+----------------------+-------------------+
|         tableId         | Type               |        Labels        | Time Partitioning |
+-------------------------+--------------------+----------------------+-------------------+
| mytable                 | TABLE              | department:shipping  |                   |
| mymatview               | MATERIALIZED_VIEW  |                      |                   |
+-------------------------+--------------------+----------------------+-------------------+
```

Examples:

Enter the following command to list materialized views in dataset `  mydataset  ` in your default project.

``` text
bq ls --format=pretty mydataset
```

Enter the following command to list materialized views in dataset `  mydataset  ` in `  myotherproject  ` .

``` text
bq ls --format=pretty myotherproject:mydataset
```

### API

To list materialized views using the API, call the [`  tables.list  `](/bigquery/docs/reference/rest/v2/tables/list) method.

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

// listTables demonstrates iterating through the collection of tables in a given dataset.
func listTables(w io.Writer, projectID, datasetID string) error {
 // projectID := "my-project-id"
 // datasetID := "mydataset"
 // tableID := "mytable"
 ctx := context.Background()
 client, err := bigquery.NewClient(ctx, projectID)
 if err != nil {
     return fmt.Errorf("bigquery.NewClient: %v", err)
 }
 defer client.Close()

 ts := client.Dataset(datasetID).Tables(ctx)
 for {
     t, err := ts.Next()
     if err == iterator.Done {
         break
     }
     if err != nil {
         return err
     }
     fmt.Fprintf(w, "Table: %q\n", t.TableID)
 }
 return nil
}
```

### Python

Before trying this sample, follow the Python setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Python API reference documentation](/python/docs/reference/bigquery/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` python
from google.cloud import bigquery

# Construct a BigQuery client object.
client = bigquery.Client()

# TODO(developer): Set dataset_id to the ID of the dataset that contains
#                  the tables you are listing.
# dataset_id = 'your-project.your_dataset'

tables = client.list_tables(dataset_id)  # Make an API request.

print("Tables contained in '{}':".format(dataset_id))
for table in tables:
    print("{}.{}.{}".format(table.project, table.dataset_id, table.table_id))
```

## Get information about materialized views

You can get information about a materialized view by using SQL, the bq command-line tool, or the BigQuery API.

### Required permissions

To query information about a materialized view, you need the following Identity and Access Management (IAM) permissions:

  - `  bigquery.tables.get  `
  - `  bigquery.tables.list  `
  - `  bigquery.routines.get  `
  - `  bigquery.routines.list  `

Each of the following predefined IAM roles includes the preceding permissions:

  - `  roles/bigquery.metadataViewer  `
  - `  roles/bigquery.dataViewer  `
  - `  roles/bigquery.admin  `

For more information about BigQuery permissions, see [Access control with IAM](/bigquery/docs/access-control) .

To get information about a materialized view, including any dependant [materialized view replicas](/bigquery/docs/load-data-using-cross-cloud-transfer#materialized_view_replicas) :

### SQL

To get information about materialized views, query the [`  INFORMATION_SCHEMA.TABLES  ` view](/bigquery/docs/information-schema-tables) :

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
    SELECT * FROM PROJECT_ID.DATASET_ID.INFORMATION_SCHEMA.TABLES
    WHERE table_type = 'MATERIALIZED VIEW';
    ```
    
    Replace the following:
    
      - `  PROJECT_ID  ` : the name of the project that contains the materialized views
      - `  DATASET_ID  ` : the name of the dataset that contains the materialized views

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](/bigquery/docs/running-queries#queries) .

### bq

Use the [`  bq show  ` command](/bigquery/docs/reference/bq-cli-reference#bq_show) :

``` text
bq show --project=project_id --format=prettyjson dataset.materialized_view
```

Replace the following:

  - project\_id : the project ID. You only need to include this flag to get information about a materialized view in a different project than the default project.
  - dataset : the name of the dataset that contains the materialized view.
  - materialized\_view : the name of the materialized view that you want information about.

Example:

Enter the following command to show information about the materialized view `  my_mv  ` in the `  report_views  ` dataset in the `  myproject  ` project.

``` text
bq show --project=myproject --format=prettyjson report_views.my_mv
```

### API

To get materialized view information by using the API, call the [`  tables.get  `](/bigquery/docs/reference/rest/v2/tables/get) method.

## Delete materialized views

You can delete a materialized view through the Google Cloud console, the bq command-line tool, or the API.

**Caution:** Deleting a materialized view cannot be undone.

Deleting a materialized view also deletes any permissions associated with this materialized view. When you recreate a deleted materialized view, you must also manually [reconfigure any access permissions](/bigquery/docs/control-access-to-resources-iam) previously associated with it.

### Required permissions

To delete materialized views, you need the `  bigquery.tables.delete  ` IAM permission.

Each of the following predefined IAM roles includes the permissions that you need in order to delete a materialized view:

  - `  bigquery.dataEditor  `
  - `  bigquery.dataOwner  `
  - `  bigquery.admin  `

For more information about BigQuery Identity and Access Management (IAM), see [Predefined roles and permissions](/bigquery/docs/access-control) .

### SQL

To delete a materialized view, use the [`  DROP MATERIALIZED VIEW  ` DDL statement](/bigquery/docs/reference/standard-sql/data-definition-language#drop_materialized_view_statement) :

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
    DROP MATERIALIZED VIEW PROJECT.DATASET.MATERIALIZED_VIEW;
    ```
    
    Replace the following:
    
      - `  PROJECT  ` : the name of the project that contains the materialized view
      - `  DATASET  ` : the name of the dataset that contains the materialized view
      - `  MATERIALIZED_VIEW  ` : the name of the materialized view you want to delete

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](/bigquery/docs/running-queries#queries) .

### bq

Use the [`  bq rm  ` command](/bigquery/docs/reference/bq-cli-reference#bq_rm) to delete the materialized view.

### API

Call the [`  tables.delete  `](/bigquery/docs/reference/rest/v2/tables/delete) method and specify values for the `  projectId  ` , `  datasetId  ` , and `  tableId  ` [parameters](/bigquery/docs/reference/rest/v2/tables/delete#path-parameters) :

  - Assign the `  projectId  ` parameter to your project ID.
  - Assign the `  datasetId  ` parameter to your dataset ID.
  - Assign the `  tableId  ` parameter to the table ID of the materialized view that you're deleting.

### Java

Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Java API reference documentation](/java/docs/reference/google-cloud-bigquery/latest/overview) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` java
import com.google.cloud.bigquery.BigQuery;
import com.google.cloud.bigquery.BigQueryException;
import com.google.cloud.bigquery.BigQueryOptions;
import com.google.cloud.bigquery.TableId;

// Sample to delete materialized view
public class DeleteMaterializedView {

  public static void main(String[] args) {
    // TODO(developer): Replace these variables before running the sample.
    String datasetName = "MY_DATASET_NAME";
    String materializedViewName = "MY_MATERIALIZED_VIEW_NAME";
    deleteMaterializedView(datasetName, materializedViewName);
  }

  public static void deleteMaterializedView(String datasetName, String materializedViewName) {
    try {
      // Initialize client that will be used to send requests. This client only needs to be created
      // once, and can be reused for multiple requests.
      BigQuery bigquery = BigQueryOptions.getDefaultInstance().getService();

      TableId tableId = TableId.of(datasetName, materializedViewName);

      boolean success = bigquery.delete(tableId);
      if (success) {
        System.out.println("Materialized view deleted successfully");
      } else {
        System.out.println("Materialized view was not found");
      }
    } catch (BigQueryException e) {
      System.out.println("Materialized view was not found. \n" + e.toString());
    }
  }
}
```

**Caution:** If you delete a materialized view's base table without first deleting the materialized view, then any refresh or query of the materialized view will fail. If you decide to recreate the base table, then you must also recreate the materialized view.

## Refresh materialized views

Refreshing a materialized view updates the view's cached data to reflect the current state of its base tables.

When you query a materialized view, BigQuery returns results from both cached materialized view data and data retrieved from the base table. Where possible, BigQuery reads only the changes since the last time the view was refreshed. While recently streamed data might not be included during a refresh of the materialized view, queries always read streamed data regardless of whether a materialized view is used.

Returning query results directly from the base table incurs higher compute cost than returning results from cached materialized view data. Regularly refreshing materialized view cached data reduces the amount of data returned directly from the base table, which reduces the compute cost.

This section describes how to do the following:

  - [Configure automatic refresh](#automatic-refresh)
  - [Manually refresh a materialized view](#manual-refresh)

**Note:** If you delete a base table without first deleting the materialized view, refreshes of the materialized view will fail. To recreate a base table, you must also recreate the materialized view.

### Automatic refresh

You can enable or disable automatic refresh at any time. The automatic refresh job is performed by the `  bigquery-adminbot@system.gserviceaccount.com  ` service account and appears in the materialized view project's job history.

By default, cached data in a materialized view is automatically refreshed from the base table within 5 to 30 minutes of a change to the base table, for example, row insertions or row deletions.

You can set the [refresh frequency cap](#frequency_cap) to manage the frequency of automatic refreshes of cached data, and thus manage the costs and query performance of materialized views.

#### Enable and disable automatic refresh

To turn automatic refresh off when you create a materialized view, set `  enable_refresh  ` to `  false  ` .

``` text
CREATE MATERIALIZED VIEW PROJECT.DATASET.MATERIALIZED_VIEW
PARTITION BY RANGE_BUCKET(column_name, buckets)
OPTIONS (enable_refresh = false)
AS SELECT ...
```

For an existing materialized view, you can modify the `  enable_refresh  ` value using `  ALTER MATERIALIZED VIEW  ` .

``` text
ALTER MATERIALIZED VIEW PROJECT.DATASET.MATERIALIZED_VIEW
SET OPTIONS (enable_refresh = true);
```

**Note:** Enabling automatic refresh immediately triggers an automatic refresh of the materialized view.

#### Set the frequency cap

You can configure a frequency cap on how often automatic refresh is run. By default, materialized views are refreshed no more often than every 30 minutes.

The refresh frequency cap can be changed at any time.

To set a refresh frequency cap when you create a materialized view, set `  refresh_interval_minutes  ` in DDL (or `  refresh_interval_ms  ` in the API and bq command-line tool), to the value you want.

``` text
CREATE MATERIALIZED VIEW PROJECT.DATASET.MATERIALIZED_VIEW
OPTIONS (enable_refresh = true, refresh_interval_minutes = 60)
AS SELECT ...
```

Similarly, you can set the frequency cap when you modify a materialized view. This example assumes you have already enabled automatic refresh, and just want to change the frequency cap:

``` text
ALTER MATERIALIZED VIEW PROJECT.DATASET.MATERIALIZED_VIEW
SET OPTIONS (refresh_interval_minutes = 60);
```

The minimum refresh frequency cap is 1 minute. The maximum refresh frequency cap is 7 days.

You can perform a manual refresh of a materialized view at any time, and its timing is not subject to the frequency cap.

#### Best-effort

Automatic refresh is performed on a best-effort basis. BigQuery attempts to start a refresh within 5 minutes of a change in the base table (if the previous refresh was done earlier than 30 minutes ago), but it doesn't guarantee that the refresh will be started at that time, nor does it guarantee when it will complete.

**Note:** Querying materialized views reflects the latest state of the base tables, but if the view wasn't refreshed recently, the query cost or latency can be higher than expected.

Automatic refresh is treated similarly to a query with [batch](/bigquery/docs/running-queries#batch) priority. If the materialized view's project does not have the capacity at the moment, the refresh is delayed. If the project contains many views whose refresh turns out to be expensive, each individual view might lag significantly relative to its base tables.

### Manual refresh

You can manually refresh a materialized view at any time.

#### Required permissions

To manually refresh materialized views, you need the `  bigquery.tables.getData  ` , `  bigquery.tables.update  ` , and `  bigquery.tables.updateData  ` IAM permissions.

Each of the following predefined IAM roles includes the permissions that you need in order to manually refresh a materialized view:

  - `  bigquery.dataEditor  `
  - `  bigquery.dataOwner  `
  - `  bigquery.admin  `

For more information about BigQuery Identity and Access Management (IAM), see [Predefined roles and permissions](/bigquery/docs/access-control) .

To update the data in the materialized view, call the [`  BQ.REFRESH_MATERIALIZED_VIEW  `](/bigquery/docs/reference/system-procedures#bqrefresh_materialized_view) system procedure. When this procedure is called, BigQuery identifies the changes that have taken place in the base tables and applies those changes to the materialized view. The query to run `  BQ.REFRESH_MATERIALIZED_VIEW  ` finishes when the refresh is complete.

``` text
CALL BQ.REFRESH_MATERIALIZED_VIEW('PROJECT.DATASET.MATERIALIZED_VIEW');
```

**Caution:** Don't perform more than one refresh at a time. If you run multiple refreshes concurrently for the same materialized view, then only the first refresh to complete is successful.

## Monitor materialized views

You can get information about materialized views and materialized views refresh jobs by using the BigQuery API. For more information, see [Monitor materialized views](/bigquery/docs/materialized-views-monitor) .
