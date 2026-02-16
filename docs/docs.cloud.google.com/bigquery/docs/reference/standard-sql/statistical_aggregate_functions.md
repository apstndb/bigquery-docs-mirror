GoogleSQL for BigQuery supports statistical aggregate functions. To learn about the syntax for aggregate function calls, see [Aggregate function calls](/bigquery/docs/reference/standard-sql/aggregate-function-calls) .

## Function list

<table>
<thead>
<tr class="header">
<th>Name</th>
<th>Summary</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/statistical_aggregate_functions#corr"><code dir="ltr" translate="no">        CORR       </code></a></td>
<td>Computes the Pearson coefficient of correlation of a set of number pairs.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/statistical_aggregate_functions#covar_pop"><code dir="ltr" translate="no">        COVAR_POP       </code></a></td>
<td>Computes the population covariance of a set of number pairs.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/statistical_aggregate_functions#covar_samp"><code dir="ltr" translate="no">        COVAR_SAMP       </code></a></td>
<td>Computes the sample covariance of a set of number pairs.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/statistical_aggregate_functions#stddev"><code dir="ltr" translate="no">        STDDEV       </code></a></td>
<td>An alias of the <code dir="ltr" translate="no">       STDDEV_SAMP      </code> function.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/statistical_aggregate_functions#stddev_pop"><code dir="ltr" translate="no">        STDDEV_POP       </code></a></td>
<td>Computes the population (biased) standard deviation of the values.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/statistical_aggregate_functions#stddev_samp"><code dir="ltr" translate="no">        STDDEV_SAMP       </code></a></td>
<td>Computes the sample (unbiased) standard deviation of the values.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/statistical_aggregate_functions#var_pop"><code dir="ltr" translate="no">        VAR_POP       </code></a></td>
<td>Computes the population (biased) variance of the values.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/statistical_aggregate_functions#var_samp"><code dir="ltr" translate="no">        VAR_SAMP       </code></a></td>
<td>Computes the sample (unbiased) variance of the values.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/statistical_aggregate_functions#variance"><code dir="ltr" translate="no">        VARIANCE       </code></a></td>
<td>An alias of <code dir="ltr" translate="no">       VAR_SAMP      </code> .</td>
</tr>
</tbody>
</table>

## `     CORR    `

``` text
CORR(
  X1, X2
)
[ OVER over_clause ]

over_clause:
  { named_window | ( [ window_specification ] ) }

window_specification:
  [ named_window ]
  [ PARTITION BY partition_expression [, ...] ]
  [ ORDER BY expression [ { ASC | DESC }  ] [, ...] ]
  [ window_frame_clause ]
```

**Description**

Returns the [Pearson coefficient](https://en.wikipedia.org/wiki/Pearson_product-moment_correlation_coefficient) of correlation of a set of number pairs. For each number pair, the first number is the dependent variable and the second number is the independent variable. The return result is between `  -1  ` and `  1  ` . A result of `  0  ` indicates no correlation.

All numeric types are supported. If the input is `  NUMERIC  ` or `  BIGNUMERIC  ` then the internal aggregation is stable with the final output converted to a `  FLOAT64  ` . Otherwise the input is converted to a `  FLOAT64  ` before aggregation, resulting in a potentially unstable result.

This function ignores any input pairs that contain one or more `  NULL  ` values. If there are fewer than two input pairs without `  NULL  ` values, this function returns `  NULL  ` .

`  NaN  ` is produced if:

  - Any input value is `  NaN  `
  - Any input value is positive infinity or negative infinity.
  - The variance of `  X1  ` or `  X2  ` is `  0  ` .
  - The covariance of `  X1  ` and `  X2  ` is `  0  ` .

To learn more about the optional aggregate clauses that you can pass into this function, see [Aggregate function calls](/bigquery/docs/reference/standard-sql/aggregate-function-calls) .

To learn more about the `  OVER  ` clause and how to use it, see [Window function calls](/bigquery/docs/reference/standard-sql/window-function-calls) .

**Return Data Type**

`  FLOAT64  `

**Examples**

``` text
SELECT CORR(y, x) AS results
FROM
  UNNEST(
    [
      STRUCT(1.0 AS y, 5.0 AS x),
      (3.0, 9.0),
      (4.0, 7.0)]);

/*--------------------+
 | results            |
 +--------------------+
 | 0.6546536707079772 |
 +--------------------*/
```

``` text
SELECT CORR(y, x) AS results
FROM
  UNNEST(
    [
      STRUCT(1.0 AS y, 5.0 AS x),
      (3.0, 9.0),
      (4.0, NULL)]);

/*---------+
 | results |
 +---------+
 | 1       |
 +---------*/
```

``` text
SELECT CORR(y, x) AS results
FROM UNNEST([STRUCT(1.0 AS y, NULL AS x),(9.0, 3.0)])

/*---------+
 | results |
 +---------+
 | NULL    |
 +---------*/
```

``` text
SELECT CORR(y, x) AS results
FROM UNNEST([STRUCT(1.0 AS y, NULL AS x),(9.0, NULL)])

/*---------+
 | results |
 +---------+
 | NULL    |
 +---------*/
```

``` text
SELECT CORR(y, x) AS results
FROM
  UNNEST(
    [
      STRUCT(1.0 AS y, 5.0 AS x),
      (3.0, 9.0),
      (4.0, 7.0),
      (5.0, 1.0),
      (7.0, CAST('Infinity' as FLOAT64))])

/*---------+
 | results |
 +---------+
 | NaN     |
 +---------*/
```

``` text
SELECT CORR(x, y) AS results
FROM
  (
    SELECT 0 AS x, 0 AS y
    UNION ALL
    SELECT 0 AS x, 0 AS y
  )

/*---------+
 | results |
 +---------+
 | NaN     |
 +---------*/
```

## `     COVAR_POP    `

``` text
COVAR_POP(
  X1, X2
)
[ OVER over_clause ]

over_clause:
  { named_window | ( [ window_specification ] ) }

window_specification:
  [ named_window ]
  [ PARTITION BY partition_expression [, ...] ]
  [ ORDER BY expression [ { ASC | DESC }  ] [, ...] ]
  [ window_frame_clause ]
```

**Description**

Returns the population [covariance](https://en.wikipedia.org/wiki/Covariance) of a set of number pairs. The first number is the dependent variable; the second number is the independent variable. The return result is between `  -Inf  ` and `  +Inf  ` .

All numeric types are supported. If the input is `  NUMERIC  ` or `  BIGNUMERIC  ` then the internal aggregation is stable with the final output converted to a `  FLOAT64  ` . Otherwise the input is converted to a `  FLOAT64  ` before aggregation, resulting in a potentially unstable result.

This function ignores any input pairs that contain one or more `  NULL  ` values. If there is no input pair without `  NULL  ` values, this function returns `  NULL  ` . If there is exactly one input pair without `  NULL  ` values, this function returns `  0  ` .

`  NaN  ` is produced if:

  - Any input value is `  NaN  `
  - Any input value is positive infinity or negative infinity.

To learn more about the optional aggregate clauses that you can pass into this function, see [Aggregate function calls](/bigquery/docs/reference/standard-sql/aggregate-function-calls) .

This function can be used with the [`  AGGREGATION_THRESHOLD  ` clause](/bigquery/docs/reference/standard-sql/query-syntax#agg_threshold_clause) .

To learn more about the `  OVER  ` clause and how to use it, see [Window function calls](/bigquery/docs/reference/standard-sql/window-function-calls) .

**Return Data Type**

`  FLOAT64  `

**Examples**

``` text
SELECT COVAR_POP(y, x) AS results
FROM
  UNNEST(
    [
      STRUCT(1.0 AS y, 1.0 AS x),
      (2.0, 6.0),
      (9.0, 3.0),
      (2.0, 6.0),
      (9.0, 3.0)])

/*---------------------+
 | results             |
 +---------------------+
 | -1.6800000000000002 |
 +---------------------*/
```

``` text
SELECT COVAR_POP(y, x) AS results
FROM UNNEST([STRUCT(1.0 AS y, NULL AS x),(9.0, 3.0)])

/*---------+
 | results |
 +---------+
 | 0       |
 +---------*/
```

``` text
SELECT COVAR_POP(y, x) AS results
FROM UNNEST([STRUCT(1.0 AS y, NULL AS x),(9.0, NULL)])

/*---------+
 | results |
 +---------+
 | NULL    |
 +---------*/
```

``` text
SELECT COVAR_POP(y, x) AS results
FROM
  UNNEST(
    [
      STRUCT(1.0 AS y, 1.0 AS x),
      (2.0, 6.0),
      (9.0, 3.0),
      (2.0, 6.0),
      (NULL, 3.0)])

/*---------+
 | results |
 +---------+
 | -1      |
 +---------*/
```

``` text
SELECT COVAR_POP(y, x) AS results
FROM
  UNNEST(
    [
      STRUCT(1.0 AS y, 1.0 AS x),
      (2.0, 6.0),
      (9.0, 3.0),
      (2.0, 6.0),
      (CAST('Infinity' as FLOAT64), 3.0)])

/*---------+
 | results |
 +---------+
 | NaN     |
 +---------*/
```

## `     COVAR_SAMP    `

``` text
COVAR_SAMP(
  X1, X2
)
[ OVER over_clause ]

over_clause:
  { named_window | ( [ window_specification ] ) }

window_specification:
  [ named_window ]
  [ PARTITION BY partition_expression [, ...] ]
  [ ORDER BY expression [ { ASC | DESC }  ] [, ...] ]
  [ window_frame_clause ]
```

**Description**

Returns the sample [covariance](https://en.wikipedia.org/wiki/Covariance) of a set of number pairs. The first number is the dependent variable; the second number is the independent variable. The return result is between `  -Inf  ` and `  +Inf  ` .

All numeric types are supported. If the input is `  NUMERIC  ` or `  BIGNUMERIC  ` then the internal aggregation is stable with the final output converted to a `  FLOAT64  ` . Otherwise the input is converted to a `  FLOAT64  ` before aggregation, resulting in a potentially unstable result.

This function ignores any input pairs that contain one or more `  NULL  ` values. If there are fewer than two input pairs without `  NULL  ` values, this function returns `  NULL  ` .

`  NaN  ` is produced if:

  - Any input value is `  NaN  `
  - Any input value is positive infinity or negative infinity.

To learn more about the optional aggregate clauses that you can pass into this function, see [Aggregate function calls](/bigquery/docs/reference/standard-sql/aggregate-function-calls) .

This function can be used with the [`  AGGREGATION_THRESHOLD  ` clause](/bigquery/docs/reference/standard-sql/query-syntax#agg_threshold_clause) .

To learn more about the `  OVER  ` clause and how to use it, see [Window function calls](/bigquery/docs/reference/standard-sql/window-function-calls) .

**Return Data Type**

`  FLOAT64  `

**Examples**

``` text
SELECT COVAR_SAMP(y, x) AS results
FROM
  UNNEST(
    [
      STRUCT(1.0 AS y, 1.0 AS x),
      (2.0, 6.0),
      (9.0, 3.0),
      (2.0, 6.0),
      (9.0, 3.0)])

/*---------+
 | results |
 +---------+
 | -2.1    |
 +---------*/
```

``` text
SELECT COVAR_SAMP(y, x) AS results
FROM
  UNNEST(
    [
      STRUCT(1.0 AS y, 1.0 AS x),
      (2.0, 6.0),
      (9.0, 3.0),
      (2.0, 6.0),
      (NULL, 3.0)])

/*----------------------+
 | results              |
 +----------------------+
 | --1.3333333333333333 |
 +----------------------*/
```

``` text
SELECT COVAR_SAMP(y, x) AS results
FROM UNNEST([STRUCT(1.0 AS y, NULL AS x),(9.0, 3.0)])

/*---------+
 | results |
 +---------+
 | NULL    |
 +---------*/
```

``` text
SELECT COVAR_SAMP(y, x) AS results
FROM UNNEST([STRUCT(1.0 AS y, NULL AS x),(9.0, NULL)])

/*---------+
 | results |
 +---------+
 | NULL    |
 +---------*/
```

``` text
SELECT COVAR_SAMP(y, x) AS results
FROM
  UNNEST(
    [
      STRUCT(1.0 AS y, 1.0 AS x),
      (2.0, 6.0),
      (9.0, 3.0),
      (2.0, 6.0),
      (CAST('Infinity' as FLOAT64), 3.0)])

/*---------+
 | results |
 +---------+
 | NaN     |
 +---------*/
```

## `     STDDEV    `

``` text
STDDEV(
  [ DISTINCT ]
  expression
)
[ OVER over_clause ]

over_clause:
  { named_window | ( [ window_specification ] ) }

window_specification:
  [ named_window ]
  [ PARTITION BY partition_expression [, ...] ]
  [ ORDER BY expression [ { ASC | DESC }  ] [, ...] ]
  [ window_frame_clause ]
```

**Description**

An alias of [STDDEV\_SAMP](#stddev_samp) .

## `     STDDEV_POP    `

``` text
STDDEV_POP(
  [ DISTINCT ]
  expression
)
[ OVER over_clause ]

over_clause:
  { named_window | ( [ window_specification ] ) }

window_specification:
  [ named_window ]
  [ PARTITION BY partition_expression [, ...] ]
  [ ORDER BY expression [ { ASC | DESC }  ] [, ...] ]
  [ window_frame_clause ]
```

**Description**

Returns the population (biased) standard deviation of the values. The return result is between `  0  ` and `  +Inf  ` .

All numeric types are supported. If the input is `  NUMERIC  ` or `  BIGNUMERIC  ` then the internal aggregation is stable with the final output converted to a `  FLOAT64  ` . Otherwise the input is converted to a `  FLOAT64  ` before aggregation, resulting in a potentially unstable result.

This function ignores any `  NULL  ` inputs. If all inputs are ignored, this function returns `  NULL  ` . If this function receives a single non- `  NULL  ` input, it returns `  0  ` .

`  NaN  ` is produced if:

  - Any input value is `  NaN  `
  - Any input value is positive infinity or negative infinity.

To learn more about the optional aggregate clauses that you can pass into this function, see [Aggregate function calls](/bigquery/docs/reference/standard-sql/aggregate-function-calls) .

This function can be used with the [`  AGGREGATION_THRESHOLD  ` clause](/bigquery/docs/reference/standard-sql/query-syntax#agg_threshold_clause) .

If this function is used with the `  OVER  ` clause, it's part of a window function call. In a window function call, aggregate function clauses can't be used. To learn more about the `  OVER  ` clause and how to use it, see [Window function calls](/bigquery/docs/reference/standard-sql/window-function-calls) .

**Return Data Type**

`  FLOAT64  `

**Examples**

``` text
SELECT STDDEV_POP(x) AS results FROM UNNEST([10, 14, 18]) AS x

/*-------------------+
 | results           |
 +-------------------+
 | 3.265986323710904 |
 +-------------------*/
```

``` text
SELECT STDDEV_POP(x) AS results FROM UNNEST([10, 14, NULL]) AS x

/*---------+
 | results |
 +---------+
 | 2       |
 +---------*/
```

``` text
SELECT STDDEV_POP(x) AS results FROM UNNEST([10, NULL]) AS x

/*---------+
 | results |
 +---------+
 | 0       |
 +---------*/
```

``` text
SELECT STDDEV_POP(x) AS results FROM UNNEST([NULL]) AS x

/*---------+
 | results |
 +---------+
 | NULL    |
 +---------*/
```

``` text
SELECT STDDEV_POP(x) AS results FROM UNNEST([10, 14, CAST('Infinity' as FLOAT64)]) AS x

/*---------+
 | results |
 +---------+
 | NaN     |
 +---------*/
```

## `     STDDEV_SAMP    `

``` text
STDDEV_SAMP(
  [ DISTINCT ]
  expression
)
[ OVER over_clause ]

over_clause:
  { named_window | ( [ window_specification ] ) }

window_specification:
  [ named_window ]
  [ PARTITION BY partition_expression [, ...] ]
  [ ORDER BY expression [ { ASC | DESC }  ] [, ...] ]
  [ window_frame_clause ]
```

**Description**

Returns the sample (unbiased) standard deviation of the values. The return result is between `  0  ` and `  +Inf  ` .

All numeric types are supported. If the input is `  NUMERIC  ` or `  BIGNUMERIC  ` then the internal aggregation is stable with the final output converted to a `  FLOAT64  ` . Otherwise the input is converted to a `  FLOAT64  ` before aggregation, resulting in a potentially unstable result.

This function ignores any `  NULL  ` inputs. If there are fewer than two non- `  NULL  ` inputs, this function returns `  NULL  ` .

`  NaN  ` is produced if:

  - Any input value is `  NaN  `
  - Any input value is positive infinity or negative infinity.

To learn more about the optional aggregate clauses that you can pass into this function, see [Aggregate function calls](/bigquery/docs/reference/standard-sql/aggregate-function-calls) .

This function can be used with the [`  AGGREGATION_THRESHOLD  ` clause](/bigquery/docs/reference/standard-sql/query-syntax#agg_threshold_clause) .

If this function is used with the `  OVER  ` clause, it's part of a window function call. In a window function call, aggregate function clauses can't be used. To learn more about the `  OVER  ` clause and how to use it, see [Window function calls](/bigquery/docs/reference/standard-sql/window-function-calls) .

**Return Data Type**

`  FLOAT64  `

**Examples**

``` text
SELECT STDDEV_SAMP(x) AS results FROM UNNEST([10, 14, 18]) AS x

/*---------+
 | results |
 +---------+
 | 4       |
 +---------*/
```

``` text
SELECT STDDEV_SAMP(x) AS results FROM UNNEST([10, 14, NULL]) AS x

/*--------------------+
 | results            |
 +--------------------+
 | 2.8284271247461903 |
 +--------------------*/
```

``` text
SELECT STDDEV_SAMP(x) AS results FROM UNNEST([10, NULL]) AS x

/*---------+
 | results |
 +---------+
 | NULL    |
 +---------*/
```

``` text
SELECT STDDEV_SAMP(x) AS results FROM UNNEST([NULL]) AS x

/*---------+
 | results |
 +---------+
 | NULL    |
 +---------*/
```

``` text
SELECT STDDEV_SAMP(x) AS results FROM UNNEST([10, 14, CAST('Infinity' as FLOAT64)]) AS x

/*---------+
 | results |
 +---------+
 | NaN     |
 +---------*/
```

## `     VAR_POP    `

``` text
VAR_POP(
  [ DISTINCT ]
  expression
)
[ OVER over_clause ]

over_clause:
  { named_window | ( [ window_specification ] ) }

window_specification:
  [ named_window ]
  [ PARTITION BY partition_expression [, ...] ]
  [ ORDER BY expression [ { ASC | DESC }  ] [, ...] ]
  [ window_frame_clause ]
```

**Description**

Returns the population (biased) variance of the values. The return result is between `  0  ` and `  +Inf  ` .

All numeric types are supported. If the input is `  NUMERIC  ` or `  BIGNUMERIC  ` then the internal aggregation is stable with the final output converted to a `  FLOAT64  ` . Otherwise the input is converted to a `  FLOAT64  ` before aggregation, resulting in a potentially unstable result.

This function ignores any `  NULL  ` inputs. If all inputs are ignored, this function returns `  NULL  ` . If this function receives a single non- `  NULL  ` input, it returns `  0  ` .

`  NaN  ` is produced if:

  - Any input value is `  NaN  `
  - Any input value is positive infinity or negative infinity.

If this function is used with the `  OVER  ` clause, it's part of a window function call. In a window function call, aggregate function clauses can't be used. To learn more about the `  OVER  ` clause and how to use it, see [Window function calls](/bigquery/docs/reference/standard-sql/window-function-calls) .

**Return Data Type**

`  FLOAT64  `

**Examples**

``` text
SELECT VAR_POP(x) AS results FROM UNNEST([10, 14, 18]) AS x

/*--------------------+
 | results            |
 +--------------------+
 | 10.666666666666666 |
 +--------------------*/
```

``` text
SELECT VAR_POP(x) AS results FROM UNNEST([10, 14, NULL]) AS x

/*----------+
 | results |
 +---------+
 | 4       |
 +---------*/
```

``` text
SELECT VAR_POP(x) AS results FROM UNNEST([10, NULL]) AS x

/*----------+
 | results |
 +---------+
 | 0       |
 +---------*/
```

``` text
SELECT VAR_POP(x) AS results FROM UNNEST([NULL]) AS x

/*---------+
 | results |
 +---------+
 | NULL    |
 +---------*/
```

``` text
SELECT VAR_POP(x) AS results FROM UNNEST([10, 14, CAST('Infinity' as FLOAT64)]) AS x

/*---------+
 | results |
 +---------+
 | NaN     |
 +---------*/
```

## `     VAR_SAMP    `

``` text
VAR_SAMP(
  [ DISTINCT ]
  expression
)
[ OVER over_clause ]

over_clause:
  { named_window | ( [ window_specification ] ) }

window_specification:
  [ named_window ]
  [ PARTITION BY partition_expression [, ...] ]
  [ ORDER BY expression [ { ASC | DESC }  ] [, ...] ]
  [ window_frame_clause ]
```

**Description**

Returns the sample (unbiased) variance of the values. The return result is between `  0  ` and `  +Inf  ` .

All numeric types are supported. If the input is `  NUMERIC  ` or `  BIGNUMERIC  ` then the internal aggregation is stable with the final output converted to a `  FLOAT64  ` . Otherwise the input is converted to a `  FLOAT64  ` before aggregation, resulting in a potentially unstable result.

This function ignores any `  NULL  ` inputs. If there are fewer than two non- `  NULL  ` inputs, this function returns `  NULL  ` .

`  NaN  ` is produced if:

  - Any input value is `  NaN  `
  - Any input value is positive infinity or negative infinity.

To learn more about the optional aggregate clauses that you can pass into this function, see [Aggregate function calls](/bigquery/docs/reference/standard-sql/aggregate-function-calls) .

This function can be used with the [`  AGGREGATION_THRESHOLD  ` clause](/bigquery/docs/reference/standard-sql/query-syntax#agg_threshold_clause) .

If this function is used with the `  OVER  ` clause, it's part of a window function call. In a window function call, aggregate function clauses can't be used. To learn more about the `  OVER  ` clause and how to use it, see [Window function calls](/bigquery/docs/reference/standard-sql/window-function-calls) .

**Return Data Type**

`  FLOAT64  `

**Examples**

``` text
SELECT VAR_SAMP(x) AS results FROM UNNEST([10, 14, 18]) AS x

/*---------+
 | results |
 +---------+
 | 16      |
 +---------*/
```

``` text
SELECT VAR_SAMP(x) AS results FROM UNNEST([10, 14, NULL]) AS x

/*---------+
 | results |
 +---------+
 | 8       |
 +---------*/
```

``` text
SELECT VAR_SAMP(x) AS results FROM UNNEST([10, NULL]) AS x

/*---------+
 | results |
 +---------+
 | NULL    |
 +---------*/
```

``` text
SELECT VAR_SAMP(x) AS results FROM UNNEST([NULL]) AS x

/*---------+
 | results |
 +---------+
 | NULL    |
 +---------*/
```

``` text
SELECT VAR_SAMP(x) AS results FROM UNNEST([10, 14, CAST('Infinity' as FLOAT64)]) AS x

/*---------+
 | results |
 +---------+
 | NaN     |
 +---------*/
```

## `     VARIANCE    `

``` text
VARIANCE(
  [ DISTINCT ]
  expression
)
[ OVER over_clause ]

over_clause:
  { named_window | ( [ window_specification ] ) }

window_specification:
  [ named_window ]
  [ PARTITION BY partition_expression [, ...] ]
  [ ORDER BY expression [ { ASC | DESC }  ] [, ...] ]
  [ window_frame_clause ]
```

**Description**

An alias of [VAR\_SAMP](#var_samp) .
