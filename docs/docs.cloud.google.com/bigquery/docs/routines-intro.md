# Introduction to routines

This document describes how to choose a routine, which is a resource type that you use to create functions or stored procedures in BigQuery.

## Supported routines

BigQuery supports the following routines:

  - [User-defined functions](/bigquery/docs/user-defined-functions) (UDFs)
  - [User-defined aggregate functions](/bigquery/docs/user-defined-aggregates) (UDAFs)
  - [Table functions](/bigquery/docs/table-functions)
  - [Remote functions](/bigquery/docs/remote-functions)
  - [Stored procedures](/bigquery/docs/procedures)

## How to choose a routine

This section describes factors to consider when choosing a routine and compares routines by task.

### Factors to consider

To choose a routine, consider the following factors, which are described in the sections for each type of routine:

  - The type of task to implement.
  - The programming language to use.
  - The type of persistence to implement for the routine: temporary or persistent.
  - The type of reuse required for the routine: across single or multiple queries.
  - Performance considerations.
  - Accessing external services.
  - Sharing the routine with users.

### Compare routines by task

The following table shows the type of tasks you can perform for each type of routine:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p><strong>Task</strong></p></th>
<th><p><strong>Routine resource type</strong></p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Create functions that perform general-purpose tasks in BigQuery.</p></td>
<td><p>SQL or Javascript UDF</p>
<p>SQL or Javascript UDAF</p></td>
</tr>
<tr class="even">
<td><p>Create functions that perform general-purpose tasks in BigQuery and that communicate with external Google Cloud systems using a <a href="/bigquery/docs/create-cloud-resource-connection">Cloud resource connection</a> .</p></td>
<td><p>Python UDF</p></td>
</tr>
<tr class="odd">
<td><p>Create functions that aggregate data.</p></td>
<td><p>UDAFs</p></td>
</tr>
<tr class="even">
<td><p>Create a table using parameters.</p></td>
<td><p>Table functions</p></td>
</tr>
<tr class="odd">
<td><p>Create functions that use languages, libraries, or services that are unsupported in BigQuery. These functions directly integrate with <a href="/functions/docs/concepts/overview">Cloud Run functions</a> and <a href="/run/docs/overview/what-is-cloud-run">Cloud Run</a> .</p></td>
<td><p>Remote functions</p></td>
</tr>
<tr class="even">
<td><p>Execute multiple statements in one query as a multi-statement query using <a href="/bigquery/docs/reference/standard-sql/procedural-language">procedural language</a> . You can use a multi-statement query to do the following:</p>
<ul>
<li>Run multiple statements in a sequence, with shared state.</li>
<li>Automate management tasks such as creating or dropping tables.</li>
<li>Implement complex logic using programming constructs such as <code dir="ltr" translate="no">         IF        </code> and <code dir="ltr" translate="no">         WHILE        </code> .</li>
</ul>
<p>Create and call stored procedures for Apache Spark in BigQuery.</p></td>
<td><p>Stored procedures</p></td>
</tr>
</tbody>
</table>

## User-defined functions (UDFs)

A UDF lets you create a function by using a SQL expression, JavaScript code, or Python code. UDFs accept columns of input, perform actions on the input, and return the result of those actions as a value.

You can define UDFs as either persistent or temporary. You can reuse persistent UDFs across multiple queries, while temporary UDFs only exist in the scope of a single query.

You can create UDFs for use with [custom masking routines](/bigquery/docs/column-data-masking-intro#custom_mask) , which return a column's value after applying a UDF to the column. After you create the custom masking routine, it's available as a masking rule in [Create data policies](/bigquery/docs/column-data-masking#create_data_policies) .

For more information about UDFs, see the following resources:

  - [User-defined functions](/bigquery/docs/user-defined-functions)
  - [User-defined functions in legacy SQL](/bigquery/docs/user-defined-functions-legacy)
  - [Compare UDFs and UDAFs](#compare-udfs)

### Language-based UDFs

  - *SQL-based UDFs* support [templated UDF parameters](/bigquery/docs/user-defined-functions#templated-sql-udf-parameters) , which can match more than one argument type when the UDF is called. SQL UDFs can also return the value of a [scalar subquery](/bigquery/docs/reference/standard-sql/subqueries#scalar_subquery_concepts) .
  - *Javascript-based UDFs* let you call code written in JavaScript from a SQL query.
      - JavaScript UDFs typically consume more slot resources as compared to standard SQL queries, decreasing job performance.
      - If the function can be expressed in SQL, it's often more optimal to run the code as a standard SQL query job.
  - *Python-based UDFs* are built and run on BigQuery managed resources. These UDFs let you implement a function in Python and use it in a SQL query.
      - You can [access a Google Cloud service or an external service](/bigquery/docs/user-defined-functions-python#use-online-service) from a Python UDF by using the [Cloud resource connection](/bigquery/docs/create-cloud-resource-connection) service account.
      - You can also install third-party libraries from from [the Python Package Index (PyPI)](https://pypi.org/) .

### Community contributed UDFs

In addition to the UDFs you create, community contributed UDFs are available in the `  bigquery-public-data.persistent_udfs  ` public dataset and the open source [`  bigquery-utils  ` GitHub repository](https://github.com/GoogleCloudPlatform/bigquery-utils) .

## User-defined aggregate functions (UDAFs)

A UDAF lets you create an aggregate function by using an expression that contains SQL or Javascript code. A UDAF accepts columns of input, performs a calculation on a group of rows at a time, and then returns the result of that calculation as a single value.

UDAFs can't mutate data, talk to external systems, or send logs to Google Cloud Observability or similar applications.

For more information, see the following resources:

  - [User-defined aggregate functions](/bigquery/docs/user-defined-aggregates)
  - [Limitations](/bigquery/docs/user-defined-aggregates#limitations)
  - [SQL aggregate functions reference](/bigquery/docs/reference/standard-sql/aggregate_functions)

### SQL UDAFs

SQL UDAFs normally aggregate function parameters across all rows in a [group](/bigquery/docs/reference/standard-sql/query-syntax#group_by_clause) . However, you can specify a function parameter as non-aggregate by using the `  NOT AGGREGATE  ` keyword. A non-aggregate function parameter is a scalar function parameter with a constant value for all rows in a group. SQL UDAFs can contain both aggregate and non-aggregate parameters.

### Javascript UDAFs

Javascript UDAFs can include Javascript libraries. The JavaScript function body can include custom JavaScript code such as JavaScript global variables and custom functions.

Because Javascript-based functions typically use more resources, consulting these [performance tips](/bigquery/docs/user-defined-aggregates#performance-tips) can be helpful.

Javascript UDAFs have some constraints. Only [specific type encodings are allowed](/bigquery/docs/user-defined-aggregates#javascript-type-encodings) , and there are [requirements](/bigquery/docs/user-defined-aggregates#serialize-javascript-udaf) for serialization and deserialization.

## Compare UDFs and UDAFs

Choosing a UDF rather than choosing a UDAF depends on the specific task that you are trying to perform.

  - To perform a calculation or transformation on individual data values, use a UDF.
  - To do the same on groups of data values, use a UDAF.

For example, if you want to calculate the average of a column of numbers, then use a UDAF. If you want to convert a column of strings to uppercase, then use a UDF.

UDFs and UDAFs have the following similarities:

  - UDFs and UDAFs can't mutate data, talk to external systems, or send logs to Google Cloud Observability or similar applications. The exception is Python UDFs, which can access external services using a Cloud resource connection. However, Python UDFs don't support [VPC service controls](/vpc-service-controls/docs/overview) or [customer-managed encryption keys (CMEK)](/kms/docs/cmek) .
  - UDAFs have the same limitations as UDFs, plus [a few more](/bigquery/docs/user-defined-aggregates#limitations) .
  - UDFs and UDAFs have the same [quotas and limits](/bigquery/quotas#udf_limits) .

UDFs and UDAFs have the following differences:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><p><strong>Attribute</strong></p></th>
<th><p><strong>UDFs</strong></p></th>
<th><p><strong>UDAFs</strong></p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Definition</p></td>
<td><p>User-defined functions (UDFs) accept columns of input, perform actions on the input, and return the result of those actions as a value.</p></td>
<td><p>User-defined aggregate functions (UDAFs) accept columns of input, perform a calculation on a group of rows at a time, and then return the result of that calculation as a single value.</p></td>
</tr>
<tr class="even">
<td><p>Languages supported</p></td>
<td><p>SQL, Javascript, and Python</p></td>
<td><p>SQL and Javascript</p></td>
</tr>
<tr class="odd">
<td><p>Persistence</p></td>
<td><ul>
<li>Can be temporary or persistent.</li>
<li>You can use persistent UDFs across multiple queries.</li>
<li>You can use temporary UDFs for only a single query.</li>
<li>Python UDFs can only be persistent, not temporary.</li>
</ul></td>
<td><ul>
<li>Can be temporary or persistent.</li>
<li>You can use persistent UDAFs across multiple queries.</li>
<li>You can use temporary UDAFs for only a single query, script, session or procedure.</li>
<li>Persistent UDAFs are safe to call when they are shared between owners.</li>
</ul></td>
</tr>
<tr class="even">
<td><p>Arguments and data types</p></td>
<td><p>UDFs accept parameter values that conform to GoogleSQL for BigQuery <a href="/bigquery/docs/reference/standard-sql/data-types">data types</a> . Some SQL types have a direct mapping to JavaScript types, but others don't. See <a href="/bigquery/docs/user-defined-functions#supported-javascript-udf-data-types">supported types for Javascript</a> .</p>
<p>For a SQL UDF, parameter values can be <code dir="ltr" translate="no">        ANY TYPE       </code> , which can match more than one argument type when the function is called.</p>
<p>Only Javascript UDFs have a determinism specifier that provides a hint to BigQuery as to whether the query result can be cached.</p></td>
<td><p>SQL and Javascript UDAFs accept parameters values that conform to GoogleSQL for BigQuery <a href="/bigquery/docs/reference/standard-sql/data-types">data types</a> .</p>
<p>Function parameters can be aggregate or non-aggregate.</p></td>
</tr>
<tr class="odd">
<td><p>Usage</p></td>
<td><p>UDFs are commonly used for data cleaning, transformation, and validation.</p></td>
<td><p>UDAFs are commonly used for calculating summary statistics, such as averages, sums, and counts.</p></td>
</tr>
</tbody>
</table>

## Table functions

A table function, also called a table-valued function (TVF), is a UDF that returns a table. You can use a table function anywhere that you can use a table. Table functions behave similarly to views, but a table function can take parameters.

You can do the following with table functions:

  - Pass in multiple parameters.
  - Call a table function in any context where a table is valid.
  - Join the output from a table function with another table.
  - Use a table function in a [subquery](/bigquery/docs/reference/standard-sql/subqueries#array_subquery_concepts) .

For more information about table functions, see [Table functions](/bigquery/docs/table-functions) , [Limitations](/bigquery/docs/table-functions#limitations) , and [Quotas and limits](/bigquery/quotas#table_function_limits) .

## Remote functions

Remote functions enable you to implement your function in languages other than SQL and Javascript, or enable you to use libraries or services that are not supported in BigQuery UDFs.

A BigQuery remote function integrates your Google SQL function with [Cloud Run functions](/functions/docs/concepts/overview) and [Cloud Run](/run/docs/overview/what-is-cloud-run) using any supported language, and then invokes those functions from Google SQL queries.

The following tasks are examples of what you can do with remote functions:

  - [Analyze unstructured data in object tables](/bigquery/docs/object-table-remote-function) .
  - [Perform content translation](/bigquery/docs/remote-functions-translation-tutorial) .

Creating a remote function requires the following steps:

1.  Create the HTTP endpoint in Cloud Run functions or Cloud Run.
2.  Create a remote function in BigQuery using the `  CLOUD_RESOURCE  ` connection type.
3.  Use the remote function in a query just like any other UDF for BigQuery.

For more information about remote functions, see [Remote functions](/bigquery/docs/remote-functions) , [Limitations](/bigquery/docs/remote-functions#limitations) , and [Quotas and limits](/bigquery/quotas#remote_function_limits) .

## Stored procedures

A SQL stored procedure is a collection of statements that can be called from other queries or other stored procedures. You name and store a procedure in a BigQuery dataset.

Stored procedures support procedural language statements, which let you do things like define variables and implement control flow. You can learn more about procedural language statements in the [Procedural language reference](/bigquery/docs/reference/standard-sql/procedural-language) .

A stored procedure can do the following:

  - Take input arguments and return values as output.
  - Access or modify data across multiple datasets by multiple users.
  - Contain a [multi-statement query](/bigquery/docs/multi-statement-queries) .

Some stored procedures are built into BigQuery and don't need to be created. These are called system procedures, and you can learn more about them in the [System procedures reference](/bigquery/docs/reference/system-procedures) .

Stored procedures for [Spark in BigQuery](/bigquery/docs/spark-procedures) are also supported. These procedures have [quotas and limits](/bigquery/quotas#spark-procedure) .

To learn more about stored procedures, see [SQL stored procedures](/bigquery/docs/procedures) .
