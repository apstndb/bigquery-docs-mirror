# Overview of logical and materialized views

This document describes and compares logical and materialized views in BigQuery. In modern data warehousing, views serve as an important abstraction layer between raw data and business intelligence. Within BigQuery, architects typically choose between two types: logical (standard) views and materialized views. While these views share a common interface, their underlying mechanics, performance profiles, and cost implications differ.

## Logical views

A logical (standard) view is a virtual table defined by a SQL query. It does not store any physical data; instead, it stores the query logic required to retrieve data from the underlying base tables.

When you query a logical view, the BigQuery query engine expands the view into its underlying query. This process means BigQuery re-executes the view every time it is called.

The benefits of logical views include the following:

  - **No storage overhead.** Because no additional data is stored, you pay only for the storage of the base tables.
  - **Real-time accuracy.** Because the query runs at execution time, results always reflect the most current state of the base tables.
  - **Logical abstraction.** Simplifies complex joins or applies row-level security without duplicating data.
  - **SQL flexibility.** Supports the full range of BigQuery SQL, including complex window functions, user-defined functions (UDFs), and all join types.

## Materialized views

Materialized views are precomputed views that periodically store the results of a SQL query. Unlike logical views, they physically store the computed data, which lets BigQuery serve results faster without repeatedly processing the raw base data. This can reduce query latency for large datasets by pre-processing queries and can reduce compute costs for frequently used queries.

BigQuery materialized views combine the speed of precomputed data with the accuracy of a live view. They achieve this through the following:

  - **Automatic refresh.** A background process updates the materialized views when base tables change.
  - **Data freshness.** If a query occurs while a background refresh is pending, BigQuery automatically compensates for the unprocessed base table changes to provide up-to-date results.
  - **Smart tuning.** The query optimizer can automatically reroute queries from base tables to the materialized view if it determines the materialized view can provide the answer more efficiently.

## Comparison

The following table summarizes the similarities and differences between BigQuery logical views and materialized views:

<table>
<thead>
<tr class="header">
<th><strong>Dimension</strong></th>
<th><strong>Logical view</strong></th>
<th><strong>Materialized view</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Data Persistence</strong></td>
<td>None (virtual)</td>
<td>Physical (stored on disk)</td>
</tr>
<tr class="even">
<td><strong>Execution</strong></td>
<td>Every time the view is called</td>
<td>Precomputed; background refresh</td>
</tr>
<tr class="odd">
<td><strong>Data Staleness</strong></td>
<td>Never</td>
<td>Optional <sup>1</sup> (via refresh)</td>
</tr>
<tr class="even">
<td><strong>Performance</strong></td>
<td>Variable (base table dependent)</td>
<td>Consistent and fast</td>
</tr>
<tr class="odd">
<td><strong>SQL Complexity</strong></td>
<td>Unlimited</td>
<td><a href="/bigquery/docs/materialized-views-create">Limited</a></td>
</tr>
<tr class="even">
<td><strong>Optimized For</strong></td>
<td>Security and abstraction</td>
<td>Speed and cost reduction</td>
</tr>
<tr class="odd">
<td><strong>Maintenance &amp; storage costs</strong></td>
<td>No</td>
<td>Yes</td>
</tr>
</tbody>
</table>

<sup>1</sup> The [`  --max_staleness  ` option](/bigquery/docs/materialized-views-create#max_staleness) improves query performance with controlled costs when processing large, frequently changing datasets.

### When to use logical views

  - **Semantic layering** . Rename complex column names into business-friendly terms for non-technical users.
  - **Rapid development** . Use when logic is in flux and you don't want to manage the overhead of physical storage.
  - **Consolidated data sources** . Provide a data source for visualization tools such as [Looker Studio](/looker/docs) or [BigQuery sharing (formerly Analytics Hub)](/bigquery/docs/analytics-hub-introduction) .

### When to use materialized views

  - **Pre-process data** . Improve query performance by preparing aggregates, filters, joins, and clusters.
  - **Dashboard acceleration** . Empower BI tools like Looker that frequently query the same aggregate metrics—for example, daily active users.
  - **Real-time analytics on large streams** . Can provide faster responses on tables that receive high-velocity streaming data.
  - **Cost management** . Reduce the cost of repetitive, expensive queries over large datasets.

## Best practices

For a well-architected BigQuery environment, *logical views* are a useful tool for consolidating the data you need. Reserve *materialized views* for use as a performance optimization tool for specific, high-traffic query patterns that involve heavy aggregation.

To learn how to monitor the use and performance of materialized views, see [`  MATERIALIZED_VIEWS  ` view](/bigquery/docs/information-schema-materialized-views) .

## What's next

  - [Introduction to logical views](/bigquery/docs/views-intro)
  - [Create logical views](/bigquery/docs/views)
  - [Introduction to materialized views](/bigquery/docs/materialized-views-intro)
  - [Create materialized views](/bigquery/docs/materialized-views-create)
