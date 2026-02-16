# Teradata SQL translation guide

This document details the similarities and differences in SQL syntax between Teradata and BigQuery to help you plan your migration. Use [batch SQL translation](/bigquery/docs/batch-sql-translator) to migrate your SQL scripts in bulk, or [interactive SQL translation](/bigquery/docs/interactive-sql-translator) to translate ad-hoc queries.

## Data types

This section shows equivalents between data types in Teradata and in BigQuery.

**Note:** Teradata supports [`  DEFAULT  `](https://docs.teradata.com/r/Enterprise_IntelliFlex_VMware/SQL-Data-Definition-Language-Syntax-and-Examples/Table-Statements/CREATE-TABLE-and-CREATE-TABLE-AS/Syntax-Elements/column_partition_definition/column_data_type_attribute/DEFAULT?tocId=FGX%7EnkdqLciLCOJTJMvFnA) and other [constraints](https://docs.teradata.com/r/Enterprise_IntelliFlex_VMware/SQL-Data-Definition-Language-Syntax-and-Examples/Table-Statements/CREATE-TABLE-and-CREATE-TABLE-AS/Syntax-Elements/column_partition_definition/table_constraint) ; these are not used in BigQuery.

<table style="width:29%;">
<colgroup>
<col style="width: 28%" />
<col style="width: 0%" />
<col style="width: 0%" />
</colgroup>
<thead>
<tr class="header">
<th>Teradata</th>
<th>BigQuery</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         INTEGER       </code></td>
<td><code dir="ltr" translate="no">         INT64       </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         SMALLINT       </code></td>
<td><code dir="ltr" translate="no">         INT64       </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         BYTEINT       </code></td>
<td><code dir="ltr" translate="no">         INT64       </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         BIGINT       </code></td>
<td><code dir="ltr" translate="no">         INT64       </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         DECIMAL       </code></td>
<td><p><code dir="ltr" translate="no">          NUMERIC, DECIMAL        </code></p>
<p><code dir="ltr" translate="no">          BIGNUMERIC, BIGDECIMAL        </code></p></td>
<td><p>Use BigQuery's <code dir="ltr" translate="no">        NUMERIC       </code> (alias <code dir="ltr" translate="no">        DECIMAL       </code> ) when the scale (digits after the decimal point) &lt;= 9.<br />
Use BigQuery's <code dir="ltr" translate="no">        BIGNUMERIC       </code> (alias <code dir="ltr" translate="no">        BIGDECIMAL       </code> ) when the scale &gt; 9.</p>
<p>Use BigQuery's <a href="/bigquery/docs/reference/standard-sql/data-types#parameterized_decimal_type">parameterized</a> decimal data types if you need to enforce custom digit or scale bounds (constraints).</p>
<p>Teradata allows you to insert values of higher precision by rounding the stored value; however, it keeps the high precision in calculations. This can lead to <a href="https://docs.teradata.com/r/SQL-Data-Types-and-Literals/July-2021/Numeric-Data-Types/Rounding">unexpected rounding behavior</a> compared to the ANSI standard.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         FLOAT       </code></td>
<td><code dir="ltr" translate="no">         FLOAT64       </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         NUMERIC       </code></td>
<td><p><code dir="ltr" translate="no">          NUMERIC, DECIMAL        </code></p>
<p><code dir="ltr" translate="no">          BIGNUMERIC, BIGDECIMAL        </code></p></td>
<td><p>Use BigQuery's <code dir="ltr" translate="no">        NUMERIC       </code> (alias <code dir="ltr" translate="no">        DECIMAL       </code> ) when the scale (digits after the decimal point) &lt;= 9.<br />
Use BigQuery's <code dir="ltr" translate="no">        BIGNUMERIC       </code> (alias <code dir="ltr" translate="no">        BIGDECIMAL       </code> ) when the scale &gt; 9.</p>
<p>Use BigQuery's <a href="/bigquery/docs/reference/standard-sql/data-types#parameterized_decimal_type">parameterized</a> decimal data types if you need to enforce custom digit or scale bounds (constraints).</p>
<p>Teradata allows you to insert values of higher precision by rounding the stored value; however, it keeps the high precision in calculations. This can lead to <a href="https://docs.teradata.com/r/SQL-Data-Types-and-Literals/July-2021/Numeric-Data-Types/Rounding">unexpected rounding behavior</a> compared to the ANSI standard.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         NUMBER       </code></td>
<td><p><code dir="ltr" translate="no">          NUMERIC, DECIMAL        </code></p>
<p><code dir="ltr" translate="no">          BIGNUMERIC, BIGDECIMAL        </code></p></td>
<td><p>Use BigQuery's <code dir="ltr" translate="no">        NUMERIC       </code> (alias <code dir="ltr" translate="no">        DECIMAL       </code> ) when the scale (digits after the decimal point) &lt;= 9.<br />
Use BigQuery's <code dir="ltr" translate="no">        BIGNUMERIC       </code> (alias <code dir="ltr" translate="no">        BIGDECIMAL       </code> ) when the scale &gt; 9.</p>
<p>Use BigQuery's <a href="/bigquery/docs/reference/standard-sql/data-types#parameterized_decimal_type">parameterized</a> decimal data types if you need to enforce custom digit or scale bounds (constraints).</p>
<p>Teradata allows you to insert values of higher precision by rounding the stored value; however, it keeps the high precision in calculations. This can lead to <a href="https://docs.teradata.com/r/SQL-Data-Types-and-Literals/July-2021/Numeric-Data-Types/Rounding">unexpected rounding behavior</a> compared to the ANSI standard.</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         REAL       </code></td>
<td><code dir="ltr" translate="no">         FLOAT64       </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         CHAR/CHARACTER       </code></td>
<td><code dir="ltr" translate="no">         STRING       </code></td>
<td><p>Use BigQuery's <a href="/bigquery/docs/reference/standard-sql/data-types#parameterized_string_type">parameterized</a> <code dir="ltr" translate="no">        STRING       </code> data type if you need to enforce a maximum character length.</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         VARCHAR       </code></td>
<td><code dir="ltr" translate="no">         STRING       </code></td>
<td><p>Use BigQuery's <a href="/bigquery/docs/reference/standard-sql/data-types#parameterized_string_type">parameterized</a> <code dir="ltr" translate="no">        STRING       </code> data type if you need to enforce a maximum character length.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         CLOB       </code></td>
<td><code dir="ltr" translate="no">         STRING       </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         JSON       </code></td>
<td><code dir="ltr" translate="no">         JSON       </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         BLOB       </code></td>
<td><code dir="ltr" translate="no">         BYTES       </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         BYTE       </code></td>
<td><code dir="ltr" translate="no">         BYTES       </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         VARBYTE       </code></td>
<td><code dir="ltr" translate="no">         BYTES       </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         DATE       </code></td>
<td><code dir="ltr" translate="no">         DATE       </code></td>
<td>BigQuery does not support custom formatting similar to what Teradata with DataForm in SDF supports.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         TIME       </code></td>
<td><code dir="ltr" translate="no">         TIME       </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         TIME WITH TIME ZONE       </code></td>
<td><code dir="ltr" translate="no">         TIME       </code></td>
<td>Teradata stores the <code dir="ltr" translate="no">       TIME      </code> data type in UTC and allows you to pass an offset from UTC using the <code dir="ltr" translate="no">       WITH TIME ZONE      </code> syntax. <code dir="ltr" translate="no"></code> The <code dir="ltr" translate="no">       TIME      </code> data type in BigQuery represents a time that's independent of any date or time zone.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         TIMESTAMP       </code></td>
<td><code dir="ltr" translate="no">         TIMESTAMP       </code></td>
<td>Both Teradata and BigQuery <code dir="ltr" translate="no">         TIMESTAMP       </code> data types have microsecond precision (but Teradata supports leap seconds, while BigQuery does not).<br />
<br />
Both Teradata and BigQuery data types are usually associated with a UTC time zone ( <a href="/bigquery/docs/reference/standard-sql/data-types#time_zones">details</a> ).</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         TIMESTAMP WITH TIME ZONE       </code></td>
<td><code dir="ltr" translate="no">         TIMESTAMP       </code></td>
<td>The Teradata <code dir="ltr" translate="no">       TIMESTAMP      </code> can be set to a different time zone system-wide, per user or per column (using <code dir="ltr" translate="no">         WITH TIME ZONE       </code> ).<br />
<br />
The BigQuery <code dir="ltr" translate="no">       TIMESTAMP      </code> type assumes UTC if you don't explicitly specify a time zone. Make sure you either export time zone information correctly (do not concatenate a <code dir="ltr" translate="no">       DATE      </code> and <code dir="ltr" translate="no">       TIME      </code> value without time zone information) so that BigQuery can convert it on import. Or make sure that you convert time zone information to UTC before exporting.<br />
<br />
BigQuery has <code dir="ltr" translate="no">       DATETIME      </code> for an abstraction between civil time, which does not show a timezone when it is output, and <code dir="ltr" translate="no">       TIMESTAMP      </code> , which is a precise point in time that always shows the UTC timezone.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         ARRAY       </code></td>
<td><code dir="ltr" translate="no">         ARRAY       </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         MULTI-DIMENSIONAL ARRAY       </code></td>
<td><code dir="ltr" translate="no">         ARRAY       </code></td>
<td>In BigQuery, use an array of structs, with each struct containing a field of type <code dir="ltr" translate="no">       ARRAY      </code> (For details, see the BigQuery <a href="/bigquery/docs/arrays#building_arrays_of_arrays">documentation</a> ).</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         INTERVAL HOUR       </code></td>
<td><code dir="ltr" translate="no">         INT64       </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         INTERVAL MINUTE       </code></td>
<td><code dir="ltr" translate="no">         INT64       </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         INTERVAL SECOND       </code></td>
<td><code dir="ltr" translate="no">         INT64       </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         INTERVAL DAY       </code></td>
<td><code dir="ltr" translate="no">         INT64       </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         INTERVAL MONTH       </code></td>
<td><code dir="ltr" translate="no">         INT64       </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         INTERVAL YEAR       </code></td>
<td><code dir="ltr" translate="no">         INT64       </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         PERIOD(DATE)       </code></td>
<td><code dir="ltr" translate="no">         DATE       </code> , <code dir="ltr" translate="no">         DATE       </code></td>
<td><code dir="ltr" translate="no">       PERIOD(DATE)      </code> should be converted to two <code dir="ltr" translate="no">       DATE      </code> columns containing the start date and end date so that they can be used with window functions.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         PERIOD(TIMESTAMP WITH TIME ZONE)       </code></td>
<td><code dir="ltr" translate="no">         TIMESTAMP       </code> , <code dir="ltr" translate="no">         TIMESTAMP       </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         PERIOD(TIMESTAMP)       </code></td>
<td><code dir="ltr" translate="no">         TIMESTAMP       </code> , <code dir="ltr" translate="no">         TIMESTAMP       </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         PERIOD(TIME)       </code></td>
<td><code dir="ltr" translate="no">         TIME       </code> , <code dir="ltr" translate="no">         TIME       </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         PERIOD(TIME WITH TIME ZONE)       </code></td>
<td><code dir="ltr" translate="no">         TIME       </code> , <code dir="ltr" translate="no">         TIME       </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         UDT       </code></td>
<td><code dir="ltr" translate="no">         STRING       </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         XML       </code></td>
<td><code dir="ltr" translate="no">         STRING       </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         TD_ANYTYPE       </code></td>
<td><code dir="ltr" translate="no">         STRING       </code></td>
<td></td>
</tr>
</tbody>
</table>

For more information on type casting, see the next section.

### Teradata type formatting

Teradata SQL uses a set of default formats for displaying expressions and column data, and for conversions between data types. For example, a `  PERIOD(DATE)  ` data type in `  INTEGERDATE  ` mode is formatted as `  YY/MM/DD  ` by default. We suggest that you use ANSIDATE mode whenever possible to ensure ANSI SQL compliance, and use this chance to clean up legacy formats.

Teradata allows automatic application of custom formats using the `  FORMAT  ` clause, without changing the underlying storage, either as a data type attribute when you create a table using DDL, or in a derived expression. For example, a `  FORMAT  ` specification `  9.99  ` rounds any `  FLOAT  ` value to two digits. In BigQuery, this functionality has to be converted by using the `  ROUND()  ` function.

This functionality requires handling of intricate edge cases. For instance, when the `  FORMAT  ` clause is applied to a `  NUMERIC  ` column, you must take into [account special rounding and formatting rules](https://docs.teradata.com/r/SQL-Data-Types-and-Literals/July-2021/Data-Type-Formats-and-Format-Phrases/FORMAT-Phrase-and-NUMERIC-Formats) . A `  FORMAT  ` clause can be used to implicitly cast an `  INTEGER  ` epoch value to a `  DATE  ` format. Or a `  FORMAT  ` specification `  X(6)  ` on a `  VARCHAR  ` column truncates the column value, and you have to therefore convert to a `  SUBSTR()  ` function. This behavior is not ANSI SQL compliant. Therefore, we suggest not migrating column formats to BigQuery.

If column formats are absolutely required, use [Views](/bigquery/docs/views) or [user-defined functions (UDFs)](/bigquery/docs/user-defined-functions) .

For information about the default formats that Teradata SQL uses for each data type, see the [Teradata default formatting](https://docs.teradata.com/r/SQL-Data-Types-and-Literals/July-2021/Data-Type-Formats-and-Format-Phrases/Data-Type-Default-Formats) documentation.

### Timestamp and date type formatting

The following table summarizes the differences in timestamp and date formatting elements between Teradata SQL and GoogleSQL.

**Note:** There are no parentheses in the Teradata formats, because the formats ( `  CURRENT_*  ` ) are keywords, not functions.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Teradata format</th>
<th>Teradata description</th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         CURRENT_TIMESTAMP                 CURRENT_TIME       </code></td>
<td><code dir="ltr" translate="no">       TIME      </code> and <code dir="ltr" translate="no">       TIMESTAMP      </code> information in Teradata can have different time zone information, which is defined using <code dir="ltr" translate="no">       WITH   TIME ZONE      </code> .</td>
<td>If possible, use <code dir="ltr" translate="no">       CURRENT_TIMESTAMP()      </code> , which is formatted in ISO format. However, the output format does always show the UTC timezone. (Internally, BigQuery does not have a timezone.)<br />
<br />
Note the following details on differences in the ISO format.<br />
<br />
<code dir="ltr" translate="no">       DATETIME      </code> is formatted based on output channel conventions. In the BigQuery command-line tool and BigQuery console, it's formatted using a <code dir="ltr" translate="no">       T      </code> separator according to RFC 3339. However, in Python and Java JDBC, a space is used as a separator.<br />
<br />
If you want to use an explicit format, use <code dir="ltr" translate="no">         FORMAT_DATETIME()       </code> , which makes an explicit cast a string. For example, the following expression always returns a space separator:<br />
<br />
<code dir="ltr" translate="no">       CAST(CURRENT_DATETIME() AS STRING)      </code><br />
<br />
Teradata supports a <code dir="ltr" translate="no">       DEFAULT      </code> keyword in <code dir="ltr" translate="no">       TIME      </code> columns to set the current time (timestamp); this is not used in BigQuery.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         CURRENT_DATE       </code></td>
<td>Dates are stored in Teradata as <code dir="ltr" translate="no">       INT64      </code> values using the following formula:<br />
<br />
<code dir="ltr" translate="no">       (YEAR - 1900) * 10000 + (MONTH * 100) + DAY      </code><br />
<br />
Dates can be formatted as integers.</td>
<td>BigQuery has a separate <code dir="ltr" translate="no">       DATE      </code> format that always returns a date in ISO 8601 format.<br />
<br />
<code dir="ltr" translate="no">       DATE_FROM_UNIX_DATE      </code> can't be used, because it is 1970-based.<br />
<br />
Teradata supports a <code dir="ltr" translate="no">       DEFAULT      </code> keyword in <code dir="ltr" translate="no">       DATE      </code> columns to set the current date; this is not used in BigQuery.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         CURRENT_DATE-3       </code></td>
<td>Date values are represented as integers. Teradata supports arithmetic operators for date types.</td>
<td>For date types, use <code dir="ltr" translate="no">         DATE_ADD()       </code> or <code dir="ltr" translate="no">         DATE_SUB()       </code> .<br />
<br />
BigQuery uses arithmetic operators for data types: <code dir="ltr" translate="no">       INT64      </code> , <code dir="ltr" translate="no">       NUMERIC      </code> , and <code dir="ltr" translate="no">       FLOAT64      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         SYS_CALENDAR.CALENDAR       </code></td>
<td>Teradata provides a view for calendar operations to go beyond integer operations.</td>
<td>Not used in BigQuery.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         SET SESSION DATEFORM=ANSIDATE       </code></td>
<td>Set the session or system date format to ANSI (ISO 8601).</td>
<td>BigQuery always uses ISO 8601, so make sure you convert Teradata dates and times.</td>
</tr>
</tbody>
</table>

## Query syntax

This section addresses differences in query syntax between Teradata and BigQuery.

### `     SELECT    ` statement

Most Teradata [`  SELECT  ` statements](https://docs.teradata.com/r/SQL-Data-Manipulation-Language/July-2021/SELECT-Statements) are compatible with BigQuery. The following table contains a list of minor differences.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Teradata</th>
<th></th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         SEL       </code></td>
<td></td>
<td>Convert to <code dir="ltr" translate="no">       SELECT      </code> . BigQuery does not use the <code dir="ltr" translate="no">       SEL      </code> abbreviation.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         SELECT               (               subquery              ) AS flag,              CASE WHEN flag = 1 THEN ...       </code></td>
<td></td>
<td>In BigQuery, columns cannot reference the output of other columns defined within the same select list. Prefer moving a subquery into a <code dir="ltr" translate="no">       WITH      </code> clause.<br />
<br />
<code dir="ltr" translate="no">       WITH flags AS (                subquery               ),              SELECT              CASE WHEN flags.flag = 1 THEN ...       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         SELECT              * FROM               table               WHERE A LIKE ANY ('               string1              ', '               string2              ')       </code></td>
<td></td>
<td>BigQuery does not use the <code dir="ltr" translate="no">       ANY      </code> logical predicate.<br />
<br />
The same functionality can be achieved using multiple <code dir="ltr" translate="no">       OR      </code> operators:<br />
<br />
<code dir="ltr" translate="no">       SELECT * FROM               table               WHERE col LIKE '               string1              ' OR              col LIKE '               string2              '      </code><br />
<br />
In this case, string comparison also differs. See <a href="#comparison_operators">Comparison operators</a> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         SELECT              TOP 10 * FROM               table       </code></td>
<td></td>
<td>BigQuery uses <code dir="ltr" translate="no">       LIMIT      </code> at the end of a query instead of <code dir="ltr" translate="no">       TOP               n       </code> following the <code dir="ltr" translate="no">       SELECT      </code> keyword.</td>
</tr>
</tbody>
</table>

### Comparison operators

The following table shows Teradata comparison operators that are specific to Teradata and must be converted to the ANSI SQL:2011 compliant operators used in BigQuery.

For information about operators in BigQuery, see the [Operators](/bigquery/docs/reference/standard-sql/operators) section of the BigQuery documentation.

<table style="width:50%;">
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 0%" />
</colgroup>
<thead>
<tr class="header">
<th>Teradata</th>
<th>BigQuery</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         exp              EQ               exp2       </code><br />
<code dir="ltr" translate="no">         exp              IN               (exp2, exp3)       </code></td>
<td><code dir="ltr" translate="no">         exp              =               exp2       </code><br />
<code dir="ltr" translate="no">         exp              IN               (exp2, exp3)       </code><br />
<br />
To keep non-ANSI semantics for <code dir="ltr" translate="no">       NOT CASESPECIFIC      </code> , you can use<br />
<code dir="ltr" translate="no">       RTRIM(UPPER(               exp              )) = RTRIM(UPPER(               exp2              ))      </code></td>
<td>When comparing strings for equality, Teradata <em>might</em> ignore trailing whitespaces, while BigQuery considers them part of the string. For example, <code dir="ltr" translate="no">       'xyz'=' xyz'      </code> is <code dir="ltr" translate="no">       TRUE      </code> in Teradata but <code dir="ltr" translate="no">       FALSE      </code> in BigQuery.<br />
<br />
Teradata also provides a <code dir="ltr" translate="no">         NOT CASESPECIFIC       </code> column attribute that instructs Teradata to ignore case when comparing two strings. BigQuery is always case specific when comparing strings. For example, <code dir="ltr" translate="no">       'xYz' = 'xyz'      </code> is <code dir="ltr" translate="no">       TRUE      </code> in Teradata but <code dir="ltr" translate="no">       FALSE      </code> in BigQuery.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         exp              LE                 exp2         </code></td>
<td><code dir="ltr" translate="no">         exp              &lt;=               exp2       </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         exp              LT               exp2       </code></td>
<td><code dir="ltr" translate="no">         exp              &lt;               exp2       </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         exp              NE               exp2       </code></td>
<td><code dir="ltr" translate="no">         exp              &lt;&gt;               exp2                 exp              !=               exp2       </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         exp              GE               exp2       </code></td>
<td><code dir="ltr" translate="no">         exp              &gt;=               exp2       </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         exp              GT               exp2       </code></td>
<td><code dir="ltr" translate="no">         exp              &gt;               exp2       </code></td>
<td></td>
</tr>
</tbody>
</table>

### `     JOIN    ` conditions

BigQuery and Teradata support the same `  JOIN  ` , `  ON  ` , and `  USING  ` conditions. The following table contains a list of minor differences.

<table style="width:50%;">
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 0%" />
</colgroup>
<thead>
<tr class="header">
<th>Teradata</th>
<th>BigQuery</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       FROM               A              JOIN               B              ON               A.date              &gt;               B.start_date              AND               A.date              &lt;               B.end_date       </code></td>
<td><code dir="ltr" translate="no">       FROM               A              LEFT OUTER JOIN               B              ON               A.date              &gt;               B.start_date              AND               A.date              &lt;               B.end_date       </code></td>
<td>BigQuery supports inequality <code dir="ltr" translate="no">       JOIN      </code> clauses for all inner joins or if at least one equality condition is given (=). But not just one inequality condition (= and &lt;) in an <code dir="ltr" translate="no">       OUTER JOIN      </code> . Such constructs are sometimes used to query date or integer ranges. BigQuery prevents users from inadvertently creating large cross joins.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       FROM               A              ,               B              ON               A.id              =               B.id       </code></td>
<td><code dir="ltr" translate="no">       FROM               A              JOIN               B              ON               A.id              =               B.id       </code></td>
<td>Using a comma between tables in Teradata is equal to an <code dir="ltr" translate="no">       INNER JOIN      </code> , while in BigQuery it equals a <code dir="ltr" translate="no">       CROSS JOIN      </code> (Cartesian product). Because the comma in BigQuery <a href="/bigquery/docs/reference/standard-sql/migrating-from-legacy-sql#comma_operator_with_tables">legacy SQL is treated as <code dir="ltr" translate="no">        UNION       </code></a> , we recommend making the operation explicit to avoid confusion.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       FROM               A              JOIN               B              ON  (COALESCE(               A.id              , 0) = COALESCE(               B.id              , 0))      </code></td>
<td><code dir="ltr" translate="no">       FROM               A              JOIN               B              ON  (COALESCE(               A.id              , 0) = COALESCE(               B.id              , 0))      </code></td>
<td>No difference for scalar (constant) functions.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       FROM               A              JOIN               B              ON               A.id              = (SELECT MAX(               B.id              ) FROM               B              )      </code></td>
<td><code dir="ltr" translate="no">       FROM               A              JOIN (SELECT MAX(               B.id              ) FROM               B              )               B1              ON               A.id              =               B1.id       </code></td>
<td>BigQuery prevents users from using subqueries, correlated subqueries, or aggregations in join predicates. This lets BigQuery parallelize queries.</td>
</tr>
</tbody>
</table>

### Type conversion and casting

BigQuery has fewer but wider data types than Teradata, which requires BigQuery to be stricter in casting.

<table style="width:50%;">
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 0%" />
</colgroup>
<thead>
<tr class="header">
<th>Teradata</th>
<th>BigQuery</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         exp              EQ               exp2       </code><br />
<code dir="ltr" translate="no">         exp              IN               (exp2, exp3)       </code></td>
<td><code dir="ltr" translate="no">         exp              =               exp2       </code><br />
<code dir="ltr" translate="no">         exp              IN               (exp2, exp3)       </code><br />
<br />
To keep non-ANSI semantics for <code dir="ltr" translate="no">       NOT CASESPECIFIC      </code> , you can use<br />
<code dir="ltr" translate="no">       RTRIM(UPPER(               exp              )) = RTRIM(UPPER(               exp2              ))      </code></td>
<td>When comparing strings for equality, Teradata <em>might</em> ignore trailing whitespaces, while BigQuery considers them part of the string. For example, <code dir="ltr" translate="no">       'xyz'=' xyz'      </code> is <code dir="ltr" translate="no">       TRUE      </code> in Teradata but <code dir="ltr" translate="no">       FALSE      </code> in BigQuery.<br />
<br />
Teradata also provides a <code dir="ltr" translate="no">         NOT CASESPECIFIC       </code> column attribute that instructs Teradata to ignore case when comparing two strings. BigQuery is always case specific when comparing strings. For example, <code dir="ltr" translate="no">       'xYz' = 'xyz'      </code> is <code dir="ltr" translate="no">       TRUE      </code> in Teradata but <code dir="ltr" translate="no">       FALSE      </code> in BigQuery.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       CAST(               long_varchar_column              AS CHAR(6))      </code></td>
<td><code dir="ltr" translate="no">       LPAD(               long_varchar_column              , 6)      </code></td>
<td>Casting a character column in Teradata is sometimes used as a non-standard and non-optimal way to create a padded substring.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       CAST(92617 AS TIME) 92617 (FORMAT '99:99:99')      </code></td>
<td><code dir="ltr" translate="no">       PARSE_TIME("%k%M%S", CAST(92617 AS STRING))      </code><br />
</td>
<td>Teradata performs many <a href="https://docs.teradata.com/r/SQL-Data-Types-and-Literals/July-2021/Data-Type-Conversions/Implicit-Type-Conversions">more implicit type conversions</a> and rounding than BigQuery, which is generally stricter and enforces ANSI standards.<br />
(This example returns 09:26:17)</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       CAST(48.5 (FORMAT 'zz') AS FLOAT)      </code></td>
<td><code dir="ltr" translate="no">       CAST(SUBSTR(CAST(48.5 AS STRING), 0, 2) AS FLOAT64)      </code><br />
</td>
<td>Floating point and numeric data types can require special <a href="https://docs.teradata.com/r/SQL-Data-Types-and-Literals/July-2021/Numeric-Data-Types/Rounding">rounding rules</a> when applied with formats such as currencies.<br />
(This example returns 48)</td>
</tr>
</tbody>
</table>

#### Cast `     FLOAT    ` / `     DECIMAL    ` to `     INT    `

Where Teradata uses Gaussian and Banker algorithms to round numerics, use the [`  ROUND_HALF_EVEN  ` `  RoundingMode  `](/bigquery/docs/reference/rest/v2/RoundingMode) in BigQuery:

``` text
round(CAST(2.5 as Numeric),0, 'ROUND_HALF_EVEN')
```

#### Cast `     STRING    ` to `     NUMERIC    ` or `     BIGNUMERIC    `

When converting from `  STRING  ` to numeric values, use the correct data type, either `  NUMERIC  ` or `  BIGNUMERIC  ` , based on the number of decimal places in your `  STRING  ` value.

For more information about the supported numeric precision and scale in BigQuery, see [Decimal types](/bigquery/docs/reference/standard-sql/data-types#decimal_types) .

See also [Comparison operators](#comparison_operators) and [column formats](#type_formatting) . Both comparisons and column formatting can behave like type casts.

### `     QUALIFY    ` , `     ROWS    ` clauses

The `  QUALIFY  ` clause in Teradata allows you to [filter results for window functions](https://docs.teradata.com/reader/2_MC9vCtAJRlKle2Rpb0mA/19NnI91neorAi7LX6SJXBw) . Alternatively, a [`  ROWS  ` phrase](https://docs.teradata.com/r/SQL-Functions-Expressions-and-Predicates/July-2021/Ordered-Analytical/Window-Aggregate-Functions/The-Window-Feature/ROWS-Phrase) can be used for the same task. These work similar to a `  HAVING  ` condition for a `  GROUP  ` clause, limiting the output of what in BigQuery are called [window functions](/bigquery/docs/reference/standard-sql/window-function-calls) .

<table style="width:40%;">
<colgroup>
<col style="width: 40%" />
<col style="width: 0%" />
</colgroup>
<thead>
<tr class="header">
<th>Teradata</th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       SELECT               col1              ,               col2               FROM               table               QUALIFY ROW_NUMBER() OVER (PARTITION BY               col1              ORDER BY               col2              ) = 1;      </code></td>
<td>The Teradata <code dir="ltr" translate="no">       QUALIFY      </code> clause with a window function like <code dir="ltr" translate="no">       ROW_NUMBER()      </code> , <code dir="ltr" translate="no">       SUM()      </code> , <code dir="ltr" translate="no">       COUNT()      </code> and with <code dir="ltr" translate="no">       OVER PARTITION BY      </code> is expressed in BigQuery as a <code dir="ltr" translate="no">       WHERE      </code> clause on a subquery that contains an analytics value.<br />
<br />
Using <code dir="ltr" translate="no">       ROW_NUMBER()      </code> :<br />
<br />
<code dir="ltr" translate="no">       SELECT               col1              ,               col2               FROM (              SELECT               col1              ,               col2              ,              ROW_NUMBER() OVER (PARTITION BY               col1              ORDER BY               col2              ) RN              FROM               table               ) WHERE RN = 1;      </code><br />
<br />
Using <code dir="ltr" translate="no">       ARRAY_AGG      </code> , which supports larger partitions:<br />
<br />
<code dir="ltr" translate="no">       SELECT                result              .*              FROM (              SELECT              ARRAY_AGG(               table              ORDER BY               table              .               col2               DESC LIMIT 1)[OFFSET(0)]              FROM               table               GROUP BY               col1               ) AS               result              ;      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       SELECT               col1              ,               col2               FROM               table               AVG(               col1              ) OVER (PARTITION BY               col1              ORDER BY               col2              ROWS BETWEEN 2 PRECEDING AND CURRENT ROW);      </code></td>
<td><code dir="ltr" translate="no">       SELECT               col1              ,               col2               FROM               table               AVG(               col1              ) OVER (PARTITION BY               col1              ORDER BY               col2              RANGE BETWEEN 2 PRECEDING AND CURRENT ROW);      </code><br />
<br />
In BigQuery, both <code dir="ltr" translate="no">       RANGE      </code> and <code dir="ltr" translate="no">       ROWS      </code> can be used in the window frame clause. However, window clauses can only be used with window functions like <code dir="ltr" translate="no">       AVG()      </code> , not with numbering functions like <code dir="ltr" translate="no">       ROW_NUMBER()      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       SELECT               col1              ,               col2               FROM               table               QUALIFY ROW_NUMBER() OVER (PARTITION BY               col1              ORDER BY               col2              ) = 1;      </code></td>
<td><code dir="ltr" translate="no">       SELECT               col1              ,                col2              FROM                Dataset-name              .table              QUALIFY row_number() OVER (PARTITION BY upper(               a.col1              ) ORDER BY upper(               a.col2              )) = 1      </code></td>
</tr>
</tbody>
</table>

### `     NORMALIZE    ` keyword

Teradata provides the [`  NORMALIZE  `](https://docs.teradata.com/r/Enterprise_IntelliFlex_VMware/SQL-Data-Definition-Language-Syntax-and-Examples/Table-Statements/ALTER-TABLE/ALTER-TABLE-Syntax-Elements/ALTER-TABLE-Syntax-Elements-Basic/ALTER-TABLE-Basic-Options/NORMALIZE) keyword for `  SELECT  ` clauses to coalesce overlapping periods or intervals into a single period or interval that encompasses all individual period values.

BigQuery does not support the `  PERIOD  ` type, so any `  PERIOD  ` type column in Teradata has to be inserted into BigQuery as two separate `  DATE  ` or `  DATETIME  ` fields that correspond to the start and end of the period.

<table>
<thead>
<tr class="header">
<th>Teradata</th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       SELECT NORMALIZE              client_id,              item_sid,              BEGIN(               period              ) AS min_date,              END(               period              ) AS max_date,              FROM                table              ;       </code></td>
<td><code dir="ltr" translate="no">       SELECT              t.client_id,              t.item_sid,              t.min_date,              MAX(t.dwh_valid_to) AS max_date              FROM (              SELECT              d1.client_id,              d1.item_sid,              d1.dwh_valid_to AS dwh_valid_to,              MIN(d2.dwh_valid_from) AS min_date              FROM                table              d1              LEFT JOIN                table              d2              ON              d1.client_id = d2.client_id              AND d1.item_sid = d2.item_sid              AND d1.dwh_valid_to &gt;= d2.dwh_valid_from              AND d1.dwh_valid_from &lt; = d2.dwh_valid_to              GROUP BY              d1.client_id,              d1.item_sid,              d1.dwh_valid_to ) t              GROUP BY              t.client_id,              t.item_sid,              t.min_date;      </code></td>
</tr>
</tbody>
</table>

## Functions

The following sections list mappings between Teradata functions and BigQuery equivalents.

### Aggregate functions

The following table maps common Teradata aggregate, statistical aggregate, and approximate aggregate functions to their BigQuery equivalents. BigQuery offers the following additional aggregate functions:

  - [`  ANY_VALUE  `](/bigquery/docs/reference/standard-sql/aggregate_functions#any_value)
  - [`  APPROX_COUNT_DISTINCT  `](/bigquery/docs/reference/standard-sql/approximate_aggregate_functions#approx_count_distinct)
  - [`  APPROX_QUANTILES  `](/bigquery/docs/reference/standard-sql/approximate_aggregate_functions#approx_quantiles)
  - [`  APPROX_TOP_COUNT  `](/bigquery/docs/reference/standard-sql/approximate_aggregate_functions#approx_top_count)
  - [`  APPROX_TOP_SUM  `](/bigquery/docs/reference/standard-sql/approximate_aggregate_functions#approx_top_sum)
  - [`  COUNTIF  `](/bigquery/docs/reference/standard-sql/aggregate_functions#countif)
  - [`  LOGICAL_AND  `](/bigquery/docs/reference/standard-sql/aggregate_functions#logical_and)
  - [`  LOGICAL_OR  `](/bigquery/docs/reference/standard-sql/aggregate_functions#logical_or)
  - [`  STRING_AGG  `](/bigquery/docs/reference/standard-sql/aggregate_functions#string_agg)

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Teradata</th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         AVG       </code></td>
<td><code dir="ltr" translate="no">         AVG       </code><br />
<strong>Note</strong> : BigQuery provides approximate results when calculating the average of <code dir="ltr" translate="no">       INT      </code> values.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         BITAND       </code></td>
<td><code dir="ltr" translate="no">         BIT_AND       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         BITNOT       </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/operators#bitwise_operators">Bitwise not operator</a> ( <code dir="ltr" translate="no">       ~      </code> )</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         BITOR       </code></td>
<td><code dir="ltr" translate="no">         BIT_OR       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         BITXOR       </code></td>
<td><code dir="ltr" translate="no">         BIT_XOR       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         CORR       </code></td>
<td><code dir="ltr" translate="no">         CORR       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         COUNT       </code></td>
<td><code dir="ltr" translate="no">         COUNT       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         COVAR_POP       </code></td>
<td><code dir="ltr" translate="no">         COVAR_POP       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         COVAR_SAMP       </code></td>
<td><code dir="ltr" translate="no">         COVAR_SAMP       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         MAX       </code></td>
<td><code dir="ltr" translate="no">         MAX       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         MIN       </code></td>
<td><code dir="ltr" translate="no">         MIN       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         REGR_AVGX       </code></td>
<td><code dir="ltr" translate="no">         AVG              (              IF(               dep_var_expression              is NULL              OR               ind_var_expression              is NULL,              NULL,               ind_var_expression              )              )      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         REGR_AVGY       </code></td>
<td><code dir="ltr" translate="no">         AVG              (              IF(               dep_var_expression              is NULL              OR               ind_var_expression              is NULL,              NULL,               dep_var_expression              )              )      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         REGR_COUNT       </code></td>
<td><code dir="ltr" translate="no">         SUM              (              IF(               dep_var_expression              is NULL              OR               ind_var_expression              is NULL,              NULL, 1)              )      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         REGR_INTERCEPT       </code></td>
<td><code dir="ltr" translate="no">         AVG              (               dep_var_expression              ) -               AVG              (               ind_var_expression              ) *     (               COVAR_SAMP              (               ind_var_expression              ,                dep_var_expression              )              /               VARIANCE              (               ind_var_expression              ))      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         REGR_R2       </code></td>
<td><code dir="ltr" translate="no">       (               COUNT              (               dep_var_expression              )*                SUM              (               ind_var_expression              *               dep_var_expression              ) -                SUM              (               dep_var_expression              ) *               SUM              (               ind_var_expression              ))              /               SQRT              (              (               COUNT              (               ind_var_expression              )*                SUM              (               POWER              (               ind_var_expression              , 2))*                POWER              (               SUM              (               ind_var_expression              ),2))*              (               COUNT              (               dep_var_expression              )*                SUM              (               POWER              (               dep_var_expression              , 2))*                POWER              (               SUM              (               dep_var_expression              ), 2)))      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         REGR_SLOPE       </code></td>
<td><code dir="ltr" translate="no">       -               COVAR_SAMP              (               ind_var_expression              ,                dep_var_expression              )              /               VARIANCE              (               ind_var_expression              )      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         REGR_SXX       </code></td>
<td><code dir="ltr" translate="no">         SUM              (               POWER              (               ind_var_expression              , 2)) -               COUNT              (               ind_var_expression              ) *                POWER              (               AVG              (               ind_var_expression              ),2)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         REGR_SXY       </code></td>
<td><code dir="ltr" translate="no">         SUM              (               ind_var_expression              *               dep_var_expression              ) -               COUNT              (               ind_var_expression              )              *               AVG              (               ind_var_expression              ) *               AVG              (               dep_var_expression              )      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         REGR_SYY       </code></td>
<td><code dir="ltr" translate="no">         SUM              (               POWER              (               dep_var_expression              , 2)) -               COUNT              (               dep_var_expression              )              *               POWER              (               AVG              (               dep_var_expression              ),2)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         SKEW       </code></td>
<td>Custom user-defined function.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         STDDEV_POP       </code></td>
<td><code dir="ltr" translate="no">         STDDEV_POP       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         STDDEV_SAMP       </code></td>
<td><code dir="ltr" translate="no">         STDDEV_SAMP              ,               STDDEV       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         SUM       </code></td>
<td><code dir="ltr" translate="no">         SUM       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         VAR_POP       </code></td>
<td><code dir="ltr" translate="no">         VAR_POP       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         VAR_SAMP       </code></td>
<td><code dir="ltr" translate="no">         VAR_SAMP              ,               VARIANCE       </code></td>
</tr>
</tbody>
</table>

### Analytical functions and window functions

The following table maps common Teradata analytic and aggregate analytic functions to their BigQuery window function equivalents. BigQuery offers the following additional functions:

  - [`  ANY_VALUE  `](/bigquery/docs/reference/standard-sql/aggregate_functions#any_value)
  - [`  AVG  `](/bigquery/docs/reference/standard-sql/aggregate_functions#avg)
  - [`  COUNTIF  `](/bigquery/docs/reference/standard-sql/aggregate_functions#countif)
  - [`  LAG  `](/bigquery/docs/reference/standard-sql/navigation_functions#lag)
  - [`  LEAD  `](/bigquery/docs/reference/standard-sql/navigation_functions#lead)
  - [`  LOGICAL_AND  `](/bigquery/docs/reference/standard-sql/aggregate_functions#logical_and)
  - [`  LOGICAL_OR  `](/bigquery/docs/reference/standard-sql/aggregate_functions#logical_or)
  - [`  NTH_VALUE  `](/bigquery/docs/reference/standard-sql/navigation_functions#nth_value)
  - [`  NTILE  `](/bigquery/docs/reference/standard-sql/numbering_functions#ntile)
  - [`  STRING_AGG  `](/bigquery/docs/reference/standard-sql/aggregate_functions#string_agg)

<table style="width:45%;">
<colgroup>
<col style="width: 45%" />
<col style="width: 0%" />
</colgroup>
<thead>
<tr class="header">
<th>Teradata</th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         ARRAY_AGG       </code></td>
<td><code dir="ltr" translate="no">         ARRAY_AGG       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         ARRAY_CONCAT, (|| operator)       </code></td>
<td><code dir="ltr" translate="no">         ARRAY_CONCAT_AGG, (|| operator)       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         BITAND       </code></td>
<td><code dir="ltr" translate="no">         BIT_AND       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         BITNOT       </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/operators#bitwise_operators">Bitwise not operator</a> ( <code dir="ltr" translate="no">       ~      </code> )</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         BITOR       </code></td>
<td><code dir="ltr" translate="no">         BIT_OR       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         BITXOR       </code></td>
<td><code dir="ltr" translate="no">         BIT_XOR       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         CORR       </code></td>
<td><code dir="ltr" translate="no">         CORR       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         COUNT       </code></td>
<td><code dir="ltr" translate="no">         COUNT       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         COVAR_POP       </code></td>
<td><code dir="ltr" translate="no">         COVAR_POP       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         COVAR_SAMP       </code></td>
<td><code dir="ltr" translate="no">         COVAR_SAMP       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         CUME_DIST       </code></td>
<td><code dir="ltr" translate="no">         CUME_DIST       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         DENSE_RANK       </code> (ANSI)</td>
<td><code dir="ltr" translate="no">         DENSE_RANK       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         FIRST_VALUE       </code></td>
<td><code dir="ltr" translate="no">         FIRST_VALUE       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         LAST_VALUE       </code></td>
<td><code dir="ltr" translate="no">         LAST_VALUE       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         MAX       </code></td>
<td><code dir="ltr" translate="no">         MAX       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         MIN       </code></td>
<td><code dir="ltr" translate="no">         MIN       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         PERCENT_RANK       </code></td>
<td><code dir="ltr" translate="no">         PERCENT_RANK       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         PERCENTILE_CONT       </code> , <code dir="ltr" translate="no">         PERCENTILE_DISC       </code></td>
<td><code dir="ltr" translate="no">         PERCENTILE_CONT       </code> , <code dir="ltr" translate="no">         PERCENTILE_DISC       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         QUANTILE       </code></td>
<td><code dir="ltr" translate="no">         NTILE       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         RANK       </code> (ANSI)</td>
<td><code dir="ltr" translate="no">         RANK       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         ROW_NUMBER       </code></td>
<td><code dir="ltr" translate="no">         ROW_NUMBER       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         STDDEV_POP       </code></td>
<td><code dir="ltr" translate="no">         STDDEV_POP       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         STDDEV_SAMP       </code></td>
<td><code dir="ltr" translate="no">         STDDEV_SAMP              ,               STDDEV       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         SUM       </code></td>
<td><code dir="ltr" translate="no">         SUM       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         VAR_POP       </code></td>
<td><code dir="ltr" translate="no">         VAR_POP       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         VAR_SAMP       </code></td>
<td><code dir="ltr" translate="no">         VAR_SAMP              ,               VARIANCE       </code></td>
</tr>
</tbody>
</table>

### Date/time functions

The following table maps common Teradata date/time functions to their BigQuery equivalents. BigQuery offers the following additional date/time functions:

  - [`  CURRENT_DATETIME  `](/bigquery/docs/reference/standard-sql/datetime_functions#current_datetime)
  - [`  DATE_ADD  `](/bigquery/docs/reference/standard-sql/date_functions#date_add)
  - [`  DATE_DIFF  `](/bigquery/docs/reference/standard-sql/date_functions#date_diff)
  - [`  DATE_FROM_UNIX_DATE  `](/bigquery/docs/reference/standard-sql/date_functions#date_from_unix_date)
  - [`  DATE_SUB  `](/bigquery/docs/reference/standard-sql/date_functions#date_sub)
  - [`  DATE_TRUNC  `](/bigquery/docs/reference/standard-sql/date_functions#date_trunc)
  - [`  DATETIME  `](/bigquery/docs/reference/standard-sql/datetime_functions#datetime)
  - [`  DATETIME_ADD  `](/bigquery/docs/reference/standard-sql/datetime_functions#datetime_add)
  - [`  DATETIME_DIFF  `](/bigquery/docs/reference/standard-sql/datetime_functions#datetime_diff)
  - [`  DATETIME_SUB  `](/bigquery/docs/reference/standard-sql/datetime_functions#datetime_sub)
  - [`  DATETIME_TRUNC  `](/bigquery/docs/reference/standard-sql/datetime_functions#datetime_trunc)
  - [`  PARSE_DATE  `](/bigquery/docs/reference/standard-sql/date_functions#parse_date)
  - [`  PARSE_DATETIME  `](/bigquery/docs/reference/standard-sql/datetime_functions#parse_datetime)
  - [`  PARSE_TIME  `](/bigquery/docs/reference/standard-sql/time_functions#parse_time)
  - [`  PARSE_TIMESTAMP  `](/bigquery/docs/reference/standard-sql/timestamp_functions#parse_timestamp)
  - [`  STRING  `](/bigquery/docs/reference/standard-sql/string_functions)
  - [`  TIME  `](/bigquery/docs/reference/standard-sql/time_functions#time)
  - [`  TIME_ADD  `](/bigquery/docs/reference/standard-sql/time_functions#time_add)
  - [`  TIME_DIFF  `](/bigquery/docs/reference/standard-sql/time_functions#time_diff)
  - [`  TIME_SUB  `](/bigquery/docs/reference/standard-sql/time_functions#time_sub)
  - [`  TIME_TRUNC  `](/bigquery/docs/reference/standard-sql/time_functions#time_trunc)
  - [`  TIMESTAMP  `](/bigquery/docs/reference/standard-sql/timestamp_functions#timestamp)
  - [`  TIMESTAMP_ADD  `](/bigquery/docs/reference/standard-sql/timestamp_functions#timestamp_add)
  - [`  TIMESTAMP_DIFF  `](/bigquery/docs/reference/standard-sql/timestamp_functions#timestamp_diff)
  - [`  TIMESTAMP_MICROS  `](/bigquery/docs/reference/standard-sql/timestamp_functions#timestamp_micros)
  - [`  TIMESTAMP_MILLIS  `](/bigquery/docs/reference/standard-sql/timestamp_functions#timestamp_millis)
  - [`  TIMESTAMP_SECONDS  `](/bigquery/docs/reference/standard-sql/timestamp_functions#timestamp_seconds)
  - [`  TIMESTAMP_SUB  `](/bigquery/docs/reference/standard-sql/timestamp_functions#timestamp_sub)
  - [`  TIMESTAMP_TRUNC  `](/bigquery/docs/reference/standard-sql/timestamp_functions#timestamp_trunc)
  - [`  UNIX_DATE  `](/bigquery/docs/reference/standard-sql/date_functions#unix_date)
  - [`  UNIX_MICROS  `](/bigquery/docs/reference/standard-sql/timestamp_functions#unix_micros)
  - [`  UNIX_MILLIS  `](/bigquery/docs/reference/standard-sql/timestamp_functions#unix_millis)
  - [`  UNIX_SECONDS  `](/bigquery/docs/reference/standard-sql/timestamp_functions#unix_seconds)

<table>
<thead>
<tr class="header">
<th>Teradata</th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         ADD_MONTHS       </code></td>
<td><code dir="ltr" translate="no">         DATE_ADD              ,               TIMESTAMP_ADD       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         CURRENT_DATE       </code></td>
<td><code dir="ltr" translate="no">         CURRENT_DATE       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         CURRENT_TIME       </code></td>
<td><code dir="ltr" translate="no">         CURRENT_TIME       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         CURRENT_TIMESTAMP       </code></td>
<td><code dir="ltr" translate="no">         CURRENT_TIMESTAMP       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         DATE              + k      </code></td>
<td><code dir="ltr" translate="no">         DATE_ADD              (               date_expression              , INTERVAL               k              DAY)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         DATE              - k      </code></td>
<td><code dir="ltr" translate="no">         DATE_SUB              (               date_expression              , INTERVAL               k              DAY)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         EXTRACT       </code></td>
<td><code dir="ltr" translate="no">         EXTRACT              (DATE),               EXTRACT              (TIMESTAMP)      </code></td>
</tr>
<tr class="even">
<td></td>
<td><code dir="ltr" translate="no">         FORMAT_DATE       </code></td>
</tr>
<tr class="odd">
<td></td>
<td><code dir="ltr" translate="no">         FORMAT_DATETIME       </code></td>
</tr>
<tr class="even">
<td></td>
<td><code dir="ltr" translate="no">         FORMAT_TIME       </code></td>
</tr>
<tr class="odd">
<td></td>
<td><code dir="ltr" translate="no">         FORMAT_TIMESTAMP       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         LAST_DAY       </code></td>
<td><code dir="ltr" translate="no">         LAST_DAY       </code> <strong>Note</strong> : This function supports both <code dir="ltr" translate="no">       DATE      </code> and <code dir="ltr" translate="no">       DATETIME      </code> input expressions.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         MONTHS_BETWEEN       </code></td>
<td><code dir="ltr" translate="no">         DATE_DIFF              (               date_expression              ,               date_expression              , MONTH)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         NEXT_DAY       </code></td>
<td><code dir="ltr" translate="no">         DATE_ADD              (                DATE_TRUNC              (                date_expression              ,              WEEK(day_value)              ),              INTERVAL 1 WEEK              )      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         OADD_MONTHS       </code></td>
<td><code dir="ltr" translate="no">         DATE_SUB              (                DATE_TRUNC              (                DATE_ADD              (                date_expression              ,              INTERVAL               num_months              MONTH              ),              MONTH              ),              INTERVAL 1 DAY              )      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         td_day_of_month       </code></td>
<td><code dir="ltr" translate="no">         EXTRACT              (DAY FROM               date_expression              )                EXTRACT              (DAY FROM               timestamp_expression              )      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         td_day_of_week       </code></td>
<td><code dir="ltr" translate="no">         EXTRACT              (DAYOFWEEK FROM               date_expression              )                EXTRACT              (DAYOFWEEK FROM               timestamp_expression              )      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         td_day_of_year       </code></td>
<td><code dir="ltr" translate="no">         EXTRACT              (DAYOFYEAR FROM               date_expression              )                EXTRACT              (DAYOFYEAR FROM               timestamp_expression              )      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         td_friday       </code></td>
<td><code dir="ltr" translate="no">         DATE_TRUNC              (                date_expression              ,              WEEK(FRIDAY)              )      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         td_monday       </code></td>
<td><code dir="ltr" translate="no">         DATE_TRUNC              (                date_expression              ,              WEEK(MONDAY)              )      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         td_month_begin       </code></td>
<td><code dir="ltr" translate="no">         DATE_TRUNC              (               date_expression              , MONTH)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         td_month_end       </code></td>
<td><code dir="ltr" translate="no">         DATE_SUB              (                DATE_TRUNC              (                DATE_ADD              (                date_expression              ,              INTERVAL 1 MONTH              ),              MONTH              ),              INTERVAL 1 DAY              )      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         td_month_of_calendar       </code></td>
<td><code dir="ltr" translate="no">       (               EXTRACT              (YEAR FROM               date_expression              ) - 1900) * 12 +               EXTRACT              (MONTH FROM               date_expression              )      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         td_month_of_quarter       </code></td>
<td><code dir="ltr" translate="no">         EXTRACT              (MONTH FROM               date_expression              )              - ((               EXTRACT              (QUARTER FROM               date_expression              ) - 1) * 3)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         td_month_of_year       </code></td>
<td><code dir="ltr" translate="no">         EXTRACT              (MONTH FROM               date_expression              )                EXTRACT              (MONTH FROM               timestamp_expression              )      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         td_quarter_begin       </code></td>
<td><code dir="ltr" translate="no">         DATE_TRUNC              (               date_expression              , QUARTER)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         td_quarter_end       </code></td>
<td><code dir="ltr" translate="no">         DATE_SUB              (                DATE_TRUNC              (                DATE_ADD              (                date_expression              ,              INTERVAL 1 QUARTER              ),              QUARTER              ),              INTERVAL 1 DAY              )      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         td_quarter_of_calendar       </code></td>
<td><code dir="ltr" translate="no">       (               EXTRACT              (YEAR FROM               date_expression              )              - 1900) * 4              +               EXTRACT              (QUARTER FROM               date_expression              )      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         td_quarter_of_year       </code></td>
<td><code dir="ltr" translate="no">         EXTRACT              (QUARTER FROM               date_expression              )                EXTRACT              (QUARTER FROM               timestamp_expression              )      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         td_saturday       </code></td>
<td><code dir="ltr" translate="no">         DATE_TRUNC              (                date_expression              ,              WEEK(SATURDAY)              )      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         td_sunday       </code></td>
<td><code dir="ltr" translate="no">         DATE_TRUNC              (                date_expression              ,              WEEK(SUNDAY)              )      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         td_thursday       </code></td>
<td><code dir="ltr" translate="no">         DATE_TRUNC              (                date_expression              ,              WEEK(THURSDAY)              )      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         td_tuesday       </code></td>
<td><code dir="ltr" translate="no">         DATE_TRUNC              (                date_expression              ,              WEEK(TUESDAY)              )      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         td_wednesday       </code></td>
<td><code dir="ltr" translate="no">         DATE_TRUNC              (                date_expression              ,              WEEK(WEDNESDAY)              )      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         td_week_begin       </code></td>
<td><code dir="ltr" translate="no">         DATE_TRUNC              (               date_expression              , WEEK)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         td_week_end       </code></td>
<td><code dir="ltr" translate="no">         DATE_SUB              (                DATE_TRUNC              (                DATE_ADD              (                date_expression              ,              INTERVAL 1 WEEK              ),              WEEK              ),              INTERVAL 1 DAY              )      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         td_week_of_calendar       </code></td>
<td><code dir="ltr" translate="no">       (               EXTRACT              (YEAR FROM               date_expression              ) - 1900) * 52 +               EXTRACT              (WEEK FROM               date_expression              )      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         td_week_of_month       </code></td>
<td><code dir="ltr" translate="no">         EXTRACT              (WEEK FROM               date_expression              )              -               EXTRACT              (WEEK FROM               DATE_TRUNC              (               date_expression              , MONTH))      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         td_week_of_year       </code></td>
<td><code dir="ltr" translate="no">         EXTRACT              (WEEK FROM               date_expression              )                EXTRACT              (WEEK FROM               timestamp_expression              )      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         td_weekday_of_month       </code></td>
<td><code dir="ltr" translate="no">         CAST              (                CEIL              (                EXTRACT              (DAY FROM               date_expression              )              / 7              ) AS INT64              )      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         td_year_begin       </code></td>
<td><code dir="ltr" translate="no">         DATE_TRUNC              (               date_expression              , YEAR)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         td_year_end       </code></td>
<td><code dir="ltr" translate="no">         DATE_SUB              (                DATE_TRUNC              (                DATE_ADD              (                date_expression              ,              INTERVAL 1 YEAR              ),              YEAR              ),              INTERVAL 1 DAY              )      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         td_year_of_calendar       </code></td>
<td><code dir="ltr" translate="no">         EXTRACT              (YEAR FROM               date_expression              )      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         TO_DATE       </code></td>
<td><code dir="ltr" translate="no">         PARSE_DATE       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         TO_TIMESTAMP       </code></td>
<td><code dir="ltr" translate="no">         PARSE_TIMESTAMP       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         TO_TIMESTAMP_TZ       </code></td>
<td><code dir="ltr" translate="no">         PARSE_TIMESTAMP       </code></td>
</tr>
</tbody>
</table>

### String functions

The following table maps Teradata string functions to their BigQuery equivalents. BigQuery offers the following additional string functions:

  - [`  BYTE_LENGTH  `](/bigquery/docs/reference/standard-sql/string_functions#byte_length)
  - [`  CODE_POINTS_TO_BYTES  `](/bigquery/docs/reference/standard-sql/string_functions#code_points_to_bytes)
  - [`  ENDS_WITH  `](/bigquery/docs/reference/standard-sql/string_functions#ends_with)
  - [`  FROM_BASE32  `](/bigquery/docs/reference/standard-sql/string_functions#from_base32)
  - [`  FROM_BASE64  `](/bigquery/docs/reference/standard-sql/string_functions#from_base64)
  - [`  FROM_HEX  `](/bigquery/docs/reference/standard-sql/string_functions#from_hex)
  - [`  NORMALIZE  `](/bigquery/docs/reference/standard-sql/string_functions#normalize)
  - [`  NORMALIZE_AND_CASEFOLD  `](/bigquery/docs/reference/standard-sql/string_functions#normalize_and_casefold)
  - [`  REGEXP_CONTAINS  `](/bigquery/docs/reference/standard-sql/string_functions#regexp_contains)
  - [`  REGEXP_EXTRACT  `](/bigquery/docs/reference/standard-sql/string_functions#regexp_extract)
  - [`  REGEXP_EXTRACT_ALL  `](/bigquery/docs/reference/standard-sql/string_functions#regexp_extract_all)
  - [`  REPEAT  `](/bigquery/docs/reference/standard-sql/string_functions#repeat)
  - [`  REPLACE  `](/bigquery/docs/reference/standard-sql/string_functions#replace)
  - [`  SAFE_CONVERT_BYTES_TO_STRING  `](/bigquery/docs/reference/standard-sql/string_functions#safe_convert_bytes_to_string)
  - [`  SPLIT  `](/bigquery/docs/reference/standard-sql/string_functions#split)
  - [`  STARTS_WITH  `](/bigquery/docs/reference/standard-sql/string_functions#starts_with)
  - [`  STRPOS  `](/bigquery/docs/reference/standard-sql/string_functions#strpos)
  - [`  TO_BASE32  `](/bigquery/docs/reference/standard-sql/string_functions#to_base32)
  - [`  TO_BASE64  `](/bigquery/docs/reference/standard-sql/string_functions#to_base64)
  - [`  TO_CODE_POINTS  `](/bigquery/docs/reference/standard-sql/string_functions#to_code_points)
  - [`  TO_HEX  `](/bigquery/docs/reference/standard-sql/string_functions#to_hex)

<table style="width:38%;">
<colgroup>
<col style="width: 38%" />
<col style="width: 0%" />
</colgroup>
<thead>
<tr class="header">
<th>Teradata</th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         ASCII       </code></td>
<td><code dir="ltr" translate="no">         TO_CODE_POINTS              (               string_expression              )[               OFFSET              (0)]      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         CHAR2HEXINT       </code></td>
<td><code dir="ltr" translate="no">         TO_HEX       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         CHARACTER LENGTH       </code></td>
<td><code dir="ltr" translate="no">         CHAR_LENGTH       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         CHARACTER LENGTH       </code></td>
<td><code dir="ltr" translate="no">         CHARACTER_LENGTH       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         CHR       </code></td>
<td><code dir="ltr" translate="no">         CODE_POINTS_TO_STRING              (              [mod(               numeric_expression              , 256)]              )      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         CONCAT, (|| operator)       </code></td>
<td><code dir="ltr" translate="no">         CONCAT, (|| operator)       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         CSV       </code></td>
<td>Custom user-defined function.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         CSVLD       </code></td>
<td>Custom user-defined function.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         FORMAT       </code></td>
<td><code dir="ltr" translate="no">         FORMAT       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         INDEX       </code></td>
<td><code dir="ltr" translate="no">         STRPOS              (               string              ,               substring              )      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         INITCAP       </code></td>
<td><code dir="ltr" translate="no">         INITCAP       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         INSTR       </code></td>
<td>Custom user-defined function.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         LEFT       </code></td>
<td><code dir="ltr" translate="no">         SUBSTR              (               source_string              , 1,               length              )      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         LENGTH       </code></td>
<td><code dir="ltr" translate="no">         LENGTH       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         LOWER       </code></td>
<td><code dir="ltr" translate="no">         LOWER       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         LPAD       </code></td>
<td><code dir="ltr" translate="no">         LPAD       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         LTRIM       </code></td>
<td><code dir="ltr" translate="no">         LTRIM       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         NGRAM       </code></td>
<td>Custom user-defined function.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         NVP       </code></td>
<td>Custom user-defined function.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         OREPLACE       </code></td>
<td><code dir="ltr" translate="no">         REPLACE       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         OTRANSLATE       </code></td>
<td>Custom user-defined function.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         POSITION       </code></td>
<td><code dir="ltr" translate="no">         STRPOS              (               string              ,               substring              )      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         REGEXP_INSTR       </code></td>
<td><code dir="ltr" translate="no">         STRPOS              (               source_string              ,                REGEXP_EXTRACT              (               source_string              ,               regexp_string              ))      </code><br />
<br />
<strong>Note</strong> : Returns first occurrence.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         REGEXP_REPLACE       </code></td>
<td><code dir="ltr" translate="no">         REGEXP_REPLACE       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         REGEXP_SIMILAR       </code></td>
<td><code dir="ltr" translate="no">       IF(               REGEXP_CONTAINS              ,1,0)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         REGEXP_SUBSTR       </code></td>
<td><code dir="ltr" translate="no">         REGEXP_EXTRACT              ,                REGEXP_EXTRACT_ALL       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         REGEXP_SPLIT_TO_TABLE       </code></td>
<td>Custom user-defined function.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         REVERSE       </code></td>
<td><code dir="ltr" translate="no">         REVERSE       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         RIGHT       </code></td>
<td><code dir="ltr" translate="no">         SUBSTR              (               source_string              , -1,               length              )      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         RPAD       </code></td>
<td><code dir="ltr" translate="no">         RPAD       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         RTRIM       </code></td>
<td><code dir="ltr" translate="no">         RTRIM       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         STRTOK       </code><br />
<br />
<strong>Note</strong> : Each character in the delimiter string argument is considered a separate delimiter character. The default delimiter is a space character.</td>
<td><code dir="ltr" translate="no">         SPLIT              (               instring              ,               delimiter              )[               ORDINAL              (               tokennum              )]      </code><br />
<br />
<strong>Note</strong> : The entire <em>delimiter</em> string argument is used as a single delimiter. The default delimiter is a comma.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         STRTOK_SPLIT_TO_TABLE       </code></td>
<td>Custom user-defined function</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         SUBSTRING       </code> , <code dir="ltr" translate="no">         SUBSTR       </code></td>
<td><code dir="ltr" translate="no">         SUBSTR       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         TRIM       </code></td>
<td><code dir="ltr" translate="no">         TRIM       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         UPPER       </code></td>
<td><code dir="ltr" translate="no">         UPPER       </code></td>
</tr>
</tbody>
</table>

### Math functions

The following table maps Teradata math functions to their BigQuery equivalents. BigQuery offers the following additional math functions:

  - [`  DIV  `](/bigquery/docs/reference/standard-sql/mathematical_functions#div)
  - [`  IEEE_DIVIDE  `](/bigquery/docs/reference/standard-sql/mathematical_functions#ieee_divide)
  - [`  IS_INF  `](/bigquery/docs/reference/standard-sql/mathematical_functions#is_inf)
  - [`  IS_NAN  `](/bigquery/docs/reference/standard-sql/mathematical_functions#is_nan)
  - [`  LOG10  `](/bigquery/docs/reference/standard-sql/mathematical_functions#log10)
  - [`  SAFE_DIVIDE  `](/bigquery/docs/reference/standard-sql/mathematical_functions#safe_divide)

<table>
<thead>
<tr class="header">
<th>Teradata</th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         ABS       </code></td>
<td><code dir="ltr" translate="no">         ABS       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         ACOS       </code></td>
<td><code dir="ltr" translate="no">         ACOS       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         ACOSH       </code></td>
<td><code dir="ltr" translate="no">         ACOSH       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         ASIN       </code></td>
<td><code dir="ltr" translate="no">         ASIN       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         ASINH       </code></td>
<td><code dir="ltr" translate="no">         ASINH       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         ATAN       </code></td>
<td><code dir="ltr" translate="no">         ATAN       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         ATAN2       </code></td>
<td><code dir="ltr" translate="no">         ATAN2       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         ATANH       </code></td>
<td><code dir="ltr" translate="no">         ATANH       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         CEILING       </code></td>
<td><code dir="ltr" translate="no">         CEIL       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         CEILING       </code></td>
<td><code dir="ltr" translate="no">         CEILING       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         COS       </code></td>
<td><code dir="ltr" translate="no">         COS       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         COSH       </code></td>
<td><code dir="ltr" translate="no">         COSH       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         EXP       </code></td>
<td><code dir="ltr" translate="no">         EXP       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         FLOOR       </code></td>
<td><code dir="ltr" translate="no">         FLOOR       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         GREATEST       </code></td>
<td><code dir="ltr" translate="no">         GREATEST       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         LEAST       </code></td>
<td><code dir="ltr" translate="no">         LEAST       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         LN       </code></td>
<td><code dir="ltr" translate="no">         LN       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         LOG       </code></td>
<td><code dir="ltr" translate="no">         LOG       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         MOD       </code> ( <code dir="ltr" translate="no">       %      </code> operator)</td>
<td><code dir="ltr" translate="no">         MOD       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         NULLIFZERO       </code></td>
<td><code dir="ltr" translate="no">         NULLIF              (               expression              , 0)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         POWER       </code> ( <code dir="ltr" translate="no">       **      </code> operator)</td>
<td><code dir="ltr" translate="no">         POWER              ,               POW       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         RANDOM       </code></td>
<td><code dir="ltr" translate="no">         RAND       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         ROUND       </code></td>
<td><code dir="ltr" translate="no">         ROUND       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         SIGN       </code></td>
<td><code dir="ltr" translate="no">         SIGN       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         SIN       </code></td>
<td><code dir="ltr" translate="no">         SIN       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         SINH       </code></td>
<td><code dir="ltr" translate="no">         SINH       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         SQRT       </code></td>
<td><code dir="ltr" translate="no">         SQRT       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         TAN       </code></td>
<td><code dir="ltr" translate="no">         TAN       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         TANH       </code></td>
<td><code dir="ltr" translate="no">         TANH       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         TRUNC       </code></td>
<td><code dir="ltr" translate="no">         TRUNC       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         ZEROIFNULL       </code></td>
<td><code dir="ltr" translate="no">         IFNULL              (               expression              , 0),               COALESCE              (               expression              , 0)      </code></td>
</tr>
</tbody>
</table>

#### Rounding functions

Where Teradata uses Gaussian and Banker algorithms to round numerics, use the [`  ROUND_HALF_EVEN  ` `  RoundingMode  `](/bigquery/docs/reference/rest/v2/RoundingMode) in BigQuery:

``` text
-- Teradata syntax
round(3.45,1)

-- BigQuery syntax
round(CAST(3.45 as Numeric),1, 'ROUND_HALF_EVEN')
```

## DML syntax

This section addresses differences in data management language syntax between Teradata and BigQuery.

### `     INSERT    ` statement

Most Teradata `  INSERT  ` statements are compatible with BigQuery. The following table shows exceptions.

DML scripts in BigQuery have slightly different consistency semantics than the equivalent statements in Teradata. For an overview of snapshot isolation and session and transaction handling, see the [`  CREATE INDEX  `](#create_index) section elsewhere in this document.

<table style="width:38%;">
<colgroup>
<col style="width: 38%" />
<col style="width: 0%" />
</colgroup>
<thead>
<tr class="header">
<th>Teradata</th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         INSERT INTO                table              VALUES (...);      </code></td>
<td><code dir="ltr" translate="no">         INSERT INTO                table              (...) VALUES (...);      </code><br />
<br />
Teradata offers a <code dir="ltr" translate="no">       DEFAULT      </code> keyword for non-nullable columns.<br />
<br />
<strong>Note:</strong> In BigQuery, omitting column names in the <code dir="ltr" translate="no">       INSERT      </code> statement only works if values for all columns in the target table are included in ascending order based on their ordinal positions.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         INSERT INTO                table              VALUES (1,2,3);                INSERT INTO                table              VALUES (4,5,6);                INSERT INTO                table              VALUES (7,8,9);      </code></td>
<td><code dir="ltr" translate="no">         INSERT INTO                table              VALUES (1,2,3),              (4,5,6),              (7,8,9);       </code><br />
Teradata has a concept of <a href="https://docs.teradata.com/r/Basic-Teradata-Query-Reference/February-2022/Using-BTEQ/SQL-Requests/Request-Types">multi-statement request (MSR)</a> , which sends multiple <code dir="ltr" translate="no">       INSERT      </code> statements at a time. In BigQuery, this is not recommended due to the implicit transaction boundary between statements. Use <a href="/bigquery/docs/reference/standard-sql/dml-syntax#insert_values_with_subquery">multi-value</a> <code dir="ltr" translate="no">       INSERT      </code> instead.<br />
<br />
BigQuery allows concurrent <code dir="ltr" translate="no">       INSERT      </code> statements but might <a href="https://cloud.google.com/blog/products/data-analytics/dml-without-limits-now-in-bigquery">queue <code dir="ltr" translate="no">        UPDATE       </code></a> . To improve performance, consider the following approaches:<br />

<ul>
<li>Combine multiple rows in a single <code dir="ltr" translate="no">         INSERT        </code> statement, instead of one row per <code dir="ltr" translate="no">         INSERT        </code> operation.</li>
<li>Combine multiple DML statements (including <code dir="ltr" translate="no">         INSERT        </code> ) using a <code dir="ltr" translate="no">           MERGE         </code> statement.</li>
<li>Use <code dir="ltr" translate="no">         CREATE TABLE ... AS SELECT        </code> to create and populate new tables instead of <code dir="ltr" translate="no">         UPDATE        </code> or <code dir="ltr" translate="no">         DELETE        </code> , in particular when querying <a href="/bigquery/docs/querying-partitioned-tables#query_an_ingestion-time_partitioned_table">partitioned fields</a> or <a href="/bigquery/docs/reference/standard-sql/query-syntax#for_system_time_as_of">rollback or restore</a> .</li>
</ul></td>
</tr>
</tbody>
</table>

### `     UPDATE    ` statement

Most [Teradata `  UPDATE  ` statements](https://docs.teradata.com/r/Teradata-MultiLoad-Reference/February-2022/Teradata-MultiLoad-Commands/UPDATE) are compatible with BigQuery, except for the following items:

  - When you use a `  FROM  ` clause, the ordering of the `  FROM  ` and `  SET  ` clauses is reversed in Teradata and BigQuery.
  - In GoogleSQL, each `  UPDATE  ` statement must include the `  WHERE  ` keyword, followed by a condition. To update all rows in the table, use `  WHERE true  ` .

As a best practice, you should group multiple DML mutations instead of single `  UPDATE  ` and `  INSERT  ` statements. DML scripts in BigQuery have slightly different consistency semantics than equivalent statements in Teradata. For an overview on snapshot isolation and session and transaction handling, see the [`  CREATE INDEX  `](#create_index) section elsewhere in this document.

The following table shows Teradata `  UPDATE  ` statements and BigQuery statements that accomplish the same tasks.

For more information about `  UPDATE  ` in BigQuery, see the [BigQuery `  UPDATE  ` examples](/bigquery/docs/reference/standard-sql/dml-syntax#update_examples) in the DML documentation.

<table>
<thead>
<tr class="header">
<th>Teradata</th>
<th></th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       UPDATE                 table_A                 FROM               table_A              ,               table_B               SET              y =               table_B              .y,              z =               table_B              .z + 1              WHERE               table_A              .x =               table_B              .x              AND               table_A              .y IS NULL;      </code></td>
<td></td>
<td><code dir="ltr" translate="no">       UPDATE               table_A               SET              y =               table_B              .y,              z =               table_B              .z + 1              FROM               table_B               WHERE               table_A              .x =               table_B              .x              AND               table_A              .y IS NULL;      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       UPDATE               table              alias              SET x = x + 1              WHERE f(x) IN (0, 1);      </code></td>
<td></td>
<td><code dir="ltr" translate="no">       UPDATE               table               SET x = x + 1              WHERE f(x) IN (0, 1);      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       UPDATE               table_A               FROM               table_A              ,               table_B              ,               B               SET z =               table_B              .z              WHERE               table_A              .x =               table_B              .x              AND               table_A              .y =               table_B              .y;       </code></td>
<td></td>
<td><code dir="ltr" translate="no">       UPDATE               table_A               SET z =               table_B              .z              FROM               table_B               WHERE               table_A              .x =               table_B              .x              AND               table_A              .y =               table_B              .y;      </code></td>
</tr>
</tbody>
</table>

### `     DELETE    ` and `     TRUNCATE    ` statements

Both the `  DELETE  ` and `  TRUNCATE  ` statements are supported ways to remove rows from a table without affecting the table schema or indexes. `  TRUNCATE  ` deletes all the data, while `  DELETE  ` removes the selected rows from the table.

In BigQuery, the `  DELETE  ` statement must have a `  WHERE  ` clause. To delete all rows in the table (truncate), use `  WHERE true  ` . To speed truncate operations up for very large tables, we recommend using the [`  CREATE OR REPLACE TABLE ... AS SELECT  `](/bigquery/docs/reference/standard-sql/data-definition-language#creating_a_new_table_from_an_existing_table) statement, using a `  LIMIT 0  ` on the same table to replace itself. However, make sure to manually add partitioning and clustering information when using it.

Teradata vacuums deleted rows later. This means that `  DELETE  ` operations are initially faster than in BigQuery, but they require resources later, especially large-scale `  DELETE  ` operations that impact the majority of a table. To use a similar approach in BigQuery, we suggest reducing the number of `  DELETE  ` operations, such as by copying the rows not to be deleted into a new table. Alternatively, you can [remove entire partitions](/bigquery/docs/managing-partitioned-tables#delete_a_partition) . Both of these options are designed to be faster operations than atomic DML mutations.

For more information about `  DELETE  ` in BigQuery, see the [`  DELETE  ` examples](/bigquery/docs/reference/standard-sql/dml-syntax#delete_examples) in the DML documentation.

<table style="width:38%;">
<colgroup>
<col style="width: 38%" />
<col style="width: 0%" />
</colgroup>
<thead>
<tr class="header">
<th>Teradata</th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       BEGIN TRANSACTION;              LOCKING TABLE               table_A              FOR EXCLUSIVE;              DELETE FROM               table_A              ;              INSERT INTO               table_A              SELECT * FROM               table_B              ;              END TRANSACTION;      </code></td>
<td>Replacing the contents of a table with query output is the equivalent of a transaction. You can do this with either a <a href="/bigquery/docs/reference/bq-cli-reference#bq_query">query</a> operation or a <a href="/bigquery/docs/managing-tables#copy-table">copy</a> operation.<br />
<br />
Using a query operation:<br />
<br />
<code dir="ltr" translate="no">       bq query --replace --destination_table               table_A              'SELECT * FROM               table_B              ';      </code><br />
<br />
Using a copy operation:<br />
<br />
<code dir="ltr" translate="no">       bq cp -f               table_A                table_B       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       DELETE               database              .               table              ALL;      </code></td>
<td><code dir="ltr" translate="no">       DELETE FROM               table              WHERE TRUE;      </code><br />
<br />
Or for very large tables a faster way:<br />
<code dir="ltr" translate="no">       CREATE OR REPLACE               table              AS SELECT * FROM               table              LIMIT 0;      </code></td>
</tr>
</tbody>
</table>

### `     MERGE    ` statement

The `  MERGE  ` statement can combine `  INSERT  ` , `  UPDATE  ` , and `  DELETE  ` operations into a single "upsert" statement and perform the operations atomically. The `  MERGE  ` operation must match at most one source row for each target row. BigQuery and Teradata both follow ANSI Syntax.

Teradata's `  MERGE  ` operation is limited to matching primary keys within one [access module processor (AMP)](https://docs.teradata.com/r/Database-Introduction/July-2021/Teradata-Database-Hardware-and-Software-Architecture/Virtual-Processors/Access-Module-Processor) . In contrast, BigQuery has no size or column limitation for `  MERGE  ` operations, therefore using `  MERGE  ` is a useful optimization. However, if the `  MERGE  ` is primarily a large delete, see optimizations for `  DELETE  ` elsewhere in this document.

DML scripts in BigQuery have slightly different consistency semantics than equivalent statements in Teradata. For example, Teradata's SET tables in session mode might [ignore duplicates](https://docs.teradata.com/reader/b8dd8xEYJnxfsq4uFRrHQQ/4OgUH6g%7EQfr0TwCyhBrg9g) during a `  MERGE  ` operation. For an overview on handling MULTISET and SET tables, snapshot isolation, and session and transaction handling, see the [`  CREATE INDEX  `](#create_index) section elsewhere in this document.

### Rows-affected variables

In Teradata, the [`  ACTIVITY_COUNT  `](https://docs.teradata.com/r/SQL-Stored-Procedures-and-Embedded-SQL/July-2021/Result-Code-Variables/ACTIVITY_COUNT) variable is a Teradata ANSI SQL extension populated with the number of rows affected by a DML statement.

The [`  @@row_count  ` system variable](/bigquery/docs/reference/standard-sql/scripting#system_variables) in the [Scripting feature](/bigquery/docs/reference/standard-sql/scripting) has similar functionality. In BigQuery it would be more common to check the [`  numDmlAffectedRows  `](/bigquery/docs/reference/rest/v2/jobs/query#body.QueryResponse.FIELDS.num_dml_affected_rows) return value in the audit logs or the [`  INFORMATION_SCHEMA  `](/bigquery/docs/information-schema-jobs) views.

## DDL syntax

This section addresses differences in data definition language syntax between Teradata and BigQuery.

### `     CREATE TABLE    ` statement

Most Teradata [`  CREATE TABLE  `](https://docs.teradata.com/r/SQL-Data-Definition-Language-Syntax-and-Examples/July-2021/Table-Statements/CREATE-TABLE-and-CREATE-TABLE-AS) statements are compatible with BigQuery, except for the following syntax elements, which are not used in BigQuery:

  - `  MULTISET  ` . See the `  CREATE INDEX  ` section.
  - `  VOLATILE  ` . See the [Temporary tables](#temporary_tables) section.
  - `  [NO] FALLBACK  ` . See the [Rollback](#rollback) section.
  - `  [NO] BEFORE JOURNAL  ` , `  [NO] AFTER JOURNAL  `
  - `  CHECKSUM = DEFAULT | val  `
  - `  DEFAULT MERGEBLOCKRATIO  `
  - `  PRIMARY INDEX ( col , ...)  ` . See the `  CREATE INDEX  ` section.
  - `  UNIQUE PRIMARY INDEX  ` . See the `  CREATE INDEX  ` section.
  - `  CONSTRAINT  `
  - `  DEFAULT  `
  - `  IDENTITY  `

For more information about `  CREATE TABLE  ` in BigQuery, see the [BigQuery `  CREATE  ` examples](/bigquery/docs/reference/standard-sql/data-definition-language#create_table_statement) in the DML documentation.

#### Column options and attributes

The following column specifications for the `  CREATE TABLE  ` statement are not used in BigQuery:

  - `  FORMAT ' format '  ` . See the Teradata [type formatting](#type_formatting) section.
  - `  CHARACTER SET name  ` . BigQuery always uses UTF-8 encoding.
  - `  [NOT] CASESPECIFIC  `
  - `  COMPRESS val | ( val , ...)  `

Teradata extends the ANSI standard with a column [`  TITLE  `](https://docs.teradata.com/r/SQL-Data-Types-and-Literals/July-2021/Data-Type-Formats-and-Format-Phrases/TITLE) option. This feature can be similarly implemented in BigQuery using the column description as shown in the following table. Note this option is not available for Views.

<table>
<thead>
<tr class="header">
<th>Teradata</th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         CREATE TABLE              table (                col1              VARCHAR(30) TITLE '               column desc              '              );      </code></td>
<td><code dir="ltr" translate="no">         CREATE TABLE                dataset              .               table              (                col1              STRING                OPTIONS              (description="               column desc              ")              );      </code></td>
</tr>
</tbody>
</table>

#### Temporary tables

Teradata supports [volatile](https://docs.teradata.com/r/SQL-Fundamentals/July-2021/Database-Objects/Tables/Volatile-Tables) tables, which are often used to store intermediate results in scripts. There are several ways to achieve something similar to volatile tables in BigQuery:

  - **[`  CREATE TEMPORARY TABLE  `](/bigquery/docs/reference/standard-sql/data-definition-language#create_table_statement)** can be used in [Scripting](/bigquery/docs/reference/standard-sql/scripting) , and is valid during the lifetime of the script. If the table has to exist beyond a script, you can use the other options in this list.

  - **Dataset TTL:** Create a dataset that has a short time to live (for example, 1 hour) so that any tables created in the dataset are effectively temporary since they won't persist longer than the dataset's time to live. You can prefix all the table names in this dataset with `  temp  ` to clearly denote that the tables are temporary.

  - **Table TTL:** Create a table that has a table-specific short time to live using DDL statements similar to the following:
    
    ``` text
    CREATE TABLE temp.name (col1, col2, ...)
    OPTIONS(expiration_timestamp=TIMESTAMP_ADD(CURRENT_TIMESTAMP(), INTERVAL 1 HOUR));
    ```

  - **`  WITH  ` clause** : If a temporary table is needed only within the same block, use a temporary result using a [`  WITH  `](/bigquery/docs/reference/standard-sql/query-syntax#with_clause) statement or subquery. This is the most efficient option.

An often-used pattern in Teradata scripts ( [BTEQ](https://docs.teradata.com/r/Basic-Teradata-Query-Reference/February-2022/Introduction-to-BTEQ/Overview-of-BTEQ) ) is to create a permanent table, insert a value in it, use this like a temporary table in ongoing statements, and then delete or truncate the table afterwards. In effect, this uses the table as a constant variable (a semaphore). This approach is not efficient in BigQuery, and we recommend using [real variables](/bigquery/docs/reference/standard-sql/scripting#set) in [Scripting](/bigquery/docs/reference/standard-sql/scripting) instead, or using `  CREATE OR REPLACE  ` with [`  AS SELECT  `](/bigquery/docs/reference/standard-sql/data-definition-language#create_table_statement) query syntax to create a table that already has values in it.

### `     CREATE VIEW    ` statement

The following table shows equivalents between Teradata and BigQuery for the `  CREATE VIEW  ` statement. The clauses for table locking such as [`  LOCKING ROW FOR ACCESS  `](https://docs.teradata.com/r/SQL-Data-Manipulation-Language/July-2021/Statement-Syntax/LOCKING-Request-Modifier/Usage-Notes/Using-LOCKING-ROW) are not needed within BigQuery.

**Note:** Teradata does not directly support [materialized views](/bigquery/docs/materialized-views-intro) like BigQuery, only join indexes.

<table>
<thead>
<tr class="header">
<th>Teradata</th>
<th>BigQuery</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         CREATE VIEW                view_name              AS SELECT ...      </code></td>
<td><code dir="ltr" translate="no">         CREATE VIEW                view_name              AS SELECT ...      </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         REPLACE VIEW                view_name              AS SELECT ...      </code></td>
<td><code dir="ltr" translate="no">         CREATE OR REPLACE VIEW                 view_name              AS              SELECT ...      </code></td>
<td></td>
</tr>
<tr class="odd">
<td>Not supported</td>
<td><code dir="ltr" translate="no">         CREATE VIEW IF NOT EXISTS               OPTIONS(               view_option_list              )              AS SELECT ...      </code></td>
<td>Creates a new view only if the view does not currently exist in the specified dataset.</td>
</tr>
</tbody>
</table>

### `     CREATE [UNIQUE] INDEX    ` statement

Teradata requires indices for all tables and requires special workarounds like [MULTISET](https://docs.teradata.com/r/SQL-Data-Definition-Language-Syntax-and-Examples/July-2021/Table-Statements/CREATE-FOREIGN-TABLE/CREATE-FOREIGN-TABLE-Syntax-Elements/MULTISET) tables and [NoPI Tables](https://docs.teradata.com/r/Database-Design/July-2021/Primary-Index-Primary-AMP-Index-and-NoPI-Objects/NoPI-Tables-Column-Partitioned-NoPI-Tables-and-Column-Partitioned-NoPI-Join-Indexes) to work with non-unique or non-indexed data.

BigQuery does not require indices. This section describes approaches in BigQuery for how to create functionality similar to how indexes are used in Teradata where there is an actual business logic need.

#### Indexing for performance

Because it's a column-oriented database with query and storage optimization, BigQuery doesn't need explicit indexes. BigQuery provides functionality such as [partitioning and clustering](/bigquery/docs/clustered-tables) as well as [nested fields](/bigquery/docs/nested-repeated) , which can increase query efficiency and performance by optimizing how data is stored.

Teradata does not support materialized views. However, it offers [join indexes](https://docs.teradata.com/r/Database-Design/July-2021/Join-and-Hash-Indexes/Join-Indexes) using the `  CREATE JOIN INDEX  ` statement, which essentially materializes data that's needed for a join. BigQuery does not need materialized indexes to speed up performance, just as it doesn't need dedicated spool space for joins.

For other optimization cases, [materialized views](/bigquery/docs/materialized-views-intro) can be used.

#### Indexing for consistency (UNIQUE, PRIMARY INDEX)

In Teradata, a unique index can be used to prevent rows with non-unique keys in a table. If a process tries to insert or update data that has a value that's already in the index, the operation either fails with an index violation (MULTISET tables) or silently ignores it (SET tables).

Because BigQuery doesn't provide explicit indexes, a `  MERGE  ` statement can be used instead to insert only unique records into a target table from a staging table while discarding duplicate records. However, there is no way to prevent a user with edit permissions from inserting a duplicate record, because BigQuery never locks during `  INSERT  ` operations. To generate an error for duplicate records in BigQuery, you can use a `  MERGE  ` statement from a staging table, as shown in the following example.

<table>
<thead>
<tr class="header">
<th>Teradata</th>
<th></th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         CREATE              [               UNIQUE              ]               INDEX              name;      </code></td>
<td></td>
<td><code dir="ltr" translate="no">       MERGE `prototype.FIN_MERGE` t              USING `prototype.FIN_TEMP_IMPORT` m              ON t.               col1              = m.               col1               AND t.               col2              = m.               col2               WHEN MATCHED THEN              UPDATE SET t.               col1              = ERROR(CONCAT('Encountered error for ', m.               col1              , ' ', m.               col2              ))              WHEN NOT MATCHED THEN              INSERT (               col1              ,               col2              ,               col3              ,               col4              ,               col5              ,               col6              ,               col7              ,               col8              ) VALUES(               col1              ,               col2              ,               col3              ,               col4              ,               col5              ,               col6              ,CURRENT_TIMESTAMP(),CURRENT_TIMESTAMP());       </code></td>
</tr>
</tbody>
</table>

More often, users prefer to [remove duplicates independently](/bigquery/streaming-data-into-bigquery#manually_removing_duplicates) in order to find errors in downstream systems.  
BigQuery does not support `  DEFAULT  ` and `  IDENTITY  ` (sequences) columns.

#### Indexing to achieve locking

Teradata provides resources in the [access module processor](https://docs.teradata.com/r/Database-Introduction/July-2021/Teradata-Database-Hardware-and-Software-Architecture/Virtual-Processors/Access-Module-Processor) (AMP); queries can consume all-AMP, single-AMP, or group-AMP resources. DDL statements are all-AMP and therefore similar to a global DDL lock. BigQuery doesn't have a lock mechanism like this and can run concurrent queries and `  INSERT  ` statements up to your quota; only concurrent `  UPDATE  ` DML statements have certain [concurrency implications](https://cloud.google.com/blog/products/data-analytics/dml-without-limits-now-in-bigquery) : `  UPDATE  ` operations against the same partition are queued to ensure snapshot isolation, so you don't have to lock to prevent phantom reads or lost updates.

Because of these differences, the following Teradata elements are not used in BigQuery:

  - `  ON COMMIT DELETE ROWS;  `
  - `  ON COMMIT PRESERVE ROWS;  `

## Procedural SQL statements

This section describes how to convert procedural SQL statements that are used in stored procedures, functions, and triggers from Teradata to BigQuery Scripting, procedures, or user-defined functions (UDFs). All of these are available for system administrators to check using the [`  INFORMATION_SCHEMA  `](/bigquery/docs/information-schema-routines) views.

### `     CREATE PROCEDURE    ` statement

Stored procedures are supported as part of BigQuery [Scripting](/bigquery/docs/reference/standard-sql/scripting) .

In BigQuery, Scripting refers to any use of control statements, whereas procedures are named scripts (with arguments if needed) that can be called from other Scripts and stored permanently, if needed. A user-defined function (UDF) can also be written in JavaScript.

<table>
<thead>
<tr class="header">
<th>Teradata</th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         CREATE PROCEDURE       </code></td>
<td><code dir="ltr" translate="no">         CREATE PROCEDURE       </code> if a name is required, otherwise use inline with <code dir="ltr" translate="no">         BEGIN       </code> or in a single line with <code dir="ltr" translate="no">         CREATE TEMP FUNCTION       </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         REPLACE PROCEDURE       </code></td>
<td><code dir="ltr" translate="no">         CREATE OR REPLACE PROCEDURE       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         CALL       </code></td>
<td><code dir="ltr" translate="no">         CALL       </code></td>
</tr>
</tbody>
</table>

The sections that follow describe ways to convert existing Teradata procedural statements to BigQuery Scripting statements that have similar functionality.

### Variable declaration and assignment

BigQuery variables are valid during the lifetime of the script.

<table>
<thead>
<tr class="header">
<th>Teradata</th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         DECLARE       </code></td>
<td><code dir="ltr" translate="no">         DECLARE       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         SET       </code></td>
<td><code dir="ltr" translate="no">         SET       </code></td>
</tr>
</tbody>
</table>

### Error condition handlers

Teradata uses handlers on status codes in procedures for error control. In BigQuery, error handling is a core feature of the main control flow, similar to what other languages provide with `  TRY ... CATCH  ` blocks.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Teradata</th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         DECLARE EXIT HANDLER              FOR               SQLEXCEPTION       </code></td>
<td><code dir="ltr" translate="no">         BEGIN ... EXCEPTION WHEN ERROR THEN       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         SIGNAL                sqlstate       </code></td>
<td><code dir="ltr" translate="no">         RAISE                message       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         DECLARE CONTINUE HANDLER              FOR SQLSTATE VALUE 23505;      </code></td>
<td>Exception handlers that trigger for certain error conditions are not used by BigQuery.<br />
<br />
We recommend using <code dir="ltr" translate="no">         ASSERT       </code> statements where exit conditions are used for pre-checks or debugging, because this is ANSI SQL:2011 compliant.</td>
</tr>
</tbody>
</table>

The [`  SQLSTATE  `](https://docs.teradata.com/r/SQL-Stored-Procedures-and-Embedded-SQL/July-2021/Result-Code-Variables/SQLSTATE) variable in Teradata is similar to the [`  @@error  ` system variable](/bigquery/docs/reference/standard-sql/scripting#system_variables) in BigQuery. In BigQuery, it is more common to investigate errors using [audit logging](/bigquery/docs/reference/auditlogs) or the [`  INFORMATION_SCHEMA  `](/bigquery/docs/information-schema-routines) views.

### Cursor declarations and operations

Because BigQuery doesn't support cursors or sessions, the following statements aren't used in BigQuery:

  - `  DECLARE cursor_name CURSOR [FOR | WITH] ...  `
  - `  PREPARE stmt_id FROM sql_str ;  `
  - `  OPEN cursor_name [USING var , ...];  `
  - `  FETCH cursor_name INTO var , ...;  `
  - `  CLOSE cursor_name ;  `

### Dynamic SQL statements

The [Scripting feature](/bigquery/docs/reference/standard-sql/scripting) in BigQuery supports dynamic SQL statements like those shown in the following table.

<table>
<thead>
<tr class="header">
<th>Teradata</th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         EXECUTE IMMEDIATE                sql_str              ;      </code></td>
<td><code dir="ltr" translate="no">         EXECUTE IMMEDIATE                sql_str              ;      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         EXECUTE                stmt_id              [USING               var              ,...];      </code></td>
<td><code dir="ltr" translate="no">         EXECUTE IMMEDIATE                stmt_id              USING               var              ;      </code></td>
</tr>
</tbody>
</table>

The following Dynamic SQL statements are not used in BigQuery:

  - `  PREPARE stmt_id FROM sql_str ;  `

### Flow-of-control statements

The [Scripting feature](/bigquery/docs/reference/standard-sql/scripting) in BigQuery supports flow-of-control statements like those shown in the following table.

<table>
<colgroup>
<col style="width: 45%" />
<col style="width: 55%" />
</colgroup>
<thead>
<tr class="header">
<th>Teradata</th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         IF                condition                THEN                stmts                ELSE                stmts                END IF       </code></td>
<td><code dir="ltr" translate="no">         IF                condition                THEN                stmts                ELSE                stmts                END IF       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">           label_name                :               LOOP                stmts                END LOOP                  label_name                ;      </code></td>
<td>GOTO-style block constructs are not used in BigQuery.<br />
<br />
We recommend rewriting them as <a href="/bigquery/docs/user-defined-functions">user-defined functions (UDFs)</a> or use <code dir="ltr" translate="no">         ASSERT       </code> statements where they are used for error handling.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         REPEAT                stmts              UNTIL               condition                END REPEAT              ;      </code></td>
<td><code dir="ltr" translate="no">         WHILE                condition                DO                stmts                END WHILE       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         LEAVE                outer_proc_label              ;      </code></td>
<td><code dir="ltr" translate="no">         LEAVE       </code> is not used for GOTO-style blocks; it is used as a synonym for <code dir="ltr" translate="no">       BREAK      </code> to leave a <code dir="ltr" translate="no">       WHILE      </code> loop.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         LEAVE                label              ;      </code></td>
<td><code dir="ltr" translate="no">         LEAVE       </code> is not used for GOTO-style blocks; it is used as a synonym for <code dir="ltr" translate="no">       BREAK      </code> to leave a <code dir="ltr" translate="no">       WHILE      </code> loop.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         WITH RECURSIVE                temp_table              AS ( ... );      </code></td>
<td>Recursive queries (also known as recursive common table expressions (CTE)) are not used in BigQuery. They can be rewritten using arrays of <code dir="ltr" translate="no">         UNION ALL       </code> .</td>
</tr>
</tbody>
</table>

The following flow-of-control statements are not used in BigQuery because BigQuery doesn't use cursors or sessions:

  - `  FOR var AS SELECT ... DO stmts END FOR ;  `
  - `  FOR var AS cur CURSOR FOR SELECT ... DO stmts END FOR ;  `

## Metadata and transaction SQL statements

<table>
<colgroup>
<col style="width: 45%" />
<col style="width: 55%" />
</colgroup>
<thead>
<tr class="header">
<th>Teradata</th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         HELP TABLE                table_name              ;      </code><br />
<code dir="ltr" translate="no">         HELP VIEW                view_name              ;      </code></td>
<td><code dir="ltr" translate="no">       SELECT              * EXCEPT(is_generated, generation_expression, is_stored, is_updatable)              FROM              mydataset.INFORMATION_SCHEMA.COLUMNS;              WHERE              table_name=               table_name       </code><br />
<br />
The same query is valid to get column information for views.<br />
For more information, see the <a href="/bigquery/docs/information-schema-tables?#columns_view">Column view in the BigQuery <code dir="ltr" translate="no">        INFORMATION_SCHEMA       </code></a> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       SELECT * FROM dbc.tables WHERE tablekind = 'T';      </code><br />
<br />
(Teradata DBC view)</td>
<td><code dir="ltr" translate="no">       SELECT              * EXCEPT(is_typed)              FROM              mydataset.INFORMATION_SCHEMA.TABLES;      </code><br />
<br />
For more information, see <a href="/bigquery/docs/information-schema-intro">Introduction to BigQuery <code dir="ltr" translate="no">        INFORMATION_SCHEMA       </code></a> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         HELP STATISTICS                table_name              ;      </code></td>
<td><code dir="ltr" translate="no">       APPROX_COUNT_DISTINCT(               col              )      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       COLLECT STATS USING SAMPLE ON               table_name                column              (...);      </code></td>
<td>Not used in BigQuery.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       LOCKING TABLE               table_name              FOR EXCLUSIVE;      </code></td>
<td>BigQuery always uses snapshot isolation. For details, see <a href="#consistency_guarantees">Consistency guarantees</a> elsewhere in this document.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       SET SESSION CHARACTERISTICS AS TRANSACTION ISOLATION LEVEL ...      </code></td>
<td>BigQuery always uses Snapshot Isolation. For details, see <a href="#consistency_guarantees">Consistency guarantees</a> elsewhere in this document.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       BEGIN TRANSACTION;              SELECT ...              END TRANSACTION;      </code></td>
<td>BigQuery always uses Snapshot Isolation. For details, see <a href="#consistency_guarantees">Consistency guarantees</a> elsewhere in this document.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         EXPLAIN              ...      </code></td>
<td>Not used in BigQuery.<br />
<br />
Similar features are the <a href="/bigquery/query-plan-explanation">query plan explanation in the BigQuery web UI</a> and the slot allocation visible in the <code dir="ltr" translate="no">         INFORMATION_SCHEMA       </code> views and in <a href="/bigquery/docs/monitoring">audit logging in Cloud Monitoring</a> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       BEGIN TRANSACTION;              SELECT ...              END TRANSACTION;      </code></td>
<td><code dir="ltr" translate="no">       BEGIN              BEGIN TRANSACTION;              COMMIT TRANSACTION;              EXCEPTION WHEN ERROR THEN              -- Roll back the transaction inside the exception handler.              SELECT @@error.message;              ROLLBACK TRANSACTION;              END;      </code></td>
</tr>
</tbody>
</table>

### Multi-statement and multi-line SQL statements

Both Teradata and BigQuery support transactions (sessions) and therefore support statements separated by semicolons that are consistently executed together. For more information, see [Multi-statement transactions](/bigquery/docs/transactions) .

## Error codes and messages

Teradata error codes and BigQuery error codes are different. Providing a REST API, BigQuery relies primarily on [HTTP status codes](/bigquery/docs/error-messages) plus detailed error messages.

If your application logic is currently catching the following errors, try to eliminate the source of the error, because BigQuery will not return the same error codes.

  - `  SQLSTATE = '02000'  ` —"Row not found"
  - `  SQLSTATE = '21000'  ` —"Cardinality violation (Unique Index)"
  - `  SQLSTATE = '22000'  ` —"Data violation (Data Type)"
  - `  SQLSTATE = '23000'  ` —"Constraint Violation"

In BigQuery, it would be more common to use the [`  INFORMATION_SCHEMA  `](/bigquery/docs/information-schema-jobs) views or [audit logging](/bigquery/docs/reference/auditlogs) to drill down into errors.

For information about how to handle errors in Scripting, see the sections that follow.

## Consistency guarantees and transaction isolation

Both Teradata and BigQuery are atomic—that is, ACID-compliant on a per-mutation level across many rows. For example, a `  MERGE  ` operation is completely atomic, even with multiple inserted and updated values.

### Transactions

Teradata provides either Read Uncommitted (allowing dirty reads) or Serializable transaction [isolation level](https://docs.teradata.com/r/SQL-Data-Definition-Language-Detailed-Topics/July-2021/END-LOGGING-SET-TIME-ZONE/SET-SESSION-CHARACTERISTICS-AS-TRANSACTION-ISOLATION-LEVEL/Definition-of-Isolation-Level) when running in session mode (instead of auto-commit mode). In the best case, Teradata achieves strictly serializable isolation by using pessimistic locking against a row hash across all columns of rows across all partitions. Deadlocks are possible. DDL always forces a transaction boundary. Teradata Fastload jobs run independently, but only on empty tables.

BigQuery also [supports transactions](/bigquery/docs/transactions) . BigQuery helps ensure [optimistic concurrency control](https://en.wikipedia.org/wiki/Optimistic_concurrency_control) (first to commit wins) with [snapshot isolation](https://en.wikipedia.org/wiki/Snapshot_isolation) , in which a query reads the last committed data before the query starts. This approach guarantees the same level of consistency on a per-row, per-mutation basis and across rows within the same DML statement, yet avoids deadlocks. In the case of multiple `  UPDATE  ` statements against the same table, BigQuery switches to [pessimistic concurrency control](/bigquery/docs/reference/standard-sql/data-manipulation-language#limitations) and [queues](https://cloud.google.com/blog/products/data-analytics/dml-without-limits-now-in-bigquery) multiple `  UPDATE  ` statements, automatically retrying in case of conflicts. `  INSERT  ` DML statements and load jobs can run concurrently and independently to append to tables.

### Rollback

Teradata supports [two session rollback modes](https://docs.teradata.com/r/SQL-Request-and-Transaction-Processing/July-2021/Transaction-Processing/Rollback-Processing) , ANSI session mode and Teradata session mode ( `  SET SESSION CHARACTERISTICS  ` and `  SET SESSION TRANSACTION  ` ), depending on which rollback mode you want. In failure cases, the transaction might not be rolled back.

BigQuery supports the [`  ROLLBACK TRANSACTION  ` statement](/bigquery/docs/reference/standard-sql/procedural-language#rollback_transaction) . There is no [`  ABORT  ` statement](https://docs.teradata.com/r/Database-Utilities/July-2021/Dump-Unload/Load-Utility-dul/DUL-Commands/ABORT) in BigQuery.

## Database limits

Always check [the BigQuery public documentation](/bigquery/quotas) for the latest quotas and limits. Many quotas for large-volume users can be raised by contacting the Cloud Support team. The following table shows a comparison of the Teradata and BigQuery database limits.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Teradata</th>
<th>BigQuery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Tables per database</td>
<td>Unrestricted</td>
<td>Unrestricted</td>
</tr>
<tr class="even">
<td>Columns per table</td>
<td>2,048</td>
<td>10,000</td>
</tr>
<tr class="odd">
<td>Maximum row size</td>
<td>1 MB</td>
<td>100 MB</td>
</tr>
<tr class="even">
<td>Column name length</td>
<td>128 Unicode chars</td>
<td>300 Unicode characters</td>
</tr>
<tr class="odd">
<td>Table description length</td>
<td>128 Unicode chars</td>
<td>16,384 Unicode characters</td>
</tr>
<tr class="even">
<td>Rows per table</td>
<td>Unlimited</td>
<td>Unlimited</td>
</tr>
<tr class="odd">
<td>Maximum SQL request length</td>
<td>1 MB</td>
<td>1 MB (maximum unresolved GoogleSQL query length)<br />
12 MB (maximum resolved legacy and GoogleSQL query length)<br />
<br />
Streaming:<br />

<ul>
<li>10 MB (HTTP request size limit)</li>
<li>10,000 (maximum rows per request)</li>
</ul></td>
</tr>
<tr class="even">
<td>Maximum request and response size</td>
<td>7 MB (request), 16 MB (response)</td>
<td>10 MB (request) and 10 GB (response), or virtually unlimited if you use pagination or the Cloud Storage API.</td>
</tr>
<tr class="odd">
<td>Maximum number of concurrent sessions</td>
<td>120 per parsing engine (PE)</td>
<td>1,000 concurrent multi-statement queries (can be raised with a <a href="/bigquery/docs/slots">slot reservation</a> ), 300 concurrent API requests per user.</td>
</tr>
<tr class="even">
<td>Maximum number of concurrent (fast) loads</td>
<td>30 (default 5)</td>
<td>No concurrency limit; jobs are queued. 100,000 load jobs per project per day.</td>
</tr>
</tbody>
</table>
