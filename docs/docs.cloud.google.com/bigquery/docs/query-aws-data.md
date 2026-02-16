# Query Amazon S3 data

**Important:** The term "BigLake" on this page refers to an access delegation functionality for external tables in BigQuery. For information about BigLake, the stand-alone Google Cloud product that includes BigLake metastore, the Apache Iceberg REST catalog, and BigLake tables for Apache Iceberg see [BigLake overview](/biglake/docs/introduction) .

This document describes how to query data stored in an [Amazon Simple Storage Service (Amazon S3) BigLake table](/bigquery/docs/omni-aws-create-external-table) .

## Before you begin

Ensure that you have a [Amazon S3 BigLake table](/bigquery/docs/omni-aws-create-external-table) .

### Required roles

To query Amazon S3 BigLake tables, ensure that the caller of the BigQuery API has the following roles:

  - BigQuery Connection User ( `  roles/bigquery.connectionUser  ` )
  - BigQuery Data Viewer ( `  roles/bigquery.dataViewer  ` )
  - BigQuery User ( `  roles/bigquery.user  ` )

The caller can be your account or an [Amazon S3 connection service account](/bigquery/docs/omni-aws-create-connection#creating-aws-connection) . Depending on your permissions, you can grant these roles to yourself or ask your administrator to grant them to you. For more information about granting roles, see [Viewing the grantable roles on resources](/iam/docs/viewing-grantable-roles) .

To see the exact permissions that are required to query Amazon S3 BigLake tables, expand the **Required permissions** section:

#### Required permissions

  - `  bigquery.connections.use  `
  - `  bigquery.jobs.create  `
  - `  bigquery.readsessions.create  ` (Only required if you are [reading data with the BigQuery Storage Read API](/bigquery/docs/reference/storage) )
  - `  bigquery.tables.get  `
  - `  bigquery.tables.getData  `

You might also be able to get these permissions with [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

## Query Amazon S3 BigLake tables

After creating a Amazon S3 BigLake table, you can [query it using GoogleSQL syntax](/bigquery/docs/running-queries) , the same as if it were a standard BigQuery table.

The [cached query results](/bigquery/docs/cached-results) are stored in a BigQuery temporary table. To query a temporary BigLake table, see [Query a temporary BigLake table](#query-temp-biglake-table) . For more information about BigQuery Omni limitations and quotas, see [limitations](/bigquery/docs/omni-introduction#limitations) and [quotas](/bigquery/docs/omni-introduction#quotas_and_limits) .

When creating a reservation in a BigQuery Omni region, use the Enterprise edition. To learn how to create a reservation with an edition, see [Create reservations](/bigquery/docs/reservations-tasks#create_reservations) .

Run a query on a BigLake Amazon S3 table:

### SQL

To query the table:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
    SELECT * FROM DATASET_NAME.TABLE_NAME;
    ```
    
    Replace the following:
    
      - `  DATASET_NAME  ` : the dataset name that you created
    
      - `  TABLE_NAME  ` : the name of the [table that you created](#create-biglake-table)
    
      - Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](/bigquery/docs/running-queries#queries) .

### Java

Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Java API reference documentation](/java/docs/reference/google-cloud-bigquery/latest/overview) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` java
import com.google.cloud.bigquery.BigQuery;
import com.google.cloud.bigquery.BigQueryException;
import com.google.cloud.bigquery.BigQueryOptions;
import com.google.cloud.bigquery.CsvOptions;
import com.google.cloud.bigquery.DatasetId;
import com.google.cloud.bigquery.ExternalTableDefinition;
import com.google.cloud.bigquery.Field;
import com.google.cloud.bigquery.QueryJobConfiguration;
import com.google.cloud.bigquery.Schema;
import com.google.cloud.bigquery.StandardSQLTypeName;
import com.google.cloud.bigquery.TableId;
import com.google.cloud.bigquery.TableInfo;
import com.google.cloud.bigquery.TableResult;

// Sample to queries an external data source aws s3 using a permanent table
public class QueryExternalTableAws {

  public static void main(String[] args) throws InterruptedException {
    // TODO(developer): Replace these variables before running the sample.
    String projectId = "MY_PROJECT_ID";
    String datasetName = "MY_DATASET_NAME";
    String externalTableName = "MY_EXTERNAL_TABLE_NAME";
    // Query to find states starting with 'W'
    String query =
        String.format(
            "SELECT * FROM s%.%s.%s WHERE name LIKE 'W%%'",
            projectId, datasetName, externalTableName);
    queryExternalTableAws(query);
  }

  public static void queryExternalTableAws(String query) throws InterruptedException {
    try {
      // Initialize client that will be used to send requests. This client only needs to be created
      // once, and can be reused for multiple requests.
      BigQuery bigquery = BigQueryOptions.getDefaultInstance().getService();

      TableResult results = bigquery.query(QueryJobConfiguration.of(query));

      results
          .iterateAll()
          .forEach(row -> row.forEach(val -> System.out.printf("%s,", val.toString())));

      System.out.println("Query on aws external permanent table performed successfully.");
    } catch (BigQueryException e) {
      System.out.println("Query not performed \n" + e.toString());
    }
  }
}
```

## Query a temporary table

BigQuery creates temporary tables to store query results. To retrieve query result from temporary tables, you can use the Google Cloud console or the [BigQuery API](/bigquery/docs/reliability-read#read_with_api) .

Select one of the following options:

### Console

When you [query a BigLake table](#query-biglake-table) that references external cloud data, you can view the query results displayed in the Google Cloud console.

### API

To query a BigLake table using the API, follow these steps:

1.  Create a [Job object](/bigquery/docs/reference/rest/v2/Job) .
2.  Call the [`  jobs.insert  ` method](/bigquery/docs/reference/v2/jobs/insert) to run the query asynchronously or the [`  jobs.query  ` method](/bigquery/docs/reference/rest/v2/jobs/query) to run the query synchronously, passing in the `  Job  ` object.
3.  Read rows with the [`  jobs.getQueryResults  `](/bigquery/docs/reference/rest/v2/jobs/getQueryResults) by passing the given job reference, and the [`  tabledata.list  `](/bigquery/docs/reference/rest/v2/tabledata/list) methods by passing the given table reference of the query result.

## Query the `     _FILE_NAME    ` pseudocolumn

Tables based on external data sources provide a pseudocolumn named `  _FILE_NAME  ` . This column contains the fully qualified path to the file to which the row belongs. This column is available only for tables that reference external data stored in **Cloud Storage** , **Google Drive** , **Amazon S3** , and **Azure Blob Storage** .

The `  _FILE_NAME  ` column name is reserved, which means that you cannot create a column by that name in any of your tables. To select the value of `  _FILE_NAME  ` , you must use an alias. The following example query demonstrates selecting `  _FILE_NAME  ` by assigning the alias `  fn  ` to the pseudocolumn.

``` text
  bq query \
  --project_id=PROJECT_ID \
  --use_legacy_sql=false \
  'SELECT
     name,
     _FILE_NAME AS fn
   FROM
     `DATASET.TABLE_NAME`
   WHERE
     name contains "Alex"' 
```

Replace the following:

  - `  PROJECT_ID  ` is a valid project ID (this flag is not required if you use Cloud Shell or if you set a default project in the Google Cloud CLI)
  - `  DATASET  ` is the name of the dataset that stores the permanent external table
  - `  TABLE_NAME  ` is the name of the permanent external table

When the query has a filter predicate on the `  _FILE_NAME  ` pseudocolumn, BigQuery attempts to skip reading files that do not satisfy the filter. Similar recommendations to [querying ingestion-time partitioned tables using pseudocolumns](/bigquery/docs/querying-partitioned-tables#query_an_ingestion-time_partitioned_table) apply when constructing query predicates with the `  _FILE_NAME  ` pseudocolumn.

## What's next

  - Learn about [using SQL in BigQuery](/bigquery/docs/introduction-sql) .
  - Learn about [BigQuery Omni](/bigquery/docs/omni-introduction) .
  - Learn about [BigQuery quotas](/bigquery/quotas) .
