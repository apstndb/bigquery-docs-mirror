# Snowflake SQL translation guide

This document details the similarities and differences in SQL syntax between Snowflake and BigQuery to help accelerate the planning and execution of moving your EDW (Enterprise Data Warehouse) to BigQuery. Snowflake data warehousing is designed to work with Snowflake-specific SQL syntax. Scripts written for Snowflake might need to be altered before you can use them in BigQuery, because the SQL dialects vary between the services. Use [batch SQL translation](/bigquery/docs/batch-sql-translator) to migrate your SQL scripts in bulk, or [interactive SQL translation](/bigquery/docs/interactive-sql-translator) to translate ad hoc queries. Snowflake SQL is supported by both tools in [preview](https://cloud.google.com/products#product-launch-stages) .

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
BigQuery supports <code dir="ltr" translate="no">       NUMERIC      </code> and <code dir="ltr" translate="no">       BIGNUMERIC      </code> with <a href="/bigquery/docs/reference/standard-sql/data-types#decimal_types">optionally specified precision and scale within certain bounds</a> .</td>
</tr>
<tr class="even">
<td><a href="https://docs.snowflake.com/en/sql-reference/data-types-numeric.html#int-integer-bigint-smallint-tinyint-byteint"><code dir="ltr" translate="no">        INT/INTEGER       </code></a></td>
<td><code dir="ltr" translate="no">         BIGNUMERIC       </code></td>
<td><code dir="ltr" translate="no">       INT/INTEGER      </code> and all other <code dir="ltr" translate="no">       INT      </code> -like datatypes, such as <code dir="ltr" translate="no">       BIGINT, TINYINT, SMALLINT, BYTEINT      </code> represent an alias for the <code dir="ltr" translate="no">       NUMBER      </code> datatype where the precision and scale cannot be specified and is always <code dir="ltr" translate="no">       NUMBER(38, 0)      </code><br />
<br />
The <a href="/bigquery/docs/config-yaml-translation#optimize_and_improve_the_performance_of_translated_sql"><code dir="ltr" translate="no">        REWRITE_ZERO_SCALE_NUMERIC_AS_INTEGER       </code> configuration option</a> can be used to instead convert <code dir="ltr" translate="no">       INTEGER      </code> and related types to <code dir="ltr" translate="no">       INT64      </code> .</td>
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
<td>The <code dir="ltr" translate="no">       VARCHAR      </code> data type in Snowflake has a maximum length of 16 MB (uncompressed). If length is not specified, the default is the maximum length.<br />
<br />
The <code dir="ltr" translate="no">       STRING      </code> data type in BigQuery is stored as variable length UTF-8 encoded Unicode. The maximum length is 16,000 characters.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         CHAR/CHARACTER       </code></td>
<td><code dir="ltr" translate="no">         STRING       </code></td>
<td>The <code dir="ltr" translate="no">       CHAR      </code> data type in Snowflake has a maximum length of 1.</td>
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
<td><code dir="ltr" translate="no">         DATETIME       </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         TIMESTAMP_TZ       </code></td>
<td><code dir="ltr" translate="no">         TIMESTAMP       </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         OBJECT       </code></td>
<td><code dir="ltr" translate="no">         JSON       </code></td>
<td>The <code dir="ltr" translate="no">       OBJECT      </code> type in Snowflake does not support explicitly-typed values. Values are of the <code dir="ltr" translate="no">       VARIANT      </code> type.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         VARIANT       </code></td>
<td><code dir="ltr" translate="no">         JSON       </code></td>
<td>The <code dir="ltr" translate="no">       OBJECT      </code> type in Snowflake does not support explicitly-typed values. Values are of the <code dir="ltr" translate="no">       VARIANT      </code> type.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         ARRAY       </code></td>
<td><code dir="ltr" translate="no">         ARRAY&lt;JSON&gt;       </code></td>
<td>The <code dir="ltr" translate="no">       ARRAY      </code> type in Snowflake can only support <code dir="ltr" translate="no">       VARIANT      </code> types, whereas the ARRAY type in <code dir="ltr" translate="no">       BigQuery      </code> can support all data types with the exception of an array itself.</td>
</tr>
</tbody>
</table>

BigQuery also has the following data types which do not have a direct Snowflake analogue:

  - [`  DATETIME  `](/bigquery/docs/reference/standard-sql/data-types#datetime_type)
  - [`  GEOGRAPHY  `](/bigquery/docs/reference/standard-sql/data-types#geography_type)

## Query syntax and query operators

This section addresses differences in query syntax between Snowflake and BigQuery.

### `     SELECT    ` statement

Most [Snowflake `  SELECT  ` statements](https://docs.snowflake.net/manuals/sql-reference/sql/select.html) are compatible with BigQuery. The following table contains a list of minor differences.

Snowflake

BigQuery

`  SELECT TOP ...  `

`  FROM table  `

`  SELECT expression  `

`  FROM table  `

`  ORDER BY expression DESC  `

`  LIMIT number  `

`  SELECT  `

`  x/total AS probability,  `

`  ROUND(100 * probability, 1) AS pct  `

`  FROM raw_data  `

  
Note: Snowflake supports creating and referencing an alias in the same `  SELECT  ` statement.

`  SELECT  `

`  x/total AS probability,  `

`  ROUND(100 * (x/total), 1) AS pct  `

`  FROM raw_data  `

`  SELECT * FROM (  `

`  VALUES (1), (2), (3)  `

`  )  `

`  SELECT AS VALUE STRUCT (1, 2, 3)  `

Snowflake aliases and identifiers are case-insensitive by default. To preserve case, enclose aliases and identifiers with double quotes (").

### `     FROM    ` clause

A [`  FROM  ` clause](https://docs.snowflake.net/manuals/sql-reference/constructs/from.html) in a query specifies the possible tables, views, subquery, or table functions to use in a SELECT statement. All of these table references are supported in BigQuery.

The following table contains a list of minor differences.

Snowflake

BigQuery

`  SELECT $1, $2 FROM ( VALUES (1, 'one'), (2, 'two'));  `

`  WITH table1 AS ( SELECT STRUCT(1 as number, 'one' as spelling) UNION ALL SELECT STRUCT(2 as number, 'two' as spelling) ) SELECT * FROM table1  `

`  SELECT* FROM table SAMPLE (10)  `

`  SELECT* FROM table  `

`  TABLESAMPLE  `

`  BERNOULLI (0.1 PERCENT)  `

`  SELECT * FROM table1 AT (TIMESTAMP => timestamp) SELECT * FROM table1 BEFORE (STATEMENT => statementID)  `

`  SELECT * FROM table  `

`  FOR SYSTEM_TIME AS OF timestamp  `

  
Note: BigQuery does not have a direct alternative to Snowflake's BEFORE using a statement ID. The value of *timestamp* cannot be more than 7 days before the current timestamp.

`  @[namespace]<stage_name>[/path]  `

BigQuery does not support the concept of staged files.

`  SELECT*  `

`  FROM table  `

`  START WITH predicate  `

`  CONNECT BY  `

`  [PRIOR] col1 = [PRIOR] col2  `

`  [, ...]  `

`  ...  `

BigQuery does not offer a direct alternative to Snowflake's `  CONNECT BY  ` .

BigQuery tables can be referenced in the `  FROM  ` clause using:

  - `  [project_id].[dataset_id].[table_name]  `
  - `  [dataset_id].[table_name]  `
  - `  [table_name]  `

BigQuery also supports [additional table references](/bigquery/docs/reference/standard-sql/query-syntax#from_clause) :

  - Historical versions of the table definition and rows using [`  FOR SYSTEM_TIME AS OF  `](/bigquery/docs/reference/standard-sql/query-syntax#sql_syntax)
  - Field paths, or any path that resolves to a field within a data type (that is, a `  STRUCT  ` )
  - [Flattened arrays](/bigquery/docs/arrays#querying_nested_arrays)

### `     WHERE    ` clause

The Snowflake [`  WHERE  `](https://docs.snowflake.net/manuals/sql-reference/constructs/where.html) clause and BigQuery [`  WHERE  `](/bigquery/docs/reference/standard-sql/query-syntax#where_clause) clause are identical, except for the following:

Snowflake

BigQuery

`  SELECT col1, col2 FROM table1, table2 WHERE col1 = col2(+)  `

`  SELECT col1, col2 FROM table1 INNER JOIN table2 ON col1 = col2  ` Note: BigQuery does not support the `  (+)  ` syntax for `  JOIN  ` s

### `     JOIN    ` types

Both Snowflake and BigQuery support the following types of join:

  - `  [INNER] JOIN  `
  - `  LEFT [OUTER] JOIN  `
  - `  RIGHT [OUTER] JOIN  `
  - `  FULL [OUTER] JOIN  `
  - `  CROSS JOIN  ` and the equivalent [implicit "comma cross join"](/bigquery/docs/reference/standard-sql/query-syntax#cross_join)

Both Snowflake and BigQuery support the `  ON  ` and `  USING  ` clause.

The following table contains a list of minor differences.

Snowflake

BigQuery

`  SELECT col1  `

`  FROM table1  `

`  NATURAL JOIN  `

`  table2  `

`  SELECT col1  `

`  FROM table1  `

`  INNER JOIN  `

`  table2  `

`  USING (col1, col2 [, ...])  `

  
Note: In BigQuery, `  JOIN  ` clauses require a JOIN condition unless it is a CROSS JOIN or one of the joined tables is a field within a data type or an array.

`  SELECT ... FROM table1 AS t1, LATERAL ( SELECT*  `

`  FROM table2 AS t2  `

`  WHERE t1.col = t2.col )  `

  
Note: Unlike the output of a non-lateral join, the output from a lateral join includes only the rows generated from the in-line view. The rows on the left-hand side do not need to be joined to the right hand side because the rows on the left-hand side have already been taken into account by being passed into the in-line view.

`  SELECT ... FROM table1 as t1 LEFT JOIN table2 as t2  `

`  ON t1.col = t2.col  `

Note: BigQuery does not support a direct alternative for `  LATERAL JOIN  ` s.

### `     WITH    ` clause

A [BigQuery `  WITH  ` clause](/bigquery/docs/reference/standard-sql/query-syntax#with_clause) contains one or more named subqueries which execute every time a subsequent `  SELECT  ` statement references them. [Snowflake `  WITH  `](https://docs.snowflake.net/manuals/sql-reference/constructs/with.html) clauses behave the same as BigQuery with the exception that BigQuery does not support `  WITH RECURSIVE  ` .

### `     GROUP BY    ` clause

Snowflake `  GROUP BY  ` clauses support [`  GROUP BY  `](https://docs.snowflake.net/manuals/sql-reference/constructs/group-by.html) , [`  GROUP BY ROLLUP  `](https://docs.snowflake.net/manuals/sql-reference/constructs/group-by-rollup.html) , [`  GROUP BY GROUPING SETS  `](https://docs.snowflake.net/manuals/sql-reference/constructs/group-by-grouping-sets.html) , and [`  GROUP BY CUBE  `](https://docs.snowflake.net/manuals/sql-reference/constructs/group-by-cube.html) , while BigQuery `  GROUP BY  ` clauses supports [`  GROUP BY  `](/bigquery/docs/reference/standard-sql/query-syntax#group_by_clause) , [`  GROUP BY ALL  `](/bigquery/docs/reference/standard-sql/query-syntax#group_by_all) , [`  GROUP BY ROLLUP  `](/bigquery/docs/reference/standard-sql/query-syntax#group_by_rollup) , [`  GROUP BY GROUPING SETS  `](/bigquery/docs/reference/standard-sql/query-syntax#group_by_grouping_sets) , and [`  GROUP BY CUBE  `](/bigquery/docs/reference/standard-sql/query-syntax#group_by_cube) .

Snowflake [`  HAVING  `](https://docs.snowflake.net/manuals/sql-reference/constructs/having.html) and BigQuery [`  HAVING  `](/bigquery/docs/reference/standard-sql/query-syntax#having_clause) are synonymous. Note that `  HAVING  ` occurs after `  GROUP BY  ` and aggregation, and before `  ORDER BY  ` .

Snowflake

BigQuery

`  SELECT col1 as one, col2 as two  `

`  FROM table GROUP BY (one, 2)  `

`  SELECT col1 as one, col2 as two  `

`  FROM table GROUP BY (one, 2)  `

`  SELECT col1 as one, col2 as two  `

`  FROM table GROUP BY ROLLUP (one, 2)  `

`  SELECT col1 as one, col2 as two  `

`  FROM table GROUP BY ROLLUP (one, 2)  `

`  SELECT col1 as one, col2 as two  `

`  FROM table GROUP BY GROUPING SETS (one, 2)  `

  
Note: Snowflake allows up to 128 grouping sets in the same query block

`  SELECT col1 as one, col2 as two  `

`  FROM table GROUP BY GROUPING SETS (one, 2)  `

`  SELECT col1 as one, col2 as two  `

`  FROM table GROUP BY CUBE (one,2)  `

  
Note: Snowflake allows up to 7 elements (128 grouping sets) in each cube

`  SELECT col1 as one, col2 as two  `

`  FROM table GROUP BY CUBE (one, 2)  `

### `     ORDER BY    ` clause

There are some minor differences between [Snowflake `  ORDER BY  ` clauses](https://docs.snowflake.net/manuals/sql-reference/constructs/order-by.html) and [BigQuery `  ORDER BY  `](/bigquery/docs/reference/standard-sql/query-syntax#order_by_clause) clauses.

Snowflake

BigQuery

In Snowflake, `  NULL  ` s are ranked last by default (ascending order).

In BigQuery, `  NULLS  ` are ranked first by default (ascending order).

You can specify whether `  NULL  ` values should be ordered first or last using `  NULLS FIRST  ` or `  NULLS LAST  ` , respectively.

There's no equivalent to specify whether `  NULL  ` values should be first or last in BigQuery.

### `     LIMIT/FETCH    ` clause

The [`  LIMIT/FETCH  `](https://docs.snowflake.net/manuals/sql-reference/constructs/limit.html) clause in Snowflake constrains the maximum number of rows returned by a statement or subquery. [`  LIMIT  `](https://docs.snowflake.net/manuals/sql-reference/constructs/limit.html) (Postgres syntax) and [`  FETCH  `](https://docs.snowflake.net/manuals/sql-reference/constructs/limit.html) (ANSI syntax) produce the same result.

In Snowflake and BigQuery, applying a `  LIMIT  ` clause to a query does not affect the amount of data that is read.

Snowflake

BigQuery

`  SELECT col1, col2  `

`  FROM table  `

`  ORDER BY col1  `

`  LIMIT count OFFSET start  `

  

`  SELECT ...  `

`  FROM ...  `

`  ORDER BY ...  `

`  OFFSET start {[ROW | ROWS]} FETCH {[FIRST | NEXT]} count  `

`  {[ROW | ROWS]} [ONLY]  `

  
Note: `  NULL  ` , empty string (''), and $$$$ values are accepted and are treated as "unlimited". Primary use is for connectors and drivers.

`  SELECT col1, col2  `

`  FROM table  `

`  ORDER BY col1  `

`  LIMIT count OFFSET start  `

  
Note: BigQuery does not support `  FETCH  ` . `  LIMIT  ` replaces `  FETCH  ` .  
  
Note: In BigQuery, `  OFFSET  ` must be used together with a `  LIMIT count  ` . Make sure to set the `  count  ` INT64 value to the minimum necessary ordered rows for best performance. Ordering all result rows unnecessarily will lead to worse query execution performance.

### `     QUALIFY    ` clause

The [`  QUALIFY  `](https://docs.snowflake.net/manuals/sql-reference/constructs/qualify.html) clause in Snowflake allows you to filter results for window functions similar to what `  HAVING  ` does with aggregate functions and `  GROUP BY  ` clauses.

Snowflake

BigQuery

`  SELECT col1, col2 FROM table QUALIFY ROW_NUMBER() OVER (PARTITION BY col1 ORDER BY col2) = 1;  `

The Snowflake `  QUALIFY  ` clause with an analytics function like `  ROW_NUMBER()  ` , `  COUNT()  ` , and with `  OVER PARTITION BY  ` is expressed in BigQuery as a [`  WHERE  `](/bigquery/docs/reference/standard-sql/query-syntax#where_clause) clause on a subquery that contains the analytics value.  
  
Using `  ROW_NUMBER ()  ` :  
  
`  SELECT col1, col2  `  

`  FROM ( SELECT col1, col2  `

`  ROW NUMBER() OVER (PARTITION BY col1 ORDER by col2) RN FROM table ) WHERE RN = 1;  `

  
Using `  ARRAY_AGG()  ` , which supports larger partitions:  
  

`  SELECT result.* FROM ( SELECT ARRAY_AGG(table ORDER BY table.col2 DESC LIMIT 1) [OFFSET(0)] FROM table  `

`  GROUP BY col1 ) AS result;  `

## Functions

The following sections list Snowflake functions and their BigQuery equivalents.

### Aggregate functions

The following table shows mappings between common Snowflake aggregate, aggregate analytic, and approximate aggregate functions with their BigQuery equivalents.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Snowflake</th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          ANY_VALUE                ([DISTINCT] expression) [OVER ...]       </code></p>
<br />
Note: <code dir="ltr" translate="no">       DISTINCT      </code> does not have any effect</td>
<td><p><code dir="ltr" translate="no">          ANY_VALUE                (expression) [OVER ...]       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          APPROX_COUNT_DISTINCT                ([DISTINCT] expression) [OVER ...]       </code></p>
<br />
Note: <code dir="ltr" translate="no">       DISTINCT      </code> does not have any effect</td>
<td><p><code dir="ltr" translate="no">          APPROX_COUNT_DISTINCT                (expression)       </code></p>
<br />
Note: BigQuery does not support <code dir="ltr" translate="no">       APPROX_COUNT_DISTINCT      </code> with Window Functions</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          APPROX_PERCENTILE                (expression, percentile) [OVER ...]       </code></p>
<br />
Note: Snowflake does not have the option to <code dir="ltr" translate="no">       RESPECT NULLS      </code></td>
<td><p><code dir="ltr" translate="no">          APPROX_QUANTILES                ([DISTINCT] expression,100) [OFFSET((CAST(TRUNC(percentile * 100) as INT64))]       </code></p>
<br />
Note: BigQuery does not support <code dir="ltr" translate="no">       APPROX_QUANTILES      </code> with Window Functions</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          APPROX_PERCENTILE_ACCUMULATE                (expression)       </code></p></td>
<td>BigQuery does not support the ability to store intermediate state when predicting approximate values.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          APPROX_PERCENTILE_COMBINE                (state)       </code></p></td>
<td>BigQuery does not support the ability to store intermediate state when predicting approximate values.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          APPROX_PERCENTILE_ESTIMATE                (state, percentile)       </code></p></td>
<td>BigQuery does not support the ability to store intermediate state when predicting approximate values.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          APPROX_TOP_K                (expression, [number [counters]]       </code></p>
<br />
Note: If no number parameter is specified, default is 1. Counters should be significantly larger than number.</td>
<td><p><code dir="ltr" translate="no">          APPROX_TOP_COUNT                (expression, number)       </code></p>
<br />
Note: BigQuery does not support <code dir="ltr" translate="no">       APPROX_TOP_COUNT      </code> with Window Functions.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          APPROX_TOP_K_ACCUMULATE                (expression, counters)       </code></p></td>
<td>BigQuery does not support the ability to store intermediate state when predicting approximate values.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          APPROX_TOP_K_COMBINE                (state, [counters])       </code></p></td>
<td>BigQuery does not support the ability to store intermediate state when predicting approximate values.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          APPROX_TOP_K_ESTIMATE                (state, [k])       </code></p></td>
<td>BigQuery does not support the ability to store intermediate state when predicting approximate values.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          APPROXIMATE_JACCARD_INDEX                ([DISTINCT] expression)       </code></p></td>
<td><br />
You can use a custom UDF to implement <code dir="ltr" translate="no">       MINHASH      </code> with <code dir="ltr" translate="no">       k      </code> distinct hash functions. Another approach to reduce the variance in <code dir="ltr" translate="no">       MINHASH      </code> is to keep<br />
<code dir="ltr" translate="no">       k      </code> of the minimum values of one hash function. In this case Jaccard index can be approximated as following:<br />

<p><code dir="ltr" translate="no">        WITH       </code></p>
<p><code dir="ltr" translate="no">        minhash_A AS (       </code></p>
<p><code dir="ltr" translate="no">        SELECT DISTINCT                 FARM_FINGERPRINT(TO_JSON_STRING                (t)) AS h       </code></p>
<p><code dir="ltr" translate="no">        FROM TA AS t       </code></p>
<p><code dir="ltr" translate="no">        ORDER BY h       </code></p>
<p><code dir="ltr" translate="no">        LIMIT k),       </code></p>
<p><code dir="ltr" translate="no">        minhash_B AS (       </code></p>
<p><code dir="ltr" translate="no">        SELECT DISTINCT                 FARM_FINGERPRINT(TO_JSON_STRING                (t)) AS h       </code></p>
<p><code dir="ltr" translate="no">        FROM TB AS t       </code></p>
<p><code dir="ltr" translate="no">        ORDER BY h       </code></p>
<p><code dir="ltr" translate="no">        LIMIT k)       </code></p>
<p><code dir="ltr" translate="no">        SELECT       </code></p>
<p><code dir="ltr" translate="no">        COUNT(*) / k AS APPROXIMATE_JACCARD_INDEX       </code></p>
<p><code dir="ltr" translate="no">        FROM minhash_A       </code></p>
<p><code dir="ltr" translate="no">        INNER JOIN minhash_B       </code></p>
<p><code dir="ltr" translate="no">        ON minhash_A.h = minhash_B.h       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          APPROXIMATE_SIMILARITY                ([DISTINCT] expression)       </code></p></td>
<td><br />
It is a synonym for <code dir="ltr" translate="no">         APPROXIMATE_JACCARD_INDEX       </code> and can be implemented in the same way.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          ARRAY_AGG                ([DISTINCT] expression1) [WITHIN GROUP (ORDER BY ...)]       </code></p>
<p><code dir="ltr" translate="no">        [OVER ([PARTITION BY expression2])]       </code></p>
<p><code dir="ltr" translate="no">        Note: Snowflake does not support ability to IGNORE|RESPECT NULLS and to LIMIT directly in ARRAY_AGG.       </code></p></td>
<td><p><code dir="ltr" translate="no">          ARRAY_AGG                ([DISTINCT] expression1       </code></p>
<p><code dir="ltr" translate="no">        [{IGNORE|RESPECT}] NULLS] [ORDER BY ...] LIMIT ...])       </code></p>
<p><code dir="ltr" translate="no">        [OVER (...)]       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          AVG                ([DISTINCT] expression) [OVER ...]       </code></p></td>
<td><p><code dir="ltr" translate="no">          AVG                ([DISTINCT] expression) [OVER ...]       </code></p>
<br />
Note: BigQuery's <code dir="ltr" translate="no">       AVG      </code> does not perform automatic casting on <code dir="ltr" translate="no">       STRING      </code> s.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          BITAND_AGG                (expression)       </code></p>
<p><code dir="ltr" translate="no">        [OVER ...]       </code></p></td>
<td><p><code dir="ltr" translate="no">          BIT_AND                (expression) [OVER ...]       </code></p>
Note: BigQuery does not implicitly cast character/text columns to the nearest <code dir="ltr" translate="no">       INTEGER      </code> .</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          BITOR_AGG                (expression)       </code></p>
<p><code dir="ltr" translate="no">        [OVER ...]       </code></p></td>
<td><p><code dir="ltr" translate="no">          BIT_OR                (expression)       </code></p>
<p><code dir="ltr" translate="no">        [OVER ...]       </code></p>
<br />
Note: BigQuery does not implicitly cast character/text columns to the nearest <code dir="ltr" translate="no">       INTEGER      </code> .</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          BITXOR_AGG                ([DISTINCT] expression) [OVER ...]       </code></p></td>
<td><p><code dir="ltr" translate="no">          BIT_XOR                ([DISTINCT] expression) [OVER ...]       </code></p>
<br />
Note: BigQuery does not implicitly cast character/text columns to the nearest <code dir="ltr" translate="no">       INTEGER      </code> .</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          BOOLAND_AGG                (expression) [OVER ...]       </code></p>
<br />
Note: Snowflake allows numeric, decimal, and floating point values to be treated as <code dir="ltr" translate="no">       TRUE      </code> if not zero.</td>
<td><p><code dir="ltr" translate="no">          LOGICAL_AND                (expression)       </code></p>
<p><code dir="ltr" translate="no">        [OVER ...]       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          BOOLOR_AGG                (expression)       </code></p>
<p><code dir="ltr" translate="no">        [OVER ...]       </code></p>
<br />
Note: Snowflake allows numeric, decimal, and floating point values to be treated as <code dir="ltr" translate="no">       TRUE      </code> if not zero.</td>
<td><p><code dir="ltr" translate="no">          LOGICAL_OR                (expression)       </code></p>
<p><code dir="ltr" translate="no">        [OVER ...]       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          BOOLXOR_AGG                (expression)       </code></p>
<p><code dir="ltr" translate="no">        [OVER ([PARTITION BY &lt;partition_expr&gt; ])       </code></p>
<br />
Note: Snowflake allows numeric, decimal, and floating point values to be treated as <code dir="ltr" translate="no">       TRUE      </code> if not zero.</td>
<td>For numeric expression:<br />

<p><code dir="ltr" translate="no">        SELECT       </code></p>
<p><code dir="ltr" translate="no">        CASE                 COUNT                (*)       </code></p>
<p><code dir="ltr" translate="no">        WHEN 1 THEN TRUE       </code></p>
<p><code dir="ltr" translate="no">        WHEN 0 THEN NULL       </code></p>
<p><code dir="ltr" translate="no">        ELSE FALSE       </code></p>
<p><code dir="ltr" translate="no">        END AS BOOLXOR_AGG       </code></p>
<p><code dir="ltr" translate="no">        FROM T       </code></p>
<p><code dir="ltr" translate="no">        WHERE expression != 0       </code></p>
<br />
To use <code dir="ltr" translate="no">       OVER      </code> you can run the following (boolean example provided):<br />

<p><code dir="ltr" translate="no">        SELECT       </code></p>
<p><code dir="ltr" translate="no">        CASE COUNT(expression) OVER (PARTITION BY partition_expr)       </code></p>
<p><code dir="ltr" translate="no">        WHEN 0 THEN NULL       </code></p>
<p><code dir="ltr" translate="no">        ELSE       </code></p>
<p><code dir="ltr" translate="no">        CASE COUNT(       </code></p>
<p><code dir="ltr" translate="no">        CASE expression       </code></p>
<p><code dir="ltr" translate="no">        WHEN TRUE THEN 1       </code></p>
<p><code dir="ltr" translate="no">        END) OVER (PARTITION BY partition_expr)       </code></p>
<p><code dir="ltr" translate="no">        WHEN 1 THEN TRUE       </code></p>
<p><code dir="ltr" translate="no">        ELSE FALSE       </code></p>
<p><code dir="ltr" translate="no">        END       </code></p>
<p><code dir="ltr" translate="no">        END AS BOOLXOR_AGG       </code></p>
<p><code dir="ltr" translate="no">        FROM T       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          CORR                (dependent, independent)       </code></p>
<p><code dir="ltr" translate="no">        [OVER ...]       </code></p></td>
<td><p><code dir="ltr" translate="no">          CORR                (dependent, independent)       </code></p>
<p><code dir="ltr" translate="no">        [OVER ...]       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          COUNT                ([DISTINCT] expression [,expression2]) [OVER ...]       </code></p></td>
<td><p><code dir="ltr" translate="no">          COUNT                ([DISTINCT] expression [,expression2]) [OVER ...]       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          COVAR_POP                (dependent, independent) [OVER ...]       </code></p></td>
<td><p><code dir="ltr" translate="no">          COVAR_POP                (dependent, independent) [OVER ...]       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          COVAR_SAMP                (dependent, independent)       </code></p>
<p><code dir="ltr" translate="no">        [OVER ...]       </code></p></td>
<td><p><code dir="ltr" translate="no">          COVAR_SAMP                (dependent, independent)       </code></p>
<p><code dir="ltr" translate="no">        [OVER ...]       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          GROUPING                (expression1, [,expression2...])       </code></p></td>
<td>BigQuery does not support a direct alternative to Snowflake's <code dir="ltr" translate="no">       GROUPING      </code> . Available through a User-Defined Function.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          GROUPING_ID                (expression1, [,expression2...])       </code></p></td>
<td>BigQuery does not support a direct alternative to Snowflake's <code dir="ltr" translate="no">       GROUPING_ID      </code> . Available through a User-Defined Function.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          HASH_AGG                ([DISTINCT] expression1, [,expression2])       </code></p>
<p><code dir="ltr" translate="no">        [OVER ...]       </code></p></td>
<td>SELECT<br />
<code dir="ltr" translate="no">         BIT_XOR              (      </code><br />
<code dir="ltr" translate="no">         FARM_FINGERPRINT              (      </code><br />
<code dir="ltr" translate="no">         TO_JSON_STRING              (t))) [OVER]      </code><br />
FROM t</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        SELECT                 HLL                ([DISTINCT] expression1, [,expression2])       </code></p>
<p><code dir="ltr" translate="no">        [OVER  ...]       </code></p>
<br />
Note: Snowflake does not allow you to specify precision.</td>
<td><p><code dir="ltr" translate="no">        SELECT                 HLL_COUNT.EXTRACT                (sketch) FROM (       </code></p>
<p><code dir="ltr" translate="no">        SELECT                 HLL_COUNT.INIT                (expression)       </code></p>
<p><code dir="ltr" translate="no">        AS  sketch     FROM table )       </code></p>
<br />
Note: BigQuery does not support <code dir="ltr" translate="no">       HLL_COUNT…      </code> with Window Functions. A user cannot include multiple expressions in a single <code dir="ltr" translate="no">       HLL_COUNT...      </code> function.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          HLL_ACCUMULATE                ([DISTINCT] expression)       </code></p>
<br />
Note: Snowflake does not allow you to specify precision.</td>
<td><code dir="ltr" translate="no">         HLL_COUNT.INIT       </code> (expression [, precision])</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          HLL_COMBINE                ([DISTINCT] state)       </code></p></td>
<td><code dir="ltr" translate="no">         HLL_COUNT.MERGE_PARTIAL       </code> (sketch)</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          HLL_ESTIMATE                (state)       </code></p></td>
<td><p><code dir="ltr" translate="no">          HLL_COUNT.EXTRACT                (sketch)       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          HLL_EXPORT                (binary)       </code></p></td>
<td>BigQuery does not support a direct alternative to Snowflake's <code dir="ltr" translate="no">       HLL_EXPORT      </code> .</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          HLL_IMPORT                (object)       </code></p></td>
<td>BigQuery does not support a direct alternative to Snowflake's <code dir="ltr" translate="no">       HLL_IMPORT      </code> .</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          KURTOSIS                (expression)       </code></p>
<p><code dir="ltr" translate="no">        [OVER ...]       </code></p></td>
<td>BigQuery does not support a direct alternative to Snowflake's <code dir="ltr" translate="no">       KURTOSIS      </code> .</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          LISTAGG                (       </code></p>
<p><code dir="ltr" translate="no">        [DISTINCT] aggregate_expression       </code></p>
<p><code dir="ltr" translate="no">        [, delimiter]       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p>
<p><code dir="ltr" translate="no">        [OVER ...]       </code></p></td>
<td><p><code dir="ltr" translate="no">          STRING_AGG                (       </code></p>
<p><code dir="ltr" translate="no">        [DISTINCT] aggregate_expression       </code></p>
<p><code dir="ltr" translate="no">        [, delimiter]       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p>
<p><code dir="ltr" translate="no">        [OVER ...]       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          MEDIAN                (expression) [OVER ...]       </code></p>
<br />
Note: Snowflake does not support ability to <code dir="ltr" translate="no">       IGNORE|RESPECT NULLS      </code> and to <code dir="ltr" translate="no">       LIMIT      </code> directly in <code dir="ltr" translate="no">       ARRAY_AGG.      </code></td>
<td><p><code dir="ltr" translate="no">          PERCENTILE_CONT                (       </code></p>
<p><code dir="ltr" translate="no">        value_expression,       </code></p>
<p><code dir="ltr" translate="no">        0.5       </code></p>
[ {RESPECT | IGNORE} NULLS]<br />

<p><code dir="ltr" translate="no">        ) OVER()       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          MAX                (expression) [OVER ...]       </code></p>
<br />

<p><code dir="ltr" translate="no">          MIN                (expression) [OVER ...]       </code></p></td>
<td><p><code dir="ltr" translate="no">          MAX                (expression) [OVER ...]       </code></p>
<br />

<p><code dir="ltr" translate="no">          MIN                (expression) [OVER ...]       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          MINHASH                (k, [DISTINCT] expressions)       </code></p></td>
<td>You can use a custom UDF to implement <code dir="ltr" translate="no">       MINHASH      </code> with <code dir="ltr" translate="no">       k      </code> distinct hash functions. Another approach to reduce the variance in <code dir="ltr" translate="no">       MINHASH      </code> is to keep <code dir="ltr" translate="no">       k      </code> of the minimum values of one hash function: <code dir="ltr" translate="no">       SELECT DISTINCT      </code><br />
<code dir="ltr" translate="no">         FARM_FINGERPRINT              (      </code><br />
<code dir="ltr" translate="no">         TO_JSON_STRING              (t)) AS MINHASH      </code><br />

<p><code dir="ltr" translate="no">        FROM t       </code></p>
<p><code dir="ltr" translate="no">        ORDER BY MINHASH       </code></p>
<p><code dir="ltr" translate="no">        LIMIT k       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          MINHASH_COMBINE                ([DISTINCT] state)       </code></p></td>
<td><code>         FROM (   SELECT DISTINCT      FARM_FINGERPRINT(       TO_JSON_STRING(t)) AS h   FROM TA AS t   ORDER BY h   LIMIT k   UNION   SELECT DISTINCT      FARM_FINGERPRINT(       TO_JSON_STRING(t)) AS h   FROM TB AS t   ORDER BY h   LIMIT k )   ORDER BY h LIMIT k       </code></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          MODE                (expr1)       </code></p>
<p><code dir="ltr" translate="no">        OVER ( [ PARTITION BY &lt;expr2&gt; ] )       </code></p></td>
<td><p><code dir="ltr" translate="no">        SELECT expr1       </code></p>
<p><code dir="ltr" translate="no">        FROM (       </code></p>
<p><code dir="ltr" translate="no">        SELECT       </code></p>
<p><code dir="ltr" translate="no">        expr1,       </code></p>
<p><code dir="ltr" translate="no">          ROW_NUMBER                () OVER (       </code></p>
<p><code dir="ltr" translate="no">        PARTITION BY expr2       </code></p>
<p><code dir="ltr" translate="no">        ORDER BY cnt DESC) rn       </code></p>
<p><code dir="ltr" translate="no">        FROM (       </code></p>
<p><code dir="ltr" translate="no">        SELECT       </code></p>
<p><code dir="ltr" translate="no">        expr1,       </code></p>
<p><code dir="ltr" translate="no">        expr2,       </code></p>
<p><code dir="ltr" translate="no">          COUNTIF                (expr1 IS NOT NULL) OVER       </code></p>
<p><code dir="ltr" translate="no">        (PARTITION BY expr2, expr1) cnt       </code></p>
<p><code dir="ltr" translate="no">        FROM t))       </code></p>
<p><code dir="ltr" translate="no">        WHERE rn = 1       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          OBJECT_AGG                (key, value) [OVER ...]       </code></p></td>
<td>You may consider using <a href="/bigquery/docs/reference/standard-sql/json_functions#to_json_string"><code dir="ltr" translate="no">        TO_JSON_STRING       </code></a> to convert a value into JSON-formatted string</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          PERCENTILE_CONT                (percentile) WITHIN GROUP (ORDER BY value_expression)       </code></p>
<p><code dir="ltr" translate="no">        [OVER ...]       </code></p></td>
<td><p><code dir="ltr" translate="no">          PERCENTILE_CONT                (       </code></p>
<p><code dir="ltr" translate="no">        value_expression,       </code></p>
<p><code dir="ltr" translate="no">        percentile       </code></p>
[ {RESPECT | IGNORE} NULLS]<br />

<p><code dir="ltr" translate="no">        ) OVER()       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          PERCENTILE_DISC                (percentile) WITHIN GROUP (ORDER BY value_expression)       </code></p>
<p><code dir="ltr" translate="no">        [OVER ...]       </code></p></td>
<td><p><code dir="ltr" translate="no">          PERCENTILE_DISC                (       </code></p>
<p><code dir="ltr" translate="no">        value_expression,       </code></p>
<p><code dir="ltr" translate="no">        percentile       </code></p>
[ {RESPECT | IGNORE} NULLS]<br />

<p><code dir="ltr" translate="no">        ) OVER()       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          REGR_AVGX                (dependent, independent)       </code></p>
<p><code dir="ltr" translate="no">        [OVER ...]       </code></p></td>
<td><p><code dir="ltr" translate="no">        SELECT                 AVG                (independent) [OVER ...]       </code></p>
<p><code dir="ltr" translate="no">        FROM table       </code></p>
<p><code dir="ltr" translate="no">        WHERE (       </code></p>
<p><code dir="ltr" translate="no">        (dependent IS NOT NULL) AND       </code></p>
<p><code dir="ltr" translate="no">        (independent IS NOT NULL)       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          REGR_AVGY                (dependent, independent)       </code></p>
<p><code dir="ltr" translate="no">        [OVER ...]       </code></p></td>
<td><p><code dir="ltr" translate="no">        SELECT                 AVG                (dependent) [OVER ...]       </code></p>
<p><code dir="ltr" translate="no">        FROM table       </code></p>
<p><code dir="ltr" translate="no">        WHERE (       </code></p>
<p><code dir="ltr" translate="no">        (dependent IS NOT NULL) AND       </code></p>
<p><code dir="ltr" translate="no">        (independent IS NOT NULL)       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          REGR_COUNT                (dependent, independent)       </code></p>
<p><code dir="ltr" translate="no">        [OVER ...]       </code></p></td>
<td><p><code dir="ltr" translate="no">        SELECT                 COUNT                (*) [OVER ...]       </code></p>
<p><code dir="ltr" translate="no">        FROM table       </code></p>
<p><code dir="ltr" translate="no">        WHERE (       </code></p>
<p><code dir="ltr" translate="no">        (dependent IS NOT NULL) AND       </code></p>
<p><code dir="ltr" translate="no">        (independent IS NOT NULL)       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          REGR_INTERCEPT                (dependent, independent)       </code></p>
<p><code dir="ltr" translate="no">        [OVER ...]       </code></p></td>
<td><p><code dir="ltr" translate="no">        SELECT       </code></p>
<p><code dir="ltr" translate="no">          AVG                (dependent) -       </code></p>
<p><code dir="ltr" translate="no">          COVAR_POP                (dependent,independent)/       </code></p>
<p><code dir="ltr" translate="no">          VAR_POP                (dependent) *       </code></p>
<p><code dir="ltr" translate="no">          AVG                (independent)       </code></p>
<p><code dir="ltr" translate="no">        [OVER ...]       </code></p>
<p><code dir="ltr" translate="no">        FROM table       </code></p>
<p><code dir="ltr" translate="no">        WHERE (       </code></p>
<p><code dir="ltr" translate="no">        (dependent IS NOT NULL) AND       </code></p>
<p><code dir="ltr" translate="no">        (independent IS NOT NULL)       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p>
<p><code dir="ltr" translate="no">        [GROUP BY ...]       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          REGR_R2                (dependent, independent)       </code></p>
<p><code dir="ltr" translate="no">        [OVER ...]       </code></p></td>
<td><p><code dir="ltr" translate="no">        SELECT       </code></p>
<p><code dir="ltr" translate="no">        CASE       </code></p>
<p><code dir="ltr" translate="no">        WHEN                 VAR_POP                (independent) = 0       </code></p>
<p><code dir="ltr" translate="no">        THEN NULL       </code></p>
<p><code dir="ltr" translate="no">        WHEN VAR_POP(dependent) = 0 AND VAR_POP(independent) != 0       </code></p>
<p><code dir="ltr" translate="no">        THEN 1       </code></p>
<p><code dir="ltr" translate="no">        ELSE                 POWER                (                 CORR                (dependent, independent), 2)       </code></p>
<p><code dir="ltr" translate="no">        END AS ...       </code></p>
<p><code dir="ltr" translate="no">        FROM table       </code></p>
<p><code dir="ltr" translate="no">        WHERE (       </code></p>
<p><code dir="ltr" translate="no">        (dependent IS NOT NULL) AND       </code></p>
<p><code dir="ltr" translate="no">        (independent IS NOT NULL)       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p>
<p><code dir="ltr" translate="no">        [GROUP BY ...]       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          REGR_SLOPE                (dependent, independent)       </code></p>
<p><code dir="ltr" translate="no">        [OVER ...]       </code></p></td>
<td><p><code dir="ltr" translate="no">        SELECT       </code></p>
<p><code dir="ltr" translate="no">          COVAR_POP                (dependent,independent)/       </code></p>
<p><code dir="ltr" translate="no">          VAR_POP                (dependent)       </code></p>
<p><code dir="ltr" translate="no">        [OVER ...]       </code></p>
<p><code dir="ltr" translate="no">        FROM table       </code></p>
<p><code dir="ltr" translate="no">        WHERE (       </code></p>
<p><code dir="ltr" translate="no">        (dependent IS NOT NULL) AND       </code></p>
<p><code dir="ltr" translate="no">        (independent IS NOT NULL)       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p>
<p><code dir="ltr" translate="no">        [GROUP BY ...]       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          REGR_SXX                (dependent, independent)       </code></p>
<p><code dir="ltr" translate="no">        [OVER ...]       </code></p></td>
<td><p><code dir="ltr" translate="no">        SELECT                 COUNT                (*)*                 VAR_POP                (independent)       </code></p>
<p><code dir="ltr" translate="no">        [OVER ...]       </code></p>
<p><code dir="ltr" translate="no">        FROM table       </code></p>
<p><code dir="ltr" translate="no">        WHERE (       </code></p>
<p><code dir="ltr" translate="no">        (dependent IS NOT NULL) AND       </code></p>
<p><code dir="ltr" translate="no">        (independent IS NOT NULL)       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p>
<p><code dir="ltr" translate="no">        [GROUP BY ...]       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          REGR_SYY                (dependent, independent)       </code></p>
<p><code dir="ltr" translate="no">        [OVER ...]       </code></p></td>
<td><p><code dir="ltr" translate="no">        SELECT                 COUNT                (*)*                 VAR_POP                (dependent)       </code></p>
<p><code dir="ltr" translate="no">        [OVER ...]       </code></p>
<p><code dir="ltr" translate="no">        FROM table       </code></p>
<p><code dir="ltr" translate="no">        WHERE (       </code></p>
<p><code dir="ltr" translate="no">        (dependent IS NOT NULL) AND       </code></p>
<p><code dir="ltr" translate="no">        (independent IS NOT NULL)       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p>
<p><code dir="ltr" translate="no">        [GROUP BY ...]       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          SKEW                (expression)       </code></p></td>
<td>BigQuery does not support a direct alternative to Snowflake's <code dir="ltr" translate="no">       SKEW      </code> .</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          STDDEV                ([DISTINCT] expression)       </code></p>
<p><code dir="ltr" translate="no">        [OVER ...]       </code></p></td>
<td><p><code dir="ltr" translate="no">          STDDEV                ([DISTINCT] expression)       </code></p>
<p><code dir="ltr" translate="no">        [OVER ...]       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          STDDEV_POP                ([DISTINCT] expression)       </code></p>
<p><code dir="ltr" translate="no">        [OVER ...]       </code></p></td>
<td><p><code dir="ltr" translate="no">          STDDEV_POP                ([DISTINCT] expression)       </code></p>
<p><code dir="ltr" translate="no">        [OVER ...]       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          STDDEV_SAMP                ([DISTINCT] expression)       </code></p>
<p><code dir="ltr" translate="no">        [OVER ...]       </code></p></td>
<td><p><code dir="ltr" translate="no">          STDDEV_SAMP                ([DISTINCT] expression)       </code></p>
<p><code dir="ltr" translate="no">        [OVER ...]       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          SUM                ([DISTINCT] expression)       </code></p>
<p><code dir="ltr" translate="no">        [OVER ...]       </code></p></td>
<td><p><code dir="ltr" translate="no">          SUM                ([DISTINCT] expression)       </code></p>
<p><code dir="ltr" translate="no">        [OVER ...]       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          VAR_POP                ([DISTINCT] expression)       </code></p>
<p><code dir="ltr" translate="no">        [OVER ...]       </code></p>
<br />
Note: Snowflake supports the ability to cast <code dir="ltr" translate="no">       VARCHAR      </code> s to floating point values.</td>
<td><p><code dir="ltr" translate="no">          VAR_POP                ([DISTINCT] expression)       </code></p>
<p><code dir="ltr" translate="no">        [OVER ...]       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          VARIANCE_POP                ([DISTINCT] expression)       </code></p>
<p><code dir="ltr" translate="no">        [OVER ...]       </code></p>
<br />
Note: Snowflake supports the ability to cast <code dir="ltr" translate="no">       VARCHAR      </code> s to floating point values.</td>
<td><p><code dir="ltr" translate="no">          VAR_POP                ([DISTINCT] expression)       </code></p>
<p><code dir="ltr" translate="no">        [OVER ...]       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          VAR_SAMP                ([DISTINCT] expression)       </code></p>
<p><code dir="ltr" translate="no">        [OVER ...]       </code></p>
<br />
Note: Snowflake supports the ability to cast <code dir="ltr" translate="no">       VARCHAR      </code> s to floating point values.</td>
<td><p><code dir="ltr" translate="no">          VAR_SAMP                ([DISTINCT] expression)       </code></p>
<p><code dir="ltr" translate="no">        [OVER ...]       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          VARIANCE                ([DISTINCT] expression)       </code></p>
<p><code dir="ltr" translate="no">        [OVER ...]       </code></p>
<br />
Note: Snowflake supports the ability to cast <code dir="ltr" translate="no">       VARCHAR      </code> s to floating point values.</td>
<td><p><code dir="ltr" translate="no">          VARIANCE                ([DISTINCT] expression)       </code></p>
<p><code dir="ltr" translate="no">        [OVER ...]       </code></p></td>
</tr>
</tbody>
</table>

BigQuery also offers the following [aggregate](/bigquery/docs/reference/standard-sql/aggregate_functions) , [aggregate analytic](/bigquery/docs/reference/standard-sql/aggregate_analytic_functions) , and [approximate aggregate](/bigquery/docs/reference/standard-sql/approximate_aggregate_functions) functions, which do not have a direct analogue in Snowflake:

  - [`  COUNTIF  `](/bigquery/docs/reference/standard-sql/aggregate_functions#countif)
  - [`  ARRAY_CONCAT_AGG  `](/bigquery/docs/reference/standard-sql/aggregate_functions#array_concat_agg)
  - [`  HLL_COUNT.MERGE  `](/bigquery/docs/reference/standard-sql/hll_functions#hll_countmerge)

### Bitwise expression functions

The following table shows mappings between common Snowflake bitwise expression functions with their BigQuery equivalents.

If the data type of an expression is not `  INTEGER  ` , Snowflake attempts to cast to `  INTEGER  ` . However, BigQuery does not attempt to cast to `  INTEGER  ` .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Snowflake</th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          BITAND                (expression1, expression2)       </code></p></td>
<td><p><code dir="ltr" translate="no">          BIT_AND                (x) FROM UNNEST([expression1, expression2]) AS x  expression1 &amp; expression2       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          BITNOT                (expression)       </code></p></td>
<td><p><code dir="ltr" translate="no">          ~                expression       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          BITOR                (expression1, expression2)       </code></p></td>
<td><p><code dir="ltr" translate="no">          BIT_OR                (x) FROM UNNEST([expression1, expression2]) AS x       </code></p>
<br />

<p><code dir="ltr" translate="no">        expression1                 |                expression2       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          BITSHIFTLEFT                (expression, n)       </code></p></td>
<td><p><code dir="ltr" translate="no">        expression                 &lt;&lt;                n       </code></p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         BITSHIFTRIGHT       </code><br />

<p><code dir="ltr" translate="no">        (expression, n)       </code></p></td>
<td><p><code dir="ltr" translate="no">        expression                 &gt;&gt;                n       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          BITXOR                (expression, expression)       </code></p>
<br />
Note: Snowflake does not support <code dir="ltr" translate="no">       DISTINCT.      </code></td>
<td><p><code dir="ltr" translate="no">          BIT_XOR                ([DISTINCT] x) FROM UNNEST([expression1, expression2]) AS x       </code></p>
<br />

<p><code dir="ltr" translate="no">        expression ^ expression       </code></p></td>
</tr>
</tbody>
</table>

### Conditional expression functions

The following table shows mappings between common Snowflake conditional expressions with their BigQuery equivalents.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Snowflake</th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        expression                 [ NOT ] BETWEEN                lower AND upper       </code></p></td>
<td><p><code dir="ltr" translate="no">        (expression                 &gt;=                lower AND expression &lt;= upper)       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          BOOLAND                (expression1, expression2)       </code></p>
<br />
Note: Snowflake allows numeric, decimal, and floating point values to be treated as <code dir="ltr" translate="no">       TRUE      </code> if not zero.</td>
<td><p><code dir="ltr" translate="no">          LOGICAL_AND                (x)       </code></p>
<p><code dir="ltr" translate="no">        FROM UNNEST([expression1, expression2]) AS x       </code></p>
<br />

<p><code dir="ltr" translate="no">        expression1                 AND                expression2       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          BOOLNOT                (expression1)       </code></p>
<br />
Note: Snowflake allows numeric, decimal, and floating point values to be treated as <code dir="ltr" translate="no">       TRUE      </code> if not zero.</td>
<td><p><code dir="ltr" translate="no">          NOT                expression       </code></p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         BOOLOR       </code><br />
<br />
Note: Snowflake allows numeric, decimal, and floating point values to be treated as <code dir="ltr" translate="no">       TRUE      </code> if not zero.</td>
<td><p><code dir="ltr" translate="no">          LOGICAL_OR                (x) FROM UNNEST([expression1, expression2]) AS x       </code></p>
<br />

<p><code dir="ltr" translate="no">        expression1                 OR                expression2       </code></p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         BOOLXOR       </code><br />
<br />
Note: Snowflake allows numeric, decimal, and floating point values to be treated as <code dir="ltr" translate="no">       TRUE      </code> if not zero.</td>
<td>BigQuery does not support a direct alternative to Snowflake's <code dir="ltr" translate="no">       BOOLXOR.      </code></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          CASE                [expression]     WHEN condition1 THEN result1     [WHEN condition2 THEN result2]       </code></p>
<p><code dir="ltr" translate="no">        [...]       </code></p>
<p><code dir="ltr" translate="no">        [ELSE result3]       </code></p>
<p><code dir="ltr" translate="no">        END       </code></p></td>
<td><p><code dir="ltr" translate="no">          CASE                [expression]     WHEN condition1 THEN result1     [WHEN condition2 THEN result2]       </code></p>
<p><code dir="ltr" translate="no">        [...]       </code></p>
<p><code dir="ltr" translate="no">        [ELSE result3]       </code></p>
<p><code dir="ltr" translate="no">        END       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          COALESCE                (expr1, expr2, [,...])       </code></p>
<br />
Note: Snowflake requires at least two expressions. BigQuery only requires one.</td>
<td><p><code dir="ltr" translate="no">          COALESCE                (expr1, [,...])       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          DECODE                (expression, search1, result1, [search2, result2...] [,default])       </code></p></td>
<td><p><code dir="ltr" translate="no">          CASE                [expression]     WHEN condition1 THEN result1     [WHEN condition2 THEN result2]       </code></p>
<p><code dir="ltr" translate="no">        [...]       </code></p>
<p><code dir="ltr" translate="no">        [ELSE result3]       </code></p>
<p><code dir="ltr" translate="no">        END       </code></p>
Note: BigQuery supports subqueries in condition statements. This can be used to reproduce Snowflake's <code dir="ltr" translate="no">       DECODE      </code> . User must use <code dir="ltr" translate="no">       IS NULL      </code> instead of <code dir="ltr" translate="no">       = NULL      </code> to match <code dir="ltr" translate="no">       NULL      </code> select expressions with <code dir="ltr" translate="no">       NULL      </code> search expressions.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          EQUAL_NULL                (expression1, expression2)       </code></p></td>
<td>BigQuery does not support a direct alternative to Snowflake's <code dir="ltr" translate="no">       EQUAL_NULL.      </code></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          GREATEST                (expression1, [,expression2]...)       </code></p></td>
<td><p><code dir="ltr" translate="no">          GREATEST                (expression1, [,expression2]...)       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          IFF                (condition, true_result, false_result)       </code></p></td>
<td><p><code dir="ltr" translate="no">          IF                (condition, true_result, false_result)       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          IFNULL                (expression1, expression2)       </code></p></td>
<td><p><code dir="ltr" translate="no">          IFNULL                (expression1, expression2)       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          [ NOT ] IN                ...       </code></p></td>
<td><p><code dir="ltr" translate="no">          [ NOT ] IN                ...       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        expression1                 IS [ NOT ] DISTINCT FROM                expression2       </code></p></td>
<td>BigQuery does not support a direct alternative to Snowflake's <code dir="ltr" translate="no">       IS [ NOT ] DISTINCT FROM.      </code></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        expression                 IS [ NOT ] NULL        </code></p></td>
<td><p><code dir="ltr" translate="no">        expression                 IS [ NOT ] NULL        </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          IS_NULL_VALUE                (variant_expr)       </code></p></td>
<td>BigQuery does not support <code dir="ltr" translate="no">       VARIANT      </code> data types.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          LEAST                (expression,...)       </code></p></td>
<td><p><code dir="ltr" translate="no">          LEAST                (expression,...)       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          NULLIF                (expression1,expression2)       </code></p></td>
<td><p><code dir="ltr" translate="no">          NULLIF                (expression1,expression2)       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          NVL                (expression1, expression2)       </code></p></td>
<td><p><code dir="ltr" translate="no">          IFNULL                (expression1,expression2)       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          NVL2                (expr1,expr2,expr2)       </code></p></td>
<td><p><code dir="ltr" translate="no">          IF                (expr1 IS NOT NULL, expr2,expr3)       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          REGR_VALX                (expr1,expr2)       </code></p></td>
<td><p><code dir="ltr" translate="no">          IF                (expr1 IS NULL, NULL, expr2)       </code></p>
Note: BigQuery does not support a direct alternative to Snowflake's <code dir="ltr" translate="no">       REGR...      </code> functions.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          REGR_VALY                (expr1,expr2)       </code></p></td>
<td><p><code dir="ltr" translate="no">          IF                (expr2 IS NULL, NULL, expr1)       </code></p>
<br />
Note: BigQuery does not support a direct alternative to Snowflake's <code dir="ltr" translate="no">       REGR...      </code> functions.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          ZEROIFNULL                (expression)       </code></p></td>
<td><p><code dir="ltr" translate="no">          IFNULL                (expression,0)       </code></p></td>
</tr>
</tbody>
</table>

### Context functions

The following table shows mappings between common Snowflake context functions with their BigQuery equivalents.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Snowflake</th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          CURRENT_ACCOUNT                ()       </code></p></td>
<td><p><code dir="ltr" translate="no">          SESSION_USER                ()       </code></p>
<br />
Note: Not direct comparison. Snowflake returns account ID, BigQuery returns user email address.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          CURRENT_CLIENT                ()       </code></p></td>
<td><p>Concept not used in BigQuery</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          CURRENT_DATABASE                ()       </code></p></td>
<td><p><code dir="ltr" translate="no">        SELECT catalog_name       </code></p>
<p><code dir="ltr" translate="no">        FROM                 INFORMATION_SCHEMA.SCHEMATA        </code></p>
<p>This returns a table of project names. Not a direct comparison.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          CURRENT_DATE                [()]       </code></p>
<br />
Note: Snowflake does not enforce '()' after <code dir="ltr" translate="no">       CURRENT_DATE      </code> command to comply with ANSI standards.</td>
<td><p><code dir="ltr" translate="no">          CURRENT_DATE                ([timezone])       </code></p>
<br />
Note: BigQuery's <code dir="ltr" translate="no">       CURRENT_DATE      </code> supports optional time zone specification.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          CURRENT_REGION                ()       </code></p></td>
<td><p><code dir="ltr" translate="no">        SELECT location       </code></p>
<p><code dir="ltr" translate="no">        FROM                 INFORMATION_SCHEMA.SCHEMATA        </code></p>
<br />
Note: BigQuery's <code dir="ltr" translate="no">       INFORMATION_SCHEMA.SCHEMATA      </code> returns more generalized location references than Snowflake's <code dir="ltr" translate="no">       CURRENT_REGION()      </code> . Not a direct comparison.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          CURRENT_ROLE                ()       </code></p></td>
<td><p>Concept not used in BigQuery</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          CURRENT_SCHEMA                ()       </code></p></td>
<td><p><code dir="ltr" translate="no">        SELECT schema_name       </code></p>
<p><code dir="ltr" translate="no">        FROM                 INFORMATION_SCHEMA.SCHEMATA        </code></p>
<p>This returns a table of all datasets (also called schemas) available in the project or region. Not a direct comparison.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          CURRENT_SCHEMAS                ()       </code></p></td>
<td><p>Concept not used in BigQuery</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          CURRENT_SESSION                ()       </code></p></td>
<td><p>Concept not used in BigQuery</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          CURRENT_STATEMENT                ()       </code></p></td>
<td><p><code dir="ltr" translate="no">        SELECT query       </code></p>
<p><code dir="ltr" translate="no">        FROM                 INFORMATION_SCHEMA.JOBS_BY_*        </code></p>
<br />
Note: BigQuery's <code dir="ltr" translate="no">       INFORMATION_SCHEMA.JOBS_BY_*      </code> allows for searching for queries by job type, start/end type, etc.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          CURRENT_TIME                [([frac_sec_prec])]       </code></p>
<br />
Note: Snowflake allows for optional fractional second precision. Valid values range from 0-9 nanoseconds. Default value is 9. To comply with ANSI, this can be called without '()'.</td>
<td><p><code dir="ltr" translate="no">          CURRENT_TIME                ()       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          CURRENT_TIMESTAMP                [([frac_sec_prec])]       </code></p>
<br />
Note: Snowflake allows for optional fractional second precision. Valid values range from 0-9 nanoseconds. Default value is 9. To comply with ANSI, this can be called without '()'. Set <code dir="ltr" translate="no">       TIMEZONE      </code> as a session parameter.</td>
<td><p><code dir="ltr" translate="no">          CURRENT_DATETIME                ([timezone])                 CURRENT_TIMESTAMP                ()       </code></p>
<br />
<strong>Note: <code dir="ltr" translate="no"></code></strong> <code dir="ltr" translate="no">       CURRENT_DATETIME      </code> returns <code dir="ltr" translate="no">       DATETIME      </code> data type (not supported in Snowflake). <code dir="ltr" translate="no">       CURRENT_TIMESTAMP      </code> returns <code dir="ltr" translate="no">       TIMESTAMP      </code> data type.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          CURRENT_TRANSACTION                ()       </code></p></td>
<td><p><code dir="ltr" translate="no">        SELECT job_id       </code></p>
<p><code dir="ltr" translate="no">        FROM                 INFORMATION_SCHEMA.JOBS_BY_*        </code></p>
Note: BigQuery's <code dir="ltr" translate="no">         INFORMATION_SCHEMA.JOBS_BY_*       </code> allows for searching for job IDs by job type, start/end type, etc.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        CURRENT_USER[()]       </code></p>
<br />
Note: Snowflake does not enforce '()' after <code dir="ltr" translate="no">       CURRENT_USER      </code> command to comply with ANSI standards.</td>
<td><p><code dir="ltr" translate="no">        SESSION_USER()       </code></p>
<br />

<p><code dir="ltr" translate="no">        SELECT user_email       </code></p>
<p><code dir="ltr" translate="no">        FROM                 INFORMATION_SCHEMA.JOBS_BY_*        </code></p>
Note: Not direct comparison. Snowflake returns username; BigQuery returns user email address.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          CURRENT_VERSION                ()       </code></p></td>
<td><p>Concept not used in BigQuery</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          CURRENT_WAREHOUSE()        </code></p></td>
<td><p><code dir="ltr" translate="no">        SELECT catalg_name       </code></p>
<p><code dir="ltr" translate="no">        FROM                 INFORMATION_SCHEMA.SCHEMATA        </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          LAST_QUERY_ID                ([num])       </code></p></td>
<td><p><code dir="ltr" translate="no">        SELECT job_id       </code></p>
<p><code dir="ltr" translate="no">        FROM                 INFORMATION_SCHEMA.JOBS_BY_*        </code></p>
<br />
Note: BigQuery's <code dir="ltr" translate="no">       INFORMATION_SCHEMA.JOBS_BY_*      </code> allows for searching for job IDs by job type, start/end type, etc.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          LAST_TRANSACTION                ()       </code></p></td>
<td><p><code dir="ltr" translate="no">        SELECT job_id       </code></p>
<p><code dir="ltr" translate="no">        FROM                 INFORMATION_SCHEMA.JOBS_BY_*        </code></p>
<br />
Note: BigQuery's <code dir="ltr" translate="no">         INFORMATION_SCHEMA.JOBS_BY_*       </code> allows for searching for job IDs by job type, start/end type, etc.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          LOCALTIME                ()       </code></p>
<br />
Note: Snowflake does not enforce '()' after <code dir="ltr" translate="no">       LOCALTIME      </code> command to comply with ANSI standards.</td>
<td><p><code dir="ltr" translate="no">          CURRENT_TIME                ()       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          LOCALTIMESTAMP                ()       </code></p></td>
<td><p><code dir="ltr" translate="no">          CURRENT_DATETIME                ([timezone])                 CURRENT_TIMESTAMP                ()       </code></p>
<br />
<strong>Note: <code dir="ltr" translate="no"></code></strong> <code dir="ltr" translate="no">       CURRENT_DATETIME      </code> returns <code dir="ltr" translate="no">       DATETIME      </code> data type (not supported in Snowflake). <code dir="ltr" translate="no">       CURRENT_TIMESTAMP      </code> returns <code dir="ltr" translate="no">       TIMESTAMP      </code> data type.</td>
</tr>
</tbody>
</table>

### Conversion functions

The following table shows mappings between common Snowflake conversion functions with their BigQuery equivalents.

Keep in mind that functions that seem identical in Snowflake and BigQuery may return different data types.

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
<td><p><code dir="ltr" translate="no">          CAST                (expression AS type)       </code></p>
<br />

<p><code dir="ltr" translate="no">        expression :: type       </code></p></td>
<td><p><code dir="ltr" translate="no">          CAST                (expression AS type)       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          TO_ARRAY                (expression)       </code></p></td>
<td><p><code dir="ltr" translate="no">          [expression]        </code></p>
<br />

<p><code dir="ltr" translate="no">          ARRAY                (subquery)       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          TO_BINARY                (expression[, format])       </code></p>
<br />
Note: Snowflake supports <code dir="ltr" translate="no">       HEX      </code> , <code dir="ltr" translate="no">       BASE64      </code> , and <code dir="ltr" translate="no">       UTF-8      </code> conversion. Snowflake also supports <code dir="ltr" translate="no">       TO_BINARY      </code> using the <code dir="ltr" translate="no">       VARIANT      </code> data type. BigQuery does not have an alternative to the <code dir="ltr" translate="no">       VARIANT      </code> data type.</td>
<td><p><code dir="ltr" translate="no">          TO_HEX                (CAST(expression AS BYTES))                 TO_BASE64                (CAST(expression AS BYTES))       </code></p>
<p><code dir="ltr" translate="no">          CAST                (expression AS BYTES)       </code></p>
<br />
Note: BigQuery's default <code dir="ltr" translate="no">       STRING      </code> casting uses <code dir="ltr" translate="no">       UTF-8      </code> encoding. Snowflake does not have an option to support <code dir="ltr" translate="no">       BASE32      </code> encoding.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          TO_BOOLEAN                (expression)       </code></p>
<br />
Note:<br />

<ul>
<li><code dir="ltr" translate="no">         INT64                  TRUE:        </code> otherwise, <code dir="ltr" translate="no">         FALSE: 0        </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">         STRING                  TRUE: "true"/"t"/"yes"/"y"/"on"/"1", FALSE: "false"/"f"/"no"/"n"/"off"/"0"        </code></li>
</ul></td>
<td><p><code dir="ltr" translate="no">          CAST                (expression AS BOOL)       </code></p>
<br />
Note:<br />

<ul>
<li><code dir="ltr" translate="no">         INT64                  TRUE:        </code> otherwise, <code dir="ltr" translate="no">         FALSE: 0        </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">         STRING                  TRUE: "true", FALSE: "false"        </code></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          TO_CHAR                (expression[, format])       </code></p>
<br />

<p><code dir="ltr" translate="no">          TO_VARCHAR                (expression[, format])       </code></p>
<br />
Note: Snowflake's format models can be found <a href="https://docs.snowflake.net/manuals/sql-reference/sql-format-models.html">here</a> . BigQuery does not have an alternative to the <code dir="ltr" translate="no">       VARIANT      </code> data type.</td>
<td><p><code dir="ltr" translate="no">          CAST                (expression AS STRING)       </code></p>
<br />
Note: BigQuery's input expression can be formatted using <code dir="ltr" translate="no">         FORMAT_DATE       </code> , <code dir="ltr" translate="no">         FORMAT_DATETIME       </code> , <code dir="ltr" translate="no">         FORMAT_TIME       </code> , or <code dir="ltr" translate="no">         FORMAT_TIMESTAMP       </code> .</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          TO_DATE                (expression[, format])       </code></p>
<br />

<p><code dir="ltr" translate="no">          DATE                (expression[, format])       </code></p>
<br />
Note: Snowflake supports the ability to directly convert <code dir="ltr" translate="no">       INTEGER      </code> types to <code dir="ltr" translate="no">       DATE      </code> types. Snowflake's format models can be found <a href="https://docs.snowflake.net/manuals/sql-reference/functions-conversion.html#date-and-time-formats-in-conversion-functions">here</a> . BigQuery does not have an alternative to the <code dir="ltr" translate="no">       VARIANT      </code> data type.</td>
<td><p><code dir="ltr" translate="no">          CAST                (expression AS DATE)       </code></p>
<br />
Note: BigQuery's input expression can be formatted using <code dir="ltr" translate="no">         FORMAT       </code> , <code dir="ltr" translate="no">         FORMAT_DATETIME       </code> , or <code dir="ltr" translate="no">         FORMAT_TIMESTAMP       </code> .</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          TO_DECIMAL                (expression[, format]       </code></p>
<p><code dir="ltr" translate="no">        [,precision[, scale]]       </code></p>
<br />

<p><code dir="ltr" translate="no">          TO_NUMBER                (expression[, format]       </code></p>
<p><code dir="ltr" translate="no">        [,precision[, scale]]       </code></p>
<br />

<p><code dir="ltr" translate="no">          TO_NUMERIC                (expression[, format]       </code></p>
<p><code dir="ltr" translate="no">        [,precision[, scale]]       </code></p>
<br />
Note: Snowflake's format models for the <code dir="ltr" translate="no">       DECIMAL      </code> , <code dir="ltr" translate="no">       NUMBER      </code> , and <code dir="ltr" translate="no">       NUMERIC      </code> data types can be found <a href="https://docs.snowflake.net/manuals/sql-reference/sql-format-models.html">here</a> . BigQuery does not have an alternative to the <code dir="ltr" translate="no">       VARIANT      </code> data type.</td>
<td><p><code dir="ltr" translate="no">          ROUND                (                 CAST                (expression AS NUMERIC)       </code></p>
<p><code dir="ltr" translate="no">        , x)       </code></p>
<br />
Note: BigQuery's input expression can be formatted using <code dir="ltr" translate="no">         FORMAT              .      </code></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          TO_DOUBLE                (expression[, format])       </code></p>
<br />
Note: Snowflake's format models for the <code dir="ltr" translate="no">       DOUBLE      </code> data types can be found <a href="https://docs.snowflake.net/manuals/sql-reference/sql-format-models.html">here</a> . BigQuery does not have an alternative to the <code dir="ltr" translate="no">       VARIANT      </code> data type.</td>
<td><p><code dir="ltr" translate="no">          CAST                (expression AS FLOAT64)       </code></p>
<br />
Note: BigQuery's input expression can be formatted using <code dir="ltr" translate="no">         FORMAT              .      </code></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          TO_JSON                (variant_expression)       </code></p></td>
<td>BigQuery does not have an alternative to Snowflake's <code dir="ltr" translate="no">       VARIANT      </code> data type.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          TO_OBJECT                (variant_expression)       </code></p></td>
<td>BigQuery does not have an alternative to Snowflake's <code dir="ltr" translate="no">       VARIANT      </code> data type.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          TO_TIME                (expression[, format])       </code></p>
<br />

<p><code dir="ltr" translate="no">          TIME                (expression[, format])       </code></p>
<br />
Note: Snowflake's format models for the <code dir="ltr" translate="no">       STRING      </code> data types can be found <a href="https://docs.snowflake.net/manuals/sql-reference/functions-conversion.html">here</a> . BigQuery does not have an alternative to the <code dir="ltr" translate="no">       VARIANT      </code> data type.</td>
<td><p><code dir="ltr" translate="no">          CAST                (expression AS TIME)       </code></p>
<br />
Note: BigQuery does not have an alternative to Snowflake's <code dir="ltr" translate="no">       VARIANT      </code> data type. BigQuery's input expression can be formatted using <code dir="ltr" translate="no">         FORMAT       </code> , <code dir="ltr" translate="no">         FORMAT_DATETIME       </code> , <code dir="ltr" translate="no">         FORMAT_TIMESTAMP       </code> , or <code dir="ltr" translate="no">         FORMAT_TIME       </code> .</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          TO_TIMESTAMP                (expression[, scale])       </code></p>
<br />

<p><code dir="ltr" translate="no">          TO_TIMESTAMP_LTZ                (expression[, scale])       </code></p>
<br />

<p><code dir="ltr" translate="no">          TO_TIMESTAMP_NTZ                (expression[, scale])       </code></p>
<br />

<p><code dir="ltr" translate="no">          TO_TIMESTAMP_TZ                (expression[, scale])       </code></p>
<br />
Note: BigQuery does not have an alternative to the <code dir="ltr" translate="no">       VARIANT      </code> data type.</td>
<td><p><code dir="ltr" translate="no">          CAST                (expression AS TIMESTAMP)       </code></p>
<br />
Note: BigQuery's input expression can be formatted using <code dir="ltr" translate="no">         FORMAT       </code> , <code dir="ltr" translate="no">         FORMAT_DATE       </code> , <code dir="ltr" translate="no">         FORMAT_DATETIME       </code> , <code dir="ltr" translate="no">         FORMAT_TIME       </code> . Timezone can be included/not included through <code dir="ltr" translate="no">         FORMAT_TIMESTAMP       </code> parameters.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          TO_VARIANT                (expression)       </code></p></td>
<td>BigQuery does not have an alternative to Snowflake's <code dir="ltr" translate="no">       VARIANT      </code> data type.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          TO_XML                (variant_expression)       </code></p></td>
<td>BigQuery does not have an alternative to Snowflake's <code dir="ltr" translate="no">       VARIANT      </code> data type.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          TRY_CAST                (expression AS type)       </code></p></td>
<td><p><code dir="ltr" translate="no">          SAFE_CAST                (expression AS type)       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          TRY_TO_BINARY                (expression[, format])       </code></p></td>
<td><p><code dir="ltr" translate="no">          TO_HEX                (SAFE_CAST(expression AS BYTES))                 TO_BASE64                (SAFE_CAST(expression AS BYTES))       </code></p>
<p><code dir="ltr" translate="no">          SAFE_CAST                (expression AS BYTES)       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          TRY_TO_BOOLEAN                (expression)       </code></p></td>
<td><p><code dir="ltr" translate="no">          SAFE_CAST                (expression AS BOOL)       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          TRY_TO_DATE                (expression)       </code></p></td>
<td><p><code dir="ltr" translate="no">          SAFE_CAST                (expression AS DATE)       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          TRY_TO_DECIMAL                (expression[, format]       </code></p>
<p><code dir="ltr" translate="no">        [,precision[, scale]]       </code></p>
<br />

<p><code dir="ltr" translate="no">          TRY_TO_NUMBER                (expression[, format]       </code></p>
<p><code dir="ltr" translate="no">        [,precision[, scale]]       </code></p>
<br />

<p><code dir="ltr" translate="no">          TRY_TO_NUMERIC                (expression[, format]       </code></p>
<p><code dir="ltr" translate="no">        [,precision[, scale]]       </code></p></td>
<td><p><code dir="ltr" translate="no">          ROUND                (       </code></p>
<p><code dir="ltr" translate="no">          SAFE_CAST                (expression AS NUMERIC)       </code></p>
<p><code dir="ltr" translate="no">        , x)       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          TRY_TO_DOUBLE                (expression)       </code></p></td>
<td><p><code dir="ltr" translate="no">          SAFE_CAST                (expression AS FLOAT64)       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          TRY_TO_TIME                (expression)       </code></p></td>
<td><p><code dir="ltr" translate="no">          SAFE_CAST                (expression AS TIME)       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          TRY_TO_TIMESTAMP                (expression)       </code></p>
<br />

<p><code dir="ltr" translate="no">          TRY_TO_TIMESTAMP_LTZ                (expression)       </code></p>
<br />

<p><code dir="ltr" translate="no">          TRY_TO_TIMESTAMP_NTZ                (expression)       </code></p>
<br />

<p><code dir="ltr" translate="no">          TRY_TO_TIMESTAMP_TZ                (expression)       </code></p></td>
<td><p><code dir="ltr" translate="no">          SAFE_CAST                (expression AS TIMESTAMP)       </code></p></td>
</tr>
</tbody>
</table>

BigQuery also offers the following conversion functions, which do not have a direct analogue in Snowflake:

  - [`  CODE_POINTS_TO_BYTES  `](/bigquery/docs/reference/standard-sql/string_functions#code_points_to_bytes)
  - [`  CODE_POINTS_TO_STRING  `](/bigquery/docs/reference/standard-sql/string_functions#code_points_to_string)
  - [`  FORMAT  `](/bigquery/docs/reference/standard-sql/string_functions#format_string)
  - [`  FROM_BASE32  `](/bigquery/docs/reference/standard-sql/string_functions#from_base32)
  - [`  FROM_BASE64  `](/bigquery/docs/reference/standard-sql/string_functions#from_base64)
  - [`  FROM_HEX  `](/bigquery/docs/reference/standard-sql/string_functions#from_hex)
  - [`  SAFE_CONVERT_BYTES_TO_STRING  `](/bigquery/docs/reference/standard-sql/string_functions#safe_convert_bytes_to_string)
  - [`  TO_BASE32  `](/bigquery/docs/reference/standard-sql/string_functions#to_base32)
  - [`  TO_CODE_POINTS  `](/bigquery/docs/reference/standard-sql/string_functions#to_code_points)

### Data generation functions

The following table shows mappings between common Snowflake data generation functions with their BigQuery equivalents.

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
<td><p><code dir="ltr" translate="no">          NORMAL                (mean, stddev, gen)       </code></p></td>
<td>BigQuery does not support a direct comparison to Snowflake's <code dir="ltr" translate="no">       NORMAL.      </code></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          RANDOM                ([seed])       </code></p></td>
<td><p><code dir="ltr" translate="no">        IF(                 RAND                ()&gt;0.5,   CAST(RAND()*POW(10, 18) AS INT64),       </code></p>
<p><code dir="ltr" translate="no">        (-1)*CAST(RAND()*POW(10, 18) AS       </code></p>
<p><code dir="ltr" translate="no">        INT64))       </code></p>
<br />
Note: BigQuery does not support seeding</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          RANDSTR                (length, gen)       </code></p></td>
<td>BigQuery does not support a direct comparison to Snowflake's <code dir="ltr" translate="no">       RANDSTR.      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         SEQ1 / SEQ2 / SEQ4 / SEQ8       </code></td>
<td>BigQuery does not support a direct comparison to Snowflake's <code dir="ltr" translate="no">       SEQ_.      </code></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          UNIFORM                (min, max, gen)       </code></p></td>
<td><p><code dir="ltr" translate="no">        CAST(min + RAND()*(max-min) AS INT64)       </code></p>
<br />
Note:Use persistent UDFs to create an equivalent to Snowflake's <code dir="ltr" translate="no">       UNIFORM      </code> . Example <a href="https://medium.com/@hoffa/new-in-bigquery-persistent-udfs-c9ea4100fd83">here</a> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         UUID_STRING              ([uuid, name])        </code> Note: Snowflake returns 128 random bits. Snowflake supports both version 4 (random) and version 5 (named) UUIDs.</td>
<td><p><code dir="ltr" translate="no">          GENERATE_UUID                ()       </code></p>
<br />
Note: BigQuery returns 122 random bits. BigQuery only supports version 4 UUIDs.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          ZIPF                (s, N, gen)       </code></p></td>
<td>BigQuery does not support a direct comparison to Snowflake's <code dir="ltr" translate="no">       ZIPF.      </code></td>
</tr>
</tbody>
</table>

### Date and time functions

The following table shows mappings between common Snowflake date and time functions with their BigQuery equivalents. BigQuery data and time functions include [Date functions](/bigquery/docs/reference/standard-sql/date_functions) , [Datetime functions](/bigquery/docs/reference/standard-sql/datetime_functions) , [Time functions](/bigquery/docs/reference/standard-sql/time_functions) , and [Timestamp functions](/bigquery/docs/reference/standard-sql/timestamp_functions) .

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
<td><p><code dir="ltr" translate="no">          ADD_MONTHS                (date, months)       </code></p></td>
<td><p><code dir="ltr" translate="no">          CAST                (       </code></p>
<p><code dir="ltr" translate="no">          DATE_ADD                (       </code></p>
<p><code dir="ltr" translate="no">        date,       </code></p>
<p><code dir="ltr" translate="no">        INTERVAL integer MONTH       </code></p>
<p><code dir="ltr" translate="no">        ) AS TIMESTAMP       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          CONVERT_TIMEZONE                (source_tz, target_tz, source_timestamp)       </code></p>
<br />

<p><code dir="ltr" translate="no">          CONVERT_TIMEZONE                (target_tz, source_timestamp)       </code></p></td>
<td><p><code dir="ltr" translate="no">          PARSE_TIMESTAMP                (       </code></p>
<p><code dir="ltr" translate="no">        "%c%z",       </code></p>
<p><code dir="ltr" translate="no">          FORMAT_TIMESTAMP                (       </code></p>
<p><code dir="ltr" translate="no">        "%c%z",       </code></p>
<p><code dir="ltr" translate="no">        timestamp,       </code></p>
<p><code dir="ltr" translate="no">        target_timezone       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p>
<br />
Note: source_timezone is always UTC in BigQuery</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          DATE_FROM_PARTS                (year, month, day)       </code></p>
<br />
Note: Snowflake supports overflow and negative dates. For example, <code dir="ltr" translate="no">       DATE_FROM_PARTS(2000, 1 + 24, 1)      </code> returns Jan 1, 2002. This is not supported in BigQuery.</td>
<td><p><code dir="ltr" translate="no">          DATE                (year, month, day)       </code></p>
<br />

<p><code dir="ltr" translate="no">          DATE                (timestamp_expression[, timezone])       </code></p>
<br />

<p><code dir="ltr" translate="no">          DATE                (datetime_expression)       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          DATE_PART                (part, dateOrTime)       </code></p>
<br />
Note: Snowflake supports the day of week ISO, nanosecond, and epoch second/millisecond/microsecond/nanosecond part types. BigQuery does not. See full list of Snowflake part types <a href="https://docs.snowflake.net/manuals/sql-reference/functions-date-time.html#label-supported-date-time-parts">here <code dir="ltr" translate="no"></code></a> <code dir="ltr" translate="no">       .      </code></td>
<td><p><code dir="ltr" translate="no">          EXTRACT                (part FROM dateOrTime)       </code></p>
<br />
Note: BigQuery supports the week(&lt;weekday&gt;), microsecond, and millisecond part types. Snowflake does not. See full list of BigQuery part types <a href="/bigquery/docs/reference/standard-sql/date_functions#extract">here</a> and <a href="/bigquery/docs/reference/standard-sql/timestamp_functions#extract">here</a> .</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          DATE_TRUNC                (part, dateOrTime)       </code></p>
<br />
Note: Snowflake supports the nanosecond part type. BigQuery does not. See full list of Snowflake part types <a href="https://docs.snowflake.net/manuals/sql-reference/functions-date-time.html#label-supported-date-time-parts">here <code dir="ltr" translate="no"></code></a> <code dir="ltr" translate="no">       .      </code></td>
<td><p><code dir="ltr" translate="no">          DATE_TRUNC                (date, part)       </code></p>
<br />

<p><code dir="ltr" translate="no">          DATETIME_TRUNC                (datetime, part)       </code></p>
<br />

<p><code dir="ltr" translate="no">          TIME_TRUNC                (time, part)       </code></p>
<br />

<p><code dir="ltr" translate="no">          TIMESTAMP_TRUNC                (timestamp, part[, timezone])       </code></p>
<br />
Note: BigQuery supports the week(&lt;weekday&gt;), ISO week, and ISO year part types. Snowflake does not.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          DATEADD                (part, value, dateOrTime)       </code></p></td>
<td><p><code dir="ltr" translate="no">          DATE_ADD                (date, INTERVAL value part)       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          DATEDIFF                (       </code></p>
<p><code dir="ltr" translate="no">        part,       </code></p>
<p><code dir="ltr" translate="no">        start_date_or_time,       </code></p>
<p><code dir="ltr" translate="no">        end_date_or_time       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p>
<br />
Note: Snowflake supports calculating the difference between two date, time, and timestamp types in this function.</td>
<td><p><code dir="ltr" translate="no">          DATE_DIFF                (       </code></p>
<p><code dir="ltr" translate="no">        end_date,       </code></p>
<p><code dir="ltr" translate="no">        start_date,       </code></p>
<p><code dir="ltr" translate="no">        part       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p>
<br />

<p><code dir="ltr" translate="no">          DATETIME_DIFF                (       </code></p>
<p><code dir="ltr" translate="no">        end_datetime,       </code></p>
<p><code dir="ltr" translate="no">        start_datetime,       </code></p>
<p><code dir="ltr" translate="no">        part       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p>
<br />

<p><code dir="ltr" translate="no">          TIME_DIFF                (       </code></p>
<p><code dir="ltr" translate="no">        start_time,       </code></p>
<p><code dir="ltr" translate="no">        end_time,       </code></p>
<p><code dir="ltr" translate="no">        part       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p>
<br />

<p><code dir="ltr" translate="no">          TIMESTAMP_DIFF                (       </code></p>
<p><code dir="ltr" translate="no">        end_timestamp,       </code></p>
<p><code dir="ltr" translate="no">        start_timestamp,       </code></p>
<p><code dir="ltr" translate="no">        part       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p>
<br />
Note: BigQuery supports the week(&lt;weekday&gt;) and ISO year part types.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          DAYNAME                (dateOrTimestamp)       </code></p></td>
<td><p><code dir="ltr" translate="no">          FORMAT_DATE                ('%a', date)       </code></p>
<br />

<p><code dir="ltr" translate="no">          FORMAT_DATETIME                ('%a', datetime)       </code></p>
<br />

<p><code dir="ltr" translate="no">          FORMAT_TIMESTAMP                ('%a', timestamp)       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          EXTRACT                (part FROM dateOrTime)       </code></p>
<br />
Note: Snowflake supports the day of week ISO, nanosecond, and epoch second/millisecond/microsecond/nanosecond part types. BigQuery does not. See full list of Snowflake part types <a href="https://docs.snowflake.net/manuals/sql-reference/functions-date-time.html#label-supported-date-time-parts">here <code dir="ltr" translate="no"></code></a> <code dir="ltr" translate="no">       .      </code></td>
<td><p><code dir="ltr" translate="no">          EXTRACT                (part FROM dateOrTime)       </code></p>
<br />
Note: BigQuery supports the week(&lt;weekday&gt;), microsecond, and millisecond part types. Snowflake does not. See full list of BigQuery part types <a href="/bigquery/docs/reference/standard-sql/date_functions#extract">here</a> and <a href="/bigquery/docs/reference/standard-sql/timestamp_functions#extract">here</a> .</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          [HOUR, MINUTE, SECOND]                (timeOrTimestamp)       </code></p></td>
<td><p><code dir="ltr" translate="no">          EXTRACT                (part FROM timestamp [AT THE ZONE timezone])       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          LAST_DAY                (dateOrTime[, part])       </code></p></td>
<td><p><code dir="ltr" translate="no">        DATE_SUB(   DATE_TRUNC(       </code></p>
<p><code dir="ltr" translate="no">        DATE_ADD(date, INTERVAL       </code></p>
<p><code dir="ltr" translate="no">        1 part),       </code></p>
<p><code dir="ltr" translate="no">        part),       </code></p>
<p><code dir="ltr" translate="no">        INTERVAL 1 DAY)       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          MONTHNAME(dateOrTimestamp)        </code></p></td>
<td><p><code dir="ltr" translate="no">          FORMAT_DATE                ('%b', date)       </code></p>
<br />

<p><code dir="ltr" translate="no">          FORMAT_DATETIME                ('%b', datetime)       </code></p>
<br />

<p><code dir="ltr" translate="no">          FORMAT_TIMESTAMP                ('%b', timestamp)       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          NEXT_DAY                (dateOrTime, dowString)       </code></p></td>
<td><p><code dir="ltr" translate="no">        DATE_ADD(       </code></p>
<p><code dir="ltr" translate="no">        DATE_TRUNC(       </code></p>
<p><code dir="ltr" translate="no">        date,       </code></p>
<p><code dir="ltr" translate="no">        WEEK(dowString)),       </code></p>
<p><code dir="ltr" translate="no">        INTERVAL 1 WEEK)       </code></p>
<br />
Note: dowString might need to be reformatted. For example, Snowflake's 'su' will be BigQuery's 'SUNDAY'.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          PREVIOUS_DAY                (dateOrTime, dowString)       </code></p></td>
<td><p><code dir="ltr" translate="no">        DATE_TRUNC(       </code></p>
<p><code dir="ltr" translate="no">        date,       </code></p>
<p><code dir="ltr" translate="no">        WEEK(dowString)       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p>
<br />
Note: dowString might need to be reformatted. For example, Snowflake's 'su' will be BigQuery's 'SUNDAY'.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          TIME_FROM_PARTS                (hour, minute, second[, nanosecond)       </code></p>
<br />
Note: Snowflake supports overflow times. For example, <code dir="ltr" translate="no">       TIME_FROM_PARTS(0, 100, 0)      </code> returns 01:40:00... This is not supported in BigQuery. BigQuery does not support nanoseconds.</td>
<td><p><code dir="ltr" translate="no">          TIME                (hour, minute, second)       </code></p>
<br />

<p><code dir="ltr" translate="no">        TIME(timestamp, [timezone])       </code></p>
<br />

<p><code dir="ltr" translate="no">        TIME(datetime)       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          TIME_SLICE                (dateOrTime, sliceLength, part[, START]       </code></p>
<br />

<p><code dir="ltr" translate="no">        TIME_SLICE(dateOrTime, sliceLength, part[, END]       </code></p></td>
<td><p><code dir="ltr" translate="no">        DATE_TRUNC(       </code></p>
<p><code dir="ltr" translate="no">        DATE_SUB(CURRENT_DATE(),       </code></p>
<p><code dir="ltr" translate="no">        INTERVAL value MONTH),       </code></p>
<p><code dir="ltr" translate="no">        MONTH)       </code></p>
<br />

<p><code dir="ltr" translate="no">        DATE_TRUNC(       </code></p>
<p><code dir="ltr" translate="no">        DATE_ADD(CURRENT_DATE(),       </code></p>
<p><code dir="ltr" translate="no">        INTERVAL value MONTH),       </code></p>
<p><code dir="ltr" translate="no">        MONTH)       </code></p>
<br />
Note: BigQuery does not support a direct, exact comparison to Snowflake's <code dir="ltr" translate="no">       TIME_SLICE      </code> . Use <code dir="ltr" translate="no">       DATETINE_TRUNC      </code> , <code dir="ltr" translate="no">       TIME_TRUNC      </code> , <code dir="ltr" translate="no">       TIMESTAMP_TRUNC      </code> for appropriate data type.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          TIMEADD                (part, value, dateOrTime)       </code></p></td>
<td><p><code dir="ltr" translate="no">          TIME_ADD                (time, INTERVAL value part)       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          TIMEDIFF                (       </code></p>
<p><code dir="ltr" translate="no">        part,       </code></p>
<p><code dir="ltr" translate="no">        expression1,       </code></p>
<p><code dir="ltr" translate="no">        expression2,       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p>
<br />
Note: Snowflake supports calculating the difference between two date, time, and timestamp types in this function.</td>
<td><p><code dir="ltr" translate="no">          DATE_DIFF                (       </code></p>
<p><code dir="ltr" translate="no">        dateExpression1,       </code></p>
<p><code dir="ltr" translate="no">        dateExpression2,       </code></p>
<p><code dir="ltr" translate="no">        part       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p>
<br />

<p><code dir="ltr" translate="no">          DATETIME_DIFF                (       </code></p>
<p><code dir="ltr" translate="no">        datetimeExpression1,       </code></p>
<p><code dir="ltr" translate="no">        datetimeExpression2,       </code></p>
<p><code dir="ltr" translate="no">        part       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p>
<br />

<p><code dir="ltr" translate="no">          TIME_DIFF                (       </code></p>
<p><code dir="ltr" translate="no">        timeExpression1,       </code></p>
<p><code dir="ltr" translate="no">        timeExpression2,       </code></p>
<p><code dir="ltr" translate="no">        part       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p>
<br />

<p><code dir="ltr" translate="no">          TIMESTAMP_DIFF                (       </code></p>
<p><code dir="ltr" translate="no">        timestampExpression1,       </code></p>
<p><code dir="ltr" translate="no">        timestampExpression2,       </code></p>
<p><code dir="ltr" translate="no">        part       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p>
<br />
Note: BigQuery supports the week(&lt;weekday&gt;) and ISO year part types.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          TIMESTAMP_[LTZ, NTZ, TZ _]FROM_PARTS                (year, month, day, hour, second [, nanosecond][, timezone])       </code></p></td>
<td><p><code dir="ltr" translate="no">          TIMESTAMP                (       </code></p>
<p><code dir="ltr" translate="no">        string_expression[, timezone] |   date_expression[, timezone] |       </code></p>
<p><code dir="ltr" translate="no">        datetime_expression[, timezone]       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p>
<br />
Note: BigQuery requires timestamps be inputted as <code dir="ltr" translate="no">       STRING      </code> types. Example: <code dir="ltr" translate="no">       "2008-12-25 15:30:00"      </code></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          TIMESTAMPADD                (part, value, dateOrTime)       </code></p></td>
<td><p><code dir="ltr" translate="no">          TIMESTAMPADD                (timestamp, INTERVAL value part)       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          TIMESTAMPDIFF                (       </code></p>
<p><code dir="ltr" translate="no">        part,       </code></p>
<p><code dir="ltr" translate="no">        expression1,       </code></p>
<p><code dir="ltr" translate="no">        expression2,       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p>
<br />
Note: Snowflake supports calculating the difference between two date, time, and timestamp types in this function.</td>
<td><p><code dir="ltr" translate="no">          DATE_DIFF                (       </code></p>
<p><code dir="ltr" translate="no">        dateExpression1,       </code></p>
<p><code dir="ltr" translate="no">        dateExpression2,       </code></p>
<p><code dir="ltr" translate="no">        part       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p>
<br />

<p><code dir="ltr" translate="no">          DATETIME_DIFF                (       </code></p>
<p><code dir="ltr" translate="no">        datetimeExpression1,       </code></p>
<p><code dir="ltr" translate="no">        datetimeExpression2,       </code></p>
<p><code dir="ltr" translate="no">        part       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p>
<br />

<p><code dir="ltr" translate="no">          TIME_DIFF                (       </code></p>
<p><code dir="ltr" translate="no">        timeExpression1,       </code></p>
<p><code dir="ltr" translate="no">        timeExpression2,       </code></p>
<p><code dir="ltr" translate="no">        part       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p>
<br />

<p><code dir="ltr" translate="no">          TIMESTAMP_DIFF                (       </code></p>
<p><code dir="ltr" translate="no">        timestampExpression1,       </code></p>
<p><code dir="ltr" translate="no">        timestampExpression2,       </code></p>
<p><code dir="ltr" translate="no">        part       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p>
<br />
Note: BigQuery supports the week(&lt;weekday&gt;) and ISO year part types.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          TRUNC                (dateOrTime, part)       </code></p>
<br />
Note: Snowflake supports the nanosecond part type. BigQuery does not. See full list of Snowflake part types <a href="https://docs.snowflake.net/manuals/sql-reference/functions-date-time.html#label-supported-date-time-parts">here <code dir="ltr" translate="no"></code></a> <code dir="ltr" translate="no">       .      </code></td>
<td><p><code dir="ltr" translate="no">          DATE_TRUNC                (date, part)       </code></p>
<br />

<p><code dir="ltr" translate="no">          DATETIME_TRUNC                (datetime, part)       </code></p>
<br />

<p><code dir="ltr" translate="no">          TIME_TRUNC                (time, part)       </code></p>
<br />

<p><code dir="ltr" translate="no">          TIMESTAMP_TRUNC                (timestamp, part[, timezone])       </code></p>
<br />
Note: BigQuery supports the week(&lt;weekday&gt;), ISO week, and ISO year part types. Snowflake does not.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          [YEAR*, DAY*, WEEK*, MONTH, QUARTER]                (dateOrTimestamp)       </code></p></td>
<td><p><code dir="ltr" translate="no">          EXTRACT                (part FROM timestamp [AT THE ZONE timezone])       </code></p></td>
</tr>
</tbody>
</table>

BigQuery also offers the following date and time functions, which do not have a direct analogue in Snowflake:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><ul>
<li><code dir="ltr" translate="no">           DATE_SUB         </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">           PARSE_DATE         </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">           DATETIME_ADD         </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">           PARSE_DATETIME         </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">           PARSE_TIME         </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">           TIMESTAMP_SUB         </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">           TIMESTAMP_SECONDS         </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">           UNIX_SECONDS         </code></li>
</ul></th>
<th><ul>
<li><code dir="ltr" translate="no">           DATE_FROM_UNIX_DATE         </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">           UNIX_DATE         </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">           DATETIME_SUB         </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">           TIME_SUB         </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">           STRING         </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">           FORMAT_TIMESTAMP         </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">           TIMESTAMP_MILLIS         </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">           UNIX_MILLIS         </code></li>
</ul></th>
<th><ul>
<li><code dir="ltr" translate="no">           FORMAT_DATE         </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">           DATETIME         </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">           FORMAT_DATETIME         </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">           FORMAT_TIME         </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">           TIMESTAMP_ADD         </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">           PARSE_TIMESTAMP         </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">           TIMESTAMP_MICROS         </code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">           UNIX_MICROS         </code></li>
</ul></th>
</tr>
</thead>
<tbody>
</tbody>
</table>

### Information schema and table functions

BigQuery does not conceptually support many of Snowflake's information schema and table functions. Snowflake offers the following information schema and table functions, which do not have a direct analogue in BigQuery:

  - [`  AUTOMATIC_CLUSTERING_HISTORY  `](https://docs.snowflake.net/manuals/sql-reference/functions/automatic_clustering_history.html)
  - [`  COPY_HISTORY  `](https://docs.snowflake.net/manuals/sql-reference/functions/copy_history.html)
  - [`  DATA_TRANSFER_HISTORY  `](https://docs.snowflake.net/manuals/sql-reference/functions/data_transfer_history.html)
  - [`  DATABASE_REFRESH_HISTORY  `](https://docs.snowflake.net/manuals/sql-reference/functions/database_refresh_history.html)
  - [`  DATABASE_REFRESH_PROGRESS, DATABASE_REFRESH_PROGRESS_BY_JOB  `](https://docs.snowflake.net/manuals/sql-reference/functions/database_refresh_progress.html)
  - [`  DATABASE_STORAGE_USAGE_HISTORY  `](https://docs.snowflake.net/manuals/sql-reference/functions/database_storage_usage_history.html)
  - [`  EXTERNAL_TABLE_FILES  `](https://docs.snowflake.net/manuals/sql-reference/functions/external_table_files.html)
  - [`  EXTERNAL_TABLE_FILE_REGISTRATION_HISTORY  `](https://docs.snowflake.net/manuals/sql-reference/functions/external_table_registration_history.html)
  - [`  LOGIN_HISTORY  ` , `  LOGIN_HISTORY_BY_USER  `](https://docs.snowflake.net/manuals/sql-reference/functions/login_history.html)
  - [`  MATERIALIZED_VIEW_REFRESH_HISTORY  `](https://docs.snowflake.net/manuals/sql-reference/functions/materialized_view_refresh_history.html)
  - [`  PIPE_USAGE_HISTORY  `](https://docs.snowflake.net/manuals/sql-reference/functions/pipe_usage_history.html)
  - [`  REPLICATION_USAGE_HISTORY  `](https://docs.snowflake.net/manuals/sql-reference/functions/replication_usage_history.html)
  - [`  STAGE_STORAGE_USAGE_HISTORY  `](https://docs.snowflake.net/manuals/sql-reference/functions/stage_storage_usage_history.html)
  - [`  TASK_DEPENDENTS  `](https://docs.snowflake.net/manuals/sql-reference/functions/task_dependents.html)
  - [`  VALIDATE_PIPE_LOAD  `](https://docs.snowflake.net/manuals/sql-reference/functions/validate_pipe_load.html)
  - [`  WAREHOUSE_LOAD_HISTORY  `](https://docs.snowflake.net/manuals/sql-reference/functions/warehouse_load_history.html)
  - [`  WAREHOUSE_METERING_HISTORY  `](https://docs.snowflake.net/manuals/sql-reference/functions/warehouse_metering_history.html)

Below is a list of associated BigQuery and Snowflake information schema and table functions.

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
<td><code dir="ltr" translate="no">         QUERY_HISTORY       </code><br />
<br />
<code dir="ltr" translate="no">         QUERY_HISTORY_BY_*       </code></td>
<td><code dir="ltr" translate="no">         INFORMATION_SCHEMA.JOBS_BY_*       </code><br />
<br />
Note: Not a direct alternative.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         TASK_HISTORY       </code></td>
<td><code dir="ltr" translate="no">         INFORMATION_SCHEMA.JOBS_BY_*       </code><br />
<br />
Note: Not a direct alternative.</td>
</tr>
</tbody>
</table>

BigQuery offers the following information schema and table functions, which do not have a direct analogue in Snowflake:

  - [`  INFORMATION_SCHEMA.SCHEMATA  `](/bigquery/docs/information-schema-datasets)
  - [`  INFORMATION_SCHEMA.ROUTINES  `](/bigquery/docs/information-schema-routines)
  - [`  INFORMATION_SCHEMA.TABLES  `](/bigquery/docs/information-schema-tables)
  - [`  INFORMATION_SCHEMA.VIEWS  `](/bigquery/docs/information-schema-views)

### Numeric functions

The following table shows mappings between common Snowflake numeric functions with their BigQuery equivalents.

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
<td><p><code dir="ltr" translate="no">          ABS                (expression)       </code></p></td>
<td><p><code dir="ltr" translate="no">          ABS                (expression)       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          ACOS                (expression)       </code></p></td>
<td><p><code dir="ltr" translate="no">          ACOS                (expression)       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          ACOSH                (expression)       </code></p></td>
<td><p><code dir="ltr" translate="no">          ACOSH                (expression)       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          ASIN                (expression)       </code></p></td>
<td><p><code dir="ltr" translate="no">          ASIN                (expression)       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          ASINH                (expression)       </code></p></td>
<td><p><code dir="ltr" translate="no">          ASINH                (expression)       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          ATAN                (expression)       </code></p></td>
<td><p><code dir="ltr" translate="no">          ATAN                (expression)       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          ATAN2                (y, x)       </code></p></td>
<td><p><code dir="ltr" translate="no">          ATAN2                (y, x)       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          ATANH                (expression)       </code></p></td>
<td><p><code dir="ltr" translate="no">          ATANH                (expression)       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          CBRT                (expression)       </code></p></td>
<td><p><code dir="ltr" translate="no">          POW                (expression, ⅓)       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          CEIL                (expression [, scale])       </code></p></td>
<td><p><code dir="ltr" translate="no">          CEIL                (expression)       </code></p>
<br />
Note: BigQuery's <code dir="ltr" translate="no">       CEIL      </code> does not support the ability to indicate precision or scale. <code dir="ltr" translate="no">       ROUND      </code> does not allow you to specify to round up.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          COS                (expression)       </code></p></td>
<td><p><code dir="ltr" translate="no">          COS                (expression)       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          COSH                (expression)       </code></p></td>
<td><p><code dir="ltr" translate="no">          COSH                (expression)       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          COT                (expression)       </code></p></td>
<td><p><code dir="ltr" translate="no">        1/                 TAN                (expression)       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          DEGREES                (expression)       </code></p></td>
<td><p><code dir="ltr" translate="no">        (expression)*(180/ACOS(-1))       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          EXP                (expression)       </code></p></td>
<td><p><code dir="ltr" translate="no">          EXP                (expression)       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          FACTORIAL                (expression)       </code></p></td>
<td>BigQuery does not have a direct alternative to Snowflake's <code dir="ltr" translate="no">       FACTORIAL      </code> . Use a user-defined function.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          FLOOR                (expression [, scale])       </code></p></td>
<td><p><code dir="ltr" translate="no">          FLOOR                (expression)       </code></p>
<br />
Note: BigQuery's <code dir="ltr" translate="no">       FLOOR      </code> does not support the ability to indicate precision or scale. <code dir="ltr" translate="no">       ROUND      </code> does not allow you to specify to round up. <code dir="ltr" translate="no">       TRUNC      </code> performs synonymously for positive numbers but not negative numbers, as it evaluates absolute value.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          HAVERSINE                (lat1, lon1, lat2, lon2)       </code></p></td>
<td><p><code dir="ltr" translate="no">          ST_DISTANCE                (                 ST_GEOGPOINT                (lon1, lat1),       </code></p>
<p><code dir="ltr" translate="no">        ST_GEOGPOINT(lon2, lat2)       </code></p>
<p><code dir="ltr" translate="no">        )/1000       </code></p>
<br />
Note: Not an exact match, but close enough.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          LN                (expression)       </code></p></td>
<td><p><code dir="ltr" translate="no">          LN                (expression)       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          LOG                (base, expression)       </code></p></td>
<td><p><code dir="ltr" translate="no">          LOG                (expression [,base])       </code></p>
<br />

<p><code dir="ltr" translate="no">          LOG10                (expression)       </code></p>
<br />
Note:Default base for <code dir="ltr" translate="no">       LOG      </code> is 10.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          MOD                (expression1, expression2)       </code></p></td>
<td><p><code dir="ltr" translate="no">          MOD                (expression1, expression2)       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          PI                ()       </code></p></td>
<td><p><code dir="ltr" translate="no">          ACOS                (-1)       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          POW                (x, y)       </code></p>
<br />

<p><code dir="ltr" translate="no">          POWER                (x, y)       </code></p></td>
<td><p><code dir="ltr" translate="no">          POW                (x, y)       </code></p>
<br />

<p><code dir="ltr" translate="no">          POWER                (x, y)       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          RADIANS                (expression)       </code></p></td>
<td><p><code dir="ltr" translate="no">        (expression)*(                 ACOS                (-1)/180)       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          ROUND                (expression [, scale])       </code></p></td>
<td><p><code dir="ltr" translate="no">          ROUND                (expression, [, scale])       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          SIGN                (expression)       </code></p></td>
<td><p><code dir="ltr" translate="no">          SIGN                (expression)       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          SIN                (expression)       </code></p></td>
<td><p><code dir="ltr" translate="no">          SIN                (expression)       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          SINH                (expression)       </code></p></td>
<td><p><code dir="ltr" translate="no">          SINH                (expression)       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          SQRT                (expression)       </code></p></td>
<td><p><code dir="ltr" translate="no">          SQRT                (expression)       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          SQUARE                (expression)       </code></p></td>
<td><p><code dir="ltr" translate="no">          POW                (expression, 2)       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          TAN                (expression)       </code></p></td>
<td><p><code dir="ltr" translate="no">          TAN                (expression)       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          TANH                (expression)       </code></p></td>
<td><p><code dir="ltr" translate="no">          TANH                (expression)       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          TRUNC                (expression [, scale])       </code></p>
<br />

<p><code dir="ltr" translate="no">          TRUNCATE                (expression [, scale])       </code></p></td>
<td><p><code dir="ltr" translate="no">          TRUNC                (expression [, scale])       </code></p>
<br />
Note: BigQuery's returned value must be smaller than the expression; it does not support equal to.</td>
</tr>
</tbody>
</table>

BigQuery also offers the following [mathematical](/bigquery/docs/reference/standard-sql/mathematical_functions) functions, which do not have a direct analogue in Snowflake:

  - [`  IS_INF  `](/bigquery/docs/reference/standard-sql/mathematical_functions#is_inf)
  - [`  IS_NAN  `](/bigquery/docs/reference/standard-sql/mathematical_functions#is_nan)
  - [`  IEEE_DIVIDE  `](/bigquery/docs/reference/standard-sql/mathematical_functions#ieee_divide)
  - [`  DIV  `](/bigquery/docs/reference/standard-sql/mathematical_functions#div)
  - [`  SAFE_DIVIDE  `](/bigquery/docs/reference/standard-sql/mathematical_functions#safe_divide)
  - [`  SAFE_MULTIPLY  `](/bigquery/docs/reference/standard-sql/mathematical_functions#safe_multiply)
  - [`  SAFE_NEGATE  `](/bigquery/docs/reference/standard-sql/mathematical_functions#safe_negate)
  - [`  SAFE_ADD  `](/bigquery/docs/reference/standard-sql/mathematical_functions#safe_add)
  - [`  SAFE_SUBTRACT  `](/bigquery/docs/reference/standard-sql/mathematical_functions#safe_subtract)
  - [`  RANGE_BUCKET  `](/bigquery/docs/reference/standard-sql/mathematical_functions#range_bucket)

### Semi-structured data functions

<table>
<thead>
<tr class="header">
<th><strong>Snowflake</strong></th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         ARRAY_APPEND       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         ARRAY_CAT       </code></td>
<td><code dir="ltr" translate="no">         ARRAY_CONCAT       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         ARRAY_COMPACT       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         ARRAY_CONSTRUCT       </code></td>
<td><code dir="ltr" translate="no">         [ ]       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         ARRAY_CONSTRUCT_COMPACT       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         ARRAY_CONTAINS       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         ARRAY_INSERT       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         ARRAY_INTERSECTION       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         ARRAY_POSITION       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         ARRAY_PREPEND       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><a href="https://docs.aws.amazon.com/redshift/latest/dg/r_DATEADD_function.html"><code dir="ltr" translate="no">        ARRAY_SIZE       </code></a></td>
<td><code dir="ltr" translate="no">         ARRAY_LENGTH       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         ARRAY_SLICE       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         ARRAY_TO_STRING       </code></td>
<td><code dir="ltr" translate="no">         ARRAY_TO_STRING       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         ARRAYS_OVERLAP       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         AS_&lt;object_type&gt;       </code></td>
<td><code dir="ltr" translate="no">         CAST       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         AS_ARRAY       </code></td>
<td><code dir="ltr" translate="no">         CAST       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         AS_BINARY       </code></td>
<td><code dir="ltr" translate="no">         CAST       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         AS_BOOLEAN       </code></td>
<td><code dir="ltr" translate="no">         CAST       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         AS_CHAR , AS_VARCHAR       </code></td>
<td><code dir="ltr" translate="no">         CAST       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         AS_DATE       </code></td>
<td><code dir="ltr" translate="no">         CAST       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         AS_DECIMAL , AS_NUMBER       </code></td>
<td><code dir="ltr" translate="no">         CAST       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         AS_DOUBLE , AS_REAL       </code></td>
<td><code dir="ltr" translate="no">         CAST       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         AS_INTEGER       </code></td>
<td><code dir="ltr" translate="no">         CAST       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         AS_OBJECT       </code></td>
<td><code dir="ltr" translate="no">         CAST       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         AS_TIME       </code></td>
<td><code dir="ltr" translate="no">         CAST       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         AS_TIMESTAMP_*       </code></td>
<td><code dir="ltr" translate="no">         CAST       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         CHECK_JSON       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         CHECK_XML       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         FLATTEN       </code></td>
<td><code dir="ltr" translate="no">         UNNEST       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         GET       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         GET_IGNORE_CASE       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        GET_PATH , :       </code></p></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         IS_&lt;object_type&gt;       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         IS_ARRAY       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         IS_BINARY       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         IS_BOOLEAN       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         IS_CHAR , IS_VARCHAR       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         IS_DATE , IS_DATE_VALUE       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         IS_DECIMAL       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         IS_DOUBLE , IS_REAL       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         IS_INTEGER       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         IS_OBJECT       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         IS_TIME       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         IS_TIMESTAMP_*       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         OBJECT_CONSTRUCT       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         OBJECT_DELETE       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         OBJECT_INSERT       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         PARSE_JSON       </code></td>
<td><code dir="ltr" translate="no">         JSON_EXTRACT       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         PARSE_XML       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         STRIP_NULL_VALUE       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         STRTOK_TO_ARRAY       </code></td>
<td><code dir="ltr" translate="no">         SPLIT       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         TRY_PARSE_JSON       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         TYPEOF       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         XMLGET       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td></td>
<td></td>
</tr>
</tbody>
</table>

### String and binary functions

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
<td><p><code dir="ltr" translate="no">        string1 || string2       </code></p></td>
<td><p><code dir="ltr" translate="no">        CONCAT(string1, string2)       </code></p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         ASCII       </code></td>
<td><p><code dir="ltr" translate="no">        TO_CODE_POINTS(string1)[OFFSET(0)]       </code></p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         BASE64_DECODE_BINARY       </code></td>
<td><p><code dir="ltr" translate="no">        SAFE_CONVERT_BYTES_TO_STRING(       </code></p>
<p><code dir="ltr" translate="no">        FROM_BASE64(&lt;bytes_input&gt;)       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         BASE64_DECODE_STRING       </code></td>
<td><p><code dir="ltr" translate="no">        SAFE_CONVERT_BYTES_TO_STRING(       </code></p>
<p><code dir="ltr" translate="no">        FROM_BASE64(&lt;string1&gt;)       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         BASE64_ENCODE       </code></td>
<td><p><code dir="ltr" translate="no">        TO_BASE64(       </code></p>
<p><code dir="ltr" translate="no">        SAFE_CAST(&lt;string1&gt; AS BYTES)       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         BIT_LENGTH       </code></td>
<td><p><code dir="ltr" translate="no">        BYTE_LENGTH * 8       </code></p>
<code dir="ltr" translate="no">         CHARACTER_LENGTH       </code></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        CHARINDEX(substring, string)       </code></p></td>
<td><p><code dir="ltr" translate="no">        STRPOS(string, substring)       </code></p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         CHR,CHAR       </code></td>
<td><p><code dir="ltr" translate="no">        CODE_POINTS_TO_STRING([number])       </code></p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         COLLATE       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         COLLATION       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         COMPRESS       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="even">
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        CONCAT(string1, string2)       </code></p></td>
<td><p><code dir="ltr" translate="no">        CONCAT(string1, string2)       </code></p>
<strong>Note</strong> : BigQuery's <code dir="ltr" translate="no">         CONCAT       </code> (...) supports concatenating any number of strings.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         CONTAINS       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         DECOMPRESS_BINARY       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         DECOMPRESS_STRING       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         EDITDISTANCE       </code></td>
<td><code dir="ltr" translate="no">         EDIT_DISTANCE       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         ENDSWITH       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         HEX_DECODE_BINARY       </code></td>
<td><p><code dir="ltr" translate="no">        SAFE_CONVERT_BYTES_TO_STRING(       </code></p>
<p><code dir="ltr" translate="no">        FROM_HEX(&lt;string1&gt;)       </code></p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         HEX_DECODE_STRING       </code></td>
<td><p><code dir="ltr" translate="no">        SAFE_CONVERT_BYTES_TO_STRING(       </code></p>
<p><code dir="ltr" translate="no">        FROM_HEX(&lt;string1&gt;)       </code></p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         HEX_ENCODE       </code></td>
<td><p><code dir="ltr" translate="no">        TO_HEX(       </code></p>
<p><code dir="ltr" translate="no">        SAFE_CAST(&lt;string1&gt; AS BYTES))       </code></p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         ILIKE       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         ILIKE ANY       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         INITCAP       </code></td>
<td><code dir="ltr" translate="no">         INITCAP        </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         INSERT       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         LEFT       </code></td>
<td><a href="https://github.com/GoogleCloudPlatform/bigquery-utils/blob/master/udfs/migration/teradata/left.sqlx">User Defined Function</a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         LENGTH       </code></td>
<td><p><code dir="ltr" translate="no">        LENGTH(expression)       </code></p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         LIKE       </code></td>
<td><code dir="ltr" translate="no">         LIKE       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         LIKE ALL       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         LIKE ANY       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         LOWER       </code></td>
<td><p><code dir="ltr" translate="no">        LOWER(string)       </code></p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         LPAD       </code></td>
<td><p><code dir="ltr" translate="no">        LPAD(string1, length[, string2])       </code></p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         LTRIM       </code></td>
<td><p><code dir="ltr" translate="no">        LTRIM(string1, trim_chars)       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        MD5,MD5_HEX       </code></p></td>
<td><p><code dir="ltr" translate="no">        MD5(string)       </code></p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         MD5_BINARY       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         OCTET_LENGTH       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         PARSE_IP       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         PARSE_URL       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         POSITION       </code></td>
<td><p><code dir="ltr" translate="no">        STRPOS(string, substring)       </code></p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         REPEAT       </code></td>
<td><p><code dir="ltr" translate="no">        REPEAT(string, integer)       </code></p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         REPLACE       </code></td>
<td><p><code dir="ltr" translate="no">        REPLACE(string1, old_chars, new_chars)       </code></p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         REVERSE       </code><br />

<p><code dir="ltr" translate="no">        number_characters       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p></td>
<td><p><code dir="ltr" translate="no">        REVERSE(expression)       </code></p>
<p><code dir="ltr" translate="no"></code></p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         RIGHT       </code></td>
<td><a href="https://github.com/GoogleCloudPlatform/bigquery-utils/blob/master/udfs/migration/teradata/right.sqlx">User Defined Function</a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         RPAD       </code></td>
<td><code dir="ltr" translate="no">         RPAD       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         RTRIM       </code></td>
<td><p><code dir="ltr" translate="no">        RTRIM(string, trim_chars)       </code></p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         RTRIMMED_LENGTH       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         SHA1,SHA1_HEX       </code></td>
<td><p><code dir="ltr" translate="no">        SHA1(string)       </code></p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         SHA1_BINARY       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         SHA2,SHA2_HEX       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         SHA2_BINARY       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         SOUNDEX       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         SPACE       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         SPLIT       </code></td>
<td><code dir="ltr" translate="no">         SPLIT       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         SPLIT_PART       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         SPLIT_TO_TABLE       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         STARTSWITH       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         STRTOK       </code></td>
<td><p><code dir="ltr" translate="no">        SPLIT(instring, delimiter)[ORDINAL(tokennum)]       </code></p>
<br />
Note: The entire delimiter string argument is used as a single delimiter. The default delimiter is a comma.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         STRTOK_SPLIT_TO_TABLE       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         SUBSTR,SUBSTRING       </code></td>
<td><code dir="ltr" translate="no">         SUBSTR       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         TRANSLATE       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         TRIM       </code></td>
<td><code dir="ltr" translate="no">         TRIM       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         TRY_BASE64_DECODE_BINARY       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         TRY_BASE64_DECODE_STRING       </code></td>
<td><p><code dir="ltr" translate="no">        SUBSTR(string, 0, integer)       </code></p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         TRY_HEX_DECODE_BINARY       </code></td>
<td><p><code dir="ltr" translate="no">        SUBSTR(string, -integer)       </code></p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         TRY_HEX_DECODE_STRING       </code></td>
<td><p><code dir="ltr" translate="no">        LENGTH(expression)       </code></p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         UNICODE       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        UPPER       </code></p></td>
<td><code dir="ltr" translate="no">         UPPER       </code></td>
</tr>
<tr class="even">
<td></td>
<td></td>
</tr>
</tbody>
</table>

### String functions (regular expressions)

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
<td><code dir="ltr" translate="no">         REGEXP       </code></td>
<td><p><code dir="ltr" translate="no">        IF(                 REGEXP_CONTAINS                ,1,0)=1       </code></p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         REGEXP_COUNT       </code></td>
<td><p><code dir="ltr" translate="no">          ARRAY_LENGTH                (       </code></p>
<p><code dir="ltr" translate="no">          REGEXP_EXTRACT_ALL                (       </code></p>
<p><code dir="ltr" translate="no">        source_string,       </code></p>
<p><code dir="ltr" translate="no">        pattern       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p>
<br />
<strong>If <code dir="ltr" translate="no">        position       </code> is specified:</strong><br />

<p><code dir="ltr" translate="no">        ARRAY_LENGTH(       </code></p>
<p><code dir="ltr" translate="no">        REGEXP_EXTRACT_ALL(       </code></p>
<p><code dir="ltr" translate="no">          SUBSTR                (source_string, IF(position &lt;= 0, 1, position)),       </code></p>
<p><code dir="ltr" translate="no">        pattern       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p>
<br />
Note: BigQuery provides regular expression support using the <a href="https://github.com/google/re2/wiki/Syntax">re2</a> library; see that documentation for its regular expression syntax.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         REGEXP_INSTR       </code></td>
<td><p><code dir="ltr" translate="no">          IFNULL                (       </code></p>
<p><code dir="ltr" translate="no">          STRPOS                (       </code></p>
<p><code dir="ltr" translate="no">        source_string,       </code></p>
<p><code dir="ltr" translate="no">        REGEXP_EXTRACT(       </code></p>
<p><code dir="ltr" translate="no">        source_string,       </code></p>
<p><code dir="ltr" translate="no">        pattern)       </code></p>
<p><code dir="ltr" translate="no">        ), 0)       </code></p>
<br />
<strong><a href="/bigquery/docs/reference/standard-sql/conditional_expressions">If</a> <code dir="ltr" translate="no">        position       </code> is specified:</strong><br />

<p><code dir="ltr" translate="no">        IFNULL(       </code></p>
<p><code dir="ltr" translate="no">        STRPOS(       </code></p>
<p><code dir="ltr" translate="no">        SUBSTR(source_string, IF(position &lt;= 0, 1, position)),       </code></p>
<p><code dir="ltr" translate="no">        REGEXP_EXTRACT(       </code></p>
<p><code dir="ltr" translate="no">        SUBSTR(source_string, IF(position &lt;= 0, 1, position)),       </code></p>
<p><code dir="ltr" translate="no">        pattern)       </code></p>
<p><code dir="ltr" translate="no">        ) + IF(position &lt;= 0, 1, position) - 1, 0)       </code></p>
<br />
<strong>If <code dir="ltr" translate="no">        occurrence       </code> is specified:</strong><br />

<p><code dir="ltr" translate="no">        IFNULL(       </code></p>
<p><code dir="ltr" translate="no">        STRPOS(       </code></p>
<p><code dir="ltr" translate="no">        SUBSTR(source_string, IF(position &lt;= 0, 1, position)),       </code></p>
<p><code dir="ltr" translate="no">        REGEXP_EXTRACT_ALL(       </code></p>
<p><code dir="ltr" translate="no">        SUBSTR(source_string, IF(position &lt;= 0, 1, position)),       </code></p>
<p><code dir="ltr" translate="no">        pattern       </code></p>
<p><code dir="ltr" translate="no">        )[                 SAFE_ORDINAL                (occurrence)]       </code></p>
<p><code dir="ltr" translate="no">        ) + IF(position &lt;= 0, 1, position) - 1, 0)       </code></p>
<br />
Note: BigQuery provides regular expression support using the <a href="https://github.com/google/re2/wiki/Syntax">re2</a> library; see that documentation for its regular expression syntax.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        REGEXP_LIKE       </code></p></td>
<td><p><code dir="ltr" translate="no">        IF(REGEXP_CONTAINS,1,0)=1       </code></p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         REGEXP_REPLACE       </code></td>
<td><p><code dir="ltr" translate="no">        REGEXP_REPLACE(       </code></p>
<p><code dir="ltr" translate="no">        source_string,       </code></p>
<p><code dir="ltr" translate="no">        pattern,       </code></p>
<p><code dir="ltr" translate="no">        ""       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p>
<br />
<strong>If <code dir="ltr" translate="no">        replace_string       </code> is specified:</strong><br />

<p><code dir="ltr" translate="no">        REGEXP_REPLACE(       </code></p>
<p><code dir="ltr" translate="no">        source_string,       </code></p>
<p><code dir="ltr" translate="no">        pattern,       </code></p>
<p><code dir="ltr" translate="no">        replace_string       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p>
<br />
<strong>If <code dir="ltr" translate="no">        position       </code> is specified:</strong><br />

<p><code dir="ltr" translate="no">        CASE       </code></p>
<p><code dir="ltr" translate="no">        WHEN position &gt; LENGTH(source_string) THEN source_string       </code></p>
<p><code dir="ltr" translate="no">        WHEN position &lt;= 0 THEN       </code></p>
<p><code dir="ltr" translate="no">        REGEXP_REPLACE(       </code></p>
<p><code dir="ltr" translate="no">        source_string,       </code></p>
<p><code dir="ltr" translate="no">        pattern,       </code></p>
<p><code dir="ltr" translate="no">        ""       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p>
<p><code dir="ltr" translate="no">        ELSE       </code></p>
<p><code dir="ltr" translate="no">        CONCAT(       </code></p>
<p><code dir="ltr" translate="no">        SUBSTR(       </code></p>
<p><code dir="ltr" translate="no">        source_string, 1, position - 1),       </code></p>
<p><code dir="ltr" translate="no">        REGEXP_REPLACE(       </code></p>
<p><code dir="ltr" translate="no">        SUBSTR(source_string, position),       </code></p>
<p><code dir="ltr" translate="no">        pattern,       </code></p>
<p><code dir="ltr" translate="no">        replace_string       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p>
<p><code dir="ltr" translate="no">        END       </code></p>
<br />
Note: BigQuery provides regular expression support using the <a href="https://github.com/google/re2/wiki/Syntax">re2</a> library; see that documentation for its regular expression syntax.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         REGEXP_SUBSTR       </code></td>
<td><p><code dir="ltr" translate="no">        REGEXP_EXTRACT(       </code></p>
<p><code dir="ltr" translate="no">        source_string,       </code></p>
<p><code dir="ltr" translate="no">        pattern       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p>
<br />
<strong>If <code dir="ltr" translate="no">        position       </code> is specified:</strong><br />

<p><code dir="ltr" translate="no">        REGEXP_EXTRACT(       </code></p>
<p><code dir="ltr" translate="no">        SUBSTR(source_string, IF(position &lt;= 0, 1, position)),       </code></p>
<p><code dir="ltr" translate="no">        pattern       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p>
<br />
<strong>If <code dir="ltr" translate="no">        occurrence       </code> is specified:</strong><br />

<p><code dir="ltr" translate="no">        REGEXP_EXTRACT_ALL(       </code></p>
<p><code dir="ltr" translate="no">        SUBSTR(source_string, IF(position &lt;= 0, 1, position)),       </code></p>
<p><code dir="ltr" translate="no">        pattern       </code></p>
<p><code dir="ltr" translate="no">        )[SAFE_ORDINAL(occurrence)]       </code></p>
<br />
Note: BigQuery provides regular expression support using the <a href="https://github.com/google/re2/wiki/Syntax">re2</a> library; see that documentation for its regular expression syntax.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         RLIKE       </code></td>
<td><p><code dir="ltr" translate="no">        IF(REGEXP_CONTAINS,1,0)=1       </code></p></td>
</tr>
</tbody>
</table>

### System functions

<table>
<thead>
<tr class="header">
<th><strong>Snowflake</strong></th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         SYSTEM$ABORT_SESSION       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         SYSTEM$ABORT_TRANSACTION       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         SYSTEM$CANCEL_ALL_QUERIES       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         SYSTEM$CANCEL_QUERY       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         SYSTEM$CLUSTERING_DEPTH       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         SYSTEM$CLUSTERING_INFORMATION       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         SYSTEM$CLUSTERING_RATIO — Deprecated       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         SYSTEM$CURRENT_USER_TASK_NAME       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         SYSTEM$DATABASE_REFRESH_HISTORY       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         SYSTEM$DATABASE_REFRESH_PROGRESS , SYSTEM$DATABASE_REFRESH_PROGRESS_BY_JOB       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><a href="https://docs.aws.amazon.com/redshift/latest/dg/r_DATEADD_function.html"><code dir="ltr" translate="no">        SYSTEM$GET_AWS_SNS_IAM_POLICY       </code></a></td>
<td>Custom user-defined function</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         SYSTEM$GET_PREDECESSOR_RETURN_VALUE       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         SYSTEM$LAST_CHANGE_COMMIT_TIME       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         SYSTEM$PIPE_FORCE_RESUME       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         SYSTEM$PIPE_STATUS       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         SYSTEM$SET_RETURN_VALUE       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         SYSTEM$SHOW_OAUTH_CLIENT_SECRETS       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         SYSTEM$STREAM_GET_TABLE_TIMESTAMP       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         SYSTEM$STREAM_HAS_DATA       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         SYSTEM$TASK_DEPENDENTS_ENABLE       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         SYSTEM$TYPEOF       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         SYSTEM$USER_TASK_CANCEL_ONGOING_EXECUTIONS       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         SYSTEM$WAIT       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         SYSTEM$WHITELIST       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         SYSTEM$WHITELIST_PRIVATELINK       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="even">
<td></td>
<td></td>
</tr>
</tbody>
</table>

### Table functions

**Snowflake**

BigQuery

`  GENERATOR  `

Custom user-defined function

`  GET_OBJECT_REFERENCES  `

Custom user-defined function

`  RESULT_SCAN  `

Custom user-defined function

`  VALIDATE  `

Custom user-defined function

### Utility and hash functions

**Snowflake**

BigQuery

`  GET_DDL  `

[Feature Request](https://issuetracker.google.com/issues/119245739)

`  HASH  `

HASH is a Snowflake-specific proprietary function. Can't be translated without knowing the underlying logic used by Snowflake.

### Window functions

**Snowflake**

BigQuery

`  CONDITIONAL_CHANGE_EVENT  `

Custom user-defined function

`  CONDITIONAL_TRUE_EVENT  `

Custom user-defined function

`  CUME_DIST  `

`  CUME_DIST  `

`  DENSE_RANK  `

`  DENSE_RANK  `

`  FIRST_VALUE  `

`  FIRST_VALUE  `

`  LAG  `

`  LAG  `

`  LAST_VALUE  `

`  LAST_VALUE  `

`  LEAD  `

`  LEAD  `

`  NTH_VALUE  `

`  NTH_VALUE  `

`  NTILE  `

`  NTILE  `

`  PERCENT_RANK  `

`  PERCENT_RANK  `

`  RANK  `

`  RANK  `

`  RATIO_TO_REPORT  `

Custom user-defined function

`  ROW_NUMBER  `

`  ROW_NUMBER  `

`  WIDTH_BUCKET  `

Custom user-defined function

BigQuery also supports [`  SAFE_CAST  `](/bigquery/docs/reference/standard-sql/conversion_functions#safe_casting) (expression AS typename), which returns NULL if BigQuery is unable to perform a cast (for example, [`  SAFE_CAST  `](/bigquery/docs/reference/standard-sql/conversion_functions#safe_casting) ("apple" AS INT64) returns NULL).

## Operators

The following sections list Snowflake operators and their BigQuery equivalents.

### Arithmetic operators

The following table shows mappings between Snowflake [arithmetic operators](https://docs.snowflake.net/manuals/sql-reference/operators-arithmetic.html) with their BigQuery equivalents.

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
<td><p><code dir="ltr" translate="no">        (Unary) (+'5')       </code></p></td>
<td><p><code dir="ltr" translate="no">        CAST("5" AS NUMERIC)       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        a + b       </code></p></td>
<td><p><code dir="ltr" translate="no">        a + b       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        (Unary) (-'5')       </code></p></td>
<td><p><code dir="ltr" translate="no">        (-1) * CAST("5" AS NUMERIC)       </code></p>
<br />
Note: BigQuery supports standard unary minus, but does not convert integers in string format to <code dir="ltr" translate="no">       INT64      </code> , <code dir="ltr" translate="no">       NUMERIC      </code> , or <code dir="ltr" translate="no">       FLOAT64      </code> type.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        a - b       </code></p></td>
<td><p><code dir="ltr" translate="no">        a - b       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        date1 - date2       </code></p>
<br />

<p><code dir="ltr" translate="no">        date1 - 365       </code></p></td>
<td><p><code dir="ltr" translate="no">          DATE_DIFF                (date1, date2, date_part)                 DATE_SUB                (date1, date2, date_part)       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        a * b       </code></p></td>
<td><p><code dir="ltr" translate="no">        a * b       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        a / b       </code></p></td>
<td><p><code dir="ltr" translate="no">        a / b       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        a % b       </code></p></td>
<td><p><code dir="ltr" translate="no">          MOD                (a, b)       </code></p></td>
</tr>
</tbody>
</table>

To view Snowflake scale and precision details when performing arithmetic operations, see the Snowflake [documentation](https://docs.snowflake.net/manuals/sql-reference/operators-arithmetic.html#scale-and-precision-in-arithmetic-operations) .

### Comparison operators

Snowflake [comparison operators](https://docs.snowflake.net/manuals/sql-reference/operators-comparison.html) and BigQuery [comparison operators](/bigquery/docs/reference/standard-sql/operators#comparison_operators) are the same.

### Logical/boolean operators

Snowflake [logical/boolean operators](https://docs.snowflake.net/manuals/sql-reference/operators-logical.html) and BigQuery [logical/boolean operators](/bigquery/docs/reference/standard-sql/operators#logical_operators) are the same.

### Set operators

The following table shows mappings between Snowflake [set operators](https://docs.snowflake.net/manuals/sql-reference/operators-query.html) with their BigQuery equivalents.

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
<td><p><code dir="ltr" translate="no">        SELECT ...                 INTERSECT                SELECT ...       </code></p></td>
<td><p><code dir="ltr" translate="no">        SELECT ...       </code></p>
<code dir="ltr" translate="no">         INTERSECT DISTINCT       </code><br />

<p><code dir="ltr" translate="no">        SELECT...       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        SELECT ...                 MINUS                SELECT ...       </code></p>
<p><code dir="ltr" translate="no">        SELECT ...                 EXCEPT                SELECT …       </code></p>
<br />
<strong>Note: <code dir="ltr" translate="no"></code></strong> <code dir="ltr" translate="no">       MINUS      </code> and <code dir="ltr" translate="no">       EXCEPT      </code> are synonyms.</td>
<td><p><code dir="ltr" translate="no">        SELECT ...                 EXCEPT DISTINCT                SELECT ...       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        SELECT ...                 UNION                SELECT ...       </code></p>
<p><code dir="ltr" translate="no">        SELECT ...                 UNION ALL                SELECT ...       </code></p></td>
<td><p><code dir="ltr" translate="no">        SELECT ...                 UNION DISTINCT                SELECT ...       </code></p>
<br />

<p><code dir="ltr" translate="no">        SELECT ...                 UNION ALL                SELECT ...       </code></p></td>
</tr>
</tbody>
</table>

### Subquery operators

The following table shows mappings between Snowflake [subquery operators](https://docs.snowflake.net/manuals/sql-reference/operators-subquery.html) with their BigQuery equivalents.

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
<td><p><code dir="ltr" translate="no">        SELECT ... FROM ... WHERE col &lt;operator&gt;                 ALL                …  SELECT ... FROM ... WHERE col &lt;operator&gt;                 ANY                ...       </code></p></td>
<td>BigQuery does not support a direct alternative to Snowflake's ALL/ANY.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        SELECT ... FROM ...       </code></p>
<p><code dir="ltr" translate="no">        WHERE                 [NOT] EXISTS                ...       </code></p></td>
<td><p><code dir="ltr" translate="no">        SELECT ... FROM ...       </code></p>
<p><code dir="ltr" translate="no">        WHERE                 [NOT] EXISTS                ...       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        SELECT ... FROM ...       </code></p>
<p><code dir="ltr" translate="no">        WHERE                 [NOT] IN                ...       </code></p></td>
<td><p><code dir="ltr" translate="no">        SELECT ... FROM ...       </code></p>
<p><code dir="ltr" translate="no">        WHERE                 [NOT] IN                ...       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        SELECT * FROM table1       </code></p>
<p><code dir="ltr" translate="no">        UNION       </code></p>
<p><code dir="ltr" translate="no">        SELECT * FROM table2       </code></p>
<p><code dir="ltr" translate="no">        EXCEPT       </code></p>
<p><code dir="ltr" translate="no">        SELECT * FROM table3       </code></p></td>
<td><p><code dir="ltr" translate="no">        SELECT * FROM table1       </code></p>
<p><code dir="ltr" translate="no">        UNION ALL       </code></p>
<p><code dir="ltr" translate="no">        (       </code></p>
<p><code dir="ltr" translate="no">        SELECT * FROM table2       </code></p>
<p><code dir="ltr" translate="no">        EXCEPT       </code></p>
<p><code dir="ltr" translate="no">        SELECT * FROM table3       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p>
<br />
<strong>Note</strong> : BigQuery requires parentheses to separate different set operations. If the same set operator is repeated, parentheses are not necessary.</td>
</tr>
</tbody>
</table>

## DML syntax

This section addresses differences in data management language syntax between Snowflake and BigQuery.

### `     INSERT    ` statement

Snowflake offers a configurable `  DEFAULT  ` keyword for columns. In BigQuery, the `  DEFAULT  ` value for nullable columns is NULL and `  DEFAULT  ` is not supported for required columns. Most [Snowflake `  INSERT  ` statements](https://docs.snowflake.net/manuals/sql-reference/sql/insert.html) are compatible with BigQuery. The following table shows exceptions.

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
<td><p><code dir="ltr" translate="no">          INSERT                [OVERWRITE] INTO table       </code></p>
<p><code dir="ltr" translate="no">        VALUES [... | DEFAULT | NULL] ...       </code></p>
<br />
Note: BigQuery does not support inserting <code dir="ltr" translate="no">       JSON      </code> objects with an <code dir="ltr" translate="no">       INSERT      </code> statement <code dir="ltr" translate="no">       .      </code></td>
<td><p><code dir="ltr" translate="no">          INSERT                [INTO] table (column1 [, ...])       </code></p>
<code dir="ltr" translate="no">       VALUES (DEFAULT [, ...])        </code> Note: BigQuery does not support a direct alternative to Snowflake's <code dir="ltr" translate="no">       OVERWRITE      </code> . Use <code dir="ltr" translate="no">       DELETE      </code> instead.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          INSERT                INTO table (column1 [, ...]) SELECT... FROM ...       </code></p></td>
<td><p><code dir="ltr" translate="no">          INSERT                [INTO] table (column1, [,...])       </code></p>
<p><code dir="ltr" translate="no">        SELECT ...       </code></p>
<p><code dir="ltr" translate="no">        FROM ...       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          INSERT                [OVERWRITE] ALL &lt;intoClause&gt; ...                 INSERT                [OVERWRITE] {FIRST | ALL} {WHEN condition THEN &lt;intoClause&gt;}       </code></p>
<p><code dir="ltr" translate="no">        [...]       </code></p>
<p><code dir="ltr" translate="no">        [ELSE &lt;intoClause&gt;]       </code></p>
<code dir="ltr" translate="no">       ...        </code> <strong>Note: <code dir="ltr" translate="no"></code></strong> <code dir="ltr" translate="no">       &lt;intoClause&gt;      </code> represents standard <code dir="ltr" translate="no">       INSERT statement      </code> , listed above.</td>
<td>BigQuery does not support conditional and unconditional multi-table <code dir="ltr" translate="no">       INSERTs      </code> . <code dir="ltr" translate="no"></code></td>
</tr>
</tbody>
</table>

BigQuery also supports inserting values using a subquery (where one of the values is computed using a subquery), which is not supported in Snowflake. For example:

``` text
INSERT INTO table (column1, column2)
VALUES ('value_1', (
  SELECT column2
  FROM table2
))
```

### `     COPY    ` statement

Snowflake supports copying data from stages files to an existing table and from a table to a named internal stage, a named external stage, and an external location (Amazon S3, Google Cloud Storage, or Microsoft Azure).

  - [`  COPY INTO <table>  `](https://docs.snowflake.net/manuals/sql-reference/sql/copy-into-table.html)
  - [`  COPY INTO <location>  `](https://docs.snowflake.net/manuals/sql-reference/sql/copy-into-location.html)

BigQuery does not use the SQL `  COPY  ` command to load data, but you can use any of several non-SQL [tools and options](/bigquery/docs/loading-data) to load data into BigQuery tables. You can also use data pipeline sinks provided in [Apache Spark](/dataproc/docs/concepts/connectors/bigquery#other_sparkhadoop_clusters) or [Apache Beam](https://beam.apache.org/documentation/io/built-in/google-bigquery/#writing-to-bigquery) to write data into BigQuery.

### `     UPDATE    ` statement

Most Snowflake `  UPDATE  ` statements are compatible with BigQuery. The following table shows exceptions.

**Snowflake**

BigQuery

`  UPDATE table SET col = value [,...] [FROM ...] [WHERE ...]  `

`  UPDATE table  `

`  SET column = expression [,...]  `

`  [FROM ...]  `

`  WHERE TRUE  `

  
**Note** : All `  UPDATE  ` statements in BigQuery require a `  WHERE  ` keyword, followed by a condition.

### `     DELETE    ` and `     TRUNCATE TABLE    ` statements

The `  DELETE  ` and `  TRUNCATE TABLE  ` statements are both ways to remove rows from a table without affecting the table schema or indexes.

In Snowflake, both `  DELETE  ` and `  TRUNCATE TABLE  ` maintain deleted data using Snowflake's Time Travel for recovery purposes for the data retention period. However, DELETE does not delete the external file load history and load metadata.

In BigQuery, the `  DELETE  ` statement must have a `  WHERE  ` clause. For more information about `  DELETE  ` in BigQuery, see the [BigQuery `  DELETE  ` examples](/bigquery/docs/reference/standard-sql/dml-syntax#delete_examples) in the DML documentation.

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
<td><p><code dir="ltr" translate="no">          DELETE                FROM table_name [USING ...]       </code></p>
<p><code dir="ltr" translate="no">        [WHERE ...]       </code></p>
<br />
<br />

<p><code dir="ltr" translate="no">          TRUNCATE                [TABLE] [IF EXISTS] table_name       </code></p></td>
<td><p><code dir="ltr" translate="no">          DELETE                [FROM] table_name [alias]       </code></p>
<p><code dir="ltr" translate="no">        WHERE ...       </code></p>
<br />
Note: BigQuery <code dir="ltr" translate="no">       DELETE      </code> statements require a <code dir="ltr" translate="no">       WHERE      </code> clause.</td>
</tr>
</tbody>
</table>

### `     MERGE    ` statement

The `  MERGE  ` statement can combine `  INSERT  ` , `  UPDATE  ` , and `  DELETE  ` operations into a single "upsert" statement and perform the operations automatically. The `  MERGE  ` operation must match at most one source row for each target row.

BigQuery tables are limited to 1,000 DML statements per day, so you should optimally consolidate INSERT, UPDATE, and DELETE statements into a single MERGE statement as shown in the following table:

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
<td><p><code dir="ltr" translate="no">          MERGE                INTO target USING source ON target.key = source.key WHEN MATCHED AND source.filter = 'Filter_exp' THEN       </code></p>
<p><code dir="ltr" translate="no">        UPDATE SET     target.col1 = source.col1,     target.col1 = source.col2,       </code></p>
<p><code dir="ltr" translate="no">        ...       </code></p>
<code dir="ltr" translate="no"> </code> Note: Snowflake supports a ERROR_ON_NONDETERMINISTIC_MERGE session parameter to handle nondeterministic results.</td>
<td><p><code dir="ltr" translate="no">          MERGE                target       </code></p>
<p><code dir="ltr" translate="no">        USING source       </code></p>
<p><code dir="ltr" translate="no">        ON target.key = source.key       </code></p>
<p><code dir="ltr" translate="no">        WHEN MATCHED AND source.filter = 'filter_exp' THEN       </code></p>
<p><code dir="ltr" translate="no">        UPDATE SET       </code></p>
<p><code dir="ltr" translate="no">        target.col1 = source.col1,       </code></p>
<p><code dir="ltr" translate="no">        target.col2 = source.col2,       </code></p>
<p><code dir="ltr" translate="no">        ...       </code></p>
<br />
<br />
Note: All columns must be listed if updating all columns.</td>
</tr>
</tbody>
</table>

### `     GET    ` and `     LIST    ` statements

The [`  GET  `](https://docs.snowflake.net/manuals/sql-reference/sql/get.html) statement downloads data files from one of the following Snowflake stages to a local directory/folder on a client machine:

  - Named internal stage
  - Internal stage for a specified table
  - Internal stage for the current user

The [`  LIST  `](https://docs.snowflake.net/manuals/sql-reference/sql/list.html) (LS) statement returns a list of files that have been staged (that is, uploaded from a local file system or unloaded from a table) in one of the following Snowflake stages:

  - Named internal stage
  - Named external stage
  - Stage for a specified table
  - Stage for the current user

BigQuery does not support the concept of staging and does not have `  GET  ` and `  LIST  ` equivalents.

### `     PUT    ` and `     REMOVE    ` statements

The [`  PUT  `](https://docs.snowflake.net/manuals/sql-reference/sql/put.html) statement uploads (that is, stages) data files from a local directory/folder on a client machine to one of the following Snowflake stages:

  - Named internal stage
  - Internal stage for a specified table
  - Internal stage for the current user

The [`  REMOVE  `](https://docs.snowflake.net/manuals/sql-reference/sql/remove.html) `  (RM)  ` statement removes files that have been staged in one of the following Snowflake internal stages:

  - Named internal stage
  - Stage for a specified table
  - Stage for the current user

BigQuery does not support the concept of staging and does not have `  PUT  ` and `  REMOVE  ` equivalents.

## DDL syntax

This section addresses differences in data definition language syntax between Snowflake and BigQuery.

### Database, Schema, and Share DDL

Most of Snowflake's terminology matches that of BigQuery's except that Snowflake Database is similar to BigQuery Dataset. See the [detailed Snowflake to BigQuery terminology mapping.](https://docs.google.com/document/d/1J-qvYV5d6WTPDv1WLIRD1diFzZ5kD0IMRuKVLOJjHEE/edit)

#### `     CREATE DATABASE    ` statement

Snowflake supports creating and managing a database via [database management commands](https://docs.snowflake.net/manuals/sql-reference/ddl-database.html#database-management) while BigQuery provides multiple options like using Console, CLI, Client Libraries, etc. for [creating datasets](/bigquery/docs/datasets) . This section will use BigQuery CLI commands corresponding to the Snowflake commands to address the differences.

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
<td><p><code dir="ltr" translate="no">        CREATE DATABASE &lt;name&gt;       </code></p>
<br />
Note: Snowflake provides these <a href="https://docs.snowflake.net/manuals/sql-reference/identifiers-syntax.html">requirements</a> for naming databases. It allows only 255 characters in the name.</td>
<td><p><code dir="ltr" translate="no">        bq mk &lt;name&gt;       </code></p>
<br />
Note: BigQuery has similar <a href="/bigquery/docs/datasets#dataset-naming">dataset naming requirements</a> as Snowflake except that it allows 1024 characters in the name.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        CREATE OR REPLACE DATABASE &lt;name&gt;       </code></p></td>
<td>Replacing the dataset is not supported in BigQuery.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        CREATE TRANSIENT DATABASE &lt;name&gt;       </code></p></td>
<td>Creating temporary dataset is not supported in BigQuery.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        CREATE DATABASE IF NOT EXISTS &lt;name&gt;       </code></p></td>
<td>Concept not supported in BigQuery</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        CREATE DATABASE &lt;name&gt;       </code></p>
<p><code dir="ltr" translate="no">        CLONE &lt;source_db&gt;       </code></p>
<p><code dir="ltr" translate="no">        [ { AT | BEFORE }       </code></p>
<p><code dir="ltr" translate="no">        ( { TIMESTAMP =&gt; &lt;timestamp&gt; |       </code></p>
<p><code dir="ltr" translate="no">        OFFSET =&gt; &lt;time_difference&gt; |       </code></p>
<p><code dir="ltr" translate="no">        STATEMENT =&gt; &lt;id&gt; } ) ]       </code></p></td>
<td>Cloning datasets is not supported in BigQuery.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        CREATE DATABASE &lt;name&gt;       </code></p>
<p><code dir="ltr" translate="no">        DATA_RETENTION_TIME_IN_DAYS = &lt;num&gt;       </code></p></td>
<td>Time travel at the dataset level is not supported in BigQuery. However, time travel for table and query results is supported.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        CREATE DATABASE &lt;name&gt;       </code></p>
<p><code dir="ltr" translate="no">        DEFAULT_DDL_COLLATION = '&lt;collation_specification&gt;'       </code></p></td>
<td>Collation in DDL is not supported in BigQuery.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        CREATE DATABASE &lt;name&gt;       </code></p>
<p><code dir="ltr" translate="no">        COMMENT = '&lt;string_literal&gt;'       </code></p></td>
<td><p><code dir="ltr" translate="no">        bq mk \       </code></p>
<p><code dir="ltr" translate="no">        --description "&lt;string_literal&gt;" \       </code></p>
<p><code dir="ltr" translate="no">        &lt;name&gt;       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        CREATE DATABASE &lt;name&gt;       </code></p>
<p><code dir="ltr" translate="no">        FROM SHARE &lt;provider_account&gt;.&lt;share_name&gt;       </code></p></td>
<td>Creating shared datasets is not supported in BigQuery. However, users can <a href="/bigquery/docs/dataset-access-controls#controlling_access_to_a_dataset">share the dataset via Console/UI</a> once the dataset is created.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        CREATE DATABASE &lt;name&gt;       </code></p>
<p><code dir="ltr" translate="no">        AS REPLICA OF       </code></p>
<p><code dir="ltr" translate="no">        &lt;region&gt;.&lt;account&gt;.&lt;primary_db_name&gt;       </code></p>
<p><code dir="ltr" translate="no">        AUTO_REFRESH_MATERIALIZED_VIEWS_ON_SECONDARY = { TRUE | FALSE }       </code></p>
<br />
Note: Snowflake provides the option for <a href="https://docs.snowflake.net/manuals/sql-reference/sql/create-database.html#id1">automatic background maintenance of materialized views</a> in the secondary database which is not supported in BigQuery.</td>
<td><p><code dir="ltr" translate="no">        bq mk --transfer_config \       </code></p>
<p><code dir="ltr" translate="no">        --target_dataset = &lt;name&gt; \       </code></p>
<p><code dir="ltr" translate="no">        --data_source = cross_region_copy \ --params='       </code></p>
<p><code dir="ltr" translate="no">        {"source_dataset_id":"&lt;primary_db_name&gt;"       </code></p>
<p><code dir="ltr" translate="no">        ,"source_project_id":"&lt;project_id&gt;"       </code></p>
<p><code dir="ltr" translate="no">        ,"overwrite_destination_table":"true"}'       </code></p>
Note: BigQuery supports <a href="/bigquery/docs/copying-datasets">copying datasets</a> using the <a href="/bigquery/docs/transfer-service-overview">BigQuery Data Transfer Service</a> . <a href="/bigquery/docs/copying-datasets#before_you_begin">See here</a> for a dataset copying prerequisites.</td>
</tr>
</tbody>
</table>

BigQuery also offers the following **`  bq mk  `** command options, which do not have a direct analogue in Snowflake:

  - `  --location <dataset_location>  `
  - `  --default_table_expiration <time_in_seconds>  `
  - `  --default_partition_expiration <time_in_seconds>  `

#### `     ALTER DATABASE    ` statement

This section will use BigQuery CLI commands corresponding to the Snowflake commands to address the differences in ALTER statements.

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
<td><p><code dir="ltr" translate="no">          ALTER DATABASE                [ IF EXISTS ] &lt;name&gt; RENAME TO &lt;new_db_name&gt;       </code></p></td>
<td>Renaming datasets is not supported in BigQuery but copying datasets is supported.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          ALTER DATABASE                &lt;name&gt;       </code></p>
<p><code dir="ltr" translate="no">        SWAP WITH &lt;target_db_name&gt;       </code></p></td>
<td>Swapping datasets is not supported in BigQuery.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          ALTER DATABASE                &lt;name&gt;       </code></p>
<p><code dir="ltr" translate="no">        SET       </code></p>
<p><code dir="ltr" translate="no">        [DATA_RETENTION_TIME_IN_DAYS = &lt;num&gt;]       </code></p>
<p><code dir="ltr" translate="no">        [ DEFAULT_DDL_COLLATION = '&lt;value&gt;']       </code></p></td>
<td>Managing data retention and collation at dataset level is not supported in BigQuery.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          ALTER                DATABASE &lt;name&gt;       </code></p>
<p><code dir="ltr" translate="no">        SET COMMENT = '&lt;string_literal&gt;'       </code></p></td>
<td><p><code dir="ltr" translate="no">          bq                update \       </code></p>
<p><code dir="ltr" translate="no">        --description "&lt;string_literal&gt;" &lt;name&gt;       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          ALTER DATABASE                &lt;name&gt;       </code></p>
<p><code dir="ltr" translate="no">        ENABLE REPLICATION TO ACCOUNTS &lt;snowflake_region&gt;.&lt;account_name&gt;       </code></p>
<p><code dir="ltr" translate="no">        [ , &lt;snowflake_region&gt;.&lt;account_name&gt; ... ]       </code></p></td>
<td>Concept not supported in BigQuery.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          ALTER DATABASE                &lt;name&gt;       </code></p>
<p><code dir="ltr" translate="no">        DISABLE REPLICATION [ TO ACCOUNTS &lt;snowflake_region&gt;.&lt;account_name&gt;       </code></p>
<p><code dir="ltr" translate="no">        [ , &lt;snowflake_region&gt;.&lt;account_name&gt; ... ]]       </code></p></td>
<td>Concept not supported in BigQuery.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          ALTER DATABASE                &lt;name&gt;       </code></p>
<p><code dir="ltr" translate="no">        SET AUTO_REFRESH_MATERIALIZED_VIEWS_ON_SECONDARY = { TRUE | FALSE }       </code></p></td>
<td>Concept not supported in BigQuery.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          ALTER DATABASE                &lt;name&gt; REFRESH       </code></p></td>
<td>Concept not supported in BigQuery.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          ALTER DATABASE                &lt;name&gt;       </code></p>
<p><code dir="ltr" translate="no">        ENABLE FAILOVER TO ACCOUNTS &lt;snowflake_region&gt;.&lt;account_name&gt;       </code></p>
<p><code dir="ltr" translate="no">        [ , &lt;snowflake_region&gt;.&lt;account_name&gt; ... ]       </code></p></td>
<td>Concept not supported in BigQuery.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          ALTER DATABASE                &lt;name&gt;       </code></p>
<p><code dir="ltr" translate="no">        DISABLE FAILOVER [ TO ACCOUNTS &lt;snowflake_region&gt;.&lt;account_name&gt;       </code></p>
<p><code dir="ltr" translate="no">        [ , &lt;snowflake_region&gt;.&lt;account_name&gt; ... ]]       </code></p></td>
<td>Concept not supported in BigQuery.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          ALTER DATABASE                &lt;name&gt;       </code></p>
<p><code dir="ltr" translate="no">        PRIMARY       </code></p></td>
<td>Concept not supported in BigQuery.</td>
</tr>
</tbody>
</table>

#### `     DROP DATABASE    ` statement

This section will use BigQuery CLI command corresponding to the Snowflake command to address the difference in DROP statement.

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
<td><p><code dir="ltr" translate="no">          DROP DATABASE                [ IF EXISTS ] &lt;name&gt;       </code></p>
<p><code dir="ltr" translate="no">        [ CASCADE | RESTRICT ]       </code></p>
<br />
Note: In Snowflake, dropping a database does not permanently remove it from the system. A version of the dropped database is retained for the number of days specified by the <code dir="ltr" translate="no">       DATA_RETENTION_TIME_IN_DAYS      </code> parameter for the database.</td>
<td><p><code dir="ltr" translate="no">          bq rm                -r -f -d &lt;name&gt;       </code></p>
<br />

<p><code dir="ltr" translate="no">        Where       </code></p>
<code dir="ltr" translate="no">       -r      </code> is to remove all objects in the dataset<br />

<p><code dir="ltr" translate="no">        -f is to skip confirmation for execution       </code></p>
<code dir="ltr" translate="no">       -d      </code> indicates dataset<br />
<br />
Note: In BigQuery, deleting a dataset is permanent. Also, cascading is not supported at the dataset level as all the data and objects in the dataset are deleted.</td>
</tr>
</tbody>
</table>

Snowflake also supports the [`  UNDROP DATASET  `](https://docs.snowflake.net/manuals/sql-reference/sql/undrop-database.html) command, which restores the most recent version of a dropped datasets. This is not supported in BigQuery at the dataset level.

#### `     USE DATABASE    ` statement

Snowflake provides the option to set the database for a user session using [`  USE DATABASE  `](https://docs.snowflake.net/manuals/sql-reference/sql/use-database.html#use-database) command. This removes the need for specifying fully-qualified object names in SQL commands. BigQuery does not provide any alternative to Snowflake's USE DATABASE command.

#### `     SHOW DATABASE    ` statement

This section will use BigQuery CLI command corresponding to the Snowflake command to address the difference in SHOW statement.

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
<td><p><code dir="ltr" translate="no">          SHOW DATABASES        </code></p>
<br />
Note: Snowflake provides a single option to list and show details about all the databases including dropped databases that are within the retention period.</td>
<td><code dir="ltr" translate="no">         bq ls       </code> --format=prettyjson<br />
and / or<br />

<p><code dir="ltr" translate="no">          bq show                &lt;dataset_name&gt;       </code></p>
<br />
Note: In BigQuery, the ls command provides only dataset names and basic information, and the show command provides details like last modified timestamp, ACLs, and labels of a dataset. BigQuery also provides more details about the datasets via <a href="/bigquery/docs/dataset-metadata#information_schema_beta">Information Schema</a> .</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          SHOW TERSE DATABASES        </code></p>
<br />
Note: With the TERSE option, Snowflake allows to display only specific information/fields about datasets.</td>
<td>Concept not supported in BigQuery.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          SHOW DATABASES HISTORY        </code></p></td>
<td>Time travel concept is not supported in BigQuery at the dataset level.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         SHOW DATABASES       </code><br />

<p><code dir="ltr" translate="no">        [LIKE '&lt;pattern&gt;']       </code></p>
<p><code dir="ltr" translate="no">        [STARTS WITH '&lt;name_string&gt;']       </code></p></td>
<td>Filtering results by dataset names is not supported in BigQuery. However, <a href="/bigquery/docs/dataset-metadata#getting_dataset_information">filtering by labels</a> is supported.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         SHOW DATABASES       </code><br />

<p><code dir="ltr" translate="no">        LIMIT &lt;rows&gt; [FROM '&lt;name_string&gt;']       </code></p>
<br />
Note: By default, Snowflake does not limit the number of results. However, the value for <a href="https://docs.snowflake.net/manuals/sql-reference/sql/show-databases.html#usage-notes">LIMIT</a> cannot exceed 10K.</td>
<td><p><code dir="ltr" translate="no">          bq ls                \       </code></p>
<p><code dir="ltr" translate="no">        --max_results &lt;rows&gt;       </code></p>
<br />
Note: By default, BigQuery only displays 50 results.</td>
</tr>
</tbody>
</table>

BigQuery also offers the following **`  bq  `** command options, which do not have a direct analogue in Snowflake:

  - *bq ls --format=pretty* : Returns basic formatted results
  - \*bq ls -a: \*Returns only anonymous datasets (the ones starting with an underscore)
  - *bq ls --all* : Returns all datasets including anonymous ones
  - *bq ls --filter labels.key:value* : Returns results filtered by dataset label
  - *bq ls --d* : Excludes anonymous datasets form results
  - *bq show --format=pretty* : Returns detailed basic formatted results for all datasets

#### `     SCHEMA    ` management

Snowflake provides multiple [schema management](https://docs.snowflake.net/manuals/sql-reference/ddl-database.html#schema-management) commands similar to its database management commands. This concept of creating and managing schema is not supported in BigQuery.

However, BigQuery allows you to specify a table's schema when you load data into a table, and when you create an empty table. Alternatively, you can use schema [auto-detection](/bigquery/docs/schema-detect#auto-detect) for supported data formats.

#### `     SHARE    ` management

Snowflake provides multiple [share management](https://docs.snowflake.net/manuals/sql-reference/ddl-database.html#share-management) commands similar to its database and schema management commands. This concept of creating and managing share is not supported in BigQuery.

### Table, View, and Sequence DDL

#### `     CREATE TABLE    ` statement

Most Snowflake `  CREATE TABLE  ` statements are compatible with BigQuery, except for the following syntax elements, which are not used in BigQuery:

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
<td><p><code dir="ltr" translate="no">        CREATE TABLE table_name       </code></p>
<p><code dir="ltr" translate="no">        (       </code></p>
<p><code dir="ltr" translate="no">        col1 data_type1 NOT NULL,       </code></p>
<p><code dir="ltr" translate="no">        col2 data_type2 NULL,       </code></p>
<p><code dir="ltr" translate="no">        col3 data_type3 UNIQUE,       </code></p>
<p><code dir="ltr" translate="no">        col4 data_type4 PRIMARY KEY,       </code></p>
<p><code dir="ltr" translate="no">        col5 data_type5       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p>
<br />
Note: <code dir="ltr" translate="no">       UNIQUE      </code> and <code dir="ltr" translate="no">       PRIMARY KEY      </code> constraints are informational and are not enforced by the Snowflake system.</td>
<td><p><code dir="ltr" translate="no">        CREATE TABLE table_name       </code></p>
<p><code dir="ltr" translate="no">        (       </code></p>
<p><code dir="ltr" translate="no">        col1 data_type1 NOT NULL,       </code></p>
<p><code dir="ltr" translate="no">        col2 data_type2,       </code></p>
<p><code dir="ltr" translate="no">        col3 data_type3,       </code></p>
<p><code dir="ltr" translate="no">        col4 data_type4,       </code></p>
<p><code dir="ltr" translate="no">        col5 data_type5,       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        CREATE TABLE table_name       </code></p>
<p><code dir="ltr" translate="no">        (       </code></p>
<p><code dir="ltr" translate="no">        col1 data_type1[,...]       </code></p>
<p><code dir="ltr" translate="no">        table_constraints       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p>
<br />
where <code dir="ltr" translate="no">       table_constraints      </code> are:<br />

<p><code dir="ltr" translate="no">        [UNIQUE(column_name [, ... ])]       </code></p>
<p><code dir="ltr" translate="no">        [PRIMARY KEY(column_name [, ...])]       </code></p>
<p><code dir="ltr" translate="no">        [FOREIGN KEY(column_name [, ...])       </code></p>
<p><code dir="ltr" translate="no">        REFERENCES reftable [(refcolumn)]       </code></p>
<br />
<strong>Note: <code dir="ltr" translate="no"></code></strong> <code dir="ltr" translate="no">       UNIQUE      </code> and <code dir="ltr" translate="no">       PRIMARY KEY      </code> constraints are informational and are not enforced by the Snowflake system.</td>
<td><p><code dir="ltr" translate="no">        CREATE TABLE table_name       </code></p>
<p><code dir="ltr" translate="no">        (       </code></p>
<p><code dir="ltr" translate="no">        col1 data_type1[,...]       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p>
<p><code dir="ltr" translate="no">          PARTITION BY                column_name       </code></p>
<p><code dir="ltr" translate="no">          CLUSTER BY                column_name [, ...]       </code></p>
<br />
Note: BigQuery does not use <code dir="ltr" translate="no">       UNIQUE      </code> , <code dir="ltr" translate="no">       PRIMARY KEY      </code> , or <code dir="ltr" translate="no">       FOREIGN      </code> <code dir="ltr" translate="no">       KEY      </code> table constraints. To achieve similar optimization that these constraints provide during query execution, partition and cluster your BigQuery tables. <code dir="ltr" translate="no">       CLUSTER BY      </code> supports up to four columns.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        CREATE TABLE table_name       </code></p>
<p><code dir="ltr" translate="no">        LIKE original_table_name       </code></p></td>
<td>See <a href="/bigquery/docs/information-schema-tables#example_3">this example</a> to learn how to use the <code dir="ltr" translate="no">       INFORMATION_SCHEMA      </code> tables to copy column names, data types, and NOT NULL constraints to a new table.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        CREATE TABLE table_name       </code></p>
<p><code dir="ltr" translate="no">        (       </code></p>
<p><code dir="ltr" translate="no">        col1 data_type1       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p>
<p><code dir="ltr" translate="no">        BACKUP NO       </code></p>
<br />
Note:In Snowflake, the <code dir="ltr" translate="no">       BACKUP NO      </code> setting is specified to "save processing time when creating snapshots and restoring from snapshots and to reduce storage space."</td>
<td>The <code dir="ltr" translate="no">       BACKUP NO      </code> table option is not used nor needed because BigQuery automatically keeps up to 7 days of historical versions of all your tables, without any effect on processing time nor billed storage.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        CREATE TABLE table_name       </code></p>
<p><code dir="ltr" translate="no">        (       </code></p>
<p><code dir="ltr" translate="no">        col1 data_type1       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p>
<p><code dir="ltr" translate="no">        table_attributes       </code></p>
<br />
where <code dir="ltr" translate="no">       table_attributes      </code> are:<br />

<p><code dir="ltr" translate="no">        [DISTSTYLE {AUTO|EVEN|KEY|ALL}]       </code></p>
<p><code dir="ltr" translate="no">        [DISTKEY (column_name)]       </code></p>
<p><code dir="ltr" translate="no">        [[COMPOUND|INTERLEAVED] SORTKEY       </code></p>
<p><code dir="ltr" translate="no">        (column_name [, ...])]       </code></p>
<p><code dir="ltr" translate="no"></code></p></td>
<td>BigQuery supports clustering which allows storing keys in sorted order.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        CREATE TABLE table_name       </code></p>
<p><code dir="ltr" translate="no">        AS SELECT ...       </code></p></td>
<td><p><code dir="ltr" translate="no">        CREATE TABLE table_name       </code></p>
<p><code dir="ltr" translate="no">        AS SELECT ...       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        CREATE TABLE IF NOT EXISTS table_name       </code></p>
<p><code dir="ltr" translate="no">        ...       </code></p></td>
<td><p><code dir="ltr" translate="no">        CREATE TABLE IF NOT EXISTS table_name       </code></p>
<p><code dir="ltr" translate="no">        ...       </code></p></td>
</tr>
</tbody>
</table>

BigQuery also supports the DDL statement `  CREATE OR REPLACE TABLE  ` statement which overwrites a table if it already exists.

BigQuery's `  CREATE TABLE  ` statement also supports the following clauses, which do not have a Snowflake equivalent:

  - [`  PARTITION BY  ` partition\_statement](/bigquery/docs/reference/standard-sql/data-definition-language#partition_expression)
  - [`  CLUSTER BY  ` clustering\_column\_list](/bigquery/docs/reference/standard-sql/data-definition-language#clustering_column_list)
  - [`  OPTIONS  ` (table\_options\_list)](/bigquery/docs/reference/standard-sql/data-definition-language#table_option_list)

For more information about `  CREATE TABLE  ` in BigQuery, see [`  CREATE TABLE  ` statement examples](/bigquery/docs/reference/standard-sql/data-definition-language#create-table-examples) in the DDL documentation.

#### `     ALTER TABLE    ` statement

This section will use BigQuery CLI commands corresponding to the Snowflake commands to address the differences in ALTER statements for tables.

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
<td><p><code dir="ltr" translate="no">          ALTER TABLE                [ IF EXISTS ] &lt;name&gt; RENAME TO &lt;new_name&gt;       </code></p></td>
<td><p><code dir="ltr" translate="no">          ALTER TABLE                [IF EXISTS] &lt;name&gt;       </code></p>
<p><code dir="ltr" translate="no">        SET OPTIONS (friendly_name="&lt;new_name&gt;")       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          ALTER TABLE                &lt;name&gt;       </code></p>
<p><code dir="ltr" translate="no">        SWAP WITH &lt;target_db_name&gt;       </code></p></td>
<td>Swapping tables is not supported in BigQuery.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          ALTER TABLE                &lt;name&gt;       </code></p>
<p><code dir="ltr" translate="no">        SET       </code></p>
<p><code dir="ltr" translate="no">        [DEFAULT_DDL_COLLATION = '&lt;value&gt;']       </code></p></td>
<td>Managing data collation for tables is not supported in BigQuery.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          ALTER TABLE                &lt;name&gt;       </code></p>
<p><code dir="ltr" translate="no">        SET       </code></p>
<p><code dir="ltr" translate="no">        [DATA_RETENTION_TIME_IN_DAYS = &lt;num&gt;]       </code></p></td>
<td><p><code dir="ltr" translate="no">          ALTER TABLE                [IF EXISTS] &lt;name&gt;       </code></p>
<p><code dir="ltr" translate="no">        SET OPTIONS (expiration_timestamp=&lt;timestamp&gt;)       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          ALTER TABLE                &lt;name&gt;       </code></p>
<p><code dir="ltr" translate="no">        SET       </code></p>
<p><code dir="ltr" translate="no">        COMMENT = '&lt;string_literal&gt;'       </code></p></td>
<td><p><code dir="ltr" translate="no">          ALTER TABLE                [IF EXISTS] &lt;name&gt;       </code></p>
<p><code dir="ltr" translate="no">        SET OPTIONS (description='&lt;string_literal&gt;')       </code></p></td>
</tr>
</tbody>
</table>

Additionally, Snowflake provides [clustering, column, and constraint options](https://docs.snowflake.net/manuals/sql-reference/sql/alter-table.html#syntax) for altering tables that are not supported by BigQuery.

#### `     DROP TABLE    ` and `     UNDROP TABLE    ` statements

This section will use BigQuery CLI command corresponding to the Snowflake command to address the difference in DROP and UNDROP statements.

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
<td><p><code dir="ltr" translate="no">          DROP TABLE                [IF EXISTS] &lt;table_name&gt;       </code></p>
<p><code dir="ltr" translate="no">        [CASCADE | RESTRICT]       </code></p>
<br />
Note: In Snowflake, dropping a table does not permanently remove it from the system. A version of the dropped table is retained for the number of days specified by the <code dir="ltr" translate="no">       DATA_RETENTION_TIME_IN_DAYS      </code> parameter for the database.</td>
<td><p><code dir="ltr" translate="no">          bq rm                -r -f -d &lt;dataset_name&gt;.&lt;table_name&gt;       </code></p>
<br />

<p><code dir="ltr" translate="no">        Where       </code></p>
-r is to remove all objects in the dataset<br />
-f is to skip confirmation for execution<br />
-d indicates dataset<br />
<br />
Note: In BigQuery, deleting a table is also not permanent but a snapshot is maintained only for 7 days.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          UNDROP TABLE                &lt;table_name&gt;       </code></p></td>
<td><p><code dir="ltr" translate="no">          bq cp                \ &lt;dataset_name&gt;.&lt;table_name&gt;@&lt;unix_timestamp&gt; &lt;dataset_name&gt;.&lt;new_table_name&gt;       </code></p>
<br />
<strong>Note</strong> : In BigQuery, you need to first, determine a UNIX timestamp of when the table existed (in milliseconds). Then, copy the table at that timestamp to a new table. The new table must have a different name than the deleted table.</td>
</tr>
</tbody>
</table>

#### `     CREATE EXTERNAL TABLE    ` statement

BigQuery allows creating both [permanent and temporary external tables](/bigquery/external-data-sources) and querying data directly from:

  - [Bigtable](/bigquery/external-data-bigtable)
  - [Cloud Storage](/bigquery/external-data-cloud-storage)
  - [Google Drive](/bigquery/external-data-drive)
  - [Cloud SQL (beta)](/bigquery/docs/cloud-sql-federated-queries)

Snowflake allows creating a [permanent external table](https://docs.snowflake.com/en/sql-reference/sql/create-external-table.html#create-external-table) which when queried, reads data from a set of one or more files in a specified external stage.

This section will use BigQuery CLI command corresponding to the Snowflake command to address the differences in CREATE EXTERNAL TABLE statement.

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
<td><code dir="ltr" translate="no">         CREATE [OR REPLACE] EXTERNAL TABLE       </code><br />

<p><code dir="ltr" translate="no">        table       </code></p>
<p><code dir="ltr" translate="no">        ((&lt;col_name&gt; &lt;col_type&gt; AS &lt;expr&gt; )       </code></p>
<p><code dir="ltr" translate="no">        | (&lt;part_col_name&gt; &lt;col_type&gt; AS &lt;part_expr&gt;)[ inlineConstraint ]       </code></p>
<p><code dir="ltr" translate="no">        [ , ... ] )       </code></p>
<p><code dir="ltr" translate="no">        LOCATION = externalStage       </code></p>
<p><code dir="ltr" translate="no">        FILE_FORMAT =       </code></p>
<p><code dir="ltr" translate="no">        ({FORMAT_NAME='&lt;file_format_name&gt;'       </code></p>
<p><code dir="ltr" translate="no">        |TYPE=source_format [formatTypeOptions]})       </code></p>
<br />

<p><code dir="ltr" translate="no">        Where:       </code></p>
<p><code dir="ltr" translate="no">        externalStage = @[namespace.]ext_stage_name[/path]       </code></p>
<br />
<strong>Note</strong> : Snowflake allows staging the files containing data to be read and specifying format type options for external tables. Snowflake format types - CSV, JSON, AVRO, PARQUET, ORC are all supported by BigQuery except the XML type.</td>
<td><p><code dir="ltr" translate="no">        [1]                 bq mk                \       </code></p>
<p><code dir="ltr" translate="no">        --external_table_definition=definition_file \       </code></p>
<p><code dir="ltr" translate="no">        dataset.table       </code></p>
<br />

<p><code dir="ltr" translate="no">        OR       </code></p>
<br />

<p><code dir="ltr" translate="no">        [2]                 bq mk                \       </code></p>
<p><code dir="ltr" translate="no">        --external_table_definition=schema_file@source_format={Cloud Storage URI | drive_URI} \       </code></p>
<p><code dir="ltr" translate="no">        dataset.table       </code></p>
<br />

<p><code dir="ltr" translate="no">        OR       </code></p>
<br />

<p><code dir="ltr" translate="no">        [3]                 bq mk                \       </code></p>
<p><code dir="ltr" translate="no">        --external_table_definition=schema@source_format = {Cloud Storage URI | drive_URI} \       </code></p>
<p><code dir="ltr" translate="no">        dataset.table       </code></p>
<br />
<strong>Note</strong> : BigQuery allows creating a permanent table linked to your data source using a table definition file [1], a JSON schema file [2] or an inline schema definition [3]. Staging files to be read and specifying format type options is not supported in BigQuery.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">          CREATE [OR REPLACE] EXTERNAL TABLE                [IF EXISTS]       </code></p>
<p><code dir="ltr" translate="no">        &lt;table_name&gt;       </code></p>
<p><code dir="ltr" translate="no">        ((&lt;col_name&gt; &lt;col_type&gt; AS &lt;expr&gt; )       </code></p>
<p><code dir="ltr" translate="no">        [ , ... ] )       </code></p>
<p><code dir="ltr" translate="no">        [PARTITION BY (&lt;identifier&gt;, ...)]       </code></p>
<p><code dir="ltr" translate="no">        LOCATION = externalStage       </code></p>
<p><code dir="ltr" translate="no">        [REFRESH_ON_CREATE = {TRUE|FALSE}]       </code></p>
<p><code dir="ltr" translate="no">        [AUTO_REFRESH = {TRUE|FALSE}]       </code></p>
<p><code dir="ltr" translate="no">        [PATTERN = '&lt;regex_pattern&gt;']       </code></p>
<p><code dir="ltr" translate="no">        FILE_FORMAT = ({FORMAT_NAME = '&lt;file_format_name&gt;' | TYPE = { CSV | JSON | AVRO | ORC | PARQUET} [ formatTypeOptions]})       </code></p>
<p><code dir="ltr" translate="no">        [COPY GRANTS]       </code></p>
<p><code dir="ltr" translate="no">        [COMMENT = '&lt;string_literal&gt;']       </code></p></td>
<td><p><code dir="ltr" translate="no">          bq mk                \       </code></p>
<p><code dir="ltr" translate="no">        --external_table_definition=definition_file \       </code></p>
<p><code dir="ltr" translate="no">        dataset.table       </code></p>
<br />
Note: BigQuery does not support any of the optional parameter options provided by Snowflake for creating external tables. For partitioning, BigQuery supports using the <code dir="ltr" translate="no">       _FILE_NAME      </code> pseudocolumn to create partitioned tables/views on top of the external tables. For more information, see <a href="/bigquery/docs/query-cloud-storage-data#query_the_file_name_pseudo-column">Query the <code dir="ltr" translate="no">        _FILE_NAME       </code> pseudocolumn</a> .</td>
</tr>
</tbody>
</table>

Additionally, BigQuery also supports [querying externally partitioned data](/bigquery/docs/hive-partitioned-queries-gcs) in AVRO, PARQUET, ORC, JSON and CSV formats that is stored on Google Cloud Storage using a [default hive partitioning layout](/bigquery/docs/hive-partitioned-queries-gcs#supported_data_layouts) .

#### `     CREATE VIEW    ` statement

The following table shows equivalents between Snowflake and BigQuery for the `  CREATE VIEW  ` statement.

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
<td><p><code dir="ltr" translate="no">          CREATE VIEW                view_name AS SELECT ...       </code></p></td>
<td><p><code dir="ltr" translate="no">          CREATE VIEW                view_name AS SELECT ...       </code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        CREATE OR REPLACE VIEW view_name AS SELECT ...       </code></p></td>
<td><code dir="ltr" translate="no">         CREATE OR REPLACE VIEW       </code><br />

<p><code dir="ltr" translate="no">        view_name AS SELECT ...       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        CREATE VIEW view_name       </code></p>
<p><code dir="ltr" translate="no">        (column_name, ...)       </code></p>
<p><code dir="ltr" translate="no">        AS SELECT ...       </code></p></td>
<td><p><code dir="ltr" translate="no">        CREATE VIEW view_name       </code></p>
<p><code dir="ltr" translate="no">        AS SELECT ...       </code></p></td>
</tr>
<tr class="even">
<td>Not supported</td>
<td><code dir="ltr" translate="no">         CREATE VIEW IF NOT EXISTS       </code><br />

<p><code dir="ltr" translate="no">        view_name       </code></p>
<p><code dir="ltr" translate="no">        OPTIONS(                 view_option_list                )       </code></p>
<p><code dir="ltr" translate="no">        AS SELECT ...       </code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        CREATE VIEW view_name       </code></p>
<p><code dir="ltr" translate="no">        AS SELECT ...       </code></p>
<p><code dir="ltr" translate="no">        WITH NO SCHEMA BINDING       </code></p></td>
<td>In BigQuery, to create a view all referenced objects must already exist.<br />
<br />
BigQuery allows to query <a href="/bigquery/docs/external-data-sources">external data sources</a> .</td>
</tr>
</tbody>
</table>

#### `     CREATE SEQUENCE    ` statement

Sequences are not used in BigQuery, this can be achieved with the following batch way. For more information on surrogate keys and slowly changing dimensions (SCD), see the following guides:

  - [BigQuery Surrogate Keys](https://medium.com/google-cloud/bigquery-surrogate-keys-672b2e110f80)
  - [BigQuery and surrogate keys: A practical approach](https://cloud.google.com/blog/products/data-analytics/bigquery-and-surrogate-keys-practical-approach)

<table>
<thead>
<tr class="header">
<th><p><code dir="ltr" translate="no">        INSERT INTO dataset.table SELECT   *,   ROW_NUMBER() OVER () AS id FROM dataset.table       </code></p></th>
</tr>
</thead>
<tbody>
</tbody>
</table>

### Data loading and unloading DDL

Snowflake supports data loading and unloading via stage, file format and pipe management commands. BigQuery also provides multiple options for such as bq load, BigQuery Data Transfer Service, bq extract, etc. This section highlights the differences in the usage of these methodologies for data loading and unloading.

### Account and Session DDL

Snowflake's Account and Session concepts are not supported in BigQuery. BigQuery allows management of accounts via [Cloud IAM](/bigquery/docs/access-control) at all levels. Also, multi statement transactions are not supported in BigQuery.

## User-defined functions (UDF)

A UDF enables you to create functions for custom operations. These functions accept columns of input, perform actions, and return the result of those actions as a value

Both [Snowflake](https://docs.snowflake.net/manuals/sql-reference/ddl-udf.html#udf-management) and [BigQuery](/bigquery/docs/user-defined-functions) support UDF using SQL expressions and Javascript Code.

See the [GoogleCloudPlatform/bigquery-utils/](https://github.com/GoogleCloudPlatform/bigquery-utils/tree/master/udfs/community) GitHub repository for a library of common BigQuery UDFs.

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
Note: In BigQuery <a href="/bigquery/docs/user-defined-functions#sql-udf-structure">SQL UDF</a> , return data type is optional. BigQuery infers the result type of the function from the SQL function body when a query calls the function.</td>
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
Note:In BigQuery <a href="/bigquery/docs/user-defined-functions#sql-udf-structure">SQL UDF</a> , returning table type is not supported but is on the product roadmap and will be available soon. However, BigQuery supports returning ARRAY of type STRUCT.</td>
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
Note: BigQuery supports using ANY TYPE as argument type. The function will accept an input of any type for this argument. For more information, see <a href="/bigquery/docs/user-defined-functions#templated-sql-udf-parameters">templated parameter</a> in BigQuery.</td>
</tr>
</tbody>
</table>

BigQuery also supports the `  CREATE FUNCTION IF NOT EXISTS  ` statement which treats the query as successful and takes no action if a function with the same name already exists.

BigQuery's `  CREATE FUNCTION  ` statement also supports creating [`  TEMPORARY or TEMP functions  `](/bigquery/docs/user-defined-functions) , which do not have a Snowflake equivalent. See [calling UDFs](/bigquery/docs/reference/standard-sql/syntax#calling_persistent_user-defined_functions_udfs) for details on executing a BigQuery persistent UDF.

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

As configuring function security and adding function comments is not available in BigQuery, `  ALTER FUNCTION  ` syntax is not supported. However, the [CREATE FUNCTION](/bigquery/docs/user-defined-functions#sql-udf-structure) statement can be used to create a UDF with the same function definition but a different name.

### `     DESCRIBE FUNCTION    ` syntax

Snowflake supports describing a UDF using [DESC\[RIBE\] FUNCTION](https://docs.snowflake.net/manuals/sql-reference/sql/desc-function.html) syntax. This is not supported in BigQuery. However, querying UDF metadata via INFORMATION SCHEMA will be available soon as part of the product roadmap.

### `     SHOW USER FUNCTIONS    ` syntax

In Snowflake, [SHOW USER FUNCTIONS](https://docs.snowflake.net/manuals/sql-reference/sql/show-user-functions.html) syntax can be used to list all UDFs for which users have access privileges. This is not supported in BigQuery. However, querying UDF metadata via INFORMATION SCHEMA will be available soon as part of the product roadmap.

## Stored procedures

Snowflake [stored procedures](https://docs.snowflake.net/manuals/sql-reference/stored-procedures-usage.html) are written in JavaScript, which can execute SQL statements by calling a JavaScript API. In BigQuery, stored procedures are defined using a [block](/bigquery/docs/reference/standard-sql/scripting#begin) of SQL statements.

### `     CREATE PROCEDURE    ` syntax

In Snowflake, a stored procedure is executed with a [CALL](https://docs.snowflake.net/manuals/sql-reference/sql/call.html) command while in BigQuery, stored procedures are [executed](/bigquery/docs/reference/standard-sql/data-definition-language#create_procedure) like any other BigQuery function.

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

<table>
<thead>
<tr class="header">
<th><strong>Snowflake</strong></th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">          BEGIN                [ { WORK | TRANSACTION } ] [ NAME &lt;name&gt; ];  START_TRANSACTION [ name &lt;name&gt; ];       </code></p></td>
<td>BigQuery always uses Snapshot Isolation. For details, see <a href="#consistency-guarantees-and-transaction-isolation">Consistency guarantees</a> elsewhere in this document.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        COMMIT;       </code></p></td>
<td>Not used in BigQuery.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        ROLLBACK;       </code></p></td>
<td>Not used in BigQuery</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        SHOW LOCKS [ IN ACCOUNT ]; SHOW TRANSACTIONS [ IN ACCOUNT ];  Note: If the user has the ACCOUNTADMIN role, the user can see locks/transactions for all users in the account.       </code></p></td>
<td>Not used in BigQuery.</td>
</tr>
</tbody>
</table>

## Multi-statement and multi-line SQL statements

Both Snowflake and BigQuery support transactions (sessions) and therefore support statements separated by semicolons that are consistently executed together. For more information, see [Multi-statement transactions](/bigquery/docs/transactions) .

## Metadata columns for staged files

Snowflake automatically generates metadata for files in internal and external stages. This metadata can be [queried](https://docs.snowflake.net/manuals/user-guide/querying-stage.html) and [loaded](https://docs.snowflake.net/manuals/sql-reference/sql/copy-into-table.html) into a table alongside regular data columns. The following metadata columns can be utilized:

  - [METADATA$FILENAME](https://docs.snowflake.net/manuals/user-guide/querying-metadata.html#metadata-columns)
  - [METADATA$FILE\_ROW\_NUMBER](https://docs.snowflake.net/manuals/user-guide/querying-metadata.html#metadata-columns)

## Consistency guarantees and transaction isolation

Both Snowflake and BigQuery are atomic—that is, ACID-compliant on a per-mutation level across many rows.

### Transactions

Each Snowflake transaction is assigned a unique start time (includes milliseconds) that is set as the transaction ID. Snowflake only supports the [`  READ COMMITTED  `](https://docs.snowflake.net/manuals/sql-reference/transactions.html#read-committed-isolation) isolation level. However, a statement can see changes made by another statement if they are both in the same transaction - even though those changes are not committed yet. Snowflake transactions acquire locks on resources (tables) when that resource is being modified. Users can adjust the maximum time a blocked statement will wait until the statement times out. DML statements are autocommitted if the [`  AUTOCOMMIT  `](https://docs.snowflake.net/manuals/sql-reference/parameters.html#autocommit) parameter is turned on.

BigQuery also [supports transactions](/bigquery/docs/transactions) . BigQuery helps ensure [optimistic concurrency control](https://en.wikipedia.org/wiki/Optimistic_concurrency_control) (first to commit wins) with [snapshot isolation](https://en.wikipedia.org/wiki/Snapshot_isolation) , in which a query reads the last committed data before the query starts. This approach guarantees the same level of consistency on a per-row, per-mutation basis and across rows within the same DML statement, yet avoids deadlocks. In the case of multiple DML updates against the same table, BigQuery switches to [pessimistic concurrency control](/bigquery/docs/data-manipulation-language#dml-limitations) . Load jobs can run completely independently and append to tables. However, BigQuery does not provide an explicit transaction boundary or session.

## Rollback

If a Snowflake transaction's session is unexpectedly terminated before the transaction is committed or rolled back, the transaction is left in a detached state. The user should run SYSTEM$ABORT\_TRANSACTION to abort the detached transaction or Snowflake will roll back the detached transaction after four idle hours. If a deadlock occurs, Snowflake detects the deadlock and selects the more recent statement to roll back. If the DML statement in an explicitly opened transaction fails, the changes are rolled back, but the transaction is kept open until it is committed or rolled back. DDL statements in Snowflake cannot be rolled back as they are autocommitted.

BigQuery supports the [`  ROLLBACK TRANSACTION  ` statement](/bigquery/docs/reference/standard-sql/procedural-language#rollback_transaction) . There is no [`  ABORT  ` statement](https://docs.teradata.com/reader/huc7AEHyHSROUkrYABqNIg/c6KYQ4ySu4QTCkKS4f5A2w) in BigQuery.

## Database limits

Always check [the BigQuery public documentation](/bigquery/quotas) for the latest quotas and limits. Many quotas for large-volume users can be raised by contacting the Cloud Support team.

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
