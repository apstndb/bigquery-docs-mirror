---
name: documents/docs.cloud.google.com/bigquery/docs/postgresql-federated-queries
uri: https://docs.cloud.google.com/bigquery/docs/postgresql-federated-queries
title: Run PostgreSQL federated queries
description: Shows how to connect to and query data in PostgreSQL from BigQuery using federated queries.
data_source: docs.cloud.google.com
---

# Run PostgreSQL federated queries

> **Preview**
>
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

> **Note:** To get support or provide feedback for this preview feature, contact <bq-3p-federation-support@google.com> .

As a data analyst, you can query relational data residing in PostgreSQL directly from BigQuery in real time, without copying or moving data.

BigQuery PostgreSQL federation uses the BigQuery Connection API to connect to PostgreSQL database engines. You can then use the [`EXTERNAL_QUERY` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/federated_query_functions#external_query) to send your SQL query directly to PostgreSQL for execution, and the results are streamed directly back.

## Limitations

PostgreSQL federated queries are subject to the following limitations:

- You can only execute read-only queries through the `EXTERNAL_QUERY` function. Data definition language (DDL) and data manipulation language (DML) statements aren't supported.

- Federation is only accessible through the `EXTERNAL_QUERY` function. Creating BigQuery external tables or permanent datasets that directly map to PostgreSQL tables isn't supported.

- Federated query latency might be noticeably higher than executing the query directly in PostgreSQL.

- The underlying connection service might hibernate inactive connections. The first query that uses a PostgreSQL connection after a period of inactivity might take more than a minute to run while the connector initializes.

- DNS peering isn't supported. You must connect using an IP address or a fully resolvable hostname within your VPC network.

- The PostgreSQL SQL query must specify explicit column aliases for any columns that contain function results or expressions (for example, `SELECT COUNT(*) AS total_count` ). Unaliased expressions produce column names with special characters that are invalid in BigQuery table schema definitions.

- When the usage of the Compute Engine API in the query project is restricted by [VPC Service Controls](https://docs.cloud.google.com/vpc-service-controls/docs/overview) , the federated query fails if the connection uses a network attachment. Ensure that appropriate VPC Service Controls ingress and egress rules are configured.

- No additional [SQL pushdowns](https://docs.cloud.google.com/bigquery/docs/federated-queries-intro#sql_pushdowns) are supported for PostgreSQL. Filters and aggregations in the outer BigQuery query aren't pushed down into the inner query within the `EXTERNAL_QUERY` function. You must specify predicates and column projections directly inside the inner PostgreSQL SQL statement to limit the rows and columns that are transferred across the network.

- Only PostgreSQL database username and password authentication is supported. Third-party identity providers, Kerberos, and cloud provider IAM authentication aren't supported.

- `CREATE TABLE ... AS SELECT` (CTAS) statements fail with `Unsupported type INT32` or `Unsupported type FLOAT` errors if the query selects 16-bit integer columns ( `int2` , `smallint` , `smallserial` ) or single-precision float columns ( `float4` , `real` ). To save query results into a new BigQuery table, explicitly cast integer columns to `INT64` and float columns to `FLOAT64` in your query:

  ```
  CREATE TABLE mydataset.mytable AS
  SELECT
  CAST(small_col AS INT64) AS small_col,
  CAST(real_col AS FLOAT64) AS real_col,
  ...
  FROM EXTERNAL_QUERY(...);
  ```

  Inserting into an existing table with `INSERT INTO <table> SELECT ...` succeeds without manual casts because BigQuery automatically widens `INT32` and `FLOAT` values to match the target table's `INT64` and `FLOAT64` columns.

- Both `time [ without time zone ]` and `time with time zone` ( `timetz` ) truncate fractional sub-second (microsecond) values to whole seconds. If microsecond precision is required, format or cast the column to `text` or `varchar` in the `EXTERNAL_QUERY` statement.

- All PostgreSQL `numeric` and `decimal` columns map to `BIGNUMERIC(76, 38)` . Columns with scale greater than 38 are rounded to 38 decimal places, and values that exceed the `BIGNUMERIC` range (more than 38 full integer digits) fail with an out-of-range error. In addition, special values `NaN` , `Infinity` , and `-Infinity` aren't supported and fail at runtime. To query numbers with larger integer parts, higher fractional precision, or special values, cast the column to `text` in the `EXTERNAL_QUERY` statement.

- Fixed-length `character(n)` / `char(n)` ( `bpchar` ) values preserve trailing spaces up to length *n* when mapped to BigQuery `STRING` .

- Dates and timestamps prior to October 15, 1582 are subject to a 10-day calendar shift due to the historical Gregorian calendar transition. Cast historical dates to `text` in the `EXTERNAL_QUERY` statement to preserve exact dates.

## Supported PostgreSQL environments and versions

Query federation supports PostgreSQL databases across the following deployment environments:

- Cloud-hosted or on-premises PostgreSQL databases accessible through public IP addresses or network attachments (over Cloud VPN or Cloud Interconnect)
- Self-hosted PostgreSQL instances on Compute Engine or other infrastructure
- PostgreSQL 16 (Recommended) and PostgreSQL 15

> **Note:** To run federated queries against Cloud SQL for PostgreSQL or AlloyDB for PostgreSQL, use the dedicated [Cloud SQL federated queries](https://docs.cloud.google.com/bigquery/docs/cloud-sql-federated-queries) or [AlloyDB federated queries](https://docs.cloud.google.com/bigquery/docs/alloydb-federated-queries) connectors, which support SQL pushdowns.

## Before you begin

Ensure that your BigQuery administrator has [created a PostgreSQL connection](https://docs.cloud.google.com/bigquery/docs/connect-to-postgresql) and [shared](https://docs.cloud.google.com/bigquery/docs/working-with-connections#share-connections) it with you.

### Required roles

To get the permissions that you need to query PostgreSQL, ask your administrator to grant you the [BigQuery Connection User](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.connectionUser) ( `roles/bigquery.connectionUser` ) IAM role on the project. For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## Query data

To send a federated query to PostgreSQL from a GoogleSQL query, use the [`EXTERNAL_QUERY` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/federated_query_functions#external_query) .

The following example is a federated query that joins customer records in BigQuery named `mydataset.customers` with transactional sales orders in PostgreSQL:

```
SELECT
  c.customer_id,
  c.name,
  fo.first_order_date
FROM
  mydataset.customers AS c
LEFT OUTER JOIN EXTERNAL_QUERY(
  'projects/my-project/locations/us-central1/connections/postgres_prod_conn',
  '''SELECT customer_id, MIN(order_date) AS first_order_date
     FROM orders
     GROUP BY customer_id''') AS fo
  ON fo.customer_id = c.customer_id
GROUP BY
  c.customer_id,
  c.name,
  fo.first_order_date;
```

## View a PostgreSQL table schema

You can query the PostgreSQL `information_schema` tables using `EXTERNAL_QUERY` to retrieve database metadata:

### List all tables in a schema

```
SELECT *
FROM EXTERNAL_QUERY(
  'projects/PROJECT_ID/locations/LOCATION/connections/CONNECTION_ID',
  '''SELECT table_schema, table_name, table_type
     FROM information_schema.tables
     WHERE table_schema = 'SCHEMA_NAME'
     ORDER BY table_name''');
```

### View columns and data types in a table

```
SELECT *
FROM EXTERNAL_QUERY(
  'projects/PROJECT_ID/locations/LOCATION/connections/CONNECTION_ID',
  '''SELECT column_name, data_type, is_nullable
     FROM information_schema.columns
     WHERE table_schema = 'SCHEMA_NAME' AND table_name = 'TABLE_NAME'
     ORDER BY ordinal_position''');
```

## Data type mapping

When you execute a federated query, BigQuery converts the data from PostgreSQL into GoogleSQL data types according to the following table:

| PostgreSQL data type                       | BigQuery data type                                                                                                                                                         |
|--------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Boolean types**                          |                                                                                                                                                                            |
| `bool` , `boolean`                         | `BOOL`                                                                                                                                                                     |
| **Numeric types**                          |                                                                                                                                                                            |
| `int2` , `smallint` , `smallserial`        | `INT64` (interactive queries; see [Limitations](https://docs.cloud.google.com/bigquery/docs/postgresql-federated-queries#limitations) for `CREATE TABLE ... AS SELECT` )   |
| `int4` , `integer` , `serial`              | `INT64`                                                                                                                                                                    |
| `int8` , `bigint` , `bigserial`            | `INT64`                                                                                                                                                                    |
| `numeric` , `decimal`                      | `BIGNUMERIC(76, 38)`                                                                                                                                                       |
| `float4` , `real`                          | `FLOAT64` (interactive queries; see [Limitations](https://docs.cloud.google.com/bigquery/docs/postgresql-federated-queries#limitations) for `CREATE TABLE ... AS SELECT` ) |
| `float8` , `double precision`              | `FLOAT64`                                                                                                                                                                  |
| **Date and time types**                    |                                                                                                                                                                            |
| `date`                                     | `DATE`                                                                                                                                                                     |
| `timestamp [ without time zone ]`          | `DATETIME`                                                                                                                                                                 |
| `timestamp with time zone` , `timestamptz` | `TIMESTAMP`                                                                                                                                                                |
| `time [ without time zone ]`               | `TIME`                                                                                                                                                                     |
| `time with time zone` , `timetz`           | `TIME`                                                                                                                                                                     |
| **Character and text types**               |                                                                                                                                                                            |
| `character(n)` , `char(n)` , `bpchar`      | `STRING`                                                                                                                                                                   |
| `character varying(n)` , `varchar(n)`      | `STRING`                                                                                                                                                                   |
| `text`                                     | `STRING`                                                                                                                                                                   |

## Pricing

The cost of running a federated query is based on three factors:

- The compute cost of executing the query in PostgreSQL (charged by your PostgreSQL database provider or hosting environment)
- The bandwidth cost of transferring the query results from PostgreSQL to BigQuery (egress network charges from your database hosting provider)
- The compute cost of executing the query in BigQuery

Any PostgreSQL compute and egress costs are billed directly by your PostgreSQL provider or infrastructure host, not Google. To limit bandwidth cost, we recommend that you write the query in the `EXTERNAL_QUERY` statement so that it excludes all columns and rows that aren't needed to compute the final result.

There is no additional cost for running federated queries in BigQuery. For more information about BigQuery pricing, see [Pricing](https://cloud.google.com/bigquery/pricing) .

If your connection uses Google Cloud networking components, the following pricing might also apply:

- [Virtual Private Cloud pricing](https://docs.cloud.google.com/vpc/pricing)
- [Cloud VPN pricing](https://docs.cloud.google.com/network-connectivity/docs/vpn/pricing)
- [Cloud NAT pricing](https://docs.cloud.google.com/nat/pricing)
- [Cloud Interconnect pricing](https://docs.cloud.google.com/network-connectivity/docs/interconnect/pricing)

## What's next

- Learn how to [connect to PostgreSQL](https://docs.cloud.google.com/bigquery/docs/connect-to-postgresql) .
- Learn more about [federated queries](https://docs.cloud.google.com/bigquery/docs/federated-queries-intro) .
- Learn about [managing connections](https://docs.cloud.google.com/bigquery/docs/working-with-connections) .
- Learn about [AlloyDB federated queries](https://docs.cloud.google.com/bigquery/docs/alloydb-federated-queries) .
- Learn about [Cloud SQL federated queries](https://docs.cloud.google.com/bigquery/docs/cloud-sql-federated-queries) .
