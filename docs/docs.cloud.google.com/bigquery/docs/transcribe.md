# Transcribe audio files with the ML.TRANSCRIBE function

This document describes how to use the [`  ML.TRANSCRIBE  ` function](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-transcribe) with a [remote model](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-service) to transcribe audio files from an [object table](/bigquery/docs/object-table-introduction) .

## Supported locations

You must create the remote model used in this procedure in one of the following [locations](/bigquery/docs/locations) :

  - `  asia-northeast1  `
  - `  asia-south1  `
  - `  asia-southeast1  `
  - `  australia-southeast1  `
  - `  eu  `
  - `  europe-west1  `
  - `  europe-west2  `
  - `  europe-west3  `
  - `  europe-west4  `
  - `  northamerica-northeast1  `
  - `  us  `
  - `  us-central1  `
  - `  us-east1  `
  - `  us-east4  `
  - `  us-west1  `

You must run the `  ML.TRANSCRIBE  ` function in the same region as the remote model.

## Required roles

To create a remote model and transcribe audio files, you need the following Identity and Access Management (IAM) roles at the project level:

  - Create a speech recognizer: Cloud Speech Editor ( `  roles/speech.editor  ` )

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
  - Create a speech recognizer:
      - `  speech.recognizers.create  `
      - `  speech.recognizers.get  `
      - `  speech.recognizers.recognize  `
      - `  speech.recognizers.update  `

You might also be able to get these permissions with [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-permissions) .

## Before you begin

1.  Sign in to your Google Cloud account. If you're new to Google Cloud, [create an account](https://console.cloud.google.com/freetrial) to evaluate how our products perform in real-world scenarios. New customers also get $300 in free credits to run, test, and deploy workloads.

2.  In the Google Cloud console, on the project selector page, select or create a Google Cloud project.
    
    **Roles required to select or create a project**
    
      - **Select a project** : Selecting a project doesn't require a specific IAM role—you can select any project that you've been granted a role on.
      - **Create a project** : To create a project, you need the Project Creator role ( `  roles/resourcemanager.projectCreator  ` ), which contains the `  resourcemanager.projects.create  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .
    
    **Note** : If you don't plan to keep the resources that you create in this procedure, create a project instead of selecting an existing project. After you finish these steps, you can delete the project, removing all resources associated with the project.

3.  [Verify that billing is enabled for your Google Cloud project](/billing/docs/how-to/verify-billing-enabled#confirm_billing_is_enabled_on_a_project) .

4.  Enable the BigQuery, BigQuery Connection API, and Speech-to-Text APIs.
    
    **Roles required to enable APIs**
    
    To enable APIs, you need the Service Usage Admin IAM role ( `  roles/serviceusage.serviceUsageAdmin  ` ), which contains the `  serviceusage.services.enable  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .

5.  In the Google Cloud console, on the project selector page, select or create a Google Cloud project.
    
    **Roles required to select or create a project**
    
      - **Select a project** : Selecting a project doesn't require a specific IAM role—you can select any project that you've been granted a role on.
      - **Create a project** : To create a project, you need the Project Creator role ( `  roles/resourcemanager.projectCreator  ` ), which contains the `  resourcemanager.projects.create  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .
    
    **Note** : If you don't plan to keep the resources that you create in this procedure, create a project instead of selecting an existing project. After you finish these steps, you can delete the project, removing all resources associated with the project.

6.  [Verify that billing is enabled for your Google Cloud project](/billing/docs/how-to/verify-billing-enabled#confirm_billing_is_enabled_on_a_project) .

7.  Enable the BigQuery, BigQuery Connection API, and Speech-to-Text APIs.
    
    **Roles required to enable APIs**
    
    To enable APIs, you need the Service Usage Admin IAM role ( `  roles/serviceusage.serviceUsageAdmin  ` ), which contains the `  serviceusage.services.enable  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .

## Create a recognizer

Speech-to-Text supports resources called recognizers. Recognizers represent stored and reusable recognition configurations. You can [create a recognizer](/speech-to-text/v2/docs/recognizers) to logically group together transcriptions or traffic for your application.

Creating a speech recognizer is optional. If you choose to create a speech recognizer, note the project ID, location, and recognizer ID of the recognizer for use in the `  CREATE MODEL  ` statement, as described in [`  SPEECH_RECOGNIZER  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-service#speech_recognizer) . If you choose not to create a speech recognizer, you must specify a value for the [`  recognition_config  ` argument](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-transcribe#arguments) of the `  ML.TRANSCRIBE  ` function.

You can only use the `  chirp  ` [transcription model](/speech-to-text/v2/docs/transcription-model#transcription_models) in the speech recognizer or `  recognition_config  ` value that you provide.

## Create a dataset

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

4.  Click the **Select a role** field and then type `  Cloud Speech Client  ` in **Filter** .

5.  Click **Add another role** .

6.  In the **Select a role** field, select **Cloud Storage** , and then select **Storage Object Viewer** .

7.  Click **Save** .

### gcloud

Use the [`  gcloud projects add-iam-policy-binding  ` command](/sdk/gcloud/reference/projects/add-iam-policy-binding) :

``` text
gcloud projects add-iam-policy-binding 'PROJECT_NUMBER' --member='serviceAccount:MEMBER' --role='roles/speech.client' --condition=None
gcloud projects add-iam-policy-binding 'PROJECT_NUMBER' --member='serviceAccount:MEMBER' --role='roles/storage.objectViewer' --condition=None
```

Replace the following:

  - `  PROJECT_NUMBER  ` : your project number.
  - `  MEMBER  ` : the service account ID that you copied earlier.

Failure to grant the permission results in a `  Permission denied  ` error.

**Note:** If you create the recognizer in a different project than the Cloud Storage bucket used by the object table, grant the service account Identity and Access Management (IAM) roles as follows:

  - Grant the service account the Cloud Speech Client role in the project that contains the recognizer.
  - Grant the service account the Storage Object Viewer role in the project that contains the Cloud Storage bucket.
  - Grant the Speech-to-Text service agent ( `  service- my_project_number @gcp-sa-speech.iam.gserviceaccount.com  ` ) the Storage Object Viewer role in the project that contains the Cloud Storage bucket.

## Create an object table

[Create an object table](/bigquery/docs/object-tables) over a set of audio files in Cloud Storage. The audio files in the object table must be of a [supported type](/speech-to-text/docs/encoding#audio-encodings) .

The Cloud Storage bucket used by the object table should be in the same project where you plan to create the model and call the `  ML.TRANSCRIBE  ` function. If you want to call the `  ML.TRANSCRIBE  ` function in a different project than the one that contains the Cloud Storage bucket used by the object table, you must [grant the Storage Admin role at the bucket level](/storage/docs/access-control/using-iam-permissions#bucket-add) to the `  service-A@gcp-sa-aiplatform.iam.gserviceaccount.com  ` service account.

## Create a model

Create a remote model with a [`  REMOTE_SERVICE_TYPE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-service#remote_service_type) of `  CLOUD_AI_SPEECH_TO_TEXT_V2  ` :

``` text
CREATE OR REPLACE MODEL
`PROJECT_ID.DATASET_ID.MODEL_NAME`
REMOTE WITH CONNECTION {DEFAULT | `PROJECT_ID.REGION.CONNECTION_ID`}
OPTIONS (
  REMOTE_SERVICE_TYPE = 'CLOUD_AI_SPEECH_TO_TEXT_V2',
  SPEECH_RECOGNIZER = 'projects/PROJECT_NUMBER/locations/LOCATION/recognizers/RECOGNIZER_ID'
);
```

Replace the following:

  - `  PROJECT_ID  ` : your project ID.

  - `  DATASET_ID  ` : the ID of the dataset to contain the model.

  - `  MODEL_NAME  ` : the name of the model.

  - `  REGION  ` : the region used by the connection.

  - `  CONNECTION_ID  ` : the connection ID—for example, `  myconnection  ` .
    
    When you [view the connection details](/bigquery/docs/working-with-connections#view-connections) in the Google Cloud console, the connection ID is the value in the last section of the fully qualified connection ID that is shown in **Connection ID** —for example `  projects/myproject/locations/connection_location/connections/ myconnection  ` .

  - `  PROJECT_NUMBER  ` : the project number of the project that contains the speech recognizer. You can find this value on the **Project info** card in the **Dashboard** page of the Google Cloud console.

  - `  LOCATION  ` : the location used by the speech recognizer. You can find this value in the **Location** field on the [**List recognizers** page](https://console.cloud.google.com/speech/recognizers/list) of the Google Cloud console.

  - `  RECOGNIZER_ID  ` : the speech recognizer ID. You can find this value in the **ID** field on the [**List recognizers** page](https://console.cloud.google.com/speech/recognizers/list) of the Google Cloud console.
    
    This option isn't required. If you don't specify a value for it, a default recognizer is used. In that case, you must specify a value for the `  recognition_config  ` parameter of the `  ML.TRANSCRIBE  ` function in order to provide a configuration for the default recognizer.
    
    You can only use the `  chirp  ` [transcription model](/speech-to-text/v2/docs/transcription-model#transcription_models) in the `  recognition_config  ` value that you provide.

**Important:** You must specify the project ID for the connection even if the connection is in the default project.

## Transcribe audio files

Transcribe audio files with the `  ML.TRANSCRIBE  ` function:

``` text
SELECT *
FROM ML.TRANSCRIBE(
  MODEL `PROJECT_ID.DATASET_ID.MODEL_NAME`,
  TABLE `PROJECT_ID.DATASET_ID.OBJECT_TABLE_NAME`,
  RECOGNITION_CONFIG => ( JSON 'recognition_config')
);
```

Replace the following:

  - `  PROJECT_ID  ` : your project ID.

  - `  DATASET_ID  ` : the ID of the dataset that contains the model.

  - `  MODEL_NAME  ` : the name of the model.

  - `  OBJECT_TABLE_NAME  ` : the name of the object table that contains the URIs of the audio files to process.

  - `  recognition_config  ` : a [`  RecognitionConfig  ` resource](/speech-to-text/v2/docs/reference/rest/v2/projects.locations.recognizers#recognitionconfig) in JSON format.
    
    If a recognizer has been specified for the remote model by using the [`  SPEECH_RECOGNIZER  ` option](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-service#speech_recognizer) , you can't specify a `  recognition_config  ` value.
    
    If no recognizer has been specified for the remote model by using the `  SPEECH_RECOGNIZER  ` option, you must specify a `  recognition_config  ` value. This value is used to provide a configuration for the default recognizer.
    
    You can only use the `  chirp  ` [transcription model](/speech-to-text/v2/docs/transcription-model#transcription_models) in the `  recognition_config  ` value that you provide.

## Examples

**Example 1**

The following example transcribes the audio files represented by the `  audio  ` table without overriding the recognizer's default configuration:

``` text
SELECT *
FROM ML.TRANSCRIBE(
  MODEL `myproject.mydataset.transcribe_model`,
  TABLE `myproject.mydataset.audio`
);
```

The following example transcribes the audio files represented by the `  audio  ` table and provides a configuration for the default recognizer:

``` text
SELECT *
FROM ML.TRANSCRIBE(
  MODEL `myproject.mydataset.transcribe_model`,
  TABLE `myproject.mydataset.audio`,
  recognition_config => ( JSON '{"language_codes": ["en-US" ],"model": "chirp","auto_decoding_config": {}}')
);
```

## What's next

  - For more information about model inference in BigQuery ML, see [Model inference overview](/bigquery/docs/reference/standard-sql/inference-overview) .
  - For more information about using Cloud AI APIs to perform AI tasks, see [AI application overview](/bigquery/docs/ai-application-overview) .
  - For more information about supported SQL statements and functions for generative AI models, see [End-to-end user journeys for generative AI models](/bigquery/docs/e2e-journey-genai) .
