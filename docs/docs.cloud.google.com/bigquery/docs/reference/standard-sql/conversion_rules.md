---
name: documents/docs.cloud.google.com/bigquery/docs/reference/standard-sql/conversion_rules
uri: https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/conversion_rules
title: Conversion rules
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

GoogleSQL for BigQuery supports conversion. Conversion includes, but isn't limited to, casting, coercion, and supertyping.

- Casting is explicit conversion and uses the [`CAST()`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/conversion_functions#cast) function.
- Coercion is implicit conversion, which GoogleSQL performs automatically under the conditions described below.
- A supertype is a common type to which two or more expressions can be coerced.

There are also conversions that have their own function names, such as `PARSE_DATE()` . To learn more about these functions, see [Conversion functions](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/conversion_functions) .

### Comparison of casting and coercion

The following table summarizes all possible cast and coercion possibilities for GoogleSQL data types. The *Coerce to* column applies to all expressions of a given data type, (for example, a column), but literals and parameters can also be coerced. See [literal coercion](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/conversion_rules#literal_coercion) and [query parameter coercion](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/conversion_rules#parameter_coercion) for details.

| From type    | Cast to                                                                                                       | Coerce to                        |
|--------------|---------------------------------------------------------------------------------------------------------------|----------------------------------|
| `INT64`      | `BOOL` `INT64` `NUMERIC` `BIGNUMERIC` `FLOAT64` `STRING`                                                      | `NUMERIC` `BIGNUMERIC` `FLOAT64` |
| `NUMERIC`    | `INT64` `NUMERIC` `BIGNUMERIC` `FLOAT64` `STRING`                                                             | `BIGNUMERIC` `FLOAT64`           |
| `BIGNUMERIC` | `INT64` `NUMERIC` `BIGNUMERIC` `FLOAT64` `STRING`                                                             | `FLOAT64`                        |
| `FLOAT64`    | `INT64` `NUMERIC` `BIGNUMERIC` `FLOAT64` `STRING`                                                             |                                  |
| `BOOL`       | `BOOL` `INT64` `STRING`                                                                                       |                                  |
| `STRING`     | `BOOL` `INT64` `NUMERIC` `BIGNUMERIC` `FLOAT64` `STRING` `BYTES` `DATE` `DATETIME` `TIME` `TIMESTAMP` `RANGE` |                                  |
| `BYTES`      | `STRING` `BYTES`                                                                                              |                                  |
| `DATE`       | `STRING` `DATE` `DATETIME` `TIMESTAMP`                                                                        | `DATETIME`                       |
| `DATETIME`   | `STRING` `DATE` `DATETIME` `TIME` `TIMESTAMP`                                                                 |                                  |
| `TIME`       | `STRING` `TIME`                                                                                               |                                  |
| `TIMESTAMP`  | `STRING` `DATE` `DATETIME` `TIME` `TIMESTAMP`                                                                 |                                  |
| `ARRAY`      | `ARRAY`                                                                                                       |                                  |
| `STRUCT`     | `STRUCT`                                                                                                      |                                  |
| `RANGE`      | `RANGE` `STRING`                                                                                              |                                  |

### Casting

Most data types can be cast from one type to another with the `CAST` function. When using `CAST` , a query can fail if GoogleSQL is unable to perform the cast. If you want to protect your queries from these types of errors, you can use `SAFE_CAST` . To learn more about the rules for `CAST` , `SAFE_CAST` and other casting functions, see [Conversion functions](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/conversion_functions) .

### Coercion

GoogleSQL coerces the result type of an argument expression to another type if needed to match function signatures. For example, if function `func()` is defined to take a single argument of type `FLOAT64` and an expression is used as an argument that has a result type of `INT64` , then the result of the expression will be coerced to `FLOAT64` type before `func()` is computed.

#### Literal coercion

GoogleSQL supports the following literal coercions:

| Input data type   | Result data type                     | Notes                                                 |
|-------------------|--------------------------------------|-------------------------------------------------------|
| `FLOAT64` literal | `NUMERIC`                            | Coercion may not be exact, and returns a close value. |
| `STRING` literal  | `DATE` `DATETIME` `TIME` `TIMESTAMP` |                                                       |

Literal coercion is needed when the actual literal type is different from the type expected by the function in question. For example, if function `func()` takes a DATE argument, then the expression `func("2014-09-27")` is valid because the string literal `"2014-09-27"` is coerced to `DATE` .

Literal conversion is evaluated at analysis time, and gives an error if the input literal can't be converted successfully to the target type.

> **Note:** String literals don't coerce to numeric types.

#### Query parameter coercion

GoogleSQL supports the following query parameter coercions:

| Input data type    | Result data type                     |
|--------------------|--------------------------------------|
| `STRING parameter` | `DATE` `DATETIME` `TIME` `TIMESTAMP` |

If the parameter value can't be coerced successfully to the target type, an error is provided.

### Supertypes

A supertype is a common type to which two or more expressions can be coerced. Supertypes are used with set operations such as `UNION ALL` and expressions such as `CASE` that expect multiple arguments with matching types. Each type has one or more supertypes, including itself, which defines its set of supertypes.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Input type</th>
<th>Supertypes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>BOOL</code></td>
<td><code>BOOL</code><br />
</td>
</tr>
<tr class="even">
<td><code>INT64</code></td>
<td><code>INT64</code><br />
<code>FLOAT64</code><br />
<code>NUMERIC</code><br />
<code>BIGNUMERIC</code><br />
</td>
</tr>
<tr class="odd">
<td><code>FLOAT64</code></td>
<td><code>FLOAT64</code><br />
</td>
</tr>
<tr class="even">
<td><code>NUMERIC</code></td>
<td><code>NUMERIC</code><br />
<code>BIGNUMERIC</code><br />
<code>FLOAT64</code><br />
</td>
</tr>
<tr class="odd">
<td><code>DECIMAL</code></td>
<td><code>DECIMAL</code><br />
<code>BIGDECIMAL</code><br />
<code>FLOAT64</code><br />
</td>
</tr>
<tr class="even">
<td><code>BIGNUMERIC</code></td>
<td><code>BIGNUMERIC</code><br />
<code>FLOAT64</code><br />
</td>
</tr>
<tr class="odd">
<td><code>BIGDECIMAL</code></td>
<td><code>BIGDECIMAL</code><br />
<code>FLOAT64</code><br />
</td>
</tr>
<tr class="even">
<td><code>STRING</code></td>
<td><code>STRING</code><br />
</td>
</tr>
<tr class="odd">
<td><code>DATE</code></td>
<td><code>DATE</code><br />
</td>
</tr>
<tr class="even">
<td><code>TIME</code></td>
<td><code>TIME</code><br />
</td>
</tr>
<tr class="odd">
<td><code>DATETIME</code></td>
<td><code>DATETIME</code><br />
</td>
</tr>
<tr class="even">
<td><code>TIMESTAMP</code></td>
<td><code>TIMESTAMP</code><br />
</td>
</tr>
<tr class="odd">
<td><code>BYTES</code></td>
<td><code>BYTES</code><br />
</td>
</tr>
<tr class="even">
<td><code>STRUCT</code></td>
<td><code>STRUCT</code> with the same field position types.</td>
</tr>
<tr class="odd">
<td><code>ARRAY</code></td>
<td><code>ARRAY</code> with the same element types.</td>
</tr>
<tr class="even">
<td><code>GEOGRAPHY</code></td>
<td><code>GEOGRAPHY</code><br />
</td>
</tr>
<tr class="odd">
<td><code>GRAPH_ELEMENT</code></td>
<td><code>GRAPH_ELEMENT</code> . Graph element <code>a</code> is a supertype of graph element <code>b</code> if the following are true:
<ul>
<li>Graph element <code>a</code> and <code>b</code> are the same element kind.</li>
<li>Graph element <code>a</code> 's property type list is a compatible superset of graph element <code>b</code> 's property type list. This means that properties with the same name must also have the same type.</li>
</ul></td>
</tr>
<tr class="even">
<td><code>GRAPH_PATH</code></td>
<td><code>GRAPH_PATH</code> . Graph path <code>a</code> is a supertype of graph path <code>b</code> if the following are true:
<ul>
<li>The node type for <code>a</code> is a supertype of the node type for <code>b</code> .</li>
<li>The edge type for <code>a</code> is a supertype of the edge type for <code>b</code> .</li>
<li>Graph path <code>a</code> 's property type list is a compatible superset of graph path <code>b</code> 's property type list. This means that properties with the same name must also have the same type.</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>RANGE</code></td>
<td><code>RANGE</code> with the same subtype.</td>
</tr>
</tbody>
</table>

If you want to find the supertype for a set of input types, first determine the intersection of the set of supertypes for each input type. If that set is empty then the input types have no common supertype. If that set is non-empty, then the common supertype is generally the [most specific](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/conversion_rules#supertype_specificity) type in that set. Generally, the most specific type is the type with the most restrictive domain.

**Examples**

| Input types       | Common supertype | Returns   | Notes                                                                                                                     |
|-------------------|------------------|-----------|---------------------------------------------------------------------------------------------------------------------------|
| `INT64` `FLOAT64` | `FLOAT64`        | `FLOAT64` | If you apply supertyping to `INT64` and `FLOAT64` , supertyping succeeds because they they share a supertype, `FLOAT64` . |
| `INT64` `BOOL`    | None             | Error     | If you apply supertyping to `INT64` and `BOOL` , supertyping fails because they don't share a common supertype.           |

#### Exact and inexact types

Numeric types can be exact or inexact. For supertyping, if all of the input types are exact types, then the resulting supertype can only be an exact type.

The following table contains a list of exact and inexact numeric data types.

| Exact types                    | Inexact types |
|--------------------------------|---------------|
| `INT64` `NUMERIC` `BIGNUMERIC` | `FLOAT64`     |

**Examples**

| Input types       | Common supertype | Returns   | Notes                                                                                                                                         |
|-------------------|------------------|-----------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| `INT64` `FLOAT64` | `FLOAT64`        | `FLOAT64` | If supertyping is applied to `INT64` and `FLOAT64` , supertyping succeeds because there are exact and inexact numeric types being supertyped. |

#### Types specificity

Each type has a domain of values that it supports. A type with a narrow domain is more specific than a type with a wider domain. Exact types are more specific than inexact types because inexact types have a wider range of domain values that are supported than exact types. For example, `INT64` is more specific than `FLOAT64` .

#### Supertypes and literals

Supertype rules for literals are more permissive than for normal expressions, and are consistent with implicit coercion rules. The following algorithm is used when the input set of types includes types related to literals:

- If there exists non-literals in the set, find the set of common supertypes of the non-literals.
- If there is at least one possible supertype, find the [most specific](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/conversion_rules#supertype_specificity) type to which the remaining literal types can be implicitly coerced and return that supertype. Otherwise, there is no supertype.
- If the set only contains types related to literals, compute the supertype of the literal types.
- If all input types are related to `NULL` literals, then the resulting supertype is `INT64` .
- If no common supertype is found, an error is produced.

**Examples**

| Input types                             | Common supertype | Returns     |
|-----------------------------------------|------------------|-------------|
| `INT64` literal `UINT64` expression     | `UINT64`         | `UINT64`    |
| `TIMESTAMP` expression `STRING` literal | `TIMESTAMP`      | `TIMESTAMP` |
| `NULL` literal `NULL` literal           | `INT64`          | `INT64`     |
| `BOOL` literal `TIMESTAMP` literal      | None             | Error       |
