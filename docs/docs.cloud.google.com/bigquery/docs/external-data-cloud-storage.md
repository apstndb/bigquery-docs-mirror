# Create Cloud Storage external tables

**Important:** The term "BigLake" on this page refers to an access delegation functionality for external tables in BigQuery. For information about BigLake, the stand-alone Google Cloud product that includes BigLake metastore, the Apache Iceberg REST catalog, and BigLake tables for Apache Iceberg see [BigLake overview](/biglake/docs/introduction) .

BigQuery supports querying Cloud Storage data in the following formats:

  - Comma-separated values (CSV)
  - JSON (newline-delimited)
  - Avro
  - ORC
  - Parquet
  - Datastore exports
  - Firestore exports

BigQuery supports querying Cloud Storage data from these [storage classes](/storage/docs/storage-classes) :

  - Standard
  - Nearline
  - Coldline
  - Archive

To query a Cloud Storage external table, you must have permissions on both the external table and the Cloud Storage files. We recommend using a [BigLake table](/bigquery/docs/biglake-intro) instead if possible. BigLake tables provide access delegation, so that you only need permissions on the BigLake table in order to query the Cloud Storage data.

Be sure to [consider the location](/bigquery/docs/locations#data-locations) of your dataset and Cloud Storage bucket when you query data stored in Cloud Storage.

## Before you begin

Grant Identity and Access Management (IAM) roles that give users the necessary permissions to perform each task in this document. The permissions required to perform a task (if any) are listed in the "Required permissions" section of the task.

## Required roles

To create an external table, you need the `  bigquery.tables.create  ` BigQuery Identity and Access Management (IAM) permission.

Each of the following predefined Identity and Access Management roles includes this permission:

  - BigQuery Data Editor ( `  roles/bigquery.dataEditor  ` )
  - BigQuery Data Owner ( `  roles/bigquery.dataOwner  ` )
  - BigQuery Admin ( `  roles/bigquery.admin  ` )

You also need the following permissions to access the Cloud Storage bucket that contains your data:

  - `  storage.buckets.get  `
  - `  storage.objects.get  `
  - `  storage.objects.list  ` (required if you are using a URI [wildcard](#wildcard-support) )

The Cloud Storage Storage Admin ( `  roles/storage.admin  ` ) predefined Identity and Access Management role includes these permissions.

If you are not a principal in any of these roles, ask your administrator to grant you access or to create the external table for you.

For more information on Identity and Access Management roles and permissions in BigQuery, see [Predefined roles and permissions](/bigquery/docs/access-control) .

### Access scopes for Compute Engine instances

If, from a Compute Engine instance, you need to query an external table that is linked to a Cloud Storage source, the instance must have at least the Cloud Storage read-only [access scope](/compute/docs/access/service-accounts#accesscopesiam) ( `  https://www.googleapis.com/auth/devstorage.read_only  ` ).

The scopes control the Compute Engine instance's access to Google Cloud products, including Cloud Storage. Applications running on the instance use the service account attached to the instance to call Google Cloud APIs.

If you set up a Compute Engine instance to run as the [default Compute Engine service account](/compute/docs/access/service-accounts#default_service_account) , the instance is by default granted a number of [default scopes](/compute/docs/access/service-accounts#default_scopes) , including the `  https://www.googleapis.com/auth/devstorage.read_only  ` scope.

If instead you set up the instance with a custom service account, make sure to explicitly grant the `  https://www.googleapis.com/auth/devstorage.read_only  ` scope to the instance.

For information about applying scopes to a Compute Engine instance, see [Changing the service account and access scopes for an instance](/compute/docs/access/create-enable-service-accounts-for-instances#changeserviceaccountandscopes) . For more information about Compute Engine service accounts, see [Service accounts](/compute/docs/access/service-accounts) .

## Create external tables on unpartitioned data

You can create a permanent table linked to your external data source by:

  - Using the Google Cloud console
  - Using the [`  bq mk  `](/bigquery/docs/reference/bq-cli-reference#bq_mk) command
  - Creating an [`  ExternalDataConfiguration  `](/bigquery/docs/reference/rest/v2/tables#externaldataconfiguration) when you use the [`  tables.insert  `](/bigquery/docs/reference/rest/v2/tables/insert) API method
  - Running the [`  CREATE EXTERNAL TABLE  `](/bigquery/docs/reference/standard-sql/data-definition-language#create_external_table_statement) data definition language (DDL) statement.
  - Using the client libraries

Select one of the following options:

### Console

1.  Go to the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :
    
    If you don't see the left pane, click last\_page **Expand left pane** to open the pane.

3.  In the **Explorer** pane, expand your project, click **Datasets** , and then select a dataset.

4.  Expand the more\_vert **Actions** option and click **Create table** .

5.  In the **Source** section, specify the following details:
    
    1.  For **Create table from** , select **Google Cloud Storage**
    
    2.  For **Select file from GCS bucket or use a URI pattern** , browse to select a bucket and file to use, or type the path in the format `  gs://bucket_name/[folder_name/]file_name  ` .
        
        You can't specify multiple URIs in the Google Cloud console, but you can select multiple files by specifying one asterisk ( `  *  ` ) wildcard character. For example, `  gs://mybucket/file_name*  ` . For more information, see [Wildcard support for Cloud Storage URIs](/bigquery/docs/external-data-cloud-storage#wildcard-support) .
        
        The Cloud Storage bucket must be in the same location as the dataset that contains the table you're creating.
    
    3.  For **File format** , select the format that matches your file.

6.  In the **Destination** section, specify the following details:
    
    1.  For **Project** , choose the project in which to create the table.
    
    2.  For **Dataset** , choose the dataset in which to create the table.
    
    3.  For **Table** , enter the name of the table you are creating.
    
    4.  For **Table type** , select **External table** .

7.  In the **Schema** section, you can either enable [schema auto-detection](/bigquery/docs/schema-detect) or manually specify a schema if you have a source file. If you don't have a source file, you must manually specify a schema.
    
      - To enable schema auto-detection, select the **Auto-detect** option.
    
      - To manually specify a schema, leave the **Auto-detect** option unchecked. Enable **Edit as text** and enter the table schema as a [JSON array](/bigquery/docs/schemas#specifying_a_json_schema_file) .

8.  To ignore rows with extra column values that do not match the schema, expand the **Advanced options** section and select **Unknown values** .

9.  Click **Create table** .

After the permanent table is created, you can run a query against the table as if it were a native BigQuery table. After your query completes, you can [export the results](/bigquery/docs/writing-results) as CSV or JSON files, save the results as a table, or save the results to Google Sheets.

### SQL

You can create a permanent external table by running the [`  CREATE EXTERNAL TABLE  ` DDL statement](/bigquery/docs/reference/standard-sql/data-definition-language#create_external_table_statement) . You can specify the schema explicitly, or use [schema auto-detection](/bigquery/docs/schema-detect) to infer the schema from the external data.

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
    CREATE EXTERNAL TABLE `PROJECT_ID.DATASET.EXTERNAL_TABLE_NAME`
      OPTIONS (
        format ="TABLE_FORMAT",
        uris = ['BUCKET_PATH'[,...]]
        );
    ```
    
    Replace the following:
    
      - `  PROJECT_ID  ` : the name of your project in which you want to create the table—for example, `  myproject  `
    
      - `  DATASET  ` : the name of the BigQuery dataset that you want to create the table in—for example, `  mydataset  `
    
      - `  EXTERNAL_TABLE_NAME  ` : the name of the table that you want to create—for example, `  mytable  `
    
      - `  TABLE_FORMAT  ` : the format of the table that you want to create—for example, `  PARQUET  `
    
      - `  BUCKET_PATH  ` : the path to the Cloud Storage bucket that contains the data for the external table, in the format `  ['gs://bucket_name/[folder_name/]file_name']  ` .
        
        You can select multiple files from the bucket by specifying one asterisk ( `  *  ` ) wildcard character in the path. For example, `  ['gs://mybucket/file_name*']  ` . For more information, see [Wildcard support for Cloud Storage URIs](/bigquery/docs/external-data-cloud-storage#wildcard-support) .
        
        You can specify multiple buckets for the `  uris  ` option by providing multiple paths.
        
        The following examples show valid `  uris  ` values:
        
          - `  ['gs://bucket/path1/myfile.csv']  `
          - `  ['gs://bucket/path1/*.csv']  `
          - `  ['gs://bucket/path1/*', 'gs://bucket/path2/file00*']  `
        
        When you specify `  uris  ` values that target multiple files, all of those files must share a compatible schema.
        
        For more information about using Cloud Storage URIs in BigQuery, see [Cloud Storage resource path](/bigquery/docs/external-data-cloud-storage#google-cloud-storage-uri) .

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](/bigquery/docs/running-queries#queries) .

**Examples**

The following example uses schema auto-detection to create an external table named `  sales  ` that is linked to a CSV file stored in Cloud Storage:

``` text
CREATE OR REPLACE EXTERNAL TABLE mydataset.sales
  OPTIONS (
  format = 'CSV',
  uris = ['gs://mybucket/sales.csv']);
```

The next example specifies a schema explicitly and skips the first row in the CSV file:

``` text
CREATE OR REPLACE EXTERNAL TABLE mydataset.sales (
  Region STRING,
  Quarter STRING,
  Total_Sales INT64
) OPTIONS (
    format = 'CSV',
    uris = ['gs://mybucket/sales.csv'],
    skip_leading_rows = 1);
```

### bq

To create an external table, use the [`  bq mk  ` command](/bigquery/docs/reference/bq-cli-reference#bq_mk) with the [`  --external_table_definition  `](/bigquery/docs/reference/bq-cli-reference#external_table_definition_flag) flag. This flag contains either a path to a [table definition file](/bigquery/docs/external-table-definition) or an inline table definition.

**Option 1: Table definition file**

Use the [`  bq mkdef  `](/bigquery/docs/reference/bq-cli-reference#bq_mkdef) command to create a table definition file, and then pass the file path to the `  bq mk  ` command as follows:

``` text
bq mkdef --source_format=SOURCE_FORMAT \
  BUCKET_PATH > DEFINITION_FILE

bq mk --table \
  --external_table_definition=DEFINITION_FILE \
  DATASET_NAME.TABLE_NAME \
  SCHEMA
```

Replace the following:

  - `  SOURCE_FORMAT  ` : the format of the external data source. For example, `  CSV  ` .

  - `  BUCKET_PATH  ` : the path to the Cloud Storage bucket that contains the data for the table, in the format `  gs://bucket_name/[folder_name/]file_pattern  ` .
    
    You can select multiple files from the bucket by specifying one asterisk ( `  *  ` ) wildcard character in the `  file_pattern  ` . For example, `  gs://mybucket/file00*.parquet  ` . For more information, see [Wildcard support for Cloud Storage URIs](/bigquery/docs/external-data-cloud-storage#wildcard-support) .
    
    You can specify multiple buckets for the `  uris  ` option by providing multiple paths.
    
    The following examples show valid `  uris  ` values:
    
      - `  gs://bucket/path1/myfile.csv  `
      - `  gs://bucket/path1/*.parquet  `
      - `  gs://bucket/path1/file1*  ` , `  gs://bucket1/path1/*  `
    
    When you specify `  uris  ` values that target multiple files, all of those files must share a compatible schema.
    
    For more information about using Cloud Storage URIs in BigQuery, see [Cloud Storage resource path](/bigquery/docs/external-data-cloud-storage#google-cloud-storage-uri) .

  - `  DEFINITION_FILE  ` : the path to the [table definition file](/bigquery/docs/external-table-definition) on your local machine.

  - `  DATASET_NAME  ` : the name of the dataset that contains the table.

  - `  TABLE_NAME  ` : the name of the table you're creating.

  - `  SCHEMA  ` : specifies a path to a [JSON schema file](/bigquery/docs/schemas#specifying_a_json_schema_file) , or specifies the schema in the form `  field:data_type,field:data_type,...  ` .

Example:

``` text
bq mkdef --source_format=CSV gs://mybucket/sales.csv > mytable_def

bq mk --table --external_table_definition=mytable_def \
  mydataset.mytable \
  Region:STRING,Quarter:STRING,Total_sales:INTEGER
```

To use schema auto-detection, set the `  --autodetect=true  ` flag in the `  mkdef  ` command and omit the schema:

``` text
bq mkdef --source_format=CSV --autodetect=true \
  gs://mybucket/sales.csv > mytable_def

bq mk --table --external_table_definition=mytable_def \
  mydataset.mytable
```

**Option 2: Inline table definition**

Instead of creating a table definition file, you can pass the table definition directly to the `  bq mk  ` command:

``` text
bq mk --table \
  --external_table_definition=@SOURCE_FORMAT=BUCKET_PATH \
  DATASET_NAME.TABLE_NAME \
  SCHEMA
```

Replace the following:

  - `  SOURCE_FORMAT  ` : the format of the external data source
    
    For example, `  CSV  ` .

  - `  BUCKET_PATH  ` : the path to the Cloud Storage bucket that contains the data for the table, in the format `  gs://bucket_name/[folder_name/]file_pattern  ` .
    
    You can select multiple files from the bucket by specifying one asterisk ( `  *  ` ) wildcard character in the `  file_pattern  ` . For example, `  gs://mybucket/file00*.parquet  ` . For more information, see [Wildcard support for Cloud Storage URIs](/bigquery/docs/external-data-cloud-storage#wildcard-support) .
    
    You can specify multiple buckets for the `  uris  ` option by providing multiple paths.
    
    The following examples show valid `  uris  ` values:
    
      - `  gs://bucket/path1/myfile.csv  `
      - `  gs://bucket/path1/*.parquet  `
      - `  gs://bucket/path1/file1*  ` , `  gs://bucket1/path1/*  `
    
    When you specify `  uris  ` values that target multiple files, all of those files must share a compatible schema.
    
    For more information about using Cloud Storage URIs in BigQuery, see [Cloud Storage resource path](/bigquery/docs/external-data-cloud-storage#google-cloud-storage-uri) .

  - `  DATASET_NAME  ` : the name of the dataset that contains the table.

  - `  TABLE_NAME  ` : the name of the table you're creating.

  - `  SCHEMA  ` : specifies a path to a [JSON schema file](/bigquery/docs/schemas#specifying_a_json_schema_file) , or specifies the schema in the form `  field:data_type,field:data_type,...  ` . To use schema auto-detection, omit this argument.

Example:

``` text
bq mkdef --source_format=CSV gs://mybucket/sales.csv > mytable_def
bq mk --table --external_table_definition=mytable_def \
  mydataset.mytable \
  Region:STRING,Quarter:STRING,Total_sales:INTEGER
```

### API

Call the [`  tables.insert  ` method](/bigquery/docs/reference/rest/v2/tables/insert) API method, and create an [`  ExternalDataConfiguration  `](/bigquery/docs/reference/rest/v2/tables#externaldataconfiguration) in the [`  Table  ` resource](/bigquery/docs/reference/rest/v2/tables#Table) that you pass in.

Specify the `  schema  ` property or set the `  autodetect  ` property to `  true  ` to enable schema auto detection for supported data sources.

### Java

Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Java API reference documentation](/java/docs/reference/google-cloud-bigquery/latest/overview) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` java
import com.google.cloud.bigquery.BigQuery;
import com.google.cloud.bigquery.BigQueryException;
import com.google.cloud.bigquery.BigQueryOptions;
import com.google.cloud.bigquery.CsvOptions;
import com.google.cloud.bigquery.ExternalTableDefinition;
import com.google.cloud.bigquery.Field;
import com.google.cloud.bigquery.QueryJobConfiguration;
import com.google.cloud.bigquery.Schema;
import com.google.cloud.bigquery.StandardSQLTypeName;
import com.google.cloud.bigquery.TableId;
import com.google.cloud.bigquery.TableInfo;
import com.google.cloud.bigquery.TableResult;

// Sample to queries an external data source using a permanent table
public class QueryExternalGCSPerm {

  public static void runQueryExternalGCSPerm() {
    // TODO(developer): Replace these variables before running the sample.
    String datasetName = "MY_DATASET_NAME";
    String tableName = "MY_TABLE_NAME";
    String sourceUri = "gs://cloud-samples-data/bigquery/us-states/us-states.csv";
    Schema schema =
        Schema.of(
            Field.of("name", StandardSQLTypeName.STRING),
            Field.of("post_abbr", StandardSQLTypeName.STRING));
    String query =
        String.format("SELECT * FROM %s.%s WHERE name LIKE 'W%%'", datasetName, tableName);
    queryExternalGCSPerm(datasetName, tableName, sourceUri, schema, query);
  }

  public static void queryExternalGCSPerm(
      String datasetName, String tableName, String sourceUri, Schema schema, String query) {
    try {
      // Initialize client that will be used to send requests. This client only needs to be created
      // once, and can be reused for multiple requests.
      BigQuery bigquery = BigQueryOptions.getDefaultInstance().getService();

      // Skip header row in the file.
      CsvOptions csvOptions = CsvOptions.newBuilder().setSkipLeadingRows(1).build();

      TableId tableId = TableId.of(datasetName, tableName);
      // Create a permanent table linked to the GCS file
      ExternalTableDefinition externalTable =
          ExternalTableDefinition.newBuilder(sourceUri, csvOptions).setSchema(schema).build();
      bigquery.create(TableInfo.of(tableId, externalTable));

      // Example query to find states starting with 'W'
      TableResult results = bigquery.query(QueryJobConfiguration.of(query));

      results
          .iterateAll()
          .forEach(row -> row.forEach(val -> System.out.printf("%s,", val.toString())));

      System.out.println("Query on external permanent table performed successfully.");
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
// Import the Google Cloud client library and create a client
const {BigQuery} = require('@google-cloud/bigquery');
const bigquery = new BigQuery();

async function queryExternalGCSPerm() {
  // Queries an external data source using a permanent table

  /**
   * TODO(developer): Uncomment the following lines before running the sample.
   */
  // const datasetId = "my_dataset";
  // const tableId = "my_table";

  // Configure the external data source
  const dataConfig = {
    sourceFormat: 'CSV',
    sourceUris: ['gs://cloud-samples-data/bigquery/us-states/us-states.csv'],
    // Optionally skip header row
    csvOptions: {skipLeadingRows: 1},
  };

  // For all options, see https://cloud.google.com/bigquery/docs/reference/v2/tables#resource
  const options = {
    schema: schema,
    externalDataConfiguration: dataConfig,
  };

  // Create an external table linked to the GCS file
  const [table] = await bigquery
    .dataset(datasetId)
    .createTable(tableId, options);

  console.log(`Table ${table.id} created.`);

  // Example query to find states starting with 'W'
  const query = `SELECT post_abbr
  FROM \`${datasetId}.${tableId}\`
  WHERE name LIKE 'W%'`;

  // Run the query as a job
  const [job] = await bigquery.createQueryJob(query);
  console.log(`Job ${job.id} started.`);

  // Wait for the query to finish
  const [rows] = await job.getQueryResults();

  // Print the results
  console.log('Rows:');
  console.log(rows);
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
table_id = "your-project.your_dataset.your_table_name"

# TODO(developer): Set the external source format of your table.
# Note that the set of allowed values for external data sources is
# different than the set used for loading data (see :class:`~google.cloud.bigquery.job.SourceFormat`).
external_source_format = "AVRO"

# TODO(developer): Set the source_uris to point to your data in Google Cloud
source_uris = [
    "gs://cloud-samples-data/bigquery/federated-formats-reference-file-schema/a-twitter.avro",
    "gs://cloud-samples-data/bigquery/federated-formats-reference-file-schema/b-twitter.avro",
    "gs://cloud-samples-data/bigquery/federated-formats-reference-file-schema/c-twitter.avro",
]

# Create ExternalConfig object with external source format
external_config = bigquery.ExternalConfig(external_source_format)
# Set source_uris that point to your data in Google Cloud
external_config.source_uris = source_uris

# TODO(developer) You have the option to set a reference_file_schema_uri, which points to
# a reference file for the table schema
reference_file_schema_uri = "gs://cloud-samples-data/bigquery/federated-formats-reference-file-schema/b-twitter.avro"

external_config.reference_file_schema_uri = reference_file_schema_uri

table = bigquery.Table(table_id)
# Set the external data configuration of the table
table.external_data_configuration = external_config
table = client.create_table(table)  # Make an API request.

print(
    f"Created table with external source format {table.external_data_configuration.source_format}"
)
```

## Create external tables on partitioned data

You can create an external table for Hive partitioned data that resides in Cloud Storage. After you create an externally partitioned table, you can't change the partition key. You need to recreate the table to change the partition key.

To create an external table for Hive partitioned data, choose one of the following options:

### Console

In the Google Cloud console, go to **BigQuery** .

In the left pane, click explore **Explorer** .

In the **Explorer** pane, expand your project, click **Datasets** , and then select a dataset.

Click more\_vert **Actions** , and then click **Create table** . This opens the **Create table** pane.

In the **Source** section, specify the following details:

1.  For **Create table from** , select **Google Cloud Storage** .
2.  For **Select file from Cloud Storage bucket** , enter the path to the Cloud Storage folder, using [wildcards](/bigquery/docs/batch-loading-data#load-wildcards) . For example, `  my_bucket/my_files*  ` . The Cloud Storage bucket must be in the same location as the dataset that contains the table you want to create, append, or overwrite.
3.  From the **File format** list, select the file type.
4.  Select the **Source data partitioning** checkbox, and then for **Select Source URI Prefix** , enter the Cloud Storage URI prefix. For example, `  gs://my_bucket/my_files  ` .
5.  In the **Partition inference mode** section, select one of the following options:
      - **Automatically infer types** : set the partition schema detection mode to `  AUTO  ` .
      - **All columns are strings** : set the partition schema detection mode to `  STRINGS  ` .
      - **Provide my own** : set the partition schema detection mode to `  CUSTOM  ` and manually enter the schema information for the partition keys. For more information, see [Provide a custom partition key schema](/bigquery/docs/hive-partitioned-loads-gcs#custom_partition_key_schema) .
6.  Optional: To require a partition filter on all queries for this table, select the **Require partition filter** checkbox. Requiring a partition filter can reduce cost and improve performance. For more information, see [Requiring predicate filters on partition keys in queries](/bigquery/docs/hive-partitioned-queries-gcs#requiring_predicate_filters_on_partition_keys_in_queries) .

In the **Destination** section, specify the following details:

1.  For **Project** , select the project in which you want to create the table.
2.  For **Dataset** , select the dataset in which you want to create the table.
3.  For **Table** , enter the name of the table that you want to create.
4.  For **Table type** , select **External table** .

In the **Schema** section, enter the [schema](/bigquery/docs/schemas) definition.

To enable the [auto detection](/bigquery/docs/schema-detect) of schema, select **Auto detect** .

To ignore rows with extra column values that do not match the schema, expand the **Advanced options** section and select **Unknown values** .

Click **Create table** .

### SQL

Use the [`  CREATE EXTERNAL TABLE  ` DDL statement](/bigquery/docs/reference/standard-sql/data-definition-language#create_external_table_statement) .

The following example uses automatic detection of Hive partition keys:

``` text
CREATE EXTERNAL TABLE `PROJECT_ID.DATASET.EXTERNAL_TABLE_NAME`
WITH PARTITION COLUMNS
OPTIONS (
format = 'SOURCE_FORMAT',
uris = ['GCS_URIS'],
hive_partition_uri_prefix = 'GCS_URI_SHARED_PREFIX',
require_hive_partition_filter = BOOLEAN);
```

Replace the following:

  - `  SOURCE_FORMAT  ` : the format of the external data source, such as `  PARQUET  `
  - `  GCS_URIS  ` : the path to the Cloud Storage folder, using wildcard format
  - `  GCS_URI_SHARED_PREFIX  ` : the source URI prefix without the wildcard
  - `  BOOLEAN  ` : whether to require a predicate filter at query time. This flag is optional. The default value is `  false  ` .

The following example uses custom Hive partition keys and types by listing them in the `  WITH PARTITION COLUMNS  ` clause:

``` text
CREATE EXTERNAL TABLE `PROJECT_ID.DATASET.EXTERNAL_TABLE_NAME`
WITH PARTITION COLUMNS (PARTITION_COLUMN_LIST)
OPTIONS (
format = 'SOURCE_FORMAT',
uris = ['GCS_URIS'],
hive_partition_uri_prefix = 'GCS_URI_SHARED_PREFIX',
require_hive_partition_filter = BOOLEAN);
```

Replace the following:

  - `  PARTITION_COLUMN_LIST  ` : a list of columns following the same order in the path of Cloud Storage folder, in the format of:

<!-- end list -->

``` text
KEY1 TYPE1, KEY2 TYPE2
```

The following example creates an externally partitioned table. It uses schema auto-detection to detect both the file schema and the hive partitioning layout. If the external path is `  gs://bucket/path/field_1=first/field_2=1/data.parquet  ` , the partition columns are detected as `  field_1  ` ( `  STRING  ` ) and `  field_2  ` ( `  INT64  ` ).

``` text
CREATE EXTERNAL TABLE dataset.AutoHivePartitionedTable
WITH PARTITION COLUMNS
OPTIONS (
uris = ['gs://bucket/path/*'],
format = 'PARQUET',
hive_partition_uri_prefix = 'gs://bucket/path',
require_hive_partition_filter = false);
```

The following example creates an externally partitioned table by explicitly specifying the partition columns. This example assumes that the external file path has the pattern `  gs://bucket/path/field_1=first/field_2=1/data.parquet  ` .

``` text
CREATE EXTERNAL TABLE dataset.CustomHivePartitionedTable
WITH PARTITION COLUMNS (
field_1 STRING, -- column order must match the external path
field_2 INT64)
OPTIONS (
uris = ['gs://bucket/path/*'],
format = 'PARQUET',
hive_partition_uri_prefix = 'gs://bucket/path',
require_hive_partition_filter = false);
```

### bq

First, use the [`  bq mkdef  `](/bigquery/docs/reference/bq-cli-reference#bq_mkdef) command to create a table definition file:

``` text
bq mkdef \
--source_format=SOURCE_FORMAT \
--hive_partitioning_mode=PARTITIONING_MODE \
--hive_partitioning_source_uri_prefix=GCS_URI_SHARED_PREFIX \
--require_hive_partition_filter=BOOLEAN \
 GCS_URIS > DEFINITION_FILE
```

Replace the following:

  - `  SOURCE_FORMAT  ` : the format of the external data source. For example, `  CSV  ` .
  - `  PARTITIONING_MODE  ` : the Hive partitioning mode. Use one of the following values:
      - `  AUTO  ` : Automatically detect the key names and types.
      - `  STRINGS  ` : Automatically convert the key names to strings.
      - `  CUSTOM  ` : Encode the key schema in the source URI prefix.
  - `  GCS_URI_SHARED_PREFIX  ` : the source URI prefix.
  - `  BOOLEAN  ` : specifies whether to require a predicate filter at query time. This flag is optional. The default value is `  false  ` .
  - `  GCS_URIS  ` : the path to the Cloud Storage folder, using wildcard format.
  - `  DEFINITION_FILE  ` : the path to the [table definition file](/bigquery/external-table-definition) on your local machine.

If `  PARTITIONING_MODE  ` is `  CUSTOM  ` , include the partition key schema in the source URI prefix, using the following format:

``` text
--hive_partitioning_source_uri_prefix=GCS_URI_SHARED_PREFIX/{KEY1:TYPE1}/{KEY2:TYPE2}/...
```

After you create the table definition file, use the [`  bq mk  `](/bigquery/docs/reference/bq-cli-reference#mk-table) command to create the external table:

``` text
bq mk --external_table_definition=DEFINITION_FILE \
DATASET_NAME.TABLE_NAME \
SCHEMA
```

Replace the following:

  - `  DEFINITION_FILE  ` : the path to the table definition file.
  - `  DATASET_NAME  ` : the name of the dataset that contains the table.
  - `  TABLE_NAME  ` : the name of the table you're creating.
  - `  SCHEMA  ` : specifies a path to a [JSON schema file](/bigquery/docs/schemas#specifying_a_json_schema_file) , or specifies the schema in the form `  field:data_type,field:data_type,...  ` . To use schema auto-detection, omit this argument.

**Examples**

The following example uses `  AUTO  ` Hive partitioning mode:

``` text
bq mkdef --source_format=CSV \
  --hive_partitioning_mode=AUTO \
  --hive_partitioning_source_uri_prefix=gs://myBucket/myTable \
  gs://myBucket/myTable/* > mytable_def

bq mk --external_table_definition=mytable_def \
  mydataset.mytable \
  Region:STRING,Quarter:STRING,Total_sales:INTEGER
```

The following example uses `  STRING  ` Hive partitioning mode:

``` text
bq mkdef --source_format=CSV \
  --hive_partitioning_mode=STRING \
  --hive_partitioning_source_uri_prefix=gs://myBucket/myTable \
  gs://myBucket/myTable/* > mytable_def

bq mk --external_table_definition=mytable_def \
  mydataset.mytable \
  Region:STRING,Quarter:STRING,Total_sales:INTEGER
```

The following example uses `  CUSTOM  ` Hive partitioning mode:

``` text
bq mkdef --source_format=CSV \
  --hive_partitioning_mode=CUSTOM \
  --hive_partitioning_source_uri_prefix=gs://myBucket/myTable/{dt:DATE}/{val:STRING} \
  gs://myBucket/myTable/* > mytable_def

bq mk --external_table_definition=mytable_def \
  mydataset.mytable \
  Region:STRING,Quarter:STRING,Total_sales:INTEGER
```

### API

To set Hive partitioning using the BigQuery API, include a [hivePartitioningOptions](/bigquery/docs/reference/rest/v2/tables#hivepartitioningoptions) object in the [ExternalDataConfiguration](/bigquery/docs/reference/rest/v2/tables#externaldataconfiguration) object when you create the [table definition file](/bigquery/external-table-definition) .

If you set the `  hivePartitioningOptions.mode  ` field to `  CUSTOM  ` , you must encode the partition key schema in the `  hivePartitioningOptions.sourceUriPrefix  ` field as follows: `  gs:// BUCKET / PATH_TO_TABLE /{ KEY1 : TYPE1 }/{ KEY2 : TYPE2 }/...  `

To enforce the use of a predicate filter at query time, set the `  hivePartitioningOptions.requirePartitionFilter  ` field to `  true  ` .

### Java

Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Java API reference documentation](/java/docs/reference/google-cloud-bigquery/latest/overview) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` java
import com.google.cloud.bigquery.BigQuery;
import com.google.cloud.bigquery.BigQueryException;
import com.google.cloud.bigquery.BigQueryOptions;
import com.google.cloud.bigquery.ExternalTableDefinition;
import com.google.cloud.bigquery.FormatOptions;
import com.google.cloud.bigquery.HivePartitioningOptions;
import com.google.cloud.bigquery.TableId;
import com.google.cloud.bigquery.TableInfo;

// Sample to create external table using hive partitioning
public class SetHivePartitioningOptions {

  public static void main(String[] args) {
    // TODO(developer): Replace these variables before running the sample.
    String datasetName = "MY_DATASET_NAME";
    String tableName = "MY_TABLE_NAME";
    String sourceUri = "gs://cloud-samples-data/bigquery/hive-partitioning-samples/customlayout/*";
    String sourceUriPrefix =
        "gs://cloud-samples-data/bigquery/hive-partitioning-samples/customlayout/{pkey:STRING}/";
    setHivePartitioningOptions(datasetName, tableName, sourceUriPrefix, sourceUri);
  }

  public static void setHivePartitioningOptions(
      String datasetName, String tableName, String sourceUriPrefix, String sourceUri) {
    try {
      // Initialize client that will be used to send requests. This client only needs to be created
      // once, and can be reused for multiple requests.
      BigQuery bigquery = BigQueryOptions.getDefaultInstance().getService();

      // Configuring partitioning options
      HivePartitioningOptions hivePartitioningOptions =
          HivePartitioningOptions.newBuilder()
              .setMode("CUSTOM")
              .setRequirePartitionFilter(true)
              .setSourceUriPrefix(sourceUriPrefix)
              .build();

      TableId tableId = TableId.of(datasetName, tableName);
      ExternalTableDefinition customTable =
          ExternalTableDefinition.newBuilder(sourceUri, FormatOptions.parquet())
              .setAutodetect(true)
              .setHivePartitioningOptions(hivePartitioningOptions)
              .build();
      bigquery.create(TableInfo.of(tableId, customTable));
      System.out.println("External table created using hivepartitioningoptions");
    } catch (BigQueryException e) {
      System.out.println("External table was not created" + e.toString());
    }
  }
}
```

## Query external tables

For more information, see [Query Cloud Storage data in external tables](/bigquery/docs/query-cloud-storage-data) .

## Upgrade external tables to BigLake

You can upgrade tables based on Cloud Storage to BigLake tables by associating the external table to a connection. If you want to use [metadata caching](/bigquery/docs/biglake-intro#metadata_caching_for_performance) with the BigLake table, you can specify settings for this at the same time. To get table details such as source format and source URI, see [Get table information](/bigquery/docs/tables#get_table_information) .

To update an external table to a BigLake table, select one of the following options:

### SQL

Use the [`  CREATE OR REPLACE EXTERNAL TABLE  ` DDL statement](/bigquery/docs/reference/standard-sql/data-definition-language#create_external_table_statement) to update a table:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
    CREATE OR REPLACE EXTERNAL TABLE
      `PROJECT_ID.DATASET.EXTERNAL_TABLE_NAME`
      WITH CONNECTION {`REGION.CONNECTION_ID` | DEFAULT}
      OPTIONS(
        format ="TABLE_FORMAT",
        uris = ['BUCKET_PATH'],
        max_staleness = STALENESS_INTERVAL,
        metadata_cache_mode = 'CACHE_MODE'
        );
    ```
    
    Replace the following:
    
      - `  PROJECT_ID  ` : the name of the project that contains the table
    
      - `  DATASET  ` : the name of the dataset that contains the table
    
      - `  EXTERNAL_TABLE_NAME  ` : the name of the table
    
      - `  REGION  ` : the region that contains the connection
    
      - `  CONNECTION_ID  ` : the name of the connection to use
        
        To use a [default connection](/bigquery/docs/default-connections) , specify `  DEFAULT  ` instead of the connection string containing `  REGION . CONNECTION_ID  ` .
    
      - `  TABLE_FORMAT  ` : the format used by the table
        
        You can't change this when updating the table.
    
      - `  BUCKET_PATH  ` : the path to the Cloud Storage bucket that contains the data for the external table, in the format `  ['gs://bucket_name/[folder_name/]file_name']  ` .
        
        You can select multiple files from the bucket by specifying one asterisk ( `  *  ` ) wildcard character in the path. For example, `  ['gs://mybucket/file_name*']  ` . For more information, see [Wildcard support for Cloud Storage URIs](/bigquery/docs/external-data-cloud-storage#wildcard-support) .
        
        You can specify multiple buckets for the `  uris  ` option by providing multiple paths.
        
        The following examples show valid `  uris  ` values:
        
          - `  ['gs://bucket/path1/myfile.csv']  `
          - `  ['gs://bucket/path1/*.csv']  `
          - `  ['gs://bucket/path1/*', 'gs://bucket/path2/file00*']  `
        
        When you specify `  uris  ` values that target multiple files, all of those files must share a compatible schema.
        
        For more information about using Cloud Storage URIs in BigQuery, see [Cloud Storage resource path](/bigquery/docs/external-data-cloud-storage#google-cloud-storage-uri) .
    
      - `  STALENESS_INTERVAL  ` : specifies whether cached metadata is used by operations against the table, and how fresh the cached metadata must be in order for the operation to use it
        
        For more information about metadata caching considerations, see [Metadata caching for performance](/bigquery/docs/biglake-intro#metadata_caching_for_performance) .
        
        To disable metadata caching, specify 0. This is the default.
        
        To enable metadata caching, specify an [interval literal](/bigquery/docs/reference/standard-sql/lexical#interval_literals) value between 30 minutes and 7 days. For example, specify `  INTERVAL 4 HOUR  ` for a 4 hour staleness interval. With this value, operations against the table use cached metadata if it has been refreshed within the past 4 hours. If the cached metadata is older than that, the operation retrieves metadata from Cloud Storage instead.
    
      - `  CACHE_MODE  ` : specifies whether the metadata cache is refreshed automatically or manually
        
        For more information on metadata caching considerations, see [Metadata caching for performance](/bigquery/docs/biglake-intro#metadata_caching_for_performance) .
        
        Set to `  AUTOMATIC  ` for the metadata cache to be refreshed at a system-defined interval, usually somewhere between 30 and 60 minutes.
        
        Set to `  MANUAL  ` if you want to refresh the metadata cache on a schedule you determine. In this case, you can call the [`  BQ.REFRESH_EXTERNAL_METADATA_CACHE  ` system procedure](/bigquery/docs/reference/system-procedures#bqrefresh_external_metadata_cache) to refresh the cache.
        
        You must set `  CACHE_MODE  ` if `  STALENESS_INTERVAL  ` is set to a value greater than 0.

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](/bigquery/docs/running-queries#queries) .

### bq

Use the [`  bq mkdef  `](/bigquery/docs/reference/bq-cli-reference#bq_mkdef) and [`  bq update  `](/bigquery/docs/reference/bq-cli-reference#bq_update) commands to update a table:

1.  Generate an [external table definition](/bigquery/external-table-definition#table-definition) , that describes the aspects of the table to change:
    
    ``` text
    bq mkdef --connection_id=PROJECT_ID.REGION.CONNECTION_ID \
    --source_format=TABLE_FORMAT \
    --metadata_cache_mode=CACHE_MODE \
    "BUCKET_PATH" > /tmp/DEFINITION_FILE
    ```
    
    Replace the following:
    
      - `  PROJECT_ID  ` : the name of the project that contains the connection
    
      - `  REGION  ` : the region that contains the connection
    
      - `  CONNECTION_ID  ` : the name of the connection to use
    
      - `  TABLE_FORMAT  ` : the format used by the table. You can't change this when updating the table.
    
      - `  CACHE_MODE  ` : specifies whether the metadata cache is refreshed automatically or manually. For more information on metadata caching considerations, see [Metadata caching for performance](/bigquery/docs/biglake-intro#metadata_caching_for_performance) .
        
        Set to `  AUTOMATIC  ` for the metadata cache to be refreshed at a system-defined interval, usually somewhere between 30 and 60 minutes.
        
        Set to `  MANUAL  ` if you want to refresh the metadata cache on a schedule you determine. In this case, you can call the [`  BQ.REFRESH_EXTERNAL_METADATA_CACHE  ` system procedure](/bigquery/docs/reference/system-procedures#bqrefresh_external_metadata_cache) to refresh the cache.
        
        You must set `  CACHE_MODE  ` if `  STALENESS_INTERVAL  ` is set to a value greater than 0.
    
      - `  BUCKET_PATH  ` : the path to the Cloud Storage bucket that contains the data for the external table, in the format `  gs://bucket_name/[folder_name/]file_name  ` .
        
        You can limit the files selected from the bucket by specifying one asterisk ( `  *  ` ) wildcard character in the path. For example, `  gs://mybucket/file_name*  ` . For more information, see [Wildcard support for Cloud Storage URIs](/bigquery/docs/external-data-cloud-storage#wildcard-support) .
        
        You can specify multiple buckets for the `  uris  ` option by providing multiple paths.
        
        The following examples show valid `  uris  ` values:
        
          - `  gs://bucket/path1/myfile.csv  `
          - `  gs://bucket/path1/*.csv  `
          - `  gs://bucket/path1/*,gs://bucket/path2/file00*  `
        
        When you specify `  uris  ` values that target multiple files, all of those files must share a compatible schema.
        
        For more information about using Cloud Storage URIs in BigQuery, see [Cloud Storage resource path](/bigquery/docs/external-data-cloud-storage#google-cloud-storage-uri) .
    
      - `  DEFINITION_FILE  ` : the name of the table definition file that you are creating.

2.  Update the table using the new external table definition:
    
    ``` text
    bq update --max_staleness=STALENESS_INTERVAL \
    --external_table_definition=/tmp/DEFINITION_FILE \
    PROJECT_ID:DATASET.EXTERNAL_TABLE_NAME
    ```
    
    Replace the following:
    
      - `  STALENESS_INTERVAL  ` : specifies whether cached metadata is used by operations against the table, and how fresh the cached metadata must be in order for the operation to use it. For more information about metadata caching considerations, see [Metadata caching for performance](/bigquery/docs/biglake-intro#metadata_caching_for_performance) .
        
        To disable metadata caching, specify 0. This is the default.
        
        To enable metadata caching, specify an interval value between 30 minutes and 7 days, using the `  Y-M D H:M:S  ` format described in the [`  INTERVAL  ` data type](/bigquery/docs/reference/standard-sql/data-types#interval_type) documentation. For example, specify `  0-0 0 4:0:0  ` for a 4 hour staleness interval. With this value, operations against the table use cached metadata if it has been refreshed within the past 4 hours. If the cached metadata is older than that, the operation retrieves metadata from Cloud Storage instead.
    
      - `  DEFINITION_FILE  ` : the name of the table definition file that you created or updated.
    
      - `  PROJECT_ID  ` : the name of the project that contains the table
    
      - `  DATASET  ` : the name of the dataset that contains the table
    
      - `  EXTERNAL_TABLE_NAME  ` : the name of the table

## Cloud Storage resource path

When you create an external table based on a Cloud Storage data source, you must provide the path to the data.

The Cloud Storage resource path contains your bucket name and your object (filename). For example, if the Cloud Storage bucket is named `  mybucket  ` and the data file is named `  myfile.csv  ` , the resource path would be `  gs://mybucket/myfile.csv  ` .

BigQuery does not support Cloud Storage resource paths that include multiple consecutive slashes after the initial double slash. Cloud Storage object names can contain multiple consecutive slash ("/") characters. However, BigQuery converts multiple consecutive slashes into a single slash. For example, the following resource path, though valid in Cloud Storage, does not work in BigQuery: `  gs:// bucket /my//object//name  ` .

To retrieve the Cloud Storage resource path:

1.  Open the Cloud Storage console.

2.  Browse to the location of the object (file) that contains the source data.

3.  Click on the name of the object.
    
    The **Object details** page opens.

4.  Copy the value provided in the **gsutil URI** field, which begins with `  gs://  ` .

**Note:** You can also use the [`  gcloud storage ls  `](/sdk/gcloud/reference/storage/ls) command to list buckets or objects.

### Wildcard support for Cloud Storage URIs

If your data is separated into multiple files, you can use an asterisk (\*) wildcard to select multiple files. Use of the asterisk wildcard must follow these rules:

  - The asterisk can appear inside the object name or at the end of the object name.
  - Using multiple asterisks is unsupported. For example, the path `  gs://mybucket/fed-*/temp/*.csv  ` is invalid.
  - Using an asterisk with the bucket name is unsupported.

Examples:

  - The following example shows how to select all of the files in all the folders which start with the prefix `  gs://mybucket/fed-samples/fed-sample  ` :
    
    ``` text
    gs://mybucket/fed-samples/fed-sample*
    ```

  - The following example shows how to select only files with a `  .csv  ` extension in the folder named `  fed-samples  ` and any subfolders of `  fed-samples  ` :
    
    ``` text
    gs://mybucket/fed-samples/*.csv
    ```

  - The following example shows how to select files with a naming pattern of `  fed-sample*.csv  ` in the folder named `  fed-samples  ` . This example doesn't select files in subfolders of `  fed-samples  ` .
    
    ``` text
    gs://mybucket/fed-samples/fed-sample*.csv
    ```

When using the bq command-line tool, you might need to escape the asterisk on some platforms.

You can't use an asterisk wildcard when you create external tables linked to Datastore or Firestore exports.

## Pricing

The following Cloud Storage retrieval and data transfer fees apply to BigQuery requests:

  - Retrieval fees for Nearline, Coldline, and Archive storage classes are charged according to existing [pricing documentation](https://cloud.google.com/storage/pricing#retrieval-pricing) and [retrieval SKUs](/bigquery/docs/skus?filter=95FF-2EF5-5EA1%20Retrieval&currency=USD) .
  - Inter-region network data transfer fees are charged when a BigQuery job in one location reads data stored in a Cloud Storage bucket in a different location. These charges are covered by following SKUs:
      - Google Cloud Storage Data Transfer between continent 1 and continent 2. For example, see [Google Cloud Storage Data Transfer between Northern America and Europe](/bigquery/docs/skus?currency=USD&filter=C7FF-4F9E-C0DB&e=48754805) for data transfer from `  us-central1  ` to `  europe-west1  ` .
      - Network Data Transfer Google Cloud Inter Region within a continent. For example, see [Network Data Transfer Google Cloud Inter Region within Northern America](/bigquery/docs/skus?currency=USD&filter=8878-37D4-D2AC&e=48754805) for data transfer from `  us-east4  ` to `  US  ` .

## Limitations

For information about limitations that apply to external tables, see [External table limitations](/bigquery/docs/external-tables#limitations) .

## What's next

  - Learn about [external tables](/bigquery/docs/external-tables) .
  - Learn about [BigLake tables](/bigquery/docs/biglake-intro) .
