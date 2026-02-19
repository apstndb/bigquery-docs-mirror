GoogleSQL for BigQuery supports operators. Operators are represented by special characters or keywords; they don't use function call syntax. An operator manipulates any number of data inputs, also called operands, and returns a result.

Common conventions:

  - Unless otherwise specified, all operators return `  NULL  ` when one of the operands is `  NULL  ` .
  - All operators will throw an error if the computation result overflows.
  - For all floating point operations, `  +/-inf  ` and `  NaN  ` may only be returned if one of the operands is `  +/-inf  ` or `  NaN  ` . In other cases, an error is returned.

### Operator precedence

The following table lists all GoogleSQL operators from highest to lowest precedence, i.e., the order in which they will be evaluated within a statement.

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Order of Precedence</th>
<th>Operator</th>
<th>Input Data Types</th>
<th>Name</th>
<th>Operator Arity</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>1</td>
<td>Field access operator</td>
<td><code dir="ltr" translate="no">        STRUCT       </code><br />
<code dir="ltr" translate="no">        JSON       </code><br />
</td>
<td>Field access operator</td>
<td>Binary</td>
</tr>
<tr class="even">
<td></td>
<td>Array subscript operator</td>
<td><code dir="ltr" translate="no">       ARRAY      </code></td>
<td>Array position. Must be used with <code dir="ltr" translate="no">       OFFSET      </code> or <code dir="ltr" translate="no">       ORDINAL      </code> —see <a href="/bigquery/docs/reference/standard-sql/array_functions">Array Functions</a> .</td>
<td>Binary</td>
</tr>
<tr class="odd">
<td></td>
<td>JSON subscript operator</td>
<td><code dir="ltr" translate="no">       JSON      </code></td>
<td>Field name or array position in JSON.</td>
<td>Binary</td>
</tr>
<tr class="even">
<td>2</td>
<td><code dir="ltr" translate="no">       +      </code></td>
<td>All numeric types</td>
<td>Unary plus</td>
<td>Unary</td>
</tr>
<tr class="odd">
<td></td>
<td><code dir="ltr" translate="no">       -      </code></td>
<td>All numeric types</td>
<td>Unary minus</td>
<td>Unary</td>
</tr>
<tr class="even">
<td></td>
<td><code dir="ltr" translate="no">       ~      </code></td>
<td>Integer or <code dir="ltr" translate="no">       BYTES      </code></td>
<td>Bitwise not</td>
<td>Unary</td>
</tr>
<tr class="odd">
<td>3</td>
<td><code dir="ltr" translate="no">       *      </code></td>
<td>All numeric types</td>
<td>Multiplication</td>
<td>Binary</td>
</tr>
<tr class="even">
<td></td>
<td><code dir="ltr" translate="no">       /      </code></td>
<td>All numeric types</td>
<td>Division</td>
<td>Binary</td>
</tr>
<tr class="odd">
<td></td>
<td><code dir="ltr" translate="no">       ||      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code> , <code dir="ltr" translate="no">       BYTES      </code> , or <code dir="ltr" translate="no">       ARRAY&lt;T&gt;      </code></td>
<td>Concatenation operator</td>
<td>Binary</td>
</tr>
<tr class="even">
<td>4</td>
<td><code dir="ltr" translate="no">       +      </code></td>
<td>All numeric types, <code dir="ltr" translate="no">       DATE      </code> with <code dir="ltr" translate="no">       INT64      </code> , <code dir="ltr" translate="no">       INTERVAL      </code></td>
<td>Addition</td>
<td>Binary</td>
</tr>
<tr class="odd">
<td></td>
<td><code dir="ltr" translate="no">       -      </code></td>
<td>All numeric types, <code dir="ltr" translate="no">       DATE      </code> with <code dir="ltr" translate="no">       INT64      </code> , <code dir="ltr" translate="no">       INTERVAL      </code></td>
<td>Subtraction</td>
<td>Binary</td>
</tr>
<tr class="even">
<td>5</td>
<td><code dir="ltr" translate="no">       &lt;&lt;      </code></td>
<td>Integer or <code dir="ltr" translate="no">       BYTES      </code></td>
<td>Bitwise left-shift</td>
<td>Binary</td>
</tr>
<tr class="odd">
<td></td>
<td><code dir="ltr" translate="no">       &gt;&gt;      </code></td>
<td>Integer or <code dir="ltr" translate="no">       BYTES      </code></td>
<td>Bitwise right-shift</td>
<td>Binary</td>
</tr>
<tr class="even">
<td>6</td>
<td><code dir="ltr" translate="no">       &amp;      </code></td>
<td>Integer or <code dir="ltr" translate="no">       BYTES      </code></td>
<td>Bitwise and</td>
<td>Binary</td>
</tr>
<tr class="odd">
<td>7</td>
<td><code dir="ltr" translate="no">       ^      </code></td>
<td>Integer or <code dir="ltr" translate="no">       BYTES      </code></td>
<td>Bitwise xor</td>
<td>Binary</td>
</tr>
<tr class="even">
<td>8</td>
<td><code dir="ltr" translate="no">       |      </code></td>
<td>Integer or <code dir="ltr" translate="no">       BYTES      </code></td>
<td>Bitwise or</td>
<td>Binary</td>
</tr>
<tr class="odd">
<td>9 (Comparison Operators)</td>
<td><code dir="ltr" translate="no">       =      </code></td>
<td>Any comparable type. See <a href="/bigquery/docs/reference/standard-sql/data-types">Data Types</a> for a complete list.</td>
<td>Equal</td>
<td>Binary</td>
</tr>
<tr class="even">
<td></td>
<td><code dir="ltr" translate="no">       &lt;      </code></td>
<td>Any comparable type. See <a href="/bigquery/docs/reference/standard-sql/data-types">Data Types</a> for a complete list.</td>
<td>Less than</td>
<td>Binary</td>
</tr>
<tr class="odd">
<td></td>
<td><code dir="ltr" translate="no">       &gt;      </code></td>
<td>Any comparable type. See <a href="/bigquery/docs/reference/standard-sql/data-types">Data Types</a> for a complete list.</td>
<td>Greater than</td>
<td>Binary</td>
</tr>
<tr class="even">
<td></td>
<td><code dir="ltr" translate="no">       &lt;=      </code></td>
<td>Any comparable type. See <a href="/bigquery/docs/reference/standard-sql/data-types">Data Types</a> for a complete list.</td>
<td>Less than or equal to</td>
<td>Binary</td>
</tr>
<tr class="odd">
<td></td>
<td><code dir="ltr" translate="no">       &gt;=      </code></td>
<td>Any comparable type. See <a href="/bigquery/docs/reference/standard-sql/data-types">Data Types</a> for a complete list.</td>
<td>Greater than or equal to</td>
<td>Binary</td>
</tr>
<tr class="even">
<td></td>
<td><code dir="ltr" translate="no">       !=      </code> , <code dir="ltr" translate="no">       &lt;&gt;      </code></td>
<td>Any comparable type. See <a href="/bigquery/docs/reference/standard-sql/data-types">Data Types</a> for a complete list.</td>
<td>Not equal</td>
<td>Binary</td>
</tr>
<tr class="odd">
<td></td>
<td><code dir="ltr" translate="no">       [NOT] LIKE      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code> and <code dir="ltr" translate="no">       BYTES      </code></td>
<td>Value does [not] match the pattern specified</td>
<td>Binary</td>
</tr>
<tr class="even">
<td></td>
<td>Quantified LIKE</td>
<td><code dir="ltr" translate="no">       STRING      </code> and <code dir="ltr" translate="no">       BYTES      </code></td>
<td>Checks a search value for matches against several patterns.</td>
<td>Binary</td>
</tr>
<tr class="odd">
<td></td>
<td><code dir="ltr" translate="no">       [NOT] BETWEEN      </code></td>
<td>Any comparable types. See <a href="/bigquery/docs/reference/standard-sql/data-types">Data Types</a> for a complete list.</td>
<td>Value is [not] within the range specified</td>
<td>Binary</td>
</tr>
<tr class="even">
<td></td>
<td><code dir="ltr" translate="no">       [NOT] IN      </code></td>
<td>Any comparable types. See <a href="/bigquery/docs/reference/standard-sql/data-types">Data Types</a> for a complete list.</td>
<td>Value is [not] in the set of values specified</td>
<td>Binary</td>
</tr>
<tr class="odd">
<td></td>
<td><code dir="ltr" translate="no">       IS [NOT] NULL      </code></td>
<td>All</td>
<td>Value is [not] <code dir="ltr" translate="no">       NULL      </code></td>
<td>Unary</td>
</tr>
<tr class="even">
<td></td>
<td><code dir="ltr" translate="no">       IS [NOT] TRUE      </code></td>
<td><code dir="ltr" translate="no">       BOOL      </code></td>
<td>Value is [not] <code dir="ltr" translate="no">       TRUE      </code> .</td>
<td>Unary</td>
</tr>
<tr class="odd">
<td></td>
<td><code dir="ltr" translate="no">       IS [NOT] FALSE      </code></td>
<td><code dir="ltr" translate="no">       BOOL      </code></td>
<td>Value is [not] <code dir="ltr" translate="no">       FALSE      </code> .</td>
<td>Unary</td>
</tr>
<tr class="even">
<td>10</td>
<td><code dir="ltr" translate="no">       NOT      </code></td>
<td><code dir="ltr" translate="no">       BOOL      </code></td>
<td>Logical <code dir="ltr" translate="no">       NOT      </code></td>
<td>Unary</td>
</tr>
<tr class="odd">
<td>11</td>
<td><code dir="ltr" translate="no">       AND      </code></td>
<td><code dir="ltr" translate="no">       BOOL      </code></td>
<td>Logical <code dir="ltr" translate="no">       AND      </code></td>
<td>Binary</td>
</tr>
<tr class="even">
<td>12</td>
<td><code dir="ltr" translate="no">       OR      </code></td>
<td><code dir="ltr" translate="no">       BOOL      </code></td>
<td>Logical <code dir="ltr" translate="no">       OR      </code></td>
<td>Binary</td>
</tr>
</tbody>
</table>

For example, the logical expression:

`  x OR y AND z  `

is interpreted as:

`  ( x OR ( y AND z ) )  `

Operators with the same precedence are left associative. This means that those operators are grouped together starting from the left and moving right. For example, the expression:

`  x AND y AND z  `

is interpreted as:

`  ( ( x AND y ) AND z )  `

The expression:

`  x * y / z  `

is interpreted as:

`  ( ( x * y ) / z )  `

All comparison operators have the same priority, but comparison operators aren't associative. Therefore, parentheses are required to resolve ambiguity. For example:

`  (x < y) IS FALSE  `

### Operator list

<table>
<thead>
<tr class="header">
<th>Name</th>
<th>Summary</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="#field_access_operator">Field access operator</a></td>
<td>Gets the value of a field.</td>
</tr>
<tr class="even">
<td><a href="#array_subscript_operator">Array subscript operator</a></td>
<td>Gets a value from an array at a specific position.</td>
</tr>
<tr class="odd">
<td><a href="#struct_subscript_operator">Struct subscript operator</a></td>
<td>Gets the value of a field at a selected position in a struct.</td>
</tr>
<tr class="even">
<td><a href="#json_subscript_operator">JSON subscript operator</a></td>
<td>Gets a value of an array element or field in a JSON expression.</td>
</tr>
<tr class="odd">
<td><a href="#arithmetic_operators">Arithmetic operators</a></td>
<td>Performs arithmetic operations.</td>
</tr>
<tr class="even">
<td><a href="#date_arithmetics_operators">Date arithmetics operators</a></td>
<td>Performs arithmetic operations on dates.</td>
</tr>
<tr class="odd">
<td><a href="#datetime_subtraction">Datetime subtraction</a></td>
<td>Computes the difference between two datetimes as an interval.</td>
</tr>
<tr class="even">
<td><a href="#interval_arithmetic_operators">Interval arithmetic operators</a></td>
<td>Adds an interval to a datetime or subtracts an interval from a datetime.</td>
</tr>
<tr class="odd">
<td><a href="#bitwise_operators">Bitwise operators</a></td>
<td>Performs bit manipulation.</td>
</tr>
<tr class="even">
<td><a href="#logical_operators">Logical operators</a></td>
<td>Tests for the truth of some condition and produces <code dir="ltr" translate="no">       TRUE      </code> , <code dir="ltr" translate="no">       FALSE      </code> , or <code dir="ltr" translate="no">       NULL      </code> .</td>
</tr>
<tr class="odd">
<td><a href="#comparison_operators">Comparison operators</a></td>
<td>Compares operands and produces the results of the comparison as a <code dir="ltr" translate="no">       BOOL      </code> value.</td>
</tr>
<tr class="even">
<td><a href="#exists_operator"><code dir="ltr" translate="no">        EXISTS       </code> operator</a></td>
<td>Checks if a subquery produces one or more rows.</td>
</tr>
<tr class="odd">
<td><a href="#in_operators"><code dir="ltr" translate="no">        IN       </code> operator</a></td>
<td>Checks for an equal value in a set of values.</td>
</tr>
<tr class="even">
<td><a href="#is_operators"><code dir="ltr" translate="no">        IS       </code> operators</a></td>
<td>Checks for the truth of a condition and produces either <code dir="ltr" translate="no">       TRUE      </code> or <code dir="ltr" translate="no">       FALSE      </code> .</td>
</tr>
<tr class="odd">
<td><a href="#is_distinct"><code dir="ltr" translate="no">        IS DISTINCT FROM       </code> operator</a></td>
<td>Checks if values are considered to be distinct from each other.</td>
</tr>
<tr class="even">
<td><a href="#like_operator"><code dir="ltr" translate="no">        LIKE       </code> operator</a></td>
<td>Checks if values are like or not like one another.</td>
</tr>
<tr class="odd">
<td><a href="#like_operator_quantified">Quantified <code dir="ltr" translate="no">        LIKE       </code> operator</a></td>
<td>Checks a search value for matches against several patterns.</td>
</tr>
<tr class="even">
<td><a href="#concatenation_operator">Concatenation operator</a></td>
<td>Combines multiple values into one.</td>
</tr>
<tr class="odd">
<td><a href="#with_expression"><code dir="ltr" translate="no">        WITH       </code> expression</a></td>
<td>Creates variables for re-use and produces a result expression.</td>
</tr>
</tbody>
</table>

### Field access operator

``` text
expression.fieldname[. ...]
```

**Description**

Gets the value of a field. Alternatively known as the dot operator. Can be used to access nested fields. For example, `  expression.fieldname1.fieldname2  ` .

Input values:

  - `  STRUCT  `
  - `  JSON  `

**Note:** If the field to access is within a `  STRUCT  ` , you can use the [struct subscript operator](#struct_subscript_operator) to access the field by its position within the `  STRUCT  ` instead of by its name. Accessing by a field by position is useful when fields are un-named or have ambiguous names.

**Return type**

  - For `  STRUCT  ` : SQL data type of `  fieldname  ` . If a field isn't found in the struct, an error is thrown.
  - For `  JSON  ` : `  JSON  ` . If a field isn't found in a JSON value, a SQL `  NULL  ` is returned.

**Example**

In the following example, the field access operations are `  .address  ` and `  .country  ` .

``` text
SELECT
  STRUCT(
    STRUCT('Yonge Street' AS street, 'Canada' AS country)
      AS address).address.country

/*---------+
 | country |
 +---------+
 | Canada  |
 +---------*/
```

### Array subscript operator

**Note:** Syntax characters enclosed in double quotes ( `  ""  ` ) are literal and required.

``` text
array_expression "[" array_subscript_specifier "]"

array_subscript_specifier:
  { index | position_keyword(index) }

position_keyword:
  { OFFSET | SAFE_OFFSET | ORDINAL | SAFE_ORDINAL }
```

**Description**

Gets a value from an array at a specific position.

Input values:

  - `  array_expression  ` : The input array.
  - `  position_keyword(index)  ` : Determines where the index for the array should start and how out-of-range indexes are handled. The index is an integer that represents a specific position in the array.
      - `  OFFSET(index)  ` : The index starts at zero. Produces an error if the index is out of range. To produce `  NULL  ` instead of an error, use `  SAFE_OFFSET(index)  ` . This position keyword produces the same result as `  index  ` by itself.
      - `  SAFE_OFFSET(index)  ` : The index starts at zero. Returns `  NULL  ` if the index is out of range.
      - `  ORDINAL(index)  ` : The index starts at one. Produces an error if the index is out of range. To produce `  NULL  ` instead of an error, use `  SAFE_ORDINAL(index)  ` .
      - `  SAFE_ORDINAL(index)  ` : The index starts at one. Returns `  NULL  ` if the index is out of range.
  - `  index  ` : An integer that represents a specific position in the array. If used by itself without a position keyword, the index starts at zero and produces an error if the index is out of range. To produce `  NULL  ` instead of an error, use the `  SAFE_OFFSET(index)  ` or `  SAFE_ORDINAL(index)  ` position keyword.

**Return type**

`  T  ` where `  array_expression  ` is `  ARRAY<T>  ` .

**Examples**

In following query, the array subscript operator is used to return values at specific position in `  item_array  ` . This query also shows what happens when you reference an index ( `  6  ` ) in an array that's out of range. If the `  SAFE  ` prefix is included, `  NULL  ` is returned, otherwise an error is produced.

``` text
SELECT
  ["coffee", "tea", "milk"] AS item_array,
  ["coffee", "tea", "milk"][0] AS item_index,
  ["coffee", "tea", "milk"][OFFSET(0)] AS item_offset,
  ["coffee", "tea", "milk"][ORDINAL(1)] AS item_ordinal,
  ["coffee", "tea", "milk"][SAFE_OFFSET(6)] AS item_safe_offset

/*---------------------+------------+-------------+--------------+------------------+
 | item_array          | item_index | item_offset | item_ordinal | item_safe_offset |
 +---------------------+------------+-------------+--------------+------------------+
 | [coffee, tea, milk] | coffee     | coffee      | coffee       | NULL             |
 +----------------------------------+-------------+--------------+------------------*/
```

When you reference an index that's out of range in an array, and a positional keyword that begins with `  SAFE  ` isn't included, an error is produced. For example:

``` text
-- Error. Array index 6 is out of bounds.
SELECT ["coffee", "tea", "milk"][6] AS item_offset
```

``` text
-- Error. Array index 6 is out of bounds.
SELECT ["coffee", "tea", "milk&quot;][OFFSET(6)] AS item_offset
```

### Struct subscript operator

**Note:** Syntax characters enclosed in double quotes ( `  ""  ` ) are literal and required.

``` text
struct_expression "[" struct_subscript_specifier "]"

struct_subscript_specifier:
  { index | position_keyword(index) }

position_keyword:
  { OFFSET | ORDINAL }
```

**Description**

Gets the value of a field at a selected position in a struct.

**Input types**

  - `  struct_expression  ` : The input struct.
  - `  position_keyword(index)  ` : Determines where the index for the struct should start and how out-of-range indexes are handled. The index is an integer literal or constant that represents a specific position in the struct.
      - `  OFFSET(index)  ` : The index starts at zero. Produces an error if the index is out of range. Produces the same result as `  index  ` by itself.
      - `  ORDINAL(index)  ` : The index starts at one. Produces an error if the index is out of range.
  - `  index  ` : An integer literal or constant that represents a specific position in the struct. If used by itself without a position keyword, the index starts at zero and produces an error if the index is out of range.

**Note:** The struct subscript operator doesn't support `  SAFE  ` positional keywords at this time.

**Examples**

In following query, the struct subscript operator is used to return values at specific locations in `  item_struct  ` using position keywords. This query also shows what happens when you reference an index ( `  6  ` ) in an struct that's out of range.

``` text
SELECT
  STRUCT<INT64, STRING, BOOL>(23, "tea", FALSE)[0] AS field_index<,
  STRUCTINT64, ST>RING, BOOL(23, "tea", FALSE)[OFFSET(0)] AS fi<eld_offset,
  STRUC>TINT64, STRING, BOOL(23, "tea", FALSE)[ORDINAL(1)] AS field_ordinal

/*-------------+--------------+---------------+
 | field_index | field_offset | field_ordinal |
 +-------------+--------------+---------------+
 | 23          | 23           | 23            |
 +-------------+--------------+---------------*/
```

When you reference an index that's out of range in a struct, an error is produced. For example:

``` text
-- Error: Field ordinal 6 is out of bounds in STRUCT
SELECT STRUCT<INT64, STRING, BOOL>(23, "tea", FALSE)[6] AS field_offset
```

``` text
-- Error: Field ordinal 6 is out of bounds in STRUCT
SELECT STRUCT<INT64, STRING, BOOL>(23, "tea", FALSE)[OFFSET(6)] AS field_offset
```

### JSON subscript operator

**Note:** Syntax characters enclosed in double quotes ( `  ""  ` ) are literal and required.

``` text
json_expression "[" array_element_id "]"
```

``` text
json_expression "[" field_name "]"
```

**Description**

Gets a value of an array element or field in a JSON expression. Can be used to access nested data.

Input values:

  - `  JSON expression  ` : The `  JSON  ` expression that contains an array element or field to return.
  - `  [array_element_id]  ` : An `  INT64  ` expression that represents a zero-based index in the array. If a negative value is entered, or the value is greater than or equal to the size of the array, or the JSON expression doesn't represent a JSON array, a SQL `  NULL  ` is returned.
  - `  [field_name]  ` : A `  STRING  ` expression that represents the name of a field in JSON. If the field name isn't found, or the JSON expression isn't a JSON object, a SQL `  NULL  ` is returned.

**Return type**

`  JSON  `

**Example**

In the following example:

  - `  json_value  ` is a JSON expression.
  - `  .class  ` is a JSON field access.
  - `  .students  ` is a JSON field access.
  - `  [0]  ` is a JSON subscript expression with an element offset that accesses the zeroth element of an array in the JSON value.
  - `  ['name']  ` is a JSON subscript expression with a field name that accesses a field.

<!-- end list -->

``` text
SELECT json_value.class.students[0]['name'] AS first_student
FROM
  UNNEST(
    [
      JSON '{"class" : {"students" : [{"name" : "Jane"}]}}',
      JSON '{"class" : {"students" : []}}',
      JSON '{"class" : {"students" : [{"name" : "John"}, {"name": "Jamie"}]}}'])
    AS json_value;

/*-----------------+
 | first_student   |
 +-----------------+
 | "Jane"          |
 | NULL            |
 | "John"          |
 +-----------------*/
```

### Arithmetic operators

All arithmetic operators accept input of numeric type `  T  ` , and the result type has type `  T  ` unless otherwise indicated in the description below:

<table>
<thead>
<tr class="header">
<th>Name</th>
<th>Syntax</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Addition</td>
<td><code dir="ltr" translate="no">       X + Y      </code></td>
</tr>
<tr class="even">
<td>Subtraction</td>
<td><code dir="ltr" translate="no">       X - Y      </code></td>
</tr>
<tr class="odd">
<td>Multiplication</td>
<td><code dir="ltr" translate="no">       X * Y      </code></td>
</tr>
<tr class="even">
<td>Division</td>
<td><code dir="ltr" translate="no">       X / Y      </code></td>
</tr>
<tr class="odd">
<td>Unary Plus</td>
<td><code dir="ltr" translate="no">       + X      </code></td>
</tr>
<tr class="even">
<td>Unary Minus</td>
<td><code dir="ltr" translate="no">       - X      </code></td>
</tr>
</tbody>
</table>

NOTE: Divide by zero operations return an error. To return a different result, consider the `  IEEE_DIVIDE  ` or `  SAFE_DIVIDE  ` functions.

Result types for Addition, Subtraction and Multiplication:

<table>
<thead>
<tr class="header">
<th>INPUT</th>
<th><code dir="ltr" translate="no">       INT64      </code></th>
<th><code dir="ltr" translate="no">       NUMERIC      </code></th>
<th><code dir="ltr" translate="no">       BIGNUMERIC      </code></th>
<th><code dir="ltr" translate="no">       FLOAT64      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
</tr>
</tbody>
</table>

Result types for Division:

<table>
<thead>
<tr class="header">
<th>INPUT</th>
<th><code dir="ltr" translate="no">       INT64      </code></th>
<th><code dir="ltr" translate="no">       NUMERIC      </code></th>
<th><code dir="ltr" translate="no">       BIGNUMERIC      </code></th>
<th><code dir="ltr" translate="no">       FLOAT64      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
</tr>
</tbody>
</table>

Result types for Unary Plus:

<table>
<thead>
<tr class="header">
<th>INPUT</th>
<th><code dir="ltr" translate="no">       INT64      </code></th>
<th><code dir="ltr" translate="no">       NUMERIC      </code></th>
<th><code dir="ltr" translate="no">       BIGNUMERIC      </code></th>
<th><code dir="ltr" translate="no">       FLOAT64      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>OUTPUT</td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
</tr>
</tbody>
</table>

Result types for Unary Minus:

<table>
<thead>
<tr class="header">
<th>INPUT</th>
<th><code dir="ltr" translate="no">       INT64      </code></th>
<th><code dir="ltr" translate="no">       NUMERIC      </code></th>
<th><code dir="ltr" translate="no">       BIGNUMERIC      </code></th>
<th><code dir="ltr" translate="no">       FLOAT64      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>OUTPUT</td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
</tr>
</tbody>
</table>

### Date arithmetics operators

Operators '+' and '-' can be used for arithmetic operations on dates.

``` text
date_expression + int64_expression
int64_expression + date_expression
date_expression - int64_expression
```

**Description**

Adds or subtracts `  int64_expression  ` days to or from `  date_expression  ` . This is equivalent to `  DATE_ADD  ` or `  DATE_SUB  ` functions, when interval is expressed in days.

**Return Data Type**

`  DATE  `

**Example**

``` text
SELECT DATE "2020-09-22" + 1 AS day_later, DATE "2020-09-22" - 7 AS week_ago

/*------------+------------+
 | day_later  | week_ago   |
 +------------+------------+
 | 2020-09-23 | 2020-09-15 |
 +------------+------------*/
```

### Datetime subtraction

``` text
date_expression - date_expression
timestamp_expression - timestamp_expression
datetime_expression - datetime_expression
```

**Description**

Computes the difference between two datetime values as an interval.

**Return Data Type**

`  INTERVAL  `

**Example**

``` text
SELECT
  DATE "2021-05-20" - DATE "2020-04-19" AS date_diff,
  TIMESTAMP "2021-06-01 12:34:56.789" - TIMESTAMP "2021-05-31 00:00:00" AS time_diff

/*-------------------+------------------------+
 | date_diff         | time_diff              |
 +-------------------+------------------------+
 | 0-0 396 0:0:0     | 0-0 0 36:34:56.789     |
 +-------------------+------------------------*/
```

### Interval arithmetic operators

**Addition and subtraction**

``` text
date_expression + interval_expression = DATETIME
date_expression - interval_expression = DATETIME
timestamp_expression + interval_expression = TIMESTAMP
timestamp_expression - interval_expression = TIMESTAMP
datetime_expression + interval_expression = DATETIME
datetime_expression - interval_expression = DATETIME
```

**Description**

Adds an interval to a datetime value or subtracts an interval from a datetime value.

**Example**

``` text
SELECT
  DATE "2021-04-20" + INTERVAL 25 HOUR AS date_plus,
  TIMESTAMP "2021-05-02 00:01:02.345+00" - INTERVAL 10 SECOND AS time_minus;

/*-------------------------+--------------------------------+
 | date_plus               | time_minus                     |
 +-------------------------+--------------------------------+
 | 2021-04-21 01:00:00     | 2021-05-02 00:00:52.345+00     |
 +-------------------------+--------------------------------*/
```

**Multiplication and division**

``` text
interval_expression * integer_expression = INTERVAL
interval_expression / integer_expression = INTERVAL
```

**Description**

Multiplies or divides an interval value by an integer.

**Example**

``` text
SELECT
  INTERVAL '1:2:3' HOUR TO SECOND * 10 AS mul1,
  INTERVAL 35 SECOND * 4 AS mul2,
  INTERVAL 10 YEAR / 3 AS div1,
  INTERVAL 1 MONTH / 12 AS div2

/*----------------+--------------+-------------+--------------+
 | mul1           | mul2         | div1        | div2         |
 +----------------+--------------+-------------+--------------+
 | 0-0 0 10:20:30 | 0-0 0 0:2:20 | 3-4 0 0:0:0 | 0-0 2 12:0:0 |
 +----------------+--------------+-------------+--------------*/
```

### Bitwise operators

All bitwise operators return the same type and the same length as the first operand.

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Name</th>
<th>Syntax</th>
<th>Input Data Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Bitwise not</td>
<td><code dir="ltr" translate="no">       ~ X      </code></td>
<td>Integer or <code dir="ltr" translate="no">       BYTES      </code></td>
<td>Performs logical negation on each bit, forming the ones' complement of the given binary value.</td>
</tr>
<tr class="even">
<td>Bitwise or</td>
<td><code dir="ltr" translate="no">       X | Y      </code></td>
<td><code dir="ltr" translate="no">       X      </code> : Integer or <code dir="ltr" translate="no">       BYTES      </code><br />
<code dir="ltr" translate="no">       Y      </code> : Same type as <code dir="ltr" translate="no">       X      </code></td>
<td>Takes two bit patterns of equal length and performs the logical inclusive <code dir="ltr" translate="no">       OR      </code> operation on each pair of the corresponding bits. This operator throws an error if <code dir="ltr" translate="no">       X      </code> and <code dir="ltr" translate="no">       Y      </code> are bytes of different lengths.</td>
</tr>
<tr class="odd">
<td>Bitwise xor</td>
<td><code dir="ltr" translate="no">       X ^ Y      </code></td>
<td><code dir="ltr" translate="no">       X      </code> : Integer or <code dir="ltr" translate="no">       BYTES      </code><br />
<code dir="ltr" translate="no">       Y      </code> : Same type as <code dir="ltr" translate="no">       X      </code></td>
<td>Takes two bit patterns of equal length and performs the logical exclusive <code dir="ltr" translate="no">       OR      </code> operation on each pair of the corresponding bits. This operator throws an error if <code dir="ltr" translate="no">       X      </code> and <code dir="ltr" translate="no">       Y      </code> are bytes of different lengths.</td>
</tr>
<tr class="even">
<td>Bitwise and</td>
<td><code dir="ltr" translate="no">       X &amp; Y      </code></td>
<td><code dir="ltr" translate="no">       X      </code> : Integer or <code dir="ltr" translate="no">       BYTES      </code><br />
<code dir="ltr" translate="no">       Y      </code> : Same type as <code dir="ltr" translate="no">       X      </code></td>
<td>Takes two bit patterns of equal length and performs the logical <code dir="ltr" translate="no">       AND      </code> operation on each pair of the corresponding bits. This operator throws an error if <code dir="ltr" translate="no">       X      </code> and <code dir="ltr" translate="no">       Y      </code> are bytes of different lengths.</td>
</tr>
<tr class="odd">
<td>Left shift</td>
<td><code dir="ltr" translate="no">       X &lt;&lt; Y      </code></td>
<td><code dir="ltr" translate="no">       X      </code> : Integer or <code dir="ltr" translate="no">       BYTES      </code><br />
<code dir="ltr" translate="no">       Y      </code> : <code dir="ltr" translate="no">       INT64      </code></td>
<td>Shifts the first operand <code dir="ltr" translate="no">       X      </code> to the left. This operator returns <code dir="ltr" translate="no">       0      </code> or a byte sequence of <code dir="ltr" translate="no">       b'\x00'      </code> if the second operand <code dir="ltr" translate="no">       Y      </code> is greater than or equal to the bit length of the first operand <code dir="ltr" translate="no">       X      </code> (for example, <code dir="ltr" translate="no">       64      </code> if <code dir="ltr" translate="no">       X      </code> has the type <code dir="ltr" translate="no">       INT64      </code> ). This operator throws an error if <code dir="ltr" translate="no">       Y      </code> is negative.</td>
</tr>
<tr class="even">
<td>Right shift</td>
<td><code dir="ltr" translate="no">       X &gt;&gt; Y      </code></td>
<td><code dir="ltr" translate="no">       X      </code> : Integer or <code dir="ltr" translate="no">       BYTES      </code><br />
<code dir="ltr" translate="no">       Y      </code> : <code dir="ltr" translate="no">       INT64      </code></td>
<td>Shifts the first operand <code dir="ltr" translate="no">       X      </code> to the right. This operator doesn't perform sign bit extension with a signed type (i.e., it fills vacant bits on the left with <code dir="ltr" translate="no">       0      </code> ). This operator returns <code dir="ltr" translate="no">       0      </code> or a byte sequence of <code dir="ltr" translate="no">       b'\x00'      </code> if the second operand <code dir="ltr" translate="no">       Y      </code> is greater than or equal to the bit length of the first operand <code dir="ltr" translate="no">       X      </code> (for example, <code dir="ltr" translate="no">       64      </code> if <code dir="ltr" translate="no">       X      </code> has the type <code dir="ltr" translate="no">       INT64      </code> ). This operator throws an error if <code dir="ltr" translate="no">       Y      </code> is negative.</td>
</tr>
</tbody>
</table>

### Logical operators

GoogleSQL supports the `  AND  ` , `  OR  ` , and `  NOT  ` logical operators. Logical operators allow only `  BOOL  ` or `  NULL  ` input and use [three-valued logic](https://en.wikipedia.org/wiki/Three-valued_logic) to produce a result. The result can be `  TRUE  ` , `  FALSE  ` , or `  NULL  ` :

<table>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">       x      </code></th>
<th><code dir="ltr" translate="no">       y      </code></th>
<th><code dir="ltr" translate="no">       x AND y      </code></th>
<th><code dir="ltr" translate="no">       x OR y      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       TRUE      </code></td>
<td><code dir="ltr" translate="no">       TRUE      </code></td>
<td><code dir="ltr" translate="no">       TRUE      </code></td>
<td><code dir="ltr" translate="no">       TRUE      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       TRUE      </code></td>
<td><code dir="ltr" translate="no">       FALSE      </code></td>
<td><code dir="ltr" translate="no">       FALSE      </code></td>
<td><code dir="ltr" translate="no">       TRUE      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       TRUE      </code></td>
<td><code dir="ltr" translate="no">       NULL      </code></td>
<td><code dir="ltr" translate="no">       NULL      </code></td>
<td><code dir="ltr" translate="no">       TRUE      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       FALSE      </code></td>
<td><code dir="ltr" translate="no">       TRUE      </code></td>
<td><code dir="ltr" translate="no">       FALSE      </code></td>
<td><code dir="ltr" translate="no">       TRUE      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       FALSE      </code></td>
<td><code dir="ltr" translate="no">       FALSE      </code></td>
<td><code dir="ltr" translate="no">       FALSE      </code></td>
<td><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       FALSE      </code></td>
<td><code dir="ltr" translate="no">       NULL      </code></td>
<td><code dir="ltr" translate="no">       FALSE      </code></td>
<td><code dir="ltr" translate="no">       NULL      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       NULL      </code></td>
<td><code dir="ltr" translate="no">       TRUE      </code></td>
<td><code dir="ltr" translate="no">       NULL      </code></td>
<td><code dir="ltr" translate="no">       TRUE      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       NULL      </code></td>
<td><code dir="ltr" translate="no">       FALSE      </code></td>
<td><code dir="ltr" translate="no">       FALSE      </code></td>
<td><code dir="ltr" translate="no">       NULL      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       NULL      </code></td>
<td><code dir="ltr" translate="no">       NULL      </code></td>
<td><code dir="ltr" translate="no">       NULL      </code></td>
<td><code dir="ltr" translate="no">       NULL      </code></td>
</tr>
</tbody>
</table>

<table>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">       x      </code></th>
<th><code dir="ltr" translate="no">       NOT x      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       TRUE      </code></td>
<td><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       FALSE      </code></td>
<td><code dir="ltr" translate="no">       TRUE      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       NULL      </code></td>
<td><code dir="ltr" translate="no">       NULL      </code></td>
</tr>
</tbody>
</table>

The order of evaluation of operands to `  AND  ` and `  OR  ` can vary, and evaluation can be skipped if unnecessary.

**Examples**

The examples in this section reference a table called `  entry_table  ` :

``` text
/*-------+
 | entry |
 +-------+
 | a     |
 | b     |
 | c     |
 | NULL  |
 +-------*/
```

``` text
SELECT 'a' FROM entry_table WHERE entry = >9;a'

--> a = 'a&>#39; = '>a' = TRUE
--> b = 'b&#>39; = 'a' = FALSE
-- NULL = NULL = 'a' = NULL

/*-------+
 | entry |
 +-------+
 | a     |
 +-------*/
```

``` text
SELECT entry FROM entry_table WHERE NOT (entry = 'a')>

-- a = NOT('>;a' = &#>39;a') = >NOT(TRUE) = FALSE>
-- b = NOT(&>#39;b' = &#>39;a') = NOT(F>ALSE) = TRUE>
-- NULL = NOT(NULL = 'a') = NOT(NULL) = NULL

/*-------+
 | entry |
 +-------+
 | b     |
 | c     |
 +-------*/
```

``` text
SELECT entry FROM entry_table WHERE entry IS NULL

-- a => 'a' I>S NULL = FALS>E
-- b = '>b' IS NULL => FALSE
-- NULL >= NULL IS NULL = TRUE

/*-------+
 | entry |
 +-------+
 | NULL  |
 +-------*/
```

### Comparison operators

Compares operands and produces the results of the comparison as a `  BOOL  ` value. These comparison operators are available:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Name</th>
<th>Syntax</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Less Than</td>
<td><code dir="ltr" translate="no">       X &lt; Y      </code></td>
<td>Returns <code dir="ltr" translate="no">       TRUE      </code> if <code dir="ltr" translate="no">       X      </code> is less than <code dir="ltr" translate="no">       Y      </code> . This operator supports specifying <a href="/bigquery/docs/reference/standard-sql/collation-concepts">collation</a> .</td>
</tr>
<tr class="even">
<td>Less Than or Equal To</td>
<td><code dir="ltr" translate="no">       X &lt;= Y      </code></td>
<td>Returns <code dir="ltr" translate="no">       TRUE      </code> if <code dir="ltr" translate="no">       X      </code> is less than or equal to <code dir="ltr" translate="no">       Y      </code> . This operator supports specifying <a href="/bigquery/docs/reference/standard-sql/collation-concepts">collation</a> .</td>
</tr>
<tr class="odd">
<td>Greater Than</td>
<td><code dir="ltr" translate="no">       X &gt; Y      </code></td>
<td>Returns <code dir="ltr" translate="no">       TRUE      </code> if <code dir="ltr" translate="no">       X      </code> is greater than <code dir="ltr" translate="no">       Y      </code> . This operator supports specifying <a href="/bigquery/docs/reference/standard-sql/collation-concepts">collation</a> .</td>
</tr>
<tr class="even">
<td>Greater Than or Equal To</td>
<td><code dir="ltr" translate="no">       X &gt;= Y      </code></td>
<td>Returns <code dir="ltr" translate="no">       TRUE      </code> if <code dir="ltr" translate="no">       X      </code> is greater than or equal to <code dir="ltr" translate="no">       Y      </code> . This operator supports specifying <a href="/bigquery/docs/reference/standard-sql/collation-concepts">collation</a> .</td>
</tr>
<tr class="odd">
<td>Equal</td>
<td><code dir="ltr" translate="no">       X = Y      </code></td>
<td>Returns <code dir="ltr" translate="no">       TRUE      </code> if <code dir="ltr" translate="no">       X      </code> is equal to <code dir="ltr" translate="no">       Y      </code> . This operator supports specifying <a href="/bigquery/docs/reference/standard-sql/collation-concepts">collation</a> .</td>
</tr>
<tr class="even">
<td>Not Equal</td>
<td><code dir="ltr" translate="no">       X != Y      </code><br />
<code dir="ltr" translate="no">       X &lt;&gt; Y      </code></td>
<td>Returns <code dir="ltr" translate="no">       TRUE      </code> if <code dir="ltr" translate="no">       X      </code> isn't equal to <code dir="ltr" translate="no">       Y      </code> . This operator supports specifying <a href="/bigquery/docs/reference/standard-sql/collation-concepts">collation</a> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       BETWEEN      </code></td>
<td><code dir="ltr" translate="no">       X [NOT] BETWEEN Y AND Z      </code></td>
<td><p>Returns <code dir="ltr" translate="no">        TRUE       </code> if <code dir="ltr" translate="no">        X       </code> is [not] within the range specified. The result of <code dir="ltr" translate="no">        X BETWEEN Y AND Z       </code> is equivalent to <code dir="ltr" translate="no">        Y &lt;= X AND X &lt;= Z       </code> but <code dir="ltr" translate="no">        X       </code> is evaluated only once in the former. This operator supports specifying <a href="/bigquery/docs/reference/standard-sql/collation-concepts">collation</a> .</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       LIKE      </code></td>
<td><code dir="ltr" translate="no">       X [NOT] LIKE Y      </code></td>
<td>See the <a href="#like_operator">`LIKE` operator</a> for details.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       IN      </code></td>
<td>Multiple</td>
<td>See the <a href="#in_operator">`IN` operator</a> for details.</td>
</tr>
</tbody>
</table>

The following rules apply to operands in a comparison operator:

  - The operands must be [comparable](/bigquery/docs/reference/standard-sql/data-types#comparable_data_types) .
  - A comparison operator generally requires both operands to be of the same type.
  - If the operands are of different types, and the values of those types can be converted to a common type without loss of precision, they are generally coerced to that common type for the comparison.
  - A literal operand is generally coerced to the same data type of a non-literal operand that's part of the comparison.
  - Struct operands support only these comparison operators: equal ( `  =  ` ), not equal ( `  !=  ` and `  <>  ` ), and `  IN  ` .

The following rules apply when comparing these data types:

  - `  FLOAT64  ` : All comparisons with `  NaN  ` return `  FALSE  ` , except for `  !=  ` and `  <>  ` , which return `  TRUE  ` .

  - `  BOOL  ` : `  FALSE  ` is less than `  TRUE  ` .

  - `  STRING  ` : Strings are compared codepoint-by-codepoint, which means that canonically equivalent strings are only guaranteed to compare as equal if they have been normalized first.

  - `  JSON  ` : You can't compare JSON, but you can compare the values inside of JSON if you convert the values to SQL values first. For more information, see [`  JSON  ` functions](/bigquery/docs/reference/standard-sql/json_functions) .

  - `  NULL  ` : Any operation with a `  NULL  ` input returns `  NULL  ` .

  - `  STRUCT  ` : When testing a struct for equality, it's possible that one or more fields are `  NULL  ` . In such cases:
    
      - If all non- `  NULL  ` field values are equal, the comparison returns `  NULL  ` .
      - If any non- `  NULL  ` field values aren't equal, the comparison returns `  FALSE  ` .
    
    The following table demonstrates how `  STRUCT  ` data types are compared when they have fields that are `  NULL  ` valued.
    
    <table>
    <thead>
    <tr class="header">
    <th>Struct1</th>
    <th>Struct2</th>
    <th>Struct1 = Struct2</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><code dir="ltr" translate="no">         STRUCT(1, NULL)        </code></td>
    <td><code dir="ltr" translate="no">         STRUCT(1, NULL)        </code></td>
    <td><code dir="ltr" translate="no">         NULL        </code></td>
    </tr>
    <tr class="even">
    <td><code dir="ltr" translate="no">         STRUCT(1, NULL)        </code></td>
    <td><code dir="ltr" translate="no">         STRUCT(2, NULL)        </code></td>
    <td><code dir="ltr" translate="no">         FALSE        </code></td>
    </tr>
    <tr class="odd">
    <td><code dir="ltr" translate="no">         STRUCT(1,2)        </code></td>
    <td><code dir="ltr" translate="no">         STRUCT(1, NULL)        </code></td>
    <td><code dir="ltr" translate="no">         NULL        </code></td>
    </tr>
    </tbody>
    </table>

### `     EXISTS    ` operator

``` text
EXISTS( subquery )
```

**Description**

Returns `  TRUE  ` if the subquery produces one or more rows. Returns `  FALSE  ` if the subquery produces zero rows. Never returns `  NULL  ` . To learn more about how you can use a subquery with `  EXISTS  ` , see [`  EXISTS  ` subqueries](/bigquery/docs/reference/standard-sql/subqueries#exists_subquery_concepts) .

**Examples**

In this example, the `  EXISTS  ` operator returns `  FALSE  ` because there are no rows in `  Words  ` where the direction is `  south  ` :

``` text
WITH Words AS (
  SELECT 'Intend' as value, 'east' as direction UNION ALL
  SELECT 'Secure', 'north' UNION ALL
  SELECT 'Clarity', 'west'
 )
SELECT EXISTS( SELECT value FROM Words WHERE direction = 'south' ) as result;

/*--------+
 | result |
 +--------+
 | FALSE  |
 +--------*/
```

### `     IN    ` operator

The `  IN  ` operator supports the following syntax:

``` text
search_value [NOT] IN value_set

value_set:
  {
    (expression[, ...])
    | (subquery)
    | UNNEST(array_expression)
  }
```

**Description**

Checks for an equal value in a set of values. [Semantic rules](#semantic_rules_in) apply, but in general, `  IN  ` returns `  TRUE  ` if an equal value is found, `  FALSE  ` if an equal value is excluded, otherwise `  NULL  ` . `  NOT IN  ` returns `  FALSE  ` if an equal value is found, `  TRUE  ` if an equal value is excluded, otherwise `  NULL  ` .

  - `  search_value  ` : The expression that's compared to a set of values.

  - `  value_set  ` : One or more values to compare to a search value.
    
      - `  (expression[, ...])  ` : A list of expressions.
    
      - `  (subquery)  ` : A [subquery](/bigquery/docs/reference/standard-sql/subqueries#about_subqueries) that returns a single column. The values in that column are the set of values. If no rows are produced, the set of values is empty.
    
      - `  UNNEST(array_expression)  ` : An [UNNEST operator](/bigquery/docs/reference/standard-sql/query-syntax#unnest_operator) that returns a column of values from an array expression. This is equivalent to:
        
        ``` text
        IN (SELECT element FROM UNNEST(array_expression) AS element)
        ```

This operator supports [collation](/bigquery/docs/reference/standard-sql/collation-concepts#collate_funcs) , but these limitations apply:

  - `  [NOT] IN UNNEST  ` doesn't support collation.
  - If collation is used with a list of expressions, there must be at least one item in the list.

**Semantic rules**

When using the `  IN  ` operator, the following semantics apply in this order:

  - Returns `  FALSE  ` if `  value_set  ` is empty.
  - Returns `  NULL  ` if `  search_value  ` is `  NULL  ` .
  - Returns `  TRUE  ` if `  value_set  ` contains a value equal to `  search_value  ` .
  - Returns `  NULL  ` if `  value_set  ` contains a `  NULL  ` .
  - Returns `  FALSE  ` .

When using the `  NOT IN  ` operator, the following semantics apply in this order:

  - Returns `  TRUE  ` if `  value_set  ` is empty.
  - Returns `  NULL  ` if `  search_value  ` is `  NULL  ` .
  - Returns `  FALSE  ` if `  value_set  ` contains a value equal to `  search_value  ` .
  - Returns `  NULL  ` if `  value_set  ` contains a `  NULL  ` .
  - Returns `  TRUE  ` .

The semantics of:

``` text
x IN (y, z, ...)
```

are defined as equivalent to:

``` text
(x = y) OR (x = z) OR ...
```

and the subquery and array forms are defined similarly.

``` text
x NOT IN ...
```

is equivalent to:

``` text
NOT(x IN ...)
```

The `  UNNEST  ` form treats an array scan like `  UNNEST  ` in the [`  FROM  `](/bigquery/docs/reference/standard-sql/query-syntax#from_clause) clause:

``` text
x [NOT] IN UNNEST(<array expression>)
```

This form is often used with array parameters. For example:

``` text
x IN UNNEST(@array_parameter)
```

See the [Arrays](/bigquery/docs/arrays#filtering_arrays) topic for more information on how to use this syntax.

`  IN  ` can be used with multi-part keys by using the struct constructor syntax. For example:

``` text
(Key1, Key2) IN ( (12,34), (56,78) )
(Key1, Key2) IN ( SELECT (table.a, table.b) FROM table )
```

See the [Struct Type](/bigquery/docs/reference/standard-sql/data-types#struct_type) topic for more information.

**Return Data Type**

`  BOOL  `

**Examples**

You can use these `  WITH  ` clauses to emulate temporary tables for `  Words  ` and `  Items  ` in the following examples:

``` text
WITH Words AS (
  SELECT 'Intend' as value UNION ALL
  SELECT 'Secure' UNION ALL
  SELECT 'Clarity' UNION ALL
  SELECT 'Peace' UNION ALL
  SELECT 'Intend'
 )
SELECT * FROM Words;

/*----------+
 | value    |
 +----------+
 | Intend   |
 | Secure   |
 | Clarity  |
 | Peace    |
 | Intend   |
 +----------*/
```

``` text
WITH
  Items AS (
    SELECT STRUCT('blue' AS color, 'round' AS shape) AS info UNION ALL
    SELECT STRUCT('blue', 'square') UNION ALL
    SELECT STRUCT('red', 'round')
  )
SELECT * FROM Items;

/*----------------------------+
 | info                       |
 +----------------------------+
 | {blue color, round shape}  |
 | {blue color, square shape} |
 | {red color, round shape}   |
 +----------------------------*/
```

Example with `  IN  ` and an expression:

``` text
SELECT * FROM Words WHERE value IN ('Intend', 'Secure');

/*----------+
 | value    |
 +----------+
 | Intend   |
 | Secure   |
 | Intend   |
 +----------*/
```

Example with `  NOT IN  ` and an expression:

``` text
SELECT * FROM Words WHERE value NOT IN ('Intend');

/*----------+
 | value    |
 +----------+
 | Secure   |
 | Clarity  |
 | Peace    |
 +----------*/
```

Example with `  IN  ` , a scalar subquery, and an expression:

``` text
SELECT * FROM Words WHERE value IN ((SELECT 'Intend'), 'Clarity');

/*----------+
 | value    |
 +----------+
 | Intend   |
 | Clarity  |
 | Intend   |
 +----------*/
```

Example with `  IN  ` and an `  UNNEST  ` operation:

``` text
SELECT * FROM Words WHERE value IN UNNEST(['Secure', 'Clarity']);

/*----------+
 | value    |
 +----------+
 | Secure   |
 | Clarity  |
 +----------*/
```

Example with `  IN  ` and a struct:

``` text
SELECT
  (SELECT AS STRUCT Items.info) as item
FROM
  Items
WHERE (info.shape, info.color) IN (('round', 'blue'));

/*------------------------------------+
 | item                               |
 +------------------------------------+
 | { {blue color, round shape} info } |
 +------------------------------------*/
```

### `     IS    ` operators

IS operators return TRUE or FALSE for the condition they are testing. They never return `  NULL  ` , even for `  NULL  ` inputs, unlike the `  IS_INF  ` and `  IS_NAN  ` functions defined in [Mathematical Functions](/bigquery/docs/reference/standard-sql/mathematical_functions) . If `  NOT  ` is present, the output `  BOOL  ` value is inverted.

<table>
<thead>
<tr class="header">
<th>Function Syntax</th>
<th>Input Data Type</th>
<th>Result Data Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       X IS TRUE      </code></td>
<td><code dir="ltr" translate="no">       BOOL      </code></td>
<td><code dir="ltr" translate="no">       BOOL      </code></td>
<td>Evaluates to <code dir="ltr" translate="no">       TRUE      </code> if <code dir="ltr" translate="no">       X      </code> evaluates to <code dir="ltr" translate="no">       TRUE      </code> . Otherwise, evaluates to <code dir="ltr" translate="no">       FALSE      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       X IS NOT TRUE      </code></td>
<td><code dir="ltr" translate="no">       BOOL      </code></td>
<td><code dir="ltr" translate="no">       BOOL      </code></td>
<td>Evaluates to <code dir="ltr" translate="no">       FALSE      </code> if <code dir="ltr" translate="no">       X      </code> evaluates to <code dir="ltr" translate="no">       TRUE      </code> . Otherwise, evaluates to <code dir="ltr" translate="no">       TRUE      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       X IS FALSE      </code></td>
<td><code dir="ltr" translate="no">       BOOL      </code></td>
<td><code dir="ltr" translate="no">       BOOL      </code></td>
<td>Evaluates to <code dir="ltr" translate="no">       TRUE      </code> if <code dir="ltr" translate="no">       X      </code> evaluates to <code dir="ltr" translate="no">       FALSE      </code> . Otherwise, evaluates to <code dir="ltr" translate="no">       FALSE      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       X IS NOT FALSE      </code></td>
<td><code dir="ltr" translate="no">       BOOL      </code></td>
<td><code dir="ltr" translate="no">       BOOL      </code></td>
<td>Evaluates to <code dir="ltr" translate="no">       FALSE      </code> if <code dir="ltr" translate="no">       X      </code> evaluates to <code dir="ltr" translate="no">       FALSE      </code> . Otherwise, evaluates to <code dir="ltr" translate="no">       TRUE      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       X IS NULL      </code></td>
<td>Any value type</td>
<td><code dir="ltr" translate="no">       BOOL      </code></td>
<td>Evaluates to <code dir="ltr" translate="no">       TRUE      </code> if <code dir="ltr" translate="no">       X      </code> evaluates to <code dir="ltr" translate="no">       NULL      </code> . Otherwise evaluates to <code dir="ltr" translate="no">       FALSE      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       X IS NOT NULL      </code></td>
<td>Any value type</td>
<td><code dir="ltr" translate="no">       BOOL      </code></td>
<td>Evaluates to <code dir="ltr" translate="no">       FALSE      </code> if <code dir="ltr" translate="no">       X      </code> evaluates to <code dir="ltr" translate="no">       NULL      </code> . Otherwise evaluates to <code dir="ltr" translate="no">       TRUE      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       X IS UNKNOWN      </code></td>
<td><code dir="ltr" translate="no">       BOOL      </code></td>
<td><code dir="ltr" translate="no">       BOOL      </code></td>
<td>Evaluates to <code dir="ltr" translate="no">       TRUE      </code> if <code dir="ltr" translate="no">       X      </code> evaluates to <code dir="ltr" translate="no">       NULL      </code> . Otherwise evaluates to <code dir="ltr" translate="no">       FALSE      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       X IS NOT UNKNOWN      </code></td>
<td><code dir="ltr" translate="no">       BOOL      </code></td>
<td><code dir="ltr" translate="no">       BOOL      </code></td>
<td>Evaluates to <code dir="ltr" translate="no">       FALSE      </code> if <code dir="ltr" translate="no">       X      </code> evaluates to <code dir="ltr" translate="no">       NULL      </code> . Otherwise, evaluates to <code dir="ltr" translate="no">       TRUE      </code> .</td>
</tr>
</tbody>
</table>

### `     IS DISTINCT FROM    ` operator

``` text
expression_1 IS [NOT] DISTINCT FROM expression_2
```

**Description**

`  IS DISTINCT FROM  ` returns `  TRUE  ` if the input values are considered to be distinct from each other by the [`  DISTINCT  `](/bigquery/docs/reference/standard-sql/query-syntax#select_distinct) and [`  GROUP BY  `](/bigquery/docs/reference/standard-sql/query-syntax#group_by_clause) clauses. Otherwise, returns `  FALSE  ` .

`  a IS DISTINCT FROM b  ` being `  TRUE  ` is equivalent to:

  - `  SELECT COUNT(DISTINCT x) FROM UNNEST([a,b]) x  ` returning `  2  ` .
  - `  SELECT * FROM UNNEST([a,b]) x GROUP BY x  ` returning 2 rows.

`  a IS DISTINCT FROM b  ` is equivalent to `  NOT (a = b)  ` , except for the following cases:

  - This operator never returns `  NULL  ` so `  NULL  ` values are considered to be distinct from non- `  NULL  ` values, not other `  NULL  ` values.
  - `  NaN  ` values are considered to be distinct from non- `  NaN  ` values, but not other `  NaN  ` values.

You can use this operation with fields in a complex data type, but not on the complex data types themselves. These complex data types can't be compared directly:

  - `  STRUCT  `
  - `  ARRAY  `

Input values:

  - `  expression_1  ` : The first value to compare. This can be a groupable data type, `  NULL  ` or `  NaN  ` .
  - `  expression_2  ` : The second value to compare. This can be a groupable data type, `  NULL  ` or `  NaN  ` .
  - `  NOT  ` : If present, the output `  BOOL  ` value is inverted.

**Return type**

`  BOOL  `

**Examples**

These return `  TRUE  ` :

``` text
SELECT 1 IS DISTINCT FROM 2
```

``` text
SELECT 1 IS DISTINCT FROM NULL
```

``` text
SELECT 1 IS NOT DISTINCT FROM 1
```

``` text
SELECT NULL IS NOT DISTINCT FROM NULL
```

These return `  FALSE  ` :

``` text
SELECT NULL IS DISTINCT FROM NULL
```

``` text
SELECT 1 IS DISTINCT FROM 1
```

``` text
SELECT 1 IS NOT DISTINCT FROM 2
```

``` text
SELECT 1 IS NOT DISTINCT FROM NULL
```

### `     LIKE    ` operator

``` text
expression_1 [NOT] LIKE expression_2
```

**Description**

`  LIKE  ` returns `  TRUE  ` if the string in the first operand `  expression_1  ` matches a pattern specified by the second operand `  expression_2  ` , otherwise returns `  FALSE  ` .

`  NOT LIKE  ` returns `  TRUE  ` if the string in the first operand `  expression_1  ` doesn't match a pattern specified by the second operand `  expression_2  ` , otherwise returns `  FALSE  ` .

Expressions can contain these characters:

  - A percent sign ( `  %  ` ) matches any number of characters or bytes.
  - An underscore ( `  _  ` ) matches a single character or byte.
  - You can escape `  \  ` , `  _  ` , or `  %  ` using two backslashes. For example, `  \\%  ` . If you are using raw strings, only a single backslash is required. For example, `  r'\%'  ` .

This operator supports [collation](/bigquery/docs/reference/standard-sql/collation-concepts#collate_funcs) , but caveats apply:

  - Each `  %  ` character in `  expression_2  ` represents an *arbitrary string specifier* . An arbitrary string specifier can represent any sequence of `  0  ` or more characters.

  - A character in the expression represents itself and is considered a *single character specifier* unless:
    
      - The character is a percent sign ( `  %  ` ).
    
      - The character is an underscore ( `  _  ` ) and the collator isn't `  und:ci  ` .

  - These additional rules apply to the underscore ( `  _  ` ) character:
    
      - If the collator isn't `  und:ci  ` , an error is produced when an underscore isn't escaped in `  expression_2  ` .
    
      - If the collator isn't `  und:ci  ` , the underscore isn't allowed when the operands have collation specified.
    
      - Some *compatibility composites* , such as the fi-ligature ( `  ﬁ  ` ) and the telephone sign ( `  ℡  ` ), will produce a match if they are compared to an underscore.
    
      - A single underscore matches the idea of what a character is, based on an approximation known as a [*grapheme cluster*](https://www.unicode.org/reports/tr29/#Grapheme_Cluster_Boundaries) .

  - For a contiguous sequence of single character specifiers, equality depends on the collator and its language tags and tailoring.
    
      - By default, the `  und:ci  ` collator doesn't fully normalize a string. Some canonically equivalent strings are considered unequal for both the `  =  ` and `  LIKE  ` operators.
    
      - The `  LIKE  ` operator with collation has the same behavior as the `  =  ` operator when there are no wildcards in the strings.
    
      - Character sequences with secondary or higher-weighted differences are considered unequal. This includes accent differences and some special cases.
        
        For example there are three ways to produce German sharp `  ß  ` :
        
          - `  \u1E9E  `
          - `  \U00DF  `
          - `  ss  `
        
        `  \u1E9E  ` and `  \U00DF  ` are considered equal but differ in tertiary. They are considered equal with `  und:ci  ` collation but different from `  ss  ` , which has secondary differences.
    
      - Character sequences with tertiary or lower-weighted differences are considered equal. This includes case differences and kana subtype differences, which are considered equal.

  - There are [ignorable characters](https://www.unicode.org/charts/collation/chart_Ignored.html) defined in Unicode. Ignorable characters are ignored in the pattern matching.

**Return type**

`  BOOL  `

**Examples**

The following examples illustrate how you can check to see if the string in the first operand matches a pattern specified by the second operand.

``` text
-- Returns TRUE
SELECT 'apple' LIKE 'a%';
```

``` text
-- Returns FALSE
SELECT '%a' LIKE &#39;apple';
```

``` text
-- Returns FALSE
SELECT 'apple' NOT LIKE 'a%';
```

``` text
-- Returns TRUE
SELECT '%a' NOT LIKE &#39;apple';
```

``` text
-- Produces an error
SELECT NULL LIKE 'a%';
```

``` text
-- Produces an error
SELECT 'apple' LIKE NULL;
```

The following example illustrates how to search multiple patterns in an array to find a match with the `  LIKE  ` operator:

``` text
WITH Words AS
 (SELECT 'Intend with clarity.' as value UNION ALL
  SELECT 'Secure with intention.' UNION ALL
  SELECT 'Clarity and security.')
SELECT value
FROM Words WHERE
  EXISTS(
    SELECT value FROM UNNEST(['%ity%', '%and%']) AS pattern
    WHERE value LIKE pattern
  );

/*------------------------+
 | value                  |
 +------------------------+
 | Intend with clarity.   |
 | Clarity and security.  |
 +------------------------*/
```

The following examples illustrate how collation can be used with the `  LIKE  ` operator.

``` text
-- Returns FALSE
'Foo' LIKE '%foo%'
```

``` text
-- Returns TRUE
COLLATE('Foo', 'und:ci') LIKE COLLATE(';%foo%', 'und:ci');
```

``` text
-- Returns TRUE
COLLATE('Foo', 'und:ci') = COLLATE(&#39;foo', 'und:ci');
```

``` text
-- Produces an error
COLLATE('Foo', 'und:ci') LIKE COLLATE(';%foo%', 'binary');
```

``` text
-- Produces an error
COLLATE('Foo', 'und:ci') LIKE COLLATE(';%f_o%', 'und:ci');
```

``` text
-- Returns TRUE
COLLATE('Foo_', 'und:ci') LIKE COLLATE('%foo\\_%', 'und:ci');
```

There are two capital forms of `  ß  ` . We can use either `  SS  ` or `  ẞ  ` as upper case. While the difference between `  ß  ` and `  ẞ  ` is case difference (tertiary difference), the difference between sharp `  s  ` and `  ss  ` is secondary and considered not equal using the `  und:ci  ` collator. For example:

``` text
-- Returns FALSE
'MASSE' LIKE 'Maße';
```

``` text
-- Returns FALSE
COLLATE('MASSE', 'und:ci') LIKE '%Maße%';
```

``` text
-- Returns FALSE
COLLATE('MASSE', 'und:ci') = COLLATE(9;Maße', 'und:ci');
```

The kana differences in Japanese are considered as tertiary or quaternary differences, and should be considered as equal in the `  und:ci  ` collator with secondary strength.

  - `  '\u3042'  ` is `  'あ'  ` (hiragana)
  - `  '\u30A2'  ` is `  'ア'  ` (katakana)

For example:

``` text
-- Returns FALSE
'\u3042' LIKE ';%\u30A2%';
```

``` text
-- Returns TRUE
COLLATE('\u3042', 'und:ci') LIKE COLLATE('%\u30A2%', 'und:ci');
```

``` text
-- Returns TRUE
COLLATE('\u3042', 'und:ci') = COLLATE('\u30A2', 'und:ci');
```

When comparing two strings, the `  und:ci  ` collator compares the collation units based on the specification of the collation. Even though the number of code points is different, the two strings are considered equal when the collation units are considered the same.

  - `  '\u0041\u030A'  ` is `  'Å'  ` (two code points)
  - `  '\u0061\u030A'  ` is `  'å'  ` (two code points)
  - `  '\u00C5'  ` is `  'Å'  ` (one code point)

In the following examples, the difference between `  '\u0061\u030A'  ` and `  '\u00C5'  ` is tertiary.

``` text
-- Returns FALSE
'\u0061\u030A' LIKE ';%\u00C5%';
```

``` text
-- Returns TRUE
COLLATE('\u0061\u030A', 'und:ci') LIKE '%\u00C5%';
```

``` text
-- Returns TRUE
COLLATE('\u0061\u030A', 'und:ci') = COLLATE('\u00C5', 'und:ci');
```

In the following example, `  '\u0083'  ` is a `  NO BREAK HERE  ` character and is ignored.

``` text
-- Returns FALSE
'\u0083' LIKE '';
```

``` text
-- Returns TRUE
COLLATE('\u0083', 'und:ci') LIKE '';
```

### Quantified `     LIKE    ` operator

The quantified `  LIKE  ` operator supports the following syntax:

``` text
search_value [NOT] LIKE quantifier patterns

quantifier:
 { ANY | SOME | ALL }

patterns:
  {
    (expression[, ...])
    UNNEST(array_expression)
  }
```

**Description**

Checks `  search_value  ` for matches against several patterns. Each comparison is case-sensitive. Wildcard searches are supported. [Semantic rules](#semantic_rules_quant_like) apply, but in general, `  LIKE  ` returns `  TRUE  ` if a matching pattern is found, `  FALSE  ` if a matching pattern isn't found, or otherwise `  NULL  ` . `  NOT LIKE  ` returns `  FALSE  ` if a matching pattern is found, `  TRUE  ` if a matching pattern isn't found, or otherwise `  NULL  ` .

  - `  search_value  ` : The value to search for matching patterns. This value can be a `  STRING  ` or `  BYTES  ` type.

  - `  patterns  ` : The patterns to look for in the search value. Each pattern must resolve to the same type as `  search_value  ` . Each pattern is one of the following:
    
      - A list of one or more patterns that match the `  search_value  ` type.
    
      - An [`  UNNEST  `](/bigquery/docs/reference/standard-sql/query-syntax#unnest_operator) operation that returns a column of values with the same type as `  search_value  ` from an array expression.
    
    The regular expressions that are supported by the [`  LIKE  ` operator](#like_operator) are also supported by `  patterns  ` in the [quantified `  LIKE  ` operator](#like_operator) .

  - `  quantifier  ` : Condition for pattern matching.
    
      - `  ANY  ` : Checks if the set of patterns contains at least one pattern that matches the search value.
    
      - `  SOME  ` : Synonym for `  ANY  ` .
    
      - `  ALL  ` : Checks if every pattern in the set of patterns matches the search value.

**Collation caveats**

[Collation](/bigquery/docs/reference/standard-sql/collation-concepts#collate_funcs) is supported, but with the following caveats:

  - The collation caveats that apply to the [`  LIKE  ` operator](#like_operator) also apply to the quantified `  LIKE  ` operator.
  - If a collation-supported input contains no collation specification or an empty collation specification and another input contains an explicitly defined collation, the explicitly defined collation is used for all of the inputs.
  - All inputs with a non-empty, explicitly defined collation specification must have the same type of collation specification, otherwise an error is thrown.

**Semantics rules**

When using the quantified `  LIKE  ` operator with `  ANY  ` or `  SOME  ` , the following semantics apply in this order:

1.  Returns `  FALSE  ` if `  patterns  ` is empty.
2.  Returns `  NULL  ` if `  search_value  ` is `  NULL  ` .
3.  Returns `  TRUE  ` `  search_value LIKE pattern  ` is `  TRUE  ` for at least one value in `  patterns  ` .
4.  Returns `  NULL  ` if a pattern in `  patterns  ` is `  NULL  ` .
5.  Returns `  FALSE  ` .

When using the quantified `  LIKE  ` operator with `  ALL  ` , the following semantics apply in this order:

1.  Returns `  TRUE  ` if `  patterns  ` is empty.
2.  Returns `  NULL  ` if `  search_value  ` is `  NULL  ` .
3.  Returns `  FALSE  ` if `  search_value LIKE pattern  ` is `  FALSE  ` for at least one value in `  patterns  ` .
4.  Returns `  NULL  ` if a pattern in `  patterns  ` is `  NULL  ` .
5.  Returns `  TRUE  ` .

When using the quantified `  NOT LIKE  ` operator with `  ANY  ` or `  SOME  ` , the following semantics apply in this order:

1.  Returns `  FALSE  ` if `  patterns  ` is empty.
2.  Returns `  NULL  ` if `  search_value  ` is `  NULL  ` .
3.  Returns `  TRUE  ` if `  search_value LIKE pattern  ` is `  FALSE  ` for at least one value in `  patterns  ` .
4.  Returns `  NULL  ` if a pattern in `  patterns  ` is `  NULL  ` .
5.  Returns `  FALSE  ` .

When using the quantified `  NOT LIKE  ` operator with `  ALL  ` , the following semantics apply in this order:

1.  Returns `  TRUE  ` if `  patterns  ` is empty.
2.  For `  pattern_array  ` , returns `  TRUE  ` if `  patterns  ` is empty.
3.  Returns `  NULL  ` if `  search_value  ` is `  NULL  ` .
4.  Returns `  FALSE  ` if `  search_value LIKE pattern  ` is `  TRUE  ` for at least one value in `  patterns  ` .
5.  Returns `  NULL  ` if a pattern in `  patterns  ` is `  NULL  ` .
6.  Returns `  TRUE  ` .

**Return Data Type**

`  BOOL  `

**Examples**

You can use these `  WITH  ` clauses to emulate temporary tables for `  Words  ` in the following examples:

``` text
WITH Words AS
 (SELECT 'Intend with clarity.' as value UNION ALL
  SELECT 'Secure with intention.' UNION ALL
  SELECT 'Clarity and security.')

/*------------------------+
 | value                  |
 +------------------------+
 | Intend with clarity.   |
 | Secure with intention. |
 | Clarity and security.  |
 +------------------------*/
```

The following example checks to see if the `  Intend%  ` or `  %intention%  ` pattern exists in a value and produces that value if either pattern is found:

``` text
SELECT * FROM Words WHERE value LIKE ANY ('Intend%', '%intention%');

/*------------------------+
 | value                  |
 +------------------------+
 | Intend with clarity.   |
 | Secure with intention. |
 +------------------------*/
```

The following example checks to see if the `  %ity%  ` pattern exists in a value and produces that value if the pattern is found.

Example with `  LIKE ALL  ` :

``` text
SELECT * FROM Words WHERE value LIKE ALL ('%ity%');

/*-----------------------+
 | value                 |
 +-----------------------+
 | Intend with clarity.  |
 | Clarity and security. |
 +-----------------------*/
```

The following example checks to see if the `  %ity%  ` pattern exists in a value produces that value if the pattern isn't found:

``` text
SELECT * FROM Words WHERE value NOT LIKE ('%ity%');

/*------------------------+
 | value                  |
 +------------------------+
 | Secure with intention. |
 +------------------------*/
```

You can pass in an array for `  patterns  ` . For example:

``` text
SELECT * FROM Words WHERE value LIKE ANY UNNEST(['%ion%', '%and%']);

/*------------------------+
 | value                  |
 +------------------------+
 | Secure with intention. |
 | Clarity and security.  |
 +------------------------*/
```

The following queries illustrate some of the semantic rules for the quantified `  LIKE  ` operator:

``` text
SELECT
  NULL LIKE ANY ('a', 'b'), -- NULL
  'a' LIKE ANY ('a', 'c'), -- TRUE
  'a' LIKE ANY ('b', 'c'), -- FALSE
  'a' LIKE ANY ('a', NULL), -- TRUE
  'a' LIKE ANY ('b', NULL), -- NULL
  NULL NOT LIKE ANY ('a', 'b'), -- NULL
  'a' NOT LIKE ANY ('a', 'b&#39;), -- TRUE
  'a' NOT LIKE ANY ('a', '%a%'), -- FALSE
  'a' NOT LIKE ANY ('a', NULL), -- NULL
  'a' NOT LIKE ANY ('b', NULL); -- TRUE
```

``` text
SELECT
  NULL LIKE SOME ('a', 'b'), -- NULL
  'a' LIKE SOME ('a', 'c'), -- TRUE
  'a' LIKE SOME ('b', 'c'), -- FALSE
  'a' LIKE SOME ('a', NULL), -- TRUE
  'a' LIKE SOME ('b', NULL), -- NULL
  NULL NOT LIKE SOME ('a', 'b'), -- NULL
  'a' NOT LIKE SOME ('a', 'b'), -- TRUE
  'a' NOT LIKE SOME ('a', '%a%'), -- FALSE
  'a' NOT LIKE SOME ('a', NULL), -- NULL
  'a' NOT LIKE SOME ('b', NULL); -- TRUE
```

``` text
SELECT
  NULL LIKE ALL ('a', 'b'), -- NULL
  'a' LIKE ALL ('a', '%a%'), -- TRUE
  'a' LIKE ALL ('a', 'c'), -- FALSE
  'a' LIKE ALL ('a', NULL), -- NULL
  'a' LIKE ALL ('b', NULL), -- FALSE
  NULL NOT LIKE ALL ('a', 'b'), -- NULL
  'a' NOT LIKE ALL ('b', 'c&#39;), -- TRUE
  'a' NOT LIKE ALL ('a', 'c'), -- FALSE
  'a' NOT LIKE ALL ('a', NULL), -- FALSE
  'a' NOT LIKE ALL ('b', NULL); -- NULL
```

The following queries illustrate some of the semantic rules for the quantified `  LIKE  ` operator and collation:

``` text
SELECT
  COLLATE('a', 'und:ci') LIKE ALL ('a', 'A'), -- TRUE
  'a' LIKE ALL (COLLATE('a', 'und:ci'), 'A'), -- TRUE
  'a' LIKE ALL ('%A%', COLLATE('a', 'und:ci')); -- TRUE
```

``` text
-- ERROR: BYTES and STRING values can't be used together.
SELECT b'a' LIKE ALL (COLLATE('a';, 'und:ci'), 'A');
```

### Concatenation operator

The concatenation operator combines multiple values into one.

<table>
<thead>
<tr class="header">
<th>Function Syntax</th>
<th>Input Data Type</th>
<th>Result Data Type</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       STRING || STRING [ || ... ]      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       BYTES || BYTES [ || ... ]      </code></td>
<td><code dir="ltr" translate="no">       BYTES      </code></td>
<td><code dir="ltr" translate="no">       BYTES      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       ARRAY&lt;T&gt; || ARRAY&lt;T&gt; [ || ... ]      </code></td>
<td><code dir="ltr" translate="no">       ARRAY&lt;T&gt;      </code></td>
<td><code dir="ltr" translate="no">       ARRAY&lt;T&gt;      </code></td>
</tr>
</tbody>
</table>

**Note:** The concatenation operator is translated into a nested [`  CONCAT  `](/bigquery/docs/reference/standard-sql/string_functions#concat) function call. For example, `  'A' || 'B' || 'C'  ` becomes `  CONCAT('A', CONCAT('B', 'C'))  ` .

### `     WITH    ` expression

``` text
WITH(variable_assignment[, ...], result_expression)

variable_assignment:
  variable_name AS expression
```

**Description**

Creates one or more variables. Each variable can be used in subsequent expressions within the `  WITH  ` expression. Returns the value of `  result_expression  ` .

  - `  variable_assignment  ` : Introduces a variable. The variable name must be unique within a given `  WITH  ` expression. Each expression can reference the variables that come before it. For example, if you create variable `  a  ` , then follow it with variable `  b  ` , then you can reference `  a  ` inside of the expression for `  b  ` .
    
      - `  variable_name  ` : The name of the variable.
    
      - `  expression  ` : The value to assign to the variable.

  - `  result_expression  ` : An expression that can use all of the variables defined before it. The value of `  result_expression  ` is returned by the `  WITH  ` expression.

**Return Type**

  - The type of the `  result_expression  ` .

**Requirements and Caveats**

  - A variable can only be assigned once within a `  WITH  ` expression.
  - Variables created during `  WITH  ` may not be used in analytic or aggregate function arguments. For example, `  WITH(a AS ..., SUM(a))  ` produces an error.
  - Each variable's expression is evaluated only once.

**Examples**

The following example first concatenates variable `  a  ` with `  b  ` , then variable `  b  ` with `  c  ` :

``` text
SELECT WITH(a AS '123',               -- a is '123'
            b AS CONCAT(a, '456'),    -- b is '123456'
            c AS '789',               -- c is '789'
            CONCAT(b, c)) AS result;  -- b + c is '123456789'

/*-------------+
 | result      |
 +-------------+
 | '123456789' |
 +-------------*/
```

In the following example, the volatile expression `  RAND()  ` is evaluated once. The value of the result expression is always `  0.0  ` :

``` text
SELECT WITH(a AS RAND(), a - a);

/*---------+
 | result  |
 +---------+
 | 0.0     |
 +---------*/
```

Aggregate or analytic function results can be stored in variables.

``` text
SELECT WITH(s AS SUM(input), c AS COUNT(input), s/c)
FROM UNNEST([1.0, 2.0, 3.0]) AS input;

/*---------+
 | result  |
 +---------+
 | 2.0     |
 +---------*/
```

Variables can't be used in aggregate or analytic function call arguments.

``` text
SELECT WITH(diff AS a - b, AVG(diff))
FROM UNNEST([
              STRUCT(1 AS a, 2 AS b),
              STRUCT(3 AS a, 4 AS b),
              STRUCT(5 AS a, 6 AS b)
            ]);

-- ERROR: WITH variables like 'diff' can't be used in aggregate or analytic
-- function arguments.
```

A `  WITH  ` expression is different from a `  WITH  ` clause. The following example shows a query that uses both:

``` text
WITH my_table AS (
  SELECT 1 AS x, 2 AS y
  UNION ALL
  SELECT 3 AS x, 4 AS y
  UNION ALL
  SELECT 5 AS x, 6 AS y
)
SELECT WITH(a AS SUM(x), b AS COUNT(x), a/b) AS avg_x, AVG(y) AS avg_y
FROM my_table
WHERE x > 1;

/*-------+-------+
 | avg_x | avg_y |
 +-------+-------+
 | 4     | 5     |
 +-------+-------*/
```
