---
name: documents/docs.cloud.google.com/bigquery/docs/migration/hive-sql
uri: https://docs.cloud.google.com/bigquery/docs/migration/hive-sql
title: Apache Hive SQL translation guide
description: Provides a reference to compare statements, functions, data types, and other SQL objects between the Apache Hive and GoogleSQL dialects.
data_source: docs.cloud.google.com
---

# Apache Hive SQL translation guide

This document details the similarities and differences in SQL syntax between Apache Hive and BigQuery to help you plan your migration. To migrate your SQL scripts in bulk, use [batch SQL translation](https://docs.cloud.google.com/bigquery/docs/batch-sql-translator) . To translate ad hoc queries, use [interactive SQL translation](https://docs.cloud.google.com/bigquery/docs/interactive-sql-translator) .

In some cases, there's no direct mapping between a SQL element in Hive and BigQuery. However, in most cases, BigQuery offers an alternative element to Hive to help you achieve the same functionality, as shown in the examples in this document.

The intended audience for this document is enterprise architects, database administrators, application developers, and IT security specialists. It assumes that you're familiar with Hive.

## Data types

Hive and BigQuery have different data type systems. In most cases, you can map data types in Hive to [BigQuery data types](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-types) with a few exceptions, such as `MAP` and `UNION` . Hive supports more implicit type casting than BigQuery. As a result, the batch SQL translator inserts many explicit casts.

| **Hive**    | **BigQuery**                               |
|-------------|--------------------------------------------|
| `TINYINT`   | `INT64`                                    |
| `SMALLINT`  | `INT64`                                    |
| `INT`       | `INT64`                                    |
| `BIGINT`    | `INT64`                                    |
| `DECIMAL`   | `NUMERIC`                                  |
| `FLOAT`     | `FLOAT64`                                  |
| `DOUBLE`    | `FLOAT64`                                  |
| `BOOLEAN`   | `BOOL`                                     |
| `STRING`    | `STRING`                                   |
| `VARCHAR`   | `STRING`                                   |
| `CHAR`      | `STRING`                                   |
| `BINARY`    | `BYTES`                                    |
| `DATE`      | `DATE`                                     |
| \-          | `DATETIME`                                 |
| \-          | `TIME`                                     |
| `TIMESTAMP` | `DATETIME/TIMESTAMP`                       |
| `INTERVAL`  | \-                                         |
| `ARRAY`     | `ARRAY`                                    |
| `STRUCT`    | `STRUCT`                                   |
| `MAPS`      | `STRUCT` with key values ( `REPEAT` field) |
| `UNION`     | `STRUCT` with different types              |
| \-          | `GEOGRAPHY`                                |
| \-          | `JSON`                                     |

## Query syntax

This section addresses differences in query syntax between Hive and BigQuery.

### `SELECT` statement

Most Hive [`SELECT`](https://cwiki.apache.org/confluence/display/hive/languagemanual+select#LanguageManualSelect-SelectSyntax) statements are compatible with BigQuery. The following table contains a list of minor differences:

| **Case**           | **Hive**                                                                                                                                                | **BigQuery**                                                                                                                 |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| Subquery           | `SELECT * FROM ( SELECT 10 as col1, "test" as col2, "test" as col3 ) tmp_table;`                                                                        | `SELECT * FROM ( SELECT 10 as col1, "test" as col2, "test" as col3 );`                                                       |
| Column filtering   | `` SET hive.support.quoted.identifiers=none; SELECT `(col2|col3)?+.+` FROM ( SELECT 10 as col1, "test" as col2, "test" as col3 ) tmp_table; ``          | `SELECT * EXCEPT(col2,col3) FROM ( SELECT 10 as col1, "test" as col2, "test" as col3 );`                                     |
| Exploding an array | `SELECT tmp_table.pageid, adid FROM ( SELECT 'test_value' pageid, Array(1,2,3) ad_id) tmp_table LATERAL VIEW explode(tmp_table.ad_id) adTable AS adid;` | `SELECT tmp_table.pageid, ad_id FROM ( SELECT 'test_value' pageid, [1,2,3] ad_id) tmp_table, UNNEST(tmp_table.ad_id) ad_id;` |

### `FROM` clause

The `FROM` clause in a query lists the table references from which data is selected. In Hive, possible table references include tables, views, and subqueries. BigQuery also supports all these table references.

You can reference BigQuery tables in the `FROM` clause by using the following:

- `[project_id].[dataset_id].[table_name]`
- `[dataset_id].[table_name]`
- `[table_name]`

BigQuery also supports [additional table references](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/query-syntax#from_clause) :

- Historical versions of the table definition and rows using [`FOR SYSTEM_TIME AS OF`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/query-syntax#for_system_time_as_of)
- [Field paths](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/query-syntax#field_path) , or any path that resolves to a field within a data type (such as a `STRUCT` )
- [Flattened arrays](https://docs.cloud.google.com/bigquery/docs/arrays#querying_nested_arrays)

### Comparison operators

The following table provides details about converting operators from Hive to BigQuery:

| **Function or operator**                                                     | **Hive**                                                                                                                           | **BigQuery**                                                                                                                                                                                                                                                                                                                                                                                                                             |
|------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `-` Unary minus `*` Multiplication `/` Division `+` Addition `-` Subtraction | All [number types](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Types#LanguageManualTypes-NumericTypes)         | All [number types](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-types#numeric_types) . To prevent errors during the divide operation, consider using [`SAFE_DIVIDE`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#safe_divide) or [`IEEE_DIVIDE`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#ieee_divide) .       |
| `~` Bitwise not `|` Bitwise OR `&` Bitwise AND `^` Bitwise XOR               | Boolean data type                                                                                                                  | Boolean data type.                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Left shift                                                                   | `shiftleft(TINYINT|SMALLINT|INT a, INT b) shiftleft(BIGINT a, INT b)`                                                              | `<<` Integer or bytes `A << B` , where `B` must be same type as `A`                                                                                                                                                                                                                                                                                                                                                                      |
| Right shift                                                                  | `shiftright(TINYINT|SMALLINT|INT a, INT b) shiftright(BIGINT a, INT b)`                                                            | `>>` Integer or bytes `A >> B` , where `B` must be same type as `A`                                                                                                                                                                                                                                                                                                                                                                      |
| Modulus (remainder)                                                          | `X % Y` All [number types](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Types#LanguageManualTypes-NumericTypes) | `MOD(X, Y)`                                                                                                                                                                                                                                                                                                                                                                                                                              |
| Integer division                                                             | `A DIV B` and `A/B` for detailed precision                                                                                         | All [number types](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-types#numeric_types) . Note: To prevent errors during the divide operation, consider using [`SAFE_DIVIDE`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#safe_divide) or [`IEEE_DIVIDE`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#ieee_divide) . |
| Unary negation                                                               | `!` , `NOT`                                                                                                                        | `NOT`                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| Types supporting equality comparisons                                        | All [primitive types](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Types#LanguageManualTypes-Overview)          | All [comparable types and `STRUCT`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-types) .                                                                                                                                                                                                                                                                                                                     |
|                                                                              | `a <=> b`                                                                                                                          | Not supported. Translate to the following: `(a = b AND b IS NOT NULL OR a IS NULL)`                                                                                                                                                                                                                                                                                                                                                      |
|                                                                              | `a <> b`                                                                                                                           | Not supported. Translate to the following: `NOT (a = b AND b IS NOT NULL OR a IS NULL)`                                                                                                                                                                                                                                                                                                                                                  |
| Relational operators ( `=, ==, !=, <, >, >=` )                               | All [primitive types](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-RelationalOperators)   | All [comparable types](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/operators#comparison_operators) .                                                                                                                                                                                                                                                                                                              |
| String comparison                                                            | `RLIKE` , `REGEXP`                                                                                                                 | `REGEXP_CONTAINS` built-in function. Uses BigQuery [regex syntax for string functions](https://github.com/google/re2/wiki/Syntax) for the regular expression patterns.                                                                                                                                                                                                                                                                   |
| `[NOT] LIKE, [NOT] BETWEEN, IS [NOT] NULL`                                   | `A [NOT] BETWEEN B AND C, A IS [NOT] (TRUE|FALSE), A [NOT] LIKE B`                                                                 | Same as Hive. In addition, BigQuery also supports the [`IN` operator](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/operators#in_operators) .                                                                                                                                                                                                                                                                       |

### JOIN conditions

Both Hive and BigQuery support the following types of joins:

- `[INNER] JOIN`

- `LEFT [OUTER] JOIN`

- `RIGHT [OUTER] JOIN`

- `FULL [OUTER] JOIN`

- `CROSS JOIN` and the equivalent implicit [comma cross join](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/query-syntax#cross_join)

For more information, see [Join operation](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/query-syntax#join_types) and [Hive joins](https://cwiki.apache.org/confluence/display/hive/languagemanual+joins) .

### Type conversion and casting

The following table provides details about converting functions from Hive to BigQuery:

| **Function or operator** | **Hive**                                 | **BigQuery**                                                                                                                                                                                                                                                                                                                                     |
|--------------------------|------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Type casting             | When a cast fails, \`NULL\` is returned. | Same syntax as Hive. For more information about BigQuery type conversion rules, see [Conversion rules](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/conversion_rules) . If cast fails, you see an error. To have the same behavior as Hive, use `SAFE_CAST` instead.                                                       |
| `SAFE` function calls    |                                          | If you prefix function calls with [`SAFE`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/functions-reference#safe_prefix) , the function returns `NULL` instead of reporting failure. For example, `SAFE.SUBSTR('foo', 0, -2) AS safe_output;` returns `NULL` . Note: When casting safely without errors, use `SAFE_CAST` . |

#### Implicit conversion types

When migrating to BigQuery, you need to convert most of your [Hive implicit conversions](https://cwiki.apache.org/confluence/display/hive/languagemanual+types#LanguageManualTypes-AllowedImplicitConversions) to BigQuery explicit conversions except for the following data types, which BigQuery implicitly converts.

| **From BigQuery type** | **To BigQuery type**                 |
|------------------------|--------------------------------------|
| `INT64`                | `FLOAT64` , `NUMERIC` , `BIGNUMERIC` |
| `BIGNUMERIC`           | `FLOAT64`                            |
| `NUMERIC`              | `BIGNUMERIC` , `FLOAT64`             |

BigQuery also performs implicit conversions for the following literals:

| **From BigQuery type**                                   | **To BigQuery type** |
|----------------------------------------------------------|----------------------|
| `STRING` literal (for example, `"2008-12-25"` )          | `DATE`               |
| `STRING` literal (for example, `"2008-12-25 15:30:00"` ) | `TIMESTAMP`          |
| `STRING` literal (for example, `"2008-12-25T07:30:00"` ) | `DATETIME`           |
| `STRING` literal (for example, `"15:30:00"` )            | `TIME`               |

#### Explicit conversion types

If you want to convert Hive data types that BigQuery doesn't implicitly convert, use the BigQuery [`CAST(expression AS type)` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/conversion_functions#cast) .

## Functions

This section covers common functions used in Hive and BigQuery.

### Aggregate functions

The following table shows mappings between common Hive aggregate, statistical aggregate, and approximate aggregate functions with their BigQuery equivalents:

| **Hive**                                                                                                                                                                    | **BigQuery**                                                                                                                                                                                                                                                                                       |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `count(DISTINCT expr[, expr...])`                                                                                                                                           | `count(DISTINCT expr[, expr...])`                                                                                                                                                                                                                                                                  |
| `percentile_approx(DOUBLE col, array(p1 [, p2]...) [, B]) WITHIN GROUP (ORDER BY expression)`                                                                               | [`APPROX_QUANTILES`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/approximate_aggregate_functions#approx_quantiles)` (expression, 100)[OFFSET(CAST(TRUNC(percentile * 100) as INT64))]` BigQuery doesn't support the rest of the arguments that Hive defines.                |
| [`AVG`](https://cwiki.apache.org/confluence/display/hive/languagemanual+udf#LanguageManualUDF-Built-inAggregateFunctions(UDAF))                                             | `AVG`                                                                                                                                                                                                                                                                                              |
| [`X | Y`](https://cwiki.apache.org/confluence/display/hive/languagemanual+udf#LanguageManualUDF-OperatorsprecedencesOperatorsPrecedencesOperatorsPrecedences)               | [`BIT_OR`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/aggregate_functions#bit_or)` / X | Y`                                                                                                                                                                                |
| [`X ^ Y`](https://cwiki.apache.org/confluence/display/hive/languagemanual+udf#LanguageManualUDF-OperatorsprecedencesOperatorsPrecedencesOperatorsPrecedences)               | [`BIT_XOR`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/aggregate_functions#bit_xor)` / X ^ Y`                                                                                                                                                                              |
| [`X & Y`](https://cwiki.apache.org/confluence/display/hive/languagemanual+udf#LanguageManualUDF-OperatorsprecedencesOperatorsPrecedencesOperatorsPrecedences)               | [`BIT_AND`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/aggregate_functions#bit_and)` / X & Y`                                                                                                                                                                              |
| [`COUNT`](https://cwiki.apache.org/confluence/display/hive/languagemanual+udf#LanguageManualUDF-Built-inAggregateFunctions(UDAF))                                           | `COUNT`                                                                                                                                                                                                                                                                                            |
| `COLLECT_SET(col), \ COLLECT_LIST(col` )                                                                                                                                    | [`ARRAY_AGG`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/aggregate_functions#array_agg)` (col)`                                                                                                                                                                            |
| [`COUNT`](https://cwiki.apache.org/confluence/display/hive/languagemanual+udf#LanguageManualUDF-Built-inAggregateFunctions(UDAF))                                           | [`COUNT`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/aggregate_functions#count)                                                                                                                                                                                            |
| `MAX`                                                                                                                                                                       | [`MAX`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/aggregate_functions#max)                                                                                                                                                                                                |
| `MIN`                                                                                                                                                                       | [`MIN`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/aggregate_functions#min)                                                                                                                                                                                                |
| `REGR_AVGX`                                                                                                                                                                 | `AVG(` `IF(dep_var_expr is NULL` `OR ind_var_expr is NULL,` `NULL, ind_var_expr)` `)`                                                                                                                                                                                                              |
| `REGR_AVGY`                                                                                                                                                                 | `AVG(` `IF(dep_var_expr is NULL` `OR ind_var_expr is NULL,` `NULL, dep_var_expr)` `)`                                                                                                                                                                                                              |
| `REGR_COUNT`                                                                                                                                                                | `SUM(` `IF(dep_var_expr is NULL` `OR ind_var_expr is NULL,` `NULL, 1)` `)`                                                                                                                                                                                                                         |
| `REGR_INTERCEPT`                                                                                                                                                            | `AVG(dep_var_expr)` `- AVG(ind_var_expr)` `* (COVAR_SAMP(ind_var_expr,dep_var_expr)` `/ VARIANCE(ind_var_expr)` `)`                                                                                                                                                                                |
| `REGR_R2`                                                                                                                                                                   | `(COUNT(dep_var_expr) *` `SUM(ind_var_expr * dep_var_expr) -` `SUM(dep_var_expr) * SUM(ind_var_expr))` `/ SQRT(` `(COUNT(ind_var_expr) *` `SUM(POWER(ind_var_expr, 2)) *` `POWER(SUM(ind_var_expr),2)) *` `(COUNT(dep_var_expr) *` `SUM(POWER(dep_var_expr, 2)) *` `POWER(SUM(dep_var_expr), 2)))` |
| `REGR_SLOPE`                                                                                                                                                                | `COVAR_SAMP(ind_var_expr,` `dep_var_expr)` `/ VARIANCE(ind_var_expr)`                                                                                                                                                                                                                              |
| `REGR_SXX`                                                                                                                                                                  | `SUM(POWER(ind_var_expr, 2)) - COUNT(ind_var_expr) * POWER(AVG(ind_var_expr),2)`                                                                                                                                                                                                                   |
| `REGR_SXY`                                                                                                                                                                  | `SUM(ind_var_expr*dep_var_expr) - COUNT(ind_var_expr) * AVG(ind) * AVG(dep_var_expr)`                                                                                                                                                                                                              |
| `REGR_SYY`                                                                                                                                                                  | `SUM(POWER(dep_var_expr, 2)) - COUNT(dep_var_expr) * POWER(AVG(dep_var_expr),2)`                                                                                                                                                                                                                   |
| [`ROLLUP`](https://cwiki.apache.org/confluence/display/Hive/Enhanced+Aggregation%2C+Cube%2C+Grouping+and+Rollup#EnhancedAggregation,Cube,GroupingandRollup-CubesandRollups) | [`ROLLUP`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/query-syntax#group_by_clause)                                                                                                                                                                                        |
| `STDDEV_POP`                                                                                                                                                                | `STDDEV_POP`                                                                                                                                                                                                                                                                                       |
| `STDDEV_SAMP`                                                                                                                                                               | `STDDEV_SAMP, STDDEV`                                                                                                                                                                                                                                                                              |
| `SUM`                                                                                                                                                                       | `SUM`                                                                                                                                                                                                                                                                                              |
| `VAR_POP`                                                                                                                                                                   | `VAR_POP`                                                                                                                                                                                                                                                                                          |
| `VAR_SAMP`                                                                                                                                                                  | `VAR_SAMP, VARIANCE`                                                                                                                                                                                                                                                                               |
| `CONCAT_WS`                                                                                                                                                                 | [`STRING_AGG`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/aggregate_functions#string_agg)                                                                                                                                                                                  |

### Analytical functions

The following table shows mappings between common Hive analytical functions with their BigQuery equivalents:

| **Hive**                                                                                                                                                         | **BigQuery**                                                                                                                                                                                                                                              |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `AVG`                                                                                                                                                            | [`AVG`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/aggregate_functions#avg)                                                                                                                                                       |
| `COUNT`                                                                                                                                                          | [`COUNT`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/aggregate_functions#count)                                                                                                                                                   |
| `COVAR_POP`                                                                                                                                                      | [`COVAR_POP`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/statistical_aggregate_functions#covar_pop)                                                                                                                               |
| `COVAR_SAMP`                                                                                                                                                     | [`COVAR_SAMP`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/statistical_aggregate_functions#covar_samp)                                                                                                                             |
| `CUME_DIST`                                                                                                                                                      | [`CUME_DIST`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/numbering_functions#cume_dist)                                                                                                                                           |
| `DENSE_RANK`                                                                                                                                                     | [`DENSE_RANK`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/numbering_functions#dense_rank)                                                                                                                                         |
| [`FIRST_VALUE`](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+WindowingAndAnalytics#LanguageManualWindowingAndAnalytics-EnhancementstoHiveQL)  | [`FIRST_VALUE`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/navigation_functions#first_value)                                                                                                                                      |
| `LAST_VALUE`                                                                                                                                                     | [`LAST_VALUE`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/navigation_functions#last_value)                                                                                                                                        |
| `LAG`                                                                                                                                                            | [`LAG`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/navigation_functions#lag)                                                                                                                                                      |
| `LEAD`                                                                                                                                                           | [`LEAD`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/navigation_functions#lead)                                                                                                                                                    |
| `COLLECT_LIST, \ COLLECT_SET`                                                                                                                                    | [`ARRAY_AGG`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/aggregate_functions#array_agg) [`ARRAY_CONCAT_AGG`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/aggregate_functions#array_concat_agg)             |
| `MAX`                                                                                                                                                            | [`MAX`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/aggregate_functions#max)                                                                                                                                                       |
| `MIN`                                                                                                                                                            | [`MIN`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/aggregate_functions#min)                                                                                                                                                       |
| `NTILE`                                                                                                                                                          | [`NTILE`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/numbering_functions#ntile)` (constant_integer_expression)`                                                                                                                   |
| [`PERCENT_RANK`](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+WindowingAndAnalytics#LanguageManualWindowingAndAnalytics-EnhancementstoHiveQL) | [`PERCENT_RANK`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/numbering_functions#percent_rank)                                                                                                                                     |
| `RANK ()`                                                                                                                                                        | [`RANK`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/numbering_functions#rank)                                                                                                                                                     |
| `ROW_NUMBER`                                                                                                                                                     | [`ROW_NUMBER`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/numbering_functions#row_number)                                                                                                                                         |
| `STDDEV_POP`                                                                                                                                                     | [`STDDEV_POP`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/statistical_aggregate_functions#stddev_pop)                                                                                                                             |
| `STDDEV_SAMP`                                                                                                                                                    | [`STDDEV_SAMP`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/statistical_aggregate_functions#stddev_samp)` , `[`STDDEV`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/statistical_aggregate_functions#stddev) |
| `SUM`                                                                                                                                                            | [`SUM`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/aggregate_functions#sum)                                                                                                                                                       |
| `VAR_POP`                                                                                                                                                        | [`VAR_POP`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/statistical_aggregate_functions#var_pop)                                                                                                                                   |
| `VAR_SAMP`                                                                                                                                                       | [`VAR_SAMP`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/statistical_aggregate_functions#var_samp)` , `[`VARIANCE`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/statistical_aggregate_functions#variance)   |
| `VARIANCE`                                                                                                                                                       | [`VARIANCE ()`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/statistical_aggregate_functions#variance)                                                                                                                              |
| [`WIDTH_BUCKET`](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-Built-inFunctions)                                        | A user-defined function (UDF) can be used.                                                                                                                                                                                                                |

### Date and time functions

The following table shows mappings between common Hive date and time functions and their BigQuery equivalents:

|                                                                |                                                                                                                                                                                                                                                                                                                                                                 |
|----------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `DATE_ADD`                                                     | [`DATE_ADD(date_expression, INTERVAL int64_expression date_part)`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/date_functions#date_add)                                                                                                                                                                                                  |
| `DATE_SUB`                                                     | [`DATE_SUB(date_expression, INTERVAL int64_expression date_part)`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/date_functions#date_sub)                                                                                                                                                                                                  |
| `CURRENT_DATE`                                                 | [`CURRENT_DATE`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/date_functions#current_date)                                                                                                                                                                                                                                                |
| `CURRENT_TIME`                                                 | [`CURRENT_TIME`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/time_functions#current_time)                                                                                                                                                                                                                                                |
| `CURRENT_TIMESTAMP`                                            | [`CURRENT_DATETIME`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/datetime_functions#current_datetime) is recommended, as this value is timezone-free and synonymous with `CURRENT_TIMESTAMP` \\ [`CURRENT_TIMESTAMP`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/timestamp_functions#current_timestamp) in Hive. |
| `EXTRACT(field FROM source)`                                   | [`EXTRACT(part FROM datetime_expression)`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/datetime_functions#extract)                                                                                                                                                                                                                       |
| `LAST_DAY`                                                     | `DATE_SUB( DATE_TRUNC( DATE_ADD( date_expression, INTERVAL 1 MONTH ` `), MONTH ), INTERVAL 1 DAY)`                                                                                                                                                                                                                                                              |
| `MONTHS_BETWEEN`                                               | [`DATE_DIFF`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/date_functions#date_diff)` (date_expression, date_expression, MONTH)`                                                                                                                                                                                                          |
| `NEXT_DAY`                                                     | `DATE_ADD( DATE_TRUNC( date_expression, WEEK(day_value) ), INTERVAL 1 WEEK ` `)`                                                                                                                                                                                                                                                                                |
| `TO_DATE`                                                      | [`PARSE_DATE`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/date_functions#parse_date)                                                                                                                                                                                                                                                    |
| `FROM_UNIXTIME`                                                | [`UNIX_SECONDS`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/timestamp_functions#unix_seconds)                                                                                                                                                                                                                                           |
| `FROM_UNIXTIMESTAMP`                                           | [`FORMAT_TIMESTAMP`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/timestamp_functions#format_timestamp)                                                                                                                                                                                                                                   |
| `YEAR \ QUARTER \ MONTH \ HOUR \ MINUTE \ SECOND \ WEEKOFYEAR` | [`EXTRACT`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/timestamp_functions#extract)                                                                                                                                                                                                                                                     |
| `DATEDIFF`                                                     | [`DATE_DIFF`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/date_functions#date_diff)                                                                                                                                                                                                                                                      |

BigQuery offers the following additional date and time functions:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><ul>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/datetime_functions#current_datetime"><code>CURRENT_DATETIME</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/date_functions#date_from_unix_date"><code>DATE_FROM_UNIX_DATE</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/date_functions#date_trunc"><code>DATE_TRUNC</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/datetime_functions#datetime"><code>DATETIME</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/datetime_functions#datetime_trunc"><code>DATETIME_TRUNC</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/date_functions#format_date"><code>FORMAT_DATE</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/datetime_functions#format_datetime"><code>FORMAT_DATETIME</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/time_functions#format_time"><code>FORMAT_TIME</code></a></li>
</ul></td>
<td><ul>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/timestamp_functions#format_timestamp"><code>FORMAT_TIMESTAMP</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/datetime_functions#parse_datetime"><code>PARSE_DATETIME</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/time_functions#parse_time"><code>PARSE_TIME</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/timestamp_functions#string"><code>STRING</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/time_functions#time"><code>TIME</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/time_functions#time_add"><code>TIME_ADD</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/time_functions#time_diff"><code>TIME_DIFF</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/time_functions#time_sub"><code>TIME_SUB</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/time_functions#time_trunc"><code>TIME_TRUNC</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/timestamp_functions#timestamp"><code>TIMESTAMP</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/timestamp_functions#timestamp_add"><code>TIMESTAMP_ADD</code></a></li>
</ul></td>
<td><ul>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/timestamp_functions#timestamp_diff"><code>TIMESTAMP_DIFF</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/timestamp_functions#timestamp_micros"><code>TIMESTAMP_MICROS</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/timestamp_functions#timestamp_millis"><code>TIMESTAMP_MILLIS</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/timestamp_functions#timestamp_seconds"><code>TIMESTAMP_SECONDS</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/timestamp_functions#timestamp_sub"><code>TIMESTAMP_SUB</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/timestamp_functions#timestamp_trunc"><code>TIMESTAMP_TRUNC</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/date_functions#unix_date"><code>UNIX_DATE</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/timestamp_functions#unix_micros"><code>UNIX_MICROS</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/timestamp_functions#unix_millis"><code>UNIX_MILLIS</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/timestamp_functions#unix_seconds"><code>UNIX_SECONDS</code></a></li>
</ul></td>
</tr>
</tbody>
</table>

### String functions

The following table shows mappings between Hive string functions and their BigQuery equivalents:

| **Hive**              | **BigQuery**                                                                                                                                    |
|-----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| `ASCII`               | [`TO_CODE_POINTS(string_expr)[OFFSET(0)]`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/string_functions#to_code_points)  |
| `HEX`                 | [`TO_HEX`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/string_functions#to_hex)                                          |
| `LENGTH`              | [`CHAR_LENGTH`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/string_functions#char_length)                                |
| `LENGTH`              | [`CHARACTER_LENGTH`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/string_functions#character_length)                      |
| `CHR`                 | [`CODE_POINTS_TO_STRING`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/string_functions#code_points_to_string)            |
| `CONCAT`              | [`CONCAT`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/string_functions#concat)                                          |
| `LOWER`               | [`LOWER`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/string_functions#lower)                                            |
| `LPAD`                | [`LPAD`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/string_functions#lpad)                                              |
| `LTRIM`               | [`LTRIM`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/string_functions#ltrim)                                            |
| `REGEXP_EXTRACT`      | [`REGEXP_EXTRACT`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/string_functions#regexp_extract)                          |
| `REGEXP_REPLACE`      | [`REGEXP_REPLACE`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/string_functions#regexp_replace)                          |
| `REPLACE`             | [`REPLACE`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/string_functions#replace)                                        |
| `REVERSE`             | [`REVERSE`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/string_functions#reverse)                                        |
| `RPAD`                | [`RPAD`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/string_functions#rpad)                                              |
| `RTRIM`               | [`RTRIM`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/string_functions#rtrim)                                            |
| `SOUNDEX`             | [`SOUNDEX`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/string_functions#soundex)                                        |
| `SPLIT`               | [`SPLIT`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/string_functions#split)` (instring, delimiter)[ORDINAL(tokennum)]` |
| `SUBSTR, \ SUBSTRING` | [`SUBSTR`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/string_functions#substr)                                          |
| `TRANSLATE`           | [`TRANSLATE`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/string_functions#translate)                                    |
| `LTRIM`               | [`LTRIM`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/string_functions#ltrim)                                            |
| `RTRIM`               | [`RTRIM`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/string_functions#rtrim)                                            |
| `TRIM`                | [`TRIM`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/string_functions#trim)                                              |
| `UPPER`               | [`UPPER`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/string_functions#upper)                                            |

BigQuery offers the following additional string functions:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><ul>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/string_functions#byte_length"><code>BYTE_LENGTH</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/string_functions#code_points_to_bytes"><code>CODE_POINTS_TO_BYTES</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/string_functions#ends_with"><code>ENDS_WITH</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/string_functions#from_base32"><code>FROM_BASE32</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/string_functions#from_base64"><code>FROM_BASE64</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/string_functions#from_hex"><code>FROM_HEX</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/string_functions#normalize"><code>NORMALIZE</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/string_functions#normalize_and_casefold"><code>NORMALIZE_AND_CASEFOLD</code></a></li>
</ul></td>
<td><ul>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/string_functions#repeat"><code>REPEAT</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/string_functions#safe_convert_bytes_to_string"><code>SAFE_CONVERT_BYTES_TO_STRING</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/string_functions#split"><code>SPLIT</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/string_functions#starts_with"><code>STARTS_WITH</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/string_functions#strpos"><code>STRPOS</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/string_functions#to_base32"><code>TO_BASE32</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/string_functions#to_base64"><code>TO_BASE64</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/string_functions#to_code_points"><code>TO_CODE_POINTS</code></a></li>
</ul></td>
</tr>
</tbody>
</table>

### Math functions

The following table shows mappings between Hive [math functions](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-MathematicalFunctions) and their BigQuery equivalents:

| **Hive**           | **BigQuery**                                                                                                                                                                                                                                            |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `ABS`              | [`ABS`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#abs)                                                                                                                                                  |
| `ACOS`             | [`ACOS`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#acos)                                                                                                                                                |
| `ASIN`             | [`ASIN`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#asin)                                                                                                                                                |
| `ATAN`             | [`ATAN`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#atan)                                                                                                                                                |
| `CEIL`             | [`CEIL`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#ceil)                                                                                                                                                |
| `CEILING`          | [`CEILING`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#ceiling)                                                                                                                                          |
| `COS`              | [`COS`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#cos)                                                                                                                                                  |
| `FLOOR`            | [`FLOOR`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#floor)                                                                                                                                              |
| `GREATEST`         | [`GREATEST`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#greatest)                                                                                                                                        |
| `LEAST`            | [`LEAST`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#least)                                                                                                                                              |
| `LN`               | [`LN`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#ln)                                                                                                                                                    |
| `LNNVL`            | Use with `ISNULL` .                                                                                                                                                                                                                                     |
| `LOG`              | [`LOG`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#log)                                                                                                                                                  |
| `MOD (% operator)` | [`MOD`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#mod)                                                                                                                                                  |
| `POWER`            | [`POWER`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#power)` , `[`POW`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#pow)                                   |
| `RAND`             | [`RAND`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#rand)                                                                                                                                                |
| `ROUND`            | [`ROUND`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#round)                                                                                                                                              |
| `SIGN`             | [`SIGN`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#sign)                                                                                                                                                |
| `SIN`              | [`SIN`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#sin)                                                                                                                                                  |
| `SQRT`             | [`SQRT`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#sqrt)                                                                                                                                                |
| `HASH`             | [`FARM_FINGERPRINT, MD5, SHA1, SHA256, SHA512`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/hash_functions)                                                                                                                      |
| `STDDEV_POP`       | [`STDDEV_POP`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/statistical_aggregate_functions#stddev_pop)                                                                                                                           |
| `STDDEV_SAMP`      | [`STDDEV_SAMP`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/statistical_aggregate_functions#stddev_samp)                                                                                                                         |
| `TAN`              | [`TAN`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#tan)                                                                                                                                                  |
| `TRUNC`            | [`TRUNC`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#trunc)                                                                                                                                              |
| `NVL`              | [`IFNULL`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/conditional_expressions#ifnull)` (expr, 0), `[`COALESCE`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/conditional_expressions#coalesce)` (exp, 0)` |

BigQuery offers the following additional math functions:

- [`DIV`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#div)
- [`IEEE_DIVIDE`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#ieee_divide)
- [`IS_INF`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#is_inf)
- [`IS_NAN`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#is_nan)
- [`LOG10`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#log10)
- [`SAFE_DIVIDE`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#safe_divide)

### Logical and conditional functions

The following table shows mappings between Hive logical and conditional functions and their BigQuery equivalents:

| **Hive**                                                                                                                  | **BigQuery**                                                                                                                                                                                                                                            |
|---------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [`CASE`](https://cwiki.apache.org/confluence/display/hive/languagemanual+udf#LanguageManualUDF-ConditionalFunctions)      | [`CASE`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/conditional_expressions#case_expr)                                                                                                                                          |
| [`COALESCE`](https://cwiki.apache.org/confluence/display/hive/languagemanual+udf#LanguageManualUDF-ConditionalFunctions)  | [`COALESCE`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/conditional_expressions#coalesce)                                                                                                                                       |
| [`NVL`](https://cwiki.apache.org/confluence/display/hive/languagemanual+udf#LanguageManualUDF-ConditionalFunctions)       | [`IFNULL`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/conditional_expressions#ifnull)` (expr, 0), `[`COALESCE`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/conditional_expressions#coalesce)` (exp, 0)` |
| [`NULLIF`](https://cwiki.apache.org/confluence/display/hive/languagemanual+udf#LanguageManualUDF-ConditionalFunctions)    | [`NULLIF`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/conditional_expressions#nullif)                                                                                                                                           |
| [`IF`](https://cwiki.apache.org/confluence/display/hive/languagemanual+udf#LanguageManualUDF-ConditionalFunctions)        | [`IF(expr, true_result, else_result)`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/conditional_expressions#if)                                                                                                                   |
| [`ISNULL`](https://cwiki.apache.org/confluence/display/hive/languagemanual+udf#LanguageManualUDF-ConditionalFunctions)    | `IS NULL`                                                                                                                                                                                                                                               |
| [`ISNOTNULL`](https://cwiki.apache.org/confluence/display/hive/languagemanual+udf#LanguageManualUDF-ConditionalFunctions) | `IS NOT NULL`                                                                                                                                                                                                                                           |
| [`NULLIF`](https://cwiki.apache.org/confluence/display/hive/languagemanual+udf#LanguageManualUDF-ConditionalFunctions)    | [`NULLIF`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/conditional_expressions#nullif)                                                                                                                                           |

### UDFs and UDAFs

Apache Hive supports writing user defined functions (UDFs) in Java. You can load UDFs into Hive to be used in regular queries. [BigQuery UDFs](https://docs.cloud.google.com/bigquery/docs/user-defined-functions) must be written in GoogleSQL or JavaScript. Converting the Hive UDFs to SQL UDFs is recommended because SQL UDFs perform better. If you need to use JavaScript, read [Best Practices for JavaScript UDFs](https://docs.cloud.google.com/bigquery/docs/user-defined-functions#best-practices-for-javascript-udfs) . For other languages, BigQuery supports [remote functions](https://docs.cloud.google.com/bigquery/docs/remote-functions) that let you invoke your functions in [Cloud Run functions](https://docs.cloud.google.com/functions/docs/concepts/overview) or [Cloud Run](https://docs.cloud.google.com/run/docs/overview/what-is-cloud-run) from GoogleSQL queries.

BigQuery does not support user-defined aggregation functions (UDAFs).

## DML syntax

This section addresses differences in data manipulation language (DML) syntax between Hive and BigQuery.

### `INSERT` statement

Most Hive `INSERT` statements are compatible with BigQuery. The following table shows exceptions:

| **Hive**                                                                                                                                                                 | **BigQuery**                                                                                                                                                                                                                                                                                                                                    |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `INSERT INTO TABLE tablename [PARTITION (partcol1[=val1], partcol2[=val2] ...)] VALUES values_row [, values_row ...]`                                                    | [`INSERT INTO`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/dml-syntax#insert_statement)` `*`table`*` (...) VALUES (...);` Note: In BigQuery, omitting column names in the `INSERT` statement only works if values for all columns in the target table are included in ascending order based on their ordinal positions. |
| `INSERT OVERWRITE [LOCAL] DIRECTORY directory1` `[ROW FORMAT row_format] [STORED AS file_format] (Note: Only available starting with Hive 0.11.0)` `SELECT ... FROM ...` | BigQuery doesn't support the insert-overwrite operations. This Hive syntax can be migrated to [`TRUNCATE`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/dml-syntax#truncate_table_statement) and [`INSERT`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/dml-syntax#insert_statement) statements.   |

BigQuery imposes [DML quotas](https://docs.cloud.google.com/bigquery/quotas#data-manipulation-language-statements) that restrict the number of DML statements that you can execute daily. To make the best use of your quota, consider the following approaches:

- Combine multiple rows in a single `INSERT` statement, instead of one row for each `INSERT` operation.

- Combine multiple DML statements (including `INSERT` ) by using a `MERGE` statement.

- Use `CREATE TABLE ... AS SELECT` to create and populate new tables.

### `UPDATE` statement

Most Hive `UPDATE` statements are compatible with BigQuery. The following table shows exceptions:

| **Hive**                                                                        | **BigQuery**                                                                                                                                                            |
|---------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `UPDATE tablename SET column = value [, column = value ...] [WHERE expression]` | `UPDATE table` `SET column = expression [,...]` `[FROM ...]` `WHERE TRUE` Note: All `UPDATE` statements in BigQuery require a `WHERE` keyword, followed by a condition. |

### `DELETE` and `TRUNCATE` statements

You can use `DELETE` or `TRUNCATE` statements to remove rows from a table without affecting the table schema or indexes.

In BigQuery, the `DELETE` statement must have a `WHERE` clause. For more information about `DELETE` in BigQuery, see [`DELETE` examples](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/dml-syntax#delete_examples) .

| **Hive**                                                                                                                                                           | **BigQuery**                                                                                                                                                                                     |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [`DELETE`](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DML#LanguageManualDML-Delete)` FROM tablename [WHERE expression]`                       | [`DELETE FROM`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/dml-syntax#delete_statement)` table_name` `WHERE TRUE` BigQuery `DELETE` statements require a `WHERE` clause. |
| [`TRUNCATE`](https://cwiki.apache.org/confluence/display/hive/languagemanual+ddl#LanguageManualDDL-TruncateTable)` [TABLE] table_name [PARTITION partition_spec];` | [`TRUNCATE TABLE`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/dml-syntax#truncate_table_statement)` [[project_name.]dataset_name.]table_name`                            |

### `MERGE` statement

The `MERGE` statement can combine `INSERT` , `UPDATE` , and `DELETE` operations into a single *upsert* statement and perform the operations. The `MERGE` operation must match one source row at most for each target row.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Hive</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DML#LanguageManualDML-Merge">MERGE INTO</a> AS T USING
AS S <code>ON</code> <code>WHEN MATCHED [AND ] THEN UPDATE SET</code> <code>WHEN MATCHED [AND ] THEN DELETE</code> <code>WHEN NOT MATCHED [AND ] THEN INSERT VALUES</code></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/dml-syntax#merge_statement"><code>MERGE target</code></a> <code>USING source</code> <code>ON target.key = source.key</code> <code>WHEN MATCHED AND source.filter = 'filter_exp' THEN</code> <code>UPDATE SET</code> <code>target.col1 = source.col1,</code> <code>target.col2 = source.col2,</code> <code>...</code> Note: You must list all columns that need to be updated.</td>
</tr>
</tbody>
</table>

### `ALTER` statement

The following table provides details about converting `CREATE VIEW` statements from Hive to BigQuery:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Function</strong></th>
<th><strong>Hive</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>Rename table</code></td>
<td><a href="https://cwiki.apache.org/confluence/display/hive/languagemanual+ddl#LanguageManualDDL-RenameTable"><code>ALTER TABLE</code></a><code> table_name RENAME TO new_table_name;</code></td>
<td>Not supported. A workaround is to use a copy job with the name that you want as the destination table, and then delete the old one.<br />

<p><code>bq copy project.dataset.old_table project.dataset.new_table</code></p>
<p><code>bq rm --table project.dataset.old_table</code></p></td>
</tr>
<tr class="even">
<td><code>Table properties</code></td>
<td><a href="https://cwiki.apache.org/confluence/display/hive/languagemanual+ddl#LanguageManualDDL-AlterTableProperties"><code>ALTER TABLE</code></a><code> table_name SET TBLPROPERTIES table_properties;</code>
<p><code>table_properties:</code></p>
<p><code>: (property_name = property_value, property_name = property_value, ... )</code></p>
<p><strong><code>Table Comment:</code></strong> <code>ALTER TABLE table_name SET TBLPROPERTIES ('comment' = new_comment);</code></p></td>
<td><code>{ALTER TABLE | ALTER TABLE IF EXISTS}</code>
<p><code>table_name</code></p>
<p><code>SET OPTIONS( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#table_set_options_list"><code>table_set_options_list</code></a><code> )</code></p></td>
</tr>
<tr class="odd">
<td><code>SerDe properties (Serialize and deserialize)</code></td>
<td><a href="https://cwiki.apache.org/confluence/display/hive/languagemanual+ddl#LanguageManualDDL-AddSerDeProperties"><code>ALTER TABLE</code></a><code> table_name [PARTITION partition_spec] SET SERDE serde_class_name [WITH SERDEPROPERTIES serde_properties];</code>
<p><code>ALTER TABLE table_name [PARTITION partition_spec] SET SERDEPROPERTIES serde_properties;</code></p>
<p><code>serde_properties:</code></p>
<p><code>: (property_name = property_value, property_name = property_value, ... )</code></p></td>
<td>Serialization and deserialization is managed by the BigQuery service and isn't user configurable.
<p>To learn how to let BigQuery read data from CSV, JSON, AVRO, PARQUET, or ORC files, see <a href="https://docs.cloud.google.com/bigquery/docs/external-data-cloud-storage">Create Cloud Storage external tables</a> .</p>
<p>Supports CSV, JSON, AVRO, and PARQUET export formats. For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/exporting-data#export_formats_and_compression_types">Export formats and compression types</a> .</p></td>
</tr>
<tr class="even">
<td><code>Table storage properties</code></td>
<td><a href="https://cwiki.apache.org/confluence/display/hive/languagemanual+ddl#LanguageManualDDL-AlterTableStorageProperties"><code>ALTER TABLE</code></a><code> table_name CLUSTERED BY (col_name, col_name, ...) [SORTED BY (col_name, ...)]</code> <code>INTO num_buckets BUCKETS;</code></td>
<td>Not supported for the <code>ALTER</code> statements.</td>
</tr>
<tr class="odd">
<td><code>Skewed table</code></td>
<td><strong><code>Skewed:</code></strong> <a href="https://cwiki.apache.org/confluence/display/hive/languagemanual+ddl#LanguageManualDDL-AlterTableSkewedorStoredasDirectories"><code>ALTER TABLE</code></a><code> table_name SKEWED BY (col_name1, col_name2, ...)</code> <code>ON ([(col_name1_value, col_name2_value, ...) [, (col_name1_value, col_name2_value), ...]</code>
<p><code>[STORED AS DIRECTORIES];</code></p>
<p><strong><code>Not Skewed:</code></strong> <code>ALTER TABLE table_name NOT SKEWED;</code></p>
<p><strong><code>Not Stored as Directories:</code></strong> <code>ALTER TABLE table_name NOT STORED AS DIRECTORIES;</code></p>
<p><strong><code>Skewed Location:</code></strong> <code>ALTER TABLE table_name SET SKEWED LOCATION (col_name1="location1" [, col_name2="location2", ...] );</code></p></td>
<td>Balancing storage for performance queries is managed by the BigQuery service and isn't configurable.</td>
</tr>
<tr class="even">
<td><code>Table constraints</code></td>
<td><a href="https://cwiki.apache.org/confluence/display/hive/languagemanual+ddl#LanguageManualDDL-AlterTableConstraints"><code>ALTER TABLE</code></a><code> table_name ADD CONSTRAINT constraint_name PRIMARY KEY (column, ...) DISABLE NOVALIDATE;</code> <code>ALTER TABLE table_name ADD CONSTRAINT constraint_name FOREIGN KEY (column, ...) REFERENCES table_name(column, ...) DISABLE NOVALIDATE RELY;</code>
<p><code>ALTER TABLE table_name DROP CONSTRAINT constraint_name;</code></p></td>
<td><code>ALTER TABLE [[project_name.]dataset_name.]table_name</code><br />
<code>ADD [CONSTRAINT [IF NOT EXISTS] [constraint_name]] constraint NOT ENFORCED;</code><br />
<code>ALTER TABLE [[project_name.]dataset_name.]table_name</code><br />
<code>ADD PRIMARY KEY(column_list) NOT ENFORCED;</code><br />

<p>For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#alter_table_add_primary_key_statement"><code>ALTER TABLE ADD PRIMARY KEY</code> statement</a> .</p></td>
</tr>
<tr class="odd">
<td><code>Add partition</code></td>
<td><a href="https://cwiki.apache.org/confluence/display/hive/languagemanual+ddl#LanguageManualDDL-AlterEitherTableorPartition"><code>ALTER TABLE</code></a><code> table_name ADD [IF NOT EXISTS] PARTITION partition_spec [LOCATION 'location'][, PARTITION partition_spec [LOCATION 'location'], ...];</code>
<p><code>partition_spec:</code></p>
<p><code>: (partition_column = partition_col_value, partition_column = partition_col_value, ...)</code></p></td>
<td>Not supported. Additional partitions are added as needed when data with new values in the partition columns are loaded.<br />

<p>For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/managing-partitioned-tables">Manage partitioned tables</a> .</p></td>
</tr>
<tr class="even">
<td><code>Rename partition</code></td>
<td><a href="https://cwiki.apache.org/confluence/display/hive/languagemanual+ddl#LanguageManualDDL-RenamePartition"><code>ALTER TABLE</code></a><code> table_name PARTITION partition_spec RENAME TO PARTITION partition_spec;</code></td>
<td>Not supported.</td>
</tr>
<tr class="odd">
<td><code>Exchange partition</code></td>
<td><code>-- Move partition from table_name_1 to table_name_2</code>
<p><code>ALTER TABLE table_name_2 </code><a href="https://cwiki.apache.org/confluence/display/hive/languagemanual+ddl#LanguageManualDDL-ExchangePartition"><code>EXCHANGE</code></a><code> PARTITION (partition_spec) WITH TABLE table_name_1;</code> <code>-- multiple partitions</code></p>
<p><code>ALTER TABLE table_name_2 EXCHANGE PARTITION (partition_spec, partition_spec2, ...) WITH TABLE table_name_1;</code></p></td>
<td>Not supported.</td>
</tr>
<tr class="even">
<td><code>Recover partition</code></td>
<td><a href="https://cwiki.apache.org/confluence/display/hive/languagemanual+ddl#LanguageManualDDL-RecoverPartitions(MSCKREPAIRTABLE)"><code>MSCK [REPAIR]</code></a><code> TABLE table_name [ADD/DROP/SYNC PARTITIONS];</code></td>
<td>Not supported.</td>
</tr>
<tr class="odd">
<td><code>Drop partition</code></td>
<td><a href="https://cwiki.apache.org/confluence/display/hive/languagemanual+ddl#LanguageManualDDL-DropPartitions"><code>ALTER TABLE table_name DROP</code></a><code> [IF EXISTS] PARTITION partition_spec[, PARTITION partition_spec, ...]</code> <code>[IGNORE PROTECTION] [PURGE];</code></td>
<td>Supported using the following methods:
<ul>
<li><code>bq rm 'mydataset.table_name$partition_id'</code></li>
<li><code>DELETE from table_name$partition_id WHERE 1=1</code></li>
</ul>
<br />

<p>For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/managing-partitioned-tables#delete_a_partition">Delete a partition</a> .</p></td>
</tr>
<tr class="even">
<td><code>(Un)Archive partition</code></td>
<td><a href="https://cwiki.apache.org/confluence/display/hive/languagemanual+ddl#LanguageManualDDL-(Un)ArchivePartition"><code>ALTER TABLE table_name ARCHIVE</code></a><code> PARTITION partition_spec;</code> <code>ALTER TABLE table_name UNARCHIVE PARTITION partition_spec;</code></td>
<td>Not supported.</td>
</tr>
<tr class="odd">
<td><code>Table and partition file format</code></td>
<td><a href="https://cwiki.apache.org/confluence/display/hive/languagemanual+ddl#LanguageManualDDL-AlterTable/PartitionFileFormat"><code>ALTER TABLE table_name [PARTITION partition_spec]</code></a><code> SET FILEFORMAT file_format;</code></td>
<td>Not supported.</td>
</tr>
<tr class="even">
<td><code>Table and partition location</code></td>
<td><a href="https://cwiki.apache.org/confluence/display/hive/languagemanual+ddl#LanguageManualDDL-AlterTable/PartitionLocation"><code>ALTER TABLE table_name [PARTITION partition_spec]</code></a><code> SET LOCATION "new location";</code></td>
<td>Not supported.</td>
</tr>
<tr class="odd">
<td><code>Table and partition touch</code></td>
<td><a href="https://cwiki.apache.org/confluence/display/hive/languagemanual+ddl#LanguageManualDDL-AlterTable/PartitionTouch"><code>ALTER TABLE table_name TOUCH</code></a><code> [PARTITION partition_spec];</code></td>
<td>Not supported.</td>
</tr>
<tr class="even">
<td><code>Table and partition protection</code></td>
<td><a href="https://cwiki.apache.org/confluence/display/hive/languagemanual+ddl#LanguageManualDDL-AlterTable/PartitionProtections"><code>ALTER TABLE table_name [PARTITION partition_spec]</code></a><code> ENABLE|DISABLE NO_DROP [CASCADE];</code>
<p><code>ALTER TABLE table_name [PARTITION partition_spec] ENABLE|DISABLE OFFLINE;</code></p></td>
<td>Not supported.</td>
</tr>
<tr class="odd">
<td><code>Table and partition compact</code></td>
<td><a href="https://cwiki.apache.org/confluence/display/hive/languagemanual+ddl#LanguageManualDDL-AlterTable/PartitionCompact"><code>ALTER TABLE table_name [PARTITION (partition_key = 'partition_value' [, ...])]</code></a> <code>COMPACT 'compaction_type'[AND WAIT]</code>
<p><code>[WITH OVERWRITE TBLPROPERTIES ("property"="value" [, ...])];</code></p></td>
<td>Not supported.</td>
</tr>
<tr class="even">
<td><code>Table and artition concatenate</code></td>
<td><a href="https://cwiki.apache.org/confluence/display/hive/languagemanual+ddl#LanguageManualDDL-AlterTable/PartitionConcatenate"><code>ALTER TABLE table_name [PARTITION (partition_key = 'partition_value' [, ...])]</code></a><code> CONCATENATE;</code></td>
<td>Not supported.</td>
</tr>
<tr class="odd">
<td><code>Table and partition columns</code></td>
<td><a href="https://cwiki.apache.org/confluence/display/hive/languagemanual+ddl#LanguageManualDDL-AlterTable/PartitionUpdatecolumns"><code>ALTER TABLE table_name [PARTITION (partition_key = 'partition_value' [, ...])]</code></a><code> UPDATE COLUMNS;</code></td>
<td>Not supported for the <code>ALTER TABLE</code> statements.</td>
</tr>
<tr class="even">
<td><code>Column name, type, position, and comment</code></td>
<td><a href="https://cwiki.apache.org/confluence/display/hive/languagemanual+ddl#LanguageManualDDL-AlterColumn"><code>ALTER TABLE table_name [PARTITION partition_spec]</code></a><code> CHANGE [COLUMN] col_old_name col_new_name column_type</code> <code>[COMMENT col_comment] [FIRST|AFTER column_name] [CASCADE|RESTRICT];</code></td>
<td>Not supported.</td>
</tr>
</tbody>
</table>

## DDL syntax

This section addresses differences in Data Definition Language (DDL) syntax between Hive and BigQuery.

### `CREATE TABLE` and `DROP TABLE` statements

The following table provides details about converting `CREATE TABLE` statements from Hive to BigQuery:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Type</strong></th>
<th><strong>Hive</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Managed tables</td>
<td><code>create table table_name (</code>
<p><code>id int,</code></p>
<p><code>dtDontQuery string,</code></p>
<p><code>name string</code></p>
<p><code>)</code></p></td>
<td><code>CREATE TABLE `myproject`.mydataset.table_name ( </code>
<p>id INT64,</p>
<p>dtDontQuery STRING,</p>
<p>name STRING</p>
<p><code>)</code></p></td>
</tr>
<tr class="even">
<td>Partitioned tables</td>
<td><code>create table table_name (</code>
<p><code>id int,</code></p>
<p><code>dt string,</code></p>
<p><code>name string</code></p>
<p><code>)</code></p>
<p><code>partitioned by (date string)</code></p></td>
<td><code>CREATE TABLE `myproject`.mydataset.table_name ( </code>
<p>id INT64,</p>
<p>dt DATE,</p>
<p>name STRING</p>
<p>)</p>
<p>PARTITION BY dt</p>
<p>OPTIONS(</p>
<p>partition_expiration_days=3,</p>
<p>description="a table partitioned by date_col"</p>
<p><code>)</code></p></td>
</tr>
<tr class="odd">
<td><code>Create table as select (CTAS)</code></td>
<td><code>CREATE TABLE new_key_value_store</code>
<p><code>ROW FORMAT SERDE "org.apache.hadoop.hive.serde2.columnar.ColumnarSerDe"</code></p>
<p><code>STORED AS RCFile</code></p>
<p><code>AS</code></p>
<p><code>SELECT (key % 1024) new_key, concat(key, value) key_value_pair, dt</code></p>
<p><code>FROM key_value_store</code></p>
<p><code>SORT BY new_key, key_value_pair;</code></p></td>
<td><code>CREATE TABLE `myproject`.mydataset.new_key_value_store</code>
<p>When partitioning by date, uncomment the following:</p>
<p><code>PARTITION BY dt</code></p>
<p>OPTIONS(</p>
<p><code>description="Table Description",</code></p>
<p>When partitioning by date, uncomment the following. It's recommended to use <code>require_partition</code> when the table is partitioned.</p>
<p><code>require_partition_filter=TRUE</code></p>
<p><code>) AS</code></p>
<p><code>SELECT (key % 1024) new_key, concat(key, value) key_value_pair, dt</code></p>
<p><code>FROM key_value_store</code></p>
<p><code>SORT BY new_key, key_value_pair'</code></p></td>
</tr>
<tr class="even">
<td><code>Create Table Like:</code>
<p>The <code>LIKE</code> form of <code>CREATE TABLE</code> lets you copy an existing table definition exactly.</p></td>
<td><code>CREATE TABLE empty_key_value_store</code>
<p><code>LIKE key_value_store [TBLPROPERTIES (property_name=property_value, ...)];</code></p></td>
<td>Not supported.</td>
</tr>
<tr class="odd">
<td>Bucketed sorted tables (clustered in BigQuery terminology)</td>
<td><code>CREATE TABLE page_view(</code>
<p><code>viewTime INT,</code></p>
<p><code>userid BIGINT,</code></p>
<p><code>page_url STRING,</code></p>
<p><code>referrer_url STRING,</code></p>
<p><code>ip STRING COMMENT 'IP Address of the User'</code></p>
<p><code>)</code></p>
<p><code>COMMENT 'This is the page view table'</code></p>
<p><code>PARTITIONED BY(dt STRING, country STRING)</code></p>
<p><code>CLUSTERED BY(userid) SORTED BY(viewTime) INTO 32 BUCKETS</code></p>
<p><code>ROW FORMAT DELIMITED</code></p>
<p><code>FIELDS TERMINATED BY '\001'</code></p>
<p><code>COLLECTION ITEMS TERMINATED BY '\002'</code></p>
<p><code>MAP KEYS TERMINATED BY '\003'</code></p>
<p><code>STORED AS SEQUENCEFILE;</code></p></td>
<td><code>CREATE TABLE `myproject` mydataset.page_view ( </code>
<p>viewTime INT,</p>
<p>dt DATE,</p>
<p>userId BIGINT,</p>
<p>page_url STRING,</p>
<p>referrer_url STRING,</p>
<p>ip STRING OPTIONS (description="IP Address of the User")</p>
<p>)</p>
<p>PARTITION BY dt</p>
<p>CLUSTER BY userId</p>
<p>OPTIONS (</p>
<p>partition_expiration_days=3,</p>
<p>description="This is the page view table",</p>
<p>require_partition_filter=TRUE</p>
<p><code>)'</code></p>
<p>For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/creating-clustered-tables">Create and use clustered tables</a> .</p></td>
</tr>
<tr class="even">
<td>Skewed tables (tables where one or more columns have skewed values)</td>
<td><code>CREATE TABLE list_bucket_multiple (col1 STRING, col2 int, col3 STRING)</code>
<p><code>SKEWED BY (col1, col2) ON (('s1',1), ('s3',3), ('s13',13), ('s78',78)) [STORED AS DIRECTORIES];</code></p></td>
<td>Not supported.</td>
</tr>
<tr class="odd">
<td>Temporary tables</td>
<td><code>CREATE TEMPORARY TABLE list_bucket_multiple (</code>
<p><code>col1 STRING,</code></p>
<p><code>col2 int,</code></p>
<p><code>col3 STRING);</code></p></td>
<td>You can achieve this using expiration time as follows:
<p><code>CREATE TABLE mydataset.newtable</code></p>
<p><code>(</code></p>
<p><code>col1 STRING OPTIONS(description="An optional INTEGER field"),</code></p>
<p><code>col2 INT64,</code></p>
<p><code>col3 STRING</code></p>
<p><code>)</code></p>
<p><code>PARTITION BY DATE(_PARTITIONTIME)</code></p>
<p><code>OPTIONS(</code></p>
<p><code>expiration_timestamp=TIMESTAMP "2020-01-01 00:00:00 UTC",</code></p>
<p><code>partition_expiration_days=1,</code></p>
<p><code>description="a table that expires in 2020, with each partition living for 24 hours",</code></p>
<p><code>labels=[("org_unit", "development")]</code></p>
<p><code>)</code></p></td>
</tr>
<tr class="even">
<td>Transactional tables</td>
<td><code>CREATE TRANSACTIONAL TABLE transactional_table_test(key string, value string) PARTITIONED BY(ds string) STORED AS ORC;</code></td>
<td>All table modifications in BigQuery are ACID (atomicity, consistency, isolation, durability) compliant.</td>
</tr>
<tr class="odd">
<td>Drop table</td>
<td><code>DROP TABLE [IF EXISTS] table_name [PURGE];</code></td>
<td><code>{DROP TABLE | DROP TABLE IF EXISTS}</code>
<p><code>table_name</code></p></td>
</tr>
<tr class="even">
<td>Truncate table</td>
<td><code>TRUNCATE TABLE table_name [PARTITION partition_spec];</code>
<p><code>partition_spec:</code></p>
<p><code>: (partition_column = partition_col_value, partition_column = partition_col_value, ...)</code></p></td>
<td>Not supported. The following workarounds are available:
<ul>
<li>Drop and create the table again with the same schema.</li>
<li>Set write disposition for table to <code>WRITE_TRUNCATE</code> if the truncate operation is a common use case for the given table.</li>
<li>Use the <code>CREATE OR REPLACE TABLE</code> statement.</li>
<li>Use the <code>DELETE from table_name WHERE 1=1</code> statement.</li>
</ul>
<p>Note: Specific partitions can also be truncated. For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/managing-partitioned-tables#delete_a_partition">Delete a partition</a> .</p></td>
</tr>
</tbody>
</table>

### `CREATE EXTERNAL TABLE` and `DROP EXTERNAL TABLE` statements

For external table support in BigQuery, see [Introduction to external data sources](https://docs.cloud.google.com/bigquery/external-data-sources) .

### `CREATE VIEW` and `DROP VIEW` statements

The following table provides details about converting `CREATE VIEW` statements from Hive to BigQuery:

| **Hive**                                                                                                                                                                                                                                                                                                                                                                                           | **BigQuery**                                                                                                                                                                                                                                                                                                                                                                                                               |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `CREATE VIEW [IF NOT EXISTS] [db_name.]view_name [(column_name [COMMENT column_comment], ...) ]` `[COMMENT view_comment]` `[TBLPROPERTIES (property_name = property_value, ...)]` `AS SELECT ...;`                                                                                                                                                                                                 | `{CREATE VIEW | CREATE VIEW IF NOT EXISTS | CREATE OR REPLACE VIEW} view_name [OPTIONS( `[`view_option_list`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#view_option_list)` )] ` `AS query_expression`                                                                                                                                                                    |
| `CREATE MATERIALIZED VIEW [IF NOT EXISTS] [db_name.]materialized_view_name` `[DISABLE REWRITE]` `[COMMENT materialized_view_comment]` `[PARTITIONED ON (col_name, ...)]` `[` `[ROW FORMAT row_format]` `[STORED AS file_format]` `| STORED BY 'storage.handler.class.name' [WITH SERDEPROPERTIES (...)]` `]` `[LOCATION hdfs_path]` `[TBLPROPERTIES (property_name=property_value, ...)]` `AS` `;` | `CREATE MATERIALIZED VIEW [IF NOT EXISTS] \ [project_id].[dataset_id].materialized_view_name -- cannot disable rewrites in BigQuery [OPTIONS( [description="materialized_view_comment",] \ [other `[`materialized_view_option_list`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#materialized_view_option_list)` ] )] ` `[PARTITION BY (col_name)] --same as source table` |

### `CREATE FUNCTION` and `DROP FUNCTION` statements

The following table provides details about converting stored procedures from Hive to BigQuery:

| **Hive**                                                                                                                        | **BigQuery**                                                                                                                                                                                                                                                |
|---------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `CREATE TEMPORARY FUNCTION function_name AS class_name;`                                                                        | `CREATE { TEMPORARY | TEMP } FUNCTION function_name ([named_parameter[, ...]])` `[RETURNS data_type]` `AS (sql_expression)` `named_parameter:` `param_name param_type`                                                                                      |
| `DROP TEMPORARY FUNCTION [IF EXISTS] function_name;`                                                                            | Not supported.                                                                                                                                                                                                                                              |
| `CREATE FUNCTION [db_name.]function_name AS class_name` `[USING JAR|FILE|ARCHIVE 'file_uri' [, JAR|FILE|ARCHIVE 'file_uri'] ];` | Supported for allowlisted projects as an alpha feature. `CREATE { FUNCTION | FUNCTION IF NOT EXISTS | OR REPLACE FUNCTION }` `function_name ([named_parameter[, ...]])` `[RETURNS data_type]` `AS (expression);` `named_parameter:` `param_name param_type` |
| `DROP FUNCTION [IF EXISTS] function_name;`                                                                                      | `DROP FUNCTION [ IF EXISTS ] function_name`                                                                                                                                                                                                                 |
| `RELOAD FUNCTION;`                                                                                                              | Not supported.                                                                                                                                                                                                                                              |

### `CREATE MACRO` and `DROP MACRO` statements

The following table provides details about converting procedural SQL statements used in creating macro from Hive to BigQuery with variable declaration and assignment:

| **Hive**                                                                  | **BigQuery**                                                      |
|---------------------------------------------------------------------------|-------------------------------------------------------------------|
| `CREATE TEMPORARY MACRO macro_name([col_name col_type, ...]) expression;` | Not supported. In some cases, this can be substituted with a UDF. |
| `DROP TEMPORARY MACRO [IF EXISTS] macro_name;`                            | Not supported.                                                    |

## Error codes and messages

[Hive error codes](https://cwiki.apache.org/confluence/display/GEODE/Error+Codes) and [BigQuery error codes](https://docs.cloud.google.com/bigquery/troubleshooting-errors) are different. If your application logic is catching errors, eliminate the source of the error because BigQuery doesn't return the same error codes.

In BigQuery, it's common to use the [INFORMATION_SCHEMA](https://docs.cloud.google.com/bigquery/docs/information-schema-jobs) views or [audit logging](https://docs.cloud.google.com/bigquery/docs/reference/auditlogs) to examine errors.

## Consistency guarantees and transaction isolation

Both Hive and BigQuery support transactions with ACID semantics. [Transactions](https://cwiki.apache.org/confluence/display/Hive/Hive+Transactions#HiveTransactions-ACIDandTransactionsinHive) are enabled by default in Hive 3.

### ACID semantics

Hive supports [snapshot isolation](https://cwiki.apache.org/confluence/display/hive/hive+transactions) . When you execute a query, the query is provided with a consistent snapshot of the database, which it uses until the end of its execution. Hive provides full ACID semantics at the row level, letting one application add rows when another application reads from the same partition without interfering with each other.

BigQuery provides [optimistic concurrency control](https://en.wikipedia.org/wiki/Optimistic_concurrency_control) (first to commit wins) with [snapshot isolation](https://en.wikipedia.org/wiki/Snapshot_isolation) , in which a query reads the last committed data before the query starts. This approach guarantees the same level of consistency for each row and mutation, and across rows within the same DML statement, while avoiding deadlocks. For multiple DML updates to the same table, BigQuery switches to [pessimistic concurrency control](https://docs.cloud.google.com/bigquery/docs/data-manipulation-language#dml-limitations) . Load jobs can run independently and append tables; however, BigQuery doesn't provide an explicit transaction boundary or session.

### Transactions

Hive doesn't support multi-statement transactions. It doesn't support `BEGIN` , `COMMIT` , and `ROLLBACK` statements. In Hive, all language operations are auto-committed.

BigQuery supports multi-statement transactions inside a single query or across multiple queries when you use sessions. A multi-statement transaction lets you perform mutating operations, such as inserting or deleting rows from one or more tables and either committing or rolling back the changes. For more information, see [Multi-statement transactions](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/transactions) .
