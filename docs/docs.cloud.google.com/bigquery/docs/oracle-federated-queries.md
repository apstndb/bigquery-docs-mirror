---
name: documents/docs.cloud.google.com/bigquery/docs/oracle-federated-queries
uri: https://docs.cloud.google.com/bigquery/docs/oracle-federated-queries
title: Run Oracle federated queries
description: Shows how to connect to and query data in Oracle from BigQuery using federated queries.
data_source: docs.cloud.google.com
---

# Run Oracle federated queries

> **Preview**
>
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

> **Note:** To get support or provide feedback for this preview feature, contact <bq-3p-federation-support@google.com> .

As a data analyst, you can query relational data residing in Oracle directly from BigQuery in real time, without copying or moving data.

BigQuery Oracle federation uses the BigQuery Connection API to connect to Oracle database engines. You can then use the [`EXTERNAL_QUERY` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/federated_query_functions#external_query) to send your SQL query directly to Oracle for execution, and the results are streamed directly back.

## Limitations

Oracle federated queries are subject to the following limitations:

- You can only execute read-only queries through the `EXTERNAL_QUERY` function. Data definition language (DDL) and data manipulation language (DML) statements aren't supported.

- Federation is only accessible through the `EXTERNAL_QUERY` function. Creating BigQuery external tables or permanent datasets that directly map to Oracle tables isn't supported.

- Federated query latency might be noticeably higher than executing the query directly in Oracle.

- The underlying connection service might hibernate inactive connections. The first query that uses a Oracle connection after a period of inactivity might take more than a minute to run while the connector initializes.

- DNS peering isn't supported. You must connect using an IP address or a fully resolvable hostname within your VPC network.

- The Oracle SQL query must specify explicit column aliases for any columns that contain function results or expressions (for example, `SELECT COUNT(*) AS total_count` ). Unaliased expressions produce column names with special characters that are invalid in BigQuery table schema definitions.

- When the usage of the Compute Engine API in the query project is restricted by [VPC Service Controls](https://docs.cloud.google.com/vpc-service-controls/docs/overview) , the federated query fails if the connection uses a network attachment. Ensure that appropriate VPC Service Controls ingress and egress rules are configured.

- No additional [SQL pushdowns](https://docs.cloud.google.com/bigquery/docs/federated-queries-intro#sql_pushdowns) are supported for Oracle. Filters and aggregations in the outer BigQuery query aren't pushed down into the inner query within the `EXTERNAL_QUERY` function. You must specify predicates and column projections directly inside the inner Oracle SQL statement to limit the rows and columns that are transferred across the network.

- Only Oracle database username and password authentication is supported. Third-party identity providers, Kerberos, RADIUS, and Oracle Cloud Infrastructure (OCI) IAM authentication aren't supported.

- Complex or proprietary Oracle types such as user-defined types (UDTs), spatial types ( `SDO_GEOMETRY` ), collection types ( `VARRAY` , nested tables), `SYS.ANYDATA` , `REF` , `BFILE` , and binary `JSON` (OSON) columns aren't supported. To query a binary `JSON` column, serialize it to text in your query (for example, with `JSON_SERIALIZE(column_name)` or `JSON_QUERY` ).

- Unconstrained `NUMBER` columns and calculated numeric expressions map to BigQuery `STRING` to preserve full precision without truncation or overflow. Constrained `NUMBER(p, s)` columns map to `NUMERIC` (when precision is less than or equal to 38 and scale is less than or equal to 9) or `BIGNUMERIC` (when scale is greater than 9 or integer digits are greater than 29).

- Fixed-length `CHAR(n)` and `NCHAR(n)` columns preserve trailing whitespace padding up to length *n* when mapped to BigQuery `STRING` .

- Dates and timestamps prior to October 15, 1582 might experience a 10-day calendar shift due to the historical Gregorian calendar transition. To preserve exact historical dates prior to 1582, cast them to `VARCHAR2` in the `EXTERNAL_QUERY` statement.

## Supported Oracle environments and versions

Query federation supports Oracle databases across the following deployment environments:

- Oracle Database@Google Cloud
- Oracle Exadata Database Service
- On-premises Oracle instances connected to Google Cloud through Cloud VPN, Cloud Interconnect, or public IP over the internet

Query federation supports the following Oracle versions:

- Oracle Database 23.x (23ai)
- Oracle Database 21.x
- Oracle Database 19.x (19c)

## Before you begin

Ensure that your BigQuery administrator has [created an Oracle connection](https://docs.cloud.google.com/bigquery/docs/connect-to-oracle) and [shared](https://docs.cloud.google.com/bigquery/docs/working-with-connections#share-connections) it with you.

### Required roles

To get the permissions that you need to query Oracle, ask your administrator to grant you the [BigQuery Connection User](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.connectionUser) ( `roles/bigquery.connectionUser` ) IAM role on the project. For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## Query data

To send a federated query to Oracle from a GoogleSQL query, use the [`EXTERNAL_QUERY` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/federated_query_functions#external_query) .

The following example is a federated query that joins customer records in BigQuery named `mydataset.customers` with live order records from an Oracle database:

```
SELECT
  bq_cust.customer_id,
  bq_cust.customer_name,
  oracle_orders.order_id,
  oracle_orders.order_status,
  oracle_orders.order_total
FROM
  mydataset.customers AS bq_cust
JOIN
  EXTERNAL_QUERY(
    'projects/my-project/locations/us-central1/connections/oracle_prod_conn',
    '''SELECT customer_id, order_id, order_status, order_total
       FROM orders
       WHERE order_date >= SYSDATE - 1''') AS oracle_orders
  ON bq_cust.customer_id = oracle_orders.customer_id;
```

## View an Oracle table schema

You can query the Oracle data dictionary views through `EXTERNAL_QUERY` to inspect database metadata, discover tables, and review column schemas before running analytics.

### List all accessible tables

```
SELECT *
FROM EXTERNAL_QUERY(
  'projects/PROJECT_ID/locations/LOCATION/connections/CONNECTION_ID',
  '''SELECT owner, table_name, tablespace_name, status
     FROM all_tables
     ORDER BY owner, table_name''');
```

### View columns and data types in a table

```
SELECT *
FROM EXTERNAL_QUERY(
  'projects/PROJECT_ID/locations/LOCATION/connections/CONNECTION_ID',
  '''SELECT column_name, data_type, data_length, data_precision, data_scale, nullable
     FROM all_tab_columns
     WHERE owner = 'SCHEMA_NAME' AND table_name = 'TABLE_NAME'
     ORDER BY column_id''');
```

## Data type mapping

When you execute a federated query, BigQuery converts the data from Oracle into GoogleSQL data types according to the following table:

| Oracle data type                                | BigQuery data type |
|-------------------------------------------------|--------------------|
| **Numeric types**                               |                    |
| `NUMBER(p, s)` (p ≤ 38, s ≤ 9)                  | `NUMERIC`          |
| `NUMBER(p, s)` (s \> 9 or p \> 38)              | `BIGNUMERIC`       |
| `NUMBER` (unconstrained or floating scale)      | `STRING`           |
| `FLOAT` , `FLOAT(p)`                            | `FLOAT64`          |
| `BINARY_FLOAT`                                  | `FLOAT64`          |
| `BINARY_DOUBLE`                                 | `FLOAT64`          |
| **Character and string types**                  |                    |
| `CHAR(n)`                                       | `STRING`           |
| `NCHAR(n)`                                      | `STRING`           |
| `VARCHAR2(n)`                                   | `STRING`           |
| `NVARCHAR2(n)`                                  | `STRING`           |
| `CLOB`                                          | `STRING`           |
| `NCLOB`                                         | `STRING`           |
| `LONG`                                          | `STRING`           |
| **Binary types**                                |                    |
| `RAW(n)`                                        | `BYTES`            |
| `BLOB`                                          | `BYTES`            |
| `LONG RAW`                                      | `BYTES`            |
| **Date, time, and interval types**              |                    |
| `DATE`                                          | `DATETIME`         |
| `TIMESTAMP` , `TIMESTAMP(p)`                    | `DATETIME`         |
| `TIMESTAMP WITH TIME ZONE`                      | `TIMESTAMP`        |
| `TIMESTAMP WITH LOCAL TIME ZONE`                | `TIMESTAMP`        |
| `INTERVAL YEAR TO MONTH`                        | `STRING`           |
| `INTERVAL DAY TO SECOND`                        | `STRING`           |
| **Row identification types**                    |                    |
| `ROWID`                                         | `STRING`           |
| `UROWID`                                        | `STRING`           |
| **Semistructured, vector, and XML types**       |                    |
| `JSON` (textual / OSON with text serialization) | `STRING`           |
| `VECTOR`                                        | `STRING`           |
| `XMLTYPE`                                       | `STRING`           |

## Pricing

The cost of running a federated query is based on three factors:

- The compute cost of executing the query in Oracle (charged by your Oracle database provider or hosting environment)
- The bandwidth cost of transferring the query results from Oracle to BigQuery (egress network charges from your database hosting provider)
- The compute cost of executing the query in BigQuery

Any Oracle-related costs depend on the type of Oracle service and hosting environment that you use. To limit bandwidth cost, we recommend that you write the query in the `EXTERNAL_QUERY` statement so that it excludes all columns and rows that aren't needed to compute the final result.

There is no additional cost for running federated queries in BigQuery. For more information about BigQuery pricing, see [Pricing](https://cloud.google.com/bigquery/pricing) .

If your connection uses Google Cloud networking components, the following pricing might also apply:

- [Virtual Private Cloud pricing](https://docs.cloud.google.com/vpc/pricing)
- [Cloud VPN pricing](https://docs.cloud.google.com/network-connectivity/docs/vpn/pricing)
- [Cloud NAT pricing](https://docs.cloud.google.com/nat/pricing)
- [Cloud Interconnect pricing](https://docs.cloud.google.com/network-connectivity/docs/interconnect/pricing)

## What's next

- Learn how to [connect to Oracle](https://docs.cloud.google.com/bigquery/docs/connect-to-oracle) .
- Learn more about [federated queries](https://docs.cloud.google.com/bigquery/docs/federated-queries-intro) .
- Learn about [managing connections](https://docs.cloud.google.com/bigquery/docs/working-with-connections) .
