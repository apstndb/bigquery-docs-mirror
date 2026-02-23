# Creating partitioned tables

This page describes how to create partitioned tables in BigQuery. For an overview of partitioned tables, see [Introduction to partitioned tables](/bigquery/docs/partitioned-tables) .

## Before you begin

Grant Identity and Access Management (IAM) roles that give users the necessary permissions to perform each task in this document.

### Required permissions

### Required roles

To get the permissions that you need to create a table, ask your administrator to grant you the following IAM roles :

  - [BigQuery Job User](/iam/docs/roles-permissions/bigquery#bigquery.jobUser) ( `  roles/bigquery.jobUser  ` ) on the project if you're creating a table by loading data or by saving query results to a table.
  - [BigQuery Data Editor](/iam/docs/roles-permissions/bigquery#bigquery.dataEditor) ( `  roles/bigquery.dataEditor  ` ) on the dataset where you're creating the table.

For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

These predefined roles contain the permissions required to create a table. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

The following permissions are required to create a table:

  - `  bigquery.tables.create  ` on the dataset where you're creating the table.
  - `  bigquery.tables.getData  ` on all tables and views that your query references if you're saving query results as a table.
  - `  bigquery.jobs.create  ` on the project if you're creating the table by loading data or by saving query results to a table.
  - `  bigquery.tables.updateData  ` on the table if you're appending to or overwriting a table with query results.

You might also be able to get these permissions with [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

## Create an empty partitioned table

The steps to create a partitioned table in BigQuery are similar to creating a [standard table](/bigquery/docs/tables) , except that you specify the partitioning options, along with any other table options.

### Create a time-unit column-partitioned table

To create an empty time-unit column-partitioned table with a schema definition:

### Console

In the Google Cloud console, go to the **BigQuery** page.

In the left pane, click explore **Explorer** .

In the **Explorer** pane, expand your project, click **Datasets** , and then select a dataset.

In the **Dataset info** section, click add\_box **Create table** .

In the **Create table** pane, specify the following details:

1.  In the **Source** section, select **Empty table** in the **Create table from** list.
2.  In the **Destination** section, specify the following details:
    1.  For **Dataset** , select the dataset in which you want to create the table.
    2.  In the **Table** field, enter the name of the table that you want to create.
    3.  Verify that the **Table type** field is set to **Native table** .
3.  In the **Schema** section, enter the [schema](/bigquery/docs/schemas) definition. The schema must include a `  DATE  ` , `  TIMESTAMP  ` , or `  DATETIME  ` column for the partitioning column. For more information, see [Specifying a schema](/bigquery/docs/schemas) . You can enter schema information manually by using one of the following methods:
      - Option 1: Click **Edit as text** and paste the schema in the form of a JSON array. When you use a JSON array, you generate the schema using the same process as [creating a JSON schema file](/bigquery/docs/schemas#specifying_a_json_schema_file) . You can view the schema of an existing table in JSON format by entering the following command:
        
        ``` text
            bq show --format=prettyjson dataset.table
            
        ```
    
      - Option 2: Click add\_box **Add field** and enter the table schema. Specify each field's **Name** , [**Type**](/bigquery/docs/schemas#standard_sql_data_types) , and [**Mode**](/bigquery/docs/schemas#modes) .
4.  In the **Partition and cluster settings** section, in the **Partitioning** list, select **Partition by field** , and then choose the partitioning column. This option is only available if the schema contains a `  DATE  ` , `  TIMESTAMP  ` , or `  DATETIME  ` column.
5.  Optional: To require a partition filter on all queries for this table, select the **Require partition filter** checkbox. A partition filter can reduce cost and improve performance. For more information, see [Set partition filter requirements](/bigquery/docs/managing-partitioned-tables#require-filter) .
6.  Select the **Partitioning type** .
7.  Optional: In the **Advanced options** section, if you want to use a customer-managed encryption key, then select the **Use a customer-managed encryption key (CMEK)** option. By default, BigQuery [encrypts customer content stored at rest](/docs/security/encryption/default-encryption) by using a Google-owned and Google-managed encryption key.
8.  Click **Create table** .

**Note:** You can't set the partition expiration in the Google Cloud console. To set the partition after you create the table, see [Updating the partition expiration](/bigquery/docs/managing-partitioned-tables#partition-expiration) .

### SQL

To create a time-unit column-partitioned table, use the [`  CREATE TABLE  ` DDL statement](/bigquery/docs/reference/standard-sql/data-definition-language#create_table_statement) with a [`  PARTITION BY  ` clause](/bigquery/docs/reference/standard-sql/data-definition-language#partition_expression) .

The following example creates a table with daily partitions based on the `  transaction_date  ` column:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
    CREATE TABLE
      mydataset.newtable (transaction_id INT64, transaction_date DATE)
    PARTITION BY
      transaction_date
      OPTIONS (
        partition_expiration_days = 3,
        require_partition_filter = TRUE);
    ```
    
    Use the [`  OPTIONS  ` clause](/bigquery/docs/reference/standard-sql/data-definition-language#table_option_list) to set table options such as the [partition expiration](/bigquery/docs/managing-partitioned-tables#partition-expiration) and the [partition filter requirements](/bigquery/docs/managing-partitioned-tables#require-filter) .

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](/bigquery/docs/running-queries#queries) .

The default partitioning type for `  DATE  ` columns is daily partitioning. To specify a different partitioning type, include the [`  DATE_TRUNC  `](/bigquery/docs/reference/standard-sql/date_functions#date_trunc) function in the `  PARTITION BY  ` clause. For example, the following query creates a table with monthly partitions:

``` text
CREATE TABLE
  mydataset.newtable (transaction_id INT64, transaction_date DATE)
PARTITION BY
  DATE_TRUNC(transaction_date, MONTH)
  OPTIONS (
    partition_expiration_days = 3,
    require_partition_filter = TRUE);
```

You can also specify a `  TIMESTAMP  ` or `  DATETIME  ` column as the partitioning column. In that case, include the `  TIMESTAMP_TRUNC  ` or `  DATETIME_TRUNC  ` function in the `  PARTITION BY  ` clause to specify the partition type. For example, the following statement creates a table with daily partitions based on a `  TIMESTAMP  ` column:

``` text
CREATE TABLE
  mydataset.newtable (transaction_id INT64, transaction_ts TIMESTAMP)
PARTITION BY
  TIMESTAMP_TRUNC(transaction_ts, DAY)
  OPTIONS (
    partition_expiration_days = 3,
    require_partition_filter = TRUE);
```

### bq

1.  In the Google Cloud console, activate Cloud Shell.
    
    At the bottom of the Google Cloud console, a [Cloud Shell](/shell/docs/how-cloud-shell-works) session starts and displays a command-line prompt. Cloud Shell is a shell environment with the Google Cloud CLI already installed and with values already set for your current project. It can take a few seconds for the session to initialize.

2.  Use the [`  bq mk  `](/bigquery/docs/reference/bq-cli-reference#mk-table) command with the `  --table  ` flag (or `  -t  ` shortcut):
    
    ``` text
    bq mk \
       --table \
       --schema SCHEMA \
       --time_partitioning_field COLUMN \
       --time_partitioning_type UNIT_TIME \
       --time_partitioning_expiration EXPIRATION_TIME \
       --require_partition_filter=BOOLEAN
       PROJECT_ID:DATASET.TABLE
    ```
    
    Replace the following:
    
      - SCHEMA : A schema definition in the format `  column:data_type,column:data_type  ` or the path to a JSON schema file on your local machine. For more information, see [Specifying a schema](/bigquery/docs/schemas) .
      - COLUMN : The name of the partitioning column. In the table schema, this column must be a `  TIMESTAMP  ` , `  DATETIME  ` , or `  DATE  ` type.
      - UNIT\_TIME : The partitioning type. Supported values include `  DAY  ` , `  HOUR  ` , `  MONTH  ` , or `  YEAR  ` .
      - EXPIRATION\_TIME : The expiration time for the table's partitions, in seconds. The `  --time_partitioning_expiration  ` flag is optional. For more information, see [Set the partition expiration](/bigquery/docs/managing-partitioned-tables#partition-expiration) .
      - BOOLEAN : If `  true  ` then queries on this table must include a partition filter. The `  --require_partition_filter  ` flag is optional. For more information, see [Set partition filter requirements](/bigquery/docs/managing-partitioned-tables#require-filter) .
      - PROJECT\_ID : The project ID. If omitted, your default project is used.
      - DATASET : The name of a dataset in your project.
      - TABLE : The name of the table to create.
    
    For other command-line options, see [`  bq mk  `](/bigquery/docs/reference/bq-cli-reference#mk-table) .
    
    The following example creates a table named `  mytable  ` that is partitioned on the `  ts  ` column, using hourly partitioning. The partition expiration is 259,200 seconds (3 days).
    
    ``` text
    bq mk \
       -t \
       --schema 'ts:TIMESTAMP,qtr:STRING,sales:FLOAT' \
       --time_partitioning_field ts \
       --time_partitioning_type HOUR \
       --time_partitioning_expiration 259200  \
       mydataset.mytable
    ```

### Terraform

Use the [`  google_bigquery_table  `](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/bigquery_table) resource.

**Note:** To create BigQuery objects using Terraform, you must enable the Cloud Resource Manager API.

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

The following example creates a table named `  mytable  ` that is partitioned by day:

``` terraform
resource "google_bigquery_dataset" "default" {
  dataset_id                      = "mydataset"
  default_partition_expiration_ms = 2592000000  # 30 days
  default_table_expiration_ms     = 31536000000 # 365 days
  description                     = "dataset description"
  location                        = "US"
  max_time_travel_hours           = 96 # 4 days

  labels = {
    billing_group = "accounting",
    pii           = "sensitive"
  }
}

resource "google_bigquery_table" "default" {
  dataset_id = google_bigquery_dataset.default.dataset_id
  table_id   = "mytable"

  time_partitioning {
    type          = "DAY"
    field         = "Created"
    expiration_ms = 432000000 # 5 days
  }
  require_partition_filter = true

  schema = <<EOF
[
  {
    "name": "ID",
    "type": "INT64",
    "mode": "NULLABLE",
    "description": "Item ID"
  },
  {
    "name": "Created",
    "type": "TIMESTAMP",
    "description": "Record creation timestamp"
  },
  {
    "name": "Item",
    "type": "STRING",
    "mode": "NULLABLE"
  }
]
EOF

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

Call the [`  tables.insert  `](/bigquery/docs/reference/rest/v2/tables/insert) method with a defined [table resource](/bigquery/docs/reference/rest/v2/tables) that specifies the `  timePartitioning  ` property and the `  schema  ` property.

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

// createTablePartitioned demonstrates creating a table and specifying a time partitioning configuration.
func createTablePartitioned(projectID, datasetID, tableID string) error {
 // projectID := "my-project-id"
 // datasetID := "mydatasetid"
 // tableID := "mytableid"
 ctx := context.Background()

 client, err := bigquery.NewClient(ctx, projectID)
 if err != nil {
     return fmt.Errorf("bigquery.NewClient: %v", err)
 }
 defer client.Close()

 sampleSchema := bigquery.Schema{
     {Name: "name", Type: bigquery.StringFieldType},
     {Name: "post_abbr", Type: bigquery.IntegerFieldType},
     {Name: "date", Type: bigquery.DateFieldType},
 }
 metadata := &bigquery.TableMetadata{
     TimePartitioning: &bigquery.TimePartitioning{
         Field:      "date",
         Expiration: 90 * 24 * time.Hour,
     },
     Schema: sampleSchema,
 }
 tableRef := client.Dataset(datasetID).Table(tableID)
 if err := tableRef.Create(ctx, metadata); err != nil {
     return err
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
import com.google.cloud.bigquery.Field;
import com.google.cloud.bigquery.Schema;
import com.google.cloud.bigquery.StandardSQLTypeName;
import com.google.cloud.bigquery.StandardTableDefinition;
import com.google.cloud.bigquery.TableId;
import com.google.cloud.bigquery.TableInfo;
import com.google.cloud.bigquery.TimePartitioning;

// Sample to create a partition table
public class CreatePartitionedTable {

  public static void main(String[] args) {
    // TODO(developer): Replace these variables before running the sample.
    String datasetName = "MY_DATASET_NAME";
    String tableName = "MY_TABLE_NAME";
    Schema schema =
        Schema.of(
            Field.of("name", StandardSQLTypeName.STRING),
            Field.of("post_abbr", StandardSQLTypeName.STRING),
            Field.of("date", StandardSQLTypeName.DATE));
    createPartitionedTable(datasetName, tableName, schema);
  }

  public static void createPartitionedTable(String datasetName, String tableName, Schema schema) {
    try {
      // Initialize client that will be used to send requests. This client only needs to be created
      // once, and can be reused for multiple requests.
      BigQuery bigquery = BigQueryOptions.getDefaultInstance().getService();

      TableId tableId = TableId.of(datasetName, tableName);

      TimePartitioning partitioning =
          TimePartitioning.newBuilder(TimePartitioning.Type.DAY)
              .setField("date") //  name of column to use for partitioning
              .setExpirationMs(7776000000L) // 90 days
              .build();

      StandardTableDefinition tableDefinition =
          StandardTableDefinition.newBuilder()
              .setSchema(schema)
              .setTimePartitioning(partitioning)
              .build();
      TableInfo tableInfo = TableInfo.newBuilder(tableId, tableDefinition).build();

      bigquery.create(tableInfo);
      System.out.println("Partitioned table created successfully");
    } catch (BigQueryException e) {
      System.out.println("Partitioned table was not created. \n" + e.toString());
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

async function createTablePartitioned() {
  // Creates a new partitioned table named "my_table" in "my_dataset".

  /**
   * TODO(developer): Uncomment the following lines before running the sample.
   */
  // const datasetId = "my_dataset";
  // const tableId = "my_table";
  const schema = 'Name:string, Post_Abbr:string, Date:date';

  // For all options, see https://cloud.google.com/bigquery/docs/reference/v2/tables#resource
  const options = {
    schema: schema,
    location: 'US',
    timePartitioning: {
      type: 'DAY',
      expirationMS: '7776000000',
      field: 'date',
    },
  };

  // Create a new table in the dataset
  const [table] = await bigquery
    .dataset(datasetId)
    .createTable(tableId, options);
  console.log(`Table ${table.id} created with partitioning: `);
  console.log(table.metadata.timePartitioning);
}
```

### Python

Before trying this sample, follow the Python setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Python API reference documentation](/python/docs/reference/bigquery/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` python
from google.cloud import bigquery

client = bigquery.Client()

# Use format "your-project.your_dataset.your_table_name" for table_id
table_id = your_fully_qualified_table_id
schema = [
    bigquery.SchemaField("name", "STRING"),
    bigquery.SchemaField("post_abbr", "STRING"),
    bigquery.SchemaField("date", "DATE"),
]
table = bigquery.Table(table_id, schema=schema)
table.time_partitioning = bigquery.TimePartitioning(
    type_=bigquery.TimePartitioningType.DAY,
    field="date",  # name of column to use for partitioning
    expiration_ms=1000 * 60 * 60 * 24 * 90,
)  # 90 days

table = client.create_table(table)

print(
    f"Created table {table.project}.{table.dataset_id}.{table.table_id}, "
    f"partitioned on column {table.time_partitioning.field}."
)
```

### Create an ingestion-time partitioned table

To create an empty ingestion-time partitioned table with a schema definition:

### Console

1.  Open the BigQuery page in the Google Cloud console.

2.  In the **Explorer** panel, expand your project and select a dataset.

3.  Expand the more\_vert **Actions** option and click **Open** .

4.  In the details panel, click **Create table** add\_box .

5.  On the **Create table** page, in the **Source** section, select **Empty table.**

6.  In the **Destination** section:
    
      - For **Dataset name** , choose the appropriate dataset.
      - In the **Table name** field, enter the name of the table.
      - Verify that **Table type** is set to **Native table** .

7.  In the **Schema** section, enter the [schema](/bigquery/docs/schemas) definition.

8.  In the **Partition and cluster settings** section, for **Partitioning** , click **Partition by ingestion time** .

9.  (Optional) To require a partition filter on all queries for this table, select the **Require partition filter** checkbox. Requiring a partition filter can reduce cost and improve performance. For more information, see [Set partition filter requirements](/bigquery/docs/managing-partitioned-tables#require-filter) .

10. Click **Create table** .

**Note:** You can't set the partition expiration in the Google Cloud console. To set the partition after you create the table, see [Updating the partition expiration](/bigquery/docs/managing-partitioned-tables#partition-expiration) .

### SQL

To create an ingestion-time partitioned table, use the [`  CREATE TABLE  ` statement](/bigquery/docs/reference/standard-sql/data-definition-language#create_table_statement) with a [`  PARTITION BY  ` clause](/bigquery/docs/reference/standard-sql/data-definition-language#partition_expression) that partitions on `  _PARTITIONDATE  ` .

The following example creates a table with daily partitions:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
    CREATE TABLE
      mydataset.newtable (transaction_id INT64)
    PARTITION BY
      _PARTITIONDATE
      OPTIONS (
        partition_expiration_days = 3,
        require_partition_filter = TRUE);
    ```
    
    Use the [`  OPTIONS  ` clause](/bigquery/docs/reference/standard-sql/data-definition-language#table_option_list) to set table options such as the [partition expiration](/bigquery/docs/managing-partitioned-tables#partition-expiration) and the [partition filter requirements](/bigquery/docs/managing-partitioned-tables#require-filter) .

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](/bigquery/docs/running-queries#queries) .

The default partitioning type for ingestion-time partitioning is daily partitioning. To specify a different partitioning type, include the [`  DATE_TRUNC  `](/bigquery/docs/reference/standard-sql/date_functions#date_trunc) function in the `  PARTITION BY  ` clause. For example, the following query creates a table with monthly partitions:

``` text
CREATE TABLE
  mydataset.newtable (transaction_id INT64)
PARTITION BY
  DATE_TRUNC(_PARTITIONTIME, MONTH)
  OPTIONS (
    partition_expiration_days = 3,
    require_partition_filter = TRUE);
```

### bq

1.  In the Google Cloud console, activate Cloud Shell.
    
    At the bottom of the Google Cloud console, a [Cloud Shell](/shell/docs/how-cloud-shell-works) session starts and displays a command-line prompt. Cloud Shell is a shell environment with the Google Cloud CLI already installed and with values already set for your current project. It can take a few seconds for the session to initialize.

2.  Use the [`  bq mk  `](/bigquery/docs/reference/bq-cli-reference#mk-table) command with the `  --table  ` flag (or `  -t  ` shortcut):
    
    ``` text
    bq mk \
       --table \
       --schema SCHEMA \
       --time_partitioning_type UNIT_TIME \
       --time_partitioning_expiration EXPIRATION_TIME \
       --require_partition_filter=BOOLEAN  \
       PROJECT_ID:DATASET.TABLE
    ```
    
    Replace the following:
    
      - SCHEMA : A definition in the format `  column:data_type,column:data_type  ` or the path to a JSON schema file on your local machine. For more information, see [Specifying a schema](/bigquery/docs/schemas) .
      - UNIT\_TIME : The partitioning type. Supported values include `  DAY  ` , `  HOUR  ` , `  MONTH  ` , or `  YEAR  ` .
      - EXPIRATION\_TIME : The expiration time for the table's partitions, in seconds. The `  --time_partitioning_expiration  ` flag is optional. For more information, see [Set the partition expiration](/bigquery/docs/managing-partitioned-tables#partition-expiration) .
      - BOOLEAN : If `  true  ` then queries on this table must include a partition filter. The `  --require_partition_filter  ` flag is optional. For more information, see [Set partition filter requirements](/bigquery/docs/managing-partitioned-tables#require-filter) .
      - PROJECT\_ID : The project ID. If omitted, your default project is used.
      - DATASET : The name of a dataset in your project.
      - TABLE : The name of the table to create.
    
    For other command-line options, see [`  bq mk  `](/bigquery/docs/reference/bq-cli-reference#mk-table) .
    
    The following example creates an ingestion-time partitioned table named `  mytable  ` . The table has daily partitioning, with a partition expiration of 259,200 seconds (3 days).
    
    ``` text
    bq mk \
       -t \
       --schema qtr:STRING,sales:FLOAT,year:STRING \
       --time_partitioning_type DAY \
       --time_partitioning_expiration 259200 \
       mydataset.mytable
    ```

### Terraform

Use the [`  google_bigquery_table  `](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/bigquery_table) resource.

**Note:** To create BigQuery objects using Terraform, you must enable the Cloud Resource Manager API.

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

The following example creates a table named `  mytable  ` that is partitioned by ingestion time:

``` terraform
resource "google_bigquery_dataset" "default" {
  dataset_id                      = "mydataset"
  default_partition_expiration_ms = 2592000000  # 30 days
  default_table_expiration_ms     = 31536000000 # 365 days
  description                     = "dataset description"
  location                        = "US"
  max_time_travel_hours           = 96 # 4 days

  labels = {
    billing_group = "accounting",
    pii           = "sensitive"
  }
}

resource "google_bigquery_table" "default" {
  dataset_id = google_bigquery_dataset.default.dataset_id
  table_id   = "mytable"

  time_partitioning {
    type          = "MONTH"
    expiration_ms = 604800000 # 7 days
  }
  require_partition_filter = true

  schema = <<EOF
[
  {
    "name": "ID",
    "type": "INT64",
    "mode": "NULLABLE",
    "description": "Item ID"
  },
  {
    "name": "Item",
    "type": "STRING",
    "mode": "NULLABLE"
  }
]
EOF

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

Call the [`  tables.insert  `](/bigquery/docs/reference/rest/v2/tables/insert) method with a defined [table resource](/bigquery/docs/reference/rest/v2/tables) that specifies the `  timePartitioning  ` property and the `  schema  ` property.

### Create an integer-range partitioned table

To create an empty integer-range partitioned table with a schema definition:

### Console

1.  Open the BigQuery page in the Google Cloud console.

2.  In the **Explorer** panel, expand your project and select a dataset.

3.  Expand the more\_vert **Actions** option and click **Open** .

4.  In the details panel, click **Create table** add\_box .

5.  On the **Create table** page, in the **Source** section, select **Empty table.**

6.  In the **Destination** section:
    
      - For **Dataset name** , choose the appropriate dataset.
      - In the **Table name** field, enter the name of the table.
      - Verify that **Table type** is set to **Native table** .

7.  In the **Schema** section, enter the schema definition. Make sure the schema includes an `  INTEGER  ` column for the partitioning column. For more information, see [Specifying a schema](/bigquery/docs/schemas) .

8.  In the **Partition and cluster settings** section, in the **Partitioning** drop-down list, select **Partition by field** and choose the partitioning column. This option is only available if the schema contains an `  INTEGER  ` column.

9.  Provide values for **Start** , **End** , and **Interval** :
    
      - **Start** is the start of first partition range (inclusive).
      - **End** is the end of last partition range (exclusive).
      - **Interval** is the width of each partition range.
    
    Values outside of these ranges go into a special `  __UNPARTITIONED__  ` partition.

10. (Optional) To require a partition filter on all queries for this table, select the **Require partition filter** checkbox. Requiring a partition filter can reduce cost and improve performance. For more information, see [Set partition filter requirements](/bigquery/docs/managing-partitioned-tables#require-filter) .

11. Click **Create table** .

**Note:** You can't set the partition expiration in the Google Cloud console. To set the partition after you create the table, see [Updating the partition expiration](/bigquery/docs/managing-partitioned-tables#partition-expiration) .

### SQL

To create an integer-range partitioned table, use the [`  CREATE TABLE  ` DDL statement](/bigquery/docs/reference/standard-sql/data-definition-language#create_table_statement) with a [`  PARTITION BY  ` clause](/bigquery/docs/reference/standard-sql/data-definition-language#partition_expression) .

The following example creates a table that is partitioned on the `  customer_id  ` column with start 0, end 100, and interval 10:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
    CREATE TABLE mydataset.newtable (customer_id INT64, date1 DATE)
    PARTITION BY
      RANGE_BUCKET(customer_id, GENERATE_ARRAY(0, 100, 10))
      OPTIONS (
        require_partition_filter = TRUE);
    ```
    
    Use the [`  OPTIONS  ` clause](/bigquery/docs/reference/standard-sql/data-definition-language#table_option_list) to set table options such as the [partition filter requirements](/bigquery/docs/managing-partitioned-tables#require-filter) .

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](/bigquery/docs/running-queries#queries) .

### bq

1.  In the Google Cloud console, activate Cloud Shell.
    
    At the bottom of the Google Cloud console, a [Cloud Shell](/shell/docs/how-cloud-shell-works) session starts and displays a command-line prompt. Cloud Shell is a shell environment with the Google Cloud CLI already installed and with values already set for your current project. It can take a few seconds for the session to initialize.

2.  Use the [`  bq mk  `](/bigquery/docs/reference/bq-cli-reference#mk-table) command with the `  --table  ` flag (or `  -t  ` shortcut):
    
    ``` text
    bq mk \
       --schema schema \
       --range_partitioning=COLUMN_NAME,START,END,INTERVAL \
       --require_partition_filter=BOOLEAN  \
       PROJECT_ID:DATASET.TABLE
    ```
    
    Replace the following:
    
      - SCHEMA : An inline schema definition in the format `  column:data_type,column:data_type  ` or the path to a JSON schema file on your local machine. For more information, see [Specifying a schema](/bigquery/docs/schemas) .
      - COLUMN\_NAME : The name of the partitioning column. In the table schema, this column must be an `  INTEGER  ` type.
      - START : The start of first partition range (inclusive).
      - END : The end of last partition range (exclusive).
      - INTERVAL : The width of each partition range.
      - BOOLEAN : If `  true  ` then queries on this table must include a partition filter. The `  --require_partition_filter  ` flag is optional. For more information, see [Set partition filter requirements](/bigquery/docs/managing-partitioned-tables#require-filter) .
      - PROJECT\_ID : The project ID. If omitted, your default project is used.
      - DATASET : The name of a dataset in your project.
      - TABLE : The name of the table to create.
    
    Values outside of the partition range go into a special `  __UNPARTITIONED__  ` partition.
    
    For other command-line options, see [`  bq mk  `](/bigquery/docs/reference/bq-cli-reference#mk-table) .
    
    The following example creates a table named `  mytable  ` that is partitioned on the `  customer_id  ` column.
    
    ``` text
    bq mk \
       -t \
       --schema 'customer_id:INTEGER,qtr:STRING,sales:FLOAT' \
       --range_partitioning=customer_id,0,100,10 \
       mydataset.mytable
    ```

### Terraform

Use the [`  google_bigquery_table  `](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/bigquery_table) resource.

**Note:** To create BigQuery objects using Terraform, you must enable the Cloud Resource Manager API.

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

The following example creates a table named `  mytable  ` that is partitioned by integer range:

``` terraform
resource "google_bigquery_dataset" "default" {
  dataset_id                      = "mydataset"
  default_partition_expiration_ms = 2592000000  # 30 days
  default_table_expiration_ms     = 31536000000 # 365 days
  description                     = "dataset description"
  location                        = "US"
  max_time_travel_hours           = 96 # 4 days

  labels = {
    billing_group = "accounting",
    pii           = "sensitive"
  }
}

resource "google_bigquery_table" "default" {
  dataset_id = google_bigquery_dataset.default.dataset_id
  table_id   = "mytable"

  range_partitioning {
    field = "ID"
    range {
      start    = 0
      end      = 1000
      interval = 10
    }
  }
  require_partition_filter = true

  schema = <<EOF
[
  {
    "name": "ID",
    "type": "INT64",
    "description": "Item ID"
  },
  {
    "name": "Item",
    "type": "STRING",
    "mode": "NULLABLE"
  }
]
EOF

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

Call the [`  tables.insert  `](/bigquery/docs/reference/rest/v2/tables/insert) method with a defined [table resource](/bigquery/docs/reference/rest/v2/tables) that specifies the `  rangePartitioning  ` property and the `  schema  ` property.

### Java

Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Java API reference documentation](/java/docs/reference/google-cloud-bigquery/latest/overview) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` java
import com.google.cloud.bigquery.BigQuery;
import com.google.cloud.bigquery.BigQueryException;
import com.google.cloud.bigquery.BigQueryOptions;
import com.google.cloud.bigquery.Field;
import com.google.cloud.bigquery.RangePartitioning;
import com.google.cloud.bigquery.Schema;
import com.google.cloud.bigquery.StandardSQLTypeName;
import com.google.cloud.bigquery.StandardTableDefinition;
import com.google.cloud.bigquery.TableId;
import com.google.cloud.bigquery.TableInfo;

// Sample to create a range partitioned table
public class CreateRangePartitionedTable {

  public static void main(String[] args) {
    // TODO(developer): Replace these variables before running the sample.
    String datasetName = "MY_DATASET_NAME";
    String tableName = "MY_TABLE_NAME";
    Schema schema =
        Schema.of(
            Field.of("integerField", StandardSQLTypeName.INT64),
            Field.of("stringField", StandardSQLTypeName.STRING),
            Field.of("booleanField", StandardSQLTypeName.BOOL),
            Field.of("dateField", StandardSQLTypeName.DATE));
    createRangePartitionedTable(datasetName, tableName, schema);
  }

  public static void createRangePartitionedTable(
      String datasetName, String tableName, Schema schema) {
    try {
      // Initialize client that will be used to send requests. This client only needs to be created
      // once, and can be reused for multiple requests.
      BigQuery bigquery = BigQueryOptions.getDefaultInstance().getService();

      TableId tableId = TableId.of(datasetName, tableName);

      // Note: The field must be a top- level, NULLABLE/REQUIRED field.
      // The only supported type is INTEGER/INT64
      RangePartitioning partitioning =
          RangePartitioning.newBuilder()
              .setField("integerField")
              .setRange(
                  RangePartitioning.Range.newBuilder()
                      .setStart(1L)
                      .setInterval(2L)
                      .setEnd(10L)
                      .build())
              .build();

      StandardTableDefinition tableDefinition =
          StandardTableDefinition.newBuilder()
              .setSchema(schema)
              .setRangePartitioning(partitioning)
              .build();
      TableInfo tableInfo = TableInfo.newBuilder(tableId, tableDefinition).build();

      bigquery.create(tableInfo);
      System.out.println("Range partitioned table created successfully");
    } catch (BigQueryException e) {
      System.out.println("Range partitioned table was not created. \n" + e.toString());
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

async function createTableRangePartitioned() {
  // Creates a new integer range partitioned table named "my_table"
  // in "my_dataset".

  /**
   * TODO(developer): Uncomment the following lines before running the sample.
   */
  // const datasetId = "my_dataset";
  // const tableId = "my_table";

  const schema = [
    {name: 'fullName', type: 'STRING'},
    {name: 'city', type: 'STRING'},
    {name: 'zipcode', type: 'INTEGER'},
  ];

  // To use integer range partitioning, select a top-level REQUIRED or
  // NULLABLE column with INTEGER / INT64 data type. Values that are
  // outside of the range of the table will go into the UNPARTITIONED
  // partition. Null values will be in the NULL partition.
  const rangePartition = {
    field: 'zipcode',
    range: {
      start: 0,
      end: 100000,
      interval: 10,
    },
  };

  // For all options, see https://cloud.google.com/bigquery/docs/reference/v2/tables#resource
  const options = {
    schema: schema,
    rangePartitioning: rangePartition,
  };

  // Create a new table in the dataset
  const [table] = await bigquery
    .dataset(datasetId)
    .createTable(tableId, options);

  console.log(`Table ${table.id} created with integer range partitioning: `);
  console.log(table.metadata.rangePartitioning);
}
```

### Python

Before trying this sample, follow the Python setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Python API reference documentation](/python/docs/reference/bigquery/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` python
from google.cloud import bigquery

# Construct a BigQuery client object.
client = bigquery.Client()

# TODO(developer): Set table_id to the ID of the table to create.
# table_id = "your-project.your_dataset.your_table_name"

schema = [
    bigquery.SchemaField("full_name", "STRING"),
    bigquery.SchemaField("city", "STRING"),
    bigquery.SchemaField("zipcode", "INTEGER"),
]

table = bigquery.Table(table_id, schema=schema)
table.range_partitioning = bigquery.RangePartitioning(
    # To use integer range partitioning, select a top-level REQUIRED /
    # NULLABLE column with INTEGER / INT64 data type.
    field="zipcode",
    range_=bigquery.PartitionRange(start=0, end=100000, interval=10),
)
table = client.create_table(table)  # Make an API request.
print(
    "Created table {}.{}.{}".format(table.project, table.dataset_id, table.table_id)
)
```

## Create a partitioned table from a query result

You can create a partitioned table from a query result in the following ways:

  - In SQL, use a `  CREATE TABLE ... AS SELECT  ` statement. You can use this approach to create a table that is partitioned by time-unit column or integer range, but not ingestion time.

  - Use the bq command-line tool or the BigQuery API to set a destination table for a query. When the query runs, BigQuery writes the results to the destination table. You can use this approach for any partitioning type.

  - Call the `  jobs.insert  ` API method and specify the partitioning in either the `  timePartitioning  ` property or the `  rangePartitioning  ` property.

### SQL

Use the [`  CREATE TABLE  `](/bigquery/docs/reference/standard-sql/data-definition-language#create_table_statement) statement. Include a [`  PARTITION BY  `](/bigquery/docs/reference/standard-sql/data-definition-language#partition_expression) clause to configure the partitioning.

The following example creates a table that is partitioned on the `  transaction_date  ` column:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
    CREATE TABLE
      mydataset.newtable (transaction_id INT64, transaction_date DATE)
    PARTITION BY
      transaction_date
    AS (
      SELECT
        transaction_id, transaction_date
      FROM
        mydataset.mytable
    );
    ```
    
    Use the [`  OPTIONS  ` clause](/bigquery/docs/reference/standard-sql/data-definition-language#table_option_list) to set table options such as the [partition filter requirements](/bigquery/docs/managing-partitioned-tables#require-filter) .

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](/bigquery/docs/running-queries#queries) .

### bq

1.  In the Google Cloud console, activate Cloud Shell.
    
    At the bottom of the Google Cloud console, a [Cloud Shell](/shell/docs/how-cloud-shell-works) session starts and displays a command-line prompt. Cloud Shell is a shell environment with the Google Cloud CLI already installed and with values already set for your current project. It can take a few seconds for the session to initialize.

2.  To create a partitioned table from a query, use the [`  bq query  `](/bigquery/docs/reference/bq-cli-reference#bq_query) command with the `  --destination_table  ` flag and the `  --time_partitioning_type  ` flag.
    
    Time-unit column-partitioning:
    
    ``` text
    bq query \
       --use_legacy_sql=false \
       --destination_table TABLE_NAME \
       --time_partitioning_field COLUMN \
       --time_partitioning_type UNIT_TIME \
       'QUERY_STATEMENT'
    ```
    
    Ingestion-time partitioning:
    
    ``` text
    bq query \
       --use_legacy_sql=false \
       --destination_table TABLE_NAME \
       --time_partitioning_type UNIT_TIME \
       'QUERY_STATEMENT'
    ```
    
    Integer-range partitioning:
    
    ``` text
    bq query \
       --use_legacy_sql=false \
       --destination_table PROJECT_ID:DATASET.TABLE \
       --range_partitioning COLUMN,START,END,INTERVAL \
       'QUERY_STATEMENT'
    ```
    
    Replace the following:
    
      - PROJECT\_ID : The project ID. If omitted, your default project is used.
      - DATASET : The name of a dataset in your project.
      - TABLE : The name of the table to create.
      - COLUMN : The name of the partitioning column.
      - UNIT\_TIME : The partitioning type. Supported values include `  DAY  ` , `  HOUR  ` , `  MONTH  ` , or `  YEAR  ` .
      - START : The start of range partitioning, inclusive.
      - END : The end of range partitioning, exclusive.
      - INTERVAL : The width of each range within the partition.
      - QUERY\_STATEMENT : The query used to populate the table.
    
    The following example creates a table that is partitioned on the `  transaction_date  ` column, using monthly partitioning.
    
    ``` text
    bq query \
       --use_legacy_sql=false \
       --destination_table mydataset.newtable \
       --time_partitioning_field transaction_date \
       --time_partitioning_type MONTH \
       'SELECT transaction_id, transaction_date FROM mydataset.mytable'
    ```
    
    The following example creates a table that is partitioned on the `  customer_id  ` column, using integer-range partitioning.
    
    ``` text
    bq query \
       --use_legacy_sql=false \
       --destination_table mydataset.newtable \
       --range_partitioning customer_id,0,100,10 \
       'SELECT * FROM mydataset.ponies'
    ```
    
    For ingestion-time partitioned tables, you can also load data into a specific partition by using a [partition decorator](/bigquery/docs/managing-partitioned-table-data#write-to-partition) . The following example creates a new ingestion-time partitioned table and loads data into the `  20180201  ` (February 1, 2018) partition:
    
    ``` text
    bq query \
       --use_legacy_sql=false  \
       --time_partitioning_type=DAY \
       --destination_table='newtable$20180201' \
       'SELECT * FROM mydataset.mytable'
    ```

### API

To save query results to a partitioned table, call the [`  jobs.insert  `](/bigquery/docs/reference/rest/v2/jobs/insert) method. Configure a `  query  ` job. Specify the destination table in the `  destinationTable  ` . Specify the partitioning in either the `  timePartitioning  ` property or the `  rangePartitioning  ` property.

## Convert date-sharded tables into ingestion-time partitioned tables

If you previously created date-sharded tables, you can convert the entire set of related tables into a single ingestion-time partitioned table by using the [`  partition  `](/bigquery/docs/reference/bq-cli-reference#bq_partition) command in the bq command-line tool.

``` text
bq --location=LOCATION partition \
    --time_partitioning_type=PARTITION_TYPE \
    --time_partitioning_expiration INTEGER \
    PROJECT_ID:SOURCE_DATASET.SOURCE_TABLE \
    PROJECT_ID:DESTINATION_DATASET.DESTINATION_TABLE
```

Replace the following:

  - LOCATION : The name of your location. The `  --location  ` flag is optional.
  - PARTITION\_TYPE : The partition type. Possible values include `  DAY  ` , `  HOUR  ` , `  MONTH  ` , or `  YEAR  ` .
  - INTEGER : The partition expiration time, in seconds. There is no minimum value. The expiration time evaluates to the partition's UTC date plus the integer value. The `  time_partitioning_expiration  ` flag is optional.
  - PROJECT\_ID : Your project ID.
  - SOURCE\_DATASET : The dataset that contains the date-sharded tables.
  - SOURCE\_TABLE : The prefix of your date-sharded tables.
  - DESTINATION\_DATASET ; The dataset for the new partitioned table.
  - DESTINATION\_TABLE ; The name of the partitioned table to create.

The `  partition  ` command does not support the `  --label  ` , `  --expiration  ` , `  --add_tags  ` , or `  --description  ` flags. You can add labels, a table expiration, [tags](/bigquery/docs/tags) , and a description to the table after it is created.

When you run the `  partition  ` command, BigQuery creates a copy job that generates partitions from the sharded tables.

The following example creates an ingestion-time partitioned table named `  mytable_partitioned  ` from a set of date-sharded tables prefixed with `  sourcetable_  ` . The new table is partitioned daily, with a partition expiration of 259,200 seconds (3 days).

``` text
bq partition \
    --time_partitioning_type=DAY \
    --time_partitioning_expiration 259200 \
    mydataset.sourcetable_ \
    mydataset.mytable_partitioned
```

If the date-sharded tables were `  sourcetable_20180126  ` and `  sourcetable_20180127  ` , this command would create the following partitions: `  mydataset.mytable_partitioned$20180126  ` and `  mydataset.mytable_partitioned$20180127  ` .

## Partitioned table security

Access control for partitioned tables is the same as access control for standard tables. For more information, see [Introduction to table access controls](/bigquery/docs/table-access-controls-intro) .

## What's next

  - To learn how to manage and update partitioned tables, see [Managing partitioned tables](/bigquery/docs/managing-partitioned-tables) .
  - For information on querying partitioned tables, see [Querying partitioned tables](/bigquery/docs/querying-partitioned-tables) .
