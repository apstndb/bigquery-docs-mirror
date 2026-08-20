---
name: documents/docs.cloud.google.com/bigquery/docs/vector-index-text-search-tutorial
uri: https://docs.cloud.google.com/bigquery/docs/vector-index-text-search-tutorial
title: Perform semantic search and retrieval-augmented generation
description: Use BigQuery ML and Agent Platform to generate text embeddings, and then use the embeddings to perform a semantic search and retrieval-augmented generation.
data_source: docs.cloud.google.com
---

In this tutorial, you use a [remote model](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model) with the [`AI.GENERATE_EMBEDDING` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate-embedding) to generate [text embeddings](https://docs.cloud.google.com/bigquery/docs/generative-ai-overview#text_embedding) in a BigQuery table. You then create a [vector index](https://docs.cloud.google.com/bigquery/docs/vector-index) to index the embeddings to improve search performance.

You use the [`VECTOR_SEARCH` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/search_functions#vector_search) with the embeddings to search for similar text. Vector search is a technique to compare similar objects using embeddings, which are high-dimensional numerical vectors that represent a given entity, like a piece of text.

Finally, you perform [retrieval-augmented generation (RAG)](https://cloud.google.com/use-cases/retrieval-augmented-generation) by generating text with the [`AI.GENERATE_TEXT` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate-text) . RAG is an AI framework that combines the strengths of information retrieval systems (such as search and databases) with the capabilities of generative large language models (LLMs). By combining your data and world knowledge with LLM language skills, grounded generation is more accurate, up-to-date, and relevant to your specific needs.

This tutorial uses data from the [Google Patents Research public dataset](https://console.cloud.google.com/bigquery?p=patents-public-data&d=google_patents_research&page=dataset&ws=!1m5!1m4!3m2!1spatents-public-data!2sgoogle_patents_research!23sLEGACY_URL_PARAM) .

## Objectives

  - Create a BigQuery ML remote model over a Gemini Enterprise Agent Platform embedding model.
  - Use the remote model with the `AI.GENERATE_EMBEDDING` function to generate embeddings from text in a BigQuery table.
  - Create a vector index to index the embeddings in order to improve search performance.
  - Use the `VECTOR_SEARCH` function with the embeddings to search for similar text.
  - Perform RAG by generating text with the `AI.GENERATE_TEXT` function, and using vector search results to augment the prompt input and improve results.

## Costs

In this document, you use the following billable components of Google Cloud:

  - **BigQuery ML** : You incur costs for the data that you process in BigQuery.
  - **Gemini Enterprise Agent Platform** : You incur costs for calls to the Agent Platform service that's represented by the remote model.

To generate a cost estimate based on your projected usage, use the [pricing calculator](https://docs.cloud.google.com/products/calculator) .

New Google Cloud users might be eligible for a [free trial](https://docs.cloud.google.com/free) .

For more information, see the following pricing pages:

  - [BigQuery pricing](https://cloud.google.com/bigquery/pricing)
  - [Agent Platform pricing](https://cloud.google.com/vertex-ai/pricing#generative_ai_models)

## Before you begin

1.  In the Google Cloud console, on the project selector page, select or create a Google Cloud project.
    
    **Roles required to select or create a project**
    
      - **Select a project** : Selecting a project doesn't require a specific IAM role—you can select any project that you've been granted a role on.
      - **Create a project** : To create a project, you need the Project Creator role ( `roles/resourcemanager.projectCreator` ), which contains the `resourcemanager.projects.create` permission. [Learn how to grant roles](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .
    
    > **Note** : If you don't plan to keep the resources that you create in this procedure, create a project instead of selecting an existing project. After you finish these steps, you can delete the project, removing all resources associated with the project.

2.  [Verify that billing is enabled for your Google Cloud project](https://docs.cloud.google.com/billing/docs/how-to/verify-billing-enabled#confirm_billing_is_enabled_on_a_project) .

3.  Enable the BigQuery, Cloud Storage, and Gemini Enterprise Agent Platform APIs.
    
    **Roles required to enable APIs**
    
    To enable APIs, you need the `serviceusage.services.enable` permission. If you created the project, then you likely already have this permission through the Owner role ( `roles/owner` ). Otherwise, you can get this permission through the Service Usage Admin role ( `roles/serviceusage.serviceUsageAdmin` ). [Learn how to grant roles](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

### Required roles

To get the permissions that you need to complete this tutorial, ask your administrator to grant you the following IAM roles:

  - Create datasets, tables, and models: [BigQuery Data Owner](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner) ( `roles/bigquery.dataOwner` )
  - Run BigQuery jobs: [BigQuery Job User](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.jobUser) ( `roles/bigquery.jobUser` )
  - Create and manage connections: [BigQuery Connection Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.connectionAdmin) ( `roles/bigquery.connectionAdmin` )

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

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

## Create the remote model for text embedding generation

In this section, you create a remote model that represents a hosted Agent Platform text embedding generation model. When you create the model, you use the [`DEFAULT` connection](https://docs.cloud.google.com/bigquery/docs/default-connections) to call the [Text embeddings API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/text-embeddings-api) to get text embeddings using the `text-embedding-005` model. If you don't have a default connection, the `CREATE MODEL` statement creates one for you.

To create the text embedding model, follow these steps:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  To create the model, paste this command into the query editor, and then click play\_circle **Run** :
    
        CREATE OR REPLACE MODEL `bqml_tutorial.embedding_model`
          REMOTE WITH CONNECTION DEFAULT
          OPTIONS (ENDPOINT = 'text-embedding-005');
    
    The query takes several seconds to complete, after which the model `embedding_model` can be accessed through the **Explorer** pane.
    
    You receive a confirmation message like the following: `Successfully created model named embedding_model.`

## Generate text embeddings

Generate text embeddings from patent abstracts using the [`AI.GENERATE_EMBEDDING` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate-embedding) , and then write them to a BigQuery table so that they can be searched.

Embedding generation using the [`AI.GENERATE_EMBEDDING` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate-embedding) might fail due to Agent Platform LLM [quotas](https://docs.cloud.google.com/bigquery/quotas#cloud_ai_service_functions) or service unavailability. If it fails, error details are returned in the `status` column in the query results.

For alternative text embedding generation methods in BigQuery, see the [Embed text with pretrained TensorFlow models tutorial](https://docs.cloud.google.com/bigquery/docs/generate-embedding-with-tensorflow-models) .

To generate text embeddings, paste this command into the query editor, and then click play\_circle **Run** :

``` 
  CREATE OR REPLACE TABLE bqml_tutorial.embeddings AS  SELECT * FROM AI.GENERATE_EMBEDDING(    MODEL bqml_tutorial.embedding_model,    (      SELECT *, abstract AS content      FROM patents-public-data.google_patents_research.publications      WHERE LENGTH(abstract) > 0 AND LENGTH(title) > 0 AND country = 'Singapore'    )  )  WHERE LENGTH(status) = 0;  
```

This query takes several minutes to complete. You receive a confirmation message like the following: `This statement created a new table named embeddings.`

## Create a vector index

If you create a vector index on an embedding column, a vector search that's performed on that column uses the [Approximate Nearest Neighbor](https://en.wikipedia.org/wiki/Nearest_neighbor_search#Approximation_methods) search technique. This technique improves vector search performance and returns more approximate results, but [recall](https://developers.google.com/machine-learning/crash-course/classification/precision-and-recall#recallsearch_term_rules) is reduced.

To create a vector index, you use the [`CREATE VECTOR INDEX`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_vector_index_statement) data definition language (DDL) statement. To verify that the index is available, you query the [`INFORMATION_SCHEMA.VECTOR_INDEXES` view](https://docs.cloud.google.com/bigquery/docs/information-schema-vector-indexes) to verify that the `coverage_percentage` column value is greater than `0` , and the `last_refresh_time` column value isn't `NULL` .

To create and verify the vector index, follow these steps:

1.  To create the vector index, paste this command into the query editor, and then click play\_circle **Run** :
    
        CREATE OR REPLACE VECTOR INDEX my_index
        ON `bqml_tutorial.embeddings`(embedding)
        OPTIONS(index_type = 'IVF',
          distance_type = 'COSINE',
          ivf_options = '{"num_lists":500}');
    
    You receive a confirmation message like the following: `The vector index creation on table bqml_tutorial.embeddings was initiated. Please query bqml_tutorial.INFORMATION_SCHEMA.VECTOR_INDEXES to check the progress of the index.`
    
    Creating a vector index typically takes only a few seconds. It takes another two to three minutes for the vector index to be populated asynchronously.

2.  To verify that the index is ready to be used, paste this command into the query editor, and then click play\_circle **Run** :
    
        SELECT table_name, index_name, index_status,
        coverage_percentage, last_refresh_time, disable_reason
        FROM `PROJECT_ID.bqml_tutorial.INFORMATION_SCHEMA.VECTOR_INDEXES`;
    
    Replace `  PROJECT_ID  ` with your project ID.
    
    After you run the query, the index is available if the `index_status` column in the results shows that the index is `ACTIVE` , and if the `coverage_percentage` value is `100` .

## Perform a text similarity search using the vector index

Use the [`VECTOR_SEARCH` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/search_functions#vector_search) to search for relevant patents that match embeddings generated from a text query.

The `top_k` argument determines the number of matches to return, in this case five. The `fraction_lists_to_search` option determines the percentage of vector index lists to search. [The vector index you created](https://docs.cloud.google.com/bigquery/docs/vector-index-text-search-tutorial#create_a_vector_index) has 500 lists, so the `fraction_lists_to_search` value of `.01` indicates that this vector search scans five of those lists. A lower `fraction_lists_to_search` value as shown here provides lower [recall](https://developers.google.com/machine-learning/crash-course/classification/accuracy-precision-recall#recall) and faster performance.

For more information about vector index lists, see the `num_lists` [vector index option](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#vector_index_option_list) .

The model you use to generate the embeddings in this query must be the same as the one you use to generate the embeddings in the table you're comparing against, otherwise the search results won't be accurate.

To perform a text similarity search, paste this command into the query editor, and then click play\_circle **Run** :

``` 
  SELECT query.query, base.publication_number, base.title, base.abstract  FROM VECTOR_SEARCH(    TABLE bqml_tutorial.embeddings, 'embedding',    (    SELECT embedding, content AS query    FROM AI.GENERATE_EMBEDDING(    MODEL bqml_tutorial.embedding_model,    (SELECT 'improving password security' AS content))    ),    top_k => 5, options => '{"fraction_lists_to_search": 0.01}');  
```

The output is similar to the following:

    +-----------------------------+--------------------+-------------------------------------------------+-------------------------------------------------+
    |            query            | publication_number |                       title                     |                      abstract                   |
    +-----------------------------+--------------------+-------------------------------------------------+-------------------------------------------------+
    | improving password security | SG-120868-A1       | Data storage device security method and a...    | Methods for improving security in data stora... |
    | improving password security | SG-10201610585W-A  | Passsword management system and process...      | PASSSWORD MANAGEMENT SYSTEM AND PROCESS ...     |
    | improving password security | SG-148888-A1       | Improved system and method for...               | IMPROVED SYSTEM AND METHOD FOR RANDOM...        |
    | improving password security | SG-194267-A1       | Method and system for protecting a password...  | A system for providing security for a...        |
    | improving password security | SG-120868-A1       | Data storage device security...                 | Methods for improving security in data...       |
    +-----------------------------+--------------------+-------------------------------------------------+-------------------------------------------------+

## Create the remote model for text generation

To create a remote model that represents a hosted Agent Platform text generation model, paste this command into the query editor, and then click play\_circle **Run** :

``` 
  CREATE OR REPLACE MODEL bqml_tutorial.text_model    REMOTE WITH CONNECTION DEFAULT    OPTIONS (ENDPOINT = 'gemini-2.5-flash');  
```

You receive a confirmation message similar to the following: `Successfully created model named text_model.`

## Generate text augmented by vector search results

Feed the search results as prompts to generate text with the [`AI.GENERATE_TEXT` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate-text) .

To augment the vector search results, paste this command into the query editor, and then click play\_circle **Run** :

``` 
  SELECT result AS generated, prompt  FROM AI.GENERATE_TEXT(    MODEL bqml_tutorial.text_model,    (      SELECT CONCAT(        'Propose some project ideas to improve user password security using the context below: ',        STRING_AGG(          FORMAT("patent title: %s, patent abstract: %s", base.title, base.abstract),          ',\n')        ) AS prompt,      FROM VECTOR_SEARCH(        TABLE bqml_tutorial.embeddings, 'embedding',        (          SELECT embedding, content AS query          FROM AI.GENERATE_EMBEDDING(            MODEL bqml_tutorial.embedding_model,            (SELECT 'improving password security' AS content)          )        ),      top_k => 5, options => '{"fraction_lists_to_search": 0.01}')    ),    STRUCT(600 AS max_output_tokens));  
```

The output is similar to the following:

    +------------------------------------------------+------------------------------------------------------------+
    |            generated                           | prompt                                                     |
    +------------------------------------------------+------------------------------------------------------------+
    | These patents suggest several project ideas to | Propose some project ideas to improve user password        |
    | improve user password security.  Here are      | security using the context below: patent title: Active     |
    | some, categorized by the patent they build     | new password entry dialog with compact visual indication   |
    | upon:                                          | of adherence to password policy, patent abstract:          |
    |                                                | An active new password entry dialog provides a compact     |
    | **I. Projects based on "Active new password    | visual indication of adherence to password policies. A     |
    | entry dialog with compact visual indication of | visual indication of progress towards meeting all          |
    | adherence to password policy":**               | applicable password policies is included in the display    |
    |                                                | and updated as new password characters are being...        |
    +------------------------------------------------+------------------------------------------------------------+

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

Alternatively, to keep the project and delete the resources used in this tutorial, follow these steps:

1.  Go to the **BigQuery** page.

2.  In the left pane, expand your project, and then click **Datasets** .

3.  For the `bqml_tutorial` dataset, click more\_vert **Open actions \> Delete** .

4.  In the **Delete dataset** dialog, click **Delete** to confirm.

5.  In the left pane, click **Connections** .

6.  For the `__default_cloudresource_connection__` connection, click more\_vert **Open actions \> Delete** .

7.  In the **Delete connection** dialog, enter `delete` , and then click **Delete** to confirm.

## What's next

  - To learn how to create a RAG pipeline based on parsed PDF content, see [Parse PDFs in a retrieval-augmented generation pipeline](https://docs.cloud.google.com/bigquery/docs/rag-pipeline-pdf) .
