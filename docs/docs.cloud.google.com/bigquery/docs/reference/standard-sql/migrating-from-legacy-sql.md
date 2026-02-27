# Migrating to GoogleSQL

BigQuery supports two SQL dialects: [GoogleSQL](/bigquery/docs/introduction-sql) and [legacy SQL](/bigquery/docs/reference/legacy-sql) . This document explains the differences between the two dialects, including [syntax](#syntax_differences) , [functions](#function_comparison) , and [semantics](#semantic_differences) , and gives examples of some of the [highlights of GoogleSQL](#standard_sql_highlights) .

## Comparison of legacy and GoogleSQL

When initially released, BigQuery ran queries using a non-GoogleSQL dialect known as [BigQuery SQL](/bigquery/docs/reference/legacy-sql) . With the launch of BigQuery 2.0, BigQuery released support for [GoogleSQL](/bigquery/docs/introduction-sql) , and renamed BigQuery SQL to legacy SQL. GoogleSQL is the preferred SQL dialect for querying data stored in BigQuery.

### Do I have to migrate to GoogleSQL?

We recommend migrating from legacy SQL to GoogleSQL, but it's not required for existing queries that use legacy SQL in some cases. For more information, see [Legacy SQL feature availability](/bigquery/docs/legacy-sql-feature-availability) .

### Enabling GoogleSQL

You have a choice of whether to use legacy or GoogleSQL when you run a query. For information about switching between SQL dialects, see [BigQuery SQL dialects](/bigquery/docs/introduction-sql#bigquery-sql-dialects) .

### Advantages of GoogleSQL

GoogleSQL complies with the SQL 2011 standard, and has extensions that support querying nested and repeated data. It has several advantages over legacy SQL, including:

  - Composability using [`  WITH  ` clauses](#composability_using_with_clauses) and [SQL functions](#composability_using_sql_functions)
  - [Subqueries in the `  SELECT  ` list and `  WHERE  ` clause](#subqueries_in_more_places)
  - [Correlated subqueries](#correlated_subqueries)
  - [`  ARRAY  ` and `  STRUCT  ` data types](#arrays_and_structs)
  - [Inserts, updates, and deletes](/bigquery/docs/data-manipulation-language)
  - `  COUNT(DISTINCT <expr>)  ` is exact and scalable, providing the accuracy of `  EXACT_COUNT_DISTINCT  ` without its limitations
  - Automatic predicate push-down through `  JOIN  ` s
  - Complex `  JOIN  ` predicates, including arbitrary expressions

For examples that demonstrate some of these features, see [GoogleSQL highlights](#standard_sql_highlights) .

## GoogleSQL highlights

This section discusses some of the highlights of GoogleSQL compared to legacy SQL.

### Composability using `     WITH    ` clauses

Some of the GoogleSQL examples on this page make use of a [`  WITH  ` clause](/bigquery/docs/reference/standard-sql/query-syntax#with_clause) , which enables extraction or reuse of named subqueries. For example:

``` text
#standardSQL
WITH T AS (
  SELECT x FROM UNNEST([1, 2, 3, 4]) AS x
)
SELECT x / (SELECT SUM(x) FROM T) AS weighted_x
FROM T;
```

This query defines a named subquery `  T  ` that contains `  x  ` values of 1, 2, 3, and 4. It selects `  x  ` values from `  T  ` and divides them by the sum of all `  x  ` values in `  T  ` . This query is equivalent to a query where the contents of `  T  ` are inline:

``` text
#standardSQL
SELECT
  x / (SELECT SUM(x)
       FROM (SELECT x FROM UNNEST([1, 2, 3, 4]) AS x)) AS weighted_x
FROM (SELECT x FROM UNNEST([1, 2, 3, 4]) AS x);
```

As another example, consider this query, which uses multiple named subqueries:

``` text
#standardSQL
WITH T AS (
  SELECT x FROM UNNEST([1, 2, 3, 4]) AS x
),
TPlusOne AS (
  SELECT x + 1 AS y
  FROM T
),
TPlusOneTimesTwo AS (
  SELECT y * 2 AS z
  FROM TPlusOne
)
SELECT z
FROM TPlusOneTimesTwo;
```

This query defines a sequence of transformations of the original data, followed by a `  SELECT  ` statement over `  TPlusOneTimesTwo  ` . This query is equivalent to the following query, which inlines the computations:

``` text
#standardSQL
SELECT (x + 1) * 2 AS z
FROM (SELECT x FROM UNNEST([1, 2, 3, 4]) AS x);
```

For more information, see [`  WITH  ` clause](/bigquery/docs/reference/standard-sql/query-syntax#with_clause) .

### Composability using SQL functions

GoogleSQL supports [user-defined SQL functions](/bigquery/docs/user-defined-functions#sql-udf-structure) . You can use user-defined SQL functions to define common expressions and then reference them from the query. For example:

``` text
#standardSQL
-- Computes the harmonic mean of the elements in 'arr'.
-- The harmonic mean of x_1, x_2, ..., x_n can be expressed as:
--   n / ((1 / x_1) + (1 / x_2) + ... + (1 / x_n))
CREATE TEMPORARY FUNCTION HarmonicMean(arr ARRAY<FLOAT64>) AS
(
  ARRAY_LENGTH(arr) / (SELECT SUM(1 / x) FROM UNNEST(arr) AS x)
);

WITH T AS (
  SELECT GENERATE_ARRAY(1.0, x * 4, x) AS arr
  FROM UNNEST([1, 2, 3, 4, 5]) AS x
)
SELECT arr, HarmonicMean(arr) AS h_mean
FROM T;
```

This query defines a SQL function named `  HarmonicMean  ` and then applies it to the array column `  arr  ` from `  T  ` .

### Subqueries in more places

GoogleSQL supports subqueries in the `  SELECT  ` list, `  WHERE  ` clause, and anywhere else in the query that expects an expression. For example, consider the following GoogleSQL query that computes the fraction of warm days in Seattle in 2015:

``` text
#standardSQL
WITH SeattleWeather AS (
  SELECT *
  FROM `bigquery-public-data.noaa_gsod.gsod2015`
  WHERE stn = '994014'
)
SELECT
  COUNTIF(max >= 70) /
    (SELECT COUNT(*) FROM SeattleWeather) AS warm_days_fraction
FROM SeattleWeather;
```

The Seattle weather station has an ID of `  '994014'  ` . The query computes the number of warm days based on those where the temperature reached 70 degrees Fahrenheit, or approximately 21 degrees Celsius, divided by the total number of recorded days for that station in 2015.

### Correlated subqueries

In GoogleSQL, subqueries can reference correlated columns; that is, columns that originate from the outer query. For example, consider the following GoogleSQL query:

``` text
#standardSQL
WITH WashingtonStations AS (
  SELECT weather.stn AS station_id, ANY_VALUE(station.name) AS name
  FROM `bigquery-public-data.noaa_gsod.stations` AS station
  INNER JOIN `bigquery-public-data.noaa_gsod.gsod2015` AS weather
  ON station.usaf = weather.stn
  WHERE station.state = 'WA' AND station.usaf != '999999'
  GROUP BY station_id
)
SELECT washington_stations.name,
  (SELECT COUNT(*)
   FROM `bigquery-public-data.noaa_gsod.gsod2015` AS weather
   WHERE washington_stations.station_id = weather.stn
   AND max >= 70) AS warm_days
FROM WashingtonStations AS washington_stations
ORDER BY warm_days DESC;
```

This query computes the names of weather stations in Washington state and the number of days in 2015 that the temperature reached 70 degrees Fahrenheit, or approximately 21 degrees Celsius. Notice that there is a subquery in the `  SELECT  ` list, and that the subquery references `  washington_stations.station_id  ` from the outer scope, namely `  FROM WashingtonStations AS washington_stations  ` .

### Arrays and structs

`  ARRAY  ` and `  STRUCT  ` are powerful concepts in GoogleSQL. As an example that uses both, consider the following query, which computes the top two articles for each day in the HackerNews dataset:

``` text
#standardSQL
WITH TitlesAndScores AS (
  SELECT
    ARRAY_AGG(STRUCT(title, score)) AS titles,
    EXTRACT(DATE FROM time_ts) AS date
  FROM `bigquery-public-data.hacker_news.stories`
  WHERE score IS NOT NULL AND title IS NOT NULL
  GROUP BY date)
SELECT date,
  ARRAY(SELECT AS STRUCT title, score
        FROM UNNEST(titles)
        ORDER BY score DESC
        LIMIT 2)
  AS top_articles
FROM TitlesAndScores
ORDER BY date DESC;
```

The `  WITH  ` clause defines `  TitlesAndScores  ` , which contains two columns. The first is an array of structs, where one field is an article title and the second is a score. The `  ARRAY_AGG  ` expression returns an array of these structs for each day.

The `  SELECT  ` statement following the `  WITH  ` clause uses an `  ARRAY  ` subquery to sort and return the top two articles within each array in accordance with the `  score  ` , then returns the results in descending order by date.

For more information about arrays and `  ARRAY  ` subqueries, see [Working with arrays](/bigquery/docs/arrays) . See also the references for [arrays](/bigquery/docs/reference/standard-sql/data-types#array_type) and [structs](/bigquery/docs/reference/standard-sql/data-types#struct_type) .

## Data type differences

Legacy SQL types have an equivalent in GoogleSQL. In some cases, the type has a different name. The following table lists each legacy SQL data type and its GoogleSQL equivalent.

<table>
<thead>
<tr class="header">
<th>Legacy SQL</th>
<th>GoogleSQL</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       BOOLEAN      </code></td>
<td><code dir="ltr" translate="no">       BOOLEAN      </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       FLOAT      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td>Legacy SQL has limited support for <code dir="ltr" translate="no">       NUMERIC      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
<td>Legacy SQL has limited support for <code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       BYTES      </code></td>
<td><code dir="ltr" translate="no">       BYTES      </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       RECORD      </code></td>
<td><code dir="ltr" translate="no">       STRUCT      </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       REPEATED      </code></td>
<td><code dir="ltr" translate="no">       ARRAY      </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>See <a href="#timestamp_type_differences"><code dir="ltr" translate="no">        TIMESTAMP       </code> differences</a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       DATE      </code></td>
<td><code dir="ltr" translate="no">       DATE      </code></td>
<td>Legacy SQL has limited support for <code dir="ltr" translate="no">       DATE      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       TIME      </code></td>
<td><code dir="ltr" translate="no">       TIME      </code></td>
<td>Legacy SQL has limited support for <code dir="ltr" translate="no">       TIME      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       DATETIME      </code></td>
<td><code dir="ltr" translate="no">       DATETIME      </code></td>
<td>Legacy SQL has limited support for <code dir="ltr" translate="no">       DATETIME      </code></td>
</tr>
</tbody>
</table>

For more information see:

  - [GoogleSQL data types reference](/bigquery/docs/reference/standard-sql/data-types)
  - [Legacy SQL data types reference](/bigquery/docs/data-types)

### `     TIMESTAMP    ` type differences

GoogleSQL has a [stricter range of valid `  TIMESTAMP  ` values](/bigquery/docs/reference/standard-sql/data-types#timestamp_type) than legacy SQL does. In GoogleSQL, valid `  TIMESTAMP  ` values are in the range of `  0001-01-01 00:00:00.000000  ` to `  9999-12-31 23:59:59.999999  ` . For example, you can select the minimum and maximum `  TIMESTAMP  ` values using GoogleSQL:

``` text
#standardSQL
SELECT
  min_timestamp,
  max_timestamp,
  UNIX_MICROS(min_timestamp) AS min_unix_micros,
  UNIX_MICROS(max_timestamp) AS max_unix_micros
FROM (
  SELECT
    TIMESTAMP '0001-01-01 00:00:00.000000' AS min_timestamp,
    TIMESTAMP '9999-12-31 23:59:59.999999' AS max_timestamp
);
```

This query returns `  -62135596800000000  ` as `  min_unix_micros  ` and `  253402300799999999  ` as `  max_unix_micros  ` .

If you select a column that contains timestamp values outside of this range, you receive an error:

``` text
#standardSQL
SELECT timestamp_column_with_invalid_values
FROM MyTableWithInvalidTimestamps;
```

This query returns the following error:

``` text
Cannot return an invalid timestamp value of -8446744073709551617
microseconds relative to the Unix epoch. The range of valid
timestamp values is [0001-01-1 00:00:00, 9999-12-31 23:59:59.999999]
```

To correct the error, one option is to define and use a [user-defined function](/bigquery/docs/user-defined-functions) to filter the invalid timestamps:

``` text
#standardSQL
CREATE TEMP FUNCTION TimestampIsValid(t TIMESTAMP) AS (
  t >= TIMESTAMP('0001-01-01 00:00:00') AND
  t <= TIMESTAMP('9999-12-31 23:59:59.999999')
);

SELECT timestamp_column_with_invalid_values
FROM MyTableWithInvalidTimestamps
WHERE TimestampIsValid(timestamp_column_with_invalid_values);
```

Another option to correct the error is to use the [`  SAFE_CAST  `](/bigquery/docs/reference/standard-sql/conversion_functions#safe_casting) function with the timestamp column. For example:

``` text
#standardSQL
SELECT SAFE_CAST(timestamp_column_with_invalid_values AS STRING) AS timestamp_string
FROM MyTableWithInvalidTimestamps;
```

This query returns `  NULL  ` rather than a timestamp string for invalid timestamp values.

### Automatic data type coercions

Both legacy and GoogleSQL support coercions (automatic conversions) between certain data types. For example, BigQuery coerces a value of type `  INT64  ` to `  FLOAT64  ` if the query passes it to a function that requires `  FLOAT64  ` as input.

The following legacy SQL coercions are not supported in GoogleSQL and need to be explicitly cast to the correct type:

<table>
<thead>
<tr class="header">
<th>Coercion</th>
<th>Translation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       BOOLEAN      </code> to <code dir="ltr" translate="no">       INT64      </code> or <code dir="ltr" translate="no">       FLOAT64      </code></td>
<td>Use <code dir="ltr" translate="no">       SAFE_CAST(bool AS INT64)      </code> or <code dir="ltr" translate="no">       SAFE_CAST(bool AS FLOAT64)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       INT64      </code> to <code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>Use <code dir="ltr" translate="no">       TIMESTAMP_MICROS(micros_value)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       STRING      </code> to <code dir="ltr" translate="no">       BYTES      </code></td>
<td>Use <code dir="ltr" translate="no">       SAFE_CAST(str AS BYTES)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       STRING      </code> to <code dir="ltr" translate="no">       INT64      </code> , <code dir="ltr" translate="no">       FLOAT64      </code> , or <code dir="ltr" translate="no">       BOOL      </code></td>
<td>Mostly supported by GoogleSQL. For corner cases use <code dir="ltr" translate="no">       SAFE_CAST(str AS INT64)      </code> , <code dir="ltr" translate="no">       SAFE_CAST(str AS FLOAT64)      </code> , or <code dir="ltr" translate="no">       SAFE_CAST(str AS BOOL)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       STRING      </code> to <code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>Mostly supported by GoogleSQL. For corner cases use <code dir="ltr" translate="no">       TIMESTAMP(str)      </code> or <code dir="ltr" translate="no">       SAFE_CAST(str AS TIMESTAMP)      </code></td>
</tr>
</tbody>
</table>

For example, the following legacy SQL query uses implicit coercions:

``` text
#legacySQL
SELECT
  1 + true as boolean_int_coercion,
  TIMESTAMP(1234567890) as integer_timestamp_coercion;
```

In GoogleSQL, this query is invalid. To achieve the same result, you must use explicit casting:

``` text
#standardSQL
SELECT
  1 + SAFE_CAST(true AS INT64) as boolean_coercion,
  TIMESTAMP_MICROS(1234567890) as integer_timestamp_coercion;
```

## Syntax differences

While GoogleSQL and legacy SQL syntaxes are similar, there are some crucial differences.

### Escaping reserved keywords and invalid identifiers

In legacy SQL, you escape reserved keywords and identifiers that contain invalid characters such as a space `  ` or hyphen `  -  ` using square brackets `  []  ` . In GoogleSQL, you escape such keywords and identifiers using backticks ``  `  `` . For example:

``` text
#standardSQL
SELECT
  word,
  SUM(word_count) AS word_count
FROM
  `bigquery-public-data.samples.shakespeare`
WHERE word IN ('me', 'I', 'you')
GROUP BY word;
```

Legacy SQL allows reserved keywords in some places that GoogleSQL does not. For example, the following query fails due to a `  Syntax error  ` using standard SQL:

``` text
#standardSQL
SELECT
  COUNT(*) AS rows
FROM
  `bigquery-public-data.samples.shakespeare`;
```

To fix the error, escape the alias `  rows  ` using backticks:

``` text
#standardSQL
SELECT
  COUNT(*) AS `rows`
FROM
  `bigquery-public-data.samples.shakespeare`;
```

The following is a list of keywords allowed in legacy SQL, but not in GoogleSQL:

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<td><ul>
<li><code dir="ltr" translate="no">         ALL        </code></li>
<li><code dir="ltr" translate="no">         AND        </code></li>
<li><code dir="ltr" translate="no">         ANY        </code></li>
<li><code dir="ltr" translate="no">         ARRAY        </code></li>
<li><code dir="ltr" translate="no">         ASSERT_ROWS_MODIFIED        </code></li>
<li><code dir="ltr" translate="no">         AT        </code></li>
<li><code dir="ltr" translate="no">         COLLATE        </code></li>
<li><code dir="ltr" translate="no">         CURRENT        </code></li>
<li><code dir="ltr" translate="no">         DEFAULT        </code></li>
<li><code dir="ltr" translate="no">         DESC        </code></li>
<li><code dir="ltr" translate="no">         END        </code></li>
<li><code dir="ltr" translate="no">         ENUM        </code></li>
</ul></td>
<td><ul>
<li><code dir="ltr" translate="no">         ESCAPE        </code></li>
<li><code dir="ltr" translate="no">         EXCEPT        </code></li>
<li><code dir="ltr" translate="no">         EXCLUDE        </code></li>
<li><code dir="ltr" translate="no">         EXTRACT        </code></li>
<li><code dir="ltr" translate="no">         FETCH        </code></li>
<li><code dir="ltr" translate="no">         FOR        </code></li>
<li><code dir="ltr" translate="no">         GROUP        </code></li>
<li><code dir="ltr" translate="no">         GROUPING        </code></li>
<li><code dir="ltr" translate="no">         GROUPS        </code></li>
<li><code dir="ltr" translate="no">         IF        </code></li>
<li><code dir="ltr" translate="no">         INTERVAL        </code></li>
<li><code dir="ltr" translate="no">         IS        </code></li>
</ul></td>
<td><ul>
<li><code dir="ltr" translate="no">         LATERAL        </code></li>
<li><code dir="ltr" translate="no">         NATURAL        </code></li>
<li><code dir="ltr" translate="no">         NEW        </code></li>
<li><code dir="ltr" translate="no">         NO        </code></li>
<li><code dir="ltr" translate="no">         NULLS        </code></li>
<li><code dir="ltr" translate="no">         OF        </code></li>
<li><code dir="ltr" translate="no">         ORDER        </code></li>
<li><code dir="ltr" translate="no">         PROTO        </code></li>
<li><code dir="ltr" translate="no">         QUALIFY        </code></li>
<li><code dir="ltr" translate="no">         RANGE        </code></li>
<li><code dir="ltr" translate="no">         RECURSIVE        </code></li>
</ul></td>
<td><ul>
<li><code dir="ltr" translate="no">         RESPECT        </code></li>
<li><code dir="ltr" translate="no">         ROLLUP        </code></li>
<li><code dir="ltr" translate="no">         ROWS        </code></li>
<li><code dir="ltr" translate="no">         SOME        </code></li>
<li><code dir="ltr" translate="no">         STRUCT        </code></li>
<li><code dir="ltr" translate="no">         TABLESAMPLE        </code></li>
<li><code dir="ltr" translate="no">         TO        </code></li>
<li><code dir="ltr" translate="no">         TREAT        </code></li>
<li><code dir="ltr" translate="no">         UNNEST        </code></li>
<li><code dir="ltr" translate="no">         WHEN        </code></li>
<li><code dir="ltr" translate="no">         WINDOW        </code></li>
</ul></td>
</tr>
</tbody>
</table>

For a more comprehensive list of reserved keywords and what constitutes valid identifiers, see the [Reserved keywords](/bigquery/docs/reference/standard-sql/lexical#reserved_keywords) section in [Lexical structure](/bigquery/docs/reference/standard-sql/lexical) .

### Project-qualified table names

In legacy SQL, to query a table with a project-qualified name, you can use either a colon `  :  ` or a period `  .  ` . In GoogleSQL however, you must use only periods `  .  ` .

Example legacy SQL query:

``` text
#legacySQL
SELECT
  word
FROM
  [bigquery-public-data:samples.shakespeare]
LIMIT 1;
```

The GoogleSQL equivalent is:

``` text
#standardSQL
SELECT
  word
FROM
  `bigquery-public-data.samples.shakespeare`
LIMIT 1;
```

If your project name includes a domain, such as `  example.com:myproject  ` , you use `  example.com:myproject  ` as the project name, including the `  :  ` .

### Table decorators

[Table decorators](/bigquery/docs/table-decorators) are used to run a query on a subset of data.

#### Time decorator (snapshot decorator)

You can achieve the semantics of time decorators (formerly known as *snapshot decorators* ) by using the [`  FOR SYSTEM_TIME AS OF  `](/bigquery/docs/reference/standard-sql/query-syntax#for_system_time_as_of) clause, which references the historical version of a table at a specified timestamp. For more information, see [Accessing historical data using time travel](/bigquery/docs/time-travel) .

#### Range decorator

There is no exact equivalent to range decorators in GoogleSQL. You can achieve similar semantics by creating a time-partitioned table and using a partition filter when querying data. For more information, see [Querying partitioned tables](/bigquery/docs/querying-partitioned-tables) .

Another option is to create date-sharded tables and filter on the `  _TABLE_SUFFIX  ` pseudocolumn. For more information, see [GoogleSQL wildcard tables](/bigquery/docs/querying-wildcard-tables#wildcard_table_syntax) .

#### Partition decorator

The equivalent of a partition decorator in GoogleSQL is a filter on the partitioning column. For more information, see [Querying partitioned tables](/bigquery/docs/querying-partitioned-tables) .

For example, consider a legacy SQL query using a `  table  ` partitioned over the `  _PARTITIONTIME  ` pseudocolumn:

``` text
#legacySQL
SELECT * FROM dataset.table$20160501;
```

The GoogleSQL equivalent is:

``` text
#standardSQL
SELECT * FROM dataset.table
WHERE _PARTITIONTIME=TIMESTAMP('2016-05-01');
```

Another option is to filter on the `  _TABLE_SUFFIX  ` pseudocolumn. For more information, see [GoogleSQL wildcard tables](/bigquery/docs/querying-wildcard-tables#wildcard_table_syntax) .

### Table wildcard functions

In legacy SQL, you can use the following [table wildcard functions](/bigquery/docs/reference/legacy-sql#tablewildcardfunctions) to query multiple tables.

  - `  TABLE_DATE_RANGE  `
  - `  TABLE_DATE_RANGE_STRICT  `
  - `  TABLE_QUERY  `

These functions are not supported in GoogleSQL, but they can be migrated using a filter on `  _TABLE_SUFFIX  ` pseudocolumn.

For example, consider the following legacy SQL query, which counts the number of rows across 2010 and 2011 in the National Oceanic and Atmospheric Administration GSOD (global summary of the day) tables:

``` text
#legacySQL
SELECT COUNT(*)
FROM TABLE_QUERY([bigquery-public-data:noaa_gsod],
                 'table_id IN ("gsod2010", "gsod2011")');
```

An equivalent query using GoogleSQL is:

``` text
#standardSQL
SELECT COUNT(*)
FROM `bigquery-public-data.noaa_gsod.*`
WHERE _TABLE_SUFFIX IN ("gsod2010", "gsod2011");
```

For more information, including examples of all wildcard functions, see [Migrating table wildcard functions](#migrating_table_wildcard_functions) .

### Comma operator with tables

In legacy SQL, the comma operator `  ,  ` has the non-standard meaning of [`  UNION ALL BY NAME  `](/bigquery/docs/reference/standard-sql/query-syntax#set_operators) when applied to tables. In GoogleSQL, the comma operator has the standard meaning of `  JOIN  ` .

For example, consider the following legacy SQL query:

``` text
#legacySQL
SELECT
  x,
  y
FROM
  (SELECT 1 AS x, "foo" AS y),
  (SELECT 2 AS x, "bar" AS y);
```

This is equivalent to the GoogleSQL query:

``` text
#standardSQL
SELECT
  x,
  y
FROM
  (SELECT 1 AS x, "foo" AS y UNION ALL BY NAME
   SELECT 2 AS x, "bar" AS y);
```

Legacy SQL associates columns by name instead of by position. To get the same behavior in GoogleSQL, use `  UNION ALL BY NAME  ` . For example, the following query shows a translation where the column names and order are swapped:

``` text
#legacySQL
SELECT * FROM (SELECT 1 AS A, 2 as B), (SELECT 3 AS B, 4 as A);
```

The GoogleSQL equivalent will look like:

``` text
#standardSQL
SELECT * FROM (SELECT 1 AS A, 2 as B) UNION ALL BY NAME (SELECT 3 AS B, 4 as A);
```

Where the result in both cases will be:

``` text
+---+---+
| A | B |
+---+---+
| 1 | 2 |
| 4 | 3 |
+---+---+
```

### Logical views

You cannot query a logical view defined with legacy SQL using GoogleSQL, and conversely, you cannot query a logical view defined with GoogleSQL using legacy SQL due to differences in syntax and semantics between the dialects. Instead, you would need to create a new view that uses GoogleSQL -- possibly under a different name -- to replace a view that uses legacy SQL.

As an example, suppose that view `  V  ` is defined using legacy SQL as:

``` text
#legacySQL
SELECT *, UTC_USEC_TO_DAY(timestamp_col) AS day
FROM MyTable;
```

Suppose that view `  W  ` is defined using legacy SQL as:

``` text
#legacySQL
SELECT user, action, day
FROM V;
```

Suppose that you execute the following legacy SQL query daily, but you want to migrate it to use GoogleSQL instead:

``` text
#legacySQL
SELECT EXACT_COUNT_DISTINCT(user), action, day
FROM W
GROUP BY action, day;
```

One possible migration path is to create new views using different names. The steps involved are:

Create a view named `  V2  ` using GoogleSQL with the following contents:

``` text
#standardSQL
SELECT *, EXTRACT(DAY FROM timestamp_col) AS day
FROM MyTable;
```

Create a view named `  W2  ` using GoogleSQL with the following contents:

``` text
#standardSQL
SELECT user, action, day
FROM V2;
```

Change your query that executes daily to use GoogleSQL and refer to `  W2  ` instead:

``` text
#standardSQL
SELECT COUNT(DISTINCT user), action, day
FROM W2
GROUP BY action, day;
```

Another option is to delete views `  V  ` and `  W  ` , then recreate them using standard SQL under the same names. With this option, you would need to migrate all of your queries that reference `  V  ` or `  W  ` to use GoogleSQL at the same time, however.

## Function comparison

The following is a partial list of legacy SQL functions and their GoogleSQL equivalents.

<table>
<thead>
<tr class="header">
<th>Legacy SQL</th>
<th>GoogleSQL</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       INTEGER(x)      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/conversion_functions#safe_casting"><code dir="ltr" translate="no">        SAFE_CAST(x AS INT64)       </code></a></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       CAST(x AS INTEGER)      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/conversion_functions#safe_casting"><code dir="ltr" translate="no">        SAFE_CAST(x AS INT64)       </code></a></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       DATEDIFF(t1, t2)      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/date_functions#date_diff"><code dir="ltr" translate="no">        DATE_DIFF(DATE(t1), DATE(t2), DAY)       </code></a></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       NOW()      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#current_timestamp"><code dir="ltr" translate="no">        UNIX_MICROS(CURRENT_TIMESTAMP())       </code></a></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       STRFTIME_UTC_USEC(ts_usec, fmt)      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#format_timestamp"><code dir="ltr" translate="no">        FORMAT_TIMESTAMP(fmt, TIMESTAMP_MICROS(ts_usec))       </code></a></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       UTC_USEC_TO_DAY(ts_usec)      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#timestamp_trunc"><code dir="ltr" translate="no">        UNIX_MICROS(TIMESTAMP_TRUNC(TIMESTAMP_MICROS(ts_usec), DAY))       </code></a></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       UTC_USEC_TO_WEEK(ts_usec, day_of_week)      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#timestamp_trunc"><code dir="ltr" translate="no">        UNIX_MICROS(TIMESTAMP_ADD(TIMESTAMP_TRUNC(TIMESTAMP_MICROS(ts_usec), WEEK),INTERVAL day_of_week DAY))       </code></a></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       REGEXP_MATCH(s, pattern)      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#regexp_contains"><code dir="ltr" translate="no">        REGEXP_CONTAINS(s, pattern)       </code></a></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       IS_NULL(x)      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/operators#is_operators"><code dir="ltr" translate="no">        x IS NULL       </code></a></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       LEFT(s, len)      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#substr"><code dir="ltr" translate="no">        SUBSTR(s, 0, len)       </code></a></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       RIGHT(s, len)      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#substr"><code dir="ltr" translate="no">        SUBSTR(s, -len)       </code></a></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       s CONTAINS "foo"      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#strpos"><code dir="ltr" translate="no">        STRPOS(s, "foo") &gt; 0       </code></a> or <a href="/bigquery/docs/reference/standard-sql/operators#comparison_operators"><code dir="ltr" translate="no">        s LIKE '%foo%'       </code></a></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       INSTR(s, "foo")      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#strpos"><code dir="ltr" translate="no">        STRPOS(s, "foo")       </code></a></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       x % y      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#mod"><code dir="ltr" translate="no">        MOD(x, y)       </code></a></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       NEST(x)      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#array_agg"><code dir="ltr" translate="no">        ARRAY_AGG(x)       </code></a></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       GROUP_CONCAT_UNQUOTED(s, sep)      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#string_agg"><code dir="ltr" translate="no">        STRING_AGG(s, sep)       </code></a></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       SOME(x)      </code></td>
<td><code dir="ltr" translate="no">       IFNULL(      </code> <a href="/bigquery/docs/reference/standard-sql/operators#logical_operators"><code dir="ltr" translate="no">        LOGICAL_OR(x)       </code></a> <code dir="ltr" translate="no">       , false)      </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       EVERY(x)      </code></td>
<td><code dir="ltr" translate="no">       IFNULL(      </code> <a href="/bigquery/docs/reference/standard-sql/operators#logical_operators"><code dir="ltr" translate="no">        LOGICAL_AND(x)       </code></a> <code dir="ltr" translate="no">       , true)      </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       COUNT(DISTINCT x)      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/approximate_aggregate_functions#approx_count_distinct"><code dir="ltr" translate="no">        APPROX_COUNT_DISTINCT(x)       </code></a></td>
<td>see <a href="#count_function_comparison">notes below</a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       EXACT_COUNT_DISTINCT(x)      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#count"><code dir="ltr" translate="no">        COUNT(DISTINCT x)       </code></a></td>
<td>see <a href="#count_function_comparison">notes below</a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       QUANTILES(x, boundaries)      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/approximate_aggregate_functions#approx_quantiles"><code dir="ltr" translate="no">        APPROX_QUANTILES(x, boundaries-1)       </code></a></td>
<td>output needs to be <a href="/bigquery/docs/reference/standard-sql/migrating-from-legacy-sql#removing_repetition_with_flatten">unnested</a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       TOP(x, num), COUNT(*)      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/approximate_aggregate_functions#approx_top_count"><code dir="ltr" translate="no">        APPROX_TOP_COUNT(x, num)       </code></a></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       NTH(index, arr) WITHIN RECORD      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/operators#array_subscript_operator"><code dir="ltr" translate="no">        arr[SAFE_ORDINAL(index)]       </code></a></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       COUNT(arr) WITHIN RECORD      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/array_functions#array_length"><code dir="ltr" translate="no">        ARRAY_LENGTH(arr)       </code></a></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       HOST(url)      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/net_functions#nethost"><code dir="ltr" translate="no">        NET.HOST(url)       </code></a></td>
<td>see <a href="#url_function_comparison">differences below</a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       TLD(url)      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/net_functions#netpublic_suffix"><code dir="ltr" translate="no">        NET.PUBLIC_SUFFIX(url)       </code></a></td>
<td>see <a href="#url_function_comparison">differences below</a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       DOMAIN(url)      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/net_functions#netreg_domain"><code dir="ltr" translate="no">        NET.REG_DOMAIN(url)       </code></a></td>
<td>see <a href="#url_function_comparison">differences below</a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       PARSE_IP(addr_string)      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/net_functions#netipv4_to_int64"><code dir="ltr" translate="no">        NET.IPV4_TO_INT64       </code></a> <code dir="ltr" translate="no">       (      </code> <a href="/bigquery/docs/reference/standard-sql/net_functions#netip_from_string"><code dir="ltr" translate="no">        NET.IP_FROM_STRING       </code></a> <code dir="ltr" translate="no">       (addr_string))      </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       FORMAT_IP(addr_int64)      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/net_functions#netip_to_string"><code dir="ltr" translate="no">        NET.IP_TO_STRING       </code></a> <code dir="ltr" translate="no">       (      </code> <a href="/bigquery/docs/reference/standard-sql/net_functions#netipv4_from_int64"><code dir="ltr" translate="no">        NET.IPV4_FROM_INT64       </code></a> <code dir="ltr" translate="no">       (addr_int64 &amp; 0xFFFFFFFF))      </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       PARSE_PACKED_IP(addr_string)      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/net_functions#netip_from_string"><code dir="ltr" translate="no">        NET.IP_FROM_STRING(addr_string)       </code></a></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       FORMAT_PACKED_IP(addr_bytes)      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/net_functions#netip_to_string"><code dir="ltr" translate="no">        NET.IP_TO_STRING(addr_bytes)       </code></a></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       NVL(expr, null_default)      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/conditional_expressions#ifnull"><code dir="ltr" translate="no">        IFNULL(expr, null_default)       </code></a></td>
<td></td>
</tr>
</tbody>
</table>

For more information about GoogleSQL functions, see [All functions](/bigquery/docs/reference/standard-sql/functions-all) .

### `     COUNT    ` function comparison

Both legacy SQL and GoogleSQL contain a COUNT function. However, each function behaves differently, depending on the SQL dialect you use.

In legacy SQL, `  COUNT(DISTINCT x)  ` returns an approximate count. In standard SQL, it returns an exact count. For an approximate count of distinct values that runs faster and requires fewer resources, use [`  APPROX_COUNT_DISTINCT  `](/bigquery/docs/reference/standard-sql/approximate_aggregate_functions#approx_count_distinct) .

### URL function comparison

Both legacy SQL and GoogleSQL contain functions for parsing URLs. In legacy SQL, these functions are `  HOST(url)  ` , `  TLD(url)  ` , and `  DOMAIN(url)  ` . In standard SQL, these functions are [`  NET.HOST(url)  `](/bigquery/docs/reference/standard-sql/net_functions#nethost) , [`  NET.PUBLIC_SUFFIX(url)  `](/bigquery/docs/reference/standard-sql/net_functions#netpublic_suffix) , and [`  NET.REG_DOMAIN(url)  `](/bigquery/docs/reference/standard-sql/net_functions#netreg_domain) .

**Improvements in GoogleSQL functions**

  - GoogleSQL URL functions can parse URLs starting with "//".
  - When the input is not compliant with [RFC 3986](https://tools.ietf.org/html/rfc3986#appendix-A) or is not a URL (for example, "mailto:?to=\&subject=\&body="), different rules are applied to parse the input. In particular, GoogleSQL URL functions can parse non-standard inputs without "//", such as "www.google.com". For best results, it is recommended that you ensure that inputs are URLs and comply with RFC 3986.
  - `  NET.PUBLIC_SUFFIX  ` returns results without leading dots. For example, it returns "com" instead of ".com". This complies with the format in the [public suffix list](https://publicsuffix.org/list/public_suffix_list.dat) .
  - `  NET.PUBLIC_SUFFIX  ` and `  NET.REG_DOMAIN  ` support uppercase letters and internationalized domain names. `  TLD  ` and `  DOMAIN  ` don't support them (might return unexpected results).

**Minor differences on edge cases**

  - If the input does not contain any suffix in the [public suffix list](https://publicsuffix.org/list/public_suffix_list.dat) , `  NET.PUBLIC_SUFFIX  ` and `  NET.REG_DOMAIN  ` return NULL, while `  TLD  ` and `  DOMAIN  ` return non-NULL values as best effort guesses.
  - If the input contains only a public suffix without a preceding label (for example, "http://com"), `  NET.PUBLIC_SUFFIX  ` returns the public suffix, while `  TLD  ` returns an empty string. Similarly, `  NET.REG_DOMAIN  ` returns NULL, while `  DOMAIN  ` returns the public suffix.
  - For inputs with IPv6 hosts, `  NET.HOST  ` does not remove brackets from the result, as specified by [RFC 3986](https://tools.ietf.org/html/rfc3986#appendix-A) .
  - For inputs with IPv4 hosts, `  NET.REG_DOMAIN  ` returns NULL, while `  DOMAIN  ` returns the first 3 octets.

**Examples**

In the following table, gray text color indicates results that are the same between legacy and GoogleSQL.

<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>URL (description)</th>
<th>HOST</th>
<th>NET.HOST</th>
<th>TLD</th>
<th>NET.PUBLIC _SUFFIX</th>
<th>DOMAIN</th>
<th>NET.REG_DOMAIN</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>"//google.com"<br />
<span class="small">(starting with "//")</span></td>
<td>NULL</td>
<td>"google.com"</td>
<td>NULL</td>
<td>"com"</td>
<td>NULL</td>
<td>"google.com"</td>
</tr>
<tr class="even">
<td>"google.com"<br />
<span class="small">(non-standard; no "//")</span></td>
<td>NULL</td>
<td>"google.com"</td>
<td>NULL</td>
<td>"com"</td>
<td>NULL</td>
<td>"google.com"</td>
</tr>
<tr class="odd">
<td>"http://user:pass@word@x.com"<br />
<span class="small">(non-standard with multiple "@")</span></td>
<td>"word@x.com"</td>
<td>"x.com"</td>
<td>".com"</td>
<td>"com"</td>
<td>"word@x.com"</td>
<td>"x.com"</td>
</tr>
<tr class="even">
<td>" http: // foo.com:1:2"<br />
<span class="small">(non-standard with multiple ":")</span></td>
<td>"foo.com:1"</td>
<td>"foo.com"</td>
<td>".com:1"</td>
<td>"com"</td>
<td>"foo.com"</td>
<td>"foo.com"</td>
</tr>
<tr class="odd">
<td>"http://x.Co.uk"<br />
<span class="small">(upper case letters)</span></td>
<td>"x.Co.uk"</td>
<td>"x.Co.uk"</td>
<td>".uk"</td>
<td>"Co.uk"</td>
<td>"Co.uk"</td>
<td>"x.Co.uk"</td>
</tr>
<tr class="even">
<td>"http://a.b"<br />
<span class="small">(public suffix not found)</span></td>
<td>"a.b"</td>
<td>"a.b"</td>
<td>".b"</td>
<td>NULL</td>
<td>"a.b"</td>
<td>NULL</td>
</tr>
<tr class="odd">
<td>"http://com"<br />
<span class="small">(host contains only a public suffix)</span></td>
<td>"com"</td>
<td>"com"</td>
<td>""</td>
<td>"com"</td>
<td>"com"</td>
<td>NULL</td>
</tr>
<tr class="even">
<td>"http://[::1]"<br />
<span class="small">(IPv6 host; no public suffix)</span></td>
<td>"::1"</td>
<td>"[::1]"</td>
<td>""</td>
<td>NULL</td>
<td>"::1"</td>
<td>NULL</td>
</tr>
<tr class="odd">
<td>"http://1.2.3.4"<br />
<span class="small">(IPv4 host; no public suffix)</span></td>
<td>"1.2.3.4"</td>
<td>"1.2.3.4"</td>
<td>""</td>
<td>NULL</td>
<td>"1.2.3"</td>
<td>NULL</td>
</tr>
</tbody>
</table>

## Differences in repeated field handling

A `  REPEATED  ` type in legacy SQL is equivalent to an `  ARRAY  ` of that type in GoogleSQL. For example, `  REPEATED INTEGER  ` is equivalent to `  ARRAY<INT64>  ` in GoogleSQL. The following section discusses some of the differences in operations on repeated fields between legacy and GoogleSQL.

### `     NULL    ` elements and `     NULL    ` arrays

GoogleSQL supports `  NULL  ` array elements, but raises an error if there is a `  NULL  ` array element in the query result. If there is a `  NULL  ` array column in the query result, GoogleSQL stores it as an empty array.

### Selecting nested repeated leaf fields

Using legacy SQL, you can "dot" into a nested repeated field without needing to consider where the repetition occurs. In GoogleSQL, attempting to "dot" into a nested repeated field results in an error. For example:

``` text
#standardSQL
SELECT
  repository.url,
  payload.pages.page_name
FROM
  `bigquery-public-data.samples.github_nested`
LIMIT 5;
```

Attempting to execute this query returns:

``` text
Cannot access field page_name on a value with type
ARRAY<STRUCT<action STRING, html_url STRING, page_name STRING, ...>>
```

To correct the error and return an array of `  page_name  ` s in the result, use an `  ARRAY  ` subquery instead. For example:

``` text
#standardSQL
SELECT
  repository.url,
  ARRAY(SELECT page_name FROM UNNEST(payload.pages)) AS page_names
FROM
  `bigquery-public-data.samples.github_nested`
LIMIT 5;
```

For more information about arrays and `  ARRAY  ` subqueries, see [Working with arrays](/bigquery/docs/arrays) .

### Filtering repeated fields

Using legacy SQL, you can filter repeated fields directly using a `  WHERE  ` clause. In GoogleSQL, you can express similar logic with a `  JOIN  ` comma operator followed by a filter. For example, consider the following legacy SQL query:

``` text
#legacySQL
SELECT
  payload.pages.title
FROM
  [bigquery-public-data:samples.github_nested]
WHERE payload.pages.page_name IN ('db_jobskill', 'Profession');
```

This query returns all `  title  ` s of pages for which the `  page_name  ` is either `  db_jobskill  ` or `  Profession  ` . You can express a similar query in GoogleSQL as:

``` text
#standardSQL
SELECT
  page.title
FROM
  `bigquery-public-data.samples.github_nested`,
  UNNEST(payload.pages) AS page
WHERE page.page_name IN ('db_jobskill', 'Profession');
```

One difference between the preceding legacy SQL and GoogleSQL queries is that if you unset the **Flatten Results** option and execute the legacy SQL query, `  payload.pages.title  ` is `  REPEATED  ` in the query result. To achieve the same semantics in GoogleSQL and return an array for the `  title  ` column, use an `  ARRAY  ` subquery instead:

``` text
#standardSQL
SELECT
  title
FROM (
  SELECT
    ARRAY(SELECT title FROM UNNEST(payload.pages)
          WHERE page_name IN ('db_jobskill', 'Profession')) AS title
  FROM
    `bigquery-public-data.samples.github_nested`)
WHERE ARRAY_LENGTH(title) > 0;
```

This query creates an array of `  title  ` s where the `  page_name  ` is either `  'db_jobskill'  ` or `  'Profession'  ` , then filters any rows where the array did not match that condition using `  ARRAY_LENGTH(title) > 0  ` .

For more information about arrays, see [Working with arrays](/bigquery/docs/arrays) .

### Structure of selected nested leaf fields

Legacy SQL preserves the structure of nested leaf fields in the `  SELECT  ` list when the **Flatten Results** option is unset, whereas GoogleSQL does not. For example, consider the following legacy SQL query:

``` text
#legacySQL
SELECT
  repository.url,
  repository.has_downloads
FROM
  [bigquery-public-data.samples.github_nested]
LIMIT 5;
```

This query returns `  url  ` and `  has_downloads  ` within a record named `  repository  ` when **Flatten Results** is unset. Now consider the following GoogleSQL query:

``` text
#standardSQL
SELECT
  repository.url,
  repository.has_downloads
FROM
  `bigquery-public-data.samples.github_nested`
LIMIT 5;
```

This query returns `  url  ` and `  has_downloads  ` as top-level columns; they are not part of a `  repository  ` record or struct. To return them as part of a struct, use the `  STRUCT  ` operator:

``` text
#standardSQL
SELECT
  STRUCT(
    repository.url,
    repository.has_downloads) AS repository
FROM
  `bigquery-public-data.samples.github_nested`
LIMIT 5;
```

### Removing repetition with `     FLATTEN    `

GoogleSQL does not have a `  FLATTEN  ` function as in legacy SQL, but you can achieve similar semantics using the `  JOIN  ` (comma) operator. For example, consider the following legacy SQL query:

``` text
#legacySQL
SELECT
  repository.url,
  payload.pages.page_name
FROM
  FLATTEN([bigquery-public-data:samples.github_nested], payload.pages.page_name)
LIMIT 5;
```

You can express a similar query in GoogleSQL as follows:

``` text
#standardSQL
SELECT
  repository.url,
  page.page_name
FROM
  `bigquery-public-data.samples.github_nested`,
  UNNEST(payload.pages) AS page
LIMIT 5;
```

Or, equivalently, use `  JOIN  ` rather than the comma `  ,  ` operator:

``` text
#standardSQL
SELECT
  repository.url,
  page.page_name
FROM
  `bigquery-public-data.samples.github_nested`
JOIN
  UNNEST(payload.pages) AS page
LIMIT 5;
```

One important difference is that the legacy SQL query returns a row where `  payload.pages.page_name  ` is `  NULL  ` if `  payload.pages  ` is empty. The standard SQL query, however, does not return a row if `  payload.pages  ` is empty. To achieve exactly the same semantics, use a `  LEFT JOIN  ` or `  LEFT OUTER JOIN  ` . For example:

``` text
#standardSQL
SELECT
  repository.url,
  page.page_name
FROM
  `bigquery-public-data.samples.github_nested`
LEFT JOIN
  UNNEST(payload.pages) AS page
LIMIT 5;
```

For more information about arrays, see [Working with arrays](/bigquery/docs/arrays) . For more information about `  UNNEST  ` , see the [`  UNNEST  `](/bigquery/docs/reference/standard-sql/query-syntax#unnest_operator) topic.

### Filtering rows with `     OMIT RECORD IF    `

The `  OMIT IF  ` clause from legacy SQL lets you filter rows based on a condition that can apply to repeated fields. In GoogleSQL, you can model an `  OMIT IF  ` clause with an `  EXISTS  ` clause, `  IN  ` clause, or simple filter. For example, consider the following legacy SQL query:

``` text
#legacySQL
SELECT
  repository.url,
FROM
  [bigquery-public-data:samples.github_nested]
OMIT RECORD IF
  EVERY(payload.pages.page_name != 'db_jobskill'
        AND payload.pages.page_name != 'Profession');
```

The analogous GoogleSQL query is:

``` text
#standardSQL
SELECT
  repository.url
FROM
  `bigquery-public-data.samples.github_nested`
WHERE EXISTS (
  SELECT 1 FROM UNNEST(payload.pages)
  WHERE page_name = 'db_jobskill'
    OR page_name = 'Profession');
```

Here the `  EXISTS  ` clause evaluates to `  true  ` if there is at least one element of `  payload.pages  ` where the page name is `  'db_jobskill'  ` or `  'Profession'  ` .

Alternatively, suppose that the legacy SQL query uses `  IN  ` :

``` text
#legacySQL
SELECT
  repository.url,
FROM
  [bigquery-public-data:samples.github_nested]
OMIT RECORD IF NOT
  SOME(payload.pages.page_name IN ('db_jobskill', 'Profession'));
```

In GoogleSQL, you can express the query using an `  EXISTS  ` clause with `  IN  ` :

``` text
#standardSQL
SELECT
  repository.url
FROM
  `bigquery-public-data.samples.github_nested`
WHERE EXISTS (
  SELECT 1 FROM UNNEST(payload.pages)
  WHERE page_name IN ('db_jobskill', 'Profession'));
```

Consider the following legacy SQL query that filters records with 80 or fewer pages:

``` text
#legacySQL
SELECT
  repository.url,
FROM
  [bigquery-public-data:samples.github_nested]
OMIT RECORD IF
  COUNT(payload.pages.page_name) <= 80;
```

In this case, you can use a filter with `  ARRAY_LENGTH  ` in GoogleSQL:

``` text
#standardSQL
SELECT
  repository.url
FROM
  `bigquery-public-data.samples.github_nested`
WHERE
  ARRAY_LENGTH(payload.pages) > 80;
```

Note that the `  ARRAY_LENGTH  ` function applies to the repeated `  payload.pages  ` field directly rather than the nested field `  payload.pages.page_name  ` as in the legacy SQL query.

For more information about arrays and `  ARRAY  ` subqueries, see [Working with arrays](/bigquery/docs/arrays) .

## Semantic differences

The semantics of some operations differ between legacy and GoogleSQL.

### Runtime errors

Some functions in legacy SQL return `  NULL  ` for invalid input, potentially masking problems in queries or in data. GoogleSQL is generally more strict, and raises an error if an input is invalid.

  - For all mathematical functions and operators, legacy SQL does not check for overflows. GoogleSQL adds overflow checks, and raises an error if a computation overflows. This includes the `  +  ` , `  -  ` , `  *  ` operators, the `  SUM  ` , `  AVG  ` , and `  STDDEV  ` aggregate functions, and others.
  - GoogleSQL raises an error upon division by zero, whereas legacy SQL returns `  NULL  ` . To return `  NULL  ` for division by zero in GoogleSQL, use [`  SAFE_DIVIDE  `](/bigquery/docs/reference/standard-sql/mathematical_functions#safe_divide) .
  - GoogleSQL raises an error for `  CAST  ` s where the input format is invalid or out of range for the target type, whereas legacy SQL returns `  NULL  ` . To avoid raising an error for an invalid cast in GoogleSQL, use [`  SAFE_CAST  `](/bigquery/docs/reference/standard-sql/conversion_functions#safe_casting) .

### Nested repeated results

Queries executed using GoogleSQL preserve any nesting and repetition of the columns in the result, and the **Flatten Results** option has no effect. To return top-level columns for nested fields, use the `  .*  ` operator on struct columns. For example:

``` text
#standardSQL
SELECT
  repository.*
FROM
  `bigquery-public-data.samples.github_nested`
LIMIT 5;
```

To return top-level columns for repeated nested fields ( `  ARRAY  ` s of `  STRUCT  ` s), use a `  JOIN  ` to take the cross product of the table's rows and the elements of the repeated nested field. For example:

``` text
#standardSQL
SELECT
  repository.url,
  page.*
FROM
  `bigquery-public-data.samples.github_nested`
JOIN
  UNNEST(payload.pages) AS page
LIMIT 5;
```

For more information about arrays and `  ARRAY  ` subqueries, see [Working with arrays](/bigquery/docs/arrays) .

### NOT IN conditions and NULL

Legacy SQL does not comply with the SQL standard in its handling of `  NULL  ` with `  NOT IN  ` conditions, whereas GoogleSQL does. Consider the following legacy SQL query, which finds the number of words that don't appear in the GitHub sample table as locations:

``` text
#legacySQL
SELECT COUNT(*)
FROM [bigquery-public-data.samples.shakespeare]
WHERE word NOT IN (
  SELECT actor_attributes.location
  FROM [bigquery-public-data.samples.github_nested]
);
```

This query returns 163,716 as the count, indicating that there are 163,716 words that don't appear as locations in the GitHub table. Now consider the following GoogleSQL query:

``` text
#standardSQL
SELECT COUNT(*)
FROM `bigquery-public-data.samples.shakespeare`
WHERE word NOT IN (
  SELECT actor_attributes.location
  FROM `bigquery-public-data.samples.github_nested`
);
```

This query returns 0 as the count. The difference is due to the semantics of `  NOT IN  ` with GoogleSQL, which returns `  NULL  ` if any value on the right hand side is `  NULL  ` . To achieve the same results as with the legacy SQL query, use a `  WHERE  ` clause to exclude the `  NULL  ` values:

``` text
#standardSQL
SELECT COUNT(*)
FROM `bigquery-public-data.samples.shakespeare`
WHERE word NOT IN (
  SELECT actor_attributes.location
  FROM `bigquery-public-data.samples.github_nested`
  WHERE actor_attributes.location IS NOT NULL
);
```

This query returns 163,716 as the count. Alternatively, use a `  NOT EXISTS  ` condition:

``` text
#standardSQL
SELECT COUNT(*)
FROM `bigquery-public-data.samples.shakespeare` AS t
WHERE NOT EXISTS (
  SELECT 1
  FROM `bigquery-public-data.samples.github_nested`
  WHERE t.word = actor_attributes.location
);
```

This query also returns 163,716 as the count. For further reading, see the [comparison operators](/bigquery/docs/reference/standard-sql/operators#comparison_operators) section of the documentation, which explains the semantics of `  IN  ` , `  NOT IN  ` , `  EXISTS  ` , and other comparison operators.

## Differences in user-defined JavaScript functions

The [User-defined functions](/bigquery/docs/user-defined-functions) topic documents how to use JavaScript user-defined functions with GoogleSQL. This section explains some of the key differences between user-defined functions in legacy and GoogleSQL.

### Functions in the query text

With GoogleSQL, you use `  CREATE TEMPORARY FUNCTION  ` as part of the query body rather than specifying user-defined functions separately. Examples of defining functions separately include using the UDF Editor in the Google Cloud console or using the `  --udf_resource  ` flag in [the bq command-line tool](/bigquery/docs/reference/bq-cli-reference) .

Consider the following GoogleSQL query:

``` text
#standardSQL
-- Computes the harmonic mean of the elements in 'arr'.
-- The harmonic mean of x_1, x_2, ..., x_n can be expressed as:
--   n / ((1 / x_1) + (1 / x_2) + ... + (1 / x_n))
CREATE TEMPORARY FUNCTION HarmonicMean(arr ARRAY<FLOAT64>)
  RETURNS FLOAT64 LANGUAGE js AS """
var sum_of_reciprocals = 0;
for (var i = 0; i < arr.length; ++i) {
  sum_of_reciprocals += 1 / arr[i];
}
return arr.length / sum_of_reciprocals;
""";

WITH T AS (
  SELECT GENERATE_ARRAY(1.0, x * 4, x) AS arr
  FROM UNNEST([1, 2, 3, 4, 5]) AS x
)
SELECT arr, HarmonicMean(arr) AS h_mean
FROM T;
```

This query defines a JavaScript function named `  HarmonicMean  ` and then applies it to the array column `  arr  ` from `  T  ` .

For more information about user-defined functions, see the [User-defined functions](/bigquery/docs/user-defined-functions) topic.

### Functions operate on values rather than rows

In legacy SQL, JavaScript functions operate on rows from a table. In standard SQL, as in the preceding example, JavaScript functions operate on values. To pass a row value to a JavaScript function using GoogleSQL, define a function that takes a struct of the same row type as the table. For example:

``` text
#standardSQL
-- Takes a struct of x, y, and z and returns a struct with a new field foo.
CREATE TEMPORARY FUNCTION AddField(s STRUCT<x FLOAT64, y BOOL, z STRING>)
  RETURNS STRUCT<x FLOAT64, y BOOL, z STRING, foo STRING> LANGUAGE js AS """
var new_struct = new Object();
new_struct.x = s.x;
new_struct.y = s.y;
new_struct.z = s.z;
if (s.y) {
  new_struct.foo = 'bar';
} else {
  new_struct.foo = 'baz';
}

return new_struct;
""";

WITH T AS (
  SELECT x, MOD(off, 2) = 0 AS y, CAST(x AS STRING) AS z
  FROM UNNEST([5.0, 4.0, 3.0, 2.0, 1.0]) AS x WITH OFFSET off
)
SELECT AddField(t).*
FROM T AS t;
```

This query defines a JavaScript function that takes a struct with the same row type as `  T  ` and creates a new struct with an additional field named `  foo  ` . The `  SELECT  ` statement passes the row `  t  ` as input to the function and uses `  .*  ` to return the fields of the resulting struct in the output.

## Migrating table wildcard functions

This section describes in detail how to migrate legacy SQL [table wildcard functions](/bigquery/docs/reference/legacy-sql#tablewildcardfunctions) to GoogleSQL.

### The TABLE\_DATE\_RANGE function

The legacy SQL `  TABLE_DATE_RANGE  ` functions work on tables that conform to a specific naming scheme: `  <prefix>YYYYMMDD  ` , where the `  <prefix>  ` represents the first part of a table name and `  YYYYMMDD  ` represents the date associated with that table's data.

For example, the following legacy SQL query finds the average temperature from a set of daily tables that contain Seattle area weather data:

``` text
#legacySQL
SELECT
  ROUND(AVG(TemperatureF),1) AS AVG_TEMP_F
FROM
  TABLE_DATE_RANGE([mydataset.sea_weather_],
                    TIMESTAMP("2016-05-01"),
                    TIMESTAMP("2016-05-09"))
```

In GoogleSQL, an equivalent query uses a table wildcard and the `  BETWEEN  ` clause.

``` text
#standardSQL
SELECT
  ROUND(AVG(TemperatureF),1) AS AVG_TEMP_F
FROM
  `mydataset.sea_weather_*`
WHERE
  _TABLE_SUFFIX BETWEEN '20160501' AND '20160509'
```

### The TABLE\_DATE\_RANGE\_STRICT function

This function is equivalent to `  TABLE_DATE_RANGE  ` , except that it fails with an error if any daily table in the sequence is missing.

**Note:** If you don't need the query to fail when tables are missing, use the simpler `  _TABLE_SUFFIX BETWEEN 'YYYYMMDD' AND 'YYYYMMDD'  ` filter, as shown in the [`  TABLE_DATE_RANGE  ` migration example](#the_table_date_range_function) .

**Detailed migration for the TABLE\_DATE\_RANGE\_STRICT function**

Consider the same query as in the previous example, with the `  TABLE_DATE_RANGE_STRICT  ` function:

``` text
#legacySQL
SELECT
  ROUND(AVG(TemperatureF),1) AS AVG_TEMP_F
FROM
  TABLE_DATE_RANGE_STRICT([mydataset.sea_weather_],
                    TIMESTAMP("2016-05-01"),
                    TIMESTAMP("2016-05-09"))
```

To make an equivalent GoogleSQL query with error handling, the query should be split into two phases: validation and query execution. Depending on the application and query complexity, it can be achieved using [Composability using WITH clauses](#composability_using_with_clauses) or [BigQuery Scripting (procedural SQL)](/bigquery/docs/reference/standard-sql/procedural-language) .

Translated query using [`  WITH  ` clause](#composability_using_with_clauses) and conditional `  ERROR  ` :

``` text
#standardSQL
WITH MissingTables AS (
  SELECT
    STRING_AGG(FORMAT_DATE('%Y%m%d', day), ', ') AS missing_suffixes
  FROM
    UNNEST(GENERATE_DATE_ARRAY(DATE '2016-05-01', DATE '2016-05-09')) AS day
  WHERE
    FORMAT_DATE('%Y%m%d', day) NOT IN (
      SELECT _TABLE_SUFFIX
      FROM `mydataset.sea_weather_*`
      WHERE _TABLE_SUFFIX BETWEEN '20160501' AND '20160509'
    )
)
SELECT
  IF(missing_suffixes IS NOT NULL,
    ERROR(FORMAT("Not found suffixes: %s", missing_suffixes)),
    (
      SELECT ROUND(AVG(TemperatureF),1)
      FROM `mydataset.sea_weather_*`
      WHERE _TABLE_SUFFIX BETWEEN '20160501' AND '20160509'
    )
  ) AS AVG_TEMP_F
FROM MissingTables
```

And using [BigQuery Scripting (procedural SQL)](/bigquery/docs/reference/standard-sql/procedural-language) :

``` text
#standardSQL
BEGIN
  DECLARE missing_suffixes STRING;

  SET missing_suffixes = (
    SELECT STRING_AGG(FORMAT_DATE('%Y%m%d', day), ', ')
    FROM UNNEST(GENERATE_DATE_ARRAY(DATE '2016-05-01', DATE '2016-05-09')) AS day
    WHERE FORMAT_DATE('%Y%m%d', day) NOT IN (
      SELECT _TABLE_SUFFIX
      FROM `mydataset.sea_weather_*`
      WHERE _TABLE_SUFFIX BETWEEN '20160501' AND '20160509'
    )
  );

  -- Raise error or run query
  IF missing_suffixes IS NOT NULL THEN
    SELECT ERROR(FORMAT("Not found suffixes: %s", missing_suffixes));
  ELSE
    SELECT
      ROUND(AVG(TemperatureF),1) AS AVG_TEMP_F
    FROM
      `mydataset.sea_weather_*`
    WHERE
      _TABLE_SUFFIX BETWEEN '20160501' AND '20160509';
  END IF;
END;
```

### The TABLE\_QUERY function

The legacy SQL `  TABLE_QUERY  ` function lets you find table names based on patterns. When migrating a `  TABLE_QUERY  ` function to GoogleSQL, which does not support the `  TABLE_QUERY  ` function, you can instead filter using the `  _TABLE_SUFFIX  ` pseudocolumn. Keep the following differences in mind when migrating:

  - In legacy SQL, you place the `  TABLE_QUERY  ` function in the `  FROM  ` clause, whereas in GoogleSQL, you filter using the `  _TABLE_SUFFIX  ` pseudocolumn in the `  WHERE  ` clause.

  - In legacy SQL, the `  TABLE_QUERY  ` function operates on the entire table name (or `  table_id  ` ), whereas in GoogleSQL, the `  _TABLE_SUFFIX  ` pseudocolumn contains part or all of the table name, depending on how you use the wildcard character.

#### Filter in the WHERE clause

When migrating from legacy SQL to GoogleSQL, move the filter to the `  WHERE  ` clause. For example, the following query finds the maximum temperatures across all years that end in the number `  0  ` :

``` text
#legacySQL
SELECT
  max,
  ROUND((max-32)*5/9,1) celsius,
  year
FROM
  TABLE_QUERY([bigquery-public-data:noaa_gsod],
               'REGEXP_MATCH(table_id, r"0$")')
WHERE
  max != 9999.9 # code for missing data
  AND max > 100 # to improve ORDER BY performance
ORDER BY
  max DESC
```

In GoogleSQL, an equivalent query uses a table wildcard and places the regular expression function, `  REGEXP_CONTAINS  ` , in the `  WHERE  ` clause:

``` text
#standardSQL
SELECT
  max,
  ROUND((max-32)*5/9,1) celsius,
  year
FROM
  `bigquery-public-data.noaa_gsod.gsod*`
WHERE
  max != 9999.9 # code for missing data
  AND max > 100 # to improve ORDER BY performance
  AND REGEXP_CONTAINS(_TABLE_SUFFIX, r"0$")
ORDER BY
  max DESC
```

#### Differences between table\_id and \_TABLE\_SUFFIX

In the legacy SQL `  TABLE_QUERY(dataset, expr)  ` function, the second parameter is an expression that operates over the entire table name, using the value `  table_id  ` . When migrating to GoogleSQL, the filter that you create in the `  WHERE  ` clause operates on the value of `  _TABLE_SUFFIX  ` , which can include part or all of the table name, depending on your use of the wildcard character.

For example, the following legacy SQL query uses the entire table name in a regular expression to find the maximum temperatures across all years that end in the number `  0  ` :

``` text
#legacySQL
SELECT
  max,
  ROUND((max-32)*5/9,1) celsius,
  year
FROM
  TABLE_QUERY([bigquery-public-data:noaa_gsod], 'REGEXP_MATCH(table_id, r"gsod\d{3}0")')
WHERE
  max != 9999.9 # code for missing data
  AND max > 100 # to improve ORDER BY performance
ORDER BY
  max DESC
```

In GoogleSQL, an equivalent query can use the entire table name or only a part of the table name. You can use an empty prefix in GoogleSQL so that your filter operates over the entire table name ``  FROM `bigquery-public-data.noaa_gsod.*`  `` .

However, longer prefixes perform better than empty prefixes, so the following example uses a longer prefix, which means that the value of `  _TABLE_SUFFIX  ` is only part of the table name.

``` text
#standardSQL
SELECT
  max,
  ROUND((max-32)*5/9,1) celsius,
  year
FROM
  `bigquery-public-data.noaa_gsod.gsod*`
WHERE
  max != 9999.9 # code for missing data
  AND max > 100 # to improve ORDER BY performance
  AND REGEXP_CONTAINS(_TABLE_SUFFIX, r"\d{3}0")
ORDER BY
  max DESC
```
