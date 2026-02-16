# Amazon Redshift SQL translation guide

This document details the similarities and differences in SQL syntax between Amazon Redshift and BigQuery to help you plan your migration. Use [batch SQL translation](/bigquery/docs/batch-sql-translator) to migrate your SQL scripts in bulk, or [interactive SQL translation](/bigquery/docs/interactive-sql-translator) to translate ad hoc queries.

The intended audience for this guide is enterprise architects, database administrators, application developers, and IT security specialists. It assumes you are familiar with Amazon Redshift.

**Note:** In some cases, there is no direct mapping between a SQL element in Amazon Redshift and BigQuery. However, in most cases, you can achieve the same functionality in BigQuery that you can in Amazon Redshift using alternative means, as shown in the examples in this document.

## Data types

This section shows equivalents between data types in Amazon Redshift and in BigQuery.

**Amazon Redshift**

**BigQuery**

**Notes**

**Data type**

**Alias**

**Data type**

`  SMALLINT  `

`  INT2  `

`  INT64  `

Amazon Redshift's `  SMALLINT  ` is 2 bytes, whereas BigQuery's `  INT64  ` is 8 bytes.

`  INTEGER  `

`  INT, INT4  `

`  INT64  `

Amazon Redshift's `  INTEGER  ` is 4 bytes, whereas BigQuery's `  INT64  ` is 8 bytes.

`  BIGINT  `

`  INT8  `

`  INT64  `

Both Amazon Redshift's `  BIGINT  ` and BigQuery's `  INT64  ` are 8 bytes.

`  DECIMAL  `

`  NUMERIC  `

`  NUMERIC  `

`  REAL  `

`  FLOAT4  `

`  FLOAT64  `

Amazon Redshift's `  REAL  ` is 4 bytes, whereas BigQuery's `  FLOAT64  ` is 8 bytes.

`  DOUBLE PRECISION  `

`  FLOAT8, FLOAT  `

`  FLOAT64  `

`  BOOLEAN  `

`  BOOL  `

`  BOOL  `

Amazon Redshift's `  BOOLEAN  ` can use `  TRUE  ` , `  t  ` , `  true  ` , `  y  ` , `  yes  ` , and `  1  ` as valid literal values for true. BigQuery's `  BOOL  ` data type uses case-insensitive `  TRUE  ` .

`  CHAR  `

`  CHARACTER, NCHAR, BPCHAR  `

`  STRING  `

`  VARCHAR  `

`  CHARACTER VARYING, NVARCHAR, TEXT  `

`  STRING  `

`  DATE  `

`  DATE  `

`  TIMESTAMP  `

`  TIMESTAMP WITHOUT TIME ZONE  `

`  DATETIME  `

`  TIMESTAMPTZ  `

`  TIMESTAMP WITH TIME ZONE  `

`  TIMESTAMP  `

Note: In BigQuery, [time zones](/bigquery/docs/reference/standard-sql/data-types#time_zones) are used when parsing timestamps or formatting timestamps for display. A string-formatted timestamp might include a time zone, but when BigQuery parses the string, it stores the timestamp in the equivalent UTC time. When a time zone is not explicitly specified, the default time zone, UTC, is used. [Time zone names](https://en.wikipedia.org/wiki/List_of_time_zone_abbreviations) or [offset from UTC](/bigquery/docs/reference/standard-sql/timestamp_functions#timezone_definitions) using (-|+)HH:MM are supported, but time zone abbreviations such as PDT are not supported.

`  GEOMETRY  `

`  GEOGRAPHY  `

Support for querying geospatial data.

BigQuery also has the following data types that do not have a direct Amazon Redshift analog:

  - [`  ARRAY  `](/bigquery/docs/reference/standard-sql/data-types#array_type)
  - [`  BYTES  `](/bigquery/docs/reference/standard-sql/data-types#bytes_type)
  - [`  TIME  `](/bigquery/docs/reference/standard-sql/data-types#time_type)
  - [`  STRUCT  `](/bigquery/docs/reference/standard-sql/data-types#struct_type)

### Implicit conversion types

When migrating to BigQuery, you need to convert most of your [Amazon Redshift implicit conversions](https://docs.aws.amazon.com/redshift/latest/dg/c_Supported_data_types.html#r_Type_conversion) to BigQuery's explicit conversions except for the following data types, which BigQuery implicitly converts.

BigQuery performs implicit conversions for the following data types:

<table>
<thead>
<tr class="header">
<th><strong>From BigQuery type</strong></th>
<th><strong>To BigQuery type</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        INT64       </code></p></td>
<td><p><code dir="ltr" translate="no">        FLOAT64       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        INT64       </code></p></td>
<td><p><code dir="ltr" translate="no">        NUMERIC       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        NUMERIC       </code></p></td>
<td><p><code dir="ltr" translate="no">        FLOAT64       </code></p></td>
</tr>
</tbody>
</table>

BigQuery also performs implicit conversions for the following literals:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>From BigQuery type</strong></th>
<th><strong>To BigQuery type</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       STRING      </code> literal<br />
(e.g. "2008-12-25")</td>
<td><p><code dir="ltr" translate="no">        DATE       </code></p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       STRING      </code> literal<br />
(e.g. "2008-12-25 15:30:00")</td>
<td><p><code dir="ltr" translate="no">        TIMESTAMP       </code></p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       STRING      </code> literal<br />
(e.g. "2008-12-25T07:30:00")</td>
<td><p><code dir="ltr" translate="no">        DATETIME       </code></p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       STRING      </code> literal<br />
(e.g. "15:30:00")</td>
<td><p><code dir="ltr" translate="no">        TIME       </code></p></td>
</tr>
</tbody>
</table>

### Explicit conversion types

You can convert Amazon Redshift data types that BigQuery doesn't implicitly convert using BigQuery's [`  CAST(expression AS type)  `](/bigquery/docs/reference/standard-sql/conversion_functions#cast) function or any of the [`  DATE  `](/bigquery/docs/reference/standard-sql/date_functions) and [`  TIMESTAMP  `](/bigquery/docs/reference/standard-sql/timestamp_functions) conversion functions.

When migrating your queries, change any occurrences of the Amazon Redshift [`  CONVERT(type, expression)  `](https://docs.aws.amazon.com/redshift/latest/dg/r_CAST_function.html#convert-function) function (or the :: syntax) to BigQuery's [`  CAST(expression AS type)  `](/bigquery/docs/reference/standard-sql/conversion_functions#cast) function, as shown in the table in the [Data type formatting functions](#data_type_formatting_functions) section.

## Query syntax

This section addresses differences in query syntax between Amazon Redshift and BigQuery.

### `     SELECT    ` statement

Most Amazon Redshift [`  SELECT  `](https://docs.aws.amazon.com/redshift/latest/dg/r_SELECT_synopsis.html) statements are compatible with BigQuery. The following table contains a list of minor differences.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Amazon Redshift</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        SELECT TOP number expression                FROM table       </code></p></td>
<td><p><code dir="ltr" translate="no">        SELECT expression                FROM table                ORDER BY expression DESC                LIMIT number       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        SELECT                x/total AS probability,                ROUND(100 * probability, 1) AS pct                FROM raw_data       </code><br />
<br />
Note: Redshift supports creating and referencing an alias in the same <code dir="ltr" translate="no">        SELECT       </code> statement.</p></td>
<td><p><code dir="ltr" translate="no">        SELECT                x/total AS probability,                ROUND(100 * (x/total), 1) AS pct                FROM raw_data       </code></p></td>
</tr>
</tbody>
</table>

BigQuery also supports the following expressions in `  SELECT  ` statements, which do not have a Amazon Redshift equivalent:

  - [`  EXCEPT  `](/bigquery/docs/reference/standard-sql/query-syntax#select_except)
  - [`  REPLACE  `](/bigquery/docs/reference/standard-sql/query-syntax#select_replace)

### `     FROM    ` clause

A [`  FROM  `](https://docs.aws.amazon.com/redshift/latest/dg/r_FROM_clause30.html) clause in a query lists the table references that data is selected from. In Amazon Redshift, possible table references include tables, views, and subqueries. All of these table references are supported in BigQuery.

BigQuery tables can be referenced in the `  FROM  ` clause using the following:

  - `  [project_id].[dataset_id].[table_name]  `
  - `  [dataset_id].[table_name]  `
  - `  [table_name]  `

BigQuery also supports additional table references:

  - Historical versions of the table definition and rows using [`  FOR SYSTEM_TIME AS OF  `](/bigquery/docs/reference/standard-sql/query-syntax#for_system_time_as_of) .
  - [Field paths](/bigquery/docs/reference/standard-sql/query-syntax#field_path) , or any path that resolves to a field within a data type (such as a `  STRUCT  ` ).
  - [Flattened arrays](/bigquery/docs/arrays#querying_nested_arrays) .

### `     JOIN    ` types

Both Amazon Redshift and BigQuery support the following types of join:

  - `  [INNER] JOIN  `
  - `  LEFT [OUTER] JOIN  `
  - `  RIGHT [OUTER] JOIN  `
  - `  FULL [OUTER] JOIN  `
  - `  CROSS JOIN  ` and the equivalent [implicit comma cross join](/bigquery/docs/reference/standard-sql/query-syntax#cross_join) .

The following table contains a list of minor differences.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Amazon Redshift</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        SELECT col                FROM table1                NATURAL INNER JOIN                table2       </code></p></td>
<td><p><code dir="ltr" translate="no">        SELECT col1                FROM table1                INNER JOIN                table2                USING (col1, col2 [, ...])       </code></p>
<br />
Note: In BigQuery, <code dir="ltr" translate="no">       JOIN      </code> clauses require a <code dir="ltr" translate="no">       JOIN      </code> condition unless the clause is a <code dir="ltr" translate="no">       CROSS JOIN      </code> or one of the joined tables is a field within a data type or an array.</td>
</tr>
</tbody>
</table>

### `     WITH    ` clause

A BigQuery [`  WITH  `](/bigquery/docs/reference/standard-sql/query-syntax#with_clause) clause contains one or more named subqueries that execute when a subsequent `  SELECT  ` statement references them. Amazon Redshift [`  WITH  `](https://docs.aws.amazon.com/redshift/latest/dg/r_WITH_clause.html) clauses behave the same as BigQuery's with the exception that you can evaluate the clause once and reuse its results.

### Set operators

There are some minor differences between [Amazon Redshift set operators](https://docs.aws.amazon.com/redshift/latest/dg/r_UNION.html#r_UNION-order-of-evaluation-for-set-operators) and [BigQuery set](/bigquery/docs/reference/standard-sql/query-syntax#set_operators) [operators](/bigquery/docs/reference/standard-sql/query-syntax#set_operators) . However, all set operations that are feasible in Amazon Redshift are replicable in BigQuery.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Amazon Redshift</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        SELECT * FROM table1                UNION                SELECT * FROM table2       </code></p></td>
<td><p><code dir="ltr" translate="no">        SELECT * FROM table1                UNION DISTINCT                SELECT * FROM table2       </code></p>
<p>Note: Both BigQuery and Amazon Redshift support the <code dir="ltr" translate="no">        UNION ALL       </code> operator.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        SELECT * FROM table1                INTERSECT                SELECT * FROM table2       </code></p></td>
<td><p><code dir="ltr" translate="no">        SELECT * FROM table1                INTERSECT DISTINCT                SELECT * FROM table2       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        SELECT * FROM table1                EXCEPT                SELECT * FROM table2       </code></p></td>
<td><p><code dir="ltr" translate="no">        SELECT * FROM table1                EXCEPT DISTINCT                SELECT * FROM table2       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        SELECT * FROM table1                MINUS                SELECT * FROM table2       </code></p></td>
<td><p><code dir="ltr" translate="no">        SELECT * FROM table1                EXCEPT DISTINCT                SELECT * FROM table2       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        SELECT * FROM table1                UNION                SELECT * FROM table2                EXCEPT                SELECT * FROM table3       </code></p></td>
<td><p><code dir="ltr" translate="no">        SELECT * FROM table1                UNION ALL                (                SELECT * FROM table2                EXCEPT                SELECT * FROM table3                )       </code></p>
<br />
Note: BigQuery requires parentheses to separate different set operations. If the same set operator is repeated, parentheses are not necessary.</td>
</tr>
</tbody>
</table>

### `     ORDER BY    ` clause

There are some minor differences between Amazon Redshift [`  ORDER BY  `](https://docs.amazonaws.cn/en_us/redshift/latest/dg/r_ORDER_BY_clause.html) clauses and BigQuery [`  ORDER BY  `](/bigquery/docs/reference/standard-sql/query-syntax#order_by_clause) clauses.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Amazon Redshift</th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>In Amazon Redshift, <code dir="ltr" translate="no">       NULL      </code> s are ranked last by default (ascending order).</td>
<td>In BigQuery, <code dir="ltr" translate="no">       NULL      </code> s are ranked first by default (ascending order).</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        SELECT *                FROM table                ORDER BY expression                LIMIT ALL       </code></p></td>
<td><p><code dir="ltr" translate="no">        SELECT *                FROM table                ORDER BY expression       </code></p>
<br />
<br />
Note: BigQuery does not use the <code dir="ltr" translate="no">       LIMIT ALL      </code> syntax, but <code dir="ltr" translate="no">       ORDER BY      </code> sorts all rows by default, resulting in the same behavior as Amazon Redshift's <code dir="ltr" translate="no">       LIMIT ALL      </code> clause. We highly recommend including a <code dir="ltr" translate="no">       LIMIT      </code> clause with every <code dir="ltr" translate="no">       ORDER BY      </code> clause. Ordering all result rows unnecessarily degrades query execution performance.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        SELECT *                FROM table                ORDER BY expression                OFFSET 10       </code></p></td>
<td><p><code dir="ltr" translate="no">        SELECT *                FROM table                ORDER BY expression                LIMIT                 count                OFFSET 10       </code></p>
<br />
<br />
Note: In BigQuery, <code dir="ltr" translate="no">       OFFSET      </code> must be used together with a <code dir="ltr" translate="no">       LIMIT      </code> <em>count</em> . Make sure to set the <em>count</em> <code dir="ltr" translate="no">       INT64      </code> value to the minimum necessary ordered rows. Ordering all result rows<br />
unnecessarily degrades query execution performance.</td>
</tr>
</tbody>
</table>

### Conditions

The following table shows [Amazon Redshift conditions](https://docs.aws.amazon.com/redshift/latest/dg/r_conditions.html) , or predicates, that are specific to Amazon Redshift and must be converted to their BigQuery equivalent.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Amazon Redshift</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        a                 = ANY                (subquery)       </code></p>
<p><code dir="ltr" translate="no">        a                 = SOME                (subquery)       </code></p></td>
<td><p><code dir="ltr" translate="no">        a                 IN                subquery       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        a                 &lt;&gt; ALL                (subquery)       </code></p>
<p><code dir="ltr" translate="no">        a != ALL (subquery)       </code></p></td>
<td><p><code dir="ltr" translate="no">        a                 NOT IN                subquery       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        a                 IS UNKNOWN        </code></p>
<p><code dir="ltr" translate="no">        expression                 ILIKE                pattern       </code></p></td>
<td><p><code dir="ltr" translate="no">        a                 IS NULL        </code></p>
<p><code dir="ltr" translate="no">          LOWER                (expression)                 LIKE                LOWER(pattern)       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        expression                 LIKE                pattern ESCAPE 'escape_char'       </code></p></td>
<td><p><code dir="ltr" translate="no">        expression                 LIKE                pattern       </code></p>
<br />
Note: BigQuery does not support custom escape characters. You must use two backslashes \\ as escape characters for BigQuery.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        expression [NOT]                 SIMILAR TO                pattern       </code></p></td>
<td><p><code dir="ltr" translate="no">        IF(                LENGTH(                REGEXP_REPLACE(                expression,                pattern,                ''                ) = 0,                True,                False                )       </code></p>
<br />
Note: If <code dir="ltr" translate="no">       NOT      </code> is specified, wrap the above <code dir="ltr" translate="no">       IF      </code> expression in a <code dir="ltr" translate="no">       NOT      </code> expression as shown below:<br />
<br />

<p><code dir="ltr" translate="no">        NOT(                IF(                LENGTH(...                )       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        expression                 [!] ~                pattern       </code></p></td>
<td><p><code dir="ltr" translate="no">          [NOT]                  REGEXP_CONTAINS                (                expression,                regex                )       </code></p></td>
</tr>
</tbody>
</table>

## Functions

The following sections list Amazon Redshift functions and their BigQuery equivalents.

### Aggregate functions

The following table shows mappings between common Amazon Redshift aggregate, aggregate analytic, and approximate aggregate functions with their BigQuery equivalents.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Amazon Redshift</th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         APPROXIMATE COUNT              (DISTINCT expression)      </code></td>
<td><code dir="ltr" translate="no">         APPROX_COUNT_DISTINCT              (expression)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         APPROXIMATE PERCENTILE_DISC              (              percentile              ) WITHIN GROUP (ORDER BY expression)      </code></td>
<td><code dir="ltr" translate="no">         APPROX_QUANTILES              (expression, 100)              [OFFSET(CAST(TRUNC(percentile * 100) as INT64))]      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         AVG              ([DISTINCT] expression)      </code></td>
<td><code dir="ltr" translate="no">         AVG              ([DISTINCT] expression)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         COUNT              (expression)      </code></td>
<td><code dir="ltr" translate="no">         COUNT              (expression)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         LISTAGG              (              [DISTINCT] aggregate_expression              [, delimiter] )              [WITHIN GROUP (ORDER BY order_list)]      </code></td>
<td><code dir="ltr" translate="no">         STRING_AGG              (              [DISTINCT] aggregate_expression              [, delimiter]              [ORDER BY order_list] )      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         MAX              (expression)      </code></td>
<td><code dir="ltr" translate="no">         MAX              (expression)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         MEDIAN              (median_expression)      </code></td>
<td><code dir="ltr" translate="no">         PERCENTILE_CONT              ( median_expression, 0.5 ) OVER()      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         MIN              (expression)      </code></td>
<td><code dir="ltr" translate="no">         MIN              (expression)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         PERCENTILE_CONT              (              percentile              ) WITHIN GROUP (ORDER BY expression)      </code></td>
<td><code dir="ltr" translate="no">         PERCENTILE_CONT              (              median_expression,              percentile              ) OVER()      </code><br />
<br />
Note: Does not cover aggregation use cases.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         STDDEV              ([DISTINCT] expression)      </code></td>
<td><code dir="ltr" translate="no">         STDDEV              ([DISTINCT] expression)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         STDDEV_SAMP              ([DISTINCT] expression)      </code></td>
<td><code dir="ltr" translate="no">         STDDEV_SAMP              ([DISTINCT] expression)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         STDDEV_POP              ([DISTINCT] expression)      </code></td>
<td><code dir="ltr" translate="no">         STDDEV_POP              ([DISTINCT] expression)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         SUM              ([DISTINCT] expression)      </code></td>
<td><code dir="ltr" translate="no">         SUM              ([DISTINCT] expression)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         VARIANCE              ([DISTINCT] expression)      </code></td>
<td><code dir="ltr" translate="no">         VARIANCE              ([DISTINCT] expression)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         VAR_SAMP              ([DISTINCT] expression)      </code></td>
<td><code dir="ltr" translate="no">         VAR_SAMP              ([DISTINCT] expression)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         VAR_POP              ([DISTINCT] expression)      </code></td>
<td><code dir="ltr" translate="no">         VAR_POP              ([DISTINCT] expression)      </code></td>
</tr>
</tbody>
</table>

BigQuery also offers the following [aggregate](/bigquery/docs/reference/standard-sql/aggregate_functions) , [aggregate analytic](/bigquery/docs/reference/standard-sql/aggregate_analytic_functions) , and [approximate aggregate](/bigquery/docs/reference/standard-sql/approximate_aggregate_functions) functions, which do not have a direct analogue in Amazon Redshift:

  - [`  ANY_VALUE  `](/bigquery/docs/reference/standard-sql/aggregate_functions#any_value)
  - [`  APPROX_TOP_COUNT  `](/bigquery/docs/reference/standard-sql/approximate_aggregate_functions#approx_top_count)
  - [`  APPROX_TOP_SUM  `](/bigquery/docs/reference/standard-sql/approximate_aggregate_functions#approx_top_sum)
  - [`  ARRAY_AGG  `](/bigquery/docs/reference/standard-sql/aggregate_functions#array_agg)
  - [`  ARRAY_CONCAT_AGG  `](/bigquery/docs/reference/standard-sql/aggregate_functions#array_concat_agg)
  - [`  COUNTIF  `](/bigquery/docs/reference/standard-sql/aggregate_functions#countif)
  - [`  CORR  `](/bigquery/docs/reference/standard-sql/statistical_aggregate_functions#corr)
  - [`  COVAR_POP  `](/bigquery/docs/reference/standard-sql/statistical_aggregate_functions#covar_pop)
  - [`  COVAR_SAMP  `](/bigquery/docs/reference/standard-sql/statistical_aggregate_functions#covar_samp)

### Bitwise aggregate functions

The following table shows mappings between common Amazon Redshift bitwise aggregate functions with their BigQuery equivalents.

<table>
<thead>
<tr class="header">
<th><strong>Amazon Redshift</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         BIT_AND              (expression)      </code></td>
<td><code dir="ltr" translate="no">         BIT_AND              (expression)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         BIT_OR              (expression)      </code></td>
<td><code dir="ltr" translate="no">         BIT_OR              (expression)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         BOOL_AND              &gt;(expression)      </code></td>
<td><code dir="ltr" translate="no">         LOGICAL_AND              (expression)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         BOOL_OR              (expression)      </code></td>
<td><code dir="ltr" translate="no">         LOGICAL_OR              (expression)      </code></td>
</tr>
</tbody>
</table>

BigQuery also offers the following [bit-wise aggregate](/bigquery/docs/reference/standard-sql/bit_functions) function, which does not have a direct analogue in Amazon Redshift:

  - [`  BIT_XOR  `](/bigquery/docs/reference/standard-sql/aggregate_functions#bit_xor)

### Window functions

The following table shows mappings between common Amazon Redshift window functions with their BigQuery equivalents. Windowing functions in BigQuery include [analytic aggregate functions](/bigquery/docs/reference/standard-sql/aggregate_analytic_functions) , [aggregate functions](/bigquery/docs/reference/standard-sql/aggregate_functions) , [navigation functions](/bigquery/docs/reference/standard-sql/navigation_functions) , and [numbering functions](/bigquery/docs/reference/standard-sql/numbering_functions) .

  

<table>
<thead>
<tr class="header">
<th><strong>Amazon Redshift</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         AVG              (expression) OVER              (              [PARTITION BY expr_list]              [ORDER BY order_list frame_clause]              )      </code></td>
<td><code dir="ltr" translate="no">         AVG              (expression) OVER              (              [PARTITION BY expr_list]              [ORDER BY order_list]              [frame_clause]              )      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         COUNT              (expression) OVER              (              [PARTITION BY expr_list]              [ORDER BY order_list              frame_clause]              )      </code></td>
<td><code dir="ltr" translate="no">         COUNT              (expression) OVER              (              [PARTITION BY expr_list]              [ORDER BY order_list]              [frame_clause]              )      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         CUME_DIST              () OVER              (              [PARTITION BY partition_expression]              [ORDER BY order_list]              )      </code></td>
<td><code dir="ltr" translate="no">         CUME_DIST              () OVER              (              [PARTITION BY partition_expression]              ORDER BY order_list              )      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         DENSE_RANK              () OVER              (              [PARTITION BY expr_list]              [ORDER BY order_list]              )      </code></td>
<td><code dir="ltr" translate="no">         DENSE_RANK              () OVER              (              [PARTITION BY expr_list]              ORDER BY order_list              )      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         FIRST_VALUE              (expression) OVER              (              [PARTITION BY expr_list]              [ORDER BY order_list              frame_clause]              )      </code></td>
<td><code dir="ltr" translate="no">         FIRST_VALUE              (expression) OVER              (              [PARTITION BY expr_list]              [ORDER BY order_list]              [frame_clause]              )      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         LAST_VALUE              (expression) OVER              (              [PARTITION BY expr_list]              [ORDER BY order_list              frame_clause]              )      </code></td>
<td><code dir="ltr" translate="no">         LAST_VALUE              (expression) OVER              (              [PARTITION BY expr_list]              [ORDER BY order_list              frame_clause]              )      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         LAG              (value_expr [, offset]) OVER              (              [PARTITION BY window_partition]              ORDER BY window_ordering              )      </code></td>
<td><code dir="ltr" translate="no">         LAG              (value_expr [, offset]) OVER              (              [PARTITION BY window_partition]              ORDER BY window_ordering              )      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         LEAD              (value_expr [, offset]) OVER              (              [PARTITION BY window_partition]              ORDER BY window_ordering              )      </code></td>
<td><code dir="ltr" translate="no">         LEAD              (value_expr [, offset]) OVER              (              [PARTITION BY window_partition]              ORDER BY window_ordering              )      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         LISTAGG              (              [DISTINCT] expression              [, delimiter]              )              [WITHIN GROUP              (ORDER BY order_list)]              OVER (              [PARTITION BY partition_expression] )      </code></td>
<td><code dir="ltr" translate="no">         STRING_AGG              (              [DISTINCT] aggregate_expression              [, delimiter]  )              OVER (              [PARTITION BY partition_list]              [ORDER BY order_list] )      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         MAX              (expression) OVER              (              [PARTITION BY expr_list]              [ORDER BY order_list              frame_clause]              )      </code></td>
<td><code dir="ltr" translate="no">         MAX              (expression) OVER              (              [PARTITION BY expr_list]              [ORDER BY order_list]              [frame_clause]              )      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         MEDIAN              (median_expression) OVER              (              [PARTITION BY partition_expression] )      </code></td>
<td><code dir="ltr" translate="no">         PERCENTILE_CONT              (              median_expression,              0.5              )              OVER ( [PARTITION BY partition_expression] )      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         MIN              (expression) OVER              (              [PARTITION BY expr_list]              [ORDER BY order_list              frame_clause]              )      </code></td>
<td><code dir="ltr" translate="no">         MIN              (expression) OVER              (              [PARTITION BY expr_list]              [ORDER BY order_list]              [frame_clause]              )      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         NTH_VALUE              (expression, offset) OVER ( [PARTITION BY window_partition] [ORDER BY window_ordering frame_clause] )      </code></td>
<td><code dir="ltr" translate="no">         NTH_VALUE              (expression, offset)  OVER              (              [PARTITION BY window_partition]              ORDER BY window_ordering              [frame_clause]              )      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         NTILE              (expr) OVER              (              [PARTITION BY expression_list]              [ORDER BY order_list]              )      </code></td>
<td><code dir="ltr" translate="no">         NTILE              (expr) OVER              (              [PARTITION BY expression_list]              ORDER BY order_list              )      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         PERCENT_RANK              () OVER              (              [PARTITION BY partition_expression]              [ORDER BY order_list]              )      </code></td>
<td><code dir="ltr" translate="no">         PERCENT_RANK              () OVER              (              [PARTITION BY partition_expression]              ORDER BY order_list              )      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         PERCENTILE_CONT              (percentile)              WITHIN GROUP (ORDER BY expr) OVER              (              [PARTITION BY expr_list] )      </code></td>
<td><code dir="ltr" translate="no">         PERCENTILE_CONT              (expr, percentile) OVER              (              [PARTITION BY expr_list] )      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         PERCENTILE_DISC              (percentile)  WITHIN GROUP (ORDER BY expr) OVER              (              [PARTITION BY expr_list]              )      </code></td>
<td><code dir="ltr" translate="no">         PERCENTILE_DISC              (expr, percentile) OVER              (              [PARTITION BY expr_list] )      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         RANK              () OVER              (              [PARTITION BY expr_list]              [ORDER BY order_list]              )      </code></td>
<td><code dir="ltr" translate="no">         RANK              () OVER              (              [PARTITION BY expr_list]              ORDER BY order_list              )      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         RATIO_TO_REPORT              (ratio_expression) OVER              (              [PARTITION BY partition_expression] )      </code></td>
<td><code dir="ltr" translate="no">       ratio_expression               SUM              (ratio_expression) OVER              (              [PARTITION BY partition_expression] )      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         ROW_NUMBER              () OVER              (              [PARTITION BY expr_list]              [ORDER BY order_list]              )      </code></td>
<td><code dir="ltr" translate="no">         ROW_NUMBER              () OVER              (              [PARTITION BY expr_list]              [ORDER BY order_list]              )      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         STDDEV              (expression) OVER              (              [PARTITION BY expr_list]              [ORDER BY order_list              frame_clause]              )      </code></td>
<td><code dir="ltr" translate="no">         STDDEV              (expression) OVER              (              [PARTITION BY expr_list]              [ORDER BY order_list]              [frame_clause] )      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         STDDEV_SAMP              (expression) OVER              (              [PARTITION BY expr_list]              [ORDER BY order_list              frame_clause]              )      </code></td>
<td><code dir="ltr" translate="no">         STDDEV_SAMP              (expression) OVER              (              [PARTITION BY expr_list]              [ORDER BY order_list]              [frame_clause]              )      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         STDDEV_POP              (expression) OVER              (              [PARTITION BY expr_list]              [ORDER BY order_list]              [frame_clause]              )      </code></td>
<td><code dir="ltr" translate="no">         STDDEV_POP              (expression) OVER              (              [PARTITION BY expr_list]              [ORDER BY order_list]              [frame_clause] )      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         SUM              (expression) OVER              (              [PARTITION BY expr_list]              [ORDER BY order_list]              [frame_clause]              )      </code></td>
<td><code dir="ltr" translate="no">         SUM              (expression) OVER              (              [PARTITION BY expr_list]              [ORDER BY order_list]              [frame_clause]              )      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         VAR_POP              (expression) OVER              (              [PARTITION BY expr_list]              [ORDER BY order_list]              [frame_clause]              )      </code></td>
<td><code dir="ltr" translate="no">         VAR_POP              (expression) OVER              (              [PARTITION BY expr_list]              [ORDER BY order_list]              [frame_clause]              )      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         VAR_SAMP              (expression) OVER              (              [PARTITION BY expr_list]              [ORDER BY order_list]              [frame_clause]              )      </code></td>
<td><code dir="ltr" translate="no">         VAR_SAMP              (expression) OVER              (              [PARTITION BY expr_list]              [ORDER BY order_list]              [frame_clause]              )      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         VARIANCE              (expression) OVER              (              [PARTITION BY expr_list]              [ORDER BY order_list]              [frame_clause]              )      </code></td>
<td><code dir="ltr" translate="no">         VARIANCE              (expression) OVER              (              [PARTITION BY expr_list]              [ORDER BY order_list]              [frame_clause]              )      </code></td>
</tr>
</tbody>
</table>

### Conditional expressions

The following table shows mappings between common Amazon Redshift conditional expressions with their BigQuery equivalents.

<table>
<thead>
<tr class="header">
<th><strong>Amazon Redshift</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         CASE              expression              WHEN value THEN result              [WHEN...]              [ELSE else_result]              END      </code></td>
<td><code dir="ltr" translate="no">         CASE              expression              WHEN value THEN result              [WHEN...]              [ELSE else_result]              END      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         COALESCE              (expression1[, ...])      </code></td>
<td><code dir="ltr" translate="no">         COALESCE              (expression1[, ...])      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         DECODE              (              expression,              search1, result1              [, search2, result2...]              [, default]              )      </code></td>
<td><code dir="ltr" translate="no">         CASE              expression              WHEN value1 THEN result1              [WHEN value2 THEN result2]              [ELSE default]              END      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         GREATEST              (value [, ...])      </code></td>
<td><code dir="ltr" translate="no">         GREATEST              (value [, ...])      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         LEAST              (value [, ...])      </code></td>
<td><code dir="ltr" translate="no">         LEAST              (value [, ...])      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         NVL              (expression1[, ...])      </code></td>
<td><code dir="ltr" translate="no">         COALESCE              (expression1[, ...])      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         NVL2              (              expression,              not_null_return_value,              null_return_value              )      </code></td>
<td><code dir="ltr" translate="no">         IF              (              expression IS NULL,              null_return_value,              not_null_return_value              )      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         NULLIF              (expression1, expression2)      </code></td>
<td><code dir="ltr" translate="no">         NULLIF              (expression1, expression2)      </code></td>
</tr>
</tbody>
</table>

BigQuery also offers the following conditional expressions, which do not have a direct analogue in Amazon Redshift:

  - [`  IF  `](/bigquery/docs/reference/standard-sql/conditional_expressions#if)
  - [`  IFNULL  `](/bigquery/docs/reference/standard-sql/conditional_expressions#ifnull)

### Date and time functions

The following table shows mappings between common Amazon Redshift date and time functions with their BigQuery equivalents. BigQuery data and time functions include [date functions](/bigquery/docs/reference/standard-sql/date_functions) , [datetime](/bigquery/docs/reference/standard-sql/datetime_functions) [functions](/bigquery/docs/reference/standard-sql/datetime_functions) , [time functions](/bigquery/docs/reference/standard-sql/time_functions) , and [timestamp functions](/bigquery/docs/reference/standard-sql/timestamp_functions) .

Keep in mind that functions that seem identical in Amazon Redshift and BigQuery might return different data types.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Amazon Redshift</th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         ADD_MONTHS              (              date,              integer              )      </code></td>
<td><code dir="ltr" translate="no">         CAST              (               DATE_ADD              (              date,              INTERVAL integer MONTH              )              AS TIMESTAMP              )      </code></td>
</tr>
<tr class="even">
<td>timestamptz_or_timestamp <code dir="ltr" translate="no">         AT TIME ZONE              timezone      </code></td>
<td><code dir="ltr" translate="no">         PARSE_TIMESTAMP              (              "%c%z",                FORMAT_TIMESTAMP              (              "%c%z",              timestamptz_or_timestamp,              timezone              )              )      </code><br />
<br />
Note: <a href="/bigquery/docs/reference/standard-sql/data-types#time_zones">Time zones</a> are used when parsing timestamps or formatting timestamps for display. A string-formatted timestamp might include a time zone, but when BigQuery parses the string, it stores the timestamp in the equivalent UTC time. When a time zone is not explicitly specified, the default time zone, UTC, is used. <a href="http://www.iana.org/time-zones">Time zone names</a> or <a href="/bigquery/docs/reference/standard-sql/timestamp_functions#timezone_definitions">offset from UTC</a> (-HH:MM) are supported, but time zone abbreviations (such as PDT) are not supported.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         CONVERT_TIMEZONE              (              [source_timezone],              target_timezone,              timestamp              )      </code></td>
<td><code dir="ltr" translate="no">         PARSE_TIMESTAMP              (              "%c%z",                FORMAT_TIMESTAMP              (              "%c%z",              timestamp,              target_timezone              )              )      </code><br />
<br />
Note: <code dir="ltr" translate="no">       source_timezone      </code> is UTC in BigQuery.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         CURRENT_DATE       </code><br />
<br />
Note: Returns start date for the current transaction in the current session time zone (UTC by default).</td>
<td><code dir="ltr" translate="no">         CURRENT_DATE              ()      </code><br />
<br />
Note: Returns start date for the current statement in the UTC time zone.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         DATE_CMP              (date1, date2)      </code></td>
<td><code dir="ltr" translate="no">         CASE               WHEN date1 = date2 THEN 0              WHEN date1 &gt; date2 THEN 1              ELSE -1              END      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         DATE_CMP_TIMESTAMP              (date1, date2)      </code></td>
<td><code dir="ltr" translate="no">         CASE               WHEN date1 = CAST(date2 AS DATE)              THEN 0              WHEN date1 &gt; CAST(date2 AS DATE)              THEN 1              ELSE -1              END      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         DATE_CMP_TIMESTAMPTZ              (date, timestamptz)      </code></td>
<td><code dir="ltr" translate="no">         CASE               WHEN date &gt;               DATE              (timestamptz)              THEN 1              WHEN date &lt;               DATE              (timestamptz)              THEN -1              ELSE 0              END      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         DATE_PART_YEAR              (date)      </code></td>
<td><code dir="ltr" translate="no">         EXTRACT              (YEAR FROM date)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         DATEADD              (date_part, interval, date)      </code></td>
<td><code dir="ltr" translate="no">         CAST              (                DATE_ADD              (              date,              INTERVAL interval datepart              )              AS TIMESTAMP              )      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         DATEDIFF              (              date_part,              date_expression1,              date_expression2              )      </code></td>
<td><code dir="ltr" translate="no">         DATE_DIFF              (              date_expression2,              date_expression1,              date_part              )      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         DATE_PART              (date_part, date)      </code></td>
<td><code dir="ltr" translate="no">         EXTRACT              (date_part FROM date)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         DATE_TRUNC              ('date_part', timestamp)      </code></td>
<td><code dir="ltr" translate="no">         TIMESTAMP_TRUNC              (timestamp, date_part)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         EXTRACT              (date_part FROM timestamp)      </code></td>
<td><code dir="ltr" translate="no">         EXTRACT              (date_part FROM timestamp)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         GETDATE              ()      </code></td>
<td><code dir="ltr" translate="no">       PARSE_TIMESTAMP(              "%c",              FORMAT_TIMESTAMP(              "%c",                CURRENT_TIMESTAMP              ()              )              )      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         INTERVAL_CMP              (              interval_literal1,              interval_literal2              )      </code></td>
<td>For intervals in Redshift, there are 360 days in a year. In BigQuery, you can use the following user-defined function (UDF) to parse a Redshift interval and translate it to seconds.<br />
<br />
<code dir="ltr" translate="no">         CREATE TEMP FUNCTION               parse_interval(interval_literal STRING) AS (              (select sum(case              when unit in ('minutes', 'minute', 'm' )              then num * 60              when unit in ('hours', 'hour', 'h') then num              * 60 * 60              when unit in ('days', 'day', 'd' ) then num              * 60 * 60 * 24              when unit in ('weeks', 'week', 'w') then num              * 60 * 60 * 24 * 7              when unit in ('months', 'month' ) then num *              60 * 60 * 24 * 30              when unit in ('years', 'year') then num * 60              * 60 * 24 * 360              else num              end)              from (              select              cast(regexp_extract(value,              r'^[0-9]*\.?[0-9]+') as numeric) num,              substr(value, length(regexp_extract(value,              r'^[0-9]*\.?[0-9]+')) + 1) unit              from                UNNEST              (                SPLIT              (              replace(              interval_literal, ' ', ''), ',')) value              )));      </code><br />
<br />
To compare interval literals, perform:<br />
<br />
<code dir="ltr" translate="no">         IF              (              parse_interval(interval_literal1) &gt;              parse_interval(interval_literal2),              1,                IF              (              parse_interval(interval_literal1) &gt;              parse_interval(interval_literal2),              -1,              0              )              )      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         LAST_DAY              (date)      </code></td>
<td><code dir="ltr" translate="no">         DATE_SUB              (                DATE_ADD              (              date,              INTERVAL 1 MONTH              ),              INTERVAL 1 DAY              )      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         MONTHS_BETWEEN              (              date1,              date2              )      </code></td>
<td><code dir="ltr" translate="no">         DATE_DIFF              (              date1,              date2,              MONTH              )      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         NEXT_DAY              (date, day)      </code></td>
<td><code dir="ltr" translate="no">         DATE_ADD              (                DATE_TRUNC              (              date,              WEEK(day)              ),              INTERVAL 1 WEEK              )      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         SYSDATE       </code><br />
<br />
Note: Returns start timestamp for the current transaction in the current session time zone (UTC by default).</td>
<td><code dir="ltr" translate="no">         CURRENT_TIMESTAMP              ()      </code><br />
<br />
Note: Returns start timestamp for the current statement in the UTC time zone.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         TIMEOFDAY              ()      </code></td>
<td><code dir="ltr" translate="no">         FORMAT_TIMESTAMP              (              "%a %b %d %H:%M:%E6S %E4Y %Z",                CURRENT_TIMESTAMP              ())      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         TIMESTAMP_CMP              (              timestamp1,              timestamp2              )      </code></td>
<td><code dir="ltr" translate="no">       CASE              WHEN timestamp1 = timestamp2              THEN 0              WHEN timestamp1 &gt; timestamp2              THEN 1              ELSE -1              END      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         TIMESTAMP_CMP_DATE              (              timestamp,              date              )      </code></td>
<td><code dir="ltr" translate="no">       CASE              WHEN                EXTRACT              (              DATE FROM timestamp              ) = date              THEN 0              WHEN                EXTRACT              (              DATE FROM timestamp) &gt; date              THEN 1              ELSE -1              END      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         TIMESTAMP_CMP_TIMESTAMPTZ              (              timestamp,              timestamptz              )      </code><br />
<br />
Note: Redshift compares timestamps in the user session-defined time zone. Default user session time zone is UTC.</td>
<td><code dir="ltr" translate="no">       CASE              WHEN timestamp = timestamptz              THEN 0              WHEN timestamp &gt; timestamptz              THEN 1              ELSE -1              END      </code><br />
<br />
Note: BigQuery compares timestamps in the UTC time zone.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         TIMESTAMPTZ_CMP              (              timestamptz1,              timestamptz2              )      </code><br />
<br />
Note: Redshift compares timestamps in the user session-defined time zone. Default user session time zone is UTC.</td>
<td><code dir="ltr" translate="no">       CASE              WHEN timestamptz1 = timestamptz2              THEN 0              WHEN timestamptz1 &gt; timestamptz2              THEN 1              ELSE -1              END      </code><br />
<br />
Note: BigQuery compares timestamps in the UTC time zone.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         TIMESTAMPTZ_CMP_DATE              (              timestamptz,              date              )      </code><br />
<br />
Note: Redshift compares timestamps in the user session-defined time zone. Default user session time zone is UTC.</td>
<td><code dir="ltr" translate="no">       CASE              WHEN                EXTRACT              (              DATE FROM timestamptz) = date              THEN 0              WHEN                EXTRACT              (              DATE FROM timestamptz) &gt; date              THEN 1              ELSE -1              END      </code><br />
<br />
Note: BigQuery compares timestamps in the UTC time zone.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         TIMESTAMPTZ_CMP_TIMESTAMP              (              timestamptz,              Timestamp              )      </code><br />
<br />
Note: Redshift compares timestamps in the user session-defined time zone. Default user session time zone is UTC.</td>
<td><code dir="ltr" translate="no">       CASE              WHEN timestamp = timestamptz              THEN 0              WHEN timestamp &gt; timestamptz              THEN 1              ELSE -1              END      </code><br />
<br />
Note: BigQuery compares timestamps in the UTC time zone.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         TIMEZONE              (              timezone,              Timestamptz_or_timestamp              )      </code></td>
<td><code dir="ltr" translate="no">         PARSE_TIMESTAMP              (              "%c%z",               FORMAT_TIMESTAMP              (              "%c%z",              timestamptz_or_timestamp,              timezone              )              )      </code><br />
<br />
Note: <a href="/bigquery/docs/reference/standard-sql/data-types#time_zones">Time zones</a> are used when parsing timestamps or formatting timestamps for display. A string-formatted timestamp might include a time zone, but when BigQuery parses the string, it stores the timestamp in the equivalent UTC time. When a time zone is not explicitly specified, the default time zone, UTC, is used. <a href="http://www.iana.org/time-zones">Time zone names</a> or <a href="/bigquery/docs/reference/standard-sql/timestamp_functions#timezone_definitions">offset from UTC</a> (-HH:MM) are supported but time zone abbreviations (such as PDT) are not supported.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         TO_TIMESTAMP              (timestamp, format)      </code></td>
<td><code dir="ltr" translate="no">         PARSE_TIMESTAMP              (                format              ,                FORMAT_TIMESTAMP              (                format              ,              timestamp              )              )      </code><br />
<br />
Note: BigQuery follows a different set of <a href="/bigquery/docs/reference/standard-sql/format-elements#format_elements_date_time">format elements</a> . <a href="/bigquery/docs/reference/standard-sql/data-types#time_zones">Time zones</a> are used when parsing timestamps or formatting timestamps for display. A string-formatted timestamp might include a time zone, but when BigQuery parses the string, it stores the timestamp in the equivalent UTC time. When a time zone is not explicitly specified, the default time zone, UTC, is used. <a href="http://www.iana.org/time-zones">Time zone names</a> or <a href="/bigquery/docs/reference/standard-sql/timestamp_functions#timezone_definitions">offset from UTC</a> (-HH:MM) are supported in the format string but time zone abbreviations (such as PDT) are not supported.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         TRUNC              (timestamp)      </code></td>
<td><code dir="ltr" translate="no">         CAST              (timestamp AS DATE)      </code></td>
</tr>
</tbody>
</table>

BigQuery also offers the following date and time functions, which do not have a direct analogue in Amazon Redshift:

  - [`  EXTRACT  `](/bigquery/docs/reference/standard-sql/date_functions#extract)
  - [`  DATE  `](/bigquery/docs/reference/standard-sql/date_functions#date)
  - [`  DATE_SUB  `](/bigquery/docs/reference/standard-sql/date_functions#date_sub)
  - [`  DATE_ADD  `](/bigquery/docs/reference/standard-sql/date_functions#date_add) (returning `  DATE  ` data type)
  - [`  DATE_FROM_UNIX_DATE  `](/bigquery/docs/reference/standard-sql/date_functions#date_from_unix_date)
  - [`  FORMAT_DATE  `](/bigquery/docs/reference/standard-sql/date_functions#format_date)
  - [`  PARSE_DATE  `](/bigquery/docs/reference/standard-sql/date_functions#parse_date)
  - [`  UNIX_DATE  `](/bigquery/docs/reference/standard-sql/date_functions#unix_date)
  - [`  DATETIME  `](/bigquery/docs/reference/standard-sql/datetime_functions#datetime)
  - [`  DATETIME_ADD  `](/bigquery/docs/reference/standard-sql/datetime_functions#datetime_add)
  - [`  DATETIME_SUB  `](/bigquery/docs/reference/standard-sql/datetime_functions#datetime_sub)
  - [`  DATETIME_DIFF  `](/bigquery/docs/reference/standard-sql/datetime_functions#datetime_diff)
  - [`  DATETIME_TRUNC  `](/bigquery/docs/reference/standard-sql/datetime_functions#datetime_trunc)
  - [`  FORMAT_DATETIME  `](/bigquery/docs/reference/standard-sql/datetime_functions#format_datetime)
  - [`  PARSE_DATETIME  `](/bigquery/docs/reference/standard-sql/datetime_functions#parse_datetime)
  - [`  CURRENT_TIME  `](/bigquery/docs/reference/standard-sql/time_functions#current_time)
  - [`  TIME  `](/bigquery/docs/reference/standard-sql/time_functions#time)
  - [`  TIME_ADD  `](/bigquery/docs/reference/standard-sql/time_functions#time_add)
  - [`  TIME_SUB  `](/bigquery/docs/reference/standard-sql/time_functions#time_sub)
  - [`  TIME_DIFF  `](/bigquery/docs/reference/standard-sql/time_functions#time_diff)
  - [`  TIME_TRUNC  `](/bigquery/docs/reference/standard-sql/time_functions#time_trunc)
  - [`  FORMAT_TIME  `](/bigquery/docs/reference/standard-sql/time_functions#format_time)
  - [`  PARSE_TIME  `](/bigquery/docs/reference/standard-sql/time_functions#parse_time)
  - [`  TIMESTAMP_SECONDS  `](/bigquery/docs/reference/standard-sql/timestamp_functions#timestamp_seconds)
  - [`  TIMESTAMP_MILLIS  `](/bigquery/docs/reference/standard-sql/timestamp_functions#timestamp_millis)
  - [`  TIMESTAMP_MICROS  `](/bigquery/docs/reference/standard-sql/timestamp_functions#timestamp_micros)
  - [`  UNIX_SECONDS  `](/bigquery/docs/reference/standard-sql/timestamp_functions#unix_seconds)
  - [`  UNIX_MILLIS  `](/bigquery/docs/reference/standard-sql/timestamp_functions#unix_millis)
  - [`  UNIX_MICROS  `](/bigquery/docs/reference/standard-sql/timestamp_functions#unix_micros)

### Mathematical operators

The following table shows mappings between common Amazon Redshift mathematical operators with their BigQuery equivalents.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Amazon Redshift</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        X + Y       </code></p></td>
<td><p><code dir="ltr" translate="no">        X + Y       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        X - Y       </code></p></td>
<td><p><code dir="ltr" translate="no">        X - Y       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        X * Y       </code></p></td>
<td><p><code dir="ltr" translate="no">        X * Y       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        X / Y       </code></p>
<br />
Note: If the operator is<br />
performing integer division (in other words, if <code dir="ltr" translate="no">       X      </code> and <code dir="ltr" translate="no">       Y      </code> are both integers), an integer is returned. If the operator is performing non-integer division, a non-integer is returned.</td>
<td>If integer division:<br />
<code dir="ltr" translate="no">         CAST              (               FLOOR              (X / Y) AS INT64)      </code><br />
<br />
If not integer division:<br />

<p><code dir="ltr" translate="no">          CAST                (X / Y AS INT64)       </code></p>
<br />
Note: Division in BigQuery returns a non-integer.<br />
To prevent errors from a division operation (division by zero error), use <code dir="ltr" translate="no">         SAFE_DIVIDE              (X, Y)      </code> or <code dir="ltr" translate="no">         IEEE_DIVIDE              (X, Y)      </code> .</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        X % Y       </code></p></td>
<td><p><code dir="ltr" translate="no">          MOD                (X, Y)       </code></p>
<br />
Note: To prevent errors from a division operation (division by zero error), use <code dir="ltr" translate="no">         SAFE              .               MOD              (X, Y)      </code> . <code dir="ltr" translate="no">         SAFE              .               MOD              (X, 0)      </code> results in 0.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        X ^ Y       </code></p></td>
<td><p><code dir="ltr" translate="no">          POW                (X, Y)       </code></p>
<p><code dir="ltr" translate="no">          POWER                (X, Y)       </code></p>
<br />
Note: Unlike Amazon Redshift, the <code dir="ltr" translate="no">       ^      </code> operator in BigQuery performs Bitwise xor.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        | / X       </code></p></td>
<td><p><code dir="ltr" translate="no">          SQRT                (X)       </code></p>
<br />
Note: To prevent errors from a square root operation (negative input), use <code dir="ltr" translate="no">         SAFE              .               SQRT              (X)      </code> . Negative input with <code dir="ltr" translate="no">         SAFE              .               SQRT              (X)      </code> results in <code dir="ltr" translate="no">       NULL      </code> .</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        || / X       </code></p></td>
<td><p><code dir="ltr" translate="no">          SIGN                (X) *                 POWER                (                 ABS                (X), 1/3)       </code></p>
<br />
Note: BigQuery's <code dir="ltr" translate="no">         POWER              (X, Y)      </code> returns an error if <code dir="ltr" translate="no">       X      </code> is a finite value less than 0 and <code dir="ltr" translate="no">       Y      </code> is a noninteger.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        @ X       </code></p></td>
<td><p><code dir="ltr" translate="no">          ABS                (X)       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        X &lt;&lt; Y       </code></p></td>
<td><p><code dir="ltr" translate="no">        X                 &lt;&lt;                Y       </code></p>
<br />
Note: This operator returns 0 or a byte sequence of b'\x00' if the second operand <code dir="ltr" translate="no">       Y      </code> is greater than or equal to the bit length of the first operand <code dir="ltr" translate="no">       X      </code> (for example, 64 if <code dir="ltr" translate="no">       X      </code> has the type INT64). This operator throws an error if <code dir="ltr" translate="no">       Y      </code> is negative.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        X &gt;&gt; Y       </code></p></td>
<td><p><code dir="ltr" translate="no">        X                 &gt;&gt;                Y       </code></p>
<br />
Note: Shifts the first operand <code dir="ltr" translate="no">       X      </code> to the right. This operator does not do sign bit extension with a signed type (it fills vacant bits on the left with 0). This operator returns 0 or a byte sequence of<br />
b'\x00' if the second operand <code dir="ltr" translate="no">       Y      </code> is greater than or equal to the bit length of the first operand <code dir="ltr" translate="no">       X      </code> (for example, 64 if <code dir="ltr" translate="no">       X      </code> has the type INT64). This operator throws an error if <code dir="ltr" translate="no">       Y      </code> is negative.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        X &amp; Y       </code></p></td>
<td><p><code dir="ltr" translate="no">        X                 &amp;                Y       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        X | Y       </code></p></td>
<td><p><code dir="ltr" translate="no">        X                 |                Y       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        ~X       </code></p></td>
<td><p><code dir="ltr" translate="no">          ~                X       </code></p></td>
</tr>
</tbody>
</table>

BigQuery also offers the following mathematical operator, which does not have a direct analog in Amazon Redshift:

  - [`  X ^ Y  `](/bigquery/docs/reference/standard-sql/operators#bitwise_operators) (Bitwise xor)

### Math functions

<table>
<thead>
<tr class="header">
<th><strong>Amazon Redshift</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         ABS              (number)      </code></td>
<td><code dir="ltr" translate="no">         ABS              (number)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         ACOS              (number)      </code></td>
<td><code dir="ltr" translate="no">         ACOS              (number)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         ASIN              (number)      </code></td>
<td><code dir="ltr" translate="no">         ASIN              (number)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         ATAN              (number)      </code></td>
<td><code dir="ltr" translate="no">         ATAN              (number)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         ATAN2              (number1, number2)      </code></td>
<td><code dir="ltr" translate="no">         ATAN2              (number1, number2)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         CBRT              (number)      </code></td>
<td><code dir="ltr" translate="no">         POWER              (number, 1/3)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         CEIL              (number)      </code></td>
<td><code dir="ltr" translate="no">         CEIL              (number)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         CEILING              (number)      </code></td>
<td><code dir="ltr" translate="no">         CEILING              (number)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         CHECKSUM              (expression)      </code></td>
<td><code dir="ltr" translate="no">         FARM_FINGERPRINT              (expression)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         COS              (number)      </code></td>
<td><code dir="ltr" translate="no">         COS              (number)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         COT              (number)      </code></td>
<td><code dir="ltr" translate="no">       1/               TAN              (number)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         DEGREES              (number)      </code></td>
<td><code dir="ltr" translate="no">       number      </code> *180/ <code dir="ltr" translate="no">         ACOS              (-1)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         DEXP              (number)      </code></td>
<td><code dir="ltr" translate="no">         EXP              (number)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         DLOG1              (number)      </code></td>
<td><code dir="ltr" translate="no">         LN              (number)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         DLOG10              (number)      </code></td>
<td><code dir="ltr" translate="no">         LOG10              (number)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         EXP              (number)      </code></td>
<td><code dir="ltr" translate="no">         EXP              (number)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         FLOOR              (number)      </code></td>
<td><code dir="ltr" translate="no">         FLOOR              (number)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         LN              number)      </code></td>
<td><code dir="ltr" translate="no">         LN              (number)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         LOG              (number)      </code></td>
<td><code dir="ltr" translate="no">         LOG10              (number)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         MOD              (number1, number2)      </code></td>
<td><code dir="ltr" translate="no">         MOD              (number1, number2)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         PI       </code></td>
<td><code dir="ltr" translate="no">         ACOS              (-1)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         POWER              (expression1, expression2)      </code></td>
<td><code dir="ltr" translate="no">         POWER              (expression1,         expression2)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         RADIANS              (number)      </code></td>
<td><code dir="ltr" translate="no">         ACOS              (-1)*(number/180)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         RANDOM              ()      </code></td>
<td><code dir="ltr" translate="no">         RAND              ()      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         ROUND              (number [, integer])      </code></td>
<td><code dir="ltr" translate="no">         ROUND              (number [, integer])      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         SIN              (number)      </code></td>
<td><code dir="ltr" translate="no">         SIN              (number)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         SIGN              (number)      </code></td>
<td><code dir="ltr" translate="no">         SIGN              (number)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         SQRT              (number)      </code></td>
<td><code dir="ltr" translate="no">         SQRT              (number)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         TAN              (number)      </code></td>
<td><code dir="ltr" translate="no">         TAN              (number)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         TO_HEX              (number)      </code></td>
<td><code dir="ltr" translate="no">         FORMAT              ('%x', number)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         TRUNC              (number [, integer])+-+++      </code></td>
<td><code dir="ltr" translate="no">         TRUNC              (number [, integer])      </code></td>
</tr>
</tbody>
</table>

### String functions

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Amazon Redshift</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>string1 <code dir="ltr" translate="no">         ||              string2      </code></td>
<td><code dir="ltr" translate="no">         CONCAT              (string1, string2)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         BPCHARCMP              (string1, string2)      </code></td>
<td><code dir="ltr" translate="no">         CASE               WHEN string1 = string2 THEN 0              WHEN string1 &gt; string2 THEN 1              ELSE -1              END      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         BTRIM              (string [, matching_string])      </code></td>
<td><code dir="ltr" translate="no">         TRIM              (string [, matching_string])      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         BTTEXT_PATTERN_CMP              (string1, string2)      </code></td>
<td><code dir="ltr" translate="no">         CASE               WHEN string1 = string2 THEN 0              WHEN string1 &gt; string2 THEN 1              ELSE -1              END      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         CHAR_LENGTH              (expression)      </code></td>
<td><code dir="ltr" translate="no">         CHAR_LENGTH              (expression)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         CHARACTER_LENGTH              (expression)      </code></td>
<td><code dir="ltr" translate="no">         CHARACTER_LENGTH              (expression)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         CHARINDEX              (substring, string)      </code></td>
<td><code dir="ltr" translate="no">         STRPOS              (string, substring)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         CHR              (number)      </code></td>
<td><code dir="ltr" translate="no">         CODE_POINTS_TO_STRING              ([number])      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         CONCAT              (string1, string2)      </code></td>
<td><code dir="ltr" translate="no">         CONCAT              (string1,         string2)      </code><br />
<br />
Note: BigQuery's <code dir="ltr" translate="no">         CONCAT       </code> (...) supports<br />
concatenating any number of strings.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         CRC32       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         FUNC_SHA1              (string)      </code></td>
<td><code dir="ltr" translate="no">         SHA1              (string)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         INITCAP       </code></td>
<td><code dir="ltr" translate="no">         INITCAP       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         LEFT              (string, integer)      </code></td>
<td><code dir="ltr" translate="no">         SUBSTR              (string, 0, integer)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         RIGHT              (string, integer)      </code></td>
<td><code dir="ltr" translate="no">         SUBSTR              (string, -integer)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         LEN              (expression)      </code></td>
<td><code dir="ltr" translate="no">         LENGTH              (expression)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         LENGTH              (expression)      </code></td>
<td><code dir="ltr" translate="no">         LENGTH              (expression)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         LOWER              (string)      </code></td>
<td><code dir="ltr" translate="no">         LOWER              (string)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         LPAD              (string1, length[, string2])      </code></td>
<td><code dir="ltr" translate="no">         LPAD              (string1, length[, string2])      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         RPAD              (string1, length[, string2])      </code></td>
<td><code dir="ltr" translate="no">         RPAD              (string1, length[, string2])      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         LTRIM              (string, trim_chars)      </code></td>
<td><code dir="ltr" translate="no">         LTRIM              (string, trim_chars)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         MD5              (string)      </code></td>
<td><code dir="ltr" translate="no">         MD5              (string)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         OCTET_LENGTH              (expression)      </code></td>
<td><code dir="ltr" translate="no">         BYTE_LENGTH              (expression)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         POSITION              (substring IN string)      </code></td>
<td><code dir="ltr" translate="no">         STRPOS              (string, substring)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         QUOTE_IDENT              (string)      </code></td>
<td><code dir="ltr" translate="no">         CONCAT              ('"',string,'"')      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         QUOTE_LITERAL              (string)      </code></td>
<td><code dir="ltr" translate="no">         CONCAT              ("'",string,"'")      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         REGEXP_COUNT              ( source_string, pattern              [,position]              )      </code></td>
<td><code dir="ltr" translate="no">         ARRAY_LENGTH              (               REGEXP_EXTRACT_ALL              (              source_string,              pattern              )              )      </code><br />
<br />
If <code dir="ltr" translate="no">       position      </code> is specified:<br />
<br />
<code dir="ltr" translate="no">         ARRAY_LENGTH              (               REGEXP_EXTRACT_ALL              (                SUBSTR              (source_string,               IF              (position &lt;= 0, 1, position)),              pattern              )              )      </code><br />
<br />
Note: BigQuery provides regular expression support using the <code dir="ltr" translate="no">         re2       </code> library; see that documentation for its regular expression syntax.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         REGEXP_INSTR              (              source_string,              pattern              [,position              [,occurrence]] )      </code></td>
<td><code dir="ltr" translate="no">         IFNULL              (               STRPOS              (              source_string,               REGEXP_EXTRACT              (              source_string,              pattern)              ),0)      </code><br />
<br />
If <code dir="ltr" translate="no">       source_string      </code> is specified:<br />
<br />
<code dir="ltr" translate="no">       REGEXP_REPLACE(              source_string,               pattern,              replace_string              )      </code><br />
<br />
If <code dir="ltr" translate="no">       position      </code> is specified:<br />
<br />
<code dir="ltr" translate="no">         IFNULL              (               STRPOS              (                SUBSTR              (source_string,               IF              (position              &lt;= 0, 1, position)),               REGEXP_EXTRACT              (                SUBSTR              (source_string,               IF              (position &lt;= 0, 1, position)),              pattern)              ) +               IF              (position &lt;= 0, 1, position) - 1, 0)      </code><br />
<br />
If <code dir="ltr" translate="no">       occurrence      </code> is specified:<br />
<br />
<code dir="ltr" translate="no">         IFNULL              (               STRPOS              (                SUBSTR              (source_string,               IF              (position              &lt;= 0, 1, position)),               REGEXP_EXTRACT_ALL              (                SUBSTR              (source_string,               IF              (position &lt;= 0, 1, position)),              pattern              )[               SAFE_ORDINAL              (occurrence)]              ) +               IF              (position &lt;= 0, 1, position) - 1, 0)      </code><br />
<br />
Note: BigQuery provides regular expression<br />
support using the <code dir="ltr" translate="no">         re2       </code> library; see that<br />
documentation for its regular expression<br />
syntax.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         REGEXP_REPLACE              ( source_string,              pattern              [, replace_string [, position]]              )      </code></td>
<td><code dir="ltr" translate="no">         REGEXP_REPLACE              (              source_string,              pattern,              ""              )      </code><br />
<br />
If <code dir="ltr" translate="no">       source_string      </code> is specified:<br />
<br />
<code dir="ltr" translate="no">         REGEXP_REPLACE              (              source_string,               pattern, replace_string              )      </code><br />
<br />
If <code dir="ltr" translate="no">       position      </code> is specified:<br />
<br />
<code dir="ltr" translate="no">         CASE               WHEN position &gt;               LENGTH              (source_string) THEN source_string              WHEN position &lt;= 0 THEN               REGEXP_REPLACE              (              source_string, pattern,              ""              ) ELSE                CONCAT              (               SUBSTR              (              source_string, 1, position - 1),               REGEXP_REPLACE              (                SUBSTR              (source_string, position), pattern,              replace_string              )              ) END      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         REGEXP_SUBSTR              ( source_string, pattern              [, position              [, occurrence]] )      </code></td>
<td><code dir="ltr" translate="no">         REGEXP_EXTRACT              (              source_string, pattern              )      </code><br />
<br />
If <code dir="ltr" translate="no">       position      </code> is specified:<br />
<br />
<code dir="ltr" translate="no">         REGEXP_EXTRACT              (                SUBSTR              (source_string,               IF              (position &lt;= 0, 1, position)),              pattern               )      </code><br />
<br />
If <code dir="ltr" translate="no">       occurrence      </code> is specified:<br />
<br />
<code dir="ltr" translate="no">         REGEXP_EXTRACT_ALL              (                SUBSTR              (source_string,               IF              (position &lt;= 0, 1, position)),                pattern              )[               SAFE_ORDINAL              (occurrence)]      </code><br />
<br />
Note: BigQuery provides regular expression support using the <code dir="ltr" translate="no">         re2       </code> library; see that documentation for its regular expression syntax.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         REPEAT              (string, integer)      </code></td>
<td><code dir="ltr" translate="no">         REPEAT              (string, integer)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         REPLACE              (string, old_chars, new_chars)      </code></td>
<td><code dir="ltr" translate="no">         REPLACE              (string, old_chars, new_chars)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         REPLICA              (string, integer)      </code></td>
<td><code dir="ltr" translate="no">         REPEAT              (string, integer)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         REVERSE              (expression)      </code></td>
<td><code dir="ltr" translate="no">         REVERSE              (expression)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         RTRIM              (string, trim_chars)      </code></td>
<td><code dir="ltr" translate="no">         RTRIM              (string, trim_chars)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         SPLIT_PART              (string, delimiter, part)      </code></td>
<td><code dir="ltr" translate="no">         SPLIT              (              string              delimiter              )               SAFE_ORDINAL              (part)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         STRPOS              (string, substring)      </code></td>
<td><code dir="ltr" translate="no">         STRPOS              (string, substring)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         STRTOL              (string, base)      </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         SUBSTRING              (              string,              start_position, number_characters )      </code></td>
<td><code dir="ltr" translate="no">         SUBSTR              (              string,              start_position, number_characters )      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         TEXTLEN              (expression)      </code></td>
<td><code dir="ltr" translate="no">         LENGTH              (expression)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         TRANSLATE              (              expression,              characters_to_replace, characters_to_substitute )      </code></td>
<td>Can be implemented using UDFs:<br />
<br />
<code dir="ltr" translate="no">         CREATE TEMP FUNCTION               translate(expression STRING,              characters_to_replace STRING, characters_to_substitute STRING) AS ( IF(LENGTH(characters_to_replace) &lt; LENGTH(characters_to_substitute) OR LENGTH(expression) &lt;              LENGTH(characters_to_replace), expression,              (SELECT              STRING_AGG(              IFNULL(              (SELECT ARRAY_CONCAT([c],              SPLIT(characters_to_substitute, ''))[SAFE_OFFSET((              SELECT IFNULL(MIN(o2) + 1,              0) FROM              UNNEST(SPLIT(characters_to_replace,              '')) AS k WITH OFFSET o2              WHERE k = c))]              ),              ''),              '' ORDER BY o1)              FROM UNNEST(SPLIT(expression, ''))              AS c WITH OFFSET o1              ))              );      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         TRIM              ([BOTH] string)      </code></td>
<td><code dir="ltr" translate="no">         TRIM              (string)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         TRIM              ([BOTH] characters FROM string)      </code></td>
<td><code dir="ltr" translate="no">         TRIM              (string, characters)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         UPPER              (string)      </code></td>
<td><code dir="ltr" translate="no">         UPPER              (string)      </code></td>
</tr>
</tbody>
</table>

### Data type formatting functions

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Amazon Redshift</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         CAST              (expression AS type)      </code></td>
<td><code dir="ltr" translate="no">         CAST              (expression AS type)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       expression               ::              type      </code></td>
<td><code dir="ltr" translate="no">         CAST              (expression AS type)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         CONVERT              (type, expression)      </code></td>
<td><code dir="ltr" translate="no">         CAST              (expression AS type)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         TO_CHAR              (              timestamp_expression, format              )      </code></td>
<td><code dir="ltr" translate="no">         FORMAT_TIMESTAMP              (              format,              timestamp_expression              )      </code><br />
<br />
Note: BigQuery and Amazon Redshift differ in how to specify a format string for <code dir="ltr" translate="no">       timestamp_expression      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         TO_CHAR              (              numeric_expression,              format              )      </code></td>
<td><code dir="ltr" translate="no">         FORMAT              (              format,              numeric_expression              )      </code><br />
<br />
Note: BigQuery and Amazon Redshift differ in how to specify a format string for <code dir="ltr" translate="no">       timestamp_expression      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         TO_DATE              (date_string, format)      </code></td>
<td><code dir="ltr" translate="no">         PARSE_DATE              (date_string, format)      </code><br />
<br />
Note: BigQuery and Amazon Redshift differ in how to specify a format string for <code dir="ltr" translate="no">       date_string      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         TO_NUMBER              (string, format)      </code></td>
<td><code dir="ltr" translate="no">         CAST              (                FORMAT              (              format,              numeric_expression              ) TO INT64              )      </code><br />
<br />
Note: BigQuery and Amazon Redshift differ in how to specify a numeric format string.</td>
</tr>
</tbody>
</table>

BigQuery also supports [`  SAFE_CAST  `](/bigquery/docs/reference/standard-sql/conversion_functions#safe_casting) `  (expression AS typename)  ` , which returns `  NULL  ` if BigQuery is unable to perform a cast; for example, [`  SAFE_CAST  `](/bigquery/docs/reference/standard-sql/conversion_functions#safe_casting) `  ("apple" AS INT64)  ` returns `  NULL  ` .

## DML syntax

This section addresses differences in data management language syntax between Amazon Redshift and BigQuery.

### `     INSERT    ` statement

Amazon Redshift offers a configurable `  DEFAULT  ` keyword for columns. In BigQuery, the `  DEFAULT  ` value for nullable columns is `  NULL  ` , and `  DEFAULT  ` is not supported for required columns. Most [Amazon Redshift `  INSERT  ` statements](https://docs.aws.amazon.com/redshift/latest/dg/r_INSERT_30.html) are compatible with BigQuery. The following table shows exceptions.

<table>
<thead>
<tr class="header">
<th><strong>Amazon Redshift</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       INSERT INTO table (column1 [, ...])              DEFAULT VALUES      </code></td>
<td><code dir="ltr" translate="no">       INSERT [INTO] table (column1 [, ...])              VALUES (DEFAULT [, ...])      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       INSERT INTO table (column1, [,...]) VALUES (              SELECT ...              FROM ...              )      </code></td>
<td><code dir="ltr" translate="no">       INSERT [INTO] table (column1, [,...])              SELECT ...              FROM ...      </code></td>
</tr>
</tbody>
</table>

BigQuery also supports inserting values using a subquery (where one of the values is computed using a subquery), which is not supported in Amazon Redshift. For example:

``` text
INSERT INTO table (column1, column2)
VALUES ('value_1', (
SELECT column2
FROM table2
))
```

### `     COPY    ` statement

Amazon Redshift's [`  COPY  `](https://docs.aws.amazon.com/redshift/latest/dg/r_COPY.html) command loads data into a table from data files or from an Amazon DynamoDB table. BigQuery does not use the `  SQL COPY  ` command to load data, but you can use any of several non-SQL tools and options to [load data into BigQuery tables](/bigquery/docs/loading-data) . You can also use data pipeline sinks provided in [Apache Spark](/dataproc/docs/concepts/connectors/cloud-storage#other_sparkhadoop_clusters) or [Apache Beam](https://beam.apache.org/documentation/io/built-in/google-bigquery/#writing-to-bigquery) to write data into BigQuery.

### `     UPDATE    ` statement

Most Amazon Redshift `  UPDATE  ` statements are compatible with BigQuery. The following table shows exceptions.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Amazon Redshift</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       UPDATE table              SET column = expression [,...] [FROM ...]      </code></td>
<td><code dir="ltr" translate="no">       UPDATE table              SET column = expression [,...]              [FROM ...]              WHERE TRUE      </code><br />
<br />
Note: All <code dir="ltr" translate="no">       UPDATE      </code> statements in BigQuery require a <code dir="ltr" translate="no">       WHERE      </code> keyword, followed by a condition.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       UPDATE table              SET column = DEFAULT [,...] [FROM ...]              [WHERE ...]      </code></td>
<td><code dir="ltr" translate="no">       UPDATE table              SET column = NULL [, ...]              [FROM ...]              WHERE ...      </code><br />
<br />
Note: BigQuery's <code dir="ltr" translate="no">       UPDATE      </code> command does not support <code dir="ltr" translate="no">       DEFAULT      </code> values.<br />
<br />
If the Amazon Redshift <code dir="ltr" translate="no">       UPDATE      </code> statement does not include a <code dir="ltr" translate="no">       WHERE      </code> clause, the BigQuery <code dir="ltr" translate="no">       UPDATE      </code> statement should be conditioned <code dir="ltr" translate="no">       WHERE TRUE      </code> .</td>
</tr>
</tbody>
</table>

### `     DELETE    ` and `     TRUNCATE    ` statements

The `  DELETE  ` and `  TRUNCATE  ` statements are both ways to remove rows from a table without affecting the table schema or indexes.

In Amazon Redshift, the `  TRUNCATE  ` statement is recommended over an unqualified `  DELETE  ` statement because it is faster and does not require `  VACUUM  ` and `  ANALYZE  ` operations afterward. However, you can use `  DELETE  ` statements to achieve the same effect.

In BigQuery, the `  DELETE  ` statement must have a `  WHERE  ` clause. For more information about `  DELETE  ` in BigQuery, see the BigQuery [`  DELETE  ` examples](/bigquery/docs/reference/standard-sql/dml-syntax#delete_examples) in the DML documentation.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Amazon Redshift</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         DELETE [FROM]              table_name      </code><br />
<br />
<code dir="ltr" translate="no">         TRUNCATE [TABLE]              table_name      </code></td>
<td><code dir="ltr" translate="no">         DELETE FROM              table_name              WHERE TRUE      </code><br />
<br />
BigQuery <code dir="ltr" translate="no">       DELETE      </code> statements require a <code dir="ltr" translate="no">       WHERE      </code> clause.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       DELETE FROM table_name              USING other_table              WHERE table_name.id=other_table.id      </code></td>
<td><code dir="ltr" translate="no">       DELETE FROM table_name              WHERE table_name.id IN (              SELECT id              FROM other_table              )      </code><br />
<br />
<code dir="ltr" translate="no">       DELETE FROM table_name              WHERE EXISTS (              SELECT id              FROM other_table              WHERE table_name.id = other_table.id )      </code><br />
<br />
In Amazon Redshift, <code dir="ltr" translate="no">       USING      </code> allows additional tables to be referenced in the <code dir="ltr" translate="no">       WHERE      </code> clause. This can be achieved in BigQuery by using a subquery in the <code dir="ltr" translate="no">       WHERE      </code> clause.</td>
</tr>
</tbody>
</table>

### `     MERGE    ` statement

The `  MERGE  ` statement can combine `  INSERT  ` , `  UPDATE  ` , and `  DELETE  ` operations into a single upsert statement and perform the operations atomically. The `  MERGE  ` operation must match at most one source row for each target row.

Amazon Redshift does not support a single `  MERGE  ` command. However, a merge operation can be performed in Amazon Redshift by performing `  INSERT  ` , `  UPDATE  ` , and `  DELETE  ` operations in a transaction.

#### Merge operation by replacing existing rows

In Amazon Redshift, an overwrite of all of the columns in the target table can be performed using a `  DELETE  ` statement and then an `  INSERT  ` statement. The `  DELETE  ` statement removes rows that should be updated, and then the `  INSERT  ` statement inserts the updated rows. BigQuery tables are limited to 1,000 DML statements per day, so you should consolidate `  INSERT  ` , `  UPDATE  ` , and `  DELETE  ` statements into a single `  MERGE  ` statement as shown in the following table.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Amazon Redshift</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>See <a href="https://docs.aws.amazon.com/redshift/latest/dg/merge-replacing-existing-rows.html">Performing a merge operation by</a> <a href="https://docs.aws.amazon.com/redshift/latest/dg/merge-replacing-existing-rows.html">replacing existing rows</a> .<br />
<br />
<code dir="ltr" translate="no">       CREATE TEMP TABLE temp_table;               INSERT INTO temp_table              SELECT *              FROM source              WHERE source.filter = 'filter_exp';               BEGIN TRANSACTION;               DELETE FROM target              USING temp_table              WHERE target.key = temp_table.key;               INSERT INTO target              SELECT *              FROM temp_table;               END TRANSACTION;               DROP TABLE temp_table;      </code></td>
<td><code dir="ltr" translate="no">       MERGE target              USING source              ON target.key = source.key              WHEN MATCHED AND source.filter = 'filter_exp' THEN              UPDATE SET              target.col1 = source.col1,              target.col2 = source.col2,              ...      </code><br />
<br />
Note: All columns must be listed if updating all columns.</td>
</tr>
<tr class="even">
<td>See <a href="https://docs.aws.amazon.com/redshift/latest/dg/merge-specify-a-column-list.html">Performing a merge operation by</a> <a href="https://docs.aws.amazon.com/redshift/latest/dg/merge-specify-a-column-list.html">specifying a column list</a> .<br />
<br />
<code dir="ltr" translate="no">       CREATE TEMP TABLE temp_table;               INSERT INTO temp_table              SELECT *              FROM source              WHERE source.filter = 'filter_exp';               BEGIN TRANSACTION;               UPDATE target SET              col1 = temp_table.col1,              col2 = temp_table.col2              FROM temp_table              WHERE target.key=temp_table.key;               INSERT INTO target              SELECT *              FROM      </code></td>
<td><code dir="ltr" translate="no">       MERGE target              USING source              ON target.key = source.key              WHEN MATCHED AND source.filter = 'filter_exp' THEN              UPDATE SET              target.col1 = source.col1,              target.col2 = source.col2      </code></td>
</tr>
</tbody>
</table>

## DDL syntax

This section addresses differences in data definition language syntax between Amazon Redshift and BigQuery.

### `     SELECT INTO    ` statement

In Amazon Redshift, the `  SELECT INTO  ` statement can be used to insert the results of a query into a new table, combining table creation and insertion.

<table>
<thead>
<tr class="header">
<th><strong>Amazon Redshift</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       SELECT expression, ... INTO table              FROM ...      </code></td>
<td><code dir="ltr" translate="no">       INSERT table              SELECT expression, ...              FROM ...      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       WITH subquery_table AS ( SELECT ...              )              SELECT expression, ... INTO table              FROM subquery_table              ...      </code></td>
<td><code dir="ltr" translate="no">       INSERT table              WITH subquery_table AS (              SELECT ...              )              SELECT expression, ...              FROM subquery_table              ...      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       SELECT expression              INTO TEMP table              FROM ...               SELECT expression              INTO TEMPORARY table              FROM ...      </code></td>
<td>BigQuery offers several ways to emulate temporary tables. See the <a href="#temporary_tables">temporary tables</a> section for more information.</td>
</tr>
</tbody>
</table>

### `     CREATE TABLE    ` statement

Most Amazon Redshift [`  CREATE TABLE  `](https://docs.teradata.com/reader/scPHvjfglIlB8F70YliLAw/t9ZHBbmVpK7GrnocHmVG1Q) statements are compatible with BigQuery, except for the following syntax elements, which are not used in BigQuery:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Amazon Redshift</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       CREATE TABLE table_name (              col1 data_type1 NOT NULL,              col2 data_type2 NULL,              col3 data_type3 UNIQUE,              col4 data_type4 PRIMARY KEY,              col5 data_type5              )      </code><br />
<br />
Note: <code dir="ltr" translate="no">       UNIQUE      </code> and <code dir="ltr" translate="no">       PRIMARY KEY      </code> constraints are informational and <a href="https://docs.aws.amazon.com/redshift/latest/dg/t_Defining_constraints.html">are not enforced by the Amazon Redshift</a> <a href="https://docs.aws.amazon.com/redshift/latest/dg/t_Defining_constraints.html">system</a> .</td>
<td><code dir="ltr" translate="no">       CREATE TABLE table_name (              col1 data_type1 NOT NULL,              col2 data_type2,              col3 data_type3,              col4 data_type4,              col5 data_type5,              )      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       CREATE TABLE table_name              (              col1 data_type1[,...]              table_constraints              )              where table_constraints are:              [UNIQUE(column_name [, ... ])]              [PRIMARY KEY(column_name [, ...])]              [FOREIGN KEY(column_name [, ...])              REFERENCES reftable [(refcolumn)]      </code><br />
<br />
Note: <code dir="ltr" translate="no">       UNIQUE      </code> and <code dir="ltr" translate="no">       PRIMARY KEY      </code> constraints are informational and <a href="https://docs.aws.amazon.com/redshift/latest/dg/t_Defining_constraints.html">are not enforced by the Amazon Redshift system</a> .</td>
<td><code dir="ltr" translate="no">       CREATE TABLE table_name              (              col1 data_type1[,...]              )                PARTITION BY              column_name                CLUSTER BY              column_name [, ...]      </code><br />
<br />
Note: BigQuery does not use <code dir="ltr" translate="no">       UNIQUE      </code> , <code dir="ltr" translate="no">       PRIMARY KEY      </code> , or <code dir="ltr" translate="no">       FOREIGN KEY      </code> table constraints. To achieve similar optimization that these constraints provide during query execution, partition and cluster your BigQuery tables. <code dir="ltr" translate="no">       CLUSTER BY      </code> supports up to 4 columns.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       CREATE TABLE table_name              LIKE original_table_name      </code></td>
<td>Reference <a href="/bigquery/docs/information-schema-tables#example_3">this example</a> to learn how to use the <code dir="ltr" translate="no">       INFORMATION_SCHEMA      </code> tables to copy column names, data types, and <code dir="ltr" translate="no">       NOT NULL      </code> constraints to a new table.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       CREATE TABLE table_name              (              col1 data_type1              )              BACKUP NO      </code><br />
<br />
Note: In Amazon Redshift, the <code dir="ltr" translate="no">         BACKUP NO       </code> setting is specified to save processing time and reduce storage space.</td>
<td>The <code dir="ltr" translate="no">       BACKUP NO      </code> table option is not used or needed because BigQuery automatically keeps up to 7 days of historical versions of all of your tables with no effect on processing time or billed storage.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       CREATE TABLE table_name              (              col1 data_type1              )              table_attributes              where table_attributes are:              [DISTSTYLE {AUTO|EVEN|KEY|ALL}]              [DISTKEY (column_name)]              [[COMPOUND|INTERLEAVED] SORTKEY              (column_name [, ...])]      </code></td>
<td>BigQuery supports clustering, which allows storing keys in sorted order.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       CREATE TABLE table_name              AS SELECT ...      </code></td>
<td><code dir="ltr" translate="no">       CREATE TABLE table_name              AS SELECT ...      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       CREATE TABLE IF NOT EXISTS table_name ...      </code></td>
<td><code dir="ltr" translate="no">       CREATE TABLE IF NOT EXISTS              table_name              ...      </code></td>
</tr>
</tbody>
</table>

BigQuery also supports the DDL statement `  CREATE OR REPLACE TABLE  ` , which overwrites a table if it already exists.

BigQuery's `  CREATE TABLE  ` statement also supports the following clauses, which do not have an Amazon Redshift equivalent:

  - [`  PARTITION BY partition  ` statement](/bigquery/docs/reference/standard-sql/data-definition-language#partition_expression)
  - [`  CLUSTER BY clustering_column_list  `](/bigquery/docs/reference/standard-sql/data-definition-language#clustering_column_list)
  - [`  OPTIONS(table_options_list)  `](/bigquery/docs/reference/standard-sql/data-definition-language#table_option_list)

For more information about `  CREATE TABLE  ` in BigQuery, see the BigQuery [`  CREATE TABLE  ` examples](/bigquery/docs/reference/standard-sql/data-definition-language#create-table-examples) in the DML documentation.

#### Temporary tables

Amazon Redshift supports temporary tables, which are only visible within the current session. There are several ways to emulate temporary tables in BigQuery:

  - Dataset TTL: Create a dataset that has a short time to live (for example, one hour) so that any tables created in the dataset are effectively temporary because they won't persist longer than the dataset's time to live. You can prefix all of the table names in this dataset with temp to clearly denote that the tables are temporary.

  - Table TTL: Create a table that has a table-specific short time to live using DDL statements similar to the following:
    
    ``` text
    CREATE TABLE
    temp.name (col1, col2, ...)
    OPTIONS (expiration_timestamp=TIMESTAMP_ADD(CURRENT_TIMESTAMP(),
    INTERVAL 1 HOUR));
    ```

### `     CREATE VIEW    ` statement

The following table shows equivalents between Amazon Redshift and BigQuery for the `  CREATE VIEW  ` statement.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Amazon Redshift</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       CREATE VIEW view_name AS SELECT ...      </code> code&gt;</td>
<td><code dir="ltr" translate="no">         CREATE VIEW              view_name AS SELECT         ...      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       CREATE OR REPLACE VIEW view_name AS SELECT ...      </code></td>
<td><code dir="ltr" translate="no">         CREATE OR REPLACE VIEW               view_name AS              SELECT ...      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       CREATE VIEW view_name              (column_name, ...)              AS SELECT ...      </code></td>
<td><code dir="ltr" translate="no">         CREATE VIEW              view_name AS SELECT ...      </code></td>
</tr>
<tr class="even">
<td>Not supported.</td>
<td><code dir="ltr" translate="no">         CREATE VIEW IF NOT EXISTS              c view_name              OPTIONS(               view_option_list              )              AS SELECT …      </code><br />
<br />
Creates a new view only if the view does not exist in the specified dataset.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       CREATE VIEW view_name              AS SELECT ...                WITH NO SCHEMA BINDING       </code><br />
<br />
In Amazon Redshift, a late binding view is required in order to reference an external table.</td>
<td>In BigQuery, to create a view, all referenced objects must already exist.<br />
<br />
BigQuery allows you to <a href="/bigquery/external-data-sources">query external data sources.</a></td>
</tr>
</tbody>
</table>

## User-defined functions (UDFs)

A UDF lets you create functions for custom operations. These functions accept columns of input, perform actions, and return the result of those actions as a value.

Both Amazon Redshift and BigQuery support UDFs using SQL expressions. Additionally, in Amazon Redshift you can create a [Python-based UDF](https://docs.aws.amazon.com/redshift/latest/dg/udf-python-language-support.html) , and in BigQuery you can create a [JavaScript-based UDF](/bigquery/docs/user-defined-functions#javascript-udf-structure) .

Refer to the [Google Cloud BigQuery utilities GitHub repository](https://github.com/GoogleCloudPlatform/bigquery-utils/tree/master/udfs/community) for a library of common BigQuery UDFs.

### `     CREATE FUNCTION    ` syntax

The following table addresses differences in SQL UDF creation syntax between Amazon Redshift and BigQuery.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Amazon Redshift</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         CREATE [OR REPLACE] FUNCTION               function_name              ([sql_arg_name sql_arg_data_type[,..]]) RETURNS data_type              IMMUTABLE              AS $$              sql_function_definition              $$ LANGUAGE sql      </code></td>
<td><code dir="ltr" translate="no">         CREATE [OR REPLACE] FUNCTION               function_name              ([sql_arg_name sql_arg_data_type[,..]]) AS              sql_function_definition      </code><br />
<br />
Note: In a BigQuery <a href="/bigquery/docs/user-defined-functions#sql-udf-structure">SQL UDF</a> , a return data type is optional. BigQuery infers the result type of the function from the SQL function body when a query calls the function.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         CREATE [OR REPLACE] FUNCTION               function_name              ([sql_arg_name sql_arg_data_type[,..]]) RETURNS data_type              { VOLATILE | STABLE | IMMUTABLE } AS $$              sql_function_definition              $$ LANGUAGE sql      </code></td>
<td><code dir="ltr" translate="no">         CREATE [OR REPLACE] FUNCTION               function_name              ([sql_arg_name sql_arg_data_type[,..]]) RETURNS data_type              AS sql_function_definition      </code><br />
<br />
Note: Function volatility is not a configurable parameter in BigQuery. All BigQuery UDF volatility is equivalent to Amazon Redshift's <code dir="ltr" translate="no">       IMMUTABLE      </code> volatility (that is, it does not do database lookups or otherwise use information not directly present in its argument list).</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         CREATE [OR REPLACE] FUNCTION               function_name              ([sql_arg_name sql_arg_data_type[,..]]) RETURNS data_type              IMMUTABLE              AS $$              SELECT_clause              $$ LANGUAGE sql      </code><br />
<br />
Note: Amazon Redshift supports only a <code dir="ltr" translate="no">       SQL SELECT      </code> clause as function definition. Also, the <code dir="ltr" translate="no">       SELECT      </code> clause cannot include any of the <code dir="ltr" translate="no">       FROM, INTO, WHERE, GROUP BY, ORDER BY,      </code> and <code dir="ltr" translate="no">       LIMIT      </code> clauses.</td>
<td><code dir="ltr" translate="no">         CREATE [OR REPLACE] FUNCTION               function_name              ([sql_arg_name sql_arg_data_type[,..]]) RETURNS data_type              AS sql_expression      </code><br />
<br />
Note: BigQuery supports any SQL expressions as function definition. However, referencing tables, views, or models is not supported.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         CREATE [OR REPLACE] FUNCTION               function_name              ([sql_arg_name sql_arg_data_type[,..]]) RETURNS data_type              IMMUTABLE              AS $$              sql_function_definition              $$ LANGUAGE sql      </code></td>
<td><code dir="ltr" translate="no">         CREATE [OR REPLACE] FUNCTION              function_name ([sql_arg_name sql_arg_data_type[,..]]) RETURNS data_type AS sql_function_definition      </code><br />
<br />
Note: Language literal need not be specified in a GoogleSQL UDF. BigQuery interprets the SQL expression by default. Also, the Amazon Redshift dollar quoting ( <code dir="ltr" translate="no">       $$      </code> ) is not supported in BigQuery.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         CREATE [OR REPLACE] FUNCTION              function_name (integer, integer) RETURNS integer IMMUTABLE AS $$ SELECT $1 + $2 $$ LANGUAGE sql      </code></td>
<td><code dir="ltr" translate="no">         CREATE [OR REPLACE] FUNCTION               function_name              (x INT64, y INT64)              RETURNS INT64              AS              SELECT x + y      </code><br />
<br />
Note: BigQuery UDFs require all input arguments to be named. The Amazon Redshift argument variables ( <code dir="ltr" translate="no">       $1      </code> , <code dir="ltr" translate="no">       $2      </code> , …) are not supported in BigQuery.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         CREATE [OR REPLACE] FUNCTION               function_name              (integer, integer)              RETURNS integer              IMMUTABLE              AS $$              SELECT $1 + $2              $$ LANGUAGE sql      </code><br />
<br />
Note: Amazon Redshift does not support <code dir="ltr" translate="no">       ANY TYPE      </code> for SQL UDFs. However, it supports using the <code dir="ltr" translate="no">         ANYELEMENT       </code> data type in Python-based UDFs.</td>
<td><code dir="ltr" translate="no">         CREATE [OR REPLACE] FUNCTION               function_name              (x ANY TYPE, y ANY TYPE)              AS              SELECT x + y      </code><br />
<br />
Note: BigQuery supports using <code dir="ltr" translate="no">       ANY TYPE      </code> as argument type. The function accepts an input of any type for this argument. For more information, see <a href="/bigquery/docs/user-defined-functions#templated-sql-udf-parameters">templated parameter</a> in BigQuery.</td>
</tr>
</tbody>
</table>

BigQuery also supports the `  CREATE FUNCTION IF NOT EXISTS  ` statement, which treats the query as successful and takes no action if a function with the same name already exists.

BigQuery's `  CREATE FUNCTION  ` statement also supports creating [`  TEMPORARY  `](/bigquery/docs/reference/standard-sql/data-definition-language#create_function_statement) or `  TEMP  ` functions, which do not have an Amazon Redshift equivalent.

See [calling UDFs](/bigquery/docs/reference/standard-sql/syntax#calling_persistent_user-defined_functions_udfs) for details on executing a BigQuery-persistent UDF.

### `     DROP FUNCTION    ` syntax

The following table addresses differences in `  DROP FUNCTION  ` syntax between Amazon Redshift and BigQuery.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Amazon Redshift</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         DROP FUNCTION               function_name              ( [arg_name] arg_type [, ...] ) [ CASCADE | RESTRICT ]      </code></td>
<td><code dir="ltr" translate="no">         DROP FUNCTION               dataset_name.function_name      </code><br />
<br />
Note: BigQuery does not require using the function's signature for deleting the function. Also, removing function dependencies is not supported in BigQuery.</td>
</tr>
</tbody>
</table>

BigQuery also supports the [`  DROP FUNCTION IF EXISTS  `](/bigquery/docs/reference/standard-sql/data-definition-language#drop_function_statement) statement, which deletes the function only if the function exists in the specified dataset.

BigQuery requires that you specify the `  project_name  ` if the function is not located in the current project.

### UDF components

This section highlights the similarities and differences in UDF components between Amazon Redshift andBigQuery.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Component</strong></th>
<th><strong>Amazon Redshift</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Name</strong></td>
<td>Amazon Redshift <a href="https://docs.aws.amazon.com/redshift/latest/dg/udf-naming-udfs.html">recommends</a> using the prefix <code dir="ltr" translate="no">       _f      </code> for function names to avoid conflicts with existing or future built-in SQL function names.</td>
<td>In BigQuery, you can use any custom function name.</td>
</tr>
<tr class="even">
<td><strong>Arguments</strong></td>
<td>Arguments are optional. You can use name and data types for Python UDF arguments and only data types for SQL UDF arguments. In SQL UDFs, you must refer to arguments using <code dir="ltr" translate="no">       $1      </code> , <code dir="ltr" translate="no">       $2      </code> , and so on. Amazon Redshift also <a href="https://docs.aws.amazon.com/redshift/latest/dg/r_CREATE_FUNCTION.html">restricts the number of arguments</a> to 32.</td>
<td>Arguments are optional, but if you specify arguments, they must use both name and data types for both JavaScript and SQL UDFs. The maximum number of arguments for a persistent UDF is 256.</td>
</tr>
<tr class="odd">
<td><strong>Data type</strong></td>
<td>Amazon Redshift supports a different set of data types for <a href="https://docs.aws.amazon.com/redshift/latest/dg/c_Supported_data_types.html">SQL</a> and <a href="https://docs.aws.amazon.com/redshift/latest/dg/udf-data-types.html">Python</a> UDFs.<br />
For a Python UDF, the data type might also be <code dir="ltr" translate="no">         ANYELEMENT       </code> .<br />
<br />
You must specify a <code dir="ltr" translate="no">       RETURN      </code> data type for both SQL and Python UDFs.<br />
<br />
See <a href="#data_types">Data types</a> in this document for equivalents between data types in Amazon Redshift and in BigQuery.</td>
<td>BigQuery supports a different set of data types for <a href="/bigquery/docs/reference/standard-sql/data-types">SQL</a> and <a href="/bigquery/docs/user-defined-functions#supported-javascript-udf-data-types">JavaScript</a> UDFs.<br />
For a SQL UDF, the data type might also be <code dir="ltr" translate="no">       ANY TYPE      </code> . For more information, see <a href="/bigquery/docs/user-defined-functions#templated-sql-udf-parameters">templated parameters</a> in BigQuery.<br />
<br />
The <code dir="ltr" translate="no">       RETURN      </code> data type is optional for SQL UDFs.<br />
<br />
See <a href="/bigquery/docs/user-defined-functions#supported-javascript-udf-data-types">Supported JavaScript UDF data types</a> for information on how BigQuery data types map to JavaScript data types.</td>
</tr>
<tr class="even">
<td><strong>Definition</strong></td>
<td>For both SQL and Python UDFs, you must enclose the function definition using dollar quoting, as in a pair of dollar signs ( <code dir="ltr" translate="no">       $$      </code> ), to indicate the start and end of the function statements.<br />
<br />
For <a href="https://docs.aws.amazon.com/redshift/latest/dg/udf-creating-a-scalar-sql-udf.html">SQL UDFs,</a> Amazon Redshift supports only a SQL <code dir="ltr" translate="no">       SELECT      </code> clause as the function definition. Also, the <code dir="ltr" translate="no">       SELECT      </code> clause cannot include any of the <code dir="ltr" translate="no">       FROM      </code> , <code dir="ltr" translate="no">       INTO      </code> , <code dir="ltr" translate="no">       WHERE      </code> , <code dir="ltr" translate="no">       GROUP      </code><br />
<code dir="ltr" translate="no">       BY      </code> , <code dir="ltr" translate="no">       ORDER BY      </code> , and <code dir="ltr" translate="no">       LIMIT      </code> clauses.<br />
<br />
For <a href="https://docs.aws.amazon.com/redshift/latest/dg/udf-python-language-support.html">Python UDFs</a> , you can write a Python program using the <a href="https://docs.python.org/2/library/index.html">Python 2.7 Standard Library</a> or import your custom modules by creating one using the <code dir="ltr" translate="no">         CREATE LIBRARY       </code> command.</td>
<td>In BigQuery, you need to enclose the JavaScript code in quotes. See <a href="/bigquery/docs/user-defined-functions#quoting-rules">Quoting</a> <a href="/bigquery/docs/user-defined-functions#quoting-rules">rules</a> for more information.<br />
<br />
For <a href="/bigquery/docs/user-defined-functions#sql-udf-structure">SQL UDFs</a> , you can use any SQL expressions as the function definition. However, BigQuery doesn't support referencing tables, views, or models.<br />
<br />
For <a href="/bigquery/docs/user-defined-functions#javascript-udf-structure">JavaScript UDFs</a> , you can <a href="/bigquery/docs/user-defined-functions#including-javascript-libraries">include</a> <a href="/bigquery/docs/user-defined-functions#including-javascript-libraries">external code libraries</a> directly using the <code dir="ltr" translate="no">       OPTIONS      </code> section. You can also use the <a href="https://github.com/GoogleCloudPlatform/bigquery-udf-test-tool">BigQuery UDF test tool</a> to test your functions.</td>
</tr>
<tr class="odd">
<td><strong>Language</strong></td>
<td>You must use the <code dir="ltr" translate="no">       LANGUAGE      </code> literal to specify the language as either <code dir="ltr" translate="no">       sql      </code> for SQL UDFs or <code dir="ltr" translate="no">       plpythonu      </code> for Python UDFs.</td>
<td>You need not specify <code dir="ltr" translate="no">       LANGUAGE      </code> for SQL UDFs but must specify the language as <code dir="ltr" translate="no">       js      </code> for JavaScript UDFs.</td>
</tr>
<tr class="even">
<td><strong>State</strong></td>
<td>Amazon Redshift does not support creating temporary UDFs.<br />
<br />
Amazon Redshift provides an option to define the <a href="https://docs.aws.amazon.com/redshift/latest/dg/r_CREATE_FUNCTION.html#r_CREATE_FUNCTION-parameters">volatility of a function</a> using <code dir="ltr" translate="no">       VOLATILE      </code> , <code dir="ltr" translate="no">       STABLE      </code> , or <code dir="ltr" translate="no">       IMMUTABLE      </code> literals. This is used for optimization by the query optimizer.</td>
<td>BigQuery supports both persistent and temporary UDFs. You can reuse persistent UDFs across multiple queries, whereas you can only use temporary UDFs in a single query.<br />
<br />
Function volatility is not a configurable parameter in BigQuery. All BigQuery UDF volatility is equivalent to Amazon Redshift's <code dir="ltr" translate="no">       IMMUTABLE      </code> volatility.</td>
</tr>
<tr class="odd">
<td><strong>Security and privileges</strong></td>
<td>To create a UDF, you must have <a href="https://docs.aws.amazon.com/redshift/latest/dg/udf-security-and-privileges.html">permission for usage on language</a> for SQL or plpythonu (Python). By default, <code dir="ltr" translate="no">       USAGE ON LANGUAGE SQL      </code> is granted to <code dir="ltr" translate="no">       PUBLIC      </code> , but you must explicitly grant <code dir="ltr" translate="no">       USAGE ON LANGUAGE PLPYTHONU      </code> to specific users or groups.<br />
Also, you must be a superuser to replace a UDF.</td>
<td>Granting explicit permissions for creating or deleting any type of UDF is not necessary in BigQuery. Any user assigned a role of <a href="/bigquery/docs/access-control#bigquery">BigQuery Data Editor</a> (having <code dir="ltr" translate="no">       bigquery.routines.               *       </code> as one of the permissions) can create or delete functions for the specified dataset.<br />
<br />
BigQuery also supports creating custom roles. This can be managed using <a href="/iam/docs/roles-overview#custom">Cloud IAM</a> .</td>
</tr>
<tr class="even">
<td><strong>Limits</strong></td>
<td>See <a href="https://docs.aws.amazon.com/redshift/latest/dg/udf-constraints.html">Python UDF limits</a> .</td>
<td>See <a href="/bigquery/quotas#udf_limits">limits on user-defined functions</a> .</td>
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
<th><strong>Amazon Redshift</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       SELECT * FROM               STL_ANALYZE              WHERE name              = 'T';      </code></td>
<td>Not used in BigQuery. You don't need to gather statistics in order to improve query performance. To get information about your data distribution, you can use <a href="/bigquery/docs/reference/standard-sql/approximate_aggregate_functions">approximate aggregate functions</a> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         ANALYZE              [[ table_name[(column_name              [, ...])]]      </code></td>
<td>Not used in BigQuery.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         LOCK TABLE              table_name;      </code></td>
<td>Not used in BigQuery.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         BEGIN TRANSACTION              ; SELECT ...                END TRANSACTION              ;      </code></td>
<td>BigQuery uses snapshot isolation. For details, see <a href="#consistency_guarantees_and_transaction_isolation">Consistency guarantees</a> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         EXPLAIN              ...      </code></td>
<td>Not used in BigQuery.<br />
<br />
Similar features are the <a href="/bigquery/query-plan-explanation">query plan explanation</a> in the BigQuery Google Cloud console, and in <a href="/bigquery/docs/monitoring">audit logging in Cloud Monitoring</a> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       SELECT * FROM               SVV_TABLE_INFO              WHERE              table = 'T';      </code></td>
<td><code dir="ltr" translate="no">       SELECT * EXCEPT(is_typed) FROM              mydataset.INFORMATION_SCHEMA.TABLES;      </code><br />
<br />
For more information see <a href="/bigquery/docs/information-schema-intro">Introduction to BigQuery <code dir="ltr" translate="no">        INFORMATION_SCHEMA       </code></a> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         VACUUM              [table_name]      </code></td>
<td>Not used in BigQuery. BigQuery <a href="/bigquery/docs/clustered-tables#automatic_reclustering">clustered tables are automatically sorted</a> .</td>
</tr>
</tbody>
</table>

### Multi-statement and multi-line SQL statements

Both Amazon Redshift and BigQuery support transactions (sessions) and therefore support statements separated by semicolons that are consistently executed together. For more information, see [Multi-statement transactions](/bigquery/docs/transactions) .

## Procedural SQL statements

### `     CREATE PROCEDURE    ` statement

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Amazon Redshift</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         CREATE or REPLACE PROCEDURE       </code></td>
<td><code dir="ltr" translate="no">         CREATE PROCEDURE       </code> if a name is required.<br />
<br />
Otherwise, use inline with <code dir="ltr" translate="no">         BEGIN       </code> or in a single line with <code dir="ltr" translate="no">         CREATE TEMP FUNCTION       </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         CALL       </code></td>
<td><code dir="ltr" translate="no">         CALL       </code></td>
</tr>
</tbody>
</table>

### Variable declaration and assignment

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Amazon Redshift</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         DECLARE       </code></td>
<td><code dir="ltr" translate="no">         DECLARE       </code><br />
<br />
Declares a variable of the specified type.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         SET       </code></td>
<td><code dir="ltr" translate="no">         SET       </code><br />
<br />
Sets a variable to have the value of the provided expression, or sets multiple variables at the same time based on the result of multiple expressions.</td>
</tr>
</tbody>
</table>

### Error condition handlers

In Amazon Redshift, an error encountered during the execution of a stored procedure ends the execution flow, ends the transaction, and rolls back the transaction. These results occur because subtransactions are not supported. In an Amazon Redshift-stored procedure, the only supported `  handler_statement  ` is `  RAISE  ` . In BigQuery, error handling is a core feature of the main control flow, similar to what other languages provide with `  TRY ... CATCH  ` blocks.

<table>
<thead>
<tr class="header">
<th><strong>Amazon Redshift</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         BEGIN ... EXCEPTION WHEN OTHERS                THEN       </code></td>
<td><code dir="ltr" translate="no">         BEGIN ... EXCEPTION WHEN ERROR THEN       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         RAISE       </code></td>
<td><code dir="ltr" translate="no">         RAISE       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       [ &lt;&lt;label&gt;&gt; ] [ DECLARE declarations ]              BEGIN              statements EXCEPTION              BEGIN              statements              EXCEPTION              WHEN OTHERS THEN              Handler_statements              END;      </code></td>
<td><code dir="ltr" translate="no">       BEGIN              BEGIN              ...              EXCEPTION WHEN ERROR THEN SELECT 1/0;              END;               EXCEPTION WHEN ERROR THEN -- The exception thrown from the inner exception handler lands here. END;      </code></td>
</tr>
</tbody>
</table>

### Cursor declarations and operations

Because BigQuery doesn't support cursors or sessions, the following statements aren't used in BigQuery:

  - [`  DECLARE  `](https://docs.aws.amazon.com/redshift/latest/dg/declare.html) [`  cursor_name  `](https://docs.aws.amazon.com/redshift/latest/dg/declare.html) [`  CURSOR  `](https://docs.aws.amazon.com/redshift/latest/dg/declare.html) `  [FOR] ...  `
  - [`  PREPARE  `](https://docs.aws.amazon.com/redshift/latest/dg/r_PREPARE.html) `  plan_name [ (datatype [, ...] ) ] AS statement  `
  - [`  OPEN  `](https://docs.amazonaws.cn/en_us/redshift/latest/dg/c_PLpgSQL-statements.html#r_PLpgSQL-cursors) `  cursor_name FOR SELECT ...  `
  - [`  FETCH  `](https://docs.aws.amazon.com/redshift/latest/dg/fetch.html) `  [ NEXT | ALL | {FORWARD [ count | ALL ] } ] FROM cursor_name  `
  - [`  CLOSE  `](https://docs.aws.amazon.com/redshift/latest/dg/close.html) `  cursor_name;  `

If you're using the cursor to return a result set, you can achieve similar behavior using [temporary tables](/bigquery/docs/reference/standard-sql/data-definition-language#create_table_statement) in BigQuery.

### Dynamic SQL statements

The [scripting feature](/bigquery/docs/reference/standard-sql/scripting) in BigQuery supports dynamic SQL statements like those shown in the following table.

<table>
<thead>
<tr class="header">
<th><strong>Amazon Redshift</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         EXECUTE       </code></td>
<td><code dir="ltr" translate="no">         EXECUTE IMMEDIATE       </code></td>
</tr>
</tbody>
</table>

### Flow-of-control statements

<table>
<thead>
<tr class="header">
<th><strong>Amazon Redshift</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         IF..THEN..ELSIF..THEN..ELSE..END IF       </code></td>
<td><code dir="ltr" translate="no">         IF              condition              THEN stmts              ELSE stmts              END IF      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         name CURSOR [ ( arguments ) ] FOR query       </code></td>
<td>Cursors or sessions are not used in BigQuery.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       [&lt;               &gt;]                 LOOP                 statements                END LOOP [ label ];       </code></td>
<td><code dir="ltr" translate="no">         LOOP               sql_statement_list END LOOP;      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         WHILE condition LOOP stmts END LOOP       </code></td>
<td><code dir="ltr" translate="no">         WHILE              condition              DO stmts              END WHILE      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         EXIT       </code></td>
<td><code dir="ltr" translate="no">         BREAK       </code></td>
</tr>
</tbody>
</table>

## Consistency guarantees and transaction isolation

Both Amazon Redshift and BigQuery are atomic—that is, ACID-compliant on a per-mutation level across many rows.

### Transactions

Amazon Redshift supports [serializable isolation](https://docs.aws.amazon.com/redshift/latest/dg/r_BEGIN.html#r_BEGIN-synopsis) by default for transactions. Amazon Redshift lets you [specify](https://docs.aws.amazon.com/redshift/latest/dg/r_BEGIN.html#r_BEGIN-parameters) any of the four SQL standard transaction isolation levels but processes all isolation levels as serializable.

BigQuery also [supports transactions](/bigquery/docs/transactions) . BigQuery helps ensure [optimistic concurrency control](https://en.wikipedia.org/wiki/Optimistic_concurrency_control) (first to commit has priority) with [snapshot](https://en.wikipedia.org/wiki/Snapshot_isolation) [isolation](https://en.wikipedia.org/wiki/Snapshot_isolation) , in which a query reads the last committed data before the query starts. This approach guarantees the same level of consistency on a per-row, per-mutation basis and across rows within the same DML statement, yet avoids deadlocks. In the case of multiple DML updates against the same table, BigQuery switches to [pessimistic concurrency control](/bigquery/docs/data-manipulation-language#dml-limitations) . Load jobs can run completely independently and append to tables.

### Rollback

If Amazon Redshift encounters any error while running a stored procedure, it rolls back all changes made in a transaction. Additionally, you can use the `  ROLLBACK  ` transaction control statement in a stored procedure to discard all changes.

In BigQuery, you can use the [`  ROLLBACK TRANSACTION  ` statement](/bigquery/docs/reference/standard-sql/procedural-language#rollback_transaction) .

## Database limits

Check the [BigQuery public documentation](/bigquery/quotas) for the latest quotas and limits. Many quotas for large-volume users can be raised by contacting the Cloud support team. The following table shows a comparison of the Amazon Redshift and BigQuery database limits.

<table>
<thead>
<tr class="header">
<th><strong>Limit</strong></th>
<th><strong>Amazon Redshift</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Tables in each database for large and xlarge cluster node types</td>
<td>9,900</td>
<td>Unrestricted</td>
</tr>
<tr class="even">
<td>Tables in each database for 8xlarge cluster node types</td>
<td>20,000</td>
<td>Unrestricted</td>
</tr>
<tr class="odd">
<td>User-defined databases you can create for each cluster</td>
<td>60</td>
<td>Unrestricted</td>
</tr>
<tr class="even">
<td>Maximum row size</td>
<td>4 MB</td>
<td>100 MB</td>
</tr>
</tbody>
</table>
