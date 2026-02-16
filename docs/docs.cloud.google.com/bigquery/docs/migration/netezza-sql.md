# IBM Netezza SQL translation guide

IBM Netezza data warehousing is designed to work with Netezza-specific SQL syntax. Netezza SQL is based on Postgres 7.2. SQL scripts written for Netezza can't be used in a BigQuery data warehouse without alterations, because the SQL dialects vary.

This document details the similarities and differences in SQL syntax between Netezza and BigQuery in the following areas:

  - Data types
  - SQL language elements
  - Query syntax
  - Data manipulation language (DML)
  - Data definition language (DDL)
  - Stored procedures
  - Functions

You can also use [batch SQL translation](/bigquery/docs/batch-sql-translator) to migrate your SQL scripts in bulk, or [interactive SQL translation](/bigquery/docs/interactive-sql-translator) to translate ad-hoc queries. IBM Netezza SQL/NZPLSQL is supported by both tools in [preview](https://cloud.google.com/products#product-launch-stages) .

## Data types

<table>
<thead>
<tr class="header">
<th><strong>Netezza</strong></th>
<th><strong>BigQuery</strong></th>
<th><strong>Notes</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       INTEGER/INT/INT4      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/data-types#integer_types"><code dir="ltr" translate="no">        INT64       </code></a></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       SMALLINT/INT2      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/data-types#integer_types"><code dir="ltr" translate="no">        INT64       </code></a></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       BYTEINT/INT1      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/data-types#integer_types"><code dir="ltr" translate="no">        INT64       </code></a></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       BIGINT/INT8      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/data-types#integer_types"><code dir="ltr" translate="no">        INT64       </code></a></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       DECIMAL      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/data-types#numeric-type"><code dir="ltr" translate="no">        NUMERIC       </code></a></td>
<td>The <code dir="ltr" translate="no">       DECIMAL      </code> data type in Netezza is an alias for the <code dir="ltr" translate="no">       NUMERIC      </code> data type.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       NUMERIC      </code> ]</td>
<td><a href="/bigquery/docs/reference/standard-sql/data-types#numeric-type"><code dir="ltr" translate="no">        NUMERIC       </code></a> <a href="/bigquery/docs/reference/standard-sql/data-types#integer_types"><code dir="ltr" translate="no">        INT64       </code></a></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       NUMERIC(p,s)      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/data-types#numeric-type"><code dir="ltr" translate="no">        NUMERIC       </code></a></td>
<td>The <code dir="ltr" translate="no">       NUMERIC      </code> type in BigQuery does not enforce custom digit or scale bounds (constraints) like Netezza does. BigQuery has fixed 9 digits after the decimal, while Netezza allows a custom setup. In Netezza, precision <code dir="ltr" translate="no">       p      </code> can range from 1 to 38, and scale <code dir="ltr" translate="no">       s      </code> from 0 to the precision.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       FLOAT(p)      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/data-types#floating_point_types"><code dir="ltr" translate="no">        FLOAT64       </code></a></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       REAL/FLOAT(6)      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/data-types#floating_point_types"><code dir="ltr" translate="no">        FLOAT64       </code></a></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       DOUBLE PRECISION/FLOAT(14)      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/data-types#floating_point_types"><code dir="ltr" translate="no">        FLOAT64       </code></a></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       CHAR/CHARACTER      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#string"><code dir="ltr" translate="no">        STRING       </code></a></td>
<td>The <code dir="ltr" translate="no">       STRING      </code> type in BigQuery is variable-length and does not require manually setting a max character length as the Netezza <code dir="ltr" translate="no">       CHARACTER      </code> and <code dir="ltr" translate="no">       VARCHAR      </code> types require. The default value of <code dir="ltr" translate="no">       n      </code> in <code dir="ltr" translate="no">       CHAR(n)      </code> is 1. The maximum character string size is 64,000.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       VARCHAR      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#string"><code dir="ltr" translate="no">        STRING       </code></a></td>
<td>The <code dir="ltr" translate="no">       STRING      </code> type in BigQuery is variable-length and does not require manually setting a max character length as the Netezza <code dir="ltr" translate="no">       CHARACTER      </code> and <code dir="ltr" translate="no">       VARCHAR      </code> types require. The maximum character string size is 64,000.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       NCHAR      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#string"><code dir="ltr" translate="no">        STRING       </code></a></td>
<td>The <code dir="ltr" translate="no">       STRING      </code> type in BigQuery is stored as variable length UTF-8 encoded Unicode. The maximum length is 16,000 characters.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       NVARCHAR      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#string"><code dir="ltr" translate="no">        STRING       </code></a></td>
<td>The <code dir="ltr" translate="no">       STRING      </code> type in BigQuery is stored as variable-length UTF-8-encoded Unicode. The maximum length is 16,000 characters.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       VARBINARY      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/data-types#bytes_type"><code dir="ltr" translate="no">        BYTES       </code></a></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ST_GEOMETRY      </code></td>
<td><a href="/bigquery/docs/gis-data"><code dir="ltr" translate="no">        GEOGRAPHY       </code></a></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       BOOLEAN/BOOL      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/data-types#boolean_type"><code dir="ltr" translate="no">        BOOL       </code></a></td>
<td>The <code dir="ltr" translate="no">       BOOL      </code> type in BigQuery can only accept <code dir="ltr" translate="no">       TRUE/FALSE      </code> , unlike the <code dir="ltr" translate="no">       BOOL      </code> type in Netezza, which can accept a variety of values like <code dir="ltr" translate="no">       0/1      </code> , <code dir="ltr" translate="no">       yes/no      </code> , <code dir="ltr" translate="no">       true/false,      </code> <code dir="ltr" translate="no">       on/off      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       DATE      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/data-types#date_type"><code dir="ltr" translate="no">        DATE       </code></a></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       TIME      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/data-types#time_type"><code dir="ltr" translate="no">        TIME       </code></a></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       TIMETZ/TIME WITH TIME ZONE      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/data-types#time_type"><code dir="ltr" translate="no">        TIME       </code></a></td>
<td>Netezza stores the <code dir="ltr" translate="no">       TIME      </code> data type in UTC and lets you pass an offset from UTC using the <code dir="ltr" translate="no">       WITH TIME ZONE      </code> syntax. The <code dir="ltr" translate="no">       TIME      </code> data type in BigQuery represents a time that's independent of any date or time zone.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/data-types#datetime_type"><code dir="ltr" translate="no">        DATETIME       </code></a></td>
<td>The Netezza <code dir="ltr" translate="no">       TIMESTAMP      </code> type does not include a time zone, the same as the BigQuery <code dir="ltr" translate="no">       DATETIME      </code> type.</td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/data-types#array_type"><code dir="ltr" translate="no">        ARRAY       </code></a></td>
<td>There is no array data type in Netezza. The array type is instead stored in a varchar field.</td>
</tr>
</tbody>
</table>

## Timestamp and date type formatting

When you convert date type formatting elements from Netezza to GoogleSQL, you must pay particular attention to time zone differences between `  TIMESTAMP  ` and `  DATETIME  ` , as summarized in the following table:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Netezza</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       CURRENT_TIMESTAMP      </code><br />
<code dir="ltr" translate="no">       CURRENT_TIME      </code><br />
<br />
<code dir="ltr" translate="no">       TIME      </code> information in Netezza can have different time zone information, which is defined using the <code dir="ltr" translate="no">       WITH TIME ZONE      </code> syntax.</td>
<td>If possible, use the <code dir="ltr" translate="no">       CURRENT_TIMESTAMP      </code> function, which is formatted correctly. However, the output format does not always show the UTC time zone (internally, BigQuery does not have a time zone). The <code dir="ltr" translate="no">       DATETIME      </code> object in the bq command-line tool and Google Cloud console is formatted using a <code dir="ltr" translate="no">       T      </code> separator according to RFC 3339. However, in Python and Java JDBC, a space is used as a separator. Use the explicit <a href="/bigquery/docs/reference/standard-sql/datetime_functions#format_datetime"><code dir="ltr" translate="no">        FORMAT_DATETIME       </code></a> function to define the date format correctly. Otherwise, an explicit cast is made to a string, for example:<br />
<code dir="ltr" translate="no">       CAST(CURRENT_DATETIME() AS STRING)      </code><br />
This also returns a space separator.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       CURRENT_DATE      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/date_functions#current_date"><code dir="ltr" translate="no">        CURRENT_DATE       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       CURRENT_DATE-3      </code></td>
<td>BigQuery does not support arithmetic data operations. Instead, use the <a href="/bigquery/docs/reference/standard-sql/date_functions#date_add"><code dir="ltr" translate="no">        DATE_ADD       </code></a> function.</td>
</tr>
</tbody>
</table>

## `     SELECT    ` statement

Generally, the Netezza `  SELECT  ` statement is compatible with BigQuery. The following table contains a list of exceptions:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Netezza</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>A <code dir="ltr" translate="no">       SELECT      </code> statement without <code dir="ltr" translate="no">       FROM      </code> clause</td>
<td>Supports special case such as the following:
<p><code dir="ltr" translate="no">        SELECT 1 UNION ALL SELECT 2;       </code></p></td>
</tr>
<tr class="even">
<td><pre class="text" dir="ltr" data-is-upgraded="" translate="no"><code>SELECT
  (subquery) AS flag,
  CASE WHEN flag = 1 THEN ...</code></pre></td>
<td>In BigQuery, columns cannot reference the output of other columns defined within the same query. You must duplicate the logic or move the logic into a nested query.
<p>Option 1</p>
<pre class="text" dir="ltr" data-is-upgraded="" translate="no"><code>SELECT
  (subquery) AS flag,
  CASE WHEN (subquery) = 1 THEN ...</code></pre>
<p>Option 2</p>
<pre class="text" dir="ltr" data-is-upgraded="" translate="no"><code>SELECT
  q.*,
  CASE WHEN flag = 1 THEN ...
FROM (
  SELECT
    (subquery) AS flag,
    ...
  ) AS q</code></pre></td>
</tr>
</tbody>
</table>

## Comparison operators

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Netezza</strong></th>
<th><strong>BigQuery</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       exp = exp2      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/operators#comparison_operators"><code dir="ltr" translate="no">        exp = exp2       </code></a></td>
<td>Equal</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       exp &lt;= exp2      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/operators#comparison_operators"><code dir="ltr" translate="no">        exp &lt;= exp2       </code></a></td>
<td>Less than or equal to</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       exp &lt; exp2      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/operators#comparison_operators"><code dir="ltr" translate="no">        exp &lt; exp2       </code></a></td>
<td>Less than</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       exp &lt;&gt; exp2      </code><br />
<code dir="ltr" translate="no">       exp != exp2      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/operators#comparison_operators"><code dir="ltr" translate="no">        exp &lt;&gt; exp2       </code></a><br />
<a href="/bigquery/docs/reference/standard-sql/operators#comparison_operators"><code dir="ltr" translate="no">        exp != exp2       </code></a></td>
<td>Not equal</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       exp &gt;= exp2      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/operators#comparison_operators"><code dir="ltr" translate="no">        exp &gt;= exp2       </code></a></td>
<td>Greater than or equal to</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       exp &gt; exp2      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/operators#comparison_operators"><code dir="ltr" translate="no">        exp &gt; exp2       </code></a></td>
<td>Greater than</td>
</tr>
</tbody>
</table>

## Built-in SQL functions

<table>
<thead>
<tr class="header">
<th><strong>Netezza</strong></th>
<th><strong>BigQuery</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       CURRENT_DATE      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/date_functions#current_date"><code dir="ltr" translate="no">        CURRENT_DATE       </code></a></td>
<td>Get the current date (year, month, and day).</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       CURRENT_TIME      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/time_functions#current_time"><code dir="ltr" translate="no">        CURRENT_TIME       </code></a></td>
<td>Get the current time with fraction.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       CURRENT_TIMESTAMP      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#current_timestamp"><code dir="ltr" translate="no">        CURRENT_TIMESTAMP       </code></a></td>
<td>Get the current system date and time, to the nearest full second.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       NOW      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#current_timestamp"><code dir="ltr" translate="no">        CURRENT_TIMESTAMP       </code></a></td>
<td>Get the current system date and time, to the nearest full second.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       COALESCE(exp, 0)      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/conditional_expressions#coalesce"><code dir="ltr" translate="no">        COALESCE(exp, 0)       </code></a></td>
<td>Replace <code dir="ltr" translate="no">       NULL      </code> with zero.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       NVL(exp, 0)      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/conditional_expressions#ifnull"><code dir="ltr" translate="no">        IFNULL(exp, 0)       </code></a></td>
<td>Replace <code dir="ltr" translate="no">       NULL      </code> with zero.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       EXTRACT(DOY FROM timestamp_expression)      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/date_functions#extract"><code dir="ltr" translate="no">        EXTRACT(DAYOFYEAR FROM timestamp_expression)       </code></a></td>
<td>Return the number of days from the beginning of the year.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ADD_MONTHS(date_expr, num_expr)      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/date_functions#date_add"><code dir="ltr" translate="no">        DATE_ADD(date, INTERVAL k MONTH)       </code></a></td>
<td>Add months to a date.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       DURATION_ADD(date, k)      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/date_functions#date_add"><code dir="ltr" translate="no">        DATE_ADD(date, INTERVAL k DAY)       </code></a></td>
<td>Perform addition on dates.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       DURATION_SUBTRACT(date, k)      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/date_functions#date_sub"><code dir="ltr" translate="no">        DATE_SUB(date, INTERVAL k DAY)       </code></a></td>
<td>Perform subtraction on dates.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       str1 || str2      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#concat"><code dir="ltr" translate="no">        CONCAT(str1, str2)       </code></a></td>
<td>Concatenate strings.</td>
</tr>
</tbody>
</table>

## Functions

This section compares Netezza and BigQuery functions.

### Aggregate functions

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Netezza</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#any_value"><code dir="ltr" translate="no">        ANY_VALUE       </code></a></td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/approximate_aggregate_functions#approx_count_distinct"><code dir="ltr" translate="no">        APPROX_COUNT_DISTINCT       </code></a></td>
</tr>
<tr class="odd">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/approximate_aggregate_functions#approx_quantiles"><code dir="ltr" translate="no">        APPROX_QUANTILES       </code></a></td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/approximate_aggregate_functions#approx_top_count"><code dir="ltr" translate="no">        APPROX_TOP_COUNT       </code></a></td>
</tr>
<tr class="odd">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/approximate_aggregate_functions#approx_top_sum"><code dir="ltr" translate="no">        APPROX_TOP_SUM       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       AVG      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#avg"><code dir="ltr" translate="no">        AVG       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       intNand      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#bit_and"><code dir="ltr" translate="no">        BIT_AND       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       intNnot      </code></td>
<td>Bitwise not operator: <a href="/bigquery/docs/reference/standard-sql/operators#bitwise_operators"><code dir="ltr" translate="no">        ~       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       intNor      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#bit_or"><code dir="ltr" translate="no">        BIT_OR       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       intNxor      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#bit_xor"><code dir="ltr" translate="no">        BIT_XOR       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       intNshl      </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       intNshr      </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       CORR      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/statistical_aggregate_functions#corr"><code dir="ltr" translate="no">        CORR       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       COUNT      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#count"><code dir="ltr" translate="no">        COUNT       </code></a></td>
</tr>
<tr class="odd">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#countif"><code dir="ltr" translate="no">        COUNTIF       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       COVAR_POP      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/statistical_aggregate_functions#covar_pop"><code dir="ltr" translate="no">        COVAR_POP       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       COVAR_SAMP      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/statistical_aggregate_functions#covar_samp"><code dir="ltr" translate="no">        COVAR_SAMP       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       GROUPING      </code></td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#logical_and"><code dir="ltr" translate="no">        LOGICAL_AND       </code></a></td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#logical_or"><code dir="ltr" translate="no">        LOGICAL_OR       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       MAX      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#max"><code dir="ltr" translate="no">        MAX       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       MIN      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#min"><code dir="ltr" translate="no">        MIN       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       MEDIAN      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/navigation_functions#percentile_cont"><code dir="ltr" translate="no">        PERCENTILE_CONT       </code></a> <code dir="ltr" translate="no">       (x, 0.5)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       STDDEV_POP      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/statistical_aggregate_functions#stddev_pop"><code dir="ltr" translate="no">        STDDEV_POP       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       STDDEV_SAMP      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/statistical_aggregate_functions#stddev_samp"><code dir="ltr" translate="no">        STDDEV_SAMP       </code></a><br />
<a href="/bigquery/docs/reference/standard-sql/statistical_aggregate_functions#stddev"><code dir="ltr" translate="no">        STDDEV       </code></a></td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#string_agg"><code dir="ltr" translate="no">        STRING_AGG       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       SUM      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#sum"><code dir="ltr" translate="no">        SUM       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       VAR_POP      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/statistical_aggregate_functions#var_pop"><code dir="ltr" translate="no">        VAR_POP       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       VAR_SAMP      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/statistical_aggregate_functions#var_samp"><code dir="ltr" translate="no">        VAR_SAMP       </code></a><br />
<a href="/bigquery/docs/reference/standard-sql/statistical_aggregate_functions#variance"><code dir="ltr" translate="no">        VARIANCE       </code></a></td>
</tr>
</tbody>
</table>

### Analytical functions

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Netezza</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#any_value"><code dir="ltr" translate="no">        ANY_VALUE       </code></a></td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#array_agg"><code dir="ltr" translate="no">        ARRAY_AGG       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       ARRAY_CONCAT      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#array_concat_agg"><code dir="ltr" translate="no">        ARRAY_CONCAT_AGG       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ARRAY_COMBINE      </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       ARRAY_COUNT      </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ARRAY_SPLIT      </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       ARRAY_TYPE      </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       AVG      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#avg"><code dir="ltr" translate="no">        AVG       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       intNand      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#bit_and"><code dir="ltr" translate="no">        BIT_AND       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       intNnot      </code></td>
<td>Bitwise not operator: <a href="/bigquery/docs/reference/standard-sql/operators#bitwise_operators"><code dir="ltr" translate="no">        ~       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       intNor      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#bit_or"><code dir="ltr" translate="no">        BIT_OR       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       intNxor      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#bit_xor"><code dir="ltr" translate="no">        BIT_XOR       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       intNshl      </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       intNshr      </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       CORR      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/statistical_aggregate_functions#corr"><code dir="ltr" translate="no">        CORR       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       COUNT      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#count"><code dir="ltr" translate="no">        COUNT       </code></a></td>
</tr>
<tr class="odd">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#countif"><code dir="ltr" translate="no">        COUNTIF       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       COVAR_POP      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/statistical_aggregate_functions#covar_pop"><code dir="ltr" translate="no">        COVAR_POP       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       COVAR_SAMP      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/statistical_aggregate_functions#covar_samp"><code dir="ltr" translate="no">        COVAR_SAMP       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       CUME_DIST      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/numbering_functions#cume_dist"><code dir="ltr" translate="no">        CUME_DIST       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       DENSE_RANK      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/numbering_functions#dense_rank"><code dir="ltr" translate="no">        DENSE_RANK       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       FIRST_VALUE      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/navigation_functions#first_value"><code dir="ltr" translate="no">        FIRST_VALUE       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       LAG      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/navigation_functions#lag"><code dir="ltr" translate="no">        LAG       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       LAST_VALUE      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/navigation_functions#last_value"><code dir="ltr" translate="no">        LAST_VALUE       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       LEAD      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/navigation_functions#lead"><code dir="ltr" translate="no">        LEAD       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       AND      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#logical_and"><code dir="ltr" translate="no">        LOGICAL_AND       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       OR      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#logical_or"><code dir="ltr" translate="no">        LOGICAL_OR       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       MAX      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#max"><code dir="ltr" translate="no">        MAX       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       MIN      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#min"><code dir="ltr" translate="no">        MIN       </code></a></td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/navigation_functions#nth_value"><code dir="ltr" translate="no">        NTH_VALUE       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       NTILE      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/numbering_functions#ntile"><code dir="ltr" translate="no">        NTILE       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       PERCENT_RANK      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/numbering_functions#percent_rank"><code dir="ltr" translate="no">        PERCENT_RANK       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       PERCENTILE_CONT      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/navigation_functions#percentile_cont"><code dir="ltr" translate="no">        PERCENTILE_CONT       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       PERCENTILE_DISC      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/navigation_functions#percentile_disc"><code dir="ltr" translate="no">        PERCENTILE_DISC       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       RANK      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/numbering_functions#rank"><code dir="ltr" translate="no">        RANK       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ROW_NUMBER      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/numbering_functions#row_number"><code dir="ltr" translate="no">        ROW_NUMBER       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       STDDEV      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/statistical_aggregate_functions#stddev"><code dir="ltr" translate="no">        STDDEV       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       STDDEV_POP      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/statistical_aggregate_functions#stddev_pop"><code dir="ltr" translate="no">        STDDEV_POP       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       STDDEV_SAMP      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/statistical_aggregate_functions#stddev_samp"><code dir="ltr" translate="no">        STDDEV_SAMP       </code></a></td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#string_agg"><code dir="ltr" translate="no">        STRING_AGG       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       SUM      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#sum"><code dir="ltr" translate="no">        SUM       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       VARIANCE      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/statistical_aggregate_functions#variance"><code dir="ltr" translate="no">        VARIANCE       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       VAR_POP      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/statistical_aggregate_functions#var_pop"><code dir="ltr" translate="no">        VAR_POP       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       VAR_SAMP      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/statistical_aggregate_functions#var_samp"><code dir="ltr" translate="no">        VAR_SAMP       </code></a><br />
<a href="/bigquery/docs/reference/standard-sql/statistical_aggregate_functions#variance"><code dir="ltr" translate="no">        VARIANCE       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       WIDTH_BUCKET      </code></td>
<td></td>
</tr>
</tbody>
</table>

### Date and time functions

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Netezza</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       ADD_MONTHS      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/date_functions#date_add"><code dir="ltr" translate="no">        DATE_ADD       </code></a><br />
<a href="/bigquery/docs/reference/standard-sql/timestamp_functions#timestamp_add"><code dir="ltr" translate="no">        TIMESTAMP_ADD       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       AGE      </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       CURRENT_DATE      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/date_functions#current_date"><code dir="ltr" translate="no">        CURRENT_DATE       </code></a></td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/datetime_functions#current_datetime"><code dir="ltr" translate="no">        CURRENT_DATETIME       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       CURRENT_TIME      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/time_functions#current_time"><code dir="ltr" translate="no">        CURRENT_TIME       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       CURRENT_TIME(p)      </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       CURRENT_TIMESTAMP      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#current_timestamp"><code dir="ltr" translate="no">        CURRENT_TIMESTAMP       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       CURRENT_TIMESTAMP(p)      </code></td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/date_functions#date"><code dir="ltr" translate="no">        DATE       </code></a></td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/date_functions#date_add"><code dir="ltr" translate="no">        DATE_ADD       </code></a></td>
</tr>
<tr class="odd">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/date_functions#date_diff"><code dir="ltr" translate="no">        DATE_DIFF       </code></a></td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/date_functions#date_from_unix_date"><code dir="ltr" translate="no">        DATE_FROM_UNIX_DATE       </code></a></td>
</tr>
<tr class="odd">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/date_functions#date_sub"><code dir="ltr" translate="no">        DATE_SUB       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       DATE_TRUNC      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/date_functions#date_trunc"><code dir="ltr" translate="no">        DATE_TRUNC       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       DATE_PART      </code></td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/datetime_functions#datetime"><code dir="ltr" translate="no">        DATETIME       </code></a></td>
</tr>
<tr class="odd">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/datetime_functions#datetime_add"><code dir="ltr" translate="no">        DATETIME_ADD       </code></a></td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/datetime_functions#datetime_diff"><code dir="ltr" translate="no">        DATETIME_DIFF       </code></a></td>
</tr>
<tr class="odd">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/datetime_functions#datetime_sub"><code dir="ltr" translate="no">        DATETIME_SUB       </code></a></td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/datetime_functions#datetime_trunc"><code dir="ltr" translate="no">        DATETIME_TRUNC       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       DURATION_ADD      </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       DURATION_SUBTRACT      </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       EXTRACT      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/date_functions#extract"><code dir="ltr" translate="no">        EXTRACT (DATE)       </code></a><br />
<a href="/bigquery/docs/reference/standard-sql/timestamp_functions#extract"><code dir="ltr" translate="no">        EXTRACT (TIMESTAMP)       </code></a></td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/date_functions#format_date"><code dir="ltr" translate="no">        FORMAT_DATE       </code></a></td>
</tr>
<tr class="odd">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/datetime_functions#format_datetime"><code dir="ltr" translate="no">        FORMAT_DATETIME       </code></a></td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/time_functions#format_time"><code dir="ltr" translate="no">        FORMAT_TIME       </code></a></td>
</tr>
<tr class="odd">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#format_timestamp"><code dir="ltr" translate="no">        FORMAT_TIMESTAMP       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       LAST_DAY      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/date_functions#date_sub"><code dir="ltr" translate="no">        DATE_SUB       </code></a> <code dir="ltr" translate="no">       (      </code> <a href="/bigquery/docs/reference/standard-sql/date_functions#date_trunc"><code dir="ltr" translate="no">        DATE_TRUNC       </code></a> <code dir="ltr" translate="no">       (      </code> <a href="/bigquery/docs/reference/standard-sql/date_functions#date_add"><code dir="ltr" translate="no">        DATE_ADD       </code></a> <code dir="ltr" translate="no">       (      </code> <code dir="ltr" translate="no">       date_expression, INTERVAL 1 MONTH ), MONTH ),      </code> <code dir="ltr" translate="no">       INTERVAL 1 DAY )      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       MONTHS_BETWEEN      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/date_functions#date_diff"><code dir="ltr" translate="no">        DATE_DIFF       </code></a> <code dir="ltr" translate="no">       (date_expression,      </code> <code dir="ltr" translate="no">       date_expression, MONTH)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       NEXT_DAY      </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       NOW      </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       OVERLAPS      </code></td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/date_functions#parse_date"><code dir="ltr" translate="no">        PARSE_DATE       </code></a></td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/datetime_functions#parse_datetime"><code dir="ltr" translate="no">        PARSE_DATETIME       </code></a></td>
</tr>
<tr class="odd">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/time_functions#parse_time"><code dir="ltr" translate="no">        PARSE_TIME       </code></a></td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#parse_timestamp"><code dir="ltr" translate="no">        PARSE_TIMESTAMP       </code></a></td>
</tr>
<tr class="odd">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#string"><code dir="ltr" translate="no">        STRING       </code></a></td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/time_functions#time"><code dir="ltr" translate="no">        TIME       </code></a></td>
</tr>
<tr class="odd">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/time_functions#time_add"><code dir="ltr" translate="no">        TIME_ADD       </code></a></td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/time_functions#time_diff"><code dir="ltr" translate="no">        TIME_DIFF       </code></a></td>
</tr>
<tr class="odd">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/time_functions#time_sub"><code dir="ltr" translate="no">        TIME_SUB       </code></a></td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/time_functions#time_trunc"><code dir="ltr" translate="no">        TIME_TRUNC       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       TIMEOFDAY      </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/datetime_functions#datetime"><code dir="ltr" translate="no">        DATETIME       </code></a></td>
</tr>
<tr class="odd">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#timestamp_add"><code dir="ltr" translate="no">        TIMESTAMP_ADD       </code></a></td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#timestamp_diff"><code dir="ltr" translate="no">        TIMESTAMP_DIFF       </code></a></td>
</tr>
<tr class="odd">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#timestamp_micros"><code dir="ltr" translate="no">        TIMESTAMP_MICROS       </code></a></td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#timestamp_millis"><code dir="ltr" translate="no">        TIMESTAMP_MILLIS       </code></a></td>
</tr>
<tr class="odd">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#timestamp_seconds"><code dir="ltr" translate="no">        TIMESTAMP_SECONDS       </code></a></td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#timestamp_sub"><code dir="ltr" translate="no">        TIMESTAMP_SUB       </code></a></td>
</tr>
<tr class="odd">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#timestamp_trunc"><code dir="ltr" translate="no">        TIMESTAMP_TRUNC       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       TIMEZONE      </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       TO_DATE      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/date_functions#parse_date"><code dir="ltr" translate="no">        PARSE_DATE       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       TO_TIMESTAMP      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#parse_timestamp"><code dir="ltr" translate="no">        PARSE_TIMESTAMP       </code></a></td>
</tr>
<tr class="odd">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/date_functions#unix_date"><code dir="ltr" translate="no">        UNIX_DATE       </code></a></td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#unix_micros"><code dir="ltr" translate="no">        UNIX_MICROS       </code></a></td>
</tr>
<tr class="odd">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#unix_millis"><code dir="ltr" translate="no">        UNIX_MILLIS       </code></a></td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#unix_seconds"><code dir="ltr" translate="no">        UNIX_SECONDS       </code></a></td>
</tr>
</tbody>
</table>

### String functions

<table>
<thead>
<tr class="header">
<th><strong>Netezza</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       ASCII      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#to_code_points"><code dir="ltr" translate="no">        TO_CODE_POINTS       </code></a> <code dir="ltr" translate="no">       (string_expr)[OFFSET(0)]      </code></td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#byte_length"><code dir="ltr" translate="no">        BYTE_LENGTH       </code></a></td>
</tr>
<tr class="odd">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#to_hex"><code dir="ltr" translate="no">        TO_HEX       </code></a></td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#char_length"><code dir="ltr" translate="no">        CHAR_LENGTH       </code></a></td>
</tr>
<tr class="odd">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#character_length"><code dir="ltr" translate="no">        CHARACTER_LENGTH       </code></a></td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#code_points_to_bytes"><code dir="ltr" translate="no">        CODE_POINTS_TO_BYTES       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       BTRIM      </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       CHR      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#code_points_to_string"><code dir="ltr" translate="no">        CODE_POINTS_TO_STRING       </code></a> <code dir="ltr" translate="no">       ([numeric_expr])      </code></td>
</tr>
<tr class="odd">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#concat"><code dir="ltr" translate="no">        CONCAT       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       DBL_MP      </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       DLE_DST      </code></td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#ends_with"><code dir="ltr" translate="no">        ENDS_WITH       </code></a></td>
</tr>
<tr class="odd">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#format_string"><code dir="ltr" translate="no">        FORMAT       </code></a></td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#from_base32"><code dir="ltr" translate="no">        FROM_BASE32       </code></a></td>
</tr>
<tr class="odd">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#from_base64"><code dir="ltr" translate="no">        FROM_BASE64       </code></a></td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#from_hex"><code dir="ltr" translate="no">        FROM_HEX       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       HEX_TO_BINARY      </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       HEX_TO_GEOMETRY      </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       INITCAP      </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       INSTR      </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       INT_TO_STRING      </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       LE_DST      </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       LENGTH      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#length"><code dir="ltr" translate="no">        LENGTH       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       LOWER      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#lower"><code dir="ltr" translate="no">        LOWER       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       LPAD      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#lpad"><code dir="ltr" translate="no">        LPAD       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       LTRIM      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#ltrim"><code dir="ltr" translate="no">        LTRIM       </code></a></td>
</tr>
<tr class="odd">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#normalize"><code dir="ltr" translate="no">        NORMALIZE       </code></a></td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#normalize_and_casefold"><code dir="ltr" translate="no">        NORMALIZE_AND_CASEFOLD       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       PRI_MP      </code></td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#regexp_contains"><code dir="ltr" translate="no">        REGEXP_CONTAINS       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       REGEXP_EXTRACT      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#regexp_extract"><code dir="ltr" translate="no">        REGEXP_EXTRACT       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       REGEXP_EXTRACT_ALL      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#regexp_extract_all"><code dir="ltr" translate="no">        REGEXP_EXTRACT_ALL       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       REGEXP_EXTRACT_ALL_SP      </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       REGEXP_EXTRACT_SP      </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       REGEXP_INSTR      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#strpos"><code dir="ltr" translate="no">        STRPOS       </code></a> <code dir="ltr" translate="no">       (col,      </code> <a href="/bigquery/docs/reference/standard-sql/string_functions#regexp_extract"><code dir="ltr" translate="no">        REGEXP_EXTRACT       </code></a> <code dir="ltr" translate="no">       ()      </code> )</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       REGEXP_LIKE      </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       REGEXP_MATCH_COUNT      </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       REGEXP_REPLACE      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#regexp_replace"><code dir="ltr" translate="no">        REGEXP_REPLACE       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       REGEXP_REPLACE_SP      </code></td>
<td><code dir="ltr" translate="no">       IF(      </code> <a href="/bigquery/docs/reference/standard-sql/string_functions#regexp_contains"><code dir="ltr" translate="no">        REGEXP_CONTAINS       </code></a> <code dir="ltr" translate="no">       ,1,0)      </code></td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#regexp_extract"><code dir="ltr" translate="no">        REGEXP_EXTRACT       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       REPEAT      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#repeat"><code dir="ltr" translate="no">        REPEAT       </code></a></td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#replace"><code dir="ltr" translate="no">        REPLACE       </code></a></td>
</tr>
<tr class="odd">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#reverse"><code dir="ltr" translate="no">        REVERSE       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       RPAD      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#rpad"><code dir="ltr" translate="no">        RPAD       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       RTRIM      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#rtrim"><code dir="ltr" translate="no">        RTRIM       </code></a></td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#safe_convert_bytes_to_string"><code dir="ltr" translate="no">        SAFE_CONVERT_BYTES_TO_STRING       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       SCORE_MP      </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       SEC_MP      </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       SOUNDEX      </code></td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#split"><code dir="ltr" translate="no">        SPLIT       </code></a></td>
</tr>
<tr class="odd">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#starts_with"><code dir="ltr" translate="no">        STARTS_WITH       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       STRING_TO_INT      </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       STRPOS      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#strpos"><code dir="ltr" translate="no">        STRPOS       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       SUBSTR      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#substr"><code dir="ltr" translate="no">        SUBSTR       </code></a></td>
</tr>
<tr class="odd">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#to_base32"><code dir="ltr" translate="no">        TO_BASE32       </code></a></td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#to_base64"><code dir="ltr" translate="no">        TO_BASE64       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       TO_CHAR      </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       TO_DATE      </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       TO_NUMBER      </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       TO_TIMESTAMP      </code></td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#to_code_points"><code dir="ltr" translate="no">        TO_CODE_POINTS       </code></a></td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#to_hex"><code dir="ltr" translate="no">        TO_HEX       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       TRANSLATE      </code></td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#trim"><code dir="ltr" translate="no">        TRIM       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       UPPER      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#upper"><code dir="ltr" translate="no">        UPPER       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       UNICODE      </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       UNICODES      </code></td>
<td></td>
</tr>
</tbody>
</table>

### Math functions

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Netezza</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       ABS      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#abs"><code dir="ltr" translate="no">        ABS       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ACOS      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#acos"><code dir="ltr" translate="no">        ACOS       </code></a></td>
</tr>
<tr class="odd">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#acosh"><code dir="ltr" translate="no">        ACOSH       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ASIN      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#asin"><code dir="ltr" translate="no">        ASIN       </code></a></td>
</tr>
<tr class="odd">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#asinh"><code dir="ltr" translate="no">        ASINH       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ATAN      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#atan"><code dir="ltr" translate="no">        ATAN       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       ATAN2      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#atan2"><code dir="ltr" translate="no">        ATAN2       </code></a></td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#atanh"><code dir="ltr" translate="no">        ATANH       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       CEIL      </code><br />
<code dir="ltr" translate="no">       DCEIL      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#ceil"><code dir="ltr" translate="no">        CEIL       </code></a></td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#ceiling"><code dir="ltr" translate="no">        CEILING       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       COS      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#cos"><code dir="ltr" translate="no">        COS       </code></a></td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#cosh"><code dir="ltr" translate="no">        COSH       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       COT      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#cot"><code dir="ltr" translate="no">        COT       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       DEGREES      </code></td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#div"><code dir="ltr" translate="no">        DIV       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       EXP      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#exp"><code dir="ltr" translate="no">        EXP       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       FLOOR      </code><br />
<code dir="ltr" translate="no">       DFLOOR      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#floor"><code dir="ltr" translate="no">        FLOOR       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       GREATEST      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#greatest"><code dir="ltr" translate="no">        GREATEST       </code></a></td>
</tr>
<tr class="odd">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#ieee_divide"><code dir="ltr" translate="no">        IEEE_DIVIDE       </code></a></td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#is_inf"><code dir="ltr" translate="no">        IS_INF       </code></a></td>
</tr>
<tr class="odd">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#is_nan"><code dir="ltr" translate="no">        IS_NAN       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       LEAST      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#least"><code dir="ltr" translate="no">        LEAST       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       LN      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#ln"><code dir="ltr" translate="no">        LN       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       LOG      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#log"><code dir="ltr" translate="no">        LOG       </code></a></td>
</tr>
<tr class="odd">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#log10"><code dir="ltr" translate="no">        LOG10       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       MOD      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#mod"><code dir="ltr" translate="no">        MOD       </code></a></td>
</tr>
<tr class="odd">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/conditional_expressions#nullif"><code dir="ltr" translate="no">        NULLIF       </code></a> <code dir="ltr" translate="no">       (expr, 0)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       PI      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#acos"><code dir="ltr" translate="no">        ACOS       </code></a> <code dir="ltr" translate="no">       (-1)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       POW      </code><br />
<code dir="ltr" translate="no">       FPOW      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#power"><code dir="ltr" translate="no">        POWER       </code></a><br />
<a href="/bigquery/docs/reference/standard-sql/mathematical_functions#pow"><code dir="ltr" translate="no">        POW       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       RADIANS      </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       RANDOM      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#rand"><code dir="ltr" translate="no">        RAND       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ROUND      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#round"><code dir="ltr" translate="no">        ROUND       </code></a></td>
</tr>
<tr class="odd">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#safe_divide"><code dir="ltr" translate="no">        SAFE_DIVIDE       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       SETSEED      </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       SIGN      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#sign"><code dir="ltr" translate="no">        SIGN       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       SIN      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#sin"><code dir="ltr" translate="no">        SIN       </code></a></td>
</tr>
<tr class="odd">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#sinh"><code dir="ltr" translate="no">        SINH       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       SQRT      </code><br />
<code dir="ltr" translate="no">       NUMERIC_SQRT      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#sqrt"><code dir="ltr" translate="no">        SQRT       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       TAN      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#tan"><code dir="ltr" translate="no">        TAN       </code></a></td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#tanh"><code dir="ltr" translate="no">        TANH       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       TRUNC      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#trunc"><code dir="ltr" translate="no">        TRUNC       </code></a></td>
</tr>
<tr class="even">
<td></td>
<td><a href="/bigquery/docs/reference/standard-sql/conditional_expressions#ifnull"><code dir="ltr" translate="no">        IFNULL       </code></a> <code dir="ltr" translate="no">       (expr, 0)      </code></td>
</tr>
</tbody>
</table>

## DML syntax

This section compares Netezza and BigQuery DML syntax.

### `     INSERT    ` statement

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Netezza</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" translate="no"><code>INSERT INTO table VALUES (...);</code></pre></td>
<td><pre class="text" dir="ltr" data-is-upgraded="" translate="no"><code>INSERT INTO table (...) VALUES (...);</code></pre>
<br />
Netezza offers a <code dir="ltr" translate="no">       DEFAULT      </code> keyword and other constraints for columns. In BigQuery, omitting column names in the <code dir="ltr" translate="no">       INSERT      </code> statement is valid only if all columns are given.</td>
</tr>
<tr class="even">
<td><pre class="text" dir="ltr" data-is-upgraded="" translate="no"><code>INSERT INTO table (...) VALUES (...);
INSERT INTO table (...) VALUES (...);</code></pre></td>
<td><pre class="text" dir="ltr" data-is-upgraded="" translate="no"><code>INSERT INTO table VALUES (), ();</code></pre>
<p>BigQuery imposes <a href="/bigquery/quotas#data-manipulation-language-statements">DML quotas</a> , which restrict the number of DML statements you can execute daily. To make the best use of your quota, consider the following approaches:</p>
<ul>
<li>Combine multiple rows in a single <code dir="ltr" translate="no">         INSERT        </code> statement, instead of one row per <code dir="ltr" translate="no">         INSERT        </code> statement.</li>
</ul>
<ul>
<li>Combine multiple DML statements (including an <code dir="ltr" translate="no">         INSERT        </code> statement) using a <code dir="ltr" translate="no">         MERGE        </code> statement.</li>
</ul>
<ul>
<li>Use a <code dir="ltr" translate="no">         CREATE TABLE ... AS SELECT        </code> statement to create and populate new tables.</li>
</ul></td>
</tr>
</tbody>
</table>

DML scripts in BigQuery have slightly different consistency semantics than the equivalent statements in Netezza. Also note that BigQuery does not offer constraints apart from `  NOT NULL  ` .

For an overview of snapshot isolation and session and transaction handling, see [Consistency guarantees and transaction isolation](#consistency_guarantees_and_transaction_isolation) .

### `     UPDATE    ` statement

In Netezza, the `  WHERE  ` clause is optional, but in BigQuery it is necessary.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Netezza</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" translate="no"><code>UPDATE tbl
SET
tbl.col1=val1;</code></pre></td>
<td>Not supported without the <code dir="ltr" translate="no">       WHERE      </code> clause. Use a <code dir="ltr" translate="no">       WHERE true      </code> clause to update all rows.</td>
</tr>
<tr class="even">
<td><pre class="text" dir="ltr" data-is-upgraded="" translate="no"><code>UPDATE A
SET
  y = B.y,
  z = B.z + 1
FROM B
WHERE A.x = B.x
  AND A.y IS NULL;</code></pre></td>
<td><pre class="text" dir="ltr" data-is-upgraded="" translate="no"><code>UPDATE A
SET
  y = B.y,
  z = B.z + 1
FROM B
WHERE A.x = B.x
  AND A.y IS NULL;</code></pre></td>
</tr>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" translate="no"><code>UPDATE A alias
SET x = x + 1
WHERE f(x) IN (0, 1)</code></pre></td>
<td><pre class="text" dir="ltr" data-is-upgraded="" translate="no"><code>UPDATE A
SET x = x + 1
WHERE f(x) IN (0, 1);</code></pre></td>
</tr>
<tr class="even">
<td><pre class="text" dir="ltr" data-is-upgraded="" translate="no"><code>UPDATE A
SET z = B.z
FROM B
WHERE A.x = B.x
  AND A.y = B.y</code></pre></td>
<td><pre class="text" dir="ltr" data-is-upgraded="" translate="no"><code>UPDATE A
SET z = B.z
FROM B
WHERE A.x = B.x
  AND A.y = B.y;</code></pre></td>
</tr>
</tbody>
</table>

For examples, see [`  UPDATE  ` examples](/bigquery/docs/reference/standard-sql/dml-syntax#update_examples) .

Because of [DML quotas](/bigquery/quotas#data-manipulation-language-statements) , we recommend that you use larger `  MERGE  ` statements instead of multiple single `  UPDATE  ` and `  INSERT  ` statements. DML scripts in BigQuery have slightly different consistency semantics than equivalent statements in Netezza. For an overview of snapshot isolation and session and transaction handling, see [Consistency guarantees and transaction isolation](#consistency_guarantees_and_transaction_isolation) .

### `     DELETE    ` and `     TRUNCATE    ` statements

The `  DELETE  ` and `  TRUNCATE  ` statements are both ways to remove rows from a table without affecting the table schema or indexes. The `  TRUNCATE  ` statement has the same effect as the `  DELETE  ` statement, but is much faster than the `  DELETE  ` statement for large tables. The `  TRUNCATE  ` statement is supported in Netezza but not supported in BigQuery. However, you can use `  DELETE  ` statements in both Netezza and BigQuery.

In BigQuery, the `  DELETE  ` statement must have a `  WHERE  ` clause. In Netezza, the `  WHERE  ` clause is optional. If the `  WHERE  ` clause is not specified, all the rows in the Netezza table are deleted.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Netezza</strong></th>
<th><strong>BigQuery</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" translate="no"><code>BEGIN;
LOCK TABLE A IN EXCLUSIVE MODE;
DELETE FROM A;
INSERT INTO A SELECT * FROM B;
COMMIT;</code></pre></td>
<td>Replacing the contents of a table with query output is the equivalent of a transaction. You can do this with either a <a href="/bigquery/docs/reference/bq-cli-reference#bq_query"><code dir="ltr" translate="no">        query       </code></a> or a <a href="/bigquery/docs/managing-tables#copy-table">copy ( <code dir="ltr" translate="no">        cp       </code> )</a> operation.<br />
<br />

<pre class="text" dir="ltr" data-is-upgraded="" translate="no"><code>bq query \

--replace \

--destination_table \

tableA \

&#39;SELECT * \

FROM tableB \

WHERE ...&#39;</code></pre>
<pre class="text" dir="ltr" data-is-upgraded="" translate="no"><code>bq cp \

-f tableA tableB</code></pre></td>
<td>Replace the contents of a table with the results of a query.</td>
</tr>
<tr class="even">
<td><pre class="text" dir="ltr" data-is-upgraded="" translate="no"><code>DELETE FROM database.table</code></pre></td>
<td><pre class="text" dir="ltr" data-is-upgraded="" translate="no"><code>DELETE FROM table WHERE TRUE;</code></pre></td>
<td>In Netezza, when a delete statement is run, the rows are not deleted physically but only marked for deletion. Running the <code dir="ltr" translate="no">       GROOM TABLE      </code> or <code dir="ltr" translate="no">       nzreclaim      </code> commands later removes the rows marked for deletion and reclaims the corresponding disk space.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       GROOM TABLE      </code></td>
<td></td>
<td>Netezza uses the <code dir="ltr" translate="no">       GROOM TABLE      </code> command to reclaim disk space by removing rows marked for deletion.</td>
</tr>
</tbody>
</table>

### `     MERGE    ` statement

A `  MERGE  ` statement must match at most one source row for each target row. DML scripts in BigQuery have slightly different consistency semantics than the equivalent statements in Netezza. For an overview of snapshot isolation and session and transaction handling, see [Consistency guarantees and transaction isolation](#consistency_guarantees_and_transaction_isolation) . For examples, see [BigQuery `  MERGE  ` examples](/bigquery/docs/reference/standard-sql/dml-syntax#merge_examples) and Netezza `  MERGE  ` examples.

## DDL syntax

This section compares Netezza and BigQuery DDL syntax.

### `     CREATE TABLE    ` statement

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Netezza</strong></th>
<th><strong>BigQuery</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       TEMP      </code><br />
<code dir="ltr" translate="no">       TEMPORARY      </code></td>
<td>With BigQuery's DDL support, you can create a table from the results of a query and specify its expiration at creation time. For example, for three days:<br />
<br />
<code dir="ltr" translate="no">       CREATE TABLE      </code> <code dir="ltr" translate="no">       'my-project.public_dump.vtemp'      </code><br />
<code dir="ltr" translate="no">       OPTIONS      </code> (<br />
<code dir="ltr" translate="no">       expiration_timestamp=TIMESTAMP_ADD(CURRENT_TIMESTAMP(),      </code><br />
<code dir="ltr" translate="no">       INTERVAL 3 DAY))      </code></td>
<td>Create tables temporary to a session.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ZONE MAPS      </code></td>
<td>Not supported.</td>
<td>Quick search for <code dir="ltr" translate="no">       WHERE      </code> condition.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       DISTRIBUTE ON      </code></td>
<td><code dir="ltr" translate="no">       PARTITION BY      </code></td>
<td>Partitioning. This is not a direct translation. <code dir="ltr" translate="no">       DISTRIBUTE ON      </code> shares data between nodes, usually with a unique key for even distribution, while <code dir="ltr" translate="no">       PARTITION BY      </code> prunes data into segments.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ORGANIZE ON      </code></td>
<td><code dir="ltr" translate="no">       CLUSTER BY      </code></td>
<td>Both Netezza and BigQuery support up to four keys for clustering. Netezza clustered base tables (CBT) provide equal precedence to each of the clustering columns. BigQuery gives precedence to the first column on which the table is clustered, followed by the second column, and so on.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       ROW SECURITY      </code></td>
<td><code dir="ltr" translate="no">       Authorized View      </code></td>
<td>Row-level security.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       CONSTRAINT      </code></td>
<td>Not supported</td>
<td>Check constraints.</td>
</tr>
</tbody>
</table>

### `     DROP    ` statement

<table>
<thead>
<tr class="header">
<th><strong>Netezza</strong></th>
<th><strong>BigQuery</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       DROP TABLE      </code></td>
<td><code dir="ltr" translate="no">       DROP TABLE      </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       DROP DATABASE      </code></td>
<td><code dir="ltr" translate="no">       DROP DATABASE      </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       DROP VIEW      </code></td>
<td><code dir="ltr" translate="no">       DROP VIEW      </code></td>
<td></td>
</tr>
</tbody>
</table>

### Column options and attributes

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Netezza</strong></th>
<th><strong>BigQuery</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       NULL      </code><br />
<code dir="ltr" translate="no">       NOT NULL      </code></td>
<td><a href="/bigquery/docs/schemas#modes"><code dir="ltr" translate="no">        NULLABLE       </code></a><br />
<a href="/bigquery/docs/schemas#modes"><code dir="ltr" translate="no">        REQUIRED       </code></a></td>
<td>Specify if the column is allowed to contain <code dir="ltr" translate="no">       NULL      </code> values.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       REFERENCES      </code></td>
<td>Not supported</td>
<td>Specify column constraint.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       UNIQUE      </code></td>
<td>Not supported</td>
<td>Each value in the column must be unique.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       DEFAULT      </code></td>
<td>Not supported</td>
<td>Default value for all values in the column.</td>
</tr>
</tbody>
</table>

### Temporary tables

Netezza supports `  TEMPORARY  ` tables that exist during the duration of a session.

To build a temporary table in BigQuery, do the following:

1.  Create a dataset that has a short time to live (for example, 12 hours).

2.  Create the temporary table in the dataset, with a table name prefix of `  temp  ` . For example, to create a table that expires in one hour, do this:
    
    ``` text
    CREATE TABLE temp.name (col1, col2, ...)
    OPTIONS(expiration_timestamp = TIMESTAMP_ADD(CURRENT_TIMESTAMP(),
    INTERVAL 1 HOUR));
    ```

3.  Start reading and writing from the temporary table.

You can also [remove duplicates independently](/bigquery/streaming-data-into-bigquery#manually_removing_duplicates) in order to find errors in downstream systems.

Note that BigQuery does not support `  DEFAULT  ` and `  IDENTITY  ` (sequences) columns.

## Procedural SQL statements

Netezza uses the NZPLSQL scripting language to work with stored procedures. NZPLSQL is based on Postgres' PL/pgSQL language. This section describes how to convert procedural SQL statements used in stored procedures, functions, and triggers from Netezza to BigQuery.

### `     CREATE PROCEDURE    ` statement

Netezza and BigQuery both support creating stored procedures by using the [`  CREATE PROCEDURE  `](/bigquery/docs/reference/standard-sql/data-definition-language#create_procedure) statement. For more information, see [Work with SQL stored procedures](/bigquery/docs/procedures) .

### Variable declaration and assignment

<table>
<thead>
<tr class="header">
<th><strong>Netezza</strong></th>
<th><strong>BigQuery</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       DECLARE var datatype(len) [DEFAULT value];      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/procedural-language#declare"><code dir="ltr" translate="no">        DECLARE       </code></a></td>
<td>Declare variable.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       SET var = value;      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/procedural-language#set"><code dir="ltr" translate="no">        SET       </code></a></td>
<td>Assign value to variable.</td>
</tr>
</tbody>
</table>

### Exception handlers

Netezza supports exception handlers that can be triggered for certain error conditions. BigQuery does not support condition handlers.

<table>
<thead>
<tr class="header">
<th><strong>Netezza</strong></th>
<th><strong>BigQuery</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       EXCEPTION      </code></td>
<td>Not supported</td>
<td>Declare SQL exception handler for general errors.</td>
</tr>
</tbody>
</table>

### Dynamic SQL statements

Netezza supports dynamic SQL queries inside stored procedures. BigQuery does not support dynamic SQL statements.

<table>
<thead>
<tr class="header">
<th><strong>Netezza</strong></th>
<th><strong>BigQuery</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       EXECUTE IMMEDIATE      </code> <code dir="ltr" translate="no">       sql_str;      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/procedural-language#execute_immediate"><code dir="ltr" translate="no">        EXECUTE IMMEDIATE       </code></a> <code dir="ltr" translate="no">       sql_str;      </code></td>
<td>Execute dynamic SQL.</td>
</tr>
</tbody>
</table>

### Flow-of-control statements

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Netezza</strong></th>
<th><strong>BigQuery</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       IF THEN ELSE STATEMENT      </code><br />
<code dir="ltr" translate="no">       IF      </code> <em>condition</em><br />
<code dir="ltr" translate="no">       THEN ...      </code><br />
<code dir="ltr" translate="no">       ELSE ...      </code><br />
<code dir="ltr" translate="no">       END IF;      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/procedural-language#if"><code dir="ltr" translate="no">        IF       </code></a> <em>condition</em><br />
<code dir="ltr" translate="no">       THEN ...      </code><br />
<code dir="ltr" translate="no">       ELSE ...      </code><br />
<code dir="ltr" translate="no">       END IF;      </code></td>
<td>Execute conditionally.</td>
</tr>
<tr class="even">
<td>Iterative Control<br />
<code dir="ltr" translate="no">       FOR var AS SELECT ...      </code><br />
<code dir="ltr" translate="no">       DO      </code> <em>stmts</em> <code dir="ltr" translate="no">       END FOR;      </code><br />
<code dir="ltr" translate="no">       FOR var AS cur CURSOR      </code><br />
<code dir="ltr" translate="no">       FOR SELECT ...      </code><br />
<code dir="ltr" translate="no">       DO stmts END FOR;      </code></td>
<td>Not supported</td>
<td>Iterate over a collection of rows.</td>
</tr>
<tr class="odd">
<td>Iterative Control<br />
<code dir="ltr" translate="no">       LOOP stmts END LOOP;      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/procedural-language#loops"><code dir="ltr" translate="no">        LOOP       </code></a><br />
<code dir="ltr" translate="no">       sql_statement_list END LOOP;      </code></td>
<td>Loop block of statements.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       EXIT WHEN      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/procedural-language#break"><code dir="ltr" translate="no">        BREAK       </code></a></td>
<td>Exit a procedure.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       WHILE *condition* LOOP      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/procedural-language#while"><code dir="ltr" translate="no">        WHILE       </code></a> <em>condition</em><br />
<code dir="ltr" translate="no">       DO ...      </code><br />
<code dir="ltr" translate="no">       END WHILE      </code></td>
<td>Execute a loop of statements until a while condition fails.</td>
</tr>
</tbody>
</table>

### Other statements and procedural language elements

<table>
<thead>
<tr class="header">
<th><strong>Netezza</strong></th>
<th><strong>BigQuery</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       CALL      </code> <code dir="ltr" translate="no">       proc(param,...)      </code></td>
<td>Not supported</td>
<td>Execute a procedure.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       EXEC      </code> <code dir="ltr" translate="no">       proc(param,...)      </code></td>
<td>Not supported</td>
<td>Execute a procedure.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       EXECUTE      </code> <code dir="ltr" translate="no">       proc(param,...)      </code></td>
<td>Not supported</td>
<td>Execute a procedure.</td>
</tr>
</tbody>
</table>

## Multi-statement and multi-line SQL statements

Both Netezza and BigQuery support transactions (sessions) and therefore support statements separated by semicolons that are consistently executed together. For more information, see [Multi-statement transactions](/bigquery/docs/transactions) .

## Other SQL statements

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Netezza</strong></th>
<th><strong>BigQuery</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       GENERATE STATISTICS      </code></td>
<td></td>
<td>Generate statistics for all the tables in the current database.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       GENERATE STATISTICS ON table_name      </code></td>
<td></td>
<td>Generate statistics for a specific table.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       GENERATE STATISTICS ON table_name(col1,col4)      </code></td>
<td>Either use <a href="/bigquery/docs/reference/standard-sql/aggregate_functions">statistical functions</a> like <code dir="ltr" translate="no">       MIN, MAX, AVG,      </code> etc., use the UI, or use the Cloud Data Loss Prevention API.</td>
<td>Generate statistics for specific columns in a table.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       GENERATE STATISTICS ON table_name      </code></td>
<td><code dir="ltr" translate="no">       APPROX_COUNT_DISTINCT(col)      </code></td>
<td>Show the number of unique values for columns.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       INSERT INTO table_name      </code></td>
<td><code dir="ltr" translate="no">       INSERT INTO table_name      </code></td>
<td>Insert a row.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       LOCK TABLE      </code> <code dir="ltr" translate="no">       table_name FOR      </code> <code dir="ltr" translate="no">       EXCLUSIVE;      </code></td>
<td>Not supported</td>
<td>Lock row.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       SET SESSION      </code> <code dir="ltr" translate="no">       CHARACTERISTICS AS      </code> <code dir="ltr" translate="no">       TRANSACTION ISOLATION LEVEL      </code> ...</td>
<td>BigQuery always uses Snapshot Isolation. For details, see <a href="#consistency_guarantees_and_transaction_isolation">Consistency guarantees and transaction isolation</a> .</td>
<td>Define the transaction isolation level.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       BEGIN TRANSACTION      </code><br />
<code dir="ltr" translate="no">       END TRANSACTION      </code><br />
<code dir="ltr" translate="no">       COMMIT      </code><br />
</td>
<td>BigQuery always uses Snapshot Isolation. For details, see <a href="#consistency_guarantees_and_transaction_isolation">Consistency guarantees and transaction isolation</a> .</td>
<td>Define the transaction boundary for multi-statement requests.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       EXPLAIN      </code> ...</td>
<td>Not supported. Similar features in the <a href="/bigquery/query-plan-explanation">query plan and timeline</a></td>
<td>Show query plan for a <code dir="ltr" translate="no">       SELECT      </code> statement.</td>
</tr>
<tr class="even">
<td>User Views metadata<br />
System Views metadata</td>
<td><code dir="ltr" translate="no">       SELECT      </code><br />
<code dir="ltr" translate="no">       * EXCEPT(is_typed)      </code><br />
<code dir="ltr" translate="no">       FROM      </code><br />
<code dir="ltr" translate="no">       mydataset.INFORMATION_SCHEMA.TABLES;      </code><br />
<br />
BigQuery <a href="/bigquery/docs/information-schema-intro">Information Schema</a></td>
<td>Query objects in the database</td>
</tr>
</tbody>
</table>

## Consistency guarantees and transaction isolation

Both Netezza and BigQuery are atomic, that is, [ACID](https://en.wikipedia.org/wiki/ACID) compliant on a per-mutation level across many rows. For example, a `  MERGE  ` operation is completely atomic, even with multiple inserted values.

### Transactions

Netezza syntactically accepts all four modes of ANSI SQL transaction isolation. However, regardless of what mode is specified, only the `  SERIALIZABLE  ` mode is used, which provides the highest possible level of consistency. This mode also avoids dirty, non repeatable, and phantom reads between concurrent transactions. Netezza does not use conventional locking to enforce consistency. Instead, it uses serialization dependency checking, a form of optimistic concurrency control to automatically roll back the latest transaction when two transactions attempt to modify the same data.

BigQuery also [supports transactions](/bigquery/docs/transactions) . BigQuery helps ensure optimistic concurrency control (first to commit has priority) with snapshot isolation, in which a query reads the last committed data before the query starts. This approach ensures the same level of consistency on a per-row, per-mutation basis and across rows within the same DML statement, yet avoids deadlocks. In the case of multiple DML updates against the same table, BigQuery switches to [pessimistic concurrency control](/bigquery/docs/data-manipulation-language#dml-limitations) . Load jobs can run completely independently and append to tables.

### Rollback

Netezza supports the `  ROLLBACK TRANSACTION  ` statement to abort the current transaction and rollback all the changes made in the transaction.

In BigQuery, you can use the [`  ROLLBACK TRANSACTION  ` statement](/bigquery/docs/reference/standard-sql/procedural-language#rollback_transaction) .

## Database limits

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Limit</strong></th>
<th><strong>Netezza</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Tables per database</td>
<td>32,000</td>
<td>Unrestricted</td>
</tr>
<tr class="even">
<td>Columns per table</td>
<td>1600</td>
<td>10000</td>
</tr>
<tr class="odd">
<td>Maximum row size</td>
<td>64 KB</td>
<td>100 MB</td>
</tr>
<tr class="even">
<td>Column and table name length</td>
<td>128 bytes</td>
<td>16,384 Unicode characters</td>
</tr>
<tr class="odd">
<td>Rows per table</td>
<td>Unlimited</td>
<td>Unlimited</td>
</tr>
<tr class="even">
<td>Maximum SQL request length</td>
<td></td>
<td>1 MB (maximum unresolved standard SQL query length).<br />
<br />
12 MB (maximum resolved legacy and standard SQL query length).<br />
<br />
Streaming:<br />
10 MB (HTTP request size limit)<br />
10,000 (maximum rows per request)</td>
</tr>
<tr class="odd">
<td>Maximum request and response size</td>
<td></td>
<td>10 MB (request) and 10 GB (response) or virtually unlimited if using pagination or the Cloud Storage API.</td>
</tr>
<tr class="even">
<td>Maximum number of concurrent sessions</td>
<td>63 concurrent read-write transactions. 2000 concurrent connections to the server.</td>
<td>100 concurrent queries (can be raised with <a href="/bigquery/docs/slots">slot reservation</a> ), 300 concurrent API requests per user.</td>
</tr>
</tbody>
</table>

## What's next

  - Get step-by-step instructions to [Migrate from IBM Netezza to BigQuery](/bigquery/docs/migration/netezza) .
