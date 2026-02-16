GoogleSQL for BigQuery supports collation. Collation defines rules to sort and compare strings in certain [operations](#collate_operations) , such as conditional expressions, joins, and groupings.

By default, GoogleSQL sorts strings case-sensitively. This means that `  a  ` and `  A  ` are treated as different letters, and `  Z  ` would come before `  a  ` .

**Example default sorting:** Apple, Zebra, apple

By contrast, collation lets you sort and compare strings case-insensitively or according to specific language rules.

**Example case-insensitive collation:** Apple, apple, Zebra

To customize collation for a collation-supported operation, you typically [assign a collation specification](#collate_define) to at least one string in the operation inputs. Some operations can't use collation, but can [propagate collation through them](#collate_propagate) .

Collation is useful when you need fine-tuned control over how values are sorted, joined, or grouped in tables.

## Operations affected by collation

The following example query operations are affected by collation when sorting and comparing strings:

<table>
<thead>
<tr class="header">
<th>Operations</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Collation-supported <a href="#collate_funcs">comparison operations</a></td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/query-syntax#join_types">Join operations</a></td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/query-syntax#order_by_clause"><code dir="ltr" translate="no">        ORDER BY       </code></a></td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/query-syntax#group_by_clause"><code dir="ltr" translate="no">        GROUP BY       </code></a></td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/query-syntax#window_clause"><code dir="ltr" translate="no">        WINDOW       </code></a> for window functions</td>
</tr>
<tr class="even">
<td>Collation-supported <a href="#collate_funcs">scalar functions</a></td>
</tr>
<tr class="odd">
<td>Collation-supported <a href="#collate_funcs">aggregate functions</a></td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/query-syntax#set_operators">Set operations</a></td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/conditional_expressions#nullif"><code dir="ltr" translate="no">        NULLIF       </code> conditional expression</a></td>
</tr>
</tbody>
</table>

## Operations that propagate collation

Collation can pass through some query operations to other parts of a query. When collation passes through an operation in a query, this is known as *propagation* . During propagation:

  - If an input contains no collation specification or an empty collation specification and another input contains an explicitly defined collation, the explicitly defined collation is used for all of the inputs.
  - All inputs with a non-empty explicitly defined collation specification must have the same type of collation specification, otherwise an error is thrown.

GoogleSQL has several [functions](#functions_propagation) , [operators](#operators_propagation) , and [expressions](#expressions_propagation) that can propagate collation.

In the following example, the `  'und:ci'  ` collation specification is propagated from the `  character  ` column to the `  ORDER BY  ` operation.

``` text
-- With collation
SELECT *
FROM UNNEST([
  COLLATE('B', 'und:ci'),
  'b',
  'a'
]) AS character
ORDER BY character

/*-----------+
 | character |
 +-----------+
 | a         |
 | B         |
 | b         |
 +-----------*/
```

``` text
-- Without collation
SELECT *
FROM UNNEST([
  'B',
  'b',
  'a'
]) AS character
ORDER BY character

/*-----------+
 | character |
 +-----------+
 | B         |
 | a         |
 | b         |
 +-----------*/
```

### Functions

The following example functions propagate collation.

<table>
<thead>
<tr class="header">
<th>Function</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/aead_encryption_functions#aeaddecrypt_string"><code dir="ltr" translate="no">        AEAD.DECRYPT_STRING       </code></a></td>
<td></td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#any_value"><code dir="ltr" translate="no">        ANY_VALUE       </code></a></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#array_agg"><code dir="ltr" translate="no">        ARRAY_AGG       </code></a></td>
<td>Collation on input arguments are propagated as collation on the array element.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/array_functions#array_first"><code dir="ltr" translate="no">        ARRAY_FIRST       </code></a></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/array_functions#array_last"><code dir="ltr" translate="no">        ARRAY_LAST       </code></a></td>
<td></td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/array_functions#array_slice"><code dir="ltr" translate="no">        ARRAY_SLICE       </code></a></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/array_functions#array_to_string"><code dir="ltr" translate="no">        ARRAY_TO_STRING       </code></a></td>
<td>Collation on array elements are propagated to output.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#collate"><code dir="ltr" translate="no">        COLLATE       </code></a></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#concat"><code dir="ltr" translate="no">        CONCAT       </code></a></td>
<td></td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#format_string"><code dir="ltr" translate="no">        FORMAT       </code></a></td>
<td>Collation from <code dir="ltr" translate="no">       format_string      </code> to the returned string is propagated.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/date_functions#format_date"><code dir="ltr" translate="no">        FORMAT_DATE       </code></a></td>
<td>Collation from <code dir="ltr" translate="no">       format_string      </code> to the returned string is propagated.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/datetime_functions#format_datetime"><code dir="ltr" translate="no">        FORMAT_DATETIME       </code></a></td>
<td>Collation from <code dir="ltr" translate="no">       format_string      </code> to the returned string is propagated.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/time_functions#format_time"><code dir="ltr" translate="no">        FORMAT_TIME       </code></a></td>
<td>Collation from <code dir="ltr" translate="no">       format_string      </code> to the returned string is propagated.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/timestamp_functions#format_timestamp"><code dir="ltr" translate="no">        FORMAT_TIMESTAMP       </code></a></td>
<td>Collation from <code dir="ltr" translate="no">       format_string      </code> to the returned string is propagated.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#greatest"><code dir="ltr" translate="no">        GREATEST       </code></a></td>
<td></td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/navigation_functions#lag"><code dir="ltr" translate="no">        LAG       </code></a></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/navigation_functions#lead"><code dir="ltr" translate="no">        LEAD       </code></a></td>
<td></td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#least"><code dir="ltr" translate="no">        LEAST       </code></a></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#left"><code dir="ltr" translate="no">        LEFT       </code></a></td>
<td></td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#lower"><code dir="ltr" translate="no">        LOWER       </code></a></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#lpad"><code dir="ltr" translate="no">        LPAD       </code></a></td>
<td></td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#max"><code dir="ltr" translate="no">        MAX       </code></a></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#min"><code dir="ltr" translate="no">        MIN       </code></a></td>
<td></td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/net_functions#nethost"><code dir="ltr" translate="no">        NET.HOST       </code></a></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/net_functions#netpublic_suffix"><code dir="ltr" translate="no">        NET.PUBLIC_SUFFIX       </code></a></td>
<td></td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/net_functions#netreg_domain"><code dir="ltr" translate="no">        NET.REG_DOMAIN       </code></a></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/navigation_functions#nth_value"><code dir="ltr" translate="no">        NTH_VALUE       </code></a></td>
<td></td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#normalize"><code dir="ltr" translate="no">        NORMALIZE       </code></a></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#normalize_and_casefold"><code dir="ltr" translate="no">        NORMALIZE_AND_CASEFOLD       </code></a></td>
<td></td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#repeat"><code dir="ltr" translate="no">        REPEAT       </code></a></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#replace"><code dir="ltr" translate="no">        REPLACE       </code></a></td>
<td></td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#reverse"><code dir="ltr" translate="no">        REVERSE       </code></a></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#right"><code dir="ltr" translate="no">        RIGHT       </code></a></td>
<td></td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#rpad"><code dir="ltr" translate="no">        RPAD       </code></a></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#soundex"><code dir="ltr" translate="no">        SOUNDEX       </code></a></td>
<td></td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#split"><code dir="ltr" translate="no">        SPLIT       </code></a></td>
<td>Collation on input arguments are propagated as collation on the array element.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#string_agg"><code dir="ltr" translate="no">        STRING_AGG       </code></a></td>
<td></td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#substr"><code dir="ltr" translate="no">        SUBSTR       </code></a></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#upper"><code dir="ltr" translate="no">        UPPER       </code></a></td>
<td></td>
</tr>
</tbody>
</table>

### Operators

The following example operators propagate collation.

<table>
<thead>
<tr class="header">
<th>Operator</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/operators#concatenation_operator"><code dir="ltr" translate="no">        ||       </code> concatenation operator</a></td>
<td></td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/operators#array_subscript_operator">Array subscript operator</a></td>
<td>Propagated to output.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/query-syntax#set_operators">Set operators</a></td>
<td>Collation of an output column is decided by the collations of input columns at the same position.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/operators#field_access_operator"><code dir="ltr" translate="no">        STRUCT       </code> field access operator</a></td>
<td>When getting a <code dir="ltr" translate="no">       STRUCT      </code> , collation on the <code dir="ltr" translate="no">       STRUCT      </code> field is propagated as the output collation.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/query-syntax#unnest_operator"><code dir="ltr" translate="no">        UNNEST       </code></a></td>
<td>Collation on the input array element is propagated to output.</td>
</tr>
</tbody>
</table>

### Expressions

The following example expressions propagate collation.

<table>
<thead>
<tr class="header">
<th>Expression</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/data-types#array_type"><code dir="ltr" translate="no">        ARRAY       </code></a></td>
<td>When you construct an <code dir="ltr" translate="no">       ARRAY      </code> , collation on input arguments is propagated on the elements in the <code dir="ltr" translate="no">       ARRAY      </code> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/conditional_expressions#case"><code dir="ltr" translate="no">        CASE       </code></a></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/conditional_expressions#case_expr"><code dir="ltr" translate="no">        CASE       </code> expr</a></td>
<td></td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/conditional_expressions#coalesce"><code dir="ltr" translate="no">        COALESCE       </code></a></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/conditional_expressions#if"><code dir="ltr" translate="no">        IF       </code></a></td>
<td></td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/conditional_expressions#ifnull"><code dir="ltr" translate="no">        IFNULL       </code></a></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/conditional_expressions#nullif"><code dir="ltr" translate="no">        NULLIF       </code></a></td>
<td></td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/data-types#struct_type"><code dir="ltr" translate="no">        STRUCT       </code></a></td>
<td>When you construct a <code dir="ltr" translate="no">       STRUCT      </code> , collation on input arguments is propagated on the fields in the <code dir="ltr" translate="no">       STRUCT      </code> .</td>
</tr>
</tbody>
</table>

## Additional features that support collation

These features in BigQuery generally support collation:

<table>
<thead>
<tr class="header">
<th>Feature</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="/bigquery/docs/views-intro">Views</a></td>
<td></td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/materialized-views-intro">Materialized views</a></td>
<td>This feature supports collation, but <a href="#limitations">limitations apply</a></td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/table-functions">Table functions</a></td>
<td>This feature supports collation, but <a href="#limitations">limitations apply</a></td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/bi-engine-intro">BI engine</a></td>
<td></td>
</tr>
</tbody>
</table>

## Where you can assign a collation specification

You can assign a [collation specification](#collate_spec_details) to these collation-supported types:

  - A `  STRING  `
  - A `  STRING  ` field in a `  STRUCT  `
  - A `  STRING  ` element in an `  ARRAY  `

In addition:

  - You can assign a default collation specification to a dataset when you create or alter it. This assigns a default collation specification to all future tables that are added to the dataset if the tables don't have their own default collation specifications.
  - You can assign a default collation specification to a table when you create or alter it. This assigns a collation specification to all future collation-supported columns that are added to the table if the columns don't have collation specifications. This overrides a default collation specification on a dataset.
  - You can assign a collation specification to a collation-supported type in a column. A column that contains a collation-supported type in its column dataset is a collation-supported column. This overrides a default collation specification on a table.
  - You can assign a collation specification to a collation-supported query operation.
  - You can assign a collation specification to a collation-supported expression with the `  COLLATE  ` function. This overrides any collation specifications set previously.

In summary:

You can define a default collation specification for a dataset. For example:

``` text
CREATE SCHEMA (...)
DEFAULT COLLATE 'und:ci'
```

You can define a default collation specification for a table. For example:

``` text
CREATE TABLE (...)
DEFAULT COLLATE 'und:ci'
```

You can define a collation specification for a collation-supported column. For example:

``` text
CREATE TABLE (
  case_insensitive_column STRING COLLATE 'und:ci'
)
```

You can specify a collation specification for a collation-supported expression with the `  COLLATE  ` function. For example:

``` text
SELECT COLLATE('a', 'und:ci') AS character
```

### DDL statements

You can assign a collation specification to the following DDL statements.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Location</th>
<th>Support</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Dataset</td>
<td><a href="/bigquery/docs/reference/standard-sql/data-definition-language#create_schema_statement"><code dir="ltr" translate="no">        CREATE SCHEMA       </code></a></td>
<td>Create a dataset and optionally add a default collation specification to the dataset.</td>
</tr>
<tr class="even">
<td>Dataset</td>
<td><a href="/bigquery/docs/reference/standard-sql/data-definition-language#alter_schema_collate_statement"><code dir="ltr" translate="no">        ALTER SCHEMA       </code></a></td>
<td>Updates the default collation specification for a dataset.</td>
</tr>
<tr class="odd">
<td>Table</td>
<td><a href="/bigquery/docs/reference/standard-sql/data-definition-language#create_table_statement"><code dir="ltr" translate="no">        CREATE TABLE       </code></a></td>
<td>Create a table and optionally add a default collation specification to a table or a collation specification to a collation-supported type in a column.<br />
<br />
You can't have collation on a column used with <code dir="ltr" translate="no">       CLUSTERING      </code> .</td>
</tr>
<tr class="even">
<td>Table</td>
<td><a href="/bigquery/docs/reference/standard-sql/data-definition-language#alter_table_collate_statement"><code dir="ltr" translate="no">        ALTER TABLE       </code></a></td>
<td>Update the default collation specification for collation-supported type in a table.</td>
</tr>
<tr class="odd">
<td>Column</td>
<td><a href="/bigquery/docs/reference/standard-sql/data-definition-language#alter_table_add_column_statement"><code dir="ltr" translate="no">        ADD COLUMN       </code></a></td>
<td>Add a collation specification to a collation-supported type in a new column in an existing table.</td>
</tr>
</tbody>
</table>

### Data types

You can assign a collation specification to the following data types.

<table>
<thead>
<tr class="header">
<th>Type</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/data-types#string_type"><code dir="ltr" translate="no">        STRING       </code></a></td>
<td>You can apply a collation specification directly to this data type.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/data-types#struct_type"><code dir="ltr" translate="no">        STRUCT       </code></a></td>
<td>You can apply a collation specification to a <code dir="ltr" translate="no">       STRING      </code> field in a <code dir="ltr" translate="no">       STRUCT      </code> . A <code dir="ltr" translate="no">       STRUCT      </code> can have <code dir="ltr" translate="no">       STRING      </code> fields with different collation specifications. A <code dir="ltr" translate="no">       STRUCT      </code> can only be used in comparisons with the following operators and conditional expressions: <code dir="ltr" translate="no">       =      </code> , <code dir="ltr" translate="no">       !=      </code> , <code dir="ltr" translate="no">       IN      </code> , <code dir="ltr" translate="no">       NULLIF      </code> , and <code dir="ltr" translate="no">       CASE      </code> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/data-types#array_type"><code dir="ltr" translate="no">        ARRAY       </code></a></td>
<td>You can apply a collation specification to a <code dir="ltr" translate="no">       STRING      </code> element in an <code dir="ltr" translate="no">       ARRAY      </code> . An <code dir="ltr" translate="no">       ARRAY      </code> can have <code dir="ltr" translate="no">       STRING      </code> elements with different collation specifications.</td>
</tr>
</tbody>
</table>

**Note:** Use the [`  COLLATE  `](/bigquery/docs/reference/standard-sql/string_functions#collate) function to apply a collation specification to collation-supported expressions.

### Functions, operators, and conditional expressions

You can assign a collation specification to the following functions, operators, and conditional expressions.

#### Functions

<table>
<thead>
<tr class="header">
<th>Type</th>
<th>Support</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Scalar</td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#collate"><code dir="ltr" translate="no">        COLLATE       </code></a></td>
<td></td>
</tr>
<tr class="even">
<td>Scalar</td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#ends_with"><code dir="ltr" translate="no">        ENDS_WITH       </code></a></td>
<td></td>
</tr>
<tr class="odd">
<td>Scalar</td>
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#greatest"><code dir="ltr" translate="no">        GREATEST       </code></a></td>
<td></td>
</tr>
<tr class="even">
<td>Scalar</td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#instr"><code dir="ltr" translate="no">        INSTR       </code></a></td>
<td></td>
</tr>
<tr class="odd">
<td>Scalar</td>
<td><a href="/bigquery/docs/reference/standard-sql/mathematical_functions#least"><code dir="ltr" translate="no">        LEAST       </code></a></td>
<td></td>
</tr>
<tr class="even">
<td>Scalar</td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#replace"><code dir="ltr" translate="no">        REPLACE       </code></a></td>
<td></td>
</tr>
<tr class="odd">
<td>Scalar</td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#split"><code dir="ltr" translate="no">        SPLIT       </code></a></td>
<td></td>
</tr>
<tr class="even">
<td>Scalar</td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#starts_with"><code dir="ltr" translate="no">        STARTS_WITH       </code></a></td>
<td></td>
</tr>
<tr class="odd">
<td>Scalar</td>
<td><a href="/bigquery/docs/reference/standard-sql/string_functions#strpos"><code dir="ltr" translate="no">        STRPOS       </code></a></td>
<td></td>
</tr>
<tr class="even">
<td>Aggregate</td>
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#count"><code dir="ltr" translate="no">        COUNT       </code></a></td>
<td>This operator is only affected by collation when the input includes the <code dir="ltr" translate="no">       DISTINCT      </code> argument.</td>
</tr>
<tr class="odd">
<td>Aggregate</td>
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#max"><code dir="ltr" translate="no">        MAX       </code></a></td>
<td></td>
</tr>
<tr class="even">
<td>Aggregate</td>
<td><a href="/bigquery/docs/reference/standard-sql/aggregate_functions#min"><code dir="ltr" translate="no">        MIN       </code></a></td>
<td></td>
</tr>
</tbody>
</table>

#### Operators

<table>
<thead>
<tr class="header">
<th>Support</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/operators#comparison_operators"><code dir="ltr" translate="no">        &lt;       </code></a></td>
<td></td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/operators#comparison_operators"><code dir="ltr" translate="no">        &lt;=       </code></a></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/operators#comparison_operators"><code dir="ltr" translate="no">        &gt;       </code></a></td>
<td></td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/operators#comparison_operators"><code dir="ltr" translate="no">        &gt;=       </code></a></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/operators#comparison_operators"><code dir="ltr" translate="no">        =       </code></a></td>
<td></td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/operators#comparison_operators"><code dir="ltr" translate="no">        !=       </code></a></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/operators#comparison_operators"><code dir="ltr" translate="no">        [NOT] BETWEEN       </code></a></td>
<td></td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/operators#in_operators"><code dir="ltr" translate="no">        [NOT] IN       </code></a></td>
<td><a href="/bigquery/docs/reference/standard-sql/operators#in_operators">Limitations apply</a> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/operators#like_operator"><code dir="ltr" translate="no">        [NOT] LIKE       </code></a></td>
<td><a href="/bigquery/docs/reference/standard-sql/operators#like_operator">Limitations apply</a> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/operators#like_operator_quantified">Quantified <code dir="ltr" translate="no">        [NOT] LIKE       </code></a></td>
<td><a href="/bigquery/docs/reference/standard-sql/operators#like_operator_quantified">Limitations apply</a> .</td>
</tr>
</tbody>
</table>

#### Conditional expressions

<table>
<thead>
<tr class="header">
<th>Support</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/conditional_expressions#case"><code dir="ltr" translate="no">        CASE       </code></a></td>
<td></td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/conditional_expressions#case_expr"><code dir="ltr" translate="no">        CASE       </code> expr</a></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/conditional_expressions#nullif"><code dir="ltr" translate="no">        NULLIF       </code></a></td>
<td></td>
</tr>
</tbody>
</table>

The preceding collation-supported operations (functions, operators, and conditional expressions) can include input with explicitly defined collation specifications for collation-supported types. In a collation-supported operation:

  - All inputs with a non-empty, explicitly defined collation specification must be the same, otherwise an error is thrown.
  - If an input doesn't contain an explicitly defined collation and another input contains an explicitly defined collation, the explicitly defined collation is used for both.

For example:

``` text
-- Assume there's a table with this column declaration:
CREATE TABLE table_a
(
    col_a STRING COLLATE 'und:ci',
    col_b STRING COLLATE '',
    col_c STRING,
    col_d STRING COLLATE 'und:ci'
);

-- This runs. Column 'b' has a collation specification and the
-- column 'c' doesn't.
SELECT STARTS_WITH(col_b_expression, col_c_expression)
FROM table_a;

-- This runs. Column 'a' and 'd' have the same collation specification.
SELECT STARTS_WITH(col_a_expression, col_d_expression)
FROM table_a;

-- This runs. Even though column 'a' and 'b' have different
-- collation specifications, column 'b' is considered the default collation
-- because it's assigned to an empty collation specification.
SELECT STARTS_WITH(col_a_expression, col_b_expression)
FROM table_a;

-- This works. Even though column 'a' and 'b' have different
-- collation specifications, column 'b' is updated to use the same
-- collation specification as column 'a'.
SELECT STARTS_WITH(col_a_expression, COLLATE(col_b_expression, 'und:ci'))
FROM table_a;

-- This runs. Column 'c' doesn't have a collation specification, so it uses the
-- collation specification of column 'd'.
SELECT STARTS_WITH(col_c_expression, col_d_expression)
FROM table_a;
```

## Collation specification details

A collation specification determines how strings are sorted and compared in [collation-supported operations](#collate_operations) . You can define the [Unicode collation specification](#unicode_collation) , `  und:ci  ` , for [collation-supported types](#collate_define) .

If a collation specification isn't defined, the default collation specification is used. To learn more, see the next section.

### Default collation specification

When a collation specification isn't assigned or is empty, `  'binary'  ` collation is used. Binary collation indicates that the operation should return data in [Unicode code point order](https://en.wikipedia.org/wiki/List_of_Unicode_characters) . You can't set binary collation explicitly.

In general, the following behavior occurs when an empty string is included in collation:

  - If a string has `  und:ci  ` collation, the string comparison is case-insensitive.
  - If a string has empty collation, the string comparison is case-sensitive.
  - If string not assigned collation, the string comparison is case-sensitive.
  - A column with unassigned collation inherit the table's default collation.
  - A column with empty collation doesn't inherit the table's default collation.

### Unicode collation specification

``` text
collation_specification:
  'language_tag:collation_attribute'
```

A unicode collation specification indicates that the operation should use the [Unicode Collation Algorithm](http://www.unicode.org/reports/tr10/) to sort and compare strings. The collation specification can be a `  STRING  ` literal or a query parameter.

#### The language tag

The language tag determines how strings are generally sorted and compared. Allowed values for `  language_tag  ` are:

  - `  und  ` : A locale string representing the *undetermined* locale. `  und  ` is a special language tag defined in the [IANA language subtag registry](https://www.iana.org/assignments/language-subtag-registry/language-subtag-registry) and used to indicate an undetermined locale. This is also known as the *root* locale and can be considered the *default* Unicode collation. It defines a reasonable, locale agnostic collation.

#### The collation attribute

In addition to the language tag, the unicode collation specification must have a `  collation_attribute  ` , which enables additional rules for sorting and comparing strings. Allowed values are:

  - `  ci  ` : Collation is case-insensitive.

#### Collation specification example

This is what the `  ci  ` collation attribute looks like when used with the `  und  ` language tag in the `  COLLATE  ` function:

``` text
COLLATE('orange1', 'und:ci')
```

#### Caveats

  - Differing strings can be considered equal. For instance, `  ẞ  ` (LATIN CAPITAL LETTER SHARP S) is considered equal to `  'SS'  ` in some contexts. The following expressions both evaluate to `  TRUE  ` :
    
      - `  COLLATE('ẞ', 'und:ci') > COLLATE('SS', 'und:ci')  `
      - `  COLLATE('ẞ1', 'und:ci') < COLLATE('SS2', 'und:ci')  `
    
    This is similar to how case insensitivity works.

  - In search operations, strings with different lengths could be considered equal. To ensure consistency, collation should be used without search tailoring.

  - There are a wide range of unicode code points (punctuation, symbols, etc), that are treated as if they aren't there. So strings with and without them are sorted identically. For example, the format control code point `  U+2060  ` is ignored when the following strings are sorted:
    
    ``` text
    SELECT *
    FROM UNNEST([
      COLLATE('oran\u2060ge1', 'und:ci'),
      COLLATE('\u2060orange2', 'und:ci'),
      COLLATE('orange3', 'und:ci')
    ]) AS fruit
    ORDER BY fruit
    
    /*---------+
    | fruit   |
    +---------+
    | orange1 |
    | orange2 |
    | orange3 |
    +---------*/
    ```

  - Ordering *may* change. The Unicode specification of the `  und  ` collation can change occasionally, which can affect sorting order.

## Limitations

Limitations for supported features are captured in the previous sections, but here are a few general limitations to keep in mind:

  - `  und:ci  ` and empty collation are supported, but not other collation specifications.

  - Operations and functions that don't support collation produce an error if they encounter collated values.

  - You can't set non-empty collation on a clustering field.
    
    ``` text
    CREATE TABLE my_dataset.my_table
    (
      word STRING COLLATE 'und:ci',
      number INT64
    )
    CLUSTER BY word;
    
    -- User error:
    -- "CLUSTER BY STRING column word with
    -- collation und:ci isn't supported"
    ```

  - You can't create a materialized view with collated sort keys in an aggregate function.
    
    ``` text
    CREATE MATERIALIZED VIEW my_dataset.my_view
    AS SELECT
      -- Assume collated_table.col_ci is a string column with 'und:ci' collation.
      ARRAY_AGG(col_int64 ORDER BY col_ci) AS col_int64_arr
    FROM my_dataset.collated_table;
    
    -- User error:
    -- "Sort key with collation in aggregate function array_agg isn't
    -- supported in materialized view"
    ```

  - If a materialized view has joined on collated columns and not all of the collated columns were produced by the materialized view, it's possible that a query with the materialized view will use data from base tables rather than the materialized view.
    
    ``` text
    CREATE MATERIALIZED VIEW my_dataset.my_mv
    AS SELECT
      t1.col_ci AS t1_col_ci,
      t2.col_int64 AS t2_col_int64
    FROM my_dataset.collated_table1 AS t1
    JOIN my_dataset.collated_table2 AS t2
    ON t1.col_ci = t2.col_ci
    
    SELECT * FROM my_dataset.my_mv
    WHERE t1_col_ci = 'abc'
    
    -- Assuming collated_table1.col_ci and collated_table2.col_ci are columns
    -- with 'und:ci' collation, the query to my_mv may use data from
    -- collated_table1 and collated_table2, rather than data from my_mv.
    ```

  - Table functions can't take collated arguments.
    
    ``` text
    CREATE TABLE FUNCTION my_dataset.my_tvf(x STRING) AS (
      SELECT x
    );
    
    SELECT * FROM my_dataset.my_tvf(COLLATE('abc', 'und:ci'));
    
    -- User error:
    -- "Collation 'und:ci' on argument of TVF call isn't allowed"
    ```

  - A table function with collated output columns isn't supported if an explicit result schema is present.
    
    ``` text
    CREATE TABLE FUNCTION my_dataset.my_tvf(x STRING)
    RETURNS TABLE<output_str STRING>
    AS (SELECT COLLATE(x, 'und:ci') AS output_str);
    
    -- User error:
    -- "Collation 'und:ci' on output column output_str isn't allowed when an
    -- explicit result schema is present"
    ```

  - User-defined functions (UDFs) can't take collated arguments.
    
    ``` text
    CREATE FUNCTION tmp_dataset.my_udf(x STRING) AS (x);
    
    SELECT tmp_dataset.my_udf(col_ci)
    FROM shared_dataset.table_collation_simple;
    
    -- User error:
    -- "Collation isn't allowed on argument x ('und:ci').
    -- Use COLLATE(arg, '') to remove collation at [1:8]"
    ```

  - Collation in the return type of a user-defined function body isn't allowed.
    
    ``` text
    CREATE FUNCTION my_dataset.my_udf(x STRING) AS (COLLATE(x, 'und:ci'));
    
    -- User error:
    -- "Collation ['und:ci'] in return type of user-defined function body is
    -- not allowed"
    ```

  - [External tables](/bigquery/docs/external-data-sources) don't support collation.
