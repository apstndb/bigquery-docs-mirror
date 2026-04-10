# Snowflake SQL translation guide

This document details the similarities and differences in SQL syntax between Snowflake and BigQuery to help accelerate the planning and execution of moving your EDW (Enterprise Data Warehouse) to BigQuery. Snowflake data warehousing is designed to work with Snowflake-specific SQL syntax. Scripts written for Snowflake might need to be altered before you can use them in BigQuery, because the SQL dialects vary between the services. Use [batch SQL translation](https://docs.cloud.google.com/bigquery/docs/batch-sql-translator) to migrate your SQL scripts in bulk, or [interactive SQL translation](https://docs.cloud.google.com/bigquery/docs/interactive-sql-translator) to translate ad hoc queries. Snowflake SQL is supported by both tools in [preview](https://cloud.google.com/products#product-launch-stages) .

**Note:** In some cases, there is no direct mapping between a SQL element in Snowflake and BigQuery. However, in most cases, you can achieve the same functionality in BigQuery that you can in Snowflake using an alternative means, as shown in the examples in this document.

## Data types

This section shows equivalents between data types in Snowflake and in BigQuery.

  
  

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Snowflake</th>
<th>BigQuery</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         NUMBER/ DECIMAL/NUMERIC       </code></td>
<td><code dir="ltr" translate="no">         NUMERIC/BIGNUMERIC       </code></td>
<td>Can be mapped to <code dir="ltr" translate="no">       NUMERIC      </code> or <code dir="ltr" translate="no">       BIGNUMERIC      </code> , depending on precision and scale.<br />
<br />
The <code dir="ltr" translate="no">       NUMBER      </code> data type in Snowflake supports 38 digits of precision and 37 digits of scale. Precision and scale can be specified according to the user.<br />
<br />
BigQuery supports <code dir="ltr" translate="no">       NUMERIC      </code> and <code dir="ltr" translate="no">       BIGNUMERIC      </code> with <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-types#decimal_types">optionally specified precision and scale within certain bounds</a> .</td>
</tr>
<tr class="even">
<td><a href="https://docs.snowflake.com/en/sql-reference/data-types-numeric.html#int-integer-bigint-smallint-tinyint-byteint"><code dir="ltr" translate="no">        INT/INTEGER       </code></a></td>
<td><code dir="ltr" translate="no">         BIGNUMERIC       </code></td>
<td><code dir="ltr" translate="no">       INT/INTEGER      </code> and all other <code dir="ltr" translate="no">       INT      </code> -like datatypes, such as <code dir="ltr" translate="no">       BIGINT, TINYINT, SMALLINT, BYTEINT      </code> represent an alias for the <code dir="ltr" translate="no">       NUMBER      </code> datatype where the precision and scale cannot be specified and is always <code dir="ltr" translate="no">       NUMBER(38, 0)      </code><br />
<br />
BigQuery converts <code dir="ltr" translate="no">       INTEGER      </code> to <code dir="ltr" translate="no">       INT64      </code> by default. To configure the SQL translation to convert it to other data types, you can use the <a href="https://docs.cloud.google.com/bigquery/docs/config-yaml-translation#optimize_and_improve_the_performance_of_translated_sql"><code dir="ltr" translate="no">        REWRITE_ZERO_SCALE_NUMERIC_AS_INTEGER       </code> configuration option</a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         BIGINT       </code></td>
<td><code dir="ltr" translate="no">         BIGNUMERIC       </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         SMALLINT       </code></td>
<td><code dir="ltr" translate="no">         BIGNUMERIC       </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         TINYINT       </code></td>
<td><code dir="ltr" translate="no">         BIGNUMERIC       </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         BYTEINT       </code></td>
<td><code dir="ltr" translate="no">         BIGNUMERIC       </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         FLOAT/                FLOAT4/                FLOAT8       </code></td>
<td><code dir="ltr" translate="no">         FLOAT64       </code></td>
<td>The <code dir="ltr" translate="no">       FLOAT      </code> data type in Snowflake establishes 'NaN' as &gt; X, where X is any FLOAT value (other than 'NaN' itself).<br />
<br />
The <code dir="ltr" translate="no">       FLOAT      </code> data type in BigQuery establishes 'NaN' as &lt; X, where X is any FLOAT value (other than 'NaN' itself).</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         DOUBLE/                DOUBLE PRECISION/       </code><br />
<code dir="ltr" translate="no">         REAL       </code></td>
<td><code dir="ltr" translate="no">         FLOAT64       </code></td>
<td>The <code dir="ltr" translate="no">       DOUBLE      </code> data type in Snowflake is synonymous with the <code dir="ltr" translate="no">       FLOAT      </code> data type in Snowflake, but is commonly incorrectly displayed as <code dir="ltr" translate="no">       FLOAT      </code> . It is properly stored as <code dir="ltr" translate="no">       DOUBLE      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         VARCHAR       </code></td>
<td><code dir="ltr" translate="no">         STRING       </code></td>
<td>The <code dir="ltr" translate="no">       VARCHAR      </code> data type in Snowflake has a maximum length of 128 MB (uncompressed). If length is not specified, the default is the maximum length.<br />
<br />
The <code dir="ltr" translate="no">       STRING      </code> data type in BigQuery is stored as variable length UTF-8 encoded Unicode. For more information about column and row limits, see <a href="https://docs.cloud.google.com/bigquery/quotas#query_jobs">Query jobs</a> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         CHAR/CHARACTER       </code></td>
<td><code dir="ltr" translate="no">         STRING       </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         STRING/TEXT       </code></td>
<td><code dir="ltr" translate="no">         STRING       </code></td>
<td>The <code dir="ltr" translate="no">       STRING      </code> data type in Snowflake is synonymous with Snowflake's VARCHAR.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         BINARY       </code></td>
<td><code dir="ltr" translate="no">         BYTES       </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         VARBINARY       </code></td>
<td><code dir="ltr" translate="no">         BYTES       </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         BOOLEAN       </code></td>
<td><code dir="ltr" translate="no">         BOOL       </code></td>
<td>The <code dir="ltr" translate="no">       BOOL      </code> data type in BigQuery can only accept <code dir="ltr" translate="no">       TRUE/FALSE      </code> , unlike the <code dir="ltr" translate="no">       BOOL      </code> data type in Snowflake, which can accept TRUE/FALSE/NULL.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         DATE       </code></td>
<td><code dir="ltr" translate="no">         DATE       </code></td>
<td>The <code dir="ltr" translate="no">       DATE      </code> type in Snowflake accepts most common date formats, unlike the <code dir="ltr" translate="no">       DATE      </code> type in BigQuery, which only accepts dates in the format, 'YYYY-[M]M-[D]D'.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         TIME       </code></td>
<td><code dir="ltr" translate="no">         TIME       </code></td>
<td>The TIME type in Snowflake supports 0 to 9 nanoseconds of precision, whereas the TIME type in BigQuery supports 0 to 6 nanoseconds of precision.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         TIMESTAMP       </code></td>
<td><code dir="ltr" translate="no">         DATETIME       </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code> is a user-configurable alias which defaults to <code dir="ltr" translate="no">         TIMESTAMP_NTZ       </code> which maps to <code dir="ltr" translate="no">       DATETIME      </code> in BigQuery.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         TIMESTAMP_LTZ       </code></td>
<td><code dir="ltr" translate="no">         TIMESTAMP       </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         TIMESTAMP_NTZ/DATETIME        </code> <code dir="ltr" translate="no"></code></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         DATETIME       </code></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         TIMESTAMP_TZ       </code></td>
<td><code dir="ltr" translate="no">         TIMESTAMP       </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         OBJECT       </code></td>
<td><code dir="ltr" translate="no">         JSON       </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         VARIANT       </code></td>
<td><code dir="ltr" translate="no">         JSON       </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         ARRAY       </code></td>
<td><code dir="ltr" translate="no">         ARRAY&lt;JSON&gt;       </code></td>
<td>The SQL translation service preserves the data type for typed arrays. For untyped arrays, such as <code dir="ltr" translate="no">       ARRAY&lt;VARIANT&gt;      </code> , BigQuery converts these to <code dir="ltr" translate="no">       ARRAY&lt;JSON&gt;      </code></td>
</tr>
</tbody>
</table>

BigQuery also has the following data types which do not have a direct Snowflake analogue:

  - [`  DATETIME  `](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-types#datetime_type)
  - [`  GEOGRAPHY  `](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-types#geography_type)

## `     CREATE FUNCTION    ` syntax

The following table addresses differences in SQL UDF creation syntax between Snowflake and BigQuery.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Snowflake</strong></th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          CREATE [ OR REPLACE ] FUNCTION        </code></p>
<p><code dir="ltr" translate="no">        function_name       </code></p>
<p><code dir="ltr" translate="no">        ([sql_arg_name sql_arg_data_type[,..]])       </code></p>
<p><code dir="ltr" translate="no">        RETURNS data_type       </code></p>
<p><code dir="ltr" translate="no">        AS  sql_function_definition       </code></p>
<p><code dir="ltr" translate="no">        s       </code></p></td>
<td><p><code dir="ltr" translate="no">          CREATE [OR REPLACE] FUNCTION                function_name       </code></p>
<p><code dir="ltr" translate="no">        ([sql_arg_name sql_arg_data_type[,..]])       </code></p>
<p><code dir="ltr" translate="no">        AS sql_function_definition       </code></p>
<br />
Note: In BigQuery <a href="https://docs.cloud.google.com/bigquery/docs/user-defined-functions#sql-udf-structure">SQL UDF</a> , return data type is optional. BigQuery infers the result type of the function from the SQL function body when a query calls the function.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        CREATE [OR REPLACE] FUNCTION       </code></p>
<p><code dir="ltr" translate="no">        function_name       </code></p>
<p><code dir="ltr" translate="no">        ([sql_arg_name sql_arg_data_type[,..]])       </code></p>
<p><code dir="ltr" translate="no">        RETURNS TABLE (col_name, col_data_type[,..])       </code></p>
<p><code dir="ltr" translate="no">        AS  sql_function_definition       </code></p>
<br />
</td>
<td><p><code dir="ltr" translate="no">        CREATE [OR REPLACE] FUNCTION function_name       </code></p>
<p><code dir="ltr" translate="no">        ([sql_arg_name sql_arg_data_type[,..]])       </code></p>
<p><code dir="ltr" translate="no">        RETURNS data_type       </code></p>
<p><code dir="ltr" translate="no">        AS  sql_function_definition       </code></p>
<br />
Note:In BigQuery <a href="https://docs.cloud.google.com/bigquery/docs/user-defined-functions#sql-udf-structure">SQL UDF</a> , returning table type is not supported but is on the product roadmap and will be available soon. However, BigQuery supports returning ARRAY of type STRUCT.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          CREATE [SECURE] FUNCTION        </code></p>
<p><code dir="ltr" translate="no">        function_name       </code></p>
<p><code dir="ltr" translate="no">        ([sql_arg_name sql_arg_data_type[,..]])       </code></p>
<p><code dir="ltr" translate="no">        RETURNS data_type       </code></p>
<p><code dir="ltr" translate="no">        AS  sql_function_definition       </code></p>
<br />
Note: Snowflake provides secure option to restrict UDF definition and details only to authorized users (that is, users who are granted the role that owns the view).</td>
<td><p><code dir="ltr" translate="no">          CREATE FUNCTION        </code></p>
<p><code dir="ltr" translate="no">        function_name       </code></p>
<p><code dir="ltr" translate="no">        ([sql_arg_name sql_arg_data_type[,..]])       </code></p>
<p><code dir="ltr" translate="no">        RETURNS data_type       </code></p>
<p><code dir="ltr" translate="no">        AS  sql_function_definition       </code></p>
<br />
Note: Function security is not a configurable parameter in BigQuery. BigQuery supports creating IAM roles and permissions to restrict access to underlying data and function definition.<br />
</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        CREATE [OR REPLACE] FUNCTION       </code></p>
<p><code dir="ltr" translate="no">        function_name       </code></p>
<p><code dir="ltr" translate="no">        ([sql_arg_name sql_arg_data_type[,..]])       </code></p>
<p><code dir="ltr" translate="no">        RETURNS data_type       </code></p>
<p><code dir="ltr" translate="no">        [ { CALLED ON NULL INPUT | { RETURNS NULL ON NULL INPUT | STRICT } } ]       </code></p>
<p><code dir="ltr" translate="no">        AS   sql_function_definition       </code></p></td>
<td><p><code dir="ltr" translate="no">        CREATE [OR REPLACE] FUNCTION function_name       </code></p>
<p><code dir="ltr" translate="no">        ([sql_arg_name sql_arg_data_type[,..]])       </code></p>
<p><code dir="ltr" translate="no">        RETURNS data_type       </code></p>
<p><code dir="ltr" translate="no">        AS  sql_function_definition       </code></p>
<br />
Note: Function behaviour for null inputs is implicitly handled in BigQuery and need not be specified as a separate option.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        CREATE [OR REPLACE] FUNCTION       </code></p>
<p><code dir="ltr" translate="no">        function_name       </code></p>
<p><code dir="ltr" translate="no">        ([sql_arg_name sql_arg_data_type[,..]])       </code></p>
<p><code dir="ltr" translate="no">        RETURNS data_type       </code></p>
<p><code dir="ltr" translate="no">        [VOLATILE | IMMUTABLE]       </code></p>
<p><code dir="ltr" translate="no">        AS   sql_function_definition       </code></p></td>
<td><p><code dir="ltr" translate="no">        CREATE [OR REPLACE] FUNCTION       </code></p>
<p><code dir="ltr" translate="no">        function_name       </code></p>
<p><code dir="ltr" translate="no">        ([sql_arg_name sql_arg_data_type[,..]])       </code></p>
<p><code dir="ltr" translate="no">        RETURNS data_type       </code></p>
<p><code dir="ltr" translate="no">        AS  sql_function_definition       </code></p>
<br />
Note:Function volatility is not a configurable parameter in BigQuery. All BigQuery UDF volatility is equivalent to Snowflake's <code dir="ltr" translate="no">       IMMUTABLE      </code> volatility (that is, it does not do database lookups or otherwise use information not directly present in its argument list).</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        CREATE [OR REPLACE] FUNCTION       </code></p>
<p><code dir="ltr" translate="no">        function_name       </code></p>
<p><code dir="ltr" translate="no">        ([sql_arg_name sql_arg_data_type[,..]])       </code></p>
<p><code dir="ltr" translate="no">        RETURNS data_type       </code></p>
<p><code dir="ltr" translate="no">        AS [' | $$]       </code></p>
<p><code dir="ltr" translate="no">        sql_function_definition       </code></p>
<p><code dir="ltr" translate="no">        [' | $$]       </code></p></td>
<td><code dir="ltr" translate="no">         CREATE [OR REPLACE] FUNCTION       </code><br />

<p><code dir="ltr" translate="no">        function_name       </code></p>
<p><code dir="ltr" translate="no">        ([sql_arg_name sql_arg_data_type[,..]])       </code></p>
<p><code dir="ltr" translate="no">        RETURNS data_type       </code></p>
<p><code dir="ltr" translate="no">        AS  sql_function_definition       </code></p>
<br />
Note: Using single quotes or a character sequence like dollar quoting ($$) is not required or supported in BigQuery. BigQuery implicitly interprets the SQL expression.<br />
</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        CREATE [OR REPLACE] FUNCTION       </code></p>
<p><code dir="ltr" translate="no">        function_name       </code></p>
<p><code dir="ltr" translate="no">        ([sql_arg_name sql_arg_data_type[,..]])       </code></p>
<p><code dir="ltr" translate="no">        RETURNS data_type       </code></p>
<p><code dir="ltr" translate="no">        [COMMENT = '&lt;string_literal&gt;']       </code></p>
<p><code dir="ltr" translate="no">        AS   sql_function_definition       </code></p></td>
<td><p><code dir="ltr" translate="no">        CREATE [OR REPLACE] FUNCTION       </code></p>
<p><code dir="ltr" translate="no">        function_name       </code></p>
<p><code dir="ltr" translate="no">        ([sql_arg_name sql_arg_data_type[,..]])       </code></p>
<p><code dir="ltr" translate="no">        RETURNS data_type       </code></p>
<p><code dir="ltr" translate="no">        AS  sql_function_definition       </code></p>
<br />
Note: Adding comments or descriptions in UDFs is not supported in BigQuery.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        CREATE [OR REPLACE] FUNCTION function_name       </code></p>
<p><code dir="ltr" translate="no">        (x integer, y integer)       </code></p>
<p><code dir="ltr" translate="no">        RETURNS integer       </code></p>
<p><code dir="ltr" translate="no">        AS $$       </code></p>
<p><code dir="ltr" translate="no">        SELECT x + y       </code></p>
<p><code dir="ltr" translate="no">        $$       </code></p>
<br />
Note: Snowflake does not support ANY TYPE for SQL UDFs. However, it supports using <a href="https://docs.snowflake.net/manuals/sql-reference/data-types-semistructured.html#variant">VARIANT</a> data types.</td>
<td><p><code dir="ltr" translate="no">        CREATE [OR REPLACE] FUNCTION function_name       </code></p>
<p><code dir="ltr" translate="no">        (x ANY TYPE, y ANY TYPE)       </code></p>
<p><code dir="ltr" translate="no">        AS       </code></p>
<p><code dir="ltr" translate="no">        SELECT x + y       </code></p>
<br />
<br />
Note: BigQuery supports using ANY TYPE as argument type. The function will accept an input of any type for this argument. For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/user-defined-functions#templated-sql-udf-parameters">templated parameter</a> in BigQuery.</td>
</tr>
</tbody>
</table>

BigQuery also supports the `  CREATE FUNCTION IF NOT EXISTS  ` statement which treats the query as successful and takes no action if a function with the same name already exists.

BigQuery's `  CREATE FUNCTION  ` statement also supports creating [`  TEMPORARY or TEMP functions  `](https://docs.cloud.google.com/bigquery/docs/user-defined-functions) , which do not have a Snowflake equivalent. See [calling UDFs](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/syntax#calling_persistent_user-defined_functions_udfs) for details on executing a BigQuery persistent UDF.

## `     DROP FUNCTION    ` syntax

The following table addresses differences in DROP FUNCTION syntax between Snowflake and BigQuery.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Snowflake</strong></th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          DROP FUNCTION                [IF EXISTS]       </code></p>
<p><code dir="ltr" translate="no">        function_name       </code></p>
<p><code dir="ltr" translate="no">        ([arg_data_type, ... ])       </code></p></td>
<td><p><code dir="ltr" translate="no">          DROP FUNCTION                [IF EXISTS] dataset_name.function_name       </code></p>
<br />
Note: BigQuery does not require using the function's signature (argument data type) for deleting the function.</td>
</tr>
</tbody>
</table>

BigQuery requires that you specify the `  project_name  ` if the function is not located in the current project.

## Additional function commands

This section covers additional UDF commands supported by Snowflake that are not directly available in BigQuery.

### `     ALTER FUNCTION    ` syntax

Snowflake supports the following operations using [`  ALTER FUNCTION  `](https://docs.snowflake.net/manuals/sql-reference/sql/alter-function.html) syntax.

  - Renaming a UDF
  - Converting to (or reverting from) a secure UDF
  - Adding, overwriting, removing a comment for a UDF

As configuring function security and adding function comments is not available in BigQuery, `  ALTER FUNCTION  ` syntax is not supported. However, the [CREATE FUNCTION](https://docs.cloud.google.com/bigquery/docs/user-defined-functions#sql-udf-structure) statement can be used to create a UDF with the same function definition but a different name.

### `     DESCRIBE FUNCTION    ` syntax

Snowflake supports describing a UDF using [DESC\[RIBE\] FUNCTION](https://docs.snowflake.net/manuals/sql-reference/sql/desc-function.html) syntax. This is not supported in BigQuery. However, querying UDF metadata via INFORMATION SCHEMA will be available soon as part of the product roadmap.

### `     SHOW USER FUNCTIONS    ` syntax

In Snowflake, [SHOW USER FUNCTIONS](https://docs.snowflake.net/manuals/sql-reference/sql/show-user-functions.html) syntax can be used to list all UDFs for which users have access privileges. This is not supported in BigQuery. However, querying UDF metadata via INFORMATION SCHEMA will be available soon as part of the product roadmap.

## Stored procedures

Snowflake [stored procedures](https://docs.snowflake.net/manuals/sql-reference/stored-procedures-usage.html) are written in JavaScript, which can execute SQL statements by calling a JavaScript API. In BigQuery, stored procedures are defined using a [block](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/scripting#begin) of SQL statements.

### `     CREATE PROCEDURE    ` syntax

In Snowflake, a stored procedure is executed with a [CALL](https://docs.snowflake.net/manuals/sql-reference/sql/call.html) command while in BigQuery, stored procedures are [executed](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_procedure) like any other BigQuery function.

The following table addresses differences in stored procedure creation syntax between Snowflake and BigQuery.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Snowflake</strong></th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          CREATE [OR REPLACE] PROCEDURE        </code></p>
<p><code dir="ltr" translate="no">        procedure_name       </code></p>
<p><code dir="ltr" translate="no">        ([arg_name arg_data_type[,..]])       </code></p>
<p><code dir="ltr" translate="no">        RETURNS data_type       </code></p>
<p><code dir="ltr" translate="no">        AS procedure_definition;       </code></p>
<br />
Note: Snowflake requires that stored procedures return a single value. Hence, return data type is a required option.</td>
<td><code dir="ltr" translate="no">         CREATE [OR REPLACE] PROCEDURE       </code><br />

<p><code dir="ltr" translate="no">        procedure_name       </code></p>
<p><code dir="ltr" translate="no">        ([arg_mode arg_name arg_data_type[,..]])       </code></p>
<p><code dir="ltr" translate="no">        BEGIN       </code></p>
<p><code dir="ltr" translate="no">        procedure_definition       </code></p>
<p><code dir="ltr" translate="no">        END;       </code></p>
<br />

<p><code dir="ltr" translate="no">        arg_mode: IN | OUT | INOUT       </code></p>
<br />
Note: BigQuery doesn't support a return type for stored procedures. Also, it requires specifying argument mode for each argument passed.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        CREATE [OR REPLACE] PROCEDURE       </code></p>
<p><code dir="ltr" translate="no">        procedure_name       </code></p>
<p><code dir="ltr" translate="no">        ([arg_name arg_data_type[,..]])       </code></p>
<p><code dir="ltr" translate="no">        RETURNS data_type       </code></p>
<p><code dir="ltr" translate="no">        AS       </code></p>
<p><code dir="ltr" translate="no">        $$       </code></p>
<p><code dir="ltr" translate="no">        javascript_code       </code></p>
<p><code dir="ltr" translate="no">        $$;       </code></p></td>
<td><p><code dir="ltr" translate="no">        CREATE [OR REPLACE] PROCEDURE       </code></p>
<p><code dir="ltr" translate="no">        procedure_name       </code></p>
<p><code dir="ltr" translate="no">        ([arg_name arg_data_type[,..]])       </code></p>
<p><code dir="ltr" translate="no">        BEGIN       </code></p>
<p><code dir="ltr" translate="no">        statement_list       </code></p>
<p><code dir="ltr" translate="no">        END;       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        CREATE [OR REPLACE] PROCEDURE       </code></p>
<p><code dir="ltr" translate="no">        procedure_name       </code></p>
<p><code dir="ltr" translate="no">        ([arg_name arg_data_type[,..]])       </code></p>
<p><code dir="ltr" translate="no">        RETURNS data_type       </code></p>
<p><code dir="ltr" translate="no">        [{CALLED ON NULL INPUT | {RETURNS NULL ON NULL INPUT | STRICT}}]       </code></p>
<p><code dir="ltr" translate="no">        AS procedure_definition;       </code></p></td>
<td><code dir="ltr" translate="no">         CREATE [OR REPLACE] PROCEDURE       </code><br />

<p><code dir="ltr" translate="no">        procedure_name       </code></p>
<p><code dir="ltr" translate="no">        ([arg_name arg_data_type[,..]])       </code></p>
<p><code dir="ltr" translate="no">        BEGIN       </code></p>
<p><code dir="ltr" translate="no">        procedure_definition       </code></p>
<p><code dir="ltr" translate="no">        END;       </code></p>
<br />
Note: Procedure behavior for null inputs is implicitly handled in BigQuery and need not be specified as a separate option.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         CREATE [OR REPLACE] PROCEDURE       </code><br />

<p><code dir="ltr" translate="no">        procedure_name       </code></p>
<p><code dir="ltr" translate="no">        ([arg_name arg_data_type[,..]])       </code></p>
<p><code dir="ltr" translate="no">        RETURNS data_type       </code></p>
<p><code dir="ltr" translate="no">        [VOLATILE | IMMUTABLE]       </code></p>
<p><code dir="ltr" translate="no">        AS procedure_definition;       </code></p></td>
<td><p><code dir="ltr" translate="no">        CREATE [OR REPLACE] PROCEDURE       </code></p>
<p><code dir="ltr" translate="no">        procedure_name       </code></p>
<p><code dir="ltr" translate="no">        ([arg_name arg_data_type[,..]])       </code></p>
<p><code dir="ltr" translate="no">        BEGIN       </code></p>
<p><code dir="ltr" translate="no">        procedure_definition       </code></p>
<p><code dir="ltr" translate="no">        END;       </code></p>
<br />
Note:Procedure volatility is not a configurable parameter in BigQuery. It's equivalent to Snowflake's <code dir="ltr" translate="no">       IMMUTABLE      </code> volatility.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         CREATE [OR REPLACE] PROCEDURE       </code><br />

<p><code dir="ltr" translate="no">        procedure_name       </code></p>
<p><code dir="ltr" translate="no">        ([arg_name arg_data_type[,..]])       </code></p>
<p><code dir="ltr" translate="no">        RETURNS data_type       </code></p>
<p><code dir="ltr" translate="no">        [COMMENT = '&lt;string_literal&gt;']       </code></p>
<p><code dir="ltr" translate="no">        AS   procedure_definition;       </code></p></td>
<td><p><code dir="ltr" translate="no">        CREATE [OR REPLACE] PROCEDURE       </code></p>
<p><code dir="ltr" translate="no">        procedure_name       </code></p>
<p><code dir="ltr" translate="no">        ([arg_name arg_data_type[,..]])       </code></p>
<p><code dir="ltr" translate="no">        BEGIN       </code></p>
<p><code dir="ltr" translate="no">        procedure_definition       </code></p>
<p><code dir="ltr" translate="no">        END;       </code></p>
<br />
Note: Adding comments or descriptions in procedure definitions is not supported in BigQuery.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         CREATE [OR REPLACE] PROCEDURE       </code><br />

<p><code dir="ltr" translate="no">        procedure_name       </code></p>
<p><code dir="ltr" translate="no">        ([arg_name arg_data_type[,..]])       </code></p>
<p><code dir="ltr" translate="no">        RETURNS data_type       </code></p>
<p><code dir="ltr" translate="no">        [EXECUTE AS { CALLER | OWNER }]       </code></p>
<p><code dir="ltr" translate="no">        AS procedure_definition;       </code></p>
<br />
Note: Snowflake supports specifying the caller or owner of the procedure for execution</td>
<td><p><code dir="ltr" translate="no">        CREATE [OR REPLACE] PROCEDURE       </code></p>
<p><code dir="ltr" translate="no">        procedure_name       </code></p>
<p><code dir="ltr" translate="no">        ([arg_name arg_data_type[,..]])       </code></p>
<p><code dir="ltr" translate="no">        BEGIN       </code></p>
<p><code dir="ltr" translate="no">        procedure_definition       </code></p>
<p><code dir="ltr" translate="no">        END;       </code></p>
<br />
Note: BigQuery stored procedures are always executed as the caller</td>
</tr>
</tbody>
</table>

BigQuery also supports the `  CREATE PROCEDURE IF NOT EXISTS  ` statement which treats the query as successful and takes no action if a function with the same name already exists.

### `     DROP PROCEDURE    ` syntax

The following table addresses differences in DROP FUNCTION syntax between Snowflake and BigQuery.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Snowflake</strong></th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          DROP PROCEDURE                [IF EXISTS]       </code></p>
<p><code dir="ltr" translate="no">        procedure_name       </code></p>
<p><code dir="ltr" translate="no">        ([arg_data_type, ... ])       </code></p></td>
<td><p><code dir="ltr" translate="no">          DROP PROCEDURE                [IF EXISTS] dataset_name.procedure_name       </code></p>
<br />
Note: BigQuery does not require using procedure's signature (argument data type) for deleting the procedure.</td>
</tr>
</tbody>
</table>

BigQuery requires that you specify the `  project_name  ` if the procedure is not located in the current project.

### Additional procedure commands

Snowflake provides additional commands like [`  ALTER PROCEDURE  `](https://docs.snowflake.net/manuals/sql-reference/sql/alter-procedure.html) , [`  DESC[RIBE] PROCEDURE  `](https://docs.snowflake.net/manuals/sql-reference/sql/desc-procedure.html) , and [`  SHOW PROCEDURES  `](https://docs.snowflake.net/manuals/sql-reference/sql/show-procedures.html) to manage the stored procedures. These are not supported in BigQuery.

## Metadata and transaction SQL statements

| **Snowflake**                                                                                                                                                                                   | BigQuery                                                                                                                                                                                                                             |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `           BEGIN                [ { WORK \| TRANSACTION } ] [ NAME <name> ];  START_TRANSACTION [ name <name> ];        `                                                                      | BigQuery always uses Snapshot Isolation. For details, see [Consistency guarantees](https://docs.cloud.google.com/bigquery/docs/migration/snowflake-sql#consistency-guarantees-and-transaction-isolation) elsewhere in this document. |
| `         COMMIT;        `                                                                                                                                                                      | Not used in BigQuery.                                                                                                                                                                                                                |
| `         ROLLBACK;        `                                                                                                                                                                    | Not used in BigQuery                                                                                                                                                                                                                 |
| `         SHOW LOCKS [ IN ACCOUNT ]; SHOW TRANSACTIONS [ IN ACCOUNT ];  Note: If the user has the ACCOUNTADMIN role, the user can see locks/transactions for all users in the account.        ` | Not used in BigQuery.                                                                                                                                                                                                                |

## Multi-statement and multi-line SQL statements

Both Snowflake and BigQuery support transactions (sessions) and therefore support statements separated by semicolons that are consistently executed together. For more information, see [Multi-statement transactions](https://docs.cloud.google.com/bigquery/docs/transactions) .

## Metadata columns for staged files

Snowflake automatically generates metadata for files in internal and external stages. This metadata can be [queried](https://docs.snowflake.net/manuals/user-guide/querying-stage.html) and [loaded](https://docs.snowflake.net/manuals/sql-reference/sql/copy-into-table.html) into a table alongside regular data columns. The following metadata columns can be utilized:

  - [METADATA$FILENAME](https://docs.snowflake.net/manuals/user-guide/querying-metadata.html#metadata-columns)
  - [METADATA$FILE\_ROW\_NUMBER](https://docs.snowflake.net/manuals/user-guide/querying-metadata.html#metadata-columns)

## Consistency guarantees and transaction isolation

Both Snowflake and BigQuery are atomic—that is, ACID-compliant on a per-mutation level across many rows.

### Transactions

Each Snowflake transaction is assigned a unique start time (includes milliseconds) that is set as the transaction ID. Snowflake only supports the [`  READ COMMITTED  `](https://docs.snowflake.net/manuals/sql-reference/transactions.html#read-committed-isolation) isolation level. However, a statement can see changes made by another statement if they are both in the same transaction - even though those changes are not committed yet. Snowflake transactions acquire locks on resources (tables) when that resource is being modified. Users can adjust the maximum time a blocked statement will wait until the statement times out. DML statements are autocommitted if the [`  AUTOCOMMIT  `](https://docs.snowflake.net/manuals/sql-reference/parameters.html#autocommit) parameter is turned on.

BigQuery also [supports transactions](https://docs.cloud.google.com/bigquery/docs/transactions) . BigQuery helps ensure [optimistic concurrency control](https://en.wikipedia.org/wiki/Optimistic_concurrency_control) (first to commit wins) with [snapshot isolation](https://en.wikipedia.org/wiki/Snapshot_isolation) , in which a query reads the last committed data before the query starts. This approach guarantees the same level of consistency on a per-row, per-mutation basis and across rows within the same DML statement, yet avoids deadlocks. In the case of multiple DML updates against the same table, BigQuery switches to [pessimistic concurrency control](https://docs.cloud.google.com/bigquery/docs/data-manipulation-language#dml-limitations) . Load jobs can run completely independently and append to tables. However, BigQuery does not provide an explicit transaction boundary or session.

## Rollback

If a Snowflake transaction's session is unexpectedly terminated before the transaction is committed or rolled back, the transaction is left in a detached state. The user should run SYSTEM$ABORT\_TRANSACTION to abort the detached transaction or Snowflake will roll back the detached transaction after four idle hours. If a deadlock occurs, Snowflake detects the deadlock and selects the more recent statement to roll back. If the DML statement in an explicitly opened transaction fails, the changes are rolled back, but the transaction is kept open until it is committed or rolled back. DDL statements in Snowflake cannot be rolled back as they are autocommitted.

BigQuery supports the [`  ROLLBACK TRANSACTION  ` statement](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/procedural-language#rollback_transaction) . There is no [`  ABORT  ` statement](https://docs.teradata.com/reader/huc7AEHyHSROUkrYABqNIg/c6KYQ4ySu4QTCkKS4f5A2w) in BigQuery.

## Database limits

Always check [the BigQuery public documentation](https://docs.cloud.google.com/bigquery/quotas) for the latest quotas and limits. Many quotas for large-volume users can be raised by contacting the Cloud Support team.

All Snowflake accounts have soft-limits set by default. Soft-limits are set during account creation and can vary. Many Snowflake soft-limits can be raised through the Snowflake account team or a support ticket.

The following table shows a comparison of the Snowflake and BigQuery database limits.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Limit</strong></th>
<th><strong>Snowflake</strong></th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Size of query text</td>
<td>1 MB</td>
<td>1 MB</td>
</tr>
<tr class="even">
<td>Maximum number of concurrent queries</td>
<td>XS Warehouse - 8<br />
S Warehouse - 16<br />
M Warehouse - 32<br />
<em>L Warehouse - 64<br />
XL Warehouse - 128</em></td>
<td>100</td>
</tr>
</tbody>
</table>
