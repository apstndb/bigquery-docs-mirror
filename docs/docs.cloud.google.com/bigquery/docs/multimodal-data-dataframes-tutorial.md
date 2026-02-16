# Analyze multimodal data in Python with BigQuery DataFrames

**Preview**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

**Note:** To provide feedback or request support for this feature, send an email to <bq-objectref-feedback@google.com> .

This tutorial shows you how to [analyze multimodal data](/bigquery/docs/analyze-multimodal-data) in a Python notebook by using [BigQuery DataFrames](/bigquery/docs/bigquery-dataframes-introduction) classes and methods.

This tutorial uses the product catalog from the public Cymbal pet store dataset.

To upload a notebook already populated with the tasks covered in this tutorial, see [BigFrames Multimodal DataFrame](https://console.cloud.google.com/bigquery/import?url=https://github.com/googleapis/python-bigquery-dataframes/blob/main/notebooks/experimental/multimodal_dataframe.ipynb) .

## Objectives

  - Create multimodal DataFrames.
  - Combine structured and unstructured data in a DataFrame.
  - Transform images.
  - Generate text and embeddings based on image data.
  - Chunk PDFs for further analysis.

## Costs

In this document, you use the following billable components of Google Cloud:

  - **BigQuery** : you incur costs for the data that you process in BigQuery.
  - **BigQuery Python UDFs** : you incur costs for using BigQuery DataFrames image transformation and chunk PDF methods.
  - **Cloud Storage** : you incur costs for the objects stored in Cloud Storage.
  - **Vertex AI** : you incur costs for calls to Vertex AI models.

To generate a cost estimate based on your projected usage, use the [pricing calculator](/products/calculator) .

New Google Cloud users might be eligible for a [free trial](/free) .

For more information about, see the following pricing pages:

  - [BigQuery pricing](https://cloud.google.com/bigquery/pricing)
  - [BigQuery Python UDF pricing](/bigquery/docs/user-defined-functions-python#pricing)
  - [Cloud Storage pricing](https://cloud.google.com/storage/pricing)
  - [Vertex AI pricing](/vertex-ai/generative-ai/pricing)

## Before you begin

1.  In the Google Cloud console, on the project selector page, select or create a Google Cloud project.
    
    **Roles required to select or create a project**
    
      - **Select a project** : Selecting a project doesn't require a specific IAM role—you can select any project that you've been granted a role on.
      - **Create a project** : To create a project, you need the Project Creator role ( `  roles/resourcemanager.projectCreator  ` ), which contains the `  resourcemanager.projects.create  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .
    
    **Note** : If you don't plan to keep the resources that you create in this procedure, create a project instead of selecting an existing project. After you finish these steps, you can delete the project, removing all resources associated with the project.

2.  [Verify that billing is enabled for your Google Cloud project](/billing/docs/how-to/verify-billing-enabled#confirm_billing_is_enabled_on_a_project) .

3.  Enable the BigQuery, BigQuery Connection, Cloud Storage, and Vertex AI APIs.
    
    **Roles required to enable APIs**
    
    To enable APIs, you need the Service Usage Admin IAM role ( `  roles/serviceusage.serviceUsageAdmin  ` ), which contains the `  serviceusage.services.enable  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .

### Required roles

To get the permissions that you need to complete this tutorial, ask your administrator to grant you the following IAM roles:

  - Create a connection: [BigQuery Connection Admin](/iam/docs/roles-permissions/bigquery#bigquery.connectionAdmin) ( `  roles/bigquery.connectionAdmin  ` )
  - Grant permissions to the connection's service account: [Project IAM Admin](/iam/docs/roles-permissions/resourcemanager#resourcemanager.projectIamAdmin) ( `  roles/resourcemanager.projectIamAdmin  ` )
  - Create a Cloud Storage bucket: [Storage Admin](/iam/docs/roles-permissions/storage#storage.admin) ( `  roles/storage.admin  ` )
  - Run BigQuery jobs: [BigQuery User](/iam/docs/roles-permissions/bigquery#bigquery.user) ( `  roles/bigquery.user  ` )
  - Create and call Python UDFs: [BigQuery Data Editor](/iam/docs/roles-permissions/bigquery#bigquery.dataEditor) ( `  roles/bigquery.dataEditor  ` )
  - Create URLs that let you read and modify Cloud Storage objects: [BigQuery ObjectRef Admin](/iam/docs/roles-permissions/bigquery#bigquery.objectRefAdmin) ( `  roles/bigquery.objectRefAdmin  ` )
  - Use notebooks:
      - [BigQuery Read Session User](/iam/docs/roles-permissions/bigquery#bigquery.readSessionUser) ( `  roles/bigquery.readSessionUser  ` )
      - [Notebook Runtime User](/iam/docs/roles-permissions/aiplatform#aiplatform.notebookRuntimeUser) ( `  roles/aiplatform.notebookRuntimeUser  ` )
      - [Notebook Runtime User](/iam/docs/roles-permissions/aiplatform#aiplatform.notebookRuntimeUser) ( `  roles/aiplatform.notebookRuntimeUser  ` )
      - [Code Creator](/iam/docs/roles-permissions/dataform#dataform.codeCreator) ( `  roles/dataform.codeCreator  ` )

For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

## Set up

In this section, you create the Cloud Storage bucket, connection, and notebook used in this tutorial.

### Create a bucket

Create a Cloud Storage bucket for storing transformed objects:

1.  In the Google Cloud console, go to the **Buckets** page.

2.  Click add\_box **Create** .

3.  On the **Create a bucket** page, in the **Get started** section, enter a globally unique name that meets the [bucket name requirements](/storage/docs/buckets#naming) .

4.  Click **Create** .

### Create a connection

Create a [Cloud resource connection](/bigquery/docs/create-cloud-resource-connection) and get the connection's service account. BigQuery uses the connection to access objects in Cloud Storage.

1.  Go to the **BigQuery** page.

2.  In the **Explorer** pane, click add **Add data** .
    
    The **Add data** dialog opens.

3.  In the **Filter By** pane, in the **Data Source Type** section, select **Business Applications** .
    
    Alternatively, in the **Search for data sources** field, you can enter `  Vertex AI  ` .

4.  In the **Featured data sources** section, click **Vertex AI** .

5.  Click the **Vertex AI Models: BigQuery Federation** solution card.

6.  In the **Connection type** list, select **Vertex AI remote models, remote functions, BigLake and Spanner (Cloud Resource)** .

7.  In the **Connection ID** field, type `  bigframes-default-connection  ` .

8.  Click **Create connection** .

9.  Click **Go to connection** .

10. In the **Connection info** pane, copy the service account ID for use in a later step.

### Grant permissions to the connection's service account

Grant the connection's service account the roles that it needs to access Cloud Storage and Vertex AI. You must grant these roles in the same project you created or selected in the [Before you begin](#before_you_begin) section.

To grant the role, follow these steps:

1.  Go to the **IAM & Admin** page.

2.  Click person\_add **Grant access** .

3.  In the **New principals** field, enter the service account ID that you copied earlier.

4.  In the **Select a role** field, choose **Cloud Storage** , and then select **Storage Object User** .

5.  Click **Add another role** .

6.  In the **Select a role** field, select **Vertex AI** , and then select **Vertex AI User** .

7.  Click **Save** .

### Create a notebook

Create a notebook where you can run Python code:

1.  Go to the **BigQuery** page.

2.  In the tab bar of the editor pane, click the arrow\_drop\_down drop-down arrow next to add\_box **SQL query** , and then click **Notebook** .

3.  In the **Start with a template** pane, click **Close** .

4.  Click **Connect \> Connect to a runtime** .

5.  If you have an existing runtime, accept the default settings and click **Connect** . If you don't have an existing runtime, select **Create new Runtime** , and then click **Connect** .
    
    It might take several minutes for the runtime to get set up.

## Create a multimodal DataFrame

Create a multimodal DataFrame that integrates structured and unstructured data by using the [`  from_glob_path  ` method](/python/docs/reference/bigframes/latest/bigframes.session.Session#bigframes_session_Session_from_glob_path) of the [`  Session  ` class](/python/docs/reference/bigframes/latest/bigframes.session.Session) :

1.  In the notebook, create a code cell and copy the following code into it:
    
    ``` python
    import bigframes
    
    # Flags to control preview image/video preview size
    bigframes.options.display.blob_display_width = 300
    
    import bigframes.pandas as bpd
    
    # Create blob columns from wildcard path.
    df_image = bpd.from_glob_path(
        "gs://cloud-samples-data/bigquery/tutorials/cymbal-pets/images/*", name="image"
    )
    # Other ways are: from string uri column
    # df = bpd.DataFrame({"uri": ["gs://<my_bucket>/<my_file_0>", "gs://<my_bucket>/<my_file_1>"]})
    # df["blob_col"] = df["uri"].str.to_blob()
    
    # From an existing object table
    # df = bpd.read_gbq_object_table("<my_object_table>", name="blob_col")
    
    # Take only the 5 images to deal with. Preview the content of the Mutimodal DataFrame
    df_image = df_image.head(5)
    df_image
    ```

2.  Click play\_circle\_filled **Run** .
    
    The final call to `  df_image  ` returns the images that have been added to the DataFrame. Alternatively, you could call the `  .display  ` method.

## Combine structured and unstructured data in the DataFrame

Combine text and image data in the multimodal DataFrame:

1.  In the notebook, create a code cell and copy the following code into it:
    
    ``` python
    # Combine unstructured data with structured data
    df_image["author"] = ["alice", "bob", "bob", "alice", "bob"]  # type: ignore
    df_image["content_type"] = df_image["image"].blob.content_type()
    df_image["size"] = df_image["image"].blob.size()
    df_image["updated"] = df_image["image"].blob.updated()
    df_image
    ```

2.  Click **Run** play\_circle\_filled .
    
    The code returns the DataFrame data.

3.  In the notebook, create a code cell and copy the following code into it:
    
    ``` python
    # Filter images and display, you can also display audio and video types. Use width/height parameters to constrain window sizes.
    df_image[df_image["author"] == "alice"]["image"].blob.display()
    ```

4.  Click **Run** play\_circle\_filled .
    
    The code returns images from the DataFrame where the `  author  ` column value is `  alice  ` .

## Perform image transformations

Transform image data by using the following methods of the [`  Series.BlobAccessor  ` class](/python/docs/reference/bigframes/latest/bigframes.operations.blob.BlobAccessor) :

  - [`  image_blur  `](/python/docs/reference/bigframes/latest/bigframes.operations.blob.BlobAccessor#bigframes_operations_blob_BlobAccessor_image_blur)
  - [`  image_normalize  `](/python/docs/reference/bigframes/latest/bigframes.operations.blob.BlobAccessor#bigframes_operations_blob_BlobAccessor_image_normalize)
  - [`  image_resize  `](/python/docs/reference/bigframes/latest/bigframes.operations.blob.BlobAccessor#bigframes_operations_blob_BlobAccessor_image_resize)

The transformed images are written to Cloud Storage.

Transform images:

1.  In the notebook, create a code cell and copy the following code into it:
    
    ``` python
    df_image["blurred"] = df_image["image"].blob.image_blur(
        (20, 20), dst=f"{dst_bucket}/image_blur_transformed/", engine="opencv"
    )
    df_image["resized"] = df_image["image"].blob.image_resize(
        (300, 200), dst=f"{dst_bucket}/image_resize_transformed/", engine="opencv"
    )
    df_image["normalized"] = df_image["image"].blob.image_normalize(
        alpha=50.0,
        beta=150.0,
        norm_type="minmax",
        dst=f"{dst_bucket}/image_normalize_transformed/",
        engine="opencv",
    )
    
    # You can also chain functions together
    df_image["blur_resized"] = df_image["blurred"].blob.image_resize(
        (300, 200), dst=f"{dst_bucket}/image_blur_resize_transformed/", engine="opencv"
    )
    df_image
    ```

2.  Update all references to `  {dst_bucket}  ` to refer to the [bucket that you created](#create_a_bucket) , in the format `  gs:// mybucket  ` .

3.  Click **Run** play\_circle\_filled .
    
    The code returns the original images as well as all of their transformations.

## Generate text

Generate text from multimodal data by using the [`  predict  ` method](/python/docs/reference/bigframes/latest/bigframes.ml.llm.GeminiTextGenerator#bigframes_ml_llm_GeminiTextGenerator_predict) of the [`  GeminiTextGenerator  ` class](/python/docs/reference/bigframes/latest/bigframes.ml.llm.GeminiTextGenerator) :

1.  In the notebook, create a code cell and copy the following code into it:
    
    ``` python
    from bigframes.ml import llm
    
    gemini = llm.GeminiTextGenerator(model_name="gemini-2.0-flash-001")
    
    # Deal with first 2 images as example
    df_image = df_image.head(2)
    
    # Ask the same question on the images
    df_image = df_image.head(2)
    answer = gemini.predict(df_image, prompt=["what item is it?", df_image["image"]])
    answer[["ml_generate_text_llm_result", "image"]]
    ```

2.  Click **Run** play\_circle\_filled .
    
    The code returns the first two images in `  df_image  ` , along with text generated in response to the question `  what item is it?  ` for both images.

3.  In the notebook, create a code cell and copy the following code into it:
    
    ``` python
    # Ask different questions
    df_image["question"] = [  # type: ignore
        "what item is it?",
        "what color is the picture?",
    ]
    answer_alt = gemini.predict(
        df_image, prompt=[df_image["question"], df_image["image"]]
    )
    answer_alt[["ml_generate_text_llm_result", "image"]]
    ```

4.  Click **Run** play\_circle\_filled .
    
    The code returns the first two images in `  df_image  ` , with text generated in response to the question `  what item is it?  ` for the first image, and text generated in response to the question `  what color is the picture?  ` for the second image.

## Generate embeddings

Generate embeddings for multimodal data by using the [`  predict  ` method](/python/docs/reference/bigframes/latest/bigframes.ml.llm.MultimodalEmbeddingGenerator#bigframes_ml_llm_MultimodalEmbeddingGenerator_predict) of the [`  MultimodalEmbeddingGenerator  ` class](/python/docs/reference/bigframes/latest/bigframes.ml.llm.MultimodalEmbeddingGenerator) :

1.  In the notebook, create a code cell and copy the following code into it:
    
    ``` python
    # Generate embeddings on images
    embed_model = llm.MultimodalEmbeddingGenerator()
    embeddings = embed_model.predict(df_image["image"])
    embeddings
    ```

2.  Click **Run** play\_circle\_filled .
    
    The code returns the embeddings generated by a call to an embedding model.

## Chunk PDFs

Chunk PDF objects by using the [`  pdf_chunk  ` method](/python/docs/reference/bigframes/latest/bigframes.operations.blob.BlobAccessor#bigframes_operations_blob_BlobAccessor_pdf_chunk) of the [`  Series.BlobAccessor  ` class](/python/docs/reference/bigframes/latest/bigframes.operations.blob.BlobAccessor) :

1.  In the notebook, create a code cell and copy the following code into it:
    
    ``` python
    # PDF chunking
    df_pdf = bpd.from_glob_path(
        "gs://cloud-samples-data/bigquery/tutorials/cymbal-pets/documents/*", name="pdf"
    )
    df_pdf["chunked"] = df_pdf["pdf"].blob.pdf_chunk(engine="pypdf")
    chunked = df_pdf["chunked"].explode()
    chunked
    ```

2.  Click **Run** play\_circle\_filled .
    
    The code returns the chunked PDF data.

## Clean up

**Caution** : Deleting a project has the following effects:

  - **Everything in the project is deleted.** If you used an existing project for the tasks in this document, when you delete it, you also delete any other work you've done in the project.
  - **Custom project IDs are lost.** When you created this project, you might have created a custom project ID that you want to use in the future. To preserve the URLs that use the project ID, such as an `  appspot.com  ` URL, delete selected resources inside the project instead of deleting the whole project.

If you plan to explore multiple architectures, tutorials, or quickstarts, reusing projects can help you avoid exceeding project quota limits.

In the Google Cloud console, go to the **Manage resources** page.

In the project list, select the project that you want to delete, and then click **Delete** .

In the dialog, type the project ID, and then click **Shut down** to delete the project.
