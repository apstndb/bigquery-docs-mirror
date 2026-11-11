---
name: documents/docs.cloud.google.com/bigquery/docs/config-yaml-translation
uri: https://docs.cloud.google.com/bigquery/docs/config-yaml-translation
title: Transform SQL translations with YAML
description: Learn how to use configuration YAML files to customize and transform SQL translations when migrating to BigQuery.
data_source: docs.cloud.google.com
---

# Transform SQL translations with YAML

configuration YAML files let you customize how BigQuery translates SQL code from your source database during a migration. The BigQuery Migration Service supports two kinds of configuration YAML files: `*.config.yaml` translation configuration files that give the translation engine deterministic rules, and `*.ai_config.yaml` Gemini-based configuration files that give Gemini natural-language rules.

To customize a SQL translation with configuration YAML files, do the following:

1.  **Create configuration files** : Create deterministic [`*.config.yaml` translation configuration files](https://docs.cloud.google.com/bigquery/docs/config-yaml-translation#yaml_guidelines) , [`*.ai_config.yaml` Gemini-based configuration files](https://docs.cloud.google.com/bigquery/docs/config-yaml-translation#ai_yaml_guidelines) , or [both types of configuration files](https://docs.cloud.google.com/bigquery/docs/config-yaml-translation#config-processing-order) to combine structural rules with Gemini customization.
2.  **Provide the files to a translation job** : [Submit the configuration files](https://docs.cloud.google.com/bigquery/docs/config-yaml-translation#provide-config-files) when you translate a single query or batch SQL files.
3.  **Review the translation outputs** : [Locate the translated SQL and Gemini suggestions](https://docs.cloud.google.com/bigquery/docs/config-yaml-translation#translation-outputs) in the response when you translate a single query, or in Cloud Storage when you translate batch SQL files.

## Types of configuration YAML files

The following table compares the two types of configuration YAML files:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Feature</th>
<th>Translation configuration ( <code>*.config.yaml</code> )</th>
<th>Gemini-based configuration ( <code>*.ai_config.yaml</code> )</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<th>How rules are applied</th>
<td>Rules are applied by the translation engine as deterministic rules on the parsed SQL, so the same input and configuration always produce the same output.</td>
<td>Rules are applied by Gemini as natural-language instructions and examples applied to the SQL text. Output can vary between runs, so always review and verify suggestions before using them.</td>
</tr>
<tr class="even">
<th>What can be transformed</th>
<td>The translation engine can transform any objects or settings that it recognizes. This includes database, schema, table, column, and function names and types, table properties such as partitioning, clustering, and expiration, session defaults, UDF signatures, optimizations, and statement output such as <code>GROUP BY</code> and <code>SELECT *</code> style.</td>
<td>Gemini can change any SQL transformation that you can describe in natural language. This includes formatting and comments, replacing patterns, rewriting constructs that the engine doesn't translate the way you want, and generating an explanation of the translation.</td>
</tr>
<tr class="odd">
<th>Requirements</th>
<td><ul>
<li>The input SQL must parse in the source dialect.</li>
<li>Rules can't act on text in the input SQL that the parser doesn't recognize, such as <code>${VAR}</code> placeholders or template syntax.</li>
<li>Use a <code>SOURCE_SQL</code> rule in <code>*.ai_config.yaml</code> files or your own preprocessing to remove such text first.</li>
</ul></td>
<td><ul>
<li>You must enable Gemini AI suggestions for the job.</li>
<li>The job must run in a <a href="https://docs.cloud.google.com/vertex-ai/generative-ai/docs/learn/locations#google_model_endpoint_locations">supported processing location</a> .</li>
<li>Gemini usage is free up to a limit.</li>
</ul></td>
</tr>
<tr class="even">
<th>Where the result appears</th>
<td>The result appears in the translated SQL itself, such as in the translation response or in the <code>sql/</code> output directory in Cloud Storage.</td>
<td>The result appears as separate Gemini suggestions in the Google Cloud console, in separate suggestion fields or output files in the Google Cloud CLI and MCP server, or in separate <code>*_suggestion/</code> output directories in Cloud Storage. For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/config-yaml-translation#translation-outputs">Where to find translation outputs</a> .</td>
</tr>
<tr class="odd">
<th>Filename</th>
<td>File names must end with <code>.config.yaml</code> —for example, <code>rename-tables.config.yaml</code> .</td>
<td>File names must end with <code>.ai_config.yaml</code> —for example, <code>style-rules.ai_config.yaml</code> .</td>
</tr>
<tr class="even">
<th>The translation service ignores any YAML file in the input that doesn't end with <code>.config.yaml</code> or <code>.ai_config.yaml</code> and reports the ignored file in the translation log.</th>
<td></td>
<td></td>
</tr>
<tr class="odd">
<th>Reference</th>
<td>For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/config-yaml-translation#yaml_guidelines">Guidelines to create a configuration YAML file</a> and <a href="https://docs.cloud.google.com/bigquery/docs/config-yaml-translation#yaml_examples">configuration YAML examples</a> on this page.</td>
<td>For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/config-yaml-translation#ai_yaml_guidelines">Create a Gemini-based configuration YAML file</a> on this page.</td>
</tr>
</tbody>
</table>

### How the two kinds of rules are applied

A translation job applies configuration rules in the following order:

1.  Gemini applies `SOURCE_SQL` rules in `*.ai_config.yaml` files to the original input SQL to produce rewritten source SQL.
2.  The translation engine translates the rewritten source SQL from the preceding step—or the original input SQL if no `SOURCE_SQL` rules apply—and applies any rules in `*.config.yaml` files to produce the translated SQL.
3.  Gemini applies `TARGET_SQL` rules in `*.ai_config.yaml` files to the translated SQL from the preceding step to produce rewritten target SQL. If your `*.ai_config.yaml` files include `TRANSLATION_EXPLANATION` rules, then Gemini also generates a text explanation of the translated SQL.

We recommend that you use `*.config.yaml` rules for repeatable, structural changes such as renaming objects, mapping types, and setting partitioning. We recommend that you use `*.ai_config.yaml` rules for changes that the engine can't express, or for cleaning up input that doesn't parse. You can use both types of configuration files in the same job.

## Provide configuration files to a translation

The Google Cloud console, gcloud CLI, BigQuery Migration API, and BigQuery Migration Service MCP server support using multiple configuration files in a single translation job. For more information, see [Applying multiple YAML configurations](https://docs.cloud.google.com/bigquery/docs/config-yaml-translation#yaml_multiple) .

To provide configuration files to a translation job, select one of the following options:

### Console

- To use configuration files when translating a single query, specify them in the translation settings of the interactive translator:
  - `*.config.yaml` : In the **Translation Configuration Source Location** field in the translation settings, [specify a Cloud Storage path](https://docs.cloud.google.com/bigquery/docs/interactive-sql-translator#translate-with-additional-configs) to the configuration file.
  - `*.ai_config.yaml` : [Create customization rules](https://docs.cloud.google.com/bigquery/docs/interactive-sql-translator#customize) , which are saved to `__default.ai_config.yaml` , or specify a Cloud Storage path.
- To use configuration files while batch translating SQL files, do the following:
  - `*.config.yaml` : Upload the configuration files in the input Cloud Storage directory, then in the translation settings, [specify a path to the directory in the **File location details** field](https://docs.cloud.google.com/bigquery/docs/batch-sql-translator#submit_a_translation_job) .
  - `*.ai_config.yaml` : Upload the configuration files in the input Cloud Storage directory, then in the translation settings, select **Optional settings** \> **Gemini AI suggestions** .

### gcloud

> **Preview**
>
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

- When using the [`gcloud alpha bq migration translate` command](https://docs.cloud.google.com/bigquery/docs/interactive-sql-translator#translate_a_query_into_standard_sql) , use the `--translation-config-files` flag to specify either `*.config.yaml` or `*.ai_config.yaml` files.
- When using the [`gcloud alpha bq migration translate-batch` command](https://docs.cloud.google.com/bigquery/docs/batch-sql-translator#config-yaml) , do one of the following:
  - `*.config.yaml` : Include the files in the input directory that you pass to `--source-gcs-uris` or `--source-local-dirs` , or pass individual files with the `--source-gcs-files` or `--source-local-files` flag.
  - `*.ai_config.yaml` : Include the files in the input directory that you pass to `--source-gcs-uris` or `--source-local-dirs` , or pass individual files with the `--source-gcs-files` or `--source-local-files` flag, and add the `--enable-ai-suggestion` flag.

### API

In the [BigQuery Migration API](https://docs.cloud.google.com/bigquery/docs/api-sql-translator) , whether you translate a single query or batch SQL files, do the following:

- `*.config.yaml` : Upload the files under the input path in `source_spec.base_uri` , pass a `gcs_file_path` entry in `source_spec` when the file isn't under `base_uri` , or pass an inline `literal` entry in `source_spec` .
- `*.ai_config.yaml` : Provide the files in `source_spec` under `base_uri` , as a `gcs_file_path` entry when the file isn't under `base_uri` , or as an inline `literal` entry, and include `"suggestion"` in `target_types` —for example, `"target_types": ["sql", "suggestion"]` .

### MCP

In the [BigQuery Migration Service MCP server](https://docs.cloud.google.com/bigquery/docs/use-bigquery-migration-mcp) :

- To translate a single query ( `translate_query` ), do the following:
  - `*.config.yaml` : Pass inline `translationConfigs` entries.
  - `*.ai_config.yaml` : Pass inline `aiSuggestionConfigs` entries.
- To translate batch SQL files ( `translate_batch_queries` ), do the following:
  - `*.config.yaml` : Upload the files under `sourceBaseUri` , or list them in `configurationFilePaths` when they aren't under `sourceBaseUri` .
  - `*.ai_config.yaml` : Upload the files under `sourceBaseUri` , or list them in `configurationFilePaths` when they aren't under `sourceBaseUri` , and set `enableAiSuggestions` to `true` .

## Where to find translation outputs

Depending on the configuration files that you provide, a translation job can produce the following outputs:

- Translated SQL from the translation engine after it applies any rules in `*.config.yaml` files.
- Rewritten source SQL from Gemini after it applies `SOURCE_SQL` rules in `*.ai_config.yaml` files.
- Rewritten target SQL from Gemini after it applies `TARGET_SQL` rules in `*.ai_config.yaml` files.
- A translation explanation from Gemini when your `*.ai_config.yaml` files include `TRANSLATION_EXPLANATION` rules, or when you request an explanation on demand.

Where you find these outputs depends on how you run the translation:

- To find outputs when you translate a single query in the Google Cloud console or the gcloud CLI, see [Explore the translation output](https://docs.cloud.google.com/bigquery/docs/interactive-sql-translator#translation-output) in the interactive SQL translator guide.
- To find outputs when you translate batch SQL files in Cloud Storage or review them in the Google Cloud console, see [Explore the translation output](https://docs.cloud.google.com/bigquery/docs/batch-sql-translator#explore_the_translation_output) in the batch SQL translator guide.
- To find outputs when you use the BigQuery Migration API, see [Retrieve results](https://docs.cloud.google.com/bigquery/docs/api-sql-translator#retrieve_results) in the BigQuery Migration API guide. For single-query translations, add the output paths that you want— `sql/<var>PATH</var>` , `source_sql_query_customization_suggestion/<var>PATH</var>` , `target_sql_query_customization_suggestion/<var>PATH</var>` , or `translation_explanation_suggestion/<var>PATH</var>` —to `target_return_literals` to receive them in `translatedLiterals` .
- To find outputs when you use the BigQuery Migration Service MCP server, see [Use the BigQuery Migration Service MCP server](https://docs.cloud.google.com/bigquery/docs/use-bigquery-migration-mcp) . The `translate_query` and `get_translation` tools return `translatedQuery` , `sourceSqlSuggestion` , and `targetSqlSuggestion` , and the `explain_translation` tool returns a translation explanation.

## Translation `*.config.yaml` file requirements

A translation `*.config.yaml` file must meet the following requirements to be compatible with the BigQuery Migration Service:

- When you upload `*.config.yaml` files under the input Cloud Storage path for a batch translation job, configuration files placed anywhere under the input path apply to the entire job. They don't need to be at the root level or copied into each subdirectory. For information on how to create buckets and upload files to Cloud Storage, see [Create buckets](https://docs.cloud.google.com/storage/docs/creating-buckets) and [Upload objects from a filesystem](https://docs.cloud.google.com/storage/docs/uploading-objects) .
- The file size for a single `*.config.yaml` file must not exceed 1 MB.
- The total file size of all `*.config.yaml` files used in a single SQL translation job must not exceed 4 MB.
- If you are using `regex` syntax for name matching, use [RE2/J](https://github.com/google/re2j) .
- All translation configuration file names must end with `.config.yaml` —for example, `change-case.config.yaml` . `config.yaml` alone isn't a valid name for the configuration file.

## Guidelines to create a configuration YAML file

This section provides some general guidelines to create a configuration YAML file:

### Header

Each configuration file must contain a header specifying the type of configuration. The `object_rewriter` type is used to specify SQL translations in a configuration YAML file. The following example uses the `object_rewriter` type to transform a name case:

```
type: object_rewriter
global:
  case:
    all: UPPERCASE
```

### Entity selection

To perform entity-specific transformations, specify the entity in the configuration file. All `match` properties are optional; only use the `match` properties needed for a transformation. The following configuration YAML exposes properties to be matched in order to select specific entities:

```
match:
  database: <literal_name>
  schema: <literal_name>
  relation: <literal_name>
  attribute: <literal_name>
  databaseRegex: <regex>
  schemaRegex: <regex>
  relationRegex: <regex>
  attributeRegex: <regex>
```

Description of each `match` property:

- `database` or `db` : the project_id component.
- `schema` : the dataset component.
- `relation` : the table component.
- `attribute` : the column component. Only valid for attribute selection
- `databaseRegex` or `dbRegex` : matches a `database` property with a regular expression ( [Preview](https://cloud.google.com/products/#product-launch-stages) ).
- `schemaRegex` : matches `schema` properties to regular expressions ( [Preview](https://cloud.google.com/products/#product-launch-stages) ).
- `relationRegex` : matches `relation` properties with regular expressions ( [Preview](https://cloud.google.com/products/#product-launch-stages) ).
- `attributeRegex` : matches `attribute` properties with regular expressions. Only valid for attribute selection ( [Preview](https://cloud.google.com/products/#product-launch-stages) ).

For example, the following configuration YAML specifies the `match` properties to select the `testdb.acme.employee` table for a temporary table transformation.

```
type: object_rewriter
relation:
-
  match:
    database: testdb
    schema: acme
    relation: employee
  temporary: true
```

You can use the `databaseRegex` , `schemaRegex` , `relationRegex` , and `attributeRegex` properties to specify regular expressions in order to select a subset of entities. The following example changes all relations from `tmp_schema` schema in `testdb` to temporary, as long as their name starts with `tmp_` :

```
type: object_rewriter
relation:
-
  match:
    schema: tmp_schema
    relationRegex: "tmp_.*"
  temporary: true
```

Both literal and `regex` properties are matched in a case-insensitive manner. You can enforce case-sensitive matching by using a `regex` with a disabled `i` flag, as seen in the following example:

```
match:
  relationRegex: "(?-i:<actual_regex>)"
```

You can also specify fully-qualified entities using an equivalent short-string syntax. A short-string syntax expects exactly 3 (for relation selection) or 4 (for attribute selection) name segments delimited with dots, as the example `testdb.acme.employee` . The segments are then internally interpreted as if they were passed as `database` , `schema` , `relation` and `attribute` respectively. This means that names are matched literally, thus regular expressions are not allowed in short syntax. The following example shows the use of short-string syntax to specify a fully-qualified entity in a configuration YAML file:

```
type: object_rewriter
relation:
-
  match : "testdb.acme.employee"
  temporary: true
```

If a table contains a dot in the name, you cannot specify the name using a short syntax. In this case, you must use an object match. The following example changes the `testdb.acme.stg.employee` table to temporary:

```
type: object_rewriter
relation:
-
  match:
    database: testdb
    schema: acme
    relation: stg.employee
  temporary: true
```

The configuration YAML accepts `key` as an alias to `match` .

### Default database

Some input SQL dialects, notably Teradata, do not support `database-name` in the qualified name. In this case, the easiest way to match entities is to omit `database` property in `match` .

However, you can set the `default_database` property of the BigQuery Migration Service and use that default database in the `match` .

### Supported target attribute types

You can use the configuration YAML file to [perform attribute type transformations](https://docs.cloud.google.com/bigquery/docs/config-yaml-translation#change_type_of_a_column_attribute) , where you transform the data type of a column from the source type to a target type. The configuration YAML file supports the following target types:

- `BOOLEAN`
- `TINYINT`
- `SMALLINT`
- `INTEGER`
- `BIGINT`
- `FLOAT`
- `DOUBLE`
- `NUMERIC` (Supports optional precision and scale, such as `NUMERIC(18, 2)` )
- `TIME`
- `TIMETZ`
- `DATE`
- `DATETIME`
- `TIMESTAMP`
- `TIMESTAMPTZ`
- `CHAR` (Supports optional precision, such as `CHAR(42)` )
- `VARCHAR` (Supports optional precision, such as `VARCHAR(42)` )

## Configuration YAML examples

This section provides examples to create various configuration YAML files to use with your SQL translations. Each example outlines the YAML syntax to transform your SQL translation in specific ways, along with a brief description. Each example also provides the contents of a `teradata-input.sql` or `hive-input.sql` file and a `bq-output.sql` file so that you can compare the effects of a configuration YAML on a BigQuery SQL query translation.

The following examples use Teradata or Apache Hive as the input SQL dialect and BigQuery SQL as the output dialect. The following examples also use `testdb` as the default database, and `testschema` as the schema search path.

### Change object-name case

> **Preview**
>
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

The following configuration YAML changes the upper or lower-casing of object names:

```
type: object_rewriter
global:
  case:
    all: UPPERCASE
    database: LOWERCASE
    attribute: LOWERCASE
```

A SQL translation with this configuration YAML file might look like the following:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><code>teradata-input.sql</code></td>
<td><pre data-fenced=""><code>create table x(a int);
      select * from x;</code></pre></td>
</tr>
<tr class="even">
<td><code>bq-output.sql</code></td>
<td><pre data-fenced=""><code>CREATE TABLE testdb.TESTSCHEMA.X
      (
        a INT64
      )
      ;
      SELECT
          X.a
        FROM
          testdb.TESTSCHEMA.X
      ;</code></pre></td>
</tr>
</tbody>
</table>

### Make table temporary

> **Preview**
>
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

The following configuration YAML changes a regular table to a [temporary table](https://docs.cloud.google.com/bigquery/docs/writing-results#temporary_and_permanent_tables) :

```
type: object_rewriter
relation:
  -
    match: "testdb.testschema.x"
    temporary: true
```

A SQL translation with this configuration YAML file might look like the following:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><code>teradata-input.sql</code></td>
<td><pre data-fenced=""><code>create table x(a int);</code></pre></td>
</tr>
<tr class="even">
<td><code>bq-output.sql</code></td>
<td><pre data-fenced=""><code>CREATE TEMPORARY TABLE x
    (
      a INT64
    )
    ;</code></pre></td>
</tr>
</tbody>
</table>

### Make table ephemeral

> **Preview**
>
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

The following configuration YAML changes a regular table to an [ephemeral table](https://docs.cloud.google.com/bigquery/docs/managing-tables#updating_a_tables_expiration_time) with a 60 second expiration.

```
type: object_rewriter
relation:
  -
    match: "testdb.testschema.x"
    ephemeral:
      expireAfterSeconds: 60
```

A SQL translation with this configuration YAML file might look like the following:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><code>teradata-input.sql</code></td>
<td><pre data-fenced=""><code>create table x(a int);</code></pre></td>
</tr>
<tr class="even">
<td><code>bq-output.sql</code></td>
<td><pre data-fenced=""><code>CREATE TABLE testdb.testschema.x
    (
      a INT64
    )
    OPTIONS(
      expiration_timestamp=timestamp_add(current_timestamp(), interval 60 SECOND)
    );</code></pre></td>
</tr>
</tbody>
</table>

### Set partition expiration

> **Preview**
>
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

The following configuration YAML changes the [expiration of a partitioned table](https://docs.cloud.google.com/bigquery/docs/managing-partitioned-tables#partition-expiration) to 1 day:

```
type: object_rewriter
relation:
  -
    match: "testdb.testschema.x"
    partitionLifetime:
      expireAfterSeconds: 86400
```

A SQL translation with this configuration YAML file might look like the following:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><code>teradata-input.sql</code></td>
<td><pre data-fenced=""><code>create table x(a int, b int) partition by (a);</code></pre></td>
</tr>
<tr class="even">
<td><code>bq-output.sql</code></td>
<td><pre data-fenced=""><code>CREATE TABLE testdb.testschema.x
    (
      a INT64,
      b INT64
    )
    CLUSTER BY a
    OPTIONS(
      partition_expiration_days=1
    );</code></pre></td>
</tr>
</tbody>
</table>

### Change external location or format for a table

> **Preview**
>
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

The following configuration YAML changes the [external location and format for a table](https://docs.cloud.google.com/bigquery/docs/external-data-sources#external_tables) :

```
type: object_rewriter
relation:
  -
    match: "testdb.testschema.x"
    external:
      locations: "gs://path/to/department/files"
      format: ORC
```

A SQL translation with this configuration YAML file might look like the following:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><code>teradata-input.sql</code></td>
<td><pre data-fenced=""><code>create table x(a int);</code></pre></td>
</tr>
<tr class="even">
<td><code>bq-output.sql</code></td>
<td><pre data-fenced=""><code>CREATE EXTERNAL TABLE testdb.testschema.x
    (
      a INT64
    )
    OPTIONS(
      format=&#39;ORC&#39;,
      uris=[
        &#39;gs://path/to/department/files&#39;
      ]
    );</code></pre></td>
</tr>
</tbody>
</table>

### Set or change table description

> **Preview**
>
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

The following configuration YAML sets the description of a table:

```
type: object_rewriter
relation:
  -
    match: "testdb.testschema.x"
    description:
      text: "Example description."
```

A SQL translation with this configuration YAML file might look like the following:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><code>teradata-input.sql</code></td>
<td><pre data-fenced=""><code>create table x(a int);</code></pre></td>
</tr>
<tr class="even">
<td><code>bq-output.sql</code></td>
<td><pre data-fenced=""><code>CREATE TABLE testdb.testschema.x
    (
      a INT64
    )
    OPTIONS(
      description=&#39;Example description.&#39;
    );</code></pre></td>
</tr>
</tbody>
</table>

### Set or change table partitioning

The following configuration YAML changes the [partitioning scheme of a table](https://docs.cloud.google.com/bigquery/docs/partitioned-tables) so that it partitions by a date column:

```
type: object_rewriter
relation:
  -
    match: "testdb.testschema.x"
    partition:
      simple:
        add: [a]
  -
    match: "testdb.testschema.y"
    partition:
      simple:
        remove: [a]
```

A SQL translation with this configuration YAML file might look like the following:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><code>teradata-input.sql</code></td>
<td><pre data-fenced=""><code>create table x(a date, b int);
    create table y(a date, b int) partition by (a);</code></pre></td>
</tr>
<tr class="even">
<td><code>bq-output.sql</code></td>
<td><pre data-fenced=""><code>CREATE TABLE testdb.testschema.x
    (
      a DATE,
      b INT64
    )
    PARTITION BY a;
    CREATE TABLE testdb.testschema.y
    (
      a DATE,
      b INT64
    )
    ;</code></pre></td>
</tr>
</tbody>
</table>

The following configuration YAML changes the [partitioning scheme of a table](https://docs.cloud.google.com/bigquery/docs/partitioned-tables) so that it partitions by range bucket:

```
type: object_rewriter
relation:
-
  key: "testdb.testschema.mytable"
  partition:
    range_bucket:
      column: "id"
      start: 0
      end: 100
      step: 10
      options:
        require_partition_filter: "TRUE"
```

A SQL translation with this configuration YAML file might look like the following:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><code>snowflake-input.sql</code></td>
<td><pre data-fenced=""><code>create table testschema.mytable (date timestamp_ntz, id number, content variant);</code></pre></td>
</tr>
<tr class="even">
<td><code>bq-output.sql</code></td>
<td><pre data-fenced=""><code>create table testdb.testschema.mytable
      (
        date datetime,
        id int64,
        content json
      )
      partition by range_bucket(id, generate_array(0, 100, 10))
      options(
        require_partition_filter=true
      );</code></pre></td>
</tr>
</tbody>
</table>

### Set or change table clustering

The following configuration YAML changes the [clustering scheme of a table](https://docs.cloud.google.com/bigquery/docs/clustered-tables) :

```
type: object_rewriter
relation:
  -
    match: "testdb.testschema.x"
    clustering:
      add: [a]
  -
    match: "testdb.testschema.y"
    clustering:
      remove: [b]
```

A SQL translation with this configuration YAML file might look like the following:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><code>hive-input.sql</code></td>
<td><pre data-fenced=""><code>create table x(a int, b int);
    create table y(a int, b int) clustered by (b) into 16 buckets;</code></pre></td>
</tr>
<tr class="even">
<td><code>bq-output.sql</code></td>
<td><pre data-fenced=""><code>CREATE TABLE testdb.testschema.x
    (
      a INT64,
      b INT64
    )
    CLUSTER BY a;
    CREATE TABLE testdb.testschema.y
    (
      a INT64,
      b INT64
    )
    ;</code></pre></td>
</tr>
</tbody>
</table>

### Change type of a column attribute

> **Preview**
>
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

The following configuration YAML changes the data type for an attribute of a column:

```
type: object_rewriter
attribute:
  -
    match:
      database: testdb
      schema: testschema
      attributeRegex: "a+"
    type:
      target: NUMERIC(10,2)
```

You can transform the source data type to any of the [supported target attribute types](https://docs.cloud.google.com/bigquery/docs/config-yaml-translation#supported_target_attribute_types) .

A SQL translation with this configuration YAML file might look like the following:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><code>teradata-input.sql</code></td>
<td><pre data-fenced=""><code>create table x(a int, b int, aa int);</code></pre></td>
</tr>
<tr class="even">
<td><code>bq-output.sql</code></td>
<td><pre data-fenced=""><code>CREATE TABLE testdb.testschema.x
    (
      a NUMERIC(31, 2),
      b INT64,
      aa NUMERIC(31, 2)
    )
    ;</code></pre></td>
</tr>
</tbody>
</table>

> **Note:** BigQuery translation increases numeric precision to the highest precision available for a given scale.

### Add connection to external data lake

> **Preview**
>
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

The following configuration YAML marks the source table as being an external table that points to data stored in an external data lake, specified by a data lake connection.

```
type: object_rewriter
relation:
-
  key: "testdb.acme.employee"
  external:
    connection_id: "connection_test"
```

A SQL translation with this configuration YAML file might look like the following:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><code>hive-input.sql</code></td>
<td><pre data-fenced=""><code>CREATE TABLE x
    (
      a VARCHAR(150),
      b INT
    );</code></pre></td>
</tr>
<tr class="even">
<td><code>bq-output.sql</code></td>
<td><pre data-fenced=""><code>CREATE EXTERNAL TABLE x
    (
      a STRING,
      b INT64
    )
    WITH CONNECTION `connection_test`
    OPTIONS(
    );</code></pre></td>
</tr>
</tbody>
</table>

### Change the character encoding of an input file

> **Preview**
>
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

By default, the BigQuery Migration Service attempts to automatically detect the character encoding of input files. In cases where BigQuery Migration Service might misidentify the encoding of a file, you can use a configuration YAML to specify the character encoding explicitly.

The following configuration YAML specifies the explicit character encoding of the input file as `ISO-8859-1` .

```
type: experimental_input_formats
formats:
- source:
    pathGlob: "*.sql"
  contents:
    raw:
      charset: iso-8859-1
```

### Global type conversion

> **Preview**
>
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

The following configuration YAML changes a data type to another across all scripts, and specifies a source data type to avoid in the transpiled script. This is different from the [Change type of a column attribute](https://docs.cloud.google.com/bigquery/docs/config-yaml-translation#change_type_of_a_column_attribute) configuration, where only the data type for a single attribute is changed.

BigQuery supports the following data type conversions:

- `DATETIME` to `TIMESTAMP`
- `TIMESTAMP` to `DATETIME` (accepts optional time zone)
- `TIMESTAMP WITH TIME ZONE` to `DATETIME` (accepts optional time zone)
- `CHAR` to `VARCHAR`

In the following example, the configuration YAML converts a `TIMESTAMP` data type to `DATETIME` .

```
type: experimental_object_rewriter
global:
  typeConvert:
    timestamp: DATETIME
```

### Setting default time zone

> **Preview**
>
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

Database dialects have varying semantics and names for different date and time related data types. The translation service standardizes on the following terminology in its YAML configuration, regardless of the name of the input dialect's data type:

- A `datetime` is a combination of `Y-M-D H:M:S` that is not fixed to any particular time zone. `datetime` represents a wall-clock time and not a particular instant.
- A `timestamp` represents a particular, or absolute time instant and as such, is implicitly fixed to a particular time zone, which might be a session-level or database setting.
- A `timestamptz` represents a particular instant like a `timestamp` , but unlike a `timestamp` it carries with it a particular time zone offset. While they represent the same instant, `2019-06-01 12:00:00+4` and `2019-06-01 06:00:00-2` are considered different `timestamptz` values.

In dialects like Teradata, datetime-related functions such as `current_date` , `current_time` , or `current_timestamp` return timestamps based on an implicitly configured session time zone parameter. BigQuery, on the other hand, always returns timestamps in UTC. To ensure consistent behavior between the two dialects, it might be necessary to configure a time zone accordingly.

We recommend that you specify the default time zone for translation if your source database has a default that is not UTC. This will ensure correct behavior of the translated query by preserving the time zone.

In the following example, the configuration YAML converts a `TIMESTAMP` and a `TIMESTAMPTZ` data type to `DATETIME` , with the target time zone set to `Europe/Paris` .

For valid string time zone values, see [Time zones](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-types#time_zones) .

```
type: experimental_object_rewriter
global:
  typeConvert:
    timestamp:
      target: DATETIME
      timezone: Europe/Paris
    timestamptz:
      target: DATETIME
      timezone: Europe/Paris
```

A SQL translation with this configuration YAML file might look like the following:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><code>snowflake-input.sql</code></td>
<td><pre data-fenced=""><code>create table x(c_timestamp timestamp_ltz, c_timestamptz timestamp_tz, c_datetime timestamp_ntz);

      select c_timestamp from x where c_timestamp &gt; current_timestamp(0);
      select c_timestamptz from x where c_timestamptz &gt; cast(current_timestamp(0) as timestamp_tz);
      select c_datetime from x where c_datetime &gt; cast(current_timestamp(0) as timestamp_ntz);</code></pre></td>
</tr>
<tr class="even">
<td><code>bq-output.sql</code></td>
<td><pre data-fenced=""><code>CREATE TABLE x
      (
        c_timestamp DATETIME,
        c_timestamptz DATETIME,
        c_datetime DATETIME
      )
      ;
      SELECT
          x.c_timestamp
        FROM
          test.x
        WHERE x.c_timestamp &gt; datetime(current_timestamp(), &#39;Europe/Paris&#39;)
      ;
      SELECT
          x.c_timestamptz
        FROM
          test.x
        WHERE x.c_timestamptz &gt; datetime(current_timestamp(), &#39;Europe/Paris&#39;)
      ;
      SELECT
          x.c_datetime
        FROM
          test.x
        WHERE x.c_datetime &gt; datetime(current_timestamp(), &#39;Europe/Paris&#39;)
      ;</code></pre></td>
</tr>
</tbody>
</table>

In the following example, the configuration YAML converts a `DATETIME` data type to `TIMESTAMP` .

By default, `TIMESTAMPTZ` is converted to `TIMESTAMP` with no configuration required.

```
type: experimental_object_rewriter
global:
  typeConvert:
    datetime:
      target: TIMESTAMP
```

A SQL translation with this configuration YAML file might look like the following:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><code>snowflake-input.sql</code></td>
<td><pre data-fenced=""><code>create table x(c_timestamp timestamp_ltz, c_timestamptz timestamp_tz, c_datetime timestamp_ntz);

      select c_timestamp from x where c_timestamp &gt; current_timestamp(0);
      select c_timestamptz from x where c_timestamptz &gt; cast(current_timestamp(0) as timestamp_tz);
      select c_datetime from x where c_datetime &gt; cast(current_timestamp(0) as timestamp_ntz);</code></pre></td>
</tr>
<tr class="even">
<td><code>bq-output.sql</code></td>
<td><pre data-fenced=""><code>CREATE TABLE x
      (
        c_timestamp TIMESTAMP,
        c_timestamptz TIMESTAMP,
        c_datetime TIMESTAMP
      )
      ;
      SELECT
          x.c_timestamp
        FROM
          test.x
        WHERE x.c_timestamp &gt; current_timestamp()
      ;
      SELECT
          x.c_timestamptz
        FROM
          test.x
        WHERE x.c_timestamptz &gt; current_timestamp()
      ;
      SELECT
          x.c_datetime
        FROM
          test.x
        WHERE x.c_datetime &gt; current_timestamp()
      ;</code></pre></td>
</tr>
</tbody>
</table>

### Select statement modification

> **Preview**
>
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

The following configuration YAML changes the star projection, `GROUP BY` , and `ORDER BY` clauses in `SELECT` statements.

`starProjection` supports the following configurations:

- `ALLOW`
- `PRESERVE` (default)
- `EXPAND`

`groupBy` and `orderBy` support the following configurations:

- `EXPRESSION`
- `ALIAS`
- `INDEX`

In the following example, the configuration YAML configures the star projection to `EXPAND` .

```
type: experimental_statement_rewriter
select:
  starProjection: EXPAND
```

A SQL translation with this configuration YAML file might look like the following:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><code>teradata-input.sql</code></td>
<td><pre data-fenced=""><code>create table x(a int, b TIMESTAMP);
      select * from x;</code></pre></td>
</tr>
<tr class="even">
<td><code>bq-output.sql</code></td>
<td><pre data-fenced=""><code>CREATE TABLE x
      (
        a INT64,
        b DATETIME
      )
      ;
      SELECT
          x.a
          x.b
        FROM
          x
      ;</code></pre></td>
</tr>
</tbody>
</table>

### UDF specification

In most cases, the BigQuery SQL translator can automatically parse the data definition language (DDL) of external user-defined functions (UDFs) to determine their input and output data types, even if the UDF body is written in an external language. However, for certain source dialects, the translator might not be able to automatically compile the UDF signature. To ensure that SQL statements referencing these UDFs are translated accurately without having to supply the original DDL, you can use a YAML configuration file to explicitly register the UDF signatures.

The following configuration YAML specifies the signature of user-defined functions (UDFs) that are used in the source scripts. Much like [metadata zip files](https://docs.cloud.google.com/bigquery/docs/generate-metadata) , UDF definitions can help to produce a more accurate translation of input scripts.

```
type: metadata
udfs:
  - "date parse_short_date(dt int)"
```

A SQL translation with this configuration YAML file might look like the following:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><code>teradata-input.sql</code></td>
<td><pre data-fenced=""><code>create table x(dt int);
      select parse_short_date(dt) + 1 from x;</code></pre></td>
</tr>
<tr class="even">
<td><code>bq-output.sql</code></td>
<td><pre data-fenced=""><code>CREATE TABLE x
      (
        dt INT64
      )
      ;
      SELECT
          date_add(parse_short_date(x.dt), interval 1 DAY)
        FROM
          x
      ;</code></pre></td>
</tr>
</tbody>
</table>

### Setting decimal precision strictness

> **Preview**
>
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

By default, BigQuery Migration Service increases numeric precision to the highest precision available for a given scale. The following configuration YAML overrides this behavior by configuring the precision strictness to retain the decimal precision of the source statement.

```
type: experimental_statement_rewriter
common:
  decimalPrecision: STRICT
```

A SQL translation with this configuration YAML file might look like the following:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><code>teradata-input.sql</code></td>
<td><pre data-fenced=""><code>create table x(a decimal(3,0));</code></pre></td>
</tr>
<tr class="even">
<td><code>bq-output.sql</code></td>
<td><pre data-fenced=""><code>CREATE TABLE x
      (
        a NUMERIC(3)
      )
      ;</code></pre></td>
</tr>
</tbody>
</table>

### Setting string precision strictness

> **Preview**
>
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

By default, BigQuery Migration Service omits string precision when translating `CHAR` and `VARCHAR` columns. This can help prevent truncation errors when values are written. Some SQL dialects, such as Teradata, truncate values that exceed the maximum precision on write, while BigQuery returns an error in this scenario.

If your application doesn't rely on the source dialect's truncation behavior, consider preserving the column's precision in the translated type definition.

The following configuration YAML overrides this behavior by configuring the precision strictness to retain the string precision of the source statement.

```
type: experimental_statement_rewriter
common:
  stringPrecision: STRICT
```

A SQL translation with this configuration YAML file might look like the following:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><code>teradata-input.sql</code></td>
<td><pre data-fenced=""><code>create table x(a varchar(3));</code></pre></td>
</tr>
<tr class="even">
<td><code>bq-output.sql</code></td>
<td><pre data-fenced=""><code>CREATE TABLE x
      (
        a STRING(3)
      )
      ;</code></pre></td>
</tr>
</tbody>
</table>

### Output name mapping

> **Preview**
>
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

You can use configuration YAML to map SQL object names. You can change different parts of the name depending on the object being mapped.

#### Static name mapping

Use static name mapping to map the name of an entity. If you only want to change specific parts of the name while keeping other parts of the name the same, then only include the parts that need to change.

The following configuration YAML changes the name of the table from `my_db.my_schema.my_table` to `my_new_db.my_schema.my_new_table` .

```
type: experimental_object_rewriter
relation:
-
  match: "my_db.my_schema.my_table"
  outputName:
    database: "my_new_db"
    relation: "my_new_table"
```

A SQL translation with this configuration YAML file might look like the following:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><code>teradata-input.sql</code></td>
<td><pre data-fenced=""><code>create table my_db.my_schema.my_table(a int);</code></pre></td>
</tr>
<tr class="even">
<td><code>bq-output.sql</code></td>
<td><pre data-fenced=""><code>CREATE TABLE my_new_db.my_schema.my_new_table
      (
        a INT64
      )</code></pre></td>
</tr>
</tbody>
</table>

You can use static name mapping to update the region used by names in the [public user-defined functions](https://github.com/GoogleCloudPlatform/bigquery-utils/tree/master/udfs) .

The following example changes the names in the `bqutil.fn` UDF from using the default `us` multi-region to using the `europe_west2` region:

```
type: experimental_object_rewriter
function:
-
  match:
    database: bqutil
    schema: fn
  outputName:
    database: bqutil
    schema: fn_europe_west2
```

#### Dynamic name mapping

Use dynamic name mapping to change several objects at the same time, and create new names based on the mapped objects.

The following configuration YAML changes the name of all tables by adding the prefix `stg_` to those that belong to the `staging` schema, and then moves those tables to the `production` schema.

```
type: experimental_object_rewriter
relation:
-
  match:
    schema: staging
  outputName:
    schema: production
    relation: "stg_${relation}"
```

A SQL translation with this configuration YAML file might look like the following:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><code>teradata-input.sql</code></td>
<td><pre data-fenced=""><code>create table staging.my_table(a int);</code></pre></td>
</tr>
<tr class="even">
<td><code>bq-output.sql</code></td>
<td><pre data-fenced=""><code>CREATE TABLE production.stg_my_table
      (
        a INT64
      )
      ;</code></pre></td>
</tr>
</tbody>
</table>

### Specifying default database and schema search path

> **Preview**
>
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

The following configuration YAML specifies a [default database](https://docs.cloud.google.com/bigquery/docs/output-name-mapping#default_database) and [schema search path](https://docs.cloud.google.com/bigquery/docs/output-name-mapping#default_schema) .

```
type: environment
session:
  defaultDatabase: myproject
  schemaSearchPath: [myschema1, myschema2]
```

A SQL translation with this configuration YAML file might look like the following:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><code>teradata-input.sql</code></td>
<td><pre data-fenced=""><code>SELECT * FROM database.table
      SELECT * FROM table1</code></pre></td>
</tr>
<tr class="even">
<td><code>bq-output.sql</code></td>
<td><pre data-fenced=""><code>SELECT * FROM myproject.database.table.
      SELECT * FROM myproject.myschema1.table1</code></pre></td>
</tr>
</tbody>
</table>

### Setting `NLS_DATE_FORMAT`

> **Preview**
>
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

The following configuration YAML sets the `NLS_DATE_FORMAT` parameter to the format `DD/MM/YYYY` . We recommend that you specify `NLS_DATE_FORMAT` for implicit uses of date format and casts. If not set, the default format for translation, `DD-MON-RR` , is used.

```
type: environment
session:
  dateFormat: DD/MM/YYYY
```

A SQL translation with this configuration YAML file might look like the following:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><code>oracle-input.sql</code></td>
<td><pre data-fenced=""><code>create table x(dt date default &#39;31/12/1999&#39;);
    insert into x values (&#39;01/01/2000&#39;);</code></pre></td>
</tr>
<tr class="even">
<td><code>bq-output.sql</code></td>
<td><pre data-fenced=""><code>CREATE TABLE testdb.testschema.x
      (
        DT DATETIME DEFAULT DATETIME &#39;1999-12-31 00:00:00&#39;
      )
      ;
      INSERT INTO testdb.testschema.x (DT)
        VALUES (DATETIME &#39;2000-01-01 00:00:00&#39;)
      ;</code></pre></td>
</tr>
</tbody>
</table>

### Global output name rewrite

> **Preview**
>
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

The following configuration YAML changes the output names of all objects (database, schema, relation, and attributes) in the script according to the configured rules.

```
type: experimental_object_rewriter
global:
  outputName:
    regex:
      - match: '\s'
        replaceWith: '_'
      - match: '>='
        replaceWith: 'gte'
      - match: '^[^a-zA-Z_].*'
        replaceWith: '_$0'
```

A SQL translation with this configuration YAML file might look like the following:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><code>teradata-input.sql</code></td>
<td><pre data-fenced=""><code>create table &quot;test special chars &gt;= 12&quot;(&quot;42eid&quot; int, &quot;custom column&quot; varchar(10));</code></pre></td>
</tr>
<tr class="even">
<td><code>bq-output.sql</code></td>
<td><pre data-fenced=""><code>CREATE TABLE test_special_chars_employees_gte_12
      (
        _42eid INT64,
        custom_column STRING
      )
      ;</code></pre></td>
</tr>
</tbody>
</table>

### Optimize and improve the performance of translated SQL

Optional transformations can be applied to translated SQL in order to introduce changes that can improve performance or cost. These optimizations are strictly case dependent and should be evaluated against unmodified SQL output to assess their actual effect on performance.

The following configuration YAML enables optional transformations. The configuration accepts a list of optimizations and, for optimizations which accept parameters, a section with optional parameter values.

```
type: optimizer
transformations:
  - name: PRECOMPUTE_INDEPENDENT_SUBSELECTS
  - name: REWRITE_CTE_TO_TEMP_TABLE
    parameters:
      threshold: 1
```

| Optimization                                 | Optional parameter               | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|----------------------------------------------|----------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `PRECOMPUTE_INDEPENDENT_SUBSELECTS`          | `scope: [PREDICATE, PROJECTION]` | Rewrites the query by adding a `DECLARE` statement to replace an expression in either `PREDICATE` clauses or `PROJECTION` with a precomputed variable. This will be identified as a static predicate allowing for a reduction of the amount of data read. If the scope is omitted, the default value is `PREDICATE` (i.e. `WHERE` and `JOIN-ON` clause). Extracting a scalar subquery to a `DECLARE` statement will make the original predicate static and therefore qualify for improved execution planning. This optimization will introduce new SQL statements.                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `REWRITE_CTE_TO_TEMP_TABLE`                  | `threshold: N`                   | Rewrites common table expressions (CTE) to temporary tables when there are more than `N` references to the same common table expression. This reduces query complexity and forces single execution of the common table expression. If `N` is omitted, the default value is 4. We recommend using this optimization when non-trivial CTEs are referenced multiple times. Introducing temporary tables has an overhead that might be larger than eventual multiple executions of a low complexity or low cardinality CTE. This optimization will introduce new SQL statements.                                                                                                                                                                                                                                                                                                                                                                                                         |
| `REWRITE_ZERO_SCALE_NUMERIC_AS_INTEGER`      | `bigint: N`                      | Rewrites zero-scale `NUMERIC/BIGNUMERIC` attributes to `INT64` type if the precision is within `N` . If `N` is omitted, the default value is `18` . We recommend using this optimization when you translate from source dialects that don't have integer types. Changing column types requires reviewing all downstream uses for type compatibility and semantic changes. For example, fractional divisions becoming integer divisions, or code expecting numeric values. Snowflake translations have this optimization for zero-scale numerics up to precision 38 enabled by default. This optimization ensures that a Snowflake `INTEGER` , which is implicitly represented as `NUMBER(38,0)` in Snowflake, translates to a BigQuery `INT64` instead of a `BIGNUMERIC(38)` . If your application uses numbers with precisions that are over 18, we recommend disabling this functionality to ensure that BigQuery can process the full range of values needed by your application. |
| `DROP_TEMP_TABLE`                            |                                  | Adds `DROP TABLE` statements for all temporary tables created in a script and not dropped by the end of it. This reduces the storage billing period for the temporary table from 24 hours to the script running time. This optimization will introduce new SQL statements. We recommend using this optimization when temporary tables are not accessed for any further processing after the end of script execution. This optimization will introduce new SQL statements.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `REGEXP_CONTAINS_TO_LIKE`                    |                                  | Rewrites some categories of `REGEXP_CONTAINS` matching patterns to `LIKE` expressions. We recommend using this optimization when no other process, such as macro replacement, relies on the regular expression pattern literals being preserved unchanged in output SQL.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `ADD_DISTINCT_TO_SUBQUERY_IN_SET_COMPARISON` |                                  | Adds `DISTINCT` clause to subqueries used as value set for `[NOT] IN` operator. We recommend using this optimization when the cardinality (distinct number of values) of the subquery result is significantly lower than the number of values. When this precondition is not met this transformation can have negative effects on performance.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `APPROXIMATE_RANGE_PARTITIONS`               |                                  | Approximates non-contiguous or non-regular integer partitioning schemes by converting them to contiguous, equally sized partition ranges supported by BigQuery. By default, such partitioning schemes don't influence the table partitioning scheme in translated DDL statements. We recommend using this optimization when the source table uses a non-contiguous partitioning function like the Teradata `RANGE_N` function and would benefit from an equally sized partition scheme in BigQuery.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |

#### Optimization examples

The following optimization converts zero-scale numeric types with precision less than or equal to 38 to `INT64` in BigQuery.

```
# An INTEGER is internally represented as NUMBER(38,0) in Snowflake.
# To convert Snowflake INTEGER to INT64 in BigQuery, enable the rewrite for precision <= 38.
# Note that this can produce incorrect results if your application logic uses more than 18 digits of precision.
#
# This configuration is enabled by default for the Snowflake Dialect.
type: optimizer
transformations:
  - name: REWRITE_ZERO_SCALE_NUMERIC_AS_INTEGER
    parameters:
      bigint: 38
```

A SQL translation with this optimization might look like the following:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><code>snowflake-input.sql</code></td>
<td><pre data-fenced=""><code>CREATE TABLE numbers(i INTEGER, n NUMERIC(10,0));</code></pre></td>
</tr>
<tr class="even">
<td><code>bq-output.sql</code></td>
<td><pre data-fenced=""><code>CREATE TABLE numbers(i INT64, n INT64);</code></pre></td>
</tr>
</tbody>
</table>

The following configuration disables the optimization in dialects, such as Snowflake, where it is enabled by default. This configuration converts numeric types to either `NUMERIC` or `BIGNUMERIC` depending on the input precision, instead of the default of `INT64` .

```
type: optimizer
transformations:
  - name: REWRITE_ZERO_SCALE_NUMERIC_AS_INTEGER
    enabled: false
```

A SQL translation with this optimization might look like the following:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><code>snowflake-input.sql</code></td>
<td><pre data-fenced=""><code>CREATE TABLE numbers(i INTEGER, n NUMERIC(10,0));</code></pre></td>
</tr>
<tr class="even">
<td><code>bq-output.sql</code></td>
<td><pre data-fenced=""><code>CREATE TABLE numbers(i BIGNUMERIC(38), n NUMERIC(29));</code></pre></td>
</tr>
</tbody>
</table>

## Create a Gemini-based configuration YAML file

> **Note:** The translation service can call Gemini to generate suggestions for your SQL translation based on your `*.ai_config.yaml` file. For a comparison with deterministic `*.config.yaml` files and the order in which rules run, see [Types of configuration YAML files](https://docs.cloud.google.com/bigquery/docs/config-yaml-translation#config-types) .

To generate AI output, provide at least one `*.ai_config.yaml` file and enable Gemini AI suggestions when the interface requires it. For more information, see [Provide configuration files to a translation](https://docs.cloud.google.com/bigquery/docs/config-yaml-translation#provide-config-files) .

### Requirements

The configuration YAML file for AI outputs must have a suffix of `.ai_config.yaml` . For example, `rules_1.ai_config.yaml` .

### Supported fields

Unlike a `*.config.yaml` file, a `*.ai_config.yaml` file doesn't include a `type` header. Instead, the file contains a top-level `translation_rules` list, where each rule supports the following fields:

- `suggestion_type` (optional): Specify the type of AI suggestion to be generated. The following suggestion types are supported:
  - `QUERY_CUSTOMIZATION` (default): Generates AI suggestions for SQL code based on the translation rules specified in the `*.ai_config.yaml` file.
  - `TRANSLATION_EXPLANATION` : Generates text that includes a summary of the translated GoogleSQL query and the differences and inconsistencies between the source SQL query and the translated GoogleSQL query.
- `rewrite_target` (optional): Specify `SOURCE_SQL` to apply the rule to the original input SQL before the translation engine runs, or `TARGET_SQL` to apply the rule to the translated SQL that the translation engine produces. The default value is `TARGET_SQL` . For more information, see [How the two kinds of rules are applied](https://docs.cloud.google.com/bigquery/docs/config-yaml-translation#config-processing-order) .
- `instruction` (optional): Describe in natural language the change to apply to the input SQL or translated SQL for `QUERY_CUSTOMIZATION` rules, or the explanation to generate for `TRANSLATION_EXPLANATION` rules.
- `examples` (optional): Provide a list of `input` and `output` SQL pairs that show how you want a SQL pattern to be modified.

You can add additional `translation_rules` and additional `examples` as necessary.

### Examples

The following examples create Gemini-based configuration YAML files which you can use with your SQL translations.

#### Remove the upper function in the default translation output query

```
translation_rules:
- instruction: "Remove upper() function"
  examples:
  - input: "upper(X)"
    output: "X"
```

#### Create multiple translation rules to customize the translation output

```
translation_rules:
- instruction: "Remove upper() function"
  suggestion_type: QUERY_CUSTOMIZATION
  rewrite_target: TARGET_SQL
  examples:
  - input: "upper(X)"
    output: "X"
- instruction: "Insert a comment at the head that explains each statement in detail."
  suggestion_type: QUERY_CUSTOMIZATION
  rewrite_target: TARGET_SQL
```

#### Remove SQL comments from the translation input query

```
translation_rules:
- instruction: "Remove all the sql comments in the input sql query."
  suggestion_type: QUERY_CUSTOMIZATION
  rewrite_target: SOURCE_SQL
```

#### Generate translation explanations using default LLM prompt

This example uses the default LLM prompts provided by the translation service to generate text explanations:

```
translation_rules:
- suggestion_type: "TRANSLATION_EXPLANATION"
```

#### Generates translation explanations using your own natural language prompts

```
translation_rules:
- suggestion_type: "TRANSLATION_EXPLANATION"
  instruction: "Explain the syntax differences between the source Teradata query and the translated GoogleSQL query."
```

#### Multiple suggestion types in a single configuration YAML file

```
translation_rules:
- suggestion_type: "TRANSLATION_EXPLANATION"
  instruction: "Explain the syntax differences between the source Teradata query and the translated GoogleSQL query."
- instruction: "Remove upper() function"
  suggestion_type: QUERY_CUSTOMIZATION
  rewrite_target: TARGET_SQL
  examples:
  - input: "upper(X)"
    output: "X"
- instruction: "Remove all the sql comments in the input sql query."
  suggestion_type: QUERY_CUSTOMIZATION
  rewrite_target: SOURCE_SQL
```

## Applying multiple YAML configurations

When you translate a single query or batch SQL files, you can provide multiple configuration YAML files in a single translation job to reflect multiple transformations. If multiple configurations conflict, one transformation might override another. We recommend using different types of configuration settings in each file to avoid conflicting transformations in the same translation job.

The following example lists two separate configuration YAML files that were provided for a single SQL translation job, one to change a column's attribute, and the other to set the table as temporary:

`change-type-example.config.yaml` :

```
type: object_rewriter
attribute:
  -
    match: "testdb.testschema.x.a"
    type:
      target: NUMERIC(10,2)
```

`make-temp-example.config.yaml` :

```
type: object_rewriter
relation:
  -
    match: "testdb.testschema.x"
    temporary: true
```

A SQL translation with these two configuration YAML files might look like the following:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><code>teradata-input.sql</code></td>
<td><pre data-fenced=""><code>create table x(a int);</code></pre></td>
</tr>
<tr class="even">
<td><code>bq-output.sql</code></td>
<td><pre data-fenced=""><code>CREATE TEMPORARY TABLE x
    (
      a NUMERIC(31, 2)
    )
    ;</code></pre></td>
</tr>
</tbody>
</table>
