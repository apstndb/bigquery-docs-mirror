In this tutorial, you import TensorFlow models into a BigQuery ML dataset. Then, you use a SQL query to make predictions from the imported models.

## Objectives

  - Use the `  CREATE MODEL  ` statement to import TensorFlow models into BigQuery ML.
  - Use the `  ML.PREDICT  ` function to make predictions with the imported TensorFlow models.

## Costs

In this document, you use the following billable components of Google Cloud:

  - [BigQuery](https://cloud.google.com/bigquery/pricing)
  - [BigQuery ML](https://cloud.google.com/bigquery/pricing#bqml)

To generate a cost estimate based on your projected usage, use the [pricing calculator](/products/calculator) .

New Google Cloud users might be eligible for a [free trial](/free) .

When you finish the tasks that are described in this document, you can avoid continued billing by deleting the resources that you created. For more information, see [Clean up](#clean-up) .

## Before you begin

1.  Ensure that the BigQuery API is enabled.

2.  Ensure that you have the [necessary permissions](#required_permissions) to perform the tasks in this document.

### Required roles

If you create a new project, you are the project owner, and you are granted all of the required Identity and Access Management (IAM) permissions that you need to complete this tutorial.

If you are using an existing project, the [BigQuery Studio Admin](/bigquery/docs/access-control#bigquery.studioAdmin) ( `  roles/bigquery.studioAdmin  ` ) role grants all of the permissions that are needed to complete this tutorial.

Make sure that you have the following role or roles on the project: [BigQuery Studio Admin](/bigquery/docs/access-control#bigquery.studioAdmin) ( `  roles/bigquery.studioAdmin  ` ).

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

For more information about IAM permissions in BigQuery, see [BigQuery permissions](/bigquery/docs/access-control#bq-permissions) .

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

## Import a TensorFlow model

The following steps show you how to import a model from Cloud Storage. The path to the model is `  gs://cloud-training-demos/txtclass/export/exporter/1549825580/*  ` . The imported model name is `  imported_tf_model  ` .

Note the Cloud Storage URI ends in a wildcard character ( `  *  ` ). This character indicates that BigQuery ML should import any assets associated with the model.

The imported model is a TensorFlow text classifier model that predicts which website published a given article title.

To import the TensorFlow model into your dataset, follow these steps.

### Console

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  For **Create new** , click **SQL query** .

3.  In the query editor, enter this `  CREATE MODEL  ` statement, and then click **Run** .
    
    ``` text
      CREATE OR REPLACE MODEL `bqml_tutorial.imported_tf_model`
      OPTIONS (MODEL_TYPE='TENSORFLOW',
        MODEL_PATH='gs://cloud-training-demos/txtclass/export/exporter/1549825580/*')
    ```
    
    When the operation is complete, you should see a message like `  Successfully created model named imported_tf_model  ` .

4.  Your new model appears in the **Resources** panel. Models are indicated by the model icon: .

5.  If you select the new model in the **Resources** panel, information about the model appears below the **Query editor** .

### bq

1.  Import the TensorFlow model from Cloud Storage by entering the following `  CREATE MODEL  ` statement.
    
    ``` text
    bq query --use_legacy_sql=false \
    "CREATE OR REPLACE MODEL
      `bqml_tutorial.imported_tf_model`
    OPTIONS
      (MODEL_TYPE='TENSORFLOW',
        MODEL_PATH='gs://cloud-training-demos/txtclass/export/exporter/1549825580/*')"
    ```

2.  After you import the model, verify that the model appears in the dataset.
    
    ``` text
    bq ls -m bqml_tutorial
    ```
    
    The output is similar to the following:
    
    ``` text
    tableId             Type
    ------------------- -------
    imported_tf_model   MODEL
    ```

### API

[Insert a new job](/bigquery/docs/reference/rest/v2/jobs/insert) and populate the [jobs\#configuration.query](/bigquery/docs/reference/rest/v2/jobs/query) property in the request body.

``` text
{
  "query": "CREATE MODEL `PROJECT_ID:bqml_tutorial.imported_tf_model` OPTIONS(MODEL_TYPE='TENSORFLOW' MODEL_PATH='gs://cloud-training-demos/txtclass/export/exporter/1549825580/*')"
}
```

Replace `  PROJECT_ID  ` with the name of your project and dataset.

### BigQuery DataFrames

Before trying this sample, follow the BigQuery DataFrames setup instructions in the [BigQuery quickstart using BigQuery DataFrames](/bigquery/docs/dataframes-quickstart) . For more information, see the [BigQuery DataFrames reference documentation](/python/docs/reference/bigframes/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up ADC for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

Import the model by using the `  TensorFlowModel  ` object.

``` python
import bigframes
from bigframes.ml.imported import TensorFlowModel

bigframes.options.bigquery.project = PROJECT_ID
# You can change the location to one of the valid locations: https://cloud.google.com/bigquery/docs/locations#supported_locations
bigframes.options.bigquery.location = "US"

imported_tensorflow_model = TensorFlowModel(
    model_path="gs://cloud-training-demos/txtclass/export/exporter/1549825580/*"
)
```

For more information about importing TensorFlow models into BigQuery ML, including format and storage requirements, see the [`  CREATE MODEL  ` statement for importing TensorFlow models](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-tensorflow) .

## Make predictions with the imported TensorFlow model

After importing the TensorFlow model, you use the [`  ML.PREDICT  ` function](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-predict) to make predictions with the model.

The following query uses `  imported_tf_model  ` to make predictions using input data from the `  full  ` table in the public dataset `  hacker_news  ` . In the query, the TensorFlow model's `  serving_input_fn  ` function specifies that the model expects a single input string named `  input  ` . The subquery assigns the alias `  input  ` to the `  title  ` column in the subquery's `  SELECT  ` statement.

To make predictions with the imported TensorFlow model, follow these steps.

### Console

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  Under **Create new** , click **SQL query** .

3.  In the query editor, enter this query that uses the `  ML.PREDICT  ` function.
    
    ``` text
    SELECT *
      FROM ML.PREDICT(MODEL `bqml_tutorial.imported_tf_model`,
        (
         SELECT title AS input
         FROM bigquery-public-data.hacker_news.full
        )
    )
    ```
    
    The query results should look like this:

### bq

Enter this command to run the query that uses `  ML.PREDICT  ` .

``` text
bq query \
--use_legacy_sql=false \
'SELECT *
FROM ML.PREDICT(
  MODEL `bqml_tutorial.imported_tf_model`,
  (SELECT title AS input FROM `bigquery-public-data.hacker_news.full`))'
```

The results should look like this:

``` console
+------------------------------------------------------------------------+----------------------------------------------------------------------------------+
|                               dense_1                                  |                                       input                                      |
+------------------------------------------------------------------------+----------------------------------------------------------------------------------+
|   ["0.6251608729362488","0.2989124357700348","0.07592673599720001"]    | How Red Hat Decides Which Open Source Companies t...                             |
|   ["0.014276246540248394","0.972910463809967","0.01281337533146143"]   | Ask HN: Toronto/GTA mastermind around side income for big corp. dev?             |
|   ["0.9821603298187256","1.8601855117594823E-5","0.01782100833952427"] | Ask HN: What are good resources on strategy and decision making for your career? |
|   ["0.8611106276512146","0.06648492068052292","0.07240450382232666"]   | Forget about promises, use harvests                                              |
+------------------------------------------------------------------------+----------------------------------------------------------------------------------+
```

### API

[Insert a new job](/bigquery/docs/reference/rest/v2/jobs/insert) and populate the [jobs\#configuration.query](/bigquery/docs/reference/rest/v2/jobs/query) property as in the request body. Replace `  project_id  ` with the name of your project.

``` text
{
  "query": "SELECT * FROM ML.PREDICT(MODEL `project_id.bqml_tutorial.imported_tf_model`, (SELECT * FROM input_data))"
}
```

### BigQuery DataFrames

Before trying this sample, follow the BigQuery DataFrames setup instructions in the [BigQuery quickstart using BigQuery DataFrames](/bigquery/docs/dataframes-quickstart) . For more information, see the [BigQuery DataFrames reference documentation](/python/docs/reference/bigframes/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up ADC for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

Use the [`  predict  `](/python/docs/reference/bigframes/latest/bigframes.ml.llm.PaLM2TextGenerator#bigframes_ml_llm_PaLM2TextGenerator_predict) function to run the TensorFlow model:

``` python
import bigframes.pandas as bpd

df = bpd.read_gbq("bigquery-public-data.hacker_news.full")
df_pred = df.rename(columns={"title": "input"})
predictions = imported_tensorflow_model.predict(df_pred)
predictions.head(5)
```

The results should look like this:

In the query results, the `  dense_1  ` column contains an array of probability values, and the `  input  ` column contains the corresponding string values from the input table. Each array element value represents the probability that the corresponding input string is an article title from a particular publication.

## Clean up

To avoid incurring charges to your Google Cloud account for the resources used in this tutorial, either delete the project that contains the resources, or keep the project and delete the individual resources.

### Delete the project

### Console

**Caution** : Deleting a project has the following effects:

  - **Everything in the project is deleted.** If you used an existing project for the tasks in this document, when you delete it, you also delete any other work you've done in the project.
  - **Custom project IDs are lost.** When you created this project, you might have created a custom project ID that you want to use in the future. To preserve the URLs that use the project ID, such as an `  appspot.com  ` URL, delete selected resources inside the project instead of deleting the whole project.

If you plan to explore multiple architectures, tutorials, or quickstarts, reusing projects can help you avoid exceeding project quota limits.

In the Google Cloud console, go to the **Manage resources** page.

In the project list, select the project that you want to delete, and then click **Delete** .

In the dialog, type the project ID, and then click **Shut down** to delete the project.

### gcloud

**Caution** : Deleting a project has the following effects:

  - **Everything in the project is deleted.** If you used an existing project for the tasks in this document, when you delete it, you also delete any other work you've done in the project.
  - **Custom project IDs are lost.** When you created this project, you might have created a custom project ID that you want to use in the future. To preserve the URLs that use the project ID, such as an `  appspot.com  ` URL, delete selected resources inside the project instead of deleting the whole project.

If you plan to explore multiple architectures, tutorials, or quickstarts, reusing projects can help you avoid exceeding project quota limits.

In the Google Cloud console, go to the **Manage resources** page.

In the project list, select the project that you want to delete, and then click **Delete** .

In the dialog, type the project ID, and then click **Shut down** to delete the project.

### Delete individual resources

Alternatively, remove the individual resources used in this tutorial:

1.  [Delete the imported model](/bigquery/docs/deleting-models) .

2.  Optional: [Delete the dataset](/bigquery/docs/managing-datasets#delete-datasets) .

## What's next

  - For an overview of BigQuery ML, see [Introduction to BigQuery ML](/bigquery/docs/bqml-introduction) .
  - To get started using BigQuery ML, see [Create machine learning models in BigQuery ML](/bigquery/docs/create-machine-learning-model) .
  - For more information about importing TensorFlow models, see [The `  CREATE MODEL  ` statement for importing TensorFlow models](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-tensorflow) .
  - For more information about working with models, see these resources:
      - [Get model metadata](/bigquery/docs/getting-model-metadata)
      - [Update model metadata](/bigquery/docs/updating-model-metadata)
      - [Manage models](/bigquery/docs/managing-models)
  - For more information on using the BigQuery DataFrames API in a BigQuery notebook, see:
      - [Introduction to BigQuery notebooks](/bigquery/docs/notebooks-introduction)
      - [Overview of BigQuery DataFrames](/python/docs/reference/bigframes/latest)
