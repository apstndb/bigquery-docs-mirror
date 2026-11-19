---
name: documents/docs.cloud.google.com/bigquery/docs/object-table-inference
uri: https://docs.cloud.google.com/bigquery/docs/object-table-inference
title: Run inference on image object tables
description: Classify images with object tables in BigQuery ML.
data_source: docs.cloud.google.com
---

BigQuery lets you classify or extract features from images in Cloud Storage by running SQL queries on [object tables](https://docs.cloud.google.com/bigquery/docs/object-table-introduction) . You can apply custom or pretrained vision models directly in BigQuery for catalog tagging, content moderation, and defect detection without moving files or building pipelines.

In this tutorial, you create an object table of sample pet product images, import a ResNet-18 [ONNX](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-onnx) model, and generate class predictions.

## Objectives

- Create a BigQuery reservation for running inference with imported models on object tables.
- Create a dataset, a Cloud resource connection, and an object table over sample product images in Cloud Storage.
- Import a pretrained ResNet-18 ONNX model into BigQuery ML and inspect its input and output fields.
- Preprocess and classify images by using the `ML.DECODE_IMAGE` , `ML.RESIZE_IMAGE` , and `ML.PREDICT` functions.

## Costs

In this document, you use the following billable components of Google Cloud:

- **BigQuery** : You incur slot capacity costs for the reservation that you create, storage costs for the object table, and query processing costs.
- **BigQuery ML** : You incur costs for creating the model and running inference in BigQuery ML.
- **Cloud Storage** : You incur costs if you store your own images or model artifacts in Cloud Storage.

To generate a cost estimate based on your projected usage, use the [pricing calculator](https://docs.cloud.google.com/products/calculator) .

New Google Cloud users might be eligible for a [free trial](https://docs.cloud.google.com/free) .

For more information, see [BigQuery pricing](https://cloud.google.com/bigquery/pricing) , [BigQuery ML pricing](https://cloud.google.com/bigquery/pricing#bqml) , and [Cloud Storage pricing](https://cloud.google.com/storage/pricing) .

## Before you begin

### Required roles

To get the permissions that you need to complete this tutorial, ask your administrator to grant you the following IAM roles on the project:

- Create datasets, object tables, and models: [BigQuery Data Editor](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor) ( `roles/bigquery.dataEditor` )
- Create, delegate, and use connections: [BigQuery Connection Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.connectionAdmin) ( `roles/bigquery.connectionAdmin` )
- Grant permissions to the connection's service account: [Project IAM Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/resourcemanager#resourcemanager.projectIamAdmin) ( `roles/resourcemanager.projectIamAdmin` )
- Create reservations and reservation assignments: [BigQuery Resource Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin) ( `roles/bigquery.resourceAdmin` )
- Run BigQuery jobs: [BigQuery Job User](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.jobUser) ( `roles/bigquery.jobUser` )
- Upload custom models or images to Cloud Storage (optional): [Storage Object Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/storage#storage.objectAdmin) ( `roles/storage.objectAdmin` )

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## Limitations

Running inference on image object tables with imported models has the following limitations:

- **Pricing and reservations:** Using BigQuery ML [imported models](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/inference-overview#inference_using_imported_models) with object tables requires capacity-based pricing through reservations in the [Enterprise or Enterprise Plus edition](https://docs.cloud.google.com/bigquery/docs/editions-intro) . On-demand pricing isn't supported.
- **Image files:** Images referenced by the object table must meet the following requirements:
  - Each image file must be less than 20 MB in size and in JPEG, PNG, or BMP format. When you pass an image to `ML.DECODE_IMAGE` , the image must be 10 MB or smaller.
  - The combined size of all image files in the object table must be less than 1 TB.
  - Specify at most 10 source URIs in the `uris` option of the object table. Specifying more than 10 bucket URIs can cause queries to fail with a `Resources exceeded during query execution` memory error when listing a large number of files. If you need to reference more than 10 buckets, split them across multiple object tables.
- **Imported models:** The model must meet the following requirements:
  - The model must be a [TensorFlow](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-tensorflow) or [TensorFlow Lite](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-tflite) model, or a PyTorch model in [ONNX format](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-onnx) , and it must meet the general limitations for that model type.
  - The serialized model size must be less than 450 MB, and the deserialized (in-memory) model size must be less than 1,000 MB.
  - The model input tensor must have a data type of `tf.float32` with values in `[0, 1)` or `tf.uint8` with values in `[0, 255)` , and a shape of `[batch_size, width, height, 3]` , where `batch_size` is `-1` , `None` , or `1` , and `width` and `height` are greater than `0` .
  - The model must be trained on images in the `RGB` , `HSV` , `YIQ` , `YUV` , or `GRAYSCALE` color space. You can use the [`ML.CONVERT_COLOR_SPACE` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-convert-color-space) to convert input images to match your model's color space.

## Create a reservation

To run BigQuery ML inference with an imported model on an object table, you must assign a BigQuery reservation (Enterprise or Enterprise Plus edition) to your project for `QUERY` jobs. If your project already has a reservation assigned in the `US` multi-region, you can skip this section.

### Create the slot reservation

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the navigation menu, click **Workload management** .

3.  Click **Create reservation** .

4.  On the **Create reservation** page, configure the reservation:

    1.  In the **Reservation name** field, enter `bqml-tutorial-reservation` .
    2.  For **Location** , select **us (multiple regions in United States)** .
    3.  Leave the remaining default settings as they are, and then click **Save** .

### Assign the reservation to your project

1.  On the **Capacity management** page, in the **Slot reservations** table, find `bqml-tutorial-reservation` .
2.  Click **Actions \> Create assignment** .
3.  In the **Create an assignment** pane, click **Browse** and select your project.
4.  For **Job type** , select **QUERY** .
5.  Click **Create** .

## Create a dataset

Create the `bqml_tutorial` dataset in the `US` multi-region to store your object table and imported model.

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

## Create a connection

Create a [Cloud resource connection](https://docs.cloud.google.com/bigquery/docs/create-cloud-resource-connection) in the `US` multi-region, where you created the dataset, and then copy the connection's service account ID. BigQuery uses this connection to read image files from Cloud Storage.

Select one of the following options:

### Console

1.  Go to the **BigQuery** page.

2.  In the left pane, click **Explorer** :

    ![Highlighted button for the Explorer pane.](https://docs.cloud.google.com/static/bigquery/images/explorer-tab.png)

    If you don't see the left pane, click **Expand left pane** to open the pane.

3.  In the **Explorer** pane, expand your project name, and then click **Connections** .

4.  On the **Connections** page, click **Create connection** .

5.  For **Connection type** , choose **Vertex AI remote models, remote functions, BigLake and Spanner (Cloud Resource)** .

6.  In the **Connection ID** field, enter a name for your connection.

7.  For **Location type** , select a location for your connection. The connection should be colocated with your other resources such as datasets.

8.  Click **Create connection** .

9.  Click **Go to connection** .

10. In the **Connection info** pane, copy the service account ID for use in a later step.

### SQL

Use the [`CREATE CONNECTION` statement](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_connection_statement) :

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:

    ```
    CREATE CONNECTION [IF NOT EXISTS] `CONNECTION_NAME`
    OPTIONS (
      connection_type = "CLOUD_RESOURCE",
      friendly_name = "FRIENDLY_NAME",
      description = "DESCRIPTION"
      );
    ```

    Replace the following:

    - `CONNECTION_NAME` : the name of the connection in either the `PROJECT_ID `` . `` LOCATION `` . `` CONNECTION_ID` , `LOCATION `` . `` CONNECTION_ID` , or `CONNECTION_ID` format. If the project or location are omitted, then they are inferred from the project and location where the statement is run.
    - `FRIENDLY_NAME` (optional): a descriptive name for the connection.
    - `DESCRIPTION` (optional): a description of the connection.

3.  Click **Run** .

For more information about how to run queries, see [Run an interactive query](https://docs.cloud.google.com/bigquery/docs/running-queries#queries) .

### bq

1.  In a command-line environment, create a connection:

    ```
    bq mk --connection --location=REGION --project_id=PROJECT_ID \
        --connection_type=CLOUD_RESOURCE CONNECTION_ID
    ```

    The `--project_id` parameter overrides the default project.

    Replace the following:

    - `REGION` : your [connection region](https://docs.cloud.google.com/bigquery/docs/locations#supported_locations)
    - `PROJECT_ID` : your Google Cloud project ID
    - `CONNECTION_ID` : an ID for your connection

    When you create a connection resource, BigQuery creates a unique system service account and associates it with the connection.

    **Troubleshooting** : If you get the following connection error, [update the Google Cloud SDK](https://docs.cloud.google.com/sdk/docs/quickstart) :

    ```console
    Flags parsing error: flag --connection_type=CLOUD_RESOURCE: value should be one of...
    ```

2.  Retrieve and copy the service account ID for use in a later step:

    ```
    bq show --connection PROJECT_ID.REGION.CONNECTION_ID
    ```

    The output is similar to the following:

    ```console
    name                          properties
    1234.REGION.CONNECTION_ID     {"serviceAccountId": "connection-1234-9u56h9@gcp-sa-bigquery-condel.iam.gserviceaccount.com"}
    ```

### Python

Before trying this sample, follow the Python setup instructions in the [BigQuery quickstart using client libraries](https://docs.cloud.google.com/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/bigquery/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](https://docs.cloud.google.com/bigquery/docs/authentication#client-libs) .

```python
import google.api_core.exceptions
from google.cloud import bigquery_connection_v1

client = bigquery_connection_v1.ConnectionServiceClient()


def create_connection(
    project_id: str,
    location: str,
    connection_id: str,
):
    """Creates a BigQuery connection to a Cloud Resource.

    Cloud Resource connection creates a service account which can then be
    granted access to other Google Cloud resources for federated queries.

    Args:
        project_id: The Google Cloud project ID.
        location: The location of the connection (for example, "us-central1").
        connection_id: The ID of the connection to create.
    """

    parent = client.common_location_path(project_id, location)

    connection = bigquery_connection_v1.Connection(
        friendly_name="Example Connection",
        description="A sample connection for a Cloud Resource.",
        cloud_resource=bigquery_connection_v1.CloudResourceProperties(),
    )

    try:
        created_connection = client.create_connection(
            parent=parent, connection_id=connection_id, connection=connection
        )
        print(f"Successfully created connection: {created_connection.name}")
        print(f"Friendly name: {created_connection.friendly_name}")
        print(
            f"Service Account: {created_connection.cloud_resource.service_account_id}"
        )

    except google.api_core.exceptions.AlreadyExists:
        print(f"Connection with ID '{connection_id}' already exists.")
        print("Please use a different connection ID.")
    except Exception as e:
        print(f"An unexpected error occurred while creating the connection: {e}")
```

### Node.js

Before trying this sample, follow the Node.js setup instructions in the [BigQuery quickstart using client libraries](https://docs.cloud.google.com/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Node.js API reference documentation](https://googleapis.dev/nodejs/bigquery/latest/index.html) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](https://docs.cloud.google.com/bigquery/docs/authentication#client-libs) .

```javascript
const {ConnectionServiceClient} =
  require('@google-cloud/bigquery-connection').v1;
const {status} = require('@grpc/grpc-js');

const client = new ConnectionServiceClient();

/**
 * Creates a new BigQuery connection to a Cloud Resource.
 *
 * A Cloud Resource connection creates a service account that can be granted access
 * to other Google Cloud resources.
 *
 * @param {string} projectId The Google Cloud project ID. for example, 'example-project-id'
 * @param {string} location The location of the project to create the connection in. for example, 'us-central1'
 * @param {string} connectionId The ID of the connection to create. for example, 'example-connection-id'
 */
async function createConnection(projectId, location, connectionId) {
  const parent = client.locationPath(projectId, location);

  const connection = {
    friendlyName: 'Example Connection',
    description: 'A sample connection for a Cloud Resource',
    // The service account for this cloudResource will be created by the API.
    // Its ID will be available in the response.
    cloudResource: {},
  };

  const request = {
    parent,
    connectionId,
    connection,
  };

  try {
    const [response] = await client.createConnection(request);

    console.log(`Successfully created connection: ${response.name}`);
    console.log(`Friendly name: ${response.friendlyName}`);

    console.log(`Service Account: ${response.cloudResource.serviceAccountId}`);
  } catch (err) {
    if (err.code === status.ALREADY_EXISTS) {
      console.log(`Connection '${connectionId}' already exists.`);
    } else {
      console.error(`Error creating connection: ${err.message}`);
    }
  }
}
```

### Java

Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](https://docs.cloud.google.com/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Java API reference documentation](https://docs.cloud.google.com/java/docs/reference/google-cloud-bigquery/latest/overview) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](https://docs.cloud.google.com/bigquery/docs/authentication#client-libs) .

```java
import com.google.api.gax.rpc.AlreadyExistsException;
import com.google.api.gax.rpc.ApiException;
import com.google.cloud.bigquery.connection.v1.CloudResourceProperties;
import com.google.cloud.bigquery.connection.v1.Connection;
import com.google.cloud.bigquery.connection.v1.CreateConnectionRequest;
import com.google.cloud.bigquery.connection.v1.LocationName;
import com.google.cloud.bigqueryconnection.v1.ConnectionServiceClient;
import java.io.IOException;

public class CreateConnection {

  /**
   * Creates a BigQuery connection to a Cloud Resource. A Cloud Resource connection provisions a
   * service account that can be granted access to other Google Cloud resources for federated
   * queries.
   *
   * @param projectId The Google Cloud project ID (for example, "example-project-id").
   * @param location The geographic location of the connection (for example, "us-central1").
   * @param connectionId The ID of the connection to create (for example, "example-connection-id").
   */
  public static void createConnection(String projectId, String location, String connectionId) {
    LocationName parent = LocationName.of(projectId, location);

    // CloudResourceProperties provisions a managed Google Cloud service account on creation.
    CloudResourceProperties cloudResourceProperties = CloudResourceProperties.newBuilder().build();
    Connection connection =
        Connection.newBuilder()
            .setFriendlyName("Example Connection")
            .setDescription("Cloud Resource connection for federated queries.")
            .setCloudResource(cloudResourceProperties)
            .build();

    CreateConnectionRequest request =
        CreateConnectionRequest.newBuilder()
            .setParent(parent.toString())
            .setConnectionId(connectionId)
            .setConnection(connection)
            .build();

    try (ConnectionServiceClient client = ConnectionServiceClient.create()) {
      Connection response = client.createConnection(request);

      System.out.printf("Successfully created connection: %s%n", response.getName());
      System.out.printf("Friendly name: %s%n", response.getFriendlyName());
      System.out.printf(
          "Service Account: %s%n", response.getCloudResource().getServiceAccountId());
    } catch (AlreadyExistsException err) {
      System.err.printf(
          "error: connection '%s' already exists in location '%s' for project '%s': %s%n",
          connectionId, location, projectId, err.getMessage());
    } catch (ApiException | IOException err) {
      System.err.printf(
          "error: failed to create connection '%s' in location '%s' for project '%s': %s%n",
          connectionId, location, projectId, err.getMessage());
    }
  }
```

### Terraform

Use the [`google_bigquery_connection`](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/bigquery_connection) resource.

> **Note:** To create BigQuery objects using Terraform, you must enable the [Cloud Resource Manager API](https://docs.cloud.google.com/resource-manager/reference/rest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](https://docs.cloud.google.com/bigquery/docs/authentication#client-libs) .

The following example creates a Cloud resource connection named `my_cloud_resource_connection` in the `US` region:

```terraform
# This queries the provider for project information.
data "google_project" "default" {}

# This creates a cloud resource connection in the US region named my_cloud_resource_connection.
# Note: The cloud resource nested object has only one output field - serviceAccountId.
resource "google_bigquery_connection" "default" {
  connection_id = "my_cloud_resource_connection"
  project       = data.google_project.default.project_id
  location      = "US"
  cloud_resource {}
}
```

To apply your Terraform configuration in a Google Cloud project, complete the steps in the following sections.

## Prepare Cloud Shell

1.  Launch [Cloud Shell](https://shell.cloud.google.com/) .

2.  Set the default Google Cloud project where you want to apply your Terraform configurations.

    You only need to run this command once per project, and you can run it in any directory.

    ```
    export GOOGLE_CLOUD_PROJECT=PROJECT_ID
    ```

    Environment variables are overridden if you set explicit values in the Terraform configuration file.

## Prepare the directory

Each Terraform configuration file must have its own directory (also called a *root module* ).

1.  In [Cloud Shell](https://shell.cloud.google.com/) , create a directory and a new file within that directory. The filename must have the `.tf` extension—for example `main.tf` . In this tutorial, the file is referred to as `main.tf` .

    ```
    mkdir DIRECTORY && cd DIRECTORY && touch main.tf
    ```

2.  If you are following a tutorial, you can copy the sample code in each section or step.

    Copy the sample code into the newly created `main.tf` .

    Optionally, copy the code from GitHub. This is recommended when the Terraform snippet is part of an end-to-end solution.

3.  Review and modify the sample parameters to apply to your environment.

4.  Save your changes.

5.  Initialize Terraform. You only need to do this once per directory.

    ```
    terraform init
    ```

    Optionally, to use the latest Google provider version, include the `-upgrade` option:

    ```
    terraform init -upgrade
    ```

## Apply the changes

1.  Review the configuration and verify that the resources that Terraform is going to create or update match your expectations:

    ```
    terraform plan
    ```

    Make corrections to the configuration as necessary.

2.  Apply the Terraform configuration by running the following command and entering `yes` at the prompt:

    ```
    terraform apply
    ```

    Wait until Terraform displays the "Apply complete!" message.

3.  [Open your Google Cloud project](https://console.cloud.google.com/) to view the results. In the Google Cloud console, navigate to your resources in the UI to make sure that Terraform has created or updated them.

> **Note:** Terraform samples typically assume that the required APIs are enabled in your Google Cloud project.

### Grant permissions to the connection's service account

Grant the connection's service account the Storage Object Viewer ( `roles/storage.objectViewer` ) role so that the object table can read image files in Cloud Storage:

### Console

1.  Go to the **IAM & Admin** page.

2.  Click **Grant access** .

3.  In the **New principals** field, enter the service account ID that you copied earlier.

4.  In the **Select a role** field, choose **Cloud Storage** , and then select **Storage Object Viewer** .

5.  Click **Save** .

### gcloud

Use the [`gcloud projects add-iam-policy-binding` command](https://docs.cloud.google.com/sdk/gcloud/reference/projects/add-iam-policy-binding) :

```
gcloud projects add-iam-policy-binding PROJECT_ID \
    --member='serviceAccount:MEMBER' \
    --role='roles/storage.objectViewer' \
    --condition=None
```

Replace the following:

- `PROJECT_ID` : your Google Cloud project ID
- `MEMBER` : the service account ID that you copied earlier

## Create an object table

Use the [`CREATE EXTERNAL TABLE` statement](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_external_table_statement) to create an [object table](https://docs.cloud.google.com/bigquery/docs/object-tables) named `product_images` over a public Cloud Storage bucket of Cymbal Pets product images:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, run the following statement:

    ```
    CREATE OR REPLACE EXTERNAL TABLE `bqml_tutorial.product_images`
      WITH CONNECTION `us.CONNECTION_ID`
      OPTIONS (
        object_metadata = 'SIMPLE',
        uris = ['gs://cloud-samples-data/bigquery/tutorials/cymbal-pets/images/*.png']
      );
    ```

    Replace `CONNECTION_ID` with the ID of the BigQuery connection that you created—for example, `myconnection` . When you [view the connection details](https://docs.cloud.google.com/bigquery/docs/working-with-connections#view-connections) in the Google Cloud console, this value is the last segment of the fully qualified ID shown in **Connection ID** (for example, `projects/myproject/locations/us/connections/myconnection` ).

## Import a model into BigQuery ML

Use the [`CREATE MODEL` statement](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-onnx) to import a prebuilt ResNet-18 image classification model in ONNX format from a public Cloud Storage bucket into your dataset. If you want to use your own TensorFlow, TensorFlow Lite, or ONNX model, [upload the model artifacts](https://docs.cloud.google.com/storage/docs/uploading-objects) to a Cloud Storage bucket and specify your bucket URI in `MODEL_PATH` .

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, run the following statement:

    ```
    CREATE OR REPLACE MODEL `bqml_tutorial.imported_onnx_model`
      OPTIONS (
        MODEL_TYPE = 'ONNX',
        MODEL_PATH = 'gs://cloud-samples-data/bigquery/ml/onnx/resnet18.onnx'
      );
    ```

    The query takes several seconds to complete, after which `imported_onnx_model` appears in the `bqml_tutorial` dataset in the **Explorer** pane. Because the query uses a `CREATE MODEL` statement, there are no query results.

## Inspect the model

Inspect the imported model to identify its expected input and output field names. You reference these field names when you run inference on the object table:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click **Explorer** . If you don't see the left pane, click **Expand left pane** to open it.

3.  In the **Explorer** pane, expand your project, click **Datasets** , and then click `bqml_tutorial` .

4.  Click the **Models** tab, and then click `imported_onnx_model` .

    - **Label Column** shows the output field returned by the model: `class_label` ( `INT64` ), which represents the predicted [ImageNet class ID](https://raw.githubusercontent.com/pytorch/hub/master/imagenet_classes.txt) .
    - **Feature Columns** shows the input field expected by the model: `input` ( `FLOAT64` `REPEATED` ). For ResNet-18, each decoded image must be resized to `224` by `224` pixels and aliased as `input` .

    If you import your own TensorFlow SavedModel and need to check the exact input tensor dimensions, install TensorFlow locally and run the [`saved_model_cli show` command](https://www.tensorflow.org/guide/saved_model#show_command) .

## Run inference on the object table

Classify the ball product images in the `product_images` object table by using the [`ML.PREDICT` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-predict) . Inside the input subquery, the [`ML.DECODE_IMAGE` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-decode-image) converts raw image bytes from the object table's `data` column into a multi-dimensional `ARRAY` , and the [`ML.RESIZE_IMAGE` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-resize-image) resizes each image to `224` by `224` pixels to match the model's `input` feature. If your model requires a different color space or `[0, 255)` integer pixel values, you can also chain the [`ML.CONVERT_COLOR_SPACE`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-convert-color-space) or [`ML.CONVERT_IMAGE_TYPE`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-convert-image-type) functions.

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, run the following statement to classify the products in the object table that contain the word *ball* in their URI:

    ```
    SELECT
      uri,
      class_label
    FROM
      ML.PREDICT(
        MODEL `bqml_tutorial.imported_onnx_model`,
        (
          SELECT
            uri,
            ML.RESIZE_IMAGE(ML.DECODE_IMAGE(data), 224, 224, FALSE) AS input
          FROM
            `bqml_tutorial.product_images`
          WHERE
            uri LIKE '%-ball%'
        )
      );
    ```

    The output is similar to the following:

    ```console
    +-----------------------------------------------------------------------------------------------------+-------------+
    | uri                                                                                                 | class_label |
    +-----------------------------------------------------------------------------------------------------+-------------+
    | gs://cloud-samples-data/bigquery/tutorials/cymbal-pets/images/playful-pup-tennis-ball.png           | 852         |
    | gs://cloud-samples-data/bigquery/tutorials/cymbal-pets/images/cozy-naps-catnip-toy-ball.png         | 911         |
    | gs://cloud-samples-data/bigquery/tutorials/cymbal-pets/images/fluffy-buns-hamster-exercise-ball.png | 768         |
    | ...                                                                                                 | ...         |
    +-----------------------------------------------------------------------------------------------------+-------------+
    ```

    Each `class_label` value maps to a zero-indexed entry in the [ImageNet labels](https://raw.githubusercontent.com/pytorch/hub/master/imagenet_classes.txt) list. For example, `852` corresponds to `tennis ball` for the Playful Pup Tennis Ball product image.

## Save preprocessed images for repeated inference

If you plan to run multiple inference queries or compare several models on the same images, you can materialize the decoded and resized image arrays in a standard BigQuery table so that you don't decode the raw image files on every query:

1.  In the query editor, write the decoded and resized images to a standard table:

    ```
    CREATE OR REPLACE TABLE `bqml_tutorial.preprocessed_images` AS (
      SELECT
        uri,
        ML.RESIZE_IMAGE(ML.DECODE_IMAGE(data), 224, 224, FALSE) AS input
      FROM
        `bqml_tutorial.product_images`
      WHERE
        uri LIKE '%-ball%'
    );
    ```

2.  Run `ML.PREDICT` directly on the `preprocessed_images` table:

    ```
    SELECT
      uri,
      class_label
    FROM
      ML.PREDICT(
        MODEL `bqml_tutorial.imported_onnx_model`,
        (
          SELECT
            uri,
            input
          FROM
            `bqml_tutorial.preprocessed_images`
        )
      );
    ```

    The query returns the same `uri` and `class_label` predictions without re-reading or decoding the source PNG files from Cloud Storage.

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

If you want to reuse your project, delete the individual resources that you created for this tutorial:

### Console

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  Delete the `bqml_tutorial` dataset. Deleting the dataset also deletes the object table, the `preprocessed_images` table, and the imported model:

    1.  In the **Explorer** pane, expand your project and click **Datasets** .
    2.  Click `bqml_tutorial` .
    3.  In the details pane, click **Delete** .
    4.  In the **Delete dataset** dialog, click **Delete** .

3.  Delete the connection:

    1.  In the **Explorer** pane, expand your project and click **Connections** .
    2.  Click the connection that you created.
    3.  In the details pane, click **Delete** .
    4.  In the **Delete connection** dialog, enter `delete` , and then click **Delete** .

4.  If you created the `bqml-tutorial-reservation` reservation for this tutorial, delete the assignment and reservation to avoid continued slot charges:

    1.  In the navigation menu, click **Capacity management** .
    2.  In the **Slot reservations** table, expand `bqml-tutorial-reservation` .
    3.  Next to your project assignment, click **Actions \> Delete** , and then confirm deletion.
    4.  Next to `bqml-tutorial-reservation` , click **Actions \> Delete** , and then confirm deletion.

### bq

1.  Delete the `bqml_tutorial` dataset and all tables and models in it:

    ```
    bq rm --dataset --recursive --force bqml_tutorial
    ```

2.  Delete the connection:

    ```
    bq rm --connection PROJECT_ID.us.CONNECTION_ID
    ```

    Replace the following:

    - `PROJECT_ID` : your project ID
    - `CONNECTION_ID` : the ID of the connection that you created

3.  If you created the `bqml-tutorial-reservation` reservation, remove its project assignment and delete the reservation:

    ```
    bq rm --project_id=PROJECT_ID --location=us \
      --reservation_assignment \
      bqml-tutorial-reservation.ASSIGNMENT_ID
    bq rm --project_id=PROJECT_ID --location=us \
      --reservation bqml-tutorial-reservation
    ```

    Replace the following:

    - `PROJECT_ID` : your project ID
    - `ASSIGNMENT_ID` : the ID of the reservation assignment. To get the assignment ID, see [Find a project's reservation assignment](https://docs.cloud.google.com/bigquery/docs/reservations-assignments#list-assignment) .

## What's next

- Try [running inference on an object table by using a ResNet 50 classification model](https://docs.cloud.google.com/bigquery/docs/inference-tutorial-resnet) .
- Try [running inference on an object table by using a MobileNet V3 feature vector model](https://docs.cloud.google.com/bigquery/docs/inference-tutorial-mobilenet) .
- Learn how to [analyze images with a Gemini model](https://docs.cloud.google.com/bigquery/docs/image-analysis) or [annotate images with the `ML.ANNOTATE_IMAGE` function](https://docs.cloud.google.com/bigquery/docs/annotate-image) .
- Learn how to [analyze object tables by using remote functions](https://docs.cloud.google.com/bigquery/docs/object-table-remote-function) .
- See more image preprocessing examples in the [`ML.DECODE_IMAGE` reference documentation](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-decode-image#examples) .
