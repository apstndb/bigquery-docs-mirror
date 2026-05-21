---
name: documents/docs.cloud.google.com/bigquery/docs/rag-pipeline-pdf
uri: https://docs.cloud.google.com/bigquery/docs/rag-pipeline-pdf
title: Parse PDFs in a retrieval-augmented generation pipeline
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

This tutorial guides you through the process of creating a retrieval-augmented generation (RAG) pipeline based on parsed PDF content.

PDF files, such as financial documents, can be challenging to use in RAG pipelines because of their complex structure and mix of text, figures, and tables. This tutorial shows you how to use the [`AI.PARSE_DOCUMENT` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-parse-document) in combination with Document AI's layout parser to build a RAG pipeline based on key information extracted from a PDF file.

## Objectives

This tutorial covers the following tasks:

  - Create a Cloud Storage bucket and upload a sample PDF file.
  - [Create a Document AI processor](https://docs.cloud.google.com/document-ai/docs/create-processor#create-processor) that you can use to parse the PDF file.
  - Use the [`AI.PARSE_DOCUMENT` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-parse-document) to parse the PDF contents into chunks and then write that content to a BigQuery table.
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

## Upload the sample PDF to Cloud Storage

To upload the sample PDF to Cloud Storage, follow these steps:

1.  Download the `scf23.pdf` sample PDF by going to <https://www.federalreserve.gov/publications/files/scf23.pdf> and clicking download download .
2.  [Create a Cloud Storage bucket](https://docs.cloud.google.com/storage/docs/creating-buckets) .
3.  [Upload](https://docs.cloud.google.com/storage/docs/uploading-objects) the `scf23.pdf` file to the bucket.

## Create a document processor

[Create a document processor](https://docs.cloud.google.com/document-ai/docs/create-processor#create-processor) based on the [layout parser processor](https://docs.cloud.google.com/document-ai/docs/layout-parse-chunk) in the `us` multi-region. Copy the prediction endpoint from the **Processor details** page to use in the next section.

## Parse the PDF file into chunks

Use the document processor with the `AI.PARSE_DOCUMENT` function to parse the PDF file into chunks, and then write that content to a table.

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, run the following statement:
    
        CREATE OR REPLACE TABLE bqml_tutorial.parsed_pdf
        AS (
          SELECT *
          FROM
            AI.PARSE_DOCUMENT(
              (
                SELECT
                  OBJ.MAKE_REF("gs://BUCKET/scf23.pdf") AS ref
              ),
              endpoint => "PREDICTION_ENDPOINT",
              chunk_size => 250)
        );

## Generate embeddings

Generate embeddings for the parsed PDF content and then write them to a table:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, run the following statement:
    
        CREATE OR REPLACE TABLE `bqml_tutorial.embeddings` AS (
          SELECT *, AI.EMBED(content, endpoint => 'text-embedding-005') AS embedding
          FROM bqml_tutorial.parsed_pdf
        );

## Run a vector search

Run a vector search against the parsed PDF content.

The following query takes text input, creates an embedding for that input using the `AI.EMBED` function, and then uses the `VECTOR_SEARCH` function to match the input embedding with the most similar PDF content embeddings. The results are the top ten PDF chunks that are most related to changes in family net worth.

1.  Go to the **BigQuery** page.

2.  In the query editor, run the following SQL statement:
    
        SELECT distance, base.chunk_id, base.start_page, base.end_page, base.content
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

Perform a vector search on the embeddings to identify semantically similar PDF content, and then use the `AI.GENERATE_TEXT` function with the vector search results to augment the prompt input and improve the text generation results. In this case, the query uses information from the PDF chunks to answer a question about the change in family net worth over the past decade.

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, run the following statement:
    
        SELECT
          AI.GENERATE(
            CONCAT('Did the typical family net worth change? How does this compare the SCF survey a decade earlier? Be concise and use the following context:',
                    STRING_AGG(FORMAT("context: %s", base.content), ',\n')
            )
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

\- Learn more about the [`AI.PARSE_DOCUMENT` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-parse-document) . - Learn more about performing [semantic search and RAG](https://docs.cloud.google.com/bigquery/docs/vector-index-text-search-tutorial) .
