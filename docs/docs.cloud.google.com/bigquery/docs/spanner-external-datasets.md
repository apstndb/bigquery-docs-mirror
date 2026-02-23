# Create Spanner external datasets

This document describes how to create an external dataset (also known as a federated dataset) in BigQuery that's linked to an existing GoogleSQL or PostgreSQL database in [Spanner](/spanner/docs) .

An external dataset is a connection between BigQuery and an external data source at the dataset level. It lets you query transactional data in Spanner databases with GoogleSQL without needing to copy or import all of the data from Spanner to BigQuery storage. These query results are [stored in BigQuery](/bigquery/docs/writing-results#temporary_and_permanent_tables) .

The tables in an external dataset are automatically populated from the tables in the corresponding external data source. You can query these tables directly in BigQuery, but you cannot make modifications, additions, or deletions. However, any updates that you make in the external data source are automatically reflected in BigQuery.

When you query Spanner, query results are by default saved in temporary tables. They can also optionally be saved as a new BigQuery table, joined with other tables, or merged with existing tables using [DML](/bigquery/docs/reference/standard-sql/dml-syntax) .

## Required permissions

To get the permission that you need to create an external dataset, ask your administrator to grant you the [BigQuery User](/iam/docs/roles-permissions/bigquery#bigquery.user) ( `  roles/bigquery.user  ` ) IAM role . For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

This predefined role contains the `  bigquery.datasets.create  ` permission, which is required to create an external dataset.

You might also be able to get this permission with [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

For more information about IAM roles and permissions in BigQuery, see [Introduction to IAM](/bigquery/docs/access-control) .

## Use a `     CLOUD_RESOURCE    ` connection

Optionally, Spanner external datasets can use a `  CLOUD_RESOURCE  ` connection to interact with your Spanner database, so that you can provide a user access to Spanner data through BigQuery, without giving them direct access to the Spanner database. Because the service account from `  CLOUD_RESOURCE  ` connection handles retrieving data from the Spanner, you only have to grant users access to the Spanner external dataset.

Before you create Spanner external datasets with a `  CLOUD_RESOURCE  ` connection, do the following:

### Create a connection

You can create or use an existing [`  CLOUD_RESOURCE  ` connection](/bigquery/docs/create-cloud-resource-connection) to connect to Spanner. Make sure to create the connection in the same [location](/bigquery/docs/locations) that you plan to create your Spanner external dataset.

Select one of the following options:

### Console

1.  Go to the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :
    
    If you don't see the left pane, click last\_page **Expand left pane** to open the pane.

3.  In the **Explorer** pane, expand your project name, and then click **Connections** .

4.  On the **Connections** page, click **Create connection** .

5.  For **Connection type** , choose **Vertex AI remote models, remote functions, BigLake and Spanner (Cloud Resource)** .

6.  In the **Connection ID** field, enter a name for your connection.

7.  For **Location type** , select a location for your connection. The connection should be colocated with your other resources such as datasets.

8.  Click **Create connection** .

9.  Click **Go to connection** .

10. In the **Connection info** pane, copy the service account ID for use in a later step.

### bq

1.  In a command-line environment, create a connection:
    
    ``` text
    bq mk --connection --location=REGION --project_id=PROJECT_ID \
        --connection_type=CLOUD_RESOURCE CONNECTION_ID
    ```
    
    The `  --project_id  ` parameter overrides the default project.
    
    Replace the following:
    
      - `  REGION  ` : your [connection region](/bigquery/docs/locations#supported_locations)
      - `  PROJECT_ID  ` : your Google Cloud project ID
      - `  CONNECTION_ID  ` : an ID for your connection
    
    When you create a connection resource, BigQuery creates a unique system service account and associates it with the connection.
    
    **Troubleshooting** : If you get the following connection error, [update the Google Cloud SDK](/sdk/docs/quickstart) :
    
    ``` console
    Flags parsing error: flag --connection_type=CLOUD_RESOURCE: value should be one of...
    ```

2.  Retrieve and copy the service account ID for use in a later step:
    
    ``` text
    bq show --connection PROJECT_ID.REGION.CONNECTION_ID
    ```
    
    The output is similar to the following:
    
    ``` console
    name                          properties
    1234.REGION.CONNECTION_ID     {"serviceAccountId": "connection-1234-9u56h9@gcp-sa-bigquery-condel.iam.gserviceaccount.com"}
    ```

### Python

Before trying this sample, follow the Python setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Python API reference documentation](/python/docs/reference/bigquery/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` python
import google.api_core.exceptions
from google.cloud import bigquery_connection_v1

client = bigquery_connection_v1.ConnectionServiceClient()


def create_connection(
    project_id: str,
    location: str,
    connection_id: str,
):
    """Creates a BigQuery connection to a Cloud Resource.

    Cloud Resource connection creates a service account which can then be
    granted access to other Google Cloud resources for federated queries.

    Args:
        project_id: The Google Cloud project ID.
        location: The location of the connection (for example, "us-central1").
        connection_id: The ID of the connection to create.
    """

    parent = client.common_location_path(project_id, location)

    connection = bigquery_connection_v1.Connection(
        friendly_name="Example Connection",
        description="A sample connection for a Cloud Resource.",
        cloud_resource=bigquery_connection_v1.CloudResourceProperties(),
    )

    try:
        created_connection = client.create_connection(
            parent=parent, connection_id=connection_id, connection=connection
        )
        print(f"Successfully created connection: {created_connection.name}")
        print(f"Friendly name: {created_connection.friendly_name}")
        print(
            f"Service Account: {created_connection.cloud_resource.service_account_id}"
        )

    except google.api_core.exceptions.AlreadyExists:
        print(f"Connection with ID '{connection_id}' already exists.")
        print("Please use a different connection ID.")
    except Exception as e:
        print(f"An unexpected error occurred while creating the connection: {e}")
```

### Node.js

Before trying this sample, follow the Node.js setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Node.js API reference documentation](https://googleapis.dev/nodejs/bigquery/latest/index.html) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` javascript
const {ConnectionServiceClient} =
  require('@google-cloud/bigquery-connection').v1;
const {status} = require('@grpc/grpc-js');

const client = new ConnectionServiceClient();

/**
 * Creates a new BigQuery connection to a Cloud Resource.
 *
 * A Cloud Resource connection creates a service account that can be granted access
 * to other Google Cloud resources.
 *
 * @param {string} projectId The Google Cloud project ID. for example, 'example-project-id'
 * @param {string} location The location of the project to create the connection in. for example, 'us-central1'
 * @param {string} connectionId The ID of the connection to create. for example, 'example-connection-id'
 */
async function createConnection(projectId, location, connectionId) {
  const parent = client.locationPath(projectId, location);

  const connection = {
    friendlyName: 'Example Connection',
    description: 'A sample connection for a Cloud Resource',
    // The service account for this cloudResource will be created by the API.
    // Its ID will be available in the response.
    cloudResource: {},
  };

  const request = {
    parent,
    connectionId,
    connection,
  };

  try {
    const [response] = await client.createConnection(request);

    console.log(`Successfully created connection: ${response.name}`);
    console.log(`Friendly name: ${response.friendlyName}`);

    console.log(`Service Account: ${response.cloudResource.serviceAccountId}`);
  } catch (err) {
    if (err.code === status.ALREADY_EXISTS) {
      console.log(`Connection '${connectionId}' already exists.`);
    } else {
      console.error(`Error creating connection: ${err.message}`);
    }
  }
}
```

### Terraform

Use the [`  google_bigquery_connection  `](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/bigquery_connection) resource.

**Note:** To create BigQuery objects using Terraform, you must enable the [Cloud Resource Manager API](/resource-manager/reference/rest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

The following example creates a Cloud resource connection named `  my_cloud_resource_connection  ` in the `  US  ` region:

``` terraform
# This queries the provider for project information.
data "google_project" "default" {}

# This creates a cloud resource connection in the US region named my_cloud_resource_connection.
# Note: The cloud resource nested object has only one output field - serviceAccountId.
resource "google_bigquery_connection" "default" {
  connection_id = "my_cloud_resource_connection"
  project       = data.google_project.default.project_id
  location      = "US"
  cloud_resource {}
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

After you create the connection, open it, and in the **Connection info** pane, copy the service account ID. You need this ID when you configure permissions for the connection. When you create a connection resource, BigQuery creates a unique system service account and associates it with the connection.

### Set up access

You must give the service account that is associated with the new connection read access to your Spanner instance or database. It is recommended to use Cloud Spanner Database Reader with DataBoost ( `  roles/spanner.databaseReaderWithDataBoost  ` ) predefined IAM role.

Follow these steps to grant access to database-level roles for the service account that you copied earlier from the connection:

1.  Go to the Spanner **Instances** page.

2.  Click the name of the instance that contains your database to go to the **Instance details** page.

3.  In the **Overview** tab, select the checkbox for your database.  
    The **Info panel** appears.

4.  Click **Add principal** .

5.  In the **Add principals** panel, in **New principals** , enter the service account ID that you copied earlier.

6.  In the **Select a role** field, select **Cloud Spanner Database Reader with DataBoost role** .

7.  Click **Save** .

## Create an external dataset

To create an external dataset, do the following:

### Console

1.  Open the BigQuery page in the Google Cloud console.

2.  In the left pane, click explore **Explorer** :
    
    If you don't see the left pane, click last\_page **Expand left pane** to open the pane.

3.  In the **Explorer** pane, select the project where you want to create the dataset.

4.  Click more\_vert **View actions** , and then click **Create dataset** .

5.  On the **Create dataset** page, do the following:
    
      - For **Dataset ID** , enter a unique dataset name.
    
      - For **Location type** , choose a location for the dataset, such as `  us-central1  ` or multiregion `  us  ` . After you create a dataset, the location can't be changed.
    
      - For **External Dataset** , do the following:
        
          - Check the box next to **Link to an external dataset** .
          - For **External dataset type** , select `  Spanner  ` .
          - For **External source** , enter the full identifier of your Spanner database in the following format: `  projects/ PROJECT_ID /instances/ INSTANCE /databases/ DATABASE  ` . For example: `  projects/my_project/instances/my_instance/databases/my_database  ` .
          - Optionally, for **Database role** enter the name of a Spanner database role. For more information read about Database roles used for [creating Spanner Connections](/bigquery/docs/connect-to-spanner#create-spanner-connection)
          - Optionally, check the box next to **Use a Cloud Resource connection** to create the external dataset with a connection.
    
      - Leave the other default settings as they are.

6.  Click **Create dataset** .

### SQL

Use the [`  CREATE EXTERNAL SCHEMA  ` data definition language (DDL) statement](/bigquery/docs/reference/standard-sql/data-definition-language#create_external_schema_statement) .

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
    CREATE EXTERNAL SCHEMA DATASET_NAME
      OPTIONS (
        external_source = 'SPANNER_EXTERNAL_SOURCE',
        location = 'LOCATION');
    /*
      Alternatively, create with a connection:
    */
    CREATE EXTERNAL SCHEMA DATASET_NAME
      WITH CONNECTION PROJECT_ID.LOCATION.CONNECTION_NAME
      OPTIONS (
        external_source = 'SPANNER_EXTERNAL_SOURCE',
        location = 'LOCATION');
    ```
    
    Replace the following:
    
      - `  DATASET_NAME  ` : the name of your new dataset in BigQuery.
      - `  SPANNER_EXTERNAL_SOURCE  ` : the full, qualified Spanner database name, with a prefix identifying the source, in the following format: `  google-cloudspanner://[ DATABASE_ROLE @]/projects/ PROJECT_ID /instances/ INSTANCE /databases/ DATABASE  ` . For example: `  google-cloudspanner://admin@/projects/my_project/instances/my_instance/databases/my_database  ` or `  google-cloudspanner:/projects/my_project/instances/my_instance/databases/my_database  ` .
      - `  LOCATION  ` : the location of your new dataset in BigQuery, for example, `  us-central1  ` . After you create a dataset, you can't change its location.
      - (Optional) `  CONNECTION_NAME  ` : the name of your Cloud resource connection.

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](/bigquery/docs/running-queries#queries) .

### bq

In a command-line environment, create an external dataset by using the [`  bq mk  ` command](/bigquery/docs/reference/bq-cli-reference#mk-dataset) :

``` text
bq --location=LOCATION mk --dataset \
    --external_source SPANNER_EXTERNAL_SOURCE \
    DATASET_NAME
```

Alternatively, create with a connection:

``` text
bq --location=LOCATION mk --dataset \
    --external_source SPANNER_EXTERNAL_SOURCE \
    --connection_id PROJECT_ID.LOCATION.CONNECTION_NAME \
    DATASET_NAME
```

Replace the following:

  - `  LOCATION  ` : the location of your new dataset in BigQuery—for example, `  us-central1  ` . After you create a dataset, you can't change its location. You can set a default location value by using the [`  .bigqueryrc  ` file](/bigquery/docs/bq-command-line-tool#setting_default_values_for_command-line_flags) .
  - `  SPANNER_EXTERNAL_SOURCE  ` : the full, qualified Spanner database name, with a prefix identifying the source, in the following format: `  google-cloudspanner://[ DATABASE_ROLE @]/projects/ PROJECT_ID /instances/ INSTANCE /databases/ DATABASE  ` . For example: `  google-cloudspanner://admin@/projects/my_project/instances/my_instance/databases/my_database  ` or `  google-cloudspanner:/projects/my_project/instances/my_instance/databases/my_database  ` .
  - `  DATASET_NAME  ` : the name of your new dataset in BigQuery. To create a dataset in a project other than your default project, add the project ID to the dataset name in the following format: `  PROJECT_ID  ` : `  DATASET_NAME  ` .
  - (Optional) `  CONNECTION_NAME  ` : the name of your Cloud resource connection.

### Terraform

Use the [`  google_bigquery_dataset  ` resource](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/bigquery_dataset#example-usage---bigquery-dataset-external-reference-aws-docs) .

**Note:** To create BigQuery objects using Terraform, you must enable the [Cloud Resource Manager API](/resource-manager/reference/rest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

The following example creates a Spanner external dataset:

``` terraform
resource "google_bigquery_dataset" "default" {
  dataset_id    = "my_external_dataset"
  friendly_name = "My external dataset"
  description   = "This is a test description."
  location      = "US"
  external_dataset_reference {
    # The full identifier of your Spanner database.
    external_source = "google-cloudspanner:/projects/my_project/instances/my_instance/databases/my_database"
    # Must be empty for a Spanner external dataset.
    connection = ""
  }
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

Call the [`  datasets.insert  ` method](/bigquery/docs/reference/rest/v2/datasets/insert) with a defined [dataset resource](/bigquery/docs/reference/rest/v2/datasets) and [`  externalDatasetReference  ` field](/bigquery/docs/reference/rest/v2/datasets#ExternalDatasetReference) for your Spanner database.

Note that names of the tables in the external datasets are case insensitive.

When you create the external datasets with a `  CLOUD_RESOURCE  ` connection, you need to have the `  bigquery.connections.delegate  ` permission (available from the BigQuery Connection Admin role) on the connection that is used by the external datasets.

## Control access to tables

Spanner external datasets support end-user credentials (EUC). That means that access to the Spanner tables from external datasets is controlled by Spanner. Users can query these tables only if they have access granted in Spanner.

Spanner external datasets also support access delegation. Access delegation decouples access to the Spanner tables from external datasets and the direct access to the underlying Spanner tables. A Cloud resource connection associated with a service account is used to connect to the Spanner. Users can query these Spanner tables from external datasets even if they don't have access granted in Spanner.

## List tables in an external dataset

To list the tables that are available for query in your external dataset, see [Listing datasets](/bigquery/docs/listing-datasets) .

## Get table information

To get information on the tables in your external dataset, such as schema details, see [Get table information](/bigquery/docs/tables#get_table_information) .

## Query Spanner data

[Querying tables](/bigquery/docs/running-queries) in external datasets is the same as querying tables in any other BigQuery dataset. However, data modification operations (DML) aren't supported.

Queries against tables in Spanner external datasets use [Data Boost](/bigquery/docs/spanner-federated-queries#data_boost) by default and it cannot be changed. Because of that you need [additional permissions](/bigquery/docs/spanner-federated-queries#before_you_begin_2) to run such queries.

## Create a view in an external dataset

You can't create a view in an external dataset. However, you can create a view in a standard dataset that's based on a table in an external dataset. For more information, see [Create views](/bigquery/docs/views) .

## Delete an external dataset

Deleting an external dataset is the same as deleting any other BigQuery dataset. Deleting external datasets does not impact tables in the Spanner database. For more information, see [Delete datasets](/bigquery/docs/managing-datasets#delete-datasets) .

## Create a non-incremental materialized view based on tables from an external dataset

**Preview**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

Before you proceed, you must create the underlying Spanner external dataset using a [`  CLOUD_RESOURCE  ` connection](/bigquery/docs/spanner-external-datasets#use_a_cloud_resource_connection) .

You can create non-incremental materialized views that reference [Spanner external dataset tables](/bigquery/docs/spanner-external-datasets) by using the `  allow_non_incremental_definition  ` option. The following example uses a base Spanner external dataset table:

``` text
/*
  You must create the spanner_external_dataset with a CLOUD_RESOURCE connection.
*/
CREATE MATERIALIZED VIEW sample_dataset.sample_spanner_mv
  OPTIONS (
      enable_refresh = true, refresh_interval_minutes = 60,
      max_staleness = INTERVAL "24" HOUR,
        allow_non_incremental_definition = true)
AS
  SELECT COUNT(*) cnt FROM spanner_external_dataset.spanner_table;
```

## Limitations

  - BigQuery federated queries [limitations](/bigquery/docs/federated-queries-intro#limitations) apply.
  - Only tables from a default Spanner schema are accessible in BigQuery. Tables from [named schemas](/spanner/docs/schema-and-data-model#named-schemas) aren't supported.
  - Primary and foreign keys defined in Spanner database aren't visible in BigQuery.
  - If a table in Spanner database contains a column of a type that isn't supported by BigQuery then this column won't be accessible on BigQuery side.
  - You can't add, delete, or update data or metadata in tables in a Spanner external dataset.
  - You can't create new tables, views, or materialized views in a Spanner external dataset.
  - [`  INFORMATION_SCHEMA  ` views](/bigquery/docs/information-schema-intro) aren't supported.
  - [Metadata caching](/bigquery/docs/biglake-intro#metadata_caching_for_performance) isn't supported.
  - Dataset-level settings that are related to table creation defaults don't affect external datasets because you can't create tables manually.
  - Write API and Read API aren't supported.
  - Row-level security, column-level security, and data masking aren't supported.
  - Incremental materialized views based on tables from Spanner external datasets aren't supported, however, non-incremental materialized views are supported in preview.
  - Integration with Dataplex Universal Catalog isn't supported. For example, data profiles and data quality scans aren't supported.
  - Tags on a table level aren't supported.
  - SQL auto completion does not work with Spanner external tables when you write queries.
  - [Scan with Sensitive Data Protection](/bigquery/docs/scan-with-dlp#scanning-bigquery-data-using-the-cloud-console) isn't supported for external datasets.
  - Sharing with BigQuery sharing (formerly Analytics Hub) isn't supported for external datasets.
  - If the Spanner external dataset uses end-user credentials (EUC), you can create an authorized view that references the external dataset. However, when this view is queried, then EUC of a person who executes a query will be sent to Spanner.
  - If the Spanner external dataset uses a Cloud resource connection for access delegation, you can create an authorized view or an authorized routine that references the external dataset.

## What's next

  - Learn more about [Spanner federated queries](/bigquery/docs/spanner-federated-queries) .
  - Learn more about [creating materialized views over Spanner external datasets](/bigquery/docs/materialized-views-create#spanner) .
