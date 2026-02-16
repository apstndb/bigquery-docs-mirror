# Legacy SQL data types

This document details the data types supported by BigQuery's legacy SQL query syntax. The preferred query syntax for BigQuery is GoogleSQL. For information on data types in GoogleSQL, see the [GoogleSQL data types](/bigquery/docs/reference/standard-sql/data-types) .

## Legacy SQL data types

Your data can include the following data types:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Data type</th>
<th>Possible values</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>STRING</td>
<td>Variable-length character (UTF-8) data.</td>
</tr>
<tr class="even">
<td>BYTES</td>
<td>Variable-length binary data.
<ul>
<li>Imported BYTES data must be base64-encoded, except for Avro BYTES data, which BigQuery can read and convert.</li>
<li>BYTES data read from a BigQuery table are base64-encoded, unless you export to Avro format, in which case the Avro bytes data type applies.</li>
</ul></td>
</tr>
<tr class="odd">
<td>INTEGER</td>
<td><p>64-bit signed integer.</p>
<p>If you are using the BigQuery API to load an integer outside the range of [-2 <sup>53</sup> +1, 2 <sup>53</sup> -1] (in most cases, this means larger than 9,007,199,254,740,991), into an integer (INT64) column, you must pass it as a string to avoid data corruption. This issue is caused by a limitation on integer size in JSON/ECMAScript. For more information, see <a href="https://www.rfc-editor.org/rfc/rfc7159.html#section-6">the Numbers section of RFC 7159</a> .</p></td>
</tr>
<tr class="even">
<td>FLOAT</td>
<td>Double-precision floating-point format.</td>
</tr>
<tr class="odd">
<td>NUMERIC</td>
<td>Legacy SQL has limited support for NUMERIC. For more information, see <a href="#numeric-type-support">Exact numeric in legacy SQL</a> .</td>
</tr>
<tr class="even">
<td>BIGNUMERIC</td>
<td>Legacy SQL has limited support for BIGNUMERIC. For more information, see <a href="#numeric-type-support">Exact numeric in legacy SQL</a> .</td>
</tr>
<tr class="odd">
<td>BOOLEAN</td>
<td><ul>
<li><strong>CSV format:</strong> <code dir="ltr" translate="no">         1        </code> or <code dir="ltr" translate="no">         0        </code> , <code dir="ltr" translate="no">         true        </code> or <code dir="ltr" translate="no">         false        </code> , <code dir="ltr" translate="no">         t        </code> or <code dir="ltr" translate="no">         f        </code> , <code dir="ltr" translate="no">         yes        </code> or <code dir="ltr" translate="no">         no        </code> , or <code dir="ltr" translate="no">         y        </code> or <code dir="ltr" translate="no">         n        </code> (all case-insensitive).</li>
<li><strong>JSON format:</strong> <code dir="ltr" translate="no">         true        </code> or <code dir="ltr" translate="no">         false        </code> (case-insensitive).</li>
</ul></td>
</tr>
<tr class="even">
<td>RECORD</td>
<td>A collection of one or more other fields.</td>
</tr>
<tr class="odd">
<td>TIMESTAMP</td>
<td><p>You can describe TIMESTAMP data types as either UNIX timestamps or calendar datetimes. BigQuery stores TIMESTAMP data internally as a UNIX timestamp with microsecond precision.</p>
<p><strong>UNIX timestamps</strong></p>
<p>A positive or negative decimal number. A positive number specifies the number of seconds since the epoch (1970-01-01 00:00:00 UTC), and a negative number specifies the number of seconds before the epoch. Up to 6 decimal places (microsecond precision) are preserved.</p>
<p><strong>Date and time strings</strong></p>
<p>A date and time string in the format <code dir="ltr" translate="no">        YYYY-MM-DD HH:MM:SS       </code> . The <code dir="ltr" translate="no">        UTC       </code> and <code dir="ltr" translate="no">        Z       </code> specifiers are supported.</p>
<p>You can supply a timezone offset in your date and time strings, but BigQuery doesn't preserve the offset after converting the value to its internal format. If you need to preserve the original timezone data, store the timezone offset in a separate column. The leading zero is required when you specify a single-digit timezone offset.</p>
<p>Date and time strings must be quoted when using JSON format.</p>
<p><strong>Examples</strong></p>
<p>The following examples show identical ways of describing specific dates, in both UNIX timestamp and date and time string formats.</p>
<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Event</th>
<th>UNIX timestamp format</th>
<th>Date/time string format</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Minor (M4.2) earthquake near Oklahoma City</td>
<td><div class="sourceCode" id="cb1" dir="ltr" data-is-upgraded="" translate="no"><pre class="sourceCode bash"><code class="sourceCode bash"><span id="cb1-1"><a href="#cb1-1"></a><span class="ex">1408452095.220</span></span>
<span id="cb1-2"><a href="#cb1-2"></a><span class="ex">1408452095.220000</span></span></code></pre></div></td>
<td><div class="sourceCode" id="cb2" dir="ltr" data-is-upgraded="" translate="no"><pre class="sourceCode bash"><code class="sourceCode bash"><span id="cb2-1"><a href="#cb2-1"></a><span class="ex">2014-08-19</span> 07:41:35.220 -05:00</span>
<span id="cb2-2"><a href="#cb2-2"></a><span class="ex">2014-08-19</span> 12:41:35.220 UTC</span>
<span id="cb2-3"><a href="#cb2-3"></a><span class="ex">2014-08-19</span> 12:41:35.220</span>
<span id="cb2-4"><a href="#cb2-4"></a><span class="ex">2014-08-19</span> 12:41:35.220000</span>
<span id="cb2-5"><a href="#cb2-5"></a><span class="ex">2014-08-19T12</span>:41:35.220Z</span></code></pre></div></td>
</tr>
<tr class="even">
<td>Neil Armstrong sets foot on the moon</td>
<td><div class="sourceCode" id="cb3" dir="ltr" data-is-upgraded="" translate="no"><pre class="sourceCode bash"><code class="sourceCode bash"><span id="cb3-1"><a href="#cb3-1"></a><span class="ex">-14182916</span></span></code></pre></div></td>
<td><div class="sourceCode" id="cb4" dir="ltr" data-is-upgraded="" translate="no"><pre class="sourceCode bash"><code class="sourceCode bash"><span id="cb4-1"><a href="#cb4-1"></a><span class="ex">1969-07-20</span> 20:18:04</span>
<span id="cb4-2"><a href="#cb4-2"></a><span class="ex">1969-07-20</span> 20:18:04 UTC</span>
<span id="cb4-3"><a href="#cb4-3"></a><span class="ex">1969-07-20T20</span>:18:04</span></code></pre></div></td>
</tr>
<tr class="odd">
<td>Deadline for fixing <a href="https://en.wikipedia.org/wiki/Year_10,000_problem">Y10k bug</a></td>
<td><div class="sourceCode" id="cb5" dir="ltr" data-is-upgraded="" translate="no"><pre class="sourceCode bash"><code class="sourceCode bash"><span id="cb5-1"><a href="#cb5-1"></a><span class="ex">253402300800</span></span>
<span id="cb5-2"><a href="#cb5-2"></a><span class="ex">2.53402300800e11</span></span></code></pre></div></td>
<td><div class="sourceCode" id="cb6" dir="ltr" data-is-upgraded="" translate="no"><pre class="sourceCode bash"><code class="sourceCode bash"><span id="cb6-1"><a href="#cb6-1"></a><span class="ex">10000-01-01</span> 00:00</span></code></pre></div></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>DATE</td>
<td>Legacy SQL has limited support for DATE. For more information, see <a href="#civil-time">Civil time in legacy SQL</a> .</td>
</tr>
<tr class="odd">
<td>TIME</td>
<td>Legacy SQL has limited support for TIME. For more information, see <a href="#civil-time">Civil time in legacy SQL</a> .</td>
</tr>
<tr class="even">
<td>DATETIME</td>
<td>Legacy SQL has limited support for DATETIME. For more information, see <a href="#civil-time">Civil time in legacy SQL</a> .</td>
</tr>
</tbody>
</table>

## Exact numeric in legacy SQL

You can read NUMERIC or BIGNUMERIC values in non-modifying clauses such as `  SELECT list (with aliases)  ` , `  GROUP BY keys  ` , and pass-through fields in window functions, and so on. However, any computation over NUMERIC or BIGNUMERIC values, including comparisons, produces undefined results.

The following cast and conversion functions are supported in legacy SQL:

  - `  CAST(<numeric> AS STRING)  `
  - `  CAST(<bignumeric> AS STRING)  `
  - `  CAST(<string> AS NUMERIC)  `
  - `  CAST(<string> AS BIGNUMERIC)  `

## Civil time in legacy SQL

You can read civil time data types—DATE, TIME, and DATETIME—and process them with non-modifying operators such as `  SELECT list (with aliases)  ` , `  GROUP BY keys  ` , and pass-through fields in window functions, etc. However, any other computation over civil time values, including comparisons, produces undefined results.

The following casts and conversion functions are supported in legacy SQL:

  - `  CAST(<date> AS STRING)  `
  - `  CAST(<time> AS STRING)  `
  - `  CAST(<datetime> AS STRING)  `
  - `  CAST(<string> AS DATE)  `
  - `  CAST(<string> AS TIME)  `
  - `  CAST(<string> AS DATETIME)  `

In practice, legacy SQL interprets civil time values as integers, and operations on integers that you think are civil time values produce unexpected results.

To compute values using civil time data types, consider [GoogleSQL](/bigquery/sql-reference) , which supports all SQL operations on the [DATE](/bigquery/sql-reference/data-types#date-type) , [DATETIME](/bigquery/sql-reference/data-types#datetime-type) , and [TIME](/bigquery/sql-reference/data-types#time-type) data types.

## What's next

  - To set a field's data type using the API, see [`  schema.fields.type  `](/bigquery/docs/reference/rest/v2/tables#TableFieldSchema.FIELDS.type) .
  - For GoogleSQL data types, see [data types](/bigquery/sql-reference/data-types) .
