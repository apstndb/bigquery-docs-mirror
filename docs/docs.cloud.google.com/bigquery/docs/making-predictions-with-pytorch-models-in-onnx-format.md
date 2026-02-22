[Open Neural Network Exchange](https://onnx.ai/) (ONNX) provides a uniform format designed to represent any machine learning framework. BigQuery ML support for ONNX lets you:

  - Train a model using your favorite framework.
  - Convert the model into ONNX model format.
  - Import the ONNX model into BigQuery and make predictions using BigQuery ML.

This tutorial shows you how to import ONNX models trained with [PyTorch](https://pytorch.org/) into a BigQuery dataset and use them to make predictions from a SQL query.

**Important:** You must have a reservation in order to run predictions using imported models and object tables. For more information, see the [Limitations](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-onnx#limitations) on imported ONNX models.

## Objectives

  - Import a pretrained model using [PyTorch](https://pytorch.org/) .
  - [Convert the model to ONNX format](https://github.com/onnx/tutorials#converting-to-onnx-format) using [torch.onnx](https://pytorch.org/docs/stable/onnx.html) .
  - Use the `  CREATE MODEL  ` statement to import the ONNX model into BigQuery.
  - Use the `  ML.PREDICT  ` function to make predictions with the imported ONNX model.

## Costs

In this document, you use the following billable components of Google Cloud:

  - [BigQuery](https://cloud.google.com/bigquery/pricing)
  - [BigQuery ML](https://cloud.google.com/bigquery/pricing#bqml)
  - [Cloud Storage](/storage/pricing)

To generate a cost estimate based on your projected usage, use the [pricing calculator](/products/calculator) .

New Google Cloud users might be eligible for a [free trial](/free) .

When you finish the tasks that are described in this document, you can avoid continued billing by deleting the resources that you created. For more information, see [Clean up](#clean-up) .

## Before you begin

1.  Ensure that you have the [necessary permissions](#required_roles) to perform the tasks in this document.

### Required roles

If you create a new project, you're the project owner, and you're granted all of the required Identity and Access Management (IAM) permissions that you need to complete this tutorial.

If you are using an existing project, do the following.

Make sure that you have the following role or roles on the project:

  - [BigQuery Studio Admin](/bigquery/docs/access-control#bigquery.studioUser) ( `  roles/bigquery.studioAdmin  ` )
  - [BigQuery Connection Admin](/bigquery/docs/access-control#bigquery.connectionAdmin) ( `  roles/bigquery.connectionAdmin  ` )
  - [Storage Admin](/storage/docs/access-control/iam-roles#standard-roles) `  (roles/storage.admin)  `

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

For more information about IAM permissions in BigQuery, see [IAM permissions](/bigquery/docs/object-table-introduction) .

## Optional: Train a model and convert it to ONNX format

The following code samples show you how to import a pretrained classification model into PyTorch and how to convert the resulting model into ONNX format. This tutorial uses a prebuilt example model stored at `  gs://cloud-samples-data/bigquery/ml/onnx/resnet18.onnx  ` . You don't have to complete these steps if you're using the sample model.

### Create a PyTorch vision model for image classification

Use the following code sample to import a PyTorch pretrained [resnet18](https://pytorch.org/vision/main/models/generated/torchvision.models.resnet18.html) model that accepts decoded image data returned by the BigQuery ML [`  ML.DECODE_IMAGE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-decode-image) and [`  ML.RESIZE_IMAGE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-resize-image) functions.

``` text
import torch
import torch.nn as nn

# Define model input format to match the output format of
# ML.DECODE_IMAGE function: [height, width, channels]
dummy_input = torch.randn(1, 224, 224, 3, device="cpu")

# Load a pretrained pytorch model for image classification
model = torch.hub.load('pytorch/vision:v0.10.0', 'resnet18', pretrained=True)

# Reshape input format from [batch_size, height, width, channels]
# to [batch_size, channels, height, width]
class ReshapeLayer(nn.Module):
    def __init__(self):
        super().__init__()

    def forward(self, x):
        x = x.permute(0, 3, 1, 2)  # reorder dimensions
        return x

class ArgMaxLayer(nn.Module):
    def __init__(self):
        super().__init__()

    def forward(self, x):
       return torch.argmax(x, dim=1)

final_model = nn.Sequential(
    ReshapeLayer(),
    model,
    nn.Softmax(),
    ArgMaxLayer()
)
```

### Convert the model into ONNX format

Use the following sample to export the PyTorch vision model using [torch.onnx](https://pytorch.org/docs/stable/onnx.html) . The exported ONNX file is named `  resnet18.onnx  ` .

``` text
torch.onnx.export(final_model,            # model being run
                  dummy_input,            # model input
                  "resnet18.onnx",        # where to save the model
                  opset_version=10,       # the ONNX version to export the model to
                  input_names = ['input'],         # the model's input names
                  output_names = ['class_label'])  # the model's output names
```

### Upload the ONNX model to Cloud Storage

After you save your model, do the following:

  - [Create a Cloud Storage bucket](/storage/docs/creating-buckets) to store the model.
  - [Upload the ONNX model to your Cloud Storage bucket](/storage/docs/uploading-objects) .

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

## Import the ONNX model into BigQuery

The following steps show you how to import the sample ONNX model from Cloud Storage into your dataset by using a [`  CREATE MODEL  `](https://pytorch.org/vision/main/models/generated/torchvision.models.resnet18.html) statement.

### Console

1.  In the Google Cloud console, go to the **BigQuery Studio** page.

2.  In the query editor, enter the following [`  CREATE MODEL  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-onnx) statement.
    
    ``` text
    CREATE OR REPLACE MODEL `bqml_tutorial.imported_onnx_model`
     OPTIONS (MODEL_TYPE='ONNX',
      MODEL_PATH='BUCKET_PATH')
    ```
    
    Replace `  BUCKET_PATH  ` with the path to the model that you uploaded to Cloud Storage. If you're using the sample model, replace `  BUCKET_PATH  ` with the following value: `  gs://cloud-samples-data/bigquery/ml/onnx/resnet18.onnx  ` .
    
    When the operation is complete, you see a message similar to the following: `  Successfully created model named imported_onnx_model  ` .
    
    Your new model appears in the **Resources** panel. Models are indicated by the model icon: If you select the new model in the **Resources** panel, information about the model appears adjacent to the **Query editor** .

### bq

1.  Import the ONNX model from Cloud Storage by entering the following `  CREATE MODEL  ` statement.
    
    ``` text
    bq query --use_legacy_sql=false \
    "CREATE OR REPLACE MODEL
      `bqml_tutorial.imported_onnx_model`
    OPTIONS
      (MODEL_TYPE='ONNX',
       MODEL_PATH='BUCKET_PATH')"
    ```
    
    Replace `  BUCKET_PATH  ` with the path to the model that you uploaded to Cloud Storage. If you're using the sample model, replace `  BUCKET_PATH  ` with this value: `  gs://cloud-samples-data/bigquery/ml/onnx/resnet18.onnx  ` .

2.  After you import the model, verify that the model appears in the dataset.
    
    ``` text
    bq ls -m bqml_tutorial
    ```
    
    The output is similar to the following:
    
    ``` text
    tableId               Type
    --------------------- -------
    imported_onnx_model  MODEL
    ```

For more information about importing ONNX models into BigQuery, including format and storage requirements, see [The `  CREATE MODEL  ` statement for importing ONNX models](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-onnx) .

## Create an object table in BigQuery to analyze image data

An [object table](/bigquery/docs/object-table-introduction) is a read-only table over unstructured data objects that reside in Cloud Storage. Object tables let you analyze unstructured data from BigQuery.

In this tutorial, you use the `  ML.PREDICT  ` function to output the predicted class label of an input image that is stored in a Cloud Storage bucket.

Creating the object table requires you to do the following:

  - Create a Cloud Storage bucket and upload an image of a goldfish.
  - Create a Cloud resource connection that is used to access the object table.
  - Grant access to the resource connection's service account.

### Create a bucket and upload an image

Follow these steps to create a Cloud Storage bucket and to upload an image of a goldfish.

### Console

**Note:** When creating a bucket using the Google Cloud console, you're only required to set a globally unique name for your bucket; all other steps are either optional or have default settings.

1.  In the Google Cloud console, go to the Cloud Storage **Buckets** page.  

2.  Click add\_box **Create** .

3.  On the **Create a bucket** page, enter your bucket information.
    
    1.  In the **Get started** section, do the following:
        
        1.  In the box, enter `  bqml_images  ` .
        
        2.  Click **Continue** .
    
    2.  In the **Choose where to store your data** section, do the following:
        
        1.  For **Location type** , select **Multi-region** .
        
        2.  From the location type's menu, select **US (multiple regions in United States)** .
        
        3.  Click **Continue** .
    
    3.  In the **Choose a storage class for your data** section:
        
        1.  Select **Set a default class** .
        
        2.  Select **Standard** .
        
        3.  Click **Continue** .
    
    4.  In the remaining sections, leave the default values.

4.  Click **Create** .

### Command line

Enter the following `  gcloud storage buckets create  ` command:

``` text
gcloud storage buckets create gs://bqml_images --location=us
```

If the request is successful, the command returns the following message:

``` text
Creating gs://bqml_images/...
```

### Upload an image to your Cloud Storage bucket

After the bucket is created, download an image of a goldfish, and upload it to your Cloud Storage bucket.

Complete the following steps to upload the image:

### Console

1.  In the Google Cloud console, go to the Cloud Storage **Buckets** page.  

2.  In the list of buckets, click **`  bqml_images  `** .

3.  In the **Objects** tab for the bucket, do one of the following:
    
      - Drag the file from your desktop or file manager to the main pane in the Google Cloud console.
    
      - Click **Upload \> Upload files** , select the image file you want to upload in the dialog that appears, then click **Open** .

### Command line

Enter the following `  gcloud storage cp  ` command:

``` text
gcloud storage cp OBJECT_LOCATION gs://bqml_images/IMAGE_NAME
```

Replace the following:

  - `  OBJECT_LOCATION  ` : the local path to your image file. For example, `  Desktop/goldfish.jpg  ` .
  - `  IMAGE_NAME  ` : the name of the image. For example, `  goldfish.jpg  ` .

If successful, the response is similar to the following:

``` text
Completed files 1/1 | 164.3kiB/164.3kiB
```

### Create a BigQuery Cloud resource connection

You must have a Cloud resource connection to connect to the [object table](/bigquery/docs/object-table-introduction) that you create later in this tutorial.

Cloud resource connections let you query data that's stored outside of BigQuery in Google Cloud services like Cloud Storage or Spanner, or in third-party sources like AWS or Azure. These external connections use the BigQuery Connection API.

Follow these steps to create your Cloud resource connection.

### Console

1.  Go to the **BigQuery Studio** page.

2.  In the left pane, click explore **Explorer** :
    
    If you don't see the left pane, click last\_page **Expand left pane** to open the pane.

3.  In the **Explorer** pane, click add **Add data** .
    
    The **Add data** dialog opens.

4.  In the **Filter By** pane, in the **Data Source Type** section, select **Databases** .
    
    Alternatively, in the **Search for data sources** field, you can enter `  Vertex AI  ` .

5.  In the **Featured data sources** section, click **Vertex AI** .

6.  Click the **Vertex AI Models: BigQuery Federation** solution card.

7.  In the **Connection type** list, select **Vertex AI remote models, remote functions and BigLake (Cloud Resource)** .

8.  In the **Connection ID** field, enter `  bqml_tutorial  ` .

9.  Verify that **Multi-region—US** is selected.

10. Click **Create connection** .

11. At the bottom of the window, click **Go to connection** . Alternatively, in the **Explorer** pane, click **Connections** , and then click **`  us.bqml_tutorial  `** .

12. In the **Connection info** pane, copy the service account ID. You need this ID when you configure permissions for the connection. When you create a connection resource, BigQuery creates a unique system service account and associates it with the connection.

### bq

1.  Create a connection:
    
    ``` text
    bq mk --connection --location=US --project_id=PROJECT_ID \
        --connection_type=CLOUD_RESOURCE bqml_tutorial
    ```
    
    Replace `  PROJECT_ID  ` with your Google Cloud project ID. The `  --project_id  ` parameter overrides the default project.
    
    When you create a connection resource, BigQuery creates a unique system service account and associates it with the connection.
    
    **Troubleshooting** : If you get the following connection error, [update the Google Cloud SDK](/sdk/docs/quickstart) :
    
    ``` console
    Flags parsing error: flag --connection_type=CLOUD_RESOURCE: value should be one of...
    ```

2.  Retrieve and copy the service account ID for use in a later step:
    
    ``` text
    bq show --connection PROJECT_ID.us.bqml_tutorial
    ```
    
    The output is similar to the following:
    
    ``` console
    name                          properties
    1234.REGION.CONNECTION_ID {"serviceAccountId": "connection-1234-9u56h9@gcp-sa-bigquery-condel.iam.gserviceaccount.com"}
    ```

### Set up connection access

Grant the Storage Object Admin role to the Cloud resource connection's service account. You must grant this role in the same project where you uploaded the image files.

**Note:** If the connection is in a different project, this error is returned: `  bqcx-1234567890-xxxx@gcp-sa-bigquery-condel.iam.gserviceaccount.com does not have the permission to access resource  ` .

To grant the role, follow these steps:

1.  Go to the **IAM & Admin** page.

2.  Click person\_add **Grant Access** .

3.  In the **New principals** field, enter the Cloud resource connection's Service account ID that you copied previously.

4.  In the **Select a role** field, choose **Cloud Storage** , and then select **Storage object admin** .

5.  Click **Save** .

### Create the object table

Follow these steps to create an object table named `  goldfish_image_table  ` using the goldfish image you uploaded to Cloud Storage.

### Console

1.  Go to the **BigQuery Studio** page.

2.  In the query editor, enter this query to create the object table.
    
    ``` text
    CREATE EXTERNAL TABLE `bqml_tutorial.goldfish_image_table`
    WITH CONNECTION `us.bqml_tutorial`
    OPTIONS(
    object_metadata = 'SIMPLE',
    uris = ['gs://bqml_images/IMAGE_NAME'],
    max_staleness = INTERVAL 1 DAY,
    metadata_cache_mode = 'AUTOMATIC');
    ```
    
    Replace `  IMAGE_NAME  ` with the name of the image file—for example, `  goldfish.jpg  ` .
    
    When the operation is complete, you see a message like `  This statement created a new table named goldfish_image_table  ` .

### bq

1.  Create the object table by entering the following `  CREATE EXTERNAL TABLE  ` statement.
    
    ``` text
    bq query --use_legacy_sql=false \
    "CREATE EXTERNAL TABLE `bqml_tutorial.goldfish_image_table`
    WITH CONNECTION `us.bqml_tutorial`
    OPTIONS(
    object_metadata = 'SIMPLE',
    uris = ['gs://bqml_images/IMAGE_NAME'],
    max_staleness = INTERVAL 1 DAY,
    metadata_cache_mode = 'AUTOMATIC')"
    ```
    
    Replace `  IMAGE_NAME  ` with the name of the image file—for example, `  goldfish.jpg  ` .

2.  After you create the object table, verify that it appears in the dataset.
    
    ``` text
    bq ls bqml_tutorial
    ```
    
    The output is similar to the following:
    
    ``` text
    tableId               Type
    --------------------- --------
    goldfish_image_table  EXTERNAL
    ```

For more information, see [Create object tables](/bigquery/docs/object-tables) .

## Make predictions with the imported ONNX model

**Important:** You must have a reservation in order to run predictions using imported models and object tables. For more information, see the [limitations](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-onnx#limitations) on imported ONNX models.  
  
If you don't have a reservation, running a query using `  ML.PREDICT  ` produces this error: ``  BigQuery ML inference using imported models and object tables requires a reservation, but no reservations were assigned for job type `QUERY`...`  `` .

You use the following query that contains the [`  ML.PREDICT  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-predict) function to make predictions from image data in the input object table `  goldfish_image_table  ` . This query outputs the predicted class label of the input image based on the [ImageNet labels](https://raw.githubusercontent.com/pytorch/hub/master/imagenet_classes.txt) dictionary.

In the query, the [`  ML.DECODE_IMAGE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-decode-image) function is required to decode the image data so that it can be interpreted by `  ML.PREDICT  ` . The [`  ML.RESIZE_IMAGE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-resize-image) function is called to resize the image to fit the size of the model's input (224\*224).

For more information about running inference on image object tables, see [Run inference on image object tables](/bigquery/docs/object-table-inference) .

To make predictions from your image data, do the following.

### Console

1.  Go to the **BigQuery Studio** page.

2.  In the query editor, enter the following `  ML.PREDICT  ` query.
    
    ``` text
     SELECT
       class_label
     FROM
       ML.PREDICT(MODEL bqml_tutorial.imported_onnx_model,
         (
         SELECT
           ML.RESIZE_IMAGE(ML.DECODE_IMAGE(DATA),
             224,
             224,
             FALSE) AS input
         FROM
           bqml_tutorial.goldfish_image_table))
     
    ```
    
    The query results are similar to the following:

### bq

Enter the following `  bq query  ` command:

``` text
bq query --use_legacy_sql=false \
'SELECT
  class_label
FROM
  ML.PREDICT(MODEL `bqml_tutorial.imported_onnx_model`,
    (
    SELECT
      ML.RESIZE_IMAGE(ML.DECODE_IMAGE(DATA),
        224,
        224,
        FALSE) AS input
    FROM
      bqml_tutorial.goldfish_image_table))'
```

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

Alternatively, to remove the individual resources used in this tutorial, do the following:

1.  [Delete the imported model](/bigquery/docs/deleting-models) .

2.  (Optional) [Delete the dataset](/bigquery/docs/managing-datasets#delete-datasets) .

3.  [Delete the Cloud resource connection](/bigquery/docs/working-with-connections#delete-connections) .

4.  [Delete the Cloud Storage bucket](https://cloud.google.com/storage/docs/deleting-buckets#delete-bucket) .

## What's next

  - For more information about importing ONNX models, see [The `  CREATE MODEL  ` statement for ONNX models](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-onnx) .
  - For more information about available ONNX converters and tutorials, see [Converting to ONNX format](https://github.com/onnx/tutorials#converting-to-onnx-format) .
  - For an overview of BigQuery ML, see [Introduction to BigQuery ML](/bigquery/docs/bqml-introduction) .
  - To get started using BigQuery ML, see [Create machine learning models in BigQuery ML](/bigquery/docs/create-machine-learning-model) .
