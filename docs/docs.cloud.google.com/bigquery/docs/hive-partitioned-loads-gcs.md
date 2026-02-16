# Loading externally partitioned data

BigQuery can load data that is stored in Cloud Storage using a Hive partitioning layout. *Hive partitioning* means that the external data is organized into multiple files, with a naming convention to separate files into different partitions. For more information, see [Supported data layouts](#supported_data_layouts) .

By default, the data is not partitioned in BigQuery after you load it, unless you explicitly create a [partitioned table](/bigquery/docs/partitioned-tables) .

## Load Hive partitioned data

To load Hive partitioned data, choose one of the following options:

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
4.  For **Table type** , select **Native table** .

In the **Schema** section, enter the [schema](/bigquery/docs/schemas) definition.

To enable the [auto detection](/bigquery/docs/schema-detect) of schema, select **Auto detect** .

To ignore rows with extra column values that do not match the schema, expand the **Advanced options** section and select **Unknown values** .

Click **Create table** .

### SQL

To create an externally partitioned table, use the `  WITH PARTITION COLUMNS  ` clause of the [`  LOAD DATA  ` statement](/bigquery/docs/reference/standard-sql/load-statements#load_data_statement) to specify the partition schema details.

For an example, see [Load a file that is externally partitioned](/bigquery/docs/reference/standard-sql/load-statements#load_a_file_that_is_externally_partitioned) .

### bq

Load Hive partitioned data using automatic partition key type detection:

``` text
bq load --source_format=ORC --hive_partitioning_mode=AUTO \
--hive_partitioning_source_uri_prefix=gcs_uri_shared_prefix \
dataset.table gcs_uris
```

Load Hive partitioned data using string-typed partition key detection:

``` text
bq load --source_format=CSV --autodetect \
--hive_partitioning_mode=STRINGS \
--hive_partitioning_source_uri_prefix=gcs_uri_shared_prefix \
dataset.table gcs_uris
```

Load Hive partitioned data using a custom partition key schema that is encoded using the `  source\_uri\_prefix  ` field:

``` text
bq load --source_format=JSON --hive_partitioning_mode=CUSTOM \
--hive_partitioning_source_uri_prefix=gcs_uri_shared_prefix/partition_key_schema \
dataset.table gcs_uris file_schema
```

The partition key schema is encoded immediately following the source URI prefix. Use the following format to specify `  --hive_partitioning_source_uri_prefix  ` :

``` text
--hive_partitioning_source_uri_prefix=gcs_uri_shared_prefix/{key1:TYPE1}/{key2:TYPE2}/{key3:TYPE3}
```

### API

Support for Hive partitioning exists by setting the [`  HivePartitioningOptions  `](/bigquery/docs/reference/rest/v2/tables#hivepartitioningoptions) on the [`  JobConfigurationLoad  `](/bigquery/docs/reference/rest/v2/Job#jobconfigurationload) .

**Note:** When `  hivePartitioningOptions.mode  ` is set to `  CUSTOM  ` , you must encode the partition key schema in the `  hivePartitioningOptions.sourceUriPrefix  ` field as follows: `  gs:// BUCKET / PATH_TO_TABLE /{ KEY1 : TYPE1 }/{ KEY2 : TYPE2 }/...  `

## Perform incremental loads

Consider the following data layout:

``` text
gs://my_bucket/my_table/dt=2019-10-31/val=1/file1
gs://my_bucket/my_table/dt=2018-10-31/val=2/file2
gs://my_bucket/my_table/dt=2017-10-31/val=3/file3
gs://my_bucket/my_table/dt=2016-10-31/val=4/file4
```

To load only data from 2019-10-31, do the following:

  - Set the [Hive partitioning mode](/bigquery/docs/hive-partitioned-queries-gcs#partition_schema_detection_modes) to `  AUTO  ` , `  STRINGS  ` , or `  CUSTOM  ` .
  - Set the source URI prefix to `  gs://my_bucket/my_table/  ` for `  AUTO  ` or `  STRINGS  ` Hive partitioning modes. For CUSTOM, provide `  gs://my_bucket/my_table/{dt:DATE}/{val:INTEGER}  ` .
  - Use the URI `  gs://my_bucket/my_table/dt=2019-10-31/*  ` .
  - Data is loaded with `  dt  ` and `  val  ` columns included, with values `  2019-10-31  ` and `  1  ` , respectively.

To load only data from specific files, do the following:

  - Set the [Hive partitioning mode](/bigquery/docs/hive-partitioned-queries-gcs#partition_schema_detection_modes) to `  AUTO  ` , `  STRINGS  ` , or `  CUSTOM  ` .
  - Set the source URI prefix to `  gs://my_bucket/my_table/  ` for `  AUTO  ` or `  STRINGS  ` Hive partitioning modes. For `  CUSTOM  ` , provide `  gs://my_bucket/my_table/{dt:DATE}/{val:INTEGER}  ` .
  - Use the URIs `  gs://my_bucket/my_table/dt=2017-10-31/val=3/file3,gs://my_bucket/my_table/dt=2016-10-31/val=4/file4  ` .
  - Data is loaded from both files with the `  dt  ` and `  val  ` columns filled in.

## Partition schema

The following sections explain the [default Hive partitioned layout](#supported_data_layouts) and the [schema detection modes](#detection_modes) that BigQuery supports.

### Supported data layouts

Hive partition keys appear as normal columns when you query data from Cloud Storage. The data must follow a default Hive partitioned layout. For example, the following files follow the default layout—the key-value pairs are configured as directories with an equal sign (=) as a separator, and the partition keys are always in the same order:

``` text
gs://my_bucket/my_table/dt=2019-10-31/lang=en/my_filename
gs://my_bucket/my_table/dt=2018-10-31/lang=fr/my_filename
```

The common source URI prefix in this example is `  gs://my_bucket/my_table  ` .

### Unsupported data layouts

If the partition key names are not encoded in the directory path, partition schema detection fails. For example, consider the following path, which does not encode the partition key names:

``` text
gs://my_bucket/my_table/2019-10-31/en/my_filename
```

Files where the schema is not in a consistent order also fail detection. For example, consider the following two files with inverted partition key encodings:

``` text
gs://my_bucket/my_table/dt=2019-10-31/lang=en/my_filename
gs://my_bucket/my_table/lang=fr/dt=2018-10-31/my_filename
```

### Detection modes

BigQuery supports three modes of Hive partition schema detection:

  - `  AUTO  ` : Key names and types are automatically detected. The following types can be detected:
    
      - [STRING](/bigquery/docs/reference/standard-sql/data-types#string_type)
    
      - [INTEGER](/bigquery/docs/reference/standard-sql/data-types#integer_types)
    
      - [DATE](/bigquery/docs/reference/standard-sql/data-types#date_type)
        
        For example, `  /date=2018-10-18/  ` .
    
      - [TIMESTAMP](/bigquery/docs/reference/standard-sql/data-types#timestamp_type)
        
        For example, `  /time=2018-10-18 16:00:00+00/  ` .

  - `  STRINGS  ` : Key names are automatically converted to `  STRING  ` type.

  - `  CUSTOM  ` : Partition key schema is encoded as specified in the source URI prefix.

#### Custom partition key schema

To use a `  CUSTOM  ` schema, you must specify the schema in the source URI prefix field. Using a `  CUSTOM  ` schema lets you specify the type for each partition key. The values must validly parse as the specified type or the query fails.

For example, if you set the `  source_uri_prefix  ` flag to `  gs://my_bucket/my_table/{dt:DATE}/{val:STRING}  ` , BigQuery treats `  val  ` as a STRING, `  dt  ` as a DATE, and uses `  gs://my_bucket/my_table  ` as the source URI prefix for the matched files.

## Limitations

  - Hive partitioning support is built assuming a common source URI prefix for all URIs that ends immediately before partition encoding, as follows: `  gs:// BUCKET / PATH_TO_TABLE /  ` .

  - The directory structure of a Hive partitioned table is assumed to have the same partitioning keys appear in the same order, with a maximum of ten partition keys per table.

  - The data must follow a [default Hive partitioning layout](#supported_data_layouts) .

  - The Hive partitioning keys and the columns in the underlying files cannot overlap.

  - Support is for [GoogleSQL](/bigquery/docs/reference/standard-sql/query-syntax) only.

  - All [limitations for loading from Cloud Storage](/bigquery/docs/batch-loading-data#limitations) apply.

## What's next

  - Learn about [partitioned tables](/bigquery/docs/partitioned-tables) .
  - Learn how to [use SQL in BigQuery](/bigquery/docs/introduction-sql) .
