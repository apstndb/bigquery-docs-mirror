# Cloud SQL federated queries

As a data analyst, you can query data in Cloud SQL from BigQuery using [federated queries](/bigquery/docs/federated-queries-intro) .

BigQuery Cloud SQL federation enables BigQuery to query data residing in Cloud SQL in real time, without copying or moving data. Query federation supports both MySQL (2nd generation) and PostgreSQL instances in Cloud SQL.

Alternatively, to replicate data into BigQuery, you can also use Cloud Data Fusion or [Datastream](/datastream/docs/overview) . For more about using Cloud Data Fusion, see [Replicating data from MySQL to BigQuery](/data-fusion/docs/tutorials/replicating-data/mysql-to-bigquery) .

## Before you begin

  - Ensure that your BigQuery administrator has created a [Cloud SQL connection](/bigquery/docs/connect-to-sql#create-sql-connection) and [shared](/bigquery/docs/connect-to-sql#share_connections) it with you.

  - To get the permissions that you need to query a Cloud SQL instance, ask your administrator to grant you the [BigQuery Connection User](/iam/docs/roles-permissions/bigquery#bigquery.connectionUser) ( `  roles/bigquery.connectionUser  ` ) IAM role on your project. For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .
    
    You might also be able to get the required permissions through [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

## Query data

To send a federated query to Cloud SQL from a GoogleSQL query, use the [`  EXTERNAL_QUERY  ` function](/bigquery/docs/reference/standard-sql/federated_query_functions#external_query) .

Suppose that you store a customer table in BigQuery, while storing a sales table in Cloud SQL, and want to join the two tables in a single query. The following example makes a federated query to a Cloud SQL table named `  orders  ` and joins the results with a BigQuery table named `  mydataset.customers  ` .

``` text
SELECT c.customer_id, c.name, rq.first_order_date
FROM mydataset.customers AS c
LEFT OUTER JOIN EXTERNAL_QUERY(
  'us.connection_id',
  '''SELECT customer_id, MIN(order_date) AS first_order_date
  FROM orders
  GROUP BY customer_id''') AS rq ON rq.customer_id = c.customer_id
GROUP BY c.customer_id, c.name, rq.first_order_date;
```

The example query includes 3 parts:

1.  Run the external query `  SELECT customer_id, MIN(order_date) AS first_order_date FROM orders GROUP BY customer_id  ` in the operational PostgreSQL database to get the first order date for each customer through the `  EXTERNAL_QUERY()  ` function.
2.  Join the external query result table with the customers table in BigQuery by `  customer_id  ` .
3.  Select customer information and first order date.

## View a Cloud SQL table schema

You can use the `  EXTERNAL_QUERY()  ` function to query information\_schema tables to access database metadata, such as list all tables in the database or show table schema. The following example information\_schema queries work in both MySQL and PostgreSQL. You can learn more from [MySQL information\_schema tables](https://dev.mysql.com/doc/refman/8.0/en/information-schema-introduction.html) and [PostgreSQL information\_schema tables](https://www.postgresql.org/docs/9.1/information-schema.html) .

``` text
-- List all tables in a database.
SELECT * FROM EXTERNAL_QUERY("connection_id",
"select * from information_schema.tables;");
```

``` text
-- List all columns in a table.
SELECT * FROM EXTERNAL_QUERY("connection_id",
"select * from information_schema.columns where table_name='x';");
```

## Connection details

The following table shows the Cloud SQL connection properties:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Property name</th>
<th>Value</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       name      </code></td>
<td>string</td>
<td>Name of the connection resource in the format: project_id.location_id.connection_id.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       location      </code></td>
<td>string</td>
<td>Location of the connection which must either match the Cloud SQL instance location or be a multi-region of the corresponding jurisdiction. For example, a Cloud SQL instance in <code dir="ltr" translate="no">       us-east4      </code> can use <code dir="ltr" translate="no">       US      </code> , while a Cloud SQL instance in <code dir="ltr" translate="no">       europe-north1      </code> can use <code dir="ltr" translate="no">       EU      </code> . Only BigQuery queries running in this location will be able to use this connection.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       friendlyName      </code></td>
<td>string</td>
<td>A user-friendly display name for the connection.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       description      </code></td>
<td>string</td>
<td>Description of the connection.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       cloudSql.type      </code></td>
<td>string</td>
<td>Can be "POSTGRES" or "MYSQL".</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       cloudSql.instanceId      </code></td>
<td>string</td>
<td>Name of the <a href="/sql/docs/mysql/instance-settings#instance-id-2ndgen">Cloud SQL instance</a> , usually in the format of:<br />
<br />
<code dir="ltr" translate="no">       Project-id:location-id:instance-id      </code><br />
<br />
You can find the instance ID in the <a href="https://console.cloud.google.com/sql/instances">Cloud SQL instance</a> detail page.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       cloudSql.database      </code></td>
<td>string</td>
<td>The Cloud SQL database that you want to connect to.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       cloudSql.serviceAccountId      </code></td>
<td>string</td>
<td>The service account configured to access the Cloud SQL database.</td>
</tr>
</tbody>
</table>

The following table shows the properties for the Cloud SQL instance credential:

<table>
<thead>
<tr class="header">
<th>Property name</th>
<th>Value</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       username      </code></td>
<td>string</td>
<td>Database username</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       password      </code></td>
<td>string</td>
<td>Database password</td>
</tr>
</tbody>
</table>

## Track BigQuery federated queries

When you run a federated query against Cloud SQL, BigQuery annotates the query with a comment similar to the following:

``` text
/* Federated query from BigQuery. Project ID: PROJECT_ID, BigQuery Job ID: JOB_ID. */
```

If you are monitoring logs for query usage on a MySQL or PostgreSQL database, the following annotation can help you identify queries coming from BigQuery.

1.  Go to the **Logs Explorer** page.

2.  In the **Query** tab, enter the following query:
    
    ``` text
    resource.type="cloudsql_database"
    textPayload=~"Federated query from BigQuery"
    ```

3.  Click **Run query** .
    
    If there are records available for BigQuery federated queries, a list of records similar to the following appears in **Query results** :
    
    ``` text
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

## Troubleshooting

This section helps you troubleshoot issues you might encounter when sending a federated query to Cloud SQL.

**Issue:** Failed to connect to database server. If you are querying a MySQL database, you might encounter the following error:

`  Invalid table-valued function EXTERNAL_QUERY Failed to connect to MySQL database. Error: MysqlErrorCode(2013): Lost connection to MySQL server during query.  `

Alternatively, if you are querying a PostgreSQL database, you might encounter the following error:

  - `  Invalid table-valued function EXTERNAL_QUERY Connect to PostgreSQL server failed: server closed the connection unexpectedly This probably means the server terminated abnormally before or while processing the request.  `  
    **Resolution:** Ensure that valid credentials were used and all prerequisites were followed to create the [connection for Cloud SQL](/bigquery/docs/connect-to-sql) . Check if the service account that is automatically created when a connection to Cloud SQL is created has the Cloud SQL Client ( `  roles/cloudsql.client  ` ) role. The service account is of the following format: `  service- PROJECT_NUMBER @gcp-sa-bigqueryconnection.iam.gserviceaccount.com  ` . For detailed instructions, see [Grant access to the service account](/bigquery/docs/connect-to-sql#access-sql) .

## What's next

  - Learn about [federated queries](/bigquery/docs/federated-queries-intro) .
  - Learn about [MySQL to BigQuery data type mapping](/bigquery/docs/reference/standard-sql/federated_query_functions#mysql_mapping) .
  - Learn about [PostgreSQL to BigQuery data type mapping](/bigquery/docs/reference/standard-sql/federated_query_functions#postgresql_mapping) .
  - Learn about [unsupported data types](/bigquery/docs/reference/standard-sql/federated_query_functions#unsupported_data_types) .
