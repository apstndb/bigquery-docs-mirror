---
name: documents/docs.cloud.google.com/bigquery/docs/column-aliases
uri: https://docs.cloud.google.com/bigquery/docs/column-aliases
title: Work with reusable column aliases
description: Learn about using an alias for an expression in the SELECT clause of a SQL query and immediately reference that alias in the same SELECT list or in the query's WHERE clause.
data_source: docs.cloud.google.com
---

# Work with reusable column aliases

GoogleSQL in BigQuery supports reusable column aliases. A reusable column alias lets you define an alias for an expression in the `SELECT` clause of a SQL query and immediately reference that alias within the same `SELECT` list or in the `WHERE` clause of the same query block.

For example, the following query shows you how to filter results based on a calculation, such as `gross_price` . You can reference the alias `gross_price` directly in the `WHERE` clause instead of repeating the calculation in the `WHERE` clause or using a subquery:

```
SELECT
  net_price * 1.23 as gross_price
FROM
  product
WHERE
  gross_price < 10.0
```

Reusable column aliases provide you with:

- **Simplified SQL syntax** : you can write clean, concise, left-to-right calculations without repeating complex expressions or wrapping queries in subqueries.
- **Improved readability** : analysts and developers can declare an expression once and then reuse it immediately. This makes queries easier to read, debug, and maintain.

## Enable or disable reusable column aliases

> **Important:** Before you enable reusable column aliases, evaluate their impact on your existing workloads. Column aliases change a query's [name resolution order](https://docs.cloud.google.com/bigquery/docs/column-aliases#name-resolution-order) .

By default, reusable column aliases are disabled. To use column aliases, your BigQuery administrator must enable the feature by setting the `reusable_column_aliases_mode` option to `on` using one of the following Data definition language (DDL) statements:

- To enable column aliases at the organization level, use the [ALTER ORGANIZATION SET OPTIONS statement](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#alter_organization_set_options_statement) .

- To enable column aliases at the project level, use the [ALTER PROJECT SET OPTIONS statement](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#alter_project_set_options_statement) .

To set this configuration option, you need the BigQuery Admin ( `roles/bigquery.admin` ) role, or the `bigquery.projects.update` permission on the project or `bigquery.organizations.update` permission on the organization. For information on the permissions required to set configuration options, see [Required permissions](https://docs.cloud.google.com/bigquery/docs/default-configuration#required_permissions) on the Manage configuration settings page.

To disable reusable column aliases, set `reusable_column_aliases_mode` to `off` . If you set the value to `NULL` , the system default is used, and the feature is also disabled.

### Examples

To enable reusable column aliases at the organization level, enter the following DDL statement:

```
ALTER ORGANIZATION
SET OPTIONS (
  `region-REGION.reusable_column_aliases_mode` = "on"
);
```

Replace ` REGION ` with your region.

To enable reusable column aliases at the project level, enter the following DDL statement:

```
ALTER PROJECT PROJECT_ID
SET OPTIONS (
  `region-REGION.reusable_column_aliases_mode` = "on"
);
```

Replace the following:

- ` REGION ` : your region.
- ` PROJECT_ID ` : your project ID.

### Verify whether column aliases are enabled or disabled

You can verify whether reusable column aliases are enabled or disabled at the project or organization level by querying the following information schema views:

- [`PROJECT_OPTIONS`](https://docs.cloud.google.com/bigquery/docs/information-schema-project-options)
- [`ORGANIZATION_OPTIONS`](https://docs.cloud.google.com/bigquery/docs/information-schema-organization-options)
- [`EFFECTIVE_PROJECT_OPTIONS`](https://docs.cloud.google.com/bigquery/docs/information-schema-effective-project-options)

For more information on working with information schema views, see [Introduction to `INFORMATION_SCHEMA`](https://docs.cloud.google.com/bigquery/docs/information-schema-intro) .

## How to use reusable column aliases

You can use an alias—an identifier assigned to an expression—in a `WHERE` clause or a `SELECT` clause:

- `WHERE` clause: Filtering based on a calculated column defined in the SELECT list.
- `SELECT` clause: Using a calculated alias to define another alias within the same projection list or to determine what data is returned by the query.

### Example

This example shows you how to use reusable column aliases to calculate a value based on another calculation you defined earlier in the `SELECT` list. The query also shows you how to refer to the alias in the `WHERE` clause:

```
SELECT
  net_price * 1.23 as gross_price,
  gross_price * 0.5 as discounted_gross_price
FROM
  product
WHERE
  discounted_gross_price < 10.0;
```

## Behavioral changes (semantic drift) in query name resolution order

An identifier name can exist as a physical column in your table *and* as an alias you create so you should consider the query's name resolution order. BigQuery resolves names in the following order:

1.  **Column name** : Existing columns in the table always have the highest priority.
2.  **Alias** : the alias defined in the query.
3.  **Outer query column** : columns from a parent query.
4.  **Function argument** : if it's running within a user-defined function (UDF) or a table-valued function (TVF).
5.  **Script variables** : variables defined in a script.

Based on this order, if your table has a column named `gross_price` , and you create an alias named `gross_price` , the query uses the column value, not your alias.

This means that if you have an outer query column, function argument, or script variable with the same name as an alias you define in your SELECT clause, BigQuery uses the **alias** value for calculations instead of the variable or argument.

### Examples of how name resolution order works

The following examples show how name resolution order works with reusable column aliases when there are naming conflicts.

#### Conflict with an outer query column

If you don't enable reusable column aliases, an alias defined in the `SELECT` clause that has the same name as a column in the outer query results in the outer query column being used. With reusable column aliases enabled, the alias "shadows" the outer query column within the query scope.

In the following example, a nested query uses aliases and has access to the columns from the outer query:

```
SELECT
  name,
  net_price,
  category_id, -- table product has category_id column
  (SELECT 100 AS category_id -- alias defined with the same name
     FROM category c
     WHERE
       id = category_id  -- Now the alias category_id is used here, not the outer query column
  ) as X
FROM
  product;
```

If you don't enable reusable column aliases, the subquery uses the `category_id` column from the `product` table in the outer query. As a result, the `category_id` value varies by row. If you enable reusable column aliases, the query uses the alias value of `100` for all rows.

#### Conflict with function arguments

If a query is running inside a User-Defined Function (UDF), an alias defined within that query has precedence over the function's arguments.

In the following example, the `calculate_metric` function has an input argument named `val` :

```
CREATE TEMP FUNCTION calculate_metric(val INT64) AS ((
  SELECT AS STRUCT
    5 AS val,       -- Alias defined as constant 5
    val + 10        -- Reference to 'val'
));

-- Calling the function with argument 100
SELECT calculate_metric(100);
```

If you don't enable reusable column aliases, the query uses the argument value passed to the function ( `100` ), and the result is calculated as `110 (100 + 10)` . If you enable reusable column aliases, the query uses the alias defined in the `SELECT` list ( `5` ), and the result is calculated as `15 (5 + 10)` .

#### Conflict with script variables

If you don't enable reusable column aliases, and you have an alias defined in the `SELECT` clause that has the same name as a script variable, the script variable is used. If you enable reusable column aliases, the alias shadows the variable within the query scope.

The following example declares a variable named `gross_price` that has a default value of `10.0` . The query also calculates a column and aliases it as `gross_price` :

```
DECLARE gross_price NUMERIC DEFAULT 10.0;

SELECT
  net_price * 1.23 AS gross_price,
  -- Usage of 'gross_price' here determines the behavior
  gross_price * 0.5 AS discounted_gross_price
FROM
  product;
```

If you don't enable reusable column aliases, the query uses the variable value of `10.0` . The result is a `discounted_gross_price` value of `5.0` that is a constant for all rows. The result is calculated as `10.0 * 0.5 = 5.0` .

If you enable reusable column aliases, the query uses the alias value of `net_price * 1.23` . The result is a `discounted_gross_price` value that varies per row. The result is calculated as `(net_price * 1.23) * 0.5` .

## Best practices

When you use reusable column aliases, consider the following best practices:

- Before you enable reusable column aliases, evaluate their impact on your existing workloads.
- To prevent unintended behavior or silent behavioral changes (semantic drift), don't use the name of your script variables, function arguments, or columns in outer queries as the name of your alias.
- If you are migrating SQL from a source dialect that supports aliasing semantics such as Teradata or Snowflake, follow the [SQL translation instructions](https://docs.cloud.google.com/bigquery/docs/column-aliases#translating-sql-with-migration-service) before you start your migration.

## Troubleshooting column aliases

The following examples show you how to troubleshoot common issues with reusable column aliases.

**Issue** : You get unexpected query results or the alias appears to be ignored.

**Resolution** : Verify the [name resolution order](https://docs.cloud.google.com/bigquery/docs/column-aliases#name-resolution-order) . If your table contains a column with the same name as your alias, the column name has higher priority than the alias. Give your alias a unique name to avoid this conflict.

**Error** : `Column not found` .

**Resolution** : Ensure that you aren't using a forward reference. You can only reference an alias that was defined prior to its usage. This is evaluated from left to right.

**Error** : `Column name is ambiguous` .

**Resolution** : Ensure the alias name isn't defined more than once in the same `SELECT` list before it's referenced.

## Limitations

Reusable column aliases are subject to the following limitations:

- When a query includes grouping or aggregation, aliases to unaggregated expressions (grouping columns or projections of grouping columns) aren't allowed in the `WHERE` clause or as arguments to aggregate functions. In the following query, alias `b` improperly refers to an expression that includes `a` , which is a grouping column:

  ```
  SELECT a+1 as b, sum(b) -- sum(b) is invalid.
  FROM t
  WHERE b > 5         -- Referencing b under WHERE clause is not allowed.
  GROUP BY a
  ```

- Aliases that reference an aggregate or window function directly or transitively, can't be used in the `WHERE` clause or as arguments to other aggregate functions. In the following query, alias `x` improperly refers to an aggregate function:

  ```
  SELECT sum(a) AS x, sum(x) -- sum(x) is invalid.
  FROM t
  WHERE x > 0          -- Referencing x under WHERE clause is not allowed.
  ```

- Applying a window function over an alias which refers to another window function directly or transitively, isn't allowed. In the following query, alias `x` refers to a window function which is invalid:

  ```
  SELECT count(*) over() AS x, sum(x) over() -- sum(x) over() is invalid.
  FROM t
  ```

- Reusable column aliases aren't supported by [pipe syntax](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/pipe-syntax) .

- Reusable column aliases aren't supported by [Graph Query Language (GQL)](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/graph-intro) .
