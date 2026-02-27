# Legacy SQL feature availability

This document describes upcoming restrictions to BigQuery legacy SQL availability, which are based on usage during an evaluation period and take effect after June 1, 2026. These changes are part of BigQuery's transition away from legacy SQL to GoogleSQL, the recommended, ANSI-compliant dialect for BigQuery.

Migrating to GoogleSQL offers these benefits over legacy SQL:

  - It can be more cost-effective, using the [BigQuery advanced runtime](/bigquery/docs/advanced-runtime) for better performance.
  - It lets you use features not supported by legacy SQL, such as [DML](/bigquery/docs/reference/standard-sql/dml-syntax) and [DDL](/bigquery/docs/reference/standard-sql/data-definition-language) statements, Common Table Expressions (CTEs), complex subqueries and join predicates, [materialized views](/bigquery/docs/materialized-views-intro) , [search indexes](/bigquery/docs/search) , and [Generative AI functions](/bigquery/docs/generative-ai-overview) .

## How feature availability works

BigQuery monitors the use of legacy SQL features during an evaluation period. For organizations and projects that don't use legacy SQL between November 1, 2025, and June 1, 2026, legacy SQL becomes unavailable after the evaluation period ends. For organizations and projects that use legacy SQL during the evaluation period, you can continue to run queries using the specific set of legacy SQL features that you use.

Feature usage is aggregated at the organization level. If any project within an organization uses a feature, that feature remains available to all other projects in the organization. For projects not associated with an organization, feature availability is managed at the project level.

## Legacy SQL feature sets

Legacy SQL capabilities are organized into three feature sets: basic language capabilities, extended language capabilities, and function groupings. The following sections detail the features within each set.

### Basic language capabilities

These features are the core of legacy SQL. This entire feature set is available to any organization or stand-alone project that runs at least one legacy SQL query during the evaluation period.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Category</th>
<th>Features</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Query syntax</td>
<td><ul>
<li><code dir="ltr" translate="no">         SELECT        </code></li>
<li><code dir="ltr" translate="no">         FROM        </code></li>
<li><code dir="ltr" translate="no">         JOIN        </code></li>
<li><code dir="ltr" translate="no">         WHERE        </code></li>
<li><code dir="ltr" translate="no">         GROUP BY        </code></li>
<li><code dir="ltr" translate="no">         HAVING        </code></li>
<li><code dir="ltr" translate="no">         ORDER BY        </code></li>
<li><code dir="ltr" translate="no">         LIMIT        </code></li>
</ul></td>
</tr>
<tr class="even">
<td>Expression logic</td>
<td><strong>Literals:</strong>
<ul>
<li><code dir="ltr" translate="no">         TRUE        </code></li>
<li><code dir="ltr" translate="no">         FALSE        </code></li>
<li><code dir="ltr" translate="no">         NULL        </code></li>
</ul>
<br />
<strong>Logical operators:</strong>
<ul>
<li><code dir="ltr" translate="no">         AND        </code></li>
<li><code dir="ltr" translate="no">         OR        </code></li>
<li><code dir="ltr" translate="no">         NOT        </code></li>
</ul>
<br />
<strong>Comparison functions:</strong>
<ul>
<li><code dir="ltr" translate="no">         =        </code></li>
<li><code dir="ltr" translate="no">         !=        </code></li>
<li><code dir="ltr" translate="no">         &lt;&gt;        </code></li>
<li><code dir="ltr" translate="no">         &lt;        </code></li>
<li><code dir="ltr" translate="no">         &lt;=        </code></li>
<li><code dir="ltr" translate="no">         &gt;        </code></li>
<li><code dir="ltr" translate="no">         &gt;=        </code></li>
<li><code dir="ltr" translate="no">         IN        </code></li>
<li><code dir="ltr" translate="no">         IS NULL        </code></li>
<li><code dir="ltr" translate="no">         IS NOT NULL        </code></li>
<li><code dir="ltr" translate="no">         IS_EXPLICITLY_DEFINED        </code></li>
<li><code dir="ltr" translate="no">         IS_INF        </code></li>
<li><code dir="ltr" translate="no">         IS_NAN        </code></li>
<li><code dir="ltr" translate="no">         ... BETWEEN ... AND ...        </code></li>
</ul>
<br />
<strong>Control flow statements:</strong>
<ul>
<li><code dir="ltr" translate="no">         IF        </code></li>
<li><code dir="ltr" translate="no">         IFNULL        </code></li>
<li><code dir="ltr" translate="no">         CASE WHEN … THEN …        </code></li>
</ul></td>
</tr>
<tr class="odd">
<td>Basic operations</td>
<td><strong>Arithmetic operators:</strong>
<ul>
<li><code dir="ltr" translate="no">         +        </code></li>
<li><code dir="ltr" translate="no">         -        </code></li>
<li><code dir="ltr" translate="no">         *        </code></li>
<li><code dir="ltr" translate="no">         /        </code></li>
<li><code dir="ltr" translate="no">         %        </code></li>
</ul>
<br />
<strong>Basic aggregate functions:</strong>
<ul>
<li><code dir="ltr" translate="no">         AVG        </code></li>
<li><code dir="ltr" translate="no">         COUNT        </code></li>
<li><code dir="ltr" translate="no">         FIRST        </code></li>
<li><code dir="ltr" translate="no">         LAST        </code></li>
<li><code dir="ltr" translate="no">         MAX        </code></li>
<li><code dir="ltr" translate="no">         MIN        </code></li>
<li><code dir="ltr" translate="no">         NTH        </code></li>
<li><code dir="ltr" translate="no">         SUM        </code></li>
</ul></td>
</tr>
<tr class="even">
<td>Data elements</td>
<td><strong>Basic Data Types:</strong>
<ul>
<li><code dir="ltr" translate="no">         BYTES        </code></li>
<li><code dir="ltr" translate="no">         BOOLEAN        </code></li>
<li><code dir="ltr" translate="no">         FLOAT        </code></li>
<li><code dir="ltr" translate="no">         INTEGER        </code></li>
<li><code dir="ltr" translate="no">         STRING        </code></li>
<li><code dir="ltr" translate="no">         TIMESTAMP        </code></li>
</ul>
<br />
<strong>Structured and partially supported data types:</strong>
<ul>
<li>Exact Numeric: <code dir="ltr" translate="no">         NUMERIC        </code> , <code dir="ltr" translate="no">         BIGNUMERIC        </code></li>
<li>Civil Time: <code dir="ltr" translate="no">         DATE        </code> , <code dir="ltr" translate="no">         TIME        </code> , <code dir="ltr" translate="no">         DATETIME        </code></li>
<li>Structured Fields: Nested fields, repeated fields</li>
</ul>
<br />
<strong>Casting Functions:</strong>
<ul>
<li><code dir="ltr" translate="no">         CAST(expr AS type)        </code></li>
<li><code dir="ltr" translate="no">         BOOLEAN        </code></li>
<li><code dir="ltr" translate="no">         BYTES        </code></li>
<li><code dir="ltr" translate="no">         FLOAT        </code></li>
<li><code dir="ltr" translate="no">         INTEGER        </code></li>
<li><code dir="ltr" translate="no">         STRING        </code></li>
</ul>
<br />
<strong>Coercions:</strong> All automatic data type coercions are included.</td>
</tr>
</tbody>
</table>

### Extended language capabilities

This category includes specific legacy SQL features that go beyond the basic set. Unlike basic capabilities or function groupings, each feature in this category is tracked individually. You must explicitly use each feature during the evaluation period for it to remain available.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Category</th>
<th>Features</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Extended features</td>
<td><ul>
<li><a href="/bigquery/docs/reference/legacy-sql#comma-as-union-all">Comma as <code dir="ltr" translate="no">          UNION ALL         </code></a></li>
<li><a href="/bigquery/docs/reference/legacy-sql#flatten-operator">Explicit <code dir="ltr" translate="no">          FLATTEN         </code> operator</a></li>
<li><a href="/bigquery/docs/reference/legacy-sql#each"><code dir="ltr" translate="no">          GROUP BY         </code> with <code dir="ltr" translate="no">          EACH         </code> modifier</a></li>
<li><a href="/bigquery/docs/reference/legacy-sql#stringfunctions"><code dir="ltr" translate="no">          IGNORE CASE         </code> modifier</a></li>
<li><a href="/bigquery/docs/reference/legacy-sql#each-modifier"><code dir="ltr" translate="no">          JOIN         </code> with <code dir="ltr" translate="no">          EACH         </code> modifier</a></li>
<li><a href="/bigquery/docs/reference/standard-sql/migrating-from-legacy-sql#logical_views">Logical views</a></li>
<li><a href="/bigquery/docs/reference/legacy-sql#omit"><code dir="ltr" translate="no">          OMIT … IF         </code> clause</a></li>
<li><a href="/bigquery/docs/reference/legacy-sql#semi-joins">Semi-join or Anti-join</a></li>
<li><a href="/bigquery/docs/reference/legacy-sql#from-tables">Table decorator - Partition</a></li>
<li><a href="/bigquery/docs/table-decorators#range_decorators">Table decorator - Range</a></li>
<li><a href="/bigquery/docs/table-decorators#time_decorators">Table decorator - Time</a></li>
<li><a href="/bigquery/docs/user-defined-functions-legacy">User-defined functions</a></li>
<li><a href="/bigquery/docs/reference/legacy-sql#table-date-range">Wildcard - <code dir="ltr" translate="no">          TABLE_DATE_RANGE         </code></a></li>
<li><a href="/bigquery/docs/reference/legacy-sql#table-date-range-strict">Wildcard - <code dir="ltr" translate="no">          TABLE_DATE_RANGE_STRICT         </code></a></li>
<li><a href="/bigquery/docs/reference/legacy-sql#table-query">Wildcard - <code dir="ltr" translate="no">          TABLE_QUERY         </code></a></li>
<li><a href="/bigquery/docs/reference/legacy-sql#within"><code dir="ltr" translate="no">          WITHIN         </code> modifier for aggregate functions</a></li>
</ul></td>
</tr>
</tbody>
</table>

### Function groupings

Built-in functions are organized into related categories. Using any single function within a grouping during the evaluation period makes all functions in that entire grouping available.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Function Grouping</th>
<th>Functions</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Advanced window functions</td>
<td><ul>
<li><code dir="ltr" translate="no">         CUME_DIST        </code></li>
<li><code dir="ltr" translate="no">         DENSE_RANK        </code></li>
<li><code dir="ltr" translate="no">         FIRST_VALUE        </code></li>
<li><code dir="ltr" translate="no">         LAG        </code></li>
<li><code dir="ltr" translate="no">         LAST_VALUE        </code></li>
<li><code dir="ltr" translate="no">         LEAD        </code></li>
<li><code dir="ltr" translate="no">         NTH_VALUE        </code></li>
<li><code dir="ltr" translate="no">         NTILE        </code></li>
<li><code dir="ltr" translate="no">         PERCENT_RANK        </code></li>
<li><code dir="ltr" translate="no">         PERCENTILE_CONT        </code></li>
<li><code dir="ltr" translate="no">         PERCENTILE_DISC        </code></li>
<li><code dir="ltr" translate="no">         RANK        </code></li>
<li><code dir="ltr" translate="no">         RATIO_TO_REPORT        </code></li>
<li><code dir="ltr" translate="no">         ROW_NUMBER        </code></li>
</ul></td>
</tr>
<tr class="even">
<td>Aggregate functions for statistics</td>
<td><ul>
<li><code dir="ltr" translate="no">         CORR        </code></li>
<li><code dir="ltr" translate="no">         COVAR_POP        </code></li>
<li><code dir="ltr" translate="no">         COVAR_SAMP        </code></li>
<li><code dir="ltr" translate="no">         STDDEV        </code></li>
<li><code dir="ltr" translate="no">         STDDEV_POP        </code></li>
<li><code dir="ltr" translate="no">         STDDEV_SAMP        </code></li>
<li><code dir="ltr" translate="no">         VARIANCE        </code></li>
<li><code dir="ltr" translate="no">         VAR_POP        </code></li>
<li><code dir="ltr" translate="no">         VAR_SAMP        </code></li>
</ul></td>
</tr>
<tr class="odd">
<td>Aggregate functions returning repeated field</td>
<td><ul>
<li><code dir="ltr" translate="no">         NEST        </code></li>
<li><code dir="ltr" translate="no">         QUANTILES        </code></li>
<li><code dir="ltr" translate="no">         UNIQUE        </code></li>
</ul></td>
</tr>
<tr class="even">
<td>Aggregate functions with bits operations</td>
<td><ul>
<li><code dir="ltr" translate="no">         BIT_AND        </code></li>
<li><code dir="ltr" translate="no">         BIT_OR        </code></li>
<li><code dir="ltr" translate="no">         BIT_XOR        </code></li>
</ul></td>
</tr>
<tr class="odd">
<td>Aggregate functions with concatenation</td>
<td><ul>
<li><code dir="ltr" translate="no">         GROUP_CONCAT        </code></li>
<li><code dir="ltr" translate="no">         GROUP_CONCAT_UNQUOTED        </code></li>
</ul></td>
</tr>
<tr class="even">
<td>Aggregate functions with sort</td>
<td><ul>
<li><code dir="ltr" translate="no">         COUNT([DISTINCT])        </code></li>
<li><code dir="ltr" translate="no">         EXACT_COUNT_DISTINCT        </code></li>
<li><code dir="ltr" translate="no">         TOP ... COUNT(*)        </code></li>
</ul></td>
</tr>
<tr class="odd">
<td>Basic window functions</td>
<td><ul>
<li><code dir="ltr" translate="no">         AVG        </code></li>
<li><code dir="ltr" translate="no">         COUNT(*)        </code></li>
<li><code dir="ltr" translate="no">         COUNT([DISTINCT])        </code></li>
<li><code dir="ltr" translate="no">         MAX        </code></li>
<li><code dir="ltr" translate="no">         MIN        </code></li>
<li><code dir="ltr" translate="no">         STDDEV        </code></li>
<li><code dir="ltr" translate="no">         SUM        </code></li>
</ul></td>
</tr>
<tr class="even">
<td>Bitwise functions</td>
<td><ul>
<li><code dir="ltr" translate="no">         &amp;        </code></li>
<li><code dir="ltr" translate="no">         |        </code></li>
<li><code dir="ltr" translate="no">         ^        </code></li>
<li><code dir="ltr" translate="no">         &lt;&lt;        </code></li>
<li><code dir="ltr" translate="no">         &gt;&gt;        </code></li>
<li><code dir="ltr" translate="no">         ~        </code></li>
<li><code dir="ltr" translate="no">         BIT_COUNT        </code></li>
</ul></td>
</tr>
<tr class="odd">
<td>Conditional expressions</td>
<td><ul>
<li><code dir="ltr" translate="no">         COALESCE        </code></li>
<li><code dir="ltr" translate="no">         EVERY        </code></li>
<li><code dir="ltr" translate="no">         GREATEST        </code></li>
<li><code dir="ltr" translate="no">         LEAST        </code></li>
<li><code dir="ltr" translate="no">         NVL        </code></li>
<li><code dir="ltr" translate="no">         SOME        </code></li>
</ul></td>
</tr>
<tr class="even">
<td>Conversion functions</td>
<td><ul>
<li><code dir="ltr" translate="no">         FROM_BASE64        </code></li>
<li><code dir="ltr" translate="no">         HEX_STRING        </code></li>
<li><code dir="ltr" translate="no">         TO_BASE64        </code></li>
</ul></td>
</tr>
<tr class="odd">
<td>Current time functions</td>
<td><ul>
<li><code dir="ltr" translate="no">         NOW        </code></li>
<li><code dir="ltr" translate="no">         CURRENT_DATE        </code></li>
<li><code dir="ltr" translate="no">         CURRENT_TIME        </code></li>
<li><code dir="ltr" translate="no">         CURRENT_TIMESTAMP        </code></li>
</ul></td>
</tr>
<tr class="even">
<td>Current user functions</td>
<td><ul>
<li><code dir="ltr" translate="no">         CURRENT_USER        </code></li>
</ul></td>
</tr>
<tr class="odd">
<td>Date and time functions</td>
<td><ul>
<li><code dir="ltr" translate="no">         DATE        </code></li>
<li><code dir="ltr" translate="no">         DATE_ADD        </code></li>
<li><code dir="ltr" translate="no">         DATEDIFF        </code></li>
<li><code dir="ltr" translate="no">         TIME        </code></li>
<li><code dir="ltr" translate="no">         TIMESTAMP        </code></li>
</ul></td>
</tr>
<tr class="even">
<td>Function RAND</td>
<td><ul>
<li><code dir="ltr" translate="no">         RAND        </code></li>
</ul></td>
</tr>
<tr class="odd">
<td>Functions returning repeated field</td>
<td><ul>
<li><code dir="ltr" translate="no">         POSITION        </code></li>
<li><code dir="ltr" translate="no">         SPLIT        </code></li>
</ul></td>
</tr>
<tr class="even">
<td>Hashing functions</td>
<td><ul>
<li><code dir="ltr" translate="no">         HASH        </code></li>
<li><code dir="ltr" translate="no">         SHA1        </code></li>
<li><code dir="ltr" translate="no">         FARM_FINGERPRINT        </code></li>
</ul></td>
</tr>
<tr class="odd">
<td>IP functions</td>
<td><ul>
<li><code dir="ltr" translate="no">         FORMAT_IP        </code></li>
<li><code dir="ltr" translate="no">         FORMAT_PACKED_IP        </code></li>
<li><code dir="ltr" translate="no">         PARSE_IP        </code></li>
<li><code dir="ltr" translate="no">         PARSE_PACKED_IP        </code></li>
</ul></td>
</tr>
<tr class="even">
<td>JSON functions</td>
<td><ul>
<li><code dir="ltr" translate="no">         JSON_EXTRACT        </code></li>
<li><code dir="ltr" translate="no">         JSON_EXTRACT_SCALAR        </code></li>
</ul></td>
</tr>
<tr class="odd">
<td>Mathematical functions</td>
<td><ul>
<li><code dir="ltr" translate="no">         ABS        </code></li>
<li><code dir="ltr" translate="no">         ACOS        </code></li>
<li><code dir="ltr" translate="no">         ASIN        </code></li>
<li><code dir="ltr" translate="no">         ATAN        </code></li>
<li><code dir="ltr" translate="no">         ATAN2        </code></li>
<li><code dir="ltr" translate="no">         CEIL        </code></li>
<li><code dir="ltr" translate="no">         COS        </code></li>
<li><code dir="ltr" translate="no">         DEGREES        </code></li>
<li><code dir="ltr" translate="no">         EXP        </code></li>
<li><code dir="ltr" translate="no">         FLOOR        </code></li>
<li><code dir="ltr" translate="no">         LN        </code></li>
<li><code dir="ltr" translate="no">         LOG        </code></li>
<li><code dir="ltr" translate="no">         LOG10        </code></li>
<li><code dir="ltr" translate="no">         LOG2        </code></li>
<li><code dir="ltr" translate="no">         PI        </code></li>
<li><code dir="ltr" translate="no">         POW        </code></li>
<li><code dir="ltr" translate="no">         RADIANS        </code></li>
<li><code dir="ltr" translate="no">         ROUND        </code></li>
<li><code dir="ltr" translate="no">         SIN        </code></li>
<li><code dir="ltr" translate="no">         SQRT        </code></li>
<li><code dir="ltr" translate="no">         TAN        </code></li>
</ul></td>
</tr>
<tr class="even">
<td>Mathematical hyperbolic functions</td>
<td><ul>
<li><code dir="ltr" translate="no">         ACOSH        </code></li>
<li><code dir="ltr" translate="no">         ASINH        </code></li>
<li><code dir="ltr" translate="no">         ATANH        </code></li>
<li><code dir="ltr" translate="no">         COSH        </code></li>
<li><code dir="ltr" translate="no">         SINH        </code></li>
<li><code dir="ltr" translate="no">         TANH        </code></li>
</ul></td>
</tr>
<tr class="odd">
<td>Part of TIMESTAMP functions</td>
<td><ul>
<li><code dir="ltr" translate="no">         DAY        </code></li>
<li><code dir="ltr" translate="no">         DAYOFWEEK        </code></li>
<li><code dir="ltr" translate="no">         DAYOFYEAR        </code></li>
<li><code dir="ltr" translate="no">         HOUR        </code></li>
<li><code dir="ltr" translate="no">         MINUTE        </code></li>
<li><code dir="ltr" translate="no">         MONTH        </code></li>
<li><code dir="ltr" translate="no">         QUARTER        </code></li>
<li><code dir="ltr" translate="no">         SECOND        </code></li>
<li><code dir="ltr" translate="no">         WEEK        </code></li>
<li><code dir="ltr" translate="no">         YEAR        </code></li>
</ul></td>
</tr>
<tr class="even">
<td>Regular expression functions</td>
<td><ul>
<li><code dir="ltr" translate="no">         REGEXP_MATCH        </code></li>
<li><code dir="ltr" translate="no">         REGEXP_EXTRACT        </code></li>
<li><code dir="ltr" translate="no">         REGEXP_REPLACE        </code></li>
</ul></td>
</tr>
<tr class="odd">
<td>String functions</td>
<td><ul>
<li><code dir="ltr" translate="no">         CONTAINS        </code></li>
<li><code dir="ltr" translate="no">         CONCAT        </code></li>
<li><code dir="ltr" translate="no">         INSTR        </code></li>
<li><code dir="ltr" translate="no">         LEFT        </code></li>
<li><code dir="ltr" translate="no">         LENGTH        </code></li>
<li><code dir="ltr" translate="no">         LOWER        </code></li>
<li><code dir="ltr" translate="no">         LPAD        </code></li>
<li><code dir="ltr" translate="no">         LTRIM        </code></li>
<li><code dir="ltr" translate="no">         REPLACE        </code></li>
<li><code dir="ltr" translate="no">         RIGHT        </code></li>
<li><code dir="ltr" translate="no">         RPAD        </code></li>
<li><code dir="ltr" translate="no">         RTRIM        </code></li>
<li><code dir="ltr" translate="no">         SUBSTR        </code></li>
<li><code dir="ltr" translate="no">         UPPER        </code></li>
</ul></td>
</tr>
<tr class="even">
<td>URL functions</td>
<td><ul>
<li><code dir="ltr" translate="no">         HOST        </code></li>
<li><code dir="ltr" translate="no">         DOMAIN        </code></li>
<li><code dir="ltr" translate="no">         TLD        </code></li>
</ul></td>
</tr>
<tr class="odd">
<td>UNIX timestamp functions</td>
<td><ul>
<li><code dir="ltr" translate="no">         FORMAT_UTC_USEC        </code></li>
<li><code dir="ltr" translate="no">         MSEC_TO_TIMESTAMP        </code></li>
<li><code dir="ltr" translate="no">         PARSE_UTC_USEC        </code></li>
<li><code dir="ltr" translate="no">         SEC_TO_TIMESTAMP        </code></li>
<li><code dir="ltr" translate="no">         STRFTIME_UTC_USEC        </code></li>
<li><code dir="ltr" translate="no">         TIMESTAMP_TO_SEC        </code></li>
<li><code dir="ltr" translate="no">         TIMESTAMP_TO_MSEC        </code></li>
<li><code dir="ltr" translate="no">         TIMESTAMP_TO_USEC        </code></li>
<li><code dir="ltr" translate="no">         USEC_TO_TIMESTAMP        </code></li>
<li><code dir="ltr" translate="no">         UTC_USEC_TO_DAY        </code></li>
<li><code dir="ltr" translate="no">         UTC_USEC_TO_HOUR        </code></li>
<li><code dir="ltr" translate="no">         UTC_USEC_TO_MONTH        </code></li>
<li><code dir="ltr" translate="no">         UTC_USEC_TO_WEEK        </code></li>
<li><code dir="ltr" translate="no">         UTC_USEC_TO_YEAR        </code></li>
</ul></td>
</tr>
</tbody>
</table>

## Examples of feature availability

The following examples demonstrate how feature availability works.

### Example: Accessing basic language capabilities

A project runs a legacy SQL query during the evaluation period. Assume table `  T  ` contains a column `  X  ` of type `  INTEGER  ` .

``` text
#legacySQL
SELECT X FROM T
```

This usage ensures that all projects within the organization retain the ability to run queries that use any feature from the basic language capabilities set. For example, the following query continues to work:

``` text
#legacySQL
SELECT X FROM T WHERE X > 10
```

### Example: Using function groupings

A project uses one function from a specific function grouping. Assume table `  T  ` contains a column `  X  ` of type `  FLOAT  ` .

``` text
#legacySQL
SELECT SIN(X) FROM T
```

The use of the `  SIN()  ` function makes the entire mathematical functions grouping available. Consequently, all projects within the organization can use any other function from that grouping, such as `  COS()  ` .

``` text
#legacySQL
SELECT COS(X) FROM T
```

Conversely, the following query fails after the evaluation period if no project in the organization uses any function from the aggregate functions for statistics grouping.

``` text
#legacySQL
SELECT STDDEV(X) FROM T
```

### Example: Feature retention across different tables

Assume table `  X  ` has a column `  A  ` ( `  INTEGER  ` ) and table `  Y  ` has column `  B  ` ( `  FLOAT  ` ). A project runs the following query during the evaluation period:

``` text
#legacySQL
SELECT SIN(A) FROM X
```

The organization can run the following query after the evaluation period ends. The query works because the mathematical functions feature was retained by the first query. The retention is independent of the specific table, column name, or data type used, as both `  INTEGER  ` and `  FLOAT  ` are part of the basic language capability.

``` text
#legacySQL
SELECT COS(B) FROM Y
```

### Example: Complex query

Assume table `  T  ` contains a column `  X  ` of type `  STRING  ` . A project runs the following query during the evaluation period:

``` text
#legacySQL
SELECT value, AVG(FLOAT(value)) OVER (ORDER BY value) AS avg
 FROM (
  SELECT LENGTH(SPLIT(X, ',')) AS value
    FROM T
)
```

This query uses features from the basic language capabilities and three function groupings: basic window functions, string functions, and functions returning repeated values. All projects within the organization retain these features. Therefore, a new query that uses a different combination of functions from those same retained feature sets succeeds.

``` text
#legacySQL
SELECT value, COUNT(STRING(value)) OVER (ORDER BY value) as count
 FROM (
  SELECT CONCAT(SPLIT(X, ','), '123') AS value
    FROM T
)
```

## Frequently asked questions

**Can a new organization use legacy SQL?**

Following the evaluation period, legacy SQL isn't available for new organizations or projects. In special cases, you can [request an exemption](https://forms.gle/mSgyvY9peo4LLBj67) . If you're unable to access Google Forms, instead email <bq-legacysql-support@google.com> with your organizational ID, current usage levels, recent usage date, migration challenges, and an estimated timeline for transitioning to GoogleSQL.

**Do existing legacy SQL queries stop working?**

Existing queries will continue to work as long as all the legacy SQL features they use were used by at least one project in your organization during the evaluation period. A query might fail if it relies on a feature that was not used during this period, so we recommend that you ensure all critical queries are run.

**Can an existing organization that uses legacy SQL create new projects that also use it?**

Yes. All features that any project in your organization accessed during the evaluation period remain available to all projects, old and new, in your organization.

**Is there a tool to check which legacy SQL features my organization uses?**

There isn't a tool to audit specific feature usage. You can track legacy SQL usage by querying `  INFORMATION_SCHEMA.JOBS  ` views as described in [Legacy SQL query jobs count per project](/bigquery/docs/information-schema-jobs#legacy_sql_query_jobs_count_per_project) . You can also review your query logs in Cloud Logging to check for specific syntax usage.

**Do I have to migrate to GoogleSQL?**

Migration isn't required, but it is encouraged. GoogleSQL is the modern, fully-featured, and recommended dialect.

**What if a rarely used legacy SQL query does not run during the evaluation period?**

To ensure that a query continues to work, run it once during the evaluation period. If you're unable to run it then, you can [request an exemption](https://forms.gle/mSgyvY9peo4LLBj67) . If you're unable to access Google Forms, instead email <bq-legacysql-support@google.com> with your organizational ID, current usage levels, recent usage date, migration challenges, and an estimated timeline for transitioning to GoogleSQL.

## What's next

  - To migrate your queries from legacy SQL to GoogleSQL, see the [migration guide](/bigquery/docs/reference/standard-sql/migrating-from-legacy-sql) .
