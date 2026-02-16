GoogleSQL for BigQuery supports conversion. Conversion includes, but isn't limited to, casting, coercion, and supertyping.

  - Casting is explicit conversion and uses the [`  CAST()  `](/bigquery/docs/reference/standard-sql/conversion_functions#cast) function.
  - Coercion is implicit conversion, which GoogleSQL performs automatically under the conditions described below.
  - A supertype is a common type to which two or more expressions can be coerced.

There are also conversions that have their own function names, such as `  PARSE_DATE()  ` . To learn more about these functions, see [Conversion functions](/bigquery/docs/reference/standard-sql/conversion_functions) .

### Comparison of casting and coercion

The following table summarizes all possible cast and coercion possibilities for GoogleSQL data types. The *Coerce to* column applies to all expressions of a given data type, (for example, a column), but literals and parameters can also be coerced. See [literal coercion](#literal_coercion) and [query parameter coercion](#parameter_coercion) for details.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>From type</th>
<th>Cast to</th>
<th>Coerce to</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td><code dir="ltr" translate="no">        BOOL       </code><br />
<code dir="ltr" translate="no">        INT64       </code><br />
<code dir="ltr" translate="no">        NUMERIC       </code><br />
<code dir="ltr" translate="no">        BIGNUMERIC       </code><br />
<code dir="ltr" translate="no">        FLOAT64       </code><br />
<code dir="ltr" translate="no">        STRING       </code><br />
</td>
<td><code dir="ltr" translate="no">        NUMERIC       </code><br />
<code dir="ltr" translate="no">        BIGNUMERIC       </code><br />
<code dir="ltr" translate="no">        FLOAT64       </code><br />
</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td><code dir="ltr" translate="no">        INT64       </code><br />
<code dir="ltr" translate="no">        NUMERIC       </code><br />
<code dir="ltr" translate="no">        BIGNUMERIC       </code><br />
<code dir="ltr" translate="no">        FLOAT64       </code><br />
<code dir="ltr" translate="no">        STRING       </code><br />
</td>
<td><code dir="ltr" translate="no">        BIGNUMERIC       </code><br />
<code dir="ltr" translate="no">        FLOAT64       </code><br />
</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
<td><code dir="ltr" translate="no">        INT64       </code><br />
<code dir="ltr" translate="no">        NUMERIC       </code><br />
<code dir="ltr" translate="no">        BIGNUMERIC       </code><br />
<code dir="ltr" translate="no">        FLOAT64       </code><br />
<code dir="ltr" translate="no">        STRING       </code><br />
</td>
<td><code dir="ltr" translate="no">        FLOAT64       </code><br />
</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
<td><code dir="ltr" translate="no">        INT64       </code><br />
<code dir="ltr" translate="no">        NUMERIC       </code><br />
<code dir="ltr" translate="no">        BIGNUMERIC       </code><br />
<code dir="ltr" translate="no">        FLOAT64       </code><br />
<code dir="ltr" translate="no">        STRING       </code><br />
</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       BOOL      </code></td>
<td><code dir="ltr" translate="no">        BOOL       </code><br />
<code dir="ltr" translate="no">        INT64       </code><br />
<code dir="ltr" translate="no">        STRING       </code><br />
</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><code dir="ltr" translate="no">        BOOL       </code><br />
<code dir="ltr" translate="no">        INT64       </code><br />
<code dir="ltr" translate="no">        NUMERIC       </code><br />
<code dir="ltr" translate="no">        BIGNUMERIC       </code><br />
<code dir="ltr" translate="no">        FLOAT64       </code><br />
<code dir="ltr" translate="no">        STRING       </code><br />
<code dir="ltr" translate="no">        BYTES       </code><br />
<code dir="ltr" translate="no">        DATE       </code><br />
<code dir="ltr" translate="no">        DATETIME       </code><br />
<code dir="ltr" translate="no">        TIME       </code><br />
<code dir="ltr" translate="no">        TIMESTAMP       </code><br />
<code dir="ltr" translate="no">        RANGE       </code><br />
</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       BYTES      </code></td>
<td><code dir="ltr" translate="no">        STRING       </code><br />
<code dir="ltr" translate="no">        BYTES       </code><br />
</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       DATE      </code></td>
<td><code dir="ltr" translate="no">        STRING       </code><br />
<code dir="ltr" translate="no">        DATE       </code><br />
<code dir="ltr" translate="no">        DATETIME       </code><br />
<code dir="ltr" translate="no">        TIMESTAMP       </code><br />
</td>
<td><code dir="ltr" translate="no">        DATETIME       </code><br />
</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       DATETIME      </code></td>
<td><code dir="ltr" translate="no">        STRING       </code><br />
<code dir="ltr" translate="no">        DATE       </code><br />
<code dir="ltr" translate="no">        DATETIME       </code><br />
<code dir="ltr" translate="no">        TIME       </code><br />
<code dir="ltr" translate="no">        TIMESTAMP       </code><br />
</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       TIME      </code></td>
<td><code dir="ltr" translate="no">        STRING       </code><br />
<code dir="ltr" translate="no">        TIME       </code><br />
</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td><code dir="ltr" translate="no">        STRING       </code><br />
<code dir="ltr" translate="no">        DATE       </code><br />
<code dir="ltr" translate="no">        DATETIME       </code><br />
<code dir="ltr" translate="no">        TIME       </code><br />
<code dir="ltr" translate="no">        TIMESTAMP       </code><br />
</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ARRAY      </code></td>
<td><code dir="ltr" translate="no">        ARRAY       </code><br />
</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       STRUCT      </code></td>
<td><code dir="ltr" translate="no">        STRUCT       </code><br />
</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       RANGE      </code></td>
<td><code dir="ltr" translate="no">        RANGE       </code><br />
<code dir="ltr" translate="no">        STRING       </code><br />
</td>
<td></td>
</tr>
</tbody>
</table>

### Casting

Most data types can be cast from one type to another with the `  CAST  ` function. When using `  CAST  ` , a query can fail if GoogleSQL is unable to perform the cast. If you want to protect your queries from these types of errors, you can use `  SAFE_CAST  ` . To learn more about the rules for `  CAST  ` , `  SAFE_CAST  ` and other casting functions, see [Conversion functions](/bigquery/docs/reference/standard-sql/conversion_functions) .

### Coercion

GoogleSQL coerces the result type of an argument expression to another type if needed to match function signatures. For example, if function `  func()  ` is defined to take a single argument of type `  FLOAT64  ` and an expression is used as an argument that has a result type of `  INT64  ` , then the result of the expression will be coerced to `  FLOAT64  ` type before `  func()  ` is computed.

#### Literal coercion

GoogleSQL supports the following literal coercions:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Input data type</th>
<th>Result data type</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       FLOAT64      </code> literal</td>
<td><code dir="ltr" translate="no">        NUMERIC       </code><br />
</td>
<td>Coercion may not be exact, and returns a close value.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       STRING      </code> literal</td>
<td><code dir="ltr" translate="no">        DATE       </code><br />
<code dir="ltr" translate="no">        DATETIME       </code><br />
<code dir="ltr" translate="no">        TIME       </code><br />
<code dir="ltr" translate="no">        TIMESTAMP       </code><br />
</td>
<td></td>
</tr>
</tbody>
</table>

Literal coercion is needed when the actual literal type is different from the type expected by the function in question. For example, if function `  func()  ` takes a DATE argument, then the expression `  func("2014-09-27")  ` is valid because the string literal `  "2014-09-27"  ` is coerced to `  DATE  ` .

Literal conversion is evaluated at analysis time, and gives an error if the input literal can't be converted successfully to the target type.

**Note:** String literals don't coerce to numeric types.

#### Query parameter coercion

GoogleSQL supports the following query parameter coercions:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Input data type</th>
<th>Result data type</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       STRING parameter      </code></td>
<td><code dir="ltr" translate="no">        DATE       </code><br />
<code dir="ltr" translate="no">        DATETIME       </code><br />
<code dir="ltr" translate="no">        TIME       </code><br />
<code dir="ltr" translate="no">        TIMESTAMP       </code><br />
</td>
</tr>
</tbody>
</table>

If the parameter value can't be coerced successfully to the target type, an error is provided.

### Supertypes

A supertype is a common type to which two or more expressions can be coerced. Supertypes are used with set operations such as `  UNION ALL  ` and expressions such as `  CASE  ` that expect multiple arguments with matching types. Each type has one or more supertypes, including itself, which defines its set of supertypes.

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
<td><code dir="ltr" translate="no">       BOOL      </code></td>
<td><code dir="ltr" translate="no">        BOOL       </code><br />
</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td><code dir="ltr" translate="no">        INT64       </code><br />
<code dir="ltr" translate="no">        FLOAT64       </code><br />
<code dir="ltr" translate="no">        NUMERIC       </code><br />
<code dir="ltr" translate="no">        BIGNUMERIC       </code><br />
</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
<td><code dir="ltr" translate="no">        FLOAT64       </code><br />
</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td><code dir="ltr" translate="no">        NUMERIC       </code><br />
<code dir="ltr" translate="no">        BIGNUMERIC       </code><br />
<code dir="ltr" translate="no">        FLOAT64       </code><br />
</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       DECIMAL      </code></td>
<td><code dir="ltr" translate="no">        DECIMAL       </code><br />
<code dir="ltr" translate="no">        BIGDECIMAL       </code><br />
<code dir="ltr" translate="no">        FLOAT64       </code><br />
</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
<td><code dir="ltr" translate="no">        BIGNUMERIC       </code><br />
<code dir="ltr" translate="no">        FLOAT64       </code><br />
</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       BIGDECIMAL      </code></td>
<td><code dir="ltr" translate="no">        BIGDECIMAL       </code><br />
<code dir="ltr" translate="no">        FLOAT64       </code><br />
</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><code dir="ltr" translate="no">        STRING       </code><br />
</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       DATE      </code></td>
<td><code dir="ltr" translate="no">        DATE       </code><br />
</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       TIME      </code></td>
<td><code dir="ltr" translate="no">        TIME       </code><br />
</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       DATETIME      </code></td>
<td><code dir="ltr" translate="no">        DATETIME       </code><br />
</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td><code dir="ltr" translate="no">        TIMESTAMP       </code><br />
</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       BYTES      </code></td>
<td><code dir="ltr" translate="no">        BYTES       </code><br />
</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       STRUCT      </code></td>
<td><code dir="ltr" translate="no">       STRUCT      </code> with the same field position types.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       ARRAY      </code></td>
<td><code dir="ltr" translate="no">       ARRAY      </code> with the same element types.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       GEOGRAPHY      </code></td>
<td><code dir="ltr" translate="no">        GEOGRAPHY       </code><br />
</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       RANGE      </code></td>
<td><code dir="ltr" translate="no">       RANGE      </code> with the same subtype.</td>
</tr>
</tbody>
</table>

If you want to find the supertype for a set of input types, first determine the intersection of the set of supertypes for each input type. If that set is empty then the input types have no common supertype. If that set is non-empty, then the common supertype is generally the [most specific](#supertype_specificity) type in that set. Generally, the most specific type is the type with the most restrictive domain.

**Examples**

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Input types</th>
<th>Common supertype</th>
<th>Returns</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">        INT64       </code><br />
<code dir="ltr" translate="no">        FLOAT64       </code><br />
</td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
<td>If you apply supertyping to <code dir="ltr" translate="no">       INT64      </code> and <code dir="ltr" translate="no">       FLOAT64      </code> , supertyping succeeds because they they share a supertype, <code dir="ltr" translate="no">       FLOAT64      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">        INT64       </code><br />
<code dir="ltr" translate="no">        BOOL       </code><br />
</td>
<td>None</td>
<td>Error</td>
<td>If you apply supertyping to <code dir="ltr" translate="no">       INT64      </code> and <code dir="ltr" translate="no">       BOOL      </code> , supertyping fails because they don't share a common supertype.</td>
</tr>
</tbody>
</table>

#### Exact and inexact types

Numeric types can be exact or inexact. For supertyping, if all of the input types are exact types, then the resulting supertype can only be an exact type.

The following table contains a list of exact and inexact numeric data types.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Exact types</th>
<th>Inexact types</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">        INT64       </code><br />
<code dir="ltr" translate="no">        NUMERIC       </code><br />
<code dir="ltr" translate="no">        BIGNUMERIC       </code><br />
</td>
<td><code dir="ltr" translate="no">        FLOAT64       </code><br />
</td>
</tr>
</tbody>
</table>

**Examples**

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Input types</th>
<th>Common supertype</th>
<th>Returns</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">        INT64       </code><br />
<code dir="ltr" translate="no">        FLOAT64       </code><br />
</td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
<td>If supertyping is applied to <code dir="ltr" translate="no">       INT64      </code> and <code dir="ltr" translate="no">       FLOAT64      </code> , supertyping succeeds because there are exact and inexact numeric types being supertyped.</td>
</tr>
</tbody>
</table>

#### Types specificity

Each type has a domain of values that it supports. A type with a narrow domain is more specific than a type with a wider domain. Exact types are more specific than inexact types because inexact types have a wider range of domain values that are supported than exact types. For example, `  INT64  ` is more specific than `  FLOAT64  ` .

#### Supertypes and literals

Supertype rules for literals are more permissive than for normal expressions, and are consistent with implicit coercion rules. The following algorithm is used when the input set of types includes types related to literals:

  - If there exists non-literals in the set, find the set of common supertypes of the non-literals.
  - If there is at least one possible supertype, find the [most specific](#supertype_specificity) type to which the remaining literal types can be implicitly coerced and return that supertype. Otherwise, there is no supertype.
  - If the set only contains types related to literals, compute the supertype of the literal types.
  - If all input types are related to `  NULL  ` literals, then the resulting supertype is `  INT64  ` .
  - If no common supertype is found, an error is produced.

**Examples**

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Input types</th>
<th>Common supertype</th>
<th>Returns</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       INT64      </code> literal<br />
<code dir="ltr" translate="no">       UINT64      </code> expression<br />
</td>
<td><code dir="ltr" translate="no">       UINT64      </code></td>
<td><code dir="ltr" translate="no">       UINT64      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       TIMESTAMP      </code> expression<br />
<code dir="ltr" translate="no">       STRING      </code> literal<br />
</td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       NULL      </code> literal<br />
<code dir="ltr" translate="no">       NULL      </code> literal<br />
</td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       BOOL      </code> literal<br />
<code dir="ltr" translate="no">       TIMESTAMP      </code> literal<br />
</td>
<td>None</td>
<td>Error</td>
</tr>
</tbody>
</table>
