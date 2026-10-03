---
name: documents/docs.cloud.google.com/bigquery/docs/legacy-sql-feature-availability
uri: https://docs.cloud.google.com/bigquery/docs/legacy-sql-feature-availability
title: Legacy SQL feature availability
description: Learn about the changes to BigQuery legacy SQL usage restrictions.
data_source: docs.cloud.google.com
---

# Legacy SQL feature availability

This document describes upcoming restrictions to BigQuery legacy SQL availability, which are based on usage during an evaluation period and take effect after June 1, 2026. These changes are part of BigQuery's transition away from legacy SQL to GoogleSQL, the recommended, ANSI-compliant dialect for BigQuery.

Migrating to GoogleSQL offers these benefits over legacy SQL:

- It can be more cost-effective, using the [BigQuery advanced runtime](https://docs.cloud.google.com/bigquery/docs/running-queries#advanced-runtime) for better performance.
- It lets you use features not supported by legacy SQL, such as [DML](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/dml-syntax) and [DDL](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language) statements, Common Table Expressions (CTEs), complex subqueries and join predicates, [materialized views](https://docs.cloud.google.com/bigquery/docs/materialized-views-intro) , [search indexes](https://docs.cloud.google.com/bigquery/docs/search) , and [Generative AI functions](https://docs.cloud.google.com/bigquery/docs/generative-ai-overview) .

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
<li><code>SELECT</code></li>
<li><code>FROM</code></li>
<li><code>JOIN</code></li>
<li><code>WHERE</code></li>
<li><code>GROUP BY</code></li>
<li><code>HAVING</code></li>
<li><code>ORDER BY</code></li>
<li><code>LIMIT</code></li>
</ul></td>
</tr>
<tr class="even">
<td>Expression logic</td>
<td><strong>Literals:</strong>
<ul>
<li><code>TRUE</code></li>
<li><code>FALSE</code></li>
<li><code>NULL</code></li>
</ul>
<br />
<strong>Logical operators:</strong>
<ul>
<li><code>AND</code></li>
<li><code>OR</code></li>
<li><code>NOT</code></li>
</ul>
<br />
<strong>Comparison functions:</strong>
<ul>
<li><code>=</code></li>
<li><code>!=</code></li>
<li><code>&lt;&gt;</code></li>
<li><code>&lt;</code></li>
<li><code>&lt;=</code></li>
<li><code>&gt;</code></li>
<li><code>&gt;=</code></li>
<li><code>IN</code></li>
<li><code>IS NULL</code></li>
<li><code>IS NOT NULL</code></li>
<li><code>IS_EXPLICITLY_DEFINED</code></li>
<li><code>IS_INF</code></li>
<li><code>IS_NAN</code></li>
<li><code>... BETWEEN ... AND ...</code></li>
</ul>
<br />
<strong>Control flow statements:</strong>
<ul>
<li><code>IF</code></li>
<li><code>IFNULL</code></li>
<li><code>CASE WHEN … THEN …</code></li>
</ul></td>
</tr>
<tr class="odd">
<td>Basic operations</td>
<td><strong>Arithmetic operators:</strong>
<ul>
<li><code>+</code></li>
<li><code>-</code></li>
<li><code>*</code></li>
<li><code>/</code></li>
<li><code>%</code></li>
</ul>
<br />
<strong>Basic aggregate functions:</strong>
<ul>
<li><code>AVG</code></li>
<li><code>COUNT</code></li>
<li><code>FIRST</code></li>
<li><code>LAST</code></li>
<li><code>MAX</code></li>
<li><code>MIN</code></li>
<li><code>NTH</code></li>
<li><code>SUM</code></li>
</ul></td>
</tr>
<tr class="even">
<td>Data elements</td>
<td><strong>Basic Data Types:</strong>
<ul>
<li><code>BYTES</code></li>
<li><code>BOOLEAN</code></li>
<li><code>FLOAT</code></li>
<li><code>INTEGER</code></li>
<li><code>STRING</code></li>
<li><code>TIMESTAMP</code></li>
</ul>
<br />
<strong>Structured and partially supported data types:</strong>
<ul>
<li>Exact Numeric: <code>NUMERIC</code> , <code>BIGNUMERIC</code></li>
<li>Civil Time: <code>DATE</code> , <code>TIME</code> , <code>DATETIME</code></li>
<li>Structured Fields: Nested fields, repeated fields</li>
</ul>
<br />
<strong>Casting Functions:</strong>
<ul>
<li><code>CAST(expr AS type)</code></li>
<li><code>BOOLEAN</code></li>
<li><code>BYTES</code></li>
<li><code>FLOAT</code></li>
<li><code>INTEGER</code></li>
<li><code>STRING</code></li>
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
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/legacy-sql#comma-as-union-all">Comma as <code>UNION ALL</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/legacy-sql#flatten-operator">Explicit <code>FLATTEN</code> operator</a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/legacy-sql#each"><code>GROUP BY</code> with <code>EACH</code> modifier</a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/legacy-sql#stringfunctions"><code>IGNORE CASE</code> modifier</a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/legacy-sql#each-modifier"><code>JOIN</code> with <code>EACH</code> modifier</a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/migrating-from-legacy-sql#logical_views">Logical views</a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/legacy-sql#omit"><code>OMIT … IF</code> clause</a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/legacy-sql#semi-joins">Semi-join or Anti-join</a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/legacy-sql#from-tables">Table decorator - Partition</a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/table-decorators#range_decorators">Table decorator - Range</a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/table-decorators#time_decorators">Table decorator - Time</a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/user-defined-functions-legacy">User-defined functions</a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/legacy-sql#table-date-range">Wildcard - <code>TABLE_DATE_RANGE</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/legacy-sql#table-date-range-strict">Wildcard - <code>TABLE_DATE_RANGE_STRICT</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/legacy-sql#table-query">Wildcard - <code>TABLE_QUERY</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/legacy-sql#within"><code>WITHIN</code> modifier for aggregate functions</a></li>
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
<li><code>CUME_DIST</code></li>
<li><code>DENSE_RANK</code></li>
<li><code>FIRST_VALUE</code></li>
<li><code>LAG</code></li>
<li><code>LAST_VALUE</code></li>
<li><code>LEAD</code></li>
<li><code>NTH_VALUE</code></li>
<li><code>NTILE</code></li>
<li><code>PERCENT_RANK</code></li>
<li><code>PERCENTILE_CONT</code></li>
<li><code>PERCENTILE_DISC</code></li>
<li><code>RANK</code></li>
<li><code>RATIO_TO_REPORT</code></li>
<li><code>ROW_NUMBER</code></li>
</ul></td>
</tr>
<tr class="even">
<td>Aggregate functions for statistics</td>
<td><ul>
<li><code>CORR</code></li>
<li><code>COVAR_POP</code></li>
<li><code>COVAR_SAMP</code></li>
<li><code>STDDEV</code></li>
<li><code>STDDEV_POP</code></li>
<li><code>STDDEV_SAMP</code></li>
<li><code>VARIANCE</code></li>
<li><code>VAR_POP</code></li>
<li><code>VAR_SAMP</code></li>
</ul></td>
</tr>
<tr class="odd">
<td>Aggregate functions returning repeated field</td>
<td><ul>
<li><code>NEST</code></li>
<li><code>QUANTILES</code></li>
<li><code>UNIQUE</code></li>
</ul></td>
</tr>
<tr class="even">
<td>Aggregate functions with bits operations</td>
<td><ul>
<li><code>BIT_AND</code></li>
<li><code>BIT_OR</code></li>
<li><code>BIT_XOR</code></li>
</ul></td>
</tr>
<tr class="odd">
<td>Aggregate functions with concatenation</td>
<td><ul>
<li><code>GROUP_CONCAT</code></li>
<li><code>GROUP_CONCAT_UNQUOTED</code></li>
</ul></td>
</tr>
<tr class="even">
<td>Aggregate functions with sort</td>
<td><ul>
<li><code>COUNT([DISTINCT])</code></li>
<li><code>EXACT_COUNT_DISTINCT</code></li>
<li><code>TOP ... COUNT(*)</code></li>
</ul></td>
</tr>
<tr class="odd">
<td>Basic window functions</td>
<td><ul>
<li><code>AVG</code></li>
<li><code>COUNT(*)</code></li>
<li><code>COUNT([DISTINCT])</code></li>
<li><code>MAX</code></li>
<li><code>MIN</code></li>
<li><code>STDDEV</code></li>
<li><code>SUM</code></li>
</ul></td>
</tr>
<tr class="even">
<td>Bitwise functions</td>
<td><ul>
<li><code>&amp;</code></li>
<li><code>|</code></li>
<li><code>^</code></li>
<li><code>&lt;&lt;</code></li>
<li><code>&gt;&gt;</code></li>
<li><code>~</code></li>
<li><code>BIT_COUNT</code></li>
</ul></td>
</tr>
<tr class="odd">
<td>Conditional expressions</td>
<td><ul>
<li><code>COALESCE</code></li>
<li><code>EVERY</code></li>
<li><code>GREATEST</code></li>
<li><code>LEAST</code></li>
<li><code>NVL</code></li>
<li><code>SOME</code></li>
</ul></td>
</tr>
<tr class="even">
<td>Conversion functions</td>
<td><ul>
<li><code>FROM_BASE64</code></li>
<li><code>HEX_STRING</code></li>
<li><code>TO_BASE64</code></li>
</ul></td>
</tr>
<tr class="odd">
<td>Current time functions</td>
<td><ul>
<li><code>NOW</code></li>
<li><code>CURRENT_DATE</code></li>
<li><code>CURRENT_TIME</code></li>
<li><code>CURRENT_TIMESTAMP</code></li>
</ul></td>
</tr>
<tr class="even">
<td>Current user functions</td>
<td><ul>
<li><code>CURRENT_USER</code></li>
</ul></td>
</tr>
<tr class="odd">
<td>Date and time functions</td>
<td><ul>
<li><code>DATE</code></li>
<li><code>DATE_ADD</code></li>
<li><code>DATEDIFF</code></li>
<li><code>TIME</code></li>
<li><code>TIMESTAMP</code></li>
</ul></td>
</tr>
<tr class="even">
<td>Function RAND</td>
<td><ul>
<li><code>RAND</code></li>
</ul></td>
</tr>
<tr class="odd">
<td>Functions returning repeated field</td>
<td><ul>
<li><code>POSITION</code></li>
<li><code>SPLIT</code></li>
</ul></td>
</tr>
<tr class="even">
<td>Hashing functions</td>
<td><ul>
<li><code>HASH</code></li>
<li><code>SHA1</code></li>
<li><code>FARM_FINGERPRINT</code></li>
</ul></td>
</tr>
<tr class="odd">
<td>IP functions</td>
<td><ul>
<li><code>FORMAT_IP</code></li>
<li><code>FORMAT_PACKED_IP</code></li>
<li><code>PARSE_IP</code></li>
<li><code>PARSE_PACKED_IP</code></li>
</ul></td>
</tr>
<tr class="even">
<td>JSON functions</td>
<td><ul>
<li><code>JSON_EXTRACT</code></li>
<li><code>JSON_EXTRACT_SCALAR</code></li>
</ul></td>
</tr>
<tr class="odd">
<td>Mathematical functions</td>
<td><ul>
<li><code>ABS</code></li>
<li><code>ACOS</code></li>
<li><code>ASIN</code></li>
<li><code>ATAN</code></li>
<li><code>ATAN2</code></li>
<li><code>CEIL</code></li>
<li><code>COS</code></li>
<li><code>DEGREES</code></li>
<li><code>EXP</code></li>
<li><code>FLOOR</code></li>
<li><code>LN</code></li>
<li><code>LOG</code></li>
<li><code>LOG10</code></li>
<li><code>LOG2</code></li>
<li><code>PI</code></li>
<li><code>POW</code></li>
<li><code>RADIANS</code></li>
<li><code>ROUND</code></li>
<li><code>SIN</code></li>
<li><code>SQRT</code></li>
<li><code>TAN</code></li>
</ul></td>
</tr>
<tr class="even">
<td>Mathematical hyperbolic functions</td>
<td><ul>
<li><code>ACOSH</code></li>
<li><code>ASINH</code></li>
<li><code>ATANH</code></li>
<li><code>COSH</code></li>
<li><code>SINH</code></li>
<li><code>TANH</code></li>
</ul></td>
</tr>
<tr class="odd">
<td>Part of TIMESTAMP functions</td>
<td><ul>
<li><code>DAY</code></li>
<li><code>DAYOFWEEK</code></li>
<li><code>DAYOFYEAR</code></li>
<li><code>HOUR</code></li>
<li><code>MINUTE</code></li>
<li><code>MONTH</code></li>
<li><code>QUARTER</code></li>
<li><code>SECOND</code></li>
<li><code>WEEK</code></li>
<li><code>YEAR</code></li>
</ul></td>
</tr>
<tr class="even">
<td>Regular expression functions</td>
<td><ul>
<li><code>REGEXP_MATCH</code></li>
<li><code>REGEXP_EXTRACT</code></li>
<li><code>REGEXP_REPLACE</code></li>
</ul></td>
</tr>
<tr class="odd">
<td>String functions</td>
<td><ul>
<li><code>CONTAINS</code></li>
<li><code>CONCAT</code></li>
<li><code>INSTR</code></li>
<li><code>LEFT</code></li>
<li><code>LENGTH</code></li>
<li><code>LOWER</code></li>
<li><code>LPAD</code></li>
<li><code>LTRIM</code></li>
<li><code>REPLACE</code></li>
<li><code>RIGHT</code></li>
<li><code>RPAD</code></li>
<li><code>RTRIM</code></li>
<li><code>SUBSTR</code></li>
<li><code>UPPER</code></li>
</ul></td>
</tr>
<tr class="even">
<td>URL functions</td>
<td><ul>
<li><code>HOST</code></li>
<li><code>DOMAIN</code></li>
<li><code>TLD</code></li>
</ul></td>
</tr>
<tr class="odd">
<td>UNIX timestamp functions</td>
<td><ul>
<li><code>FORMAT_UTC_USEC</code></li>
<li><code>MSEC_TO_TIMESTAMP</code></li>
<li><code>PARSE_UTC_USEC</code></li>
<li><code>SEC_TO_TIMESTAMP</code></li>
<li><code>STRFTIME_UTC_USEC</code></li>
<li><code>TIMESTAMP_TO_SEC</code></li>
<li><code>TIMESTAMP_TO_MSEC</code></li>
<li><code>TIMESTAMP_TO_USEC</code></li>
<li><code>USEC_TO_TIMESTAMP</code></li>
<li><code>UTC_USEC_TO_DAY</code></li>
<li><code>UTC_USEC_TO_HOUR</code></li>
<li><code>UTC_USEC_TO_MONTH</code></li>
<li><code>UTC_USEC_TO_WEEK</code></li>
<li><code>UTC_USEC_TO_YEAR</code></li>
</ul></td>
</tr>
</tbody>
</table>

## Examples of feature availability

The following examples demonstrate how feature availability works.

### Example: Accessing basic language capabilities

A project runs a legacy SQL query during the evaluation period. Assume table `T` contains a column `X` of type `INTEGER` .

```
#legacySQL
SELECT X FROM T
```

This usage ensures that all projects within the organization retain the ability to run queries that use any feature from the basic language capabilities set. For example, the following query continues to work:

```
#legacySQL
SELECT X FROM T WHERE X > 10
```

### Example: Using function groupings

A project uses one function from a specific function grouping. Assume table `T` contains a column `X` of type `FLOAT` .

```
#legacySQL
SELECT SIN(X) FROM T
```

The use of the `SIN()` function makes the entire mathematical functions grouping available. Consequently, all projects within the organization can use any other function from that grouping, such as `COS()` .

```
#legacySQL
SELECT COS(X) FROM T
```

Conversely, the following query fails after the evaluation period if no project in the organization uses any function from the aggregate functions for statistics grouping.

```
#legacySQL
SELECT STDDEV(X) FROM T
```

### Example: Feature retention across different tables

Assume table `X` has a column `A` ( `INTEGER` ) and table `Y` has column `B` ( `FLOAT` ). A project runs the following query during the evaluation period:

```
#legacySQL
SELECT SIN(A) FROM X
```

The organization can run the following query after the evaluation period ends. The query works because the mathematical functions feature was retained by the first query. The retention is independent of the specific table, column name, or data type used, as both `INTEGER` and `FLOAT` are part of the basic language capability.

```
#legacySQL
SELECT COS(B) FROM Y
```

### Example: Complex query

Assume table `T` contains a column `X` of type `STRING` . A project runs the following query during the evaluation period:

```
#legacySQL
SELECT value, AVG(FLOAT(value)) OVER (ORDER BY value) AS avg
 FROM (
  SELECT LENGTH(SPLIT(X, ',')) AS value
    FROM T
)
```

This query uses features from the basic language capabilities and three function groupings: basic window functions, string functions, and functions returning repeated values. All projects within the organization retain these features. Therefore, a new query that uses a different combination of functions from those same retained feature sets succeeds.

```
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

There isn't a tool to audit specific feature usage. You can track legacy SQL usage by querying `INFORMATION_SCHEMA.JOBS` views as described in [Legacy SQL query jobs count per project](https://docs.cloud.google.com/bigquery/docs/information-schema-jobs#legacy_sql_query_jobs_count_per_project) . You can also review your query logs in Cloud Logging to check for specific syntax usage.

**Do I have to migrate to GoogleSQL?**

Migration isn't required, but it is encouraged. GoogleSQL is the modern, fully-featured, and recommended dialect.

**What if a rarely used legacy SQL query does not run during the evaluation period?**

To ensure that a query continues to work, run it once during the evaluation period. If you're unable to run it then, you can [request an exemption](https://forms.gle/mSgyvY9peo4LLBj67) . If you're unable to access Google Forms, instead email <bq-legacysql-support@google.com> with your organizational ID, current usage levels, recent usage date, migration challenges, and an estimated timeline for transitioning to GoogleSQL.

## What's next

- To migrate your queries from legacy SQL to GoogleSQL, see the [migration guide](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/migrating-from-legacy-sql) .
