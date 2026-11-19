---
name: documents/docs.cloud.google.com/bigquery/docs/translate-text
uri: https://docs.cloud.google.com/bigquery/docs/translate-text
title: Translate text with the AI.TRANSLATE function
description: Use the AI.TRANSLATE function with the Cloud Translation API to translate text in BigQuery.
data_source: docs.cloud.google.com
---

The [`AI.TRANSLATE` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-translate) lets you translate text between languages directly in BigQuery. For example, you can localize product catalogs, translate customer feedback for global support teams, or standardize multilingual survey responses without building separate data pipelines. The function connects BigQuery to the Cloud Translation API by using your end-user credentials, so you don't need to create a connection or a remote model.

In this tutorial, you create a sample table of multilingual customer feedback, translate text into English with automatic language detection, inspect translation metadata, and translate movie reviews into Spanish by using the [Translation LLM](https://docs.cloud.google.com/translate/docs/translation-llm) model.

## Objectives

- Create a dataset and a sample table of multilingual text.
- Translate multilingual text into English with automatic language detection.
- Return translation metadata and detected source language codes.
- Translate nuanced text by using the Translation LLM model.

## Costs

In this document, you use the following billable components of Google Cloud:

- **BigQuery.** You incur costs for the data that you process in BigQuery.
- **Cloud Translation.** You incur costs for calls to the Cloud Translation API.

To generate a cost estimate based on your projected usage, use the [pricing calculator](https://docs.cloud.google.com/products/calculator) .

New Google Cloud users might be eligible for a [free trial](https://docs.cloud.google.com/free) .

For more information, see [BigQuery pricing](https://cloud.google.com/bigquery/pricing) and [Translation pricing](https://cloud.google.com/translate/pricing) .

## Before you begin

### Console

1.  Make sure that you have the following role or roles on the project: **BigQuery Data Editor** , **BigQuery Job User** , **Cloud Translation API User** .

    #### Check for the roles

    1.  In the Google Cloud console, go to the **IAM** page.

    2.  Select the project.

    3.  In the **Principal** column, find all rows that identify you or a group that you're included in. To learn which groups you're included in, contact your administrator.

    4.  For all rows that specify or include you, check the **Role** column to see whether the list of roles includes the required roles.

    #### Grant the roles

    1.  In the Google Cloud console, go to the **IAM** page.

    2.  Select the project.

    3.  Click **Grant access** .

    4.  In the **New principals** field, enter your user identifier. This is typically the email address for a Google Account.

    5.  Click **Select a role** , then search for the role.

    6.  To grant additional roles, click **Add another role** and add each additional role.

    7.  Click **Save** .

### gcloud

1.  Grant roles to your user account. Run the following command once for each of the following IAM roles: `roles/bigquery.dataEditor, roles/bigquery.jobUser, roles/cloudtranslate.user`

    ```
    gcloud projects add-iam-policy-binding PROJECT_ID --member="user:USER_IDENTIFIER" --role=ROLE
    ```

    Replace the following:

    - `PROJECT_ID` : Your project ID.
    - `USER_IDENTIFIER` : The identifier for your user account. For example, `myemail@example.com` .
    - `ROLE` : The IAM role that you grant to your user account.

## Create a dataset

To create a BigQuery dataset, select one of the following options:

### Console

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click **Explorer** :

    ![Highlighted button for the Explorer pane.](https://docs.cloud.google.com/static/bigquery/images/explorer-tab.png)

    If you don't see the left pane, click **Expand left pane** to open the pane.

3.  In **Explorer** , expand your project, and then click **Datasets** .

4.  On the **Datasets** page, click **Create dataset** .

5.  In the **Create dataset** pane, do the following:

    - For **Dataset ID** , enter `bqml_tutorial` .

    - For **Data location** , select **US** .

    Leave the remaining default settings as they are.

6.  Click **Create dataset** .

### bq

To create a new dataset, use the [`bq mk --dataset` command](https://docs.cloud.google.com/bigquery/docs/reference/bq-cli-reference#mk-dataset) .

1.  Create a dataset named `bqml_tutorial` with the data location set to `US` :

    ```
    bq mk --dataset \
      --location=US \
      --description "BigQuery ML tutorial dataset." \
      bqml_tutorial
    ```

2.  Confirm that the dataset was created:

    ```
    bq ls
    ```

### API

Call the [`datasets.insert`](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/datasets/insert) method with a defined [dataset resource](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/datasets) :

```
{
  "datasetReference": {
     "datasetId": "bqml_tutorial"
  }
}
```

## Create a sample table

Use the [`CREATE TABLE` statement](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_table_statement) to create a table of multilingual customer feedback in the `bqml_tutorial` dataset:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, run the following statement:

    ```
    CREATE OR REPLACE TABLE `bqml_tutorial.customer_feedback` AS (
      SELECT
        *
      FROM
        UNNEST(
          [
            STRUCT<feedback_id INT64, feedback_text STRING>(
              1, 'El servicio de entrega fue rápido y confiable.'),
            (2, 'Je suis très satisfait de la qualité de ce produit.'),
            (3, 'Die Benutzeroberfläche der App ist sehr übersichtlich.'),
            (4, 'O suporte ao cliente resolveu meu problema com rapidez.')
          ])
    );
    ```

## Translate multilingual text

Use the [`AI.TRANSLATE` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-translate) to translate the customer feedback into English ( `en` ). When you omit the `source_language` argument, the Cloud Translation API automatically detects the source language of each row and translates the text by using the default [Neural Machine Translation (NMT)](https://docs.cloud.google.com/translate/docs/advanced/nmt-model) model:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, run the following statement to translate the feedback into English:

    ```
    SELECT
      feedback_id,
      feedback_text,
      AI.TRANSLATE(feedback_text, 'en') AS translated_text
    FROM
      `bqml_tutorial.customer_feedback`;
    ```

    For a list of valid target language codes, see the [supported languages](https://docs.cloud.google.com/translate/docs/languages) .

    The output is similar to the following:

    ```console
    +-------------+-----------------------------+-----------------------------+
    | feedback_id | feedback_text               | translated_text             |
    +-------------+-----------------------------+-----------------------------+
    | 1           | El servicio de entrega fue  | The delivery service was    |
    |             | rápido y confiable.         | fast and reliable.          |
    +-------------+-----------------------------+-----------------------------+
    | 2           | Je suis très satisfait de   | I am very satisfied with    |
    |             | la qualité de ce produit.   | the quality of this         |
    |             |                             | product.                    |
    +-------------+-----------------------------+-----------------------------+
    | 3           | Die Benutzeroberfläche der  | The app's user interface is |
    |             | App ist sehr übersichtlich. | very clear.                 |
    +-------------+-----------------------------+-----------------------------+
    | 4           | O suporte ao cliente        | Customer support resolved   |
    |             | resolveu meu problema com   | my issue quickly.           |
    |             | rapidez.                    |                             |
    +-------------+-----------------------------+-----------------------------+
    ```

## Return translation details and detected languages

When you process text from multiple regions, you might want to record the detected source language alongside each translation or check for per-row errors. Set `return_details => TRUE` in the [`AI.TRANSLATE` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-translate) to return a `STRUCT` value that includes the translated text, execution status, and API response metadata:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, run the following statement to extract the detected language code, translated text, and status for each row:

    ```
    WITH
      translations AS (
        SELECT
          feedback_id,
          AI.TRANSLATE(
            feedback_text,
            'en',
            return_details => TRUE) AS translation
        FROM
          `bqml_tutorial.customer_feedback`
      )
    SELECT
      feedback_id,
      STRING(translation.details.detected_language_code) AS detected_language,
      translation.result AS translated_text,
      translation.status
    FROM
      translations;
    ```

    The output is similar to the following:

    ```console
    +-------------+-------------------+-----------------------------+--------+
    | feedback_id | detected_language | translated_text             | status |
    +-------------+-------------------+-----------------------------+--------+
    | 1           | es                | The delivery service was    | OK     |
    |             |                   | fast and reliable.          |        |
    +-------------+-------------------+-----------------------------+--------+
    | 2           | fr                | I am very satisfied with    | OK     |
    |             |                   | the quality of this         |        |
    |             |                   | product.                    |        |
    +-------------+-------------------+-----------------------------+--------+
    | 3           | de                | The app's user interface is | OK     |
    |             |                   | very clear.                 |        |
    +-------------+-------------------+-----------------------------+--------+
    | 4           | pt                | Customer support resolved   | OK     |
    |             |                   | my issue quickly.           |        |
    +-------------+-------------------+-----------------------------+--------+
    ```

    When `return_details` is set to `TRUE` , the returned `STRUCT` contains the following fields:

    - `result` : a `STRING` value that contains the translated text, or `NULL` if an error occurs.
    - `status` : a `STRING` value that contains `OK` when the operation succeeds, or an error message if an error occurs.
    - `details` : a `JSON` value that contains the Cloud Translation API response for the row, including `detected_language_code` when the source language is detected automatically, or error details if an error occurs.

## Translate text with the Translation LLM

For text that contains informal language, slang, or complex sentiment, such as customer or movie reviews, set `model => 'translation-llm'` in the [`AI.TRANSLATE` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-translate) to use the [Translation LLM](https://docs.cloud.google.com/translate/docs/translation-llm) model instead of the default NMT model. When you know the language of the input column, you can also specify the `source_language` argument:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, run the following statement to translate five English movie reviews from a public dataset into Spanish ( `es` ):

    ```
    SELECT
      review,
      AI.TRANSLATE(
        review,
        'es',
        source_language => 'en',
        model => 'translation-llm') AS translated_review
    FROM
      `bigquery-public-data.imdb.reviews`
    LIMIT 5;
    ```

    The output is similar to the following:

    ```console
    +------------------------------------+------------------------------------+
    | review                             | translated_review                  |
    +------------------------------------+------------------------------------+
    | Once again Mr. Costner has dragged | Una vez más, el Sr. Costner ha     |
    | out a movie for far longer than... | alargado una película mucho más... |
    +------------------------------------+------------------------------------+
    | This movie is amazing because the  | Esta película es increíble porque  |
    | fact that real people portray...   | las personas reales se...          |
    +------------------------------------+------------------------------------+
    | ...                                | ...                                |
    +------------------------------------+------------------------------------+
    ```

## Clean up

To avoid incurring charges to your Google Cloud account for the resources used in this tutorial, either delete the project that contains the resources, or keep the project and delete the individual resources.

### Delete the project

> **Caution** : Deleting a project has the following effects:
>
> - **Everything in the project is deleted.** If you used an existing project for the tasks in this document, when you delete it, you also delete any other work you've done in the project.
> - **Custom project IDs are lost.** When you created this project, you might have created a custom project ID that you want to use in the future. To preserve the URLs that use the project ID, such as an `appspot.com` URL, delete selected resources inside the project instead of deleting the whole project.
>
> If you plan to explore multiple architectures, tutorials, or quickstarts, reusing projects can help you avoid exceeding project quota limits.

Delete a Google Cloud project:

```
gcloud projects delete PROJECT_ID
```

### Delete individual resources

If you want to reuse the project, delete the dataset that you created for this tutorial:

### Console

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  Delete the `bqml_tutorial` dataset. Deleting the dataset also deletes the `customer_feedback` table:

    1.  In the **Explorer** pane, expand your project, and then click **Datasets** .

    2.  In the **Datasets** list, click the `bqml_tutorial` dataset.

    3.  In the details pane, click **Delete** .

    4.  In the **Delete dataset** dialog, click **Delete** .

### gcloud

- Delete the `bqml_tutorial` dataset and the `customer_feedback` table:

```
bq rm --dataset --recursive bqml_tutorial
```

## What's next

- Learn more about the [`AI.TRANSLATE` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-translate) .
- Learn more about the [Translation LLM](https://docs.cloud.google.com/translate/docs/translation-llm) and [Neural Machine Translation](https://docs.cloud.google.com/translate/docs/advanced/nmt-model) models.
- Compare text analysis options in [Choose a natural language processing function](https://docs.cloud.google.com/bigquery/docs/choose-ml-text-function) .
- Learn more about [generative AI in BigQuery](https://docs.cloud.google.com/bigquery/docs/generative-ai-overview) .
- See supported SQL statements and functions in [End-to-end user journeys for generative AI models](https://docs.cloud.google.com/bigquery/docs/e2e-journey-genai) .
