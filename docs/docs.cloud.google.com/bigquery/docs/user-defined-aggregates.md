# User-defined aggregate functions

This document describes how to create, call, and delete user-defined aggregate functions (UDAFs) in BigQuery.

A UDAF lets you create an aggregate function by using an expression that contains code. A UDAF accepts columns of input, performs a calculation on a group of rows at a time, and then returns the result of that calculation as a single value.

## Create a SQL UDAF

This section describes the various ways that you can create a persistent or temporary SQL UDAF in BigQuery.

### Create a persistent SQL UDAF

You can create a SQL UDAF that is persistent, meaning that you can reuse the UDAF across multiple queries. Persistent UDAFs are safe to call when they are shared between owners. UDAFs can't mutate data, talk to external systems, or send logs to Google Cloud Observability or similar applications.

To create a persistent UDAF, use the [`  CREATE AGGREGATE FUNCTION  ` statement](/bigquery/docs/reference/standard-sql/data-definition-language#sql-create-udaf-function) without the `  TEMP  ` or `  TEMPORARY  ` keyword. You must include the dataset in the function path.

For example, the following query creates a persistent UDAF that's called `  ScaledAverage  ` :

``` text
CREATE AGGREGATE FUNCTION myproject.mydataset.ScaledAverage(
  dividend FLOAT64,
  divisor FLOAT64)
RETURNS FLOAT64
AS (
  AVG(dividend / divisor)
);
```

### Create a temporary SQL UDAF

You can create a SQL UDAF that is temporary, meaning that the UDAF only exists in the scope of a single query, script, session, or procedure.

To create a temporary UDAF, use the [`  CREATE AGGREGATE FUNCTION  ` statement](/bigquery/docs/reference/standard-sql/data-definition-language#sql-create-udaf-function) with the `  TEMP  ` or `  TEMPORARY  ` keyword.

For example, the following query creates a temporary UDAF that's called `  ScaledAverage  ` :

``` text
CREATE TEMP AGGREGATE FUNCTION ScaledAverage(
  dividend FLOAT64,
  divisor FLOAT64)
RETURNS FLOAT64
AS (
  AVG(dividend / divisor)
);
```

### Use aggregate and non-aggregate parameters

You can create a SQL UDAF that has both aggregate and non-aggregate parameters.

UDAFs normally aggregate function parameters across all rows in a [group](/bigquery/docs/reference/standard-sql/query-syntax#group_by_clause) . However, you can specify a function parameter as non-aggregate with the `  NOT AGGREGATE  ` keyword.

A non-aggregate function parameter is a scalar function parameter with a constant value for all rows in a group. A valid non-aggregate function parameter must be a literal. Inside the UDAF definition, aggregate function parameters can only appear as function arguments to aggregate function calls. References to non-aggregate function parameters can appear anywhere in the UDAF definition.

For example, the following function contains an aggregate parameter that's called `  dividend  ` , and a non-aggregate parameter called `  divisor  ` :

``` text
-- Create the function.
CREATE TEMP AGGREGATE FUNCTION ScaledSum(
  dividend FLOAT64,
  divisor FLOAT64 NOT AGGREGATE)
RETURNS FLOAT64
AS (
  SUM(dividend) / divisor
);
```

### Use the default project in the function body

In the body of a SQL UDAF, any references to BigQuery entities, such as tables or views, must include the project ID unless the entity resides in the same project that contains the UDAF.

For example, consider the following statement:

``` text
CREATE AGGREGATE FUNCTION project1.dataset_a.ScaledAverage(
  dividend FLOAT64,
  divisor FLOAT64)
RETURNS FLOAT64
AS (
  ( SELECT AVG(dividend / divisor) FROM dataset_a.my_table )
);
```

If you run the preceding statement in the `  project1  ` project, the statement succeeds because `  my_table  ` exists in `  project1  ` . However, if you run the preceding statement from a different project, the statement fails. To correct the error, include the project ID in the table reference:

``` text
CREATE AGGREGATE FUNCTION project1.dataset_a.ScaledAverage(
  dividend FLOAT64,
  divisor FLOAT64)
RETURNS FLOAT64
AS (
  ( SELECT AVG(dividend / divisor) FROM project1.dataset_a.my_table )
);
```

You can also reference an entity in a different project or dataset from the one where you create the function:

``` text
CREATE AGGREGATE FUNCTION project1.dataset_a.ScaledAverage(
  dividend FLOAT64,
  divisor FLOAT64)
RETURNS FLOAT64
AS (
  ( SELECT AVG(dividend / divisor) FROM project2.dataset_c.my_table )
);
```

## Create a JavaScript UDAF

This section describes the various ways in which you can create a JavaScript UDAF in BigQuery. There are a few rules to observe when creating a JavaScript UDAF:

  - The body of the JavaScript UDAF must be a quoted string literal that represents the JavaScript code. To learn more about the different types of quoted string literals that you can use, see [Formats for quoted literals](/bigquery/docs/reference/standard-sql/lexical#quoted_literals) .

  - Only certain type encodings are allowed. For more information, see [Permitted SQL type encodings in a JavaScript UDAF](#javascript-type-encodings) .

  - The JavaScript function body must include four JavaScript functions that initialize, aggregate, merge, and finalize the results for the JavaScript UDAF ( `  initialState  ` , `  aggregate  ` , `  merge  ` , and `  finalize  ` ). For more information, see [Permitted SQL type encodings in a JavaScript UDAF](#required-javascript-aggregate-functions) .

  - Any value returned by the `  initialState  ` function or that is left in the `  state  ` argument after the `  aggregate  ` or `  merge  ` function is called, must be serializable. If you want to work with non-serializable aggregation data, such as functions or symbol fields, you must use the included `  serialize  ` and `  deserialize  ` functions. To learn more, see [Serialize and deserialize data in a JavaScript UDAF](#serialize-javascript-udaf) .

### Create a persistent JavaScript UDAF

You can create a JavaScript UDAF that is persistent, meaning that you can reuse the UDAF across multiple queries. Persistent UDAFs are safe to call when they are shared between owners. UDAFs can't mutate data, talk to external systems, or send logs to Google Cloud Observability or similar applications.

To create a persistent UDAF, use the [`  CREATE AGGREGATE FUNCTION  ` statement](/bigquery/docs/reference/standard-sql/data-definition-language#javascript-create-udaf-function) without the `  TEMP  ` or `  TEMPORARY  ` keyword. You must include the dataset in the function path.

The following query creates a persistent JavaScript UDAF that's called `  SumPositive  ` :

``` text
CREATE OR REPLACE AGGREGATE FUNCTION my_project.my_dataset.SumPositive(x FLOAT64)
RETURNS FLOAT64
LANGUAGE js
AS r'''

  export function initialState() {
    return {sum: 0}
  }
  export function aggregate(state, x) {
    if (x > 0) {
      state.sum += x;
    }
  }
  export function merge(state, partialState) {
    state.sum += partialState.sum;
  }
  export function finalize(state) {
    return state.sum;
  }

''';

-- Call the JavaScript UDAF.
WITH numbers AS (
  SELECT * FROM UNNEST([1.0, -1.0, 3.0, -3.0, 5.0, -5.0]) AS x)
SELECT my_project.my_dataset.SumPositive(x) AS sum FROM numbers;

/*-----*
 | sum |
 +-----+
 | 9.0 |
 *-----*/
```

### Create a temporary JavaScript UDAF

You can create a JavaScript UDAF that is temporary, meaning that the UDAF only exists in the scope of a single query, script, session, or procedure.

To create a temporary UDAF, use the [`  CREATE AGGREGATE FUNCTION  ` statement](/bigquery/docs/reference/standard-sql/data-definition-language#javascript-create-udaf-function) with the `  TEMP  ` or `  TEMPORARY  ` keyword.

The following query creates a temporary JavaScript UDAF that's called `  SumPositive  ` :

``` text
CREATE TEMP AGGREGATE FUNCTION SumPositive(x FLOAT64)
RETURNS FLOAT64
LANGUAGE js
AS r'''

  export function initialState() {
    return {sum: 0}
  }
  export function aggregate(state, x) {
    if (x > 0) {
      state.sum += x;
    }
  }
  export function merge(state, partialState) {
    state.sum += partialState.sum;
  }
  export function finalize(state) {
    return state.sum;
  }

''';

-- Call the JavaScript UDAF.
WITH numbers AS (
  SELECT * FROM UNNEST([1.0, -1.0, 3.0, -3.0, 5.0, -5.0]) AS x)
SELECT SumPositive(x) AS sum FROM numbers;

/*-----*
 | sum |
 +-----+
 | 9.0 |
 *-----*/
```

### Include non-aggregate parameters in a JavaScript UDAF

You can create a JavaScript UDAF that has both aggregate and non-aggregate parameters.

UDAFs normally aggregate function parameters across all rows in a [group](/bigquery/docs/reference/standard-sql/query-syntax#group_by_clause) . However, you can specify a function parameter as non-aggregate with the `  NOT AGGREGATE  ` keyword.

A non-aggregate function parameter is a scalar function parameter with a constant value for all rows in a group. A valid non-aggregate function parameter must be a literal. Inside the UDAF definition, aggregate function parameters can only appear as function arguments to aggregate function calls. References to non-aggregate function parameters can appear anywhere in the UDAF definition.

In the following example, the JavaScript UDAF contains an aggregate parameter called `  s  ` and a non-aggregate parameter called `  delimiter  ` :

``` text
CREATE TEMP AGGREGATE FUNCTION JsStringAgg(
  s STRING,
  delimiter STRING NOT AGGREGATE)
RETURNS STRING
LANGUAGE js
AS r'''

  export function initialState() {
    return {strings: []}
  }
  export function aggregate(state, s) {
    state.strings.push(s);
  }
  export function merge(state, partialState) {
    state.strings = state.strings.concat(partialState.strings);
  }
  export function finalize(state, delimiter) {
    return state.strings.join(delimiter);
  }

''';

-- Call the JavaScript UDAF.
WITH strings AS (
  SELECT * FROM UNNEST(["aaa", "bbb", "ccc", "ddd"]) AS values)
SELECT JsStringAgg(values, '.') AS result FROM strings;

/*-----------------*
 | result          |
 +-----------------+
 | aaa.bbb.ccc.ddd |
 *-----------------*/
```

### Serialize and deserialize data in a JavaScript UDAF

BigQuery must serialize any object returned by the `  initialState  ` function or that is left in the `  state  ` argument after the `  aggregate  ` or `  merge  ` function is called. BigQuery supports serializing an object if all fields are one of the following:

  - A JavaScript primitive value (for example: `  2  ` , `  "abc"  ` , `  null  ` , `  undefined  ` ).
  - A JavaScript object for which BigQuery supports serializing all field values.
  - A JavaScript array for which BigQuery supports serializing all elements.

The following return values are serializable:

``` text
export function initialState() {
  return {a: "", b: 3, c: null, d: {x: 23} }
}
```

``` text
export function initialState() {
  return {value: 2.3};
}
```

The following return values are not serializable:

``` text
export function initialState() {
  return {
    value: function() {return 6;}
  }
}
```

``` text
export function initialState() {
  return 2.3;
}
```

If you want to work with non-serializable aggregation states, the JavaScript UDAF must include the `  serialize  ` and `  deserialize  ` functions. The `  serialize  ` function converts the aggregation state into a serializable object; the `  deserialize  ` function converts the serializable object back into an aggregation state.

In the following example, an external library calculates sums by using an interface:

``` text
export class SumAggregator {
 constructor() {
   this.sum = 0;
 }
 update(value) {
   this.sum += value;
 }
 getSum() {
   return this.sum;
 }
}
```

The following query doesn't execute because the `  SumAggregator  ` class object is not BigQuery-serializable, due to the presence of functions inside of the class.

``` text
CREATE TEMP AGGREGATE FUNCTION F(x FLOAT64)
RETURNS FLOAT64
LANGUAGE js
AS r'''

  class SumAggregator {
   constructor() {
     this.sum = 0;
   }

   update(value) {
     this.sum += value;
   }

   getSum() {
     return this.sum;
   }
  }

  export function initialState() {
   return new SumAggregator();
  }

  export function aggregate(agg, value) {
   agg.update(value);
  }

  export function merge(agg1, agg2) {
   agg1.update(agg2.getSum());
  }

  export function finalize(agg) {
   return agg.getSum();
  }

''';

--Error: getSum is not a function
SELECT F(x) AS results FROM UNNEST([1,2,3,4]) AS x;
```

If you add the `  serialize  ` and `  deserialize  ` functions to the preceding query, the query runs because the `  SumAggregator  ` class object is converted to an object that is BigQuery-serializable and then back to a `  SumAggregator  ` class object again.

``` text
CREATE TEMP AGGREGATE FUNCTION F(x FLOAT64)
RETURNS FLOAT64
LANGUAGE js
AS r'''

  class SumAggregator {
   constructor() {
     this.sum = 0;
   }

   update(value) {
     this.sum += value;
   }

   getSum() {
     return this.sum;
   }
  }

  export function initialState() {
   return new SumAggregator();
  }

  export function aggregate(agg, value) {
   agg.update(value);
  }

  export function merge(agg1, agg2) {
   agg1.update(agg2.getSum());
  }

  export function finalize(agg) {
   return agg.getSum();
  }

  export function serialize(agg) {
   return {sum: agg.getSum()};
  }

  export function deserialize(serialized) {
   var agg = new SumAggregator();
   agg.update(serialized.sum);
   return agg;
  }

''';

SELECT F(x) AS results FROM UNNEST([1,2,3,4]) AS x;

/*-----------------*
 | results         |
 +-----------------+
 | 10.0            |
 *-----------------*/
```

To learn more about the serialization functions, see [Optional JavaScript serialization functions](#javascript-serialization-functions) .

### Include global variables and custom functions in a JavaScript UDAF

The JavaScript function body can include custom JavaScript code such as JavaScript global variables and custom functions.

Global variables are executed when the JavaScript is loaded into BigQuery and before the `  initialState  ` function is executed. Global variables might be useful if you need to perform one-time initialization work that shouldn't repeat for each aggregation group, as would be the case with the `  initialState  ` , `  aggregate  ` , `  merge  ` , and `  finalize  ` functions.

Don't use global variables to store aggregation state. Instead, limit aggregation state to objects passed to exported functions. Only use global variables to cache expensive operations that are not specific to any particular aggregation operation.

In the following query, the `  SumOfPrimes  ` function calculates a sum, but only prime numbers are included in the calculation. In the JavaScript function body, there are two global variables, `  primes  ` and `  maxTested  ` , that are initialized first. In addition, there is a custom function called `  isPrime  ` that checks if a number is prime.

``` text
CREATE TEMP AGGREGATE FUNCTION SumOfPrimes(x INT64)
RETURNS INT64
LANGUAGE js
AS r'''

  var primes = new Set([2]);
  var maxTested = 2;

  function isPrime(n) {
    if (primes.has(n)) {
      return true;
    }
    if (n <= maxTested) {
      return false;
    }
    for (var k = 2; k < n; ++k) {
      if (!isPrime(k)) {
        continue;
      }
      if ((n % k) == 0) {
        maxTested = n;
        return false;
      }
    }
    maxTested = n;
    primes.add(n);
    return true;
  }

  export function initialState() {
    return {sum: 0};
  }

  export function aggregate(state, x) {
    x = Number(x);
    if (isPrime(x)) {
      state.sum += x;
    }
  }

  export function merge(state, partialState) {
    state.sum += partialState.sum;
  }

  export function finalize(state) {
    return state.sum;
  }

''';

-- Call the JavaScript UDAF.
WITH numbers AS (
  SELECT * FROM UNNEST([10, 11, 13, 17, 19, 20]) AS x)
SELECT SumOfPrimes(x) AS sum FROM numbers;

/*-----*
 | sum |
 +-----+
 | 60  |
 *-----*/
```

### Include JavaScript libraries

You can extend your JavaScript UDAFs with the `  library  ` option in the `  OPTIONS  ` clause. This option lets you specify external code libraries for the JavaScript UDAF, and then import those libraries with the `  import  ` declaration.

In the following example, code in `  bar.js  ` is available to any code in the function body of the JavaScript UDAF:

``` text
CREATE TEMP AGGREGATE FUNCTION JsAggFn(x FLOAT64)
RETURNS FLOAT64
LANGUAGE js
OPTIONS (library = ['gs://foo/bar.js'])
AS r'''

  import doInterestingStuff from 'bar.js';

  export function initialState() {
    return ...
  }
  export function aggregate(state, x) {
    var result = doInterestingStuff(x);
    ...
  }
  export function merge(state, partial_state) {
    ...
  }
  export function finalize(state) {
    return ...;
  }

''';
```

### Required JavaScript structure

Unlike a JavaScript UDF, where the function body is free-form JavaScript that runs for every row, the function body for a JavaScript UDAF is a JavaScript module that contains some built-in exported functions, which are invoked at various stages in the aggregation process. Some of these built-in functions are required, while others are optional. You can also add your JavaScript functions.

#### Required JavaScript aggregation functions

You can include your JavaScript functions, but the JavaScript function body must include the following exportable JavaScript functions:

  - `  initialState([nonAggregateParam])  ` : returns a JavaScript object that represents an aggregation state in which no rows have been aggregated yet.

  - `  aggregate(state, aggregateParam[, ...][, nonAggregateParam])  ` : aggregates one row of data, updating state to store the result of the aggregation. Does not return a value.

  - `  merge(state, partialState, [nonAggregateParam])  ` : merges aggregation state `  partialState  ` into aggregation state `  state  ` . This function is used when the engine aggregates different sections of data in parallel and needs to combine the results. Does not return a value.

  - `  finalize(finalState, [nonAggregateParam])  ` : returns the final result of the aggregate function, given a final aggregation state `  finalState  ` .

To learn more about the required functions, see [Required functions in a JavaScript UDAF](/bigquery/docs/reference/standard-sql/data-definition-language#javascript-interface-functions-udaf) .

#### Optional JavaScript serialization functions

If you want to work with non-serializable aggregation states, the JavaScript UDAF must provide the `  serialize  ` and `  deserialize  ` functions. The `  serialize  ` function converts the aggregation state to a BigQuery-serializable object; the `  deserialize  ` function converts the BigQuery-serializable object back into an aggregation state.

  - `  serialize(state)  ` : returns a serializable object that contains the information in aggregation state, to be deserialized through the `  deserialize  ` function.

  - `  deserialize(serializedState)  ` : deserializes `  serializedState  ` (previously serialized by the `  serialize  ` function) into an aggregation state that can be passed into the `  serialize  ` , `  aggregate  ` , `  merge  ` , or `  finalize  ` functions.

To learn more about the built-in JavaScript serialization functions, see [Serialization functions for a JavaScript UDAF](/bigquery/docs/reference/standard-sql/data-definition-language#javascript-serialization-functions-udaf) .

To learn how to serialize and deserialize data with a JavaScript UDAF, see [Serialize and deserialize data in a JavaScript UDAF](#serialize-javascript-udaf) .

### Permitted SQL type encodings in a JavaScript UDAF

In JavaScript UDAFs, the following supported [GoogleSQL data types](/bigquery/docs/reference/standard-sql/data-types) represent [JavaScript data types](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects) as follows:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>GoogleSQL<br />
data type</th>
<th>JavaScript<br />
data type</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       ARRAY      </code></td>
<td><code dir="ltr" translate="no">       Array      </code></td>
<td>An array of arrays is not supported. To get around this limitation, use the <code dir="ltr" translate="no">       Array&lt;Object&lt;Array&gt;&gt;      </code> (JavaScript) and <code dir="ltr" translate="no">       ARRAY&lt;STRUCT&lt;ARRAY&gt;&gt;      </code> (GoogleSQL) data types.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
<td><code dir="ltr" translate="no">       Number      </code> or <code dir="ltr" translate="no">       String      </code></td>
<td>Same as <code dir="ltr" translate="no">       NUMERIC      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       BOOL      </code></td>
<td><code dir="ltr" translate="no">       Boolean      </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       BYTES      </code></td>
<td><code dir="ltr" translate="no">       Uint8Array      </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       DATE      </code></td>
<td><code dir="ltr" translate="no">       Date      </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
<td><code dir="ltr" translate="no">       Number      </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td><code dir="ltr" translate="no">       BigInt      </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       JSON      </code></td>
<td>Various types</td>
<td>The GoogleSQL <code dir="ltr" translate="no">       JSON      </code> data type can be converted into a JavaScript <code dir="ltr" translate="no">       Object      </code> , <code dir="ltr" translate="no">       Array      </code> , or other GoogleSQL-supported JavaScript data type.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td><code dir="ltr" translate="no">       Number      </code> or <code dir="ltr" translate="no">       String      </code></td>
<td>If a <code dir="ltr" translate="no">       NUMERIC      </code> value can be represented exactly as an <a href="https://en.wikipedia.org/wiki/Floating-point_arithmetic#IEEE_754:_floating_point_in_modern_computers">IEEE 754 floating-point</a> value (range <code dir="ltr" translate="no">       [-2               53              , 2               53              ]      </code> ), and has no fractional part, it is encoded as a <code dir="ltr" translate="no">       Number      </code> data type, otherwise it is encoded as a <code dir="ltr" translate="no">       String      </code> data type.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><code dir="ltr" translate="no">       String      </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       STRUCT      </code></td>
<td><code dir="ltr" translate="no">       Object      </code></td>
<td>Each <code dir="ltr" translate="no">       STRUCT      </code> field is a named property in the <code dir="ltr" translate="no">       Object      </code> data type. An unnamed <code dir="ltr" translate="no">       STRUCT      </code> field is not supported.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td><code dir="ltr" translate="no">       Date      </code></td>
<td><code dir="ltr" translate="no">       Date      </code> contains a microsecond field with the microsecond fraction of <code dir="ltr" translate="no">       TIMESTAMP      </code> .</td>
</tr>
</tbody>
</table>

**Note:** The SQL encodings for JavaScript UDAFs are different from those for JavaScript UDFs.

## Call a UDAF

This section describes the various ways that you can call a persistent or temporary UDAF after you create it in BigQuery.

**Note:** JavaScript UDAF calls don't support the `  ORDER BY  ` clause.

### Call a persistent UDAF

You can call a persistent UDAF in the same way that you call a built-in aggregate function. For more information, see [Aggregate function calls](/bigquery/docs/reference/standard-sql/aggregate-function-calls) . You must include the dataset in the function path.

In the following example, the query calls a persistent UDAF that's called `  WeightedAverage  ` :

``` text
SELECT my_project.my_dataset.WeightedAverage(item, weight, 2) AS weighted_average
FROM (
  SELECT 1 AS item, 2.45 AS weight UNION ALL
  SELECT 3 AS item, 0.11 AS weight UNION ALL
  SELECT 5 AS item, 7.02 AS weight
);
```

A table with the following results is produced:

``` text
/*------------------*
 | weighted_average |
 +------------------+
 | 4.5              |
 *------------------*/
```

### Call a temporary UDAF

You can call a temporary UDAF in the same way that you call a built-in aggregate function. For more information, see [Aggregate function calls](/bigquery/docs/reference/standard-sql/aggregate-function-calls) .

The temporary function must be included in a [multi-statement query](/bigquery/docs/multi-statement-queries) or [procedure](/bigquery/docs/procedures) that contains the UDAF function call.

In the following example, the query calls a temporary UDAF that's called `  WeightedAverage  ` :

``` text
CREATE TEMP AGGREGATE FUNCTION WeightedAverage(...)

-- Temporary UDAF function call
SELECT WeightedAverage(item, weight, 2) AS weighted_average
FROM (
  SELECT 1 AS item, 2.45 AS weight UNION ALL
  SELECT 3 AS item, 0.11 AS weight UNION ALL
  SELECT 5 AS item, 7.02 AS weight
);
```

A table with the following results is produced:

``` text
/*------------------*
 | weighted_average |
 +------------------+
 | 4.5              |
 *------------------*/
```

### Ignore or include rows with `     NULL    ` values

When a JavaScript UDAF is called with the `  IGNORE NULLS  ` argument, BigQuery automatically skips over rows for which any aggregate argument evaluates to `  NULL  ` . Such rows are excluded from the aggregation completely and are not passed to the JavaScript `  aggregate  ` function. When `  RESPECT NULLS  ` argument is provided, `  NULL  ` filtration is disabled, and every row is passed to the JavaScript UDAF, regardless of `  NULL  ` values.

When neither the `  IGNORE NULLS  ` nor `  RESPECT NULLS  ` argument is provided, the default argument is `  IGNORE NULLS  ` .

The following example illustrates the default `  NULL  ` behavior, the `  IGNORE NULLS  ` behavior, and the `  RESPECT NULLS  ` behavior:

``` text
CREATE TEMP AGGREGATE FUNCTION SumPositive(x FLOAT64)
RETURNS FLOAT64
LANGUAGE js
AS r'''

  export function initialState() {
    return {sum: 0}
  }
  export function aggregate(state, x) {
    if (x == null) {
      // Use 1000 instead of 0 as placeholder for null so
      // that NULL values passed are visible in the result.
      state.sum += 1000;
      return;
    }
    if (x > 0) {
      state.sum += x;
    }
  }
  export function merge(state, partialState) {
    state.sum += partialState.sum;
  }
  export function finalize(state) {
    return state.sum;
  }

''';

-- Call the JavaScript UDAF.
WITH numbers AS (
  SELECT * FROM UNNEST([1.0, 2.0, NULL]) AS x)
SELECT
  SumPositive(x) AS sum,
  SumPositive(x IGNORE NULLS) AS sum_ignore_nulls,
  SumPositive(x RESPECT NULLS) AS sum_respect_nulls
FROM numbers;

/*-----+------------------+-------------------*
 | sum | sum_ignore_nulls | sum_respect_nulls |
 +-----+------------------+-------------------+
 | 3.0 | 3.0              | 1003.0            |
 *-----+------------------+-------------------*/
```

## Delete a UDAF

This section describes the various ways that you can delete a persistent or temporary UDAF after you created it in BigQuery.

### Delete a persistent UDAF

To delete a persistent UDAF, use the [`  DROP FUNCTION  ` statement](/bigquery/docs/reference/standard-sql/data-definition-language#drop_function_statement) . You must include the dataset in the function path.

In the following example, the query deletes a persistent UDAF that's called `  WeightedAverage  ` :

``` text
DROP FUNCTION IF EXISTS my_project.my_dataset.WeightedAverage;
```

### Delete a temporary UDAF

To delete a temporary UDAF, use the [`  DROP FUNCTION  ` statement](/bigquery/docs/reference/standard-sql/data-definition-language#drop_function_statement) .

In the following example, the query deletes a temporary UDAF that's called `  WeightedAverage  ` :

``` text
DROP FUNCTION IF EXISTS WeightedAverage;
```

A temporary UDAF expires as soon as the query finishes. The UDAF doesn't need to be deleted unless you want to remove it early from a [multi-statement query](/bigquery/docs/multi-statement-queries) or [procedure](/bigquery/docs/procedures) .

## List UDAFs

UDAFs are a type of routine. To list all of the routines in a dataset, see [List routines](/bigquery/docs/routines#list_routines) .

## Performance tips

If you want to improve the performance of your queries, consider the following:

  - Prefilter your input. Processing data in JavaScript is more expensive than in SQL, so it is best to filter the input as much as possible in SQL first.
    
    The following query is less efficient because it filters the input by using `  x > 0  ` in the UDAF call:
    
    ``` text
    SELECT JsFunc(x) FROM t;
    ```
    
    The following query is more efficient because it prefilters the input by using `  WHERE x > 0  ` before the UDAF is called:
    
    ``` text
    SELECT JsFunc(x) FROM t WHERE x > 0;
    ```

  - Use built-in aggregate functions instead of JavaScript when possible. Re-implementing a built-in aggregate function in JavaScript is slower than calling a built-in aggregate function that does the same thing.
    
    The following query is less efficient because it implements a UDAF:
    
    ``` text
    SELECT SumSquare(x) FROM t;
    ```
    
    The following query is more efficient because it implements a built-in function that produces the same results as the previous query:
    
    ``` text
    SELECT SUM(x*x) FROM t;
    ```

  - JavaScript UDAFs are appropriate for more complex aggregation operations, which can't be expressed through built-in functions.

  - Use memory efficiently. The JavaScript processing environment has limited memory available for each query. JavaScript UDAF queries that accumulate too much local state might fail due to memory exhaustion. Be especially mindful about minimizing the size of aggregation state objects and avoid aggregation states which accumulate large numbers of rows.
    
    The following query is not efficient because the `  aggregate  ` function uses an unbounded amount of memory when the number of rows processed gets large.
    
    ``` text
    export function initialState() {
      return {rows: []};
    }
    export function aggregate(state, x) {
      state.rows.push(x);
    }
    ...
    ```

  - Use partitioned tables when possible. JavaScript UDAFs typically run more efficiently when querying against a partitioned table compared to a non-partitioned table, because a partitioned table stores data in many smaller files compared to a non-partitioned table, thus enabling higher parallelism.

## Limitations

  - UDAFs have the same limitations that apply to UDFs. For details, see [UDF limitations](/bigquery/docs/user-defined-functions#limitations) .

  - Only literals, query parameters, and script variables can be passed in as non-aggregate arguments for a UDAF.

  - The use of the `  ORDER BY  ` clause in a JavaScript UDAF function call is unsupported.
    
    ``` text
    SELECT MyUdaf(x ORDER BY y) FROM t; -- Error: ORDER BY is unsupported.
    ```

## Pricing

UDAFs are billed using the standard [BigQuery pricing](https://cloud.google.com/bigquery/pricing) model.

## Quotas and limits

UDAFs have the same quotas and limits that apply to UDFs. For information about UDF quotas, see [Quotas and limits](/bigquery/quotas#udf_limits) .
