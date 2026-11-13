---
name: documents/docs.cloud.google.com/bigquery/docs/mysql-federated-queries
uri: https://docs.cloud.google.com/bigquery/docs/mysql-federated-queries
title: Run MySQL federated queries
description: Shows how to connect to and query data in MySQL from BigQuery using federated queries.
data_source: docs.cloud.google.com
---

# Run MySQL federated queries

> **Preview**
>
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

> **Note:** To get support or provide feedback for this preview feature, contact <bq-3p-federation-support@google.com> .

As a data analyst, you can query relational data residing in MySQL directly from BigQuery in real time, without copying or moving data.

BigQuery MySQL federation uses the BigQuery Connection API to connect to MySQL database engines. You can then use the [`EXTERNAL_QUERY` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/federated_query_functions#external_query) to send your SQL query directly to MySQL for execution, and the results are streamed directly back.

## Limitations

MySQL federated queries are subject to the following limitations:

- You can only execute read-only queries through the `EXTERNAL_QUERY` function. Data definition language (DDL) and data manipulation language (DML) statements aren't supported.

- Federation is only accessible through the `EXTERNAL_QUERY` function. Creating BigQuery external tables or permanent datasets that directly map to MySQL tables isn't supported.

- Federated query latency might be noticeably higher than executing the query directly in MySQL.

- The underlying connection service might hibernate inactive connections. The first query that uses a MySQL connection after a period of inactivity might take more than a minute to run while the connector initializes.

- DNS peering isn't supported. You must connect using an IP address or a fully resolvable hostname within your VPC network.

- The MySQL SQL query must specify explicit column aliases for any columns that contain function results or expressions (for example, `SELECT COUNT(*) AS total_count` ). Unaliased expressions produce column names with special characters that are invalid in BigQuery table schema definitions.

- When the usage of the Compute Engine API in the query project is restricted by [VPC Service Controls](https://docs.cloud.google.com/vpc-service-controls/docs/overview) , the federated query fails if the connection uses a network attachment. Ensure that appropriate VPC Service Controls ingress and egress rules are configured.

- No additional [SQL pushdowns](https://docs.cloud.google.com/bigquery/docs/federated-queries-intro#sql_pushdowns) are supported for MySQL. Filters and aggregations in the outer BigQuery query aren't pushed down into the inner query within the `EXTERNAL_QUERY` function. You must specify predicates and column projections directly inside the inner MySQL SQL statement to limit the rows and columns that are transferred across the network.

- Only MySQL database username and password authentication is supported. Third-party identity providers, Kerberos, and cloud provider IAM authentication aren't supported.

- `CREATE TABLE ... AS SELECT` (CTAS) statements fail with `Unsupported type INT32` or `Unsupported type FLOAT` errors if the query selects 32-bit integer columns ( `TINYINT` , `SMALLINT` , and `BOOLEAN` / `TINYINT(1)` ) or single-precision float columns ( `FLOAT` ). To save query results into a new BigQuery table, explicitly cast integer columns to `INT64` and float columns to `FLOAT64` in your query:

  ```
  CREATE TABLE mydataset.mytable AS
  SELECT
  CAST(tiny_col AS INT64) AS tiny_col,
  CAST(small_col AS INT64) AS small_col,
  ...
  FROM EXTERNAL_QUERY(...);
  ```

  Inserting into an existing table with `INSERT INTO <table> SELECT ...` succeeds without manual casts because BigQuery automatically widens `INT32` and `FLOAT` values to match the target table's `INT64` and `FLOAT64` columns.

- While MySQL `DECIMAL` and `NUMERIC` columns map to `BIGNUMERIC(76, 38)` , MySQL allows precision up to 65. If a value contains more than 38 integer digits (precision minus scale is greater than 38), it exceeds the `BIGNUMERIC` integer range and the query fails at runtime. To query values with more than 38 integer digits, cast them to `CHAR` or `VARCHAR` in the `EXTERNAL_QUERY` statement.

- The `TIME` data type truncates fractional sub-second (microsecond) values to whole seconds (for example, `12:34:56.789123` becomes `12:34:56` ). Furthermore, MySQL `TIME` supports elapsed durations from `-838:59:59` to `838:59:59` , whereas BigQuery `TIME` only supports time-of-day values from `00:00:00` to `23:59:59.999999` . Values outside `00:00:00` to `23:59:59` cause runtime query errors. If microsecond precision or elapsed duration values are required, cast the column to `CHAR` or `VARCHAR` inside the `EXTERNAL_QUERY` statement.

- Dates and timestamps prior to October 15, 1582 are subject to a 10-day calendar shift due to the historical Gregorian calendar transition. To preserve exact historical dates prior to 1582, cast them to `CHAR` or `VARCHAR` in the `EXTERNAL_QUERY` statement.

## Supported MySQL environments and versions

Query federation supports MySQL databases across the following deployment environments:

- Cloud-hosted or on-premises MySQL databases accessible through public IP addresses or network attachments (over Cloud VPN or Cloud Interconnect)
- Self-hosted MySQL instances on Compute Engine or other infrastructure
- MySQL 8.4 LTS and 8.0

> **Note:** To run federated queries against Cloud SQL for MySQL, use the dedicated [Cloud SQL federated queries](https://docs.cloud.google.com/bigquery/docs/cloud-sql-federated-queries) connector, which supports SQL pushdowns.

## Before you begin

Ensure that your BigQuery administrator has [created a MySQL connection](https://docs.cloud.google.com/bigquery/docs/connect-to-mysql) and [shared](https://docs.cloud.google.com/bigquery/docs/working-with-connections#share-connections) it with you.

### Required roles

To get the permissions that you need to query MySQL, ask your administrator to grant you the [BigQuery Connection User](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.connectionUser) ( `roles/bigquery.connectionUser` ) IAM role on the project. For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## Query data

To send a federated query to MySQL from a GoogleSQL query, use the [`EXTERNAL_QUERY` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/federated_query_functions#external_query) .

The following example is a federated query that joins customer records in BigQuery named `mydataset.customers` with transactional sales orders in MySQL:

```
SELECT
  c.customer_id,
  c.name,
  fo.first_order_date
FROM
  mydataset.customers AS c
LEFT OUTER JOIN EXTERNAL_QUERY(
  'projects/my-project/locations/us-central1/connections/mysql_prod_conn',
  '''SELECT CUSTOMER_ID, MIN(ORDER_DATE) AS first_order_date
     FROM ORDERS
     GROUP BY CUSTOMER_ID''') AS fo
  ON fo.customer_id = c.customer_id
GROUP BY
  c.customer_id,
  c.name,
  fo.first_order_date;
```

## View a MySQL table schema

You can query the MySQL `INFORMATION_SCHEMA` views through `EXTERNAL_QUERY` to inspect database metadata, discover tables, and review column schemas before running analytics.

### List all databases

```
SELECT *
FROM EXTERNAL_QUERY(
  'projects/PROJECT_ID/locations/LOCATION/connections/CONNECTION_ID',
  '''SELECT SCHEMA_NAME, DEFAULT_CHARACTER_SET_NAME
     FROM INFORMATION_SCHEMA.SCHEMATA''');
```

### List tables in a database

```
SELECT *
FROM EXTERNAL_QUERY(
  'projects/PROJECT_ID/locations/LOCATION/connections/CONNECTION_ID',
  """SELECT TABLE_SCHEMA, TABLE_NAME, TABLE_TYPE, ENGINE
     FROM INFORMATION_SCHEMA.TABLES
     WHERE TABLE_SCHEMA = 'DATABASE_NAME'""");
```

### View columns and data types in a table

```
SELECT *
FROM EXTERNAL_QUERY(
  'projects/PROJECT_ID/locations/LOCATION/connections/CONNECTION_ID',
  """SELECT COLUMN_NAME, DATA_TYPE, IS_NULLABLE, COLUMN_TYPE
     FROM INFORMATION_SCHEMA.COLUMNS
     WHERE TABLE_SCHEMA = 'DATABASE_NAME' AND TABLE_NAME = 'TABLE_NAME'""");
```

## Data type mapping

When you execute a federated query, BigQuery converts the data from MySQL into GoogleSQL data types according to the following table:

| MySQL data type                                  | BigQuery data type                                                                                                                                                    |
|--------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Numeric types**                                |                                                                                                                                                                       |
| `BOOLEAN` , `BOOL` , `TINYINT(1)`                | `INT64` (interactive queries; see [Limitations](https://docs.cloud.google.com/bigquery/docs/mysql-federated-queries#limitations) for `CREATE TABLE ... AS SELECT` )   |
| `TINYINT` , `SMALLINT`                           | `INT64` (interactive queries; see [Limitations](https://docs.cloud.google.com/bigquery/docs/mysql-federated-queries#limitations) for `CREATE TABLE ... AS SELECT` )   |
| `MEDIUMINT` , `INT` , `INTEGER`                  | `INT64`                                                                                                                                                               |
| `BIGINT`                                         | `INT64`                                                                                                                                                               |
| `BIGINT UNSIGNED` , `BIGINT ZEROFILL` , `SERIAL` | `BIGNUMERIC(76, 38)`                                                                                                                                                  |
| `DECIMAL` , `DEC` , `NUMERIC` , `FIXED`          | `BIGNUMERIC(76, 38)`                                                                                                                                                  |
| `FLOAT`                                          | `FLOAT64` (interactive queries; see [Limitations](https://docs.cloud.google.com/bigquery/docs/mysql-federated-queries#limitations) for `CREATE TABLE ... AS SELECT` ) |
| `DOUBLE` , `DOUBLE PRECISION` , `REAL`           | `FLOAT64`                                                                                                                                                             |
| **Date and time types**                          |                                                                                                                                                                       |
| `DATE`                                           | `DATE`                                                                                                                                                                |
| `DATETIME`                                       | `DATETIME`                                                                                                                                                            |
| `TIMESTAMP`                                      | `TIMESTAMP`                                                                                                                                                           |
| `TIME`                                           | `TIME`                                                                                                                                                                |
| **String and text types**                        |                                                                                                                                                                       |
| `CHAR`                                           | `STRING`                                                                                                                                                              |
| `VARCHAR`                                        | `STRING`                                                                                                                                                              |
| `BINARY`                                         | `BYTES`                                                                                                                                                               |
| `VARBINARY`                                      | `BYTES`                                                                                                                                                               |
| `TINYBLOB` , `BLOB` , `MEDIUMBLOB` , `LONGBLOB`  | `BYTES`                                                                                                                                                               |
| `TINYTEXT` , `TEXT` , `MEDIUMTEXT` , `LONGTEXT`  | `STRING`                                                                                                                                                              |
| `ENUM`                                           | `STRING`                                                                                                                                                              |
| `SET`                                            | `STRING`                                                                                                                                                              |

## Pricing

The cost of running a federated query is based on three factors:

- The compute cost of executing the query in MySQL (charged by your MySQL database provider or hosting environment)
- The bandwidth cost of transferring the query results from MySQL to BigQuery (egress network charges from your database hosting provider)
- The compute cost of executing the query in BigQuery

Any MySQL compute and egress costs are billed directly by your MySQL provider or infrastructure host, not Google. To limit bandwidth cost, we recommend that you write the query in the `EXTERNAL_QUERY` statement so that it excludes all columns and rows that aren't needed to compute the final result.

There is no additional cost for running federated queries in BigQuery. For more information about BigQuery pricing, see [Pricing](https://cloud.google.com/bigquery/pricing) .

If your connection uses Google Cloud networking components, the following pricing might also apply:

- [Virtual Private Cloud pricing](https://docs.cloud.google.com/vpc/pricing)
- [Cloud VPN pricing](https://docs.cloud.google.com/network-connectivity/docs/vpn/pricing)
- [Cloud NAT pricing](https://docs.cloud.google.com/nat/pricing)
- [Cloud Interconnect pricing](https://docs.cloud.google.com/network-connectivity/docs/interconnect/pricing)

## What's next

- Learn how to [connect to MySQL](https://docs.cloud.google.com/bigquery/docs/connect-to-mysql) .
- Learn more about [federated queries](https://docs.cloud.google.com/bigquery/docs/federated-queries-intro) .
- Learn about [managing connections](https://docs.cloud.google.com/bigquery/docs/working-with-connections) .
