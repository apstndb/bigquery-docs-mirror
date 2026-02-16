# Use externally partitioned data

**Important:** The term "BigLake" on this page refers to an access delegation functionality for external tables in BigQuery. For information about BigLake, the stand-alone Google Cloud product that includes BigLake metastore, the Apache Iceberg REST catalog, and BigLake tables for Apache Iceberg see [BigLake overview](/biglake/docs/introduction) .

You can use BigQuery external tables to query partitioned data in the following data stores:

  - [Cloud Storage](/bigquery/docs/create-cloud-storage-table-biglake#create-biglake-partitioned-data)
  - [Amazon Simple Storage Service (Amazon S3)](/bigquery/docs/omni-aws-create-external-table#create-biglake-table-partitioned)
  - [Azure Blob Storage](/bigquery/docs/omni-azure-create-external-table#create-biglake-table-partitioned)

The external partitioned data must use a [default Hive partitioning layout](#supported_data_layouts) and be in one of the following formats:

  - Avro
  - CSV
  - JSON
  - ORC
  - Parquet

To query externally partitioned data, you must create a [BigLake table](/bigquery/docs/create-cloud-storage-table-biglake) or an [external table](/bigquery/docs/external-data-cloud-storage#create-external-table-partitioned) . We recommend using BigLake tables because they let you enforce fine-grained security at the table level. For information about BigLake and external tables, see [Introduction to BigLake tables](/bigquery/docs/biglake-intro) and [Introduction to external tables](/bigquery/docs/external-tables) .

You enable Hive partitioning support by setting the appropriate options in the [table definition file](/bigquery/docs/external-table-definition#create_a_definition_file_for_hive-partitioned_data) . For instructions about querying managed partitioned tables, see [Introduction to partitioned tables](/bigquery/docs/partitioned-tables) .

## Partition schema

The following sections explain the [default Hive partitioned layout](#supported_data_layouts) and the [schema detection modes](#detection_modes) that BigQuery supports.

To avoid reading unnecessary files and to improve performance, you can use [predicate filters on partition keys in queries](#partition_pruning) .

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

### Partition pruning

BigQuery prunes partitions when possible using query predicates on the partition keys. This lets BigQuery avoid reading unnecessary files, which helps improve performance.

### Predicate filters on partition keys in queries

When you create an externally partitioned table, you can require the use of predicate filters on partition keys by enabling the `  requirePartitionFilter  ` option under [HivePartitioningOptions](/bigquery/docs/reference/rest/v2/tables#hivepartitioningoptions) .

When this option is enabled, attempts to query the externally partitioned table without specifying a `  WHERE  ` clause produce the following error: `  Cannot query over table <table_name> without a filter over column(s) <partition key names> that can be used for partition elimination  ` .

**Note:** There must be at least one predicate that only references one or more partition keys for the filter to be considered eligible for partition elimination. For example, for a table with partition key `  val  ` and column `  f  ` in the file, both of the following `  WHERE  ` clauses satisfy the requirement:  
`  WHERE val = "key"  `  
`  WHERE val = "key" AND f = "column"  `

However, `  WHERE (val = "key" OR f = "column")  ` is not sufficient.

## Limitations

  - Hive partitioning support is built assuming a common source URI prefix for all URIs that ends immediately before partition encoding, as follows: `  gs:// BUCKET / PATH_TO_TABLE /  ` .

  - The directory structure of a Hive partitioned table is assumed to have the same partitioning keys appear in the same order, with a maximum of ten partition keys per table.

  - The data must follow a [default Hive partitioning layout](#supported_data_layouts) .

  - The Hive partitioning keys and the columns in the underlying files cannot overlap.

  - Support is for [GoogleSQL](/bigquery/docs/reference/standard-sql/query-syntax) only.

  - All [limitations](/bigquery/external-data-sources#external_data_source_limitations) for querying external data sources stored on Cloud Storage apply.

## What's next

  - Learn about [partitioned tables](/bigquery/docs/partitioned-tables) .
  - Learn how to [use SQL in BigQuery](/bigquery/docs/introduction-sql) .
