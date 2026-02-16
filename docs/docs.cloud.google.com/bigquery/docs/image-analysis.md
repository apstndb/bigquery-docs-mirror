# Analyze images with a Gemini model

This tutorial shows you how to create a BigQuery ML [remote model](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model) that is based on the [`  gemini-2.5-flash  ` model](/vertex-ai/generative-ai/docs/learn/models#gemini-models) , and then use that model with the [`  AI.GENERATE_TEXT  ` function](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate-text) functions to analyze a set of movie poster images.

This tutorial covers the following tasks:

  - Creating a [BigQuery object table](/bigquery/docs/object-table-introduction) over image data in a Cloud Storage bucket.
  - Creating a BigQuery ML remote model that targets the Vertex AI `  gemini-2.5-flash  ` model.
  - Using the remote model with the `  AI.GENERATE_TEXT  ` function to identify the movies associated with a set of movie posters.

The movie poster data is available from the public Cloud Storage bucket `  gs://cloud-samples-data/vertex-ai/dataset-management/datasets/classic-movie-posters  ` .

## Required roles

To run this tutorial, you need the following Identity and Access Management (IAM) roles:

  - Create and use BigQuery datasets, connections, and models: BigQuery Admin ( `  roles/bigquery.admin  ` ).
  - Grant permissions to the connection's service account: Project IAM Admin ( `  roles/resourcemanager.projectIamAdmin  ` ).

These predefined roles contain the permissions required to perform the tasks in this document. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

  - Create a dataset: `  bigquery.datasets.create  `
  - Create, delegate, and use a connection: `  bigquery.connections.*  `
  - Set the default connection: `  bigquery.config.*  `
  - Set service account permissions: `  resourcemanager.projects.getIamPolicy  ` and `  resourcemanager.projects.setIamPolicy  `
  - Create an object table: `  bigquery.tables.create  ` and `  bigquery.tables.update  `
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
  - **Vertex AI** : You incur costs for calls to the Vertex AI model that is represented by the BigQuery remote model.

To generate a cost estimate based on your projected usage, use the [pricing calculator](/products/calculator) .

New Google Cloud users might be eligible for a [free trial](/free) .

For more information about BigQuery pricing, see [BigQuery pricing](https://cloud.google.com/bigquery/pricing) in the BigQuery documentation.

For more information about Vertex AI generative AI pricing, see the [Vertex AI pricing](/vertex-ai/generative-ai/pricing) page.

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

## Create the object table

Create an object table over the movie poster images in the public Cloud Storage [bucket](https://console.cloud.google.com/storage/browser/cloud-samples-data/vertex-ai/dataset-management/datasets/classic-movie-posters;tab=objects?prefix=&forceOnObjectsSortingFiltering=false) . The object table makes it possible to analyze the images without moving them from Cloud Storage.

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, run the following query to create the object table:
    
    ``` text
    CREATE OR REPLACE EXTERNAL TABLE `bqml_tutorial.movie_posters`
      WITH CONNECTION DEFAULT
      OPTIONS (
        object_metadata = 'SIMPLE',
        uris =
          ['gs://cloud-samples-data/vertex-ai/dataset-management/datasets/classic-movie-posters/*']);
    ```

## Create the remote model

Create a remote model that represents a Vertex AI `  gemini-2.5-flash  ` model:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, run the following query to create the remote model:
    
    ``` text
    CREATE OR REPLACE MODEL `bqml_tutorial.gemini-vision`
      REMOTE WITH CONNECTION DEFAULT
      OPTIONS (ENDPOINT = 'gemini-2.5-flash');
    ```
    
    The query takes several seconds to complete, after which the `  gemini-vision  ` model appears in the `  bqml_tutorial  ` dataset in the **Explorer** pane. Because the query uses a `  CREATE MODEL  ` statement to create a model, there are no query results.

## Analyze the movie posters

Use the remote model to analyze the movie posters and determine what movie each poster represents, and then write this data to a table.

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, run the following query to analyze the movie poster images:
    
    ``` text
    CREATE OR REPLACE TABLE
      `bqml_tutorial.movie_posters_results` AS (
      SELECT
        uri,
       result
      FROM
        AI.GENERATE_TEXT( MODEL `bqml_tutorial.gemini-vision`,
          TABLE `bqml_tutorial.movie_posters`,
          STRUCT( 0.2 AS temperature,
            'For the movie represented by this poster, what is the movie title and year of release? Answer in JSON format with two keys: title, year. title should be string, year should be integer.' AS PROMPT)));
        
    ```

3.  In the query editor, run the following statement to view the table data:
    
    ``` text
    SELECT * FROM `bqml_tutorial.movie_posters_results`;
    ```
    
    The output is similar to the following:
    
    ``` console
    +--------------------------------------------+----------------------------------+
    | uri                                        | result                           |
    +--------------------------------------------+----------------------------------+
    | gs://cloud-samples-data/vertex-ai/dataset- | json                          |
    | management/datasets/classic-movie-         | {                                |
    | posters/little_annie_rooney.jpg            |  "title": "Little Annie Rooney", |
    |                                            |  "year": 1912                    |
    |                                            | }                                |
    |                                            |                              |
    +--------------------------------------------+----------------------------------+
    | gs://cloud-samples-data/vertex-ai/dataset- | json                          |
    | management/datasets/classic-movie-         | {                                |
    | posters/mighty_like_a_mouse.jpg            |  "title": "Mighty Like a Moose", |
    |                                            |  "year": 1926                    |
    |                                            | }                                |
    |                                            |                              |
    +--------------------------------------------+----------------------------------+
    | gs://cloud-samples-data/vertex-ai/dataset- | json                          |
    | management/datasets/classic-movie-         | {                                |
    | posters/brown_of_harvard.jpeg              |  "title": "Brown of Harvard",    |
    |                                            |  "year": 1926                    |
    |                                            | }                                |
    |                                            |                              |
    +--------------------------------------------+----------------------------------+
    ```

## Format the model output

Format the movie analysis data returned by the model to make the movie title and year data more readable.

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, run the following query to format the data:
    
    ```` text
    CREATE OR REPLACE TABLE
      `bqml_tutorial.movie_posters_results_formatted` AS (
      SELECT
        uri,
        JSON_QUERY(RTRIM(LTRIM(results.result, " ```json"), "```"), "$.title") AS title,
        JSON_QUERY(RTRIM(LTRIM(results.result, " ```json"), "```"), "$.year") AS year
      FROM
        `bqml_tutorial.movie_posters_results` results );
    ````

3.  In the query editor, run the following statement to view the table data:
    
    ``` text
    SELECT * FROM `bqml_tutorial.movie_posters_results_formatted`;
    ```
    
    The output is similar to the following:
    
    ``` console
    +--------------------------------------------+----------------------------+------+
    | uri                                        | title                      | year |
    +--------------------------------------------+----------------------------+------+
    | gs://cloud-samples-data/vertex-ai/dataset- | "Barque sortant du port"   | 1895 |
    | management/datasets/classic-movie-         |                            |      |
    | posters/barque_sortant_du_port.jpeg        |                            |      |
    +--------------------------------------------+----------------------------+------+
    | gs://cloud-samples-data/vertex-ai/dataset- | "The Great Train Robbery"  | 1903 |
    | management/datasets/classic-movie-         |                            |      |
    | posters/the_great_train_robbery.jpg        |                            |      |
    +--------------------------------------------+----------------------------+------+
    | gs://cloud-samples-data/vertex-ai/dataset- | "Little Annie Rooney"      | 1912 |
    | management/datasets/classic-movie-         |                            |      |
    | posters/little_annie_rooney.jpg            |                            |      |
    +--------------------------------------------+----------------------------+------+
    ```

## Clean up

**Caution** : Deleting a project has the following effects:

  - **Everything in the project is deleted.** If you used an existing project for the tasks in this document, when you delete it, you also delete any other work you've done in the project.
  - **Custom project IDs are lost.** When you created this project, you might have created a custom project ID that you want to use in the future. To preserve the URLs that use the project ID, such as an `  appspot.com  ` URL, delete selected resources inside the project instead of deleting the whole project.

If you plan to explore multiple architectures, tutorials, or quickstarts, reusing projects can help you avoid exceeding project quota limits.

In the Google Cloud console, go to the **Manage resources** page.

In the project list, select the project that you want to delete, and then click **Delete** .

In the dialog, type the project ID, and then click **Shut down** to delete the project.
