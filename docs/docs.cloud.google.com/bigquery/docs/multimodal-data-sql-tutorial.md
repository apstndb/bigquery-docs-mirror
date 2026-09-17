---
name: documents/docs.cloud.google.com/bigquery/docs/multimodal-data-sql-tutorial
uri: https://docs.cloud.google.com/bigquery/docs/multimodal-data-sql-tutorial
title: Analyze multimodal data with SQL, object tables, and BigQuery DataFrames
description: Use ObjectRef values, SQL functions, and Generative AI functions to process multimodal data.
data_source: docs.cloud.google.com
---

This tutorial shows you how to use SQL queries, the [`AI.GENERATE` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate) , the [`AI.EMBED` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-embed) and [BigQuery DataFrames](https://docs.cloud.google.com/bigquery/docs/bigquery-dataframes-introduction) to [analyze multimodal data](https://docs.cloud.google.com/bigquery/docs/analyze-multimodal-data) from the Cymbal pet store public dataset.

The `AI.GENERATE` function lets you analyze any combination of structured and unstructured data, and the `AI.EMBED` function lets you create [embeddings](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-embed#embeddings) from text or image data in BigQuery.

You find similar images by using the [`VECTOR_SEARCH`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/search_functions#vector_search) function. The `VECTOR_SEARCH` function lets you perform a semantic search or a hybrid search on embeddings to find similar entities.

This tutorial uses a persistent [object table](https://docs.cloud.google.com/bigquery/docs/object-table-introduction) that stores `ObjectRef` values.

## Objectives

  - Use `ObjectRef` values to store image data alongside structured data in a BigQuery table.
  - Use the `AI.GENERATE` function to enrich your data.
  - Use the `AI.EMBED` function to generate embeddings based on image data.
  - Use the `VECTOR_SEARCH` function to find similar images.
  - Use arrays of `ObjectRef` values to summarize user manuals.

## Costs

In this document, you use the following billable components of Google Cloud:

  - **BigQuery** : you incur costs for the data that you process in BigQuery.
  - **Cloud Storage** : you incur costs for reading the objects stored in Cloud Storage.
  - **Gemini Enterprise Agent Platform** : you incur costs for calls to Agent Platform models.

To generate a cost estimate based on your projected usage, use the [pricing calculator](https://docs.cloud.google.com/products/calculator) .

New Google Cloud users might be eligible for a [free trial](https://docs.cloud.google.com/free) .

For more information about costs, see the following pricing pages:

  - [BigQuery pricing](https://cloud.google.com/bigquery/pricing)
  - [Cloud Storage pricing](https://cloud.google.com/storage/pricing)
  - [Agent Platform pricing](https://docs.cloud.google.com/vertex-ai/generative-ai/pricing)

## Before you begin

1.  In the Google Cloud console, on the project selector page, select or create a Google Cloud project.
    
    **Roles required to select or create a project**
    
      - **Select a project** : Selecting a project doesn't require a specific IAM role—you can select any project that you've been granted a role on.
      - **Create a project** : To create a project, you need the Project Creator role ( `roles/resourcemanager.projectCreator` ), which contains the `resourcemanager.projects.create` permission. [Learn how to grant roles](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .
    
    > **Note** : If you don't plan to keep the resources that you create in this procedure, create a project instead of selecting an existing project. After you finish these steps, you can delete the project, removing all resources associated with the project.

2.  [Verify that billing is enabled for your Google Cloud project](https://docs.cloud.google.com/billing/docs/how-to/verify-billing-enabled#confirm_billing_is_enabled_on_a_project) .

3.  Enable the BigQuery, BigQuery Connection, Cloud Storage, and Agent Platform API APIs.
    
    **Roles required to enable APIs**
    
    To enable APIs, you need the `serviceusage.services.enable` permission. If you created the project, then you likely already have this permission through the Owner role ( `roles/owner` ). Otherwise, you can get this permission through the Service Usage Admin role ( `roles/serviceusage.serviceUsageAdmin` ). [Learn how to grant roles](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

### Required roles

To get the permissions that you need to complete this tutorial, ask your administrator to grant you the following IAM roles:

  - Create datasets and tables: [BigQuery Data Owner](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner) ( `roles/bigquery.dataOwner` )
  - Run BigQuery jobs: [BigQuery Job User](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.jobUser) ( `roles/bigquery.jobUser` )
  - Create connections: [BigQuery Connection Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.connectionAdmin) ( `roles/bigquery.connectionAdmin` )
  - Grant permissions to a connection's service account: [Project IAM Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/resourcemanager#resourcemanager.projectIamAdmin) ( `roles/resourcemanager.projectIamAdmin` )
  - Create URLs that let you read and modify Cloud Storage objects: [BigQuery ObjectRef Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.objectRefAdmin) ( `roles/bigquery.objectRefAdmin` )

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## Create the dataset, tables, models, and connection

In this section, you create the dataset, connection, tables, and models used in this tutorial.

### Create a dataset

Create a BigQuery dataset to contain the objects you create in this tutorial by choosing one of the following:

### Console

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :
    
    ![Highlighted button for the Explorer pane.](https://docs.cloud.google.com/static/bigquery/images/explorer-tab.png)
    
    If you don't see the left pane, click last\_page **Expand left pane** to open the pane.

3.  In **Explorer** , expand your project, and then click **Datasets** .

4.  On the **Datasets** page, click add **Create dataset** .

5.  On the **Create dataset** page, do the following:
    
    1.  For **Dataset ID** , enter `cymbal_pets` .
    
    2.  For **Data location** , select **US** .
    
    3.  Leave the remaining default settings as they are, and click **Create dataset** .

### SQL

Use the [`CREATE SCHEMA` statement](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_schema_statement) .

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
        CREATE SCHEMA PROJECT_ID.cymbal_pets  OPTIONS (    description = 'Dataset for BigQuery ML tutorial',    location = 'US');
    
    Replace `  PROJECT_ID  ` with your project ID.

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](https://docs.cloud.google.com/bigquery/docs/running-queries#queries) .

You receive a confirmation message similar to the following: `The dataset named cymbal_pets was created.`

### Create a connection

Create a [Cloud resource connection](https://docs.cloud.google.com/bigquery/docs/create-cloud-resource-connection) and get the connection's service account. BigQuery uses the connection to access objects in Cloud Storage.

1.  In the left pane, click explore **Explorer** :
    
    ![Highlighted button for the Explorer pane.](https://docs.cloud.google.com/static/bigquery/images/explorer-tab.png)

2.  In the **Explorer** pane, click **Connections** .

3.  On the **Connections** page, click **Create connection** .

4.  On the **External data source** page, do the following:
    
    1.  For **Connection type** , choose **Vertex AI remote models, remote functions, Lakehouse and Spanner (Cloud Resource)** .
    
    2.  In the **Connection ID** field, type `cymbal_conn` .
    
    3.  Leave the remaining settings as they are, and then click **Create connection** .

5.  On the **Connections** page, click `cymbal_conn` .

6.  In the **Connection info** pane, copy the **Service account ID** value. It is required for the following steps.

### Grant permissions on to use Agent Platform models

Grant the connection's service account the Agent Platform User role to access remote models in Agent Platform. You must grant this role in the same project you created or selected previously. Granting the roles in a different project results in the error `bqcx-1234567890-abcd@gcp-sa-bigquery-condel.iam.gserviceaccount.com does not have the permission to access resource` .

To grant the service account access to use Agent Platform models, follow these steps:

1.  Go to the **IAM & Admin** page.

2.  Click person\_add **Grant access** .

3.  In the **Grant access** dialog, do the following:
    
    1.  In the **New principals** field, enter the service account ID that you copied earlier.
    
    2.  In the **Select a role** field, choose or search for **Agent Platform User** .
    
    3.  Click **Save** .

### Create the `products` table

To create a standard table that contains the Cymbal pets product information, follow these steps to load the data from Cloud Storage:

1.  In the Google Cloud console, go to the **Studio** page.

2.  To create the `products` table, choose one of the following options:
    
    ### SQL
    
    Paste this command into the query editor, and then click play\_circle **Run** :
    
        LOAD DATA OVERWRITE cymbal_pets.products
        FROM
          FILES(
            format = 'avro',
            uris = [
              'gs://cloud-samples-data/bigquery/tutorials/cymbal-pets/tables/products/products_*.avro']);
    
    You receive a confirmation message similar to the following: `Data was successfully loaded into managed table.`
    
    ### BigQuery DataFrames
    
    Before trying this sample, follow the BigQuery DataFrames setup instructions in the [BigQuery quickstart using BigQuery DataFrames](https://docs.cloud.google.com/bigquery/docs/dataframes-quickstart) . For more information, see the [BigQuery DataFrames reference documentation](https://docs.cloud.google.com/python/docs/reference/bigframes/latest) .
    
    To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up ADC for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .
    
        import bigframes.bigquery as bbq
        import bigframes.pandas as bpd
        
        bbq.load_data(
            "cymbal_pets.products",
            write_disposition="OVERWRITE",
            from_files_options={
                "format": "avro",
                "uris": [
                    "gs://cloud-samples-data/bigquery/tutorials/cymbal-pets/tables/products/products_*.avro"
                ],
            },
        )
    
        import bigframes.bigquery as bbq
        import bigframes.pandas as bpd
        
        bbq.load_data(
            "cymbal_pets.products",
            write_disposition="OVERWRITE",
            from_files_options={
                "format": "avro",
                "uris": [
                    "gs://cloud-samples-data/bigquery/tutorials/cymbal-pets/tables/products/products_*.avro"
                ],
            },
        )

### Create the `product_images` table

To create an object table ( `product_images` ) that contains the Cymbal pets product images, select one of the following options:

``` 

* { SQL }

  Paste this command into the query editor, and then click
  <span class="material-icons" aria-hidden="true">play_circle</span>
  **Run**:

  <pre class="lang-googlesql notranslate prettyprint devsite-click-to-copy">
  CREATE OR REPLACE EXTERNAL TABLE cymbal_pets.product_images
    WITH CONNECTION `us.cymbal_conn`
    OPTIONS (
      object_metadata = 'SIMPLE',
      uris = ['gs://cloud-samples-data/bigquery/tutorials/cymbal-pets/images/*.png'],
      max_staleness = INTERVAL 30 MINUTE,
      metadata_cache_mode = AUTOMATIC);
  </pre>

  You receive a confirmation message similar to the following: `This
  statement created a new table named product_images.`

* { BigQuery DataFrames }

       Before trying this sample, follow the BigQuery DataFrames
    setup instructions in the BigQuery quickstart
    using BigQuery DataFrames.
    For more information, see the
    BigQuery DataFrames reference documentation.
  To authenticate to BigQuery, set up Application Default Credentials.
    For more information, see Set
    up ADC for a local development environment.
   

    









  
  
  
  
  







  
  
  
    
  




  



  









  



  
  
  
  
  






  
  














  





  
    
  
  











  









  




  



  

  bbq.create_external_table(
    "cymbal_pets.product_images",
    replace=True,
    connection_name="us.cymbal_conn",
    options={
        "object_metadata": "SIMPLE",
        "uris": [
            "gs://cloud-samples-data/bigquery/tutorials/cymbal-pets/images/*.png"
        ],
    },
)
```

    bbq.create_external_table(
        "cymbal_pets.product_images",
        replace=True,
        connection_name="us.cymbal_conn",
        options={
            "object_metadata": "SIMPLE",
            "uris": [
                "gs://cloud-samples-data/bigquery/tutorials/cymbal-pets/images/*.png"
            ],
        },
    )

### Create models

The SQL instructions in this tutorial show how to call AI functions that don't require you to create a model. If you're following the BigQuery DataFrames instructions, select that option to create [remote models](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model) that represent a Gemini model and a multimodal embedding model.

### SQL

You can skip this step.

### BigQuery DataFrames

Before trying this sample, follow the BigQuery DataFrames setup instructions in the [BigQuery quickstart using BigQuery DataFrames](https://docs.cloud.google.com/bigquery/docs/dataframes-quickstart) . For more information, see the [BigQuery DataFrames reference documentation](https://docs.cloud.google.com/python/docs/reference/bigframes/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up ADC for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    gemini_model = bbq.ml.create_model(
        "cymbal_pets.gemini",
        replace=True,
        connection_name="us.cymbal_conn",
        options={"endpoint": "gemini-3.5-flash"},
    )

    gemini_model = bbq.ml.create_model(
        "cymbal_pets.gemini",
        replace=True,
        connection_name="us.cymbal_conn",
        options={"endpoint": "gemini-3.5-flash"},
    )

    embedding_model = bbq.ml.create_model(
        "cymbal_pets.embedding_model",
        replace=True,
        connection_name="us.cymbal_conn",
        options={"endpoint": "gemini-embedding-2"},
    )

    embedding_model = bbq.ml.create_model(
        "cymbal_pets.embedding_model",
        replace=True,
        connection_name="us.cymbal_conn",
        options={"endpoint": "gemini-embedding-2"},
    )

## Create a `products_mm` table with multimodal data

Create a `products_mm` table that contains an `image` column populated with product images from the `product_images` object table. The `image` column that is created is a [`STRUCT`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-types#struct_type) column that uses [`ObjectRef`](https://docs.cloud.google.com/bigquery/docs/work-with-objectref) values to store image data alongside structured data in a BigQuery [standard table](https://docs.cloud.google.com/bigquery/docs/tables-intro#standard-tables) .

An `ObjectRef` value is a `STRUCT` type with a predefined schema that references Cloud Storage objects for [multimodal analysis](https://docs.cloud.google.com/bigquery/docs/analyze-multimodal-data) . `ObjectRef` values can be processed by [`OBJ` functions](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/objectref_functions) , [AI functions](https://docs.cloud.google.com/bigquery/docs/generative-ai-overview) , or [Python user-defined functions](https://docs.cloud.google.com/bigquery/docs/user-defined-functions-python) .

To create and populate the `products_mm` table, follow these steps:

1.  To create a `products_mm` table, choose one of the following options:
    
    ### SQL
    
    Paste this command into the query editor, and then click play\_circle **Run** :
    
        CREATE OR REPLACE TABLE cymbal_pets.products_mm
        AS
        SELECT products.* EXCEPT (uri), ot.ref AS image FROM cymbal_pets.products
        INNER JOIN cymbal_pets.product_images ot
        ON ot.uri = products.uri;
    
    You receive a confirmation message similar to the following: `This statement created a new table named products_mm.`
    
    ### BigQuery DataFrames
    
    Before trying this sample, follow the BigQuery DataFrames setup instructions in the [BigQuery quickstart using BigQuery DataFrames](https://docs.cloud.google.com/bigquery/docs/dataframes-quickstart) . For more information, see the [BigQuery DataFrames reference documentation](https://docs.cloud.google.com/python/docs/reference/bigframes/latest) .
    
    To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up ADC for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .
    
        df_images = bpd.read_gbq("SELECT * FROM cymbal_pets.product_images")
        df_products = bpd.read_gbq("cymbal_pets.products")
        
        df_products_mm = df_images.merge(df_products, on="uri").drop(columns="uri")
        df_products_mm = df_products_mm.rename(columns={"ref": "image"})
    
        df_images = bpd.read_gbq("SELECT * FROM cymbal_pets.product_images")
        df_products = bpd.read_gbq("cymbal_pets.products")
        
        df_products_mm = df_images.merge(df_products, on="uri").drop(columns="uri")
        df_products_mm = df_products_mm.rename(columns={"ref": "image"})

2.  To view the `image` column data, choose one of the following options:
    
    ### SQL
    
    Paste this command into the query editor, and then click play\_circle **Run** :
    
        SELECT product_name, image
        FROM cymbal_pets.products_mm
    
    ### BigQuery DataFrames
    
    Before trying this sample, follow the BigQuery DataFrames setup instructions in the [BigQuery quickstart using BigQuery DataFrames](https://docs.cloud.google.com/bigquery/docs/dataframes-quickstart) . For more information, see the [BigQuery DataFrames reference documentation](https://docs.cloud.google.com/python/docs/reference/bigframes/latest) .
    
    To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up ADC for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .
    
        df_products_mm[["product_name", "image"]]
    
        df_products_mm[["product_name", "image"]]
    
    The results look similar to the following:
    
    ```console
    +--------------------------------+--------------------------------------+---------------+-------------------------------+------------------------------------------------+
    | product_name                   | image.uri                            | image.version | image.authorizer              | image.details                                  |
    +--------------------------------+--------------------------------------+---------------+-------------------------------+------------------------------------------------+
    |  AquaClear Aquarium Background | gs://cloud-samples-data/bigquery/    | 1234567891011 | myproject.region.myconnection | {"gcs_metadata":{"content_type":"image/png",   |
    |                                | tutorials/cymbal-pets/images/        |               |                               | "md5_hash":"494f63b9b137975ff3e7a11b060edb1d", |
    |                                | aquaclear-aquarium-background.png    |               |                               | "size":1282805,"updated":1742492680017000}}    |
    +--------------------------------+--------------------------------------+---------------+-------------------------------+------------------------------------------------+
    |  AquaClear Aquarium            | gs://cloud-samples-data/bigquery/    | 2345678910112 | myproject.region.myconnection | {"gcs_metadata":{"content_type":"image/png",   |
    |  Gravel Vacuum                 | tutorials/cymbal-pets/images/        |               |                               | "md5_hash":"b7bfc2e2641a77a402a1937bcf0003fd", |
    |                                | aquaclear-aquarium-gravel-vacuum.png |               |                               | "size":820254,"updated":1742492682411000}}     |
    +--------------------------------+--------------------------------------+---------------+-------------------------------+------------------------------------------------+
    | ...                            | ...                                  | ...           |                               | ...                                            |
    +--------------------------------+--------------------------------------+---------------+-------------------------------+------------------------------------------------+
    ```

## Generate product information

Use the [`AI.GENERATE` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate) to generate the following data for the pet store products:

  - Add an `image_description` column to the `products_mm` table.
  - Populate the `animal_type` , `search_keywords` , and `subcategory` columns of the `products_mm` table.
  - Run a query that returns a description of each product brand and also a count of the number of products from that brand. The brand description is generated by analyzing product information for all of the products from that brand, including product images.

With the `AI.GENERATE` function, you can choose to generate text or [structured output](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate#use_structured_output) according to a custom schema that you specify. The function works by sending requests to a Gemini model and returns a struct that contains your generated data, the full model response, and a status.

To generate the product data, follow these steps:

1.  To generate the product information using `AI.GENERATE` , choose one of the following options:
    
    ### SQL
    
    To create and populate the `image_description` column, paste the following into the query editor, and then click play\_circle **Run** :
    
        -- Add the column to the existing table
        ALTER TABLE bqml_tutorial.products_mm
        ADD COLUMN IF NOT EXISTS image_description STRING;
        
        -- Populate the new column using the AI.GENERATE function
        UPDATE bqml_tutorial.products_mm
        SET image_description = AI.GENERATE(
        ('Describe the following image: ', image),
        endpoint => 'gemini-3.5-flash'
        ).result
        WHERE image_description IS NULL;
    
    You receive a confirmation message similar to the following: `This statement altered the table named products_mm.`
    
    ### BigQuery DataFrames
    
    Before trying this sample, follow the BigQuery DataFrames setup instructions in the [BigQuery quickstart using BigQuery DataFrames](https://docs.cloud.google.com/bigquery/docs/dataframes-quickstart) . For more information, see the [BigQuery DataFrames reference documentation](https://docs.cloud.google.com/python/docs/reference/bigframes/latest) .
    
    To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up ADC for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .
    
        df_products_mm["url"] = bbq.obj.get_access_url(
            df_products_mm["image"], "R"
        ).to_frame()
        df_products_mm["prompt0"] = "Can you describe the following image?"
        
        df_products_mm["prompt"] = bbq.struct(df_products_mm[["prompt0", "url"]])
        df_products_mm = bbq.ai.generate_table(
            gemini_model, df_products_mm, output_schema={"image_description": "STRING"}
        )
        
        df_products_mm = df_products_mm[
            [
                "product_id",
                "product_name",
                "brand",
                "category",
                "subcategory",
                "animal_type",
                "search_keywords",
                "price",
                "description",
                "inventory_level",
                "supplier_id",
                "average_rating",
                "image",
                "image_description",
            ]
        ]
    
        df_products_mm["url"] = bbq.obj.get_access_url(
            df_products_mm["image"], "R"
        ).to_frame()
        df_products_mm["prompt0"] = "Can you describe the following image?"
        
        df_products_mm["prompt"] = bbq.struct(df_products_mm[["prompt0", "url"]])
        df_products_mm = bbq.ai.generate_table(
            gemini_model, df_products_mm, output_schema={"image_description": "STRING"}
        )
        
        df_products_mm = df_products_mm[
            [
                "product_id",
                "product_name",
                "brand",
                "category",
                "subcategory",
                "animal_type",
                "search_keywords",
                "price",
                "description",
                "inventory_level",
                "supplier_id",
                "average_rating",
                "image",
                "image_description",
            ]
        ]

2.  To view the contents of the `image_description` column, paste the following into the query editor, and then click play\_circle **Run** :
    
        SELECT product_name, image_description
        FROM cymbal_pets.products_mm;
    
    The results look similar to the following:
    
    ```console
    +--------------------------------+-------------------------------------+
    | product_name                   | image_description                   |
    +--------------------------------+-------------------------------------+
    |  AquaClear Aquarium Background | The image shows a colorful coral    |
    |                                | reef backdrop. The background is a  |
    |                                | blue ocean with a bright light...   |
    |                                |                                     |
    |                                |                                     |
    +--------------------------------+-------------------------------------+
    |  AquaClear Aquarium            | The image shows a long, clear       |
    |  Gravel Vacuum                 | plastic tube with a green hose      |
    |                                | attached to one end. The tube...    |
    |                                |                                     |
    |                                |                                     |
    +--------------------------------+-------------------------------------+
    | ...                            | ...                                 |
    +--------------------------------+-------------------------------------+
    ```

3.  To update the `animal_type` , `search_keywords` , and `subcategory` columns with generated data, choose one of the following options:
    
    ### SQL
    
    Paste the following into the query editor, and then click play\_circle **Run** :
    
        UPDATE cymbal_pets.products_mm t
        SET
        animal_type = r.animal_type,
        search_keywords = SPLIT(r.search_keywords, ','),
        subcategory = r.subcategory
        FROM (
        SELECT
          product_id,
          g.* EXCEPT(full_response, status)
        FROM bqml_tutorial.products_mm,
        UNNEST([AI.GENERATE(
          ('For the image and description of a pet product, concisely generate the following metadata: 1) animal_type and 2) 5 SEO search keywords (comma separated), and 3) product subcategory. ', image, description),
          endpoint => 'gemini-3.5-flash',
          output_schema => 'animal_type STRING, search_keywords STRING, subcategory STRING'
        )]) AS g
        ) r
        WHERE t.product_id = r.product_id;
    
    You receive a confirmation message similar to the following: `This statement modified 205 rows in products_mm.`
    
    ### BigQuery DataFrames
    
    Before trying this sample, follow the BigQuery DataFrames setup instructions in the [BigQuery quickstart using BigQuery DataFrames](https://docs.cloud.google.com/bigquery/docs/dataframes-quickstart) . For more information, see the [BigQuery DataFrames reference documentation](https://docs.cloud.google.com/python/docs/reference/bigframes/latest) .
    
    To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up ADC for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .
    
        df_prompt = bbq.obj.get_access_url(df_products_mm["image"], "R").to_frame()
        df_prompt[
            "prompt0"
        ] = "For the image of a pet product, concisely generate the following metadata: 1) animal_type and 2) 5 SEO search keywords, and 3) product subcategory."
        
        df_products_mm["prompt"] = bbq.struct(df_prompt[["prompt0", "image"]])
        
        df_products_mm = df_products_mm.drop(
            columns=["animal_type", "search_keywords", "subcategory"]
        )
        df_products_mm = bbq.ai.generate_table(
            gemini_model,
            df_products_mm,
            output_schema="animal_type STRING, search_keywords ARRAY<STRING>, subcategory STRING",
        )
    
        df_prompt = bbq.obj.get_access_url(df_products_mm["image"], "R").to_frame()
        df_prompt[
            "prompt0"
        ] = "For the image of a pet product, concisely generate the following metadata: 1) animal_type and 2) 5 SEO search keywords, and 3) product subcategory."
        
        df_products_mm["prompt"] = bbq.struct(df_prompt[["prompt0", "image"]])
        
        df_products_mm = df_products_mm.drop(
            columns=["animal_type", "search_keywords", "subcategory"]
        )
        df_products_mm = bbq.ai.generate_table(
            gemini_model,
            df_products_mm,
            output_schema="animal_type STRING, search_keywords ARRAY<STRING>, subcategory STRING",
        )

4.  To view the generated data, choose one of the following options:
    
    ### SQL
    
    Paste the following into the query editor, and then click play\_circle **Run** :
    
        SELECT
        product_name,
        image_description,
        animal_type,
        search_keywords,
        subcategory,
        FROM cymbal_pets.products_mm;
    
    ### BigQuery DataFrames
    
    Before trying this sample, follow the BigQuery DataFrames setup instructions in the [BigQuery quickstart using BigQuery DataFrames](https://docs.cloud.google.com/bigquery/docs/dataframes-quickstart) . For more information, see the [BigQuery DataFrames reference documentation](https://docs.cloud.google.com/python/docs/reference/bigframes/latest) .
    
    To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up ADC for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .
    
        df_products_mm[
            [
                "product_name",
                "image_description",
                "animal_type",
                "search_keywords",
                "subcategory",
            ]
        ]
    
        df_products_mm[
            [
                "product_name",
                "image_description",
                "animal_type",
                "search_keywords",
                "subcategory",
            ]
        ]
    
    The results look similar to the following:
    
    ```console
    +--------------------------------+-------------------------------------+-------------+------------------------+------------------+
    | product_name                   | image_description                   | animal_type | search_keywords        | subcategory      |
    +--------------------------------+-------------------------------------+-------------+------------------------+------------------+
    |  AquaClear Aquarium Background | The image shows a colorful coral    | fish        | aquarium background    | aquarium decor   |
    |                                | reef backdrop. The background is a  |             | fish tank backdrop     |                  |
    |                                | blue ocean with a bright light...   |             | coral reef decor       |                  |
    |                                |                                     |             | underwater scenery     |                  |
    |                                |                                     |             | aquarium decoration    |                  |
    +--------------------------------+-------------------------------------+-------------+------------------------+------------------+
    |  AquaClear Aquarium            | The image shows a long, clear       | fish        | aquarium gravel vacuum | aquarium         |
    |  Gravel Vacuum                 | plastic tube with a green hose      |             | aquarium cleaning      | cleaning         |
    |                                | attached to one end. The tube...    |             | aquarium maintenance   |                  |
    |                                |                                     |             | fish tank cleaning     |                  |
    |                                |                                     |             | gravel siphon          |                  |
    +--------------------------------+-------------------------------------+-------------+------------------------+------------------+
    | ...                            | ...                                 | ...         |  ...                   | ...              |
    +--------------------------------+-------------------------------------+-------------+------------------------+------------------+
    ```

5.  To generate a description of each product brand and a count of the number of products from that brand, choose one of the following options:
    
    ### SQL
    
    Paste the following into the query editor, and then click play\_circle **Run** :
    
        SELECT
        brand,
        COUNT(*) AS cnt,
        AI.GENERATE(('Use the images and text to give one concise brand description ',
                    'for a website brand page. Return the description only.',
                      ARRAY_AGG(image LIMIT 10), ARRAY_AGG(description), ARRAY_AGG(category),
                      ARRAY_AGG(subcategory)),
                    endpoint => 'gemini-2.5-pro').result AS brand_description
        FROM
        cymbal_pets.products_mm
        GROUP BY brand
        ORDER BY cnt DESC;
    
    ### BigQuery DataFrames
    
    Before trying this sample, follow the BigQuery DataFrames setup instructions in the [BigQuery quickstart using BigQuery DataFrames](https://docs.cloud.google.com/bigquery/docs/dataframes-quickstart) . For more information, see the [BigQuery DataFrames reference documentation](https://docs.cloud.google.com/python/docs/reference/bigframes/latest) .
    
    To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up ADC for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .
    
        df_agg = df_products_mm[
            ["image", "description", "category", "subcategory", "brand"]
        ]
        df_agg["image"] = bbq.obj.get_access_url(df_products_mm["image"], "R")
        df_agg = bbq.array_agg(df_agg.groupby(by=["brand"]))
        
        df_agg["cnt"] = bbq.array_length(df_agg["image"])
        
        df_prompt = df_agg[["image", "description", "category", "subcategory"]]
        df_prompt[
            "prompt0"
        ] = "Use the images and text to give one concise brand description for a website brand page. Return the description only. "
        
        df_agg["prompt"] = bbq.struct(
            df_prompt[["prompt0", "image", "description", "category", "subcategory"]]
        )
        
        df_agg = df_agg.reset_index()
        
        df_agg = bbq.ai.generate_table(
            gemini_model, df_agg, output_schema={"brand_description": "STRING"}
        )
        df_agg[["brand", "brand_description", "cnt"]]
    
        df_agg = df_products_mm[
            ["image", "description", "category", "subcategory", "brand"]
        ]
        df_agg["image"] = bbq.obj.get_access_url(df_products_mm["image"], "R")
        df_agg = bbq.array_agg(df_agg.groupby(by=["brand"]))
        
        df_agg["cnt"] = bbq.array_length(df_agg["image"])
        
        df_prompt = df_agg[["image", "description", "category", "subcategory"]]
        df_prompt[
            "prompt0"
        ] = "Use the images and text to give one concise brand description for a website brand page. Return the description only. "
        
        df_agg["prompt"] = bbq.struct(
            df_prompt[["prompt0", "image", "description", "category", "subcategory"]]
        )
        
        df_agg = df_agg.reset_index()
        
        df_agg = bbq.ai.generate_table(
            gemini_model, df_agg, output_schema={"brand_description": "STRING"}
        )
        df_agg[["brand", "brand_description", "cnt"]]
    
    The results look similar to the following:
    
    ```console
    +--------------+-------------------------------------+-----+
    | brand        | brand_description                   | cnt |
    +--------------+-------------------------------------+-----+
    |  AquaClear   | AquaClear is a brand of aquarium    | 33  |
    |              | and pond care products that offer   |     |
    |              | a wide range of solutions for...    |     |
    +--------------+-------------------------------------+-----+
    |  Ocean       | Ocean Bites is a brand of cat food  | 28  |
    |  Bites       | that offers a variety of recipes    |     |
    |              | and formulas to meet the specific.. |     |
    +--------------+-------------------------------------+-----+
    |  ...         | ...                                 |...  |
    +--------------+-------------------------------------+-----+
    ```

## Generate embeddings and perform a vector search

Generate embeddings from image data, and then use the embeddings to return similar images by using [vector search](https://docs.cloud.google.com/bigquery/docs/vector-search-intro) .

In a production scenario, we recommend creating a [vector index](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_vector_index_statement) before running a vector search. A vector index lets you perform the vector search more quickly, and it returns more approximate results, but recall is reduced.

To create the embeddings and perform a vector search, follow these steps:

1.  To create the `products_embeddings` table, choose one of the following options:
    
    ### SQL
    
    Paste the following into the query editor, and then click play\_circle **Run** :
    
        CREATE OR REPLACE TABLE cymbal_pets.products_embedding
        AS (
        SELECT
          product_id,
          AI.EMBED(image, endpoint => 'gemini-embedding-2').result AS embedding,
          image
        FROM cymbal_pets.products_mm
        );
    
    You receive a confirmation message similar to the following: `This statement created a new table named products_embedding.`
    
    ### BigQuery DataFrames
    
    Before trying this sample, follow the BigQuery DataFrames setup instructions in the [BigQuery quickstart using BigQuery DataFrames](https://docs.cloud.google.com/bigquery/docs/dataframes-quickstart) . For more information, see the [BigQuery DataFrames reference documentation](https://docs.cloud.google.com/python/docs/reference/bigframes/latest) .
    
    To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up ADC for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .
    
        df_products_mm["content"] = bbq.obj.get_access_url(df_products_mm["image"], "R")
        df_embed = bbq.ai.generate_embedding(
            embedding_model, df_products_mm[["content", "product_id"]]
        )
        
        df_embed.to_gbq("cymbal_pets.products_embedding", if_exists="replace")
    
        df_products_mm["content"] = bbq.obj.get_access_url(df_products_mm["image"], "R")
        df_embed = bbq.ai.generate_embedding(
            embedding_model, df_products_mm[["content", "product_id"]]
        )
        
        df_embed.to_gbq("cymbal_pets.products_embedding", if_exists="replace")

2.  To perform a vector search that returns product images that are similar to the given input image, choose one of the following options:
    
    ### SQL
    
    Paste the following into the query editor, and then click play\_circle **Run** :
    
        SELECT *
        FROM
        VECTOR_SEARCH(
          TABLE cymbal_pets.products_embedding,
          'embedding',
          query_value => AI.EMBED(
                          OBJ.MAKE_REF('gs://cloud-samples-data/bigquery/tutorials/cymbal-pets/images/cozy-naps-cat-scratching-post-with-condo.png'),
                          endpoint => 'gemini-embedding-2').result);
    
    ### BigQuery DataFrames
    
    Before trying this sample, follow the BigQuery DataFrames setup instructions in the [BigQuery quickstart using BigQuery DataFrames](https://docs.cloud.google.com/bigquery/docs/dataframes-quickstart) . For more information, see the [BigQuery DataFrames reference documentation](https://docs.cloud.google.com/python/docs/reference/bigframes/latest) .
    
    To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up ADC for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .
    
        df_image = bpd.DataFrame(
            {
                "uri": [
                    "gs://cloud-samples-data/bigquery/tutorials/cymbal-pets/images/cozy-naps-cat-scratching-post-with-condo.png"
                ]
            }
        ).cache()
        df_image["image"] = bbq.obj.make_ref(df_image["uri"], "us.cymbal_conn")
        df_search = bbq.ai.generate_embedding(
            embedding_model,
            bbq.obj.get_access_url(bbq.obj.fetch_metadata(df_image["image"]), "R"),
        )
        
        search_result = bbq.vector_search(
            "cymbal_pets.products_embedding", "embedding", df_search["embedding"]
        )
        search_result
    
        df_image = bpd.DataFrame(
            {
                "uri": [
                    "gs://cloud-samples-data/bigquery/tutorials/cymbal-pets/images/cozy-naps-cat-scratching-post-with-condo.png"
                ]
            }
        ).cache()
        df_image["image"] = bbq.obj.make_ref(df_image["uri"], "us.cymbal_conn")
        df_search = bbq.ai.generate_embedding(
            embedding_model,
            bbq.obj.get_access_url(bbq.obj.fetch_metadata(df_image["image"]), "R"),
        )
        
        search_result = bbq.vector_search(
            "cymbal_pets.products_embedding", "embedding", df_search["embedding"]
        )
        search_result
    
    The results look similar to the following:
    
    ```console
    +-----------------+-----------------+----------------+----------------------------------------------+--------------------+-------------------------------+------------------------------------------------+----------------+
    | query.embedding | base.product_id | base.embedding | base.image.uri                               | base.image.version | base.image.authorizer         | base.image.details                             | distance       |
    +-----------------+-----------------+----------------+----------------------------------------------+--------------------+-------------------------------+------------------------------------------------+----------------+
    | -0.0112330541   | 181             | -0.0112330541  | gs://cloud-samples-data/bigquery/            | 12345678910        | myproject.region.myconnection | {"gcs_metadata":{"content_type":               | 0.0            |
    | 0.0142525584    |                 |  0.0142525584  | tutorials/cymbal-pets/images/                |                    |                               | "image/png","md5_hash":"21234567hst16555w60j", |                |
    | 0.0135886827    |                 |  0.0135886827  | cozy-naps-cat-scratching-post-with-condo.png |                    |                               | "size":828318,"updated":1742492688982000}}     |                |
    | 0.0149955815    |                 |  0.0149955815  |                                              |                    |                               |                                                |                |
    | ...             |                 |  ...           |                                              |                    |                               |                                                |                |
    |                 |                 |                |                                              |                    |                               |                                                |                |
    |                 |                 |                |                                              |                    |                               |                                                |                |
    +-----------------+-----------------+----------------+----------------------------------------------+--------------------+-------------------------------+------------------------------------------------+----------------+
    | -0.0112330541   | 187             | -0.0190353896  | gs://cloud-samples-data/bigquery/            | 23456789101        | myproject.region.myconnection | {"gcs_metadata":{"content_type":               | 0.4216330832.. |
    | 0.0142525584    |                 |  0.0116206668  | tutorials/cymbal-pets/images/                |                    |                               | "image/png","md5_hash":"7328728fhakd9937djo4", |                |
    | 0.0135886827    |                 |  0.0136198215  | cozy-naps-cat-scratching-post-with-bed.png   |                    |                               | "size":860113,"updated":1742492688774000}}     |                |
    | 0.0149955815    |                 |  0.0173457414  |                                              |                    |                               |                                                |                |
    | ...             |                 |  ...           |                                              |                    |                               |                                                |                |
    |                 |                 |                |                                              |                    |                               |                                                |                |
    |                 |                 |                |                                              |                    |                               |                                                |                |
    +-----------------+-----------------+----------------+----------------------------------------------+--------------------+-------------------------------+------------------------------------------------+----------------+
    | ...             | ...             | ...            | ...                                          | ...                | ...                           | ...                                            | ...            |
    +-----------------+-----------------+----------------+----------------------------------------------+--------------------+-------------------------------+------------------------------------------------+----------------+
    ```

## Process ordered multimodal data using arrays of `ObjectRef` values

This section shows you how to summarize user manuals by processing ordered multimodal data using arrays of `ObjectRef` values. BigQuery can analyze multiple unstructured files simultaneously using arrays.

You complete the following tasks:

1.  Create the `product_manuals` table so that it contains both a PDF file for the `Crittercuisine Pro 5000` product manual, and PDF files for each page of that manual.

2.  Create a table that maps the manual to its chunks. The complete manual and the manual pages are each stored in an `ObjectRef` column.

3.  Analyze an array of `ObjectRef` values together to return a single generated value.

4.  Analyze an array of `ObjectRef` values separately and return a generated value for each array value.

To process ordered multimodal data using `ObjectRef` values, follow these steps:

1.  To create the `product_manuals` table, choose one of the following options:
    
    ### SQL
    
    Paste the following into the query editor, and then click play\_circle **Run** :
    
        CREATE OR REPLACE EXTERNAL TABLE `cymbal_pets.product_manuals`
        WITH CONNECTION `us.cymbal_conn`
        OPTIONS (
          object_metadata = 'SIMPLE',
          uris = [
              'gs://cloud-samples-data/bigquery/tutorials/cymbal-pets/documents/*.pdf',
              'gs://cloud-samples-data/bigquery/tutorials/cymbal-pets/document_chunks/*.pdf']);
    
    You receive a confirmation message similar to the following: `This statement created a new table named product_manuals.`
    
    ### BigQuery DataFrames
    
    Before trying this sample, follow the BigQuery DataFrames setup instructions in the [BigQuery quickstart using BigQuery DataFrames](https://docs.cloud.google.com/bigquery/docs/dataframes-quickstart) . For more information, see the [BigQuery DataFrames reference documentation](https://docs.cloud.google.com/python/docs/reference/bigframes/latest) .
    
    To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up ADC for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .
    
        bbq.create_external_table(
            "cymbal_pets.product_manuals_all",
            replace=True,
            connection_name="us.cymbal_conn",
            options={
                "object_metadata": "SIMPLE",
                "uris": [
                    "gs://cloud-samples-data/bigquery/tutorials/cymbal-pets/documents/*.pdf",
                    "gs://cloud-samples-data/bigquery/tutorials/cymbal-pets/document_chunks/*.pdf",
                ],
            },
        )
    
        bbq.create_external_table(
            "cymbal_pets.product_manuals_all",
            replace=True,
            connection_name="us.cymbal_conn",
            options={
                "object_metadata": "SIMPLE",
                "uris": [
                    "gs://cloud-samples-data/bigquery/tutorials/cymbal-pets/documents/*.pdf",
                    "gs://cloud-samples-data/bigquery/tutorials/cymbal-pets/document_chunks/*.pdf",
                ],
            },
        )

2.  To write PDF data to the `map_manual_to_chunks` table, choose one of the following options:
    
    ### SQL
    
    Paste the following into the query editor, and then click play\_circle **Run** :
    
        -- Extract the file and chunks into a single table.
        -- Store the chunks in the chunks column as array of ObjectRefs (ordered by page number)
        CREATE OR REPLACE TABLE cymbal_pets.map_manual_to_chunks
        AS
        SELECT ARRAY_AGG(m1.ref)[0] manual, ARRAY_AGG(m2.ref ORDER BY m2.ref.uri) chunks
        FROM cymbal_pets.product_manuals m1
        JOIN cymbal_pets.product_manuals m2
        ON
          REGEXP_EXTRACT(m1.uri, r'.*/([^.]*).[^/]+')
          = REGEXP_EXTRACT(m2.uri, r'.*/([^.]*)_page[0-9]+.[^/]+')
        GROUP BY m1.uri;
    
    You receive a confirmation message similar to the following: `This statement created a new table named map_manual_to_chunks.`
    
    ### BigQuery DataFrames
    
    Before trying this sample, follow the BigQuery DataFrames setup instructions in the [BigQuery quickstart using BigQuery DataFrames](https://docs.cloud.google.com/bigquery/docs/dataframes-quickstart) . For more information, see the [BigQuery DataFrames reference documentation](https://docs.cloud.google.com/python/docs/reference/bigframes/latest) .
    
    To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up ADC for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .
    
        df1 = bpd.read_gbq("SELECT * FROM cymbal_pets.product_manuals_all").sort_values(
            "uri"
        )
        df2 = df1.copy()
        df1["name"] = df1["uri"].str.extract(r".*/([^.]*).[^/]+")
        df2["name"] = df2["uri"].str.extract(r".*/([^.]*)_page[0-9]+.[^/]+")
        df_manuals_all = df1.merge(df2, on="name")
        df_manuals_agg = (
            bbq.array_agg(df_manuals_all[["ref_x", "uri_x"]].groupby("uri_x"))["ref_x"]
            .str[0]
            .to_frame()
        )
        df_manuals_agg["chunks"] = bbq.array_agg(
            df_manuals_all[["ref_y", "uri_x"]].groupby("uri_x")
        )["ref_y"]
    
        df1 = bpd.read_gbq("SELECT * FROM cymbal_pets.product_manuals_all").sort_values(
            "uri"
        )
        df2 = df1.copy()
        df1["name"] = df1["uri"].str.extract(r".*/([^.]*).[^/]+")
        df2["name"] = df2["uri"].str.extract(r".*/([^.]*)_page[0-9]+.[^/]+")
        df_manuals_all = df1.merge(df2, on="name")
        df_manuals_agg = (
            bbq.array_agg(df_manuals_all[["ref_x", "uri_x"]].groupby("uri_x"))["ref_x"]
            .str[0]
            .to_frame()
        )
        df_manuals_agg["chunks"] = bbq.array_agg(
            df_manuals_all[["ref_y", "uri_x"]].groupby("uri_x")
        )["ref_y"]

3.  To view the PDF data in the `map_manual_to_chunks` table, choose one of the following options:
    
    ### SQL
    
    Paste the following into the query editor, and then click play\_circle **Run** :
    
        SELECT *
        FROM cymbal_pets.map_manual_to_chunks;
    
    ### BigQuery DataFrames
    
    Before trying this sample, follow the BigQuery DataFrames setup instructions in the [BigQuery quickstart using BigQuery DataFrames](https://docs.cloud.google.com/bigquery/docs/dataframes-quickstart) . For more information, see the [BigQuery DataFrames reference documentation](https://docs.cloud.google.com/python/docs/reference/bigframes/latest) .
    
    To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up ADC for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .
    
        df_manuals_agg
    
        df_manuals_agg
    
    The results look similar to the following:
    
    ```console
    +-------------------------------------+--------------------------------+-----------------------------------+------------------------------------------------------+-------------------------------------------+---------------------------------+------------------------------------+-------------------------------------------------------+
    | manual.uri                          | manual.version                 | manual.authorizer                 | manual.details                                       | chunks.uri                                | chunks.version                  | chunks.authorizer                  | chunks.details                                        |
    +-------------------------------------+--------------------------------+-----------------------------------+------------------------------------------------------+-------------------------------------------+---------------------------------+------------------------------------+-------------------------------------------------------+
    | gs://cloud-samples-data/bigquery/   | 1742492785900455               | myproject.region.myconnection     | {"gcs_metadata":{"content_type":"application/pef",   | gs://cloud-samples-data/bigquery/         | 1745875761227129                | myproject.region.myconnection      | {"gcs_metadata":{"content_type":"application/pdf",    |
    | tutorials/cymbal-pets/documents/    |                                |                                   | "md5_hash":"c9032b037693d15a33210d638c763d0e",       | tutorials/cymbal-pets/documents/          |                                 |                                    | "md5_hash":"5a1116cce4978ec1b094d8e8b49a1d7c",        |
    | crittercuisine_5000_user_manual.pdf |                                |                                   | "size":566105,"updated":1742492785941000}}           | crittercuisine_5000_user_manual_page1.pdf |                                 |                                    | "size":504583,"updated":1745875761266000}}            |
    |                                     |                                |                                   |                                                      +-------------------------------------------+---------------------------------+------------------------------------+-------------------------------------------------------+
    |                                     |                                |                                   |                                                      | crittercuisine_5000_user_manual_page1.pdf | 1745875760613874                | myproject.region.myconnection      | {"gcs_metadata":{"content_type":"application/pdf",    |
    |                                     |                                |                                   |                                                      | tutorials/cymbal-pets/documents/          |                                 |                                    | "md5_hash":"94d03ec65d28b173bc87eac7e587b325",        |
    |                                     |                                |                                   |                                                      | crittercuisine_5000_user_manual_page2.pdf |                                 |                                    | "size":94622,"updated":1745875760649000}}             |
    |                                     |                                |                                   |                                                      +-------------------------------------------+---------------------------------+------------------------------------+-------------------------------------------------------+
    |                                     |                                |                                   |                                                      | ...                                       | ...                             |  ...                               | ...                                                   |
    +-------------------------------------+--------------------------------+-----------------------------------+------------------------------------------------------+-------------------------------------------+---------------------------------+------------------------------------+-------------------------------------------------------+
    ```

4.  To generate a single response from a Gemini model based on the analysis of an array of `ObjectRef` values, choose one of the following options:
    
    ### SQL
    
    Paste the following into the query editor, and then click play\_circle **Run** :
    
        SELECT
        AI.GENERATE((
          '''Can you provide a page by page summary for the first 3 pages of the attached manual?
          Only write one line for each page. The pages are provided in serial order''',
          chunks),
          endpoint => 'gemini-3.5-flash').result AS Response,
        FROM cymbal_pets.map_manual_to_chunks;
    
    ### BigQuery DataFrames
    
    Before trying this sample, follow the BigQuery DataFrames setup instructions in the [BigQuery quickstart using BigQuery DataFrames](https://docs.cloud.google.com/bigquery/docs/dataframes-quickstart) . For more information, see the [BigQuery DataFrames reference documentation](https://docs.cloud.google.com/python/docs/reference/bigframes/latest) .
    
    To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up ADC for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .
    
        df_manuals_agg["chunks_url"] = bbq.array_agg(
            bbq.obj.get_access_url(df_manuals_agg.explode("chunks")["chunks"], "R").groupby(
                "uri_x"
            )
        )
        df_manuals_agg[
            "prompt0"
        ] = "Can you provide a page by page summary for the first 3 pages of the attached manual? Only write one line for each page. The pages are provided in serial order"
        df_manuals_agg["prompt"] = bbq.struct(df_manuals_agg[["prompt0", "chunks_url"]])
        
        result = bbq.ai.generate_text(gemini_model, df_manuals_agg["prompt"])["result"]
        result
    
        df_manuals_agg["chunks_url"] = bbq.array_agg(
            bbq.obj.get_access_url(df_manuals_agg.explode("chunks")["chunks"], "R").groupby(
                "uri_x"
            )
        )
        df_manuals_agg[
            "prompt0"
        ] = "Can you provide a page by page summary for the first 3 pages of the attached manual? Only write one line for each page. The pages are provided in serial order"
        df_manuals_agg["prompt"] = bbq.struct(df_manuals_agg[["prompt0", "chunks_url"]])
        
        result = bbq.ai.generate_text(gemini_model, df_manuals_agg["prompt"])["result"]
        result
    
    The results look similar to the following:
    
    ```console
    +---------------------------------------------------------------------------+
    | Response                                                                  |
    +---------------------------------------------------------------------------+
    | Here is a one-line summary for each of the first 3 pages:                 |
    |                                                                           |
    | Page 1 introduces the CritterCuisine Pro 5000 automatic pet feeder and    |
    | presents the initial part of the manual's Table of Contents.              |
    | Page 2 lists the items included with the feeder and details important     |
    | safety precautions for its use.                                           |
    | Page 3 describes the feeder's key features, provides assembly and initial |
    | setup instructions, and begins the programming guide with clock setting.  |
    +---------------------------------------------------------------------------+
    ```

5.  To generate multiple responses from a Gemini model based on the analysis of an array of `ObjectRef` values, choose one of the following options:
    
    ### SQL
    
    Paste the following into the query editor, and then click play\_circle **Run** :
    
        WITH results AS (
        SELECT
          AI.GENERATE((
            '''Can you provide a page by page summary for the first 3 pages of the attached manual?
            Only write one line for each page. The pages are provided in serial order''',
            chunks),
            endpoint => 'gemini-3.5-flash',
            output_schema =>  'page1_summary STRING, page2_summary STRING, page3_summary STRING').*
        FROM cymbal_pets.map_manual_to_chunks)
        SELECT page1_summary, page2_summary, page3_summary
        FROM results;
    
    ### BigQuery DataFrames
    
    Before trying this sample, follow the BigQuery DataFrames setup instructions in the [BigQuery quickstart using BigQuery DataFrames](https://docs.cloud.google.com/bigquery/docs/dataframes-quickstart) . For more information, see the [BigQuery DataFrames reference documentation](https://docs.cloud.google.com/python/docs/reference/bigframes/latest) .
    
    To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up ADC for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .
    
        result = bbq.ai.generate_table(
            gemini_model,
            df_manuals_agg["prompt"],
            output_schema={
                "page1_summary": "STRING",
                "page2_summary": "STRING",
                "page3_summary": "STRING",
            },
        )[["page1_summary", "page2_summary", "page3_summary"]]
        result
    
        result = bbq.ai.generate_table(
            gemini_model,
            df_manuals_agg["prompt"],
            output_schema={
                "page1_summary": "STRING",
                "page2_summary": "STRING",
                "page3_summary": "STRING",
            },
        )[["page1_summary", "page2_summary", "page3_summary"]]
        result
    
    The results look similar to the following:
    
    ```console
    +-----------------------------------------------+-------------------------------------------+----------------------------------------------------+
    | page1_summary                                 | page2_summary                             | page3_summary                                      |
    +-----------------------------------------------+-------------------------------------------+----------------------------------------------------+
    | This manual provides an overview of the       | This section explains how to program      | This page covers connecting the feeder to Wi-Fi    |
    | CritterCuisine Pro 5000 automatic pet feeder, | the feeder's clock, set feeding           | using the CritterCuisine Connect app,  remote      |
    | including its features, safety precautions,   | schedules, copy and delete meal settings, | feeding, managing feeding schedules, viewing       |
    | assembly instructions, and initial setup.     | manually feed your pet, record            | feeding logs, receiving low food alerts,           |
    |                                               | a voice message, and understand           | updating firmware, creating multiple pet profiles, |
    |                                               | the low food level indicator.             | sharing access with other users, and cleaning      |
    |                                               |                                           | and maintaining the feeder.                        |
    +-----------------------------------------------+-------------------------------------------+----------------------------------------------------+
    ```

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

6.  For the `cymbal_conn` connection, click more\_vert **Open actions \> Delete** .

7.  In the **Delete connection** dialog, enter `delete` , and then click **Delete** to confirm.

## What's next

  - For more information on working with multimodal data, see [Analyze multimodal data in BigQuery](https://docs.cloud.google.com/bigquery/docs/analyze-multimodal-data) .
  - For more information on `ObjectRef` values, see [Work with ObjectRef values](https://docs.cloud.google.com/bigquery/docs/work-with-objectref) .
  - To learn how to analyze multimodal data with SQL and the `OBJ.LIST` function, see [Analyze multimodal data with SQL](https://docs.cloud.google.com/bigquery/docs/multimodal-sql-object-list-tutorial) .
