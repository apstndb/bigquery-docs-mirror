---
name: documents/docs.cloud.google.com/bigquery/docs/reference/standard-sql/load-statements
uri: https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/load-statements
title: Load statements in GoogleSQL
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# Load statements in GoogleSQL

## `LOAD DATA` statement

Loads data from one or more files into a table. The statement can create a new table, append data into an existing table or partition, or overwrite an existing table or partition. If the `LOAD DATA` statement fails, the table into which you are loading data remains unchanged.

### Syntax

```
LOAD DATA {OVERWRITE|INTO}  [{TEMP|TEMPORARY} TABLE]
[[project_name.]dataset_name.]table_name
[(
  column_list
)]
[[OVERWRITE] PARTITIONS (partition_column_name=partition_value)]
[PARTITION BY partition_expression]
[CLUSTER BY clustering_column_list]
[OPTIONS (table_option_list)]
FROM FILES(load_option_list)
[WITH PARTITION COLUMNS
  [(partition_column_list)]
]
[WITH CONNECTION connection_name]

column_list: column[, ...]

partition_column_list: partition_column_name, partition_column_type[, ...]
```

### Arguments

- `INTO` : If a table with this name already exists, the statement appends data to the table. You must use `INTO` instead of `OVERWRITE` if your statement includes the `PARTITIONS` clause.

- `OVERWRITE` : If a table with this name already exists, the statement overwrites the table.

- `{TEMP|TEMPORARY} TABLE` : Use this clause to create or write to a temporary table.

- `project_name` : The name of the project for the table. The value defaults to the project that runs this DDL query.

- `dataset_name` : The name of the dataset for the table.

- `table_name` : The name of the table.

- `column_list` : Contains the table's schema information as a list of table columns. For more information about table schemas, see [Specifying a schema](https://docs.cloud.google.com/bigquery/docs/schemas) . If you don't specify a schema, BigQuery uses [schema auto-detection](https://docs.cloud.google.com/bigquery/docs/schema-detect) to infer the schema.

  When you load hive-partitioned data into a new table or overwrite an existing table, then that table schema contains the hive-partitioned columns and the columns in the `column_list` .

  If you append hive-partitioned data to an existing table, then the hive-partitioned columns and `column_list` can be a subset of the existing columns. If the combined list of columns in not a subset of the existing columns, then the following rules apply:

  - If your data is self-describing, such as ORC, PARQUET, or AVRO, then columns in the source file that are omitted from the `column_list` are ignored. Columns in the `column_list` that don't exist in the source file are written with `NULL` values. If a column is in the `column_list` and the source file, then their types must match.

  - If your data is not self-describing, such as CSV or JSON, then columns in the source file that are omitted from the `column_list` are only ignored if you set `ignore_unknown_values` to `TRUE` . Otherwise this statement returns an error. You can't list columns in the `column_list` that don't exist in the source file.

- `[OVERWRITE] PARTITIONS` : Use this clause to write to or overwrite exactly one partition. When you use this clause, the statement must begin with `LOAD DATA INTO` .

- `partition_column_name` : The name of the partitioned column to write to. If you use both the `PARTITIONS` and the `PARTITION BY` clauses, then the column names must match.

- `partition_value` : The `partition_id` of the partition to append or overwrite. To find the `partition_id` values of a table, query the [`INFORMATION_SCHEMA.PARTITIONS` view](https://docs.cloud.google.com/bigquery/docs/information-schema-partitions) . You can't set the `partition_value` to `__NULL__` or `__UNPARTITIONED__` . You can only append to or overwrite one partition. If your data contains values that belong to multiple partitions, then the statement fails with an error. This `partition_value` must be literal value.

- `partition_expression` : Specifies the table partitioning when creating a new table.

- `clustering_column_list` : Specifies table clustering when creating a new table. The value is a comma-separated list of column names, with up to four columns.

- [`table_option_list`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/load-statements#table_option_list) : Specifies options for creating the table. If you include this clause and the table already exists, then the options must match the existing table specification.

- `partition_column_list` : A list of external partitioning columns.

- `connection_name` : The connection name that is used to read the source files from an [external data source](https://docs.cloud.google.com/bigquery/external-data-sources) .

- [`load_option_list`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/load-statements#load_option_list) : Specifies options for loading the data.

If no table exists with the specified name, then the statement creates a new table. If a table already exists with the specified name, then the behavior depends on the `INTO` or `OVERWRITE` keyword. The `INTO` keyword appends the data to the table, and the `OVERWRITE` keyword overwrites the table.

If your external data uses a [hive-partitioned layout](https://docs.cloud.google.com/bigquery/docs/hive-partitioned-queries-gcs#supported_data_layouts) , then include the `WITH PARTITION COLUMNS` clause. If you include the `WITH PARTITION COLUMNS` clause without `partition_column_list` , then BigQuery infers the partitioning from the data layout. If you include both `column_list` and `WITH PARTITION COLUMNS` , then `partition_column_list` is required.

You can't use the `LOAD DATA` statement to load data into a temporary table.

### `column`

`(column_name column_schema[, ...])` contains the table's schema information in a comma-separated list.

> **Note:** Constraints cannot be specified on `ARRAY` or `STRUCT` elements.

```
column :=
  column_name column_schema

column_schema :=
   {
     simple_type
     | STRUCT<field_list>
     | ARRAY<array_element_schema>
   }
   [PRIMARY KEY NOT ENFORCED | REFERENCES table_name(column_name) NOT ENFORCED]
   [ DEFAULT default_expression |
     embedding_generation |
     identity_column ]
   [NOT NULL]
   [OPTIONS(column_option_list)]

simple_type :=
  { data_type | STRING COLLATE collate_specification }

field_list :=
  field_name column_schema [, ...]

array_element_schema :=
  { simple_type | STRUCT<field_list> }
  [NOT NULL]

embedding_generation :=
  GENERATED ALWAYS AS (generation_expression) STORED OPTIONS(generation_option_list)

identity_column :=
  [ GENERATED { ALWAYS | BY DEFAULT } ] AS IDENTITY (
    [ START WITH start_value ]
    [ INCREMENT BY increment_value ])
```

- [`column_name`](https://docs.cloud.google.com/bigquery/docs/schemas#column_names) is the name of the column. A column name:

  - Must contain only letters (a-z, A-Z), numbers (0-9), or underscores (\_)
  - Must start with a letter or underscore
  - Can be up to 300 characters

- `column_schema` : Similar to a [data type](https://docs.cloud.google.com/bigquery/docs/schemas#standard_sql_data_types) , but supports an optional `NOT NULL` constraint for types other than `ARRAY` . `column_schema` also supports options on top-level columns and `STRUCT` fields.

  `column_schema` can be used only in the column definition list of `CREATE TABLE` statements. It cannot be used as a type in expressions.

- `simple_type` : Any [supported data type](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-types) aside from `STRUCT` and `ARRAY` .

  If `simple_type` is a `STRING` , it supports an additional clause for [collation](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/collation-concepts#collate_spec_details) , which defines how a resulting `STRING` can be compared and sorted. The syntax looks like this:

  ```
  STRING COLLATE collate_specification
  ```

  If you have `DEFAULT COLLATE collate_specification` assigned to the table, the collation specification for a column overrides the specification for the table.

- `default_expression` : The [default value](https://docs.cloud.google.com/bigquery/docs/default-values) assigned to the column. You cannot specify `DEFAULT` if `GENERATED ALWAYS AS` is specified.

- `field_list` : Represents the fields in a struct.

- `field_name` : The name of the struct field. Struct field names have the same restrictions as column names.

- `NOT NULL` : When the `NOT NULL` constraint is present for a column or field, the column or field is created with `REQUIRED` mode. Conversely, when the `NOT NULL` constraint is absent, the column or field is created with `NULLABLE` mode.

  Columns and fields of `ARRAY` type do not support the `NOT NULL` modifier. For example, a `column_schema` of `ARRAY<INT64> NOT NULL` is invalid, since `ARRAY` columns have `REPEATED` mode and can be empty but cannot be `NULL` . An array element in a table can never be `NULL` , regardless of whether the `NOT NULL` constraint is specified. For example, `ARRAY<INT64>` is equivalent to `ARRAY<INT64 NOT NULL>` .

  The `NOT NULL` attribute of a table's `column_schema` does not propagate through queries over the table. If table `T` contains a column declared as `x INT64 NOT NULL` , for example, `CREATE TABLE dataset.newtable AS SELECT x FROM T` creates a table named `dataset.newtable` in which `x` is `NULLABLE` .

- `generation_expression` : ( [Preview](https://cloud.google.com/products#product-launch-stages) ) An expression for an automatically generated embedding column. Setting this field enables [autonomous embedding generation](https://docs.cloud.google.com/bigquery/docs/autonomous-embedding-generation) on the table. The only supported `generation_expression` syntax is a call to the [`AI.EMBED` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-embed) .

  - You can't specify `GENERATED ALWAYS AS` if `DEFAULT` is specified.
  - The `connection_id` argument to `AI.EMBED` is required when used in a generation expression.
  - The type of the column must be `STRUCT<result ARRAY<FLOAT64>, status STRING>` .

- `generation_option_list` : The options for a generated column. The only supported option is `asynchronous = TRUE` .

- `ALWAYS` : The [identity column](https://docs.cloud.google.com/bigquery/docs/identity-columns) can only have generated values. You can't manually insert values into the column. This mode is the default mode.

- `BY DEFAULT` : You can manually insert values into the [identity column](https://docs.cloud.google.com/bigquery/docs/identity-columns) . If you add a row to the table and don't specify a value for the column, or specify a `NULL` value, then a generated value is used.

- `start_value` : An `INT64` literal that contains the first generated value to use for the identity column. The default value is 1.

- `increment_value` : An `INT64` value other than 0 that contains the minimum difference between successive values generated for the identity column. Some values might be skipped. The difference between successive generated values is always a multiple of the `increment_value` . For example, if your starting value is 1 and your increment is 2, then the generated values can only include odd numbers. The default value is 1.

### `column_option_list`

Specify a column option list in the following format:

`NAME=VALUE, ...`

`NAME` and `VALUE` must be one of the following combinations:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><code>NAME</code></th>
<th><code>VALUE</code></th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>description</code></td>
<td><p><code>STRING</code></p></td>
<td><p>Example: <code>description="a unique id"</code></p>
<p>This property is equivalent to the <a href="https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/tables#TableFieldSchema.FIELDS.description">schema.fields[].description</a> table resource property.</p></td>
</tr>
<tr class="even">
<td><code>rounding_mode</code></td>
<td><p><code>STRING</code></p></td>
<td><p>Example: <code>rounding_mode = "ROUND_HALF_EVEN"</code></p>
<p>This specifies the <a href="https://docs.cloud.google.com/bigquery/docs/schemas#rounding_mode">rounding mode</a> that's used for values written to a <code>NUMERIC</code> or <code>BIGNUMERIC</code> type column or <code>STRUCT</code> field. The following values are supported:</p>
<ul>
<li><code>"ROUND_HALF_AWAY_FROM_ZERO"</code> : Halfway cases are rounded away from zero. For example, 2.25 is rounded to 2.3, and -2.25 is rounded to -2.3.</li>
<li><code>"ROUND_HALF_EVEN"</code> : Halfway cases are rounded towards the nearest even digit. For example, 2.25 is rounded to 2.2 and -2.25 is rounded to -2.2.</li>
</ul>
<p>This property is equivalent to the <a href="https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/tables#TableFieldSchema.FIELDS.rounding_mode"><code>roundingMode</code></a> table resource property.</p></td>
</tr>
<tr class="odd">
<td><code>data_policies</code></td>
<td><code>ARRAY&lt;STRING&gt;</code></td>
<td><p>Applies a <a href="https://docs.cloud.google.com/bigquery/docs/column-data-masking#create_data_policies">data policy</a> to a column in a table.</p>
<p>Example: <code>data_policies = ["{'name':'myproject.region-us.data_policy_name1'}", "{'name':'myproject.region-us.data_policy_name2'}"]</code></p>
<p>The <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#alter_column_set_data_type_statement"><code>ALTER TABLE ALTER COLUMN</code></a> statement supports the <code>=</code> and <code>+=</code> operators to add data policies to a specific column.</p>
<p>Example: <code>data_policies +=["data_policy1", "data_policy2"]</code></p></td>
</tr>
<tr class="even">
<td><code>data_governance_tags</code></td>
<td><code>ARRAY&lt;STRUCT&lt;STRING, STRING&gt;&gt;</code></td>
<td><p>Applies <a href="https://docs.cloud.google.com/bigquery/docs/tags#data-governance-tags">data governance tags</a> to a column in a table.</p>
<p>Example: <code>data_governance_tags = [("myproject/tag_key", "tag_value")]</code></p></td>
</tr>
</tbody>
</table>

`VALUE` is a constant expression containing only literals, query parameters, and scalar functions.

The constant expression **cannot** contain:

- A reference to a table
- Subqueries or SQL statements such as `SELECT` , `CREATE` , or `UPDATE`
- User-defined functions, aggregate functions, or analytic functions
- The following scalar functions:
  - `ARRAY_TO_STRING`
  - `REPLACE`
  - `REGEXP_REPLACE`
  - `RAND`
  - `FORMAT`
  - `LPAD`
  - `RPAD`
  - `REPEAT`
  - `SESSION_USER`
  - `GENERATE_ARRAY`
  - `GENERATE_DATE_ARRAY`

Setting the `VALUE` replaces the existing value of that option for the column, if there was one. Setting the `VALUE` to `NULL` clears the column's value for that option.

### `partition_expression`

`PARTITION BY` is an optional clause that controls [table](https://docs.cloud.google.com/bigquery/docs/partitioned-tables) and [vector index](https://docs.cloud.google.com/bigquery/docs/vector-index#partitions) partitioning. `partition_expression` is an expression that determines how to partition the table or vector index. The partition expression can contain the following values:

- `_PARTITIONDATE` . Partition by ingestion time with daily partitions. This syntax cannot be used with the `AS query_statement` clause.

- `DATE(_PARTITIONTIME)` . Equivalent to `_PARTITIONDATE` . This syntax cannot be used with the `AS query_statement` clause.

- `<date_column>` . Partition by a `DATE` column with daily partitions.

- `DATE({ <timestamp_column> | <datetime_column> })` . Partition by a `TIMESTAMP` or `DATETIME` column with daily partitions.

- `DATETIME_TRUNC(<datetime_column>, { DAY | HOUR | MONTH | YEAR })` . Partition by a `DATETIME` column with the specified partitioning type.

- `TIMESTAMP_TRUNC(<timestamp_column>, { DAY | HOUR | MONTH | YEAR })` . Partition by a `TIMESTAMP` column with the specified partitioning type.

- `TIMESTAMP_TRUNC(_PARTITIONTIME, { DAY | HOUR | MONTH | YEAR })` . Partition by ingestion time with the specified partitioning type. This syntax cannot be used with the `AS query_statement` clause.

- `DATE_TRUNC(<date_column>, { MONTH | YEAR })` . Partition by a `DATE` column with the specified partitioning type.

- `RANGE_BUCKET(<int64_column>, GENERATE_ARRAY(<start>, <end>[, <interval>]))` . Partition by an integer column with the specified range, where:

  - `start` is the start of range partitioning, inclusive.
  - `end` is the end of range partitioning, exclusive.
  - `interval` is the width of each range within the partition. Defaults to 1.

### `table_option_list`

The option list lets you set table options such as a [label](https://docs.cloud.google.com/bigquery/docs/labels) and an expiration time. You can include multiple options using a comma-separated list.

Specify a table option list in the following format:

`NAME=VALUE, ...`

`NAME` and `VALUE` must be one of the following combinations:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><code>NAME</code></th>
<th><code>VALUE</code></th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>expiration_timestamp</code></td>
<td><code>TIMESTAMP</code></td>
<td><p>Example: <code>expiration_timestamp=TIMESTAMP "2025-01-01 00:00:00 UTC"</code></p>
<p>This property is equivalent to the <a href="https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.expiration_time">expirationTime</a> table resource property.</p></td>
</tr>
<tr class="even">
<td><code>partition_expiration_days</code></td>
<td><p><code>FLOAT64</code></p></td>
<td><p>Example: <code>partition_expiration_days=7</code></p>
<p>Sets the partition expiration in days. For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/managing-partitioned-tables#partition-expiration">Set the partition expiration</a> . By default, partitions don't expire.</p>
<p>This property is equivalent to the <a href="https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/tables#TimePartitioning.FIELDS.expiration_ms">timePartitioning.expirationMs</a> table resource property but uses days instead of milliseconds. One day is equivalent to 86400000 milliseconds, or 24 hours.</p>
<p>This property can only be set if the table is partitioned.</p></td>
</tr>
<tr class="odd">
<td><code>require_partition_filter</code></td>
<td><p><code>BOOL</code></p></td>
<td><p>Example: <code>require_partition_filter=true</code></p>
<p>Specifies whether queries on this table must include a predicate filter that filters on the partitioning column. For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/managing-partitioned-tables#require-filter">Set partition filter requirements</a> . The default value is <code>false</code> .</p>
<p>This property is equivalent to the <a href="https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/tables#TimePartitioning.FIELDS.require_partition_filter">timePartitioning.requirePartitionFilter</a> table resource property.</p>
<p>This property can only be set if the table is partitioned.</p></td>
</tr>
<tr class="even">
<td><code>friendly_name</code></td>
<td><p><code>STRING</code></p></td>
<td><p>Example: <code>friendly_name="my_table"</code></p>
<p>This property is equivalent to the <a href="https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.friendly_name">friendlyName</a> table resource property.</p></td>
</tr>
<tr class="odd">
<td><code>description</code></td>
<td><p><code>STRING</code></p></td>
<td><p>Example: <code>description="a table that expires in 2025"</code></p>
<p>This property is equivalent to the <a href="https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.description">description</a> table resource property.</p></td>
</tr>
<tr class="even">
<td><code>labels</code></td>
<td><p><code>ARRAY&lt;STRUCT&lt;STRING, STRING&gt;&gt;</code></p></td>
<td><p>Example: <code>labels=[("org_unit", "development")]</code></p>
<p>This property is equivalent to the <a href="https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.labels">labels</a> table resource property.</p></td>
</tr>
<tr class="odd">
<td><code>default_rounding_mode</code></td>
<td><p><code>STRING</code></p></td>
<td><p>Example: <code>default_rounding_mode = "ROUND_HALF_EVEN"</code></p>
<p>This specifies the default <a href="https://docs.cloud.google.com/bigquery/docs/schemas#rounding_mode">rounding mode</a> that's used for values written to any new <code>NUMERIC</code> or <code>BIGNUMERIC</code> type columns or <code>STRUCT</code> fields in the table. It does not impact existing fields in the table. The following values are supported:</p>
<ul>
<li><code>"ROUND_HALF_AWAY_FROM_ZERO"</code> : Halfway cases are rounded away from zero. For example, 2.5 is rounded to 3.0, and -2.5 is rounded to -3.</li>
<li><code>"ROUND_HALF_EVEN"</code> : Halfway cases are rounded towards the nearest even digit. For example, 2.5 is rounded to 2.0 and -2.5 is rounded to -2.0.</li>
</ul>
<p>This property is equivalent to the <a href="https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.default_rounding_mode"><code>defaultRoundingMode</code></a> table resource property.</p></td>
</tr>
<tr class="even">
<td><code>enable_change_history</code></td>
<td><p><code>BOOL</code></p></td>
<td><p>Example: <code>enable_change_history=TRUE</code></p>
<p>Set this property to <code>TRUE</code> in order to capture <a href="https://docs.cloud.google.com/bigquery/docs/change-history">change history</a> on the table, which you can then view by using the <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/time-series-functions#changes"><code>CHANGES</code> function</a> . Enabling this table option has an impact on costs; for more information see <a href="https://docs.cloud.google.com/bigquery/docs/change-history#pricing_and_costs">Pricing and costs</a> . The default is <code>FALSE</code> .</p></td>
</tr>
<tr class="odd">
<td><code>max_staleness</code></td>
<td><p><code>INTERVAL</code></p></td>
<td><p>Example: <code>max_staleness=INTERVAL "4:0:0" HOUR TO SECOND</code></p>
<p>The maximum interval behind the current time where it's acceptable to read stale data. For example, with <a href="https://docs.cloud.google.com/bigquery/docs/change-data-capture">change data capture</a> , when this option is set, the table copy operation is denied if data is more stale than the <code>max_staleness</code> value.</p>
<p><code>max_staleness</code> is disabled by default.</p></td>
</tr>
<tr class="even">
<td><code>enable_fine_grained_mutations</code></td>
<td><p><code>BOOL</code></p></td>
<td><p>In <a href="https://cloud.google.com/products/#product-launch-stages">preview</a> .</p>
<p>Example: <code>enable_fine_grained_mutations=TRUE</code></p>
<p>Set this property to <code>TRUE</code> to enable <a href="https://docs.cloud.google.com/bigquery/docs/data-manipulation-language#fine-grained_dml">fine-grained DML optimization</a> on the table. The default is <code>FALSE</code> .</p></td>
</tr>
<tr class="odd">
<td><code>storage_uri</code></td>
<td><p><code>STRING</code></p></td>
<td><p>In <a href="https://cloud.google.com/products/#product-launch-stages">preview</a> .</p>
<p>Example: <code>storage_uri= </code><var translate="no"> gs: </var><code> // </code><var translate="no"> BUCKET_DIRECTORY </var><code> / </code><var translate="no"> TABLE_DIRECTORY </var><code> /</code></p>
<p>A fully qualified location prefix for the external folder where data is stored. Supports <code>gs:</code> buckets.</p>
<p>Required for <a href="https://docs.cloud.google.com/bigquery/docs/managed-tables">managed tables</a> .</p></td>
</tr>
<tr class="even">
<td><code>file_format</code></td>
<td><p><code>STRING</code></p></td>
<td><p>In <a href="https://cloud.google.com/products/#product-launch-stages">preview</a> .</p>
<p>Example: <code>file_format=PARQUET</code></p>
<p>The open-source file format in which the table data is stored. Only <code>PARQUET</code> is supported.</p>
<p>Required for <a href="https://docs.cloud.google.com/bigquery/docs/managed-tables">managed tables</a> .</p>
<p>The default is <code>PARQUET</code> .</p></td>
</tr>
<tr class="odd">
<td><code>table_format</code></td>
<td><p><code>STRING</code></p></td>
<td><p>In <a href="https://cloud.google.com/products/#product-launch-stages">preview</a> .</p>
<p>Example: <code>table_format=ICEBERG</code></p>
<p>The open table format in which metadata-only snapshots are stored. Only <code>ICEBERG</code> is supported.</p>
<p>Required for <a href="https://docs.cloud.google.com/bigquery/docs/managed-tables">managed tables</a> .</p>
<p>The default is <code>ICEBERG</code> .</p></td>
</tr>
<tr class="even">
<td><code>tags</code></td>
<td><code>&lt;ARRAY&lt;STRUCT&lt;STRING, STRING&gt;&gt;&gt;</code></td>
<td>An array of IAM tags for the table, expressed as key-value pairs. The key should be the <a href="https://docs.cloud.google.com/iam/docs/tags-access-control#definitions">namespaced key name</a> , and the value should be the <a href="https://docs.cloud.google.com/iam/docs/tags-access-control#definitions">short name</a> .</td>
</tr>
</tbody>
</table>

`VALUE` is a constant expression containing only literals, query parameters, and scalar functions.

The constant expression **cannot** contain:

- A reference to a table
- Subqueries or SQL statements such as `SELECT` , `CREATE` , or `UPDATE`
- User-defined functions, aggregate functions, or analytic functions
- The following scalar functions:
  - `ARRAY_TO_STRING`
  - `REPLACE`
  - `REGEXP_REPLACE`
  - `RAND`
  - `FORMAT`
  - `LPAD`
  - `RPAD`
  - `REPEAT`
  - `SESSION_USER`
  - `GENERATE_ARRAY`
  - `GENERATE_DATE_ARRAY`

### `load_option_list`

Specifies options for loading data from external files. The `format` and `uris` options are required. Specify the option list in the following format: `NAME=VALUE, ...`

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Options</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>allow_jagged_rows</code></td>
<td><p><code>BOOL</code></p>
<p>If <code>true</code> , allow rows that are missing trailing optional columns.</p>
<p>Applies to CSV data.</p></td>
</tr>
<tr class="even">
<td><code>allow_quoted_newlines</code></td>
<td><p><code>BOOL</code></p>
<p>If <code>true</code> , allow quoted data sections that contain newline characters in the file.</p>
<p>Applies to CSV data.</p></td>
</tr>
<tr class="odd">
<td><code>bigtable_options</code></td>
<td><p><code>STRING</code></p>
<p>Only required when creating a Bigtable external table.</p>
<p>Specifies the schema of the Bigtable external table in JSON format.</p>
<p>For a list of Bigtable table definition options, see <a href="https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/tables#bigtableoptions"><code>BigtableOptions</code></a> in the REST API reference.</p></td>
</tr>
<tr class="even">
<td><code>column_name_character_map</code></td>
<td><p><code>STRING</code></p>
<p>Defines the scope of supported column name characters and the handling behavior of unsupported characters. The default setting is <code>STRICT</code> , which means unsupported characters cause BigQuery to throw errors. <code>V1</code> and <code>V2</code> replace any unsupported characters with underscores.</p>
<p>Supported values include:</p>
<ul>
<li><code>STRICT</code> . Enables <a href="https://docs.cloud.google.com/bigquery/docs/schemas#flexible-column-names">flexible column names</a> . This is the default value. Load jobs with unsupported characters in column names fail with an error message. To configure the replacement of unsupported characters with underscores so that the load job succeeds, specify the <a href="https://docs.cloud.google.com/bigquery/docs/default-configuration"><code>default_column_name_character_map</code></a> configuration setting.</li>
<li><code>V1</code> . Column names can only contain <a href="https://docs.cloud.google.com/bigquery/docs/schemas#column_names">standard column name characters</a> . Unsupported characters (except <a href="https://docs.cloud.google.com/bigquery/docs/loading-data-cloud-storage-parquet#limitations_2">periods in Parquet file column names</a> ) are replaced with underscores. This is the default behavior for tables created before the introduction of <code>column_name_character_map</code> .</li>
<li><code>V2</code> . Besides <a href="https://docs.cloud.google.com/bigquery/docs/schemas#column_names">standard column name characters</a> , it also supports <a href="https://docs.cloud.google.com/bigquery/docs/schemas#flexible-column-names">flexible column names</a> . Unsupported characters (except <a href="https://docs.cloud.google.com/bigquery/docs/loading-data-cloud-storage-parquet#limitations_2">periods in Parquet file column names</a> ) are replaced with underscores.</li>
</ul>
<p>Applies to CSV and Parquet data.</p></td>
</tr>
<tr class="odd">
<td><code>compression</code></td>
<td><p><code>STRING</code></p>
<p>The compression type of the data source. Supported values include: <code>GZIP</code> . If not specified, the data source is uncompressed.</p>
<p>Applies to CSV and JSON data.</p></td>
</tr>
<tr class="even">
<td><code>decimal_target_types</code></td>
<td><p><code>ARRAY&lt;STRING&gt;</code></p>
<p>Determines how to convert a <code>Decimal</code> type. Equivalent to <a href="https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/tables#ExternalDataConfiguration.FIELDS.decimal_target_types">ExternalDataConfiguration.decimal_target_types</a></p>
<p>Example: <code>["NUMERIC", "BIGNUMERIC"]</code> .</p></td>
</tr>
<tr class="odd">
<td><code>enable_list_inference</code></td>
<td><p><code>BOOL</code></p>
<p>If <code>true</code> , use schema inference specifically for Parquet LIST logical type.</p>
<p>Applies to Parquet data.</p></td>
</tr>
<tr class="even">
<td><code>enable_logical_types</code></td>
<td><p><code>BOOL</code></p>
<p>If <code>true</code> , convert Avro logical types into their corresponding SQL types. For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/loading-data-cloud-storage-avro#logical_types">Logical types</a> .</p>
<p>Applies to Avro data.</p></td>
</tr>
<tr class="odd">
<td><code>encoding</code></td>
<td><p><code>STRING</code></p>
<p>The character encoding of the data. Supported values include: <code>UTF8</code> (or <code>UTF-8</code> ), <code>ISO_8859_1</code> (or <code>ISO-8859-1</code> ), <code>UTF-16BE</code> , <code>UTF-16LE</code> , <code>UTF-32BE</code> , or <code>UTF-32LE</code> . The default value is <code>UTF-8</code> .</p>
<p>Applies to CSV data.</p></td>
</tr>
<tr class="even">
<td><code>enum_as_string</code></td>
<td><p><code>BOOL</code></p>
<p>If <code>true</code> , infer Parquet ENUM logical type as STRING instead of BYTES by default.</p>
<p>Applies to Parquet data.</p></td>
</tr>
<tr class="odd">
<td><code>field_delimiter</code></td>
<td><p><code>STRING</code></p>
<p>The separator for fields in a CSV file.</p>
<p>Applies to CSV data.</p></td>
</tr>
<tr class="even">
<td><code>format</code></td>
<td><p><code>STRING</code></p>
<p>The format of the external data. Supported values for <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_external_table_statement"><code>CREATE EXTERNAL TABLE</code></a> include: <code>AVRO</code> , <code>CLOUD_BIGTABLE</code> , <code>CSV</code> , <code>DATASTORE_BACKUP</code> , <code>DELTA_LAKE</code> ( <a href="https://cloud.google.com/products/#product-launch-stages">preview</a> ), <code>GOOGLE_SHEETS</code> , <code>NEWLINE_DELIMITED_JSON</code> (or <code>JSON</code> ), <code>ORC</code> , <code>PARQUET</code> .</p>
<p>Supported values for <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/load-statements"><code>LOAD DATA</code></a> include: <code>AVRO</code> , <code>CSV</code> , <code>DELTA_LAKE</code> ( <a href="https://cloud.google.com/products/#product-launch-stages">preview</a> ) <code>NEWLINE_DELIMITED_JSON</code> (or <code>JSON</code> ), <code>ORC</code> , <code>PARQUET</code> .</p>
<p>The value <code>JSON</code> is equivalent to <code>NEWLINE_DELIMITED_JSON</code> .</p></td>
</tr>
<tr class="odd">
<td><code>hive_partition_uri_prefix</code></td>
<td><p><code>STRING</code></p>
<p>A common prefix for all source URIs before the partition key encoding begins. Applies only to hive-partitioned external tables.</p>
<p>Applies to Avro, CSV, JSON, Parquet, and ORC data.</p>
<p>Example: <code>"gs://bucket/path"</code> .</p></td>
</tr>
<tr class="even">
<td><code>file_set_spec_type</code></td>
<td><p><code>STRING</code></p>
<p>Specifies how to interpret source URIs for load jobs and external tables.</p>
<p>Supported values include:</p>
<ul>
<li><code>FILE_SYSTEM_MATCH</code> . Expands source URIs by listing files from the object store. This is the default behavior if FileSetSpecType is not set.</li>
<li><code>NEW_LINE_DELIMITED_MANIFEST</code> . Indicates that the provided URIs are newline-delimited manifest files, with one URI per line. Wildcard URIs are not supported in the manifest files, and all referenced data files must be in the same bucket as the manifest file.</li>
</ul>
<p>For example, if you have a source URI of <code>"gs://bucket/path/file"</code> and the <code>file_set_spec_type</code> is <code>FILE_SYSTEM_MATCH</code> , then the file is used directly as a data file. If the <code>file_set_spec_type</code> is <code>NEW_LINE_DELIMITED_MANIFEST</code> , then each line in the file is interpreted as a URI that points to a data file.</p></td>
</tr>
<tr class="odd">
<td><code>ignore_unknown_values</code></td>
<td><p><code>BOOL</code></p>
<p>If <code>true</code> , ignore extra values that are not represented in the table schema, without returning an error.</p>
<p>Applies to CSV and JSON data.</p></td>
</tr>
<tr class="even">
<td><code>json_extension</code></td>
<td><p><code>STRING</code></p>
<p>For JSON data, indicates a particular JSON interchange format. If not specified, BigQuery reads the data as generic JSON records.</p>
<p>Supported values include:<br />
<code>GEOJSON</code> . Newline-delimited GeoJSON data. For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/geospatial-data#external-geojson">Creating an external table from a newline-delimited GeoJSON file</a> .</p></td>
</tr>
<tr class="odd">
<td><code>max_bad_records</code></td>
<td><p><code>INT64</code></p>
<p>The maximum number of bad records to ignore when reading the data.</p>
<p>Applies to: CSV, JSON, and Google Sheets data.</p></td>
</tr>
<tr class="even">
<td><code>max_staleness</code></td>
<td><p><code>INTERVAL</code></p>
<p>Applicable for <a href="https://docs.cloud.google.com/bigquery/docs/biglake-intro#metadata_caching_for_performance">BigLake tables</a> and <a href="https://docs.cloud.google.com/bigquery/docs/object-table-introduction#metadata_caching_for_performance">object tables</a> .</p>
<p>Specifies whether cached metadata is used by operations against the table, and how fresh the cached metadata must be in order for the operation to use it.</p>
<p>To disable metadata caching, specify 0. This is the default.</p>
<p>To enable metadata caching, specify an <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/lexical#interval_literals">interval literal</a> value between 30 minutes and 7 days. For example, specify <code>INTERVAL 4 HOUR</code> for a 4 hour staleness interval. With this value, operations against the table use cached metadata if it has been refreshed within the past 4 hours. If the cached metadata is older than that, the operation falls back to retrieving metadata from Cloud Storage instead.</p></td>
</tr>
<tr class="odd">
<td><code>null_marker</code></td>
<td><p><code>STRING</code></p>
<p>The string that represents <code>NULL</code> values in a CSV file.</p>
<p>Applies to CSV data.</p></td>
</tr>
<tr class="even">
<td><code>null_markers</code></td>
<td><p><code>ARRAY&lt;STRING&gt;</code></p>
<p>The list of strings that represent <code>NULL</code> values in a CSV file.</p>
<p>This option cannot be used with <code>null_marker</code> option.</p>
<p>Applies to CSV data.</p></td>
</tr>
<tr class="odd">
<td><code>object_metadata</code></td>
<td><p><code>STRING</code></p>
<p>Only required when creating an <a href="https://docs.cloud.google.com/bigquery/docs/object-table-introduction">object table</a> .</p>
<p>Set the value of this option to <code>SIMPLE</code> when creating an object table.</p></td>
</tr>
<tr class="even">
<td><code>preserve_ascii_control_characters</code></td>
<td><p><code>BOOL</code></p>
<p>If <code>true</code> , then the embedded ASCII control characters which are the first 32 characters in the ASCII table, ranging from '\x00' to '\x1F', are preserved.</p>
<p>Applies to CSV data.</p></td>
</tr>
<tr class="odd">
<td><code>quote</code></td>
<td><p><code>STRING</code></p>
<p>The string used to quote data sections in a CSV file. If your data contains quoted newline characters, also set the <code>allow_quoted_newlines</code> property to <code>true</code> .</p>
<p>Applies to CSV data.</p></td>
</tr>
<tr class="even">
<td><code>skip_leading_rows</code></td>
<td><p><code>INT64</code></p>
<p>The number of rows at the top of a file to skip when reading the data.</p>
<p>Applies to CSV and Google Sheets data.</p></td>
</tr>
<tr class="odd">
<td><code>source_column_match</code></td>
<td><p><code>STRING</code></p>
<p>This controls the strategy used to match loaded columns to the schema.</p>
<p>If this value is unspecified, then the default is based on how the schema is provided. If autodetect is enabled, then the default behavior is to match columns by name. Otherwise, the default is to match columns by position. This is done to keep the behavior backward-compatible.</p>
<p>Supported values include:</p>
<ul>
<li><code>POSITION</code> : matches by position. This option assumes that the columns are ordered the same way as the schema.</li>
<li><code>NAME</code> : matches by name. This option reads the header row as column names and reorders columns to match the field names in the schema. Column names are read from the last skipped row based on the <code>skip_leading_rows</code> property.</li>
</ul></td>
</tr>
<tr class="even">
<td><code>tags</code></td>
<td><code>&lt;ARRAY&lt;STRUCT&lt;STRING, STRING&gt;&gt;&gt;</code>
<p>An array of IAM tags for the table, expressed as key-value pairs. The key should be the <a href="https://docs.cloud.google.com/iam/docs/tags-access-control#definitions">namespaced key name</a> , and the value should be the <a href="https://docs.cloud.google.com/iam/docs/tags-access-control#definitions">short name</a> .</p></td>
</tr>
<tr class="odd">
<td><code>time_zone</code></td>
<td><p><code>STRING</code></p>
<p>Default time zone that will apply when parsing timestamp values that have no specific time zone.</p>
<p>Check <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-types#time_zone_name">valid time zone names</a> .</p>
<p>If this value is not present, the timestamp values without specific time zone is parsed using default time zone UTC.</p>
<p>Applies to CSV and JSON data.</p></td>
</tr>
<tr class="even">
<td><code>date_format</code></td>
<td><p><code>STRING</code></p>
<p><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/format-elements#format_string_as_datetime">Format elements</a> that define how the DATE values are formatted in the input files (for example, <code>MM/DD/YYYY</code> ).</p>
<p>If this value is present, this format is the only compatible DATE format. <a href="https://docs.cloud.google.com/bigquery/docs/schema-detect#date_and_time_values">Schema autodetection</a> will also decide DATE column type based on this format instead of the existing format.</p>
<p>If this value is not present, the DATE field is parsed with the <a href="https://docs.cloud.google.com/bigquery/docs/loading-data-cloud-storage-csv#data_types">default formats</a> .</p>
<p>Applies to CSV and JSON data.</p></td>
</tr>
<tr class="odd">
<td><code>datetime_format</code></td>
<td><p><code>STRING</code></p>
<p><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/format-elements#format_string_as_datetime">Format elements</a> that define how the DATETIME values are formatted in the input files (for example, <code>MM/DD/YYYY HH24:MI:SS.FF3</code> ).</p>
<p>If this value is present, this format is the only compatible DATETIME format. <a href="https://docs.cloud.google.com/bigquery/docs/schema-detect#date_and_time_values">Schema autodetection</a> will also decide DATETIME column type based on this format instead of the existing format.</p>
<p>If this value is not present, the DATETIME field is parsed with the <a href="https://docs.cloud.google.com/bigquery/docs/loading-data-cloud-storage-csv#data_types">default formats</a> .</p>
<p>Applies to CSV and JSON data.</p></td>
</tr>
<tr class="even">
<td><code>time_format</code></td>
<td><p><code>STRING</code></p>
<p><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/format-elements#format_string_as_datetime">Format elements</a> that define how the TIME values are formatted in the input files (for example, <code>HH24:MI:SS.FF3</code> ).</p>
<p>If this value is present, this format is the only compatible TIME format. <a href="https://docs.cloud.google.com/bigquery/docs/schema-detect#date_and_time_values">Schema autodetection</a> will also decide TIME column type based on this format instead of the existing format.</p>
<p>If this value is not present, the TIME field is parsed with the <a href="https://docs.cloud.google.com/bigquery/docs/loading-data-cloud-storage-csv#data_types">default formats</a> .</p>
<p>Applies to CSV and JSON data.</p></td>
</tr>
<tr class="odd">
<td><code>timestamp_format</code></td>
<td><p><code>STRING</code></p>
<p><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/format-elements#format_string_as_datetime">Format elements</a> that define how the TIMESTAMP values are formatted in the input files (for example, <code>MM/DD/YYYY HH24:MI:SS.FF3</code> ).</p>
<p>If this value is present, this format is the only compatible TIMESTAMP format. <a href="https://docs.cloud.google.com/bigquery/docs/schema-detect#date_and_time_values">Schema autodetection</a> will also decide TIMESTAMP column type based on this format instead of the existing format.</p>
<p>If this value is not present, the TIMESTAMP field is parsed with the <a href="https://docs.cloud.google.com/bigquery/docs/loading-data-cloud-storage-csv#data_types">default formats</a> .</p>
<p>Applies to CSV and JSON data.</p></td>
</tr>
<tr class="even">
<td><code>uris</code></td>
<td><p>For external tables, including object tables, that aren't Bigtable tables:</p>
<p><code>ARRAY&lt;STRING&gt;</code></p>
<p>An array of fully qualified URIs for the external data locations. Each URI can contain one asterisk ( <code>*</code> ) <a href="https://docs.cloud.google.com/bigquery/docs/loading-data-cloud-storage#load-wildcards">wildcard character</a> , which must come after the bucket name. When you specify <code>uris</code> values that target multiple files, all of those files must share a compatible schema.</p>
<p>The following examples show valid <code>uris</code> values:</p>
<ul>
<li><code>['gs://bucket/path1/myfile.csv']</code></li>
<li><code>['gs://bucket/path1/*.csv']</code></li>
<li><code>['gs://bucket/path1/*', 'gs://bucket/path2/file00*']</code></li>
</ul>
<br />

<p>For Bigtable tables:</p>
<p><code>STRING</code></p>
<p>The URI identifying the Bigtable table to use as a data source. You can only specify one Bigtable URI.</p>
<p>Example: <code>https://googleapis.com/bigtable/projects/ </code><var translate="no"> project_id </var><code> /instances/ </code><var translate="no"> instance_id </var><code> [/appProfiles/ </code><var translate="no"> app_profile </var><code> ]/tables/ </code><var translate="no"> table_name</var></p>
<p>For more information on constructing a Bigtable URI, see <a href="https://docs.cloud.google.com/bigquery/docs/create-bigtable-external-table#bigtable-uri">Retrieve the Bigtable URI</a> .</p></td>
</tr>
</tbody>
</table>

### Examples

The following examples show common use cases for the `LOAD DATA` statement.

#### Load data into a table

The following example loads an Avro file into a table. Avro is a self-describing format, so BigQuery infers the schema.

```
LOAD DATA INTO mydataset.table1
  FROM FILES(
    format='AVRO',
    uris = ['gs://bucket/path/file.avro']
  )
```

The following example loads two CSV files into a table, using schema autodetection.

```
LOAD DATA INTO mydataset.table1
  FROM FILES(
    format='CSV',
    uris = ['gs://bucket/path/file1.csv', 'gs://bucket/path/file2.csv']
  )
```

#### Load data using a schema

The following example loads a CSV file into a table, using a specified table schema.

```
LOAD DATA INTO mydataset.table1(x INT64, y STRING)
  FROM FILES(
    skip_leading_rows=1,
    format='CSV',
    uris = ['gs://bucket/path/file.csv']
  )
```

#### Set options when creating a new table

The following example creates a new table with a description and an expiration time.

```
LOAD DATA INTO mydataset.table1
  OPTIONS(
    description="my table",
    expiration_timestamp="2025-01-01 00:00:00 UTC&quot;
  )
  FROM FILES(
    format='AVRO',
    uris = ['gs://bucket/path/file.avro']
  )
```

#### Overwrite an existing table

The following example overwrites an existing table.

```
LOAD DATA OVERWRITE mydataset.table1
  FROM FILES(
    format='AVRO',
    uris = ['gs://bucket/path/file.avro']
  )
```

#### Load data into a temporary table

The following example loads an Avro file into a temporary table.

```
LOAD DATA INTO TEMP TABLE mydataset.table1
  FROM FILES(
    format='AVRO',
    uris = ['gs://bucket/path/file.avro']
  )
```

#### Specify table partitioning and clustering

The following example creates a table that is partitioned by the `transaction_date` field and clustered by the `customer_id` field. It also configures the partitions to expire after three days.

```
LOAD DATA INTO mydataset.table1
  PARTITION BY transaction_date
  CLUSTER BY customer_id
  OPTIONS(
    partition_expiration_days=3
  )
  FROM FILES(
    format='AVRO',
    uris = ['gs://bucket/path/file.avro']
  )
```

#### Load data into a partition

The following example loads data into a selected partition of an ingestion-time partitioned table:

```
LOAD DATA INTO mydataset.table1
PARTITIONS(_PARTITIONTIME = TIMESTAMP '2016-01-01&#39;)
  PARTITION BY _PARTITIONTIME
  FROM FILES(
    format = 'AVRO',
    uris = ['gs://bucket/path/file.avro']
  )
```

#### Load a file that is externally partitioned

The following example loads a set of external files that use a [hive partitioning](https://docs.cloud.google.com/bigquery/docs/hive-partitioned-queries-gcs#supported_data_layouts) layout.

```
LOAD DATA INTO mydataset.table1
  FROM FILES(
    format='AVRO',
    uris = ['gs://bucket/path/*'],
    hive_partition_uri_prefix='gs://bucket/path'
  )
  WITH PARTITION COLUMNS(
    field_1 STRING, -- column order must match the external path
    field_2 INT64
  )
```

The following example infers the partitioning layout:

```
LOAD DATA INTO mydataset.table1
  FROM FILES(
    format='AVRO',
    uris = ['gs://bucket/path/*'],
    hive_partition_uri_prefix='gs://bucket/path'
  )
  WITH PARTITION COLUMNS
```

If you include both `column_list` and `WITH PARTITION COLUMNS` , then you must explicitly list the partitioning columns. For example, the following query returns an error:

```
-- This query returns an error.
LOAD DATA INTO mydataset.table1
  (
    x INT64, -- column_list is given but the partition column list is missing
    y STRING
  )
  FROM FILES(
    format='AVRO',
    uris = ['gs://bucket/path/*'],
    hive_partition_uri_prefix='gs://bucket/path'
  )
  WITH PARTITION COLUMNS
```

#### Load data with BigQuery Omni transfer

#### Example 1

The following example loads a parquet file named `sample.parquet` from an Amazon S3 bucket into the `test_parquet` table with an auto-detect schema:

```
LOAD DATA INTO mydataset.testparquet
  FROM FILES (
    uris = ['s3://test-bucket/sample.parquet'],
    format = 'PARQUET'
  )
  WITH CONNECTION `aws-us-east-1.test-connection`
```

#### Example 2

The following example loads a CSV file with the prefix `sampled*` from your Blob Storage into the `test_csv` table with predefined column partitioning by time:

```
LOAD DATA INTO mydataset.test_csv (Number INT64, Name STRING, Time DATE)
  PARTITION BY Time
  FROM FILES (
    format = 'CSV', uris = ['azure://test.blob.core.windows.net/container/sampled*'],
    skip_leading_rows=1
  )
  WITH CONNECTION `azure-eastus2.test-connection`
```

#### Example 3

The following example overwrites the existing table `test_parquet` with data from a file named `sample.parquet` with an auto-detect schema:

```
LOAD DATA OVERWRITE mydataset.testparquet
  FROM FILES (
    uris = ['s3://test-bucket/sample.parquet'],
    format = 'PARQUET'
  )
  WITH CONNECTION `aws-us-east-1.test-connection`
```
