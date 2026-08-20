---
name: documents/docs.cloud.google.com/bigquery/docs/generate-text-scalar
uri: https://docs.cloud.google.com/bigquery/docs/generate-text-scalar
title: Generate text with the AI.GENERATE function
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

This tutorial shows you how to generate text from text, audio, or video by using the [`AI.GENERATE` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate) along with a hosted Gemini model. This approach eliminates the need to create and maintain your own model.

## Objectives

  - Summarize news articles.
  - Generate structured output from news articles that includes a summary and overall sentiment.
  - Create a transcript of a video in Japanese and translate it to English.
  - Generate a summary and list of topics from audio content.

## Costs

In this document, you use the following billable components of Google Cloud:

  - **BigQuery ML** : You incur costs for the data that you process in BigQuery.
  - **Gemini Enterprise Agent Platform** : You incur costs for calls to the Agent Platform model.

To generate a cost estimate based on your projected usage, use the [pricing calculator](https://docs.cloud.google.com/products/calculator) .

New Google Cloud users might be eligible for a [free trial](https://docs.cloud.google.com/free) .

For more information, see [BigQuery pricing](https://cloud.google.com/bigquery/pricing) and [Agent Platform pricing](https://cloud.google.com/vertex-ai/generative-ai/pricing) .

## Before you begin

1.  Enable the BigQuery API.
    
    **Roles required to enable APIs**
    
    To enable APIs, you need the `serviceusage.services.enable` permission. If you created the project, then you likely already have this permission through the Owner role ( `roles/owner` ). Otherwise, you can get this permission through the Service Usage Admin role ( `roles/serviceusage.serviceUsageAdmin` ). [Learn how to grant roles](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .
    
    For new projects, the BigQuery API is automatically enabled.

### Required roles

To get the permissions that you need to use the `AI.GENERATE` function, ask your administrator to grant you the following IAM roles:

  - Create and use BigQuery datasets and tables: [BigQuery Data Editor](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor) ( `roles/bigquery.dataEditor` ) on your project.
  - Create, delegate, and use BigQuery connections: [BigQuery Connections Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.connectionsAdmin) ( `roles/bigquery.connectionsAdmin` ) on your project.
  - Grant permissions to the connection's service account: [Project IAM Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/resourcemanager#resourcemanager.projectIamAdmin) ( `roles/resourcemanager.projectIamAdmin` ) on the project that contains the Gemini Enterprise Agent Platform endpoint.
  - Create BigQuery jobs: [BigQuery Job User](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.jobUser) ( `roles/bigquery.jobUser` ) on your project.

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

These predefined roles contain the permissions required to use the `AI.GENERATE` function. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

The following permissions are required to use the `AI.GENERATE` function:

  - Create a dataset: `bigquery.datasets.create`
  - Create, delegate, and use a connection: `bigquery.connections.*`
  - Set service account permissions:
      - `resourcemanager.projects.getIamPolicy`
      - `resourcemanager.projects.setIamPolicy`
  - Query table data: `bigquery.tables.getData`

You might also be able to get these permissions with [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## Create a dataset

Create a BigQuery dataset to contain your resources:

### Console

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :
    
    ![Highlighted button for the Explorer pane.](https://docs.cloud.google.com/static/bigquery/images/explorer-tab.png)
    
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

1.  To create a new dataset, use the [`bq mk`](https://docs.cloud.google.com/bigquery/docs/reference/bq-cli-reference#mk-dataset) command with the `--location` flag:
    
        bq --location=LOCATION mk -d DATASET_ID
    
    Replace the following:
    
      - `  LOCATION  ` : the dataset's [location](https://docs.cloud.google.com/bigquery/docs/locations) .
      - `  DATASET_ID  ` : the ID of the dataset that you're creating.

2.  Confirm that the dataset was created:
    
        bq ls

## Create a connection

After you create the training dataset, you establish a connection to link BigQuery and external sources. Create a [Cloud resource connection](https://docs.cloud.google.com/bigquery/docs/create-cloud-resource-connection) and get the connection's service account. Create the connection in the same [location](https://docs.cloud.google.com/bigquery/docs/locations) as the dataset that you created in the previous step.

Select one of the following options:

### Console

1.  Go to the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :
    
    ![Highlighted button for the Explorer pane.](https://docs.cloud.google.com/static/bigquery/images/explorer-tab.png)
    
    If you don't see the left pane, click last\_page **Expand left pane** to open the pane.

3.  In the **Explorer** pane, expand your project name, and then click **Connections** .

4.  On the **Connections** page, click **Create connection** .

5.  For **Connection type** , choose **Vertex AI remote models, remote functions, BigLake and Spanner (Cloud Resource)** .

6.  In the **Connection ID** field, enter a name for your connection.

7.  For **Location type** , select a location for your connection. The connection should be colocated with your other resources such as datasets.

8.  Click **Create connection** .

9.  Click **Go to connection** .

10. In the **Connection info** pane, copy the service account ID for use in a later step.

### SQL

Use the [`CREATE CONNECTION` statement](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_connection_statement) :

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
        CREATE CONNECTION [IF NOT EXISTS] `CONNECTION_NAME`
        OPTIONS (
          connection_type = "CLOUD_RESOURCE",
          friendly_name = "FRIENDLY_NAME",
          description = "DESCRIPTION"
          );
    
    Replace the following:
    
      - `  CONNECTION_NAME  ` : the name of the connection in either the `  PROJECT_ID . LOCATION . CONNECTION_ID  ` , `  LOCATION . CONNECTION_ID  ` , or `  CONNECTION_ID  ` format. If the project or location are omitted, then they are inferred from the project and location where the statement is run.
      - `  FRIENDLY_NAME  ` (optional): a descriptive name for the connection.
      - `  DESCRIPTION  ` (optional): a description of the connection.

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](https://docs.cloud.google.com/bigquery/docs/running-queries#queries) .

### bq

1.  In a command-line environment, create a connection:
    
        bq mk --connection --location=REGION --project_id=PROJECT_ID \
            --connection_type=CLOUD_RESOURCE CONNECTION_ID
    
    The `--project_id` parameter overrides the default project.
    
    Replace the following:
    
      - `  REGION  ` : your [connection region](https://docs.cloud.google.com/bigquery/docs/locations#supported_locations)
      - `  PROJECT_ID  ` : your Google Cloud project ID
      - `  CONNECTION_ID  ` : an ID for your connection
    
    When you create a connection resource, BigQuery creates a unique system service account and associates it with the connection.
    
    **Troubleshooting** : If you get the following connection error, [update the Google Cloud SDK](https://docs.cloud.google.com/sdk/docs/quickstart) :
    
    ```console
    Flags parsing error: flag --connection_type=CLOUD_RESOURCE: value should be one of...
    ```

2.  Retrieve and copy the service account ID for use in a later step:
    
        bq show --connection PROJECT_ID.REGION.CONNECTION_ID
    
    The output is similar to the following:
    
    ```console
    name                          properties
    1234.REGION.CONNECTION_ID     {"serviceAccountId": "connection-1234-9u56h9@gcp-sa-bigquery-condel.iam.gserviceaccount.com"}
    ```

### Python

Before trying this sample, follow the Python setup instructions in the [BigQuery quickstart using client libraries](https://docs.cloud.google.com/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/bigquery/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](https://docs.cloud.google.com/bigquery/docs/authentication#client-libs) .

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

### Node.js

Before trying this sample, follow the Node.js setup instructions in the [BigQuery quickstart using client libraries](https://docs.cloud.google.com/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Node.js API reference documentation](https://googleapis.dev/nodejs/bigquery/latest/index.html) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](https://docs.cloud.google.com/bigquery/docs/authentication#client-libs) .

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

### Terraform

Use the [`google_bigquery_connection`](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/bigquery_connection) resource.

> **Note:** To create BigQuery objects using Terraform, you must enable the [Cloud Resource Manager API](https://docs.cloud.google.com/resource-manager/reference/rest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](https://docs.cloud.google.com/bigquery/docs/authentication#client-libs) .

The following example creates a Cloud resource connection named `my_cloud_resource_connection` in the `US` region:

```terraform
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
    
        export GOOGLE_CLOUD_PROJECT=PROJECT_ID
    
    Environment variables are overridden if you set explicit values in the Terraform configuration file.

## Prepare the directory

Each Terraform configuration file must have its own directory (also called a *root module* ).

1.  In [Cloud Shell](https://shell.cloud.google.com/) , create a directory and a new file within that directory. The filename must have the `.tf` extension—for example `main.tf` . In this tutorial, the file is referred to as `main.tf` .
    
        mkdir DIRECTORY && cd DIRECTORY && touch main.tf

2.  If you are following a tutorial, you can copy the sample code in each section or step.
    
    Copy the sample code into the newly created `main.tf` .
    
    Optionally, copy the code from GitHub. This is recommended when the Terraform snippet is part of an end-to-end solution.

3.  Review and modify the sample parameters to apply to your environment.

4.  Save your changes.

5.  Initialize Terraform. You only need to do this once per directory.
    
        terraform init
    
    Optionally, to use the latest Google provider version, include the `-upgrade` option:
    
        terraform init -upgrade

## Apply the changes

1.  Review the configuration and verify that the resources that Terraform is going to create or update match your expectations:
    
        terraform plan
    
    Make corrections to the configuration as necessary.

2.  Apply the Terraform configuration by running the following command and entering `yes` at the prompt:
    
        terraform apply
    
    Wait until Terraform displays the "Apply complete\!" message.

3.  [Open your Google Cloud project](https://console.cloud.google.com/) to view the results. In the Google Cloud console, navigate to your resources in the UI to make sure that Terraform has created or updated them.

> **Note:** Terraform samples typically assume that the required APIs are enabled in your Google Cloud project.

### Give the service account access

Grant the connection's service account the Agent Platform User and Storage Object Viewer roles. To grant the roles, follow these steps:

1.  Go to the **IAM & Admin** page.

2.  Click person\_add **Add** .
    
    The **Add principals** dialog opens.

3.  In the **New principals** field, enter the service account ID that you copied earlier.

4.  In the **Select a role** field, select **Vertex AI** , and then select **Agent Platform User** .

5.  Click **Add another role** .

6.  In the **Select a role** field, choose **Cloud Storage** , and then select **Storage Object Viewer** .

7.  Click **Save** .

## Summarize text and use the default output format

To summarize news articles, call the `AI.GENERATE` function with the article text as your prompt. By default, the output includes the generated summary text, the full response, and a status that is empty if the function returns successfully.

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, run the following query:
    
        WITH
        bbc_news AS (
          SELECT body FROM `bigquery-public-data.bbc_news.fulltext` LIMIT 5
        )
        SELECT AI.GENERATE(body, endpoint => 'gemini-2.5-pro') AS news FROM bbc_news;
    
    The output is similar to the following:
    
        +---------------------------------------------+------------------------------------+---------------+
        | news.result                                 | news.full_response                 | news.status   |
        +---------------------------------------------+------------------------------------+---------------+
        | This article presents a debate about the    | {"candidates":[{"avg_logprobs":    |               |
        | "digital divide" between rich and poor      | -0.31465074559841777, content":    |               |
        | nations. Here's a breakdown of the key...   | {"parts":[{"text":"This article... |               |
        +---------------------------------------------+------------------------------------+---------------+
        | This article discusses how advanced         | {"candidates":[{"avg_logprobs":    |               |
        | mapping technology is aiding humanitarian   | -0.21313422900091983,"content":    |               |
        | efforts in Darfur, Sudan. Here's a...       | {"parts":[{"text":"This article... |               |
        +---------------------------------------------+------------------------------------+---------------+
        | ...                                         | ...                                | ...           |
        +---------------------------------------------+------------------------------------+---------------+

## Summarize text and output structured results

Follow these steps to generate text using the `AI.GENERATE` function, and use the `AI.GENERATE` function's `output_schema` argument to format the output:

1.  In the Google Cloud console, go to the BigQuery page.

2.  In the query editor, run the following query:
    
        WITH bbc_news AS (
          SELECT
            body
          FROM
            `bigquery-public-data`.bbc_news.fulltext
          LIMIT 5
        )
        SELECT
          news.good_sentiment,
          news.summary
        FROM
          bbc_news,
          UNNEST(ARRAY[AI.GENERATE(body, endpoint => 'gemini-2.5-pro', output_schema  => 'summary STRING, good_sentiment BOOL')]) AS news;
    
    The output is similar to the following:
    
        +----------------+--------------------------------------------+
        | good_sentiment | summary                                    |
        +----------------+--------------------------------------------+
        | true           | A World Bank report suggests the digital   |
        |                | divide is rapidly closing due to increased |
        |                | access to technology in developing...      |
        +----------------+--------------------------------------------+
        | false          | A massive earthquake and subsequent        |
        |                | waves have devastated southern Asia, with  |
        |                | Sri Lanka, India, Indonesia, and...        |
        +----------------+--------------------------------------------+
        | ...            | ...                                        |
        +----------------+--------------------------------------------+

## Transcribe and translate video content

You can process multimedia files stored in Cloud Storage by using external object tables. The following steps show how to create an [object table](https://docs.cloud.google.com/bigquery/docs/object-table-introduction) for video files, transcribe the Japanese video content, and translate the text to English.

1.  In the Google Cloud console, go to the BigQuery page.

2.  In the query editor, run the following query to create the object table:
    
        CREATE OR REPLACE EXTERNAL TABLE `bqml_tutorial.video`
        WITH CONNECTION `us.test_connection`
        OPTIONS (
          object_metadata = 'SIMPLE',
          uris =
            ['gs://cloud-samples-data/generative-ai/video/*']);

3.  In the query editor, run the following query to transcribe and translate the `pixel8.mp4` file:
    
        SELECT
          AI.GENERATE(
            (OBJ.GET_ACCESS_URL(ref, 'r'), 'Transcribe the video in Japanese and then translate to English.'),
            endpoint => 'gemini-2.5-pro',
            output_schema => 'japanese_transcript STRING, english_translation STRING'
          ).* EXCEPT (full_response, status)
        FROM
          `bqml_tutorial.video`
        WHERE
          REGEXP_CONTAINS(uri, 'pixel8.mp4');
    
    The output is similar to the following:
    
        +--------------------------------------------+--------------------------------+
        | english_translation                        | japanese_transcript            |
        +--------------------------------------------+--------------------------------+
        | My name is Saeka Shimada. I'm a            | 島田 さえか です 。 東京 で フ     |
        | photographer in Tokyo. Tokyo has many      | ォトグラファー を し て い ま      |
        | faces. The city at night is totally...     | す 。 東京 に は いろんな 顔 が    |
        +--------------------------------------------+--------------------------------+

## Analyze audio file content

Follow these steps to create an object table over public audio content, and then analyze the content of the audio files.

1.  In the Google Cloud console, go to the BigQuery page.

2.  In the query editor, run the following query to create the object table:
    
        CREATE OR REPLACE EXTERNAL TABLE `bqml_tutorial.audio`
        WITH CONNECTION `us.test_connection`
        OPTIONS (
          object_metadata = 'SIMPLE',
          uris =
            ['gs://cloud-samples-data/generative-ai/audio/*']);

3.  In the query editor, run the following query to analyze the audio files:
    
        SELECT
          AI.GENERATE(
            (OBJ.GET_ACCESS_URL(ref, 'r'), 'Summarize the content of this audio file.'),
            endpoint => 'gemini-2.5-pro',
            output_schema => 'topic ARRAY<STRING>, summary STRING'
          ).* EXCEPT (full_response, status), uri
        FROM
          `bqml_tutorial.audio`;
    
    The results look similar to the following:
    
        +--------------------------------------------+-----------------------------------------------------------+
        | summary                                    | topic              | uri                                  |
        +--------------------------------------------+-----------------------------------------------------------+
        | The audio contains a distinctive 'beep'    | beep sound         | gs://cloud-samples-data/generativ... |
        | sound, followed by the characteristic      |                    |                                      |
        | sound of a large vehicle or bus backing..  |                    |                                      |
        +--------------------------------------------+--------------------+--------------------------------------+
        |                                            | vehicle backing up |                                      |
        |                                            +--------------------+                                      |
        |                                            | bus                |                                      |
        |                                            +--------------------+                                      |
        |                                            | alarm              |                                      |
        +--------------------------------------------+--------------------+--------------------------------------+
        | The speaker introduces themselves          | Introduction       | gs://cloud-samples-data/generativ... |
        | as Gemini and expresses their excitement   |                    |                                      |
        | and readiness to dive into something..     |                    |                                      |
        +--------------------------------------------+--------------------+--------------------------------------+
        |                                            | Readiness          |                                      |
        |                                            +--------------------+                                      |
        |                                            | Excitement         |                                      |
        |                                            +--------------------+                                      |
        |                                            | Collaboration      |                                      |
        +--------------------------------------------+--------------------+--------------------------------------+
        | ...                                        | ...                | ...                                  |
        +--------------------------------------------+--------------------+--------------------------------------+

## Clean up

To avoid incurring charges to your Google Cloud account for the resources used in this tutorial, either delete the project that contains the resources, or keep the project and delete the individual resources.

> **Caution** : Deleting a project has the following effects:
> 
>   - **Everything in the project is deleted.** If you used an existing project for the tasks in this document, when you delete it, you also delete any other work you've done in the project.
>   - **Custom project IDs are lost.** When you created this project, you might have created a custom project ID that you want to use in the future. To preserve the URLs that use the project ID, such as an `appspot.com` URL, delete selected resources inside the project instead of deleting the whole project.
> 
> If you plan to explore multiple architectures, tutorials, or quickstarts, reusing projects can help you avoid exceeding project quota limits.

In the Google Cloud console, go to the **Manage resources** page.

In the project list, select the project that you want to delete, and then click **Delete** .

In the dialog, type the project ID, and then click **Shut down** to delete the project.

### Delete individual resources

If you want to reuse the project, then delete the resources that you created for the tutorial.

### Console

1.  Go to the BigQuery page.

2.  Delete the `bqml_tutorial` dataset. Deleting the dataset also deletes the remote model.
    
    1.  In the **Explorer** pane, expand your project and click **Datasets** .
    
    2.  In the **Datasets** list, click the `bqml_tutorial` dataset.
    
    3.  In the details pane, click delete **Delete** .
    
    4.  In the **Delete dataset** dialog, click **Delete** .

3.  Delete the connection:
    
    1.  In the **Explorer** pane, expand your project and click **Connections** .
    
    2.  In the **Connection ID** list, click the connection that you created.
    
    3.  In the details pane, click delete **Delete** .
    
    4.  In the **Delete connection** dialog, enter `delete` to confirm deletion.
    
    5.  Click **Delete** .

### gcloud

1.  Delete the `bqml_tutorial` dataset and the remote model:
    
        bq rm --dataset --recursive bqml_tutorial

2.  Delete the connection.
    
        bq rm --connection PROJECT_ID.LOCATION.CONNECTION_ID
    
    Replace the following:
    
      - PROJECT\_ID : your Google Cloud project ID
      - LOCATION : the connection's location
      - CONNECTION\_ID : the connection ID

## What's next

  - Learn more about [generative AI in BigQuery](https://docs.cloud.google.com/bigquery/docs/generative-ai-overview) .
  - Learn more about [choosing a text generation function](https://docs.cloud.google.com/bigquery/docs/choose-text-generation-function) .
