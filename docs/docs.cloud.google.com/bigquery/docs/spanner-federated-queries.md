# Spanner federated queries

As a data analyst, you can query data in Spanner from BigQuery using [federated queries](/bigquery/docs/federated-queries-intro) .

BigQuery Spanner federation enables BigQuery to query data residing in Spanner in real-time, without copying or moving data.

You can query Spanner data in two ways:

  - Create a Spanner external dataset.
  - Use an [`  EXTERNAL_QUERY  `](/bigquery/docs/reference/standard-sql/federated_query_functions#external_query) function.

## Use external datasets

The simplest way to query Spanner tables is to [create an external dataset](/bigquery/docs/spanner-external-datasets) . Once you create the external dataset, your tables from the corresponding Spanner database are visible in BigQuery and you can use them in your queries - for example in joins, unions or subqueries. However, no data is moved from Spanner to BigQuery storage.

You don't need to create a connection to query Spanner data if you create an external dataset.

## Use `     EXTERNAL_QUERY    ` function

Like for other federated databases, you can also query Spanner data with an [`  EXTERNAL_QUERY  `](/bigquery/docs/reference/standard-sql/federated_query_functions#external_query) function. This may be useful if you want to have more control over the connection parameters.

### Before you begin

  - Ensure that your BigQuery administrator has created a [Spanner connection](/bigquery/docs/connect-to-spanner#create-spanner-connection) and [shared](/bigquery/docs/connect-to-spanner#share_connections) it with you. See [Choose the right connection](#right-connection) .

  - To get the permissions that you need to query a Spanner instance, ask your administrator to grant you the BigQuery Connection User ( `  roles/bigquery.connectionUser  ` ) Identity and Access Management (IAM) role. You also need to ask your administrator to grant you one of the following:
    
      - If you are a fine-grained access control user, you need access to a database role that has the `  SELECT  ` privilege on all Spanner schema objects in your queries.
      - If you aren't a fine-grained access control user, you need the Cloud Spanner Database Reader ( `  roles/spanner.databaseReader  ` ) IAM role.
    
    For information about granting IAM roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) . For information about fine-grained access control, see [About fine-grained access control](/spanner/docs/fgac-about) .

### Choose the right connection

If you are a Spanner fine-grained access control user, when you run a federated query with an [`  EXTERNAL_QUERY  `](/bigquery/docs/reference/standard-sql/federated_query_functions#external_query) function, you must use a Spanner connection that specifies a database role. Then all queries that you run with this connection use that database role.

If you use a connection that doesn't specify a database role, you must have the IAM roles indicated in [Before you begin](#begin) .

### Query data

To send a federated query to Spanner from a GoogleSQL query, use the [`  EXTERNAL_QUERY  `](/bigquery/docs/reference/standard-sql/federated_query_functions#external_query) function.

Formulate your Spanner query in either GoogleSQL or PostgreSQL, depending on the specified dialect of the database.

The following example makes a federated query to a Spanner database named `  orders  ` and joins the results with a BigQuery table named `  mydataset.customers  ` .

``` text
SELECT c.customer_id, c.name, rq.first_order_date
FROM mydataset.customers AS c
LEFT OUTER JOIN EXTERNAL_QUERY(
  'my-project.us.example-db',
  '''SELECT customer_id, MIN(order_date) AS first_order_date
  FROM orders
  GROUP BY customer_id''') AS rq
  ON rq.customer_id = c.customer_id
GROUP BY c.customer_id, c.name, rq.first_order_date;
```

## Spanner Data Boost

Data Boost is a fully managed, serverless feature that provides independent compute resources for supported Spanner workloads. Data Boost lets you execute analytics queries and data exports with near-zero impact to existing workloads on the provisioned Spanner instance. Data Boost lets you run federated queries with independent compute capacity separate from your provisioned instances to avoid impacting existing workloads on Spanner. Data Boost is most impactful when you run complex ad hoc queries, or when you want to process large amounts of data without impacting the existing Spanner workload. Running federated queries with Data Boost can lead to significantly lower CPU consumption, and in some cases, lower query latency.

### Before you begin

To get the permission that you need to enable access to Data Boost, ask your administrator to grant you the [Cloud Spanner Database Reader with DataBoost](/iam/docs/roles-permissions/spanner#spanner.databaseReaderWithDataBoost) ( `  roles/spanner.databaseReaderWithDataBoost  ` ) IAM role on the Spanner database. For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

This predefined role contains the `  spanner.databases.useDataBoost  ` permission, which is required to enable access to Data Boost.

You might also be able to get this permission with [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

### Enable Data Boost

When using external datasets, Data Boost is always used and you don't have to enable it manually.

If you want to use Data Boost for your `  EXTERNAL_QUERY  ` queries, you must enable it when [creating a connection](/bigquery/docs/connect-to-spanner) that is used by your query.

## Read data in parallel

Spanner can divide certain queries into smaller pieces, or partitions, and fetch the partitions in parallel. For more information, including a list of limitations, see [Read data in parallel](/spanner/docs/reads#read_data_in_parallel) in the Spanner documentation.

To view the query execution plan for a Spanner query, see [Understand how Spanner executes queries](/spanner/docs/sql-best-practices#how-execute-queries) .

When running federated queries with external datasets, the "Read data in parallel" option is always used.

To enable parallel reads when using the [`  EXTERNAL_QUERY  `](/bigquery/docs/reference/standard-sql/federated_query_functions#external_query) , enable it when you [create the Connection](/bigquery/docs/connect-to-spanner) .

## Manage query execution priority

When you run federated queries with an `  EXTERNAL_QUERY  ` function, you can assign priority ( `  high  ` , `  medium  ` , or `  low  ` ) to individual queries by specifying the `  query_execution_priority  ` option:

``` text
SELECT *
FROM EXTERNAL_QUERY(
  'my-project.us.example-db',
  '''SELECT customer_id, MIN(order_date) AS first_order_date
  FROM orders
  GROUP BY customer_id''',
  '{"query_execution_priority":"high"}');
```

The default priority is `  medium  ` .

Queries with priority `  high  ` will compete with transactional traffic. Queries with priority `  low  ` are best-effort, and might get preempted by background load, for example scheduled backups.

**Caution:** Queries with `  low  ` priority fall below queries like backup jobs which might never complete within the timeouts for BigQuery.

When running federated queries with external datasets, all queries have always `  medium  ` priority.

## View a Spanner table schema

If you use external datasets, your Spanner tables are visible directly in BigQuery Studio and you can see their schemas.

However, you can also see the schemas without defining external datasets. You can use `  EXTERNAL_QUERY  ` function also to query information\_schema views to access database metadata. The following example returns information about the columns in the table `  MyTable  ` :

### Google SQL database

``` text
SELECT *
FROM EXTERNAL_QUERY(
  'my-project.us.example-db',
  '''SELECT t.column_name, t.spanner_type, t.is_nullable
    FROM information_schema.columns AS t
    WHERE
      t.table_catalog = ''
      AND t.table_schema = ''
     AND t.table_name = 'MyTable'
    ORDER BY t.ordinal_position
  ''');
```

### PostgreSQL database

``` text
SELECT * from EXTERNAL_QUERY(
 'my-project.us.postgresql.example-db',
  '''SELECT t.column_name, t.data_type, t.is_nullable
    FROM information_schema.columns AS t
    WHERE
      t.table_schema = 'public' and t.table_name='MyTable'
    ORDER BY t.ordinal_position
  ''');
```

For more information, see the following information schema references in the Spanner documentation:

  - [GoogleSQL information schema](/spanner/docs/information-schema)
  - [PostgreSQL information schema](/spanner/docs/information-schema-pg)

## Pricing

  - On the BigQuery side, standard [federated query pricing](/bigquery/docs/federated-queries-intro#pricing) applies.
  - On the Spanner side, queries are subject to [Spanner pricing](https://cloud.google.com/spanner/pricing) .

## Cross region queries

BigQuery supports federated queries where Spanner instances and BigQuery datasets are in different regions. These queries incur an additional Spanner data transfer charge. For more information see [Spanner pricing](https://cloud.google.com/spanner/pricing#network) .

You are charged for the data transfer, based on the following [SKUs](/skus/sku-groups/cloud-spanner) :

  - Network Intra-region Cross-Zone Data Transfer Out
  - Network Inter-Region Data Transfer Out to the Same Continent
  - Network Inter-Region Data Transfer Out to a Different Continent

Data transfer is charged based on the BigQuery region you run the query in and the nearest Spanner region that has read-write or read-only replicas.

For BigQuery multi-region configurations ( `  US  ` or `  EU  ` ), data transfer costs from Spanner are determined as follows:

  - BigQuery `  US  ` multi-region: Spanner region `  us-central1  `
  - BigQuery `  EU  ` multi-region: Spanner region `  europe-west1  `

For example:

  - BigQuery ( `  US  ` multi-region) and Spanner ( `  us-central1  ` ): Costs apply for data transfer within the same region.
  - BigQuery ( `  US  ` multi-region) and Spanner ( `  us-west4  ` ): Costs apply for Data transfer between regions within the same continent.

## Troubleshooting

This section helps you troubleshoot issues you might encounter when sending a federated query to Spanner.

  - Issue: Query is not root partitionable.  
    **Resolution:** If you configure the connection to read data in parallel, either the first operator in the query execution plan must be a distributed union, or your execution plan must not have any distributed unions. To resolve this error, view the query execution plan and rewrite the query. For more information, see [Understand how Spanner executes queries](/spanner/docs/sql-best-practices#how-execute-queries) .
  - Issue: Deadline exceeded.  
    **Resolution:** Select the option to [read data in parallel](#read_data_in_parallel) and rewrite the query to be root partitionable. For more information, see [Understand how Spanner executes queries](/spanner/docs/sql-best-practices#how-execute-queries) .

## What's next

  - Learn about [creating Spanner external datasets](/bigquery/docs/spanner-external-datasets)
  - Learn about [federated queries](/bigquery/docs/federated-queries-intro) .
  - Learn about [Spanner to BigQuery data type mapping](/bigquery/docs/reference/standard-sql/federated_query_functions#spanner-mapping) .
