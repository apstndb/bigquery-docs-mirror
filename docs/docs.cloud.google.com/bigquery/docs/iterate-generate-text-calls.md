---
name: documents/docs.cloud.google.com/bigquery/docs/iterate-generate-text-calls
uri: https://docs.cloud.google.com/bigquery/docs/iterate-generate-text-calls
title: Handle quota errors by calling ML.GENERATE_TEXT iteratively
description: Create a remote model and iterate through calls to the ML.GENERATE_TEXT function using a public stored procedure to handle quota errors.
data_source: docs.cloud.google.com
---

The BigQuery `bqutil.procedure.bqml_generate_text` public stored procedure lets you iterate through batch calls to the [`ML.GENERATE_TEXT` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-generate-text) so you can process large datasets without exceeding endpoint [quotas and limits](https://docs.cloud.google.com/bigquery/quotas#generative_ai_functions) . Because BigQuery query jobs finish even when the function fails on individual rows, high request volumes can leave `RESOURCE EXHAUSTED` retryable errors in your output table. In this tutorial, you create a remote model and run the stored procedure to iteratively retry failed rows until all records in a public news dataset are processed.

To review the source code for the stored procedure in GitHub, see [`bqml_generate_text.sqlx`](https://github.com/GoogleCloudPlatform/bigquery-utils/blob/master/stored_procedures/definitions/bqml_generate_text.sqlx) . For more information about the stored procedure parameters and usage, see the [README file](https://github.com/GoogleCloudPlatform/bigquery-utils/blob/master/stored_procedures/README.md#bqml_generate_text-source_table-string-target_table-string-ml_model-string-prompt_column-string-key_columns-array-options_string-string) .

## Objectives

- Create a BigQuery dataset.
- Create a BigQuery ML [remote model](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model) over a `gemini-3.5-flash-lite` model.
- Run the `bqutil.procedure.bqml_generate_text` stored procedure to iteratively generate text from the `bigquery-public-data.bbc_news.fulltext` public dataset.
- Verify the generated text results and confirm that no retryable quota errors remain.

## Costs

In this document, you use the following billable components of Google Cloud:

- **BigQuery ML** : You incur costs for the data that you process in BigQuery.
- **Gemini Enterprise Agent Platform** : You incur costs for calls to the Agent Platform model.

To generate a cost estimate based on your projected usage, use the [pricing calculator](https://docs.cloud.google.com/products/calculator) .

New Google Cloud users might be eligible for a [free trial](https://docs.cloud.google.com/free) .

For more information, see [BigQuery pricing](https://cloud.google.com/bigquery/pricing) and [Agent Platform pricing](https://docs.cloud.google.com/vertex-ai/generative-ai/pricing) .

## Before you begin

1.  Enable the BigQuery, BigQuery Connection, and Agent Platform API APIs, if any are not already enabled.

    **Roles required to enable APIs**

    To enable APIs, you need the `serviceusage.services.enable` permission. If you created the project, then you likely already have this permission through the Owner role ( `roles/owner` ). Otherwise, you can get this permission through the Service Usage Admin role ( `roles/serviceusage.serviceUsageAdmin` ). [Learn how to grant roles](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

### Required roles

To get the permissions that you need to complete this tutorial, ask your administrator to grant you the following IAM roles:

- Create and use BigQuery datasets, connections, and models: [BigQuery Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin) ( `roles/bigquery.admin` ) on your project
- Grant permissions to the connection's service account: [Project IAM Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/resourcemanager#resourcemanager.projectIamAdmin) ( `roles/resourcemanager.projectIamAdmin` ) on your project

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

These predefined roles contain the permissions required to complete this tutorial. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

The following permissions are required to complete this tutorial:

- Create a dataset: `bigquery.datasets.create`
- Create, delegate, and use a connection: `bigquery.connections.*`
- Set the default connection: `bigquery.config.*`
- Set service account permissions:
  - `resourcemanager.projects.getIamPolicy`
  - `resourcemanager.projects.setIamPolicy`
- Create a model and run inference:
  - `bigquery.jobs.create`
  - `bigquery.models.create`
  - `bigquery.models.getData`
  - `bigquery.models.updateData`
  - `bigquery.models.updateMetadata`

You might also be able to get these permissions with [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## Create a dataset

To create a BigQuery dataset, select one of the following options:

### Console

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :

    ![Highlighted button for the Explorer pane.](https://docs.cloud.google.com/static/bigquery/images/explorer-tab.png)

    If you don't see the left pane, click last_page **Expand left pane** to open the pane.

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

## Create the remote model

Use the [`CREATE MODEL` statement](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model) to create a remote model that represents a hosted Agent Platform `gemini-3.5-flash-lite` model:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, run the following statement:

    ```
    CREATE OR REPLACE MODEL `bqml_tutorial.generate_text`
      REMOTE WITH CONNECTION DEFAULT
      OPTIONS (ENDPOINT = 'gemini-3.5-flash-lite');
    ```

    The query takes several seconds to complete, after which the `generate_text` model appears in the `bqml_tutorial` dataset in the **Explorer** pane. Because the query uses a `CREATE MODEL` statement to create a model, there are no query results.

## Run the stored procedure

Use the [`CALL` statement](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/procedural-language#call) to run the `bqutil.procedure.bqml_generate_text` stored procedure. This stored procedure iterates through calls to the [`ML.GENERATE_TEXT` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-generate-text) by using the `bqml_tutorial.generate_text` model and the `bigquery-public-data.bbc_news.fulltext` public table:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, run the following statement:

    ```
    CALL `bqutil.procedure.bqml_generate_text`(
        "bigquery-public-data.bbc_news.fulltext",          -- source table
        "PROJECT_ID.bqml_tutorial.news_generated_text",  -- destination table
        "PROJECT_ID.bqml_tutorial.generate_text",        -- model
        "body",                                            -- prompt column
        ["filename"],                                      -- key columns
        '{"flatten_json_output": true}'                    -- optional arguments
    );
    ```

    Replace `PROJECT_ID` with your project ID.

    The stored procedure creates the `bqml_tutorial.news_generated_text` table to contain the output of the `ML.GENERATE_TEXT` function.

3.  When the query finishes running, confirm that there are no rows in the `bqml_tutorial.news_generated_text` table that contain a retryable error. In the query editor, run the following statement:

    ```
    SELECT *
    FROM `bqml_tutorial.news_generated_text`
    WHERE ml_generate_text_status LIKE '%A retryable error occurred%';
    ```

    The query returns the message `There is no data to display` .

4.  In the query editor, run the following statement to inspect a sample of the generated text results:

    ```
    SELECT
      filename,
      prompt,
      ml_generate_text_llm_result,
      ml_generate_text_status
    FROM `bqml_tutorial.news_generated_text`
    LIMIT 3;
    ```

    The output is similar to the following:

    ```console
    +------------------------+------------------------------------------+-----------------------------------------------------------+-------------------------+
    | filename               | prompt                                   | ml_generate_text_llm_result                               | ml_generate_text_status |
    +------------------------+------------------------------------------+-----------------------------------------------------------+-------------------------+
    | bbc/tech/209.txt       | A 20-year-old US man is selling...       | It looks like you shared a news article about Andrew...   |                         |
    | bbc/business/375.txt   | South Korea's largest credit card...     | It looks like you shared a news article about the 2004... |                         |
    | bbc/sport/139.txt      | A brave defensive display, led by...     | It looks like you have shared a match report from a...    |                         |
    +------------------------+------------------------------------------+-----------------------------------------------------------+-------------------------+
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

If you want to reuse the project, then delete the resources that you created for this tutorial:

### Console

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  Delete the `bqml_tutorial` dataset. Deleting the dataset also deletes the remote model and the output table:

    1.  In the **Explorer** pane, expand your project and click **Datasets** .

    2.  In the **Datasets** list, click the `bqml_tutorial` dataset.

    3.  In the details pane, click delete **Delete** .

    4.  In the **Delete dataset** dialog, click **Delete** .

### bq

Delete the `bqml_tutorial` dataset, the remote model, and the output table:

```
bq rm --dataset --recursive bqml_tutorial
```

## What's next

- Learn more about the [`ML.GENERATE_TEXT` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-generate-text) and the [`AI.GENERATE_TEXT` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate-text) .
- Learn more about [generative AI in BigQuery](https://docs.cloud.google.com/bigquery/docs/generative-ai-overview) .
- Learn how to [choose a text generation function](https://docs.cloud.google.com/bigquery/docs/choose-text-generation-function) .
