# Introduction to logical views

This document provides an overview of BigQuery support for logical views. A view is a virtual table defined by a SQL query. The default type of view for BigQuery is a *logical view* . Query results contain only the data from the tables and fields specified in the query that defines the view.

The query that defines a view is run each time the view is queried.

Common use cases for views include the following:

  - Provide a reusable name for a complex query or a limited set of data that you can then [authorize](/bigquery/docs/authorized-views) other users to access. After you create a view, a user can then [query](/bigquery/docs/running-queries) the view as they would a table.
  - Abstract and store calculation and join logic in a common object to simplify query use.
  - Provide access to a subset of data and calculation logic without providing access to the base tables.
  - Optimize queries with high computation cost and small dataset results for [several use cases](/bigquery/docs/materialized-views-intro#use_cases) .

You can also use views in other contexts:

  - As a data source for a visualization tool such as [Looker Studio](/looker/docs) .
  - As a means of sharing data to subscribers of [BigQuery sharing (formerly Analytics Hub)](/bigquery/docs/analytics-hub-introduction) .

For a comparison of logical, materialized views, and authorized views, see [Overview of logical and materialized views](/bigquery/docs/logical-materialized-view-overview) .

## Logical views limitations

BigQuery views are subject to the following limitations:

  - Views are read-only. For example, you can't run queries that insert, update, or delete data.
  - The dataset that contains your view and the dataset that contains the tables referenced by the view must be in the same [location](/bigquery/docs/locations) .
  - A reference inside of a view must be qualified with a dataset. The default dataset doesn't affect a view body.
  - You cannot use the `  TableDataList  ` JSON API method to retrieve data from a view. For more information, see [Tabledata: list](/bigquery/docs/reference/rest/v2/tabledata/list) .
  - You cannot mix GoogleSQL and legacy SQL queries when using views. A GoogleSQL query cannot reference a view defined using legacy SQL syntax.
  - You cannot reference [query parameters](/bigquery/docs/parameterized-queries) in views.
  - The schemas of the underlying tables are stored with the view when the view is created. If columns are added, deleted, or modified after the view is created, the view isn't automatically updated and the reported schema will remain inaccurate until the view SQL definition is changed or the view is recreated. Even though the reported schema may be inaccurate, all submitted queries produce accurate results.
  - You cannot automatically update a legacy SQL view to GoogleSQL syntax. To modify the query used to define a view, you can use the following:
      - The [**Edit query**](/bigquery/docs/updating-views#update-sql) option in the Google Cloud console
      - The [`  bq update --view  `](/bigquery/docs/reference/bq-cli-reference#bq_update) command in the bq command-line tool
      - The [BigQuery Client libraries](/bigquery/docs/reference/libraries)
      - The [update](/bigquery/docs/reference/rest/v2/tables/update) or [patch](/bigquery/docs/reference/rest/v2/tables/patch) API methods.
  - You cannot include a temporary user-defined function or a temporary table in the SQL query that defines a view.
  - You cannot reference a view in a [wildcard table](/bigquery/docs/querying-wildcard-tables) query.

## Logical views quotas

For information on quotas and limits that apply to views, see [View limits](/bigquery/quotas#view_limits) . SQL queries used to define views are also subject to the quotas on [query jobs](/bigquery/quotas#query_jobs) .

## Logical views pricing

BigQuery uses logical views by default, not [materialized views](/bigquery/docs/materialized-views-intro) . Because views are not materialized by default, the query that defines the view is run each time the view is queried. Queries are billed according to the total amount of data in all table fields referenced directly or indirectly by the top-level query.

  - For general query pricing, see [On-demand compute pricing](https://cloud.google.com/bigquery/pricing#on_demand_pricing) .
  - For pricing associated with materialized views, see [Materialized views pricing](/bigquery/docs/materialized-views-intro#materialized_views_pricing) .

## Logical views security

To control access to views in BigQuery, see [Authorized views](/bigquery/docs/authorized-views) .

## What's next

  - For information on creating views, see [Creating views](/bigquery/docs/views) .
  - For information on creating an authorized view, see [Creating authorized views](/bigquery/docs/authorized-views) .
  - For information on getting view metadata, see [Getting information about views](/bigquery/docs/view-metadata) .
  - For more information on managing views, see [Managing views](/bigquery/docs/managing-views) .
