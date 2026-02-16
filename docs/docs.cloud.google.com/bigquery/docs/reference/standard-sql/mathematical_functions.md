GoogleSQL for BigQuery supports mathematical functions. All mathematical functions have the following behaviors:

  - They return `  NULL  ` if any of the input parameters is `  NULL  ` .
  - They return `  NaN  ` if any of the arguments is `  NaN  ` .

## Categories

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Category</th>
<th>Functions</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Trigonometric</td>
<td><a href="#acos"><code dir="ltr" translate="no">        ACOS       </code></a> <a href="#acosh"><code dir="ltr" translate="no">        ACOSH       </code></a> <a href="#asin"><code dir="ltr" translate="no">        ASIN       </code></a> <a href="#asinh"><code dir="ltr" translate="no">        ASINH       </code></a> <a href="#atan"><code dir="ltr" translate="no">        ATAN       </code></a> <a href="#atan2"><code dir="ltr" translate="no">        ATAN2       </code></a> <a href="#atanh"><code dir="ltr" translate="no">        ATANH       </code></a> <a href="#cos"><code dir="ltr" translate="no">        COS       </code></a> <a href="#cosh"><code dir="ltr" translate="no">        COSH       </code></a> <a href="#cot"><code dir="ltr" translate="no">        COT       </code></a> <a href="#coth"><code dir="ltr" translate="no">        COTH       </code></a> <a href="#csc"><code dir="ltr" translate="no">        CSC       </code></a> <a href="#csch"><code dir="ltr" translate="no">        CSCH       </code></a> <a href="#sec"><code dir="ltr" translate="no">        SEC       </code></a> <a href="#sech"><code dir="ltr" translate="no">        SECH       </code></a> <a href="#sin"><code dir="ltr" translate="no">        SIN       </code></a> <a href="#sinh"><code dir="ltr" translate="no">        SINH       </code></a> <a href="#tan"><code dir="ltr" translate="no">        TAN       </code></a> <a href="#tanh"><code dir="ltr" translate="no">        TANH       </code></a></td>
</tr>
<tr class="even">
<td>Exponential and<br />
logarithmic</td>
<td><a href="#exp"><code dir="ltr" translate="no">        EXP       </code></a> <a href="#ln"><code dir="ltr" translate="no">        LN       </code></a> <a href="#log"><code dir="ltr" translate="no">        LOG       </code></a> <a href="#log10"><code dir="ltr" translate="no">        LOG10       </code></a></td>
</tr>
<tr class="odd">
<td>Rounding and<br />
truncation</td>
<td><a href="#ceil"><code dir="ltr" translate="no">        CEIL       </code></a> <a href="#ceiling"><code dir="ltr" translate="no">        CEILING       </code></a> <a href="#floor"><code dir="ltr" translate="no">        FLOOR       </code></a> <a href="#round"><code dir="ltr" translate="no">        ROUND       </code></a> <a href="#trunc"><code dir="ltr" translate="no">        TRUNC       </code></a></td>
</tr>
<tr class="even">
<td>Power and<br />
root</td>
<td><a href="#cbrt"><code dir="ltr" translate="no">        CBRT       </code></a> <a href="#pow"><code dir="ltr" translate="no">        POW       </code></a> <a href="#power"><code dir="ltr" translate="no">        POWER       </code></a> <a href="#sqrt"><code dir="ltr" translate="no">        SQRT       </code></a></td>
</tr>
<tr class="odd">
<td>Sign</td>
<td><a href="#abs"><code dir="ltr" translate="no">        ABS       </code></a> <a href="#sign"><code dir="ltr" translate="no">        SIGN       </code></a></td>
</tr>
<tr class="even">
<td>Distance</td>
<td><a href="#cosine_distance"><code dir="ltr" translate="no">        COSINE_DISTANCE       </code></a> <a href="#euclidean_distance"><code dir="ltr" translate="no">        EUCLIDEAN_DISTANCE       </code></a></td>
</tr>
<tr class="odd">
<td>Comparison</td>
<td><a href="#greatest"><code dir="ltr" translate="no">        GREATEST       </code></a> <a href="#least"><code dir="ltr" translate="no">        LEAST       </code></a></td>
</tr>
<tr class="even">
<td>Random number generator</td>
<td><a href="#rand"><code dir="ltr" translate="no">        RAND       </code></a></td>
</tr>
<tr class="odd">
<td>Arithmetic and error handling</td>
<td><a href="#div"><code dir="ltr" translate="no">        DIV       </code></a> <a href="#ieee_divide"><code dir="ltr" translate="no">        IEEE_DIVIDE       </code></a> <a href="#is_inf"><code dir="ltr" translate="no">        IS_INF       </code></a> <a href="#is_nan"><code dir="ltr" translate="no">        IS_NAN       </code></a> <a href="#mod"><code dir="ltr" translate="no">        MOD       </code></a> <a href="#safe_add"><code dir="ltr" translate="no">        SAFE_ADD       </code></a> <a href="#safe_divide"><code dir="ltr" translate="no">        SAFE_DIVIDE       </code></a> <a href="#safe_multiply"><code dir="ltr" translate="no">        SAFE_MULTIPLY       </code></a> <a href="#safe_negate"><code dir="ltr" translate="no">        SAFE_NEGATE       </code></a> <a href="#safe_subtract"><code dir="ltr" translate="no">        SAFE_SUBTRACT       </code></a></td>
</tr>
<tr class="even">
<td>Bucket</td>
<td><a href="#range_bucket"><code dir="ltr" translate="no">        RANGE_BUCKET       </code></a></td>
</tr>
</tbody>
</table>

## Function list

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Name</th>
<th>Summary</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#abs"><code dir="ltr" translate="no">        ABS       </code></a></td>
<td>Computes the absolute value of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#acos"><code dir="ltr" translate="no">        ACOS       </code></a></td>
<td>Computes the inverse cosine of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#acosh"><code dir="ltr" translate="no">        ACOSH       </code></a></td>
<td>Computes the inverse hyperbolic cosine of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#asin"><code dir="ltr" translate="no">        ASIN       </code></a></td>
<td>Computes the inverse sine of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#asinh"><code dir="ltr" translate="no">        ASINH       </code></a></td>
<td>Computes the inverse hyperbolic sine of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#atan"><code dir="ltr" translate="no">        ATAN       </code></a></td>
<td>Computes the inverse tangent of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#atan2"><code dir="ltr" translate="no">        ATAN2       </code></a></td>
<td>Computes the inverse tangent of <code dir="ltr" translate="no">       X/Y      </code> , using the signs of <code dir="ltr" translate="no">       X      </code> and <code dir="ltr" translate="no">       Y      </code> to determine the quadrant.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#atanh"><code dir="ltr" translate="no">        ATANH       </code></a></td>
<td>Computes the inverse hyperbolic tangent of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#avg"><code dir="ltr" translate="no">        AVG       </code></a></td>
<td>Gets the average of non- <code dir="ltr" translate="no">       NULL      </code> values.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/aggregate_functions">Aggregate functions</a> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/aggregate-dp-functions#dp_avg"><code dir="ltr" translate="no">        AVG       </code> (Differential Privacy)</a></td>
<td><code dir="ltr" translate="no">       DIFFERENTIAL_PRIVACY      </code> -supported <code dir="ltr" translate="no">       AVG      </code> .<br />
<br />
Gets the differentially-private average of non- <code dir="ltr" translate="no">       NULL      </code> , non- <code dir="ltr" translate="no">       NaN      </code> values in a query with a <code dir="ltr" translate="no">       DIFFERENTIAL_PRIVACY      </code> clause.<br />
<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/aggregate-dp-functions">Differential privacy functions</a> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#cbrt"><code dir="ltr" translate="no">        CBRT       </code></a></td>
<td>Computes the cube root of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#ceil"><code dir="ltr" translate="no">        CEIL       </code></a></td>
<td>Gets the smallest integral value that isn't less than <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#ceiling"><code dir="ltr" translate="no">        CEILING       </code></a></td>
<td>Synonym of <code dir="ltr" translate="no">       CEIL      </code> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#cos"><code dir="ltr" translate="no">        COS       </code></a></td>
<td>Computes the cosine of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#cosh"><code dir="ltr" translate="no">        COSH       </code></a></td>
<td>Computes the hyperbolic cosine of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#cosine_distance"><code dir="ltr" translate="no">        COSINE_DISTANCE       </code></a></td>
<td>Computes the cosine distance between two vectors.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#cot"><code dir="ltr" translate="no">        COT       </code></a></td>
<td>Computes the cotangent of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#coth"><code dir="ltr" translate="no">        COTH       </code></a></td>
<td>Computes the hyperbolic cotangent of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#csc"><code dir="ltr" translate="no">        CSC       </code></a></td>
<td>Computes the cosecant of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#csch"><code dir="ltr" translate="no">        CSCH       </code></a></td>
<td>Computes the hyperbolic cosecant of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#div"><code dir="ltr" translate="no">        DIV       </code></a></td>
<td>Divides integer <code dir="ltr" translate="no">       X      </code> by integer <code dir="ltr" translate="no">       Y      </code> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#exp"><code dir="ltr" translate="no">        EXP       </code></a></td>
<td>Computes <code dir="ltr" translate="no">       e      </code> to the power of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#euclidean_distance"><code dir="ltr" translate="no">        EUCLIDEAN_DISTANCE       </code></a></td>
<td>Computes the Euclidean distance between two vectors.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#floor"><code dir="ltr" translate="no">        FLOOR       </code></a></td>
<td>Gets the largest integral value that isn't greater than <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#greatest"><code dir="ltr" translate="no">        GREATEST       </code></a></td>
<td>Gets the greatest value among <code dir="ltr" translate="no">       X1,...,XN      </code> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#ieee_divide"><code dir="ltr" translate="no">        IEEE_DIVIDE       </code></a></td>
<td>Divides <code dir="ltr" translate="no">       X      </code> by <code dir="ltr" translate="no">       Y      </code> , but doesn't generate errors for division by zero or overflow.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#is_inf"><code dir="ltr" translate="no">        IS_INF       </code></a></td>
<td>Checks if <code dir="ltr" translate="no">       X      </code> is positive or negative infinity.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#is_nan"><code dir="ltr" translate="no">        IS_NAN       </code></a></td>
<td>Checks if <code dir="ltr" translate="no">       X      </code> is a <code dir="ltr" translate="no">       NaN      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#least"><code dir="ltr" translate="no">        LEAST       </code></a></td>
<td>Gets the least value among <code dir="ltr" translate="no">       X1,...,XN      </code> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#ln"><code dir="ltr" translate="no">        LN       </code></a></td>
<td>Computes the natural logarithm of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#log"><code dir="ltr" translate="no">        LOG       </code></a></td>
<td>Computes the natural logarithm of <code dir="ltr" translate="no">       X      </code> or the logarithm of <code dir="ltr" translate="no">       X      </code> to base <code dir="ltr" translate="no">       Y      </code> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#log10"><code dir="ltr" translate="no">        LOG10       </code></a></td>
<td>Computes the natural logarithm of <code dir="ltr" translate="no">       X      </code> to base 10.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#max"><code dir="ltr" translate="no">        MAX       </code></a></td>
<td>Gets the maximum non- <code dir="ltr" translate="no">       NULL      </code> value.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/aggregate_functions">Aggregate functions</a> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#max_by"><code dir="ltr" translate="no">        MAX_BY       </code></a></td>
<td>Synonym for <code dir="ltr" translate="no">       ANY_VALUE(x HAVING MAX y)      </code> .<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/aggregate_functions">Aggregate functions</a> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#min_by"><code dir="ltr" translate="no">        MIN_BY       </code></a></td>
<td>Synonym for <code dir="ltr" translate="no">       ANY_VALUE(x HAVING MIN y)      </code> .<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/aggregate_functions">Aggregate functions</a> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#mod"><code dir="ltr" translate="no">        MOD       </code></a></td>
<td>Gets the remainder of the division of <code dir="ltr" translate="no">       X      </code> by <code dir="ltr" translate="no">       Y      </code> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#pow"><code dir="ltr" translate="no">        POW       </code></a></td>
<td>Produces the value of <code dir="ltr" translate="no">       X      </code> raised to the power of <code dir="ltr" translate="no">       Y      </code> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#power"><code dir="ltr" translate="no">        POWER       </code></a></td>
<td>Synonym of <code dir="ltr" translate="no">       POW      </code> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#rand"><code dir="ltr" translate="no">        RAND       </code></a></td>
<td>Generates a pseudo-random value of type <code dir="ltr" translate="no">       FLOAT64      </code> in the range of <code dir="ltr" translate="no">       [0, 1)      </code> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#range_bucket"><code dir="ltr" translate="no">        RANGE_BUCKET       </code></a></td>
<td>Scans through a sorted array and returns the 0-based position of a point's upper bound.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#round"><code dir="ltr" translate="no">        ROUND       </code></a></td>
<td>Rounds <code dir="ltr" translate="no">       X      </code> to the nearest integer or rounds <code dir="ltr" translate="no">       X      </code> to <code dir="ltr" translate="no">       N      </code> decimal places after the decimal point.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#safe_add"><code dir="ltr" translate="no">        SAFE_ADD       </code></a></td>
<td>Equivalent to the addition operator ( <code dir="ltr" translate="no">       X + Y      </code> ), but returns <code dir="ltr" translate="no">       NULL      </code> if overflow occurs.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#safe_divide"><code dir="ltr" translate="no">        SAFE_DIVIDE       </code></a></td>
<td>Equivalent to the division operator ( <code dir="ltr" translate="no">       X / Y      </code> ), but returns <code dir="ltr" translate="no">       NULL      </code> if an error occurs.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#safe_multiply"><code dir="ltr" translate="no">        SAFE_MULTIPLY       </code></a></td>
<td>Equivalent to the multiplication operator ( <code dir="ltr" translate="no">       X * Y      </code> ), but returns <code dir="ltr" translate="no">       NULL      </code> if overflow occurs.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#safe_negate"><code dir="ltr" translate="no">        SAFE_NEGATE       </code></a></td>
<td>Equivalent to the unary minus operator ( <code dir="ltr" translate="no">       -X      </code> ), but returns <code dir="ltr" translate="no">       NULL      </code> if overflow occurs.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#safe_subtract"><code dir="ltr" translate="no">        SAFE_SUBTRACT       </code></a></td>
<td>Equivalent to the subtraction operator ( <code dir="ltr" translate="no">       X - Y      </code> ), but returns <code dir="ltr" translate="no">       NULL      </code> if overflow occurs.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#sec"><code dir="ltr" translate="no">        SEC       </code></a></td>
<td>Computes the secant of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#sech"><code dir="ltr" translate="no">        SECH       </code></a></td>
<td>Computes the hyperbolic secant of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#sign"><code dir="ltr" translate="no">        SIGN       </code></a></td>
<td>Produces -1 , 0, or +1 for negative, zero, and positive arguments respectively.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#sin"><code dir="ltr" translate="no">        SIN       </code></a></td>
<td>Computes the sine of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#sinh"><code dir="ltr" translate="no">        SINH       </code></a></td>
<td>Computes the hyperbolic sine of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#sqrt"><code dir="ltr" translate="no">        SQRT       </code></a></td>
<td>Computes the square root of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#sum"><code dir="ltr" translate="no">        SUM       </code></a></td>
<td>Gets the sum of non- <code dir="ltr" translate="no">       NULL      </code> values.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/aggregate_functions">Aggregate functions</a> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/aggregate-dp-functions#dp_sum"><code dir="ltr" translate="no">        SUM       </code> (Differential Privacy)</a></td>
<td><code dir="ltr" translate="no">       DIFFERENTIAL_PRIVACY      </code> -supported <code dir="ltr" translate="no">       SUM      </code> .<br />
<br />
Gets the differentially-private sum of non- <code dir="ltr" translate="no">       NULL      </code> , non- <code dir="ltr" translate="no">       NaN      </code> values in a query with a <code dir="ltr" translate="no">       DIFFERENTIAL_PRIVACY      </code> clause.<br />
<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/aggregate-dp-functions">Differential privacy functions</a> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#tan"><code dir="ltr" translate="no">        TAN       </code></a></td>
<td>Computes the tangent of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#tanh"><code dir="ltr" translate="no">        TANH       </code></a></td>
<td>Computes the hyperbolic tangent of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#trunc"><code dir="ltr" translate="no">        TRUNC       </code></a></td>
<td>Rounds a number like <code dir="ltr" translate="no">       ROUND(X)      </code> or <code dir="ltr" translate="no">       ROUND(X, N)      </code> , but always rounds towards zero and never overflows.</td>
</tr>
</tbody>
</table>

## `     ABS    `

``` text
ABS(X)
```

**Description**

Computes absolute value. Returns an error if the argument is an integer and the output value can't be represented as the same type; this happens only for the largest negative input value, which has no positive representation.

<table>
<thead>
<tr class="header">
<th>X</th>
<th>ABS(X)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>25</td>
<td>25</td>
</tr>
<tr class="even">
<td>-25</td>
<td>25</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       +inf      </code></td>
<td><code dir="ltr" translate="no">       +inf      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       -inf      </code></td>
<td><code dir="ltr" translate="no">       +inf      </code></td>
</tr>
</tbody>
</table>

**Return Data Type**

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

## `     ACOS    `

``` text
ACOS(X)
```

**Description**

Computes the principal value of the inverse cosine of X. The return value is in the range \[0,π\]. Generates an error if X is a value outside of the range \[-1, 1\].

<table>
<thead>
<tr class="header">
<th>X</th>
<th>ACOS(X)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       +inf      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       -inf      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       NaN      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
<tr class="even">
<td>X &lt; -1</td>
<td>Error</td>
</tr>
<tr class="odd">
<td>X &gt; 1</td>
<td>Error</td>
</tr>
</tbody>
</table>

## `     ACOSH    `

``` text
ACOSH(X)
```

**Description**

Computes the inverse hyperbolic cosine of X. Generates an error if X is a value less than 1.

<table>
<thead>
<tr class="header">
<th>X</th>
<th>ACOSH(X)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       +inf      </code></td>
<td><code dir="ltr" translate="no">       +inf      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       -inf      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       NaN      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
<tr class="even">
<td>X &lt; 1</td>
<td>Error</td>
</tr>
</tbody>
</table>

## `     ASIN    `

``` text
ASIN(X)
```

**Description**

Computes the principal value of the inverse sine of X. The return value is in the range \[-π/2,π/2\]. Generates an error if X is outside of the range \[-1, 1\].

<table>
<thead>
<tr class="header">
<th>X</th>
<th>ASIN(X)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       +inf      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       -inf      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       NaN      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
<tr class="even">
<td>X &lt; -1</td>
<td>Error</td>
</tr>
<tr class="odd">
<td>X &gt; 1</td>
<td>Error</td>
</tr>
</tbody>
</table>

## `     ASINH    `

``` text
ASINH(X)
```

**Description**

Computes the inverse hyperbolic sine of X. Doesn't fail.

<table>
<thead>
<tr class="header">
<th>X</th>
<th>ASINH(X)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       +inf      </code></td>
<td><code dir="ltr" translate="no">       +inf      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       -inf      </code></td>
<td><code dir="ltr" translate="no">       -inf      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       NaN      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
</tbody>
</table>

## `     ATAN    `

``` text
ATAN(X)
```

**Description**

Computes the principal value of the inverse tangent of X. The return value is in the range \[-π/2,π/2\]. Doesn't fail.

<table>
<thead>
<tr class="header">
<th>X</th>
<th>ATAN(X)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       +inf      </code></td>
<td>π/2</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       -inf      </code></td>
<td>-π/2</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       NaN      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
</tbody>
</table>

## `     ATAN2    `

``` text
ATAN2(X, Y)
```

**Description**

Calculates the principal value of the inverse tangent of X/Y using the signs of the two arguments to determine the quadrant. The return value is in the range \[-π,π\].

<table>
<thead>
<tr class="header">
<th>X</th>
<th>Y</th>
<th>ATAN2(X, Y)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       NaN      </code></td>
<td>Any value</td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
<tr class="even">
<td>Any value</td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
<tr class="odd">
<td>0.0</td>
<td>0.0</td>
<td>0.0</td>
</tr>
<tr class="even">
<td>Positive Finite value</td>
<td><code dir="ltr" translate="no">       -inf      </code></td>
<td>π</td>
</tr>
<tr class="odd">
<td>Negative Finite value</td>
<td><code dir="ltr" translate="no">       -inf      </code></td>
<td>-π</td>
</tr>
<tr class="even">
<td>Finite value</td>
<td><code dir="ltr" translate="no">       +inf      </code></td>
<td>0.0</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       +inf      </code></td>
<td>Finite value</td>
<td>π/2</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       -inf      </code></td>
<td>Finite value</td>
<td>-π/2</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       +inf      </code></td>
<td><code dir="ltr" translate="no">       -inf      </code></td>
<td>¾π</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       -inf      </code></td>
<td><code dir="ltr" translate="no">       -inf      </code></td>
<td>-¾π</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       +inf      </code></td>
<td><code dir="ltr" translate="no">       +inf      </code></td>
<td>π/4</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       -inf      </code></td>
<td><code dir="ltr" translate="no">       +inf      </code></td>
<td>-π/4</td>
</tr>
</tbody>
</table>

## `     ATANH    `

``` text
ATANH(X)
```

**Description**

Computes the inverse hyperbolic tangent of X. Generates an error if X is outside of the range (-1, 1).

<table>
<thead>
<tr class="header">
<th>X</th>
<th>ATANH(X)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       +inf      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       -inf      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       NaN      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
<tr class="even">
<td>X &lt; -1</td>
<td>Error</td>
</tr>
<tr class="odd">
<td>X &gt; 1</td>
<td>Error</td>
</tr>
</tbody>
</table>

## `     CBRT    `

``` text
CBRT(X)
```

**Description**

Computes the cube root of `  X  ` . `  X  ` can be any data type that [coerces to `  FLOAT64  `](/bigquery/docs/reference/standard-sql/conversion_rules) . Supports the `  SAFE.  ` prefix.

<table>
<thead>
<tr class="header">
<th>X</th>
<th>CBRT(X)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       +inf      </code></td>
<td><code dir="ltr" translate="no">       inf      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       -inf      </code></td>
<td><code dir="ltr" translate="no">       -inf      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       NaN      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       0      </code></td>
<td><code dir="ltr" translate="no">       0      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       NULL      </code></td>
<td><code dir="ltr" translate="no">       NULL      </code></td>
</tr>
</tbody>
</table>

**Return Data Type**

`  FLOAT64  `

**Example**

``` text
SELECT CBRT(27) AS cube_root;

/*--------------------+
 | cube_root          |
 +--------------------+
 | 3.0000000000000004 |
 +--------------------*/
```

## `     CEIL    `

``` text
CEIL(X)
```

**Description**

Returns the smallest integral value that isn't less than X.

<table>
<thead>
<tr class="header">
<th>X</th>
<th>CEIL(X)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>2.0</td>
<td>2.0</td>
</tr>
<tr class="even">
<td>2.3</td>
<td>3.0</td>
</tr>
<tr class="odd">
<td>2.8</td>
<td>3.0</td>
</tr>
<tr class="even">
<td>2.5</td>
<td>3.0</td>
</tr>
<tr class="odd">
<td>-2.3</td>
<td>-2.0</td>
</tr>
<tr class="even">
<td>-2.8</td>
<td>-2.0</td>
</tr>
<tr class="odd">
<td>-2.5</td>
<td>-2.0</td>
</tr>
<tr class="even">
<td>0</td>
<td>0</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       +inf      </code></td>
<td><code dir="ltr" translate="no">       +inf      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       -inf      </code></td>
<td><code dir="ltr" translate="no">       -inf      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       NaN      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
</tbody>
</table>

**Return Data Type**

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
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
</tr>
</tbody>
</table>

## `     CEILING    `

``` text
CEILING(X)
```

**Description**

Synonym of CEIL(X)

## `     COS    `

``` text
COS(X)
```

**Description**

Computes the cosine of X where X is specified in radians. Never fails.

<table>
<thead>
<tr class="header">
<th>X</th>
<th>COS(X)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       +inf      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       -inf      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       NaN      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
</tbody>
</table>

## `     COSH    `

``` text
COSH(X)
```

**Description**

Computes the hyperbolic cosine of X where X is specified in radians. Generates an error if overflow occurs.

<table>
<thead>
<tr class="header">
<th>X</th>
<th>COSH(X)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       +inf      </code></td>
<td><code dir="ltr" translate="no">       +inf      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       -inf      </code></td>
<td><code dir="ltr" translate="no">       +inf      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       NaN      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
</tbody>
</table>

## `     COSINE_DISTANCE    `

``` text
COSINE_DISTANCE(vector1, vector2)
```

**Description**

Computes the [cosine distance](https://en.wikipedia.org/wiki/Cosine_similarity#Cosine_distance) between two vectors.

**Definitions**

  - `  vector1  ` : A vector that's represented by an `  ARRAY<T>  ` value or a sparse vector that is represented by an `  ARRAY<STRUCT<dimension,magnitude>>  ` value.
  - `  vector2  ` : A vector that's represented by an `  ARRAY<T>  ` value or a sparse vector that is represented by an `  ARRAY<STRUCT<dimension,magnitude>>  ` value.

**Details**

  - `  ARRAY<T>  ` can be used to represent a vector. Each zero-based index in this array represents a dimension. The value for each element in this array represents a magnitude.
    
    `  T  ` can represent the following and must be the same for both vectors:
    
      - `  FLOAT64  `
    
    In the following example vector, there are four dimensions. The magnitude is `  10.0  ` for dimension `  0  ` , `  55.0  ` for dimension `  1  ` , `  40.0  ` for dimension `  2  ` , and `  34.0  ` for dimension `  3  ` :
    
    ``` text
    [10.0, 55.0, 40.0, 34.0]
    ```

  - `  ARRAY<STRUCT<dimension,magnitude>>  ` can be used to represent a sparse vector. With a sparse vector, you only need to include dimension-magnitude pairs for non-zero magnitudes. If a magnitude isn't present in the sparse vector, the magnitude is implicitly understood to be zero.
    
    For example, if you have a vector with 10,000 dimensions, but only 10 dimensions have non-zero magnitudes, then the vector is a sparse vector. As a result, it's more efficient to describe a sparse vector by only mentioning its non-zero magnitudes.
    
    In `  ARRAY<STRUCT<dimension,magnitude>>  ` , `  STRUCT<dimension,magnitude>  ` represents a dimension-magnitude pair for each non-zero magnitude in a sparse vector. These parts need to be included for each dimension-magnitude pair:
    
      - `  dimension  ` : A `  STRING  ` or `  INT64  ` value that represents a dimension in a vector.
    
      - `  magnitude  ` : A `  FLOAT64  ` value that represents a non-zero magnitude for a specific dimension in a vector.
    
    You don't need to include empty dimension-magnitude pairs in a sparse vector. For example, the following sparse vector and non-sparse vector are equivalent:
    
    ``` text
    -- sparse vector ARRAY<STRUCT<INT64, FLOAT64>>
    [(1, 10.0), (2, 30.0), (5, 40.0)]
    ```
    
    ``` text
    -- vector ARRAY<FLOAT64>
    [0.0, 10.0, 30.0, 0.0, 0.0, 40.0]
    ```
    
    In a sparse vector, dimension-magnitude pairs don't need to be in any particular order. The following sparse vectors are equivalent:
    
    ``` text
    [('a', 10.0), ('b', 30.0), ('d', 40.0)]
    ```
    
    ``` text
    [('d', 40.0), ('a', 10.0), ('b', 30.0)]
    ```

  - Both non-sparse vectors in this function must share the same dimensions, and if they don't, an error is produced.

  - A vector can't be a zero vector. A vector is a zero vector if it has no dimensions or all dimensions have a magnitude of `  0  ` , such as `  []  ` or `  [0.0, 0.0]  ` . If a zero vector is encountered, an error is produced.

  - An error is produced if a magnitude in a vector is `  NULL  ` .

  - If a vector is `  NULL  ` , `  NULL  ` is returned.

**Return type**

`  FLOAT64  `

**Examples**

In the following example, non-sparsevectors are used to compute the cosine distance:

``` text
SELECT COSINE_DISTANCE([1.0, 2.0], [3.0, 4.0]) AS results;

/*----------+
 | results  |
 +----------+
 | 0.016130 |
 +----------*/
```

In the following example, sparse vectors are used to compute the cosine distance:

``` text
SELECT COSINE_DISTANCE(
 [(1, 1.0), (2, 2.0)],
 [(2, 4.0), (1, 3.0)]) AS results;

 /*----------+
  | results  |
  +----------+
  | 0.016130 |
  +----------*/
```

The ordering of numeric values in a vector doesn't impact the results produced by this function. For example these queries produce the same results even though the numeric values in each vector is in a different order:

``` text
SELECT COSINE_DISTANCE([1.0, 2.0], [3.0, 4.0]) AS results;
```

``` text
SELECT COSINE_DISTANCE([2.0, 1.0], [4.0, 3.0]) AS results;
```

``` text
SELECT COSINE_DISTANCE([(1, 1.0), (2, 2.0)], [(1, 3.0), (2, 4.0)]) AS results;
```

``` text
 /*----------+
  | results  |
  +----------+
  | 0.016130 |
  +----------*/
```

In the following example, the function can't compute cosine distance against the first vector, which is a zero vector:

``` text
-- ERROR
SELECT COSINE_DISTANCE([0.0, 0.0], [3.0, 4.0]) AS results;
```

``` text
-- ERROR
SELECT COSINE_DISTANCE([(1, 0.0), (2, 0.0)], [(1, 3.0), (2, 4.0)]) AS results;
```

Both non-sparse vectors must have the same dimensions. If not, an error is produced. In the following example, the first vector has two dimensions and the second vector has three:

``` text
-- ERROR
SELECT COSINE_DISTANCE([9.0, 7.0], [8.0, 4.0, 5.0]) AS results;
```

If you use sparse vectors and you repeat a dimension, an error is produced:

``` text
-- ERROR
SELECT COSINE_DISTANCE(
  [(1, 9.0), (2, 7.0), (2, 8.0)], [(1, 8.0), (2, 4.0), (3, 5.0)]) AS results;
```

## `     COT    `

``` text
COT(X)
```

**Description**

Computes the cotangent for the angle of `  X  ` , where `  X  ` is specified in radians. `  X  ` can be any data type that [coerces to `  FLOAT64  `](/bigquery/docs/reference/standard-sql/conversion_rules) . Supports the `  SAFE.  ` prefix.

<table>
<thead>
<tr class="header">
<th>X</th>
<th>COT(X)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       +inf      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       -inf      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       NaN      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       0      </code></td>
<td><code dir="ltr" translate="no">       Error      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       NULL      </code></td>
<td><code dir="ltr" translate="no">       NULL      </code></td>
</tr>
</tbody>
</table>

**Return Data Type**

`  FLOAT64  `

**Example**

``` text
SELECT COT(1) AS a, SAFE.COT(0) AS b;

/*---------------------+------+
 | a                   | b    |
 +---------------------+------+
 | 0.64209261593433065 | NULL |
 +---------------------+------*/
```

## `     COTH    `

``` text
COTH(X)
```

**Description**

Computes the hyperbolic cotangent for the angle of `  X  ` , where `  X  ` is specified in radians. `  X  ` can be any data type that [coerces to `  FLOAT64  `](/bigquery/docs/reference/standard-sql/conversion_rules) . Supports the `  SAFE.  ` prefix.

<table>
<thead>
<tr class="header">
<th>X</th>
<th>COTH(X)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       +inf      </code></td>
<td><code dir="ltr" translate="no">       1      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       -inf      </code></td>
<td><code dir="ltr" translate="no">       -1      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       NaN      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       0      </code></td>
<td><code dir="ltr" translate="no">       Error      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       NULL      </code></td>
<td><code dir="ltr" translate="no">       NULL      </code></td>
</tr>
</tbody>
</table>

**Return Data Type**

`  FLOAT64  `

**Example**

``` text
SELECT COTH(1) AS a, SAFE.COTH(0) AS b;

/*----------------+------+
 | a              | b    |
 +----------------+------+
 | 1.313035285499 | NULL |
 +----------------+------*/
```

## `     CSC    `

``` text
CSC(X)
```

**Description**

Computes the cosecant of the input angle, which is in radians. `  X  ` can be any data type that [coerces to `  FLOAT64  `](/bigquery/docs/reference/standard-sql/conversion_rules) . Supports the `  SAFE.  ` prefix.

<table>
<thead>
<tr class="header">
<th>X</th>
<th>CSC(X)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       +inf      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       -inf      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       NaN      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       0      </code></td>
<td><code dir="ltr" translate="no">       Error      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       NULL      </code></td>
<td><code dir="ltr" translate="no">       NULL      </code></td>
</tr>
</tbody>
</table>

**Return Data Type**

`  FLOAT64  `

**Example**

``` text
SELECT CSC(100) AS a, CSC(-1) AS b, SAFE.CSC(0) AS c;

/*----------------+-----------------+------+
 | a              | b               | c    |
 +----------------+-----------------+------+
 | -1.97485753142 | -1.188395105778 | NULL |
 +----------------+-----------------+------*/
```

## `     CSCH    `

``` text
CSCH(X)
```

**Description**

Computes the hyperbolic cosecant of the input angle, which is in radians. `  X  ` can be any data type that [coerces to `  FLOAT64  `](/bigquery/docs/reference/standard-sql/conversion_rules) . Supports the `  SAFE.  ` prefix.

<table>
<thead>
<tr class="header">
<th>X</th>
<th>CSCH(X)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       +inf      </code></td>
<td><code dir="ltr" translate="no">       0      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       -inf      </code></td>
<td><code dir="ltr" translate="no">       0      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       NaN      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       0      </code></td>
<td><code dir="ltr" translate="no">       Error      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       NULL      </code></td>
<td><code dir="ltr" translate="no">       NULL      </code></td>
</tr>
</tbody>
</table>

**Return Data Type**

`  FLOAT64  `

**Example**

``` text
SELECT CSCH(0.5) AS a, CSCH(-2) AS b, SAFE.CSCH(0) AS c;

/*----------------+----------------+------+
 | a              | b              | c    |
 +----------------+----------------+------+
 | 1.919034751334 | -0.27572056477 | NULL |
 +----------------+----------------+------*/
```

## `     DIV    `

``` text
DIV(X, Y)
```

**Description**

Returns the result of integer division of X by Y. Division by zero returns an error. Division by -1 may overflow.

<table>
<thead>
<tr class="header">
<th>X</th>
<th>Y</th>
<th>DIV(X, Y)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>20</td>
<td>4</td>
<td>5</td>
</tr>
<tr class="even">
<td>12</td>
<td>-7</td>
<td>-1</td>
</tr>
<tr class="odd">
<td>20</td>
<td>3</td>
<td>6</td>
</tr>
<tr class="even">
<td>0</td>
<td>20</td>
<td>0</td>
</tr>
<tr class="odd">
<td>20</td>
<td>0</td>
<td>Error</td>
</tr>
</tbody>
</table>

**Return Data Type**

The return data type is determined by the argument types with the following table.

<table>
<thead>
<tr class="header">
<th>INPUT</th>
<th><code dir="ltr" translate="no">       INT64      </code></th>
<th><code dir="ltr" translate="no">       NUMERIC      </code></th>
<th><code dir="ltr" translate="no">       BIGNUMERIC      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
</tr>
</tbody>
</table>

## `     EXP    `

``` text
EXP(X)
```

**Description**

Computes *e* to the power of X, also called the natural exponential function. If the result underflows, this function returns a zero. Generates an error if the result overflows.

<table>
<thead>
<tr class="header">
<th>X</th>
<th>EXP(X)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>0.0</td>
<td>1.0</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       +inf      </code></td>
<td><code dir="ltr" translate="no">       +inf      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       -inf      </code></td>
<td>0.0</td>
</tr>
</tbody>
</table>

**Return Data Type**

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
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
</tr>
</tbody>
</table>

## `     EUCLIDEAN_DISTANCE    `

``` text
EUCLIDEAN_DISTANCE(vector1, vector2)
```

**Description**

Computes the [Euclidean distance](https://en.wikipedia.org/wiki/Euclidean_distance) between two vectors.

**Definitions**

  - `  vector1  ` : A vector that's represented by an `  ARRAY<T>  ` value or a sparse vector that is represented by an `  ARRAY<STRUCT<dimension,magnitude>>  ` value.
  - `  vector2  ` : A vector that's represented by an `  ARRAY<T>  ` value or a sparse vector that is represented by an `  ARRAY<STRUCT<dimension,magnitude>>  ` value.

**Details**

  - `  ARRAY<T>  ` can be used to represent a vector. Each zero-based index in this array represents a dimension. The value for each element in this array represents a magnitude.
    
    `  T  ` can represent the following and must be the same for both vectors:
    
      - `  FLOAT64  `
    
    In the following example vector, there are four dimensions. The magnitude is `  10.0  ` for dimension `  0  ` , `  55.0  ` for dimension `  1  ` , `  40.0  ` for dimension `  2  ` , and `  34.0  ` for dimension `  3  ` :
    
    ``` text
    [10.0, 55.0, 40.0, 34.0]
    ```

  - `  ARRAY<STRUCT<dimension,magnitude>>  ` can be used to represent a sparse vector. With a sparse vector, you only need to include dimension-magnitude pairs for non-zero magnitudes. If a magnitude isn't present in the sparse vector, the magnitude is implicitly understood to be zero.
    
    For example, if you have a vector with 10,000 dimensions, but only 10 dimensions have non-zero magnitudes, then the vector is a sparse vector. As a result, it's more efficient to describe a sparse vector by only mentioning its non-zero magnitudes.
    
    In `  ARRAY<STRUCT<dimension,magnitude>>  ` , `  STRUCT<dimension,magnitude>  ` represents a dimension-magnitude pair for each non-zero magnitude in a sparse vector. These parts need to be included for each dimension-magnitude pair:
    
      - `  dimension  ` : A `  STRING  ` or `  INT64  ` value that represents a dimension in a vector.
    
      - `  magnitude  ` : A `  FLOAT64  ` value that represents a non-zero magnitude for a specific dimension in a vector.
    
    You don't need to include empty dimension-magnitude pairs in a sparse vector. For example, the following sparse vector and non-sparse vector are equivalent:
    
    ``` text
    -- sparse vector ARRAY<STRUCT<INT64, FLOAT64>>
    [(1, 10.0), (2, 30.0), (5, 40.0)]
    ```
    
    ``` text
    -- vector ARRAY<FLOAT64>
    [0.0, 10.0, 30.0, 0.0, 0.0, 40.0]
    ```
    
    In a sparse vector, dimension-magnitude pairs don't need to be in any particular order. The following sparse vectors are equivalent:
    
    ``` text
    [('a', 10.0), ('b', 30.0), ('d', 40.0)]
    ```
    
    ``` text
    [('d', 40.0), ('a', 10.0), ('b', 30.0)]
    ```

  - Both non-sparse vectors in this function must share the same dimensions, and if they don't, an error is produced.

  - A vector can be a zero vector. A vector is a zero vector if it has no dimensions or all dimensions have a magnitude of `  0  ` , such as `  []  ` or `  [0.0, 0.0]  ` .

  - An error is produced if a magnitude in a vector is `  NULL  ` .

  - If a vector is `  NULL  ` , `  NULL  ` is returned.

**Return type**

`  FLOAT64  `

**Examples**

In the following example, non-sparse vectors are used to compute the Euclidean distance:

``` text
SELECT EUCLIDEAN_DISTANCE([1.0, 2.0], [3.0, 4.0]) AS results;

/*----------+
 | results  |
 +----------+
 | 2.828    |
 +----------*/
```

In the following example, sparse vectors are used to compute the Euclidean distance:

``` text
SELECT EUCLIDEAN_DISTANCE(
 [(1, 1.0), (2, 2.0)],
 [(2, 4.0), (1, 3.0)]) AS results;

 /*----------+
  | results  |
  +----------+
  | 2.828    |
  +----------*/
```

The ordering of magnitudes in a vector doesn't impact the results produced by this function. For example these queries produce the same results even though the magnitudes in each vector is in a different order:

``` text
SELECT EUCLIDEAN_DISTANCE([1.0, 2.0], [3.0, 4.0]);
```

``` text
SELECT EUCLIDEAN_DISTANCE([2.0, 1.0], [4.0, 3.0]);
```

``` text
SELECT EUCLIDEAN_DISTANCE([(1, 1.0), (2, 2.0)], [(1, 3.0), (2, 4.0)]) AS results;
```

``` text
 /*----------+
  | results  |
  +----------+
  | 2.828    |
  +----------*/
```

Both non-sparse vectors must have the same dimensions. If not, an error is produced. In the following example, the first vector has two dimensions and the second vector has three:

``` text
-- ERROR
SELECT EUCLIDEAN_DISTANCE([9.0, 7.0], [8.0, 4.0, 5.0]) AS results;
```

If you use sparse vectors and you repeat a dimension, an error is produced:

``` text
-- ERROR
SELECT EUCLIDEAN_DISTANCE(
  [(1, 9.0), (2, 7.0), (2, 8.0)], [(1, 8.0), (2, 4.0), (3, 5.0)]) AS results;
```

## `     FLOOR    `

``` text
FLOOR(X)
```

**Description**

Returns the largest integral value that isn't greater than X.

<table>
<thead>
<tr class="header">
<th>X</th>
<th>FLOOR(X)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>2.0</td>
<td>2.0</td>
</tr>
<tr class="even">
<td>2.3</td>
<td>2.0</td>
</tr>
<tr class="odd">
<td>2.8</td>
<td>2.0</td>
</tr>
<tr class="even">
<td>2.5</td>
<td>2.0</td>
</tr>
<tr class="odd">
<td>-2.3</td>
<td>-3.0</td>
</tr>
<tr class="even">
<td>-2.8</td>
<td>-3.0</td>
</tr>
<tr class="odd">
<td>-2.5</td>
<td>-3.0</td>
</tr>
<tr class="even">
<td>0</td>
<td>0</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       +inf      </code></td>
<td><code dir="ltr" translate="no">       +inf      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       -inf      </code></td>
<td><code dir="ltr" translate="no">       -inf      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       NaN      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
</tbody>
</table>

**Return Data Type**

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
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
</tr>
</tbody>
</table>

## `     GREATEST    `

``` text
GREATEST(X1,...,XN)
```

**Description**

Returns the greatest value among `  X1,...,XN  ` . If any argument is `  NULL  ` , returns `  NULL  ` . Otherwise, in the case of floating-point arguments, if any argument is `  NaN  ` , returns `  NaN  ` . In all other cases, returns the value among `  X1,...,XN  ` that has the greatest value according to the ordering used by the `  ORDER BY  ` clause. The arguments `  X1, ..., XN  ` must be coercible to a common supertype, and the supertype must support ordering.

<table>
<thead>
<tr class="header">
<th>X1,...,XN</th>
<th>GREATEST(X1,...,XN)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>3,5,1</td>
<td>5</td>
</tr>
</tbody>
</table>

This function supports specifying [collation](/bigquery/docs/reference/standard-sql/collation-concepts) .

**Return Data Types**

Data type of the input values.

## `     IEEE_DIVIDE    `

``` text
IEEE_DIVIDE(X, Y)
```

**Description**

Divides X by Y; this function never fails. Returns `  FLOAT64  ` . Unlike the division operator (/), this function doesn't generate errors for division by zero or overflow.

<table>
<thead>
<tr class="header">
<th>X</th>
<th>Y</th>
<th>IEEE_DIVIDE(X, Y)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>20.0</td>
<td>4.0</td>
<td>5.0</td>
</tr>
<tr class="even">
<td>20.0</td>
<td>6.0</td>
<td>3.3333333333333335</td>
</tr>
<tr class="odd">
<td>0.0</td>
<td>25.0</td>
<td>0.0</td>
</tr>
<tr class="even">
<td>25.0</td>
<td>0.0</td>
<td><code dir="ltr" translate="no">       +inf      </code></td>
</tr>
<tr class="odd">
<td>-25.0</td>
<td>0.0</td>
<td><code dir="ltr" translate="no">       -inf      </code></td>
</tr>
<tr class="even">
<td>25.0</td>
<td>-0.0</td>
<td><code dir="ltr" translate="no">       -inf      </code></td>
</tr>
<tr class="odd">
<td>0.0</td>
<td>0.0</td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
<tr class="even">
<td>0.0</td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       NaN      </code></td>
<td>0.0</td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       +inf      </code></td>
<td><code dir="ltr" translate="no">       +inf      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       -inf      </code></td>
<td><code dir="ltr" translate="no">       -inf      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
</tbody>
</table>

## `     IS_INF    `

``` text
IS_INF(X)
```

**Description**

Returns `  TRUE  ` if the value is positive or negative infinity.

<table>
<thead>
<tr class="header">
<th>X</th>
<th>IS_INF(X)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       +inf      </code></td>
<td><code dir="ltr" translate="no">       TRUE      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       -inf      </code></td>
<td><code dir="ltr" translate="no">       TRUE      </code></td>
</tr>
<tr class="odd">
<td>25</td>
<td><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
</tbody>
</table>

## `     IS_NAN    `

``` text
IS_NAN(X)
```

**Description**

Returns `  TRUE  ` if the value is a `  NaN  ` value.

<table>
<thead>
<tr class="header">
<th>X</th>
<th>IS_NAN(X)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       NaN      </code></td>
<td><code dir="ltr" translate="no">       TRUE      </code></td>
</tr>
<tr class="even">
<td>25</td>
<td><code dir="ltr" translate="no">       FALSE      </code></td>
</tr>
</tbody>
</table>

## `     LEAST    `

``` text
LEAST(X1,...,XN)
```

**Description**

Returns the least value among `  X1,...,XN  ` . If any argument is `  NULL  ` , returns `  NULL  ` . Otherwise, in the case of floating-point arguments, if any argument is `  NaN  ` , returns `  NaN  ` . In all other cases, returns the value among `  X1,...,XN  ` that has the least value according to the ordering used by the `  ORDER BY  ` clause. The arguments `  X1, ..., XN  ` must be coercible to a common supertype, and the supertype must support ordering.

<table>
<thead>
<tr class="header">
<th>X1,...,XN</th>
<th>LEAST(X1,...,XN)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>3,5,1</td>
<td>1</td>
</tr>
</tbody>
</table>

This function supports specifying [collation](/bigquery/docs/reference/standard-sql/collation-concepts) .

**Return Data Types**

Data type of the input values.

## `     LN    `

``` text
LN(X)
```

**Description**

Computes the natural logarithm of X. Generates an error if X is less than or equal to zero.

<table>
<thead>
<tr class="header">
<th>X</th>
<th>LN(X)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>1.0</td>
<td>0.0</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       +inf      </code></td>
<td><code dir="ltr" translate="no">       +inf      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       X &lt;= 0      </code></td>
<td>Error</td>
</tr>
</tbody>
</table>

**Return Data Type**

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
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
</tr>
</tbody>
</table>

## `     LOG    `

``` text
LOG(X [, Y])
```

**Description**

If only X is present, `  LOG  ` is a synonym of `  LN  ` . If Y is also present, `  LOG  ` computes the logarithm of X to base Y.

<table>
<thead>
<tr class="header">
<th>X</th>
<th>Y</th>
<th>LOG(X, Y)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>100.0</td>
<td>10.0</td>
<td>2.0</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       -inf      </code></td>
<td>Any value</td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
<tr class="odd">
<td>Any value</td>
<td><code dir="ltr" translate="no">       +inf      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       +inf      </code></td>
<td>0.0 &lt; Y &lt; 1.0</td>
<td><code dir="ltr" translate="no">       -inf      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       +inf      </code></td>
<td>Y &gt; 1.0</td>
<td><code dir="ltr" translate="no">       +inf      </code></td>
</tr>
<tr class="even">
<td>X &lt;= 0</td>
<td>Any value</td>
<td>Error</td>
</tr>
<tr class="odd">
<td>Any value</td>
<td>Y &lt;= 0</td>
<td>Error</td>
</tr>
<tr class="even">
<td>Any value</td>
<td>1.0</td>
<td>Error</td>
</tr>
</tbody>
</table>

**Return Data Type**

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

## `     LOG10    `

``` text
LOG10(X)
```

**Description**

Similar to `  LOG  ` , but computes logarithm to base 10.

<table>
<thead>
<tr class="header">
<th>X</th>
<th>LOG10(X)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>100.0</td>
<td>2.0</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       -inf      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       +inf      </code></td>
<td><code dir="ltr" translate="no">       +inf      </code></td>
</tr>
<tr class="even">
<td>X &lt;= 0</td>
<td>Error</td>
</tr>
</tbody>
</table>

**Return Data Type**

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
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
</tr>
</tbody>
</table>

## `     MOD    `

``` text
MOD(X, Y)
```

**Description**

Modulo function: returns the remainder of the division of X by Y. Returned value has the same sign as X. An error is generated if Y is 0.

<table>
<thead>
<tr class="header">
<th>X</th>
<th>Y</th>
<th>MOD(X, Y)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>25</td>
<td>12</td>
<td>1</td>
</tr>
<tr class="even">
<td>25</td>
<td>0</td>
<td>Error</td>
</tr>
</tbody>
</table>

**Return Data Type**

The return data type is determined by the argument types with the following table.

<table>
<thead>
<tr class="header">
<th>INPUT</th>
<th><code dir="ltr" translate="no">       INT64      </code></th>
<th><code dir="ltr" translate="no">       NUMERIC      </code></th>
<th><code dir="ltr" translate="no">       BIGNUMERIC      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
</tr>
</tbody>
</table>

## `     POW    `

``` text
POW(X, Y)
```

**Description**

Returns the value of X raised to the power of Y. If the result underflows and isn't representable, then the function returns a value of zero.

<table>
<thead>
<tr class="header">
<th>X</th>
<th>Y</th>
<th>POW(X, Y)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>2.0</td>
<td>3.0</td>
<td>8.0</td>
</tr>
<tr class="even">
<td>1.0</td>
<td>Any value including <code dir="ltr" translate="no">       NaN      </code></td>
<td>1.0</td>
</tr>
<tr class="odd">
<td>Any value including <code dir="ltr" translate="no">       NaN      </code></td>
<td>0</td>
<td>1.0</td>
</tr>
<tr class="even">
<td>-1.0</td>
<td><code dir="ltr" translate="no">       +inf      </code></td>
<td>1.0</td>
</tr>
<tr class="odd">
<td>-1.0</td>
<td><code dir="ltr" translate="no">       -inf      </code></td>
<td>1.0</td>
</tr>
<tr class="even">
<td>ABS(X) &lt; 1</td>
<td><code dir="ltr" translate="no">       -inf      </code></td>
<td><code dir="ltr" translate="no">       +inf      </code></td>
</tr>
<tr class="odd">
<td>ABS(X) &gt; 1</td>
<td><code dir="ltr" translate="no">       -inf      </code></td>
<td>0.0</td>
</tr>
<tr class="even">
<td>ABS(X) &lt; 1</td>
<td><code dir="ltr" translate="no">       +inf      </code></td>
<td>0.0</td>
</tr>
<tr class="odd">
<td>ABS(X) &gt; 1</td>
<td><code dir="ltr" translate="no">       +inf      </code></td>
<td><code dir="ltr" translate="no">       +inf      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       -inf      </code></td>
<td>Y &lt; 0</td>
<td>0.0</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       -inf      </code></td>
<td>Y &gt; 0</td>
<td><code dir="ltr" translate="no">       -inf      </code> if Y is an odd integer, <code dir="ltr" translate="no">       +inf      </code> otherwise</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       +inf      </code></td>
<td>Y &lt; 0</td>
<td>0</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       +inf      </code></td>
<td>Y &gt; 0</td>
<td><code dir="ltr" translate="no">       +inf      </code></td>
</tr>
<tr class="even">
<td>Finite value &lt; 0</td>
<td>Non-integer</td>
<td>Error</td>
</tr>
<tr class="odd">
<td>0</td>
<td>Finite value &lt; 0</td>
<td>Error</td>
</tr>
</tbody>
</table>

**Return Data Type**

The return data type is determined by the argument types with the following table.

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

## `     POWER    `

``` text
POWER(X, Y)
```

**Description**

Synonym of [`  POW(X, Y)  `](#pow) .

## `     RAND    `

``` text
RAND()
```

**Description**

Generates a pseudo-random value of type `  FLOAT64  ` in the range of \[0, 1), inclusive of 0 and exclusive of 1.

## `     RANGE_BUCKET    `

``` text
RANGE_BUCKET(point, boundaries_array)
```

**Description**

`  RANGE_BUCKET  ` scans through a sorted array and returns the 0-based position of the point's upper bound. This can be useful if you need to group your data to build partitions, histograms, business-defined rules, and more.

`  RANGE_BUCKET  ` follows these rules:

  - If the point exists in the array, returns the index of the next larger value.
    
    ``` text
    RANGE_BUCKET(20, [0, 10, 20, 30, 40]) -- 3 is return value
    RANGE_BUCKET(20, [0, 10, 20, 20, 40, 40]) -- 4 is return value
    ```

  - If the point doesn't exist in the array, but it falls between two values, returns the index of the larger value.
    
    ``` text
    RANGE_BUCKET(25, [0, 10, 20, 30, 40]) -- 3 is return value
    ```

  - If the point is smaller than the first value in the array, returns 0.
    
    ``` text
    RANGE_BUCKET(-10, [5, 10, 20, 30, 40]) -- 0 is return value
    ```

  - If the point is greater than or equal to the last value in the array, returns the length of the array.
    
    ``` text
    RANGE_BUCKET(80, [0, 10, 20, 30, 40]) -- 5 is return value
    ```

  - If the array is empty, returns 0.
    
    ``` text
    RANGE_BUCKET(80, []) -- 0 is return value
    ```

  - If the point is `  NULL  ` or `  NaN  ` , returns `  NULL  ` .
    
    ``` text
    RANGE_BUCKET(NULL, [0, 10, 20, 30, 40]) -- NULL is return value
    ```

  - The data type for the point and array must be compatible.
    
    ``` text
    RANGE_BUCKET('a', ['a', 'b', 'c', 'd']) -- 1 is return value
    RANGE_BUCKET(1.2, [1, 1.2, 1.4, 1.6]) -- 2 is return value
    RANGE_BUCKET(1.2, [1, 2, 4, 6]) -- execution failure
    ```

Execution failure occurs when:

  - The array has a `  NaN  ` or `  NULL  ` value in it.
    
    ``` text
    RANGE_BUCKET(80, [NULL, 10, 20, 30, 40]) -- execution failure
    ```

  - The array isn't sorted in ascending order.
    
    ``` text
    RANGE_BUCKET(30, [10, 30, 20, 40, 50]) -- execution failure
    ```

**Parameters**

  - `  point  ` : A generic value.
  - `  boundaries_array  ` : A generic array of values.

**Note:** The data type for `  point  ` and the element type of `  boundaries_array  ` must be equivalent. The data type must be [comparable](/bigquery/docs/reference/standard-sql/data-types#data_type_properties) .

**Return Value**

`  INT64  `

**Examples**

In a table called `  students  ` , check to see how many records would exist in each `  age_group  ` bucket, based on a student's age:

  - age\_group 0 (age \< 10)
  - age\_group 1 (age \>= 10, age \< 20)
  - age\_group 2 (age \>= 20, age \< 30)
  - age\_group 3 (age \>= 30)

<!-- end list -->

``` text
WITH students AS
(
  SELECT 9 AS age UNION ALL
  SELECT 20 AS age UNION ALL
  SELECT 25 AS age UNION ALL
  SELECT 31 AS age UNION ALL
  SELECT 32 AS age UNION ALL
  SELECT 33 AS age
)
SELECT RANGE_BUCKET(age, [10, 20, 30]) AS age_group, COUNT(*) AS count
FROM students
GROUP BY 1

/*--------------+-------+
 | age_group    | count |
 +--------------+-------+
 | 0            | 1     |
 | 2            | 2     |
 | 3            | 3     |
 +--------------+-------*/
```

## `     ROUND    `

``` text
ROUND(X [, N [, rounding_mode]])
```

**Description**

If only X is present, rounds X to the nearest integer. If N is present, rounds X to N decimal places after the decimal point. If N is negative, rounds off digits to the left of the decimal point. Rounds halfway cases away from zero. Generates an error if overflow occurs.

If X is a `  NUMERIC  ` or `  BIGNUMERIC  ` type, then you can explicitly set `  rounding_mode  ` to one of the following:

  - [`  "ROUND_HALF_AWAY_FROM_ZERO"  `](https://en.wikipedia.org/wiki/Rounding#Rounding_half_away_from_zero) : (Default) Rounds halfway cases away from zero.
  - [`  "ROUND_HALF_EVEN"  `](https://en.wikipedia.org/wiki/Rounding#Rounding_half_to_even) : Rounds halfway cases towards the nearest even digit.

If you set the `  rounding_mode  ` and X isn't a `  NUMERIC  ` or `  BIGNUMERIC  ` type, then the function generates an error.

<table>
<thead>
<tr class="header">
<th>Expression</th>
<th>Return Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       ROUND(2.0)      </code></td>
<td>2.0</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ROUND(2.3)      </code></td>
<td>2.0</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       ROUND(2.8)      </code></td>
<td>3.0</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ROUND(2.5)      </code></td>
<td>3.0</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       ROUND(-2.3)      </code></td>
<td>-2.0</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ROUND(-2.8)      </code></td>
<td>-3.0</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       ROUND(-2.5)      </code></td>
<td>-3.0</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ROUND(0)      </code></td>
<td>0</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       ROUND(+inf)      </code></td>
<td><code dir="ltr" translate="no">       +inf      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ROUND(-inf)      </code></td>
<td><code dir="ltr" translate="no">       -inf      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       ROUND(NaN)      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ROUND(123.7, -1)      </code></td>
<td>120.0</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       ROUND(1.235, 2)      </code></td>
<td>1.24</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ROUND(NUMERIC "2.25", 1, "ROUND_HALF_EVEN")      </code></td>
<td>2.2</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       ROUND(NUMERIC "2.35", 1, "ROUND_HALF_EVEN")      </code></td>
<td>2.4</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ROUND(NUMERIC "2.251", 1, "ROUND_HALF_EVEN")      </code></td>
<td>2.3</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       ROUND(NUMERIC "-2.5", 0, "ROUND_HALF_EVEN")      </code></td>
<td>-2</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ROUND(NUMERIC "2.5", 0, "ROUND_HALF_AWAY_FROM_ZERO")      </code></td>
<td>3</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       ROUND(NUMERIC "-2.5", 0, "ROUND_HALF_AWAY_FROM_ZERO")      </code></td>
<td>-3</td>
</tr>
</tbody>
</table>

**Return Data Type**

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
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
</tr>
</tbody>
</table>

## `     SAFE_ADD    `

``` text
SAFE_ADD(X, Y)
```

**Description**

Equivalent to the addition operator ( `  +  ` ), but returns `  NULL  ` if overflow occurs.

<table>
<thead>
<tr class="header">
<th>X</th>
<th>Y</th>
<th>SAFE_ADD(X, Y)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>5</td>
<td>4</td>
<td>9</td>
</tr>
</tbody>
</table>

**Return Data Type**

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

## `     SAFE_DIVIDE    `

``` text
SAFE_DIVIDE(X, Y)
```

**Description**

Equivalent to the division operator ( `  X / Y  ` ), but returns `  NULL  ` if an error occurs, such as a division by zero error.

<table>
<thead>
<tr class="header">
<th>X</th>
<th>Y</th>
<th>SAFE_DIVIDE(X, Y)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>20</td>
<td>4</td>
<td>5</td>
</tr>
<tr class="even">
<td>0</td>
<td>20</td>
<td><code dir="ltr" translate="no">       0      </code></td>
</tr>
<tr class="odd">
<td>20</td>
<td>0</td>
<td><code dir="ltr" translate="no">       NULL      </code></td>
</tr>
</tbody>
</table>

**Return Data Type**

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

## `     SAFE_MULTIPLY    `

``` text
SAFE_MULTIPLY(X, Y)
```

**Description**

Equivalent to the multiplication operator ( `  *  ` ), but returns `  NULL  ` if overflow occurs.

<table>
<thead>
<tr class="header">
<th>X</th>
<th>Y</th>
<th>SAFE_MULTIPLY(X, Y)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>20</td>
<td>4</td>
<td>80</td>
</tr>
</tbody>
</table>

**Return Data Type**

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

## `     SAFE_NEGATE    `

``` text
SAFE_NEGATE(X)
```

**Description**

Equivalent to the unary minus operator ( `  -  ` ), but returns `  NULL  ` if overflow occurs.

<table>
<thead>
<tr class="header">
<th>X</th>
<th>SAFE_NEGATE(X)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>+1</td>
<td>-1</td>
</tr>
<tr class="even">
<td>-1</td>
<td>+1</td>
</tr>
<tr class="odd">
<td>0</td>
<td>0</td>
</tr>
</tbody>
</table>

**Return Data Type**

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

## `     SAFE_SUBTRACT    `

``` text
SAFE_SUBTRACT(X, Y)
```

**Description**

Returns the result of Y subtracted from X. Equivalent to the subtraction operator ( `  -  ` ), but returns `  NULL  ` if overflow occurs.

<table>
<thead>
<tr class="header">
<th>X</th>
<th>Y</th>
<th>SAFE_SUBTRACT(X, Y)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>5</td>
<td>4</td>
<td>1</td>
</tr>
</tbody>
</table>

**Return Data Type**

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

## `     SEC    `

``` text
SEC(X)
```

**Description**

Computes the secant for the angle of `  X  ` , where `  X  ` is specified in radians. `  X  ` can be any data type that [coerces to `  FLOAT64  `](/bigquery/docs/reference/standard-sql/conversion_rules) .

<table>
<thead>
<tr class="header">
<th>X</th>
<th>SEC(X)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       +inf      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       -inf      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       NaN      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       NULL      </code></td>
<td><code dir="ltr" translate="no">       NULL      </code></td>
</tr>
</tbody>
</table>

**Return Data Type**

`  FLOAT64  `

**Example**

``` text
SELECT SEC(100) AS a, SEC(-1) AS b;

/*----------------+---------------+
 | a              | b             |
 +----------------+---------------+
 | 1.159663822905 | 1.85081571768 |
 +----------------+---------------*/
```

## `     SECH    `

``` text
SECH(X)
```

**Description**

Computes the hyperbolic secant for the angle of `  X  ` , where `  X  ` is specified in radians. `  X  ` can be any data type that [coerces to `  FLOAT64  `](/bigquery/docs/reference/standard-sql/conversion_rules) . Never produces an error.

<table>
<thead>
<tr class="header">
<th>X</th>
<th>SECH(X)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       +inf      </code></td>
<td><code dir="ltr" translate="no">       0      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       -inf      </code></td>
<td><code dir="ltr" translate="no">       0      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       NaN      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       NULL      </code></td>
<td><code dir="ltr" translate="no">       NULL      </code></td>
</tr>
</tbody>
</table>

**Return Data Type**

`  FLOAT64  `

**Example**

``` text
SELECT SECH(0.5) AS a, SECH(-2) AS b, SECH(100) AS c;

/*----------------+----------------+---------------------+
 | a              | b              | c                   |
 +----------------+----------------+---------------------+
 | 0.88681888397  | 0.265802228834 | 7.4401519520417E-44 |
 +----------------+----------------+---------------------*/
```

## `     SIGN    `

``` text
SIGN(X)
```

**Description**

Returns `  -1  ` , `  0  ` , or `  +1  ` for negative, zero and positive arguments respectively. For floating point arguments, this function doesn't distinguish between positive and negative zero.

<table>
<thead>
<tr class="header">
<th>X</th>
<th>SIGN(X)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>25</td>
<td>+1</td>
</tr>
<tr class="even">
<td>0</td>
<td>0</td>
</tr>
<tr class="odd">
<td>-25</td>
<td>-1</td>
</tr>
<tr class="even">
<td>NaN</td>
<td>NaN</td>
</tr>
</tbody>
</table>

**Return Data Type**

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

## `     SIN    `

``` text
SIN(X)
```

**Description**

Computes the sine of X where X is specified in radians. Never fails.

<table>
<thead>
<tr class="header">
<th>X</th>
<th>SIN(X)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       +inf      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       -inf      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       NaN      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
</tbody>
</table>

## `     SINH    `

``` text
SINH(X)
```

**Description**

Computes the hyperbolic sine of X where X is specified in radians. Generates an error if overflow occurs.

<table>
<thead>
<tr class="header">
<th>X</th>
<th>SINH(X)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       +inf      </code></td>
<td><code dir="ltr" translate="no">       +inf      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       -inf      </code></td>
<td><code dir="ltr" translate="no">       -inf      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       NaN      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
</tbody>
</table>

## `     SQRT    `

``` text
SQRT(X)
```

**Description**

Computes the square root of X. Generates an error if X is less than 0.

<table>
<thead>
<tr class="header">
<th>X</th>
<th>SQRT(X)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       25.0      </code></td>
<td><code dir="ltr" translate="no">       5.0      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       +inf      </code></td>
<td><code dir="ltr" translate="no">       +inf      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       X &lt; 0      </code></td>
<td>Error</td>
</tr>
</tbody>
</table>

**Return Data Type**

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
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
</tr>
</tbody>
</table>

## `     TAN    `

``` text
TAN(X)
```

**Description**

Computes the tangent of X where X is specified in radians. Generates an error if overflow occurs.

<table>
<thead>
<tr class="header">
<th>X</th>
<th>TAN(X)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       +inf      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       -inf      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       NaN      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
</tbody>
</table>

## `     TANH    `

``` text
TANH(X)
```

**Description**

Computes the hyperbolic tangent of X where X is specified in radians. Doesn't fail.

<table>
<thead>
<tr class="header">
<th>X</th>
<th>TANH(X)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       +inf      </code></td>
<td>1.0</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       -inf      </code></td>
<td>-1.0</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       NaN      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
</tbody>
</table>

## `     TRUNC    `

``` text
TRUNC(X [, N])
```

**Description**

If only X is present, `  TRUNC  ` rounds X to the nearest integer whose absolute value isn't greater than the absolute value of X. If N is also present, `  TRUNC  ` behaves like `  ROUND(X, N)  ` , but always rounds towards zero and never overflows.

<table>
<thead>
<tr class="header">
<th>X</th>
<th>TRUNC(X)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>2.0</td>
<td>2.0</td>
</tr>
<tr class="even">
<td>2.3</td>
<td>2.0</td>
</tr>
<tr class="odd">
<td>2.8</td>
<td>2.0</td>
</tr>
<tr class="even">
<td>2.5</td>
<td>2.0</td>
</tr>
<tr class="odd">
<td>-2.3</td>
<td>-2.0</td>
</tr>
<tr class="even">
<td>-2.8</td>
<td>-2.0</td>
</tr>
<tr class="odd">
<td>-2.5</td>
<td>-2.0</td>
</tr>
<tr class="even">
<td>0</td>
<td>0</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       +inf      </code></td>
<td><code dir="ltr" translate="no">       +inf      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       -inf      </code></td>
<td><code dir="ltr" translate="no">       -inf      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       NaN      </code></td>
<td><code dir="ltr" translate="no">       NaN      </code></td>
</tr>
</tbody>
</table>

**Return Data Type**

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
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
</tr>
</tbody>
</table>
