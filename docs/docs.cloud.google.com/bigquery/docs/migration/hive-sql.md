# Apache Hive SQL translation guide

This document details the similarities and differences in SQL syntax between Apache Hive and BigQuery to help you plan your migration. To migrate your SQL scripts in bulk, use [batch SQL translation](/bigquery/docs/batch-sql-translator) . To translate ad hoc queries, use [interactive SQL translation](/bigquery/docs/interactive-sql-translator) .

In some cases, there's no direct mapping between a SQL element in Hive and BigQuery. However, in most cases, BigQuery offers an alternative element to Hive to help you achieve the same functionality, as shown in the examples in this document.

The intended audience for this document is enterprise architects, database administrators, application developers, and IT security specialists. It assumes that you're familiar with Hive.

## Data types

Hive and BigQuery have different data type systems. In most cases, you can map data types in Hive to [BigQuery data types](/bigquery/docs/reference/standard-sql/data-types) with a few exceptions, such as `  MAP  ` and `  UNION  ` . Hive supports more implicit type casting than BigQuery. As a result, the batch SQL translator inserts many explicit casts.

<table>
<thead>
<tr class="header">
<th><strong>Hive</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       TINYINT      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       SMALLINT      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       INT      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       BIGINT      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       DECIMAL      </code></td>
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       FLOAT      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       DOUBLE      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       BOOLEAN      </code></td>
<td><code dir="ltr" translate="no">       BOOL      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       VARCHAR      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       CHAR      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       BINARY      </code></td>
<td><code dir="ltr" translate="no">       BYTES      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       DATE      </code></td>
<td><code dir="ltr" translate="no">       DATE      </code></td>
</tr>
<tr class="even">
<td>-</td>
<td><code dir="ltr" translate="no">       DATETIME      </code></td>
</tr>
<tr class="odd">
<td>-</td>
<td><code dir="ltr" translate="no">       TIME      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td><code dir="ltr" translate="no">       DATETIME/TIMESTAMP      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       INTERVAL      </code></td>
<td>-</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ARRAY      </code></td>
<td><code dir="ltr" translate="no">       ARRAY      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       STRUCT      </code></td>
<td><code dir="ltr" translate="no">       STRUCT      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       MAPS      </code></td>
<td><code dir="ltr" translate="no">       STRUCT      </code> with key values ( <code dir="ltr" translate="no">       REPEAT      </code> field)</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       UNION      </code></td>
<td><code dir="ltr" translate="no">       STRUCT      </code> with different types</td>
</tr>
<tr class="even">
<td>-</td>
<td><code dir="ltr" translate="no">       GEOGRAPHY      </code></td>
</tr>
<tr class="odd">
<td>-</td>
<td><code dir="ltr" translate="no">       JSON      </code></td>
</tr>
</tbody>
</table>

## Query syntax

This section addresses differences in query syntax between Hive and BigQuery.

### `     SELECT    ` statement

Most Hive [`  SELECT  `](https://cwiki.apache.org/confluence/display/hive/languagemanual+select#LanguageManualSelect-SelectSyntax) statements are compatible with BigQuery. The following table contains a list of minor differences:

<table>
<thead>
<tr class="header">
<th><strong>Case</strong></th>
<th><strong>Hive</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Subquery</td>
<td><p><code dir="ltr" translate="no">        SELECT * FROM (                SELECT 10 as col1, "test" as col2, "test" as col3                ) tmp_table;       </code></p></td>
<td><p><code dir="ltr" translate="no">        SELECT * FROM (                SELECT 10 as col1, "test" as col2, "test" as col3                );       </code></p></td>
</tr>
<tr class="even">
<td>Column filtering</td>
<td><p><code dir="ltr" translate="no">        SET hive.support.quoted.identifiers=none;                SELECT `(col2|col3)?+.+` FROM (                SELECT 10 as col1, "test" as col2, "test" as col3                ) tmp_table;       </code></p></td>
<td><p><code dir="ltr" translate="no">        SELECT * EXCEPT(col2,col3) FROM (                SELECT 10 as col1, "test" as col2, "test" as col3                );       </code></p></td>
</tr>
<tr class="odd">
<td>Exploding an array</td>
<td><p><code dir="ltr" translate="no">        SELECT tmp_table.pageid, adid FROM (                SELECT 'test_value' pageid,  Array(1,2,3) ad_id) tmp_table                LATERAL VIEW                explode(tmp_table.ad_id) adTable AS adid;       </code></p></td>
<td><p><code dir="ltr" translate="no">        SELECT tmp_table.pageid, ad_id FROM (                SELECT 'test_value' pageid, [1,2,3] ad_id) tmp_table,                UNNEST(tmp_table.ad_id) ad_id;       </code></p></td>
</tr>
</tbody>
</table>

### `     FROM    ` clause

The `  FROM  ` clause in a query lists the table references from which data is selected. In Hive, possible table references include tables, views, and subqueries. BigQuery also supports all these table references.

You can reference BigQuery tables in the `  FROM  ` clause by using the following:

  - `  [project_id].[dataset_id].[table_name]  `
  - `  [dataset_id].[table_name]  `
  - `  [table_name]  `

BigQuery also supports [additional table references](/bigquery/docs/reference/standard-sql/query-syntax#from_clause) :

  - Historical versions of the table definition and rows using [`  FOR SYSTEM_TIME AS OF  `](/bigquery/docs/reference/standard-sql/query-syntax#for_system_time_as_of)
  - [Field paths](/bigquery/docs/reference/standard-sql/query-syntax#field_path) , or any path that resolves to a field within a data type (such as a `  STRUCT  ` )
  - [Flattened arrays](/bigquery/docs/arrays#querying_nested_arrays)

### Comparison operators

The following table provides details about converting operators from Hive to BigQuery:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Function or operator</strong></th>
<th><strong>Hive</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       -      </code> Unary minus<br />
<code dir="ltr" translate="no">       *      </code> Multiplication<br />
<code dir="ltr" translate="no">       /      </code> Division<br />
<code dir="ltr" translate="no">       +      </code> Addition<br />
<code dir="ltr" translate="no">       -      </code> Subtraction</td>
<td>All <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Types#LanguageManualTypes-NumericTypes" class="external">number types</a></td>
<td>All <a href="/bigquery/docs/reference/standard-sql/data-types#numeric_types">number types</a> .<br />

<p>To prevent errors during the divide operation, consider using <code dir="ltr" translate="no">          SAFE_DIVIDE        </code> or <code dir="ltr" translate="no">          IEEE_DIVIDE        </code> .</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ~      </code> Bitwise not<br />
<code dir="ltr" translate="no">       |      </code> Bitwise OR<br />
<code dir="ltr" translate="no">       &amp;      </code> Bitwise AND<br />
<code dir="ltr" translate="no">       ^      </code> Bitwise XOR</td>
<td>Boolean data type</td>
<td>Boolean data type.</td>
</tr>
<tr class="odd">
<td>Left shift</td>
<td><p><code dir="ltr" translate="no">        shiftleft(TINYINT|SMALLINT|INT a, INT b)                shiftleft(BIGINT a, INT b)       </code></p></td>
<td><p><code dir="ltr" translate="no">        &lt;&lt;       </code> Integer or bytes</p>
<p><code dir="ltr" translate="no">        A &lt;&lt; B       </code> , where <code dir="ltr" translate="no">        B       </code> must be same type as <code dir="ltr" translate="no">        A       </code></p></td>
</tr>
<tr class="even">
<td>Right shift</td>
<td><p><code dir="ltr" translate="no">        shiftright(TINYINT|SMALLINT|INT a, INT b)                shiftright(BIGINT a, INT b)       </code></p></td>
<td><p><code dir="ltr" translate="no">        &gt;&gt;       </code> Integer or bytes</p>
<p><code dir="ltr" translate="no">        A &gt;&gt; B       </code> , where <code dir="ltr" translate="no">        B       </code> must be same type as <code dir="ltr" translate="no">        A       </code></p></td>
</tr>
<tr class="odd">
<td>Modulus (remainder)</td>
<td><code dir="ltr" translate="no">       X % Y      </code><br />

<p>All <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Types#LanguageManualTypes-NumericTypes" class="external">number types</a></p></td>
<td><code dir="ltr" translate="no">       MOD(X, Y)      </code></td>
</tr>
<tr class="even">
<td>Integer division</td>
<td><code dir="ltr" translate="no">       A DIV B      </code> and <code dir="ltr" translate="no">       A/B      </code> for detailed precision</td>
<td>All <a href="/bigquery/docs/reference/standard-sql/data-types#numeric_types">number types</a> .<br />

<p>Note: To prevent errors during the divide operation, consider using <code dir="ltr" translate="no">          SAFE_DIVIDE        </code> or <code dir="ltr" translate="no">          IEEE_DIVIDE        </code> .</p></td>
</tr>
<tr class="odd">
<td>Unary negation</td>
<td><code dir="ltr" translate="no">       !      </code> , <code dir="ltr" translate="no">       NOT      </code></td>
<td><code dir="ltr" translate="no">       NOT      </code></td>
</tr>
<tr class="even">
<td>Types supporting equality comparisons</td>
<td>All <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Types#LanguageManualTypes-Overview" class="external">primitive types</a></td>
<td>All <a href="/bigquery/docs/reference/standard-sql/data-types">comparable types and <code dir="ltr" translate="no">        STRUCT       </code></a> .</td>
</tr>
<tr class="odd">
<td></td>
<td><code dir="ltr" translate="no">       a &lt;=&gt; b      </code></td>
<td>Not supported. Translate to the following:<br />

<p><code dir="ltr" translate="no">        (a = b AND b IS NOT NULL OR a IS NULL)       </code></p></td>
</tr>
<tr class="even">
<td></td>
<td><code dir="ltr" translate="no">       a &lt;&gt; b      </code></td>
<td>Not supported. Translate to the following:<br />

<p><code dir="ltr" translate="no">        NOT (a = b AND b IS NOT NULL OR a IS NULL)       </code></p></td>
</tr>
<tr class="odd">
<td>Relational operators ( <code dir="ltr" translate="no">       =, ==, !=, &lt;, &gt;, &gt;=      </code> )</td>
<td>All <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-RelationalOperators" class="external">primitive types</a></td>
<td>All <a href="/bigquery/docs/reference/standard-sql/operators#comparison_operators">comparable types</a> .</td>
</tr>
<tr class="even">
<td>String comparison</td>
<td><code dir="ltr" translate="no">       RLIKE      </code> , <code dir="ltr" translate="no">       REGEXP      </code></td>
<td><code dir="ltr" translate="no">       REGEXP_CONTAINS      </code> built-in function. Uses BigQuery <a href="https://github.com/google/re2/wiki/Syntax" class="external">regex syntax for string functions</a> for the regular expression patterns.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       [NOT] LIKE, [NOT] BETWEEN, IS [NOT] NULL      </code></td>
<td><code dir="ltr" translate="no">       A [NOT] BETWEEN B AND C, A IS [NOT] (TRUE|FALSE), A [NOT] LIKE B      </code></td>
<td>Same as Hive. In addition, BigQuery also supports the <a href="/bigquery/docs/reference/standard-sql/operators#in_operators"><code dir="ltr" translate="no">        IN       </code> operator</a> .</td>
</tr>
</tbody>
</table>

### JOIN conditions

Both Hive and BigQuery support the following types of joins:

  - `  [INNER] JOIN  `

  - `  LEFT [OUTER] JOIN  `

  - `  RIGHT [OUTER] JOIN  `

  - `  FULL [OUTER] JOIN  `

  - `  CROSS JOIN  ` and the equivalent implicit [comma cross join](/bigquery/docs/reference/standard-sql/query-syntax#cross_join)

For more information, see [Join operation](/bigquery/docs/reference/standard-sql/query-syntax#join_types) and [Hive joins](https://cwiki.apache.org/confluence/display/hive/languagemanual+joins) .

### Type conversion and casting

The following table provides details about converting functions from Hive to BigQuery:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Function or operator</strong></th>
<th><strong>Hive</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Type casting</td>
<td>When a cast fails, `NULL` is returned.</td>
<td><p>Same syntax as Hive. For more information about BigQuery type conversion rules, see <a href="/bigquery/docs/reference/standard-sql/conversion_rules">Conversion rules</a> .</p>
<p>If cast fails, you see an error. To have the same behavior as Hive, use <code dir="ltr" translate="no">        SAFE_CAST       </code> instead.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       SAFE      </code> function calls</td>
<td></td>
<td>If you prefix function calls with <a href="/bigquery/docs/reference/standard-sql/functions-reference#safe_prefix"><code dir="ltr" translate="no">        SAFE       </code></a> , the function returns <code dir="ltr" translate="no">       NULL      </code> instead of reporting failure. For example, <code dir="ltr" translate="no">       SAFE.SUBSTR('foo', 0, -2) AS safe_output;      </code> returns <code dir="ltr" translate="no">       NULL      </code> .<br />

<p>Note: When casting safely without errors, use <code dir="ltr" translate="no">        SAFE_CAST       </code> .</p></td>
</tr>
</tbody>
</table>

#### Implicit conversion types

When migrating to BigQuery, you need to convert most of your [Hive implicit conversions](https://cwiki.apache.org/confluence/display/hive/languagemanual+types#LanguageManualTypes-AllowedImplicitConversions) to BigQuery explicit conversions except for the following data types, which BigQuery implicitly converts.

<table>
<thead>
<tr class="header">
<th><strong>From BigQuery type</strong></th>
<th><strong>To BigQuery type</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code> , <code dir="ltr" translate="no">       NUMERIC      </code> , <code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code> , <code dir="ltr" translate="no">       FLOAT64      </code></td>
</tr>
</tbody>
</table>

BigQuery also performs implicit conversions for the following literals:

<table>
<thead>
<tr class="header">
<th><strong>From BigQuery type</strong></th>
<th><strong>To BigQuery type</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       STRING      </code> literal (for example, <code dir="ltr" translate="no">       "2008-12-25"      </code> )</td>
<td><code dir="ltr" translate="no">       DATE      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       STRING      </code> literal (for example, <code dir="ltr" translate="no">       "2008-12-25 15:30:00"      </code> )</td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       STRING      </code> literal (for example, <code dir="ltr" translate="no">       "2008-12-25T07:30:00"      </code> )</td>
<td><code dir="ltr" translate="no">       DATETIME      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       STRING      </code> literal (for example, <code dir="ltr" translate="no">       "15:30:00"      </code> )</td>
<td><code dir="ltr" translate="no">       TIME      </code></td>
</tr>
</tbody>
</table>

#### Explicit conversion types

If you want to convert Hive data types that BigQuery doesn't implicitly convert, use the BigQuery [`  CAST(expression AS type)  ` function](/bigquery/docs/reference/standard-sql/conversion_functions#cast) .

## Functions

This section covers common functions used in Hive and BigQuery.

### Aggregate functions

The following table shows mappings between common Hive aggregate, statistical aggregate, and approximate aggregate functions with their BigQuery equivalents:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Hive</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       count(DISTINCT expr[, expr...])      </code></td>
<td><code dir="ltr" translate="no">       count(DISTINCT expr[, expr...])      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       percentile_approx(DOUBLE col, array(p1 [, p2]...) [, B]) WITHIN GROUP (ORDER BY expression)      </code></td>
<td><code dir="ltr" translate="no">         APPROX_QUANTILES              (expression, 100)[OFFSET(CAST(TRUNC(percentile * 100) as INT64))]      </code><br />

<p>BigQuery doesn't support the rest of the arguments that Hive defines.</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         AVG       </code></td>
<td><code dir="ltr" translate="no">       AVG      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         X | Y       </code></td>
<td><code dir="ltr" translate="no">         BIT_OR              / X | Y      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         X ^ Y       </code></td>
<td><code dir="ltr" translate="no">         BIT_XOR              / X ^ Y      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         X &amp; Y       </code></td>
<td><code dir="ltr" translate="no">         BIT_AND              / X &amp; Y      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         COUNT       </code></td>
<td><code dir="ltr" translate="no">       COUNT      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       COLLECT_SET(col), \ COLLECT_LIST(col      </code> )</td>
<td><code dir="ltr" translate="no">         ARRAY_AGG              (col)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         COUNT       </code></td>
<td><code dir="ltr" translate="no">         COUNT       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       MAX      </code></td>
<td><code dir="ltr" translate="no">         MAX       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       MIN      </code></td>
<td><code dir="ltr" translate="no">         MIN       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       REGR_AVGX      </code></td>
<td><code dir="ltr" translate="no">       AVG(      </code>
<p><code dir="ltr" translate="no">        IF(dep_var_expr is NULL       </code></p>
<p><code dir="ltr" translate="no">        OR ind_var_expr is NULL,       </code></p>
<p><code dir="ltr" translate="no">        NULL, ind_var_expr)       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       REGR_AVGY      </code></td>
<td><code dir="ltr" translate="no">       AVG(      </code>
<p><code dir="ltr" translate="no">        IF(dep_var_expr is NULL       </code></p>
<p><code dir="ltr" translate="no">        OR ind_var_expr is NULL,       </code></p>
<p><code dir="ltr" translate="no">        NULL, dep_var_expr)       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       REGR_COUNT      </code></td>
<td><code dir="ltr" translate="no">       SUM(      </code>
<p><code dir="ltr" translate="no">        IF(dep_var_expr is NULL       </code></p>
<p><code dir="ltr" translate="no">        OR ind_var_expr is NULL,       </code></p>
<p><code dir="ltr" translate="no">        NULL, 1)       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       REGR_INTERCEPT      </code></td>
<td><code dir="ltr" translate="no">       AVG(dep_var_expr)      </code>
<p><code dir="ltr" translate="no">        - AVG(ind_var_expr)       </code></p>
<p><code dir="ltr" translate="no">        * (COVAR_SAMP(ind_var_expr,dep_var_expr)       </code></p>
<p><code dir="ltr" translate="no">        / VARIANCE(ind_var_expr)       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       REGR_R2      </code></td>
<td><code dir="ltr" translate="no">       (COUNT(dep_var_expr) *      </code>
<p><code dir="ltr" translate="no">        SUM(ind_var_expr * dep_var_expr) -       </code></p>
<p><code dir="ltr" translate="no">        SUM(dep_var_expr) * SUM(ind_var_expr))       </code></p>
<p><code dir="ltr" translate="no">        / SQRT(       </code></p>
<p><code dir="ltr" translate="no">        (COUNT(ind_var_expr) *       </code></p>
<p><code dir="ltr" translate="no">        SUM(POWER(ind_var_expr, 2)) *       </code></p>
<p><code dir="ltr" translate="no">        POWER(SUM(ind_var_expr),2)) *       </code></p>
<p><code dir="ltr" translate="no">        (COUNT(dep_var_expr) *       </code></p>
<p><code dir="ltr" translate="no">        SUM(POWER(dep_var_expr, 2)) *       </code></p>
<p><code dir="ltr" translate="no">        POWER(SUM(dep_var_expr), 2)))       </code></p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       REGR_SLOPE      </code></td>
<td><code dir="ltr" translate="no">       COVAR_SAMP(ind_var_expr,      </code>
<p><code dir="ltr" translate="no">        dep_var_expr)       </code></p>
<p><code dir="ltr" translate="no">        / VARIANCE(ind_var_expr)       </code></p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       REGR_SXX      </code></td>
<td><code dir="ltr" translate="no">       SUM(POWER(ind_var_expr, 2)) - COUNT(ind_var_expr) * POWER(AVG(ind_var_expr),2)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       REGR_SXY      </code></td>
<td><code dir="ltr" translate="no">       SUM(ind_var_expr*dep_var_expr) - COUNT(ind_var_expr) * AVG(ind) * AVG(dep_var_expr)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       REGR_SYY      </code></td>
<td><code dir="ltr" translate="no">       SUM(POWER(dep_var_expr, 2)) - COUNT(dep_var_expr) * POWER(AVG(dep_var_expr),2)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         ROLLUP       </code></td>
<td><code dir="ltr" translate="no">         ROLLUP       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       STDDEV_POP      </code></td>
<td><code dir="ltr" translate="no">       STDDEV_POP      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       STDDEV_SAMP      </code></td>
<td><code dir="ltr" translate="no">       STDDEV_SAMP, STDDEV      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       SUM      </code></td>
<td><code dir="ltr" translate="no">       SUM      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       VAR_POP      </code></td>
<td><code dir="ltr" translate="no">       VAR_POP      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       VAR_SAMP      </code></td>
<td><code dir="ltr" translate="no">       VAR_SAMP, VARIANCE      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       CONCAT_WS      </code></td>
<td><code dir="ltr" translate="no">         STRING_AGG       </code></td>
</tr>
</tbody>
</table>

### Analytical functions

The following table shows mappings between common Hive analytical functions with their BigQuery equivalents:

<table>
<thead>
<tr class="header">
<th><strong>Hive</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       AVG      </code></td>
<td><code dir="ltr" translate="no">         AVG       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       COUNT      </code></td>
<td><code dir="ltr" translate="no">         COUNT       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       COVAR_POP      </code></td>
<td><code dir="ltr" translate="no">         COVAR_POP       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       COVAR_SAMP      </code></td>
<td><code dir="ltr" translate="no">         COVAR_SAMP       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       CUME_DIST      </code></td>
<td><code dir="ltr" translate="no">         CUME_DIST       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       DENSE_RANK      </code></td>
<td><code dir="ltr" translate="no">         DENSE_RANK       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         FIRST_VALUE       </code></td>
<td><code dir="ltr" translate="no">         FIRST_VALUE       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       LAST_VALUE      </code></td>
<td><code dir="ltr" translate="no">         LAST_VALUE       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       LAG      </code></td>
<td><code dir="ltr" translate="no">         LAG       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       LEAD      </code></td>
<td><code dir="ltr" translate="no">         LEAD       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       COLLECT_LIST, \ COLLECT_SET      </code></td>
<td><code dir="ltr" translate="no">         ARRAY_AGG       </code> <code dir="ltr" translate="no">         ARRAY_CONCAT_AGG       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       MAX      </code></td>
<td><code dir="ltr" translate="no">         MAX       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       MIN      </code></td>
<td><code dir="ltr" translate="no">         MIN       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       NTILE      </code></td>
<td><code dir="ltr" translate="no">         NTILE              (constant_integer_expression)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         PERCENT_RANK       </code></td>
<td><code dir="ltr" translate="no">         PERCENT_RANK       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       RANK ()      </code></td>
<td><code dir="ltr" translate="no">         RANK       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       ROW_NUMBER      </code></td>
<td><code dir="ltr" translate="no">         ROW_NUMBER       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       STDDEV_POP      </code></td>
<td><code dir="ltr" translate="no">         STDDEV_POP       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       STDDEV_SAMP      </code></td>
<td><code dir="ltr" translate="no">         STDDEV_SAMP              ,               STDDEV       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       SUM      </code></td>
<td><code dir="ltr" translate="no">         SUM       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       VAR_POP      </code></td>
<td><code dir="ltr" translate="no">         VAR_POP       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       VAR_SAMP      </code></td>
<td><code dir="ltr" translate="no">         VAR_SAMP              ,               VARIANCE       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       VARIANCE      </code></td>
<td><code dir="ltr" translate="no">         VARIANCE ()       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         WIDTH_BUCKET       </code></td>
<td>A user-defined function (UDF) can be used.</td>
</tr>
</tbody>
</table>

### Date and time functions

The following table shows mappings between common Hive date and time functions and their BigQuery equivalents:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       DATE_ADD      </code></td>
<td><code dir="ltr" translate="no">         DATE_ADD(date_expression, INTERVAL int64_expression date_part)       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       DATE_SUB      </code></td>
<td><code dir="ltr" translate="no">         DATE_SUB(date_expression, INTERVAL int64_expression date_part)       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       CURRENT_DATE      </code></td>
<td><code dir="ltr" translate="no">         CURRENT_DATE       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       CURRENT_TIME      </code></td>
<td><code dir="ltr" translate="no">         CURRENT_TIME       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       CURRENT_TIMESTAMP      </code></td>
<td><code dir="ltr" translate="no">         CURRENT_DATETIME       </code> is recommended, as this value is timezone-free and synonymous with <code dir="ltr" translate="no">       CURRENT_TIMESTAMP      </code> \ <code dir="ltr" translate="no">         CURRENT_TIMESTAMP       </code> in Hive.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       EXTRACT(field FROM source)      </code></td>
<td><code dir="ltr" translate="no">         EXTRACT(part FROM datetime_expression)       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       LAST_DAY      </code></td>
<td><code dir="ltr" translate="no">       DATE_SUB( DATE_TRUNC( DATE_ADD(       </code>
<p>date_expression, INTERVAL 1 MONTH</p>
<p><code dir="ltr" translate="no">        ), MONTH ), INTERVAL 1 DAY)       </code></p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       MONTHS_BETWEEN      </code></td>
<td><code dir="ltr" translate="no">         DATE_DIFF              (date_expression, date_expression, MONTH)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       NEXT_DAY      </code></td>
<td><code dir="ltr" translate="no">       DATE_ADD(       </code>
<p>DATE_TRUNC(</p>
<p>date_expression,</p>
<p>WEEK(day_value)</p>
<p>),</p>
<p>INTERVAL 1 WEEK</p>
<p><code dir="ltr" translate="no">        )       </code></p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       TO_DATE      </code></td>
<td><code dir="ltr" translate="no">         PARSE_DATE       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       FROM_UNIXTIME      </code></td>
<td><code dir="ltr" translate="no">         UNIX_SECONDS       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       FROM_UNIXTIMESTAMP      </code></td>
<td><code dir="ltr" translate="no">         FORMAT_TIMESTAMP       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       YEAR \ QUARTER \ MONTH \ HOUR \ MINUTE \ SECOND \ WEEKOFYEAR      </code></td>
<td><code dir="ltr" translate="no">         EXTRACT       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       DATEDIFF      </code></td>
<td><code dir="ltr" translate="no">         DATE_DIFF       </code></td>
</tr>
</tbody>
</table>

BigQuery offers the following additional date and time functions:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><ul>
<li><code dir="ltr" translate="no">           CURRENT_DATETIME         </code></li>
<li><code dir="ltr" translate="no">           DATE_FROM_UNIX_DATE         </code></li>
<li><code dir="ltr" translate="no">           DATE_TRUNC         </code></li>
<li><code dir="ltr" translate="no">           DATETIME         </code></li>
<li><code dir="ltr" translate="no">           DATETIME_TRUNC         </code></li>
<li><code dir="ltr" translate="no">           FORMAT_DATE         </code></li>
<li><code dir="ltr" translate="no">           FORMAT_DATETIME         </code></li>
<li><code dir="ltr" translate="no">           FORMAT_TIME         </code></li>
</ul></td>
<td><ul>
<li><code dir="ltr" translate="no">           FORMAT_TIMESTAMP         </code></li>
<li><code dir="ltr" translate="no">           PARSE_DATETIME         </code></li>
<li><code dir="ltr" translate="no">           PARSE_TIME         </code></li>
<li><code dir="ltr" translate="no">           STRING         </code></li>
<li><code dir="ltr" translate="no">           TIME         </code></li>
<li><code dir="ltr" translate="no">           TIME_ADD         </code></li>
<li><code dir="ltr" translate="no">           TIME_DIFF         </code></li>
<li><code dir="ltr" translate="no">           TIME_SUB         </code></li>
<li><code dir="ltr" translate="no">           TIME_TRUNC         </code></li>
<li><code dir="ltr" translate="no">           TIMESTAMP         </code></li>
<li><code dir="ltr" translate="no">           TIMESTAMP_ADD         </code></li>
</ul></td>
<td><ul>
<li><code dir="ltr" translate="no">           TIMESTAMP_DIFF         </code></li>
<li><code dir="ltr" translate="no">           TIMESTAMP_MICROS         </code></li>
<li><code dir="ltr" translate="no">           TIMESTAMP_MILLIS         </code></li>
<li><code dir="ltr" translate="no">           TIMESTAMP_SECONDS         </code></li>
<li><code dir="ltr" translate="no">           TIMESTAMP_SUB         </code></li>
<li><code dir="ltr" translate="no">           TIMESTAMP_TRUNC         </code></li>
<li><code dir="ltr" translate="no">           UNIX_DATE         </code></li>
<li><code dir="ltr" translate="no">           UNIX_MICROS         </code></li>
<li><code dir="ltr" translate="no">           UNIX_MILLIS         </code></li>
<li><code dir="ltr" translate="no">           UNIX_SECONDS         </code></li>
</ul></td>
</tr>
</tbody>
</table>

### String functions

The following table shows mappings between Hive string functions and their BigQuery equivalents:

<table>
<thead>
<tr class="header">
<th><strong>Hive</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       ASCII      </code></td>
<td><code dir="ltr" translate="no">         TO_CODE_POINTS(string_expr)[OFFSET(0)]       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       HEX      </code></td>
<td><code dir="ltr" translate="no">         TO_HEX       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       LENGTH      </code></td>
<td><code dir="ltr" translate="no">         CHAR_LENGTH       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       LENGTH      </code></td>
<td><code dir="ltr" translate="no">         CHARACTER_LENGTH       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       CHR      </code></td>
<td><code dir="ltr" translate="no">         CODE_POINTS_TO_STRING       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       CONCAT      </code></td>
<td><code dir="ltr" translate="no">         CONCAT       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       LOWER      </code></td>
<td><code dir="ltr" translate="no">         LOWER       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       LPAD      </code></td>
<td><code dir="ltr" translate="no">         LPAD       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       LTRIM      </code></td>
<td><code dir="ltr" translate="no">         LTRIM       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       REGEXP_EXTRACT      </code></td>
<td><code dir="ltr" translate="no">         REGEXP_EXTRACT       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       REGEXP_REPLACE      </code></td>
<td><code dir="ltr" translate="no">         REGEXP_REPLACE       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       REPLACE      </code></td>
<td><code dir="ltr" translate="no">         REPLACE       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       REVERSE      </code></td>
<td><code dir="ltr" translate="no">         REVERSE       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       RPAD      </code></td>
<td><code dir="ltr" translate="no">         RPAD       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       RTRIM      </code></td>
<td><code dir="ltr" translate="no">         RTRIM       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       SOUNDEX      </code></td>
<td><code dir="ltr" translate="no">         SOUNDEX       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       SPLIT      </code></td>
<td><code dir="ltr" translate="no">         SPLIT              (instring, delimiter)[ORDINAL(tokennum)]      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       SUBSTR, \ SUBSTRING      </code></td>
<td><code dir="ltr" translate="no">         SUBSTR       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       TRANSLATE      </code></td>
<td><code dir="ltr" translate="no">         TRANSLATE       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       LTRIM      </code></td>
<td><code dir="ltr" translate="no">         LTRIM       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       RTRIM      </code></td>
<td><code dir="ltr" translate="no">         RTRIM       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       TRIM      </code></td>
<td><code dir="ltr" translate="no">         TRIM       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       UPPER      </code></td>
<td><code dir="ltr" translate="no">         UPPER       </code></td>
</tr>
</tbody>
</table>

BigQuery offers the following additional string functions:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><ul>
<li><code dir="ltr" translate="no">           BYTE_LENGTH         </code></li>
<li><code dir="ltr" translate="no">           CODE_POINTS_TO_BYTES         </code></li>
<li><code dir="ltr" translate="no">           ENDS_WITH         </code></li>
<li><code dir="ltr" translate="no">           FROM_BASE32         </code></li>
<li><code dir="ltr" translate="no">           FROM_BASE64         </code></li>
<li><code dir="ltr" translate="no">           FROM_HEX         </code></li>
<li><code dir="ltr" translate="no">           NORMALIZE         </code></li>
<li><code dir="ltr" translate="no">           NORMALIZE_AND_CASEFOLD         </code></li>
</ul></td>
<td><ul>
<li><code dir="ltr" translate="no">           REPEAT         </code></li>
<li><code dir="ltr" translate="no">           SAFE_CONVERT_BYTES_TO_STRING         </code></li>
<li><code dir="ltr" translate="no">           SPLIT         </code></li>
<li><code dir="ltr" translate="no">           STARTS_WITH         </code></li>
<li><code dir="ltr" translate="no">           STRPOS         </code></li>
<li><code dir="ltr" translate="no">           TO_BASE32         </code></li>
<li><code dir="ltr" translate="no">           TO_BASE64         </code></li>
<li><code dir="ltr" translate="no">           TO_CODE_POINTS         </code></li>
</ul></td>
</tr>
</tbody>
</table>

### Math functions

The following table shows mappings between Hive [math functions](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-MathematicalFunctions) and their BigQuery equivalents:

<table>
<thead>
<tr class="header">
<th><strong>Hive</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       ABS      </code></td>
<td><code dir="ltr" translate="no">         ABS       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ACOS      </code></td>
<td><code dir="ltr" translate="no">         ACOS       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       ASIN      </code></td>
<td><code dir="ltr" translate="no">         ASIN       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ATAN      </code></td>
<td><code dir="ltr" translate="no">         ATAN       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       CEIL      </code></td>
<td><code dir="ltr" translate="no">         CEIL       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       CEILING      </code></td>
<td><code dir="ltr" translate="no">         CEILING       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       COS      </code></td>
<td><code dir="ltr" translate="no">         COS       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       FLOOR      </code></td>
<td><code dir="ltr" translate="no">         FLOOR       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       GREATEST      </code></td>
<td><code dir="ltr" translate="no">         GREATEST       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       LEAST      </code></td>
<td><code dir="ltr" translate="no">         LEAST       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       LN      </code></td>
<td><code dir="ltr" translate="no">         LN       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       LNNVL      </code></td>
<td>Use with <code dir="ltr" translate="no">       ISNULL      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       LOG      </code></td>
<td><code dir="ltr" translate="no">         LOG       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       MOD (% operator)      </code></td>
<td><code dir="ltr" translate="no">         MOD       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       POWER      </code></td>
<td><code dir="ltr" translate="no">         POWER              ,               POW       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       RAND      </code></td>
<td><code dir="ltr" translate="no">         RAND       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       ROUND      </code></td>
<td><code dir="ltr" translate="no">         ROUND       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       SIGN      </code></td>
<td><code dir="ltr" translate="no">         SIGN       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       SIN      </code></td>
<td><code dir="ltr" translate="no">         SIN       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       SQRT      </code></td>
<td><code dir="ltr" translate="no">         SQRT       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       HASH      </code></td>
<td><code dir="ltr" translate="no">         FARM_FINGERPRINT, MD5, SHA1, SHA256, SHA512       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       STDDEV_POP      </code></td>
<td><code dir="ltr" translate="no">         STDDEV_POP       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       STDDEV_SAMP      </code></td>
<td><code dir="ltr" translate="no">         STDDEV_SAMP       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       TAN      </code></td>
<td><code dir="ltr" translate="no">         TAN       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       TRUNC      </code></td>
<td><code dir="ltr" translate="no">         TRUNC       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       NVL      </code></td>
<td><code dir="ltr" translate="no">         IFNULL                (expr, 0),                 COALESCE                (exp, 0)       </code></td>
</tr>
</tbody>
</table>

BigQuery offers the following additional math functions:

  - `  DIV  `
  - `  IEEE_DIVIDE  `
  - `  IS_INF  `
  - `  IS_NAN  `
  - `  LOG10  `
  - `  SAFE_DIVIDE  `

### Logical and conditional functions

The following table shows mappings between Hive logical and conditional functions and their BigQuery equivalents:

<table>
<thead>
<tr class="header">
<th><strong>Hive</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         CASE       </code></td>
<td><code dir="ltr" translate="no">         CASE       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         COALESCE       </code></td>
<td><code dir="ltr" translate="no">         COALESCE       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         NVL       </code></td>
<td><code dir="ltr" translate="no">         IFNULL              (expr, 0),               COALESCE              (exp, 0)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         NULLIF       </code></td>
<td><code dir="ltr" translate="no">         NULLIF       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         IF       </code></td>
<td><code dir="ltr" translate="no">         IF(expr, true_result, else_result)       </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         ISNULL       </code></td>
<td><code dir="ltr" translate="no">       IS NULL      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         ISNOTNULL       </code></td>
<td><code dir="ltr" translate="no">       IS NOT NULL      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         NULLIF       </code></td>
<td><code dir="ltr" translate="no">         NULLIF       </code></td>
</tr>
</tbody>
</table>

### UDFs and UDAFs

Apache Hive supports writing user defined functions (UDFs) in Java. You can load UDFs into Hive to be used in regular queries. [BigQuery UDFs](/bigquery/docs/user-defined-functions) must be written in GoogleSQL or JavaScript. Converting the Hive UDFs to SQL UDFs is recommended because SQL UDFs perform better. If you need to use JavaScript, read [Best Practices for JavaScript UDFs](/bigquery/docs/user-defined-functions#best-practices-for-javascript-udfs) . For other languages, BigQuery supports [remote functions](/bigquery/docs/remote-functions) that let you invoke your functions in [Cloud Run functions](/functions/docs/concepts/overview) or [Cloud Run](/run/docs/overview/what-is-cloud-run) from GoogleSQL queries.

BigQuery does not support user-defined aggregation functions (UDAFs).

## DML syntax

This section addresses differences in data manipulation language (DML) syntax between Hive and BigQuery.

### `     INSERT    ` statement

Most Hive `  INSERT  ` statements are compatible with BigQuery. The following table shows exceptions:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Hive</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       INSERT INTO TABLE tablename [PARTITION (partcol1[=val1], partcol2[=val2] ...)] VALUES values_row [, values_row ...]      </code></td>
<td><code dir="ltr" translate="no">         INSERT INTO                table              (...) VALUES (...);      </code>
<p>Note: In BigQuery, omitting column names in the <code dir="ltr" translate="no">        INSERT       </code> statement only works if values for all columns in the target table are included in ascending order based on their ordinal positions.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       INSERT OVERWRITE [LOCAL] DIRECTORY directory1      </code>
<p><code dir="ltr" translate="no">        [ROW FORMAT row_format] [STORED AS file_format] (Note: Only available starting with Hive 0.11.0)       </code></p>
<p><code dir="ltr" translate="no">        SELECT ... FROM ...       </code></p></td>
<td>BigQuery doesn't support the insert-overwrite operations. This Hive syntax can be migrated to <code dir="ltr" translate="no">         TRUNCATE       </code> and <code dir="ltr" translate="no">         INSERT       </code> statements.</td>
</tr>
</tbody>
</table>

BigQuery imposes [DML quotas](/bigquery/quotas#data-manipulation-language-statements) that restrict the number of DML statements that you can execute daily. To make the best use of your quota, consider the following approaches:

  - Combine multiple rows in a single `  INSERT  ` statement, instead of one row for each `  INSERT  ` operation.

  - Combine multiple DML statements (including `  INSERT  ` ) by using a `  MERGE  ` statement.

  - Use `  CREATE TABLE ... AS SELECT  ` to create and populate new tables.

### `     UPDATE    ` statement

Most Hive `  UPDATE  ` statements are compatible with BigQuery. The following table shows exceptions:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Hive</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       UPDATE tablename SET column = value [, column = value ...] [WHERE expression]      </code></td>
<td><code dir="ltr" translate="no">       UPDATE table      </code>
<p><code dir="ltr" translate="no">        SET column = expression [,...]       </code></p>
<p><code dir="ltr" translate="no">        [FROM ...]       </code></p>
<p><code dir="ltr" translate="no">        WHERE TRUE       </code></p>
<p>Note: All <code dir="ltr" translate="no">        UPDATE       </code> statements in BigQuery require a <code dir="ltr" translate="no">        WHERE       </code> keyword, followed by a condition.</p></td>
</tr>
</tbody>
</table>

### `     DELETE    ` and `     TRUNCATE    ` statements

You can use `  DELETE  ` or `  TRUNCATE  ` statements to remove rows from a table without affecting the table schema or indexes.

In BigQuery, the `  DELETE  ` statement must have a `  WHERE  ` clause. For more information about `  DELETE  ` in BigQuery, see [`  DELETE  ` examples](/bigquery/docs/reference/standard-sql/dml-syntax#delete_examples) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Hive</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         DELETE              FROM tablename [WHERE expression]      </code></td>
<td><code dir="ltr" translate="no">         DELETE FROM              table_name      </code> <code dir="ltr" translate="no">       WHERE TRUE      </code>
<p>BigQuery <code dir="ltr" translate="no">        DELETE       </code> statements require a <code dir="ltr" translate="no">        WHERE       </code> clause.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         TRUNCATE              [TABLE] table_name [PARTITION partition_spec];      </code></td>
<td><code dir="ltr" translate="no">         TRUNCATE TABLE              [[project_name.]dataset_name.]table_name      </code></td>
</tr>
</tbody>
</table>

### `     MERGE    ` statement

The `  MERGE  ` statement can combine `  INSERT  ` , `  UPDATE  ` , and `  DELETE  ` operations into a single *upsert* statement and perform the operations. The `  MERGE  ` operation must match one source row at most for each target row.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Hive</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         MERGE INTO                AS T USING                AS S       </code> <code dir="ltr" translate="no">       ON        </code>
<p><code dir="ltr" translate="no">        WHEN MATCHED [AND                 ] THEN UPDATE SET           </code></p>
<p><code dir="ltr" translate="no">        WHEN MATCHED [AND                 ] THEN DELETE        </code></p>
<p><code dir="ltr" translate="no">        WHEN NOT MATCHED [AND                 ] THEN INSERT VALUES           </code></p></td>
<td><code dir="ltr" translate="no">         MERGE target       </code> <code dir="ltr" translate="no">       USING source      </code>
<p><code dir="ltr" translate="no">        ON target.key = source.key       </code></p>
<p><code dir="ltr" translate="no">        WHEN MATCHED AND source.filter = 'filter_exp' THEN       </code></p>
<p><code dir="ltr" translate="no">        UPDATE SET       </code></p>
<p><code dir="ltr" translate="no">        target.col1 = source.col1,       </code></p>
<p><code dir="ltr" translate="no">        target.col2 = source.col2,       </code></p>
<p><code dir="ltr" translate="no">        ...       </code></p>
<p>Note: You must list all columns that need to be updated.</p></td>
</tr>
</tbody>
</table>

### `     ALTER    ` statement

The following table provides details about converting `  CREATE VIEW  ` statements from Hive to BigQuery:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Function</strong></th>
<th><strong>Hive</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       Rename table      </code></td>
<td><code dir="ltr" translate="no">         ALTER TABLE              table_name RENAME TO new_table_name;      </code></td>
<td>Not supported. A workaround is to use a copy job with the name that you want as the destination table, and then delete the old one.<br />

<p><code dir="ltr" translate="no">        bq copy  project.dataset.old_table  project.dataset.new_table       </code></p>
<p><code dir="ltr" translate="no">        bq rm --table project.dataset.old_table       </code></p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       Table properties      </code></td>
<td><code dir="ltr" translate="no">         ALTER TABLE              table_name SET TBLPROPERTIES table_properties;      </code> <code dir="ltr" translate="no"></code>
<p><code dir="ltr" translate="no">        table_properties:       </code></p>
<p><code dir="ltr" translate="no">        : (property_name = property_value, property_name = property_value, ... )       </code></p>
<p><strong><code dir="ltr" translate="no">         Table Comment:        </code></strong> <code dir="ltr" translate="no">        ALTER TABLE table_name SET TBLPROPERTIES ('comment' = new_comment);       </code></p></td>
<td><code dir="ltr" translate="no">       {ALTER TABLE | ALTER TABLE IF EXISTS}      </code>
<p><code dir="ltr" translate="no">        table_name       </code></p>
<p><code dir="ltr" translate="no">        SET OPTIONS(                 table_set_options_list                )       </code></p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       SerDe properties (Serialize and deserialize)      </code></td>
<td><code dir="ltr" translate="no">         ALTER TABLE              table_name [PARTITION partition_spec] SET SERDE serde_class_name [WITH SERDEPROPERTIES serde_properties];      </code> <code dir="ltr" translate="no"></code>
<p><code dir="ltr" translate="no">        ALTER TABLE table_name [PARTITION partition_spec] SET SERDEPROPERTIES serde_properties;       </code></p>
<p><code dir="ltr" translate="no"></code></p>
<p><code dir="ltr" translate="no">        serde_properties:       </code></p>
<p><code dir="ltr" translate="no">        : (property_name = property_value, property_name = property_value, ... )       </code></p></td>
<td>Serialization and deserialization is managed by the BigQuery service and isn't user configurable.
<p>To learn how to let BigQuery read data from CSV, JSON, AVRO, PARQUET, or ORC files, see <a href="/bigquery/docs/external-data-cloud-storage">Create Cloud Storage external tables</a> .</p>
<p>Supports CSV, JSON, AVRO, and PARQUET export formats. For more information, see <a href="/bigquery/docs/exporting-data#export_formats_and_compression_types">Export formats and compression types</a> .</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       Table storage properties      </code></td>
<td><code dir="ltr" translate="no">         ALTER TABLE              table_name CLUSTERED BY (col_name, col_name, ...) [SORTED BY (col_name, ...)]      </code> <code dir="ltr" translate="no">       INTO num_buckets BUCKETS;      </code></td>
<td>Not supported for the <code dir="ltr" translate="no">       ALTER      </code> statements.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       Skewed table      </code></td>
<td><strong><code dir="ltr" translate="no">        Skewed:       </code></strong> <code dir="ltr" translate="no">         ALTER TABLE              table_name SKEWED BY (col_name1, col_name2, ...)      </code> <code dir="ltr" translate="no">       ON ([(col_name1_value, col_name2_value, ...) [, (col_name1_value, col_name2_value), ...]      </code>
<p><code dir="ltr" translate="no">        [STORED AS DIRECTORIES];       </code></p>
<p><strong><code dir="ltr" translate="no">         Not Skewed:        </code></strong> <code dir="ltr" translate="no">        ALTER TABLE table_name NOT SKEWED;       </code></p>
<p><strong><code dir="ltr" translate="no">         Not Stored as Directories:        </code></strong> <code dir="ltr" translate="no">        ALTER TABLE table_name NOT STORED AS DIRECTORIES;       </code></p>
<p><strong><code dir="ltr" translate="no">         Skewed Location:        </code></strong> <code dir="ltr" translate="no">        ALTER TABLE table_name SET SKEWED LOCATION (col_name1="location1" [, col_name2="location2", ...] );       </code></p></td>
<td>Balancing storage for performance queries is managed by the BigQuery service and isn't configurable.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       Table constraints      </code></td>
<td><code dir="ltr" translate="no">         ALTER TABLE              table_name ADD CONSTRAINT constraint_name PRIMARY KEY (column, ...) DISABLE NOVALIDATE;      </code> <code dir="ltr" translate="no">       ALTER TABLE table_name ADD CONSTRAINT constraint_name FOREIGN KEY (column, ...) REFERENCES table_name(column, ...) DISABLE NOVALIDATE RELY;      </code>
<p><code dir="ltr" translate="no">        ALTER TABLE table_name DROP CONSTRAINT constraint_name;       </code></p></td>
<td><code dir="ltr" translate="no">       ALTER TABLE [[project_name.]dataset_name.]table_name      </code><br />
<code dir="ltr" translate="no">       ADD [CONSTRAINT [IF NOT EXISTS] [constraint_name]] constraint NOT ENFORCED;      </code><br />
<code dir="ltr" translate="no">       ALTER TABLE [[project_name.]dataset_name.]table_name      </code><br />
<code dir="ltr" translate="no">       ADD PRIMARY KEY(column_list) NOT ENFORCED;      </code><br />

<p>For more information, see <a href="/bigquery/docs/reference/standard-sql/data-definition-language#alter_table_add_primary_key_statement"><code dir="ltr" translate="no">         ALTER TABLE ADD PRIMARY KEY        </code> statement</a> .</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       Add partition      </code></td>
<td><code dir="ltr" translate="no">         ALTER TABLE              table_name ADD [IF NOT EXISTS] PARTITION partition_spec [LOCATION 'location'][, PARTITION partition_spec [LOCATION 'location'], ...];      </code> <code dir="ltr" translate="no"></code>
<p><code dir="ltr" translate="no">        partition_spec:       </code></p>
<p><code dir="ltr" translate="no">        : (partition_column = partition_col_value, partition_column = partition_col_value, ...)       </code></p></td>
<td>Not supported. Additional partitions are added as needed when data with new values in the partition columns are loaded.<br />

<p>For more information, see <a href="/bigquery/docs/managing-partitioned-tables">Managing partitioned tables</a> .</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       Rename partition      </code></td>
<td><code dir="ltr" translate="no">         ALTER TABLE              table_name PARTITION partition_spec RENAME TO PARTITION partition_spec;      </code></td>
<td>Not supported.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       Exchange partition      </code></td>
<td><code dir="ltr" translate="no">       -- Move partition from table_name_1 to table_name_2      </code>
<p><code dir="ltr" translate="no">        ALTER TABLE table_name_2                 EXCHANGE                PARTITION (partition_spec) WITH TABLE table_name_1;       </code> <code dir="ltr" translate="no">        -- multiple partitions       </code></p>
<p><code dir="ltr" translate="no">        ALTER TABLE table_name_2 EXCHANGE PARTITION (partition_spec, partition_spec2, ...) WITH TABLE table_name_1;       </code></p></td>
<td>Not supported.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       Recover partition      </code></td>
<td><code dir="ltr" translate="no">         MSCK [REPAIR]              TABLE table_name [ADD/DROP/SYNC PARTITIONS];      </code></td>
<td>Not supported.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       Drop partition      </code></td>
<td><code dir="ltr" translate="no">         ALTER TABLE table_name DROP              [IF EXISTS] PARTITION partition_spec[, PARTITION partition_spec, ...]      </code> <code dir="ltr" translate="no">       [IGNORE PROTECTION] [PURGE];      </code></td>
<td>Supported using the following methods:
<ul>
<li><code dir="ltr" translate="no">         bq rm 'mydataset.table_name$partition_id'        </code></li>
<li><code dir="ltr" translate="no">         DELETE from table_name$partition_id WHERE 1=1        </code></li>
</ul></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       (Un)Archive partition      </code></td>
<td><code dir="ltr" translate="no">         ALTER TABLE table_name ARCHIVE              PARTITION partition_spec;      </code> <code dir="ltr" translate="no">       ALTER TABLE table_name UNARCHIVE PARTITION partition_spec;      </code></td>
<td>Not supported.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       Table and partition file format      </code></td>
<td><code dir="ltr" translate="no">         ALTER TABLE table_name [PARTITION partition_spec]              SET FILEFORMAT file_format;      </code></td>
<td>Not supported.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       Table and partition location      </code></td>
<td><code dir="ltr" translate="no">         ALTER TABLE table_name [PARTITION partition_spec]              SET LOCATION "new location";      </code></td>
<td>Not supported.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       Table and partition touch      </code></td>
<td><code dir="ltr" translate="no">         ALTER TABLE table_name TOUCH              [PARTITION partition_spec];      </code></td>
<td>Not supported.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       Table and partition protection      </code></td>
<td><code dir="ltr" translate="no">         ALTER TABLE table_name [PARTITION partition_spec]              ENABLE|DISABLE NO_DROP [CASCADE];      </code> <code dir="ltr" translate="no"></code>
<p><code dir="ltr" translate="no">        ALTER TABLE table_name [PARTITION partition_spec] ENABLE|DISABLE OFFLINE;       </code></p></td>
<td>Not supported.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       Table and partition compact      </code></td>
<td><code dir="ltr" translate="no">         ALTER TABLE table_name [PARTITION (partition_key = 'partition_value' [, ...])]       </code> <code dir="ltr" translate="no">       COMPACT 'compaction_type'[AND WAIT]      </code>
<p><code dir="ltr" translate="no">        [WITH OVERWRITE TBLPROPERTIES ("property"="value" [, ...])];       </code></p></td>
<td>Not supported.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       Table and artition concatenate      </code></td>
<td><code dir="ltr" translate="no">         ALTER TABLE table_name [PARTITION (partition_key = 'partition_value' [, ...])]              CONCATENATE;      </code></td>
<td>Not supported.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       Table and partition columns      </code></td>
<td><code dir="ltr" translate="no">         ALTER TABLE table_name [PARTITION (partition_key = 'partition_value' [, ...])]              UPDATE COLUMNS;      </code></td>
<td>Not supported for the <code dir="ltr" translate="no">       ALTER TABLE      </code> statements.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       Column name, type, position, and comment      </code></td>
<td><code dir="ltr" translate="no">         ALTER TABLE table_name [PARTITION partition_spec]              CHANGE [COLUMN] col_old_name col_new_name column_type      </code> <code dir="ltr" translate="no">       [COMMENT col_comment] [FIRST|AFTER column_name] [CASCADE|RESTRICT];      </code></td>
<td>Not supported.</td>
</tr>
</tbody>
</table>

## DDL syntax

This section addresses differences in Data Definition Language (DDL) syntax between Hive and BigQuery.

### `     CREATE TABLE    ` and `     DROP TABLE    ` statements

The following table provides details about converting `  CREATE TABLE  ` statements from Hive to BigQuery:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Type</strong></th>
<th><strong>Hive</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Managed tables</td>
<td><code dir="ltr" translate="no">       create table table_name (      </code>
<p><code dir="ltr" translate="no">        id                int,       </code></p>
<p><code dir="ltr" translate="no">        dtDontQuery       string,       </code></p>
<p><code dir="ltr" translate="no">        name              string       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p></td>
<td><code dir="ltr" translate="no">       CREATE TABLE `myproject`.mydataset.table_name (       </code>
<p>id INT64,</p>
<p>dtDontQuery STRING,</p>
<p>name STRING</p>
<p><code dir="ltr" translate="no">        )       </code></p></td>
</tr>
<tr class="even">
<td>Partitioned tables</td>
<td><code dir="ltr" translate="no">       create table table_name (      </code>
<p><code dir="ltr" translate="no">        id       int,       </code></p>
<p><code dir="ltr" translate="no">        dt       string,       </code></p>
<p><code dir="ltr" translate="no">        name     string       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p>
<p><code dir="ltr" translate="no">        partitioned by (date string)       </code></p></td>
<td><code dir="ltr" translate="no">       CREATE TABLE `myproject`.mydataset.table_name (       </code>
<p>id INT64,</p>
<p>dt DATE,</p>
<p>name STRING</p>
<p>)</p>
<p>PARTITION BY dt</p>
<p>OPTIONS(</p>
<p>partition_expiration_days=3,</p>
<p>description="a table partitioned by date_col"</p>
<p><code dir="ltr" translate="no">        )       </code></p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       Create table as select (CTAS)      </code></td>
<td><code dir="ltr" translate="no">       CREATE TABLE new_key_value_store      </code>
<p><code dir="ltr" translate="no">        ROW FORMAT SERDE "org.apache.hadoop.hive.serde2.columnar.ColumnarSerDe"       </code></p>
<p><code dir="ltr" translate="no">        STORED AS RCFile       </code></p>
<p><code dir="ltr" translate="no">        AS       </code></p>
<p><code dir="ltr" translate="no">        SELECT (key % 1024) new_key, concat(key, value) key_value_pair, dt       </code></p>
<p><code dir="ltr" translate="no">        FROM key_value_store       </code></p>
<p><code dir="ltr" translate="no">        SORT BY new_key, key_value_pair;       </code></p></td>
<td><code dir="ltr" translate="no">       CREATE TABLE `myproject`.mydataset.new_key_value_store      </code>
<p>When partitioning by date, uncomment the following:</p>
<p><code dir="ltr" translate="no">        PARTITION BY dt       </code></p>
<code dir="ltr" translate="no"></code>
<p>OPTIONS(</p>
<p><code dir="ltr" translate="no">        description="Table Description",       </code></p>
<p>When partitioning by date, uncomment the following. It's recommended to use <code dir="ltr" translate="no">        require_partition       </code> when the table is partitioned.</p>
<p><code dir="ltr" translate="no">        require_partition_filter=TRUE       </code></p>
<p><code dir="ltr" translate="no">        ) AS       </code></p>
<p><code dir="ltr" translate="no">        SELECT (key % 1024) new_key, concat(key, value) key_value_pair, dt       </code></p>
<p><code dir="ltr" translate="no">        FROM key_value_store       </code></p>
<p><code dir="ltr" translate="no">        SORT BY new_key, key_value_pair'       </code></p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       Create Table Like:      </code>
<p>The <code dir="ltr" translate="no">        LIKE       </code> form of <code dir="ltr" translate="no">        CREATE TABLE       </code> lets you copy an existing table definition exactly.</p></td>
<td><code dir="ltr" translate="no">       CREATE TABLE empty_key_value_store      </code>
<p><code dir="ltr" translate="no">        LIKE key_value_store [TBLPROPERTIES (property_name=property_value, ...)];       </code></p></td>
<td>Not supported.</td>
</tr>
<tr class="odd">
<td>Bucketed sorted tables (clustered in BigQuery terminology)</td>
<td><code dir="ltr" translate="no">       CREATE TABLE page_view(      </code>
<p><code dir="ltr" translate="no">        viewTime INT,       </code></p>
<p><code dir="ltr" translate="no">        userid BIGINT,       </code></p>
<p><code dir="ltr" translate="no">        page_url STRING,       </code></p>
<p><code dir="ltr" translate="no">        referrer_url STRING,       </code></p>
<p><code dir="ltr" translate="no">        ip STRING COMMENT 'IP Address of the User'       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p>
<p><code dir="ltr" translate="no">        COMMENT 'This is the page view table'       </code></p>
<p><code dir="ltr" translate="no">        PARTITIONED BY(dt STRING, country STRING)       </code></p>
<p><code dir="ltr" translate="no">        CLUSTERED BY(userid) SORTED BY(viewTime) INTO 32 BUCKETS       </code></p>
<p><code dir="ltr" translate="no">        ROW FORMAT DELIMITED       </code></p>
<p><code dir="ltr" translate="no">        FIELDS TERMINATED BY '\001'       </code></p>
<p><code dir="ltr" translate="no">        COLLECTION ITEMS TERMINATED BY '\002'       </code></p>
<p><code dir="ltr" translate="no">        MAP KEYS TERMINATED BY '\003'       </code></p>
<p><code dir="ltr" translate="no">        STORED AS SEQUENCEFILE;       </code></p></td>
<td><code dir="ltr" translate="no">       CREATE TABLE `myproject` mydataset.page_view (       </code>
<p>viewTime INT,</p>
<p>dt DATE,</p>
<p>userId BIGINT,</p>
<p>page_url STRING,</p>
<p>referrer_url STRING,</p>
<p>ip STRING OPTIONS (description="IP Address of the User")</p>
<p>)</p>
<p>PARTITION BY dt</p>
<p>CLUSTER BY userId</p>
<p>OPTIONS (</p>
<p>partition_expiration_days=3,</p>
<p>description="This is the page view table",</p>
<p>require_partition_filter=TRUE</p>
<p><code dir="ltr" translate="no">        )'       </code></p>
<p>For more information, see <a href="/bigquery/docs/creating-clustered-tables">Create and use clustered tables</a> .</p></td>
</tr>
<tr class="even">
<td>Skewed tables (tables where one or more columns have skewed values)</td>
<td><code dir="ltr" translate="no">       CREATE TABLE list_bucket_multiple (col1 STRING, col2 int, col3 STRING)      </code>
<p><code dir="ltr" translate="no">        SKEWED BY (col1, col2) ON (('s1',1), ('s3',3), ('s13',13), ('s78',78)) [STORED AS DIRECTORIES];       </code></p></td>
<td>Not supported.</td>
</tr>
<tr class="odd">
<td>Temporary tables</td>
<td><code dir="ltr" translate="no">       CREATE TEMPORARY TABLE list_bucket_multiple (      </code>
<p><code dir="ltr" translate="no">        col1 STRING,       </code></p>
<p><code dir="ltr" translate="no">        col2 int,       </code></p>
<p><code dir="ltr" translate="no">        col3 STRING);       </code></p></td>
<td>You can achieve this using expiration time as follows:
<p><code dir="ltr" translate="no">        CREATE TABLE mydataset.newtable       </code></p>
<p><code dir="ltr" translate="no">        (       </code></p>
<p><code dir="ltr" translate="no">        col1 STRING OPTIONS(description="An optional INTEGER field"),       </code></p>
<p><code dir="ltr" translate="no">        col2 INT64,       </code></p>
<p><code dir="ltr" translate="no">        col3 STRING       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p>
<p><code dir="ltr" translate="no">        PARTITION BY DATE(_PARTITIONTIME)       </code></p>
<p><code dir="ltr" translate="no">        OPTIONS(       </code></p>
<p><code dir="ltr" translate="no">        expiration_timestamp=TIMESTAMP "2020-01-01 00:00:00 UTC",       </code></p>
<p><code dir="ltr" translate="no">        partition_expiration_days=1,       </code></p>
<p><code dir="ltr" translate="no">        description="a table that expires in 2020, with each partition living for 24 hours",       </code></p>
<p><code dir="ltr" translate="no">        labels=[("org_unit", "development")]       </code></p>
<p><code dir="ltr" translate="no">        )       </code></p></td>
</tr>
<tr class="even">
<td>Transactional tables</td>
<td><code dir="ltr" translate="no">       CREATE TRANSACTIONAL TABLE transactional_table_test(key string, value string) PARTITIONED BY(ds string) STORED AS ORC;      </code></td>
<td>All table modifications in BigQuery are ACID (atomicity, consistency, isolation, durability) compliant.</td>
</tr>
<tr class="odd">
<td>Drop table</td>
<td><code dir="ltr" translate="no">       DROP TABLE [IF EXISTS] table_name [PURGE];      </code></td>
<td><code dir="ltr" translate="no">       {DROP TABLE | DROP TABLE IF EXISTS}      </code>
<p><code dir="ltr" translate="no">        table_name       </code></p></td>
</tr>
<tr class="even">
<td>Truncate table</td>
<td><code dir="ltr" translate="no">       TRUNCATE TABLE table_name [PARTITION partition_spec];      </code>
<p><code dir="ltr" translate="no">        partition_spec:       </code></p>
<p><code dir="ltr" translate="no">        : (partition_column = partition_col_value, partition_column = partition_col_value, ...)       </code></p></td>
<td>Not supported. The following workarounds are available:
<ul>
<li>Drop and create the table again with the same schema.</li>
<li>Set write disposition for table to <code dir="ltr" translate="no">         WRITE_TRUNCATE        </code> if the truncate operation is a common use case for the given table.</li>
<li>Use the <code dir="ltr" translate="no">         CREATE OR REPLACE TABLE        </code> statement.</li>
<li>Use the <code dir="ltr" translate="no">         DELETE from table_name WHERE 1=1        </code> statement.</li>
</ul>
<p>Note: Specific partitions can also be truncated. For more information, see <a href="/bigquery/docs/managing-partitioned-tables#delete_a_partition">Delete a partition</a> .</p></td>
</tr>
</tbody>
</table>

### `     CREATE EXTERNAL TABLE    ` and `     DROP EXTERNAL TABLE    ` statements

For external table support in BigQuery, see [Introduction to external data sources](/bigquery/external-data-sources) .

### `     CREATE VIEW    ` and `     DROP VIEW    ` statements

The following table provides details about converting `  CREATE VIEW  ` statements from Hive to BigQuery:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Hive</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       CREATE VIEW [IF NOT EXISTS] [db_name.]view_name [(column_name [COMMENT column_comment], ...) ]      </code>
<p><code dir="ltr" translate="no">        [COMMENT view_comment]       </code></p>
<p><code dir="ltr" translate="no">        [TBLPROPERTIES (property_name = property_value, ...)]       </code></p>
<p><code dir="ltr" translate="no">        AS SELECT ...;       </code></p></td>
<td><code dir="ltr" translate="no">       {CREATE VIEW | CREATE VIEW IF NOT EXISTS | CREATE OR REPLACE VIEW}       </code>
<p>view_name</p>
<p>[OPTIONS( <a href="/bigquery/docs/reference/standard-sql/data-definition-language#view_option_list">view_option_list</a> )]</p>
<p><code dir="ltr" translate="no">        AS query_expression       </code></p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       CREATE MATERIALIZED VIEW [IF NOT EXISTS] [db_name.]materialized_view_name      </code>
<p><code dir="ltr" translate="no">        [DISABLE REWRITE]       </code></p>
<p><code dir="ltr" translate="no">        [COMMENT materialized_view_comment]       </code></p>
<p><code dir="ltr" translate="no">        [PARTITIONED ON (col_name, ...)]       </code></p>
<p><code dir="ltr" translate="no">        [       </code></p>
<p><code dir="ltr" translate="no">        [ROW FORMAT row_format]       </code></p>
<p><code dir="ltr" translate="no">        [STORED AS file_format]       </code></p>
<p><code dir="ltr" translate="no">        | STORED BY 'storage.handler.class.name' [WITH SERDEPROPERTIES (...)]       </code></p>
<p><code dir="ltr" translate="no">        ]       </code></p>
<p><code dir="ltr" translate="no">        [LOCATION hdfs_path]       </code></p>
<p><code dir="ltr" translate="no">        [TBLPROPERTIES (property_name=property_value, ...)]       </code></p>
<p><code dir="ltr" translate="no">        AS       </code></p>
<p><code dir="ltr" translate="no">          ;        </code></p></td>
<td><code dir="ltr" translate="no">       CREATE MATERIALIZED VIEW [IF NOT EXISTS] \ [project_id].[dataset_id].materialized_view_name       </code>
<p>-- cannot disable rewrites in BigQuery</p>
<p>[OPTIONS(</p>
<p>[description="materialized_view_comment",] \ [other <a href="/bigquery/docs/reference/standard-sql/data-definition-language#materialized_view_option_list">materialized_view_option_list</a> ]</p>
<p>)]</p>
<p><code dir="ltr" translate="no">        [PARTITION BY (col_name)] --same as source table       </code></p></td>
</tr>
</tbody>
</table>

### `     CREATE FUNCTION    ` and `     DROP FUNCTION    ` statements

The following table provides details about converting stored procedures from Hive to BigQuery:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Hive</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       CREATE TEMPORARY FUNCTION function_name AS class_name;      </code></td>
<td><code dir="ltr" translate="no">       CREATE  { TEMPORARY | TEMP }  FUNCTION function_name ([named_parameter[, ...]])      </code>
<p><code dir="ltr" translate="no">        [RETURNS data_type]       </code></p>
<p><code dir="ltr" translate="no">        AS (sql_expression)       </code></p>
<p><code dir="ltr" translate="no">        named_parameter:       </code></p>
<p><code dir="ltr" translate="no">        param_name param_type       </code></p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       DROP TEMPORARY FUNCTION [IF EXISTS] function_name;      </code></td>
<td>Not supported.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       CREATE FUNCTION [db_name.]function_name AS class_name      </code>
<p><code dir="ltr" translate="no">        [USING JAR|FILE|ARCHIVE 'file_uri' [, JAR|FILE|ARCHIVE 'file_uri'] ];       </code></p></td>
<td>Supported for allowlisted projects as an alpha feature.<br />

<p><code dir="ltr" translate="no">        CREATE { FUNCTION | FUNCTION IF NOT EXISTS | OR REPLACE FUNCTION }       </code></p>
<p><code dir="ltr" translate="no">        function_name ([named_parameter[, ...]])       </code></p>
<p><code dir="ltr" translate="no">        [RETURNS data_type]       </code></p>
<p><code dir="ltr" translate="no">        AS (expression);       </code></p>
<p><code dir="ltr" translate="no">        named_parameter:       </code></p>
<p><code dir="ltr" translate="no">        param_name param_type       </code></p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       DROP FUNCTION [IF EXISTS] function_name;      </code></td>
<td><code dir="ltr" translate="no">       DROP FUNCTION [ IF EXISTS ] function_name      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       RELOAD FUNCTION;      </code></td>
<td>Not supported.</td>
</tr>
</tbody>
</table>

### `     CREATE MACRO    ` and `     DROP MACRO    ` statements

The following table provides details about converting procedural SQL statements used in creating macro from Hive to BigQuery with variable declaration and assignment:

<table>
<thead>
<tr class="header">
<th><strong>Hive</strong></th>
<th><strong>BigQuery</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       CREATE TEMPORARY MACRO macro_name([col_name col_type, ...]) expression;      </code></td>
<td>Not supported. In some cases, this can be substituted with a UDF.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       DROP TEMPORARY MACRO [IF EXISTS] macro_name;      </code></td>
<td>Not supported.</td>
</tr>
</tbody>
</table>

## Error codes and messages

[Hive error codes](https://cwiki.apache.org/confluence/display/GEODE/Error+Codes) and [BigQuery error codes](/bigquery/troubleshooting-errors) are different. If your application logic is catching errors, eliminate the source of the error because BigQuery doesn't return the same error codes.

In BigQuery, it's common to use the [INFORMATION\_SCHEMA](/bigquery/docs/information-schema-jobs) views or [audit logging](/bigquery/docs/reference/auditlogs) to examine errors.

## Consistency guarantees and transaction isolation

Both Hive and BigQuery support transactions with ACID semantics. [Transactions](https://cwiki.apache.org/confluence/display/Hive/Hive+Transactions#HiveTransactions-ACIDandTransactionsinHive) are enabled by default in Hive 3.

### ACID semantics

Hive supports [snapshot isolation](https://cwiki.apache.org/confluence/display/hive/hive+transactions) . When you execute a query, the query is provided with a consistent snapshot of the database, which it uses until the end of its execution. Hive provides full ACID semantics at the row level, letting one application add rows when another application reads from the same partition without interfering with each other.

BigQuery provides [optimistic concurrency control](https://en.wikipedia.org/wiki/Optimistic_concurrency_control) (first to commit wins) with [snapshot isolation](https://en.wikipedia.org/wiki/Snapshot_isolation) , in which a query reads the last committed data before the query starts. This approach guarantees the same level of consistency for each row and mutation, and across rows within the same DML statement, while avoiding deadlocks. For multiple DML updates to the same table, BigQuery switches to [pessimistic concurrency control](/bigquery/docs/data-manipulation-language#dml-limitations) . Load jobs can run independently and append tables; however, BigQuery doesn't provide an explicit transaction boundary or session.

### Transactions

Hive doesn't support multi-statement transactions. It doesn't support `  BEGIN  ` , `  COMMIT  ` , and `  ROLLBACK  ` statements. In Hive, all language operations are auto-committed.

BigQuery supports multi-statement transactions inside a single query or across multiple queries when you use sessions. A multi-statement transaction lets you perform mutating operations, such as inserting or deleting rows from one or more tables and either committing or rolling back the changes. For more information, see [Multi-statement transactions](/bigquery/docs/reference/standard-sql/transactions) .
