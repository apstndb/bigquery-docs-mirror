---
name: documents/docs.cloud.google.com/bigquery/docs/migration/databricks-sql
uri: https://docs.cloud.google.com/bigquery/docs/migration/databricks-sql
title: Databricks and Apache Spark SQL translation reference
description: Learn how the BigQuery Migration Service translates Databricks SQL and Apache Spark SQL queries, Delta Lake DDL, and Unity Catalog schemas into GoogleSQL.
data_source: docs.cloud.google.com
---

# Databricks and Apache Spark SQL translation reference

> **Preview**
>
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

The BigQuery Migration Service lets you translate Databricks SQL and Apache Spark SQL statements into GoogleSQL. You can convert queries, Delta Lake table definitions, and Unity Catalog namespaces when migrating lakehouse and data warehouse workloads to BigQuery.

To translate your SQL scripts and metadata in bulk, use the [batch SQL translator](https://docs.cloud.google.com/bigquery/docs/batch-sql-translator) or the [BigQuery Migration API](https://docs.cloud.google.com/bigquery/docs/api-sql-translator) . For ad hoc queries in BigQuery Studio, use the [interactive SQL translator](https://docs.cloud.google.com/bigquery/docs/interactive-sql-translator) . Before translating workloads, you can also [run a migration assessment for Databricks](https://docs.cloud.google.com/bigquery/docs/migration-assessment#databricks) to evaluate your existing environment.

## Overview of the Databricks and Spark SQL dialect

The BigQuery Migration Service provides a single unified translator for both Databricks SQL and Spark SQL workloads. Databricks SQL is an extension of Spark SQL, and workloads often combine open-source Spark SQL syntax with Databricks-specific features. You can translate both dialects together without separating Databricks SQL statements from Spark SQL statements. The translator supports the following SQL dialects and versions:

- **Databricks SQL** : SQL syntax for Databricks SQL warehouses and Databricks runtime, including the following features:

  - Delta Lake table data definition language (DDL) statements with `USING DELTA` , `PARTITIONED BY` , and `CLUSTER BY` clauses
  - Unity Catalog three-part object names in the format `catalog.schema.table`
  - Databricks-specific built-in functions

- **Spark SQL 3.x and 4.x** : modern open-source Spark SQL syntax, expressions, and query constructs.

- **Legacy Spark SQL 2.x** : Spark SQL 2.x and Apache Hive-inherited syntax.

### Translation interface identifiers

In the Google Cloud console, the unified source dialect is named **Databricks/SparkSQL** . To maintain backward compatibility for existing Spark SQL translation workflows, the BigQuery Migration API, the Google Cloud CLI, and the BigQuery Migration Service MCP server continue to use the Spark SQL identifiers ( `sparksqlDialect` , `Translation_SparkSQL2BQ` , `SparkSQL2BigQuery_Translation` , and `SparkSQL` ) for both Databricks SQL and Spark SQL workloads. The following table summarizes the dialect identifiers across each translation interface:

| Interface                                                                                 | Setting or field   | Value for Databricks and Spark SQL                                                                                                      |
|-------------------------------------------------------------------------------------------|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------|
| Google Cloud console (interactive SQL translator and batch SQL translator)                | **Source dialect** | **Databricks/SparkSQL**                                                                                                                 |
| Google Cloud CLI ( `gcloud alpha bq migration` )                                          | `--source-dialect` | `SparkSQL`                                                                                                                              |
| BigQuery Migration API ( `TranslationConfigDetails` )                                     | `sourceDialect`    | `{"sparksqlDialect": {}}`                                                                                                               |
| BigQuery Migration API ( `MigrationTask` )                                                | `type`             | `Translation_SparkSQL2BQ` or `SparkSQL2BigQuery_Translation`                                                                            |
| BigQuery Migration Service MCP server ( `translate_query` and `translate_batch_queries` ) | `sourceDialect`    | `SparkSQL`                                                                                                                              |
| `dwh-migration-dumper` command-line extraction tool                                       | `--connector`      | `databricks` for Unity Catalog and the Databricks legacy `hive_metastore` catalog, or `hiveql` for a self-managed Apache Hive Metastore |

## Prepare your Databricks SQL input files

Before you submit a translation job, export your Databricks SQL queries, views, and table definitions into SQL text files. You can collect SQL from the following Databricks sources:

- **SQL warehouses and dashboards** : saved queries, dashboard queries, and query history from Databricks SQL.
- **Databricks notebooks** : SQL cells exported from notebooks. If a notebook mixes Python or Scala cells with `%sql` cells, extract only the SQL statements into SQL files.
- **Table and view DDL** : `CREATE TABLE` and `CREATE VIEW` statements exported with the [`SHOW CREATE TABLE` command](https://docs.databricks.com/gcp/en/sql/language-manual/sql-ref-syntax-aux-show-create-table) , or schema metadata extracted automatically by using the [`dwh-migration-dumper` tool](https://docs.cloud.google.com/bigquery/docs/generate-metadata#databricks) .
- **Scheduled jobs and workflows** : SQL task files referenced by Databricks workflows or orchestration pipelines.

### Resolve templating and notebook syntax

The SQL translator requires valid SQL statements as input. Before uploading your SQL files for translation, remove or resolve non-SQL templating and notebook constructs:

- **Notebook magic commands** : remove leading `%sql` , `%python` , `%scala` , or `%run` magic lines from exported notebook files.
- **Notebook widgets and parameters** : replace Databricks widget references and named parameter markers such as `${param}` , `:param` , and `getArgument()` with valid SQL literals or standard query parameters.

## Supported SQL statements and translation examples

The Databricks and Spark SQL translator supports the following types of SQL statements:

- **Queries** : `SELECT` queries, `WITH` clauses, and set operations
- **DDL statements** : statements such as `CREATE TABLE` , `CREATE TABLE AS SELECT` , `CREATE VIEW` , `ALTER TABLE` , and `DROP TABLE`
- **Data manipulation language (DML) statements** : statements such as `INSERT` , `UPDATE` , `DELETE` , `MERGE` , and `TRUNCATE TABLE`

### Query translation example

The translator converts Databricks SQL and Spark SQL query constructs—including common table expressions (CTEs), window functions, `LATERAL VIEW explode` clauses, higher-order array functions, and date and string functions—into equivalent GoogleSQL expressions.

The following table compares a Databricks SQL analytical query with the translated GoogleSQL output:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Databricks SQL input</th>
<th>Translated GoogleSQL output</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre data-fenced=""><code>SELECT
  c.customer_segment,
  date_format(o.order_ts, &#39;yyyy-MM&#39;) AS order_month,
  count(DISTINCT o.order_id) AS orders,
  sum(item.price * item.qty) AS gross_revenue,
  nvl(avg(o.discount_pct), 0.0) AS avg_discount
FROM main.sales.orders AS o
JOIN main.sales.customers AS c
  ON o.customer_id = c.customer_id
LATERAL VIEW explode(o.line_items) items AS item
WHERE o.order_ts &gt;= date_sub(current_date(), 90)
GROUP BY ALL
ORDER BY gross_revenue DESC;</code></pre></td>
<td><pre data-fenced=""><code>SELECT
  c.customer_segment,
  FORMAT_TIMESTAMP(&#39;%Y-%m&#39;, o.order_ts) AS order_month,
  COUNT(DISTINCT o.order_id) AS orders,
  SUM(item.price * item.qty) AS gross_revenue,
  COALESCE(AVG(o.discount_pct), 0.0) AS avg_discount
FROM `main`.sales.orders AS o
INNER JOIN `main`.sales.customers AS c
  ON o.customer_id = c.customer_id
CROSS JOIN UNNEST(o.line_items) AS item
WHERE o.order_ts &gt;= TIMESTAMP(DATE_SUB(CURRENT_DATE(), INTERVAL 90 DAY))
GROUP BY ALL
ORDER BY gross_revenue DESC;</code></pre></td>
</tr>
</tbody>
</table>

### Delta Lake table DDL translation

When translating Databricks `CREATE TABLE` DDL statements or generating target DDL from a metadata ZIP file extracted with the `dwh-migration-dumper` tool, the translator converts source storage layouts and table formats into BigQuery `CREATE TABLE` statements, including the following elements:

- `USING DELTA` clauses
- Column comments
- Table properties
- Partitioning with `PARTITIONED BY` clauses
- Clustering with `CLUSTER BY` and `CLUSTERED BY` clauses

By default, the translator generates `CREATE TABLE` DDL for standard BigQuery tables. If you're migrating lakehouse tables to open table formats on Cloud Storage, you can use a [configuration YAML file](https://docs.cloud.google.com/bigquery/docs/config-yaml-translation#yaml_examples) to generate DDL for [Apache Iceberg managed tables](https://docs.cloud.google.com/bigquery/docs/biglake-iceberg-tables-in-bigquery) or external tables instead.

The following table shows how a Databricks Delta Lake table definition translates into GoogleSQL:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Databricks SQL input</th>
<th>Translated GoogleSQL output</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre data-fenced=""><code>CREATE TABLE IF NOT EXISTS main.sales.orders (
  order_id BIGINT NOT NULL,
  customer_id STRING,
  order_ts TIMESTAMP,
  order_date DATE,
  total_amount DECIMAL(18, 2),
  tags ARRAY&lt;STRING&gt;
)
USING DELTA
PARTITIONED BY (order_date)
CLUSTER BY (customer_id)
COMMENT &#39;Customer orders&#39;;</code></pre></td>
<td><pre data-fenced=""><code>CREATE TABLE IF NOT EXISTS `main`.sales.orders (
  order_id INT64 NOT NULL,
  customer_id STRING,
  order_ts TIMESTAMP,
  order_date DATE,
  total_amount NUMERIC(31, 2),
  tags ARRAY&lt;STRING&gt;
)
PARTITION BY order_date
CLUSTER BY customer_id
OPTIONS (
  description = &#39;Customer orders&#39;
);</code></pre></td>
</tr>
</tbody>
</table>

#### Partitioning and clustering limits and requirements

Databricks and BigQuery enforce different limits and column data type requirements for table partitioning and clustering:

- **Partitioning ( `PARTITIONED BY` )** : source `PARTITIONED BY` clauses map to BigQuery `PARTITION BY` . [Partitioned tables](https://docs.cloud.google.com/bigquery/docs/partitioned-tables) in BigQuery support a single partitioning column ( `DATE` , `DATETIME` , `TIMESTAMP` , or `INT64` range partitioning).
- **Clustering ( `CLUSTER BY` and `CLUSTERED BY` )** : source `CLUSTER BY` and `CLUSTERED BY` clauses map to BigQuery `CLUSTER BY` . [Clustered tables](https://docs.cloud.google.com/bigquery/docs/clustered-tables) in BigQuery support up to four explicit clustering columns. If a source table uses automatic liquid clustering ( `CLUSTER BY AUTO` ) without explicit column names, the translator omits the `CLUSTER BY` clause.

When a source table specifies more partitioning or clustering columns than BigQuery supports, the translator selects a subset of columns that conforms to BigQuery limits. To customize the target partitioning or clustering columns, use a configuration YAML file to [set or change table partitioning](https://docs.cloud.google.com/bigquery/docs/config-yaml-translation#set_or_change_table_partitioning) or [set or change table clustering](https://docs.cloud.google.com/bigquery/docs/config-yaml-translation#set_or_change_table_clustering) .

## Extracted Databricks metadata archive

You can use the [`dwh-migration-dumper` tool](https://docs.cloud.google.com/bigquery/docs/generate-metadata#databricks) to extract metadata from the following sources:

- Databricks Unity Catalog
- The Databricks legacy Hive metastore in the `hive_metastore` catalog
- A self-managed Hive Metastore

When you run the `dwh-migration-dumper` tool with the `databricks` connector, the tool packages the extracted catalog metadata into CSV files inside a metadata ZIP archive. The metadata archive captures the following object attributes for translation:

- Three-part object identifiers consisting of the `catalog` , `schema` , and `table` names
- Column names, data types, nullability, and column comments
- Data source format values, such as `DELTA` , `ICEBERG` , or `PARQUET`
- Table type, whether managed or external, and storage location URI
- Partitioning and clustering columns

Providing this metadata ZIP archive in your interactive or batch translation jobs helps the translator resolve unqualified column references, apply accurate type casts, and preserve table layouts.

You can also use the metadata ZIP archive for [metadata translation](https://docs.cloud.google.com/bigquery/docs/batch-sql-translator#translate_metadata) to generate per-table schema mapping YAML files (commonly referred to as `tables.yaml` files) for the [BigQuery Migration Service validation service](https://docs.cloud.google.com/bigquery/docs/migration/migration-validation#supported-data-warehouses) . The validation service can use these schema mapping files to verify that tables are migrated accurately even when a workload doesn't include SQL scripts.

## Unity Catalog three-part names

Databricks Unity Catalog uses a three-level namespace in the format `catalog.schema.table` , which maps to the three-level BigQuery identifier in the format `project_id.dataset.table` :

- **Catalog** : corresponds to the `database` name part in BigQuery Migration Service and maps to the BigQuery project ID.
- **Schema** : corresponds to the `schema` name part and maps to the BigQuery dataset name.
- **Table or view** : corresponds to the `relation` name part and maps to the BigQuery table or view name.

To ensure that two-part ( `schema.table` ) and three-part ( `catalog.schema.table` ) references resolve to your target BigQuery project and dataset, configure the following settings:

1.  **Set the default database and schema search path** : configure the following options in a [configuration YAML file](https://docs.cloud.google.com/bigquery/docs/config-yaml-translation#specifying_default_database_and_schema_search_path) with the `type: environment` header, or in the `sourceEnv` fields in the BigQuery Migration API:

    - Set the `defaultDatabase` property to the Unity Catalog name that your scripts assume, such as `main` .
    - Add any default schemas to the `schemaSearchPath` property.

2.  **Map Unity Catalog names to BigQuery projects and datasets** : because a Unity Catalog name such as `main` rarely matches your target Google Cloud project ID, add an [output name mapping rule](https://docs.cloud.google.com/bigquery/docs/config-yaml-translation#output_name_mapping) in a `.config.yaml` file to map the `catalog.schema` namespace to the `project_id.dataset` identifier. For more information, see [Map SQL object names for translation](https://docs.cloud.google.com/bigquery/docs/output-name-mapping) .

## Limitations and unsupported features

In [Preview](https://cloud.google.com/products#product-launch-stages) , the Databricks and Spark SQL translator supports only SQL statements. The following Databricks features don't have direct SQL translation support and require manual migration or redesign:

- **Non-SQL notebook code** : PySpark, Scala, R, and Python cells in Databricks notebooks aren't translated by the SQL translator.
- **Delta Live Tables and Lakeflow Declarative Pipelines** : pipeline declarations, `CREATE OR REFRESH STREAMING TABLE` syntax, and the `STREAM` relation function aren't supported.
- **Databricks operational and storage maintenance commands** : commands specific to Delta Lake and Spark execution management—such as `OPTIMIZE` (including `ZORDER BY` clauses), `VACUUM` , `CACHE TABLE` , `UNCACHE TABLE` , `REFRESH TABLE` , and `ANALYZE TABLE` —have no equivalent in BigQuery, which manages storage optimization and caching automatically. These commands are reported as translation warnings.
- **Unity Catalog governance and storage objects** : `GRANT` and `REVOKE` statements on Unity Catalog securables, row filters, column masks, external locations, storage credentials, and Unity Catalog volumes aren't translated. Configure equivalent access controls in BigQuery by using [Identity and Access Management roles](https://docs.cloud.google.com/bigquery/docs/access-control) , [row-level security](https://docs.cloud.google.com/bigquery/docs/row-level-security-intro) , and [column-level security](https://docs.cloud.google.com/bigquery/docs/column-level-security-intro) .
- **Unsupported user-defined functions (UDFs)** : Python UDFs, Scala UDFs, and SQL UDFs that use unsupported language features or runtime libraries must be rewritten as [BigQuery UDFs](https://docs.cloud.google.com/bigquery/docs/user-defined-functions) . In addition, the `dwh-migration-dumper` tool doesn't extract UDF metadata from the legacy `hive_metastore` catalog. To help the translator resolve queries that call custom UDFs when UDF metadata isn't available or when you don't supply the original `CREATE FUNCTION` DDL, register the UDF signatures in a [configuration YAML file](https://docs.cloud.google.com/bigquery/docs/config-yaml-translation#udf_specification) .
- **Non-ANSI execution semantics** : translated queries use BigQuery default ANSI SQL semantics, which match the default ANSI mode in Databricks SQL and Spark 4.0 and later. In ANSI mode, operations such as division by zero, arithmetic overflow, and invalid type casts return runtime errors instead of `NULL` . If your legacy Databricks or Spark workloads rely on non-ANSI mode, update affected expressions in the translated SQL to use the `SAFE_CAST` and `SAFE_DIVIDE` functions, or the [`SAFE.` prefix](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/functions-reference#safe_prefix) , where `NULL` -on-error behavior is required.

## What's next

- Learn how to [extract metadata from Databricks](https://docs.cloud.google.com/bigquery/docs/generate-metadata#databricks) with the `dwh-migration-dumper` tool.
- Learn how to [translate queries interactively](https://docs.cloud.google.com/bigquery/docs/interactive-sql-translator) in BigQuery Studio.
- Learn how to [run a batch SQL translation job](https://docs.cloud.google.com/bigquery/docs/batch-sql-translator) .
- Learn how to [customize translations with configuration YAML files](https://docs.cloud.google.com/bigquery/docs/config-yaml-translation) .
- Learn how to [translate queries with an AI agent using the BigQuery Migration Service MCP server](https://docs.cloud.google.com/bigquery/docs/use-bigquery-migration-mcp) .
- Learn how to [troubleshoot migration and SQL translation issues](https://docs.cloud.google.com/bigquery/docs/troubleshoot-migrations) .
