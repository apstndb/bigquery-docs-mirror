# Data definition language (DDL) statements in GoogleSQL

Data definition language (DDL) statements let you create and modify BigQuery resources using [GoogleSQL](/bigquery/docs/reference/standard-sql) query syntax. You can use DDL commands to create, alter, and delete resources, such as the following:

  - [Datasets](/bigquery/docs/datasets-intro)
  - [Tables](/bigquery/docs/tables-intro)
  - [Table schemas](/bigquery/docs/managing-table-schemas)
  - [Table clones](/bigquery/docs/table-clones-intro)
  - [Table snapshots](/bigquery/docs/table-snapshots-intro)
  - [Views](/bigquery/docs/views)
  - [User-defined functions](#create_function_statement) (UDFs)
  - [Indexes](/bigquery/docs/search-intro)
  - [Capacity commitments and reservations](/bigquery/docs/reservations-intro)
  - [Row-level access policies](/bigquery/docs/managing-row-level-security)

## Required permissions

To create a job that runs a DDL statement, you must have the `  bigquery.jobs.create  ` permission for the project where you are running the job. Each DDL statement also requires specific permissions on the affected resources, which are documented under each statement.

### IAM roles

The predefined IAM roles `  bigquery.user  ` , `  bigquery.jobUser  ` , and `  bigquery.admin  ` include the required `  bigquery.jobs.create  ` permission.

For more information about IAM roles in BigQuery, see [Predefined roles and permissions](/bigquery/access-control) or the [IAM permissions reference](/iam/docs/permissions-reference) .

## Run DDL statements

You can run DDL statements by using the Google Cloud console, by using the bq command-line tool, by calling the [`  jobs.query  `](/bigquery/docs/reference/rest/v2/jobs/query) REST API, or programmatically using the [BigQuery API client libraries](/bigquery/docs/reference/libraries) .

### Console

1.  Go to the BigQuery page in the Google Cloud console.

2.  Click **Compose new query** .

3.  Enter the DDL statement into the **Query editor** text area. For example:
    
    ``` text
     CREATE TABLE mydataset.newtable ( x INT64 )
     
    ```

4.  Click **Run** .

### bq

Enter the [`  bq query  `](/bigquery/docs/reference/bq-cli-reference#bq_query) command and supply the DDL statement as the query parameter. Set the `  use_legacy_sql  ` flag to `  false  ` .

``` text
bq query --use_legacy_sql=false \
  'CREATE TABLE mydataset.newtable ( x INT64 )'
```

### API

Call the [`  jobs.query  `](/bigquery/docs/reference/rest/v2/jobs/query) method and supply the DDL statement in the request body's `  query  ` property.

DDL functionality extends the information returned by a [Jobs resource](/bigquery/docs/reference/rest/v2/jobs#resource) . `  statistics.query.statementType  ` includes the following additional values for DDL support:

  - `  CREATE_TABLE  `
  - `  CREATE_TABLE_AS_SELECT  `
  - `  DROP_TABLE  `
  - `  CREATE_VIEW  `
  - `  DROP_VIEW  `

`  statistics.query  ` has 2 additional fields:

`  ddlOperationPerformed  ` : The DDL operation performed, possibly dependent on the existence of the DDL target. Current values include:

  - `  CREATE  ` : The query created the DDL target.
  - `  SKIP  ` : No-op. Examples — `  CREATE TABLE IF NOT EXISTS  ` was submitted, and the table exists. Or `  DROP TABLE IF EXISTS  ` was submitted, and the table does not exist.
  - `  REPLACE  ` : The query replaced the DDL target. Example — `  CREATE OR REPLACE TABLE  ` was submitted, and the table already exists.
  - `  DROP  ` : The query deleted the DDL target.

`  ddlTargetTable  ` : When you submit a `  CREATE TABLE/VIEW  ` statement or a `  DROP TABLE/VIEW  ` statement, the target table is returned as an object with 3 fields:

  - "projectId": string
  - "datasetId": string
  - "tableId": string

### Java

Call the [`  BigQuery.create()  `](/java/docs/reference/google-cloud-bigquery/latest/com.google.cloud.bigquery.BigQuery#com_google_cloud_bigquery_BigQuery_create_com_google_cloud_bigquery_JobInfo_com_google_cloud_bigquery_BigQuery_JobOption____) method to start a query job. Call the [`  Job.waitFor()  `](/java/docs/reference/google-cloud-bigquery/latest/com.google.cloud.bigquery.Job#com_google_cloud_bigquery_Job_waitFor_com_google_cloud_RetryOption____) method to wait for the DDL query to finish.

Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Java API reference documentation](/java/docs/reference/google-cloud-bigquery/latest/overview) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` java
import com.google.cloud.bigquery.BigQuery;
import com.google.cloud.bigquery.BigQueryException;
import com.google.cloud.bigquery.BigQueryOptions;
import com.google.cloud.bigquery.Job;
import com.google.cloud.bigquery.JobInfo;
import com.google.cloud.bigquery.QueryJobConfiguration;

// Sample to create a view using DDL
public class DDLCreateView {

  public static void runDDLCreateView() {
    // TODO(developer): Replace these variables before running the sample.
    String projectId = "MY_PROJECT_ID";
    String datasetId = "MY_DATASET_ID";
    String tableId = "MY_VIEW_ID";
    String ddl =
        "CREATE VIEW "
            + "`"
            + projectId
            + "."
            + datasetId
            + "."
            + tableId
            + "`"
            + " OPTIONS("
            + " expiration_timestamp=TIMESTAMP_ADD("
            + " CURRENT_TIMESTAMP(), INTERVAL 48 HOUR),"
            + " friendly_name=\"new_view\","
            + " description=\"a view that expires in 2 days\","
            + " labels=[(\"org_unit\", \"development\")]"
            + " )"
            + " AS SELECT name, state, year, number"
            + " FROM `bigquery-public-data.usa_names.usa_1910_current`"
            + " WHERE state LIKE 'W%'`";
    ddlCreateView(ddl);
  }

  public static void ddlCreateView(String ddl) {
    try {
      // Initialize client that will be used to send requests. This client only needs to be created
      // once, and can be reused for multiple requests.
      BigQuery bigquery = BigQueryOptions.getDefaultInstance().getService();

      QueryJobConfiguration config = QueryJobConfiguration.newBuilder(ddl).build();

      // create a view using query and it will wait to complete job.
      Job job = bigquery.create(JobInfo.of(config));
      job = job.waitFor();
      if (job.isDone()) {
        System.out.println("View created successfully");
      } else {
        System.out.println("View was not created");
      }
    } catch (BigQueryException | InterruptedException e) {
      System.out.println("View was not created. \n" + e.toString());
    }
  }
}
```

### Node.js

Before trying this sample, follow the Node.js setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Node.js API reference documentation](https://googleapis.dev/nodejs/bigquery/latest/index.html) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` javascript
// Import the Google Cloud client library and create a client
const {BigQuery} = require('@google-cloud/bigquery');
const bigquery = new BigQuery();

async function ddlCreateView() {
  // Creates a view via a DDL query

  /**
   * TODO(developer): Uncomment the following lines before running the sample.
   */
  // const projectId = "my_project"
  // const datasetId = "my_dataset"
  // const tableId = "my_new_view"

  const query = `
  CREATE VIEW \`${projectId}.${datasetId}.${tableId}\`
  OPTIONS(
      expiration_timestamp=TIMESTAMP_ADD(
          CURRENT_TIMESTAMP(), INTERVAL 48 HOUR),
      friendly_name="new_view",
      description="a view that expires in 2 days",
      labels=[("org_unit", "development")]
  )
  AS SELECT name, state, year, number
      FROM \`bigquery-public-data.usa_names.usa_1910_current\`
      WHERE state LIKE 'W%'`;

  // For all options, see https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query
  const options = {
    query: query,
  };

  // Run the query as a job
  const [job] = await bigquery.createQueryJob(options);

  job.on('complete', metadata => {
    console.log(`Created new view ${tableId} via job ${metadata.id}`);
  });
}
```

### Python

Call the [`  Client.query()  `](/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client#google_cloud_bigquery_client_Client_query) method to start a query job. Call the [`  QueryJob.result()  `](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJob#google_cloud_bigquery_job_QueryJob_result) method to wait for the DDL query to finish.

Before trying this sample, follow the Python setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Python API reference documentation](/python/docs/reference/bigquery/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` python
# from google.cloud import bigquery
# project = 'my-project'
# dataset_id = 'my_dataset'
# table_id = 'new_view'
# client = bigquery.Client(project=project)

sql = """
CREATE VIEW `{}.{}.{}`
OPTIONS(
    expiration_timestamp=TIMESTAMP_ADD(
        CURRENT_TIMESTAMP(), INTERVAL 48 HOUR),
    friendly_name="new_view",
    description="a view that expires in 2 days",
    labels=[("org_unit", "development")]
)
AS SELECT name, state, year, number
    FROM `bigquery-public-data.usa_names.usa_1910_current`
    WHERE state LIKE 'W%'
""".format(
    project, dataset_id, table_id
)

job = client.query(sql)  # API request.
job.result()  # Waits for the query to finish.

print(
    'Created new view "{}.{}.{}".'.format(
        job.destination.project,
        job.destination.dataset_id,
        job.destination.table_id,
    )
)
```

## On-demand query size calculation

If you use on-demand billing, BigQuery charges for data definition language (DDL) queries based on the number of bytes processed by the query.

<table>
<thead>
<tr class="header">
<th>DDL statement</th>
<th>Bytes processed</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       CREATE TABLE      </code></td>
<td>None.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       CREATE TABLE ... AS SELECT ...      </code></td>
<td>The sum of bytes processed for all the columns referenced from the tables scanned by the query.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       CREATE VIEW      </code></td>
<td>None.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       DROP TABLE      </code></td>
<td>None.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       DROP VIEW      </code></td>
<td>None.</td>
</tr>
</tbody>
</table>

For more information about cost estimation, see [Estimate and control costs](/bigquery/docs/best-practices-costs) .

## `     CREATE SCHEMA    ` statement

Creates a new dataset.

**Key Point:** This SQL statement uses the term `  SCHEMA  ` to refer to a logical collection of tables, views, and other resources. The equivalent concept in BigQuery is a *dataset* . In this context, `  SCHEMA  ` does not refer to BigQuery [table schemas](/bigquery/docs/schemas) .

### Syntax

``` text
CREATE SCHEMA [ IF NOT EXISTS ]
[project_name.]dataset_name
[DEFAULT COLLATE collate_specification]
[OPTIONS(schema_option_list)]
```

### Arguments

  - `  IF NOT EXISTS  ` : If any dataset exists with the same name, the `  CREATE  ` statement has no effect.

  - `  DEFAULT COLLATE collate_specification  ` : When a new table is created in the dataset, the table inherits a default [collation specification](/bigquery/docs/reference/standard-sql/collation-concepts#default_collation) unless a collation specification is explicitly specified for a table or a [column](#column_name_and_column_schema) .
    
    If you remove or change this collation specification later with the `  ALTER SCHEMA  ` statement, this will not change existing collation specifications in this dataset. If you want to update an existing collation specification in a dataset, you must alter the column that contains the specification.

  - `  project_name  ` : The name of the project where you are creating the dataset. Defaults to the project that runs this DDL statement.

  - `  dataset_name  ` : The name of the dataset to create.

  - [`  schema_option_list  `](#schema_option_list) : A list of options for creating the dataset.

### Details

The dataset is created in the location that you specify in the query settings. For more information, see [Specifying your location](/bigquery/docs/locations#specify_locations) .

For more information about creating a dataset, see [Creating datasets](/bigquery/docs/datasets) . For information about quotas, see [Dataset limits](/bigquery/quotas#dataset_limits) .

### `     schema_option_list    `

The option list specifies options for the dataset. Specify the options in the following format: `  NAME=VALUE, ...  `

The following options are supported:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">       NAME      </code></th>
<th><code dir="ltr" translate="no">       VALUE      </code></th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       default_kms_key_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Specifies the default Cloud KMS key for encrypting table data in this dataset. You can override this value when you create a table.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       default_partition_expiration_days      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
<td>Specifies the default expiration time, in days, for table partitions in this dataset. You can override this value when you create a table.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       default_rounding_mode      </code></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>Example: <code dir="ltr" translate="no">        default_rounding_mode = "ROUND_HALF_EVEN"       </code></p>
<p>This specifies the <a href="/bigquery/docs/reference/rest/v2/datasets#Dataset.FIELDS.default_rounding_mode"><code dir="ltr" translate="no">         defaultRoundingMode        </code></a> that is used for new tables created in this dataset. It does not impact existing tables. The following values are supported:</p>
<ul>
<li><code dir="ltr" translate="no">         "ROUND_HALF_AWAY_FROM_ZERO"        </code> : Halfway cases are rounded away from zero. For example, 2.25 is rounded to 2.3, and -2.25 is rounded to -2.3.</li>
<li><code dir="ltr" translate="no">         "ROUND_HALF_EVEN"        </code> : Halfway cases are rounded towards the nearest even digit. For example, 2.25 is rounded to 2.2 and -2.25 is rounded to -2.2.</li>
</ul></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       default_table_expiration_days      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
<td>Specifies the default expiration time, in days, for tables in this dataset. You can override this value when you create a table.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       description      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The description of the dataset.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       failover_reservation      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Associates the dataset to a reservation in the case of a failover scenario.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       friendly_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>A descriptive name for the dataset.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       is_case_insensitive      </code></td>
<td><code dir="ltr" translate="no">       BOOL      </code></td>
<td><code dir="ltr" translate="no">       TRUE      </code> if the dataset and its table names are case-insensitive, otherwise <code dir="ltr" translate="no">       FALSE      </code> . By default, this is <code dir="ltr" translate="no">       FALSE      </code> , which means the dataset and its table names are case-sensitive.
<ul>
<li>Datasets: <code dir="ltr" translate="no">         mydataset        </code> and <code dir="ltr" translate="no">         MyDataset        </code> can coexist in the same project, unless one of them has case-sensitivity turned off.</li>
<li>Tables: <code dir="ltr" translate="no">         mytable        </code> and <code dir="ltr" translate="no">         MyTable        </code> can coexist in the same dataset if case-sensitivity for the dataset is turned on.</li>
</ul></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       is_primary      </code></td>
<td><code dir="ltr" translate="no">       BOOLEAN      </code></td>
<td>Declares if the dataset is the primary replica.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       labels      </code></td>
<td><code dir="ltr" translate="no">       &lt;ARRAY&lt;STRUCT&lt;STRING, STRING&gt;&gt;&gt;      </code></td>
<td>An array of labels for the dataset, expressed as key-value pairs.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       location      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The location in which to create the dataset. If you don't specify this option, the dataset is created in the location where the query runs. If you specify this option and also explicitly set the location for the query job, the two values must match; otherwise the query fails.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       max_time_travel_hours      </code></td>
<td><code dir="ltr" translate="no">       SMALLINT      </code></td>
<td>Specifies the duration in hours of the <a href="/bigquery/docs/time-travel#time_travel">time travel window</a> for the dataset. The <code dir="ltr" translate="no">       max_time_travel_hours      </code> value must be an integer expressed in multiples of 24 (48, 72, 96, 120, 144, 168) between 48 (2 days) and 168 (7 days). 168 hours is the default if this option isn't specified.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       primary_replica      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The replica name to set as the <a href="/bigquery/docs/data-replication">primary replica</a> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       storage_billing_model      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><p>Alters the <a href="/bigquery/docs/datasets-intro#dataset_storage_billing_models">storage billing model</a> for the dataset. Set the <code dir="ltr" translate="no">        storage_billing_model       </code> value to <code dir="ltr" translate="no">        PHYSICAL       </code> to use physical bytes when calculating storage charges, or to <code dir="ltr" translate="no">        LOGICAL       </code> to use logical bytes. <code dir="ltr" translate="no">        LOGICAL       </code> is the default.</p>
<p>The <code dir="ltr" translate="no">        storage_billing_model       </code> option is only available for datasets that have been updated after December 1, 2022. For datasets that were last updated before that date, the storage billing model is <code dir="ltr" translate="no">        LOGICAL       </code> .</p>
<p>When you change a dataset's billing model, it takes 24 hours for the change to take effect.</p>
<p>Once you change a dataset's storage billing model, you must wait 14 days before you can change the storage billing model again.</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       tags      </code></td>
<td><code dir="ltr" translate="no">       &lt;ARRAY&lt;STRUCT&lt;STRING, STRING&gt;&gt;&gt;      </code></td>
<td>An array of IAM tags for the dataset, expressed as key-value pairs. The key should be the <a href="/iam/docs/tags-access-control#definitions">namespaced key name</a> , and the value should be the <a href="/iam/docs/tags-access-control#definitions">short name</a> .</td>
</tr>
</tbody>
</table>

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.datasets.create      </code></td>
<td>The project where you create the dataset.</td>
</tr>
</tbody>
</table>

### Examples

#### Creating a new dataset

The following example creates a dataset with a default table expiration and a set of labels.

``` text
CREATE SCHEMA mydataset
OPTIONS(
  location="us",
  default_table_expiration_days=3.75,
  labels=[("label1","value1"),("label2","value2")]
  )
```

#### Creating a case-insensitive dataset

The following example creates a case-insensitive dataset. Both the dataset name and table names inside the dataset are case-insensitive.

``` text
CREATE SCHEMA mydataset
OPTIONS(
  is_case_insensitive=TRUE
)
```

#### Creating a dataset with collation support

The following example creates a dataset with a collation specification.

``` text
CREATE SCHEMA mydataset
DEFAULT COLLATE 'und:ci'
```

## `     CREATE TABLE    ` statement

Creates a new table.

### Syntax

``` text
CREATE [ OR REPLACE ] [ TEMP | TEMPORARY ] TABLE [ IF NOT EXISTS ]
table_name
[(
  column | constraint_definition[, ...]
)]
[DEFAULT COLLATE collate_specification]
[PARTITION BY partition_expression]
[CLUSTER BY clustering_column_list]
[WITH CONNECTION connection_name]
[OPTIONS(table_option_list)]
[AS query_statement]

column:=
column_definition

constraint_definition:=
[primary_key]
| [[CONSTRAINT constraint_name] foreign_key, ...]

primary_key :=
PRIMARY KEY (column_name[, ...]) NOT ENFORCED

foreign_key :=
FOREIGN KEY (column_name[, ...]) foreign_reference

foreign_reference :=
REFERENCES primary_key_table(column_name[, ...]) NOT ENFORCED
```

### Arguments

  - `  OR REPLACE  ` : Replaces any table with the same name if it exists. Cannot appear with `  IF NOT EXISTS  ` .

  - `  TEMP | TEMPORARY  ` : Creates a [temporary table](/bigquery/docs/multi-statement-queries#temporary_tables) .

  - `  IF NOT EXISTS  ` : If any table exists with the same name, the `  CREATE  ` statement has no effect. Cannot appear with `  OR REPLACE  ` .

  - `  table_name  ` : The name of the table to create. See [Table path syntax](#table_path) . For temporary tables, do not include the project name or dataset name.

  - [`  column  `](#column_name_and_column_schema) : The table's schema information.

  - [`  constraint_definition  `](/bigquery/docs/information-schema-table-constraints) : An expression that defines a table constraint.

  - [`  collation_specification  `](/bigquery/docs/reference/standard-sql/collation-concepts#default_collation) : When a new column is added to the table without an explicit collation specification, the [column](#column_name_and_column_schema) inherits this collation specification for `  STRING  ` types.
    
    If you remove or change this collation specification later with the `  ALTER TABLE  ` statement, this will not change existing collation specifications in this table. If you want to update an existing collation specification in a table, you must alter the column that contains the specification.
    
    If the table is part of a dataset, the default collation specification for this table overrides the default collation specification for the dataset.

  - [`  partition_expression  `](#partition_expression) : An expression that determines how to partition the table.

  - [`  clustering_column_list  `](#clustering_column_list) : A comma-separated list of column references that determine how to cluster the table. You cannot have collation on columns in this list.

  - `  connection_name  ` : Specifies a [connection resource](/bigquery/docs/connections-api-intro) that has credentials for accessing the external data. Specify the connection name in the form PROJECT\_ID . LOCATION . CONNECTION\_ID . If the project ID or location contains a dash, enclose the connection name in backticks ( ``  `  `` ). To use a [default connection](/bigquery/docs/default-connections) , specify `  DEFAULT  ` instead of the connection string containing PROJECT\_ID . LOCATION . CONNECTION\_ID .

  - [`  table_option_list  `](#table_option_list) : A list of options for creating the table.

  - `  query_statement  ` : The query from which the table should be created. For the query syntax, see [SQL syntax reference](/bigquery/docs/reference/standard-sql/query-syntax) . If a collation specification is used on this table, collation passes through this query statement.

  - `  primary_key  ` : An expression that defines a primary key [table constraint](/bigquery/docs/primary-foreign-keys) . BigQuery only supports unenforced primary keys.

  - `  foreign_key  ` : An expression that defines a foreign key [table constraint](/bigquery/docs/primary-foreign-keys) . BigQuery only supports unenforced foreign keys.

### Details

`  CREATE TABLE  ` statements must comply with the following rules:

  - Only one `  CREATE  ` statement is allowed.
  - Either the column list, the `  AS query_statement  ` clause, or both must be present.
  - When both the column list and the `  AS query_statement  ` clause are present, BigQuery ignores the names in the `  AS query_statement  ` clause and matches the columns with the column list by position.
  - When the `  AS query_statement  ` clause is present and the column list is absent, BigQuery determines the column names and types from the `  AS query_statement  ` clause.
  - Column names must be specified either through the column list, the `  AS query_statement  ` clause or schema of the table in the `  LIKE  ` clause.
  - Duplicate column names are not allowed.
  - When both the `  LIKE  ` and the `  AS query_statement  ` clause are present, the column list in the query statement must match the columns of the table referenced by the `  LIKE  ` clause.
  - Table names are case-sensitive unless the dataset they belong to is not. To create a case-insensitive dataset, see [Creating a case-insensitive dataset](/bigquery/docs/reference/standard-sql/data-definition-language#creating_a_case-insensitive_dataset) . To alter a dataset to make it case-insensitive dataset, see [Turning on case insensitivity for a dataset](/bigquery/docs/reference/standard-sql/data-definition-language#turning_on_case_insensitivity_for_a_dataset) .

Limitations:

  - It is not possible to create an [ingestion-time partitioned table](/bigquery/docs/creating-partitioned-tables) from the result of a query. Instead, use a `  CREATE TABLE  ` DDL statement to create the table, and then use an [`  INSERT  ` DML statement](/bigquery/docs/reference/standard-sql/dml-syntax#insert_statement) to insert data into it.
  - It is not possible to use the `  OR REPLACE  ` modifier to replace a table with a different kind of partitioning. Instead, `  DROP  ` the table, and then use a `  CREATE TABLE ... AS SELECT ...  ` statement to recreate it.

This statement supports the following variants, which have the same limitations:

  - [`  CREATE TABLE LIKE  `](#create_table_like) : Create a table with the same schema as an existing table.
  - [`  CREATE TABLE COPY  `](#create_table_copy) : Create a table by copying schema and data from an existing table.

### `     column    `

`  (column_name column_schema[, ...])  ` contains the table's schema information in a comma-separated list.

**Note:** Constraints cannot be specified on `  ARRAY  ` or `  STRUCT  ` elements.

``` text
column :=
  column_name column_schema

column_schema :=
   {
     simple_type
     | STRUCT<field_list>
     | ARRAY<array_element_schema>
   }
   [PRIMARY KEY NOT ENFORCED | REFERENCES table_name(column_name) NOT ENFORCED]
   [ DEFAULT default_expression |
     GENERATED ALWAYS AS (generation_expression) STORED OPTIONS(generation_option_list) ]
   [NOT NULL]
   [OPTIONS(column_option_list)]

simple_type :=
  { data_type | STRING COLLATE collate_specification }

field_list :=
  field_name column_schema [, ...]

array_element_schema :=
  { simple_type | STRUCT<field_list> }
  [NOT NULL]
```

  - [`  column_name  `](/bigquery/docs/schemas#column_names) is the name of the column. A column name:
    
      - Must contain only letters (a-z, A-Z), numbers (0-9), or underscores (\_)
      - Must start with a letter or underscore
      - Can be up to 300 characters

  - `  column_schema  ` : Similar to a [data type](/bigquery/docs/schemas#standard_sql_data_types) , but supports an optional `  NOT NULL  ` constraint for types other than `  ARRAY  ` . `  column_schema  ` also supports options on top-level columns and `  STRUCT  ` fields.
    
    `  column_schema  ` can be used only in the column definition list of `  CREATE TABLE  ` statements. It cannot be used as a type in expressions.

  - `  simple_type  ` : Any [supported data type](/bigquery/docs/reference/standard-sql/data-types) aside from `  STRUCT  ` and `  ARRAY  ` .
    
    If `  simple_type  ` is a `  STRING  ` , it supports an additional clause for [collation](/bigquery/docs/reference/standard-sql/collation-concepts#collate_spec_details) , which defines how a resulting `  STRING  ` can be compared and sorted. The syntax looks like this:
    
    ``` text
    STRING COLLATE collate_specification
    ```
    
    If you have `  DEFAULT COLLATE collate_specification  ` assigned to the table, the collation specification for a column overrides the specification for the table.

  - `  default_expression  ` : The [default value](/bigquery/docs/default-values) assigned to the column. You cannot specify `  DEFAULT  ` if `  GENERATED ALWAYS AS  ` is specified.

  - `  generation_expression  ` : ( [Preview](https://cloud.google.com/products#product-launch-stages) ) An expression for an automatically generated embedding column. Setting this field enables [autonomous embedding generation](/bigquery/docs/autonomous-embedding-generation) on the table. The only supported `  generation_expression  ` syntax is a call to the [`  AI.EMBED  ` function](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-embed) .
    
      - You can't specify `  GENERATED ALWAYS AS  ` if `  DEFAULT  ` is specified.
      - The `  connection_id  ` argument to `  AI.EMBED  ` is required when used in a generation expression.
      - The type of the column must be `  STRUCT<result ARRAY<FLOAT64>, status STRING>  ` .

  - `  generation_option_list  ` : The options for a generated column. The only supported option is `  asynchronous = TRUE  ` .

  - `  field_list  ` : Represents the fields in a struct.

  - `  field_name  ` : The name of the struct field. Struct field names have the same restrictions as column names.

  - `  NOT NULL  ` : When the `  NOT NULL  ` constraint is present for a column or field, the column or field is created with `  REQUIRED  ` mode. Conversely, when the `  NOT NULL  ` constraint is absent, the column or field is created with `  NULLABLE  ` mode.
    
    Columns and fields of `  ARRAY  ` type do not support the `  NOT NULL  ` modifier. For example, a `  column_schema  ` of `  ARRAY<INT64> NOT NULL  ` is invalid, since `  ARRAY  ` columns have `  REPEATED  ` mode and can be empty but cannot be `  NULL  ` . An array element in a table can never be `  NULL  ` , regardless of whether the `  NOT NULL  ` constraint is specified. For example, `  ARRAY<INT64>  ` is equivalent to `  ARRAY<INT64 NOT NULL>  ` .
    
    The `  NOT NULL  ` attribute of a table's `  column_schema  ` does not propagate through queries over the table. If table `  T  ` contains a column declared as `  x INT64 NOT NULL  ` , for example, `  CREATE TABLE dataset.newtable AS SELECT x FROM T  ` creates a table named `  dataset.newtable  ` in which `  x  ` is `  NULLABLE  ` .

### `     partition_expression    `

`  PARTITION BY  ` is an optional clause that controls [table](/bigquery/docs/partitioned-tables) and [vector index](/bigquery/docs/vector-index#partitions) partitioning. `  partition_expression  ` is an expression that determines how to partition the table or vector index. The partition expression can contain the following values:

  - `  _PARTITIONDATE  ` . Partition by ingestion time with daily partitions. This syntax cannot be used with the `  AS query_statement  ` clause.

  - `  DATE(_PARTITIONTIME)  ` . Equivalent to `  _PARTITIONDATE  ` . This syntax cannot be used with the `  AS query_statement  ` clause.

  - `  <date_column>  ` . Partition by a `  DATE  ` column with daily partitions.

  - `  DATE({ <timestamp_column> | <datetime_column> })  ` . Partition by a `  TIMESTAMP  ` or `  DATETIME  ` column with daily partitions.

  - `  DATETIME_TRUNC(<datetime_column>, { DAY | HOUR | MONTH | YEAR })  ` . Partition by a `  DATETIME  ` column with the specified partitioning type.

  - `  TIMESTAMP_TRUNC(<timestamp_column>, { DAY | HOUR | MONTH | YEAR })  ` . Partition by a `  TIMESTAMP  ` column with the specified partitioning type.

  - `  TIMESTAMP_TRUNC(_PARTITIONTIME, { DAY | HOUR | MONTH | YEAR })  ` . Partition by ingestion time with the specified partitioning type. This syntax cannot be used with the `  AS query_statement  ` clause.

  - `  DATE_TRUNC(<date_column>, { MONTH | YEAR })  ` . Partition by a `  DATE  ` column with the specified partitioning type.

  - `  RANGE_BUCKET(<int64_column>, GENERATE_ARRAY(<start>, <end>[, <interval>]))  ` . Partition by an integer column with the specified range, where:
    
      - `  start  ` is the start of range partitioning, inclusive.
      - `  end  ` is the end of range partitioning, exclusive.
      - `  interval  ` is the width of each range within the partition. Defaults to 1.

### `     clustering_column_list    `

`  CLUSTER BY  ` is an optional clause that controls [table clustering](/bigquery/docs/creating-clustered-tables) . `  clustering_column_list  ` is a comma-separated list that determines how to cluster the table. The clustering column list can contain a list of up to four clustering columns.

**Note:** You cannot have collation on a column in `  clustering_column_list  ` .

### `     table_option_list    `

The option list lets you set table options such as a [label](/bigquery/docs/labels) and an expiration time. You can include multiple options using a comma-separated list.

Specify a table option list in the following format:

`  NAME=VALUE, ...  `

`  NAME  ` and `  VALUE  ` must be one of the following combinations:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">       NAME      </code></th>
<th><code dir="ltr" translate="no">       VALUE      </code></th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       expiration_timestamp      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td><p>Example: <code dir="ltr" translate="no">        expiration_timestamp=TIMESTAMP "2025-01-01 00:00:00 UTC"       </code></p>
<p>This property is equivalent to the <a href="/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.expiration_time">expirationTime</a> table resource property.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       partition_expiration_days      </code></td>
<td><p><code dir="ltr" translate="no">        FLOAT64       </code></p></td>
<td><p>Example: <code dir="ltr" translate="no">        partition_expiration_days=7       </code></p>
<p>Sets the partition expiration in days. For more information, see <a href="/bigquery/docs/managing-partitioned-tables#partition-expiration">Set the partition expiration</a> . By default, partitions don't expire.</p>
<p>This property is equivalent to the <a href="/bigquery/docs/reference/rest/v2/tables#TimePartitioning.FIELDS.expiration_ms">timePartitioning.expirationMs</a> table resource property but uses days instead of milliseconds. One day is equivalent to 86400000 milliseconds, or 24 hours.</p>
<p>This property can only be set if the table is partitioned.</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       require_partition_filter      </code></td>
<td><p><code dir="ltr" translate="no">        BOOL       </code></p></td>
<td><p>Example: <code dir="ltr" translate="no">        require_partition_filter=true       </code></p>
<p>Specifies whether queries on this table must include a a predicate filter that filters on the partitioning column. For more information, see <a href="/bigquery/docs/managing-partitioned-tables#require-filter">Set partition filter requirements</a> . The default value is <code dir="ltr" translate="no">        false       </code> .</p>
<p>This property is equivalent to the <a href="/bigquery/docs/reference/rest/v2/tables#TimePartitioning.FIELDS.require_partition_filter">timePartitioning.requirePartitionFilter</a> table resource property.</p>
<p>This property can only be set if the table is partitioned.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       kms_key_name      </code></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>Example: <code dir="ltr" translate="no">        kms_key_name="projects/                 project_id                /locations/       </code> <code dir="ltr" translate="no">          location                /keyRings/                 keyring                /cryptoKeys/                 key                "       </code></p>
<p>This property is equivalent to the <a href="/bigquery/docs/reference/rest/v2/EncryptionConfiguration#FIELDS.kms_key_name">encryptionConfiguration.kmsKeyName</a> table resource property.</p>
<p>See more details about <a href="/bigquery/docs/customer-managed-encryption">Protecting data with Cloud KMS keys</a> .</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       friendly_name      </code></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>Example: <code dir="ltr" translate="no">        friendly_name="my_table"       </code></p>
<p>This property is equivalent to the <a href="/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.friendly_name">friendlyName</a> table resource property.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       description      </code></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>Example: <code dir="ltr" translate="no">        description="a table that expires in 2025"       </code></p>
<p>This property is equivalent to the <a href="/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.description">description</a> table resource property.</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       labels      </code></td>
<td><p><code dir="ltr" translate="no">        ARRAY&lt;STRUCT&lt;STRING, STRING&gt;&gt;       </code></p></td>
<td><p>Example: <code dir="ltr" translate="no">        labels=[("org_unit", "development")]       </code></p>
<p>This property is equivalent to the <a href="/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.labels">labels</a> table resource property.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       default_rounding_mode      </code></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>Example: <code dir="ltr" translate="no">        default_rounding_mode = "ROUND_HALF_EVEN"       </code></p>
<p>This specifies the default <a href="/bigquery/docs/schemas#rounding_mode">rounding mode</a> that's used for values written to any new <code dir="ltr" translate="no">        NUMERIC       </code> or <code dir="ltr" translate="no">        BIGNUMERIC       </code> type columns or <code dir="ltr" translate="no">        STRUCT       </code> fields in the table. It does not impact existing fields in the table. The following values are supported:</p>
<ul>
<li><code dir="ltr" translate="no">         "ROUND_HALF_AWAY_FROM_ZERO"        </code> : Halfway cases are rounded away from zero. For example, 2.5 is rounded to 3.0, and -2.5 is rounded to -3.</li>
<li><code dir="ltr" translate="no">         "ROUND_HALF_EVEN"        </code> : Halfway cases are rounded towards the nearest even digit. For example, 2.5 is rounded to 2.0 and -2.5 is rounded to -2.0.</li>
</ul>
<p>This property is equivalent to the <a href="/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.default_rounding_mode"><code dir="ltr" translate="no">         defaultRoundingMode        </code></a> table resource property.</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       enable_change_history      </code></td>
<td><p><code dir="ltr" translate="no">        BOOL       </code></p></td>
<td><p>In <a href="https://cloud.google.com/products/#product-launch-stages">preview</a> .</p>
<p>Example: <code dir="ltr" translate="no">        enable_change_history=TRUE       </code></p>
<p>Set this property to <code dir="ltr" translate="no">        TRUE       </code> in order to capture <a href="/bigquery/docs/change-history">change history</a> on the table, which you can then view by using the <a href="/bigquery/docs/reference/standard-sql/time-series-functions#changes"><code dir="ltr" translate="no">         CHANGES        </code> function</a> . Enabling this table option has an impact on costs; for more information see <a href="/bigquery/docs/change-history#pricing_and_costs">Pricing and costs</a> . The default is <code dir="ltr" translate="no">        FALSE       </code> .</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       max_staleness      </code></td>
<td><p><code dir="ltr" translate="no">        INTERVAL       </code></p></td>
<td><p>Example: <code dir="ltr" translate="no">        max_staleness=INTERVAL "4:0:0" HOUR TO SECOND       </code></p>
<p>The maximum interval behind the current time where it's acceptable to read stale data. For example, with <a href="/bigquery/docs/change-data-capture">change data capture</a> , when this option is set, the table copy operation is denied if data is more stale than the <code dir="ltr" translate="no">        max_staleness       </code> value.</p>
<p><code dir="ltr" translate="no">        max_staleness       </code> is disabled by default.</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       enable_fine_grained_mutations      </code></td>
<td><p><code dir="ltr" translate="no">        BOOL       </code></p></td>
<td><p>In <a href="https://cloud.google.com/products/#product-launch-stages">preview</a> .</p>
<p>Example: <code dir="ltr" translate="no">        enable_fine_grained_mutations=TRUE       </code></p>
<p>Set this property to <code dir="ltr" translate="no">        TRUE       </code> to enable <a href="/bigquery/docs/data-manipulation-language#fine-grained_dml">fine-grained DML optimization</a> on the table. The default is <code dir="ltr" translate="no">        FALSE       </code> .</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       storage_uri      </code></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>In <a href="https://cloud.google.com/products/#product-launch-stages">preview</a> .</p>
<p>Example: <code dir="ltr" translate="no">        storage_uri=                 gs:                //                 BUCKET_DIRECTORY                /                 TABLE_DIRECTORY                /       </code></p>
<p>A fully qualified location prefix for the external folder where data is stored. Supports <code dir="ltr" translate="no">        gs:       </code> buckets.</p>
<p>Required for <a href="/bigquery/docs/managed-tables">managed tables</a> .</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       file_format      </code></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>In <a href="https://cloud.google.com/products/#product-launch-stages">preview</a> .</p>
<p>Example: <code dir="ltr" translate="no">        file_format=PARQUET       </code></p>
<p>The open-source file format in which the table data is stored. Only <code dir="ltr" translate="no">        PARQUET       </code> is supported.</p>
<p>Required for <a href="/bigquery/docs/managed-tables">managed tables</a> .</p>
<p>The default is <code dir="ltr" translate="no">        PARQUET       </code> .</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       table_format      </code></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>In <a href="https://cloud.google.com/products/#product-launch-stages">preview</a> .</p>
<p>Example: <code dir="ltr" translate="no">        table_format=ICEBERG       </code></p>
<p>The open table format in which metadata-only snapshots are stored. Only <code dir="ltr" translate="no">        ICEBERG       </code> is supported.</p>
<p>Required for <a href="/bigquery/docs/managed-tables">managed tables</a> .</p>
<p>The default is <code dir="ltr" translate="no">        ICEBERG       </code> .</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       tags      </code></td>
<td><code dir="ltr" translate="no">       &lt;ARRAY&lt;STRUCT&lt;STRING, STRING&gt;&gt;&gt;      </code></td>
<td>An array of IAM tags for the table, expressed as key-value pairs. The key should be the <a href="/iam/docs/tags-access-control#definitions">namespaced key name</a> , and the value should be the <a href="/iam/docs/tags-access-control#definitions">short name</a> .</td>
</tr>
</tbody>
</table>

`  VALUE  ` is a constant expression containing only literals, query parameters, and scalar functions.

The constant expression **cannot** contain:

  - A reference to a table
  - Subqueries or SQL statements such as `  SELECT  ` , `  CREATE  ` , or `  UPDATE  `
  - User-defined functions, aggregate functions, or analytic functions
  - The following scalar functions:
      - `  ARRAY_TO_STRING  `
      - `  REPLACE  `
      - `  REGEXP_REPLACE  `
      - `  RAND  `
      - `  FORMAT  `
      - `  LPAD  `
      - `  RPAD  `
      - `  REPEAT  `
      - `  SESSION_USER  `
      - `  GENERATE_ARRAY  `
      - `  GENERATE_DATE_ARRAY  `

If `  VALUE  ` evaluates to `  NULL  ` , the corresponding option `  NAME  ` in the `  CREATE TABLE  ` statement is ignored.

### `     column_option_list    `

Specify a column option list in the following format:

`  NAME=VALUE, ...  `

`  NAME  ` and `  VALUE  ` must be one of the following combinations:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">       NAME      </code></th>
<th><code dir="ltr" translate="no">       VALUE      </code></th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       description      </code></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>Example: <code dir="ltr" translate="no">        description="a unique id"       </code></p>
<p>This property is equivalent to the <a href="/bigquery/docs/reference/rest/v2/tables#TableFieldSchema.FIELDS.description">schema.fields[].description</a> table resource property.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       rounding_mode      </code></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>Example: <code dir="ltr" translate="no">        rounding_mode = "ROUND_HALF_EVEN"       </code></p>
<p>This specifies the <a href="/bigquery/docs/schemas#rounding_mode">rounding mode</a> that's used for values written to a <code dir="ltr" translate="no">        NUMERIC       </code> or <code dir="ltr" translate="no">        BIGNUMERIC       </code> type column or <code dir="ltr" translate="no">        STRUCT       </code> field. The following values are supported:</p>
<ul>
<li><code dir="ltr" translate="no">         "ROUND_HALF_AWAY_FROM_ZERO"        </code> : Halfway cases are rounded away from zero. For example, 2.25 is rounded to 2.3, and -2.25 is rounded to -2.3.</li>
<li><code dir="ltr" translate="no">         "ROUND_HALF_EVEN"        </code> : Halfway cases are rounded towards the nearest even digit. For example, 2.25 is rounded to 2.2 and -2.25 is rounded to -2.2.</li>
</ul>
<p>This property is equivalent to the <a href="/bigquery/docs/reference/rest/v2/tables#TableFieldSchema.FIELDS.rounding_mode"><code dir="ltr" translate="no">         roundingMode        </code></a> table resource property.</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       data_policies      </code></td>
<td><code dir="ltr" translate="no">       ARRAY&lt;STRING&gt;      </code></td>
<td><p>Applies a <a href="/bigquery/docs/column-data-masking#create_data_policies">data policy</a> to a column in a table.</p>
<p>Example: <code dir="ltr" translate="no">        data_policies = ["{'name':'myproject.region-us.data_policy_name1'}",                                           "{'name':'myproject.region-us.data_policy_name2'}"]       </code></p>
<p>The <a href="/bigquery/docs/reference/standard-sql/data-definition-language#alter_column_set_data_type_statement"><code dir="ltr" translate="no">         ALTER TABLE ALTER COLUMN        </code></a> statement supports the <code dir="ltr" translate="no">        =       </code> and <code dir="ltr" translate="no">        +=       </code> operators to add data policies to a specific column.</p>
<p>Example: <code dir="ltr" translate="no">        data_policies +=["data_policy1", "data_policy2"]       </code></p></td>
</tr>
</tbody>
</table>

`  VALUE  ` is a constant expression containing only literals, query parameters, and scalar functions.

The constant expression **cannot** contain:

  - A reference to a table
  - Subqueries or SQL statements such as `  SELECT  ` , `  CREATE  ` , or `  UPDATE  `
  - User-defined functions, aggregate functions, or analytic functions
  - The following scalar functions:
      - `  ARRAY_TO_STRING  `
      - `  REPLACE  `
      - `  REGEXP_REPLACE  `
      - `  RAND  `
      - `  FORMAT  `
      - `  LPAD  `
      - `  RPAD  `
      - `  REPEAT  `
      - `  SESSION_USER  `
      - `  GENERATE_ARRAY  `
      - `  GENERATE_DATE_ARRAY  `

Setting the `  VALUE  ` replaces the existing value of that option for the column, if there was one. Setting the `  VALUE  ` to `  NULL  ` clears the column's value for that option.

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.tables.create      </code></td>
<td>The dataset where you create the table.</td>
</tr>
</tbody>
</table>

In addition, the `  OR REPLACE  ` clause requires `  bigquery.tables.update  ` and `  bigquery.tables.updateData  ` permissions.

If the `  OPTIONS  ` clause includes any expiration options, then the `  bigquery.tables.delete  ` permission is also required.

### Examples

#### Creating a new table

The following example creates a partitioned table named `  newtable  ` in `  mydataset  ` :

``` text
CREATE TABLE mydataset.newtable
(
  x INT64 OPTIONS(description="An optional INTEGER field"),
  y STRUCT <
    a ARRAY <STRING> OPTIONS(description="A repeated STRING field"),
    b BOOL
  >
)
PARTITION BY _PARTITIONDATE
OPTIONS(
  expiration_timestamp=TIMESTAMP "2025-01-01 00:00:00 UTC",
  partition_expiration_days=1,
  description="a table that expires in 2025, with each partition living for 24 hours",
  labels=[("org_unit", "development")]
)
```

If you haven't configured a default project, prepend a project ID to the dataset name in the example SQL, and enclose the name in backticks if `  project_id  ` contains special characters: ``  ` project_id.dataset.table `  `` . So, instead of `  mydataset.newtable  ` , your table qualifier might be ``  `myproject.mydataset.newtable`  `` .

If the table name exists in the dataset, the following error is returned:

`  Already Exists: project_id:dataset.table  `

The table uses the following `  partition_expression  ` to partition the table: `  PARTITION BY _PARTITIONDATE  ` . This expression partitions the table using the date in the `  _PARTITIONDATE  ` pseudocolumn.

The table schema contains two columns:

  - **x:** An integer, with description "An optional INTEGER field"

  - **y:** A STRUCT containing two columns:
    
      - **a:** An array of strings, with description "A repeated STRING field"
      - **b:** A boolean
    
    **Note:** When you examine the table schema in the Google Cloud console, a STRUCT is displayed as a RECORD column, and an ARRAY is displayed as a REPEATED column. The STRUCT and ARRAY data types are used to create nested and repeated data in BigQuery. For more information, see [Specifying nested and repeated fields](/bigquery/docs/nested-repeated) .

The table option list specifies the:

  - **Table expiration time:** January 1, 2025 at 00:00:00 UTC
  - **Partition expiration time:** 1 day
  - **Description:** `  A table that expires in 2025  `
  - **Label:** `  org_unit = development  `

#### Creating a new table from an existing table

The following example creates a table named `  top_words  ` in `  mydataset  ` from a query:

``` text
CREATE TABLE mydataset.top_words
OPTIONS(
  description="Top ten words per Shakespeare corpus"
) AS
SELECT
  corpus,
  ARRAY_AGG(STRUCT(word, word_count) ORDER BY word_count DESC LIMIT 10) AS top_words
FROM `bigquery-public-data`.samples.shakespeare
GROUP BY corpus;
```

If you haven't configured a default project, prepend a project ID to the dataset name in the example SQL, and enclose the name in backticks if `  project_id  ` contains special characters: ``  ` project_id.dataset.table `  `` . So, instead of `  mydataset.top_words  ` , your table qualifier might be ``  `myproject.mydataset.top_words`  `` .

If the table name exists in the dataset, the following error is returned:

`  Already Exists: project_id:dataset.table  `

The table schema contains 2 columns:

  - **corpus:** Name of a Shakespeare corpus

  - **top\_words:** An `  ARRAY  ` of `  STRUCT  ` s containing 2 fields: `  word  ` (a `  STRING  ` ) and `  word_count  ` (an `  INT64  ` with the word count)
    
    **Note:** When you examine the table schema in the Google Cloud console, a STRUCT is displayed as a RECORD column, and an ARRAY is displayed as a REPEATED column. The STRUCT and ARRAY data types are used to create nested and repeated data in BigQuery. For more information, see [Specifying nested and repeated fields](/bigquery/docs/nested-repeated) .

The table option list specifies the:

  - **Description:** `  Top ten words per Shakespeare corpus  `

#### Creating a table only if the table doesn't exist

The following example creates a table named `  newtable  ` in `  mydataset  ` only if no table named `  newtable  ` exists in `  mydataset  ` . If the table name exists in the dataset, no error is returned, and no action is taken.

``` text
CREATE TABLE IF NOT EXISTS mydataset.newtable (x INT64, y STRUCT <a ARRAY <STRING>, b BOOL>)
OPTIONS(
  expiration_timestamp=TIMESTAMP "2025-01-01 00:00:00 UTC",
  description="a table that expires in 2025",
  labels=[("org_unit", "development")]
)
```

If you haven't configured a default project, prepend a project ID to the dataset name in the example SQL, and enclose the name in backticks if `  project_id  ` contains special characters: ``  ` project_id.dataset.table `  `` . So, instead of `  mydataset.newtable  ` , your table qualifier might be ``  `myproject.mydataset.newtable`  `` .

The table schema contains 2 columns:

  - **x:** An integer

  - **y:** A STRUCT containing a (an array of strings) and b (a boolean)
    
    **Note:** When you examine the table schema in the Google Cloud console, a STRUCT is displayed as a RECORD, and an ARRAY is displayed as REPEATED. The STRUCT and ARRAY data types are used to create nested and repeated data in BigQuery. For more information, see [Specifying nested and repeated fields](/bigquery/docs/nested-repeated) .

The table option list specifies the:

  - **Expiration time:** January 1, 2025 at 00:00:00 UTC
  - **Description:** `  A table that expires in 2025  `
  - **Label:** `  org_unit = development  `

#### Creating or replacing a table

The following example creates a table named `  newtable  ` in `  mydataset  ` , and if `  newtable  ` exists in `  mydataset  ` , it is overwritten with an empty table.

``` text
CREATE OR REPLACE TABLE mydataset.newtable (x INT64, y STRUCT <a ARRAY <STRING>, b BOOL>)
OPTIONS(
  expiration_timestamp=TIMESTAMP "2025-01-01 00:00:00 UTC",
  description="a table that expires in 2025",
  labels=[("org_unit", "development")]
)
```

If you haven't configured a default project, prepend a project ID to the dataset name in the example SQL, and enclose the name in backticks if `  project_id  ` contains special characters: ``  ` project_id.dataset.table `  `` . So, instead of `  mydataset.newtable  ` , your table qualifier might be ``  `myproject.mydataset.newtable`  `` .

The table schema contains 2 columns:

  - **x:** An integer

  - **y:** A STRUCT containing a (an array of strings) and b (a boolean)
    
    **Note:** When you examine the table schema in the Google Cloud console, a STRUCT is displayed as a RECORD, and an ARRAY is displayed as REPEATED. The STRUCT and ARRAY data types are used to create nested and repeated data in BigQuery. For more information, see [Specifying nested and repeated fields](/bigquery/docs/nested-repeated) .

The table option list specifies the:

  - **Expiration time:** January 1, 2025 at 00:00:00 UTC
  - **Description:** `  A table that expires in 2025  `
  - **Label:** `  org_unit = development  `

#### Creating a table with `     REQUIRED    ` columns

The following example creates a table named `  newtable  ` in `  mydataset  ` . The `  NOT NULL  ` modifier in the column definition list of a `  CREATE TABLE  ` statement specifies that a column or field is created in `  REQUIRED  ` mode.

``` text
CREATE TABLE mydataset.newtable (
  x INT64 NOT NULL,
  y STRUCT <
    a ARRAY <STRING>,
    b BOOL NOT NULL,
    c FLOAT64
  > NOT NULL,
  z STRING
)
```

If you haven't configured a default project, prepend a project ID to the dataset name in the example SQL, and enclose the name in backticks if `  project_id  ` contains special characters: ``  ` project_id.dataset.table `  `` . So, instead of `  mydataset.newtable  ` , your table qualifier might be ``  `myproject.mydataset.newtable`  `` .

If the table name exists in the dataset, the following error is returned:

`  Already Exists: project_id:dataset.table  `

The table schema contains 3 columns:

  - **x:** A `  REQUIRED  ` integer

  - **y:** A `  REQUIRED  ` STRUCT containing a (an array of strings), b (a `  REQUIRED  ` boolean), and c (a `  NULLABLE  ` float)

  - **z:** A `  NULLABLE  ` string
    
    **Note:** When you examine the table schema in the Google Cloud console, a STRUCT is displayed as a RECORD, and an ARRAY is displayed as REPEATED. The STRUCT and ARRAY data types are used to create nested and repeated data in BigQuery. For more information, see [Specifying nested and repeated fields](/bigquery/docs/nested-repeated) .

#### Creating a table with collation support

The following examples create a table named `  newtable  ` in `  mydataset  ` with columns `  a  ` , `  b  ` , `  c  ` , and a struct with fields `  x  ` and `  y  ` .

All `  STRING  ` column schemas in this table are collated with `  'und:ci'  ` :

``` text
CREATE TABLE mydataset.newtable (
  a STRING,
  b STRING,
  c STRUCT <
    x FLOAT64
    y ARRAY <STRING>
  >
)
DEFAULT COLLATE 'und:ci';
```

Only `  b  ` and `  y  ` are collated with `  'und:ci'  ` :

``` text
CREATE TABLE mydataset.newtable (
  a STRING,
  b STRING COLLATE 'und:ci',
  c STRUCT <
    x FLOAT64
    y ARRAY <STRING COLLATE 'und:ci'>
  >
);
```

#### Creating a table with parameterized data types

The following example creates a table named `  newtable  ` in `  mydataset  ` . The parameters in parentheses specify that the column contains a parameterized data type. See [Parameterized Data Types](/bigquery/docs/reference/standard-sql/data-types#parameterized_data_types) for more information about parameterized types.

``` text
CREATE TABLE mydataset.newtable (
  x STRING(10),
  y STRUCT <
    a ARRAY <BYTES(5)>,
    b NUMERIC(15, 2) OPTIONS(rounding_mode = 'ROUND_HALF_EVEN'),
    c FLOAT64
  >,
  z BIGNUMERIC(35)
)
```

If you haven't configured a default project, prepend a project ID to the dataset name in the example SQL, and enclose the name in backticks if `  project_id  ` contains special characters: ``  ` project_id.dataset.table `  `` . Instead of `  mydataset.newtable  ` , your table qualifier should be ``  `myproject.mydataset.newtable`  `` .

If the table name exists in the dataset, the following error is returned:

`  Already Exists: project_id:dataset.table  `

The table schema contains 3 columns:

  - **x:** A parameterized string with a maximum length of 10
  - **y:** A STRUCT containing a (an array of parameterized bytes with a maximum length of 5), b (a parameterized NUMERIC with a maximum precision of 15, maximum scale of 2, and rounding mode set to 'ROUND\_HALF\_EVEN'), and c (a float)
  - **z:** A parameterized BIGNUMERIC with a maximum precision of 35 and maximum scale of 0

#### Creating a partitioned table

The following example creates a [partitioned table](/bigquery/docs/partitioned-tables#date_timestamp_partitioned_tables) named `  newtable  ` in `  mydataset  ` using a `  DATE  ` column:

``` text
CREATE TABLE mydataset.newtable (transaction_id INT64, transaction_date DATE)
PARTITION BY transaction_date
OPTIONS(
  partition_expiration_days=3,
  description="a table partitioned by transaction_date"
)
```

If you haven't configured a default project, prepend a project ID to the dataset name in the example SQL, and enclose the name in backticks if `  project_id  ` contains special characters: ``  ` project_id.dataset.table `  `` . So, instead of `  mydataset.newtable  ` , your table qualifier might be ``  `myproject.mydataset.newtable`  `` .

The table schema contains 2 columns:

  - **transaction\_id:** An integer
  - **transaction\_date:** A date

The table option list specifies the:

  - **Partition expiration:** Three days
  - **Description:** `  A table partitioned by transaction_date  `

#### Creating a partitioned table from the result of a query

The following example creates a [partitioned table](/bigquery/docs/partitioned-tables#date_timestamp_partitioned_tables) named `  days_with_rain  ` in `  mydataset  ` using a `  DATE  ` column:

``` text
CREATE TABLE mydataset.days_with_rain
PARTITION BY date
OPTIONS (
  partition_expiration_days=365,
  description="weather stations with precipitation, partitioned by day"
) AS
SELECT
  DATE(CAST(year AS INT64), CAST(mo AS INT64), CAST(da AS INT64)) AS date,
  (SELECT ANY_VALUE(name) FROM `bigquery-public-data.noaa_gsod.stations` AS stations
   WHERE stations.usaf = stn) AS station_name,  -- Stations can have multiple names
  prcp
FROM `bigquery-public-data.noaa_gsod.gsod2017` AS weather
WHERE prcp != 99.9  -- Filter unknown values
  AND prcp > 0      -- Filter stations/days with no precipitation
```

If you haven't configured a default project, prepend a project ID to the dataset name in the example SQL, and enclose the name in backticks if `  project_id  ` contains special characters: ``  ` project_id.dataset.table `  `` . So, instead of `  mydataset.days_with_rain  ` , your table qualifier might be ``  `myproject.mydataset.days_with_rain`  `` .

The table schema contains 2 columns:

  - **date:** The `  DATE  ` of data collection
  - **station\_name:** The name of the weather station as a `  STRING  `
  - **prcp:** The amount of precipitation in inches as a `  FLOAT64  `

The table option list specifies the:

  - **Partition expiration:** One year
  - **Description:** `  Weather stations with precipitation, partitioned by day  `

#### Creating a clustered table

##### Example 1

The following example creates a [clustered table](/bigquery/docs/clustered-tables) named `  myclusteredtable  ` in `  mydataset  ` . The table is a [partitioned table](/bigquery/docs/partitioned-tables) , partitioned by a truncated `  TIMESTAMP  ` column and clustered by a `  STRING  ` column named `  customer_id  ` .

``` text
CREATE TABLE mydataset.myclusteredtable
(
  input_timestamp TIMESTAMP,
  customer_id STRING,
  transaction_amount NUMERIC
)
PARTITION BY TIMESTAMP_TRUNC(input_timestamp, HOUR)
CLUSTER BY customer_id
OPTIONS (
  partition_expiration_days=3,
  description="a table clustered by customer_id"
)
```

If you haven't configured a default project, prepend a project ID to the dataset name in the example SQL, and enclose the name in backticks if `  project_id  ` contains special characters: ``  ` project_id.dataset.table `  `` . So, instead of `  mydataset.myclusteredtable  ` , your table qualifier might be ``  `myproject.mydataset.myclusteredtable`  `` .

The table schema contains 3 columns:

  - **input\_timestamp:** The time of data collection as a `  TIMESTAMP  `
  - **customer\_id:** The customer ID as a `  STRING  `
  - **transaction\_amount:** The transaction amount as `  NUMERIC  `

The table option list specifies the:

  - **Partition expiration:** 3 days
  - **Description:** `  A table clustered by customer_id  `

##### Example 2

The following example creates a [clustered table](/bigquery/docs/clustered-tables) named `  myclusteredtable  ` in `  mydataset  ` . The table is an [ingestion-time partitioned table](/bigquery/docs/creating-partitioned-tables) .

``` text
CREATE TABLE mydataset.myclusteredtable
(
  customer_id STRING,
  transaction_amount NUMERIC
)
PARTITION BY DATE(_PARTITIONTIME)
CLUSTER BY
  customer_id
OPTIONS (
  partition_expiration_days=3,
  description="a table clustered by customer_id"
)
```

If you haven't configured a default project, prepend a project ID to the dataset name in the example SQL, and enclose the name in backticks if `  project_id  ` contains special characters: ``  ` project_id.dataset.table `  `` . So, instead of `  mydataset.myclusteredtable  ` , your table qualifier might be ``  `myproject.mydataset.myclusteredtable`  `` .

The table schema contains 2 columns:

  - **customer\_id:** The customer ID as a `  STRING  `
  - **transaction\_amount:** The transaction amount as `  NUMERIC  `

The table option list specifies the:

  - **Partition expiration:** 3 days
  - **Description:** `  A table clustered by customer_id  `

##### Example 3

The following example creates a [clustered table](/bigquery/docs/clustered-tables) named `  myclusteredtable  ` in `  mydataset  ` . The table is not partitioned.

``` text
CREATE TABLE mydataset.myclusteredtable
(
  customer_id STRING,
  transaction_amount NUMERIC
)
CLUSTER BY
  customer_id
OPTIONS (
  description="a table clustered by customer_id"
)
```

If you haven't configured a default project, prepend a project ID to the dataset name in the example SQL, and enclose the name in backticks if `  project_id  ` contains special characters: ``  ` project_id.dataset.table `  `` . So, instead of `  mydataset.myclusteredtable  ` , your table qualifier might be ``  `myproject.mydataset.myclusteredtable`  `` .

The table schema contains 2 columns:

  - **customer\_id:** The customer ID as a `  STRING  `
  - **transaction\_amount:** The transaction amount as `  NUMERIC  `

The table option list specifies the:

  - **Description:** `  A table clustered by customer_id  `

#### Creating a table with autonomous embedding generation

**Preview**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

The following example creates a table named `  embedded_table  ` in `  mydataset  ` with an [autonomous embedding generation](/bigquery/docs/autonomous-embedding-generation) column `  embedding  ` that generates embeddings from `  content  ` column:

``` text
CREATE TABLE mydataset.embedded_table (
  id INT64,
  content STRING,
  embedding STRUCT, status STRING>
    GENERATED ALWAYS AS (
      AI.EMBED(
        content,
        connection_id => "US.embed_connection",
        endpoint => "text-embedding-005")
    )
    STORED OPTIONS (asynchronous = true)
);
```

#### Creating a clustered table from the result of a query

##### Example 1

The following example creates a partitioned and [clustered table](/bigquery/docs/clustered-tables) named `  myclusteredtable  ` in `  mydataset  ` using the result of a query.

``` text
CREATE TABLE mydataset.myclusteredtable
(
  input_timestamp TIMESTAMP,
  customer_id STRING,
  transaction_amount NUMERIC
)
PARTITION BY DATE(input_timestamp)
CLUSTER BY
  customer_id
OPTIONS (
  partition_expiration_days=3,
  description="a table clustered by customer_id"
)
AS SELECT * FROM mydataset.myothertable
```

If you haven't configured a default project, prepend a project ID to the dataset name in the example SQL, and enclose the name in backticks if `  project_id  ` contains special characters: ``  ` project_id.dataset.table `  `` . So, instead of `  mydataset.myclusteredtable  ` , your table qualifier might be ``  `myproject.mydataset.myclusteredtable`  `` .

The table schema contains 3 columns:

  - **input\_timestamp:** The time of data collection as a `  TIMESTAMP  `
  - **customer\_id:** The customer ID as a `  STRING  `
  - **transaction\_amount:** The transaction amount as `  NUMERIC  `

The table option list specifies the:

  - **Partition expiration:** 3 days
  - **Description:** `  A table clustered by customer_id  `

##### Example 2

The following example creates a [clustered table](/bigquery/docs/clustered-tables) named `  myclusteredtable  ` in `  mydataset  ` using the result of a query. The table is not partitioned.

``` text
CREATE TABLE mydataset.myclusteredtable
(
  customer_id STRING,
  transaction_amount NUMERIC
)
CLUSTER BY
  customer_id
OPTIONS (
  description="a table clustered by customer_id"
)
AS SELECT * FROM mydataset.myothertable
```

If you haven't configured a default project, prepend a project ID to the dataset name in the example SQL, and enclose the name in backticks if `  project_id  ` contains special characters: ``  ` project_id.dataset.table `  `` . So, instead of `  mydataset.myclusteredtable  ` , your table qualifier might be ``  `myproject.mydataset.myclusteredtable`  `` .

The table schema contains 2 columns:

  - **customer\_id:** The customer ID as a `  STRING  `
  - **transaction\_amount:** The transaction amount as `  NUMERIC  `

The table option list specifies the:

  - **Description:** `  A table clustered by customer_id  `

#### Creating a temporary table

The following example creates a temporary table named `  Example  ` and inserts values into it.

``` text
CREATE TEMP TABLE Example
(
  x INT64,
  y STRING
);

INSERT INTO Example
VALUES (5, 'foo');

INSERT INTO Example
VALUES (6, 'bar');

SELECT *
FROM Example;
```

This script returns the following output:

``` text
+-----+---+-----+
| Row | x | y   |
+-----+---|-----+
| 1   | 5 | foo |
| 2   | 6 | bar |
+-----+---|-----+
```

#### Load data across clouds

#### Example 1

Suppose you have a BigLake table named `  myawsdataset.orders  ` that references data from [Amazon S3](/bigquery/docs/omni-aws-create-external-table) . You want to transfer data from that table to a BigQuery table `  myotherdataset.shipments  ` in the US multi-region.

First, display information about the `  myawsdataset.orders  ` table:

``` text
    bq show myawsdataset.orders;
```

The output is similar to the following:

``` text
  Last modified             Schema              Type     Total URIs   Expiration
----------------- -------------------------- ---------- ------------ -----------
  31 Oct 17:40:28   |- l_orderkey: integer     EXTERNAL   1
                    |- l_partkey: integer
                    |- l_suppkey: integer
                    |- l_linenumber: integer
                    |- l_returnflag: string
                    |- l_linestatus: string
                    |- l_commitdate: date
```

Next, display information about the `  myotherdataset.shipments  ` table:

``` text
  bq show myotherdataset.shipments
```

The output is similar to the following. Some columns are omitted to simplify the output.

``` text
  Last modified             Schema             Total Rows   Total Bytes   Expiration   Time Partitioning   Clustered Fields   Total Logical
 ----------------- --------------------------- ------------ ------------- ------------ ------------------- ------------------ ---------------
  31 Oct 17:34:31   |- l_orderkey: integer      3086653      210767042                                                         210767042
                    |- l_partkey: integer
                    |- l_suppkey: integer
                    |- l_commitdate: date
                    |- l_shipdate: date
                    |- l_receiptdate: date
                    |- l_shipinstruct: string
                    |- l_shipmode: string
```

Now, using the `  CREATE TABLE AS SELECT  ` statement you can selectively load data to the `  myotherdataset.orders  ` table in the US multi-region:

``` text
CREATE OR REPLACE TABLE
  myotherdataset.orders
  PARTITION BY DATE_TRUNC(l_commitdate, YEAR) AS
SELECT
  *
FROM
  myawsdataset.orders
WHERE
  EXTRACT(YEAR FROM l_commitdate) = 1992;
```

**Note:** If you get a `  ResourceExhausted  ` error, retry after sometime. If the issue persists, you can [contact support](/bigquery/docs/getting-support) .

You can then perform a join operation with the newly created table:

``` text
SELECT
  orders.l_orderkey,
  orders.l_orderkey,
  orders.l_suppkey,
  orders.l_commitdate,
  orders.l_returnflag,
  shipments.l_shipmode,
  shipments.l_shipinstruct
FROM
  myotherdataset.shipments
JOIN
  `myotherdataset.orders` as orders
ON
  orders.l_orderkey = shipments.l_orderkey
AND orders.l_partkey = shipments.l_partkey
AND orders.l_suppkey = shipments.l_suppkey
WHERE orders.l_returnflag = 'R'; -- 'R' means refunded.
```

When new data is available, append the data of the 1993 year to the destination table using the `  INSERT INTO SELECT  ` statement:

``` text
INSERT INTO
   myotherdataset.orders
 SELECT
   *
 FROM
   myawsdataset.orders
 WHERE
   EXTRACT(YEAR FROM l_commitdate) = 1993;
```

#### Example 2

The following example inserts data into an ingestion-time partitioned table:

``` text
CREATE TABLE
 mydataset.orders(id String, numeric_id INT64)
PARTITION BY _PARTITIONDATE;
```

After creating a partitioned table, you can insert data into the ingestion-time partitioned table:

``` text
INSERT INTO
 mydataset.orders(
   _PARTITIONTIME,
   id,
   numeric_id)
SELECT
 TIMESTAMP("2023-01-01"),
 id,
 numeric_id,
FROM
 mydataset.ordersof23
WHERE
 numeric_id > 4000000;
```

## `     CREATE TABLE LIKE    ` statement

Creates a new table with all of the same metadata of another table.

### Syntax

``` text
CREATE [ OR REPLACE ] TABLE [ IF NOT EXISTS ]
table_name
LIKE [[project_name.]dataset_name.]source_table_name
...
[OPTIONS(table_option_list)]
```

### Details

This statement is a variant of the `  CREATE TABLE  ` statement and has the same [limitations](#create_table_details) . Other than the use of the `  LIKE  ` clause in place of a column list, the syntax is identical to the `  CREATE TABLE  ` syntax.

The `  CREATE TABLE LIKE  ` statement copies only the metadata of the source table. You can use the `  AS query_statement  ` clause to include data into the new table.

The new table has no relationship to the source table after creation; thus modifications to the source table will not propagate to the new table.

By default, the new table inherits partitioning, clustering, and options metadata from the source table. You can customize metadata in the new table by using the optional clauses in the SQL statement. For example, if you want to specify a different set of options for the new table, then include the `  OPTIONS  ` clause with a list of options and values. This behavior matches that of `  ALTER TABLE SET OPTIONS  ` .

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.tables.create      </code></td>
<td>The dataset where you create the table.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigquery.tables.get      </code></td>
<td>The source table.</td>
</tr>
</tbody>
</table>

In addition, the `  OR REPLACE  ` clause requires `  bigquery.tables.update  ` and `  bigquery.tables.updateData  ` permissions.

If the `  OPTIONS  ` clause includes any expiration options, then the `  bigquery.tables.delete  ` permission is also required.

### Examples

#### Example 1

The following example creates a new table named `  newtable  ` in `  mydataset  ` with the same metadata as `  sourcetable  ` :

``` text
CREATE TABLE mydataset.newtable
LIKE mydataset.sourcetable
```

#### Example 2

The following example creates a new table named `  newtable  ` in `  mydataset  ` with the same metadata as `  sourcetable  ` and the data from the `  SELECT  ` statement:

``` text
CREATE TABLE mydataset.newtable
LIKE mydataset.sourcetable
AS SELECT * FROM mydataset.myothertable
```

## `     CREATE TABLE COPY    ` statement

Creates a table that has the same metadata and data as another table. The source table can be a table, a [table clone](/bigquery/docs/table-clones-intro) , or a [table snapshot](/bigquery/docs/table-snapshots-intro) .

### Syntax

``` text
CREATE [ OR REPLACE ] TABLE [ IF NOT EXISTS ] table_name
COPY source_table_name
...
[OPTIONS(table_option_list)]
```

### Details

This statement is a variant of the `  CREATE TABLE  ` statement and has the same [limitations](#create_table_details) . Other than the use of the `  COPY  ` clause in place of a column list, the syntax is identical to the `  CREATE TABLE  ` syntax.

The `  CREATE TABLE COPY  ` statement copies both the metadata and data from the source table.

The new table inherits partitioning and clustering from the source table. By default, the table options metadata from the source table are also inherited, but you can override table options by using the `  OPTIONS  ` clause. The behavior is equivalent to running `  ALTER TABLE SET OPTIONS  ` after the table is copied.

The new table has no relationship to the source table after creation; modifications to the source table are not propagated to the new table.

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.tables.create      </code></td>
<td>The dataset where you create the table copy.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigquery.tables.get      </code></td>
<td>The source table.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.tables.getData      </code></td>
<td>The source table.</td>
</tr>
</tbody>
</table>

In addition, the `  OR REPLACE  ` clause requires `  bigquery.tables.update  ` and `  bigquery.tables.updateData  ` permissions.

If the `  OPTIONS  ` clause includes any expiration options, then the `  bigquery.tables.delete  ` permission is also required.

## `     CREATE SNAPSHOT TABLE    ` statement

Creates a [table snapshot](/bigquery/docs/table-snapshots-intro) based on a source table. The source table can be a table, a [table clone](/bigquery/docs/table-clones-intro) , or a table snapshot.

### Syntax

``` text
CREATE SNAPSHOT TABLE [ IF NOT EXISTS ] table_snapshot_name
CLONE source_table_name
[FOR SYSTEM_TIME AS OF time_expression]
[OPTIONS(snapshot_option_list)]
```

### Arguments

  - `  IF NOT EXISTS  ` : If a table snapshot or other [table resource](/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.type) exists with the same name, the `  CREATE  ` statement has no effect.

  - `  table_snapshot_name  ` : The name of the table snapshot that you want to create. The table snapshot name must be unique per dataset. See [Table path syntax](#table_path) .

  - `  source_table_name  ` : The name of the table that you want to snapshot or the table snapshot that you want to copy. See [Table path syntax](#table_path) .
    
    If the source table is a standard table, then BigQuery creates a table snapshot of the source table. If the source table is a table snapshot, then BigQuery creates a copy of the table snapshot.

  - [`  FOR SYSTEM_TIME AS OF  `](/bigquery/docs/reference/standard-sql/query-syntax#for_system_time_as_of) : Lets you select the version of the table that was current at the time specified by `  timestamp_expression  ` . It can only be used when creating a snapshot of a table; it can't be used when making a copy of a table snapshot.

  - [`  snapshot_option_list  `](#snapshot_option_list) : Additional table snapshot creation options such as a [label](/bigquery/docs/labels) and an expiration time.

### Details

`  CREATE SNAPSHOT TABLE  ` statements must comply with the following rules:

  - Only one `  CREATE  ` statement is allowed.
  - The source table must be one of the following:
      - A table
      - A table clone
      - A table snapshot
  - The `  FOR SYSTEM_TIME AS OF  ` clause can only be used when creating a snapshot of a table or table clone; it can't be used when making a copy of a table snapshot.

### `     snapshot_option_list    `

The option list lets you set table snapshot options such as a [label](/bigquery/docs/labels) and an expiration time. You can include multiple options using a comma-separated list.

Specify a table snapshot option list in the following format:

`  NAME=VALUE, ...  `

`  NAME  ` and `  VALUE  ` must be one of the following combinations:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">       NAME      </code></th>
<th><code dir="ltr" translate="no">       VALUE      </code></th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       expiration_timestamp      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td><p>Example: <code dir="ltr" translate="no">        expiration_timestamp=TIMESTAMP "2025-01-01 00:00:00 UTC"       </code></p>
<p>This property is equivalent to the <a href="/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.expiration_time"><code dir="ltr" translate="no">         expirationTime        </code></a> table resource property.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       friendly_name      </code></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>Example: <code dir="ltr" translate="no">        friendly_name="my_table_snapshot"       </code></p>
<p>This property is equivalent to the <a href="/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.friendly_name"><code dir="ltr" translate="no">         friendlyName        </code></a> table resource property.</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       description      </code></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>Example: <code dir="ltr" translate="no">        description="A table snapshot that expires in 2025"       </code></p>
<p>This property is equivalent to the <a href="/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.description"><code dir="ltr" translate="no">         description        </code></a> table resource property.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       labels      </code></td>
<td><p><code dir="ltr" translate="no">        ARRAY&lt;STRUCT&lt;STRING, STRING&gt;&gt;       </code></p></td>
<td><p>Example: <code dir="ltr" translate="no">        labels=[("org_unit", "development")]       </code></p>
<p>This property is equivalent to the <a href="/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.labels"><code dir="ltr" translate="no">         labels        </code></a> table resource property.</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       tags      </code></td>
<td><code dir="ltr" translate="no">       &lt;ARRAY&lt;STRUCT&lt;STRING, STRING&gt;&gt;&gt;      </code></td>
<td>An array of IAM tags expressed as key-value pairs. The key should be the <a href="/iam/docs/tags-access-control#definitions">namespaced key name</a> , and the value should be the <a href="/iam/docs/tags-access-control#definitions">short name</a> .</td>
</tr>
</tbody>
</table>

`  VALUE  ` is a constant expression that contains only literals, query parameters, and scalar functions.

The constant expression cannot contain:

  - A reference to a table
  - Subqueries or SQL statements such as `  SELECT  ` , `  CREATE  ` , and `  UPDATE  `
  - User-defined functions, aggregate functions, or analytic functions
  - The following scalar functions:
      - `  ARRAY_TO_STRING  `
      - `  REPLACE  `
      - `  REGEXP_REPLACE  `
      - `  RAND  `
      - `  FORMAT  `
      - `  LPAD  `
      - `  RPAD  `
      - `  REPEAT  `
      - `  SESSION_USER  `
      - `  GENERATE_ARRAY  `
      - `  GENERATE_DATE_ARRAY  `

If `  VALUE  ` evaluates to `  NULL  ` , the corresponding option `  NAME  ` in the `  CREATE SNAPSHOT TABLE  ` statement is ignored.

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.tables.create      </code></td>
<td>The dataset where you create the table snapshot.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigquery.tables.createSnapshot      </code></td>
<td>The source table.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.tables.get      </code></td>
<td>The source table.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigquery.tables.getData      </code></td>
<td>The source table.</td>
</tr>
</tbody>
</table>

### Examples

#### Create a table snapshot: fail if it already exists

The following example creates a table snapshot of the table `  myproject.mydataset.mytable  ` . The table snapshot is created in the dataset `  mydataset  ` and is named `  mytablesnapshot  ` :

``` text
CREATE SNAPSHOT TABLE `myproject.mydataset.mytablesnapshot`
CLONE `myproject.mydataset.mytable`
OPTIONS(
  expiration_timestamp=TIMESTAMP_ADD(CURRENT_TIMESTAMP(), INTERVAL 48 HOUR),
  friendly_name="my_table_snapshot",
  description="A table snapshot that expires in 2 days",
  labels=[("org_unit", "development")]
)
```

If the table snapshot name already exists in the dataset, then the following error is returned:

`  Already Exists: myproject.mydataset.mytablesnapshot  `

The table snapshot option list specifies the following:

  - **Expiration time:** 48 hours after the time the table snapshot is created
  - **Friendly name:** `  my_table_snapshot  `
  - **Description:** `  A table snapshot that expires in 2 days  `
  - **Label:** `  org_unit = development  `

#### Create a table snapshot: ignore if it already exists

The following example creates a table snapshot of the table `  myproject.mydataset.mytable  ` . The table snapshot is created in the dataset `  mydataset  ` and is named `  mytablesnapshot  ` :

``` text
CREATE SNAPSHOT TABLE IF NOT EXISTS `myproject.mydataset.mytablesnapshot`
CLONE `myproject.mydataset.mytable`
OPTIONS(
  expiration_timestamp=TIMESTAMP_ADD(CURRENT_TIMESTAMP(), INTERVAL 48 HOUR),
  friendly_name="my_table_snapshot",
  description="A table snapshot that expires in 2 days"
  labels=[("org_unit", "development")]
)
```

The table snapshot option list specifies the following:

  - **Expiration time:** 48 hours after the time the table snapshot is created
  - **Friendly name:** `  my_table_snapshot  `
  - **Description:** `  A table snapshot that expires in 2 days  `
  - **Label:** `  org_unit = development  `

If the table snapshot name already exists in the dataset, then no action is taken, and no error is returned.

For information about restoring table snapshots, see [`  CREATE TABLE CLONE  `](#create_table_clone_statement) .

For information about removing table snapshots, see [`  DROP SNAPSHOT TABLE  `](#drop_snapshot_table_statement) .

## `     CREATE TABLE CLONE    ` statement

Creates a [table clone](/bigquery/docs/table-clones-intro) based on a source table. The source table can be a table, a table clone, or a [table snapshot](/bigquery/docs/table-snapshots-intro) .

### Syntax

``` text
CREATE TABLE [ IF NOT EXISTS ]
destination_table_name
CLONE source_table_name [FOR SYSTEM_TIME AS OF time_expression]
...
[OPTIONS(table_option_list)]
```

### Details

Other than the use of the `  CLONE  ` clause in place of a column list, the syntax is identical to the `  CREATE TABLE  ` syntax.

### Arguments

  - `  IF NOT EXISTS  ` : If the specified destination table name already exists, the `  CREATE  ` statement has no effect.

  - `  destination_table_name  ` : The name of the table that you want to create. The table name must be unique per dataset. The table name can contain the following:
    
      - Up to 1,024 characters
      - Letters (upper or lower case), numbers, and underscores

  - `  OPTIONS(table_option_list)  ` : Lets you specify additional table creation options such as a [label](/bigquery/docs/labels) and an expiration time.

  - `  source_table_name  ` : The name of the source table.

`  CREATE TABLE CLONE  ` statements must comply with the following rules:

  - Only one `  CREATE  ` statement is allowed.
  - The table that is being cloned must be a table, a table clone, or a table snapshot.

### `     OPTIONS    `

`  CREATE TABLE CLONE  ` options are the same as [`  CREATE TABLE  ` options](#table_option_list) .

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.tables.create      </code></td>
<td>The dataset where you create the table clone.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigquery.tables.get      </code></td>
<td>The source table.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.tables.getData      </code></td>
<td>The source table.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigquery.tables.restoreSnapshot      </code></td>
<td>The source table (required only if the source table is a table snapshot).</td>
</tr>
</tbody>
</table>

If the `  OPTIONS  ` clause includes any expiration options, then the `  bigquery.tables.delete  ` permission is also required.

### Examples

#### Restore a table snapshot: fail if destination table already exists

The following example creates the table `  myproject.mydataset.mytable  ` from the table snapshot `  myproject.mydataset.mytablesnapshot  ` :

``` text
CREATE TABLE `myproject.mydataset.mytable`
CLONE `myproject.mydataset.mytablesnapshot`
OPTIONS(
  expiration_timestamp=TIMESTAMP_ADD(CURRENT_TIMESTAMP(), INTERVAL 365 DAY),
  friendly_name="my_table",
  description="A table that expires in 1 year",
  labels=[("org_unit", "development")]
)
```

If the table name exists in the dataset, then the following error is returned:

`  Already Exists: myproject.mydataset.mytable.  `

The table option list specifies the following:

  - **Expiration time:** 365 days after the time that the table is created
  - **Friendly name:** `  my_table  `
  - **Description:** `  A table that expires in 1 year  `
  - **Label:** `  org_unit = development  `

#### Create a clone of a table: ignore if the destination table already exists

The following example creates the table clone `  myproject.mydataset.mytableclone  ` based on the table `  myproject.mydataset.mytable  ` :

``` text
CREATE TABLE IF NOT EXISTS `myproject.mydataset.mytableclone`
CLONE `myproject.mydataset.mytable`
OPTIONS(
  expiration_timestamp=TIMESTAMP_ADD(CURRENT_TIMESTAMP(), INTERVAL 365 DAY),
  friendly_name="my_table",
  description="A table that expires in 1 year",
  labels=[("org_unit", "development")]
)
```

The table option list specifies the following:

  - **Expiration time:** 365 days after the time the table is created
  - **Friendly name:** `  my_table  `
  - **Description:** `  A table that expires in 1 year  `
  - **Label:** `  org_unit = development  `

If the table name exists in the dataset, then no action is taken, and no error is returned.

For information about creating a copy of a table, see [`  CREATE TABLE COPY  `](#create_snapshot_table_statement) .

For information about creating a snapshot of a table, see [`  CREATE SNAPSHOT TABLE  `](#create_snapshot_table_statement) .

## `     CREATE VIEW    ` statement

Creates a new view.

### Syntax

``` text
CREATE [ OR REPLACE ] VIEW [ IF NOT EXISTS ] view_name
[(view_column_name_list)]
[OPTIONS(view_option_list)]
AS query_expression

view_column_name_list :=
  view_column[, ...]

view_column :=
  column_name [OPTIONS(view_column_option_list)]
```

### Arguments

  - `  OR REPLACE  ` : Replaces any view with the same name if it exists. Cannot appear with `  IF NOT EXISTS  ` .

  - `  IF NOT EXISTS  ` : If a view or other [table resource](/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.type) exists with the same name, the `  CREATE  ` statement has no effect. Cannot appear with `  OR REPLACE  ` .

  - `  view_name  ` : The name of the view you're creating. See [Table path syntax](#table_path) .

  - [`  view_column_name_list  `](#view_column_name_list) : Lets you explicitly specify the column names of the view, which may be aliases to the column names in the underlying SQL query.

  - [`  view_option_list  `](#view_option_list) : Additional view creation options such as a [label](/bigquery/docs/labels) and an expiration time.

  - `  query_expression  ` : The GoogleSQL query expression used to define the view.

### Details

`  CREATE VIEW  ` statements must comply with the following rules:

  - Only one `  CREATE  ` statement is allowed.

### `     view_column_name_list    `

The view's column name list is optional. The names must be unique but do not have to be the same as the column names of the underlying SQL query. For example, if your view is created with the following statement:

``` text
CREATE VIEW mydataset.age_groups(age, count) AS SELECT age, COUNT(*)
FROM mydataset.people
group by age;
```

Then you can query it with:

``` text
SELECT age, count from mydataset.age_groups;
```

The number of columns in the column name list must match the number of columns in the underlying SQL query. If the columns in the table of the underlying SQL query is added or dropped, the view becomes invalid and must be recreated. For example, if the `  age  ` column is dropped from the `  mydataset.people  ` table, then the view created in the previous example becomes invalid.

### `     view_column_option_list    `

The `  view_column_option_list  ` lets you specify optional top-level column options. Column options for a view have the same syntax and requirements as for a table, but with a different list of `  NAME  ` and `  VALUE  ` fields:

<table>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">       NAME      </code></th>
<th><code dir="ltr" translate="no">       VALUE      </code></th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       description      </code></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>Example: <code dir="ltr" translate="no">        description="a unique id"       </code></p></td>
</tr>
</tbody>
</table>

### `     view_option_list    `

The option list allows you to set view options such as a [label](/bigquery/docs/labels) and an expiration time. You can include multiple options using a comma-separated list.

Specify a view option list in the following format:

`  NAME=VALUE, ...  `

`  NAME  ` and `  VALUE  ` must be one of the following combinations:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">       NAME      </code></th>
<th><code dir="ltr" translate="no">       VALUE      </code></th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       expiration_timestamp      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td><p>Example: <code dir="ltr" translate="no">        expiration_timestamp=TIMESTAMP "2025-01-01 00:00:00 UTC"       </code></p>
<p>This property is equivalent to the <a href="/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.expiration_time">expirationTime</a> table resource property.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       friendly_name      </code></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>Example: <code dir="ltr" translate="no">        friendly_name="my_view"       </code></p>
<p>This property is equivalent to the <a href="/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.friendly_name">friendlyName</a> table resource property.</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       description      </code></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>Example: <code dir="ltr" translate="no">        description="a view that expires in 2025"       </code></p>
<p>This property is equivalent to the <a href="/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.description">description</a> table resource property.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       labels      </code></td>
<td><p><code dir="ltr" translate="no">        ARRAY&lt;STRUCT&lt;STRING, STRING&gt;&gt;       </code></p></td>
<td><p>Example: <code dir="ltr" translate="no">        labels=[("org_unit", "development")]       </code></p>
<p>This property is equivalent to the <a href="/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.labels">labels</a> table resource property.</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       privacy_policy      </code></td>
<td><p><code dir="ltr" translate="no">        JSON-formatted STRING       </code></p></td>
<td><p>The policies to enforce when anyone queries the view. To learn more about the policies available for a view, see the <a href="/bigquery/docs/reference/standard-sql/data-definition-language#privacy_policy"><code dir="ltr" translate="no">         privacy_policy        </code></a> view option.</p>
<strong>Note:</strong> Time travel is disabled on any view that has an analysis rule.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       tags      </code></td>
<td><code dir="ltr" translate="no">       &lt;ARRAY&lt;STRUCT&lt;STRING, STRING&gt;&gt;&gt;      </code></td>
<td>An array of IAM tags for the view, expressed as key-value pairs. The key should be the <a href="/iam/docs/tags-access-control#definitions">namespaced key name</a> , and the value should be the <a href="/iam/docs/tags-access-control#definitions">short name</a> .</td>
</tr>
</tbody>
</table>

`  VALUE  ` is a constant expression containing only literals, query parameters, and scalar functions.

The constant expression **cannot** contain:

  - A reference to a table
  - Subqueries or SQL statements such as `  SELECT  ` , `  CREATE  ` , or `  UPDATE  `
  - User-defined functions, aggregate functions, or analytic functions
  - The following scalar functions:
      - `  ARRAY_TO_STRING  `
      - `  REPLACE  `
      - `  REGEXP_REPLACE  `
      - `  RAND  `
      - `  FORMAT  `
      - `  LPAD  `
      - `  RPAD  `
      - `  REPEAT  `
      - `  SESSION_USER  `
      - `  GENERATE_ARRAY  `
      - `  GENERATE_DATE_ARRAY  `

If `  VALUE  ` evaluates to `  NULL  ` , the corresponding option `  NAME  ` in the `  CREATE VIEW  ` statement is ignored.

### `     privacy_policy    `

The following policies are available in the [`  privacy_policy  ` view option](/bigquery/docs/reference/standard-sql/data-definition-language#view_option_list) to create [analysis rules](/bigquery/docs/analysis-rules) . A policy represents a condition that needs to be met before a query can be run.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Policy</th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        aggregation_threshold_policy       </code></p></td>
<td><p>The aggregation threshold policy to enforce when a view is queried.</p>
<p>Syntax:</p>
<pre class="text" dir="ltr" data-is-upgraded="" translate="no"><code>&#39;{
  &quot;aggregation_threshold_policy&quot;: {
    &quot;threshold&quot;: value,
    &quot;privacy_unit_columns&quot;: value
  }
}&#39;</code></pre>
<p>Parameters:</p>
<ul>
<li><code dir="ltr" translate="no">         aggregation_threshold_policy        </code> : An aggregation threshold policy for the view. When this parameter is included, a minimum number of distinct entities must be present in a set of data in the view.</li>
<li><code dir="ltr" translate="no">         threshold        </code> : The minimum number of distinct privacy units (privacy unit column values) that need to contribute to each row in the query results. If a potential row doesn't satisfy this threshold, that row is omitted from the query results. <code dir="ltr" translate="no">         value        </code> is a positive JSON integer.</li>
<li><code dir="ltr" translate="no">         privacy_unit_columns        </code> : The columns that represents the privacy unit columns in a view. At this time, a view can have only one privacy unit column. <code dir="ltr" translate="no">         value        </code> is a JSON string.</li>
</ul>
<p>Example:</p>
<code dir="ltr" translate="no">       privacy_policy='{"aggregation_threshold_policy":       {"threshold" : 50,       "privacy_unit_columns": "ID"}}'      </code></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        differential_privacy_policy       </code></p></td>
<td><p>A differential privacy policy for the view. When this parameter is included, only differentially private queries can be run on the view.</p>
<p>Syntax:</p>
<pre class="text" dir="ltr" data-is-upgraded="" translate="no"><code>&#39;{
  &quot;differential_privacy_policy&quot;: {
    &quot;privacy_unit_column&quot;: value,
    &quot;max_epsilon_per_query&quot;: value,
    &quot;epsilon_budget&quot;: value,
    &quot;delta_per_query&quot;: value,
    &quot;delta_budget&quot;: value,
    &quot;max_groups_contributed&quot;: value
  }
}&#39;</code></pre>
<p>Parameters:</p>
<ul>
<li><code dir="ltr" translate="no">         differential_privacy_policy        </code> : The differential privacy policy for the view.</li>
<li><code dir="ltr" translate="no">         privacy_unit_column        </code> : The column that represents the privacy unit column for differentially private queries on the view. <code dir="ltr" translate="no">         value        </code> is a JSON string.</li>
<li><code dir="ltr" translate="no">         max_epsilon_per_query        </code> : The maximum amount of epsilon that can be specified for a differentially private query on the view. <code dir="ltr" translate="no">         value        </code> is a JSON number from 0.001 to 1e+15.</li>
<li><code dir="ltr" translate="no">         epsilon_budget        </code> : The amount of epsilon that can be used in totality for all differentially private queries on the view. <code dir="ltr" translate="no">         value        </code> is JSON number from 0.001 to 1e+15.</li>
<li><code dir="ltr" translate="no">         delta_per_query        </code> : The maximum amount of delta that can be specified for a differentially private query on the view. <code dir="ltr" translate="no">         value        </code> is a JSON number from 1e-15 to 1.</li>
<li><code dir="ltr" translate="no">         delta_budget        </code> : The amount of delta that can be used in totality for all differentially private queries on the view. The budget must be larger than the delta for any differentially private query on the view. <code dir="ltr" translate="no">         value        </code> is a JSON number from 1e-15 to `1000`.</li>
<li><code dir="ltr" translate="no">         max_groups_contributed        </code> : The maximum number of groups to which each protected entity can contribute in a differentially private query. <code dir="ltr" translate="no">         value        </code> is a non-negative JSON integer.</li>
</ul>
<p>Example:</p>
<code dir="ltr" translate="no">       privacy_policy='{"differential_privacy_policy": {       "privacy_unit_column": "contributor_id",       "max_epsilon_per_query": 0.01,       "epsilon_budget": 25.6,       "delta_per_query": 0.005,       "delta_budget": 9.6,       "max_groups_contributed": 2}}'      </code></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        join_restriction_policy       </code></p></td>
<td><p>A join restriction policy for the view. When this parameter is included, only the specified joins can be run on the specified columns in the view.</p>
<p>This policy can be used alone or with other policies, such as the aggregation threshold or differential privacy policy.</p>
<p>Syntax:</p>
<pre class="text" dir="ltr" data-is-upgraded="" translate="no"><code>&#39;{
  &quot;join_restriction_policy&quot;: {
    &quot;join_condition&quot;: value,
    &quot;join_allowed_columns&quot;: value
  }
}&#39;</code></pre>
<p>Parameters:</p>
<ul>
<li><code dir="ltr" translate="no">         join_restriction_policy        </code> : The join restriction policy for the view.</li>
<li><code dir="ltr" translate="no">         join_condition        </code> : The type of join condition to enforce on the view. <code dir="ltr" translate="no">         value        </code> can be one of the following JSON strings:
<ul>
<li><code dir="ltr" translate="no">           JOIN_ALL          </code> : All columns in <code dir="ltr" translate="no">           join_allowed_columns          </code> must be inner joined upon for this view to be queried.</li>
<li><code dir="ltr" translate="no">           JOIN_ANY          </code> : At least one column in <code dir="ltr" translate="no">           join_allowed_columns          </code> must be joined upon for this view to be queried.</li>
<li><code dir="ltr" translate="no">           JOIN_BLOCKED          </code> : This view can't be joined along any column. Don't set <code dir="ltr" translate="no">           join_allowed_columns          </code> in this case. This can be used with all analysis rules except for the <a href="/bigquery/docs/analysis-rules#list_overlap_rules">list overlap analysis rule</a> .</li>
<li><code dir="ltr" translate="no">           JOIN_NOT_REQUIRED          </code> : A join is not required to query this view. If a join is used, only the columns in <code dir="ltr" translate="no">           join_allowed_columns          </code> can be used. This can be used with all analysis rules except for the <a href="/bigquery/docs/analysis-rules#list_overlap_rules">list overlap analysis rule</a> .</li>
</ul></li>
<li><code dir="ltr" translate="no">         join_allowed_columns        </code> : A list of columns that can be part of a join operation. <code dir="ltr" translate="no">         value        </code> is a JSON array.</li>
</ul>
<p>Example:</p>
<code dir="ltr" translate="no">       privacy_policy='{"join_restriction_policy": {       "join_condition": 'JOIN_ANY',       "join_allowed_columns": ['col1', 'col2']}}'      </code></td>
</tr>
</tbody>
</table>

**Note:** Time travel is disabled on any view that has a policy.

### Default project in view body

If the view is created in the same project used to run the `  CREATE VIEW  ` statement, the view body `  query_expression  ` can reference entities without specifying the project; the default project is the project which owns the view. Consider the sample query below.

``` text
CREATE VIEW myProject.myDataset.myView AS SELECT * FROM anotherDataset.myTable;
```

After running the above `  CREATE VIEW  ` query in the project `  myProject  ` , you can run the query `  SELECT * FROM myProject.myDataset.myView  ` . Regardless of the project you choose to run this `  SELECT  ` query, the referenced table `  anotherDataset.myTable  ` is always resolved against project `  myProject  ` .

If the view is not created in the same project used to run the `  CREATE VIEW  ` statement, then all references in the view body `  query_expression  ` must be qualified with project IDs. For instance, the preceding sample `  CREATE VIEW  ` query is invalid if it runs in a project different from `  myProject  ` .

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.tables.create      </code></td>
<td>The dataset where you create the view.</td>
</tr>
</tbody>
</table>

In addition, the `  OR REPLACE  ` clause requires `  bigquery.tables.update  ` permission.

If the `  OPTIONS  ` clause includes an expiration time, then the `  bigquery.tables.delete  ` permission is also required.

### Examples

#### Creating a new view

The following example creates a view named `  newview  ` in `  mydataset  ` :

``` text
CREATE VIEW `myproject.mydataset.newview`
OPTIONS(
  expiration_timestamp=TIMESTAMP_ADD(CURRENT_TIMESTAMP(), INTERVAL 48 HOUR),
  friendly_name="newview",
  description="a view that expires in 2 days",
  labels=[("org_unit", "development")]
)
AS SELECT column_1, column_2, column_3 FROM `myproject.mydataset.mytable`
```

If the view name exists in the dataset, the following error is returned:

`  Already Exists: project_id:dataset.table  `

The view is defined using the following GoogleSQL query:

``  SELECT column_1, column_2, column_3 FROM `myproject.mydataset.mytable`  ``

The view option list specifies the:

  - **Expiration time:** 48 hours from the time the view is created
  - **Friendly name:** `  newview  `
  - **Description:** `  A view that expires in 2 days  `
  - **Label:** `  org_unit = development  `

#### Creating a view only if the view doesn't exist

The following example creates a view named `  newview  ` in `  mydataset  ` only if no view named `  newview  ` exists in `  mydataset  ` . If the view name exists in the dataset, no error is returned, and no action is taken.

``` text
CREATE VIEW IF NOT EXISTS `myproject.mydataset.newview`
OPTIONS(
  expiration_timestamp=TIMESTAMP_ADD(CURRENT_TIMESTAMP(), INTERVAL 48 HOUR),
  friendly_name="newview",
  description="a view that expires in 2 days",
  labels=[("org_unit", "development")]
)
AS SELECT column_1, column_2, column_3 FROM `myproject.mydataset.mytable`
```

The view is defined using the following GoogleSQL query:

``  SELECT column_1, column_2, column_3 FROM `myproject.mydataset.mytable`  ``

The view option list specifies the:

  - **Expiration time:** 48 hours from the time the view is created
  - **Friendly name:** `  newview  `
  - **Description:** `  A view that expires in 2 days  `
  - **Label:** `  org_unit = development  `

#### Creating or replacing a view

The following example creates a view named `  newview  ` in `  mydataset  ` , and if `  newview  ` exists in `  mydataset  ` , it is overwritten using the specified query expression.

``` text
CREATE OR REPLACE VIEW `myproject.mydataset.newview`
OPTIONS(
  expiration_timestamp=TIMESTAMP_ADD(CURRENT_TIMESTAMP(), INTERVAL 48 HOUR),
  friendly_name="newview",
  description="a view that expires in 2 days",
  labels=[("org_unit", "development")]
)
AS SELECT column_1, column_2, column_3 FROM `myproject.mydataset.mytable`
```

The view is defined using the following GoogleSQL query:

`  SELECT column_1, column_2, column_3 FROM myproject.mydataset.mytable  `

The view option list specifies the:

  - **Expiration time:** 48 hours from the time the view is created
  - **Friendly name:** `  newview  `
  - **Description:** `  A view that expires in 2 days  `
  - **Label:** `  org_unit = development  `

#### Creating a view with column descriptions

The following example creates a view named `  newview  ` in `  mydataset  ` . This view definition provides the column description for each column in `  mytable  ` . You can rename columns from the original query.

``` text
CREATE VIEW `myproject.mydataset.newview` (
  column_1_new_name OPTIONS (DESCRIPTION='Description of the column 1 contents'),
  column_2_new_name OPTIONS (DESCRIPTION='Description of the column 2 contents'),
  column_3_new_name OPTIONS (DESCRIPTION='Description of the column 3 contents')
)
AS SELECT column_1, column_2, column_3 FROM `myproject.mydataset.mytable`
```

## `     CREATE MATERIALIZED VIEW    ` statement

Creates a new materialized view.

### Syntax

``` text
CREATE [ OR REPLACE ] MATERIALIZED VIEW [ IF NOT EXISTS ] materialized_view_name
[PARTITION BY partition_expression]
[CLUSTER BY clustering_column_list]
[OPTIONS(materialized_view_option_list)]
AS query_expression
```

### Arguments

  - `  OR REPLACE  ` : Replaces a materialized view with the same name if it exists. Cannot appear with `  IF NOT EXISTS  ` .

  - `  IF NOT EXISTS  ` : If a materialized view or other [table resource](/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.type) exists with the same name, the `  CREATE  ` statement has no effect. Cannot appear with `  OR REPLACE  ` .

  - `  materialized_view_name  ` : The name of the materialized view you're creating. See [Table path syntax](#table_path) .
    
    If the `  project_name  ` is omitted from the materialized view name, or it is the same as the project that runs this DDL query, then the latter is also used as the default project for references to tables, functions, and other resources in `  query_expression  ` . The default project of the references is fixed and does not depend on the future queries that invoke the new materialized view. Otherwise, all references in `  query_expression  ` must be qualified with project names.
    
    The materialized view name must be unique per dataset.

  - [`  partition_expression  `](#partition_expression) : An expression that determines how to partition the table. A materialized view can only be partitioned in the same way as the table in `  query expression  ` (the *base table* ) is partitioned.

  - [`  clustering_column_list  `](#clustering_column_list) : A comma-separated list of column references that determine how to cluster the materialized view.

  - [`  materialized_view_option_list  `](#materialized_view_option_list) : Allows you to specify additional materialized view options such as a whether refresh is enabled, the refresh interval, a [label](/bigquery/docs/labels) , and an expiration time.

  - `  query_expression  ` : The GoogleSQL query expression used to define the materialized view.

### Details

`  CREATE MATERIALIZED VIEW  ` statements must comply with the following rules:

  - Only one `  CREATE  ` statement is allowed.

#### Default project in materialized view body

If the materialized view is created in the same project used to run the `  CREATE MATERIALIZED VIEW  ` statement, the materialized view body `  query_expression  ` can reference entities without specifying the project; the default project is the project which owns the materialized view. Consider the sample query below.

``` text
CREATE MATERIALIZED VIEW myProject.myDataset.myView AS SELECT * FROM anotherDataset.myTable;
```

After running the above `  CREATE MATERIALIZED VIEW  ` query in the project `  myProject  ` , you can run the query `  SELECT * FROM myProject.myDataset.myView  ` . Regardless of the project you choose to run this `  SELECT  ` query, the referenced table `  anotherDataset.myTable  ` is always resolved against project `  myProject  ` .

If the materialized view is not created in the same project used to run the `  CREATE VIEW  ` statement, then all references in the materialized view body `  query_expression  ` must be qualified with project IDs. For instance, the preceding sample `  CREATE MATERIALIZED VIEW  ` query is invalid if it runs in a project different from `  myProject  ` .

### `     materialized_view_option_list    `

The option list allows you to set materialized view options such as a whether refresh is enabled. the refresh interval, a [label](/bigquery/docs/labels) and an expiration time. You can include multiple options using a comma-separated list.

Specify a materialized view option list in the following format:

`  NAME=VALUE, ...  `

`  NAME  ` and `  VALUE  ` must be one of the following combinations:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">       NAME      </code></th>
<th><code dir="ltr" translate="no">       VALUE      </code></th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       enable_refresh      </code></td>
<td><code dir="ltr" translate="no">       BOOLEAN      </code></td>
<td><p>Example: <code dir="ltr" translate="no">        enable_refresh=false       </code><br />
Default: <code dir="ltr" translate="no">        true       </code></p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       refresh_interval_minutes      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
<td><p>Example: <code dir="ltr" translate="no">        refresh_interval_minutes=20       </code><br />
Default: <code dir="ltr" translate="no">        refresh_interval_minutes=30       </code></p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       expiration_timestamp      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td><p>Example: <code dir="ltr" translate="no">        expiration_timestamp=TIMESTAMP "2025-01-01 00:00:00 UTC"       </code></p>
<p>This property is equivalent to the <a href="/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.expiration_time">expirationTime</a> table resource property. <code dir="ltr" translate="no">        expiration_timestamp       </code> is optional and not used by default.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       max_staleness      </code></td>
<td><code dir="ltr" translate="no">       INTERVAL      </code></td>
<td><p>Example: <code dir="ltr" translate="no">        max_staleness=INTERVAL "4:0:0" HOUR TO SECOND       </code></p>
<p>The <a href="/bigquery/docs/materialized-views-create#max_staleness"><code dir="ltr" translate="no">         max_staleness        </code> property</a> provides consistently high performance with controlled costs when processing large, frequently changing datasets. <code dir="ltr" translate="no">        max_staleness       </code> is disabled by default.</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       allow_non_incremental_definition      </code></td>
<td><code dir="ltr" translate="no">       BOOLEAN      </code></td>
<td><p>Example: <code dir="ltr" translate="no">        allow_non_incremental_definition=true       </code></p>
<p>The <a href="/bigquery/docs/materialized-views-create#non-incremental"><code dir="ltr" translate="no">         allow_non_incremental_definition        </code> property</a> supports an expanded range of SQL queries to create materialized views. <code dir="ltr" translate="no">        allow_non_incremental_definition=true       </code> is disabled by default. <code dir="ltr" translate="no">        CREATE MATERIALIZED VIEW       </code> statement support only. The <code dir="ltr" translate="no">        allow_non_incremental_definition       </code> property can't be changed after the materialized view is created.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       kms_key_name      </code></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>Example: <code dir="ltr" translate="no">        kms_key_name="projects/                 project_id                /locations/       </code> <code dir="ltr" translate="no">          location                /keyRings/                 keyring                /cryptoKeys/                 key                "       </code></p>
<p>This property is equivalent to the <a href="/bigquery/docs/reference/rest/v2/EncryptionConfiguration#FIELDS.kms_key_name">encryptionConfiguration.kmsKeyName</a> table resource property.</p>
<p>See more details about <a href="/bigquery/docs/customer-managed-encryption">Protecting data with Cloud KMS keys</a> .</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       friendly_name      </code></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>Example: <code dir="ltr" translate="no">        friendly_name="my_mv"       </code></p>
<p>This property is equivalent to the <a href="/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.friendly_name">friendlyName</a> table resource property.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       description      </code></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>Example: <code dir="ltr" translate="no">        description="a materialized view that expires in 2025"       </code></p>
<p>This property is equivalent to the <a href="/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.description">description</a> table resource property.</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       labels      </code></td>
<td><p><code dir="ltr" translate="no">        ARRAY&lt;STRUCT&lt;STRING, STRING&gt;&gt;       </code></p></td>
<td><p>Example: <code dir="ltr" translate="no">        labels=[("org_unit", "development")]       </code></p>
<p>This property is equivalent to the <a href="/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.labels">labels</a> table resource property.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       tags      </code></td>
<td><code dir="ltr" translate="no">       ARRAY&lt;STRUCT&lt;STRING, STRING&gt;&gt;      </code></td>
<td>An array of IAM tags for the materialized view, expressed as key-value pairs. The key should be the <a href="/iam/docs/tags-access-control#definitions">namespaced key name</a> , and the value should be the <a href="/iam/docs/tags-access-control#definitions">short name</a> .</td>
</tr>
</tbody>
</table>

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.tables.create      </code></td>
<td>The dataset where you create the materialized view.</td>
</tr>
</tbody>
</table>

In addition, the `  OR REPLACE  ` clause requires `  bigquery.tables.update  ` permission.

If the `  OPTIONS  ` clause includes any expiration options, then the `  bigquery.tables.delete  ` permission is also required.

### Examples

#### Creating a new materialized view

The following example creates a materialized view named `  new_mv  ` in `  mydataset  ` :

``` text
CREATE MATERIALIZED VIEW `myproject.mydataset.new_mv`
OPTIONS(
  expiration_timestamp=TIMESTAMP_ADD(CURRENT_TIMESTAMP(), INTERVAL 48 HOUR),
  friendly_name="new_mv",
  description="a materialized view that expires in 2 days",
  labels=[("org_unit", "development")],
  enable_refresh=true,
  refresh_interval_minutes=20
)
AS SELECT column_1, SUM(column_2) AS sum_2, AVG(column_3) AS avg_3
FROM `myproject.mydataset.mytable`
GROUP BY column_1
```

If the materialized view name exists in the dataset, the following error is returned:

`  Already Exists: project_id:dataset.materialized_view  `

When you use a DDL statement to create a materialized view, you must specify the project, dataset, and materialized view in the following format: ``  ` project_id.dataset.materialized_view `  `` (including the backticks if `  project_id  ` contains special characters); for example, ``  `myproject.mydataset.new_mv`  `` .

The materialized view is defined using the following GoogleSQL query:

``  SELECT column_1, column_2, column_3 FROM `myproject.mydataset.mytable`  ``

The materialized view option list specifies the:

  - **Expiration time:** 48 hours from the time the materialized view is created
  - **Friendly name:** `  new_mv  `
  - **Description:** `  A materialized view that expires in 2 days  `
  - **Label:** `  org_unit = development  `
  - **Refresh enabled:** true
  - **Refresh interval:** 20 minutes

#### Creating a materialized view only if the materialized view doesn't exist

The following example creates a materialized view named `  new_mv  ` in `  mydataset  ` only if no materialized view named `  new_mv  ` exists in `  mydataset  ` . If the materialized view name exists in the dataset, no error is returned, and no action is taken.

``` text
CREATE MATERIALIZED VIEW IF NOT EXISTS `myproject.mydataset.new_mv`
OPTIONS(
  expiration_timestamp=TIMESTAMP_ADD(CURRENT_TIMESTAMP(), INTERVAL 48 HOUR),
  friendly_name="new_mv",
  description="a view that expires in 2 days",
  labels=[("org_unit", "development")],
  enable_refresh=false
)
AS SELECT column_1, column_2, column_3 FROM `myproject.mydataset.mytable`
```

The materialized view is defined using the following GoogleSQL query:

``  SELECT column_1, column_2, column_3 FROM `myproject.mydataset.mytable`  ``

The materialized view option list specifies the:

  - **Expiration time:** 48 hours from the time the view is created
  - **Friendly name:** `  new_mv  `
  - **Description:** `  A view that expires in 2 days  `
  - **Label:** `  org_unit = development  `
  - **Refresh enabled:** false

#### Creating a materialized view with partitioning and clustering

The following example creates a materialized view named `  new_mv  ` in `  mydataset  ` , partitioned by the `  col_datetime  ` column and clustered by the `  col_int  ` column:

``` text
CREATE MATERIALIZED VIEW `myproject.mydataset.new_mv`
PARTITION BY DATE(col_datetime)
CLUSTER BY col_int
AS SELECT col_int, col_datetime, COUNT(1) as cnt
   FROM `myproject.mydataset.mv_base_table`
   GROUP BY col_int, col_datetime
```

The base table, `  mv_base_table  ` , must also be partitioned by the `  col_datetime  ` column. For more information, see [Working with partitioned and clustered tables](/bigquery/docs/materialized-views#partition_cluster) .

## `     CREATE MATERIALIZED VIEW AS REPLICA OF    ` statement

Creates a [replica of a materialized view](/bigquery/docs/load-data-using-cross-cloud-transfer#materialized_view_replicas) . The source materialized view must be over an Amazon Simple Storage Service (Amazon S3) BigLake table. You can use the materialized view replica to make Amazon S3 data available locally for joins.

For more information, see [Create materialized view replicas](/bigquery/docs/load-data-using-cross-cloud-transfer#create) .

### Syntax

``` text
CREATE MATERIALIZED VIEW replica_name
[OPTIONS(materialized_view_replica_option_list)]
AS REPLICA OF source_materialized_view_name
```

### Arguments

  - `  replica_name  ` : The name of the materialized view replica you're creating, in [table path syntax](#table_path) . If the project name is omitted from the materialized view replica name, the current project is used as the default.
    
    The materialized view replica name must be unique for each dataset.

  - [`  materialized_view_replica_option_list  `](#materialized_view_replica_option_list) : Allows you to specify options such as the replication interval.

  - `  source_materialized_view_name  ` : The name of the materialized view you are replicating, in table path syntax. The source materialized view must be over an Amazon S3 BigLake table, and must be authorized on the dataset that contains that table.

### `     materialized_view_replica_option_list    `

The option list lets you set materialized view replica options.

Specify a materialized view replica option list in the following format:

`  NAME=VALUE, ...  `

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">       NAME      </code></th>
<th><code dir="ltr" translate="no">       VALUE      </code></th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       replication_interval_seconds      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td><p>Specifies how often to replicate the data from the source materialized view to the replica. Must be a value between <code dir="ltr" translate="no">        60       </code> and <code dir="ltr" translate="no">        3,600       </code> , inclusive. Defaults to <code dir="ltr" translate="no">        300       </code> (5 minutes).</p>
<p>Example: <code dir="ltr" translate="no">        replication_interval_seconds=900       </code></p></td>
</tr>
</tbody>
</table>

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

  - `  bigquery.tables.create  `
  - `  bigquery.tables.get  `
  - `  bigquery.tables.getData  `
  - `  bigquery.tables.replicateData  `
  - `  bigquery.jobs.create  `

### Example

The following example creates a materialized view replica named `  mv_replica  ` in `  bq_dataset  ` :

``` text
CREATE MATERIALIZED VIEW `myproject.bq_dataset.mv_replica`
OPTIONS(
  replication_interval_seconds=600
)
AS REPLICA OF `myproject.s3_dataset.my_s3_mv`
```

## `     CREATE EXTERNAL SCHEMA    ` statement

Creates a new federated dataset.

A federated dataset is a connection between BigQuery and an external data source at the dataset level. For more information about creating federated datasets, see the following:

  - [Create AWS Glue federated datasets](/bigquery/docs/glue-federated-datasets) .
  - [Create Spanner federated datasets](/bigquery/docs/spanner-external-datasets) .

### Syntax

``` text
CREATE EXTERNAL SCHEMA [ IF NOT EXISTS ] dataset_name
[WITH CONNECTION connection_name]
[OPTIONS(external_schema_option_list)]
```

### Arguments

  - `  IF NOT EXISTS  ` : If any dataset exists with the same name, the `  CREATE  ` statement has no effect.

  - `  dataset_name  ` : The name of the dataset to create.

  - `  connection_name  ` : Specifies a [connection resource](/bigquery/docs/connections-api-intro) that has credentials for accessing the external data. Specify the connection name in the form PROJECT\_ID . LOCATION . CONNECTION\_ID . If the project ID or location contains a dash, enclose the connection name in backticks ( ``  `  `` ).

  - [`  external_schema_option_list  `](#external_schema_option_list) : A list of options for creating the federated dataset.

### Details

The dataset is created in the location that you specify in the query settings. For more information, see [Specify locations](/bigquery/docs/locations#specify_locations) . The location must support the kind of federated dataset that you are creating, for example, you can only create AWS Glue federated datasets in AWS locations.

For more information about creating a dataset, see [Create datasets](/bigquery/docs/datasets) . For information about quotas, see [dataset limits](/bigquery/quotas#dataset_limits) .

### `     external_schema_option_list    `

The option list specifies options for the federated dataset. Specify the options in the following format: `  NAME=VALUE, ...  `

The following options are supported:

<table>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">       NAME      </code></th>
<th><code dir="ltr" translate="no">       VALUE      </code></th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       description      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The description of the dataset.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       friendly_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>A descriptive name for the dataset.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       labels      </code></td>
<td><code dir="ltr" translate="no">       &lt;ARRAY&lt;STRUCT&lt;STRING, STRING&gt;&gt;&gt;      </code></td>
<td>An array of labels for the dataset, expressed as key-value pairs.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       location      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The location in which to create the dataset. If you don't specify this option, the dataset is created in the location where the query runs. If you specify this option and also explicitly set the location for the query job, the two values must match; otherwise the query fails. The location must support the kind of federated dataset that you are creating, for example, you can only create AWS Glue federated datasets in AWS locations.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       external_source      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The source of the external dataset. For AWS Glue federated datasets this must be an <a href="https://docs.aws.amazon.com/glue/latest/dg/glue-specifying-resource-arns.html">Amazon Resource Name (ARN)</a> , with a prefix identifying the source, such as <code dir="ltr" translate="no">       aws-glue://      </code> . For Spanner federated datasets, this must be a specific Spanner database with a <code dir="ltr" translate="no">       google-cloudspanner:/      </code> prefix. For example: <code dir="ltr" translate="no">       google-cloudspanner:/projects/my_project/instances/my_instance/databases/my_database      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       tags      </code></td>
<td><code dir="ltr" translate="no">       &lt;ARRAY&lt;STRUCT&lt;STRING, STRING&gt;&gt;&gt;      </code></td>
<td>An array of IAM tags expressed as key-value pairs. The key should be the <a href="/iam/docs/tags-access-control#definitions">namespaced key name</a> , and the value should be the <a href="/iam/docs/tags-access-control#definitions">short name</a> .</td>
</tr>
</tbody>
</table>

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.datasets.create      </code></td>
<td>The project where you create the federated dataset.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigquery.connections.use      </code></td>
<td>The project where you create the federated dataset.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.connections.delegate      </code></td>
<td>The project where you create the federated dataset.</td>
</tr>
</tbody>
</table>

### Examples

The following example creates an AWS Glue federated dataset:

``` text
CREATE EXTERNAL SCHEMA mydataset
WITH CONNECTION myproject.`aws-us-east-1`.myconnection
  OPTIONS (
    external_source = 'aws-glue://arn:aws:glue:us-east-1:123456789:database/test_database',
    location = 'aws-us-east-1');
```

## `     CREATE EXTERNAL TABLE    ` statement

Creates a new external table.

External tables let BigQuery query data that is stored outside of BigQuery storage. For more information about external tables, see [Introduction to external data sources](/bigquery/external-data-sources) .

### Syntax

``` text
CREATE [ OR REPLACE ] EXTERNAL TABLE [ IF NOT EXISTS ] table_name
[(
  column_name column_schema,
  ...
)]
[WITH CONNECTION {connection_name | DEFAULT}]
[WITH PARTITION COLUMNS
  [(
      partition_column_name partition_column_type,
      ...
  )]
]
OPTIONS (
  external_table_option_list,
  ...
);
```

### Arguments

  - `  OR REPLACE  ` : Replaces any external table with the same name if it exists. Cannot appear with `  IF NOT EXISTS  ` .

  - `  IF NOT EXISTS  ` : If an external table or other [table resource](/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.type) exists with the same name, the `  CREATE  ` statement has no effect. Cannot appear with `  OR REPLACE  ` .

  - `  table_name  ` : The name of the external table. See [Table path syntax](#table_path) .

  - `  column_name  ` : The name of a column in the table.

  - `  column_schema  ` : Specifies the schema of the column. It uses the same syntax as the [`  column_schema  `](#column_name_and_column_schema) definition in the [`  CREATE TABLE  `](#create_table_statement) statement. If you don't include this clause, BigQuery detects the schema automatically.

  - `  connection_name  ` : Specifies a [connection resource](/bigquery/docs/connections-api-intro) that has credentials for accessing the external data. Specify the connection name in the form PROJECT\_ID . LOCATION . CONNECTION\_ID . If the project ID or location contains a dash, enclose the connection name in backticks ( ``  `  `` ). To use a [default connection](/bigquery/docs/default-connections) , specify `  DEFAULT  ` instead of the connection string containing PROJECT\_ID . LOCATION . CONNECTION\_ID .

  - `  partition_column_name  ` : The name of a partition column. Include this field if your external data uses a hive-partitioned layout. For more information, see: [Supported data layouts](/bigquery/docs/hive-partitioned-queries-gcs#supported_data_layouts) .

  - `  partition_column_type  ` : The partition column type.

  - [`  external_table_option_list  `](#external_table_option_list) : A list of options for creating the external table.

### Details

The `  CREATE EXTERNAL TABLE  ` statement does not support creating temporary external tables.

To create an externally partitioned table, use the `  WITH PARTITION COLUMNS  ` clause to specify the partition schema details. BigQuery validates the column definitions against the external data location. The schema declaration must strictly follow the ordering of the fields in the external path. For more information about external partitioning, see [Querying externally partitioned data](/bigquery/docs/hive-partitioned-queries-gcs) .

### `     external_table_option_list    `

The option list specifies options for creating the external table. The `  format  ` and `  uris  ` options are required. Specify the option list in the following format: `  NAME=VALUE, ...  `

Options

`  allow_jagged_rows  `

`  BOOL  `

If `  true  ` , allow rows that are missing trailing optional columns.

Applies to CSV data.

`  allow_quoted_newlines  `

`  BOOL  `

If `  true  ` , allow quoted data sections that contain newline characters in the file.

Applies to CSV data.

`  bigtable_options  `

`  STRING  `

Only required when creating a Bigtable external table.

Specifies the schema of the Bigtable external table in JSON format.

For a list of Bigtable table definition options, see `  BigtableOptions  ` in the REST API reference.

`  compression  `

`  STRING  `

The compression type of the data source. Supported values include: `  GZIP  ` . If not specified, the data source is uncompressed.

Applies to CSV and JSON data.

`  decimal_target_types  `

`  ARRAY<STRING>  `

Determines how to convert a `  Decimal  ` type. Equivalent to [ExternalDataConfiguration.decimal\_target\_types](/bigquery/docs/reference/rest/v2/tables#ExternalDataConfiguration.FIELDS.decimal_target_types)

Example: `  ["NUMERIC", "BIGNUMERIC"]  ` .

`  description  `

`  STRING  `

A description of this table.

`  enable_list_inference  `

`  BOOL  `

If `  true  ` , use schema inference specifically for Parquet LIST logical type.

Applies to Parquet data.

`  enable_logical_types  `

`  BOOL  `

If `  true  ` , convert Avro logical types into their corresponding SQL types. For more information, see [Logical types](/bigquery/docs/loading-data-cloud-storage-avro#logical_types) .

Applies to Avro data.

`  encoding  `

`  STRING  `

The character encoding of the data. Supported values include: `  UTF8  ` (or `  UTF-8  ` ), `  ISO_8859_1  ` (or `  ISO-8859-1  ` ), `  UTF-16BE  ` , `  UTF-16LE  ` , `  UTF-32BE  ` , or `  UTF-32LE  ` . The default value is `  UTF-8  ` .

Applies to CSV data.

`  enum_as_string  `

`  BOOL  `

If `  true  ` , infer Parquet ENUM logical type as STRING instead of BYTES by default.

Applies to Parquet data.

`  expiration_timestamp  `

`  TIMESTAMP  `

The time when this table expires. If not specified, the table does not expire.

Example: `  "2025-01-01 00:00:00 UTC"  ` .

`  field_delimiter  `

`  STRING  `

The separator for fields in a CSV file.

Applies to CSV data.

`  format  `

`  STRING  `

The format of the external data. Supported values for [`  CREATE EXTERNAL TABLE  `](/bigquery/docs/reference/standard-sql/data-definition-language#create_external_table_statement) include: `  AVRO  ` , `  CLOUD_BIGTABLE  ` , `  CSV  ` , `  DATASTORE_BACKUP  ` , `  DELTA_LAKE  ` ( [preview](https://cloud.google.com/products/#product-launch-stages) ), `  GOOGLE_SHEETS  ` , `  NEWLINE_DELIMITED_JSON  ` (or `  JSON  ` ), `  ORC  ` , `  PARQUET  ` .

Supported values for [`  LOAD DATA  `](/bigquery/docs/reference/standard-sql/load-statements) include: `  AVRO  ` , `  CSV  ` , `  DELTA_LAKE  ` ( [preview](https://cloud.google.com/products/#product-launch-stages) ) `  NEWLINE_DELIMITED_JSON  ` (or `  JSON  ` ), `  ORC  ` , `  PARQUET  ` .

The value `  JSON  ` is equivalent to `  NEWLINE_DELIMITED_JSON  ` .

`  hive_partition_uri_prefix  `

`  STRING  `

A common prefix for all source URIs before the partition key encoding begins. Applies only to hive-partitioned external tables.

Applies to Avro, CSV, JSON, Parquet, and ORC data.

Example: `  "gs://bucket/path"  ` .

`  file_set_spec_type  `

`  STRING  `

Specifies how to interpret source URIs for load jobs and external tables.

Supported values include:

  - `  FILE_SYSTEM_MATCH  ` . Expands source URIs by listing files from the object store. This is the default behavior if FileSetSpecType is not set.
  - `  NEW_LINE_DELIMITED_MANIFEST  ` . Indicates that the provided URIs are newline-delimited manifest files, with one URI per line. Wildcard URIs are not supported in the manifest files, and all referenced data files must be in the same bucket as the manifest file.

For example, if you have a source URI of `  "gs://bucket/path/file"  ` and the `  file_set_spec_type  ` is `  FILE_SYSTEM_MATCH  ` , then the file is used directly as a data file. If the `  file_set_spec_type  ` is `  NEW_LINE_DELIMITED_MANIFEST  ` , then each line in the file is interpreted as a URI that points to a data file.

`  ignore_unknown_values  `

`  BOOL  `

If `  true  ` , ignore extra values that are not represented in the table schema, without returning an error.

Applies to CSV and JSON data.

`  json_extension  `

`  STRING  `

For JSON data, indicates a particular JSON interchange format. If not specified, BigQuery reads the data as generic JSON records.

Supported values include:  
`  GEOJSON  ` . Newline-delimited GeoJSON data. For more information, see [Creating an external table from a newline-delimited GeoJSON file](/bigquery/docs/geospatial-data#external-geojson) .

`  max_bad_records  `

`  INT64  `

The maximum number of bad records to ignore when reading the data.

Applies to: CSV, JSON, and Google Sheets data.

`  max_staleness  `

`  INTERVAL  `

Applicable for [BigLake tables](/bigquery/docs/biglake-intro#metadata_caching_for_performance) and [object tables](/bigquery/docs/object-table-introduction#metadata_caching_for_performance) .

Specifies whether cached metadata is used by operations against the table, and how fresh the cached metadata must be in order for the operation to use it.

To disable metadata caching, specify 0. This is the default.

To enable metadata caching, specify an [interval literal](/bigquery/docs/reference/standard-sql/lexical#interval_literals) value between 30 minutes and 7 days. For example, specify `  INTERVAL 4 HOUR  ` for a 4 hour staleness interval. With this value, operations against the table use cached metadata if it has been refreshed within the past 4 hours. If the cached metadata is older than that, the operation falls back to retrieving metadata from Cloud Storage instead.

`  null_marker  `

`  STRING  `

The string that represents `  NULL  ` values in a CSV file.

Applies to CSV data.

`  null_markers  `

`  ARRAY<STRING>  `

The list of strings that represent `  NULL  ` values in a CSV file.

This option cannot be used with `  null_marker  ` option.

Applies to CSV data.

`  object_metadata  `

`  STRING  `

Only required when creating an [object table](/bigquery/docs/object-table-introduction) .

Set the value of this option to `  SIMPLE  ` when creating an object table.

`  preserve_ascii_control_characters  `

`  BOOL  `

If `  true  ` , then the embedded ASCII control characters which are the first 32 characters in the ASCII table, ranging from '\\x00' to '\\x1F', are preserved.

Applies to CSV data.

`  projection_fields  `

`  STRING  `

A list of entity properties to load.

Applies to Datastore data.

`  quote  `

`  STRING  `

The string used to quote data sections in a CSV file. If your data contains quoted newline characters, also set the `  allow_quoted_newlines  ` property to `  true  ` .

Applies to CSV data.

`  reference_file_schema_uri  `

`  STRING  `

User provided reference file with the table schema.

Applies to Parquet/ORC/AVRO data.

Example: `  "gs://bucket/path/reference_schema_file.parquet"  ` .

`  require_hive_partition_filter  `

`  BOOL  `

If `  true  ` , all queries over this table require a partition filter that can be used to eliminate partitions when reading data. Applies only to hive-partitioned external tables.

Applies to Avro, CSV, JSON, Parquet, and ORC data.

`  sheet_range  `

`  STRING  `

Range of a Google Sheets spreadsheet to query from.

Applies to Google Sheets data.

Example: `  "sheet1!A1:B20"  ` ,

`  skip_leading_rows  `

`  INT64  `

The number of rows at the top of a file to skip when reading the data.

Applies to CSV and Google Sheets data.

`  source_column_match  `

`  STRING  `

This controls the strategy used to match loaded columns to the schema.

If this value is unspecified, then the default is based on how the schema is provided. If autodetect is enabled, then the default behavior is to match columns by name. Otherwise, the default is to match columns by position. This is done to keep the behavior backward-compatible.

Supported values include:

  - `  POSITION  ` : matches by position. This option assumes that the columns are ordered the same way as the schema.
  - `  NAME  ` : matches by name. This option reads the header row as column names and reorders columns to match the field names in the schema. Column names are read from the last skipped row based on the `  skip_leading_rows  ` property.

`  tags  `

`  <ARRAY<STRUCT<STRING, STRING>>>  `

An array of IAM tags for the table, expressed as key-value pairs. The key should be the [namespaced key name](/iam/docs/tags-access-control#definitions) , and the value should be the [short name](/iam/docs/tags-access-control#definitions) .

`  time_zone  `

`  STRING  `

Default time zone that will apply when parsing timestamp values that have no specific time zone.

Check [valid time zone names](/bigquery/docs/reference/standard-sql/data-types#time_zone_name) .

If this value is not present, the timestamp values without specific time zone is parsed using default time zone UTC.

Applies to CSV and JSON data.

`  date_format  `

`  STRING  `

[Format elements](/bigquery/docs/reference/standard-sql/format-elements#format_string_as_datetime) that define how the DATE values are formatted in the input files (for example, `  MM/DD/YYYY  ` ).

If this value is present, this format is the only compatible DATE format. [Schema autodetection](/bigquery/docs/schema-detect#date_and_time_values) will also decide DATE column type based on this format instead of the existing format.

If this value is not present, the DATE field is parsed with the [default formats](/bigquery/docs/loading-data-cloud-storage-csv#data_types) .

Applies to CSV and JSON data.

`  datetime_format  `

`  STRING  `

[Format elements](/bigquery/docs/reference/standard-sql/format-elements#format_string_as_datetime) that define how the DATETIME values are formatted in the input files (for example, `  MM/DD/YYYY HH24:MI:SS.FF3  ` ).

If this value is present, this format is the only compatible DATETIME format. [Schema autodetection](/bigquery/docs/schema-detect#date_and_time_values) will also decide DATETIME column type based on this format instead of the existing format.

If this value is not present, the DATETIME field is parsed with the [default formats](/bigquery/docs/loading-data-cloud-storage-csv#data_types) .

Applies to CSV and JSON data.

`  time_format  `

`  STRING  `

[Format elements](/bigquery/docs/reference/standard-sql/format-elements#format_string_as_datetime) that define how the TIME values are formatted in the input files (for example, `  HH24:MI:SS.FF3  ` ).

If this value is present, this format is the only compatible TIME format. [Schema autodetection](/bigquery/docs/schema-detect#date_and_time_values) will also decide TIME column type based on this format instead of the existing format.

If this value is not present, the TIME field is parsed with the [default formats](/bigquery/docs/loading-data-cloud-storage-csv#data_types) .

Applies to CSV and JSON data.

`  timestamp_format  `

`  STRING  `

[Format elements](/bigquery/docs/reference/standard-sql/format-elements#format_string_as_datetime) that define how the TIMESTAMP values are formatted in the input files (for example, `  MM/DD/YYYY HH24:MI:SS.FF3  ` ).

If this value is present, this format is the only compatible TIMESTAMP format. [Schema autodetection](/bigquery/docs/schema-detect#date_and_time_values) will also decide TIMESTAMP column type based on this format instead of the existing format.

If this value is not present, the TIMESTAMP field is parsed with the [default formats](/bigquery/docs/loading-data-cloud-storage-csv#data_types) .

Applies to CSV and JSON data.

`  uris  `

For external tables, including object tables, that aren't Bigtable tables:

`  ARRAY<STRING>  `

An array of fully qualified URIs for the external data locations. Each URI can contain one asterisk ( `  *  ` ) [wildcard character](/bigquery/docs/loading-data-cloud-storage#load-wildcards) , which must come after the bucket name. When you specify `  uris  ` values that target multiple files, all of those files must share a compatible schema.

The following examples show valid `  uris  ` values:

  - `  ['gs://bucket/path1/myfile.csv']  `
  - `  ['gs://bucket/path1/*.csv']  `
  - `  ['gs://bucket/path1/*', 'gs://bucket/path2/file00*']  `

  

For Bigtable tables:

`  STRING  `

The URI identifying the Bigtable table to use as a data source. You can only specify one Bigtable URI.

Example: `  https://googleapis.com/bigtable/projects/ project_id /instances/ instance_id [/appProfiles/ app_profile ]/tables/ table_name  `

For more information on constructing a Bigtable URI, see [Retrieve the Bigtable URI](/bigquery/docs/create-bigtable-external-table#bigtable-uri) .

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.tables.create      </code></td>
<td>The dataset where you create the external table.</td>
</tr>
</tbody>
</table>

In addition, the `  OR REPLACE  ` clause requires `  bigquery.tables.update  ` permission.

If the `  OPTIONS  ` clause includes an expiration time, then the `  bigquery.tables.delete  ` permission is also required.

### Examples

The following example creates a BigLake table and explicitly specifies the schema. It also specifies refreshing metadata cache automatically at a system-defined interval.

``` text
CREATE OR REPLACE EXTERNAL TABLE mydataset.newtable (x INT64, y STRING, z BOOL)
  WITH CONNECTION myconnection
  OPTIONS(
    format ="PARQUET",
    max_staleness = STALENESS_INTERVAL,
    metadata_cache_mode = 'AUTOMATIC');
```

The following example creates an external table from multiple URIs. The data format is CSV. This example uses schema auto-detection.

``` text
CREATE EXTERNAL TABLE dataset.CsvTable OPTIONS (
  format = 'CSV',
  uris = ['gs://bucket/path1.csv', 'gs://bucket/path2.csv']
);
```

The following example creates an external table from a CSV file and explicitly specifies the schema. It also specifies the field delimiter ( `  '|'  ` ) and sets the maximum number of bad records allowed.

``` text
CREATE OR REPLACE EXTERNAL TABLE dataset.CsvTable
(
  x INT64,
  y STRING
)
OPTIONS (
  format = 'CSV',
  uris = ['gs://bucket/path1.csv'],
  field_delimiter = '|',
  max_bad_records = 5
);
```

The following example creates an externally partitioned table. It uses schema auto-detection to detect both the file schema and the hive partitioning layout. If the external path is `  gs://bucket/path/field_1=first/field_2=1/data.parquet  ` , the partition columns are detected as `  field_1  ` ( `  STRING  ` ) and `  field_2  ` ( `  INT64  ` ).

``` text
CREATE EXTERNAL TABLE dataset.AutoHivePartitionedTable
WITH PARTITION COLUMNS
OPTIONS (
  uris = ['gs://bucket/path/*'],
  format = 'PARQUET',
  hive_partition_uri_prefix = 'gs://bucket/path',
  require_hive_partition_filter = false);
```

The following example creates an externally partitioned table by explicitly specifying the partition columns. This example assumes that the external file path has the pattern `  gs://bucket/path/field_1=first/field_2=1/data.parquet  ` .

``` text
CREATE EXTERNAL TABLE dataset.CustomHivePartitionedTable
WITH PARTITION COLUMNS (
  field_1 STRING, -- column order must match the external path
  field_2 INT64)
OPTIONS (
  uris = ['gs://bucket/path/*'],
  format = 'PARQUET',
  hive_partition_uri_prefix = 'gs://bucket/path',
  require_hive_partition_filter = false);
```

## `     CREATE FUNCTION    ` statement

Creates a new [user-defined function](/bigquery/docs/user-defined-functions) (UDF). BigQuery supports UDFs written in SQL, JavaScript, or Python.

### Syntax

To create a SQL UDF, use the following syntax:

``` text
CREATE [ OR REPLACE ] [ TEMPORARY | TEMP ] FUNCTION [ IF NOT EXISTS ]
    [[project_name.]dataset_name.]function_name
    ([named_parameter[, ...]])
     ([named_parameter[, ...]])
  [RETURNS data_type]
  AS (sql_expression)
  [OPTIONS (function_option_list)]

named_parameter:
  param_name param_type
```

To create a JavaScript UDF, use the following syntax:

``` text
CREATE [OR REPLACE] [TEMPORARY | TEMP] FUNCTION [IF NOT EXISTS]
    [[project_name.]dataset_name.]function_name
    ([named_parameter[, ...]])
  RETURNS data_type
  [determinism_specifier]
  LANGUAGE js
  [OPTIONS (function_option_list)]
  AS javascript_code

named_parameter:
  param_name param_type

determinism_specifier:
  { DETERMINISTIC | NOT DETERMINISTIC }
```

To create a Python UDF, use the following syntax:

**Preview**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

**Note:** For support during the preview, email <bq-python-udf-feedback@google.com> .

``` text
CREATE [OR REPLACE] FUNCTION [IF NOT EXISTS]
    [project_name.]dataset_name.function_name
    ([named_parameter[, ...]])
  RETURNS data_type
  LANGUAGE python
  [WITH CONNECTION connection_path]
  OPTIONS (function_option_list)
  AS python_code

named_parameter:
  param_name param_type
```

To create a remote function, use the following syntax:

``` text
CREATE [OR REPLACE] [TEMPORARY | TEMP] FUNCTION [IF NOT EXISTS]
    [[project_name.]dataset_name.]function_name
    ([named_parameter[, ...]])
  RETURNS data_type
  REMOTE WITH CONNECTION connection_path
  [OPTIONS (function_option_list)]

named_parameter:
  param_name param_type
```

Routine names must contain only letters, numbers, and underscores, and be at most 256 characters long.

### Arguments

  - `  OR REPLACE  ` : Replaces any function with the same name if it exists. Cannot appear with `  IF NOT EXISTS  ` .

  - `  IF NOT EXISTS  ` : If any dataset exists with the same name, the `  CREATE  ` statement has no effect. Cannot appear with `  OR REPLACE  ` .

  - `  TEMP  ` or `  TEMPORARY  ` : Creates a temporary function. If the clause is not present, the statement creates a persistent UDF. You can reuse persistent UDFs across multiple queries, whereas you can only use temporary UDFs in a single query, script, session, or procedure.

  - `  project_name  ` : For persistent functions, the name of the project where you are creating the function. Defaults to the project that runs the DDL query. Do not include the project name for temporary functions.

  - `  dataset_name  ` : For persistent functions, the name of the dataset where you are creating the function. Defaults to the `  defaultDataset  ` in the request. Do not include the dataset name for temporary functions.

  - `  function_name  ` : The name of the function.

  - `  named_parameter  ` : A comma-separated `  param_name  ` and `  param_type  ` pair. The value of `  param_type  ` is a BigQuery [data type](/bigquery/docs/reference/standard-sql/data-types) . For a SQL UDF, the value of `  param_type  ` can also be `  ANY TYPE  ` .

  - `  determinism_specifier  ` : Applies only to JavaScript UDFs. Provides a hint to BigQuery as to whether the query result can be cached. Can be one of the following values:
    
      - `  DETERMINISTIC  ` : The function always returns the same result when passed the same arguments. The query result is potentially cacheable. For example, if the function `  add_one(i)  ` always returns `  i + 1  ` , the function is deterministic.
    
      - `  NOT DETERMINISTIC  ` : The function does not always return the same result when passed the same arguments, and therefore is not cacheable. For example, if the functionj `  add_random(i)  ` returns `  i + rand()  ` , the function is not deterministic and BigQuery does not use cached results.
        
        If all of the invoked functions are `  DETERMINISTIC  ` , BigQuery tries to cache the result, unless the results can't be cached for other reasons. For more information, see [Using cached query results](/bigquery/docs/cached-results) .

  - `  data_type  ` : The data type that the function returns.
    
      - If the function is defined in SQL, then the `  RETURNS  ` clause is optional. If the `  RETURNS  ` clause is omitted, then BigQuery infers the result type of the function from the SQL function body when a query calls the function.
    
      - If the function is defined in JavaScript, then the `  RETURNS  ` clause is required. For more information about allowed values for `  data_type  ` , see [Supported JavaScript UDF data types](/bigquery/docs/reference/standard-sql/user-defined-functions#supported-javascript-udf-data-types) .

  - `  sql_expression  ` : The SQL expression that defines the function.

  - [`  function_option_list  `](#function_option_list) : A list of options for creating the function.

  - `  javascript_code  ` : The definition of a JavaScript function. The value is a [string literal](/bigquery/docs/reference/standard-sql/lexical#string_and_bytes_literals) . If the code includes quotes and backslashes, it must be either escaped or represented as a raw string. For example, the code `  return "\n";  ` can be represented as one of the following:
    
      - Quoted string `  "return \"\\n\";"  ` . Both quotes and backslashes need to be escaped.
      - Triple quoted string: `  """return "\\n";"""  ` . Backslashes need to be escaped, quotes don't.
      - Raw string: `  r"""return "\n";"""  ` . No escaping is needed.

  - `  python_code  ` : The definition of a Python function. The value is a [string literal](/bigquery/docs/reference/standard-sql/lexical#string_and_bytes_literals) . If the code includes quotes and backslashes, it must be escaped or represented as a raw string. For example, the code `  return "\n";  ` can be represented as one of the following:
    
      - Quoted string: `  "return \"\\n\";"  ` . Both quotes and backslashes need to be escaped.
      - Triple quoted string: `  """return "\\n";"""  ` . Backslashes need to be escaped, quotes don't.
      - Raw string: `  r"""return "\n";"""  ` . No escaping is needed.

  - `  connection_name  ` : Specifies a [connection resource](/bigquery/docs/connections-api-intro) that has credentials for accessing the remote endpoint or for running Python code. Specify the connection name in the form `  project_name.location.connection_id  ` : If the project name or location contains a dash, enclose the connection name in backticks ( ``  `  `` ).

### `     function_option_list    `

The option list specifies options for creating a UDF. The following options are supported:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">       NAME      </code></th>
<th><code dir="ltr" translate="no">       VALUE      </code></th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       description      </code></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td>A description of the UDF. This option isn't supported when creating a temporary function.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       library      </code></td>
<td><p><code dir="ltr" translate="no">        ARRAY &lt;STRING&gt;       </code></p></td>
<td><p>An array of JavaScript libraries to include in the function definition. Applies only to JavaScript and Python UDFs. For more information, see <a href="/bigquery/docs/user-defined-functions-python#use-imported-lib">Including JavaScript libraries</a> .</p>
<p>Example: <code dir="ltr" translate="no">        ["gs://my-bucket/lib1.js", "gs://my-bucket/lib2.js"]       </code></p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       endpoint      </code></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td>An HTTP endpoint of Cloud Functions. Applies only to remote functions.
<p>Example: <code dir="ltr" translate="no">        "https://us-east1-your-project.cloudfunctions.net/foo"       </code></p>
<p>For more information, see <a href="/bigquery/docs/remote-functions#create_a_remote_function">Create a remote function</a> .</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       user_defined_context      </code></td>
<td><p><code dir="ltr" translate="no">        ARRAY &lt;STRUCT &lt;STRING,STRING&gt;&gt;       </code></p></td>
<td><p>A list of key-value pairs that will be sent with every HTTP request when the function is invoked. Applies only to remote functions.</p>
<p>Example: <code dir="ltr" translate="no">        [("key1","value1"),("key2", "value2")]       </code></p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       max_batching_rows      </code></td>
<td><p><code dir="ltr" translate="no">        INT64       </code></p></td>
<td><p>The maximum number of rows in each HTTP request. If not specified, BigQuery decides how many rows are included in a HTTP request. Applies only to remote functions and Python UDFs.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       runtime_version      </code></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>The name of the runtime version to run provided Python code. Applies only to Python UDFs. Example: <code dir="ltr" translate="no">        python-3.11       </code></p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       entry_point      </code></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>The name of the function defined in Python code as the entry point when the Python UDF is invoked. Applies only to Python UDFs.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       packages      </code></td>
<td><p><code dir="ltr" translate="no">        ARRAY&lt;STRING&gt;       </code></p></td>
<td><p>An array of Python packages to install in the function definition. Applies only to Python UDFs. For more information, see <a href="/bigquery/docs/user-defined-functions-python#third-party-packages">Use third party packages</a> .</p>
<p>Example: <code dir="ltr" translate="no">        ["pandas&gt;=2.1", "google-cloud-translate==3.11"]       </code></p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       container_cpu      </code></td>
<td><p><code dir="ltr" translate="no">        DOUBLE       </code></p></td>
<td><p>Amount of CPU provisioned for a Python UDF container instance. Applied only to Python UDFs. For more information, see <a href="/bigquery/docs/user-defined-functions-python#configure-container-limits">Configure container limits for Python UDF</a> .</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       container_memory      </code></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>Amount of memory provisioned for a Python UDF container instance. Applies only to Python UDFs. For more information, see <a href="/bigquery/docs/user-defined-functions-python#configure-container-limits">Configure container limits for Python UDF</a> .</p></td>
</tr>
</tbody>
</table>

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.routines.create      </code></td>
<td>The dataset where you create the function.</td>
</tr>
</tbody>
</table>

In addition, the `  OR REPLACE  ` clause requires `  bigquery.routines.update  ` permission.

To create a remote function, additional [IAM permissions](/bigquery/docs/access-control#bq-permissions) are needed:

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.connections.delegate      </code></td>
<td>The connection which you use to create the remote function.</td>
</tr>
</tbody>
</table>

### Examples

#### Create a SQL UDF

The following example creates a persistent SQL UDF named `  multiplyInputs  ` in a dataset named `  mydataset  ` .

``` text
CREATE FUNCTION mydataset.multiplyInputs(x FLOAT64, y FLOAT64)
RETURNS FLOAT64
AS (x * y);
```

#### Create a JavaScript UDF

The following example creates a temporary JavaScript UDF named `  multiplyInputs  ` and calls it from inside a `  SELECT  ` statement.

``` text
CREATE TEMP FUNCTION multiplyInputs(x FLOAT64, y FLOAT64)
RETURNS FLOAT64
LANGUAGE js
AS r"""
  return x*y;
""";


SELECT multiplyInputs(a, b) FROM (SELECT 3 as a, 2 as b);
```

#### Create a remote function

The following example creates a temporary remote function named `  tempRemoteMultiplyInputs  ` in `  US  ` location, using a connection called `  myconnection  ` in the 'US' region.

``` text
CREATE TEMP FUNCTION tempRemoteMultiplyInputs(x FLOAT64, y FLOAT64)
RETURNS FLOAT64
REMOTE WITH CONNECTION us.myconnection
OPTIONS(endpoint="https://us-central1-myproject.cloudfunctions.net/multiply");
```

The following example creates a persistent remote function named `  remoteMultiplyInputs  ` in a dataset named `  mydataset  ` using a connection called `  myconnection  ` . The location and project of the dataset and the connection must match.

``` text
CREATE FUNCTION mydataset.remoteMultiplyInputs(x FLOAT64, y FLOAT64)
RETURNS FLOAT64
REMOTE WITH CONNECTION us.myconnection
OPTIONS(endpoint="https://us-central1-myproject.cloudfunctions.net/multiply");
```

#### Create a Python UDF

The following example creates a Python UDF named `  multiplyInputs  ` .

``` text
CREATE FUNCTION mydataset.multiplyInputs(x FLOAT64, y FLOAT64)
RETURNS FLOAT64
LANGUAGE python
OPTIONS(entry_point='multiply', runtime_version='python-3.11' packages=['pandas==2.2'])
AS r"""
import pandas as pd

def multiply(df: pd.DataFrame):
  return df['x'] * df['y']

""";
```

## `     CREATE AGGREGATE FUNCTION    ` statement (SQL)

Creates a new SQL [user-defined aggregate function](/bigquery/docs/user-defined-aggregates) (UDAF).

### Syntax

To create a SQL UDAF, use the following syntax:

``` text
CREATE
  [ OR REPLACE ]
  [ { TEMPORARY | TEMP } ]
  AGGREGATE FUNCTION
  [ IF NOT EXISTS ]
  function_path ( [ function_parameter[, ...] ] )
  [ RETURNS data_type ]
  AS ( sql_function_body )
  [ OPTIONS ( function_option_list ) ]

function_path:
  [[project_name.]dataset_name.]function_name

function_parameter:
  parameter_name
  data_type
  [ NOT AGGREGATE ]
```

### Arguments

  - `  OR REPLACE  ` : Replaces any function with the same name if it exists. `  OR REPLACE  ` can't appear with `  IF NOT EXISTS  ` .
  - `  IF NOT EXISTS  ` : If any dataset exists with the same name, the `  CREATE  ` statement has no effect. `  IF NOT EXISTS  ` can't appear with `  OR REPLACE  ` .
  - `  TEMP  ` or `  TEMPORARY  ` : The function is temporary; that is, it exists for the lifetime of a single query, script, session, or procedure. A temporary function can't have the same name as a built-in function. If the names match, an error is produced. If `  TEMP  ` or `  TEMPORARY  ` is not included, a persistent function is created. You can reuse persistent functions across multiple queries.
  - `  function_path  ` : The path where the function must be created and the name of the function.
      - `  project_name  ` : For persistent functions, the name of the project where you are creating the function. Defaults to the project that runs the DDL query. Don't include the project name for temporary functions.
      - `  dataset_name  ` : For persistent functions, the name of the dataset where you are creating the function. Defaults to `  defaultDataset  ` in the request. Don't include the dataset name for temporary functions.
      - `  function_name  ` : The name of the function. Function names must contain only letters, numbers, and underscores, and be at most 256 characters long.
  - `  function_parameter  ` : A parameter for the function.
      - `  parameter_name  ` : The name of the function parameter.
      - `  parameter_data_type  ` : The GoogleSQL [data type](/bigquery/docs/reference/standard-sql/data-types) for the function parameter.
      - `  NOT AGGREGATE  ` : The function parameter is not an aggregate. A non-aggregate function parameter can appear anywhere in the function definition.
  - `  return_data_type  ` : The GoogleSQL data type that the function should return. GoogleSQL infers the result data type of the function from the function body when the `  RETURN  ` clause is omitted.
  - `  function_body  ` : The SQL expression that defines the function body.
  - `  function_option_list  ` : A list of options for creating the function. For more information, see [`  function_option_list  `](#sql-udaf-function-option-list) .

### `     function_option_list    `

The option list specifies options for creating a SQL UDAF. The following options are supported:

<table>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">       NAME      </code></th>
<th><code dir="ltr" translate="no">       VALUE      </code></th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       description      </code></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td>A description of the UDAF.</td>
</tr>
</tbody>
</table>

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.routines.create      </code></td>
<td>The dataset where you create the function.</td>
</tr>
</tbody>
</table>

In addition, the `  OR REPLACE  ` clause requires the `  bigquery.routines.update  ` permission.

### Examples

#### Create and call a SQL UDAF

The following example shows a persistent SQL UDAF that includes a non-aggregate function parameter. Inside the function definition, the aggregate `  SUM  ` method takes the aggregate function parameter dividend, while the non-aggregate division operator ( `  /  ` ) takes the non-aggregate function parameter divisor.

``` text
CREATE AGGREGATE FUNCTION myProject.myDataset.ScaledSum(
  dividend FLOAT64,
  divisor FLOAT64 NOT AGGREGATE)
RETURNS FLOAT64
AS (
  SUM(dividend) / divisor
);

-- Call the SQL UDAF.
SELECT ScaledSum(col1, 2) AS scaled_sum
FROM (
  SELECT 1 AS col1 UNION ALL
  SELECT 3 AS col1 UNION ALL
  SELECT 5 AS col1
);

/*------------*
 | scaled_sum |
 +------------+
 | 4.5        |
 *------------*/
```

## `     CREATE AGGREGATE FUNCTION    ` statement (JavaScript)

Creates a new [JavaScript user-defined aggregate function](/bigquery/docs/user-defined-aggregates) (UDAF).

### Syntax

To create a JavaScript UDAF, use the following syntax:

``` text
CREATE
  [ OR REPLACE ]
  [ { TEMPORARY | TEMP } ]
  AGGREGATE FUNCTION
  [ IF NOT EXISTS ]
  function_path([ function_parameter[, ...] ])
  RETURNS return_data_type
  LANGUAGE js
  [ OPTIONS ( function_option_list ) ]
  AS function_body

function_path:
  [[project_name.]dataset_name.]function_name

function_parameter:
  parameter_name parameter_data_type [ NOT AGGREGATE ]
```

### Arguments

  - `  OR REPLACE  ` : Replaces any function with the same name if it exists. `  OR REPLACE  ` can't appear with `  IF NOT EXISTS  ` .
  - `  IF NOT EXISTS  ` : If any dataset exists with the same name, the `  CREATE  ` statement has no effect. `  IF NOT EXISTS  ` can't appear with `  OR REPLACE  ` .
  - `  TEMP  ` or `  TEMPORARY  ` : The function is temporary; that is, it exists for the lifetime of a single query, script, session, or procedure. A temporary function can't have the same name as a built-in function. If the names match, an error is produced. If `  TEMP  ` or `  TEMPORARY  ` is not included, a persistent function is created. You can reuse persistent functions across multiple queries.
  - `  function_path  ` : The path where the function must be created and the name of the function.
      - `  project_name  ` : For persistent functions, the name of the project where you are creating the function. Defaults to the project that runs the DDL query. Don't include the project name for temporary functions.
      - `  dataset_name  ` : For persistent functions, the name of the dataset where you are creating the function. Defaults to `  defaultDataset  ` in the request. Don't include the dataset name for temporary functions.
      - `  function_name  ` : The name of the function. Function names must contain only letters, numbers, and underscores, and be at most 256 characters long.
  - `  function_parameter  ` : A parameter for the function.
      - `  parameter_name  ` : The name of the function parameter.
      - `  parameter_data_type  ` : The GoogleSQL [data type](/bigquery/docs/reference/standard-sql/data-types) for the function parameter.
      - `  NOT AGGREGATE  ` : The function parameter is not an aggregate. Only one non-aggregate function parameter is allowed per JavaScript UDAF, and it must be the last parameter in the list.
  - `  return_data_type  ` : The GoogleSQL data type that the function should return.
  - `  function_body  ` : The JavaScript expression that defines the function body. For more information, see [`  function_body  `](#javascript-udaf-function-body) .
  - `  function_option_list  ` : A list of options for creating the function. For more information, see [`  function_option_list  `](#javascript-udaf-function-option-list) .

### `     function_body    `

The body of the JavaScript function must be a quoted string literal that represents the JavaScript code. To learn more about the different types of quoted string literals you can use, see [Formats for quoted literals](/bigquery/docs/reference/standard-sql/lexical#quoted_literals) .

Only certain type encodings are allowed. To learn more, see [SQL type encodings in a JavaScript UDAF](#javascript-type-encodings-udaf) .

The JavaScript function body must include four JavaScript functions that initialize, aggregate, merge, and finalize the results for the JavaScript UDAF. To learn more about the `  initialState  ` , `  aggregate  ` , `  merge  ` , and `  finalize  ` JavaScript functions, see [Required aggregate functions in a JavaScript UDAF](#javascript-interface-functions-udaf) .

Only serialized data can be passed into the JavaScript aggregate functions. If you need to serialize data such as functions or symbols to pass them into the aggregate functions, use the JavaScript serialization functions. For more information, see [Serialization functions for a JavaScript UDAF](#javascript-serialization-functions-udaf) .

### `     function_option_list    `

The option list specifies options for creating a JavaScript UDAF. The following options are supported:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">       NAME      </code></th>
<th><code dir="ltr" translate="no">       VALUE      </code></th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       description      </code></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td>A description of the UDAF.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       library      </code></td>
<td><p><code dir="ltr" translate="no">        ARRAY&lt;STRING&gt;       </code></p></td>
<td><p>An array of JavaScript libraries to include in the JavaScript UDAF function body.</p>
<p>Example: <code dir="ltr" translate="no">        ["gs://my-bucket/lib1.js", "gs://my-bucket/lib2.js"]       </code></p></td>
</tr>
</tbody>
</table>

### SQL type encodings in a JavaScript UDAF

In JavaScript UDAFs, [GoogleSQL data types](/bigquery/docs/reference/standard-sql/data-types) represent [JavaScript data types](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects) in the following manner:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>GoogleSQL<br />
data type</th>
<th>JavaScript<br />
data type</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       ARRAY      </code></td>
<td><code dir="ltr" translate="no">       Array      </code></td>
<td>An array of arrays is not supported. To get around this limitation, use the <code dir="ltr" translate="no">       Array&lt;Object&lt;Array&gt;&gt;      </code> (JavaScript) and <code dir="ltr" translate="no">       ARRAY&lt;STRUCT&lt;ARRAY&gt;&gt;      </code> (GoogleSQL) data types.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
<td><code dir="ltr" translate="no">       Number      </code> or <code dir="ltr" translate="no">       String      </code></td>
<td>Same as <code dir="ltr" translate="no">       NUMERIC      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       BOOL      </code></td>
<td><code dir="ltr" translate="no">       Boolean      </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       BYTES      </code></td>
<td><code dir="ltr" translate="no">       Uint8Array      </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       DATE      </code></td>
<td><code dir="ltr" translate="no">       Date      </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
<td><code dir="ltr" translate="no">       Number      </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td><code dir="ltr" translate="no">       BigInt      </code></td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       JSON      </code></td>
<td>Various types</td>
<td>The GoogleSQL <code dir="ltr" translate="no">       JSON      </code> data type can be converted into a JavaScript <code dir="ltr" translate="no">       Object      </code> , <code dir="ltr" translate="no">       Array      </code> , or other GoogleSQL-supported JavaScript data type.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td><code dir="ltr" translate="no">       Number      </code> or <code dir="ltr" translate="no">       String      </code></td>
<td>If a <code dir="ltr" translate="no">       NUMERIC      </code> value can be represented exactly as an <a href="https://en.wikipedia.org/wiki/Floating-point_arithmetic#IEEE_754:_floating_point_in_modern_computers">IEEE 754 floating-point</a> value (range <code dir="ltr" translate="no">       [-2               53              , 2               53              ]      </code> ), and has no fractional part, it is encoded as a <code dir="ltr" translate="no">       Number      </code> data type, otherwise it is encoded as a <code dir="ltr" translate="no">       String      </code> data type.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><code dir="ltr" translate="no">       String      </code></td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       STRUCT      </code></td>
<td><code dir="ltr" translate="no">       Object      </code></td>
<td>Each <code dir="ltr" translate="no">       STRUCT      </code> field is a named property in the <code dir="ltr" translate="no">       Object      </code> data type. An unnamed <code dir="ltr" translate="no">       STRUCT      </code> field is not supported.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td><code dir="ltr" translate="no">       Date      </code></td>
<td><code dir="ltr" translate="no">       Date      </code> contains a microsecond field with the microsecond fraction of <code dir="ltr" translate="no">       TIMESTAMP      </code> .</td>
</tr>
</tbody>
</table>

**Note:** The SQL encodings for JavaScript UDAFs are different from those for JavaScript UDFs.

### Required aggregation functions in a JavaScript UDAF

The JavaScript function body must include the following exportable JavaScript functions:

  - `  initialState  ` function: Sets up the initial aggregation state of the UDAF and then returns the initial aggregation state.
    
    **Syntax:**
    
    ``` text
    export function initialState([nonAggregateParam]){...}
    ```
    
    **Parameters:**
    
      - `  nonAggregateParam  ` : Replace this parameter with a `  NOT AGGREGATE  ` function parameter name.
    
    **Examples:**
    
    ``` text
    export function initialState(){...}
    ```
    
    ``` text
    export function initialState(initialSum){...}
    ```

  - `  aggregate  ` function: Aggregates one row of data, updating state to store the result of the aggregation. Doesn't return a value.
    
    **Syntax:**
    
    ``` text
    export function aggregate(state, aggregateParam[, ...][, nonAggregateParam]){...}
    ```
    
    **Parameters:**
    
      - `  state  ` : The aggregate state, which is `  initialState  ` on the first invocation, and then the return value of the previous call to `  aggregate  ` thereafter.
    
      - `  aggregateParam  ` : The name of an aggregation parameter in the JavaScript UDAF. The argument for this parameter will be aggregated.
    
      - `  nonAggregateParam  ` : Replace with a `  NOT AGGREGATE  ` function parameter name.
    
    **Example:**
    
    ``` text
    export function aggregate(currentState, aggX, aggWeight, initialSum)
    ```

  - `  merge  ` function: Combines two aggregation states from a prior call to the `  aggregate  ` , `  merge  ` , or `  initialState  ` function. This function does not return a value.
    
    **Syntax:**
    
    ``` text
    export function merge(state, partialState[, nonAggregateParam]){...}
    ```
    
    **Parameters:**
    
      - `  state  ` : The state into which `  partialState  ` is merged.
    
      - `  partialState  ` : The second aggregation state to merge.
    
      - `  nonAggregateParam  ` : Replace with a `  NOT AGGREGATE  ` function parameter name.
    
    **Details:**
    
    Depending on the size and organization of the underlying data being queried, the `  merge  ` function might or might not be called. For example, if a particular set of data is small, or the data is partitioned in a way that results in small sets of data, the `  merge  ` function won't be called.
    
    **Example:**
    
    ``` text
    export function merge(currentState, partialState, initialSum)
    ```

  - `  finalize  ` function: Computes the final aggregation result and then returns this result for the UDAF.
    
    **Syntax:**
    
    ``` text
    export function finalize(state[, nonAggregateParam]){...}
    ```
    
    **Parameters:**
    
      - `  state  ` : The final aggregation state.
    
      - `  nonAggregateParam  ` : Replace with a `  NOT AGGREGATE  ` function parameter name.
    
    The final aggregation state is returned by the `  merge  ` function (or `  aggregate  ` function if `  merge  ` is never invoked). If the input is empty after `  NULL  ` filtering, the final aggregation state is `  initialState  ` .
    
    **Example:**
    
    ``` text
    export function finalize(finalState, initialSum)
    ```

### Serialization functions for a JavaScript UDAF

If you want to work with non-serializable aggregation states, the JavaScript UDAF must provide the `  serialize  ` and `  deserialize  ` functions:

  - `  serialize  ` function: Converts an aggregation state into a BigQuery-serializable object. An object in JavaScript is BigQuery-serializable if all fields are a JavaScript primitive data type (for example, `  String  ` , `  Number  ` , `  null  ` , `  undefined  ` ), another BigQuery-serializable object, or a JavaScript `  Array  ` , where all elements are either primitives or BigQuery-serializable objects.
    
    Syntax:
    
    ``` text
    export function serialize(state[, nonAggregateParam]){...}
    ```
    
    Arguments:
    
      - `  state  ` : The aggregation state to serialize.
    
      - `  nonAggregateParam  ` : Replace with a `  NOT AGGREGATE  ` function parameter name.
    
    Example:
    
    ``` text
    export function serialize(stateToSerialize, initialSum)
    ```

  - `  deserialize  ` function: Converts a serialized state into an aggregation state. An aggregated state can be passed into the `  serialize  ` , `  aggregate  ` , `  merge  ` , and `  finalize  ` functions.
    
    Syntax:
    
    ``` text
    export function deserialize(serializedState[, nonAggregateParam]){...}
    ```
    
    Arguments:
    
      - `  serializedState  ` : The serialized state to convert into the aggregation state.
    
      - `  nonAggregateParam  ` : Replace with a `  NOT AGGREGATE  ` function parameter name.
    
    Example:
    
    ``` text
    export function deserialize(stateToDeserialize, initialSum)
    ```

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.routines.create      </code></td>
<td>The dataset where you create the function.</td>
</tr>
</tbody>
</table>

In addition, the `  OR REPLACE  ` clause requires the `  bigquery.routines.update  ` permission.

### Examples

#### Calculate the positive sum of all rows

A JavaScript UDAF is similar to a JavaScript UDF, but defines an aggregate function instead of a scalar function. In the following example, a temporary JavaScript UDAF calculates the sum of all rows that have a positive value. The JavaScript UDAF body is quoted within a raw string:

``` text
CREATE TEMP AGGREGATE FUNCTION SumPositive(x FLOAT64)
RETURNS FLOAT64
LANGUAGE js
AS r'''
  export function initialState() {
    return {sum: 0}
  }
  export function aggregate(state, x) {
    if (x > 0) {
      state.sum += x;
    }
  }
  export function merge(state, partialState) {
    state.sum += partialState.sum;
  }
  export function finalize(state) {
    return state.sum;
  }
''';

-- Call the JavaScript UDAF.
WITH numbers AS (
  SELECT * FROM UNNEST([1.0, -1.0, 3.0, -3.0, 5.0, -5.0]) AS x)
SELECT SumPositive(x) AS sum
FROM numbers;

/*-----*
 | sum |
 +-----+
 | 9.0 |
 *-----*/
```

#### Get the weighted average of all rows

A JavaScript UDAF can have aggregate and non-aggregate parameters. In the following example, the JavaScript UDAF calculates the weighted average for `  x  ` after starting with an initial sum ( `  initialSum  ` ). `  x  ` and `  weight  ` are aggregate parameters, and `  initialSum  ` is a non-aggregate parameter:

``` text
CREATE OR REPLACE AGGREGATE FUNCTION my_project.my_dataset.WeightedAverage(
    x INT64,
    weight FLOAT64,
    initialSum FLOAT64 NOT AGGREGATE)
RETURNS INT64
LANGUAGE js
AS '''
   export function initialState(initialSum) {
     return {count: 0, sum: initialSum}
   }
   export function aggregate(state, x, weight) {
     state.count += 1;
     state.sum += Number(x) * weight;
   }
   export function merge(state, partialState) {
     state.sum += partialState.sum;
     state.count += partialState.count;
   }
   export function finalize(state) {
     return state.sum / state.count;
   }
''';

SELECT my_project.my_dataset.WeightedAverage(item, weight, 2) AS weighted_average
FROM (
  SELECT 1 AS item, 2.45 AS weight UNION ALL
  SELECT 3 AS item, 0.11 AS weight UNION ALL
  SELECT 5 AS item, 7.02 AS weight
);

/*------------------*
 | weighted_average |
 +------------------+
 | 13               |
 *------------------*/
```

## `     CREATE TABLE FUNCTION    ` statement

Creates a new [table function](/bigquery/docs/table-functions) , also called a *table-valued function* (TVF).

### Syntax

``` text
CREATE [ OR REPLACE ] TABLE FUNCTION [ IF NOT EXISTS ]
  [[project_name.]dataset_name.]function_name
  ( [ function_parameter [, ...] ] )
  [RETURNS TABLE < column_declaration [, ...] > ]
  [OPTIONS (table_function_options_list) ]
  AS sql_query

function_parameter:
  parameter_name { data_type | ANY TYPE | TABLE < column_declaration [, ...] > }

column_declaration:
  column_name data_type
```

### Arguments

  - `  OR REPLACE  ` : Replaces any table function with the same name if it exists. Cannot appear with `  IF NOT EXISTS  ` .
  - `  IF NOT EXISTS  ` : If any table function exists with the same name, the `  CREATE  ` statement has no effect. Cannot appear with `  OR REPLACE  ` .
  - `  project_name  ` : The name of the project where you are creating the function. Defaults to the project that runs this DDL statement.
  - `  dataset_name  ` : The name of the dataset where you are creating the function.
  - `  function_name  ` : The name of the function to create.
  - `  function_parameter  ` : A parameter for the function, specified as a parameter name and a data type. The value of `  data_type  ` is a scalar BigQuery [data type](/bigquery/docs/reference/standard-sql/data-types) or `  ANY TYPE  ` , or a table schema. Using [table parameters](/bigquery/docs/table-functions#table_parameters) in a table function is in [Preview](https://cloud.google.com/products#product-launch-stages) .
  - `  RETURNS TABLE  ` : The schema of the table that the function returns, specified as a comma-separated list of column name and data type pairs. If `  RETURNS TABLE  ` is absent, BigQuery infers the output schema from the query statement in the function body. If `  RETURNS TABLE  ` is included, the names in the returned table type must match column names from the SQL query.
  - `  sql_query  ` : Specifies the SQL query to run. The SQL query must include names for all columns.

### `     table_function_options_list    `

The `  table_function_options_list  ` lets you specify table function options. Table function options have the same syntax and requirements as table options but with a different list of `  NAME  ` s and `  VALUE  ` s:

<table>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">       NAME      </code></th>
<th><code dir="ltr" translate="no">       VALUE      </code></th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       description      </code></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td>The description of the table function.</td>
</tr>
</tbody>
</table>

### Details

BigQuery coerces argument types when possible. For example, if the parameter type is `  FLOAT64  ` and you pass an `  INT64  ` value, then BigQuery coerces it to a `  FLOAT64  ` .

If a parameter type is `  ANY TYPE  ` , the function accepts an input of any type for this argument. The type that you pass to the function must be compatible with the function definition. If you pass an argument with an incompatible type, the query returns an error. If more than one parameter has type `  ANY TYPE  ` , BigQuery does not enforce any type relationship between them. If the parameter type is a table schema, the function accepts an input table containing a superset of those columns in any order.

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.routines.create      </code></td>
<td>The dataset where you create the table function.</td>
</tr>
</tbody>
</table>

In addition, the `  OR REPLACE  ` clause requires `  bigquery.routines.update  ` permission.

### Examples

The following table function takes an `  INT64  ` parameter that is used to filter the results of a query:

``` text
CREATE OR REPLACE TABLE FUNCTION mydataset.names_by_year(y INT64)
AS
  SELECT year, name, SUM(number) AS total
  FROM `bigquery-public-data.usa_names.usa_1910_current`
  WHERE year = y
  GROUP BY year, name
```

The following example specifies the return `  TABLE  ` type in the `  RETURNS  ` clause:

``` text
CREATE OR REPLACE TABLE FUNCTION mydataset.names_by_year(y INT64)
RETURNS TABLE<name STRING, year INT64, total INT64>
AS
  SELECT year, name, SUM(number) AS total
  FROM `bigquery-public-data.usa_names.usa_1910_current`
  WHERE year = y
  GROUP BY year, name
```

The following example computes total sales for items with the name `  item_name  ` from the `  orders  ` table:

``` text
CREATE TABLE FUNCTION mydataset.compute_sales (
  orders TABLE<item STRING, sales INT64>, item_name STRING)
AS (
  SELECT SUM(sales) AS total_sales, item
  FROM orders
  WHERE item = item_name
  GROUP BY item
);
```

## `     CREATE PROCEDURE    ` statement

Creates a new [procedure](/bigquery/docs/procedures) , which is a block of statements that can be called from other queries. Procedures can call themselves recursively.

### Syntax

To create a [GoogleSQL stored procedure](/bigquery/docs/procedures) , use the following syntax:

``` text
CREATE [OR REPLACE] PROCEDURE [IF NOT EXISTS]
[[project_name.]dataset_name.]procedure_name (procedure_argument[, ...] )
[OPTIONS(procedure_option_list)]
BEGIN
multi_statement_query
END;

procedure_argument: [procedure_argument_mode] argument_name argument_type

procedure_argument_mode: IN | OUT | INOUT
```

To create a [stored procedure for Apache Spark](/bigquery/docs/spark-procedures) , use the following syntax:

``` text
CREATE [OR REPLACE] PROCEDURE [IF NOT EXISTS]
[[project_name.]dataset_name.]procedure_name (procedure_argument[, ...] )
[EXTERNAL SECURITY external_security]
WITH CONNECTION connection_project_id.connection_region.connection_id
[OPTIONS(procedure_option_list)]
LANGUAGE language [AS pyspark_code]

procedure_argument: [procedure_argument_mode] argument_name argument_type

procedure_argument_mode: IN | OUT | INOUT

external_security: INVOKER
```

### Arguments

  - `  OR REPLACE  ` : Replaces any procedure with the same name if it exists. Cannot appear with `  IF NOT EXISTS  ` .

  - `  IF NOT EXISTS  ` : If any procedure exists with the same name, the `  CREATE  ` statement has no effect. Cannot appear with `  OR REPLACE  ` .

  - `  project_name  ` : The name of the project where you are creating the procedure. Defaults to the project that runs this DDL query. If the project name contains special characters such as colons, it should be quoted in backticks ``  `  `` (example: ``  `google.com:my_project`  `` ).

  - `  dataset_name  ` : The name of the dataset where you are creating the procedure. Defaults to the `  defaultDataset  ` in the request.

  - `  procedure_name  ` : The name of the procedure to create.

  - `  external_security  ` : The procedure to be executed with the privileges of the user that calls it.

  - `  connection_project_id  ` : the project that contains the [connection](/bigquery/docs/connect-to-spark) to run Spark procedures—for example, `  myproject  ` .

  - `  connection_region  ` : the region that contains the connection to run Spark procedures—for example, `  us  ` .

  - `  connection_id  ` : the connection ID—for example, `  myconnection  ` .
    
    When you [view the connection details](/bigquery/docs/working-with-connections#view-connections) in the Google Cloud console, the connection ID is the value in the last section of the fully qualified connection ID that is shown in **Connection ID** —for example `  projects/myproject/locations/connection_location/connections/ myconnection  ` .
    
    For more information, see [Create a stored procedure for Apache Spark](/bigquery/docs/spark-procedures#create-spark-procedure) .

  - `  multi_statement_query  ` : The [multi-statement query](/bigquery/docs/multi-statement-queries) to run.

  - `  language  ` : The language in which the stored procedure for Apache Spark is written. BigQuery supports stored procedures for Apache Spark that are written in Python, Java, or Scala.

  - `  pyspark_code  ` : The PySpark code for the stored procedure for Apache Spark if you want to pass the body of the procedure inline. Cannot appear with `  main_file_uri  ` in [`  procedure_option_list  `](#procedure_option_list) .

  - `  argument_type  ` : Any valid BigQuery [type](/bigquery/docs/reference/standard-sql/data-types) .

  - `  procedure_argument_mode  ` : Specifies whether an argument is an input, an output, or both.

### `     procedure_option_list    `

The `  procedure_option_list  ` lets you specify procedure options. Procedure options have the same syntax and requirements as table options but with a different list of `  NAME  ` s and `  VALUE  ` s:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">       NAME      </code></th>
<th><code dir="ltr" translate="no">       VALUE      </code></th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       strict_mode      </code></td>
<td><p><code dir="ltr" translate="no">        BOOL       </code></p></td>
<td>It is useful for catching many common types of errors. The errors are not exhaustive, and successful creation of a procedure with <code dir="ltr" translate="no">       strict_mode      </code> doesn't guarantee that the procedure will successfully execute at runtime.
<p>If <code dir="ltr" translate="no">        strict_mode       </code> is <code dir="ltr" translate="no">        TRUE       </code> , the procedure body undergoes additional checks for errors such as non-existent tables or columns. The <code dir="ltr" translate="no">        CREATE PROCEDURE       </code> statement fails if the body fails any of these checks.</p>
<p>If <code dir="ltr" translate="no">        strict_mode       </code> is <code dir="ltr" translate="no">        FALSE       </code> , the procedure body is checked only for syntax. Procedures which invoke themselves recursively should be created with <code dir="ltr" translate="no">        strict_mode=FALSE       </code> to avoid errors caused by the procedure not yet existing while it is being validated.</p>
<p>Default value is <code dir="ltr" translate="no">        TRUE       </code> .</p>
Example: <code dir="ltr" translate="no">       strict_mode=FALSE      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       description      </code></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td>A description of the procedure.<br />
Example: <code dir="ltr" translate="no">       description="A procedure that runs a query."      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       engine      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><p>The engine type for processing stored procedures for Apache Spark. Must be specified for stored procedures for Spark.</p>
Valid value: <code dir="ltr" translate="no">       engine="SPARK"      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       runtime_version      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><p>The runtime version of stored procedures for Spark.</p>
<p>If not specified, the system default runtime version is used. Stored procedures for Spark support the same list of runtime versions as Serverless for Apache Spark. However, we recommend to specify a runtime version. For more information, see <a href="/dataproc-serverless/docs/concepts/versions/spark-runtime-versions">Serverless for Apache Spark runtime releases</a> .</p>
Example: <code dir="ltr" translate="no">       runtime_version="1.1"      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       container_image      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><p>Custom container image for the runtime environment of the stored procedure for Spark.</p>
<p>If not specified, the system default container image that includes the default Spark, Java, and Python packages associated with a runtime version is used.</p>
<p>You can provide a custom container Docker image that includes your own built Java or Python dependencies. As Spark is mounted into your custom container at runtime, you must omit Spark in your custom container image.</p>
<p>For optimized performance, we recommend you to host your image in Artifact Registry. For more information, see <a href="/dataproc-serverless/docs/guides/custom-containers">Use custom containers with Serverless for Apache Spark</a> .</p>
<p>Example: <code dir="ltr" translate="no">        container_image="us-docker.pkg.dev/my-project-id/my-images/my-image”       </code></p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       properties      </code></td>
<td><code dir="ltr" translate="no">       ARRAY&lt;STRUCT&lt;STRING, STRING&gt;&gt;      </code></td>
<td><p>A key-value pair to include properties for stored procedures for Spark.</p>
<p>Stored procedures for Spark support most of the <a href="https://spark.apache.org/docs/latest/configuration.html#spark-properties" class="external">Spark properties</a> and a list of <a href="/dataproc-serverless/docs/concepts/properties#custom_spark_properties">Serverless for Apache Spark properties</a> . If you specify unsupported Spark properties such as YARN-related Spark properties, BigQuery fails to create the stored procedure. You can add Spark properties using the following format: <code dir="ltr" translate="no">        [("key1","value1"),("key2", "value2")]       </code></p>
For example:
<pre class="text" dir="ltr" data-is-upgraded="" data-syntax="Bash" translate="no"><code>bq query --nouse_legacy_sql --dry_run
&#39;CREATE PROCEDURE my_bq_project.my_dataset.spark_proc()
WITH CONNECTION `my-project-id.us.my-connection`
OPTIONS(
engine=&quot;SPARK&quot;,
main_file_uri=&quot;gs://my-bucket/my-pyspark-main.py&quot;,
properties=[
(&quot;spark.executor.instances&quot;, &quot;3&quot;),
(&quot;spark.yarn.am.memory&quot;, &quot;3g&quot;)
])
LANGUAGE PYTHON&#39;

# Error in query string: Invalid value: \
Invalid properties: \
Attempted to set unsupported properties: \
[spark:spark.yarn.am.memory] at [1:1]</code></pre>
<strong>Note:</strong> You can use the <a href="/bigquery/docs/running-queries#dry-run">BigQuery dry run feature</a> to validate your stored procedure without creating it.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       main_file_uri      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><p>The Cloud Storage URI of the main Python, Scala, or Java JAR file of the Spark application. Applies only to stored procedures for Spark.</p>
<p>Alternatively, if you want to add the body of the stored procedure that's written in Python in the <code dir="ltr" translate="no">        CREATE PROCEDURE       </code> statement, add the code after <code dir="ltr" translate="no">        LANGUAGE PYTHON AS       </code> as shown in the example in <a href="/bigquery/docs/spark-procedures#use-inline-code">Use inline code</a> .</p>
Example: <code dir="ltr" translate="no">       main_file_uri="gs://my-bucket/my-pyspark-main.py"      </code>
<p>For Scala and Java languages, this field contains a path to only one JAR file. You can set only one value for <code dir="ltr" translate="no">        main_file_uri       </code> and <code dir="ltr" translate="no">        main_class       </code> .</p>
Example: <code dir="ltr" translate="no">       main_file_uri="gs://my-bucket/my-scala-main.jar"      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       main_class      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><p>Applies only to stored procedures for Spark written in Java and Scala. Specify a fully-qualified class name in a JAR set with the <code dir="ltr" translate="no">        jar_uris       </code> option. You can set only one value for <code dir="ltr" translate="no">        main_file_uri       </code> and <code dir="ltr" translate="no">        main_class       </code> .</p>
Example: <code dir="ltr" translate="no">       main_class=”com.example.wordcount”      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       py_file_uris      </code></td>
<td><code dir="ltr" translate="no">       ARRAY&lt;STRING&gt;      </code></td>
<td><p>Python files to be placed on the <code dir="ltr" translate="no">        PYTHONPATH       </code> for a PySpark application. Applies only to stored procedures for Apache Spark written in Python.</p>
<p>Optional. Cloud Storage URIs of Python files to pass to the PySpark framework. Supported file formats include the following: <code dir="ltr" translate="no">        .py       </code> , <code dir="ltr" translate="no">        .egg       </code> , and <code dir="ltr" translate="no">        .zip       </code> .</p>
Example: <code dir="ltr" translate="no">       py_file_uris=[ "gs://my-bucket/my-pyspark-file1.py",         "gs://my-bucket/my-pyspark-file2.py" ]      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       jar_uris      </code></td>
<td><code dir="ltr" translate="no">       ARRAY&lt;STRING&gt;      </code></td>
<td><p>Path to the JAR files to include on the driver and executor classpaths. Applies only to stored procedures for Apache Spark.</p>
<p>Optional. Cloud Storage URIs of JAR files to add to the classpath of the Spark driver and tasks.</p>
Example:<br />
<code dir="ltr" translate="no">       jar_uris=["gs://my-bucket/my-lib1.jar",         "gs://my-bucket/my-lib2.jar"]      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       file_uris      </code></td>
<td><code dir="ltr" translate="no">       ARRAY&lt;STRING&gt;      </code></td>
<td><p>Files to be placed in the working directory of each executor. Applies only to stored procedures for Apache Spark.</p>
Optional. Cloud Storage URIs of files to be placed in the working directory of each executor. Example:<br />
<code dir="ltr" translate="no">       file_uris=["gs://my-bucket/my-file1",       "gs://my-bucket/my-file2"]      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       archive_uris      </code></td>
<td><code dir="ltr" translate="no">       ARRAY&lt;STRING&gt;      </code></td>
<td><p>Archive files to be extracted into the working directory of each executor. Applies only to stored procedures for Apache Spark.</p>
<p>Optional. Cloud Storage URIs of archives to be extracted into the working directory of each executor. Supported file formats include the following: <code dir="ltr" translate="no">        .jar       </code> , <code dir="ltr" translate="no">        .tar       </code> , <code dir="ltr" translate="no">        .tar.gz       </code> , <code dir="ltr" translate="no">        .tgz       </code> , and <code dir="ltr" translate="no">        .zip       </code> .</p>
Example:<br />
<code dir="ltr" translate="no">       archive_uris=["gs://my-bucket/my-archive1.zip",      "gs://my-bucket/my-archive2.zip"]      </code></td>
</tr>
</tbody>
</table>

#### Argument mode

`  IN  ` indicates that the argument is only an input to the procedure. You can specify either a variable or a value expression for `  IN  ` arguments.

`  OUT  ` indicates that the argument is an output of the procedure. An `  OUT  ` argument is initialized to `  NULL  ` when the procedure starts. You must specify a variable for `  OUT  ` arguments.

`  INOUT  ` indicates that the argument is both an input to and an output from the procedure. You must specify a variable for `  INOUT  ` arguments. An `  INOUT  ` argument can be referenced in the body of a procedure as a variable and assigned new values.

If neither `  IN  ` , `  OUT  ` , nor `  INOUT  ` is specified, the argument is treated as an `  IN  ` argument.

#### Variable scope

If a variable is declared outside a procedure, passed as an INOUT or OUT argument to a procedure, and the procedure assigns a new value to that variable, that new value is visible outside of the procedure.

Variables declared in a procedure are not visible outside of the procedure, and vice versa.

An `  OUT  ` or `  INOUT  ` argument can be assigned a value using `  SET  ` , in which case the modified value is visible outside of the procedure. If the procedure exits successfully, then the value of the `  OUT  ` or `  INOUT  ` argument is the final value assigned to that `  INOUT  ` variable.

[Temporary tables](#create-table-statement) exist for the duration of the script, so if a procedure creates a temporary table, the caller of the procedure will be able to reference the temporary table as well.

### Default project in procedure body

Procedure bodies can reference entities without specifying the project; the default project is the project which owns the procedure, not necessarily the project used to run the `  CREATE PROCEDURE  ` statement. Consider the sample query below.

``` text
CREATE PROCEDURE myProject.myDataset.QueryTable()
BEGIN
  SELECT * FROM anotherDataset.myTable;
END;
```

After creating the above procedure, you can run the query `  CALL myProject.myDataset.QueryTable()  ` . Regardless of the project you choose to run this `  CALL  ` query, the referenced table `  anotherDataset.myTable  ` is always resolved against project `  myProject  ` .

### Required permissions

This statement requires the following [IAM permission](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.routines.create      </code></td>
<td>The dataset where you create the procedure.</td>
</tr>
</tbody>
</table>

To create a stored procedure for Apache Spark, additional [IAM permission](/bigquery/docs/access-control#bq-permissions) are needed:

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.connections.delegate      </code></td>
<td>The connection which you use to <a href="/bigquery/docs/spark-procedures#create-spark-procedure">create the stored procedure for Apache Spark</a> .</td>
</tr>
</tbody>
</table>

In addition, the `  OR REPLACE  ` clause requires `  bigquery.routines.update  ` permission.

### SQL examples

You can also see [examples of stored procedures for Apache Spark](/bigquery/docs/spark-procedures#example-spark-procedure) .

The following example creates a SQL procedure that both takes `  x  ` as an input argument and returns `  x  ` as output; because no argument mode is present for the argument `  delta  ` , it is an input argument. The procedure consists of a block containing a single statement, which assigns the sum of the two input arguments to `  x  ` .

``` text
CREATE PROCEDURE mydataset.AddDelta(INOUT x INT64, delta INT64)
BEGIN
  SET x = x + delta;
END;
```

The following example calls the `  AddDelta  ` procedure from the example above, passing it the variable `  accumulator  ` both times; because the changes to `  x  ` within `  AddDelta  ` are visible outside of `  AddDelta  ` , these procedure calls increment `  accumulator  ` by a total of 8.

``` text
DECLARE accumulator INT64 DEFAULT 0;
CALL mydataset.AddDelta(accumulator, 5);
CALL mydataset.AddDelta(accumulator, 3);
SELECT accumulator;
```

This returns the following:

``` text
+-------------+
| accumulator |
+-------------+
|           8 |
+-------------+
```

The following example creates the procedure `  SelectFromTablesAndAppend  ` , which takes `  target_date  ` as an input argument and returns `  rows_added  ` as an output. The procedure creates a temporary table `  DataForTargetDate  ` from a query; then, it calculates the number of rows in `  DataForTargetDate  ` and assigns the result to `  rows_added  ` . Next, it inserts a new row into `  TargetTable  ` , passing the value of `  target_date  ` as one of the column names. Finally, it drops the table `  DataForTargetDate  ` and returns `  rows_added  ` .

``` text
CREATE PROCEDURE mydataset.SelectFromTablesAndAppend(
  target_date DATE, OUT rows_added INT64)
BEGIN
  CREATE TEMP TABLE DataForTargetDate AS
  SELECT t1.id, t1.x, t2.y
  FROM dataset.partitioned_table1 AS t1
  JOIN dataset.partitioned_table2 AS t2
  ON t1.id = t2.id
  WHERE t1.date = target_date
    AND t2.date = target_date;

  SET rows_added = (SELECT COUNT(*) FROM DataForTargetDate);

  SELECT id, x, y, target_date  -- note that target_date is a parameter
  FROM DataForTargetDate;

  DROP TABLE DataForTargetDate;
END;
```

The following example declares a variable `  rows_added  ` , then passes it as an argument to the `  SelectFromTablesAndAppend  ` procedure from the previous example, along with the value of `  CURRENT_DATE  ` ; then it returns a message stating how many rows were added.

``` text
DECLARE rows_added INT64;
CALL mydataset.SelectFromTablesAndAppend(CURRENT_DATE(), rows_added);
SELECT FORMAT('Added %d rows', rows_added);
```

## `     CREATE ROW ACCESS POLICY    ` statement

Creates or replaces a [row-level access policy](/bigquery/docs/row-level-security-intro) . Row-level access policies on a table must have unique names.

### Syntax

``` text
CREATE [ OR REPLACE ] ROW ACCESS POLICY [ IF NOT EXISTS ]
row_access_policy_name ON table_name
[GRANT TO (grantee_list)]
FILTER USING (filter_expression);
```

### Arguments

  - `  IF NOT EXISTS  ` : If any row-level access policy exists with the same name, the `  CREATE  ` statement has no effect. Cannot appear with `  OR REPLACE  ` .

  - `  row_access_policy_name  ` : The name of the row-level access policy that you are creating. The row-level access policy name must be unique for each table. The row-level access policy name can contain the following:
    
      - Up to 256 characters.
      - Letters (upper or lowercase), numbers, and underscores. Must start with a letter.

  - `  table_name  ` : The name of the table that you want to create a row-level access policy for. The table must already exist.

  - `  GRANT TO grantee_list  ` : An optional clause that specifies the initial members that the row-level access policy should be created with.
    
    **Caution:** If no `  grantee_list  ` is provided, then the row-level access policy for the specified filter is initialized with no principals. This configuration prevents all data reads by everyone.
    
    `  grantee_list  ` is a list of `  iam_member  ` users or groups. Strings must be valid [IAM principals](/iam/docs/overview#concepts_related_identity) , or members, following the format of an [IAM Policy Binding member](/iam/docs/reference/rest/v1/Binding) , and must be quoted. The following types are supported:
    
    Example: `  user:alice@example.com  `
    
    `  grantee_list  ` types

  - `  filter_expression  ` : Defines the subset of table rows to show only to the members of the `  grantee_list  ` . The `  filter_expression  ` is similar to the `  WHERE  ` clause in a `  SELECT  ` query.
    
    The following are valid filter expressions:
    
      - GoogleSQL scalar functions.
      - `  SESSION_USER()  ` , to restrict access only to rows that belong to the user running the query. If none of the row-level access policies are applicable to the querying user, then the user has no access to the data in the table.
      - `  TRUE  ` . Grants the principals in the `  grantee_list  ` field access to all rows of the table.
    
    The filter expression cannot contain the following:
    
      - References to other tables, such as [subqueries](/bigquery/docs/reference/standard-sql/subqueries) .
      - SQL statements such as `  SELECT  ` , `  CREATE  ` , or `  UPDATE  ` .
      - User-defined functions.

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.rowAccessPolicies.create      </code></td>
<td>The target table.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigquery.rowAccessPolicies.setIamPolicy      </code></td>
<td>The target table.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.tables.getData      </code></td>
<td>The target table.</td>
</tr>
</tbody>
</table>

## `     CREATE CAPACITY    ` statement

Purchases [slots](/bigquery/docs/slots) by creating a new capacity commitment.

**Caution:** Before you purchase slots, understand the details of the [commitment plans](/bigquery/docs/reservations-workload-management#slot_commitments) and [pricing](https://cloud.google.com/bigquery/pricing#on_demand_pricing) .

### Syntax

``` text
CREATE CAPACITY
`project_id.location_id.commitment_id`
OPTIONS (capacity_commitment_option_list);
```

### Arguments

  - `  project_id  ` : The project ID of the administration project that will maintain ownership of this commitment.
  - `  location_id  ` : The [location](/bigquery/docs/locations#supported_locations) of the commitment.
  - `  commitment_id  ` : The ID of the commitment. The value must be unique to the project and location. It must start and end with a lowercase letter or a number and contain only lowercase letters, numbers and dashes.
  - [`  capacity_commitment_option_list  `](#capacity_commitment_option_list) : The options you can set to describe the capacity commitment.

### `     capacity_commitment_option_list    `

The option list specifies options for the capacity commitment. Specify the options in the following format: `  NAME=VALUE, ...  `

The following options are supported:

<table>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">       NAME      </code></th>
<th><code dir="ltr" translate="no">       TYPE      </code></th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       plan      </code></td>
<td>String</td>
<td>The commitment plan to purchase. Supported values include: <code dir="ltr" translate="no">       ANNUAL      </code> , <code dir="ltr" translate="no">       THREE_YEAR      </code> , and <code dir="ltr" translate="no">       TRIAL      </code> . For more information, see <a href="/bigquery/docs/reservations-workload-management#slot_commitments">Commitment plans</a> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       renewal_plan      </code></td>
<td>String</td>
<td>The commitment renewal plan. Applies only when <code dir="ltr" translate="no">       plan      </code> is <code dir="ltr" translate="no">       ANNUAL      </code> , <code dir="ltr" translate="no">       THREE_YEAR      </code> , or <code dir="ltr" translate="no">       TRIAL      </code> . For more information, see <a href="/bigquery/docs/reservations-workload-management#renew-commitments">Renewing commitments</a> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       slot_count      </code></td>
<td>Integer</td>
<td>The number of slots in the commitment.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       edition      </code></td>
<td>String</td>
<td>The edition associated with this reservation. For more information about editions, see <a href="/bigquery/docs/editions-intro">Introduction to BigQuery editions</a> .</td>
</tr>
</tbody>
</table>

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.capacityCommitments.create      </code></td>
<td>The administration project that maintains ownership of the commitments.</td>
</tr>
</tbody>
</table>

### Example

The following example creates a capacity commitment of 100 annual slots that are located in the `  region-us  ` region and managed by a project `  admin_project  ` :

``` text
CREATE CAPACITY `admin_project.region-us.my-commitment`
OPTIONS (
  slot_count = 100,
  plan = 'ANNUAL');
```

## `     CREATE RESERVATION    ` statement

Creates a reservation. For more information, see [Introduction to Reservations](/bigquery/docs/reservations-intro) .

### Syntax

``` text
CREATE RESERVATION
`project_id.location_id.reservation_id`
OPTIONS (reservation_option_list);
```

### Arguments

  - `  project_id  ` : The project ID of the administration project where the capacity commitment was created.
  - `  location  ` : The [location](/bigquery/docs/locations#supported_locations) of the reservation.
  - `  reservation_id  ` : The reservation ID.
  - [`  reservation_option_list  `](#reservation_option_list) : The options you can set to describe the reservation.

#### `     reservation_option_list    `

The option list specifies options for the dataset. Specify the options in the following format: `  NAME=VALUE, ...  `

The following options are supported:

<table>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">       NAME      </code></th>
<th><code dir="ltr" translate="no">       TYPE      </code></th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       ignore_idle_slots      </code></td>
<td><code dir="ltr" translate="no">       BOOLEAN      </code></td>
<td>If the value is <code dir="ltr" translate="no">       true      </code> , then the reservation uses only the slots that are provisioned to it. The default value is <code dir="ltr" translate="no">       false      </code> . For more information, see <a href="/bigquery/docs/slots#idle_slots">Idle slots</a> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       slot_capacity      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>The number of slots to allocate to the reservation. If this reservation was created with an <a href="/bigquery/docs/editions-intro">edition</a> , this is equivalent to the amount of <a href="/bigquery/docs/slots-autoscaling-intro#using_reservations_with_baseline_and_autoscaling_slots">baseline slots</a> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       target_job_concurrency      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>A soft upper bound on the number of jobs that can run concurrently in this reservation.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       edition      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The edition associated with this reservation. For more information about editions, see <a href="/bigquery/docs/editions-intro">Introduction to BigQuery editions</a> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       autoscale_max_slots      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>The maximum number of slots that could be added to the reservation by autoscaling.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       secondary_location      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The secondary location to use in the case of disaster recovery.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       max_slots      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>The maximum number of slots the reservation can consume. For more details about predictable reservations, see <a href="/bigquery/docs/reservations-workload-management#predictable">Reservation predictability</a> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       scaling_mode      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The scaling mode of the reservation. This value must be configured together with <code dir="ltr" translate="no">       max_slots      </code> . Also, this value must be aligned with <code dir="ltr" translate="no">       ignore_idle_slots      </code> . For details, see <a href="/bigquery/docs/reservations-workload-management#predictable">Reservation predictability</a> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       labels      </code></td>
<td><code dir="ltr" translate="no">       &lt;ARRAY&lt;STRUCT&lt;STRING, STRING&gt;&gt;&gt;      </code></td>
<td>An array of labels for the reservation, expressed as key-value pairs.</td>
</tr>
</tbody>
</table>

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.reservations.create      </code></td>
<td>The administration project that maintains ownership of the commitments.</td>
</tr>
</tbody>
</table>

### Example

The following example creates a reservation of 100 slots in the project `  admin_project  ` :

``` text
CREATE RESERVATION `admin_project.region-us.prod`
OPTIONS (
  slot_capacity = 100);
```

## `     CREATE ASSIGNMENT    ` statement

Assigns a project, folder, or organization to a reservation.

### Syntax

``` text
CREATE ASSIGNMENT
`project_id.location_id.reservation_id.assignment_id`
OPTIONS (assignment_option_list)
```

### Arguments

  - `  project_id  ` : The project ID of the administration project where the reservation was created.
  - `  location  ` : The [location](/bigquery/docs/locations#supported_locations) of the reservation.
  - `  reservation_id  ` : The reservation ID.
  - `  assignment_id  ` : The ID of the assignment. The value must be unique to the project and location. It must start and end with a lowercase letter or a number and contain only lowercase letters, numbers and dashes.
  - [`  assignment_option_list  `](#assignment_option_list) : The options you can set to describe assignment.

To remove a project from any reservations and use on-demand billing instead, set `  reservation_id  ` to `  none  ` .

### `     assignment_option_list    `

The option list specifies options for the dataset. Specify the options in the following format: `  NAME=VALUE, ...  `

The following options are supported:

<table>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">       NAME      </code></th>
<th><code dir="ltr" translate="no">       TYPE      </code></th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       assignee      </code></td>
<td>String</td>
<td>The ID of the project, folder, or organization to assign to the reservation.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       job_type      </code></td>
<td>String</td>
<td>The type of job to assign to this reservation. Supported values include <code dir="ltr" translate="no">       QUERY      </code> , <code dir="ltr" translate="no">       PIPELINE      </code> , <code dir="ltr" translate="no">       ML_EXTERNAL      </code> , <code dir="ltr" translate="no">       CONTINUOUS      </code> , and <code dir="ltr" translate="no">       BACKGROUND      </code> . For more information, see <a href="/bigquery/docs/reservations-workload-management#assignments">Reservation assignments</a> .</td>
</tr>
</tbody>
</table>

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.reservationAssignments.create      </code></td>
<td>The administration project and the assignee.</td>
</tr>
</tbody>
</table>

### Example

The following example assigns the project `  my_project  ` to the `  prod  ` reservation for query jobs:

``` text
CREATE ASSIGNMENT `admin_project.region-us.prod.my_assignment`
OPTIONS (
  assignee = 'projects/my_project',
  job_type = 'QUERY');
```

The following example assigns an organization to the `  prod  ` reservation for pipeline jobs, such as load and extract jobs:

``` text
CREATE ASSIGNMENT `admin_project.region-us.prod.my_assignment`
OPTIONS (
  assignee = 'organizations/1234',
  job_type = 'PIPELINE');
```

## `     CREATE SEARCH INDEX    ` statement

Creates a new [search index](/bigquery/docs/search-index) on one or more columns of a table.

A search index enables efficient queries using the [`  SEARCH  `](/bigquery/docs/reference/standard-sql/search_functions#search) function.

### Syntax

``` text
CREATE SEARCH INDEX [ IF NOT EXISTS ] index_name
ON table_name({ALL COLUMNS [WITH COLUMN OPTIONS(column [, ...])] | column [, ...]})
[OPTIONS(index_option_list)]

column:=
column_name [OPTIONS(index_column_option_list)]
```

### Arguments

  - `  IF NOT EXISTS  ` : If there is already a search index by that name on the table, do nothing. If the table has a search index by a different name, then return an error.

  - `  index_name  ` : The name of the search index you're creating. Since the search index is always created in the same project and dataset as the base table, there is no need to specify these in the name.

  - `  table_name  ` : The name of the table. See [Table path syntax](#table_path) .

  - `  ALL COLUMNS  ` : If data types are not specified, creates a search index on every column in the table which contains a `  STRING  ` field. If data types are specified, create a search index on every column in the table which matches any of the data types specified.

  - `  WITH COLUMN OPTIONS  ` : Can only be used with `  ALL COLUMNS  ` to set options on specific indexed columns.

  - `  column_name  ` : The name of a top-level column in the table which is one of the following supported data types or contains a field with one of the supported data types:
    
    <table>
    <thead>
    <tr class="header">
    <th>Supported data types</th>
    <th>Notes</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><code dir="ltr" translate="no">         STRING        </code></td>
    <td>Primitive data type.</td>
    </tr>
    <tr class="even">
    <td><code dir="ltr" translate="no">         INT64        </code></td>
    <td>Primitive data type.</td>
    </tr>
    <tr class="odd">
    <td><code dir="ltr" translate="no">         TIMESTAMP        </code></td>
    <td>Primitive data type.</td>
    </tr>
    <tr class="even">
    <td><code dir="ltr" translate="no">         ARRAY&lt;PRIMITIVE_DATA_TYPE&gt;        </code></td>
    <td>Must contain a primitive data type in this list.</td>
    </tr>
    <tr class="odd">
    <td><code dir="ltr" translate="no">         STRUCT        </code> or <code dir="ltr" translate="no">         ARRAY&lt;STRUCT&gt;        </code></td>
    <td>Must contain at least one nested field that is a primitive data type in this list or <code dir="ltr" translate="no">         ARRAY&lt;PRIMITIVE_DATA_TYPE&gt;        </code> .</td>
    </tr>
    <tr class="even">
    <td><code dir="ltr" translate="no">         JSON        </code></td>
    <td>Must contain at least one nested field of a type that matches any data types in this list.</td>
    </tr>
    </tbody>
    </table>

  - [`  index_column_option_list  `](#index_column_option_list) : The list of options to set on indexed columns.

  - [`  index_option_list  `](#index_option_list) : The list of options to set on the search index.

### Details

You can create only one search index per base table. You cannot create a search index on a view or materialized view. To modify which columns are indexed, [`  DROP  `](#drop_search_index) the current index and create a new one.

BigQuery returns an error if any `  column_name  ` is not a `  STRING  ` or does not contain a `  STRING  ` field, or if you call `  CREATE SEARCH INDEX  ` on `  ALL COLUMNS  ` of a table which contains no `  STRING  ` fields.

Creating a search index fails on a table which has column ACLs or row filters; however, these may all be added to the table after creation of the index.

### `     index_option_list    `

The option list specifies options for the search index. Specify the options in the following format: `  NAME=VALUE, ...  `

The following options are supported:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">       NAME      </code></th>
<th><code dir="ltr" translate="no">       VALUE      </code></th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       analyzer      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><p>Example: <code dir="ltr" translate="no">        analyzer='LOG_ANALYZER'       </code></p>
<p>The <a href="/bigquery/docs/reference/standard-sql/text-analysis">text analyzer</a> to use to generate tokens for the search index. The supported values are <code dir="ltr" translate="no">        'LOG_ANALYZER'       </code> , <code dir="ltr" translate="no">        'NO_OP_ANALYZER'       </code> , and <code dir="ltr" translate="no">        'PATTERN_ANALYZER'       </code> .</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       analyzer_options      </code></td>
<td><code dir="ltr" translate="no">       JSON-formatted STRING      </code></td>
<td>The text analyzer configurations to set when creating a search index. Supported when <code dir="ltr" translate="no">       analyzer      </code> is equal to <code dir="ltr" translate="no">       'LOG_ANALYZER'      </code> or <code dir="ltr" translate="no">       'PATTERN_ANALYZER'      </code> . For examples of JSON-formatted strings with different text analyzers, see <a href="/bigquery/docs/text-analysis-search">Work with text analyzers</a> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       data_types      </code></td>
<td><code dir="ltr" translate="no">       ARRAY&lt;STRING&gt;      </code></td>
<td><p>Example: <code dir="ltr" translate="no">        data_types=['STRING', 'INT64', 'TIMESTAMP']       </code></p>
<p>An array of data types to set when creating a search index. Supported data types are <code dir="ltr" translate="no">        STRING       </code> , <code dir="ltr" translate="no">        INT64       </code> and <code dir="ltr" translate="no">        TIMESTAMP       </code> . If <code dir="ltr" translate="no">        data_types       </code> is not set, <code dir="ltr" translate="no">        STRING       </code> fields are indexed by default.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       default_index_column_granularity      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><p>In <a href="https://cloud.google.com/products#product-launch-stages">Preview</a> .</p>
<p>Example: <code dir="ltr" translate="no">        default_index_column_granularity='GLOBAL'       </code></p>
<p>The default granularity of information to store for each indexed column. The supported values are <code dir="ltr" translate="no">        'GLOBAL'       </code> (default) and <code dir="ltr" translate="no">        'COLUMN'       </code> . For more information, see <a href="/bigquery/docs/search-index#column-granularity">Index with column granularity</a> .</p></td>
</tr>
</tbody>
</table>

### `     index_column_option_list    `

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">       NAME      </code></th>
<th><code dir="ltr" translate="no">       VALUE      </code></th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       index_granularity      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><p>In <a href="https://cloud.google.com/products#product-launch-stages">Preview</a> .</p>
<p>Example: <code dir="ltr" translate="no">        index_granularity='GLOBAL'       </code></p>
<p>The granularity of information to store for the indexed column. This setting overrides the default granularity specified in the <code dir="ltr" translate="no">        default_index_column_granularity       </code> field of the index options. The supported values are <code dir="ltr" translate="no">        'GLOBAL'       </code> (default) and <code dir="ltr" translate="no">        'COLUMN'       </code> . For more information, see <a href="/bigquery/docs/search-index#column-granularity">Index with column granularity</a> .</p></td>
</tr>
</tbody>
</table>

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.tables.createIndex      </code></td>
<td>The base table where you create the index.</td>
</tr>
</tbody>
</table>

### Examples

The following example creates a search index called `  my_index  ` on all string columns of `  my_table  ` . In this case, the index is only created on column `  a  ` .

``` text
CREATE TABLE dataset.my_table(a STRING, b INT64);

CREATE SEARCH INDEX my_index
ON dataset.my_table(ALL COLUMNS);
```

The following example creates a search index on columns `  a  ` , `  my_struct.string_field  ` , and `  b  ` that uses the `  NO_OP_ANALYZER  ` text analyzer. It sets the default index column granularity to `  COLUMN  ` and overrides the setting for column `  a  ` to `  GLOBAL  ` .

``` text
CREATE TABLE dataset.complex_table(
  a STRING,
  my_struct STRUCT <string_field STRING, int_field INT64>,
  b ARRAY <STRING>
);

CREATE SEARCH INDEX my_index
ON dataset.complex_table(
  a OPTIONS(index_granularity = 'GLOBAL'),
  my_struct,
  b)
OPTIONS (
  analyzer = 'NO_OP_ANALYZER',
  default_index_column_granularity = 'COLUMN');
```

## `     CREATE VECTOR INDEX    ` statement

Creates a new [vector index](/bigquery/docs/vector-index) on a column of a table.

A vector index lets you perform a [vector search](/bigquery/docs/vector-search-intro) more quickly, with the trade-off of reducing [recall](https://developers.google.com/machine-learning/crash-course/classification/precision-and-recall#recall) and so returning more approximate results.

### Syntax

``` text
CREATE [ OR REPLACE ] VECTOR INDEX [ IF NOT EXISTS ] index_name
ON table_name(column_name)
[STORING(stored_column_name [, ...])]
[PARTITION BY partition_expression]
OPTIONS(index_option_list);
```

### Arguments

  - `  OR REPLACE  ` : Replaces any vector index with the same name if it exists. Can't appear with `  IF NOT EXISTS  ` .

  - `  IF NOT EXISTS  ` : If there is already a vector index by that name on the table, do nothing. If the table has a vector index by a different name, then return an error.

  - `  index_name  ` : The name of the vector index you're creating. Since the index is always created in the same project and dataset as the base table, there is no need to specify these in the name.

  - `  table_name  ` : The name of the table. See [Table path syntax](#table_path) .

  - `  column_name  ` : The name of a column with a type of `  ARRAY<FLOAT64>  ` , or if you're using [autonomous embedding generation (Preview)](/bigquery/docs/autonomous-embedding-generation) , a `  STRUCT<result ARRAY<FLOAT64>, status STRING>  ` column. If column type is `  ARRAY<FLOAT64>  ` , then all elements in the array must be non- `  NULL  ` , and all values in the column must have the same array dimensions. If your index type is `  TREE_AH  ` , then the array dimension must be at least 2.

  - `  stored_column_name  ` : The name of a top-level column in the table to store in the vector index. The column type can't be `  RANGE  ` . Stored columns are not used if the table has a row-level access policy or the column has a policy tag. To learn more, see [Store columns and pre-filter](/bigquery/docs/vector-index#stored-columns) .

  - [`  partition_expression  `](#partition_expression) : An expression that determines how to partition the vector index. You can only partition TreeAH indexes. ( [Preview](https://cloud.google.com/products#product-launch-stages) )

  - [`  index_option_list  `](#vector_index_option_list) : The list of options to set on the vector index.

### Details

You can only create vector indexes on [standard tables](/bigquery/docs/tables-intro#standard-tables) .

You can create only one vector index per table. You can't create a vector index on a table that already has a [search index](#create_search_index_statement) with the same index name.

To modify which column is indexed, [`  DROP  `](#drop_vector_index) the current index and create a new one.

### `     index_option_list    `

The option list specifies options for the vector index. Specify the options in the following format: `  NAME=VALUE, ...  `

The following options are supported:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">       NAME      </code></th>
<th><code dir="ltr" translate="no">       VALUE      </code></th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       index_type      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Required. The algorithm to use to build the vector index. The supported values are <code dir="ltr" translate="no">       IVF      </code> and <code dir="ltr" translate="no">       TREE_AH      </code> .
<p><code dir="ltr" translate="no">        IVF       </code> : Specifying <code dir="ltr" translate="no">        IVF       </code> builds the vector index as an inverted file index (IVF). An IVF uses a k-means algorithm to cluster the vector data, and then partitions the vector data based on those clusters. When you use the <a href="/bigquery/docs/reference/standard-sql/search_functions#vector_search"><code dir="ltr" translate="no">         VECTOR_SEARCH        </code> function</a> to search the vector data, it can use these partitions to reduce the amount of data it needs to read in order to determine a result.</p>
<p><code dir="ltr" translate="no">        TREE_AH       </code> : Uses Google's <a href="https://github.com/google-research/google-research/blob/master/scann/docs/algorithms.md">ScaNN algorithm</a> . <code dir="ltr" translate="no">        TREE_AH       </code> is a tree-quantization based index, leveraging k-means clustering for partitioning and asymmetric hashing (product quantization) for fast approximate distance computation. For more information, see <a href="/bigquery/docs/vector-index#tree-ah-index">TreeAH index</a> .</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       distance_type      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Specifies the default distance type to use when performing a vector search using this index. The supported values are <a href="https://en.wikipedia.org/wiki/Euclidean_distance"><code dir="ltr" translate="no">        EUCLIDEAN       </code></a> , <a href="https://en.wikipedia.org/wiki/Cosine_similarity#Cosine_Distance"><code dir="ltr" translate="no">        COSINE       </code></a> , and <a href="https://en.wikipedia.org/wiki/Dot_product"><code dir="ltr" translate="no">        DOT_PRODUCT       </code></a> . <code dir="ltr" translate="no">       EUCLIDEAN      </code> is the default.
<p>The index creation itself always uses <code dir="ltr" translate="no">        EUCLIDEAN       </code> distance for training but the distance used in the <code dir="ltr" translate="no">        VECTOR_SEARCH       </code> function can be different.</p>
<p>If you specify a value for the <code dir="ltr" translate="no">        distance_type       </code> argument of the <a href="/bigquery/docs/reference/standard-sql/search_functions#vector_search"><code dir="ltr" translate="no">         VECTOR_SEARCH        </code> function</a> , that value is used instead of the vector index's <code dir="ltr" translate="no">        distance_type       </code> value.</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       ivf_options      </code></td>
<td><code dir="ltr" translate="no">       JSON-formatted STRING      </code></td>
<td>The options to use with the <code dir="ltr" translate="no">       IVF      </code> algorithm. Defaults to <code dir="ltr" translate="no">       '{}'      </code> to denote that all underlying options use their corresponding default values.
<p>The only supported option is <code dir="ltr" translate="no">        num_lists       </code> . Specify an <code dir="ltr" translate="no">        INT64       </code> less than or equal to 5,000 that determines how many lists the IVF algorithm creates. For example, <code dir="ltr" translate="no">        ivf_options = '{"num_lists":1000}'       </code> .</p>
<p>During indexing, vectors are assigned to the list corresponding to their nearest cluster centroid. If you omit this argument, BigQuery determines a default value based on your data characteristics. The default value works well for most use cases.</p>
<p><code dir="ltr" translate="no">        num_lists       </code> controls query tuning granularity. Higher values create more lists, so you can set the <code dir="ltr" translate="no">        fraction_lists_to_search       </code> option of the <code dir="ltr" translate="no">        VECTOR_SEARCH       </code> function to scan a smaller percentage of the index. For example, scanning 1% of 100 lists as opposed to scanning 10% of 10 lists. This enables finer control of the search speed and recall but slightly increases the indexing cost. Set this argument value based on how precisely you need to tune query scope.</p>
<p>The statement fails if <code dir="ltr" translate="no">        ivf_options       </code> is specified and <code dir="ltr" translate="no">        index_type       </code> is not <code dir="ltr" translate="no">        IVF       </code> .</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       tree_ah_options      </code></td>
<td><code dir="ltr" translate="no">       JSON-formatted STRING      </code></td>
<td>The options to use with the <code dir="ltr" translate="no">       TREE_AH      </code> algorithm. Defaults to <code dir="ltr" translate="no">       '{}'      </code> to denote that all underlying options use their corresponding default values.
<p>Two options are supported: <code dir="ltr" translate="no">        leaf_node_embedding_node       </code> and <code dir="ltr" translate="no">        normalization_type       </code> .</p>
<p><code dir="ltr" translate="no">        leaf_node_embedding_count       </code> is an <code dir="ltr" translate="no">        INT64       </code> value greater than or equal to 500 that specifies the approximate number of vectors in each leaf node of the tree that the TreeAH algorithm creates. The TreeAH algorithm divides the whole data space into a number of lists, with each list containing approximately <code dir="ltr" translate="no">        leaf_node_embedding_count       </code> data points. A lower value creates more lists with fewer data points, while a larger value creates fewer lists with more data points. The default is 1,000, which is appropriate for most datasets.</p>
<p><code dir="ltr" translate="no">        normalization_type       </code> : the type of normalization performed on each base table and query vector prior to any processing. The supported values are <code dir="ltr" translate="no">        NONE       </code> and <code dir="ltr" translate="no">        L2       </code> . <code dir="ltr" translate="no">        L2       </code> is also referred to as the <a href="https://en.wikipedia.org/wiki/Norm_(mathematics)#Euclidean_norm">Euclidean norm</a> . Defaults to <code dir="ltr" translate="no">        NONE       </code> . Normalization happens before any processing, for both the base table data and the query data, but doesn't modify the embedding column in the table. Depending on the dataset, the embedding model, and the distance type used during <a href="/bigquery/docs/reference/standard-sql/search_functions#vector_search"><code dir="ltr" translate="no">         VECTOR_SEARCH        </code></a> , normalizing the embeddings might improve recall.</p>
<p>For example <code dir="ltr" translate="no">        tree_ah_options = '{"leaf_node_embedding_count": 1000,     "normalization_type": "L2"}'       </code></p>
<p>The statement fails if <code dir="ltr" translate="no">        tree_ah_options       </code> is specified and <code dir="ltr" translate="no">        index_type       </code> is not <code dir="ltr" translate="no">        TREE_AH       </code> .</p></td>
</tr>
</tbody>
</table>

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.tables.createIndex      </code></td>
<td>The table where you create the vector index.</td>
</tr>
</tbody>
</table>

If you choose to use the `  OR REPLACE  ` clause, you must also have the `  bigquery.tables.updateIndex  ` permission.

### Examples

The following examples show how to create vector indexes with different options. They assume that you have a base table named `  my_table  ` , which contains a column called `  embedding  ` of type `  ARRAY<FLOAT64>  ` and a [sufficient number of rows](/bigquery/quotas#vector_index_limits) .

This example creates a vector index of type `  IVF  ` on the `  embedding  ` column of `  my_table  ` :

``` text
CREATE VECTOR INDEX my_index ON my_dataset.my_table(embedding)
OPTIONS (index_type = 'IVF');
```

The following example creates a vector index on the `  embedding  ` column of `  my_table  ` , and specifies the distance type to use and the IVF options:

``` text
CREATE VECTOR INDEX my_index ON my_dataset.my_table(embedding)
OPTIONS (
  index_type = 'IVF',
  distance_type = 'COSINE',
  ivf_options = '{"num_lists":2500}');
```

The following example creates a vector index on the `  embedding  ` column of `  my_table  ` , and specifies the distance type to use and the `  TREE_AH  ` options:

``` text
CREATE VECTOR INDEX my_index ON my_dataset.my_table(embedding)
OPTIONS (
  index_type = 'TREE_AH',
  distance_type = 'EUCLIDEAN',
  tree_ah_options = '{"normalization_type": "L2"}');
```

## `     CREATE DATA_POLICY    ` statement

**Preview**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

**Note:** To provide feedback or request support for this feature, send an email to <bigquery-security@google.com> .

Creates or replaces a [data policy](/bigquery/docs/column-data-masking#data-policies-on-column) . The name of the data policy must be unique within the project.

### Syntax

``` text
CREATE [ OR REPLACE ] DATA_POLICY [ IF NOT EXISTS ] `project_id.region-location_id.data_policy_id`
OPTIONS(index_option_list);
```

### Arguments

  - `  OR REPLACE  ` : Replaces any data policy with the same name if it exists. Can't appear with `  IF NOT EXISTS  ` .

  - `  IF NOT EXISTS  ` : If there is already a data policy by that name in the project, the `  CREATE  ` statement has no effect.

  - `  project_id  ` : The project ID of the project where the data policy will reside in.

  - `  location_id  ` : The location of the data policy.

  - `  data_policy_id  ` : The name of the data policy that is unique within the project that the data policy resides in.

  - [`  index_option_list  `](#datapolicy_option_list) : The list of options to set on the data policy.

### `     index_option_list    `

The option list specifies options for the data policy. Specify the options in the following format: `  NAME=VALUE, ...  `

The following options are supported:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">       NAME      </code></th>
<th><code dir="ltr" translate="no">       VALUE      </code></th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       data_policy_type      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The supported values are <code dir="ltr" translate="no">       DATA_MASKING_POLICY      </code> and <code dir="ltr" translate="no">       RAW_DATA_ACCESS_POLICY      </code> .
<p>If not specified, the default value is <code dir="ltr" translate="no">        RAW_DATA_ACCESS_POLICY       </code> .</p>
<p>You can't update this field once the data policy has been created.</p>
<p><code dir="ltr" translate="no">        DATA_MASKING_POLICY       </code> type should come with <code dir="ltr" translate="no">        masking_expression       </code> set.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       masking_expression      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Specifies the <a href="/bigquery/docs/reference/bigquerydatapolicy/rest/v2/projects.locations.dataPolicies#PredefinedExpression">predefined masking rule</a> or a <a href="/bigquery/docs/column-data-masking-intro#custom_mask">custom masking routine</a> .</td>
</tr>
</tbody>
</table>

### Required permissions

The user or service account that creates a data policy must have the `  bigquery.dataPolicies.create  ` permission.

The `  bigquery.dataPolicies.create  ` permission is included in the BigQuery Data Policy Admin, BigQuery Admin and BigQuery Data Owner roles.

If you are creating a data policy that references a custom masking routine, you also need [routine permissions](/bigquery/docs/routines#permissions) .

## `     ALTER SCHEMA SET DEFAULT COLLATE    ` statement

Sets [collation specifications](/bigquery/docs/reference/standard-sql/collation-concepts#collate_spec_details) on a dataset.

### Syntax

``` text
ALTER SCHEMA [IF EXISTS]
[project_name.]dataset_name
SET DEFAULT COLLATE collate_specification
```

### Arguments

  - `  IF EXISTS  ` : If no dataset exists with that name, the statement has no effect.

  - `  DEFAULT COLLATE collate_specification  ` : When a new table is created in the dataset, the table inherits a default [collation specification](/bigquery/docs/reference/standard-sql/collation-concepts#default_collation) unless a collation specification is explicitly specified for a [column](#column_name_and_column_schema) .
    
    The updated collation specification only applies to tables created afterwards.

  - `  project_name  ` : The name of the project that contains the dataset. Defaults to the project that runs this DDL statement.

  - `  dataset_name  ` : The name of the dataset.

  - [`  collate_specification  `](/bigquery/docs/reference/standard-sql/collation-concepts#collate_spec_details) : Specifies the collation specifications to set.

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.datasets.get      </code></td>
<td>The dataset to alter.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigquery.datasets.update      </code></td>
<td>The dataset to alter.</td>
</tr>
</tbody>
</table>

### Example

Assume you have an existing table, `  mytable_a  ` , in a dataset called `  mydataset  ` . For example:

``` text
CREATE SCHEMA mydataset
```

``` text
CREATE TABLE mydataset.mytable_a
(
  number INT64,
  word STRING
)
```

``` text
+----------------------+
| mydataset.mytable_a  |
|   number INT64       |
|   word STRING        |
+----------------------+
```

At a later time, you decide to add a collation specification to your dataset. For example:

``` text
ALTER SCHEMA mydataset
SET DEFAULT COLLATE 'und:ci'
```

If you create a new table for your dataset, it inherits `  COLLATE 'und:ci'  ` for all `  STRING  ` columns. For example, collation is added to `  characters  ` when you create the `  mytable_b  ` table in the `  mydataset  ` dataset:

``` text
CREATE TABLE mydataset.mytable_b
(
  amount INT64,
  characters STRING
)
```

``` text
+--------------------------------------+
| mydataset.mytable_b                  |
|   amount INT64                       |
|   characters STRING COLLATE 'und:ci' |
+--------------------------------------+
```

However, although you have updated the collation specification for the dataset, your existing table, `  mytable_a  ` , continues to use the previous collation specification. For example:

``` text
+---------------------+
| mydataset.mytable_a |
|   number INT64      |
|   word STRING       |
+---------------------+
```

## `     ALTER SCHEMA SET OPTIONS    ` statement

Sets options on a dataset.

The statement runs in the location of the dataset if the dataset exists, unless you specify the location in the query settings. For more information, see [Specifying your location](/bigquery/docs/locations#specify_locations) .

### Syntax

``` text
ALTER SCHEMA [IF EXISTS]
[project_name.]dataset_name
SET OPTIONS(schema_set_options_list)
```

### Arguments

  - `  IF EXISTS  ` : If no dataset exists with that name, the statement has no effect.

  - `  project_name  ` : The name of the project that contains the dataset. Defaults to the project that runs this DDL statement.

  - `  dataset_name  ` : The name of the dataset.

  - [`  schema_set_options_list  `](#schema_set_options_list) : The list of options to set.

### `     schema_set_options_list    `

The option list specifies options for the dataset. Specify the options in the following format: `  NAME=VALUE, ...  `

The following options are supported:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">       NAME      </code></th>
<th><code dir="ltr" translate="no">       VALUE      </code></th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       default_kms_key_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Specifies the default Cloud KMS key for encrypting table data in this dataset. You can override this value when you create a table.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       default_partition_expiration_days      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
<td>Specifies the default expiration time, in days, for table partitions in this dataset. You can override this value when you create a table.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       default_rounding_mode      </code></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>Example: <code dir="ltr" translate="no">        default_rounding_mode = "ROUND_HALF_EVEN"       </code></p>
<p>This specifies the <a href="/bigquery/docs/reference/rest/v2/datasets#Dataset.FIELDS.default_rounding_mode"><code dir="ltr" translate="no">         defaultRoundingMode        </code></a> that is used for new tables created in this dataset. It does not impact existing tables. The following values are supported:</p>
<ul>
<li><code dir="ltr" translate="no">         "ROUND_HALF_AWAY_FROM_ZERO"        </code> : Halfway cases are rounded away from zero. For example, 2.25 is rounded to 2.3, and -2.25 is rounded to -2.3.</li>
<li><code dir="ltr" translate="no">         "ROUND_HALF_EVEN"        </code> : Halfway cases are rounded towards the nearest even digit. For example, 2.25 is rounded to 2.2 and -2.25 is rounded to -2.2.</li>
</ul></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       default_table_expiration_days      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
<td>Specifies the default expiration time, in days, for tables in this dataset. You can override this value when you create a table.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       description      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The description of the dataset.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       failover_reservation      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Associates the dataset to a reservation in the case of a failover scenario.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       friendly_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>A descriptive name for the dataset.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       is_case_insensitive      </code></td>
<td><code dir="ltr" translate="no">       BOOL      </code></td>
<td><code dir="ltr" translate="no">       TRUE      </code> if the dataset and its table names are case-insensitive, otherwise <code dir="ltr" translate="no">       FALSE      </code> . By default, this is <code dir="ltr" translate="no">       FALSE      </code> , which means the dataset and its table names are case-sensitive.
<ul>
<li>Datasets: <code dir="ltr" translate="no">         mydataset        </code> and <code dir="ltr" translate="no">         MyDataset        </code> can coexist in the same project, unless one of them has case-sensitivity turned off.</li>
<li>Tables: <code dir="ltr" translate="no">         mytable        </code> and <code dir="ltr" translate="no">         MyTable        </code> can coexist in the same dataset if case-sensitivity for the dataset is turned on.</li>
</ul></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       is_primary      </code></td>
<td><code dir="ltr" translate="no">       BOOLEAN      </code></td>
<td>Declares if the dataset is the primary replica.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       labels      </code></td>
<td><code dir="ltr" translate="no">       &lt;ARRAY&lt;STRUCT&lt;STRING, STRING&gt;&gt;&gt;      </code></td>
<td>An array of labels for the dataset, expressed as key-value pairs.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       max_time_travel_hours      </code></td>
<td><code dir="ltr" translate="no">       SMALLINT      </code></td>
<td>Specifies the duration in hours of the <a href="/bigquery/docs/time-travel#time_travel">time travel window</a> for the dataset. The <code dir="ltr" translate="no">       max_time_travel_hours      </code> value must be an integer expressed in multiples of 24 (48, 72, 96, 120, 144, 168) between 48 (2 days) and 168 (7 days). 168 hours is the default if this option isn't specified.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       primary_replica      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The replica name to set as the <a href="/bigquery/docs/data-replication">primary replica</a> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       storage_billing_model      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><p>Alters the <a href="/bigquery/docs/datasets-intro#dataset_storage_billing_models">storage billing model</a> for the dataset. Set the <code dir="ltr" translate="no">        storage_billing_model       </code> value to <code dir="ltr" translate="no">        PHYSICAL       </code> to use physical bytes when calculating storage charges, or to <code dir="ltr" translate="no">        LOGICAL       </code> to use logical bytes. <code dir="ltr" translate="no">        LOGICAL       </code> is the default.</p>
<p>The <code dir="ltr" translate="no">        storage_billing_model       </code> option is only available for datasets that have been updated after December 1, 2022. For datasets that were last updated before that date, the storage billing model is <code dir="ltr" translate="no">        LOGICAL       </code> .</p>
<p>When you change a dataset's billing model, it takes 24 hours for the change to take effect.</p>
<p>Once you change a dataset's storage billing model, you must wait 14 days before you can change the storage billing model again.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       tags      </code></td>
<td><code dir="ltr" translate="no">       &lt;ARRAY&lt;STRUCT&lt;STRING, STRING&gt;&gt;&gt;      </code></td>
<td>An array of IAM tags for the dataset, expressed as key-value pairs. The key should be the <a href="/iam/docs/tags-access-control#definitions">namespaced key name</a> , and the value should be the <a href="/iam/docs/tags-access-control#definitions">short name</a> .</td>
</tr>
</tbody>
</table>

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.datasets.get      </code></td>
<td>The dataset to alter.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigquery.datasets.update      </code></td>
<td>The dataset to alter.</td>
</tr>
</tbody>
</table>

### Examples

#### Setting the default table expiration for a dataset

The following example sets the default table expiration.

``` text
ALTER SCHEMA mydataset
SET OPTIONS(
  default_table_expiration_days=3.75
  )
```

#### Turning on case insensitivity for a dataset

The following example turns on case insensitivity for the name of a dataset and the table names within that dataset.

``` text
ALTER SCHEMA mydataset
SET OPTIONS(
  is_case_insensitive=TRUE
)
```

## `     ALTER SCHEMA ADD REPLICA    ` statement

Adds a replica to a schema ( [preview](https://cloud.google.com/products/#product-launch-stages) ).

### Syntax

``` text
ALTER SCHEMA [IF EXISTS]
[project_name.]dataset_name
ADD REPLICA replica_name [OPTIONS(add_replica_options_list)]
```

### Arguments

  - `  IF EXISTS  ` : If no dataset exists with that name, the statement has no effect.
  - `  dataset_name  ` : The name of the table to alter. See [Table path syntax](#table_path) .
  - `  replica_name  ` : The name of the new replica. Conventionally, this is the same as the location you are creating the replica in.
  - [`  add_replica_option_list  `](#add_replica_options_list) : The list of options to set.

### `     add_replica_options_list    `

The option list specifies options for the dataset. Specify the options in the following format: `  NAME=VALUE, ...  `

The following options are supported:

<table>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">       NAME      </code></th>
<th><code dir="ltr" translate="no">       VALUE      </code></th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       location      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The location in which to create the replica.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       replica_kms_key      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The Cloud Key Management Service key set in the destination region. <code dir="ltr" translate="no">       replica_kms_key      </code> is used as a substitute encryption key in the destination region for any keys used in the source region. Any table in the source region that's encrypted with a Cloud KMS key is encrypted with the <code dir="ltr" translate="no">       replica_kms_key      </code> . This value must be a Cloud KMS key created in the replica dataset's region, not the source dataset's region. For more information about setting up a Cloud KMS key, see <a href="/bigquery/docs/customer-managed-encryption#grant_permission">Grant encryption and decryption permission</a> .</td>
</tr>
</tbody>
</table>

### Required permissions

To get the permissions that you need to manage replicas, ask your administrator to grant you the [BigQuery Data Editor](/iam/docs/roles-permissions/bigquery#bigquery.dataEditor) ( `  roles/bigquery.dataEditor  ` ) IAM role on your schema. For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

### Examples

The following example adds a secondary replica that is named `  EU  ` in the `  EU  ` multi-region to a schema that is named `  cross_region_dataset  ` :

``` text
ALTER SCHEMA cross_region_dataset
ADD REPLICA `EU` OPTIONS(location=`eu`);
```

## `     ALTER SCHEMA DROP REPLICA    ` statement

Drops a replica from a schema ( [preview](https://cloud.google.com/products/#product-launch-stages) ).

### Syntax

``` text
ALTER SCHEMA [IF EXISTS] dataset_name
DROP REPLICA replica_name
```

  - `  IF EXISTS  ` : If no dataset exists with that name, the statement has no effect.
  - `  dataset_name  ` : The name of the table to alter. See [Table path syntax](#table_path) .
  - `  replica_name  ` : The name of the replica to drop.

### Required permissions

To get the permissions that you need to manage replicas, ask your administrator to grant you the [BigQuery Data Editor](/iam/docs/roles-permissions/bigquery#bigquery.dataEditor) ( `  roles/bigquery.dataEditor  ` ) IAM role on your schema. For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

### Examples

The following example removes a replica that is located in the `  us-east4  ` region from the `  cross_region_dataset  ` dataset:

``` text
ALTER SCHEMA [IF EXISTS] cross_region_dataset
DROP REPLICA `us-east4`
```

## `     ALTER TABLE SET OPTIONS    ` statement

Sets the options on a table.

### Syntax

``` text
ALTER TABLE [IF EXISTS] table_name
SET OPTIONS(table_set_options_list)
```

### Arguments

  - `  IF EXISTS  ` : If no table exists with that name, the statement has no effect.

  - `  table_name  ` : The name of the table to alter. See [Table path syntax](#table_path) .

  - [`  table_set_options_list  `](#table_set_options_list) : The list of options to set.

### Details

This statement is not supported for [external tables](/bigquery/docs/external-tables) .

### `     table_set_options_list    `

The option list lets you set table options such as a [label](/bigquery/docs/labels) and an expiration time. You can include multiple options using a comma-separated list.

Specify a table option list in the following format:

`  NAME=VALUE, ...  `

`  NAME  ` and `  VALUE  ` must be one of the following combinations:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">       NAME      </code></th>
<th><code dir="ltr" translate="no">       VALUE      </code></th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       expiration_timestamp      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td><p>Example: <code dir="ltr" translate="no">        expiration_timestamp=TIMESTAMP "2025-01-01 00:00:00 UTC"       </code></p>
<p>This property is equivalent to the <a href="/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.expiration_time">expirationTime</a> table resource property.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       partition_expiration_days      </code></td>
<td><p><code dir="ltr" translate="no">        FLOAT64       </code></p></td>
<td><p>Example: <code dir="ltr" translate="no">        partition_expiration_days=7       </code></p>
<p>Sets the partition expiration in days. For more information, see <a href="/bigquery/docs/managing-partitioned-tables#partition-expiration">Set the partition expiration</a> . By default, partitions don't expire.</p>
<p>This property is equivalent to the <a href="/bigquery/docs/reference/rest/v2/tables#TimePartitioning.FIELDS.expiration_ms">timePartitioning.expirationMs</a> table resource property but uses days instead of milliseconds. One day is equivalent to 86400000 milliseconds, or 24 hours.</p>
<p>This property can only be set if the table is partitioned.</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       require_partition_filter      </code></td>
<td><p><code dir="ltr" translate="no">        BOOL       </code></p></td>
<td><p>Example: <code dir="ltr" translate="no">        require_partition_filter=true       </code></p>
<p>Specifies whether queries on this table must include a a predicate filter that filters on the partitioning column. For more information, see <a href="/bigquery/docs/managing-partitioned-tables#require-filter">Set partition filter requirements</a> . The default value is <code dir="ltr" translate="no">        false       </code> .</p>
<p>This property is equivalent to the <a href="/bigquery/docs/reference/rest/v2/tables#TimePartitioning.FIELDS.require_partition_filter">timePartitioning.requirePartitionFilter</a> table resource property.</p>
<p>This property can only be set if the table is partitioned.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       kms_key_name      </code></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>Example: <code dir="ltr" translate="no">        kms_key_name="projects/                 project_id                /locations/       </code> <code dir="ltr" translate="no">          location                /keyRings/                 keyring                /cryptoKeys/                 key                "       </code></p>
<p>This property is equivalent to the <a href="/bigquery/docs/reference/rest/v2/EncryptionConfiguration#FIELDS.kms_key_name">encryptionConfiguration.kmsKeyName</a> table resource property.</p>
<p>See more details about <a href="/bigquery/docs/customer-managed-encryption">Protecting data with Cloud KMS keys</a> .</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       friendly_name      </code></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>Example: <code dir="ltr" translate="no">        friendly_name="my_table"       </code></p>
<p>This property is equivalent to the <a href="/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.friendly_name">friendlyName</a> table resource property.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       description      </code></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>Example: <code dir="ltr" translate="no">        description="a table that expires in 2025"       </code></p>
<p>This property is equivalent to the <a href="/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.description">description</a> table resource property.</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       labels      </code></td>
<td><p><code dir="ltr" translate="no">        ARRAY&lt;STRUCT&lt;STRING, STRING&gt;&gt;       </code></p></td>
<td><p>Example: <code dir="ltr" translate="no">        labels=[("org_unit", "development")]       </code></p>
<p>This property is equivalent to the <a href="/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.labels">labels</a> table resource property.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       default_rounding_mode      </code></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>Example: <code dir="ltr" translate="no">        default_rounding_mode = "ROUND_HALF_EVEN"       </code></p>
<p>This specifies the default <a href="/bigquery/docs/schemas#rounding_mode">rounding mode</a> that's used for values written to any new <code dir="ltr" translate="no">        NUMERIC       </code> or <code dir="ltr" translate="no">        BIGNUMERIC       </code> type columns or <code dir="ltr" translate="no">        STRUCT       </code> fields in the table. It does not impact existing fields in the table. The following values are supported:</p>
<ul>
<li><code dir="ltr" translate="no">         "ROUND_HALF_AWAY_FROM_ZERO"        </code> : Halfway cases are rounded away from zero. For example, 2.5 is rounded to 3.0, and -2.5 is rounded to -3.</li>
<li><code dir="ltr" translate="no">         "ROUND_HALF_EVEN"        </code> : Halfway cases are rounded towards the nearest even digit. For example, 2.5 is rounded to 2.0 and -2.5 is rounded to -2.0.</li>
</ul>
<p>This property is equivalent to the <a href="/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.default_rounding_mode"><code dir="ltr" translate="no">         defaultRoundingMode        </code></a> table resource property.</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       enable_change_history      </code></td>
<td><p><code dir="ltr" translate="no">        BOOL       </code></p></td>
<td><p>In <a href="https://cloud.google.com/products/#product-launch-stages">preview</a> .</p>
<p>Example: <code dir="ltr" translate="no">        enable_change_history=TRUE       </code></p>
<p>Set this property to <code dir="ltr" translate="no">        TRUE       </code> in order to capture <a href="/bigquery/docs/change-history">change history</a> on the table, which you can then view by using the <a href="/bigquery/docs/reference/standard-sql/time-series-functions#changes"><code dir="ltr" translate="no">         CHANGES        </code> function</a> . Enabling this table option has an impact on costs; for more information see <a href="/bigquery/docs/change-history#pricing_and_costs">Pricing and costs</a> . The default is <code dir="ltr" translate="no">        FALSE       </code> .</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       max_staleness      </code></td>
<td><p><code dir="ltr" translate="no">        INTERVAL       </code></p></td>
<td><p>Example: <code dir="ltr" translate="no">        max_staleness=INTERVAL "4:0:0" HOUR TO SECOND       </code></p>
<p>The maximum interval behind the current time where it's acceptable to read stale data. For example, with <a href="/bigquery/docs/change-data-capture">change data capture</a> , when this option is set, the table copy operation is denied if data is more stale than the <code dir="ltr" translate="no">        max_staleness       </code> value.</p>
<p><code dir="ltr" translate="no">        max_staleness       </code> is disabled by default.</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       enable_fine_grained_mutations      </code></td>
<td><p><code dir="ltr" translate="no">        BOOL       </code></p></td>
<td><p>In <a href="https://cloud.google.com/products/#product-launch-stages">preview</a> .</p>
<p>Example: <code dir="ltr" translate="no">        enable_fine_grained_mutations=TRUE       </code></p>
<p>Set this property to <code dir="ltr" translate="no">        TRUE       </code> to enable <a href="/bigquery/docs/data-manipulation-language#fine-grained_dml">fine-grained DML optimization</a> on the table. The default is <code dir="ltr" translate="no">        FALSE       </code> .</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       storage_uri      </code></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>In <a href="https://cloud.google.com/products/#product-launch-stages">preview</a> .</p>
<p>Example: <code dir="ltr" translate="no">        storage_uri=                 gs:                //                 BUCKET_DIRECTORY                /                 TABLE_DIRECTORY                /       </code></p>
<p>A fully qualified location prefix for the external folder where data is stored. Supports <code dir="ltr" translate="no">        gs:       </code> buckets.</p>
<p>Required for <a href="/bigquery/docs/managed-tables">managed tables</a> .</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       file_format      </code></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>In <a href="https://cloud.google.com/products/#product-launch-stages">preview</a> .</p>
<p>Example: <code dir="ltr" translate="no">        file_format=PARQUET       </code></p>
<p>The open-source file format in which the table data is stored. Only <code dir="ltr" translate="no">        PARQUET       </code> is supported.</p>
<p>Required for <a href="/bigquery/docs/managed-tables">managed tables</a> .</p>
<p>The default is <code dir="ltr" translate="no">        PARQUET       </code> .</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       table_format      </code></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>In <a href="https://cloud.google.com/products/#product-launch-stages">preview</a> .</p>
<p>Example: <code dir="ltr" translate="no">        table_format=ICEBERG       </code></p>
<p>The open table format in which metadata-only snapshots are stored. Only <code dir="ltr" translate="no">        ICEBERG       </code> is supported.</p>
<p>Required for <a href="/bigquery/docs/managed-tables">managed tables</a> .</p>
<p>The default is <code dir="ltr" translate="no">        ICEBERG       </code> .</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       tags      </code></td>
<td><code dir="ltr" translate="no">       &lt;ARRAY&lt;STRUCT&lt;STRING, STRING&gt;&gt;&gt;      </code></td>
<td>An array of IAM tags for the table, expressed as key-value pairs. The key should be the <a href="/iam/docs/tags-access-control#definitions">namespaced key name</a> , and the value should be the <a href="/iam/docs/tags-access-control#definitions">short name</a> .</td>
</tr>
</tbody>
</table>

`  VALUE  ` is a constant expression containing only literals, query parameters, and scalar functions.

The constant expression **cannot** contain:

  - A reference to a table
  - Subqueries or SQL statements such as `  SELECT  ` , `  CREATE  ` , or `  UPDATE  `
  - User-defined functions, aggregate functions, or analytic functions
  - The following scalar functions:
      - `  ARRAY_TO_STRING  `
      - `  REPLACE  `
      - `  REGEXP_REPLACE  `
      - `  RAND  `
      - `  FORMAT  `
      - `  LPAD  `
      - `  RPAD  `
      - `  REPEAT  `
      - `  SESSION_USER  `
      - `  GENERATE_ARRAY  `
      - `  GENERATE_DATE_ARRAY  `

Setting the value replaces the existing value of that option for the table, if there was one. Setting the value to `  NULL  ` clears the table's value for that option.

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.tables.get      </code></td>
<td>The table to alter.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigquery.tables.update      </code></td>
<td>The table to alter.</td>
</tr>
</tbody>
</table>

### Examples

#### Setting the expiration timestamp and description on a table

The following example sets the expiration timestamp on a table to seven days from the execution time of the `  ALTER TABLE  ` statement, and sets the description as well:

``` text
ALTER TABLE mydataset.mytable
SET OPTIONS (
  expiration_timestamp=TIMESTAMP_ADD(CURRENT_TIMESTAMP(), INTERVAL 7 DAY),
  description="Table that expires seven days from now"
)
```

#### Setting the require partition filter attribute on a partitioned table

The following example sets the [`  timePartitioning.requirePartitionFilter  `](/bigquery/docs/reference/rest/v2/tables#TimePartitioning) attribute on a [partitioned table](/bigquery/docs/partitioned-tables) :

``` text
ALTER TABLE mydataset.mypartitionedtable
SET OPTIONS (require_partition_filter=true)
```

Queries that reference this table must use a filter on the partitioning column, or else BigQuery returns an error. Setting this option to `  true  ` can help prevent mistakes in querying more data than intended.

#### Clearing the expiration timestamp on a table

The following example clears the expiration timestamp on a table so that it will not expire:

``` text
ALTER TABLE mydataset.mytable
SET OPTIONS (expiration_timestamp=NULL)
```

## `     ALTER TABLE ADD COLUMN    ` statement

Adds one or more new columns to an existing table schema.

### Syntax

``` text
ALTER TABLE table_name
ADD COLUMN [IF NOT EXISTS] column [, ...]
```

### Arguments

  - `  table_name  ` : The name of the table. See [Table path syntax](#table_path) .

  - `  IF NOT EXISTS  ` : If the column name already exists, the statement has no effect.

  - `  column  ` : The column to add. This includes the name of the column and schema to add. The column name and schema use the same syntax used in the [`  CREATE TABLE  `](#create_table_statement) statement.

### Details

You cannot use this statement to create:

  - Partitioned columns.
  - Clustered columns.
  - Nested columns inside existing `  RECORD  ` fields.

You cannot add a `  REQUIRED  ` column to an existing table schema. However, you can create a nested `  REQUIRED  ` column as part of a new `  RECORD  ` field.

This statement is not supported for [external tables](/bigquery/docs/external-tables) .

Without the `  IF NOT EXISTS  ` clause, if the table already contains a column with that name, the statement returns an error. If the `  IF NOT EXISTS  ` clause is included and the column name already exists, no error is returned, and no action is taken.

The value of the new column for existing rows is set to one of the following:

  - `  NULL  ` if the new column was added with `  NULLABLE  ` mode. This is the default mode.
  - An empty `  ARRAY  ` if the new column was added with `  REPEATED  ` mode.

For more information about schema modifications in BigQuery, see [Modifying table schemas](/bigquery/docs/managing-table-schemas) .

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.tables.get      </code></td>
<td>The table to alter.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigquery.tables.update      </code></td>
<td>The table to alter.</td>
</tr>
</tbody>
</table>

### Examples

#### Adding columns

The following example adds the following columns to an existing table named `  mytable  ` :

  - Column `  A  ` of type `  STRING  ` .
  - Column `  B  ` of type `  GEOGRAPHY  ` .
  - Column `  C  ` of type `  NUMERIC  ` with `  REPEATED  ` mode.
  - Column `  D  ` of type `  DATE  ` with a description.

<!-- end list -->

``` text
ALTER TABLE mydataset.mytable
  ADD COLUMN A STRING,
  ADD COLUMN IF NOT EXISTS B GEOGRAPHY,
  ADD COLUMN C ARRAY <NUMERIC>,
  ADD COLUMN D DATE OPTIONS(description="my description")
```

If any of the columns named `  A  ` , `  C  ` , or `  D  ` already exist, the statement fails. If column `  B  ` already exists, the statement succeeds because of the `  IF NOT EXISTS  ` clause.

#### Adding a `     RECORD    ` column

The following example adds a column named `  A  ` of type `  STRUCT  ` that contains the following nested columns:

  - Column `  B  ` of type `  GEOGRAPHY  ` .
  - Column `  C  ` of type `  INT64  ` with `  REPEATED  ` mode.
  - Column `  D  ` of type `  INT64  ` with `  REQUIRED  ` mode.
  - Column `  E  ` of type `  TIMESTAMP  ` with a description.

<!-- end list -->

``` text
ALTER TABLE mydataset.mytable
   ADD COLUMN A STRUCT<
       B GEOGRAPHY,
       C ARRAY <INT64>,
       D INT64 NOT NULL,
       E TIMESTAMP OPTIONS(description="creation time")
       >
```

The query fails if the table already has a column named `  A  ` , even if that column does not contain any of the nested columns that are specified.

The new `  STRUCT  ` named `  A  ` is nullable, but the nested column `  D  ` within `  A  ` is required for any `  STRUCT  ` values of `  A  ` .

#### Adding collation support to a column

When you create a new column for your table, you can specifically assign a new collation specification to that column.

``` text
ALTER TABLE mydataset.mytable
ADD COLUMN word STRING COLLATE 'und:ci'
```

## `     ALTER TABLE ADD FOREIGN KEY    ` statement

Adds a [foreign key constraint](/bigquery/docs/primary-foreign-keys) to an existing table. You can add multiple foreign key constraints by using additional `  ADD FOREIGN KEY  ` statements.

### Syntax

``` text
ALTER TABLE [[project_name.]dataset_name.]fk_table_name
ADD [CONSTRAINT [IF NOT EXISTS] constraint_name] FOREIGN KEY (fk_column_name[, ...])
REFERENCES pk_table_name(pk_column_name[,...]) NOT ENFORCED
[ADD...];
```

### Arguments

  - `  project_name  ` : The name of the project containing the table with a [primary key](/bigquery/docs/primary-foreign-keys) . Defaults to the project that runs this DDL statement if undefined.
  - `  dataset_name  ` : The name of the dataset that contains the table with a primary key. Defaults to the project that runs this DDL statement if undefined.
  - `  fk_table_name  ` : The name of the existing table to add a foreign key to.
  - `  IF NOT EXISTS  ` : If a constraint of the same name already exists in the defined table, the statement has no effect.
  - `  constraint_name  ` : The name of the constraint to add.
  - `  fk_column_name  ` : In the foreign key table, the name of the foreign key column. Only top-level columns can be used as foreign key columns.
  - `  pk_table_name  ` : The name of the table that contains the primary key.
  - `  pk_column_name  ` : In the primary key table, the name of the primary key column. Only top-level columns can be used as primary key columns.

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.tables.get      </code></td>
<td>The table to alter.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigquery.tables.update      </code></td>
<td>The table to alter.</td>
</tr>
</tbody>
</table>

### Examples

The following example adds the `  my_fk_name  ` foreign key constraint to the `  fk_table  ` table. This example depends on an existing table, `  pk_table  ` .

1.  Add a primary key to the `  pk_table  ` table:
    
    ``` text
    ALTER TABLE pk_table
    ADD PRIMARY KEY (x,y) NOT ENFORCED;
    ```

2.  Create a table named `  fk_table  ` for the foreign key.
    
    ``` text
    CREATE TABLE fk_table(x int64, y int64, i int64, j int64, u int64, v int64);
    ```

3.  Add the `  my_fk_name  ` foreign key constraint to the `  fk_table  ` .
    
    ``` text
    ALTER TABLE fk_table
    ADD CONSTRAINT my_fk_name FOREIGN KEY (u, v)
    REFERENCES pk_table(x, y) NOT ENFORCED
    ```

The following example adds the `  fk  ` and `  fk2  ` foreign key constraints to the `  fk_table  ` table in a single statement. This example depends on an existing table, `  pk_table  ` .

1.  Add a primary key to the `  pk_table  ` table:
    
    ``` text
    ALTER TABLE pk_table
    ADD PRIMARY KEY (x,y) NOT ENFORCED;
    ```

2.  Create a table named `  fk_table  ` for multiple foreign key constraints.
    
    ``` text
    CREATE TABLE fk_table(x int64, y int64, i int64, j int64, u int64, v int64);
    ```

3.  Add the `  fk  ` and `  fk2  ` constraints to `  fk_table  ` in one statement.
    
    ``` text
    ALTER TABLE fk_table
    ADD PRIMARY KEY (x,y) NOT ENFORCED,
    ADD CONSTRAINT fk FOREIGN KEY (u, v) REFERENCES pk_table(x, y) NOT ENFORCED,
    ADD CONSTRAINT fk2 FOREIGN KEY (i, j) REFERENCES pk_table(x, y) NOT ENFORCED;
    ```

## `     ALTER TABLE ADD PRIMARY KEY    ` statement

Adds a [primary key](/bigquery/docs/primary-foreign-keys) to an existing table.

### Syntax

``` text
ALTER TABLE [[project_name.]dataset_name.]table_name
ADD PRIMARY KEY(column_list) NOT ENFORCED;
```

### Arguments

  - `  project_name  ` : The name of the project containing the table with a primary key. Defaults to the project that runs this DDL statement if undefined.
  - `  dataset_name  ` : The name of the dataset that contains the table with a primary key.
  - `  table_name  ` : The name of the existing table with a primary key.
  - `  column_list  ` : The list of columns to be added as primary keys.

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.tables.get      </code></td>
<td>The table to alter.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigquery.tables.update      </code></td>
<td>The table to alter.</td>
</tr>
</tbody>
</table>

### Examples

The following example adds the primary key constraint of `  x  ` and `  y  ` to the `  pk_table  ` table.

``` text
ALTER TABLE pk_table ADD PRIMARY KEY (x,y) NOT ENFORCED;
```

## `     ALTER TABLE RENAME TO    ` statement

Renames a clone, snapshot, or table.

The `  ALTER TABLE RENAME TO  ` statement recreates the table in the destination dataset with the creation timestamp of the original table. If you have configured [dataset-level table expiration](/bigquery/docs/updating-datasets#table-expiration) , the renamed table might be immediately deleted if its original creation timestamp falls outside of the expiration window.

**Caution:** Renaming a table deletes all [tags](/data-catalog/docs/tags-and-tag-templates#tags) (deprecated) or [aspects](/dataplex/docs/enrich-entries-metadata#aspects) that may be attached to it or its columns in [Data Catalog](/data-catalog) or [Dataplex Universal Catalog](/dataplex/docs/catalog-overview) , respectively.

### Syntax

``` text
ALTER TABLE [IF EXISTS] table_name
RENAME TO new_table_name
```

### Arguments

  - `  IF EXISTS  ` : If no table exists with that name, the statement has no effect.

  - `  table_name  ` : The name of the table to rename. See [Table path syntax](#table_path) .

  - `  new_table_name  ` : The new name of the table. The value of `  new_table_name  ` must only include the name of the table, not the full [table path syntax](#table_path) . The new name cannot be an existing table name.

### Details

  - If you want to rename a table that has data streaming into it, you must stop the streaming, commit any pending streams, and wait for BigQuery to indicate that streaming is not in use.
  - While a table can usually be renamed 5 hours after the last streaming operation, it might take longer.
  - Existing table ACLs and row access policies are preserved, but table ACL and row access policy updates made during the table rename are not preserved.
  - You can't concurrently rename a table and run a DML statement on that table.
  - Renaming a table removes all [Data Catalog tags](/data-catalog/docs/tags-and-tag-templates) (deprecated) and [Dataplex Universal Catalog aspects](/dataplex/docs/enrich-entries-metadata#aspects) on the table.
  - Any search index or vector index created on the table is dropped when the table is renamed.
  - You can't rename external tables.

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.tables.get      </code></td>
<td>The table to alter.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigquery.tables.update      </code></td>
<td>The table to alter.</td>
</tr>
</tbody>
</table>

### Examples

#### Renaming a table

The following example renames the table `  mydataset.mytable  ` to `  mydataset.mynewtable  ` :

``` text
ALTER TABLE mydataset.mytable RENAME TO mynewtable
```

## `     ALTER TABLE RENAME COLUMN    ` statement

**Caution:** Renaming a column deletes all [Data Catalog tags](/data-catalog/docs/tags-and-tag-templates#tags) (deprecated) and [Dataplex Universal Catalog aspects](/dataplex/docs/enrich-entries-metadata#aspects) that are attached to it. Primary key columns can't be renamed.

Renames one or more columns in an existing table schema.

### Syntax

``` text
ALTER TABLE [IF EXISTS] table_name
RENAME COLUMN [IF EXISTS] column_to_column[, ...]

column_to_column :=
    column_name TO new_column_name
```

### Arguments

  - `  (ALTER TABLE) IF EXISTS  ` : If the specified table does not exist, the statement has no effect.

  - `  table_name  ` : The name of the table to alter. See [Table path syntax](#table_path) .

  - `  (ALTER COLUMN) IF EXISTS  ` : If the specified column does not exist, the statement has no effect.

  - `  column_name  ` : The name of the top-level column you're altering.

  - `  new_column_name  ` : The new name of the column. The new name cannot be an existing column name.

### Details

This statement is not supported for [external tables](/bigquery/docs/external-tables) .

If the table to be modified has active row-level access policies, the statement returns an error.

Without the `  IF EXISTS  ` clause, if the table does not contain a column with that name, then the statement returns an error. If the `  IF EXISTS  ` clause is included and the column name does not exist, then no error is returned, and no action is taken.

This statement only renames the column from the table. Any objects that refer to the column, such as views or materialized views, must be updated or recreated separately.

You cannot use this statement to rename the following:

  - Subfields, such as nested columns in a `  STRUCT  `
  - Partitioning columns
  - Clustering columns
  - Fields that are part of primary key constraints or foreign key constraints
  - Columns in a table that has row access policies

After one or more columns in a table are renamed, you cannot do the following:

  - Query the table with legacy SQL.
  - Query the table as a wildcard table.

Renaming the columns with their original names removes these restrictions.

Multiple `  RENAME COLUMN  ` statements in one `  ALTER TABLE  ` statement are supported. The sequence of renames are interpreted and validated in order. Each `  column_name  ` must refer to a column name that exists after all preceding renames have been applied. `  RENAME COLUMN  ` cannot be used with other `  ALTER TABLE  ` actions in one statement.

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.tables.get      </code></td>
<td>The table to alter.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigquery.tables.update      </code></td>
<td>The table to alter.</td>
</tr>
</tbody>
</table>

### Examples

#### Renaming columns

The following example renames columns from an existing table named `  mytable  ` :

  - Column `  A  ` -\> `  columnA  `
  - Column `  B  ` -\> `  columnB  `

<!-- end list -->

``` text
ALTER TABLE mydataset.mytable
  RENAME COLUMN A TO columnA,
  RENAME COLUMN IF EXISTS B TO columnB
```

If column `  A  ` does not exist, then the statement fails. If column `  B  ` does not exist, then the statement still succeeds because of the `  IF EXISTS  ` clause.

The following example swaps the names of `  columnA  ` and `  columnB  ` :

``` text
ALTER TABLE mydataset.mytable
  RENAME COLUMN columnA TO temp_col,
  RENAME COLUMN columnB TO columnA,
  RENAME COLUMN temp_col TO columnB
```

## `     ALTER TABLE DROP COLUMN    ` statement

Drops one or more columns from an existing table schema.

### Syntax

``` text
ALTER TABLE table_name
DROP COLUMN [IF EXISTS] column_name [, ...]
```

### Arguments

  - `  table_name  ` : The name of the table to alter. See [Table path syntax](#table_path) . The table must already exist and have a schema.

  - `  IF EXISTS  ` : If the specified column does not exist, the statement has no effect.

  - `  column_name  ` : The name of the column to drop.

### Details

Dropping a column is a metadata-only operation and does not immediately free up the storage that is associated with the dropped column. The storage is freed up the next time the table is written to, typically when you perform a DML operation on it or when a background optimzation job happens. Since `  DROP COLUMN  ` is not a data cleanup operation, there is no guaranteed time window within which the data will be deleted.

There are two options for immediately reclaiming storage:

  - Overwrite a table with a `  SELECT * EXCEPT  ` query.
  - Export the data to Cloud Storage, delete the unwanted columns, and then load the data into a new table with the correct schema.

You can restore a dropped column in a table using [time travel](/bigquery/docs/access-historical-data#restore-a-table) . You cannot use this statement to drop the following:

  - Partitioned columns
  - Clustered columns
  - Fields that are part of [primary key constraints or foreign key constraints](/bigquery/docs/primary-foreign-keys)
  - Nested columns inside existing `  RECORD  ` fields
  - Columns in a table that has row access policies

After one or more columns in a table are dropped you cannot do the following:

  - Query the table with legacy SQL.
  - Query the table as a wildcard table.

This statement is not supported for [external tables](/bigquery/docs/external-tables) .

Without the `  IF EXISTS  ` clause, if the table does not contain a column with that name, then the statement returns an error. If the `  IF EXISTS  ` clause is included and the column name does not exist, then no error is returned, and no action is taken.

This statement only removes the column from the table. Any objects that refer to the column, such as views or materialized views, must be updated or recreated separately.

For more information about schema modifications in BigQuery, see [Modifying table schemas](/bigquery/docs/managing-table-schemas) .

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.tables.get      </code></td>
<td>The table to alter.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigquery.tables.update      </code></td>
<td>The table to alter.</td>
</tr>
</tbody>
</table>

### Examples

#### Dropping columns

The following example drops the following columns from an existing table named `  mytable  ` :

  - Column `  A  `
  - Column `  B  `

<!-- end list -->

``` text
ALTER TABLE mydataset.mytable
  DROP COLUMN A,
  DROP COLUMN IF EXISTS B
```

If the column named `  A  ` does not exist, then the statement fails. If column `  B  ` does not exist, then the statement still succeeds because of the `  IF EXISTS  ` clause.

After one or more columns in a table are dropped, you cannot do the following:

  - Query the table with legacy SQL.
  - Accelerate queries on the table with BigQuery BI Engine.
  - Query the table as a Wildcard Table.
  - Copy the table in the Google Cloud console.
  - Copy the table using the [`  bq cp  `](/bigquery/docs/reference/bq-cli-reference#bq_cp) command.

Recreating the table using `  CREATE TABLE ... AS SELECT ...  ` removes these restrictions.

## `     ALTER TABLE DROP CONSTRAINT    ` statement

Drops a constraint from an existing table. You can use this statement to drop [foreign key constraints](/bigquery/docs/primary-foreign-keys) from a table.

### Syntax

``` text
ALTER TABLE [[project_name.]dataset_name.]table_name
DROP CONSTRAINT [IF EXISTS] constraint_name;
```

### Arguments

  - `  project_name  ` : The name of the project containing the table with a primary key. Defaults to the project that runs this DDL statement if undefined.
  - `  dataset_name  ` : The name of the dataset that contains the table with a primary key.
  - `  table_name  ` : The name of the existing table with a primary key.
  - `  IF EXISTS  ` : If no primary key exists in the defined table, the statement has no effect.
  - `  constraint_name  ` : The name of the constraint to drop.

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.tables.get      </code></td>
<td>The table to alter.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigquery.tables.update      </code></td>
<td>The table to alter.</td>
</tr>
</tbody>
</table>

### Examples

The following example drops the constraint `  myConstraint  ` from the existing table `  myTable  ` .

``` text
ALTER TABLE mytable DROP CONSTRAINT myConstraint;
```

## `     ALTER TABLE DROP PRIMARY KEY    ` statement

Drops a [primary key](/bigquery/docs/primary-foreign-keys) from an existing table.

### Syntax

``` text
ALTER TABLE [[project_name.]dataset_name.]table_name
DROP PRIMARY KEY [IF EXISTS];
```

### Arguments

  - `  project_name  ` : The name of the project containing the table with a primary key. Defaults to the project that runs this DDL statement if undefined.
  - `  dataset_name  ` : The name of the dataset that contains the table with a primary key.
  - `  table_name  ` : The name of the existing table with a primary key.
  - `  IF EXISTS  ` : If no primary key exists in the defined table, the statement has no effect.

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.tables.get      </code></td>
<td>The table to alter.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigquery.tables.update      </code></td>
<td>The table to alter.</td>
</tr>
</tbody>
</table>

### Examples

The following example drops all primary keys from the existing table `  myTable  ` .

``` text
ALTER TABLE myTable
DROP PRIMARY KEY;
```

## `     ALTER TABLE SET DEFAULT COLLATE    ` statement

Sets [collation specifications](/bigquery/docs/reference/standard-sql/collation-concepts#collate_spec_details) on a table.

### Syntax

``` text
ALTER TABLE
  table_name
  SET DEFAULT COLLATE collate_specification
```

### Arguments

  - `  table_name  ` : The name of the table to alter. See [Table path syntax](#table_path) . The table must already exist and have a schema.

  - `  SET DEFAULT COLLATE collate_specification  ` : When a new column is created in the schema, and if the column does not have an explicit [collation specification](/bigquery/docs/reference/standard-sql/collation-concepts#default_collation) , the [column](#column_name_and_column_schema) inherits this collation specification for `  STRING  ` types. The updated collation specification only applies to columns added afterwards.
    
    If you want to add a collation specification on a new column in an existing table, you can do this when you [add the column](#alter_table_add_column_statement) . If you add a collation specification directly on a column, the collation specification for the column has precedence over a table's default collation specification. You cannot update an existing collation specification on a column.

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.tables.get      </code></td>
<td>The table to alter.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigquery.tables.update      </code></td>
<td>The table to alter.</td>
</tr>
</tbody>
</table>

### Example

Assume you have an existing table, `  mytable  ` , in a schema called `  mydataset  ` .

``` text
CREATE TABLE mydataset.mytable
(
  number INT64,
  word STRING
) DEFAULT COLLATE 'und:ci'
```

When you create `  mytable  ` , all `  STRING  ` columns inherit `  COLLATE 'und:ci'  ` . The resulting table has this structure:

``` text
+--------------------------------+
| mydataset.mytable              |
|   number INT64                 |
|   word STRING COLLATE 'und:ci' |
+--------------------------------+
```

At a later time, you decide to change the collation specification for your table.

``` text
ALTER TABLE mydataset.mytable
SET DEFAULT COLLATE ''
```

Although you have updated the collation specification, your existing column, `  word  ` , continues to use the previous collation specification.

``` text
+--------------------------------+
| mydataset.mytable              |
|   number INT64                 |
|   word STRING COLLATE 'und:ci' |
+--------------------------------+
```

However, if you create a new column for your table, the new column includes the new collation specification. In the following example a column called `  name  ` is added. Because the new collation specification is empty, the default collation specification is used.

``` text
ALTER TABLE mydataset.mytable
ADD COLUMN name STRING
```

``` text
+--------------------------------+
| mydataset.mytable              |
|   number INT64                 |
|   word STRING COLLATE 'und:ci' |
|   name STRING COLLATE          |
+--------------------------------+
```

## `     ALTER COLUMN SET OPTIONS    ` statement

Sets options, such as the column description, on a column in a table or view in BigQuery.

### Syntax

``` text
ALTER { TABLE | VIEW } [IF EXISTS] name
ALTER COLUMN [IF EXISTS] column_name
SET OPTIONS({ column_set_options_list | view_column_set_options_list })
```

### Arguments

  - `  (ALTER { TABLE | VIEW }) IF EXISTS  ` : If no table or view exists with that name, then the statement has no effect.

  - `  name  ` : The name of the table or view to alter. See [Table path syntax](#table_path) .

  - `  (ALTER COLUMN) IF EXISTS  ` : If the specified column does not exist, the statement has no effect.

  - `  column_name  ` : The name of the top-level column you're altering. Modifying subfields, such as nested columns in a `  STRUCT  ` , is not supported.

  - [`  column_set_options_list  `](#column_set_options_list) : The list of options to set on the column of the table. This option must be used with `  TABLE  ` .

  - [`  view_column_set_options_list  `](#view_column_set_options_list) : The list of options to set on the column of the view. This option must be used with `  VIEW  ` .

### Details

This statement is not supported for [external tables](/bigquery/docs/external-tables) .

### `     column_set_options_list    `

Specify a column option list in the following format:

`  NAME=VALUE, ...  `

`  NAME  ` and `  VALUE  ` must be one of the following combinations:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">       NAME      </code></th>
<th><code dir="ltr" translate="no">       VALUE      </code></th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       description      </code></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>Example: <code dir="ltr" translate="no">        description="a unique id"       </code></p>
<p>This property is equivalent to the <a href="/bigquery/docs/reference/rest/v2/tables#TableFieldSchema.FIELDS.description">schema.fields[].description</a> table resource property.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       rounding_mode      </code></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>Example: <code dir="ltr" translate="no">        rounding_mode = "ROUND_HALF_EVEN"       </code></p>
<p>This specifies the <a href="/bigquery/docs/schemas#rounding_mode">rounding mode</a> that's used for values written to a <code dir="ltr" translate="no">        NUMERIC       </code> or <code dir="ltr" translate="no">        BIGNUMERIC       </code> type column or <code dir="ltr" translate="no">        STRUCT       </code> field. The following values are supported:</p>
<ul>
<li><code dir="ltr" translate="no">         "ROUND_HALF_AWAY_FROM_ZERO"        </code> : Halfway cases are rounded away from zero. For example, 2.25 is rounded to 2.3, and -2.25 is rounded to -2.3.</li>
<li><code dir="ltr" translate="no">         "ROUND_HALF_EVEN"        </code> : Halfway cases are rounded towards the nearest even digit. For example, 2.25 is rounded to 2.2 and -2.25 is rounded to -2.2.</li>
</ul>
<p>This property is equivalent to the <a href="/bigquery/docs/reference/rest/v2/tables#TableFieldSchema.FIELDS.rounding_mode"><code dir="ltr" translate="no">         roundingMode        </code></a> table resource property.</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       data_policies      </code></td>
<td><code dir="ltr" translate="no">       ARRAY&lt;STRING&gt;      </code></td>
<td><p>Applies a <a href="/bigquery/docs/column-data-masking#create_data_policies">data policy</a> to a column in a table.</p>
<p>Example: <code dir="ltr" translate="no">        data_policies = ["{'name':'myproject.region-us.data_policy_name1'}",                                           "{'name':'myproject.region-us.data_policy_name2'}"]       </code></p>
<p>The <a href="/bigquery/docs/reference/standard-sql/data-definition-language#alter_column_set_data_type_statement"><code dir="ltr" translate="no">         ALTER TABLE ALTER COLUMN        </code></a> statement supports the <code dir="ltr" translate="no">        =       </code> and <code dir="ltr" translate="no">        +=       </code> operators to add data policies to a specific column.</p>
<p>Example: <code dir="ltr" translate="no">        data_policies +=["data_policy1", "data_policy2"]       </code></p></td>
</tr>
</tbody>
</table>

`  VALUE  ` is a constant expression containing only literals, query parameters, and scalar functions.

The constant expression **cannot** contain:

  - A reference to a table
  - Subqueries or SQL statements such as `  SELECT  ` , `  CREATE  ` , or `  UPDATE  `
  - User-defined functions, aggregate functions, or analytic functions
  - The following scalar functions:
      - `  ARRAY_TO_STRING  `
      - `  REPLACE  `
      - `  REGEXP_REPLACE  `
      - `  RAND  `
      - `  FORMAT  `
      - `  LPAD  `
      - `  RPAD  `
      - `  REPEAT  `
      - `  SESSION_USER  `
      - `  GENERATE_ARRAY  `
      - `  GENERATE_DATE_ARRAY  `

Setting the `  VALUE  ` replaces the existing value of that option for the column, if there was one. Setting the `  VALUE  ` to `  NULL  ` clears the column's value for that option.

### `     view_column_set_options_list    `

The `  view_column_option_list  ` lets you specify optional top-level column options. Column options for a view have the same syntax and requirements as for a table, but with a different list of `  NAME  ` and `  VALUE  ` fields:

<table>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">       NAME      </code></th>
<th><code dir="ltr" translate="no">       VALUE      </code></th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       description      </code></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>Example: <code dir="ltr" translate="no">        description="a unique id"       </code></p></td>
</tr>
</tbody>
</table>

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.tables.get      </code></td>
<td>The table to alter.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigquery.tables.update      </code></td>
<td>The table to alter.</td>
</tr>
</tbody>
</table>

### Examples

The following example sets a new description on a table column called `  price  ` :

``` text
ALTER TABLE mydataset.mytable
ALTER COLUMN price
SET OPTIONS (description = 'Price per unit');
```

The following example sets a new description on a view column called `  total  ` :

``` text
ALTER VIEW mydataset.myview
ALTER COLUMN total
SET OPTIONS (description = 'Total sales of the product');
```

## `     ALTER COLUMN DROP NOT NULL    ` statement

Removes a `  NOT NULL  ` constraint from a column in a table in BigQuery.

### Syntax

``` text
ALTER TABLE [IF EXISTS] table_name
ALTER COLUMN [IF EXISTS] column DROP NOT NULL
```

### Arguments

  - `  (ALTER TABLE) IF EXISTS  ` : If no table exists with that name, the statement has no effect.

  - `  table_name  ` : The name of the table to alter. See [Table path syntax](#table_path) .

  - `  (ALTER COLUMN) IF EXISTS  ` : If the specified column does not exist, the statement has no effect.

  - `  column_name  ` : The name of the top level column you're altering. Modifying subfields is not supported.

### Details

If a column does not have a `  NOT NULL  ` constraint the query returns an error.

This statement is not supported for [external tables](/bigquery/docs/external-tables) .

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.tables.get      </code></td>
<td>The table to alter.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigquery.tables.update      </code></td>
<td>The table to alter.</td>
</tr>
</tbody>
</table>

### Examples

The following example removes the `  NOT NULL  ` constraint from a column called `  mycolumn  ` :

``` text
ALTER TABLE mydataset.mytable
ALTER COLUMN mycolumn
DROP NOT NULL
```

## `     ALTER COLUMN SET DATA TYPE    ` statement

Changes the data type of a column in a table in BigQuery to a less restrictive data type. For example, a `  NUMERIC  ` data type can be changed to a `  BIGNUMERIC  ` type but not the reverse.

### Syntax

``` text
ALTER TABLE [IF EXISTS] table_name
ALTER COLUMN [IF EXISTS] column_name SET DATA TYPE column_schema
```

### Arguments

  - `  (ALTER TABLE) IF EXISTS  ` : If no table exists with that name, the statement has no effect.

  - `  table_name  ` : The name of the table to alter. See [Table path syntax](#table_path) .

  - `  (ALTER COLUMN) IF EXISTS  ` : If the specified column does not exist, the statement has no effect.

  - `  column_name  ` : The name of the top level column you're altering. Modifying subfields is not supported.

  - `  column_schema  ` : The schema that you're converting the column to. This schema uses the same syntax used in the [`  CREATE TABLE  `](#create_table_statement) statement.

### Details

The following data type conversions are supported: :

  - `  INT64  ` to `  NUMERIC  ` , `  BIGNUMERIC  ` , `  FLOAT64  `
  - `  NUMERIC  ` to `  BIGNUMERIC  ` , `  FLOAT64  `

You can also convert data types from more restrictive to less restrictive [parameterized data types](/bigquery/docs/reference/standard-sql/data-types#parameterized_data_types) . For example, you can increase the maximum length of a string type or increase the precision or scale of a numeric type.

The following are examples of valid parameterized data type conversions:

  - `  NUMERIC(10, 6)  ` to `  NUMERIC(12, 8)  `
  - `  NUMERIC  ` to `  BIGNUMERIC(40, 20)  `
  - `  STRING(5)  ` to `  STRING(7)  `

This statement is not supported for [external tables](/bigquery/docs/external-tables) .

Without the `  IF EXISTS  ` clause, if the table does not contain a column with that name, the statement returns an error. If the `  IF EXISTS  ` clause is included and the column name does not exist, no error is returned, and no action is taken.

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.tables.get      </code></td>
<td>The table to alter.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigquery.tables.update      </code></td>
<td>The table to alter.</td>
</tr>
</tbody>
</table>

### Examples

#### Changing the data type for a column

The following example changes the data type of column `  c1  ` from an `  INT64  ` to `  NUMERIC  ` :

``` text
CREATE TABLE dataset.my_table(c1 INT64);

ALTER TABLE dataset.my_table ALTER COLUMN c1 SET DATA TYPE NUMERIC;
```

#### Changing the data type for a field

The following example changes the data type of one of the fields in the `  s1  ` column:

``` text
CREATE TABLE dataset.my_table(s1 STRUCT <a INT64, b STRING>);

ALTER TABLE dataset.my_table ALTER COLUMN s1
SET DATA TYPE STRUCT <a NUMERIC, b STRING>;
```

#### Changing precision

The following example changes the precision of a parameterized data type column:

``` text
CREATE TABLE dataset.my_table (pt NUMERIC(7,2));

ALTER TABLE dataset.my_table
ALTER COLUMN pt
SET DATA TYPE NUMERIC(8,2);
```

## `     ALTER COLUMN SET DEFAULT    ` statement

Sets the [default value](/bigquery/docs/default-values) of a column.

### Syntax

``` text
ALTER TABLE [IF EXISTS] table_name ALTER COLUMN [IF EXISTS] column_name
SET DEFAULT default_expression;
```

### Arguments

  - `  (ALTER TABLE) IF EXISTS  ` : If the specified table does not exist, the statement has no effect.

  - `  table_name  ` : The name of the table to alter. See [Table path syntax](#table_path) .

  - `  (ALTER COLUMN) IF EXISTS  ` : If the specified column does not exist, the statement has no effect.

  - `  column_name  ` : The name of the top-level column to add a default value to.

  - `  default_expression  ` : The default value assigned to the column. The expression must be a [literal](/bigquery/docs/reference/standard-sql/lexical#literals) or one of the following functions:
    
      - [`  CURRENT_DATE  `](/bigquery/docs/reference/standard-sql/date_functions#current_date)
      - [`  CURRENT_DATETIME  `](/bigquery/docs/reference/standard-sql/datetime_functions#current_datetime)
      - [`  CURRENT_TIME  `](/bigquery/docs/reference/standard-sql/time_functions#current_time)
      - [`  CURRENT_TIMESTAMP  `](/bigquery/docs/reference/standard-sql/timestamp_functions#current_timestamp)
      - [`  GENERATE_UUID  `](/bigquery/docs/reference/standard-sql/utility-functions#generate_uuid)
      - [`  RAND  `](/bigquery/docs/reference/standard-sql/mathematical_functions#rand)
      - [`  SESSION_USER  `](/bigquery/docs/reference/standard-sql/security_functions#session_user)
      - [`  ST_GEOGPOINT  `](/bigquery/docs/reference/standard-sql/geography_functions#st_geogpoint)

### Details

Setting the default value for a column only affects future inserts to the table. It does not change any existing table data.

The type of the default value must match the type of the column. A `  STRUCT  ` type can only have a default value set for the entire `  STRUCT  ` field. You cannot set the default value for a subset of the fields. You cannot set the default value of an array to `  NULL  ` or set an element within an array to `  NULL  ` .

If the default value is a function, it is evaluated at the time that the value is written to the table, not the time the table is created.

You can't set default values on columns that are [primary keys](/bigquery/docs/primary-foreign-keys) .

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.tables.get      </code></td>
<td>The table to alter.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigquery.tables.update      </code></td>
<td>The table to alter.</td>
</tr>
</tbody>
</table>

### Examples

The following example sets the default value of the column `  mycolumn  ` to the current time:

``` text
ALTER TABLE mydataset.mytable
ALTER COLUMN mycolumn
SET DEFAULT CURRENT_TIME();
```

## `     ALTER COLUMN DROP DEFAULT    ` statement

Removes the [default value](/bigquery/docs/default-values) assigned to a column. This is the same as setting the default value to `  NULL  ` .

### Syntax

``` text
ALTER TABLE [IF EXISTS] table_name ALTER COLUMN [IF EXISTS] column_name
DROP DEFAULT;
```

### Arguments

  - `  (ALTER TABLE) IF EXISTS  ` : If the specified table does not exist, the statement has no effect.

  - `  table_name  ` : The name of the table to alter. See [Table path syntax](#table_path) .

  - `  (ALTER COLUMN) IF EXISTS  ` : If the specified column does not exist, the statement has no effect.

  - `  column_name  ` : The name of the top-level column to remove the default value from. If you drop the default value from a column that does not have a default set, an error is returned.

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.tables.get      </code></td>
<td>The table to alter.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigquery.tables.update      </code></td>
<td>The table to alter.</td>
</tr>
</tbody>
</table>

### Examples

The following example removes the default value from the column `  mycolumn  ` :

``` text
ALTER TABLE mydataset.mytable
ALTER COLUMN mycolumn
DROP DEFAULT;
```

## `     ALTER VIEW SET OPTIONS    ` statement

Sets the options on a [view](/bigquery/docs/views) .

### Syntax

``` text
ALTER VIEW [IF EXISTS] view_name
SET OPTIONS(view_set_options_list)
```

### Arguments

  - `  IF EXISTS  ` : If no view exists with that name, the statement has no effect.

  - `  view_name  ` : The name of the view to alter. See [Table path syntax](#table_path) .

  - [`  view_set_options_list  `](#view_set_options_list) : The list of options to set.

### `     view_set_options_list    `

The option list allows you to set view options such as a [label](/bigquery/docs/labels) and an expiration time. You can include multiple options using a comma-separated list.

Specify a view option list in the following format:

`  NAME=VALUE, ...  `

`  NAME  ` and `  VALUE  ` must be one of the following combinations:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">       NAME      </code></th>
<th><code dir="ltr" translate="no">       VALUE      </code></th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       expiration_timestamp      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td><p>Example: <code dir="ltr" translate="no">        expiration_timestamp=TIMESTAMP "2025-01-01 00:00:00 UTC"       </code></p>
<p>This property is equivalent to the <a href="/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.expiration_time">expirationTime</a> table resource property.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       friendly_name      </code></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>Example: <code dir="ltr" translate="no">        friendly_name="my_view"       </code></p>
<p>This property is equivalent to the <a href="/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.friendly_name">friendlyName</a> table resource property.</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       description      </code></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>Example: <code dir="ltr" translate="no">        description="a view that expires in 2025"       </code></p>
<p>This property is equivalent to the <a href="/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.description">description</a> table resource property.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       labels      </code></td>
<td><p><code dir="ltr" translate="no">        ARRAY&lt;STRUCT&lt;STRING, STRING&gt;&gt;       </code></p></td>
<td><p>Example: <code dir="ltr" translate="no">        labels=[("org_unit", "development")]       </code></p>
<p>This property is equivalent to the <a href="/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.labels">labels</a> table resource property.</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       privacy_policy      </code></td>
<td><p><code dir="ltr" translate="no">        JSON-formatted STRING       </code></p></td>
<td><p>The policies to enforce when anyone queries the view. To learn more about the policies available for a view, see the <a href="/bigquery/docs/reference/standard-sql/data-definition-language#privacy_policy"><code dir="ltr" translate="no">         privacy_policy        </code></a> view option.</p>
<strong>Note:</strong> Time travel is disabled on any view that has an analysis rule.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       tags      </code></td>
<td><code dir="ltr" translate="no">       &lt;ARRAY&lt;STRUCT&lt;STRING, STRING&gt;&gt;&gt;      </code></td>
<td>An array of IAM tags for the view, expressed as key-value pairs. The key should be the <a href="/iam/docs/tags-access-control#definitions">namespaced key name</a> , and the value should be the <a href="/iam/docs/tags-access-control#definitions">short name</a> .</td>
</tr>
</tbody>
</table>

`  VALUE  ` is a constant expression containing only literals, query parameters, and scalar functions.

The constant expression **cannot** contain:

  - A reference to a table
  - Subqueries or SQL statements such as `  SELECT  ` , `  CREATE  ` , or `  UPDATE  `
  - User-defined functions, aggregate functions, or analytic functions
  - The following scalar functions:
      - `  ARRAY_TO_STRING  `
      - `  REPLACE  `
      - `  REGEXP_REPLACE  `
      - `  RAND  `
      - `  FORMAT  `
      - `  LPAD  `
      - `  RPAD  `
      - `  REPEAT  `
      - `  SESSION_USER  `
      - `  GENERATE_ARRAY  `
      - `  GENERATE_DATE_ARRAY  `

Setting the value replaces the existing value of that option for the view, if there was one. Setting the value to `  NULL  ` clears the view's value for that option.

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.tables.get      </code></td>
<td>The view to alter.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigquery.tables.update      </code></td>
<td>The view to alter.</td>
</tr>
</tbody>
</table>

### Examples

#### Setting the expiration timestamp and description on a view

The following example sets the expiration timestamp on a view to seven days from the execution time of the `  ALTER VIEW  ` statement, and sets the description as well:

``` text
ALTER VIEW mydataset.myview
SET OPTIONS (
  expiration_timestamp=TIMESTAMP_ADD(CURRENT_TIMESTAMP(), INTERVAL 7 DAY),
  description="View that expires seven days from now"
)
```

## `     ALTER MATERIALIZED VIEW SET OPTIONS    ` statement

Sets the options on a materialized view.

### Syntax

``` text
ALTER MATERIALIZED VIEW [IF EXISTS] materialized_view_name
SET OPTIONS(materialized_view_set_options_list)
```

### Arguments

  - `  IF EXISTS  ` : If no materialized view exists with that name, the statement has no effect.

  - `  materialized_view_name  ` : The name of the materialized view to alter. See [Table path syntax](#table_path) .

  - [`  materialized_view_set_options_list  `](#materialized_view_set_options_list) : The list of options to set.

### `     materialized_view_set_options_list    `

The option list allows you to set materialized view options such as a whether refresh is enabled. the refresh interval, a [label](/bigquery/docs/labels) and an expiration time. You can include multiple options using a comma-separated list.

Specify a materialized view option list in the following format:

`  NAME=VALUE, ...  `

`  NAME  ` and `  VALUE  ` must be one of the following combinations:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">       NAME      </code></th>
<th><code dir="ltr" translate="no">       VALUE      </code></th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       enable_refresh      </code></td>
<td><code dir="ltr" translate="no">       BOOLEAN      </code></td>
<td><p>Example: <code dir="ltr" translate="no">        enable_refresh=false       </code><br />
Default: <code dir="ltr" translate="no">        true       </code></p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       refresh_interval_minutes      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
<td><p>Example: <code dir="ltr" translate="no">        refresh_interval_minutes=20       </code><br />
Default: <code dir="ltr" translate="no">        refresh_interval_minutes=30       </code></p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       expiration_timestamp      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td><p>Example: <code dir="ltr" translate="no">        expiration_timestamp=TIMESTAMP "2025-01-01 00:00:00 UTC"       </code></p>
<p>This property is equivalent to the <a href="/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.expiration_time">expirationTime</a> table resource property. <code dir="ltr" translate="no">        expiration_timestamp       </code> is optional and not used by default.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       max_staleness      </code></td>
<td><code dir="ltr" translate="no">       INTERVAL      </code></td>
<td><p>Example: <code dir="ltr" translate="no">        max_staleness=INTERVAL "4:0:0" HOUR TO SECOND       </code></p>
<p>The <a href="/bigquery/docs/materialized-views-create#max_staleness"><code dir="ltr" translate="no">         max_staleness        </code> property</a> provides consistently high performance with controlled costs when processing large, frequently changing datasets. <code dir="ltr" translate="no">        max_staleness       </code> is disabled by default.</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       allow_non_incremental_definition      </code></td>
<td><code dir="ltr" translate="no">       BOOLEAN      </code></td>
<td><p>Example: <code dir="ltr" translate="no">        allow_non_incremental_definition=true       </code></p>
<p>The <a href="/bigquery/docs/materialized-views-create#non-incremental"><code dir="ltr" translate="no">         allow_non_incremental_definition        </code> property</a> supports an expanded range of SQL queries to create materialized views. <code dir="ltr" translate="no">        allow_non_incremental_definition=true       </code> is disabled by default. <code dir="ltr" translate="no">        CREATE MATERIALIZED VIEW       </code> statement support only. The <code dir="ltr" translate="no">        allow_non_incremental_definition       </code> property can't be changed after the materialized view is created.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       kms_key_name      </code></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>Example: <code dir="ltr" translate="no">        kms_key_name="projects/                 project_id                /locations/       </code> <code dir="ltr" translate="no">          location                /keyRings/                 keyring                /cryptoKeys/                 key                "       </code></p>
<p>This property is equivalent to the <a href="/bigquery/docs/reference/rest/v2/EncryptionConfiguration#FIELDS.kms_key_name">encryptionConfiguration.kmsKeyName</a> table resource property.</p>
<p>See more details about <a href="/bigquery/docs/customer-managed-encryption">Protecting data with Cloud KMS keys</a> .</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       friendly_name      </code></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>Example: <code dir="ltr" translate="no">        friendly_name="my_mv"       </code></p>
<p>This property is equivalent to the <a href="/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.friendly_name">friendlyName</a> table resource property.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       description      </code></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><p>Example: <code dir="ltr" translate="no">        description="a materialized view that expires in 2025"       </code></p>
<p>This property is equivalent to the <a href="/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.description">description</a> table resource property.</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       labels      </code></td>
<td><p><code dir="ltr" translate="no">        ARRAY&lt;STRUCT&lt;STRING, STRING&gt;&gt;       </code></p></td>
<td><p>Example: <code dir="ltr" translate="no">        labels=[("org_unit", "development")]       </code></p>
<p>This property is equivalent to the <a href="/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.labels">labels</a> table resource property.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       tags      </code></td>
<td><code dir="ltr" translate="no">       ARRAY&lt;STRUCT&lt;STRING, STRING&gt;&gt;      </code></td>
<td>An array of IAM tags for the materialized view, expressed as key-value pairs. The key should be the <a href="/iam/docs/tags-access-control#definitions">namespaced key name</a> , and the value should be the <a href="/iam/docs/tags-access-control#definitions">short name</a> .</td>
</tr>
</tbody>
</table>

Setting the value replaces the existing value of that option for the materialized view, if there was one. Setting the value to `  NULL  ` clears the materialized view's value for that option.

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.tables.get      </code></td>
<td>The materialized view to alter.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigquery.tables.update      </code></td>
<td>The materialized view to alter.</td>
</tr>
</tbody>
</table>

### Examples

#### Setting the enable refresh state and refresh interval on a materialized view

The following example enables refresh and sets the refresh interval to 20 minutes on a materialized view:

``` text
ALTER MATERIALIZED VIEW mydataset.my_mv
SET OPTIONS (
  enable_refresh=true,
  refresh_interval_minutes=20
)
```

## `     ALTER ORGANIZATION SET OPTIONS    ` statement

Sets the options on an organization.

### Syntax

``` text
ALTER ORGANIZATION
SET OPTIONS (
  organization_set_options_list);
```

### Arguments

  - [`  organization_set_options_list  `](#organziation_set_options_list) : The list of options to set.

### `     organization_set_options_list    `

The option list specifies options for the organization. Specify the options in the following format: `  NAME=VALUE, ...  `

The following options are supported:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">       NAME      </code></th>
<th><code dir="ltr" translate="no">       VALUE      </code></th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       default_kms_key_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><p>The default Cloud Key Management Service key for encrypting table data, including temporary or anonymous tables. For more information, see <a href="/bigquery/docs/customer-managed-encryption">Customer-managed Cloud KMS keys</a> .</p>
<p>Example: <code dir="ltr" translate="no">        kms_key_name="projects/                 project_id                /locations/       </code> <code dir="ltr" translate="no">          location                /keyRings/                 keyring                /cryptoKeys/                 key                "       </code></p>
<p>This property is equivalent to the <a href="/bigquery/docs/reference/rest/v2/EncryptionConfiguration#FIELDS.kms_key_name"><code dir="ltr" translate="no">         encryptionConfiguration.kmsKeyName        </code></a> table resource property.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       default_time_zone      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><p>The default time zone to use in time zone-dependent SQL functions, when a time zone is not specified as an argument. For more information, see <a href="/bigquery/docs/reference/standard-sql/data-types#time_zones">time zones</a> .</p>
<p>Example: <code dir="ltr" translate="no">        `region-us.default_time_zone` = "America/Los_Angeles"       </code> . Sets the default time zone to <code dir="ltr" translate="no">        America/Los_Angeles       </code> in the <code dir="ltr" translate="no">        us       </code> region.</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       default_query_job_timeout_ms      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td><p>The default time after which a query job times out. The timeout period must be between 5 minutes and 48 hours.</p>
<p>Example: <code dir="ltr" translate="no">        `region-us.default_query_job_timeout_ms` = 1800000       </code> . Sets the default query job timeout time to 30 minutes for all jobs in the <code dir="ltr" translate="no">        us       </code> region.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       default_interactive_query_queue_timeout_ms      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td><p>The default amount of time that an interactive query is queued. If unset, the default is 6 hours. The minimum value is 1 millisecond. The maximum value is 48 hours. To disable interactive query queueing, set the value to -1.</p>
<p>Example: <code dir="ltr" translate="no">        `region-us.default_interactive_query_queue_timeout_ms` = 1800000       </code> . Sets the default queue timeout for interactive queries in the <code dir="ltr" translate="no">        us       </code> region to 30 minutes.</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       default_batch_query_queue_timeout_ms      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td><p>The default amount of time that a batch query is queued. If unset, the default is 24 hours. The minimum value is 1 millisecond. The maximum value is 48 hours. To disable batch query queueing, set the value to -1.</p>
<p>Example: <code dir="ltr" translate="no">        `region-us.default_batch_query_queue_timeout_ms` = 1800000       </code> . Sets the default queue timeout for batch queries in the <code dir="ltr" translate="no">        us       </code> region to 30 minutes.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       default_query_optimizer_options      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><p>The history-based query optimizations. This option can be one of the following:</p>
<ul>
<li><code dir="ltr" translate="no">         'adaptive=on'        </code> : Use history-based query optimizations.</li>
<li><code dir="ltr" translate="no">         'adaptive=off'        </code> : Don't use history-based query optimizations.</li>
<li><code dir="ltr" translate="no">         NULL        </code> (default): Use the default history-based query optimizations setting, which is equivalent to <code dir="ltr" translate="no">         'adaptive=on'        </code> .</li>
</ul>
<p>Example: <code dir="ltr" translate="no">        `region-us.default_query_optimizer_options` = 'adaptive=on'       </code></p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       query_runtime      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><p>Specifies whether the BigQuery query processor uses the <a href="/bigquery/docs/advanced-runtime">advanced runtime</a> . Set the <code dir="ltr" translate="no">        query_runtime       </code> value to <code dir="ltr" translate="no">        advanced       </code> to enable the advanced runtime before it's rolled out as the default runtime.</p>
<p>Example: <code dir="ltr" translate="no">        `region-us.query_runtime` = 'advanced'       </code> . Enables the advanced runtime.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       enable_global_queries_execution      </code></td>
<td><code dir="ltr" translate="no">       BOOL      </code></td>
<td><p>Determines if <a href="/bigquery/docs/global-queries">global queries</a> can be run. The default value is <code dir="ltr" translate="no">        FALSE       </code> , which means that global queries are not enabled.</p>
<p>Example: <code dir="ltr" translate="no">        `region-us.enable_global_queries_execution` = true       </code> . Enables global queries.</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       enable_global_queries_data_access      </code></td>
<td><code dir="ltr" translate="no">       BOOL      </code></td>
<td><p>Determines if <a href="/bigquery/docs/global-queries">global queries</a> can access data stored in the region. The default value is <code dir="ltr" translate="no">        FALSE       </code> , which means that global queries can't copy data from this region regardless of the project in which they run.</p>
<p>Example: <code dir="ltr" translate="no">        `region-us.enable_global_queries_data_access` = true       </code> .</p></td>
</tr>
</tbody>
</table>

Setting the value replaces the existing value of that option for the organization, if there is one. Setting the value to `  NULL  ` clears the organization's value for that option.

### Required permissions

The `  ALTER ORGANIZATION SET OPTIONS  ` statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.config.update      </code></td>
<td>The organization to alter.</td>
</tr>
</tbody>
</table>

### Examples

The following example sets the default time zone to America/Chicago and the default query job timeout to one hour for an organization in the US region:

``` text
ALTER ORGANIZATION
SET OPTIONS (
  `region-us.default_time_zone` = "America/Chicago",
  `region-us.default_job_query_timeout_ms` = 3600000
);
```

The following example sets the default time zone, the default query job timeout, the default interactive and batch queue timeouts, and the default Cloud KMS key, clearing the organization level default settings:

``` text
ALTER ORGANIZATION
SET OPTIONS (
  `region-us.default_time_zone` = NULL,
  `region-us.default_kms_key_name` = NULL,
  `region-us.default_query_job_timeout_ms` = NULL,
  `region-us.default_interactive_query_queue_timeout_ms` = NULL,
  `region-us.default_batch_query_queue_timeout_ms` = NULL);
```

## `     ALTER PROJECT SET OPTIONS    ` statement

Sets the options on a project.

### Syntax

``` text
ALTER PROJECT project_id
SET OPTIONS (project_set_options_list);
```

### Arguments

  - `  project_id  ` : The name of the project you're altering. This argument is optional, and defaults to the project that runs this DDL query.
  - [`  project_set_options_list  `](#project_set_options_list) : The list of options to set.

### `     project_set_options_list    `

The option list specifies options for the project. Specify the options in the following format: `  NAME=VALUE, ...  `

The following options are supported:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">       NAME      </code></th>
<th><code dir="ltr" translate="no">       VALUE      </code></th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       default_kms_key_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><p>The default Cloud Key Management Service key for encrypting table data, including temporary or anonymous tables. For more information, see <a href="/bigquery/docs/customer-managed-encryption">Customer-managed Cloud KMS keys</a> .</p>
<p>Example: <code dir="ltr" translate="no">        kms_key_name="projects/                 project_id                /locations/                 location                /keyRings/                 keyring                /cryptoKeys/                 key                "       </code></p>
<p>This property is equivalent to the <a href="/bigquery/docs/reference/rest/v2/EncryptionConfiguration#FIELDS.kms_key_name"><code dir="ltr" translate="no">         encryptionConfiguration.kmsKeyName        </code></a> table resource property.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       default_time_zone      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><p>The default time zone to use in time zone-dependent SQL functions, when a time zone is not specified as an argument. For more information, see <a href="/bigquery/docs/reference/standard-sql/data-types#time_zones">time zones</a> .</p>
<p>Example: <code dir="ltr" translate="no">        `region-us.default_time_zone` = "America/Los_Angeles"       </code> . Sets the default time zone to <code dir="ltr" translate="no">        America/Los_Angeles       </code> in the <code dir="ltr" translate="no">        us       </code> region.</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       default_query_job_timeout_ms      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td><p>The default time after which a query job times out. The timeout period must be between 5 minutes and 48 hours.</p>
<p>Example: <code dir="ltr" translate="no">        `region-us.default_query_job_timeout_ms` = 1800000       </code> . Sets the default query job timeout time to 30 minutes for jobs run in the <code dir="ltr" translate="no">        us       </code> region.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       default_interactive_query_queue_timeout_ms      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td><p>The default amount of time that an interactive query is queued. If unset, the default is 6 hours. The minimum value is 1 millisecond. The maximum value is 48 hours. To disable interactive query queueing, set the value to -1.</p>
<p>Example: <code dir="ltr" translate="no">        `region-us.default_interactive_query_queue_timeout_ms` = 1800000       </code> . Sets the default queue timeout for interactive queries in the <code dir="ltr" translate="no">        us       </code> region to 30 minutes.</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       default_batch_query_queue_timeout_ms      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td><p>The default amount of time that a batch query is queued. If unset, the default is 24 hours. The minimum value is 1 millisecond. The maximum value is 48 hours. To disable batch query queueing, set the value to -1.</p>
<p>Example: <code dir="ltr" translate="no">        `region-us.default_batch_query_queue_timeout_ms` = 1800000       </code> . Sets the default queue timeout for batch queries in the <code dir="ltr" translate="no">        us       </code> region to 30 minutes.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       default_query_optimizer_options      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><p>The history-based query optimizations. This option can be one of the following:</p>
<ul>
<li><code dir="ltr" translate="no">         'adaptive=on'        </code> : Use history-based query optimizations.</li>
<li><code dir="ltr" translate="no">         'adaptive=off'        </code> : Don't use history-based query optimizations.</li>
<li><code dir="ltr" translate="no">         NULL        </code> (default): Use the default history-based query optimizations setting, which is equivalent to <code dir="ltr" translate="no">         'adaptive=on'        </code> .</li>
</ul>
<p>Example: <code dir="ltr" translate="no">        `region-us.default_query_optimizer_options` = 'adaptive=on'       </code></p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       default_cloud_resource_connection_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><p>The default connection to use when creating tables and models ([Preview](/products#product-launch-stages)). Only specify the connection's ID, and exclude the attached project ID and region prefixes. Using default connections can cause the permissions granted to the connection's service account to be updated, depending on the type of table or model you create. For more information, see the <a href="/bigquery/docs/default-connections">Default connection overview</a> .</p>
<p>Example: <code dir="ltr" translate="no">        `region-us.default_cloud_resource_connection_id` = "connection_1"       </code> . Sets the default connection to <code dir="ltr" translate="no">        connection_1       </code> in the <code dir="ltr" translate="no">        us       </code> region.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       default_sql_dialect_option      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><p>The default sql query dialect for executing query jobs using the bq command-line tool or BigQuery API. Changing this setting doesn't affect the default dialect in the console. This option can be one of the following:</p>
<ul>
<li><code dir="ltr" translate="no">         'default_legacy_sql'        </code> (default): Use legacy SQL if the query dialect isn't specified at the job level.</li>
<li><code dir="ltr" translate="no">         'default_google_sql'        </code> : Use GoogleSQL if the query dialect isn't specified at the job level.</li>
<li><code dir="ltr" translate="no">         'only_google_sql'        </code> : Use GoogleSQL if the query dialect is not specified at the job level. Reject jobs with query dialect set to legacy SQL.</li>
<li><code dir="ltr" translate="no">         'NULL'        </code> : Use the default query dialect setting, which is equivalent to <code dir="ltr" translate="no">         'default_legacy_sql'        </code> .</li>
</ul>
<p>Example: <code dir="ltr" translate="no">        `region-us.default_sql_dialect_option` = 'default_google_sql'       </code> . Use google SQL if the query dialect isn't specified at the job level.</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       query_runtime      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><p>Specifies whether the BigQuery query processor uses the <a href="/bigquery/docs/advanced-runtime">advanced runtime</a> . Set the <code dir="ltr" translate="no">        query_runtime       </code> value to <code dir="ltr" translate="no">        advanced       </code> to enable the advanced runtime before it's rolled out as the default runtime.</p>
<p>Example: <code dir="ltr" translate="no">        `region-us.query_runtime` = 'advanced'       </code> . Enables the advanced runtime.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       enable_reservation_based_fairness      </code></td>
<td><code dir="ltr" translate="no">       BOOL      </code></td>
<td><p>Determines how idle slots are shared. If <code dir="ltr" translate="no">        false       </code> (default), idle slots are equally distributed across all query projects. If <code dir="ltr" translate="no">        true       </code> , idle slots are shared equally across all reservations first, and then across projects within the reservation. For more information, see <a href="/bigquery/docs/slots#fairness">reservation-based fairness</a> .</p>
<p>Example: <code dir="ltr" translate="no">        `region-us.enable_reservation_based_fairness` = true       </code> . Enables reservation-based fairness.</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       enable_global_queries_execution      </code></td>
<td><code dir="ltr" translate="no">       BOOL      </code></td>
<td><p>Determines if <a href="/bigquery/docs/global-queries">global queries</a> can be run. The default value is <code dir="ltr" translate="no">        FALSE       </code> , which means that global queries are not enabled.</p>
<p>Example: <code dir="ltr" translate="no">        `region-us.enable_global_queries_execution` = true       </code> . Enables global queries.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       enable_global_queries_data_access      </code></td>
<td><code dir="ltr" translate="no">       BOOL      </code></td>
<td><p>Determines if <a href="/bigquery/docs/global-queries">global queries</a> can access data stored in the region. The default value is <code dir="ltr" translate="no">        FALSE       </code> , which means that global queries can't copy data from this region regardless of the project in which they run.</p>
<p>Example: <code dir="ltr" translate="no">        `region-us.enable_global_queries_data_access` = true       </code> .</p></td>
</tr>
</tbody>
</table>

Setting the value replaces the existing value of that option for the project, if there was one. Setting the value to `  NULL  ` clears the project's value for that option.

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.config.update      </code></td>
<td>The project to alter.</td>
</tr>
</tbody>
</table>

### Examples

The following example sets the default time zone to `  America/New_York  ` and the default query job timeout to 30 minutes for a project in the `  us  ` region.

``` text
ALTER PROJECT project_id
SET OPTIONS (
  `region-us.default_time_zone` = "America/New_York",
  `region-us.default_job_query_timeout_ms` = 1800000
);
```

The following example sets the default time zone, the default query job timeout, the default Cloud KMS key to `  NULL  ` , and the default interactive and batch queue timeouts and default sql dialect, clearing the project level default settings:

``` text
ALTER PROJECT project_id
SET OPTIONS (
  `region-us.default_time_zone` = NULL,
  `region-us.default_kms_key_name` = NULL,
  `region-us.default_query_job_timeout_ms` = NULL,
  `region-us.default_interactive_query_queue_timeout_ms` = NULL,
  `region-us.default_batch_query_queue_timeout_ms` = NULL,
  `region-us.default_sql_dialect_option` = NULL);
```

## `     ALTER BI_CAPACITY SET OPTIONS    ` statement

Sets the options on BigQuery BI Engine capacity.

### Syntax

``` text
ALTER BI_CAPACITY `project_id.location_id.default`
SET OPTIONS(bi_capacity_options_list)
```

### Arguments

  - `  project_id  ` : Optional project ID of the project that will benefit from BI Engine acceleration. If omitted, the query project ID is used.

  - `  location_id  ` : The [location](/bigquery/docs/locations#supported_locations) where data needs to be cached, prefixed with `  region-  ` . Examples: `  region-us  ` , `  region-us-central1  ` .

  - [`  bi_capacity_options_list  `](#bi_capacity_options_list) : The list of options to set.

### `     bi_capacity_options_list    `

The option list specifies a set of options for BigQuery BI Engine capacity.

Specify a column option list in the following format:

`  NAME=VALUE, ...  `

The following options are supported:

<table>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">       NAME      </code></th>
<th><code dir="ltr" translate="no">       VALUE      </code></th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       size_gb      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td>Specifies the size of the reservation in gigabytes.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       preferred_tables      </code></td>
<td><code dir="ltr" translate="no">       &lt;ARRAY&lt;STRING&gt;&gt;      </code></td>
<td>List of tables that acceleration should be applied to. Format: <code dir="ltr" translate="no">         project              .               dataset              .               table              or               dataset              .               table       </code> . If project is omitted, query project is used.</td>
</tr>
</tbody>
</table>

Setting `  VALUE  ` replaces the existing value of that option for the BI Engine capacity, if there is one. Setting `  VALUE  ` to `  NULL  ` clears the value for that option.

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.bireservations.update      </code></td>
<td>BI Engine reservation</td>
</tr>
</tbody>
</table>

### Examples

#### Allocating BI Engine capacity without preferred tables

``` text
ALTER BI_CAPACITY `my-project.region-us.default`
SET OPTIONS(
  size_gb = 250
)
```

#### Deallocating BI capacity

``` text
ALTER BI_CAPACITY `my-project.region-us.default`
SET OPTIONS(
  size_gb = 0
)
```

#### Removing a set of preferred tables from reservation

``` text
ALTER BI_CAPACITY `my-project.region-us.default`
SET OPTIONS(
  preferred_tables = NULL
)
```

#### Allocating BI Capacity with preferred tables list

``` text
ALTER BI_CAPACITY `my-project.region-us.default`
SET OPTIONS(
  size_gb = 250,
  preferred_tables = ["data_project1.dataset1.table1",
                      "data_project2.dataset2.table2"]
)
```

#### Overwriting list of preferred tables without changing the size

``` text
ALTER BI_CAPACITY `region-us.default`
SET OPTIONS(
  preferred_tables = ["dataset1.table1",
                      "data_project2.dataset2.table2"]
)
```

## `     ALTER CAPACITY SET OPTIONS    ` statement

Alters an existing capacity commitment.

### Syntax

``` text
ALTER CAPACITY `project_id.location_id.commitment_id`
SET OPTIONS (alter_capacity_commitment_option_list);
```

### Arguments

  - `  project_id  ` : The project ID of the administration project that maintains ownership of this commitment.
  - `  location_id  ` : The [location](/bigquery/docs/locations#supported_locations) of the commitment.
  - `  commitment_id  ` : The ID of the commitment. The value must be unique to the project and location. It must start and end with a lowercase letter or a number and contain only lowercase letters, numbers and dashes.
  - [`  alter_capacity_commitment_option_list  `](#alter_capacity_commitment_option_list) : The options you can set to alter the capacity commitment.

### `     alter_capacity_commitment_option_list    `

The option list specifies options for the dataset. Specify the options in the following format: `  NAME=VALUE, ...  `

The following options are supported:

<table>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">       NAME      </code></th>
<th><code dir="ltr" translate="no">       TYPE      </code></th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       plan      </code></td>
<td>String</td>
<td>The commitment plan to purchase. Supported values include: <code dir="ltr" translate="no">       ANNUAL      </code> , <code dir="ltr" translate="no">       THREE_YEAR      </code> , and <code dir="ltr" translate="no">       TRIAL      </code> . For more information, see <a href="/bigquery/docs/reservations-workload-management#slot_commitments">slot commitments</a> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       renewal_plan      </code></td>
<td>String</td>
<td>The plan this capacity commitment is converted to after <code dir="ltr" translate="no">       commitment_end_time      </code> passes. Once the plan is changed, the committed period is extended according to the commitment plan. Applicable for ANNUAL, THREE_YEAR, and TRIAL commitments.</td>
</tr>
</tbody>
</table>

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.capacityCommitments.update      </code></td>
<td>The administration project that maintains ownership of the commitments.</td>
</tr>
</tbody>
</table>

### Example

The following example changes a capacity commitment to a three-year plan that is located in the `  region-us  ` region and managed by a project `  admin_project  ` :

``` text
ALTER CAPACITY `admin_project.region-us.my-commitment`
SET OPTIONS (
  plan = 'THREE_YEAR');
```

## `     ALTER RESERVATION SET OPTIONS    ` statement

Alters an existing reservation.

### Syntax

``` text
ALTER RESERVATION `project_id.location_id.reservation_id`
SET OPTIONS (alter_reservation_option_list);
```

### Arguments

  - `  project_id  ` : The project ID of the administration project that maintains ownership of this reservation.
  - `  location_id  ` : The [location](/bigquery/docs/locations#supported_locations) of the reservation.
  - `  reservation_id  ` : The ID of the reservation. The value must be unique to the project and location. It must start and end with a lowercase letter or a number and contain only lowercase letters, numbers and dashes.
  - [`  alter_reservation_option_list  `](#alter_reservation_option_list) : The options you can set to alter the reservation.

### `     alter_reservation_option_list    `

The option list specifies options for the dataset. Specify the options in the following format: `  NAME=VALUE, ...  `

The following options are supported:

<table>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">       NAME      </code></th>
<th><code dir="ltr" translate="no">       TYPE      </code></th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       ignore_idle_slots      </code></td>
<td><code dir="ltr" translate="no">       BOOLEAN      </code></td>
<td>If the value is <code dir="ltr" translate="no">       true      </code> , then the reservation uses only the slots that are provisioned to it. The default value is <code dir="ltr" translate="no">       false      </code> . For more information, see <a href="/bigquery/docs/slots#idle_slots">Idle slots</a> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       slot_capacity      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>The number of slots to allocate to the reservation. If this reservation was created with an <a href="/bigquery/docs/editions-intro">edition</a> , this is equivalent to the amount of <a href="/bigquery/docs/slots-autoscaling-intro#using_reservations_with_baseline_and_autoscaling_slots">baseline slots</a> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       target_job_concurrency      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>A soft upper bound on the number of jobs that can run concurrently in this reservation.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       autoscale_max_slots      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>The maximum number of slots that can be added to the reservation by autoscaling.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       secondary_location      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The secondary location to use in the case of disaster recovery.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       is_primary      </code></td>
<td><code dir="ltr" translate="no">       BOOLEAN      </code></td>
<td>If the value is <code dir="ltr" translate="no">       true      </code> , the reservation is set to be the primary reservation.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       labels      </code></td>
<td><code dir="ltr" translate="no">       &lt;ARRAY&lt;STRUCT&lt;STRING, STRING&gt;&gt;&gt;      </code></td>
<td>An array of labels for the reservation, expressed as key-value pairs.</td>
</tr>
</tbody>
</table>

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.reservations.update      </code></td>
<td>The administration project that maintains ownership of the commitments.</td>
</tr>
</tbody>
</table>

### Examples

#### Autoscaling example

The following example changes an autoscaling reservation to 300 baseline slots and 400 autoscaling slots for a max reservation size of 700. These slots are located in the `  region-us  ` region and managed by a project `  admin_project  ` :

``` text
ALTER RESERVATION `admin_project.region-us.my-reservation`
SET OPTIONS (
  slot_capacity = 300,
  autoscale_max_slots = 400);
```

## `     ALTER VECTOR INDEX REBUILD    ` statement

**Preview**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

**Note:** To provide feedback or request support for this feature, send email to <bq-vector-search@google.com> .

Rebuild a [vector index](/bigquery/docs/vector-index) on a table.

### Syntax

``` text
ALTER VECTOR INDEX [ IF EXISTS ] index_name
ON table_name
REBUILD;
```

### Arguments

  - `  IF EXISTS  ` : If no vector index exists with that name, the statement has no effect.

  - `  index_name  ` : The name of the vector index to rebuild.

  - `  table_name  ` : The name of the table that the vector index is on. See [Table path syntax](#table_path) .
    
    If the table doesn't contain a vector index, or if the table contains a different vector index than the one specified in the `  index_name  ` argument, the query fails.

  - `  REBUILD  ` : Indicates that the statement rebuilds the vector index. This argument is required.

### Details

Use the `  ALTER VECTOR INDEX REBUILD  ` statement to rebuild an active vector index on a table without having to drop the vector index, and without any index downtime. When you run the statement, BigQuery creates a shadow index on the table and trains it in the background. BigQuery promotes the shadow index to be the active index when the shadow index has enough coverage.

To run the `  ALTER VECTOR INDEX REBUILD  ` statement, you must [create a reservation assignment](/bigquery/docs/reservations-assignments#assign_my_prod_project_to_prod_reservation) with a job type of `  BACKGROUND  ` for the project that contains the table. If you run the statement without an appropriate reservation, the query fails.

You can have only one vector index rebuild in progress at a time. The `  ALTER VECTOR INDEX REBUILD  ` statement completes before the shadow index replaces the active index, because the shadow index training and cutover happen asynchronously. If you start another vector index rebuild before the shadow index replaces the initial index, the second rebuild request fails.

### Required permissions

To get the permissions that you need to alter vector indexes, ask your administrator to grant you the BigQuery Data Editor ( `  roles/bigquery.dataEditor  ` ) or BigQuery Data Owner ( `  roles/bigquery.dataOwner  ` ) IAM role on your table. For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

### Examples

The following example rebuilds the `  index1  ` vector index on the `  sales  ` table:

``` text
ALTER VECTOR INDEX IF EXISTS index1
ON mydataset.sales
REBUILD;
```

## `     ALTER DATA_POLICY    ` statement

**Preview**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

**Note:** To provide feedback or request support for this feature, send an email to <bigquery-security@google.com> .

### Syntax

``` text
ALTER DATA_POLICY [ IF EXISTS ] `project_id.region-location_id.data_policy_id`
SET OPTIONS (alter_option_list);
```

### Arguments

  - `  IF EXISTS  ` : If no data policy exists with that name, the statement has no effect.

  - `  project_id  ` : The project ID of the project where the data policy will reside in.

  - `  location_id  ` : The location of the data policy.

  - `  data_policy_id  ` : The name of the data policy to be updated.

  - [`  alter_option_list  `](#alter_datapolicy_option_list) : The list of options to update on the data policy.

### `     alter_option_list    `

The option list specifies options for the data policy. Specify the options in the following format: `  NAME=VALUE, ...  `

The following options are supported:

<table>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">       NAME      </code></th>
<th><code dir="ltr" translate="no">       VALUE      </code></th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       data_policy_type      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Set it to <code dir="ltr" translate="no">       DATA_MASKING_POLICY      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       masking_expression      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Specifies the <a href="/bigquery/docs/reference/bigquerydatapolicy/rest/v2/projects.locations.dataPolicies#PredefinedExpression">predefined masking rule</a> or a <a href="/bigquery/docs/column-data-masking-intro#custom_mask">custom masking routine</a> .</td>
</tr>
</tbody>
</table>

### Required permissions

The user or service account that updates a data policy must have the `  bigquery.dataPolicies.update  ` permission.

The `  bigquery.dataPolicies.update  ` permission is included in the BigQuery Data Policy Admin, BigQuery Admin and BigQuery Data Owner roles.

## `     DROP SCHEMA    ` statement

Deletes a dataset.

### Syntax

``` text
DROP [EXTERNAL] SCHEMA [IF EXISTS]
[project_name.]dataset_name
[ CASCADE | RESTRICT ]
```

### Arguments

  - `  EXTERNAL  ` : Specifies if that dataset is a federated dataset. The `  DROP EXTERNAL  ` statement only removes the external definition from BigQuery. The data stored in the external location is not affected.

  - `  IF EXISTS  ` : If no dataset exists with that name, the statement has no effect.

  - `  project_name  ` : The name of the project that contains the dataset. Defaults to the project that runs this DDL statement.

  - `  dataset_name  ` : The name of the dataset to delete.

  - `  CASCADE  ` : Deletes the dataset and all resources within the dataset, such as tables, views, and functions. You must have permission to delete the resources, or else the statement returns an error. For a list of BigQuery permissions, see [Predefined roles and permissions](/bigquery/docs/access-control) .

  - `  RESTRICT  ` : Deletes the dataset only if it's empty. Otherwise, returns an error. If you don't specify either `  CASCADE  ` or `  RESTRICT  ` , then the default behavior is `  RESTRICT  ` .

### Details

The statement runs in the location of the dataset if it exists, unless you specify the location in the query settings. For more information, see [Specifying your location](/bigquery/docs/locations#specify_locations) .

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.datasets.delete      </code></td>
<td>The dataset to delete.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigquery.tables.delete      </code></td>
<td>The dataset to delete. If the dataset is empty, then this permission is not required.</td>
</tr>
</tbody>
</table>

### Examples

The following example deletes the dataset named `  mydataset  ` . If the dataset does not exist or is not empty, then the statement returns an error.

``` text
DROP SCHEMA mydataset
```

The following example drops the dataset named `  mydataset  ` and any resources in that dataset. If the dataset does not exist, then no error is returned.

``` text
DROP SCHEMA IF EXISTS mydataset CASCADE
```

## `     UNDROP SCHEMA    ` statement

**Preview**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

[Undeletes a dataset](/bigquery/docs/restore-deleted-datasets) within your time travel window.

### Syntax

``` text
UNDROP SCHEMA [IF NOT EXISTS]
[project_name.]dataset_name
[OPTIONS (location="us")]
```

### Arguments

  - `  IF NOT EXISTS  ` : If a dataset already exists with that name, the statement has no effect.

  - `  project_name  ` : The name of the project that contained the deleted dataset. Defaults to the project that runs this DDL statement.

  - `  dataset_name  ` : The name of the dataset to undelete.

  - `  location  ` : Original location of the deleted dataset.

### Details

When you run this statement, you must [specify the location](/bigquery/docs/locations#specify_locations) where the dataset was deleted. If you don't, the `  US  ` multi-region is used.

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.datasets.create      </code></td>
<td>The project where you are undeleting the dataset.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigquery.datasets.get      </code></td>
<td>The dataset that you are undeleting.</td>
</tr>
</tbody>
</table>

### Examples

The following example undeletes the dataset named `  mydataset  ` . If the dataset already exists or has passed the time travel window, then the statement returns an error.

``` text
UNDROP SCHEMA mydataset;
```

## `     DROP TABLE    ` statement

Deletes a table or [table clone](/bigquery/docs/table-clones-intro) .

### Syntax

``` text
DROP TABLE [IF EXISTS] table_name
```

### Arguments

  - `  IF EXISTS  ` : If no table exists with that name, the statement has no effect.

  - `  table_name  ` : The name of the table to delete. See [Table path syntax](#table_path) .

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.tables.delete      </code></td>
<td>The table to delete.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigquery.tables.get      </code></td>
<td>The table to delete.</td>
</tr>
</tbody>
</table>

### Examples

#### Deleting a table

The following example deletes a table named `  mytable  ` in the `  mydataset  ` :

``` text
DROP TABLE mydataset.mytable
```

If the table name does not exist in the dataset, the following error is returned:

`  Error: Not found: Table myproject:mydataset.mytable  `

#### Deleting a table only if the table exists

The following example deletes a table named `  mytable  ` in `  mydataset  ` only if the table exists. If the table name does not exist in the dataset, no error is returned, and no action is taken.

``` text
DROP TABLE IF EXISTS mydataset.mytable
```

## `     DROP SNAPSHOT TABLE    ` statement

Deletes a [table snapshot](/bigquery/docs/table-snapshots-intro) .

### Syntax

``` text
DROP SNAPSHOT TABLE [IF EXISTS] table_snapshot_name
```

### Arguments

  - `  IF EXISTS  ` : If no table snapshot exists with that name, then the statement has no effect.

  - `  table_snapshot_name  ` : The name of the table snapshot to delete. See [Table path syntax](#table_path) .

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.tables.deleteSnapshot      </code></td>
<td>The table snapshot to delete.</td>
</tr>
</tbody>
</table>

### Examples

#### Delete a table snapshot: fail if it doesn't exist

The following example deletes the table snapshot named `  mytablesnapshot  ` in the `  mydataset  ` dataset:

``` text
DROP SNAPSHOT TABLE mydataset.mytablesnapshot
```

If the table snapshot does not exist in the dataset, then the following error is returned:

`  Error: Not found: Table snapshot myproject:mydataset.mytablesnapshot  `

#### Delete a table snapshot: ignore if it doesn't exist

The following example deletes the table snapshot named `  mytablesnapshot  ` in the `  mydataset  ` dataset.

``` text
DROP SNAPSHOT TABLE IF EXISTS mydataset.mytablesnapshot
```

If the table snapshot doesn't exist in the dataset, then no action is taken, and no error is returned.

For information about creating table snapshots, see [CREATE SNAPSHOT TABLE](#create_snapshot_table_statement) .

For information about restoring table snapshots, see [CREATE TABLE CLONE](#create_table_clone_statement) .

## `     DROP EXTERNAL TABLE    ` statement

Deletes an external table.

### Syntax

``` text
DROP EXTERNAL TABLE [IF EXISTS] table_name
```

### Arguments

  - `  IF EXISTS  ` : If no external table exists with that name, then the statement has no effect.

  - `  table_name  ` : The name of the external table to delete. See [Table path syntax](#table_path) .

### Details

If `  table_name  ` exists but is not an external table, the statement returns the following error:

`  Cannot drop table_name which has type TYPE . An external table was expected.  `

The `  DROP EXTERNAL  ` statement only removes the external table definition from BigQuery. The data stored in the external location is not affected.

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.tables.delete      </code></td>
<td>The external table to delete.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigquery.tables.get      </code></td>
<td>The external table to delete.</td>
</tr>
</tbody>
</table>

### Examples

The following example drops the external table named `  external_table  ` from the dataset `  mydataset  ` . It returns an error if the external table does not exist.

``` text
DROP EXTERNAL TABLE mydataset.external_table
```

The following example drops the external table named `  external_table  ` from the dataset `  mydataset  ` . If the external table does not exist, no error is returned.

``` text
DROP EXTERNAL TABLE IF EXISTS mydataset.external_table
```

## `     DROP VIEW    ` statement

Deletes a view.

### Syntax

``` text
DROP VIEW [IF EXISTS] view_name
```

### Arguments

  - `  IF EXISTS  ` : If no view exists with that name, the statement has no effect.

  - `  view_name  ` : The name of the view to delete. See [Table path syntax](#table_path) .

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.tables.delete      </code></td>
<td>The view to delete.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigquery.tables.get      </code></td>
<td>The view to delete.</td>
</tr>
</tbody>
</table>

### Examples

#### Deleting a view

The following example deletes a view named `  myview  ` in `  mydataset  ` :

``` text
DROP VIEW mydataset.myview
```

If the view name does not exist in the dataset, the following error is returned:

`  Error: Not found: Table myproject:mydataset.myview  `

#### Deleting a view only if the view exists

The following example deletes a view named `  myview  ` in `  mydataset  ` only if the view exists. If the view name does not exist in the dataset, no error is returned, and no action is taken.

``` text
DROP VIEW IF EXISTS mydataset.myview
```

## `     DROP MATERIALIZED VIEW    ` statement

Deletes a materialized view.

### Syntax

``` text
DROP MATERIALIZED VIEW [IF EXISTS] mv_name
```

### Arguments

  - `  IF EXISTS  ` : If no materialized view exists with that name, the statement has no effect.

  - `  mv_name  ` : The name of the materialized view to delete. See [Table path syntax](#table_path) .

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.tables.delete      </code></td>
<td>The materialized view to delete.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigquery.tables.get      </code></td>
<td>The materialized view to delete.</td>
</tr>
</tbody>
</table>

### Examples

#### Deleting a materialized view

The following example deletes a materialized view named `  my_mv  ` in `  mydataset  ` :

``` text
DROP MATERIALIZED VIEW mydataset.my_mv
```

If the materialized view name does not exist in the dataset, the following error is returned:

`  Error: Not found: Table myproject:mydataset.my_mv  `

If you are deleting a materialized view in another project, you must specify the project, dataset, and materialized view in the following format: ``  ` project_id.dataset.materialized_view `  `` (including the backticks if `  project_id  ` contains special characters); for example, ``  `myproject.mydataset.my_mv`  `` .

#### Deleting a materialized view only if it exists

The following example deletes a materialized view named `  my_mv  ` in `  mydataset  ` only if the materialized view exists. If the materialized view name does not exist in the dataset, no error is returned, and no action is taken.

``` text
DROP MATERIALIZED VIEW IF EXISTS mydataset.my_mv
```

If you are deleting a materialized view in another project, you must specify the project, dataset, and materialized view in the following format: ``  ` project_id.dataset.materialized_view `,  `` (including the backticks if `  project_id  ` contains special characters); for example, ``  `myproject.mydataset.my_mv`  `` .

## `     DROP FUNCTION    ` statement

Deletes a persistent user-defined function (UDF) or user-defined aggregate function (UDAF).

### Syntax

``` text
DROP FUNCTION [IF EXISTS] [[project_name.]dataset_name.]function_name
```

### Arguments

  - `  IF EXISTS  ` : If no function exists with that name, the statement has no effect.

  - `  project_name  ` : The name of the project containing the function to delete. Defaults to the project that runs this DDL query. If the project name contains special characters such as colons, it should be quoted in backticks ``  `  `` (example: ``  `google.com:my_project`  `` ).

  - `  dataset_name  ` : The name of the dataset containing the function to delete. Defaults to the `  defaultDataset  ` in the request.

  - `  function_name  ` : The name of the function you're deleting.

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.routines.delete      </code></td>
<td>The function to delete.</td>
</tr>
</tbody>
</table>

### Examples

The following example statement deletes the function `  parseJsonAsStruct  ` contained in the dataset `  mydataset  ` .

``` text
DROP FUNCTION mydataset.parseJsonAsStruct;
```

The following example statement deletes the function `  parseJsonAsStruct  ` from the dataset `  sample_dataset  ` in the project `  other_project  ` .

``` text
DROP FUNCTION `other_project`.sample_dataset.parseJsonAsStruct;
```

## `     DROP TABLE FUNCTION    `

**Preview**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

Deletes a [table function](/bigquery/docs/table-functions) .

### Syntax

``` text
DROP TABLE FUNCTION [IF EXISTS] [[project_name.]dataset_name.]function_name
```

### Arguments

  - `  IF EXISTS  ` : If no table function exists with this name, the statement has no effect.

  - `  project_name  ` : The name of the project containing the table function to delete. Defaults to the project that runs this DDL query.

  - `  dataset_name  ` : The name of the dataset containing the table function to delete.

  - `  function_name  ` : The name of the table function to delete.

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.routines.delete      </code></td>
<td>The table function to delete.</td>
</tr>
</tbody>
</table>

### Example

The following example deletes a table function named `  my_table_function  ` :

``` text
DROP TABLE FUNCTION mydataset.my_table_function;
```

## `     DROP PROCEDURE    ` statement

Deletes a stored procedure.

### Syntax

``` text
DROP PROCEDURE [IF EXISTS] [[project_name.]dataset_name.]procedure_name
```

### Arguments

  - `  IF EXISTS  ` : If no procedure exists with that name, the statement has no effect.

  - `  project_name  ` : The name of the project containing the procedure to delete. Defaults to the project that runs this DDL query. If the project name contains special characters such as colons, it should be quoted in backticks ``  `  `` (example: ``  `google.com:my_project`  `` ).

  - `  dataset_name  ` : The name of the dataset containing the procedure to delete. Defaults to the `  defaultDataset  ` in the request.

  - `  procedure_name  ` : The name of the procedure you're deleting.

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.routines.delete      </code></td>
<td>The procedure to delete.</td>
</tr>
</tbody>
</table>

### Examples

The following example statement deletes the procedure `  myprocedure  ` contained in the dataset `  mydataset  ` .

``` text
DROP PROCEDURE mydataset.myProcedure;
```

The following example statement deletes the procedure `  myProcedure  ` from the dataset `  sample_dataset  ` in the project `  other_project  ` .

``` text
DROP PROCEDURE `other-project`.sample_dataset.myprocedure;
```

## `     DROP ROW ACCESS POLICY    ` statement

Deletes a row-level access policy.

**Important:** You cannot delete the last row-level access policy from a table using `  DROP ROW ACCESS POLICY  ` . Attempting to do so results in an error. To delete the last row-level access policy on table, you must use `  DROP ALL ROW ACCESS POLICIES  ` instead.

### Syntax

``` text
DROP ROW ACCESS POLICY [ IF EXISTS ]
row_access_policy_name ON table_name;
```

``` text
DROP ALL ROW ACCESS POLICIES ON table_name;
```

### Arguments

  - `  IF EXISTS  ` : If no row-level access policy exists with that name, the statement has no effect.

  - `  row_access_policy_name  ` : The name of the row-level access policy that you are deleting. Each row-level access policy on a table has a unique name.

  - `  table_name  ` : The name of the table with the row-level access policy or policies that you want to delete.

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.rowAccessPolicies.delete      </code></td>
<td>The row-level access policy to delete.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigquery.rowAccessPolicies.setIamPolicy      </code></td>
<td>The row-level access policy to delete.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.rowAccessPolicies.list      </code></td>
<td>The table to delete all row-level access policies on. Only required for <code dir="ltr" translate="no">       DROP ALL      </code> statements.</td>
</tr>
</tbody>
</table>

### Examples

Delete a row-level access policy from a table:

``` text
DROP ROW ACCESS POLICY my_row_filter ON project.dataset.my_table;
```

Delete all the row-level access policies from a table:

``` text
DROP ALL ROW ACCESS POLICIES ON project.dataset.my_table;
```

## `     DROP CAPACITY    ` statement

Deletes a capacity commitment.

### Syntax

``` text
DROP CAPACITY [IF EXISTS]
project_id.location.capacity-commitment-id
```

### Arguments

  - `  IF EXISTS  ` : If no capacity commitment exists with that ID, the statement has no effect.
  - `  project_id  ` : The project ID of the administration project where the reservation was created.
  - `  location  ` : The [location](/bigquery/docs/locations#supported_locations) of the commitment.
  - `  capacity-commitment-id  ` : The capacity commitment ID.

To find the capacity commitment ID, query the [`  INFORMATION_SCHEMA.CAPACITY_COMMITMENTS_BY_PROJECT  `](/bigquery/docs/information-schema-capacity-commitments) table.

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.capacityCommitments.delete      </code></td>
<td>The administration project that maintains ownership of the commitments.</td>
</tr>
</tbody>
</table>

### Example

The following example deletes the capacity commitment:

``` text
DROP CAPACITY `admin_project.region-us.1234`
```

## `     DROP RESERVATION    ` statement

Deletes a reservation.

### Syntax

``` text
DROP RESERVATION [IF EXISTS]
project_id.location.reservation_id
```

### Arguments

  - `  IF EXISTS  ` : If no reservation exists with that ID, the statement has no effect.
  - `  project_id  ` : The project ID of the administration project where the reservation was created.
  - `  location  ` : The [location](/bigquery/docs/locations#supported_locations) of the reservation.
  - `  reservation_id  ` : The reservation ID.

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.reservations.delete      </code></td>
<td>The administration project that maintains ownership of the commitments.</td>
</tr>
</tbody>
</table>

### Example

The following example deletes the reservation `  prod  ` :

``` text
DROP RESERVATION `admin_project.region-us.prod`
```

## `     DROP ASSIGNMENT    ` statement

Deletes a reservation assignment.

### Syntax

``` text
DROP ASSIGNMENT [IF EXISTS]
project_id.location.reservation_id.assignment_id
```

### Arguments

  - `  IF EXISTS  ` : If no assignment exists with that ID, the statement has no effect.
  - `  project_id  ` : The project ID of the administration project where the reservation was created.
  - `  location  ` : The [location](/bigquery/docs/locations#supported_locations) of the reservation.
  - `  reservation_id  ` : The reservation ID.
  - `  assignment_id  ` : The assignment ID.

To find the assignment ID, query the [`  INFORMATION_SCHEMA.ASSIGNMENTS  ` view](/bigquery/docs/information-schema-assignments) .

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.reservationAssignments.delete      </code></td>
<td>The administration project and the assignee.</td>
</tr>
</tbody>
</table>

### Example

The following example deletes an assignment from the reservation named `  prod  ` :

``` text
DROP ASSIGNMENT `admin_project.region-us.prod.1234`
```

## `     DROP SEARCH INDEX    ` statement

Deletes a search index on a table.

### Syntax

``` text
DROP SEARCH INDEX [ IF EXISTS ] index_name ON table_name
```

### Arguments

  - `  IF EXISTS  ` : If no search index exists with that name on the table, the statement has no effect.
  - `  index_name  ` : The name of the search index to be deleted.
  - `  table_name  ` : The name of the table with the index.

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.tables.deleteIndex      </code></td>
<td>The table with the search index to delete.</td>
</tr>
</tbody>
</table>

### Example

The following example deletes a search index `  my_index  ` from `  my_table  ` :

``` text
DROP SEARCH INDEX my_index ON dataset.my_table;
```

## `     DROP VECTOR INDEX    ` statement

Deletes a vector index on a table.

### Syntax

``` text
DROP VECTOR INDEX [ IF EXISTS ] index_name ON table_name
```

### Arguments

  - `  IF EXISTS  ` : If no vector index exists with that name on the table, the statement has no effect.
  - `  index_name  ` : The name of the vector index to be deleted.
  - `  table_name  ` : The name of the table with the vector index.

### Required permissions

This statement requires the following [IAM permissions](/bigquery/docs/access-control#bq-permissions) :

<table>
<thead>
<tr class="header">
<th>Permission</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.tables.deleteIndex      </code></td>
<td>The table with the vector index to delete.</td>
</tr>
</tbody>
</table>

### Example

The following example deletes a vector index `  my_index  ` from `  my_table  ` :

``` text
DROP VECTOR INDEX my_index ON dataset.my_table;
```

## `     DROP DATA_POLICY    ` statement

**Preview**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

**Note:** To provide feedback or request support for this feature, send an email to <bigquery-security@google.com> .

Deletes a data policy in a project.

### Syntax

``` text
DROP DATA_POLICY [ IF EXISTS ] `myproject.region-us.data_policy_name`;
```

### Arguments

  - `  IF EXISTS  ` : If no data policy exists with that name, the statement has no effect.

  - `  project_id  ` : The project ID of the project where the data policy will reside in.

  - `  location_id  ` : The location of the data policy.

  - `  data_policy_id  ` : The name of the data policy to be deleted.

### Required permissions

The user or service account that creates a data policy must have the `  bigquery.dataPolicies.delete  ` permission. This permission is included in the BigQuery Data Policy Admin, BigQuery Admin and BigQuery Data Owner roles.

## Table path syntax

Use the following syntax when specifying the path of a [table resource](/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.type) , including standard tables, views, materialized views, external tables, and table snapshots.

``` text
table_path :=
  [[project_name.]dataset_name.]table_name
```

  - `  project_name  ` : The name of the project that contains the table resource. Defaults to the project that runs the DDL query. If the project name contains special characters such as colons, quote the name in backticks ``  `  `` (example: ``  `google.com:my_project`  `` ).

  - `  dataset_name  ` : The name of the dataset that contains the table resource. Defaults to the `  defaultDataset  ` in the request.

  - `  table_name  ` : The name of the table resource.

When you create a table in BigQuery, the table name must be unique per dataset. The table name can:

  - Contain characters with a total of up to 1,024 UTF-8 bytes.
  - Contain Unicode characters in category L (letter), M (mark), N (number), Pc (connector, including underscore), Pd (dash), Zs (space). For more information, see [General Category](https://wikipedia.org/wiki/Unicode_character_property#General_Category) .

The following are all examples of valid table names: `  table 01  ` , `  ग्राहक  ` , `  00_お客様  ` , `  étudiant-01  ` .

Caveats:

  - Table names are case-sensitive by default. `  mytable  ` and `  MyTable  ` can coexist in the same dataset, unless they are part of a [dataset with case-sensitivity turned off](/bigquery/docs/reference/standard-sql/data-definition-language#creating_a_case-insensitive_dataset) .

  - Some table names and table name prefixes are reserved. If you receive an error saying that your table name or prefix is reserved, then select a different name and try again.

  - If you include multiple dot operators ( `  .  ` ) in a sequence, the duplicate operators are implicitly stripped.
    
    For example, this: `  project_name....dataset_name..table_name  `
    
    Becomes this: `  project_name.dataset_name.table_name  `
