# Create Amazon S3 BigLake external tables

**Important:** The term "BigLake" on this page refers to an access delegation functionality for external tables in BigQuery. For information about BigLake, the stand-alone Google Cloud product that includes BigLake metastore, the Apache Iceberg REST catalog, and BigLake tables for Apache Iceberg see [BigLake overview](/biglake/docs/introduction) .

This document describes how to create an Amazon Simple Storage Service (Amazon S3) BigLake table. A [BigLake table](/bigquery/docs/biglake-intro) lets you use access delegation to query data in Amazon S3. Access delegation decouples access to the BigLake table from access to the underlying datastore.

For information about how data flows between BigQuery and Amazon S3, see [Data flow when querying data](/bigquery/docs/omni-introduction#query-data) .

## Before you begin

Ensure that you have a [connection to access Amazon S3 data](/bigquery/docs/omni-aws-create-connection) .

### Required roles

To get the permissions that you need to create an external table, ask your administrator to grant you the [BigQuery Admin](/iam/docs/roles-permissions/bigquery#bigquery.admin) ( `  roles/bigquery.admin  ` ) IAM role on your dataset. For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

This predefined role contains the permissions required to create an external table. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

The following permissions are required to create an external table:

  - `  bigquery.tables.create  `
  - `  bigquery.connections.delegate  `

You might also be able to get these permissions with [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

## Create a dataset

Before you create an external table, you need to create a dataset in the [supported region](/bigquery/docs/omni-introduction#locations) . Select one of the following options:

### Console

Go to the **BigQuery** page.

In the left pane, click explore **Explorer** .

In the **Explorer** pane, select the project where you want to create the dataset.

Click more\_vert **View actions** , and then click **Create dataset** .

On the **Create dataset** page, specify the following details:

1.  For **Dataset ID** enter a unique dataset [name](/bigquery/docs/datasets#dataset-naming) .
2.  For **Data location** choose a [supported region](/bigquery/docs/omni-introduction#locations) .
3.  Optional: To delete tables automatically, select the **Enable table expiration** checkbox and set the **Default maximum table age** in days. Data in Amazon S3 is not deleted when the table expires.
4.  If you want to use [default collation](/bigquery/docs/reference/standard-sql/collation-concepts) , expand the **Advanced options** section and then select the **Enable default collation** option.
5.  Click **Create dataset** .

### SQL

Use the [`  CREATE SCHEMA  ` DDL statement](/bigquery/docs/reference/standard-sql/data-definition-language#create_schema_statement) . The following example create a dataset in the `  aws-us-east-1  ` region:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
    CREATE SCHEMA mydataset
    OPTIONS (
      location = 'aws-us-east-1');
    ```

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](/bigquery/docs/running-queries#queries) .

### bq

In a command-line environment, create a dataset using the [`  bq mk  ` command](/bigquery/docs/reference/bq-cli-reference#mk-dataset) :

``` text
bq --location=LOCATION mk \
    --dataset \
PROJECT_ID:DATASET_NAME
```

The `  --project_id  ` parameter overrides the default project.

Replace the following:

  - `  LOCATION  ` : the location of your dataset
    
    For information about supported regions, see [Locations](/bigquery/docs/omni-introduction#locations) . After you create a dataset, you can't change its location. You can set a default value for the location by using the [`  .bigqueryrc  ` file](/bigquery/docs/bq-command-line-tool#setting_default_values_for_command-line_flags) .

  - `  PROJECT_ID  ` : your project ID

  - `  DATASET_NAME  ` : the name of the dataset that you want to create
    
    To create a dataset in a project other than your default project, add the project ID to the dataset name in the following format: `  PROJECT_ID : DATASET_NAME  ` .

### Java

Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Java API reference documentation](/java/docs/reference/google-cloud-bigquery/latest/overview) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` java
import com.google.cloud.bigquery.BigQuery;
import com.google.cloud.bigquery.BigQueryException;
import com.google.cloud.bigquery.BigQueryOptions;
import com.google.cloud.bigquery.Dataset;
import com.google.cloud.bigquery.DatasetInfo;

// Sample to create a aws dataset
public class CreateDatasetAws {

  public static void main(String[] args) {
    // TODO(developer): Replace these variables before running the sample.
    String projectId = "MY_PROJECT_ID";
    String datasetName = "MY_DATASET_NAME";
    // Note: As of now location only supports aws-us-east-1
    String location = "aws-us-east-1";
    createDatasetAws(projectId, datasetName, location);
  }

  public static void createDatasetAws(String projectId, String datasetName, String location) {
    try {
      // Initialize client that will be used to send requests. This client only needs to be created
      // once, and can be reused for multiple requests.
      BigQuery bigquery = BigQueryOptions.getDefaultInstance().getService();

      DatasetInfo datasetInfo =
          DatasetInfo.newBuilder(projectId, datasetName).setLocation(location).build();

      Dataset dataset = bigquery.create(datasetInfo);
      System.out.println(
          "Aws dataset created successfully :" + dataset.getDatasetId().getDataset());
    } catch (BigQueryException e) {
      System.out.println("Aws dataset was not created. \n" + e.toString());
    }
  }
}
```

## Create BigLake tables on unpartitioned data

Select one of the following options:

### Console

1.  Go to the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :
    
    If you don't see the left pane, click last\_page **Expand left pane** to open the pane.

3.  In the **Explorer** pane, expand your project, click **Datasets** , and then select a dataset.

4.  In the **Dataset info** section, click add\_box **Create table** .

5.  On the **Create table** page, in the **Source** section, do the following:
    
    1.  For **Create table from** , select **Amazon S3** .
    2.  For **Select S3 path** , enter a URI pointing to the Amazon S3 data in the format `  s3:// BUCKET_NAME / PATH  ` . Replace `  BUCKET_NAME  ` with the name of the Amazon S3 bucket; the bucket's region should be the same as the dataset's region. Replace `  PATH  ` with the path that you would like to write the exported file to; it can contain one wildcard `  *  ` .
    3.  For **File format** , select the data format in Amazon S3. Supported formats are **AVRO** , **CSV** , **DELTA\_LAKE** , **ICEBERG** , **JSONL** , **ORC** , and **PARQUET** .

6.  In the **Destination** section, specify the following details:
    
    1.  For **Dataset** , choose the appropriate dataset.
    2.  In the **Table** field, enter the name of the table.
    3.  Verify that **Table type** is set to **External table** .
    4.  For **Connection ID** , choose the appropriate connection ID from the drop-down. For information about connections, see [Connect to Amazon S3](/bigquery/docs/omni-aws-create-connection) .

7.  In the **Schema** section, you can either enable [schema auto-detection](/bigquery/docs/schema-detect) or manually specify a schema if you have a source file. If you don't have a source file, you must manually specify a schema.
    
      - To enable schema auto-detection, select the **Auto-detect** option.
    
      - To manually specify a schema, leave the **Auto-detect** option unchecked. Enable **Edit as text** and enter the table schema as a [JSON array](/bigquery/docs/schemas#specifying_a_json_schema_file) .

8.  Click **Create table** .

### SQL

To create a BigLake table, use the [`  CREATE EXTERNAL TABLE  ` statement](/bigquery/docs/reference/standard-sql/data-definition-language#create_external_table_statement) with the `  WITH CONNECTION  ` clause:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
    CREATE EXTERNAL TABLE DATASET_NAME.TABLE_NAME
      WITH CONNECTION `AWS_LOCATION.CONNECTION_NAME`
      OPTIONS (
        format = "DATA_FORMAT",
        uris = ["S3_URI"],
        max_staleness = STALENESS_INTERVAL,
        metadata_cache_mode = 'CACHE_MODE');
    ```
    
    Replace the following:
    
      - `  DATASET_NAME  ` : the name of the dataset you created
    
      - `  TABLE_NAME  ` : the name you want to give to this table
    
      - `  AWS_LOCATION  ` : an AWS location in Google Cloud (for example, \`aws-us-east-1\`)
    
      - `  CONNECTION_NAME  ` : the name of the connection you created
    
      - `  DATA_FORMAT  ` : any of the supported [BigQuery federated formats](/bigquery/external-data-sources) (such as `  AVRO  ` , `  CSV  ` , `  DELTA_LAKE  ` , `  ICEBERG  ` , or `  PARQUET  ` ( [preview](https://cloud.google.com/products/#product-launch-stages) ))
    
      - `  S3_URI  ` : a URI pointing to the Amazon S3 data (for example, `  s3://bucket/path  ` )
    
      - `  STALENESS_INTERVAL  ` : specifies whether cached metadata is used by operations against the BigLake table, and how fresh the cached metadata must be in order for the operation to use it. For more information about metadata caching considerations, see [Metadata caching for performance](/bigquery/docs/omni-introduction#metadata_caching_for_performance) .
        
        To disable metadata caching, specify 0. This is the default.
        
        To enable metadata caching, specify an [interval literal](/bigquery/docs/reference/standard-sql/lexical#interval_literals) value between 30 minutes and 7 days. For example, specify `  INTERVAL 4 HOUR  ` for a 4 hour staleness interval. With this value, operations against the table use cached metadata if it has been refreshed within the past 4 hours. If the cached metadata is older than that, the operation retrieves metadata from Amazon S3 instead.
    
      - `  CACHE_MODE  ` : specifies whether the metadata cache is refreshed automatically or manually. For more information about metadata caching considerations, see [Metadata caching for performance](/bigquery/docs/omni-introduction#metadata_caching_for_performance) .
        
        Set to `  AUTOMATIC  ` for the metadata cache to be refreshed at a system-defined interval, usually somewhere between 30 and 60 minutes.
        
        Set to `  MANUAL  ` if you want to refresh the metadata cache on a schedule you determine. In this case, you can call the [`  BQ.REFRESH_EXTERNAL_METADATA_CACHE  ` system procedure](/bigquery/docs/reference/system-procedures#bqrefresh_external_metadata_cache) to refresh the cache.
        
        You must set `  CACHE_MODE  ` if `  STALENESS_INTERVAL  ` is set to a value greater than 0.

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](/bigquery/docs/running-queries#queries) .

Example:

``` text
CREATE EXTERNAL TABLE awsdataset.awstable
  WITH CONNECTION `aws-us-east-1.s3-read-connection`
  OPTIONS (
    format="CSV",
    uris=["s3://s3-bucket/path/file.csv"],
    max_staleness = INTERVAL 1 DAY,
    metadata_cache_mode = 'AUTOMATIC'
);
```

### bq

Create a [table definition file](/bigquery/external-table-definition) :

``` text
bq mkdef  \
--source_format=DATA_FORMAT \
--connection_id=AWS_LOCATION.CONNECTION_NAME \
--metadata_cache_mode=CACHE_MODE \
S3_URI > table_def
```

Replace the following:

  - `  DATA_FORMAT  ` : any of the supported [BigQuery federated formats](/bigquery/external-data-sources) (such as `  AVRO  ` , `  CSV  ` , `  DELTA_LAKE  ` , `  ICEBERG  ` , or `  PARQUET  ` ).

  - `  S3_URI  ` : a URI pointing to the Amazon S3 data (for example, `  s3://bucket/path  ` ).

  - `  AWS_LOCATION  ` : an AWS location in Google Cloud (for example, `  aws-us-east-1  ` ).

  - `  CONNECTION_NAME  ` : the name of the connection you created.

  - `  CACHE_MODE  ` : specifies whether the metadata cache is refreshed automatically or manually. You only need to include this flag if you also plan to use the `  --max_staleness  ` flag in the subsequent `  bq mk  ` command to enable metadata caching. For more information about metadata caching considerations, see [Metadata caching for performance](/bigquery/docs/omni-introduction#metadata_caching_for_performance) .
    
    Set to `  AUTOMATIC  ` for the metadata cache to be refreshed at a system-defined interval, usually somewhere between 30 and 60 minutes.
    
    Set to `  MANUAL  ` if you want to refresh the metadata cache on a schedule you determine. In this case, you can call the [`  BQ.REFRESH_EXTERNAL_METADATA_CACHE  ` system procedure](/bigquery/docs/reference/system-procedures#bqrefresh_external_metadata_cache) to refresh the cache. You must set `  CACHE_MODE  ` if `  STALENESS_INTERVAL  ` is set to a value greater than 0.

**Note:** To override the default project, use the `  --project_id= PROJECT_ID  ` parameter. Replace `  PROJECT_ID  ` with the ID of your Google Cloud project.

Next, create the BigLake table:

``` text
bq mk --max_staleness=STALENESS_INTERVAL --external_table_definition=table_def DATASET_NAME.TABLE_NAME
```

Replace the following:

  - `  STALENESS_INTERVAL  ` : specifies whether cached metadata is used by operations against the BigLake table, and how fresh the cached metadata must be in order for the operation to use it. For more information about metadata caching considerations, see [Metadata caching for performance](/bigquery/docs/omni-introduction#metadata_caching_for_performance) .
    
    To disable metadata caching, specify 0. This is the default.
    
    To enable metadata caching, specify an [interval literal](/bigquery/docs/reference/standard-sql/lexical#interval_literals) value between 30 minutes and 7 days. For example, specify `  INTERVAL 4 HOUR  ` for a 4 hour staleness interval. With this value, operations against the table use cached metadata if it has been refreshed within the past 4 hours. If the cached metadata is older than that, the operation retrieves metadata from Amazon S3 instead.

  - `  DATASET_NAME  ` : the name of the dataset you created.

  - `  TABLE_NAME  ` : the name you want to give to this table.

For example, the following command creates a new BigLake table, `  awsdataset.awstable  ` , which can query your Amazon S3 data that's stored at the path `  s3://s3-bucket/path/file.csv  ` and has a read connection in the location `  aws-us-east-1  ` :

``` text
bq mkdef  \
--autodetect \
--source_format=CSV \
--connection_id=aws-us-east-1.s3-read-connection \
--metadata_cache_mode=AUTOMATIC \
s3://s3-bucket/path/file.csv > table_def

bq mk --max_staleness=INTERVAL "1" HOUR \
--external_table_definition=table_def awsdataset.awstable
```

### API

Call the [`  tables.insert  ` method](/bigquery/docs/reference/rest/v2/tables/insert) API method, and create an [`  ExternalDataConfiguration  `](/bigquery/docs/reference/rest/v2/tables#externaldataconfiguration) in the [`  Table  ` resource](/bigquery/docs/reference/rest/v2/tables#Table) that you pass in.

Specify the `  schema  ` property or set the `  autodetect  ` property to `  true  ` to enable schema auto detection for supported data sources.

Specify the `  connectionId  ` property to identify the connection to use for connecting to Amazon S3.

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
import com.google.cloud.bigquery.Schema;
import com.google.cloud.bigquery.StandardSQLTypeName;
import com.google.cloud.bigquery.TableId;
import com.google.cloud.bigquery.TableInfo;

// Sample to create an external aws table
public class CreateExternalTableAws {

  public static void main(String[] args) {
    // TODO(developer): Replace these variables before running the sample.
    String projectId = "MY_PROJECT_ID";
    String datasetName = "MY_DATASET_NAME";
    String tableName = "MY_TABLE_NAME";
    String connectionId = "MY_CONNECTION_ID";
    String sourceUri = "s3://your-bucket-name/";
    CsvOptions options = CsvOptions.newBuilder().setSkipLeadingRows(1).build();
    Schema schema =
        Schema.of(
            Field.of("name", StandardSQLTypeName.STRING),
            Field.of("post_abbr", StandardSQLTypeName.STRING));
    ExternalTableDefinition externalTableDefinition =
        ExternalTableDefinition.newBuilder(sourceUri, options)
            .setConnectionId(connectionId)
            .setSchema(schema)
            .build();
    createExternalTableAws(projectId, datasetName, tableName, externalTableDefinition);
  }

  public static void createExternalTableAws(
      String projectId,
      String datasetName,
      String tableName,
      ExternalTableDefinition externalTableDefinition) {
    try {
      // Initialize client that will be used to send requests. This client only needs to be created
      // once, and can be reused for multiple requests.
      BigQuery bigquery = BigQueryOptions.getDefaultInstance().getService();

      TableId tableId = TableId.of(projectId, datasetName, tableName);
      TableInfo tableInfo = TableInfo.newBuilder(tableId, externalTableDefinition).build();

      bigquery.create(tableInfo);
      System.out.println("Aws external table created successfully");

      // Clean up
      bigquery.delete(TableId.of(projectId, datasetName, tableName));
    } catch (BigQueryException e) {
      System.out.println("Aws external was not created." + e.toString());
    }
  }
}
```

## Create BigLake tables on partitioned data

You can create a BigLake table for Hive partitioned data in Amazon S3. After you create an externally partitioned table, you can't change the partition key. You need to recreate the table to change the partition key.

To create a BigLake table based on Hive partitioned data, select one of the following options:

### Console

1.  Go to the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :

3.  In the **Explorer** pane, expand your project, click **Datasets** , and select a dataset.

4.  Click **Create table** . This opens the **Create table** pane.

5.  In the **Source** section, specify the following details:
    
    1.  For **Create table from** , select **Amazon S3** .
    
    2.  Provide the path to the folder, using [wildcards](/bigquery/docs/batch-loading-data#load-wildcards) . For example, `  s3://mybucket/*  ` .
        
        The folder must be in the same location as the dataset that contains the table you want to create, append, or overwrite.
    
    3.  From the **File format** list, select the file type.
    
    4.  Select the **Source data partitioning** checkbox, and then specify the following details:
        
        1.  For **Select Source URI Prefix** , enter the URI prefix. For example, `  s3://mybucket/my_files  ` .
        
        2.  Optional: To require a partition filter on all queries for this table, select the **Require partition filter** checkbox. Requiring a partition filter can reduce cost and improve performance. For more information, see [Requiring predicate filters on partition keys in queries](/bigquery/docs/hive-partitioned-queries-gcs#requiring_predicate_filters_on_partition_keys_in_queries) .
        
        3.  In the **Partition inference mode** section, select one of the following options:
            
              - **Automatically infer types** : set the partition schema detection mode to `  AUTO  ` .
              - **All columns are strings** : set the partition schema detection mode to `  STRINGS  ` .
              - **Provide my own** : set the partition schema detection mode to `  CUSTOM  ` and manually enter the schema information for the partition keys. For more information, see [Custom partition key schema](/bigquery/docs/hive-partitioned-loads-gcs#custom_partition_key_schema) .

6.  In the **Destination** section, specify the following details:
    
    1.  For **Project** , select the project in which you want to create the table.
    2.  For **Dataset** , select the dataset in which you want to create the table.
    3.  For **Table** , enter the name of the table that you want to create.
    4.  For **Table type** , verify that **External table** is selected.
    5.  For **Connection ID** , select the connection that you created earlier.

7.  In the **Schema** section, you can either enable [schema auto-detection](/bigquery/docs/schema-detect) or manually specify a schema if you have a source file. If you don't have a source file, you must manually specify a schema.
    
      - To enable schema auto-detection, select the **Auto-detect** option.
    
      - To manually specify a schema, leave the **Auto-detect** option unchecked. Enable **Edit as text** and enter the table schema as a [JSON array](/bigquery/docs/schemas#specifying_a_json_schema_file) .

8.  To ignore rows with extra column values that don't match the schema, expand the **Advanced options** section and select **Unknown values** .

9.  Click **Create table** .

### SQL

Use the [`  CREATE EXTERNAL TABLE  ` DDL statement](/bigquery/docs/reference/standard-sql/data-definition-language#create_external_table_statement) :

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
    CREATE EXTERNAL TABLE `PROJECT_ID.DATASET.EXTERNAL_TABLE_NAME`
    WITH PARTITION COLUMNS
    (
      PARTITION_COLUMN PARTITION_COLUMN_TYPE,
    )
    WITH CONNECTION `PROJECT_ID.REGION.CONNECTION_ID`
    OPTIONS (
      hive_partition_uri_prefix = "HIVE_PARTITION_URI_PREFIX",
      uris=['FILE_PATH'],
      format ="TABLE_FORMAT"
      max_staleness = STALENESS_INTERVAL,
      metadata_cache_mode = 'CACHE_MODE'
    );
    ```
    
    Replace the following:
    
      - `  PROJECT_ID  ` : the name of your project in which you want to create the table—for example, `  myproject  `
    
      - `  DATASET  ` : the name of the BigQuery dataset that you want to create the table in—for example, `  mydataset  `
    
      - `  EXTERNAL_TABLE_NAME  ` : the name of the table that you want to create—for example, `  mytable  `
    
      - `  PARTITION_COLUMN  ` : the name of the partitioning column
    
      - `  PARTITION_COLUMN_TYPE  ` : the type of the partitioning column
    
      - `  REGION  ` : the region that contains the connection—for example, `  us  `
    
      - `  CONNECTION_ID  ` : the name of the connection—for example, `  myconnection  `
    
      - `  HIVE_PARTITION_URI_PREFIX  ` : hive partitioning uri prefix–for example: `  s3://mybucket/  `
    
      - `  FILE_PATH  ` : path to the data source for the external table that you want to create—for example: `  s3://mybucket/*.parquet  `
    
      - `  TABLE_FORMAT  ` : the format of the table that you want to create—for example, `  PARQUET  `
    
      - `  STALENESS_INTERVAL  ` : specifies whether cached metadata is used by operations against the BigLake table, and how fresh the cached metadata must be in order for the operation to use it. For more information about metadata caching considerations, see [Metadata caching for performance](/bigquery/docs/omni-introduction#metadata_caching_for_performance) .
        
        To disable metadata caching, specify 0. This is the default.
        
        To enable metadata caching, specify an [interval literal](/bigquery/docs/reference/standard-sql/lexical#interval_literals) value between 30 minutes and 7 days. For example, specify `  INTERVAL 4 HOUR  ` for a 4 hour staleness interval. With this value, operations against the table use cached metadata if it has been refreshed within the past 4 hours. If the cached metadata is older than that, the operation retrieves metadata from Amazon S3 instead.
    
      - `  CACHE_MODE  ` : specifies whether the metadata cache is refreshed automatically or manually. For more information about metadata caching considerations, see [Metadata caching for performance](/bigquery/docs/omni-introduction#metadata_caching_for_performance) .
        
        Set to `  AUTOMATIC  ` for the metadata cache to be refreshed at a system-defined interval, usually somewhere between 30 and 60 minutes.
        
        Set to `  MANUAL  ` if you want to refresh the metadata cache on a schedule you determine. In this case, you can call the [`  BQ.REFRESH_EXTERNAL_METADATA_CACHE  ` system procedure](/bigquery/docs/reference/system-procedures#bqrefresh_external_metadata_cache) to refresh the cache.
        
        You must set `  CACHE_MODE  ` if `  STALENESS_INTERVAL  ` is set to a value greater than 0.

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](/bigquery/docs/running-queries#queries) .

**Examples**

The following example creates a BigLake table over partitioned data in Amazon S3. The schema is autodetected.

``` text
CREATE EXTERNAL TABLE `my_dataset.my_table`
WITH PARTITION COLUMNS
(
  sku STRING,
)
WITH CONNECTION `us.my-connection`
OPTIONS(
  hive_partition_uri_prefix = "s3://mybucket/products",
  uris = ['s3://mybucket/products/*']
  max_staleness = INTERVAL 1 DAY,
  metadata_cache_mode = 'AUTOMATIC'
);
```

### bq

First, use the [`  bq mkdef  `](/bigquery/docs/reference/bq-cli-reference#bq_mkdef) command to create a table definition file:

``` text
bq mkdef \
--source_format=SOURCE_FORMAT \
--connection_id=REGION.CONNECTION_ID \
--hive_partitioning_mode=PARTITIONING_MODE \
--hive_partitioning_source_uri_prefix=URI_SHARED_PREFIX \
--require_hive_partition_filter=BOOLEAN \
--metadata_cache_mode=CACHE_MODE \
 URIS > DEFINITION_FILE
```

Replace the following:

  - `  SOURCE_FORMAT  ` : the format of the external data source. For example, `  CSV  ` .

  - `  REGION  ` : the region that contains the connection—for example, `  us  ` .

  - `  CONNECTION_ID  ` : the name of the connection—for example, `  myconnection  ` .

  - `  PARTITIONING_MODE  ` : the Hive partitioning mode. Use one of the following values:
    
      - `  AUTO  ` : Automatically detect the key names and types.
      - `  STRINGS  ` : Automatically convert the key names to strings.
      - `  CUSTOM  ` : Encode the key schema in the source URI prefix.

  - `  URI_SHARED_PREFIX  ` : the source URI prefix.

  - `  BOOLEAN  ` : specifies whether to require a predicate filter at query time. This flag is optional. The default value is `  false  ` .

  - `  CACHE_MODE  ` : specifies whether the metadata cache is refreshed automatically or manually. You only need to include this flag if you also plan to use the `  --max_staleness  ` flag in the subsequent `  bq mk  ` command to enable metadata caching. For more information about metadata caching considerations, see [Metadata caching for performance](/bigquery/docs/omni-introduction#metadata_caching_for_performance) .
    
    Set to `  AUTOMATIC  ` for the metadata cache to be refreshed at a system-defined interval, usually somewhere between 30 and 60 minutes.
    
    Set to `  MANUAL  ` if you want to refresh the metadata cache on a schedule you determine. In this case, you can call the [`  BQ.REFRESH_EXTERNAL_METADATA_CACHE  ` system procedure](/bigquery/docs/reference/system-procedures#bqrefresh_external_metadata_cache) to refresh the cache. You must set `  CACHE_MODE  ` if `  STALENESS_INTERVAL  ` is set to a value greater than 0.

  - `  URIS  ` : the path to the Amazon S3 folder, using wildcard format.

  - `  DEFINITION_FILE  ` : the path to the [table definition file](/bigquery/external-table-definition) on your local machine.

If `  PARTITIONING_MODE  ` is `  CUSTOM  ` , include the partition key schema in the source URI prefix, using the following format:

``` text
--hive_partitioning_source_uri_prefix=URI_SHARED_PREFIX/{KEY1:TYPE1}/{KEY2:TYPE2}/...
```

After you create the table definition file, use the [`  bq mk  `](/bigquery/docs/reference/bq-cli-reference#mk-table) command to create the BigLake table:

``` text
bq mk --max_staleness=STALENESS_INTERVAL \
--external_table_definition=DEFINITION_FILE \
DATASET_NAME.TABLE_NAME \
SCHEMA
```

Replace the following:

  - `  STALENESS_INTERVAL  ` : specifies whether cached metadata is used by operations against the BigLake table, and how fresh the cached metadata must be in order for the operation to use it. For more information about metadata caching considerations, see [Metadata caching for performance](/bigquery/docs/omni-introduction#metadata_caching_for_performance) .
    
    To disable metadata caching, specify 0. This is the default.
    
    To enable metadata caching, specify an [interval literal](/bigquery/docs/reference/standard-sql/lexical#interval_literals) value between 30 minutes and 7 days. For example, specify `  INTERVAL 4 HOUR  ` for a 4 hour staleness interval. With this value, operations against the table use cached metadata if it has been refreshed within the past 4 hours. If the cached metadata is older than that, the operation retrieves metadata from Amazon S3 instead.

  - `  DEFINITION_FILE  ` : the path to the table definition file.

  - `  DATASET_NAME  ` : the name of the dataset that contains the table.

  - `  TABLE_NAME  ` : the name of the table you're creating.

  - `  SCHEMA  ` : specifies a path to a [JSON schema file](/bigquery/docs/schemas#specifying_a_json_schema_file) , or specifies the schema in the form `  field:data_type,field:data_type,...  ` . To use schema auto-detection, omit this argument.

**Examples**

The following example uses `  AUTO  ` Hive partitioning mode for Amazon S3 data:

``` text
bq mkdef --source_format=CSV \
  --connection_id=us.my-connection \
  --hive_partitioning_mode=AUTO \
  --hive_partitioning_source_uri_prefix=s3://mybucket/myTable \
  --metadata_cache_mode=AUTOMATIC \
  s3://mybucket/* > mytable_def

bq mk --max_staleness=INTERVAL "1" HOUR \
  --external_table_definition=mytable_def \
  mydataset.mytable \
  Region:STRING,Quarter:STRING,Total_sales:INTEGER
```

The following example uses `  STRING  ` Hive partitioning mode for Amazon S3 data:

``` text
bq mkdef --source_format=CSV \
  --connection_id=us.my-connection \
  --hive_partitioning_mode=STRING \
  --hive_partitioning_source_uri_prefix=s3://mybucket/myTable \
  --metadata_cache_mode=AUTOMATIC \
  s3://mybucket/myTable/* > mytable_def

bq mk --max_staleness=INTERVAL "1" HOUR \
  --external_table_definition=mytable_def \
  mydataset.mytable \
  Region:STRING,Quarter:STRING,Total_sales:INTEGER
```

### API

To set Hive partitioning using the BigQuery API, include the [`  hivePartitioningOptions  `](/bigquery/docs/reference/rest/v2/tables#hivepartitioningoptions) object in the [`  ExternalDataConfiguration  `](/bigquery/docs/reference/rest/v2/tables#externaldataconfiguration) object when you create the [table definition file](/bigquery/external-table-definition) . To create a BigLake table, you must also specify a value for the `  connectionId  ` field.

If you set the `  hivePartitioningOptions.mode  ` field to `  CUSTOM  ` , you must encode the partition key schema in the `  hivePartitioningOptions.sourceUriPrefix  ` field as follows: `  s3:// BUCKET / PATH_TO_TABLE /{ KEY1 : TYPE1 }/{ KEY2 : TYPE2 }/...  `

To enforce the use of a predicate filter at query time, set the `  hivePartitioningOptions.requirePartitionFilter  ` field to `  true  ` .

## Delta Lake tables

Delta Lake is an open source table format that supports petabyte scale data tables. Delta Lake tables can be queried as both temporary and permanent tables, and is supported as a [BigLake table](/bigquery/docs/biglake-intro) .

### Schema synchronization

Delta Lake maintains a canonical schema as part of its metadata. You can't update a schema using a JSON metadata file. To update the schema:

1.  Use the [`  bq update  ` command](/bigquery/docs/reference/bq-cli-reference#bq_update) with the `  --autodetect_schema  ` flag:
    
    ``` bash
    bq update --autodetect_schema
    PROJECT_ID:DATASET.TABLE
    ```
    
    Replace the following:
    
      - `  PROJECT_ID  ` : the project ID containing the table that you want to update
    
      - `  DATASET  ` : the dataset containing the table that you want to update
    
      - `  TABLE  ` : the table that you want to update

### Type conversion

BigQuery converts Delta Lake data types to the following BigQuery data types:

<table>
<thead>
<tr class="header">
<th><strong>Delta Lake Type</strong></th>
<th><strong>BigQuery Type</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       boolean      </code></td>
<td><code dir="ltr" translate="no">       BOOL      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       byte      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       int      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       long      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       float      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       double      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       Decimal(P/S)      </code></td>
<td><code dir="ltr" translate="no">       NUMERIC      </code> or <code dir="ltr" translate="no">       BIG_NUMERIC      </code> depending on precision</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       date      </code></td>
<td><code dir="ltr" translate="no">       DATE      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       time      </code></td>
<td><code dir="ltr" translate="no">       TIME      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       timestamp (not partition column)      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       timestamp (partition column)      </code></td>
<td><code dir="ltr" translate="no">       DATETIME      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       string      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       binary      </code></td>
<td><code dir="ltr" translate="no">       BYTES      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       array&lt;Type&gt;      </code></td>
<td><code dir="ltr" translate="no">       ARRAY&lt;Type&gt;      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       struct      </code></td>
<td><code dir="ltr" translate="no">       STRUCT      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       map&lt;KeyType, ValueType&gt;      </code></td>
<td><code dir="ltr" translate="no">       ARRAY&lt;Struct&lt;key KeyType, value ValueType&gt;&gt;      </code></td>
</tr>
</tbody>
</table>

### Limitations

The following limitations apply to Delta Lake tables:

  - [External table limitations](/bigquery/docs/external-tables#limitations) apply to Delta Lake tables.

  - Delta Lake tables are only supported on BigQuery Omni and have the associated [limitations](/bigquery/docs/omni-introduction#limitations) .

  - You can't update a table with a new JSON metadata file. You must use an auto detect schema table update operation. See [Schema synchronization](#schema_synchronization) for more information.

  - BigLake security features only protect Delta Lake tables when accessed through BigQuery services.

### Create a Delta Lake table

The following example creates an external table by using the [`  CREATE EXTERNAL TABLE  `](/bigquery/docs/reference/standard-sql/data-definition-language#create_external_table_statement) statement with the Delta Lake format:

``` googlesql
CREATE [OR REPLACE] EXTERNAL TABLE table_name
WITH CONNECTION connection_name
OPTIONS (
         format = 'DELTA_LAKE',
         uris = ["parent_directory"]
       );
```

Replace the following:

  - table\_name : The name of the table.

  - connection\_name : The name of the connection. The connection must identify either an [Amazon S3](/bigquery/docs/omni-aws-create-connection) or a [Blob Storage](/bigquery/docs/omni-azure-create-connection) source.

  - parent\_directory : The URI of the parent directory.

### Cross-cloud transfer with Delta Lake

The following example uses the [`  LOAD DATA  `](/bigquery/docs/reference/standard-sql/other-statements#load_data_statement) statement to load data to the appropriate table:

``` googlesql
LOAD DATA [INTO | OVERWRITE] table_name
FROM FILES (
        format = 'DELTA_LAKE',
        uris = ["parent_directory"]
)
WITH CONNECTION connection_name;
```

For more examples of cross-cloud data transfers, see [Load data with cross cloud operations](/bigquery/docs/load-data-using-cross-cloud-transfer#load-data) .

## Query BigLake tables

For more information, see [Query Amazon S3 data](/bigquery/docs/query-aws-data) .

## View resource metadata

**Preview**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

You can view the resource metadata with [`  INFORMATION_SCHEMA  `](/bigquery/docs/information-schema-intro) views. When you query the [`  JOBS_BY_*  `](/bigquery/docs/information-schema-jobs) , [`  JOBS_TIMELINE_BY_*  `](/bigquery/docs/information-schema-jobs-timeline) , and [`  RESERVATION*  `](/bigquery/docs/information-schema-reservations) views, you must [specify the query's processing location](/bigquery/docs/locations#specify_locations) that is collocated with the table's region. For information about BigQuery Omni locations, see [Locations](/bigquery/docs/locations#omni-loc) . For all other system tables, specifying the query job location is *optional* .

For information about the system tables that BigQuery Omni supports, see [Limitations](/bigquery/docs/omni-introduction#limitations) .

To query `  JOBS_*  ` and `  RESERVATION*  ` system tables, select one of the following methods to specify the processing location:

### Console

1.  Go to the **BigQuery** page.

2.  If the **Editor** tab isn't visible, then click add\_box **Compose new query** .

3.  Click **More** \> **Query settings** . The **Query settings** dialog opens.

4.  In the **Query settings** dialog, for **Additional settings** \> **Data location** , select the [BigQuery region](/bigquery/docs/locations#omni-loc) that is collocated with the BigQuery Omni region. For example, if your BigQuery Omni region is `  aws-us-east-1  ` , specify `  us-east4  ` .

5.  Select the remaining fields and click **Save** .

### bq

Use the `  --location  ` flag to set the job's processing location to the [BigQuery region](/bigquery/docs/locations#omni-loc) that is collocated with the BigQuery Omni region. For example, if your BigQuery Omni region is `  aws-us-east-1  ` , specify `  us-east4  ` .

**Example**

``` text
bq query --use_legacy_sql=false --location=us-east4 \
"SELECT * FROM region-aws-us-east-1.INFORMATION_SCHEMA.JOBS limit 10;"
```

``` text
bq query --use_legacy_sql=false --location=asia-northeast3 \
"SELECT * FROM region-aws-ap-northeast-2.INFORMATION_SCHEMA.JOBS limit 10;"
```

### API

If you are [running jobs programmatically](/bigquery/docs/running-jobs) , set the location argument to the [BigQuery region](/bigquery/docs/locations#omni-loc) that is collocated with the BigQuery Omni region. For example, if your BigQuery Omni region is `  aws-us-east-1  ` , specify `  us-east4  ` .

The following example lists the metadata refresh jobs in last six hours:

``` text
SELECT
 *
FROM
 `region-REGION_NAME`.INFORMATION_SCHEMA.JOBS_BY_PROJECT
WHERE
 job_id LIKE '%metadata_cache_refresh%'
 AND creation_time > TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 6 HOUR)
ORDER BY start_time desc
LIMIT 10;
```

Replace REGION\_NAME with your region.

## VPC Service Controls

You can use VPC Service Controls perimeters to restrict access from BigQuery Omni to an external cloud service as an extra layer of defense. For example, VPC Service Controls perimeters can limit exports from your BigQuery Omni tables to a specific Amazon S3 bucket or Blob Storage container.

To learn more about VPC Service Controls, see [Overview of VPC Service Controls](/vpc-service-controls/docs/overview) .

### Required permission

Ensure that you have the required permissions to configure service perimeters. To view a list of IAM roles required to configure VPC Service Controls, see [Access control with IAM](/vpc-service-controls/docs/access-control) in the VPC Service Controls documentation.

### Set up VPC Service Controls using the Google Cloud console

1.  In the Google Cloud console navigation menu, click **Security** , and then click **VPC Service Controls** .

2.  To set up VPC Service Controls for BigQuery Omni, follow the steps in the [Create a service perimeter](/vpc-service-controls/docs/create-service-perimeters#create_a_service_perimeter) guide, and when you are in the **Egress rules** pane, follow these steps:
    
    1.  In the **Egress rules** panel, click **Add rule** .
    
    2.  In the **From attributes of the API client** section, select an option from the **Identity** list.
    
    3.  Select **To attributes of external resources** .
    
    4.  To add an external resource, click **Add external resources** .
    
    5.  In the **Add external resource** dialog, for **External resource name** , enter a valid resource name. For example:
        
          - For Amazon Simple Storage Service (Amazon S3): `  s3:// BUCKET_NAME  `
            
            Replace BUCKET\_NAME with the name of your Amazon S3 bucket.
        
          - For Azure Blob Storage: `  azure://myaccount.blob.core.windows.net/ CONTAINER_NAME  `
            
            Replace CONTAINER NAME with the name of your Blob Storage container.
        
        For a list of egress rule attributes, see [Egress rules reference](/vpc-service-controls/docs/ingress-egress-rules#egress_rules_reference) .
    
    6.  Select the methods that you want to allow on your external resources:
        
        1.  If you want to allow all methods, select **All methods** in the **Methods** list.
        2.  If you want to allow specific methods, select **Selected method** , click **Select methods** , and then select the methods that you want to allow on your external resources.
    
    7.  Click **Create perimeter** .

### Set up VPC Service Controls using the gcloud CLI

To set up VPC Service Controls using the gcloud CLI, follow these steps:

1.  [Set the default access policy](#set-default-policy) .
2.  [Create the egress policy input file](#create-egress-file) .
3.  [Add the egress policy](#add-egress-policy) .

#### Set the default access policy

An access policy is an organization-wide container for access levels and service perimeters. For information about setting a default access policy or getting an access policy name, see [Managing an access policy](/access-context-manager/docs/manage-access-policy#set-default) .

#### Create the egress policy input file

An egress rule block defines the allowed access from within a perimeter to resources outside of that perimeter. For external resources, the `  externalResources  ` property defines the external resource paths allowed access from within your VPC Service Controls perimeter.

Egress rules can be configured using a JSON file, or a YAML file. The following sample uses the `  .yaml  ` format:

``` text
- egressTo:
    operations:
    - serviceName: bigquery.googleapis.com
      methodSelectors:
      - method: "*"
      *OR*
      - permission: "externalResource.read"
    externalResources:
      - EXTERNAL_RESOURCE_PATH
  egressFrom:
    identityType: IDENTITY_TYPE
    *OR*
    identities:
    - serviceAccount:SERVICE_ACCOUNT
```

  - `  egressTo  ` : lists allowed service operations on Google Cloud resources in specified projects outside the perimeter.

  - `  operations  ` : list accessible services and actions or methods that a client satisfying the `  from  ` block conditions is allowed to access.

  - `  serviceName  ` : set `  bigquery.googleapis.com  ` for BigQuery Omni.

  - `  methodSelectors  ` : list methods that a client satisfying the `  from  ` conditions can access. For restrictable methods and permissions for services, see [Supported service method restrictions](/vpc-service-controls/docs/supported-method-restrictions) .

  - `  method  ` : a valid service method, or `  \"*\"  ` to allow all `  serviceName  ` methods.

  - `  permission  ` : a valid service permission, such as `  \"*\"  ` , `  externalResource.read  ` , or `  externalResource.write  ` . Access to resources outside the perimeter is allowed for operations that require this permission.

  - `  externalResources  ` : lists external resources that clients inside a perimeter can access. Replace EXTERNAL\_RESOURCE\_PATH with either a valid Amazon S3 bucket, such as `  s3://bucket_name  ` , or a Blob Storage container path, such as `  azure://myaccount.blob.core.windows.net/container_name  ` .

  - `  egressFrom  ` : lists allowed service operations on Google Cloud resources in specified projects within the perimeter.

  - `  identityType  ` or `  identities  ` : defines the identity types that can access the specified resources outside the perimeter. Replace IDENTITY\_TYPE with one of the following valid values:
    
      - `  ANY_IDENTITY  ` : to allow all identities.
      - `  ANY_USER_ACCOUNT  ` : to allow all users.
      - `  ANY_SERVICE_ACCOUNT  ` : to allow all service accounts

  - `  identities  ` : lists service accounts that can access the specified resources outside the perimeter.

  - `  serviceAccount  ` (optional): replace SERVICE\_ACCOUNT with the service account that can access the specified resources outside the perimeter.

#### Examples

The following example is a policy that allows egress operations from inside the perimeter to the `  s3://mybucket  ` Amazon S3 location in AWS.

``` text
- egressTo:
    operations:
    - serviceName: bigquery.googleapis.com
      methodSelectors:
      - method: "*"
    externalResources:
      - s3://mybucket
      - s3://mybucket2
  egressFrom:
    identityType: ANY_IDENTITY
```

The following example allows egress operations to a Blob Storage container:

``` text
- egressTo:
    operations:
    - serviceName: bigquery.googleapis.com
      methodSelectors:
      - method: "*"
    externalResources:
      - azure://myaccount.blob.core.windows.net/mycontainer
  egressFrom:
    identityType: ANY_IDENTITY
```

For more information about egress policies, see the [Egress rules reference](/vpc-service-controls/docs/ingress-egress-rules#egress-rules-reference) .

#### Add the egress policy

To add the egress policy when you create a new service perimeter, use the [`  gcloud access-context-manager perimeters create  ` command](/sdk/gcloud/reference/access-context-manager/perimeters/create) . For example, the following command creates a new perimeter named `  omniPerimeter  ` that includes the project with project number `  12345  ` , restricts the BigQuery API, and adds an egress policy defined in the `  egress.yaml  ` file:

``` text
gcloud access-context-manager perimeters create omniPerimeter \
    --title="Omni Perimeter" \
    --resources=projects/12345 \
    --restricted-services=bigquery.googleapis.com \
    --egress-policies=egress.yaml
```

To add the egress policy to an existing service perimeter, use the [`  gcloud access-context-manager perimeters update  ` command](/sdk/gcloud/reference/access-context-manager/perimeters/update) . For example, the following command adds an egress policy defined in the `  egress.yaml  ` file to an existing service perimeter named `  omniPerimeter  ` :

``` text
gcloud access-context-manager perimeters update omniPerimeter
    --set-egress-policies=egress.yaml
```

### Verify your perimeter

To verify the perimeter, use the [`  gcloud access-context-manager perimeters describe  ` command](/sdk/gcloud/reference/access-context-manager/perimeters/describe) :

``` text
gcloud access-context-manager perimeters describe PERIMETER_NAME
```

Replace PERIMETER\_NAME with the name of the perimeter.

For example, the following command describes the perimeter `  omniPerimeter  ` :

``` text
gcloud access-context-manager perimeters describe omniPerimeter
```

For more information, see [Managing service perimeters](/vpc-service-controls/docs/manage-service-perimeters#list-and-describe) .

## Allow BigQuery Omni VPC access to Amazon S3

As a BigQuery administrator, you can create an S3 bucket policy to grant BigQuery Omni access to your Amazon S3 resources. This ensures that only authorized BigQuery Omni VPCs can interact with your Amazon S3, enhancing the security of your data.

### Apply an S3 bucket policy for BigQuery Omni VPC

To apply an S3 bucket policy, use the AWS CLI or Terraform:

### AWS CLI

Run the following command to apply an S3 bucket policy that includes a condition using the `  aws:SourceVpc  ` attribute:

``` text
  aws s3api put-bucket-policy \
    --bucket=BUCKET_NAME \
    --policy "{
      \"Version\": \"2012-10-17\",
      \"Id\": \"RestrictBucketReads\",
      \"Statement\": [
          {
              \"Sid\": \"AccessOnlyToOmniVPC\",
              \"Principal\": \"*\",
              \"Action\": [\"s3:ListBucket\", \"s3:GetObject\"],
              \"Effect\": \"Allow\",
              \"Resource\": [\"arn:aws:s3:::BUCKET_NAME\",
                             \"arn:aws:s3:::BUCKET_NAME/*\"],
              \"Condition\": {
                  \"StringEquals\": {
                    \"aws:SourceVpc\": \"VPC_ID\"
                  }
              }
          }
      ]
    }"
```

Replace the following:

  - `  BUCKET_NAME  ` : the Amazon S3 bucket that you want BigQuery to access.
  - `  VPC_ID  ` : the BigQuery Omni VPC ID of the BigQuery Omni region collocated with the Amazon S3 bucket. You can find this information in the table on this page.

### Terraform

Add the following to your Terraform configuration file:

``` text
  resource "aws_s3_bucket" "example" {
    bucket = "BUCKET_NAME"
  }

  resource "aws_s3_bucket_policy" "example" {
    bucket = aws_s3_bucket.example.id
    policy = jsonencode({
      Version = "2012-10-17"
      Id      = "RestrictBucketReads"
      Statement = [
          {
              Sid       = "AccessOnlyToOmniVPC"
              Effect    = "Allow"
              Principal = "*"
              Action    = ["s3:GetObject", "s3:ListBucket"]
              Resource  = [
                  aws_s3_bucket.example.arn,
                  "${aws_s3_bucket.example.arn}/*"
                  ]
              Condition = {
                  StringEquals = {
                      "aws:SourceVpc": "VPC_ID"
                  }
              }
          },
      ]
    })
  }
```

Replace the following:

  - `  BUCKET_NAME  ` : the Amazon S3 bucket that you want BigQuery to access.
  - `  VPC_ID  ` : the BigQuery Omni VPC ID of the BigQuery Omni region collocated with the Amazon S3 bucket.

### BigQuery Omni VPC Resource IDs

<table>
<thead>
<tr class="header">
<th><strong>Region</strong></th>
<th><strong>VPC ID</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>aws-ap-northeast-2</td>
<td>vpc-0b488548024288af2</td>
</tr>
<tr class="even">
<td>aws-ap-southeast-2</td>
<td>vpc-0726e08afef3667ca</td>
</tr>
<tr class="odd">
<td>aws-eu-central-1</td>
<td>vpc-05c7bba12ad45558f</td>
</tr>
<tr class="even">
<td>aws-eu-west-1</td>
<td>vpc-0e5c646979bbe73a0</td>
</tr>
<tr class="odd">
<td>aws-us-east-1</td>
<td>vpc-0bf63a2e71287dace</td>
</tr>
<tr class="even">
<td>aws-us-west-2</td>
<td>vpc-0cc24e567b9d2c1cb</td>
</tr>
</tbody>
</table>

## Limitations

For a full list of limitations that apply to BigLake tables based on Amazon S3 and Blob Storage, see [Limitations](/bigquery/docs/omni-introduction#limitations) .

## What's next

  - Learn about [BigQuery Omni](/bigquery/docs/omni-introduction) .
  - Use the [BigQuery Omni with AWS lab](https://www.cloudskillsboost.google/catalog_lab/5345) .
  - Learn about [BigLake tables](/bigquery/docs/biglake-intro) .
  - Learn how to [export query results to Amazon S3](/bigquery/docs/omni-aws-export-results-to-s3) .
  - Learn how to create [materialized views over Amazon Simple Storage Service (Amazon S3) metadata cache-enabled tables](/bigquery/docs/materialized-views-intro#biglake) .
  - Learn how to make Amazon S3 data in a materialized view available locally for joins by [creating a replica of the materialized view](/bigquery/docs/load-data-using-cross-cloud-transfer#materialized_view_replicas) .
