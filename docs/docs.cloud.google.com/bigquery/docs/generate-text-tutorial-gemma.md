# Generate text by using a Gemma open model and the AI.GENERATE\_TEXT function

This tutorial shows you how to create a [remote model](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-open) that's based on the [Gemma model](/vertex-ai/generative-ai/docs/learn/models#gemma-models) , and then how to use that model with the [`  AI.GENERATE_TEXT  ` function](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate-text) to extract keywords and perform sentiment analysis on movie reviews from the `  bigquery-public-data.imdb.reviews  ` public table.

## Required permissions

To run this tutorial, you need the following Identity and Access Management (IAM) roles:

  - Create and use BigQuery datasets, connections, and models: BigQuery Admin ( `  roles/bigquery.admin  ` ).
  - Grant permissions to the connection's service account: Project IAM Admin ( `  roles/resourcemanager.projectIamAdmin  ` ).
  - Deploy and undeploy models in Vertex AI: Vertex AI Administrator ( `  roles/aiplatform.admin  ` ).

These predefined roles contain the permissions required to perform the tasks in this document. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

  - Create a dataset: `  bigquery.datasets.create  `
  - Create, delegate, and use a connection: `  bigquery.connections.*  `
  - Set the default connection: `  bigquery.config.*  `
  - Set service account permissions: `  resourcemanager.projects.getIamPolicy  ` and `  resourcemanager.projects.setIamPolicy  `
  - Deploy and undeploy a Vertex AI model:
      - `  aiplatform.endpoints.deploy  `
      - `  aiplatform.endpoints.undeploy  `
  - Create a model and run inference:
      - `  bigquery.jobs.create  `
      - `  bigquery.models.create  `
      - `  bigquery.models.getData  `
      - `  bigquery.models.updateData  `
      - `  bigquery.models.updateMetadata  `

You might also be able to get these permissions with [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

## Costs

In this document, you use the following billable components of Google Cloud:

  - **BigQuery ML** : You incur costs for the data that you process in BigQuery.
  - **Vertex AI** : You incur costs for calls to the Vertex AI model that's represented by the remote model.

To generate a cost estimate based on your projected usage, use the [pricing calculator](/products/calculator) .

New Google Cloud users might be eligible for a [free trial](/free) .

For more information about BigQuery pricing, see [BigQuery pricing](https://cloud.google.com/bigquery/pricing) in the BigQuery documentation.

Open models that you deploy to Vertex AI are charged per machine-hour. This means billing starts as soon as the endpoint is fully set up, and continues until you un-deploy it. For more information about Vertex AI pricing, see the [Vertex AI pricing](https://cloud.google.com/vertex-ai/pricing#prediction-prices) page.

## Before you begin

1.  In the Google Cloud console, on the project selector page, select or create a Google Cloud project.
    
    **Roles required to select or create a project**
    
      - **Select a project** : Selecting a project doesn't require a specific IAM role—you can select any project that you've been granted a role on.
      - **Create a project** : To create a project, you need the Project Creator role ( `  roles/resourcemanager.projectCreator  ` ), which contains the `  resourcemanager.projects.create  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .
    
    **Note** : If you don't plan to keep the resources that you create in this procedure, create a project instead of selecting an existing project. After you finish these steps, you can delete the project, removing all resources associated with the project.

2.  [Verify that billing is enabled for your Google Cloud project](/billing/docs/how-to/verify-billing-enabled#confirm_billing_is_enabled_on_a_project) .

3.  Enable the BigQuery, BigQuery Connection, and Vertex AI APIs.
    
    **Roles required to enable APIs**
    
    To enable APIs, you need the Service Usage Admin IAM role ( `  roles/serviceusage.serviceUsageAdmin  ` ), which contains the `  serviceusage.services.enable  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .

## Create a dataset

Create a BigQuery dataset to store your ML model.

### Console

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the **Explorer** pane, click your project name.

3.  Click more\_vert **View actions \> Create dataset**

4.  On the **Create dataset** page, do the following:
    
      - For **Dataset ID** , enter `  bqml_tutorial  ` .
    
      - For **Location type** , select **Multi-region** , and then select **US (multiple regions in United States)** .
    
      - Leave the remaining default settings as they are, and click **Create dataset** .

### bq

To create a new dataset, use the [`  bq mk  `](/bigquery/docs/reference/bq-cli-reference#mk-dataset) command with the `  --location  ` flag. For a full list of possible parameters, see the [`  bq mk --dataset  ` command](/bigquery/docs/reference/bq-cli-reference#mk-dataset) reference.

1.  Create a dataset named `  bqml_tutorial  ` with the data location set to `  US  ` and a description of `  BigQuery ML tutorial dataset  ` :
    
    ``` text
    bq --location=US mk -d \
     --description "BigQuery ML tutorial dataset." \
     bqml_tutorial
    ```
    
    Instead of using the `  --dataset  ` flag, the command uses the `  -d  ` shortcut. If you omit `  -d  ` and `  --dataset  ` , the command defaults to creating a dataset.

2.  Confirm that the dataset was created:
    
    ``` text
    bq ls
    ```

### API

Call the [`  datasets.insert  `](/bigquery/docs/reference/rest/v2/datasets/insert) method with a defined [dataset resource](/bigquery/docs/reference/rest/v2/datasets) .

``` text
{
  "datasetReference": {
     "datasetId": "bqml_tutorial"
  }
}
```

### BigQuery DataFrames

Before trying this sample, follow the BigQuery DataFrames setup instructions in the [BigQuery quickstart using BigQuery DataFrames](/bigquery/docs/dataframes-quickstart) . For more information, see the [BigQuery DataFrames reference documentation](/python/docs/reference/bigframes/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up ADC for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
import google.cloud.bigquery

bqclient = google.cloud.bigquery.Client()
bqclient.create_dataset("bqml_tutorial", exists_ok=True)
```

## Create the remote model

Create a remote model that represents a hosted Vertex AI model:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, run the following statement:

<!-- end list -->

``` text
CREATE OR REPLACE MODEL `bqml_tutorial.gemma_model`
  REMOTE WITH CONNECTION DEFAULT
  OPTIONS (
    MODEL_GARDEN_MODEL_NAME = 'publishers/google/models/gemma3@gemma-3-270m-it',
    MACHINE_TYPE = 'g2-standard-12'
  );
```

The query takes up to 20 minutes to complete, after which the `  gemma_model  ` model appears in the `  bqml_tutorial  ` dataset in the **Explorer** pane. Because the query uses a `  CREATE MODEL  ` statement to create a model, there are no query results.

## Perform keyword extraction

Perform keyword extraction on [IMDB](https://www.imdb.com/) movie reviews by using the remote model and the `  AI.GENERATE_TEXT  ` function:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement to perform keyword extraction on 10 movie reviews:
    
    ``` text
    -- This function takes your instruction and wraps it with chat template for
    -- better output quality.
    -- This is usually the recommended way when using Gemma instruction-tuned models.
    CREATE TEMP FUNCTION FormatPromptWithChatTemplate(user_instruction STRING) AS (
      CONCAT(
        '<start_of_turn>user\n',
        user_instruction,
        '<end_of_turn>\n<start_of_turn>model\n'
      )
    );
    
    SELECT
      *
    FROM
      AI.GENERATE_TEXT(
        MODEL `bqml_tutorial.gemma_model`,
        (
          SELECT
            FormatPromptWithChatTemplate(
              'Extract the key words from the movie review below: ' || review)
              AS prompt,
            *
          FROM
            `bigquery-public-data.imdb.reviews`
          LIMIT 10
        ),
        STRUCT(
          0.2 AS temperature,
          100 AS max_output_tokens));
    ```
    
    For more information about using chat templates with Gemma, see [Gemma formatting and system instructions](https://ai.google.dev/gemma/docs/core/prompt-structure) .
    
    The output is similar to the following, with non-generated columns omitted for clarity:
    
    ``` text
    +----------------------------------------------+-------------------------+-----------------------------+-----+
    | result                                       | status                  | prompt                      | ... |
    +----------------------------------------------+-------------------------------------------------------+-----+
    | Here are some key words from the             |                         | <start_of_turn>user         |     |
    | movie review: * **Romance:**                 |                         | Extract the key words from  |     |
    | "romantic tryst," "elope" * **Comedy:**      |                         | the movie review below:     |     |
    | "Contrived Comedy" * **Burglary:**           |                         | Linda Arvidson (as Jennie)  |     |
    | "burglar," "rob," "booty" * **Chase:**       |                         | and Harry Solter (as Frank) |     |
    | "chases," "escape" * **Director:** "D.W.     |                         | are enjoying a romantic     |     |
    | Griffith" * **Actors:** "Linda Arvidson,"... |                         | tryst, when in walks her... |     |
    +----------------------------------------------+-------------------------+-----------------------------+-----+
    | Here are some key words from the             |                         | <start_of_turn>user         |     |
    | movie review: * **Elderbush Gilch:** The     |                         | Extract the key words from  |     |
    | name of the movie being reviewed. *          |                         | the movie review below:     |     |
    | **Disappointment:** The reviewer's           |                         | This is the second addition |     |
    | overall feeling about the film. *            |                         | to Frank Baum's personally  |     |
    | **Dim-witted:** Describes the story          |                         | produced trilogy of Oz      |     |
    | line negatively. * **Moronic, sadistic,...   |                         | films. It's essentially ... |     |
    +----------------------------------------------+-------------------------+-----------------------------+-----+
    ```
    
    The results include the following columns:
    
      - `  result  ` : the generated text.
      - `  status  ` : the API response status for the corresponding row. If the operation was successful, this value is empty.
      - `  prompt  ` : the prompt that is used for the sentiment analysis.
      - All of the columns from the `  bigquery-public-data.imdb.reviews  ` table.

## Perform sentiment analysis

Perform sentiment analysis on [IMDB](https://www.imdb.com/) movie reviews by using the remote model and the `  AI.GENERATE_TEXT  ` function:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, run the following statement to perform sentiment analysis on 10 movie reviews:
    
    ``` text
    -- This function takes your instruction and wraps it with chat template for
    -- better output quality.
    -- This is usually the recommended way when using Gemma instruction-tuned models.
    CREATE TEMP FUNCTION FormatPromptWithChatTemplate(user_instruction STRING) AS (
      CONCAT(
        '<start_of_turn>user\n',
        user_instruction,
        '<end_of_turn>\n<start_of_turn>model\n'
      )
    );
    
    SELECT
      *
    FROM
      AI.GENERATE_TEXT(
        MODEL `bqml_tutorial.gemma_model`,
        (
          SELECT
            FormatPromptWithChatTemplate(
              'Analyze the sentiment of the following movie review and classify it as either POSITIVE or NEGATIVE. \nMovie Review: '
              || review) AS prompt,
            *
          FROM
            `bigquery-public-data.imdb.reviews`
          LIMIT 10
        ),
        STRUCT(
          0.2 AS temperature,
          128 AS max_output_tokens));
    ```
    
    For more information about using chat templates with Gemma, see [Gemma formatting and system instructions](https://ai.google.dev/gemma/docs/core/prompt-structure) .
    
    The output is similar to the following, with non-generated columns omitted for clarity:
    
    ``` text
    +-----------------------------+-------------------------+-----------------------------+-----+
    | result                      | status                  | prompt                      | ... |
    +-----------------------------+-------------------------------------------------------+-----+
    | **NEGATIVE**                |                         | <start_of_turn>user         |     |
    |                             |                         | Analyze the sentiment of    |     |
    |                             |                         | movie review and classify   |     |
    |                             |                         | it as either POSITIVE or    |     |
    |                             |                         | NEGATIVE. Movie Review:     |     |
    |                             |                         | Although Charlie Chaplin    |     |
    |                             |                         | made some great short       |     |
    |                             |                         | comedies in the late...     |     |
    +-----------------------------+-------------------------+-----------------------------+-----+
    | **NEGATIVE**                |                         | <start_of_turn>user         |     |
    |                             |                         | Analyze the sentiment of    |     |
    |                             |                         | movie review and classify   |     |
    |                             |                         | it as either POSITIVE or    |     |
    |                             |                         | NEGATIVE. Movie Review:     |     |
    |                             |                         | Opulent sets and sumptuous  |     |
    |                             |                         | costumes well photographed  |     |
    |                             |                         | by Theodor Sparkuhl, and... |     |
    +-----------------------------+-------------------------+-----------------------------+-----+
    ```
    
    The results include the same columns documented for [Perform keyword extraction](#perform_keyword_extraction) .

## Undeploy model

If you choose not to [delete your project as recommended](#clean_up) , you must undeploy the Gemma model in Vertex AI to avoid continued billing for it. BigQuery automatically undeploys the model after a specified period of idleness (6.5 hours by default). Alternatively, you can immediately undeploy the model by using the [`  ALTER MODEL  ` statement](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-alter-model) , as shown in the following example:

``` text
ALTER MODEL `bqml_tutorial.gemma_model`
SET OPTIONS (deploy_model = false);
```

For more information, see [Automatic or immediate open model undeployment](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-open#managed-model-undeployment) .

## Clean up

**Caution** : Deleting a project has the following effects:

  - **Everything in the project is deleted.** If you used an existing project for the tasks in this document, when you delete it, you also delete any other work you've done in the project.
  - **Custom project IDs are lost.** When you created this project, you might have created a custom project ID that you want to use in the future. To preserve the URLs that use the project ID, such as an `  appspot.com  ` URL, delete selected resources inside the project instead of deleting the whole project.

If you plan to explore multiple architectures, tutorials, or quickstarts, reusing projects can help you avoid exceeding project quota limits.

In the Google Cloud console, go to the **Manage resources** page.

In the project list, select the project that you want to delete, and then click **Delete** .

In the dialog, type the project ID, and then click **Shut down** to delete the project.
