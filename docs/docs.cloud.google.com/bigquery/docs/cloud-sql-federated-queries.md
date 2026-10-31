---
name: documents/docs.cloud.google.com/bigquery/docs/cloud-sql-federated-queries
uri: https://docs.cloud.google.com/bigquery/docs/cloud-sql-federated-queries
title: Cloud SQL federated queries
description: Shows how to query data in Cloud SQL from BigQuery using federated queries.
data_source: docs.cloud.google.com
---

# Cloud SQL federated queries

[Federated queries](https://docs.cloud.google.com/bigquery/docs/federated-queries-intro) in BigQuery let you query data residing in Cloud SQL in real time without copying or moving data. Query federation supports both Cloud SQL for MySQL and Cloud SQL for PostgreSQL instances in Cloud SQL.

Alternatively, to replicate data into BigQuery, you can use Cloud Data Fusion or [Datastream](https://docs.cloud.google.com/datastream/docs/overview) . For more information about using Cloud Data Fusion, see [Replicating data from MySQL to BigQuery](https://docs.cloud.google.com/data-fusion/docs/tutorials/replicating-data/mysql-to-bigquery) .

## Before you begin

To run federated queries on your data in Cloud SQL, do the following:

1.  Ensure that your BigQuery administrator has [created a Cloud SQL connection](https://docs.cloud.google.com/bigquery/docs/connect-to-sql#create-sql-connection) and [shared the connection](https://docs.cloud.google.com/bigquery/docs/connect-to-sql#share_connections) with you.
2.  Verify that the BigQuery Connection service agent has been granted the Cloud SQL Client ( `roles/cloudsql.client` ) role. For more information, see [Grant access to the service agent](https://docs.cloud.google.com/bigquery/docs/connect-to-sql#access-sql) .
3.  If your Cloud SQL instance uses a private IP address, ensure that a private path was enabled when the instance was created. For more information, see [Connect to Cloud SQL](https://docs.cloud.google.com/bigquery/docs/connect-to-sql) and [Configure private IP](https://docs.cloud.google.com/sql/docs/mysql/configure-private-ip) .

### Required roles

To get the permissions that you need to query a Cloud SQL instance, ask your administrator to grant you the [BigQuery Connection User](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.connectionUser) ( `roles/bigquery.connectionUser` ) IAM role on your project. For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## Query data

To send a federated query to Cloud SQL from a GoogleSQL query, use the [`EXTERNAL_QUERY` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/federated_query_functions#external_query) .

### Connection identifier format

The first argument to the `EXTERNAL_QUERY` function is the connection identifier. You can specify the connection identifier using one of the following formats:

- **Short format** : `[ `` LOCATION `` .] `` CONNECTION_ID` (for example, `'us.my-connection'` or `'my-connection'` )
- **Fully qualified format** : `projects/ `` PROJECT_ID `` /locations/ `` LOCATION `` /connections/ `` CONNECTION_ID`
- **Friendly path format** : `PROJECT_ID `` . `` LOCATION `` . `` CONNECTION_ID` (for example, `'my-project.us.my-connection'` )

If you execute a query in a shared view across multiple projects, always use the fully qualified connection identifier to avoid connecting to the wrong project.

### Run a federated query

Suppose that you store a customer table in BigQuery, while storing an orders table in Cloud SQL, and want to join the two tables in a single query. The following example makes a federated query to a Cloud SQL table named `orders` and joins the results with a BigQuery table named `mydataset.customers` .

Select one of the following options to run the federated query:

### Console

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter your query:

    ```
    SELECT c.customer_id, c.name, rq.first_order_date
    FROM mydataset.customers AS c
    LEFT OUTER JOIN EXTERNAL_QUERY(
      'us.CONNECTION_ID',
      '''SELECT customer_id, MIN(order_date) AS first_order_date
      FROM orders
      GROUP BY customer_id''') AS rq ON rq.customer_id = c.customer_id
    GROUP BY c.customer_id, c.name, rq.first_order_date;
    ```

    Replace `CONNECTION_ID` with the ID of your BigQuery connection.

3.  Click play_circle **Run** .

    The query results appear in the **Query results** pane.

### bq

1.  

2.  In the Google Cloud console, activate Cloud Shell.

    At the bottom of the Google Cloud console, a [Cloud Shell](https://docs.cloud.google.com/shell/docs/how-cloud-shell-works) session starts and displays a command-line prompt. Cloud Shell is a shell environment with the Google Cloud CLI already installed and with values already set for your current project. It can take a few seconds for the session to initialize.

3.  Run the [`bq query`](https://docs.cloud.google.com/bigquery/docs/reference/bq-cli-reference#bq_query) command with the `--use_legacy_sql=false` flag:

    ```
    bq query \
        --use_legacy_sql=false \
        'SELECT c.customer_id, c.name, rq.first_order_date
        FROM mydataset.customers AS c
        LEFT OUTER JOIN EXTERNAL_QUERY(
          "us.CONNECTION_ID",
          """SELECT customer_id, MIN(order_date) AS first_order_date
          FROM orders
          GROUP BY customer_id""") AS rq ON rq.customer_id = c.customer_id
        GROUP BY c.customer_id, c.name, rq.first_order_date;'
    ```

    Replace `CONNECTION_ID` with the ID of your BigQuery connection.

The example query includes 3 parts:

1.  Run the external query `SELECT customer_id, MIN(order_date) AS first_order_date FROM orders GROUP BY customer_id` in the operational Cloud SQL database to get the first order date for each customer through the `EXTERNAL_QUERY()` function.
2.  Join the external query result table with the customers table in BigQuery by `customer_id` .
3.  Select customer information and first order date.

## View a Cloud SQL table schema

You can use the `EXTERNAL_QUERY()` function to query `INFORMATION_SCHEMA` views to access database metadata, such as listing all tables in the database or showing table schemas. The following example `INFORMATION_SCHEMA` queries work in both MySQL and PostgreSQL. You can learn more from [MySQL information_schema tables](https://dev.mysql.com/doc/refman/8.4/en/information-schema-introduction.html) and [PostgreSQL information_schema tables](https://www.postgresql.org/docs/current/information-schema.html) .

```
-- List all tables in a database.
SELECT * FROM EXTERNAL_QUERY("CONNECTION_ID",
"SELECT * FROM information_schema.tables;");
```

```
-- List all columns in a table.
SELECT * FROM EXTERNAL_QUERY("CONNECTION_ID",
"SELECT * FROM information_schema.columns WHERE table_name='x';");
```

Replace `CONNECTION_ID` with the ID of your BigQuery connection.

## Track BigQuery federated queries

When you run a federated query against Cloud SQL, BigQuery annotates the query with a comment similar to the following:

```
/* Federated query from BigQuery. Project ID: PROJECT_ID, BigQuery Job ID: JOB_ID. */
```

If you monitor logs for query usage on a MySQL or PostgreSQL database, the annotation helps you identify queries originating from BigQuery.

1.  In the Google Cloud console, go to the **Logs Explorer** page.

2.  In the **Query** tab, enter the following query:

    ```
    resource.type="cloudsql_database"
    textPayload=~"Federated query from BigQuery"
    ```

3.  Click **Run query** .

    If there are records available for BigQuery federated queries, a list of records similar to the following appears in **Query results** :

    ```
    YYYY-MM-DD hh:mm:ss.millis UTC [3210064]: [4-1]
    db=DATABASE, user=USER_ACCOUNT
    STATEMENT: SELECT 1 FROM (SELECT FROM company_name_table) t;
    /* Federated query from BigQuery.
    Project ID: PROJECT_ID, BigQuery Job ID: JOB_ID
    */

    YYYY-MM-DD hh:mm:ss.millis UTC [3210532]: [2-1]
    db=DATABASE, user=USER_ACCOUNT
    STATEMENT: SELECT "company_id", "company type_id" FROM
    (SELECT FROM company_name_table) t;
    /* Federated query from BigQuery.
    Project ID: PROJECT_ID, BigQuery Job ID: JOB_ID
    */
    ```

## Connection details

The following table shows the Cloud SQL connection properties:

| Property name               | Value  | Description                                                                                                                                                                                                                                                                                                                                    |
|-----------------------------|--------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                      | string | Name of the connection resource in the format: `projects/ `` PROJECT_ID `` /locations/ `` LOCATION `` /connections/ `` CONNECTION_ID` .                                                                                                                                                                                                        |
| `location`                  | string | Location of the connection which must either match the Cloud SQL instance location or be a multi-region of the corresponding jurisdiction. For example, a Cloud SQL instance in `us-east4` can use `US` , while a Cloud SQL instance in `europe-north1` can use `EU` . Only BigQuery queries running in this location can use this connection. |
| `friendlyName`              | string | A user-friendly display name for the connection.                                                                                                                                                                                                                                                                                               |
| `description`               | string | Description of the connection.                                                                                                                                                                                                                                                                                                                 |
| `cloudSql.type`             | string | Can be `POSTGRES` or `MYSQL` .                                                                                                                                                                                                                                                                                                                 |
| `cloudSql.instanceId`       | string | Name of the [Cloud SQL instance](https://docs.cloud.google.com/sql/docs/mysql/instance-settings#instance-id-2ndgen) , usually in the format: `PROJECT_ID `` : `` LOCATION `` : `` INSTANCE_ID` . You can find the instance ID on the [Cloud SQL instances](https://console.cloud.google.com/sql/instances) page.                               |
| `cloudSql.database`         | string | The Cloud SQL database to connect to.                                                                                                                                                                                                                                                                                                          |
| `cloudSql.serviceAccountId` | string | The service account configured to access the Cloud SQL database.                                                                                                                                                                                                                                                                               |

The following table shows the properties for the Cloud SQL instance credential:

| Property name | Value  | Description        |
|---------------|--------|--------------------|
| `username`    | string | Database username. |
| `password`    | string | Database password. |

## Query performance and best practices

To optimize the performance of federated queries and avoid placing unnecessary load on your Cloud SQL instance, consider the following best practices:

- **Filter early in the external query** : Apply `WHERE` filters and `GROUP BY` aggregations inside the `EXTERNAL_QUERY` SQL statement instead of filtering in the outer BigQuery query. Executing filters in Cloud SQL reduces the amount of data transferred across the network to BigQuery.
- **Prune columns** : Select only the specific columns needed in the `EXTERNAL_QUERY` statement rather than using `SELECT *` . This reduces network transfer volume and query execution time.
- **Use read replicas** : To isolate analytical query workloads from your primary production database, create a [Cloud SQL read replica](https://docs.cloud.google.com/sql/docs/mysql/replication#read-replicas) and configure your BigQuery connection to query the replica.
- **Colocate datasets and instances** : For lowest latency, locate your BigQuery dataset and connection in the same region as your Cloud SQL instance, or in the corresponding multi-region (such as `US` or `EU` ). For more information, see [Supported regions](https://docs.cloud.google.com/bigquery/docs/federated-queries-intro#supported_region_alloy_sql) .

## Troubleshooting

This section helps you troubleshoot issues you might encounter when sending a federated query to Cloud SQL.

### Failed to connect to database server

When you query a MySQL database, you might encounter the following error:

```
Invalid table-valued function EXTERNAL_QUERY Failed to connect to MySQL database. Error: MysqlErrorCode(2013): Lost connection to MySQL server during query.
```

When you query a PostgreSQL database, you might encounter the following error:

```
Invalid table-valued function EXTERNAL_QUERY Connect to PostgreSQL server failed: server closed the connection unexpectedly This probably means the server terminated abnormally before or while processing the request.
```

**Resolution**

To resolve this issue, verify the following prerequisites:

1.  Ensure that valid credentials were used and all setup steps were followed when [creating the connection for Cloud SQL](https://docs.cloud.google.com/bigquery/docs/connect-to-sql) .

2.  Verify that the BigQuery Connection service agent has been granted the Cloud SQL Client ( `roles/cloudsql.client` ) role. The service agent email is formatted as:

    ```
    service-PROJECT_NUMBER@gcp-sa-bigqueryconnection.iam.gserviceaccount.com
    ```

    For detailed instructions, see [Grant access to the service agent](https://docs.cloud.google.com/bigquery/docs/connect-to-sql#access-sql) .

3.  If your Cloud SQL instance uses a private IP address, ensure that you enabled a private path when you [created the Cloud SQL instance](https://docs.cloud.google.com/sql/docs/postgres/create-instance) . Enabling a private path lets BigQuery access data in Cloud SQL and run queries over a private connection.

### Failed to connect to MySQL database due to authentication plugin

When you run a federated query against a MySQL instance, you might encounter the following error:

```
Invalid table-valued function EXTERNAL_QUERY Failed to connect to MySQL database. Error: MysqlErrorCode(2059): Authentication plugin 'caching_sha2_password' cannot be loaded: /usr/lib/plugin/caching_sha2_password.so: cannot open shared object file: No such file or directory at [1:15]
```

**Resolution**

This error occurs for database user accounts configured with [caching_sha2_password authentication](https://dev.mysql.com/doc/refman/8.4/en/native-pluggable-authentication.html) , which is not supported for federated queries.

If your Cloud SQL instance runs MySQL version 8.0 or earlier, you can change the authentication plugin for the user account used by BigQuery. Run the following command on the Cloud SQL instance:

```
ALTER USER 'USERNAME'@'%' IDENTIFIED WITH mysql_native_password BY 'PASSWORD';
```

Replace the following:

- `USERNAME` : The database user account that BigQuery uses to connect to your Cloud SQL for MySQL instance.
- `PASSWORD` : The password for the database user account.

If your Cloud SQL instance runs MySQL version 8.4, the `mysql_native_password` plugin is deprecated. We do not recommend downgrading an existing database from 8.4 to 8.0 for production workloads.

Upgrading an instance from an earlier version to MySQL 8.4 does not affect existing database connections, provided that you do not change the user authentication plugin before upgrading. Because only users created with `mysql_native_password` can be used for federated queries, queries sent to MySQL 8.4 must use a user account created before upgrading.

## Limitations

Federated queries in Cloud SQL are subject to the following limitations:

- **Read-only queries** : Federated queries are read-only. External queries must be `SELECT` statements; data definition language (DDL) and data manipulation language (DML) statements are not supported.
- **Query performance** : Federated queries are not as fast as querying BigQuery storage. BigQuery must wait for Cloud SQL to execute the external query and transfer the result set over the network.
- **Region constraints** : The BigQuery query processing location must match or be compatible with the Cloud SQL instance location. For more information, see [Supported regions](https://docs.cloud.google.com/bigquery/docs/federated-queries-intro#supported_region_alloy_sql) .
- **Unsupported data types** : If an external query returns a data type that is not supported by BigQuery, the query fails. You can cast the unsupported data type to a supported data type within the external query. For more information, see [Data type mappings](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/federated_query_functions#mysql_mapping) .
- **Maximum connections** : A federated query can reference at most 10 unique connections.
- **Authentication plugin limitation** : The MySQL `caching_sha2_password` plugin is not supported for federated queries. For more information, see [Troubleshooting](https://docs.cloud.google.com/bigquery/docs/cloud-sql-federated-queries#mysql_auth_plugin) .

## What's next

- Learn about [federated queries](https://docs.cloud.google.com/bigquery/docs/federated-queries-intro) .
- Learn about [MySQL to BigQuery data type mapping](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/federated_query_functions#mysql_mapping) .
- Learn about [PostgreSQL to BigQuery data type mapping](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/federated_query_functions#postgresql_mapping) .
- Learn about [unsupported data types](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/federated_query_functions#unsupported_data_types) .
