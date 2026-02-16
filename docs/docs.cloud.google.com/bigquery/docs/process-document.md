# Process documents with the ML.PROCESS\_DOCUMENT function

This document describes how to use the [`  ML.PROCESS_DOCUMENT  ` function](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-process-document) with a [remote model](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-service) to extract useful insights from documents in an [object table](/bigquery/docs/object-table-introduction) .

## Supported locations

You must create the remote model used in this procedure in either the `  US  ` or `  EU  ` [multi-region](/bigquery/docs/locations#multi-regions) . You must run the `  ML.PROCESS_DOCUMENT  ` function in the same region as the remote model.

## Required roles

To create a remote model and process documents, you need the following Identity and Access Management (IAM) roles at the project level:

  - Create a document processor: Document AI Editor ( `  roles/documentai.editor  ` )

  - Create and use BigQuery datasets, tables, and models: BigQuery Data Editor ( `  roles/bigquery.dataEditor  ` )

  - Create, delegate, and use BigQuery connections: BigQuery Connections Admin ( `  roles/bigquery.connectionsAdmin  ` )
    
    If you don't have a [default connection](/bigquery/docs/default-connections) configured, you can create and set one as part of running the `  CREATE MODEL  ` statement. To do so, you must have BigQuery Admin ( `  roles/bigquery.admin  ` ) on your project. For more information, see [Configure the default connection](/bigquery/docs/default-connections#configure_the_default_connection) .

  - Grant permissions to the connection's service account: Project IAM Admin ( `  roles/resourcemanager.projectIamAdmin  ` )

  - Create BigQuery jobs: BigQuery Job User ( `  roles/bigquery.jobUser  ` )

These predefined roles contain the permissions required to perform the tasks in this document. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

  - Create a dataset: `  bigquery.datasets.create  `
  - Create, delegate, and use a connection: `  bigquery.connections.*  `
  - Set service account permissions: `  resourcemanager.projects.getIamPolicy  ` and `  resourcemanager.projects.setIamPolicy  `
  - Create a model and run inference:
      - `  bigquery.jobs.create  `
      - `  bigquery.models.create  `
      - `  bigquery.models.getData  `
      - `  bigquery.models.updateData  `
      - `  bigquery.models.updateMetadata  `
  - Create an object table: `  bigquery.tables.create  ` and `  bigquery.tables.update  `
  - Create a document processor:
      - `  documentai.processors.create  `
      - `  documentai.processors.update  `
      - `  documentai.processors.delete  `

You might also be able to get these permissions with [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-permissions) .

## Before you begin

1.  Sign in to your Google Cloud account. If you're new to Google Cloud, [create an account](https://console.cloud.google.com/freetrial) to evaluate how our products perform in real-world scenarios. New customers also get $300 in free credits to run, test, and deploy workloads.

2.  In the Google Cloud console, on the project selector page, select or create a Google Cloud project.
    
    **Roles required to select or create a project**
    
      - **Select a project** : Selecting a project doesn't require a specific IAM role—you can select any project that you've been granted a role on.
      - **Create a project** : To create a project, you need the Project Creator role ( `  roles/resourcemanager.projectCreator  ` ), which contains the `  resourcemanager.projects.create  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .
    
    **Note** : If you don't plan to keep the resources that you create in this procedure, create a project instead of selecting an existing project. After you finish these steps, you can delete the project, removing all resources associated with the project.

3.  [Verify that billing is enabled for your Google Cloud project](/billing/docs/how-to/verify-billing-enabled#confirm_billing_is_enabled_on_a_project) .

4.  Enable the BigQuery, BigQuery Connection API, and Document AI APIs.
    
    **Roles required to enable APIs**
    
    To enable APIs, you need the Service Usage Admin IAM role ( `  roles/serviceusage.serviceUsageAdmin  ` ), which contains the `  serviceusage.services.enable  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .

5.  In the Google Cloud console, on the project selector page, select or create a Google Cloud project.
    
    **Roles required to select or create a project**
    
      - **Select a project** : Selecting a project doesn't require a specific IAM role—you can select any project that you've been granted a role on.
      - **Create a project** : To create a project, you need the Project Creator role ( `  roles/resourcemanager.projectCreator  ` ), which contains the `  resourcemanager.projects.create  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .
    
    **Note** : If you don't plan to keep the resources that you create in this procedure, create a project instead of selecting an existing project. After you finish these steps, you can delete the project, removing all resources associated with the project.

6.  [Verify that billing is enabled for your Google Cloud project](/billing/docs/how-to/verify-billing-enabled#confirm_billing_is_enabled_on_a_project) .

7.  Enable the BigQuery, BigQuery Connection API, and Document AI APIs.
    
    **Roles required to enable APIs**
    
    To enable APIs, you need the Service Usage Admin IAM role ( `  roles/serviceusage.serviceUsageAdmin  ` ), which contains the `  serviceusage.services.enable  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .

## Create a processor

[Create a processor](/document-ai/docs/create-processor#create-processor) in Document AI to process the documents. The processor must be of a [supported type](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-service#document_processor) .

## Create a dataset

You must create the dataset, the connection and the document processor in the same region.

Create a BigQuery dataset to contain your resources:

### Console

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :
    
    If you don't see the left pane, click last\_page **Expand left pane** to open the pane.

3.  In the **Explorer** pane, click your project name.

4.  Click more\_vert **View actions \> Create dataset** .

5.  On the **Create dataset** page, do the following:
    
    1.  For **Dataset ID** , type a name for the dataset.
    
    2.  For **Location type** , select **Region** or **Multi-region** .
        
          - If you selected **Region** , then select a location from the **Region** list.
          - If you selected **Multi-region** , then select **US** or **Europe** from the **Multi-region** list.
    
    3.  Click **Create dataset** .

### bq

1.  To create a new dataset, use the [`  bq mk  `](/bigquery/docs/reference/bq-cli-reference#mk-dataset) command with the `  --location  ` flag:
    
    ``` text
    bq --location=LOCATION mk -d DATASET_ID
    ```
    
    Replace the following:
    
      - `  LOCATION  ` : the dataset's [location](/bigquery/docs/locations) .
      - `  DATASET_ID  ` is the ID of the dataset that you're creating.

2.  Confirm that the dataset was created:
    
    ``` text
    bq ls
    ```

## Create a connection

Create a [Cloud resource connection](/bigquery/docs/create-cloud-resource-connection) and get the connection's service account. Create the connection in the same [location](/bigquery/docs/locations) as the dataset you created in the previous step.

You can skip this step if you either have a default connection configured, or you have the BigQuery Admin role.

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

### Grant access to the service account

Select one of the following options:

### Console

1.  Go to the **IAM & Admin** page.

2.  Click person\_add **Grant Access** .
    
    The **Add principals** dialog opens.

3.  In the **New principals** field, enter the service account ID that you copied earlier.

4.  In the **Select a role** field, select **Document AI** , and then select **Document AI Viewer** .

5.  Click **Add another role** .

6.  In the **Select a role** field, select **Cloud Storage** , and then select **Storage Object Viewer** .

7.  Click **Save** .

### gcloud

Use the [`  gcloud projects add-iam-policy-binding  ` command](/sdk/gcloud/reference/projects/add-iam-policy-binding) :

``` text
gcloud projects add-iam-policy-binding 'PROJECT_NUMBER' --member='serviceAccount:MEMBER' --role='roles/documentai.viewer' --condition=None
gcloud projects add-iam-policy-binding 'PROJECT_NUMBER' --member='serviceAccount:MEMBER' --role='roles/storage.objectViewer' --condition=None
```

Replace the following:

  - `  PROJECT_NUMBER  ` : your project number.
  - `  MEMBER  ` : the service account ID that you copied earlier.

Failure to grant the permission results in a `  Permission denied  ` error.

**Note:** If you create the processor in a different project than the Cloud Storage bucket used by the object table, grant the service account Identity and Access Management (IAM) roles as follows:

  - Grant the service account the Document AI Viewer role in the project that contains the processor.
  - Grant the service account the Storage Object Viewer role in the project that contains the Cloud Storage bucket.

## Create a model

Create a remote model with a [`  REMOTE_SERVICE_TYPE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-service#remote_service_type) of `  CLOUD_AI_DOCUMENT_V1  ` :

``` text
CREATE OR REPLACE MODEL
`PROJECT_ID.DATASET_ID.MODEL_NAME`
REMOTE WITH CONNECTION {DEFAULT | `PROJECT_ID.REGION.CONNECTION_ID`}
OPTIONS (
  REMOTE_SERVICE_TYPE = 'CLOUD_AI_DOCUMENT_V1',
  DOCUMENT_PROCESSOR = 'PROCESSOR_ID'
);
```

Replace the following:

  - `  PROJECT_ID  ` : your project ID.

  - `  DATASET_ID  ` : the ID of the dataset to contain the model.

  - `  MODEL_NAME  ` : the name of the model.

  - `  REGION  ` : the region used by the connection.

  - `  CONNECTION_ID  ` : the connection ID—for example, `  myconnection  ` .
    
    When you [view the connection details](/bigquery/docs/working-with-connections#view-connections) in the Google Cloud console, the connection ID is the value in the last section of the fully qualified connection ID that is shown in **Connection ID** —for example `  projects/myproject/locations/connection_location/connections/ myconnection  ` .

  - `  PROCESSOR_ID  ` : the document processor ID. To find this value, [view the processor details](/document-ai/docs/create-processor#get-processor) , and then look at the **ID** row in the **Basic Information** section.

**Important:** You must specify the project ID for the connection even if the connection is in the default project.

To see the model output columns, click **Go to model** in the query result after the model is created. The output columns are shown in the **Labels** section of the **Schema** tab.

## Create an object table

[Create an object table](/bigquery/docs/object-tables) over a set of documents in Cloud Storage. The documents in the object table must be of a [supported type](/document-ai/docs/file-types) .

## Process documents

Process all the documents with the `  ML.PROCESS_DOCUMENT  ` :

``` text
SELECT *
FROM ML.PROCESS_DOCUMENT(
  MODEL `PROJECT_ID.DATASET_ID.MODEL_NAME`,
  TABLE `PROJECT_ID.DATASET_ID.OBJECT_TABLE_NAME`
  [, PROCESS_OPTIONS => ( JSON 'PROCESS_OPTIONS')]
);
```

Replace the following:

  - `  PROJECT_ID  ` : your project ID.
  - `  DATASET_ID  ` : the ID of the dataset that contains the model.
  - `  MODEL_NAME  ` : the name of the model.
  - `  OBJECT_TABLE_NAME  ` : the name of the object table that contains the URIs of the documents to process.
  - `  PROCESS_OPTIONS  ` : the json configuration that specifies how to process documents. For example, you use this to specify document chunking for the layout parser

Alternatively, process some of the documents with the `  ML.PROCESS_DOCUMENT  ` :

``` text
SELECT *
FROM ML.PROCESS_DOCUMENT(
  MODEL `PROJECT_ID.DATASET_ID.MODEL_NAME`,
  (SELECT *
  FROM `PROJECT_ID.DATASET_ID.OBJECT_TABLE_NAME`
  WHERE FILTERS
  LIMIT NUM_DOCUMENTS
  )
  [, PROCESS_OPTIONS => ( JSON 'PROCESS_OPTIONS')]
);
```

Replace the following:

  - `  PROJECT_ID  ` : your project ID.
  - `  DATASET_ID  ` : the ID of the dataset that contains the model.
  - `  MODEL_NAME  ` : the name of the model.
  - `  OBJECT_TABLE_NAME  ` : the name of the object table that contains the URIs of the documents to process.
  - `  FILTERS  ` : conditions to filter out the documents you want to process on the object table columns.
  - `  NUM_DOCUMENTS  ` : the max number of documents you want to process.
  - `  PROCESS_OPTIONS  ` : the json configuration that defines the configuration, such as chunking config for layout parser

## Examples

**Example 1**

The following example uses the [expense parser](/document-ai/docs/processors-list#processor_expense-parser) to process the documents represented by the `  documents  ` table:

``` text
SELECT *
FROM ML.PROCESS_DOCUMENT(
  MODEL `myproject.mydataset.expense_parser`,
  TABLE `myproject.mydataset.documents`
);
```

This query returns the parsed expense reports, including the currency, total amount, receipt date, and line items on the expense reports. The `  ml_process_document_result  ` column contains the raw output of the expense parser, and the `  ml_process_document_status  ` column contains any errors returned by the document processing.

**Example 2**

The following example shows how to filter the object table to choose which documents to process, and then write the results to a new table:

``` text
CREATE TABLE `myproject.mydataset.expense_details`
AS
SELECT uri, content_type, receipt_date, purchase_time, total_amount, currency
FROM
  ML.PROCESS_DOCUMENT(
    MODEL `myproject.mydataset.expense_parser`,
    (SELECT * FROM `myproject.mydataset.expense_reports`
    WHERE uri LIKE '%restaurant%'));
```

## What's next

  - For more information about model inference in BigQuery ML, see [Model inference overview](/bigquery/docs/reference/standard-sql/inference-overview) .
  - For more information about using Cloud AI APIs to perform AI tasks, see [AI application overview](/bigquery/docs/ai-application-overview) .
  - For more information about supported SQL statements and functions for generative AI models, see [End-to-end user journeys for generative AI models](/bigquery/docs/e2e-journey-genai) .
