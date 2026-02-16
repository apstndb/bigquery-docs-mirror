# Generate text with the AI.GENERATE function

This tutorial shows you how to generate text from text or multimodal data by using the [`  AI.GENERATE  ` function](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate) . With the `  AI.GENERATE  ` function, you use a [Cloud resource connection](/bigquery/docs/create-cloud-resource-connection) to connect to a hosted Gemini model so that you don't have to create and maintain a model of your own.

This tutorial shows you how to complete the following tasks:

  - Summarize text content and output results in the function's default format.
  - Summarize text content and output structured results.
  - Transcribe and translate video content.
  - Analyze audio file content.

## Costs

In this document, you use the following billable components of Google Cloud:

  - **BigQuery ML** : You incur costs for the data that you process in BigQuery.
  - **Vertex AI** : You incur costs for calls to the Vertex AI model.

To generate a cost estimate based on your projected usage, use the [pricing calculator](/products/calculator) .

New Google Cloud users might be eligible for a [free trial](/free) .

For more information about BigQuery pricing, see [BigQuery pricing](https://cloud.google.com/bigquery/pricing) in the BigQuery documentation.

For more information about Vertex AI generative AI pricing, see the [Vertex AI pricing](/vertex-ai/generative-ai/pricing) page.

## Before you begin

Sign in to your Google Cloud account. If you're new to Google Cloud, [create an account](https://console.cloud.google.com/freetrial) to evaluate how our products perform in real-world scenarios. New customers also get $300 in free credits to run, test, and deploy workloads.

In the Google Cloud console, on the project selector page, select or create a Google Cloud project.

**Roles required to select or create a project**

  - **Select a project** : Selecting a project doesn't require a specific IAM role—you can select any project that you've been granted a role on.
  - **Create a project** : To create a project, you need the Project Creator role ( `  roles/resourcemanager.projectCreator  ` ), which contains the `  resourcemanager.projects.create  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .

**Note** : If you don't plan to keep the resources that you create in this procedure, create a project instead of selecting an existing project. After you finish these steps, you can delete the project, removing all resources associated with the project.

[Verify that billing is enabled for your Google Cloud project](/billing/docs/how-to/verify-billing-enabled#confirm_billing_is_enabled_on_a_project) .

Enable the BigQuery API.

**Roles required to enable APIs**

To enable APIs, you need the Service Usage Admin IAM role ( `  roles/serviceusage.serviceUsageAdmin  ` ), which contains the `  serviceusage.services.enable  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .

In the Google Cloud console, on the project selector page, select or create a Google Cloud project.

**Roles required to select or create a project**

  - **Select a project** : Selecting a project doesn't require a specific IAM role—you can select any project that you've been granted a role on.
  - **Create a project** : To create a project, you need the Project Creator role ( `  roles/resourcemanager.projectCreator  ` ), which contains the `  resourcemanager.projects.create  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .

**Note** : If you don't plan to keep the resources that you create in this procedure, create a project instead of selecting an existing project. After you finish these steps, you can delete the project, removing all resources associated with the project.

[Verify that billing is enabled for your Google Cloud project](/billing/docs/how-to/verify-billing-enabled#confirm_billing_is_enabled_on_a_project) .

Enable the BigQuery API.

**Roles required to enable APIs**

To enable APIs, you need the Service Usage Admin IAM role ( `  roles/serviceusage.serviceUsageAdmin  ` ), which contains the `  serviceusage.services.enable  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .

BigQuery is automatically enabled in new projects. To activate BigQuery in a pre-existing project, go to

Enable the BigQuery API.

**Roles required to enable APIs**

To enable APIs, you need the Service Usage Admin IAM role ( `  roles/serviceusage.serviceUsageAdmin  ` ), which contains the `  serviceusage.services.enable  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .

### Required roles

To use the `  AI.GENERATE  ` function, you need the following Identity and Access Management (IAM) roles:

  - Create and use BigQuery datasets and tables: BigQuery Data Editor ( `  roles/bigquery.dataEditor  ` ) on your project.
  - Create, delegate, and use BigQuery connections: BigQuery Connections Admin ( `  roles/bigquery.connectionsAdmin  ` ) on your project.
  - Grant permissions to the connection's service account: Project IAM Admin ( `  roles/resourcemanager.projectIamAdmin  ` ) on the project that contains the Vertex AI endpoint.
  - Create BigQuery jobs: BigQuery Job User ( `  roles/bigquery.jobUser  ` ) on your project.

These predefined roles contain the permissions required to perform the tasks in this document. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

  - Create a dataset: `  bigquery.datasets.create  `
  - Create, delegate, and use a connection: `  bigquery.connections.*  `
  - Set service account permissions: `  resourcemanager.projects.getIamPolicy  ` and `  resourcemanager.projects.setIamPolicy  `
  - Query table data: `  bigquery.tables.getData  `

You might also be able to get these permissions with [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

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

## Create a connection

Create a [Cloud resource connection](/bigquery/docs/create-cloud-resource-connection) and get the connection's service account. Create the connection in the same [location](/bigquery/docs/locations) as the dataset that you created in the previous step.

Follow these steps to create a connection:

1.  Go to the **BigQuery** page.

2.  In the **Explorer** pane, click add **Add data** :
    
    The **Add data** dialog opens.

3.  In the **Filter By** pane, in the **Data Source Type** section, select **Business Applications** .
    
    Alternatively, in the **Search for data sources** field, you can enter `  Vertex AI  ` .

4.  In the **Featured data sources** section, click **Vertex AI** .

5.  Click the **Vertex AI Models: BigQuery Federation** solution card.

6.  In the **Connection type** list, select **Vertex AI remote models, remote functions, BigLake and Spanner (Cloud Resource)** .

7.  In the **Connection ID** field, type `  test_connection  ` .

8.  Click **Create connection** .

9.  Click **Go to connection** .

10. In the **Connection info** pane, copy the service account ID for use in the next step.

### Give the service account access

Grant the connection's service account the Vertex AI User role.

To grant the role, follow these steps:

1.  Go to the **IAM & Admin** page.

2.  Click person\_add **Add** .
    
    The **Add principals** dialog opens.

3.  In the **New principals** field, enter the service account ID that you copied earlier.

4.  In the **Select a role** field, select **Vertex AI** , and then select **Vertex AI User** .

5.  Click **Add another role** .

6.  In the **Select a role** field, choose **Cloud Storage** , and then select **Storage Object Viewer** .

7.  Click **Save** .

## Summarize text and use the default output format

Follow these steps to generate text using the `  AI.GENERATE  ` function, and output the results in the `  AI.GENERATE  ` function's default format:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, run the following query:
    
    ``` text
    WITH
    bbc_news AS (
      SELECT body FROM `bigquery-public-data.bbc_news.fulltext` LIMIT 5
    )
    SELECT AI.GENERATE(body, connection_id => 'us.test_connection') AS news FROM bbc_news;
    ```
    
    The output is similar to the following:
    
    ``` text
    +---------------------------------------------+------------------------------------+---------------+
    | news.result                                 | news.full_response                 | news.status   |
    +---------------------------------------------+------------------------------------+---------------+
    | This article presents a debate about the    | {"candidates":[{"avg_logprobs":    |               |
    | "digital divide" between rich and poor      | -0.31465074559841777, content":    |               |
    | nations. Here's a breakdown of the key..    | {"parts":[{"text":"This article..  |               |
    +---------------------------------------------+------------------------------------+---------------+
    | This article discusses how advanced         | {"candidates":[{"avg_logprobs":    |               |
    | mapping technology is aiding humanitarian   | -0.21313422900091983,"content":    |               |
    | efforts in Darfur, Sudan. Here's a...       | {"parts":[{"text":"This article..  |               |
    +---------------------------------------------+------------------------------------+---------------+
    | ...                                         | ...                                | ...           |
    +---------------------------------------------+------------------------------------+---------------+
    ```

## Summarize text and output structured results

Follow these steps to generate text using the `  AI.GENERATE  ` function, and use the `  AI.GENERATE  ` function's `  output_schema  ` argument to format the output:

1.  In the Google Cloud console, go to the BigQuery page.

2.  In the query editor, run the following query:
    
    ``` text
    WITH
    bbc_news AS (
      SELECT
        body
      FROM
        `bigquery-public-data`.bbc_news.fulltext
      LIMIT 5
    )
    SELECT
    news.good_sentiment,
    news.summary
    FROM
    bbc_news,
    UNNEST(ARRAY[AI.GENERATE(body, connection_id  => 'us.test', output_schema  => 'summary STRING, good_sentiment BOOL')]) AS news;
    ```
    
    The output is similar to the following:
    
    ``` text
    +----------------+--------------------------------------------+
    | good_sentiment | summary                                    |
    +----------------+--------------------------------------------+
    | true           | A World Bank report suggests the digital   |
    |                | divide is rapidly closing due to increased |
    |                | access to technology in developing..       |
    +----------------+--------------------------------------------+
    | true           | A review of sports games, focusing on the  |
    |                | rivalry between EA Sports and ESPN, and    |
    |                | the recent deal where EA acquired the..    |
    +----------------+--------------------------------------------+
    | ...            | ...                                        |
    +----------------+--------------------------------------------+
    ```

## Transcribe and translate video content

Follow these steps to create an object table over public video content, and then transcribe and translate a video:

1.  In the Google Cloud console, go to the BigQuery page.

2.  In the query editor, run the following query to create the object table:
    
    ``` text
    CREATE OR REPLACE EXTERNAL TABLE `bqml_tutorial.video`
    WITH CONNECTION `us.test_connection`
    OPTIONS (
      object_metadata = 'SIMPLE',
      uris =
        ['gs://cloud-samples-data/generative-ai/video/*']);
    ```

3.  In the query editor, run the following query to transcribe and translate the `  pixel8.mp4  ` file:
    
    ``` text
    SELECT
    AI.GENERATE(
      (OBJ.GET_ACCESS_URL(ref, 'r'), 'Transcribe the video in Japanese and then translate to English.'),
      connection_id => 'us.test_connection',
      endpoint => 'gemini-2.5-flash',
      output_schema => 'japanese_transcript STRING, english_translation STRING'
    ).* EXCEPT (full_response, status)
    FROM
    `bqml_tutorial.video`
    WHERE
    REGEXP_CONTAINS(uri, 'pixel8.mp4');
    ```
    
    The output is similar to the following:
    
    ``` text
    +--------------------------------------------+--------------------------------+
    | english_translation                        | japanese_transcript            |
    +--------------------------------------------+--------------------------------+
    | My name is Saeka Shimada. I'm a            | 島田 さえか です 。 東京 で フ     |
    | photographer in Tokyo. Tokyo has many      | ォトグラファー を し て い ま      |
    | faces. The city at night is totally...     | す 。 東京 に は いろんな 顔 が    |
    +--------------------------------------------+--------------------------------+
    ```

## Analyze audio file content

Follow these steps to create an object table over public audio content, and then analyze the content of the audio files.

1.  In the Google Cloud console, go to the BigQuery page.

2.  In the query editor, run the following query to create the object table:
    
    ``` text
    CREATE OR REPLACE EXTERNAL TABLE `bqml_tutorial.audio`
      WITH CONNECTION `us.test_connection`
      OPTIONS (
        object_metadata = 'SIMPLE',
        uris =
          ['gs://cloud-samples-data/generative-ai/audio/*']);
    ```

3.  In the query editor, run the following query to analyze the audio files:
    
    ``` text
    SELECT
    AI.GENERATE(
      (OBJ.GET_ACCESS_URL(ref, 'r'), 'Summarize the content of this audio file.'),
      connection_id => 'us.test_connection',
      endpoint => 'gemini-2.5-flash',
      output_schema => 'topic ARRAY<STRING>, summary STRING'
    ).* EXCEPT (full_response, status), uri
    FROM
    `bqml_tutorial.audio`;
    ```
    
    The results look similar to the following:
    
    ``` text
    +--------------------------------------------+-----------------------------------------------------------+
    | summary                                    | topic              | uri                                  |
    +--------------------------------------------+-----------------------------------------------------------+
    | The audio contains a distinctive 'beep'    | beep sound         | gs://cloud-samples-data/generativ... |
    | sound, followed by the characteristic      |                    |                                      |
    | sound of a large vehicle or bus backing..  |                    |                                      |
    +--------------------------------------------+--------------------+--------------------------------------+
    |                                            | vehicle backing up |                                      |
    |                                            +--------------------+                                      |
    |                                            | bus                |                                      |
    |                                            +--------------------+                                      |
    |                                            | alarm              |                                      |
    +--------------------------------------------+--------------------+--------------------------------------+
    | The speaker introduces themselves          | Introduction       | gs://cloud-samples-data/generativ... |
    | as Gemini and expresses their excitement   |                    |                                      |
    | and readiness to dive into something..     |                    |                                      |
    +--------------------------------------------+--------------------+--------------------------------------+
    |                                            | Readiness          |                                      |
    |                                            +--------------------+                                      |
    |                                            | Excitement         |                                      |
    |                                            +--------------------+                                      |
    |                                            | Collaboration      |                                      |
    +--------------------------------------------+--------------------+--------------------------------------+
    | ...                                        | ...                | ...                                  |
    +--------------------------------------------+--------------------+--------------------------------------+
    ```

## Clean up

**Caution** : Deleting a project has the following effects:

  - **Everything in the project is deleted.** If you used an existing project for the tasks in this document, when you delete it, you also delete any other work you've done in the project.
  - **Custom project IDs are lost.** When you created this project, you might have created a custom project ID that you want to use in the future. To preserve the URLs that use the project ID, such as an `  appspot.com  ` URL, delete selected resources inside the project instead of deleting the whole project.

If you plan to explore multiple architectures, tutorials, or quickstarts, reusing projects can help you avoid exceeding project quota limits.

In the Google Cloud console, go to the **Manage resources** page.

In the project list, select the project that you want to delete, and then click **Delete** .

In the dialog, type the project ID, and then click **Shut down** to delete the project.
