---
name: documents/docs.cloud.google.com/bigquery/docs/vector-search
uri: https://docs.cloud.google.com/bigquery/docs/vector-search
title: Search embeddings with vector search
description: Perform a similarity search on embeddings stored in BigQuery tables by using the `VECTOR_SEARCH` function and optionally a vector index.
data_source: docs.cloud.google.com
---

This tutorial shows you how to perform a [similarity search](https://wikipedia.org/wiki/Similarity_search) on embeddings stored in BigQuery tables by using the [`VECTOR_SEARCH` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/search_functions#vector_search) and a [vector index](https://docs.cloud.google.com/bigquery/docs/vector-index) .

Vector search is a technique to compare similar objects using embeddings, and it is used to power Google products, including Google Search, YouTube, and Google Play. You can use vector search to perform semantic searches at scale, or you can perform a **hybrid search** that combines a semantic search with a lexical (keyword) search. When you use [vector indexes](https://docs.cloud.google.com/bigquery/docs/vector-index) with vector search, you can take advantage of foundational technologies like inverted file indexing (IVF) and the [ScaNN algorithm](https://research.google/blog/announcing-scann-efficient-vector-similarity-search/) .

Vector search is built on embeddings. Embeddings are high-dimensional numerical vectors that represent a given entity, like a piece of text or an audio file. Machine learning (ML) models use embeddings to encode semantics about such entities to make it easier to reason about and compare them. For example, a common operation in clustering, classification, and recommendation models is to measure the distance between vectors in an [embedding space](https://en.wikipedia.org/wiki/Latent_space) to find items that are most semantically similar.

## Objectives

  - Perform a similarity search on embeddings stored in BigQuery tables by using the `VECTOR_SEARCH` function.
  - Use a vector index to improve vector search performance.
  - Perform a search that uses a vector index and a search that doesn't use an index.
  - Evaluate recall by comparing the results of searches with an index and searches without an index.

## Costs

The `VECTOR_SEARCH` function uses [BigQuery compute pricing](https://cloud.google.com/bigquery/pricing#analysis_pricing_models) . You are charged for similarity search, using on-demand or editions pricing.

  - On-demand: you are charged for the amount of bytes scanned in the base table, the index, and the search query.

  - Editions pricing: you are charged for the slots required to complete the job within your reservation edition. Larger, more complex similarity calculations incur more charges.
    
    > **Note:** Using an index isn't supported in [Standard editions](https://docs.cloud.google.com/bigquery/docs/editions-intro) .

For more information, see [BigQuery pricing](https://cloud.google.com/bigquery/pricing) .

## Before you begin

1.  In the Google Cloud console, on the project selector page, select or create a Google Cloud project.
    
    **Roles required to select or create a project**
    
      - **Select a project** : Selecting a project doesn't require a specific IAM role—you can select any project that you've been granted a role on.
      - **Create a project** : To create a project, you need the Project Creator role ( `roles/resourcemanager.projectCreator` ), which contains the `resourcemanager.projects.create` permission. [Learn how to grant roles](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .
    
    > **Note** : If you don't plan to keep the resources that you create in this procedure, create a project instead of selecting an existing project. After you finish these steps, you can delete the project, removing all resources associated with the project.

2.  [Verify that billing is enabled for your Google Cloud project](https://docs.cloud.google.com/billing/docs/how-to/verify-billing-enabled#confirm_billing_is_enabled_on_a_project) .

3.  Enable the BigQuery API.
    
    **Roles required to enable APIs**
    
    To enable APIs, you need the `serviceusage.services.enable` permission. If you created the project, then you likely already have this permission through the Owner role ( `roles/owner` ). Otherwise, you can get this permission through the Service Usage Admin role ( `roles/serviceusage.serviceUsageAdmin` ). [Learn how to grant roles](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

### Required roles

To get the permissions that you need to complete this tutorial, ask your administrator to grant you the following IAM roles on the project:

  - Create datasets, tables, and vector indexes: [BigQuery Data Editor](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor) ( `roles/bigquery.dataEditor` )
  - Run BigQuery jobs: [BigQuery Job User](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.jobUser) ( `roles/bigquery.jobUser` )

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

## Create tables to store data and embeddings

In this section, you create the `patents` table that contains patents embeddings. The embeddings are based on a subset of the [Google Patents](https://console.cloud.google.com/marketplace/product/google_patents_public_datasets/google-patents-public-data) public dataset. You also create the `patents2` table that contains a patent embedding to find nearest neighbors.

To create the tables, follow these steps:

1.  To create the `patents` table, paste the following in the query editor, and then click play\_circle **Run** :
    
        CREATE TABLE bqml_tutorial.patents AS
        SELECT * FROM `patents-public-data.google_patents_research.publications`
        WHERE ARRAY_LENGTH(embedding_v1) > 0
         AND publication_number NOT IN ('KR-20180122872-A')
        LIMIT 1000000;
    
    You receive a confirmation message like the following: `This statement created a new table named patents.`

2.  To create the `patents2` table that contains a patent embedding to find nearest neighbors, paste the following in the query editor, and then click play\_circle **Run** :
    
        CREATE TABLE bqml_tutorial.patents2 AS
        SELECT * FROM `patents-public-data.google_patents_research.publications`
        WHERE publication_number = 'KR-20180122872-A';
    
    You receive a confirmation message like the following: `This statement created a new table named patents2.`

## Create a vector index

When you use `VECTOR_SEARCH` with a vector index, `VECTOR_SEARCH` uses the [Approximate Nearest Neighbor](https://en.wikipedia.org/wiki/Nearest_neighbor_search#Approximation_methods) method to improve vector search performance, with the trade-off of reducing [recall](https://developers.google.com/machine-learning/crash-course/classification/precision-and-recall#recallsearch_term_rules) and so returning more approximate results. Without a vector index, `VECTOR_SEARCH` uses [brute force search](https://en.wikipedia.org/wiki/Brute-force_search) to measure distance for every record.

In this section, you create the `my_index` vector index on the `embedding_v1` column of the `patents` table. You then verify that the index is available.

To create the vector index, follow these steps:

1.  To create the `my_index` vector index on the `embedding_v1` column of the `patents` table, paste the following in the query editor, and then click play\_circle **Run** :
    
        CREATE OR REPLACE VECTOR INDEX my_index ON bqml_tutorial.patents(embedding_v1)
        STORING(publication_number, title)
        OPTIONS(distance_type='COSINE', index_type='IVF');
    
    You receive a confirmation message like the following: `The vector index creation on table bqml_tutorial.patents was initiated. Please query bqml_tutorial.INFORMATION_SCHEMA.VECTOR_INDEXES to check the progress of the index.`

2.  To confirm that the vector index is ready, paste the following in the query editor, and then click play\_circle **Run** :
    
        SELECT * FROM bqml_tutorial.INFORMATION_SCHEMA.VECTOR_INDEXES;
    
    In the query results, verify that the `index_status` is `ACTIVE` , and that the `coverage_percentage` value is `100` . It may take several minutes for `coverage_percentage` to reach `100` .

## Use the `VECTOR_SEARCH` function with an index

After the vector index is created and populated, use the `VECTOR_SEARCH` function to find the nearest neighbor for the embedding in the `embedding_v1` column in the `patents2` table. This query uses the vector index in the search, so `VECTOR_SEARCH` uses an [Approximate Nearest Neighbor](https://en.wikipedia.org/wiki/Nearest_neighbor_search#Approximation_methods) method to find the embedding's nearest neighbor.

> **Note:** Vector indexes are more effective on large datasets. If you want to see this in action, [recreate the `vector_search.patents` table](https://docs.cloud.google.com/bigquery/docs/vector-search#create_test_tables_to_store_data_and_embeddings) without the `LIMIT 1000000` clause, [recreate the vector index](https://docs.cloud.google.com/bigquery/docs/vector-search#create_a_vector_index) , and then run the following query.

To use the `VECTOR_SEARCH` function with an index, paste the following in the query editor, and then click play\_circle **Run** :

    SELECT query.publication_number AS query_publication_number,
      query.title AS query_title,
      base.publication_number AS base_publication_number,
      base.title AS base_title,
      distance
    FROM
      VECTOR_SEARCH(
        TABLE bqml_tutorial.patents,
        'embedding_v1',
        TABLE bqml_tutorial.patents2,
        top_k => 5,
        distance_type => 'COSINE',
        options => '{"fraction_lists_to_search": 0.005}');

The results look similar to the following:

```console
+--------------------------+-------------------------------------------------------------+-------------------------+--------------------------------------------------------------------------------------------------------------------------+---------------------+
| query_publication_number |                         query_title                         | base_publication_number |                                                        base_title                                                        |      distance       |
+--------------------------+-------------------------------------------------------------+-------------------------+--------------------------------------------------------------------------------------------------------------------------+---------------------+
| KR-20180122872-A         | Rainwater management system based on rainwater keeping unit | CN-106599080-B          | A kind of rapid generation for keeping away big vast transfer figure based on GIS                                        | 0.14471956347590609 |
| KR-20180122872-A         | Rainwater management system based on rainwater keeping unit | CN-114118544-A          | Urban waterlogging detection method and device                                                                           | 0.17472108931171348 |
| KR-20180122872-A         | Rainwater management system based on rainwater keeping unit | KR-20200048143-A        | Method and system for mornitoring dry stream using unmanned aerial vehicle                                               | 0.17561990745619782 |
| KR-20180122872-A         | Rainwater management system based on rainwater keeping unit | KR-101721695-B1         | Urban Climate Impact Assessment method of Reflecting Urban Planning Scenarios and Analysis System using the same         | 0.17696129365559843 |
| KR-20180122872-A         | Rainwater management system based on rainwater keeping unit | CN-109000731-B          | The experimental rig and method that research inlet for stom water chocking-up degree influences water discharged amount | 0.17902723269642917 |
+--------------------------+-------------------------------------------------------------+-------------------------+--------------------------------------------------------------------------------------------------------------------------+---------------------+
```

## Use the `VECTOR_SEARCH` function with brute force

In this section, you use the `VECTOR_SEARCH` function to find the nearest neighbor for the embedding in the `embedding_v1` column in the `patents2` table. This query doesn't use the vector index in the search, so `VECTOR_SEARCH` finds the embedding's exact nearest neighbor.

To use `VECTOR_SEARCH` with brute force, paste the following in the query editor, and then click play\_circle **Run** :

    SELECT query.publication_number AS query_publication_number,
      query.title AS query_title,
      base.publication_number AS base_publication_number,
      base.title AS base_title,
      distance
    FROM
      VECTOR_SEARCH(
        TABLE bqml_tutorial.patents,
        'embedding_v1',
        TABLE bqml_tutorial.patents2,
        top_k => 5,
        distance_type => 'COSINE',
        options => '{"use_brute_force":true}');

The results look similar to the following:

```console
+--------------------------+-------------------------------------------------------------+-------------------------+--------------------------------------------------------------------------------------------------------------------------+---------------------+
| query_publication_number |                         query_title                         | base_publication_number |                                                        base_title                                                        |      distance       |
+--------------------------+-------------------------------------------------------------+-------------------------+--------------------------------------------------------------------------------------------------------------------------+---------------------+
| KR-20180122872-A         | Rainwater management system based on rainwater keeping unit | CN-106599080-B          | A kind of rapid generation for keeping away big vast transfer figure based on GIS                                        |  0.1447195634759062 |
| KR-20180122872-A         | Rainwater management system based on rainwater keeping unit | CN-114118544-A          | Urban waterlogging detection method and device                                                                           |  0.1747210893117136 |
| KR-20180122872-A         | Rainwater management system based on rainwater keeping unit | KR-20200048143-A        | Method and system for mornitoring dry stream using unmanned aerial vehicle                                               | 0.17561990745619782 |
| KR-20180122872-A         | Rainwater management system based on rainwater keeping unit | KR-101721695-B1         | Urban Climate Impact Assessment method of Reflecting Urban Planning Scenarios and Analysis System using the same         | 0.17696129365559843 |
| KR-20180122872-A         | Rainwater management system based on rainwater keeping unit | CN-109000731-B          | The experimental rig and method that research inlet for stom water chocking-up degree influences water discharged amount | 0.17902723269642928 |
+--------------------------+-------------------------------------------------------------+-------------------------+--------------------------------------------------------------------------------------------------------------------------+---------------------+
```

## Evaluate recall

When you perform a vector search with an index, it returns approximate results, but it reduces [recall](https://developers.google.com/machine-learning/crash-course/classification/precision-and-recall#recallsearch_term_rules) . You can compute recall by comparing the results returned by vector search with an index, and the results returned by vector search with brute force. The `publication_number` value uniquely identifies a patent, so it is used for comparison in the following query.

To evaluate recall, paste the following in the query editor, and then click play\_circle **Run** :

    WITH approx_results AS (
      SELECT query.publication_number AS query_publication_number,
        base.publication_number AS base_publication_number
      FROM
        VECTOR_SEARCH(
          TABLE bqml_tutorial.patents,
          'embedding_v1',
          TABLE bqml_tutorial.patents2,
          top_k => 5,
          distance_type => 'COSINE',
          options => '{"fraction_lists_to_search": 0.005}')
    ),
      exact_results AS (
      SELECT query.publication_number AS query_publication_number,
        base.publication_number AS base_publication_number
      FROM
        VECTOR_SEARCH(
          TABLE bqml_tutorial.patents,
          'embedding_v1',
          TABLE bqml_tutorial.patents2,
          top_k => 5,
          distance_type => 'COSINE',
          options => '{"use_brute_force":true}')
    )
    
    SELECT
      a.query_publication_number,
      SUM(CASE WHEN a.base_publication_number = e.base_publication_number THEN 1 ELSE 0 END) / 5 AS recall
    FROM exact_results e LEFT JOIN approx_results a
      ON e.query_publication_number = a.query_publication_number
    GROUP BY a.query_publication_number;

The results look like the following:

```console
+--------------------------+--------+
| query_publication_number | recall |
+--------------------------+--------+
| KR-20180122872-A         |    1.0 |
+--------------------------+--------+
```

If the recall is lower than you would like, you can increase the `fraction_lists_to_search` value, but you experience potentially higher latency and resource usage. To tune your vector search, you can try multiple runs of `VECTOR_SEARCH` with different argument values, save the results to tables, and then compare the results.

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

## What's next
