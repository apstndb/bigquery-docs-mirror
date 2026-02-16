# Create Google Drive external tables

This document describes how to create an external table over data stored in Google Drive.

BigQuery supports external tables over both personal Drive files and shared files. For more information on Drive, see [Drive training and help](https://support.google.com/a/users/answer/9282958) .

You can create external tables over files in Drive that have the following formats:

  - Comma-separated values (CSV)
  - Newline-delimited JSON
  - Avro
  - Google Sheets

## Before you begin

Before you create an external table, gather some information and make sure you have permission to create the table.

### Retrieve Drive URIs

To create an external table for a Google Drive data source, you must provide the [Drive URI](#drive-uri) . You can retrieve the Drive URI directly from the URL of your Drive data:

**URI format**

  - `  https://docs.google.com/spreadsheets/d/ FILE_ID  `
    
    or

  - `  https://drive.google.com/open?id= FILE_ID  `

where `  FILE_ID  ` is the alphanumeric ID for your Drive file.

### Authenticate and enable Drive access

Accessing data hosted within Drive requires an additional OAuth scope. To authenticate to BigQuery and enable drive access, do the following:

### Console

Follow the web-based authentication steps when you create an [external table](#create_external_tables) in the Google Cloud console. When you are prompted, click **Allow** to give BigQuery Client Tools access to Drive.

### gcloud

1.  In the Google Cloud console, activate Cloud Shell.
    
    At the bottom of the Google Cloud console, a [Cloud Shell](/shell/docs/how-cloud-shell-works) session starts and displays a command-line prompt. Cloud Shell is a shell environment with the Google Cloud CLI already installed and with values already set for your current project. It can take a few seconds for the session to initialize.

2.  Enter the following command to ensure that you have the latest version of the Google Cloud CLI.
    
    ``` text
    gcloud components update
    ```

3.  Enter the following command to authenticate with Drive.
    
    ``` text
    gcloud auth login --enable-gdrive-access
    ```

**Note:** If you use Cloud Shell to access your Drive data, you do not need to update the Google Cloud CLI or authenticate with Drive.

### API

Request the appropriate [OAuth scope for Drive](https://developers.google.com/identity/protocols/googlescopes#drive) in addition to the scope for BigQuery:

1.  Sign in by running the [`  gcloud auth login --enable-gdrive-access  ` command](/sdk/gcloud/reference/auth/login) .
2.  Obtain the OAuth access token with the Drive scope that is used for your API by running the [`  gcloud auth print-access-token  ` command](/sdk/gcloud/reference/auth/print-access-token) .

### Python

1.  [Create an OAuth Client ID](https://support.google.com/cloud/answer/6158849) .

2.  Set up [Application Default Credentials (ADC)](/docs/authentication/application-default-credentials) in your local environment with the required scopes by doing the following:
    
    1.  [Install](/sdk/docs/install) the Google Cloud CLI, then [initialize](/sdk/docs/initializing) it by running the following command:
        
        ``` text
        gcloud init
        ```
    
    2.  Create local authentication credentials for your Google Account:
        
        ``` text
        gcloud auth application-default login \
            --client-id-file=CLIENT_ID_FILE \
            --scopes=https://www.googleapis.com/auth/drive,https://www.googleapis.com/auth/cloud-platform
        ```
        
        Replace `  CLIENT_ID_FILE  ` with the file containing your OAuth Client ID.
        
        For more information, see [User credentials provided by using the gcloud CLI](/docs/authentication/application-default-credentials#personal) .

### Java

1.  [Create an OAuth Client ID](https://support.google.com/cloud/answer/6158849) .

2.  Set up [Application Default Credentials (ADC)](/docs/authentication/application-default-credentials) in your local environment with the required scopes by doing the following:
    
    1.  [Install](/sdk/docs/install) the Google Cloud CLI, then [initialize](/sdk/docs/initializing) it by running the following command:
        
        ``` text
        gcloud init
        ```
    
    2.  Create local authentication credentials for your Google Account:
        
        ``` text
        gcloud auth application-default login \
            --client-id-file=CLIENT_ID_FILE \
            --scopes=https://www.googleapis.com/auth/drive,https://www.googleapis.com/auth/cloud-platform
        ```
        
        Replace `  CLIENT_ID_FILE  ` with the file containing your OAuth Client ID.
        
        For more information, see [User credentials provided by using the gcloud CLI](/docs/authentication/application-default-credentials#personal) .

### Required roles

To create an external table, you need the `  bigquery.tables.create  ` BigQuery Identity and Access Management (IAM) permission.

Each of the following predefined Identity and Access Management roles includes this permission:

  - BigQuery Data Editor ( `  roles/bigquery.dataEditor  ` )
  - BigQuery Data Owner ( `  roles/bigquery.dataOwner  ` )
  - BigQuery Admin ( `  roles/bigquery.admin  ` )

If you are not a principal in any of these roles, ask your administrator to grant you access or to create the external table for you.

For more information on Identity and Access Management roles and permissions in BigQuery, see [Predefined roles and permissions](/bigquery/docs/access-control) .

## Create external tables

You can create a permanent table linked to your external data source by:

  - Using the Google Cloud console
  - Using the bq command-line tool's `  mk  ` command
  - Creating an [`  ExternalDataConfiguration  `](/bigquery/docs/reference/rest/v2/tables#externaldataconfiguration) when you use the [`  tables.insert  `](/bigquery/docs/reference/rest/v2/tables/insert) API method
  - Using the client libraries

To create an external table:

### Console

1.  In the Google Cloud console, open the BigQuery page.

2.  In the left pane, click explore **Explorer** :
    
    If you don't see the left pane, click last\_page **Expand left pane** to open the pane.

3.  In the **Explorer** pane, expand your project, click **Datasets** , and then select a dataset.

4.  In the details pane, click **Create table** add\_box .

5.  On the **Create table** page, in the **Source** section:
    
      - For **Create table from** , select **Drive** .
    
      - In the **Select Drive URI** field, enter the [Drive URI](#drive-uri) . Note that wildcards are not supported for Drive URIs.
    
      - For **File format** , select the format of your data. Valid formats for Drive data include:
        
          - Comma-separated values (CSV)
          - Newline delimited JSON
          - Avro
          - Sheets
        
        **Note:** In the Google Cloud console, choosing Avro or Datastore backup hides the **Automatically detect** option because these file types are self-describing.

6.  (Optional) If you choose Sheets, in the **Sheet range (Optional)** box, specify the sheet and cell range to query. You can specify a sheet name, or you can specify `  sheet_name!top_left_cell_id:bottom_right_cell_id  ` for a cell range; for example, "Sheet1\!A1:B20". If **Sheet range** is not specified, the first sheet in the file is used.

7.  On the **Create table** page, in the **Destination** section:
    
      - For **Dataset name** , choose the appropriate dataset, and in the **Table name** field, enter the name of the table you're creating in BigQuery.
    
      - Verify that **Table type** is set to **External table** .

8.  In the **Schema** section, enter the [schema](/bigquery/docs/schemas) definition.
    
      - For JSON or CSV files, you can check the **Auto-detect** option to enable schema [auto-detect](/bigquery/docs/schema-detect) . **Auto-detect** is not available for Datastore exports, Firestore exports, and Avro files. Schema information for these file types is automatically retrieved from the self-describing source data.
      - Enter schema information manually by:
          - Enabling **Edit as text** and entering the table schema as a JSON array. Note: You can view the schema of an existing table in JSON format by entering the following command in the bq command-line tool: `  bq show --format=prettyjson DATASET . TABLE  ` .
          - Using **Add field** to manually input the schema.

9.  Click **Create table** .

10. If necessary, select your account and then click **Allow** to give the BigQuery client tools access to Drive.

You can then run a query against the table as if it were a standard BigQuery table, subject to the [limitations](/bigquery/external-data-sources#external_data_source_limitations) on external data sources.

After your query completes, you can download the results as CSV or JSON, save the results as a table, or save the results to Sheets. See [Download, save, and export data](/bigquery/bigquery-web-ui#exportdata) for more information.

### bq

You create a table in the bq command-line tool using the `  bq mk  ` command. When you use the bq command-line tool to create a table linked to an external data source, you can identify the table's schema using:

  - A [table definition file](/bigquery/external-table-definition) (stored on your local machine)
  - An inline schema definition
  - A JSON schema file (stored on your local machine)

To create a permanent table linked to your Drive data source using a table definition file, enter the following command.

``` text
bq mk \
--external_table_definition=DEFINITION_FILE \
DATASET.TABLE
```

Where:

  - `  DEFINITION_FILE  ` is the path to the [table definition file](/bigquery/external-table-definition) on your local machine.
  - `  DATASET  ` is the name of the dataset that contains the table.
  - `  TABLE  ` is the name of the table you're creating.

For example, the following command creates a permanent table named `  mytable  ` using a table definition file named `  mytable_def  ` .

``` text
bq mk --external_table_definition=/tmp/mytable_def mydataset.mytable
```

To create a permanent table linked to your external data source using an inline schema definition, enter the following command.

``` text
bq mk \
--external_table_definition=SCHEMA@SOURCE_FORMAT=DRIVE_URI \
DATASET.TABLE
```

Where:

  - `  SCHEMA  ` is the schema definition in the format `  FIELD : DATA_TYPE , FIELD : DATA_TYPE  ` .
  - `  SOURCE_FORMAT  ` is `  CSV  ` , `  NEWLINE_DELIMITED_JSON  ` , `  AVRO  ` , or `  GOOGLE_SHEETS  ` .
  - `  DRIVE_URI  ` is your [Drive URI](#drive-uri) .
  - `  DATASET  ` is the name of the dataset that contains the table.
  - `  TABLE  ` is the name of the table you're creating.

For example, the following command creates a permanent table named `  sales  ` linked to a Sheets file stored in Drive with the following schema definition: `  Region:STRING,Quarter:STRING,Total_sales:INTEGER  ` .

``` text
bq mk \
--external_table_definition=Region:STRING,Quarter:STRING,Total_sales:INTEGER@GOOGLE_SHEETS=https://drive.google.com/open?id=1234_AbCD12abCd \
mydataset.sales
```

To create a permanent table linked to your external data source using a JSON schema file, enter the following command.

``` text
bq mk \
--external_table_definition=SCHEMA_FILE@SOURCE_FORMAT=DRIVE_URI \
DATASET.TABLE
```

Where:

  - `  SCHEMA_FILE  ` is the path to the JSON schema file on your local machine.
  - `  SOURCE_FORMAT  ` is `  CSV  ` , `  NEWLINE_DELIMITED_JSON  ` , `  AVRO  ` , or `  GOOGLE_SHEETS  ` .
  - `  DRIVE_URI  ` is your [Drive URI](#drive-uri) .
  - `  DATASET  ` is the name of the dataset that contains the table.
  - `  TABLE  ` is the name of the table you're creating.

If your [table definition file](/bigquery/external-table-definition) contains [Sheets-specific configuration](/bigquery/docs/reference/rest/v2/tables#GoogleSheetsOptions) , then you can skip leading rows and specify a defined sheet range.

The following example creates a table named `  sales  ` linked to a CSV file stored in Drive using the `  /tmp/sales_schema.json  ` schema file.

``` text
bq mk \
--external_table_definition=/tmp/sales_schema.json@CSV=https://drive.google.com/open?id=1234_AbCD12abCd \
mydataset.sales
```

After the permanent table is created, you can then run a query against the table as if it were a standard BigQuery table, subject to the [limitations](/bigquery/external-data-sources#external_data_source_limitations) on external data sources.

After your query completes, you can download the results as CSV or JSON, save the results as a table, or save the results to Sheets. See [Download, save, and export data](/bigquery/bigquery-web-ui#exportdata) for more information.

### API

Create an [`  ExternalDataConfiguration  `](/bigquery/docs/reference/rest/v2/tables#externaldataconfiguration) when you use the [`  tables.insert  `](/bigquery/docs/reference/rest/v2/tables/insert) API method. Specify the `  schema  ` property or set the `  autodetect  ` property to `  true  ` to enable schema auto detection for supported data sources.

### Python

``` text
from google.cloud import bigquery
import google.auth

credentials, project = google.auth.default()

# Construct a BigQuery client object.
client = bigquery.Client(credentials=credentials, project=project)

# TODO(developer): Set dataset_id to the ID of the dataset to fetch.
# dataset_id = "your-project.your_dataset"

# Configure the external data source.
dataset = client.get_dataset(dataset_id)
table_id = "us_states"
schema = [
    bigquery.SchemaField("name", "STRING"),
    bigquery.SchemaField("post_abbr", "STRING"),
]
table = bigquery.Table(dataset.table(table_id), schema=schema)
external_config = bigquery.ExternalConfig("GOOGLE_SHEETS")
# Use a shareable link or grant viewing access to the email address you
# used to authenticate with BigQuery (this example Sheet is public).
sheet_url = (
    "https://docs.google.com/spreadsheets"
    "/d/1i_QCL-7HcSyUZmIbP9E6lO_T5u3HnpLe7dnpHaijg_E/edit?usp=sharing"
)
external_config.source_uris = [sheet_url]
options = external_config.google_sheets_options
assert options is not None
options.skip_leading_rows = 1  # Optionally skip header row.
options.range = (
    "us-states!A20:B49"  # Optionally set range of the sheet to query from.
)
table.external_data_configuration = external_config

# Create a permanent table linked to the Sheets file.
table = client.create_table(table)  # Make an API request.

# Example query to find states starting with "W".
sql = 'SELECT * FROM `{}.{}` WHERE name LIKE "W%"'.format(dataset_id, table_id)

results = client.query_and_wait(sql)  # Make an API request.

# Wait for the query to complete.
w_states = list(results)
print(
    "There are {} states with names starting with W in the selected range.".format(
        len(w_states)
    )
)
```

### Java

``` text
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
import com.google.cloud.bigquery.TableId;
import com.google.cloud.bigquery.TableInfo;
import com.google.cloud.bigquery.TableResult;
import com.google.common.collect.ImmutableSet;
import java.io.IOException;

// Sample to queries an external data source using a permanent table
public class QueryExternalSheetsPerm {

  public static void main(String[] args) {
    // TODO(developer): Replace these variables before running the sample.
    String datasetName = "MY_DATASET_NAME";
    String tableName = "MY_TABLE_NAME";
    String sourceUri =
        "https://docs.google.com/spreadsheets/d/1i_QCL-7HcSyUZmIbP9E6lO_T5u3HnpLe7dnpHaijg_E/edit?usp=sharing";
    Schema schema =
        Schema.of(
            Field.of("name", StandardSQLTypeName.STRING),
            Field.of("post_abbr", StandardSQLTypeName.STRING));
    String query =
        String.format("SELECT * FROM %s.%s WHERE name LIKE 'W%%'", datasetName, tableName);
    queryExternalSheetsPerm(datasetName, tableName, sourceUri, schema, query);
  }

  public static void queryExternalSheetsPerm(
      String datasetName, String tableName, String sourceUri, Schema schema, String query) {
    try {

      GoogleCredentials credentials =
          ServiceAccountCredentials.getApplicationDefault();

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

      TableId tableId = TableId.of(datasetName, tableName);
      // Create a permanent table linked to the Sheets file.
      ExternalTableDefinition externalTable =
          ExternalTableDefinition.newBuilder(sourceUri, sheetsOptions).setSchema(schema).build();
      bigquery.create(TableInfo.of(tableId, externalTable));

      // Example query to find states starting with 'W'
      TableResult results = bigquery.query(QueryJobConfiguration.of(query));

      results
          .iterateAll()
          .forEach(row -> row.forEach(val -> System.out.printf("%s,", val.toString())));

      System.out.println("Query on external permanent table performed successfully.");
    } catch (BigQueryException | InterruptedException | IOException e) {
      System.out.println("Query not performed \n" + e.toString());
    }
  }
}
```

## Query external tables

For more information, see [Query Drive data](/bigquery/docs/query-drive-data) .

## The `     _FILE_NAME    ` pseudocolumn

Tables based on external data sources provide a pseudo column named `  _FILE_NAME  ` . This column contains the fully qualified path to the file to which the row belongs. This column is available only for tables that reference external data stored in **Cloud Storage** and **Google Drive** .

The `  _FILE_NAME  ` column name is reserved, which means that you cannot create a column by that name in any of your tables.
