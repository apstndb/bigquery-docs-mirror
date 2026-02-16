GoogleSQL for BigQuery supports conversion functions. These data type conversions are explicit, but some conversions can happen implicitly. You can learn more about implicit and explicit conversion [here](/bigquery/docs/reference/standard-sql/conversion_rules) .

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
<td><a href="/bigquery/docs/reference/standard-sql/array_functions#array_to_string"><code dir="ltr" translate="no">        ARRAY_TO_STRING       </code></a></td>
<td>Produces a concatenation of the elements in an array as a <code dir="ltr" translate="no">       STRING      </code> value.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/array_functions">Array functions</a> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/json_functions#bool_for_json"><code dir="ltr" translate="no">        BOOL       </code></a></td>
<td>Converts a JSON boolean to a SQL <code dir="ltr" translate="no">       BOOL      </code> value.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/json_functions">JSON functions</a> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/conversion_functions#cast"><code dir="ltr" translate="no">        CAST       </code></a></td>
<td>Convert the results of an expression to the given type.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#chr"><code dir="ltr" translate="no">        CHR       </code></a></td>
<td>Converts a Unicode code point to a character.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/string_functions">String functions</a> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#code_points_to_bytes"><code dir="ltr" translate="no">        CODE_POINTS_TO_BYTES       </code></a></td>
<td>Converts an array of extended ASCII code points to a <code dir="ltr" translate="no">       BYTES      </code> value.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/string_functions">String aggregate functions</a> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#code_points_to_string"><code dir="ltr" translate="no">        CODE_POINTS_TO_STRING       </code></a></td>
<td>Converts an array of extended ASCII code points to a <code dir="ltr" translate="no">       STRING      </code> value.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/string_functions">String aggregate functions</a> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/date_functions#date_from_unix_date"><code dir="ltr" translate="no">        DATE_FROM_UNIX_DATE       </code></a></td>
<td>Interprets an <code dir="ltr" translate="no">       INT64      </code> expression as the number of days since 1970-01-01.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/date_functions">Date functions</a> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#from_base32"><code dir="ltr" translate="no">        FROM_BASE32       </code></a></td>
<td>Converts a base32-encoded <code dir="ltr" translate="no">       STRING      </code> value into a <code dir="ltr" translate="no">       BYTES      </code> value.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/string_functions">String functions</a> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#from_base64"><code dir="ltr" translate="no">        FROM_BASE64       </code></a></td>
<td>Converts a base64-encoded <code dir="ltr" translate="no">       STRING      </code> value into a <code dir="ltr" translate="no">       BYTES      </code> value.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/string_functions">String functions</a> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#from_hex"><code dir="ltr" translate="no">        FROM_HEX       </code></a></td>
<td>Converts a hexadecimal-encoded <code dir="ltr" translate="no">       STRING      </code> value into a <code dir="ltr" translate="no">       BYTES      </code> value.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/string_functions">String functions</a> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/json_functions#int64_for_json"><code dir="ltr" translate="no">        INT64       </code></a></td>
<td>Converts a JSON number to a SQL <code dir="ltr" translate="no">       INT64      </code> value.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/json_functions">JSON functions</a> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/json_functions#lax_bool"><code dir="ltr" translate="no">        LAX_BOOL       </code></a></td>
<td>Attempts to convert a JSON value to a SQL <code dir="ltr" translate="no">       BOOL      </code> value.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/json_functions">JSON functions</a> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/json_functions#lax_double"><code dir="ltr" translate="no">        LAX_FLOAT64       </code></a></td>
<td>Attempts to convert a JSON value to a SQL <code dir="ltr" translate="no">       FLOAT64      </code> value.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/json_functions">JSON functions</a> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/json_functions#lax_int64"><code dir="ltr" translate="no">        LAX_INT64       </code></a></td>
<td>Attempts to convert a JSON value to a SQL <code dir="ltr" translate="no">       INT64      </code> value.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/json_functions">JSON functions</a> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/json_functions#lax_string"><code dir="ltr" translate="no">        LAX_STRING       </code></a></td>
<td>Attempts to convert a JSON value to a SQL <code dir="ltr" translate="no">       STRING      </code> value.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/json_functions">JSON functions</a> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/conversion_functions#parse_bignumeric"><code dir="ltr" translate="no">        PARSE_BIGNUMERIC       </code></a></td>
<td>Converts a <code dir="ltr" translate="no">       STRING      </code> value to a <code dir="ltr" translate="no">       BIGNUMERIC      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/date_functions#parse_date"><code dir="ltr" translate="no">        PARSE_DATE       </code></a></td>
<td>Converts a <code dir="ltr" translate="no">       STRING      </code> value to a <code dir="ltr" translate="no">       DATE      </code> value.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/date_functions">Date functions</a> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/datetime_functions#parse_datetime"><code dir="ltr" translate="no">        PARSE_DATETIME       </code></a></td>
<td>Converts a <code dir="ltr" translate="no">       STRING      </code> value to a <code dir="ltr" translate="no">       DATETIME      </code> value.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/datetime_functions">Datetime functions</a> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/json_functions#parse_json"><code dir="ltr" translate="no">        PARSE_JSON       </code></a></td>
<td>Converts a JSON-formatted <code dir="ltr" translate="no">       STRING      </code> value to a <code dir="ltr" translate="no">       JSON      </code> value.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/json_functions">JSON functions</a> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/conversion_functions#parse_numeric"><code dir="ltr" translate="no">        PARSE_NUMERIC       </code></a></td>
<td>Converts a <code dir="ltr" translate="no">       STRING      </code> value to a <code dir="ltr" translate="no">       NUMERIC      </code> value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/time_functions#parse_time"><code dir="ltr" translate="no">        PARSE_TIME       </code></a></td>
<td>Converts a <code dir="ltr" translate="no">       STRING      </code> value to a <code dir="ltr" translate="no">       TIME      </code> value.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/time_functions">Time functions</a> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#parse_timestamp"><code dir="ltr" translate="no">        PARSE_TIMESTAMP       </code></a></td>
<td>Converts a <code dir="ltr" translate="no">       STRING      </code> value to a <code dir="ltr" translate="no">       TIMESTAMP      </code> value.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/timestamp_functions">Timestamp functions</a> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/conversion_functions#safe_casting"><code dir="ltr" translate="no">        SAFE_CAST       </code></a></td>
<td>Similar to the <code dir="ltr" translate="no">       CAST      </code> function, but returns <code dir="ltr" translate="no">       NULL      </code> when a runtime error is produced.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#safe_convert_bytes_to_string"><code dir="ltr" translate="no">        SAFE_CONVERT_BYTES_TO_STRING       </code></a></td>
<td>Converts a <code dir="ltr" translate="no">       BYTES      </code> value to a <code dir="ltr" translate="no">       STRING      </code> value and replace any invalid UTF-8 characters with the Unicode replacement character, <code dir="ltr" translate="no">       U+FFFD      </code> .<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/string_functions">String functions</a> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/json_functions#string_for_json"><code dir="ltr" translate="no">        STRING       </code> (JSON)</a></td>
<td>Converts a JSON string to a SQL <code dir="ltr" translate="no">       STRING      </code> value.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/json_functions">JSON functions</a> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#string"><code dir="ltr" translate="no">        STRING       </code> (Timestamp)</a></td>
<td>Converts a <code dir="ltr" translate="no">       TIMESTAMP      </code> value to a <code dir="ltr" translate="no">       STRING      </code> value.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/timestamp_functions">Timestamp functions</a> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#timestamp_micros"><code dir="ltr" translate="no">        TIMESTAMP_MICROS       </code></a></td>
<td>Converts the number of microseconds since 1970-01-01 00:00:00 UTC to a <code dir="ltr" translate="no">       TIMESTAMP      </code> .<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/timestamp_functions">Timestamp functions</a> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#timestamp_millis"><code dir="ltr" translate="no">        TIMESTAMP_MILLIS       </code></a></td>
<td>Converts the number of milliseconds since 1970-01-01 00:00:00 UTC to a <code dir="ltr" translate="no">       TIMESTAMP      </code> .<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/timestamp_functions">Timestamp functions</a> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#timestamp_seconds"><code dir="ltr" translate="no">        TIMESTAMP_SECONDS       </code></a></td>
<td>Converts the number of seconds since 1970-01-01 00:00:00 UTC to a <code dir="ltr" translate="no">       TIMESTAMP      </code> .<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/timestamp_functions">Timestamp functions</a> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#to_base32"><code dir="ltr" translate="no">        TO_BASE32       </code></a></td>
<td>Converts a <code dir="ltr" translate="no">       BYTES      </code> value to a base32-encoded <code dir="ltr" translate="no">       STRING      </code> value.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/string_functions">String functions</a> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#to_base64"><code dir="ltr" translate="no">        TO_BASE64       </code></a></td>
<td>Converts a <code dir="ltr" translate="no">       BYTES      </code> value to a base64-encoded <code dir="ltr" translate="no">       STRING      </code> value.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/string_functions">String functions</a> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#to_code_points"><code dir="ltr" translate="no">        TO_CODE_POINTS       </code></a></td>
<td>Converts a <code dir="ltr" translate="no">       STRING      </code> or <code dir="ltr" translate="no">       BYTES      </code> value into an array of extended ASCII code points.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/string_functions">String functions</a> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#to_hex"><code dir="ltr" translate="no">        TO_HEX       </code></a></td>
<td>Converts a <code dir="ltr" translate="no">       BYTES      </code> value to a hexadecimal <code dir="ltr" translate="no">       STRING      </code> value.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/string_functions">String functions</a> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/json_functions#to_json"><code dir="ltr" translate="no">        TO_JSON       </code></a></td>
<td>Converts a SQL value to a JSON value.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/json_functions">JSON functions</a> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/json_functions#to_json_string"><code dir="ltr" translate="no">        TO_JSON_STRING       </code></a></td>
<td>Converts a SQL value to a JSON-formatted <code dir="ltr" translate="no">       STRING      </code> value.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/json_functions">JSON functions</a> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/date_functions#unix_date"><code dir="ltr" translate="no">        UNIX_DATE       </code></a></td>
<td>Converts a <code dir="ltr" translate="no">       DATE      </code> value to the number of days since 1970-01-01.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/date_functions">Date functions</a> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#unix_micros"><code dir="ltr" translate="no">        UNIX_MICROS       </code></a></td>
<td>Converts a <code dir="ltr" translate="no">       TIMESTAMP      </code> value to the number of microseconds since 1970-01-01 00:00:00 UTC.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/timestamp_functions">Timestamp functions</a> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#unix_millis"><code dir="ltr" translate="no">        UNIX_MILLIS       </code></a></td>
<td>Converts a <code dir="ltr" translate="no">       TIMESTAMP      </code> value to the number of milliseconds since 1970-01-01 00:00:00 UTC.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/timestamp_functions">Timestamp functions</a> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#unix_seconds"><code dir="ltr" translate="no">        UNIX_SECONDS       </code></a></td>
<td>Converts a <code dir="ltr" translate="no">       TIMESTAMP      </code> value to the number of seconds since 1970-01-01 00:00:00 UTC.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/timestamp_functions">Timestamp functions</a> .</td>
</tr>
</tbody>
</table>

## `     CAST    `

``` text
CAST(expression AS typename [format_clause])
```

**Description**

Cast syntax is used in a query to indicate that the result type of an expression should be converted to some other type.

When using `  CAST  ` , a query can fail if GoogleSQL is unable to perform the cast. If you want to protect your queries from these types of errors, you can use [SAFE\_CAST](#safe_casting) .

Casts between supported types that don't successfully map from the original value to the target domain produce runtime errors. For example, casting `  BYTES  ` to `  STRING  ` where the byte sequence isn't valid UTF-8 results in a runtime error.

Some casts can include a [format clause](/bigquery/docs/reference/standard-sql/format-elements#formatting_syntax) , which provides instructions for how to conduct the cast. For example, you could instruct a cast to convert a sequence of bytes to a BASE64-encoded string instead of a UTF-8-encoded string.

The structure of the format clause is unique to each type of cast and more information is available in the section for that cast.

**Examples**

The following query results in `  "true"  ` if `  x  ` is `  1  ` , `  "false"  ` for any other non- `  NULL  ` value, and `  NULL  ` if `  x  ` is `  NULL  ` .

``` text
CAST(x=1 AS STRING)
```

### CAST AS ARRAY

``` text
CAST(expression AS ARRAY<element_type>)
```

**Description**

GoogleSQL supports [casting](#cast) to `  ARRAY  ` . The `  expression  ` parameter can represent an expression for these data types:

  - `  ARRAY  `

**Conversion rules**

<table>
<thead>
<tr class="header">
<th>From</th>
<th>To</th>
<th>Rule(s) when casting <code dir="ltr" translate="no">       x      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       ARRAY      </code></td>
<td><code dir="ltr" translate="no">       ARRAY      </code></td>
<td>Must be the exact same array type.</td>
</tr>
</tbody>
</table>

### CAST AS BIGNUMERIC

``` text
CAST(expression AS BIGNUMERIC)
```

**Description**

GoogleSQL supports [casting](#cast) to `  BIGNUMERIC  ` . The `  expression  ` parameter can represent an expression for these data types:

  - `  INT64  `
  - `  FLOAT64  `
  - `  NUMERIC  `
  - `  BIGNUMERIC  `
  - `  STRING  `

**Conversion rules**

<table>
<thead>
<tr class="header">
<th>From</th>
<th>To</th>
<th>Rule(s) when casting <code dir="ltr" translate="no">       x      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>FLOAT64</td>
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
<td>The floating point number will round <a href="https://en.wikipedia.org/wiki/Rounding#Round_half_away_from_zero">half away from zero</a> . Casting a <code dir="ltr" translate="no">       NaN      </code> , <code dir="ltr" translate="no">       +inf      </code> or <code dir="ltr" translate="no">       -inf      </code> will return an error. Casting a value outside the range of <code dir="ltr" translate="no">       BIGNUMERIC      </code> returns an overflow error.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
<td>The numeric literal contained in the string must not exceed the maximum precision or range of the <code dir="ltr" translate="no">       BIGNUMERIC      </code> type, or an error will occur. If the number of digits after the decimal point exceeds 38, then the resulting <code dir="ltr" translate="no">       BIGNUMERIC      </code> value will round <a href="https://en.wikipedia.org/wiki/Rounding#Round_half_away_from_zero">half away from zero</a> to have 38 digits after the decimal point.</td>
</tr>
</tbody>
</table>

### CAST AS BOOL

``` text
CAST(expression AS BOOL)
```

**Description**

GoogleSQL supports [casting](#cast) to `  BOOL  ` . The `  expression  ` parameter can represent an expression for these data types:

  - `  INT64  `
  - `  BOOL  `
  - `  STRING  `

**Conversion rules**

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>From</th>
<th>To</th>
<th>Rule(s) when casting <code dir="ltr" translate="no">       x      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>INT64</td>
<td><code dir="ltr" translate="no">       BOOL      </code></td>
<td>Returns <code dir="ltr" translate="no">       FALSE      </code> if <code dir="ltr" translate="no">       x      </code> is <code dir="ltr" translate="no">       0      </code> , <code dir="ltr" translate="no">       TRUE      </code> otherwise.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><code dir="ltr" translate="no">       BOOL      </code></td>
<td>Returns <code dir="ltr" translate="no">       TRUE      </code> if <code dir="ltr" translate="no">       x      </code> is <code dir="ltr" translate="no">       "true"      </code> and <code dir="ltr" translate="no">       FALSE      </code> if <code dir="ltr" translate="no">       x      </code> is <code dir="ltr" translate="no">       "false"      </code><br />
All other values of <code dir="ltr" translate="no">       x      </code> are invalid and throw an error instead of casting to a boolean.<br />
A string is case-insensitive when converting to a boolean.</td>
</tr>
</tbody>
</table>

### CAST AS BYTES

``` text
CAST(expression AS BYTES [format_clause])
```

**Description**

GoogleSQL supports [casting](#cast) to `  BYTES  ` . The `  expression  ` parameter can represent an expression for these data types:

  - `  BYTES  `
  - `  STRING  `

**Format clause**

When an expression of one type is cast to another type, you can use the [format clause](/bigquery/docs/reference/standard-sql/format-elements#formatting_syntax) to provide instructions for how to conduct the cast. You can use the format clause in this section if `  expression  ` is a `  STRING  ` .

  - [Format string as bytes](/bigquery/docs/reference/standard-sql/format-elements#format_string_as_bytes)

**Conversion rules**

<table>
<thead>
<tr class="header">
<th>From</th>
<th>To</th>
<th>Rule(s) when casting <code dir="ltr" translate="no">       x      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><code dir="ltr" translate="no">       BYTES      </code></td>
<td>Strings are cast to bytes using UTF-8 encoding. For example, the string "©", when cast to bytes, would become a 2-byte sequence with the hex values C2 and A9.</td>
</tr>
</tbody>
</table>

### CAST AS DATE

``` text
CAST(expression AS DATE [format_clause])
```

**Description**

GoogleSQL supports [casting](#cast) to `  DATE  ` . The `  expression  ` parameter can represent an expression for these data types:

  - `  STRING  `
  - `  DATETIME  `
  - `  TIMESTAMP  `

**Format clause**

When an expression of one type is cast to another type, you can use the [format clause](/bigquery/docs/reference/standard-sql/format-elements#formatting_syntax) to provide instructions for how to conduct the cast. You can use the format clause in this section if `  expression  ` is a `  STRING  ` .

  - [Format string as date and time](/bigquery/docs/reference/standard-sql/format-elements#format_string_as_datetime)

**Conversion rules**

<table>
<thead>
<tr class="header">
<th>From</th>
<th>To</th>
<th>Rule(s) when casting <code dir="ltr" translate="no">       x      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><code dir="ltr" translate="no">       DATE      </code></td>
<td>When casting from string to date, the string must conform to the supported date literal format, and is independent of time zone. If the string expression is invalid or represents a date that's outside of the supported min/max range, then an error is produced.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td><code dir="ltr" translate="no">       DATE      </code></td>
<td>Casting from a timestamp to date effectively truncates the timestamp as of the default time zone.</td>
</tr>
</tbody>
</table>

### CAST AS DATETIME

``` text
CAST(expression AS DATETIME [format_clause])
```

**Description**

GoogleSQL supports [casting](#cast) to `  DATETIME  ` . The `  expression  ` parameter can represent an expression for these data types:

  - `  STRING  `
  - `  DATETIME  `
  - `  TIMESTAMP  `

**Format clause**

When an expression of one type is cast to another type, you can use the [format clause](/bigquery/docs/reference/standard-sql/format-elements#formatting_syntax) to provide instructions for how to conduct the cast. You can use the format clause in this section if `  expression  ` is a `  STRING  ` .

  - [Format string as date and time](/bigquery/docs/reference/standard-sql/format-elements#format_string_as_datetime)

**Conversion rules**

<table>
<thead>
<tr class="header">
<th>From</th>
<th>To</th>
<th>Rule(s) when casting <code dir="ltr" translate="no">       x      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><code dir="ltr" translate="no">       DATETIME      </code></td>
<td>When casting from string to datetime, the string must conform to the supported datetime literal format, and is independent of time zone. If the string expression is invalid or represents a datetime that's outside of the supported min/max range, then an error is produced.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td><code dir="ltr" translate="no">       DATETIME      </code></td>
<td>Casting from a timestamp to datetime effectively truncates the timestamp as of the default time zone.</td>
</tr>
</tbody>
</table>

### CAST AS FLOAT64

``` text
CAST(expression AS FLOAT64)
```

**Description**

GoogleSQL supports [casting](#cast) to floating point types. The `  expression  ` parameter can represent an expression for these data types:

  - `  INT64  `
  - `  FLOAT64  `
  - `  NUMERIC  `
  - `  BIGNUMERIC  `
  - `  STRING  `

**Conversion rules**

<table>
<thead>
<tr class="header">
<th>From</th>
<th>To</th>
<th>Rule(s) when casting <code dir="ltr" translate="no">       x      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>INT64</td>
<td>FLOAT64</td>
<td>Returns a close but potentially not exact floating point value.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td>FLOAT64</td>
<td><code dir="ltr" translate="no">       NUMERIC      </code> will convert to the closest floating point number with a possible loss of precision.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
<td>FLOAT64</td>
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code> will convert to the closest floating point number with a possible loss of precision.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>FLOAT64</td>
<td>Returns <code dir="ltr" translate="no">       x      </code> as a floating point value, interpreting it as having the same form as a valid floating point literal. Also supports casts from <code dir="ltr" translate="no">       "[+,-]inf"      </code> to <code dir="ltr" translate="no">       [,-]Infinity      </code> , <code dir="ltr" translate="no">       "[+,-]infinity"      </code> to <code dir="ltr" translate="no">       [,-]Infinity      </code> , and <code dir="ltr" translate="no">       "[+,-]nan"      </code> to <code dir="ltr" translate="no">       NaN      </code> . Conversions are case-insensitive.</td>
</tr>
</tbody>
</table>

### CAST AS INT64

``` text
CAST(expression AS INT64)
```

**Description**

GoogleSQL supports [casting](#cast) to integer types. The `  expression  ` parameter can represent an expression for these data types:

  - `  INT64  `
  - `  FLOAT64  `
  - `  NUMERIC  `
  - `  BIGNUMERIC  `
  - `  BOOL  `
  - `  STRING  `

**Conversion rules**

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>From</th>
<th>To</th>
<th>Rule(s) when casting <code dir="ltr" translate="no">       x      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>FLOAT64</td>
<td>INT64</td>
<td>Returns the closest integer value.<br />
Halfway cases such as 1.5 or -0.5 round away from zero.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       BOOL      </code></td>
<td>INT64</td>
<td>Returns <code dir="ltr" translate="no">       1      </code> if <code dir="ltr" translate="no">       x      </code> is <code dir="ltr" translate="no">       TRUE      </code> , <code dir="ltr" translate="no">       0      </code> otherwise.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>INT64</td>
<td>A hex string can be cast to an integer. For example, <code dir="ltr" translate="no">       0x123      </code> to <code dir="ltr" translate="no">       291      </code> or <code dir="ltr" translate="no">       -0x123      </code> to <code dir="ltr" translate="no">       -291      </code> .</td>
</tr>
</tbody>
</table>

**Examples**

If you are working with hex strings ( `  0x123  ` ), you can cast those strings as integers:

``` text
SELECT '0x123' as hex_value, CAST('0x123' as INT64) as hex_to_int;

/*-----------+------------+
 | hex_value | hex_to_int |
 +-----------+------------+
 | 0x123     | 291        |
 +-----------+------------*/
```

``` text
SELECT '-0x123' as hex_value, CAST('-0x123' as INT64) as hex_to_int;

/*-----------+------------+
 | hex_value | hex_to_int |
 +-----------+------------+
 | -0x123    | -291       |
 +-----------+------------*/
```

### CAST AS INTERVAL

``` text
CAST(expression AS INTERVAL)
```

**Description**

GoogleSQL supports [casting](#cast) to `  INTERVAL  ` . The `  expression  ` parameter can represent an expression for these data types:

  - `  STRING  `

**Conversion rules**

<table>
<thead>
<tr class="header">
<th>From</th>
<th>To</th>
<th>Rule(s) when casting <code dir="ltr" translate="no">       x      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><code dir="ltr" translate="no">       INTERVAL      </code></td>
<td>When casting from string to interval, the string must conform to either <a href="https://en.wikipedia.org/wiki/ISO_8601#Durations">ISO 8601 Duration</a> standard or to interval literal format 'Y-M D H:M:S.F'. Partial interval literal formats are also accepted when they aren't ambiguous, for example 'H:M:S'. If the string expression is invalid or represents an interval that is outside of the supported min/max range, then an error is produced.</td>
</tr>
</tbody>
</table>

**Examples**

``` text
SELECT input, CAST(input AS INTERVAL) AS output
FROM UNNEST([
  '1-2 3 10:20:30.456',
  '1-2',
  '10:20:30',
  'P1Y2M3D',
  'PT10H20M30,456S'
]) input

/*--------------------+--------------------+
 | input              | output             |
 +--------------------+--------------------+
 | 1-2 3 10:20:30.456 | 1-2 3 10:20:30.456 |
 | 1-2                | 1-2 0 0:0:0        |
 | 10:20:30           | 0-0 0 10:20:30     |
 | P1Y2M3D            | 1-2 3 0:0:0        |
 | PT10H20M30,456S    | 0-0 0 10:20:30.456 |
 +--------------------+--------------------*/
```

### CAST AS NUMERIC

``` text
CAST(expression AS NUMERIC)
```

**Description**

GoogleSQL supports [casting](#cast) to `  NUMERIC  ` . The `  expression  ` parameter can represent an expression for these data types:

  - `  INT64  `
  - `  FLOAT64  `
  - `  NUMERIC  `
  - `  BIGNUMERIC  `
  - `  STRING  `

**Conversion rules**

<table>
<thead>
<tr class="header">
<th>From</th>
<th>To</th>
<th>Rule(s) when casting <code dir="ltr" translate="no">       x      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td>The floating point number will round <a href="https://en.wikipedia.org/wiki/Rounding#Round_half_away_from_zero">half away from zero</a> . Casting a <code dir="ltr" translate="no">       NaN      </code> , <code dir="ltr" translate="no">       +inf      </code> or <code dir="ltr" translate="no">       -inf      </code> will return an error. Casting a value outside the range of <code dir="ltr" translate="no">       NUMERIC      </code> returns an overflow error.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td>The numeric literal contained in the string must not exceed the maximum precision or range of the <code dir="ltr" translate="no">       NUMERIC      </code> type, or an error will occur. If the number of digits after the decimal point exceeds nine, then the resulting <code dir="ltr" translate="no">       NUMERIC      </code> value will round <a href="https://en.wikipedia.org/wiki/Rounding#Round_half_away_from_zero">half away from zero</a> . to have nine digits after the decimal point.</td>
</tr>
</tbody>
</table>

### CAST AS RANGE

``` text
CAST(expression AS RANGE)
```

**Description**

GoogleSQL supports [casting](#cast) to `  RANGE  ` . The `  expression  ` parameter can represent an expression for these data types:

  - `  STRING  `

**Conversion rules**

<table>
<thead>
<tr class="header">
<th>From</th>
<th>To</th>
<th>Rule(s) when casting <code dir="ltr" translate="no">       x      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><code dir="ltr" translate="no">       RANGE      </code></td>
<td>When casting from string to range, the string must conform to the supported range literal format. If the string expression is invalid or represents a range that's outside of the supported subtype min/max range, then an error is produced.</td>
</tr>
</tbody>
</table>

**Examples**

``` text
SELECT CAST(
  '[2020-01-01, 2020-01-02)'
  AS RANGE<DATE>) AS string_to_range

/*----------------------------------------+
 | string_to_range                        |
 +----------------------------------------+
 | [DATE '2020-01-01', DATE '2020-01-02') |
 +----------------------------------------*/
```

``` text
SELECT CAST(
  '[2014-09-27 12:30:00.45, 2016-10-17 11:15:00.33)'
  AS RANGE<DATETIME>) AS string_to_range

/*------------------------------------------------------------------------+
 | string_to_range                                                        |
 +------------------------------------------------------------------------+
 | [DATETIME '2014-09-27 12:30:00.45', DATETIME '2016-10-17 11:15:00.33') |
 +------------------------------------------------------------------------*/
```

``` text
SELECT CAST(
  '[2014-09-27 12:30:00+08, 2016-10-17 11:15:00+08)'
  AS RANGE<TIMESTAMP>) AS string_to_range

-- Results depend upon where this query was executed.
/*---------------------------------------------------------------------------+
 | string_to_range                                                           |
 +---------------------------------------------------------------------------+
 | [TIMESTAMP '2014-09-27 12:30:00+08', TIMESTAMP '2016-10-17 11:15:00 UTC') |
 +---------------------------------------------------------------------------*/
```

``` text
SELECT CAST(
  '[UNBOUNDED, 2020-01-02)'
  AS RANGE<DATE>) AS string_to_range

/*--------------------------------+
 | string_to_range                |
 +--------------------------------+
 | [UNBOUNDED, DATE '2020-01-02') |
 +--------------------------------*/
```

``` text
SELECT CAST(
  '[2020-01-01, NULL)'
  AS RANGE<DATE>) AS string_to_range

/*--------------------------------+
 | string_to_range                |
 +--------------------------------+
 | [DATE '2020-01-01', UNBOUNDED) |
 +--------------------------------*/
```

### CAST AS STRING

``` text
CAST(expression AS STRING [format_clause [AT TIME ZONE timezone_expr]])
```

**Description**

GoogleSQL supports [casting](#cast) to `  STRING  ` . The `  expression  ` parameter can represent an expression for these data types:

  - `  INT64  `
  - `  FLOAT64  `
  - `  NUMERIC  `
  - `  BIGNUMERIC  `
  - `  BOOL  `
  - `  BYTES  `
  - `  TIME  `
  - `  DATE  `
  - `  DATETIME  `
  - `  TIMESTAMP  `
  - `  RANGE  `
  - `  INTERVAL  `
  - `  STRING  `

**Format clause**

When an expression of one type is cast to another type, you can use the [format clause](/bigquery/docs/reference/standard-sql/format-elements#formatting_syntax) to provide instructions for how to conduct the cast. You can use the format clause in this section if `  expression  ` is one of these data types:

  - `  INT64  `
  - `  FLOAT64  `
  - `  NUMERIC  `
  - `  BIGNUMERIC  `
  - `  BYTES  `
  - `  TIME  `
  - `  DATE  `
  - `  DATETIME  `
  - `  TIMESTAMP  `

The format clause for `  STRING  ` has an additional optional clause called `  AT TIME ZONE timezone_expr  ` , which you can use to specify a specific time zone to use during formatting of a `  TIMESTAMP  ` . If this optional clause isn't included when formatting a `  TIMESTAMP  ` , the default time zone, UTC, is used.

For more information, see the following topics:

  - [Format bytes as string](/bigquery/docs/reference/standard-sql/format-elements#format_bytes_as_string)
  - [Format date and time as string](/bigquery/docs/reference/standard-sql/format-elements#format_date_time_as_string)
  - [Format numeric type as string](/bigquery/docs/reference/standard-sql/format-elements#format_numeric_type_as_string)

**Conversion rules**

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>From</th>
<th>To</th>
<th>Rule(s) when casting <code dir="ltr" translate="no">       x      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>FLOAT64</td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Returns an approximate string representation. A returned <code dir="ltr" translate="no">       NaN      </code> or <code dir="ltr" translate="no">       0      </code> will not be signed.<br />
</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       BOOL      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Returns <code dir="ltr" translate="no">       "true"      </code> if <code dir="ltr" translate="no">       x      </code> is <code dir="ltr" translate="no">       TRUE      </code> , <code dir="ltr" translate="no">       "false"      </code> otherwise.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       BYTES      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Returns <code dir="ltr" translate="no">       x      </code> interpreted as a UTF-8 string.<br />
For example, the bytes literal <code dir="ltr" translate="no">       b'\xc2\xa9'      </code> , when cast to a string, is interpreted as UTF-8 and becomes the unicode character "©".<br />
An error occurs if <code dir="ltr" translate="no">       x      </code> isn't valid UTF-8.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       TIME      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Casting from a time type to a string is independent of time zone and is of the form <code dir="ltr" translate="no">       HH:MM:SS      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       DATE      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Casting from a date type to a string is independent of time zone and is of the form <code dir="ltr" translate="no">       YYYY-MM-DD      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       DATETIME      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Casting from a datetime type to a string is independent of time zone and is of the form <code dir="ltr" translate="no">       YYYY-MM-DD HH:MM:SS      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>When casting from timestamp types to string, the timestamp is interpreted using the default time zone, UTC. The number of subsecond digits produced depends on the number of trailing zeroes in the subsecond part: the CAST function will truncate zero, three, or six digits.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       INTERVAL      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Casting from an interval to a string is of the form <code dir="ltr" translate="no">       Y-M D H:M:S      </code> .</td>
</tr>
</tbody>
</table>

**Examples**

``` text
SELECT CAST(CURRENT_DATE() AS STRING) AS current_date

/*---------------+
 | current_date  |
 +---------------+
 | 2021-03-09    |
 +---------------*/
```

``` text
SELECT CAST(CURRENT_DATE() AS STRING FORMAT 'DAY') AS current_day

/*-------------+
 | current_day |
 +-------------+
 | MONDAY      |
 +-------------*/
```

``` text
SELECT CAST(
  TIMESTAMP '2008-12-25 00:00:00+00:00'
  AS STRING FORMAT 'YYYY-MM-DD HH24:MI:SS TZH:TZM') AS date_time_to_string

-- Results depend upon where this query was executed.
/*------------------------------+
 | date_time_to_string          |
 +------------------------------+
 | 2008-12-24 16:00:00 -08:00   |
 +------------------------------*/
```

``` text
SELECT CAST(
  TIMESTAMP '2008-12-25 00:00:00+00:00'
  AS STRING FORMAT 'YYYY-MM-DD HH24:MI:SS TZH:TZM'
  AT TIME ZONE 'Asia/Kolkata') AS date_time_to_string

-- Because the time zone is specified, the result is always the same.
/*------------------------------+
 | date_time_to_string          |
 +------------------------------+
 | 2008-12-25 05:30:00 +05:30   |
 +------------------------------*/
```

``` text
SELECT CAST(INTERVAL 3 DAY AS STRING) AS interval_to_string

/*--------------------+
 | interval_to_string |
 +--------------------+
 | 0-0 3 0:0:0        |
 +--------------------*/
```

``` text
SELECT CAST(
  INTERVAL "1-2 3 4:5:6.789" YEAR TO SECOND
  AS STRING) AS interval_to_string

/*--------------------+
 | interval_to_string |
 +--------------------+
 | 1-2 3 4:5:6.789    |
 +--------------------*/
```

### CAST AS STRUCT

``` text
CAST(expression AS STRUCT)
```

**Description**

GoogleSQL supports [casting](#cast) to `  STRUCT  ` . The `  expression  ` parameter can represent an expression for these data types:

  - `  STRUCT  `

**Conversion rules**

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>From</th>
<th>To</th>
<th>Rule(s) when casting <code dir="ltr" translate="no">       x      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       STRUCT      </code></td>
<td><code dir="ltr" translate="no">       STRUCT      </code></td>
<td>Allowed if the following conditions are met:<br />

<ol>
<li>The two structs have the same number of fields.</li>
<li>The original struct field types can be explicitly cast to the corresponding target struct field types (as defined by field order, not field name).</li>
</ol></td>
</tr>
</tbody>
</table>

### CAST AS TIME

``` text
CAST(expression AS TIME [format_clause])
```

**Description**

GoogleSQL supports [casting](#cast) to TIME. The `  expression  ` parameter can represent an expression for these data types:

  - `  STRING  `
  - `  TIME  `
  - `  DATETIME  `
  - `  TIMESTAMP  `

**Format clause**

When an expression of one type is cast to another type, you can use the [format clause](/bigquery/docs/reference/standard-sql/format-elements#formatting_syntax) to provide instructions for how to conduct the cast. You can use the format clause in this section if `  expression  ` is a `  STRING  ` .

  - [Format string as date and time](/bigquery/docs/reference/standard-sql/format-elements#format_string_as_datetime)

**Conversion rules**

<table>
<thead>
<tr class="header">
<th>From</th>
<th>To</th>
<th>Rule(s) when casting <code dir="ltr" translate="no">       x      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><code dir="ltr" translate="no">       TIME      </code></td>
<td>When casting from string to time, the string must conform to the supported time literal format, and is independent of time zone. If the string expression is invalid or represents a time that's outside of the supported min/max range, then an error is produced.</td>
</tr>
</tbody>
</table>

### CAST AS TIMESTAMP

``` text
CAST(expression AS TIMESTAMP [format_clause [AT TIME ZONE timezone_expr]])
```

**Description**

GoogleSQL supports [casting](#cast) to `  TIMESTAMP  ` . The `  expression  ` parameter can represent an expression for these data types:

  - `  STRING  `
  - `  DATETIME  `
  - `  TIMESTAMP  `

**Format clause**

When an expression of one type is cast to another type, you can use the [format clause](/bigquery/docs/reference/standard-sql/format-elements#formatting_syntax) to provide instructions for how to conduct the cast. You can use the format clause in this section if `  expression  ` is a `  STRING  ` .

  - [Format string as date and time](/bigquery/docs/reference/standard-sql/format-elements#format_string_as_datetime)

The format clause for `  TIMESTAMP  ` has an additional optional clause called `  AT TIME ZONE timezone_expr  ` , which you can use to specify a specific time zone to use during formatting. If this optional clause isn't included, the default time zone, UTC, is used.

**Conversion rules**

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>From</th>
<th>To</th>
<th>Rule(s) when casting <code dir="ltr" translate="no">       x      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>When casting from string to a timestamp, <code dir="ltr" translate="no">       string_expression      </code> must conform to the supported timestamp literal formats, or else a runtime error occurs. The <code dir="ltr" translate="no">       string_expression      </code> may itself contain a time zone.<br />
<br />
If there is a time zone in the <code dir="ltr" translate="no">       string_expression      </code> , that time zone is used for conversion, otherwise the default time zone, UTC, is used. If the string has fewer than six digits, then it's implicitly widened.<br />
<br />
An error is produced if the <code dir="ltr" translate="no">       string_expression      </code> is invalid, has more than six subsecond digits (i.e., precision greater than microseconds), or represents a time outside of the supported timestamp range.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       DATE      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>Casting from a date to a timestamp interprets <code dir="ltr" translate="no">       date_expression      </code> as of midnight (start of the day) in the default time zone, UTC.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       DATETIME      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>Casting from a datetime to a timestamp interprets <code dir="ltr" translate="no">       datetime_expression      </code> in the default time zone, UTC.<br />
<br />
Most valid datetime values have exactly one corresponding timestamp in each time zone. However, there are certain combinations of valid datetime values and time zones that have zero or two corresponding timestamp values. This happens in a time zone when clocks are set forward or set back, such as for Daylight Savings Time. When there are two valid timestamps, the earlier one is used. When there is no valid timestamp, the length of the gap in time (typically one hour) is added to the datetime.</td>
</tr>
</tbody>
</table>

**Examples**

The following example casts a string-formatted timestamp as a timestamp:

``` text
SELECT CAST("2020-06-02 17:00:53.110+00:00" AS TIMESTAMP) AS as_timestamp

-- Results depend upon where this query was executed.
/*-----------------------------+
 | as_timestamp                |
 +-----------------------------+
 | 2020-06-03 00:00:53.110 UTC |
 +-----------------------------*/
```

The following examples cast a string-formatted date and time as a timestamp. These examples return the same output as the previous example.

``` text
SELECT CAST('06/02/2020 17:00:53.110' AS TIMESTAMP FORMAT 'MM/DD/YYYY HH24:MI:SS.FF3' AT TIME ZONE 'UTC') AS as_timestamp
```

``` text
SELECT CAST('06/02/2020 17:00:53.110' AS TIMESTAMP FORMAT 'MM/DD/YYYY HH24:MI:SS.FF3' AT TIME ZONE '+00') AS as_timestamp
```

``` text
SELECT CAST('06/02/2020 17:00:53.110 +00' AS TIMESTAMP FORMAT 'MM/DD/YYYY HH24:MI:SS.FF3 TZH') AS as_timestamp
```

## `     PARSE_BIGNUMERIC    `

``` text
PARSE_BIGNUMERIC(string_expression)
```

**Description**

Converts a `  STRING  ` to a `  BIGNUMERIC  ` value.

The numeric literal contained in the string must not exceed the [maximum precision or range](/bigquery/docs/reference/standard-sql/data-types#decimal_types) of the `  BIGNUMERIC  ` type, or an error occurs. If the number of digits after the decimal point exceeds 38, then the resulting `  BIGNUMERIC  ` value rounds [half away from zero](https://en.wikipedia.org/wiki/Rounding#Round_half_away_from_zero) to have 38 digits after the decimal point.

``` text
-- This example shows how a string with a decimal point is parsed.
SELECT PARSE_BIGNUMERIC("123.45") AS parsed;

/*--------+
 | parsed |
 +--------+
 | 123.45 |
 +--------*/

-- This example shows how a string with an exponent is parsed.
SELECT PARSE_BIGNUMERIC("123.456E37") AS parsed;

/*-----------------------------------------+
 | parsed                                  |
 +-----------------------------------------+
 | 123400000000000000000000000000000000000 |
 +-----------------------------------------*/

-- This example shows the rounding when digits after the decimal point exceeds 38.
SELECT PARSE_BIGNUMERIC("1.123456789012345678901234567890123456789") as parsed;

/*------------------------------------------+
 | parsed                                   |
 +------------------------------------------+
 | 1.12345678901234567890123456789012345679 |
 +------------------------------------------*/
```

This function is similar to using the [`  CAST AS BIGNUMERIC  `](#cast_bignumeric) function except that the `  PARSE_BIGNUMERIC  ` function only accepts string inputs and allows the following in the string:

  - Spaces between the sign (+/-) and the number
  - Signs (+/-) after the number

Rules for valid input strings:

<table>
<thead>
<tr class="header">
<th>Rule</th>
<th>Example Input</th>
<th>Output</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>The string can only contain digits, commas, decimal points and signs.</td>
<td>"- 12,34567,89.0"</td>
<td>-123456789</td>
</tr>
<tr class="even">
<td>Whitespaces are allowed anywhere except between digits.</td>
<td>" - 12.345 "</td>
<td>-12.345</td>
</tr>
<tr class="odd">
<td>Only digits and commas are allowed before the decimal point.</td>
<td>" 12,345,678"</td>
<td>12345678</td>
</tr>
<tr class="even">
<td>Only digits are allowed after the decimal point.</td>
<td>"1.234 "</td>
<td>1.234</td>
</tr>
<tr class="odd">
<td>Use <code dir="ltr" translate="no">       E      </code> or <code dir="ltr" translate="no">       e      </code> for exponents. After the <code dir="ltr" translate="no">       e      </code> , digits and a leading sign indicator are allowed.</td>
<td>" 123.45e-1"</td>
<td>12.345</td>
</tr>
<tr class="even">
<td>If the integer part isn't empty, then it must contain at least one digit.</td>
<td>" 0,.12 -"</td>
<td>-0.12</td>
</tr>
<tr class="odd">
<td>If the string contains a decimal point, then it must contain at least one digit.</td>
<td>" .1"</td>
<td>0.1</td>
</tr>
<tr class="even">
<td>The string can't contain more than one sign.</td>
<td>" 0.5 +"</td>
<td>0.5</td>
</tr>
</tbody>
</table>

**Return Data Type**

`  BIGNUMERIC  `

**Examples**

This example shows an input with spaces before, after, and between the sign and the number:

``` text
SELECT PARSE_BIGNUMERIC("  -  12.34 ") as parsed;

/*--------+
 | parsed |
 +--------+
 | -12.34 |
 +--------*/
```

This example shows an input with an exponent as well as the sign after the number:

``` text
SELECT PARSE_BIGNUMERIC("12.34e-1-") as parsed;

/*--------+
 | parsed |
 +--------+
 | -1.234 |
 +--------*/
```

This example shows an input with multiple commas in the integer part of the number:

``` text
SELECT PARSE_BIGNUMERIC("  1,2,,3,.45 + ") as parsed;

/*--------+
 | parsed |
 +--------+
 | 123.45 |
 +--------*/
```

This example shows an input with a decimal point and no digits in the whole number part:

``` text
SELECT PARSE_BIGNUMERIC(".1234  ") as parsed;

/*--------+
 | parsed |
 +--------+
 | 0.1234 |
 +--------*/
```

**Examples of invalid inputs**

This example is invalid because the whole number part contains no digits:

``` text
SELECT PARSE_BIGNUMERIC(",,,.1234  ") as parsed;
```

This example is invalid because there are whitespaces between digits:

``` text
SELECT PARSE_BIGNUMERIC("1  23.4 5  ") as parsed;
```

This example is invalid because the number is empty except for an exponent:

``` text
SELECT PARSE_BIGNUMERIC("  e1 ") as parsed;
```

This example is invalid because the string contains multiple signs:

``` text
SELECT PARSE_BIGNUMERIC("  - 12.3 - ") as parsed;
```

This example is invalid because the value of the number falls outside the range of `  BIGNUMERIC  ` :

``` text
SELECT PARSE_BIGNUMERIC("12.34E100 ") as parsed;
```

This example is invalid because the string contains invalid characters:

``` text
SELECT PARSE_BIGNUMERIC("$12.34") as parsed;
```

## `     PARSE_NUMERIC    `

``` text
PARSE_NUMERIC(string_expression)
```

**Description**

Converts a `  STRING  ` to a `  NUMERIC  ` value.

The numeric literal contained in the string must not exceed the [maximum precision or range](/bigquery/docs/reference/standard-sql/data-types#decimal_types) of the `  NUMERIC  ` type, or an error occurs. If the number of digits after the decimal point exceeds nine, then the resulting `  NUMERIC  ` value rounds [half away from zero](https://en.wikipedia.org/wiki/Rounding#Round_half_away_from_zero) to have nine digits after the decimal point.

``` text
-- This example shows how a string with a decimal point is parsed.
SELECT PARSE_NUMERIC("123.45") AS parsed;

/*--------+
 | parsed |
 +--------+
 | 123.45 |
 +--------*/

-- This example shows how a string with an exponent is parsed.
SELECT PARSE_NUMERIC("12.34E27") as parsed;

/*-------------------------------+
 | parsed                        |
 +-------------------------------+
 | 12340000000000000000000000000 |
 +-------------------------------*/

-- This example shows the rounding when digits after the decimal point exceeds 9.
SELECT PARSE_NUMERIC("1.0123456789") as parsed;

/*-------------+
 | parsed      |
 +-------------+
 | 1.012345679 |
 +-------------*/
```

This function is similar to using the [`  CAST AS NUMERIC  `](#cast_numeric) function except that the `  PARSE_NUMERIC  ` function only accepts string inputs and allows the following in the string:

  - Spaces between the sign (+/-) and the number
  - Signs (+/-) after the number

Rules for valid input strings:

<table>
<thead>
<tr class="header">
<th>Rule</th>
<th>Example Input</th>
<th>Output</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>The string can only contain digits, commas, decimal points and signs.</td>
<td>"- 12,34567,89.0"</td>
<td>-123456789</td>
</tr>
<tr class="even">
<td>Whitespaces are allowed anywhere except between digits.</td>
<td>" - 12.345 "</td>
<td>-12.345</td>
</tr>
<tr class="odd">
<td>Only digits and commas are allowed before the decimal point.</td>
<td>" 12,345,678"</td>
<td>12345678</td>
</tr>
<tr class="even">
<td>Only digits are allowed after the decimal point.</td>
<td>"1.234 "</td>
<td>1.234</td>
</tr>
<tr class="odd">
<td>Use <code dir="ltr" translate="no">       E      </code> or <code dir="ltr" translate="no">       e      </code> for exponents. After the <code dir="ltr" translate="no">       e      </code> , digits and a leading sign indicator are allowed.</td>
<td>" 123.45e-1"</td>
<td>12.345</td>
</tr>
<tr class="even">
<td>If the integer part isn't empty, then it must contain at least one digit.</td>
<td>" 0,.12 -"</td>
<td>-0.12</td>
</tr>
<tr class="odd">
<td>If the string contains a decimal point, then it must contain at least one digit.</td>
<td>" .1"</td>
<td>0.1</td>
</tr>
<tr class="even">
<td>The string can't contain more than one sign.</td>
<td>" 0.5 +"</td>
<td>0.5</td>
</tr>
</tbody>
</table>

**Return Data Type**

`  NUMERIC  `

**Examples**

This example shows an input with spaces before, after, and between the sign and the number:

``` text
SELECT PARSE_NUMERIC("  -  12.34 ") as parsed;

/*--------+
 | parsed |
 +--------+
 | -12.34 |
 +--------*/
```

This example shows an input with an exponent as well as the sign after the number:

``` text
SELECT PARSE_NUMERIC("12.34e-1-") as parsed;

/*--------+
 | parsed |
 +--------+
 | -1.234 |
 +--------*/
```

This example shows an input with multiple commas in the integer part of the number:

``` text
SELECT PARSE_NUMERIC("  1,2,,3,.45 + ") as parsed;

/*--------+
 | parsed |
 +--------+
 | 123.45 |
 +--------*/
```

This example shows an input with a decimal point and no digits in the whole number part:

``` text
SELECT PARSE_NUMERIC(".1234  ") as parsed;

/*--------+
 | parsed |
 +--------+
 | 0.1234 |
 +--------*/
```

**Examples of invalid inputs**

This example is invalid because the whole number part contains no digits:

``` text
SELECT PARSE_NUMERIC(",,,.1234  ") as parsed;
```

This example is invalid because there are whitespaces between digits:

``` text
SELECT PARSE_NUMERIC("1  23.4 5  ") as parsed;
```

This example is invalid because the number is empty except for an exponent:

``` text
SELECT PARSE_NUMERIC("  e1 ") as parsed;
```

This example is invalid because the string contains multiple signs:

``` text
SELECT PARSE_NUMERIC("  - 12.3 - ") as parsed;
```

This example is invalid because the value of the number falls outside the range of `  BIGNUMERIC  ` :

``` text
SELECT PARSE_NUMERIC("12.34E100 ") as parsed;
```

This example is invalid because the string contains invalid characters:

``` text
SELECT PARSE_NUMERIC("$12.34") as parsed;
```

## `     SAFE_CAST    `

``` text
SAFE_CAST(expression AS typename [format_clause])
```

**Description**

When using `  CAST  ` , a query can fail if GoogleSQL is unable to perform the cast. For example, the following query generates an error:

``` text
SELECT CAST("apple" AS INT64) AS not_a_number;
```

If you want to protect your queries from these types of errors, you can use `  SAFE_CAST  ` . `  SAFE_CAST  ` replaces runtime errors with `  NULL  ` s. However, during static analysis, impossible casts between two non-castable types still produce an error because the query is invalid.

``` text
SELECT SAFE_CAST("apple" AS INT64) AS not_a_number;

/*--------------+
 | not_a_number |
 +--------------+
 | NULL         |
 +--------------*/
```

Some casts can include a [format clause](/bigquery/docs/reference/standard-sql/format-elements#formatting_syntax) , which provides instructions for how to conduct the cast. For example, you could instruct a cast to convert a sequence of bytes to a BASE64-encoded string instead of a UTF-8-encoded string.

The structure of the format clause is unique to each type of cast and more information is available in the section for that cast.

If you are casting from bytes to strings, you can also use the function, [`  SAFE_CONVERT_BYTES_TO_STRING  `](/bigquery/docs/reference/standard-sql/string_functions#safe_convert_bytes_to_string) . Any invalid UTF-8 characters are replaced with the unicode replacement character, `  U+FFFD  ` .
