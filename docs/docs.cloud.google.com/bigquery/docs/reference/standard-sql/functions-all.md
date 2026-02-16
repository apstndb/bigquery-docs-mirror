GoogleSQL is the new name for Google Standard SQL\! New name, same great SQL dialect.

This topic contains all functions supported by GoogleSQL for BigQuery.

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
<td><a href="/bigquery/docs/reference/standard-sql/aead_encryption_functions#aeaddecrypt_bytes"><code dir="ltr" translate="no">        AEAD.DECRYPT_BYTES       </code></a></td>
<td>Uses the matching key from a keyset to decrypt a <code dir="ltr" translate="no">       BYTES      </code> ciphertext.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/aead_encryption_functions#aeaddecrypt_string"><code dir="ltr" translate="no">        AEAD.DECRYPT_STRING       </code></a></td>
<td>Uses the matching key from a keyset to decrypt a <code dir="ltr" translate="no">       BYTES      </code> ciphertext into a <code dir="ltr" translate="no">       STRING      </code> plaintext.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/aead_encryption_functions#aeadencrypt"><code dir="ltr" translate="no">        AEAD.ENCRYPT       </code></a></td>
<td>Encrypts <code dir="ltr" translate="no">       STRING      </code> plaintext, using the primary cryptographic key in a keyset.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#any_value"><code dir="ltr" translate="no">        ANY_VALUE       </code></a></td>
<td>Gets an expression for some row.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/time-series-functions#appends"><code dir="ltr" translate="no">        APPENDS       </code></a></td>
<td>Returns all rows appended to a table for a given time range.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/approximate_aggregate_functions#approx_count_distinct"><code dir="ltr" translate="no">        APPROX_COUNT_DISTINCT       </code></a></td>
<td>Gets the approximate result for <code dir="ltr" translate="no">       COUNT(DISTINCT expression)      </code> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/approximate_aggregate_functions#approx_quantiles"><code dir="ltr" translate="no">        APPROX_QUANTILES       </code></a></td>
<td>Gets the approximate quantile boundaries.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/approximate_aggregate_functions#approx_top_count"><code dir="ltr" translate="no">        APPROX_TOP_COUNT       </code></a></td>
<td>Gets the approximate top elements and their approximate count.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/approximate_aggregate_functions#approx_top_sum"><code dir="ltr" translate="no">        APPROX_TOP_SUM       </code></a></td>
<td>Gets the approximate top elements and sum, based on the approximate sum of an assigned weight.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/array_functions#array"><code dir="ltr" translate="no">        ARRAY       </code></a></td>
<td>Produces an array with one element for each row in a subquery.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#array_agg"><code dir="ltr" translate="no">        ARRAY_AGG       </code></a></td>
<td>Gets an array of values.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/array_functions#array_concat"><code dir="ltr" translate="no">        ARRAY_CONCAT       </code></a></td>
<td>Concatenates one or more arrays with the same element type into a single array.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#array_concat_agg"><code dir="ltr" translate="no">        ARRAY_CONCAT_AGG       </code></a></td>
<td>Concatenates arrays and returns a single array as a result.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/array_functions#array_first"><code dir="ltr" translate="no">        ARRAY_FIRST       </code></a></td>
<td>Gets the first element in an array.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/array_functions#array_last"><code dir="ltr" translate="no">        ARRAY_LAST       </code></a></td>
<td>Gets the last element in an array.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/array_functions#array_length"><code dir="ltr" translate="no">        ARRAY_LENGTH       </code></a></td>
<td>Gets the number of elements in an array.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/array_functions#array_reverse"><code dir="ltr" translate="no">        ARRAY_REVERSE       </code></a></td>
<td>Reverses the order of elements in an array.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/array_functions#array_slice"><code dir="ltr" translate="no">        ARRAY_SLICE       </code></a></td>
<td>Produces an array containing zero or more consecutive elements from an input array.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/array_functions#array_to_string"><code dir="ltr" translate="no">        ARRAY_TO_STRING       </code></a></td>
<td>Produces a concatenation of the elements in an array as a <code dir="ltr" translate="no">       STRING      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#ascii"><code dir="ltr" translate="no">        ASCII       </code></a></td>
<td>Gets the ASCII code for the first character or byte in a <code dir="ltr" translate="no">       STRING      </code> or <code dir="ltr" translate="no">       BYTES      </code> value.</td>
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
<td>Gets the average of non- <code dir="ltr" translate="no">       NULL      </code> values.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/aggregate-dp-functions#dp_avg"><code dir="ltr" translate="no">        AVG       </code> (Differential Privacy)</a></td>
<td><code dir="ltr" translate="no">       DIFFERENTIAL_PRIVACY      </code> -supported <code dir="ltr" translate="no">       AVG      </code> .<br />
<br />
Gets the differentially-private average of non- <code dir="ltr" translate="no">       NULL      </code> , non- <code dir="ltr" translate="no">       NaN      </code> values in a query with a <code dir="ltr" translate="no">       DIFFERENTIAL_PRIVACY      </code> clause.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/text-analysis-functions#bag_of_words"><code dir="ltr" translate="no">        BAG_OF_WORDS       </code></a></td>
<td>Gets the frequency of each term (token) in a tokenized document.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#bit_and"><code dir="ltr" translate="no">        BIT_AND       </code></a></td>
<td>Performs a bitwise AND operation on an expression.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/bit_functions#bit_count"><code dir="ltr" translate="no">        BIT_COUNT       </code></a></td>
<td>Gets the number of bits that are set in an input expression.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#bit_or"><code dir="ltr" translate="no">        BIT_OR       </code></a></td>
<td>Performs a bitwise OR operation on an expression.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#bit_xor"><code dir="ltr" translate="no">        BIT_XOR       </code></a></td>
<td>Performs a bitwise XOR operation on an expression.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/json_functions#bool_for_json"><code dir="ltr" translate="no">        BOOL       </code></a></td>
<td>Converts a JSON boolean to a SQL <code dir="ltr" translate="no">       BOOL      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#byte_length"><code dir="ltr" translate="no">        BYTE_LENGTH       </code></a></td>
<td>Gets the number of <code dir="ltr" translate="no">       BYTES      </code> in a <code dir="ltr" translate="no">       STRING      </code> or <code dir="ltr" translate="no">       BYTES      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/conversion_functions#cast"><code dir="ltr" translate="no">        CAST       </code></a></td>
<td>Convert the results of an expression to the given type.</td>
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
<td><a href="/bigquery/docs/reference/standard-sql/time-series-functions#changes"><code dir="ltr" translate="no">        CHANGES       </code></a></td>
<td>Returns all rows that have changed in a table for a given time range.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#char_length"><code dir="ltr" translate="no">        CHAR_LENGTH       </code></a></td>
<td>Gets the number of characters in a <code dir="ltr" translate="no">       STRING      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#character_length"><code dir="ltr" translate="no">        CHARACTER_LENGTH       </code></a></td>
<td>Synonym for <code dir="ltr" translate="no">       CHAR_LENGTH      </code> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#chr"><code dir="ltr" translate="no">        CHR       </code></a></td>
<td>Converts a Unicode code point to a character.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#code_points_to_bytes"><code dir="ltr" translate="no">        CODE_POINTS_TO_BYTES       </code></a></td>
<td>Converts an array of extended ASCII code points to a <code dir="ltr" translate="no">       BYTES      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#code_points_to_string"><code dir="ltr" translate="no">        CODE_POINTS_TO_STRING       </code></a></td>
<td>Converts an array of extended ASCII code points to a <code dir="ltr" translate="no">       STRING      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#collate"><code dir="ltr" translate="no">        COLLATE       </code></a></td>
<td>Combines a <code dir="ltr" translate="no">       STRING      </code> value and a collation specification into a collation specification-supported <code dir="ltr" translate="no">       STRING      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#concat"><code dir="ltr" translate="no">        CONCAT       </code></a></td>
<td>Concatenates one or more <code dir="ltr" translate="no">       STRING      </code> or <code dir="ltr" translate="no">       BYTES      </code> values into a single result.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#contains_substr"><code dir="ltr" translate="no">        CONTAINS_SUBSTR       </code></a></td>
<td>Performs a normalized, case-insensitive search to see if a value exists as a substring in an expression.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/statistical_aggregate_functions#corr"><code dir="ltr" translate="no">        CORR       </code></a></td>
<td>Computes the Pearson coefficient of correlation of a set of number pairs.</td>
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
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#count"><code dir="ltr" translate="no">        COUNT       </code></a></td>
<td>Gets the number of rows in the input, or the number of rows with an expression evaluated to any value other than <code dir="ltr" translate="no">       NULL      </code> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/aggregate-dp-functions#dp_count"><code dir="ltr" translate="no">        COUNT       </code> (Differential Privacy)</a></td>
<td><code dir="ltr" translate="no">       DIFFERENTIAL_PRIVACY      </code> -supported <code dir="ltr" translate="no">       COUNT      </code> .<br />
<br />
Signature 1: Gets the differentially-private count of rows in a query with a <code dir="ltr" translate="no">       DIFFERENTIAL_PRIVACY      </code> clause.<br />
<br />
Signature 2: Gets the differentially-private count of rows with a non- <code dir="ltr" translate="no">       NULL      </code> expression in a query with a <code dir="ltr" translate="no">       DIFFERENTIAL_PRIVACY      </code> clause.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#countif"><code dir="ltr" translate="no">        COUNTIF       </code></a></td>
<td>Gets the number of <code dir="ltr" translate="no">       TRUE      </code> values for an expression.</td>
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
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#csc"><code dir="ltr" translate="no">        CSC       </code></a></td>
<td>Computes the cosecant of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#csch"><code dir="ltr" translate="no">        CSCH       </code></a></td>
<td>Computes the hyperbolic cosecant of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/numbering_functions#cume_dist"><code dir="ltr" translate="no">        CUME_DIST       </code></a></td>
<td>Gets the cumulative distribution (relative position (0,1]) of each row within a window.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/date_functions#current_date"><code dir="ltr" translate="no">        CURRENT_DATE       </code></a></td>
<td>Returns the current date as a <code dir="ltr" translate="no">       DATE      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/datetime_functions#current_datetime"><code dir="ltr" translate="no">        CURRENT_DATETIME       </code></a></td>
<td>Returns the current date and time as a <code dir="ltr" translate="no">       DATETIME      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/time_functions#current_time"><code dir="ltr" translate="no">        CURRENT_TIME       </code></a></td>
<td>Returns the current time as a <code dir="ltr" translate="no">       TIME      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#current_timestamp"><code dir="ltr" translate="no">        CURRENT_TIMESTAMP       </code></a></td>
<td>Returns the current date and time as a <code dir="ltr" translate="no">       TIMESTAMP      </code> object.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/date_functions#date"><code dir="ltr" translate="no">        DATE       </code></a></td>
<td>Constructs a <code dir="ltr" translate="no">       DATE      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/date_functions#date_add"><code dir="ltr" translate="no">        DATE_ADD       </code></a></td>
<td>Adds a specified time interval to a <code dir="ltr" translate="no">       DATE      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/time-series-functions#date_bucket"><code dir="ltr" translate="no">        DATE_BUCKET       </code></a></td>
<td>Gets the lower bound of the date bucket that contains a date.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/date_functions#date_diff"><code dir="ltr" translate="no">        DATE_DIFF       </code></a></td>
<td>Gets the number of unit boundaries between two <code dir="ltr" translate="no">       DATE      </code> values at a particular time granularity.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/date_functions#date_from_unix_date"><code dir="ltr" translate="no">        DATE_FROM_UNIX_DATE       </code></a></td>
<td>Interprets an <code dir="ltr" translate="no">       INT64      </code> expression as the number of days since 1970-01-01.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/date_functions#date_sub"><code dir="ltr" translate="no">        DATE_SUB       </code></a></td>
<td>Subtracts a specified time interval from a <code dir="ltr" translate="no">       DATE      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/date_functions#date_trunc"><code dir="ltr" translate="no">        DATE_TRUNC       </code></a></td>
<td>Truncates a <code dir="ltr" translate="no">       DATE      </code> , <code dir="ltr" translate="no">       DATETIME      </code> , or <code dir="ltr" translate="no">       TIMESTAMP      </code> value at a particular granularity.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/datetime_functions#datetime"><code dir="ltr" translate="no">        DATETIME       </code></a></td>
<td>Constructs a <code dir="ltr" translate="no">       DATETIME      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/datetime_functions#datetime_add"><code dir="ltr" translate="no">        DATETIME_ADD       </code></a></td>
<td>Adds a specified time interval to a <code dir="ltr" translate="no">       DATETIME      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/time-series-functions#datetime_bucket"><code dir="ltr" translate="no">        DATETIME_BUCKET       </code></a></td>
<td>Gets the lower bound of the datetime bucket that contains a datetime.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/datetime_functions#datetime_diff"><code dir="ltr" translate="no">        DATETIME_DIFF       </code></a></td>
<td>Gets the number of unit boundaries between two <code dir="ltr" translate="no">       DATETIME      </code> values at a particular time granularity.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/datetime_functions#datetime_sub"><code dir="ltr" translate="no">        DATETIME_SUB       </code></a></td>
<td>Subtracts a specified time interval from a <code dir="ltr" translate="no">       DATETIME      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/datetime_functions#datetime_trunc"><code dir="ltr" translate="no">        DATETIME_TRUNC       </code></a></td>
<td>Truncates a <code dir="ltr" translate="no">       DATETIME      </code> or <code dir="ltr" translate="no">       TIMESTAMP      </code> value at a particular granularity.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/numbering_functions#dense_rank"><code dir="ltr" translate="no">        DENSE_RANK       </code></a></td>
<td>Gets the dense rank (1-based, no gaps) of each row within a window.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/aead_encryption_functions#deterministic_decrypt_bytes"><code dir="ltr" translate="no">        DETERMINISTIC_DECRYPT_BYTES       </code></a></td>
<td>Uses the matching key from a keyset to decrypt a <code dir="ltr" translate="no">       BYTES      </code> ciphertext, using deterministic AEAD.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/aead_encryption_functions#deterministic_decrypt_string"><code dir="ltr" translate="no">        DETERMINISTIC_DECRYPT_STRING       </code></a></td>
<td>Uses the matching key from a keyset to decrypt a <code dir="ltr" translate="no">       BYTES      </code> ciphertext into a <code dir="ltr" translate="no">       STRING      </code> plaintext, using deterministic AEAD.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/aead_encryption_functions#deterministic_encrypt"><code dir="ltr" translate="no">        DETERMINISTIC_ENCRYPT       </code></a></td>
<td>Encrypts <code dir="ltr" translate="no">       STRING      </code> plaintext, using the primary cryptographic key in a keyset, using deterministic AEAD encryption.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#div"><code dir="ltr" translate="no">        DIV       </code></a></td>
<td>Divides integer <code dir="ltr" translate="no">       X      </code> by integer <code dir="ltr" translate="no">       Y      </code> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/dlp_functions#dlp_deterministic_encrypt"><code dir="ltr" translate="no">        DLP_DETERMINISTIC_ENCRYPT       </code></a></td>
<td>Encrypts data with a DLP compatible algorithm.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/dlp_functions#dlp_deterministic_decrypt"><code dir="ltr" translate="no">        DLP_DETERMINISTIC_DECRYPT       </code></a></td>
<td>Decrypts DLP-encrypted data.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/dlp_functions#dlp_key_chain"><code dir="ltr" translate="no">        DLP_KEY_CHAIN       </code></a></td>
<td>Gets a data encryption key that's wrapped by Cloud Key Management Service.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/json_functions#double_for_json"><code dir="ltr" translate="no">        FLOAT64       </code></a></td>
<td>Converts a JSON number to a SQL <code dir="ltr" translate="no">       FLOAT64      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#edit_distance"><code dir="ltr" translate="no">        EDIT_DISTANCE       </code></a></td>
<td>Computes the Levenshtein distance between two <code dir="ltr" translate="no">       STRING      </code> or <code dir="ltr" translate="no">       BYTES      </code> values.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#ends_with"><code dir="ltr" translate="no">        ENDS_WITH       </code></a></td>
<td>Checks if a <code dir="ltr" translate="no">       STRING      </code> or <code dir="ltr" translate="no">       BYTES      </code> value is the suffix of another value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/debugging_functions#error"><code dir="ltr" translate="no">        ERROR       </code></a></td>
<td>Produces an error with a custom error message.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#exp"><code dir="ltr" translate="no">        EXP       </code></a></td>
<td>Computes <code dir="ltr" translate="no">       e      </code> to the power of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/table-functions-built-in#external_object_transform"><code dir="ltr" translate="no">        EXTERNAL_OBJECT_TRANSFORM       </code></a></td>
<td>Produces an object table with the original columns plus one or more additional columns.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/federated_query_functions#external_query"><code dir="ltr" translate="no">        EXTERNAL_QUERY       </code></a></td>
<td>Executes a query on an external database and returns the results as a temporary table.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/date_functions#extract"><code dir="ltr" translate="no">        EXTRACT       </code></a></td>
<td>Extracts part of a date from a <code dir="ltr" translate="no">       DATE      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/datetime_functions#extract"><code dir="ltr" translate="no">        EXTRACT       </code></a></td>
<td>Extracts part of a date and time from a <code dir="ltr" translate="no">       DATETIME      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/interval_functions#extract"><code dir="ltr" translate="no">        EXTRACT       </code></a></td>
<td>Extracts part of an <code dir="ltr" translate="no">       INTERVAL      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/time_functions#extract"><code dir="ltr" translate="no">        EXTRACT       </code></a></td>
<td>Extracts part of a <code dir="ltr" translate="no">       TIME      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#extract"><code dir="ltr" translate="no">        EXTRACT       </code></a></td>
<td>Extracts part of a <code dir="ltr" translate="no">       TIMESTAMP      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#euclidean_distance"><code dir="ltr" translate="no">        EUCLIDEAN_DISTANCE       </code></a></td>
<td>Computes the Euclidean distance between two vectors.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/hash_functions#farm_fingerprint"><code dir="ltr" translate="no">        FARM_FINGERPRINT       </code></a></td>
<td>Computes the fingerprint of a <code dir="ltr" translate="no">       STRING      </code> or <code dir="ltr" translate="no">       BYTES      </code> value, using the FarmHash Fingerprint64 algorithm.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/navigation_functions#first_value"><code dir="ltr" translate="no">        FIRST_VALUE       </code></a></td>
<td>Gets a value for the first row in the current window frame.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#floor"><code dir="ltr" translate="no">        FLOOR       </code></a></td>
<td>Gets the largest integral value that isn't greater than <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/date_functions#format_date"><code dir="ltr" translate="no">        FORMAT_DATE       </code></a></td>
<td>Formats a <code dir="ltr" translate="no">       DATE      </code> value according to a specified format string.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/datetime_functions#format_datetime"><code dir="ltr" translate="no">        FORMAT_DATETIME       </code></a></td>
<td>Formats a <code dir="ltr" translate="no">       DATETIME      </code> value according to a specified format string.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/time_functions#format_time"><code dir="ltr" translate="no">        FORMAT_TIME       </code></a></td>
<td>Formats a <code dir="ltr" translate="no">       TIME      </code> value according to the specified format string.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#format_timestamp"><code dir="ltr" translate="no">        FORMAT_TIMESTAMP       </code></a></td>
<td>Formats a <code dir="ltr" translate="no">       TIMESTAMP      </code> value according to the specified format string.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#format_string"><code dir="ltr" translate="no">        FORMAT       </code></a></td>
<td>Formats data and produces the results as a <code dir="ltr" translate="no">       STRING      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#from_base32"><code dir="ltr" translate="no">        FROM_BASE32       </code></a></td>
<td>Converts a base32-encoded <code dir="ltr" translate="no">       STRING      </code> value into a <code dir="ltr" translate="no">       BYTES      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#from_base64"><code dir="ltr" translate="no">        FROM_BASE64       </code></a></td>
<td>Converts a base64-encoded <code dir="ltr" translate="no">       STRING      </code> value into a <code dir="ltr" translate="no">       BYTES      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#from_hex"><code dir="ltr" translate="no">        FROM_HEX       </code></a></td>
<td>Converts a hexadecimal-encoded <code dir="ltr" translate="no">       STRING      </code> value into a <code dir="ltr" translate="no">       BYTES      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/time-series-functions#gap_fill"><code dir="ltr" translate="no">        GAP_FILL       </code></a></td>
<td>Finds and fills gaps in a time series.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/array_functions#generate_array"><code dir="ltr" translate="no">        GENERATE_ARRAY       </code></a></td>
<td>Generates an array of values in a range.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/array_functions#generate_date_array"><code dir="ltr" translate="no">        GENERATE_DATE_ARRAY       </code></a></td>
<td>Generates an array of dates in a range.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/range-functions#generate_range_array"><code dir="ltr" translate="no">        GENERATE_RANGE_ARRAY       </code></a></td>
<td>Splits a range into an array of subranges.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/array_functions#generate_timestamp_array"><code dir="ltr" translate="no">        GENERATE_TIMESTAMP_ARRAY       </code></a></td>
<td>Generates an array of timestamps in a range.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/utility-functions#generate_uuid"><code dir="ltr" translate="no">        GENERATE_UUID       </code></a></td>
<td>Produces a random universally unique identifier (UUID) as a <code dir="ltr" translate="no">       STRING      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#greatest"><code dir="ltr" translate="no">        GREATEST       </code></a></td>
<td>Gets the greatest value among <code dir="ltr" translate="no">       X1,...,XN      </code> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#grouping"><code dir="ltr" translate="no">        GROUPING       </code></a></td>
<td>Checks if a groupable value in the <code dir="ltr" translate="no">       GROUP BY      </code> clause is aggregated.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/hll_functions#hll_countextract"><code dir="ltr" translate="no">        HLL_COUNT.EXTRACT       </code></a></td>
<td>Extracts a cardinality estimate of an HLL++ sketch.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/hll_functions#hll_countinit"><code dir="ltr" translate="no">        HLL_COUNT.INIT       </code></a></td>
<td>Aggregates values of the same underlying type into a new HLL++ sketch.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/hll_functions#hll_countmerge"><code dir="ltr" translate="no">        HLL_COUNT.MERGE       </code></a></td>
<td>Merges HLL++ sketches of the same underlying type into a new sketch, and then gets the cardinality of the new sketch.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/hll_functions#hll_countmerge_partial"><code dir="ltr" translate="no">        HLL_COUNT.MERGE_PARTIAL       </code></a></td>
<td>Merges HLL++ sketches of the same underlying type into a new sketch.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#ieee_divide"><code dir="ltr" translate="no">        IEEE_DIVIDE       </code></a></td>
<td>Divides <code dir="ltr" translate="no">       X      </code> by <code dir="ltr" translate="no">       Y      </code> , but doesn't generate errors for division by zero or overflow.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#initcap"><code dir="ltr" translate="no">        INITCAP       </code></a></td>
<td>Formats a <code dir="ltr" translate="no">       STRING      </code> as proper case, which means that the first character in each word is uppercase and all other characters are lowercase.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#instr"><code dir="ltr" translate="no">        INSTR       </code></a></td>
<td>Finds the position of a subvalue inside another value, optionally starting the search at a given offset or occurrence.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/json_functions#int64_for_json"><code dir="ltr" translate="no">        INT64       </code></a></td>
<td>Converts a JSON number to a SQL <code dir="ltr" translate="no">       INT64      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#is_inf"><code dir="ltr" translate="no">        IS_INF       </code></a></td>
<td>Checks if <code dir="ltr" translate="no">       X      </code> is positive or negative infinity.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#is_nan"><code dir="ltr" translate="no">        IS_NAN       </code></a></td>
<td>Checks if <code dir="ltr" translate="no">       X      </code> is a <code dir="ltr" translate="no">       NaN      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/json_functions#json_array"><code dir="ltr" translate="no">        JSON_ARRAY       </code></a></td>
<td>Creates a JSON array.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/json_functions#json_array_append"><code dir="ltr" translate="no">        JSON_ARRAY_APPEND       </code></a></td>
<td>Appends JSON data to the end of a JSON array.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/json_functions#json_array_insert"><code dir="ltr" translate="no">        JSON_ARRAY_INSERT       </code></a></td>
<td>Inserts JSON data into a JSON array.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/json_functions#json_extract"><code dir="ltr" translate="no">        JSON_EXTRACT       </code></a></td>
<td>(Deprecated) Extracts a JSON value and converts it to a SQL JSON-formatted <code dir="ltr" translate="no">       STRING      </code> or <code dir="ltr" translate="no">       JSON      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/json_functions#json_extract_array"><code dir="ltr" translate="no">        JSON_EXTRACT_ARRAY       </code></a></td>
<td>(Deprecated) Extracts a JSON array and converts it to a SQL <code dir="ltr" translate="no">       ARRAY&lt;JSON-formatted STRING&gt;      </code> or <code dir="ltr" translate="no">       ARRAY&lt;JSON&gt;      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/json_functions#json_extract_scalar"><code dir="ltr" translate="no">        JSON_EXTRACT_SCALAR       </code></a></td>
<td>(Deprecated) Extracts a JSON scalar value and converts it to a SQL <code dir="ltr" translate="no">       STRING      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/json_functions#json_extract_string_array"><code dir="ltr" translate="no">        JSON_EXTRACT_STRING_ARRAY       </code></a></td>
<td>(Deprecated) Extracts a JSON array of scalar values and converts it to a SQL <code dir="ltr" translate="no">       ARRAY&lt;STRING&gt;      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/json_functions#json_flatten"><code dir="ltr" translate="no">        JSON_FLATTEN       </code></a></td>
<td>Produces a new SQL <code dir="ltr" translate="no">       ARRAY&lt;JSON&gt;      </code> value containing all non-array values that are either directly in the input JSON value or children of one or more consecutively nested arrays in the input JSON value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/json_functions#json_keys"><code dir="ltr" translate="no">        JSON_KEYS       </code></a></td>
<td>Extracts unique JSON keys from a JSON expression.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/json_functions#json_object"><code dir="ltr" translate="no">        JSON_OBJECT       </code></a></td>
<td>Creates a JSON object.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/json_functions#json_query"><code dir="ltr" translate="no">        JSON_QUERY       </code></a></td>
<td>Extracts a JSON value and converts it to a SQL JSON-formatted <code dir="ltr" translate="no">       STRING      </code> or <code dir="ltr" translate="no">       JSON      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/json_functions#json_query_array"><code dir="ltr" translate="no">        JSON_QUERY_ARRAY       </code></a></td>
<td>Extracts a JSON array and converts it to a SQL <code dir="ltr" translate="no">       ARRAY&lt;JSON-formatted STRING&gt;      </code> or <code dir="ltr" translate="no">       ARRAY&lt;JSON&gt;      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/json_functions#json_remove"><code dir="ltr" translate="no">        JSON_REMOVE       </code></a></td>
<td>Produces JSON with the specified JSON data removed.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/json_functions#json_set"><code dir="ltr" translate="no">        JSON_SET       </code></a></td>
<td>Inserts or replaces JSON data.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/json_functions#json_strip_nulls"><code dir="ltr" translate="no">        JSON_STRIP_NULLS       </code></a></td>
<td>Removes JSON nulls from JSON objects and JSON arrays.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/json_functions#json_type"><code dir="ltr" translate="no">        JSON_TYPE       </code></a></td>
<td>Gets the JSON type of the outermost JSON value and converts the name of this type to a SQL <code dir="ltr" translate="no">       STRING      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/json_functions#json_value"><code dir="ltr" translate="no">        JSON_VALUE       </code></a></td>
<td>Extracts a JSON scalar value and converts it to a SQL <code dir="ltr" translate="no">       STRING      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/json_functions#json_value_array"><code dir="ltr" translate="no">        JSON_VALUE_ARRAY       </code></a></td>
<td>Extracts a JSON array of scalar values and converts it to a SQL <code dir="ltr" translate="no">       ARRAY&lt;STRING&gt;      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/interval_functions#justify_days"><code dir="ltr" translate="no">        JUSTIFY_DAYS       </code></a></td>
<td>Normalizes the day part of an <code dir="ltr" translate="no">       INTERVAL      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/interval_functions#justify_hours"><code dir="ltr" translate="no">        JUSTIFY_HOURS       </code></a></td>
<td>Normalizes the time part of an <code dir="ltr" translate="no">       INTERVAL      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/interval_functions#justify_interval"><code dir="ltr" translate="no">        JUSTIFY_INTERVAL       </code></a></td>
<td>Normalizes the day and time parts of an <code dir="ltr" translate="no">       INTERVAL      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/aead_encryption_functions#keysadd_key_from_raw_bytes"><code dir="ltr" translate="no">        KEYS.ADD_KEY_FROM_RAW_BYTES       </code></a></td>
<td>Adds a key to a keyset, and return the new keyset as a serialized <code dir="ltr" translate="no">       BYTES      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/aead_encryption_functions#keyskeyset_chain"><code dir="ltr" translate="no">        KEYS.KEYSET_CHAIN       </code></a></td>
<td>Produces a Tink keyset that's encrypted with a Cloud KMS key.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/aead_encryption_functions#keyskeyset_from_json"><code dir="ltr" translate="no">        KEYS.KEYSET_FROM_JSON       </code></a></td>
<td>Converts a <code dir="ltr" translate="no">       STRING      </code> JSON keyset to a serialized <code dir="ltr" translate="no">       BYTES      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/aead_encryption_functions#keyskeyset_length"><code dir="ltr" translate="no">        KEYS.KEYSET_LENGTH       </code></a></td>
<td>Gets the number of keys in the provided keyset.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/aead_encryption_functions#keyskeyset_to_json"><code dir="ltr" translate="no">        KEYS.KEYSET_TO_JSON       </code></a></td>
<td>Gets a JSON <code dir="ltr" translate="no">       STRING      </code> representation of a keyset.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/aead_encryption_functions#keysnew_keyset"><code dir="ltr" translate="no">        KEYS.NEW_KEYSET       </code></a></td>
<td>Gets a serialized keyset containing a new key based on the key type.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/aead_encryption_functions#keysnew_wrapped_keyset"><code dir="ltr" translate="no">        KEYS.NEW_WRAPPED_KEYSET       </code></a></td>
<td>Creates a new keyset and encrypts it with a Cloud KMS key.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/aead_encryption_functions#keysrewrap_keyset"><code dir="ltr" translate="no">        KEYS.REWRAP_KEYSET       </code></a></td>
<td>Re-encrypts a wrapped keyset with a new Cloud KMS key.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/aead_encryption_functions#keysrotate_keyset"><code dir="ltr" translate="no">        KEYS.ROTATE_KEYSET       </code></a></td>
<td>Adds a new primary cryptographic key to a keyset, based on the key type.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/aead_encryption_functions#keysrotate_wrapped_keyset"><code dir="ltr" translate="no">        KEYS.ROTATE_WRAPPED_KEYSET       </code></a></td>
<td>Rewraps a keyset and rotates it.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/kll_functions#kll_quantilesextract_int64"><code dir="ltr" translate="no">        KLL_QUANTILES.EXTRACT_INT64       </code></a></td>
<td>Gets a selected number of quantiles from an <code dir="ltr" translate="no">       INT64      </code> -initialized KLL sketch.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/kll_functions#kll_quantilesextract_double"><code dir="ltr" translate="no">        KLL_QUANTILES.EXTRACT_FLOAT64       </code></a></td>
<td>Gets a selected number of quantiles from a <code dir="ltr" translate="no">       FLOAT64      </code> -initialized KLL sketch.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/kll_functions#kll_quantilesextract_point_int64"><code dir="ltr" translate="no">        KLL_QUANTILES.EXTRACT_POINT_INT64       </code></a></td>
<td>Gets a specific quantile from an <code dir="ltr" translate="no">       INT64      </code> -initialized KLL sketch.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/kll_functions#kll_quantilesextract_point_double"><code dir="ltr" translate="no">        KLL_QUANTILES.EXTRACT_POINT_FLOAT64       </code></a></td>
<td>Gets a specific quantile from a <code dir="ltr" translate="no">       FLOAT64      </code> -initialized KLL sketch.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/kll_functions#kll_quantilesinit_int64"><code dir="ltr" translate="no">        KLL_QUANTILES.INIT_INT64       </code></a></td>
<td>Aggregates values into an <code dir="ltr" translate="no">       INT64      </code> -initialized KLL sketch.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/kll_functions#kll_quantilesinit_double"><code dir="ltr" translate="no">        KLL_QUANTILES.INIT_FLOAT64       </code></a></td>
<td>Aggregates values into a <code dir="ltr" translate="no">       FLOAT64      </code> -initialized KLL sketch.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/kll_functions#kll_quantilesmerge_int64"><code dir="ltr" translate="no">        KLL_QUANTILES.MERGE_INT64       </code></a></td>
<td>Merges <code dir="ltr" translate="no">       INT64      </code> -initialized KLL sketches into a new sketch, and then gets the quantiles from the new sketch.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/kll_functions#kll_quantilesmerge_double"><code dir="ltr" translate="no">        KLL_QUANTILES.MERGE_FLOAT64       </code></a></td>
<td>Merges <code dir="ltr" translate="no">       FLOAT64      </code> -initialized KLL sketches into a new sketch, and then gets the quantiles from the new sketch.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/kll_functions#kll_quantilesmerge_partial"><code dir="ltr" translate="no">        KLL_QUANTILES.MERGE_PARTIAL       </code></a></td>
<td>Merges KLL sketches of the same underlying type into a new sketch.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/kll_functions#kll_quantilesmerge_point_int64"><code dir="ltr" translate="no">        KLL_QUANTILES.MERGE_POINT_INT64       </code></a></td>
<td>Merges <code dir="ltr" translate="no">       INT64      </code> -initialized KLL sketches into a new sketch, and then gets a specific quantile from the new sketch.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/kll_functions#kll_quantilesmerge_point_double"><code dir="ltr" translate="no">        KLL_QUANTILES.MERGE_POINT_FLOAT64       </code></a></td>
<td>Merges <code dir="ltr" translate="no">       FLOAT64      </code> -initialized KLL sketches into a new sketch, and then gets a specific quantile from the new sketch.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/navigation_functions#lag"><code dir="ltr" translate="no">        LAG       </code></a></td>
<td>Gets a value for a preceding row.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/date_functions#last_day"><code dir="ltr" translate="no">        LAST_DAY       </code></a></td>
<td>Gets the last day in a specified time period that contains a <code dir="ltr" translate="no">       DATE      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/datetime_functions#last_day"><code dir="ltr" translate="no">        LAST_DAY       </code></a></td>
<td>Gets the last day in a specified time period that contains a <code dir="ltr" translate="no">       DATETIME      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/navigation_functions#last_value"><code dir="ltr" translate="no">        LAST_VALUE       </code></a></td>
<td>Gets a value for the last row in the current window frame.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/json_functions#lax_bool"><code dir="ltr" translate="no">        LAX_BOOL       </code></a></td>
<td>Attempts to convert a JSON value to a SQL <code dir="ltr" translate="no">       BOOL      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/json_functions#lax_double"><code dir="ltr" translate="no">        LAX_FLOAT64       </code></a></td>
<td>Attempts to convert a JSON value to a SQL <code dir="ltr" translate="no">       FLOAT64      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/json_functions#lax_int64"><code dir="ltr" translate="no">        LAX_INT64       </code></a></td>
<td>Attempts to convert a JSON value to a SQL <code dir="ltr" translate="no">       INT64      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/json_functions#lax_string"><code dir="ltr" translate="no">        LAX_STRING       </code></a></td>
<td>Attempts to convert a JSON value to a SQL <code dir="ltr" translate="no">       STRING      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/navigation_functions#lead"><code dir="ltr" translate="no">        LEAD       </code></a></td>
<td>Gets a value for a subsequent row.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#least"><code dir="ltr" translate="no">        LEAST       </code></a></td>
<td>Gets the least value among <code dir="ltr" translate="no">       X1,...,XN      </code> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#left"><code dir="ltr" translate="no">        LEFT       </code></a></td>
<td>Gets the specified leftmost portion from a <code dir="ltr" translate="no">       STRING      </code> or <code dir="ltr" translate="no">       BYTES      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#length"><code dir="ltr" translate="no">        LENGTH       </code></a></td>
<td>Gets the length of a <code dir="ltr" translate="no">       STRING      </code> or <code dir="ltr" translate="no">       BYTES      </code> value.</td>
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
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#logical_and"><code dir="ltr" translate="no">        LOGICAL_AND       </code></a></td>
<td>Gets the logical AND of all non- <code dir="ltr" translate="no">       NULL      </code> expressions.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#logical_or"><code dir="ltr" translate="no">        LOGICAL_OR       </code></a></td>
<td>Gets the logical OR of all non- <code dir="ltr" translate="no">       NULL      </code> expressions.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#lower"><code dir="ltr" translate="no">        LOWER       </code></a></td>
<td>Formats alphabetic characters in a <code dir="ltr" translate="no">       STRING      </code> value as lowercase.<br />
<br />
Formats ASCII characters in a <code dir="ltr" translate="no">       BYTES      </code> value as lowercase.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#lpad"><code dir="ltr" translate="no">        LPAD       </code></a></td>
<td>Prepends a <code dir="ltr" translate="no">       STRING      </code> or <code dir="ltr" translate="no">       BYTES      </code> value with a pattern.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#ltrim"><code dir="ltr" translate="no">        LTRIM       </code></a></td>
<td>Identical to the <code dir="ltr" translate="no">       TRIM      </code> function, but only removes leading characters.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/interval_functions#make_interval"><code dir="ltr" translate="no">        MAKE_INTERVAL       </code></a></td>
<td>Constructs an <code dir="ltr" translate="no">       INTERVAL      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#max"><code dir="ltr" translate="no">        MAX       </code></a></td>
<td>Gets the maximum non- <code dir="ltr" translate="no">       NULL      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#max_by"><code dir="ltr" translate="no">        MAX_BY       </code></a></td>
<td>Synonym for <code dir="ltr" translate="no">       ANY_VALUE(x HAVING MAX y)      </code> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/hash_functions#md5"><code dir="ltr" translate="no">        MD5       </code></a></td>
<td>Computes the hash of a <code dir="ltr" translate="no">       STRING      </code> or <code dir="ltr" translate="no">       BYTES      </code> value, using the MD5 algorithm.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#min"><code dir="ltr" translate="no">        MIN       </code></a></td>
<td>Gets the minimum non- <code dir="ltr" translate="no">       NULL      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#min_by"><code dir="ltr" translate="no">        MIN_BY       </code></a></td>
<td>Synonym for <code dir="ltr" translate="no">       ANY_VALUE(x HAVING MIN y)      </code> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#mod"><code dir="ltr" translate="no">        MOD       </code></a></td>
<td>Gets the remainder of the division of <code dir="ltr" translate="no">       X      </code> by <code dir="ltr" translate="no">       Y      </code> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/net_functions#nethost"><code dir="ltr" translate="no">        NET.HOST       </code></a></td>
<td>Gets the hostname from a URL.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/net_functions#netip_from_string"><code dir="ltr" translate="no">        NET.IP_FROM_STRING       </code></a></td>
<td>Converts an IPv4 or IPv6 address from a <code dir="ltr" translate="no">       STRING      </code> value to a <code dir="ltr" translate="no">       BYTES      </code> value in network byte order.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/net_functions#netip_net_mask"><code dir="ltr" translate="no">        NET.IP_NET_MASK       </code></a></td>
<td>Gets a network mask.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/net_functions#netip_to_string"><code dir="ltr" translate="no">        NET.IP_TO_STRING       </code></a></td>
<td>Converts an IPv4 or IPv6 address from a <code dir="ltr" translate="no">       BYTES      </code> value in network byte order to a <code dir="ltr" translate="no">       STRING      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/net_functions#netip_trunc"><code dir="ltr" translate="no">        NET.IP_TRUNC       </code></a></td>
<td>Converts a <code dir="ltr" translate="no">       BYTES      </code> IPv4 or IPv6 address in network byte order to a <code dir="ltr" translate="no">       BYTES      </code> subnet address.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/net_functions#netipv4_from_int64"><code dir="ltr" translate="no">        NET.IPV4_FROM_INT64       </code></a></td>
<td>Converts an IPv4 address from an <code dir="ltr" translate="no">       INT64      </code> value to a <code dir="ltr" translate="no">       BYTES      </code> value in network byte order.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/net_functions#netipv4_to_int64"><code dir="ltr" translate="no">        NET.IPV4_TO_INT64       </code></a></td>
<td>Converts an IPv4 address from a <code dir="ltr" translate="no">       BYTES      </code> value in network byte order to an <code dir="ltr" translate="no">       INT64      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/net_functions#netpublic_suffix"><code dir="ltr" translate="no">        NET.PUBLIC_SUFFIX       </code></a></td>
<td>Gets the public suffix from a URL.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/net_functions#netreg_domain"><code dir="ltr" translate="no">        NET.REG_DOMAIN       </code></a></td>
<td>Gets the registered or registrable domain from a URL.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/net_functions#netsafe_ip_from_string"><code dir="ltr" translate="no">        NET.SAFE_IP_FROM_STRING       </code></a></td>
<td>Similar to the <code dir="ltr" translate="no">       NET.IP_FROM_STRING      </code> , but returns <code dir="ltr" translate="no">       NULL      </code> instead of producing an error if the input is invalid.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#normalize"><code dir="ltr" translate="no">        NORMALIZE       </code></a></td>
<td>Case-sensitively normalizes the characters in a <code dir="ltr" translate="no">       STRING      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#normalize_and_casefold"><code dir="ltr" translate="no">        NORMALIZE_AND_CASEFOLD       </code></a></td>
<td>Case-insensitively normalizes the characters in a <code dir="ltr" translate="no">       STRING      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/navigation_functions#nth_value"><code dir="ltr" translate="no">        NTH_VALUE       </code></a></td>
<td>Gets a value for the Nth row of the current window frame.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/numbering_functions#ntile"><code dir="ltr" translate="no">        NTILE       </code></a></td>
<td>Gets the quantile bucket number (1-based) of each row within a window.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/objectref_functions#objfetch_metadata"><code dir="ltr" translate="no">        OBJ.FETCH_METADATA       </code></a></td>
<td>Fetches Cloud Storage metadata for a partially populated <code dir="ltr" translate="no">       ObjectRef      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/objectref_functions#objget_access_url"><code dir="ltr" translate="no">        OBJ.GET_ACCESS_URL       </code></a></td>
<td>Returns access URLs for a Cloud Storage object.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/objectref_functions#objmake_ref"><code dir="ltr" translate="no">        OBJ.MAKE_REF       </code></a></td>
<td>Creates an <code dir="ltr" translate="no">       ObjectRef      </code> value that contains reference information for a Cloud Storage object.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#octet_length"><code dir="ltr" translate="no">        OCTET_LENGTH       </code></a></td>
<td>Alias for <code dir="ltr" translate="no">       BYTE_LENGTH      </code> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/conversion_functions#parse_bignumeric"><code dir="ltr" translate="no">        PARSE_BIGNUMERIC       </code></a></td>
<td>Converts a <code dir="ltr" translate="no">       STRING      </code> value to a <code dir="ltr" translate="no">       BIGNUMERIC      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/date_functions#parse_date"><code dir="ltr" translate="no">        PARSE_DATE       </code></a></td>
<td>Converts a <code dir="ltr" translate="no">       STRING      </code> value to a <code dir="ltr" translate="no">       DATE      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/datetime_functions#parse_datetime"><code dir="ltr" translate="no">        PARSE_DATETIME       </code></a></td>
<td>Converts a <code dir="ltr" translate="no">       STRING      </code> value to a <code dir="ltr" translate="no">       DATETIME      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/json_functions#parse_json"><code dir="ltr" translate="no">        PARSE_JSON       </code></a></td>
<td>Converts a JSON-formatted <code dir="ltr" translate="no">       STRING      </code> value to a <code dir="ltr" translate="no">       JSON      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/conversion_functions#parse_numeric"><code dir="ltr" translate="no">        PARSE_NUMERIC       </code></a></td>
<td>Converts a <code dir="ltr" translate="no">       STRING      </code> value to a <code dir="ltr" translate="no">       NUMERIC      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/time_functions#parse_time"><code dir="ltr" translate="no">        PARSE_TIME       </code></a></td>
<td>Converts a <code dir="ltr" translate="no">       STRING      </code> value to a <code dir="ltr" translate="no">       TIME      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#parse_timestamp"><code dir="ltr" translate="no">        PARSE_TIMESTAMP       </code></a></td>
<td>Converts a <code dir="ltr" translate="no">       STRING      </code> value to a <code dir="ltr" translate="no">       TIMESTAMP      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/numbering_functions#percent_rank"><code dir="ltr" translate="no">        PERCENT_RANK       </code></a></td>
<td>Gets the percentile rank (from 0 to 1) of each row within a window.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/navigation_functions#percentile_cont"><code dir="ltr" translate="no">        PERCENTILE_CONT       </code></a></td>
<td>Computes the specified percentile for a value, using linear interpolation.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/aggregate-dp-functions#dp_percentile_cont"><code dir="ltr" translate="no">        PERCENTILE_CONT       </code> (Differential Privacy)</a></td>
<td><code dir="ltr" translate="no">       DIFFERENTIAL_PRIVACY      </code> -supported <code dir="ltr" translate="no">       PERCENTILE_CONT      </code> .<br />
<br />
Computes a differentially-private percentile across privacy unit columns in a query with a <code dir="ltr" translate="no">       DIFFERENTIAL_PRIVACY      </code> clause.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/navigation_functions#percentile_disc"><code dir="ltr" translate="no">        PERCENTILE_DISC       </code></a></td>
<td>Computes the specified percentile for a discrete value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#pow"><code dir="ltr" translate="no">        POW       </code></a></td>
<td>Produces the value of <code dir="ltr" translate="no">       X      </code> raised to the power of <code dir="ltr" translate="no">       Y      </code> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#power"><code dir="ltr" translate="no">        POWER       </code></a></td>
<td>Synonym of <code dir="ltr" translate="no">       POW      </code> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#rand"><code dir="ltr" translate="no">        RAND       </code></a></td>
<td>Generates a pseudo-random value of type <code dir="ltr" translate="no">       FLOAT64      </code> in the range of <code dir="ltr" translate="no">       [0, 1)      </code> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/range-functions#range"><code dir="ltr" translate="no">        RANGE       </code></a></td>
<td>Constructs a range of <code dir="ltr" translate="no">       DATE      </code> , <code dir="ltr" translate="no">       DATETIME      </code> , or <code dir="ltr" translate="no">       TIMESTAMP      </code> values.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#range_bucket"><code dir="ltr" translate="no">        RANGE_BUCKET       </code></a></td>
<td>Scans through a sorted array and returns the 0-based position of a point's upper bound.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/range-functions#range_contains"><code dir="ltr" translate="no">        RANGE_CONTAINS       </code></a></td>
<td>Signature 1: Checks if one range is in another range.<br />
<br />
Signature 2: Checks if a value is in a range.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/range-functions#range_end"><code dir="ltr" translate="no">        RANGE_END       </code></a></td>
<td>Gets the upper bound of a range.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/range-functions#range_intersect"><code dir="ltr" translate="no">        RANGE_INTERSECT       </code></a></td>
<td>Gets a segment of two ranges that intersect.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/range-functions#range_overlaps"><code dir="ltr" translate="no">        RANGE_OVERLAPS       </code></a></td>
<td>Checks if two ranges overlap.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/range-functions#range_sessionize"><code dir="ltr" translate="no">        RANGE_SESSIONIZE       </code></a></td>
<td>Produces a table of sessionized ranges.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/range-functions#range_start"><code dir="ltr" translate="no">        RANGE_START       </code></a></td>
<td>Gets the lower bound of a range.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/numbering_functions#rank"><code dir="ltr" translate="no">        RANK       </code></a></td>
<td>Gets the rank (1-based) of each row within a window.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#regexp_contains"><code dir="ltr" translate="no">        REGEXP_CONTAINS       </code></a></td>
<td>Checks if a value is a partial match for a regular expression.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#regexp_extract"><code dir="ltr" translate="no">        REGEXP_EXTRACT       </code></a></td>
<td>Produces a substring that matches a regular expression.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#regexp_extract_all"><code dir="ltr" translate="no">        REGEXP_EXTRACT_ALL       </code></a></td>
<td>Produces an array of all substrings that match a regular expression.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#regexp_instr"><code dir="ltr" translate="no">        REGEXP_INSTR       </code></a></td>
<td>Finds the position of a regular expression match in a value, optionally starting the search at a given offset or occurrence.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#regexp_replace"><code dir="ltr" translate="no">        REGEXP_REPLACE       </code></a></td>
<td>Produces a <code dir="ltr" translate="no">       STRING      </code> value where all substrings that match a regular expression are replaced with a specified value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#regexp_substr"><code dir="ltr" translate="no">        REGEXP_SUBSTR       </code></a></td>
<td>Synonym for <code dir="ltr" translate="no">       REGEXP_EXTRACT      </code> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#repeat"><code dir="ltr" translate="no">        REPEAT       </code></a></td>
<td>Produces a <code dir="ltr" translate="no">       STRING      </code> or <code dir="ltr" translate="no">       BYTES      </code> value that consists of an original value, repeated.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#replace"><code dir="ltr" translate="no">        REPLACE       </code></a></td>
<td>Replaces all occurrences of a pattern with another pattern in a <code dir="ltr" translate="no">       STRING      </code> or <code dir="ltr" translate="no">       BYTES      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#reverse"><code dir="ltr" translate="no">        REVERSE       </code></a></td>
<td>Reverses a <code dir="ltr" translate="no">       STRING      </code> or <code dir="ltr" translate="no">       BYTES      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#right"><code dir="ltr" translate="no">        RIGHT       </code></a></td>
<td>Gets the specified rightmost portion from a <code dir="ltr" translate="no">       STRING      </code> or <code dir="ltr" translate="no">       BYTES      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#round"><code dir="ltr" translate="no">        ROUND       </code></a></td>
<td>Rounds <code dir="ltr" translate="no">       X      </code> to the nearest integer or rounds <code dir="ltr" translate="no">       X      </code> to <code dir="ltr" translate="no">       N      </code> decimal places after the decimal point.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/numbering_functions#row_number"><code dir="ltr" translate="no">        ROW_NUMBER       </code></a></td>
<td>Gets the sequential row number (1-based) of each row within a window.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#rpad"><code dir="ltr" translate="no">        RPAD       </code></a></td>
<td>Appends a <code dir="ltr" translate="no">       STRING      </code> or <code dir="ltr" translate="no">       BYTES      </code> value with a pattern.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#rtrim"><code dir="ltr" translate="no">        RTRIM       </code></a></td>
<td>Identical to the <code dir="ltr" translate="no">       TRIM      </code> function, but only removes trailing characters.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#s2_cellidfrompoint"><code dir="ltr" translate="no">        S2_CELLIDFROMPOINT       </code></a></td>
<td>Gets the S2 cell ID covering a point <code dir="ltr" translate="no">       GEOGRAPHY      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#s2_coveringcellids"><code dir="ltr" translate="no">        S2_COVERINGCELLIDS       </code></a></td>
<td>Gets an array of S2 cell IDs that cover a <code dir="ltr" translate="no">       GEOGRAPHY      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#safe_add"><code dir="ltr" translate="no">        SAFE_ADD       </code></a></td>
<td>Equivalent to the addition operator ( <code dir="ltr" translate="no">       X + Y      </code> ), but returns <code dir="ltr" translate="no">       NULL      </code> if overflow occurs.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/conversion_functions#safe_casting"><code dir="ltr" translate="no">        SAFE_CAST       </code></a></td>
<td>Similar to the <code dir="ltr" translate="no">       CAST      </code> function, but returns <code dir="ltr" translate="no">       NULL      </code> when a runtime error is produced.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#safe_convert_bytes_to_string"><code dir="ltr" translate="no">        SAFE_CONVERT_BYTES_TO_STRING       </code></a></td>
<td>Converts a <code dir="ltr" translate="no">       BYTES      </code> value to a <code dir="ltr" translate="no">       STRING      </code> value and replace any invalid UTF-8 characters with the Unicode replacement character, <code dir="ltr" translate="no">       U+FFFD      </code> .</td>
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
<td><a href="/bigquery/docs/reference/standard-sql/search_functions#search"><code dir="ltr" translate="no">        SEARCH       </code></a></td>
<td>Checks to see whether a table or other search data contains a set of search terms.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#sec"><code dir="ltr" translate="no">        SEC       </code></a></td>
<td>Computes the secant of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#sech"><code dir="ltr" translate="no">        SECH       </code></a></td>
<td>Computes the hyperbolic secant of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/security_functions#session_user"><code dir="ltr" translate="no">        SESSION_USER       </code></a></td>
<td>Get the email address or principal identifier of the user that's running the query.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/hash_functions#sha1"><code dir="ltr" translate="no">        SHA1       </code></a></td>
<td>Computes the hash of a <code dir="ltr" translate="no">       STRING      </code> or <code dir="ltr" translate="no">       BYTES      </code> value, using the SHA-1 algorithm.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/hash_functions#sha256"><code dir="ltr" translate="no">        SHA256       </code></a></td>
<td>Computes the hash of a <code dir="ltr" translate="no">       STRING      </code> or <code dir="ltr" translate="no">       BYTES      </code> value, using the SHA-256 algorithm.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/hash_functions#sha512"><code dir="ltr" translate="no">        SHA512       </code></a></td>
<td>Computes the hash of a <code dir="ltr" translate="no">       STRING      </code> or <code dir="ltr" translate="no">       BYTES      </code> value, using the SHA-512 algorithm.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#sign"><code dir="ltr" translate="no">        SIGN       </code></a></td>
<td>Produces -1 , 0, or +1 for negative, zero, and positive arguments respectively.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#sin"><code dir="ltr" translate="no">        SIN       </code></a></td>
<td>Computes the sine of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#sinh"><code dir="ltr" translate="no">        SINH       </code></a></td>
<td>Computes the hyperbolic sine of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#soundex"><code dir="ltr" translate="no">        SOUNDEX       </code></a></td>
<td>Gets the Soundex codes for words in a <code dir="ltr" translate="no">       STRING      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#split"><code dir="ltr" translate="no">        SPLIT       </code></a></td>
<td>Splits a <code dir="ltr" translate="no">       STRING      </code> or <code dir="ltr" translate="no">       BYTES      </code> value, using a delimiter.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#sqrt"><code dir="ltr" translate="no">        SQRT       </code></a></td>
<td>Computes the square root of <code dir="ltr" translate="no">       X      </code> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_angle"><code dir="ltr" translate="no">        ST_ANGLE       </code></a></td>
<td>Takes three point <code dir="ltr" translate="no">       GEOGRAPHY      </code> values, which represent two intersecting lines, and returns the angle between these lines.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_area"><code dir="ltr" translate="no">        ST_AREA       </code></a></td>
<td>Gets the area covered by the polygons in a <code dir="ltr" translate="no">       GEOGRAPHY      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_asbinary"><code dir="ltr" translate="no">        ST_ASBINARY       </code></a></td>
<td>Converts a <code dir="ltr" translate="no">       GEOGRAPHY      </code> value to a <code dir="ltr" translate="no">       BYTES      </code> WKB geography value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_asgeojson"><code dir="ltr" translate="no">        ST_ASGEOJSON       </code></a></td>
<td>Converts a <code dir="ltr" translate="no">       GEOGRAPHY      </code> value to a <code dir="ltr" translate="no">       STRING      </code> GeoJSON geography value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_astext"><code dir="ltr" translate="no">        ST_ASTEXT       </code></a></td>
<td>Converts a <code dir="ltr" translate="no">       GEOGRAPHY      </code> value to a <code dir="ltr" translate="no">       STRING      </code> WKT geography value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_azimuth"><code dir="ltr" translate="no">        ST_AZIMUTH       </code></a></td>
<td>Gets the azimuth of a line segment formed by two point <code dir="ltr" translate="no">       GEOGRAPHY      </code> values.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_boundary"><code dir="ltr" translate="no">        ST_BOUNDARY       </code></a></td>
<td>Gets the union of component boundaries in a <code dir="ltr" translate="no">       GEOGRAPHY      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_boundingbox"><code dir="ltr" translate="no">        ST_BOUNDINGBOX       </code></a></td>
<td>Gets the bounding box for a <code dir="ltr" translate="no">       GEOGRAPHY      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_buffer"><code dir="ltr" translate="no">        ST_BUFFER       </code></a></td>
<td>Gets the buffer around a <code dir="ltr" translate="no">       GEOGRAPHY      </code> value, using a specific number of segments.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_bufferwithtolerance"><code dir="ltr" translate="no">        ST_BUFFERWITHTOLERANCE       </code></a></td>
<td>Gets the buffer around a <code dir="ltr" translate="no">       GEOGRAPHY      </code> value, using tolerance.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_centroid"><code dir="ltr" translate="no">        ST_CENTROID       </code></a></td>
<td>Gets the centroid of a <code dir="ltr" translate="no">       GEOGRAPHY      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_centroid_agg"><code dir="ltr" translate="no">        ST_CENTROID_AGG       </code></a></td>
<td>Gets the centroid of a set of <code dir="ltr" translate="no">       GEOGRAPHY      </code> values.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_closestpoint"><code dir="ltr" translate="no">        ST_CLOSESTPOINT       </code></a></td>
<td>Gets the point on a <code dir="ltr" translate="no">       GEOGRAPHY      </code> value which is closest to any point in a second <code dir="ltr" translate="no">       GEOGRAPHY      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_clusterdbscan"><code dir="ltr" translate="no">        ST_CLUSTERDBSCAN       </code></a></td>
<td>Performs DBSCAN clustering on a group of <code dir="ltr" translate="no">       GEOGRAPHY      </code> values and produces a 0-based cluster number for this row.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_contains"><code dir="ltr" translate="no">        ST_CONTAINS       </code></a></td>
<td>Checks if one <code dir="ltr" translate="no">       GEOGRAPHY      </code> value contains another <code dir="ltr" translate="no">       GEOGRAPHY      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_convexhull"><code dir="ltr" translate="no">        ST_CONVEXHULL       </code></a></td>
<td>Returns the convex hull for a <code dir="ltr" translate="no">       GEOGRAPHY      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_coveredby"><code dir="ltr" translate="no">        ST_COVEREDBY       </code></a></td>
<td>Checks if all points of a <code dir="ltr" translate="no">       GEOGRAPHY      </code> value are on the boundary or interior of another <code dir="ltr" translate="no">       GEOGRAPHY      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_covers"><code dir="ltr" translate="no">        ST_COVERS       </code></a></td>
<td>Checks if all points of a <code dir="ltr" translate="no">       GEOGRAPHY      </code> value are on the boundary or interior of another <code dir="ltr" translate="no">       GEOGRAPHY      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_difference"><code dir="ltr" translate="no">        ST_DIFFERENCE       </code></a></td>
<td>Gets the point set difference between two <code dir="ltr" translate="no">       GEOGRAPHY      </code> values.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_dimension"><code dir="ltr" translate="no">        ST_DIMENSION       </code></a></td>
<td>Gets the dimension of the highest-dimensional element in a <code dir="ltr" translate="no">       GEOGRAPHY      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_disjoint"><code dir="ltr" translate="no">        ST_DISJOINT       </code></a></td>
<td>Checks if two <code dir="ltr" translate="no">       GEOGRAPHY      </code> values are disjoint (don't intersect).</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_distance"><code dir="ltr" translate="no">        ST_DISTANCE       </code></a></td>
<td>Gets the shortest distance in meters between two <code dir="ltr" translate="no">       GEOGRAPHY      </code> values.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_dump"><code dir="ltr" translate="no">        ST_DUMP       </code></a></td>
<td>Returns an array of simple <code dir="ltr" translate="no">       GEOGRAPHY      </code> components in a <code dir="ltr" translate="no">       GEOGRAPHY      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_dwithin"><code dir="ltr" translate="no">        ST_DWITHIN       </code></a></td>
<td>Checks if any points in two <code dir="ltr" translate="no">       GEOGRAPHY      </code> values are within a given distance.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_endpoint"><code dir="ltr" translate="no">        ST_ENDPOINT       </code></a></td>
<td>Gets the last point of a linestring <code dir="ltr" translate="no">       GEOGRAPHY      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_equals"><code dir="ltr" translate="no">        ST_EQUALS       </code></a></td>
<td>Checks if two <code dir="ltr" translate="no">       GEOGRAPHY      </code> values represent the same <code dir="ltr" translate="no">       GEOGRAPHY      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_extent"><code dir="ltr" translate="no">        ST_EXTENT       </code></a></td>
<td>Gets the bounding box for a group of <code dir="ltr" translate="no">       GEOGRAPHY      </code> values.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_exteriorring"><code dir="ltr" translate="no">        ST_EXTERIORRING       </code></a></td>
<td>Returns a linestring <code dir="ltr" translate="no">       GEOGRAPHY      </code> value that corresponds to the outermost ring of a polygon <code dir="ltr" translate="no">       GEOGRAPHY      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_geogfrom"><code dir="ltr" translate="no">        ST_GEOGFROM       </code></a></td>
<td>Converts a <code dir="ltr" translate="no">       STRING      </code> or <code dir="ltr" translate="no">       BYTES      </code> value into a <code dir="ltr" translate="no">       GEOGRAPHY      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_geogfromgeojson"><code dir="ltr" translate="no">        ST_GEOGFROMGEOJSON       </code></a></td>
<td>Converts a <code dir="ltr" translate="no">       STRING      </code> GeoJSON geometry value into a <code dir="ltr" translate="no">       GEOGRAPHY      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_geogfromtext"><code dir="ltr" translate="no">        ST_GEOGFROMTEXT       </code></a></td>
<td>Converts a <code dir="ltr" translate="no">       STRING      </code> WKT geometry value into a <code dir="ltr" translate="no">       GEOGRAPHY      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_geogfromwkb"><code dir="ltr" translate="no">        ST_GEOGFROMWKB       </code></a></td>
<td>Converts a <code dir="ltr" translate="no">       BYTES      </code> or hexadecimal-text <code dir="ltr" translate="no">       STRING      </code> WKT geometry value into a <code dir="ltr" translate="no">       GEOGRAPHY      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_geogpoint"><code dir="ltr" translate="no">        ST_GEOGPOINT       </code></a></td>
<td>Creates a point <code dir="ltr" translate="no">       GEOGRAPHY      </code> value for a given longitude and latitude.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_geogpointfromgeohash"><code dir="ltr" translate="no">        ST_GEOGPOINTFROMGEOHASH       </code></a></td>
<td>Gets a point <code dir="ltr" translate="no">       GEOGRAPHY      </code> value that's in the middle of a bounding box defined in a <code dir="ltr" translate="no">       STRING      </code> GeoHash value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_geohash"><code dir="ltr" translate="no">        ST_GEOHASH       </code></a></td>
<td>Converts a point <code dir="ltr" translate="no">       GEOGRAPHY      </code> value to a <code dir="ltr" translate="no">       STRING      </code> GeoHash value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_geometrytype"><code dir="ltr" translate="no">        ST_GEOMETRYTYPE       </code></a></td>
<td>Gets the Open Geospatial Consortium (OGC) geometry type for a <code dir="ltr" translate="no">       GEOGRAPHY      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_hausdorffdistance"><code dir="ltr" translate="no">        ST_HAUSDORFFDISTANCE       </code></a></td>
<td>Gets the discrete Hausdorff distance between two geometries.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_hausdorffdwithin"><code dir="ltr" translate="no">        ST_HAUSDORFFDWITHIN       </code></a></td>
<td>Checks if the Hausdorff distance between two <code dir="ltr" translate="no">       GEOGRAPHY      </code> values is within a given distance.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_interiorrings"><code dir="ltr" translate="no">        ST_INTERIORRINGS       </code></a></td>
<td>Gets the interior rings of a polygon <code dir="ltr" translate="no">       GEOGRAPHY      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_intersection"><code dir="ltr" translate="no">        ST_INTERSECTION       </code></a></td>
<td>Gets the point set intersection of two <code dir="ltr" translate="no">       GEOGRAPHY      </code> values.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_intersects"><code dir="ltr" translate="no">        ST_INTERSECTS       </code></a></td>
<td>Checks if at least one point appears in two <code dir="ltr" translate="no">       GEOGRAPHY      </code> values.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_intersectsbox"><code dir="ltr" translate="no">        ST_INTERSECTSBOX       </code></a></td>
<td>Checks if a <code dir="ltr" translate="no">       GEOGRAPHY      </code> value intersects a rectangle.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_isclosed"><code dir="ltr" translate="no">        ST_ISCLOSED       </code></a></td>
<td>Checks if all components in a <code dir="ltr" translate="no">       GEOGRAPHY      </code> value are closed.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_iscollection"><code dir="ltr" translate="no">        ST_ISCOLLECTION       </code></a></td>
<td>Checks if the total number of points, linestrings, and polygons is greater than one in a <code dir="ltr" translate="no">       GEOGRAPHY      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_isempty"><code dir="ltr" translate="no">        ST_ISEMPTY       </code></a></td>
<td>Checks if a <code dir="ltr" translate="no">       GEOGRAPHY      </code> value is empty.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_isring"><code dir="ltr" translate="no">        ST_ISRING       </code></a></td>
<td>Checks if a <code dir="ltr" translate="no">       GEOGRAPHY      </code> value is a closed, simple linestring.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_length"><code dir="ltr" translate="no">        ST_LENGTH       </code></a></td>
<td>Gets the total length of lines in a <code dir="ltr" translate="no">       GEOGRAPHY      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_lineinterpolatepoint"><code dir="ltr" translate="no">        ST_LINEINTERPOLATEPOINT       </code></a></td>
<td>Gets a point at a specific fraction in a linestring <code dir="ltr" translate="no">       GEOGRAPHY      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_linelocatepoint"><code dir="ltr" translate="no">        ST_LINELOCATEPOINT       </code></a></td>
<td>Gets a section of a linestring <code dir="ltr" translate="no">       GEOGRAPHY      </code> value between the start point and a point <code dir="ltr" translate="no">       GEOGRAPHY      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_linesubstring"><code dir="ltr" translate="no">        ST_LINESUBSTRING       </code></a></td>
<td>Gets a segment of a single linestring at a specific starting and ending fraction.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_makeline"><code dir="ltr" translate="no">        ST_MAKELINE       </code></a></td>
<td>Creates a linestring <code dir="ltr" translate="no">       GEOGRAPHY      </code> value by concatenating the point and linestring vertices of <code dir="ltr" translate="no">       GEOGRAPHY      </code> values.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_makepolygon"><code dir="ltr" translate="no">        ST_MAKEPOLYGON       </code></a></td>
<td>Constructs a polygon <code dir="ltr" translate="no">       GEOGRAPHY      </code> value by combining a polygon shell with polygon holes.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_makepolygonoriented"><code dir="ltr" translate="no">        ST_MAKEPOLYGONORIENTED       </code></a></td>
<td>Constructs a polygon <code dir="ltr" translate="no">       GEOGRAPHY      </code> value, using an array of linestring <code dir="ltr" translate="no">       GEOGRAPHY      </code> values. The vertex ordering of each linestring determines the orientation of each polygon ring.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_maxdistance"><code dir="ltr" translate="no">        ST_MAXDISTANCE       </code></a></td>
<td>Gets the longest distance between two non-empty <code dir="ltr" translate="no">       GEOGRAPHY      </code> values.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_npoints"><code dir="ltr" translate="no">        ST_NPOINTS       </code></a></td>
<td>An alias of <code dir="ltr" translate="no">       ST_NUMPOINTS      </code> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_numgeometries"><code dir="ltr" translate="no">        ST_NUMGEOMETRIES       </code></a></td>
<td>Gets the number of geometries in a <code dir="ltr" translate="no">       GEOGRAPHY      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_numpoints"><code dir="ltr" translate="no">        ST_NUMPOINTS       </code></a></td>
<td>Gets the number of vertices in the a <code dir="ltr" translate="no">       GEOGRAPHY      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_perimeter"><code dir="ltr" translate="no">        ST_PERIMETER       </code></a></td>
<td>Gets the length of the boundary of the polygons in a <code dir="ltr" translate="no">       GEOGRAPHY      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_pointn"><code dir="ltr" translate="no">        ST_POINTN       </code></a></td>
<td>Gets the point at a specific index of a linestring <code dir="ltr" translate="no">       GEOGRAPHY      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_regionstats"><code dir="ltr" translate="no">        ST_REGIONSTATS       </code></a></td>
<td>Computes statistics describing the pixels in a geospatial raster image that intersect a <code dir="ltr" translate="no">       GEOGRAPHY      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_simplify"><code dir="ltr" translate="no">        ST_SIMPLIFY       </code></a></td>
<td>Converts a <code dir="ltr" translate="no">       GEOGRAPHY      </code> value into a simplified <code dir="ltr" translate="no">       GEOGRAPHY      </code> value, using tolerance.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_snaptogrid"><code dir="ltr" translate="no">        ST_SNAPTOGRID       </code></a></td>
<td>Produces a <code dir="ltr" translate="no">       GEOGRAPHY      </code> value, where each vertex has been snapped to a longitude/latitude grid.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_startpoint"><code dir="ltr" translate="no">        ST_STARTPOINT       </code></a></td>
<td>Gets the first point of a linestring <code dir="ltr" translate="no">       GEOGRAPHY      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_touches"><code dir="ltr" translate="no">        ST_TOUCHES       </code></a></td>
<td>Checks if two <code dir="ltr" translate="no">       GEOGRAPHY      </code> values intersect and their interiors have no elements in common.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_union"><code dir="ltr" translate="no">        ST_UNION       </code></a></td>
<td>Gets the point set union of multiple <code dir="ltr" translate="no">       GEOGRAPHY      </code> values.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_union_agg"><code dir="ltr" translate="no">        ST_UNION_AGG       </code></a></td>
<td>Aggregates over <code dir="ltr" translate="no">       GEOGRAPHY      </code> values and gets their point set union.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_within"><code dir="ltr" translate="no">        ST_WITHIN       </code></a></td>
<td>Checks if one <code dir="ltr" translate="no">       GEOGRAPHY      </code> value contains another <code dir="ltr" translate="no">       GEOGRAPHY      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_x"><code dir="ltr" translate="no">        ST_X       </code></a></td>
<td>Gets the longitude from a point <code dir="ltr" translate="no">       GEOGRAPHY      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_y"><code dir="ltr" translate="no">        ST_Y       </code></a></td>
<td>Gets the latitude from a point <code dir="ltr" translate="no">       GEOGRAPHY      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#starts_with"><code dir="ltr" translate="no">        STARTS_WITH       </code></a></td>
<td>Checks if a <code dir="ltr" translate="no">       STRING      </code> or <code dir="ltr" translate="no">       BYTES      </code> value is a prefix of another value.</td>
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
<td><a href="/bigquery/docs/reference/standard-sql/json_functions#string_for_json"><code dir="ltr" translate="no">        STRING       </code> (JSON)</a></td>
<td>Converts a JSON string to a SQL <code dir="ltr" translate="no">       STRING      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#string"><code dir="ltr" translate="no">        STRING       </code> (Timestamp)</a></td>
<td>Converts a <code dir="ltr" translate="no">       TIMESTAMP      </code> value to a <code dir="ltr" translate="no">       STRING      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#string_agg"><code dir="ltr" translate="no">        STRING_AGG       </code></a></td>
<td>Concatenates non- <code dir="ltr" translate="no">       NULL      </code> <code dir="ltr" translate="no">       STRING      </code> or <code dir="ltr" translate="no">       BYTES      </code> values.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#strpos"><code dir="ltr" translate="no">        STRPOS       </code></a></td>
<td>Finds the position of the first occurrence of a subvalue inside another value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#substr"><code dir="ltr" translate="no">        SUBSTR       </code></a></td>
<td>Gets a portion of a <code dir="ltr" translate="no">       STRING      </code> or <code dir="ltr" translate="no">       BYTES      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#substring"><code dir="ltr" translate="no">        SUBSTRING       </code></a></td>
<td>Alias for <code dir="ltr" translate="no">       SUBSTR      </code></td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#sum"><code dir="ltr" translate="no">        SUM       </code></a></td>
<td>Gets the sum of non- <code dir="ltr" translate="no">       NULL      </code> values.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/aggregate-dp-functions#dp_sum"><code dir="ltr" translate="no">        SUM       </code> (Differential Privacy)</a></td>
<td><code dir="ltr" translate="no">       DIFFERENTIAL_PRIVACY      </code> -supported <code dir="ltr" translate="no">       SUM      </code> .<br />
<br />
Gets the differentially-private sum of non- <code dir="ltr" translate="no">       NULL      </code> , non- <code dir="ltr" translate="no">       NaN      </code> values in a query with a <code dir="ltr" translate="no">       DIFFERENTIAL_PRIVACY      </code> clause.</td>
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
<td><a href="/bigquery/docs/reference/standard-sql/text-analysis-functions#text_analyze"><code dir="ltr" translate="no">        TEXT_ANALYZE       </code></a></td>
<td>Extracts terms (tokens) from text and converts them into a tokenized document.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/text-analysis-functions#tf_idf"><code dir="ltr" translate="no">        TF_IDF       </code></a></td>
<td>Evaluates how relevant a term (token) is to a tokenized document in a set of tokenized documents.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/time_functions#time"><code dir="ltr" translate="no">        TIME       </code></a></td>
<td>Constructs a <code dir="ltr" translate="no">       TIME      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/time_functions#time_add"><code dir="ltr" translate="no">        TIME_ADD       </code></a></td>
<td>Adds a specified time interval to a <code dir="ltr" translate="no">       TIME      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/time_functions#time_diff"><code dir="ltr" translate="no">        TIME_DIFF       </code></a></td>
<td>Gets the number of unit boundaries between two <code dir="ltr" translate="no">       TIME      </code> values at a particular time granularity.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/time_functions#time_sub"><code dir="ltr" translate="no">        TIME_SUB       </code></a></td>
<td>Subtracts a specified time interval from a <code dir="ltr" translate="no">       TIME      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/time_functions#time_trunc"><code dir="ltr" translate="no">        TIME_TRUNC       </code></a></td>
<td>Truncates a <code dir="ltr" translate="no">       TIME      </code> value at a particular granularity.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#timestamp"><code dir="ltr" translate="no">        TIMESTAMP       </code></a></td>
<td>Constructs a <code dir="ltr" translate="no">       TIMESTAMP      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#timestamp_add"><code dir="ltr" translate="no">        TIMESTAMP_ADD       </code></a></td>
<td>Adds a specified time interval to a <code dir="ltr" translate="no">       TIMESTAMP      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/time-series-functions#timestamp_bucket"><code dir="ltr" translate="no">        TIMESTAMP_BUCKET       </code></a></td>
<td>Gets the lower bound of the timestamp bucket that contains a timestamp.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#timestamp_diff"><code dir="ltr" translate="no">        TIMESTAMP_DIFF       </code></a></td>
<td>Gets the number of unit boundaries between two <code dir="ltr" translate="no">       TIMESTAMP      </code> values at a particular time granularity.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#timestamp_micros"><code dir="ltr" translate="no">        TIMESTAMP_MICROS       </code></a></td>
<td>Converts the number of microseconds since 1970-01-01 00:00:00 UTC to a <code dir="ltr" translate="no">       TIMESTAMP      </code> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#timestamp_millis"><code dir="ltr" translate="no">        TIMESTAMP_MILLIS       </code></a></td>
<td>Converts the number of milliseconds since 1970-01-01 00:00:00 UTC to a <code dir="ltr" translate="no">       TIMESTAMP      </code> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#timestamp_seconds"><code dir="ltr" translate="no">        TIMESTAMP_SECONDS       </code></a></td>
<td>Converts the number of seconds since 1970-01-01 00:00:00 UTC to a <code dir="ltr" translate="no">       TIMESTAMP      </code> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#timestamp_sub"><code dir="ltr" translate="no">        TIMESTAMP_SUB       </code></a></td>
<td>Subtracts a specified time interval from a <code dir="ltr" translate="no">       TIMESTAMP      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#timestamp_trunc"><code dir="ltr" translate="no">        TIMESTAMP_TRUNC       </code></a></td>
<td>Truncates a <code dir="ltr" translate="no">       TIMESTAMP      </code> or <code dir="ltr" translate="no">       DATETIME      </code> value at a particular granularity.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#to_base32"><code dir="ltr" translate="no">        TO_BASE32       </code></a></td>
<td>Converts a <code dir="ltr" translate="no">       BYTES      </code> value to a base32-encoded <code dir="ltr" translate="no">       STRING      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#to_base64"><code dir="ltr" translate="no">        TO_BASE64       </code></a></td>
<td>Converts a <code dir="ltr" translate="no">       BYTES      </code> value to a base64-encoded <code dir="ltr" translate="no">       STRING      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#to_code_points"><code dir="ltr" translate="no">        TO_CODE_POINTS       </code></a></td>
<td>Converts a <code dir="ltr" translate="no">       STRING      </code> or <code dir="ltr" translate="no">       BYTES      </code> value into an array of extended ASCII code points.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#to_hex"><code dir="ltr" translate="no">        TO_HEX       </code></a></td>
<td>Converts a <code dir="ltr" translate="no">       BYTES      </code> value to a hexadecimal <code dir="ltr" translate="no">       STRING      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/json_functions#to_json"><code dir="ltr" translate="no">        TO_JSON       </code></a></td>
<td>Converts a SQL value to a JSON value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/json_functions#to_json_string"><code dir="ltr" translate="no">        TO_JSON_STRING       </code></a></td>
<td>Converts a SQL value to a JSON-formatted <code dir="ltr" translate="no">       STRING      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#translate"><code dir="ltr" translate="no">        TRANSLATE       </code></a></td>
<td>Within a value, replaces each source character with the corresponding target character.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#trim"><code dir="ltr" translate="no">        TRIM       </code></a></td>
<td>Removes the specified leading and trailing Unicode code points or bytes from a <code dir="ltr" translate="no">       STRING      </code> or <code dir="ltr" translate="no">       BYTES      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#trunc"><code dir="ltr" translate="no">        TRUNC       </code></a></td>
<td>Rounds a number like <code dir="ltr" translate="no">       ROUND(X)      </code> or <code dir="ltr" translate="no">       ROUND(X, N)      </code> , but always rounds towards zero and never overflows.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/utility-functions#typeof"><code dir="ltr" translate="no">        TYPEOF       </code></a></td>
<td>Gets the name of the data type for an expression.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#unicode"><code dir="ltr" translate="no">        UNICODE       </code></a></td>
<td>Gets the Unicode code point for the first character in a value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/date_functions#unix_date"><code dir="ltr" translate="no">        UNIX_DATE       </code></a></td>
<td>Converts a <code dir="ltr" translate="no">       DATE      </code> value to the number of days since 1970-01-01.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#unix_micros"><code dir="ltr" translate="no">        UNIX_MICROS       </code></a></td>
<td>Converts a <code dir="ltr" translate="no">       TIMESTAMP      </code> value to the number of microseconds since 1970-01-01 00:00:00 UTC.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#unix_millis"><code dir="ltr" translate="no">        UNIX_MILLIS       </code></a></td>
<td>Converts a <code dir="ltr" translate="no">       TIMESTAMP      </code> value to the number of milliseconds since 1970-01-01 00:00:00 UTC.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#unix_seconds"><code dir="ltr" translate="no">        UNIX_SECONDS       </code></a></td>
<td>Converts a <code dir="ltr" translate="no">       TIMESTAMP      </code> value to the number of seconds since 1970-01-01 00:00:00 UTC.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#upper"><code dir="ltr" translate="no">        UPPER       </code></a></td>
<td>Formats alphabetic characters in a <code dir="ltr" translate="no">       STRING      </code> value as uppercase.<br />
<br />
Formats ASCII characters in a <code dir="ltr" translate="no">       BYTES      </code> value as uppercase.</td>
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
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/search_functions#vector_search"><code dir="ltr" translate="no">        VECTOR_SEARCH       </code></a></td>
<td>Performs a vector search on embeddings to find semantically similar entities.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/vectorindex_functions#vector_indexstatistics"><code dir="ltr" translate="no">        VECTOR_INDEX.STATISTICS       </code></a></td>
<td>Calculate how much an indexed table's data has drifted between when a vector index was trained and the present.</td>
</tr>
</tbody>
</table>
