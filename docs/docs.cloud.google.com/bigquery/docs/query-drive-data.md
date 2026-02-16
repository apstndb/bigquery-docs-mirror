# Query Drive data

This document describes how to query data stored in an [Google Drive external table](/bigquery/docs/external-data-drive) .

BigQuery supports queries against both personal Drive files and shared files. For more information on Drive, see [Google Drive training and help](https://support.google.com/a/users/answer/9282958) .

You can query Drive data from a [permanent external table](#permanent-tables) or from a [temporary external table](#temporary-tables) that you create when you run the query.

## Limitations

For limitations related to external tables, see [external table limitations](/bigquery/docs/external-tables#limitations) .

## Required roles

To query Drive external tables, ensure you have the following roles:

  - BigQuery Data Viewer ( `  roles/bigquery.dataViewer  ` )
  - BigQuery User ( `  roles/bigquery.user  ` )

Depending on your permissions, you can grant these roles to yourself or ask your administrator to grant them to you. For more information about granting roles, see [Viewing the grantable roles on resources](/iam/docs/viewing-grantable-roles) .

To see the exact BigQuery permissions that are required to query external tables, expand the **Required permissions** section:

#### Required permissions

  - `  bigquery.jobs.create  `
  - `  bigquery.readsessions.create  ` (Only required if you are [reading data with the BigQuery Storage Read API](/bigquery/docs/reference/storage) )
  - `  bigquery.tables.get  `
  - `  bigquery.tables.getData  `

You might also be able to get these permissions with [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

## Drive permissions

At a minimum, to query external data in Drive you must be granted [`  View  `](https://support.google.com/drive/answer/2494822?co=GENIE.Platform%3DDesktop) access to the Drive file linked to the external table.

## Scopes for Compute Engine instances

When you create a Compute Engine instance, you can specify a list of scopes for the instance. The scopes control the instance's access to Google Cloud products, including Drive. Applications running on the VM use the service account to call Google Cloud APIs.

If you set up a Compute Engine instance to run as a [service account](/compute/docs/access/create-enable-service-accounts-for-instances) , and that service account accesses an external table linked to a Drive data source, you must add the [OAuth scope for Drive](https://developers.google.com/identity/protocols/googlescopes#drivev3) ( `  https://www.googleapis.com/auth/drive.readonly  ` ) to the instance.

For information on applying scopes to a Compute Engine instance, see [Changing the service account and access scopes for an instance](/compute/docs/access/create-enable-service-accounts-for-instances#changeserviceaccountandscopes) . For more information on Compute Engine service accounts, see [Service accounts](/compute/docs/access/service-accounts) .

## Query Drive data using permanent external tables

After creating a Drive external table, you can [query it using GoogleSQL syntax](/bigquery/docs/running-queries) , the same as if it were a standard BigQuery table. For example, `  SELECT field1, field2 FROM mydataset.my_drive_table;  ` .

## Query Drive data using temporary tables

Querying an external data source using a temporary table is useful for one-time, ad-hoc queries over external data, or for extract, transform, and load (ETL) processes.

To query an external data source without creating a permanent table, you provide a table definition for the temporary table, and then use that table definition in a command or call to query the temporary table. You can provide the table definition in any of the following ways:

  - A [table definition file](/bigquery/external-table-definition)
  - An inline schema definition
  - A [JSON schema file](/bigquery/docs/schemas#specifying_a_json_schema_file)

The table definition file or supplied schema is used to create the temporary external table, and the query runs against the temporary external table.

When you use a temporary external table, you do not create a table in one of your BigQuery datasets. Because the table is not permanently stored in a dataset, it cannot be shared with others.

### Create and query temporary tables

You can create and query a temporary table linked to an external data source by using the bq command-line tool, the API, or the client libraries.

### bq

You query a temporary table linked to an external data source using the `  bq query  ` command with the `  --external_table_definition  ` flag. When you use the bq command-line tool to query a temporary table linked to an external data source, you can identify the table's schema using:

  - A [table definition file](/bigquery/external-table-definition) (stored on your local machine)
  - An inline schema definition
  - A JSON schema file (stored on your local machine)

To query a temporary table linked to your external data source using a table definition file, enter the following command.

``` text
bq --location=LOCATION query \
--external_table_definition=TABLE::DEFINITION_FILE \
'QUERY'
```

Where:

  - `  LOCATION  ` is your [location](/bigquery/docs/locations) . The `  --location  ` flag is optional.
  - `  TABLE  ` is the name of the temporary table you're creating.
  - `  DEFINITION_FILE  ` is the path to the [table definition file](/bigquery/external-table-definition) on your local machine.
  - `  QUERY  ` is the query you're submitting to the temporary table.

For example, the following command creates and queries a temporary table named `  sales  ` using a table definition file named `  sales_def  ` .

``` text
bq query \
--external_table_definition=sales::sales_def \
'SELECT
   Region,Total_sales
 FROM
   sales'
```

To query a temporary table linked to your external data source using an inline schema definition, enter the following command.

``` text
bq --location=LOCATION query \
--external_table_definition=TABLE::SCHEMA@SOURCE_FORMAT=DRIVE_URI \
'QUERY'
```

Where:

  - `  LOCATION  ` is your [location](/bigquery/docs/locations) . The `  --location  ` flag is optional.
  - `  TABLE  ` is the name of the temporary table you're creating.
  - `  SCHEMA  ` is the inline schema definition in the format `  FIELD : DATA_TYPE , FIELD : DATA_TYPE  ` .
  - `  SOURCE_FORMAT  ` is `  CSV  ` , `  NEWLINE_DELIMITED_JSON  ` , `  AVRO  ` , or `  GOOGLE_SHEETS  ` .
  - `  DRIVE_URI  ` is your [Drive URI](#drive-uri) .
  - `  QUERY  ` is the query you're submitting to the temporary table.

For example, the following command creates and queries a temporary table named `  sales  ` linked to a CSV file stored in Drive with the following schema definition: `  Region:STRING,Quarter:STRING,Total_sales:INTEGER  ` .

``` text
bq --location=US query \
--external_table_definition=sales::Region:STRING,Quarter:STRING,Total_sales:INTEGER@CSV=https://drive.google.com/open?id=1234_AbCD12abCd \
'SELECT
   Region,Total_sales
 FROM
   sales'
```

To query a temporary table linked to your external data source using a JSON schema file, enter the following command.

``` text
bq --location=LOCATION query \
--external_table_definition=SCHEMA_FILE@SOURCE_FORMT=DRIVE_URI \
'QUERY'
```

Where:

  - `  LOCATION  ` is your [location](/bigquery/docs/locations) . The `  --location  ` flag is optional.
  - `  SCHEMA_FILE  ` is the path to the JSON schema file on your local machine.
  - `  SOURCE_FILE  ` is `  CSV  ` , `  NEWLINE_DELIMITED_JSON  ` , `  AVRO  ` , or `  GOOGLE_SHEETS  ` .
  - `  DRIVE_URI  ` is your [Drive URI](#drive-uri) .
  - `  QUERY  ` is the query you're submitting to the temporary table.

For example, the following command creates and queries a temporary table named `  sales  ` linked to a CSV file stored in Drive using the `  /tmp/sales_schema.json  ` schema file.

``` text
bq query \
--external_table_definition=sales::/tmp/sales_schema.json@CSV=https://drive.google.com/open?id=1234_AbCD12abCd \
'SELECT
   Total_sales
 FROM
   sales'
```

### API

  - Create a [query job configuration](/bigquery/docs/reference/rest/v2/Job#jobconfigurationquery) . See [Querying data](/bigquery/querying-data) for information about calling [`  jobs.query  `](/bigquery/docs/reference/v2/jobs/query) and [`  jobs.insert  `](/bigquery/docs/reference/v2/jobs/insert) .

  - Specify the external data source by creating an [`  ExternalDataConfiguration  `](/bigquery/docs/reference/rest/v2/tables#externaldataconfiguration) .

### Python

Before trying this sample, follow the Python setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Python API reference documentation](/python/docs/reference/bigquery/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` python
from google.cloud import bigquery
import google.auth

# Create credentials with Drive & BigQuery API scopes.
# Both APIs must be enabled for your project before running this code.
credentials, project = google.auth.default(
    scopes=[
        "https://www.googleapis.com/auth/drive",
        "https://www.googleapis.com/auth/bigquery",
    ]
)

# Construct a BigQuery client object.
client = bigquery.Client(credentials=credentials, project=project)

# Configure the external data source and query job.
external_config = bigquery.ExternalConfig("GOOGLE_SHEETS")

# Use a shareable link or grant viewing access to the email address you
# used to authenticate with BigQuery (this example Sheet is public).
sheet_url = (
    "https://docs.google.com/spreadsheets"
    "/d/1i_QCL-7HcSyUZmIbP9E6lO_T5u3HnpLe7dnpHaijg_E/edit?usp=sharing"
)
external_config.source_uris = [sheet_url]
external_config.schema = [
    bigquery.SchemaField("name", "STRING"),
    bigquery.SchemaField("post_abbr", "STRING"),
]
external_config.options.skip_leading_rows = 1  # Optionally skip header row.
external_config.options.range = (
    "us-states!A20:B49"  # Optionally set range of the sheet to query from.
)
table_id = "us_states"
job_config = bigquery.QueryJobConfig(table_definitions={table_id: external_config})

# Example query to find states starting with "W".
sql = 'SELECT * FROM `{}` WHERE name LIKE "W%"'.format(table_id)

query_job = client.query(sql, job_config=job_config)  # Make an API request.

# Wait for the query to complete.
w_states = list(query_job)
print(
    "There are {} states with names starting with W in the selected range.".format(
        len(w_states)
    )
)
```

### Java

Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Java API reference documentation](/java/docs/reference/google-cloud-bigquery/latest/overview) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` java
import com.google.auth.oauth2.GoogleCredentials;
import com.google.auth.oauth2.ServiceAccountCredentials;
import com.google.cloud.bigquery.BigQuery;
import com.google.cloud.bigquery.BigQueryException;
import com.google.cloud.bigquery.BigQueryOptions;
import com.google.cloud.bigquery.ExternalTableDefinition;
import com.google.cloud.bigquery.Field;
import com.google.cloud.bigquery.GoogleSheetsOptions;
import com.google.cloud.bigquery.QueryJobConfiguration;
import com.google.cloud.bigquery.Schema;
import com.google.cloud.bigquery.StandardSQLTypeName;
import com.google.cloud.bigquery.TableResult;
import com.google.common.collect.ImmutableSet;
import java.io.IOException;

// Sample to queries an external data source using a temporary table
public class QueryExternalSheetsTemp {

  public static void main(String[] args) {
    // TODO(developer): Replace these variables before running the sample.
    String tableName = "MY_TABLE_NAME";
    String sourceUri =
        "https://docs.google.com/spreadsheets/d/1i_QCL-7HcSyUZmIbP9E6lO_T5u3HnpLe7dnpHaijg_E/edit?usp=sharing";
    Schema schema =
        Schema.of(
            Field.of("name", StandardSQLTypeName.STRING),
            Field.of("post_abbr", StandardSQLTypeName.STRING));
    String query = String.format("SELECT * FROM %s WHERE name LIKE 'W%%'", tableName);
    queryExternalSheetsTemp(tableName, sourceUri, schema, query);
  }

  public static void queryExternalSheetsTemp(
      String tableName, String sourceUri, Schema schema, String query) {
    try {

      // Create credentials with Drive & BigQuery API scopes.
      // Both APIs must be enabled for your project before running this code.
      GoogleCredentials credentials =
          ServiceAccountCredentials.getApplicationDefault()
              .createScoped(
                  ImmutableSet.of(
                      "https://www.googleapis.com/auth/bigquery",
                      "https://www.googleapis.com/auth/drive"));

      // Initialize client that will be used to send requests. This client only needs to be created
      // once, and can be reused for multiple requests.
      BigQuery bigquery =
          BigQueryOptions.newBuilder().setCredentials(credentials).build().getService();

      // Skip header row in the file.
      GoogleSheetsOptions sheetsOptions =
          GoogleSheetsOptions.newBuilder()
              .setSkipLeadingRows(1) // Optionally skip header row.
              .setRange("us-states!A20:B49") // Optionally set range of the sheet to query from.
              .build();

      // Configure the external data source and query job.
      ExternalTableDefinition externalTable =
          ExternalTableDefinition.newBuilder(sourceUri, sheetsOptions).setSchema(schema).build();
      QueryJobConfiguration queryConfig =
          QueryJobConfiguration.newBuilder(query)
              .addTableDefinition(tableName, externalTable)
              .build();

      // Example query to find states starting with 'W'
      TableResult results = bigquery.query(queryConfig);

      results
          .iterateAll()
          .forEach(row -> row.forEach(val -> System.out.printf("%s,", val.toString())));

      System.out.println("Query on external temporary table performed successfully.");
    } catch (BigQueryException | InterruptedException | IOException e) {
      System.out.println("Query not performed \n" + e.toString());
    }
  }
}
```

## Troubleshooting

Error string: `  Resources exceeded during query execution: Google Sheets service overloaded.  `

This can be a transient error that can be fixed by rerunning the query. If the error persists after a query rerun, consider simplifying your spreadsheet; for example, by minimizing the use of formulas. For more information, see [external table limitations](/bigquery/docs/external-tables#limitations) .

## What's next

  - Learn about [using SQL in BigQuery](/bigquery/docs/introduction-sql) .
  - Learn about [external tables](/bigquery/docs/external-tables) .
  - Learn about [BigQuery quotas](/bigquery/quotas) .
