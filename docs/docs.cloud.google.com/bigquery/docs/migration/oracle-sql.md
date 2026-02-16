# Oracle SQL translation guide

This document details the similarities and differences in SQL syntax between Oracle and BigQuery to help you plan your migration. Use [batch SQL translation](/bigquery/docs/batch-sql-translator) to migrate your SQL scripts in bulk, or [interactive SQL translation](/bigquery/docs/interactive-sql-translator) to translate ad-hoc queries.

**Note:** In some cases, there is no direct mapping between a SQL element in Oracle and BigQuery. However, in most cases, you can achieve the same functionality in BigQuery that you can in Oracle using an alternative means, as shown in the examples in this document.

## Data types

This section shows equivalents between data types in Oracle and in BigQuery.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Oracle</th>
<th>BigQuery</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         VARCHAR2       </code></td>
<td><code dir="ltr" translate="no">         STRING       </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         NVARCHAR2       </code></td>
<td><code dir="ltr" translate="no">         STRING       </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         CHAR       </code></td>
<td><code dir="ltr" translate="no">         STRING       </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         NCHAR       </code></td>
<td><code dir="ltr" translate="no">         STRING       </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         CLOB       </code></td>
<td><code dir="ltr" translate="no">         STRING       </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         NCLOB       </code></td>
<td><code dir="ltr" translate="no">         STRING       </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         INTEGER       </code></td>
<td><code dir="ltr" translate="no">         INT64       </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         SHORTINTEGER       </code></td>
<td><code dir="ltr" translate="no">         INT64       </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         LONGINTEGER       </code></td>
<td><code dir="ltr" translate="no">         INT64       </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         NUMBER       </code></td>
<td><code dir="ltr" translate="no">         NUMERIC       </code></td>
<td>BigQuery does not allow user specification of custom values for precision or scale. As a result, a column in Oracle may be defined so that it has a bigger scale than BigQuery supports.
<p>Additionally, before storing a decimal number Oracle rounds up if that number has more digits after the decimal point than is specified for the corresponding column. In BigQuery this feature could be implemented using <code dir="ltr" translate="no">        ROUND()       </code> function.</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         NUMBER(*, x)       </code></td>
<td><code dir="ltr" translate="no">         NUMERIC       </code></td>
<td>BigQuery does not allow user specification of custom values for precision or scale. As a result, a column in Oracle may be defined so that it has a bigger scale than BigQuery supports.
<p>Additionally, before storing a decimal number Oracle rounds up if that number has more digits after the decimal point than is specified for the corresponding column. In BigQuery this feature could be implemented using <code dir="ltr" translate="no">        ROUND()       </code> function.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         NUMBER(x, -y)       </code></td>
<td><code dir="ltr" translate="no">         INT64       </code></td>
<td>If a user tries to store a decimal number, Oracle rounds it up to a whole number. For BigQuery an attempt to store a decimal number in a column defined as <code dir="ltr" translate="no">       INT64      </code> results in an error. In this case, <code dir="ltr" translate="no">       ROUND()      </code> function should be applied.
<p>BigQuery <code dir="ltr" translate="no">        INT64       </code> data types allow up to 18 digits of precision. If a number field has more than 18 digits, <code dir="ltr" translate="no">        FLOAT64       </code> data type should be used in BigQuery.</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         NUMBER(x)       </code></td>
<td><code dir="ltr" translate="no">         INT64       </code></td>
<td>If a user tries to store a decimal number, Oracle rounds it up to a whole number. For BigQuery an attempt to store a decimal number in a column defined as <code dir="ltr" translate="no">       INT64      </code> results in an error. In this case, <code dir="ltr" translate="no">       ROUND()      </code> function should be applied.
<p>BigQuery <code dir="ltr" translate="no">        INT64       </code> data types allow up to 18 digits of precision. If a number field has more than 18 digits, <code dir="ltr" translate="no">        FLOAT64       </code> data type should be used in BigQuery.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       FLOAT      </code></td>
<td><code dir="ltr" translate="no">         FLOAT64       </code> / <code dir="ltr" translate="no">         NUMERIC       </code></td>
<td><code dir="ltr" translate="no">       FLOAT      </code> is an exact data type, and it's a <code dir="ltr" translate="no">       NUMBER      </code> subtype in Oracle. In BigQuery, <code dir="ltr" translate="no">       FLOAT64      </code> is an approximate data type. <code dir="ltr" translate="no">       NUMERIC      </code> may be a better match for <code dir="ltr" translate="no">       FLOAT      </code> type in BigQuery.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         BINARY_DOUBLE       </code></td>
<td><code dir="ltr" translate="no">         FLOAT64       </code> / <code dir="ltr" translate="no">         NUMERIC       </code></td>
<td><code dir="ltr" translate="no">       FLOAT      </code> is an exact data type, and it's a <code dir="ltr" translate="no">       NUMBER      </code> subtype in Oracle. In BigQuery, <code dir="ltr" translate="no">       FLOAT64      </code> is an approximate data type. <code dir="ltr" translate="no">       NUMERIC      </code> may be a better match for <code dir="ltr" translate="no">       FLOAT      </code> type in BigQuery.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         BINARY_FLOAT       </code></td>
<td><code dir="ltr" translate="no">         FLOAT64       </code> / <code dir="ltr" translate="no">         NUMERIC       </code></td>
<td><code dir="ltr" translate="no">       FLOAT      </code> is an exact data type, and it's a <code dir="ltr" translate="no">       NUMBER      </code> subtype in Oracle. In BigQuery, <code dir="ltr" translate="no">       FLOAT64      </code> is an approximate data type. <code dir="ltr" translate="no">       NUMERIC      </code> may be a better match for <code dir="ltr" translate="no">       FLOAT      </code> type in BigQuery.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       LONG      </code></td>
<td><code dir="ltr" translate="no">         BYTES       </code></td>
<td><code dir="ltr" translate="no">       LONG      </code> data type is used in earlier versions and is not suggested in new versions of Oracle Database.
<p><code dir="ltr" translate="no">        BYTES       </code> data type in BigQuery can be used if it is necessary to hold <code dir="ltr" translate="no">        LONG       </code> data in BigQuery. A better approach would be putting binary objects in Cloud Storage and holding references in BigQuery.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       BLOB      </code></td>
<td><code dir="ltr" translate="no">         BYTES       </code></td>
<td><code dir="ltr" translate="no">       BYTES      </code> data type can be used to store variable-length binary data. If this field is not queried and not used in analytics, a better option is to store binary data in Cloud Storage.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         BFILE       </code></td>
<td><code dir="ltr" translate="no">         STRING       </code></td>
<td>Binary files can be stored in Cloud Storage and <code dir="ltr" translate="no">       STRING      </code> data type can be used for referencing files in a BigQuery table.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       DATE      </code></td>
<td><code dir="ltr" translate="no">         DATETIME       </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         TIMESTAMP       </code></td>
<td><code dir="ltr" translate="no">         TIMESTAMP       </code></td>
<td>BigQuery supports microsecond precision (10 <sup>-6</sup> ) in comparison to Oracle which supports precision ranging from 0 to 9.
<p>BigQuery supports a time zone region name from a TZ database and time zone offset from UTC.</p>
<p>In BigQuery a time zone conversion should be manually performed to match Oracle's <code dir="ltr" translate="no">        TIMESTAMP WITH LOCAL TIME ZONE       </code> feature.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         TIMESTAMP(x)       </code></td>
<td><code dir="ltr" translate="no">         TIMESTAMP       </code></td>
<td>BigQuery supports microsecond precision (10 <sup>-6</sup> ) in comparison to Oracle which supports precision ranging from 0 to 9.
<p>BigQuery supports a time zone region name from a TZ database and time zone offset from UTC.</p>
<p>In BigQuery a time zone conversion should be manually performed to match Oracle's <code dir="ltr" translate="no">        TIMESTAMP WITH LOCAL TIME ZONE       </code> feature.</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         TIMESTAMP WITH TIME ZONE       </code></td>
<td><code dir="ltr" translate="no">         TIMESTAMP       </code></td>
<td>BigQuery supports microsecond precision (10 <sup>-6</sup> ) in comparison to Oracle which supports precision ranging from 0 to 9.
<p>BigQuery supports a time zone region name from a TZ database and time zone offset from UTC.</p>
<p>In BigQuery a time zone conversion should be manually performed to match Oracle's <code dir="ltr" translate="no">        TIMESTAMP WITH LOCAL TIME ZONE       </code> feature.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         TIMESTAMP WITH LOCAL TIME ZONE       </code></td>
<td><code dir="ltr" translate="no">         TIMESTAMP       </code></td>
<td>BigQuery supports microsecond precision (10 <sup>-6</sup> ) in comparison to Oracle which supports precision ranging from 0 to 9.
<p>BigQuery supports a time zone region name from a TZ database and time zone offset from UTC.</p>
<p>In BigQuery a time zone conversion should be manually performed to match Oracle's <code dir="ltr" translate="no">        TIMESTAMP WITH LOCAL TIME ZONE       </code> feature.</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         INTERVAL YEAR TO MONTH       </code></td>
<td><code dir="ltr" translate="no">         STRING       </code></td>
<td>Interval values can be stored as <code dir="ltr" translate="no">       STRING      </code> data type in BigQuery.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         INTERVAL DAY TO SECOND       </code></td>
<td><code dir="ltr" translate="no">         STRING       </code></td>
<td>Interval values can be stored as <code dir="ltr" translate="no">       STRING      </code> data type in BigQuery.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         RAW       </code></td>
<td><code dir="ltr" translate="no">         BYTES       </code></td>
<td><code dir="ltr" translate="no">       BYTES      </code> data type can be used to store variable-length binary data. If this field is not queried and used in analytics, a better option is to store binary data on Cloud Storage.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         LONG RAW       </code></td>
<td><code dir="ltr" translate="no">         BYTES       </code></td>
<td><code dir="ltr" translate="no">       BYTES      </code> data type can be used to store variable-length binary data. If this field is not queried and used in analytics, a better option is to store binary data on Cloud Storage.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         ROWID       </code></td>
<td><code dir="ltr" translate="no">         STRING       </code></td>
<td>These data types are used Oracle internally to specify unique addresses to rows in a table. Generally, <code dir="ltr" translate="no">       ROWID      </code> or <code dir="ltr" translate="no">       UROWID      </code> field should not be used in applications. But if this is the case, <code dir="ltr" translate="no">       STRING      </code> data type can be used to hold this data.</td>
</tr>
</tbody>
</table>

### Type formatting

Oracle SQL uses a set of default formats set as parameters for displaying expressions and column data, and for conversions between data types. For example, `  NLS_DATE_FORMAT  ` set as `  YYYY/MM/DD  ` formats dates as `  YYYY/MM/DD  ` by default. You can find more information about [the NLS settings in the Oracle online documentation](https://docs.oracle.com/cd/B28359_01/server.111/b28298/ch3globenv.htm) . In BigQuery, there are no initialization parameters.

By default, BigQuery expects all source data to be UTF-8 encoded when loading. Optionally, if you have CSV files with data encoded in ISO-8859-1 format, you can explicitly specify the encoding when you import your data so that BigQuery can properly convert your data to UTF-8 during the import process.

It is only possible to import data that is ISO-8859-1 or UTF-8 encoded. BigQuery stores and returns the data as UTF-8 encoded. Intended date format or time zone can be set in [`  DATE  `](/bigquery/docs/reference/standard-sql/date_functions) and [`  TIMESTAMP  `](/bigquery/docs/reference/standard-sql/timestamp_functions) functions.

### Timestamp and date type formatting

When you convert timestamp and date formatting elements from Oracle to BigQuery, you must pay attention to time zone differences between `  TIMESTAMP  ` and `  DATETIME  ` as summarized in the following table.

Notice there are no parentheses in the Oracle formats because the formats ( `  CURRENT_*  ` ) are keywords, not functions.

Oracle

BigQuery

Notes

`  CURRENT_TIMESTAMP  `

`  TIMESTAMP  ` information in Oracle can have different time zone information, which is defined using `  WITH TIME ZONE  ` in column definition or setting `  TIME_ZONE  ` variable.

If possible, use the `  CURRENT_TIMESTAMP()  ` function, which is formatted in ISO format. However, the output format does always show the UTC time zone. (Internally, BigQuery does not have a time zone.)

Note the following details on differences in the ISO format:

`  DATETIME  ` is formatted based on output channel conventions. In the BigQuery command-line tool and BigQuery console `  DATETIME  ` is formatted using a `  T  ` separator according to RFC 3339. However, in Python and Java JDBC, a space is used as a separator.

If you want to use an explicit format, use the `  FORMAT_DATETIME  ` () function, which makes an explicit cast a string. For example, the following expression always returns a space separator: `  CAST(CURRENT_DATETIME() AS STRING)  `

`  CURRENT_DATE SYSDATE  `

Oracle uses 2 types for date:

  - type 12
  - type 13

Oracle uses type 12 when storing dates. Internally, these are numbers with fixed-length. Oracle uses type 13 when a is returned by `  SYSDATE or CURRENT_DATE  `

BigQuery has a separate `  DATE  ` format that always returns a date in [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) format.

`  DATE_FROM_UNIX_DATE  ` can't be used because it is 1970-based.

`  CURRENT_DATE -3  `

Date values are represented as integers. Oracle supports arithmetic operators for date types.

For date types, use `  DATE_ADD  ` () or `  DATE_SUB  ` (). BigQuery uses arithmetic operators for data types: `  INT64  ` , `  NUMERIC  ` , and `  FLOAT64  ` .

`  NLS_DATE_FORMAT  `

Set the session or system date format.

BigQuery always uses [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) , so make sure you convert Oracle dates and times.

## Query syntax

This section addresses differences in query syntax between Oracle and BigQuery.

### `     SELECT    ` statements

Most Oracle `  SELECT  ` statements are compatible with BigQuery.

## Functions, operators, and expressions

The following sections list mappings between Oracle functions and BigQuery equivalents.

### Comparison operators

Oracle and BigQuery comparison operators are ANSI SQL:2011 compliant. The comparison operators in the table below are the same in both BigQuery and Oracle. You can use [`  REGEXP_CONTAINS  `](/bigquery/docs/reference/standard-sql/string_functions#regexp_contains) instead of `  REGEXP_LIKE  ` in BigQuery.

<table>
<thead>
<tr class="header">
<th>Operator</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       "="      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/operators#comparison_operators">Equal</a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       &lt;&gt;      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/operators#comparison_operators">Not equal</a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       !=      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/operators#comparison_operators">Not equal</a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       &gt;      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/operators#comparison_operators">Greater than</a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       &gt;=      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/operators#comparison_operators">Greater than or equal</a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       &lt;      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/operators#comparison_operators">Less than</a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       &lt;=      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/operators#comparison_operators">Less than or equal</a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       IN ( )      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/operators#comparison_operators">Matches a value in a list</a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       NOT      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/operators#comparison_operators">Negates a condition</a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       BETWEEN      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/operators#comparison_operators">Within a range (inclusive)</a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       IS NULL      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/operators#comparison_operators"><code dir="ltr" translate="no">        NULL       </code> value</a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       IS NOT NULL      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/operators#comparison_operators">Not <code dir="ltr" translate="no">        NULL       </code> value</a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       LIKE      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/operators#comparison_operators">Pattern matching with %</a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       EXISTS      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/operators#comparison_operators">Condition is met if subquery returns at least one row</a></td>
</tr>
</tbody>
</table>

The operators on the table are the same both in BigQuery and Oracle.

### Logical expressions and functions

<table>
<thead>
<tr class="header">
<th>Oracle</th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         CASE       </code></td>
<td><code dir="ltr" translate="no">         CASE       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         COALESCE       </code></td>
<td><code dir="ltr" translate="no">         COALESCE(expr1, ..., exprN)       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         DECODE       </code></td>
<td><code dir="ltr" translate="no">         CASE.. WHEN.. END       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         NANVL       </code></td>
<td><code dir="ltr" translate="no">         IFNULL       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         FETCH NEXT&gt;       </code></td>
<td><code dir="ltr" translate="no">         LIMIT       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         NULLIF       </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/conditional_expressions#nullif"><code dir="ltr" translate="no">        NULLIF(expression, expression_to_match)       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         NVL       </code></td>
<td><code dir="ltr" translate="no">         IFNULL(expr, 0), COALESCE(exp, 0)       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         NVL2       </code></td>
<td><code dir="ltr" translate="no">         IF(expr, true_result, else_result)       </code></td>
</tr>
</tbody>
</table>

### Aggregate functions

The following table shows mappings between common Oracle aggregate, statistical aggregate, and approximate aggregate functions with their BigQuery equivalents:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Oracle</th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         ANY_VALUE       </code><br />
(from Oracle 19c)</td>
<td><code dir="ltr" translate="no">         ANY_VALUE       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       APPROX_COUNT      </code></td>
<td><code dir="ltr" translate="no">         HLL_COUNT              set of functions with specified precision      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         APPROX_COUNT_DISTINCT       </code></td>
<td><code dir="ltr" translate="no">         APPROX_COUNT_DISTINCT       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         APPROX_COUNT_DISTINCT_AGG       </code></td>
<td><code dir="ltr" translate="no">         APPROX_COUNT_DISTINCT       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         APPROX_COUNT_DISTINCT_DETAIL       </code></td>
<td><code dir="ltr" translate="no">         APPROX_COUNT_DISTINCT       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         APPROX_PERCENTILE              (percentile) WITHIN GROUP (ORDER BY expression)      </code></td>
<td><code dir="ltr" translate="no">         APPROX_QUANTILES              (expression, 100)[              OFFSET(CAST(TRUNC(percentile * 100) as INT64))]      </code><br />
BigQuery doesn't support the rest of arguments that Oracle defines.</td>
</tr>
<tr class="odd">
<td><code>         APPROX_PERCENTILE_AGG       </code></td>
<td><code dir="ltr" translate="no">         APPROX_QUANTILES              (expression, 100)[              OFFSET(CAST(TRUNC(percentile * 100) as INT64))]      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         APPROX_PERCENTILE_DETAIL       </code></td>
<td><code dir="ltr" translate="no">         APPROX_QUANTILES              (expression, 100)[OFFSET(CAST(TRUNC(percentile * 100) as INT64))]      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         APPROX_SUM       </code></td>
<td><code dir="ltr" translate="no">         APPROX_TOP_SUM(expression, weight, number)       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         AVG       </code></td>
<td><code dir="ltr" translate="no">         AVG       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         BIT_COMPLEMENT       </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/operators">bitwise not operator: ~</a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         BIT_OR       </code></td>
<td><code dir="ltr" translate="no">         BIT_OR              ,               X | Y       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         BIT_XOR       </code></td>
<td><code dir="ltr" translate="no">         BIT_XOR              ,               X ^ Y       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         BITAND       </code></td>
<td><code dir="ltr" translate="no">         BIT_AND              ,               X &amp; Y       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         CARDINALITY       </code></td>
<td><code dir="ltr" translate="no">         COUNT       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         COLLECT       </code></td>
<td>BigQuery doesn't support <code dir="ltr" translate="no">       TYPE AS TABLE OF      </code> . Consider using <code dir="ltr" translate="no">         STRING_AGG()       </code> or <code dir="ltr" translate="no">         ARRAY_AGG()       </code> in BigQuery</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         CORR              /CORR_K/      </code> <code dir="ltr" translate="no">       CORR_S      </code></td>
<td><code dir="ltr" translate="no">         CORR       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         COUNT       </code></td>
<td><code dir="ltr" translate="no">         COUNT       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         COVAR_POP       </code></td>
<td><code dir="ltr" translate="no">         COVAR_POP       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         COVAR_SAMP       </code></td>
<td><code dir="ltr" translate="no">         COVAR_SAMP       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         FIRST       </code></td>
<td>Does not exist implicitly in BigQuery. Consider using <a href="/bigquery/docs/user-defined-functions">user-defined functions (UDFs)</a> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         GROUP_ID       </code></td>
<td>Not used in BigQuery</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         GROUPING       </code></td>
<td><code dir="ltr" translate="no">         GROUPING       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         GROUPING_ID       </code></td>
<td>Not used in BigQuery.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       LAST      </code></td>
<td>Does not exist implicitly in BigQuery. Consider using <a href="/bigquery/docs/user-defined-functions">UDFs</a> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         LISTAGG       </code></td>
<td><code dir="ltr" translate="no">         STRING_AGG              ,               ARRAY_CONCAT_AGG              (expression [ORDER BY key [{ASC|DESC}] [, ... ]] [LIMIT n])      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         MAX       </code></td>
<td><code dir="ltr" translate="no">         MAX       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         MIN       </code></td>
<td><code dir="ltr" translate="no">         MIN       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       OLAP_CONDITION      </code></td>
<td>Oracle specific, does not exist in BigQuery.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       OLAP_EXPRESSION      </code></td>
<td>Oracle specific, does not exist in BigQuery.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       OLAP_EXPRESSION_BOOL      </code></td>
<td>Oracle specific, does not exist in BigQuery.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       OLAP_EXPRESSION_DATE      </code></td>
<td>Oracle specific, does not exist in BigQuery.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       OLAP_EXPRESSION_TEXT      </code></td>
<td>Oracle specific, does not exist in BigQuery.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       OLAP_TABLE      </code></td>
<td>Oracle specific, does not exist in BigQuery.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       POWERMULTISET      </code></td>
<td>Oracle specific, does not exist in BigQuery.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       POWERMULTISET_BY_CARDINALITY      </code></td>
<td>Oracle specific, does not exist in BigQuery.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       QUALIFY      </code></td>
<td>Oracle specific, does not exist in BigQuery.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         REGR_AVGX       </code></td>
<td><code dir="ltr" translate="no">         AVG              (      </code><br />
<code dir="ltr" translate="no">       IF(dep_var_expr is NULL      </code><br />
<code dir="ltr" translate="no">       OR ind_var_expr is NULL,      </code><br />
<code dir="ltr" translate="no">       NULL, ind_var_expr)      </code><br />
<code dir="ltr" translate="no">       )      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         REGR_AVGY       </code></td>
<td><code dir="ltr" translate="no">         AVG              (      </code><br />
<code dir="ltr" translate="no">       IF(dep_var_expr is NULL      </code><br />
<code dir="ltr" translate="no">       OR ind_var_expr is NULL,      </code><br />
<code dir="ltr" translate="no">       NULL, dep_var_expr)      </code><br />
<code dir="ltr" translate="no">       )      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         REGR_COUNT       </code></td>
<td><code dir="ltr" translate="no">         SUM              (      </code><br />
<code dir="ltr" translate="no">       IF(dep_var_expr is NULL      </code><br />
<code dir="ltr" translate="no">       OR ind_var_expr is NULL,      </code><br />
<code dir="ltr" translate="no">       NULL, 1)      </code><br />
<code dir="ltr" translate="no">       )      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         REGR_INTERCEPT       </code></td>
<td><code dir="ltr" translate="no">         AVG              (dep_var_expr)              - AVG(ind_var_expr)              * (COVAR_SAMP(ind_var_expr,dep_var_expr)              /               VARIANCE              (ind_var_expr)              )      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         REGR_R2       </code></td>
<td><code dir="ltr" translate="no">       (COUNT(dep_var_expr) *                SUM              (ind_var_expr * dep_var_expr) -              SUM(dep_var_expr) * SUM(ind_var_expr))              / SQRT(              (COUNT(ind_var_expr) *              SUM(POWER(ind_var_expr, 2)) *              POWER(SUM(ind_var_expr),2)) *              (COUNT(dep_var_expr) *              SUM(POWER(dep_var_expr, 2)) *              POWER(SUM(dep_var_expr), 2)))       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         REGR_SLOPE       </code></td>
<td><code dir="ltr" translate="no">         COVAR_SAMP              (ind_var_expr,      </code>
<p><code dir="ltr" translate="no">        dep_var_expr)       </code></p>
<p><code dir="ltr" translate="no">        /                 VARIANCE                (ind_var_expr)       </code></p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         REGR_SXX       </code></td>
<td><code dir="ltr" translate="no">         SUM              (POWER(ind_var_expr, 2)) - COUNT(ind_var_expr) * POWER(               AVG              (ind_var_expr),2)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         REGR_SXY       </code></td>
<td><code dir="ltr" translate="no">         SUM              (ind_var_expr*dep_var_expr) - COUNT(ind_var_expr) *               AVG              (ind) * AVG(dep_var_expr)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         REGR_SYY       </code></td>
<td><code dir="ltr" translate="no">         SUM              (POWER(dep_var_expr, 2)) - COUNT(dep_var_expr) * POWER(               AVG              (dep_var_expr),2)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         ROLLUP       </code></td>
<td><code dir="ltr" translate="no">         ROLLUP       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         STDDEV_POP       </code></td>
<td><code dir="ltr" translate="no">         STDDEV_POP       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         STDDEV_SAMP       </code></td>
<td><code dir="ltr" translate="no">         STDDEV_SAMP              ,               STDDEV       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         SUM       </code></td>
<td><code dir="ltr" translate="no">         SUM       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         VAR_POP       </code></td>
<td><code dir="ltr" translate="no">         VAR_POP       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         VAR_SAMP       </code></td>
<td><code dir="ltr" translate="no">         VAR_SAMP              ,               VARIANCE       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         WM_CONCAT       </code></td>
<td><code dir="ltr" translate="no">         STRING_AGG       </code></td>
</tr>
</tbody>
</table>

BigQuery offers the following additional aggregate functions:

  - `  ANY_VALUE  `
  - `  APPROX_TOP_COUNT  `
  - `  COUNTIF  `
  - `  LOGICAL_AND  `
  - `  LOGICAL_OR  `

### Analytical functions

The following table shows mappings between common Oracle analytic and aggregate analytic functions with their BigQuery equivalents.

<table>
<thead>
<tr class="header">
<th>Oracle</th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         AVG       </code></td>
<td><code dir="ltr" translate="no">         AVG       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         BIT_COMPLEMENT       </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/operators">bitwise not operator: ~</a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         BIT_OR       </code></td>
<td><code dir="ltr" translate="no">         BIT_OR              ,               X | Y       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         BIT_XOR       </code></td>
<td><code dir="ltr" translate="no">         BIT_XOR              ,               X ^ Y       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         BITAND       </code></td>
<td><code dir="ltr" translate="no">         BIT_AND              ,               X &amp; Y       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       BOOL_TO_INT      </code></td>
<td><code dir="ltr" translate="no">         CAST              (X AS INT64)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       COUNT      </code></td>
<td><code dir="ltr" translate="no">         COUNT       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         COVAR_POP       </code></td>
<td><code dir="ltr" translate="no">         COVAR_POP       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         COVAR_SAMP       </code></td>
<td><code dir="ltr" translate="no">         COVAR_SAMP       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       CUBE_TABLE      </code></td>
<td>Isn't supported in BigQuery. Consider using a BI tool or a custom UDF</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         CUME_DIST       </code></td>
<td><code dir="ltr" translate="no">         CUME_DIST       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         DENSE_RANK              (ANSI)      </code></td>
<td><code dir="ltr" translate="no">         DENSE_RANK       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       FEATURE_COMPARE      </code></td>
<td>Does not exist implicitly in BigQuery. Consider using UDFs and BigQuery ML</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       FEATURE_DETAILS      </code></td>
<td>Does not exist implicitly in BigQuery. Consider using UDFs and BigQuery ML</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       FEATURE_ID      </code></td>
<td>Does not exist implicitly in BigQuery. Consider using UDFs and BigQuery ML</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       FEATURE_SET      </code></td>
<td>Does not exist implicitly in BigQuery. Consider using UDFs and BigQuery ML</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       FEATURE_VALUE      </code></td>
<td>Does not exist implicitly in BigQuery. Consider using UDFs and BigQuery ML</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         FIRST_VALUE       </code></td>
<td><code dir="ltr" translate="no">         FIRST_VALUE       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       HIER_CAPTION      </code></td>
<td>Hierarchical queries are not supported in BigQuery.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       HIER_CHILD_COUNT      </code></td>
<td>Hierarchical queries are not supported in BigQuery.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       HIER_COLUMN      </code></td>
<td>Hierarchical queries are not supported in BigQuery.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       HIER_DEPTH      </code></td>
<td>Hierarchical queries are not supported in BigQuery.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       HIER_DESCRIPTION      </code></td>
<td>Hierarchical queries are not supported in BigQuery.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       HIER_HAS_CHILDREN      </code></td>
<td>Hierarchical queries are not supported in BigQuery.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       HIER_LEVEL      </code></td>
<td>Hierarchical queries are not supported in BigQuery.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       HIER_MEMBER_NAME      </code></td>
<td>Hierarchical queries are not supported in BigQuery.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       HIER_ORDER      </code></td>
<td>Hierarchical queries are not supported in BigQuery.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       HIER_UNIQUE_MEMBER_NAME      </code></td>
<td>Hierarchical queries are not supported in BigQuery.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         LAST_VALUE       </code></td>
<td><code dir="ltr" translate="no">         LAST_VALUE       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         LAG       </code></td>
<td><code dir="ltr" translate="no">         LAG       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         LEAD       </code></td>
<td><code dir="ltr" translate="no">         LEAD       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       LISTAGG      </code></td>
<td><code dir="ltr" translate="no">         ARRAY_AGG                 STRING_AGG                 ARRAY_CONCAT_AGG       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         MATCH_NUMBER       </code></td>
<td>Pattern recognition and calculation can be done with regular expressions and UDFs in BigQuery</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         MATCH_RECOGNIZE       </code></td>
<td>Pattern recognition and calculation can be done with regular expressions and UDFs in BigQuery</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         MAX       </code></td>
<td><code dir="ltr" translate="no">         MAX       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         MEDIAN       </code></td>
<td><code dir="ltr" translate="no">         PERCENTILE_CONT(x, 0.5 RESPECT NULLS) OVER()       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         MIN       </code></td>
<td><code dir="ltr" translate="no">         MIN       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         NTH_VALUE       </code></td>
<td><code dir="ltr" translate="no">         NTH_VALUE              (value_expression, constant_integer_expression [{RESPECT | IGNORE} NULLS])      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         NTILE       </code></td>
<td><code dir="ltr" translate="no">         NTILE              (constant_integer_expression)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         PERCENT_RANK               PERCENT_RANKM      </code></td>
<td><code dir="ltr" translate="no">         PERCENT_RANK       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         PERCENTILE_CONT                 PERCENTILE_DISC       </code></td>
<td><code dir="ltr" translate="no">         PERCENTILE_CONT       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         PERCENTILE_CONT                 PERCENTILE_DISC       </code></td>
<td><code dir="ltr" translate="no">         PERCENTILE_DISC       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         PRESENTNNV       </code></td>
<td>Oracle specific, does not exist in BigQuery.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         PRESENTV       </code></td>
<td>Oracle specific, does not exist in BigQuery.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         PREVIOUS       </code></td>
<td>Oracle specific, does not exist in BigQuery.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         RANK       </code> (ANSI)</td>
<td><code dir="ltr" translate="no">         RANK       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         RATIO_TO_REPORT              (expr) OVER (partition clause)      </code></td>
<td><code dir="ltr" translate="no">       expr / SUM(expr) OVER (partition clause)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         ROW_NUMBER       </code></td>
<td><code dir="ltr" translate="no">         ROW_NUMBER       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         STDDEV_POP       </code></td>
<td><code dir="ltr" translate="no">         STDDEV_POP       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         STDDEV_SAMP       </code></td>
<td><code dir="ltr" translate="no">         STDDEV_SAMP              ,               STDDEV       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         SUM       </code></td>
<td><code dir="ltr" translate="no">         SUM       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         VAR_POP       </code></td>
<td><code dir="ltr" translate="no">         VAR_POP       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         VAR_SAMP       </code></td>
<td><code dir="ltr" translate="no">         VAR_SAMP              ,               VARIANCE       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         VARIANCE       </code></td>
<td><code dir="ltr" translate="no">         VARIANCE              ()      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         WIDTH_BUCKET       </code></td>
<td>UDF can be used.</td>
</tr>
</tbody>
</table>

### Date/time functions

The following table shows mappings between common Oracle date/time functions and their BigQuery equivalents.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Oracle</th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         ADD_MONTHS              (date, integer)      </code></td>
<td><code dir="ltr" translate="no">         DATE_ADD              (date, INTERVAL integer MONTH),      </code><br />
If date is a <code dir="ltr" translate="no">       TIMESTAMP      </code> you can use
<p><code dir="ltr" translate="no">          EXTRACT                (DATE FROM TIMESTAMP_ADD(date, INTERVAL integer MONTH))       </code></p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         CURRENT_DATE       </code></td>
<td><code dir="ltr" translate="no">         CURRENT_DATE       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       CURRENT_TIME      </code></td>
<td><code dir="ltr" translate="no">         CURRENT_TIME       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         CURRENT_TIMESTAMP       </code></td>
<td><code dir="ltr" translate="no">         CURRENT_TIMESTAMP       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         DATE              - k      </code></td>
<td><code dir="ltr" translate="no">         DATE_SUB              (date_expression, INTERVAL k DAY)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         DATE              + k      </code></td>
<td><code dir="ltr" translate="no">         DATE_ADD              (date_expression, INTERVAL k DAY)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       DBTIMEZONE      </code></td>
<td>BigQuery does not support the database time zone.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         EXTRACT       </code></td>
<td><code dir="ltr" translate="no">         EXTRACT(DATE)              ,               EXTRACT(TIMESTAMP)       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         LAST_DAY       </code></td>
<td><code dir="ltr" translate="no">         DATE_SUB              (                DATE_TRUNC              (                DATE_ADD              (              date_expression,              INTERVAL 1 MONTH              ),              MONTH              ),              INTERVAL 1 DAY              )      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         LOCALTIMESTAMP       </code></td>
<td>BigQuery doesn't support time zone settings.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         MONTHS_BETWEEN       </code></td>
<td><code dir="ltr" translate="no">         DATE_DIFF              (date_expression, date_expression, MONTH)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         NEW_TIME       </code></td>
<td><code dir="ltr" translate="no">       DATE(timestamp_expression, time zone)              TIME(timestamp, time zone)              DATETIME(timestamp_expression, time zone)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         NEXT_DAY       </code></td>
<td><code dir="ltr" translate="no">         DATE_ADD              (                DATE_TRUNC              (              date_expression,              WEEK(day_value)              ),              INTERVAL 1 WEEK              )      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       SYS_AT_TIME_ZONE      </code></td>
<td><code dir="ltr" translate="no">         CURRENT_DATE              ([time_zone])      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         SYSDATE       </code></td>
<td><code dir="ltr" translate="no">         CURRENT_DATE()       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         SYSTIMESTAMP       </code></td>
<td><code dir="ltr" translate="no">         CURRENT_TIMESTAMP()       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         TO_DATE       </code></td>
<td><code dir="ltr" translate="no">         PARSE_DATE       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         TO_TIMESTAMP       </code></td>
<td><code dir="ltr" translate="no">         PARSE_TIMESTAMP       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         TO_TIMESTAMP_TZ       </code></td>
<td><code dir="ltr" translate="no">         PARSE_TIMESTAMP       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         TZ_OFFSET       </code></td>
<td>Isn't supported in BigQuery. Consider using a custom UDF.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       WM_CONTAINS      </code><br />
<code dir="ltr" translate="no">       WM_EQUALS      </code><br />
<code dir="ltr" translate="no">       WM_GREATERTHAN      </code><br />
<code dir="ltr" translate="no">       WM_INTERSECTION      </code><br />
<code dir="ltr" translate="no">       WM_LDIFF      </code><br />
<code dir="ltr" translate="no">       WM_LESSTHAN      </code><br />
<code dir="ltr" translate="no">       WM_MEETS      </code><br />
<code dir="ltr" translate="no">       WM_OVERLAPS      </code><br />
<code dir="ltr" translate="no">       WM_RDIFF      </code><br />
</td>
<td>Periods are not used in BigQuery. UDFs can be used to compare two periods.</td>
</tr>
</tbody>
</table>

BigQuery offers the following additional date/time functions:

  - `  CURRENT_DATETIME  `

  - `  DATE_FROM_UNIX_DATE  `

  - `  DATE_TRUNC  `

  - `  DATETIME  `

  - `  DATETIME_ADD  `

  - `  DATETIME_DIFF  `

  - `  DATETIME_SUB  `

  - `  DATETIME_TRUNC  `

  - `  FORMAT_DATE  `

  - `  FORMAT_DATETIME  `

  - `  FORMAT_TIME  `

  - `  FORMAT_TIMESTAMP  `

  - `  PARSE_DATETIME  `

  - `  PARSE_TIME  `

  - `  STRING  `

  - `  TIME  `

  - `  TIME_ADD  `

  - `  TIME_DIFF  `

  - `  TIME_SUB  `

  - `  TIME_TRUNC  `

  - `  TIMESTAMP  `

  - `  TIMESTAMP_ADD  `

  - `  TIMESTAMP_DIFF  `

  - `  TIMESTAMP_MICROS  `

  - `  TIMESTAMP_MILLIS  `

  - `  TIMESTAMP_SECONDS  `

  - `  TIMESTAMP_SUB  `

  - `  TIMESTAMP_TRUNC  `

  - `  UNIX_DATE  `

  - `  UNIX_MICROS  `

  - `  UNIX_MILLIS  `

  - `  UNIX_SECONDS  `

### String functions

The following table shows mappings between Oracle string functions and their BigQuery equivalents:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Oracle</th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         ASCII       </code></td>
<td><code dir="ltr" translate="no">         TO_CODE_POINTS(string_expr)[OFFSET(0)]       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         ASCIISTR       </code></td>
<td>BigQuery doesn't support UTF-16</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         RAWTOHEX       </code></td>
<td><code dir="ltr" translate="no">         TO_HEX       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         LENGTH       </code></td>
<td><code dir="ltr" translate="no">         CHAR_LENGTH       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       LENGTH      </code></td>
<td><code dir="ltr" translate="no">         CHARACTER_LENGTH       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         CHR       </code></td>
<td><code dir="ltr" translate="no">         CODE_POINTS_TO_STRING              (              [mod(numeric_expr, 256)]              )      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         COLLATION       </code></td>
<td>Doesn't exist in BigQuery. BigQuery doesn't support COLLATE in DML</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         COMPOSE       </code></td>
<td>Custom user-defined function.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       CONCAT, (|| operator)      </code></td>
<td><code dir="ltr" translate="no">         CONCAT       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         DECOMPOSE       </code></td>
<td>Custom user-defined function.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       ESCAPE_REFERENCE (UTL_I18N)      </code></td>
<td>Is not supported in BigQuery. Consider using a user-defined function.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         INITCAP       </code></td>
<td><code dir="ltr" translate="no">         INITCAP       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         INSTR/INSTR2/INSTR4/INSTRB/INSTRC       </code></td>
<td>Custom user-defined function.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         LENGTH/LENGTH2/LENGTH4/LENGTHB/LENGTHC       </code></td>
<td><code dir="ltr" translate="no">         LENGTH       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         LOWER       </code></td>
<td><code dir="ltr" translate="no">        LOWER      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         LPAD       </code></td>
<td><code dir="ltr" translate="no">         LPAD       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         LTRIM       </code></td>
<td><code dir="ltr" translate="no">         LTRIM       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         NLS_INITCAP       </code></td>
<td>Custom user-defined function.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         NLS_LOWER       </code></td>
<td><code dir="ltr" translate="no">         LOWER       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         NLS_UPPER       </code></td>
<td><code dir="ltr" translate="no">         UPPER       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         NLSSORT       </code></td>
<td>Oracle specific, does not exist in BigQuery.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       POSITION      </code></td>
<td><code dir="ltr" translate="no">         STRPOS(string, substring)       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       PRINTBLOBTOCLOB      </code></td>
<td>Oracle specific, does not exist in BigQuery.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         REGEXP_COUNT       </code></td>
<td><code dir="ltr" translate="no">         ARRAY_LENGTH(REGEXP_EXTRACT_ALL(value, regex))       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         REGEXP_INSTR       </code></td>
<td><code dir="ltr" translate="no">         STRPOS              (source_string,               REGEXP_EXTRACT              (source_string, regexp_string))      </code>
<p>Note: Returns first occurrence.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         REGEXP_REPLACE       </code></td>
<td><code dir="ltr" translate="no">         REGEXP_REPLACE       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       REGEXP_LIKE      </code></td>
<td><code dir="ltr" translate="no">       IF(               REGEXP_CONTAINS              ,1,0)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         REGEXP_SUBSTR       </code></td>
<td><code dir="ltr" translate="no">       REGEXP_EXTRACT, REGEXP_EXTRACT_ALL      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         REPLACE       </code></td>
<td><code dir="ltr" translate="no">         REPLACE       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         REVERSE       </code></td>
<td><code dir="ltr" translate="no">         REVERSE       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       RIGHT      </code></td>
<td><code dir="ltr" translate="no">         SUBSTR              (source_string, -1, length)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         RPAD       </code></td>
<td><code dir="ltr" translate="no">         RPAD       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         RTRIM       </code></td>
<td><code dir="ltr" translate="no">         RTRIM       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         SOUNDEX       </code></td>
<td>Isn't supported in BigQuery. Consider using a custom UDF</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         STRTOK       </code></td>
<td><code dir="ltr" translate="no">         SPLIT              (instring, delimiter)[ORDINAL(tokennum)]      </code>
<p><code dir="ltr" translate="no">        Note: The entire delimiter string argument is used as a single delimiter. The default delimiter is a comma.       </code></p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         SUBSTR/SUBSTRB/SUBSTRC/SUBSTR2/SUBSTR4       </code></td>
<td><code dir="ltr" translate="no">         SUBSTR       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         TRANSLATE       </code></td>
<td><code dir="ltr" translate="no">         REPLACE       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         TRANSLATE USING       </code></td>
<td><code dir="ltr" translate="no">         REPLACE       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         TRIM       </code></td>
<td><code dir="ltr" translate="no">         TRIM       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         UNISTR       </code></td>
<td><code dir="ltr" translate="no">         CODE_POINTS_TO_STRING       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         UPPER       </code></td>
<td><code dir="ltr" translate="no">         UPPER       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ||      </code> (VERTICAL BARS)</td>
<td><code dir="ltr" translate="no">         CONCAT       </code></td>
</tr>
</tbody>
</table>

BigQuery offers the following additional string functions:

  - `  BYTE_LENGTH  `
  - `  CODE_POINTS_TO_BYTES  `
  - `  ENDS_WITH  `
  - `  FROM_BASE32  `
  - `  FROM_BASE64  `
  - `  FROM_HEX  `
  - `  NORMALIZE  `
  - `  NORMALIZE_AND_CASEFOLD  `
  - `  REPEAT  `
  - `  SAFE_CONVERT_BYTES_TO_STRING  `
  - `  SPLIT  `
  - `  STARTS_WITH  `
  - `  STRPOS  `
  - `  TO_BASE32  `
  - `  TO_BASE64  `
  - `  TO_CODE_POINTS  `

### Math functions

The following table shows mappings between Oracle math functions and their BigQuery equivalents.

<table>
<thead>
<tr class="header">
<th>Oracle</th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         ABS       </code></td>
<td><code dir="ltr" translate="no">         ABS       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         ACOS       </code></td>
<td><code dir="ltr" translate="no">         ACOS       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       ACOSH      </code></td>
<td><code dir="ltr" translate="no">         ACOSH       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         ASIN       </code></td>
<td><code dir="ltr" translate="no">         ASIN       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       ASINH      </code></td>
<td><code dir="ltr" translate="no">         ASINH       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         ATAN       </code></td>
<td><code dir="ltr" translate="no">         ATAN       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         ATAN2       </code></td>
<td><code dir="ltr" translate="no">         ATAN2       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ATANH      </code></td>
<td><code dir="ltr" translate="no">         ATANH       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         CEIL       </code></td>
<td><code dir="ltr" translate="no">         CEIL       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       CEILING      </code></td>
<td><code dir="ltr" translate="no">         CEILING       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         COS       </code></td>
<td><code dir="ltr" translate="no">         COS       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         COSH       </code></td>
<td><code dir="ltr" translate="no">         COSH       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         EXP       </code></td>
<td><code dir="ltr" translate="no">         EXP       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         FLOOR       </code></td>
<td><code dir="ltr" translate="no">         FLOOR       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         GREATEST       </code></td>
<td><code dir="ltr" translate="no">         GREATEST       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         LEAST       </code></td>
<td><code dir="ltr" translate="no">         LEAST       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         LN       </code></td>
<td><code dir="ltr" translate="no">         LN       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         LNNVL       </code></td>
<td>use with <code dir="ltr" translate="no">       ISNULL      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         LOG       </code></td>
<td><code dir="ltr" translate="no">         LOG       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         MOD              (% operator)      </code></td>
<td><code dir="ltr" translate="no">         MOD       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         POWER              (** operator)      </code></td>
<td><code dir="ltr" translate="no">         POWER              ,               POW       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       DBMS_RANDOM.VALUE      </code></td>
<td><code dir="ltr" translate="no">         RAND       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       RANDOMBYTES      </code></td>
<td>Isn't supported in BigQuery. Consider using a custom UDF and RAND function</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       RANDOMINTEGER      </code></td>
<td><code dir="ltr" translate="no">       CAST(FLOOR(10*RAND()) AS INT64)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       RANDOMNUMBER      </code></td>
<td>Isn't supported in BigQuery. Consider using a custom UDF and RAND function</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         REMAINDER       </code></td>
<td><code dir="ltr" translate="no">         MOD       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         ROUND       </code></td>
<td><code dir="ltr" translate="no">         ROUND       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         ROUND_TIES_TO_EVEN       </code></td>
<td><code dir="ltr" translate="no">       ROUND()      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         SIGN       </code></td>
<td><code dir="ltr" translate="no">         SIGN       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         SIN       </code></td>
<td><code dir="ltr" translate="no">         SIN       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         SINH       </code></td>
<td><code dir="ltr" translate="no">         SINH       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         SQRT       </code></td>
<td><code dir="ltr" translate="no">         SQRT       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         STANDARD_HASH       </code></td>
<td><code dir="ltr" translate="no">       FARM_FINGERPRINT, MD5, SHA1, SHA256, SHA512      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         STDDEV       </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/statistical_aggregate_functions#stddev">STDDEV</a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         TAN       </code></td>
<td><code dir="ltr" translate="no">         TAN       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         TANH       </code></td>
<td><code dir="ltr" translate="no">         TANH       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         TRUNC       </code></td>
<td><code dir="ltr" translate="no">         TRUNC       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       NVL      </code></td>
<td><code dir="ltr" translate="no">         IFNULL              (expr, 0),               COALESCE              (exp, 0)      </code></td>
</tr>
</tbody>
</table>

BigQuery offers the following additional math functions:

  - `  DIV  `
  - `  IEEE_DIVIDE  `
  - `  IS_INF  `
  - `  IS_NAN  `
  - `  LOG10  `
  - `  SAFE_DIVIDE  `

### Type conversion functions

The following table shows mappings between Oracle type conversion functions and their BigQuery equivalents.

Oracle

BigQuery

`  BIN_TO_NUM  `

`  SAFE_CONVERT_BYTES_TO_STRING(value)  `

`  CAST(x AS INT64)  `

`  BINARY2VARCHAR  `

`  SAFE_CONVERT_BYTES_TO_STRING(value)  `

`  CAST CAST_FROM_BINARY_DOUBLE CAST_FROM_BINARY_FLOAT CAST_FROM_BINARY_INTEGER CAST_FROM_NUMBER CAST_TO_BINARY_DOUBLE CAST_TO_BINARY_FLOAT CAST_TO_BINARY_INTEGER CAST_TO_NUMBER CAST_TO_NVARCHAR2 CAST_TO_RAW >CAST_TO_VARCHAR  `

`  CAST(expr AS typename)  `

`  CHARTOROWID  `

Oracle specific not needed.

`  CONVERT  `

BigQuery doesn't support character sets. Consider using custom user-defined function.

`  EMPTY_BLOB  `

`  BLOB  ` is not used in BigQuery.

`  EMPTY_CLOB  `

`  CLOB  ` is not used in BigQuery.

`  FROM_TZ  `

Types with time zones are not supported in BigQuery. Consider using a user-defined function and FORMAT\_TIMESTAMP

`  INT_TO_BOOL  `

`  CAST  `

`  IS_BIT_SET  `

Does not exist implicitly in BigQuery. Consider using UDFs

`  NCHR  `

UDF can be used to get char equivalent of binary

`  NUMTODSINTERVAL  `

`  INTERVAL  ` data type is not supported in BigQuery

`  NUMTOHEX  `

Isn't supported in BigQuery. Consider using a custom UDF and `  TO_HEX  ` function

`  NUMTOHEX2  `

`  NUMTOYMINTERVAL  `

`  INTERVAL  ` data type is not supported in BigQuery.

`  RAW_TO_CHAR  `

Oracle specific, does not exist in BigQuery.

`  RAW_TO_NCHAR  `

Oracle specific, does not exist in BigQuery.

`  RAW_TO_VARCHAR2  `

Oracle specific, does not exist in BigQuery.

`  RAWTOHEX  `

Oracle specific, does not exist in BigQuery.

`  RAWTONHEX  `

Oracle specific, does not exist in BigQuery.

`  RAWTONUM  `

Oracle specific, does not exist in BigQuery.

`  RAWTONUM2  `

Oracle specific, does not exist in BigQuery.

`  RAWTOREF  `

Oracle specific, does not exist in BigQuery.

`  REFTOHEX  `

Oracle specific, does not exist in BigQuery.

`  REFTORAW  `

Oracle specific, does not exist in BigQuery.

`  ROWIDTOCHAR  `

`  ROWID  ` is Oracle specific type and does not exist in BigQuery. This value should be represented as string.

`  ROWIDTONCHAR  `

`  ROWID  ` is Oracle specific type and does not exist in BigQuery. This value should be represented as string.

`  SCN_TO_TIMESTAMP  `

`  SCN  ` is Oracle specific type and does not exist in BigQuery. This value should be represented as timestamp.

`  TO_ACLID TO_ANYLOB TO_APPROX_COUNT_DISTINCT TO_APPROX_PERCENTILE TO_BINARY_DOUBLE TO_BINARY_FLOAT TO_BLOB TO_CHAR TO_CLOB TO_DATE TO_DSINTERVAL TO_LOB TO_MULTI_BYTE TO_NCHAR TO_NCLOB TO_NUMBER TO_RAW TO_SINGLE_BYTE TO_TIME  `  
[TO\_TIMESTAMP](https://docs.oracle.com/en/database/oracle/oracle-database/12.2/sqlrf/TO_TIMESTAMP.html)  
[TO\_TIMESTAMP\_TZ](https://docs.oracle.com/en/database/oracle/oracle-database/12.2/sqlrf/TO_TIMESTAMP_TZ.html)  
TO\_TIME\_TZ  
TO\_UTC\_TIMEZONE\_TZ  
[TO\_YMINTERVAL](https://docs.oracle.com/en/database/oracle/oracle-database/12.2/sqlrf/TO_YMINTERVAL.html)  

`  CAST(expr AS typename)  `  
`  PARSE_DATE  `  
`  PARSE_TIMESTAMP  `  
Cast syntax is used in a query to indicate that the result type of an expression should be converted to some other type.

`  TREAT  `

Oracle specific, does not exist in BigQuery.

`  VALIDATE_CONVERSION  `

Isn't supported in BigQuery. Consider using a custom UDF

`  VSIZE  `

Isn't supported in BigQuery. Consider using a custom UDF

### JSON functions

The following table shows mappings between Oracle JSON functions and their BigQuery equivalents.

<table>
<thead>
<tr class="header">
<th>Oracle</th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       AS_JSON      </code></td>
<td><code dir="ltr" translate="no">       TO_JSON_STRING(value[, pretty_print])      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         JSON_ARRAY       </code></td>
<td>Consider using UDFs and <code dir="ltr" translate="no">       TO_JSON_STRING      </code> function</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         JSON_ARRAYAGG       </code></td>
<td>Consider using UDFs and <code dir="ltr" translate="no">       TO_JSON_STRING      </code> function</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         JSON_DATAGUIDE       </code></td>
<td>Custom user-defined function.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         JSON_EQUAL       </code></td>
<td>Custom user-defined function.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         JSON_EXIST       </code></td>
<td>Consider using UDFs and <code dir="ltr" translate="no">       JSON_EXTRACT      </code> or <code dir="ltr" translate="no">       JSON_EXTRACT_SCALAR      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         JSON_MERGEPATCH       </code></td>
<td>Custom user-defined function.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         JSON_OBJECT       </code></td>
<td>Is not supported by BigQuery.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         JSON_OBJECTAGG       </code></td>
<td>Is not supported by BigQuery.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         JSON_QUERY       </code></td>
<td>Consider using UDFs and <code dir="ltr" translate="no">       JSON_EXTRACT      </code> or <code dir="ltr" translate="no">       JSON_EXTRACT_SCALAR      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         JSON_TABLE       </code></td>
<td>Custom user-defined function.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       JSON_TEXTCONTAINS      </code></td>
<td>Consider using UDFs and <code dir="ltr" translate="no">       JSON_EXTRACT      </code> or <code dir="ltr" translate="no">       JSON_EXTRACT_SCALAR      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         JSON_VALUE       </code></td>
<td><code dir="ltr" translate="no">       JSON_EXTRACT_SCALAR      </code></td>
</tr>
</tbody>
</table>

### XML functions

BigQuery does not provide implicit XML functions. XML can be loaded to BigQuery as string and UDFs can be used to parse XML. Alternatively, XML processing be done by an ETL/ELT tool such as [Dataflow](/dataflow/docs) . The following list shows Oracle XML functions:

Oracle

BigQuery

`  DELETEXML  `

BigQuery [UDFs]() or ETL tool like Dataflow can be used to process XML.

`  ENCODE_SQL_XML  `

`  EXISTSNODE  `

`  EXTRACTCLOBXML  `

`  EXTRACTVALUE  `

`  INSERTCHILDXML  `

`  INSERTCHILDXMLAFTER  `

`  INSERTCHILDXMLBEFORE  `

`  INSERTXMLAFTER  `

`  INSERTXMLBEFORE  `

`  SYS_XMLAGG  `

`  SYS_XMLANALYZE  `

`  SYS_XMLCONTAINS  `

`  SYS_XMLCONV  `

`  SYS_XMLEXNSURI  `

`  SYS_XMLGEN  `

`  SYS_XMLI_LOC_ISNODE  `

`  SYS_XMLI_LOC_ISTEXT  `

`  SYS_XMLINSTR  `

`  SYS_XMLLOCATOR_GETSVAL  `

`  SYS_XMLNODEID  `

`  SYS_XMLNODEID_GETLOCATOR  `

`  SYS_XMLNODEID_GETOKEY  `

`  SYS_XMLNODEID_GETPATHID  `

`  SYS_XMLNODEID_GETPTRID  `

`  SYS_XMLNODEID_GETRID  `

`  SYS_XMLNODEID_GETSVAL  `

`  SYS_XMLT_2_SC  `

`  SYS_XMLTRANSLATE  `

`  SYS_XMLTYPE2SQL  `

`  UPDATEXML  `

`  XML2OBJECT  `

`  XMLCAST  `

`  XMLCDATA  `

`  XMLCOLLATVAL  `

`  XMLCOMMENT  `

`  XMLCONCAT  `

`  XMLDIFF  `

`  XMLELEMENT  `

`  XMLEXISTS  `

`  XMLEXISTS2  `

`  XMLFOREST  `

`  XMLISNODE  `

`  XMLISVALID  `

`  XMLPARSE  `

`  XMLPATCH  `

`  XMLPI  `

`  XMLQUERY  `

`  XMLQUERYVAL  `

`  XMLSERIALIZE  `

`  XMLTABLE  `

`  XMLTOJSON  `

`  XMLTRANSFORM  `

`  XMLTRANSFORMBLOB  `

`  XMLTYPE  `

### Machine learning functions

Machine learning (ML) functions in Oracle and BigQuery are different. Oracle requires advanced analytics pack and licenses to do ML on the database. Oracle uses the `  DBMS_DATA_MINING  ` package for ML. Converting Oracle data miner jobs requires rewriting the code to work with BigQuery features. You can choose from comprehensive [Google AI offerings](https://cloud.google.com/products/ai/) , including the following products and features:

  - [BigQuery AI](/bigquery/docs/ai-introduction)
  - [Vertex AI](/vertex-ai/docs/start/introduction-unified-platform)
  - [AI APIs for Google Cloud](https://cloud.google.com/ai/apis)

You can use [BigQuery ML](/bigquery/docs/bqml-introduction) or [Vertex AI development tools](/vertex-ai/docs/general/developer-tools-overview) to develop, train, and evaluate ML models.

The following table shows Oracle ML functions:

Oracle

BigQuery

`  CLASSIFIER  `

See [BigQuery ML](/bigquery/docs/bqml-introduction) for machine learning classifier and regression options

`  CLUSTER_DETAILS  `

`  CLUSTER_DISTANCE  `

`  CLUSTER_ID  `

`  CLUSTER_PROBABILITY  `

`  CLUSTER_SET  `

`  PREDICTION  `

`  PREDICTION_BOUNDS  `

`  PREDICTION_COST  `

`  PREDICTION_DETAILS  `

`  PREDICTION_PROBABILITY  `

`  PREDICTION_SET  `

### Security functions

The following table shows the functions for identifying the user in Oracle and BigQuery:

<table>
<thead>
<tr class="header">
<th>Oracle</th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         UID       </code></td>
<td><code dir="ltr" translate="no">         SESSION_USER       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       USER/SESSION_USER/CURRENT_USER      </code></td>
<td><code dir="ltr" translate="no">         SESSION_USER()       </code></td>
</tr>
</tbody>
</table>

### Set or array functions

The following table shows set or array functions in Oracle and their equivalents in BigQuery:

<table>
<thead>
<tr class="header">
<th>Oracle</th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         MULTISET       </code></td>
<td><code dir="ltr" translate="no">         ARRAY_AGG       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         MULTISET EXCEPT       </code></td>
<td><code dir="ltr" translate="no">         ARRAY_AGG([DISTINCT] expression)       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         MULTISET INTERSECT       </code></td>
<td><code dir="ltr" translate="no">         ARRAY_AGG([DISTINCT])       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         MULTISET UNION       </code></td>
<td><code dir="ltr" translate="no">         ARRAY_AGG       </code></td>
</tr>
</tbody>
</table>

### Window functions

The following table shows window functions in Oracle and their equivalents in BigQuery.

<table>
<thead>
<tr class="header">
<th>Oracle</th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         LAG       </code></td>
<td><code dir="ltr" translate="no">         LAG              (value_expression[, offset [, default_expression]])      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         LEAD       </code></td>
<td><code dir="ltr" translate="no">         LEAD              (value_expression[, offset [, default_expression]])      </code></td>
</tr>
</tbody>
</table>

### Hierarchical or recursive queries

[Hierarchical](https://docs.oracle.com/cd/B19306_01/server.102/b14200/queries003.htm) or recursive queries are not used in BigQuery. If the depth of the hierarchy is known similar functionality can be achieved with joins, as illustrated in the following example. Another solution would be to utilize the [BigQueryStorage API](/bigquery/docs/reference/storage) and [Spark](http://sqlandhadoop.com/how-to-implement-recursive-queries-in-spark/) .

``` text
select
  array(
    select e.update.element
    union all
    select c1 from e.update.element.child as c1
    union all
    select c2 from e.update.element.child as c1, c1.child as c2
    union all
    select c3 from e.update.element.child as c1, c1.child as c2, c2.child as c3
    union all
    select c4 from e.update.element.child as c1, c1.child as c2, c2.child as c3, c3.child as c4
    union all
    select c5 from e.update.element.child as c1, c1.child as c2, c2.child as c3, c3.child as c4, c4.child as c5
  ) as flattened,
  e as event
from t, t.events as e
```

The following table shows hierarchical functions in Oracle.

Oracle

BigQuery

`  DEPTH  `

Hierarchical queries are not used in BigQuery.

`  PATH  `

`  SYS_CONNECT_BY_PATH (hierarchical)  `

### UTL functions

[`  UTL_File  `](https://docs.oracle.com/database/121/ARPLS/u_file.htm#ARPLS069) package is mainly used for reading and writing the operating system files from PL/SQL. Cloud Storage can be used for any kind of raw file staging. [External tables](/bigquery/external-table-definition) and BigQuery [load](/bigquery/docs/loading-data) and [export](/bigquery/docs/exporting-data) should be used to read and write files from and to Cloud Storage. For more information, see [Introduction to external data sources](/bigquery/external-data-sources) .

### Spatial functions

You can use BigQuery geospatial analytics to replace spatial functionality. There are `  SDO_*  ` functions and types in Oracle such as `  SDO_GEOM_KEY  ` , `  SDO_GEOM_MBR  ` , `  SDO_GEOM_MMB  ` . These functions are used for spatial analysis. You can use [geospatial analytics](/bigquery/docs/geospatial-intro) to do spatial analysis.

## DML syntax

This section addresses differences in data management language syntax between Oracle and BigQuery.

### `     INSERT    ` statement

Most Oracle `  INSERT  ` statements are compatible with BigQuery. The following table shows exceptions.

DML scripts in BigQuery have slightly different consistency semantics than the equivalent statements in Oracle. For an overview of snapshot isolation and session and transaction handling, see the [`  CREATE [UNIQUE] INDEX section  `](#create-index) elsewhere in this document.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Oracle</th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         INSERT INTO                table              VALUES (...);      </code></td>
<td><code dir="ltr" translate="no">         INSERT INTO                table              (...) VALUES (...);      </code>
<p>Oracle offers a <code dir="ltr" translate="no">        DEFAULT       </code> keyword for non-nullable columns.</p>
<p>Note: In BigQuery, omitting column names in the <code dir="ltr" translate="no">        INSERT       </code> statement only works if values for all columns in the target table are included in ascending order based on their ordinal positions.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         INSERT INTO                table              VALUES (1,2,3);              INSERT INTO               table              VALUES (4,5,6);              INSERT INTO               table              VALUES (7,8,9);              INSERT ALL              INTO               table              (col1, col2) VALUES ('val1_1', 'val1_2')              INTO               table              (col1, col2) VALUES ('val2_1', 'val2_2')              INTO               table              (col1, col2) VALUES ('val3_1', 'val3_2')              .              .              .              SELECT 1 FROM DUAL;      </code></td>
<td><code dir="ltr" translate="no">         INSERT INTO                table              VALUES (1,2,3), (4,5,6),              (7,8,9);      </code>
<p>BigQuery imposes <a href="/bigquery/quotas#data-manipulation-language-statements">DML quotas</a> , which restrict the number of DML statements you can execute daily. To make the best use of your quota, consider the following approaches:</p>
<ul>
<li>Combine multiple rows in a single <code dir="ltr" translate="no">         INSERT        </code> statement, instead of one row per <code dir="ltr" translate="no">         INSERT        </code> operation.</li>
<li>Combine multiple DML statements (including <code dir="ltr" translate="no">         INSERT        </code> ) using a <code dir="ltr" translate="no">         MERGE        </code> statement.</li>
<li>Use <code dir="ltr" translate="no">         CREATE TABLE ... AS SELECT        </code> to create and populate new tables.</li>
</ul></td>
</tr>
</tbody>
</table>

### `     UPDATE    ` statement

Oracle `  UPDATE  ` statements are mostly compatible with BigQuery, however, in BigQuery the `  UPDATE  ` statement must have a `  WHERE  ` clause.

As a best practice, you should prefer batch DML statements over multiple single `  UPDATE  ` and `  INSERT  ` statements. DML scripts in BigQuery have slightly different consistency semantics than equivalent statements in Oracle. For an overview on snapshot isolation and session and transaction handling see the [`  CREATE INDEX  `](#create-index) section in this document.

The following table shows Oracle `  UPDATE  ` statements and BigQuery statements that accomplish the same tasks.

In BigQuery the `  UPDATE  ` statement must have a `  WHERE  ` clause. For more information about `  UPDATE  ` in BigQuery, see the [BigQuery UPDATE examples](/bigquery/docs/reference/standard-sql/dml-syntax#update_examples) in the DML documentation.

### `     DELETE    ` and `     TRUNCATE    ` statements

The `  DELETE  ` and `  TRUNCATE  ` statements are both ways to remove rows from a table without affecting the table schema. `  TRUNCATE  ` is not used in BigQuery. However, you can use `  DELETE  ` statements to achieve the same effect.

In BigQuery, the `  DELETE  ` statement must have a `  WHERE  ` clause. For more information about `  DELETE  ` in BigQuery, see the [BigQuery `  DELETE  ` examples](/bigquery/docs/reference/standard-sql/dml-syntax#delete_examples) in the DML documentation.

<table>
<thead>
<tr class="header">
<th>Oracle</th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         DELETE                database              .               table              ;      </code></td>
<td><code dir="ltr" translate="no">         DELETE              FROM               table              WHERE TRUE;      </code></td>
</tr>
</tbody>
</table>

### `     MERGE    ` statement

The `  MERGE  ` statement can combine `  INSERT  ` , `  UPDATE  ` , and `  DELETE  ` operations into a single `  UPSERT  ` statement and perform the operations atomically. The `  MERGE  ` operation must match, at most, one source row for each target row. BigQuery and Oracle both follow ANSI Syntax.

However, DML scripts in BigQuery have slightly different consistency semantics than the equivalent statements in Oracle.

## DDL syntax

This section addresses differences in data definition language syntax between Oracle and BigQuery.

### `     CREATE TABLE    ` statement

Most Oracle [`  CREATE TABLE  `](https://docs.oracle.com/cd/B28359_01/server.111/b28310/tables003.htm#ADMIN01503) statements are compatible with BigQuery, except for the following constraints and syntax elements, which are not used in BigQuery:

  - `  STORAGE  `
  - `  TABLESPACE  `
  - `  DEFAULT  `
  - `  GENERATED ALWAYS AS  `
  - `  ENCRYPT  `
  - `  PRIMARY KEY ( col , ...)  ` . For more information, see [`  CREATE INDEX  `](#create-index) .
  - `  UNIQUE INDEX  ` . For more information, see [`  CREATE INDEX  `](#create-index) .
  - `  CONSTRAINT..REFERENCES  `
  - `  DEFAULT  `
  - `  PARALLEL  `
  - `  COMPRESS  `

For more information about `  CREATE TABLE  ` in BigQuery, see the [BigQuery `  CREATE TABLE  ` examples](/bigquery/docs/reference/standard-sql/data-definition-language#create-table-examples) .

#### Column options and attributes

Identity columns are introduced with Oracle 12c version which enables auto-increment on a column. This is not used in BigQuery, this can be achieved with the following batch way. For more information about surrogate keys and slowly changing dimensions (SCD), refer to the following guides:

  - [BigQuery Surrogate Keys](https://medium.com/google-cloud/bigquery-surrogate-keys-672b2e110f80)
  - [BigQuery and surrogate keys: A practical approach](https://cloud.google.com/blog/products/data-analytics/bigquery-and-surrogate-keys-practical-approach)

<table>
<thead>
<tr class="header">
<th>Oracle</th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         CREATE TABLE              table (              id NUMBER GENERATED ALWAYS AS IDENTITY,              description VARCHAR2(30)              );      </code></td>
<td><code dir="ltr" translate="no">         INSERT INTO              dataset.table SELECT              *,              ROW_NUMBER() OVER () AS id              FROM dataset.table      </code></td>
</tr>
</tbody>
</table>

#### Column comments

Oracle uses `  Comment  ` syntax to add comments on columns. This feature can be similarly implemented in BigQuery using the column description as shown in the following table:

<table>
<thead>
<tr class="header">
<th>Oracle</th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       Comment on column               table              is '               column desc              ';      </code></td>
<td><code dir="ltr" translate="no">         CREATE TABLE                dataset.table              (                col1              STRING                OPTIONS              (description="               column desc              ")              );      </code></td>
</tr>
</tbody>
</table>

#### Temporary tables

Oracle supports [temporary](https://docs.oracle.com/cd/B28359_01/server.111/b28310/tables003.htm#ADMIN11633) tables, which are often used to store intermediate results in scripts. [Temporary](/bigquery/docs/multi-statement-queries#temporary_tables) tables are supported in BigQuery.

<table>
<thead>
<tr class="header">
<th>Oracle</th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         CREATE GLOBAL TEMPORARY TABLE               temp_tab              (x INTEGER,              y VARCHAR2(50))              ON COMMIT DELETE ROWS;              COMMIT;      </code></td>
<td><code dir="ltr" translate="no">         CREATE TEMP TABLE              temp_tab              (              x INT64,              y STRING              );              DELETE FROM temp_tab WHERE TRUE;      </code></td>
</tr>
</tbody>
</table>

The following Oracle elements are not used in BigQuery:

  - `  ON COMMIT DELETE ROWS;  `
  - `  ON COMMIT PRESERVE ROWS;  `

There are also some other ways to emulate temporary tables in BigQuery:

  - **Dataset TTL:** Create a dataset that has a short time to live (for example, one hour) so that any tables created in the dataset are effectively temporary (since they won't persist longer than the dataset's time to live). You can prefix all the table names in this dataset with `  temp  ` to clearly denote that the tables are temporary.

  - **Table TTL:** Create a table that has a table-specific short time to live using DDL statements similar to the following:
    
    ``` text
    CREATE TABLE temp.name (col1, col2, ...)
    
    OPTIONS(expiration_timestamp=TIMESTAMP_ADD(CURRENT_TIMESTAMP(), INTERVAL 1 HOUR));
    ```

  - **`  WITH  ` clause:** If a temporary table is needed only within the same block, use a temporary result using a [`  WITH  `](/bigquery/docs/reference/standard-sql/query-syntax#with_clause) statement or subquery.

### `     CREATE SEQUENCE    ` statement

Sequences are not used in BigQuery, this can be achieved with the following batch way. For more information about surrogate keys and slowly changing dimensions (SCD), refer to the following guides:

  - [BigQuery Surrogate Keys](https://medium.com/google-cloud/bigquery-surrogate-keys-672b2e110f80)
  - [BigQuery and surrogate keys: A practical approach](https://cloud.google.com/blog/products/data-analytics/bigquery-and-surrogate-keys-practical-approach)

<!-- end list -->

``` text
INSERT INTO dataset.table
    SELECT *,
      ROW_NUMBER() OVER () AS id
      FROM dataset.table
```

### `     CREATE VIEW    ` statement

The following table shows equivalents between Oracle and BigQuery for the `  CREATE VIEW  ` statement.

<table>
<thead>
<tr class="header">
<th>Oracle</th>
<th>BigQuery</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         CREATE VIEW                view_name              AS SELECT ...      </code></td>
<td><code dir="ltr" translate="no">         CREATE VIEW                view_name              AS SELECT ...      </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         CREATE OR REPLACE VIEW                view_name              AS SELECT ...      </code></td>
<td><code dir="ltr" translate="no">         CREATE OR REPLACE VIEW       </code> <code dir="ltr" translate="no">         view_name              AS      </code> <code dir="ltr" translate="no">       SELECT ...      </code></td>
<td></td>
</tr>
<tr class="odd">
<td>Not supported</td>
<td><code dir="ltr" translate="no">         CREATE VIEW IF NOT EXISTS       </code> <code dir="ltr" translate="no">         view_name       </code> <code dir="ltr" translate="no">       OPTIONS(               view_option_list              )      </code> <code dir="ltr" translate="no">       AS SELECT ...      </code></td>
<td>Creates a new view only if the view does not currently exist in the specified dataset.</td>
</tr>
</tbody>
</table>

### `     CREATE MATERIALIZED VIEW    ` statement

In BigQuery materialized view refresh operations are done automatically. There is no need to specify refresh options (for example, on commit or on schedule) in BigQuery. For more information, see [Introduction to materialized views](/bigquery/docs/materialized-views-intro) .

In case the base table keeps changing by appends only, the query that uses materialized view (whether view is explicitly referenced or selected by the query optimizer) scans all materialized view plus a delta in the base table since the last view refresh. This means queries are faster and cheaper.

On the contrary, if there were any updates (DML UPDATE / MERGE) or deletions (DML DELETE, truncation, partition expiration) in the base table since the last view refresh, the materialized view are not be scanned and hence query don't get any savings until the next view refresh. Basically, any update or deletion in the base table invalidates the materialized view state.

Also, the data from the streaming buffer of the base table is not saved into materialized view. Streaming buffer is still being scanned fully regardless of whether materialized view is used.

The following table shows equivalents between Oracle and BigQuery for the `  CREATE MATERIALIZED VIEW  ` statement.

<table>
<thead>
<tr class="header">
<th>Oracle</th>
<th>BigQuery</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         CREATE MATERIALIZED VIEW                view_name               REFRESH FAST NEXT sysdate + 7              AS SELECT … FROM TABLE_1      </code></td>
<td><code dir="ltr" translate="no">         CREATE MATERIALIZED VIEW                 view_name              AS SELECT ...      </code></td>
<td></td>
</tr>
</tbody>
</table>

### `     CREATE [UNIQUE] INDEX    ` statement

This section describes approaches in BigQuery for how to create functionality similar to indexes in Oracle.

#### Indexing for performance

BigQuery doesn't need explicit indexes, because it's a column-oriented database with query and storage optimization. BigQuery provides functionality such as [partitioning and clustering](/bigquery/docs/clustered-tables#combine-clustered-partitioned-tables) as well as [nested fields](/bigquery/docs/nested-repeated) , which can increase query efficiency and performance by optimizing how data is stored.

#### Indexing for consistency (UNIQUE, PRIMARY INDEX)

In Oracle, a unique index can be used to prevent rows with non-unique keys in a table. If a process tries to insert or update data that has a value that's already in the index the operation fails with an index violation.

Because BigQuery doesn't provide explicit indexes, a `  MERGE  ` statement can be used instead to insert only unique records into a target table from a staging table while discarding duplicate records. However, there is no way to prevent a user with edit permissions from inserting a duplicate record.

To generate an error for duplicate records in BigQuery you can use a `  MERGE  ` statement from the staging table, as shown in the following example:

Oracle

BigQuery

`  CREATE [UNIQUE] INDEX name;  `

``  MERGE `prototype.FIN_MERGE` t \ USING `prototype.FIN_TEMP_IMPORT` m \ ON t. col1 = m. col1 \ AND t. col2 = m. col2 \ WHEN MATCHED THEN \ UPDATE SET t. col1 = ERROR(CONCAT('Encountered Error for ', m. col1 , ' ', m. col2 )) \ WHEN NOT MATCHED THEN \ INSERT ( col1 , col2 , col3 , col4 , col5 , col6 , col7 , col8 ) VALUES( col1 , col2 , col3 , col4 , col5 , col6 , CURRENT_TIMESTAMP(),CURRENT_TIMESTAMP());  ``

More often, users prefer to [remove duplicates independently](/bigquery/streaming-data-into-bigquery#manually_removing_duplicates) in order to find errors in downstream systems.

BigQuery does not support `  DEFAULT  ` and `  IDENTITY  ` (sequences) columns.

### Locking

BigQuery doesn't have a lock mechanism like Oracle and can run concurrent queries (up to your [quota](/bigquery/quotas) ). Only DML statements have certain [concurrency limits](/bigquery/quotas#data-manipulation-language-statements) and might require a [table lock during execution](/bigquery/docs/data-manipulation-language#dml-limitations) in some scenarios.

## Procedural SQL statements

This section describes how to convert procedural SQL statements used in stored procedures, functions and triggers from Oracle to BigQuery.

### `     CREATE PROCEDURE    ` statement

Stored Procedure is supported as part of BigQuery Scripting Beta.

<table>
<thead>
<tr class="header">
<th>Oracle</th>
<th>BigQuery</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         CREATE PROCEDURE       </code></td>
<td><code dir="ltr" translate="no">         CREATE PROCEDURE       </code></td>
<td>Similar to Oracle, BigQuery supports <code dir="ltr" translate="no">       IN, OUT, INOUT      </code> argument modes. Other syntax specifications are not supported in BigQuery.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         CREATE OR REPLACE PROCEDURE       </code></td>
<td><code dir="ltr" translate="no">         CREATE OR REPLACE PROCEDURE       </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         CALL       </code></td>
<td><code dir="ltr" translate="no">         CALL       </code></td>
<td></td>
</tr>
</tbody>
</table>

The sections that follow describe ways to convert existing Oracle procedural statements to BigQuery scripting statements that have similar functionality.

### `     CREATE TRIGGER    ` statement

Triggers are not used in BigQuery. Row based application logic should be handled on the application layer. Trigger functionality can be achieved utilising the ingestion tool, Pub/Sub and/or Cloud Run functions during the ingestion time or utilising regular scans.

### Variable declaration and assignment

The following table shows Oracle `  DECLARE  ` statements and their BigQuery equivalents.

<table>
<thead>
<tr class="header">
<th>Oracle</th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       DECLARE              L_VAR NUMBER;              BEGIN              L_VAR := 10 + 20;              END;      </code></td>
<td><code dir="ltr" translate="no">         DECLARE              L_VAR int64;              BEGIN              SET L_VAR = 10 + 20;              SELECT L_VAR;              END      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       SET               var              =               value              ;      </code></td>
<td><code dir="ltr" translate="no">         SET                var              =               value              ;      </code></td>
</tr>
</tbody>
</table>

### Cursor declarations and operations

BigQuery does not support cursors, so the following statements are not used in BigQuery:

  - `  DECLARE cursor_name CURSOR [FOR | WITH] ...  `
  - `  OPEN CUR_VAR FOR sql_str;  `
  - `  OPEN cursor_name [USING var, ...];  `
  - `  FETCH cursor_name INTO var, ...;  `
  - `  CLOSE cursor_name;  `

### Dynamic SQL statements

The following Oracle Dynamic SQL statement and its BigQuery equivalent:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Oracle</th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         EXECUTE IMMEDIATE              sql_str       </code>
<p>[USING IN OUT [, ...]];</p></td>
<td><code dir="ltr" translate="no">         EXECUTE IMMEDIATE       </code>
<p>sql_expression [INTO variable[, ...]]</p>
<p>[USING identifier[, ...]];</p>
;</td>
</tr>
</tbody>
</table>

### Flow-of-control statements

The following table shows Oracle flow-of-control statements and their BigQuery equivalents.

<table>
<thead>
<tr class="header">
<th>Oracle</th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         IF              condition THEN              [if_statement_list]              [               ELSE               else_statement_list              ]              END IF;      </code></td>
<td><code dir="ltr" translate="no">         IF              condition THEN              [if_statement_list]              [ELSE              else_statement_list              ]              END IF;      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       SET SERVEROUTPUT ON;              DECLARE              x INTEGER DEFAULT 0;              y INTEGER DEFAULT 0;              BEGIN              LOOP              IF x&gt;= 10 THEN              EXIT;                ELSIF              x&gt;= 5 THEN              y := 5;              END IF;              x := x + 1;              END LOOP;              dbms_output.put_line(x||','||y);              END;              /      </code></td>
<td><code dir="ltr" translate="no">         DECLARE              x INT64 DEFAULT 0;              DECLARE y INT64 DEFAULT 0;              LOOP              IF x&gt;= 10 THEN              LEAVE;              ELSE IF x&gt;= 5 THEN              SET y = 5;              END IF;              END IF;              SET x = x + 1;              END LOOP;              SELECT x,y;      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         LOOP               sql_statement_list              END LOOP;      </code></td>
<td><code dir="ltr" translate="no">         LOOP               sql_statement_list              END LOOP;      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         WHILE              boolean_expression DO              sql_statement_list              END WHILE;      </code></td>
<td><code dir="ltr" translate="no">         WHILE              boolean_expression DO              sql_statement_list              END WHILE;      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         FOR LOOP       </code></td>
<td><code dir="ltr" translate="no">       FOR LOOP      </code> is not used in BigQuery. Use other <code dir="ltr" translate="no">       LOOP      </code> statements.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       BREAK      </code></td>
<td><code dir="ltr" translate="no">         BREAK       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         CONTINUE       </code></td>
<td><code dir="ltr" translate="no">         CONTINUE       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         CONTINUE/EXIT WHEN       </code></td>
<td>Use <code dir="ltr" translate="no">       CONTINUE      </code> with <code dir="ltr" translate="no">       IF      </code> condition.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         GOTO       </code></td>
<td><code dir="ltr" translate="no">       GOTO      </code> statement does not exist in BigQuery. Use <code dir="ltr" translate="no">       IF      </code> condition.</td>
</tr>
</tbody>
</table>

## Metadata and transaction SQL statements

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Oracle</th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         GATHER_STATS_JOB       </code></td>
<td>Not used in BigQuery yet.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         LOCK TABLE                table_name              IN [SHARE/EXCLUSIVE] MODE NOWAIT;      </code></td>
<td>Not used in BigQuery yet.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       Alter session set isolation_level=serializable; /      </code>
<p><code dir="ltr" translate="no">          SET TRANSACTION                ...       </code></p></td>
<td>BigQuery always uses Snapshot Isolation. For details, see <a href="#consistency_guarantees_and_transaction_isolation">Consistency guarantees and transaction isolation</a> in this document.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         EXPLAIN PLAN              ...      </code></td>
<td>Not used in BigQuery.
<p>Similar features are the <a href="/bigquery/query-plan-explanation">query plan explanation in the BigQuery web UI</a> and the slot allocation, and in <a href="/bigquery/docs/monitoring">audit logging in Stackdriver</a> .</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       SELECT * FROM DBA_[*];      </code>
<p>(Oracle DBA_/ALL_/V$ views)</p></td>
<td><code dir="ltr" translate="no">       SELECT * FROM mydataset.INFORMATION_SCHEMA.TABLES;      </code>
<p>For more information, see <a href="/bigquery/docs/information-schema-intro">Introduction to BigQuery INFORMATION_SCHEMA</a> .</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       SELECT * FROM               GV$SESSION              ;      </code>
<p><code dir="ltr" translate="no">        SELECT * FROM                 V$ACTIVE_SESSION_HISTORY                ;       </code></p></td>
<td>BigQuery does not have the traditional session concept. You can view query jobs in the UI or export stackdriver audit logs to BigQuery and analyze BigQuery logs for analyzing jobs. For more information, see <a href="/bigquery/docs/managing-jobs#view-job">View job details</a> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       START TRANSACTION;      </code>
<p><code dir="ltr" translate="no">        LOCK TABLE                 table_A                IN EXCLUSIVE MODE NOWAIT;       </code></p>
<p><code dir="ltr" translate="no">        DELETE FROM                 table_A                ;       </code></p>
<p><code dir="ltr" translate="no">        INSERT INTO                 table_A                SELECT * FROM                 table_B                ;       </code></p>
<p><code dir="ltr" translate="no">        COMMIT;       </code></p></td>
<td>Replacing the contents of a table with query output is the equivalent of a transaction. You can do this with either a <a href="/bigquery/docs/reference/bq-cli-reference#bq_query">query</a> or a <a href="/bigquery/docs/managing-tables#copy-table">copy</a> operation.
<p>Using a query:</p>
<p><code dir="ltr" translate="no">        bq query --replace --                 destination_table                  table_A                'SELECT * FROM                 table_B                ';       </code></p>
<p>Using a copy:</p>
<p><code dir="ltr" translate="no">        bq cp -f                 table_A                  table_B        </code></p></td>
</tr>
</tbody>
</table>

### Multi-statement and multi-line SQL statements

Both Oracle and BigQuery support transactions (sessions) and therefore support statements separated by semicolons that are consistently executed together. For more information, see [Multi-statement transactions](/bigquery/docs/transactions) .

## Error codes and messages

[Oracle error codes](https://docs.oracle.com/database/121/DRDAS/error_code.htm#DRDAS513) and [BigQuery error codes](/bigquery/troubleshooting-errors) are different. If your application logic is currently catching the errors, try to eliminate the source of the error, because BigQuery doesn't return the same error codes.

## Consistency guarantees and transaction isolation

Both Oracle and BigQuery are atomic—that is, ACID-compliant on a per-mutation level across many rows. For example, a `  MERGE  ` operation is atomic, even with multiple inserted and updated values.

### Transactions

Oracle provides read committed or serializable [transaction isolation levels](https://blogs.oracle.com/oraclemagazine/on-transaction-isolation-levels) . Deadlocks are possible. Oracle insert append jobs run independently.

BigQuery also [supports transactions](/bigquery/docs/transactions) . BigQuery helps ensure [optimistic concurrency control](https://en.wikipedia.org/wiki/Optimistic_concurrency_control) (first to commit wins) with [snapshot isolation](https://en.wikipedia.org/wiki/Snapshot_isolation) , in which a query reads the last committed data before the query starts. This approach guarantees the same level of consistency on a per-row, per-mutation basis and across rows within the same DML statement, yet avoids deadlocks. In the case of multiple `  UPDATE  ` statements against the same table, BigQuery switches to [pessimistic concurrency control](/bigquery/docs/data-manipulation-language#dml-limitations) and [queues](https://cloud.google.com/blog/products/data-analytics/dml-without-limits-now-in-bigquery) multiple `  UPDATE  ` statements, automatically retrying in case of conflicts. `  INSERT  ` DML statements and load jobs can run concurrently and independently to append to tables.

### Rollback

Oracle supports [rollbacks](https://docs.oracle.com/cd/B19306_01/server.102/b14200/statements_9021.htm) . As there is no explicit transaction boundary in BigQuery, there is no concept of an explicit rollback in BigQuery. The workarounds are [table decorators](/bigquery/docs/table-decorators) or using [`  FOR SYSTEM_TIME AS OF  `](/bigquery/docs/reference/standard-sql/query-syntax#for_system_time_as_of) .

## Database limits

Check [BigQuery latest quotas and limits](/bigquery/quotas) . Many quotas for large-volume users can be raised by contacting the Cloud Customer Care. The following table shows a comparison of the Oracle and BigQuery database limits.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Oracle</th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Tables per database</td>
<td>Unrestricted</td>
<td>Unrestricted</td>
</tr>
<tr class="even">
<td>Columns per table</td>
<td>1000</td>
<td>10,000</td>
</tr>
<tr class="odd">
<td>Maximum row size</td>
<td>Unlimited (Depends on the column type)</td>
<td>100 MB</td>
</tr>
<tr class="even">
<td>Column and table name length</td>
<td>If v12.2&gt;= 128 Bytes
<p>Else 30 Bytes</p></td>
<td>16,384 Unicode characters</td>
</tr>
<tr class="odd">
<td>Rows per table</td>
<td>Unlimited</td>
<td>Unlimited</td>
</tr>
<tr class="even">
<td>Maximum SQL request length</td>
<td>Unlimited</td>
<td>1 MB (maximum unresolved GoogleSQL query length)
<p>12 MB (maximum resolved legacy and GoogleSQL query length)</p>
<p>Streaming:</p>
<ul>
<li>10 MB (HTTP request size limit)</li>
<li>10,000 (maximum rows per request)</li>
</ul></td>
</tr>
<tr class="odd">
<td>Maximum request &amp; response size</td>
<td>Unlimited</td>
<td>10 MB (request) and 10 GB (response), or virtually unlimited if you use pagination or the Cloud Storage API.</td>
</tr>
<tr class="even">
<td>Maximum number of concurrent sessions</td>
<td>Limited by the sessions or processes parameters</td>
<td>100 concurrent queries (can be raised with <a href="/bigquery/docs/slots">slot reservation</a> ), 300 concurrent API requests per user.</td>
</tr>
<tr class="odd">
<td>Maximum number of concurrent (fast) loads</td>
<td>Limited by the sessions or processes parameters</td>
<td>No concurrency limit; jobs are queued. 100,000 load jobs per project per day.</td>
</tr>
</tbody>
</table>

Other Oracle Database limits includes [data type limits](https://docs.oracle.com/en/database/oracle/oracle-database/19/refrn/datatype-limits.html#GUID-963C79C9-9303-49FE-8F2D-C8AAF04D3095) , [physical database limits](https://docs.oracle.com/en/database/oracle/oracle-database/19/refrn/physical-database-limits.html#GUID-939CB455-783E-458A-A2E8-81172B990FE9) , [logical database limits](https://docs.oracle.com/en/database/oracle/oracle-database/19/refrn/logical-database-limits.html#GUID-685230CF-63F5-4C5A-B8B0-037C566BDA76) and [process and runtime limits](https://docs.oracle.com/en/database/oracle/oracle-database/19/refrn/process-and-runtime-limits.html#GUID-213CC210-4B96-420C-B5B8-3A217F17FC2C) .
