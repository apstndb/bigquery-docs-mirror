---
name: documents/docs.cloud.google.com/bigquery/docs/rag-pipeline-pdf
uri: https://docs.cloud.google.com/bigquery/docs/rag-pipeline-pdf
title: Parse PDFs in a retrieval-augmented generation pipeline
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

This tutorial guides you through the process of creating a retrieval-augmented generation (RAG) pipeline based on parsed PDF content.

PDF files, such as financial documents, can be challenging to use in RAG pipelines because of their complex structure and mix of text, figures, and tables. This tutorial shows you how to use the [`ML.PROCESS_DOCUEMNT` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-parse-document) in combination with Document AI's layout parser to build a RAG pipeline based on key information extracted from a PDF file.

## Objectives

This tutorial covers the following tasks:

  - Creating a [Cloud resource connection](https://docs.cloud.google.com/bigquery/docs/create-cloud-resource-connection) so that you can connect to Cloud Storage and Vertex AI from BigQuery.
  - Create a Cloud Storage bucket and upload a sample PDF file.
  - Creating an [object table](https://docs.cloud.google.com/bigquery/docs/object-table-introduction) over the PDF file to make the PDF file available in BigQuery.
  - [Create a Document AI processor](https://docs.cloud.google.com/document-ai/docs/create-processor#create-processor) that you can use to parse the PDF file.
  - Creating a [remote model](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-service) that lets you use the Document AI API to access the document processor from BigQuery.
  - Using the remote model with the [`ML.PROCESS_DOCUMENT` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-process-document) to parse the PDF contents into chunks and then write that content to a BigQuery table.
  - Extracting PDF content from the JSON data returned by the `ML.PROCESS_DOCUMENT` function, and then writing that content to a BigQuery table.
  - Generate embeddings from the parsed PDF content, and then write those embeddings to a BigQuery table. Embeddings are numerical representations of the PDF content that enable you to perform semantic search and retrieval on the PDF content.
  - Use the [`VECTOR_SEARCH` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/search_functions#vector_search) on the embeddings to identify semantically similar PDF content.
  - Perform retrieval-augmented generation (RAG) by using the [`AI.GENERATE` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate) to generate text, using vector search results to augment the prompt input and improve results.

## Costs

In this document, you use the following billable components of Google Cloud:

  - [BigQuery](https://cloud.google.com/bigquery/pricing) : You incur costs for the data that you process in BigQuery.
  - [Gemini Enterprise Agent Platform](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) : You incur costs for calls to Agent Platform models.
  - [Document AI](https://cloud.google.com/document-ai/pricing) : You incur costs for calls to the Document AI API.
  - [Cloud Storage](https://cloud.google.com/storage/pricing) : You incur costs for object storage in Cloud Storage.

To generate a cost estimate based on your projected usage, use the [pricing calculator](https://docs.cloud.google.com/products/calculator) .

New Google Cloud users might be eligible for a [free trial](https://docs.cloud.google.com/free) .

When you finish the tasks that are described in this document, you can avoid continued billing by deleting the resources that you created. For more information, see [Clean up](https://docs.cloud.google.com/bigquery/docs/rag-pipeline-pdf#clean-up) .

## Before you begin

### Console

1.  Make sure that you have the following role or roles on the project: **Storage Admin** , **Document AI Editor** , **BigQuery Admin** , **Project IAM Admin**
    
    #### Check for the roles
    
    1.  In the Google Cloud console, go to the **IAM** page.
    
    2.  Select the project.
    
    3.  In the **Principal** column, find all rows that identify you or a group that you're included in. To learn which groups you're included in, contact your administrator.
    
    4.  For all rows that specify or include you, check the **Role** column to see whether the list of roles includes the required roles.
    
    #### Grant the roles
    
    1.  In the Google Cloud console, go to the **IAM** page.
    
    2.  Select the project.
    
    3.  Click person\_add **Grant access** .
    
    4.  In the **New principals** field, enter your user identifier. This is typically the email address for a Google Account.
    
    5.  Click **Select a role** , then search for the role.
    
    6.  To grant additional roles, click add **Add another role** and add each additional role.
    
    7.  Click **Save** .

### gcloud

1.  Grant roles to your user account. Run the following command once for each of the following IAM roles: `roles/storage.admin, roles/documentai.editor, roles/bigquery.admin, roles/resourcemanager.projectIamAdmin`
    
        gcloud projects add-iam-policy-binding PROJECT_ID --member="user:USER_IDENTIFIER" --role=ROLE
    
    Replace the following:
    
      - `  PROJECT_ID  ` : Your project ID.
      - `  USER_IDENTIFIER  ` : The identifier for your user account. For example, `myemail@example.com` .
      - `  ROLE  ` : The IAM role that you grant to your user account.

## Create a dataset

Create a BigQuery dataset to store your ML model.

### Console

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the **Explorer** pane, click your project name.

3.  Click more\_vert **View actions \> Create dataset**

4.  On the **Create dataset** page, do the following:
    
      - For **Dataset ID** , enter `bqml_tutorial` .
    
      - For **Location type** , select **Multi-region** , and then select **US** .
    
      - Leave the remaining default settings as they are, and click **Create dataset** .

### bq

To create a new dataset, use the [`bq mk --dataset` command](https://docs.cloud.google.com/bigquery/docs/reference/bq-cli-reference#mk-dataset) .

1.  Create a dataset named `bqml_tutorial` with the data location set to `US` .
    
        bq mk --dataset \
          --location=US \
          --description "BigQuery ML tutorial dataset." \
          bqml_tutorial

2.  Confirm that the dataset was created:
    
        bq ls

### API

Call the [`datasets.insert`](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/datasets/insert) method with a defined [dataset resource](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/datasets) .

    {
      "datasetReference": {
         "datasetId": "bqml_tutorial"
      }
    }

## Create a connection

Create a [Cloud resource connection](https://docs.cloud.google.com/bigquery/docs/create-cloud-resource-connection) and get the connection's service account. Create the connection in the same [location](https://docs.cloud.google.com/bigquery/docs/locations) .

You can skip this step if you either have a default connection configured, or you have the BigQuery Admin role.

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

## Grant access to the service account

Select one of the following options:

### Console

1.  Go to the **IAM & Admin** page.

2.  Click person\_add **Grant Access** .
    
    The **Add principals** dialog opens.

3.  In the **New principals** field, enter the service account ID that you copied earlier.

4.  In the **Select a role** field, select **Document AI** , and then select **Document AI Viewer** .

5.  Click **Add another role** .

6.  In the **Select a role** field, select **Cloud Storage** , and then select **Storage Object Viewer** .

7.  Click **Add another role** .

8.  In the **Select a role** field, select **Vertex AI** , and then select **Vertex AI User** .

9.  Click **Save** .

### gcloud

Use the [`gcloud projects add-iam-policy-binding` command](https://docs.cloud.google.com/sdk/gcloud/reference/projects/add-iam-policy-binding) :

``` 
gcloud projects add-iam-policy-binding 'PROJECT_NUMBER' --member='serviceAccount:MEMBER' --role='roles/documentai.viewer' --condition=None
gcloud projects add-iam-policy-binding 'PROJECT_NUMBER' --member='serviceAccount:MEMBER' --role='roles/storage.objectViewer' --condition=None
gcloud projects add-iam-policy-binding 'PROJECT_NUMBER' --member='serviceAccount:MEMBER' --role='roles/aiplatform.user' --condition=None
 
```

Replace the following:

  - `  PROJECT_NUMBER  ` : your project number.
  - `  MEMBER  ` : the service account ID that you copied earlier.

## Upload the sample PDF to Cloud Storage

To upload the sample PDF to Cloud Storage, follow these steps:

1.  Download the `scf23.pdf` sample PDF by going to <https://www.federalreserve.gov/publications/files/scf23.pdf> and clicking download download .
2.  [Create a Cloud Storage bucket](https://docs.cloud.google.com/storage/docs/creating-buckets) .
3.  [Upload](https://docs.cloud.google.com/storage/docs/uploading-objects) the `scf23.pdf` file to the bucket.

## Create an object table

Create an object table over the PDF file in Cloud Storage:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, run the following statement:
    
        CREATE OR REPLACE EXTERNAL TABLE `bqml_tutorial.pdf`
        WITH CONNECTION `LOCATION.CONNECTION_ID`
        OPTIONS(
          object_metadata = 'SIMPLE',
          uris = ['gs://BUCKET/scf23.pdf']);
    
    Replace the following:
    
      - `  LOCATION  ` : the connection location.
    
      - `  CONNECTION_ID  ` : the ID of your BigQuery connection.
        
        When you [view the connection details](https://docs.cloud.google.com/bigquery/docs/working-with-connections#view-connections) in the Google Cloud console, the `  CONNECTION_ID  ` is the value in the last section of the fully qualified connection ID that is shown in **Connection ID** , for example ` projects/myproject/locations/connection_location/connections/ myconnection  ` .
    
      - `  BUCKET  ` : the Cloud Storage bucket containing the `scf23.pdf` file. The full `uri` option value should look similar to `['gs://mybucket/scf23.pdf']` .

## Create a document processor

[Create a document processor](https://docs.cloud.google.com/document-ai/docs/create-processor#create-processor) based on the [layout parser processor](https://docs.cloud.google.com/document-ai/docs/layout-parse-chunk) in the `us` multi-region. Copy the prediction endpoint from the **Processor details** page to use in the next section.

## Create the remote model for the document processor

Create a remote model to access the Document AI processor:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, run the following statement:
    
        CREATE OR REPLACE MODEL `bqml_tutorial.parser_model`
        REMOTE WITH CONNECTION `LOCATION.CONNECTION_ID`
          OPTIONS(remote_service_type = 'CLOUD_AI_DOCUMENT_V1', document_processor = 'PROCESSOR_ID');
    
    Replace the following:
    
      - `  LOCATION  ` : the connection location.
    
      - `  CONNECTION_ID  ` : the ID of your BigQuery connection.
        
        When you [view the connection details](https://docs.cloud.google.com/bigquery/docs/working-with-connections#view-connections) in the Google Cloud console, the `  CONNECTION_ID  ` is the value in the last section of the fully qualified connection ID that is shown in **Connection ID** , for example ` projects/myproject/locations/connection_location/connections/ myconnection  ` .
    
      - `  PROCESSOR_ID  ` : the document processor ID. To find this value, [view the processor details](https://docs.cloud.google.com/document-ai/docs/create-processor#get-processor) , and then look at the **ID** row in the **Basic Information** section.

## Parse the PDF file into chunks

Use the document processor with the `ML.PROCESS_DOCUMENT` function to parse the PDF file into chunks, and then write that content to a table. The `ML.PROCESS_DOCUMENT` function returns the PDF chunks in JSON format.

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, run the following statement:
    
        CREATE or REPLACE TABLE bqml_tutorial.chunked_pdf AS (  SELECT * FROM ML.PROCESS_DOCUMENT(  MODEL bqml_tutorial.parser_model,  TABLE bqml_tutorial.pdf,  PROCESS_OPTIONS => (JSON '{"layout_config": {"chunking_config": {"chunk_size": 250}}}')  ));

## Parse the PDF chunk data into separate columns

Extract the PDF content and metadata information from the JSON data returned by the `ML.PROCESS_DOCUMENT` function, and then write that content to a table:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, run the following statement to parse the PDF content:
    
        CREATE OR REPLACE TABLE bqml_tutorial.parsed_pdf AS (SELECT  uri,  JSON_EXTRACT_SCALAR(json , '$.chunkId') AS id,  JSON_EXTRACT_SCALAR(json , '$.content') AS content,  JSON_EXTRACT_SCALAR(json , '$.pageFooters[0].text') AS page_footers_text,  JSON_EXTRACT_SCALAR(json , '$.pageSpan.pageStart') AS page_span_start,  JSON_EXTRACT_SCALAR(json , '$.pageSpan.pageEnd') AS page_span_endFROM bqml_tutorial.chunked_pdf, UNNEST(JSON_EXTRACT_ARRAY(ml_process_document_result.chunkedDocument.chunks, '$')) json);

3.  In the query editor, run the following statement to view a subset of the parsed PDF content:
    
        SELECT *
        FROM `bqml_tutorial.parsed_pdf`
        ORDER BY id
        LIMIT 5;
    
    The output is similar to the following:
    
    ``` 
    +-----------------------------------+------+------------------------------------------------------------------------------------------------------+-------------------+-----------------+---------------+
    |                uri                |  id  |                                                 content                                              | page_footers_text | page_span_start | page_span_end |
    +-----------------------------------+------+------------------------------------------------------------------------------------------------------+-------------------+-----------------+---------------+
    | gs://mybucket/scf23.pdf           | c1   | •BOARD OF OF FEDERAL GOVERN NOR RESERVE SYSTEM RESEARCH & ANALYSIS                                   | NULL              | 1               | 1             |
    | gs://mybucket/scf23.pdf           | c10  | • In 2022, 20 percent of all families, 14 percent of families in the bottom half of the usual ...    | NULL              | 8               | 9             |
    | gs://mybucket/scf23.pdf           | c100 | The SCF asks multiple questions intended to capture whether families are credit constrained, ...     | NULL              | 48              | 48            |
    | gs://mybucket/scf23.pdf           | c101 | Bankruptcy behavior over the past five years is based on a series of retrospective questions ...     | NULL              | 48              | 48            |
    | gs://mybucket/scf23.pdf           | c102 | # Percentiles of the Distributions of Income and Net Worth                                           | NULL              | 48              | 49            |
    +-----------------------------------+------+------------------------------------------------------------------------------------------------------+-------------------+-----------------+---------------+
     
    ```

## Generate embeddings

Generate embeddings for the parsed PDF content and then write them to a table:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, run the following statement:
    
        CREATE OR REPLACE TABLE `bqml_tutorial.embeddings` AS (
          SELECT *, AI.EMBED(content, endpoint => 'text-embedding-005').result AS embedding
          FROM bqml_tutorial.parsed_pdf
        );

## Run a vector search

Run a vector search against the parsed PDF content.

The following query takes text input, creates an embedding for that input using the `AI.EMBED` function, and then uses the `VECTOR_SEARCH` function to match the input embedding with the most similar PDF content embeddings. The results are the top ten PDF chunks that are most related to changes in family net worth.

1.  Go to the **BigQuery** page.

2.  In the query editor, run the following SQL statement:
    
        SELECT
          distance,
          base.id AS chunk_id,
          base.page_span_start AS start_page,
          base.page_span_end AS end_page,
          base.content
        FROM
          VECTOR_SEARCH(
            TABLE `bqml_tutorial.embeddings`,
            'embedding',
            query_value =>
              AI.EMBED(
                'Did the typical family net worth increase? If so, by how much?',
                endpoint => 'text-embedding-005').result,
            top_k => 3,
            OPTIONS => '{"fraction_lists_to_search": 0.01}')
        ORDER BY distance DESC;
    
    The output is similar to the following:
    
        +----------+----------+------------+----------+-----------------------------------+
        | distance | chunk_id | start_page | end_page | content                           |
        +----------+----------+------------+----------+-----------------------------------+
        | 0.645685 | 26       | 17         | 18       | 18 Between the first quarter of   |
        |          |          |            |          | 2019 and the first quarter of...  |
        +----------+----------+------------+----------+-----------------------------------+
        | 0.602665 | 30       | 19         | 21       | ## Net Worth by Family            |
        |          |          |            |          | Characteristics...                |
        +----------+----------+------------+----------+-----------------------------------+
        | 0.599438 | 24       | 17         | 21       | # Net Worth                       |
        |          |          |            |          | The net improvements in...        |
        +----------+----------+------------+----------+-----------------------------------+

## Generate text augmented by vector search results

Perform a vector search on the embeddings to identify semantically similar PDF content, and then use the `AI.GENERATE` function with the vector search results to augment the prompt input and improve the text generation results. In this case, the query uses information from the PDF chunks to answer a question about the change in family net worth over the past decade.

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, run the following statement:
    
        SELECT
          AI.GENERATE(
            CONCAT('Did the typical family net worth change? How does this compare the SCF survey a decade earlier? Be concise and use the following context:',
                    STRING_AGG(FORMAT("context: %s", base.content), ',\n')
            ),
            endpoint => 'gemini-2.5-pro'
          ).result AS response
        FROM
          VECTOR_SEARCH(
            TABLE `bqml_tutorial.embeddings`,
            'embedding',
            query_value =>
              AI.EMBED(
                'Did the typical family net worth increase? If so, by how much?',
                endpoint => 'text-embedding-005').result,
            top_k => 3,
            OPTIONS => '{"fraction_lists_to_search": 0.01}')
    
    The output is similar to the following:
    
        +-------------------------------------------------------------------------+
        | response                                                                |
        +-------------------------------------------------------------------------+
        | Yes, the typical family net worth changed significantly.                |
        |                                                                         |
        | Real median net worth surged 37% between the 2019 and 2022 SCF surveys. |
        | This contrasts sharply with a decade earlier (2010-2013), when real     |
        | median net worth decreased 2%.                                          |
        +-------------------------------------------------------------------------+

## Clean up

To avoid incurring charges to your Google Cloud account for the resources used in this tutorial, either delete the project that contains the resources, or keep the project and delete the individual resources.

### Delete the project

> **Caution** : Deleting a project has the following effects:
> 
>   - **Everything in the project is deleted.** If you used an existing project for the tasks in this document, when you delete it, you also delete any other work you've done in the project.
>   - **Custom project IDs are lost.** When you created this project, you might have created a custom project ID that you want to use in the future. To preserve the URLs that use the project ID, such as an `appspot.com` URL, delete selected resources inside the project instead of deleting the whole project.
> 
> If you plan to explore multiple architectures, tutorials, or quickstarts, reusing projects can help you avoid exceeding project quota limits.

Delete a Google Cloud project:

    gcloud projects delete PROJECT_ID

## What's next

  - Learn more about the [`ML.PROCESS_DOCUMENT` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-process-document) .
  - Learn more about performing [semantic search and RAG](https://docs.cloud.google.com/bigquery/docs/vector-index-text-search-tutorial) .
