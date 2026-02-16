# Create and use tables

This document describes how to create and use [standard (built-in) tables in BigQuery](/bigquery/docs/tables-intro#standard-tables) . For information about creating other table types, see the following:

  - [Creating partitioned tables](/bigquery/docs/creating-partitioned-tables)
  - [Creating and using clustered tables](/bigquery/docs/creating-clustered-tables)

After creating a table, you can do the following:

  - Control access to your table data.
  - Get information about your tables.
  - List the tables in a dataset.
  - Get table metadata.

For more information about managing tables including updating table properties, copying a table, and deleting a table, see [Managing tables](/bigquery/docs/managing-tables) .

## Before you begin

Grant Identity and Access Management (IAM) roles that give users the necessary permissions to perform each task in this document.

### Required roles

To get the permissions that you need to create a table, ask your administrator to grant you the following IAM roles:

  - [BigQuery Job User](/iam/docs/roles-permissions/bigquery#bigquery.jobUser) ( `  roles/bigquery.jobUser  ` ) on the project if you're creating a table by loading data or by saving query results to a table.
  - [BigQuery Data Editor](/iam/docs/roles-permissions/bigquery#bigquery.dataEditor) ( `  roles/bigquery.dataEditor  ` ) on the dataset where you're creating the table.

For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

These predefined roles contain the permissions required to create a table. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

The following permissions are required to create a table:

  - `  bigquery.tables.create  ` on the dataset where you're creating the table.
  - `  bigquery.tables.getData  ` on all tables and views that your query references if you're saving query results as a table.
  - `  bigquery.jobs.create  ` on the project if you're creating the table by loading data or by saving query results to a table.
  - `  bigquery.tables.updateData  ` on the table if you're appending to or overwriting a table with query results.

You might also be able to get these permissions with [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

**Note:** If you have the `  bigquery.datasets.create  ` permission, you can create tables in the datasets that you create.

## Table naming

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

## Create tables

You can create a table in BigQuery in the following ways:

  - Manually by using the Google Cloud console or the bq command-line tool [`  bq mk  `](/bigquery/docs/reference/bq-cli-reference#bq_mk) command.
  - Programmatically by calling the [`  tables.insert  `](/bigquery/docs/reference/rest/v2/tables/insert) API method.
  - By using the client libraries.
  - From query results.
  - By defining a table that references an external data source.
  - When you load data.
  - By using a [`  CREATE TABLE  `](/bigquery/docs/reference/standard-sql/data-definition-language#creating_a_new_table) data definition language (DDL) statement.

### Create an empty table with a schema definition

You can create an empty table with a schema definition in the following ways:

  - Enter the schema using the Google Cloud console.
  - Provide the schema inline using the bq command-line tool.
  - Submit a JSON schema file using the bq command-line tool.
  - Provide the schema in a [table resource](/bigquery/docs/reference/rest/v2/tables#resource:-table) when calling the APIs [`  tables.insert  ` method](/bigquery/docs/reference/rest/v2/tables/insert) .

For more information about specifying a table schema, see [Specifying a schema](/bigquery/docs/schemas) .

After the table is created, you can [load data](/bigquery/docs/loading-data) into it or populate it by [writing query results](/bigquery/docs/writing-results) to it.

To create an empty table with a schema definition:

### Console

In the Google Cloud console, go to the **BigQuery** page.

In the left pane, click explore **Explorer** .

In the **Explorer** pane, expand your project, click **Datasets** , and then select a dataset.

In the **Dataset info** section, click add\_box **Create table** .

In the **Create table** pane, specify the following details:

1.  In the **Source** section, select **Empty table** in the **Create table from** list.
2.  In the **Destination** section, specify the following details:
    1.  For **Dataset** , select the dataset in which you want to create the table.
    2.  In the **Table** field, enter the name of the table that you want to create.
    3.  Verify that the **Table type** field is set to **Native table** .
3.  In the **Schema** section, enter the [schema](/bigquery/docs/schemas) definition. You can enter schema information manually by using one of the following methods:
      - Option 1: Click **Edit as text** and paste the schema in the form of a JSON array. When you use a JSON array, you generate the schema using the same process as [creating a JSON schema file](/bigquery/docs/schemas#specifying_a_json_schema_file) . You can view the schema of an existing table in JSON format by entering the following command:
        
        ``` text
            bq show --format=prettyjson dataset.table
            
        ```
    
      - Option 2: Click add\_box **Add field** and enter the table schema. Specify each field's **Name** , [**Type**](/bigquery/docs/schemas#standard_sql_data_types) , and [**Mode**](/bigquery/docs/schemas#modes) .
4.  Optional: Specify **Partition and cluster settings** . For more information, see [Creating partitioned tables](/bigquery/docs/creating-partitioned-tables) and [Creating and using clustered tables](/bigquery/docs/creating-clustered-tables) .
5.  Optional: In the **Advanced options** section, if you want to use a customer-managed encryption key, then select the **Use a customer-managed encryption key (CMEK)** option. By default, BigQuery [encrypts customer content stored at rest](/docs/security/encryption/default-encryption) by using a Google-owned and Google-managed encryption key.
6.  Click **Create table** .

**Note:** When you create an empty table using the Google Cloud console, you cannot add a label, description, or expiration time. You can add these optional properties when you create a table using the bq command-line tool or API. After you create a table in the Google Cloud console, you can add an expiration, description, and labels.

### SQL

The following example creates a table named `  newtable  ` that expires on January 1, 2023:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
    CREATE TABLE mydataset.newtable (
      x INT64 OPTIONS (description = 'An optional INTEGER field'),
      y STRUCT <
        a ARRAY <STRING> OPTIONS (description = 'A repeated STRING field'),
        b BOOL
      >
    ) OPTIONS (
        expiration_timestamp = TIMESTAMP '2023-01-01 00:00:00 UTC',
        description = 'a table that expires in 2023',
        labels = [('org_unit', 'development')]);
    ```

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](/bigquery/docs/running-queries#queries) .

### bq

1.  In the Google Cloud console, activate Cloud Shell.
    
    At the bottom of the Google Cloud console, a [Cloud Shell](/shell/docs/how-cloud-shell-works) session starts and displays a command-line prompt. Cloud Shell is a shell environment with the Google Cloud CLI already installed and with values already set for your current project. It can take a few seconds for the session to initialize.

2.  Use the [`  bq mk  ` command](/bigquery/docs/reference/bq-cli-reference#bq_mk) with the `  --table  ` or `  -t  ` flag. You can supply table schema information inline or with a JSON schema file. For a full list of parameters, see the [`  bq mk --table  ` reference](/bigquery/docs/reference/bq-cli-reference#mk-table) . Some optional parameters include:
    
      - `  --expiration  `
      - `  --description  `
      - `  --time_partitioning_field  `
      - `  --time_partitioning_type  `
      - `  --range_partitioning  `
      - `  --clustering_fields  `
      - `  --destination_kms_key  `
      - `  --label  `
    
    `  --time_partitioning_field  ` , `  --time_partitioning_type  ` , `  --range_partitioning  ` , `  --clustering_fields  ` , and `  --destination_kms_key  ` are not demonstrated here. Refer to the following links for more information on these optional parameters:
    
      - For more information about `  --time_partitioning_field  ` , `  --time_partitioning_type  ` , and `  --range_partitioning  ` see [partitioned tables](/bigquery/docs/creating-partitioned-tables) .
      - For more information about `  --clustering_fields  ` , see [clustered tables](/bigquery/docs/creating-clustered-tables) .
      - For more information about `  --destination_kms_key  ` , see [customer-managed encryption keys](/bigquery/docs/customer-managed-encryption) .
    
    If you are creating a table in a project other than your default project, add the project ID to the dataset in the following format: `  project_id:dataset  ` .
    
    To create an empty table in an existing dataset with a schema definition, enter the following:
    
    ``` text
    bq mk \
    --table \
    --expiration=integer \
    --description=description \
    --label=key_1:value_1 \
    --label=key_2:value_2 \
    --add_tags=key_3:value_3[,...] \
    project_id:dataset.table \
    schema
    ```
    
    Replace the following:
    
      - integer is the default lifetime (in seconds) for the table. The minimum value is 3600 seconds (one hour). The expiration time evaluates to the current UTC time plus the integer value. If you set the expiration time when you create a table, the dataset's default table expiration setting is ignored.
      - description is a description of the table in quotes.
      - key\_1 : value\_1 and key\_2 : value\_2 are key-value pairs that specify [labels](/bigquery/docs/labels) .
      - key\_3 : value\_3 are key-value pairs that specify [tags](/bigquery/docs/tags) . Add multiple tags under the same flag with commas between key:value pairs.
      - project\_id is your project ID.
      - dataset is a dataset in your project.
      - table is the name of the table you're creating.
      - schema is an inline schema definition in the format field:data\_type,field:data\_type or the path to the JSON schema file on your local machine.
    
    When you specify the schema on the command line, you cannot include a `  RECORD  ` ( [`  STRUCT  `](/bigquery/docs/reference/standard-sql/data-types#struct_type) ) type, you cannot include a column description, and you cannot specify the column mode. All modes default to `  NULLABLE  ` . To include descriptions, modes, and `  RECORD  ` types, [supply a JSON schema file](/bigquery/docs/schemas#specifying_a_json_schema_file) instead.
    
    Examples:
    
    Enter the following command to create a table using an inline schema definition. This command creates a table named `  mytable  ` in `  mydataset  ` in your default project. The table expiration is set to 3600 seconds (1 hour), the description is set to `  This is my table  ` , and the label is set to `  organization:development  ` . The command uses the `  -t  ` shortcut instead of `  --table  ` . The schema is specified inline as: `  qtr:STRING,sales:FLOAT,year:STRING  ` .
    
    ``` text
    bq mk \
     -t \
     --expiration 3600 \
     --description "This is my table" \
     --label organization:development \
     mydataset.mytable \
     qtr:STRING,sales:FLOAT,year:STRING
    ```
    
    Enter the following command to create a table using a JSON schema file. This command creates a table named `  mytable  ` in `  mydataset  ` in your default project. The table expiration is set to 3600 seconds (1 hour), the description is set to `  This is my table  ` , and the label is set to `  organization:development  ` . The path to the schema file is `  /tmp/myschema.json  ` .
    
    ``` text
    bq mk \
     --table \
     --expiration 3600 \
     --description "This is my table" \
     --label organization:development \
     mydataset.mytable \
     /tmp/myschema.json
    ```
    
    Enter the following command to create a table using an JSON schema file. This command creates a table named `  mytable  ` in `  mydataset  ` in `  myotherproject  ` . The table expiration is set to 3600 seconds (1 hour), the description is set to `  This is my table  ` , and the label is set to `  organization:development  ` . The path to the schema file is `  /tmp/myschema.json  ` .
    
    ``` text
    bq mk \
     --table \
     --expiration 3600 \
     --description "This is my table" \
     --label organization:development \
     myotherproject:mydataset.mytable \
     /tmp/myschema.json
    ```
    
    After the table is created, you can [update](/bigquery/docs/managing-tables) the table's expiration, description, and labels. You can also [modify the schema definition](/bigquery/docs/managing-table-schemas) .

### Terraform

Use the [`  google_bigquery_table  `](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/bigquery_table) resource.

**Note:** To create BigQuery objects using Terraform, you must enable the Cloud Resource Manager API.

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

**Create a table**

The following example creates a table named `  mytable  ` :

``` terraform
resource "google_bigquery_dataset" "default" {
  dataset_id                      = "mydataset"
  default_partition_expiration_ms = 2592000000  # 30 days
  default_table_expiration_ms     = 31536000000 # 365 days
  description                     = "dataset description"
  location                        = "US"
  max_time_travel_hours           = 96 # 4 days

  labels = {
    billing_group = "accounting",
    pii           = "sensitive"
  }
}

resource "google_bigquery_table" "default" {
  dataset_id = google_bigquery_dataset.default.dataset_id
  table_id   = "mytable"

  schema = <<EOF
[
  {
    "name": "ID",
    "type": "INT64",
    "mode": "NULLABLE",
    "description": "Item ID"
  },
  {
    "name": "Item",
    "type": "STRING",
    "mode": "NULLABLE"
  }
]
EOF

}
```

**Create a table and grant access to it**

The following example creates a table named `  mytable  ` , then uses the [`  google_bigquery_table_iam_policy  `](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/bigquery_table_iam#google_bigquery_table_iam_policy) resource to grant access to it. Take this step only if you want to grant access to the table to principals who don't have access to the dataset in which the table resides.

``` terraform
resource "google_bigquery_dataset" "default" {
  dataset_id                      = "mydataset"
  default_partition_expiration_ms = 2592000000  # 30 days
  default_table_expiration_ms     = 31536000000 # 365 days
  description                     = "dataset description"
  location                        = "US"
  max_time_travel_hours           = 96 # 4 days

  labels = {
    billing_group = "accounting",
    pii           = "sensitive"
  }
}

resource "google_bigquery_table" "default" {
  dataset_id = google_bigquery_dataset.default.dataset_id
  table_id   = "mytable"

  schema = <<EOF
[
  {
    "name": "ID",
    "type": "INT64",
    "mode": "NULLABLE",
    "description": "Item ID"
  },
  {
    "name": "Item",
    "type": "STRING",
    "mode": "NULLABLE"
  }
]
EOF

}

data "google_iam_policy" "default" {
  binding {
    role = "roles/bigquery.dataOwner"
    members = [
      "user:raha@altostrat.com",
    ]
  }
}

resource "google_bigquery_table_iam_policy" "policy" {
  dataset_id  = google_bigquery_table.default.dataset_id
  table_id    = google_bigquery_table.default.table_id
  policy_data = data.google_iam_policy.default.policy_data
}
```

**Create a table with a customer-managed encryption key**

The following example creates a table named `  mytable  ` , and also uses the [`  google_kms_crypto_key  `](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/kms_crypto_key) and [`  google_kms_key_ring  `](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/kms_key_ring) resources to specify a [Cloud Key Management Service key](/bigquery/docs/customer-managed-encryption) for the table. You must [enable the Cloud Key Management Service API](https://console.cloud.google.com/flows/enableapi?apiid=cloudkms.googleapis.com&redirect=https://console.cloud.google.com/) before running this example.

``` terraform
resource "google_bigquery_dataset" "default" {
  dataset_id                      = "mydataset"
  default_partition_expiration_ms = 2592000000  # 30 days
  default_table_expiration_ms     = 31536000000 # 365 days
  description                     = "dataset description"
  location                        = "US"
  max_time_travel_hours           = 96 # 4 days

  labels = {
    billing_group = "accounting",
    pii           = "sensitive"
  }
}

resource "google_bigquery_table" "default" {
  dataset_id = google_bigquery_dataset.default.dataset_id
  table_id   = "mytable"

  schema = <<EOF
[
  {
    "name": "ID",
    "type": "INT64",
    "mode": "NULLABLE",
    "description": "Item ID"
  },
  {
    "name": "Item",
    "type": "STRING",
    "mode": "NULLABLE"
  }
]
EOF

  encryption_configuration {
    kms_key_name = google_kms_crypto_key.crypto_key.id
  }

  depends_on = [google_project_iam_member.service_account_access]
}

resource "google_kms_crypto_key" "crypto_key" {
  name     = "example-key"
  key_ring = google_kms_key_ring.key_ring.id
}

resource "random_id" "default" {
  byte_length = 8
}

resource "google_kms_key_ring" "key_ring" {
  name     = "${random_id.default.hex}-example-keyring"
  location = "us"
}

# Enable the BigQuery service account to encrypt/decrypt Cloud KMS keys
data "google_project" "project" {
}

resource "google_project_iam_member" "service_account_access" {
  project = data.google_project.project.project_id
  role    = "roles/cloudkms.cryptoKeyEncrypterDecrypter"
  member  = "serviceAccount:bq-${data.google_project.project.number}@bigquery-encryption.iam.gserviceaccount.com"
}
```

To apply your Terraform configuration in a Google Cloud project, complete the steps in the following sections.

## Prepare Cloud Shell

1.  Launch [Cloud Shell](https://shell.cloud.google.com/) .

2.  Set the default Google Cloud project where you want to apply your Terraform configurations.
    
    You only need to run this command once per project, and you can run it in any directory.
    
    ``` text
    export GOOGLE_CLOUD_PROJECT=PROJECT_ID
    ```
    
    Environment variables are overridden if you set explicit values in the Terraform configuration file.

## Prepare the directory

Each Terraform configuration file must have its own directory (also called a *root module* ).

1.  In [Cloud Shell](https://shell.cloud.google.com/) , create a directory and a new file within that directory. The filename must have the `  .tf  ` extension—for example `  main.tf  ` . In this tutorial, the file is referred to as `  main.tf  ` .
    
    ``` text
    mkdir DIRECTORY && cd DIRECTORY && touch main.tf
    ```

2.  If you are following a tutorial, you can copy the sample code in each section or step.
    
    Copy the sample code into the newly created `  main.tf  ` .
    
    Optionally, copy the code from GitHub. This is recommended when the Terraform snippet is part of an end-to-end solution.

3.  Review and modify the sample parameters to apply to your environment.

4.  Save your changes.

5.  Initialize Terraform. You only need to do this once per directory.
    
    ``` text
    terraform init
    ```
    
    Optionally, to use the latest Google provider version, include the `  -upgrade  ` option:
    
    ``` text
    terraform init -upgrade
    ```

## Apply the changes

1.  Review the configuration and verify that the resources that Terraform is going to create or update match your expectations:
    
    ``` text
    terraform plan
    ```
    
    Make corrections to the configuration as necessary.

2.  Apply the Terraform configuration by running the following command and entering `  yes  ` at the prompt:
    
    ``` text
    terraform apply
    ```
    
    Wait until Terraform displays the "Apply complete\!" message.

3.  [Open your Google Cloud project](https://console.cloud.google.com/) to view the results. In the Google Cloud console, navigate to your resources in the UI to make sure that Terraform has created or updated them.

**Note:** Terraform samples typically assume that the required APIs are enabled in your Google Cloud project.

### API

Call the [`  tables.insert  `](/bigquery/docs/reference/rest/v2/tables/insert) method with a defined [table resource](/bigquery/docs/reference/rest/v2/tables) .

### C\#

Before trying this sample, follow the C\# setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery C\# API reference documentation](/dotnet/docs/reference/Google.Cloud.BigQuery.V2/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` csharp
using Google.Cloud.BigQuery.V2;

public class BigQueryCreateTable
{
    public BigQueryTable CreateTable(
        string projectId = "your-project-id",
        string datasetId = "your_dataset_id"
    )
    {
        BigQueryClient client = BigQueryClient.Create(projectId);
        var dataset = client.GetDataset(datasetId);
        // Create schema for new table.
        var schema = new TableSchemaBuilder
        {
            { "full_name", BigQueryDbType.String },
            { "age", BigQueryDbType.Int64 }
        }.Build();
        // Create the table
        return dataset.CreateTable(tableId: "your_table_id", schema: schema);
    }
}
```

### Go

Before trying this sample, follow the Go setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Go API reference documentation](https://godoc.org/cloud.google.com/go/bigquery) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` go
import (
 "context"
 "fmt"
 "time"

 "cloud.google.com/go/bigquery"
)

// createTableExplicitSchema demonstrates creating a new BigQuery table and specifying a schema.
func createTableExplicitSchema(projectID, datasetID, tableID string) error {
 // projectID := "my-project-id"
 // datasetID := "mydatasetid"
 // tableID := "mytableid"
 ctx := context.Background()

 client, err := bigquery.NewClient(ctx, projectID)
 if err != nil {
     return fmt.Errorf("bigquery.NewClient: %v", err)
 }
 defer client.Close()

 sampleSchema := bigquery.Schema{
     {Name: "full_name", Type: bigquery.StringFieldType},
     {Name: "age", Type: bigquery.IntegerFieldType},
 }

 metaData := &bigquery.TableMetadata{
     Schema:         sampleSchema,
     ExpirationTime: time.Now().AddDate(1, 0, 0), // Table will be automatically deleted in 1 year.
 }
 tableRef := client.Dataset(datasetID).Table(tableID)
 if err := tableRef.Create(ctx, metaData); err != nil {
     return err
 }
 return nil
}
```

### Java

Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Java API reference documentation](/java/docs/reference/google-cloud-bigquery/latest/overview) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` java
import com.google.cloud.bigquery.BigQuery;
import com.google.cloud.bigquery.BigQueryException;
import com.google.cloud.bigquery.BigQueryOptions;
import com.google.cloud.bigquery.Field;
import com.google.cloud.bigquery.Schema;
import com.google.cloud.bigquery.StandardSQLTypeName;
import com.google.cloud.bigquery.StandardTableDefinition;
import com.google.cloud.bigquery.TableDefinition;
import com.google.cloud.bigquery.TableId;
import com.google.cloud.bigquery.TableInfo;

public class CreateTable {

  public static void runCreateTable() {
    // TODO(developer): Replace these variables before running the sample.
    String datasetName = "MY_DATASET_NAME";
    String tableName = "MY_TABLE_NAME";
    Schema schema =
        Schema.of(
            Field.of("stringField", StandardSQLTypeName.STRING),
            Field.of("booleanField", StandardSQLTypeName.BOOL));
    createTable(datasetName, tableName, schema);
  }

  public static void createTable(String datasetName, String tableName, Schema schema) {
    try {
      // Initialize client that will be used to send requests. This client only needs to be created
      // once, and can be reused for multiple requests.
      BigQuery bigquery = BigQueryOptions.getDefaultInstance().getService();

      TableId tableId = TableId.of(datasetName, tableName);
      TableDefinition tableDefinition = StandardTableDefinition.of(schema);
      TableInfo tableInfo = TableInfo.newBuilder(tableId, tableDefinition).build();

      bigquery.create(tableInfo);
      System.out.println("Table created successfully");
    } catch (BigQueryException e) {
      System.out.println("Table was not created. \n" + e.toString());
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

async function createTable() {
  // Creates a new table named "my_table" in "my_dataset".

  /**
   * TODO(developer): Uncomment the following lines before running the sample.
   */
  // const datasetId = "my_dataset";
  // const tableId = "my_table";
  // const schema = 'Name:string, Age:integer, Weight:float, IsMagic:boolean';

  // For all options, see https://cloud.google.com/bigquery/docs/reference/v2/tables#resource
  const options = {
    schema: schema,
    location: 'US',
  };

  // Create a new table in the dataset
  const [table] = await bigquery
    .dataset(datasetId)
    .createTable(tableId, options);

  console.log(`Table ${table.id} created.`);
}
```

### PHP

Before trying this sample, follow the PHP setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery PHP API reference documentation](/php/docs/reference/cloud-bigquery/latest/BigQueryClient) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` php
use Google\Cloud\BigQuery\BigQueryClient;

/** Uncomment and populate these variables in your code */
// $projectId = 'The Google project ID';
// $datasetId = 'The BigQuery dataset ID';
// $tableId = 'The BigQuery table ID';
// $fields = [
//    [
//        'name' => 'field1',
//        'type' => 'string',
//        'mode' => 'required'
//    ],
//    [
//        'name' => 'field2',
//        'type' => 'integer'
//    ],
//];

$bigQuery = new BigQueryClient([
    'projectId' => $projectId,
]);
$dataset = $bigQuery->dataset($datasetId);
$schema = ['fields' => $fields];
$table = $dataset->createTable($tableId, ['schema' => $schema]);
printf('Created table %s' . PHP_EOL, $tableId);
```

### Python

Before trying this sample, follow the Python setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Python API reference documentation](/python/docs/reference/bigquery/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` python
from google.cloud import bigquery

# Construct a BigQuery client object.
client = bigquery.Client()

# TODO(developer): Set table_id to the ID of the table to create.
# table_id = "your-project.your_dataset.your_table_name"

schema = [
    bigquery.SchemaField("full_name", "STRING", mode="REQUIRED"),
    bigquery.SchemaField("age", "INTEGER", mode="REQUIRED"),
]

table = bigquery.Table(table_id, schema=schema)
table = client.create_table(table)  # Make an API request.
print(
    "Created table {}.{}.{}".format(table.project, table.dataset_id, table.table_id)
)
```

### Ruby

Before trying this sample, follow the Ruby setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Ruby API reference documentation](https://googleapis.dev/ruby/google-cloud-bigquery/latest/Google/Cloud/Bigquery.html) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` ruby
require "google/cloud/bigquery"

def create_table dataset_id = "my_dataset"
  bigquery = Google::Cloud::Bigquery.new
  dataset  = bigquery.dataset dataset_id
  table_id = "my_table"

  table = dataset.create_table table_id do |updater|
    updater.string  "full_name", mode: :required
    updater.integer "age",       mode: :required
  end

  puts "Created table: #{table_id}"
end
```

### Create an empty table without a schema definition

### Java

Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Java API reference documentation](/java/docs/reference/google-cloud-bigquery/latest/overview) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` java
import com.google.cloud.bigquery.BigQuery;
import com.google.cloud.bigquery.BigQueryException;
import com.google.cloud.bigquery.BigQueryOptions;
import com.google.cloud.bigquery.Schema;
import com.google.cloud.bigquery.StandardTableDefinition;
import com.google.cloud.bigquery.TableDefinition;
import com.google.cloud.bigquery.TableId;
import com.google.cloud.bigquery.TableInfo;

// Sample to create a table without schema
public class CreateTableWithoutSchema {

  public static void main(String[] args) {
    // TODO(developer): Replace these variables before running the sample.
    String datasetName = "MY_DATASET_NAME";
    String tableName = "MY_TABLE_NAME";
    createTableWithoutSchema(datasetName, tableName);
  }

  public static void createTableWithoutSchema(String datasetName, String tableName) {
    try {
      // Initialize client that will be used to send requests. This client only needs to be created
      // once, and can be reused for multiple requests.
      BigQuery bigquery = BigQueryOptions.getDefaultInstance().getService();

      TableId tableId = TableId.of(datasetName, tableName);
      TableDefinition tableDefinition = StandardTableDefinition.of(Schema.of());
      TableInfo tableInfo = TableInfo.newBuilder(tableId, tableDefinition).build();

      bigquery.create(tableInfo);
      System.out.println("Table created successfully");
    } catch (BigQueryException e) {
      System.out.println("Table was not created. \n" + e.toString());
    }
  }
}
```

### Create a table from a query result

To create a table from a query result, write the results to a destination table.

### Console

1.  Open the BigQuery page in the Google Cloud console.

2.  In the left pane, click explore **Explorer** :
    
    If you don't see the left pane, click last\_page **Expand left pane** to open the pane.

3.  In the **Explorer** pane, expand your project, click **Datasets** , and then select a dataset.

4.  In the query editor, enter a valid SQL query.

5.  Click **More** and then select **Query settings** .

6.  Select the **Set a destination table for query results** option.

7.  In the **Destination** section, select the **Dataset** in which you want to create the table, and then choose a **Table Id** .

8.  In the **Destination table write preference** section, choose one of the following:
    
      - **Write if empty** — Writes the query results to the table only if the table is empty.
      - **Append to table** — Appends the query results to an existing table.
      - **Overwrite table** — Overwrites an existing table with the same name using the query results.

9.  Optional: For **Data location** , choose your [location](/bigquery/docs/locations) .

10. To update the query settings, click **Save** .

11. Click **Run** . This creates a query job that writes the query results to the table you specified.

Alternatively, if you forget to specify a destination table before running your query, you can copy the cached results table to a permanent table by clicking the [**Save Results**](#save-query-results) button above the editor.

### SQL

The following example uses the [`  CREATE TABLE  ` statement](/bigquery/docs/reference/standard-sql/data-definition-language#create_table_statement) to create the `  trips  ` table from data in the public `  bikeshare_trips  ` table:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
    CREATE TABLE mydataset.trips AS (
      SELECT
        bike_id,
        start_time,
        duration_minutes
      FROM
        bigquery-public-data.austin_bikeshare.bikeshare_trips
    );
    ```

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](/bigquery/docs/running-queries#queries) .

For more information, see [Creating a new table from an existing table](/bigquery/docs/reference/standard-sql/data-definition-language#creating_a_new_table_from_an_existing_table) .

### bq

1.  In the Google Cloud console, activate Cloud Shell.
    
    At the bottom of the Google Cloud console, a [Cloud Shell](/shell/docs/how-cloud-shell-works) session starts and displays a command-line prompt. Cloud Shell is a shell environment with the Google Cloud CLI already installed and with values already set for your current project. It can take a few seconds for the session to initialize.

2.  Enter the [`  bq query  `](/bigquery/docs/reference/bq-cli-reference#bq_query) command and specify the `  --destination_table  ` flag to create a permanent table based on the query results. Specify the `  use_legacy_sql=false  ` flag to use GoogleSQL syntax. To write the query results to a table that is not in your default project, add the project ID to the dataset name in the following format: `  project_id : dataset  ` .
    
    Optional: Supply the `  --location  ` flag and set the value to your [location](/bigquery/docs/dataset-locations) .
    
    To control the write disposition for an existing destination table, specify one of the following optional flags:
    
      - `  --append_table  ` : If the destination table exists, the query results are appended to it.
    
      - `  --replace  ` : If the destination table exists, it is overwritten with the query results.
        
        ``` text
        bq --location=location query \
        --destination_table project_id:dataset.table \
        --use_legacy_sql=false 'query'
        ```
        
        Replace the following:
    
      - `  location  ` is the name of the location used to process the query. The `  --location  ` flag is optional. For example, if you are using BigQuery in the Tokyo region, you can set the flag's value to `  asia-northeast1  ` . You can set a default value for the location by using the [`  .bigqueryrc  ` file](/bigquery/docs/bq-command-line-tool#setting_default_values_for_command-line_flags) .
    
      - `  project_id  ` is your project ID.
    
      - `  dataset  ` is the name of the dataset that contains the table to which you are writing the query results.
    
      - `  table  ` is the name of the table to which you're writing the query results.
    
      - `  query  ` is a query in GoogleSQL syntax.
        
        If no write disposition flag is specified, the default behavior is to write the results to the table only if it is empty. If the table exists and it is not empty, the following error is returned: `  BigQuery error in query operation: Error processing job project_id :bqjob_123abc456789_00000e1234f_1: Already Exists: Table project_id:dataset.table  ` .
        
        Examples:
        
        **Note:** These examples query a US-based public dataset. Because the public dataset is stored in the US multi-region location, the dataset that contains your destination table must also be in the US. You cannot query a dataset in one location and write the results to a destination table in another location.
        
        Enter the following command to write query results to a destination table named `  mytable  ` in `  mydataset  ` . The dataset is in your default project. Since no write disposition flag is specified in the command, the table must be new or empty. Otherwise, an `  Already exists  ` error is returned. The query retrieves data from the [USA Name Data public dataset](https://console.cloud.google.com/marketplace/product/social-security-administration/us-names) .
        
        ``` text
        bq query \
        --destination_table mydataset.mytable \
        --use_legacy_sql=false \
        'SELECT
        name,
        number
        FROM
        `bigquery-public-data`.usa_names.usa_1910_current
        WHERE
        gender = "M"
        ORDER BY
        number DESC'
        ```
        
        Enter the following command to use query results to overwrite a destination table named `  mytable  ` in `  mydataset  ` . The dataset is in your default project. The command uses the `  --replace  ` flag to overwrite the destination table.
        
        ``` text
        bq query \
        --destination_table mydataset.mytable \
        --replace \
        --use_legacy_sql=false \
        'SELECT
        name,
        number
        FROM
        `bigquery-public-data`.usa_names.usa_1910_current
        WHERE
        gender = "M"
        ORDER BY
        number DESC'
        ```
        
        Enter the following command to append query results to a destination table named `  mytable  ` in `  mydataset  ` . The dataset is in `  my-other-project  ` , not your default project. The command uses the `  --append_table  ` flag to append the query results to the destination table.
        
        ``` text
        bq query \
        --append_table \
        --use_legacy_sql=false \
        --destination_table my-other-project:mydataset.mytable \
        'SELECT
        name,
        number
        FROM
        `bigquery-public-data`.usa_names.usa_1910_current
        WHERE
        gender = "M"
        ORDER BY
        number DESC'
        ```
        
        The output for each of these examples looks like the following. For readability, some output is truncated.
        
        ``` text
        Waiting on bqjob_r123abc456_000001234567_1 ... (2s) Current status: DONE
        +---------+--------+
        |  name   | number |
        +---------+--------+
        | Robert  |  10021 |
        | John    |   9636 |
        | Robert  |   9297 |
        | ...              |
        +---------+--------+
        ```

### API

To save query results to a permanent table, call the [`  jobs.insert  `](/bigquery/docs/reference/rest/v2/jobs/insert) method, configure a `  query  ` job, and include a value for the `  destinationTable  ` property. To control the write disposition for an existing destination table, configure the `  writeDisposition  ` property.

To control the processing location for the query job, specify the `  location  ` property in the `  jobReference  ` section of the [job resource](/bigquery/docs/reference/rest/v2/jobs) .

### Go

Before trying this sample, follow the Go setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Go API reference documentation](https://godoc.org/cloud.google.com/go/bigquery) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` go
import (
 "context"
 "fmt"
 "io"

 "cloud.google.com/go/bigquery"
 "google.golang.org/api/iterator"
)

// queryWithDestination demonstrates saving the results of a query to a specific table by setting the destination
// via the API properties.
func queryWithDestination(w io.Writer, projectID, destDatasetID, destTableID string) error {
 // projectID := "my-project-id"
 // datasetID := "mydataset"
 // tableID := "mytable"
 ctx := context.Background()
 client, err := bigquery.NewClient(ctx, projectID)
 if err != nil {
     return fmt.Errorf("bigquery.NewClient: %v", err)
 }
 defer client.Close()

 q := client.Query("SELECT 17 as my_col")
 q.Location = "US" // Location must match the dataset(s) referenced in query.
 q.QueryConfig.Dst = client.Dataset(destDatasetID).Table(destTableID)
 // Run the query and print results when the query job is completed.
 job, err := q.Run(ctx)
 if err != nil {
     return err
 }
 status, err := job.Wait(ctx)
 if err != nil {
     return err
 }
 if err := status.Err(); err != nil {
     return err
 }
 it, err := job.Read(ctx)
 for {
     var row []bigquery.Value
     err := it.Next(&row)
     if err == iterator.Done {
         break
     }
     if err != nil {
         return err
     }
     fmt.Fprintln(w, row)
 }
 return nil
}
```

### Java

Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Java API reference documentation](/java/docs/reference/google-cloud-bigquery/latest/overview) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

To save query results to a permanent table, set the [destination table](https://cloud.google.com/java/docs/reference/google-cloud-bigquery/latest/com.google.cloud.bigquery.QueryJobConfiguration.Builder#com_google_cloud_bigquery_QueryJobConfiguration_Builder_setDestinationTable_com_google_cloud_bigquery_TableId_) to the desired [TableId](https://cloud.google.com/java/docs/reference/google-cloud-bigquery/latest/com.google.cloud.bigquery.TableId) in a [QueryJobConfiguration](https://cloud.google.com/java/docs/reference/google-cloud-bigquery/latest/com.google.cloud.bigquery.QueryJobConfiguration) .

``` java
import com.google.cloud.bigquery.BigQuery;
import com.google.cloud.bigquery.BigQueryException;
import com.google.cloud.bigquery.BigQueryOptions;
import com.google.cloud.bigquery.QueryJobConfiguration;
import com.google.cloud.bigquery.TableId;

public class SaveQueryToTable {

  public static void runSaveQueryToTable() {
    // TODO(developer): Replace these variables before running the sample.
    String query = "SELECT corpus FROM `bigquery-public-data.samples.shakespeare` GROUP BY corpus;";
    String destinationTable = "MY_TABLE";
    String destinationDataset = "MY_DATASET";

    saveQueryToTable(destinationDataset, destinationTable, query);
  }

  public static void saveQueryToTable(
      String destinationDataset, String destinationTableId, String query) {
    try {
      // Initialize client that will be used to send requests. This client only needs to be created
      // once, and can be reused for multiple requests.
      BigQuery bigquery = BigQueryOptions.getDefaultInstance().getService();

      // Identify the destination table
      TableId destinationTable = TableId.of(destinationDataset, destinationTableId);

      // Build the query job
      QueryJobConfiguration queryConfig =
          QueryJobConfiguration.newBuilder(query).setDestinationTable(destinationTable).build();

      // Execute the query.
      bigquery.query(queryConfig);

      // The results are now saved in the destination table.

      System.out.println("Saved query ran successfully");
    } catch (BigQueryException | InterruptedException e) {
      System.out.println("Saved query did not run \n" + e.toString());
    }
  }
}
```

### Node.js

Before trying this sample, follow the Node.js setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Node.js API reference documentation](https://googleapis.dev/nodejs/bigquery/latest/index.html) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` javascript
// Import the Google Cloud client library
const {BigQuery} = require('@google-cloud/bigquery');
const bigquery = new BigQuery();

async function queryDestinationTable() {
  // Queries the U.S. given names dataset for the state of Texas
  // and saves results to permanent table.

  /**
   * TODO(developer): Uncomment the following lines before running the sample.
   */
  // const datasetId = 'my_dataset';
  // const tableId = 'my_table';

  // Create destination table reference
  const dataset = bigquery.dataset(datasetId);
  const destinationTable = dataset.table(tableId);

  const query = `SELECT name
    FROM \`bigquery-public-data.usa_names.usa_1910_2013\`
    WHERE state = 'TX'
    LIMIT 100`;

  // For all options, see https://cloud.google.com/bigquery/docs/reference/v2/tables#resource
  const options = {
    query: query,
    // Location must match that of the dataset(s) referenced in the query.
    location: 'US',
    destination: destinationTable,
  };

  // Run the query as a job
  const [job] = await bigquery.createQueryJob(options);

  console.log(`Job ${job.id} started.`);
  console.log(`Query results loaded to table ${destinationTable.id}`);
}
```

### Python

Before trying this sample, follow the Python setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Python API reference documentation](/python/docs/reference/bigquery/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

To save query results to a permanent table, create a [QueryJobConfig](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJob#google_cloud_bigquery_job_QueryJob) and set the [destination](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJob#google_cloud_bigquery_job_QueryJob_destination) to the desired [TableReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableReference) . Pass the job configuration to the [query method](/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client#google_cloud_bigquery_client_Client_query) .

``` python
from google.cloud import bigquery

# Construct a BigQuery client object.
client = bigquery.Client()

# TODO(developer): Set table_id to the ID of the destination table.
# table_id = "your-project.your_dataset.your_table_name"

job_config = bigquery.QueryJobConfig(destination=table_id)

sql = """
    SELECT corpus
    FROM `bigquery-public-data.samples.shakespeare`
    GROUP BY corpus;
"""

# Start the query, passing in the extra configuration.
query_job = client.query(sql, job_config=job_config)  # Make an API request.
query_job.result()  # Wait for the job to complete.

print("Query results loaded to the table {}".format(table_id))
```

### Create a table that references an external data source

An external data source is a data source that you can query directly from BigQuery, even though the data is not stored in BigQuery storage. For example, you might have data in a different Google Cloud database, in files in Cloud Storage, or in a different cloud product altogether that you would like to analyze in BigQuery, but that you aren't prepared to migrate.

For more information, see [Introduction to external data sources](/bigquery/external-data-sources) .

### Create a table when you load data

When you load data into BigQuery, you can load data into a new table or partition, you can append data to an existing table or partition, or you can overwrite a table or partition. You don't need to create an empty table before loading data into it. You can create the new table and load your data at the same time.

When you load data into BigQuery, you can supply the table or partition schema, or for supported data formats, you can use schema [auto-detection](/bigquery/docs/schema-detect) .

For more information about loading data, see [Introduction to loading data into BigQuery](/bigquery/docs/loading-data) .

### Create a multimodal table

**Preview**

This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

**Note:** To provide feedback or request support for this feature, send an email to <bq-objectref-feedback@google.com> .

You can create a table with one or more [`  ObjectRef  `](/bigquery/docs/objectref-columns) columns in order to store metadata about unstructured data that is related to the other structured data in the table. For example, in a products table, you could create an `  ObjectRef  ` column to store product image information along with the other product data. The unstructured data itself is stored in Cloud Storage, and is made available in BigQuery by using an [object table](/bigquery/docs/object-table-introduction) .

To learn how to create a multimodal table, see [Analyze multimodal data with SQL and Python UDFs](/bigquery/docs/multimodal-data-sql-tutorial) .

## Control access to tables

To configure access to tables and views, you can grant an IAM role to an entity at the following levels, listed in order of range of resources allowed (largest to smallest):

  - a high level in the [Google Cloud resource hierarchy](/resource-manager/docs/cloud-platform-resource-hierarchy) such as the project, folder, or organization level
  - the dataset level
  - the table or view level

You can also restrict data access within tables, by using the following methods:

  - [column-level security](/bigquery/docs/column-level-security-intro)
  - [column data masking](/bigquery/docs/column-data-masking-intro)
  - [row-level security](/bigquery/docs/row-level-security-intro)

Access with any resource protected by IAM is additive. For example, if an entity does not have access at the high level such as a project, you could grant the entity access at the dataset level, and then the entity will have access to the tables and views in the dataset. Similarly, if the entity does not have access at the high level or the dataset level, you could grant the entity access at the table or view level.

Granting IAM roles at a higher level in the [Google Cloud resource hierarchy](/resource-manager/docs/cloud-platform-resource-hierarchy) such as the project, folder, or organization level gives the entity access to a broad set of resources. For example, granting a role to an entity at the project level gives that entity permissions that apply to all datasets throughout the project.

Granting a role at the dataset level specifies the operations an entity is allowed to perform on tables and views in that specific dataset, even if the entity does not have access at a higher level. For information on configuring dataset-level access controls, see [Controlling access to datasets](/bigquery/docs/dataset-access-controls) .

Granting a role at the table or view level specifies the operations an entity is allowed to perform on specific tables and views, even if the entity does not have access at a higher level. For information on configuring table-level access controls, see [Controlling access to tables and views](/bigquery/docs/table-access-controls) .

You can also create [IAM custom roles](/iam/docs/creating-custom-roles) . If you create a custom role, the permissions you grant depend on the specific operations you want the entity to be able to perform.

You can't set a "deny" permission on any resource protected by IAM.

For more information about roles and permissions, see [Understanding roles](/iam/docs/understanding-roles) in the IAM documentation and the BigQuery [IAM roles and permissions](/bigquery/docs/access-control) .

## Get information about tables

You can get information or metadata about tables in the following ways:

  - Using the Google Cloud console.
  - Using the bq command-line tool [`  bq show  `](/bigquery/docs/reference/bq-cli-reference#bq_show) command.
  - Calling the [`  tables.get  `](/bigquery/docs/reference/rest/v2/tables/get) API method.
  - Using the client libraries.
  - Querying the [`  INFORMATION_SCHEMA.VIEWS  `](/bigquery/docs/information-schema-views) view.

### Required permissions

At a minimum, to get information about tables, you must be granted `  bigquery.tables.get  ` permissions. The following predefined IAM roles include `  bigquery.tables.get  ` permissions:

  - `  bigquery.metadataViewer  `
  - `  bigquery.dataViewer  `
  - `  bigquery.dataOwner  `
  - `  bigquery.dataEditor  `
  - `  bigquery.admin  `

In addition, if a user has `  bigquery.datasets.create  ` permissions, when that user creates a dataset, they are granted `  bigquery.dataOwner  ` access to it. `  bigquery.dataOwner  ` access gives the user the ability to retrieve table metadata.

For more information on IAM roles and permissions in BigQuery, see [Access control](/bigquery/access-control) .

### Get table information

To get information about tables:

### Console

1.  In the navigation panel, in the **Resources** section, expand your project, and then select a dataset.

2.  Click the dataset name to expand it. The tables and views in the dataset appear.

3.  Click the table name.

4.  In the **Details** panel, click **Details** to display the table's description and table information.

5.  Optionally, switch to the **Schema** tab to view the table's schema definition.

### bq

1.  In the Google Cloud console, activate Cloud Shell.
    
    At the bottom of the Google Cloud console, a [Cloud Shell](/shell/docs/how-cloud-shell-works) session starts and displays a command-line prompt. Cloud Shell is a shell environment with the Google Cloud CLI already installed and with values already set for your current project. It can take a few seconds for the session to initialize.

2.  Issue the [`  bq show  `](/bigquery/docs/reference/bq-cli-reference#bq_show) command to display all table information. Use the `  --schema  ` flag to display only table schema information. The `  --format  ` flag can be used to control the output.
    
    If you are getting information about a table in a project other than your default project, add the project ID to the dataset in the following format: `  project_id:dataset  ` .
    
    ``` text
    bq show \
    --schema \
    --format=prettyjson \
    project_id:dataset.table
    ```
    
    Where:
    
      - project\_id is your project ID.
      - dataset is the name of the dataset.
      - table is the name of the table.
    
    Examples:
    
    Enter the following command to display all information about `  mytable  ` in `  mydataset  ` . `  mydataset  ` is in your default project.
    
    ``` text
    bq show --format=prettyjson mydataset.mytable
    ```
    
    Enter the following command to display all information about `  mytable  ` in `  mydataset  ` . `  mydataset  ` is in `  myotherproject  ` , not your default project.
    
    ``` text
    bq show --format=prettyjson myotherproject:mydataset.mytable
    ```
    
    Enter the following command to display only schema information about `  mytable  ` in `  mydataset  ` . `  mydataset  ` is in `  myotherproject  ` , not your default project.
    
    ``` text
    bq show --schema --format=prettyjson myotherproject:mydataset.mytable
    ```

### API

Call the [`  tables.get  `](/bigquery/docs/reference/rest/v2/tables/get) method and provide any relevant parameters.

### Go

Before trying this sample, follow the Go setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Go API reference documentation](https://godoc.org/cloud.google.com/go/bigquery) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` go
import (
 "context"
 "fmt"
 "io"

 "cloud.google.com/go/bigquery"
)

// printTableInfo demonstrates fetching metadata from a table and printing some basic information
// to an io.Writer.
func printTableInfo(w io.Writer, projectID, datasetID, tableID string) error {
 // projectID := "my-project-id"
 // datasetID := "mydataset"
 // tableID := "mytable"
 ctx := context.Background()
 client, err := bigquery.NewClient(ctx, projectID)
 if err != nil {
     return fmt.Errorf("bigquery.NewClient: %v", err)
 }
 defer client.Close()

 meta, err := client.Dataset(datasetID).Table(tableID).Metadata(ctx)
 if err != nil {
     return err
 }
 // Print basic information about the table.
 fmt.Fprintf(w, "Schema has %d top-level fields\n", len(meta.Schema))
 fmt.Fprintf(w, "Description: %s\n", meta.Description)
 fmt.Fprintf(w, "Rows in managed storage: %d\n", meta.NumRows)
 return nil
}
```

### Java

Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Java API reference documentation](/java/docs/reference/google-cloud-bigquery/latest/overview) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` java
import com.google.cloud.bigquery.BigQuery;
import com.google.cloud.bigquery.BigQueryException;
import com.google.cloud.bigquery.BigQueryOptions;
import com.google.cloud.bigquery.Table;
import com.google.cloud.bigquery.TableId;

public class GetTable {

  public static void runGetTable() {
    // TODO(developer): Replace these variables before running the sample.
    String projectId = "bigquery_public_data";
    String datasetName = "samples";
    String tableName = "shakespeare";
    getTable(projectId, datasetName, tableName);
  }

  public static void getTable(String projectId, String datasetName, String tableName) {
    try {
      // Initialize client that will be used to send requests. This client only needs to be created
      // once, and can be reused for multiple requests.
      BigQuery bigquery = BigQueryOptions.getDefaultInstance().getService();

      TableId tableId = TableId.of(projectId, datasetName, tableName);
      Table table = bigquery.getTable(tableId);
      System.out.println("Table info: " + table.getDescription());
    } catch (BigQueryException e) {
      System.out.println("Table not retrieved. \n" + e.toString());
    }
  }
}
```

### Node.js

Before trying this sample, follow the Node.js setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Node.js API reference documentation](https://googleapis.dev/nodejs/bigquery/latest/index.html) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` javascript
// Import the Google Cloud client library
const {BigQuery} = require('@google-cloud/bigquery');
const bigquery = new BigQuery();

async function getTable() {
  // Retrieves table named "my_table" in "my_dataset".

  /**
   * TODO(developer): Uncomment the following lines before running the sample
   */
  // const datasetId = "my_dataset";
  // const tableId = "my_table";

  // Retrieve table reference
  const dataset = bigquery.dataset(datasetId);
  const [table] = await dataset.table(tableId).get();

  console.log('Table:');
  console.log(table.metadata.tableReference);
}
getTable();
```

### PHP

Before trying this sample, follow the PHP setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery PHP API reference documentation](/php/docs/reference/cloud-bigquery/latest/BigQueryClient) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` php
use Google\Cloud\BigQuery\BigQueryClient;

/** Uncomment and populate these variables in your code */
//$projectId = 'The Google project ID';
//$datasetId = 'The BigQuery dataset ID';
//$tableId   = 'The BigQuery table ID';

$bigQuery = new BigQueryClient([
    'projectId' => $projectId,
]);
$dataset = $bigQuery->dataset($datasetId);
$table = $dataset->table($tableId);
```

### Python

Before trying this sample, follow the Python setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Python API reference documentation](/python/docs/reference/bigquery/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` python
from google.cloud import bigquery

# Construct a BigQuery client object.
client = bigquery.Client()

# TODO(developer): Set table_id to the ID of the model to fetch.
# table_id = 'your-project.your_dataset.your_table'

table = client.get_table(table_id)  # Make an API request.

# View table properties
print(
    "Got table '{}.{}.{}'.".format(table.project, table.dataset_id, table.table_id)
)
print("Table schema: {}".format(table.schema))
print("Table description: {}".format(table.description))
print("Table has {} rows".format(table.num_rows))
```

### Get table information using `     INFORMATION_SCHEMA    `

`  INFORMATION_SCHEMA  ` is a series of views that provide access to metadata about datasets, routines, tables, views, jobs, reservations, and streaming data.

You can query the following views to get table information:

  - Use the `  INFORMATION_SCHEMA.TABLES  ` and `  INFORMATION_SCHEMA.TABLE_OPTIONS  ` views to retrieve metadata about tables and views in a project.
  - Use the `  INFORMATION_SCHEMA.COLUMNS  ` and `  INFORMATION_SCHEMA.COLUMN_FIELD_PATHS  ` views to retrieve metadata about the columns (fields) in a table.
  - Use the `  INFORMATION_SCHEMA.TABLE_STORAGE  ` views to retrieve metadata about current and historical storage usage by a table.

The `  TABLES  ` and `  TABLE_OPTIONS  ` views also contain high-level information about views. For detailed information, query the [`  INFORMATION_SCHEMA.VIEWS  `](/bigquery/docs/information-schema-views) view instead.

#### `     TABLES    ` view

When you query the `  INFORMATION_SCHEMA.TABLES  ` view, the query results contain one row for each table or view in a dataset. For detailed information about views, query the [`  INFORMATION_SCHEMA.VIEWS  ` view](/bigquery/docs/information-schema-views) instead.

The `  INFORMATION_SCHEMA.TABLES  ` view has the following schema:

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 10%" />
<col style="width: 65%" />
</colgroup>
<thead>
<tr class="header">
<th>Column name</th>
<th>Data type</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       table_catalog      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The project ID of the project that contains the dataset.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       table_schema      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the dataset that contains the table or view. Also referred to as the <code dir="ltr" translate="no">       datasetId      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       table_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the table or view. Also referred to as the <code dir="ltr" translate="no">       tableId      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       table_type      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The table type; one of the following:<br />

<ul>
<li><code dir="ltr" translate="no">         BASE TABLE        </code> : A standard <a href="/bigquery/docs/tables-intro">table</a></li>
<li><code dir="ltr" translate="no">         CLONE        </code> : A <a href="/bigquery/docs/table-clones-intro">table clone</a></li>
<li><code dir="ltr" translate="no">         SNAPSHOT        </code> : A <a href="/bigquery/docs/table-snapshots-intro">table snapshot</a></li>
<li><code dir="ltr" translate="no">         VIEW        </code> : A <a href="/bigquery/docs/views-intro">view</a></li>
<li><code dir="ltr" translate="no">         MATERIALIZED VIEW        </code> : A <a href="/bigquery/docs/materialized-views-intro">materialized view</a> or <a href="/bigquery/docs/load-data-using-cross-cloud-transfer#materialized_view_replicas">materialized view replica</a></li>
<li><code dir="ltr" translate="no">         EXTERNAL        </code> : A table that references an <a href="/bigquery/external-data-sources">external data source</a></li>
</ul></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       managed_table_type      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>This column is in Preview. The managed table type; one of the following:<br />

<ul>
<li><code dir="ltr" translate="no">         NATIVE        </code> : A standard <a href="/bigquery/docs/tables-intro">table</a></li>
<li><code dir="ltr" translate="no">         BIGLAKE        </code> : A <a href="/bigquery/docs/iceberg-tables">BigLake table for Apache Iceberg in BigQuery</a></li>
</ul></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       is_insertable_into      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><code dir="ltr" translate="no">       YES      </code> or <code dir="ltr" translate="no">       NO      </code> depending on whether the table supports <a href="/bigquery/docs/reference/standard-sql/dml-syntax#insert_statement">DML INSERT</a> statements</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       is_fine_grained_mutations_enabled      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><code dir="ltr" translate="no">       YES      </code> or <code dir="ltr" translate="no">       NO      </code> depending on whether <a href="/bigquery/docs/data-manipulation-language#enable_fine-grained_dml">fine-grained DML mutations</a> are enabled on the table</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       is_typed      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The value is always <code dir="ltr" translate="no">       NO      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       is_change_history_enabled      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><code dir="ltr" translate="no">       YES      </code> or <code dir="ltr" translate="no">       NO      </code> depending on whether <a href="/bigquery/docs/change-history">change history</a> is enabled</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       creation_time      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>The table's creation time</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       base_table_catalog      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>For <a href="/bigquery/docs/table-clones-intro">table clones</a> and <a href="/bigquery/docs/table-snapshots-intro">table snapshots</a> , the base table's project. Applicable only to tables with <code dir="ltr" translate="no">       table_type      </code> set to <code dir="ltr" translate="no">       CLONE      </code> or <code dir="ltr" translate="no">       SNAPSHOT      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       base_table_schema      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>For <a href="/bigquery/docs/table-clones-intro">table clones</a> and <a href="/bigquery/docs/table-snapshots-intro">table snapshots</a> , the base table's dataset. Applicable only to tables with <code dir="ltr" translate="no">       table_type      </code> set to <code dir="ltr" translate="no">       CLONE      </code> or <code dir="ltr" translate="no">       SNAPSHOT      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       base_table_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>For <a href="/bigquery/docs/table-clones-intro">table clones</a> and <a href="/bigquery/docs/table-snapshots-intro">table snapshots</a> , the base table's name. Applicable only to tables with <code dir="ltr" translate="no">       table_type      </code> set to <code dir="ltr" translate="no">       CLONE      </code> or <code dir="ltr" translate="no">       SNAPSHOT      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       snapshot_time_ms      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>For <a href="/bigquery/docs/table-clones-intro">table clones</a> and <a href="/bigquery/docs/table-snapshots-intro">table snapshots</a> , the time when the <a href="/bigquery/docs/table-clones-create">clone</a> or <a href="/bigquery/docs/table-snapshots-create">snapshot</a> operation was run on the base table to create this table. If <a href="/bigquery/docs/time-travel">time travel</a> was used, then this field contains the time travel timestamp. Otherwise, the <code dir="ltr" translate="no">       snapshot_time_ms      </code> field is the same as the <code dir="ltr" translate="no">       creation_time      </code> field. Applicable only to tables with <code dir="ltr" translate="no">       table_type      </code> set to <code dir="ltr" translate="no">       CLONE      </code> or <code dir="ltr" translate="no">       SNAPSHOT      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       replica_source_catalog      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>For <a href="/bigquery/docs/load-data-using-cross-cloud-transfer#materialized_view_replicas">materialized view replicas</a> , the base materialized view's project.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       replica_source_schema      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>For <a href="/bigquery/docs/load-data-using-cross-cloud-transfer#materialized_view_replicas">materialized view replicas</a> , the base materialized view's dataset.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       replica_source_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>For <a href="/bigquery/docs/load-data-using-cross-cloud-transfer#materialized_view_replicas">materialized view replicas</a> , the base materialized view's name.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       replication_status      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>For <a href="/bigquery/docs/load-data-using-cross-cloud-transfer#materialized_view_replicas">materialized view replicas</a> , the status of the replication from the base materialized view to the materialized view replica; one of the following:<br />

<ul>
<li><code dir="ltr" translate="no">         REPLICATION_STATUS_UNSPECIFIED        </code></li>
<li><code dir="ltr" translate="no">         ACTIVE        </code> : Replication is active with no errors</li>
<li><code dir="ltr" translate="no">         SOURCE_DELETED        </code> : The source materialized view has been deleted</li>
<li><code dir="ltr" translate="no">         PERMISSION_DENIED        </code> : The source materialized view hasn't been <a href="/bigquery/docs/authorized-views">authorized</a> on the dataset that contains the source Amazon S3 BigLake tables used in the query that created the materialized view.</li>
<li><code dir="ltr" translate="no">         UNSUPPORTED_CONFIGURATION        </code> : There is an issue with the replica's <a href="/bigquery/docs/load-data-using-cross-cloud-transfer#create">prerequisites</a> other than source materialized view authorization.</li>
</ul></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       replication_error      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>If <code dir="ltr" translate="no">       replication_status      </code> indicates a replication issue for a <a href="/bigquery/docs/load-data-using-cross-cloud-transfer#materialized_view_replicas">materialized view replica</a> , <code dir="ltr" translate="no">       replication_error      </code> provides further details about the issue.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ddl      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The <a href="/bigquery/docs/reference/standard-sql/data-definition-language">DDL statement</a> that can be used to recreate the table, such as <code dir="ltr" translate="no">         CREATE TABLE       </code> or <code dir="ltr" translate="no">         CREATE VIEW       </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       default_collation_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the default <a href="/bigquery/docs/reference/standard-sql/collation-concepts">collation specification</a> if it exists; otherwise, <code dir="ltr" translate="no">       NULL      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       sync_status      </code></td>
<td><code dir="ltr" translate="no">       JSON      </code></td>
<td>The status of the sync between the primary and secondary replicas for <a href="/bigquery/docs/data-replication">cross-region replication</a> and <a href="/bigquery/docs/managed-disaster-recovery">disaster recovery</a> datasets. Returns <code dir="ltr" translate="no">       NULL      </code> if the replica is a primary replica or the dataset doesn't use replication.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       upsert_stream_apply_watermark      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>For tables that use change data capture (CDC), the time when row modifications were last applied. For more information, see <a href="/bigquery/docs/change-data-capture#monitor_table_upsert_operation_progress">Monitor table upsert operation progress</a> .</td>
</tr>
</tbody>
</table>

#### Examples

##### Example 1:

The following example retrieves table metadata for all of the tables in the dataset named `  mydataset  ` . The metadata that's returned is for all types of tables in `  mydataset  ` in your default project.

`  mydataset  ` contains the following tables:

  - `  mytable1  ` : a standard BigQuery table
  - `  myview1  ` : a BigQuery view

To run the query against a project other than your default project, add the project ID to the dataset in the following format: ``  ` project_id `. dataset .INFORMATION_SCHEMA. view  `` ; for example, ``  `myproject`.mydataset.INFORMATION_SCHEMA.TABLES  `` .

**Note:** `  INFORMATION_SCHEMA  ` view names are case-sensitive.

``` text
SELECT
  table_catalog, table_schema, table_name, table_type,
  is_insertable_into, creation_time, ddl
FROM
  mydataset.INFORMATION_SCHEMA.TABLES;
```

The result is similar to the following. For readability, some columns are excluded from the result.

``` text
+----------------+---------------+----------------+------------+--------------------+---------------------+---------------------------------------------+
| table_catalog  | table_schema  |   table_name   | table_type | is_insertable_into |    creation_time    |                     ddl                     |
+----------------+---------------+----------------+------------+--------------------+---------------------+---------------------------------------------+
| myproject      | mydataset     | mytable1       | BASE TABLE | YES                | 2018-10-29 20:34:44 | CREATE TABLE `myproject.mydataset.mytable1` |
|                |               |                |            |                    |                     | (                                           |
|                |               |                |            |                    |                     |   id INT64                                  |
|                |               |                |            |                    |                     | );                                          |
| myproject      | mydataset     | myview1        | VIEW       | NO                 | 2018-12-29 00:19:20 | CREATE VIEW `myproject.mydataset.myview1`   |
|                |               |                |            |                    |                     | AS SELECT 100 as id;                        |
+----------------+---------------+----------------+------------+--------------------+---------------------+---------------------------------------------+
```

##### Example 2:

The following example retrieves table metadata for all tables of type `  CLONE  ` or `  SNAPSHOT  ` from the `  INFORMATION_SCHEMA.TABLES  ` view. The metadata returned is for tables in `  mydataset  ` in your default project.

To run the query against a project other than your default project, add the project ID to the dataset in the following format: ``  ` project_id `. dataset .INFORMATION_SCHEMA. view  `` ; for example, ``  `myproject`.mydataset.INFORMATION_SCHEMA.TABLES  `` .

``` text
  SELECT
    table_name, table_type, base_table_catalog,
    base_table_schema, base_table_name, snapshot_time_ms
  FROM
    mydataset.INFORMATION_SCHEMA.TABLES
  WHERE
    table_type = 'CLONE'
  OR
    table_type = 'SNAPSHOT';
```

The result is similar to the following. For readability, some columns are excluded from the result.

``` text
  +--------------+------------+--------------------+-------------------+-----------------+---------------------+
  | table_name   | table_type | base_table_catalog | base_table_schema | base_table_name | snapshot_time_ms    |
  +--------------+------------+--------------------+-------------------+-----------------+---------------------+
  | items_clone  | CLONE      | myproject          | mydataset         | items           | 2018-10-31 22:40:05 |
  | orders_bk    | SNAPSHOT   | myproject          | mydataset         | orders          | 2018-11-01 08:22:39 |
  +--------------+------------+--------------------+-------------------+-----------------+---------------------+
```

##### Example 3:

The following example retrieves `  table_name  ` and `  ddl  ` columns from the `  INFORMATION_SCHEMA.TABLES  ` view for the `  population_by_zip_2010  ` table in the [`  census_bureau_usa  `](https://console.cloud.google.com/bigquery?p=bigquery-public-data&d=census_bureau_usa&page=dataset) dataset. This dataset is part of the BigQuery [public dataset program](/bigquery/public-data) .

Because the table you're querying is in another project, you add the project ID to the dataset in the following format: ``  ` project_id `. dataset .INFORMATION_SCHEMA. view  `` . In this example, the value is ``  `bigquery-public-data`.census_bureau_usa.INFORMATION_SCHEMA.TABLES  `` .

``` text
SELECT
  table_name, ddl
FROM
  `bigquery-public-data`.census_bureau_usa.INFORMATION_SCHEMA.TABLES
WHERE
  table_name = 'population_by_zip_2010';
```

The result is similar to the following:

``` text
+------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
|       table_name       |                                                                                                            ddl                                                                                                             |
+------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| population_by_zip_2010 | CREATE TABLE `bigquery-public-data.census_bureau_usa.population_by_zip_2010`                                                                                                                                               |
|                        | (                                                                                                                                                                                                                          |
|                        |   geo_id STRING OPTIONS(description="Geo code"),                                                                                                                                                                           |
|                        |   zipcode STRING NOT NULL OPTIONS(description="Five digit ZIP Code Tabulation Area Census Code"),                                                                                                                          |
|                        |   population INT64 OPTIONS(description="The total count of the population for this segment."),                                                                                                                             |
|                        |   minimum_age INT64 OPTIONS(description="The minimum age in the age range. If null, this indicates the row as a total for male, female, or overall population."),                                                          |
|                        |   maximum_age INT64 OPTIONS(description="The maximum age in the age range. If null, this indicates the row as having no maximum (such as 85 and over) or the row is a total of the male, female, or overall population."), |
|                        |   gender STRING OPTIONS(description="male or female. If empty, the row is a total population summary.")                                                                                                                    |
|                        | )                                                                                                                                                                                                                          |
|                        | OPTIONS(                                                                                                                                                                                                                   |
|                        |   labels=[("freebqcovid", "")]                                                                                                                                                                                             |
|                        | );                                                                                                                                                                                                                         |
+------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
  
```

#### `     TABLE_OPTIONS    ` view

When you query the `  INFORMATION_SCHEMA.TABLE_OPTIONS  ` view, the query results contain one row for each option, for each table or view in a dataset. For detailed information about views, query the [`  INFORMATION_SCHEMA.VIEWS  ` view](/bigquery/docs/information-schema-views) instead.

The `  INFORMATION_SCHEMA.TABLE_OPTIONS  ` view has the following schema:

<table>
<thead>
<tr class="header">
<th>Column name</th>
<th>Data type</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       table_catalog      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The project ID of the project that contains the dataset</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       table_schema      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the dataset that contains the table or view also referred to as the <code dir="ltr" translate="no">       datasetId      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       table_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the table or view also referred to as the <code dir="ltr" translate="no">       tableId      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       option_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>One of the name values in the <a href="#options_table">options table</a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       option_type      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>One of the data type values in the <a href="#options_table">options table</a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       option_value      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>One of the value options in the <a href="#options_table">options table</a></td>
</tr>
</tbody>
</table>

##### Options table

<table>
<thead>
<tr class="header">
<th><p><code dir="ltr" translate="no">        OPTION_NAME       </code></p></th>
<th><p><code dir="ltr" translate="no">        OPTION_TYPE       </code></p></th>
<th><p><code dir="ltr" translate="no">        OPTION_VALUE       </code></p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        description       </code></p></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td>A description of the table</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        enable_refresh       </code></p></td>
<td><p><code dir="ltr" translate="no">        BOOL       </code></p></td>
<td>Whether automatic refresh is enabled for a materialized view</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        expiration_timestamp       </code></p></td>
<td><p><code dir="ltr" translate="no">        TIMESTAMP       </code></p></td>
<td>The time when this table expires</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        friendly_name       </code></p></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td>The table's descriptive name</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        kms_key_name       </code></p></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td>The name of the Cloud KMS key used to encrypt the table</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        labels       </code></p></td>
<td><p><code dir="ltr" translate="no">        ARRAY&lt;STRUCT&lt;STRING, STRING&gt;&gt;       </code></p></td>
<td>An array of <code dir="ltr" translate="no">       STRUCT      </code> 's that represent the labels on the table</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        max_staleness       </code></p></td>
<td><p><code dir="ltr" translate="no">        INTERVAL       </code></p></td>
<td>The configured table's maximum staleness for <a href="/bigquery/docs/change-data-capture#manage_table_staleness">BigQuery change data capture (CDC) upserts</a></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        partition_expiration_days       </code></p></td>
<td><p><code dir="ltr" translate="no">        FLOAT64       </code></p></td>
<td>The default lifetime, in days, of all partitions in a partitioned table</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        refresh_interval_minutes       </code></p></td>
<td><p><code dir="ltr" translate="no">        FLOAT64       </code></p></td>
<td>How frequently a materialized view is refreshed</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        require_partition_filter       </code></p></td>
<td><p><code dir="ltr" translate="no">        BOOL       </code></p></td>
<td>Whether queries over the table require a partition filter</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        tags       </code></p></td>
<td><p><code dir="ltr" translate="no">        ARRAY&lt;STRUCT&lt;STRING, STRING&gt;&gt;       </code></p></td>
<td>Tags attached to a table in a namespaced &lt;key, value&gt; syntax. For more information, see <a href="/iam/docs/tags-access-control">Tags and conditional access</a> .</td>
</tr>
</tbody>
</table>

For external tables, the following options are possible:

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

`  column_name_character_map  `

`  STRING  `

Defines the scope of supported column name characters and the handling behavior of unsupported characters. The default setting is `  STRICT  ` , which means unsupported characters cause BigQuery to throw errors. `  V1  ` and `  V2  ` replace any unsupported characters with underscores.

Supported values include:

  - `  STRICT  ` . Enables [flexible column names](/bigquery/docs/schemas#flexible-column-names) . This is the default value. Load jobs with unsupported characters in column names fail with an error message. To configure the replacement of unsupported characters with underscores so that the load job succeeds, specify the [`  default_column_name_character_map  `](/bigquery/docs/default-configuration) configuration setting.
  - `  V1  ` . Column names can only contain [standard column name characters](/bigquery/docs/schemas#column_names) . Unsupported characters (except [periods in Parquet file column names](/bigquery/docs/loading-data-cloud-storage-parquet#limitations_2) ) are replaced with underscores. This is the default behavior for tables created before the introduction of `  column_name_character_map  ` .
  - `  V2  ` . Besides [standard column name characters](/bigquery/docs/schemas#column_names) , it also supports [flexible column names](/bigquery/docs/schemas#flexible-column-names) . Unsupported characters (except [periods in Parquet file column names](/bigquery/docs/loading-data-cloud-storage-parquet#limitations_2) ) are replaced with underscores.

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

#### Examples

##### Example 1:

The following example retrieves the default table expiration times for all tables in `  mydataset  ` in your default project ( `  myproject  ` ) by querying the `  INFORMATION_SCHEMA.TABLE_OPTIONS  ` view.

To run the query against a project other than your default project, add the project ID to the dataset in the following format: ``  ` project_id `. dataset .INFORMATION_SCHEMA. view  `` ; for example, ``  `myproject`.mydataset.INFORMATION_SCHEMA.TABLE_OPTIONS  `` .

**Note:** `  INFORMATION_SCHEMA  ` view names are case-sensitive.

``` text
  SELECT
    *
  FROM
    mydataset.INFORMATION_SCHEMA.TABLE_OPTIONS
  WHERE
    option_name = 'expiration_timestamp';
```

The result is similar to the following:

``` text
  +----------------+---------------+------------+----------------------+-------------+--------------------------------------+
  | table_catalog  | table_schema  | table_name |     option_name      | option_type |             option_value             |
  +----------------+---------------+------------+----------------------+-------------+--------------------------------------+
  | myproject      | mydataset     | mytable1   | expiration_timestamp | TIMESTAMP   | TIMESTAMP "2020-01-16T21:12:28.000Z" |
  | myproject      | mydataset     | mytable2   | expiration_timestamp | TIMESTAMP   | TIMESTAMP "2021-01-01T21:12:28.000Z" |
  +----------------+---------------+------------+----------------------+-------------+--------------------------------------+
  
```

**Note:** Tables without an expiration time are excluded from the query results.

##### Example 2:

The following example retrieves metadata about all tables in `  mydataset  ` that contain test data. The query uses the values in the `  description  ` option to find tables that contain "test" anywhere in the description. `  mydataset  ` is in your default project — `  myproject  ` .

To run the query against a project other than your default project, add the project ID to the dataset in the following format: ``  ` project_id `. dataset .INFORMATION_SCHEMA. view  `` ; for example, ``  `myproject`.mydataset.INFORMATION_SCHEMA.TABLE_OPTIONS  `` .

``` text
  SELECT
    *
  FROM
    mydataset.INFORMATION_SCHEMA.TABLE_OPTIONS
  WHERE
    option_name = 'description'
    AND option_value LIKE '%test%';
```

The result is similar to the following:

``` text
  +----------------+---------------+------------+-------------+-------------+--------------+
  | table_catalog  | table_schema  | table_name | option_name | option_type | option_value |
  +----------------+---------------+------------+-------------+-------------+--------------+
  | myproject      | mydataset     | mytable1   | description | STRING      | "test data"  |
  | myproject      | mydataset     | mytable2   | description | STRING      | "test data"  |
  +----------------+---------------+------------+-------------+-------------+--------------+
  
```

#### `     COLUMNS    ` view

When you query the `  INFORMATION_SCHEMA.COLUMNS  ` view, the query results contain one row for each column (field) in a table.

The `  INFORMATION_SCHEMA.COLUMNS  ` view has the following schema:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Column name</th>
<th>Data type</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       table_catalog      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The project ID of the project that contains the dataset.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       table_schema      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the dataset that contains the table also referred to as the <code dir="ltr" translate="no">       datasetId      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       table_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the table or view also referred to as the <code dir="ltr" translate="no">       tableId      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       column_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the column.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       ordinal_position      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td>The 1-indexed offset of the column within the table; if it's a pseudo column such as _PARTITIONTIME or _PARTITIONDATE, the value is <code dir="ltr" translate="no">       NULL      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       is_nullable      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><code dir="ltr" translate="no">       YES      </code> or <code dir="ltr" translate="no">       NO      </code> depending on whether the column's mode allows <code dir="ltr" translate="no">       NULL      </code> values.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       data_type      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The column's GoogleSQL <a href="/bigquery/docs/reference/standard-sql/data-types">data type</a> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       is_generated      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The value is <code dir="ltr" translate="no">       ALWAYS      </code> if the column is an <a href="/bigquery/docs/autonomous-embedding-generation">automatically generated embedding column</a> ; otherwise, the value is <code dir="ltr" translate="no">       NEVER      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       generation_expression      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The value is the generation expression used to define the column if the column is an automatically generated embedding column; otherwise the value is <code dir="ltr" translate="no">       NULL      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       is_stored      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The value is <code dir="ltr" translate="no">       YES      </code> if the column is an automatically generated embedding column; otherwise, the value is <code dir="ltr" translate="no">       NULL      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       is_hidden      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><code dir="ltr" translate="no">       YES      </code> or <code dir="ltr" translate="no">       NO      </code> depending on whether the column is a pseudo column such as _PARTITIONTIME or _PARTITIONDATE.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       is_updatable      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The value is always <code dir="ltr" translate="no">       NULL      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       is_system_defined      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><code dir="ltr" translate="no">       YES      </code> or <code dir="ltr" translate="no">       NO      </code> depending on whether the column is a pseudo column such as _PARTITIONTIME or _PARTITIONDATE.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       is_partitioning_column      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><code dir="ltr" translate="no">       YES      </code> or <code dir="ltr" translate="no">       NO      </code> depending on whether the column is a <a href="/bigquery/docs/partitioned-tables">partitioning column</a> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       clustering_ordinal_position      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td>The 1-indexed offset of the column within the table's clustering columns; the value is <code dir="ltr" translate="no">       NULL      </code> if the table is not a clustered table.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       collation_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the <a href="/bigquery/docs/reference/standard-sql/collation-concepts">collation specification</a> if it exists; otherwise, <code dir="ltr" translate="no">       NULL      </code> .<br />
<br />
If a <code dir="ltr" translate="no">       STRING      </code> or <code dir="ltr" translate="no">       ARRAY&lt;STRING&gt;      </code> is passed in, the collation specification is returned if it exists; otherwise <code dir="ltr" translate="no">       NULL      </code> is returned.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       column_default      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The <a href="/bigquery/docs/default-values">default value</a> of the column if it exists; otherwise, the value is <code dir="ltr" translate="no">       NULL      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       rounding_mode      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The mode of rounding that's used for values written to the field if its type is a parameterized <code dir="ltr" translate="no">       NUMERIC      </code> or <code dir="ltr" translate="no">       BIGNUMERIC      </code> ; otherwise, the value is <code dir="ltr" translate="no">       NULL      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       data_policies.name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The list of data policies that are attached to the column to control access and masking. This field is in ( <a href="https://cloud.google.com/products#product-launch-stages">Preview</a> ).</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       policy_tags      </code></td>
<td><code dir="ltr" translate="no">       ARRAY&lt;STRING&gt;      </code></td>
<td>The list of policy tags that are attached to the column.</td>
</tr>
</tbody>
</table>

#### Examples

The following example retrieves metadata from the `  INFORMATION_SCHEMA.COLUMNS  ` view for the `  population_by_zip_2010  ` table in the [`  census_bureau_usa  `](https://console.cloud.google.com/bigquery?p=bigquery-public-data&d=census_bureau_usa&page=dataset) dataset. This dataset is part of the BigQuery [public dataset program](https://cloud.google.com/public-datasets/) .

Because the table you're querying is in another project, the `  bigquery-public-data  ` project, you add the project ID to the dataset in the following format: ``  ` project_id `. dataset .INFORMATION_SCHEMA. view  `` ; for example, ``  `bigquery-public-data`.census_bureau_usa.INFORMATION_SCHEMA.TABLES  `` .

The following column is excluded from the query results:

  - `  IS_UPDATABLE  `

**Note:** `  INFORMATION_SCHEMA  ` view names are case-sensitive.

``` text
  SELECT
    * EXCEPT(is_updatable)
  FROM
    `bigquery-public-data`.census_bureau_usa.INFORMATION_SCHEMA.COLUMNS
  WHERE
    table_name = 'population_by_zip_2010';
```

The result is similar to the following. For readability, some columns are excluded from the result.

``` text
+------------------------+-------------+------------------+-------------+-----------+-----------+-------------------+------------------------+-----------------------------+-------------+
|       table_name       | column_name | ordinal_position | is_nullable | data_type | is_hidden | is_system_defined | is_partitioning_column | clustering_ordinal_position | policy_tags |
+------------------------+-------------+------------------+-------------+-----------+-----------+-------------------+------------------------+-----------------------------+-------------+
| population_by_zip_2010 | zipcode     |                1 | NO          | STRING    | NO        | NO                | NO                     |                        NULL | 0 rows      |
| population_by_zip_2010 | geo_id      |                2 | YES         | STRING    | NO        | NO                | NO                     |                        NULL | 0 rows      |
| population_by_zip_2010 | minimum_age |                3 | YES         | INT64     | NO        | NO                | NO                     |                        NULL | 0 rows      |
| population_by_zip_2010 | maximum_age |                4 | YES         | INT64     | NO        | NO                | NO                     |                        NULL | 0 rows      |
| population_by_zip_2010 | gender      |                5 | YES         | STRING    | NO        | NO                | NO                     |                        NULL | 0 rows      |
| population_by_zip_2010 | population  |                6 | YES         | INT64     | NO        | NO                | NO                     |                        NULL | 0 rows      |
+------------------------+-------------+------------------+-------------+-----------+-----------+-------------------+------------------------+-----------------------------+-------------+
  
```

#### `     COLUMN_FIELD_PATHS    ` view

When you query the `  INFORMATION_SCHEMA.COLUMN_FIELD_PATHS  ` view, the query results contain one row for each column [nested](/bigquery/docs/nested-repeated) within a `  RECORD  ` (or `  STRUCT  ` ) column.

The `  INFORMATION_SCHEMA.COLUMN_FIELD_PATHS  ` view has the following schema:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Column name</th>
<th>Data type</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       table_catalog      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The project ID of the project that contains the dataset.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       table_schema      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the dataset that contains the table also referred to as the <code dir="ltr" translate="no">       datasetId      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       table_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the table or view also referred to as the <code dir="ltr" translate="no">       tableId      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       column_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the column.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       field_path      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The path to a column <a href="/bigquery/docs/nested-repeated">nested</a> within a `RECORD` or `STRUCT` column.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       data_type      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The column's GoogleSQL <a href="/bigquery/docs/reference/standard-sql/data-types">data type</a> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       description      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The column's description.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       collation_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the <a href="/bigquery/docs/reference/standard-sql/collation-concepts">collation specification</a> if it exists; otherwise, <code dir="ltr" translate="no">       NULL      </code> .<br />
<br />
If a <code dir="ltr" translate="no">       STRING      </code> , <code dir="ltr" translate="no">       ARRAY&lt;STRING&gt;      </code> , or <code dir="ltr" translate="no">       STRING      </code> field in a <code dir="ltr" translate="no">       STRUCT      </code> is passed in, the collation specification is returned if it exists; otherwise, <code dir="ltr" translate="no">       NULL      </code> is returned.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       rounding_mode      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The mode of rounding that's used when applying precision and scale to+ parameterized <code dir="ltr" translate="no">       NUMERIC      </code> or <code dir="ltr" translate="no">       BIGNUMERIC      </code> values; otherwise, the value is <code dir="ltr" translate="no">       NULL      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       data_policies.name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The list of data policies that are attached to the column to control access and masking. This field is in ( <a href="https://cloud.google.com/products#product-launch-stages">Preview</a> ).</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       policy_tags      </code></td>
<td><code dir="ltr" translate="no">       ARRAY&lt;STRING&gt;      </code></td>
<td>The list of policy tags that are attached to the column.</td>
</tr>
</tbody>
</table>

#### Examples

The following example retrieves metadata from the `  INFORMATION_SCHEMA.COLUMN_FIELD_PATHS  ` view for the `  commits  ` table in the [`  github_repos  ` dataset](https://console.cloud.google.com/bigquery?p=bigquery-public-data&d=github_repos&page=dataset) . This dataset is part of the BigQuery [public dataset program](https://cloud.google.com/public-datasets/) .

Because the table you're querying is in another project, the `  bigquery-public-data  ` project, you add the project ID to the dataset in the following format: ``  ` project_id `. dataset .INFORMATION_SCHEMA. view  `` ; for example, ``  `bigquery-public-data`.github_repos.INFORMATION_SCHEMA.COLUMN_FIELD_PATHS  `` .

The `  commits  ` table contains the following nested and nested and repeated columns:

  - `  author  ` : nested `  RECORD  ` column
  - `  committer  ` : nested `  RECORD  ` column
  - `  trailer  ` : nested and repeated `  RECORD  ` column
  - `  difference  ` : nested and repeated `  RECORD  ` column

To view metadata about the `  author  ` and `  difference  ` columns, run the following query.

**Note:** `  INFORMATION_SCHEMA  ` view names are case-sensitive.

``` text
SELECT
  *
FROM
  `bigquery-public-data`.github_repos.INFORMATION_SCHEMA.COLUMN_FIELD_PATHS
WHERE
  table_name = 'commits'
  AND (column_name = 'author' OR column_name = 'difference');
```

The result is similar to the following. For readability, some columns are excluded from the result.

``` text
  +------------+-------------+---------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+
  | table_name | column_name |     field_path      |                                                                      data_type                                                                      | description | policy_tags |
  +------------+-------------+---------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+
  | commits    | author      | author              | STRUCT<name STRING, email STRING, time_sec INT64, tz_offset INT64, date TIMESTAMP>                                                                  | NULL        | 0 rows      |
  | commits    | author      | author.name         | STRING                                                                                                                                              | NULL        | 0 rows      |
  | commits    | author      | author.email        | STRING                                                                                                                                              | NULL        | 0 rows      |
  | commits    | author      | author.time_sec     | INT64                                                                                                                                               | NULL        | 0 rows      |
  | commits    | author      | author.tz_offset    | INT64                                                                                                                                               | NULL        | 0 rows      |
  | commits    | author      | author.date         | TIMESTAMP                                                                                                                                           | NULL        | 0 rows      |
  | commits    | difference  | difference          | ARRAY<STRUCT<old_mode INT64, new_mode INT64, old_path STRING, new_path STRING, old_sha1 STRING, new_sha1 STRING, old_repo STRING, new_repo STRING>> | NULL        | 0 rows      |
  | commits    | difference  | difference.old_mode | INT64                                                                                                                                               | NULL        | 0 rows      |
  | commits    | difference  | difference.new_mode | INT64                                                                                                                                               | NULL        | 0 rows      |
  | commits    | difference  | difference.old_path | STRING                                                                                                                                              | NULL        | 0 rows      |
  | commits    | difference  | difference.new_path | STRING                                                                                                                                              | NULL        | 0 rows      |
  | commits    | difference  | difference.old_sha1 | STRING                                                                                                                                              | NULL        | 0 rows      |
  | commits    | difference  | difference.new_sha1 | STRING                                                                                                                                              | NULL        | 0 rows      |
  | commits    | difference  | difference.old_repo | STRING                                                                                                                                              | NULL        | 0 rows      |
  | commits    | difference  | difference.new_repo | STRING                                                                                                                                              | NULL        | 0 rows      |
  +------------+-------------+---------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+
  
```

#### `     TABLE_STORAGE    ` view

The `  TABLE_STORAGE  ` and `  TABLE_STORAGE_BY_ORGANIZATION  ` views have the following schema:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Column name</th>
<th>Data type</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       project_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The project ID of the project that contains the dataset.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       project_number      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td>The project number of the project that contains the dataset.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       table_catalog      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The project ID of the project that contains the dataset.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       table_schema      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the dataset that contains the table or materialized view, also referred to as the <code dir="ltr" translate="no">       datasetId      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       table_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the table or materialized view, also referred to as the <code dir="ltr" translate="no">       tableId      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       creation_time      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>The creation time of the table.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       total_rows      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td>The total number of rows in the table or materialized view.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       total_partitions      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td>The number of partitions present in the table or materialized view. Unpartitioned tables return 0.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       total_logical_bytes      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td>Total number of logical (uncompressed) bytes in the table or materialized view.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       active_logical_bytes      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td>Number of logical (uncompressed) bytes that are younger than 90 days.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       long_term_logical_bytes      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td>Number of logical (uncompressed) bytes that are older than 90 days.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       current_physical_bytes      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td>Total number of physical bytes for the current storage of the table across all partitions.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       total_physical_bytes      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td>Total number of physical (compressed) bytes used for storage, including active, long-term, and time travel (deleted or changed data) bytes. Fail-safe (deleted or changed data retained after the time-travel window) bytes aren't included.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       active_physical_bytes      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td>Number of physical (compressed) bytes younger than 90 days, including time travel (deleted or changed data) bytes.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       long_term_physical_bytes      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td>Number of physical (compressed) bytes older than 90 days.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       time_travel_physical_bytes      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td>Number of physical (compressed) bytes used by time travel storage (deleted or changed data).</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       storage_last_modified_time      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>The most recent time that data was written to the table. Returns <code dir="ltr" translate="no">       NULL      </code> if no data exists.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       deleted      </code></td>
<td><code dir="ltr" translate="no">       BOOLEAN      </code></td>
<td>Indicates whether or not the table is deleted.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       table_type      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The type of table. For example, <code dir="ltr" translate="no">       BASE TABLE      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       managed_table_type      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>This column is in Preview. The managed type of the table. For example, <code dir="ltr" translate="no">       NATIVE      </code> or <code dir="ltr" translate="no">       BIGLAKE      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       fail_safe_physical_bytes      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td>Number of physical (compressed) bytes used by the fail-safe storage (deleted or changed data).</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       last_metadata_index_refresh_time      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>The last metadata index refresh time of the table.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       table_deletion_reason      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Table deletion reason if the <code dir="ltr" translate="no">       deleted      </code> field is true. The possible values are as follows:
<ul>
<li><code dir="ltr" translate="no">         TABLE_EXPIRATION:        </code> table deleted after set expiration time</li>
<li><code dir="ltr" translate="no">         DATASET_DELETION:        </code> dataset deleted by user</li>
<li><code dir="ltr" translate="no">         USER_DELETED:        </code> table was deleted by user</li>
</ul></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       table_deletion_time      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>The deletion time of the table.</td>
</tr>
</tbody>
</table>

#### Examples

##### Example 1:

The following example shows you the total logical bytes billed for the current project.

``` text
SELECT
  SUM(total_logical_bytes) AS total_logical_bytes
FROM
  `region-REGION`.INFORMATION_SCHEMA.TABLE_STORAGE;
```

The result is similar to the following:

``` text
+---------------------+
| total_logical_bytes |
+---------------------+
| 971329178274633     |
+---------------------+
```

##### Example 2:

The following example shows different storage bytes in GiB at the dataset(s) level for current project.

``` text
SELECT
  table_schema AS dataset_name,
  -- Logical
  SUM(total_logical_bytes) / power(1024, 3) AS total_logical_gib,  
  SUM(active_logical_bytes) / power(1024, 3) AS active_logical_gib, 
  SUM(long_term_logical_bytes) / power(1024, 3) AS long_term_logical_gib, 
  -- Physical
  SUM(total_physical_bytes) / power(1024, 3) AS total_physical_gib,
  SUM(active_physical_bytes) / power(1024, 3) AS active_physical_gib,
  SUM(active_physical_bytes - time_travel_physical_bytes) / power(1024, 3) AS active_no_tt_physical_gib,
  SUM(long_term_physical_bytes) / power(1024, 3) AS long_term_physical_gib,
  SUM(time_travel_physical_bytes) / power(1024, 3) AS time_travel_physical_gib,
  SUM(fail_safe_physical_bytes) / power(1024, 3) AS fail_safe_physical_gib 
FROM
  `region-REGION`.INFORMATION_SCHEMA.TABLE_STORAGE 
WHERE 
  table_type ='BASE TABLE'
GROUP BY 
  table_schema  
ORDER BY 
  dataset_name 
```

##### Example 3:

The following example shows you how to forecast the price difference per dataset between logical and physical billing models for the next 30 days. This example assumes that future storage usage is constant over the next 30 days from the moment the query was run. Note that the forecast is limited to base tables, it excludes all other types of tables within a dataset.

The prices used in the pricing variables for this query are for the `  us-central1  ` region. If you want to run this query for a different region, update the pricing variables appropriately. See [Storage pricing](https://cloud.google.com/bigquery/pricing#storage) for pricing information.

1.  Open the BigQuery page in the Google Cloud console.

2.  Enter the following GoogleSQL query in the **Query editor** box. `  INFORMATION_SCHEMA  ` requires GoogleSQL syntax. GoogleSQL is the default syntax in the Google Cloud console.
    
    ``` text
    DECLARE active_logical_gib_price FLOAT64 DEFAULT 0.02;
    DECLARE long_term_logical_gib_price FLOAT64 DEFAULT 0.01;
    DECLARE active_physical_gib_price FLOAT64 DEFAULT 0.04;
    DECLARE long_term_physical_gib_price FLOAT64 DEFAULT 0.02;
    
    WITH
     storage_sizes AS (
       SELECT
         table_schema AS dataset_name,
         -- Logical
         SUM(IF(deleted=false, active_logical_bytes, 0)) / power(1024, 3) AS active_logical_gib,
         SUM(IF(deleted=false, long_term_logical_bytes, 0)) / power(1024, 3) AS long_term_logical_gib,
         -- Physical
         SUM(active_physical_bytes) / power(1024, 3) AS active_physical_gib,
         SUM(active_physical_bytes - time_travel_physical_bytes) / power(1024, 3) AS active_no_tt_physical_gib,
         SUM(long_term_physical_bytes) / power(1024, 3) AS long_term_physical_gib,
         -- Restorable previously deleted physical
         SUM(time_travel_physical_bytes) / power(1024, 3) AS time_travel_physical_gib,
         SUM(fail_safe_physical_bytes) / power(1024, 3) AS fail_safe_physical_gib,
       FROM
         `region-REGION`.INFORMATION_SCHEMA.TABLE_STORAGE_BY_PROJECT
       WHERE total_physical_bytes + fail_safe_physical_bytes > 0
         -- Base the forecast on base tables only for highest precision results
         AND table_type  = 'BASE TABLE'
         GROUP BY 1
     )
    SELECT
      dataset_name,
      -- Logical
      ROUND(active_logical_gib, 2) AS active_logical_gib,
      ROUND(long_term_logical_gib, 2) AS long_term_logical_gib,
      -- Physical
      ROUND(active_physical_gib, 2) AS active_physical_gib,
      ROUND(long_term_physical_gib, 2) AS long_term_physical_gib,
      ROUND(time_travel_physical_gib, 2) AS time_travel_physical_gib,
      ROUND(fail_safe_physical_gib, 2) AS fail_safe_physical_gib,
      -- Compression ratio
      ROUND(SAFE_DIVIDE(active_logical_gib, active_no_tt_physical_gib), 2) AS active_compression_ratio,
      ROUND(SAFE_DIVIDE(long_term_logical_gib, long_term_physical_gib), 2) AS long_term_compression_ratio,
      -- Forecast costs logical
      ROUND(active_logical_gib * active_logical_gib_price, 2) AS forecast_active_logical_cost,
      ROUND(long_term_logical_gib * long_term_logical_gib_price, 2) AS forecast_long_term_logical_cost,
      -- Forecast costs physical
      ROUND((active_no_tt_physical_gib + time_travel_physical_gib + fail_safe_physical_gib) * active_physical_gib_price, 2) AS forecast_active_physical_cost,
      ROUND(long_term_physical_gib * long_term_physical_gib_price, 2) AS forecast_long_term_physical_cost,
      -- Forecast costs total
      ROUND(((active_logical_gib * active_logical_gib_price) + (long_term_logical_gib * long_term_logical_gib_price)) -
         (((active_no_tt_physical_gib + time_travel_physical_gib + fail_safe_physical_gib) * active_physical_gib_price) + (long_term_physical_gib * long_term_physical_gib_price)), 2) AS forecast_total_cost_difference
    FROM
      storage_sizes
    ORDER BY
      (forecast_active_logical_cost + forecast_active_physical_cost) DESC;
    ```
    
    **Note:** `  INFORMATION_SCHEMA  ` view names are case-sensitive.

3.  Click **Run** .

The result is similar to following:

``` text
+--------------+--------------------+-----------------------+---------------------+------------------------+--------------------------+-----------------------------+------------------------------+----------------------------------+-------------------------------+----------------------------------+--------------------------------+
| dataset_name | active_logical_gib | long_term_logical_gib | active_physical_gib | long_term_physical_gib | active_compression_ratio | long_term_compression_ratio | forecast_active_logical_cost | forecaset_long_term_logical_cost | forecast_active_physical_cost | forecast_long_term_physical_cost | forecast_total_cost_difference |
+--------------+--------------------+-----------------------+---------------------+------------------------+--------------------------+-----------------------------+------------------------------+----------------------------------+-------------------------------+----------------------------------+--------------------------------+
| dataset1     |               10.0 |                  10.0 |                 1.0 |                    1.0 |                     10.0 |                        10.0 |                          0.2 |                              0.1 |                          0.04 |                             0.02 |                           0.24 |
```

### List tables in a dataset

You can list tables in datasets in the following ways:

  - Using the Google Cloud console.
  - Using the bq command-line tool [`  bq ls  `](/bigquery/docs/reference/bq-cli-reference#bq_ls) command.
  - Calling the [`  tables.list  `](/bigquery/docs/reference/rest/v2/tables/list) API method.
  - Using the client libraries.

#### Required permissions

At a minimum, to list tables in a dataset, you must be granted `  bigquery.tables.list  ` permissions. The following predefined IAM roles include `  bigquery.tables.list  ` permissions:

  - `  bigquery.user  `
  - `  bigquery.metadataViewer  `
  - `  bigquery.dataViewer  `
  - `  bigquery.dataEditor  `
  - `  bigquery.dataOwner  `
  - `  bigquery.admin  `

For more information on IAM roles and permissions in BigQuery, see [Access control](/bigquery/access-control) .

#### List tables

To list the tables in a dataset:

### Console

1.  In the Google Cloud console, in the navigation pane, click your dataset to expand it. This displays the tables and views in the dataset.

2.  Scroll through the list to see the tables in the dataset. Tables and views are identified by different icons.

### bq

1.  In the Google Cloud console, activate Cloud Shell.
    
    At the bottom of the Google Cloud console, a [Cloud Shell](/shell/docs/how-cloud-shell-works) session starts and displays a command-line prompt. Cloud Shell is a shell environment with the Google Cloud CLI already installed and with values already set for your current project. It can take a few seconds for the session to initialize.

2.  Issue the [`  bq ls  `](/bigquery/docs/reference/bq-cli-reference#bq_ls) command. The `  --format  ` flag can be used to control the output. If you are listing tables in a project other than your default project, add the project ID to the dataset in the following format: `  project_id:dataset  ` .
    
    Additional flags include:
    
      - `  --max_results  ` or `  -n  ` : An integer indicating the maximum number of results. The default value is `  50  ` .
    
    <!-- end list -->
    
    ``` text
    bq ls \
    --format=pretty \
    --max_results integer \
    project_id:dataset
    ```
    
    Where:
    
      - integer is an integer representing the number of tables to list.
      - project\_id is your project ID.
      - dataset is the name of the dataset.
    
    When you run the command, the `  Type  ` field displays either `  TABLE  ` or `  VIEW  ` . For example:
    
    ``` text
    +-------------------------+-------+----------------------+-------------------+
    |         tableId         | Type  |        Labels        | Time Partitioning |
    +-------------------------+-------+----------------------+-------------------+
    | mytable                 | TABLE | department:shipping  |                   |
    | myview                  | VIEW  |                      |                   |
    +-------------------------+-------+----------------------+-------------------+
    ```
    
    Examples:
    
    Enter the following command to list tables in dataset `  mydataset  ` in your default project.
    
    ``` text
       bq ls --format=pretty mydataset
    ```
    
    Enter the following command to return more than the default output of 50 tables from `  mydataset  ` . `  mydataset  ` is in your default project.
    
    ``` text
       bq ls --format=pretty --max_results 60 mydataset
    ```
    
    Enter the following command to list tables in dataset `  mydataset  ` in `  myotherproject  ` .
    
    ``` text
       bq ls --format=pretty myotherproject:mydataset
    ```

### API

To list tables using the API, call the [`  tables.list  `](/bigquery/docs/reference/rest/v2/tables/list) method.

### C\#

Before trying this sample, follow the C\# setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery C\# API reference documentation](/dotnet/docs/reference/Google.Cloud.BigQuery.V2/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` csharp
using Google.Cloud.BigQuery.V2;
using System;
using System.Collections.Generic;
using System.Linq;

public class BigQueryListTables
{
    public void ListTables(
        string projectId = "your-project-id",
        string datasetId = "your_dataset_id"
    )
    {
        BigQueryClient client = BigQueryClient.Create(projectId);
        // Retrieve list of tables in the dataset
        List<BigQueryTable> tables = client.ListTables(datasetId).ToList();
        // Display the results
        if (tables.Count > 0)
        {
            Console.WriteLine($"Tables in dataset {datasetId}:");
            foreach (var table in tables)
            {
                Console.WriteLine($"\t{table.Reference.TableId}");
            }
        }
        else
        {
            Console.WriteLine($"{datasetId} does not contain any tables.");
        }
    }
}
```

### Go

Before trying this sample, follow the Go setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Go API reference documentation](https://godoc.org/cloud.google.com/go/bigquery) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` go
import (
 "context"
 "fmt"
 "io"

 "cloud.google.com/go/bigquery"
 "google.golang.org/api/iterator"
)

// listTables demonstrates iterating through the collection of tables in a given dataset.
func listTables(w io.Writer, projectID, datasetID string) error {
 // projectID := "my-project-id"
 // datasetID := "mydataset"
 ctx := context.Background()
 client, err := bigquery.NewClient(ctx, projectID)
 if err != nil {
     return fmt.Errorf("bigquery.NewClient: %v", err)
 }
 defer client.Close()

 ts := client.Dataset(datasetID).Tables(ctx)
 for {
     t, err := ts.Next()
     if err == iterator.Done {
         break
     }
     if err != nil {
         return err
     }
     fmt.Fprintf(w, "Table: %q\n", t.TableID)
 }
 return nil
}
```

### Java

Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Java API reference documentation](/java/docs/reference/google-cloud-bigquery/latest/overview) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` java
import com.google.api.gax.paging.Page;
import com.google.cloud.bigquery.BigQuery;
import com.google.cloud.bigquery.BigQuery.TableListOption;
import com.google.cloud.bigquery.BigQueryException;
import com.google.cloud.bigquery.BigQueryOptions;
import com.google.cloud.bigquery.DatasetId;
import com.google.cloud.bigquery.Table;

public class ListTables {

  public static void runListTables() {
    // TODO(developer): Replace these variables before running the sample.
    String projectId = "bigquery-public-data";
    String datasetName = "samples";
    listTables(projectId, datasetName);
  }

  public static void listTables(String projectId, String datasetName) {
    try {
      // Initialize client that will be used to send requests. This client only needs to be created
      // once, and can be reused for multiple requests.
      BigQuery bigquery = BigQueryOptions.getDefaultInstance().getService();

      DatasetId datasetId = DatasetId.of(projectId, datasetName);
      Page<Table> tables = bigquery.listTables(datasetId, TableListOption.pageSize(100));
      tables.iterateAll().forEach(table -> System.out.print(table.getTableId().getTable() + "\n"));

      System.out.println("Tables listed successfully.");
    } catch (BigQueryException e) {
      System.out.println("Tables were not listed. Error occurred: " + e.toString());
    }
  }
}
```

### Node.js

Before trying this sample, follow the Node.js setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Node.js API reference documentation](https://googleapis.dev/nodejs/bigquery/latest/index.html) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` javascript
// Import the Google Cloud client library
const {BigQuery} = require('@google-cloud/bigquery');
const bigquery = new BigQuery();

async function listTables() {
  // Lists tables in 'my_dataset'.

  /**
   * TODO(developer): Uncomment the following lines before running the sample.
   */
  // const datasetId = 'my_dataset';

  // List all tables in the dataset
  const [tables] = await bigquery.dataset(datasetId).getTables();

  console.log('Tables:');
  tables.forEach(table => console.log(table.id));
}
```

### PHP

Before trying this sample, follow the PHP setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery PHP API reference documentation](/php/docs/reference/cloud-bigquery/latest/BigQueryClient) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` php
use Google\Cloud\BigQuery\BigQueryClient;

/** Uncomment and populate these variables in your code */
// $projectId  = 'The Google project ID';
// $datasetId  = 'The BigQuery dataset ID';

$bigQuery = new BigQueryClient([
    'projectId' => $projectId,
]);
$dataset = $bigQuery->dataset($datasetId);
$tables = $dataset->tables();
foreach ($tables as $table) {
    print($table->id() . PHP_EOL);
}
```

### Python

Before trying this sample, follow the Python setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Python API reference documentation](/python/docs/reference/bigquery/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` python
from google.cloud import bigquery

# Construct a BigQuery client object.
client = bigquery.Client()

# TODO(developer): Set dataset_id to the ID of the dataset that contains
#                  the tables you are listing.
# dataset_id = 'your-project.your_dataset'

tables = client.list_tables(dataset_id)  # Make an API request.

print("Tables contained in '{}':".format(dataset_id))
for table in tables:
    print("{}.{}.{}".format(table.project, table.dataset_id, table.table_id))
```

### Ruby

Before trying this sample, follow the Ruby setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Ruby API reference documentation](https://googleapis.dev/ruby/google-cloud-bigquery/latest/Google/Cloud/Bigquery.html) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` ruby
require "google/cloud/bigquery"

def list_tables dataset_id = "your_dataset_id"
  bigquery = Google::Cloud::Bigquery.new
  dataset  = bigquery.dataset dataset_id

  puts "Tables in dataset #{dataset_id}:"
  dataset.tables.each do |table|
    puts "\t#{table.table_id}"
  end
end
```

## Audit table history

You can audit the history of BigQuery tables by querying Cloud Audit Logs in Logs Explorer. These logs help you track when tables were created, updated, or deleted, and identify the user or service account that made the changes.

### Required permissions

To browse audit logs, you need the `  roles/logging.privateLogViewer  ` role. For more information on IAM roles and permissions in Cloud Logging, see [Access control with IAM](/logging/docs/access-control) .

### Get audit data

You can access audit information from the Google Cloud console, `  gcloud  ` command line, REST API, and all supported languages using client libraries. The logging filter shown in the following example can be used regardless of method used.

1.  In the Google Cloud console, go to the **Logging** page.

2.  Use the following query to access the audit data:
    
    ``` text
    logName = "projects/PROJECT_ID/logs/cloudaudit.googleapis.com%2Factivity"
    AND resource.type = "bigquery_dataset"
    AND timestamp >= "STARTING_TIMESTAMP"
    AND protoPayload.@type = "type.googleapis.com/google.cloud.audit.AuditLog"
    AND (
      protoPayload.metadata.tableCreation :*
      OR protoPayload.metadata.tableChange :*
      OR protoPayload.metadata.tableDeletion :*
    )
    AND protoPayload.resourceName : "projects/PROJECT_ID/datasets/DATASET_ID/tables/"
    ```

Replace the following:

  - `  PROJECT_ID  ` : the project that contains datasets and tables you are interested in.
  - `  STARTING_TIMESTAMP  ` : the oldest logs that you want to see. Use ISO 8601 format, such as `  2025-01-01  ` or `  2025-02-03T04:05:06Z  ` .
  - `  DATASET_ID  ` : the dataset that you want to filter by.

#### Interpret the results

In the Logs Explorer result pane, expand the entry you're interested in, and then click **Expand nested fields** to show the whole message.

The logging entry contains only one of the following objects to indicate the operation performed:

  - `  protoPayload.metadata.tableCreation  ` : a table was created.
  - `  protoPayload.metadata.tableChange  ` : table metadata was changed, such as schema update, description change, or table replacement.
  - `  protoPayload.metadata.tableDeletion  ` : a table was deleted.

The content of these objects describes the requested action. For a detailed description, see [`  BigQueryAuditMetadata  `](/bigquery/docs/reference/auditlogs/rest/Shared.Types/BigQueryAuditMetadata) .

#### Explanation of the query

  - `  logName = "projects/ PROJECT_ID /logs/cloudaudit.googleapis.com%2Factivity"  ` : This line filters for Admin Activity audit logs within your Google Cloud project. These logs record API calls and actions that modify the configuration or metadata of your resources.

  - `  resource.type = "bigquery_dataset"  ` : This narrows the search to events related to BigQuery datasets, where table operations are logged.

  - `  timestamp >= " STARTING_TIMESTAMP "  ` : Filters log entries to only show those created on or after the specified timestamp.

  - `  protoPayload.@type = "type.googleapis.com/google.cloud.audit.AuditLog"  ` : Ensures the log message conforms to the standard Cloud Audit Log structure.

  - `  ( ... )  ` : This block groups conditions to find different types of table events, as outlined in the previous section. The `  :*  ` operator indicates that the key must be present. If you are interested in only one event, such as table creation, remove unnecessary conditions from this block.

  - `  protoPayload.resourceName : "projects/ PROJECT_ID /datasets/ DATASET_ID /tables/"  ` : Selects log entries matching tables contained in the specified dataset. The colon ( `  :  ` ) operator performs a substring search.
    
      - To filter entries for a single table, replace the condition with the following one: `  protoPayload.resourceName = "projects/ PROJECT_ID /datasets/ DATASET_ID /tables/ TABLE_NAME "  ` .
      - To include all tables in all datasets in the specific project, remove this condition.

For more information on log filtering, see [logging query language](/logging/docs/view/logging-query-language) .

## Table security

To control access to tables in BigQuery, see [Control access to resources with IAM](/bigquery/docs/control-access-to-resources-iam) .

## What's next

  - For more information about datasets, see [Introduction to datasets](/bigquery/docs/datasets-intro) .
  - For more information about handling table data, see [Managing table data](/bigquery/docs/managing-table-data) .
  - For more information about specifying table schemas, see [Specifying a schema](/bigquery/docs/schemas) .
  - For more information about modifying table schemas, see [Modifying table schemas](/bigquery/docs/managing-table-schemas) .
  - For more information about managing tables, see [Managing tables](/bigquery/docs/managing-tables) .
  - To see an overview of `  INFORMATION_SCHEMA  ` , go to [Introduction to BigQuery `  INFORMATION_SCHEMA  `](/bigquery/docs/information-schema-intro) .

## Try it for yourself

If you're new to Google Cloud, create an account to evaluate how BigQuery performs in real-world scenarios. New customers also get $300 in free credits to run, test, and deploy workloads.
