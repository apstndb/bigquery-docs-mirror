# Access historical data

BigQuery lets you query and restore data stored in BigQuery that has been changed or deleted within your [time travel](/bigquery/docs/time-travel) window.

## Query data at a point in time

You can query a table's historical data from any point in time within the time travel window by using a [`  FOR SYSTEM_TIME AS OF  `](/bigquery/docs/reference/standard-sql/query-syntax#for_system_time_as_of) clause. This clause takes a constant timestamp expression and references the version of the table that was current at that timestamp. The table must be stored in BigQuery; it cannot be an external table. There is no limit on table size when using `  SYSTEM_TIME AS OF  ` .

For example, the following query returns a historical version of the table from one hour ago:

``` text
SELECT *
FROM `mydataset.mytable`
  FOR SYSTEM_TIME AS OF TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 1 HOUR);
```

**Note:** The `  FOR SYSTEM_TIME AS OF  ` clause is supported in GoogleSQL. For legacy SQL, [time decorators](/bigquery/docs/table-decorators#time_decorators) provide equivalent functionality.

If the timestamp specifies a time from prior to the time travel window or from before the table was created, then the query fails and returns an error like the following:

``` text
Invalid snapshot time 1601168925462 for table
myproject:mydataset.table1@1601168925462. Cannot read before 1601573410026.
```

After you replace an existing table by using the `  CREATE OR REPLACE TABLE  ` statement, you can use `  FOR SYSTEM_TIME AS OF  ` to query the previous version of the table.

If the table was deleted, then the query fails and returns an error like the following:

``` text
Not found: Table myproject:mydataset.table was not found in location LOCATION
```

## Restore a table from a point in time

You can restore a table from historical data by copying the historical data into a new table. Copying historical data works even if the table was deleted or has expired, as long as you restore the table within the duration of the time travel window.

When you restore a table from historical data, [tags](/bigquery/docs/tags) from the source table aren't copied to the destination table. Table partitioning information also isn't copied to the destination table. To recreate the partitioning scheme of the original table, you can view the initial table creation request in [Cloud Logging](/logging/docs/view/logs-explorer-interface) and use that information to partition the restored table.

You can restore a table that was deleted but is still within the time travel window by copying the table to a new table, using the `  @<time>  ` time decorator. You can't query a deleted table, even if you use a time decorator. You must restore it first.

Use the following syntax with the `  @<time>  ` time decorator:

  - `  tableid@ TIME  ` where `  TIME  ` is the number of milliseconds since the Unix epoch.
  - `  tableid@- TIME_OFFSET  ` where `  TIME_OFFSET  ` is the relative offset from the current time, in milliseconds.
  - `  tableid@0  ` : Specifies the oldest available historical data.

To restore a table, select one of the following options:

### Console

You can't undelete a table by using the Google Cloud console.

### bq

1.  In the Google Cloud console, activate Cloud Shell.
    
    At the bottom of the Google Cloud console, a [Cloud Shell](/shell/docs/how-cloud-shell-works) session starts and displays a command-line prompt. Cloud Shell is a shell environment with the Google Cloud CLI already installed and with values already set for your current project. It can take a few seconds for the session to initialize.

2.  To restore a table, first determine a UNIX timestamp of when the table existed (in milliseconds). You can use the Linux `  date  ` command to generate the Unix timestamp from a regular timestamp value:
    
    ``` bash
    date -d '2023-08-04 16:00:34.456789Z' +%s000
    ```

3.  Then, use the `  bq copy  ` command with the `  @<time>  ` time travel decorator to perform the table copy operation.
    
    For example, enter the following command to copy the `  mydataset.mytable  ` table at the time `  1418864998000  ` into a new table `  mydataset.newtable  ` .
    
    ``` bash
    bq cp mydataset.mytable@1418864998000 mydataset.newtable
    ```
    
    (Optional) Supply the `  --location  ` flag and set the value to your [location](/bigquery/docs/locations) .
    
    You can also specify a relative offset. The following example copies the version of a table from one hour ago:
    
    ``` bash
    bq cp mydataset.mytable@-3600000 mydataset.newtable
    ```
    
    **Note:** If you attempt to recover data prior to the time travel window or from a time before the table was created, you'll receive an `  Invalid time travel timestamp  ` error. For more information, see [Troubleshoot table recovery](/bigquery/docs/restore-deleted-tables#troubleshoot_table_recovery) .

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

// deleteAndUndeleteTable demonstrates how to recover a deleted table by copying it from a point in time
// that predates the deletion event.
func deleteAndUndeleteTable(projectID, datasetID, tableID string) error {
 // projectID := "my-project-id"
 // datasetID := "mydataset"
 // tableID := "mytable"
 ctx := context.Background()
 client, err := bigquery.NewClient(ctx, projectID)
 if err != nil {
     return fmt.Errorf("bigquery.NewClient: %v", err)
 }
 defer client.Close()

 ds := client.Dataset(datasetID)
 if _, err := ds.Table(tableID).Metadata(ctx); err != nil {
     return err
 }
 // Record the current time.  We'll use this as the snapshot time
 // for recovering the table.
 snapTime := time.Now()

 // "Accidentally" delete the table.
 if err := client.Dataset(datasetID).Table(tableID).Delete(ctx); err != nil {
     return err
 }

 // Construct the restore-from tableID using a snapshot decorator.
 snapshotTableID := fmt.Sprintf("%s@%d", tableID, snapTime.UnixNano()/1e6)
 // Choose a new table ID for the recovered table data.
 recoverTableID := fmt.Sprintf("%s_recovered", tableID)

 // Construct and run a copy job.
 copier := ds.Table(recoverTableID).CopierFrom(ds.Table(snapshotTableID))
 copier.WriteDisposition = bigquery.WriteTruncate
 job, err := copier.Run(ctx)
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

 ds.Table(recoverTableID).Delete(ctx)
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
import com.google.cloud.bigquery.CopyJobConfiguration;
import com.google.cloud.bigquery.Job;
import com.google.cloud.bigquery.JobInfo;
import com.google.cloud.bigquery.TableId;

// Sample to undeleting a table
public class UndeleteTable {

  public static void runUndeleteTable() {
    // TODO(developer): Replace these variables before running the sample.
    String datasetName = "MY_DATASET_NAME";
    String tableName = "MY_TABLE_TABLE";
    String recoverTableName = "MY_RECOVER_TABLE_TABLE";
    undeleteTable(datasetName, tableName, recoverTableName);
  }

  public static void undeleteTable(String datasetName, String tableName, String recoverTableName) {
    try {
      // Initialize client that will be used to send requests. This client only needs to be created
      // once, and can be reused for multiple requests.
      BigQuery bigquery = BigQueryOptions.getDefaultInstance().getService();

      // "Accidentally" delete the table.
      bigquery.delete(TableId.of(datasetName, tableName));

      // Record the current time.  We'll use this as the snapshot time
      // for recovering the table.
      long snapTime = System.currentTimeMillis();

      // Construct the restore-from tableID using a snapshot decorator.
      String snapshotTableId = String.format("%s@%d", tableName, snapTime);

      // Construct and run a copy job.
      CopyJobConfiguration configuration =
          CopyJobConfiguration.newBuilder(
                  // Choose a new table ID for the recovered table data.
                  TableId.of(datasetName, recoverTableName),
                  TableId.of(datasetName, snapshotTableId))
              .build();

      Job job = bigquery.create(JobInfo.of(configuration));
      job = job.waitFor();
      if (job.isDone() && job.getStatus().getError() == null) {
        System.out.println("Undelete table recovered successfully.");
      } else {
        System.out.println(
            "BigQuery was unable to copy the table due to an error: \n"
                + job.getStatus().getError());
        return;
      }
    } catch (BigQueryException | InterruptedException e) {
      System.out.println("Table not found. \n" + e.toString());
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

async function undeleteTable() {
  // Undeletes "my_table_to_undelete" from "my_dataset".

  /**
   * TODO(developer): Uncomment the following lines before running the sample.
   */
  // const datasetId = "my_dataset";
  // const tableId = "my_table_to_undelete";
  // const recoveredTableId = "my_recovered_table";

  /**
   * TODO(developer): Choose an appropriate snapshot point as epoch milliseconds.
   * For this example, we choose the current time as we're about to delete the
   * table immediately afterwards.
   */
  const snapshotEpoch = Date.now();

  // Delete the table
  await bigquery
    .dataset(datasetId)
    .table(tableId)
    .delete();

  console.log(`Table ${tableId} deleted.`);

  // Construct the restore-from table ID using a snapshot decorator.
  const snapshotTableId = `${tableId}@${snapshotEpoch}`;

  // Construct and run a copy job.
  await bigquery
    .dataset(datasetId)
    .table(snapshotTableId)
    .copy(bigquery.dataset(datasetId).table(recoveredTableId));

  console.log(
    `Copied data from deleted table ${tableId} to ${recoveredTableId}`
  );
}
```

### Python

Before trying this sample, follow the Python setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Python API reference documentation](/python/docs/reference/bigquery/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` python
import time

from google.cloud import bigquery

# Construct a BigQuery client object.
client = bigquery.Client()

# TODO(developer): Choose a table to recover.
# table_id = "your-project.your_dataset.your_table"

# TODO(developer): Choose a new table ID for the recovered table data.
# recovered_table_id = "your-project.your_dataset.your_table_recovered"

# TODO(developer): Choose an appropriate snapshot point as epoch
# milliseconds. For this example, we choose the current time as we're about
# to delete the table immediately afterwards.
snapshot_epoch = int(time.time() * 1000)

# ...

# "Accidentally" delete the table.
client.delete_table(table_id)  # Make an API request.

# Construct the restore-from table ID using a snapshot decorator.
snapshot_table_id = "{}@{}".format(table_id, snapshot_epoch)

# Construct and run a copy job.
job = client.copy_table(
    snapshot_table_id,
    recovered_table_id,
    # Must match the source and destination tables location.
    location="US",
)  # Make an API request.

job.result()  # Wait for the job to complete.

print(
    "Copied data from deleted table {} to {}".format(table_id, recovered_table_id)
)
```

If you anticipate that you might want to restore a table later than what is allowed by the time travel window, then create a table snapshot of the table. For more information, see [Introduction to table snapshots](/bigquery/docs/table-snapshots-intro) .

You cannot restore a logical view directly. For more information, see [Restore a view](/bigquery/docs/managing-views#restore_a_view) .

## What's next

  - Learn more about [table snapshots](/bigquery/docs/table-snapshots-intro) .
  - Learn more about [Data retention with time travel and fail-safe](/bigquery/docs/time-travel) .
  - Learn more about [managing tables](/bigquery/docs/managing-tables) .
