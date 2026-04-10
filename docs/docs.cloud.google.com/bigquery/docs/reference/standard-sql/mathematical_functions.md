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
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#acos"><code dir="ltr" translate="no">        ACOS       </code></a> <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#acosh"><code dir="ltr" translate="no">        ACOSH       </code></a> <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#asin"><code dir="ltr" translate="no">        ASIN       </code></a> <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#asinh"><code dir="ltr" translate="no">        ASINH       </code></a> <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#atan"><code dir="ltr" translate="no">        ATAN       </code></a> <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#atan2"><code dir="ltr" translate="no">        ATAN2       </code></a> <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#atanh"><code dir="ltr" translate="no">        ATANH       </code></a> <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#cos"><code dir="ltr" translate="no">        COS       </code></a> <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#cosh"><code dir="ltr" translate="no">        COSH       </code></a> <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#cot"><code dir="ltr" translate="no">        COT       </code></a> <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#coth"><code dir="ltr" translate="no">        COTH       </code></a> <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#csc"><code dir="ltr" translate="no">        CSC       </code></a> <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#csch"><code dir="ltr" translate="no">        CSCH       </code></a> <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#sec"><code dir="ltr" translate="no">        SEC       </code></a> <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#sech"><code dir="ltr" translate="no">        SECH       </code></a> <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#sin"><code dir="ltr" translate="no">        SIN       </code></a> <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#sinh"><code dir="ltr" translate="no">        SINH       </code></a> <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#tan"><code dir="ltr" translate="no">        TAN       </code></a> <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#tanh"><code dir="ltr" translate="no">        TANH       </code></a></td>
</tr>
<tr class="even">
<td>Exponential and<br />
logarithmic</td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#exp"><code dir="ltr" translate="no">        EXP       </code></a> <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#ln"><code dir="ltr" translate="no">        LN       </code></a> <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#log"><code dir="ltr" translate="no">        LOG       </code></a> <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#log10"><code dir="ltr" translate="no">        LOG10       </code></a></td>
</tr>
<tr class="odd">
<td>Rounding and<br />
truncation</td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#ceil"><code dir="ltr" translate="no">        CEIL       </code></a> <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#ceiling"><code dir="ltr" translate="no">        CEILING       </code></a> <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#floor"><code dir="ltr" translate="no">        FLOOR       </code></a> <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#round"><code dir="ltr" translate="no">        ROUND       </code></a> <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#trunc"><code dir="ltr" translate="no">        TRUNC       </code></a></td>
</tr>
<tr class="even">
<td>Power and<br />
root</td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#cbrt"><code dir="ltr" translate="no">        CBRT       </code></a> <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#pow"><code dir="ltr" translate="no">        POW       </code></a> <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#power"><code dir="ltr" translate="no">        POWER       </code></a> <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#sqrt"><code dir="ltr" translate="no">        SQRT       </code></a></td>
</tr>
<tr class="odd">
<td>Sign</td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#abs"><code dir="ltr" translate="no">        ABS       </code></a> <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#sign"><code dir="ltr" translate="no">        SIGN       </code></a></td>
</tr>
<tr class="even">
<td>Distance</td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#cosine_distance"><code dir="ltr" translate="no">        COSINE_DISTANCE       </code></a> <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#euclidean_distance"><code dir="ltr" translate="no">        EUCLIDEAN_DISTANCE       </code></a></td>
</tr>
<tr class="odd">
<td>Comparison</td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#greatest"><code dir="ltr" translate="no">        GREATEST       </code></a> <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#least"><code dir="ltr" translate="no">        LEAST       </code></a></td>
</tr>
<tr class="even">
<td>Random number generator</td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#rand"><code dir="ltr" translate="no">        RAND       </code></a></td>
</tr>
<tr class="odd">
<td>Arithmetic and error handling</td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#div"><code dir="ltr" translate="no">        DIV       </code></a> <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#ieee_divide"><code dir="ltr" translate="no">        IEEE_DIVIDE       </code></a> <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#is_inf"><code dir="ltr" translate="no">        IS_INF       </code></a> <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#is_nan"><code dir="ltr" translate="no">        IS_NAN       </code></a> <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#mod"><code dir="ltr" translate="no">        MOD       </code></a> <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#safe_add"><code dir="ltr" translate="no">        SAFE_ADD       </code></a> <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#safe_divide"><code dir="ltr" translate="no">        SAFE_DIVIDE       </code></a> <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#safe_multiply"><code dir="ltr" translate="no">        SAFE_MULTIPLY       </code></a> <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#safe_negate"><code dir="ltr" translate="no">        SAFE_NEGATE       </code></a> <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#safe_subtract"><code dir="ltr" translate="no">        SAFE_SUBTRACT       </code></a></td>
</tr>
<tr class="even">
<td>Bucket</td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#range_bucket"><code dir="ltr" translate="no">        RANGE_BUCKET       </code></a></td>
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
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#abs"><code dir="ltr" translate="no">        ABS       </code></a></td>
<td>Computes the absolute value of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#acos"><code dir="ltr" translate="no">        ACOS       </code></a></td>
<td>Computes the inverse cosine of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#acosh"><code dir="ltr" translate="no">        ACOSH       </code></a></td>
<td>Computes the inverse hyperbolic cosine of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#asin"><code dir="ltr" translate="no">        ASIN       </code></a></td>
<td>Computes the inverse sine of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#asinh"><code dir="ltr" translate="no">        ASINH       </code></a></td>
<td>Computes the inverse hyperbolic sine of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#atan"><code dir="ltr" translate="no">        ATAN       </code></a></td>
<td>Computes the inverse tangent of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#atan2"><code dir="ltr" translate="no">        ATAN2       </code></a></td>
<td>Computes the inverse tangent of <code dir="ltr" translate="no">       X/Y      </code> , using the signs of <code dir="ltr" translate="no">       X      </code> and <code dir="ltr" translate="no">       Y      </code> to determine the quadrant.</td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#atanh"><code dir="ltr" translate="no">        ATANH       </code></a></td>
<td>Computes the inverse hyperbolic tangent of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/aggregate_functions#avg"><code dir="ltr" translate="no">        AVG       </code></a></td>
<td>Gets the average of non- <code dir="ltr" translate="no">       NULL      </code> values.<br />
For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/aggregate_functions">Aggregate functions</a> .</td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/aggregate-dp-functions#dp_avg"><code dir="ltr" translate="no">        AVG       </code> (Differential Privacy)</a></td>
<td><code dir="ltr" translate="no">       DIFFERENTIAL_PRIVACY      </code> -supported <code dir="ltr" translate="no">       AVG      </code> .<br />
<br />
Gets the differentially-private average of non- <code dir="ltr" translate="no">       NULL      </code> , non- <code dir="ltr" translate="no">       NaN      </code> values in a query with a <code dir="ltr" translate="no">       DIFFERENTIAL_PRIVACY      </code> clause.<br />
<br />
For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/aggregate-dp-functions">Differential privacy functions</a> .</td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#cbrt"><code dir="ltr" translate="no">        CBRT       </code></a></td>
<td>Computes the cube root of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#ceil"><code dir="ltr" translate="no">        CEIL       </code></a></td>
<td>Gets the smallest integral value that isn't less than <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#ceiling"><code dir="ltr" translate="no">        CEILING       </code></a></td>
<td>Synonym of <code dir="ltr" translate="no">       CEIL      </code> .</td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#cos"><code dir="ltr" translate="no">        COS       </code></a></td>
<td>Computes the cosine of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#cosh"><code dir="ltr" translate="no">        COSH       </code></a></td>
<td>Computes the hyperbolic cosine of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#cosine_distance"><code dir="ltr" translate="no">        COSINE_DISTANCE       </code></a></td>
<td>Computes the cosine distance between two vectors.</td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#cot"><code dir="ltr" translate="no">        COT       </code></a></td>
<td>Computes the cotangent of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#coth"><code dir="ltr" translate="no">        COTH       </code></a></td>
<td>Computes the hyperbolic cotangent of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#csc"><code dir="ltr" translate="no">        CSC       </code></a></td>
<td>Computes the cosecant of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#csch"><code dir="ltr" translate="no">        CSCH       </code></a></td>
<td>Computes the hyperbolic cosecant of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#div"><code dir="ltr" translate="no">        DIV       </code></a></td>
<td>Divides integer <code dir="ltr" translate="no">       X      </code> by integer <code dir="ltr" translate="no">       Y      </code> .</td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#exp"><code dir="ltr" translate="no">        EXP       </code></a></td>
<td>Computes <code dir="ltr" translate="no">       e      </code> to the power of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#euclidean_distance"><code dir="ltr" translate="no">        EUCLIDEAN_DISTANCE       </code></a></td>
<td>Computes the Euclidean distance between two vectors.</td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#floor"><code dir="ltr" translate="no">        FLOOR       </code></a></td>
<td>Gets the largest integral value that isn't greater than <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#greatest"><code dir="ltr" translate="no">        GREATEST       </code></a></td>
<td>Gets the greatest value among <code dir="ltr" translate="no">       X1,...,XN      </code> .</td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#ieee_divide"><code dir="ltr" translate="no">        IEEE_DIVIDE       </code></a></td>
<td>Divides <code dir="ltr" translate="no">       X      </code> by <code dir="ltr" translate="no">       Y      </code> , but doesn't generate errors for division by zero or overflow.</td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#is_inf"><code dir="ltr" translate="no">        IS_INF       </code></a></td>
<td>Checks if <code dir="ltr" translate="no">       X      </code> is positive or negative infinity.</td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#is_nan"><code dir="ltr" translate="no">        IS_NAN       </code></a></td>
<td>Checks if <code dir="ltr" translate="no">       X      </code> is a <code dir="ltr" translate="no">       NaN      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#least"><code dir="ltr" translate="no">        LEAST       </code></a></td>
<td>Gets the least value among <code dir="ltr" translate="no">       X1,...,XN      </code> .</td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#ln"><code dir="ltr" translate="no">        LN       </code></a></td>
<td>Computes the natural logarithm of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#log"><code dir="ltr" translate="no">        LOG       </code></a></td>
<td>Computes the natural logarithm of <code dir="ltr" translate="no">       X      </code> or the logarithm of <code dir="ltr" translate="no">       X      </code> to base <code dir="ltr" translate="no">       Y      </code> .</td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#log10"><code dir="ltr" translate="no">        LOG10       </code></a></td>
<td>Computes the natural logarithm of <code dir="ltr" translate="no">       X      </code> to base 10.</td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/aggregate_functions#max"><code dir="ltr" translate="no">        MAX       </code></a></td>
<td>Gets the maximum non- <code dir="ltr" translate="no">       NULL      </code> value.<br />
For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/aggregate_functions">Aggregate functions</a> .</td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/aggregate_functions#max_by"><code dir="ltr" translate="no">        MAX_BY       </code></a></td>
<td>Synonym for <code dir="ltr" translate="no">       ANY_VALUE(x HAVING MAX y)      </code> .<br />
For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/aggregate_functions">Aggregate functions</a> .</td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/aggregate_functions#min_by"><code dir="ltr" translate="no">        MIN_BY       </code></a></td>
<td>Synonym for <code dir="ltr" translate="no">       ANY_VALUE(x HAVING MIN y)      </code> .<br />
For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/aggregate_functions">Aggregate functions</a> .</td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#mod"><code dir="ltr" translate="no">        MOD       </code></a></td>
<td>Gets the remainder of the division of <code dir="ltr" translate="no">       X      </code> by <code dir="ltr" translate="no">       Y      </code> .</td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#pow"><code dir="ltr" translate="no">        POW       </code></a></td>
<td>Produces the value of <code dir="ltr" translate="no">       X      </code> raised to the power of <code dir="ltr" translate="no">       Y      </code> .</td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#power"><code dir="ltr" translate="no">        POWER       </code></a></td>
<td>Synonym of <code dir="ltr" translate="no">       POW      </code> .</td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#rand"><code dir="ltr" translate="no">        RAND       </code></a></td>
<td>Generates a pseudo-random value of type <code dir="ltr" translate="no">       FLOAT64      </code> in the range of <code dir="ltr" translate="no">       [0, 1)      </code> .</td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#range_bucket"><code dir="ltr" translate="no">        RANGE_BUCKET       </code></a></td>
<td>Scans through a sorted array and returns the 0-based position of a point's upper bound.</td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#round"><code dir="ltr" translate="no">        ROUND       </code></a></td>
<td>Rounds <code dir="ltr" translate="no">       X      </code> to the nearest integer or rounds <code dir="ltr" translate="no">       X      </code> to <code dir="ltr" translate="no">       N      </code> decimal places after the decimal point.</td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#safe_add"><code dir="ltr" translate="no">        SAFE_ADD       </code></a></td>
<td>Equivalent to the addition operator ( <code dir="ltr" translate="no">       X + Y      </code> ), but returns <code dir="ltr" translate="no">       NULL      </code> if overflow occurs.</td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#safe_divide"><code dir="ltr" translate="no">        SAFE_DIVIDE       </code></a></td>
<td>Equivalent to the division operator ( <code dir="ltr" translate="no">       X / Y      </code> ), but returns <code dir="ltr" translate="no">       NULL      </code> if an error occurs.</td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#safe_multiply"><code dir="ltr" translate="no">        SAFE_MULTIPLY       </code></a></td>
<td>Equivalent to the multiplication operator ( <code dir="ltr" translate="no">       X * Y      </code> ), but returns <code dir="ltr" translate="no">       NULL      </code> if overflow occurs.</td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#safe_negate"><code dir="ltr" translate="no">        SAFE_NEGATE       </code></a></td>
<td>Equivalent to the unary minus operator ( <code dir="ltr" translate="no">       -X      </code> ), but returns <code dir="ltr" translate="no">       NULL      </code> if overflow occurs.</td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#safe_subtract"><code dir="ltr" translate="no">        SAFE_SUBTRACT       </code></a></td>
<td>Equivalent to the subtraction operator ( <code dir="ltr" translate="no">       X - Y      </code> ), but returns <code dir="ltr" translate="no">       NULL      </code> if overflow occurs.</td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#sec"><code dir="ltr" translate="no">        SEC       </code></a></td>
<td>Computes the secant of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#sech"><code dir="ltr" translate="no">        SECH       </code></a></td>
<td>Computes the hyperbolic secant of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#sign"><code dir="ltr" translate="no">        SIGN       </code></a></td>
<td>Produces -1 , 0, or +1 for negative, zero, and positive arguments respectively.</td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#sin"><code dir="ltr" translate="no">        SIN       </code></a></td>
<td>Computes the sine of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#sinh"><code dir="ltr" translate="no">        SINH       </code></a></td>
<td>Computes the hyperbolic sine of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#sqrt"><code dir="ltr" translate="no">        SQRT       </code></a></td>
<td>Computes the square root of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/aggregate_functions#sum"><code dir="ltr" translate="no">        SUM       </code></a></td>
<td>Gets the sum of non- <code dir="ltr" translate="no">       NULL      </code> values.<br />
For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/aggregate_functions">Aggregate functions</a> .</td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/aggregate-dp-functions#dp_sum"><code dir="ltr" translate="no">        SUM       </code> (Differential Privacy)</a></td>
<td><code dir="ltr" translate="no">       DIFFERENTIAL_PRIVACY      </code> -supported <code dir="ltr" translate="no">       SUM      </code> .<br />
<br />
Gets the differentially-private sum of non- <code dir="ltr" translate="no">       NULL      </code> , non- <code dir="ltr" translate="no">       NaN      </code> values in a query with a <code dir="ltr" translate="no">       DIFFERENTIAL_PRIVACY      </code> clause.<br />
<br />
For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/aggregate-dp-functions">Differential privacy functions</a> .</td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#tan"><code dir="ltr" translate="no">        TAN       </code></a></td>
<td>Computes the tangent of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#tanh"><code dir="ltr" translate="no">        TANH       </code></a></td>
<td>Computes the hyperbolic tangent of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#trunc"><code dir="ltr" translate="no">        TRUNC       </code></a></td>
<td>Rounds a number like <code dir="ltr" translate="no">       ROUND(X)      </code> or <code dir="ltr" translate="no">       ROUND(X, N)      </code> , but always rounds towards zero and never overflows.</td>
</tr>
</tbody>
</table>

## `     ABS    `

    ABS(X)

**Description**

Computes absolute value. Returns an error if the argument is an integer and the output value can't be represented as the same type; this happens only for the largest negative input value, which has no positive representation.

| X                     | ABS(X)                |
| --------------------- | --------------------- |
| 25                    | 25                    |
| \-25                  | 25                    |
| `        +inf       ` | `        +inf       ` |
| `        -inf       ` | `        +inf       ` |

**Return Data Type**

| INPUT  | `        INT64       ` | `        NUMERIC       ` | `        BIGNUMERIC       ` | `        FLOAT64       ` |
| ------ | ---------------------- | ------------------------ | --------------------------- | ------------------------ |
| OUTPUT | `        INT64       ` | `        NUMERIC       ` | `        BIGNUMERIC       ` | `        FLOAT64       ` |

## `     ACOS    `

    ACOS(X)

**Description**

Computes the principal value of the inverse cosine of X. The return value is in the range \[0,π\]. Generates an error if X is a value outside of the range \[-1, 1\].

| X                     | ACOS(X)              |
| --------------------- | -------------------- |
| `        +inf       ` | `        NaN       ` |
| `        -inf       ` | `        NaN       ` |
| `        NaN       `  | `        NaN       ` |
| X \< -1               | Error                |
| X \> 1                | Error                |

## `     ACOSH    `

    ACOSH(X)

**Description**

Computes the inverse hyperbolic cosine of X. Generates an error if X is a value less than 1.

| X                     | ACOSH(X)              |
| --------------------- | --------------------- |
| `        +inf       ` | `        +inf       ` |
| `        -inf       ` | `        NaN       `  |
| `        NaN       `  | `        NaN       `  |
| X \< 1                | Error                 |

## `     ASIN    `

    ASIN(X)

**Description**

Computes the principal value of the inverse sine of X. The return value is in the range \[-π/2,π/2\]. Generates an error if X is outside of the range \[-1, 1\].

| X                     | ASIN(X)              |
| --------------------- | -------------------- |
| `        +inf       ` | `        NaN       ` |
| `        -inf       ` | `        NaN       ` |
| `        NaN       `  | `        NaN       ` |
| X \< -1               | Error                |
| X \> 1                | Error                |

## `     ASINH    `

    ASINH(X)

**Description**

Computes the inverse hyperbolic sine of X. Doesn't fail.

| X                     | ASINH(X)              |
| --------------------- | --------------------- |
| `        +inf       ` | `        +inf       ` |
| `        -inf       ` | `        -inf       ` |
| `        NaN       `  | `        NaN       `  |

## `     ATAN    `

    ATAN(X)

**Description**

Computes the principal value of the inverse tangent of X. The return value is in the range \[-π/2,π/2\]. Doesn't fail.

| X                     | ATAN(X)              |
| --------------------- | -------------------- |
| `        +inf       ` | π/2                  |
| `        -inf       ` | \-π/2                |
| `        NaN       `  | `        NaN       ` |

## `     ATAN2    `

    ATAN2(X, Y)

**Description**

Calculates the principal value of the inverse tangent of X/Y using the signs of the two arguments to determine the quadrant. The return value is in the range \[-π,π\].

| X                     | Y                     | ATAN2(X, Y)          |
| --------------------- | --------------------- | -------------------- |
| `        NaN       `  | Any value             | `        NaN       ` |
| Any value             | `        NaN       `  | `        NaN       ` |
| 0.0                   | 0.0                   | 0.0                  |
| Positive Finite value | `        -inf       ` | π                    |
| Negative Finite value | `        -inf       ` | \-π                  |
| Finite value          | `        +inf       ` | 0.0                  |
| `        +inf       ` | Finite value          | π/2                  |
| `        -inf       ` | Finite value          | \-π/2                |
| `        +inf       ` | `        -inf       ` | ¾π                   |
| `        -inf       ` | `        -inf       ` | \-¾π                 |
| `        +inf       ` | `        +inf       ` | π/4                  |
| `        -inf       ` | `        +inf       ` | \-π/4                |

## `     ATANH    `

    ATANH(X)

**Description**

Computes the inverse hyperbolic tangent of X. Generates an error if X is outside of the range (-1, 1).

| X                     | ATANH(X)             |
| --------------------- | -------------------- |
| `        +inf       ` | `        NaN       ` |
| `        -inf       ` | `        NaN       ` |
| `        NaN       `  | `        NaN       ` |
| X \< -1               | Error                |
| X \> 1                | Error                |

## `     CBRT    `

    CBRT(X)

**Description**

Computes the cube root of `  X  ` . `  X  ` can be any data type that [coerces to `  FLOAT64  `](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/conversion_rules) . Supports the `  SAFE.  ` prefix.

| X                     | CBRT(X)               |
| --------------------- | --------------------- |
| `        +inf       ` | `        inf       `  |
| `        -inf       ` | `        -inf       ` |
| `        NaN       `  | `        NaN       `  |
| `        0       `    | `        0       `    |
| `        NULL       ` | `        NULL       ` |

**Return Data Type**

`  FLOAT64  `

**Example**

    SELECT CBRT(27) AS cube_root;
    
    /*--------------------+
     | cube_root          |
     +--------------------+
     | 3.0000000000000004 |
     +--------------------*/

## `     CEIL    `

    CEIL(X)

**Description**

Returns the smallest integral value that isn't less than X.

| X                     | CEIL(X)               |
| --------------------- | --------------------- |
| 2.0                   | 2.0                   |
| 2.3                   | 3.0                   |
| 2.8                   | 3.0                   |
| 2.5                   | 3.0                   |
| \-2.3                 | \-2.0                 |
| \-2.8                 | \-2.0                 |
| \-2.5                 | \-2.0                 |
| 0                     | 0                     |
| `        +inf       ` | `        +inf       ` |
| `        -inf       ` | `        -inf       ` |
| `        NaN       `  | `        NaN       `  |

**Return Data Type**

| INPUT  | `        INT64       `   | `        NUMERIC       ` | `        BIGNUMERIC       ` | `        FLOAT64       ` |
| ------ | ------------------------ | ------------------------ | --------------------------- | ------------------------ |
| OUTPUT | `        FLOAT64       ` | `        NUMERIC       ` | `        BIGNUMERIC       ` | `        FLOAT64       ` |

## `     CEILING    `

    CEILING(X)

**Description**

Synonym of CEIL(X)

## `     COS    `

    COS(X)

**Description**

Computes the cosine of X where X is specified in radians. Never fails.

| X                     | COS(X)               |
| --------------------- | -------------------- |
| `        +inf       ` | `        NaN       ` |
| `        -inf       ` | `        NaN       ` |
| `        NaN       `  | `        NaN       ` |

## `     COSH    `

    COSH(X)

**Description**

Computes the hyperbolic cosine of X where X is specified in radians. Generates an error if overflow occurs.

| X                     | COSH(X)               |
| --------------------- | --------------------- |
| `        +inf       ` | `        +inf       ` |
| `        -inf       ` | `        +inf       ` |
| `        NaN       `  | `        NaN       `  |

## `     COSINE_DISTANCE    `

    COSINE_DISTANCE(vector1, vector2)

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
    
        [10.0, 55.0, 40.0, 34.0]

  - `  ARRAY<STRUCT<dimension,magnitude>>  ` can be used to represent a sparse vector. With a sparse vector, you only need to include dimension-magnitude pairs for non-zero magnitudes. If a magnitude isn't present in the sparse vector, the magnitude is implicitly understood to be zero.
    
    For example, if you have a vector with 10,000 dimensions, but only 10 dimensions have non-zero magnitudes, then the vector is a sparse vector. As a result, it's more efficient to describe a sparse vector by only mentioning its non-zero magnitudes.
    
    In `  ARRAY<STRUCT<dimension,magnitude>>  ` , `  STRUCT<dimension,magnitude>  ` represents a dimension-magnitude pair for each non-zero magnitude in a sparse vector. These parts need to be included for each dimension-magnitude pair:
    
      - `  dimension  ` : A `  STRING  ` or `  INT64  ` value that represents a dimension in a vector.
    
      - `  magnitude  ` : A `  FLOAT64  ` value that represents a non-zero magnitude for a specific dimension in a vector.
    
    You don't need to include empty dimension-magnitude pairs in a sparse vector. For example, the following sparse vector and non-sparse vector are equivalent:
    
        -- sparse vector ARRAY<STRUCT<INT64, FLOAT64>>
        [(1, 10.0), (2, 30.0), (5, 40.0)]
    
        -- vector ARRAY<FLOAT64>
        [0.0, 10.0, 30.0, 0.0, 0.0, 40.0]
    
    In a sparse vector, dimension-magnitude pairs don't need to be in any particular order. The following sparse vectors are equivalent:
    
        [('a', 10.0), ('b', 30.0), ('d', 40.0)]
    
        [('d', 40.0), ('a', 10.0), ('b', 30.0)]

  - Both non-sparse vectors in this function must share the same dimensions, and if they don't, an error is produced.

  - A vector can't be a zero vector. A vector is a zero vector if it has no dimensions or all dimensions have a magnitude of `  0  ` , such as `  []  ` or `  [0.0, 0.0]  ` . If a zero vector is encountered, an error is produced.

  - An error is produced if a magnitude in a vector is `  NULL  ` .

  - If a vector is `  NULL  ` , `  NULL  ` is returned.

**Return type**

`  FLOAT64  `

**Examples**

In the following example, non-sparsevectors are used to compute the cosine distance:

    SELECT COSINE_DISTANCE([1.0, 2.0], [3.0, 4.0]) AS results;
    
    /*----------+
     | results  |
     +----------+
     | 0.016130 |
     +----------*/

In the following example, sparse vectors are used to compute the cosine distance:

    SELECT COSINE_DISTANCE(
     [(1, 1.0), (2, 2.0)],
     [(2, 4.0), (1, 3.0)]) AS results;
    
     /*----------+
      | results  |
      +----------+
      | 0.016130 |
      +----------*/

The ordering of numeric values in a vector doesn't impact the results produced by this function. For example these queries produce the same results even though the numeric values in each vector is in a different order:

    SELECT COSINE_DISTANCE([1.0, 2.0], [3.0, 4.0]) AS results;

    SELECT COSINE_DISTANCE([2.0, 1.0], [4.0, 3.0]) AS results;

    SELECT COSINE_DISTANCE([(1, 1.0), (2, 2.0)], [(1, 3.0), (2, 4.0)]) AS results;

``` 
 /*----------+
  | results  |
  +----------+
  | 0.016130 |
  +----------*/
```

In the following example, the function can't compute cosine distance against the first vector, which is a zero vector:

    -- ERROR
    SELECT COSINE_DISTANCE([0.0, 0.0], [3.0, 4.0]) AS results;

    -- ERROR
    SELECT COSINE_DISTANCE([(1, 0.0), (2, 0.0)], [(1, 3.0), (2, 4.0)]) AS results;

Both non-sparse vectors must have the same dimensions. If not, an error is produced. In the following example, the first vector has two dimensions and the second vector has three:

    -- ERROR
    SELECT COSINE_DISTANCE([9.0, 7.0], [8.0, 4.0, 5.0]) AS results;

If you use sparse vectors and you repeat a dimension, an error is produced:

    -- ERROR
    SELECT COSINE_DISTANCE(
      [(1, 9.0), (2, 7.0), (2, 8.0)], [(1, 8.0), (2, 4.0), (3, 5.0)]) AS results;

## `     COT    `

    COT(X)

**Description**

Computes the cotangent for the angle of `  X  ` , where `  X  ` is specified in radians. `  X  ` can be any data type that [coerces to `  FLOAT64  `](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/conversion_rules) . Supports the `  SAFE.  ` prefix.

| X                     | COT(X)                 |
| --------------------- | ---------------------- |
| `        +inf       ` | `        NaN       `   |
| `        -inf       ` | `        NaN       `   |
| `        NaN       `  | `        NaN       `   |
| `        0       `    | `        Error       ` |
| `        NULL       ` | `        NULL       `  |

**Return Data Type**

`  FLOAT64  `

**Example**

    SELECT COT(1) AS a, SAFE.COT(0) AS b;
    
    /*---------------------+------+
     | a                   | b    |
     +---------------------+------+
     | 0.64209261593433065 | NULL |
     +---------------------+------*/

## `     COTH    `

    COTH(X)

**Description**

Computes the hyperbolic cotangent for the angle of `  X  ` , where `  X  ` is specified in radians. `  X  ` can be any data type that [coerces to `  FLOAT64  `](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/conversion_rules) . Supports the `  SAFE.  ` prefix.

| X                     | COTH(X)                |
| --------------------- | ---------------------- |
| `        +inf       ` | `        1       `     |
| `        -inf       ` | `        -1       `    |
| `        NaN       `  | `        NaN       `   |
| `        0       `    | `        Error       ` |
| `        NULL       ` | `        NULL       `  |

**Return Data Type**

`  FLOAT64  `

**Example**

    SELECT COTH(1) AS a, SAFE.COTH(0) AS b;
    
    /*----------------+------+
     | a              | b    |
     +----------------+------+
     | 1.313035285499 | NULL |
     +----------------+------*/

## `     CSC    `

    CSC(X)

**Description**

Computes the cosecant of the input angle, which is in radians. `  X  ` can be any data type that [coerces to `  FLOAT64  `](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/conversion_rules) . Supports the `  SAFE.  ` prefix.

| X                     | CSC(X)                 |
| --------------------- | ---------------------- |
| `        +inf       ` | `        NaN       `   |
| `        -inf       ` | `        NaN       `   |
| `        NaN       `  | `        NaN       `   |
| `        0       `    | `        Error       ` |
| `        NULL       ` | `        NULL       `  |

**Return Data Type**

`  FLOAT64  `

**Example**

    SELECT CSC(100) AS a, CSC(-1) AS b, SAFE.CSC(0) AS c;
    
    /*----------------+-----------------+------+
     | a              | b               | c    |
     +----------------+-----------------+------+
     | -1.97485753142 | -1.188395105778 | NULL |
     +----------------+-----------------+------*/

## `     CSCH    `

    CSCH(X)

**Description**

Computes the hyperbolic cosecant of the input angle, which is in radians. `  X  ` can be any data type that [coerces to `  FLOAT64  `](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/conversion_rules) . Supports the `  SAFE.  ` prefix.

| X                     | CSCH(X)                |
| --------------------- | ---------------------- |
| `        +inf       ` | `        0       `     |
| `        -inf       ` | `        0       `     |
| `        NaN       `  | `        NaN       `   |
| `        0       `    | `        Error       ` |
| `        NULL       ` | `        NULL       `  |

**Return Data Type**

`  FLOAT64  `

**Example**

    SELECT CSCH(0.5) AS a, CSCH(-2) AS b, SAFE.CSCH(0) AS c;
    
    /*----------------+----------------+------+
     | a              | b              | c    |
     +----------------+----------------+------+
     | 1.919034751334 | -0.27572056477 | NULL |
     +----------------+----------------+------*/

## `     DIV    `

    DIV(X, Y)

**Description**

Returns the result of integer division of X by Y. Division by zero returns an error. Division by -1 may overflow.

| X  | Y   | DIV(X, Y) |
| -- | --- | --------- |
| 20 | 4   | 5         |
| 12 | \-7 | \-1       |
| 20 | 3   | 6         |
| 0  | 20  | 0         |
| 20 | 0   | Error     |

**Return Data Type**

The return data type is determined by the argument types with the following table.

| INPUT                       | `        INT64       `      | `        NUMERIC       `    | `        BIGNUMERIC       ` |
| --------------------------- | --------------------------- | --------------------------- | --------------------------- |
| `        INT64       `      | `        INT64       `      | `        NUMERIC       `    | `        BIGNUMERIC       ` |
| `        NUMERIC       `    | `        NUMERIC       `    | `        NUMERIC       `    | `        BIGNUMERIC       ` |
| `        BIGNUMERIC       ` | `        BIGNUMERIC       ` | `        BIGNUMERIC       ` | `        BIGNUMERIC       ` |

## `     EXP    `

    EXP(X)

**Description**

Computes *e* to the power of X, also called the natural exponential function. If the result underflows, this function returns a zero. Generates an error if the result overflows.

| X                     | EXP(X)                |
| --------------------- | --------------------- |
| 0.0                   | 1.0                   |
| `        +inf       ` | `        +inf       ` |
| `        -inf       ` | 0.0                   |

**Return Data Type**

| INPUT  | `        INT64       `   | `        NUMERIC       ` | `        BIGNUMERIC       ` | `        FLOAT64       ` |
| ------ | ------------------------ | ------------------------ | --------------------------- | ------------------------ |
| OUTPUT | `        FLOAT64       ` | `        NUMERIC       ` | `        BIGNUMERIC       ` | `        FLOAT64       ` |

## `     EUCLIDEAN_DISTANCE    `

    EUCLIDEAN_DISTANCE(vector1, vector2)

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
    
        [10.0, 55.0, 40.0, 34.0]

  - `  ARRAY<STRUCT<dimension,magnitude>>  ` can be used to represent a sparse vector. With a sparse vector, you only need to include dimension-magnitude pairs for non-zero magnitudes. If a magnitude isn't present in the sparse vector, the magnitude is implicitly understood to be zero.
    
    For example, if you have a vector with 10,000 dimensions, but only 10 dimensions have non-zero magnitudes, then the vector is a sparse vector. As a result, it's more efficient to describe a sparse vector by only mentioning its non-zero magnitudes.
    
    In `  ARRAY<STRUCT<dimension,magnitude>>  ` , `  STRUCT<dimension,magnitude>  ` represents a dimension-magnitude pair for each non-zero magnitude in a sparse vector. These parts need to be included for each dimension-magnitude pair:
    
      - `  dimension  ` : A `  STRING  ` or `  INT64  ` value that represents a dimension in a vector.
    
      - `  magnitude  ` : A `  FLOAT64  ` value that represents a non-zero magnitude for a specific dimension in a vector.
    
    You don't need to include empty dimension-magnitude pairs in a sparse vector. For example, the following sparse vector and non-sparse vector are equivalent:
    
        -- sparse vector ARRAY<STRUCT<INT64, FLOAT64>>
        [(1, 10.0), (2, 30.0), (5, 40.0)]
    
        -- vector ARRAY<FLOAT64>
        [0.0, 10.0, 30.0, 0.0, 0.0, 40.0]
    
    In a sparse vector, dimension-magnitude pairs don't need to be in any particular order. The following sparse vectors are equivalent:
    
        [('a', 10.0), ('b', 30.0), ('d', 40.0)]
    
        [('d', 40.0), ('a', 10.0), ('b', 30.0)]

  - Both non-sparse vectors in this function must share the same dimensions, and if they don't, an error is produced.

  - A vector can be a zero vector. A vector is a zero vector if it has no dimensions or all dimensions have a magnitude of `  0  ` , such as `  []  ` or `  [0.0, 0.0]  ` .

  - An error is produced if a magnitude in a vector is `  NULL  ` .

  - If a vector is `  NULL  ` , `  NULL  ` is returned.

**Return type**

`  FLOAT64  `

**Examples**

In the following example, non-sparse vectors are used to compute the Euclidean distance:

    SELECT EUCLIDEAN_DISTANCE([1.0, 2.0], [3.0, 4.0]) AS results;
    
    /*----------+
     | results  |
     +----------+
     | 2.828    |
     +----------*/

In the following example, sparse vectors are used to compute the Euclidean distance:

    SELECT EUCLIDEAN_DISTANCE(
     [(1, 1.0), (2, 2.0)],
     [(2, 4.0), (1, 3.0)]) AS results;
    
     /*----------+
      | results  |
      +----------+
      | 2.828    |
      +----------*/

The ordering of magnitudes in a vector doesn't impact the results produced by this function. For example these queries produce the same results even though the magnitudes in each vector is in a different order:

    SELECT EUCLIDEAN_DISTANCE([1.0, 2.0], [3.0, 4.0]);

    SELECT EUCLIDEAN_DISTANCE([2.0, 1.0], [4.0, 3.0]);

    SELECT EUCLIDEAN_DISTANCE([(1, 1.0), (2, 2.0)], [(1, 3.0), (2, 4.0)]) AS results;

``` 
 /*----------+
  | results  |
  +----------+
  | 2.828    |
  +----------*/
```

Both non-sparse vectors must have the same dimensions. If not, an error is produced. In the following example, the first vector has two dimensions and the second vector has three:

    -- ERROR
    SELECT EUCLIDEAN_DISTANCE([9.0, 7.0], [8.0, 4.0, 5.0]) AS results;

If you use sparse vectors and you repeat a dimension, an error is produced:

    -- ERROR
    SELECT EUCLIDEAN_DISTANCE(
      [(1, 9.0), (2, 7.0), (2, 8.0)], [(1, 8.0), (2, 4.0), (3, 5.0)]) AS results;

## `     FLOOR    `

    FLOOR(X)

**Description**

Returns the largest integral value that isn't greater than X.

| X                     | FLOOR(X)              |
| --------------------- | --------------------- |
| 2.0                   | 2.0                   |
| 2.3                   | 2.0                   |
| 2.8                   | 2.0                   |
| 2.5                   | 2.0                   |
| \-2.3                 | \-3.0                 |
| \-2.8                 | \-3.0                 |
| \-2.5                 | \-3.0                 |
| 0                     | 0                     |
| `        +inf       ` | `        +inf       ` |
| `        -inf       ` | `        -inf       ` |
| `        NaN       `  | `        NaN       `  |

**Return Data Type**

| INPUT  | `        INT64       `   | `        NUMERIC       ` | `        BIGNUMERIC       ` | `        FLOAT64       ` |
| ------ | ------------------------ | ------------------------ | --------------------------- | ------------------------ |
| OUTPUT | `        FLOAT64       ` | `        NUMERIC       ` | `        BIGNUMERIC       ` | `        FLOAT64       ` |

## `     GREATEST    `

    GREATEST(X1,...,XN)

**Description**

Returns the greatest value among `  X1,...,XN  ` . If any argument is `  NULL  ` , returns `  NULL  ` . Otherwise, in the case of floating-point arguments, if any argument is `  NaN  ` , returns `  NaN  ` . In all other cases, returns the value among `  X1,...,XN  ` that has the greatest value according to the ordering used by the `  ORDER BY  ` clause. The arguments `  X1, ..., XN  ` must be coercible to a common supertype, and the supertype must support ordering.

| X1,...,XN | GREATEST(X1,...,XN) |
| --------- | ------------------- |
| 3,5,1     | 5                   |

This function supports specifying [collation](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/collation-concepts) .

**Return Data Types**

Data type of the input values.

## `     IEEE_DIVIDE    `

    IEEE_DIVIDE(X, Y)

**Description**

Divides X by Y; this function never fails. Returns `  FLOAT64  ` . Unlike the division operator (/), this function doesn't generate errors for division by zero or overflow.

| X                     | Y                     | IEEE\_DIVIDE(X, Y)    |
| --------------------- | --------------------- | --------------------- |
| 20.0                  | 4.0                   | 5.0                   |
| 20.0                  | 6.0                   | 3.3333333333333335    |
| 0.0                   | 25.0                  | 0.0                   |
| 25.0                  | 0.0                   | `        +inf       ` |
| \-25.0                | 0.0                   | `        -inf       ` |
| 25.0                  | \-0.0                 | `        -inf       ` |
| 0.0                   | 0.0                   | `        NaN       `  |
| 0.0                   | `        NaN       `  | `        NaN       `  |
| `        NaN       `  | 0.0                   | `        NaN       `  |
| `        +inf       ` | `        +inf       ` | `        NaN       `  |
| `        -inf       ` | `        -inf       ` | `        NaN       `  |

## `     IS_INF    `

    IS_INF(X)

**Description**

Returns `  TRUE  ` if the value is positive or negative infinity.

| X                     | IS\_INF(X)             |
| --------------------- | ---------------------- |
| `        +inf       ` | `        TRUE       `  |
| `        -inf       ` | `        TRUE       `  |
| 25                    | `        FALSE       ` |

## `     IS_NAN    `

    IS_NAN(X)

**Description**

Returns `  TRUE  ` if the value is a `  NaN  ` value.

| X                    | IS\_NAN(X)             |
| -------------------- | ---------------------- |
| `        NaN       ` | `        TRUE       `  |
| 25                   | `        FALSE       ` |

## `     LEAST    `

    LEAST(X1,...,XN)

**Description**

Returns the least value among `  X1,...,XN  ` . If any argument is `  NULL  ` , returns `  NULL  ` . Otherwise, in the case of floating-point arguments, if any argument is `  NaN  ` , returns `  NaN  ` . In all other cases, returns the value among `  X1,...,XN  ` that has the least value according to the ordering used by the `  ORDER BY  ` clause. The arguments `  X1, ..., XN  ` must be coercible to a common supertype, and the supertype must support ordering.

| X1,...,XN | LEAST(X1,...,XN) |
| --------- | ---------------- |
| 3,5,1     | 1                |

This function supports specifying [collation](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/collation-concepts) .

**Return Data Types**

Data type of the input values.

## `     LN    `

    LN(X)

**Description**

Computes the natural logarithm of X. Generates an error if X is less than or equal to zero.

| X                       | LN(X)                 |
| ----------------------- | --------------------- |
| 1.0                     | 0.0                   |
| `        +inf       `   | `        +inf       ` |
| `        X <= 0       ` | Error                 |

**Return Data Type**

| INPUT  | `        INT64       `   | `        NUMERIC       ` | `        BIGNUMERIC       ` | `        FLOAT64       ` |
| ------ | ------------------------ | ------------------------ | --------------------------- | ------------------------ |
| OUTPUT | `        FLOAT64       ` | `        NUMERIC       ` | `        BIGNUMERIC       ` | `        FLOAT64       ` |

## `     LOG    `

    LOG(X [, Y])

**Description**

If only X is present, `  LOG  ` is a synonym of `  LN  ` . If Y is also present, `  LOG  ` computes the logarithm of X to base Y.

| X                     | Y                     | LOG(X, Y)             |
| --------------------- | --------------------- | --------------------- |
| 100.0                 | 10.0                  | 2.0                   |
| `        -inf       ` | Any value             | `        NaN       `  |
| Any value             | `        +inf       ` | `        NaN       `  |
| `        +inf       ` | 0.0 \< Y \< 1.0       | `        -inf       ` |
| `        +inf       ` | Y \> 1.0              | `        +inf       ` |
| X \<= 0               | Any value             | Error                 |
| Any value             | Y \<= 0               | Error                 |
| Any value             | 1.0                   | Error                 |

**Return Data Type**

| INPUT                       | `        INT64       `      | `        NUMERIC       `    | `        BIGNUMERIC       ` | `        FLOAT64       ` |
| --------------------------- | --------------------------- | --------------------------- | --------------------------- | ------------------------ |
| `        INT64       `      | `        FLOAT64       `    | `        NUMERIC       `    | `        BIGNUMERIC       ` | `        FLOAT64       ` |
| `        NUMERIC       `    | `        NUMERIC       `    | `        NUMERIC       `    | `        BIGNUMERIC       ` | `        FLOAT64       ` |
| `        BIGNUMERIC       ` | `        BIGNUMERIC       ` | `        BIGNUMERIC       ` | `        BIGNUMERIC       ` | `        FLOAT64       ` |
| `        FLOAT64       `    | `        FLOAT64       `    | `        FLOAT64       `    | `        FLOAT64       `    | `        FLOAT64       ` |

## `     LOG10    `

    LOG10(X)

**Description**

Similar to `  LOG  ` , but computes logarithm to base 10.

| X                     | LOG10(X)              |
| --------------------- | --------------------- |
| 100.0                 | 2.0                   |
| `        -inf       ` | `        NaN       `  |
| `        +inf       ` | `        +inf       ` |
| X \<= 0               | Error                 |

**Return Data Type**

| INPUT  | `        INT64       `   | `        NUMERIC       ` | `        BIGNUMERIC       ` | `        FLOAT64       ` |
| ------ | ------------------------ | ------------------------ | --------------------------- | ------------------------ |
| OUTPUT | `        FLOAT64       ` | `        NUMERIC       ` | `        BIGNUMERIC       ` | `        FLOAT64       ` |

## `     MOD    `

    MOD(X, Y)

**Description**

Modulo function: returns the remainder of the division of X by Y. Returned value has the same sign as X. An error is generated if Y is 0.

| X  | Y  | MOD(X, Y) |
| -- | -- | --------- |
| 25 | 12 | 1         |
| 25 | 0  | Error     |

**Return Data Type**

The return data type is determined by the argument types with the following table.

| INPUT                       | `        INT64       `      | `        NUMERIC       `    | `        BIGNUMERIC       ` |
| --------------------------- | --------------------------- | --------------------------- | --------------------------- |
| `        INT64       `      | `        INT64       `      | `        NUMERIC       `    | `        BIGNUMERIC       ` |
| `        NUMERIC       `    | `        NUMERIC       `    | `        NUMERIC       `    | `        BIGNUMERIC       ` |
| `        BIGNUMERIC       ` | `        BIGNUMERIC       ` | `        BIGNUMERIC       ` | `        BIGNUMERIC       ` |

## `     POW    `

    POW(X, Y)

**Description**

Returns the value of X raised to the power of Y. If the result underflows and isn't representable, then the function returns a value of zero.

| X                                        | Y                                        | POW(X, Y)                                                                     |
| ---------------------------------------- | ---------------------------------------- | ----------------------------------------------------------------------------- |
| 2.0                                      | 3.0                                      | 8.0                                                                           |
| 1.0                                      | Any value including `        NaN       ` | 1.0                                                                           |
| Any value including `        NaN       ` | 0                                        | 1.0                                                                           |
| \-1.0                                    | `        +inf       `                    | 1.0                                                                           |
| \-1.0                                    | `        -inf       `                    | 1.0                                                                           |
| ABS(X) \< 1                              | `        -inf       `                    | `        +inf       `                                                         |
| ABS(X) \> 1                              | `        -inf       `                    | 0.0                                                                           |
| ABS(X) \< 1                              | `        +inf       `                    | 0.0                                                                           |
| ABS(X) \> 1                              | `        +inf       `                    | `        +inf       `                                                         |
| `        -inf       `                    | Y \< 0                                   | 0.0                                                                           |
| `        -inf       `                    | Y \> 0                                   | `        -inf       ` if Y is an odd integer, `        +inf       ` otherwise |
| `        +inf       `                    | Y \< 0                                   | 0                                                                             |
| `        +inf       `                    | Y \> 0                                   | `        +inf       `                                                         |
| Finite value \< 0                        | Non-integer                              | Error                                                                         |
| 0                                        | Finite value \< 0                        | Error                                                                         |

**Return Data Type**

The return data type is determined by the argument types with the following table.

| INPUT                       | `        INT64       `      | `        NUMERIC       `    | `        BIGNUMERIC       ` | `        FLOAT64       ` |
| --------------------------- | --------------------------- | --------------------------- | --------------------------- | ------------------------ |
| `        INT64       `      | `        FLOAT64       `    | `        NUMERIC       `    | `        BIGNUMERIC       ` | `        FLOAT64       ` |
| `        NUMERIC       `    | `        NUMERIC       `    | `        NUMERIC       `    | `        BIGNUMERIC       ` | `        FLOAT64       ` |
| `        BIGNUMERIC       ` | `        BIGNUMERIC       ` | `        BIGNUMERIC       ` | `        BIGNUMERIC       ` | `        FLOAT64       ` |
| `        FLOAT64       `    | `        FLOAT64       `    | `        FLOAT64       `    | `        FLOAT64       `    | `        FLOAT64       ` |

## `     POWER    `

    POWER(X, Y)

**Description**

Synonym of [`  POW(X, Y)  `](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#pow) .

## `     RAND    `

    RAND()

**Description**

Generates a pseudo-random value of type `  FLOAT64  ` in the range of \[0, 1), inclusive of 0 and exclusive of 1.

## `     RANGE_BUCKET    `

    RANGE_BUCKET(point, boundaries_array)

**Description**

`  RANGE_BUCKET  ` scans through a sorted array and returns the 0-based position of the point's upper bound. This can be useful if you need to group your data to build partitions, histograms, business-defined rules, and more.

`  RANGE_BUCKET  ` follows these rules:

  - If the point exists in the array, returns the index of the next larger value.
    
        RANGE_BUCKET(20, [0, 10, 20, 30, 40]) -- 3 is return value
        RANGE_BUCKET(20, [0, 10, 20, 20, 40, 40]) -- 4 is return value

  - If the point doesn't exist in the array, but it falls between two values, returns the index of the larger value.
    
        RANGE_BUCKET(25, [0, 10, 20, 30, 40]) -- 3 is return value

  - If the point is smaller than the first value in the array, returns 0.
    
        RANGE_BUCKET(-10, [5, 10, 20, 30, 40]) -- 0 is return value

  - If the point is greater than or equal to the last value in the array, returns the length of the array.
    
        RANGE_BUCKET(80, [0, 10, 20, 30, 40]) -- 5 is return value

  - If the array is empty, returns 0.
    
        RANGE_BUCKET(80, []) -- 0 is return value

  - If the point is `  NULL  ` or `  NaN  ` , returns `  NULL  ` .
    
        RANGE_BUCKET(NULL, [0, 10, 20, 30, 40]) -- NULL is return value

  - The data type for the point and array must be compatible.
    
        RANGE_BUCKET('a', ['a', 'b', 'c', 'd']) -- 1 is return value
        RANGE_BUCKET(1.2, [1, 1.2, 1.4, 1.6]) -- 2 is return value
        RANGE_BUCKET(1.2, [1, 2, 4, 6]) -- execution failure

Execution failure occurs when:

  - The array has a `  NaN  ` or `  NULL  ` value in it.
    
        RANGE_BUCKET(80, [NULL, 10, 20, 30, 40]) -- execution failure

  - The array isn't sorted in ascending order.
    
        RANGE_BUCKET(30, [10, 30, 20, 40, 50]) -- execution failure

**Parameters**

  - `  point  ` : A generic value.
  - `  boundaries_array  ` : A generic array of values.

**Note:** The data type for `  point  ` and the element type of `  boundaries_array  ` must be equivalent. The data type must be [comparable](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-types#data_type_properties) .

**Return Value**

`  INT64  `

**Examples**

In a table called `  students  ` , check to see how many records would exist in each `  age_group  ` bucket, based on a student's age:

  - age\_group 0 (age \< 10)
  - age\_group 1 (age \>= 10, age \< 20)
  - age\_group 2 (age \>= 20, age \< 30)
  - age\_group 3 (age \>= 30)

<!-- end list -->

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

## `     ROUND    `

    ROUND(X [, N [, rounding_mode]])

**Description**

If only X is present, rounds X to the nearest integer. If N is present, rounds X to N decimal places after the decimal point. If N is negative, rounds off digits to the left of the decimal point. Rounds halfway cases away from zero. Generates an error if overflow occurs.

If X is a `  NUMERIC  ` or `  BIGNUMERIC  ` type, then you can explicitly set `  rounding_mode  ` to one of the following:

  - [`  "ROUND_HALF_AWAY_FROM_ZERO"  `](https://en.wikipedia.org/wiki/Rounding#Rounding_half_away_from_zero) : (Default) Rounds halfway cases away from zero.
  - [`  "ROUND_HALF_EVEN"  `](https://en.wikipedia.org/wiki/Rounding#Rounding_half_to_even) : Rounds halfway cases towards the nearest even digit.

If you set the `  rounding_mode  ` and X isn't a `  NUMERIC  ` or `  BIGNUMERIC  ` type, then the function generates an error.

| Expression                                                             | Return Value          |
| ---------------------------------------------------------------------- | --------------------- |
| `        ROUND(2.0)       `                                            | 2.0                   |
| `        ROUND(2.3)       `                                            | 2.0                   |
| `        ROUND(2.8)       `                                            | 3.0                   |
| `        ROUND(2.5)       `                                            | 3.0                   |
| `        ROUND(-2.3)       `                                           | \-2.0                 |
| `        ROUND(-2.8)       `                                           | \-3.0                 |
| `        ROUND(-2.5)       `                                           | \-3.0                 |
| `        ROUND(0)       `                                              | 0                     |
| `        ROUND(+inf)       `                                           | `        +inf       ` |
| `        ROUND(-inf)       `                                           | `        -inf       ` |
| `        ROUND(NaN)       `                                            | `        NaN       `  |
| `        ROUND(123.7, -1)       `                                      | 120.0                 |
| `        ROUND(1.235, 2)       `                                       | 1.24                  |
| `        ROUND(NUMERIC "2.25", 1, "ROUND_HALF_EVEN")       `           | 2.2                   |
| `        ROUND(NUMERIC "2.35", 1, "ROUND_HALF_EVEN")       `           | 2.4                   |
| `        ROUND(NUMERIC "2.251", 1, "ROUND_HALF_EVEN")       `          | 2.3                   |
| `        ROUND(NUMERIC "-2.5", 0, "ROUND_HALF_EVEN")       `           | \-2                   |
| `        ROUND(NUMERIC "2.5", 0, "ROUND_HALF_AWAY_FROM_ZERO")       `  | 3                     |
| `        ROUND(NUMERIC "-2.5", 0, "ROUND_HALF_AWAY_FROM_ZERO")       ` | \-3                   |

**Return Data Type**

| INPUT  | `        INT64       `   | `        NUMERIC       ` | `        BIGNUMERIC       ` | `        FLOAT64       ` |
| ------ | ------------------------ | ------------------------ | --------------------------- | ------------------------ |
| OUTPUT | `        FLOAT64       ` | `        NUMERIC       ` | `        BIGNUMERIC       ` | `        FLOAT64       ` |

## `     SAFE_ADD    `

    SAFE_ADD(X, Y)

**Description**

Equivalent to the addition operator ( `  +  ` ), but returns `  NULL  ` if overflow occurs.

| X | Y | SAFE\_ADD(X, Y) |
| - | - | --------------- |
| 5 | 4 | 9               |

**Return Data Type**

| INPUT                       | `        INT64       `      | `        NUMERIC       `    | `        BIGNUMERIC       ` | `        FLOAT64       ` |
| --------------------------- | --------------------------- | --------------------------- | --------------------------- | ------------------------ |
| `        INT64       `      | `        INT64       `      | `        NUMERIC       `    | `        BIGNUMERIC       ` | `        FLOAT64       ` |
| `        NUMERIC       `    | `        NUMERIC       `    | `        NUMERIC       `    | `        BIGNUMERIC       ` | `        FLOAT64       ` |
| `        BIGNUMERIC       ` | `        BIGNUMERIC       ` | `        BIGNUMERIC       ` | `        BIGNUMERIC       ` | `        FLOAT64       ` |
| `        FLOAT64       `    | `        FLOAT64       `    | `        FLOAT64       `    | `        FLOAT64       `    | `        FLOAT64       ` |

## `     SAFE_DIVIDE    `

    SAFE_DIVIDE(X, Y)

**Description**

Equivalent to the division operator ( `  X / Y  ` ), but returns `  NULL  ` if an error occurs, such as a division by zero error.

| X  | Y  | SAFE\_DIVIDE(X, Y)    |
| -- | -- | --------------------- |
| 20 | 4  | 5                     |
| 0  | 20 | `        0       `    |
| 20 | 0  | `        NULL       ` |

**Return Data Type**

| INPUT                       | `        INT64       `      | `        NUMERIC       `    | `        BIGNUMERIC       ` | `        FLOAT64       ` |
| --------------------------- | --------------------------- | --------------------------- | --------------------------- | ------------------------ |
| `        INT64       `      | `        FLOAT64       `    | `        NUMERIC       `    | `        BIGNUMERIC       ` | `        FLOAT64       ` |
| `        NUMERIC       `    | `        NUMERIC       `    | `        NUMERIC       `    | `        BIGNUMERIC       ` | `        FLOAT64       ` |
| `        BIGNUMERIC       ` | `        BIGNUMERIC       ` | `        BIGNUMERIC       ` | `        BIGNUMERIC       ` | `        FLOAT64       ` |
| `        FLOAT64       `    | `        FLOAT64       `    | `        FLOAT64       `    | `        FLOAT64       `    | `        FLOAT64       ` |

## `     SAFE_MULTIPLY    `

    SAFE_MULTIPLY(X, Y)

**Description**

Equivalent to the multiplication operator ( `  *  ` ), but returns `  NULL  ` if overflow occurs.

| X  | Y | SAFE\_MULTIPLY(X, Y) |
| -- | - | -------------------- |
| 20 | 4 | 80                   |

**Return Data Type**

| INPUT                       | `        INT64       `      | `        NUMERIC       `    | `        BIGNUMERIC       ` | `        FLOAT64       ` |
| --------------------------- | --------------------------- | --------------------------- | --------------------------- | ------------------------ |
| `        INT64       `      | `        INT64       `      | `        NUMERIC       `    | `        BIGNUMERIC       ` | `        FLOAT64       ` |
| `        NUMERIC       `    | `        NUMERIC       `    | `        NUMERIC       `    | `        BIGNUMERIC       ` | `        FLOAT64       ` |
| `        BIGNUMERIC       ` | `        BIGNUMERIC       ` | `        BIGNUMERIC       ` | `        BIGNUMERIC       ` | `        FLOAT64       ` |
| `        FLOAT64       `    | `        FLOAT64       `    | `        FLOAT64       `    | `        FLOAT64       `    | `        FLOAT64       ` |

## `     SAFE_NEGATE    `

    SAFE_NEGATE(X)

**Description**

Equivalent to the unary minus operator ( `  -  ` ), but returns `  NULL  ` if overflow occurs.

| X   | SAFE\_NEGATE(X) |
| --- | --------------- |
| \+1 | \-1             |
| \-1 | \+1             |
| 0   | 0               |

**Return Data Type**

| INPUT  | `        INT64       ` | `        NUMERIC       ` | `        BIGNUMERIC       ` | `        FLOAT64       ` |
| ------ | ---------------------- | ------------------------ | --------------------------- | ------------------------ |
| OUTPUT | `        INT64       ` | `        NUMERIC       ` | `        BIGNUMERIC       ` | `        FLOAT64       ` |

## `     SAFE_SUBTRACT    `

    SAFE_SUBTRACT(X, Y)

**Description**

Returns the result of Y subtracted from X. Equivalent to the subtraction operator ( `  -  ` ), but returns `  NULL  ` if overflow occurs.

| X | Y | SAFE\_SUBTRACT(X, Y) |
| - | - | -------------------- |
| 5 | 4 | 1                    |

**Return Data Type**

| INPUT                       | `        INT64       `      | `        NUMERIC       `    | `        BIGNUMERIC       ` | `        FLOAT64       ` |
| --------------------------- | --------------------------- | --------------------------- | --------------------------- | ------------------------ |
| `        INT64       `      | `        INT64       `      | `        NUMERIC       `    | `        BIGNUMERIC       ` | `        FLOAT64       ` |
| `        NUMERIC       `    | `        NUMERIC       `    | `        NUMERIC       `    | `        BIGNUMERIC       ` | `        FLOAT64       ` |
| `        BIGNUMERIC       ` | `        BIGNUMERIC       ` | `        BIGNUMERIC       ` | `        BIGNUMERIC       ` | `        FLOAT64       ` |
| `        FLOAT64       `    | `        FLOAT64       `    | `        FLOAT64       `    | `        FLOAT64       `    | `        FLOAT64       ` |

## `     SEC    `

    SEC(X)

**Description**

Computes the secant for the angle of `  X  ` , where `  X  ` is specified in radians. `  X  ` can be any data type that [coerces to `  FLOAT64  `](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/conversion_rules) .

| X                     | SEC(X)                |
| --------------------- | --------------------- |
| `        +inf       ` | `        NaN       `  |
| `        -inf       ` | `        NaN       `  |
| `        NaN       `  | `        NaN       `  |
| `        NULL       ` | `        NULL       ` |

**Return Data Type**

`  FLOAT64  `

**Example**

    SELECT SEC(100) AS a, SEC(-1) AS b;
    
    /*----------------+---------------+
     | a              | b             |
     +----------------+---------------+
     | 1.159663822905 | 1.85081571768 |
     +----------------+---------------*/

## `     SECH    `

    SECH(X)

**Description**

Computes the hyperbolic secant for the angle of `  X  ` , where `  X  ` is specified in radians. `  X  ` can be any data type that [coerces to `  FLOAT64  `](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/conversion_rules) . Never produces an error.

| X                     | SECH(X)               |
| --------------------- | --------------------- |
| `        +inf       ` | `        0       `    |
| `        -inf       ` | `        0       `    |
| `        NaN       `  | `        NaN       `  |
| `        NULL       ` | `        NULL       ` |

**Return Data Type**

`  FLOAT64  `

**Example**

    SELECT SECH(0.5) AS a, SECH(-2) AS b, SECH(100) AS c;
    
    /*----------------+----------------+---------------------+
     | a              | b              | c                   |
     +----------------+----------------+---------------------+
     | 0.88681888397  | 0.265802228834 | 7.4401519520417E-44 |
     +----------------+----------------+---------------------*/

## `     SIGN    `

    SIGN(X)

**Description**

Returns `  -1  ` , `  0  ` , or `  +1  ` for negative, zero and positive arguments respectively. For floating point arguments, this function doesn't distinguish between positive and negative zero.

| X    | SIGN(X) |
| ---- | ------- |
| 25   | \+1     |
| 0    | 0       |
| \-25 | \-1     |
| NaN  | NaN     |

**Return Data Type**

| INPUT  | `        INT64       ` | `        NUMERIC       ` | `        BIGNUMERIC       ` | `        FLOAT64       ` |
| ------ | ---------------------- | ------------------------ | --------------------------- | ------------------------ |
| OUTPUT | `        INT64       ` | `        NUMERIC       ` | `        BIGNUMERIC       ` | `        FLOAT64       ` |

## `     SIN    `

    SIN(X)

**Description**

Computes the sine of X where X is specified in radians. Never fails.

| X                     | SIN(X)               |
| --------------------- | -------------------- |
| `        +inf       ` | `        NaN       ` |
| `        -inf       ` | `        NaN       ` |
| `        NaN       `  | `        NaN       ` |

## `     SINH    `

    SINH(X)

**Description**

Computes the hyperbolic sine of X where X is specified in radians. Generates an error if overflow occurs.

| X                     | SINH(X)               |
| --------------------- | --------------------- |
| `        +inf       ` | `        +inf       ` |
| `        -inf       ` | `        -inf       ` |
| `        NaN       `  | `        NaN       `  |

## `     SQRT    `

    SQRT(X)

**Description**

Computes the square root of X. Generates an error if X is less than 0.

| X                      | SQRT(X)               |
| ---------------------- | --------------------- |
| `        25.0       `  | `        5.0       `  |
| `        +inf       `  | `        +inf       ` |
| `        X < 0       ` | Error                 |

**Return Data Type**

| INPUT  | `        INT64       `   | `        NUMERIC       ` | `        BIGNUMERIC       ` | `        FLOAT64       ` |
| ------ | ------------------------ | ------------------------ | --------------------------- | ------------------------ |
| OUTPUT | `        FLOAT64       ` | `        NUMERIC       ` | `        BIGNUMERIC       ` | `        FLOAT64       ` |

## `     TAN    `

    TAN(X)

**Description**

Computes the tangent of X where X is specified in radians. Generates an error if overflow occurs.

| X                     | TAN(X)               |
| --------------------- | -------------------- |
| `        +inf       ` | `        NaN       ` |
| `        -inf       ` | `        NaN       ` |
| `        NaN       `  | `        NaN       ` |

## `     TANH    `

    TANH(X)

**Description**

Computes the hyperbolic tangent of X where X is specified in radians. Doesn't fail.

| X                     | TANH(X)              |
| --------------------- | -------------------- |
| `        +inf       ` | 1.0                  |
| `        -inf       ` | \-1.0                |
| `        NaN       `  | `        NaN       ` |

## `     TRUNC    `

    TRUNC(X [, N])

**Description**

If only X is present, `  TRUNC  ` rounds X to the nearest integer whose absolute value isn't greater than the absolute value of X. If N is also present, `  TRUNC  ` behaves like `  ROUND(X, N)  ` , but always rounds towards zero and never overflows.

| X                     | TRUNC(X)              |
| --------------------- | --------------------- |
| 2.0                   | 2.0                   |
| 2.3                   | 2.0                   |
| 2.8                   | 2.0                   |
| 2.5                   | 2.0                   |
| \-2.3                 | \-2.0                 |
| \-2.8                 | \-2.0                 |
| \-2.5                 | \-2.0                 |
| 0                     | 0                     |
| `        +inf       ` | `        +inf       ` |
| `        -inf       ` | `        -inf       ` |
| `        NaN       `  | `        NaN       `  |

**Return Data Type**

| INPUT  | `        INT64       `   | `        NUMERIC       ` | `        BIGNUMERIC       ` | `        FLOAT64       ` |
| ------ | ------------------------ | ------------------------ | --------------------------- | ------------------------ |
| OUTPUT | `        FLOAT64       ` | `        NUMERIC       ` | `        BIGNUMERIC       ` | `        FLOAT64       ` |
