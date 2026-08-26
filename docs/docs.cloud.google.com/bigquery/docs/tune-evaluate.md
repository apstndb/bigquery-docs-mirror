---
name: documents/docs.cloud.google.com/bigquery/docs/tune-evaluate
uri: https://docs.cloud.google.com/bigquery/docs/tune-evaluate
title: Use tuning and evaluation to improve model performance
description: Shows how to use supervised tuning and ML.EVALUATE to improve and measure remote model performance.
data_source: docs.cloud.google.com
---

This tutorial shows you how to tune a model that enriches a given sentence by providing more precise wording or adding qualifiers without changing the overall meaning. You create a [remote model](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model) that references a [Gemini Enterprise Agent Platform model](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/learn/models#gemini-models) , use [supervised tuning](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-tuned#supervised_tuning) , and then evaluate the tuned model with the [`ML.EVALUATE` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-evaluate) .

Tuning helps you customize the hosted Agent Platform model, such as when the expected behavior is difficult to define in a prompt, or when prompts don't consistently produce expected results. Supervised tuning also influences the model in the following ways:

  - Guides the model to return specific response styles—for example, being more concise or more verbose.
  - Teaches the model new behaviors—for example, responding to prompts as a specific persona.
  - Causes the model to update itself with new information.

In this tutorial, the goal is to have the model generate text whose style and content conform as closely as possible to the provided ground truth content.

## Objectives

  - Create a dataset.
  - Import training and evaluation data into tables.
  - Create a baseline model.
  - Evaluate baseline model performance.
  - Create a tuned model.
  - Evaluate tuned model performance.

## Costs

In this document, you use the following billable components of Google Cloud:

  - **BigQuery.** You incur costs for the queries that you run in BigQuery.
  - **BigQuery ML.** You incur costs for the model that you create and the processing that you perform in BigQuery ML.
  - **Gemini Enterprise Agent Platform.** You incur costs for calls to and supervised tuning of the Gemini model.

To generate a cost estimate based on your projected usage, use the [pricing calculator](https://docs.cloud.google.com/products/calculator) .

New Google Cloud users might be eligible for a [free trial](https://docs.cloud.google.com/free) .

For more information, see the following resources:

  - [BigQuery storage pricing](https://cloud.google.com/bigquery/pricing#storage)
  - [BigQuery ML pricing](https://cloud.google.com/bigquery/pricing#bqml)
  - [Agent Platform pricing](https://cloud.google.com/products/gemini-enterprise-agent-platform/pricing)

## Before you begin

To run this tutorial, you need the following Identity and Access Management (IAM) roles:

  - Create and use BigQuery datasets, connections, and models: BigQuery Admin ( `roles/bigquery.admin` ).
  - Grant permissions to the connection's service account: Project IAM Admin ( `roles/resourcemanager.projectIamAdmin` ).

These predefined roles contain the permissions that are required to perform the tasks in this document. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

  - Create a dataset: `bigquery.datasets.create`
  - Create a table: `bigquery.tables.create`
  - Create, delegate, and use a connection: `bigquery.connections.*`
  - Set the default connection: `bigquery.config.*`
  - Set service account permissions: `resourcemanager.projects.getIamPolicy` and `resourcemanager.projects.setIamPolicy`
  - Create a model and run inference:
      - `bigquery.jobs.create`
      - `bigquery.models.create`
      - `bigquery.models.getData`
      - `bigquery.models.updateData`
      - `bigquery.models.updateMetadata`

You might also be able to get these permissions with [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

1.  In the Google Cloud console, on the project selector page, select or create a Google Cloud project.
    
    **Roles required to select or create a project**
    
      - **Select a project** : Selecting a project doesn't require a specific IAM role—you can select any project that you've been granted a role on.
      - **Create a project** : To create a project, you need the Project Creator role ( `roles/resourcemanager.projectCreator` ), which contains the `resourcemanager.projects.create` permission. [Learn how to grant roles](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .
    
    > **Note** : If you don't plan to keep the resources that you create in this procedure, create a project instead of selecting an existing project. After you finish these steps, you can delete the project, removing all resources associated with the project.

2.  [Verify that billing is enabled for your Google Cloud project](https://docs.cloud.google.com/billing/docs/how-to/verify-billing-enabled#confirm_billing_is_enabled_on_a_project) .

3.  Enable the BigQuery, BigQuery Connection, Agent Platform API, and Compute Engine APIs.
    
    **Roles required to enable APIs**
    
    To enable APIs, you need the `serviceusage.services.enable` permission. If you created the project, then you likely already have this permission through the Owner role ( `roles/owner` ). Otherwise, you can get this permission through the Service Usage Admin role ( `roles/serviceusage.serviceUsageAdmin` ). [Learn how to grant roles](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

## Create a dataset

To create a BigQuery dataset, select one of the following options:

### Console

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :
    
    ![Highlighted button for the Explorer pane.](https://docs.cloud.google.com/static/bigquery/images/explorer-tab.png)
    
    If you don't see the left pane, click last\_page **Expand left pane** to open the pane.

3.  In **Explorer** , expand your project, and then click **Datasets** .

4.  On the **Datasets** page, click add **Create dataset** .

5.  In the **Create dataset** pane, do the following:
    
      - For **Dataset ID** , enter `bqml_tutorial` .
    
      - For **Data location** , select **US** .
    
    Leave the remaining default settings as they are.

6.  Click **Create dataset** .

### bq

To create a new dataset, use the [`bq mk --dataset` command](https://docs.cloud.google.com/bigquery/docs/reference/bq-cli-reference#mk-dataset) .

1.  Create a dataset named `bqml_tutorial` with the data location set to `US` :
    
        bq mk --dataset \
          --location=US \
          --description "BigQuery ML tutorial dataset." \
          bqml_tutorial

2.  Confirm that the dataset was created:
    
        bq ls

### API

Call the [`datasets.insert`](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/datasets/insert) method with a defined [dataset resource](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/datasets) :

    {
      "datasetReference": {
         "datasetId": "bqml_tutorial"
      }
    }

## Create test tables

Create tables of training and evaluation data based on the public [`task955_wiki_auto_style_transfer` dataset](https://huggingface.co/datasets/Lots-of-LoRAs/task955_wiki_auto_style_transfer) from Hugging Face.

1.  Open [Cloud Shell](https://console.cloud.google.com/bigquery?cloudshell=true) .

2.  In Cloud Shell, create tables of test and evaluation data:
    
        python3 -m pip install pandas pyarrow fsspec huggingface_hub
        
        python3 -c "import pandas as pd; df_train = pd.read_parquet('hf://datasets/Lots-of-LoRAs/task955_wiki_auto_style_transfer/data/train-00000-of-00001.parquet').drop('id', axis=1); df_train['output'] = [x[0] for x in df_train['output']]; df_train.to_json('wiki_auto_style_transfer_train.jsonl', orient='records', lines=True);"
        
        python3 -c "import pandas as pd; df_valid = pd.read_parquet('hf://datasets/Lots-of-LoRAs/task955_wiki_auto_style_transfer/data/valid-00000-of-00001.parquet').drop('id', axis=1); df_valid['output'] = [x[0] for x in df_valid['output']]; df_valid.to_json('wiki_auto_style_transfer_valid.jsonl', orient='records', lines=True);"
        
        bq load --replace=true --source_format=NEWLINE_DELIMITED_JSON bqml_tutorial.wiki_auto_style_transfer_train wiki_auto_style_transfer_train.jsonl input:STRING,output:STRING
        
        bq load --replace=true --source_format=NEWLINE_DELIMITED_JSON bqml_tutorial.wiki_auto_style_transfer_valid wiki_auto_style_transfer_valid.jsonl input:STRING,output:STRING

## View the training data

The input training data is a prompt that asks the model to elaborate a sentence without changing its general meaning. Each prompt includes the same set of two positive examples and two negative examples, along with a sentence to rewrite. The output is the more detailed sentence produced by the model.

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, run the following statement to view an example of input and output data:
    
        SELECT * FROM bqml_tutorial.wiki_auto_style_transfer_train LIMIT 1;
    
    The result is similar to the following:
    
    ```console
    +-----------------------------------------------+-------------------------------------------------+
    | input                                         | output                                          |
    +-----------------------------------------------+-------------------------------------------------+
    | Definition: In this task, we ask you to       | Merton College ( in full : The House or College |
    | elaborate the sentence without changing its   | of Scholars of Merton in the University of      |
    | general meaning. You can do so by explaining  | Oxford ) is one of the constituent colleges of  |
    | further the input sentence, using more        | the University of Oxford in England .           |
    | precise wording, adding qualifiers and        |                                                 |
    | auxiliary information etc.                    |                                                 |
    |                                               |                                                 |
    | Positive Example 1 -                          |                                                 |
    | Input: The Inheritance Cycle is a series of   |                                                 |
    | fantasy books written by Christopher Paolini. |                                                 |
    | Output: The Inheritance Cycle is a tetralogy  |                                                 |
    | of young adult high fantasy novels written by |                                                 |
    | American author Christopher Paolini.          |                                                 |
    |                                               |                                                 |
    | Positive Example 2 -                          |                                                 |
    | Input: The Greco-Roman or Graeco-Roman world, |                                                 |
    | refers to geographical regions and countries  |                                                 |
    | who had the language , culture , government   |                                                 |
    | or religion of the ancient Greeks and Romans. |                                                 |
    | Output: The Greco-Roman world , Greco-Roman   |                                                 |
    | culture , or the term Greco-Roman (spelled    |                                                 |
    | Graeco-Roman in the United Kingdom and the    |                                                 |
    | Commonwealth), when used as an adjective , as |                                                 |
    | understood by modern scholars and writers ,   |                                                 |
    | refers to those geographical regions and      |                                                 |
    | countries that culturally ( and so            |                                                 |
    |  historically ) were directly , long-term ,   |                                                 |
    | and intimately influenced by the language ,   |                                                 |
    | culture , government and religion of the      |                                                 |
    | ancient Greeks and Romans.                    |                                                 |
    |                                               |                                                 |
    | Negative Example 1 -                          |                                                 |
    | Input: Boryla, an American football           |                                                 |
    | quarterback, did not participate in the 1952  |                                                 |
    | playoffs.                                     |                                                 |
    | Output: Boryla was not in the 1952 playoffs.  |                                                 |
    |                                               |                                                 |
    | Negative Example 2 -                          |                                                 |
    | Input: The wild population in China decreased |                                                 |
    | to around 2,000 in 2005.                      |                                                 |
    | Output: By 2005, the wild population          |                                                 |
    | decreased to about 2,000.                     |                                                 |
    |                                               |                                                 |
    | Now complete the following example -          |                                                 |
    | Input: Merton College is one of the colleges  |                                                 |
    | of the University of Oxford .                 |                                                 |
    | Output:                                       |                                                 |
    +-----------------------------------------------+-------------------------------------------------+
    ```

## Create a baseline model

Create a [remote model](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model) over a Gemini model:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, run the following statement to create a remote model:
    
        CREATE OR REPLACE MODEL `bqml_tutorial.gemini_baseline`
        REMOTE WITH CONNECTION DEFAULT
        OPTIONS (ENDPOINT = 'gemini-2.5-pro');
    
    The query takes several seconds to complete, after which the `gemini_baseline` model appears in the `bqml_tutorial` dataset in the **Explorer** pane. Because the query uses a `CREATE MODEL` statement to create a model, there are no query results.

## Check the baseline model performance

To see how the remote model performs on the evaluation data without any tuning, run the [`AI.GENERATE_TEXT` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate-text) :

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, run the following statement:
    
        SELECT result, ground_truth
        FROM
          AI.GENERATE_TEXT(
            MODEL `bqml_tutorial.gemini_baseline`,
            (
              SELECT
                input AS prompt, output AS ground_truth
              FROM `bqml_tutorial.wiki_auto_style_transfer_valid`
              LIMIT 10
            ));
    
    The result is similar to the following:
    
    ```console
    +-------------------------------------------------+-------------------------------------------------+
    | result                                          | ground_truth                                    |
    +-------------------------------------------------+-------------------------------------------------+
    | In mathematics, and more specifically in graph  | In mathematics , and more specifically in graph |
    | theory, a graph is an abstract structure that   | theory , a graph is a structure amounting to a  |
    | is used to model pairwise relationships between | set of objects in which some pairs of the       |
    | objects. A graph in this context is made up of  | objects are in some sense " related " .         |
    | vertices (also called nodes or points) and      |                                                 |
    | edges (also called links or lines) that connect |                                                 |
    | pairs of vertices.                              |                                                 |
    | ...                                             | ...                                             |
    +-------------------------------------------------+-------------------------------------------------+
    ```
    
    Although the baseline model generates text that accurately reflects the facts provided in the ground truth content, the style of the text is sometimes different. The baseline model tends to produce longer elaborations than the desired ground truth.

## Evaluate the baseline model

To perform a more detailed evaluation of the model performance, use the [`ML.EVALUATE` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-evaluate) . This function computes model metrics that measure the accuracy and quality of the generated text in order to see how the model's responses compare to ideal responses.

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, run the following statement:
    
        SELECT *
        FROM
          ML.EVALUATE(
            MODEL `bqml_tutorial.gemini_baseline`,
            (
              SELECT
                input AS input_text, output AS output_text
              FROM `bqml_tutorial.wiki_auto_style_transfer_valid`
            ),
            STRUCT('text_generation' AS task_type));
    
    The result is similar to the following:
    
    ```console
    +---------------------+---------------------+-------------------------------------------+--------------------------------------------+
    | bleu4_score         | rouge-l_precision   | rouge-l_recall      | rouge-l_f1_score    | evaluation_status                          |
    +---------------------+---------------------+---------------------+---------------------+--------------------------------------------+
    | 0.32571814014498979 | 0.45752569962901607 | 0.557224161991254   | 0.49205029983307907 | {                                          |
    |                     |                     |                     |                     |  "num_successful_rows": 176,               |
    |                     |                     |                     |                     |  "num_total_rows": 176                     |
    |                     |                     |                     |                     | }                                          |
    +---------------------+---------------------+ --------------------+---------------------+--------------------------------------------+
    ```

These scores provide a quantitative way to measure performance. The next sections show you how to create a tuned model and compare its performance to the baseline model.

## Create a tuned model

Create a remote model very similar to the one you created in [Create a model](https://docs.cloud.google.com/bigquery/docs/tune-evaluate#create_a_baseline_model) , but this time specify the [`AS SELECT` clause](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-tuned#as_select) to provide the training data to tune the model.

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, run the following statement to create a [remote model](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-tuned) :
    
        CREATE OR REPLACE MODEL `bqml_tutorial.gemini_tuned`
          REMOTE
            WITH CONNECTION DEFAULT
          OPTIONS (
            endpoint = 'gemini-2.5-pro',
            max_iterations = 500,
            data_split_method = 'no_split')
        AS
        SELECT
          input AS prompt, output AS label
        FROM `bqml_tutorial.wiki_auto_style_transfer_train`;
    
    The query takes a few minutes to complete, after which the `gemini_tuned` model appears in the `bqml_tutorial` dataset in the **Explorer** pane. Because the query uses a `CREATE MODEL` statement to create a model, there are no query results.

## Check the tuned model performance

To see how the tuned model performs on the evaluation data, run the `AI.GENERATE_TEXT` function:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, run the following statement:
    
        SELECT result, ground_truth
        FROM
          AI.GENERATE_TEXT(
            MODEL `bqml_tutorial.gemini_tuned`,
            (
              SELECT
                input AS prompt, output AS ground_truth
              FROM `bqml_tutorial.wiki_auto_style_transfer_valid`
              LIMIT 10
            ));
    
    The tuned model produces text that is much more similar in style to the ground truth content.

## Evaluate the tuned model

To see how the tuned model's responses compare to ideal responses, use the `ML.EVALUATE` function:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, run the following statement:
    
        SELECT *
        FROM
          ML.EVALUATE(
            MODEL `bqml_tutorial.gemini_tuned`,
            (
              SELECT
                input AS prompt, output AS label
              FROM `bqml_tutorial.wiki_auto_style_transfer_valid`
            ),
            STRUCT('text_generation' AS task_type));
    
    The result is similar to the following:
    
    ```console
    +---------------------+---------------------+-------------------------------------------+--------------------------------------------+
    | bleu4_score         | rouge-l_precision   | rouge-l_recall      | rouge-l_f1_score    | evaluation_status                          |
    +---------------------+---------------------+---------------------+---------------------+--------------------------------------------+
    | 0.44878025403825506 | 0.57236062510796448 | 0.638794269320597   | 0.59591519400141835 | {                                          |
    |                     |                     |                     |                     |  "num_successful_rows": 176,               |
    |                     |                     |                     |                     |  "num_total_rows": 176                     |
    |                     |                     |                     |                     | }                                          |
    +---------------------+---------------------+ --------------------+---------------------+--------------------------------------------+
    ```

The tuned model shows a marked improvement in performance and outperforms the baseline model on all evaluation metrics.

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

### Delete individual resources

If you want to reuse the project, then delete the resources that you created for this tutorial.

1.  Go to the **BigQuery** page.

2.  Delete the `bqml_tutorial` dataset. Deleting the dataset also deletes the models and tables.
    
    1.  In the **Explorer** pane, expand your project and click **Datasets** .
    
    2.  In the **Datasets** list, click the `bqml_tutorial` dataset.
    
    3.  In the details pane, click delete **Delete** .
    
    4.  In the **Delete dataset** dialog, click **Delete** .

## What's next

  - Learn more about the [`ML.EVALUATE` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-evaluate) .
  - Learn more about the [`AI.GENERATE_TEXT` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate-text) .
  - Review [supervised tuning options](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-tuned#supervised_tuning) for remote models.
